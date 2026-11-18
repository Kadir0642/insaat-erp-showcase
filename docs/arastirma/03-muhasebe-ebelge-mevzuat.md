# 03 — Muhasebe, e-Belge ve Mevzuat (aday kapsam ve sınırlar)

> Belge numaraları (00–13), karar numaraları (K-xx, D-xx) ve "pilot keşif" kavramı için: [ARASTIRMA-OZETI.md](../ARASTIRMA-OZETI.md#bu-belgeler-nasıl-okunur).

> Araştırma agent'ı C · 18 Kasım 2026 · Kaynak kısaltmaları [K#] dosya sonundaki listededir (hepsine 18.11.2026'da erişildi).
> Bu dosya hukuki/mali müşavirlik görüşü değildir; oran ve eşikler firmanın SMMM'si ile teyit edilmelidir.

## Özet

- **e-Fatura büyük olasılıkla firma için zaten zorunlu.** "Gayrimenkul ... inşa ... işlemlerini yapanlar" için eşik 2022 ve sonraki yıllarda **500 bin TL** brüt hasılat; genel eşik 3 milyon TL [K1]. Bilanço esasına göre defter tutanlar için **1/1/2025'ten beri e-Defter zorunlu** [K3]. e-Fatura dışında kalan faturalar da 1/1/2026'dan beri tutardan bağımsız **e-Arşiv** olmak zorunda; 589 sayılı Tebliğ'deki bir yıllık erteleme yalnızca basit usul ve işletme esası mükellefleri kapsıyor [K2][K4].
- **ERP'nin özel entegratör olmadan doğrudan GİB'e belge göndermesi mevzuata göre mümkün ama pratik değil.** "Doğrudan entegrasyon" GİB'in kapasite ölçütlerini karşılayan ve başvurusu onaylanan mükelleflere açık (573 sayılı Tebliğ) [K4][K6]. GİB 2025–2026'da UBL-TR paketlerini yılda 10'dan fazla kez güncelledi [K7]. **[ÖNERİ]** ERP, lisanslı bir özel entegratörün API'sini kullansın.
- **Hakediş kesintileri:** KDV tevkifatı **4/10** [K9]; yıllara yaygın işlerde gelir/kurumlar vergisi stopajı **%5** (raylı sistem/gemi ve 1.6.2026'dan itibaren nükleer santral işlerinde %1) [K10]; sözleşme damga vergisi **binde 9,48**, ihale kararı **binde 5,69** [K11]. SGK ve vergi borcu sorgusu, teminat ve avans mahsupları da var [K12][K13].
- **Muhasebeleşme:** Yıllara yaygın işler **GVK 42–44**'e tabidir (dayanak VUK değil GVK 42–44'tür). Maliyetler 170–178, hakedişler 350–358 hesaplarında birikir; kâr ya da zarar işin bittiği yıl kesinleşir [K14].
- **Türkiye'deki yaygın model:** Firma ön muhasebeyi ve e-Fatura/e-Arşiv'i kendi yürütür, resmî defteri ve e-Defter'i SMMM kendi programında tutar (ikincil gözlem, doğrulanmadı).
- **Saklama:** VUK 253'e göre 5 yıl, TTK 82'ye göre 10 yıl [K15]. e-Defter'in asıl kopyası yurt içinde, ikincil kopyası en az 10 yıl GİB'de veya entegratörde tutulur [K16]. KVKK'da yurt dışı aktarım 1.6.2024'ten beri standart sözleşme ve 5 iş günü içinde bildirim gerektiriyor [K17].
- **[ÖNERİ] Kapsam:** MVP'de **Seçenek B**: ön muhasebe ve hakediş muhasebeleşmesi, entegratör üzerinden e-Fatura/e-Arşiv, SMMM'ye yapılandırılmış fiş aktarımı. Tam resmî muhasebe ve e-Defter (**Seçenek C**) ayrı ve sonraki bir faz olarak değerlendirilsin; karar müşterinin.

---

## 1. e-Belge türleri ve bu firma için olası zorunluluklar

| Belge | Zorunluluk kuralı (güncel) | Bu firma için | Kaynak |
|---|---|---|---|
| **e-Fatura** | Brüt hasılat 2022+ için ≥3 M TL (genel); **gayrimenkul/motorlu taşıt "inşa, imal, alım, satım, kiralama" yapanlar için ≥500 bin TL**. Yükümlülük şartın sağlandığı yılı izleyen 7. ayın başında başlar. | **Büyük olasılıkla zorunlu** [BELİRSİZ: ciro ve kayıt durumu sorulacak]. "İnşa" ibaresinin kamu yüklenicisini kapsaması bir yorumdur; kapsamasa bile 3 M TL genel eşik çoğu kamu yüklenicisini yakalar. Hangi eşiğin geçerli olduğu SMMM'ye sorulmalı | [K1] (RG 22.01.2022/31727, 535 s. Tebliğ metni; bağımsız inceleme R1 ikincil aktarımdan teyit etti, ISMMMO PDF'i açılmadı) |
| **e-Arşiv Fatura** | e-Fatura mükellefi, kayıtlı olmayan alıcıya e-Arşiv düzenler. e-Fatura dışındakiler 2025'te vergiler dahil 3.000 TL üstü faturaları, **1/1/2026'dan itibaren tüm faturaları** e-Arşiv olarak düzenler. 589 sayılı Tebliğ bu tarihleri yalnızca basit usul ve işletme esası mükellefler için bir yıl erteledi. | **Zorunlu** (kamu dışı/gerçek kişi alıcılar için) | [K2] (ikincil: KPMG), [K4] (ikincil: RG 31.12.2025/33124 5. Mük. özeti) |
| **e-İrsaliye** | e-Fatura'ya kayıtlı olup 2021 ve sonrası brüt hasılatı ≥10 M TL olanlar; demir-çelik imalatçı/ithalatçı/ihracatçıları. Ayrıca İnşaat Demiri İzleme Sistemi (İDİS) kapsamındakiler (≥1 M TL). | Ciro ≥10 M TL ise zorunlu. İDİS yükümlülüğü büyük olasılıkla satıcı tarafında [BELİRSİZ] | [K1], [K2], [K7] |
| **e-Defter** | **Bilanço esasına göre defter tutan herkes 1/1/2025'ten itibaren** e-Defter tutar. Defterler NES veya mali mühürle imzalanır; berat aylık ya da geçici vergi dönemi bazında yüklenir (kurumlar için ilgili ayı izleyen 4. ayın 14'üne kadar). | **Zorunlu** (A.Ş./Ltd. bilanço esasındadır) | [K3] (ikincil: RG 08.11.2024/32716 özeti) |
| e-SMM | Serbest meslek erbabı | Gerekli değil (firma alıcı tarafta) | — |
| e-Müstahsil, e-Gider Pusulası | Tarım ürünü alımı; vergi mükellefi olmayan kişiden alım | e-Gider Pusulası ara sıra gerekebilir (ör. kayıt dışı kişiden işçilik veya hurda alımı) [BELİRSİZ] | [K7] |
| e-Bilet, e-Döviz, e-Dekont | Sektöre özgü | Gerekli değil; e-Dekont bankalardan **alınır** | [K2] |

**Kamuya fatura:** Kamu idareleri de e-Fatura alıcısı olabiliyor, ancak idare bazında kayıt durumu doğrulanmadı [BELİRSİZ]. ERP, alıcının e-Fatura kayıtlı kullanıcı listesinde (GİB "UserList") olup olmadığını sorgulayıp belge tipini (e-Fatura veya e-Arşiv) **otomatik seçmelidir** [ÖNERİ] [K7].

**Hakediş faturası:** KDV Kanunu'na göre kısmi teslim olduğundan her onaylı hakediş için fatura düzenlenir. Genel KDV oranı %20'dir (ikincil, doğrulanmadı). Tevkifatlı fatura tipi ve tevkifat kodu UBL-TR'de ayrıca işaretlenir; bir hesap makinesi kaynağı kodu "622" olarak veriyor (doğrulanmadı) [K9].

## 2. Entegrasyon yolları

| Yol | Nasıl çalışır | ERP açısından |
|---|---|---|
| **GİB e-Belge Portalı** (ücretsiz) | Faturalar tarayıcıdan elle düzenlenir; mükellef başvurusu GİB'e yapılır | **API yok.** ERP ancak dışa aktarma ve elle giriş yapabilir. Düşük hacimde mümkün, otomasyon yok |
| **Özel entegratör** | Lisanslı firma UBL-TR XML'i alır, mali mühürle imzalar, GİB'e iletir, saklar. GİB listesinde 95 entegratör var (ör. Logo, Uyumsoft, İzibiz, TÜRKKEP, Veriban) [K5] | **[ÖNERİ] Ana yol.** ERP, entegratörün REST/SOAP API'sine UBL-TR gönderir; durum (kabul/ret), gelen faturalar ve e-Arşiv raporları geri çekilir |
| **Doğrudan entegrasyon** (mükellefin kendi sistemi) | Mükellef 7/24 bağlantılı sistemini GİB'e bağlar; mali mühür, BİS raporu ve test formu gerekir. 573 sayılı Tebliğ'e göre ciro, belge sayısı ve bilgi işlem altyapısı ölçütleri aranır. Şartı kaybedenin hesabı kapatılır ve bir yıl yeniden başvuru yapılamaz | küçük bir firma için **ölçütleri karşılaması olası değil** [BELİRSİZ]. Bakım yükü yüksek: GİB 2026'da 15'ten fazla paket/kılavuz güncellemesi yayımladı [K6][K7] |
| **ERP geliştiricisinin özel entegratör olması** | GİB izni, bilgi sistemleri denetim raporu, TÜRKAK onaylı ISO belgesi (Özel Entegrasyon Kılavuzu v1.14, 29.06.2026) | Tek müşterili bir proje için **orantısız** [K7][K8] |

**Sonuç:** ERP mevzuat gereği belgeyi kendi başına "geçerli e-Fatura" olarak GİB'e iletemez; ya mükellef doğrudan entegrasyon iznine sahip olmalı ya da arada lisanslı bir entegratör bulunmalı. ERP'nin işi UBL-TR üretmek ve doğrulamak, entegratör API'sini çağırmak ve durumu izlemektir.

**Tipik entegratör API'si (ikincil, sağlayıcıya göre değişir):** UBL-TR XML ya da JSON ile gönderim; UUID ve ETTN takibi; zarf durum sorgusu; gelen kutusu çekimi; uygulama yanıtı (kabul/ret); PDF/XSLT görüntü; e-Arşiv iptal; mükellef sorgusu. Test ortamı genellikle ücretsiz sunulur.

**Fiyat modeli (ikincil, doğrulanmadı):** Kontör ya da paket. Satıcı sayfalarında yıllık paketler yaklaşık 1.000–6.500 TL, kurumsal kontör fiyatı belge başına yaklaşık 5–15 TL olarak geçiyor. e-Defter kontörü dosya boyutuna göre düşüyor (ör. her 100 KB için 1 kontör). Saklamanın pakete dahil olup olmadığı mutlaka sözleşmede yazılı olmalı [K18].

**Mali mühür / NES:** e-Fatura'yı entegratör kendi mali mührüyle ya da mükellef adına imzalar. **e-Defter mükellefin mali mührü veya NES'i ile imzalanır** [K3]. Mali mühür TÜBİTAK Kamu SM'den alınır [K6]. Mührü kimin tutacağı (SMMM, entegratör veya firma) kararlaştırılmalı [BELİRSİZ].

## 3. Resmî muhasebe ve iş bölümü

- **Çerçeve:** Tekdüzen Hesap Planı (MSUGT, 1 Sıra No), yevmiye, büyük defter ve envanter defteri; envanter defteri de 2025'ten itibaren e-Defter olarak tutulabiliyor [K3]. Mali tablolar bilanço ve gelir tablosudur. Bağımsız denetime tabi olunursa TFRS ya da BOBİ FRS de devreye girer [BELİRSİZ: firma büyüklüğü].
- **Yıllara yaygın inşaat (GVK 42–44)** [K14]:
  - Birden fazla yıla yayılan işlerde kâr ya da zarar işin bittiği yıl beyan edilir. Bu işlerin kazancı geçici vergiye tabi değildir (ikincil).
  - Maliyetler 740 hesabında toplanır, dönem sonunda 170–178 hesaplarına aktarılır. Onaylı hakediş bedelleri 350–358 hesaplarına alacak kaydedilir.
  - İş bitince 350 hesabı 600'e, 170 hesabı 621'e kapatılır.
  - Kesilen %5 stopaj 193 Peşin Ödenen Vergiler hesabında izlenir ve iş bitince mahsup edilir.
  - **KDV ertelenmez:** Her hakedişte beyan edilir.
- **ERP'nin kendi tutması gereken veriler** [ÖNERİ]: Proje ve sözleşme bazında 170/350 alt hesapları, iş bazında stopaj ve teminat alt hesapları, yer teslimi ve geçici kabul tarihleri. Yer teslimiyle geçici kabul aynı yıldaysa iş yıllara yaygın sayılmaz ve stopaj uygulanmaz [K12]. Bu tarihler muhasebe yöntemini belirlediği için proje modülünde zorunlu alan olmalıdır.
- **Yaygın iş bölümü (ikincil, doğrulanmadı):** KOBİ'lerde resmî defter ve beyannameler (KDV, Muhtasar, Kurumlar, geçici vergi), e-Defter beratları ve mali tablolar SMMM'nin muhasebe programında tutulur. Firma ön muhasebe, faturalama ve cari/kasa/banka işlerini yürütür. Belgeler ya da fiş aktarım dosyaları aylık olarak SMMM'ye iletilir.
- **SMMM'ye aktarım seçenekleri** [ÖNERİ]:
  - (1) Yevmiye fişi formatında Excel/CSV (çoğu muhasebe programında "Excel'den fiş aktarımı" bulunur, ikincil).
  - (2) Hesap planı eşleme tablosu (ERP'deki hesap ve masraf merkezi → SMMM hesap kodu).
  - (3) e-Fatura XML'leri: SMMM zaten entegratörden ya da GİB'den çekebilir.
  - (4) İleride, SMMM'nin programı destekliyorsa API.
  - Hangi programı kullandığı **SMMM'ye sorulmalı** [BELİRSİZ].
- **[GEREKSİNİM]** Pilot keşifte "resmî muhasebe işlemleri" isteniyor ama kapsam açık bırakılmış. "Resmî muhasebe"nin defter tutmak mı, yoksa SMMM'ye düzenli veri vermek mi anlamına geldiği netleşmeli.

## 4. Hakedişin vergi ve kesinti tarafı

| Kalem | Oran / kural | Dayanak & durum |
|---|---|---|
| **KDV tevkifatı** | Belirlenmiş alıcılara (kamu idareleri dahil) yapılan yapım işlerinde ve bunlara bağlı mühendislik/mimarlık/etüt-proje hizmetlerinde **4/10**. Diğer KDV mükelleflerinde KDV dahil ≥5 M TL'lik işlerde de uygulanır. Taşeron zincirinde her yüklenici kendi aldığı hizmet için tevkifat yapar | KDV Genel Uygulama Tebliği I/C-2.1.3.2.1 (ikincil: [K9], [K12]) |
| **Gelir/Kurumlar vergisi stopajı** | Yıllara yaygın inşaat ve onarım hakedişlerinde **%5** (GVK 94/3, KVK 15). 9707 s. CK (karar 29.03.2025, RG 30.03.2025/32857) ile raylı sistem ve gemi inşaatında %1. 11344 s. CK (RG 19.05.2026) ile 1.6.2026'dan itibaren nükleer santral işlerinde %1 | (ikincil: [K10]; CK metinleri bu oturumda açılmadı) |
| **Damga vergisi** | Sözleşme **binde 9,48**, ihale kararı **binde 5,69**. 2026'da bir kâğıt için azami tutar 29.115.961,10 TL. Bir kaynak her hakedişte KDV hariç tutar üzerinden ve iş artışında binde 9,48 kesildiğini yazıyor | 488 s. DVK 1 sayılı tablo (ikincil: [K11], [K12]). **Hakedişte damga uygulaması [BELİRSİZ]**, SMMM ile teyit |
| **SGK** | Hakediş ödemesinden ve kesin teminat iadesinden önce idare SGK borç sorgusu yapar. Borç varsa hakedişten mahsup edilir, bakiye sonraki hakedişlerden düşülür. Kesin teminatın iadesi için ilişiksizlik belgesi aranır | 5510 s. K. md. 90; SGK Genelgesi 2008/88 ve 2020/5 (ikincil: [K13]) |
| **Vergi borcu** | Ödeme öncesi vergi borcu sorgusu yapılır; eşik üstündeki borç hakedişten kesilir. Kaynakta eşik 5.000 TL olarak geçiyor | 6183 s. K. 22/A (doğrulanmadı; tutar güncel tebliğden teyit edilmeli) |
| **Teminat / mahsuplar** | İş artışında ek kesin teminat %6, fiyat farkı teminatı %6, avans mahsubu, gecikme cezası | Tip sözleşme (ikincil: [K12]). **Hesaplama yöntemi agent 02'nin alanında** |

**ERP'nin karşılaması gerekenler** [ÖNERİ]:

- Kesinti ve teminat kuralları **tarih aralıklı parametre tablosunda** tutulmalı; mevzuat sık değişiyor (2025 ve 2026'da yeni CK'lar çıktı).
- Her hakediş için tek bir "hakediş mahsup fişi" üretilmeli:
  - Alacak tarafında: hakediş bedeli (350), hesaplanan KDV (391).
  - Borç tarafında: tevkif edilen KDV, stopaj (193), teminat kesintileri (126/226 ya da alacak alt hesabı), damga vergisi gideri, SGK/vergi mahsupları ve net tahsil edilecek tutar (120).
- Üretilen fişin SMMM tarafından onaylanması gerekir.

## 5. Ön muhasebe / finans (aday kapsam)

- **Cari hesap:** Kamu idaresi, taşeron, tedarikçi, personel avansı. Proje bazında alt kırılım; mutabakat ve yaşlandırma raporları.
- **Kasa / banka:** Çoklu hesap ve döviz; proje ile masraf merkezi etiketi.
- **Çek / senet:** Portföy, ciro, tahsil/ödeme vadesi, karşılıksız çek takibi.
- **Teminat mektupları:** Alınan ve verilen mektuplar (geçici, kesin, avans); banka, vade, komisyon ve iade takibi. Muhasebede 900'lü nazım hesaplar kullanılır (ikincil). Kamu işinde kritik bir alan [ÖNERİ: MVP].
- **Ödeme / tahsilat:** Planlama ve onay akışı; hakediş tahsilatının beklenen ve gerçekleşen karşılaştırması.
- **Banka entegrasyonu** (3 seviye):
  - (1) **Ekstre içe aktarma** (Excel/CSV, MT940): bankadan bağımsız, düşük maliyetli [ÖNERİ: MVP].
  - (2) **Bankaların kurumsal web servisleri:** Firma kendi bankasıyla sözleşme yapar; bankaya göre değişir [BELİRSİZ].
  - (3) **Açık bankacılık (BKM GEÇİT):** 6493 s. Kanun'a göre hesap bilgisi hizmeti TCMB izni gerektirir. ERP geliştiricisi lisans almadan bu hizmeti veremez; lisanslı bir aracıyla çalışmak gerekir [K19].

## 6. Saklama ve uyum

- **Süreler:** VUK 253'e göre defter ve belgeler 5 yıl, TTK 82'ye göre 10 yıl saklanır [K15]. İki süre birlikte uygulanır; pratikte esas alınan 10 yıldır.
- **Başlangıç kuralı:** VUK süresi kaydın ait olduğu yılı **izleyen takvim yılının başından**, TTK süresi deftere son kaydın yapıldığı ya da belgenin oluştuğu **takvim yılının sonundan** başlar [K15] (ikincil).
- **İstisnalar:** Süre üç durumda fiilen uzar:
  - Yıllara yaygın işlerde, işin bittiği yıla kadar tutulan kayıtlar için.
  - Zarar mahsubunda, zararın mahsup edildiği yılın zamanaşımı bitene kadar.
  - Amortismana tabi kıymetlerde, alış ve maliyet belgeleri amortisman süresi boyunca ve son amortisman yılının zamanaşımı bitene kadar (ikincil, doğrulanmadı) [K15].
  - Bu nedenle silme ya da arşivleme kuralı belge türü ve bağlı kayda göre hesaplanmalıdır [ÖNERİ]. Sistem en az **10 yıl + iş süresi** boyunca saklama yapabilmelidir [ÖNERİ]. Bu, pilot keşifteki "5–10 yıl okunabilirlik" beklentisiyle de uyumlu [GEREKSİNİM].
- **e-Belge ve e-Defter:**
  - e-Defter ve berat dosyalarının asıl kopyası **mükellefin kendi bilgi işlem sisteminde, Türkiye sınırları içinde** tutulmalıdır. Üçüncü kişide ya da yurt dışında tutmak mükellefin sorumluluğunu kaldırmaz.
  - İkincil kopya 1/1/2020'den itibaren en az **10 yıl** GİB'de veya entegratörde saklanır [K16].
  - e-Fatura ve e-Arşiv'i entegratör de saklar; ERP ayrıca UBL XML'in kendi kopyasını tutmalıdır [ÖNERİ].
- **KVKK yurt dışı aktarım (7499 s. K., RG 12.03.2024, yürürlük 1.6.2024; Yönetmelik RG 10.07.2024/32598)** [K17]:
  - Yeterlilik kararı yoksa uygun güvenceler gerekir: Kurul'un standart sözleşmesi (2024/959 s. karar, 4 tip), bağlayıcı şirket kuralları ya da taahhütname.
  - Standart sözleşme **imzadan sonra 5 iş günü içinde** Kurum'a bildirilir. Bildirim yapmamanın idari para cezası 2026 için 90.308–1.806.377 TL (ikincil).
  - **[ÖNERİ]** Muhasebe ve personel verisi için **Türkiye'de barındırma** tercih edilsin. Yurt dışı bulut seçilirse standart sözleşme ve bildirim süreci kurulsun; e-Defter asıl kopyası yine yurt içinde kalmalı. Bu konu mimari agent'ı ile birlikte değerlendirilmeli.
- **Denetim izi:**
  - TTK 65'e göre kayıt, önceki içeriği belirlenemeyecek şekilde değiştirilemez (ikincil, doğrulanmadı).
  - **[ÖNERİ]** Onaylanmış fiş ve hakedişler silinmesin; düzeltme ters kayıtla yapılsın. Kim/ne zaman/eski değer/yeni değer kaydedilsin. Dönem kilidi olsun. Fiş numaraları sıralı ve boşluksuz olsun.

## 7. ERP için kapsam seçenekleri

| | **A — Ön muhasebe + dışa aktarım** | **B — A + entegratörle e-Fatura/e-Arşiv** (ÖNERİ) | **C — Tam resmî muhasebe + e-Defter** |
|---|---|---|---|
| ERP'nin yaptığı | Cari, kasa/banka, çek/senet, teminat, hakediş mahsup fişi, SMMM'ye fiş aktarımı | A'ya ek olarak: e-Fatura/e-Arşiv düzenleme, gelen e-Faturaları çekme, kabul/ret, ileride e-İrsaliye | B'ye ek olarak: yevmiye, kebir, envanter, mali tablolar, beyanname altlıkları, e-Defter XBRL-GL üretimi ve berat yükleme (entegratör üzerinden) |
| Faturalama | Ayrı bir entegratör portalında elle; çift giriş riski | ERP'den tek akış | ERP'den tek akış |
| Yasal sorumluluk | Defter ve beyan SMMM'de; ERP yardımcı kayıt sistemi | Belge düzenleme ERP'den yapılır; hatalı belge firmaya ceza riski doğurur (VUK usulsüzlük) | Defterin doğruluğu ERP'ye bağlanır. e-Defter yazılımı GİB uyum onayı ister ve kurallara aykırılıkta onay iptal edilebilir [K3] |
| Geliştirme yükü (göreli, tahmin) | Düşük–Orta | Orta (UBL-TR, entegratör API'si, durum yönetimi, sık paket güncellemesi) | **Yüksek** (THP, dönem sonu, yıllara yaygın kapanış, enflasyon düzeltmesi, XBRL-GL, uyum testi) |
| Sürekli bakım | Düşük | Orta: UBL-TR değişikliklerine uyum (2026'da en az 6 paket güncellemesi [K7]) | Yüksek: tebliğ, kılavuz ve beyan formatları |
| İşletim maliyeti (ikincil, doğrulanmadı) | SMMM ücreti (zaten var) | + entegratör paketi/kontörü (yıllık binlerle onbinler TL arası, hacme göre) | + e-Defter kontörü/saklama; SMMM ücreti azalmayabilir, çünkü beyan ve imza yine SMMM'de |
| Risk | Excel'e geri kayma, mutabakat farkları | Entegratöre bağımlılık (API değişimi); bu risk soyutlama katmanıyla azaltılabilir | Hatalı defter, berat süresinin kaçırılması (VUK cezası), SMMM'nin ERP'yi kabul etmemesi |

**[ÖNERİ]** MVP'de **B** seçeneği, artı entegratör soyutlama katmanı (birden fazla entegratör takılabilsin) ve SMMM'ye hesap planı eşlemeli fiş aktarımı. Gerekçeler:

- e-Fatura/e-Arşiv mevzuat gereği zaten fiilî zorunluluk; ERP'den kesilmezse hakediş ile fatura arasında çift giriş oluşur.
- e-Defter'in SMMM programında kalması, yasal riski uzman olan tarafta bırakır.

**C** seçeneği, firma kendi bünyesinde muhasebe personeli istihdam etmeyi planlıyorsa ayrı bir fazda ele alınabilir. Karar müşterinindir.

---

## Kaynaklar (erişim: 18.11.2026)

- [K1] 535 s. VUK Genel Tebliği, RG 22.01.2022/31727 (ISMMMO PDF içinde RG metni). https://www.ismmmo.org.tr/dosya/3148/Mevzuat-Dosya/22012022-ebelge-kullanma-zorunlulugu-tarihleri-yeniden-belirlendi.pdf (doğrulandı: RG metni)
- [K2] KPMG, 573 s. VUK Tebliği özeti (RG 12.11.2024/32720). https://kpmgvergi.com/yayinlar/mali-bultenler/vergi/elektronik-belge-uygulamalarina-iliskin-573-sira-no-lu-vuk-tebligi-yayimlanmistir/2852 (ikincil)
- [K3] e-Defter Genel Tebliği Sıra No 5, RG 08.11.2024/32716. https://www.alomaliye.com/2024/11/08/elektronik-defter-genel-tebligi-sira-no-5/ (ikincil: RG metni aktarımı)
- [K4] 589 s. VUK Tebliği, RG 31.12.2025/33124 (5. Mük.). https://www.alomaliye.com/2025/12/31/vergi-usul-kanunu-genel-tebligi-sira-no-589/ (ikincil). GİB tebliğ listesi: https://ebelge.gib.gov.tr/efaturamevzuat.html (doğrulandı: resmî kaynak, 509 değişiklikleri 515/526/535/550/573/589)
- [K5] GİB özel entegratör listesi (95 firma). https://ebelge.gib.gov.tr/efaturaozelentegratorlerlistesi.html (doğrulandı: resmî kaynak)
- [K6] GİB Entegrasyon yöntemi. https://ebelge.gib.gov.tr/efaturaentegratorluk.html ve https://ebelge.gib.gov.tr/efaturaozelentegratorluk.html (doğrulandı: resmî kaynak). 573 s. Tebliğ doğrudan entegrasyon özeti: https://www.alomaliye.com/2024/11/12/vergi-usul-kanunu-genel-tebligi-sira-no-573/ (ikincil)
- [K7] GİB e-Belge duyuruları 2025–2026 (UBL-TR paketleri, İDİS, UserList, Özel Entegrasyon Kılavuzu v1.14). https://ebelge.gib.gov.tr/duyurular.html (doğrulandı: resmî kaynak)
- [K8] Özel entegratör başvurusunda TÜRKAK onaylı ISO şartı. https://musavirlerkulubu.com.tr/makale/e-fatura-ozel-entegrasyon-kilavuzu-guncellendi-iso-belgesi-sarti-geldi (ikincil)
- [K9] Yapım işlerinde KDV tevkifatı 4/10. https://www.muhasebenews.com/yapim-islerinde-kdv-tevkifati-yapilir-mi/ ; https://www.yontemymm.com.tr/pratik-bilgiler/kdvde-kismi-tevkifat-tablosu (ikincil; resmî metin: GİB KDV Genel Uygulama Tebliği, bu oturumda açılmadı)
- [K10] Stopaj oranları: PwC Vergi Bülteni 2025/14 https://www.pwc.com.tr/tr/hizmetlerimiz/vergi/bultenler/2025/bazi-yillara-sari-insaat-ve-onarim-isleri-istihkaklarinda-stopaj-orani-degisti.html ; 11344 s. CK: https://hukukcularevi.com/nukleer-santral-insaat-yuzde-1-vergi-tevkifati-11344-karar/ (ikincil)
- [K11] 2026 damga vergisi oranları ve azami tutar. https://www.kazimceylan.av.tr/damga-vergisi-hesaplama (ikincil)
- [K12] Yapım işlerinde hakediş kesintileri (30.07.2026). https://www.hakedis.org/yapim-islerinde-hakedis-kesintileri-ve-yuklenicilerin-diger-mali-yukumlulukleri/ (ikincil)
- [K13] SGK Genelgesi 2008/88 https://www.alomaliye.com/2008/10/30/sgk-genelgesi-200888-prim-ve-idari-para-cezasi-borclarinin-hakedislerden-mahsubu-odenmesi-ve-ilisiksizlik-belgesinin-aranilmasi-hk ; 2020/5 borç sorgusu https://www.turmob.org.tr/arsiv/mbs/resmigazete/-2020-5_Genelge_BorcSorgusu.pdf (ikincil)
- [K14] Yıllara yaygın inşaat; GVK 42 ve 170/350 hesapları. https://www.muhasebetr.com/yazarlarimiz/ufuk/005 ; https://vergiraporu.com.tr/upImage/org/2012-159-Yillara_Yaygin_Insaat_Ve_Onarma_Islerinde_Donem_Sonu_Islemleri-Kadir_Sahin%20.pdf (ikincil; GVK metni: https://www.mevzuat.gov.tr — bu oturumda açılmadı)
- [K15] VUK 253 / TTK 82 saklama süreleri. https://www.turmob.org.tr/BasinOdasi/BasinArsiv/Detay/9682a497-ca2e-487e-abb6-fe3440cdfa69/vuk-a-gore-defter-ve-belgelerin-saklanma-sureleri-ve-ozellikli-durumlar (ikincil: meslek kuruluşu)
- [K16] TÜRMOB e-Defter muhafaza ve ibraz. https://www.turmob.org.tr/e-donusum/edefter/ibrazi (ikincil: meslek kuruluşu, tebliğ maddelerini aktarıyor)
- [K17] KVKK Standart Sözleşme Bildirim Modülü duyurusu. https://www.kvkk.gov.tr/Icerik/8043/Standart-Sozlesme-Bildirim-Modulu-Hakkinda-Kamuoyu-Duyurusu (resmî kaynak; Yönetmelik ve ceza tutarları ikincil: https://cottgroup.com/tr/blog/kvkk-gdpr/item/standart-sozlesme-bildirim-yukumlulugu-ve-yaptirimlari)
- [K18] Entegratör fiyat örnekleri. https://www.ideasoft.com.tr/eticaret-cozum-merkezi/earsiv-efatura-cozumleri/edm-bilisim/ ; https://www.parasut.com/kullanim-kilavuzu/elektronik-fatura-hizmetinin-maliyeti (ikincil, satıcı sayfası)
- [K19] TCMB açık bankacılık duyurusu (Mart 2026). https://www.alomaliye.com/2026/03/17/acik-bankacilik-hizmetlerinin-yeni-ozelliklerine-iliskin-basin-duyurusu/ (ikincil)

## Açık sorular

Segment düzeyinde açık sorular:
1. Hangi şirket türleri ve hangi defter esasları (bilanço, işletme hesabı) yaygındır; hasılat büyüklüğü e-Fatura ve e-Defter zorunluluklarını nasıl etkiler?
2. Firmaların e-Fatura mükellefiyet durumu nedir; faturalar hangi yolla (portal, entegratör, mali müşavir) kesilir ve entegratör sözleşmeleri nasıl işler?
3. Mali müşavir hangi muhasebe programlarını kullanır; e-Defter'i kim tutar, mali mühür kimdedir?
4. "Resmî muhasebe" beklentisi yasal defterin ERP içinde tutulması mı, yoksa mali müşavire hazır ve düzenli veri verilmesi mi anlamına gelir? Firma içi muhasebe personeli var mıdır?
5. İdareler hakediş faturası için e-Fatura mı e-Arşiv mi ister? Tevkifat, stopaj ve damga kesintileri hakediş icmalinde nasıl görünür (örnek icmal gerekir)?
6. Taşeronlardan fatura ve hakediş nasıl gelir; taşeronlara tevkifat uygulanır mı?
7. Banka ekstresi nasıl alınır; teminat mektubu sayısı ve takip yöntemi nedir?
8. Yıllık fatura hacmi nedir (entegratör maliyeti için)?
9. Verilerin Türkiye'de barındırılması zorunlu mu, tercih mi?
10. e-İrsaliye kullanımı ve şantiyelere malzeme sevkinin belgelenmesi nasıl yürür?

## Açık noktalar / riskler

- **Hakedişte damga vergisi uygulaması** (her hakedişte binde 9,48 mi, yalnız sözleşmede mi) ikincil kaynakta geçiyor; resmî metinle teyit edilemedi.
- **6183 s. K. 22/A vergi borcu sorgusu eşiği** ve **e-Fatura tevkifat kodu (622)** doğrulanmadı.
- 573 ve 589 sayılı Tebliğlerin e-Fatura **ciro eşiklerini** değiştirmediği ikincil özetlerden çıkarıldı. 509'un güncel dipnotlu metni GİB'de mevcut ama bu oturumda okunmadı.
- **Doğrudan entegrasyonun güncel ölçütleri** (ciro, belge sayısı, ISO) GİB sayfalarında yer almıyor; başvuruya açık olup olmadığı belirsiz.
- **İDİS** (İnşaat Demiri İzleme Sistemi) yükümlülüğünün alıcı konumundaki yükleniciye bir etkisi olup olmadığı belirsiz.
- **GİB'in sık format değişiklikleri** (2026'da 15'ten fazla duyuru) B ve C seçeneklerinde sürekli bakım maliyeti yaratıyor; entegratör seçimi ve soyutlama katmanı bu riski azaltır.
- **KDV oranı ve faaliyet kodu kontrolü:** GİB 1.4.2026'da başlatmayı planladı, sonra erteledi [K7]. Devreye girdiğinde hakediş faturalarında oran ve kod hataları reddedilebilir.
- **Kapsam C:** e-Defter yazılım uyum onayı ve yasal sorumluluk yükü, küçük bir ekip için önemli bir risk.
- Maliyet rakamları satıcı sayfalarından alındı (ikincil). Gerçek teklif alınmalı.
- **Araştırılmadı:** Vergisel enflasyon düzeltmesinin yıllara yaygın işlere etkisi (2025–2027) ve dönemsel bildirimler (Ba/Bs formları, e-Beyanname). Bunlar Seçenek C'de ERP'nin, A ve B'de SMMM'nin yükü olur.
