# Demir Usta — Tasarım Kararları

Bu belge, beyin fırtınasında alınan kararları, açık soruları ve sonraya bırakılan fikirleri tutar. Diğer bilgisayarda devam ederken **önce bunu oku**.

> Felsefe: Oyunun kalbi **demircilik**. Önce bu sistemi derinlemesine oturtuyoruz. Canavar avı ve maden daha **sade/ikincil** kalacak ve demirciliğe hizmet edecek.

---

## 1) Genel

- **Oyun:** Demir Usta — 2D pixel art, Android, sevimli (Stardew/Forager havası).
- **Motor:** Godot 4 kalemle işaretli (kullanıcının Godot deneyimi var). GDD'de Unity 2D yazıyor ama **kesinleşmedi**.
- **Proje konumu:** `D:\Projects\DemirUsta` (OneDrive'da değil — senkron/yavaşlık sorunu).

---

## 2) Demircilik — alınan kararlar

**Temel ayrım:** Malzeme = silahın **karakterini** belirler. Dövme performansı = o karakterin **kalitesini** belirler.

### Malzeme & Oran
- **Serbest denge / ödünleşme** mantığı. Gizli "altın tarif" YOK. Her seçim bir ödünleşme:
  - Demir: temel hasar+sağlamlık · çok koyarsan ağır, ısıtması zor
  - Kömür: ısıya yardım (yakıt) · az = ısınmaz, çok = taşar/yakar
  - Karbon/çelik: keskinlik↑ · kırılganlık↑
  - Nadir metal (mitril, yıldız demiri): hafif+güçlü · pahalı, hassas ısı
  - Taşlar (yakut, kristal): element/büyü (ateş, buz) · dengeyi bozabilir
  - Canavar özü (ejderha pulu…): fantastik efekt · çok nadir
- **Miktar = gramaj** mantığıyla (fikir): her kalıbın hedef ağırlığı var (hançer ~200gr, uzun kılıç ~900gr…), malzemenin gramı var. Ama bu bir **form/gösterge ekranı olarak YAPILMAYACAK** (aşağıya bak).

### İki üretim yolu
1. **Tarif Defteri** — bilinen silahlar; güvenilir, ilerlemeli; level/keşifle açılır.
2. **Serbest Dövme** — kalıp seçip malzemeyle deneme. İyi bir kombinasyon tutturursan **yeni tarif olarak defterine kaydolur** (keşif döngüsü).

### Silah kimliği
`Silah = Kategori × Stil(kalıp) × Malzeme × Kalite × Görünüm`
- Kategori: kılıç, balta, balyoz, hançer, mızrak…
- Stil: tek kılıç değil — kısa, uzun, eğri pala, geniş, ince vb. farklı siluet/denge.
- Şekil **kalıptan** gelir → **Seçenek A** seçildi. (Dövme hareketinden şekil doğması = Seçenek B, sonraya ertelendi.)

### Kalite kademeleri
`Çürük → Sıradan → İyi → Kaliteli → Usta İşi → Efsanevi → İMKANSIZ`
- Sonuç **şansla** belirlenir ama zarı **performans + sınıf + malzeme kalitesi** yönlendirir.
- En üst "İmkansız" çok nadir → kusursuz dövme + nadir malzeme → **isimli efsanevi silah**.

### ⚠️ Sunum/his (ÇOK ÖNEMLİ)
Dövme bir **form/gösterge doldurma ekranı DEĞİL**. **Animasyonlu fiziksel bir sahne** olacak. Oyuncu gerçekten demircilik yapıyormuş gibi hissedecek. Akış:

> **Potaya at → Erit → Kalıba dök → Döv → Soğut → Kılıç hazır!**

Her aşama bir **fiziksel hareketle** (sürükle-at, körüğü pompala, ritimle çekiçle vur, suya daldır) ve ekranda **canlı animasyonla** gerçekleşir.
Taslak: [`mockups/forge-animated.html`](mockups/forge-animated.html).

---

## 3) Açık / sıradaki işler (demircilikte)

Dövme akışının adımları yukarıdan aşağı detaylandırılacak:
- [x] **1. Malzeme & Oran** — oturdu (yukarıdaki kararlar)
- [ ] **2. ISIT** — ısı penceresi, körük, metal rengi (her metalin farklı ısı aralığı)
- [ ] **3. DÖV** — ritim/isabet; opsiyonel katlama (folding) risk/ödül
- [ ] **4. SOĞUT** — daldırma; sıvı çeşidi (su/yağ/ejderha kanı farklı efekt)
- [ ] **5. SONUÇ** — şans + performans → kademe formülü
- [ ] Sahnenin nihai görsel tasarımı (animasyonlu sahne mockup'ı üzerinden)

---

## 4) Sonraya bırakılan fikirler (cep)

- **B** — dövme hareketinden silah şeklinin doğması
- Sınıf/ırk sistemi (Cüce / İnsan / Elf / Ork — her biri ısı penceresini, şans eğrisini, kullanılabilir malzemeleri değiştirir) → **en sona**
- Başka dükkanlar / mağazadan ürün alma
- Kendi evimiz
- Han / yemek yenen mekânlar

---

## 5) Çalışma yöntemi notu

Tasarım, superpowers **brainstorming** skill'i + tarayıcı **görsel taslak (visual companion)** ile adım adım yapılıyor. Kod yazımına **ancak tasarım onaylanınca** geçilecek (önce yazılı tasarım → sonra plan → sonra kod).
Commit tarzı: önek yok (feat/fix vb.), imza yok, sade kısa mesaj.
