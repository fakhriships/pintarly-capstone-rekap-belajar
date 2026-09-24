# Brief — Rekap Belajar

## Masalahnya

Siswa belajar berminggu-minggu di Pintarly dan hampir tidak pernah melihat hasil kerjanya sendiri secara utuh. Yang mereka ingat cuma sesi terakhir: kemarin capek, kemarin banyak yang salah. Angka-angka yang membuktikan mereka sebenarnya maju terkubur di dalam riwayat yang tidak pernah dibuka.

Tugas kamu: ubah satu blok riwayat belajar yang sudah selesai menjadi **rekap berbentuk cerita** — layar penuh, satu kartu satu fakta, cepat, enak dilihat, dan berakhir dengan sesuatu yang layak dikirim siswa ke grup temannya.

Ini brief yang paling berat di sisi visual. Kalau kamu orang yang senang membuat sesuatu terasa hidup, ini tempatnya.

## Batas cakupan

- **Mulai dari:** kartu pembuka rekap.
- **Selesai di:** gambar yang bisa dibagikan.

Datanya **sudah selesai dan tidak bertambah**. Tidak ada pelacakan berjalan, tidak ada jadwal, tidak ada "rekap minggu depan". Satu blok riwayat, satu rekap.

---

## Alur wajib

### 1. Hitung statistiknya
Dari riwayat di `data/seed.json`, hitung angka-angka yang layak diceritakan. Minimal: total waktu belajar, jumlah soal yang dikerjakan, akurasi, subtes terkuat, dan subtes yang paling perlu dibenahi.

Angka ini dihitung oleh **kode kamu**, bukan oleh model. Ini penting, dan akan jelas kenapa sebentar lagi.

### 2. Cerita berkartu
Minimal **5 kartu layar penuh**, dengan:

- maju dengan tap di sisi kanan, mundur di sisi kiri
- swipe di HP
- indikator progres di atas (seperti Instagram Story)
- lanjut otomatis setelah beberapa detik, dan bisa ditahan untuk berhenti
- bisa dibuka ulang dari awal

Isi tiap kartu kamu yang tentukan. Sebagai gambaran: total waktu, jumlah soal dan akurasi, subtes terkuat, subtes yang perlu dibenahi, kebiasaan waktu belajar, kartu penutup. Boleh beda, asal tiap kartu punya satu pesan yang jelas.

### 3. Narasi AI
Tiap kartu diberi narasi pendek yang ditulis model — kalimat yang membuat angka terasa personal, bukan sekadar label.

Aturannya satu, dan tidak bisa ditawar: **narasi tidak boleh menyebut angka atau fakta yang tidak dihasilkan oleh perhitungan kamu.** Model akan dengan senang hati menulis "kamu naik 40 persen!" padahal datanya 12 persen, atau memuji subtes yang justru paling lemah. Yang muncul di layar harus sudah lolos pemeriksaan.

### 4. Bagikan
Minimal satu kartu bisa diekspor jadi gambar yang bisa disimpan atau dikirim. Ukuran story (1080×1920) adalah pilihan yang masuk akal, tapi terserah kamu.

### 5. Tiga kondisi data
Di `seed.json` ada tiga kumpulan data: **lengkap**, **minim** (cuma beberapa sesi), dan **kosong** (tidak ada sesi sama sekali).

Ketiganya harus bisa dilihat reviewer dengan mudah — lewat parameter URL, tombol, atau apa pun yang jelas. Siswa yang datanya kosong tetap harus mendapat layar yang layak dilihat, bukan pesan error dan bukan kartu berisi angka nol semua.

Ini juga cara kamu memenuhi aturan 5 menit: reviewer harus bisa melihat ketiganya tanpa menunggu apa pun.

---

## Fitur generatif: yang kami perhatikan

**Narasi yang berpijak pada data.** Ini soal utamanya. Bagaimana kamu memastikan kalimat yang tampil tidak bertentangan dengan angka yang kamu hitung? Kirim angkanya ke dalam prompt saja tidak cukup — model tetap akan mengarang sesekali. Yang kami cari adalah lapisan pemeriksaan setelah model menjawab.

**Angka tidak boleh menunggu model.** Statistik itu milik kamu dan bisa tampil seketika. Kalau seluruh kartu baru muncul setelah model selesai menulis, rekapnya terasa lambat padahal datanya sudah siap dari awal.

**Panjang teks dijaga.** Model akan mengirim dua paragraf untuk ruang yang cuma muat satu kalimat. Tata letak kamu tidak boleh rusak karenanya.

**Riwayat berisi catatan yang ditulis siswa sendiri.** Kalau kamu memasukkannya ke prompt supaya narasinya lebih personal — ide yang bagus — ingat bahwa itu teks yang tidak kamu kontrol.

**Waktu key-nya mati, rekapnya tetap utuh.** Reviewer harus tetap bisa menyusuri semua kartu sampai ekspor gambar, dengan narasi cadangan yang jujur.

---

## Di luar cakupan

- Login, akun, multi-pengguna
- Pelacakan aktivitas berjalan, timer, pencatatan sesi baru
- Rekap berkala (mingguan, bulanan) atau penjadwalan apa pun
- Perbandingan dengan siswa lain, papan peringkat
- Mengedit atau menambah riwayat
- Notifikasi

## Kalau masih ada waktu

Tidak ada batas atas, dan sejauh apa kamu naik adalah sebagian besar penilaian kami:

- Transisi antar kartu yang benar-benar halus di HP kelas menengah
- Musik atau efek suara yang bisa dimatikan
- Getaran halus saat pindah kartu
- Confetti atau puncak visual di kartu terbaik
- Tema warna yang berubah mengikuti karakter data
- Ekspor semua kartu sekaligus
- Route OG image supaya link-nya cantik saat dibagikan
- Menghormati `prefers-reduced-motion`
- Kartu pembuka yang bikin orang mau lanjut

Satu alur yang mulus dari kartu pertama sampai gambar tersimpan jauh lebih berkesan daripada sepuluh tambahan setengah jadi.

---

## Dianggap selesai kalau

- [ ] Bisa dibuka dari HP lewat URL publik, tanpa login, tanpa setup
- [ ] Ketiga kondisi data bisa dilihat reviewer dalam 5 menit
- [ ] Kartu bisa dimajukan, dimundurkan, di-swipe, dan ditahan
- [ ] Narasi tidak pernah menyebut angka yang tidak ada di perhitungan
- [ ] Angka tampil tanpa menunggu model selesai
- [ ] Kondisi data kosong tetap menghasilkan layar yang layak
- [ ] Minimal satu kartu bisa diekspor jadi gambar
- [ ] Rekapnya masih bisa didemokan waktu API key mati
- [ ] Dark mode jalan
- [ ] Warna, radius, dan font sesuai `DESIGN_SYSTEM.md`
