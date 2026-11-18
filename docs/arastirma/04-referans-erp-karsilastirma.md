# 04 — Referans ERP Karşılaştırması ve Sade Arayüz Önerileri

> Belge numaraları (00–13), karar numaraları (K-xx, D-xx) ve "pilot keşif" kavramı için: [ARASTIRMA-OZETI.md](../ARASTIRMA-OZETI.md#bu-belgeler-nasıl-okunur).

Hazırlayan: Araştırma agent'ı D · Tarih: 18 Kasım 2026 · Durum: taslak, müşteri onayı yok.
Kaynak kodları (Ü1, D1, B1 vb.) dosyanın sonundaki "Kaynaklar" bölümündedir; tüm erişim tarihi 18.11.2026. Doğrulama gösterimi: **(R)** resmî kaynak, **(İ)** ikincil/bağımsız, **(Ü)** üretici iddiası, **(?)** doğrulanmadı.

## Özet

1. **[ÖNERİ]** İncelenen yerli ERP'lerden CANIAS'ın inşaat sayfası bütünleşik proje–maliyet–hakediş–taşeron veri yapısını vaat ediyor (Ü1) ama mobil, fiyat ve dağıtım bilgisi vermiyor; bağımsız kanıt yok. **[BELİRSİZ]** Hedef kullanıcıların hangi ekranları ve akışları beğendiği (varsa referans aldığı ürünlerde) bilinmiyor; arayüz hedefi bunu öğrenmeden somutlaşmaz.
2. **[ÖNERİ]** Yabancı inşaat ürünlerinin hiçbirinde Türkiye kamu birim fiyat/poz kataloğu doğrulanamadı; poz–hakediş bu projede fark yaratacak alan. Türkiye'deki poz/hakediş araçları ayrı ürünler (AMP, e-HakedişNet; 70.000+ poz, Ü/İ).
3. **[ÖNERİ]** SAP S/4HANA PS güçlü ama küçük ekipler için aşırı karmaşık; SAP Business One KOBİ'ye uygun ama inşaat proje yönetimi "temel" seviyede ve inşaat özellikleri ek lisans/eklenti gerektirebilir (İ).
4. **[ÖNERİ]** İncelenen iki açık kaynak ERP arasında yalnızca Odoo'nun Türkiye yerelleştirmesi resmî kaynakla doğrulandı (7/A hesap planı; Nilvera ile e-Fatura/e-Arşiv/e-İrsaliye modülleri Community'de, LGPL-3; e-Defter'in Community'de olduğu doğrulanmadı, Enterprise gerekebilir; hepsi ücretli Nilvera hesabı gerektirir) (R, D1, D5). ERPNext için resmî Türkiye yerelleştirmesi bulunamadı.
5. **[ÖNERİ]** Açık kaynak ERP'yi temel almak sıfırdan geliştirmeye gerçek bir alternatif; ama hakediş/ilerleme faturası, poz kataloğu ve kamu işi mantığı her iki yolda da özel geliştirme gerektirir. Karar kullanıcıda; önerilen: karar öncesi kısa bir kavram kanıtı (bkz. §3.4).
6. **[ÖNERİ]** Sade arayüz için 8 ilke çıkarıldı (§5): rol bazlı ana sayfa, proje merkezli gezinme, Excel benzeri tablo, hızlı giriş, mobil saha, toplu içe aktarma, Türkçe terminoloji, ilerleme rehberliği.
7. Fiyatların çoğu teklif bazlı; bulunan rakamlar toplayıcı sitelerden ve tutarsız (?).

---

## 1. CANIAS ERP

**Ürün.** Üretici IAS; Java tabanlı, üç katmanlı, TROIA dili ile geliştirilmiş; v6.01'den beri tam web destekli (Ü/İ: canias.com, Gartner yorumu) (B1). Dağıtım: şirket içi/bulut/hibrit (listeleme sitesi, ?).

**Modüller (Ü2).** Satış, CRM, finans (muhasebe, kredi/leasing, banka entegrasyonu, bütçe yönetimi), proje ve doküman yönetimi, e-dönüşüm grubu (e-Fatura, e-Defter), iş süreci yönetimi (BPM), geliştirme araçları. Resmî modül sayfasında e-Fatura ve e-Defter "ETR – E-Dönüşüm" altında ayrı listeleniyor (Ü). **[ÖNERİ]** Türkiye yerelleştirmesi var görünüyor ama kapsamı ve işleyişi (özel entegratör mü, doğrudan mı) doğrulanmadı (?).

**İnşaata özgü (Ü1).** Proje bazlı bütçe/maliyet yapısı; metraj/keşif listesinin (BOQ) satın alma, hakediş ve gider kayıtlarıyla bağlanması, planlanan–gerçekleşen sapma uyarısı; taşeron süreçleri (ayrıntısız); şantiye harcama/işçilik/ilerleme verisinin merkeze akışı; insan, ekipman, malzeme kaynak planlaması. Sayfada mobil/çevrimdışı saha erişimi, fiyat, dağıtım bilgisi **yok**. Proje modülünde Gantt, bağımlılık, zaman takibi, proje muhasebesi ve nakit akışı anılıyor (Ü3).

**Kullanıcı görüşü (İ, B1).** Bağımsız yorum sitelerinde (Capterra, TrustRadius) bu ürün için kullanıcı yorumları var; sayfalar doğrudan okunamadı, arama özetlerine göre puan 4,4/5 ve yorumlar karışık. Tek tek yorumlar temsil gücü sınırlı olduğu için burada alıntılanmamıştır.

**Fiyat.** Yayınlanmış fiyat yok (teklif bazlı); lisans modeli ve bakım ücreti doğrulanmadı (?).

**Açık soru (tam liste aşağıdaki "Açık sorular" bölümünde):** referans üründe hangi ekranlar beğeniliyor, ürün hangi modülle görüldü? **[BELİRSİZ]**

## 2. SAP

### 2.1 S/4HANA — Project System (PS)
- WBS elemanlarında maliyet toplama, kilometre taşı faturalama, bitişte duran varlığa (AuC) mahsup; SAP kendi eğitim içeriğinde kilometre taşı faturalamanın inşaat projelerinde yaygın olduğunu söylüyor (R, D4).
- Faturalama için önkoşullar zincirleme: faturalanabilir WBS, satış siparişi kalemi, kilometre taşı, faturalama planı (R, D4). Bir SAP destek notu, faturalama vade tarihi girilmeyen WBS'in 0 gelir planladığını anlatıyor — küçük bir ihmalin sessizce yanlış sonuç doğurduğu örnek (R, D4).
- Ağırlıklı kullanıcı: mühendislik/inşaat/EPC, büyük kurumsal (İ, D4).
- İnşaat ilerleme faturası (retention vb.) için iş ortağı eklentileri anılıyor (SAP iş ortağı sayfası, Ü).
- **KOBİ için:** Küçük (5–50 kullanıcılı) firmada kurulum, danışman ve lisans yükü orantısız **[ÖNERİ]**; Türkiye fiyatı bilinmiyor (?).

### 2.2 SAP Business One (KOBİ)
- Proje yönetimi "temel" düzeyde (İ, B2); inşaata özgü proje maliyeti, taşeron yönetimi vb. ek lisans/eklenti gerektirebilir (İ, B2). Yunan bir üretici müşterisinin vaka çalışmasında başlangıç sorunu "güçlü proje yönetimi eksikliği" (Ü, SAP vaka yazısı; inşaat firması değil).
- Kullanıcı yorumları: arayüz ve kurulum karmaşık, ölçeklenebilirlik sınırlı (İ, Capterra).
- Türkiye: e-Fatura/e-Defter/e-İrsaliye iş ortağı çözümleriyle yapılıyor; özel entegratör gereksinimi kaynaklar arasında çelişkili (İ, B10). 
- Fiyat: toplayıcılara göre bulut Professional kullanıcı başı ~$91–250/ay, aralık geniş (?) (B3).

## 3. Diğer referanslar

### 3.1 Uluslararası inşaat ürünleri
- **Procore:** inşaat proje yönetimi, muhasebe/genel defter değil; genelde ERP ile birlikte kullanılır (İ). Fiyat yıllık inşaat hacmine göre, sınırsız kullanıcı; tahmini yıllık $10 bin–100 bin+ (?, İ). Saha uygulaması çevrimdışı çalışma açısından övülüyor; bazı özellikler yalnız masaüstünde, yeni kullanıcılar için karmaşık bulunuyor (İ, B4). Türkiye yerelleştirmesi doğrulanmadı (?). 
- **Oracle Primavera Cloud / Aconex:** Primavera Cloud zamanlama odaklı (P6'nın bulut karşılığı değil); Aconex büyük sermaye projelerinde belge/yazışma kaydı; ikisi de teklif bazlı (İ, B5). küçük bir firma için fazla.
- **Trimble Viewpoint Vista:** muhasebe merkezli yüklenici ERP'si, fiyat teklif bazlı (İ, B5). **Buildertrend:** konut/tadilat odaklı, aylık fiyat kaynaklara göre $99–299 (tutarsız, ?). Kamu işi/hakediş mantığına uzak.
- **[ÖNERİ]** Bu ürünler birebir rakip değil; "saha ekranı ve belge akışı" için ilham kaynağı.

### 3.2 Türkiye'deki yerli çözümler
- **Uyumsoft (Liox) İnşaat ERP:** hakediş (özet verinin Excel'den içe aktarımı), satın alma, depo, sözleşme (taşeron sözleşmeleri dahil), "Maliyet Kontrol" (planlanan–gerçekleşen), standart/özel raporlar (Ü, Ü4). Poz, ekipman, mobil saha sayfada anılmıyor; e-Fatura ayrı ürün; fiyat yok.
- **AMP Hakediş ve Yaklaşık Maliyet / e-HakedişNet:** 11 idareye ait 70.000+ poz ve analiz, hakediş hesabı (Ü/İ, B6). Bunlar ERP değil, poz/hakediş programı; entegrasyon biçimi doğrulanmadı (?).
- Poz numarasının ilk iki hanesi idare kodu; Çevre, Şehircilik ve İklim Değişikliği Bakanlığı kodu 10; 2026 birim fiyatları 15.01.2026'da yayımlandı (İ, hakedis.org; site AMP ürünlerini tanıtıyor, satıcı içeriği olabilir; resmî doğrulama gerekir) (B6). Resmî yapı ayrı araştırma dosyasının konusu.
- Logo/Netsis/Mikro gibi muhasebe odaklı yerli ürünlerin inşaat modülleri bu çalışmada doğrulanamadı (?).

### 3.3 Açık kaynak ERP'ler
**Odoo**
- Lisans: Community **LGPL v3**; Enterprise **Odoo Enterprise Edition License v1.0** (abonelik zorunlu) (R, D2; sayfa gövdesi araç tarafından kısmen okunabildi, başlıklar ve arama özeti doğrulandı).
- Türkiye (Odoo 19, R, D1): `l10n_tr` (GİB 7/A hesap planı, vergiler, mali pozisyonlar), `l10n_tr_reports`, e-İrsaliye modülü; Nilvera (GİB onaylı entegratör) üzerinden e-Fatura/e-Arşiv (UBL-TR 1.2), e-Defter. Lisans: e-Fatura, e-Arşiv ve e-İrsaliye için `l10n_tr_nilvera`, `l10n_tr_nilvera_einvoice`, `l10n_tr_nilvera_einvoice_extended`, `l10n_tr_nilvera_edispatch` modülleri odoo/odoo **Community** deposunda, `'license': 'LGPL-3'` (doğrulandı: resmî kaynak kodu, D5). **e-Defter:** dokümana göre e-Defter üretimi `l10n_tr_nilvera` ile anılıyor (D1), ancak Community'deki bu modülün manifestinde ve `models/` dosyalarında (account_journal, res_company, res_partner vb.) e-Defter/ledger koduna rastlanmadı; `l10n_tr_reports` Community deposunda yok. İki bağımsız inceleme bu noktada farklı sonuçlar verdi (biri LGPL-3/Community, diğeri Enterprise gerekebilir). Sonuç: **e-Defter'in Community'de olup olmadığı doğrulanmadı**; Enterprise gerekebilir (çıkarım) **[BELİRSİZ]**. Community'de yasal raporların yeterliliği de ayrıca sınanmalı. **Tüm e-belge işlevleri ücretli Nilvera hesabı gerektirir** (entegratör hizmeti Odoo lisansından ayrı ücretlendirilir; İ, inceleme notu); modül lisansının LGPL olması hizmeti ücretsiz yapmaz. Üçüncü taraf Nilvera PDF eklentisi OPL-1 lisanslı (İ).
- İnşaat: çekirdekte ilerleme faturası/retention mantığı yok görüşü (İ, ecosire; blog ise tersini iddia ediyor — çelişkili); ücretli eklentiler: AIA tarzı ilerleme faturası ~$199 (OPL-1, Odoo Apps), kilometre taşı faturalama ~$382, ecosire özel paket $999+ (Ü/İ, B12). AIA (ABD) formatı Türk hakedişine birebir uymaz **[ÖNERİ]**.
- Fiyat: odoo.com/pricing sayfasına göre Standard €14,90, Custom €27,90 kullanıcı/ay (ilk 12 ay indirimli; ülkeye göre değişir; Odoo.sh/on-premise yalnız Custom) (doğrulandı: resmî kaynak, D6; `06-teknik-mimari-altyapi.md` ile uyumlu). Toplayıcı sitelerin farklı rakamları kullanılmadı.

**ERPNext (Frappe)**
- Lisans: **GPL-3.0** (R, D3). İnşaat dikeyi/BOQ topluluk ve satıcı işi; "gerçek inşaat OSS'si nadir" (İ).
- Türkiye: resmî yerelleştirme bulunamadı; ticari ecosire e-Arşiv/e-Fatura uygulaması ve topluluk GitHub projesi var, bakım durumu doğrulanmadı (?, B11).

### 3.4 "Açık kaynak ERP'yi temel al ve özelleştir" seçeneği

| | Artı | Eksi |
|---|---|---|
| **Odoo Community/Enterprise temel** | Hazır muhasebe, satın alma, stok, proje, kullanıcı/yetki; resmî TR yerelleştirme ve e-belge (R); büyük eklenti ekosistemi; ürün olgun; sıfırdan yazmaya göre ilk sürüm daha hızlı olabilir **[ÖNERİ]** | Hakediş/poz/kamu işi mantığı yine özel geliştirme; sürüm yükseltme ve eklenti uyumu yükü; Enterprise abonelik bağımlılığı; "sade arayüz" hedefi ürünün kendi UX'ine bağlı kalır; veri modeli Odoo'ya kilitlenir |
| **ERPNext temel** | GPL, lisans ücreti yok; Frappe framework ile hızlı özelleştirme; inşaat/proje temeli | TR yerelleştirme ve e-belge resmî değil; daha küçük TR uzman havuzu (?); GPL kopyaleft yükümlülükleri için hukuki görüş gerekir |
| **Sıfırdan geliştirme** | Poz/hakediş ve Excel geçişine göre tam uyum; arayüz üzerinde tam kontrol; lisans bağımlılığı yok | Muhasebe, e-Fatura, e-Defter, yetki, denetim izi baştan yazılır veya entegre edilir; süre ve bakım maliyeti yüksek; kapsam şişmesi riski |
| **Hibrit** | Muhasebe/e-belge için hazır sistem veya entegratör, poz–hakediş–saha için özel modül | Veri iki yerde; entegrasyon karmaşıklığı |

**[ÖNERİ]** Karar vermeden önce kısa, süre sınırlı bir kavram kanıtı: aynı mini senaryo (bir poz listesi → hakediş → e-Fatura taslağı) Odoo'da ve özel geliştirmede denenip eforu kıyaslanmalı. Nihai seçim kullanıcıya aittir. Lisans (LGPL/OEEL/GPL) etkisi için hukuki danışman görüşü gerekir (?).

---

## 4. Karşılaştırma tablosu

Gösterim: **+** kaynaklı destek; **Ü** üretici iddiası; **E** eklenti/özel geliştirme gerekir; **~** genel bilgi, bu çalışmada kaynaklanmadı; **?** doğrulanmadı; **–** yok/zayıf.

| Ürün | Proje maliyeti | Hakediş / ilerleme faturası | Satın alma | Stok | Ekipman | Taşeron | Saha mobil | Raporlama | TR yerel. | Karmaşıklık | Maliyet |
|---|---|---|---|---|---|---|---|---|---|---|---|
| CANIAS | Ü | Ü | Ü | ~ | Ü | Ü (ayrıntısız) | ? | Ü | Ü e-Fatura/e-Defter | ? | Teklif (?) |
| SAP S/4HANA PS | + WBS | + kilometre taşı; ilerleme için E | ~ | ~ | ~ | ? | ? | ~ | ? (iş ortağı) | Çok yüksek (~) | ? yüksek |
| SAP Business One | Temel (İ) | E | ~ | ~ | ? | E (İ) | ? | ~ | İş ortağı çözümü (İ) | Orta–yüksek (İ) | ~$91–250/kul./ay (?) |
| Procore | + (muhasebe yok) | ~ | ~ | – | – | + (İ) | + çevrimdışı (İ) | ~ | ? | Yeni kullanıcıya zor (İ) | Hacim bazlı $10k–100k+/yıl (?) |
| Primavera / Aconex | ? | ? | ? | – | ? | ? | ? | ? | ? | Yüksek (~) | Teklif (İ) |
| Uyumsoft Liox İnşaat | Ü | Ü (Excel içe aktarma) | Ü | Ü | ? | Ü (sözleşme) | ? | Ü | Yerli; e-Fatura ayrı ürün (Ü) | ? | Fiyat yok |
| Odoo | ~ | E ($199–999+) (İ) | ~ | ~ | ? | E (İ) | ? | ~ | + resmî (R); e-Fatura/e-Arşiv/e-İrsaliye modülleri Community/LGPL-3 (R); e-Defter'in Community'de olduğu doğrulanmadı, Enterprise gerekebilir (?); tümü ücretli Nilvera hesabı ister | Orta | CE lisanssız; Standard €14,90 / Custom €27,90 kul./ay (R, D6) |
| ERPNext | ~ (İ) | ? | ~ | ~ | ? | ? | ? | ~ | – resmî yok; 3. taraf ? | Orta | Lisanssız |

Not: Tablo, ürünleri birebir ranking değil, doğrulama boşluklarını görmek içindir. Çok sayıda "?" hücre, demo/teklif ve üretici sorgusu gerektiren noktalardır.

---

## 5. Sade arayüz önerileri

Büyük ERP'lerde belgelenen sorunlar: devasa menü yapıları, yetersiz yönlendirme, sınırlı görev desteği, karmaşık ekranlar (İ, B7; 2016 bilimsel makale, tam metin okunmadı). Aşağıdaki ilkeler **[ÖNERİ]**; müşteri onayı yoktur.

1. **Rol bazlı ana sayfa.** Sahip: kâr/zarar, nakit, proje durumu kartları; şantiye şefi: bugünün işleri, bekleyen onaylar; muhasebe: bekleyen belgeler. *Örnek:* SAP Fiori "işlevden iş rolüne" geçiş (R, SAP Learning, D4). *Dikkat:* sadeleştirme uzman kullanıcıların iş akışını parçalayabilir (İ, B8); rol ana sayfası yetki modelinin yerine geçmez.
2. **Proje merkezli gezinme.** Üstte proje seçici; tüm modüller seçili proje bağlamında. Sorular ("bu projenin maliyeti?") modül aramadan cevaplanır. *Örnek:* SAP PS'te her şeyin WBS'e bağlanması (R); Procore'un proje bazlı çalışma modeli (~).
3. **Excel benzeri tablo düzenleme.** Poz/metraj/hakediş cetvelinde hücre içi düzenleme, yapıştır, sürükle-doldur, toplam satırı, formül hücresi yerine görünür hesap sütunları. Firma bugün Excel'de; geçiş sürtünmesini azaltır. *Örnek:* Uyumsoft hakedişte Excel'den veri alma (Ü4); Odoo/ERPNext düzenlenebilir liste ızgaraları (~, kaynaklanmadı).
4. **Hızlı giriş.** Zorunlu alan az, akıllı varsayılan (proje, tarih, KDV), klavye ile ilerleme, "kaydet ve yeni", kopyala-yapıştır satır. Hangi ekranların referans alınacağı pilot keşifte öğrenilmeli **[BELİRSİZ]**.
5. **Mobil saha ekranları.** Günlük puantaj, malzeme girişi, fotoğraf, günlük rapor; az alan, büyük düğme, çevrimdışı kuyruk. *Örnek:* Procore çevrimdışı modu övülüyor; mobil sürümün masaüstünün gerisinde kalması eleştiriliyor (İ, B4) — mobilde "az ama eksiksiz" özellik seçilmeli.
6. **Toplu içe aktarma.** Şablonlu Excel/CSV içe aktarma, önizleme, hata satırı raporu, geri alma. *Örnek:* Uyumsoft CSV/Excel aktarımı (Ü4). Excel geçişi ayrı iş paketi.
7. **Türkçe terminoloji.** Sahada kullanılan dil: poz, metraj, keşif, hakediş, yaklaşık maliyet, geçici/kesin kabul, teminat, kesinti, fiyat farkı, taşeron. Muhasebede GİB 7/A hesap planı terimleri. *Örnek:* Odoo `l10n_tr` 7/A hesap planı (R, D1); Terimin yerel karşılığı önemlidir. Terim sözlüğü pilot firmayla onaylanmalı.
8. **İlerleme rehberliği ve görünür durum.** Çok adımlı işlerde (hakediş: metraj → onay → fatura) adım göstergesi, eksik veri uyarısı, "sıradaki adım" düğmesi. *Örnek:* Akademik bulgu: ilerleme rehberliği kullanılabilirlik için temel (İ, B7); SAP PS'te eksik vade tarihinin sessizce 0 gelir üretmesi, bunun tersi bir kötü örnek (R, D4).

Ek ilke **[ÖNERİ]:** "En fazla 2 tıklamada" hedefi, her ekranda tek ana eylem, gelişmiş alanlar katlanır; rapor Excel/PDF dışa aktarımı her listede.

---

## 6. Doğrulanamayan / zayıf kaynaklı iddialar
- SAP resmî Business One sayfası (403) okunamadı; SAP B1 inşaat bilgileri ikincil.
- Capterra/TrustRadius sayfaları doğrudan okunamadı; yorum özetleri arama sonuçlarından.
- Odoo dışındaki fiyatlar (SAP B1, Procore, Buildertrend) toplayıcı/rakip kaynaklı; Odoo fiyatı resmî sayfadan.
- Odoo lisans sayfasının gövdesi kısmen okunabildi (e-belge modüllerinin LGPL-3 olduğu manifestlerden doğrulandı).
- Odoo e-Defter için Community/Enterprise ayrımı: Community modülünde e-Defter kodu görünmüyor ve `l10n_tr_reports` Community'de yok; Enterprise gerekliliği çıkarım, kapalı Enterprise deposu okunamadı.
- Odoo'nun inşaat/ilerleme faturası kapasitesi kaynaklar arasında çelişkili.

## Açık sorular
Segment düzeyinde açık sorular:
1. Hedef kullanıcılar daha önce hangi ERP/ürünleri kullandı ya da beğendi; en çok kullanılan ekranlar hangileridir?
2. Referans ürünlerde en çok beğenilen ve en çok yoran şeyler nelerdir (ekran düzeni, hız, raporlar, hakediş akışı)?
3. Referans ürünler hangi modülleriyle ve ne süreyle kullanıldı; ekran görüntüsü/video örnekleri var mı?
4. Hangi işler hâlâ Excel'de yapılmak istenir (formül, pivot)? Excel benzeri tablo ekranı ne kadar önemlidir?
5. Sahada kim, hangi cihazla ve internetle veri girer? Çevrimdışı çalışma gerekir mi?
6. Hakediş hazırlığında adım adım neler yapılır ve en çok zaman nerede kaybedilir?
7. Poz/birim fiyatlar hangi kaynaktan ve hangi programla alınır (AMP, e-HakedişNet, kurum dosyası)? Bu programlar ERP'de de kalmalı mı?
8. Hazır bir ERP'yi özelleştirmek, sıfırdan yazıma göre kabul edilebilir mi; yıllık lisans/abonelik tutarı için üst sınır var mı?
9. Ekranlarda kullanılan Türkçe terimler hangileridir; ekipler arasında farklı adlandırmalar var mı?
10. Ana sayfada yöneticiler hangi 5 sayıyı her sabah görmek ister?
11. Başka referans ürünler (SAP veya inşaat yazılımı) hakkında geri bildirimler nelerdir?

## Açık noktalar / riskler
- Hedef kullanıcıların beğendiği ekranlar ve akışlar bilinmiyor; arayüz hedefi somutlaşmadan (örnek ekranlar, kullanıcı testi) UX kararı vermek riskli **[BELİRSİZ]**.
- Poz/kamu hakedişi mantığına yerli rakip dışında hazır çözüm yok; hangi hesap/rapor biçimi gerektiği müşteri ve mevzuat doğrulaması bekliyor (diğer araştırma dosyalarıyla birlikte ele alınmalı).
- Açık kaynak temel seçilirse: lisans yükümlülükleri, yükseltme maliyeti ve Enterprise abonelik bağımlılığı **[BELİRSİZ]**; hukuki görüş gerekir.
- Türkiye e-belge eşik/takvim bilgileri kaynaklar arasında çelişkili (ör. 2026–2027 geçiş tarihleri); GİB'den doğrulanmalı (İ, B10).
- Fiyatlar teklifle doğrulanmadan bütçe kararı verilmemeli.
- Rapor "sade arayüz"ü bir kural seti olarak sunar; gerçek kullanıcı testi (birkaç gerçek kullanıcıyla prototip) yapılmadan etkisi kanıtlanmış sayılmamalı.

## Kaynaklar

**Ürün siteleri (üretici iddiası, Ü)**
- Ü1 CANIAS inşaat: https://canias.com/en/erp-for-construction-companies
- Ü2 CANIAS modüller: https://canias.com/en/caniaserp-modules/fin
- Ü3 CANIAS proje/muhasebe (sektörel çözüm sayfası): https://cdnweb.canias.com/en/sectoralsolutiondetail/industrial-manufacturing/92
- Ü4 Uyumsoft İnşaat ERP: https://uyumsoft.com/insaat-erp ; e-kitap https://uyumsoft.com/assets/e-book/insaat-sektoru-erp-kullanimi.pdf

**Dokümantasyon / resmî (R)**
- D1 Odoo 19 Türkiye yerelleştirme: https://www.odoo.com/documentation/19.0/applications/finance/fiscal_localizations/turkiye.html
- D2 Odoo lisanslar: https://www.odoo.com/documentation/master/legal/licenses.html
- D3 ERPNext GitHub (GPL-3.0): https://github.com/frappe/erpnext
- D5 Odoo 19 Nilvera modül manifestleri (LGPL-3; bağımsız inceleme R2 ile doğrulandı): https://raw.githubusercontent.com/odoo/odoo/19.0/addons/l10n_tr_nilvera/__manifest__.py
- D6 Odoo fiyatları: https://www.odoo.com/pricing (06-teknik-mimari-altyapi.md üzerinden, 18.11.2026)
- D4 SAP Learning (kilometre taşı faturalama, Fiori): https://learning.sap.com/learning-journeys/discovering-the-basics-of-sap-s-4hana-project-system/billing-projects-with-milestone-billing_df54015b-12b1-438d-85a6-b278a9de8734 ; https://learning.sap.com/learning-journeys/explore-integrated-business-processes-in-sap-s-4hana/understanding-the-new-user-experience_de01a4f5-6b7a-44ad-b312-e9a6b3ffb3e4

**Bağımsız / ikincil (İ)**
- B1 CANIAS yorumları: https://www.capterra.com/p/51528/CANIAS-ERP/reviews/ ; https://www.trustradius.com/reviews/canias-erp-2025-05-21-02-14-49
- B2 SAP B1 inşaat: https://erpresearch.com/en-us/sap-business-one-for-construction ; https://www.capterra.com/p/214667/SAP-Business-One/reviews/ ; SAP vaka: https://www.sap.com/greece/documents/2024/10/8efb6e40-d97e-0010-bca6-c68f7e60039b.html
- B3 SAP B1 fiyat: https://erpresearch.com/en-gb/sap-business-one-cost
- B4 Procore: https://erpresearch.com/erp-add-ons/construction/procore ; https://projul.com/blog/procore-pricing-analysis-2026/ ; https://www.trustradius.com/reviews/procore-2025-06-25-15-24-14
- B5 Primavera/Aconex/Vista: https://erpresearch.com/erp-add-ons/construction/oracle-aconex-vs-oracle-primavera ; https://www.rfp.wiki/vendors/viewpoint/oracle-aconex
- B6 Poz/hakediş: https://www.hakedis.org/2026-birim-fiyatlari-yayinlandi-cevre-ve-sehircilik-bakanligi-birim-fiyatlarina-nasil-erisilir-2/ ; https://www.tamindir.com/indir/e-hakedisnet/
- B7 ERP kullanılabilirlik: https://www.scitepress.org/Papers/2016/57702/57702.pdf ; https://scitepress.org/Papers/2014/50990/pdf/index.html
- B8 Fiori uzman kullanıcı: https://www.heflo.com/blog/sap-fiori-for-power-users
- B10 SAP e-belge: https://blog.cloudspark.com.tr/en/sap-business-one-einvoice-eledger-integration/ ; https://mdpgroup.com/cozumler/e-donusum
- B11 ERPNext TR: https://ecosire.com/apps/erpnext/erpnext-turkey-earsiv-einvoice ; https://discuss.frappe.io/t/turkey-e-invoice-sending-app/63282
- B12 Odoo inşaat eklentileri: https://apps.odoo.com/apps/modules/18.0/construction_progress_billing_aia ; https://apps.odoo.com/apps/modules/19.0/construction_contracting_milestone_progress_billing ; https://docs.ecosire.com/odoo-modules/construction-billing
