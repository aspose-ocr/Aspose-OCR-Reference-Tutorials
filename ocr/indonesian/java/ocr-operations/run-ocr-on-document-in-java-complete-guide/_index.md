---
category: general
date: 2026-06-16
description: Jalankan OCR pada dokumen menggunakan Java dalam beberapa langkah saja.
  Pelajari cara mengonfigurasi OCR, mengenali teks dari TIFF, dan mengekstrak teks
  dari gambar multi‑halaman.
draft: false
keywords:
- run OCR on document
- how to configure OCR
- recognize text from TIFF
- extract text from multi-page
language: id
og_description: Jalankan OCR pada dokumen dengan Java. Panduan ini menunjukkan cara
  mengonfigurasi OCR, mengenali teks dari file TIFF, dan mengekstrak teks dari gambar
  multi‑halaman.
og_title: Jalankan OCR pada Dokumen di Java – Tutorial Langkah demi Langkah
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Run OCR on document using Java in just a few steps. Learn how to configure
    OCR, recognize text from TIFF, and extract text from multi‑page images.
  headline: Run OCR on Document in Java – Complete Guide
  type: TechArticle
- description: Run OCR on document using Java in just a few steps. Learn how to configure
    OCR, recognize text from TIFF, and extract text from multi‑page images.
  name: Run OCR on Document in Java – Complete Guide
  steps:
  - name: '**Streamed processing** – Some OCR SDKs let you feed pages one‑by‑one instead
      of loading the entire TIFF into memory. Look for methods like `engine.setImageStream(...)`
      that accept an `InputStream`.'
    text: '**Streamed processing** – Some OCR SDKs let you feed pages one‑by‑one instead
      of loading the entire TIFF into memory. Look for methods like `engine.setImageStream(...)`
      that accept an `InputStream`.'
  - name: '**Memory limits** – If you hit `OutOfMemoryError`, lower the thread count
      or increase the JVM heap (`-Xmx2g`).'
    text: '**Memory limits** – If you hit `OutOfMemoryError`, lower the thread count
      or increase the JVM heap (`-Xmx2g`).'
  - name: '**Post‑processing** – Use regex or natural‑language libraries to clean
      up line breaks, remove headers/footers, or extract specific fields (e.g., invoice
      numbers).'
    text: '**Post‑processing** – Use regex or natural‑language libraries to clean
      up line breaks, remove headers/footers, or extract specific fields (e.g., invoice
      numbers).'
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: Jalankan OCR pada Dokumen di Java – Panduan Lengkap
url: /id/java/ocr-operations/run-ocr-on-document-in-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jalankan OCR pada Dokumen di Java – Panduan Lengkap

Pernah perlu **menjalankan OCR pada file dokumen** tetapi tidak yakin harus mulai dari mana? Anda tidak sendirian. Baik Anda mendigitalkan arsip lama atau mengambil data dari formulir yang dipindai, mendapatkan teks yang dapat diandalkan dari gambar adalah titik sakit yang umum.

Dalam tutorial ini kami akan membimbing Anda melalui contoh praktis end‑to‑end yang menunjukkan **cara mengonfigurasi OCR**, **mengenali teks dari TIFF**, dan **mengekstrak teks dari dokumen multi‑halaman**—semua dengan hanya beberapa baris Java. Tanpa basa‑basi, hanya solusi yang dapat langsung Anda gunakan dalam proyek hari ini.

## Apa yang Akan Anda Pelajari

- Menyiapkan instance mesin OCR di Java  
- Memuat gambar TIFF multi‑halaman untuk diproses  
- Mengoptimalkan mesin dengan mengonfigurasi jumlah thread (bagian “cara mengonfigurasi OCR”)  
- Melakukan pengenalan dan mengeluarkan teks yang diekstrak  
- Menangani kasus tepi seperti file besar dan batas memori  

Pada akhir panduan ini Anda akan dapat **menjalankan OCR pada gambar dokumen** dengan percaya diri, dan Anda akan memiliki fondasi yang kuat untuk memperluas solusi ke PDF, PNG, atau bahkan aliran kamera langsung.

## Prasyarat

- Java 17 atau lebih baru (kode menggunakan kata kunci `var` untuk singkat)  
- Sebuah perpustakaan OCR yang menyediakan kelas `OcrEngine` (misalnya *Aspose.OCR for Java* atau pembungkus *Tesseract‑Java*).  
- Sebuah file TIFF multi‑halaman bernama `multi_page.tif` yang ditempatkan di direktori yang diketahui.  

Jika Anda belum memiliki perpustakaan OCR, tambahkan ke `pom.xml` (Maven) atau `build.gradle` (Gradle) – koordinat tepatnya tergantung pada vendor, tetapi kebanyakan menyediakan satu JAR yang dapat Anda referensikan.

---

## Langkah 1: Inisialisasi Mesin OCR – Cara Menjalankan OCR pada Dokumen

Hal pertama yang perlu dilakukan: Anda memerlukan objek mesin yang akan melakukan pekerjaan berat. Anggap saja sebagai otak di balik operasi.

```java
import com.example.ocr.OcrEngine;   // Replace with your actual package
import com.example.ocr.ImageStream;
import com.example.ocr.OcrResult;

public class OcrDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine instance
        OcrEngine engine = new OcrEngine();
```

> **Mengapa ini penting:** `OcrEngine` menyatukan semua pengaturan pengenalan, paket bahasa, dan opsi pemanfaatan perangkat keras. Membuatnya sekali dan menggunakannya kembali untuk banyak gambar lebih efisien daripada membuatnya berulang‑ulang.

---

## Langkah 2: Muat TIFF Multi‑Halaman – Ekstrak Teks dari Gambar Multi‑Halaman

Sekarang kita mengarahkan mesin ke file yang ingin diproses. TIFF adalah format umum untuk dokumen yang dipindai karena dapat menyimpan beberapa halaman dalam satu file.

```java
        // Step 2: Load the multi‑page image to be processed
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/multi_page.tif"));
```

> **Tip profesional:** Jika TIFF Anda berada di share jaringan, gunakan `ImageStream.fromUrl(...)` sebagai gantinya. Ini menghindari penyalinan seluruh file ke memori sebelum OCR dimulai.

---

## Langkah 3: Cara Mengonfigurasi OCR untuk Throughput Maksimum

Secara default, perpustakaan OCR biasanya berjalan pada satu thread, yang dapat menjadi bottleneck pada mesin multi‑core modern. Di sinilah kami menjawab bagian “**cara mengonfigurasi OCR**” dari teka‑teki.

```java
        // Step 3: Configure the engine to use all available CPU cores
        int availableCores = Runtime.getRuntime().availableProcessors();
        engine.getRecognitionSettings().setThreadCount(availableCores);
```

> **Mengapa ini berhasil:** Dengan menyamakan jumlah thread dengan jumlah prosesor logis, mesin OCR dapat memproses halaman yang berbeda secara paralel. Pada laptop 4‑core Anda akan melihat peningkatan kecepatan kira‑kira 3‑4× saat menangani dokumen multi‑halaman.  
> **Kasus tepi:** Beberapa lingkungan (misalnya kontainer Docker dengan kuota CPU terbatas) melaporkan lebih banyak core daripada yang diizinkan untuk digunakan. Dalam kasus seperti itu, batasi jumlah thread secara manual: `engine.getRecognitionSettings().setThreadCount(Math.min(availableCores, 2));`

---

## Langkah 4: Kenali Teks dari TIFF – Panggilan OCR Inti

Setelah semuanya terhubung, saatnya menjalankan pengenalan. Panggilan tunggal ini akan mengiterasi setiap halaman TIFF, menerapkan model bahasa, dan mengembalikan hasil gabungan.

```java
        // Step 4: Perform the OCR recognition
        OcrResult result = engine.recognize();
```

> **Apa yang terjadi di balik layar?** Mesin memecah TIFF menjadi gambar raster individual, memberi masing‑masing ke jaringan saraf OCR, dan menyatukan output teks. Jika Anda memerlukan granularitas per halaman, `result.getPages()` akan memberikan daftar objek `OcrPageResult`.

---

## Langkah 5: Keluarkan Teks yang Diakui – Verifikasi Ekstraksi

Akhirnya, kami mencetak teks yang diekstrak ke konsol. Dalam aplikasi dunia nyata Anda mungkin akan menuliskannya ke basis data atau file JSON.

```java
        // Step 5: Output the recognized text
        System.out.println(result.getText());
    }
}
```

**Output yang diharapkan (dipotong):**

```
Page 1:
Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00

Page 2:
Terms and Conditions...
```

Jika Anda melihat karakter acak alih‑alih teks bersih, periksa kembali bahwa paket bahasa yang tepat telah terpasang dan gambar tidak terlalu berisik. Langkah pra‑pemrosesan seperti deskewing atau binarisasi dapat secara dramatis meningkatkan akurasi.

---

## Menangani File Multi‑Halaman Besar – Tips untuk Ekstraksi

Meskipun alur dasar sudah kami tunjukkan, dokumen dunia nyata dapat sangat besar. Berikut beberapa pertimbangan tambahan:

1. **Pemrosesan streaming** – Beberapa SDK OCR memungkinkan Anda memberi halaman satu per satu alih‑alih memuat seluruh TIFF ke memori. Cari metode seperti `engine.setImageStream(...)` yang menerima `InputStream`.  
2. **Batas memori** – Jika Anda menemui `OutOfMemoryError`, kurangi jumlah thread atau tingkatkan heap JVM (`-Xmx2g`).  
3. **Pasca‑pemrosesan** – Gunakan regex atau perpustakaan bahasa alami untuk membersihkan pemenggalan baris, menghapus header/footer, atau mengekstrak bidang spesifik (misalnya nomor faktur).

---

## Contoh Lengkap yang Siap Pakai (Semua Langkah Digabung)

Berikut adalah kelas Java lengkap yang siap dijalankan. Tempelkan ke IDE Anda, sesuaikan paket/impor, dan jalankan.

```java
package com.example.ocrdemo;

import com.example.ocr.OcrEngine;
import com.example.ocr.ImageStream;
import com.example.ocr.OcrResult;

/**
 * Demonstrates how to run OCR on document images, configure the engine,
 * recognize text from TIFF files, and extract text from multi‑page documents.
 */
public class OcrDemo {
    public static void main(String[] args) throws Exception {
        // Create the OCR engine instance
        OcrEngine engine = new OcrEngine();

        // Load the multi‑page TIFF image
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/multi_page.tif"));

        // Configure the engine to use all CPU cores (how to configure OCR)
        int cores = Runtime.getRuntime().availableProcessors();
        engine.getRecognitionSettings().setThreadCount(cores);

        // Perform recognition (recognize text from TIFF)
        OcrResult result = engine.recognize();

        // Output the extracted text (extract text from multi‑page)
        System.out.println(result.getText());
    }
}
```

> **Tip profesional:** Bungkus panggilan `recognize()` dalam blok `try‑catch` untuk menangani `OcrException` secara elegan, terutama saat berhadapan dengan file gambar yang rusak.

---

## Kesimpulan

Kami baru saja menunjukkan cara **menjalankan OCR pada gambar dokumen** menggunakan Java, mencakup semua hal mulai dari inisialisasi mesin hingga ekstraksi teks multi‑halaman. Dengan memahami **cara mengonfigurasi OCR**, Anda dapat memaksimalkan kinerja CPU modern, sementara langkah‑langkah untuk **mengenali teks dari TIFF** dan **mengekstrak teks dari multi‑page** memberi Anda dasar yang kuat untuk proyek digitalisasi dokumen apa pun.

Apa selanjutnya? Coba ganti TIFF dengan PDF, bereksperimen dengan model bahasa khusus, atau alirkan output ke indeks pencarian. Langit adalah batasnya setelah Anda memiliki fondasi ini.

Jika Anda menemui kendala—misalnya perpustakaan OCR yang Anda pilih menggunakan API berbeda—tinggalkan komentar di bawah. Selamat coding, dan nikmati mengubah halaman yang dipindai menjadi teks yang dapat dicari!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Extract Text Images – OCR Basics with Aspose.OCR for Java](/ocr/english/java/ocr-basics/)
- [How to recognize tiff with Aspose.OCR for Java](/ocr/english/java/ocr-operations/recognize-tiff/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}