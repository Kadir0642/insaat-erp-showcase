# Araştırma Özeti (Yönetici Özeti)

> 18.11.2026 · Aşama 0 (araştırma; ERP için kod yok — D-01; yardımcı Excel analiz aracı ve görüşme paketi hazırlandı — D-06, D-07) · Kaynak: [araştırma 01–07](arastirma/) + bağımsız incelemeler [R1, R2, R3](arastirma/inceleme/). Çelişkilerde incelemenin çözümü esas alındı. Belge numaraları (00–13), karar numaraları (K-xx, D-xx) ve "pilot keşif" kavramı için sondaki [Bu belgeler nasıl okunur](#bu-belgeler-nasıl-okunur) bölümüne bakın.
> Etiketler: **[GEREKSİNİM]** pilot keşifte ifade edilen ihtiyaç · **[ÖNERİ]** araştırmaya dayalı, onaysız · **[BELİRSİZ]** netleşmeli. "→ 02 §4" = kaynak dosya ve bölüm.

## Sizden beklenen kararlar (düz özet)

- **Pilot firmayla keşifte:** ilk sürümde ne olacak (K-03); muhasebe ERP'de mi, mali müşavirde mi kalacak (K-05); resmî poz fiyatları nasıl edinilecek (K-07); veriler Türkiye'de mi tutulacak (K-06).
- **Sizin:** teknoloji yığını ve barındırma (K-04). Yaklaşım (kendi yazılımımız) karara bağlandı (D-05).

**Kısa sözlük:** YFK = birim fiyatları yayımlayan Bakanlık kurulu · YİGŞ = hakediş kurallarını içeren genel şartname · ATGB = anahtar teslimi götürü bedel · GİB = Gelir İdaresi · entegratör = e-Faturayı GİB'e ileten lisanslı firma · SMMM = mali müşavir · çok kiracılık = aynı sistemi birden çok firmaya güvenle sunabilme · MVP = ilk kullanılabilir sürüm.

## Projeyi şekillendiren 12 kritik bulgu

| # | Bulgu | Etkisi | Durum |
|---|---|---|---|
| 1 | Bu segmentteki firmaların önemli kısmı süreçlerini Excel'le yürütür *(varsayım)*; Excel'den geçiş ürünün ana iş paketlerinden biridir **[GEREKSİNİM]** | Kapsam ve tahmin, gerçek dosyalar analiz edilmeden kesinleşmez. En büyük risk belgelenmemiş formül bilgisi **[ÖNERİ]** (→ 07) | Pilot keşif + öneri |
| 2 | Yüklenici için asıl veri sözleşmenin kendisi: teklif cetveli, metraj, yeşil defter, kesintiler (→ 02 Özet 4) | Resmî katalog olmadan sözleşme kalemleriyle hakediş yapılabilir **[ÖNERİ]** | Öneri |
| 3 | YFK erişim beyanı birim fiyatların yazılım/veri tabanında izinsiz kullanımını yasaklıyor (FSEK); resmî API/XML **bulunamadı** (→ 02 §2) | Toplu poz aktarımı hukuk görüşü/lisans olmadan yapılmamalı; pilot keşifteki poz talebiyle gerilim **[BELİRSİZ]** | Yasak: doğrulandı (resmî; R1). API yokluğu: doğrulanmadı |
| 4 | 30.07.2025 hakediş değişiklikleri yalnız 01.09.2025 ve sonrası ilanlı ihalelere uygulanır (→ 02 §4) | Her sözleşmede "ilan tarihi → kural sürümü"; oranlar sabit kodlanmaz **[ÖNERİ]** | İkincil, R1 teyitli |
| 5 | Fiyat farkı F = An × B × (Pn − 1); KİK 2026/DK.D-332, TÜFE 2003=100'e atıf yapan sözleşmelerde TÜFE 2025=100 değerlerini esas alıyor; İo yorumu açık (→ 02 §5) | MVP'de elle endeksli "kontrol hesabı"; resmî tutar idarenindir | Karar metni okundu (ikincil kopya) |
| 6 | Ulusal e-hakediş kanalı ve EKAP yüklenici API'si bulunamadı (→ 02 §6, 01 §1) | Hakediş çıktısı Excel/PDF, teslim elle | Doğrulanmadı (yokluk) |
| 7 | e-Fatura büyük olasılıkla zorunlu (inşa 500 bin TL / genel 3 M TL); bilanço esasında e-Defter 2025'ten beri zorunlu; doğrudan GİB bağlantısı küçük firmaya uygun görünmüyor **[BELİRSİZ]** (→ 03 §1–2) | e-Fatura özel entegratör API'siyle, soyutlama katmanıyla **[ÖNERİ]** | Kısmen: eşikler ikincil kaynakla teyit (RG aktarımı; R1); "inşa" ibaresinin yükleniciyi kapsaması yorum; SMMM teyidi |
| 8 | Muhasebe üç seçenek: A ön muhasebe, B = A + entegratörle e-Fatura (03'ün önerisi), C tam resmî muhasebe + e-Defter (→ 03 §7) | K-05 hem kapsamı hem teknik yolu değiştirir **[BELİRSİZ]** | Öneri |
| 9 | Yıllara yaygın inşaat GVK 42–44; yer teslimi/geçici kabul tarihleri yöntemi belirler; KDV tevkifatı 4/10, stopaj %5 (→ 03 §3–4) | Tarihler zorunlu alan; kesintiler tarih aralıklı parametre | Çoğu ikincil, R1 tutarlı |
| 10 | e-Fatura XML'i OCR'sız okunur; Google/AWS fatura ayrıştırıcıları Türkçe desteklemiyor, Azure destekliyor; Türkçe fiş başarımı verisi yok (→ 05 §1–2) | Önce XML + elle giriş; PDF/fotoğraf okuma pilot sonrası, pilot keşifte teyitsiz **[BELİRSİZ]** | Doğrulandı (resmî; R2) |
| 11 | Teknik yaklaşım: kendi yazılımımız, hazır açık kaynak ERP temeli yok (D-05); yığın önerisi TypeScript + PostgreSQL; müşteri yasal defter ve e-Defter'i ERP içinde isterse yeniden değerlendirilir (→ 06 §1.3, [Teknik alternatifler](TEKNIK-ALTERNATIFLER.md)) | Karşılaştırma puanları ölçülmemiş değerlendirmedir; yığın ve barındırma açık | Karar (yaklaşım) + öneri (yığın) |
| 12 | e-belge/e-Defter asıl muhafazası Türkiye'de; AB barındırma KVKK yurt dışı aktarımı; saklama 10 yıl esas (→ 06 §4, 03 §6) | Barındırma K-06'ya bağlı; 03 Türkiye'yi, 06 "zorunlu değilse AB"yi öneriyor | Doğrulandı (KVKK, AWS; R1/R2) |

Ek gözlem **[ÖNERİ]**: teminat mektubu takibi sınırlı taramaya göre yerli ürün tanıtımlarında görünmüyor; acı noktası olduğu pilot keşifte doğrulanmalı (→ 01 Özet 4).

## Teknik beklentiler **[ÖNERİ]** (ayrıntı → 12, 06 §6–8)

| Beklenti | Önerilen hedef |
|---|---|
| Performans | Ekran p95 < 500 ms; 25 eşzamanlı kullanıcıda korunur; k6 ile yük testi |
| Yedek | RPO ≤ 15 dk, RTO ≤ 4 saat; aylık otomatik geri yükleme testi |
| 5–10 yıl okunabilirlik | 10 yıl + istisnalar saklama; yıllık CSV/Parquet + PDF/A arşiv; "tüm verimi indir" |
| Güvenlik | OWASP ASVS 5.0 Seviye 2; sahip/yöneticiye 2FA; rol × proje yetkisi |

## Doğrulanmış / doğrulanmamış

**Resmî kaynakla doğrulanan:** YFK erişim beyanı; GİB'de 95 entegratör; KVKK 5 iş günü bildirimi; Odoo e-Fatura/e-Arşiv/e-İrsaliye modülleri Community/LGPL-3; Frappe MIT; AWS İstanbul Local Zone (RDS yok); belge servislerinin dil desteği; 4734 teminat oranları.

**İkincil, teyit gereken:** e-Fatura eşikleri; YİGŞ md. 22/39/40 süreleri; kesinti ve stopaj oranları; e-teminat kararları; bulut fiyatları.

**Açık:** Odoo e-Defter Community'de mi (R1/R2 farklı); Karar 10132 geçiş kuralı; KGM/DSİ/İLBANK 2026 listeleri; hakedişte damga; entegratör gelen-fatura API'leri; Türkçe fiş doğruluğu; fiş fotoğrafının ispat değeri.

## Bu belgeler nasıl okunur

- **Pilot keşif:** ürünün gereksinim keşfinin yürütüldüğü pilot firmayla yapılan görüşmeler ve notları. Notlar pilot firmaya ait olduğu için özeldir ve bu depoda yer almaz. **[GEREKSİNİM]** etiketi, pilot keşifte ifade edilen ihtiyaç demektir.
- **"Kullanıcı":** bu belgelerde projenin ürün sahibi; ERP'nin son kullanıcısı değil.
- **R1–R3:** bağımsız inceleme raporları ([arastirma/inceleme](arastirma/inceleme/)). **R1–R20** ise yalnızca [RISKLER.md](RISKLER.md) içindeki risk numaralarıdır.
- **Kaynak kodları:** araştırma dosyalarındaki [K1], Ü1, D1, B1 gibi kodlar o dosyanın sonundaki kaynak listesine gider; karar numaraları (K-03 gibi, tireli) bunlarla karıştırılmamalıdır.

### Belge numaraları

Belgeler arasındaki kısa atıflar ("→ 02 §4", "→ 11") bu numaralara göredir.

| No | Belge | İçerik |
|---|---|---|
| 00 | [ARASTIRMA-OZETI.md](ARASTIRMA-OZETI.md) | Bu belge: yönetici özeti |
| 01 | [arastirma/01-sektor-moduller.md](arastirma/01-sektor-moduller.md) | Sektör modülleri ve iş akışı |
| 02 | [arastirma/02-poz-birim-fiyat-hakedis.md](arastirma/02-poz-birim-fiyat-hakedis.md) | Poz, resmî birim fiyat, hakediş, fiyat farkı |
| 03 | [arastirma/03-muhasebe-ebelge-mevzuat.md](arastirma/03-muhasebe-ebelge-mevzuat.md) | Muhasebe, e-belge, mevzuat |
| 04 | [arastirma/04-referans-erp-karsilastirma.md](arastirma/04-referans-erp-karsilastirma.md) | Referans ERP karşılaştırması, sade arayüz ilkeleri |
| 05 | [arastirma/05-belge-otomasyonu.md](arastirma/05-belge-otomasyonu.md) | Fiş/fatura belge otomasyonu |
| 06 | [arastirma/06-teknik-mimari-altyapi.md](arastirma/06-teknik-mimari-altyapi.md) | Teknik mimari, altyapı, güvenlik, maliyet |
| 07 | [arastirma/07-excel-gecis-plani.md](arastirma/07-excel-gecis-plani.md) | Excel'den ERP'ye geçiş planı |
| 10 | [MODUL-HARITASI.md](MODUL-HARITASI.md) | Modül haritası |
| 11 | [YOL-HARITASI.md](YOL-HARITASI.md) | MVP ve aşamalar |
| 12 | [TEKNIK-ALTERNATIFLER.md](TEKNIK-ALTERNATIFLER.md) | Teknik alternatifler |
| 13 | [RISKLER.md](RISKLER.md) | Riskler |
| 14 | (özel) | Pilot keşif görüşmesi soru listesi; bu depoda yer almaz. Girdisi, araştırma dosyalarındaki "Açık sorular" bölümleridir |
| R1–R3 | [arastirma/inceleme/](arastirma/inceleme/) | Bağımsız çapraz model incelemeleri |
| — | [GELISTIRME-SURECI.md](GELISTIRME-SURECI.md), [surec/ORTAK-KURALLAR.md](surec/ORTAK-KURALLAR.md) | Araştırmanın nasıl yürütüldüğü |

### Karar numaraları

Karar kaydı özeldir ve bu depoda yer almaz; belgelerde geçen numaraların kısa karşılıkları şunlardır. K-06…K-14 aşağıdaki "Önerilen yeni karar maddeleri" tablosundadır.

| No | Konu | Durum |
|---|---|---|
| D-01 | Aşama 0'da önce araştırma, kod yok | Alındı (2026-11-18) |
| D-02 | Geliştirme ürün sahibi + yapay zekâ agent'larıyla yapılır; dil tercihi yok, bakımı kolay ve yaygın yığın öncelikli | Alındı (2026-11-18) |
| D-03 | Ürünleşmeye açık: tek müşteriyle başla, mimari çok firmalı kullanıma hazır olsun | Alındı (2026-11-18) |
| D-04 | Açık kaynak ERP temeli ile sıfırdan geliştirme birlikte karşılaştırılır | Alındı (2026-11-18) |
| D-05 | Yaklaşım: kendi yazılımımız (sıfırdan, açık kaynak kütüphanelerle); Odoo/ERPNext gibi hazır ERP temeli kullanılmaz. Yeniden değerlendirme koşulu: müşteri yasal defter ve e-Defter'i ERP içinde isterse | Alındı (2026-11-18) |
| D-06 | Pilot keşif görüşmesi için görüşme paketi: sunum, 5 ekranlık tıklanabilir tasarım taslağı (kurgusal veri), soru listesi | Alındı (2026-11-18) |
| D-07 | Excel analiz aracı geliştirilir: yerel, statik, ağsız; çıktılar git dışı | Alındı (2026-11-18) |
| K-03 | Nihai modül kapsamı ve MVP | Bekliyor (müşteri + ürün sahibi) |
| K-04 | Bulut sağlayıcı, veritabanı ve teknoloji yığını | Bekliyor (ürün sahibi) |
| K-05 | Muhasebe ERP içinde mi, dış servis/mali müşavirde mi | Bekliyor (müşteri) |

## Önerilen yeni karar maddeleri

| # | Konu | Kimde |
|---|---|---|
| K-06 | Veri konumu: Türkiye şart mı, AB + KVKK standart sözleşme kabul mü (→ 06 §4, 03 §6) | Müşteri + hukuk |
| K-07 | Resmî poz verisi: yalnız sözleşme kalemleri / lisanslı sağlayıcı / Bakanlık izni (→ 02 §2) | Müşteri + hukuk |
| K-08 | e-Fatura entegratörü ve e-Fatura gönderiminin MVP'de mi Aşama 2'de mi olacağı (→ 03, 11) | Müşteri + SMMM + kullanıcı |
| K-09 | Belge okuma kapsamı (PDF/fotoğraf) ve yurt dışı servis kullanımı (→ 05) | Müşteri |
| K-10 | Aşama 0'da D-01'i genişletme: Excel analiz betikleri, tıklanabilir prototip, süre sınırlı kavram kanıtı (→ 11). Sonuç: araç (D-07) ve taslak (D-06) yapıldı; kavram kanıtı D-05 ile gereksizleşti | Kullanıcı (kapandı) |
| K-11 | Pilot keşif dışı modüller: teminat, taşeron, saha günlüğü, puantaj, teklif/yaklaşık maliyet (→ 01 §2) | Müşteri |
| K-12 | Excel dosyalarının işlenme kuralları: git dışı, dış servise gönderilmez, maskeleme (→ 07 §3.2) | Müşteri |
| K-13 | Tarihsel veri, açılış bakiyesi tarihi, paralel çalışma süresi (→ 07 §7) | Müşteri |
| K-14 | Web sitesi ERP'den ayrı mı (→ 06 §9) | Müşteri + kullanıcı |
