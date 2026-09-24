# Capstone Software Engineer — Pintarly

Halo! Kalau kamu membaca ini, kamu sedang melamar posisi Software Engineer di Pintarly.

Pintarly adalah platform belajar UTBK/SNBT. Penggunanya anak SMA, hampir semuanya dari HP, banyak yang koneksinya pas-pasan. Tugas ini adalah membangun **satu fitur baru untuk Pintarly**, dari nol sampai bisa dibuka orang lain di internet.

Tugasnya ada di **[BRIEF.md](./BRIEF.md)**. Baca file ini dulu sampai habis, baru buka brief-nya.

---

## Yang sebenarnya kami cari

Kami mencari engineer yang **bisa memanfaatkan AI habis-habisan** untuk membangun sesuatu — dan hasil akhirnya tetap enak dilihat.

Jadi biar jelas sejak awal:

**Pakai AI sebanyak mungkin.** Claude Code, Cursor, Codex, Copilot, agent, MCP, apa pun. Kami tidak sedang menguji apakah kamu bisa mengetik `useState` dari ingatan. Kami sedang mencari orang yang bisa mengeluarkan hasil besar dalam waktu pendek dengan tool ini, dan tahu mana hasil yang layak dikirim dan mana yang tidak.

Yang membedakan kandidat di sini bukan siapa yang menulis kode paling banyak, tapi:

- Seberapa jauh kamu sampai dalam 72 jam.
- Apakah UI-nya terlihat seperti produk Pintarly, atau seperti output AI generik.
- Apa yang terjadi waktu data yang kami kasih ternyata berantakan.
- Apakah fiturnya tetap hidup waktu hal-hal di luar kendali kamu gagal.

---

## Aturan main

- **Waktu: 72 jam** sejak kamu menerima link ini.
- **Kerjakan sendiri.** Boleh pakai AI sebebasnya, tidak boleh dikerjakan orang lain.
- **Satu kali pengumpulan.** Tidak ada babak kedua, tidak ada revisi setelah dikumpulkan.
- **Satu fitur saja**, sesuai brief. Menambah fitur di luar brief tidak menambah nilai.

## Stack

- **Next.js (App Router) + TypeScript + Tailwind CSS v4.** Ini wajib, karena design system kami ditulis untuk itu.
- **Penyimpanan data bebas**, asal datanya tidak hilang waktu halaman di-refresh. Supabase free tier paling cepat (itu yang kami pakai), tapi terserah kamu.
- **Deploy ke internet.** Vercel free tier sudah cukup. Kami harus bisa membukanya dari HP.
- Tidak perlu login. Anggap ada satu siswa, datanya sudah ada di `data/seed.json`.

## Aturan 5 menit

Reviewer kami akan membuka URL kamu dalam keadaan dingin — tanpa penjelasan, tanpa setup, dari HP — dan harus bisa melihat **seluruh fitur dalam 5 menit**.

Artinya: tidak boleh ada yang perlu ditunggu berhari-hari, tidak ada langkah setup manual, tidak ada "coba isi data dulu 20 kali baru kelihatan". Semua kondisi penting (termasuk kondisi kosong dan kondisi error) harus bisa dicapai reviewer dengan sedikit klik. Kalau ada state yang sulit dicapai, sediakan jalan pintas yang jelas.

Fitur yang tidak bisa ditunjukkan dalam 5 menit dianggap tidak ada.

## Fitur AI & API key kamu sendiri

Brief ini mewajibkan **satu fitur generatif** (lihat BRIEF.md). Ini bagian penting: produk kami hidup dari fitur AI, jadi kami ingin lihat kamu membangunnya, bukan cuma memakainya.

- **Pakai API key kamu sendiri.** Google AI Studio (Gemini) memberi key gratis tanpa kartu kredit: https://aistudio.google.com/apikey — ini jalur termurah dan model yang sama dengan yang kami pakai di produksi. Provider lain boleh, asal gratis atau kamu tanggung sendiri.
- **Key hanya boleh hidup di server.** Jangan pernah ada di bundle browser. Kalau kami menemukan `NEXT_PUBLIC_..._API_KEY` atau panggilan ke API model langsung dari komponen client, penilaiannya selesai di situ.
- **Fiturnya harus tetap sopan waktu key-nya mati.** Kuota habis, rate limit, model timeout — ini akan terjadi, mungkin tepat waktu kami sedang menilai. Aplikasi harus turun ke sesuatu yang jujur (hasil cadangan, pesan yang jelas, opsi coba lagi), bukan layar putih atau loading selamanya.
- Tulis nama variabel env yang kamu pakai di `.env.example`. **Jangan commit key kamu.**

## Data

Semua data ada di `data/seed.json`, penjelasannya di [DATA.md](./DATA.md).

**`data/seed.json` adalah spesifikasi.** Apa pun yang ada di dalamnya, aplikasi kamu harus tahan menghadapinya. Kami sengaja tidak membersihkannya — isinya mirip data produksi kami yang asli, lengkap dengan yang aneh-aneh. Kode yang cuma jalan di jalur bahagia akan kelihatan langsung.

Boleh mengubah bentuk data untuk kebutuhan internal kamu, tapi jangan menghapus baris yang merepotkan. Yang merepotkan itu justru bagian dari soal.

## Design system

Ada di [DESIGN_SYSTEM.md](./DESIGN_SYSTEM.md). Ikuti.

Saran praktis: jangan cuma baca sendiri lalu berharap AI menebak. Masukkan file itu ke konteks tool kamu (CLAUDE.md, .cursorrules, AGENTS.md, apa pun bentuknya) supaya setiap kode yang dihasilkan sudah patuh sejak awal. Ini salah satu hal yang paling membedakan hasil akhir.

## Yang dikumpulkan

Kirim tiga hal ke **dev@pintarly.id** sebelum batas waktu:

1. **Link repo** kamu (GitHub, publik atau private + undang kami).
2. **URL aplikasi** yang sudah ter-deploy.
3. **Video 3 menit** (Loom/Google Drive) — tunjukkan fiturnya jalan, lalu ceritakan singkat bagaimana kamu memakai AI untuk membangunnya dan keputusan apa yang kamu ambil sendiri.

Videonya tidak usah diedit, tidak usah rapi. Kami cuma ingin melihat aplikasinya hidup dan mendengar cara kamu berpikir.

## Yang TIDAK kami nilai

Supaya kamu tidak membuang waktu:

- Coverage test. Tulis test kalau itu membantu kamu bergerak cepat, jangan tulis demi angka.
- Dokumen arsitektur, diagram, ADR.
- Jumlah atau kerapian pesan commit.
- Fitur di luar brief.
- Apakah kamu menulis kodenya sendiri atau dihasilkan AI. Sungguh.

## Kalau ada yang tidak jelas

Sebagian hal di brief memang sengaja dibiarkan terbuka — itu ruang kamu untuk mengambil keputusan. Ambil keputusan yang paling masuk akal, lalu lanjut. Tidak perlu izin.

Kalau ada yang benar-benar buntu (link rusak, file hilang), email **dev@pintarly.id**.

Selamat mengerjakan. Kami tunggu.
