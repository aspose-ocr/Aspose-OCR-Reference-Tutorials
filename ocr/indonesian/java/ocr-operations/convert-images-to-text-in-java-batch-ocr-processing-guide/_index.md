---
category: general
date: 2026-01-02
description: Mengonversi gambar menjadi teks dengan Java menggunakan Aspose OCR. Kuasai
  pemrosesan OCR batch, baca gambar dari folder, dan filter file berdasarkan ekstensi.
draft: false
keywords:
- convert images to text
- batch ocr processing
- read images from folder
- extract text from png
- filter files by extension
language: id
og_description: Ubah gambar menjadi teks dengan cepat menggunakan Java. Tutorial ini
  mencakup pemrosesan OCR batch, membaca gambar dari folder, dan memfilter file berdasarkan
  ekstensi.
og_title: Mengonversi Gambar ke Teks di Java – Panduan OCR Batch Lengkap
tags:
- OCR
- Java
- Aspose
title: Mengonversi Gambar menjadi Teks di Java – Panduan Pemrosesan OCR Batch
url: /id/java/ocr-operations/convert-images-to-text-in-java-batch-ocr-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Mengonversi Gambar ke Teks dalam Java – Panduan Pemrosesan OCR Batch

Pernahkah Anda perlu **mengonversi gambar ke teks** tetapi tidak yakin bagaimana menangani puluhan file sekaligus? Anda tidak sendirian—para pengembang terus-menerus berjuang mengekstrak data dari PNG, JPG, dan pemindaian lainnya. Kabar baiknya? Dengan Aspose OCR Anda dapat membuat pipeline pemrosesan OCR batch dalam hitungan menit, membaca gambar dari struktur folder, dan bahkan memfilter file berdasarkan ekstensi sehingga Anda hanya bekerja pada yang penting.

Dalam tutorial ini kami akan membangun program Java yang berdiri sendiri yang menelusuri sebuah direktori, memilih setiap `.png` atau `.jpg`, mengirim setiap gambar ke Aspose OCR secara asynchronous, dan mencetak teks yang diekstrak dalam urutan aslinya. Pada akhir tutorial Anda akan memiliki potongan kode yang dapat digunakan kembali dan dapat dimasukkan ke dalam proyek apa pun yang membutuhkan **mengonversi gambar ke teks** secara skala.

---

![Contoh mengonversi gambar ke teks](https://example.com/convert-images-to-text.png "Tangkapan layar output konsol Java yang menampilkan teks yang dikonversi dari file PNG")

## Apa yang Akan Anda Bangun

- Sebuah mesin `AsposeOCR` tunggal yang dibagikan di antara thread (efisien dan thread‑safe).  
- Sebuah `ParallelRecognizer` yang menjalankan pekerjaan OCR secara paralel, sempurna untuk **pemrosesan OCR batch**.  
- Logika yang **membaca gambar dari folder** menggunakan `java.nio.file.Files`.  
- Filter sederhana untuk **mengekstrak teks dari PNG** sambil tetap menangani JPG.  
- Penutupan bersih dari thread pool internal untuk menghindari kebocoran sumber daya.

### Prasyarat

- Java 17 (atau versi LTS terbaru apa pun).  
- Maven atau Gradle untuk mengunduh pustaka Aspose OCR.  
- Sebuah folder berisi gambar PNG/JPG yang ingin Anda proses.  
- Pemahaman dasar tentang stream Java—tidak diperlukan yang rumit.

> **Tips Pro:** Jika Anda belum memiliki lisensi, Aspose menawarkan kunci sementara gratis yang dapat Anda gunakan untuk pengujian.

## Langkah 1 – Siapkan Proyek dan Tambahkan Aspose OCR

Pertama, buat proyek Maven baru (atau Gradle, terserah Anda). Tambahkan dependensi Aspose OCR ke `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Check the latest version on Maven Central -->
</dependency>
```

> **Mengapa ini penting:** Mendeklarasikan dependensi di awal memastikan kompiler dapat melihat `AsposeOCR`, `ParallelRecognizer`, dan kelas terkait. Ini juga menjamin versi yang sama digunakan di semua mesin, yang penting untuk **pemrosesan OCR batch** yang dapat direproduksi.

Setelah proses build selesai, segarkan IDE Anda dan Anda akan melihat paket Aspose di bawah `External Libraries`.

## Langkah 2 – Mengonversi Gambar ke Teks – Inisialisasi Mesin OCR

Kita hanya membutuhkan **satu** instance mesin OCR untuk seluruh proses. Membagikannya di antara thread menghemat memori dan mempercepat karena mesin memuat paket bahasa hanya sekali.

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

> **Penjelasan:** `ParallelRecognizer` membungkus mesin dalam thread‑pool. Ketika Anda mengirim banyak file, masing‑masing mendapatkan thread pekerja sendiri, memungkinkan paralelisme sejati pada CPU multi‑core.

## Langkah 3 – Membaca Gambar dari Folder – Menelusuri Pohon Direktori

Sekarang kita perlu **membaca gambar dari folder** dan mengumpulkan setiap PNG atau JPG. API `Files.walk` membuat ini menjadi satu baris, tetapi kami akan menambahkan filter untuk **mengekstrak teks dari PNG** hanya bila diperlukan.

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

> **Mengapa kami memfilter di sini:** Menggunakan `filter` memungkinkan kita **memfilter file berdasarkan ekstensi** lebih awal, yang mengurangi I/O yang tidak perlu nanti. Ini juga membuat kode lebih mudah dibaca—tidak perlu regex yang kompleks.

## Langkah 4 – Pemrosesan OCR Batch – Kirim Pekerjaan Secara Asynchronous

Dengan daftar file siap, kami mengirim setiap path ke `ParallelRecognizer`. Metode `recognizeAsync` mengembalikan `Future<OcrResult>` yang kami simpan untuk diambil nanti.

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

> **Apa yang terjadi di balik layar?** Setiap panggilan menambahkan tugas ke layanan executor internal recognizer. Tugas‑tugas berjalan secara paralel, sehingga folder dengan 100 gambar dapat diproses dalam sebagian kecil waktu dibandingkan loop satu‑thread.

## Langkah 5 – Mengambil Hasil dalam Urutan Asli – Mempertahankan Urutan File

Karena kami menyimpan futures dalam urutan yang sama dengan `imagePaths`, kami cukup mengiterasi daftar dan memanggil `get()`. Panggilan ini hanya akan menunggu sampai gambar tersebut selesai, mempertahankan urutan tanpa pencatatan tambahan.

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

**Contoh output konsol** (dipotong untuk singkat):

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

> **Penanganan kasus tepi:** Jika sebuah gambar melemparkan pengecualian (file rusak, format tidak didukung), kami menangkapnya dan melanjutkan memproses sisanya—kebiasaan penting untuk pipeline **pemrosesan OCR batch** yang andal.

## Langkah 6 – Pembersihan – Matikan Recognizer

Jangan pernah lupa mematikan thread pool internal; jika tidak, JVM Anda mungkin tidak berhenti saat keluar.

```java
// Step 6: Shut down the recognizer to clean up its internal thread pool
parallelRecognizer.shutdown();
```

Itu saja! Program kini akan menelusuri direktori apa pun, memfilter file PNG/JPG, menjalankan OCR secara paralel, dan mencetak hasilnya.

## Contoh Kerja Lengkap

Berikut adalah kelas Java lengkap yang siap disalin‑tempel. Ganti `"YOUR_DIRECTORY"` dengan path ke folder gambar Anda dan jalankan dari IDE atau baris perintah.

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

Jalankan kelas, saksikan konsol terisi dengan string yang diekstrak, dan rayakan fakta bahwa Anda baru saja **mengonversi gambar ke teks** tanpa menulis satu loop pun yang memblokir I/O.

## Pertanyaan yang Sering Diajukan (FAQ)

**Q: Bisakah saya memproses PDF atau TIFF juga?**  
A: Tentu saja. Aspose OCR mendukung banyak format—cukup tambahkan ekstensi file yang sesuai ke filter di Langkah 2.

**Q: Bagaimana jika saya membutuhkan bahasa lain, seperti Spanyol?**  
A: Ubah `RecognitionLanguage.ENGLISH` menjadi `RecognitionLanguage.SPANISH`. Pastikan paket bahasa sudah terpasang (Aspose menyertakan sebagian besar bahasa utama secara bawaan).

**Q: Folder saya berisi sub‑folder—apakah mereka akan dipindai?**  
A: Ya. `Files.walk` menelusuri seluruh pohon secara rekursif, sehingga setiap PNG/J

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}