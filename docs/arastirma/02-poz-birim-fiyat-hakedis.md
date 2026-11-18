# 02 — Poz, Resmî Birim Fiyat, Yaklaşık Maliyet, Hakediş ve Fiyat Farkı

> Belge numaraları (00–13), karar numaraları (K-xx, D-xx) ve "pilot keşif" kavramı için: [ARASTIRMA-OZETI.md](../ARASTIRMA-OZETI.md#bu-belgeler-nasıl-okunur).

> Araştırma agent'ı B · Erişim tarihi (tüm kaynaklar): **18.11.2026** · Kaynak kısaltmaları [K#] dosya sonundadır.
> Doğrulama etiketleri: **(doğrulandı: resmî kaynak)** / **(ikincil kaynak)** / **(doğrulanmadı)**. Mevzuat metinleri bu çalışmada çoğunlukla ikincil derleyicilerden (herpoz.com, alomaliye.com) okundu; uygulamaya geçmeden önce mevzuat.gov.tr / Resmî Gazete'den teyit edilmeli.

## Özet

1. **Ana kaynak Yüksek Fen Kurulu'dur (YFK, Çevre, Şehircilik ve İklim Değişikliği Bakanlığı).** 2026 rayiç, inşaat ve tesisat birim fiyatları ile analizler 15.01.2026'da yayımlandı ve 01.01.2026'dan itibaren geçerli. Eylül 2025 döneminden beri bunlara ek olarak **aylık güncel rayiç ve birim fiyat listeleri** de yayımlanıyor (dayanak: RG 30.07.2025/32971 YİİUY değişikliği; TÜİK endeksleriyle hesaplandığı doğrulanmadı). Mevcut en yeni liste Temmuz 2026'ya ait; sonraki aylar doğrulanmadı. [K1][K2][K3][K5]
2. **Lisans sorunu kritik.** YFK platformunun erişim beyanına göre içerik yalnızca ekranda görüntülenebilir. Yazılıma, dijital platforma veya veri tabanına aktarılması, Bakanlığın yazılı izni olmadan yasaktır (5846 sayılı FSEK'e atıfla). Bu yüzden resmî poz kataloğunun ERP'ye otomatik çekilmesi şimdilik **hukuken riskli**. [K4]
3. **Resmî bir API ya da XML yayını bulunamadı.** Yayınlar web sayfası ve PDF biçiminde. Piyasada lisanslı veri sağlayıcılar var: AMP Yazılım (birimfiyat.net) ve Oska Yazılım (birimfiyat.com). Ticari kaynağa göre YFK'nin lisanslı kullanım hakkı AMP'ye verilmiş. [K7][K11]
4. **Yüklenici firma için asıl veri, idarenin poz kataloğu değil sözleşmenin kendisidir.** Birim fiyat teklif cetveli, metraj, yeşil defter, hakediş dönemleri ve kesintiler bu kapsamda. Yaklaşık maliyeti idare hazırlar; firma teklif maliyetini hesaplar. Bu ayrım MVP kapsamını belirgin biçimde küçültür. [ÖNERİ]
5. **Hakediş kuralları Yapım İşleri Genel Şartnamesi'nde (YİGŞ).** Geçici hakediş için md. 39, kesin hesap ve kesin hakediş için md. 40, yeni birim fiyat için md. 22 geçerli. Üçü de **RG 30.07.2025 / 32971** ile değişti (yürürlük 01.09.2025). Ancak YİİUY Geçici Madde 34'e göre bu değişiklikler **yalnız 01.09.2025 ve sonrasında ilan edilen ya da davet yapılan ihalelere** uygulanır; daha önceki sözleşmeler eski kurallarla yürür. Bu yüzden ERP'de kural sürümü ihale ilan tarihine göre seçilmeli. [K16][K24]
6. **Fiyat farkının temel formülü F = An × B × (Pn − 1); B = 0,90.** Pn, sözleşmede sabitlenen ağırlıklarla hesaplanır: TÜFE (işçilik), Yİ-ÜFE alt endeksleri ve akaryakıt fiyatı. 2026'da TÜFE'nin baz yılı 2025=100 oldu. KİK'in 2026/DK.D-332 sayılı kararı, işçilik endeksinde 2003=100 "Genel" sütunu yerine doğrudan TÜFE 2025=100 değerlerini esas alıyor. **Açık kalan tek nokta temel endeksin (İo) yorumu.** [K12][K14][K25]
7. **MVP için önerilen kapsam:** sözleşme kalemleri, metraj/yeşil defter, ara hakediş, kümülatif takip, parametrik kesintiler, Excel/PDF çıktı ve elle endeks girişli fiyat farkı. **Yüksek riskli olanlar:** resmî katalog içe aktarımı, otomatik fiyat farkı, idareye özgü resmî hakediş formatları. [ÖNERİ]

---

## 1. Birim fiyat yayımlayan kurumlar

| Kurum | 2026 durumu | Yayın sıklığı / biçimi | Poz yapısı (örnek) | Doğrulama |
|---|---|---|---|---|
| **ÇŞİDB – Yüksek Fen Kurulu** (inşaat, mekanik, elektrik + rayiç + analiz) | 15.01.2026'da yayımlandı, yürürlük 01.01.2026 [K2] | Yıllık ana yayın ve 09/2025'ten beri **aylık güncel rayiç/birim fiyat listeleri** (PDF; Haziran–Temmuz 2026 örnekleri var) [K3][K5][K6] | `15.xxx.xxxx` inşaat, `25.` mekanik, `35.` elektrik (örn. `15.455.1002`, `35.170.1780`) [K9]; rayiç örneği `10.100.1062` Düz işçi (saat) [K11] | Yayın: doğrulandı (resmî). Poz önekleri: ikincil |
| **Karayolları GM (KGM)** — yol, köprü, tünel, bitümlü kaplama, bakım, trafik | 2026 listesi **bulunamadı** | Yıllık (2025 listesine atıflar var) [K11] | `KGM/4436`, `KGM/6208`, `KGM/4436/M` (eski tip eğik çizgili biçim) [K11] | Doğrulanmadı / ikincil |
| **İller Bankası (İLBANK)** — altyapı, içme suyu, kanalizasyon | 2026'da yayımlanacağı söylendi; yayım **doğrulanmadı** [K7] | Yıllık; YFK'den sonra çıkar [K8] | `43.527.1530`, `43.503.1314` [K11] | İkincil |
| **DSİ** | 2026 birim fiyat kitabı **bulunamadı** | Doğrulanmadı | Doğrulanmadı | Doğrulanmadı |
| **Kültür ve Turizm Bak.** (restorasyon) | Bakanlık sitesinde "2026 KTB hata düzeltme cetveli" (16.02.2026) var; bu bir 2026 yayını olduğunu düşündürüyor [K22] | Doğrulanmadı | Doğrulanmadı | Kısmen (resmî dosya adı) |
| Diğer yetkili idareler: Ulaştırma ve Altyapı Bak., MSB, Vakıflar GM, PTT, OGM, TEDAŞ | Ticari kaynağa göre YFK dışında **10 idarenin** yayın yetkisi var [K8] | Genelde YFK'den sonra yayımlanır | — | İkincil. TCDD'nin ayrı bir yetkisi doğrulanmadı |

**Poz numarası ve sürüm notları**
- 2019 birim fiyatlarıyla birlikte YFK, tüm idareler için ortak bir numaralandırma sistemine geçti. Biçim kurum kodu + grup + sıra: `XX.XXX.XXXX` (noktalarla birlikte 11 karakter). Resmî bir **eski↔yeni karşılık tablosu** bulunamadı. Eski numarayla arama yalnızca ticari yazılımların sunduğu bir özellik. [K10] (ikincil)
- KGM pozları ikincil kaynaklarda hâlâ `KGM/....` biçiminde görünüyor. Yani **poz kodu tek bir biçimde değil** [K11] (ikincil) → [ÖNERİ] Veri modelinde poz kodu serbest metin olmalı ve her poz bir kuruma bağlanmalı.
- Pozlar her yıl ekleniyor ve kaldırılıyor. 2026'da yaklaşık 135 poz eklendi, 19 poz çıkarıldı; değişikliğin büyük bölümü elektrikte. Bazı pozlar yeni numarayla yeniden tanımlandı (ör. plastik doğrama `15.455.1001` kaldırıldı, PVC `15.455.1002–1005` eklendi) [K9] (ikincil). → Poz kataloğu **yıl/yayın sürümlü** tutulmalı ve kaldırılan pozlar silinmemeli.
- **Analiz yapısı:** Birim fiyat analizi, rayiç bileşenlerinin miktarla çarpımlarının toplamına kâr ve genel gider eklenerek bulunur. Bileşenler malzeme, işçilik (saat), makine ve nakliyedir. Örneğin `15.115.1004` analizinde `10.100.1062` Düz işçi 2,5 saatlik katsayıyla yer alıyor [K11] (ikincil). Kâr ve genel gider oranı, yeni fiyat tespiti için aşağıda §4.4'te ele alınıyor.
- **Rayiç–TÜİK eşleştirme endeksleri:** YFK, her rayicin hangi TÜİK alt endeksiyle güncelleneceğini gösteren listeleri yayımlıyor [K1][K2] (doğrulandı: resmî; içerik görülmedi). Aylık listeler bu eşleştirmeyle üretiliyor gibi görünüyor (doğrulanmadı).

## 2. Veri edinme: yasal ve teknik yollar

- **Resmî kaynak (YFK):** Sayfaya girmeden önce bir "Erişim Beyanı" kabul ettiriliyor. Beyana göre içerik yalnızca ekranda görüntülenebilir ve yazılı izin olmadan çoğaltılamaz. Kaynak gösterilse bile ticari kullanım, üçüncü kişilerle paylaşım ve **yazılım, dijital platform ya da veri tabanında kullanım** yasak [K4] (doğrulandı: resmî). Bu çalışmada beyan kabul edilmedi, listelerin içi incelenmedi.
- **PDF aylık listeler** webdosya.csb.gov.tr üzerinde açık bağlantılarla duruyor [K5][K6] (doğrulandı: dosyaların varlığı). Excel, XML veya API **bulunamadı** (doğrulanmadı = yok olduğu kesin değil).
- **Hukuki belirsizlik [BELİRSİZ]:** FSEK md. 31'e göre resmî metinler koruma dışında kalıyor. Birim fiyat listelerinin bu kapsama girip girmediğini değerlendiren bir kaynak bulunamadı. Bakanlığın açık yasak beyanı karşısında **hukuk görüşü alınmadan** toplu içe aktarma (scraping, PDF ayrıştırma) yapılmamalı. [ÖNERİ]
- **Ticari sağlayıcılar:**
  - *AMP Yazılım:* Kurumsal Hakediş ve Yaklaşık Maliyet, birimfiyat.net (web), Kolay Metraj ürünleri var. Kendi beyanına göre YFK'nin "lisanslı kullanım hakkı" her yıl AMP'ye veriliyor; YFK ve İLBANK'ın "Birim Fiyat Otomasyonu"nu da AMP geliştirmiş [K7][K23] (ikincil, satıcı beyanı).
  - *Oska Yazılım:* e-HakedişNet ürünü var; birimfiyat.com verilerinin kaynağı olarak Oska gösteriliyor [K11][K23] (ikincil).
  - Ticari sağlayıcıların veri lisansı, API'si ya da toplu dışa aktarımı olup olmadığı **doğrulanmadı**. Bu konuda sağlayıcılardan teklif istenmeli. [BELİRSİZ]
- **Pratik seçenekler [ÖNERİ]:**
  1. *Sözleşme kapsamlı veri (MVP için önerilen):* Firma yalnızca kendi sözleşme kalemlerini (poz no, tanım, birim, miktar, teklif birim fiyatı) teklif cetvelinden ya da Excel'inden yarı otomatik aktarır, kullanıcı doğrular. Resmî kataloğu çoğaltmadığı için lisans riski düşük.
  2. *Lisanslı sağlayıcı (AMP/Oska) ile veri/API anlaşması:* ücretli, bağımlılık yaratır.
  3. *Bakanlıktan yazılı izin:* süre ve sonuç belirsiz.
- Tam otomatik resmî kanal bulunmadı; içe aktarım **elle/yarı otomatik** olacak.

## 3. Yaklaşık maliyet, metraj ve keşif

- **Kimin işi?** Yaklaşık maliyeti idare hazırlar. Yapım İşleri İhaleleri Uygulama Yönetmeliği'ne (YİİUY) göre md. 9 mahal listesini, metrajı ve birim fiyat tariflerini; md. 10 fiyat kaynaklarını düzenler [K17] (ikincil). Yüklenici ise **teklif birim fiyatını ve kendi maliyet analizini** hazırlar. [ÖNERİ] ERP'de "keşif / yaklaşık maliyet" modülü firmaya **teklif hazırlık ve maliyet kontrol** aracı olarak konumlanmalı.
- **Fiyat kaynakları (YİİUY md. 10/1):** Bunlar idarenin önceki benzer sözleşmeleri, kamu birim fiyat ve rayiçleri, meslek odası ve üniversite fiyatları, deneyimli yüklenicilerin maliyetleri ve piyasa araştırmasıdır. Aralarında öncelik sırası yoktur. Piyasa araştırmasında fiyatlar KDV hariç toplanır [K17] (ikincil).
- **Güncelleme (YİİUY md. 10/5, RG 30.07.2025/32971 ile eklendi, yürürlük 01.09.2025):** Güncelliğini yitirmiş kamu fiyatı, bir katsayıyla güncellenir. Katsayının payı, yaklaşık maliyetin belirlendiği aydan önceki aya ait alt endekstir. Paydası, fiyatın yürürlüğe girdiği aydan önceki aya ait alt endekstir [K17] (ikincil).
- **Metraj cetveli:** poz, mahal, adet × boy × en × yükseklik, ara toplam; düz, profil, demir ve tesisat tipleri [K23] (ikincil). **Keşif özeti:** poz × miktar × birim fiyat, iş grubu ara toplamı, KDV hariç.
- **Özel pozlar:** resmî listede olmayan kalemler (analiz ya da piyasa fiyatı) "özel" türünde ayrı tutulmalı. [ÖNERİ]

## 4. Hakediş (YİGŞ)

> YİGŞ, YİİUY'nin eki olarak yürürlükte. Hakediş maddeleri RG 08.08.2019/30856 ve **RG 30.07.2025/32971** (yürürlük 01.09.2025) ile değiştirildi [K16] (ikincil). İlk yayım tarihi ve sayısı bu çalışmada doğrulanmadı.
> **Geçiş kuralı:** YİİUY Geçici Madde 34'e göre 2025 değişiklikleri yalnız ilanı ya da daveti **01.09.2025 ve sonrasında** yapılan ihalelere uygulanır; öncekilerde eski md. 22/39/40 geçerli [K24] (ikincil). → [ÖNERİ] ERP hakediş kurallarını **sürümlü** tutmalı, sözleşmenin ihale ilan tarihine göre uygun sürümü seçmeli. Karar 10132'nin (fiyat farkı) kendi geçiş maddesi (Geçici Madde 3) de ilan tarihindeki hükümleri esas alıyor [K13] (ikincil).

### 4.1 Türler
- **Geçici (ara) hakediş, md. 39:**
  - *Birim fiyatlı işler:* Teklif cetvelindeki ya da yeni belirlenen birim fiyatlar metraj miktarlarıyla çarpılır, kesintiler düşülür. Geçici ödeme kesin ödeme sayılmaz, kazanılmış hak da doğurmaz. İhzarat bedeli de ödenebilir.
  - *Anahtar teslimi götürü bedel (ATGB) işler:* İhale dokümanındaki **ilerleme yüzdeleri** üzerinden ödenir.
  - *Karma sözleşmeler:* Her kısım kendi türünün kuralına göre ödenir.
  - Kaynak: [K16] (ikincil).
- **Zamanlama ve ödeme (md. 39/4):** Başvuru üzerine **her ayın ilk 5 işgünü** içinde düzenlenir (başvuru yoksa idare tek taraflı düzenler). Onay **30 gün**, tahakkuk **30 gün**, ödeme **15 gün** içinde (sözleşmede farklı süre yoksa). Kaynaklar bu sürelerin dayanağında çelişiyor: biri md. 39'u, diğeri ödeme süresi için Tip Sözleşme md. 11.2'yi gösteriyor (doğrulanmadı). Yüklenici düzeltmelere itirazını en geç kesin hesap teslimine kadar dilekçeyle bildirir. Geçici kabulden sonra bir defalık "ek geçici hakediş" mümkün. [K16][K24] (ikincil)
- **Kesin hakediş (md. 40):** Kesin hesaplar geçici kabulden sonra **6 ay** içinde teslim edilir. Yüklenici **60 gün** içinde yazılı itiraz etmezse çekincesiz kabul etmiş sayılır. İdare 6 ay içinde onaylar, kesin hakediş son onaydan sonra 30 gün içinde düzenlenir. ATGB işlerde ölçüm yoktur. [K16] (ikincil)

### 4.2 Ekler ve belgeler (ERP'de üretilmesi ya da izlenmesi gerekenler)
- **Yeşil defter:** İki hakediş arasında yapılan imalat miktarlarının kaydıdır. Metrajlar yeşil defterde ve eklerinde gösterilir (md. 39/1-c) [K16] (ikincil).
- **Ataşman:** Projede bulunmayan ya da uygulamada değişen imalatların ölçü krokileri ve defteri [K16] (ikincil; tanım resmî metinden doğrulanmadı).
- **Metraj cetvelleri:** Ölçümleri yapı denetim görevlisi yükleniciyle birlikte yapar. Yüklenici ölçüme katılmazsa ölçüm tek taraflı yapılır ve itiraz hakkı düşer [K16].
- **Diğer belgeler:** Yapılan işler listesi (kümülatif ve bu dönem), hakediş özeti, hakediş raporu ya da kapağı, fiyat farkı hesap cetveli, ihzarat listesi, puantaj. Ayrıca yüklenicinin tutması gereken şantiye, sürveyan ve puantaj defterleri var [ikincil, genel uygulama].
- **Hesap akışı (md. 39/4-f):** kümülatif tutar − önceki hakediş → + KDV → − sözleşme kesintileri, borçlar, cezalar, vergiler [K16] (ikincil). [ÖNERİ] ERP her hakedişi **kümülatif** saklamalı ("önceki / bu dönem / toplam").

### 4.3 Birim fiyatlı ile ATGB farkı
| | Birim fiyat | Anahtar teslimi götürü bedel |
|---|---|---|
| Ödeme esası | Ölçülen miktar × teklif birim fiyatı | Sözleşme bedeli × iş grubu ilerleme yüzdesi |
| Veri ihtiyacı | Poz bazlı kalem, metraj, yeşil defter | İş grupları, yüzde cetveli, ilerleme tespiti |
| Fiyat farkı An | O ay gerçekleşen kalemlerin sözleşme fiyatlı tutarı | Sözleşme bedeli × o ayın ilerleme yüzdesi [K12] |
| Kesin hesap | Ayrıntılı kesin metraj | Ölçüsüz, sözleşmeye göre [K16] |

### 4.4 İş artışı, eksiliş, yeni birim fiyat
- **4735 md. 24:** Öngörülemeyen durumlarda iş artışı, ATGB işlerde sözleşme bedelinin **%10'una**, birim fiyatlı işlerde **%20'sine** kadar yapılabilir. İş sözleşme bedelinin %80'inden azına tamamlanabilecekse ayrı tasfiye ve ödeme kuralları devreye girer [K19] (ikincil; mevzuat.gov.tr'den teyit edilmeli).
- İş artışı tutarının **%6'sı** oranında ek kesin teminat alınır ve artış için ayrıca damga vergisi ödenir [K18] (ikincil).
- **Yeni birim fiyat (YİGŞ md. 22, 2025'te değişti):** Analiz sırası: aşırı düşük teklif analizleri → idarelerdeki benzer analizler → önceki sözleşmeler → puantaj. Rayiçler endeks oranıyla ihale ayına çekilir. Sözleşmede oran yoksa %10 kâr + en fazla %15 genel gider uygulanır; yeni fiyat, resmî analiz fiyatının %90'ını (benzer teklif kalemi varsa teklif/resmî oranını) geçemez. Fiyat, proje değişikliği onayından sonra 30 gün içinde belirlenir; anlaşmazlıkta YFK karar verir. [K16] (ikincil) → [ÖNERİ] "Yeni birim fiyat" ayrı kayıt türü olmalı (analiz, onay, geçici/kesin).

### 4.5 Kesintiler (yalnızca liste — vergi ve muhasebe ayrıntısı **03 numaralı dosyada**)
Kaynak: [K18] (ikincil, Temmuz 2026 tarihli makale; oranlar 03'te resmî kaynaktan doğrulanmalı).
- **Vergisel:**
  - Damga vergisi (makaleye göre binde 9,48)
  - Gelir/kurumlar vergisi stopajı, yıllara sâri işlerde (GVK md. 94; makaleye göre %5)
  - KDV tevkifatı (makaleye göre 4/10)
  - Vergi ve SGK borcu mahsubu
- **Sözleşmesel:**
  - Avans mahsubu
  - Fiyat farkı teminatı (%6)
  - İş artışı ek kesin teminatı (%6)
  - Geçici kabul / kesin hesap kesintisi (makaleye göre %3)
  - İdareye borçlar ve işçi alacakları
  - Nefaset kesintisi
- **Cezai:**
  - Gecikme cezası (sözleşmede on binde 3–6/gün aralığında belirlenir)
  - Kısmi gecikme cezası
  - Eksik giderme cezaları
  - İş programını geç sunma cezası
- Sözleşme teminatları **05.01.2026'dan beri Takasbank üzerinden elektronik** sunuluyor [K21] (ikincil). Bu değişiklik teminat takibini etkiliyor ve 03 ile koordine edilmeli.

## 5. Fiyat farkı

- **Dayanak:** "4734 sayılı Kamu İhale Kanununa Göre İhale Edilen Yapım İşlerinde Uygulanacak Fiyat Farkına İlişkin Esaslar" (BKK 2013/5217). Değişiklikler:
  - RG 24.02.2022/31760 (yürürlük 26.03.2022)
  - **Cumhurbaşkanı Kararı 10132, RG 30.07.2025/32971** (yürürlük 01.09.2025)
  - Kaynak: [K12][K13] (ikincil). YFK sitesi Esaslar metnini görev mevzuatı arasında listeliyor [K1]. Güncel metin mevzuat.gov.tr'den alınmalı.
- **Formül (md. 5):**
  - **F = An × B × (Pn − 1)**, B = 0,90
  - **Pn = a(İn/İo) + b1(Çn/Ço) + b2(Dn/Do) + b3(AYn/AYo) + b4(Yn/Yo) + b5(Kn/Ko) + b6(Gn/Go) + c(Mn/Mo)**
  - Katsayılar ihale dokümanında belirlenir, toplamları 1,00 olmalıdır ve sözleşme süresince değiştirilemez [K12] (ikincil).
  - Bazı dönemler ve işler (ör. TOKİ) için B katsayısını farklılaştıran geçici kararlar olmuştu [ikincil]. Bu yüzden B, sözleşme parametresi olarak tutulmalı.
- **Endeksler:**
  - *İ (işçilik):* TÜFE "Genel"
  - *Ç (metal dışı mineral, CPA 23 ve alt kırılımları), D (ana metal/demir-çelik, 24), Y (diğer yakıtlar, 19), K (ağaç, 16), M (makine, 28):* **Yİ-ÜFE (2003=100) CPA 2008** tabloları
  - *G (diğer):* İdarenin belirlediği endeks; belirlenmemişse Genel.
  - *AY (akaryakıt):* EPDK satış fiyatı. AYo ihale tarihindeki, AYn uygulama ayının ortalama fiyatıdır.
  - Karar 10132 ile "seçilmiş sınıflar" tablosu ve alt endeksler de kullanılabilir oldu.
  - **Temel endeks** ihale tarihinin bulunduğu aya, **güncel endeks** uygulama ayına (iş programına göre işin yapılması gereken aya) aittir.
  - Kaynak: [K12][K13] (ikincil).
- **Uygulama kuralları (md. 6, özet):** Avans mahsubu An'dan düşülür (Pn < 1 ise düşülmez). Endeks açıklanmadan düzenlenen hakedişte önceki ay endeksi kullanılıp sonra düzeltilir (2025 eki). Metraj artış/azalışı kesinleştiği ayın Pn'i ile hesaplanır. Yeni fiyatlar ve cezalı süre işleri için özel kurallar var. Negatif fiyat farkı kesilir. [K12] (ikincil)
- **2026 endeks değişikliği (yüksek risk):** TÜİK, TÜFE baz yılını Ocak 2026'dan itibaren 2025=100 yaptı. KİK **2026/DK.D-332** (30.09.2026, oybirliği) Esaslar md. 5/8'e dayanıyor: işçilik endeksi olarak TÜFE (2003=100) belirtilen yapım sözleşmelerinde 2003=100 "Genel" sütunu **yerine TÜFE (2025=100) genel endeks değerleri** esas alınır. Yani yöntem bir bağlama katsayısı değil, doğrudan yeni serinin değerleri [K14][K25] (karar metni hakedis.org kopyasından okundu; kik.gov.tr kopyası görülmedi). **[BELİRSİZ]** Karar, temel endeksin (İo) nasıl ele alınacağını ayrıca belirtmiyor; bu nokta idareye ya da KİK'e sorulmalı. Yİ-ÜFE 2003=100 serisinin 2026'da sürdüğü görünüyor (doğrulanmadı).
- **Endeks kaynakları:** TÜİK bülten ve veri portalı (tablo/Excel); TCMB EVDS web servisi (kullanıcıya özel API anahtarı, CSV/XML) [K20] (doğrulandı: resmî kılavuz). Alt endekslerin EVDS kodları ve EPDK akaryakıt verisinin makine okunur kaynağı doğrulanmadı.
- **Otomatikleştirilebilirlik [ÖNERİ]:** Formül deterministik; risk girdilerde (seri, baz değişikliği, iş programına göre uygulama ayı, gecikme, avans, idare yorumları). Endeksler önce **elle (sonra EVDS'den) bir endeks tablosuna** girilsin, her hakedişte İo/İn **dondurulmuş anlık görüntü** olarak saklansın, sonuç idare hesabıyla karşılaştırılan "kontrol hesabı" olsun.

## 6. Mevcut hakediş/keşif yazılımları ve idare sistemleri

- **Yaygın ürünler:** AMP Yazılım (Kurumsal Hakediş ve Yaklaşık Maliyet, birimfiyat.net, Kolay Metraj) ve Oska Yazılım (e-HakedişNet, birimfiyat.com) [K7][K23] (ikincil). Bağımsız bir pazar payı verisi bulunamadı. Başka ürünler araştırılmadı ve doğrulanmadı.
- **Çıktı biçimleri:** AMP metraj raporlarını Word ve Excel olarak verdiğini belirtiyor [K23] (ikincil). API ya da açık veri biçimi beyanı bulunamadı.
- **İdarenin format talebi:** Ulusal düzeyde zorunlu, standart ve elektronik bir hakediş formatı **bulunamadı**. Hakediş, YİGŞ'ye göre yapı denetim görevlisi tarafından düzenlenip imzalanan rapordur. Formatlar idareden idareye değişebilir. **(doğrulanmadı)** [BELİRSİZ]
- **EKAP:** 01.08.2025'ten beri ihale/sözleşme işlemleri ve tebligatlar EKAP'ta (Kamu Alımlarının Elektronik Ortamda Yapılmasına İlişkin Uygulama Yönetmeliği, RG 18.05.2024/32550); teminatlar Takasbank'ta elektronik [K21] (ikincil). EKAP'ta **hakediş gönderim modülü ya da yüklenici API'si bulunamadı**; KGM/DSİ/İLBANK portalları doğrulanmadı. [ÖNERİ] MVP'de "çıktı üret, elle teslim et".

## 7. ERP için sonuç

### 7.1 Veri modeli öğeleri [ÖNERİ]
- **Kurum:** YFK, KGM, İLBANK, DSİ, KTB, özel.
- **FiyatYayını:** kurum, yıl, dönem/ay, yürürlük tarihi, kaynak bağlantısı, lisans notu.
- **Poz:** kod (serbest metin), kurum, tanım, birim, tarif metni, grup; yayına göre sürümlü. Kaldırılan pozlar pasif işaretlenir. Eski↔yeni eşlemesi tutulur.
- **PozFiyat:** poz, yayın, fiyat.
- **Rayiç** ve **Analiz satırı:** poz → rayiç, miktar.
- **Kâr/genel gider oranı** ve **Rayiç–TÜİK eşlemesi.**
- **Özel poz:** firma ya da idare analizi, piyasa fiyatı.
- **Sözleşme:**
  - tür (birim fiyat / ATGB / karma), idare, ihale tarihi, **ihale ilan/davet tarihi → uygulanacak kural sürümü** (01.09.2025 öncesi/sonrası), sözleşme bedeli, süre, iş programı
  - fiyat farkı var/yok, Pn katsayıları (a, b1–b6, c), B, G endeksi tanımı
  - avans oranı, teminat oranları, gecikme cezası oranı, ödeme süreleri
- **Sözleşme kalemi:** poz kodu, tanım, birim, teklif miktarı, teklif birim fiyatı. ATGB için iş grubu ve yüzde.
- **Yeni birim fiyat:** analiz, onay, geçici/kesin durumu.
- **İş artışı/eksiliş:** %10 / %20 sınırı için uyarı, onay belgesi.
- **Metraj satırı:** kalem, mahal, boyutlar/formül, ataşman referansı, ölçüm tarihi, ölçen ve onaylayan → **Yeşil defter** kaydı.
- **Hakediş dönemi:** no, tür (ara / ek geçici / kesin), dönem, kümülatif ve dönemsel miktar/tutar, durum (taslak → imzalı → onaylı → tahakkuk → ödendi), imza/onay tarihleri.
- **Endeks değeri:** kaynak (TÜİK/EPDK), seri kodu, **baz yılı**, ay, değer, yayın/revizyon tarihi.
- **Fiyat farkı hesabı:** An, endeks anlık görüntüsü, Pn, F, avans mahsubu.
- **Kesinti satırı:** tür, oran, matrah, tutar. Parametreler 03 ile ortak yönetilir.
- Her hesaplama için **denetim izi** (kim, ne zaman, hangi parametreyle) tutulur.

### 7.2 MVP uygunluğu [ÖNERİ]
| Öğe | MVP? | Gerekçe |
|---|---|---|
| Sözleşme ve kalemlerinin Excel'den aktarımı | Evet | Lisans riski düşük, firmanın Excel'ine dayanır |
| Metraj / yeşil defter / ataşman kaydı | Evet | Temel iş akışı |
| Ara hakediş (kümülatif) + Excel/PDF çıktı | Evet | Pilot keşifte açık talep [GEREKSİNİM] |
| Parametrik kesintiler | Evet (03 ile) | Oranlar ayar olarak tutulur |
| Fiyat farkı, elle endeks girişiyle | Evet, "kontrol hesabı" olarak | Formül basit, girdi riski yüksek |
| İş artışı sınır uyarısı, yeni birim fiyat kaydı | Evet, basit hâliyle | Düşük maliyet |
| Resmî poz kataloğu (tüm YFK/KGM vb.) | Hayır | Lisans ve izin gerekli. **[GEREKSİNİM] talebiyle gerilim var:** pilot keşif poz numaraları ve resmî birim fiyatların kullanılmasını istiyor; lisans çözülene kadar yalnız sözleşme kalemleri tutulabilir |
| Analiz ve rayiç motoru, yaklaşık maliyet / teklif hazırlığı | Sonraki aşama | Veri kaynağı ve kapsam belirsiz |
| Otomatik endeks çekme (EVDS) | Sonraki aşama | API anahtarı ve seri eşleme gerekli |
| İdareye özgü resmî hakediş formatları ve entegrasyon | Sonraki aşama | Resmî kanal bulunamadı |
| Kesin hesap ve kesin hakediş | Sonraki aşama | Daha seyrek, karmaşık |

### 7.3 Yüksek riskli alanlar
- Fiyat farkında endeks serisi, baz yılı ve uygulama ayı hataları doğrudan para kaybına ya da fazla ödemeye yol açar.
- Mevzuat sık değişiyor (2022, 2025, 2026). Kuralların sabit kodlanmaması, parametre ve sürüm olarak tutulması gerekiyor.
- Resmî verinin lisans durumu belirsiz.
- ERP çıktısı resmî hakediş yerine geçmez. Resmî rapor idarenindir, ERP'nin rolü kontrol ve hazırlık olmalı.

## Açık sorular

Segment düzeyinde açık sorular:
1. Bu segmentte hangi idareler ağırlıktadır (bakanlıklar, genel müdürlükler, İLBANK, DSİ, belediyeler…) ve hangi yılların birim fiyat kitapları kullanılır?
2. Sözleşme türü dağılımı nedir (birim fiyat, anahtar teslimi götürü bedel, karma)?
3. Hakedişi kim hazırlar (yüklenici mi, idarenin kontrol mühendisi mi) ve taslak hangi biçimde teslim edilir (Excel, PDF, idare şablonu, kâğıt)?
4. AMP, Oska gibi hakediş/metraj programları ne ölçüde kullanılır; ERP bunlarla birlikte mi çalışmalı, yerine mi geçmeli?
5. Excel'lerde poz kataloğu mu tutulur, yoksa yalnızca sözleşme kalemleri mi? Rayiç ve analiz hesabı yapılır mı?
6. Fiyat farkı yüklenici tarafında ne sıklıkla hesaplanır, endeksler nereden alınır, 2026'daki TÜFE baz değişikliği hakedişleri nasıl etkiler?
7. Teklif aşamasında maliyet analizi ve teklif birim fiyatı hesabı ERP'de olmalı mı?
8. Yeşil defter, ataşman ve metraj kayıtları şantiyede kim tarafından, hangi ortamda tutulur; sahadan veri girişi gerekir mi?
9. Alt yüklenicilere hakediş aynı poz ve kalem yapısıyla mı düzenlenir?
10. Resmî poz verisi için ücretli veri sağlayıcı ya da Bakanlık izin başvurusu seçenekleri firmalar için kabul edilebilir mi?

## Açık noktalar / riskler

- **Lisans:** YFK erişim beyanı yazılım ve veri tabanında kullanımı yasaklıyor. FSEK md. 31'deki resmî metin istisnasının uygulanıp uygulanmayacağı belirsiz → hukuk görüşü gerekli.
- **2026 yayınları doğrulanamadı:** KGM, DSİ ve İLBANK'ın 2026 birim fiyatları bulunamadı. YFK aylık listelerinin Ağustos–Kasım 2026 dönemi görülmedi.
- **Fiyat farkında endeks geçişi:** KİK 2026/DK.D-332 işçilik endeksinde TÜFE 2025=100 değerlerini esas alıyor. Açık kalan nokta yalnız temel endeksin (İo) yorumu. Karar metni kik.gov.tr'den teyit edilmedi.
- **Kural sürümleri:** 01.09.2025 öncesi ve sonrası ilan edilen ihaleler farklı YİGŞ ve YİİUY hükümlerine tabi. Firmanın sözleşmeleri karışıksa iki kural seti birlikte desteklenmeli.
- **Mevzuat metinleri ikincil derleyicilerden okundu;** mevzuat.gov.tr'den teyit edilmeli. Danıştay kararları bazı 2025–2026 değişikliklerini durdurdu (ikincil); kurallar mahkeme kararlarıyla da değişebiliyor.
- **İdare formatları / e-hakediş:** ulusal elektronik kanal bulunamadı; idareye özgü sistemler araştırılmadı.
- **Ticari yazılımların** lisans/API olanakları doğrulanmadı; tek sağlayıcıya bağımlılık riski.
- **Hesap sorumluluğu:** ERP hesapları "kontrol amaçlı" etiketlenmeli; resmî tutar idarenin onayladığı hakediştir.

---

## Kaynaklar (erişim: 18.11.2026)

- [K1] YFK ana sayfa ve duyurular — https://yfk.csb.gov.tr/ (resmî)
- [K2] YFK duyurusu, 15.01.2026, 2026 rayiç/birim fiyat/analiz/TÜİK eşleştirme — https://yfk.csb.gov.tr/1-ocak-2026-tarihinden-itibaren-gecerli-2026-yili-rayic-insaat-ve-tesisat-birim-fiyatlari-ve-analizleri-ile-rayic-tuik-eslestirme-endeksleri-yayinlanmistir-duyuru-469596 (resmî)
- [K3] YFK duyurusu, 19.09.2025, aylık güncel listeler — https://yfk.csb.gov.tr/aylik-guncel-rayic-ve-birim-fiyat-listelerinin-yayinlanmasi-hakkinda-duyuru-464605 (resmî)
- [K4] YFK Birim Fiyatlar / Erişim Beyanı — https://yfk.csb.gov.tr/birim-fiyatlar-i-100468 ; https://yfk.csb.gov.tr/rayic---tuik-eslestirme-endeksleri-i-113350 (resmî)
- [K5] Temmuz 2026 inşaat birim fiyat listesi (PDF, yalnızca varlığı görüldü) — https://webdosya.csb.gov.tr/v2/yfk/2026/07/2026-Temmuz-Birim-Fiyat-Listesi-n-aat-20260703140608.pdf (resmî)
- [K6] Haziran 2026 rayiç ve mekanik listeleri (PDF) — https://webdosya.csb.gov.tr/v2/yfk/2026/06/n-aat-Rayi-ler-2026-Haziran-20260605134725.pdf ; https://webdosya.csb.gov.tr/v2/yfk/2026/06/2026-HAZ-RAN-AYI-G-NCEL-MEKAN-K-TES-SAT-F-YAT-L-STES-20260605134843.pdf (resmî)
- [K7] hakedis.org (AMP), "2026 Birim Fiyatları Yayınlandı" — https://www.hakedis.org/2026-birim-fiyatlari-yayinlandi-cevre-ve-sehircilik-bakanligi-birim-fiyatlarina-nasil-erisilir-2/ (ikincil, satıcı)
- [K8] hakedis.org, "2026 Yılı Birim Fiyatları Ne Zaman Yayınlanacak?" — https://www.hakedis.org/2026-yili-birim-fiyatlari-ne-zaman-yayinlanacak/ (ikincil)
- [K9] hakedis.org, "2026 Yılında Eklenen ve Çıkarılan Pozlar" — https://www.hakedis.org/2026-yilinda-eklenen-ve-cikarilan-pozlar-listesi/ (ikincil)
- [K10] hakedis.org, "Poz No Sistemi Değişti" (12.02.2019) — https://www.hakedis.org/poz-no-sistemi-degisiyor-yeni-poz-numaralari-geliyor (ikincil)
- [K11] birimfiyat.com (Oska verisi) poz sayfaları, ör. https://birimfiyat.com/pdf/49107 , https://birimfiyat.com/pdf/41602 , https://birimfiyat.com/pdf/2841 (ikincil; arama özetlerinden)
- [K12] Fiyat Farkı Esasları md. 4–6 — https://herpoz.com/mevzuat/yapim-islerinde-uygulanacak-fiyat-farkina-iliskin-esaslar/madde-5 (ve madde-4, madde-6) (ikincil)
- [K13] Cumhurbaşkanı Kararı 10132, RG 30.07.2025/32971 — https://www.alomaliye.com/2025/07/30/kamu-ihale-kanununa-gore-ihale-edilen-hizmet-alimlarinda-mal-alimlarinda-yapim-islerinde-uygulanacak-fiyat-farklari-karar-sayisi-10132/ (ikincil)
- [K14] hakedis.org, KİK 2026/DK.D-332 — https://www.hakedis.org/?p=8791 (ikincil)
- [K15] hakedis.org, "TÜFE 2003=100'den 2025=100'e Geçiş" — https://www.hakedis.org/tufe-2003100den-tufe-2025100e-gecis/ (ikincil)
- [K16] YİGŞ md. 22, 39, 40 — https://herpoz.com/mevzuat/yapim-isleri-genel-sartnamesi/madde-39 (ve madde-22, madde-40) (ikincil)
- [K17] YİİUY md. 9–10 — https://herpoz.com/mevzuat/yapim-isleri-ihaleleri-uygulama-yonetmeligi/madde-10 (ve madde-9) (ikincil)
- [K18] hakedis.org, "Yapım İşlerinde Hakediş Kesintileri…" (30.07.2026) — https://www.hakedis.org/yapim-islerinde-hakedis-kesintileri-ve-yuklenicilerin-diger-mali-yukumlulukleri/ (ikincil)
- [K19] hakedis.org, "İş Artış-Eksiliş Hesabı" — https://www.hakedis.org/yapim-islerinde-is-artis-eksilis-hesabi-nasil-yapilir/ (ikincil)
- [K20] TCMB EVDS Web Servis Kılavuzu — https://evds2.tcmb.gov.tr/help/videos/EVDS_Web_Service_Usage_Guide.pdf (resmî; arama özetinden)
- [K21] EKAP yönetmeliği ve e-teminat — https://www.alomaliye.com/?p=158059 ; https://www.hakedis.org/sozlesme-surecine-iliskin-tum-teminatlarin-takasbank-uzerinden-elektronik-ortamda-sunulmasi-zorunlu/ (ikincil)
- [K22] KTB 2026 hata düzeltme cetveli (dosya adı) — https://engelsiz.ktb.gov.tr/Eklenti/144906,2026-ktb-hata-d-zeltme-cetveli-20260216pdf.pdf (resmî; içerik okunmadı)
- [K24] YİİUY değişikliği, RG 30.07.2025/32971 (md. 21/25/26, Geçici Madde 34) — https://www.alomaliye.com/2025/07/30/yapim-isleri-ihaleleri-uygulama-yonetmeliginde-degisiklik-30-07-2025/ (ikincil; bağımsız R1 incelemesinde okundu)
- [K25] KİK 2026/DK.D-332 karar PDF'i (hakedis.org kopyası) — https://www.hakedis.org/wp-content/uploads/2026/10/Fiyat_fark_endeksleri_2026_DK_D_332.pdf (ikincil kopya; bağımsız R1 incelemesinde okundu)
- [K23] AMP ürünleri — https://www.ostim.org.tr/amp-yazilim-sanayi-ve-ticaret-ltd-sti/kolay-metraj-programi ; Oska e-HakedişNet — https://www.tamindir.com/indir/e-hakedisnet/ (ikincil)
