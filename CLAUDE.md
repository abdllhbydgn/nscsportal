# EMS sitesi — kalıcı çalışma kuralları

> **Her sohbette önce `HAFIZA.md`'yi oku (kısa, ≤70 satır); sohbet sonunda oraya kısa not ekle. Eski kayıtlar `HAFIZA_ARSIV.md`'de: baştan OKUMA, yalnız `grep` ile ara. HAFIZA.md 70 satırı aşınca eski notları arşive taşı.**

Site tek dosyadır: `index.html` (GitHub Pages + Firebase/Firestore). Bu kurallar her oturumda geçerlidir.

## Soru ekleme / birleştirme / senkronizasyon (HER ZAMAN)
- Yeni bir soru, bulgu, CAP maddesi veya kontrol listesi eklerken **önce diğer tüm bölümlerde aynı soru var mı kontrol et** (CSR, İSG, Çevre, Sivil Savunma, Organik, Higg, OEKO-TEX, Inditex, M&S, Müşteri Denetim Soruları ve müşteri bulguları).
- Aynı soru varsa **birleştir**: yeni kayıt açma, mevcut soruyu bağla (`CUSTOMER_DOC_QUESTIONS` "same" alanı, `_qMergeDefs` grupları).
- Birleşik sorular **entegre ve senkronize** çalışır: durum değişikliği tüm grup üyelerine ve bağlı bulgulara yansır (`_syncMergedGroup`), genel toplamda bir kez sayılır (`_uniqueQuestions`).
- Bulgular soruya bağlanır (`_linkFindingsToQuestions`); bulgu ↔ soru durumu iki yönlü senkron.
- **MÜŞTERİLER VE DENETİMLER BAĞIMSIZDIR (kullanıcı kuralı):** Müşteri soruları (kategori `custq`, `inditex`, `ms`; `_isCustQ`) genel toplamdan, `_uniqueQuestions`/`calcMetrics`/birleştirmeden ve bölüm sayfalarından ÇIKARILMIŞTIR; aynı soru olsa bile birleştirme YOK. Her müşterinin kendi soru nesnesi vardır (`_brandSet`, `fqCust` tek müşteri); `CUSTOMER_DOC_QUESTIONS` satırları hep müşterinin kendi sorusudur (`r[6]` yalnız eski ortak sorudan durum/fotoğraf devri için, `_custSplitMigrate`). Yeni müşteri sorusu/bulgusu eklerken diğer bölümlerle eşleme yapma; yalnız aynı müşterinin soru/bulgusuyla ilişkilendir.

## Belge birleştirme kuralı (kullanıcı kuralı, HER ZAMAN)
- Yeni prosedür / talimat / form / SOP yazmadan önce **mevcut resmî belgelerle karşılaştır** (`prosedurler/` + `manifest.json`, `formlar/` + `manifest.json`, QMS `QMS_PRS_OFFICIAL`).
- **FORMLAR BİRLEŞTİRİLMEZ (kullanıcı kuralı):** Excel formları (`formlar/`, `FRM-*`) farklı amaçlıdır; konu benzese de birleştirme, mevcut Excel'i değiştirme, ikisini tek forma indirme. Yalnız **prosedür, talimat ve SOP** için birleştirme kuralı geçerlidir. Taslak form (`FRM-*`) ile mevcut Excel form yan yana kalır; gerekirse aralarına sadece "ilgili form" bağlantısı konur.
- Aynı konuda belge varsa **yeni ikinci kopya açma**: mevcut belgeyi daha kapsamlı ve kurumsal bir dille yazıp **tek belgede birleştir** (aynı kod/ad, revizyon R01…, `manifest.json` `rev` değişir).
- Prosedürler EN+AR tek .docx; imza bloğu mevcut şablondan (bkz. HAFIZA); üretim araçları: scratchpad `prolib.py`/`assemble.py` yöntemi (şablon docx + gövde yeniden yazımı). Belgelerin geçtiği yerler `prosedurler/refs.json` (Doküman Dizini bunu kullanır; belge eklenince yeniden üret).

## Veri ve fotoğraflar
- **FOTOĞRAFLARI SİLME.** Mevcut verileri ve sitenin işleyişini bozma.
- Kanıt fotoğrafı/belgesi yalnız "Tamamlandı" ve "Devam Ediyor" (bulgularda "Kapandı"/"Devam Ediyor") için zorunlu; "Başlanmadı"/"Açık" için istenmez. (Soru durumu adları: Tamamlandı / Devam Ediyor / Başlanmadı.)
- Sorulara sorumlu + elle termin: `q.owner`, `q.ownerDue` (admin ve Kişi Rehberi'nde "atama yetkisi" (`assign` bayrağı, `_qCanAssign`) verilmiş kişiler atar ve e-posta gönderir; bu kişiler yalnız sorumlu alanlarını onaysız yazar (`_ownerOnlyChange`); adresleri koda gömme, yönetici Kişi Rehberi → toplu ekle'den yapıştırır; birleşik grupta ortak, boş bulgu sorumlusuna geçer) — `openQOwnerDialog`. E-posta `q.ownerEmail`; Kişi Rehberi `openContactDirectory` (= `dailyAuditEmailPool`, tek ortak liste; e-posta adreslerini koda gömme); e-posta Outlook ile `qOwnerMail` / `qOwnerMailAll`.
- Sorular buluttaki tek `questions` belgesinde saklanır (1 MB sınırı) — soru metinlerini kısa tut, boyutu kontrol et.
- Performans Sistemi olduğu gibi kalır.
- Yetki modeli B: silme/değişiklik admin onayına, yeni kayıt doğrudan; personel silemez.

## EĞİTİM / TANITIM VİDEOSU BİTİŞ EKRANI (kullanıcı kuralı, 26.10.2026, HER ZAMAN)
- **Her eğitim ve tanıtım videosu** sahnenin ortasında bitmez; mutlaka son sahne "Thank you" bitiş ekranıdır: solda EMS logosu + "Thank you / Teşekkürler · شكراً" + "Quality starts with you" etiketi, sağda Abdullah Baydoğan iletişim kartı (ofis, fabrika, telefon, e-posta, web). Şablon: `tanitim/bitis_ekrani_sablon.js` (`CLOSE`), örnek metin: `tanitim/oryantasyon.json` son sahne (`kapanis`). Bitişte ≥ 3–4 sn sabit tutulur, kapanış cümleleri seslendirilir (EN ses, TR+AR altyazı). Bu ekran olmadan video teslim edilmez/yayınlanmaz.
- **VİDEO ÜRETİM İŞ AKIŞI (kullanıcı kuralı, 26.10.2026, HER ZAMAN):** videoyu **bir kez çek, hazır tut**. Sahne klipleri ve araçlar `tanitim/kaynak/` altında saklanır (README'ye bak); küçük metin/ses düzeltmesinde videoyu baştan çekme, **yalnız ilgili sahneyi yeniden çek**, klipleri yeniden birleştir. Yeni video çekince sahne klipleri + meta + araçlar da repoya konur (ephemeral konteynere güvenme).
- Eğitim videoları: İngilizce seslendirme, altyazı TÜRKÇE + ARAPÇA (tek video); Türkçe seslendirme yapma.

## Dil ve sunum
- **YENİLEMEDE AYNI SAYFA (kullanıcı kuralı):** her yeni sayfa/pencere açılışında `saveLastView("ad", params)` çağır ve `_applySavedView` içine `case` ekle; yenileyince kullanıcı ana sayfaya düşmemeli.
- Site 3 dilli kalmalı (TR/EN/AR). Soru metni "TR / EN" biçiminde; metin içinde " / " kullanma.
- Raporlar dönem başlığıyla başlar. Özet kartları `_pdfKpiBandHtml` (lacivert bant). Rapor başlığı her zaman `_pdfHeadHtml` (logo solda, ad ortada, sağda konu ikonu); imza tam genişlik bant (`_pdfSignatureCanvas`). Yeni rapor eklerken bunları kullan.
- **İMZA YERİ KURALI (tüm indirilen raporlar):** imza bandı raporun bittiği yerin hemen altına gelir; tam sığmayacaksa (yarım kalacaksa) bir sonraki sayfanın en üstüne, üstünde ince "EMS — Rapor devamı" satırıyla konur (`_pdfAddSignature`). Sayfa ortasına/altına itme.

## MOBİL KONTROL (kullanıcı kuralı, 24.10.2026, HER ZAMAN)
- Yaptığımız her yenilik ve düzeltme **mobilde de** kontrol edilir: Playwright ile 390 ve 360 px genişlikte (isMobile) aç, yatay taşma var mı bak (`scrollWidth` ≤ `innerWidth`), ekran görüntüsüyle göz at; sorun varsa düzelt, sonra teslim et. Kullanıcıya cevapta "mobilde de baktım" diye yaz.

## İş akışı
- Geliştirme dalı: `claude/selam-pwr5q1`. Her değişiklikte commit → push → main'e PR → PR'ı birleştir.
- **SÜRÜM (her değişiklikte ZORUNLU):** commit'ten hemen önce `index.html` sonundaki `EMS_BUILD` ve `version.json` aynı değere (İstanbul saati `YYYY-AA-GG SS:DD`) güncellenir. Komut:
  `B=$(TZ=Europe/Istanbul date +"%Y-%m-%d %H:%M"); sed -i "s/^const EMS_BUILD = \".*\";/const EMS_BUILD = \"$B\";/" index.html; printf '{"build": "%s"}\n' "$B" > version.json`
  **Saat gösterimi (01.11.2026):** EMS_BUILD İstanbul saatiyle (UTC+3, yaz/kış saati yok) yazılır; site bunu izleyenin YEREL saatine çevirip gösterir (Mısır kış saatinde UTC+2 → ekranda 1 saat geri). Kullanıcıya cevapta sürüm saatini KAHİRE saatiyle yaz (kış saatinde İstanbul − 1 saat; yazın aynı) ve gerekirse "İstanbul saatiyle …" ekle.
  Site en alttaki telif satırında ("© … Designer by Abdullah Baydogan" yanında) "Sürüm / Build: GG.AA.YYYY SS:DD" gösterir; yayındaki `version.json` daha yeniyse üstte "Yeni sürüm — Yenile" şeridi çıkar. Kullanıcıya cevapta yeni sürüm saatini yaz ("en altta Sürüm / Build: … görünce yeni hâldesiniz").
- Kullanıcıya Türkçe açıkla; 2–3 dakika sonra Ctrl+F5 yapmasını söyle.
- Commit/PR metinlerine model adı yazma.

## Dosya haritası (TOKEN TASARRUFU — tüm dosyayı okuma)
`index.html` ≈ 5,5 MB / ~86.000 satır. **Asla tamamını okuma.** Sembolü `grep -n` ile bul, yalnız o aralığı `sed -n 'A,Bp'` ya da Read offset/limit ile oku. (Eski satır numaraları artık yanlış; hiç kullanma, hep grep.)
Başlıca semboller: `UI_TRANSLATIONS`/`setLanguage`/`BI_STATIC_TEXT`/`_DYN_DICT` (3 dil metinleri) · `defaultAuditQuestions`, `CUSTOMER_DOC_QUESTIONS`, `OEKOTEX_QUESTIONS`, `HR_QUESTIONS`, `AR_Q_TEXT` (sorular) · `_qMergeDefs`, `_uniqueQuestions`, `_syncMergedGroup`, `_linkFindingsToQuestions` (birleştirme/bulgu) · `DAILY_AUDIT_*` (günlük iç denetim) · `_pdfHeadHtml`, `_pdfAddCanvasA4`, `REPORT_SIGNATURE` (raporlar) · `save()`, `load()`, `_transactionalMergeSave` (bulut) · `TEAM_*`, `openTeamHub` (Performans Sistemi, DOKUNMA) · `requestApproval`, `openUserManagement`, `DEPARTMENT_SCOPES` (yetki) · `openDeptAudit*`, `openDepartmentsHub` (departman denetimi) · `openAboutHub`, `CERT_STATUS_META` (Hakkımızda/sertifika) · `openCustomerDashboard`, `openAddFindingForm` (müşteri) · `_chemicalDeptStats`, `openChemicalDeptReport` (kimyasal) · `EMSShell` (kabuk/menü). Modül notları (Ür-Ge, Kimyasal Excel, Ziyaretçi Kayıt): `docs/MODULLER.md`.

Bulut: Firestore belgeleri (`questions` tek belge, 1 MB sınırı) `save()` → `_transactionalMergeSave(docId, …)` ile yazılır.
**Soru belgeleri ikiye bölündü:** genel sorular `questions`, müşteri soruları (`_isCustQ`) `customerQuestions` belgesinde (bellekte tek `auditQuestions` dizisi; `_saveQuestionDocs`, `_qCombineCloud`, `_qDocsOf`; önce müşteri belgesi yazılır, başarılıysa eski kopyalar `_qPurgeLegacyCust` ile genel belgeden temizlenir; yazılamazsa her şey genel belgeye yazılır). Doğrudan belge işlemlerinde (`_safeArrayItemUpdate`, silme) `_qDocsOf(q)` kullan.

## Araçlar
- Bulut verisini okumak için ortam değişkeni `FIREBASE_SA_JSON` (yalnız okuma yetkili servis hesabı JSON'u) varsa Firestore'u doğrudan oku; ekran görüntüsüne güvenme.
- Kullanıcı Excel/belgeleri Google Drive'a atabilir; Drive bağlantısıyla al.
- `.claude/settings.json`: sık komutlar için kalıcı izinler.

## ÖNCE ANLAT, SONRA YAP (kullanıcı kuralı)
- **HAKKIYLA, 4x4 MÜKEMMEL YAP (kullanıcının ana kuralı):** her işi eksiksiz bitir; yarım, "sonra bakarız" bırakma. Teslimden önce kendin dene (masaüstü, mobil, 3 dil, hata yok), ekran görüntüsüyle kontrol et, bulduğun her kusuru düzelt. Kullanıcıya iş bırakma; yapılabilecek her şeyi sen yap. Yapamadığın bir şey varsa nedenini açıkça söyle.
- **HER ZAMAN ÖNCE GÖSTER:** her tasarım/ekran/rapor değişikliğinde önce örnek görsel (önce–sonra) gönder; onay gelmeden main'e alma (değişiklik dalda bekleyebilir).
- Yeni bir özellik, ayar, otomasyon, eklenti ya da kullanıcıdan bir işlem (silme, kurulum, ayar) isteyen her adımda: **önce ne yapacağını ve nedenini 2–3 kısa maddeyle anlat, kullanıcının onayını bekle, sonra yap.**
- Kullanıcıya adım adım, tek seferde tek iş ver; gerekirse ekran görüntüsü üzerinde işaretleyerek göster.
- Kısa ve net yaz; teknik terim kullanma.
- **Her işin sonunda** kullanıcının işini kolaylaştıracak en fazla 1–2 kısa öneri sun (araç, otomasyon, düzen, tasarruf); onay almadan yapma.

## Belge entegrasyonu ve senkron (kullanıcı kuralı, 27.10.2026, HER ZAMAN)
- Prosedür / talimat / politika / form (manifest.json + refs.json + Doküman Dizini) **birbirine bağlı ve eşit** tutulur. Yeni belge eklenince, belge kodu/adı değişince veya belge metnine atıf eklenince **`python3 araclar/belge_senkron.py --yaz`** çalıştır: Word/Excel metninden belge kodlarını okur, `prosedurler/refs.json`'ı (kim kime atıf yapıyor) günceller, aynı bölüm+numara grubundaki bağsız belgeleri aile kuralıyla bağlar ve tutarlılığı denetler (manifest kodu ↔ dosya adı ↔ Word başlık kodu, ölü dosya, yinelenen kod, site QMS eşleme tablosundaki hedefler). Rapor: `araclar/belge_senkron_rapor.json` (sorun 0 olmalı; bulunmayan atıf varsa kullanıcıya bildir).
- Belge kartında "Belge No" alanı (doc.docNo) vardır; ad "EMS.XX.YYY.NN.NN. Ad" biçimindeyse kod otomatik No etiketi olur (`_docSplit`).

## Müşteri formu hazır cevapları (kullanıcı kuralı, 27.10.2026, HER ZAMAN)
- Müşteri soru formu (Next COP, M&S, Inditex vb.) doldurulacağı zaman **önce Google Drive'daki özel klasöre bak: "EMS – Müşteri Formları (özel)"** (içinde "Next COP Pre-Audit – Hazır Cevaplar 1 ve 2" sayfaları, OKU belgesi ve kullanıcının yüklediği doldurulmuş form var). Aynı/benzer soruya aynı cevabı yaz; yeni bilgi gelince önce o sayfayı güncelle.
- Doldurulmuş form, belgeler, maaş/sigorta/ruhsat görselleri ve cevap listesi **GitHub'a KONMAZ** (depo herkese açık; işçi ve denetim bilgisi gizli). Yalnız bu kural burada durur.
- Cevaplarda gerçek dışı beyan yazma: belgesi olmayan şeyi "var" deme; belge adı/parsel/alan farkı varsa kullanıcıya bildir; hassas cevapları (pasaport, kesinti, sigorta) belgeyle destekle.

