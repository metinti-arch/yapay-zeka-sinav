# yapay-zeka-sinav
Yapay Zeka Eğitimi Online Sınav

## Google Apps Script Kurulum

1. `apps-script/Code.gs` dosyasındaki kodu Apps Script projesine yapıştırın.
2. `SPREADSHEET_ID` ve `RESULTS_SHEET_NAME` değerlerini kontrol edin.
3. `Deploy > Manage deployments > Edit` ekranında:
   - `Execute as`: **Me**
   - `Who has access`: **Anyone**
4. Deploy sonrası oluşan `/exec` URL'sini:
   - `index.html` içindeki `SCRIPT_URL` değişkenine yazın;
   - aynı bilgileri **`DEPLOYMENT.md`** dosyasına kopyalayın (bir sonraki deploy’da neyin aktif olduğunu unutmamak için).
5. **(Önerilir)** `apps-script/appsscript.json` içeriğini projede manifest olarak ekleyin: **Project Settings** (dişli) → **Show "appsscript.json" in editor** açık olsun → sol dosya listesinde `appsscript.json` oluşturup repodaki JSON’u yapıştırın. Böylece Gmail/Sheet izinleri net talep edilir.
6. Apps Script'te `testManual()` çalıştırın; ilk çalıştırmada **izin ekranı** gelirse aşağıdaki **“The script does not have permission…”** başlığındaki adımlarla **Allow** verin. Sonra logda `{status:"ok"}` ve `emailSent: true` hedeflenir.

Not: `Execute as: User accessing the web app` seçilirse, diğer kullanıcılar Sheet/Mail yetkisi olmadığı için sonuçlar yazılamayabilir.

## E-posta gitmiyorsa

1. **Apps Script’te güncel `Code.gs`’i yapıştırıp yeniden deploy edin** (Manage deployments → Edit → Version: New version → Deploy). Eski sürüm çalışıyor olabilir.
2. **Gönderen adres (`from`)**: Kod artık `GmailApp.sendEmail` içinde **`from: SENDER_EMAIL` kullanmıyor**. Google, Gmail’de “Bu adres adına gönder” (Send mail as) doğrulanmamış bir adresle `from` kullanımında çoğu zaman hata verir; böylece **hiç mail çıkmaz**. Şu an gönderen, deployment’ı çalıştıran Google hesabıdır; yanıtlar `replyTo: metin@metintiryaki.com` ile gelir. “Gönderen” satırında mutlaka `metin@metintiryaki.com` görünsün istiyorsanız: Gmail → Ayarlar → Hesaplar → “Başka bir e-posta adresinden gönder” ile adresi doğrulayın; ardından isterseniz `Code.gs` içinde tekrar `from: SENDER_EMAIL` ekleyebilirsiniz.
3. **Kota**: Ücretsiz hesapta günlük Apps Script / Gmail kotası dolmuş olabilir. Ertesi gün deneyin veya [Apps Script quotas](https://developers.google.com/apps-script/guides/services/quotas) sayfasına bakın.
4. **Tablo sütunu**: `Sonuclar` sayfasında son sütunda `ERR: ...` yazıyorsa tam hata mesajı orada; `testManual()` çalıştırıp **Execution log**’a da bakın.
5. **Yetkilendirme**: Script ilk çalıştırmada Gmail izni istemiş olmalı; izin iptal edildiyse yeniden yetkilendirin.

### “The script does not have permission to perform that action” (mail)

Bu hata **kod hatası değil**; Google hesabı `GmailApp` / `MailApp` için **OAuth izni vermemiş** demektir.

1. Apps Script editörde üstten **`testManual`** fonksiyonunu seç → **Run** (Çalıştır).
2. **“Authorization required”** çıkarsa → **Review permissions** → Google hesabını seç.
3. **“Google hasn’t verified this app”** uyarısı çıkabilir → **Advanced** → **Go to … (unsafe)** → devam et (kendi projen).
4. Listede **Gmail** / **Send email on your behalf** / **Google Sheets** vb. → **Allow**.
5. **Executions** panelinde tekrar **Run** → logda `emailSent: true` veya Sheet’te mail sütunu **OK** olmalı.

Projeye **`appsscript.json`** (repoda `apps-script/appsscript.json`) eklediysen: Apps Script sol menüde **Project Settings** → ilgili ayarlar veya dosyayı manuel ekle; bir sonraki çalıştırmada Google **yeni kapsamlar** için tekrar izin isteyebilir — yine **Allow** deyin.

**Workspace (kurumsal) hesap:** Yönetici `script.google.com` / Gmail API kullanımını kısıtlıyorsa aynı hata görülür; IT’den “Apps Script + Gmail send” açılmasını isteyin.

