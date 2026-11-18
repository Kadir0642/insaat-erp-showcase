# Teknik Alternatifler (karar özeti)

> Belge numaraları (00–13), karar numaraları (K-xx, D-xx) ve "pilot keşif" kavramı için: [ARASTIRMA-OZETI.md](ARASTIRMA-OZETI.md#bu-belgeler-nasıl-okunur).

> 18.11.2026 · [araştırma 06](arastirma/06-teknik-mimari-altyapi.md)'nın karar odaklı özeti; 03, 04 ve R1–R3 ile birleştirildi. Çerçeve: D-02 (kullanıcı + Claude agent'ları, yaygın yığın), D-03 (çok kiracılığa hazır), D-04 (açık kaynak temel ile sıfırdan karşılaştırılacak). **Yaklaşım kararı verildi (D-05): kendi yazılımımız.** Yığın ve barındırma seçimi hâlâ açık (K-04).

## Alınan karar: kendi yazılımımız (D-05)

**Karar (ürün sahibi, 18.11.2026):** ürün sıfırdan, açık kaynak kütüphanelerle geliştirilir; Odoo, ERPNext gibi hazır açık kaynak ERP temeli kullanılmaz. e-Fatura özel entegratör API'siyle yapılır. Aşağıdaki karşılaştırma bu karara götüren değerlendirmedir ve kayıt için korunur.

**Gerekçeler:**

1. **Sade arayüz.** Karşılaştırmaya göre hazır bir ERP'nin arayüzünü sadeleştirmek zor; sıfırdan yazımda ekran düzeni tamamen elde.
2. **Ürünleşmeye ve lisansa serbestlik.** Ürünü ileride başka firmalara sunmak (D-03) için lisans koşullarından bağımsız olmak isteniyor; Odoo'da hukuki görüş gerekir (Community'de kapalı modül konusu ikincil kaynaklıdır) ve Enterprise'ta her müşteri abonelik alır.
3. **İnşaata özgü çekirdek her durumda yazılacak.** Hakediş, poz mantığı ve Excel geçişi hiçbir seçenekte hazır gelmiyor; hazır temel seçilse de bu çekirdek özel geliştirme olurdu.

**Yeniden değerlendirme koşulu:** müşteri yasal defter ve e-Defter'in ERP içinde tutulmasında ısrar ederse (K-05) karar yeniden açılır. O durumda bile ilk tercih, yasal defterin mali müşavirin programında kalıp ERP'nin ona veri aktarmasıdır.

**Kararın sonuçları ve açık kalanlar:**

- Hazır muhasebe gelmez; bu açığın ne kadar küçük olduğu K-05 yanıtına bağlıdır. Sıfırdan yolun ilk sürümü yavaş başlar (aşağıdaki tabloda görüldüğü gibi); bu bilinen bir bedeldir.
- "Odoo ile sıfırdan aynı mini senaryo" kavram kanıtı gereksiz hâle geldi.
- **Açık:** teknoloji yığını (önerilen yön TypeScript + PostgreSQL), bulut sağlayıcı ve barındırma (K-04; K-05 ve K-06 sonrası). Müşteri K-05'te tam muhasebeyi ERP içinde isterse barındırma seçimi de değişir.

## Karar için bilmeniz gerekenler (düz özet)

- **Hazır temel (Odoo)** ilk sürümü hızlandırır, muhasebe hazır gelir; ama arayüz sizin değil Odoo'nun olur ve yükseltmeler masraflıdır.
- **Sıfırdan** yazım yavaş başlar; arayüz, inşaat mantığı ve satış hakkı tamamen sizde kalır. Resmî defter mali müşavirde kalırsa muhasebe açığı küçülür.
- Muhasebe kararı (K-05) ve veri konumu (K-06) seçimi en çok değiştiren iki yanıttır.

## Yaklaşım seçenekleri (karardan önceki karşılaştırma)

Değerlendirme **[ÖNERİ]**; ölçüme değil belge incelemesine dayanır.

| Ölçüt | **Odoo temelli** | **Frappe temelli** (ERPNext'siz) | **Sıfırdan** (TypeScript + PostgreSQL) | **Hibrit** (hazır muhasebe + özel inşaat modülü) |
|---|---|---|---|---|
| İlk sürüm hızı | Hızlı | Orta | Yavaş | Orta |
| Sade arayüz **[GEREKSİNİM]** | Zor | Orta | Tam kontrol | Yalnız özel kısımda |
| TR muhasebe / e-belge | e-Fatura/e-Arşiv/e-İrsaliye Community, LGPL-3 (doğrulandı); e-Defter/TR raporlar Enterprise gerekebilir **[BELİRSİZ]**; ücretli Nilvera hesabı şart | Resmî TR yerelleştirme yok | Entegratör API'si ile e-Fatura | Hazır sistemde |
| Hakediş / poz | Özel geliştirme (hazır eklentiler ABD formatı) | Özel | Özel, tam uyum | Özel |
| Ürünleşme / lisans | Community'de kendi modülümüz kapalı olabilir (ikincil; hukuki görüş gerekir); Enterprise'ta her müşteri abonelik alır | Frappe MIT | Serbest | İki lisansa bağlı |
| Yükseltme yükü | Yüksek (özel modüller taşınmaz; $5–60 bin/sürüm, ikincil) | Orta | Düşük | Orta–yüksek |
| Çok kiracılık | Kiracı başına veritabanı (doğrulanmadı) | Kiracı başına site (doğrulandı) | Paylaşılan şema + `tenant_id` + RLS | Karışık |
| Agent verimliliği | Düşük–orta | Orta | Yüksek (değerlendirme, doğrulanmadı) | Orta |
| Lisans, 10 kullanıcı | Community 0; Custom ilk yıl ≈ €280/ay, sonra ≈ €339/ay (doğrulandı) | 0 | 0 | Ürüne göre |

ERPNext (GPLv3) TR yerelleştirmesi olmadığı için Frappe'den zayıf; düşük kodlu araçlar ana temel olarak önerilmez (→ 04 §3.3, 06 §1.1).

## Önceki öneri ve gerekçe **[ÖNERİ]** (değerlendirme; ölçülmedi; D-05 ile birincil seçenek kesinleşti)

1. **Birincil:** sıfırdan modüler monolit — TypeScript (React + Node) + PostgreSQL; kiracı ayrımı ilk günden `tenant_id` + RLS. Gerekçe: işin ağırlığı hakediş, poz, maliyet ve Excel geçişi, hiçbir açık kaynak ERP bunları vermiyor; sade arayüz; lisans serbestisi; yükseltme yükü düşük; yaygın, tip denetimli yığın agent'larla çalışmaya uygun görünüyor. Muhasebe: e-Fatura entegratör API'siyle, resmî defter SMMM'de (Seçenek B, → 03 §7).
2. **Alternatif:** Frappe Framework — yetki, rapor, baskı, kiracı altyapısı hazır; bedeli çerçeve bağımlılığı.
3. **Yığın alternatifi:** .NET 10 — para hassasiyeti en üst öncelikse. TypeScript'te para hiçbir zaman `number` tutulmaz (tip, lint, test).
4. **Karar yöntemi:** önerilen kısa kavram kanıtı, kararın verilmesiyle gereksiz hâle geldi.

## Kararı (yeniden değerlendirme) ve yığın seçimini değiştirebilecek yanıtlar

| Yanıt | Kimden | Etki |
|---|---|---|
| **K-05: tam resmî muhasebe + e-Defter ERP içinde** | Müşteri | **Odoo öne çıkar** (Enterprise olasılığıyla) veya hibrit; AB barındırma da sorunlu olur (aşağıda) |
| Hazır ERP özelleştirmesi ve abonelik bütçesi kabul | Müşteri | Odoo/hibrit lehine |
| Veri Türkiye'de zorunlu (K-06) | Müşteri | Yönetilen veritabanı seçeneği daralır, işletme yükü artar |
| Excel'ler muhasebe ağırlıklı, hakediş az | Müşteri | Hazır muhasebe temeli lehine |
| Ürünleşme yakın vadeli öncelik (D-03) | Kullanıcı | Sıfırdan/Frappe lehine — yalnız Odoo Enterprise kullanılacaksa; Community LGPL kapalı modüle izin verir (ikincil; hukuki görüş gerekir) |
| Şantiyede çevrimdışı mobil zorunlu | Müşteri | Her seçenekte ek iş (PWA/çevrimdışı kuyruk) **[BELİRSİZ]** |

D-05 sonrasında bu tablodaki Odoo/hibrit lehine satırlar yalnız yukarıdaki yeniden değerlendirme koşulunu (yasal defter ve e-Defter ERP içinde) tetikler; diğerleri yığın ve barındırma seçimini etkiler.

## Barındırma ve veri konumu

- **Yasal sınır:** e-belgelerin asıl muhafazası Türkiye'de; yurt dışında yalnız ikincil arşiv (VUK 509, tebliğ metni okundu → R1). e-Belge gönderip alan sistemin altyapısı da Türkiye'de olmalı (özel entegrasyon için; R1). **e-Defter ve beratların asıl kopyası mükellefin Türkiye'deki sisteminde** tutulur (→ 03 §6). AB barındırma KVKK yurt dışı aktarımıdır: standart sözleşme + 5 iş günü bildirim (doğrulandı).
- **İki öneri farklı yönde:** 03 muhasebe/personel verisi için **Türkiye'yi tercih** ediyor; 06 "Türkiye **zorunlu değilse** AB'de yönetilen PostgreSQL" diyor. Karar K-06 (kullanıcı + müşteri, hukuk teyidiyle). K-05 "C" çıkarsa Türkiye ağırlık kazanır.
- **[ÖNERİ]** e-Fatura/e-Arşiv asıl arşivi Türkiye'deki entegratörde; ERP kopyası ikincil (yeterliliği SMMM/hukuk teyidi **[BELİRSİZ]**).

| Seçenek | Artı | Eksi |
|---|---|---|
| AB'de yönetilen PostgreSQL | Otomatik yedek/yama; en az işletme yükü | KVKK aktarım süreci; müşteri kabulü |
| AWS İstanbul Local Zone | Türkiye'de | Yönetilen veritabanı (RDS) yok; fiyat doğrulanmadı |
| Yerli bulut / VDS | Türkiye'de, ucuz | SLA/otomasyon değişken |
| Hetzner / DigitalOcean (AB) | Ucuz | Hetzner'de yönetilen PG yok; 2026 fiyat/plan değişiklikleri |

## Performans, okunabilirlik, yedek **[ÖNERİ]** (→ 06 §6–8)

| Konu | Somut hedef |
|---|---|
| Ekran/API yanıtı | p95 < 500 ms; liste (10.000 satır) p95 < 1 s; standart rapor < 3 s; hakediş PDF < 5 s |
| Ölçek | 25 eşzamanlı kullanıcıda (küçük ekip başlangıç ölçeğinin birkaç katı) hedefler korunur, hata < %0,1 |
| Yük testi | k6 betikleri CI'da; senaryolar: sabah giriş yoğunluğu, aynı projede eşzamanlı hakediş, ay sonu rapor + dışa aktarım, 2 saatlik dayanıklılık |
| Yedek | Sürekli WAL arşivi + günlük/haftalık/aylık şifreli yedek, farklı konumda; **RPO ≤ 15 dk, RTO ≤ 4 saat**; aylık otomatik geri yükleme testi |
| 5–10 yıl okunabilirlik | Saklama 10 yıl + istisnalar; yıllık açık biçim arşiv (CSV/Parquet + veri sözlüğü), resmî çıktılar PDF/A, UBL-TR XML kopyası; kiracı bazlı "tüm verimi indir" |
| Erişilebilirlik | MVP aylık %99,5 |

## Maliyet bantları (aylık, KDV hariç, tahmini → 06 §5)

| Kalem | Bant |
|---|---|
| Altyapı 5–10 kullanıcı: minimum / önerilen / yüksek erişilebilirlik | ~€55–70 / ~€110–160 / ~$300–450 |
| Türkiye'de yerli VDS | ~$60–150 |
| 50 kullanıcı / 3–5 kiracı | ~€450–550 (Hetzner) / ~$800–1.400 (AWS, doğrulanmadı) |
| Odoo Custom, 10 kullanıcı lisansı | ilk yıl ≈ €280, sonra ≈ €339 (+ barındırma + Nilvera) |
| e-Fatura entegratörü | ~1.000–6.500 TL/yıl paket veya ~5–15 TL/belge (ikincil) |
| Belge okuma (300–3.000 sayfa) | ~$1–30 |
| Web sitesi | statik + CMS ~€0–15; yönetilen WordPress ~$5–25 |

Fiyatlar oynak; sipariş öncesi yenilenmeli. Asıl maliyet geliştirme ve bakım emeğidir.
