---
name: red-team-tactics
description: MITRE ATT&CK'a dayalı red team taktikleri prensipleri. Saldırı aşamaları, tespit kaçırma, raporlama.
allowed-tools: Read, Glob, Grep
---

# Red Team Taktikleri (Red Team Tactics)

> MITRE ATT&CK framework'üne dayalı düşman simülasyon prensipleri.

---

## 1. MITRE ATT&CK Aşamaları

### Saldırı Yaşam Döngüsü

```
KEŞİF → İLK ERİŞİM → YÜRÜTME → KALICILIK
   ↓         ↓          ↓          ↓
YETKİ YÜKSELTİM → SAVUNMA KAÇIRMA → KİMLİK ERİŞİMİ → KEŞİF
   ↓         ↓          ↓          ↓
YANAL HAREKET → TOPLAMA → C2 → SIZMA → ETKİ
```

### Aşama Hedefleri

| Aşama | Hedef |
|-------|-------|
| **Keşif** | Saldırı yüzeyini haritalama |
| **İlk Erişim** | İlk dayanak noktasını al |
| **Yürütme** | Hedefte kod çalıştır |
| **Kalıcılık** | Yeniden başlatmaları atlatma |
| **Yetki Yükseltimi** | Admin/root al |
| **Savunma Kaçırma** | Tespiti önleme |
| **Kimlik Erişimi** | Kimlik bilgilerini toplama |
| **Keşif** | Dahili ağı haritalama |
| **Yanal Hareket** | Diğer sistemlere yayılma |
| **Toplama** | Hedef veriyi toplama |
| **C2** | Komuta kanalını sürdürme |
| **Sızma** | Veriyi çıkarma |

---

## 2. Keşif Prensipleri

### Pasif vs Aktif

| Tip | Takas |
|-----|-------|
| **Pasif** | Hedef teması yok, sınırlı bilgi |
| **Aktif** | Direkt temas, daha fazla tespit riski |

### Bilgi Hedefleri

| Kategori | Değer |
|----------|-------|
| Teknoloji yığını | Saldırı vektörü seçimi |
| Çalışan bilgisi | Sosyal mühendislik |
| Ağ aralıkları | Tarama kapsamı |
| Üçüncü taraflar | Tedarik zinciri saldırısı |

---

## 3. İlk Erişim Vektörleri

### Seçim Kriterleri

| Vektör | Ne Zaman Kullanılır |
|--------|---------------------|
| **Phishing** | İnsan hedef, e-posta erişimi |
| **Genel exploitler** | Açığa çıkan savunmasız servisler |
| **Geçerli kimlik bilgileri** | Sızdırılmış veya kırılmış |
| **Tedarik zinciri** | Üçüncü taraf erişimi |

---

## 4. Yetki Yükseltimi Prensipleri

### Windows Hedefleri

| Kontrol | Fırsat |
|---------|--------|
| Tırnak içine alınmamış servis yolları | Yola yazma |
| Zayıf servis izinleri | Servisi değiştirme |
| Token yetkiler | SeDebug vb. kötüye kullanma |
| Depolanan kimlik bilgileri | Toplama |

### Linux Hedefleri

| Kontrol | Fırsat |
|---------|--------|
| SUID binary'leri | Sahip olarak yürütme |
| Sudo yapılandırma hatası | Komut yürütme |
| Kernel güvenlik açıkları | Kernel exploitleri |
| Cron işleri | Yazılabilir script'ler |

---

## 5. Savunma Kaçırma Prensipleri

### Anahtar Teknikler

| Teknik | Amaç |
|--------|------|
| LOLBins | Meşru araçları kullanma |
| Obfuscation | Kötü niyetli kodu gizleme |
| Timestomping | Dosya değişikliklerini gizleme |
| Log temizleme | Kanıtı kaldırma |

### Operasyonel Güvenlik

- Çalışma saatlerinde çalışma
- Meşru trafik desenlerini taklit etme
- Şifreli kanallar kullanma
- Normal davranışla harmanlanma

---

## 6. Yanal Hareket Prensipleri

### Kimlik Bilgisi Tipleri

| Tip | Kullanım |
|-----|----------|
| Şifre | Standart kimlik doğrulama |
| Hash | Pass-the-hash |
| Ticket | Pass-the-ticket |
| Sertifika | Sertifika kimlik doğrulaması |

### Hareket Yolları

- Admin paylaşımları
- Uzak servisler (RDP, SSH, WinRM)
- Dahili servislerin exploitasyonu

---

## 7. Active Directory Saldırıları

### Saldırı Kategorileri

| Saldırı | Hedef |
|---------|-------|
| Kerberoasting | Servis hesabı şifreleri |
| AS-REP Roasting | Pre-auth olmayan hesaplar |
| DCSync | Domain kimlik bilgileri |
| Golden Ticket | Kalıcı domain erişimi |

---

## 8. Raporlama Prensipleri

### Saldırı Anlatımı

Tam saldırı zincirini belgele:
1. İlk erişim nasıl elde edildi
2. Hangi teknikler kullanıldı
3. Hangi hedefler başarıldı
4. Tespit nerede başarısız oldu

### Tespit Boşlukları

Her başarılı teknik için:
- Neyin tespit etmesi gerekirdi?
- Tespit neden çalışmadı?
- Tespiti nasıl iyileştirilir

---

## 9. Etik Sınırlar

### Her Zaman

- Kapsam içinde kal
- Etkiyi minimize et
- Gerçek tehdit bulunursa hemen raporla
- Tüm eylemleri belgele

### Asla

- Prodüksiyon verisini yok etme
- Hizmet reddi (scoped olmadıkça)
- Proof of concept'in ötesine erişme
- Hassas veriyi saklama

---

## 10. Anti-Desenler

| ❌ Yapma | ✅ Yap |
|----------|--------|
| Exploitasyon için acele et | Metodolojiyi takip et |
| Hasara neden ol | Etkiyi minimize et |
| Raporlamayı atla | Her şeyi belgele |
| Kapsamı görmezden gel | Sınırlar içinde kal |

---

> **Unutma:** Red team, savunmaları iyileştirmek için saldırganları simüle eder, zarar vermek için değil.
