# 🚀 CNN Scratch vs Transfer Learning (MobileNetV2)

Repository ini berisi eksperimen perbandingan performa, efisiensi parameter, dan konvergensi pelatihan antara arsitektur **Convolutional Neural Network (CNN) dari awal (Scratch)** dengan teknik **Transfer Learning (MobileNetV2 Pre-trained ImageNet)** menggunakan TensorFlow / Keras.

---

## 📌 Ringkasan Hasil Eksperimen

| Metrik / Parameter | CNN Scratch | Transfer Learning (MobileNetV2) |
| :--- | :--- | :--- |
| **Dataset** | CIFAR-10 (10 Kelas) | Flower Photos - Roses vs Tulips (2 Kelas) |
| **Input Shape** | $(32, 32, 3)$ | $(160, 160, 3)$ |
| **Total Parameters** | 367,712 (1.40 MB) | 2,261,829 (8.63 MB) |
| **Trainable Parameters** | **122,570 (478 KB)** | **1,281 (5.00 KB)** |
| **Non-Trainable Params** | 0 (0.00 B) | 2,257,984 (8.61 MB) |
| **Jumlah Epoch** | 15 Epoch | 5 Epoch |
| **Akurasi Validasi** | **~73.24%** | **~90%+** |

---

## 🛠️ Ringkasan Arsitektur Model

### 1. Model CNN Scratch
- **Feature Extractor:** 3 Layer `Conv2D` dipadukan dengan `MaxPooling2D`.
- **Regularization:** `Dropout(0.5)` sebelum Fully Connected Layer untuk mencegah *overfitting*.
- **Classifier Head:** `Dense(64, activation='relu')` $\rightarrow$ `Dense(10, activation='softmax')`.
- **Metrik Utama:** Seluruh **122,570 parameter** di-update dari awal (*random initialization*).

### 2. Model Transfer Learning (MobileNetV2)
- **Base Model:** MobileNetV2 dengan bobot pre-trained ImageNet (`base_model.trainable = False`).
- **Feature Aggregation:** `GlobalAveragePooling2D`.
- **Regularization:** `Dropout(0.2)`.
- **Classifier Head:** `Dense(1, activation='sigmoid')`.
- **Metrik Utama:** Hanya **1,281 parameter** pada *classifier head* yang dilatih, sehingga proses *training* per epoch sangat ringan dan konvergen secara instan.

---

## 🔑 Kesimpulan Utama

1. **Efisiensi Komputasi:** Dengan membekukan (*freezing*) *feature extractor* MobileNetV2, jumlah *trainable parameters* berkurang **>98%** dibanding CNN Scratch, memangkas waktu *training* di GPU secara drastis.
2. **Akurasi & Konvergensi:** *Transfer Learning* memanfaatkan ekstraksi fitur hirarkis dari dataset skala besar (ImageNet), memungkinkan model mencapai akurasi **>90%** hanya dalam 5 epoch.
3. **Penerapan Praktis:** CNN Scratch sangat baik untuk memahami mekanisme visual dasar, sedangkan *Transfer Learning* merupakan metode standar terbaik untuk tugas praktis di industri.

---

## 📁 Struktur Repositori

```text
├── CNN_Scratch_vs_Transfer_Learning.ipynb   # Google Colab Notebook (Kode & Output)
└── README.md                                # Dokumentasi eksperimen
