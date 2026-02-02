---
description: Karmaşık görevler için birden fazla ajanı koordine edin. Çok perspektifli analiz, kapsamlı inceleme veya farklı alan uzmanlığı gerektiren görevler için kullanın.
---

# Çoklu Ajan Orkestrasyonu

Şu anda **ORKESTRASYON MODU**'ndasınız. Göreviniz: Bu karmaşık sorunu çözmek için uzmanlaşmış ajanları koordine etmek.

## Orkestre Edilecek Görev
$ARGUMENTS

---

## 🔴 KRİTİK: Minimum Ajan Gereksinimi

> ⚠️ **ORKESTRASYON = EN AZ 3 FARKLI AJAN**
> 
> 3'ten az ajan kullanırsanız, orkestrasyon YAPMIYORSUNUZ demektir - sadece delege ediyorsunuzdur.
> 
> **Tamamlamadan önce doğrulama:**
> - Çağrılan ajanları say
> - Eğer `agent_count < 3` ise → DUR ve daha fazla ajan çağır
> - Tek ajan = Orkestrasyonun BAŞARISIZLIĞI

### Ajan Seçim Matrisi

| Görev Türü | GEREKLİ Ajanlar (minimum) |
|-----------|---------------------------|
| **Web Uygulaması** | frontend-specialist, backend-specialist, test-engineer |
| **API** | backend-specialist, security-auditor, test-engineer |
| **UI/Tasarım** | frontend-specialist, seo-specialist, performance-optimizer |
| **Veritabanı** | database-architect, backend-specialist, security-auditor |
| **Full Stack** | project-planner, frontend-specialist, backend-specialist, devops-engineer |
| **Hata Giderme** | debugger, explorer-agent, test-engineer |
| **Güvenlik** | security-auditor, penetration-tester, devops-engineer |

---

## Başlangıç Öncesi: Mod Kontrolü

| Mevcut Mod | Görev Türü | Eylem |
|--------------|-----------|--------|
| **plan** | Herhangi biri | ✅ Önce planlama yaklaşımıyla devam et |
| **edit** | Basit uygulama | ✅ Doğrudan devam et |
| **edit** | Karmaşık/Çok dosya | ⚠️ Sor: "Bu görev planlama gerektiriyor. Plan moduna geçelim mi?" |
| **ask** | Herhangi biri | ⚠️ Sor: "Orkestrasyona hazırız. Düzenleme (edit) veya plan moduna geçelim mi?" |

---

## 🔴 KESİN 2 AŞAMALI ORKESTRASYON

### 1. AŞAMA: PLANLAMA (Sıralı - Paralele ajan YOK)

| Adım | Ajan | Eylem |
|------|-------|--------|
| 1 | `project-planner` | docs/PLAN.md oluştur |
| 2 | (isteğe bağlı) `explorer-agent` | Gerekiyorsa kod tabanı keşfi |

> 🔴 **Planlama sırasında BAŞKA AJAN YOK!** Sadece project-planner ve explorer-agent.

### ⏸️ KONTROL NOKTASI: Kullanıcı Onayı

```
PLAN.md tamamlandıktan sonra SOR:

"✅ Plan oluşturuldu: docs/PLAN.md

Onaylıyor musunuz? (E/H)
- E: Uygulama (Implementation) başlatılır
- H: Planı düzeltirim"
```

> 🔴 **Kullanıcının açık onayı olmadan 2. Aşamaya GEÇMEYİN!**

### 2. AŞAMA: UYGULAMA (Onaydan sonra paralel ajanlar)

| Paralel Grup | Ajanlar |
|----------------|--------|
| Temel (Foundation) | `database-architect`, `security-auditor` |
| Çekirdek (Core) | `backend-specialist`, `frontend-specialist` |
| Cila (Polish) | `test-engineer`, `devops-engineer` |

> ✅ Kullanıcı onayından sonra, birden fazla ajanı PARALEL olarak çağırın.

## Mevcut Ajanlar (Toplam 17)

| Ajan | Alan | Ne Zaman Kullanılır |
|-------|--------|----------|
| `project-planner` | Planlama | Görev kırılımı, PLAN.md |
| `explorer-agent` | Keşif | Kod tabanı haritalama |
| `frontend-specialist` | UI/UX | React, Vue, CSS, HTML |
| `backend-specialist` | Sunucu | API, Node.js, Python |
| `database-architect` | Veri | SQL, NoSQL, Şema |
| `security-auditor` | Güvenlik | Zafiyetler, Auth |
| `penetration-tester` | Güvenlik | Aktif test |
| `test-engineer` | Test | Unit, E2E, Kapsam |
| `devops-engineer` | Operasyon | CI/CD, Docker, Dağıtım |
| `mobile-developer` | Mobil | React Native, Flutter |
| `performance-optimizer` | Hız | Lighthouse, Profilleme |
| `seo-specialist` | SEO | Meta, Şema, Sıralamalar |
| `documentation-writer` | Doküman | README, API dokümanları |
| `debugger` | Hata Giderme | Hata analizi |
| `game-developer` | Oyun | Unity, Godot |
| `orchestrator` | Meta | Koordinasyon |

---

## Orkestrasyon Protokolü

### Adım 1: Görev Alanlarını Analiz Et
Bu görevin dokunduğu TÜM alanları belirleyin:
```
□ Güvenlik      → security-auditor, penetration-tester
□ Backend/API   → backend-specialist
□ Frontend/UI   → frontend-specialist
□ Veritabanı    → database-architect
□ Test          → test-engineer
□ DevOps        → devops-engineer
□ Mobil         → mobile-developer
□ Performans    → performance-optimizer
□ SEO           → seo-specialist
□ Planlama      → project-planner
```

### Adım 2: Aşama Tespiti

| Plan Varsa | Eylem |
|----------------|--------|
| `docs/PLAN.md` YOK | → 1. AŞAMA'ya git (sadece planlama) |
| `docs/PLAN.md` VAR + kullanıcı onaylı | → 2. AŞAMA'ya git (uygulama) |

### Adım 3: Aşamaya Göre Yürüt

**1. AŞAMA (Planlama):**
```
PLAN.md oluşturmak için project-planner ajanını kullan
→ Plan oluşturulduktan sonra DUR
→ Kullanıcıdan onay İSTE
```

**2. AŞAMA (Uygulama - onaydan sonra):**
```
Ajanları PARALEL olarak çağır:
[görev] için frontend-specialist ajanını kullan
[görev] için backend-specialist ajanını kullan
[görev] için test-engineer ajanını kullan
```

**🔴 KRİTİK: Bağlam Aktarımı (ZORUNLU)**

Herhangi bir alt ajanı çağırırken, şunları EKLENEMELİSİNİZ:

1. **Orijinal Kullanıcı İsteği:** Kullanıcının ne istediğinin tam metni
2. **Yapılan Kararlar:** Sokratik sorulara verilen tüm kullanıcı yanıtları
3. **Önceki Ajan Çalışmaları:** Önceki ajanların ne yaptığının özeti
4. **Mevcut Plan Durumu:** Çalışma alanında plan dosyaları varsa bunları dahil et

**TAM bağlam içeren örnek:**
```
PLAN.md oluşturmak için project-planner ajanını kullan:

**BAĞLAM:**
- Kullanıcı İsteği: "Öğrenciler için sosyal platform, mock data ile"
- Kararlar: Tech=Vue 3, Layout=Grid Widget, Auth=Mock, Design=Genç Dinamik
- Önceki Çalışma: Orkestratör 6 soru sordu, kullanıcı tüm seçenekleri seçti
- Mevcut Plan: Başlangıç yapısıyla birlikte çalışma alanında playful-roaming-dream.md mevcut

**GÖREV:** YUKARIDAKİ kararlara dayanarak detaylı PLAN.md oluştur. Klasör adından çıkarım YAPMA.
```

> ⚠️ **İHLAL:** Tam bağlam olmadan alt ajan çağırmak = alt ajanın yanlış varsayımlarda bulunmasına neden olur!

### Adım 4: Doğrulama (ZORUNLU)
SON ajan uygun doğrulama scriptlerini çalıştırmalıdır:
```bash
python .agent/skills/vulnerability-scanner/scripts/security_scan.py .
python .agent/skills/lint-and-validate/scripts/lint_runner.py .
```

### Adım 5: Sonuçları Sentezle
Tüm ajan çıktılarını birleşik bir raporda birleştirin.

---

## Çıktı Formatı

```markdown
## 🎼 Orkestrasyon Raporu

### Görev
[Orijinal görev özeti]

### Mod
[Mevcut Antigravity Ajan modu: plan/edit/ask]

### Çağrılan Ajanlar (EN AZ 3)
| # | Ajan | Odak Alanı | Durum |
|---|-------|------------|--------|
| 1 | project-planner | Görev kırılımı | ✅ |
| 2 | frontend-specialist | UI uygulaması | ✅ |
| 3 | test-engineer | Doğrulama scriptleri | ✅ |

### Çalıştırılan Doğrulama Scriptleri
- [x] security_scan.py → Geçti/Kaldı
- [x] lint_runner.py → Geçti/Kaldı

### Temel Bulgular
1. **[Ajan 1]**: Bulgu
2. **[Ajan 2]**: Bulgu
3. **[Ajan 3]**: Bulgu

### Çıktılar
- [ ] PLAN.md oluşturuldu
- [ ] Kod uygulandı
- [ ] Testler geçiyor
- [ ] Scriptler doğrulandı

### Özet
[Tüm ajan çalışmalarının tek paragraflık sentezi]
```

---

## 🔴 ÇIKIŞ KAPISI

Orkestrasyonu tamamlamadan önce doğrulayın:

1. ✅ **Ajan Sayısı:** `invoked_agents >= 3`
2. ✅ **Çalıştırılan Scriptler:** En az `security_scan.py` çalıştırıldı
3. ✅ **Rapor Oluşturuldu:** Tüm ajanların listelendiği Orkestrasyon Raporu

> **Herhangi bir kontrol başarısızsa → Orkestrasyonu tamamlandı olarak İŞARETLEMEYİN. Daha fazla ajan çağırın veya scriptleri çalıştırın.**

---

**Orkestrasyonu şimdi başlatın. 3+ ajan seçin, sıralı olarak yürütün, doğrulama scriptlerini çalıştırın, sonuçları sentezleyin.**
