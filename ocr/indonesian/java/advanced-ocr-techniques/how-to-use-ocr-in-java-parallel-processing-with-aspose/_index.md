---
category: general
date: 2026-10-24
description: Pelajari cara melakukan OCR pada PDF dan gambar TIFF di Java menggunakan
  pemrosesan paralel Aspose OCR. Panduan cepat dan handal untuk pengembang.
draft: false
keywords:
- perform ocr pdf
- extract image text
- java ocr library
- process scanned pdf
- aspose ocr maven
lastmod: 2026-10-24
og_description: Lakukan OCR pada file PDF di Java dengan cepat menggunakan pemrosesan
  paralel Aspose OCR. Panduan ini menunjukkan cara mengaktifkan OCR multi‑threaded,
  mengonfigurasi batas thread, dan mengekstrak teks dari gambar PDF dan TIFF secara
  efisien.
og_image_alt: Diagram of Java OCR pipeline with parallel processing using Aspose OCR
og_title: Lakukan OCR pada PDF di Java – Pemrosesan paralel dengan Aspose
schemas:
- author: Aspose
  dateModified: '2026-10-24'
  description: Learn how to perform OCR on PDF and TIFF images in Java using Aspose
    OCR's parallel processing. Fast, reliable guide for developers.
  headline: How to perform OCR on PDF in Java with parallel processing
  type: TechArticle
- questions:
  - answer: Yes, Aspose OCR’s parallel engine runs on Windows, Linux, and macOS as
      long as the JVM can create native threads.
    question: Does the parallel mode work on any operating system?
  - answer: Absolutely—pass the password to `processImage` via the overload that accepts
      a `PdfLoadOptions` object.
    question: Can I process password‑protected PDFs?
  - answer: Aspose OCR supports Java 8, 11, 17, and later LTS releases.
    question: What Java versions are officially supported?
  - answer: For images under 300 dpi, accuracy drops to around 80 %; increasing the
      resolution to 400 dpi typically pushes it above 95 %.
    question: How accurate is the OCR for low‑resolution scans?
  - answer: Yes, a valid Aspose license removes evaluation limits and enables full‑performance
      features like parallel processing.
    question: Is a commercial license required for production use?
  type: FAQPage
tags:
- OCR
- Java
- Aspose
- parallel processing
- PDF
title: Cara melakukan OCR pada PDF di Java dengan pemrosesan paralel
url: /id/java/advanced-ocr-techniques/how-to-use-ocr-in-java-parallel-processing-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara melakukan OCR pada PDF di Java dengan pemrosesan paralel

Ever wondered **how to use OCR** to pull text out of a scanned document without breaking a sweat? In this tutorial you’ll learn how to **perform OCR PDF** tasks in Java using Aspose OCR’s built‑in parallel processing. The approach works for both PDF and TIFF sources, cuts processing time dramatically, and gives you fine‑grained control over thread usage. By the end you’ll have a ready‑to‑run Java class that can extract image text from any scanned PDF or multi‑page TIFF in a fraction of the time a single‑threaded solution would need.

## Jawaban cepat
- **Apa yang dilakukan OCR paralel?** Ia membagi halaman di antara beberapa inti CPU, memungkinkan beberapa halaman diproses secara bersamaan.  
- **Perpustakaan mana yang digunakan?** Aspose.OCR untuk Java, tersedia melalui Maven Central.  
- **Apakah saya memerlukan lisensi?** Versi percobaan gratis dapat digunakan untuk pengembangan; lisensi komersial diperlukan untuk produksi.  
- **Bisakah saya membatasi jumlah thread?** Ya—gunakan `setMaxThreads(int)` untuk membatasi pool thread.  
- **Apakah solusi ini kompatibel dengan Java 8 dan yang lebih baru?** Tentu saja, berjalan pada Java 8, 11, 17, dan versi selanjutnya.

## Apa itu perform OCR PDF?
`perform OCR PDF` mengacu pada tindakan mengekstrak teks yang dapat dicari dan diedit dari dokumen PDF yang dipindai menggunakan pengenalan karakter optik. Aspose OCR membaca gambar raster setiap halaman, menjalankan mesin pengenalan, dan mengembalikan teks Unicode biasa yang dapat Anda simpan, indeks, atau proses lebih lanjut.

## Mengapa menggunakan pemrosesan paralel Aspose OCR?
Aspose OCR mendukung **lebih dari 50 format input** (termasuk PDF, TIFF, JPEG, PNG, BMP) dan dapat menangani **dokumen ratusan halaman** tanpa memuat seluruh file ke memori. Pemrosesan paralel biasanya mengurangi waktu eksekusi sebesar **30‑70 % pada laptop 4‑core** dan hingga **80 % pada server 32‑core**, menurut rangkaian benchmark Aspose.

## Prasyarat

- Java 8 atau lebih baru (kode ini juga dapat dikompilasi dengan JDK 11).  
- Perpustakaan Aspose.OCR untuk Java – Anda dapat mengambil JAR terbaru dari Maven Central (`com.aspose:aspose-ocr`).  
- File gambar (`.tif`, `.tiff`) atau PDF yang ingin Anda proses.  
- Sebagian RAM yang cukup—pemrosesan paralel akan memulai beberapa thread, tetapi Aspose efisien dalam penggunaan memori.

Jika Anda sudah memiliki semua itu, mari kita mulai.

![Diagram yang menunjukkan alur OCR – cara menggunakan OCR di Java dengan pemrosesan paralel](how-to-use-ocr-pipeline.png)

*Teks alt gambar: diagram contoh cara menggunakan OCR*

---

## Bagaimana pemrosesan paralel meningkatkan kecepatan OCR?
Pemrosesan paralel mendistribusikan pekerjaan OCR ke semua inti CPU yang tersedia, memungkinkan beberapa halaman dikenali secara bersamaan. Pada laptop quad‑core tipikal, mengaktifkan mode paralel memotong waktu pemrosesan PDF 100‑halaman dari kira‑kira 45 detik menjadi sekitar 18 detik, sementara workstation 16‑core dapat menyelesaikan pekerjaan yang sama dalam kurang dari 7 detik. Peningkatan kecepatan ini datang dengan overhead memori minimal karena setiap thread bekerja pada buffer satu halaman.

## Cara menyiapkan proyek Anda dan menambahkan Aspose OCR
Menyiapkan proyek dengan benar memastikan mesin OCR dapat dimuat pada saat runtime. Dengan menambahkan dependensi Aspose OCR ke file build Anda, kelas‑kelas menjadi tersedia di classpath, yang diperlukan untuk operasi OCR selanjutnya.

### Mengapa ini penting
Sebelum Anda dapat **perform OCR on PDF** file, perpustakaan harus berada di classpath Anda. Tanpa itu, kompiler akan melempar `ClassNotFoundException` dan Anda akan terhenti pada langkah berikutnya.

### Cara melakukannya
Jika Anda menggunakan Maven, tambahkan dependensi:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>24.10</version>
</dependency>
```

Untuk Gradle, tambahkan:

```gradle
implementation 'com.aspose:aspose-ocr:24.10'
```

> **Tip pro:** Jaga agar nomor versi tetap sinkron dengan catatan rilis Aspose; versi yang lebih baru sering menyertakan peningkatan kinerja untuk pemrosesan paralel.

## Apa itu kelas OcrEngine?
`OcrEngine` adalah kelas utama di Aspose OCR yang menggerakkan proses pengenalan untuk gambar dan dokumen PDF.  
`OcrEngine` adalah kelas inti Aspose OCR yang melakukan ekstraksi teks dari gambar dan file PDF. Ia menyediakan metode untuk mengaktifkan pemrosesan paralel, mengatur bahasa, dan mengambil teks yang dikenali sebagai string. Selain itu, ia menawarkan opsi konfigurasi untuk optimisasi memori dan pemilihan bahasa, menjadikannya fleksibel untuk berbagai skenario OCR.

## Cara membuat mesin OCR dan mengaktifkan pemrosesan paralel
Membuat instance `OcrEngine` dan mengaktifkan mode paralel mempersiapkan perpustakaan untuk mendistribusikan pekerjaan ke inti CPU. Anda juga dapat mengonfigurasi bahasa dan pengaturan lain sebelum memproses file apa pun, serta secara opsional membatasi jumlah thread agar sesuai dengan lingkungan penyebaran Anda.

Muat mesin, aktifkan mode paralel, dan secara opsional batasi pool thread:

```java
OcrEngine ocrEngine = new OcrEngine();
ocrEngine.getConfig().setUseParallelProcessing(true);
ocrEngine.getConfig().setMaxThreads(Runtime.getRuntime().availableProcessors() - 1);
```

- `setUseParallelProcessing(true)`: memberi tahu Aspose untuk membagi beban kerja di antara inti CPU yang tersedia.  
- `setMaxThreads(...)`: Anda dapat membatasi pool thread jika berada di server bersama atau ingin menyisakan ruang untuk layanan lain.  
- `processImage(inputPath)`: bekerja untuk file gambar maupun dokumen PDF, sehingga pemanggilan yang sama **melakukan OCR pada PDF** dan pada TIFF juga.

## Cara menangani tipe input yang berbeda – PDF vs. TIFF
Meskipun `processImage` menerima string path, penanganan di baliknya berbeda. PDF biasanya berisi banyak halaman, masing‑masing menjadi pekerjaan OCR terpisah. TIFF dapat berupa satu‑halaman atau multi‑halaman; Aspose memperlakukan setiap frame sebagai halaman.

### Hal yang perlu diwaspadai

| Masukan | Masalah umum | Perbaikan yang disarankan |
|---------|--------------|---------------------------|
| PDF | PDF besar dapat menghabiskan memori jika semua halaman dimuat secara bersamaan. | Gunakan `ocrEngine.getConfig().setMemoryOptimization(true);` (tersedia pada rilis yang lebih baru). |
| Multi‑page TIFF | Beberapa TIFF lama menggunakan kompresi yang tidak didukung. | Konversi ke format yang didukung terlebih dahulu, atau gunakan pembantu `TiffImage` dari Aspose. |

Berikut adalah cuplikan cepat yang menunjukkan cara mendeteksi tipe file dan mencatat pesan yang bersahabat:

```java
String ext = Files.getFileExtension(inputPath).toLowerCase();
if (ext.equals("pdf")) {
    System.out.println("Processing PDF document...");
} else if (ext.equals("tif") || ext.equals("tiff")) {
    System.out.println("Processing TIFF image...");
} else {
    System.out.println("Unsupported file type: " + ext);
}
```

## Cara memverifikasi output – apa yang harus Anda lihat?
Setelah eksekusi program mencetak teks yang diekstrak ke konsol, mempertahankan jeda baris dan pemisah halaman. Tinjau output untuk memastikan semua konten yang diharapkan muncul dan bahwa bagian yang tidak dapat dibaca ditandai dengan placeholder, menunjukkan di mana OCR tidak dapat mengenali karakter.

Saat program selesai, Anda akan melihat teks mentah yang diekstrak dicetak ke konsol. Untuk faktur yang dipindai sederhana, output mungkin terlihat seperti:

```
Invoice #12345
Date: 2023‑07‑15
Total Amount: $1,250.00
...
```

Jika OCR mengalami kesulitan pada halaman tertentu, Aspose menyisipkan baris placeholder seperti `[Unrecognizable]`. Anda dapat menyaringnya nanti jika membutuhkan data bersih.

**Pemeriksaan cepat**

Jalankan program dengan file uji yang diketahui dan bandingkan output konsol dengan dokumen asli. Jika teks cocok dalam ambang akurasi 95 %, pengaturan Anda berfungsi dengan benar.

## Cara menyesuaikan kinerja – kapan menyesuaikan jumlah thread
Menyesuaikan jumlah thread memungkinkan Anda menyeimbangkan pemanfaatan CPU dengan overhead. Pada mesin dengan inti lebih sedikit, jumlah thread yang lebih rendah mengurangi pergantian konteks, sementara pada server berinti tinggi Anda dapat meningkatkannya untuk memanfaatkan paralelisme secara penuh, selalu menguji untuk menemukan pengaturan optimal.

### Cara menemukan titik optimal
Jalankan serangkaian tes benchmark dengan nilai `setMaxThreads` yang berbeda, mengukur total waktu eksekusi untuk dokumen representatif. Plot hasilnya untuk mengidentifikasi titik di mana menambah thread tidak lagi memberikan peningkatan kecepatan.

```java
long start = System.nanoTime();
ocrEngine.processImage("large-document.pdf");
long elapsed = System.nanoTime() - start;
System.out.println("Elapsed ms: " + elapsed / 1_000_000);
```

Jalankan program dengan nilai `setMaxThreads` yang berbeda dan catat waktunya. Pilih konfigurasi yang memberikan throughput terbaik, dan kuncikan untuk produksi.

## Cara memperluas demo – pemrosesan batch banyak file
Untuk memproses banyak file secara otomatis, iterasikan direktori dan panggil rutin OCR untuk setiap dokumen. Loop luar ini juga dapat diparalelkan menggunakan `ExecutorService` jika Anda perlu menangani volume file yang besar secara bersamaan.

```java
Files.list(Paths.get("input-folder"))
     .filter(Files::isRegularFile)
     .forEach(path -> ocrEngine.processImage(path.toString()));
```

Pola ini skalabel dengan baik karena mesin sudah menjalankan halaman tiap file secara paralel. Loop luar berjalan berurutan, tetapi Anda juga dapat mengirimkan tiap file ke `ExecutorService` jika perlu memanfaatkan seluruh farm CPU.

## Kesalahan umum & cara menghindarinya

| Gejala | Penyebab yang mungkin | Perbaikan |
|--------|-----------------------|-----------|
| `OutOfMemoryError` | Terlalu banyak halaman dimuat sekaligus (terutama dengan PDF besar). | Aktifkan optimisasi memori (`setMemoryOptimization(true)`) atau proses PDF halaman‑per‑halaman menggunakan `processPage`. |
| Karakter rusak | Konfigurasi bahasa/charset yang salah. | Panggil `ocrEngine.getConfig().setLanguage(OcrLanguage.English);` atau enum bahasa yang sesuai. |
| Kinerja lambat meski flag paralel diaktifkan | OS membatasi pembuatan thread atau JVM berjalan dengan heap kecil. | Tingkatkan flag heap `-Xmx`, dan verifikasi batas thread OS (`ulimit -u`). |
| Output kosong | Resolusi gambar input < 300 dpi. | Tingkatkan resolusi gambar sebelum OCR atau gunakan scanner yang menghasilkan resolusi lebih tinggi. |

## Ringkasan – apa yang telah kami bahas
- **Cara melakukan OCR pada file PDF** dan TIFF di Java dengan `OcrEngine` Aspose.  
- Mengaktifkan **pemrosesan paralel** untuk mempercepat pengenalan.  
- Menyesuaikan jumlah thread untuk kinerja optimal.  
- Menangani kasus tepi seperti PDF besar, TIFF multi‑halaman, dan pengaturan bahasa.  
- Memperluas demo satu file menjadi pemroses batch untuk beban kerja dunia nyata.

## Langkah selanjutnya
Sekarang Anda telah menguasai dasar‑dasarnya, pertimbangkan untuk menjelajahi topik terkait berikut:

- **Ekstrak teks gambar java** dari catatan tulisan tangan (aktifkan `setHandwritingRecognition(true)`).  
- Mengintegrasikan output OCR dengan Apache Tika untuk ekstraksi metadata.  
- Menyimpan hasil di Elasticsearch untuk arsip dokumen yang dapat dicari.  
- Menggunakan OCR Aspose dengan bahasa lain seperti Python atau .NET—prinsipnya tetap sama.

Silakan bereksperimen dengan batas thread yang berbeda, format gambar, dan paket bahasa. Semakin banyak Anda mencoba, semakin baik Anda akan memahami trade‑off antara kecepatan dan akurasi.

## Pertanyaan yang sering diajukan

**Q: Apakah mode paralel bekerja pada sistem operasi apa pun?**  
A: Ya, mesin paralel Aspose OCR berjalan di Windows, Linux, dan macOS selama JVM dapat membuat thread native.

**Q: Bisakah saya memproses PDF yang dilindungi kata sandi?**  
A: Tentu saja—lewatkan kata sandi ke `processImage` melalui overload yang menerima objek `PdfLoadOptions`.

**Q: Versi Java apa yang secara resmi didukung?**  
A: Aspose OCR mendukung Java 8, 11, 17, dan rilis LTS selanjutnya.

**Q: Seberapa akurat OCR untuk pemindaian beresolusi rendah?**  
A: Untuk gambar di bawah 300 dpi, akurasi turun menjadi sekitar 80 %; meningkatkan resolusi ke 400 dpi biasanya meningkatkan di atas 95 %.

**Q: Apakah lisensi komersial diperlukan untuk penggunaan produksi?**  
A: Ya, lisensi Aspose yang valid menghapus batas evaluasi dan mengaktifkan fitur performa penuh seperti pemrosesan paralel.

---

**Terakhir Diperbarui:** 2026-10-24  
**Diuji Dengan:** Aspose.OCR 24.10 untuk Java  
**Penulis:** Aspose  






```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- check for the newest version -->
</dependency>
```

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

```java
import com.aspose.ocr.*;

public class ParallelOcrDemo {

    public static void main(String[] args) throws Exception {
        // 1️⃣ Path to the input file (TIFF or PDF)
        String inputPath = "YOUR_DIRECTORY/input.tif";

        // 2️⃣ Instantiate the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 3️⃣ Turn on parallel processing – this is the core of how to use OCR efficiently
        ocrEngine.getConfig().setUseParallelProcessing(true);

        // 4️⃣ (Optional) Limit threads – you can cap it to the number of cores you have
        // ocrEngine.getConfig().setMaxThreads(Runtime.getRuntime().availableProcessors());

        // 5️⃣ Run OCR
        OcrResult ocrResult = ocrEngine.processImage(inputPath);

        // 6️⃣ Output the recognised text
        System.out.println(ocrResult.getText());
    }
}
```

```java
import java.nio.file.*;

String ext = Files.probeContentType(Paths.get(inputPath)).toLowerCase();
if (ext.contains("pdf")) {
    System.out.println("Processing a PDF – expect multiple pages.");
} else if (ext.contains("tiff") || ext.contains("tif")) {
    System.out.println("Processing a TIFF image.");
} else {
    System.out.println("Unsupported file type. This demo works with PDF and TIFF.");
}
```

```
Invoice #12345
Date: 02/15/2026
Total Amount: $1,250.00
Thank you for your business!
```

```java
if (ocrResult.getText().trim().isEmpty()) {
    System.err.println("No text detected – verify the image quality or try a different language.");
}
```

```java
int cores = Runtime.getRuntime().availableProcessors();
System.out.println("Available processors: " + cores);

// Experiment: set max threads to half the cores first
ocrEngine.getConfig().setMaxThreads(Math.max(1, cores / 2));
```

```java
long start = System.nanoTime();
ocrEngine.processImage(inputPath);
long elapsed = System.nanoTime() - start;
System.out.println("Elapsed time (ms): " + elapsed / 1_000_000);
```

```java
Path folder = Paths.get("YOUR_DIRECTORY");
try (DirectoryStream<Path> stream = Files.newDirectoryStream(folder, "*.{tif,tiff,pdf}")) {
    for (Path file : stream) {
        System.out.println("\n--- Processing: " + file.getFileName() + " ---");
        OcrResult result = ocrEngine.processImage(file.toString());
        // Save or further process result.getText()
    }
}
```

## Tutorial Terkait

- [Cara Menggunakan OCR di Java untuk Mengekstrak Teks Dari PDF Aspose OCR](/ocr/java/advanced-ocr-techniques/how-to-use-ocr-in-java-extract-text-from-pdf-aspose-ocr/)
- [Mengenali Teks PDF dengan Aspose OCR di Java Panduan Lengkap](/ocr/java/ocr-operations/recognize-pdf-text-with-aspose-ocr-in-java-complete-guide/)
- [Cara Mengaktifkan GPU untuk OCR di Java Mengekstrak Teks Dari Gambar](/ocr/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-extract-text-from-image/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}