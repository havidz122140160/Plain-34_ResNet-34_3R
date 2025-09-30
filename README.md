# Laporan Benchmark: Perbandingan Kinerja Plain-34 vs ResNet-34

---

## Anggota Kelompok:
1. Havidz Ridho Pratama - 122140160
2. Rayhan Fadel Irwanto - 122140236
3. Royfran Roger Valentino - 122140239

---

Laporan ini menganalisis perbandingan performa antara dua arsitektur jaringan syaraf tiruan: sebuah jaringan "polos" dengan 34 lapisan (Plain-34) dan sebuah jaringan ResNet-34. Eksperimen ini bertujuan untuk mendemonstrasikan secara empiris dampak dari implementasi *residual connection* pada stabilitas dan performa pelatihan model yang dalam.

---

## 1. Konfigurasi Eksperimen

Untuk memastikan perbandingan yang adil, kedua model dilatih dengan dataset dan konfigurasi hyperparameter yang identik.

* **Dataset**: 5 Kelas Makanan Indonesia
* **Arsitektur Dasar**: ResNet-34 (Plain-34 adalah ResNet-34 tanpa *residual connection*)
* **Jumlah Epoch**: 15
* **Batch Size**: 32
* **Optimizer**: Adam
* **Learning Rate**: 0.001
* **Loss Function**: Cross-Entropy Loss
* **Seed**: 42 (untuk reproduksibilitas)

---

## 2. Hasil Performa

### 2.1. Tabel Perbandingan Metrik

Tabel berikut merangkum metrik performa kunci dari kedua model berdasarkan hasil pelatihan terbaru.

| Metrik                      | Plain-34 (Baseline) | ResNet-34          |
| --------------------------- | ------------------- | ------------------ |
| **Akurasi Validasi Terbaik** | [cite_start]~55.0% [cite: 2, 3]              | [cite_start]**~83.0%** [cite: 1, 3] |
| Akurasi Training (Final)    | [cite_start]~46.0% [cite: 2]              | [cite_start]~72.0% [cite: 1]             |
| Loss Validasi (Final)       | [cite_start]~1.30 [cite: 2]               | [cite_start]~0.60 [cite: 1]              |
| Loss Training (Final)       | [cite_start]~1.20 [cite: 2]               | [cite_start]~0.80 [cite: 1]              |

### 2.2. Grafik Kurva Pelatihan

Grafik di bawah ini memvisualisasikan perbandingan kurva akurasi validasi antara kedua model selama 15 epoch.

*Ganti placeholder di bawah ini dengan screenshot grafik perbandingan yang baru (image_ec6ac9.png)*
![Grafik Perbandingan Akurasi](https://i.imgur.com/your_new_comparison_graph_link.png)

---

## 3. Analisis Singkat

Berdasarkan hasil eksperimen terbaru, perbedaan performa antara arsitektur Plain-34 dan ResNet-34 tetap sangat signifikan. [cite_start]Model ResNet-34 berhasil mencapai akurasi validasi puncak yang jauh lebih superior, yaitu sekitar **83.0%** [cite: 1, 3][cite_start], sementara Plain-34 hanya mampu mencapai puncak di sekitar **55.0%**[cite: 2, 3].

Grafik pelatihan Plain-34 menunjukkan gejala klasik dari *degradation problem*. [cite_start]Kurva validasinya sangat tidak stabil dan performanya stagnan di level yang rendah[cite: 2]. Hal ini mengindikasikan bahwa tanpa bantuan, model gagal belajar secara efektif seiring dengan bertambahnya kedalaman jaringan. [cite_start]Proses optimisasinya menjadi tidak efisien, yang tecermin dari ketidakmampuan model untuk melampaui akurasi 55%[cite: 2].

[cite_start]Di sisi lain, meskipun kurva validasi ResNet-34 juga menunjukkan volatilitas, tren keseluruhannya jelas positif dan mampu menembus "langit-langit" performa yang tidak bisa dicapai oleh Plain-34[cite: 1, 3]. Kemampuan ResNet-34 untuk mencapai akurasi puncak yang jauh lebih tinggi membuktikan bahwa implementasi **residual connection** berhasil mengatasi masalah degradasi. "Jalan pintas" ini memungkinkan aliran gradien yang lebih baik, sehingga model yang lebih dalam dapat dilatih secara efektif. Peningkatan performa yang drastis ini mengkonfirmasi keunggulan fundamental arsitektur ResNet.

---

## 4. Link ke Source Code

Source code lengkap untuk implementasi ResNet-34 yang dimodifikasi dari Plain-34 dapat diakses melalui repositori GitHub berikut:

*Ganti placeholder di bawah ini dengan link ke repositori GitHub kelompok Abang*
`[Link ke Repositori GitHub](https://github.com/username/nama-repo)`

---

## 5. Peran dan Kontribusi AI Assistant

Sesuai ketentuan tugas, penggunaan AI Assistant dalam pengerjaan proyek ini diperbolehkan sebagai alat peningkat produktivitas. Berikut adalah rincian peran dan kontribusi AI Assistant (Gemini) dalam proyek ini.

* **Prompt dan Masalah yang Diajukan ke AI**:
    * **Pemahaman Kode**: Meminta penjelasan mengenai *starter code* `Plain-34`, termasuk struktur `PlainBlock` dan alur `forward pass`.
    * **Panduan Implementasi**: Meminta panduan langkah demi langkah untuk menyelesaikan tugas di lingkungan Google Colab, mulai dari setup awal, pelatihan model, hingga analisis perbandingan.
    * **Modifikasi Kode**: Meminta contoh kode untuk mengubah `PlainBlock` menjadi `BasicBlock` dengan menambahkan *residual connection* (`out += identity`).
    * **Debugging**: Mengajukan serangkaian *traceback error* (`NameError`, `TypeError`, `FileNotFoundError`) yang muncul selama pengembangan dan meminta penjelasan serta solusi untuk setiap error.
    * **Konseptual**: Mengajukan pertanyaan tentang konsep *deep learning* seperti *overfitting*, interpretasi grafik training, efek mengubah `SEED`, dan pentingnya *early stopping*.
    * **Generasi Laporan**: Meminta untuk dibuatkan draf laporan `README.md` ini berdasarkan hasil dan diskusi yang telah dilakukan.

* **Verifikasi dan Integrasi**:
    * Setiap potongan kode dan fungsi yang diberikan oleh AI (misalnya, fungsi `plot_history`, `visualize_predictions`, dan modifikasi `BasicBlock`) diverifikasi secara manual untuk memastikan kebenarannya dan kesesuaiannya dengan kebutuhan tugas.
    * Penjelasan konseptual dari AI (misalnya, tentang *overfitting*) dibandingkan dengan materi kuliah untuk memastikan pemahaman yang mendalam, bukan sekadar menerima jawaban.
    * Laporan yang digenerasi oleh AI ini diperiksa dan disesuaikan kembali oleh kelompok untuk mencerminkan data dan analisis terbaru dari hasil eksperimen kami.
