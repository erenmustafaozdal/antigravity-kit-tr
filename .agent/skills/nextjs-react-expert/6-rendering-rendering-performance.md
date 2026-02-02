# 6. Rendering Performansı (Rendering Performance)

> **Etki:** ORTA
> **Odak:** Rendering sürecini optimize etmek, tarayıcının yapması gereken işi azaltır.

---

## Genel Bakış

Bu bölüm, rendering performansına odaklanan **9 kural** içerir.

---

## Kural 6.1: SVG Element Yerine SVG Wrapper'ı Animasyonlayın

**Etki:** DÜŞÜK  
**Etiketler:** rendering, svg, css, animation, performance  

## SVG Element Yerine SVG Wrapper'ı Animasyonlayın

Birçok tarayıcı, SVG elementlerinde CSS3 animasyonları için donanım hızlandırmasına sahip değildir. SVG'yi bir `<div>`'e sarın ve wrapper'ı animasyonlayın.

**Yanlış (SVG'yi doğrudan animasyonlar - donanım hızlandırma yok):**

```tsx
function LoadingSpinner() {
  return (
    <svg 
      className="animate-spin"
      width="24" 
      height="24" 
      viewBox="0 0 24 24"
    >
      <circle cx="12" cy="12" r="10" stroke="currentColor" />
    </svg>
  )
}
```

**Doğru (wrapper div animasyonluyor - donanım hızlandırmalı):**

```tsx
function LoadingSpinner() {
  return (
    <div className="animate-spin">
      <svg 
        width="24" 
        height="24" 
        viewBox="0 0 24 24"
      >
        <circle cx="12" cy="12" r="10" stroke="currentColor" />
      </svg>
    </div>
  )
}
```

Bu, tüm CSS transform ve transition'lar için geçerlidir (`transform`, `opacity`, `translate`, `scale`, `rotate`). Wrapper div, tarayıcıların daha akıcı animasyonlar için GPU hızlandırması kullanmasına izin verir.

---

## Kural 6.2: Uzun Listeler İçin CSS content-visibility

**Etki:** YÜKSEK  
**Etiketler:** rendering, css, content-visibility, long-lists  

## Uzun Listeler İçin CSS content-visibility

Ekran dışı rendering'i ertelemek için `content-visibility: auto` uygulayın.

**CSS:**

```css
.message-item {
  content-visibility: auto;
  contain-intrinsic-size: 0 80px;
}
```

**Örnek:**

```tsx
function MessageList({ messages }: { messages: Message[] }) {
  return (
    <div className="overflow-y-auto h-screen">
      {messages.map(msg => (
        <div key={msg.id} className="message-item">
          <Avatar user={msg.author} />
          <div>{msg.content}</div>
        </div>
      ))}
    </div>
  )
}
```

1000 mesaj için, tarayıcı ~990 ekran dışı öğe için layout/paint'i atlar (10× daha hızlı ilk render).

---

## Kural 6.3: Statik JSX Elementlerini Yukarı Taşıyın

**Etki:** DÜŞÜK  
**Etiketler:** rendering, jsx, static, optimization  

## Statik JSX Elementlerini Yukarı Taşıyın

Yeniden oluşturulmasını önlemek için statik JSX'i componentlerin dışına çıkarın.

**Yanlış (her render'da elementi yeniden oluşturur):**

```tsx
function LoadingSkeleton() {
  return <div className="animate-pulse h-20 bg-gray-200" />
}

function Container() {
  return (
    <div>
      {loading && <LoadingSkeleton />}
    </div>
  )
}
```

**Doğru (aynı elementi yeniden kullanır):**

```tsx
const loadingSkeleton = (
  <div className="animate-pulse h-20 bg-gray-200" />
)

function Container() {
  return (
    <div>
      {loading && loadingSkeleton}
    </div>
  )
}
```

Bu özellikle büyük ve statik SVG node'ları için yararlıdır, bunlar her render'da yeniden oluşturulması pahalı olabilir.

**Not:** Projenizde [React Compiler](https://react.dev/learn/react-compiler) etkinse, compiler otomatik olarak statik JSX elementlerini yukarı taşır ve component yeniden render'larını optimize eder, manuel taşıma gereksizdir.

---

## Kural 6.4: SVG Hassasiyetini Optimize Edin

**Etki:** DÜŞÜK  
**Etiketler:** rendering, svg, optimization, svgo  

## SVG Hassasiyetini Optimize Edin

Dosya boyutunu azaltmak için SVG koordinat hassasiyetini azaltın. Optimal hassasiyet viewBox boyutuna bağlıdır, ancak genel olarak hassasiyeti azaltmak göz önünde bulundurulmalıdır.

**Yanlış (aşırı hassas):**

```svg
<path d="M 10.293847 20.847362 L 30.938472 40.192837" />
```

**Doğru (1 ondalık basamak):**

```svg
<path d="M 10.3 20.8 L 30.9 40.2" />
```

**SVGO ile otomatikleştirin:**

```bash
npx svgo --precision=1 --multipass icon.svg
```

---

## Kural 6.5: Titreme Olmadan Hydration Mismatch'i Önleyin

**Etki:** ORTA  
**Etiketler:** rendering, ssr, hydration, localStorage, flicker  

## Titreme Olmadan Hydration Mismatch'i Önleyin

İstemci tarafı depolamaya (localStorage, cookies) bağlı içerik render ederken, React hydrate olmadan önce DOM'u güncelleyen senkron bir script enjekte ederek hem SSR bozulmasını hem de hydration sonrası titremeyi önleyin.

**Yanlış (SSR'ı bozar):**

```tsx
function ThemeWrapper({ children }: { children: ReactNode }) {
  // localStorage sunucuda mevcut değil - hata fırlatır
  const theme = localStorage.getItem('theme') || 'light'
  
  return (
    <div className={theme}>
      {children}
    </div>
  )
}
```

Sunucu tarafı rendering başarısız olacaktır çünkü `localStorage` undefined'dır.

**Yanlış (görsel titreme):**

```tsx
function ThemeWrapper({ children }: { children: ReactNode }) {
  const [theme, setTheme] = useState('light')
  
  useEffect(() => {
    // Hydration'dan sonra çalışır - görünür parlamaya neden olur
    const stored = localStorage.getItem('theme')
    if (stored) {
      setTheme(stored)
    }
  }, [])
  
  return (
    <div className={theme}>
      {children}
    </div>
  )
}
```

Component önce varsayılan değerle (`light`) render olur, sonra hydration'dan sonra güncellenir, yanlış içeriğin görünür bir parlamasına neden olur.

**Doğru (titreme yok, hydration mismatch yok):**

```tsx
function ThemeWrapper({ children }: { children: ReactNode }) {
  return (
    <>
      <div id="theme-wrapper">
        {children}
      </div>
      <script
        dangerouslySetInnerHTML={{
          __html: `
            (function() {
              try {
                var theme = localStorage.getItem('theme') || 'light';
                var el = document.getElementById('theme-wrapper');
                if (el) el.className = theme;
              } catch (e) {}
            })();
          `,
        }}
      />
    </>
  )
}
```

Inline script, elementi göstermeden önce senkron olarak yürütülür, DOM'un zaten doğru değere sahip olmasını sağlar. Titreme yok, hydration mismatch yok.

Bu desen özellikle tema değiştiricileri, kullanıcı tercihleri, kimlik doğrulama durumları ve varsayılan değerleri göstermeden hemen render edilmesi gereken istemci-only veriler için yararlıdır.

---

## Kural 6.6: Beklenen Hydration Mismatch'lerini Baskılayın

**Etki:** DÜŞÜK-ORTA  
**Etiketler:** rendering, hydration, ssr, nextjs  

## Beklenen Hydration Mismatch'lerini Baskılayın

SSR framework'lerinde (örn. Next.js), bazı değerler kasıtlı olarak sunucu ve istemcide farklıdır (rastgele ID'ler, tarihler, locale/timezone formatlama). Bu *beklenen* mismatch'ler için, gürültülü uyarıları önlemek için dinamik metni `suppressHydrationWarning` olan bir elemente sarın. Bunu gerçek hataları gizlemek için kullanmayın. Aşırı kullanmayın.

**Yanlış (bilinen mismatch uyarıları):**

```tsx
function Timestamp() {
  return <span>{new Date().toLocaleString()}</span>
}
```

**Doğru (yalnızca beklenen mismatch'i baskıla):**

```tsx
function Timestamp() {
  return (
    <span suppressHydrationWarning>
      {new Date().toLocaleString()}
    </span>
  )
}
```

---

## Kural 6.7: Göster/Gizle İçin Activity Component Kullanın

**Etki:** ORTA  
**Etiketler:** rendering, activity, visibility, state-preservation  

## Göster/Gizle İçin Activity Component Kullanın

Sık sık görünürlüğünü değiştiren pahalı componentler için state/DOM'u korumak için React'in `<Activity>`'sini kullanın.

**Kullanım:**

```tsx
import { Activity } from 'react'

function Dropdown({ isOpen }: Props) {
  return (
    <Activity mode={isOpen ? 'visible' : 'hidden'}>
      <ExpensiveMenu />
    </Activity>
  )
}
```

Pahalı yeniden render'lardan ve state kaybından kaçınır.

---

## Kural 6.8: Açık Koşullu Rendering Kullanın

**Etki:** DÜŞÜK  
**Etiketler:** rendering, conditional, jsx, falsy-values  

## Açık Koşullu Rendering Kullanın

Koşul `0`, `NaN` veya render edilecek diğer falsy değerler olabildiğinde, koşullu rendering için `&&` yerine açık ternary operatörleri (`? :`) kullanın.

**Yanlış (count 0 olduğunda "0" render eder):**

```tsx
function Badge({ count }: { count: number }) {
  return (
    <div>
      {count && <span className="badge">{count}</span>}
    </div>
  )
}

// count = 0 iken, render eder: <div>0</div>
// count = 5 iken, render eder: <div><span class="badge">5</span></div>
```

**Doğru (count 0 olduğunda hiçbir şey render etmez):**

```tsx
function Badge({ count }: { count: number }) {
  return (
    <div>
      {count > 0 ? <span className="badge">{count}</span> : null}
    </div>
  )
}

// count = 0 iken, render eder: <div></div>
// count = 5 iken, render eder: <div><span class="badge">5</span></div>
```

---

## Kural 6.9: Manuel Loading State'leri Yerine useTransition Kullanın

**Etki:** DÜŞÜK  
**Etiketler:** rendering, transitions, useTransition, loading, state  

## Manuel Loading State'leri Yerine useTransition Kullanın

Loading state'leri için manuel `useState` yerine `useTransition` kullanın. Bu yerleşik `isPending` state'i sağlar ve transition'ları otomatik olarak yönetir.

**Yanlış (manuel loading state):**

```tsx
function SearchResults() {
  const [query, setQuery] = useState('')
  const [results, setResults] = useState([])
  const [isLoading, setIsLoading] = useState(false)

  const handleSearch = async (value: string) => {
    setIsLoading(true)
    setQuery(value)
    const data = await fetchResults(value)
    setResults(data)
    setIsLoading(false)
  }

  return (
    <>
      <input onChange={(e) => handleSearch(e.target.value)} />
      {isLoading && <Spinner />}
      <ResultsList results={results} />
    </>
  )
}
```

**Doğru (yerleşik pending state'i ile useTransition):**

```tsx
import { useTransition, useState } from 'react'

function SearchResults() {
  const [query, setQuery] = useState('')
  const [results, setResults] = useState([])
  const [isPending, startTransition] = useTransition()

  const handleSearch = (value: string) => {
    setQuery(value) // Input'u hemen güncelle
    
    startTransition(async () => {
      // Sonuçları fetch et ve güncelle
      const data = await fetchResults(value)
      setResults(data)
    })
  }

  return (
    <>
      <input onChange={(e) => handleSearch(e.target.value)} />
      {isPending && <Spinner />}
      <ResultsList results={results} />
    </>
  )
}
```

**Faydalar:**

- **Otomatik pending state**: `setIsLoading(true/false)` manuel olarak yönetmeye gerek yok
- **Hata dayanıklılığı**: Transition fırlatsa bile pending state doğru şekilde sıfırlanır
- **Daha iyi yanıt verebilirlik**: Güncellemeler sırasında UI'uyı yanıt verebilir tutar
- **Kesme yönetimi**: Yeni transition'lar bekleyen olanları otomatik olarak iptal eder

Referans: [useTransition](https://react.dev/reference/react/useTransition)
