---
category: general
date: 2026-11-14
description: Pelajari cara mengenali teks dari PNG di Java menggunakan Aspose OCR.
  Panduan ini juga mencakup cara mengekstrak teks dari gambar dan memuat gambar untuk
  OCR.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- recognize text from png
- extract text from image
- convert scanned image to text
- load image for ocr
- read text from image java
language: id
lastmod: 2026-11-14
og_description: Kenali teks dari PNG di Java dengan Aspose OCR. Ikuti tutorial langkah
  demi langkah ini untuk mengekstrak teks dari gambar, memuat gambar untuk OCR, dan
  membaca teks dari gambar pada proyek Java.
og_image_alt: Screenshot of Java console showing recognized text from a PNG file
og_title: Mengenali teks dari PNG di Java – panduan lengkap Aspose OCR
schemas:
- author: Aspose
  dateModified: '2026-11-14'
  description: Learn how to recognize text from PNG in Java using Aspose OCR. The
    guide also covers how to extract text from image and load image for OCR.
  headline: How to recognize text from PNG in Java with Aspose OCR
  type: TechArticle
tags:
- Aspose OCR
- Java
- Image processing
title: Cara mengenali teks dari PNG di Java dengan Aspose OCR
url: /id/java/ocr-operations/how-to-recognize-text-from-png-in-java-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara mengenali teks dari PNG di Java dengan Aspose OCR

Jika Anda perlu **mengenali teks dari file PNG** dalam aplikasi Java, tutorial ini menunjukkan solusi lengkap yang siap dijalankan. Pada akhir panduan Anda akan dapat **mengekstrak teks dari gambar**, mengonversi gambar yang dipindai menjadi teks, dan **memuat gambar untuk OCR** menggunakan pustaka Aspose OCR.

Contoh ini juga memperlihatkan cara **membaca teks dari gambar Java**, sehingga Anda dapat mengintegrasikan OCR ke layanan backend apa pun, alat desktop, atau proyek Android.

## Prasyarat

Sebelum memulai, pastikan Anda memiliki:

* Java Development Kit (JDK) 8 atau yang lebih baru terpasang.
* Maven atau Gradle untuk mengelola dependensi (contoh ini menggunakan Maven).
* File lisensi Aspose OCR untuk Java (versi evaluasi gratis dapat digunakan untuk pengujian).
* Sebuah gambar bernama `input.png` yang ditempatkan di folder yang dapat Anda referensikan dari kode Anda.

Persyaratan ini memastikan kode dapat dikompilasi dan dijalankan tanpa pengaturan tambahan.

## Langkah 1: Tambahkan Aspose OCR ke proyek Anda

Tambahkan artefak Maven Aspose OCR ke `pom.xml` Anda. Ini akan mengunduh semua kelas yang diperlukan, termasuk `OcrEngine` dan `ImageStream`.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version>
</dependency>
```

> **Pro tip:** Gunakan nomor versi terbaru (cek Maven Central) untuk mendapatkan peningkatan performa dan dukungan bahasa baru.

## Langkah 2: Muat gambar PNG untuk OCR

Mesin OCR bekerja dengan sebuah `ImageStream`. Anda harus menunjukkannya ke lokasi tepat file PNG yang ingin diproses.

```java
// Load the PNG image that contains the text you want to recognize
String imagePath = "YOUR_DIRECTORY/input.png";
ImageStream imageStream = ImageStream.fromFile(imagePath);
ocrEngine.setImage(imageStream);
```

*Mengapa ini penting*: Memuat gambar dengan benar menghindari kesalahan umum “OCR failed” yang disebabkan oleh format yang tidak didukung atau jalur file yang hilang.

## Langkah 3: Buat dan konfigurasikan mesin OCR

Instansiasi `OcrEngine` dan, bila perlu, sesuaikan bahasa atau pengaturan pengenalan. Konfigurasi default bekerja untuk teks cetak bahasa Inggris, tetapi Anda dapat mengubahnya menjadi `ocrEngine.setLanguage(Language.French)` untuk bahasa lain.

```java
// Step 3: Create the OCR engine instance
OcrEngine ocrEngine = new OcrEngine();

// Optional: set recognition language (default is English)
// ocrEngine.setLanguage(Language.English);
```

## Langkah 4: Jalankan proses OCR

Memanggil `process()` melakukan pekerjaan berat—memindai gambar, memsegmentasi karakter, dan mengonversinya menjadi teks Unicode.

```java
// Step 4: Execute the OCR operation
boolean success = ocrEngine.process();
```

Jika `process()` mengembalikan `true`, mesin telah berhasil **mengonversi gambar yang dipindai menjadi teks**. Jika tidak, periksa output konsol untuk pesan diagnostik.

## Langkah 5: Ambil dan tampilkan teks yang dikenali

Ketika OCR berhasil, Anda dapat mengambil string lengkap dengan `getText()`. Inilah inti dari fungsionalitas **read text from image Java**.

```java
if (success) {
    System.out.println("Recognized text:");
    System.out.println(ocrEngine.getText());
} else {
    System.err.println("OCR failed. Verify the image path and file format.");
}
```

Konsol kini mencetak karakter persis yang muncul di `input.png`. Anda dapat memproses string lebih lanjut—menyimpannya ke basis data, mengirimkannya ke indeks pencarian, atau melakukan analisis bahasa alami.

## Contoh lengkap yang dapat dijalankan

Menggabungkan semua langkah menghasilkan satu kelas mandiri. Salin kode di bawah ini ke file bernama `SimpleOcrDemo.java`, ganti `YOUR_DIRECTORY` dengan jalur absolut atau relatif ke PNG Anda, dan jalankan dengan `mvn exec:java`.

```java
import com.aspose.ocr.*;

public class SimpleOcrDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image to be processed
        String imagePath = "YOUR_DIRECTORY/input.png";
        ocrEngine.setImage(ImageStream.fromFile(imagePath));

        // Step 3: Run the OCR process
        if (ocrEngine.process()) {
            // Step 4: Retrieve and display the recognized text
            System.out.println("Recognized text:");
            System.out.println(ocrEngine.getText());
        } else {
            System.err.println("OCR failed. Check the image path and format.");
        }
    }
}
```

**Output yang diharapkan** (contoh untuk PNG “Hello World” sederhana):

```
Recognized text:
Hello World
```

Jika gambar berisi beberapa baris, mesin akan mempertahankan jeda baris, sehingga pasca‑pemrosesan menjadi mudah.

## Menangani kasus tepi yang umum

| Situasi | Tindakan yang disarankan |
|-----------|--------------------|
| **Gambar bukan PNG** | Konversi file ke PNG atau gunakan `ImageStream.fromFile` dengan format yang didukung (BMP, JPEG, TIFF). |
| **Pemindaian beresolusi rendah** | Tingkatkan DPI sebelum OCR (`ocrEngine.setResolution(300)`) untuk meningkatkan akurasi. |
| **Teks non‑Inggris** | Panggil `ocrEngine.setLanguage(Language.<YourLanguage>)` dan pastikan paket bahasa terpasang. |
| **Banyak file sekaligus** | Gunakan kembali satu instance `OcrEngine` dan panggil `setImage` berulang kali untuk menghindari overhead inisialisasi berulang. |

Tips ini membantu Anda **mengekstrak teks dari gambar** secara andal dari berbagai sumber.

## Pertimbangan kinerja

* **Keamanan thread** – `OcrEngine` tidak thread‑safe. Buat instance terpisah per thread jika Anda berencana memproses gambar secara bersamaan.
* **Penggunaan memori** – Gambar besar mengonsumsi lebih banyak heap. Pertimbangkan untuk memperkecil gambar dengan `ImageResize` sebelum memberikannya ke mesin.
* **Lisensi** – Versi evaluasi menambahkan watermark pada teks output. Deploy salinan berlisensi untuk penggunaan produksi.

## Langkah selanjutnya

Sekarang Anda dapat **mengenali teks dari file PNG**, Anda mungkin ingin mengeksplorasi:

* **Pemrosesan batch** – Loop melalui direktori dan tulis setiap hasil OCR ke file `.txt`.
* **Integrasi dengan Apache Tika** – Gabungkan OCR dengan ekstraksi metadata untuk pipeline pencarian full‑text.
* **Menggunakan Aspose OCR dengan Spring Boot** – Ekspos endpoint HTTP yang menerima gambar yang diunggah dan mengembalikan teks dalam format JSON.

Ekstensi ini dibangun di atas konsep inti yang dibahas dalam panduan ini.

---

*Anda telah mempelajari cara memuat gambar untuk OCR, mengonversi gambar yang dipindai menjadi teks, dan membaca teks dari gambar menggunakan kode Java Aspose OCR. Terapkan pola ini ke format gambar lain, bahasa lain, dan skenario penyebaran untuk membuka kemampuan otomasi dokumen yang kuat.*

## Apa yang Harus Anda Pelajari Selanjutnya?


Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Java OCR Example – Load Image and Recognize Text with Aspose](/ocr/english/java/ocr-basics/java-ocr-example-load-image-and-recognize-text-with-aspose/)
- [Batch Image OCR in Java – Extract Text from PNG Files Fast](/ocr/english/java/ocr-operations/batch-image-ocr-in-java-extract-text-from-png-files-fast/)
- [Extract text from image java using Aspose OCR – guide](/ocr/english/java/advanced-ocr-techniques/extract-text-from-image-with-aspose-ocr-java-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}