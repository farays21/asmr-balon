# 🎈 ASMR Balon Pemecah

Web interaktif bertema ASMR: balon-balon warna-warni melayang bebas ke kanan-kiri dan atas-bawah, dan ketika disentuh (klik / tap) balon akan pecah lengkap dengan efek visual, partikel, serta suara.

Seluruh aplikasi berada di **satu file** (`index.html`) — tanpa framework, tanpa dependency, tanpa aset eksternal.

---

## ✨ Fitur

| Fitur | Keterangan |
| --- | --- |
| 🎨 **Balon warna-warni** | 8 palet warna, ukuran acak, dengan kilau (highlight) dan simpul balon |
| 🌀 **Gerakan mengambang** | Balon berjalan ke kanan–kiri dan atas–bawah, memantul di tepi layar, ditambah gerakan bergoyang (sway) |
| 💥 **Efek pecah** | Ledakan partikel, cincin kejut (shockwave), dan flash lembut di layar |
| 🔊 **Suara ASMR** | Suara "pop" disintesis langsung dengan **Web Audio API** (getaran noise + bass thump) |
| 🌙 **Ambient layer** | Lapisan suara latar lembut yang dapat dinyalakan/dimatikan |
| 🔥 **Combo** | Memecahkan beberapa balon secara beruntun dalam 1,2 detik memicu chime dan teks combo |
| ⚙️ **Kontrol** | Tombol suara, tombol ambient, slider kecepatan, dan tombol reset |
| 📱 **Responsif** | Mendukung desktop (mouse) dan mobile (sentuh), termasuk getar haptic bila didukung |
| 🎯 **Deteksi akurat** | Hit-test berbentuk **elips**, bukan kotak, sehingga klik harus tepat mengenai badan balon |

---

## 🚀 Cara Menjalankan

1. Buka folder `test2`.
2. Klik dua kali `index.html`, atau buka lewat browser favorit:

```
D:\folder\opencode\test2\index.html
```

Atau jalankan server lokal sederhana (opsional):

```bash
# Python 3
python -m http.server 8000

# lalu buka http://localhost:8000
```

> **Catatan:** suara baru aktif setelah interaksi pertama (klik/tap), sesuai kebijakan autoplay browser. Volume bawaan perangkat Anda perlu dinaikkan agar sensasi ASMR-nya terasa.

---

## 🖱️ Cara Pakai

| Aksi | Efek |
| --- | --- |
| Klik / tap balon | Balon pecah, skor +1, suara pop |
| Memecah cepat beruntun | Combo bertambah (x2, x3, ...) + chime |
| Tombol 🔊 / 🔇 | Menyalakan / mematikan semua suara |
| Tombol 🌙 / ☀️ | Menyalakan / mematikan ambient |
| Slider **Kecepatan** | Mengatur kecepatan gerak balon (30% – 220%) |
| Tombol **⟳ Reset** | Mengosongkan panggung dan memulai ulang skor |

---

## 🧩 Struktur Proyek

```
test2/
└── index.html      # seluruh aplikasi (HTML + CSS + JS)
```

### Bagian penting di dalam `index.html`

- **`<style>`** — latar ambient (gradient + blob blur), panel HUD glassmorphism, bentuk balon, dan animasi pendukung.
- **`initAudio()` / `startAmbient()` / `playPop()` / `playChime()`** — seluruh suara dibuat secara sintetis menggunakan Web Audio API.
- **`spawnBalloon()`** — membuat balon baru beserta state geraknya (posisi, kecepatan, sway, fase).
- **`frame()`** — loop `requestAnimationFrame` yang menggerakkan semua balon dan memantulkannya di tepi layar.
- **`hitTest()`** — mendeteksi apakah koordinat pointer berada di dalam elips balon.
- **`pop()`** — menangani skor, combo, efek pecah, suara, dan respawn balon pengganti.

---

## ⚙️ Penyesuaian Cepat

Beberapa nilai yang mudah diubah di dalam `index.html`:

```js
const MAX_BALLOONS = 18;   // jumlah balon maksimal di layar
```

```js
const PALETTE = [ ... ];   // daftar warna balon (base & light)
```

- **Kecepatan dasar balon** → atur nilai `vx` / `vy` di dalam `spawnBalloon()`.
- **Besaran goyangan** → `swayAmp` dan `swaySpeed`.
- **Durasi combo** → `setTimeout(..., 1200)` di dalam fungsi `pop()`.
- **Volume ambient** → nilai `0.05` pada `setAmbient()`.

---

## 🌐 Kompatibilitas

- Chrome / Edge / Firefox / Safari versi modern
- Web Audio API & `Element.animate()` (Web Animations API) — didukung luas di browser terbaru

---

## 📄 Lisensi

Bebas digunakan dan dimodifikasi untuk keperluan pribadi maupun pembelajaran.
