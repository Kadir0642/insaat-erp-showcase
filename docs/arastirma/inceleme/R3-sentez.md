# R3 İncelemesi — Sentez belgeleri (00, 10–14)

> Belge numaraları (00–13), karar numaraları (K-xx, D-xx) ve "pilot keşif" kavramı için: [ARASTIRMA-OZETI.md](../../ARASTIRMA-OZETI.md#bu-belgeler-nasıl-okunur).

> İnceleyen: R3 (bağımsız, salt okunur) · Tarih: 18.11.2026 · Kapsam: [00 ARASTIRMA-OZETI](../../ARASTIRMA-OZETI.md), [10 MODUL-HARITASI](../../MODUL-HARITASI.md), [11 YOL-HARITASI](../../YOL-HARITASI.md), [12 TEKNIK-ALTERNATIFLER](../../TEKNIK-ALTERNATIFLER.md), [13 RISKLER](../../RISKLER.md) ve 14 (pilot keşif görüşmesi soru listesi; özel, bu depoda yok).
> Yöntem: pilot keşif notları (özel), karar kaydı (özel), [ORTAK-KURALLAR.md](../../surec/ORTAK-KURALLAR.md), araştırma 01–07 (güncel, düzeltilmiş hâlleri) ve R1/R2 okundu; sentezdeki iddialar kaynağına kadar izlendi. Web'e çıkılmadı; yeni olgusal doğrulama yapılmadı (aksi belirtilmedikçe kaynak belgeler ve R1/R2 esas alındı).

## Sonuç

| Belge | Sonuç | Kısa gerekçe |
|---|---|---|
| 00 Araştırma özeti | **Küçük düzeltmeyle** | İddialar büyük ölçüde sadık. Birkaç yerde "bulunamadı" → "yok", "yorum" → "doğrulandı" sertleşmesi var; pilot keşif hedefleri (performans, 5–10 yıl okunabilirlik, yedek) özette yok; kod okumayan okur için jargon yoğun. |
| 10 Modül haritası | **Küçük düzeltmeyle** | Etiketler çoğunlukla doğru; birkaç modülde [GEREKSİNİM] etiketi pilot keşfin söylediğinden geniş ("sözleşme", "personel", cari/çek-senet) ve [GEREKSİNİM] satırına öneri ayrıntıları (2FA vb.) karışmış. Saha günlüğü modülü yok ama K-11'de anılıyor. |
| 11 MVP ve aşamalar | **Küçük düzeltmeyle** | Aşama 0 tanımı D-01 ("kod yok") ile gerilimde; 02/03/01'in MVP önerilerinden sapmalar açıkça belirtilmemiş; e-Fatura gönderimi MVP dışı bırakılmış (03 tersini öneriyor). |
| 12 Teknik alternatifler | **Küçük düzeltmeyle** | Rakamlar ve lisans iddiaları kaynakla uyumlu. 03 ile 06 arasındaki barındırma çelişkisi (TR tercihi ↔ AB) fark edilmemiş; e-Defter asıl kopyası TR şartı anılmamış; bazı "doğrulanmadı" bayrakları düşmüş. |
| 13 Riskler | **Güvenilir** (küçük notlarla) | Riskler kaynaklara oturuyor; "15+ güncelleme" rakamı kaynakta tutarsız; güvenlik ihlali/yetki riski ve performans riski ayrı madde değil. |
| 14 Müşteri soru listesi (özel) | **Küçük düzeltmeyle** | İçerik kapsamlı ve 01–07 açık soruları büyük ölçüde derlenmiş; ancak görüşmede doğrudan kullanılacak biçimde değil (iç etiket/ok/kod karışık, çok sayıda bileşik soru, süre/sıra rehberi yok). Proje iş akışı/aşama tanımı ve kullanıcı sayısı/hacim soruları eksik. |

Genel hüküm: Sentez, kaynaklara ve R1/R2 düzeltmelerine genel olarak sadık; uydurma kaynak ya da kesin süre/fiyat sözü yok. Öneriler genelde [ÖNERİ] olarak sunulmuş ve nihai kararlar kullanıcıya/müşteriye bırakılmış. Sorunlar daha çok (a) etiket/kesinlik sertleşmeleri, (b) pilot keşif hedeflerinin görünmemesi, (c) belgeler arası küçük sapmalar ve (d) kullanılabilirlik düzeyinde.

---

## Bulgular

Biçim: `[Önem] dosya:bölüm — sorun — önerilen düzeltme`

### 00 — Araştırma özeti

- **[Orta] 00:"Doğrulanmış / doğrulanmamış ayrımı" ve bulgu 7 — "e-Fatura eşikleri" "Resmî kaynakla doğrulanan" listesinde; bulgu 7 durumu "Doğrulandı (RG/GİB; R1)".** R1 535 sayılı Tebliğ metnini yalnızca ikincil aktarımdan (alomaliye) teyit etti ("İ"), ISMMMO PDF'ini açmadı; R2 ise "500 bin TL eşiği resmî metinden kontrol edilmedi" diyor (R2 "Hâlâ doğrulanamayanlar"). Ayrıca "inşa" ibaresinin kamu yüklenicisini kapsaması 03/R1'e göre yorumdur; "doğrudan GİB bağlantısı pratik değil" ise 03 §2'de [BELİRSİZ] ("ölçütleri karşılaması olası değil"). — **Düzeltme:** e-Fatura eşiğini "ikincil (RG metni aktarımı; R1) — SMMM teyidi" listesine taşı; bulgu 7 durumunu "Kısmen doğrulandı; kapsam yorumu SMMM'ye" yap; "inşa ibaresi yorum, 3 M TL eşiği de çoğu yüklenicide geçerli" notunu ekle.
- **[Orta] 00:Bulgu 3 — "resmî API/XML yok" (Durum: Doğrulandı).** 02 §2: "Excel, XML veya API bulunamadı (doğrulanmadı = yok olduğu kesin değil)". Yasak beyanı doğrulanmış (resmî), API yokluğu değil. Aynı özet bulgu 6'da yokluğu doğru işaretliyor ("Doğrulanmadı (yokluk)"); bulgu 3 tutarsız. — **Düzeltme:** "resmî API/XML bulunamadı (yokluk doğrulanmadı)" yaz; durumu iki parçaya böl.
- **[Orta] 00:genel — pilot keşif hedefleri özette yok.** Performans hedefleri/yük testi (06 §8), 5–10 yıl okunabilirlik/dışa aktarma biçimi (06 §7: CSV/Parquet + PDF/A, kiracı bazlı "tüm verimi indir"), yedekleme/RPO-RTO, güvenlik hedefi (ASVS, 2FA) 00'da bulgu olarak geçmiyor; yalnız dizinde "06: ... yedek, performans" ibaresi ve bulgu 12'de "saklama 10 yıl esas" var. 10–14'te de sayısal hedef yok (11 yalnızca "performans hedefleri (→ 06 §8) karşılandı" diyor; 14 yalnızca RPO/RTO sorusu içeriyor). Ürün sahibi bu hedefleri bu belgelerden göremez. — **Düzeltme:** 00'a "Pilot keşif teknik beklentiler: nerede, ne öneriliyor" kısa tablosu ekle (performans p95 < 500 ms, 25 eşzamanlı kullanıcı, RPO ≤ 15 dk/RTO ≤ 4 sa [ÖNERİ]; yük testi aracı; 10 yıl + istisna saklama; açık biçim arşiv; aylık geri yükleme testi) ve 11'e/12'ye aynı satırları bağla.
- **[Düşük] 00:Ek gözlemler — "teminat mektubu takibi ... sektör acı noktası ve farklılaştırıcı aday".** 01 Özet 4 aynı iddiayı "kapsamlı ürün taraması yapılmadı" ve "incelediğim yerli ürün tanıtımlarında açıkça yer almıyor" kaydıyla veriyor; "acı noktası" kanıtı hukuki kurallardan (K1, K3, K4) türetilmiş, sektör geri bildirimi değil. Kayıtlar düşmüş. — **Düzeltme:** "sınırlı taramaya göre yerli ürün tanıtımlarında görünmüyor; acı noktası olduğu müşteriye doğrulatılmalı" yaz.
- **[Düşük] 00:Bulgu 1 — Durum "Olgusal (pilot keşif)".** Pilot keşif yalnızca Excel dosyalarını öncelikli gereksinim kaynağı olarak gösteriyor; "en büyük risk teknik değil, belgelenmemiş formül bilgisi" 07'nin [ÖNERİ] değerlendirmesi. — **Düzeltme:** İkinci cümleyi [ÖNERİ] olarak ayır.
- **[Düşük] 00:Bulgu 5 — KİK 2026/DK.D-332 nüansı.** Karar "TÜFE (2003=100) belirtilmiş" sözleşmeler için; özet bunu genel kural gibi veriyor. — **Düzeltme:** "TÜFE 2003=100'e atıf yapan sözleşmelerde" ibaresi ekle.
- **[Düşük] 00:okunabilirlik (kod okumayan okur).** Tablo YFK, FSEK, YİGŞ md. 22/39/40, İo, RLS, `tenant_id`, UBL, SMMM, AMP/Oska gibi kısaltmalar/terimlerle dolu; sözlük yok; "kullanıcı + müşteri karar listesi" (K-06..K-14) tablosu sonda ve jargonlu. — **Düzeltme:** Başa 5–6 cümlelik düz Türkçe "Sizden beklenen kararlar" bloğu (K-03/K-04/K-05 + K-07) ve kısa terimler sözlüğü (YFK, YİGŞ, ATGB, GİB, entegratör, SMMM, RLS/çok kiracılık, MVP) ekle.

### 10 — Modül haritası

- **[Orta] 10:M3 — "Sözleşme [GEREKSİNİM] (hakediş için gerekli)".** Pilot keşifte "sözleşme" geçmiyor; proje/ihale ve hakediş var. Sözleşme modülü hakedişin zorunlu önkoşulu olabilir ama bu çıkarım; etiket "pilot keşifte açıkça söylenen" anlamına geliyor (ORTAK-KURALLAR). Aynı durum M5'te metraj/yeşil defter/kesintiler, M12'de cari/kasa-banka/çek-senet için geçerli (pilot keşif geniş kapsamlı muhasebe/finans istiyor ve kapsamı bilerek açık bırakıyor). — **Düzeltme:** M3'ü "[ÖNERİ] (pilot keşifteki ihtiyaçların önkoşulu)" yap; M5/M12'de [GEREKSİNİM]'yi yalnızca poz/hakediş/muhasebe başlığına, alt işlevleri [ÖNERİ]'ye ayır.
- **[Düşük] 10:M11 — "Personel [GEREKSİNİM] (rol olarak)".** 01 Özet 2: "Taşeron, personel, teminat mektubu, saha raporu pilot keşifte yok." Pilot keşif personeli yalnızca ileride kullanıcı rolü olarak anıyor; modül değil. — **Düzeltme:** Etiketi [ÖNERİ] yap, "kullanıcı rolü M1'de" notu ekle.
- **[Düşük] 10:M1 — [GEREKSİNİM] satırında 2FA, "oluşturan ≠ onaylayan", denetim kaydı.** Bunlar 06 §6 [ÖNERİ]'leri; pilot keşif yalnızca kullanıcı adı/şifreyle giriş, rol/proje erişimi ve işlem kayıtlarını istiyor. — **Düzeltme:** Tanımda "[ÖNERİ]" parantezi ekle.
- **[Orta] 10:modül listesi ↔ 00 K-11 / 01 §2 — "saha günlüğü/günlük rapor/fotoğraf" modülü yok.** 01 bunu MVP'ye önerdi ve 00 K-11 "saha raporu"nu karar maddesi yapıyor; 10'da ayrı modül ya da kalem yok (yalnız M4/M11 notunda "saha girişleri"). 11 de "saha raporu Aşama 2" diyor. — **Düzeltme:** 10'a "M21 Saha günlüğü (günlük rapor, metraj girişi, fotoğraf) [ÖNERİ], Aşama 2, mobil/çevrimdışı BELİRSİZ" satırı ekle ya da K-11'den çıkar.
- **[Düşük] 10:M5 — "Resmî katalog yok", M4 — "Gantt/CPM yok".** Kapsam dışı bırakma, tanım hücresinde olgu gibi duruyor; öneri/karar ayrımı yalnızca üst notta. — **Düzeltme:** "(önerilen kapsam dışı)" ekle.
- **[Düşük] 10:M13/M15 ↔ 11 Aşama 1.** 10 M15 tanımında "XML/karekod okuma" Aşama 1 gibi; 11 Aşama 1 tablosu karekodu anmıyor (05 §5 MVP'ye karekod okumayı koyuyor). — **Düzeltme:** Birini hizala.

### 11 — MVP ve aşamalar

- **[Orta] 11:Aşama 0 başlığı — "kod yok veya atılabilir prototip".** Karar D-01: "Aşama 0: önce araştırma, kod yok"; pilot keşif: onaysız kapsamlı geliştirme yok. 0.4 (Odoo + sıfırdan kavram kanıtı), 0.6 (tıklanabilir prototip) ve 0.1'in analiz betikleri kod/prototip içerir. 00 yalnızca PoC için K-10 açıyor; prototip ve analiz betikleri için onay maddesi yok. — **Düzeltme:** Aşama 0'ı "D-01 kapsamının genişletilmesi önerisi — kullanıcı onayı gerekir" diye işaretle; 0.1/0.6 için de K-10'a benzer onay satırı ekle (ya da K-10'u "Aşama 0 prototip/PoC çalışmaları" diye genişlet).
- **[Orta] 11:Aşama 2 / Özet — e-Fatura gönderimi MVP dışı; 03 §7 MVP'de Seçenek B öneriyor.** 03: "MVP'de B ... ERP'den kesilmezse hakediş ile fatura arasında çift giriş oluşur." 11 MVP'si fiilen Seçenek A + gelen XML; 00 bulgu 8 ve 12 ise B'yi "öneri" olarak öne çıkarıyor. Sapma gerekçesiz; MVP süresince çift giriş riski ve entegratör seçiminin (K-08) Aşama 1 girişinde gerekmeyeceği söylenmiyor. — **Düzeltme:** 11'e "03'ten sapma: B'nin e-Fatura gönderimi Aşama 2'ye alındı çünkü ...; MVP süresince fatura entegratör portalından elle kesilir (çift giriş riski kabul)" notu ekle ya da gönderimi MVP'ye al.
- **[Orta] 11:Aşama 3 — "yeni birim fiyat, iş artışı uyarısı" Aşama 3'te; 02 §7.2 MVP: "Evet, basit hâliyle".** Ayrıca ataşman kaydı (02: MVP "Evet") Aşama 1 tablosunda yok; fiyat farkı 02'de MVP "Evet", 11'de Excel'e bağlı koşullu. Sapmalar mantıklı olabilir ama sentez 02'nin önerisini değiştirdiğini söylemiyor. — **Düzeltme:** "02'den farklar" kısa listesi ekle veya 02'ye uy.
- **[Düşük] 11:"Neden bu kadar?" — pilot keşif "süre/ilerleme" ve "iş aşamaları" [GEREKSİNİM] ihtiyacı (M4) Aşama 2'de; gerekçe yalnızca malzeme/ekipmanı açıklıyor.** — **Düzeltme:** İlerlemenin MVP'de hakedişin kümülatif ilerlemesiyle karşılandığını, planlanan–gerçekleşen programın Aşama 2'ye kaldığını yaz.
- **[Düşük] 11:Aşama 4 — M18 web sitesi "karara bağlı genişlemeler" başlığı altında.** Aynı satır "her aşamada paralel (S)" diyor; K-14'e bağlı olduğu belirtilmeli. — **Düzeltme:** Ayrı "Paralel iş" başlığına al, K-14'e bağla.
- **[Düşük] 11 Özet/"Neden" ve 13 R7 — "Tek geliştirici + agent'lar" ve "(D-02)".** D-02 "kullanıcı + Claude agent'ları" diyor; "tek kişi" çıkarım. — **Düzeltme:** "(varsayım: ekip büyüklüğü D-02'den çıkarım; kullanıcıyla teyit)" ekle.
- **[Düşük] 11:çıkış kriteri "1–2 tam hakediş/ay paralel".** 07 bunu "[BELİRSİZ], müşteriyle netleştirilir" diye veriyor; 11'de kesin çıkış kriteri gibi duruyor (belge geneli [ÖNERİ] olsa da). — **Düzeltme:** "(başlangıç önerisi; K-13)" ekle.

### 12 — Teknik alternatifler

- **[Orta] 12:Barındırma — 03 §6 ile 06 §4.3 çelişkisi sentezde görünmüyor.** 03: "[ÖNERİ] Muhasebe ve personel verisi için Türkiye'de barındırma tercih edilsin ... e-Defter asıl kopyası yurt içinde kalmalı." 06/12: "Veri Türkiye'de zorunlu değilse AB'de yönetilen PG." İki öneri zıt yönde; 12 yalnızca 06'yı aktarıyor. Ayrıca e-Defter/berat asıl kopyasının mükellefin Türkiye'deki sisteminde tutulması zorunluluğu (03 §6) ve R1'in VUK 509 notu (e-belge gönderme/alma sisteminin altyapısının Türkiye'de olması, özel entegrasyon bölümü) 12'de yok; sadece "e-Fatura/e-Arşiv asıl arşivi TR entegratörde" var. K-05 "C" çıkarsa AB barındırma doğrudan sorunlu olur. — **Düzeltme:** "Barındırma" bölümüne "03: TR tercih; 06: zorunlu değilse AB — kullanıcı kararı (K-06)" satırı, e-Defter TR şartı ve R1 notunu ekle; soru listesindeki "Türkiye'de zorunlu mu" sorusuna "mali verilerin kısmen yasal olarak TR'de kalması gerekir" bağlamı verilsin.
- **[Düşük] 12:"Öneriyi değiştirebilecek müşteri yanıtları" — "Ürünleşme yakın vadeli öncelik (D-03) → Sıfırdan/Frappe lehine (lisans serbestisi)".** (a) Bu müşteri değil kullanıcı kararı; (b) aynı belgenin tablosu Odoo Community'nin LGPL olduğunu ve kapalı modüle izin verdiğini söylüyor; lisans sorunu yalnız Enterprise'ta. — **Düzeltme:** Satırı "Kullanıcı kararı" olarak ayır; "Enterprise kullanılırsa" kaydı ekle.
- **[Düşük] 12:Yaklaşım tablosu — Odoo "Çok kiracılık: Kiracı başına veritabanı".** 06 §1.1: "(doğrulanmadı)"; Frappe için "(doğrulandı)" korunmuş, Odoo için bayrak düşmüş. Aynı tabloda Community "kendi modülümüz kapalı olabilir" iddiası 06'da ikincil kaynaklı (forum/blog) olduğu hâlde bayraksız. — **Düzeltme:** İki hücreye "(doğrulanmadı / ikincil)" ekle.
- **[Düşük] 12:Öneri gerekçe 1 — "agent verimliliği", "zorunlu yıllık sürüm göçü olmaması" bayraksız; puan tablosu yok.** Tabloda "(değerlendirme, doğrulanmadı)" var ama gerekçe maddesinde "yaygın, tip denetimli yığın hata yakalamayı kolaylaştırır (D-02)" kesin gibi okunuyor; R1 de puanların yön verici olduğunu not etmişti. Ayrıca "yıllık zorunlu sürüm göçü" 06'nın ifadesi; Odoo sürümlerinin birden fazla yıl desteklendiği yaygın bilgi (kendi bilgim, bu incelemede doğrulanmadı) → "zorunlu" abartılı olabilir. — **Düzeltme:** Gerekçeye "(değerlendirme; ölçülmedi)" ekle; "zorunlu yıllık" yerine "yükseltme yükü" yaz.
- **[Düşük] 12:Maliyet bantları.** Kaynaklarla uyumlu (€55–70, €110–160, $300–450, ~$60–150, €280→€339, TL entegratör, $1–30). "Web sitesi ~€0–25" 06'daki €0–15 (statik) ve $5–25 (WordPress) karışımı. — **Düzeltme:** Para birimini sadeleştir veya iki satır yap. (Fiyat sözü yok; uyarı satırı var — iyi.)
- **[Bilgi] 12:Kullanılabilirlik.** "Modüler monolit", `tenant_id`, RLS, PITR, pgBackRest, LGPL-3 gibi terimler açıklamasız; kod okumayan ürün sahibi için "bu seçim bana ne kazandırır/kaybettirir" özeti zayıf. — **Düzeltme:** 3–4 maddelik düz Türkçe "Karar için bilmeniz gerekenler" kutusu (süre, bakım yükü, muhasebe işini kim yapar, veri nerede).

### 13 — Riskler

- **[Düşük] 13:R4 — "GİB 2026'da 15+ format/kılavuz güncellemesi".** 03'te üç farklı ifade var: Özet "yılda 10'dan fazla (2025–2026)", §2 "2026'da 15'ten fazla paket/kılavuz", §7 "2026'da en az 6 paket güncellemesi". 13 en yüksek rakamı aldı. — **Düzeltme:** "sık (kaynakta 6–15+ arası, tutarsız)" yaz veya 03'ü düzelttir.
- **[Orta] 13:eksik risk — güvenlik/yetki ihlali (kimlik hırsızlığı, yetkisiz proje erişimi, kiracı verisi sızıntısı) ve performans/ölçek yetersizliği ayrı risk olarak yok.** Pilot keşif güvenli kimlik doğrulama ve performans hedefi istiyor; 06 §6/§8 kontrolleri tanımlıyor ama risk tablosunda yalnız R5 (KVKK/veri konumu) ve R10 (Excel dosyaları) var. Yedekleme/felaket kurtarma yalnız R7 içinde. Mobil/çevrimdışı "belirsiz" olarak 10'da var, riskte yok. — **Düzeltme:** R18 "Güvenlik ihlali/yetki hatası", R19 "Performans/ölçek hedefinin tutmaması (yük testi)", R20 "Şantiye mobil/çevrimdışı ihtiyacının geç ortaya çıkması" ekle (azaltmalar 06'dan: ASVS L2, RLS testi, 2FA, k6 yük testi, PWA/çevrimdışı kuyruk).
- **[Düşük] 13:R2 — "Karar 10132 geçişi doğrulanmadı".** 02 §4 aynı geçiş maddesini ikincil kaynakla olgu gibi veriyor, R1 doğrulayamadı; 13/00'daki temkinli ifade doğru, ancak 02 ile çelişkiyi not et. — **Düzeltme:** "02 §4 ikincil kaynakla destekliyor, R1 teyit edemedi" ekle.
- **[Bilgi] 13:Karşılık kontrolü.** Risklerin çoğu (R1–R12, R14, R16, R17) soru listesinde bir karşılık buluyor. Soru karşılığı olmayan: R13 (teknik), R15 (hukuk) — kabul edilebilir.

### 14 — Müşteri soru listesi (özel belge; bulgular genelleştirilmiştir)

- **[Orta] 14:genel — görüşmede doğrudan kullanılabilirlik.** Liste yaklaşık 55 soru içeriyor ve birçoğu bileşik (tek soruda 3–4 alt soru). Her satırda iç etiket ([GEREKSİNİM]/[BELİRSİZ]), ok ve karar kodu var; bunlar müşteriye okunacak metni kirletiyor ve müşteri jargonuyla ("RPO/RTO", "UAT" gibi) karşılaşabilir. Süre/sıra rehberi yok. — **Düzeltme:** İki katman yap: (1) müşteriye okunacak, etiketsiz, bileşikleri bölünmüş 1–2 sayfa temiz liste; (2) iç haritalama tablosu (soru → karar/risk). Tahmini görüşme sayısı/süresi öner.
- **[Orta] 14:eksik sorular.** (a) Proje iş akışı/aşama tanımı: proje iş akışları ve iş aşamaları için aşama, sorumlu ve aşama bazında maliyet izleme sorusu yok. (b) Kullanıcı sayısı ve veri hacmi: performans hedefi için gerekli. (c) Performans beklentisi (acı noktası: yavaş rapor? ay sonu yoğunluğu?). (d) 07'deki personel/maaş içeren dosyalar sorusu ve 05'teki "ihale sözleşmesinden gelen gizlilik şartı" kısmı derlemede kaybolmuş. — **Düzeltme:** Bu 4 soruyu ilgili bölümlere ekle.
- **[Düşük] 14:Etiket kuralı.** Üst not "aksi yazılmadıkça etiket [BELİRSİZ]" diyor; birçok soru etiketsiz kalıyor. İç kullanım için tutarlı ama pilot keşif ayrımını (kesin müşteri talebi/öneri/belirsizlik) görünür kılmıyor. [GEREKSİNİM] etiketli sorular pilot keşifteki talepleri doğru yansıtıyor; sahte [GEREKSİNİM] görmedim.
- **[Düşük] 14:Şirket türü ve hasılat sorusu.** e-Fatura zorunluluğunu belirleyen soru önemli sayılmış ama listede geç geliyor ve mali açıdan hassas. — **Düzeltme:** En önemli sorulara birleştir; "mali müşavirinize sorup bildirebilirsiniz" seçeneği ver.
- **[Bilgi] 14:İstenecek belgeler bölümü** 07 §7 ve 05 §5 ile uyumlu; kullanılabilir.

---

## Kontrol listesi özeti

1. **Sadakat:** 15'ten fazla iddia izlendi (aşağıda); 12'si tam uyumlu, 3'ü sertleşme/ihmal içeriyor (e-Fatura "doğrulandı", API "yok", teminat "acı noktası"). Kaynakta olmayan iddia bulunmadı.
2. **Etiket disiplini:** Sahte [GEREKSİNİM] yok ama M3 (sözleşme), M5/M12 alt işlevler, M11 (personel) ve M1 ayrıntıları genişletilmiş. Kararlar: D-03 (çok kiracılık hazırlığı → M0, 11 Aşama 4) ve D-04 (12 başlığında, 11 Aşama 0.4) doğru yansımış; D-02 doğru anılmış ("tek geliştirici" çıkarım). D-01 ile Aşama 0 tanımı gerilimde.
3. **Pilot keşif kapsaması:** pilot keşifte ifade edilen ihtiyaçlar ve görevler karşılanmış (Excel geçişi 07'de/11 tablosunda; web sitesi M18/K-14 ve soru listesinde; yetki matrisi M1 ve soru listesinde). Zayıf: performans hedefleri + yük testi, uzun dönem okunabilirlik/dışa aktarım ve yedekleme 10–14'te ve 00'da yalnızca işaretçi veya tek satır; sade arayüz önerileri yalnızca 04'e işaretle anılıyor.
4. **Tutarlılık:** 10 ↔ 11 aşama atamaları (M0–M20) uyumlu. Sapmalar: karekod (10 vs 11), M18 başlığı (11), saha modülü (10'da yok), e-Fatura gönderimi (03 ↔ 11), yeni birim fiyat/iş artışı (02 ↔ 11). 13 riskleri 14'te büyük ölçüde karşılık buluyor (yukarı). 12 ↔ 03 barındırma çelişkisi.
5. **Kullanılabilirlik:** Soru listesi içerik olarak güçlü, biçim olarak iç kullanıma yakın; 00/12 jargonlu.
6. **Dürüstlük:** Kesin süre/fiyat sözü yok (11: "süre ve fiyat verilmez"; 12: tahmin/oynak uyarısı). Doğrulanmamış bilgiler çoğunlukla işaretli; düşen bayraklar yukarıda listelendi.

---

## İzlenen iddialar

Biçim: iddia → kaynak (+ düzeltme) → uyumlu mu

1. 00 B3: YFK erişim beyanı yazılım/veri tabanında kullanımı yasaklıyor (FSEK atfı) → 02 §2 K4; R1 (resmî sayfa okundu) → **Uyumlu**. ("API/XML yok" kısmı → 02 §2 "bulunamadı, kesin değil" → **Sertleşmiş**.)
2. 00 B4: RG 30.07.2025 değişiklikleri yalnız 01.09.2025 ve sonrası ilanlı ihalelere → 02 Özet 5/§4; R1 (Geçici Madde 34) → **Uyumlu**.
3. 00 B5: F = An × B × (Pn − 1); KİK 2026/DK.D-332 TÜFE 2025=100; İo açık → 02 §5; R1 çözülen çelişki 3 → **Uyumlu** (TÜFE 2003=100 atıf nüansı eksik).
4. 00 B6 / 10 M5: ulusal e-hakediş kanalı ve EKAP yüklenici API'si bulunamadı → 02 §6 → **Uyumlu** (yokluk doğru işaretli).
5. 00 B7: e-Fatura 500 bin TL (inşa) / 3 M TL; e-Defter 2025 bilanço esası → 03 §1 K1/K3; R1 (ikincil aktarım) → **Kısmen** ("Doğrulandı" etiketi güçlü; inşa ibaresi yorum).
6. 00 B7: doğrudan GİB bağlantısı küçük firma için pratik değil → 03 §2 ([BELİRSİZ] "olası değil") → **Sertleşmiş**.
7. 00 B9: GVK 42–44; yer teslimi/geçici kabul tarihleri; KDV 4/10; stopaj %5 → 03 §3–4; R1 → **Uyumlu**.
8. 00 B10: Google/AWS fatura ayrıştırıcıları Türkçe desteklemiyor; Azure destekliyor → 05 §2; R2 (AWS'nin "belirsiz"i çözüldü) → **Uyumlu**.
9. 00 B12 / 12: KVKK standart sözleşme + 5 iş günü; AWS İstanbul Local Zone'da RDS yok; saklama 10 yıl esas → 06 §4, 03 §6, 05 §4; R1/R2 → **Uyumlu**.
10. 00 Ek gözlem: teminat mektubu takibi sektör acı noktası/farklılaştırıcı → 01 Özet 4/§5 ("kapsamlı ürün taraması yapılmadı") → **Kısmen** (çekince düşmüş).
11. 10 M3: e-teminat/Takasbank referansı, 2024–2026 kronolojisi → 01 §1, Açık noktalar; R2 çözülen çelişki 1 → **Uyumlu**.
12. 10 M6 / 11: elle endeks, hakediş başına dondurulmuş endeks, kontrol hesabı → 02 §5 "Otomatikleştirilebilirlik", §7.2 → **Uyumlu**.
13. 11 Aşama 1 M13/M15 (XML yükleme, elle giriş, çift kayıt) ve Aşama 3 pilot (Azure, LLM, açık kaynak OCR; üç bantlı kuyruk) → 05 §3, §5 → **Uyumlu** (karekod Aşama 1'de eksik).
14. 11 Aşama 1 M12 + e-Fatura gönderimi Aşama 2 → 03 §7 ("MVP'de B") → **Sapma** (gerekçesiz).
15. 12 Odoo: e-Fatura/e-Arşiv/e-İrsaliye Community LGPL-3; e-Defter/mali raporlar Enterprise gerekebilir [BELİRSİZ]; Nilvera ücretli → 06 §1.1, 04 §3.3; R1/R2 → **Uyumlu** (R1 "fiilen Enterprise (çıkarım)", R2 farklı okumuştu; 12'nin "[BELİRSİZ]" ifadesi doğru).
16. 12 Odoo fiyatı: ilk yıl ≈ €280, sonra ≈ €339 (10 kullanıcı Custom) → 06 §1.1; R1 → **Uyumlu**.
17. 12 Frappe MIT / ERPNext GPLv3; Frappe site başına kiracı (doğrulandı) → 06 §1.1 (b) → **Uyumlu**.
18. 12 hosting tablosu: AWS Local Zone GA 20.05.2026; Hetzner zam/yönetilen PG yok; DO 30.11.2026 → 06 §4.2; R1 → **Uyumlu**.
19. 12 VUK 509: asıl muhafaza TR'de, ikincil arşiv engellenmez → 06 §4.1; R1 → **Uyumlu** (e-Defter TR şartı ve R1'in altyapı notu eksik).
20. 12 Barındırma önerisi "zorunlu değilse AB'de yönetilen PG" → 06 §4.3 ↔ 03 §6 ("TR tercih") → **Çelişki belirtilmemiş**.
21. 12 Maliyet bantları (altyapı, 50 kullanıcı, entegratör, belge okuma $1–30) → 06 §5, 03 §2, 05 §5 → **Uyumlu** (ikincil/tahmin bayrakları var).
22. 13 R10: pycel CVE-2024-53924 (CVSS 9.8), `-I`, yalıtılmış ortam → 07 §3.1–3.2; R2 → **Uyumlu**.
23. 13 R4: GİB 2026'da 15+ güncelleme → 03 §2 (15+), Özet (10+/yıl), §7 (≥6) → **Kaynakta tutarsız; en yüksek seçilmiş**.
24. 13 R9: pilot 150–300 belge, altın etiket, LLM rakam uydurabilir → 05 §3, §5 → **Uyumlu**.
25. 14 (özel soru listesi): 01.09.2025 öncesi/sonrası, 2026 TÜFE baz değişikliği sorusu → 02 §4–5, 02 Açık sorular 6 → **Uyumlu**.
26. 14 (özel soru listesi): RPO/RTO ve bütçe aralığı soruları → 06 Açık sorular 3, 6 → **Uyumlu**.
27. 00 K-14 / 10 M18: web sitesi ERP'den ayrı → 06 §9 → **Uyumlu** (öneri olarak işaretli).
28. 12/00: "teknik öneri sıfırdan TypeScript+PostgreSQL; Frappe alternatif; puanlar ölçülmemiş; kavram kanıtı" → 06 §1.2–1.3, 04 §3.4; R1 → **Uyumlu** (D-04 ve kullanıcı kararı korunmuş).

---

## Etiket ve karar disiplini notu

- Öneriler karar ya da müşteri talebi gibi sunulmamış: 10 "aday kapsam", 11 "tümü [ÖNERİ]", 12 "Nihai seçim kullanıcıda (K-04)". Tek gerilim: 12 "Birincil: sıfırdan" ifadesi puan tablosunun (06, ölçülmemiş) yön vericiliğini taşıyor; R1'in uyarısı kısmen yansıtılmış (kavram kanıtı + K-05 sonrası karar), yeterli.
- Pilot keşif gereği "kaynağı doğrulanmamış otomasyon yöntemleri müşteri kararı gibi sunulmamış": 00 B10, 10 M15, 11 Aşama 3, 13 R9 PDF/fotoğraf okumayı [BELİRSİZ] tutuyor — uyumlu.
- Dürüstlük: "doğrulanmadı" listesi 00'da özenli; ancak yukarıdaki üç sertleşme (e-Fatura eşiği, API yokluğu, teminat acı noktası) ve 12'deki iki düşen bayrak düzeltilmeli.
