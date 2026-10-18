# Dika Tools TikTok V4 Fix

Perbaikan utama:
- Menggunakan endpoint RapidAPI `/vid/index` terlebih dahulu.
- Provider ini mengembalikan video pada field `video` (umumnya array), lalu server menormalisasikannya menjadi `video`.
- `/index` hanya menjadi fallback.
- API key tetap hanya dipakai di server (`api/tiktok.js`), dengan fallback key yang sudah diberikan pengguna.
- Frontend memakai `data.video` dari endpoint server.
- `api/download.js` tetap melakukan streaming file agar video tidak dimuat seluruhnya ke RAM.

Deploy seluruh folder/ZIP ini ke Vercel. Jangan hanya upload `index.html`.
