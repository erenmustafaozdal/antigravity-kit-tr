# 2. Paket Boyutu Optimizasyonu (Bundle Size Optimization)

> **Etki:** KRİTİK
> **Odak:** İlk paket boyutunu azaltmak, Time to Interactive ve Largest Contentful Paint'i iyileştirir.

---

## Genel Bakış

Bu bölüm, paket boyutu optimizasyonuna odaklanan **5 kural** içerir.

---

## Kural 2.1: Barrel Dosya Import'larından Kaçının

**Etki:** KRİTİK  
**Etiketler:** bundle, imports, tree-shaking, barrel-files, performance  

## Barrel Dosya Import'larından Kaçının

Binlerce kullanılmayan modülü yüklemekten kaçınmak için barrel dosyalardan değil, doğrudan kaynak dosyalardan import edin. **Barrel dosyalar**, birden fazla modülü yeniden export eden giriş noktalarıdır (örn. `export * from './module'` yapan `index.js`).

Popüler ikon ve component kütüphaneleri, giriş dosyalarında **10,000'e kadar yeniden export'a** sahip olabilir. Birçok React paketi için, **bunları import etmek 200-800ms sürüyor** ve hem geliştirme hızını hem üretim soğuk başlatmalarını etkiliyor.

**Neden tree-shaking yardımcı olmuyor:** Bir kütüphane external (paketlenm

emiş) olarak işaretlendiğinde, bundler onu optimize edemez. Tree-shaking'i etkinleştirmek için paketlerseniz, build'ler tüm modül grafiğini analiz ederken önemli ölçüde yavaşlar.

**Yanlış (tüm kütüphaneyi import eder):**

```tsx
import { Check, X, Menu } from 'lucide-react'
// 1,583 modül yükler, dev'de ~2.8sn ekstra sürer
// Runtime maliyeti: Her soğuk başlatmada 200-800ms

import { Button, TextField } from '@mui/material'
// 2,225 modül yükler, dev'de ~4.2sn ekstra sürer
```

**Doğru (yalnızca ihtiyacınız olanı import eder):**

```tsx
import Check from 'lucide-react/dist/esm/icons/check'
import X from 'lucide-react/dist/esm/icons/x'
import Menu from 'lucide-react/dist/esm/icons/menu'
// Yalnızca 3 modül yükler (~2KB vs ~1MB)

import Button from '@mui/material/Button'
import TextField from '@mui/material/TextField'
// Yalnızca kullandığınızı yükler
```

**Alternatif (Next.js 13.5+):**

```js
// next.config.js - optimizePackageImports kullanın
module.exports = {
  experimental: {
    optimizePackageImports: ['lucide-react', '@mui/material']
  }
}

// Sonra ergonomik barrel import'ları kullanmaya devam edebilirsiniz:
import { Check, X, Menu } from 'lucide-react'
// Build zamanında otomatik olarak doğrudan import'lara çevrilir
```

Doğrudan import'lar %15-70 daha hızlı dev boot, %28 daha hızlı build'ler, %40 daha hızlı soğuk başlatma ve önemli ölçüde daha hızlı HMR sağlar.

Yaygın olarak etkilenen kütüphaneler: `lucide-react`, `@mui/material`, `@mui/icons-material`, `@tabler/icons-react`, `react-icons`, `@headlessui/react`, `@radix-ui/react-*`, `lodash`, `ramda`, `date-fns`, `rxjs`, `react-use`.

Referans: [How we optimized package imports in Next.js](https://vercel.com/blog/how-we-optimized-package-imports-in-next-js)

---

## Kural 2.2: Koşullu Modül Yükleme

**Etki:** YÜKSEK  
**Etiketler:** bundle, conditional-loading, lazy-loading  

## Koşullu Modül Yükleme

Büyük veri veya modülleri yalnızca bir özellik etkinleştirildiğinde yükleyin.

**Örnek (animasyon karelerini lazy-load etme):**

```tsx
function AnimationPlayer({ enabled, setEnabled }: { enabled: boolean; setEnabled: React.Dispatch<React.SetStateAction<boolean>> }) {
  const [frames, setFrames] = useState<Frame[] | null>(null)

  useEffect(() => {
    if (enabled && !frames && typeof window !== 'undefined') {
      import('./animation-frames.js')
        .then(mod => setFrames(mod.frames))
        .catch(() => setEnabled(false))
    }
  }, [enabled, frames, setEnabled])

  if (!frames) return <Skeleton />
  return <Canvas frames={frames} />
}
```

`typeof window !== 'undefined'` kontrolü, bu modülün SSR için paketlenmesini önleyerek sunucu paketi boyutunu ve build hızını optimize eder.

---

## Kural 2.3: Kritik Olmayan Üçüncü Parti Kütüphaneleri Erteleyin

**Etki:** ORTA  
**Etiketler:** bundle, third-party, analytics, defer  

## Kritik Olmayan Üçüncü Parti Kütüphaneleri Erteleyin

Analytics, logging ve hata izleme kullanıcı etkileşimini bloklamaz. Bunları hydration'dan sonra yükleyin.

**Yanlış (ilk paketi bloklar):**

```tsx
import { Analytics } from '@vercel/analytics/react'

export default function RootLayout({ children }) {
  return (
    <html>
      <body>
        {children}
        <Analytics />
      </body>
    </html>
  )
}
```

**Doğru (hydration'dan sonra yüklenir):**

```tsx
import dynamic from 'next/dynamic'

const Analytics = dynamic(
  () => import('@vercel/analytics/react').then(m => m.Analytics),
  { ssr: false }
)

export default function RootLayout({ children }) {
  return (
    <html>
      <body>
        {children}
        <Analytics />
      </body>
    </html>
  )
}
```

---

## Kural 2.4: Ağır Componentler İçin Dinamik Import'lar

**Etki:** KRİTİK  
**Etiketler:** bundle, dynamic-import, code-splitting, next-dynamic  

## Ağır Componentler İçin Dinamik Import'lar

İlk render'da gerekli olmayan büyük componentleri lazy-load etmek için `next/dynamic` kullanın.

**Yanlış (Monaco ana chunk ile birlikte paketlenir ~300KB):**

```tsx
import { MonacoEditor } from './monaco-editor'

function CodePanel({ code }: { code: string }) {
  return <MonacoEditor value={code} />
}
```

**Doğru (Monaco talep üzerine yüklenir):**

```tsx
import dynamic from 'next/dynamic'

const MonacoEditor = dynamic(
  () => import('./monaco-editor').then(m => m.MonacoEditor),
  { ssr: false }
)

function CodePanel({ code }: { code: string }) {
  return <MonacoEditor value={code} />
}
```

---

## Kural 2.5: Kullanıcı Niyetine Göre Ön Yükleme

**Etki:** ORTA  
**Etiketler:** bundle, preload, user-intent, hover  

## Kullanıcı Niyetine Göre Ön Yükleme

Algılanan gecikmeyi azaltmak için ağır paketleri ihtiyaç duyulmadan önce ön yükleyin.

**Örnek (hover/focus'ta ön yükleme):**

```tsx
function EditorButton({ onClick }: { onClick: () => void }) {
  const preload = () => {
    if (typeof window !== 'undefined') {
      void import('./monaco-editor')
    }
  }

  return (
    <button
      onMouseEnter={preload}
      onFocus={preload}
      onClick={onClick}
    >
      Editörü Aç
    </button>
  )
}
```

**Örnek (özellik bayrağı etkinleştirildiğinde ön yükleme):**

```tsx
function FlagsProvider({ children, flags }: Props) {
  useEffect(() => {
    if (flags.editorEnabled && typeof window !== 'undefined') {
      void import('./monaco-editor').then(mod => mod.init())
    }
  }, [flags.editorEnabled])

  return <FlagsContext.Provider value={flags}>
    {children}
  </FlagsContext.Provider>
}
```

`typeof window !== 'undefined'` kontrolü, ön yüklenen modüllerin SSR için paketlenmesini önleyerek sunucu paketi boyutunu ve build hızını optimize eder.
