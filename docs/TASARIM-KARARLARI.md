# Demir Usta — Tasarım Kararları

Bu belge, beyin fırtınasında alınan kararları, açık soruları ve sonraya bırakılan fikirleri tutar. Diğer bilgisayarda devam ederken **önce bunu oku**.

> Felsefe: Oyunun kalbi **demircilik**. Önce bu sistemi derinlemesine oturtuyoruz. Canavar avı ve maden daha **sade/ikincil** kalacak ve demirciliğe hizmet edecek.

---

## 1) Genel

- **Oyun:** Demir Usta — 2D pixel art, Android, sevimli (Stardew/Forager havası).
- **Motor:** Godot 4 kalemle işaretli (kullanıcının Godot deneyimi var). GDD'de Unity 2D yazıyor ama **kesinleşmedi**.
- **Proje konumu:** `D:\Projects\DemirUsta` (OneDrive'da değil — senkron/yavaşlık sorunu).
- **Genişletilmiş vizyon (2026-10-27):** Stardew tarzı kasaba hayatı — demirhane + dükkân, maden, av, malzeme dükkânları, han. Referans: Stardew kasaba/demirci/envanter/dükkân içi görselleri.
- **Öncelik sırası:** önce **demircilik + dükkân** (oyunun kalbi), sonra bunları bağlayan gün döngüsü; maden, av ve han sonra.

### Tasarım ilkeleri
- **Herkes oynayabilmeli:** 30 saniyede öğrenilir, ustalaşması zaman alır. Tek elle, dokunmatik dostu.
- **Cihazı yormamalı:** düşük çözünürlüklü pixel art, sade efektler, zayıf Android telefonlarda akıcı çalışmalı.
- **"Bir gün daha" hissi:** kısa oturumlar (bir dövme ~30–60 sn), her gün küçük bir hedef ve ödül. Bağlılık iyi döngüden gelsin, sömürücü mekanikten (zorla reklam, enerji satışı) değil.
- **Sistemleri yormamak:** her mekanik sade olsun; derinlik, sistemlerin birbirine bağlanmasından gelsin.

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

### Metal ligleri (2026-10-27)
Metaller birbirine **yakın olmamalı** — hem nadirlik hem özellik olarak ayrı liglerde. Kusursuz oynasan bile demirden efsanevi çıkmaz; üst kademe için **nadir metal bulmak** gerekir (maden/ticarete anlam verir).

| | Demir | Çelik | Mitril |
|---|---|---|---|
| Bulunurluk | Bol | Seyrek | Kıymetli |
| Kademe aralığı | Kırık – Nadir (şansla Epik) | Kırık – Epik (şansla Efsanevi) | **Yaygın Olmayan – Mitik** (Yaygın Olmayan'ın altına düşmez) |
| Temel hasar | 20 | 34 | 58 |
| Ağırlık | 1200 g | 950 g | 520 g |
| Değer | ~40 – 500 | ~120 – 3.000 | ~2.000 – 28.000 |
| Doğal özellik | ⚓ Ağır | 🔪 Sert | 🪶 Hafif · ✨ Büyü iletken (element etkisi ×2) · 🛡️ Paslanmaz |

Kural: her metalin bir **aralığı** var. Performans (eğri: `perf^1.6`) tabanı metalin **kendi aralığına yayar** — kötü oyun aralığın dibine, kusursuz oyun `tavan−1`'e; şans en fazla tavana iter (bir üst kademe %6–18, iki üst ~%1.5). Böylece her metalde bütün kademeler görülür. Prototip simülasyonu (4000 deneme, demir): perf %40 → Kırık · %60 → Sıradan · %75 → Yaygın Olmayan · %90+ → Nadir (%~18 Epik). Kusursuz mitril → %99 Efsanevi / %1–2 Mitik.

### Pota ve alaşımlar (2026-10-27)
- Potada **3 yuva**; her yuvaya ayrı metal külçesi konur. Özellikler külçelerin **ortalamasıdır** (ısı bölgesi, ibre hızı, hasar, ağırlık, değer, kademe aralığı — yuvarlanarak).
- **Karışım = alaşım:** ısı bölgesi %15 daralır (alaşım daha zor ısıtılır), değeri %15 artar, ⚗️ Alaşım özelliği gelir. İlk kez yapılan alaşım **"keşfedildi!"** olarak kaydolur (Alaşım Defteri'nin çekirdeği).
- Tek bir mitril külçesi bile tavanı yükseltir (2 demir + 1 mitril → Sıradan–Efsanevi); Mitik için 3 mitril gerekir.

| Külçeler (demir, çelik, mitril) | Alaşım adı |
|---|---|
| 2, 1, 0 | Karbonlu Demir |
| 1, 2, 0 | Sertleşmiş Çelik |
| 2, 0, 1 | Mitril Damarlı Demir |
| 1, 0, 2 | Gök Demiri |
| 0, 2, 1 | Ay Çeliği |
| 0, 1, 2 | Mitril Çeliği |
| 1, 1, 1 | Üç Damar | Yıldız demiri ve diğer nadir metaller mitrilin de üstünde ayrı bir lig olacak.

### İki üretim yolu
1. **Tarif Defteri** — bilinen silahlar; güvenilir, ilerlemeli; level/keşifle açılır.
2. **Serbest Dövme** — kalıp seçip malzemeyle deneme. İyi bir kombinasyon tutturursan **yeni tarif olarak defterine kaydolur** (keşif döngüsü).

### Silah kimliği
`Silah = Kategori × Stil(kalıp) × Malzeme × Kalite × Görünüm`
- Kategori: kılıç, balta, balyoz, hançer, mızrak…
- Stil: tek kılıç değil — kısa, uzun, eğri pala, geniş, ince vb. farklı siluet/denge.
- Şekil **kalıptan** gelir → **Seçenek A** seçildi. (Dövme hareketinden şekil doğması = Seçenek B, sonraya ertelendi.)

### Kalite kademeleri (2026-10-27 — klasik RPG adları)
`Kırık → Sıradan → Yaygın Olmayan → Nadir → Epik → Efsanevi → Mitik`
(eski adlar: Çürük → Sıradan → İyi → Kaliteli → Usta İşi → Efsanevi → İmkansız — belgede eski ad geçen yerler bu sırayla eşlenir)
- Renkler (WoW geleneği, oyuncu "mor çıktı!" diye konuşabilsin): Kırık kahve-gri · Sıradan gri · Yaygın Olmayan yeşil · Nadir mavi · Epik mor · Efsanevi turuncu · Mitik pembe.
- Sonuç **şansla** belirlenir ama zarı **performans + sınıf + malzeme kalitesi** yönlendirir.
- En üst "Mitik" çok nadir → kusursuz dövme + kıymetli metal → **adını oyuncunun koyduğu silah**.
- Metal bulunurluğu kademe adlarıyla karışmasın diye ayrı kelimeler: **Bol · Seyrek · Kıymetli**.

### Silah adı (Diablo tarzı — özellikten otomatik)
Ad, silahın baskın özelliğinden seçilen **temadan** üretilir (buz suyu → buz, mitril → ışık, keskinlik ≥80 → keskin, demir → ağır, çelik → sert).

| Kademe | Kalıp | Örnek |
|---|---|---|
| Kırık | Çatlak + Metal + Kılıç | Çatlak Demir Kılıç |
| Sıradan | Metal + Kılıç | Çelik Kılıç |
| Yaygın Olmayan | Sıfat + Metal + Kılıç | Keskin Çelik Kılıç |
| Nadir | Sıfat ve Sıfat + Metal + Kılıç | Sert ve Keskin Çelik Kılıç |
| Epik | Unvan + Metal + Kılıcı | Ayazın Mitril Kılıcı |
| Efsanevi | «Destan adı» + lakap | «Kışın Dişi» — Buz Kesen · Mitril Kılıcı |
| Mitik | «Oyuncunun koyduğu ad» (oyun öneri sunar) + lakap | «Kor Yemini» — Işık Taşıyan · Mitril Kılıcı |

Temalar ve kelime havuzları: buz (Ayazın, Kuzeyin… / Kışın Dişi, Donmuş Yemin…), ışık (Şafağın, Yıldızların… / Yıldız Kırığı, Şafak Kesen…), keskin (Rüzgârın, Fırtınanın… / Sessiz Pençe, Şimşek Dili…), ağır (Dağın, Kayanın… / Dağ Kalbi, Taş Yürek…), sert (Örsün, Kalenin… / Kırılmaz Söz, Son Nöbet…). Efsanevi/Mitik adlar ün sistemine ve kasabadaki hikâyelere bağlanır.

### ⚠️ Sunum/his (ÇOK ÖNEMLİ)
Dövme bir **form/gösterge doldurma ekranı DEĞİL**. **Animasyonlu fiziksel bir sahne** olacak. Oyuncu gerçekten demircilik yapıyormuş gibi hissedecek. Akış:

> **Potaya at → Erit → Kalıba dök → Döv → Soğut → Kılıç hazır!**

Her aşama bir **fiziksel hareketle** (sürükle-at, körüğü pompala, ritimle çekiçle vur, suya daldır) ve ekranda **canlı animasyonla** gerçekleşir.
Taslak: [`mockups/forge-animated.html`](mockups/forge-animated.html).

---

### Derinlik katmanları (2026-10-27 — hepsi çekirdekte)
Referans oyunlar: Kingdom Come 2 (fiziksel akış, bileme), Fantasy Blacksmith (parçalı silah, süsleme), Shop Titans / Blacksmith Legends (ustalık, işçi), Atelier (malzeme özellikleri), Potion Craft (keşif), Moonlighter / Recettear (dükkân).

- **Tam akış:** `Potaya at → ERİT/ISIT → Kalıba dök → DÖV → SOĞUT → BİLE → BİRLEŞTİR → SÜSLE`
- **Parçalı silah:** `Ağız + Balçak + Kabza + Topuz`. Her parça ayrı malzemeden olabilir → istatistik kombinasyonu + görsel çeşitlilik.
- **Malzeme özellikleri (Atelier tarzı):** her cevher/parçanın 1–2 özelliği var (Saf, Alevli, Ağır, Kırılgan, Şanslı…), silaha aktarılır. Maden ve ava gitme sebebi.
- **Alaşım keşfi:** potada karıştırma → yeni alaşım (bakır+kalay=bronz, demir+kömür=çelik, gizli efsanevi alaşımlar) → **Alaşım Defteri**.
- **BİLE:** taşlama çarkında kaydırma → keskinlik. **SÜSLE:** kakma, gravür, taş yuvası → satış değeri (opsiyonel adım).
- **Katlama (Şam çeliği):** DÖV'de opsiyonel; her kat kalite + desen güzelliği ↑, hata riski ↑.
- **Ustalık:** tarif yıldızları (yaptıkça kalite şansı ↑, varyant açılır), usta yetenek ağacı (Isı / Çekiç / Bileme / Ticaret), alet yükseltmeleri (iyi ocak = geniş ısı bölgesi, iyi çekiç = büyük vuruş noktası).
- **Çırak:** ustalaşılmış tarifi otomatik üretir → oyuncu sadece zor/özel işleri elle yapar, tekrar sıkmaz.
- **Kademeli açılma (önemli):** oyun yalnızca ISIT → DÖV → SOĞUT ile başlar; diğer adımlar ve sistemler ilerledikçe tek tek açılır. Yeni oyuncu boğulmaz, eski oyuncu sürekli yeni şey keşfeder.
- Dükkân tarafına taşınacak fikirler: **usta damgası + isimli silahlar** (kasabada hikâyesi anlatılır), **özel siparişler** ("hafif, keskin, ateş elementli, gümüş kabzalı hançer" = bulmaca).

## 3) Açık / sıradaki işler (demircilikte)

Dövme akışının adımları yukarıdan aşağı detaylandırılacak:
- [x] **1. Malzeme & Oran** — oturdu (yukarıdaki kararlar)
- [x] **2. ISIT** — oturdu
  - Kontrol: **körüğü basılı tut = ısı yükselir, bırak = düşer.** Amaç: ibreyi metalin renkli ideal bölgesinde tutup dolum çubuğunu doldurmak. Tek parmak. Süre ~8–10 sn.
  - **Metal farkı = bölge + atalet:** her metalin ideal bölgesi farklı yerde/genişlikte, ibresi farklı hızda tepki verir. Demir: geniş bölge, ağır ibre (kolay). Çelik: orta. Mitril: dar, hızlı. Yıldız demiri: çok dar, çok sıcak. **Kömür miktarı** ibrenin yükselme hızını değiştirir (az = yavaş, çok = fırlar).
  - **Hata affedici:** bölge dışında geçen süre ISIT puanını düşürür; metal **yanmaz, malzeme kaybolmaz.** Çok kötü oyun en fazla Çürük kademeye iter.
  - ISIT puanı = ideal bölgede geçen süre yüzdesi → SONUÇ formülüne girer. Bölgenin **ortası** daha değerli (merkez 1, kenar 0.2).
  - **Zorluk metale göre artar** (demir ★ · çelik ★★ · mitril/alaşım ★★★): kıymetli metalde ideal bölge yavaşça **kayar**, ocakta ara ara **kömür patlaması** ("çıt!" / "fıss…") ibreyi iter, dolum süresi uzar.
  - Metaller potaya kendi biçimleriyle girer: **demir = kaba cevher**, **çelik = külçe**, **mitril = kristal**.
- [x] **3. DÖV** — oturdu (katlama: opsiyonel, bkz. Derinlik katmanları)
  - Kontrol: **parlayan noktalara vur.** Örsteki metalin üstünde sırayla noktalar belirir, etraflarındaki halka küçülür; halka oturduğu anda dokun → Kusursuz / İyi / Kaçtı. ~8–12 vuruş, metal her vuruşta gözle görülür şekil alır.
- [x] **4. SOĞUT** — oturdu
  - Kontrol: **daldır-tut-çıkar.** Kılıcı aşağı sürükleyip sıvıya daldır, buhar çıkar, metal rengi solar; doğru renkte yukarı çek. Erken = yumuşak (sağlamlık↓), geç = kırılgan. Hareket ISIT/DÖV'den farklı (sürükleme).
  - **Sıvılar:** Su = keskinlik↑ kırılganlık↑, dar pencere. Yağ = sağlam/dengeli, geniş pencere (kolay). Özel sıvılar silaha özellik ekler, nadir/pahalı: Buz suyu → Buz, Ejderha kanı → Ateş (çok nadir), Simyacı iksiri → özel/rastgele özellik.
- [x] **5. BİLE** — oturdu
  - Kontrol: **ağzı çizgiyle takip et.** Taşlama çarkı döner; parmağı bıçağın parlayan ağız çizgisi boyunca kaydır. Çizgiye yakınlık + düzgün hız = keskinlik. Kıvılcımlar parmağı izler.
  - **Geçiş sayısı = ödünleşme:** her geçiş keskinlik↑, sağlamlık↓ (ağız incelir). Oyuncu ne zaman duracağına kendi karar verir (hassas hançer ~5 geçiş, savaş baltası ~2).
  - **Sahne:** taş çark **kılıcın altında**, tahta sehpa + pedal üstünde; bilerken **parmağı izleyerek** ağız boyunca kayar. Kıvılcımlar çarkın değdiği noktadan dönüş yönünde (sağa) fışkırır. Ağız boyunca her nokta kendi **bilenme parlaklığını** tutar: bilenen yer parlar, bilenmeyen mat kalır.
  - **Zorluk:** ağız çizgisi düz değil **dalgalı** — kötü dövülmüş ağız daha dalgalı, kıymetli metalde tolerans daha dar. Kaydırma **hızı yeşil bantta** tutulmalı (hız son ~0,12 sn'lik gerçek yoldan ölçülür, gösterge yumuşatılır; yeşil bant göstergenin ortasında); parmak durursa **"Tav kaçtı!"** (geçiş puanı ve sağlamlık düşer).
  - **Sağlamlık dengesi:** her metalin temel sağlamlığı var (demir 85 · çelik 78 · mitril 92). İyi geçiş sağlamlığı az aşındırır (~4), kötü geçiş daha çok (~8). Sonuçta **kırılma riski** gösterilir (100 savaş vuruşunda %X; iyi bir kılıç ~%5–8).
- [x] **SOĞUT görsel:** maşayla tutulan gerçek kılıç; suya girerken sıçrama + "Tsssss!", buhar bulutları, kabarcıklar. Kılıcın **tamamı eşit** soğur (tek renk, şerit o rengi gösterir).
- [x] **SOĞUT — sade: daldır, kılıcın rengine bak, çek.** Ekranda gösterge/şerit **yok**; oyuncu kararını yalnızca kılıcın rengine bakarak verir. Kılıç soğurken **6 renk kademesinden** geçer (kademe sonlarında bir sonrakine kısa yumuşak geçiş):

  | Kademe | Renk | Sonuç | Puan |
  |---|---|---|---|
  | 1 | Beyaz | çok erken | 0,10 |
  | 2 | Sarı | erken | 0,25 |
  | 3 | Turuncu | biraz erken (yumuşak) | 0,50 |
  | **4** | **Kiraz kırmızısı** | **ÇEKME ANI** | 0,75 – 1,00 (ortası en iyi) |
  | 5 | Gri-mor | sıkıntı: çatlaklar belirip çoğalır ("çıt!"); çekilebilir ama kırılgan | 0,30 → 0,10 |
  | 6 | Siyah | **kırılır** | — |

  - **6. kademe = kalıcı kayıp:** kılıç titreyip kırmızı çatlaklarla parçalanır, **siyah parçalara** ayrılır. **Kılıç da potaya atılan malzemeler de kaybolur** (cevher/külçe/kristaller + varsa özel sıvı); yalnızca "Baştan başla".
  - Renk sırası, daldırmadan önce açıklama metninde küçük renk kutucuklarıyla gösterilir (şerit değil).
  - Sıvılar artık yalnızca **hız** ile ayrışır: yağ kırmızıya ~6 sn, kırmızı ~1,6 sn sürer · su ~4,5 / 1,2 sn · buz suyu ~3,9 / 1,0 sn.
  - (Denenip kaldırıldı: üstte sıcaklık şeridi + HEDEF penceresi; su içinde sallama + "buhar ceketi" — oyuncuya karışık geldi.)

### Kılıç görünümü malzemeye göre (2026-10-27)
Aynı kalıptan çıkan kılıçlar bile malzemesine göre **farklı görünür** — oyuncu her yeni karışımda yeni bir kılıç görür. Görünüm SOĞUT, BİLE ve SONUÇ'ta aynı (tek kılıç çizicisi).

| Malzeme | Ağız | Desen | Balçak | Topuz |
|---|---|---|---|---|
| Demir | mat koyu gri | pas lekeleri | düz, demir | yuvarlak |
| Çelik | parlak çelik | — (cilalı) | uçları kıvrık, pirinç | yuvarlak |
| Karbonlu Demir · Sertleşmiş Çelik | orta ton | şam çeliği dalgaları | düz / kıvrık | yuvarlak |
| Mitril | turkuaz, hafif hale | parlayan rün oluğu | kanatlı, gümüş | elmas kristal |
| Mitril Damarlı Demir | koyu gri | turkuaz damarlar | dikenli | elmas |
| Gök Demiri | gece mavisi, mavi hale | yıldız benekleri | kanatlı | elmas |
| Ay Çeliği | gümüş-mavi | hilal izleri | kıvrık, gümüş | halka |
| Mitril Çeliği | açık turkuaz | beyaz damarlar | kanatlı | elmas |
| Üç Damar | gri | üç renkli çapraz şeritler | dikenli | halka |

Topuz ve balçak mücevheri sonuç ekranında **kademe rengini** alır. İleride: kalıba göre siluet (pala, hançer…), SÜSLE adımında gravür/kakma bu desenlerin üstüne eklenir.
- [x] **DÖK görsel:** pota ağzına kadar dolu başlar, metal yüzeyi yatay kalarak dökülen miktarla birlikte düzgünce azalır; kalıp %100 dolar.
  - Pota **kalın duvarlı grafit döküm potası** (akıtma ağzı, altı közle parlar), demir kucak halkası + uzun demir sap; sapı **deri eldivenli demirci eli** tutar, kol ekran dışından uzanır.
  - Döküldüğü yer **kum kalıbı**: demir köşebentli tahta çerçeve, kum dokusu, **kılıç biçimli oyuk** (ağız + balçak + sap) ve soldaki **döküm hunisi**. Metal huniden girip oyuğu doldurur, sıcak metalin değdiği kumdan duman tüter.
- [x] **Demircinin eli (tüm sahnelerde aynı):** geniş deri manşetli eldiven, bilekten dirseğe kalınlaşan **kaslı ön kol** (ışık alan kas, gölge, kas çizgileri), sıvanmış kumaş yen. DÖK'te potanın sapını, DÖV'de çekici, SOĞUT'ta silahı sapından tutar.
- [x] **Kum kalıpları (silah türleri):** malzeme ekranında kalıp seçilir — **Uzun Kılıç, Kısa Kılıç, Balta, Mızrak**. Kalıba yalnızca **metal kısım** dökülür ve **örse o gelir** (kalıp = örsteki parça; dökme ile dövme birbirini tutar). Sap/kabza/balçak sonradan, BİRLEŞTİR'de takılır: **SOĞUT ve BİLE'de yalnızca çıplak metal** görünür (kılıçta sap ucunu el doğrudan, balta/mızrakta maşa tutar; SOĞUT'ta hep maşa + aynı eldivenli el), **SONUÇ'ta silah bütün hâliyle**. Kum kalıbının kutusu dökülen parçanın boyuna göre kısalır/uzar.
  - **Kalıp = örsteki parça, birebir (2026-10-27):** her biçim tek bir "parça tanımından" çizilir (yatay; x=0 sapın takıldığı yer). Kalıptan çıkan **ham parça** (%10 kısa, %30 kalın, ucu küt) kalıp oyuğunun ve örse gelen parçanın **aynısıdır** (aynı biçim, aynı boy, aynı ölçek); dövdükçe asıl biçimine geçer. DÖK, DÖV, SOĞUT ve BİLE parçayı bu tanımdan 1:1 çizer; kalıp kutusu da parçanın boyuna göre ayarlanır.
  - **Alt biçimler (her kalıbın 3 biçimi):**

    | Kalıp | Biçimler | Ayırt edici |
    |---|---|---|
    | Uzun Kılıç | Şövalye Kılıcı · Katana · Osmanlı Kılıcı | düz çift ağız + haç balçak · hafif kavis, tek ağız, kissaki, tsuba + uzun ito sargı · güçlü kavis, ucu genişleyen yelman + sahte ağız, uçları kıvrık balçak + tabanca kabza |
    | Kısa Kılıç | Kısa Kılıç · Hançer · Yatağan | geniş düz ağız · yaprak biçimli kısa ağız, küçük balçak · öne kavisli (içbükey ağız), balçaksız, kemik kulaklı kabza |
    | Balta | Tek Ağızlı · Çift Ağızlı · Sakallı | arkada çekiç yüzü · iki yanda simetrik ağız · ağzı sapa doğru sarkan "sakal" |
    | Mızrak | Yaprak Mızrak · Kanatlı Mızrak · Kargı | yaprak uç · yuvada iki kanat · ince uzun uç |

    Her biçimin kendi hasar/ağırlık/değer çarpanı ve ad kökü var ("Ay Çeliği Katanası", "Çift Ağızlı Baltası", "Kargısı"); katana, hançer gibi biçimler keskinlik bonusu alır.
  - **SOĞUT yatay:** dövülen parça yatay olarak, sıvı dolu küçük **demir tekneye** (perçinli, ayaklı; boyu parçaya göre) daldırılır; el parçayı yandan maşayla tutar. Buhar parçanın üstünden yükselip kenarlara açılır ve teknenin ağzından **dışarı taşar**.
  - **ISIT sahnesi:** iki direk üstünde **demir ray**, raydaki **makaralı araba**dan sarkan **zincire asılı pota** közlerin üstünde durur (mangalda demire asılı çaydanlık gibi). Taş ocak + kor yatağı + alevler; solda kama biçimli **deri körük** (üst tahta + kol): basılı tutunca kol inip kalkar, körük katlanır, borudan ocağa hava üfler. Seçim ekranında duvardaki levhada seçilen biçim görünür.
  - **DÖV — parça örse oturur:** balta başı alt hattı örse yaslanacak biçimde yatırılır (tek ağızlıda hafif eğik, sakallıda sakalı üzerine, çift ağızlıda iki ağzıyla); **sol el maşayla** parçayı örse bastırır, sağ el çekici savurur; değdiği yerde örs yüzü kızarır.
  - **Kısa kılıç biçimleri (2026-10-28, kullanıcının örnek görsellerine göre):** Kısa Kılıç = **kopis** (dipte dar, uca doğru göbeklenen tek ağız, sırt öne eğik; çentikli küçük koruma, sırta kavisli bilezikli sargı, öne kıvrık kanca topuz + halka + püskül) · Hançer = **düz çift ağızlı hançer** (geniş dipten düz incelir, ortası sırtlı; uçları toplu haç balçak + süslü orta blok, spiral tel sargılı kabza, top topuz) · Yatağan = **pala tipi kısa kavisli kılıç** (sırta doğru düzgün kavis; uçları helezon kıvrık balçak, ağız tarafına eğik ahşap tabanca kabza + pirinç uç).
  - **Hançer (düzeltildi, 2026-10-28):** ince üçgen diken mızrak ucu gibi duruyordu; artık ağzın yarısından fazlası neredeyse paralel ve geniş, uçta yaprak gibi kavisle (ogival) sivrilir, ortası sırtlı; ağız kabzanın ~2 katı.
  - **Envanter (2026-10-28):** 🎒 cevherler (Demir cevheri / Çelik külçesi / Mitril kristali) + yapılan silahlar; tarayıcıda saklanır. Başlangıç stoğu: 6 demir, 3 çelik, 1 mitril.
    - Potaya **yalnız envanterdeki cevher** konabilir (yuvalar stokta olmayanı atlar); "Potaya at" ile cevherler envanterden **düşer** — soğutmada kırılırsa geri gelmez.
    - Biten silah **envantere girer** (ad, kademe, tür, metal, değer).
    - **Geri eritme:** envanterdeki her silahta "🔥 Erit" — içindeki 3 cevherden **2'si geri döner, 1'i kaybolur** (rastgele). Yaptıkça-erittikçe malzeme azalır; kötü silahı eritip yeniden denemek mümkün ama bedelli.
    - Cevher 3'ün altına düşerse dövme başlamaz ("bir silahı erit"); prototipte "↺ Başlangıç stoğu" düğmesi var (oyunda yerini maden/tüccar alacak).
  - **SOĞUT teknesi ortada:** tekne ve parça alanın ortasında durur; kısa parçalarda tekne küçük ama yine ortada.
  - **BİRLEŞTİR — raf:** butonlar yerine tezgâhın üstündeki duvarda **raf**; kabza/sap seçenekleri rafta asılı (o biçimin kabzası, seçeneğin renkleriyle). Metale uyumlu olanın üstünde ✓, kilitliler karartılmış + kilit. Parça **sürüklenip** metal parçanın ucuna bırakılır ("klik", yaklaşınca yeşil parlar) ya da rafta dokunulur; yanlış yere bırakılan rafa döner; "↩ Çıkar" ile sökülür; sonra perçine 3 kez vurulur. Baltada tezgâh kısa: balta başı kenardan sarkar.
  - **Sap boyları:** balta sapı kısa (mızrağın ~%60'ı), mızrak sapı uzun.
  - **El:** kısa ve tıknaz **cüce kolu** — kalın kaslı ön kol + kabarık yuvarlak yen ucu (ince uzun kol yok).
  - **Prototip akışı (8 adım):** `Malzeme → Isıt → Dök → Döv → Soğut → Bile → Birleştir → Sonuç` (SÜSLE ileride).
  - **Mızrak (yenilendi):** dibi dar, üçte birde en geniş, uca doğru incelen yaprak uç; ortada ışıklı sırt (iki tonlu), dipte iki küçük kanat, iki bilezikli yuva + renkli püskül; sapın dibinde demir uç.

  | Tür | Kalıptaki / örsteki parça | Hasar | Ağırlık | Değer | Bileme yolu |
  |---|---|---|---|---|---|
  | Uzun Kılıç | sap ucu + uzun ağız | ×1 | ×1 | ×1 | ağız boyunca (uzun) |
  | Kısa Kılıç | sap ucu + kısa ağız | ×0,78 | ×0,6 | ×0,75 | ağız boyunca (kısa) |
  | Balta | balta başı (delikli, ağzı genişler) | ×1,25 | ×1,35 | ×0,9 | aşağı bakan balta ağzı |
  | Mızrak | yuva + yaprak uç | ×1,05 | ×1,15 | ×0,85 | ucun alt kenarı |

  Ad üretimi türe göre: "Ağır Demir Balta", "Dağın Demir Baltası", "Nöbetin Ay Çeliği Mızrağı"… Kısa bileme yollarında süre cezası yol boyuyla ölçeklenir.
- [x] **DÖV görsel — cüce çekici:** kısa sap (demir bilezikler + deri sargı + pirinç topuz), kalın kafa: geniş vuruş yüzü, arkada sivri uç, ortada **altın rün bandı**, perçinler. Çekici **deri eldivenli el** tutar, bilekten savrulur.
- [x] **6. BİRLEŞTİR** — oturdu
  - **Parçaların kaynağı:** balçak ve topuz küçük kalıba **hızlı döküm**le yapılır (tam ISIT/DÖV yok, tek dokunuşluk mini an). Kabza = ahşap + sargı (deri, ipek, ejderha derisi…), dükkânlardan / avdan gelir. Parçalar önceden üretilip **parça rafında** stoklanabilir.
  - **Marketten hazır alma:** kabza, balçak, topuz hazır olarak da satın alınabilir. Hazır = hızlı ama pahalı, kalite genelde Sıradan/İyi. Kendin yapmak = ucuz, kalite ve özellik senin elinde. Gezgin tüccar arada nadir hazır parça getirir (ör. elf işi kabza).
  - Kontrol: **sürükle-tak + perçin.** Parçayı raftan sürükleyip ağzın üstüne bırak, "klik" diye oturur; perçine 2–3 kez dokunup çivile. Beceri az, keyif seçimde ve silahın göz önünde tamamlanmasında. Her seçimde istatistik önizlemesi (hasar, ağırlık…) görünür.
  - **Prototipte (2026-10-27):** BİLE'den sonra, SONUÇ'tan önce. Tezgâhta çıplak metal yatar; seçilen kabza/sap **kayarak yerine oturur**, sonra parlayan **perçine 3 kez** dokunulur (ilk vuruştan sonra seçim kilitlenir). Kılıçlarda **kabza**, balta ve mızrakta **sap** seçilir. Seçenekler **metalin cinsine göre**: 🔒 = daha kıymetli metal ister, ✓ = metalle uyumlu (uyumluysa +5 sağlamlık, değer ×1,1, özellik olarak yazılır); metale uyumlu seçenek varsayılan gelir.

    | Kabza (kılıç) / Sap (balta, mızrak) | Sağlamlık | Değer | Ağırlık | Uyum | Şart |
    |---|---|---|---|---|---|
    | Deri sargılı ahşap kabza / Kayın sap | +0 | ×1 | ×1 | Demir → *Sağlam iş* | — |
    | Kemik kabza / Meşe sap, demir bilezikli | +5 / +6 | ×1,12 | ×1,02 / ×1,08 | Çelik → *Usta dengesi* | — |
    | İpek sargılı abanoz / Abanoz sap, ipek sargılı | +0 | ×1,35 | ×0,98 / ×0,96 | Mitril → *Elf işi* | Seyrek+ |
    | Ejderha derisi kabza / Ejderha kemiği sap | +8 | ×1,6 | ×1 | — (🐉 Ejder kavrayışı, hasar +%5) | Kıymetli |
- [x] **7. SÜSLE** — oturdu (opsiyonel adım; hepsi kademeli açılır)
  - **Gravür:** parmakla ağız üzerindeki hayalet deseni takip et (BİLE gibi ama kıvrımlı). Desenler keşfedilir / satın alınır: sarmaşık, ejderha, rune… → satış değeri↑
  - **Taş yuvası:** balçağa/topuza yakut, kristal vb. sürükle-bırak → element/büyü özelliği; taşın kalitesi önemli.
  - **Kakma:** altın/gümüş tel gömme → sadece görünüm + fiyat; soylu müşteriler sever.
  - **Usta damgası + isim:** oyuncu kendi damgasını tasarlar, her silaha vurur; Efsanevi+ silahlara isim verilir → kasabadaki ün/hikâye sistemine bağlanır.
- [x] **8. SONUÇ** — oturdu
  - Her adım 0–100 puan verir (ISIT · DÖV · SOĞUT · BİLE, +SÜSLE bonusu) → **ağırlıklı ortalama = Performans.** Ağırlıklar silah türüne göre değişir (kılıçta BİLE, balyozda DÖV daha önemli).
  - **Beceri tabanı, şans tavanı:** Performans + malzeme kalitesi + alet seviyesi + tarif ustalığı → garanti bir **taban kademe**. Şans sadece yukarı iter (bir üst kademe şansı, çok küçük ihtimalle iki). İyi oynayan asla cezalandırılmaz; İmkansız yine nadir kalır.
    - Örnek: Performans %95 + iyi malzeme → taban Usta İşi, %20 Efsanevi, %1 İMKANSIZ. Performans %40 → taban Sıradan, %15 İyi.
  - **Dramatik açılış:** silah kaldırılır, ışık kademe renklerinden geçer (gri→yeşil→mavi→mor→altın), durduğu renk = kademe; istatistik + özellikler görünür. Efsanevi'de altın patlama, İMKANSIZ'da özel sahne + isim verme. Sıradan sonuçlarda ve çırak üretiminde açılış kısalır/atlanabilir (tekrarda yormasın).
- [ ] Sahnenin nihai görsel tasarımı (animasyonlu sahne mockup'ı üzerinden)

---

## 3b) Dükkân — alınan kararlar (2026-10-27)

Referans oyunlar: Moonlighter (raf + fiyat + yüz ifadesi), Recettear (pazarlık, müşteri kişiliği, dükkân seviyesi), Shop Titans (istek + öneri, mobilya), Holy Potatoes (kahraman silahını kullanır), Stardew (koleksiyon, kargo sandığı).

- **Düzen:** vitrin (öne çıkan ürün), raflar, tezgâh, kapıda tabela.
- **Satış anı = canlı dükkân saati:** dükkânı açınca ~2–3 dk gerçek zamanlı sahne. Müşteriler kapıdan girer, rafları gezer, tezgâha gelir; oyuncu tezgâhta ilgilenir (pazarlık, öneri).
- **Müşteri tipleri** (kafada düşünce balonu ne istediğini gösterir):
  - 👨‍🌾 Köylü: ucuz alet / basit silah · ⚔️ Maceracı: istatistik + element · 🛡️ Muhafız: toplu/tekrarlanan sipariş · 👑 Soylu: süslü/kakmalı, iyi öder · 🔍 Koleksiyoncu: nadir özellikli / isimli · 🎒 Gezgin: para yerine nadir malzemeyle takas
- **Fiyat = yüz ifadesi + Fiyat Defteri:** fiyatı oyuncu koyar; tepki (😍 ucuz · 🙂 doğru · 😐 pahalı · 😡 çok pahalı) defterde kaydolur, "tatlı nokta" keşfedilir.
- **Pazarlık = hafif kaydırma:** müşteri teklif verir, oyuncu kaydırıcıyla karşı teklif yapar; sabır çubuğu 2–3 tur, kişiliğe göre değişir (soylu sabırsız ama zengin). ~5 sn. Atlanıp sabit fiyatla satılabilir.
- **Öneri:** "ateşli bir şey arıyorum" → stoktan uygun ürünü önerirsen bonus. Malzeme özellikleri burada anlam kazanır.
- **Sipariş panosu:** süreli + bonuslu siparişler, özel sipariş bulmacaları, muhafız sözleşmeleri (düzenli gelir).
- **Dekorasyon + çekicilik:** mobilya/süs yerleştir → çekicilik↑ → daha çok ve daha zengin müşteri.
- **Tamir hizmeti:** maceracı aşınmış silah getirir → kısa DÖV → hızlı para (erken oyunda ana gelir).
- **Talep panosu + olaylar:** kasaba olayları talebi değiştirir (kurt saldırısı → mızrak talebi↑) → fiyatlar oynar.
- **Kargo sandığı / toptancı:** istenmeyen ürün düşük fiyata otomatik satılır, envanter tıkanmaz.
- **Dükkân seviyesi:** satışla yükselir → yeni raf, müşteri tipi, çırak açılır.

## 3c) Gün döngüsü — alınan kararlar (2026-10-27)

- **İskelet:** 🌅 Sabah dükkân (canlı satış, siparişler) → ☀️ Öğlen market (ileride maden/av) → 🔥 Akşam demirhane (dövme, parça dökümü, tamir) → 🌙 Gece han/uyku → **gün özeti** (kazanç, ün, yarının talebi/haberi — "yarın soylu kafile geliyor!") → kayıt.
- **Saatli gün (06:00–24:00):** yürürken saat akar; bir dövme ~1–2 oyun saati harcar, dükkân saati sabahı kaplar. Dövme sahnesinin süresi sabit — acele/stres yok. 1 gün ≈ 12–15 dk gerçek zaman.
- **Sınır = zaman + yakıt:** enerji çubuğu yok. Günlük üretimi günün saati ve ocağın kömürü sınırlar; ikisi de oyun içinde geliştirilebilir (büyük ocak, çırak). Asla "enerji satın al" baskısı yok.
- **Takvim: 4 mevsim × 28 gün.** Mevsime göre talep ve malzeme değişir (kışın kürk kabza, yazın balıkçı bıçağı); her mevsimde 1–2 festival (ör. Sonbahar 15 — Demirciler Yarışması). İlk sürüm tek mevsimle başlayabilir.

## 3d) Hikâye ve ilerleme — alınan kararlar (2026-10-27)

- **Başlangıç hikâyesi = ikisi birden:** ustanın demirhanesini miras aldın ama usta esrarengiz şekilde kayboldu; o gidince kasaba da söndü. Geride yarım notlar ve kilitli tarif sayfaları var ("Yıldız demirini bul. Ocağı söndürme.").
  - **Kısa vade:** dükkânı büyüt → kasaba canlanır (han tamir edilir, kuyumcu geri döner, yeni dükkânlar açılır) — Stardew Topluluk Merkezi hissi.
  - **Uzun vade:** kayıp tarif sayfalarını bularak ustanın sırrını çöz → efsanevi alaşım / yıldız demiri.
- **Kademeli açılma — yavaş tempo** (her sistem bir süre tek başına öğrenilsin):

| Zaman | Açılan |
|---|---|
| Bahar 1–3 | ISIT → DÖV → SOĞUT · hançer kalıbı · 1 raf · köylü müşteriler |
| Bahar 4–7 | Tamir hizmeti · fiyat defteri |
| Bahar 2. hafta | BİLE · kısa kılıç · maceracılar |
| Bahar 3. hafta | Sipariş panosu · ikinci raf |
| Bahar 4. hafta | BİRLEŞTİR · parça rafı · market parçaları |
| Yaz | Pazarlık · alaşım keşfi · muhafız sözleşmeleri · dekorasyon |
| Sonbahar | SÜSLE · soylular · çırak · Demirciler Yarışması (Sonbahar 15) |
| Kış ve sonrası | Katlama · koleksiyoncular · nadir metaller · efsanevi alaşımlar · ustanın sırrı |

## 4) Sonraya bırakılan fikirler (cep)

- **Ün duvarı** (isimli silahların sahipleri/hikâyeleri, koleksiyon) ve **hırsız yakalama** mini olayı

- **B** — dövme hareketinden silah şeklinin doğması
- Sınıf/ırk sistemi (Cüce / İnsan / Elf / Ork — her biri ısı penceresini, şans eğrisini, kullanılabilir malzemeleri değiştirir) → **en sona**
- Başka dükkanlar / mağazadan ürün alma
- Kendi evimiz
- Han / yemek yenen mekânlar

---

## 5) Çalışma yöntemi notu

Tasarım, superpowers **brainstorming** skill'i + tarayıcı **görsel taslak (visual companion)** ile adım adım yapılıyor. Kod yazımına **ancak tasarım onaylanınca** geçilecek (önce yazılı tasarım → sonra plan → sonra kod).
Commit tarzı: **İngilizce**, önek yok (feat/fix/refactor vb.), imza yok (Co-Authored-By vb.), kısa ve öz mesaj; işler mantıklı parçalara bölünüp **birden fazla commit** olarak atılır.
