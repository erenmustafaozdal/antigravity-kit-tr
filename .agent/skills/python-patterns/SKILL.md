---
name: python-patterns
description: Python geliştirme prensipleri ve karar verme. Framework seçimi, async desenler, tip ipuçları, proje yapısı. Düşünmeyi öğretir, kopyalamayı değil.
allowed-tools: Read, Write, Edit, Glob, Grep
---

# Python Desenleri

> 2025 için Python geliştirme prensipleri ve karar verme.
> **Kopyalamak yerine DÜŞÜNMEYİ öğren.**

---

## ⚠️ Bu Yetenek Nasıl Kullanılır

Bu yetenek **karar verme prensiplerini** öğretir, kopyalanacak sabit kod değil.

- Belirsiz olduğunda kullanıcıya framework tercihi SOR
- BAĞLAMA göre async vs sync seç
- Her seferinde aynı framework'e varsayılan olarak gitme

---

## 1. Framework Seçimi (2025)

### Karar Ağacı

```
Ne inşa ediyorsun?
│
├── API-öncelikli / Microservices
│   └── FastAPI (async, modern, hızlı)
│
├── Full-stack web / CMS / Admin
│   └── Django (pil dahil)
│
├── Basit / Script / Öğrenme
│   └── Flask (minimal, esnek)
│
├── AI/ML API servisi
│   └── FastAPI (Pydantic, async, uvicorn)
│
└── Arka plan worker'ları
    └── Celery + herhangi bir framework
```

### Karşılaştırma Prensipleri

| Faktör | FastAPI | Django | Flask |
|--------|---------|--------|-------|
| **En iyi** | API'ler, microservices | Full-stack, CMS | Basit, öğrenme |
| **Async** | Native | Django 5.0+ | Uzantılar ile |
| **Admin** | Manuel | Yerleşik | Uzantılar ile |
| **ORM** | Kendin seç | Django ORM | Kendin seç |
| **Öğrenme eğrisi** | Düşük | Orta | Düşük |

### Sorulacak Seçim Soruları:
1. Bu yalnızca API mi yoksa full-stack mi?
2. Admin arayüzü gerekli mi?
3. Takım async'e aşina mı?
4. Mevcut altyapı var mı?

---

## 2. Async vs Sync Kararı

### Async Ne Zaman Kullanılır

```
async def daha iyi when:
├── I/O-bound işlemler (veritabanı, HTTP, dosya)
├── Birçok eşzamanlı bağlantı
├── Gerçek zamanlı özellikler
├── Microservices iletişimi
└── FastAPI/Starlette/Django ASGI

def (sync) daha iyi when:
├── CPU-bound işlemler
├── Basit script'ler
├── Eski kod tabanı
├── Takım async'e aşina değil
└── Engelleyici kütüphaneler (async versiyonu yok)
```

### Altın Kural

```
I/O-bound → async (harici için bekleme)
CPU-bound → sync + multiprocessing (hesaplama)

Yapma:
├── Sync ve async'i dikkatsizce karıştırma
├── Async kodda sync kütüphaneler kullanma
└── CPU işi için async'i zorlama
```

### Async Kütüphane Seçimi

| İhtiyaç | Async Kütüphane |
|---------|-----------------|
| HTTP client | httpx |
| PostgreSQL | asyncpg |
| Redis | aioredis / redis-py async |
| File I/O | aiofiles |
| Database ORM | SQLAlchemy 2.0 async, Tortoise |

---

## 3. Tip İpuçları Stratejisi

### Ne Zaman Tip Kullanılır

```
Her zaman tiplendir:
├── Fonksiyon parametreleri
├── Dönüş tipleri
├── Sınıf attributeları
├── Public API'ler

Atlanabilir:
├── Yerel değişkenler (çıkarımın çalışmasına izin ver)
├── Tek kullanımlık script'ler
├── Testler (genellikle)
```

### Yaygın Tip Desenleri

```python
# Bunlar desenlerdir, onları anla:

# Optional → None olabilir
from typing import Optional
def find_user(id: int) -> Optional[User]: ...

# Union → birden fazla tipten biri
def process(data: str | dict) -> None: ...

# Genel koleksiyonlar
def get_items() -> list[Item]: ...
def get_mapping() -> dict[str, int]: ...

# Callable
from typing import Callable
def apply(fn: Callable[[int], str]) -> str: ...
```

### Doğrulama için Pydantic

```
Pydantic ne zaman kullanılır:
├── API istek/yanıt modelleri
├── Yapılandırma/ayarlar
├── Veri doğrulama
├── Serialization

Faydalar:
├── Çalışma zamanı doğrulama
├── Otomatik JSON şeması
├── FastAPI ile native çalışır
└── Açık hata mesajları
```

---

## 4. Proje Yapısı Prensipleri

### Yapı Seçimi

```
Küçük proje / Script:
├── main.py
├── utils.py
└── requirements.txt

Orta API:
├── app/
│   ├── __init__.py
│   ├── main.py
│   ├── models/
│   ├── routes/
│   ├── services/
│   └── schemas/
├── tests/
└── pyproject.toml

Büyük uygulama:
├── src/
│   └── myapp/
│       ├── core/
│       ├── api/
│       ├── services/
│       ├── models/
│       └── ...
├── tests/
└── pyproject.toml
```

### FastAPI Yapı Prensipleri

```
Özellik veya katmana göre organize et:

Katmana göre:
├── routes/ (API uç noktaları)
├── services/ (iş mantığı)
├── models/ (veritabanı modelleri)
├── schemas/ (Pydantic modelleri)
└── dependencies/ (paylaşılan bağımlılıklar)

Özelliğe göre:
├── users/
│   ├── routes.py
│   ├── service.py
│   └── schemas.py
└── products/
    └── ...
```

---

## 5. Django Prensipleri (2025)

### Django Async (Django 5.0+)

```
Django async'i destekler:
├── Async view'lar
├── Async middleware
├── Async ORM (sınırlı)
└── ASGI deployment

Django'da async ne zaman kullanılır:
├── Harici API çağrıları
├── WebSocket (Channels)
├── Yüksek eşzamanlılık view'ları
└── Arka plan görev tetikleme
```

### Django En İyi Uygulamaları

```
Model tasarımı:
├── Şişman modeller, ince view'lar
├── Yaygın sorgular için manager'lar kullan
├── Paylaşılan alanlar için abstract base sınıflar

View'lar:
├── Karmaşık CRUD için sınıf-tabanlı
├── Basit uç noktalar için fonksiyon-tabanlı
├── DRF ile viewset kullan

Sorgular:
├── FK'lar için select_related()
├── M2M için prefetch_related()
├── N+1 sorgularından kaçın
└── Spesifik alanlar için .only() kullan
```

---

## 6. FastAPI Prensipleri

### FastAPI'de async def vs def

```
async def ne zaman kullan:
├── Async veritabanı driver'ları kullanırken
├── Async HTTP çağrıları yaparken
├── I/O-bound işlemler
└── Eşzamanlılığı işlemek istediğinde

def ne zaman kullan:
├── Engelleyici işlemler
├── Sync veritabanı driver'ları
├── CPU-bound iş
└── FastAPI otomatik olarak threadpool'da çalıştırır
```

### Dependency Injection

```
Bağımlılıkları şunlar için kullan:
├── Veritabanı oturumları
├── Mevcut kullanıcı / Auth
├── Yapılandırma
├── Paylaşılan kaynaklar

Faydalar:
├── Test edilebilirlik (mock bağımlılıklar)
├── Temiz ayrım
├── Otomatik temizleme (yield)
```

### Pydantic v2 Entegrasyonu

```python
# FastAPI + Pydantic sıkı entegre:

# İstek doğrulama
@app.post("/users")
async def create(user: UserCreate) -> UserResponse:
    # user zaten doğrulanmış
    ...

# Yanıt serialization
# Dönüş tipi yanıt şeması olur
```

---

## 7. Arka Plan Görevleri

### Seçim Kılavuzu

| Çözüm | En İyi |
|-------|--------|
| **BackgroundTasks** | Basit, işlem içi görevler |
| **Celery** | Dağıtık, karmaşık iş akışları |
| **ARQ** | Async, Redis-tabanlı |
| **RQ** | Basit Redis kuyruğu |
| **Dramatiq** | Actor-tabanlı, Celery'den daha basit |

### Her Birini Ne Zaman Kullanmalı

```
FastAPI BackgroundTasks:
├── Hızlı işlemler
├── Kalıcılık gerekmiyor
├── Fire-and-forget
└── Aynı işlem

Celery/ARQ:
├── Uzun süren görevler
├── Retry mantığı gerekli
├── Dağıtık worker'lar
├── Kalıcı kuyruk
└── Karmaşık iş akışları
```

---

## 8. Hata Yönetimi Prensipleri

### Exception Stratejisi

```
FastAPI'de:
├── Özel exception sınıfları oluştur
├── Exception handler'ları kaydet
├── Tutarlı hata formatı döndür
└── İç detayları açığa çıkarmadan logla

Desen:
├── Servislerde domain exceptionları fırlat
├── Handler'larda yakala ve dönüştür
└── İstemci temiz hata yanıtı alır
```

### Hata Yanıtı Felsefesi

```
Dahil et:
├── Hata kodu (programatik)
├── Mesaj (insan tarafından okunabilir)
├── Detaylar (uygulanabilirse alan düzeyinde)
└── Stack trace'ler DEĞİL (güvenlik)
```

---

## 9. Test Etme Prensipleri

### Test Stratejisi

| Tip | Amaç | Araçlar |
|-----|------|---------|
| **Unit** | İş mantığı | pytest |
| **Integration** | API uç noktaları | pytest + httpx/TestClient |
| **E2E** | Tam iş akışları | pytest + DB |

### Async Test Etme

```python
# Async testler için pytest-asyncio kullan

import pytest
from httpx import AsyncClient

@pytest.mark.asyncio
async def test_endpoint():
    async with AsyncClient(app=app, base_url="http://test") as client:
        response = await client.get("/users")
        assert response.status_code == 200
```

### Fixture Stratejisi

```
Yaygın fixture'lar:
├── db_session → Veritabanı bağlantısı
├── client → Test client
├── authenticated_user → Token'lı kullanıcı
└── sample_data → Test veri kurulumu
```

---

## 10. Karar Kontrol Listesi

İmplementasyondan önce:

- [ ] **Kullanıcıya framework tercihi soruldu mu?**
- [ ] **BU bağlam için framework seçildi mi?** (sadece varsayılan değil)
- [ ] **Async vs sync kararı verildi mi?**
- [ ] **Tip ipucu stratejisi planlandı mı?**
- [ ] **Proje yapısı tanımlandı mı?**
- [ ] **Hata yönetimi planlandı mı?**
- [ ] **Arka plan görevleri düşünüldü mü?**

---

## 11. Kaçınılacak Anti-Desenler

### ❌ YAPMA:
- Basit API'ler için Django'ya varsayılan (FastAPI daha iyi olabilir)
- Async kodda sync kütüphaneler kullan
- Public API'ler için tip ipuçlarını atla
- İş mantığını route'lara/view'lara koy
- N+1 sorgularını görmezden gel
- Async ve sync'i dikkatsizce karıştır

### ✅ YAP:
- Bağlama göre framework seç
- Async gereksinimleri hakkında sor
- Doğrulama için Pydantic kullan
- Endişeleri ayır (routes → services → repos)
- Kritik yolları test et

---

> **Unutma**: Python desenleri SENİN spesifik bağlamın için karar verme ile ilgilidir. Kod kopyalama—uygulamana en iyi hizmet edecek şey hakkında düşün.
