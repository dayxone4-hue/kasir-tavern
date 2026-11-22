# Kasir Coffee Tavern (Firebase + GitHub Pages)

Gratis memakai paket Firebase Spark dan GitHub Pages.

## 1. Buat proyek Firebase
1. Buka https://console.firebase.google.com lalu klik **Add project**, beri nama (misal `coffee-tavern`). Google Analytics boleh dimatikan.
2. Di halaman proyek, klik ikon **Web (</>)**, beri nama aplikasi, **tidak perlu** centang Firebase Hosting, lalu **Register app**.
3. Salin isi `firebaseConfig`, tempel ke berkas `firebase-config.js` (ganti semua nilai "ISI...").

## 2. Aktifkan Authentication
1. Menu **Build > Authentication > Get started**.
2. Tab **Sign-in method** > **Email/Password** > aktifkan > Save.

## 3. Buat database Firestore
1. Menu **Build > Firestore Database > Create database**.
2. Lokasi: `asia-southeast2 (Jakarta)`. Mode: **Production**.
3. Tab **Rules**: hapus isinya, tempel seluruh isi `firestore.rules`, klik **Publish**.

## 4. Buat kode verifikasi awal
Di tab **Data** Firestore: **Start collection** > Collection ID `config` > Document ID `reg` > tambah field `code` (string) berisi `1234TVN` > Save.
Kode ini tidak bisa dibaca dari web; hanya bisa diganti oleh barista yang login (Pengaturan akun > Ganti kode).

## 5. Izinkan domain GitHub Pages
**Authentication > Settings > Authorized domains > Add domain**: `USERNAME.github.io` (ganti USERNAME dengan nama akun GitHub Anda).

## 6. Unggah ke GitHub
1. Buat akun di https://github.com lalu **New repository** (misal `kasir-tavern`), tipe Public.
2. **Add file > Upload files**, unggah SEMUA berkas di folder ini kecuali folder `JANGAN-DIUNGGAH` (`index.html`, `sw.js`, `manifest.webmanifest`, `firebase-config.js`, `qris.jpg`, `icon-192.png`, `icon-512.png`, `firestore.rules`, `README.md`). Klik **Commit changes**.
3. **Settings > Pages**: Source = **Deploy from a branch**, Branch = `main`, folder `/ (root)` > Save.
4. Tunggu 1-2 menit; alamat web: `https://USERNAME.github.io/kasir-tavern/`

PENTING: repositori Public bisa dilihat siapa saja. Jangan unggah `data-awal.json` (berisi data penjualan). Isi `firebase-config.js` memang boleh publik.

## 7. Daftar akun pertama dan pindahkan data lama
1. Buka alamat web, tekan **Daftar**, isi username, PIN 4-8 angka, dan kode verifikasi `1234TVN`.
2. Klik nama akun di kanan atas > **Impor data lama** > pilih `JANGAN-DIUNGGAH/data-awal.json` > **Impor**. Lakukan SEKALI saja.
3. Akun lama tidak ikut pindah; setiap barista mendaftar ulang.

## 8. Pasang di HP/tablet
Android Chrome: menu titik tiga > **Install app / Tambahkan ke layar utama**. iPhone Safari: Share > **Add to Home Screen**. Setelah dibuka sekali dengan internet, web bisa dibuka dan dipakai offline; data dikirim otomatis saat tersambung.

## Catatan
- Rekomendasi: Google Cloud Console > APIs & Services > Credentials > API key > batasi ke `USERNAME.github.io/*`.
- Kuota gratis Spark: 50.000 pembacaan, 20.000 penulisan, 1 GB per hari/total. Cukup untuk satu kafe; pantau di Firebase Console > Usage.
- PIN dikirim ke Firebase sebagai `tvn-` + PIN (Firebase mewajibkan minimal 6 karakter). Pembekuan 3x salah (1 menit) berlaku per perangkat; Firebase juga membatasi percobaan berlebih sendiri.
- Cadangan: pakai Laporan > Unduh arsip bulanan secara rutin.
- Mengubah aplikasi: edit `index.html` di GitHub, lalu naikkan angka `V` di `sw.js` (misal `tavern-v2`) agar perangkat memuat versi baru.
