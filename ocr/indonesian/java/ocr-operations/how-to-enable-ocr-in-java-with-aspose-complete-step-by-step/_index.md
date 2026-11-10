---
category: general
date: 2026-03-18
description: Cara mengaktifkan OCR dengan cepat menggunakan Aspose OCR untuk Java.
  Pelajari cara mengenali teks dari gambar, mengatur paralelisme maksimum, mengekstrak
  teks dari PNG, dan memuat gambar untuk OCR.
draft: false
keywords:
- how to enable OCR
- recognize text from image
- set max parallelism
- extract text from png
- load image for OCR
language: id
og_description: Cara mengaktifkan OCR dengan Aspose OCR untuk Java. Panduan ini menunjukkan
  cara mengenali teks dari gambar, mengatur paralelisme maksimum, mengekstrak teks
  dari PNG, dan memuat gambar untuk OCR.
og_title: Cara Mengaktifkan OCR di Java – Tutorial Lengkap
tags:
- Aspose OCR
- Java
- Parallel Processing
title: Cara Mengaktifkan OCR di Java dengan Aspose – Panduan Lengkap Langkah demi
  Langkah
url: /id/java/ocr-operations/how-to-enable-ocr-in-java-with-aspose-complete-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Mengaktifkan OCR di Java – Panduan Langkah‑per‑Langkah Lengkap

Pernah bertanya-tanya **bagaimana cara mengaktifkan OCR** di aplikasi Java Anda tanpa menghabiskan hari menggali dokumentasi API? Anda bukan satu-satunya. Kebanyakan pengembang menemui kebuntuan ketika mereka perlu **mengenali teks dari gambar**—terutama PNG berukuran besar—sementara tetap menjaga kinerja yang dapat diterima.  

Berita baik? Dengan Aspose OCR Anda dapat mengaktifkannya, memuat gambar untuk OCR, dan bahkan meningkatkan jumlah core CPU untuk mempercepat proses. Dalam tutorial ini kami akan membahas semua yang Anda perlukan: menginstal pustaka, memuat PNG, mengatur tingkat paralelisme maksimum, dan akhirnya mengekstrak teks. Pada akhir tutorial Anda akan memiliki program yang dapat dijalankan yang **mengekstrak teks dari PNG** dalam sekejap.

### Apa yang Anda Butuhkan

- Java 17 atau lebih baru (kode dapat dikompilasi dengan versi lebih lama, tetapi 17 adalah pilihan terbaik)
- Maven atau Gradle untuk mengunduh Aspose OCR JAR (kami akan menunjukkan Maven)
- Gambar PNG yang berisi teks yang dapat dicari (semakin besar, semakin baik untuk paralelisme)
- Sedikit rasa ingin tahu—tidak diperlukan pengalaman OCR sebelumnya

Jika ada yang terdengar asing, jangan panik. Kami akan membahas prasyaratnya segera setelah pengantar dan memberi Anda perintah cepat untuk menyiapkannya.

---

## Langkah 1: Instal Aspose OCR untuk Java

Sebelum Anda dapat **mengaktifkan OCR**, pustaka harus berada di classpath Anda. Cara termudah adalah menambahkan dependensi Maven:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Check the latest version on Maven Central -->
</dependency>
```

> **Pro tip:** Jika Anda menggunakan Gradle, setaraannya adalah  
> `implementation 'com.aspose:aspose-ocr:23.12'`.  

Setelah dependensi teratasi, IDE Anda akan mengunduh JAR secara otomatis. Tidak diperlukan penanganan JAR manual.

## Langkah 2: Muat Gambar untuk OCR

Langkah praktis pertama adalah **memuat gambar untuk OCR**. Aspose menyediakan metode statis `Image.load` yang menerima jalur file atau aliran. Mari kita sederhanakan dengan menggunakan jalur file:

```java
import com.aspose.ocr.Image;

// ...

// Replace with the absolute or relative path to your PNG
String imagePath = "src/main/resources/large-document.png";
Image image = Image.load(imagePath);
```

> **Mengapa ini penting:** Memuat gambar sekali dan menggunakan kembali instance `Image` yang sama menghindari I/O tambahan ketika Anda kemudian menjalankan beberapa pengenalan pada file yang sama (mis., pengaturan bahasa yang berbeda).

Jika file tidak ditemukan, Aspose akan melempar `IOException`. Dalam produksi Anda akan membungkusnya dalam try‑catch dan mungkin beralih ke gambar default.

## Langkah 3: Buat OCR Engine dan Aktifkan Pemrosesan Paralel

Sekarang kita sampai pada inti masalah—**bagaimana cara mengaktifkan OCR** dengan paralelisme. Kelas `OcrEngine` melakukan pekerjaan berat, dan `ParallelSettings`-nya memungkinkan Anda mengontrol threading.

```java
import com.aspose.ocr.OcrEngine;
import com.aspose.ocr.ParallelSettings;

// ...

OcrEngine ocrEngine = new OcrEngine();

// Turn on parallel processing
ParallelSettings parallelSettings = new ParallelSettings();
parallelSettings.setEnabled(true);

// Set the maximum number of threads to the number of available CPU cores
int cores = Runtime.getRuntime().availableProcessors();
parallelSettings.setMaxDegreeOfParallelism(cores);

// Apply the settings to the engine
ocrEngine.setParallelSettings(parallelSettings);
```

### Mengapa mengatur `MaxDegreeOfParallelism`?

- **Kinerja:** PNG besar dapat berisi ribuan fragmen teks. Secara default Aspose memprosesnya secara berurutan, yang dapat lambat pada mesin multi‑core.
- **Kontrol:** Anda mungkin ingin membatasi thread pada server bersama untuk menghindari kelaparan layanan lain. Sesuaikan `cores` sesuai kebutuhan.

## Langkah 4: Kenali Teks dari Gambar

Dengan engine yang siap, panggilan OCR sebenarnya hanya satu baris:

```java
String recognizedText = ocrEngine.recognize(image);
```

Di balik layar, Aspose membagi gambar menjadi blok, menjalankan setiap blok melalui jaringan sarafnya, dan menyatukan hasilnya. Karena kami mengaktifkan paralelisme, blok‑blok tersebut diproses secara bersamaan.

## Langkah 5: Output atau Simpan Teks yang Diekstrak

Akhirnya, tentukan apa yang akan dilakukan dengan hasilnya. Untuk demo cepat kami akan mencetak ke konsol, tetapi Anda dapat menulis ke file, basis data, atau bahkan mengirimnya ke pipeline NLP berikutnya.

```java
System.out.println("=== OCR Result ===");
System.out.println(recognizedText);
```

Jika Anda perlu **mengekstrak teks dari PNG** secara massal, cukup bungkus langkah‑langkah di atas dalam loop yang mengiterasi direktori. Ingat untuk menggunakan kembali instance `OcrEngine` yang sama—membuat engine baru untuk setiap file menghilangkan tujuan paralelisme.

## Contoh Kerja Lengkap

Menggabungkan semuanya, berikut kelas Java lengkap yang siap dijalankan. Salin‑tempel ke `src/main/java/com/example/ParallelOcrDemo.java` dan jalankan `mvn compile exec:java`.

```java
package com.example;

import com.aspose.ocr.OcrEngine;
import com.aspose.ocr.ParallelSettings;
import com.aspose.ocr.Image;

/**
 * Demonstrates how to enable OCR with Aspose, set max parallelism,
 * load an image for OCR, and extract text from a PNG file.
 */
public class ParallelOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Enable parallel processing to speed up recognition
        ParallelSettings parallelSettings = new ParallelSettings();
        parallelSettings.setEnabled(true);
        // Use all available CPU cores; adjust if you need to limit resources
        parallelSettings.setMaxDegreeOfParallelism(
                Runtime.getRuntime().availableProcessors()
        );
        ocrEngine.setParallelSettings(parallelSettings);

        // Step 3: Load the image that contains the text to be recognized
        // Replace the path with your own PNG file location
        Image image = Image.load("src/main/resources/large-document.png");

        // Step 4: Perform OCR on the loaded image
        String recognizedText = ocrEngine.recognize(image);

        // Step 5: Output the recognized text
        System.out.println("=== OCR Result ===");
        System.out.println(recognizedText);
    }
}
```

### Output yang Diharapkan

Jika `large-document.png` berisi frasa “Hello World”, Anda akan melihat sesuatu seperti:

```
=== OCR Result ===
Hello World
```

Untuk pemindaian multi‑halaman, output akan menjadi satu string dengan pemisah baris (`\n`) yang memisahkan setiap baris teks.

## Pertanyaan Umum & Kasus Tepi

| Question | Answer |
|----------|--------|
| **Bagaimana jika PNG sangat besar (mis., 10 000 × 10 000 px)?** | Aspose secara otomatis memotong gambar menjadi ubin. Anda dapat mengontrol ukuran ubin melalui `OcrEngine.setTileSize(int width, int height)` jika memerlukan kontrol yang lebih halus. |
| **Bisakah saya membatasi penggunaan memori?** | Ya—atur `ocrEngine.setMemoryLimit(long bytes)` untuk menghindari kesalahan OutOfMemory pada mesin dengan spesifikasi rendah. |
| **Apakah paralelisme bekerja di Windows dan Linux secara sama?** | Tentu saja. Abstraksi `ParallelSettings` menggunakan `ForkJoinPool` Java, yang bersifat lintas‑platform. |
| **Bahasa apa yang didukung?** | Lebih dari 100 bahasa tersedia langsung. Panggil `ocrEngine.setLanguage("eng")` untuk bahasa Inggris, `"spa"` untuk bahasa Spanyol, dll. |
| **Saya hanya ingin mengenali angka.** | Gunakan `ocrEngine.setCharacterWhitelist("0123456789")` untuk membatasi set karakter. |

## Tips untuk OCR Siap Produksi

1. **Cache `OcrEngine`** – Membuatnya berulang kali menambah overhead. Simpan sebagai singleton jika Anda memproses banyak gambar.
2. **Validasi Input** – Periksa ukuran file dan dimensi sebelum memberi ke engine; file yang sangat besar masih dapat membuat JVM kehabisan memori meskipun ada paralelisme.
3. **Penyesuaian Thread Pool** – Jika aplikasi Anda berbagi JVM dengan layanan lain, pertimbangkan mengatur `parallelSettings.setMaxDegreeOfParallelism(Runtime.getRuntime().availableProcessors() / 2)` agar menjadi warga yang baik.
4. **Pasca‑Pemrosesan** – OCR tidak sempurna. Gunakan pemeriksa ejaan atau pembersihan regex untuk meningkatkan akurasi, terutama untuk tabel yang dipindai.

## Kesimpulan

Kami telah membahas **bagaimana cara mengaktifkan OCR** di Java menggunakan Aspose, mendemonstrasikan cara **mengenali teks dari gambar**, menunjukkan cara **mengatur paralelisme maksimum** untuk pemrosesan lebih cepat, menjelaskan cara **mengekstrak teks dari PNG**, dan menggambarkan cara yang tepat untuk **memuat gambar untuk OCR**. Potongan kode lengkap di atas siap dijalankan, dan konsepnya berlaku untuk proyek Java apa pun yang membutuhkan ekstraksi teks yang cepat dan andal.

Siap untuk langkah selanjutnya? Coba proses seluruh folder PNG, bereksperimen dengan paket bahasa yang berbeda, atau alirkan output OCR ke indeks pencarian. Tidak ada batasan setelah Anda menguasai dasar-dasarnya.

Ada pertanyaan atau mengalami masalah? Tinggalkan komentar, dan mari kita selesaikan bersama. Selamat coding!  

![how to enable OCR illustration](https://example.com/placeholder-image.png "how to enable OCR in Java with Aspose")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}