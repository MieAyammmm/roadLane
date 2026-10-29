# Pertemuan 2: Segmentasi Area Jalur (HSV + Contour)

**Tanggal:** 12/10/2026
**Durasi:** 60 menit
**Status:** ✅ Selesai

---

## Tujuan

- [x] Segmentasi area aspal dengan HSV thresholding
- [x] Menyaring vegetasi (hijau) dan trotoar terang
- [x] Membuat ROI poligon 4 titik khusus lajur kiri (aturan kemudi Indonesia)
- [x] Mengekstrak kontur area jalur dan menyederhanakannya (Douglas-Peucker)

---

## Data

| Item    | Keterangan                             |
| ------- | -------------------------------------- |
| File    | `data/lurus.png`                       |
| Kondisi | Jalan lurus, lajur kiri, cahaya terang |
| Sumber  | Youtube                                |

---

## Pipeline

```
INPUT (BGR)
  → Gaussian Blur (kernel 5×5, σ = 1.2)
  → Konversi ke HSV
  → ROI Poligon 4 titik (lajur kiri)
  → HSV Thresholding (H, S, V + eksklusi hijau)
  → Morfologi: Opening (5×5) → Closing (15×15)
  → Contour terbesar (RETR_EXTERNAL)
  → Douglas-Peucker simplification (ε = 1% keliling)
  → Overlay hasil di atas citra asli
```

### Parameter Utama

| Parameter           | Nilai    | Fungsi                                            |
| ------------------- | -------- | ------------------------------------------------- |
| `h_reject_green`    | 35 – 85  | Membuang Hue vegetasi                             |
| `s_max`             | 100      | Aspal terang tetap lolos                          |
| `v_min` / `v_max`   | 50 / 255 | Membuang area sangat gelap, menerima semua terang |
| `kernel_open_size`  | (5, 5)   | Menghapus noise kecil                             |
| `kernel_close_size` | (15, 15) | Menutup lubang pada aspal                         |
| `min_contour_area`  | 1000 px  | Mengabaikan kontur kecil                          |
| `dp_epsilon_ratio`  | 0.01     | Tingkat penyederhanaan kontur                     |

### ROI

| Titik | Koordinat (x, y) | Posisi      |
| ----- | ---------------- | ----------- |
| 1     | (450, 1010)      | Kiri bawah  |
| 2     | (1410, 1010)     | Kanan bawah |
| 3     | (970, 635)       | Kanan atas  |
| 4     | (970, 635)       | Kiri atas   |

---

## Hasil

- Area jalur lajur kiri tersegmentasi sebagai kontur tunggal
- Jumlah titik kontur setelah simplifikasi: 3
- Area kontur: 170194.00 piksel
- Overlay disimpan sebagai `result_lurus.png`

---

## Keterbatasan & Known Issues

- **ROI titik 3 dan 4 identik** `(970, 635)`, sehingga bagian atas ROI berbentuk segitiga, bukan trapesium
- Parameter ROI dan HSV masih disetel manual untuk satu gambar; belum diuji pada variasi cahaya
- Area aspal yang berwarna mirip trotoar terang berpotensi ikut terdeteksi

---

## Catatan Pembimbing

| Tanggal    | Masukan / Koreksi                                               | Tindak Lanjut                 | Status |
| ---------- | --------------------------------------------------------------- | ----------------------------- | ------ |
| 12/10/2026 | Tambahkan treshloding pada HSV agar tidak perlu membuat fix ROI | Menambah tresholding pada HSV | ✅     |

---

## Rencana Pertemuan Berikutnya

- [ ] Gunakan kondisi jalan yang berbeda
- [ ] Tambahan: Fokus baru, menangani masalah kendaraan yang menepi ke bahu jalan
