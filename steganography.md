### Cara Menyembunyikan File di Dalam Gambar (Steganography)

Di Windows, Anda bahkan bisa melakukannya secara gratis tanpa *software* tambahan, cukup menggunakan **Command Prompt (CMD)** dan *tool* kompresi gratis seperti **7-Zip** atau WinRAR.

Cara paling populer dan mudah di Windows adalah dengan menyatukan file gambar (misal `.jpg`) dengan file arsip (`.zip` atau `.rar`) yang berisi dokumen rahasia Anda.

Berikut adalah langkah-langkah mempraktikkannya kembali:

**1. Siapkan Bahan**

* Siapkan satu gambar biasa, misalnya namanya `image.jpg`.
* Masukkan semua file rahasia Anda ke dalam satu folder, lalu kompres folder tersebut menjadi file ZIP atau RAR. Beri nama, misalnya `result.zip`.
* Satukan kedua file tersebut (`image.jpg` dan `result.zip`) di dalam satu folder yang sama.

**2. Buka Command Prompt (CMD)**

* Tekan tombol `Windows + R`, ketik `cmd`, lalu tekan Enter.
* Masuk ke folder tempat Anda menyimpan file tadi dengan perintah `cd`.
* Ketik perintah berikut ini dengan teliti, lalu tekan Enter:

```cmd
copy /b image.jpg + secretfile.zip result.jpg
```

* *Penjelasan:* Perintah `/b` artinya kita menggabungkan file dalam bentuk biner. File `image.jpg` dan `secretfile.zip` akan digabungkan menjadi file baru bernama `result`.

**4. Selesai!**
Sekarang Anda akan melihat file baru bernama `result.jpg`. Jika file ini diklik dua kali, ia akan terbuka sebagai gambar biasa yang menampilkan foto pemandangan. Orang lain tidak akan curiga sama sekali.

---

### Bagaimana Cara Membuka Kembali File Rahasianya?

Untuk mengambil atau melihat file rahasia di dalamnya, caranya sangat mudah:

1. **Menggunakan 7-Zip / WinRAR:** Klik kanan pada file `result.jpg`, pilih **Open With**, lalu pilih **7-Zip File Manager** atau **WinRAR**. Anda akan melihat file `secretfile.zip` di dalamnya dan bisa langsung mengekstraknya.
2. **Ubah Ekstensi:** Cara alternatifnya, Anda tinggal mengubah nama file (`rename`) dari `result.jpg` menjadi `result.zip`. Setelah berubah menjadi folder ZIP, Anda bisa membuka dan mengekstrak isinya seperti biasa.

---

### ⚠️ Catatan Penting untuk Saat Ini (Tahun 2026)

Meskipun trik ini masih bekerja 100% di komputer lokal Anda, ada beberapa hal yang harus Anda perhatikan jika berniat mengirimkannya:

* **Jangan Kirim Lewat Chat Sosmed/Instant Messenger:** Jika Anda mengirim file `result.jpg` ini lewat WhatsApp, Telegram, atau mengunggahnya ke Facebook/Instagram sebagai *image*, sistem mereka akan melakukan **kompresi otomatis** untuk menghemat bandwidth. Proses kompresi ini akan menghapus kode biner ZIP yang ada di ekor file gambar, sehingga file rahasia Anda akan hilang dan menyisakan gambarnya saja.
* **Solusi Pengiriman:** Jika ingin mengirimkannya, kirimlah sebagai **Dokumen** (bukan foto/media) di WhatsApp, atau kompres kembali ke dalam format ZIP biasa sebelum diunggah ke cloud/email.