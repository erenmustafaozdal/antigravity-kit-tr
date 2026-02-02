# 7. JavaScript Performansı (JavaScript Performance)

> **Etki:** DÜŞÜK-ORTA
> **Odak:** Sık kullanılan yollardaki mikro-optimizasyonlar anlamlı iyileştirmelere dönüşebilir.

---

## Genel Bakış

Bu bölüm, JavaScript performansına odaklanan **12 kural** içerir.

---

## Kural 7.1: Layout Thrashing'den Kaçın

**Etki:** ORTA  
**Etiketler:** javascript, dom, css, performance, reflow, layout-thrashing  

## Layout Thrashing'den Kaçının

Stil yazmalarını layout okumalarıyla iç içe geçirmekten kaçının. Stil değişiklikleri arasında bir layout özelliği (örn. `offsetWidth`, `getBoundingClientRect()` veya `getComputedStyle()`) okuduğunuzda, tarayıcı senkron reflow tetiklemeye zorlanır.

**Bu iyi (tarayıcı stil değişikliklerini toplu hale getirir):**
```typescript
function updateElementStyles(element: HTMLElement) {
  // Her satır stili geçersiz kılar ama tarayıcı yeniden hesaplamayı toplar
  element.style.width = '100px'
  element.style.height = '200px'
  element.style.backgroundColor = 'blue'
  element.style.border = '1px solid black'
}
```

**Yanlış (iç içe okuma ve yazmalar reflow'a zorlar):**
```typescript
function layoutThrashing(element: HTMLElement) {
  element.style.width = '100px'
  const width = element.offsetWidth  // Reflow'a zorlar
  element.style.height = '200px'
  const height = element.offsetHeight  // Başka bir reflow'a zorlar
}
```

**Doğru (yazmaları topla, sonra bir kez oku):**
```typescript
function updateElementStyles(element: HTMLElement) {
  // Tüm yazmaları birlikte topla
  element.style.width = '100px'
  element.style.height = '200px'
  element.style.backgroundColor = 'blue'
  element.style.border = '1px solid black'
  
  // Tüm yazmalar bittikten sonra oku (tek reflow)
  const { width, height } = element.getBoundingClientRect()
}
```

**Doğru (okumaları topla, sonra yazmalar):**
```typescript
function avoidThrashing(element: HTMLElement) {
  // Okuma fazı - önce tüm layout sorguları
  const rect1 = element.getBoundingClientRect()
  const offsetWidth = element.offsetWidth
  const offsetHeight = element.offsetHeight
  
  // Yazma fazı - tüm stil değişiklikleri sonra
  element.style.width = '100px'
  element.style.height = '200px'
}
```

**Daha iyi: CSS sınıfları kullanın**
```css
.highlighted-box {
  width: 100px;
  height: 200px;
  background-color: blue;
  border: 1px solid black;
}
```
```typescript
function updateElementStyles(element: HTMLElement) {
  element.classList.add('highlighted-box')
  
  const { width, height } = element.getBoundingClientRect()
}
```

**React örneği:**
```tsx
// Yanlış: layout sorguları ile stil değişikliklerini iç içe geçirme
function Box({ isHighlighted }: { isHighlighted: boolean }) {
  const ref = useRef<HTMLDivElement>(null)
  
  useEffect(() => {
    if (ref.current && isHighlighted) {
      ref.current.style.width = '100px'
      const width = ref.current.offsetWidth // Layout'a zorlar
      ref.current.style.height = '200px'
    }
  }, [isHighlighted])
  
  return <div ref={ref}>İçerik</div>
}

// Doğru: sınıfı değiştir
function Box({ isHighlighted }: { isHighlighted: boolean }) {
  return (
    <div className={isHighlighted ? 'highlighted-box' : ''}>
      İçerik
    </div>
  )
}
```

Mümkün olduğunda inline stillere göre CSS sınıflarını tercih edin. CSS dosyaları tarayıcı tarafından önbelleğe alınır ve sınıflar daha iyi endişelerin ayrılmasını sağlar ve bakımı daha kolaydır.

Layout'a zorlayan işlemler hakkında daha fazla bilgi için [bu gist](https://gist.github.com/paulirish/5d52fb081b3570c81e3a) ve [CSS Triggers](https://csstriggers.com/)'a bakın.

---

## Kural 7.2: Tekrarlanan Aramalar İçin İndeks Map'leri Oluşturun

**Etki:** DÜŞÜK-ORTA  
**Etiketler:** javascript, map, indexing, optimization, performance  

## Tekrarlanan Aramalar İçin İndeks Map'leri Oluşturun

Aynı key ile birden fazla `.find()` çağrısı Map kullanmalıdır.

**Yanlış (arama başına O(n)):**

```typescript
function processOrders(orders: Order[], users: User[]) {
  return orders.map(order => ({
    ...order,
    user: users.find(u => u.id === order.userId)
  }))
}
```

**Doğru (arama başına O(1)):**

```typescript
function processOrders(orders: Order[], users: User[]) {
  const userById = new Map(users.map(u => [u.id, u]))

  return orders.map(order => ({
    ...order,
    user: userById.get(order.userId)
  }))
}
```

Map'i bir kez oluştur (O(n)), sonra tüm aramalar O(1)'dir.
1000 sipariş × 1000 kullanıcı için: 1M işlem → 2K işlem.

---

## Kural 7.3: Döngülerde Özellik Erişimini Önbelleğe Alın

**Etki:** DÜŞÜK-ORTA  
**Etiketler:** javascript, loops, optimization, caching  

## Döngülerde Özellik Erişimini Önbelleğe Alın

Sık kullanılan yollarda nesne özellik aramalarını önbelleğe alın.

**Yanlış (3 arama × N iterasyon):**

```typescript
for (let i = 0; i < arr.length; i++) {
  process(obj.config.settings.value)
}
```

**Doğru (toplam 1 arama):**

```typescript
const value = obj.config.settings.value
const len = arr.length
for (let i = 0; i < len; i++) {
  process(value)
}
```

---

## Kural 7.4: Tekrarlayan Fonksiyon Çağrılarını Önbelleğe Alın

**Etki:** ORTA  
**Etiketler:** javascript, cache, memoization, performance  

## Tekrarlayan Fonksiyon Çağrılarını Önbelleğe Alın

Aynı fonksiyon render sırasında aynı girdilerle tekrar tekrar çağrıldığında, fonksiyon sonuçlarını önbelleğe almak için modül seviyesinde bir Map kullanın.

**Yanlış (gereksiz hesaplama):**

```typescript
function ProjectList({ projects }: { projects: Project[] }) {
  return (
    <div>
      {projects.map(project => {
        // slugify() aynı proje isimleri için 100+ kez çağrılıyor
        const slug = slugify(project.name)
        
        return <ProjectCard key={project.id} slug={slug} />
      })}
    </div>
  )
}
```

**Doğru (önbelleğe alınmış sonuçlar):**

```typescript
// Modül seviyesinde önbellek
const slugifyCache = new Map<string, string>()

function cachedSlugify(text: string): string {
  if (slugifyCache.has(text)) {
    return slugifyCache.get(text)!
  }
  const result = slugify(text)
  slugifyCache.set(text, result)
  return result
}

function ProjectList({ projects }: { projects: Project[] }) {
  return (
    <div>
      {projects.map(project => {
        // Benzersiz proje adı başına yalnızca bir kez hesaplanır
        const slug = cachedSlugify(project.name)
        
        return <ProjectCard key={project.id} slug={slug} />
      })}
    </div>
  )
}
```

**Tek değer fonksiyonlar için daha basit desen:**

```typescript
let isLoggedInCache: boolean | null = null

function isLoggedIn(): boolean {
  if (isLoggedInCache !== null) {
    return isLoggedInCache
  }
  
  isLoggedInCache = document.cookie.includes('auth=')
  return isLoggedInCache
}

// Auth değiştiğinde önbelleği temizle
function onAuthChange() {
  isLoggedInCache = null
}
```

Her yerde çalışsın diye Map kullanın (hook değil): yardımcı programlar, event handler'lar, sadece React componentleri değil.

Referans: [How we made the Vercel Dashboard twice as fast](https://vercel.com/blog/how-we-made-the-vercel-dashboard-twice-as-fast)

---

## Kural 7.5: Storage API Çağrılarını Önbelleğe Alın

**Etki:** DÜŞÜK-ORTA  
**Etiketler:** javascript, localStorage, storage, caching, performance  

## Storage API Çağrılarını Önbelleğe Alın

`localStorage`, `sessionStorage` ve `document.cookie` senkron ve pahalıdır. Okumaları bellekte önbelleğe alın.

**Yanlış (her çağrıda storage'ı okur):**

```typescript
function getTheme() {
  return localStorage.getItem('theme') ?? 'light'
}
// 10 kez çağrılırsa = 10 storage okuması
```

**Doğru (Map önbelleği):**

```typescript
const storageCache = new Map<string, string | null>()

function getLocalStorage(key: string) {
  if (!storageCache.has(key)) {
    storageCache.set(key, localStorage.getItem(key))
  }
  return storageCache.get(key)
}

function setLocalStorage(key: string, value: string) {
  localStorage.setItem(key, value)
  storageCache.set(key, value)  // önbelleği senkronize tut
}
```

Her yerde çalışsın diye Map kullanın (hook değil): yardımcı programlar, event handler'lar, sadece React componentleri değil.

**Cookie önbellekleme:**

```typescript
let cookieCache: Record<string, string> | null = null

function getCookie(name: string) {
  if (!cookieCache) {
    cookieCache = Object.fromEntries(
      document.cookie.split('; ').map(c => c.split('='))
    )
  }
  return cookieCache[name]
}
```

**Önemli (harici değişikliklerden geçersiz kılın):**

Storage harici olarak değişebiliyorsa (başka bir sekme, sunucu tarafı cookie'ler), önbelleği geçersiz kılın:

```typescript
window.addEventListener('storage', (e) => {
  if (e.key) storageCache.delete(e.key)
})

document.addEventListener('visibilitychange', () => {
  if (document.visibilityState === 'visible') {
    storageCache.clear()
  }
})
```

---

## Kural 7.6: Birden Fazla Dizi İterasyonunu Birleştirin

**Etki:** DÜŞÜK-ORTA  
**Etiketler:** javascript, arrays, loops, performance  

## Birden Fazla Dizi İterasyonunu Birleştirin

Birden fazla `.filter()` veya `.map()` çağrısı diziyi birden fazla kez iterate eder. Tek bir döngüde birleştirin.

**Yanlış (3 iterasyon):**

```typescript
const admins = users.filter(u => u.isAdmin)
const testers = users.filter(u => u.isTester)
const inactive = users.filter(u => !u.isActive)
```

**Doğru (1 iterasyon):**

```typescript
const admins: User[] = []
const testers: User[] = []
const inactive: User[] = []

for (const user of users) {
  if (user.isAdmin) admins.push(user)
  if (user.isTester) testers.push(user)
  if (!user.isActive) inactive.push(user)
}
```

---

## Kural 7.7: Dizi Karşılaştırmaları İçin Erken Uzunluk Kontrolü

**Etki:** ORTA-YÜKSEK  
**Etiketler:** javascript, arrays, performance, optimization, comparison  

## Dizi Karşılaştırmaları İçin Erken Uzunluk Kontrolü

Pahalı işlemlerle dizileri karşılaştırırken (sıralama, derin eşitlik, serialization), önce uzunlukları kontrol edin. Uzunluklar farklıysa, diziler eşit olamaz.

Gerçek dünya uygulamalarında, bu optimizasyon özellikle karşılaştırma sık kullanılan yollarda çalıştığında değerlidir (event handler'lar, render döngüleri).

**Yanlış (her zaman pahalı karşılaştırma yapar):**

```typescript
function hasChanges(current: string[], original: string[]) {
  // Uzunluklar farklı olsa bile her zaman sıralar ve birleştirir
  return current.sort().join() !== original.sort().join()
}
```

İki O(n log n) sıralama, `current.length` 5 ve `original.length` 100 olduğunda bile çalışır. Dizileri birleştirme ve string'leri karşılaştırma yükü de vardır.

**Doğru (önce O(1) uzunluk kontrolü):**

```typescript
function hasChanges(current: string[], original: string[]) {
  // Uzunluklar farklıysa erken dön
  if (current.length !== original.length) {
    return true
  }
  // Yalnızca uzunluklar eşleştiğinde sırala
  const currentSorted = current.toSorted()
  const originalSorted = original.toSorted()
  for (let i = 0; i < currentSorted.length; i++) {
    if (currentSorted[i] !== originalSorted[i]) {
      return true
    }
  }
  return false
}
```

Bu yeni yaklaşım daha verimlidir çünkü:
- Uzunluklar farklı olduğunda dizileri sıralama ve birleştirme yükünden kaçınır
- Birleştirilmiş string'ler için bellek tüketiminden kaçınır (özellikle büyük diziler için önemli)
- Orijinal dizileri mutate etmekten kaçınır
- Bir fark bulunduğunda erken döner

---

## Kural 7.8: Fonksiyonlardan Erken Dönüş

**Etki:** DÜŞÜK-ORTA  
**Etiketler:** javascript, functions, optimization, early-return  

## Fonksiyonlardan Erken Dönüş

Gereksiz işlemeyi atlamak için sonuç belirlendiğinde erken dönün.

**Yanlış (cevabı bulduktan sonra bile tüm öğeleri işler):**

```typescript
function validateUsers(users: User[]) {
  let hasError = false
  let errorMessage = ''
  
  for (const user of users) {
    if (!user.email) {
      hasError = true
      errorMessage = 'E-posta gerekli'
    }
    if (!user.name) {
      hasError = true
      errorMessage = 'İsim gerekli'
    }
    // Hata bulunduktan sonra bile tüm kullanıcıları kontrol etmeye devam eder
  }
  
  return hasError ? { valid: false, error: errorMessage } : { valid: true }
}
```

**Doğru (ilk hatada hemen döner):**

```typescript
function validateUsers(users: User[]) {
  for (const user of users) {
    if (!user.email) {
      return { valid: false, error: 'E-posta gerekli' }
    }
    if (!user.name) {
      return { valid: false, error: 'İsim gerekli' }
    }
  }

  return { valid: true }
}
```

---

## Kural 7.9: RegExp Oluşturmayı Yukarı Taşıyın

**Etki:** DÜŞÜK-ORTA  
**Etiketler:** javascript, regexp, optimization, memoization  

## RegExp Oluşturmayı Yukarı Taşıyın

Render içinde RegExp oluşturmayın. Modül scope'una taşıyın veya `useMemo()` ile memoize edin.

**Yanlış (her render'da yeni RegExp):**

```tsx
function Highlighter({ text, query }: Props) {
  const regex = new RegExp(`(${query})`, 'gi')
  const parts = text.split(regex)
  return <>{parts.map((part, i) => ...)}</>
}
```

**Doğru (memoize edin veya yukarı taşıyın):**

```tsx
const EMAIL_REGEX = /^[^\s@]+@[^\s@]+\.[^\s@]+$/

function Highlighter({ text, query }: Props) {
  const regex = useMemo(
    () => new RegExp(`(${escapeRegex(query)})`, 'gi'),
    [query]
  )
  const parts = text.split(regex)
  return <>{parts.map((part, i) => ...)}</>
}
```

**Uyarı (global regex mutable state'e sahiptir):**

Global regex (`/g`) mutable `lastIndex` state'ine sahiptir:

```typescript
const regex = /foo/g
regex.test('foo')  // true, lastIndex = 3
regex.test('foo')  // false, lastIndex = 0
```

---

## Kural 7.10: Sort Yerine Min/Max İçin Döngü Kullanın

**Etki:** DÜŞÜK  
**Etiketler:** javascript, arrays, performance, sorting, algorithms  

## Sort Yerine Min/Max İçin Döngü Kullanın

En küçük veya en büyük öğeyi bulmak yalnızca dizi üzerinden tek bir geçiş gerektirir. Sıralama gereksizdir ve daha yavaştır.

**Yanlış (O(n log n) - en sonuncuyu bulmak için sırala):**

```typescript
interface Project {
  id: string
  name: string
  updatedAt: number
}

function getLatestProject(projects: Project[]) {
  const sorted = [...projects].sort((a, b) => b.updatedAt - a.updatedAt)
  return sorted[0]
}
```

Maksimum değeri bulmak için tüm diziyi sıralar.

**Yanlış (O(n log n) - en eski ve en yeni için sırala):**

```typescript
function getOldestAndNewest(projects: Project[]) {
  const sorted = [...projects].sort((a, b) => a.updatedAt - b.updatedAt)
  return { oldest: sorted[0], newest: sorted[sorted.length - 1] }
}
```

Yalnızca min/max gerektiğinde hala gereksiz yere sıralar.

**Doğru (O(n) - tek döngü):**

```typescript
function getLatestProject(projects: Project[]) {
  if (projects.length === 0) return null
  
  let latest = projects[0]
  
  for (let i = 1; i < projects.length; i++) {
    if (projects[i].updatedAt > latest.updatedAt) {
      latest = projects[i]
    }
  }
  
  return latest
}

function getOldestAndNewest(projects: Project[]) {
  if (projects.length === 0) return { oldest: null, newest: null }
  
  let oldest = projects[0]
  let newest = projects[0]
  
  for (let i = 1; i < projects.length; i++) {
    if (projects[i].updatedAt < oldest.updatedAt) oldest = projects[i]
    if (projects[i].updatedAt > newest.updatedAt) newest = projects[i]
  }
  
  return { oldest, newest }
}
```

Dizi üzerinden tek geçiş, kopyalama yok, sıralama yok.

**Alternatif (küçük diziler için Math.min/Math.max):**

```typescript
const numbers = [5, 2, 8, 1, 9]
const min = Math.min(...numbers)
const max = Math.max(...numbers)
```

Bu küçük diziler için çalışır, ancak spread operator sınırlamaları nedeniyle çok büyük diziler için daha yavaş olabilir veya hata verebilir. Chrome 143'te maksimum dizi uzunluğu yaklaşık 124000 ve Safari 18'de 638000'dir; kesin sayılar değişebilir - [fiddle'a](https://jsfiddle.net/qw1jabsx/4/) bakın. Güvenilirlik için döngü yaklaşımını kullanın.

---

## Kural 7.11: O(1) Aramalar İçin Set/Map Kullanın

**Etki:** DÜŞÜK-ORTA  
**Etiketler:** javascript, set, map, data-structures, performance  

## O(1) Aramalar İçin Set/Map Kullanın

Tekrarlayan üyelik kontrolleri için dizileri Set/Map'e dönüştürün.

**Yanlış (kontrol başına O(n)):**

```typescript
const allowedIds = ['a', 'b', 'c', ...]
items.filter(item => allowedIds.includes(item.id))
```

**Doğru (kontrol başına O(1)):**

```typescript
const allowedIds = new Set(['a', 'b', 'c', ...])
items.filter(item => allowedIds.has(item.id))
```

---

## Kural 7.12: Immutability İçin sort() Yerine toSorted() Kullanın

**Etki:** ORTA-YÜKSEK  
**Etiketler:** javascript, arrays, immutability, react, state, mutation  

## Immutability İçin sort() Yerine toSorted() Kullanın

`.sort()` diziyi yerinde mutate eder, bu da React state ve props ile hatalara neden olabilir. Mutasyon olmadan yeni bir sıralanmış dizi oluşturmak için `.toSorted()` kullanın.

**Yanlış (orijinal dizi mutate edilir):**

```typescript
function UserList({ users }: { users: User[] }) {
  // Users prop dizisini mutate eder!
  const sorted = useMemo(
    () => users.sort((a, b) => a.name.localeCompare(b.name)),
    [users]
  )
  return <div>{sorted.map(renderUser)}</div>
}
```

**Doğru (yeni dizi oluşturur):**

```typescript
function UserList({ users }: { users: User[] }) {
  // Yeni sıralanmış dizi oluşturur, orijinal değişmez
  const sorted = useMemo(
    () => users.toSorted((a, b) => a.name.localeCompare(b.name)),
    [users]
  )
  return <div>{sorted.map(renderUser)}</div>
}
```

**React'te neden önemlidir:**

1. Props/state mutasyonları React'in immutability modelini bozar - React, props ve state'in salt okunur olarak değerlendirilmesini bekler
2. Stale closure buglarına neden olur - Kapamlarda (callback'ler, effect'ler) dizileri mutate etmek beklenmedik davranışlara yol açabilir

**Tarayıcı desteği (eski tarayıcılar için fallback):**

`.toSorted()` tüm modern tarayıcılarda mevcuttur (Chrome 110+, Safari 16+, Firefox 115+, Node.js 20+). Eski ortamlar için spread operator kullanın:

```typescript
// Eski tarayıcılar için fallback
const sorted = [...items].sort((a, b) => a.value - b.value)
```

**Diğer immutable dizi metodları:**

- `.toSorted()` - immutable sort
- `.toReversed()` - immutable reverse
- `.toSpliced()` - immutable splice
- `.with()` - immutable element replacement
