# 5. Yeniden Render Optimizasyonu (Re-render Optimization)

> **Etki:** ORTA
> **Odak:** Gereksiz yeniden render'ları azaltmak, boşa giden hesaplamaları minimize eder ve UI yanıt verebilirliğini iyileştirir.

---

## Genel Bakış

Bu bölüm, yeniden render optimizasyonuna odaklanan **12 kural** içerir.

---

## Kural 5.1: Türetilmiş State'i Rendering Sırasında Hesaplayın

**Etki:** ORTA  
**Etiketler:** rerender, derived-state, useEffect, state  

## Türetilmiş State'i Rendering Sırasında Hesaplayın

Bir değer mevcut props/state'ten hesaplanabiliyorsa, onu state'te saklamayın veya bir effect'te güncellemeyin. Ekstra render'lardan ve state drift'inden kaçınmak için render sırasında türetin. Yalnızca prop değişikliklerine yanıt olarak effect'lerde state ayarlamayın; bunun yerine türetilmiş değerleri veya keyed reset'leri tercih edin.

**Yanlış (gereksiz state ve effect):**

```tsx
function Form() {
  const [firstName, setFirstName] = useState('First')
  const [lastName, setLastName] = useState('Last')
  const [fullName, setFullName] = useState('')

  useEffect(() => {
    setFullName(firstName + ' ' + lastName)
  }, [firstName, lastName])

  return <p>{fullName}</p>
}
```

**Doğru (render sırasında türet):**

```tsx
function Form() {
  const [firstName, setFirstName] = useState('First')
  const [lastName, setLastName] = useState('Last')
  const fullName = firstName + ' ' + lastName

  return <p>{fullName}</p>
}
```

Referans: [You Might Not Need an Effect](https://react.dev/learn/you-might-not-need-an-effect)

---

## Kural 5.2: State Okumayı Kullanım Noktasına Erteleyin

**Etki:** ORTA  
**Etiketler:** rerender, searchParams, localStorage, optimization  

## State Okumayı Kullanım Noktasına Erteleyin

Dinamik state'i (searchParams, localStorage) yalnızca callback'lerde okuyorsanız abone olmayın.

**Yanlış (tüm searchParams değişikliklerine abone olur):**

```tsx
function ShareButton({ chatId }: { chatId: string }) {
  const searchParams = useSearchParams()

  const handleShare = () => {
    const ref = searchParams.get('ref')
    shareChat(chatId, { ref })
  }

  return <button onClick={handleShare}>Paylaş</button>
}
```

**Doğru (talep üzerine okur, abonelik yok):**

```tsx
function ShareButton({ chatId }: { chatId: string }) {
  const handleShare = () => {
    const params = new URLSearchParams(window.location.search)
    const ref = params.get('ref')
    shareChat(chatId, { ref })
  }

  return <button onClick={handleShare}>Paylaş</button>
}
```

---

## Kural 5.3: Primitive Sonuç Tipi Olan Basit İfadeleri useMemo ile Sarmayın

**Etki:** DÜŞÜK-ORTA  
**Etiketler:** rerender, useMemo, optimization  

## Primitive Sonuç Tipi Olan Basit İfadeleri useMemo ile Sarmayın

Bir ifade basit olduğunda (birkaç mantıksal veya aritmetik operatör) ve primitive sonuç tipine sahip olduğunda (boolean, number, string), onu `useMemo` ile sarmayın. `useMemo` çağırmak ve hook bağımlılıklarını karşılaştırmak ifadenin kendisinden daha fazla kaynak tüketebilir.

**Yanlış:**

```tsx
function Header({ user, notifications }: Props) {
  const isLoading = useMemo(() => {
    return user.isLoading || notifications.isLoading
  }, [user.isLoading, notifications.isLoading])

  if (isLoading) return <Skeleton />
  // markup döndür
}
```

**Doğru:**

```tsx
function Header({ user, notifications }: Props) {
  const isLoading = user.isLoading || notifications.isLoading

  if (isLoading) return <Skeleton />
  // markup döndür
}
```

---

## Kural 5.4: Memoize Edilmiş Componentten Varsayılan Non-primitive Parametre Değerini Sabite Çıkarın

**Etki:** ORTA  
**Etiketler:** rerender, memo, optimization  

## Memoize Edilmiş Componentten Varsayılan Non-primitive Parametre Değerini Sabite Çıkarın

Memoize edilmiş component, bazı non-primitive opsiyonel parametreler (dizi, fonksiyon veya nesne gibi) için varsayılan değere sahip olduğunda, componenti bu parametre olmadan çağırmak memoization'ı bozar. Bunun nedeni, her yeniden render'da yeni değer instance'larının oluşturulması ve `memo()`'daki strict equality karşılaştırmasını geçmemeleridir.

Bu sorunu çözmek için varsayılan değeri bir sabite çıkarın.

**Yanlış (`onClick` her yeniden render'da farklı değerlere sahip):**

```tsx
const UserAvatar = memo(function UserAvatar({ onClick = () => {} }: { onClick?: () => void }) {
  // ...
})

// Opsiyonel onClick olmadan kullanıldı
<UserAvatar />
```

**Doğru (stabil varsayılan değer):**

```tsx
const NOOP = () => {};

const UserAvatar = memo(function UserAvatar({ onClick = NOOP }: { onClick?: () => void }) {
  // ...
})

// Opsiyonel onClick olmadan kullanıldı
<UserAvatar />
```

---

## Kural 5.5: Memoize Edilmiş Componentlere Çıkarın

**Etki:** ORTA  
**Etiketler:** rerender, memo, useMemo, optimization  

## Memoize Edilmiş Componentlere Çıkarın

Pahalı işleri memoize edilmiş componentlere çıkararak hesaplamadan önce erken dönüşler sağlayın.

**Yanlış (yüklenmede bile avatar hesaplar):**

```tsx
function Profile({ user, loading }: Props) {
  const avatar = useMemo(() => {
    const id = computeAvatarId(user)
    return <Avatar id={id} />
  }, [user])

  if (loading) return <Skeleton />
  return <div>{avatar}</div>
}
```

**Doğru (yüklenirken hesaplamayı atlar):**

```tsx
const UserAvatar = memo(function UserAvatar({ user }: { user: User }) {
  const id = useMemo(() => computeAvatarId(user), [user])
  return <Avatar id={id} />
})

function Profile({ user, loading }: Props) {
  if (loading) return <Skeleton />
  return (
    <div>
      <UserAvatar user={user} />
    </div>
  )
}
```

**Not:** Projenizde [React Compiler](https://react.dev/learn/react-compiler) etkinse, `memo()` ve `useMemo()` ile manuel memoization gerekli değildir. Compiler otomatik olarak yeniden render'ları optimize eder.

---

## Kural 5.6: Effect Bağımlılıklarını Daraltın

**Etki:** DÜŞÜK  
**Etiketler:** rerender, useEffect, dependencies, optimization  

## Effect Bağımlılıklarını Daraltın

Effect'in yeniden çalışmasını minimize etmek için nesneler yerine primitive bağımlılıklar belirtin.

**Yanlış (herhangi bir user alanı değiştiğinde yeniden çalışır):**

```tsx
useEffect(() => {
  console.log(user.id)
}, [user])
```

**Doğru (yalnızca id değiştiğinde yeniden çalışır):**

```tsx
useEffect(() => {
  console.log(user.id)
}, [user.id])
```

**Türetilmiş state için, effect dışında hesaplayın:**

```tsx
// Yanlış: width=767, 766, 765... de çalışır
useEffect(() => {
  if (width < 768) {
    enableMobileMode()
  }
}, [width])

// Doğru: yalnızca boolean geçişinde çalışır
const isMobile = width < 768
useEffect(() => {
  if (isMobile) {
    enableMobileMode()
  }
}, [isMobile])
```

---

## Kural 5.7: Etkileşim Mantığını Event Handler'lara Koyun

**Etki:** ORTA  
**Etiketler:** rerender, useEffect, events, side-effects, dependencies  

## Etkileşim Mantığını Event Handler'lara Koyun

Bir yan etki belirli bir kullanıcı eylemi (submit, click, drag) tarafından tetikleniyorsa, onu o event handler'da çalıştırın. Eylemi state + effect olarak modellemeyin; bu effect'lerin ilgisiz değişikliklerde yeniden çalışmasına neden olur ve eylemi kopyalayabilir.

**Yanlış (event state + effect olarak modelleniyor):**

```tsx
function Form() {
  const [submitted, setSubmitted] = useState(false)
  const theme = useContext(ThemeContext)

  useEffect(() => {
    if (submitted) {
      post('/api/register')
      showToast('Kayıt olundu', theme)
    }
  }, [submitted, theme])

  return <button onClick={() => setSubmitted(true)}>Gönder</button>
}
```

**Doğru (handler'da yap):**

```tsx
function Form() {
  const theme = useContext(ThemeContext)

  function handleSubmit() {
    post('/api/register')
    showToast('Kayıt olundu', theme)
  }

  return <button onClick={handleSubmit}>Gönder</button>
}
```

Referans: [Should this code move to an event handler?](https://react.dev/learn/removing-effect-dependencies#should-this-code-move-to-an-event-handler)

---

## Kural 5.8: Türetilmiş State'e Abone Olun

**Etki:** ORTA  
**Etiketler:** rerender, derived-state, media-query, optimization  

## Türetilmiş State'e Abone Olun

Yeniden render sıklığını azaltmak için sürekli değerler yerine türetilmiş boolean state'e abone olun.

**Yanlış (her piksel değişiminde yeniden render):**

```tsx
function Sidebar() {
  const width = useWindowWidth()  // sürekli günceller
  const isMobile = width < 768
  return <nav className={isMobile ? 'mobile' : 'desktop'} />
}
```

**Doğru (yalnızca boolean değiştiğinde yeniden render):**

```tsx
function Sidebar() {
  const isMobile = useMediaQuery('(max-width: 767px)')
  return <nav className={isMobile ? 'mobile' : 'desktop'} />
}
```

---

## Kural 5.9: Fonksiyonel setState Güncellemeleri Kullanın

**Etki:** ORTA  
**Etiketler:** react, hooks, useState, useCallback, callbacks, closures  

## Fonksiyonel setState Güncellemeleri Kullanın

Mevcut state değerine dayalı olarak state güncellerken, state değişkenine doğrudan referans vermek yerine setState'in fonksiyonel güncelleme formunu kullanın. Bu stale closure'ları önler, gereksiz bağımlılıkları ortadan kaldırır ve stabil callback referansları oluşturur.

**Yanlış (bağımlılık olarak state gerektirir):**

```tsx
function TodoList() {
  const [items, setItems] = useState(initialItems)
  
  // Callback items'a bağlı olmalı, her items değişikliğinde yeniden oluşturulur
  const addItems = useCallback((newItems: Item[]) => {
    setItems([...items, ...newItems])
  }, [items])  // ❌ items bağımlılığı yeniden oluşturmalara neden olur
  
  // Bağımlılık unutulursa stale closure riski
  const removeItem = useCallback((id: string) => {
    setItems(items.filter(item => item.id !== id))
  }, [])  // ❌ items bağımlılığı eksik - stale items kullanacak!
  
  return <ItemsEditor items={items} onAdd={addItems} onRemove={removeItem} />
}
```

**Doğru (stabil callback'ler, stale closure yok):**

```tsx
function TodoList() {
  const [items, setItems] = useState(initialItems)
  
  // Stabil callback, asla yeniden oluşturulmaz
  const addItems = useCallback((newItems: Item[]) => {
    setItems(curr => [...curr, ...newItems])
  }, [])  // ✅ Bağımlılık gerekmiyor
  
  // Her zaman en son state'i kullanır, stale closure riski yok
  const removeItem = useCallback((id: string) => {
    setItems(curr => curr.filter(item => item.id !== id))
  }, [])  // ✅ Güvenli ve stabil
  
  return <ItemsEditor items={items} onAdd={addItems} onRemove={removeItem} />
}
```

**Faydalar:**

1. **Stabil callback referansları** - State değiştiğinde callback'lerin yeniden oluşturulmasına gerek yok
2. **Stale closure yok** - Her zaman en son state değerinde çalışır
3. **Daha az bağımlılık** - Bağımlılık dizilerini basitleştirir ve memory leak'leri azaltır
4. **Hataları önler** - React closure hatalarının en yaygın kaynağını ortadan kaldırır

**Fonksiyonel güncellemeleri ne zaman kullanmalı:**

- Mevcut state değerine bağlı herhangi bir setState
- State gerektiğinde useCallback/useMemo içinde
- State'e referans veren event handler'lar
- State'i güncelleyen async işlemler

**Direkt güncellemeler ne zaman uygun:**

- State'i statik bir değere ayarlama: `setCount(0)`
- State'i yalnızca props/argümanlardan ayarlama: `setName(newName)`
- State önceki değere bağlı değilse

**Not:** Projenizde [React Compiler](https://react.dev/learn/react-compiler) etkinse, compiler bazı durumları otomatik olarak optimize edebilir, ancak doğruluk için ve stale closure hatalarını önlemek için fonksiyonel güncellemeler hala önerilir.

---

## Kural 5.10: Lazy State Initialization Kullanın

**Etki:** ORTA  
**Etiketler:** react, hooks, useState, performance, initialization  

## Lazy State Initialization Kullanın

Pahalı başlangıç değerleri için `useState`'e bir fonksiyon geçirin. Fonk siyon formu olmadan, initializer her render'da çalışır, ancak değer yalnızca bir kez kullanılır.

**Yanlış (her render'da çalışır):**

```tsx
function FilteredList({ items }: { items: Item[] }) {
  // buildSearchIndex() HER render'da çalışır, initialization'dan sonra bile
  const [searchIndex, setSearchIndex] = useState(buildSearchIndex(items))
  const [query, setQuery] = useState('')
  
  // query değiştiğinde, buildSearchIndex gereksiz yere tekrar çalışır
  return <SearchResults index={searchIndex} query={query} />
}

function UserProfile() {
  // JSON.parse her render'da çalışır
  const [settings, setSettings] = useState(
    JSON.parse(localStorage.getItem('settings') || '{}')
  )
  
  return <SettingsForm settings={settings} onChange={setSettings} />
}
```

**Doğru (yalnızca bir kez çalışır):**

```tsx
function FilteredList({ items }: { items: Item[] }) {
  // buildSearchIndex() YALNIZCA ilk render'da çalışır
  const [searchIndex, setSearchIndex] = useState(() => buildSearchIndex(items))
  const [query, setQuery] = useState('')
  
  return <SearchResults index={searchIndex} query={query} />
}

function UserProfile() {
  // JSON.parse yalnızca ilk render'da çalışır
  const [settings, setSettings] = useState(() => {
    const stored = localStorage.getItem('settings')
    return stored ? JSON.parse(stored) : {}
  })
  
  return <SettingsForm settings={settings} onChange={setSettings} />
}
```

localStorage/sessionStorage'dan başlangıç değerlerini hesaplarken, veri yapıları (indexler, map'ler) oluştururken, DOM'dan okurken veya ağır dönüşümler yaparken lazy initialization kullanın.

Basit primitive'ler (`useState(0)`), direkt referanslar (`useState(props.value)`) veya ucuz literaller (`useState({})`) için fonksiyon formu gereksizdir.

---

## Kural 5.11: Acil Olmayan Güncellemeler İçin Transition Kullanın

**Etki:** ORTA  
**Etiketler:** rerender, transitions, startTransition, performance  

## Acil Olmayan Güncellemeler İçin Transition Kullanın

UI yanıt verebilirliğini korumak için sık, acil olmayan state güncellemelerini transition olarak işaretleyin.

**Yanlış (her scroll'da UI'yi bloklar):**

```tsx
function ScrollTracker() {
  const [scrollY, setScrollY] = useState(0)
  useEffect(() => {
    const handler = () => setScrollY(window.scrollY)
    window.addEventListener('scroll', handler, { passive: true })
    return () => window.removeEventListener('scroll', handler)
  }, [])
}
```

**Doğru (bloke etmeyen güncellemeler):**

```tsx
import { startTransition } from 'react'

function ScrollTracker() {
  const [scrollY, setScrollY] = useState(0)
  useEffect(() => {
    const handler = () => {
      startTransition(() => setScrollY(window.scrollY))
    }
    window.addEventListener('scroll', handler, { passive: true })
    return () => window.removeEventListener('scroll', handler)
  }, [])
}
```

---

## Kural 5.12: Geçici Değerler İçin useRef Kullanın

**Etki:** ORTA  
**Etiketler:** rerender, useref, state, performance  

## Geçici Değerler İçin useRef Kullanın

Bir değer sık değiştiğinde ve her güncellemedebit yeniden render istemediğinizde (örn. mouse tracker'lar, interval'lar, geçici bayraklar), onu `useState` yerine `useRef`'te saklayın. Component state'i UI için tutun; geçici DOM'a yakın değerler için ref'leri kullanın. Bir ref'i güncellemek yeniden render tetiklemez.

**Yanlış (her güncellemede render eder):**

```tsx
function Tracker() {
  const [lastX, setLastX] = useState(0)

  useEffect(() => {
    const onMove = (e: MouseEvent) => setLastX(e.clientX)
    window.addEventListener('mousemove', onMove)
    return () => window.removeEventListener('mousemove', onMove)
  }, [])

  return (
    <div
      style={{
        position: 'fixed',
        top: 0,
        left: lastX,
        width: 8,
        height: 8,
        background: 'black',
      }}
    />
  )
}
```

**Doğru (tracking için yeniden render yok):**

```tsx
function Tracker() {
  const lastXRef = useRef(0)
  const dotRef = useRef<HTMLDivElement>(null)

  useEffect(() => {
    const onMove = (e: MouseEvent) => {
      lastXRef.current = e.clientX
      const node = dotRef.current
      if (node) {
        node.style.transform = `translateX(${e.clientX}px)`
      }
    }
    window.addEventListener('mousemove', onMove)
    return () => window.removeEventListener('mousemove', onMove)
  }, [])

  return (
    <div
      ref={dotRef}
      style={{
        position: 'fixed',
        top: 0,
        left: 0,
        width: 8,
        height: 8,
        background: 'black',
        transform: 'translateX(0px)',
      }}
    />
  )
}
```
