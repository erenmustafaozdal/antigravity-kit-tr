# 8. İleri Seviye Desenler (Advanced Patterns)

> **Etki:** DEĞİŞKEN
> **Odak:** Dikkatli uygulama gerektiren özel durumlar için ileri seviye desenler.

---

## Genel Bakış

Bu bölüm, ileri seviye desenlere odaklanan **3 kural** içerir.

---

## Kural 8.1: Uygulamayı Bağlanma Başına Değil Bir Kez Başlatın

**Etki:** DÜŞÜK-ORTA  
**Etiketler:** initialization, useEffect, app-startup, side-effects  

## Uygulamayı Bağlanma Başına Değil Bir Kez Başlatın

Uygulama yüklemesi başına bir kez çalışması gereken uygulama çapında başlatma kodunu, bir componentin `useEffect([])` içine koymayın. Componentler yeniden bağlanabilir ve effect'ler yeniden çalışır. Bunun yerine modül seviyesinde bir koruma kullanın veya giriş modülünde üst düzey init yapın.

**Yanlış (dev'de iki kez çalışır, yeniden bağlanmada tekrar çalışır):**

```tsx
function Comp() {
  useEffect(() => {
    loadFromStorage()
    checkAuthToken()
  }, [])

  // ...
}
```

**Doğru (uygulama yüklemesi başına bir kez):**

```tsx
let didInit = false

function Comp() {
  useEffect(() => {
    if (didInit) return
    didInit = true
    loadFromStorage()
    checkAuthToken()
  }, [])

  // ...
}
```

Referans: [Initializing the application](https://react.dev/learn/you-might-not-need-an-effect#initializing-the-application)

---

## Kural 8.2: Event Handler'ları Ref'lerde Saklayın

**Etki:** DÜŞÜK  
**Etiketler:** advanced, hooks, refs, event-handlers, optimization  

## Event Handler'ları Ref'lerde Saklayın

Callback değişikliklerinde yeniden abone olmaması gereken effect'lerde kullanıldığında, callback'leri ref'lerde saklayın.

**Yanlış (her render'da yeniden abone olur):**

```tsx
function useWindowEvent(event: string, handler: (e) => void) {
  useEffect(() => {
    window.addEventListener(event, handler)
    return () => window.removeEventListener(event, handler)
  }, [event, handler])
}
```

**Doğru (stabil abonelik):**

```tsx
function useWindowEvent(event: string, handler: (e) => void) {
  const handlerRef = useRef(handler)
  useEffect(() => {
    handlerRef.current = handler
  }, [handler])

  useEffect(() => {
    const listener = (e) => handlerRef.current(e)
    window.addEventListener(event, listener)
    return () => window.removeEventListener(event, listener)
  }, [event])
}
```

**Alternatif: en son React'teyseniz `useEffectEvent` kullanın:**

```tsx
import { useEffectEvent } from 'react'

function useWindowEvent(event: string, handler: (e) => void) {
  const onEvent = useEffectEvent(handler)

  useEffect(() => {
    window.addEventListener(event, onEvent)
    return () => window.removeEventListener(event, onEvent)
  }, [event])
}
```

`useEffectEvent` aynı desen için daha temiz bir API sağlar: her zaman handler'ın en son versiyonunu çağıran stabil bir fonksiyon referansı oluşturur.

---

## Kural 8.3: Stabil Callback Ref'leri İçin useEffectEvent

**Etki:** DÜŞÜK  
**Etiketler:** advanced, hooks, useEffectEvent, refs, optimization  

## Stabil Callback Ref'leri İçin useEffectEvent

Callback'lerde en son değerlere, bağımlılık dizilerine eklemeden erişin. Stale closure'lardan kaçınırken effect'in yeniden çalışmasını önler.

**Yanlış (her callback değişikliğinde effect yeniden çalışır):**

```tsx
function SearchInput({ onSearch }: { onSearch: (q: string) => void }) {
  const [query, setQuery] = useState('')

  useEffect(() => {
    const timeout = setTimeout(() => onSearch(query), 300)
    return () => clearTimeout(timeout)
  }, [query, onSearch])
}
```

**Doğru (React'in useEffectEvent kullanarak):**

```tsx
import { useEffectEvent } from 'react';

function SearchInput({ onSearch }: { onSearch: (q: string) => void }) {
  const [query, setQuery] = useState('')
  const onSearchEvent = useEffectEvent(onSearch)

  useEffect(() => {
    const timeout = setTimeout(() => onSearchEvent(query), 300)
    return () => clearTimeout(timeout)
  }, [query])
}
```
