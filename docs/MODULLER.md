# Modül notları (CLAUDE.md'den taşındı, içerik aynı)

İlgili modül üzerinde çalışırken oku: Ür-Ge/Ar-Ge, Kimyasal tüketim Excel'i, Ziyaretçi Kayıt.

## Ür-Ge - Ar-Ge Departmanı (kullanıcı isteği, 17-19.10.2026)
- Adı "Ür-Ge - Ar-Ge Departmanı" (kullanıcı kararı; ürün geliştirme = Ür-Ge, araştırma ve geliştirme = Ar-Ge; her projede `kind`: urge|arge, aşamaları farklı: `URGE_STAGES` / `ARGE_STAGES`; Ar-Ge alanları: hedef, bütçe, hibe, patent, sonuç). Sol menüde Yönetim Merkezi'nin altında "Ür-Ge - Ar-Ge Departmanı" düğmesi (`nav_urge`, `openUrge`); sayfa `#urge-modal` (qa-dept-overlay), kod/CSS `<script id="urge-module">` + `<style id="urge-css">` (index.html, cert-hub-modal'ın hemen üstü / ems-scroll-top düğmesinin üstü).
- Veri: bulutta AYRI `urge` belgesi (`urgeProjects`, `urgeSamples`, `urgeTests`); fotoğraf `_saveDocFileData("urge", id, "photo"/"photo2"/"photo3")`. Yetki: Kullanıcı Yönetimi'nde "Ür-Ge" kapsamı (`DEPARTMENT_SCOPES` key `urge`, `_REC_POLICY.urge*`); giriş yapan herkes görür, kapsamı olan/ yönetici düzenler (personel değişikliği/silme onaya düşer).
- Sekmeler: Pano, Projeler (aşama: Fikir→Tasarım→Numune→Test→Müşteri Onayı→Üretime Hazır→Tamamlandı), Numuneler (tur R1,R2; Revize→Yeni Tur), Testler, Raporlar (PDF `urgeDownloadPDF`, Excel `urgeDownloadXlsx`). Ür-Ge verisi yedeğe dahildir (`_extraBackupFields` / `_restoreExtraBackupFields`).

## Kimyasal tüketim Excel'i (her ay)
- Kullanıcının aylık dosyası "Monthly Consumption" biçimidir: malzeme başına 1 satır, A–I kimlik + açılış, her gün 6 sütun (Opening, Received, To Prod., Returned, Consum., Closing). `_chemImportMonthlyWide` okur; ay/yıl başlıktan alınır; o ayın kayıtları dosyadaki son hâlle değiştirilir.
- Mantık: Tüketim = Üretime çıkış − İade; Kapanış = Açılış + Giriş − Tüketim; ay sonu stok = sonraki ay başı (tutarsızlık uyarılır).
- **Kullanıcı yeni aylık Excel verdiğinde:** dosyayı `kimyasal/` klasörüne `YYYY-AA_Baski_Kimyasal_Tuketim.xlsx` adıyla koy, `kimyasal/manifest.json`'a `{file, period, rev}` ekle (aynı ay güncellenirse `rev` değiştir). Site admin açılışında `_chemAutoImportMaybe` ile otomatik içe aktarır; işlenen dosyalar bulutta `chemExcelRevs`.
- Ay geçişi uzlaştırması `_chemReconcile`: ay başı sayım > önceki ay sonu → o ayın 1'inde giriş (`chemadj_in_*`); eksik → önceki ayın son günü kullanım (`chemadj_out_*`); sonradan eklenen malzemenin ilk stoğu giriş; ayın listesinde olmayan malzeme o ay 0 (`chemabs_*`).
- Gömülü `defaultChemicalMaterials/Records` (Ağustos–Eylül) buluta yalnız `CHEM_SEED_V` değişince bir kez yazılır; bu sabiti gereksiz değiştirme (bulut kimyasal verisini sıfırlar).
- Ana sayfa kartları, tüketim ekranı ve rapor aynı dönemi (`_chemSelectedPeriod`) kullanır; aylık seri (Ağustos→) rapor, ekran ve PDF'te gösterilir.

## Ziyaretçi Kayıt (kullanıcı isteği, 27.10.2026)
- Sol menüde Ür-Ge'nin altında "Ziyaretçi Kayıt" (`nav_visitor`, `openVisitor`); sayfa `#visitor-modal`, kod/CSS `<script id="visitor-module">` + `<style id="visitor-css">` (index.html, ems-scroll-top düğmesinin üstü). Form = EMS.İD.FRM.03.01 (Ziyaretçi/Tedarikçi Güvenlik Bilgilendirme) sitede doldurulur: ziyaretçi bilgileri, amaç, 7 güvenlik kuralı onayı, parmak/fare imzası, çıkış saati tek tıkla; Bugün + Kayıtlar sekmeleri, Excel/PDF, kişi başı form PDF'i (`vzPrintForm`).
- Veri: bulutta AYLIK belgeler `visitors_YYYY_MM` (alan `visits`; 1 MB sınırı için aylık bölündü); imza resim değil küçük çizgi dizisi (`_vzEnc/_vzDec`). `_REC_POLICY` YOK (güvenlik görevlisi çıkış saatini onaysız yazar); silme yalnız admin (Firestore kuralları da personele silme vermez). Yetki: Kullanıcı Yönetimi'nde "visitor" kapsamı (`DEPARTMENT_SCOPES`) veya admin; yetkisiz kişi sayfayı göremez (kimlik no KVKK).
- Metinlerde " / " kullanma (site iki dilli ayırıcı kesiyor): "ve/veya" yaz.
