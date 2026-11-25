---
category: general
date: 2026-08-12
description: Mengenali teks dari gambar menggunakan mesin OCR Java. Pelajari cara
  mengekstrak teks dari gambar, meningkatkan akurasi OCR, dan melakukan pra‑pemrosesan
  gambar untuk OCR pada file PNG.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- recognize text from image
- how to extract text from image
- how to improve OCR accuracy
- how to preprocess image for OCR
- perform OCR on PNG
language: id
lastmod: 2026-08-12
og_description: Mengenali teks dari gambar dengan Java. Tutorial ini menunjukkan cara
  mengekstrak teks dari gambar, meningkatkan akurasi OCR, dan melakukan OCR pada PNG
  menggunakan multi‑threading dan GPU.
og_image_alt: Diagram showing Java OCR engine recognizing text from image
og_title: Mengenali teks dari gambar di Java – tutorial OCR langkah demi langkah
schemas:
- author: Aspose
  dateModified: '2026-08-12'
  description: recognize text from image using Java OCR engine. Learn how to extract
    text from image, improve OCR accuracy, and preprocess image for OCR on PNG files.
  headline: recognize text from image in Java – complete OCR guide
  type: TechArticle
- description: recognize text from image using Java OCR engine. Learn how to extract
    text from image, improve OCR accuracy, and preprocess image for OCR on PNG files.
  name: recognize text from image in Java – complete OCR guide
  steps:
  - name: Explanation of each step
    text: '| Step | Why it matters | How it helps you **recognize text from image**
      | |------|----------------|-----------------------------------------------|
      | 1️⃣ Create the OCR engine | Instantiates the core component that drives all
      subsequent operations. | Provides the entry point for all OCR actions. | '
  - name: Expected output
    text: 'If `sample-image.png` contains the sentence “Hello, world! 123”, the console
      will display something similar to:'
  - name: 1. Binarization with Otsu’s method
    text: '```java import java.awt.image.BufferedImage; import com.example.image.Binarizer;
      // hypothetical helper class'
  - name: 2. Scaling to 300 dpi
    text: '```java import com.example.image.Resizer;'
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: Mengenali teks dari gambar di Java – panduan OCR lengkap
url: /id/java/advanced-ocr-techniques/recognize-text-from-image-in-java-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# mengenali teks dari gambar di Java – panduan OCR lengkap

Jika Anda perlu **mengenali teks dari gambar** dalam aplikasi Java, tutorial ini menunjukkan secara tepat caranya. Pada akhir panduan Anda akan dapat mengekstrak teks dari file gambar, meningkatkan akurasi OCR, dan menjalankan OCR pada aset PNG dengan dukungan multi‑core dan GPU.

Banyak pengembang bertanya-tanya **bagaimana mengekstrak teks dari gambar** tanpa menulis jaringan saraf khusus. Solusinya adalah menggunakan mesin OCR yang terbukti, mengkonfigurasinya untuk kecepatan dan akurasi, serta menerapkan langkah pra‑pemrosesan yang tepat. Bagian‑bagian berikut akan memandu Anda melalui setiap persyaratan, sehingga Anda dapat menyalin kode langsung ke dalam proyek Anda.

## Apa yang akan Anda pelajari

* Menyiapkan mesin OCR di Java.  
* Mengaktifkan multi‑threading dan akselerasi GPU opsional.  
* Menambahkan paket bahasa untuk Bahasa Inggris dan Spanyol.  
* Menerapkan filter pra‑pemrosesan gambar untuk meningkatkan kualitas pengenalan.  
* Mengaktifkan korektor ejaan bawaan untuk output yang lebih bersih.  
* Melakukan OCR pada file PNG dan mencetak teks yang dikenali.  

Tidak ada layanan eksternal yang diperlukan—semua berjalan secara lokal, menjadikannya ideal untuk aplikasi offline atau yang sensitif terhadap privasi.

## Prasyarat

* Java 17 atau lebih baru (kode menggunakan sintaks `var` modern tetapi dapat dipindahkan kembali).  
* Pustaka OCR yang menyediakan kelas `OcrEngine`, `Language`, dan `EngineOptions` (misalnya **GroupDocs.Parser**, **Aspose.OCR**, atau SDK kompatibel apa pun).  
* Maven atau Gradle untuk manajemen dependensi.  
* Sebuah gambar PNG contoh (`sample-image.png`) ditempatkan di `YOUR_DIRECTORY`.  

> **Pro tip:** Jika Anda berencana memproses ribuan gambar, alokasikan RAM yang cukup untuk buffer GPU dan nonaktifkan korektor ejaan hanya ketika Anda membutuhkan output OCR mentah.

## mengenali teks dari gambar dengan mesin OCR Java

Berikut adalah program Java lengkap yang dapat dijalankan dan mengikuti delapan langkah yang ditunjukkan dalam cuplikan asli. Program ini mencakup impor, metode `main`, dan komentar inline yang menjelaskan tujuan setiap baris.

```java
// File: OcrDemo.java
import com.example.ocr.OcrEngine;            // Replace with your OCR library's package
import com.example.ocr.Language;
import com.example.ocr.EngineOptions;
import com.example.ocr.ImagePreprocessingOptions;

public class OcrDemo {

    public static void main(String[] args) {
        // Step 1: Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Enable multi‑core processing for faster throughput
        ocrEngine.getEngineOptions().setUseMultiThreading(true);

        // Step 3: (Optional) Turn on GPU acceleration if a compatible GPU is present
        ocrEngine.getEngineOptions().setUseGpu(true);

        // Step 4: Add the languages you want to recognize (English and Spanish)
        ocrEngine.getLanguage().add(Language.English);
        ocrEngine.getLanguage().add(Language.Spanish);

        // Step 5: Apply common image‑preprocessing filters to improve OCR accuracy
        ImagePreprocessingOptions imgOpts = ocrEngine.getImagePreprocessingOptions();
        imgOpts.setRotate(true);   // Auto‑rotate based on EXIF orientation
        imgOpts.setDeskew(true);   // Straighten skewed text lines
        imgOpts.setDenoise(true);  // Reduce background noise

        // Step 6: Enable the built‑in spell corrector for cleaner output
        ocrEngine.getEngineOptions().setUseSpellCorrector(true);

        // Step 7: Perform OCR on the target PNG image
        // This demonstrates how to perform OCR on PNG files efficiently.
        String imagePath = "YOUR_DIRECTORY/sample-image.png";
        String ocrResult = ocrEngine.recognizeImage(imagePath);

        // Step 8: Output the recognized text
        System.out.println("=== OCR Result ===");
        System.out.println(ocrResult);
    }
}
```

### Penjelasan setiap langkah

| Langkah | Mengapa penting | Bagaimana membantu Anda **mengenali teks dari gambar** |
|---------|----------------|--------------------------------------------------------|
| 1️⃣ Membuat mesin OCR | Membuat instance komponen inti yang mengendalikan semua operasi selanjutnya. | Menyediakan titik masuk untuk semua aksi OCR. |
| 2️⃣ Mengaktifkan pemrosesan multi‑core | CPU modern memiliki banyak core; memanfaatkannya mengurangi total waktu pemrosesan. | Mempercepat pekerjaan batch ketika Anda **melakukan OCR pada file PNG** secara paralel. |
| 3️⃣ Mengaktifkan akselerasi GPU (opsional) | GPU unggul dalam operasi piksel paralel, terutama untuk gambar besar. | Dapat mengurangi waktu pengenalan hingga 70 % pada perangkat keras yang mendukung. |
| 4️⃣ Menambahkan paket bahasa | Akurasi OCR bergantung pada model bahasa; menentukan hanya bahasa yang diperlukan mengurangi false positive. | Meningkatkan peluang mengidentifikasi karakter dengan benar ketika Anda **mengekstrak teks dari gambar** dalam skenario multibahasa. |
| 5️⃣ Pra‑pemrosesan gambar | Rotasi, perbaikan kemiringan, dan pengurangan noise memperbaiki masalah pemindaian umum. | Secara langsung **meningkatkan akurasi OCR** dengan menyajikan bitmap yang lebih bersih ke mesin. |
| 6️⃣ Korektor ejaan | Langkah pasca‑pemrosesan yang memperbaiki kesalahan ejaan OCR umum. | Menghasilkan output yang lebih dapat dibaca tanpa pembersihan manual. |
| 7️⃣ Melakukan OCR pada PNG | Metode `recognizeImage` membaca file, menerapkan pra‑pemrosesan, dan menjalankan pipeline pengenalan. | Mendemonstrasikan **melakukan OCR pada PNG** sambil menangani keanehan spesifik format (mis., kompresi lossless). |
| 8️⃣ Mencetak hasil | Memberikan umpan balik langsung untuk memverifikasi keberhasilan. | Memungkinkan Anda mengonfirmasi bahwa teks telah **dikenali dari gambar** dengan benar. |

### Output yang diharapkan

Jika `sample-image.png` berisi kalimat “Hello, world! 123”, konsol akan menampilkan sesuatu yang mirip dengan:

```
=== OCR Result ===
Hello, world! 123
```

Output yang tepat mungkin sedikit berbeda tergantung pada kualitas gambar dan pengaturan bahasa, tetapi korektor ejaan biasanya akan memperbaiki kesalahan pengenalan kecil seperti “Helli” → “Hello”.

## cara pra‑memproses gambar untuk OCR – penjelasan mendalam

Meskipun kode di atas menggunakan pra‑pemrosesan bawaan mesin, Anda juga dapat menerapkan filter khusus sebelum menyerahkan gambar ke mesin OCR. Berikut dua teknik umum:

### 1. Binarisasi dengan metode Otsu

```java
import java.awt.image.BufferedImage;
import com.example.image.Binarizer; // hypothetical helper class

BufferedImage original = ImageIO.read(new File(imagePath));
BufferedImage binary = Binarizer.otsuThreshold(original);
ocrEngine.recognizeImage(binary);
```

Binarisasi mengubah gambar menjadi hitam‑putih, yang sering **meningkatkan akurasi OCR** untuk pemindaian berkontras rendah.

### 2. Skalasi ke 300 dpi

```java
import com.example.image.Resizer;

BufferedImage scaled = Resizer.scaleToDPI(original, 300);
ocrEngine.recognizeImage(scaled);
```

Sebagian besar mesin OCR mengharapkan setidaknya 300 dpi untuk pengenalan karakter yang optimal. Skalasi mencegah mesin membaca glyph kecil secara salah.

> **Catatan:** Jika Anda mengaktifkan pra‑pemrosesan khusus dan opsi bawaan mesin, mesin akan menerapkan filternya *setelah* filter Anda. Pilih urutan yang paling cocok dengan karakteristik gambar Anda.

## cara mengekstrak teks dari gambar – menangani kasus tepi

| Situasi | Penyesuaian yang disarankan |
|---------|-----------------------------|
| **Latar belakang sangat berisik** | Tingkatkan intensitas `setDenoise(true)` atau jalankan filter median sebelum OCR. |
| **Kemiringan > 15°** | Gunakan `setDeskew(true)` *dan* berikan sudut rotasi manual melalui `imgOpts.setRotateAngle(θ)`. |
| **Bahasa campuran (mis., Inggris + Spanyol)** | Tambahkan kedua paket bahasa seperti yang ditunjukkan pada Langkah 4; mesin akan beralih konteks secara otomatis. |
| **PDF besar yang dikonversi ke PNG** | Proses setiap halaman sebagai PNG terpisah dan gabungkan hasilnya; multi‑threading (Langkah 2) akan menjaga total waktu tetap rendah. |
| **GPU tidak tersedia** | Pertahankan `setUseGpu(true)` tetapi bungkus dalam try‑catch; mesin akan kembali ke CPU tanpa crash. |

## melakukan OCR pada PNG – contoh pemrosesan batch

Ketika Anda perlu **melakukan OCR pada PNG** di seluruh direktori, loop sederhana dengan instance mesin yang sama bekerja dengan baik:

```java
Path dir = Paths.get("YOUR_DIRECTORY");
try (Stream<Path> files = Files.list(dir)) {
    files.filter(p -> p.toString().endsWith(".png"))
         .forEach(p -> {
             String text = ocrEngine.recognizeImage(p.toString());
             System.out.println("File: " + p.getFileName());
             System.out.println(text);
             System.out.println("---");
         });
}
```

Karena mesin sudah dikonfigurasi untuk multi‑core dan GPU, loop ini dapat memproses puluhan gambar secara paralel tanpa kode tambahan.

## Contoh kerja lengkap

Menggabungkan semua komponen, berikut kelas mandiri yang dapat Anda salin‑tempel ke IDE, tambahkan dependensi Maven yang tepat, dan jalankan segera:



## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Cara OCR Teks Gambar dengan Bahasa Menggunakan Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Ekstrak Teks dari Gambar Java dengan Mode Deteksi Area Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [gambar ke teks java: Konversi Gambar ke Teks dengan Aspose.OCR](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}