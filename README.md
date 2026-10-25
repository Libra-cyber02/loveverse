# LOVEVERSE — Our Little World 💗

Website game couple untuk pasangan LDR. Dibuat dengan HTML, CSS, JavaScript module, dan Firebase Realtime Database.

## Fitur di versi ini
1. **Seberapa Kenal Kita?** — jawab pertanyaan tentang pasangan dan lihat apakah jawaban cocok.
2. **Truth or Dare** — prompt truth dan dare yang ringan.
3. **Our Memories** — simpan kenangan bersama.
4. **Mini Games** — Tic-tac-toe, Batu Gunting Kertas, Sambung Kata, Tebak Emoji.
5. **Dream House** — kumpulkan love coins dan beli dekorasi rumah virtual.
6. **Love Detective** — puzzle singkat dengan pesan rahasia.
7. **Virtual Date Night** — pilih dan simpan rencana kencan.

## Penting: demo vs multiplayer lintas perangkat
- **Demo mode:** UI dan sebagian permainan berjalan, tetapi room hanya tersimpan di memori browser yang membuatnya. Kode demo tidak bisa dipakai pasangan dari perangkat berbeda.
- **Firebase mode:** setelah konfigurasi Firebase disiapkan, room dan data game disinkronkan lewat Realtime Database. Firebase Anonymous Authentication dipakai agar tiap pemain punya ID.
- Untuk pengalaman dua perangkat yang sebenarnya, lakukan setup Firebase berikut sebelum publish.

## Setup Firebase (gratis untuk mulai)
1. Buka https://console.firebase.google.com/ lalu buat project baru.
2. Di **Build → Authentication → Sign-in method**, aktifkan **Anonymous**.
3. Di **Build → Realtime Database**, buat database. Pilih region terdekat, misalnya Singapore jika tersedia.
4. Di **Project settings → General → Your apps**, tambahkan Web App dan salin konfigurasi SDK.
5. Ganti nilai `firebaseConfig` di bagian atas `app.js` dengan konfigurasi project kamu. Isi `databaseURL` dengan URL persis yang diberikan Firebase.
6. Di **Authentication → Settings → Authorized domains**, pastikan domain GitHub Pages kamu diizinkan jika diperlukan.

### Database Rules untuk uji coba
**Jangan gunakan rules terbuka ini untuk data pribadi atau publik.** Rules ini hanya untuk tes cepat dan tidak membatasi akses berdasarkan anggota room. Sebelum dipakai serius, buat rules yang membatasi akses hanya kepada dua anggota room dan validasi bentuk data.

Untuk uji awal saja, Firebase Realtime Database Rules dapat sementara memakai:
```json
{
  "rules": {
    "rooms": {
      "$roomId": {
        ".read": "auth != null",
        ".write": "auth != null"
      }
    }
  }
}
```
Aturan tersebut mengizinkan pengguna yang sudah login anonim membaca/menulis semua room. Itu bukan keamanan yang layak untuk produksi. Jangan simpan informasi sensitif. Untuk pemakaian publik, gunakan rules per-room yang memeriksa anggota room, batas pemain, dan validasi data.

## Publish ke GitHub Pages
1. Buat repository baru di GitHub, misalnya `loveverse`.
2. Upload `index.html`, `style.css`, `app.js`, dan `README.md` ke root repository (bukan hanya file ZIP).
3. Buka **Settings → Pages**.
4. Pada **Build and deployment**, pilih **Deploy from a branch**.
5. Pilih branch `main` dan folder `/(root)`, lalu **Save**.
6. Tunggu proses deploy, lalu buka URL yang diberikan GitHub Pages.

## Cara main bareng
1. Buka website di perangkat pertama dan isi nama panggilan.
2. Klik **Buat room baru**.
3. Salin kode room dan kirim ke pasangan.
4. Pasangan buka URL website yang sama, isi nama, masukkan kode, lalu klik **Gabung**.
5. Pastikan status di kanan atas menunjukkan **Terhubung real-time**.

## Catatan teknis / batasan
- Versi ini adalah starter lengkap, bukan layanan game yang sudah diaudit keamanannya.
- Demo mode tidak lintas perangkat; Firebase wajib dikonfigurasi untuk realtime.
- Untuk deploy publik, jangan memakai database rules terbuka. Tambahkan security rules yang benar dan uji dua akun/perangkat.
- Semua aktivitas yang disimpan ke Firebase berada di database project milikmu. Jangan masukkan data sensitif.
- Karena menggunakan JavaScript modules dan Firebase CDN, jalankan lewat hosting seperti GitHub Pages atau server lokal, bukan membuka `index.html` sebagai `file://`.
