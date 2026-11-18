# Modül Haritası

> Belge numaraları (00–13), karar numaraları (K-xx, D-xx) ve "pilot keşif" kavramı için: [ARASTIRMA-OZETI.md](ARASTIRMA-OZETI.md#bu-belgeler-nasıl-okunur).

> 18.11.2026 · Aday kapsamdır, onaylı kapsam değildir (K-03). Etiket sütunu modülün pilot keşifte açıkça istenip istenmediğini gösterir: **[GEREKSİNİM]** pilot keşifte var · **[ÖNERİ]** araştırmadan geliyor · **[BELİRSİZ]** kapsamı/yöntemi netleşmedi. Aşama numaraları [YOL-HARITASI.md](YOL-HARITASI.md) ile aynıdır (1 = MVP).

## Modül listesi

| # | Modül | Kısa tanım | Etiket | Bağımlılıklar | Önerilen aşama |
|---|---|---|---|---|---|
| M1 | Kullanıcı–yetki | Kullanıcı adı/şifre girişi, rol ve proje bazlı erişim, işlem kayıtları; ek olarak 2FA, oluşturan ≠ onaylayan, işlem bazlı yetki **[ÖNERİ]** (→ 06 §6) | Giriş, rol/proje erişimi, işlem kaydı **[GEREKSİNİM]** (pilot keşif); yetki matrisi **[BELİRSİZ]** | — (temel) | 1 |
| M2 | Proje / ihale | İhale takip listesi → proje; sorumlu, aşamalar, durum. EKAP otomatik çekme yok (resmî API bulunamadı → 01 §1) | **[GEREKSİNİM]** | M1 | 1 (ihale listesi sade) |
| M3 | Sözleşme & teminat | Sözleşme türü (birim fiyat/ATGB/karma), ilan tarihi → kural sürümü, yer teslimi/geçici kabul tarihleri, avans, ceza oranı; teminat mektubu defteri (vade uyarısı, e-teminat/Takasbank ref.) (→ 02 §7.1, 01 §5) | Sözleşme **[ÖNERİ]** (pilot keşifteki ihtiyaçların önkoşulu, pilot keşifte adıyla geçmiyor); teminat **[ÖNERİ]** | M2 | 1 (teminat hafif, onaya bağlı) |
| M4 | İş programı / ilerleme | Aylık planlanan–gerçekleşen ilerleme, revizyon geçmişi, gecikme cezası tahmini. Gantt/CPM önerilen kapsam dışı | **[GEREKSİNİM]** (süre/ilerleme) / ayrıntı **[ÖNERİ]** | M3, M5 | 2 |
| M5 | Metraj – poz – hakediş | Sözleşme kalemleri (poz kodu serbest metin, kuruma bağlı), metraj/yeşil defter, ataşman, ara hakediş (kümülatif), parametrik kesintiler, yeni birim fiyat kaydı ve iş artışı uyarısı (basit), Excel/PDF çıktı. Resmî katalog önerilen kapsam dışı (→ 02 §7.2) | Poz ve hakediş **[GEREKSİNİM]** (pilot keşif); metraj, yeşil defter, kesinti alt işlevleri **[ÖNERİ]**; resmî katalog **[BELİRSİZ]** (lisans) | M3, M15 | 1 (02 ile hizalı); kesin hesap/kesin hakediş 3 |
| M6 | Fiyat farkı | F = An × B × (Pn − 1); elle endeks tablosu, hakediş başına dondurulmuş endeks; "kontrol hesabı" (→ 02 §5) | **[ÖNERİ]** (hakedişin parçası; firma hesaplıyor mu **[BELİRSİZ]**) | M5 | 2 (Excel'de varsa 1); EVDS otomatik 3 |
| M7 | Satın alma | Talep → teklif karşılaştırma → sipariş → irsaliye → fatura; projeye/iş kalemine bağlı (→ 01 §2) | Malzeme takibi **[GEREKSİNİM]**; tam zincir **[ÖNERİ]** | M2, M12 | 2 |
| M8 | Stok / depo | Şantiye depoları, transfer, direkt şantiyeye sarf; hareket bazlı | **[ÖNERİ]** | M7 | 2 |
| M9 | Ekipman / demirbaş | Kendi/kiralık makine, zimmet, yakıt/saat; bakım planı sonra | **[GEREKSİNİM]** (pilot keşif) | M2 | 2 (basit kayıt); bakım 3 |
| M10 | Taşeron | Taşeron sözleşmesi, taşeron hakedişi (aynı kalem yapısı), kesintiler, SGK belge kontrol listesi (→ 01 §5) | **[ÖNERİ]** (pilot keşifte yok) | M5, M12 | 2 |
| M11 | Personel / puantaj | Saha puantajı → proje maliyeti; bordro/İSG kapsam dışı önerisi | **[ÖNERİ]** (pilot keşif personeli yalnız kullanıcı rolü olarak anıyor; rol M1'de) | M2 | 2 |
| M12 | Ön muhasebe / cari / kasa-banka | Cari (idare, taşeron, tedarikçi), kasa/banka (ekstre içe aktarma), çek/senet, gider kaydı → proje/iş kalemi, hakediş mahsup fişi, SMMM'ye fiş aktarımı (→ 03 §5, §7) | Muhasebe/finans **[GEREKSİNİM]** (pilot keşif, kapsam bilerek açık); cari, kasa-banka, çek/senet alt işlevleri **[ÖNERİ]** | M1, M2 | 1 (çekirdek); çek/senet 2 |
| M13 | e-Belge | Gelen e-Fatura XML içe aktarma; giden e-Fatura/e-Arşiv entegratör API'si ile; entegratör soyutlama katmanı (→ 03 §2) | **[GEREKSİNİM]** (e-Fatura) | M12 | Gelen XML 1; gönderim 1 veya 2 (K-08, → 11) |
| M14 | Resmî muhasebe | Yevmiye, kebir, mali tablolar, e-Defter (Seçenek C) | **[GEREKSİNİM]** ama kapsam açık **[BELİRSİZ]** (K-05) | M12, M13 | 4 veya hiç (SMMM'de kalabilir) |
| M15 | Belge otomasyonu | Belge deposu + hızlı elle giriş + XML/karekod okuma + onay kuyruğu; PDF/fotoğraf okuma pilot sonrası (→ 05 §5) | Otomatik işleme **[GEREKSİNİM]**; PDF/fotoğraf yöntemi **[BELİRSİZ]** | M12, M13 | Depo + elle giriş + XML/karekod 1; PDF/fotoğraf okuma 3 |
| M16 | Raporlama / panel | Sahip paneli (hakediş geliri vs maliyet, nakit, proje durumu), proje/aşama/kalem raporları, her listede Excel/PDF dışa aktarım | **[GEREKSİNİM]** (pilot keşif) | M5, M12 (veri kaynağı) | 1 (temel); ileri raporlar 2–3 |
| M17 | Excel içe/dışa aktarım | Şablonlu içe aktarma (önizleme, hata satırı raporu), geçiş betikleri, dışa aktarım (→ 07 §5.2) | **[GEREKSİNİM]** (pilot keşif) | Tüm veri modülleri | 1 (kalıcı özellik) |
| M18 | Kurumsal web sitesi | İçerik yönetilebilir kurumsal site, ERP'den ayrı sistem (→ 06 §9) | **[ÖNERİ]** | Yok | Paralel, ayrı iş (S) |
| M19 | Teklif / yaklaşık maliyet | Analiz–rayiç motoru, teklif cetveli; resmî veri lisansına bağlı (→ 02 §3) | **[ÖNERİ]** / **[BELİRSİZ]** | M5, K-07 | 4 |
| M20 | İş deneyim arşivi | Kesin kabulde sözleşme+kabul+hakediş dosyasını derleme | **[ÖNERİ]** | M3, M5, M15 | 3 |
| M21 | Saha günlüğü | Telefondan günlük rapor (hava, kadro, ekipman, yapılan iş, fotoğraf), metraj girişi, eksik rapor uyarısı; çevrimdışı ihtiyacı **[BELİRSİZ]** (→ 01 §5) | **[ÖNERİ]** (pilot keşifte yok; K-11) | M2, M5 | 2 |
| M0 | Çok kiracılı altyapı | `tenant_id` + RLS, kiracı bazlı dışa aktarım; kullanıcıya görünmez (D-03) | **[ÖNERİ]** (D-03 kararına dayanır) | — | 1 (tasarım düzeyinde) |

Notlar:
- **[ÖNERİ]** Sözleşme kalemi, ERP'nin omurgasıdır: hakediş geliri, bütçe ve fiili maliyet aynı kalem ağacına bağlanır (→ 01 §5 "tek iş kalemi ağacı").
- **[ÖNERİ]** Mevzuata bağlı tüm oran ve süreler (kesinti, teminat, stopaj, B katsayısı) tarih aralıklı parametre tablosunda tutulur (→ 02 §7.3, 03 §4).
- **[BELİRSİZ]** Saha mobil/çevrimdışı ihtiyacı sorulmadı; mimariye henüz yansımadı (R1). M4, M11 ve M21 saha girişleri buna bağlı.

## Ana veri akışı

```
                 [M2 Proje/ihale] ──► [M3 Sözleşme & teminat]
                                            │ (tür, ilan tarihi → kural sürümü,
                                            │  kesinti/teminat parametreleri)
                                            ▼
 Excel / teklif cetveli ──[M17]──► Sözleşme kalemi (poz, birim, miktar, teklif BF)
                                            │
             ┌──────────────────────────────┼─────────────────────────────┐
             ▼                              ▼                             ▼
   [M4 İş programı]   [M21 Saha]─► Metraj / yeşil defter            Bütçe (kalem bazlı)
   planlanan ilerleme                       │                             ▲
             │                              ▼                             │ karşılaştırma
             └──────(uygulama ayı)──► [M5 Ara hakediş] ◄──[M6 Fiyat farkı]│
                                            │ kesintiler (KDV tevk., stopaj, teminat, avans)
                                            ▼
                              Hakediş faturası ──[M13 e-Fatura, entegratör]
                                            │
                                            ▼
                         [M12 Cari: idare alacağı] ──► tahsilat (kasa/banka)
                                            │
                                            └──► SMMM'ye fiş aktarımı / [M14]

 GİDER TARAFI
 [M7 Satın alma] ─► irsaliye ─► [M8 Stok] ─► şantiyeye sarf ─┐
 Gelen e-Fatura XML / fiş ─[M15 onay]─► gider kaydı ──────────┼─► Proje maliyeti
 [M10 Taşeron hakedişi] ──────────────────────────────────────┤   (proje / aşama /
 [M11 Puantaj] · [M9 Ekipman: yakıt, kira] ───────────────────┘    iş kalemi)
                                                                       │
                                     [M12 Cari: tedarikçi/taşeron borcu]│
                                                                       ▼
                         [M16 Panel: hakediş geliri – maliyet = proje kâr/zarar]
```

Okuma: gelir hattı "sözleşme kalemi → metraj → hakediş → fatura → cari"; gider hattı "satın alma → stok → proje maliyeti" ve "belge → onay → gider → proje maliyeti". İki hat aynı iş kalemi ağacında buluşur **[ÖNERİ]**.

## Bağımlılık özeti (kritik yol)

1. **M1 + M0** her şeyin önkoşulu.
2. **M2 → M3 → M5** hakediş zinciri; M5 olmadan M6, M10 ve M16'nın gelir tarafı olmaz.
3. **M12** gider tarafının ve fatura/cari'nin önkoşulu; M13 ve M14 buna bağlı.
4. **M17** geçişte her modülün beslenme yoludur; Gerçek Excel dosyaları analiz edildiğinde modül öncelikleri değişebilir **[BELİRSİZ]** (→ 07).
5. **M14** ve **M19** müşteri kararlarına (K-05, K-07) bağlıdır; erken tasarımda yalnız veri alanları ayrılır.
