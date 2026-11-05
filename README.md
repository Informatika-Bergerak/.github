# .github — Informatika Bergerak

Repository ini menyimpan **file komunitas default** untuk seluruh organisasi **Informatika-Bergerak** di GitHub, serta profil organisasi yang tampil di halaman utama organisasi.

Repository ini bukan aplikasi yang dijalankan. Isinya hanya dokumen dan template yang dipakai bersama oleh semua repository di organisasi.

## Cara Kerjanya

GitHub memperlakukan repository bernama `.github` (harus **publik**) secara khusus. Jika sebuah repository di organisasi **tidak punya** file tertentu sendiri (misalnya `CONTRIBUTING.md`), GitHub otomatis memakai versi dari repository ini.

Artinya, kita cukup memelihara satu panduan dan satu template di sini, dan semua repository lain ikut memakainya. Kalau sebuah repository membutuhkan aturan khusus, buat file dengan nama yang sama di repository tersebut dan file itu yang akan dipakai.

## Isi Repository

| Lokasi | Fungsi |
| --- | --- |
| [`profile/`](./profile) | Isi `README.md` di dalamnya tampil sebagai profil di halaman organisasi. |
| [`ISSUE_TEMPLATE/`](./ISSUE_TEMPLATE) | Template default saat membuat Issue baru. |
| [`PULL_REQUEST_TEMPLATE.md`](./PULL_REQUEST_TEMPLATE.md) | Template default deskripsi Pull Request. |
| [`CONTRIBUTING.md`](./CONTRIBUTING.md) | Panduan alur kontribusi: branch, commit, Pull Request, dan merge. |
| `README.md` | Dokumen yang sedang kamu baca. |

> **Catatan:** Jika sebuah repository punya folder `.github/ISSUE_TEMPLATE` sendiri, template default dari repository ini tidak dipakai sama sekali di repository tersebut. Template tidak digabung, melainkan digantikan seluruhnya.

## Berkontribusi

Perubahan di repository ini memengaruhi **semua repository** di organisasi, jadi ikuti alur yang sama seperti kontribusi lainnya:

1. Buat Issue, lalu buat branch baru dari `main`.
2. Lakukan perubahan dan commit dengan format [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/), misalnya `docs: perbarui panduan kontribusi`.
3. Push branch dan buka Pull Request.
4. Tunggu review dan persetujuan sebelum di-merge.

Langkah lengkapnya ada di [CONTRIBUTING.md](./CONTRIBUTING.md). Jangan push langsung ke `main`.

## Menguji Perubahan

Template dan panduan di sini baru terlihat efeknya setelah masuk ke `main`. Agar tidak salah, sebelum membuka Pull Request:

- Pastikan tampilan Markdown rapi lewat tab **Preview** di GitHub atau pratinjau di editor.
- Pastikan semua tautan relatif (seperti `./CONTRIBUTING.md`) tidak rusak.
- Untuk template Issue, periksa bahwa file di dalam `ISSUE_TEMPLATE/` valid, terutama bagian `config.yml` atau front matter di bagian atas file jika ada.

## Bantuan

Jika ada yang kurang jelas atau kamu ragu apakah sebuah perubahan layak dimasukkan ke sini, hubungi **PM** atau **Backend/Tech Lead** sebelum membuka Pull Request.
