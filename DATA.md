# Data

Semua data ada di [`data/seed.json`](./data/seed.json). Tidak ada database yang perlu disiapkan.

## Skema yang dimaksudkan

```ts
{
  versi: string
  catatan: string
  subtes_resmi: string[]        // daftar subtes resmi SNBT
  dataset: {
    lengkap: Dataset
    minim: Dataset
    kosong: Dataset
  }
}

type Dataset = {
  siswa: {
    id: string
    nama: string
    kelas: string
    target_jurusan: string
    target_kampus: string
  }
  sesi: Sesi[]
}

type Sesi = {
  id: string                    // unik
  tanggal: string               // ISO 8601, zona +07:00
  subtes: string                // salah satu dari subtes_resmi
  topik: string
  durasi_menit: number
  jumlah_soal: number
  jumlah_benar: number          // <= jumlah_soal
  sumber: "latihan" | "tryout" | "video"
  catatan: string | null        // ditulis sendiri oleh siswa
}
```

## Tiga kondisi data

| Kunci | Isi | Untuk apa |
|---|---|---|
| `lengkap` | riwayat penuh satu siswa | kondisi utama, ini yang paling sering dilihat |
| `minim` | tiga sesi pendek | siswa yang baru mulai — angkanya terlalu sedikit untuk banyak jenis kesimpulan |
| `kosong` | tidak ada sesi sama sekali | siswa yang belum pernah belajar |

Ketiganya **wajib bisa dicapai reviewer dengan mudah**. Cara paling sederhana: `?dataset=kosong` di URL, atau pemilih kecil di pojok layar. Terserah kamu, asal jelas dan tidak perlu dijelaskan lewat chat.

Kondisi `kosong` bukan kasus pinggiran yang boleh dilewat. Di produk nyata, itu justru siswa yang paling perlu dibujuk untuk mulai.

## Catatan penting

Itu skema **yang dimaksudkan**. Isi file sebenarnya datang dari sistem produksi kami — termasuk baris hasil migrasi lama, sesi yang timer-nya lupa dimatikan, dan catatan yang diketik sendiri oleh siswa — dan tidak semuanya patuh.

Kami tidak akan memberi tahu di mana letak masalahnya. Membaca data sebelum menulis kode di atasnya adalah bagian dari pekerjaan. Periksa sendiri, lalu putuskan apa yang aplikasi kamu lakukan untuk tiap kasus: dibuang, diperbaiki, atau ditampilkan dengan catatan.

Yang kami nilai bukan apakah kamu menemukan semuanya, tapi apa yang terjadi kalau ada yang lolos — dan apakah angka yang akhirnya tampil di kartu rekap masih bisa dipercaya.

Satu petunjuk umum yang bukan jebakan, cuma kenyataan: **statistik yang salah hitung jauh lebih berbahaya daripada statistik yang tidak ditampilkan.** Rekap yang memuji siswa atas sesuatu yang tidak dia capai adalah kegagalan produk, bukan kesalahan kecil.

## `catatan` milik siswa

Field `catatan` diketik sendiri oleh siswa. Isinya pendek, informal, dan kadang berantakan.

Memasukkannya ke prompt supaya narasinya lebih personal adalah ide yang bagus. Ingat saja bahwa isinya sepenuhnya di luar kendali kamu.

## Boleh diubah?

Boleh — ubah bentuknya, pindahkan ke database, buat turunan, sesukamu.

Yang tidak boleh: menghapus baris yang merepotkan, atau merapikan file-nya sekali di awal lalu berpura-pura data produksi memang serapi itu.
