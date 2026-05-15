# YZ Sınav — Deployment notları

**Deploy → Manage deployments** penceresindeki değerleri buraya yapıştırın. Her **New version → Deploy** sonrası bu dosyayı ve `index.html` içindeki `SCRIPT_URL` satırını güncelleyin.

| Alan | Değer |
|------|--------|
| **Son güncelleme** | *(tarih / saat)* |
| **Apps Script proje adı** | YZ Sınav |
| **Web app URL** (`.../exec`) | `[https://script.google.com/macros/s/BURAYA-TAM-URL/exec](https://script.google.com/macros/s/AKfycbwMu1jzZcUOJzvbvyCeJNIlTJHHFCqQZSSzN6S5cryZIsj6jDFyCqq31c8_D9NpbWyf/exec)` |
| **Deployment ID** AKfycbwMu1jzZcUOJzvbvyCeJNIlTJHHFCqQZSSzN6S5cryZIsj6jDFyCqq31c8_D9NpbWyf|
| **Library URL** | [*(Manage deployments’ta görünüyorsa buraya)*](https://script.google.com/macros/library/d/1YjrTGRf2H6d7N7TpRBklAyBx0FB7wceCQfFCpruhlC9Wz6EStADCsMXx/12) |
| **Script düzenleyici** | `https://script.google.com/home/projects/SCRIPT_PROJECT_ID/edit` |

## `index.html` ile eşleşme

Canlı sitede kullanılan adres şu satırda olmalı (`SCRIPT_URL`):

```text
index.html → var SCRIPT_URL=".../exec";
```

`DEPLOYMENT.md` ile `SCRIPT_URL` **aynı deployment**’ı göstermeli; aksi halde eski sürüm çalışır.

## Hızlı kontrol

1. Web app URL’yi tarayıcıda aç: `...?callback=cb&action=history&email=test@test.com`  
   Beklenen: JSON veya JSONP yanıtı (hata değil).
2. Apps Script’te `testManual()` çalıştır → mail + Sheet satırı.
