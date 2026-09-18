# Road Lane Detection for Autonomous Vehicles

**Project Status:** Stage 1 - Static Image Analysis (Straight Road Detection)

## 📋 Project Overview

Implementasi pipeline **Image Processing klasik** untuk deteksi garis marka jalan pada gambar statis, dengan fokus awal pada jalan lurus.

### Teknologi

- **Language:** Python 3.8+
- **Framework:** OpenCV, NumPy, Matplotlib
- **Environment:** Google Colab
- **Approach:** Classical Image Processing (Canny Edge Detection + Hough Line Transform)

---

## 🎯 Objectives (Stage 1)

- ✅ Deteksi 2 garis marka jalan (kiri & kanan) dari gambar statis
- ✅ Ekstraksi koordinat endpoint: `(x1, y1, x2, y2)`
- ✅ Analisis road type: **JALAN LURUS** vs BELOK
- ✅ Visualisasi pipeline di 4 subplot
- ⏳ (Future) Integrasi dengan modul steering control

---

## 📊 Pipeline Architecture

INPUT IMAGE (RGB)
↓
[PREPROCESSING] Grayscale + Gaussian Blur (5×5, σ=1.0)
↓
[CANNY EDGE DETECTION] T_low=50, T_high=150
↓
[TIGHT ROI MASKING] Trapezium ROI (eliminate background noise)
↓
[HOUGHLINESP] Segment-based line detection
↓
[LANE CLASSIFICATION] Filter by slope + position
↓
[ROAD ANALYSIS] Curvature detection (STRAIGHT/CURVE)
↓
OUTPUT: Lane coordinates + Road status

---

## 🚀 Quick Start

### Prerequisites

- Google Colab account
- Sample road image (PNG/JPG format)

### Steps

1. **Open Notebook:** `notebooks/lane_detection_stage1.ipynb` di Google Colab
2. **Upload Gambar:** Unggah file gambar jalan ke Colab
3. **Run All Cells:** Execute notebook untuk melihat deteksi lane
4. **Output:** Gambar dengan 4 subplot visualization + koordinat lane

## 📝 Notes

- **Tahap Pertama:** Fokus pada akurasi deteksi, bukan kecepatan
- **Test Image:** Gunakan gambar jalan lurus dengan marka putih terang
- **Edge Cases:** Bayangan pohon, variasi pencahayaan akan ditangani di stage berikutnya
