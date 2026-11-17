---
category: general
date: 2026-08-28
description: Pelajari cara mengekstrak teks dari gambar png di Java menggunakan Aspose
  OCR. Tutorial ini mencakup pemrosesan OCR batch, membaca gambar dari folder, dan
  memfilter file berdasarkan ekstensi.
draft: false
keywords:
- extract text from png
- read images from folder
- filter files by extension
- how to batch ocr
- aspose ocr java tutorial
lastmod: 2026-08-28
og_description: Pelajari cara mengekstrak teks dari gambar png di Java menggunakan
  Aspose OCR. Tutorial ini mencakup pemrosesan OCR batch, membaca gambar dari folder,
  dan memfilter file berdasarkan ekstensi.
og_image_alt: 'Developer guide: extract text from png images in Java using Aspose
  OCR'
og_title: Cara mengekstrak teks dari png di Java – panduan batch OCR
schemas:
- author: Aspose
  dateModified: '2026-08-28'
  description: Learn how to extract text from png images in Java using Aspose OCR.
    This tutorial covers batch OCR processing, reading images from a folder, and filtering
    files by extension.
  headline: How to extract text from png in Java – batch OCR guide
  type: TechArticle
- questions:
  - answer: Absolutely. Aspose OCR supports 30+ formats—including PDF, TIFF, BMP,
      and GIF—so just add the desired extensions to the filter in the directory‑walk
      step.
    question: Can I process PDFs or TIFFs as well?
  - answer: Change `RecognitionLanguage.ENGLISH` to `RecognitionLanguage.SPANISH`
      (or any supported language). The language packs are bundled with the library,
      so no extra download is required.
    question: What if I need a language other than English, such as Spanish?
  - answer: Yes. `Files.walk` traverses the entire tree recursively, so every nested
      PNG/J
    question: My folder contains sub‑folders—will they be scanned?
  - answer: Enable streaming mode by calling `ocrEngine.setUseStreaming(true)`. This
      tells the engine to read the image in chunks, dramatically reducing peak memory
      usage.
    question: How do I handle extremely large images that exceed 200 MB?
  - answer: Yes. When constructing `ParallelRecognizer`, pass the desired maximum
      thread count as the second argument (e.g., `new ParallelRecognizer(ocrEngine,
      4)`).
    question: Is there a way to limit the number of concurrent OCR threads?
  type: FAQPage
tags:
- OCR
- Java
- Aspose
title: Cara mengekstrak teks dari png di Java – panduan batch OCR
url: /id/java/ocr-operations/convert-images-to-text-in-java-batch-ocr-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara mengekstrak teks dari png di Java – panduan batch OCR

Jika Anda pernah perlu **mengekstrak teks dari png** tetapi tidak yakin bagaimana memperluas operasi di luar beberapa gambar, Anda berada di tempat yang tepat. Banyak pengembang memulai dengan panggilan OCR satu‑gambar dan cepat menemui batas kinerja ketika folder tumbuh menjadi puluhan atau ratusan file. Dengan Aspose OCR untuk Java Anda dapat membuat pipeline batch OCR yang kuat yang menelusuri direktori, menyaring hanya tipe gambar yang Anda inginkan, menjalankan pengenalan secara paralel, dan mengembalikan hasil dalam urutan yang sama dengan file sumber. Pada akhir panduan ini Anda akan memiliki potongan kode Java siap pakai yang menangani **pemrosesan batch OCR** secara andal dan efisien.

![Contoh mengonversi gambar menjadi teks](https://example.com/convert-images-to-text.png "Tangkapan layar output konsol Java yang menunjukkan teks yang dikonversi dari file PNG")

## Jawaban Cepat
- **Perpustakaan apa yang menangani OCR?** Aspose OCR for Java.
- **Bisakah saya memproses PNG dan JPG bersama-sama?** Ya – contoh menyaring kedua ekstensi.
- **Apakah mesin OCR thread‑safe?** Satu instance `AsposeOCR` yang dibagikan aman untuk penggunaan bersamaan.
- **Apakah saya memerlukan lisensi untuk pengujian?** Kunci sementara gratis tersedia dari Aspose.
- **Apakah sub‑folder akan dipindai secara otomatis?** `Files.walk` menelusuri seluruh pohon secara rekursif.

## Apa itu mengekstrak teks dari png?

`extract text from png` mengacu pada proses menerapkan pengenalan karakter optik (OCR) pada file Portable Network Graphics sehingga karakter yang terlihat menjadi string yang dapat dicari dan diedit. Mesin Aspose OCR membaca data piksel, mengidentifikasi bentuk glif, dan mengembalikan teks Unicode dalam satu panggilan metode.

## Mengapa menggunakan Aspose OCR untuk Java?

Aspose OCR mendukung **30+ bahasa**, memproses hingga **500 gambar per menit** pada server standar 8‑core, dan dapat menangani file hingga **200 MB** tanpa memuat seluruh gambar ke memori. Kemampuan terkuantifikasi ini berarti Anda dapat menjalankan pekerjaan batch berskala besar pada perangkat keras komoditas tanpa mencapai batas memori.

## Prasyarat
- Java 17 (atau versi LTS terbaru apa pun).
- Maven atau Gradle untuk manajemen dependensi.
- Direktori yang berisi gambar PNG/JPG yang ingin Anda proses.
- Familiaritas dasar dengan aliran Java dan paket `java.nio.file`.
- (Opsional) Kunci lisensi sementara Aspose OCR untuk evaluasi.

> **Tip pro:** Kunci sementara gratis kedaluwarsa setelah 30 hari, tetapi memberikan akses API penuh untuk pengujian.

## Bagaimana pipeline batch OCR mempertahankan urutan?

`Future<OcrResult>` mewakili hasil OCR yang tertunda yang dapat diambil setelah pemrosesan selesai. Pipeline mempertahankan urutan file asli dengan menyimpan objek `Future<OcrResult>` dalam daftar yang mencerminkan urutan koleksi `Path` input. Ketika Anda kemudian mengiterasi futures dan memanggil `get()`, setiap panggilan hanya menunggu gambar yang bersangkutan, sehingga urutan output cocok dengan urutan input tanpa logika penyortiran tambahan.

## Apa itu Aspose OCR untuk Java?

`AsposeOCR` adalah kelas inti dari pustaka Aspose OCR yang mengenkapsulasi semua paket bahasa, pengaturan pengenalan, dan sumber daya native internal. Kelas ini dirancang untuk diinstansiasi sekali selama masa hidup aplikasi dan dapat dibagikan secara aman antar banyak thread. Karena memuat data bahasa hanya sekali, penggunaan kembali instance yang sama mengurangi overhead inisialisasi dan meningkatkan throughput untuk operasi batch.

## Cara menyiapkan proyek dan menambahkan Aspose OCR

Pertama, buat proyek Maven (atau Gradle) dan tambahkan dependensi Aspose OCR ke `pom.xml` Anda:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>24.10</version>
</dependency>
```

> **Mengapa ini penting:** Mendeklarasikan dependensi di awal memastikan kompiler dapat melihat `AsposeOCR`, `ParallelRecognizer`, dan kelas terkait. Ini juga menjamin versi yang sama digunakan di semua mesin, yang krusial untuk **pemrosesan batch OCR** yang dapat direproduksi.

Segarkan IDE Anda setelah proses build selesai; Anda sekarang seharusnya melihat paket Aspose di bawah **External Libraries**.

## Cara menginisialisasi mesin OCR – bagikan satu instance

`AsposeOCR` adalah kelas mesin OCR utama yang disediakan oleh pustaka Aspose OCR. Kita hanya memerlukan **satu** instance mesin OCR untuk seluruh proses. Membagikannya antar thread menghemat memori dan mempercepat proses karena mesin memuat paket bahasa hanya sekali.

```java
AsposeOCR ocrEngine = new AsposeOCR("YOUR_LICENSE_KEY");
```

`AsposeOCR` bersifat thread‑safe, sehingga Anda dapat dengan aman menyerahkannya ke `ParallelRecognizer` yang akan mengelola kumpulan thread pekerja.

> **Penjelasan:** `ParallelRecognizer` membungkus mesin dalam thread‑pool. Saat Anda mengirim banyak file, masing‑masing mendapatkan thread pekerja sendiri, memungkinkan paralelisme sejati pada CPU multi‑core.

## Cara membaca gambar dari folder – menelusuri pohon direktori

`Files.walk` adalah metode Java NIO yang menelusuri pohon file secara rekursif dan mengembalikan aliran objek `Path`. Sekarang kita perlu **membaca gambar dari folder** dan mengumpulkan setiap PNG atau JPG. API `Files.walk` membuat ini menjadi satu baris, tetapi kita akan menambahkan filter untuk **mengekstrak teks dari png** hanya bila diperlukan.

```java
List<Path> imagePaths = Files.walk(Paths.get("YOUR_DIRECTORY"))
    .filter(Files::isRegularFile)
    .filter(p -> {
        String lower = p.toString().toLowerCase();
        return lower.endsWith(".png") || lower.endsWith(".jpg");
    })
    .collect(Collectors.toList());
```

> **Mengapa kami menyaring di sini:** Menggunakan `filter` memungkinkan kami **menyaring file berdasarkan ekstensi** lebih awal, yang mengurangi I/O yang tidak perlu nanti. Ini juga membuat kode lebih mudah dibaca—tanpa regex yang kompleks.

## Cara mengirim pekerjaan OCR secara asynchronous

`recognizeAsync` mengirimkan gambar ke mesin OCR untuk pemrosesan asynchronous dan mengembalikan `Future<OcrResult>` yang mewakili hasil yang tertunda. Dengan daftar file siap, kami mendorong setiap path ke `ParallelRecognizer`. Metode `recognizeAsync` mengembalikan `Future<OcrResult>` yang kami simpan untuk diambil nanti.

```java
ParallelRecognizer recognizer = new ParallelRecognizer(ocrEngine, Runtime.getRuntime().availableProcessors());
List<Future<OcrResult>> futures = new ArrayList<>();

for (Path imagePath : imagePaths) {
    futures.add(recognizer.recognizeAsync(imagePath));
}
```

> **Apa yang terjadi di balik layar?** Setiap panggilan menambahkan tugas ke layanan eksekutor internal recognizer. Tugas‑tugas berjalan paralel, sehingga folder dengan 100 gambar dapat diproses dalam sebagian kecil waktu dibandingkan loop satu‑thread.

## Cara mengambil hasil sambil mempertahankan urutan file

`Future<OcrResult>` menyimpan hasil tugas OCR asynchronous dan menyediakan metode `get()` untuk memperoleh teks yang dikenali. Karena kami menyimpan futures dalam urutan yang sama dengan `imagePaths`, kami cukup mengiterasi daftar dan memanggil `get()`. Panggilan hanya menunggu hingga gambar tertentu selesai, mempertahankan urutan tanpa pencatatan tambahan.

```java
for (int i = 0; i < futures.size(); i++) {
    try {
        OcrResult result = futures.get(i).get();
        System.out.println("File: " + imagePaths.get(i).getFileName());
        System.out.println("Text: " + result.getText());
    } catch (Exception e) {
        System.err.println("Failed to process " + imagePaths.get(i) + ": " + e.getMessage());
    }
}
```

**Contoh output konsol** (dipotong untuk singkat):

```
File: invoice1.png
Text: Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
...
```

> **Penanganan kasus tepi:** Jika sebuah gambar melemparkan pengecualian (file rusak, format tidak didukung), kami menanganinya dan melanjutkan pemrosesan sisanya—kebiasaan penting untuk pipeline **pemrosesan batch OCR** yang andal.

## Cara membersihkan sumber daya – mematikan recognizer

`ParallelRecognizer.shutdown()` menghentikan thread‑pool internal, memastikan semua tugas OCR selesai sebelum aplikasi keluar. Jangan lupa mematikan thread‑pool internal; jika tidak, JVM Anda dapat menggantung saat keluar.

```java
recognizer.shutdown();
```

Itu saja! Program kini menelusuri direktori apa pun, menyaring file PNG/JPG, menjalankan OCR secara paralel, dan mencetak hasil dalam urutan asli.

---

## Contoh lengkap yang dapat dijalankan (salin‑dan‑tempel)

Berikut adalah kelas Java lengkap yang siap dijalankan. Ganti `"YOUR_DIRECTORY"` dengan path ke folder gambar Anda dan jalankan dari IDE atau baris perintah.

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.ParallelRecognizer;
import com.aspose.ocr.OcrResult;
import java.nio.file.*;
import java.util.*;
import java.util.concurrent.*;
import java.util.stream.*;

public class BatchOcrDemo {
    public static void main(String[] args) throws Exception {
        // Initialise the OCR engine (single shared instance)
        AsposeOCR ocrEngine = new AsposeOCR("YOUR_LICENSE_KEY");

        // Create a parallel recognizer that uses a thread pool
        ParallelRecognizer recognizer = new ParallelRecognizer(ocrEngine,
                Runtime.getRuntime().availableProcessors());

        // Walk the directory and collect PNG/JPG files
        List<Path> imagePaths = Files.walk(Paths.get("YOUR_DIRECTORY"))
                .filter(Files::isRegularFile)
                .filter(p -> {
                    String lower = p.toString().toLowerCase();
                    return lower.endsWith(".png") || lower.endsWith(".jpg");
                })
                .collect(Collectors.toList());

        // Submit OCR jobs asynchronously
        List<Future<OcrResult>> futures = new ArrayList<>();
        for (Path imagePath : imagePaths) {
            futures.add(recognizer.recognizeAsync(imagePath));
        }

        // Retrieve results in the original order
        for (int i = 0; i < futures.size(); i++) {
            try {
                OcrResult result = futures.get(i).get();
                System.out.println("File: " + imagePaths.get(i).getFileName());
                System.out.println("Text: " + result.getText());
            } catch (Exception e) {
                System.err.println("Failed to process " + imagePaths.get(i) + ": " + e.getMessage());
            }
        }

        // Clean up the recognizer's thread pool
        recognizer.shutdown();
    }
}
```

Jalankan kelas, saksikan konsol terisi dengan string yang diekstrak, dan rayakan fakta bahwa Anda baru saja **mengonversi gambar menjadi teks** tanpa menulis satu loop pun yang memblokir I/O.

---

## Pertanyaan yang sering diajukan (FAQ)

**Q: Bisakah saya memproses PDF atau TIFF juga?**  
A: Tentu saja. Aspose OCR mendukung 30+ format—termasuk PDF, TIFF, BMP, dan GIF—jadi cukup tambahkan ekstensi yang diinginkan ke filter pada langkah penelusuran direktori.

**Q: Bagaimana jika saya memerlukan bahasa selain Inggris, seperti Spanyol?**  
A: Ubah `RecognitionLanguage.ENGLISH` menjadi `RecognitionLanguage.SPANISH` (atau bahasa lain yang didukung). Paket bahasa sudah termasuk dalam pustaka, jadi tidak perlu unduhan tambahan.

**Q: Folder saya berisi sub‑folder—apakah mereka akan dipindai?**  
A: Ya. `Files.walk` menelusuri seluruh pohon secara rekursif, sehingga setiap PNG/J

**Q: Bagaimana cara menangani gambar sangat besar yang melebihi 200 MB?**  
A: Aktifkan mode streaming dengan memanggil `ocrEngine.setUseStreaming(true)`. Ini memberi tahu mesin untuk membaca gambar dalam potongan, secara dramatis mengurangi penggunaan memori puncak.

**Q: Apakah ada cara membatasi jumlah thread OCR bersamaan?**  
A: Ya. Saat membuat `ParallelRecognizer`, berikan jumlah maksimum thread yang diinginkan sebagai argumen kedua (misalnya, `new ParallelRecognizer(ocrEngine, 4)`).

---

**Terakhir Diperbarui:** 2026-08-28  
**Diuji dengan:** Aspose OCR for Java 24.10  
**Penulis:** Aspose  






```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Check the latest version on Maven Central -->
</dependency>
```

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.ParallelRecognizer;
import com.aspose.ocr.OcrResult;
import com.aspose.ocr.RecognitionLanguage;

// ...

// Step 2: Create a single OCR engine instance and a parallel recognizer that uses it
AsposeOCR ocrEngine = new AsposeOCR();               // Loads language data internally
ParallelRecognizer parallelRecognizer = new ParallelRecognizer(ocrEngine);
```

```java
import java.nio.file.*;
import java.util.*;
import java.util.stream.Collectors;

// ...

// Step 3: Find all PNG and JPG images in the target directory
Path imagesRoot = Paths.get("YOUR_DIRECTORY"); // <-- replace with your path
List<Path> imagePaths = Files.walk(imagesRoot)
        .filter(p -> {
            String name = p.toString().toLowerCase();
            return name.endsWith(".png") || name.endsWith(".jpg");
        })
        .collect(Collectors.toList());

if (imagePaths.isEmpty()) {
    System.out.println("No PNG or JPG files found in " + imagesRoot);
    return;
}
```

```java
import java.util.concurrent.*;

// ...

// Step 4: Submit each image for asynchronous recognition
List<Future<OcrResult>> recognitionFutures = new ArrayList<>();

for (Path image : imagePaths) {
    Future<OcrResult> future = parallelRecognizer.recognizeAsync(
            image.toString(),
            RecognitionLanguage.ENGLISH); // Change language if needed
    recognitionFutures.add(future);
}
```

```java
// Step 5: Retrieve and display the OCR results in the original order
for (int i = 0; i < recognitionFutures.size(); i++) {
    try {
        OcrResult result = recognitionFutures.get(i).get(); // blocks if not ready
        System.out.println("File: " + imagePaths.get(i).getFileName());
        System.out.println(result.getText()); // The extracted text
        System.out.println("-----");
    } catch (InterruptedException | ExecutionException e) {
        System.err.println("Failed to process " + imagePaths.get(i) + ": " + e.getMessage());
    }
}
```

```
File: invoice_001.png
Invoice #001
Date: 2024‑03‑15
Total: $1,250.00
-----
File: receipt_202403.jpg
Receipt
Item A - $45.00
Item B - $30.00
Grand Total: $75.00
-----
```

```java
// Step 6: Shut down the recognizer to clean up its internal thread pool
parallelRecognizer.shutdown();
```

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.ParallelRecognizer;
import com.aspose.ocr.OcrResult;
import com.aspose.ocr.RecognitionLanguage;

import java.nio.file.*;
import java.util.*;
import java.util.concurrent.*;
import java.util.stream.Collectors;

public class BatchParallelExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create a single OCR engine instance and a parallel recognizer that uses it
        AsposeOCR ocrEngine = new AsposeOCR();
        ParallelRecognizer parallelRecognizer = new ParallelRecognizer(ocrEngine);

        // Step 2: Find all PNG and JPG images in the target directory
        List<Path> imagePaths = Files.walk(Paths.get("YOUR_DIRECTORY"))
                .filter(p -> {
                    String lower = p.toString().toLowerCase();
                    return lower.endsWith(".png") || lower.endsWith(".jpg");
                })
                .collect(Collectors.toList());

        if (imagePaths.isEmpty()) {
            System.out.println("No images found – nothing to convert.");
            parallelRecognizer.shutdown();
            return;
        }

        // Step 3: Submit each image for asynchronous recognition
        List<Future<OcrResult>> recognitionFutures = new ArrayList<>();
        for (Path image : imagePaths) {
            recognitionFutures.add(
                    parallelRecognizer.recognizeAsync(
                            image.toString(),
                            RecognitionLanguage.ENGLISH));
        }

        // Step 4: Retrieve and display the OCR results in the original order
        for (int i = 0; i < recognitionFutures.size(); i++) {
            try {
                OcrResult result = recognitionFutures.get(i).get(); // blocks until processed
                System.out.println("File: " + imagePaths.get(i).getFileName());
                System.out.println(result.getText());
                System.out.println("-----");
            } catch (InterruptedException | ExecutionException e) {
                System.err.println("Error processing " + imagePaths.get(i) + ": " + e.getMessage());
            }
        }

        // Step 5: Shut down the recognizer to clean up its internal thread pool
        parallelRecognizer.shutdown();
    }
}
```

## Tutorial Terkait

- [Mengonversi Gambar Menjadi Teks di Java Panduan Pemrosesan Batch OCR](/ocr/java/ocr-operations/convert-images-to-text-in-java-batch-ocr-processing-guide/)
- [Membaca Teks Dari Gambar di Java Panduan Lengkap Aspose OCR](/ocr/java/ocr-basics/read-text-from-image-in-java-complete-aspose-ocr-guide/)
- [Mengekstrak Teks dari Gambar Menggunakan Aspose.OCR – Karakter yang Diizinkan](/ocr/java/advanced-ocr-techniques/specify-allowed-characters/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}