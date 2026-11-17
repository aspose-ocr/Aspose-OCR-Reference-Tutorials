---
category: general
date: 2026-11-17
description: Pelajari cara melakukan OCR pada gambar di Java dan mengekstrak teks
  dari foto menggunakan contoh kode sederhana. Termasuk tips membaca gambar di Java.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to perform OCR
- extract text image
- read image java
- convert image to text
- image to text java
language: id
lastmod: 2026-11-17
og_description: Cara melakukan OCR pada gambar di Java dan mengekstrak teks dengan
  cepat. Ikuti panduan ini untuk membaca gambar di Java dan mengubah gambar menjadi
  teks dengan contoh siap pakai.
og_image_alt: Screenshot showing Java code that performs OCR on an image
og_title: Cara melakukan OCR pada gambar di Java – panduan langkah demi langkah
schemas:
- author: Aspose
  dateModified: '2026-11-17'
  description: Learn how to perform OCR on an image in Java and extract text from
    pictures using a simple code example. Includes read image Java tips.
  headline: How to perform OCR on an image in Java – step‑by‑step guide
  type: TechArticle
tags:
- OCR
- Java
- Image processing
- Text extraction
title: Cara melakukan OCR pada gambar di Java – panduan langkah demi langkah
url: /id/java/ocr-basics/how-to-perform-ocr-on-an-image-in-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara melakukan OCR pada gambar di Java – panduan langkah demi langkah

Jika Anda perlu **how to perform OCR** pada gambar, tutorial ini menunjukkan solusi lengkap yang dapat dijalankan di Java. Anda akan melihat cara membaca file gambar, mengonfigurasi mesin OCR, dan mengekstrak teks yang dikenali oleh mesin tersebut.

Bekerja dengan dokumen yang dipindai, kwitansi, atau tangkapan layar sering memerlukan konversi konten visual menjadi teks yang dapat dicari. Panduan ini membawa Anda melalui setiap langkah, mulai dari memuat gambar hingga mencetak teks yang diekstrak, dan juga mencakup jebakan umum seperti format file yang tidak didukung dan hasil null.

## Prasyarat

* Java Development Kit (JDK) 8 atau yang lebih baru terpasang.
* Alat build (Maven atau Gradle) untuk mengambil pustaka OCR.
* File gambar (JPEG, PNG, BMP) yang ingin Anda proses.

Kode ini menggunakan **OCR library from the `com.asprise.ocr` package** karena hanya memerlukan satu JAR dan bekerja di semua platform utama. Ganti dengan penyedia lain (Tesseract, Google Vision, dll.) dengan menukar pernyataan import dan kode inisialisasi mesin.

## Langkah 1: Tambahkan dependensi OCR

Jika Anda menggunakan Maven, tambahkan dependensi berikut ke `pom.xml` Anda:

```xml
<dependency>
    <groupId>com.asprise.ocr</groupId>
    <artifactId>asprise-ocr</artifactId>
    <version>1.2.0</version>
</dependency>
```

Untuk Gradle, letakkan baris ini di `build.gradle`:

```gradle
implementation 'com.asprise.ocr:asprise-ocr:1.2.0'
```

Baris-baris ini memastikan bahwa kode **read image Java** dapat dikompilasi dan mesin OCR tersedia saat runtime.

## Langkah 2: Baca gambar dengan Java

Membaca file gambar adalah langkah konkret pertama dalam alur kerja **extract text image** apa pun. Kelas `ImageIO` bawaan Java menangani sebagian besar format umum.

```java
import java.awt.image.BufferedImage;
import java.io.File;
import javax.imageio.ImageIO;

/**
 * Loads an image from the supplied path.
 *
 * @param path absolute or relative path to the image file
 * @return a BufferedImage instance, or null if the file cannot be read
 */
private static BufferedImage loadImage(String path) {
    try {
        return ImageIO.read(new File(path));
    } catch (Exception e) {
        System.err.println("Failed to read image: " + e.getMessage());
        return null;
    }
}
```

**Mengapa ini penting:** `ImageIO.read` mengembalikan `null` untuk format yang tidak didukung atau file yang rusak. Metode di atas mencatat masalah tersebut dan mengembalikan `null` sehingga langkah berikutnya dapat merespons dengan baik.

## Langkah 3: Buat dan konfigurasikan mesin OCR

Mesin OCR harus mengetahui bahasa apa yang akan dikenali. Menetapkan bahasa meningkatkan akurasi secara dramatis, terutama untuk dokumen non‑English.

```java
import com.asprise.ocr.Ocr;

/**
 * Instantiates an OCR engine configured for English.
 *
 * @return a ready‑to‑use Ocr object
 */
private static Ocr createEngine() {
    Ocr ocrEngine = new Ocr();
    // The first argument is the language; "eng" is the ISO code for English.
    ocrEngine.startEngine("eng", Ocr.SPEED_FAST);
    return ocrEngine;
}
```

**Mengapa ini penting:** Memulai mesin merupakan operasi yang relatif berat, jadi Anda sebaiknya membuatnya sekali dan menggunakannya kembali untuk beberapa gambar jika aplikasi Anda memproses batch.

## Langkah 4: Lakukan OCR dan konversi gambar menjadi teks

Sekarang gambar telah dimuat dan mesin siap, Anda dapat menjalankan langkah pengenalan. Ini adalah inti dari **how to perform OCR**.

```java
/**
 * Runs OCR on a BufferedImage and returns the recognized text.
 *
 * @param ocrEngine an initialized Ocr instance
 * @param image     the image to process
 * @return the extracted text, or an empty string if nothing is recognized
 */
private static String extractText(Ocr ocrEngine, BufferedImage image) {
    if (image == null) {
        return "";
    }
    // The third parameter (0) tells the engine to return plain text.
    String result = ocrEngine.recognize(image, 0);
    return result != null ? result.trim() : "";
}
```

**Penanganan kasus tepi:** Jika gambar `null`, metode mengembalikan string kosong alih-alih melempar `NullPointerException`. Ini membuat kode di sekitarnya lebih kuat saat menangani file yang diberikan pengguna.

## Langkah 5: Tampilkan teks yang diekstrak

Akhirnya, cetak hasil ke konsol atau teruskan ke komponen lain (mis., basis data atau widget UI).

```java
/**
 * Demonstrates the full OCR workflow.
 *
 * @param args command‑line arguments (first argument = path to image)
 */
public static void main(String[] args) {
    if (args.length == 0) {
        System.err.println("Usage: java OcrDemo <path-to-image>");
        return;
    }

    String imagePath = args[0];
    BufferedImage image = loadImage(imagePath);
    Ocr ocrEngine = createEngine();

    String text = extractText(ocrEngine, image);
    System.out.println("=== Recognized Text ===");
    System.out.println(text.isEmpty() ? "(no text detected)" : text);

    // Clean up the OCR engine to free native resources.
    ocrEngine.stopEngine();
}
```

Saat Anda menjalankan program dengan `java OcrDemo sample.jpg`, konsol menampilkan karakter yang dikenali. Ini menyelesaikan siklus **convert image to text**.

### Output yang diharapkan

```
=== Recognized Text ===
The quick brown fox jumps over the lazy dog.
```

Jika gambar tidak mengandung karakter yang dapat dibaca, program mencetak `(no text detected)`.

## Variasi umum dan cara menyesuaikannya

| Variasi | Apa yang berubah | Kapan digunakan |
|-----------|--------------|-------------|
| **Different language** | Ganti `"eng"` dengan `"spa"` untuk bahasa Spanyol, `"fra"` untuk bahasa Prancis, dll. | Dokumen yang ditulis dalam bahasa selain Inggris |
| **Batch processing** | Iterasi daftar jalur file, gunakan kembali instance `Ocr` yang sama. | Set besar halaman yang dipindai |
| **Higher accuracy** | Gunakan `Ocr.SPEED_SLOW` atau aktifkan `ocrEngine.setConfig("tessedit_char_whitelist", "0123456789")` untuk pemindaian yang hanya berisi angka. | Saat kualitas OCR sangat penting (mis., nomor faktur) |
| **Tesseract alternative** | Ganti import ke `net.sourceforge.tess4j.Tesseract` dan sesuaikan kode inisialisasi. | Proyek yang sudah bergantung pada Tesseract |

## Tips profesional

* **Resize large images** sebelum memberi ke mesin; kecepatan OCR skala dengan jumlah piksel.
* **Pre‑process** gambar (grayscale, peningkatan kontras) menggunakan pustaka seperti OpenCV jika sumbernya berisik.
* **Cache the OCR engine** jika Anda memanggilnya berkali-kali dalam periode singkat—memulai dan menghentikan mesin menimbulkan overhead.
* **Validate the result** dengan ekspresi reguler ketika Anda mengharapkan format tertentu (mis., tanggal, nomor telepon).

## Kesimpulan

Anda sekarang tahu **how to perform OCR** pada gambar di Java, mulai dari membaca file hingga menampilkan teks yang diekstrak. Tutorial ini mencakup teknik **read image Java**, **extract text image**, **convert image to text**, dan **image to text java**, serta memberikan tips praktis untuk skenario dunia nyata.  

Dari sini Anda dapat:

* Mengintegrasikan langkah OCR ke layanan web yang menerima unggahan.
* Menggabungkan output dengan indeks pencarian untuk pencarian full‑text pada dokumen yang dipindai.
* Menjelajahi opsi OCR lanjutan seperti dukungan multi‑bahasa atau set karakter khusus.

Selamat coding, dan nikmati mengubah gambar menjadi teks yang dapat dicari!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Cara Menggunakan OCR di Java – Ekstrak Teks dari Gambar dengan Koreksi Ejaan](/ocr/english/java/ocr-operations/how-to-use-ocr-in-java-extract-text-from-image-with-spell-co/)
- [Konversi Gambar ke Teks di Java Menggunakan Aspose OCR – Panduan Lengkap](/ocr/english/java/ocr-operations/convert-image-to-text-in-java-using-aspose-ocr-full-guide/)
- [Cara Mengaktifkan GPU untuk OCR di Java – Ekstrak Teks dari Gambar](/ocr/english/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-extract-text-from-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}