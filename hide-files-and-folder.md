# Cara Menyembunyikan File

### 1. Mengubah Atribut Menjadi File Sistem (`System Hidden`)

Cara ini memanfaatkan Command Prompt (CMD) untuk mengubah atribut folder menjadi file sistem super rahasia (*System File*). Folder yang disembunyikan dengan cara ini **tidak akan muncul** meskipun opsi "Hidden items" di File Explorer sudah dicentang.

**Cara Menyembunyikan:**

1. Buka **Command Prompt** (CMD).
2. Ketik perintah berikut dan tekan Enter:
```cmd
attrib +s +h "D:\SecretFolder"
```


*(Ganti `D:\SecretFolder` dengan jalur folder yang ingin kamu sembunyikan).*

**Cara Mengembalikannya:**
Jika kamu ingin melihatnya kembali, jalankan perintah sebaliknya di CMD:

```cmd
attrib -s -h "D:\SecretFolder"
```

> **Catatan:** Folder ini benar-benar tidak akan terlihat kecuali seseorang mematikan opsi *"Hide protected operating system files"* di pengaturan *Folder Options* Windows, sebuah opsi yang jarang diotak-atik oleh pengguna biasa. 
---

### 2. Menyembunyikan Drive Lewat Disk Management

Jika kamu punya satu *partition* atau *drive* khusus (misalnya Drive `E:`) yang berisi data-data sensitif, kamu bisa menyembunyikan seluruh drive tersebut.

1. Klik kanan pada tombol **Start** lalu pilih **Disk Management**.
2. Cari drive yang ingin disembunyikan (misalnya Drive E:).
3. Klik kanan pada drive tersebut, lalu pilih **Change Drive Letter and Paths...**.
4. Klik huruf drive-nya (E:), lalu klik tombol **Remove** dan pilih **Yes**.

Sekarang drive tersebut akan hilang dari *This PC*. Data kamu tetap aman dan tidak terhapus.

* **Untuk mengembalikannya:** Masuk lagi ke Disk Management, klik kanan pada drive tadi, pilih *Change Drive Letter and Paths...*, klik **Add**, lalu pilih kembali huruf drive-nya.
---

### 3. Trik "God Mode" (Menyamarkan Folder Menjadi Aplikasi Sistem)

Kamu bisa mengelabui orang lain dengan mengubah folder biasa menjadi pintasan sistem yang tidak bisa dibuka secara normal, misalnya mengubah folder menjadi "Recycle Bin" atau "Control Panel".

1. Buat folder baru atau gunakan folder yang sudah ada.
2. Ubah nama (*Rename*) folder tersebut dengan menambahkan kode khusus di belakangnya.

Contoh, ubah nama folder menjadi:

* **Menjadi Recycle Bin:** `NamaFolder.{645FF040-5081-101B-9F08-00AA002F954E}`
* **Menjadi Control Panel:** `NamaFolder.{21EC2020-3AEA-1069-A2DD-08002B30309D}`

Setelah di-rename, ikon folder akan berubah menjadi Recycle Bin atau Control Panel. Jika orang lain mengkliknya, mereka akan dibawa ke Recycle Bin asli atau Control Panel, bukan ke file kamu.

* **Untuk mengembalikannya:** Kamu harus membuka CMD, lalu *rename* kembali folder tersebut ke nama biasa (menghapus kode unik di belakangnya).
```cmd
ren "OldFolderName" "NewFolderName"
```