---
category: general
date: 2026-06-06
description: Ekstrak teks dari gambar yang dipindai menggunakan Aspose OCR untuk Java.
  Pelajari cara mengenali teks dari file TIFF dengan pemrosesan paralel.
draft: false
keywords:
- extract text from scanned image
- recognize text from tiff
- Aspose OCR Java tutorial
- parallel OCR processing
- Java image recognition
language: id
og_description: Ekstrak teks dari gambar yang dipindai dengan Aspose OCR. Panduan
  ini menunjukkan cara mengenali teks dari file TIFF secara efisien menggunakan Java.
og_title: Ekstrak Teks dari Gambar Pindai – Tutorial Aspose OCR Java
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Extract text from scanned image using Aspose OCR for Java. Learn how
    to recognize text from tiff files with parallel processing.
  headline: Extract Text from Scanned Image in Java – Complete Aspose OCR Guide
  type: TechArticle
- description: Extract text from scanned image using Aspose OCR for Java. Learn how
    to recognize text from tiff files with parallel processing.
  name: Extract Text from Scanned Image in Java – Complete Aspose OCR Guide
  steps:
  - name: Maven users
    text: 'Add the following dependency to your `pom.xml`:'
  - name: Manual JAR setup
    text: Download the latest `aspose-ocr-xx.jar` from the Aspose website and place
      it on your classpath.
  - name: Expected Output
    text: '``` === Extracted Text === Invoice Number: 12345 Date: 2024‑05‑01 Total:
      $1,250.00 ... ```'
  - name: What’s Next?
    text: '- **Batch processing**: Loop over a directory of TIFFs, store each result
      in its own file. - **Integrate with Elasticsearch**: Index the extracted text
      for fast full‑text search. - **Add language detection**: Use `OcrLanguage.AutoDetect`
      for multi‑lingual documents.'
  type: HowTo
- questions:
  - answer: Absolutely. `OcrInputImage` accepts any format that Java’s ImageIO can
      read. Just replace the file extension in the path.
    question: Does this work with PNG or JPEG files?
  - answer: You could, but remember other services may need CPU cycles. A good rule
      of thumb is “total cores – 1” for dedicated OCR workers.
    question: My server has 8 cores—should I set `setMaxThreads(8)`?
  - answer: 'Check that the image isn’t completely white, that you set the correct
      language, and that the resolution is at least 200 DPI. Low‑quality scans often
      need pre‑processing (deskew, contrast boost) before feeding them to Aspose OCR.
      --- ## Wrap‑Up We’ve just **extracted text from scanned image** files u'
    question: What if the OCR result is empty?
  type: FAQPage
tags:
- Java
- OCR
- Aspose
- Image Processing
title: Ekstrak Teks dari Gambar Pindai di Java – Panduan Lengkap Aspose OCR
url: /id/java/advanced-ocr-techniques/extract-text-from-scanned-image-in-java-complete-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ekstrak Teks dari Gambar yang Dipindai – Panduan Lengkap Aspose OCR

Pernah membutuhkan untuk **mengekstrak teks dari gambar yang dipindai** tetapi merasa terhambat pada “bagaimana?”? Anda tidak sendirian. Baik Anda sedang mendigitalkan arsip lama, mengambil data dari faktur, atau membangun perpustakaan PDF yang dapat dicari, mendapatkan teks yang dapat diandalkan dari pemindaian TIFF dapat menjadi titik masalah.  

Berita baik: dengan Aspose OCR untuk Java Anda dapat **mengenali teks dari tiff** dalam beberapa baris kode, bahkan dapat meningkatkan kecepatan dengan membatasi mesin ke beberapa inti CPU. Dalam tutorial ini kami akan membahas seluruh proses—dari menyiapkan pustaka hingga menangani hasil—sehingga Anda dapat menyalin‑tempel contoh yang berfungsi langsung.

## Apa yang Dibahas dalam Tutorial Ini

- Menginstal Aspose OCR untuk Java (Maven atau JAR manual)
- Memuat gambar TIFF yang dipindai berukuran besar
- Mengonfigurasi mesin untuk menggunakan hingga 4 thread (OCR paralel)
- Menjalankan proses OCR dan mencetak teks yang diekstrak
- Kesulitan umum (memori, TIFF multi‑halaman) dan cara menghindarinya
- Tips kinerja cepat: kapan menyesuaikan `setMaxThreads`

Pada akhir tutorial Anda akan dapat **mengekstrak teks dari gambar yang dipindai** secara andal, dan Anda akan memahami mengapa penyesuaian jumlah thread penting saat Anda *mengenali teks dari tiff* dalam alur produksi.

![extract text from scanned image example](example.png "Screenshot showing extracted text from a scanned TIFF image")

## Prasyarat

Sebelum kita mulai, pastikan Anda memiliki:

1. **Java Development Kit (JDK) 8+** – versi terbaru apa pun dapat digunakan.  
2. **Maven** (atau kemampuan menambahkan JAR secara manual) – kami akan menggunakan Maven untuk kemudahan.  
3. Lisensi **Aspose OCR untuk Java** (evaluasi gratis dapat digunakan, tetapi akan menambahkan watermark).  
4. **Pemindaian TIFF besar** (misalnya `large_scan.tif`) yang ingin Anda proses.

Jika ada yang belum familiar, jangan khawatir—setiap langkah dijelaskan di bawah ini.

## Langkah 1: Tambahkan Aspose OCR ke Proyek Anda

### Pengguna Maven

Tambahkan dependensi berikut ke `pom.xml` Anda:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- check the latest version on Maven Central -->
</dependency>
```

### Pengaturan JAR Manual

Unduh `aspose-ocr-xx.jar` terbaru dari situs Aspose dan letakkan di classpath Anda.  

> **Pro tip:** Simpan JAR di folder `libs/` dan referensikan di pengaturan proyek IDE Anda. Ini menghindari kejutan “class not found” di kemudian hari.

## Langkah 2: Buat Kelas Java Sederhana

Buat file bernama `ParallelOcrDemo.java` di folder sumber Anda (`src/main/java`). Kelas ini akan menampung seluruh alur kerja OCR.

```java
package com.example.ocr;

import com.aspose.ocr.*;

public class ParallelOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 2.1: Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2.2: Load the scanned TIFF image you want to process
        // Replace the path with the actual location of your image
        ocrEngine.setImage(new OcrInputImage("YOUR_DIRECTORY/large_scan.tif"));

        // Step 2.3: Limit the engine to use up to 4 CPU cores.
        // This is useful on servers where you don't want to hog all cores.
        ocrEngine.getSettings().setMaxThreads(4);

        // Step 2.4: Run the OCR operation
        OcrResult ocrResult = ocrEngine.process();

        // Step 2.5: Output the recognized text to the console
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

> **Mengapa kami membatasi thread:** Secara default Aspose OCR akan mencoba menggunakan semua inti, yang dapat menghambat layanan lain pada mesin bersama. Menetapkan `setMaxThreads(4)` memberi tahu mesin untuk menjalankan hingga empat pekerja paralel—cukup untuk percepatan yang terasa pada kebanyakan CPU modern tanpa memonopoli sumber daya.

## Langkah 3: Kompilasi dan Jalankan

Buka terminal di root proyek dan jalankan:

```bash
mvn clean compile exec:java -Dexec.mainClass="com.example.ocr.ParallelOcrDemo"
```

Jika Anda tidak menggunakan Maven, kompilasi dengan `javac` dan jalankan:

```bash
javac -cp "libs/*" src/main/java/com/example/ocr/ParallelOcrDemo.java
java -cp "libs/*:src/main/java" com.example.ocr.ParallelOcrDemo
```

### Output yang Diharapkan

```
=== Extracted Text ===
Invoice Number: 12345
Date: 2024‑05‑01
Total: $1,250.00
...
```

Konsol akan menampilkan versi teks biasa dari apa pun yang ada pada halaman yang dipindai. Jika gambar berisi beberapa halaman, Aspose OCR akan menggabungkannya secara berurutan.

## Langkah 4: Menangani TIFF Multi‑Halaman (Kasus Tepi)

Skenario umum adalah **TIFF multi‑halaman**—bayangkan sebuah buku yang dipindai. Secara default `OcrInputImage` hanya membaca frame pertama. Untuk memproses semua halaman, gunakan `OcrInputImage` dengan `FileInputStream` dan aktifkan dukungan multi‑halaman:

```java
import java.io.FileInputStream;
import com.aspose.ocr.*;

FileInputStream fis = new FileInputStream("YOUR_DIRECTORY/multi_page.tif");
ocrEngine.setImage(new OcrInputImage(fis, true)); // 'true' enables multi‑page
```

Sekarang `ocrEngine.process()` akan mengembalikan satu `OcrResult` yang berisi teks yang digabungkan dari setiap halaman.

## Langkah 5: Penyetelan Halus Akurasi Pengenalan

Jika Anda melihat **karakter kacau** atau kata yang hilang, coba penyesuaian berikut:

| Setting | Apa yang Dilakukan | Kapan Digunakan |
|---------|--------------------|-----------------|
| `ocrEngine.getSettings().setLanguage(OcrLanguage.English)` | Memaksa model bahasa Inggris (lebih cepat, lebih akurat untuk pemindaian bahasa Inggris) | Dokumen Anda berbahasa Inggris monolingual |
| `ocrEngine.getSettings().setResolution(300)` | Meningkatkan resolusi gambar beresolusi rendah sebelum pengenalan | Pemindaian di bawah 200 DPI |
| `ocrEngine.getSettings().setNoiseRemoval(true)` | Mencoba membersihkan bintik‑bintik dan artefak | Pemindaian dengan noise berat |

Contoh potongan kode:

```java
ocrEngine.getSettings().setLanguage(OcrLanguage.English);
ocrEngine.getSettings().setResolution(300);
ocrEngine.getSettings().setNoiseRemoval(true);
```

## Langkah 6: Mengekspor Hasil ke File

Mencetak ke konsol cukup untuk demo, tetapi kode produksi biasanya menulis output ke tempat yang berguna:

```java
import java.io.FileWriter;
import java.io.IOException;

// After processing
String extractedText = ocrResult.getText();
try (FileWriter writer = new FileWriter("output.txt")) {
    writer.write(extractedText);
}
System.out.println("Text saved to output.txt");
```

Sekarang Anda memiliki file teks biasa yang dapat Anda masukkan ke indeks pencarian, basis data, atau alur analitik hilir.

## Pertanyaan yang Sering Diajukan (FAQ)

**Q: Apakah ini bekerja dengan file PNG atau JPEG?**  
A: Tentu saja. `OcrInputImage` menerima format apa pun yang dapat dibaca oleh ImageIO Java. Cukup ganti ekstensi file pada path.

**Q: Server saya memiliki 8 inti—haruskah saya mengatur `setMaxThreads(8)`?**  
A: Anda bisa, tetapi ingat layanan lain mungkin membutuhkan siklus CPU. Aturan praktis adalah “total inti – 1” untuk pekerja OCR yang berdedikasi.

**Q: Bagaimana jika hasil OCR kosong?**  
A: Periksa apakah gambar tidak sepenuhnya putih, apakah Anda telah mengatur bahasa yang tepat, dan apakah resolusinya setidaknya 200 DPI. Pemindaian berkualitas rendah sering memerlukan pra‑pemrosesan (deskew, peningkatan kontras) sebelum diberikan ke Aspose OCR.

## Kesimpulan

Kami baru saja **mengekstrak teks dari gambar yang dipindai** menggunakan Aspose OCR untuk Java, dan Anda kini tahu cara **mengenali teks dari tiff** secara efisien dengan pemrosesan paralel. Kode lengkap terdapat dalam potongan di atas, dan Anda dapat menyalin‑tempelnya ke proyek Anda segera.

### Apa Selanjutnya?

- **Pemrosesan batch**: Loop melalui direktori TIFF, simpan setiap hasil ke file terpisah.  
- **Integrasi dengan Elasticsearch**: Indeks teks yang diekstrak untuk pencarian full‑text yang cepat.  
- **Tambahkan deteksi bahasa**: Gunakan `OcrLanguage.AutoDetect` untuk dokumen multibahasa.  

Cobalah ide‑ide tersebut, dan Anda akan dengan cepat mengubah tumpukan dokumen yang dipindai menjadi data yang dapat dicari dan dapat ditindaklanjuti.

Selamat coding, dan jangan ragu meninggalkan komentar jika Anda mengalami kendala!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [How to recognize tiff with Aspose.OCR for Java](/ocr/english/java/ocr-operations/recognize-tiff/)
- [Extract Text Images – OCR Basics with Aspose.OCR for Java](/ocr/english/java/ocr-basics/)
- [Extract Text from Image Java with Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}