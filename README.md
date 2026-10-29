# Road Lane Detection

## Overview

Project ini mengembangkan pipeline **image processing klasik** (tanpa deep learning) untuk mendeteksi jalur jalan dari citra kamera, sebagai fondasi modul kemudi (_steering control_) kendaraan otonom.

### Tujuan Akhir

- Mendeteksi area/garis jalur jalan dari gambar kamera depan
- Mengekstrak koordinat jalur sebagai input untuk kontrol kemudi
- Mengklasifikasikan kondisi jalan (lurus / belok)

### Teknologi

| Komponen    | Keterangan                 |
| ----------- | -------------------------- |
| Bahasa      | Python 3.8+                |
| Library     | OpenCV, NumPy, Matplotlib  |
| Environment | Google Colab               |
| Pendekatan  | Classical Image Processing |

---

## Timeline Pertemuan

| Pertemuan | Tanggal      | Fokus                       | Pendekatan                    | Status          | Detail                            |
| --------- | ------------ | --------------------------- | ----------------------------- | --------------- | --------------------------------- |
| 1         | [24/09/2026] | Setup & deteksi garis marka | Canny + HoughLinesP           | ✅ Selesai      | [README](./Pertemuan-1/README.md) |
| 2         | [12/10/2026] | Segmentasi area jalur       | HSV + Contour                 | ✅ Selesai      | [README](./Prtemuan-2/README.md)  |
| 3         | [DD/MM/YYYY] | Tambahan area bahu jalan    | HSV + Contour + LSD vs RANSAC | ⏳ Direncanakan | —                                 |

---

## Catatan Pembimbing (Ringkasan Lintas Pertemuan)

Setiap masukan dari pembimbing dicatat di sini dan di README pertemuan terkait.

| Tanggal      | Pertemuan | Masukan / Koreksi                                 | Status             |
| ------------ | --------- | ------------------------------------------------- | ------------------ |
| [24/09/2026] | 1         | Gunakan metode yang berbeda, HSV + Contour        | ✅ Ditindaklanjuti |
| [12/10/2026] | 2         | Deteksi bahu jalan dengan garis marka keseluruhan | ✅ Ditindaklanjuti |

---

## Kontak

[dhannizd2@gmail.com] - [https://github.com/MieAyammmm]
