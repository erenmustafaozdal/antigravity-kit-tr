# 4. İstemci Tarafı Veri Çekme (Client-Side Data Fetching)

> **Etki:** ORTA-YÜKSEK
> **Odak:** Otomatik tekilleştirme ve verimli veri çekme desenleri, gereksiz ağ isteklerini azaltır.

---

## Genel Bakış

Bu bölüm, istemci tarafı veri çekmeye odaklanan **4 kural** içerir.

---

## Kural 4.1: Global Event Listener'ları Tekilleştirin

**Etki:** DÜŞÜK  
**Etiketler:** client, swr, event-listeners, subscription  

## Global Event Listener'ları Tekilleştirin

Component instance'ları arasında global event listener'ları paylaşmak için `useSWRSubscription()` kullanın.

**Yanlış (N instance = N listener):**

```tsx
function useKeyboardShortcut(key: string, callback: () => void) {
  useEffect(() => {
    const handler = (e: KeyboardEvent) => {
      if (e.metaKey && e.key === key) {
        callback()
      }
    }
    window.addEventListener('keydown', handler)
    return () => window.removeEventListener('keydown', handler)
  }, [key, callback])
}
```

`useKeyboardShortcut` hook'unu birden fazla kez kullandığınızda, her instance yeni bir listener kaydeder.

**Doğru (N instance = 1 listener):**

```tsx
import useSWRSubscription from 'swr/subscription'

// Modül seviyesinde Map, her key için callback'leri takip eder
const keyCallbacks = new Map<string, Set<() => void>>()

function useKeyboardShortcut(key: string, callback: () => void) {
  // Bu callback'i Map'e kaydet
  useEffect(() => {
    if (!keyCallbacks.has(key)) {
      keyCallbacks.set(key, new Set())
    }
    keyCallbacks.get(key)!.add(callback)

    return () => {
      const set = keyCallbacks.get(key)
      if (set) {
        set.delete(callback)
        if (set.size === 0) {
          keyCallbacks.delete(key)
        }
      }
    }
  }, [key, callback])

  useSWRSubscription('global-keydown', () => {
    const handler = (e: KeyboardEvent) => {
      if (e.metaKey && keyCallbacks.has(e.key)) {
        keyCallbacks.get(e.key)!.forEach(cb => cb())
      }
    }
    window.addEventListener('keydown', handler)
    return () => window.removeEventListener('keydown', handler)
  })
}

function Profile() {
  // Birden fazla kısayol aynı listener'ı paylaşır
  useKeyboardShortcut('p', () => { /* ... */ }) 
  useKeyboardShortcut('k', () => { /* ... */ })
  // ...
}
```

---

## Kural 4.2: Scroll Performansı İçin Passive Event Listener Kullanın

**Etki:** ORTA  
**Etiketler:** client, event-listeners, scrolling, performance, touch, wheel  

## Scroll Performansı İçin Passive Event Listener Kullanın

Touch ve wheel event listener'larına `{ passive: true }` ekleyerek anında scrolling'i etkinleştirin. Browser'lar normalde `preventDefault()` çağrısını kontrol etmek için listener'ların bitmesini bekler, bu da scroll gecikmesine neden olur.

**Yanlış:**

```typescript
useEffect(() => {
  const handleTouch = (e: TouchEvent) => console.log(e.touches[0].clientX)
  const handleWheel = (e: WheelEvent) => console.log(e.deltaY)
  
  document.addEventListener('touchstart', handleTouch)
  document.addEventListener('wheel', handleWheel)
  
  return () => {
    document.removeEventListener('touchstart', handleTouch)
    document.removeEventListener('wheel', handleWheel)
  }
}, [])
```

**Doğru:**

```typescript
useEffect(() => {
  const handleTouch = (e: TouchEvent) => console.log(e.touches[0].clientX)
  const handleWheel = (e: WheelEvent) => console.log(e.deltaY)
  
  document.addEventListener('touchstart', handleTouch, { passive: true })
  document.addEventListener('wheel', handleWheel, { passive: true })
  
  return () => {
    document.removeEventListener('touchstart', handleTouch)
    document.removeEventListener('wheel', handleWheel)
  }
}, [])
```

**Passive kullanın:** tracking/analytics, logging, `preventDefault()` çağırmayan herhangi bir listener.

**Passive kullanmayın:** özel swipe hareketleri, özel zoom kontrolleri veya `preventDefault()` ihtiyacı olan herhangi bir listener.

---

## Kural 4.3: Otomatik Tekilleştirme İçin SWR Kullanın

**Etki:** ORTA-YÜKSEK  
**Etiketler:** client, swr, deduplication, data-fetching  

## Otomatik Tekilleştirme İçin SWR Kullanın

SWR, component instance'ları arasında istek tekilleştirmesi, önbellekleme ve revalidation sağlar.

**Yanlış (tekilleştirme yok, her instance fetch eder):**

```tsx
function UserList() {
  const [users, setUsers] = useState([])
  useEffect(() => {
    fetch('/api/users')
      .then(r => r.json())
      .then(setUsers)
  }, [])
}
```

**Doğru (birden fazla instance bir isteği paylaşır):**

```tsx
import useSWR from 'swr'

function UserList() {
  const { data: users } = useSWR('/api/users', fetcher)
}
```

**Değişmez veri için:**

```tsx
import { useImmutableSWR } from '@/lib/swr'

function StaticContent() {
  const { data } = useImmutableSWR('/api/config', fetcher)
}
```

**Mutasyon için:**

```tsx
import { useSWRMutation } from 'swr/mutation'

function UpdateButton() {
  const { trigger } = useSWRMutation('/api/user', updateUser)
  return <button onClick={() => trigger()}>Güncelle</button>
}
```

Referans: [https://swr.vercel.app](https://swr.vercel.app)

---

## Kural 4.4: localStorage Verisini Versiyonlayın ve Minimize Edin

**Etki:** ORTA  
**Etiketler:** client, localStorage, storage, versioning, data-minimization  

## localStorage Verisini Versiyonlayın ve Minimize Edin

Key'lere versiyon öneki ekleyin ve yalnızca gerekli alanları saklayın. Şema çakışmalarını ve hassas verilerin kazara saklanmasını önler.

**Yanlış:**

```typescript
// Versiyon yok, her şeyi saklar, hata işleme yok
localStorage.setItem('userConfig', JSON.stringify(fullUserObject))
const data = localStorage.getItem('userConfig')
```

**Doğru:**

```typescript
const VERSION = 'v2'

function saveConfig(config: { theme: string; language: string }) {
  try {
    localStorage.setItem(`userConfig:${VERSION}`, JSON.stringify(config))
  } catch {
    // Gizli/private browsing, kota aşımı veya devre dışı bırakılmışsa fırlatır
  }
}

function loadConfig() {
  try {
    const data = localStorage.getItem(`userConfig:${VERSION}`)
    return data ? JSON.parse(data) : null
  } catch {
    return null
  }
}

// v1'den v2'ye migrasyon
function migrate() {
  try {
    const v1 = localStorage.getItem('userConfig:v1')
    if (v1) {
      const old = JSON.parse(v1)
      saveConfig({ theme: old.darkMode ? 'dark' : 'light', language: old.lang })
      localStorage.removeItem('userConfig:v1')
    }
  } catch {}
}
```

**Sunucu yanıtlarından minimal alanları saklayın:**

```typescript
// User nesnesi 20+ alana sahip, yalnızca UI'nin ihtiyacı olanları sakla
function cachePrefs(user: FullUser) {
  try {
    localStorage.setItem('prefs:v1', JSON.stringify({
      theme: user.preferences.theme,
      notifications: user.preferences.notifications
    }))
  } catch {}
}
```

**Her zaman try-catch ile sarın:** `getItem()` ve `setItem()` gizli/private browsing'de (Safari, Firefox), kota aşıldığında veya devre dışı bırakıldığında fırlatır.

**Faydalar:** Versiyonlama ile şema evrimi, azaltılmış depolama boyutu, token/PII/dahili bayrakların saklanmasını önler.
