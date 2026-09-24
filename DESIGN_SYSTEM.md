# Design System Pintarly

Ini design system yang dipakai di produk Pintarly. Semua UI yang kamu bangun di capstone ini harus mengikutinya.

Kenapa kami ketat soal ini: tool AI punya "selera bawaan" — gradient ungu, kartu kotak, tombol biru, font Inter. Kalau kamu cuma minta "bikin UI yang bagus", hasilnya akan terlihat seperti semua aplikasi AI lain di internet. Yang kami cari adalah orang yang bisa membuat tool-nya patuh pada sistem yang sudah ada. Jadi jangan cuma baca file ini — pastikan AI kamu juga membacanya.

---

## 1. Warna: WAJIB pakai CSS variable, JANGAN hex

```tsx
// SALAH
className="bg-[#ffe16f] text-[#1A1A1B] border-[#e5e7eb]"

// BENAR
className="bg-[var(--yellow-500)] text-[var(--black-charcoal)] border-[var(--neutral-200)]"
```

Alasannya bukan soal rapi-rapian: dark mode kami jalan dengan cara menukar nilai variable. Begitu kamu menulis hex, komponen itu langsung rusak di dark mode.

Definisikan semua token di bawah ini di `globals.css` kamu.

### Blue (Sky)
```css
--blue-50: #f5fcff;   --blue-100: #dff6fe;  --blue-200: #d0f2fe;
--blue-300: #baecfe;  --blue-400: #ade8fd;  --blue-500: #98e2fd;  /* aksen utama */
--blue-600: #8acee6;  --blue-700: #6ca0b4;  --blue-800: #547c8b;  --blue-900: #405f6a;
```

### Yellow (Butter) — tombol utama
```css
--yellow-50: #fffcf1;  --yellow-100: #fff6d2;  --yellow-200: #fff1bd;
--yellow-300: #ffeb9f;  --yellow-400: #ffe78c;  --yellow-500: #ffe16f;  /* CTA */
--yellow-600: #e8cd65;  --yellow-700: #b5a04f;  /* hover CTA */
--yellow-800: #8c7c3d;  --yellow-900: #6b5f2f;
```

### Green (Chartreuse)
```css
--green-50: #fafef2;  --green-100: #f1fad6;  --green-200: #eaf8c2;
--green-300: #e0f5a7;  --green-400: #daf395;  --green-500: #d1f07b;  /* aksen kedua */
--green-600: #beda70;  --green-700: #94aa57;  --green-800: #738444;  --green-900: #586534;
```

### Red (Rose/Error)
```css
--red-50: #fef2f2;  --red-100: #fee2e2;  --red-200: #fecaca;  --red-300: #fca5a5;
--red-400: #f87171;  --red-500: #ef4444;  --red-600: #dc2626;  --red-700: #b91c1c;
--red-800: #991b1b;  --red-900: #7f1d1d;
```

### Purple (Lavender)
```css
--purple-50: #faf5ff;  --purple-100: #f3e8ff;  --purple-200: #e9d5ff;
--purple-300: #d8b4fe;  --purple-400: #c084fc;  --purple-500: #a855f7;
--purple-600: #9333ea;  --purple-700: #7e22ce;  --purple-800: #6b21a8;  --purple-900: #581c87;
```

### Neutral
```css
--white-arctic: #f9fafb;  /* background utama */
--neutral-50: #f9fafb;   --neutral-100: #f3f4f6;  /* skeleton */
--neutral-200: #e5e7eb;  /* border */
--neutral-300: #d1d5db;  --neutral-400: #9ca3af;  /* placeholder */
--neutral-500: #6b7280;  /* teks sekunder */
--neutral-600: #4b5563;  --neutral-700: #374151;  --neutral-800: #1f2937;
--neutral-900: #1a1a1b;  --black-charcoal: #1a1a1b;  /* teks utama */
```

### Semantik
```css
--surface-strong: #ffffff;
--card-bg: #ffffff;
--card-border: var(--neutral-200);
--card-radius: 24px;
--button-radius: 100px;
--input-radius: 12px;
```

### Dark mode
Aktif lewat class `.dark` di `<html>`. Nilai token-nya ditukar, komponennya tidak diubah:

```css
.dark {
  --white-arctic: #202124;
  --neutral-50: #292a2d;   --neutral-100: #2d2f33;  --neutral-200: #3c4043;
  --neutral-300: #5f6368;  --neutral-400: #80868b;  --neutral-500: #9aa0a6;
  --neutral-600: #bdc1c6;  --neutral-700: #dadce0;  --neutral-800: #e8eaed;
  --neutral-900: #f1f3f4;
  --black-charcoal: #e8eaed;
  --card-bg: #303134;
  --surface-strong: #202124;
  --card-border: #3c4043;
}
```

Dark mode harus benar-benar jalan dan bisa di-toggle oleh reviewer.

---

## 2. Komposisi 60/30/10

Ini yang bikin Pintarly terasa "Pintarly" dan bukan template:

- **60% — Ethereal Clarity.** `var(--white-arctic)` sebagai kanvas utama. Lapang, banyak ruang kosong.
- **30% — Personalized Depth.** Mesh gradient lembut dari `var(--blue-500)` + `var(--green-500)`, boleh pakai overlay noise tipis.
- **10% — Action Fun.** `var(--yellow-500)` khusus untuk CTA dan elemen gamifikasi.

Kuning itu mahal. Kalau semua tombol kuning, tidak ada yang menonjol.

---

## 3. Tipografi

| Elemen | Font | Weight | Ukuran |
|---|---|---|---|
| Heading (H1, H2) | Outfit | 600–700 | 22–28px |
| Body | Plus Jakarta Sans | 400–500 | 14–16px |
| Teks tombol | Outfit | 600 | 16px |
| Teks sekunder | Plus Jakarta Sans | 400 | 14px, `var(--neutral-600)` |

Dua font ini ada di Google Fonts. Muat lewat `next/font/google`, jangan `<link>` manual.

---

## 4. Komponen

Radius itu identitas merek di sini. Jangan diubah-ubah.

**Tombol — selalu `rounded-full`**
```tsx
// Primary
className="px-5 py-2 bg-[var(--yellow-500)] hover:bg-[var(--yellow-700)] text-[var(--black-charcoal)] rounded-full text-sm font-heading font-semibold transition-all"

// Secondary
className="px-5 py-2 bg-[var(--blue-500)] hover:bg-[var(--blue-700)] text-[var(--black-charcoal)] rounded-full text-sm font-heading font-semibold transition-all"

// Outline
className="px-5 py-2 bg-white hover:bg-[var(--neutral-50)] text-[var(--neutral-700)] border border-[var(--neutral-200)] rounded-full text-sm font-heading font-semibold transition-all"
```

**Kartu — selalu `rounded-[24px]`**
```tsx
className="bg-[var(--card-bg)] rounded-[24px] border border-[var(--card-border)] p-6 shadow-sm"

// Varian glass
className="bg-white/80 backdrop-blur-md rounded-[24px] border border-[var(--neutral-200)] p-6 shadow-sm"
```

**Input — selalu `rounded-xl` (12px)**
```tsx
className="h-12 w-full rounded-xl border border-[var(--neutral-200)] px-4 text-[var(--black-charcoal)] placeholder:text-[var(--neutral-400)] focus-visible:[box-shadow:0_0_0_2px_var(--yellow-300)] focus-visible:border-[var(--yellow-300)]"
```

> **Catatan Tailwind v4 yang bakal bikin kamu bingung:** focus ring-nya sengaja ditulis sebagai arbitrary property `[box-shadow:...]`, bukan `ring-2` atau `shadow-*`. Di Tailwind v4, utility `ring-*`/`shadow-*` tidak bisa membaca CSS `var()` karena mereka lewat komposisi variable `--tw-*` dulu. Kalau kamu pakai `ring-[var(--yellow-300)]`, ring-nya tidak akan muncul dan tidak ada error apa pun. Ini bug yang sering bikin orang buang waktu satu jam.

**Badge**
```tsx
className="px-2 py-0.5 bg-[var(--blue-50)] text-[var(--blue-700)] rounded-full text-xs font-medium"
```

**Icon badge** (ikon berwarna di atas background lembut)
```tsx
// Wadah
className="w-14 h-14 rounded-xl bg-[var(--blue-50)] border border-[var(--blue-200)] flex items-center justify-center"
// Ikon di dalamnya
className="w-7 h-7 text-[var(--blue-600)]"
// Varian: tukar blue → green / yellow / red
```

**Empty state**
```tsx
<div className="flex flex-col items-center justify-center py-20">
  <div className="w-20 h-20 rounded-full bg-gradient-to-br from-[var(--blue-100)] to-[var(--green-100)] flex items-center justify-center mb-5">
    <Icon className="w-8 h-8 text-[var(--neutral-400)]" />
  </div>
  <h3 className="text-lg font-semibold text-[var(--neutral-900)] mb-1.5">Judul</h3>
  <p className="text-sm text-[var(--neutral-500)] text-center max-w-xs">Penjelasan singkat</p>
</div>
```

**Modal**
- Backdrop: `bg-black/50 backdrop-blur-sm z-50`
- Kontainer: `bg-[var(--card-bg)] rounded-2xl shadow-xl`
- Animasi: `animate-in zoom-in-95 fade-in duration-200`
- Klik backdrop **harus** menutup modal.

---

## 5. Responsif (mobile-first)

Mayoritas pengguna Pintarly membuka aplikasi dari HP. Desain dari layar kecil dulu, baru lebarkan.

| Properti | Mobile | Desktop (`md:`) |
|---|---|---|
| Padding kontainer | `px-4` | `md:px-8` |
| Jarak antar section | `space-y-6` | `md:space-y-10` |
| Padding atas | `pt-6` | `md:pt-12` |
| Padding kartu | `p-4` | `md:p-6` |
| Ukuran ikon | `w-4 h-4` | `md:w-5 md:h-5` |
| Judul section | `text-base` | `md:text-lg` |
| Lebar maksimum | `w-full` | `max-w-4xl` untuk konten |

Grid **selalu** mulai dari `grid-cols-1`:
```tsx
className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4"
```
`grid` tanpa `grid-cols-1` adalah penyebab paling sering layar HP jadi bisa digeser ke samping.

---

## 6. Ikon & animasi

- Ikon: `lucide-react`.
- Animasi: `framer-motion` kalau perlu, CSS transition kalau cukup.
- Animasi hanya `transform` dan `opacity`. Jangan menganimasikan `width`, `height`, `top`, `left` — itu memicu layout dan patah-patah di HP kelas menengah, yang dipakai sebagian besar siswa kami.

---

## 7. Yang membuat kami menutup tab

- Hex ditulis langsung di className.
- Class `gray-*` bawaan Tailwind (`text-gray-500`, `bg-gray-100`). Netral kami beda, campurannya kelihatan kotor.
- Ukuran font atau spacing arbitrary (`text-[13px]`, `p-[18px]`). Pakai skala Tailwind.
- Tombol kotak atau `rounded-md`. Tombol kami `rounded-full`, titik.
- Component kit yang bawa tampilan sendiri (MUI, Chakra, theme default shadcn, Ant Design). Headless primitive seperti Radix boleh.
- Loading state berupa spinner di tengah layar kosong. Pakai skeleton yang bentuknya mirip konten aslinya.
- Tidak ada empty state, tidak ada error state. Data yang kami kasih menjamin kamu akan butuh keduanya.
