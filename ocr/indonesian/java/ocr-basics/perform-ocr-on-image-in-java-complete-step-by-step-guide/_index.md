---
category: general
date: 2026-06-16
description: Pelajari cara melakukan OCR pada file gambar di Java. Tutorial ini mencakup
  mengenali teks dari PNG, mengekstrak teks dari gambar, mengonversi gambar menjadi
  teks, dan memuat gambar untuk OCR.
draft: false
keywords:
- perform OCR on image
- recognize text from PNG
- extract text from image
- convert image to text
- load image for OCR
language: id
og_description: Lakukan OCR pada gambar menggunakan Java. Panduan ini menunjukkan
  cara mengenali teks dari PNG, mengekstrak teks dari gambar, dan mengonversi gambar
  menjadi teks dengan contoh yang siap dijalankan.
og_title: Lakukan OCR pada Gambar di Java – Tutorial Pemrograman Lengkap
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Learn how to perform OCR on image files in Java. This tutorial covers
    recognizing text from PNG, extracting text from image, converting image to text,
    and loading image for OCR.
  headline: Perform OCR on Image in Java – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Learn how to perform OCR on image files in Java. This tutorial covers
    recognizing text from PNG, extracting text from image, converting image to text,
    and loading image for OCR.
  name: Perform OCR on Image in Java – Complete Step‑by‑Step Guide
  steps:
  - name: Expected Output
    text: 'If `hello.png` contains the phrase “Hello, OCR world!”, the console will
      display something like:'
  - name: 5.1 Dealing with Low‑Resolution Images
    text: 'If the source PNG is blurry, OCR accuracy drops. A quick fix is to upscale
      the image before feeding it to the engine:'
  - name: 5.2 Multi‑Language Documents
    text: 'If you anticipate French or German text, simply add the language codes
      to `setLanguage`:'
  - name: 5.3 Skipping Empty Pages
    text: 'Sometimes a scanned PDF page renders as a blank PNG. Detecting an empty
      image saves processing time:'
  type: HowTo
tags:
- Java
- OCR
- Image Processing
title: Lakukan OCR pada Gambar di Java – Panduan Lengkap Langkah demi Langkah
url: /id/java/ocr-basics/perform-ocr-on-image-in-java-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lakukan OCR pada Gambar di Java – Panduan Lengkap Langkah‑per‑Langkah

Pernah membutuhkan untuk **perform OCR on image** file tetapi tidak yakin pustaka Java mana yang harus dipilih? Anda tidak sendirian. Baik Anda sedang membangun pemindai struk, pengarsip dokumen, atau hanya penasaran tentang mengubah gambar menjadi teks yang dapat dicari, mempelajari cara **perform OCR on image** dengan Java adalah keterampilan yang berguna.

Dalam tutorial ini kami akan membahas semua yang Anda perlukan untuk **perform OCR on image** file: memuat gambar, mengonfigurasi mesin, mengenali teks, dan akhirnya mencetak hasilnya. Pada akhir tutorial Anda akan dapat **recognize text from PNG** file, **extract text from image** sumber, dan **convert image to text** dengan hanya beberapa baris kode.

## Prasyarat

- Java 17 atau lebih baru (kode ini dapat dikompilasi dengan JDK terbaru apa pun)
- Maven terpasang (atau alat build favorit Anda)
- Familiaritas dasar dengan sintaks Java
- File PNG yang ingin Anda uji (kami akan menyebutnya `hello.png`)

> **Pro tip:** Jika Anda tidak memiliki PNG yang siap pakai, buat satu dengan mengambil screenshot dari teks apa pun dan menyimpannya sebagai `hello.png` di folder bernama `resources`.

## Apa yang Akan Kami Bangun

Sebuah aplikasi konsol kecil bernama `OcrDemo` yang:

1. **Loads image for OCR** – membaca PNG dari disk.
2. **Performs OCR on image** – menggunakan mesin Tesseract melalui Tess4J.
3. **Extracts text from image** – mengembalikan `String` dengan konten yang dikenali.
4. Mencetak hasil ke konsol.

Mari kita mulai.

## Langkah 1: Siapkan Proyek dan Tambahkan Tess4J

Pertama, buat proyek Maven baru (atau Gradle jika Anda lebih suka). Tambahkan dependensi Tess4J, yang membungkus mesin Tesseract OCR populer.

```xml
<!-- pom.xml -->
<project>
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

> **Mengapa Tess4J?** Ini aktif dipelihara, bekerja lintas‑platform, dan memberikan Anda API Java yang bersih untuk tugas **perform OCR on image**.

## Langkah 2: Siapkan Logika Memuat Gambar

Sekarang kami akan menulis metode pembantu yang **load image for OCR**. Metode ini menggunakan `ImageIO` Java untuk membaca PNG ke dalam `BufferedImage`.

```java
package com.example.ocr;

import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;
import java.io.IOException;

/**
 * Utility class responsible for loading images from the file system.
 */
public final class ImageLoader {

    private ImageLoader() { /* utility class */ }

    /**
     * Loads a PNG (or any supported format) from the given path.
     *
     * @param path absolute or relative path to the image file
     * @return BufferedImage instance ready for OCR processing
     * @throws IOException if the file cannot be read
     */
    public static BufferedImage load(String path) throws IOException {
        File imgFile = new File(path);
        if (!imgFile.exists()) {
            throw new IOException("Image file not found: " + path);
        }
        return ImageIO.read(imgFile);
    }
}
```

Perhatikan nama metode yang jelas mencerminkan maksud **load image for OCR**, menjadikan kode mudah dipahami.

## Langkah 3: Konfigurasikan Mesin OCR untuk **Perform OCR on Image**

Dengan gambar di tangan, kami membuat instance `Tesseract`, mengaktifkan deteksi bahasa otomatis, dan memanggil `doOCR`. Ini adalah inti dari cara kami **perform OCR on image** data.

```java
package com.example.ocr;

import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;

/**
 * Wrapper around Tess4J that abstracts the OCR workflow.
 */
public final class OcrEngine {

    private final ITesseract tesseract;

    public OcrEngine() {
        tesseract = new Tesseract();

        // Use the bundled tessdata folder (you can also point to a custom one)
        tesseract.setDatapath("tessdata");

        // Enable automatic language detection – improves accuracy across multilingual images
        tesseract.setLanguage("eng"); // fallback language
        tesseract.setOcrEngineMode(ITesseract.OEM_DEFAULT);
        tesseract.setPageSegMode(ITesseract.PSM_AUTO);
    }

    /**
     * Performs OCR on the supplied BufferedImage and returns the recognized text.
     *
     * @param image image to be processed
     * @return the text extracted from the image
     * @throws TesseractException if OCR fails
     */
    public String recognize(BufferedImage image) throws TesseractException {
        return tesseract.doOCR(image);
    }
}
```

> **Mengapa mengaktifkan auto‑detect?** Ini memungkinkan mesin memilih model bahasa terbaik untuk gambar, yang sangat berguna ketika Anda **convert image to text** dari sumber yang mencampur bahasa Inggris dan skrip lain.

## Langkah 4: Gabungkan Semua – Aplikasi Utama

Berikut adalah titik masuk yang **recognize text from PNG**, **extract text from image**, dan akhirnya mencetak hasilnya. Ini adalah contoh lengkap yang dapat dijalankan.

```java
package com.example.ocr;

import net.sourceforge.tess4j.TesseractException;
import java.awt.image.BufferedImage;
import java.io.IOException;

/**
 * Demo application that shows how to perform OCR on image files.
 */
public class OcrDemo {

    public static void main(String[] args) {
        // Path to the PNG you want to process
        String imagePath = "resources/hello.png";

        try {
            // Step 1: Load image for OCR
            BufferedImage image = ImageLoader.load(imagePath);

            // Step 2: Create OCR engine instance
            OcrEngine engine = new OcrEngine();

            // Step 3: Perform OCR on image and retrieve the text
            String recognizedText = engine.recognize(image);

            // Step 4: Output the recognized text to the console
            System.out.println("=== Recognized Text ===");
            System.out.println(recognizedText);
        } catch (IOException e) {
            System.err.println("Failed to load image: " + e.getMessage());
        } catch (TesseractException e) {
            System.err.println("OCR processing error: " + e.getMessage());
        }
    }
}
```

### Output yang Diharapkan

Jika `hello.png` berisi frasa “Hello, OCR world!”, konsol akan menampilkan sesuatu seperti:

```
=== Recognized Text ===
Hello, OCR world!
```

Output sebenarnya mungkin sedikit berbeda tergantung pada kualitas gambar, tetapi Anda seharusnya melihat teks yang Anda tempatkan di PNG.

## Langkah 5: Menangani Kasus Edge Umum

### 5.1 Menangani Gambar Resolusi Rendah

Jika PNG sumber buram, akurasi OCR menurun. Solusi cepat adalah memperbesar gambar sebelum memberikannya ke mesin:

```java
import java.awt.Graphics2D;
import java.awt.RenderingHints;

public static BufferedImage upscale(BufferedImage original, int factor) {
    int width = original.getWidth() * factor;
    int height = original.getHeight() * factor;
    BufferedImage scaled = new BufferedImage(width, height, original.getType());
    Graphics2D g = scaled.createGraphics();
    g.setRenderingHint(RenderingHints.KEY_INTERPOLATION,
                       RenderingHints.VALUE_INTERPOLATION_BICUBIC);
    g.drawImage(original, 0, 0, width, height, null);
    g.dispose();
    return scaled;
}
```

Panggil `upscale(image, 2)` sebelum `engine.recognize(image)` untuk meningkatkan hasil.

### 5.2 Dokumen Multi‑Bahasa

Jika Anda mengantisipasi teks bahasa Prancis atau Jerman, cukup tambahkan kode bahasa ke `setLanguage`:

```java
tesseract.setLanguage("eng+fra+deu");
```

Mesin kemudian akan mencoba **extract text from image** menggunakan model bahasa gabungan.

### 5.3 Melewatkan Halaman Kosong

Kadang halaman PDF yang dipindai muncul sebagai PNG kosong. Mendeteksi gambar kosong menghemat waktu pemrosesan:

```java
if (image.getWidth() == 0 || image.getHeight() == 0) {
    System.out.println("Empty image – skipping OCR.");
    return;
}
```

## Langkah 6: Mengemas dan Menjalankan Aplikasi

1. **Compile:** `mvn clean compile`
2. **Run:** `mvn exec:java -Dexec.mainClass="com.example.ocr.OcrDemo"`

Pastikan folder `tessdata` (yang berisi file bahasa) berada di samping JAR yang dikompilasi atau tentukan path absolutnya di `OcrEngine`.

## Kesimpulan

Anda kini memiliki pola yang solid dan siap produksi untuk **perform OCR on image** file menggunakan Java. Dari **loading image for OCR** hingga **recognize text from PNG**, kami membahas cara **extract text from image**, **convert image to text**, dan menangani skenario rumit seperti pemindaian resolusi rendah atau konten multi‑bahasa.

Selanjutnya, Anda mungkin ingin menjelajahi:

- **Batch processing** – mengulangi direktori PNG dan menulis setiap hasil ke file `.txt`.
- **PDF generation** – menyematkan teks yang diekstrak kembali ke PDF yang dapat dicari.
- **Cloud OCR services** – membandingkan kinerja Tesseract lokal dengan API seperti Google Vision atau Azure Cognitive Services.

Silakan bereksperimen, mengubah parameter, dan berbagi temuan Anda. Selamat coding, semoga gambar Anda selalu berubah menjadi teks bersih yang dapat dicari!

![Diagram yang menunjukkan alur kerja OCR untuk melakukan OCR pada gambar](https://example.com/ocr-workflow.png "contoh melakukan OCR pada gambar")

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [mengenali teks gambar dengan Aspose OCR – Tutorial OCR Java Lengkap](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Konversi Gambar ke Teks di Java menggunakan Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [Ekstrak Teks dari Gambar Java dengan Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}