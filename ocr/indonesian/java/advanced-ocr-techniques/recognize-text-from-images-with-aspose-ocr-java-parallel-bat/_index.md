---
category: general
date: 2026-05-31
description: Mengenali teks dari gambar dengan cepat menggunakan Aspose OCR Java.
  Pelajari cara mengekstrak teks dari file PNG dan mengatur bahasa OCR untuk hasil
  optimal.
draft: false
keywords:
- recognize text from images
- extract text from png
- set OCR language
- Aspose OCR Java
- parallel OCR processing
language: id
og_description: Kenali teks dari gambar secara efisien dengan Aspose OCR Java. Tutorial
  ini menunjukkan cara mengekstrak teks dari file PNG dan mengatur bahasa OCR untuk
  pemrosesan batch.
og_title: Mengenali teks dari gambar – Aspose OCR Java Batch Paralel
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: recognize text from images quickly using Aspose OCR Java. Learn how
    to extract text from png files and set OCR language for optimal results.
  headline: recognize text from images with Aspose OCR – Java Parallel Batch Guide
  type: TechArticle
- description: recognize text from images quickly using Aspose OCR Java. Learn how
    to extract text from png files and set OCR language for optimal results.
  name: recognize text from images with Aspose OCR – Java Parallel Batch Guide
  steps:
  - name: How It Works
    text: '- **Thread Count** – The processor creates a thread pool of the size you
      specify. On a quad‑core laptop, `4` is a sweet spot; increase it for servers
      with more cores. - **Language Setting** – By calling `setLanguage(OcrLanguage.FRENCH)`,
      we tell the OCR engine to bias its dictionary toward French ch'
  - name: 1️⃣ Missing or Corrupt Images
    text: If an image path is invalid, `OcrBatchProcessor` throws an `IOException`.
      Wrap the call in a try‑catch block, log the problematic file, and continue with
      the rest of the batch.
  - name: 2️⃣ Mixed Languages in One Batch
    text: 'When you have documents in multiple languages, you can either:'
  - name: 3️⃣ Memory Constraints
    text: Processing very large images (e.g., >10 MB) can inflate heap usage. Pre‑scale
      the images or increase the JVM’s `-Xmx` flag if you encounter `OutOfMemoryError`.
  - name: 4️⃣ Customizing OCR Settings
    text: 'Beyond language, you can tweak recognition speed vs. accuracy:'
  - name: LicenseUtil.java
    text: '```java import com.aspose.ocr.*;'
  - name: ImageProvider.java
    text: '```java import java.util.*;'
  - name: ParallelBatchDemo.java
    text: '```java import com.aspose.ocr.*; import java.util.*;'
  type: HowTo
tags:
- Java
- OCR
- Aspose
- Image Processing
title: Mengenali teks dari gambar dengan Aspose OCR – Panduan Batch Paralel Java
url: /id/java/advanced-ocr-techniques/recognize-text-from-images-with-aspose-ocr-java-parallel-bat/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# mengenali teks dari gambar – Aspose OCR Java Parallel Batch Tutorial

Pernah bertanya-tanya bagaimana cara **mengenali teks dari gambar** tanpa membuat UI Anda terkunci? Mungkin Anda memiliki folder berisi pemindaian, tangkapan layar, atau bahkan campuran file PNG dan JPEG, dan Anda membutuhkan teksnya secepatnya. Kabar baiknya? Dengan Aspose OCR untuk Java Anda dapat membuat batch multi‑thread yang **mengekstrak teks dari png** (dan format lainnya) sambil Anda menikmati secangkir kopi.

Dalam panduan ini kami akan menelusuri contoh lengkap yang siap dijalankan, menunjukkan cara **mengatur bahasa OCR**, memulai empat pekerja paralel, dan mencetak hasilnya. Pada akhir tutorial Anda akan memiliki templat yang solid untuk dimasukkan ke proyek Java apa pun—tanpa tambahan yang tidak perlu, hanya kode yang Anda perlukan.

## Apa yang Akan Anda Pelajari

- Cara menerapkan lisensi Aspose OCR sehingga Anda tidak terhalang oleh batasan evaluasi.  
- Langkah‑langkah tepat untuk **mengenali teks dari gambar** secara paralel, meningkatkan throughput pada mesin multi‑core.  
- Mengapa dan bagaimana **mengatur bahasa OCR** (Prancis dalam demo) untuk akurasi yang lebih baik.  
- Cara praktis **mengekstrak teks dari png**, namun logika yang sama berlaku untuk JPG, TIFF, BMP, dll.  

**Prasyarat** – Anda memerlukan Java 8 atau yang lebih baru, Maven atau Gradle untuk mengambil pustaka Aspose OCR, dan file lisensi Aspose OCR yang valid (`Aspose.OCR.Java.lic`). Tidak diperlukan trik IDE khusus; editor apa pun yang dapat mengompilasi Java sudah cukup.

---

## Langkah 1: Tambahkan Dependensi Aspose OCR

Pertama, pastikan JAR Aspose OCR ada di classpath Anda. Jika menggunakan Maven, tambahkan:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Use the latest stable version -->
</dependency>
```

Untuk Gradle:

```gradle
implementation 'com.aspose:aspose-ocr:23.12'
```

> **Pro tip:** Pantau catatan rilis Aspose; mereka sering menambahkan paket bahasa atau perbaikan performa yang dapat mengurangi beberapa detik dari waktu batch.

## Langkah 2: Terapkan Lisensi Aspose OCR

Tanpa lisensi pustaka berjalan dalam mode demo dan akan menambahkan watermark pada output. Muat file lisensi Anda sekali, sebaiknya saat aplikasi mulai.

```java
import com.aspose.ocr.*;

public class LicenseUtil {
    /** Loads the Aspose OCR license from the given path. */
    public static void applyLicense(String licensePath) throws Exception {
        License license = new License();
        license.setLicense(licensePath);
        System.out.println("Aspose OCR license applied successfully.");
    }
}
```

Memanggil `LicenseUtil.applyLicense("Aspose.OCR.Java.lic")` memastikan setiap panggilan **mengenali teks dari gambar** berikutnya berjalan tanpa batasan.

## Langkah 3: Siapkan Daftar Gambar

Anda dapat memberi batch processor koleksi jalur file apa pun. Di bawah ini kami mendemonstrasikan **mengekstrak teks dari png** bersama file JPEG dan TIFF—ganti jalur dengan direktori Anda sendiri.

```java
import java.util.*;

public class ImageProvider {
    /** Returns a list of absolute image paths to be processed. */
    public static List<String> getImagePaths() {
        return Arrays.asList(
            "YOUR_DIRECTORY/doc1.png",   // PNG – our primary example
            "YOUR_DIRECTORY/doc2.jpg",
            "YOUR_DIRECTORY/doc3.tif"
        );
    }
}
```

> **Mengapa List?** `OcrBatchProcessor` mengharapkan `List<String>` sehingga dapat membagi pekerjaan ke thread secara otomatis.

## Langkah 4: Konfigurasi dan Jalankan Parallel Batch Processor

Sekarang masuk ke inti tutorial: membuat `OcrBatchProcessor`, menentukan berapa banyak thread yang akan dibuat, dan **mengatur bahasa OCR** ke Prancis (ubah ke `OcrLanguage.ENGLISH` atau bahasa lain yang didukung sesuai kebutuhan).

```java
import com.aspose.ocr.*;

public class ParallelBatchDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Apply the license
        LicenseUtil.applyLicense("Aspose.OCR.Java.lic");

        // 2️⃣ Gather image files
        List<String> imagePaths = ImageProvider.getImagePaths();

        // 3️⃣ Create and configure the batch processor
        OcrBatchProcessor batchProcessor = new OcrBatchProcessor();
        batchProcessor.setThreadCount(4);                 // 4 parallel workers
        batchProcessor.setLanguage(OcrLanguage.FRENCH);   // set OCR language

        // 4️⃣ Run OCR on the entire batch – this is where we **recognize text from images**
        List<OcrResult> ocrResults = batchProcessor.recognize(imagePaths);

        // 5️⃣ Output the recognized text for each file
        for (int i = 0; i < ocrResults.size(); i++) {
            System.out.println("File: " + imagePaths.get(i));
            System.out.println(ocrResults.get(i).getText());
            System.out.println("---");
        }
    }
}
```

### Cara Kerjanya

- **Jumlah Thread** – Processor membuat pool thread dengan ukuran yang Anda tentukan. Pada laptop quad‑core, `4` adalah titik optimal; tingkatkan untuk server dengan lebih banyak core.  
- **Pengaturan Bahasa** – Dengan memanggil `setLanguage(OcrLanguage.FRENCH)`, kami memberi tahu mesin OCR untuk memprioritaskan kamus bahasa Prancis, yang secara dramatis meningkatkan akurasi untuk dokumen non‑Inggris.  
- **Batch Recognition** – Metode `recognize` secara internal melakukan loop atas daftar yang diberikan, mendistribusikan pekerjaan, dan mengembalikan `List<OcrResult>` yang mempertahankan urutan asli. Ini adalah cara paling sederhana untuk **mengenali teks dari gambar** tanpa menulis kode manajemen thread sendiri.

## Langkah 5: Verifikasi Output

Saat Anda menjalankan program, seharusnya muncul sesuatu seperti:

```
File: YOUR_DIRECTORY/doc1.png
Bonjour le monde! Ceci est un test d'OCR.
---
File: YOUR_DIRECTORY/doc2.jpg
Hello world! This is an OCR test.
---
File: YOUR_DIRECTORY/doc3.tif
¡Hola mundo! Prueba de OCR.
---
```

Jika file Prancis (`doc1.png`) berisi teks berbahasa Prancis, langkah **mengatur bahasa OCR** akan membantu menangkap karakter aksen dengan benar. Untuk file PNG, ini menunjukkan cara bersih **mengekstrak teks dari png** sambil menangani format lain dalam batch yang sama.

---

## Menangani Kasus Edge Umum

### 1️⃣ Gambar Hilang atau Rusak

Jika jalur gambar tidak valid, `OcrBatchProcessor` akan melempar `IOException`. Bungkus panggilan dalam blok try‑catch, log file yang bermasalah, dan lanjutkan dengan sisa batch.

```java
try {
    List<OcrResult> results = batchProcessor.recognize(imagePaths);
} catch (IOException ex) {
    System.err.println("Failed to process: " + ex.getMessage());
}
```

### 2️⃣ Bahasa Campuran dalam Satu Batch

Ketika Anda memiliki dokumen dalam beberapa bahasa, Anda dapat:

- Menjalankan batch terpisah, masing‑masing dengan `setLanguage` sendiri.  
- Atau membiarkan bahasa tidak diatur (`OcrLanguage.AUTO_DETECT`) dan membiarkan Aspose menebak, meskipun akurasi mungkin menurun.

### 3️⃣ Kendala Memori

Memproses gambar sangat besar (misalnya >10 MB) dapat meningkatkan penggunaan heap. Skala ulang gambar terlebih dahulu atau tingkatkan flag JVM `-Xmx` jika Anda menemui `OutOfMemoryError`.

```bash
java -Xmx2g -cp yourapp.jar ParallelBatchDemo
```

### 4️⃣ Menyesuaikan Pengaturan OCR

Selain bahasa, Anda dapat menyesuaikan kecepatan vs. akurasi pengenalan:

```java
batchProcessor.setRecognitionMode(OcrRecognitionMode.ACCURATE); // default is BALANCED
```

Memilih `ACCURATE` lebih lambat tetapi menghasilkan hasil yang lebih baik untuk pemindaian yang berisik.

---

## Contoh Kerja Lengkap (Semua File)

Berikut adalah set lengkap file sumber yang Anda perlukan. Salin ke proyek Maven, sesuaikan jalur lisensi dan direktori gambar, lalu jalankan `mvn exec:java -Dexec.mainClass=ParallelBatchDemo`.

### LicenseUtil.java
```java
import com.aspose.ocr.*;

public class LicenseUtil {
    public static void applyLicense(String licensePath) throws Exception {
        License license = new License();
        license.setLicense(licensePath);
        System.out.println("Aspose OCR license applied successfully.");
    }
}
```

### ImageProvider.java
```java
import java.util.*;

public class ImageProvider {
    public static List<String> getImagePaths() {
        return Arrays.asList(
            "YOUR_DIRECTORY/doc1.png",
            "YOUR_DIRECTORY/doc2.jpg",
            "YOUR_DIRECTORY/doc3.tif"
        );
    }
}
```

### ParallelBatchDemo.java
```java
import com.aspose.ocr.*;
import java.util.*;

public class ParallelBatchDemo {
    public static void main(String[] args) throws Exception {
        // Apply license
        LicenseUtil.applyLicense("Aspose.OCR.Java.lic");

        // Gather images
        List<String> imagePaths = ImageProvider.getImagePaths();

        // Configure batch processor
        OcrBatchProcessor batchProcessor = new OcrBatchProcessor();
        batchProcessor.setThreadCount(4);                 // Parallelism
        batchProcessor.setLanguage(OcrLanguage.FRENCH);   // set OCR language

        // Recognize text from images
        List<OcrResult> ocrResults = batchProcessor.recognize(imagePaths);

        // Output results
        for (int i = 0; i < ocrResults.size(); i++) {
            System.out.println("File: " + imagePaths.get(i));
            System.out.println(ocrResults.get(i).getText());
            System.out.println("---");
        }
    }
}
```

Jalankan, dan Anda akan melihat teks yang diekstrak dari setiap file dicetak ke konsol—tepat apa yang Anda butuhkan saat membangun arsip yang dapat dicari, otomatisasi entri data, atau alat aksesibilitas.

---

## Kesimpulan

Kami baru saja membahas pola lengkap yang siap produksi untuk **mengenali teks dari gambar** menggunakan Aspose OCR untuk Java. Dengan mengonfigurasi batch processor, Anda dapat **mengekstrak teks dari png** (dan format lain) secara paralel, dan kemampuan **mengatur bahasa OCR** memastikan Anda mendapatkan akurasi tertinggi untuk beban kerja multibahasa.

Langkah selanjutnya? Coba ganti bahasa ke `OcrLanguage.SPANISH` atau bereksperimen dengan `OcrRecognitionMode.ACCURATE` untuk pemindaian yang lebih sulit. Anda juga dapat mengintegrasikan hasil ke basis data, mengirimnya ke indeks pencarian, atau mengalirkannya ke API terjemahan.

Punya skenario rumit—seperti OCR pada PDF atau pada gambar yang disimpan di cloud? Itu merupakan ekstensi alami dari apa yang kami bangun hari ini. Selami, sesuaikan pengaturan, dan biarkan mesin OCR melakukan pekerjaan berat.

Selamat coding, semoga ekstraksi teks Anda cepat dan tepat!

## Apa yang Harus Anda Pelajari Selanjutnya?

- [Extract Text Images – OCR Basics with Aspose.OCR for Java](/ocr/english/java/ocr-basics/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [recognize text image with Aspose OCR – Full Java OCR Tutorial](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}