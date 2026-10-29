# Pertemuan 1: Deteksi Garis Marka Jalan (Canny + HoughLinesP)

**Tanggal:** [24/09/2026]
**Durasi:** 60 menit
**Status:** ✅ Selesai

---

## Tujuan

- [x] Menyiapkan environment dan struktur repository
- [x] Membuat pipeline deteksi 2 garis marka jalan (kiri & kanan)
- [x] Visualisasi pipeline dalam 4 subplot

---

## Data

| Item     | Keterangan                      |
| -------- | ------------------------------- |
| File     | `data/1straight.png`            |
| Format   | PNG                             |
| Kondisi  | Jalan lurus, marka putih terang |
| Sumber   | [Youtube ]                      |
| Resolusi | [1920 × 1080]                   |

---

## Pipeline

```
INPUT (RGB)
  → Grayscale + Gaussian Blur (kernel 5×5, σ = 1.0)
  → Canny Edge Detection (T_low = 50, T_high = 150)
  → Tight ROI Trapezium (mask area jalan)
  → HoughLinesP (segmen garis)
  → Klasifikasi kiri/kanan (filter slope & posisi x)
  → Analisis kemiringan → JALAN LURUS / BELOK KIRI / BELOK KANAN
  → OUTPUT: koordinat jalur + status jalan
```

### Parameter Utama

| Parameter             | Nilai                  | Fungsi                                 |
| --------------------- | ---------------------- | -------------------------------------- |
| `GAUSSIAN_KERNEL`     | (5, 5)                 | Mereduksi noise sebelum edge detection |
| `CANNY_LOW / HIGH`    | 50 / 150               | Ambang batas tepi                      |
| `HOUGHP_THRESHOLD`    | 20                     | Minimum vote di ruang Hough            |
| `HOUGHP_MIN_LINE_LEN` | 20 px                  | Panjang minimal segmen                 |
| `HOUGHP_MAX_LINE_GAP` | 30 px                  | Celah maksimal yang disambung          |
| Filter slope          | 0.45 ≤ \|m\| ≤ 2.0     | Membuang garis horizontal dan vertikal |
| `ROI` (y)             | 65% – 95% tinggi citra | Membatasi area ke jalan                |

---

## Hasil

- Garis kiri dan kanan berhasil terdeteksi pada `1straight.png`
- Status geometris: **[isi hasil, misalnya JALAN LURUS]**
- Output visual disimpan sebagai `lane_detection_result.png`

---

## Keterbatasan

- Hanya berlaku untuk jalan lurus dan satu gambar statis

---

## Catatan Pembimbing

| Tanggal      | Masukan / Koreksi                                                                    | Tindak Lanjut                                    | Status |
| ------------ | ------------------------------------------------------------------------------------ | ------------------------------------------------ | ------ |
| [12/09/2026] | Pakai pendekatan yang berbeda dengan fokus pada area jalan menggunakan HSV + Contoyr | Deteksi area jalur jalan menggunakan HSV Contour | ✅     |

---

## Rencana Pertemuan Berikutnya

- Mengganti pendekatan ke segmentasi area jalur berbasis warna (lihat [Pertemuan 2](../Pertemuan-2/README.md))
