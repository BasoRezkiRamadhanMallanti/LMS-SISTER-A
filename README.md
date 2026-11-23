# Panduan Kolaborasi Proyek di GitHub

Gunakan satu repository untuk seluruh proyek. Semua kelompok mulai dari kode dasar yang sama di `main`, mengerjakan modul di branch masing-masing, lalu mengajukan Pull Request (PR) agar perubahan bisa diperiksa dan digabungkan.

## Pembagian branch

| Branch | Penanggung jawab | Isi |
| --- | --- | --- |
| `main` | Koordinator | Kode dasar dan hasil pekerjaan yang sudah digabung |
| `kelompok-1/authentication` | Kelompok 1 | Authentication |
| `kelompok-2/notification` | Kelompok 2 | Notification |
| `kelompok-3/course` | Kelompok 3 | Course |
| `kelompok-4/submission-file` | Kelompok 4 | Submission File |
| `kelompok-5/gateway` | Kelompok 5 | Gateway |
| `kelompok-6/assignment` | Kelompok 6 | Assignment |
| `kelompok-7/monitoring` | Kelompok 7 | Monitoring |

Setiap anggota menggunakan branch kelompoknya sesuai tabel. Di perintah clone, ganti `PEMILIK-REPO` dengan username pemilik atau nama organisasi GitHub dan `projek-kelompok` dengan nama repo yang dipakai.

## 1. Koordinator menyiapkan repository

1. Buka [New repository](https://github.com/new), pilih pemilik repo, dan isi nama proyek. Pilih **Private** jika aksesnya hanya untuk anggota yang diundang.
2. Jika proyek mulai dari nol, aktifkan **Add README** untuk membuat commit pertama. Tambahkan struktur dasar proyek ke `main` sebelum membagikan branch. Jika kode dasar sudah ada di laptop, buat repo GitHub kosong lalu [unggah kode dasar](https://docs.github.com/en/migrations/importing-source-code/using-the-command-line-to-import-source-code/adding-locally-hosted-code-to-github) ke branch `main`. Jika kode dasar sudah disalin ke GitHub, pakai repo hasil salinan yang telah disepakati bersama.
3. Untuk repo akun pribadi, buka **Settings → Collaborators → Add people**. Undang anggota dengan username GitHub mereka. Setiap anggota masuk dengan akun sendiri dan menerima undangan. [Dokumentasi undangan kolaborator](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/repository-access-and-collaboration/inviting-collaborators-to-a-personal-repository)
4. Setelah kode dasar tersedia di `main`, buat branch tiap kelompok dari `main`. Di tab **Code**, pilih `main`, buka pemilih branch, ketik nama branch kelompok, lalu pilih **Create branch**. Kembali ke `main` sebelum membuat branch kelompok berikutnya.
5. Sepakati penanggung jawab file yang dipakai bersama, seperti file rute, konfigurasi, atau migrasi basis data. Koordinasikan setiap perubahan pada file itu dengan kelompok terkait.

Jika kamu menggunakan README ini untuk repo yang sudah ada, unggah ke folder paling atas repo. Bila sudah ada `README.md`, gabungkan panduan ini dengan petunjuk instalasi proyek yang sudah tersedia.

## 2. Anggota mengambil kode ke laptop

Pastikan Git terpasang dan undangan repo sudah diterima. Buka PowerShell di folder tempat proyek akan disimpan. Contoh berikut untuk Kelompok 1 (Authentication) dan cukup dilakukan sekali per laptop. Kelompok 2–7 mengganti `kelompok-1/authentication` dengan branch masing-masing pada perintah `switch`, `pull`, dan `push`, serta saat memilih branch **compare** di Pull Request.

```powershell
git clone (https://github.com/BasoRezkiRamadhanMallanti/LMS-SISTER-A)
cd LMS-SISTER-A
git switch --track origin/kelompok-1/authentication
git branch --show-current
```

Perintah terakhir seharusnya menampilkan `kelompok-1/authentication`. Jika repo sudah pernah di-clone, buka foldernya dan jalankan `git fetch origin`. Jika branch kelompok sudah ada di laptop, gunakan `git switch kelompok-1/authentication`. Jika baru ada di GitHub, gunakan perintah `git switch --track` di atas.

## 3. Anggota mengedit dan mengunggah kode

1. Masuk ke branch kelompok. Sebelum mulai, ambil commit terbaru teman sekelompok dengan `git pull --ff-only` saat tidak ada perubahan lokal yang belum disimpan.

   ```powershell
   git switch kelompok-1/authentication
   git pull --ff-only
   ```

2. Buka folder proyek di VS Code lewat **File → Open Folder**. Pilih folder `projek-kelompok`, edit file modul yang ditugaskan, simpan, lalu jalankan dan uji perubahan sesuai petunjuk proyek. Jika punya kode dari folder lain, salin bagian modul yang diperlukan ke folder hasil clone. Periksa perbedaannya sebelum commit.
3. Periksa perubahan, pilih file yang ingin dimasukkan ke commit, lalu unggah ke branch kelompok. Pada perintah `git add`, ganti path contoh dengan file yang benar. Ulangi `git add` untuk setiap file yang ingin disertakan. Jaga agar `.env` lokal, token, kata sandi, dan file keluaran lokal tetap di luar commit.

   ```powershell
   git status
   git diff
   git add "path/ke/file-yang-diubah"
   git diff --cached
   git commit -m "Tambahkan validasi login pada modul Authentication"
   git push origin kelompok-1/authentication
   ```

4. Buka GitHub, pilih branch kelompok, lalu pastikan commit dan file yang diubah sudah muncul.

### Jika push ditolak karena branch kelompok sudah berubah

Jika teman sekelompok push lebih dulu dan Git menolak push kamu, gabungkan commit mereka ke branch kelompokmu dengan `git pull --no-rebase origin kelompok-1/authentication` setelah perubahan lokal di-commit. Jika muncul konflik, buka file yang ditandai, gabungkan perubahan yang diperlukan, lalu jalankan `git add` untuk file yang sudah diperbaiki dan `git commit` untuk menyelesaikan merge. Uji kembali sebelum menjalankan `git push origin kelompok-1/authentication`.

## 4. Kelompok mengajukan Pull Request

1. Buka repo bersama di GitHub lalu pilih **Pull requests → New pull request**.
2. Pilih **base: `main`** sebagai tujuan dan **compare: `kelompok-1/authentication`** sebagai sumber perubahan. Periksa **Files changed**.
3. Klik **Create pull request**. Isi judul, ringkasan perubahan, dan cara menguji modul.
4. Jika reviewer meminta revisi, edit dan push kembali ke branch kelompok. PR yang masih terbuka akan menampilkan commit baru dari branch itu. [Dokumentasi Pull Request GitHub](https://docs.github.com/en/pull-requests/how-tos/create-pull-requests/creating-a-pull-request)

## 5. Koordinator menggabungkan dan menguji proyek

1. Cek perubahan di setiap PR dan uji modulnya. Jika ada ketergantungan, gabungkan modul yang dibutuhkan lebih dulu.
2. Jika GitHub menampilkan konflik dengan `main`, minta kelompok terkait mengambil perubahan `main` dari branch mereka dengan `git fetch origin` lalu `git merge origin/main`. Selesaikan konflik, uji ulang, lalu push ke branch kelompok agar PR diperbarui.
3. Setelah PR lolos review, gunakan **Merge pull request** dengan opsi **Create a merge commit** jika branch kelompok akan dipakai lagi. Pertahankan branch kelompok selama masih ada pekerjaan.
4. Setelah semua PR masuk, cek versi gabungan dari `main`.

   ```powershell
   git switch main
   git pull --ff-only origin main
   ```

5. Jalankan proyek dari `main` dan uji alur antarmodul. Jika perlu perbaikan, lakukan di branch kelompok terkait dan ajukan PR baru.

**Kesepakatan tim.** Push perubahan ke branch kelompok. Masukkan perubahan ke `main` melalui PR agar semua kelompok bisa melihat dan memeriksa kode sebelum digabung.
