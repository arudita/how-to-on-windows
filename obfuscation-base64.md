# Obfuscation (Pengaburan Data/Script)

Konsep ini sebenarnya memiliki kesamaan dengan apa yang sering terjadi di dunia pengembangan web—seperti saat kode JavaScript diproses menggunakan *bundler* atau di-*uglify* agar ukurannya lebih kecil dan logikanya tidak mudah dibaca orang lain.

Namun, di lingkungan Windows, *obfuscation* biasanya diterapkan pada skrip baris perintah (seperti **PowerShell**, **Batch/CMD**, atau **VBScript**) dengan tujuan menyembunyikan niat atau logika skrip dari pengguna manusia, maupun dari perangkat lunak keamanan (seperti Antivirus).

Berikut adalah konsep dan teknik *obfuscation* yang paling umum dan bahkan didukung secara resmi oleh Windows. Mengubah perintah teks biasa menjadi format Base64 membuatnya terlihat seperti deretan karakter acak.

* **Contoh Kasus:** Anda memiliki perintah PowerShell sederhana: `Write-Host "Halo Dunia"`
* Jika diubah ke Base64, perintah tersebut menjadi: `VwByAGkAdABlAC0ASABvAHMAdAAgACIASABhAGwAbwAgAEQAdQBuAGkAYQAiAA==`
* **Cara Eksekusi:** Windows PowerShell memiliki parameter khusus untuk menjalankan teks Base64 ini tanpa harus mendekodenya secara manual, yaitu menggunakan parameter `-EncodedCommand`:
```powershell
powershell.exe -EncodedCommand VwByAGkAdABlAC0ASABvAHMAdAAgACIASABhAGwAbwAgAEQAdQBuAGkAYQAiAA==
```
---

Pada dasarnya, Base64 adalah algoritma yang mengubah data biner (angka 0 dan 1 yang dipahami komputer) menjadi teks ASCII yang aman dan bisa dibaca (huruf A-Z, a-z, angka 0-9, serta simbol `+` dan `/`). Karena semua file di komputer—baik itu teks, gambar, dokumen PDF, hingga aplikasi `.exe`—pada dasarnya adalah data biner, maka **semua jenis file dan teks bisa diubah menjadi Base64**.

Di dunia pengembangan web, teknik ini sangat lumrah digunakan. Contohnya, menyematkan gambar berukuran kecil langsung ke dalam kode HTML atau CSS (`data:image/png;base64,...`) agar browser tidak perlu melakukan HTTP *request* tambahan untuk memuat gambar tersebut. Di Windows, prinsipnya sama persis, namun sering dimanfaatkan untuk menyisipkan *script* atau memindahkan file tanpa harus mengunduh file fisiknya.

Berikut adalah langkah-langkah praktis untuk melakukan *encoding* dan *decoding* Base64 di Windows menggunakan **PowerShell**.

#### Mengubah Teks Biasa Menjadi Base64

Anda bisa mencoba ini langsung di terminal.

1. Buka aplikasi **Windows PowerShell**.
2. Masukkan teks yang ingin disandikan ke dalam sebuah variabel. Ketik perintah berikut dan tekan Enter:
```powershell
$teks = "Belajar Obfuscation di Windows"
```

3. Ubah teks tersebut menjadi format *byte*:
```powershell
$bytes = [System.Text.Encoding]::UTF8.GetBytes($teks)
```

4. Ubah *byte* tersebut menjadi string Base64:
```powershell
$base64 = [Convert]::ToBase64String($bytes)
```

5. Tampilkan hasilnya dengan mengetikkan variabelnya:
```powershell
$base64
```

*(Hasilnya akan terlihat seperti: `QmVsYWphciBPYmZ1c2NhdGlvbiBkaSBXaW5kb3dz`)*

#### Mengembalikan Base64 Menjadi Teks Asli (Decoding)

Jika Anda menemukan teks acak yang dicurigai sebagai Base64, Anda bisa menerjemahkannya kembali:

1. Simpan teks sandi di variabel:
```powershell
$sandi = "QmVsYWphciBPYmZ1c2NhdGlvbiBkaSBXaW5kb3dz"
```

2. Ubah kembali menjadi *byte*:
```powershell
$bytes = [Convert]::FromBase64String($sandi)
```

3. Terjemahkan *byte* menjadi teks asli:
```powershell
$teksAsli = [System.Text.Encoding]::UTF8.GetString($bytes)
$teksAsli
```

#### Mengubah File Utuh Menjadi Base64

Jika Anda ingin menyandikan file (misalnya gambar, konfigurasi, atau dokumen), perintahnya bisa disingkat menjadi satu baris:

```powershell
$base64File = [Convert]::ToBase64String([IO.File]::ReadAllBytes("C:\lokasi\file\anda.jpg"))
```

*(Variabel `$base64File` sekarang berisi teks sangat panjang yang merupakan wujud gambar Anda. Anda bisa menyimpannya ke file `.txt` untuk disembunyikan atau dipindahkan).*

Untuk mengembalikan teks Base64 yang tersimpan di dalam file `.txt` menjadi file utuh (misalnya menjadi gambar `.jpg` atau dokumen), logika yang digunakan adalah kebalikan dari proses sebelumnya.

Kita harus membaca teks Base64 tersebut, mengubahnya kembali menjadi *byte* (biner), lalu menyimpannya ke dalam bentuk file fisik.

#### Langkah 1: Membaca Isi File .txt

Pertama, kita harus menyuruh PowerShell membaca seluruh teks yang ada di dalam file `.txt` Anda dan menyimpannya ke dalam variabel.

```powershell
$teksBase64 = [IO.File]::ReadAllText("C:\lokasi\file_rahasia.txt")
```

*(Perintah `ReadAllText` sangat disarankan karena ia akan membaca keseluruhan isi file sebagai satu kesatuan teks, meskipun teks Base64 tersebut terpotong menjadi beberapa baris di dalam file).*

#### Langkah 2: Mengubah Teks Base64 Menjadi Byte

Sama seperti konsep yang kita bahas sebelumnya, komputer perlu mengubah wujud teks tersebut kembali menjadi biner (byte) agar bisa dibentuk menjadi file yang nyata.

```powershell
$bytes = [Convert]::FromBase64String($teksBase64)
```

#### Langkah 3: Menulis Byte Menjadi File Fisik

Langkah terakhir adalah menulis deretan byte tersebut ke dalam *hard drive* Anda menjadi file baru.

**Penting:** Base64 hanya menyimpan data mentahnya saja, tidak menyimpan nama file atau ekstensinya. Jadi, Anda **harus tahu ekstensi file aslinya** (misalnya apakah itu `.jpg`, `.pdf`, atau `.exe`) agar file tersebut bisa dibuka dengan normal.

```powershell
[IO.File]::WriteAllBytes("C:\lokasi\hasil_gambar.jpg", $bytes)
```

---

#### Cara Singkat (Satu Baris Perintah)

Jika Anda ingin mengeksekusinya secara cepat tanpa memecahnya ke dalam variabel satu per satu, Anda bisa menggabungkan langkah-langkah di atas menjadi satu baris perintah seperti ini:

```powershell
// Encode
[IO.File]::WriteAllText("C:\lokasi\file_rahasia.txt", [Convert]::ToBase64String([IO.File]::ReadAllBytes("C:\lokasi\hasil_gambar.jpg")))

// Decode
[IO.File]::WriteAllBytes("C:\lokasi\hasil_gambar.jpg", [Convert]::FromBase64String([IO.File]::ReadAllText("C:\lokasi\file_rahasia.txt")))
```

---

**Catatan Mengenai Keamanan dan Jejak Aktivitas**
Penting untuk diketahui bahwa melakukan proses *encoding* atau *decoding* melalui PowerShell seperti langkah-langkah di atas **efeknya tidak permanen** dan tidak akan mengubah konfigurasi inti sistem operasi Windows Anda. Proses ini hanya terjadi sementara di dalam memori RAM (kecuali Anda secara eksplisit menyimpan hasilnya ke dalam file baru di *hard drive*).

Namun, aktivitas ini **tetap terekam**. Perintah apa pun yang Anda ketikkan di PowerShell akan tersimpan di dalam riwayat (*command history*) PowerShell pada sesi tersebut. Selain itu, jika sistem Windows Anda mengaktifkan fitur keamanan seperti *Script Block Logging*, aktivitas teks perintah ini akan tercatat dan dapat dilihat oleh Administrator melalui *Windows Event Viewer*.

