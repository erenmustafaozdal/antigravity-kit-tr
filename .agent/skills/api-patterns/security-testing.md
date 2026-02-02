# API Güvenlik Testi

> API güvenliğini test etme prensipleri. OWASP API Top 10, kimlik doğrulama (auth) ve yetkilendirme (authz) testleri.

---

## OWASP API Güvenliği İlk 10 (Top 10)

| Zafiyet | Test Odağı |
|---------------|------------|
| **API1: BOLA** | Diğer kullanıcıların kaynaklarına erişim (Broken Object Level Authorization) |
| **API2: Broken Auth** | JWT, oturum, kimlik bilgileri yönetimi |
| **API3: Property Auth** | Toplu atama (Mass assignment), hassas veri sızıntısı |
| **API4: Kaynak Tüketimi** | İstek sınırlama (Rate limiting), Hizmet Engelleme (DoS) |
| **API5: Fonksiyon Yetkilendirme** | Admin uç noktaları, rol atlatma (Function Level Auth) |
| **API6: İş Akışı (Business Flow)** | Mantık suiistimali, otomasyon |
| **API7: SSRF** | Dahili ağ erişimi (Sunucu taraflı istek sahteciliği) |
| **API8: Yanlış Yapılandırma** | Hata ayıklama (Debug) uç noktaları, CORS hataları |
| **API9: Envanter Yönetimi** | Gölge (Shadow) API'ler, eski versiyonlar |
| **API10: Güvensiz Tüketim** | Üçüncü taraf API'lere duyulan aşırı güven |

---

## Kimlik Doğrulama (Authentication) Testi

### JWT Testleri

| Kontrol | Ne Test Edilmeli? |
|-------|--------------|
| Algoritma | "None" algoritması, algoritma karışıklığı (confusion) |
| Sır (Secret) | Zayıf sırlar, kaba kuvvet (brute force) |
| Veriler (Claims) | Son kullanma (expiration), yayıncı (issuer), hedef kitle (audience) |
| İmza | Manipülasyon, anahtar enjeksiyonu |

### Oturum (Session) Testleri

| Kontrol | Ne Test Edilmeli? |
|-------|--------------|
| Oluşturma | Tahmin edilebilirlik |
| Depolama | İstemci tarafı güvenliği (HttpOnly, Secure vb.) |
| Sonlanma | Zaman aşımı (Timeout) zorunluluğu |
| Geçersiz Kılma | Çıkış yapmanın (Logout) etkinliği |

---

## Yetkilendirme (Authorization) Testi

| Test Türü | Yaklaşım |
|-----------|----------|
| **Yatay (Horizontal)** | Aynı seviyedeki diğer kullanıcıların verilerine erişim |
| **Dikey (Vertical)** | Daha yüksek yetkili fonksiyonlara (örn. admin) erişim |
| **Bağlamsal (Context)** | İzin verilen kapsam dışındaki verilere erişim |

### BOLA/IDOR Test Akışı

1. İsteklerdeki kaynak ID'lerini belirleyin.
2. A kullanıcısının oturumuyla isteği yakalayın.
3. B kullanıcısının ID'sini kullanarak isteği tekrar gönderin.
4. Yetkisiz erişim sağlanıp sağlanmadığını kontrol edin.

---

## Girdi Doğrulama (Input Validation) Testi

| Enjeksiyon Türü | Test Odağı |
|----------------|------------|
| SQL | Sorgu manipülasyonu |
| NoSQL | Doküman sorguları |
| Komut (Command) | Sistem komutları çalıştırma |
| LDAP | Dizin sorguları |

**Yaklaşım:** Tüm parametreleri test edin, veri tipi zorlaması yapın, sınır değerleri test edin, hata mesajlarını inceleyin.

---

## İstek Sınırlama (Rate Limiting) Testi

| Pozisyon | Kontrol |
|--------|-------|
| Varlık | Herhangi bir limit var mı? |
| Atlatma (Bypass) | Header'lar, IP rotasyonu |
| Kapsam | Kullanıcı bazlı, IP bazlı, global |

**Atlatma teknikleri:** `X-Forwarded-For` kullanımı, farklı HTTP metotları, büyük/küçük harf varyasyonları, API versiyonlama.

---

## GraphQL Güvenliği

| Test | Odak |
|------|-------|
| İnceleme (Introspection) | Şema sızıntısı |
| Toplu İşlem (Batching) | Sorgu tabanlı DoS |
| İç İçe Yapı (Nesting) | Derinlik tabanlı DoS |
| Yetkilendirme | Alan (field) bazlı erişim kontrolü |

---

## Güvenlik Testi Kontrol Listesi

**Kimlik Doğrulama (Auth):**
- [ ] Atlatma (bypass) senaryoları test edildi mi?
- [ ] Kimlik bilgisi gücü kontrol edildi mi?
- [ ] Token güvenliği doğrulandı mı?

**Yetkilendirme (Authz):**
- [ ] BOLA/IDOR testleri yapıldı mı?
- [ ] Yetki yükseltme (privilege escalation) kontrol edildi mi?
- [ ] Fonksiyon bazlı erişim doğrulandı mı?

**Girdi (Input):**
- [ ] Tüm parametreler test edildi mi?
- [ ] Enjeksiyon zafiyetleri kontrol edildi mi?

**Yapılandırma (Config):**
- [ ] CORS ayarları kontrol edildi mi?
- [ ] Güvenlik header'ları (HSTS, CSP vb.) doğrulandı mı?
- [ ] Hata yönetimi (error handling) test edildi mi?

---

> **Unutma:** API'ler modern uygulamaların omurgasıdır. Onları saldırganların gözüyle test edin.
