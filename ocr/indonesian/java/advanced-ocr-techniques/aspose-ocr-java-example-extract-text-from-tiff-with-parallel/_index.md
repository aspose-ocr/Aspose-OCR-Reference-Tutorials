---
category: general
date: 2026-06-25
description: Contoh Aspose OCR Java yang menunjukkan cara mengekstrak teks dari file
  TIFF, mengonfigurasi pengaturan OCR, dan mengaktifkan pemrosesan OCR paralel untuk
  hasil yang lebih cepat.
draft: false
keywords:
- aspose ocr java example
- how to extract text
- extract text from tiff
- how to configure ocr
- parallel ocr processing
language: id
og_description: Contoh Aspose OCR Java yang menunjukkan cara mengekstrak teks dari
  gambar TIFF, mengonfigurasi OCR, dan menjalankan pemrosesan OCR paralel untuk kinerja
  optimal.
og_title: Contoh OCR Aspose Java – Ekstraksi Teks Cepat dari TIFF
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Aspose OCR Java example showing how to extract text from TIFF files,
    configure OCR settings, and enable parallel OCR processing for faster results.
  headline: Aspose OCR Java Example – Extract Text from TIFF with Parallel Processing
  type: TechArticle
- description: Aspose OCR Java example showing how to extract text from TIFF files,
    configure OCR settings, and enable parallel OCR processing for faster results.
  name: Aspose OCR Java Example – Extract Text from TIFF with Parallel Processing
  steps:
  - name: '**Add Aspose OCR to your project**'
    text: '**Add Aspose OCR to your project**'
  - name: '**Compile and execute**'
    text: '**Compile and execute**'
  - name: '**Observe the console** – you should see the OCR output sandwiched between
      the `=== OCR Output Start ===` markers.'
    text: '**Observe the console** – you should see the OCR output sandwiched between
      the `=== OCR Output Start ===` markers.'
  type: HowTo
tags:
- Aspose OCR
- Java
- Text Extraction
title: Contoh Aspose OCR Java – Ekstrak Teks dari TIFF dengan Pemrosesan Paralel
url: /id/java/advanced-ocr-techniques/aspose-ocr-java-example-extract-text-from-tiff-with-parallel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Contoh Aspose OCR Java – Ekstrak Teks dari TIFF dengan Pemrosesan Paralel

Pernah bertanya‑tanya **bagaimana mengekstrak teks** dari dokumen hasil scan yang sangat besar tanpa aplikasi Anda melambat? Anda tidak sendirian. Dalam **contoh Aspose OCR Java** ini kita akan membahas cara mengonfigurasi mesin OCR, mengaktifkan pemrosesan paralel, dan mengambil teks Unicode bersih dari file TIFF multi‑megabyte—semua dalam beberapa baris kode.

Anggap saja ini memberi aplikasi Java Anda pemindai turbo‑charged yang dapat menggerogoti halaman sambil Anda menyeruput kopi. Pada akhir panduan ini Anda akan memiliki program yang dapat dijalankan, memahami mengapa setiap pengaturan penting, dan tahu cara menyesuaikannya untuk beban kerja Anda sendiri.

---

## Apa yang Anda Butuhkan Sebelum Memulai

Sebelum kita masuk ke kode, pastikan Anda memiliki:

- **Java 17** (atau JDK terbaru) yang terpasang dan sudah ditambahkan ke `PATH`.
- Lisensi **Aspose.OCR for Java** atau kunci evaluasi gratis. Anda dapat mengambilnya dari portal Aspose.
- **Gambar TIFF besar** (`large_scan.tif`) yang ingin Anda uji—sebaiknya berukuran beberapa megabyte agar pemrosesan paralel terlihat manfaatnya.
- Alat build seperti **Maven** atau **Gradle** untuk mengunduh pustaka Aspose OCR.

Itu saja. Tidak ada mesin OCR berat atau DLL native yang harus diatur. Siap? Mari kita mulai.

---

## Contoh Aspose OCR Java: Penjelasan Kode Lengkap

Berikut adalah program Java lengkap yang berdiri sendiri. Salin‑tempel ke file bernama `ParallelOcrDemo.java`, sesuaikan jalur gambar, dan Anda siap menjalankannya.

```java
// ParallelOcrDemo.java
// Demonstrates an Aspose OCR Java example with parallel processing.

import com.aspose.ocr.*;
import com.aspose.ocr.config.*;
import com.aspose.ocr.results.*;

public class ParallelOcrDemo {
    public static void main(String[] args) {
        // -------------------------------------------------------------
        // Step 1: Create OCR configuration and enable parallel processing
        // -------------------------------------------------------------
        OcrConfig config = new OcrConfig()
                // ParallelSettings lets us run up to 8 threads simultaneously.
                .setParallelSettings(new ParallelSettings()
                        .setMaxThreads(8)); // Adjust based on CPU cores.

        // -------------------------------------------------------------
        // Step 2: Initialise the Aspose OCR engine with the configuration
        // -------------------------------------------------------------
        AsposeOCR ocrEngine = new AsposeOCR(config);

        // -------------------------------------------------------------
        // Step 3: Recognise text from a large image (extract text from tiff)
        // -------------------------------------------------------------
        // Replace the path with your actual TIFF file location.
        ImageRecognitionResult result = ocrEngine.recognizeImage("YOUR_DIRECTORY/large_scan.tif");

        // -------------------------------------------------------------
        // Step 4: Output the recognised text (how to extract text)
        // -------------------------------------------------------------
        System.out.println("=== OCR Output Start ===");
        System.out.println(result.getText());
        System.out.println("=== OCR Output End ===");
    }
}
```

> **Output yang diharapkan** (dipotong untuk singkat):  
> ```
> === OCR Output Start ===
> Lorem ipsum dolor sit amet, consectetur adipiscing elit...
> === OCR Output End ===
> ```

> **Ilustrasi gambar**  
> ![Contoh Aspose OCR Java memproses gambar](https://example.com/images/aspose-ocr-java-example.png)

> *Teks alternatif:* Contoh Aspose OCR Java menunjukkan pemrosesan paralel gambar TIFF.

---

## Cara Mengonfigurasi OCR untuk Pemrosesan Paralel OCR

Baris `new ParallelSettings().setMaxThreads(8)` adalah inti dari **pemrosesan OCR paralel**. Mengapa ini penting?

- **Pemanfaatan CPU:** Server modern sering memiliki CPU 8‑core. Dengan memunculkan hingga delapan thread, mesin dapat mendekode beberapa fragmen gambar sekaligus, memotong waktu eksekusi secara signifikan.
- **Pertimbangan memori:** Setiap thread menyimpan salinan buffer internal. Jika Anda berada pada mesin dengan memori terbatas, turunkan jumlah thread (`setMaxThreads(4)`) untuk menghindari `OutOfMemoryError`.
- **Keamanan thread:** Aspose OCR sudah thread‑safe secara default, jadi Anda tidak memerlukan kode sinkronisasi tambahan.

Jika Anda perlu memproses sekumpulan file, cukup bungkus pemanggilan `recognizeImage` di dalam `ExecutorService` Java dan gunakan kembali instance `AsposeOCR` yang sama—berkat pool thread internal yang telah Anda konfigurasikan.

---

## Cara Mengekstrak Teks dari File TIFF

TIFF (Tagged Image File Format) menjadi pilihan utama untuk dokumen hasil scan karena dapat menyimpan banyak halaman dan data lossless. Namun, tidak semua pustaka OCR menangani TIFF multi‑page dengan baik.

Aspose OCR secara otomatis mendeteksi tipe gambar dan, ketika diberikan TIFF multi‑page, memproses setiap halaman secara berurutan *di dalam* mesin paralel. Itu berarti Anda mendapatkan manfaat multi‑threading tanpa menulis kode looping tambahan.

Jika Anda hanya membutuhkan halaman pertama, berikan objek `PageOptions`:

```java
ImageRecognitionResult result = ocrEngine.recognizeImage(
        "YOUR_DIRECTORY/large_scan.tif",
        new ImageRecognitionOptions().setPageNumber(1));
```

Namun untuk pengalaman **ekstrak teks dari tiff** secara lengkap, biarkan opsi tersebut kosong seperti pada contoh.

---

## Cara Memverifikasi Hasil Ekstraksi Teks

Setelah mesin OCR selesai, `result.getText()` mengembalikan sebuah `String` biasa. Anda dapat:

- Menulisnya ke file `.txt` menggunakan `Files.writeString(Path.of("output.txt"), result.getText());`.
- Mengirimkannya ke pipeline NLP selanjutnya.
- Mencarinya dengan Lucene untuk pengambilan dokumen yang cepat.

Ingat untuk memangkas spasi putih jika Anda berencana menggabungkan hasil dari beberapa halaman:

```java
String cleaned = result.getText().trim();
```

---

## Kesalahan Umum dan Tips Profesional

| Kesalahan | Mengapa Terjadi | Solusi |
|-----------|----------------|--------|
| **Crash out‑of‑memory** | Terlalu banyak thread pada VM dengan RAM rendah. | Kurangi `setMaxThreads` atau tingkatkan heap (`-Xmx2g`). |
| **Output kosong** | Jalur gambar salah atau file tidak dapat diakses. | Periksa jalur absolut dan izin file. |
| **Karakter aneh** | TIFF sumber menggunakan enkoding yang tidak didukung. | Pra‑proses dengan ImageMagick untuk memastikan grayscale 8‑bit. |
| **Performa lambat pada mesin single‑core** | Paralelisme menambah overhead. | Setel `setMaxThreads(1)` untuk lingkungan satu core. |

Tips cepat: selalu panggil `ocrEngine.dispose()` (atau gunakan try‑with‑resources jika Anda membungkusnya) untuk membebaskan sumber daya native setelah selesai. Kebiasaan kecil ini mencegah kebocoran memori pada layanan yang berjalan lama.

---

## Menjalankan Contoh

1. **Tambahkan Aspose OCR ke proyek Anda**  
   Maven:  
   ```xml
   <dependency>
       <groupId>com.aspose</groupId>
       <artifactId>aspose-ocr</artifactId>
       <version>23.10</version>
   </dependency>
   ```  
   Gradle:  
   ```groovy
   implementation 'com.aspose:aspose-ocr:23.10'
   ```

2. **Kompilasi dan eksekusi**  
   ```bash
   javac -cp ".:path/to/aspose-ocr.jar" ParallelOcrDemo.java
   java -cp ".:path/to/aspose-ocr.jar" ParallelOcrDemo
   ```

3. **Amati konsol** – Anda akan melihat output OCR terletak di antara penanda `=== OCR Output Start ===`.

Jika output terlihat berantakan, pastikan TIFF Anda bukan varian terkompresi yang tidak didukung oleh versi pustaka saat ini. Memperbarui ke rilis Aspose OCR terbaru biasanya memperbaiki kasus semacam ini.

---

## Langkah Selanjutnya – Memperluas Contoh Aspose OCR Java

Setelah menguasai dasar‑dasarnya, pertimbangkan percobaan lanjutan berikut:

- **Pemrosesan batch:** Loop melalui direktori berisi TIFF, simpan setiap hasil ke basis data.
- **Paket bahasa:** Muat model bahasa tambahan (`ocrEngine.addLanguage(Language.Spanish);`) untuk meningkatkan akurasi pada dokumen non‑English.
- **Pra‑pemrosesan gambar:** Gunakan `java.awt` atau OpenCV untuk mengoreksi kemiringan, menghilangkan noise, atau meningkatkan kontras sebelum memberi gambar ke mesin OCR.
- **Integrasi dengan Spring Boot:** Ekspos endpoint REST yang menerima gambar unggahan dan mengembalikan teks yang diekstrak secara instan.

Masing‑masing topik ini secara alami terhubung kembali ke **cara mengonfigurasi OCR** dan **strategi pemrosesan paralel OCR**, memberi Anda pipeline yang kuat dan siap produksi.

---

## Kesimpulan

Dalam **contoh Aspose OCR Java** ini kami membahas semua yang perlu Anda ketahui untuk **mengekstrak teks** dari file TIFF besar, mengonfigurasi mesin OCR untuk kinerja optimal, dan memanfaatkan **pemrosesan OCR paralel** agar aplikasi Anda tetap responsif. Dengan mengikuti kode langkah‑demi‑langkah, menyesuaikan jumlah thread, dan menghindari jebakan umum, Anda dapat menyematkan OCR berkecepatan tinggi ke layanan Java apa pun hari ini.

Cobalah, ubah pengaturannya, dan biarkan mesin OCR melakukan pekerjaan berat sementara Anda fokus membangun fitur intelijen dokumen berikutnya. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang dapat dijalankan dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Extract Text Images – OCR Basics with Aspose.OCR for Java](/ocr/english/java/ocr-basics/)
- [How to recognize tiff with Aspose.OCR for Java](/ocr/english/java/ocr-operations/recognize-tiff/)
- [How to Use OCR - Advanced Techniques with Aspose.OCR for Java](/ocr/english/java/advanced-ocr-techniques/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}