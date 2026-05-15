# yapay-zeka-sinav
Yapay Zeka Eğitimi Online Sınav

## Google Apps Script Kurulum

1. `apps-script/Code.gs` dosyasındaki kodu Apps Script projesine yapıştırın.
2. `SPREADSHEET_ID` ve `RESULTS_SHEET_NAME` değerlerini kontrol edin.
3. `Deploy > Manage deployments > Edit` ekranında:
   - `Execute as`: **Me**
   - `Who has access`: **Anyone**
4. Deploy sonrası oluşan `/exec` URL'sini `index.html` içindeki `SCRIPT_URL` alanına yazın.
5. Apps Script'te `testManual()` çalıştırıp logda `{status:"ok"}` görün.

Not: `Execute as: User accessing the web app` seçilirse, diğer kullanıcılar Sheet/Mail yetkisi olmadığı için sonuçlar yazılamayabilir.

## E-posta gitmiyorsa

1. **Apps Script’te güncel `Code.gs`’i yapıştırıp yeniden deploy edin** (Manage deployments → Edit → Version: New version → Deploy). Eski sürüm çalışıyor olabilir.
2. **Gönderen adres (`from`)**: Kod artık `GmailApp.sendEmail` içinde **`from: SENDER_EMAIL` kullanmıyor**. Google, Gmail’de “Bu adres adına gönder” (Send mail as) doğrulanmamış bir adresle `from` kullanımında çoğu zaman hata verir; böylece **hiç mail çıkmaz**. Şu an gönderen, deployment’ı çalıştıran Google hesabıdır; yanıtlar `replyTo: metin@metintiryaki.com` ile gelir. “Gönderen” satırında mutlaka `metin@metintiryaki.com` görünsün istiyorsanız: Gmail → Ayarlar → Hesaplar → “Başka bir e-posta adresinden gönder” ile adresi doğrulayın; ardından isterseniz `Code.gs` içinde tekrar `from: SENDER_EMAIL` ekleyebilirsiniz.
3. **Kota**: Ücretsiz hesapta günlük Apps Script / Gmail kotası dolmuş olabilir. Ertesi gün deneyin veya [Apps Script quotas](https://developers.google.com/apps-script/guides/services/quotas) sayfasına bakın.
4. **Tablo sütunu**: `Sonuclar` sayfasında son sütunda `ERR: ...` yazıyorsa tam hata mesajı orada; `testManual()` çalıştırıp **Execution log**’a da bakın.
5. **Yetkilendirme**: Script ilk çalıştırmada Gmail izni istemiş olmalı; izin iptal edildiyse yeniden yetkilendirin.

