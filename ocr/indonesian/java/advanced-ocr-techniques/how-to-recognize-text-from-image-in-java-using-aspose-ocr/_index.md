---
category: general
date: 2026-09-29
description: Pelajari cara mengenali teks dari gambar dengan Java dan Aspose OCR.
  Panduan ini juga menunjukkan cara mengekstrak teks dari JPG serta cara meningkatkan
  akurasi OCR.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- recognize text from image
- extract text from jpg
- how to improve OCR accuracy
- Aspose OCR Java
- Java image processing
language: id
lastmod: 2026-09-29
og_description: Mengenali teks dari gambar di Java dengan Aspose OCR. Ikuti tutorial
  langkah demi langkah ini untuk mengekstrak teks dari JPG dan pelajari cara meningkatkan
  akurasi OCR.
og_image_alt: Java code screenshot that recognizes text from image using Aspose OCR
og_title: Mengenali teks dari gambar di Java – panduan lengkap Aspose OCR
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: Learn how to recognize text from image with Java and Aspose OCR. This
    guide also shows how to extract text from jpg and how to improve OCR accuracy.
  headline: How to recognize text from image in Java using Aspose OCR
  type: TechArticle
- description: Learn how to recognize text from image with Java and Aspose OCR. This
    guide also shows how to extract text from jpg and how to improve OCR accuracy.
  name: How to recognize text from image in Java using Aspose OCR
  steps:
  - name: '**Pre‑process the image** – apply contrast stretching or binarization using
      OpenCV before handing it to Aspose OCR. Cleaner edges give higher confidence.'
    text: '**Pre‑process the image** – apply contrast stretching or binarization using
      OpenCV before handing it to Aspose OCR. Cleaner edges give higher confidence.'
  - name: '**Crop unnecessary margins** – the engine spends time analyzing blank space,
      which can lower the overall confidence score.'
    text: '**Crop unnecessary margins** – the engine spends time analyzing blank space,
      which can lower the overall confidence score.'
  - name: '**Choose the correct language pack** – loading only the languages you need
      speeds up recognition and reduces false positives.'
    text: '**Choose the correct language pack** – loading only the languages you need
      speeds up recognition and reduces false positives.'
  - name: '**Use the latest Aspose OCR version** – each release includes updated neural
      models that improve accuracy out‑of‑the‑box.'
    text: '**Use the latest Aspose OCR version** – each release includes updated neural
      models that improve accuracy out‑of‑the‑box.'
  type: HowTo
tags:
- OCR
- Java
- Aspose
title: Cara mengenali teks dari gambar di Java menggunakan Aspose OCR
url: /id/java/advanced-ocr-techniques/how-to-recognize-text-from-image-in-java-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara mengenali teks dari gambar di Java menggunakan Aspose OCR

Jika Anda perlu **mengenali teks dari gambar** dalam aplikasi Java, tutorial ini menunjukkan solusi siap‑jalankan. Anda akan melihat cara mengekstrak teks dari file jpg, mengaktifkan akselerasi GPU, dan menerapkan koreksi ejaan untuk menjawab pertanyaan umum *bagaimana meningkatkan akurasi OCR*.

Panduan ini mencakup semua yang Anda butuhkan: penyiapan Maven, kode sumber lengkap, penjelasan setiap opsi konfigurasi, dan tips menangani gambar beresolusi rendah. Pada akhir tutorial Anda akan memiliki program yang berfungsi dan mencetak teks yang dikenali ke konsol.

## Prasyarat

Sebelum memulai, pastikan Anda memiliki:

* Java 17 (atau lebih baru) terpasang – Aspose OCR mendukung Java 8+ tetapi runtime yang lebih baru memberikan performa yang lebih baik.
* Maven 3.8+ untuk manajemen dependensi.
* Lisensi Aspose OCR untuk Java (versi percobaan gratis dapat digunakan untuk evaluasi).  
* Gambar JPG (`sample.jpg`) yang berisi teks jelas dan terbaca.

Jika Anda belum memiliki salah satu dari ini, instal JDK dari [oracle.com/java](https://www.oracle.com/java/technologies/downloads/) dan ikuti panduan instalasi Maven di situs Apache.

## Tambahkan Aspose OCR ke proyek Anda

Buat file `pom.xml` (atau tambahkan ke yang sudah ada) dan sertakan dependensi Aspose OCR:

```xml
<project>
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.example</groupId>
  <artifactId>ocr-demo</artifactId>
  <version>1.0.0</version>
  <dependencies>
    <dependency>
      <groupId>com.aspose</groupId>
      <artifactId>aspose-ocr</artifactId>
      <version>23.12</version> <!-- latest stable at time of writing -->
    </dependency>
  </dependencies>
</project>
```

Jalankan `mvn clean compile` untuk mengunduh pustaka. Dependensi ini menyertakan semua binary native yang diperlukan untuk penggunaan GPU dan koreksi ejaan.

## Langkah 1: Siapkan mesin OCR untuk mengenali teks dari gambar

Hal pertama yang Anda lakukan adalah membuat instance `OcrEngine`. Objek ini mengatur seluruh alur kerja OCR.

```java
// Step 1: Create an OCR engine instance
OcrEngine engine = new OcrEngine();
```

Membuat mesin belum memuat gambar apa pun; ia hanya menyiapkan sumber daya internal. Pemisahan ini memungkinkan Anda menggunakan mesin yang sama untuk banyak gambar, yang berguna dalam skenario batch.

## Langkah 2: Aktifkan akselerasi GPU untuk pemrosesan lebih cepat

Jika mesin Anda memiliki GPU yang kompatibel, mengaktifkannya dapat memotong waktu pengenalan hingga 70 %. Ini secara langsung menjawab *bagaimana meningkatkan akurasi OCR* dalam hal kecepatan, yang sering memungkinkan Anda menggunakan gambar beresolusi tinggi tanpa penurunan performa.

```java
// Step 2 (optional): Use GPU if available
engine.getConfiguration().setUseGpu(true);
```

> **Pro tip:** Saat dijalankan pada server tanpa tampilan (headless), pastikan driver CUDA terpasang; jika tidak, panggilan akan beralih ke CPU tanpa error.

## Langkah 3: Aktifkan koreksi ejaan untuk meningkatkan akurasi OCR

Koreksi ejaan adalah model bahasa ringan yang memperbaiki kesalahan pengenalan umum (mis., “l0ve” → “love”). Mengaktifkannya adalah salah satu cara paling efektif untuk menjawab *bagaimana meningkatkan akurasi OCR* untuk teks cetak.

```java
// Step 3 (optional): Enable spell correction
engine.getConfiguration().setSpellCorrector(true);
```

Jika Anda memproses catatan tulisan tangan yang dipindai, Anda mungkin ingin menonaktifkan fitur ini karena modelnya dioptimalkan untuk font cetak.

## Langkah 4: Muat gambar JPG yang ingin Anda ekstrak teksnya

Sekarang muat file gambar. Helper `ImageStream.fromFile` menerima format apa pun yang didukung Aspose OCR, tetapi contoh ini fokus pada JPG karena itu format web paling umum.

```java
// Step 4: Load the image that contains the text to be recognized
engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.jpg"));
```

**Mengapa JPG?** Kompresi JPEG dapat menghasilkan artefak yang membingungkan OCR. Untuk memaksimalkan akurasi, gunakan gambar dengan DPI minimal 300 dan hindari kompresi berlebih. Jika Anda memiliki PNG atau TIFF, Anda dapat langsung melewatkannya ke `fromFile`; kode yang sama tetap berfungsi tanpa perubahan.

## Langkah 5: Lakukan OCR dan ambil teks yang dikenali

Akhirnya, panggil `recognize()` dan cetak hasilnya. Metode ini mengembalikan objek `OcrResult` yang berisi teks mentah, skor kepercayaan, dan kotak pembatas setiap kata.

```java
// Step 5: Run OCR and get the result
OcrResult result = engine.recognize();
System.out.println("=== Recognized text ===");
System.out.println(result.getText());
```

### Output yang diharapkan

```
=== Recognized text ===
Welcome to Aspose OCR demo.
This text was extracted from a JPG image.
```

Jika output berisi karakter yang kacau, tinjau kembali **Langkah 3** (koreksi ejaan) dan pastikan gambar memenuhi rekomendasi DPI.

## Variasi umum dan kasus tepi

| Situasi | Penyesuaian yang disarankan |
|-----------|------------------------|
| **Gambar beresolusi rendah (< 150 DPI)** | Perbesar gambar sebelum memberi ke mesin atau gunakan `engine.getConfiguration().setScaleFactor(2.0)` agar mesin melakukan resampling internal. |
| **Dokumen multi‑bahasa** | Setel `engine.getConfiguration().setLanguage("eng,spa")` untuk memuat kamus Bahasa Inggris dan Spanyol. |
| **Banyak file sekaligus** | Gunakan kembali instance `OcrEngine` yang sama, cukup panggil `engine.setImage(...)` untuk setiap file baru. Ini menghindari pemuatan pustaka native berulang. |
| **Lingkungan dengan memori terbatas** | Nonaktifkan GPU (`setUseGpu(false)`) dan koreksi ejaan (`setSpellCorrector(false)`) untuk mengurangi penggunaan RAM. |
| **Ekstrak teks dari PNG alih‑alih JPG** | Tidak ada perubahan kode; cukup arahkan `fromFile` ke path `.png`. Pustaka secara otomatis mendeteksi formatnya. |

## Tips profesional untuk meningkatkan akurasi OCR

1. **Pra‑proses gambar** – terapkan perpanjangan kontras atau binarisasi menggunakan OpenCV sebelum menyerahkannya ke Aspose OCR. Tepi yang lebih bersih memberikan kepercayaan lebih tinggi.  
2. **Potong margin yang tidak diperlukan** – mesin menghabiskan waktu menganalisis ruang kosong, yang dapat menurunkan skor kepercayaan keseluruhan.  
3. **Pilih paket bahasa yang tepat** – memuat hanya bahasa yang Anda butuhkan mempercepat pengenalan dan mengurangi false positive.  
4. **Gunakan versi Aspose OCR terbaru** – setiap rilis menyertakan model neural yang diperbarui yang meningkatkan akurasi secara langsung.

## Contoh lengkap yang dapat dijalankan

Berikut adalah kelas Java lengkap yang menggabungkan semua langkah. Simpan sebagai `SimpleOcr.java`, sesuaikan path gambar, dan jalankan `mvn exec:java -Dexec.mainClass=SimpleOcr`.

```java
import com.aspose.ocr.*;

public class SimpleOcr {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine instance
        OcrEngine engine = new OcrEngine();

        // Step 2: (Optional) Enable GPU acceleration for faster processing
        engine.getConfiguration().setUseGpu(true);

        // Step 3: (Optional) Enable spell correction to improve OCR accuracy
        engine.getConfiguration().setSpellCorrector(true);

        // Step 4: Load the image that contains the text to be recognized
        // This example extracts text from jpg, but any supported format works.
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.jpg"));

        // Step 5: Perform OCR and retrieve the recognized text
        OcrResult result = engine.recognize();

        System.out.println("=== Recognized text ===");
        System.out.println(result.getText());
    }
}
```

Menjalankan program mencetak teks yang dikenali ke konsol, mengonfirmasi bahwa Anda telah berhasil belajar cara **mengenali teks dari gambar**, cara **mengekstrak teks dari jpg**, dan teknik kunci untuk **bagaimana meningkatkan akurasi OCR**.

## Kesimpulan

Dalam tutorial ini Anda belajar cara **mengenali teks dari gambar** di Java dengan Aspose OCR, cara **mengekstrak teks dari jpg**, dan beberapa cara praktis untuk menjawab *bagaimana meningkatkan akurasi OCR*. Pendekatannya sepenuhnya mandiri: Anda hanya memerlukan dependensi Maven, file JPEG, dan beberapa flag konfigurasi.

Langkah selanjutnya yang dapat Anda jelajahi:

* Mengonversi teks yang dikenali menjadi PDF yang dapat dicari menggunakan Aspose PDF.  
* Memproses seluruh folder gambar dengan loop sederhana (OCR batch).  
* Mengintegrasikan mesin OCR ke endpoint REST Spring Boot untuk pemrosesan gambar on‑demand.

Silakan bereksperimen dengan kualitas gambar, paket bahasa, dan pengaturan perangkat keras yang berbeda untuk melihat bagaimana tiap faktor memengaruhi performa OCR. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Pra‑proses OCR Gambar di Java dengan Aspose OCR – Tingkatkan Akurasi & Ekstrak Teks](/ocr/english/java/advanced-ocr-techniques/preprocess-image-ocr-in-java-boost-accuracy-extract-text/)
- [Cara Menggunakan OCR di Java – Mengenali Teks dari Gambar dengan Cepat](/ocr/english/java/ocr-operations/how-to-use-ocr-in-java-recognize-text-from-image-quickly/)
- [Mengenali Teks dari Gambar dengan Aspose OCR – Panduan Java Lengkap](/ocr/english/java/advanced-ocr-techniques/recognize-text-from-image-with-aspose-ocr-full-java-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}