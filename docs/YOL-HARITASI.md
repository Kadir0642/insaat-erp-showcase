# Yol Haritası: MVP ve Aşamalar

> Belge numaraları (00–13), karar numaraları (K-xx, D-xx) ve "pilot keşif" kavramı için: [ARASTIRMA-OZETI.md](ARASTIRMA-OZETI.md#bu-belgeler-nasıl-okunur).

> 18.11.2026 · Tümü **[ÖNERİ]**; müşteri onayı yok (K-03). Süre ve fiyat verilmez; göreli büyüklük: **S** küçük · **M** orta · **L** büyük. Modül kodları (M1…) [MODUL-HARITASI.md](MODUL-HARITASI.md)'nden.

## Özet

- **[ÖNERİ]** MVP'nin tek hedefi: **bir projenin hakediş gelirini ve gerçek maliyetini aynı ekranda, Excel'e gerek kalmadan görmek.** Omurga: proje–sözleşme–sözleşme kalemi–metraj–ara hakediş + gider kaydı–cari–sahip paneli.
- **[BELİRSİZ]** e-Fatura gönderimi MVP'de mi Aşama 2'de mi: iki seçenek aşağıda; karar K-05/K-08.
- **[ÖNERİ]** Satın alma, stok, taşeron, saha günlüğü Aşama 2'ye; PDF/fotoğraf okuma Aşama 3'e; tam resmî muhasebe ve resmî poz kataloğu ancak müşteri/hukuk kararıyla Aşama 4'e.
- **[BELİRSİZ]** Gerçek Excel dosyaları analiz edilince MVP içeriği değişebilir (→ 07).

## Aşama 0 — Karar öncesi adımlar (D-01: ERP için kod yok)

Aşağıdakilerin çoğu kod gerektirmez. Kod ya da prototip gerektirenler (✱) ürün kodu sayılmaz; K-10 kapsamında iki ✱ adım yapıldı: Excel analiz aracı (0.1) ve tıklanabilir ekran taslakları (0.6). Üçüncüsü olan kavram kanıtı (0.4), "kendi yazılımımız" kararıyla (D-05) gereksizleşti.

| # | Adım | Amaç | Büyüklük | Bağlı karar |
|---|---|---|---|---|
| 0.1 | **Excel envanteri** (07 aşama 1–2): sayfa, formül, makro, dış bağlantı listesi; dosyalar git dışında. Otomatik yapı raporu aracı ✱ **geliştirildi** ([Excel analiz aracı](EXCEL-ANALIZ-ARACI.md)); gerçek firma dosyalarıyla henüz çalıştırılmadı | Gerçek kapsamı doğrulamak | S–M | K-12, K-10 |
| 0.2 | **İş kuralı kartları** — önce bir kapanmış hakediş dosyası için (07 §4) | Hakediş hesabını birebir anlamak | S | — |
| 0.3 | **SMMM görüşmesi** — program, fiş aktarım biçimi, e-Defter, mali mühür | K-05'i netleştirmek | S | K-05, K-08 |
| 0.4 | ~~Kavram kanıtı — aynı mini senaryo Odoo'da ve sıfırdan (→ 04 §3.4)~~ **Düştü**: yaklaşım kararlaştırıldı (D-05) | — | — | — |
| 0.5 | **Belge örneklemesi** — 1–2 aylık gelen belgede biçim dağılımı sayımı (→ 05 §5) | Belge otomasyonunun değerini ölçmek | S | K-09 |
| 0.6 | **Ekran taslakları** (5 ekran: sahip paneli, proje özeti, ara hakediş, gelen fatura onayı, Excel içe aktarma); tıklanabilir sürüm ✱ **hazırlandı** ([Görüşme paketi](GORUSME-PAKETI.md)); görüşmede kullanılacak | Arayüz hedefini somutlaştırmak (→ 04 §5) | S | K-10 |
| 0.7 | **Hukuk görüşü** — poz verisi (FSEK), KVKK/veri konumu | Riskleri kapatmak | Dış | K-06, K-07 |

**Aşama 1'e giriş kriteri:** 0.1–0.3 tamamlandı; K-03, K-04, K-05, K-06 yanıtlandı; MVP dosyalarının iş kuralı kartları müşteri onaylı.

## Aşama 1 — MVP: "Proje maliyeti ve hakediş omurgası" (L)

**Hedef:** Seçilen 1–2 aktif projede hakediş ve maliyet takibini Excel'den ERP'ye taşımak.

| Modül | MVP içeriği |
|---|---|
| M0, M1 | Çok kiracılı veri modeli (görünmez), giriş + 2FA (sahip/yönetici), rol × proje yetkisi, denetim kaydı |
| M2, M3 | Proje; sözleşme (tür, ilan tarihi → kural sürümü, yer teslimi/geçici kabul, avans, ceza, kesinti parametreleri); teminat defteri **hafif** (K-11'e bağlı) |
| M5 | Sözleşme kalemlerinin Excel'den aktarımı, metraj/yeşil defter/ataşman, kümülatif ara hakediş, parametrik kesintiler, yeni birim fiyat kaydı ve iş artışı (%10/%20) uyarısı basit hâliyle, Excel/PDF çıktı (kontrol amaçlı) |
| M6 | Firma Excel'de fiyat farkı hesaplıyorsa: elle endeksli kontrol hesabı **[BELİRSİZ]** |
| M12 | Cari, kasa/banka (ekstre içe aktarma), gider kaydı → proje/iş kalemi, hakediş mahsup fişi taslağı, SMMM'ye fiş aktarımı |
| M13, M15 | Gelen e-Fatura XML yükleme, karekod okuma, belge deposu, hızlı elle giriş (VKN, KDV/toplam kontrolü, çift kayıt uyarısı), onay + denetim izi; e-Fatura gönderimi Seçenek 1'de |
| M16, M17 | Sahip paneli (proje bazında hakediş geliri – maliyet), aşama/kalem raporu, Excel'e dışa aktarım; şablonlu içe aktarma |

### e-Fatura gönderimi: iki seçenek (K-05, K-08)

| | **Seçenek 1 — MVP'de** (03'ün önerisi) | **Seçenek 2 — Aşama 2'de** (bu belgenin önerisi) |
|---|---|---|
| Ne | Hakediş faturası ERP'den, özel entegratör API'si üzerinden (Seçenek B, → 03 §7) | MVP'de fatura mevcut entegratör/GİB portalında elle kesilir; ERP faturayı kayıt olarak alır |
| Gerekçe | e-Fatura fiilen zorunlu; ERP'den kesilmezse hakediş ile fatura arasında çift giriş oluşur | MVP'yi entegratör seçimine (K-08), test ortamı senaryolarına ve UBL-TR bakımına bağlamamak; ayda az sayıda hakediş faturasında çift giriş yükü küçük **[BELİRSİZ]** |
| Ön koşul | K-08 Aşama 1 girişinde kararlaştırılmış olmalı | K-08 Aşama 2'ye kadar |
| Risk | MVP büyür, gecikir | Geçici çift giriş, mutabakat farkı |

Fatura hacmi düşük ve entegratör henüz belli değilse Seçenek 2; firma zaten entegratörle çalışıyor ve API'si hazırsa Seçenek 1 makul.

### 02 ve 03'ün önerilerinden farklar

- **Fiyat farkı:** 02 MVP'ye koyuyor; burada firma Excel'de hesaplıyorsa MVP'de, değilse Aşama 2'de (gereksiz efor ve endeks hatası riskinden kaçınmak için).
- **e-Fatura gönderimi:** yukarıdaki iki seçenek.
- Yeni birim fiyat, iş artışı uyarısı ve ataşman 02 ile hizalandı (MVP, basit).

**Neden bu kadar?**
- Pilot keşfin özü proje maliyeti, hakediş ve Excel'den çıkış **[GEREKSİNİM]**; diğer modüllerin değeri bunlar olmadan ölçülemez.
- Sözleşme kalemi ağacı satın alma, taşeron ve fiyat farkının bağlandığı omurga (→ 01 §5).
- Lisans (resmî poz), mevzuat (e-Defter) ve doğruluk (belge okuma) riski yüksek işler dışarıda (→ 02 §7.2, 03 §7, 05 §5).
- Ekip küçük (varsayım: D-02'den çıkarım, kullanıcıyla teyit); kapsam kayması en büyük takvim riski.
- İlerleme ve iş aşamaları **[GEREKSİNİM]** MVP'de hakedişin kümülatif ilerlemesiyle karşılanır; planlanan–gerçekleşen iş programı Aşama 2'de.
- Malzeme ve ekipman **[GEREKSİNİM]** MVP'de gider satırı düzeyinde; stok ve ekipman ayrıntısı Aşama 2'de. Excel'de merkezîyse öne alınır **[BELİRSİZ]**.

**Bağlı kararlar:** K-03, K-05, K-06, K-08, K-11, K-12, K-13; yetki matrisi.
**Çıkış kriteri:** 1–2 tam hakediş/ay kapanışı Excel ile paralel (başlangıç önerisi; K-13); açıklanamayan mutabakat farkı yok (07 §5); dosya sahipleri kabul testini onayladı; geri yükleme testi başarılı; performans ve yedek hedefleri (→ 12) sağlandı.

## Aşama 2 — Operasyon ve e-belge (L)

**Hedef:** Gider tarafını kaynağında yakalamak.
- **M13** e-Fatura/e-Arşiv gönderimi (Seçenek 2 seçildiyse), entegratör soyutlama katmanı.
- **M7** satın alma, **M8** stok/depo, **M9** ekipman/demirbaş basit kaydı.
- **M10** taşeron, **M11** puantaj, **M21** saha günlüğü, **M4** planlanan–gerçekleşen iş programı.
- **M6** fiyat farkı (Aşama 1'de yoksa); çek/senet.
- Mobil uyumlu saha ekranları; çevrimdışı ihtiyacı **[BELİRSİZ]**.

**Bağlı kararlar:** K-08, K-11, mobil/çevrimdışı. **Giriş:** Aşama 1 çıkış kriteri sağlandı. **Çıkış:** entegratör test senaryoları (temel/tevkifatlı hakediş faturası, e-Arşiv) geçti; bir ay satın alma ve taşeron işlemleri yalnız ERP'de yürüdü; ilgili Excel'ler salt-okunur arşivde.

## Aşama 3 — Otomasyon ve derinlik (M)

- **M15** PDF/fotoğraf okuma: 2–3 yaklaşımın pilotu (Azure, bir LLM, açık kaynak OCR) → üç bantlı onay kuyruğu (→ 05 §3, §5).
- **M6** otomatik endeks (EVDS); **M5** kesin hesap/kesin hakediş.
- **M9** bakım planı; **M20** iş deneyim dosyası; nakit akışı tahmini.

**Bağlı karar:** K-09. **Giriş:** pilotta "güvenle kabul edilen ama yanlış alan" oranı müşteriyle belirlenen eşiğin altında. **Çıkış:** belge başı düzeltme süresinin azaldığı ölçüldü.

## Aşama 4 — Karara bağlı genişlemeler

- **M14** tam resmî muhasebe + e-Defter: yalnız K-05 "ERP içinde" ise; teknik yol yeniden değerlendirilir (→ 12).
- **Resmî poz kataloğu ve M19** teklif/yaklaşık maliyet: K-07 çözülürse.
- **Ürünleşme** (D-03): kiracı kaydı, abonelik, kiracı bazlı yedek, bölge seçimi (→ 06 §10).

## Paralel iş

- **M18** web sitesi: ERP'den bağımsız, her aşamada yapılabilir (S); K-14'e bağlı.

## Excel geçişinin aşamalara bağlanması (→ 07 §1)

| 07 geçiş adımı | Ne zaman |
|---|---|
| 1 Envanter · 2 Anlama · 3 İş kuralı kartları | Aşama 0 |
| 4 Alan eşleme · 5 Temizleme · 6 Örnek aktarım | Aşama 1 geliştirmesiyle, MVP dosyaları için |
| 7 Mutabakat · 8 Paralel çalışma · 9 Cut-over | Aşama 1 sonu |
| Aynı 3–9 döngüsü | Aşama 2 ve 3'te ilgili dosya grubu için |

**[ÖNERİ]** Excel'e dışa aktarma ve tanıdık tablo görünümü her aşamada korunur; "Excel'e geri dönme" aylık izlenir (→ 07 §5.2). Açılış bakiyesi ve tarihsel veri K-13 ile belirlenir **[BELİRSİZ]**.
