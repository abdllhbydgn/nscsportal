# HAFIZA — sohbetler arası defter (KISA TUT: en fazla ~70 satır)

Her sohbet başında oku. Sohbet sonunda "Son notlar"a 1–3 satır ekle; 70 satırı aşınca eski notları `HAFIZA_ARSIV.md`'ye taşı.
Eski kayıtların TAMAMI `HAFIZA_ARSIV.md`'de (≈250 KB): baştan okuma, yalnız `grep -n -i "konu" HAFIZA_ARSIV.md` ile ara.

## Kullanıcı hakkında
- Abdullah Baydoğan. Türkçe, kısa ve sade cevap ister; teknik terim sevmez.
- Her işin sonunda işini kolaylaştıracak en fazla 1–2 kısa öneri sun; onay almadan yapma.
- Önce anlat, onay al, sonra yap. Adım adım, tek seferde tek iş. Tasarım/ekran/rapor değişikliğinde önce örnek göster; "yayına al" denmeden main'e alma.
- Token tasarrufu: yeni iş = yeni sohbet (`/clear`); basit işler Sonnet; büyük dosyaları baştan okuma.

## Güncel durum (site)
- Site artık "NSCS Portal": https://abdllhbydgn.github.io/nscsportal/ (eski /ems/ ve /emsportal/ 404). Bu depo adı hâlâ `ems`. Ayrı depolar: nscstr (nscstr.com), arapca (Arapça Öğren), baydoganailesi (aile sitesi), emsportal klasörü eski adlı bir kopya (güncel çalışma deposu: ems).
- Yönetici YALNIZ nscstr.com e-postası; ziyaretçi girişi kapalı (`VISITOR_ENTRY_OPEN=false`); renk NSCS turuncusu #FF8000; favicon ince turuncu "n"; Arapça = MISIR lehçesi.
- Belge kodları dosya adı/manifest/refs'te bilerek `EMS.` kalır (metinde NSCS); Performans Sistemi dokunulmaz.
- WhatsApp: +20 120 640 37 42. Telif: "© 2023 NSCS" (yıl sabit). `eroglums.com` hiçbir yerde kalmasın.

## Kalıcı kullanıcı kararları (tekrar sorma)
- Mevcut düğme/özellik/bölüm kullanıcıya SORMADAN kaldırılmaz, gizlenmez, yeri değiştirilmez.
- Yetki modeli B (silme/değişiklik admin onayına, yeni kayıt doğrudan). Rapor indirme yalnız yönetici. Yönetici zorunlu eğitimden muaf (giriş penceresi yok).
- Müşteriler ve denetimler bağımsız; Organik bölüm tamamen ayrı; Excel formları birleştirilmez; yalnız numaralı formlar (EMS.XX.FRM…) kullanılır.
- Soru silme yalnız o bölümde, geri gelmez (`deletedDefaultQuestionIds`). Aynı belgeye çok kayıt yazma: TEK işlem (ayrı işlemler "failed-precondition" verir).
- Soru/bulgu satırı tek düzen: 👤 sorumlu düğmesi + ✉️ e-posta. 2. fotoğraf yuvası yalnız müşteri soru/bulgularında.
- Durum renkleri: Tamamlandı yeşil, Devam Ediyor turuncu, Başlanmadı/Açık kırmızı.
- Sedex yalnız 25 soru; H&M'de yalnız "CAP Onay Raporu" denetimi.
- Videolar: NSCS adı, EN ses + TR/AR altyazı, son sahne "Thank you" kartı (tek adres). Sahne klipleri `tanitim/kaynak/`.
- Müşteri formu cevapları: Google Drive özel klasörü "EMS – Müşteri Formları (özel)"; GitHub'a KONMAZ.
- TEKRAR ÖNERME: yönetime kimyasal özet e-postası; 4 pop-up maddesi (tahliye, yangın, makine koruyucu, eğitim-kaza); Takvim'e sertifika hatırlatması; otomatik e-posta için servis hesabı; Firebase eklentisi (bulutta çalışmıyor, bulut verisi için ekran görüntüsü iste).

## Kalıcı düzenler
- Aylık kimyasal Excel: kullanıcı Drive "EMS Excel" klasörüne atar (id 16WSQV8I0Zsva86vxM4ZHxcW0mZ6g36XT) → `kimyasal/` + manifest (ayrıntı: `docs/MODULLER.md`).
- Takvim: her ayın 1'i 09:00 "Excel'i klasöre at". Rutin "EMS aylık bakım" (trig_01HqMkBTdsu7Hm44aSWK7mXd): her ayın 2'si 07:47, Excel + 3 site kontrolü.
- Arapça (arapca) ve nscstr özetleri: arşivde "17.11.2026" ve "Arapça" kayıtları.

## Son notlar (en yeni üstte)
- 2026-11-23: Token tasarrufu: eski HAFIZA → `HAFIZA_ARSIV.md`; CLAUDE.md'den Ür-Ge/Kimyasal/Ziyaretçi bölümleri `docs/MODULLER.md`'ye taşındı, eski satır numaralı dosya haritası kaldırıldı (index.html ~86.000 satır). Site dışı işler: şeffaf/HD kaşe, Arapça iş sözleşmesi düzenleme (Word+PDF).
- 2026-11-22: Admin Paneli'nde "Yasal Dökümanlar" (`legalDocs`, `_ahubOpenLegalDocs`): Prosedürler'deki "yasal/legal" klasörleri orada açılır, Prosedürler listesinden gizlenir (veri taşınmadı). Şirket Profili Admin Paneli'nde, sol menüde yok.
- 2026-11-21: Sertifikalar = 23 kişisel sertifika (`sertifikalar/`, kimlik no/barkod/QR gizli); Hakkımızda'da "EMS" geçmemeli; Mısır+Türkiye saatleri (Arapça Öğren, nscstr).
- 2026-11-19: Büyük ekranlarda otomatik ölçekleme `<style id="ems-autofit">` (≥1700px zoom); yeni vh/vw yazarken `calc(N * var(--vh|--dvh|--vw))` biçimini kullan.
