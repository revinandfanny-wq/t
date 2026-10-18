# Checklist sebelum build APK

[ ] Deploy web Dika Tools ke URL HTTPS yang tetap.
[ ] Set `RAPIDAPI_KEY` pada environment server bila API TikTok/Spotify memerlukannya.
[ ] Set `RESEND_API_KEY` bila ingin bukti Support Developer otomatis masuk email.
[ ] Pastikan `qris-support.jpg` tetap berada di root deploy.
[ ] Buka Dika Tools → Spotify → tempel Client ID → Simpan ID.
[ ] Salin Redirect URI yang tampil.
[ ] Masukkan Redirect URI persis sama di Spotify Developer Dashboard.
[ ] Login Spotify dari Dika Tools.
[ ] Untuk full playback, gunakan akun Spotify yang memenuhi syarat Web Playback.
[ ] Untuk Galeri Android, build APK memakai folder `android/`, bukan hanya index.html.


### RapidAPI TikTok
The supplied RapidAPI key is already embedded server-side in `api/tiktok.js` as a fallback, so Vercel RAPIDAPI_KEY is optional for this build. The key is not placed in client-side HTML/JS. For security, rotate the key if it has been shared publicly.
