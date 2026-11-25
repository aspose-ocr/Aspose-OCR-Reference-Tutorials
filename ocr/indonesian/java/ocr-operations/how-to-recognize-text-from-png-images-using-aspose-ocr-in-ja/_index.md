---
category: general
date: 2026-09-25
description: Mengenali teks dari gambar PNG dengan Aspose OCR di Java – panduan langkah
  demi langkah untuk mengekstrak teks dari gambar dan mengubah gambar menjadi teks.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- recognize text from png
- extract text from image
- convert image to text
- load image for ocr
- read english text image
language: id
lastmod: 2026-09-25
og_description: Mengenali teks dari gambar PNG menggunakan Aspose OCR di Java. Ikuti
  panduan ini untuk mengekstrak teks dari gambar, mengonversi gambar menjadi teks,
  dan membaca gambar teks bahasa Inggris.
og_image_alt: Screenshot showing recognized text output after processing a PNG with
  Aspose OCR
og_title: Mengenali teks dari gambar PNG di Java – tutorial lengkap Aspose OCR
schemas:
- author: Aspose
  dateModified: '2026-09-25'
  description: recognize text from PNG images with Aspose OCR in Java – a step‑by‑step
    guide to extract text from image and convert image to text.
  headline: How to recognize text from PNG images using Aspose OCR in Java
  type: TechArticle
- description: recognize text from PNG images with Aspose OCR in Java – a step‑by‑step
    guide to extract text from image and convert image to text.
  name: How to recognize text from PNG images using Aspose OCR in Java
  steps:
  - name: Why each line matters
    text: '| Line | Purpose | How it helps you **extract text from image** | |------|---------|---------------------------------------------|
      | `new OcrEngine()` | Instantiates the OCR processor. | Provides the engine
      that performs character analysis. | | `engine.setImage(...)` | Loads the PNG
      file into memory'
  - name: 4.1 Missing or corrupt PNG file
    text: 'If the file path is wrong, `ImageStream.fromFile` throws an `IOException`.
      Wrap the loading code in a `try‑catch` block to present a friendly message:'
  - name: 4.2 Non‑English languages
    text: 'Aspose OCR supports many languages. To recognize French, for example, replace
      the language line with:'
  - name: 4.3 Low‑resolution PNGs
    text: OCR accuracy drops when the source image is below 300 dpi. If you notice
      poor results, consider preprocessing the PNG (e.g., scaling up with `java.awt.Image`)
      before passing it to the engine.
  type: HowTo
tags:
- Aspose OCR
- Java
- Image processing
title: Cara mengenali teks dari gambar PNG menggunakan Aspose OCR di Java
url: /id/java/ocr-operations/how-to-recognize-text-from-png-images-using-aspose-ocr-in-ja/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara mengenali teks dari gambar PNG menggunakan Aspose OCR di Java

Jika Anda perlu **mengenali teks dari PNG** dalam aplikasi Java, tutorial ini menunjukkan secara tepat cara melakukannya. Pada akhir panduan Anda akan dapat **mengekstrak teks dari gambar**, mengonversi gambar menjadi teks biasa, dan menampilkan hasilnya di konsol.

Kami akan menggunakan pustaka Aspose OCR, yang menawarkan API sederhana untuk memuat gambar, memilih bahasa, dan mengambil karakter yang dikenali. Langkah‑langkah juga mencakup cara **memuat gambar untuk OCR** dengan aman dan apa yang harus dilakukan ketika mesin gagal. Tidak diperlukan layanan eksternal, dan kode berjalan pada runtime Java 8+ apa pun.

## Prasyarat

* Java 8 atau yang lebih baru terpasang (JDK 8‑21 semuanya didukung)
* Maven atau Gradle untuk mengelola dependensi (kami akan menunjukkan cuplikan Maven)
* File gambar bernama `sample.png` ditempatkan di direktori yang dapat Anda referensikan dari kode
* Familiaritas dasar dengan sintaks Java dan penanganan pengecualian

## Langkah 1: Tambahkan Aspose OCR ke proyek Anda

Aspose OCR didistribusikan sebagai artefak Maven. Tambahkan dependensi berikut ke `pom.xml` Anda:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Use the latest version available -->
</dependency>
```

Jika Anda lebih suka Gradle, yang setara adalah:

```gradle
implementation 'com.aspose:aspose-ocr:23.12'
```

Menambahkan pustaka memberi Anda akses ke `OcrEngine`, `ImageStream`, dan enum bahasa yang diperlukan untuk **mengonversi gambar menjadi teks**.

## Langkah 2: Buat kelas Java dan impor paket yang diperlukan

Buat kelas baru bernama `SampleDemo`. Impor kelas OCR dan utilitas Java standar apa pun yang akan Anda gunakan.

```java
package com.example.ocrdemo;

import com.aspose.ocr.*;
import java.io.IOException;
```

Baris `import com.aspose.ocr.*;` membawa semua yang diperlukan untuk operasi OCR, sementara `java.io.IOException` akan membantu kita menangani kesalahan terkait file.

## ## Mengenali teks dari PNG dengan Aspose OCR

Inti solusi berada di metode `main`. Ikuti langkah‑langkah bernomor di dalam metode untuk melihat cara kerja setiap bagian.

```java
public class SampleDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine instance
        OcrEngine engine = new OcrEngine();

        // Step 2: Load the image to be processed (load image for OCR)
        // Replace "YOUR_DIRECTORY" with the actual path to your PNG file.
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.png"));

        // Step 3: (Optional) Specify the language for recognition.
        // The default language is English, but we set it explicitly to
        // demonstrate how to read english text image.
        engine.setLanguage(OcrLanguage.English);

        // Step 4: Execute the OCR process
        if (engine.process()) {
            // Step 5: Retrieve and display the recognized text
            String text = engine.getText();
            System.out.println("Recognized text: " + text);
        } else {
            System.err.println("OCR processing failed.");
        }
    }
}
```

### Mengapa setiap baris penting

| Baris | Tujuan | Bagaimana itu membantu Anda **extract text from image** |
|------|---------|---------------------------------------------|
| `new OcrEngine()` | Membuat instance processor OCR. | Provides the engine that performs character analysis. |
| `engine.setImage(...)` | Memuat file PNG ke memori. | This is the **load image for OCR** step; without it the engine has nothing to read. |
| `engine.setLanguage(OcrLanguage.English)` | Memberitahu mesin model bahasa mana yang akan digunakan. | Ensures accurate recognition for **read english text image** scenarios. |
| `engine.process()` | Menjalankan algoritma pengenalan. | The heart of **convert image to text** – it scans the bitmap and builds a string. |
| `engine.getText()` | Mengembalikan karakter yang dikenali sebagai `String` Java. | Gives you the final plain‑text result you can store, search, or display. |

## Langkah 4: Tangani kasus tepi umum

Bahkan alur OCR yang ditulis dengan baik dapat menghadapi masalah. Berikut beberapa tip praktis.

### 4.1 File PNG yang hilang atau rusak

Jika jalur file salah, `ImageStream.fromFile` akan melempar `IOException`. Bungkus kode pemuatan dalam blok `try‑catch` untuk menampilkan pesan yang ramah:

```java
try {
    engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.png"));
} catch (IOException e) {
    System.err.println("Unable to load image: " + e.getMessage());
    return;
}
```

### 4.2 Bahasa non‑Inggris

Aspose OCR mendukung banyak bahasa. Untuk mengenali bahasa Prancis, misalnya, ganti baris bahasa dengan:

```java
engine.setLanguage(OcrLanguage.French);
```

Pendekatan yang sama bekerja untuk bahasa Mandarin, Arab, dll., memungkinkan Anda **extract text from image** terlepas dari skrip.

### 4.3 PNG beresolusi rendah

Akurasi OCR menurun ketika gambar sumber di bawah 300 dpi. Jika Anda melihat hasil yang buruk, pertimbangkan pra‑pemrosesan PNG (misalnya, memperbesar dengan `java.awt.Image`) sebelum mengirimkannya ke mesin.

## Langkah 5: Verifikasi output

Jalankan program dari IDE Anda atau baris perintah:

```bash
mvn compile exec:java -Dexec.mainClass="com.example.ocrdemo.SampleDemo"
```

Anda akan melihat sesuatu seperti:

```
Recognized text: Hello, world! This is a sample PNG image.
```

Jika konsol mencetak `OCR processing failed.`, periksa kembali jalur file dan pastikan gambar tidak rusak.

## Tips tambahan untuk penggunaan produksi

* **Batch processing** – Loop melalui direktori file PNG, menggunakan kembali satu instance `OcrEngine` untuk kinerja yang lebih baik.
* **Memory management** – Panggil `engine.dispose()` setelah memproses gambar besar untuk membebaskan sumber daya native.
* **Logging** – Integrasikan kerangka kerja logging (SLF4J, Log4j) alih-alih `System.out` untuk aplikasi yang dapat diskalakan.
* **Error codes** – `engine.process()` mengembalikan `false` untuk banyak alasan; gunakan `engine.getErrorCode()` untuk mendiagnosis kegagalan spesifik.

## Kesimpulan

Anda sekarang tahu cara **recognize text from PNG** gambar di Java menggunakan Aspose OCR. Alur kerja lengkap—**load image for OCR**, secara opsional mengatur bahasa ke **read english text image**, **process**, dan **extract text from image**—siap diintegrasikan ke proyek Java mana pun. Dari sini Anda dapat memperluas solusi untuk **convert image to text** bagi PDF, dokumen yang dipindai, atau umpan kamera waktu nyata.

## Langkah Selanjutnya

* Jelajahi API **convert image to text** untuk format PDF atau TIFF.
* Gabungkan alur OCR ini dengan Apache Tika untuk mengindeks teks yang diekstrak dalam mesin pencari.
* Bereksperimen dengan dukungan multibahasa dengan menukar `OcrLanguage.English` dengan enum bahasa lain.
* Selidiki pengaturan lanjutan Aspose OCR (mis., `engine.setPreprocessOptions`) untuk meningkatkan akurasi pada PNG yang berisik.

Selamat coding, dan nikmati mengubah gambar menjadi teks yang dapat dicari!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Mengenali Teks dari Gambar dengan Aspose OCR – Panduan Java Lengkap](/ocr/english/java/advanced-ocr-techniques/recognize-text-from-image-with-aspose-ocr-full-java-guide/)
- [OCR Gambar Batch di Java – Ekstrak Teks dari File PNG dengan Cepat](/ocr/english/java/ocr-operations/batch-image-ocr-in-java-extract-text-from-png-files-fast/)
- [mengenali gambar teks menggunakan Aspose OCR GPU – Java](/ocr/english/java/advanced-ocr-techniques/recognize-text-image-using-aspose-ocr-gpu-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}