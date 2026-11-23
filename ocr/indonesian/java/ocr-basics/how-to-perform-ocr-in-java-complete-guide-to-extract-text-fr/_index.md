---
category: general
date: 2026-06-06
description: cara melakukan OCR di Java – dengan cepat mengekstrak teks dari gambar,
  mengonversi gambar menjadi teks, dan membaca teks dari jpg menggunakan contoh kode
  sederhana.
draft: false
keywords:
- how to perform OCR
- ocr in java
- extract text from image
- convert image to text
- read text from jpg
language: id
og_description: cara melakukan OCR di Java – pelajari cara mengekstrak teks dari gambar,
  mengonversi gambar menjadi teks, dan membaca teks dari jpg dengan contoh siap‑jalankan.
og_title: Cara Melakukan OCR di Java – Panduan Langkah demi Langkah
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: how to perform OCR in Java – quickly extract text from image, convert
    image to text, and read text from jpg using a simple code example.
  headline: How to Perform OCR in Java – Complete Guide to Extract Text from Images
  type: TechArticle
- description: how to perform OCR in Java – quickly extract text from image, convert
    image to text, and read text from jpg using a simple code example.
  name: How to Perform OCR in Java – Complete Guide to Extract Text from Images
  steps:
  - name: What You’ll Learn
    text: '- Install an OCR library (yes, **ocr in java** is easier than you think).
      - Create and configure an OCR engine instance. - Load a JPG (or any image) and
      set the language. - Process the image and **extract text from image** files.
      - Print the recognized string to the console.'
  - name: Expected Output
    text: 'If `input.jpg` contains the Mongolian phrase “Сайн байна уу?” the console
      will show:'
  - name: 'Pro Tip: Batch Processing'
    text: 'If you need to **extract text from image** files in bulk, wrap the core
      logic in a loop:'
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: Cara Melakukan OCR di Java – Panduan Lengkap untuk Mengekstrak Teks dari Gambar
url: /id/java/ocr-basics/how-to-perform-ocr-in-java-complete-guide-to-extract-text-fr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Melakukan OCR di Java – Panduan Lengkap untuk Mengekstrak Teks dari Gambar

Pernah bertanya-tanya **bagaimana melakukan OCR** pada gambar yang Anda ambil dengan ponsel? Anda tidak sendirian. Baik Anda sedang membuat aplikasi pemindaian struk atau hanya perlu mengekstrak teks dari PDF yang dipindai, **bagaimana melakukan OCR** di Java adalah keterampilan yang cepat memberi hasil. Dalam tutorial ini kami akan membahas contoh praktis yang **mengekstrak teks dari gambar** file, **mengubah gambar menjadi teks**, dan bahkan menunjukkan cara **membaca teks dari jpg** dengan hanya beberapa baris kode.

> *Pro tip:* Pendekatan yang sama bekerja untuk PNG, BMP, atau format apa pun yang didukung mesin OCR—cukup ganti nama file.

## Cara Melakukan OCR di Java – Gambaran Umum

Optical Character Recognition (OCR) adalah teknologi yang mengubah gambar huruf menjadi teks yang sebenarnya dan dapat dicari. Dalam ekosistem Java terdapat beberapa pustaka—Tesseract, Asprise, dan SDK komersial—semua menawarkan alur kerja serupa: memuat gambar, memberi tahu mesin bahasa apa yang diharapkan, menjalankan pengenalan, dan mengambil hasilnya. Di bawah ini kami akan menggunakan kelas generik `OcrEngine` untuk menjaga contoh tetap jelas, tetapi Anda dapat menggantinya dengan implementasi konkret apa pun yang mengikuti pola yang sama.

### Apa yang Akan Anda Pelajari

- Menginstal pustaka OCR (ya, **ocr in java** lebih mudah daripada yang Anda kira).
- Membuat dan mengonfigurasi instance mesin OCR.
- Memuat JPG (atau gambar apa pun) dan mengatur bahasa.
- Memproses gambar dan **mengekstrak teks dari gambar** file.
- Mencetak string yang dikenali ke konsol.

Pada akhir tutorial Anda akan memiliki program Java mandiri yang dapat Anda masukkan ke proyek apa pun dan jalankan secara instan.

![how to perform OCR example](ocr-example.png "how to perform OCR in Java illustration")

## Langkah 1 – Instal dan Impor Pustaka OCR (ocr in java)

Sebelum Anda menulis satu baris kode Java, Anda memerlukan pustaka yang benar‑benar melakukan pekerjaan berat. Jika Anda menggunakan Maven, tambahkan dependensi seperti ini (ganti `com.example.ocr` dengan ID grup yang sebenarnya dari SDK yang Anda pilih):

```xml
<dependency>
    <groupId>com.example</groupId>
    <artifactId>ocr-sdk</artifactId>
    <version>1.4.2</version>
</dependency>
```

Jika Anda lebih suka Gradle:

```gradle
implementation 'com.example:ocr-sdk:1.4.2'
```

Setelah JAR berada di classpath Anda, impor kelas‑kelas yang diperlukan:

```java
import com.example.ocr.OcrEngine;
import com.example.ocr.OcrInputImage;
import com.example.ocr.OcrResult;
```

> **Mengapa ini penting:** Mengimpor kelas yang tepat mencegah error “cannot find symbol” dan membuat IDE Anda senang—tidak ada yang lebih menjengkelkan daripada impor yang hilang ketika Anda sedang mencoba **mengubah gambar menjadi teks**.

## Langkah 2 – Buat Instance Mesin OCR (how to perform OCR)

Sekarang pustaka sudah siap, jalankan mesin. Anggap mesin sebagai otak yang akan melihat piksel dan menebak hurufnya.

```java
// Step 2: Create an OCR engine instance
OcrEngine ocrEngine = new OcrEngine();
```

Membuat mesin biasanya murah; kebanyakan SDK mengalokasikan buffer internal secara malas, sehingga Anda dapat dengan aman menggunakan kembali instance yang sama untuk banyak gambar jika Anda memproses batch.

## Langkah 3 – Muat Gambar dan Atur Bahasa (extract text from image)

Langkah selanjutnya adalah memberi mesin sesuatu untuk dibaca. Di sini kami memuat JPEG dari disk dan memberi tahu mesin OCR bahwa teksnya berbahasa Mongolia (kode ISO 639‑2 “mon”). Anda dapat mengubah jalur atau kode bahasa sesuai kebutuhan Anda.

```java
// Step 3: Load the image you want to recognize
ocrEngine.setImage(new OcrInputImage("YOUR_DIRECTORY/input.jpg"));

// Step 3b: Specify the language (e.g., English = "eng", Mongolian = "mon")
ocrEngine.getSettings().setLanguage("mon");
```

> **Catatan samping:** Jika Anda tidak mengatur bahasa, mesin secara default menggunakan bahasa Inggris, yang dapat secara drastis menurunkan akurasi ketika teks sebenarnya berbahasa Cyrillic atau skrip lain. Selalu tentukan bahasa yang tepat bila memungkinkan.

## Langkah 4 – Proses Gambar dan Dapatkan Hasilnya (convert image to text)

Dengan gambar dan bahasa yang sudah diatur, minta mesin melakukan magisnya. Pemanggilan `process()` menjalankan algoritma OCR dan mengembalikan objek `OcrResult` yang berisi string yang dikenali serta skor kepercayaan.

```java
// Step 4: Process the image and obtain the recognition result
OcrResult ocrResult = ocrEngine.process();
```

Di balik layar, mesin mungkin melakukan pra‑pemrosesan—deskewing, binarisasi, pengurangan noise—sehingga Anda tidak perlu menulis langkah‑langkah tersebut sendiri. Itulah mengapa kebanyakan pustaka OCR modern menyenangkan untuk digunakan dalam tugas **mengubah gambar menjadi teks**.

## Langkah 5 – Keluarkan Teks yang Diekstrak (read text from jpg)

Akhirnya, ambil teks polos dari hasil dan lakukan sesuatu yang berguna dengannya. Untuk demo ini kami cukup mencetaknya ke konsol, tetapi Anda bisa menulisnya ke file, memasukkannya ke indeks pencarian, atau mengirimkannya ke layanan lain.

```java
// Step 5: Output the extracted text
System.out.println(ocrResult.getText());
```

Baris itu saja membuktikan bahwa Anda berhasil **membaca teks dari jpg** (atau format yang didukung apa pun). Jika output terlihat berantakan, periksa kembali kode bahasa dan kualitas gambar.

## Contoh Lengkap yang Berfungsi (Semua Langkah Digabung)

Berikut adalah kelas Java lengkap yang siap dijalankan dan menggabungkan semua bagian. Salin ke file bernama `OcrDemo.java`, sesuaikan jalur gambar dan bahasa, lalu jalankan `javac OcrDemo.java && java OcrDemo`.

```java
import com.example.ocr.OcrEngine;
import com.example.ocr.OcrInputImage;
import com.example.ocr.OcrResult;

/**
 * Demonstrates how to perform OCR in Java using a generic OCR SDK.
 * This example loads a JPG, sets the language to Mongolian, and prints
 * the recognized text to the console.
 *
 * Replace the import package with the actual library you are using.
 */
public class OcrDemo {

    public static void main(String[] args) {
        // Validate command‑line arguments
        if (args.length < 2) {
            System.err.println("Usage: java OcrDemo <image-path> <language-code>");
            System.exit(1);
        }

        String imagePath = args[0];   // e.g., "input.jpg"
        String language = args[1];    // e.g., "mon" for Mongolian

        // Step 1: Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image
        ocrEngine.setImage(new OcrInputImage(imagePath));

        // Step 3: Set the language (ISO‑639‑2)
        ocrEngine.getSettings().setLanguage(language);

        // Step 4: Run the recognition
        OcrResult result = ocrEngine.process();

        // Step 5: Print the extracted text
        System.out.println("=== Recognized Text ===");
        System.out.println(result.getText());
    }
}
```

### Output yang Diharapkan

Jika `input.jpg` berisi frasa Mongolia “Сайн байна уу?” konsol akan menampilkan:

```
=== Recognized Text ===
Сайн байна уу?
```

Jika gambar blur atau kode bahasa salah, Anda akan melihat karakter berantakan atau string kosong—permasalahan umum yang akan kami bahas selanjutnya.

## Masalah Umum dan Cara Memperbaikinya

| Gejala | Penyebab Kemungkinan | Solusi |
|---------|----------------------|--------|
| Karakter Cyrillic berantakan | Kode bahasa salah (default ke Inggris) | Atur `ocrEngine.getSettings().setLanguage("mon")` atau kode yang sesuai. |
| Tidak ada output sama sekali | Jalur gambar tidak tepat atau file tidak dapat dibaca | Verifikasi jalur, pastikan file ada, dan proses memiliki izin membaca. |
| Akurasi rendah (<70 %) | Gambar berkontras rendah atau terrotasi | Pra‑proses gambar: tingkatkan kontras, deskew, atau ubah ke grayscale sebelum diberikan ke mesin. |
| `OutOfMemoryError` pada PDF besar | Memuat banyak halaman resolusi tinggi sekaligus | Proses halaman satu per satu, atau turunkan resolusi gambar sebelum OCR. |

### Pro Tip: Pemrosesan Batch

Jika Anda perlu **mengekstrak teks dari gambar** file secara massal, bungkus logika inti dalam sebuah loop:

```java
for (File img : new File("batchFolder").listFiles()) {
    ocrEngine.setImage(new OcrInputImage(img.getAbsolutePath()));
    OcrResult r = ocrEngine.process();
    System.out.println(r.getText());
}
```

Potongan kode itu menunjukkan betapa mudahnya meningkatkan skala dari satu JPG ke seluruh folder pemindaian.

## Melangkah Lebih Jauh – Apa yang Harus Dijelajahi Selanjutnya?

- **Paket Bahasa:** Kebanyakan SDK OCR memungkinkan Anda mengunduh file data bahasa tambahan. Menambahkan paket baru memungkinkan Anda **mengubah gambar menjadi teks** untuk bahasa di luar Inggris dan Mongolia.
- **PDF OCR:** Gabungkan kode ini dengan Apache PDFBox untuk

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Extract Text Images – OCR Basics with Aspose.OCR for Java](/ocr/english/java/ocr-basics/)
- [Convert Image to Text in Java using Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}