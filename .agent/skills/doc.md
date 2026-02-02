# Antigravity Yetenekler (Skills)

> **Antigravity Kit'te Yetenek (Skill) oluşturma ve kullanma rehberi**

---

## 📋 Tanıtım

Antigravity'nin temel modelleri (Gemini gibi) güçlü ve çok yönlü modeller olsa da, projenizin özel bağlamını veya ekibinizin standartlarını başlangıçta bilemezler. Her kuralı veya aracı doğrudan ajanın bağlam penceresine yüklemek "araç şişmesine" (tool bloat), yüksek maliyetlere, gecikmelere ve karmaşıklığa neden olur.

**Antigravity Yetenekleri (Skills)**, bu sorunu **Kademeli Açıklama (Progressive Disclosure)** özelliği ile çözer. Bir yetenek, ihtiyaç duyulana kadar inaktif durumda bekleyen uzmanlaşmış bir bilgi paketidir. Bu bilgiler, sadece sizin özel isteğiniz yeteneğin açıklama kısmıyla eşleştiğinde ajanın bağlamına yüklenir.

---

## 📁 Yapı ve Kapsam

Yetenekler, dizin tabanlı paketlerdir. İhtiyaçlarınıza göre bu kapsamları belirleyebilirsiniz:

| Kapsam | Yol | Açıklama |
|---------|-----------|-------|
| **Çalışma Alanı (Workspace)** | `<workspace-root>/.agent/skills/` | Sadece belirli bir projeye özel |

### Yetenek Dizin Yapısı

```
my-skill/
├── SKILL.md      # (Zorunlu) Metadata ve talimatlar
├── scripts/      # (Opsiyonel) Python veya Bash scriptleri
├── references/   # (Opsiyonel) Metinler, dökümanlar, şablonlar
└── assets/       # (Opsiyonel) Görseller veya logolar
```

---

## 🔍 Örnek 1: Kod İnceleme Yeteneği (Code Review Skill)

Bu, sadece talimat içeren (instruction-only) bir yetenektir; sadece `SKILL.md` dosyasını oluşturmak yeterlidir.

### Adım 1: Dizini Oluşturun

```bash
mkdir -p .agent/skills/code-review
```

### Adım 2: SKILL.md Dosyasını Oluşturun

```markdown
---
name: code-review
description: Kod değişikliklerini hatalar, stil sorunları ve en iyi pratikler açısından inceler. PR'ları gözden geçirirken veya kod kalitesini kontrol ederken kullanın.
---

# Kod İnceleme Yeteneği

Kod incelerken şu adımları takip edin:

## İnceleme Kontrol Listesi

1. **Doğruluk**: Kod yapması gereken işi yapıyor mu?
2. **Uç Durumlar**: Hata durumları yönetilmiş mi?
3. **Stil**: Proje standartlarına uyuyor mu?
4. **Performans**: Belirgin verimsizlikler var mı?

## Geri Bildirim Nasıl Verilmeli?

- Neyin değişmesi gerektiği konusunda spesifik olun.
- Sadece "ne" olduğunu değil, "neden" olduğunu da açıklayın.
- Mümkünse alternatifler önerin.
```

> **Not**: `SKILL.md` dosyası en üstte metadata (ad, açıklama) içerir, ardından talimatlar gelir. Ajan sadece metadata kısmını okur ve talimatları sadece gerektiğinde yükler.

### Deneyin

`demo_bad_code.py` dosyasını oluşturun:

```python
import time

def get_user_data(users, id):
    # ID ile kullanıcıyı bul
    for u in users:
        if u['id'] == id:
            return u
    return None

def process_payments(items):
    total = 0
    for i in items:
        # Vergiyi hesapla
        tax = i['price'] * 0.1
        total = total + i['price'] + tax
        time.sleep(0.1)  # Yavaş ağ çağrısını simüle et
    return total

def run_batch():
    users = [{'id': 1, 'name': 'Alice'}, {'id': 2, 'name': 'Bob'}]
    items = [{'price': 10}, {'price': 20}, {'price': 100}]
    
    u = get_user_data(users, 3)
    print("User found: " + u['name'])  # None gelirse çökecek
    
    print("Total: " + str(process_payments(items)))

if __name__ == "__main__":
    run_batch()
```

**İstek**: `@demo_bad_code.py dosyasını incele`

Ajan otomatik olarak `code-review` yeteneğini tespit edecek, bilgileri yükleyecek ve talimatlara göre incelemeyi yapacaktır.

---

## 📄 Örnek 2: Lisans Başlığı Yeteneği (License Header Skill)

Bu yetenek, `resources/` dizini altındaki bir referans dosyasını kullanır.

### Adım 1: Dizini Oluşturun

```bash
mkdir -p .agent/skills/license-header-adder/resources
```

### Adım 2: Şablon Dosyasını Oluşturun

**`.agent/skills/license-header-adder/resources/HEADER.txt`**:

```
/*
 * Telif Hakkı (c) 2026 ŞİRKET_ADINIZ LLC.
 * Tüm hakları saklıdır.
 * Bu kod tescilli ve gizlidir.
 */
```

### Adım 3: SKILL.md Dosyasını Oluşturun

**`.agent/skills/license-header-adder/SKILL.md`**:

```markdown
---
name: license-header-adder
description: Yeni kaynak dosyalarına standart kurumsal lisans başlığını ekler.
---

# Lisans Başlığı Ekleyici

Bu yetenek, tüm yeni kaynak dosyalarının doğru telif hakkı başlığına sahip olmasını sağlar.

## Talimatlar

1. **Şablonu Oku**: `resources/HEADER.txt` içeriğini okuyun.
2. **Dosyaya Uygula**: Yeni bir dosya oluştururken, bu içeriği aynen başa ekleyin.
3. **Sözdizimini Uyarlayın**: 
   - C tarzı diller (Java, TS) için `/* */` bloğunu koruyun.
   - Python/Shell için `#` yorum satırlarına dönüştürün.
```

### Deneyin

**İstek**: `'Hello World' yazdıran data_processor.py adında yeni bir Python betiği oluştur.`

Ajan şablonu okuyacak, yorum satırlarını Python stiline çevirecek ve otomatik olarak dosyanın başına ekleyecektir.

---

## 🎯 Sonuç

Yetenekler oluşturarak, genel bir YZ modelini projeniz için bir uzmana dönüştürmüş olursunuz:

- ✅ En iyi pratikleri sistemleştirmiş olursunuz.
- ✅ Kod inceleme kurallarına uyulmasını sağlarsınız.
- ✅ Lisans başlıklarını otomatik eklersiniz.
- ✅ Ajan, ekibinizle nasıl çalışması gerektiğini otomatik olarak bilir.

Sürekli "lisans eklemeyi unutma" veya "commit formatını düzelt" demek yerine, artık ajan bunu otomatik olarak yapacaktır!