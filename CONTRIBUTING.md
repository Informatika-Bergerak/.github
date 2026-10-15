# Panduan Kontribusi ConCordia

## 1. Aturan Dasar

1. Satu pekerjaan harus memiliki satu Issue, satu branch, dan satu Pull Request.
2. Jangan melakukan push langsung ke branch `main`.
3. Setiap Pull Request harus ditinjau minimal satu anggota lain.
4. Perubahan harus memenuhi pemeriksaan CI yang diwajibkan sebelum merge.
5. Jangan mengunggah password, API key, token, atau file `.env` ke repository.

## 2. Membuat Branch

Pastikan branch `main` lokal sudah terbaru:

```bash
git switch main
git pull --ff-only origin main
```

Buat branch baru sesuai jenis pekerjaan:

```bash
git switch -c feat/deskripsi-singkat
```

Gunakan awalan branch berikut:
- `feat/` untuk fitur baru.
- `fix/` untuk perbaikan bug.
- `docs/` untuk dokumentasi.
- `chore/` untuk pekerjaan pemeliharaan atau konfigurasi.

Contoh: `feat/forum-post`, `fix/report-status`, atau `docs/update-readme`.

## 3. Mengubah dan Memeriksa File

Setelah selesai mengubah kode, periksa file yang berubah:

```bash
git status
git diff
```

Tambahkan hanya file yang memang ingin di-commit:

```bash
git add src/modules/forum/file-yang-diubah.ts
git diff --cached
```

Periksa kembali hasil staging sebelum membuat commit. Jangan memasukkan file rahasia atau perubahan yang tidak terkait dengan pekerjaan.

## 4. Membuat Commit

Gunakan format [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/):

```text
<tipe>: <deskripsi perubahan>
```

Contoh:

```bash
git commit -m "feat: tambah fitur posting forum"
git commit -m "fix: perbaiki validasi laporan"
git commit -m "docs: perbarui panduan instalasi"
```

Satu branch dapat memiliki beberapa commit selama seluruh commit masih berkaitan dengan Issue yang sama.

## 5. Sinkronisasi dan Push

Sebelum push pertama, ambil informasi terbaru dari repository:

```bash
git fetch origin
git rebase origin/main
```

Jika terjadi konflik, periksa dengan `git status`, selesaikan konflik sesuai kebutuhan, lalu lanjutkan rebase. Jika tidak yakin, hentikan proses dan minta bantuan sebelum melanjutkan.

Setelah rebase berhasil, kirim branch ke GitHub:

```bash
git push -u origin feat/deskripsi-singkat
```

Gunakan nama branch yang benar-benar dibuat. Jangan menjalankan rebase pada branch yang sudah dipublikasikan tanpa memahami dampaknya terhadap riwayat remote.

## 6. Membuat Pull Request

1. Buka repository ConCordia di GitHub.
2. Pilih **Compare & pull request** untuk branch yang baru di-push.
3. Isi judul dan deskripsi perubahan.
4. Hubungkan Pull Request dengan Issue menggunakan `Closes #nomor`.
5. Jelaskan cara menguji perubahan dan sertakan screenshot jika relevan.
6. Pastikan Pull Request sesuai dengan template repository.

## 7. Menangani Review

Jika reviewer meminta perubahan, lakukan perbaikan di branch yang sama:

```bash
git add src/modules/forum/file-yang-diubah.ts
git commit -m "fix: perbaiki perubahan hasil review"
git push
```

Pull Request yang sama akan diperbarui secara otomatis. Tidak perlu membuat Pull Request baru untuk pekerjaan yang sama.

## 8. Merge dan Pembersihan

Pull Request dapat di-merge setelah:
- Mendapat persetujuan reviewer yang diwajibkan.
- Semua pemeriksaan CI wajib berhasil.
- Percakapan review yang diwajibkan telah diselesaikan.

Gunakan **Squash and merge** sesuai kebijakan repository ConCordia.

Setelah merge selesai, bersihkan branch lokal:

```bash
git switch main
git pull --ff-only origin main
git branch -d feat/deskripsi-singkat
```

Branch remote dapat dihapus melalui tombol **Delete branch** pada halaman Pull Request yang sudah di-merge.

## 9. Meminta Bantuan

Jika terjadi konflik rebase, kegagalan CI, masalah autentikasi Git, atau kondisi yang tidak dipahami, hentikan langkah yang berisiko dan hubungi PM atau Backend/Tech Lead sebelum melanjutkan.
