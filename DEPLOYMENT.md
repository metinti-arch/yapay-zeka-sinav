# YZ Sınav — Deployment notları

**Deploy → Manage deployments** penceresindeki değerleri buraya yapıştırın. Her **New version → Deploy** sonrası bu dosyayı ve `index.html` içindeki `SCRIPT_URL` satırını güncelleyin.

| Alan | Değer |
|------|--------|
| **Son güncelleme** | *(tarih / saat)* |
| **Apps Script proje adı** | YZ Sınav |
| **Web app URL** (`.../exec`) | `https://script.google.com/macros/s/BURAYA-TAM-URL/exec` |
| **Deployment ID** (URL’de `/s/` ile `/exec` arası) | `AKfycb...` |
| **Library URL** | *(Manage deployments’ta görünüyorsa buraya)* |
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
