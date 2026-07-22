# Mengubah Informasi Metadata pada File

Anda sangat bisa mengubah informasi (yang sering disebut sebagai **metadata**) pada tab Details di Properties Windows. Namun, tingkat kemudahannya sangat bergantung pada jenis ekstensi file yang ingin Anda ubah.

Berikut adalah beberapa cara yang bisa dilakukan untuk mengubah informasi tersebut, mulai dari cara bawaan hingga menggunakan alat tambahan.

### 1. Cara Langsung Melalui File Explorer (Bawaan Windows)

Windows mengizinkan Anda untuk mengubah metadata secara langsung, tetapi ini terbatas pada format file tertentu yang secara bawaan dikenali oleh Windows (seperti `.jpg`, `.mp4`, `.mp3`, `.docx`, dll.).

**Langkah-langkah:**

1. Klik kanan pada file yang ingin diedit, lalu pilih **Properties**.
2. Masuk ke tab **Details**.
3. Arahkan kursor dan klik pada kolom **Value** (Nilai) di sebelah kanan kategori yang ingin diubah (misalnya *Title*, *Subject*, *Tags*, atau *Authors*).
4. Jika kolom tersebut bisa diedit, akan muncul kotak teks. Ketik informasi baru yang Anda inginkan.
5. Klik **Apply** lalu **OK** untuk menyimpan perubahan.

*Catatan: Jika Anda tidak bisa mengklik dan mengetik pada kolom tersebut, berarti Windows tidak memiliki dukungan bawaan untuk mengedit metadata tipe file tersebut (contohnya file `.txt`, `.png`, atau `.mkv`).*

### 2. Menggunakan Aplikasi Pihak Ketiga (GUI)

Jika file tidak bisa diedit melalui File Explorer, Anda bisa menggunakan perangkat lunak tambahan yang dirancang khusus untuk membaca dan menulis metadata file.

* **File Meta Association Manager:** Aplikasi ini mengaktifkan kemampuan bawaan Windows agar Anda bisa mengedit tab Details pada tipe file yang sebelumnya dikunci atau tidak didukung oleh Windows (seperti `.txt` atau file kode).
* **Mp3tag:** Sangat direkomendasikan jika Anda berurusan dengan file audio (`.mp3`, `.flac`, `.wav`). Aplikasi ini memungkinkan pengeditan massal (bulk edit) dengan antarmuka yang rapi.
* **Geosetter / XnView:** Cocok untuk mengelola secara detail metadata foto/gambar (Exif, IPTC, XMP), termasuk koordinat GPS dan model kamera.

### 3. Menggunakan Command Line (Direkomendasikan untuk Fleksibilitas Tinggi)

Untuk kontrol penuh atas hampir semua ekstensi file, menggunakan antarmuka baris perintah adalah solusi paling tangguh.

* **ExifTool (oleh Phil Harvey):** Ini adalah standar industri untuk membaca, menulis, dan memanipulasi metadata di ribuan format file.
* Cara kerja: Dijalankan melalui Command Prompt atau PowerShell.
* Contoh penggunaan: `exiftool -Title="Judul Baru" -Author="Nama Anda" namafile.ext`

* **PowerShell / Scripting (Python):** Anda juga bisa memanipulasi informasi file secara terprogram jika perlu melakukan otomasi. Di Python, *library* seperti `mutagen` (untuk audio) atau `piexif` (untuk gambar) sering digunakan untuk langsung menyuntikkan data ke tab Details file.

**Saran Tambahan:** Terkadang, informasi pada Properties merupakan refleksi dari isi file itu sendiri (misalnya pada dokumen Office, informasi *Author* diambil dari akun Microsoft Office yang membuat dokumen tersebut). Jika mengubah file dokumen, mengeditnya langsung dari aplikasi asalnya (seperti MS Word melalui menu *File > Info*) seringkali lebih aman agar struktur file tidak rusak.

---

Berbeda dengan informasi seperti *Title* atau *Author*, informasi waktu seperti **Date created** (waktu dibuat), **Date modified** (waktu diubah), dan **Date accessed** (waktu diakses) **tidak bisa diubah secara langsung** melalui tab Details di Properties.

Hal ini karena informasi tersebut dicatat dan dikelola langsung oleh sistem file Windows (seperti NTFS) untuk keperluan pelacakan dan pengindeksan. Namun, Anda tetap bisa memanipulasinya menggunakan beberapa cara berikut:

### 1. Menggunakan PowerShell (Tanpa Instalasi Aplikasi Tambahan)

Ini adalah cara bawaan Windows yang paling ampuh. Anda bisa menggunakan PowerShell untuk mengubah ketiga parameter waktu tersebut secara presisi.

**Langkah-langkah:**

1. Buka pencarian Windows, ketik **PowerShell**, lalu klik kanan dan pilih **Run as Administrator**.
2. Gunakan perintah berikut sesuai dengan informasi waktu yang ingin Anda ubah. Ganti `"C:\lokasi\file.ext"` dengan path asli file Anda, dan ubah format waktunya (Format yang paling aman digunakan adalah `YYYY-MM-DD HH:MM:SS`).

* **Mengubah Date Created (Waktu Dibuat):**
```powershell
$(Get-Item "C:\lokasi\file.ext").CreationTime = "2023-12-01 08:00:00"

```

* **Mengubah Date Modified (Waktu Diubah):**
```powershell
$(Get-Item "C:\lokasi\file.ext").LastWriteTime = "2023-12-05 14:30:00"

```

* **Mengubah Date Accessed (Waktu Diakses):**
```powershell
$(Get-Item "C:\lokasi\file.ext").LastAccessTime = "2023-12-10 09:15:00"

```

### 2. Menggunakan Aplikasi Pihak Ketiga (Lebih Praktis dengan GUI)

Jika Anda tidak terbiasa menggunakan baris perintah atau perlu mengubah banyak file sekaligus, menggunakan aplikasi tambahan adalah pilihan terbaik.

* **Attribute Changer:** Ini adalah aplikasi yang sangat populer dan gratis. Setelah diinstal, aplikasi ini akan menyatu dengan menu klik kanan Windows. Anda cukup klik kanan pada file atau folder, pilih **Change Attributes**, dan Anda bisa dengan bebas mencentang serta memodifikasi *Created*, *Modified*, dan *Accessed date* melalui antarmuka kalender yang mudah dipahami.
* **NewFileTime:** Aplikasi ini sangat ringan, gratis, dan bersifat *portable* (tidak perlu diinstal). Anda cukup *drag-and-drop* (seret dan lepas) file atau folder ke dalam aplikasi, lalu atur waktu yang baru untuk ketiga parameter tersebut secara bersamaan.
* **BulkFileChanger (dari NirSoft):** Sangat direkomendasikan jika Anda perlu menyeleksi ratusan file dan mengubah atribut waktunya secara massal berdasarkan kriteria tertentu.

**Catatan Khusus tentang "Date Accessed":**
Pada versi Windows 10 dan Windows 11 modern, fitur pelacakan "Date accessed" seringkali dinonaktifkan secara otomatis (atau ditunda penulisannya) oleh sistem untuk menghemat performa penyimpanan. Jadi, meskipun Anda mengubahnya, sistem mungkin tidak akan selalu memperbaruinya secara *real-time* saat Anda sekadar membuka file tersebut di kemudian hari.

---

### 1. Apakah Efeknya Permanen?

**Ya, perubahan ini bersifat permanen pada tingkat sistem file (NTFS).**
Perintah PowerShell yang Anda masukkan secara langsung mengubah informasi metadata file di dalam Master File Table (MFT) hard drive Anda.

Namun, Anda perlu mengingat prinsip kerja Windows setelah diubah:

* **Date Modified:** Jika Anda membuka file tersebut, lalu **mengedit dan menyimpannya kembali**, Windows akan menimpa waktu palsu yang sudah Anda atur dengan waktu modifikasi yang baru secara otomatis.
* **Date Created:** Akan tetap permanen meskipun file diedit. Namun, jika Anda menyalin (Copy) file tersebut ke folder atau drive lain, salinan baru tersebut mungkin akan mendapatkan *Date Created* yang baru (waktu saat penyalinan dilakukan).
* **Date Accessed:** Bisa berubah otomatis jika Windows membaca isi file tersebut di masa depan (jika fitur pelacakan akses aktif).

### 2. Apakah Aktivitas Ini Terekam oleh Windows?

Ini bergantung pada beberapa faktor. Secara bawaan (default) pada komputer pribadi, Windows tidak secara proaktif membunyikan "alarm" saat metadata diubah, namun jejaknya tetap ada:

**A. Riwayat PowerShell (PSReadLine)**
Windows secara otomatis menyimpan riwayat perintah PowerShell yang pernah diketikkan. Jika ada orang yang membuka PowerShell di komputer Anda dan menekan tombol panah atas, atau membuka file riwayat teks PowerShell, mereka bisa melihat perintah `$(Get-Item...).CreationTime = ...` yang pernah Anda jalankan.

**B. Windows Event Viewer (Log Sistem)**

* **Komputer Pribadi:** Secara default, Windows **tidak mencatat** aktivitas pengubahan atribut file oleh pengguna biasa ke dalam log (Event Viewer).
* **Komputer Perusahaan / Server:** Jika sistem berada di bawah kebijakan domain (Group Policy) yang mengaktifkan fitur **File System Auditing** atau **PowerShell Script Block Logging**, maka setiap eksekusi perintah PowerShell dan setiap modifikasi atribut file akan tercatat secara detail di Windows Security Logs (seperti Event ID 4663 untuk modifikasi file, atau Event ID 4104 untuk perintah PowerShell).

**C. Analisis Forensik Digital (Timestomping)**
Jika ini berkaitan dengan investigasi hukum atau audit keamanan yang mendalam, ahli forensik bisa mengetahui bahwa file tersebut telah dimanipulasi (praktik ini dalam dunia siber disebut *Timestomping*).

* **Alasannya:** Sistem file NTFS menyimpan **dua** set metadata waktu (satu di atribut `$STANDARD_INFORMATION` dan satu lagi di atribut `$FILE_NAME`). Mengubah waktu melalui PowerShell atau aplikasi GUI standar umumnya hanya mengubah atribut `$STANDARD_INFORMATION`. Ahli forensik akan membandingkan kedua atribut ini; jika waktunya tidak sinkron, mereka tahu bahwa tanggal file tersebut telah dipalsukan.
