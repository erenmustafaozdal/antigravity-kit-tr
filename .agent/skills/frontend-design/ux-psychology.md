# UX Psikolojisi Referansı

> UX yasaları, duygusal tasarım, güven inşası ve davranışsal psikoloji üzerine derinlemesine inceleme.

---

## 1. Temel UX Yasaları

### Hick Yasası

**Prensip:** Bir karar verme süresi, seçenek sayısıyla logaritmik olarak artar.

```
Karar Süresi = a + b × log₂(n + 1)
n = seçenek sayısı
```

**Uygulama:**
- Navigasyon: En fazla 5-7 ana öğe bulundurun.
- Formlar: Adımlara bölün (kademeli açıklama - progressive disclosure).
- Seçenekler: Mümkünse varsayılan seçimler sunun.
- Filtreler: En çok kullanılanlara öncelik verin, gelişmiş olanları gizleyin.

**Örnek:**
```
❌ Kötü: Tek bir menüde 15 öğe.
✅ İyi: 5 ana kategori + "Daha Fazla" seçeneği.

❌ Kötü: Aynı anda 20 form alanı göstermek.
✅ İyi: Her biri 5-7 alan içeren 3 adımlı bir sihirbaz (wizard).
```

---

### Fitts Yasası

**Prensip:** Bir hedefe ulaşma süresi, mesafe ve boyutun bir fonksiyonudur.

```
Ulaşma Süresi = a + b × log₂(1 + D/W)
D = mesafe, W = genişlik
```

**Uygulama:**
- CTA'ler: Birincil butonları daha büyük yapın (en az 44px yükseklik).
- Dokunma hedefleri: Mobilde minimum 44×44px alan sağlayın.
- Yerleşim: Önemli eylemleri doğal imleç konumuna yakın tutun.
- Köşeler: "Sihirli köşeler" (sonsuz kenar = vurması kolay).

**Buton Boyutlandırma:**
```css
/* Önem sırasına göre boyutlandırın */
.btn-primary { height: 48px; padding: 0 24px; }
.btn-secondary { height: 40px; padding: 0 16px; }
.btn-tertiary { height: 36px; padding: 0 12px; }

/* Mobil dokunma hedefleri */
@media (hover: none) {
  .btn { min-height: 44px; min-width: 44px; }
}
```

---

### Miller Yasası

**Prensip:** Ortalama bir insan, çalışma belleğinde 7±2 birim (chunk) bilgi tutabilir.

**Uygulama:**
- Listeler: 5-7 öğelik gruplara (chunks) bölün.
- Navigasyon: En fazla 7 menü öğesi kullanın.
- İçerik: Uzun metinleri başlıklarla parçalara ayırın.
- Telefon numaraları: 555-123-4567 şeklinde gruplandırın.

**Gruplandırma (Chunking) Örneği:**
```
❌ 5551234567
✅ 555-123-4567

❌ Ara vermeden yazılmış uzun bir paragraf.
✅ Kısa paragraflar.
   Madde işaretleri.
   Ve alt başlıklar.
```

---

### Von Restorff Etkisi (İzolasyon Etkisi)

**Prensip:** Diğerlerinden farklı duran bir öğenin hatırlanma olasılığı daha yüksektir.

**Uygulama:**
- CTA butonları: Diğer öğelerden farklı, belirgin bir renk kullanın.
- Fiyatlandırma: Önerilen/Popüler planı vurgulayın.
- Kritik Bilgi: Görsel olarak ayrıştırın.
- Yeni Özellikler: "Yeni" rozeti veya belirgin bir vurgu ekleyin.

**Örnek:**
```css
/* Tüm butonlar gri, birincil olan öne çıkıyor */
.btn { background: #E5E7EB; }
.btn-primary { background: #3B82F6; }

/* Önerilen planın vurgulanması */
.pricing-card { border: 1px solid #E5E7EB; }
.pricing-card.popular { 
  border: 2px solid #3B82F6;
  box-shadow: var(--shadow-lg);
}
```

---

### Seri Konum (Serial Position) Etkisi

**Prensip:** Bir listenin başındaki (primacy) ve sonundaki (recency) öğeler en iyi hatırlananlardır.

**Uygulama:**
- Navigasyon: En önemli öğeleri en başa ve en sona koyun.
- Listeler: Kritik bilgiyi listenin başında veya sonunda verin.
- Formlar: En kritik alanları başlangıca yerleştirin.
- CTA'ler: Uzun sayfalarda hem üstte hem altta eylem butonu bulundurun.

**Örnek:**
```
Navigasyon: Ana Sayfa | [diğer öğeler] | İletişim

Uzun Açılış Sayfası:
- Hero alanında CTA (üstte)
- İçerik bölümleri
- Sayfanın en altında tekrarlanan CTA
```

### Jakob Yasası

**Prensip:** Kullanıcılar zamanlarının çoğunu diğer sitelerde geçirirler. Sizin sitenizin de bildikleri ve alıştıkları diğer siteler gibi çalışmasını tercih ederler.

**Uygulama:**
- **Desenler:** Arama çubuğu ve sepet gibi öğeler için standart yerleşimleri kullanın.
- **Zihinsel Modeller:** Tanıdık ikonlar kullanın (örneğin arama için büyüteç).
- **Kelime Seçimi:** "Portala Giriş Yap" yerine "Giriş Yap" kullanın.
- **Düzen:** "Ana Sayfa" navigasyonu için logoyu sol üstte tutun.
- **Etkileşim:** Geri/İleri gitmek için kaydırma (swipe) hareketi doğal hissettirmeli.
- **Geri Bildirim:** Standart renkler kullanın (Kırmızı = Hata, Yeşil = Başarı).

**Örnek:**
```
❌ Kötü: Logoya tıklandığında "Hakkımızda" sayfasına giden bir site.
✅ İyi: Logoya tıklamak her zaman kullanıcıyı Ana Sayfaya döndürür.

❌ Kötü: "Silme" işlemini temsil etmek için "Yıldız" ikonu kullanmak.
✅ İyi: "Silme" işlemi için "Çöp Kutusu" ikonu kullanmak.
```

---

### Tesler Yasası (Karmaşıklığın Korunması)

**Prensip:** Her sistem için azaltılamayan, sadece kullanıcıdan yazılıma aktarılabilen belirli bir karmaşıklık miktarı vardır.

**Uygulama:**
- **Arka Plan:** Biçimlendirme işlemlerini sisteme bırakın (örneğin para birimi sembolü).
- **Tespit:** Kart türünü veya posta kodundan şehri otomatik olarak algılayın.
- **Otomasyon:** Geri dönen kullanıcı verilerini önceden doldurun.
- **Kişiselleştirme:** Önceki yanıtlara göre sadece ilgili form alanlarını gösterin.
- **Varsayılanlar:** Yaygın ayarlar için akıllı varsayılanlar sunun.
- **Entegrasyon:** Kayıt zahmetini azaltmak için SSO (Sosyal Girişler) kullanın.

**Örnek:**
```
❌ Kötü: Kullanıcıyı formdaki her fiyat alanına "TL" yazmaya zorlamak.
✅ İyi: Uygulamanın, konum bilgisini alarak para birimi sembolünü otomatik eklemesi.

❌ Kötü: Kullanıcıyı "Kart Türü"nü (Visa/Mastercard) manuel seçmeye zorlamak.
✅ İyi: Kart numarasının ilk dört hanesinden kart türünü otomatik algılamak.
```

---

### Parkinson Yasası

**Prensip:** Herhangi bir görev, mevcut olan tüm zamanı bitirene kadar genişler.

**Uygulama:**
- **Verimlilik:** Görev tamamlama süresini azaltmak için "Otomatik Kaydet" kullanın.
- **Hız:** Dönüşüm hunisindeki (conversion funnel) adım sayısını sınırlandırın.
- **Netlik:** Anlamı çözmek için "üzerine gelip bekleme" zahmetini önlemek adına net etiketler kullanın.
- **Geri Bildirim:** Kullanıcıların hatalarla vakit kaybetmesini önlemek için gerçek zamanlı doğrulama (validation) yapın.
- **Onboarding:** Profesyonel kullanıcılar için hızlı "Ekspres" kurulum sunun.
- **Kısıtlar:** Düşünceleri odaklamak için giriş alanlarına karakter sınırları koyun.

**Örnek:**
```
❌ Kötü: Kullanıcının sayfadan ayrılıp veri kaybetmesine izin veren 10 sayfalık bir kayıt formu.
✅ İyi: Google veya Apple Kimliği ile "Tek Tıkla Kayıt".

❌ Kötü: Kullanıcıya biyografi yazması için sınırsız süre ve boş alan verme.
✅ İyi: Saniyeler içinde bitirmelerine yardımcı olacak "Önerilen Biyografiler" özelliği sunma.
```

---

### Doherty Eşiği

**Prensip:** Bilgisayar ve kullanıcı arasındaki etkileşim hızı 400ms'nin altına düştüğünde, her iki tarafın da birbirini beklemediği bir tempoda verimlilik tavan yapar.

**Uygulama:**
- **Geri Bildirim:** Tıklamalar için anında görsel ipuçları kullanın.
- **Yükleme:** Algılanan performansı artırmak için skeleton ekranlar kullanın.
- **İyimserlik (Optimism):** Sunucu yanıt vermeden önce arayüzü güncelleyin (Optimistic UI).
- **Hareket:** Hafif gecikmeleri maskelemek için mikro-animasyonlar kullanın.
- **Önbelleğe Alma:** Sonraki sayfaları veya varlıkları arka planda önceden yükleyin.
- **Önceliklendirme:** Ağır ve yüksek çözünürlüklü görsellerden önce metin içeriğini yükleyin.

**Örnek:**
```
❌ Kötü: Tıklandıktan sonra 2 saniye boyunca hiçbir şey yapmayan bir buton.
✅ İyi: Tıklandığı an rengi değişen ve "Yükleniyor" ikonunu gösteren bir buton.

❌ Kötü: Veri çekilirken görünen boş beyaz bir ekran.
✅ İyi: İçeriğin nerede görüneceğini gri hatlarla gösteren bir skeleton ekran.
```

---

### Postel Yasası (Sağlamlık Prensibi)

**Prensip:** Kendi yaptığınız işlerde muhafazakar, başkalarından kabul ettiğiniz girdilerde cömert olun.

**Uygulama:**
- **Hata Yönetimi:** Eksik bir boşluk veya çizgi için hata vermeyin.
- **Biçimlendirme:** Tarihleri GG/AA/YYYY veya AA/GG/YYYY formatlarında kabul edin.
- **Girdiler:** Başta ve sondaki boşlukları otomatik olarak temizleyin (strip).
- **Yedekler (Fallbacks):** Kullanıcı fotoğraf yüklemediyse varsayılan bir profil resmi (avatar) kullanın.
- **Arama:** Yazım hatalarını kabul edin ve "Bunu mu demek istediniz?" önerileri sunun.
- **Erişilebilirlik:** Sitenin tüm tarayıcılarda ve cihazlarda çalıştığından emin olun.

**Örnek:**
```
❌ Kötü: Kullanıcı boşluk bıraktığı için telefon numarasını reddetmek.
✅ İyi: Girdiyi kabul edip boşlukları sistem tarafında otomatik temizlemek.

❌ Kötü: Kullanıcıyı "01" veya "Oca" yerine "Ocak" yazmaya zorlamak.
✅ İyi: Üç formatı da anlayan bir tarih alanı.
```

---

### Occam'ın Usturası (Occam’s Razor)

**Prensip:** Eşit derecede iyi tahmin yürüten hipotezler arasında, en az varsayım içeren seçilmelidir. En basit çözüm genellikle en iyisidir.

**Uygulama:**
- **Mantık:** Gereksiz tıklamaları kaldırın.
- **Görseller:** Sadece kesinlikle gerekli olan kadar font ve renk kullanın.
- **Fonksiyon:** Eğer bir alan iki işi yapabiliyorsa, onları birleştirin.
- **Metin:** Anlamı iletmek için mümkün olan en kısa metni kullanın.
- **Düzen:** Bir amaca hizmet etmeyen dekoratif öğeleri çıkarın.
- **Akış:** Kesinlikle gerekli olmadıkça dallanan yollardan kaçının.

**Örnek:**
```
❌ Kötü: Önce yeni sayfa açan, sonra e-posta, sonra şifre soran bir "Giriş" butonu.
✅ İyi: Tek bir ekran üzerinde her ikisini de soran tek bir giriş modülü.

❌ Kötü: Tek bir kart üzerinde 5 farklı font boyutu ve 4 renk kullanmak.
✅ İyi: 2 font boyutu ve 1 vurgu rengi kullanmak.
```

---

## 2. Görsel Algı (Gestalt Prensipleri)

### Yakınlık Yasası (Law of Proximity)

**Prensip:** Birbirine yakın olan nesneler, bir grup olarak algılanma eğilimindedir.

**Uygulama:**
- **Gruplandırma:** Etiketleri (labels) giriş alanlarına fiziksel olarak yakın tutun.
- **Boşluklandırma:** Birbiriyle ilgisiz içerik blokları arasında daha geniş marjlar bırakın.
- **Kartlar:** Kart içindeki metin, görsele kenarlıktan daha yakın olmalıdır.
- **Footer'lar:** Yasal linkleri, sosyal medya linklerinden ayrı bir yerde kümeleyin.
- **Navigasyon:** "Kullanıcı" ayarlarını "Uygulama" ayarlarından ayrı gruplandırın.
- **Formlar:** Adres alanlarını bir arada, Kredi Kartı alanlarını ayrı gruplandırın.

**Örnek:**
```
❌ Kötü: Bir formdaki her satır arasında eşit ve geniş boşluklar bırakmak.
✅ İyi: Etiket ile giriş alanı arasında dar boşluk, çiftler arasında ise geniş boşluk bırakmak.

❌ Kötü: Sayfanın ortasında, formdan çok uzakta duran bir "Gönder" butonu.
✅ İyi: "Gönder" butonunun son giriş alanının hemen altına yerleştirilmesi.
```

---

### Benzerlik Yasası (Law of Similarity)

**Prensip:** İnsan gözü, tasarımdaki benzer öğeleri, birbirinden ayrı olsalar bile tek bir resim, şekil veya grup olarak algılama eğilimindedir.

**Uygulama:**
- **Tutarlılık:** Tüm tıklanabilir linkler için tutarlı renkler kullanın.
- **İkonografi:** Bir setteki tüm ikonlar aynı çizgi kalınlığına (stroke weight) sahip olmalıdır.
- **Butonlar:** Aynı öneme sahip butonlar için aynı şekil ve boyutu kullanın.
- **Tipografi:** Tüm bölüm başlıkları için aynı H2 stilini kullanın.
- **Geri Bildirim:** Tüm "Sil" işlemleri aynı rengi (örneğin Kırmızı) kullanmalıdır.
- **Durumlar (States):** Hover (üzerine gelme) ve Active (basılma) durumları uygulama genelinde tutarlı olmalıdır.

**Örnek:**
```
❌ Kötü: Bazı linklerin mavi, bazılarının yeşil, bazılarının ise sadece kalın siyah olması.
✅ İyi: Uygulamadaki her tıklanabilir metin öğesinin aynı Mavi tonunda olması.

❌ Kötü: "Gönder" için "Mavi Buton", "İptal" için de yine aynı "Mavi Buton" kullanmak.
✅ İyi: "Gönder" butonunun dolu Mavi, "İptal" butonunun ise Mavi Çerçeveli (Ghost Button) olması.
```

---

### Ortak Bölge Yasası (Law of Common Region)

**Prensip:** Öğeler, net sınırları olan bir alanı paylaşıyorlarsa tek bir grup olarak algılanma eğilimindedir.

**Uygulama:**
- **Kapsayıcılar:** Görselleri ve başlıkları gruplandırmak için kartlar (cards) kullanın.
- **Kenarlıklar:** Yan paneli (sidebar) ana akıştan ayırmak için çizgiler kullanın.
- **Arka Planlar:** Sayfa alt bilgisi (footer) için farklı bir arka plan rengi kullanın.
- **Modallar:** Açılır pencereleri sayfadan ayırmak için belirgin bir kutu kullanın.
- **Listeler:** Satırlar için dönüşümlü arka plan renkleri (zebra striping) kullanın.
- **Header:** Navigasyon öğelerini gruplandırmak için en üstte sabit bir çubuk kullanın.

**Örnek:**
```
❌ Kötü: Farklı haberlerin metinlerinin ve görsellerinin iç içe geçtiği bir liste.
✅ İyi: Her haberin hafif gri arka plan üzerinde kendi beyaz kartı içinde olması.

❌ Kötü: Ana gövdeyle aynı arka plan rengine sahip bir footer.
✅ İyi: Yasal linkleri sayfa içeriğinden net bir şekilde ayıran koyu temalı bir footer.
```

---

### Üniform Bağlılık Yasası (Law of Uniform Connectedness)

**Prensip:** Görsel olarak (çizgiler, oklar vb. ile) bağlı olan öğeler, bağlantısı olmayan öğelere göre daha ilişkili algılanırlar.

**Uygulama:**
- **Akış:** Bir ilerleme sihirbazındaki (wizard) adımları birbirine bağlamak için çizgiler kullanın.
- **Menüler:** Ana butona "dokunan" veya ona bağlı olan açılır menüler (dropdowns).
- **Grafikler:** Bir grafik üzerindeki veri noktalarını birleştiren çizgiler.
- **İlişki:** Bir toggle (anahtar) butonunu kontrol ettiği metne bağlamak.
- **Hiyerarşi:** Dosya dizinleri için ağaç yapıları.
- **Formlar:** Bir "Kredi Kartı" radyo butonunu altındaki alan setine (fieldset) bağlamak.

**Örnek:**
```
❌ Kötü: "1", "2" ve "3" rakamlarının dağınık durduğu bir kurulum süreci.
✅ İyi: Bir sırayı göstermek için "1", "2" ve "3"ü birbirine bağlayan yatay bir çizgi.

❌ Kötü: Kendisini açan butona dokunmayan, havada asılı duran açılır menüler.
✅ İyi: Ana butona görsel olarak "yapışık" olan bir açılır menü.
```

---

### Basitlik Yasası (Law of Prägnanz)

**Prensip:** İnsanlar belirsiz veya karmaşık görüntüleri, mümkün olan en basit biçimde algılar ve yorumlar; çünkü en az bilişsel çabayı gerektiren yorum budur.

**Uygulama:**
- **Netlik:** Navigasyon için net, geometrik ikonlar kullanın.
- **Arındırma:** Gereksiz 3B dokuları veya gölgeleri kaldırın.
- **Şekiller:** Karmaşık çokgenler yerine standart dikdörtgen ve daireleri tercih edin.
- **Odak:** Birincil eylemler için yüksek kontrastlı silüetler kullanın.
- **Logolar:** Küçük boyutlarda bile tanınabilir, basit marka işaretleri tercih edin.
- **UX:** "Zihinsel şekli" basit tutmak için sayfa başına tek bir ana hedef belirleyin.

**Örnek:**
```
❌ Kötü: "Dosyalar" ikonu için hiper-gerçekçi 3B bir klasör çizimi.
✅ İyi: Klasörün basit bir 2B ana hattı (outline).

❌ Kötü: Yükleme (loading) ikonu olarak kullanılan çok renkli, karmaşık bir logo.
✅ İyi: Basit, tek renkli dairesel bir halka.
```

---

### Şekil/Zemin Yasası (Law of Figure/Ground)

**Prensip:** Göz, bir nesneyi çevreleyen alandan ayırır. Bir form, silüet veya şekil "şekil" (nesne) olarak algılanırken, çevreleyen alan "zemin" (arka plan) olarak algılanır.

**Uygulama:**
- **Odak:** İçeriği öne çıkarmak için modallarda yarı saydam katmanlar (scrims) kullanın.
- **Derinlik:** Bir nesnenin zeminden yukarıda olduğunu hissettirmek için gölgeler (drop shadows) kullanın.
- **Kontrast:** Koyu zemin üzerine açık metin (veya tersi).
- **Bulanıklık:** Öndeki metni vurgulamak için arka plan bulanıklığı (blur) kullanın.
- **Navigasyon:** Sayfa içeriğinin üzerinde kalan sabit (sticky) header'lar.
- **Hover:** Kartları hover durumunda hafifçe yükselterek onları nesne (figure) olarak tanımlayın.

**Örnek:**
```
❌ Kötü: Hiçbir gölgesi veya kenarlığı olmayan, sayfayla bütünleşen bir açılır pencere.
✅ İyi: Gölge efekti ve arkasında karartılmış bir katmanı olan bir modal.

❌ Kötü: Karmaşık, çok renkli bir fotoğrafın üzerine doğrudan yerleştirilmiş beyaz metin.
✅ İyi: Koyu, yarı saydam bir katman (scrim) üzerine yerleştirilmiş beyaz metin.
```

---

### Odak Noktası Yasası (Law of Focal Point)

**Prensip:** Görsel olarak öne çıkan her şey, izleyicinin dikkatini ilk önce çeker ve orada tutar.

**Uygulama:**
- **Giriş:** Temel değer önerisini (value proposition) odak noktasına yerleştirin.
- **Renk:** Nötr bir arayüzde yüksek canlılıkta tek bir "Eylem Rengi" kullanın.
- **Hareket:** Gözü çekmek için CTA üzerinde hafif bir animasyon kullanın.
- **Boyut:** En önemli istatistik en büyük fontla yazılmalıdır.
- **Tipografi:** Başlıklar için kalın (bold), gövde metni için standart ağırlık kullanın.
- **Yönlendirme:** Oklar veya bakış yönü (bir butona bakan insan fotoğrafları) kullanın.

**Örnek:**
```
❌ Kötü: Aynı boyut ve renkte 5 butonun olduğu bir ana sayfa.
✅ İyi: Parlak renkte tek bir büyük "Hemen Başla" butonu.

❌ Kötü: Dashboard'da "Toplam Gelir" ile "Sistem Versiyonu"nun aynı boyutta olması.
✅ İyi: "Toplam Gelir"in en üste, en ortaya, devasa ve kalın rakamlarla yazılması.
```

---

## 3. Bilişsel Önyargılar ve Davranış

### Zeigarnik Etkisi

**Prensip:** İnsanlar tamamlanmamış veya kesintiye uğramış görevleri, tamamlanmış görevlerden daha iyi hatırlarlar.

**Uygulama:**
- **Oyunlaştırma:** "Profil %60 tamamlandı" gibi ilerleme çubukları kullanın.
- **Etkileşim:** Bir öğrenme yolunda bir sonraki modülü merak uyandıracak şekilde gösterin.
- **Elde Tutma:** Henüz keşfedilmemiş özelliklerin bir "Yapılacaklar" listesini sunun.
- **Geri Bildirim:** Okunmamış mesajlar için kalıcı bildirim rozetleri kullanın.
- **Momentum:** Bir görevi bitirir bitirmez "Sıradaki" adımı gösterin.
- **Alışveriş:** Sepetteki "Siparişi Tamamla" hatırlatıcıları.

**Örnek:**
```
❌ Kötü: Nelerin kaldığına dair hiçbir belirti vermeyen sessiz bir onboarding süreci.
✅ İyi: "5 adımdan 3'ü tamamlandı" bilgisini veren bir kontrol listesi.

❌ Kötü: Video yarıda kesilse bile onay işareti gösteren bir eğitim uygulaması.
✅ İyi: Video bitene kadar yarım kalan bir ilerleme halkası.
```

---

### Hedef Gradyanı Etkisi (Goal Gradient Effect)

**Prensip:** Bir hedefe yaklaşma eğilimi, hedefe olan yakınlıkla birlikte artar.

**Uygulama:**
- **Momentum:** Kullanıcılara "Yapay İlerleme" verin (örneğin 2 adet hediye mühür içeren sadakat kartı).
- **İlerleme:** 10 alanlık bir formu, 5'er alanlık iki adıma bölün.
- **Geri Bildirim:** Bir görevin yarısında ulaşılan kilometre taşlarını kutlayın.
- **Motivasyon:** Kullanıcıya bir ödüle/statüye ne kadar yakın olduğunu gösterin.
- **Navigasyon:** Sona ne kadar yaklaştıklarını göstermek için breadcrumb (ekmek kırıntıları) kullanın.
- **Yükleme:** Yükleme animasyonunu %100'e yaklaştıkça hızlandırın.

**Örnek:**
```
❌ Kötü: %0'dan başlayan ve uzun bir yol gibi hissettiren bir ilerleme çubuğu.
✅ İyi: Uygulamayı açtığı için %20'den başlatılan bir ilerleme çubuğu.

❌ Kötü: "Son İnceleme" ekranının sürpriz bir 5. adım gibi hissettirdiği bir ödeme akışı.
✅ İyi: Adımların net isimlendirilmesi: "Kargo > Ödeme > Neredeyse Bitti!"
```

---

### Doruk-Son Kuralı (Peak-End Rule)

**Prensip:** İnsanlar bir deneyimi, her anın toplamı veya ortalamasından ziyade, en yoğun olduğu an (doruk) ve nasıl bittiği (son) üzerinden yargılarlar.

**Uygulama:**
- **Başarı:** "Sipariş Onaylandı" ekranını unutulmaz kılın.
- **Keyif:** Değerin sunulduğu noktada konfeti veya benzersiz bir animasyon ekleyin.
- **Destek:** Bir chat bot ile yapılan son etkileşimin yardımcı olduğundan emin olun.
- **Ayrılma (Unboarding):** Bir kullanıcı ayrıldığında bile son çıkışı temiz yapın.
- **Onboarding:** İlk oturumu net bir "Kazanç" ile bitirin.
- **Hata Yönetimi:** Bir 404 sayfasını eğlenceli ve yardımcı bir etkileşime dönüştürün.

**Örnek:**
```
❌ Kötü: 20 dakikalık bir vergi beyanı sürecinden sonra sadece "Gönderildi" yazan uygulama.
✅ İyi: Geri iade miktarının özetiyle birlikte gelen bir "Tebrikler!" ekranı.

❌ Kötü: Düz bir fontla sadece "Oyun Bitti" yazan bir oyun.
✅ İyi: Kutlama müziği eşliğinde yüksek skorları gösteren bir özet ekranı.
```

---

### Estetik-Kullanılabilirlik Etkisi (Aesthetic-Usability Effect)

**Prensip:** Kullanıcılar estetik olarak hoş buldukları bir tasarımı genellikle daha kullanışlı olarak algılarlar.

**Uygulama:**
- **Güven:** Yüksek kaliteli görseller, küçük hatalar için size "güven kredisi" kazandırır.
- **Marka:** Tutarlı ve yüksek kaliteli görseller profesyonellik inşa eder.
- **Etkileşim:** Güzel arayüzler kullanıcıların daha uzun süre keşif yapmasını sağlar.
- **Sabır:** Arayüz güzelse kullanıcılar yükleme süreleri konusunda daha bağışlayıcı olurlar.
- **Özgüven:** Temiz bir tasarım, karmaşık araçların bile daha yönetilebilir hissedilmesini sağlar.
- **Sadakat:** İnsanlar güzel ürünlerle duygusal bağ kurarlar.

**Örnek:**
```
❌ Kötü: Hizalanmamış metinler ve 90'lardan kalma uyumsuz renklerin olduğu bir bankacılık uygulaması.
✅ İyi: Yumuşak animasyonlara sahip, şık ve modern bir bankacılık uygulaması.

❌ Kötü: Düşük çözünürlüklü, pikselleşmiş stok fotoğraflar kullanmak.
✅ İyi: Yüksek çözünürlüklü, özel marka illüstrasyonları kullanmak.
```

---

### Çapalama Önyargısı (Anchoring Bias)

**Prensip:** Kullanıcılar karar verirken sunulan ilk bilgiye ("çapa") fazlasıyla güvenirler.

**Uygulama:**
- **Fiyatlandırma:** Eski fiyatın üzerini çizerek gösterin.
- **Katmanlar:** En pahalı olan "Enterprise" planını en sola koyun.
- **Sıralama:** "En Popüler" seçeneğini ilk öneri olarak öne çıkarın.
- **İndirimler:** Son fiyatı göstermeden önce "%20 Tasarruf Edin" ibaresini belirtin.
- **Limitler:** "Müşteri başına limit 12 adet" ibaresi, ürünün değerli olduğu fikrini çapalar.
- **Varsayılanlar:** Yüksek bir "Önerilen Bağış" miktarı ile başlayın.

**Örnek:**
```
❌ Kötü: Sadece fiyatı "$49" olarak göstermek.
✅ İyi: "~~$99~~ $49 (%50 İndirim)" şeklinde göstermek.

❌ Kötü: Laptop listesini en ucuzdan en pahalıya doğru sıralamak.
✅ İyi: Diğerlerinin ucuz görünmesi için en başta üst düzey bir "Pro" modeli göstermek.
```

---

### Sosyal Kanıt (Social Proof)

**Prensip:** İnsanlar bir durumda nasıl davranacaklarına karar verirken başkalarının eylemlerini kopyalarlar.

**Uygulama:**
- **Doğrulama:** "Bize katılan 50.000+ kişiden biri olun" gibi ifadeler.
- **Yorumlar:** Yıldız derecelendirmeleri ve doğrulanmış müşteri yorumları.
- **Logolar:** İş ortağı markaları gösteren "Güvenenler" bölümü.
- **Canlı Akış:** "Elif 5 dakika önce bu ürünü satın aldı" bildirimleri.
- **Aktivite:** "Şu an 300 kişi bu ürünü inceliyor."
- **Sertifikalar:** Sektörel ödüller ve güvenlik rozetleri.

**Örnek:**
```
❌ Kötü: Sadece bir formdan oluşan kayıt sayfası.
✅ İyi: "2 milyon tasarımcıya katılın" diyen bir kayıt sayfası.

❌ Kötü: İsimsiz ve fotoğrafsız anonim yorumlar.
✅ İyi: Yüz, isim ve "Doğrulanmış Alıcı" etiketi içeren yorumlar.
```

---

### Kıtlık Prensibi (Scarcity Principle)

**Prensip:** İnsanlar kıt olan bir nesneye daha yüksek, bol olanlara ise daha düşük değer biçerler.

**Uygulama:**
- **Aciliyet:** "Stokta sadece 2 ürün kaldı."
- **Zaman:** İndirimler için geri sayım sayaçları.
- **Erişim:** "Sadece davetiye ile" girilen betalar veya özel üyelikler.
- **Mevsimsellik:** "Yaz Özel" ürünleri.
- **Düşük Stok:** "Yakında tekrar stokta - şimdi ön sipariş verin."
- **Talep:** "Yoğun talep var - 10 kişinin sepetinde bu ürün var."

**Örnek:**
```
❌ Kötü: Hiç bitmeyen ve geri sayımı olmayan bir indirim.
✅ İyi: Saat işleyen bir "Günün Fırsatı."

❌ Kötü: Stok adedi belirtmeden sadece "Mevcut" yazmak.
✅ İyi: "Bu fiyata sadece son 3 adet!"
```

---

### Otorite Önyargısı (Authority Bias)

**Prensip:** Bir otorite figürünün görüşüne daha fazla doğruluk atfetme ve bu görüşten daha fazla etkilenme eğilimidir.

**Uygulama:**
- **Uzmanlık:** "Uzman onaylı" ibaresi veya profesyonel portre fotoğrafları kullanın.
- **Sertifikalar:** Güven mühürleri (Norton, ISO, HIPAA).
- **Medya:** "TechCrunch/Forbes'ta görüldüğü gibi" logoları.
- **Onaylar:** Sektör liderlerinden veya influencer'lardan gelen referanslar.
- **Dil:** Kendinden emin, profesyonel ve doğru metinler (copy).
- **Geçmiş:** Uzun ömür ve güven telkin etmek için "1950'den beri" gibi ifadeler.

**Örnek:**
```
❌ Kötü: "Admin" tarafından yazılmış bir sağlık blogu.
✅ İyi: "Kardiyolog Dr. Canan Yılmaz tarafından incelendi" ibareli sağlık makalesi.

❌ Kötü: Sertifikalardan hiç bahsetmeyen bir güvenlik uygulaması.
✅ İyi: "ISO 27001 Sertifikalı" ve "Norton Secured" logolarını sergilemek.
```

---

### Kayıptan Kaçınma (Loss Aversion)

**Prensip:** İnsanlar genellikle elde edilecek kazançtan ziyade, eşdeğer bir kayıptan kaçınmayı tercih ederler. 5 TL bulmaktansa 5 TL kaybetmemek daha önemlidir.

**Uygulama:**
- **Mesajlaşma:** "İndiriminizi kaybetmeyin."
- **Deneme Süreleri:** "Deneme süreniz bitiyor - verilerinizi şimdi koruyun."
- **Kıtlık:** "Bir kez gitti mi, temelli gider."
- **Sepetler:** "Sepetinizdeki ürünleri kaçırmayın."
- **Sadakat:** "500 puan kazandınız - sürelerinin dolmasına izin vermeyin."
- **Risk:** "30 günlük iade garantisi" (paranın "kayıp" riskini azaltır).

**Örnek:**
```
❌ Kötü: "10 TL kupon almak için buraya tıklayın."
✅ İyi: "Bekleyen 10 TL krediniz var. Bu gece süresi dolmadan kullanın!"

❌ Kötü: "Aboneliğinizi iptal edin."
✅ İyi: "İptal ederseniz, kaydettiğiniz 50 projeye erişiminizi kaybedeceksiniz."
```

---

### Sahte Konsensüs Etkisi (False-Consensus Effect)

**Prensip:** İnsanlar kendi fikir, inanç, tercih ve alışkanlıklarının normal olduğunu ve diğerleri tarafından da paylaşıldığını abartma eğilimindedirler.

**Uygulama:**
- **Test Etme:** Siz kullanıcı değilsiniz - gerçek hedef kitlelerle test yapın.
- **Araştırma:** Nitel (mülakatlar) ve nicel (analizler) verileri birlikte kullanın.
- **Önyargı:** Kişisel favorilerden kaçınmak için "Blind Design Reviews" (kör tasarım incelemeleri) yapın.
- **Persona:** Kişisel tahminler yerine oluşturulmuş Kullanıcı Personalarına sadık kalın.
- **Varyasyon:** Farklı demografik gruplardan ve yeteneklerden kullanıcılarla test yapın.
- **Nesnellik:** Gerçek kullanıcı davranışını görmek için ısı haritaları (heatmaps) kullanın.

**Örnek:**
```
❌ Kötü: Bir tasarımcının bir özelliği test etmeden "sezgisel" olduğuna karar vermesi.
✅ İyi: Hangi versiyonun daha çok tercih edildiğini görmek için A/B testi yapmak.

❌ Kötü: "Herkes İngilizce bilir" diyerek bir uygulamayı sadece İngilizce inşa etmek.
✅ İyi: Gerçek kullanıcı konum verilerine göre yerelleştirme (localization) eklemek.
```

---

### Bilgi Laneti (Curse of Knowledge)

**Prensip:** Bir şahıs başkalarıyla iletişim kurarken, diğerlerinin de konuyu anlamak için gerekli temel bilgiye sahip olduğunu farkında olmadan varsaydığında ortaya çıkan bilişsel bir önyargıdır.

**Uygulama:**
- **Metinler:** Teknik terimlerden (jargon) kaçının ve sade bir dil kullanın.
- **Onboarding:** Kullanıcının hiçbir şey bilmediğini varsayan öğreticiler.
- **Tooltip'ler:** Üzerine gelince karmaşık terimleri açıklayan ipuçları.
- **Yapı:** Kademeli açıklama (gelişmiş ayarları gizleyin).
- **Etiketler:** Navigasyon için sadece ikonlara güvenmeyin, ikon + metin etiketi kullanın.
- **Destek:** Yeni başlayanlar için kapsamlı SSS bölümleri.

**Örnek:**
```
❌ Kötü: "Exception: Null Pointer at 0x0045" diyen bir hata mesajı.
✅ İyi: "Bir şeyler yanlış gitti. Lütfen sayfayı yenilemeyi deneyin" mesajı.

❌ Kötü: Bir bulut uygulamasını "S3 Bucket Instance" gibi terimlerle yönetmek.
✅ İyi: "Dosya Depolama" gibi basit terimler kullanmak.
```

---

### Atlama Taşı Etkisi (Foot-in-the-Door)

**Prensip:** Kullanıcılar küçük görevlere evet dediklerinde, büyük görevlere de bağlılık gösterme olasılıkları artar.

**Uygulama:**
- **Dönüşüm Hunisi:** Kredi kartı istemeden önce sadece e-posta isteyin.
- **Etkileşim:** Kayıttan önce sadece bir tercih (örneğin "Karanlık Mod?") sorun.
- **Onboarding:** "Hızlı Evet/Hayır" sorularından oluşan bir seri kullanın.
- **Güven:** Abonelik istemeden önce ücretsiz bir PDF/araç sunun.
- **Profil:** Önce bir fotoğraf yüklemesini isteyin, biyografiyi sonra doldurtabilirsiniz.
- **Satış:** Ana hizmetten önce düşük maliyetli bir "eşik" (tripwire) ürün sunun.

**Örnek:**
```
❌ Kötü: Hemen kredi kartı bilgisi gerektiren bir "Ücretsiz Denemeyi Başlat" butonu.
✅ İyi: Önce e-posta ve şifre isteyip, sonra denemeyi teklif etmek.

❌ Kötü: 50 sorunun tamamını tek sayfada gösteren bir anket.
✅ İyi: Tek bir kolay "Evet/Hayır" sorusuyla başlayan bir anket.
```

---

## 2. Duygusal Tasarım (Don Norman)

### Üç İşleme Seviyesi

```
┌─────────────────────────────────────────────────────────────┐
│  VİSERAL (İlkel Beyin)                                      │
│  ─────────────────────                                      │
│  • Anlık, otomatik tepki                                     │
│  • İlk izlenimler (ilk 50ms)                                 │
│  • Estetik: renkler, şekiller, görseller                    │
│  • "Vay canına, bu harika görünüyor!"                       │
├─────────────────────────────────────────────────────────────┤
│  DAVRANIŞSAL (Fonksiyonel Beyin)                            │
│  ─────────────────────────────                              │
│  • Kullanılabilirlik ve fonksiyon                            │
│  • Etkili kullanımdan alınan keyif                          │
│  • Performans, güvenilirlik, kolaylık                       │
│  • "Bu tam beklediğim gibi çalışıyor!"                      │
├─────────────────────────────────────────────────────────────┤
│  REFLEKTİF (Bilinçli Beyin)                                  │
│  ─────────────────────────────                              │
│  • Bilinçli düşünce ve anlam                                 │
│  • Kişisel kimlik ve değerler                                │
│  • Uzun vadeli hafıza ve sadakat                            │
│  • "Bu marka benim kim olduğumu temsil ediyor"              │
└─────────────────────────────────────────────────────────────┘
```

### Her Seviye İçin Tasarım Yapmak

**Viseral:**
```css
/* Etkileyici ilk izlenim */
.hero {
  background: linear-gradient(135deg, #0ea5e9 0%, #14b8a6 100%);
  color: white;
}

/* Keyif veren mikro-etkileşimler */
.button:hover {
  transform: translateY(-2px);
  box-shadow: var(--shadow-lg);
}
```

**Davranışsal:**
```javascript
// Anlık geri bildirim
button.onclick = () => {
  button.disabled = true;
  button.textContent = 'Kaydediliyor...';
  
  save().then(() => {
    showSuccess('Kaydedildi!');  // Anında onay
  });
};
```

**Reflektif:**
```html
<!-- Marka hikayesi ve değerleri -->
<section class="about">
  <h2>Neden Varız?</h2>
  <p>Teknolojinin hayatı zorlaştırmak değil, kolaylaştırmak gerektiğine inanıyoruz...</p>
</section>

<!-- Kimlikle bağ kuran sosyal kanıt -->
<blockquote>
  "Bu araç olmak istediğim tasarımcı olmama yardımcı oldu."
</blockquote>
```

---

## 3. Güven İnşa Sistemi

### Güven Sinyali Kategorileri

| Kategori | Öğeler | Uygulama |
|----------|----------|----------------|
| **Güvenlik** | SSL, rozetler, şifreleme | Görünür asma kilit, formlarda güvenlik logoları |
| **Sosyal Kanıt** | Yorumlar, referanslar, logolar| Yıldız puanları, müşteri fotoları, marka logoları |
| **Şeffaflık** | Politikalar, fiyatlandırma, iletişim | Net linkler, gizli ücret yok, gerçek adres |
| **Profesyonellik** | Tasarım kalitesi, tutarlılık | Kırık öğe yok, tutarlı markalama |
| **Otorite** | Sertifikalar, ödüller, medya | "İçerik çekilen mecralar...", sektör sertifikaları |

### Güven Sinyali Yerleşimi

```
┌────────────────────────────────────────────────────┐
│  HEADER: Güven bandı ("Ücretsiz kargo | 30 gün    │
│          iade | Güvenli ödeme")                    │
├────────────────────────────────────────────────────┤
│  HERO: Sosyal kanıt ("10.000+ kullanıcı")          │
├────────────────────────────────────────────────────┤
│  PRODUCT: Görünür yorumlar, güvenlik rozetleri     │
├────────────────────────────────────────────────────┤
│  CHECKOUT: Ödeme ikonları, SSL rozeti, garanti     │
├────────────────────────────────────────────────────┤
│  FOOTER: İletişim bilgisi, politikalar, sertifikalar│
└────────────────────────────────────────────────────┘
```

### Güven İnşası CSS Desenleri

```css
/* Güven rozeti tasarımı */
.trust-badge {
  display: flex;
  align-items: center;
  gap: 8px;
  padding: 12px 16px;
  background: #F0FDF4;  /* Hafif yeşil = güvenlik */
  border-radius: 2px; /* Keskin köşeler = hassasiyet ve güven hissi */
  font-size: 14px;
  color: #166534;
}

/* Güvenli form göstergesi */
.secure-form::before {
  content: '🔒 Güvenli form';
  display: block;
  font-size: 12px;
  color: #166534;
  margin-bottom: 8px;
}

/* Referans/Yorum kartı */
.testimonial {
  display: flex;
  gap: 16px;
  padding: 24px;
  background: white;
  border-radius: 16px; /* Sıcak/Cana yakın = daha büyük yarıçap */
  box-shadow: var(--shadow-sm);
}

.testimonial-avatar {
  width: 48px;
  height: 48px;
  border-radius: 50%;  /* Gerçek fotolar > sadece baş harfler */
}
```

---

## 4. Bilişsel Yük Yönetimi (Cognitive Load Management)

### Üç Tip Bilişsel Yük

| Tür | Tanım | Tasarımcının Rolü |
|------|------------|-----------------|
| **İçsel (Intrinsic)** | Görevin özündeki karmaşıklık | Daha küçük adımlara bölmek |
| **Yabancı (Extraneous)**| Kötü tasarımdan gelen yük | Bunu tamamen ortadan kaldırmak! |
| **İlgili (Germane)** | Öğrenme için harcanan çaba | Desteklemek ve teşvik etmek |

### Azaltma Stratejileri

**1. Basitleştirin (Yabancı Yükü Azaltın)**
```css
/* Görsel gürültüden → Temizliğe */
.card-busy {
  border: 2px solid red;
  background: linear-gradient(...);
  box-shadow: 0 0 20px ...;
  /* Çok fazla! */
}

.card-clean {
  background: white;
  border-radius: 16px;
  box-shadow: 0 10px 30px -10px rgba(0,0,0,0.1);
  /* Sakin, odaklanmış */
}
```

**2. Bilgiyi Parçalara Bölün (Chunking)**
```html
<!-- Boğucu -->
<form>
  <!-- Aynı anda 15 alan -->
</form>

<!-- Parçalanmış -->
<form>
  <fieldset>
    <legend>Adım 1: Kişisel Bilgiler</legend>
    <!-- 3-4 alan -->
  </fieldset>
  <fieldset>
    <legend>Adım 2: Kargo Bilgileri</legend>
    <!-- 3-4 alan -->
  </fieldset>
</form>
```

**3. Kademeli Açıklama (Progressive Disclosure)**
```html
<!-- Karmaşıklığı ihtiyaç duyulana kadar gizleyin -->
<div class="filters">
  <div class="filters-basic">
    <!-- Yaygın filtreler görünür -->
  </div>
  <button onclick="toggleAdvanced()">
    Gelişmiş Seçenekler ▼
  </button>
  <div class="filters-advanced" hidden>
    <!-- Karmaşık filtreler gizli -->
  </div>
</div>
```

**4. Tanıdık Desenler Kullanın**
```
✅ Standart navigasyon yerleşimi
✅ Beklenen ikon anlamları (🔍 = arama)
✅ Geleneksel form düzenleri
✅ Yaygın jest desenleri (kaydırma, kıstırma)
```

**5. Bilgiyi Dışsallaştırın (Zihinden Sisteme Aktarın)**
```html
<!-- Kullanıcıyı hatırlamaya zorlamayın -->
<label>
  Kart Numarası
  <input type="text" inputmode="numeric" 
         autocomplete="cc-number" 
         placeholder="1234 5678 9012 3456">
</label>

<!-- Ne girdiklerini gösterin -->
<div class="order-summary">
  <p>Şuraya gönderiliyor: <strong>Mehmet Yılmaz, Taksim Mah...</strong></p>
  <a href="#">Düzenle</a>
</div>
```

---

## 5. İkna Edici Tasarım (Persuasive Design - Etik)

### Etik İkna Teknikleri

| Teknik | Etik Kullanım | Karanlık Desen (Kaçının) |
|-----------|-------------|----------------------|
| **Kıtlık** | Gerçek stok seviyeleri | Sahte geri sayım sayaçları |
| **Sosyal Kanıt** | Gerçek kullanıcı yorumları | Sahte referanslar |
| **Otorite** | Gerçek sertifikalar | Yanıltıcı rozetler |
| **Aciliyet** | Gerçek son tarihler | Yapay FOMO (kaybetme korkusu) |
| **Bağlılık** | İlerlemenin kaydedilmesi | Kullanıcıyı suçlu hissettirme |

### Dürtme (Nudge) Desenleri

**Akıllı Varsayılanlar:**
```html
<!-- Önerilen seçeneği önceden seçin -->
<input type="radio" name="plan" value="monthly">
<input type="radio" name="plan" value="annual" checked>
  Yıllık (%20 Tasarruf Edin)
```

**Çapalama (Anchoring):**
```html
<!-- İndirimi vurgulamak için orijinal fiyatı gösterin -->
<div class="price">
  <span class="original">99 TL</span>
  <span class="current">79 TL</span>
  <span class="savings">%20 İndirim</span>
</div>
```

**Sosyal Kanıt:**
```html
<!-- Gerçek zamanlı aktivite -->
<div class="activity">
  <span class="avatar">👤</span>
  <span>İstanbul'dan Meryem az önce satın aldı</span>
</div>

<!-- Toplu kanıt -->
<p>Aracımızı kullanan 50.000+ tasarımcıya katılın</p>
```

**İlerleme ve Bağlılık:**
```html
<!-- Tamamlamayı teşvik etmek için ilerlemeyi gösterin -->
<div class="progress">
  <div class="progress-bar" style="width: 60%"></div>
  <span>%60 tamamlandı - neredeyse bitti!</span>
</div>
```

---

## 6. Kullanıcı Persona Hızlı Referansı

### Z Kuşağı (1997-2012 Doğumlular)

```
ÖZELLİKLER:
- Dijital yerli, mobil öncelikli
- Otantikliğe ve çeşitliliğe değer verir
- Kısa dikkat süreleri
- Görsel odaklı öğrenme

TASARIM YAKLAŞIMI:
├── Renkler: Canlı, hiper-renkli, cesur gradyanlar
├── Tipografi: Büyük, değişken, deneysel
├── Düzen: Dikey kaydırma, mobil-yerel yapı
├── Etkileşimler: Hızlı, oyunlaştırılmış, jest tabanlı
├── İçerik: Kısa video, meme'ler, hikayeler
└── Güven: Akran yorumları > resmi otorite
```

### Y Kuşağı (1981-1996 Doğumlular)

```
ÖZELLİKLER:
- Deneyime sahip olmaktan daha çok değer verir
- Satın almadan önce araştırır
- Sosyal sorumluluk bilinci yüksektir
- Fiyat hassasiyeti olsa da kalite arar

TASARIM YAKLAŞIMI:
├── Renkler: Mat pasteller, toprak tonları
├── Tipografi: Temiz, okunaklı sans-serif
├── Düzen: Responsive, kart tabanlı
├── Etkileşimler: Yumuşak, amaca hizmet eden animasyonlar
├── İçerik: Değer odaklı, şeffaf
└── Trust: Yorumlar, sürdürülebilirlik, değerler
```

### X Kuşağı (1965-1980 Doğumlular)

```
ÖZELLİKLER:
- Bağımsız, kendine güvenen
- Verimliliğe önem veren
- Pazarlama söylemlerine şüpheyle yaklaşan
- Dengeli teknoloji kullanımı

TASARIM YAKLAŞIMI:
├── Renkler: Profesyonel, güven telkin eden
├── Tipografi: Tanıdık, muhafazakar
├── Düzen: Net hiyerarşi, geleneksel yapı
├── Etkileşimler: Fonksiyonel, gösterişsiz
├── İçerik: Doğrudan, gerçeklere dayalı
└── Güven: Uzmanlık, geçmiş başarılar
```

### Baby Boomer'lar (1946-1964 Doğumlular)

```
ÖZELLİKLER:
- Detay odaklı
- Güvendiklerinde sadık
- Kişisel hizmete değer verir
- Teknolojide daha az özgüvenli

TASARIM YAKLAŞIMI:
├── Renkler: Yüksek kontrastlı, basit palet
├── Tipografi: Büyük (18px+), yüksek kontrast
├── Düzen: Basit, doğrusal, ferah
├── Etkileşimler: Minimal, net geri bildirim
├── İçerik: Kapsamlı, detaylı
└── Güven: Telefon numaraları, gerçek insanlar
```

---

## 7. Duygu-Renk Eşleşmesi

```
┌────────────────────────────────────────────────────┐
│  DUYGU            │  RENKLER          │  KULLANIM  │
├───────────────────┼───────────────────┼────────────┤
│  Güven            │  Mavi, Yeşil      │  Finans    │
│  Heyecan          │  Kırmızı, Turuncu │  Satış     │
│  Sakinlik         │  Mavi, Açık yeşil │  Wellness  │
│  Lüks             │  Siyah, Altın     │  Premium   │
│  Yaratıcılık      │  Turkuaz, Pembe   │  Sanat     │
│  Enerji           │  Sarı, Turuncu    │  Spor      │
│  Doğa             │  Yeşil, Kahverengi│  Eko       │
│  Mutluluk         │  Sarı, Turuncu    │  Çocuk     │
│  Sofistike        │  Gri, Lacivert    │  Kurumsal  │
│  Aciliyet         │  Kırmızı          │  Hatalar   │
└───────────────────┴───────────────────┴────────────┘
```

---

## 8. Psikoloji Kontrol Listesi

### Yayından Önce

- [ ] **Hick Yasası:** Navigasyonda 7'den fazla seçenek yok. Karar yorgunluğunu azaltmak için seçenekler daraltıldı mı?
- [ ] **Fitts Yasası:** Birincil CTA'ler büyük ve ulaşılabilir. En önemli butonlara mobilde basmak kolay mı?
- [ ] **Miller Yasası:** İçerik uygun şekilde gruplandırıldı. Bilgiler 5-7'lik sindirilebilir birimler halinde mi?
- [ ] **Jakob Yasası:** Site, kullanıcıların zaten bildiği standart web kurallarına uyuyor mu?
- [ ] **Doherty Eşiği:** Sistem 400ms içinde geri bildirim veriyor mu? Skeleton ekranlar hazır mı?
- [ ] **Tesler Yasası:** Karmaşıklık, mümkün olan yerlerde kullanıcıdan sisteme aktarıldı mı?
- [ ] **Parkinson Yasası:** Görev süresini en aza indirmek için "Tek Tıkla Ödeme" gibi özellikler var mı?
- [ ] **Von Restorff:** Birincil CTA, diğer tüm öğelerden görsel olarak ayrışıyor mu?
- [ ] **Seri Konum:** En kritik bilgiler listelerin başında veya sonunda mı?
- [ ] **Gestalt Yasaları:** İlgili öğeler fiziksel olarak gruplandırıldı mı (Yakınlık) veya bir kart içinde mi (Ortak Bölge)?
- [ ] **Zeigarnik Etkisi:** Tamamlanmamış görevler için ilerleme çubuğu gibi göstergeler var mı?
- [ ] **Hedef Gradyanı:** Kullanıcıya tamamlamayı teşvik etmek için bir "başlangıç avantajı" (%20 ilerleme gibi) verildi mi?
- [ ] **Doruk-Son Kuralı:** Finaldeki "Başarı" ekranı keyifli bir an yaratıyor mu?
- [ ] **Occam'ın Usturası:** Gereksiz görsel veya fonksiyonel öğeler ayıklandı mı?
- [ ] **Estetik-Kullanılabilirlik:** Arayüz, ilk güveni sağlamak için yeterince yüksek kaliteli mi?
- [ ] **Güven & Otorite:** Güvenlik rozetleri, yorumlar ve uzman sertifikaları görünür mü?
- [ ] **Sosyal Kanıt:** Karar noktalarında gerçek kullanıcı sayıları veya referansları var mı?
- [ ] **Kıtlık & Aciliyet:** Kullanılıyorsa, kıtlık gerçek ve etik mi (örneğin gerçek düşük stok)?
- [ ] **Kayıptan Kaçınma:** Metinler, kazanılacak ektense elde tutulacak değere vurgu yapıyor mu?
- [ ] **Çapalama:** Fiyatlandırma, istenen seçeneği avantajlı gösterecek şekilde kurgulandı mı?
- [ ] **Postel Yasası:** Sistem, farklı girdi formatlarını hata vermeden kabul edecek kadar esnek mi?
- [ ] **Sahte Konsensüs:** Tasarım, sadece iç ekip tarafından değil, gerçek kullanıcılar tarafından test edildi mi?
- [ ] **Bilgi Laneti:** Metinler teknik jargondan arındırılmış ve yeni başlayanlar için anlaşılır mı?
- [ ] **Atlama Taşı:** Dönüşüm hunisi düşük sürtünmeli (örneğin sadece e-posta) görevlerle mi başlıyor?
- [ ] **Bilişsel Yük:** Arayüzü temiz tutmak için yabancı görsel gürültü en aza indirildi mi?
- [ ] **Duygusal Tasarım:** Renk paleti ve görseller hedeflenen viseral tepkiyi uyandırıyor mu?
- [ ] **Geri Bildirim:** Tüm etkileşimli öğelerin anında hover, active ve başarı durumları var mı?
- [ ] **Erişilebilirlik:** Kontrast oranları yeterli mi ve site klavye/ekran okuyucu ile gezilebiliyor mu?
- [ ] **Prägnanz:** İkonlar ve şekiller bir bakışta tanınacak kadar basit mi?
- [ ] **Şekil/Zemin:** Hangi öğenin odakta olduğu (örneğin gölgeler veya katmanlar ile) net mi?
