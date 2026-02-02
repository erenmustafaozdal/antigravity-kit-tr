# 1. Şelaleleri Ortadan Kaldırma (Eliminating Waterfalls)

> **Etki:** KRİTİK
> **Odak:** Şelaleler (waterfalls) performansın 1 numaralı katilidir. Her ardışık await tam ağ gecikmesi ekler. Bunları ortadan kaldırmak en büyük kazançları sağlar.

---

## Genel Bakış

Bu bölüm, şelaleleri ortadan kaldırmaya odaklanan **5 kural** içerir.

---

## Kural 1.1: Await'i Gerekene Kadar Ertele

**Etki:** YÜKSEK  
**Etiketler:** async, await, conditional, optimization  

## Await'i Gerekene Kadar Ertele

`await` işlemlerini yalnızca gerçekten kullanıldıkları dallara taşıyın, böylece onlara ihtiyaç duymayan kod yollarını bloklamaktan kaçının.

**Yanlış (her iki dalı da bloklar):**

```typescript
async function handleRequest(userId: string, skipProcessing: boolean) {
  const userData = await fetchUserData(userId)
  
  if (skipProcessing) {
    // Hemen dönüyor ama yine de userData'yı bekledi
    return { skipped: true }
  }
  
  // Yalnızca bu dal userData kullanıyor
  return processUserData(userData)
}
```

**Doğru (yalnızca gerektiğinde bloklar):**

```typescript
async function handleRequest(userId: string, skipProcessing: boolean) {
  if (skipProcessing) {
    // Beklemeden hemen döner
    return { skipped: true }
  }
  
  // Yalnızca gerektiğinde çek
  const userData = await fetchUserData(userId)
  return processUserData(userData)
}
```

**Başka bir örnek (erken dönüş optimizasyonu):**

```typescript
// Yanlış: her zaman izinleri çeker
async function updateResource(resourceId: string, userId: string) {
  const permissions = await fetchPermissions(userId)
  const resource = await getResource(resourceId)
  
  if (!resource) {
    return { error: 'Not found' }
  }
  
  if (!permissions.canEdit) {
    return { error: 'Forbidden' }
  }
  
  return await updateResourceData(resource, permissions)
}

// Doğru: yalnızca gerektiğinde çeker
async function updateResource(resourceId: string, userId: string) {
  const resource = await getResource(resourceId)
  
  if (!resource) {
    return { error: 'Not found' }
  }
  
  const permissions = await fetchPermissions(userId)
  
  if (!permissions.canEdit) {
    return { error: 'Forbidden' }
  }
  
  return await updateResourceData(resource, permissions)
}
```

Bu optimizasyon, atlanan dalın sık kullanıldığı veya ertelenen işlemin pahalı olduğu durumlarda özellikle değerlidir.

---

## Kural 1.2: Bağımlılık Tabanlı Paralelleştirme

**Etki:** KRİTİK  
**Etiketler:** async, parallelization, dependencies, better-all  

## Bağımlılık Tabanlı Paralelleştirme

Kısmi bağımlılıkları olan işlemler için, paralelliği maksimize etmek için `better-all` kullanın. Her görevi en erken olası anda otomatik olarak başlatır.

**Yanlış (profile gereksiz yere config'i bekliyor):**

```typescript
const [user, config] = await Promise.all([
  fetchUser(),
  fetchConfig()
])
const profile = await fetchProfile(user.id)
```

**Doğru (config ve profile paralel çalışır):**

```typescript
import { all } from 'better-all'

const { user, config, profile } = await all({
  async user() { return fetchUser() },
  async config() { return fetchConfig() },
  async profile() {
    return fetchProfile((await this.$.user).id)
  }
})
```

**Ekstra bağımlılık olmadan alternatif:**

Tüm promise'leri önce oluşturabilir ve sonunda `Promise.all()` yapabiliriz.

```typescript
const userPromise = fetchUser()
const profilePromise = userPromise.then(user => fetchProfile(user.id))

const [user, config, profile] = await Promise.all([
  userPromise,
  fetchConfig(),
  profilePromise
])
```

Referans: [https://github.com/shuding/better-all](https://github.com/shuding/better-all)

---

## Kural 1.3: API Route'larında Şelale Zincirlerini Önleyin

**Etki:** KRİTİK  
**Etiketler:** api-routes, server-actions, waterfalls, parallelization  

## API Route'larında Şelale Zincirlerini Önleyin

API route'larında ve Server Action'larda, henüz await etmeseniz bile bağımsız işlemleri hemen başlatın.

**Yanlış (config auth'u bekler, data ikisini de bekler):**

```typescript
export async function GET(request: Request) {
  const session = await auth()
  const config = await fetchConfig()
  const data = await fetchData(session.user.id)
  return Response.json({ data, config })
}
```

**Doğru (auth ve config hemen başlar):**

```typescript
export async function GET(request: Request) {
  const sessionPromise = auth()
  const configPromise = fetchConfig()
  const session = await sessionPromise
  const [config, data] = await Promise.all([
    configPromise,
    fetchData(session.user.id)
  ])
  return Response.json({ data, config })
}
```

Daha karmaşık bağımlılık zincirleri olan işlemler için, paralelliği otomatik olarak maksimize etmek için `better-all` kullanın (Bağımlılık Tabanlı Paralelleştirme'ye bakın).

---

## Kural 1.4: Bağımsız İşlemler İçin Promise.all()

**Etki:** KRİTİK  
**Etiketler:** async, parallelization, promises, waterfalls  

## Bağımsız İşlemler İçin Promise.all()

Async işlemlerin birbirine bağımlılığı olmadığında, `Promise.all()` kullanarak eşzamanlı olarak yürütün.

**Yanlış (ardışık yürütme, 3 tur gidiş-dönüş):**

```typescript
const user = await fetchUser()
const posts = await fetchPosts()
const comments = await fetchComments()
```

**Doğru (paralel yürütme, 1 tur gidiş-dönüş):**

```typescript
const [user, posts, comments] = await Promise.all([
  fetchUser(),
  fetchPosts(),
  fetchComments()
])
```

---

## Kural 1.5: Stratejik Suspense Sınırları

**Etki:** YÜKSEK  
**Etiketler:** async, suspense, streaming, layout-shift  

## Stratejik Suspense Sınırları

Async componentlerde JSX döndürmeden önce veriyi await etmek yerine, Suspense sınırları kullanarak wrapper UI'yi daha hızlı gösterin ve veri yüklenirken bekletin.

**Yanlış (wrapper veri çekme ile bloklanır):**

```tsx
async function Page() {
  const data = await fetchData() // Tüm sayfayı bloklar
  
  return (
    <div>
      <div>Sidebar</div>
      <div>Header</div>
      <div>
        <DataDisplay data={data} />
      </div>
      <div>Footer</div>
    </div>
  )
}
```

Tüm layout, yalnızca orta bölümün ihtiyacı olsa bile veriyi bekler.

**Doğru (wrapper hemen gösterilir, veri akışla gelir):**

```tsx
function Page() {
  return (
    <div>
      <div>Sidebar</div>
      <div>Header</div>
      <div>
        <Suspense fallback={<Skeleton />}>
          <DataDisplay />
        </Suspense>
      </div>
      <div>Footer</div>
    </div>
  )
}

async function DataDisplay() {
  const data = await fetchData() // Yalnızca bu componenti bloklar
  return <div>{data.content}</div>
}
```

Sidebar, Header ve Footer hemen render edilir. Yalnızca DataDisplay veriyi bekler.

**Alternatif (promise'i componentler arasında paylaş):**

```tsx
function Page() {
  // Çekmeyi hemen başlat, ama await etme
  const dataPromise = fetchData()
  
  return (
    <div>
      <div>Sidebar</div>
      <div>Header</div>
      <Suspense fallback={<Skeleton />}>
        <DataDisplay dataPromise={dataPromise} />
        <DataSummary dataPromise={dataPromise} />
      </Suspense>
      <div>Footer</div>
    </div>
  )
}

function DataDisplay({ dataPromise }: { dataPromise: Promise<Data> }) {
  const data = use(dataPromise) // Promise'i açar (unwrap)
  return <div>{data.content}</div>
}

function DataSummary({ dataPromise }: { dataPromise: Promise<Data> }) {
  const data = use(dataPromise) // Aynı promise'i yeniden kullanır
  return <div>{data.summary}</div>
}
```

Her iki component de aynı promise'i paylaşır, bu yüzden yalnızca bir fetch gerçekleşir. Layout hemen render edilir, her iki component birlikte bekler.

**Bu deseni NE ZAMAN KULLANMAYIN:**

- Layout kararları için kritik veriler gerektiğinde (konumlandırmayı etkiler)
- SEO-kritik içerik, sayfa kıvrımının üstünde (above the fold)
- Küçük, hızlı sorgularda suspense yükü buna değmez
- Layout shift'ten (yükleniyor → içerik atlama) kaçınmak istediğinizde

**Takas:** Daha hızlı ilk boyama vs potansiyel layout shift. UX önceliklerinize göre seçin.
