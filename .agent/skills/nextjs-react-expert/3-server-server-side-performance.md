# 3. Sunucu Tarafı Performans (Server-Side Performance)

> **Etki:** YÜKSEK
> **Odak:** Sunucu tarafı rendering ve veri çekmeyi optimize etmek, sunucu tarafı şelaleleri ortadan kaldırır ve yanıt sürelerini azaltır.

---

## Genel Bakış

Bu bölüm, sunucu tarafı performansına odaklanan **7 kural** içerir.

---

## Kural 3.1: Server Action'ları API Route'lar Gibi Kimlik Doğrulayın

**Etki:** KRİTİK  
**Etiketler:** server, server-actions, authentication, security, authorization  

## Server Action'ları API Route'lar Gibi Kimlik Doğrulayın

**Etki: KRİTİK (yetkisiz erişimi önler)**

Server Action'lar (`"use server"` ile işaretlenmiş fonksiyonlar) API route'lar gibi public endpoint olarak açığa çıkar. Her zaman her Server Action'ın **içinde** kimlik doğrulama ve yetkilendirme doğrulaması yapın—Server Action'lar doğrudan çağrılabildiği için yalnızca middleware, layout guard'larına veya sayfa düzeyindeki kontrollere güvenmeyin.

Next.js dokümantasyonu açıkça belirtir: "Server Action'ları public-facing API endpoint'leri gibi aynı güvenlik önlemleriyle ele alın ve kullanıcının bir mutasyon yapmasına izin verilip verilmediğini doğrulayın."

**Yanlış (kimlik doğrulama kontrolü yok):**

```typescript
'use server'

export async function deleteUser(userId: string) {
  // Herkes bunu çağırabilir! Auth kontrolü yok
  await db.user.delete({ where: { id: userId } })
  return { success: true }
}
```

**Doğru (action içinde kimlik doğrulama):**

```typescript
'use server'

import { verifySession } from '@/lib/auth'
import { unauthorized } from '@/lib/errors'

export async function deleteUser(userId: string) {
  // Her zaman action içinde auth kontrolü yapın
  const session = await verifySession()
  
  if (!session) {
    throw unauthorized('Giriş yapılmalı')
  }
  
  // Yetkilendirme kontrolü de yapın
  if (session.user.role !== 'admin' && session.user.id !== userId) {
    throw unauthorized('Diğer kullanıcıları silemezsiniz')
  }
  
  await db.user.delete({ where: { id: userId } })
  return { success: true }
}
```

**Girdi doğrulama ile:**

```typescript
'use server'

import { verifySession } from '@/lib/auth'
import { z } from 'zod'

const updateProfileSchema = z.object({
  userId: z.string().uuid(),
  name: z.string().min(1).max(100),
  email: z.string().email()
})

export async function updateProfile(data: unknown) {
  // Önce girdiyi doğrula
  const validated = updateProfileSchema.parse(data)
  
  // Sonra kimlik doğrulama
  const session = await verifySession()
  if (!session) {
    throw new Error('Yetkisiz')
  }
  
  // Sonra yetkilendirme
  if (session.user.id !== validated.userId) {
    throw new Error('Yalnızca kendi profilinizi güncelleyebilirsiniz')
  }
  
  // Son olarak mutasyonu gerçekleştir
  await db.user.update({
    where: { id: validated.userId },
    data: {
      name: validated.name,
      email: validated.email
    }
  })
  
  return { success: true }
}
```

Referans: [https://nextjs.org/docs/app/guides/authentication](https://nextjs.org/docs/app/guides/authentication)

---

## Kural 3.2: RSC Props'larında Duplicate Serialization'dan Kaçının

**Etki:** DÜŞÜK  
**Etiketler:** server, rsc, serialization, props, client-components  

## RSC Props'larında Duplicate Serialization'dan Kaçının

**Etki: DÜŞÜK (duplicate serialization'dan kaçınarak ağ yükünü azaltır)**

RSC→client serialization, değere göre değil, nesne referansına göre tekilleştirir. Aynı referans = bir kez serialize edilir; yeni referans = tekrar serialize edilir. Dönüşümleri (`.toSorted()`, `.filter()`, `.map()`) sunucuda değil, istemcide yapın.

**Yanlış (dizi kopyalanır):**

```tsx
// RSC: 6 string gönderir (2 dizi × 3 öğe)
<ClientList usernames={usernames} usernamesOrdered={usernames.toSorted()} />
```

**Doğru (3 string gönderir):**

```tsx
// RSC: bir kez gönder
<ClientList usernames={usernames} />

// Client: orada dönüştür
'use client'
const sorted = useMemo(() => [...usernames].sort(), [usernames])
```

**İç içe tekilleştirme davranışı:**

Tekilleştirme recursive çalışır. Etki veri tipine göre değişir:

- `string[]`, `number[]`, `boolean[]`: **YÜKSEK etki** - dizi + tüm primitive'ler tamamen kopyalanır
- `object[]`: **DÜŞÜK etki** - dizi kopyalanır, ama iç içe nesneler referansa göre tekilleştirilir

```tsx
// string[] - her şeyi kopyalar
usernames={['a','b']} sorted={usernames.toSorted()} // 4 string gönderir

// object[] - yalnızca dizi yapısını kopyalar
users={[{id:1},{id:2}]} sorted={users.toSorted()} // 2 dizi + 2 benzersiz nesne gönderir (4 değil)
```

**Tekilleştirmeyi bozan işlemler (yeni referanslar oluşturur):**

- Diziler: `.toSorted()`, `.filter()`, `.map()`, `.slice()`, `[...arr]`
- Nesneler: `{...obj}`, `Object.assign()`, `structuredClone()`, `JSON.parse(JSON.stringify())`

**Daha fazla örnek:**

```tsx
// ❌ Kötü
<C users={users} active={users.filter(u => u.active)} />
<C product={product} productName={product.name} />

// ✅ İyi
<C users={users} />
<C product={product} />
// Filtreleme/destructuring'i istemcide yapın
```

**İstisna:** Dönüşüm pahalıysa veya istemci orijinale ihtiyaç duymuyorsa türetilmiş veriyi gönderin.

---

## Kural 3.3: İstekler Arası LRU Önbellekleme

**Etki:** YÜKSEK  
**Etiketler:** server, cache, lru, cross-request  

## İstekler Arası LRU Önbellekleme

`React.cache()` yalnızca bir istek içinde çalışır. Ardışık istekler arasında paylaşılan veriler için (kullanıcı A butonuna sonra B butonuna tıklar), LRU cache kullanın.

**Uygulama:**

```typescript
import { LRUCache } from 'lru-cache'

const cache = new LRUCache<string, any>({
  max: 1000,
  ttl: 5 * 60 * 1000  // 5 dakika
})

export async function getUser(id: string) {
  const cached = cache.get(id)
  if (cached) return cached

  const user = await db.user.findUnique({ where: { id } })
  cache.set(id, user)
  return user
}

// İstek 1: DB sorgusu, sonuç önbelleğe alındı
// İstek 2: önbellek isabet, DB sorgusu yok
```

Ardışık kullanıcı eylemleri, saniyeler içinde aynı veriye ihtiyaç duyan birden fazla endpoint'e isabet ettiğinde kullanın.

**Vercel'in [Fluid Compute](https://vercel.com/docs/fluid-compute) ile:** LRU önbellekleme özellikle etkilidir çünkü birden fazla eşzamanlı istek aynı fonksiyon instance'ını ve önbelleği paylaşabilir. Bu, önbelleğin Redis gibi harici depolama olmadan istekler arasında kalıcı olduğu anlamına gelir.

**Geleneksel serverless'ta:** Her invocation izole çalışır, bu yüzden process'ler arası önbellekleme için Redis düşünün.

Referans: [https://github.com/isaacs/node-lru-cache](https://github.com/isaacs/node-lru-cache)

---

## Kural 3.4: RSC Sınırlarında Serialization'ı Minimize Edin

**Etki:** YÜKSEK  
**Etiketler:** server, rsc, serialization, props  

## RSC Sınırlarında Serialization'ı Minimize Edin

React Server/Client sınırı tüm nesne özelliklerini string'lere serialize eder ve bunları HTML yanıtına ve sonraki RSC isteklerine gömer. Bu serialize edilmiş veri direkt olarak sayfa ağırlığını ve yükleme süresini etkiler, bu yüzden **boyut çok önemlidir**. Yalnızca istemcinin gerçekten kullandığı alanları gönderin.

**Yanlış (tüm 50 alanı serialize eder):**

```tsx
async function Page() {
  const user = await fetchUser()  // 50 alan
  return <Profile user={user} />
}

'use client'
function Profile({ user }: { user: User }) {
  return <div>{user.name}</div>  // 1 alan kullanır
}
```

**Doğru (yalnızca 1 alanı serialize eder):**

```tsx
async function Page() {
  const user = await fetchUser()
  return <Profile name={user.name} />
}

'use client'
function Profile({ name }: { name: string }) {
  return <div>{name}</div>
}
```

---

## Kural 3.5: Component Composition ile Paralel Veri Çekme

**Etki:** KRİTİK  
**Etiketler:** server, rsc, parallel-fetching, composition  

## Component Composition ile Paralel Veri Çekme

React Server Components bir ağaç içinde sıralı olarak yürütülür. Veri çekmeyi paralel hale getirmek için composition ile yeniden yapılandırın.

**Yanlış (Sidebar, Page'in fetch'ini bekler):**

```tsx
export default async function Page() {
  const header = await fetchHeader()
  return (
    <div>
      <div>{header}</div>
      <Sidebar />
    </div>
  )
}

async function Sidebar() {
  const items = await fetchSidebarItems()
  return <nav>{items.map(renderItem)}</nav>
}
```

**Doğru (ikisi de aynı anda fetch eder):**

```tsx
async function Header() {
  const data = await fetchHeader()
  return <div>{data}</div>
}

async function Sidebar() {
  const items = await fetchSidebarItems()
  return <nav>{items.map(renderItem)}</nav>
}

export default function Page() {
  return (
    <div>
      <Header />
      <Sidebar />
    </div>
  )
}
```

**children prop ile alternatif:**

```tsx
async function Header() {
  const data = await fetchHeader()
  return <div>{data}</div>
}

async function Sidebar() {
  const items = await fetchSidebarItems()
  return <nav>{items.map(renderItem)}</nav>
}

function Layout({ children }: { children: ReactNode }) {
  return (
    <div>
      <Header />
      {children}
    </div>
  )
}

export default function Page() {
  return (
    <Layout>
      <Sidebar />
    </Layout>
  )
}
```

---

## Kural 3.6: React.cache() ile İstek Başına Tekilleştirme

**Etki:** ORTA  
**Etiketler:** server, cache, react-cache, deduplication  

## React.cache() ile İstek Başına Tekilleştirme

Sunucu tarafı istek tekilleştirmesi için `React.cache()` kullanın. Kimlik doğrulama ve veritabanı sorguları en çok fayda görür.

**Kullanım:**

```typescript
import { cache } from 'react'

export const getCurrentUser = cache(async () => {
  const session = await auth()
  if (!session?.user?.id) return null
  return await db.user.findUnique({
    where: { id: session.user.id }
  })
})
```

Tek bir istek içinde, `getCurrentUser()`'a yapılan birden fazla çağrı sorguyu yalnızca bir kez yürütür.

**Argüman olarak inline nesnelerden kaçının:**

`React.cache()` önbellek isabetini belirlemek için shallow equality (`Object.is`) kullanır. Inline nesneler her çağrıda yeni referanslar oluşturur, önbellek isabetini önler.

**Yanlış (her zaman cache miss):**

```typescript
const getUser = cache(async (params: { uid: number }) => {
  return await db.user.findUnique({ where: { id: params.uid } })
})

// Her çağrı yeni nesne oluşturur, asla önbelleği kullanmaz
getUser({ uid: 1 })
getUser({ uid: 1 })  // Cache miss, sorguyu tekrar çalıştırır
```

**Doğru (cache hit):**

```typescript
const getUser = cache(async (uid: number) => {
  return await db.user.findUnique({ where: { id: uid } })
})

// Primitive argümanlar değer eşitliği kullanır
getUser(1)
getUser(1)  // Cache hit, önbelleğe alınmış sonucu döndürür
```

Nesne geçirmek zorundaysanız, aynı referansı geçirin:

```typescript
const params = { uid: 1 }
getUser(params)  // Sorgu çalışır
getUser(params)  // Cache hit (aynı referans)
```

**Next.js'e Özgü Not:**

Next.js'te, `fetch` API'si otomatik olarak istek memoization ile genişletilir. Aynı URL ve seçeneklere sahip istekler otomatik olarak tek bir istek içinde tekilleştirilir, bu yüzden `fetch` çağrıları için `React.cache()`'e ihtiyacınız yoktur. Ancak, `React.cache()` diğer async görevler için hala gereklidir:

- Veritabanı sorguları (Prisma, Drizzle, vb.)
- Ağır hesaplamalar
- Kimlik doğrulama kontrolleri
- Dosya sistemi işlemleri
- Fetch olmayan herhangi bir async iş

Component ağacınız boyunca bu işlemleri tekilleştirmek için `React.cache()` kullan

ın.

Referans: [React.cache documentation](https://react.dev/reference/react/cache)

---

## Kural 3.7: Bloke Etmeyen İşlemler İçin after() Kullanın

**Etki:** ORTA  
**Etiketler:** server, async, logging, analytics, side-effects  

## Bloke Etmeyen İşlemler İçin after() Kullanın

Yanıt gönderildikten sonra yürütülmesi gereken işleri planlamak için Next.js'in `after()` fonksiyonunu kullanın. Bu, logging, analytics ve diğer yan etkilerin yanıtı bloke etmesini önler.

**Yanlış (yanıtı bloklar):**

```tsx
import { logUserAction } from '@/app/utils'

export async function POST(request: Request) {
  // Mutasyonu gerçekleştir
  await updateDatabase(request)
  
  // Logging yanıtı bloklar
  const userAgent = request.headers.get('user-agent') || 'unknown'
  await logUserAction({ userAgent })
  
  return new Response(JSON.stringify({ status: 'success' }), {
    status: 200,
    headers: { 'Content-Type': 'application/json' }
  })
}
```

**Doğru (bloke etmeyen):**

```tsx
import { after } from 'next/server'
import { headers, cookies } from 'next/headers'
import { logUserAction } from '@/app/utils'

export async function POST(request: Request) {
  // Mutasyonu gerçekleştir
  await updateDatabase(request)
  
  // Yanıt gönderildikten sonra logla
  after(async () => {
    const userAgent = (await headers()).get('user-agent') || 'unknown'
    const sessionCookie = (await cookies()).get('session-id')?.value || 'anonymous'
    
    logUserAction({ sessionCookie, userAgent })
  })
  
  return new Response(JSON.stringify({ status: 'success' }), {
    status: 200,
    headers: { 'Content-Type': 'application/json' }
  })
}
```

Yanıt hemen gönderilir, logging arka planda gerçekleşir.

**Yaygın kullanım durumları:**

- Analytics izleme
- Audit logging
- Bildirim gönderme
- Önbellek invalidation
- Temizlik görevleri

**Önemli notlar:**

- `after()` yanıt başarısız olsa veya redirect olsa bile çalışır
- Server Action'larda, Route Handler'larda ve Server Components'ta çalışır

Referans: [https://nextjs.org/docs/app/api-reference/functions/after](https://nextjs.org/docs/app/api-reference/functions/after)
