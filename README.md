# Analisis Ketahanan Pipeline Instance Segmentation Klasik pada Citra Silindris (Tumbler) dengan Variasi Iluminasi Ekstrem

## Deskripsi Proyek
Proyek ini menguji ketahanan pipeline instance segmentation berbasis pengolahan citra digital klasik (tanpa deep learning) untuk mendeteksi dan menghitung objek silindris (tumbler) pada dua skenario iluminasi ekstrem. Pipeline menggabungkan Gaussian Blur, CLAHE, Otsu's Thresholding, operasi morfologi (Closing & Opening), Distance Transform, dan Watershed. Hasil menunjukkan akurasi perhitungan 100% pada kedua citra uji.

## Tujuan
- Membangun pipeline segmentasi instans klasik untuk deteksi & hitung tumbler otomatis.
- Menganalisis efektivitas setiap tahapan pipeline dalam menangani variasi kontras dan bayangan.
- Mengevaluasi Distance Transform & Watershed dalam memisahkan objek yang berdempetan (oklusi).

## Tools & Library
- Python 3
- OpenCV (image processing)
- NumPy (operasi numerik)
- Matplotlib (visualisasi)
- Google Colab

## Tahapan Pipeline
1. **Grayscale & Analisis HSV** - Konversi BGR ke grayscale
2. **Spatial Filtering** - Gaussian Blur untuk reduksi noise
3. **Peningkatan Kontras** - CLAHE (clipLimit=3.0, tileGridSize=(8,8))
4. **Binarisasi** - Otsu's Thresholding + Inverse (THRESH_BINARY_INV)
5. **Morfologi** - Closing (5x5, iter 1) + Opening (5x5, iter 2) + Erosi
6. **Distance Transform** - Euclidean (L2), threshold 20% (Citra 1) & 30% (Citra 2)
7. **Watershed** - Sure foreground + Sure background + Unknown region
8. **Ekstraksi Kontur** - RETR_EXTERNAL + Area Filtering (>500 px Citra 1, >1000 px Citra 2)

## Hasil
| Skenario | Jumlah Objek (Ground Truth) | Terdeteksi | Akurasi |
|---|---|---|---|
| Citra 1 (Low Density, Latar Heterogen) | 2 | 2 | 100% |
| Citra 2 (High Density, Oklusi Ekstrem) | 1 | 1 | 100% |

- **CLAHE** efektif mengangkat detail pada objek gelap tanpa mengamplifikasi noise.
- **Morfologi Closing** menambal lubang akibat specular highlights.
- **Distance Transform + Watershed** mampu memisahkan objek yang berdempetan rapat.
- Pipeline klasik terbukti **robust** tanpa deep learning dan komputasi efisien.

## File Terkait
- Notebook Segmentasi<br>(./notebook/instance_segmentation_tumbler.ipynb)

## Author
**Fauziah Roikhana Wardah** (dan tim)
- Program Studi S1 Sains Data, Universitas Negeri Surabaya
