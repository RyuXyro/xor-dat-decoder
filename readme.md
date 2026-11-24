# 🛠️ Game .DAT Asset Tool (XOR 0x5A)

Alat berbasis web (*client-side*) ringan tanpa perlu instalasi server untuk mendekripsi, melihat pratinjau, mengekstrak, dan mengemas ulang (*repack*) file arsip `.dat` yang digunakan pada aset *game* (seperti *engine* Cocos2d-x).

Seluruh proses berjalan 100% secara lokal di dalam *browser* Anda sehingga aman dan cepat.

## ✨ Fitur Utama

1. **Batch Unpack (`.dat` ➔ `.zip`):** Memproses banyak file `.dat` sekaligus menjadi file `{namafile}.zip` standar.
2. **Limitasi Jumlah File:** Pengaturan untuk membatasi berapa banyak file `.dat` yang ingin diproses dalam satu waktu (`0` = proses semua).
3. **Pratinjau Isi Otomatis (*Live Inspector*):** Membaca dan menampilkan isi teks file konfigurasi seperti `.plist`, `.sha`, `.vsha`, `.xml`, atau `.json` langsung di layar tanpa perlu mengekstrak ZIP terlebih dahulu.
4. **Repack / Kunci Ulang (`.zip` ➔ `.dat`):** Mengenkripsi kembali arsip `.zip` yang sudah Anda edit menjadi format `.dat` siap pakai di dalam *game*.
5. **Kustomisasi Kunci XOR:** Secara *default* menggunakan kunci `0x5A` (huruf `Z`), namun dapat diubah sesuai kebutuhan.

---

## 🚀 Cara Penggunaan

### Opsi A: Langsung dari Komputer (Offline)
1. Unduh atau *clone* repositori ini.
2. Klik dua kali file **`index.html`** untuk membukanya di *browser* (Chrome, Edge, Firefox, Safari).

### Opsi B: Via GitHub Pages (Online)
1. Buka tab **Settings** > **Pages** di repositori GitHub ini.
2. Pada bagian *Branch*, pilih `main` dan klik **Save**.
3. Akses alat ini kapan saja melalui tautan GitHub Pages yang muncul.

---

## 📖 Panduan Langkah demi Langkah

### 1. Membuka & Mengekstrak File `.dat`
1. Buka `index.html` di *browser*.
2. *(Opsional)* Atur **Maksimal File** jika Anda hanya ingin memproses sejumlah file tertentu.
3. Seret dan lepas (*Drag & Drop*) file-file `.dat` ke area kotak **1. Unpack File**.
4. Klik tombol **👁️ Lihat Isi** untuk mengecek daftar file dan membaca kode `.plist` / `.sha` di dalamnya.
5. Klik **⬇️ Unduh ZIP** (atau **⬇️ Unduh Semua**) untuk menyimpan hasil konversi `{namafile}.zip`, lalu ekstrak menggunakan WinRAR / 7-Zip.

### 2. Mengunci Kembali Aset Menjadi `.dat` (*Repack*)
1. Setelah selesai mengedit aset di dalam folder hasil ekstraksi, kompres kembali isi folder tersebut menjadi file **`.zip`**.
   > ⚠️ **Penting:** Pastikan Anda mengompres **isi di dalam foldernya** (misalnya folder `shader/` atau `particles/` langsung berada di tingkat teratas ZIP, bukan terbungkus folder induk tambahan).
2. Seret file `.zip` tersebut ke area kotak **2. Repack File**.
3. Klik **⬇️ Unduh .DAT** untuk mendapatkan file `.dat` baru yang siap dimasukkan kembali ke folder *game*.

---

## 🔧 Cara Kerja Teknis
File `.dat` pada proyek ini sebenarnya adalah arsip **ZIP standar** yang setiap *byte*-nya disamarkan menggunakan operasi bitwise **XOR** dengan kunci `0x5A` (karakter ASCII `Z`), sehingga *header* asli ZIP (`50 4B 03 04` / `PK..`) berubah menjadi `0A 11 59 5E` (`Y^NZZZ...`). Alat ini membalikkan operasi tersebut di memori *browser* menggunakan JavaScript `Uint8Array` dan `JSZip`.

---

## 💡 Tips & Pemecahan Masalah (Troubleshooting)

1. **File Gagal Dikenali Sebagai ZIP Valid?**
   * Pastikan kunci XOR yang digunakan sudah benar. Secara *default* game Cocos2d-x menggunakan `0x5A`, namun beberapa game mungkin menggunakan kunci kustom lain (misalnya `0x33` atau `0xAB`). Anda dapat mengubahnya melalui kotak input **Kunci XOR** di halaman web.
2. **Game Crash Setelah File `.dat` Dimasukkan Kembali?**
   * Pastikan saat melakukan *repack* folder menjadi `.zip`, struktur foldernya tidak bersarang ganda. 
   * **Benar:** Di dalam file `.zip` langsung terdapat file/folder aset (seperti `image.png`, `config.plist`, dll.).
   * **Salah:** Di dalam file `.zip` terdapat satu folder utama dulu, baru di dalamnya berisi aset.

---
*Dibuat untuk memudahkan modifikasi aset game berbasis Cocos2d secara cepat, aman, dan tanpa instalasi rumit.*
