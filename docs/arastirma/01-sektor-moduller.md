# 01 — Sektör Modülleri: Kamu Yapım İşi Yürüten Taahhüt Firması ERP İhtiyaçları

> Belge numaraları (00–13), karar numaraları (K-xx, D-xx) ve "pilot keşif" kavramı için: [ARASTIRMA-OZETI.md](../ARASTIRMA-OZETI.md#bu-belgeler-nasıl-okunur).

Hazırlayan: Araştırma agent A · Tarih: 18 Kasım 2026 · Durum: ilk tur, müşteri onayı yok.
Etiketler: **[GEREKSİNİM]** pilot keşifte açıkça söylenen · **[ÖNERİ]** araştırmaya dayalı öneri · **[BELİRSİZ]** netleşmeli.
Kaynak kodları (K1…) dosya sonundaki "Kaynaklar" bölümünde.

## Özet
1. Kamu yapım işinin omurgası: ihale → sözleşme (+kesin teminat) → iş programı → aylık hakediş → geçici kabul → teminat süresi → kesin kabul → iş deneyim belgesi. ERP'nin tek "sözleşme/iş" kaydı etrafında bu zinciri tutması gerekir. **[ÖNERİ]**
2. Pilot keşifte açıkça anılan alanlar: kullanıcı/yetki, proje-ihale, malzeme/ekipman/demirbaş takibi, proje maliyeti ve raporlar, poz/birim fiyat, muhasebe/e-Fatura/hakediş, Excel aktarımı, belge okuma, web sitesi. Taşeron, personel, teminat mektubu, saha raporu pilot keşifte **yok**. **[GEREKSİNİM]**
3. Piyasada "standart" sayılan çekirdek: sözleşme, iş kırılımı/bütçe, hakediş, satın alma, stok/depo, maliyet kontrol, taşeron, cari/finans, raporlama. Yerli ürünlerin çoğu bunu genel ERP üzerine sektör paketi olarak sunuyor (K11, K13).
4. Teminat mektubu takibi (vade, uzatma, iade) incelediğim yerli ürün tanıtımlarında açıkça yer almıyor; hem sektör acı noktası hem farklılaştırıcı aday olabilir (kanıt mevzuattan türetilmiş; pilot keşifte doğrulanmalı). **[ÖNERİ]** (kapsamlı ürün taraması yapılmadı)
5. Teminat süreci 2024–2026'da kademeli elektronikleşti (Takasbank/EKAP): 8.4.2024 (kesin teminat), 5.1.2026 (sözleşme süreci teminatlarında elektronik düzenleme imkânı), 1.4.2026 ve sonrası ilanlı ihaleler (KİK 2026/DK.D-88). Kâğıt/elektronik ayrımı ERP teminat kaydında alan olmalı. **[ÖNERİ]**
6. Küçük ekipli (ör. 5–50 kullanıcı) bir firma için MVP önerisi: proje/sözleşme, iş kırılımı+bütçe, satın alma→stok, saha günlüğü, taşeron hakedişi (basit), teminat takibi, maliyet-hakediş paneli. Ekipman/İK ayrıntısı ve ileri planlama sonraya. **[ÖNERİ]**
7. Sektörde ERP'ye dirençin ana kaynağı "çok detaylı veri girişi" algısı (K12) → sade, özet-giriş odaklı arayüz hem pilot keşifteki hedefle hem sektör geri bildirimiyle uyumlu.

## 1. İş akışı ve her adımda ERP'nin tutacağı veri

| Adım | Ne olur (kısaca) | ERP'nin tutması gereken veri | Not / bağlantı |
|---|---|---|---|
| İhale takibi | İlanlar EKAP'tan izlenir; ilgi duyulan işler elenir | İKN, idare, iş adı, yaklaşık maliyet (biliniyorsa), ihale tarihi, karar (gir/girme), sorumlu | EKAP için belgelenmiş resmî veri API'si bulunmadı (yokluk bağımsız incelemede de teyit edildi); topluluk istemcileri belgelenmemiş uç noktalar kullanıyor (K21). Otomatik çekme ve kullanım koşulları/kazıma yasağı KİK'e sorulmalı **[BELİRSİZ]** |
| Teklif hazırlama | Yaklaşık maliyete/keşfe göre teklif birim fiyat veya götürü bedel teklif; açık ihalede e-teklif | Teklif cetveli (poz, miktar, birim fiyat), maliyet analizi, iskonto/katsayı, geçici teminat (teklif edilen bedelin ≥%3'ü, K1 m.33), sonuç | Poz/birim fiyat → **02**. Küçük ölçekli açık ihalelerde e-teklif zorunluluğu (K22) |
| Geçici teminat | Teklifle birlikte; mektup vadesi teklif geçerlilik süresinden ≥30 gün uzun (K1 m.35). e-Geçici teminat Takasbank platformu üzerinden 1.9.2021'den beri alınabiliyor (K22); zorunluluk tarihi doğrulanmadı | Mektup no, banka, tutar, vade, ihale, iade durumu, elektronik/kâğıt, Takasbank referans no | Teminat modülü, bkz. §2 |
| Sözleşme | Kesin teminat sonrası imza: ihale bedelinin %6'sı; teklif sınır değerin altındaysa Kurum yaklaşık maliyetin %6'sından az, %15'inden çok olmamak üzere oran belirleyebilir (K1 m.43; K4'te %9 ifadesi var, sözleşmeden doğrulanmalı). Sözleşme öncesi kesin teminat 8.4.2024'ten beri ilanlı ihalelerde elektronik (KİK 2024/DK.D-56; K9, ikincil) | Sözleşme bedeli, tarihler, süre, ödeme/avans, gecikme cezası oranı, fiyat farkı hükmü, kesin teminat mektubu (elektronik/kâğıt, Takasbank ref.), YAMBİS yetki belgesi no (K5) | Mektup vadesi kesin kabulü kapsayacak şekilde belirlenir (K1 m.35; K3) |
| İş programı | Yer tesliminden sonra sunulur, onaylanınca hakedişe esas olur; revizyonu olur (K10) | Aylık planlanan ilerleme/ödenek dağılımı, onaylı sürüm, revizyon tarihçesi | Süreler eski kaynağa dayanıyor; YİGŞ 2024–25'te değişti, sözleşmeden doğrulanmalı **[BELİRSİZ]** |
| Şantiye yürütme | Defter ve tutanaklar (puantaj, ataşman, yeşil defter, şantiye defteri) (K10) | Günlük rapor, metraj/ataşman, imalat miktarları, fotoğraf, puantaj | §2 saha modülü |
| Hakediş | Aylık; kesintiler ve avans mahsubu (K2) | İmalat miktarı × sözleşme birim fiyatı, yeşil defter, kesinti kalemleri, fiyat farkı, onay durumu | Hesap mantığı → **02**; vergi/e-Fatura → **03** |
| Geçici kabul | İşin kullanıma hazır hale geldiği tarihte komisyonla | Kabul tarihi, noksan listesi, tutanak (taranmış), kesin teminat iadesinin yarısı (K4) | Teminat süresi başlar (genelde 12 ay, sözleşmeye bağlı) (K3) |
| Teminat süresi / kesin kabul | Bakım-onarım dönemi; sonra kesin kabul | Süre bitiş tarihi, noksanlar, kalan teminatın iadesi (SGK ilişiksizliği şartıyla) (K4) | Mektup vade uzatması gerekebilir (K3) |
| İş deneyim belgesi | Kabul sonrası idare düzenler, EKAP'a kaydedilir | İş bitirme belgesi tutarı, tarihi, benzer iş niteliği; başvuru dosyası (sözleşme, kabul tutanağı, hakediş raporları) | Yapım işleri için tam kural teyit edilmedi; benzer hüküm KÖİ tebliğinde görüldü (K7). **[BELİRSİZ]** |

Not: Genel Tebliğ'de 16 Ekim 2026'da yapılan değişiklikle SGK/vergi borcu eşiği 5.000'den 50.000 TL'ye çıktı; yürürlük 15 Kasım 2026 (K6). Teklif evrak kontrol listesi bundan etkilenebilir; kontrol/hatırlatma özelliği için girdi.

## 2. Modül bazlı tipik ihtiyaçlar ve MVP görüşü

(MVP = küçük ekipli firma, ilk sürüm. "MVP görüşü" sütunundaki "evet" ifadeleri öneridir, karar değildir; [ÖNERİ] etiketli modüllerde müşteri onayına bağlıdır.)

| Modül | Tipik ihtiyaç | Etiket | MVP görüşü |
|---|---|---|---|
| Kullanıcı/yetki | Rol + proje bazlı erişim | **[GEREKSİNİM]** | Evet |
| Proje/ihale | İhale→proje, sorumlu, aşama, ilerleme, ihale takip listesi | **[GEREKSİNİM]** (proje, ihale) | Evet; EKAP otomatik çekme sonraya **[BELİRSİZ]** |
| İş kırılımı (WBS) + aşama | Sözleşme pozları ↔ iş kalemleri ↔ bütçe aynı ağaçta | **[GEREKSİNİM]** (aşama) / **[ÖNERİ]** (poz bağı) | Evet, çekirdek |
| Satın alma | Talep→teklif→sipariş→irsaliye→fatura, projeye/iş kalemine bağlı | **[GEREKSİNİM]** (malzeme takibi) / **[ÖNERİ]** (tam zincir) | Evet, sade; teklif karşılaştırma tek ekran |
| Stok/depo | Şantiye depoları, depolar arası transfer, direkt-şantiyeye-sarf | **[ÖNERİ]** | Evet, basit hareket bazlı |
| Saha | Günlük şantiye raporu, puantaj, metraj, fotoğraf; mobil/çevrimdışı | **[ÖNERİ]** | Evet (günlük rapor + metraj + fotoğraf); gelişmiş kalite formları sonra |
| Ekipman/demirbaş | Kendi/kiralık makine, yakıt, bakım, zimmet | **[GEREKSİNİM]** (ekipman, demirbaş) | Basit kayıt + zimmet + yakıt/saat; bakım planı sonra |
| Taşeron | Sözleşme, taşeron hakedişi, kesintiler (teminat, SGK, avans), ödeme | **[ÖNERİ]** | Evet, sade. Asıl yüklenici işçi alacağı/prim için müteselsil sorumlu (K20) → SGK/prim belgesi kontrol listesi |
| Personel/puantaj | Saha puantajı → maliyete aktarım; SGK/İSG yalnız ERP'ye dokunan kısım (çalışan–proje ataması, belge/eğitim bitiş tarihi) | **[ÖNERİ]** | Puantaj evet; bordro/İSG süreci kapsam dışı önerisi **[BELİRSİZ]** |
| Proje maliyeti | Bütçe vs gerçekleşen (aşama/kalem), hakediş geliri vs maliyet, nakit akışı | **[GEREKSİNİM]** | Evet, ana değer önerisi |
| Hakediş | Yeşil defter, icmal, kesintiler, fiyat farkı | **[GEREKSİNİM]** | Evet (detay **02**) |
| Teminat mektubu/banka | Mektup kaydı (elektronik/kâğıt, Takasbank ref. no), vade/uzatma/iade uyarısı, banka limiti, komisyon | **[ÖNERİ]** | Öneri: evet, hafif (müşteri onayına bağlı); banka entegrasyonu hayır |
| Muhasebe/e-Fatura | Cari, kasa/banka, resmî defter | **[GEREKSİNİM]** (geniş, kapsam açık) | Kapsam kararı **03**'e bağlı **[BELİRSİZ]** |
| Belge okuma | Fiş/fatura → veri, onay akışı | Otomatik işleme **[GEREKSİNİM]**; PDF/fotoğraf yöntemi **[BELİRSİZ]** (müşteri teyidi yok) | Sonraki faz önerisi; **05**'e bağlı |
| Raporlama/panel | Sahipler için özet panel, proje bazlı raporlar | **[GEREKSİNİM]** | Evet |
| İş programı/planlama | Aylık ilerleme planı, sapma | **[ÖNERİ]** | Sade aylık çizelge evet; CPM/Gantt sonra. Sektör rehberi, ERP'nin Primavera/MS Project yerini tutmadığını belirtiyor (K12, 2015) |
| İş deneyim arşivi | Belge/kabul/hakediş dosyası derleme | **[ÖNERİ]** | Kolay kazanım: belge deposu + alanlar |
| Web sitesi | CMS | **[ÖNERİ]** | ERP dışı (ayrı iş) |

## 3. Türkiye'deki inşaat odaklı yazılımlar (kısa liste)

Derin karşılaştırma **04**'te. Fiyatların hiçbiri açık değil, çoğu demo/teklif ile.

| Ürün | Odak | Fiyat modeli | Kaynak / durum |
|---|---|---|---|
| Uyumsoft İnşaat ERP (Liox ERP) | Genel ERP + sektör paketi: sözleşme, zaman (MS Project/Primavera), maliyet kontrol (yapım bütçesi kırılımı), hakediş (yeşil defter icmali Excel'den aktarım), teklif, Revit metraj, imalat kalite | Açık değil (demo) | K11 (satıcı sayfası) |
| Parsek Solutions | ERP (finans, İK, satın alma, stok, depo, proje, şantiye) + İSG + OSB | Açık değil | K13 (haber; ikincil, satıcı iddiası) |
| Muhasorex | Açık hesap/cari + müteahhit programı: şantiye bazlı maliyet, tedarikçi borcu | Açık değil | K14 (tanıtım haberi; ikincil) |
| AMP Hakediş / Yaklaşık Maliyet | Hakediş, yaklaşık maliyet, fiyat farkı (TÜİK verisi otomatik çekilir iddiası), sözleşme/kabul/tasfiye modülleri; ERP değil | Açık değil (deneme sürümü varmış) | K16 (satıcı + yan siteler; ikincil) |
| PoinWork | Şantiye puantaj/maaş/finans; çevrimdışı yerel veritabanı | Açık değil | K17 (satıcı sayfası; menşei doğrulanmadı) |
| CANIAS ERP | Üretici inşaat sayfasına göre BOQ/keşif–satın alma–hakediş–taşeron bağı, bütçe vs gerçekleşen; derinliği ve mobil/çevrimdışı desteği doğrulanmadı; fiyat yok. Detay **04** | Açık değil | K23 (üretici iddiası, bağımsız kanıt yok) |
| Logo, Netsis, Mikro vb. | Genel ERP; incelediğimde kendi inşaat/hakediş modülü kanıtı bulamadım | — | K18; **[BELİRSİZ]** |
| Tanıtım haberi: yapay zekâ destekli yerli inşaat platformu (adı belirtilmemiş) | ERP+BIM+dijital ikiz; satın alma, stok, hakediş, taşeron, doğal dil sorgu | Yok | K15 (isimsiz haber; doğrulanmadı) |

Not: Önceki taslakta CANIAS için "kanıt bulunamadı" yazmıştım; bu yanlıştı, üretici sayfası inşaat/hakediş paketini anıyor (04 ile uyumlu).

Sonuç: Yerli piyasada hakediş yazılımları (AMP gibi) ile ERP'ler ayrı yaşıyor; iki dünyayı birleştirmek açık alan gibi görünüyor, ancak tam piyasa taraması yapılmadı.

## 4. Piyasada "standart" kabul edilen modüller

Çapraz kaynak (K11, K12, K13, K14): sözleşme yönetimi · proje/iş kırılımı + bütçe · satın alma/teklif · stok/depo · hakediş · taşeron/tedarikçi cari · maliyet kontrol (planlanan–gerçekleşen) · finans/muhasebe · İK/puantaj · döküman yönetimi · raporlama. Sektör rehberine göre ERP'lerde satın alma, muhasebe, İK, makine bakım alanları sorunsuzdu; ayırt edici olan proje yönetimi ve maliyet kontrol yeteneğiydi (K12, 2015, eski veri).
Daha az standart: teminat mektubu/limit takibi, iş deneyim arşivi, EKAP ihale takibi **[ÖNERİ]**.

## 5. "Bizi öne atacak" fikirler

| Acı noktası | Kanıt | Sade çözüm önerisi |
|---|---|---|
| Hakediş ile maliyet kopuk: gelir poz birim fiyatıyla, gider fatura/irsaliye ile izleniyor | Maliyet kontrolün yapım bütçesi kırılımına bağlanması vitrin özelliği (K11); aktivitelere poz analiziyle kaynak atamanın hazır olmadığı gözlemi (K12, 2015) | Tek iş kalemi ağacı: her hakediş satırı = bir iş kalemi = bütçe + fiili maliyet. "Bu ay hakedişle alınan X, harcanan Y" tek ekran. **[ÖNERİ]** |
| Teminat mektubu vadesi/iadesi | Mektup vadesi kesin kabulü kapsamalı, gecikmede uzatılır; uzatma yeni mektup+eskisinin iadesi (K1, K3, e-teminat tebliği ikincil); yarısı geçici, kalanı kesin kabulde iade (K4) | Mektup defteri: 60/30/7 gün uyarı, uzatma geçmişi (yeni/eski mektup), kesin kabul tarihine bağlı kontrol, banka limit kullanımı. **[ÖNERİ]** |
| Şantiyeden geç/eksik veri | Saha–ofis kopukluğu ve gecikmeli veri yaygın sorun; kaynaklar yabancı ve satıcı kaynaklı (K19, ikincil) | Telefondan 1 dakikalık günlük rapor (hava, kadro, ekipman, yapılan iş, fotoğraf), zayıf sinyalde çevrimdışı kuyruk; eksik rapor günü uyarısı. **[ÖNERİ]** |
| İş programı sapması ve ceza riski | Onaylı programa uyum fiyat farkını ve cezayı etkiler (K10, 2020); günlük gecikme cezası sözleşmede (K2) | Planlanan vs gerçekleşen kümülatif ilerleme; "bu hızla bitiş tarihi" ve tahmini ceza. **[ÖNERİ]** |
| Taşeron ödeme riski | Asıl yüklenici müteselsil sorumlu; SGK/prim belgeleri hakediş eki olabilir (K20, ikincil) | Taşeron hakedişinde belge kontrol listesi: eksikse ödeme onayı uyarısı. **[ÖNERİ]** |
| Bilgi kişiye bağlı, ofis–şantiye dağınık | TMB ERP komitesi tespiti (K12, 2015) | Belgeler (sözleşme, tutanak, kabul) ilgili kayda bağlı, aranabilir. **[ÖNERİ]** |
| ERP'ye direnç ("çok veri girişi") | K12 | Excel'den içe aktarma ile başlama (rakipte de Excel icmal aktarımı var, K11), zorunlu alan azaltma. **[ÖNERİ]** |
| Sonraki ihale için hazır dosya | İş deneyim başvurusunda sözleşme+kabul+hakediş istenir (K7) | Kesin kabulde "iş deneyim dosyası" otomatik derleme. **[ÖNERİ]** |

## Açık sorular
Segment düzeyinde açık sorular (pilot keşifte ve ek görüşmelerle netleşecek):
1. Bu segmentteki firmalar aynı anda kaç proje yürütür; götürü bedel ile birim fiyat işlerinin oranı nedir; yıllara yaygın iş ne kadar yaygındır?
2. Teminat mektupları çoğunlukla hangi kanaldan ve nasıl izlenir (limit, komisyon, vade)? Kaçırılan vade ne kadar sık yaşanır?
3. Taşeron kullanımı ne kadar yaygındır; taşeron sözleşme, hakediş ve kesintileri nasıl yönetilir? Saha–ofis veri akışı hangi araçlarla (mesajlaşma, kâğıt) yürür?
4. Şantiyelerde internet ve cihaz (telefon/tablet) durumu nasıldır; günlük rapor kim tarafından, nasıl yazılır?
5. Kendi makine parkı ile kiralık ekipman oranı nedir; yakıt/bakım takibi ne ölçüde beklenir?
6. Bordro içeride mi, dışarıda mı yürür; ERP'den beklenti yalnız puantaj mıdır?
7. Teklif aşaması (yaklaşık maliyet, teklif cetveli) ERP kapsamına alınmalı mı, yoksa sözleşmeden mi başlanmalı?
8. İş programı hangi araçlarla (Excel, MS Project, Primavera) yapılır?
9. İş deneyim belgeleri ve ihale takibi kimde ve nerede tutulur?
10. Excel dışında hangi yazılımlar (hakediş programı, metraj aracı vb.) kullanılır; ERP sonrasında hangileri kalır?

## Açık noktalar / riskler
- Yerli ürün taraması geniş değil; fiyat bilgisi yok; ürün sayfaları satıcı beyanı (K11, K13, K14, K17). Derin karşılaştırma **04**.
- e-Teminat kronolojisi (bağımsız incelemede çözüldü, çelişki yok): 8.4.2024 ve sonrası ilanlı ihalelerde sözleşme öncesi kesin teminat yalnız elektronik (2024/DK.D-56, ikincil); 5.1.2026'dan itibaren sözleşme süreci teminatları (ek kesin, avans, kesin hesap, geçici kabul noksanları) Takasbank'tan elektronik düzenlenebiliyor (KİK duyurusu, imkân); ilanı 1.4.2026 ve sonrası ihalelerde bunların elektronik düzenlenmesi esas (Kurul kararı 2026/DK.D-88, 12.03.2026). Hâlâ açık: kararın 1.4.2026 öncesi ilanlı ihalelere uygulanışı ve e-geçici teminatın zorunluluk tarihi (KİK/EKAP kılavuzundan teyit). **[BELİRSİZ]**
- Yapım işlerinde iş deneyim belgesi düzenleme kuralları (süre, EKAP akışı) doğrudan doğrulanmadı; Nisan 2026'da Yönetmeliğe eklenen 22/B maddesini (belge düzenlenemeyen haller) araştırma sonucunda gördüm ama içeriğini ve hangi yönetmelik olduğunu doğrulamadım.
- Hakediş kesinti oranları ve iş programı süreleri ikincil kaynaklara dayanıyor; kamu işlerinde sözleşme/şartname ve güncel YİGŞ (2024–2025 değişiklikleri) esas alınmalı. Ayrıntı **02**.
- Mevzuat değişkendir (Tebliğ 16.10.2026); ERP'de oranlar/süreler sabit kodlanmamalı, parametrik olmalı **[ÖNERİ]**.
- Saha–ofis veri kopukluğu kanıtları yabancı, satıcı kaynaklı; Türkiye için pilot keşifte doğrulanmalı.
- 2015 tarihli TMB rehberi eski; ilkesel bulgular için kullanıldı.
- Teklif/ihale takibi için EKAP'tan otomatik veri çekme resmî olarak belgelenmiş değil; hukuki/teknik risk.

## Kaynaklar
Erişim tarihi hepsi için 18.11.2026.
- K1 Kamu İhale Kanunu 4734 (m.33 geçici teminat ≥%3; m.34–35 teminat mektubu; m.43 kesin teminat %6): https://www.mevzuat.gov.tr/mevzuatmetin/1.5.4734.pdf — (doğrulandı: resmî kaynak; konsolide metnin güncelliği doğrulanmadı)
- K2 Hakediş kesintileri (30.07.2026): https://www.hakedis.org/yapim-islerinde-hakedis-kesintileri-ve-yuklenicilerin-diger-mali-yukumlulukleri/ — (ikincil kaynak)
- K3 Yapım işlerinde teminat süresi (21.10.2024): https://www.hakedis.org/yapim-islerinde-teminat-suresi/ — (ikincil kaynak)
- K4 Teminat ve iadeleri (15.11.2023): https://www.hakedis.org/?p=6358 — (ikincil kaynak)
- K5 YAMBİS/Şantiye-M ve yeterlik (19.01.2026): https://www.hakedis.org/yapi-muteahhitligi-yetki-belgesi-yambis-ve-kamu-yapim-ihalelerinde-yeterlik-kriteri/ — (ikincil kaynak)
- K6 Genel Tebliğ değişikliği, RG 16.10.2026/33402: https://www.alomaliye.com/2026/10/16/kamu-ihalelerinde-sgk-ve-vergi-borcu-siniri-50-bin-tl/ — (ikincil kaynak)
- K7 KÖİ/lisanslı işler iş deneyim tebliği (benzer hüküm): https://alomaliye.com/2020/09/30/kamu-ozel-is-birligi-projeleri-yapim-isleri-is-deneyim-belgeleri/ — (ikincil kaynak; yapım işleri için doğrulanmadı)
- K8 e-teminat, Kurul kararı 2026/DK.D-88: https://www.alomaliye.com/2026/03/18/teminat-mektuplarinda-yeni-duzenleme-ekap-takasbank-elektronik-teminat-sistemi-basliyor/ — (ikincil kaynak)
- K9 Sözleşme süreci teminatları Takasbank (02.01.2026; 5.1.2026'dan itibaren düzenlenebilir, imkân): https://www.hakedis.org/sozlesme-surecine-iliskin-tum-teminatlarin-takasbank-uzerinden-elektronik-ortamda-sunulmasi-zorunlu/ — (ikincil kaynak; URL'deki "zorunlu" ifadesi gövdeyle uyuşmuyor; K8 ile ardışık adım). Karar metni: https://www.alomaliye.com/wp-content/uploads/2026/03/2026-DK-D-88.pdf ; kesin teminat 8.4.2024: https://www.hakedis.org/?p=6779 (ikincil)
- K10 İş programı (26.11.2020) ve defterler: https://www.hakedis.org/?p=3747 ; https://www.alomaliye.com/2018/07/09/insaat-tutulmasi-gereken-defterler/ — (ikincil kaynak, eski)
- K11 Uyumsoft İnşaat ERP: https://uyumsoft.com/insaat-erp ; e-kitap https://uyumsoft.com/assets/e-book/insaat-sektoru-erp-kullanimi.pdf — (satıcı kaynağı)
- K12 TMB ERP Komitesi "İnşaat Sektöründe ERP Kullanımı" (2015): https://www.tmb.org.tr/uploads/publications/6065b65e4e2c483e72ff8fe4/1617278550162-erp-icg-r-2.pdf — (ikincil kaynak, eski; sektör kuruluşu)
- K13 Parsek Solutions (Cumhuriyet, 23.07.2026): https://www.cumhuriyet.com.tr/is-dunyasi/erp-isg-ve-osb-surecleri-tek-veri-yapisinda-bulusuyor-2523317 — (ikincil kaynak)
- K14 Muhasorex (04.06.2026): https://www.habergazetesi.com.tr/muhasorexcom-ile-alacaklar-sahaya-iniyor — (ikincil kaynak, tanıtım)
- K15 İsimsiz yerli yapay zekâlı inşaat platformu haberi (31.07.2026): https://www.gazetebirlik.com/teknoloji/insaat-projelerinde-dijital-donusum-hizlandi-yerli-yazilimla-surecler-saniyelere-indi/1054494 — (doğrulanmadı)
- K16 AMP Yazılım: https://www.ostim.org.tr/amp-software-industry-and-trade-ltd-sti ; https://www.hakedis.org/?p=1246 — (ikincil kaynak; site AMP ürünlerini tanıtıyor, satıcı içeriği olabilir)
- K17 PoinWork: https://sites.google.com/view/poinwork/home — (satıcı kaynağı, menşei doğrulanmadı)
- K18 Logo Netsis (genel ERP): https://logo.com.tr/en/product/logo-netsis-wings — (satıcı kaynağı)
- K19 Saha–ofis veri kopukluğu (yabancı, satıcı/sektör yayını): https://www.contractormag.com/management/best-practices/article/55374079/closing-the-gap-between-the-jobsite-and-the-balance-sheet — (ikincil kaynak)
- K20 Alt yüklenici/SGK: https://www.kazimceylan.av.tr/md/alt-yuklenici-sozlesmesi ; https://www.alomaliye.com/2008/10/30/sgk-genelgesi-200888-prim-ve-idari-para-cezasi-borclarinin-hakedislerden-mahsubu-odenmesi-ve-ilisiksizlik-belgesinin-aranilmasi-hk — (ikincil kaynak; güncelliği doğrulanmadı)
- K21 EKAP istemci örneği (resmî API değil): https://glama.ai/mcp/servers/@saidsurucu/ihale-mcp/blob/fbbb8848352ed1e7657080d2819ec2fe836c5c58/ihale_client.py — (doğrulanmadı)
- K23 CANIAS inşaat çözümü: https://canias.com/en/erp-for-construction-companies — (üretici iddiası)
- K22 e-teklif zorunluluğu / e-GTM: https://hukukcularevi.com/elektronik-ihale-ekap-ve-e-teklif/ ; https://www.hakedis.org/?p=5357 — (ikincil kaynak)
