# Panduan Kontribusi ConCordia

Panduan ini menjelaskan alur kerja Git dan GitHub di ConCordia, dari mengambil pekerjaan sampai kodenya masuk ke `main`. Setiap langkah disertai penjelasan apa yang terjadi dan kenapa dilakukan, jadi cocok untuk pemula.

## Aturan Utama

1. **Satu pekerjaan = satu branch = satu Pull Request (PR).** Ini membuat riwayat perubahan mudah dilacak dan mudah di-review.
2. **Jangan push langsung ke `main`.** Branch `main` adalah versi yang dianggap stabil, jadi semua perubahan harus lewat PR.
3. **PR harus di-review minimal 1 anggota lain** dan **semua pemeriksaan CI harus lolos (hijau)** sebelum di-merge.
4. **Jangan pernah commit** password, API key, token, atau file `.env`. Sekali masuk ke riwayat Git, data rahasia sulit ditarik kembali.

## Istilah Penting

| Istilah | Artinya |
| --- | --- |
| **Branch** | Cabang kerja terpisah dari `main`, tempat kamu bekerja tanpa mengganggu kode utama. |
| **Commit** | "Titik simpan" berisi sekumpulan perubahan beserta pesan penjelasnya. |
| **Push** | Mengirim commit dari komputermu ke GitHub. |
| **Pull Request (PR)** | Permintaan agar branch-mu digabung ke `main`, sekaligus tempat review dilakukan. |
| **Rebase** | Memindahkan commit-mu supaya berada di atas versi `main` yang paling baru. |
| **CI** | Pemeriksaan otomatis di GitHub (misalnya test dan lint) yang berjalan setiap PR dibuat atau diperbarui. |

## Alur Kerja Langkah demi Langkah

### 1. Pastikan `main` lokal kamu terbaru

```bash
git switch main
git pull
```

Kamu berpindah ke `main` lalu mengunduh perubahan terbaru dari GitHub. Selalu mulai dari kondisi ini supaya branch barumu tidak berdasar pada kode yang sudah usang.

### 2. Buat branch baru dari `main`

```bash
git switch -c feat/halaman-profil
```

`-c` artinya "buat branch baru lalu langsung pindah ke sana". Beri nama sesuai jenis pekerjaan:

| Awalan | Untuk | Contoh |
| --- | --- | --- |
| `feat/` | Fitur baru | `feat/forum-post` |
| `fix/` | Perbaikan bug | `fix/report-status` |
| `docs/` | Dokumentasi | `docs/update-readme` |
| `chore/` | Pemeliharaan atau konfigurasi | `chore/update-deps` |

### 3. Edit file, lalu cek apa yang berubah

```bash
git status
git diff
```

- `git status` menampilkan file mana yang berubah. File berwarna merah belum disiapkan untuk commit, file berwarna hijau sudah.
- `git diff` menampilkan isi perubahannya baris per baris. Baris berawalan `+` ditambahkan, berawalan `-` dihapus.

Biasakan mengecek dua perintah ini sebelum commit untuk menangkap perubahan yang tidak disengaja.

### 4. Simpan progres dengan commit

```bash
git add .
git commit -m "feat: tambah komponen form profil"

# ...lanjut kerja bagian lain...
git add .
git commit -m "feat: hubungkan form profil ke API"
```

- `git add .` memilih semua perubahan untuk dimasukkan ke commit berikutnya (disebut *staging*).
- `git commit -m "..."` menyimpan perubahan tersebut sebagai satu titik simpan.
- Commit kecil dan sering lebih mudah ditelusuri daripada satu commit raksasa.

**Format pesan commit** memakai [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/): `<tipe>: <deskripsi>`. Tipe yang dipakai sama dengan awalan branch (`feat`, `fix`, `docs`, `chore`).

```text
feat: tambah fitur posting forum
fix: perbaiki validasi laporan
docs: perbarui panduan instalasi
```

> **Hati-hati dengan `git add .`**, karena perintah ini ikut memasukkan semua file yang berubah, termasuk `.env` atau file yang tidak berkaitan dengan pekerjaanmu. Cek dulu dengan `git status`. Kalau ragu, tambahkan file satu per satu:
> ```bash
> git add src/modules/forum/nama-file.ts
> git diff --cached   # lihat isi yang akan di-commit
> ```

### 5. Sinkronkan dengan `main` sebelum push

Kalau kerjamu cukup lama, `main` mungkin sudah berubah karena pekerjaan orang lain. Sinkronkan dulu supaya konflik ketahuan sekarang, bukan saat PR sudah dibuka.

```bash
git fetch origin
git rebase origin/main
```

- `git fetch origin` mengunduh informasi terbaru dari GitHub tanpa mengubah file-mu.
- `git rebase origin/main` memindahkan commit-mu ke atas `main` yang paling baru.

**Kalau muncul konflik**, Git akan berhenti dan memberi tahu file mana yang bermasalah:

1. Jalankan `git status` untuk melihat file yang konflik.
2. Buka file tersebut. Bagian yang konflik ditandai `<<<<<<<`, `=======`, dan `>>>>>>>`. Pilih isi yang benar, lalu hapus ketiga penanda itu.
3. Jalankan `git add nama-file`, lalu `git rebase --continue`.
4. Kalau bingung, batalkan dengan `git rebase --abort`. Branch-mu kembali seperti sebelum rebase, dan kamu bisa minta bantuan.

> **Jangan rebase branch yang sudah pernah di-push** tanpa paham dampaknya. Rebase mengubah riwayat commit, sehingga push berikutnya akan ditolak oleh GitHub kecuali dipaksa (force push). Kalau sudah terlanjur push dan butuh sinkronisasi, tanyakan ke Tech Lead dulu.

### 6. Kirim branch ke GitHub

```bash
git push -u origin feat/halaman-profil
```

`-u` menghubungkan branch lokal dengan branch di GitHub. Setelah ini, cukup ketik `git push` untuk push berikutnya di branch yang sama. Gunakan nama branch yang benar-benar kamu buat.

### 7. Buat Pull Request (lewat browser)

1. Buka repository ConCordia di GitHub.
2. Klik **Compare & pull request** pada branch yang baru di-push.
3. Isi judul dan deskripsi perubahan, mengikuti template PR yang tersedia.
4. Jelaskan cara mengujinya, dan sertakan screenshot kalau perubahannya terlihat di tampilan.
5. Klik **Create pull request**.

### 8. Ada revisi dari review?

Perbaiki di branch yang sama, lalu commit dan push lagi:

```bash
git add .
git commit -m "fix: perbaiki validasi sesuai review"
git push
```

PR yang sama akan terupdate otomatis dan CI berjalan ulang. **Jangan buat PR baru** untuk pekerjaan yang sama.

### 9. Merge (lewat browser)

PR siap di-merge kalau:

- reviewer yang diwajibkan sudah menyetujui (approve),
- semua pemeriksaan CI hijau, dan
- semua percakapan review sudah diselesaikan.

Klik **Squash and merge**. Semua commit di branch-mu akan digabung menjadi satu commit rapi di `main`, sesuai kebijakan repository ConCordia. Pastikan judul commit hasil squash tetap mengikuti format Conventional Commits.

### 10. Bersih-bersih setelah merge

```bash
git switch main
git pull
git branch -d feat/halaman-profil                    # hapus branch lokal
git push origin --delete feat/halaman-profil         # hapus branch remote
```

Branch remote juga bisa dihapus lewat tombol **Delete branch** di halaman PR yang sudah di-merge (biasanya GitHub menawarkannya otomatis).

## Masalah yang Sering Terjadi

| Masalah | Yang perlu dilakukan |
| --- | --- |
| **CI gagal (merah)** | Klik **Details** pada check yang gagal di halaman PR, baca lognya, perbaiki, lalu commit dan push lagi. |
| **Push ditolak** | Baca pesan errornya dan jalankan `git status`. Jangan paksa dengan `--force`. Tanyakan dulu kalau belum paham sebabnya. |
| **Terlanjur commit di `main`** | Jangan push. Hubungi Tech Lead untuk memindahkan commit ke branch yang benar. |
| **Terlanjur push file rahasia** | Segera lapor ke PM atau Tech Lead. Menghapus file saja tidak cukup, karena datanya masih ada di riwayat Git dan kuncinya harus diganti. |
| **Konflik rebase** | Ikuti langkah di bagian 5, atau `git rebase --abort` lalu minta bantuan. |

## Meminta Bantuan

Kalau terjadi konflik rebase, CI gagal terus, masalah login Git, atau kondisi yang tidak kamu pahami, **berhenti dulu dan jangan paksa lanjut**. Hubungi **PM** atau **Backend/Tech Lead** sebelum melanjutkan.
