---
category: general
date: 2026-07-21
description: Ekstrak teks dari gambar menggunakan Java OCR. Pelajari cara mengonversi
  PNG ke teks, membaca teks dari PNG, memuat gambar untuk OCR, dan melakukan OCR pada
  gambar dalam beberapa langkah saja.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- extract text from image
- convert png to text
- read text from png
- load image for ocr
- perform ocr on image
language: id
lastmod: 2026-07-21
og_description: Ekstrak teks dari gambar dengan Java. Panduan ini menunjukkan cara
  mengonversi PNG menjadi teks, membaca teks dari PNG, memuat gambar untuk OCR, dan
  melakukan OCR pada gambar secara efisien.
og_image_alt: Screenshot of Java code extracting text from an image using OCR
og_title: Ekstrak Teks dari Gambar di Java – Tutorial OCR Langkah demi Langkah
schemas:
- author: Aspose
  dateModified: '2026-07-21'
  description: Extract text from image using Java OCR. Learn how to convert PNG to
    text, read text from PNG, load image for OCR, and perform OCR on image in just
    a few steps.
  headline: Extract Text from Image in Java – Complete OCR Guide
  type: TechArticle
- description: Extract text from image using Java OCR. Learn how to convert PNG to
    text, read text from PNG, load image for OCR, and perform OCR on image in just
    a few steps.
  name: Extract Text from Image in Java – Complete OCR Guide
  steps:
  - name: Low‑Quality Images
    text: 'If the PNG is blurry or has low contrast, OCR accuracy drops. A quick fix
      is to pre‑process the image:'
  - name: Multi‑Language Support
    text: Tess4J can handle many languages. Just download the appropriate `.traineddata`
      file and point `tesseract.setLanguage("spa")` for Spanish, for example.
  - name: Large PDFs or Multi‑Page Images
    text: If you need to **extract text from image** files inside a PDF, split each
      page into PNGs first (using PDFBox) and then feed each PNG to the same OCR routine.
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: Ekstrak Teks dari Gambar di Java – Panduan OCR Lengkap
url: /id/java/ocr-basics/extract-text-from-image-in-java-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ekstrak Teks dari Gambar di Java – Panduan OCR Lengkap

Pernahkah Anda perlu **extract text from image** tetapi tidak yakin pustaka Java mana yang harus dipilih? Anda tidak sendirian. Baik Anda mendigitalkan kwitansi, memindai PDF, atau membangun arsip yang dapat dicari, mengekstrak teks dari PNG adalah masalah harian bagi banyak pengembang.

Dalam tutorial ini kami akan membahas solusi praktis yang memungkinkan Anda **convert PNG to text**, **read text from PNG**, **load image for OCR**, dan **perform OCR on image**—semua dengan beberapa baris kode Java yang bersih. Pada akhir tutorial Anda akan memiliki program yang dapat dijalankan dan dapat Anda masukkan ke dalam proyek apa pun.

## Apa yang Akan Anda Bangun

Kami akan membuat aplikasi konsol Java kecil yang:

1. Memuat file PNG dari disk.  
2. Mengirim gambar ke mesin OCR (Tess4J, pembungkus Java untuk Tesseract).  
3. Mencetak teks yang dikenali ke konsol.

Tanpa layanan eksternal, tanpa keajaiban—hanya Java murni dan mesin OCR sumber terbuka.

## Prasyarat

- **Java 17** atau lebih baru (kode dapat dikompilasi dengan versi lebih lama, tetapi Java 17 memberi Anda fitur bahasa terbaru).  
- **Maven** atau **Gradle** untuk manajemen dependensi.  
- Contoh PNG bernama `sample.png` ditempatkan di folder yang dapat Anda referensikan (misalnya `src/main/resources`).  
- Familiaritas dasar dengan metode `main` Java dan penanganan exception.

Jika ada yang terdengar tidak familiar, jangan khawatir—setiap langkah menyertakan rangkuman singkat.

## Langkah 1: Siapkan Proyek dan Tambahkan Pustaka OCR

Pertama, buat proyek Maven baru (atau Gradle jika Anda lebih suka). Tambahkan dependensi Tess4J, yang akan menyertakan binary Tesseract untuk Anda.

```xml
<!-- pom.xml -->
<project xmlns="http://maven.apache.org/POM/4.0.0" ...>
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>ocr-demo</artifactId>
    <version>1.0.0</version>
    <properties>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
    </properties>

    <dependencies>
        <!-- Tess4J – Java wrapper for Tesseract OCR -->
        <dependency>
            <groupId>net.sourceforge.tess4j</groupId>
            <artifactId>tess4j</artifactId>
            <version>5.5.1</version>
        </dependency>
    </dependencies>
</project>
```

> **Pro tip:** Jika Anda menggunakan Gradle, baris yang setara adalah `implementation 'net.sourceforge.tess4j:tess4j:5.5.1'`.

Menambahkan pustaka ini memberi Anda kelas `Tesseract`, yang menangani pekerjaan berat **performing OCR on image** data.

## Langkah 2: Muat Gambar untuk OCR

Sekarang kita perlu **load image for OCR**. Tess4J bekerja dengan `java.awt.image.BufferedImage`, jadi kami akan membaca PNG menggunakan `ImageIO`.

```java
package com.example.ocrdemo;

import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;

import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;
import java.io.IOException;

public class OcrDemo {

    /**
     * Loads a PNG file from the given path and returns a BufferedImage.
     *
     * @param path absolute or relative path to the PNG file
     * @return BufferedImage containing the image data
     * @throws IOException if the file cannot be read
     */
    private static BufferedImage loadImage(String path) throws IOException {
        // Step 2: Load the image to be recognized
        File imgFile = new File(path);
        return ImageIO.read(imgFile);
    }
```

Metode di atas dengan bersih memisahkan logika **load image for OCR**, membuat sisa kode lebih mudah diuji. Perhatikan komentar – ia mencerminkan potongan kode asli sambil memperluasnya untuk kejelasan.

## Langkah 3: Lakukan OCR pada Gambar

Dengan gambar berada di memori, kita sekarang dapat **perform OCR on image**. Instance `Tesseract` adalah mesin kita; kami akan mengkonfigurasikannya untuk menggunakan data bahasa Inggris default yang disertakan dengan Tess4J.

```java
    /**
     * Runs OCR on the supplied BufferedImage and returns the extracted text.
     *
     * @param image the image to analyze
     * @return plain text recognized from the image
     * @throws TesseractException if the OCR process fails
     */
    private static String extractText(BufferedImage image) throws TesseractException {
        // Step 1: Initialize the OCR engine
        Tesseract tesseract = new Tesseract();

        // Optional: set the datapath if you have a custom tessdata folder
        // tesseract.setDatapath("tessdata");

        // Step 4: Run OCR and capture the recognized text
        return tesseract.doOCR(image);
    }
```

Di sini kami menggabungkan “Step 1” dan “Step 4” asli menjadi satu metode, karena objek `Tesseract` murah untuk dibuat dan kami ingin kode tetap ringkas. Komentar masih merujuk pada langkah asli untuk jejak.

## Langkah 4: Gabungkan Semua – Metode Main

Akhirnya, kami menggabungkan semuanya dalam `main`. Di sinilah Anda akan **read text from PNG** dan melihat hasilnya dicetak ke konsol.

```java
    public static void main(String[] args) {
        // Adjust the path to point at your PNG file
        String imagePath = "src/main/resources/sample.png";

        try {
            // Load the PNG image
            BufferedImage image = loadImage(imagePath);

            // Extract text from the image
            String recognizedText = extractText(image);

            // Step 5: Display the extracted text
            System.out.println("=== OCR Result ===");
            System.out.println(recognizedText);
        } catch (IOException e) {
            System.err.println("Failed to load image: " + e.getMessage());
        } catch (TesseractException e) {
            System.err.println("OCR error: " + e.getMessage());
        }
    }
}
```

Saat Anda menjalankan `mvn compile exec:java -Dexec.mainClass="com.example.ocrdemo.OcrDemo"` (atau setara Gradle), Anda akan melihat sesuatu seperti:

```
=== OCR Result ===
Hello, world!
This is a sample PNG file.
```

Output tersebut membuktikan bahwa Anda telah berhasil **extract text from image**, **convert PNG to text**, dan **read text from PNG** dalam satu program yang rapi.

## Menangani Kasus Edge Umum

### Gambar Berkualitas Rendah

Jika PNG buram atau memiliki kontras rendah, akurasi OCR menurun. Solusi cepat adalah memproses ulang gambar:

```java
// Example: Convert to grayscale and apply a binary threshold
BufferedImage gray = new BufferedImage(
        image.getWidth(), image.getHeight(),
        BufferedImage.TYPE_BYTE_GRAY);
Graphics2D g = gray.createGraphics();
g.drawImage(image, 0, 0, null);
g.dispose();

// Simple binary threshold
for (int y = 0; y < gray.getHeight(); y++) {
    for (int x = 0; x < gray.getWidth(); x++) {
        int rgb = gray.getRGB(x, y) & 0xFF;
        int binary = rgb < 128 ? 0x000000 : 0xFFFFFF;
        gray.setRGB(x, y, binary);
    }
}
String text = extractText(gray);
```

### Dukungan Multi‑Bahasa

Tess4J dapat menangani banyak bahasa. Cukup unduh file `.traineddata` yang sesuai dan set `tesseract.setLanguage("spa")` untuk bahasa Spanyol, misalnya.

### PDF Besar atau Gambar Multi‑Halaman

Jika Anda perlu **extract text from image** file di dalam PDF, bagi setiap halaman menjadi PNG terlebih dahulu (menggunakan PDFBox) dan kemudian berikan setiap PNG ke rutinitas OCR yang sama.

## Contoh Lengkap yang Berfungsi (Semua Kode dalam Satu Tempat)

Berikut adalah kelas Java lengkap yang siap dijalankan. Salin‑tempel ke `src/main/java/com/example/ocrdemo/OcrDemo.java` dan Anda siap.

```java
package com.example.ocrdemo;

import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;

import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;
import java.io.IOException;

/**
 * Demonstrates how to extract text from image (PNG) using Java and Tess4J.
 */
public class OcrDemo {

    private static BufferedImage loadImage(String path) throws IOException {
        // Step 2: Load the image for OCR
        File imgFile = new File(path);
        return ImageIO.read(imgFile);
    }

    private static String extractText(BufferedImage image) throws TesseractException {
        // Step 1: Initialize the OCR engine
        Tesseract tesseract = new Tesseract();
        // Uncomment and set if you have a custom tessdata folder
        // tesseract.setDatapath("tessdata");
        // Step 4: Perform OCR on image
        return tesseract.doOCR(image);
    }

    public static void main(String[] args) {
        // Path to the PNG you want to convert to text
        String imagePath = "src/main/resources/sample.png";

        try {
            BufferedImage image = loadImage(imagePath);
            String recognizedText = extractText(image);
            System.out.println("=== OCR Result ===");
            System.out.println(recognizedText);
        } catch (IOException e) {
            System.err.println("Failed to load image: " + e.getMessage());
        } catch (TesseractException e) {
            System.err.println("Error during OCR: " + e.getMessage());
        }
    }
}
```

Menjalankan kelas ini mencetak hasil OCR, mengonfirmasi bahwa Anda telah berhasil **performed OCR on image** dan mengubah PNG Anda menjadi teks yang dapat diedit.

## Ringkasan & Langkah Selanjutnya

Kami memulai dengan **extracting text from image** menggunakan setup Java ringan. Sekarang Anda tahu cara **load image for OCR**, **perform OCR on image**, dan **read text from PNG**—blok bangunan penting untuk pipeline digitalisasi dokumen apa pun.

Ingin melangkah lebih jauh? Coba ide-ide berikut:

- **Batch processing:** Loop melalui direktori PNG dan tulis setiap hasil ke file `.txt`.  
- **Integrate with a database:** Simpan string yang diekstrak bersama metadata untuk arsip yang dapat dicari.  
- **Combine with NLP:** Berikan output OCR ke model analisis sentimen untuk wawasan cepat.

Setiap ekstensi tersebut dibangun di atas konsep inti yang kami bahas, jadi Anda siap bereksperimen.

---

*Selamat coding! Jika Anda mengalami kendala

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Ekstrak Teks dari Gambar Java dengan Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [gambar ke teks java: Convert Image to Text dengan Aspose.OCR](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [Cara OCR Teks Gambar dengan Bahasa Menggunakan Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}