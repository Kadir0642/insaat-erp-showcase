# 07 — Excel → ERP Geçiş Planı (Yöntem ve Şablonlar)

> Belge numaraları (00–13), karar numaraları (K-xx, D-xx) ve "pilot keşif" kavramı için: [ARASTIRMA-OZETI.md](../ARASTIRMA-OZETI.md#bu-belgeler-nasıl-okunur).

> Durum: Bu belge belirli bir dosyaya özgü değildir; gerçek dosyalar geldiğinde uygulanacak **yöntem ve şablonlardır**. Kaynaksız yöntem maddeleri **[ÖNERİ]** etiketlidir. Araç/teknoloji adları seçenek olarak sunulur, karar kullanıcıya aittir.

## Özet
- **[GEREKSİNİM]** Excel'den ERP'ye geçiş temel ihtiyaçtır ve ürünün ana iş paketlerinden biridir; dosyalar gerçek iş kurallarının ve veri alanlarının öncelikli kaynağıdır (pilot keşif).
- **[ÖNERİ]** Geçiş, 9 aşamalı ayrı bir ana iş paketi olarak yürütülür: envanter → anlama → iş kuralı çıkarma → alan eşleme → temizleme → örnek aktarım → mutabakat → paralel çalışma → cut-over/arşiv.
- **[ÖNERİ]** En büyük risk teknik değil bilgisel: formülü yalnızca sahibinin bildiği, belgelenmemiş kurallar. Her hesaplama "iş kuralı kartı" ile yazıya dökülüp müşteriye onaylatılır.
- **[ÖNERİ]** Doğrulama üç katmanlıdır: kontrol toplamları/satır sayıları, rastgele örneklem, kullanıcı kabul testi (UAT). Mutabakat farkı "açıklanmamış" kalmadan cut-over yapılmaz.
- **[ÖNERİ]** Müşteri dosyaları repoya girmez; yerel, git dışı, erişimi kısıtlı klasörde tutulur; onaysız dış servise gönderilmez (özellikle bulut tabanlı yapay zekâ/OCR/dönüştürücü servisleri).
- **[ÖNERİ]** "Excel'e geri dönme" riski, ERP'de Excel'e dışa aktarma, tanıdık tablo görünümleri ve içe aktarma şablonlarıyla azaltılır.
- **[BELİRSİZ]** Tarihsel verinin ne kadarı taşınacak, açılış bakiyeleri hangi tarihte ve hangi kaynakla kurulacak: müşteriyle karar gerekir.

## 1. Geçiş aşamaları

Her aşamanın **çıktısı** ve **çıkış kriteri** vardır; kriter sağlanmadan sonraki aşamaya geçilmez. **[ÖNERİ]**

| # | Aşama | Ana faaliyet | Çıktı | Çıkış kriteri |
|---|-------|--------------|-------|---------------|
| 1 | Envanter | Tüm dosyaların (güncel sürüm, kopyalar, e-posta/WhatsApp ile dolaşanlar dahil) listelenmesi, sahiplerle kısa görüşme | Envanter tablosu (§2) | Müşteri "başka dosya yok" der; kopyalar tek kanonik sürüme bağlanır |
| 2 | Anlama | Sayfa, formül, makro, adlandırılmış aralık, dosyalar arası bağlantı, pivot, koşullu biçim, gizli sayfa/satır/sütun, veri doğrulama listeleri, korumalı alanlar çıkarılır | Dosya başına "yapı raporu" (otomatik + elle) | Tüm sayfalar ve bağımlılıklar kayıt altında; gizli/yetim sayfalar açıklanmış |
| 3 | İş kuralı çıkarma | Her hesaplamanın iş dilinde karşılığı yazılır (§4), test örnekleri üretilir | İş kuralı belgeleri | Müşteri her kartı onaylamış veya düzeltmiş |
| 4 | Veri modeli / alan eşleme | Excel sütun → ERP alanı eşlemesi, anahtarlar, ilişkiler, kod listeleri | Eşleme tablosu (§3.3) | Eşlenmemiş sütun kalmamış (taşınacak / taşınmayacak / türetilecek) |
| 5 | Temizleme | Yinelenen, eksik, tutarsız birim/tarih/sayı biçimi, birleştirilmiş hücre, serbest metin | Temizleme kuralları + temizlenmiş veri + hata günlüğü | Kural listesi müşteri onaylı; reddedilen kayıtlar için sahip kararı var |
| 6 | Örnek aktarım | Küçük ama temsili bir dilim (ör. tek proje, tek dönem) test ortamına aktarılır | Aktarım betiği/şablonu + sonuç raporu | Betik tekrarlanabilir (aynı girdi → aynı çıktı) |
| 7 | Tutarlılık kontrolü | Excel toplamları ↔ ERP toplamları mutabakatı (§5) | Mutabakat raporu | Tüm fark kalemleri açıklanmış ve kabul edilmiş |
| 8 | Paralel çalışma | Belirli süre hem Excel hem ERP; sonuçlar karşılaştırılır | Haftalık fark raporu, UAT bulguları | Ardışık N dönem farksız/açıklanmış kapanış |
| 9 | Cut-over ve arşiv | Excel'e yazma kapatılır, son aktarım yapılır, Excel'ler salt-okunur arşivlenir | Geçiş tutanağı, arşiv paketi | Müşteri imzalı kabul; geri dönüş planı süresi doldu |

Notlar:
- **Paralel çalışma süresi** [BELİRSİZ]: ay kapanışı/hakediş döngüsünü en az bir kez kapsamalıdır; önerilen başlangıç noktası 1–2 tam hakediş/ay kapanışı, müşteriyle netleştirilir.
- **Cut-over öncesi dondurma**: son aktarım günü Excel'de değişiklik yapılmaz (donma penceresi); donma sonrası girişler ERP'ye elle işlenir. **[ÖNERİ]**
- **Geri dönüş planı**: cut-over sonrası belirli süre Excel arşivi salt-okunur kalır, kritik fark çıkarsa kontrollü düzeltme yapılır; çift yönlü senkronizasyon önerilmez (veri kaynağı belirsizleşir). **[ÖNERİ]**

## 2. Envanter şablonu

Dosya başına bir satır; ayrıca dosya içindeki her sayfa için ikinci tablo (sayfa envanteri). Şablon CSV/Excel olarak tutulur, **dosya içeriği değil yalnızca üst veri** içerir. **[ÖNERİ]**

**Dosya envanteri**

| Alan | Açıklama / örnek |
|------|------------------|
| Dosya kodu | EX-001 (kalıcı kimlik) |
| Dosya adı ve sürüm | "..._v3_son_FINAL.xlsx"; kanonik mi, kopya mı |
| Sahibi / kullananlar | Kim güncelliyor, kim okuyor |
| Güncelleme sıklığı | günlük / haftalık / aylık / hakediş başına / ad hoc |
| Son güncelleme tarihi | |
| Amaç | Tek cümle (ör. "şantiye malzeme çıkışı takibi") |
| Sayfa sayısı (gizli dahil) | |
| Satır sayısı (sayfa başına, kullanılan aralık) | |
| Formül var mı / yaklaşık adet | evet-hayır, adet |
| Makro (VBA) var mı | .xlsm/.xlsb, modül sayısı |
| Başka dosyaya bağlantı | Dış bağlantı yolları (ağ klasörü, e-posta eki) |
| Pivot / grafik / koşullu biçim | var-yok |
| Hassas veri var mı | kişisel veri (TC kimlik, IBAN, maaş), ticari sır, ihale teklif bilgisi |
| Veri kalitesi izlenimi | iyi / orta / zayıf (ilk bakış) |
| ERP'de karşılık gelen modül | proje, satın alma, stok, hakediş, cari, personel, ... |
| Kritiklik | Geçiş ilk sürümünde şart mı (MVP) |
| Notlar / açık sorular | |

**Sayfa envanteri**: dosya kodu, sayfa adı, gizli mi, amaç, veri/hesap/rapor sayfası mı (girdi–hesap–çıktı rolü), kullanılan aralık, birleştirilmiş hücre var mı, başlık satırı yeri. **[ÖNERİ]**

## 3. Anlama ve eşleme yöntemi

### 3.1 Otomatik analiz araçları (yalnızca öneri; seçim kullanıcıya aittir)

Bakım ve lisans bilgileri bağımsız incelemede PyPI meta verisinden ve oletools GitHub sayfasından doğrulandı, 18.11.2026 (ikincil kaynak: paket dizini). Yetenek tanımları üretici dokümanlarına dayanır; seçim öncesi güncel sürüm yeniden kontrol edilmelidir.

| Amaç | Aday araç/kütüphane | Bakım / lisans (doğrulandı: PyPI) | Artı | Eksi / dikkat |
|------|---------------------|-----------------------------------|------|----------------|
| xlsx/xlsm okuma: sayfalar, formül metinleri, adlandırılmış aralıklar, birleştirilmiş hücreler, gizli sayfa, veri doğrulama, koşullu biçim | Python **openpyxl** — https://openpyxl.readthedocs.io | 3.1.5 (28.06.2024), MIT; 2 yılı aşkın süredir yeni sürüm yok | Yaygın; formülü metin olarak okur (`data_only=False`) | .xls ve .xlsb okumaz; pivot/grafik ayrıntısı sınırlı; kaydederken öğe kaybedebilir, bu yüzden **yalnızca okuma** |
| Hesaplanmış değerleri okuma | openpyxl `data_only=True` | aynı | Excel'in son kaydettiği değer | Dosya hesaplanıp kaydedilmemişse değer boş olabilir |
| Tablo olarak toplu okuma/profil | **pandas** (https://pandas.pydata.org) | (doğrulanmadı) | Tür/eksik/yinelenen profili hızlı | Birleştirilmiş hücre ve çok başlıklı sayfalarda elle ayar ister |
| Eski .xls / .xlsb | **xlrd** (yalnız .xls), LibreOffice ile yerelde dönüştürme; .xlsb için ayrı okuyucu (ör. pyxlsb) | (doğrulanmadı) | | Dönüştürme yerelde yapılmalı |
| VBA makro çıkarımı | **oletools / olevba** — https://github.com/decalage2/oletools | PyPI son sürüm 0.60.2 (02.07.2024), BSD; GitHub'da 0.60.3 (22.05.2025) anılıyor | Makroyu **çalıştırmaz**, yalnızca okur; OpenXML (.xlsm) içinden VBA çıkarır | .xlsb desteği doğrulanamadı; PyPI ile GitHub sürüm farkı açık; makroyu anlamak yine insan emeği ister |
| Formül bağımlılık grafiği (**birincil aday**) | **formulas** (https://github.com/vinci1it2000/formulas) | 1.3.4 (11.03.2026), EUPL 1.1+ (copyleft); aktif bakımdaki tek formül aracı | Formülleri ayrıştırıp bağımlılık çıkarır; Excel'siz yeniden hesaplama | Fonksiyon kümesi sınırlı; makro/dış bağlantı kapsamaz; yalnızca iç analiz aracı olarak kullanımda dağıtım yükümlülüğü doğmaz, yine de 06'daki lisans taraması önerisine bağlanmalı |
| Formül değerlendirme (alternatif) | **xlcalculator** (https://github.com/bradbase/xlcalculator) | 0.5.0 (06.02.2023), MIT; arşivlenmemiş ama sürüm almıyor | Basit kullanım | Bakım zayıf; yalıtılmış ortamda kullanılmalı |
| Dış bağlantılar | xlsx dosyasını zip olarak açıp `xl/externalLinks/` ve `workbook.xml` incelemek (OOXML) | ek bağımlılık yok | Ek bağımlılık yok | Betikle çözümleme gerekir |
| Elle doğrulama | Excel: "Formül Denetleme > Bağımlıları İzle", "Bağlantıları Düzenle", "Ad Yöneticisi" | | Müşteriyle ekranda birlikte bakılabilir | Büyük dosyada yavaş |

**Aday listeden çıkarıldı: pycel.** CVE-2024-53924 (CVSS 9.8) uyarınca pycel 1.0b30 ve öncesi, güvenilmeyen tablodaki hazırlanmış formül yoluyla kod çalıştırmaya izin veriyor; düzeltilmiş sürüm bildirilmemiş, son sürüm 1.0b30 (13.10.2021), lisansı GPLv3 (PyPI; Debian güvenlik takipçisi). WhatsApp/e-posta ile dolaşmış dosyalar güvenilir sayılamayacağından müşteri dosyalarıyla kullanılmaz.

Önerilen çıktı: her dosya için otomatik üretilen `yapi-raporu` (sayfa listesi, formül sayısı ve en sık geçen formül desenleri, dış bağlantılar, makro modülleri, adlandırılmış aralıklar, sütun tür profili). Betikler repoda tutulabilir; **müşteri dosyaları ve bunlardan üretilen içerikli çıktılar** tutulamaz.

### 3.2 Gizlilik ve işleme kuralları **[ÖNERİ]**
- **Yalıtılmış ortam kuralı:** Müşteri dosyalarını işleyen tüm formül/makro/ayrıştırma araçları (formulas, xlcalculator, oletools, openpyxl, dönüştürücüler dahil) **ağ erişimi olmayan, yalıtılmış bir ortamda** (konteyner veya sanal makine, çıkış trafiği kapalı, salt-okunur bağlanmış girdi klasörü) çalıştırılır; dosyalar kaynak olarak güvenilmez sayılır, çalıştırılan Python `-I` modunda ve ayrı bir dizinden başlatılır.
- Müşteri dosyaları **repoya konmaz**; `.gitignore`'a eklenen, git dışı, yerel ve şifreli/erişimi kısıtlı bir klasörde (ör. proje dışı bir "musteri-verisi" dizini) tutulur.
- **Dış servise (bulut dönüştürücü, çevrimiçi OCR, genel yapay zekâ sohbet/analiz servisi) dosya veya içerik gönderilmez; müşteri onayı olmadan.** Onay alınırsa kapsam (hangi dosya, hangi servis, veri konumu) yazılı kaydedilir.
- İşleme yalnızca yerelde çalışan araçlarla yapılır; çalışma kopyası alınır, **orijinale dokunulmaz**, kopyanın hash'i (SHA-256) envantere yazılır.
- Hassas veri (TC kimlik no, IBAN, maaş, teklif fiyatları) için maskeleme kuralı: analiz ve örnek test verilerinde gerçek değerler kullanılmaz veya maskelenir. KVKK kapsamı [BELİRSİZ]: personel verisi taşınacaksa hukuki değerlendirme ayrıca yapılmalı.
- Dosyaların paylaşım kanalı (e-posta eki yerine müşterinin onayladığı güvenli kanal) müşteriyle kararlaştırılır.

### 3.3 Veri modeli ve alan eşleme şablonu **[ÖNERİ]**

| Kaynak dosya/sayfa/sütun | Örnek değer | Veri türü (Excel'de) | Hedef ERP varlığı.alanı | Dönüşüm kuralı | Zorunlu mu | Temizleme notu | Durum (taşınacak / türetilecek / taşınmayacak) |
|---|---|---|---|---|---|---|---|

Ek olarak: **kod listeleri** (birim, kategori, şantiye, taşeron adları) için "Excel'deki yazılışlar → ERP'deki kanonik değer" karşılık tablosu (ör. "m3", "M³", "metreküp" → `m3`). Excel'de bir hücrede birden çok bilgi (ör. kurgusal bir örnek: "Ad S. - 05xx...") varsa ayrıştırma kuralı yazılır.

## 4. Formül → iş kuralı belgesi şablonu

Her anlamlı hesaplama (veya aynı desendeki hesap grubu) için bir kart. Müşteri onayı olmadan kural ERP'de "doğru" sayılmaz. **[ÖNERİ]**

| Alan | İçerik |
|---|---|
| Kural kodu | IK-001 |
| Konum | Dosya kodu / sayfa / hücre veya aralık (ör. EX-004 / "Hakediş" / G12:G180) |
| Formül (ham) | `=SUMIFS(...)` (aynen) |
| İş dilindeki anlamı | "Bu hakedişte yapılan işin tutarı = bu dönem miktarı × sözleşme birim fiyatı; ..." |
| Girdiler | Hangi hücre/sayfa/dosyalar; hangisi elle girilen, hangisi başka formülden gelen |
| Çıktı | Birim, yuvarlama kuralı, hangi sayfa/rapora akıyor |
| Sınır durumları | Boş girdi, sıfır, negatif, KDV dahil/hariç, yuvarlama |
| Dosyalar arası bağlantı | Dış bağlantı varsa kaynak dosya |
| ERP'deki karşılığı | Modül, alan, hesap kuralı (hesaplanan alan / rapor / iş akışı) |
| Test örneği | Girdi → beklenen çıktı (en az 3: tipik, sınır, hatalı veri); Excel'den alınmış gerçek değerler (maskeli) |
| Belirsizlik | "Bu sabit neden 1,18?", "bu satır neden toplamdan hariç?" gibi yanıtsız sorular |
| Müşteri onayı | Onaylayan, tarih, düzeltme notu |
| Durum | taslak / müşteriye soruldu / onaylandı / ERP'de uygulandı / testten geçti |

Yöntem: (a) otomatik araçla formül desenleri gruplanır (aynı sütundaki tekrarlayan formül = tek kural); (b) tutarsız formüller (aynı sütunda farklı formül, sabit yazılmış değer) **ayrıca işaretlenir** çünkü çoğunlukla elle yapılmış istisnadır; (c) kartlar sahibiyle birlikte ekran başında gözden geçirilir; (d) test örnekleri ERP'de otomatik testlere dönüştürülür.

Türkçe yerel ayar tuzakları (temizleme kuralı olarak): ondalık virgül, metin olarak saklanmış sayılar, tarih biçimleri ve 1900/1904 tarih sistemi, büyük/küçük harf dönüşümünde İ/ı sorunu. Formül adları dosyada İngilizce saklanır, kullanıcı Türkçe görür; kural kartında formül her iki dilde yazılır. **[ÖNERİ]**

Özel dikkat: poz/birim fiyat, hakediş, KDV/stopaj/teminat kesintileri ve fiyat farkı gibi mevzuata bağlı hesaplar için kural, Excel'deki uygulamanın mevzuata uygunluğu açısından da ayrıca değerlendirilir; Excel'in hatalı olması olasılığı göz önünde tutulur (yeniden üretmek ≠ doğrulamak). **[ÖNERİ]** Mevzuat ayrıntısı ilgili araştırma dosyalarının kapsamıdır.

## 5. Doğrulama stratejisi

### 5.1 Katmanlar **[ÖNERİ]**
1. **Kontrol toplamları ve satır sayıları**: kaynakta okunan satır = aktarılan + reddedilen + bilerek atlanan. Sayısal sütunlarda toplam (tutar, miktar) ve dönem/proje/cari bazında alt toplamlar Excel ↔ ERP karşılaştırılır. Fark toleransı (ör. kuruş yuvarlama) önceden yazılır.
2. **Rastgele örneklem**: her tabloda tesadüfi N kayıt (ve risk yüksek kayıtlar: en büyük tutarlar, en eski, istisnai) alan alan karşılaştırılır; sonuç tutanağa yazılır.
3. **Kural testleri**: §4'teki test örnekleri ERP'de otomatik çalıştırılır; Excel'den gelen gerçek sonuçla aynı çıktı beklenir.
4. **Kullanıcı kabul testi (UAT)**: dosya sahibi kendi iş akışını ERP'de uçtan uca dener (ör. "geçen ayın hakedişini ERP'de yeniden üret"); beklenen çıktıyla Excel'inkini yan yana karşılaştırır.
5. **Mutabakat raporu**: her fark için sınıf: (a) Excel hatası, (b) temizleme kuralı etkisi, (c) ERP hatası, (d) açıklanamayan. (d) sıfırlanmadan geçiş onaylanmaz.

### 5.2 "Excel'e geri dönme" riskini azaltma **[ÖNERİ]**
- Her liste/rapor ekranında **Excel'e dışa aktarma** (biçimli, filtre uygulanmış görünüm); kullanıcı veriyi kaybettiği hissine kapılmaz.
- Kullanıcıların alışık olduğu **tanıdık tablo görünümleri**: Excel'deki sütun sırası ve adlarıyla kaydedilebilir görünüm, filtre/sıralama, toplu yapıştırma ile satır ekleme.
- **İçe aktarma şablonları**: Excel'de toplu veri girişi alışkanlığı için, doğrulamalı (hata satırları raporlayan, önizlemeli) şablonlar; geçiş sonrasında da kalıcı özellik olabilir.
- Aylık "hâlâ Excel kullanılan süreçler" taraması; Excel'e dönülmesinin nedeni (eksik alan, yavaş ekran, eksik rapor) geri bildirim olarak ürün listesine alınır.
- Cut-over sonrası Excel arşivi **salt-okunur** ve işaretli ("ARŞİV - güncel veri ERP'de").

## 6. Riskler

| Risk | Etki | Azaltma **[ÖNERİ]** |
|---|---|---|
| Belgelenmemiş bilgi: formülü yalnızca tek kişi biliyor | Kural yanlış taşınır; kişi ayrılırsa kayıp | Sahiple görüşme, iş kuralı kartları, ekran başı gözden geçirme; "bus factor" listesi |
| Sürüm karmaşası (aynı dosyanın kopyaları, "_son_FINAL") | Yanlış sürümden aktarma | Envanterde kanonik sürüm kararı; hash ve son değişiklik tarihi; sahibe onaylatma |
| Tarihsel verinin kapsamı | Çok geniş: maliyet/süre artar; çok dar: raporlama/denetim kaybı | Müşteriyle karar: aktif projeler detaylı, biten projeler özet/arşiv; yasal saklama süreleri ayrıca araştırılmalı [BELİRSİZ] |
| Açılış bakiyeleri (cari, kasa/banka, stok, devam eden projelerin gerçekleşen maliyeti) | Yanlış başlangıç = sürekli sapma | Net kesim tarihi; bakiyeler bağımsız kaynakla (banka ekstresi, sayım, cari mutabakatı) doğrulanır; Excel toplamına tek başına güvenilmez |
| Excel'in kendisinde hata (yanlış formül, kopuk bağlantı, sabit değer) | Hatayı ERP'ye taşımak | Tutarsız formül tespiti; müşteriye "bu hata mı, istisna mı" sorusu |
| Serbest metin/birleştirilmiş hücre/biçim tutarsızlığı | Otomatik aktarım başarısız | Temizleme kuralları, ret günlüğü, sahibin düzeltmesi |
| Hassas veri sızıntısı | Hukuki/ticari zarar | §3.2 kuralları, maskeleme, erişim kısıtı |
| Geçiş sırasında canlı işin aksaması | İş durur | Donma penceresi, paralel çalışma, geri dönüş planı |
| Kullanıcı direnci / Excel'e dönüş | ERP boş kalır | §5.2, eğitim, erken katılım (dosya sahibi UAT'de) |
| Makro içine gömülü iş kuralları | Gözden kaçar | oletools ile çıkarım, makro başına kural kartı |

## 7. Firmadan istenecekler listesi **[ÖNERİ]**

**Dosyalar**
- Tüm Excel dosyalarının **güncel sürümleri** (kopya/eski sürümler "arşiv" etiketiyle ayrı); dosya adlarını değiştirmeden.
- Mümkünse **örnek dolu bir dönem** (ör. son kapanmış hakediş/ay) ve aynı dönemin Excel'den üretilmiş çıktıları (rapor, hakediş, özet).
- Dosyaların paylaşılma yöntemi: müşterinin onayladığı güvenli kanal; teslimde dosya listesi (ad, tarih, boyut) ile birlikte. Hassas kısımlar (kimlik, IBAN, maaş) için maskeleme/çıkarma seçeneği konuşulur.
- Dosyaların dışında kullanılan başka kayıtlar: e-posta eki tablolar, WhatsApp'tan gelen Excel'ler, kâğıt defterler, PDF cetveller.

**Görüşmeler**
- Her dosyanın **sahibiyle kısa görüşme** (30–45 dk): dosyayı ne için, ne sıklıkla, kimden aldığı veriyle güncelliyor; hangi hücreler elle girilir; hangi formüller "dokunulmaz"; bilinen hatalar/istisnalar.
- **Hangi raporlar Excel'den üretiliyor**: kime gidiyor (sahipler, idare/kurum, banka, mali müşavir), hangi sıklıkta, hangi biçimde; ERP'nin bu çıktıları üretmesi gerekir.
- Hakediş, poz/birim fiyat ve sözleşme dosyalarının hangi kamu kurumu cetveli/yılı ile hazırlandığı.
- Excel'de uygulanan kesinti/oran/sabitler (KDV, stopaj, teminat, fiyat farkı) ve kaynağı.

**Kararlar**
- Taşınacak tarihsel dönem, açılış bakiyesi tarihi, cut-over için uygun dönem (ör. ay/hakediş sonu), paralel çalışma süresi, UAT'de yer alacak kişiler.

## Açık sorular
Segment düzeyinde açık sorular:
1. Bu segmentte Excel dosyalarının envanteri genellikle nasıl çıkarılır; kopya/eski sürümlerden hangisinin "gerçek" sürüm olduğu nasıl belirlenir?
2. Dosyalar hangi güvenli kanalla ve hangi hassasiyet koşuluyla (maskeleme gerekir mi) paylaşılır? Dosyaların bulut tabanlı servislere yüklenmemesi konusunda hangi kısıtlar yaygındır?
3. Son kapanmış dönemin (ay/hakediş) dolu örnek dosyaları ve Excel'den çıkan raporlar nasıl sağlanır?
4. Dosyalarda makro ve başka dosyalara bağlantı (ağ klasörü, başka çalışma kitabı) ne kadar yaygındır?
5. Formülü yalnızca bir kişinin bildiği dosya/sayfa durumu ne sıklıkla görülür; bu kişilerle görüşme nasıl planlanır?
6. Excel'den üretilip dışarıya (idare, banka, müşavir, yöneticiler) giden raporlar hangileridir; biçimleri zorunlu mu?
7. Tarihsel veriden ne kadarının ERP'ye taşınması gerekir (yalnızca aktif projeler mi, son N yıl mı, tümü mü)?
8. Açılış bakiyeleri (cari, kasa/banka, stok, devam eden projeler) hangi tarih ve hangi doğrulama kaynağıyla kurulur?
9. Geçiş döneminde Excel ve ERP'nin paralel çalışması için ne kadar süre ve hangi kapanış döngüsü uygundur?
10. Kabul testini (UAT) kimler yapar ve ne kadar zaman ayırabilir?
11. Personel/maaş gibi kişisel veri içeren dosyalar taşınmalı mı?

## Açık noktalar / riskler
- **Gerçek dosya henüz analiz edilmedi**: tüm şablonlar varsayımsaldır; dosyalar geldiğinde alan sayısı, makro kullanımı ve kalite düzeyi plan süresini belirgin değiştirebilir [BELİRSİZ].
- **Araç bilgileri**: bakım/lisans bilgileri PyPI'den doğrulandı (§3.1); olevba'nın .xlsb desteği, oletools PyPI/GitHub sürüm farkı ve pandas/xlrd bilgileri doğrulanmadı. Araç seçimi kullanıcı kararıdır. pycel güvenlik açığı nedeniyle listeden çıkarıldı.
- **Mevzuat bağlantılı kurallar** (hakediş kesintileri, KDV/stopaj, poz fiyatları): bu belge doğrulamaz; ilgili araştırma dosyalarına ve müşteri doğrulamasına bağlıdır.
- **KVKK / saklama süresi**: personel verisi ve tarihsel belgelerin taşınması/saklanması için hukuki görüş gerekebilir [BELİRSİZ].
- **Süre/emek tahmini yok**: dosya envanteri tamamlanmadan güvenilir efor tahmini yapılamaz.
- **Excel hatasını taşıma riski**: Excel'deki mevcut sonuç "doğru" varsayılmamalı; mutabakatta fark çıkması Excel'in hatalı olduğu anlamına da gelebilir, kararı müşteri verir.
