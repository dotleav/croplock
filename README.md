# CropLock

Kunci crop gambar di file Word (.docx) secara permanen — langsung di browser, tanpa server.

## Masalah

Saat gambar di-crop lewat fitur Crop bawaan Word, Word tidak memotong file
gambarnya. Word hanya menyimpan gambar aslinya (utuh) lalu menyembunyikan
bagian yang di-crop saat ditampilkan. Kalau file `.docx` itu dibuka oleh
tool lain yang mengambil gambar langsung dari dalamnya, yang terambil
adalah gambar utuh sebelum di-crop.

## Solusi

CropLock membaca `.docx` (yang sebenarnya adalah file ZIP + XML), mencari
semua gambar yang punya info crop (`a:srcRect`), memotong file gambarnya
secara nyata pakai Canvas API, lalu menulis ulang `.docx`-nya. Tampilan
dokumen di Word tidak berubah — hanya file gambar di dalamnya yang sudah
benar-benar terpotong.

## Pakai

Cukup buka `croplock.html` di browser mana saja (bisa lewat `file://`
langsung, atau di-hosting di mana saja — GitHub Pages, Netlify, dll).
Tidak butuh build step, tidak butuh server: satu file HTML mandiri, satu-satunya
dependensi eksternal adalah [JSZip](https://stuk.github.io/jszip/) yang
dimuat dari CDN (cdnjs).

Semua proses (baca, crop, tulis ulang) berjalan di browser pengguna —
file `.docx` tidak pernah dikirim kemana pun.

## Struktur

- `croplock.html` — seluruh app (markup, style, logic) dalam satu file.
