# 05 — Fiş/Fatura Belge Otomasyonu Seçenekleri

> Belge numaraları (00–13), karar numaraları (K-xx, D-xx) ve "pilot keşif" kavramı için: [ARASTIRMA-OZETI.md](../ARASTIRMA-OZETI.md#bu-belgeler-nasıl-okunur).

> Araştırma tarihi: **18 Kasım 2026**. Tüm "erişim" tarihleri bu gündür. Kod yok, teknoloji seçimi yok; seçenekler artı/eksi ile sunulur, karar kullanıcıya aittir.

## Özet

1. **[GEREKSİNİM]** Pilot keşifte fiş ve faturaların otomatik işlenmesi ihtiyacı ifade edildi. **[BELİRSİZ]** "PDF/fotoğraftan okuma" bizim varsayımımızdır; pilot keşifte teyit edilmedi. Belgelerin hangi biçimde geldiği henüz bilinmiyor.
2. **[ÖNERİ]** En ucuz ve en güvenilir yol, belge e-Fatura/e-Arşiv ise OCR'a hiç girmemek: UBL-TR XML doğrudan okunur, alanlar zaten yapılandırılmıştır. Mevzuat yönü (kâğıt faturanın bitmesi) bu yolu güçlendiriyor; ancak firmanın tedarikçi/taşeron belge karışımı ölçülmeden "çoğu e-belge" denemez.
3. Fiş (akaryakıt, market, ÖKC), taranmış PDF, kantar fişi ve kâğıt irsaliye hâlâ OCR/LLM gerektirecek. Bu belgelerin Türkçe başarımı için **kaynaklı, fiş/fatura odaklı karşılaştırma verisi bulunamadı**; pilot şart.
4. Sayfa başı maliyet hemen her seçenekte yaklaşık **1 cent veya altı** (Azure/AWS/Google ≈ 0,01 USD/sayfa; hafif LLM'ler daha ucuz). Ayda birkaç bin belgede ücret kalemi düşük; asıl maliyet geliştirme ve insan onayı emeği.
5. **Google Document AI Invoice/Expense parser ve AWS Textract AnalyzeExpense Türkçeyi resmî belgeye göre desteklemiyor** (AWS: yalnız İngilizce); Azure faturada ve termal fişte Türkçeyi listeliyor.
6. İnsan onayı vazgeçilmez: çıkarılan alanlar toplam/KDV/VKN kurallarıyla çapraz doğrulanmalı, çift kayıt kontrolü yapılmalı, her düzeltme denetim izine yazılmalı. İlk dönemde tam otomatik kabul önerilmez.
7. Belgeler yurt dışındaki bir servise gidecekse KVKK m.9 (7499 sayılı Kanun sonrası) ve veri işleme sözleşmesi konusu devreye girer; avukat teyidi gerekir.

---

## 1. Belge kaynaklarının sınıflandırılması

| Sınıf | Biçim | Çıkarım yolu | Zorluk | Durum |
|---|---|---|---|---|
| (a) e-Fatura / e-Arşiv | UBL-TR XML (+ görsel PDF) | XML ayrıştırma, OCR yok | Düşük | **[ÖNERİ]** ilk öncelik |
| (b1) Metin katmanlı PDF | Dijital PDF | PDF metin çıkarımı + kurallar/LLM | Düşük-orta | **[ÖNERİ]** |
| (b2) Taranmış PDF | Görüntü PDF | OCR/belge zekâsı/LLM | Orta | **[BELİRSİZ]** oranı bilinmiyor |
| (c) Kâğıt fiş/fotoğraf | JPEG/HEIC | OCR/LLM; fotoğraf kalitesine bağlı | Yüksek | **[BELİRSİZ]** müşteri teyidi yok |
| (d) İrsaliye, kantar fişi | Kâğıt/fotoğraf, bazen e-İrsaliye | Biçim firmaya özgü; e-İrsaliye ise XML | Çok yüksek (kâğıt) | **[BELİRSİZ]** |

### (a) e-Fatura / e-Arşiv
- e-Fatura, mali mühürlü **UBL-TR XML**'dir ve GİB merkezi platformu üzerinden gider (ikincil: [ecosio](https://ecosio.com/en/compliance/turkiye/e-invoicing/), [lookuptax](https://lookuptax.com/docs/einvoicing/e-fatura-e-arsiv-einvoicing-turkey); erişim 18.11.2026). Şema sürümü kaynaklarda 1.2.1/2.1 diye farklı geçiyor **(doğrulanmadı)**; güncel UBL-TR paketi GİB'den alınmalı.
- **Gelen faturayı çekme:** GİB portalından görüntüleme/kabul-red/XML indirme mümkün; ERP'ye otomatik çekmenin pratik yolu **özel entegratörün** gelen kutusu servisi (ikincil: [Logo belgesi](https://docs.logo.com.tr/download/attachments/50680068/Support_E-Fatura.pdf?api=v2), [Faturaport](https://faturaport.com/blog/e-fatura/gib-e-fatura-e-arsiv-ve-ubl-tr-paketlerini-guncelledi)). Belirli bir entegratörün gelen-fatura API'sini ve ücretini **doğrulayamadım**. **[BELİRSİZ]**
- **Karekod (QR):** GİB Karekod Standardı Kılavuzu (V1.1) kapsamında e-Fatura, e-Arşiv, e-İrsaliye dahil 8 belge türünde zorunlu; içerik JSON'dur: gönderen/alıcı VKN-TCKN, senaryo, tip, tarih, fatura no, ETTN, para birimi, mal/hizmet tutarı, KDV matrahı, hesaplanan KDV, vergi dahil ve ödenecek tutar (ikincil: [BirFatura](https://birfatura.com/e-belgede-karekod-zorunlu-mu/), [Sovos](https://sovos.com/tr/blog/kdv/e-belgelerde-karekod-zorunlulugu/); **resmî kılavuz metni okunamadı**, alan adları doğrulanmadı). **[ÖNERİ]** Karekod, fotoğrafı çekilmiş/taranmış e-Arşiv faturada toplam alanlarını **OCR'sız** okumaya ve OCR çıktısını çapraz doğrulamaya yarar; ancak satır kalemi içermez.
- **Zorunluluk (olgusal, ikincil):** Bilanço esasında defter tutanlar için kâğıt fatura **1.1.2026'da fiilen bitti**; basit usul ve işletme hesabı esaslı mükellefler için tam zorunluluk **1.1.2027** ([Tebliğ 589, RG 31.12.2025/33124 5. mükerrer — alomaliye özeti](https://www.alomaliye.com/2025/12/31/vergi-usul-kanunu-genel-tebligi-sira-no-589/); [Sovos](https://sovos.com/tr/blog/kdv/2026-e-fatura-zorunlulugu-ve-gecis-rehberi/)). e-Fatura geçiş eşiği 3 milyon TL brüt satış hasılatı; inşaat/imalat/alım-satım/kiralama için 500 bin TL (Sovos; ikincil, resmî metinle teyit edilmeli).
- **Oran sorusu — cevap: kısmi.** Mükellef sayısı: e-Fatura 1.565.603 (2024) → 1.937.308 (2025), +%23,7 (AA/GİB verisi, [Memurlar.net, 30.3.2026](https://www.memurlar.net/haber/1163301/kagit-fatura-tarih-oluyor-e-fatura-kullanici-sayisi-2-milyona-yaklasti.html); ikincil). Aynı haberde e-Arşiv 2025 değeri de aynı sayı çıkıyor, olası hata **(doğrulanmadı)**. Belge adedi için yılı belirtilmemiş bir tablo (e-Arşiv ≈ 10,7 milyar, e-Fatura ≈ 1,03 milyar; [Ekonomi Gazetesi köşe yazısı](https://www.ekonomigazetesi.com/kose-yazisi/kagit-fatura-tarih-olacakti-simdilik-olmadi-69094)) bulundu; yıl ve güvenilirlik **doğrulanmadı**. **Toplam faturalar içindeki e-belge payına dair kaynak bulunamadı.**
- **[ÖNERİ] Yorum:** Mevzuat yönü e-belgeye doğru; bu, "önce e-belgeyi doğrudan al" yaklaşımının mantıklı olduğunu gösteriyor. Ama bizim konumuz *gelen* belgeler: tedarikçi büyükse e-belge gelir; küçük esnaf/taşeron (basit usul) 2026 sonuna kadar kâğıt kesebilir, ÖKC fişleri ve şantiye irsaliyeleri zaten e-fatura değildir. Oran **ancak firmanın kendi belgelerinin örneklenmesiyle** bilinir.

### (c) Fiş / ÖKC
- Yazar kasa/ÖKC fişi fatura yerine geçmez; gider yazımında sorun çıkabildiğine dair ikincil kaynaklar var ([Andersen](https://tr.andersen.com/tr/images/pdf/and_27-yn-okc-ile-e-belgeler-duzenlenebilecektir.pdf)). Fişin KDV indirimi/gider olarak kabulü için **net kaynak bulamadım** → mali müşavire sorulmalı. **[BELİRSİZ]**
- Yeni nesil ÖKC'lerde e-belge düzenlenmesi yönünde değişiklik var (Tebliğ 593, [PwC bülteni 2026/13](https://www.pwc.com.tr/tr/hizmetlerimiz/vergi/dolayli-vergi/bultenler/e-donusum-bultenleri/2026/vergi-usul-kanunu-genel-tebligi-sira-no-593-resmi-gazetede-yayimlandi.html)); teknik kılavuz **16.12.2025 tarihli taslak** ([GİB YN ÖKC](https://ynokc.gib.gov.tr/UploadedFiles/Files/yn-okc-fis-ve-e-belge-formatlari-kilavuz_taslak_16122025.pdf)). Yayımlanan son hâli doğrulanmadı. Akaryakıt ÖKC fişlerinde karekod uygulandığı bildiriliyor (ikincil, İSMMMO'ya atfedilen haber); genel ÖKC fişlerinde karekod yok.

### (d) İrsaliye / kantar
- e-İrsaliye XML'dir ve karekodludur. İnşaat Demiri İzleme Sistemi kapsamındaki ve brüt satışı 1 milyon TL ve üzeri mükelleflere e-İrsaliye zorunluluğu (1.7.2026) bildiriliyor ([BirFatura](https://birfatura.com/kimlere-e-irsaliye-zorunlulugu-getirildi/); ikincil, doğrulanmadı) — bu tedarikçi tarafını etkiler, firmanın sahadaki kantar fişleri hâlâ kâğıt olabilir.
- Kâğıt irsaliye/kantar fişi: nokta vuruşlu, el yazılı, firmaya özgü; **bu belge sınıfında hazır model başarımı için kaynak bulunamadı**. **[ÖNERİ]** İlk aşamada kapsam dışı bırakıp elle giriş formu + fotoğraf eki.

---

## 2. Teknik seçenekler

Fiyatlar liste fiyatıdır, vergi hariç, USD; erişim 18.11.2026.

| Seçenek | Türkçe | Sayfa başı maliyet | Not |
|---|---|---|---|
| **Azure AI Document Intelligence** (prebuilt-invoice, prebuilt-receipt) | Fatura: `tr`/TRY **listeli**; termal fiş: Türkçe **listeli** ([MS Learn, güncelleme 19.10.2026](https://learn.microsoft.com/en-us/azure/ai-services/document-intelligence/language-support/prebuilt)) (doğrulandı: resmî kaynak) | Prebuilt **10 USD/1000 sayfa**; Read 1,5; özel model 30 (Azure Retail Prices API, westeurope, [prices.azure.com](https://prices.azure.com/api/retail/prices); fiyat sayfasının arayüzünde değerler "$-" görünüyor) | PDF/görüntü; alan güven skoru var; Türkiye bölgesi yok (fiyat sayfası bölge listesi). Satır kalemi çıkarımı var |
| **Google Document AI** (Invoice/Expense parser) | **Türkçe listede yok** (Invoice: DE, EN, ES, ET, FR, IT, LV, LT, NL, PT, RO, SV; [resmî işlemci listesi](https://docs.cloud.google.com/document-ai/docs/processors-list)) (doğrulandı: resmî kaynak) | Invoice parser 0,10 USD / 10 sayfa ([resmî fiyat sayfası alıntısı, arama özetinden; sayfa tam okunamadı](https://cloud.google.com/document-ai/pricing)) (ikincil) | AB ve ABD bölgesi var. Türkçe fatura için riskli; Form parser/özel model seçeneği ayrı |
| **AWS Textract** (AnalyzeExpense) | Yalnızca metin algılama ve Table/Layout analizi tüm dilleri destekliyor; Forms EN/ES/IT/PT/FR/DE ile sınırlı; belgede "All other APIs are limited to English" deniyor → **AnalyzeExpense: yalnız İngilizce**. Algılanan karakter listesinde ğ, ş, ı, İ da yok ([AWS](https://docs.aws.amazon.com/textract/latest/dg/limits-document.html)) (doğrulandı: resmî kaynak) | AnalyzeExpense **0,01 USD/sayfa** (ilk 1M), 0,008 sonrası; DetectDocumentText 0,0015 ([AWS fiyat](https://aws.amazon.com/textract/pricing/), us-west-2 örneği) (doğrulandı: resmî kaynak) | **[ÖNERİ]** Türkçe fiş/fatura için aday dışı bırakılması önerilir (yalnız ham metin algılama kullanılabilir, alan çıkarımı için değil) |
| **Çok kipli LLM** (Claude, Gemini, GPT) | Çok dilli; Türkçe fiş/fatura başarımı için **kaynaklı karşılaştırma bulunamadı** | Claude Sonnet 5.5: 2 / 10 USD (giriş/çıkış, MTok); Haiku 5.5: 0,10 / 0,50 (≤100K istem); Claude PDF sayfası ≈ 1.500–3.000 token ([Anthropic fiyat](https://platform.claude.com/docs/en/about-claude/pricing), [PDF desteği](https://platform.claude.com/docs/en/build-with-claude/pdf-support)). Gemini 3.5 Flash-Lite 0,30 / 2,50; Gemini 3.6/3.8 Flash 0,75 / 3,75 (31.12.2026'ya kadar), sonra 1,50 / 7,50; toplu işlem %50 indirim ([Gemini fiyat](https://aistudio.google.com/docs/pricing)) (doğrulandı: resmî kaynak). GPT fiyatı bu araştırmada doğrulanmadı | Esnek şema (JSON), satır kalemi, el yazısı toleransı; **güven skoru yok**, rakam "uydurma" riski → zorunlu kural doğrulaması. Model/fiyat hızlı değişiyor |
| **Açık kaynak OCR** (Tesseract, PaddleOCR) | PaddleOCR, Türkçe belge karşılaştırması OCRTurk'te (Şubat 2026) en iyi genel sonuçlardan; belgeler akademik makale/tez/slayt, **fiş değil** ([arXiv 2602.03693](https://arxiv.org/abs/2602.03693)) (ikincil). Tesseract'ın Türkçe fiş başarımı için veri bulunamadı | Lisans ücreti yok; sunucu + bakım emeği | Veri yurt dışına çıkmaz (KVKK avantajı). OCR yalnızca metin verir; alan eşleme/doğrulama katmanı bizim yazmamız gerekir |
| **Türkiye'deki hazır ürünler** | Paraşüt "AI OCR ile fiş ekle" (telefon kamerası, tutar/tarih/işletme çıkarımı) ([Paraşüt kılavuzu](https://www.parasut.com/kullanim-kilavuzu/parasut-ai-ocr-fis-okutma-nasil-yapilir)) **(üretici iddiası)** | Doğrulanmadı | Kapalı ürün; ERP'mize gömülemez. Kolaysoft/Mikro/Logo için fiş/fatura OCR bilgisi bulunamadı **(doğrulanmadı)**. Entegratör ürünleri **[BELİRSİZ]** |

**Gecikme:** Kaynaklı ölçüm bulamadım; bulut belge servisleri ve LLM'ler tipik olarak saniye düzeyinde tek sayfa döndürür **(doğrulanmadı)**; kullanıcı beklemeden arka planda işlenip kuyruğa düşecek tasarım ("yükle, sonra kuyruktan onayla") gecikme sorununu ortadan kaldırır. **[ÖNERİ]**

**[ÖNERİ] Seçenek yorumu (karar kullanıcıda):** Google Invoice/Expense ve AWS AnalyzeExpense Türkçe desteği olmadığı için aday dışı; Azure (belgeli Türkçe + güven skoru) ve bir çok kipli LLM'i aynı örnek sette yarıştırmak; kurallı doğrulama katmanı her iki durumda da bizim olacağından sağlayıcı değiştirilebilir (soyutlama) kurgulanmalı. PaddleOCR yalnızca veri yurt dışına çıkmasın isteniyorsa alternatif.

---

## 3. İnsan onayı akışı

**[ÖNERİ]** — aşağıdakiler araştırmaya dayalı tasarım önerisidir, müşteri onayı yoktur.

1. **Kaynağa göre hat:** e-Fatura XML → alanlar kesin sayılır, yalnızca eşleştirme (tedarikçi, proje) onaylanır. PDF/fotoğraf → çıkarılan her alan öneri sayılır.
2. **Doğrulama kuralları (otomatik):**
   - VKN 10 hane / TCKN 11 hane ve sağlama algoritması; tedarikçi daha önce kayıtlıysa unvan eşleşmesi.
   - Matrah + KDV = vergi dahil toplam; satır toplamları = belge toplamı; KDV oranı geçerli oranlar kümesinde (güncel oranlar mevzuattan alınmalı, kodda sabitlenmemeli).
   - Tarih makul aralıkta (gelecek tarih, çok eski tarih uyarısı).
   - Karekod varsa OCR toplamları karekodla karşılaştırılır; uyuşmazlık = zorunlu inceleme.
   - **Not (kaynak):** 1.4.2026'dan itibaren KDV oranının mükellefin NACE koduyla uyumu zorunluluğu bildiriliyor ([Müşavirler Kulübü](https://musavirlerkulubu.com.tr/tema-demo/katip/yazilar/nace-kodu-kdv-orani-uyum-zorunlulugu-1-nisan-2026); ikincil, doğrulanmadı); gelen belge doğrulamasında ilgili olabilir.
3. **Üç bantlı kuyruk:** (i) tüm kurallar geçti + yüksek güven → "hızlı onay" (tek tıkla); (ii) kural geçti, güven düşük → "inceleme"; (iii) kural başarısız → "düzeltme". **Eşik değerleri pilot ölçümden çıkar**, şimdiden rakam verilmez. İlk dönemde (i) bandı da insan onayından geçer; **tam otomatik kabul ancak pilotta "otomatik kabul edilen yanlış" oranı kabul edilebilir bulunursa** düşünülmeli.
4. **Çift kayıt tespiti:** e-belgede ETTN (UUID) benzersiz anahtar; diğerlerinde (tedarikçi VKN, belge no, tarih, toplam) birleşik anahtar; fişte (işyeri, tarih-saat, fiş/Z no, tutar) + dosya özeti (hash). Aynı belgenin PDF ve XML hâli ile bulut/mobil çift yüklemesi de yakalanmalı.
5. **Proje/maliyet merkezi atama önerisi:** tedarikçi→geçmiş proje/kalem eşlemesi, yükleyen kişinin atandığı şantiye, akaryakıt fişinde araç/ekipman; sistem *öneri* sunar, onaylayan seçer.
6. **Onay ve denetim izi:** yükleyen ≠ onaylayan ilkesi (tutar eşiğine bağlı; müşteriyle netleşecek). Kayıt: orijinal dosya (değişmez, hash'li), ham çıkarım çıktısı, alan bazında eski/yeni değer, kim/ne zaman/hangi sürüm model, onay/red nedeni. Bu iz ayrıca pilot doğruluk ölçümünün veri kaynağı olur.
7. Çıktı resmî muhasebe fişi değil **gider/alım kaydı taslağı**dır; muhasebe kapsamı pilot keşifte bilerek açık tutuldu **[BELİRSİZ]**.

---

## 4. Veri güvenliği ve KVKK

- **Yurt dışı aktarım:** 7499 sayılı Kanun ile KVKK m.9 değişti (1.6.2024); açık rıza artık ana dayanak değil, sıra: yeterlilik kararı → uygun güvenceler (standart sözleşme, bağlayıcı şirket kuralları). Standart sözleşmeler imzadan sonra **5 iş günü içinde Kurum'a bildirilmeli** ([KVKK duyurusu](https://www.kvkk.gov.tr/Icerik/8043/Standart-Sozlesme-Bildirim-Modulu-Hakkinda-Kamuoyu-Duyurusu) başlığı; ayrıntı hukuk büroları özetinden: [Erdem & Erdem](https://www.erdem-erdem.av.tr/bilgi-bankasi/standart-sozlesme-bildirim-modulu-hakkinda-kamuoyu-duyurusu), [alomaliye](https://www.alomaliye.com/2024/10/30/kvkk-standart-sozlesme-bildirim-modulu/)) (ikincil; resmî metin tam okunamadı). Güncel değişiklik olup olmadığı **doğrulanmadı** (bir kaynak 2026'da yeni değişiklikten söz ediyor).
- **Belgelerde kişisel veri:** şahıs işletmesi unvanı/TCKN, plaka, kart son haneleri, şantiye fotoğrafında kişiler. Tüzel kişi VKN'si tek başına kişisel veri değildir **(hukukçu teyidi gerekir)**.
- **Bölge:** Azure/Google belge servisi için AB bölgesi mevcut; Türkiye bölgesi yok (Azure fiyat sayfası bölge listesi; Google Invoice parser bölgeleri: AB/ABD/Asya/Avustralya/Kanada). AB bölgesi de Türkiye açısından "yurt dışı"dır. **[ÖNERİ]** Karar sırası: kişisel veri içermeyen belgeleri ayıklama/maskeleme mümkün mü → değilse işleyen sözleşmesi + standart sözleşme → olmuyorsa kendi sunucusunda OCR (PaddleOCR).
- **Sağlayıcı beyanları (üretici iddiası):** Gemini ücretli katmanında veri ürün iyileştirmede kullanılmaz ([Gemini fiyat sayfası](https://aistudio.google.com/docs/pricing)); Anthropic PDF özelliği sıfır veri saklama (ZDR) için uygun işaretli, "Covered Models" hariç ([Anthropic](https://platform.claude.com/docs/en/build-with-claude/pdf-support)). Sözleşmesel doğrulama gerekir.
- **Saklama:** İki süre çelişki değil, **birlikte (kümülatif) uygulanır**: VUK m.253'e göre vergi açısından 5 yıl, TTK m.82'ye göre tacirler için 10 yıl; ticaret şirketleri için pratikte **uzun olan 10 yıl esas alınır** (ikincil: [TÜRMOB](https://www.turmob.org.tr/BasinOdasi/BasinArsiv/Detay/9682a497-ca2e-487e-abb6-fe3440cdfa69/vuk-a-gore-defter-ve-belgelerin-saklanma-sureleri-ve-ozellikli-durumlar), [FFK Hukuk](https://www.ffkpartnerhukuk.com.tr/ticari-belgelerin-saklama-suresi-ne-kadardir-2026-guncel-rehber-ticari-defter-ve-belgelerin-saklama-yukumlulugu/), bağımsız inceleme R2 teyidi; VUK süresi belgenin ait olduğu yılı izleyen yıldan başlar; mali müşavir teyidi önerilir). Pilot keşifteki–10 yıl okunabilirlik hedefi [GEREKSİNİM] ile uyumlu. **Fotoğraf/tarama kopyasının ispat değeri (kâğıt aslı atılabilir mi) için net kaynak bulunamadı** → **[BELİRSİZ]**, mali müşavire sorulmalı; teyit edilene kadar kâğıt asıl saklanmalı varsayılmalı.

---

## 5. Önerilen aşamalandırma

**[ÖNERİ]** (müşteri onayı yok)

| Aşama | İçerik | Bağımlılık |
|---|---|---|
| **0 — Keşif** | Pilot firmadan 1–2 aylık gerçek belge örneği (≈150–300, tüm sınıflar); biçim dağılımı sayımı | Müşteri |
| **1 — MVP** | Belge yükleme + dosya deposu; **hızlı elle giriş formu** (tedarikçi VKN→otomatik doldur, KDV/toplam hesap kontrolü, çift kayıt uyarısı); **e-Fatura XML içe aktarma** (önce manuel yükleme; sonra entegratör/portal); karekod okuma; onay + denetim izi | e-belge payı yüksekse en çok değer burada |
| **2 — PDF/fotoğraf okuma** | Seçilen servis/LLM ile çıkarım → doğrulama kuralları → inceleme kuyruğu | Pilot sonuçları, KVKK kararı |
| **3 — Akıllı atama/otomasyon** | Proje/kalem önerisi öğrenme, güvenli bantta hızlı onay | Yeterli onaylı geçmiş veri |

**Maliyet tahmini (yalnızca çıkarım ücreti, 1 belge = 1 sayfa varsayımı; çok sayfalı belgede orantılı artar; entegratör ücreti dahil değil, bilinmiyor):**

| Hacim/ay | Azure/AWS/Google (~0,01 USD/sayfa) | Claude Sonnet 5.5 (≈0,009 USD/sayfa*) | Hafif LLM (Haiku 5.5 / Flash-Lite, ≈0,0005–0,002 USD*) |
|---|---|---|---|
| 300 | ≈ 3 USD | ≈ 3 USD | < 1 USD |
| 1.000 | ≈ 10 USD | ≈ 9 USD | ≈ 0,5–2 USD |
| 3.000 | ≈ 30 USD | ≈ 27 USD | ≈ 1,5–6 USD |

\*Hesap bizim varsayımımız: ≈2.000 giriş + 500 çıkış token/sayfa (Anthropic: sayfa başı 1.500–3.000 token). Gerçek görüntü token'ı model ve çözünürlüğe göre değişir; yanlış çıkabilir.

**Sonuç:** Çıkarım ücreti, yazılım geliştirme ve insan onay süresine kıyasla küçük kalem; seçimde belirleyici olan **doğruluk ve KVKK**, maliyet değil. **[ÖNERİ]**

**Doğruluk ölçümü (pilot):**
1. Aynı örnek setin (en az 150–300 belge; sınıf başına yeterli sayıda) elle "altın" etiketini çıkar (iki kişi, uyuşmazlık çözümü).
2. 2–3 yaklaşımı (ör. Azure prebuilt, bir LLM, PaddleOCR + kurallar) aynı sette yan yana çalıştır.
3. Ölç: alan bazlı tam eşleşme (VKN, tarih, belge no, toplam, KDV matrahı/oranı, satır kalemi); belge düzeyinde "hiç düzeltme gerekmedi" oranı; **en kritik metrik: sistemin güvenle kabul ettiği ama yanlış olan alan oranı**; belge başı düzeltme süresi.
4. Sonuçları belge sınıfına (e-PDF, tarama, ÖKC, akaryakıt, kantar) ve fotoğraf kalitesine göre kırıp raporla. Kabul eşikleri pilot verisiyle müşteriyle birlikte belirlenir.

---

## Açık sorular

Segment düzeyinde açık sorular:
1. Bu ölçekteki firmalarda ayda kaç fatura/fiş/irsaliye işlenir (yoğun ay dahil)? Bir belgede ortalama kaç sayfa/kalem vardır?
2. Gelen belgelerin dağılımı nedir: e-Fatura, e-Arşiv (e-posta PDF), kâğıt fatura, ÖKC/akaryakıt fişi, irsaliye/kantar, el yazılı? Yaklaşık yüzdeler.
3. Gelen e-Faturalar nereye düşer (mali müşavir mi, firma mı)? Hangi entegratör/portal kullanılır?
4. Belgeler mali müşavire nasıl teslim edilir, giderler nasıl kaydedilir?
5. Şantiyeden belgeyi kim, hangi kanaldan (telefon/mesajlaşma/e-posta) iletir? İnternet kapsama sorunu var mı?
6. Çıkarılan bilgiyi kim kontrol edip onaylar; tutar eşiğine göre farklı onaylayıcı gerekir mi? Yükleyen kişi onaylayabilir mi?
7. Fiş ve faturalar hangi proje/maliyet merkezine nasıl atanır? Ortak giderler (genel merkez, araç) nasıl dağıtılır?
8. Taşeron ve küçük tedarikçilerden kâğıt belge/kantar fişi/irsaliye oranı nedir? Kâğıt asıl nerede ve ne kadar süre saklanır?
9. Belgelerin yurt dışındaki bir bulut servisine gönderilmesinde kurumsal ya da ihale sözleşmesinden gelen kısıtlar var mı?
10. Pilot doğruluk ölçümü için anonimleştirilebilir örnek belge seti nasıl sağlanır?
11. "Otomatik işleme" ile asıl beklenti elle yazmayı azaltmak mı, doğrudan muhasebe kaydı üretmek mi, denetim/doğruluk mu? (PDF/fotoğraf okuma varsayımının teyidi.)

## Açık noktalar / riskler

- **[BELİRSİZ]** Beklenti PDF/fotoğraf okuma mı, yoksa yalnızca "elle girişin azaltılması" mı — bu belgede varsayım olarak korunuyor.
- **[BELİRSİZ]** Gelen e-belge payı kaynaklı olarak ölçülemedi; mükellef sayıları var, fatura adedi/payı verisi yok veya yılı belirsiz. Tek bir rakama dayanarak e-belge yolunu "yeterli" saymak risklidir.
- **[BELİRSİZ]** Entegratör gelen-fatura API'si, ücreti ve sözleşme koşulları doğrulanmadı; mali müşavir/entegratör erişim yetkisi gerekebilir.
- Türkçe fiş/fatura başarımı: Azure belgesi dil desteği sunuyor ama başarım oranı vermiyor; LLM ve açık kaynak için fiş odaklı kaynak yok. Üretici iddialarına güvenilemez; pilot şart.
- AWS AnalyzeExpense yalnız İngilizce, Google Invoice/Expense Türkçeyi desteklemiyor (ikisi de resmî belgeye göre); aday listesinde Azure, LLM ve açık kaynak kalıyor.
- İnşaat için 500 bin TL e-Fatura eşiği ve e-İrsaliye (1.7.2026) zorunluluğu resmî metinden kontrol edilmedi (ikincil kaynak); Gemini fiyatları ve entegratör gelen-fatura API'leri de doğrulanmadı.
- LLM çıkarımı güven skoru vermez ve rakam hatası üretebilir; doğrulama kuralları ve insan onayı olmadan "otomatik kabul" yapılmamalı.
- KVKK: yurt dışı aktarım yükümlülükleri (standart sözleşme, 5 iş günü bildirim) hukuk bürosu özetlerine dayanıyor; resmî metinler ve güncel değişiklikler avukata teyit ettirilmeli. Ceza tutarı bir hukuk bürosundan (doğrulanmadı), burada kullanılmadı.
- Fiş/fotoğraf kopyasının VUK açısından ispat değeri ve kâğıt asıl saklama zorunluluğu net kaynakla doğrulanamadı. Saklama süresi: VUK 5 + TTK 10 yıl birlikte uygulanır, 10 yıl esas (mali müşavir teyidi).
- Fiyatlar ve model adları hızlı değişiyor (ör. Gemini 3.x Flash fiyatı 1.1.2027'de artıyor; bazı eski modeller 1.12.2026'da yönlendirilecek); karar öncesi yeniden doğrulanmalı. Azure fiyatı resmî API'den alındı ama fiyat sayfası arayüzünde görünmedi.
- Bu araştırmadaki web sayfalarının çoğu özetleyici araçla okundu; hassas alanlar (karekod alan adları, tarih/eşikler) resmî GİB metinleriyle ayrıca teyit edilmeli.
- Yeni nesil ÖKC e-belge kılavuzu taslak (16.12.2025); fiş dünyası 2026–2027'de değişebilir, bu da fiş OCR ihtiyacını azaltabilir.
