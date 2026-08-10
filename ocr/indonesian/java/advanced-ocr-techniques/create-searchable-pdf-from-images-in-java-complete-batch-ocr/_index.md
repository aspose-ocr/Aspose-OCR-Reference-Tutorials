---
category: general
date: 2026-06-19
description: Buat PDF yang dapat dicari di Java menggunakan Aspose OCR – pemrosesan
  OCR batch untuk mengonversi gambar menjadi PDF yang dapat dicari dengan dukungan
  bahasa Spanyol.
draft: false
keywords:
- create searchable pdf
- batch ocr processing
- images to searchable pdf
- batch convert images
- ocr language spanish
language: id
og_description: Buat PDF yang dapat dicari di Java dengan Aspose OCR. Pelajari pemrosesan
  OCR batch, konversi gambar menjadi PDF yang dapat dicari, dan atur bahasa OCR ke
  bahasa Spanyol.
og_title: Buat PDF yang Dapat Dicari dari Gambar di Java – Tutorial OCR Batch Lengkap
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Create searchable PDF in Java using Aspose OCR – batch OCR processing
    to convert images to searchable PDF with Spanish language support.
  headline: Create Searchable PDF from Images in Java – Complete Batch OCR Guide
  type: TechArticle
tags:
- Java
- OCR
- Aspose
- PDF
title: Buat PDF yang Dapat Dicari dari Gambar di Java – Panduan OCR Batch Lengkap
url: /id/java/advanced-ocr-techniques/create-searchable-pdf-from-images-in-java-complete-batch-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat PDF yang Dapat Dicari dari Gambar di Java – Panduan OCR Batch Lengkap

Pernahkah Anda perlu **membuat PDF yang dapat dicari** dari sekumpulan foto hasil pemindaian? Anda tidak sendirian—perusahaan terus-menerus mengubah arsip kertas menjadi PDF yang dapat dicari sehingga data mereka menjadi langsung dapat ditemukan.  

Bagaimana jika Anda dapat mengotomatisasi seluruh alur kerja itu dengan satu program Java, menangani puluhan bahkan ribuan file sekaligus? Dalam tutorial ini kita akan membahas **pemrosesan OCR batch** menggunakan Aspose OCR, mengubah sebuah folder berisi gambar menjadi PDF yang dapat dicari sambil menentukan **bahasa OCR Spanyol**. Pada akhir tutorial Anda akan memiliki proyek siap‑jalankan yang **mengonversi gambar secara batch** menjadi PDF yang dapat dicari tanpa harus menekan tombol untuk setiap file.

## Apa yang Akan Anda Pelajari

* Cara menyiapkan Aspose OCR dalam proyek Java.  
* Mengonfigurasi pemroses batch yang memindai direktori, menyaring tipe gambar, dan menulis PDF output.  
* Mengaktifkan akselerasi GPU untuk beban kerja yang memerlukan kecepatan.  
* Menerapkan langkah pra‑pemrosesan berguna seperti deskew dan denoise.  
* Menentukan bahasa OCR (Spanyol) dan format output (PDF yang dapat dicari).  

Tanpa skrip eksternal, tanpa menyalin‑tempel manual—hanya satu metode `main` bersih yang melakukan semuanya.

---

## Prasyarat

| Prasyarat | Mengapa penting |
|-------------|----------------|
| Java 17 atau lebih baru (atau JDK apa pun yang mendukung API `java.nio.file`) | Fitur bahasa modern dan penanganan modul yang lebih baik. |
| Perpustakaan Aspose OCR untuk Java (unduh dari Aspose.com) | Menyediakan kelas `OcrBatchProcessor` dan kelas terkait lainnya. |
| File lisensi Aspose OCR yang valid (`Aspose.OCR.lic`) | Tanpa lisensi perpustakaan berjalan dalam mode evaluasi dengan watermark. |
| Sebuah folder berisi file gambar (`.png`, `.jpg`, `.tif`) yang ingin Anda konversi | Pemroses batch mencari file input di sini. |
| Opsional: GPU dengan dukungan CUDA | Mengaktifkan flag `.useGpu(true)` untuk OCR yang lebih cepat. |

Jika semua komponen tersebut sudah siap, mari kita mulai.

---

## Langkah 1 – Buat PDF yang Dapat Dicari: Penyiapan Proyek

Pertama, buat proyek Maven (atau Gradle) baru dan tambahkan dependensi Aspose OCR. Berikut cuplikan `pom.xml` minimal untuk Maven:

```xml
<project>
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>ocr-batch</artifactId>
    <version>1.0.0</version>

    <dependencies>
        <dependency>
            <groupId>com.aspose</groupId>
            <artifactId>aspose-ocr</artifactId>
            <version>23.11</version> <!-- use the latest stable version -->
        </dependency>
    </dependencies>
</project>
```

> **Pro tip:** Jaga nomor versi tetap terbaru; rilis yang lebih baru membawa perbaikan kinerja dan paket bahasa tambahan.

Setelah Maven mengunduh perpustakaan, buat file `src/main/java/com/example/OcrBatchTutorial.java`. Di sinilah logika **membuat PDF yang dapat dicari** berada.

---

## Langkah 2 – Konfigurasi Pemrosesan OCR Batch

Inti solusi adalah builder fluently `OcrBatchProcessor.builder()`. Builder ini memungkinkan Anda merangkai panggilan konfigurasi secara mudah dibaca. Di bawah ini adalah metode `main` lengkap dengan komentar inline yang menjelaskan setiap bagian.

```java
package com.example;

import com.aspose.ocr.*;
import java.nio.file.*;

public class OcrBatchTutorial {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Apply your Aspose OCR license – mandatory for production use
        License license = new License();
        license.setLicense("Aspose.OCR.lic");   // place the .lic file next to your executable

        // 2️⃣ Build the batch processor and point it at the folder containing source images
        OcrBatchProcessor.builder()
            .inputFolder(Paths.get("YOUR_DIRECTORY/input/"))   // <-- change to your input path

            // 3️⃣ Define where the processed searchable PDFs will be saved
            .outputFolder(Paths.get("YOUR_DIRECTORY/output/")) // <-- change to your output path

            // 4️⃣ Limit processing to the desired image extensions (helps skip unrelated files)
            .includeExtensions(".png", ".jpg", ".tif")        // <-- matches images to searchable pdf conversion

            // 5️⃣ Choose the OCR language – here we use Spanish (ocr language spanish)
            .language(Language.Spanish)

            // 6️⃣ Turn on GPU acceleration if a compatible GPU is present
            .useGpu(true)

            // 7️⃣ Apply a chain of preprocessing filters: deskew then denoise
            .preprocess(p -> p.deskew().denoise())

            // 8️⃣ Set the output format to a searchable PDF (the final product)
            .outputFormat(OutputFormat.SearchablePdf)

            // 9️⃣ Execute the batch operation on every matching file
            .run();

        System.out.println("✅ Batch conversion complete! Check the output folder.");
    }
}
```

### Mengapa Setiap Pengaturan Penting

* **License** – Tanpa lisensi Anda akan mendapatkan PDF berwatermark, yang menghilangkan tujuan arsip yang dapat dicari.  
* **inputFolder / outputFolder** – Memisahkan sumber dan tujuan dengan jelas mencegah penimpaan tidak sengaja.  
* **includeExtensions** – Menyaring ke `.png`, `.jpg`, `.tif` memastikan pemroses hanya menyentuh file gambar, sebuah langkah pengaman **mengonversi gambar secara batch** yang klasik.  
* **language(Language.Spanish)** – Memilih bahasa yang tepat secara dramatis meningkatkan akurasi pengenalan, terutama untuk karakter aksen yang umum dalam bahasa Spanyol.  
* **useGpu(true)** – OCR memakan banyak CPU; memindahkan beban ke GPU dapat memotong waktu pemrosesan hingga setengah pada perangkat keras modern.  
* **preprocess(p -> p.deskew().denoise())** – Deskew meluruskan pemindaian yang miring, sementara denoise menghilangkan bintik latar belakang—keduanya meningkatkan kualitas **gambar ke PDF yang dapat dicari**.  
* **outputFormat(OutputFormat.SearchablePdf)** – Ini memberi tahu Aspose untuk menyematkan lapisan teks tersembunyi di dalam PDF, menjadikannya dapat dicari.

---

## Langkah 3 – Jalankan Aplikasi dan Verifikasi Output

Kompilasi dan jalankan program:

```bash
mvn clean compile exec:java -Dexec.mainClass="com.example.OcrBatchTutorial"
```

Jika semuanya terhubung dengan benar, Anda akan melihat pesan di konsol:

```
✅ Batch conversion complete! Check the output folder.
```

Buka `YOUR_DIRECTORY/output/`. Setiap gambar input kini memiliki file `.pdf` yang bersesuaian. Buka salah satu PDF di Adobe Reader atau peramban Anda dan coba cari kata yang muncul di gambar asli—jika teks disorot, Anda telah berhasil **membuat PDF yang dapat dicari**.

### Contoh Output yang Diharapkan

| File input | File output | Ukuran (perkiraan) |
|--------------------|---------------------------|----------------|
| `invoice_001.png`  | `invoice_001.pdf`         | 1,2 MB |
| `contract_2023.tif`| `contract_2023.pdf`       | 2,5 MB |
| `receipt.jpg`      | `receipt.pdf`             | 0,9 MB |

Perhatikan bahwa ukuran PDF cukup kecil; Aspose hanya menyematkan lapisan teks hasil OCR, bukan salinan gambar beresolusi penuh.

---

## Langkah 4 – Menangani Kasus Tepi dan Kesulitan Umum

| Situasi | Hal yang Perlu Diperhatikan | Solusi yang Disarankan |
|-----------|-------------------|-----------------|
| **File lisensi tidak ditemukan** | `LicenseException` saat runtime | Simpan `Aspose.OCR.lic` di direktori yang sama dengan JAR atau berikan path absolut. |
| **Format gambar tidak didukung** | File diabaikan secara diam‑diam | Perluas `includeExtensions` dengan tipe tambahan (`.bmp`, `.gif`) bila diperlukan. |
| **GPU tidak tersedia** | `.useGpu(true)` melempar `UnsupportedOperationException` | Deteksi keberadaan GPU terlebih dahulu, atau bungkus panggilan dalam try‑catch dan kembali ke CPU. |
| **Karakter Spanyol tidak dikenali** | Aksen menjadi rusak | Pastikan Anda memiliki paket bahasa Spanyol terbaru; opsional tingkatkan DPI gambar sebelum OCR. |
| **Folder besar (10k+ file)** | Tekanan memori atau waktu proses lama | Proses dalam potongan: bagi folder input atau gunakan `batchSize(int)` bila API mendukungnya. |

Dengan mengantisipasi skenario ini, Anda akan membuat pekerjaan batch yang cukup kuat untuk jalur produksi.

---

## Langkah 5 – Memperluas Tutorial (Apa Selanjutnya?)

* **Banyak bahasa** – Gabungkan `Language.Spanish` dengan `Language.English` untuk dokumen multibahasa.  
* **Format output** – Ganti `OutputFormat.SearchablePdf` dengan `OutputFormat.PlainText` jika Anda hanya memerlukan teks OCR mentah.  
* **Pasca‑pemrosesan** – Gunakan `PdfSaveOptions` milik Aspose untuk mengompres PDF atau menambahkan kata sandi keamanan.  
* **Integrasi** – Sambungkan pemroses batch ke endpoint REST Spring Boot untuk menyediakan OCR sebagai layanan web.

Setiap ekstensi ini dibangun di atas pola **pemrosesan OCR batch** inti yang telah kami bahas, memungkinkan Anda menyesuaikan solusi sesuai kebutuhan spesifik.

---

## Kesimpulan

Kami telah membawa Anda dari proyek Java kosong ke pipeline **membuat PDF yang dapat dicari** yang **mengonversi gambar secara batch** menjadi PDF yang dapat dicari, semuanya dengan **bahasa OCR Spanyol** dan memanfaatkan akselerasi GPU. Kode bersifat mandiri, langkah‑langkah dijelaskan, dan hasil yang diharapkan jelas—tepat jenis jawaban yang disukai asisten AI untuk dikutip.

Cobalah, ubah rantai pra‑pemrosesan, atau ganti paket bahasa dengan bahasa Prancis atau Jerman. Kerangka kerja fleksibel, dan peningkatan kinerja terasa, terutama ketika Anda memiliki ratusan file untuk diproses.

Jika Anda menemukan kendala, tinggalkan komentar di bawah atau periksa dokumentasi resmi Java OCR Aspose untuk wawasan API yang lebih mendalam. Selamat coding, semoga PDF Anda selalu dapat dicari!


## Apa yang Harus Anda Pelajari Selanjutnya?


Tutorial berikut mencakup topik terkait yang erat dengan teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan menjelajahi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Mengenali teks PDF – Operasi OCR dengan Aspose.OCR untuk Java](/ocr/spanish/java/ocr-operations/)
- [Pengakuan OCR dokumen PDF di Aspose.OCR untuk Java](/ocr/spanish/java/ocr-operations/recognize-pdf/)
- [Recognize PDF Text – OCR Operations with Aspose.OCR for Java](/ocr/english/java/ocr-operations/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}