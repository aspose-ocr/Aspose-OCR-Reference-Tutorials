---
category: general
date: 2026-05-31
description: Pra‑proses gambar untuk OCR guna secara dramatis meningkatkan akurasi
  OCR dengan pra‑pemrosesan menggunakan Aspose OCR Java. Ikuti panduan lengkap langkah
  demi langkah.
draft: false
keywords:
- preprocess image for OCR
- improve OCR accuracy with preprocessing
language: id
og_description: Pra-proses gambar untuk OCR dan pelajari cara meningkatkan akurasi
  OCR dengan pra-pemrosesan di Java menggunakan Aspose OCR.
og_title: Pra-proses Gambar untuk OCR – Tingkatkan Akurasi dengan Pra-pemrosesan
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Preprocess image for OCR to dramatically improve OCR accuracy with
    preprocessing using Aspose OCR Java. Follow a complete step‑by‑step guide.
  headline: Preprocess Image for OCR – Boost Accuracy with Preprocessing
  type: TechArticle
- description: Preprocess image for OCR to dramatically improve OCR accuracy with
    preprocessing using Aspose OCR Java. Follow a complete step‑by‑step guide.
  name: Preprocess Image for OCR – Boost Accuracy with Preprocessing
  steps:
  - name: Loads the original PNG.
    text: Loads the original PNG.
  - name: Feeds it through `AutoDeskew`, `DenoiseMedian`, and `ContrastStretch`.
    text: Feeds it through `AutoDeskew`, `DenoiseMedian`, and `ContrastStretch`.
  - name: Runs the recognizer on the cleaned bitmap.
    text: Runs the recognizer on the cleaned bitmap.
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: Pra-proses Gambar untuk OCR – Tingkatkan Akurasi dengan Pra-pemrosesan
url: /id/java/advanced-ocr-techniques/preprocess-image-for-ocr-boost-accuracy-with-preprocessing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Pra-proses Gambar untuk OCR – Tingkatkan Akurasi dengan Pra-pemrosesan

Pernah bertanya-tanya mengapa hasil OCR Anda terlihat seperti kekacauan meskipun gambar sumber tampak baik? Dalam kebanyakan kasus penyebabnya tersembunyi di dalam gambar—kemiringan, noise, kontras rendah—hal-hal yang mengacaukan bahkan pengenalan paling pintar. **Preprocess image for OCR** dan Anda akan melihat lonjakan dramatis dalam kualitas.  

Dalam tutorial ini kami tidak hanya akan menunjukkan cara pra-proses gambar untuk OCR, tetapi juga menjelaskan **how to improve OCR accuracy with preprocessing** dengan membangun pipeline kecil namun kuat menggunakan Aspose OCR untuk Java. Pada akhir tutorial Anda akan memiliki program siap‑jalankan yang mengubah PNG berisik dan miring menjadi teks bersih dan dapat dibaca.

## Apa yang Akan Anda Pelajari

- Mengapa pra-pemrosesan penting untuk mesin OCR  
- Cara menyiapkan Aspose OCR dalam proyek Java  
- Kode langkah‑demi‑langkah yang **preprocesses image for OCR** menggunakan filter deskew, denoise, dan contrast  
- Tips untuk menyesuaikan pipeline agar **improve OCR accuracy with preprocessing** pada dataset Anda sendiri  

Tanpa basa‑basi, hanya contoh lengkap yang dapat dijalankan dan penjelasan di balik setiap baris.

## Prasyarat

| Requirement | Reason |
|-------------|--------|
| Java 8 atau lebih baru | Perpustakaan Aspose OCR Java menargetkan Java 8+ |
| Maven atau Gradle (opsional) | Menyederhanakan penambahan dependensi Aspose OCR |
| File lisensi Aspose OCR untuk Java (`Aspose.OCR.Java.lic`) | Diperlukan untuk membuka semua fungsi |
| Contoh gambar (misalnya `noisy_skewed.png`) | Gambar yang akan Anda *preprocess image for OCR* |

Jika ada yang belum tersedia, berhentilah sejenak dan selesaikan—mencoba menjalankan kode tanpa lisensi hanya akan menghasilkan pengecualian.

## Langkah 1: Terapkan Lisensi Aspose OCR Anda

Hal pertama yang harus dilakukan. Mesin OCR tidak akan melakukan apa pun yang berguna tanpa lisensi yang valid. Langkah ini **preprocesses image for OCR** secara tidak langsung dengan membuka seluruh set filter gambar.

```java
import com.aspose.ocr.*;

public class PreprocessDemo {
    public static void main(String[] args) throws Exception {
        // Apply your Aspose OCR license
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.Java.lic");
```

> **Pro tip:** Simpan file lisensi di luar kontrol versi. Gunakan variabel lingkungan atau brankas aman di produksi.

## Langkah 2: Inisialisasi Mesin OCR dan Muat Gambar Sumber

Sekarang kami membuat mesin, memberi tahu bahasa yang diharapkan, dan menunjuk ke file yang ingin kami *preprocess image for OCR*.

```java
        // Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Set the language – English works for most demos
        ocrEngine.setLanguage(OcrLanguage.ENGLISH);

        // Load the source image (the one that needs preprocessing)
        ocrEngine.setImage(new OcrImage("YOUR_DIRECTORY/noisy_skewed.png"));
```

Mengapa mengatur bahasa? Karena mesin dapat menerapkan heuristik khusus bahasa, yang sudah **improve OCR accuracy with preprocessing** sebelum kami menyentuh filter apa pun.

## Langkah 3: Bangun Pipeline Pra-pemrosesan

Ini adalah inti dari tutorial. Di sini kami **preprocess image for OCR** dengan menggabungkan tiga filter:

| Filter | Apa yang dilakukannya | Mengapa penting untuk akurasi |
|--------|-----------------------|------------------------------|
| `AutoDeskew` | Mendeteksi dan memperbaiki rotasi | Baris teks yang miring membingungkan segmentasi karakter |
| `DenoiseMedian(3)` | Reduksi noise dengan median‑filter (kernel = 3) | Menghapus bintik yang tampak seperti karakter asing |
| `ContrastStretch` | Meregangkan histogram untuk meningkatkan kontras | Latar belakang gelap menjadi dapat dibaca, teks terang menonjol |

```java
        // Access the preprocessor
        OcrPreprocessor preprocessor = ocrEngine.getPreprocessor();

        // 1️⃣ Correct image skew
        preprocessor.addFilter(new AutoDeskew());

        // 2️⃣ Reduce noise with a median filter (kernel size = 3)
        preprocessor.addFilter(new DenoiseMedian(3));

        // 3️⃣ Enhance contrast for sharper edges
        preprocessor.addFilter(new ContrastStretch());
```

Perhatikan bahwa kami tidak perlu menulis kode pemrosesan gambar dari awal—Aspose menyediakan filter siap pakai. Ini secara dramatis **improves OCR accuracy with preprocessing** sambil menjaga implementasi tetap singkat.

## Langkah 4: Jalankan OCR pada Gambar yang Telah Dipra‑proses

Dengan pipeline yang sudah ada, mesin secara otomatis menerapkan filter sebelum pengenalan. Yang Anda butuhkan hanya satu panggilan:

```java
        // Perform OCR on the pre‑processed image
        String extractedText = ocrEngine.recognize();
```

Di balik layar mesin:

1. Memuat PNG asli.  
2. Mengirimnya melalui `AutoDeskew`, `DenoiseMedian`, dan `ContrastStretch`.  
3. Menjalankan pengenalan pada bitmap yang sudah dibersihkan.  

Itulah keajaiban **preprocess image for OCR**—pekerjaan berat diabstraksikan.

## Langkah 5: Keluarkan Teks yang Dikenali

Akhirnya, cetak hasil ke konsol atau tulis ke file. Untuk tujuan demo, `System.out.println` sederhana sudah cukup.

```java
        // Show the extracted text
        System.out.println(extractedText);
    }
}
```

Jika semuanya berjalan lancar, Anda akan melihat kalimat bersih dan dapat dibaca alih‑alih kekacauan. Output tepatnya tergantung pada gambar sumber, tetapi Anda akan melihat peningkatan yang jelas dibandingkan menjalankan OCR pada file mentah.

### Output yang Diharapkan (contoh)

```
The quick brown fox jumps over the lazy dog.
This is a sample text line for OCR testing.
```

Jika Anda masih mendapatkan karakter aneh, periksa kembali urutan filter—kadang menerapkan `ContrastStretch` *sebelum* `DenoiseMedian` menghasilkan hasil yang lebih baik pada pemindaian yang sangat terdegradasi.

## Memvisualisasikan Pipeline (Opsional)

Di bawah ini adalah skema bagaimana gambar mengalir melalui setiap filter. Ini dapat membantu Anda menjelaskan proses kepada rekan tim atau menyematkannya dalam dokumentasi.

![diagram pipeline preprocess image for OCR](pipeline.png "Diagram yang menunjukkan tahap AutoDeskew → DenoiseMedian → ContrastStretch untuk preprocess image for OCR")

*Alt text:* *diagram preprocess image for OCR yang menggambarkan tiga filter yang diterapkan sebelum pengenalan.*

## Kesalahan Umum & Cara Memperbaikinya

| Gejala | Penyebab Kemungkinan | Perbaikan |
|---------|----------------------|-----------|
| Teks masih buram setelah pra-pemrosesan | Filter kontras tidak cukup kuat | Tingkatkan faktor stretch atau coba `HistogramEqualization` |
| OCR melempar `NullPointerException` | Path file lisensi salah | Verifikasi path dan pastikan file dapat dibaca |
| Kemiringan masih ada | Rotasi gambar > 15° (batas AutoDeskew) | Pra‑rotasi secara manual menggunakan `AffineTransform` sebelum pipeline |
| Terlalu banyak positif palsu | Tingkat noise tinggi, ukuran kernel terlalu kecil | Tingkatkan kernel median (misalnya `new DenoiseMedian(5)`) |

Dengan mengantisipasi masalah ini Anda akan **improve OCR accuracy with preprocessing** bahkan pada pemindaian yang paling sulit.

## Memperluas Pipeline

Ingin kontrol lebih? Aspose OCR memungkinkan Anda menambahkan filter khusus atau mengubah urutan filter yang ada. Berikut beberapa ide:

- **Binarization**: `preprocessor.addFilter(new BinarizeOtsu());` – memaksa menjadi hitam‑putih murni, berguna untuk dokumen cetak.  
- **Resize**: `preprocessor.addFilter(new Scale(2.0));` – memperbesar gambar beresolusi rendah, sering meningkatkan akurasi.  
- **Sharpen**: `preprocessor.addFilter(new Sharpen());` – menonjolkan tepi untuk font kecil.  

Ingat, setiap filter tambahan menambah waktu pemrosesan, jadi lakukan benchmark pada perangkat keras target Anda.

## Kode Sumber Lengkap (Siap Salin‑Tempel)

```java
import com.aspose.ocr.*;

public class PreprocessDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Apply your Aspose OCR license
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.Java.lic");

        // Step 2: Create the OCR engine and configure language & source image
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setLanguage(OcrLanguage.ENGLISH);
        ocrEngine.setImage(new OcrImage("YOUR_DIRECTORY/noisy_skewed.png"));

        // Step 3: Build a preprocessing pipeline to improve OCR accuracy with preprocessing
        OcrPreprocessor preprocessor = ocrEngine.getPreprocessor();
        preprocessor.addFilter(new AutoDeskew());               // Correct image skew
        preprocessor.addFilter(new DenoiseMedian(3));           // Reduce noise (kernel size = 3)
        preprocessor.addFilter(new ContrastStretch());         // Enhance contrast

        // Step 4: Perform OCR on the pre‑processed image
        String extractedText = ocrEngine.recognize();

        // Step 5: Output the recognized text
        System.out.println(extractedText);
    }
}
```

Simpan ini sebagai `PreprocessDemo.java`, tambahkan Aspose OCR JAR ke classpath Anda (atau deklarasikan di Maven), dan jalankan:



## Apa yang Harus Anda Pelajari Selanjutnya?

- [Cara OCR Teks Gambar dengan Bahasa Menggunakan Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Ekstrak Teks dari Gambar Java dengan Aspose.OCR Mode Deteksi Area](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Cara menghitung sudut kemiringan java menggunakan Aspose.OCR](/ocr/english/java/ocr-basics/calculate-skew-angle/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}