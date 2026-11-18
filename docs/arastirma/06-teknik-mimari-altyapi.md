# 06 — Teknik Mimari, Altyapı, Güvenlik ve Maliyet

> Belge numaraları (00–13), karar numaraları (K-xx, D-xx) ve "pilot keşif" kavramı için: [ARASTIRMA-OZETI.md](../ARASTIRMA-OZETI.md#bu-belgeler-nasıl-okunur).

> Agent F · 18 Kasım 2026 · Araştırma belgesidir; teknoloji seçimi değildir. Nihai karar kullanıcıda (K-04).
> Etiketler: **[GEREKSİNİM]** pilot keşifte açık ihtiyaç · **[ÖNERİ]** araştırmaya dayalı öneri · **[BELİRSİZ]** netleşmemiş.
> Tüm fiyatlar **tahmindir**, KDV hariçtir ve belirtilen tarihte üçüncü taraf ya da resmî sayfadan alınmıştır; sipariş öncesi yeniden kontrol edilmelidir.

## Özet

1. **[ÖNERİ]** Temel yaklaşım için öneri: **sıfırdan, modüler monolit bir web uygulaması** (TypeScript + PostgreSQL). Odoo/ERPNext ilk sürümü hızlandırır ama sade UX, ürünleştirme lisansı ve yıllık sürüm yükseltme yükü tek geliştirici için uzun vadede pahalıdır. İkinci sırada güçlü alternatif: **Frappe Framework (MIT) üzerine özel uygulama** (ERPNext'siz).
2. **[ÖNERİ]** Çok kiracılık: ilk günden **paylaşılan şema + `tenant_id` + PostgreSQL satır düzeyi güvenlik (RLS)**. Tek müşteride neredeyse sıfır ek maliyetle "hazır olma" sağlar; büyük kiracı ileride ayrı veritabanına taşınabilir.
3. **[BELİRSİZ]** Veri konumu kritik karar: e-belgelerin asıl muhafazası **Türkiye'de** olmalı (VUK 509; ikincil kopya yurt dışında olabilir). AB'de barındırma KVKK m.9 kapsamında yurt dışı aktarımdır → standart sözleşme + 5 iş günü içinde Kuruma bildirim. Büyük sağlayıcılardan Türkiye'de tam bölge yok; **AWS İstanbul Local Zone (Mayıs 2026)** var, Google–Turkcell bölgesi duyuruldu ama çalışmıyor.
4. **[ÖNERİ]** 5–10 kullanıcı için tahmini altyapı: **minimum ~€55–70/ay**, **önerilen ~€110–160/ay**, **yüksek erişilebilirlik ~$300–450/ay**. Lisans maliyeti yok (sıfırdan); e-Fatura entegratör ücretleri ayrı (agent 03).
5. **[ÖNERİ]** Güvenlik hedefi **OWASP ASVS 5.0 Seviye 2**; parola (Argon2id) + zorunlu TOTP 2FA (yönetici/sahip), rol × proje yetki modeli, değiştirilemez denetim kaydı, finansal kayıtlarda silme yerine ters kayıt.
6. **[ÖNERİ]** Yedek: WAL tabanlı PITR + günlük dump + farklı konum kopyası + **aylık otomatik geri yükleme testi**; MVP için **RPO ≤ 15 dk, RTO ≤ 4 saat**. Yıllık açık biçim arşivi (CSV/Parquet + PDF/A).
7. **[ÖNERİ]** Kurumsal web sitesi ERP'den **ayrı** (statik site + hafif CMS); maliyet ~€0–25/ay.

---

## 1. Yaklaşım karşılaştırması: hazır açık kaynak temel mi, sıfırdan mı?

### 1.1 Seçeneklerin teknik profili

**(a) Odoo Community / Enterprise üzerine modül**
- Lisans: Community **LGPLv3**; kendi modüllerimiz kapalı kaynak olabilir. Enterprise ise "Odoo Enterprise Edition License"; Enterprise kodunu dağıtmak/alt lisanslamak yasak (ikincil kaynak: [Odoo forum](https://www.odoo.com/forum/help-1/lgpl-v3-odoo-community-license-to-be-used-in-a-commercial-softwaresaas-155092), [Cybrosys](https://cybrosys.com/blog/an-overview-of-different-odoo-16-licenses), erişim 18.11.2026). Ürünleştirmede Enterprise kullanılırsa **her müşteri kendi Odoo aboneliğini almak zorunda** kalır.
- Fiyat: odoo.com/pricing sayfası Standard **€14,90**, Custom **€27,90** kullanıcı/ay — bunlar **ilk 12 ay indirimli** rakamlar; indirimsiz liste Standard **€18,60**, Custom **€33,90** (ülkeye göre değişebilir). Odoo.sh, on-premise ve harici API yalnız Custom planda (doğrulandı: resmî kaynak, [odoo.com/pricing](https://www.odoo.com/pricing), 18.11.2026). 10 kullanıcı Custom: **ilk yıl ≈ €280/ay, sonrası ≈ €339/ay** + barındırma.
- Türkiye yerelleştirmesi (Odoo 19):
  - **Community deposunda, LGPL-3:** `l10n_tr` (hesap planı, vergiler), `l10n_tr_nilvera` (bağlantı altyapısı), `l10n_tr_nilvera_einvoice` (yalnız **temel senaryo** e-Fatura/e-Arşiv), `l10n_tr_nilvera_einvoice_extended` (diğer fatura tipleri/senaryolar), `l10n_tr_nilvera_edispatch` (e-İrsaliye) (doğrulandı: resmî kaynak, [Odoo 19 Türkiye dokümanı](https://www.odoo.com/documentation/19.0/applications/finance/fiscal_localizations/turkiye.html), [manifest](https://raw.githubusercontent.com/odoo/odoo/19.0/addons/l10n_tr_nilvera_einvoice/__manifest__.py) ve kardeş modüller, 18.11.2026; R1 incelemesiyle teyit).
  - **Community'de yok:** `l10n_tr_reports` (Türkiye mali raporları) Community deposunda bulunmuyor → büyük olasılıkla Enterprise. Dokümanda e-Defter (e-Ledger) dosyası Genel Muhasebe raporu üzerinden üretiliyor; bu rapor Enterprise muhasebe raporlarına ait olduğundan **e-Defter için Enterprise gerekebilir** (çıkarım, doğrulanmadı — Enterprise deposu kapalı, dokümanda açıkça yazmıyor).
  - **Önemli koşul:** Odoo'daki **tüm e-belge işlevi (e-Fatura, e-Arşiv, e-İrsaliye, e-Defter gönderimi) ücretli bir Nilvera (özel entegratör) hesabına bağlıdır**; Odoo lisansı bu ücreti kapsamaz. Yani Odoo Community seçilse bile entegratör maliyeti ayrıca vardır (sıfırdan seçenekteki entegratör API maliyetine benzer).
- Sürüm yükseltme: Yılda bir ana sürüm; Odoo'nun yükseltme servisi çekirdek veritabanını taşır, **özel modülleri taşımaz**. Danışman tahminleri: özelleştirilmiş sistemlerde sürüm başına $5.000–60.000+ (ikincil kaynak, satıcı blogları: [Ventor](https://ventor.tech/odoo/how-to-do-odoo-upgrade/), [Cybrosys](https://www.cybrosys.com/blog/how-much-should-you-budget-for-an-odoo-20-migration), 18.11.2026).
- Çok kiracılık: veritabanı başına kiracı (dbfilter) modeli (doğrulanmadı).

**(b) ERPNext / Frappe üzerine uygulama**
- Lisans: **Frappe Framework MIT**, **ERPNext GPLv3** (doğrulandı: resmî kaynak, [Frappe lisans sayfası](https://docs.frappe.io/legal/others/license-and-trademark), 18.11.2026). GPLv3 yalnız *dağıtımda* kaynak açma yükümlülüğü doğurur; SaaS olarak sunmak dağıtım sayılmaz (AGPL değil; ikincil yorum, hukuki görüş gerekir). Müşteriye kurulum dosyası verirsek ERPNext'ten türeyen kod GPLv3 olmalıdır **[BELİRSİZ: hukuki görüş]**.
- Çok kiracılık: Bench, **her kiracıya ayrı veritabanı ve dosya klasörü (site)** verir (doğrulandı: resmî kaynak, [Scaling ERPNext](https://erpnext.com/files/Scaling%20ERPNext.pdf)).
- Türkiye yerelleştirmesi zayıf: resmî Türk hesap planı/e-Fatura modülü bulunamadı; topluluk deposu (logedosoft/ERPNext-Turkish-Delight) ve sipariş üzerine ticari modüller var, lisans ve sürüm uyumu **(doğrulanmadı)** ([Frappe forum](https://discuss.frappe.io/t/turkey-e-invoice-sending-app/63282)).
- Hibrit varyant: **ERPNext'i almadan yalnız Frappe Framework** üzerine kendi uygulamamızı yazmak (DocType, yetki, rapor, baskı şablonu, REST API, site başına kiracı hazır gelir; MIT lisans).

**(c) Sıfırdan özel web uygulaması**
- Tüm ekranlar, veri modeli ve lisans bizde. Muhasebe çekirdeği (hesap planı, yevmiye, KDV, e-belge entegratör bağlantısı) sıfırdan yazılmalı — en büyük iş yükü ve risk bu.

**(d) Düşük kodlu araçlar (Retool, Appsmith, Budibase, NocoBase vb.)**
- Dahili paneller için hızlı; ancak ürünleştirme, karmaşık muhasebe mantığı, satıcı bağımlılığı ve bazılarında AGPL/ticari lisans kısıtları nedeniyle **ana ERP temeli olarak önerilmez** **[ÖNERİ]**. Gerekirse yalnız iç yönetim/raporlama için düşünülebilir.

### 1.2 Karşılaştırma (1 = zayıf, 5 = güçlü; değerlendirme **[ÖNERİ]**, ölçülmüş değil)

| Ölçüt | Odoo | ERPNext | Frappe (ERPNext'siz) | Sıfırdan |
|---|---|---|---|---|
| İlk kullanılabilir sürüme kadar süre | 4 | 4 | 3 | 2 |
| Sade, kolay kullanılan UX yapabilme **[GEREKSİNİM]** | 2 | 2 | 3 | 5 |
| Ticari satış/lisans serbestisi | 3 (Community) / 1 (Enterprise) | 3 | 5 | 5 |
| Sürüm yükseltme yükü (yüksek puan = düşük yük) | 2 | 2 | 3 | 4 |
| Çok kiracılık esnekliği | 3 | 3 | 3 | 5 |
| Türkiye muhasebe/e-belge hazır olma | 4 | 1 | 1 | 1 (entegratör API ile) |
| İnşaat/hakediş/poz uyumu | 2 | 2 | 3 | 5 |
| Tek geliştirici + AI agent verimliliği | 2 | 2 | 3 | 5 |

Gerekçeler:
- **AI agent uyumu [ÖNERİ]:** Odoo/Frappe'de kod yazmak çerçeveye özgü kurallara (XML görünüm kalıtımı, ORM uzantıları, sürüme göre değişen API'ler) bağlıdır; agent'lar eski sürüm kalıplarını karıştırmaya yatkındır. Yaygın genel amaçlı yığınlarda (TypeScript/React, .NET, Django) eğitim verisi, tip denetimi ve test araçları daha bol olduğundan hata erken yakalanır. Bu bir gözlem/değerlendirmedir **(doğrulanmadı)**.
- **Kapsamın asıl ağırlığı** hakediş, poz/birim fiyat, proje maliyeti ve Excel geçişidir — hiçbir açık kaynak ERP bunu hazır vermez; her seçenekte özel geliştirilecek.
- **Muhasebe açığı:** Sıfırdan seçeneğin en büyük dezavantajı. Hafifletme: e-Fatura/e-Arşiv'i GİB onaylı **özel entegratörün API'si** üzerinden göndermek (agent 03), resmî defteri ilk aşamada mali müşavirin programında bırakıp ERP'den dışa aktarım vermek (K-05'e bağlı **[BELİRSİZ]**).

### 1.3 Öneri **[ÖNERİ]**
1. **Birincil:** Sıfırdan, modüler monolit. Gerekçe: sade UX, inşaat odaklı veri modeli, tam lisans serbestisi, çok kiracılığı baştan tasarlama, AI agent verimliliği, yıllık zorunlu sürüm göçü yok.
2. **Alternatif:** Frappe Framework üzerine özel uygulama — altyapıyı (yetki, rapor, baskı, kiracı) hızlı kazanmak isteniyorsa. Bedeli: çerçeveye bağımlılık, sade UX için Frappe arayüzünü aşma ihtiyacı.
3. **Muhasebe çekirdeği tam ERP içinde istenirse** (K-05 "içinde" çıkarsa) Odoo yeniden değerlendirilmeli; e-Defter/mali raporlar için Enterprise gerekebileceği (yukarıda) hesaba katılmalı. Bu durumda inşaat modülleri Odoo modülü olarak yazılır ve UX hedefinden taviz verilir.
4. Yukarıdaki puanlar ölçüme değil değerlendirmeye dayanır ve sıfırdan seçeneğe yön verir; nihai karar **K-04/K-05 sonrası**, agent 04'ün önerdiği **kavram kanıtı (PoC)** ile birlikte verilmelidir.

---

## 2. Sıfırdan seçeneği için yığın alternatifleri

| | **A. TypeScript tam yığın** | **B. .NET 10 (C#)** | **C. Python / Django** |
|---|---|---|---|
| Örnek bileşenler | React + Vite (SPA), Node.js API (Fastify/NestJS/Hono), Drizzle veya Prisma ORM, Zod şema doğrulama | ASP.NET Core + EF Core; arayüz React veya Blazor | Django + DRF; arayüz React veya HTMX |
| Destek takvimi | Node 24 LTS EOL 30.04.2028; Node 26 LTS 28.10.2026 (ikincil kaynak, [endoflife.date](https://endoflife.date/nodejs)) | .NET 10 LTS: 11.11.2025 → 14.11.2028 (doğrulandı: resmî kaynak, [Microsoft](https://dotnet.microsoft.com/en-us/platform/support/policy/dotnet-core)) | Django LTS döngüsü (doğrulanmadı) |
| Artılar | Önde ve arkada tek dil; ortak tipler (form doğrulaması iki uçta aynı); ERP tablo/form ekosistemi en zengin (TanStack Table, AG Grid, React Hook Form); AI agent'ların en çok örnek gördüğü yığınlardan | `decimal` tipi yerleşik (finans için ideal); güçlü tip sistemi; ASP.NET Identity'de 2FA hazır; uzun LTS; kurumsal olgunluk | Yerleşik `Decimal`; Django admin ile hızlı iç paneller; olgun auth/ORM/migration; veri analizi/OCR/AI kütüphaneleri |
| Eksiler | JS `number` kayan noktalı → para için **mutlaka** decimal kütüphanesi ve kural/lint disiplini; npm bağımlılık zinciri riski; çerçeve çeşitliliği (karar yorgunluğu) | Önde ayrı dil (React ise TS) → iki dil; bazı PDF kütüphaneleri ticari lisanslı (QuestPDF topluluk lisansı yıllık ciro < $1M için ücretsiz, ikincil/resmî: [questpdf.com](https://questpdf.com/pricing.html)) | Tip güvenliği isteğe bağlı (mypy/pyright); zengin SPA için yine TS gerekir → iki dil; eşzamanlılık modeli daha zayıf |
| PDF / Excel | HTML→PDF (Playwright/Chromium) veya pdfmake; ExcelJS | QuestPDF, ClosedXML | WeasyPrint, openpyxl |
| ERP uygunluğu | 4/5 | 5/5 | 4/5 |
| AI agent uyumu | 5/5 | 4/5 | 4/5 |

**Öneri [ÖNERİ]:** **A (TypeScript) birincil, B (.NET) güçlü alternatif.** Tek kişinin yıllarca bakımı için tek dil ve paylaşılan tipler belirleyici; finansal doğruluk riski "para asla `number` değildir" kuralının kodda (markalı `Money` tipi, ESLint kuralı, testler) zorlanmasıyla yönetilir. Para hassasiyeti en üst öncelikse B seçilmeli.

### 2.1 Veritabanı **[ÖNERİ]: PostgreSQL (17/18)**
- PostgreSQL 18, 25.09.2025'te çıktı; yerleşik `uuidv7()`, sanal üretilmiş sütunlar, asenkron I/O (doğrulandı: resmî kaynak, [postgresql.org](https://postgresql.org/about/news/postgresql-18-released-3142/)).
- Alternatifler: MySQL/MariaDB (RLS yok), SQL Server (lisans maliyeti), SQLite (çok kullanıcılı sunucu için uygun değil). PostgreSQL; RLS, `numeric`, JSONB, tam metin arama, olgun yedek araçları ve tüm bulutlarda yönetilen sürümüyle en dengeli seçim.
- **Para/ondalık:** Tutarlar `numeric(19,4)`, birim fiyat/miktar için `numeric(18,6)` gibi açık hassasiyet; `float/real/money` tipi yasak; para birimi sütunu (TRY, USD, EUR) ve kur tablosu; yuvarlama kuralı (kuruş, satır mı toplam mı) iş kuralı olarak belgelenmeli **[BELİRSİZ: gerçek Excel dosyalarıyla doğrulanacak]**.
- **İşlem bütünlüğü:** Fiş/hakediş kaydı tek transaction; çift taraflı kayıtta borç = alacak kısıtı (deferred constraint veya uygulama + test); belge numaraları için boşluksuz sıra (kilitli sayaç tablosu).
- **Denetim izi:** (1) Uygulama düzeyinde olay günlüğü (kim, ne zaman, hangi kayıt, eski/yeni değer, IP); (2) kritik tablolarda tetikleyiciyle `audit_log` (yalnız INSERT izni olan tablo); (3) isteğe bağlı hash zinciri ile kurcalama tespiti. Onaylanmış finansal kayıt güncellenmez/silinmez; düzeltme **ters kayıtla** yapılır.
- **Zaman:** `timestamptz` + `Europe/Istanbul` görüntüleme; mali dönem kilitleme.

---

## 3. Çok kiracılık modelleri

| Model | Ayrım gücü | İşletme yükü | Maliyet | Not |
|---|---|---|---|---|
| **Paylaşılan şema + `tenant_id` + RLS** | Orta–yüksek (RLS doğru kurulursa) | En düşük; tek migration | En düşük | SaaS'ta en yaygın başlangıç |
| Kiracı başına şema | Yüksek | Migration her şemada; yüzlerce şemada zorlaşır | Düşük | Orta yol |
| Kiracı başına veritabanı | En yüksek; kiracı bazlı yedek/geri yükleme kolay | En yüksek (bağlantı, izleme, migration ×N) | Yüksek | Odoo/Frappe'nin modeli |

**Öneri [ÖNERİ]: Paylaşılan şema + RLS, "taşınabilir" tasarımla.**
- Her iş tablosunda `tenant_id NOT NULL`; bileşik yabancı anahtarlar (`tenant_id, id`) ile kiracılar arası referans imkânsız.
- RLS politikası `tenant_id = current_setting('app.tenant_id')::uuid`; tablolarda `FORCE ROW LEVEL SECURITY`; uygulama **süper kullanıcı olmayan, BYPASSRLS'siz** rolle bağlanır; her istekte transaction başında `SET LOCAL app.tenant_id`.
- Otomatik test: "A kiracısı B'nin verisini göremez" testleri CI'da zorunlu.
- Kiracı bazlı dışa aktarım/silme betiği baştan yazılır → ileride büyük ya da özel istekli kiracıyı ayrı veritabanına taşımak mümkün ("hibrit/silo" büyüme yolu).
- Tek müşteride ek maliyet: yalnız tasarım disiplini; altyapı maliyeti sıfır.

---

## 4. Barındırma ve veri konumu

### 4.1 Mevzuat çerçevesi (ayrıntı agent 03'te)
- **KVKK m.9 (7499 sayılı Kanun ile 2024 değişikliği):** Yurt dışı aktarım; yeterlilik kararı, **uygun güvenceler** (standart sözleşme, bağlayıcı şirket kuralları, taahhütname) veya arızi aktarım istisnalarına dayanır. Kurum 4 tip standart sözleşme yayımladı (sorumlu→işleyen tipi barındırma için tipik) (doğrulandı: resmî kaynak, [KVKK Standart Sözleşmeler](https://www.kvkk.gov.tr/Icerik/7929/Standart-Sozlesmeler)). İmzadan sonra **5 iş günü içinde** Kuruma bildirim (KEP/fiziki/Bildirim Modülü); metin değiştirilemez, imza tarihleri yazılmalı (ikincil kaynak + resmî duyuru: [KVKK duyurusu](https://www.kvkk.gov.tr/Icerik/8170/Yurt-Disina-Kisisel-Veri-Aktariminda-Kullanilacak-Standart-Sozlesmelerde-Dikkat-Edilmesi-Gereken-Hususlara-Iliskin-Kamuoyu-Duyurusu), [Erdem & Erdem](https://www.erdem-erdem.av.tr/bilgi-bankasi/standart-sozlesme-bildirim-modulu-hakkinda-kamuoyu-duyurusu)).
- **VUK 509 Sıra No'lu Tebliğ:** e-belgelerin muhafazası **Türkiye sınırları içinde** yapılmalı; yurt dışında **ikincil** arşiv engellenmez; e-Defter ve beratları mükellefin kendi sistemlerinde, ikincil kopya izinli entegratörde (ikincil kaynak, [alomaliye özet](https://www.alomaliye.com/2019/12/23/vuk-509-genel-tebligi-uygulamalarina-iliskin-sikca-sorular/); 573 sayılı tebliğ değişiklikleri kontrol edilmeli **(doğrulanmadı)**).
- **Mimari sonucu [ÖNERİ]:** e-Fatura/e-Arşiv asıl arşivini **izinli özel entegratörde (Türkiye)** tutmak; ERP'deki kopya ikincil kabul edilebilir. Bunun yeterli olup olmadığı **[BELİRSİZ: mali müşavir/hukukçu teyidi]**.

### 4.2 Sağlayıcılar (18.11.2026 itibarıyla)

| Sağlayıcı | Türkiye'de altyapı | Yönetilen PostgreSQL | Not |
|---|---|---|---|
| AWS | **İstanbul Local Zone** (20.05.2026 GA): EC2 C7i/M7i/R7i, EBS, S3 One Zone-IA, ALB, ECS/EKS; **RDS yok**; ana bölge Frankfurt (doğrulandı: resmî kaynak, [AWS duyuru](https://aws.amazon.com/about-aws/whats-new/2026/05/aws-local-zones-istanbul-turkiye/)) | Frankfurt'ta RDS; İstanbul'da EC2 üzerinde kendi PG | Local Zone fiyatları **(doğrulanmadı)** |
| Google Cloud | Turkcell ortaklığıyla `turkiye1` bölgesi **duyuruldu, çalışmıyor**; hedef ~2028–2029 (ikincil kaynak, [DCD](https://www.datacenterdynamics.com/en/news/google-and-turkcell-team-up-for-cloud-region-and-data-center-in-t%C3%BCrkiye/), [Daily Sabah](https://www.dailysabah.com/business/tech/big-tech-bets-on-turkiye-as-cloud-investments-accelerate)) | Cloud SQL (AB bölgeleri) | — |
| Azure | Türkiye bölgesi duyurusu bulunamadı (doğrulanmadı; 2023 tarihli MS yanıtı "duyurulmuş bölge yok") | AB bölgeleri | — |
| Huawei Cloud | TR-Istanbul bölgesi (3 AZ) olduğu ifade ediliyor — **doğrulanamadı** (ikincil arama özeti; bağımsız incelemede açılan resmî sayfada bölge adı görülmedi) ([Huawei altyapı](https://huaweicloud.com/eu/de-de/about/global-infrastructure.html)) | RDS for PostgreSQL'in İstanbul'da varlığı **(doğrulanmadı)** | Bölge ve hizmet varlığı doğrulanmadı |
| Hetzner (DE/FI) | Yok | **Yok** (kendin yönet) | 2026'da iki zam (Nisan, 15 Haziran); CX/CAX siparişe kapalı görünüyor (ikincil kaynak, [bitdoze, 20.10.2026](https://www.bitdoze.com/hetzner-cloud-cost-optimized-plans/)) |
| DigitalOcean (AMS/FRA) | Yok | Var; HA için ikinci düğüm aynı fiyattan; **30.11.2026'dan itibaren standby yalnız Advanced Edition'da** (doğrulandı: resmî kaynak, [DO plan değişikliği](https://docs.digitalocean.com/release-notes/upcoming/dbaas-plan-changes/)) | — |
| Yerli (Turkcell Bulut, Türk Telekom Bulut, Natro, Turhost, Teknosos vb.) | Var | Kurumsal teklif usulü; yönetilen PG liste fiyatı bulunamadı | 8 GB RAM VDS ≈ $12–37/ay (ikincil kaynak, [karekod.org, 26.09.2026 kontrol](https://www.karekod.org/blog/en-ucuz-vds-fiyatlari/)); API/otomasyon ve SLA olgunluğu sağlayıcıya göre değişir |

### 4.3 Yönetilen veritabanı mı, kendin mi?
- **Yönetilen (RDS, DO, Cloud SQL):** Otomatik PITR, yama, yedek, failover; tek geliştiricinin gece uykusu için değerli. Bedeli 2–3 kat fiyat ve (Türkiye'de) yokluk.
- **Kendin yönet:** Ucuz, konum serbest; ama pgBackRest/WAL-G, izleme, yama, geri yükleme testi sorumluluğu sende. Konteyner + hazır betiklerle yönetilebilir; agent'larla otomasyon yazılabilir.
- **Öneri [ÖNERİ]:** Veri Türkiye'de zorunlu değilse → **AB'de yönetilen PG** (KVKK standart sözleşmesiyle). Türkiye zorunluysa → **AWS İstanbul Local Zone veya yerli bulutta kendi yönetilen PG + pgBackRest**, şifreli ikincil yedek. Hangisi olduğu pilot keşif sorusudur **[BELİRSİZ]**.

---

## 5. Maliyet (tahmini, aylık, KDV hariç, altyapı yalnız)

Fiyat kaynakları: Hetzner — [bitdoze tablosu, 20.10.2026](https://www.bitdoze.com/hetzner-cloud-cost-optimized-plans/) (CPX22 €19,49; CPX32 €35,49; CCX13 €42,99; CCX23 €85,99; CCX33 €138,49; yedek ≈ sunucu fiyatının %20'si — ikincil kaynak); DigitalOcean HA PG $30 + $30 standby'dan başlar ([DO fiyat](https://docs.digitalocean.com/products/databases/postgresql/details/pricing/)); AWS RDS db.t4g.medium Multi-AZ ≈ $95–110/ay ([sparecores](https://sparecores.com/database/aws/db.t4g.medium), ikincil kaynak). Erişim 18.11.2026.

### 5.1 Tek müşteri, 5–10 kullanıcı

| Seviye | Bileşenler (örnek) | Tahmini aylık |
|---|---|---|
| **Minimum** | Hetzner CPX32 (4 vCPU/8 GB) tek sunucu: uygulama + PG; sunucu yedeği; harici nesne depolamaya WAL/dump; Cloudflare ücretsiz; Let's Encrypt | **~€55–70** |
| **Önerilen** | Uygulama CPX22 + ayrı DB CCX13 (ayrılmış vCPU) + pgBackRest → farklı konum nesne depolama + izleme/hata takibi ücretsiz katmanları; *veya* DO droplet + yönetilen PG (HA'sız) | **~€110–160** |
| **Yüksek erişilebilirlik** | AWS Frankfurt: 2× EC2 (iki AZ) + ALB + RDS PG Multi-AZ + S3 (sürümlenmiş, başka bölgeye kopya) + CloudWatch | **~$300–450** |
| Türkiye'de tutma varyantı | Yerli VDS (8 GB) ×2 (uygulama, DB) + ikinci yerli sağlayıcıda yedek; *veya* AWS İstanbul Local Zone EC2 + EBS + S3 One Zone-IA | **~$60–150** (yerli) / **doğrulanmadı** (Local Zone) |

Ayrıca (altyapı dışı, tahmin): alan adı ~$15/yıl; işlemsel e-posta ~$0–20/ay; e-Fatura özel entegratör kontör/abonelik (agent 03); OCR/AI belge okuma kullanım bazlı (agent 05 vb.).

### 5.2 50 kullanıcı / 3–5 kiracı
- Hetzner: 2× CCX23 uygulama + CCX33 birincil DB + CCX33 replika + yük dengeleyici + nesne depolama → **~€450–550/ay**.
- AWS Frankfurt: Auto Scaling 2–3 EC2 + RDS db.m7g.large Multi-AZ + ALB + S3/yedek → **~$800–1.400/ay** (doğrulanmadı, hesaplayıcıyla teyit gerekir).
- Kiracı başına altyapı maliyeti 50 kullanıcıda ~€100–300/kiracı/ay aralığına iner — fiyatlandırma modeli için girdi **[ÖNERİ]**.

Karşılaştırma için: Odoo Custom 10 kullanıcı yalnız lisans **ilk yıl ≈ €280/ay, sonrası ≈ €339/ay** (barındırma ve Nilvera entegratör ücreti hariç).

---

## 6. Güvenlik **[GEREKSİNİM: güvenli kimlik doğrulama, rol/proje bazlı erişim, işlem kayıtları]**

Hedef standart: **OWASP ASVS 5.0 (30.05.2025), Seviye 2** (doğrulandı: resmî kaynak, [OWASP ASVS](https://owasp.org/www-project-application-security-verification-standard/), [GitHub](https://github.com/OWASP/ASVS)).

**Kimlik doğrulama [ÖNERİ]**
- Kullanıcı adı/e-posta + parola (**Argon2id**, sızdırılmış parola listesi kontrolü, en az 12 karakter).
- **TOTP 2FA**: üst yönetim, yönetici ve muhasebe rolleri için zorunlu; diğerleri için önerilir. Passkey/WebAuthn ileride.
- Oturum: sunucu tarafı oturum, `HttpOnly; Secure; SameSite=Lax` çerez, boşta 30 dk / mutlak 12 saat zaman aşımı, aktif cihaz listesi ve uzaktan oturum kapatma; giriş denemesi hız sınırı ve kilitleme.
- Çok kiracılı üründe ileride kiracı bazlı SSO (OIDC) seçeneği.

**Yetkilendirme [ÖNERİ]**
- **RBAC + proje kapsamı (ABAC-lite):** izin = rol (ör. "Şantiye Şefi") × kapsam (atandığı projeler) × işlem (görüntüle/oluştur/onayla/sil). Sahipler tüm projeler; şantiye şefi yalnız kendi projeleri.
- Yetki kontrolü tek merkezde (policy katmanı), hem API'de hem rapor sorgularında; kiracı ayrımı ayrıca RLS ile veritabanında.
- Onay akışları (hakediş, ödeme) için görevler ayrılığı: oluşturan ≠ onaylayan.
- Yetki matrisi pilot keşifte netleşecek **[BELİRSİZ]**.

**Diğer kontroller [ÖNERİ]**
- OWASP Top 10 için: parametreli sorgular/ORM, çıktı kaçışlama, CSP başlığı, CSRF koruması, dosya yüklemede tür/boyut kontrolü ve virüs taraması, SSRF'ye karşı dış istek beyaz listesi.
- Şifreleme: TLS 1.2+ (HSTS); disk ve yedek şifreleme; TCKN/IBAN gibi alanlar için uygulama düzeyinde alan şifrelemesi.
- Sır yönetimi: sırlar depoda asla yok; sağlayıcı sır yöneticisi (AWS Secrets Manager vb.) veya SOPS + age; anahtar rotasyonu.
- Tedarik zinciri: Renovate/Dependabot, `npm audit`/SCA, CodeQL (SAST), OWASP ZAP (DAST) CI'da; canlıya çıkış öncesi bağımsız sızma testi.
- Denetim kaydı: giriş/çıkış, yetki değişikliği, finansal kayıt değişikliği, dışa aktarım ve toplu silme olayları; en az VUK/TTK saklama süresi kadar tutulur; yalnız ekleme.
- KVKK: kişisel veri envanteri, saklama/imha politikası, erişim kaydı (agent 03 ile bağlantılı).

---

## 7. Yedekleme ve uzun dönem okunabilirlik **[GEREKSİNİM: 5–10 yıl okunabilir, aranabilir, dışarı alınabilir]**

**Yedek stratejisi [ÖNERİ]** — 3-2-1 kuralı
- **Sürekli:** WAL arşivleme (pgBackRest/WAL-G veya yönetilen PITR) → **farklı konumda** nesne depolama; PITR penceresi ≥ 14 gün.
- **Günlük:** `pg_dump` mantıksal yedek (30 gün), **haftalık** (12 hafta), **aylık** (yasal süre boyunca) — şifreli, değiştirilemez (object lock/versioning).
- **Dosyalar:** fiş/fatura görüntüleri nesne depolamada sürümlemeli; ikinci konuma kopya.
- **Geri yükleme testi:** aylık otomatik (yedekten ayrı ortama kur → kayıt sayıları/sağlama toplamı karşılaştır → rapor); yılda bir tam felaket tatbikatı.

| Seviye | RPO | RTO |
|---|---|---|
| MVP (önerilen) | ≤ 15 dk | ≤ 4 saat |
| Yüksek erişilebilirlik | ≤ 1 dk | ≤ 1 saat |

**Uzun dönem okunabilirlik [ÖNERİ]**
- Yıllık (ve mali dönem kapanışında) **açık biçim arşivi:** tablo başına CSV (UTF-8) + Parquet, şema açıklaması (veri sözlüğü, Markdown/JSON), SQL düz metin dump.
- Resmî çıktılar (hakediş, fatura görselleştirme, raporlar) **PDF/A** olarak; e-belgelerin asıl XML'i (UBL-TR) entegratör arşivine ek olarak saklanır.
- Kiracı bazlı "tüm verimi indir" işlevi (ürünleştirmede satış argümanı ve KVKK/sözleşme çıkışı için gerekli).
- Yasal saklama: VUK m.253 (5 yıl, ilgili yılı izleyen takvim yılından) ve TTK m.82 (10 yıl, ilgili takvim yılı sonundan) **birlikte** uygulanır; e-Defter/berat ikincil kopyası da en az 10 yıl (ikincil kaynak; R1 incelemesi). Başlangıç kuralları ve istisnalar (yıllara yaygın iş, amortismana tabi kıymet) için **agent 05** belgesine bakınız. Arşiv politikası 10 yıl + istisnalar esasıyla kurulmalı **[ÖNERİ]**.

---

## 8. Performans hedefleri ve yük testi **[GEREKSİNİM: ölçülebilir hedef ve yük testi]**

**Önerilen hedefler [ÖNERİ]** (küçük ekip başlangıç ölçeğinin birkaç katı başlık payı ile):

| Ölçüt | Hedef |
|---|---|
| Normal ekran/API isteği | p95 < 500 ms, p99 < 1,5 s |
| Liste/filtre (10.000 satır, sayfalı) | p95 < 1 s |
| Standart rapor (proje maliyet özeti, cari) | < 3 s |
| Ağır rapor (çok yıllı, tüm projeler) | arka planda, < 60 s, bitince bildirim |
| PDF hakediş çıktısı | < 5 s |
| Excel içe aktarma (10.000 satır) | < 2 dk, doğrulama raporuyla |
| Eşzamanlı aktif kullanıcı | 25 kullanıcıda hedefler korunur; hata oranı < %0,1 |
| Erişilebilirlik | MVP %99,5 / HA %99,9 aylık |

**Araçlar:** k6 (betik tabanlı, CI dostu), Locust (Python), Artillery, JMeter; tarayıcı düzeyinde Playwright ile gerçek kullanıcı akışı süreleri. Üretimde gerçek kullanıcı ölçümü: OpenTelemetry + metrik paneli; yavaş sorgu günlüğü (`pg_stat_statements`).

**Senaryolar:** sabah giriş patlaması; aynı projede eşzamanlı hakediş/metraj girişi (kilit çakışması); ay sonu rapor + Excel dışa aktarım eşzamanlı; büyük Excel içe aktarımı sürerken normal kullanım; 2 saatlik dayanıklılık (soak) testi; 3 yıllık sentetik veriyle (gerçek Excel hacmine göre ölçeklenmiş) test.

---

## 9. Kurumsal web sitesi **[ÖNERİ: ERP'den ayrı, içerik yönetilebilir bir kurumsal site — segmentte sık görülen ek ihtiyaç]**

| Seçenek | Artı | Eksi | Tahmini maliyet |
|---|---|---|---|
| **Ayrı statik site + hafif CMS** (ör. Astro + Decap/Git tabanlı veya başsız CMS) | Hızlı, güvenli, neredeyse sıfır bakım; ERP saldırı yüzeyine eklenmez | İçerik paneli ERP'den ayrı | €0–15/ay (statik barındırma ücretsiz katman + alan adı) |
| Hazır CMS (yönetilen WordPress) | Tanıdık panel, eklenti bol | Eklenti güvenlik yamaları | ~$5–25/ay |
| ERP içinde | Tek giriş | ERP'yi herkese açık trafiğe açar; kapsamı büyütür | Geliştirme zamanı |

**Öneri [ÖNERİ]:** Ayrı statik site + basit CMS; ERP `erp.alanadi.com.tr` alt alan adında, sitede yalnız "Personel girişi" bağlantısı. ERP'den haber/proje referansı çekmek ileride API ile eklenebilir.

---

## 10. Önerilen mimari taslağı **[ÖNERİ]**

**Bileşenler (MVP):**
1. **Web istemcisi:** React SPA (statik dosya, CDN'den).
2. **API sunucusu:** modüler monolit (modüller: kimlik/yetki, proje, poz/birim fiyat, maliyet, hakediş, satın alma/stok, cari/finans, belge, içe/dışa aktarım, raporlama).
3. **PostgreSQL:** tek veritabanı, RLS ile kiracı ayrımı, denetim tabloları.
4. **İş kuyruğu + worker:** PDF/Excel üretimi, ağır raporlar, e-belge gönderimi, OCR; başlangıçta PostgreSQL tabanlı kuyruk (ör. pg-boss) — ek servis gerektirmez.
5. **Nesne depolama (S3 uyumlu):** fiş/fatura görüntüleri, üretilen PDF'ler, yedekler.
6. **Dış servisler:** GİB özel entegratör API'si, işlemsel e-posta, OCR/AI belge okuma, (ileride) banka.
7. **Gözlem:** yapılandırılmış loglar, metrikler, hata takibi, uptime izleme.
8. **CI/CD:** Git deposu → testler (birim, entegrasyon, kiracı izolasyonu, e2e) → konteyner imajı → staging → üretim.

```
                 Kullanıcı tarayıcısı
                        │ HTTPS
              ┌─────────▼──────────┐
              │ CDN / WAF (ör. CF) │──► Statik SPA dosyaları
              └─────────┬──────────┘
                        │ /api
              ┌─────────▼──────────┐       ┌──────────────────────┐
              │ API (modüler       │──────►│ Dış: e-Fatura        │
              │ monolit, konteyner)│       │ entegratör, e-posta, │
              └──┬──────────┬──────┘       │ OCR/AI               │
                 │          │ iş kuyruğu   └──────────▲───────────┘
                 │   ┌──────▼──────┐                  │
                 │   │ Worker      │──────────────────┘
                 │   │ PDF/Excel/  │
                 │   │ rapor/OCR   │
                 │   └──┬──────┬───┘
         ┌───────▼──────▼┐  ┌──▼──────────────┐
         │ PostgreSQL    │  │ Nesne depolama  │
         │ (RLS, audit)  │  │ (belgeler)      │
         └───────┬───────┘  └────────┬────────┘
                 │ WAL + dump        │ kopya
         ┌───────▼───────────────────▼────────┐
         │ Farklı konumda şifreli yedek deposu │
         └────────────────────────────────────┘
```

**Büyüme yolu:**
- **Aşama 1 (MVP, tek müşteri):** tek sunucuda API + worker konteyneri, ayrı ya da yönetilen PG; Docker Compose.
- **Aşama 2 (birkaç kiracı, ~50 kullanıcı):** API'yi 2+ örneğe çoğalt + yük dengeleyici; PG okuma replikası rapor için; kuyruk Redis/ayrı worker havuzu gerekirse.
- **Aşama 3 (ürün):** kiracı kayıt/faturalama, kiracı bazlı yedek-geri yükleme, isteğe bağlı büyük kiracı için ayrı veritabanı, bölge seçeneği (TR/AB), SOC2/ISO 27001 benzeri süreçler. Mikroservis ancak gerçek ihtiyaçta.

---

## Açık sorular

Segment düzeyinde açık sorular:
1. Mali verilerin **fiziksel olarak Türkiye'de** tutulması bu segmentte şart mıdır, yoksa AB'deki güvenilir bir veri merkezi sözleşmeyle kabul edilebilir mi?
2. e-Fatura/e-Arşiv için hangi **özel entegratörler** tercih edilir? Arşiv hizmeti entegratörden mi alınır?
3. Sistem kesintisinde kabul edilebilir en uzun süre nedir (ör. 1 saat / 4 saat / 1 gün)? En fazla kaç dakikalık veri kaybı kabul edilebilir?
4. Kullanıcılar şantiyeden mobil/tablet ile mi bağlanır? İnternet bağlantısı zayıf yerler var mı (çevrimdışı çalışma ihtiyacı)?
5. Yönetici rolleri için **iki adımlı doğrulama** (telefon uygulaması kodu) zorunlu olabilir mi?
6. Aylık altyapı bütçesi için kabaca hangi aralık uygundur: €50–100 / €100–200 / €300+?
7. Kurumsal web sitesi içeriğini kim, ne sıklıkla günceller?
8. Denetim/teftiş sırasında sistemden hangi biçimde çıktı istenir (PDF, Excel, e-Defter dosyası)?
9. Muhasebe/resmî defter ERP içinde mi tutulur, yoksa mali müşavirin programında mı kalır (K-05)? Bu yanıt hazır ERP temeli ile sıfırdan geliştirme kararını doğrudan etkiler.

## Açık noktalar / riskler

- **Muhasebe çekirdeği riski:** Sıfırdan yaklaşımda resmî muhasebe (hesap planı, KDV, e-Defter) en büyük iş yüküdür; K-05 "ERP içinde" çıkarsa takvim ve öneri yeniden değerlendirilmeli.
- **Veri konumu hukuki teyidi:** VUK 509 (573 değişiklikleriyle güncel metin) ve KVKK m.9 yorumunun — özellikle şifreli yedeğin yurt dışında tutulmasının — mali müşavir/hukukçu tarafından teyidi gerekir.
- **Türkiye'de yönetilen PG eksikliği:** AWS İstanbul Local Zone'da RDS yok; Huawei TR-Istanbul'da RDS PG varlığı ve yerli sağlayıcıların yönetilen DB/SLA olgunluğu **doğrulanmadı**. Türkiye şartı, tek geliştiriciye veritabanı işletme yükü getirir.
- **Fiyat oynaklığı:** Hetzner 2026'da iki kez zam yaptı ve ucuz serileri siparişe kapattı; DigitalOcean 30.11.2026'da HA planlarını değiştiriyor. Maliyet tablosu sipariş öncesi yenilenmeli; fiyatların bir kısmı üçüncü taraf kaynaktır.
- **Odoo/ERPNext değerlendirmesi:** Odoo'da e-Defter ve Türkiye mali raporları için Enterprise gereksinimi çıkarımdır (doğrulanmadı); Odoo Türkiye'ye özgü fiyatlar ve ERPNext Türkiye modüllerinin lisans/sürüm durumu doğrulanmadı.
- **Lisans yükümlülükleri:** GPL/LGPL/AGPL bağımlılıkları ürünleştirmede risk; bağımlılık lisans taraması CI'a eklenmeli. Ticari satış öncesi hukuki görüş alınmalı.
- **TypeScript para riski:** Ondalık disiplini ihlali sessiz hata üretir; tip/lint/test kuralları ilk günden zorunlu olmalı.
- **Tek kişi bağımlılığı (bus factor):** Belgeler, altyapının kod olarak tanımlanması (IaC), otomatik testler ve runbook'lar zorunlu; aksi hâlde bakım ve felaket kurtarma tek kişiye bağlı kalır.
- **AI agent verimliliği karşılaştırması** gözlem/değerlendirmedir, ölçülmüş veri değildir.
