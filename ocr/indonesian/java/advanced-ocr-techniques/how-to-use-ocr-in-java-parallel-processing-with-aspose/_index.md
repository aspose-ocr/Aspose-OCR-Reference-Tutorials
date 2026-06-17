---
category: general
date: 2026-02-27
description: Pelajari cara menggunakan OCR di Java untuk mengekstrak teks gambar dari
  file TIFF dan PDF menggunakan pemrosesan paralel Aspose OCR. Panduan cepat dan sederhana.
draft: false
keywords:
- how to use ocr
- perform ocr on pdf
- extract text from tiff
- extract image text java
language: id
og_description: Pelajari cara menggunakan OCR di Java untuk mengekstrak teks gambar
  dari file TIFF dan PDF menggunakan pemrosesan paralel Aspose OCR.
og_title: Cara Menggunakan OCR di Java – Pemrosesan Paralel dengan Aspose
tags:
- OCR
- Java
- Aspose
title: Cara Menggunakan OCR di Java – Pemrosesan Paralel dengan Aspose
url: /id/java/advanced-ocr-techniques/how-to-use-ocr-in-java-parallel-processing-with-aspose/
---

Add Aspose OCR". Translate.

Then "### Why this matters". Translate.

Paragraph.

Then "### How to do it". Translate.

Then code placeholders.

Then blockquote pro tip.

Then next sections similarly.

We must translate all text, including table content.

Let's translate step by step.

Will keep code block placeholders unchanged.

Now produce final content.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menggunakan OCR di Java – Pemrosesan Paralel dengan Aspose

Pernah bertanya-tanya **bagaimana cara menggunakan OCR** untuk mengambil teks dari dokumen yang dipindai tanpa kesulitan? Anda bukan satu-satunya. Pengembang terus-menerus menemui kendala ketika mereka perlu membaca teks dari gambar—terutama TIFF dan PDF—sementara tetap menjaga kinerja.

Dalam tutorial ini kami akan menunjukkan solusi lengkap yang siap‑jalankan yang **mengekstrak teks gambar di Java** menggunakan Aspose OCR, mengaktifkan pemrosesan paralel, dan bahkan memungkinkan Anda membatasi jumlah thread. Pada akhirnya Anda akan memiliki satu kelas yang dapat **melakukan OCR pada PDF** dan **mengekstrak teks dari TIFF** dalam sebagian kecil waktu dibandingkan pendekatan satu‑thread.

> **Apa yang akan Anda dapatkan**  
> * Penjelasan jelas mengapa OCR paralel penting.  
> * Program Java lengkap (tanpa impor yang hilang).  
> * Tips untuk menyesuaikan penggunaan thread dan menangani jebakan umum.  

## Prasyarat

- Java 8 atau lebih baru (kode juga dapat dikompilasi dengan JDK 11).  
- Perpustakaan Aspose.OCR untuk Java – Anda dapat mengambil JAR terbaru dari Maven Central (`com.aspose:aspose-ocr`).  
- File gambar (`.tif`, `.tiff`) atau PDF yang ingin Anda proses.  
- Jumlah RAM yang cukup—pemrosesan paralel akan memunculkan beberapa thread, tetapi Aspose efisien dalam penggunaan memori.

Jika Anda sudah memiliki semua itu, mari kita mulai.

![Diagram yang menunjukkan alur OCR – cara menggunakan OCR di Java dengan pemrosesan paralel](how-to-use-ocr-pipeline.png)

*Teks alt gambar: contoh diagram cara menggunakan OCR*

---

## Langkah 1: Siapkan Proyek Anda dan Tambahkan Aspose OCR

### Mengapa ini penting

Sebelum Anda dapat **melakukan OCR pada PDF** atau gambar apa pun, perpustakaan harus berada di classpath Anda. Tanpa itu, kompiler akan melempar `ClassNotFoundException` dan Anda akan terhenti pada langkah dua.

### Cara melakukannya

Jika Anda menggunakan Maven, tambahkan dependensi:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- check for the newest version -->
</dependency>
```

Untuk Gradle:

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

> **Pro tip:** Jaga nomor versi tetap sinkron dengan catatan rilis Aspose; versi yang lebih baru sering kali menyertakan perbaikan kinerja untuk pemrosesan paralel.

---

## Langkah 2: Buat OCR Engine dan Aktifkan Pemrosesan Paralel

### Mengapa ini penting

Secara default Aspose OCR berjalan pada satu thread. Ketika Anda memberinya PDF multi‑halaman atau batch TIFF, engine akan memproses setiap halaman satu per satu—lambat dan tidak efisien. Mengaktifkan pemrosesan paralel memungkinkan CPU mengolah beberapa halaman sekaligus, memotong waktu eksekusi secara dramatis.

### Kode

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

**Penjelasan baris‑baris kunci**

- `setUseParallelProcessing(true)`: memberi tahu Aspose untuk membagi beban kerja ke seluruh core CPU yang tersedia.  
- `setMaxThreads(...)`: Anda dapat membatasi pool thread jika berada di server bersama atau ingin menyisakan ruang untuk layanan lain.  
- `processImage(inputPath)`: bekerja untuk file gambar maupun dokumen PDF, sehingga pemanggilan yang sama **melakukan OCR pada PDF** dan pada TIFF.

---

## Langkah 3: Menangani Berbagai Tipe Input – PDF vs. TIFF

### Mengapa ini penting

Meskipun `processImage` menerima string path, penanganan di baliknya berbeda. PDF biasanya berisi banyak halaman, masing‑masing menjadi pekerjaan OCR terpisah. TIFF dapat berupa satu halaman atau multi‑halaman; Aspose memperlakukan setiap frame sebagai halaman.

### Hal yang Perlu Diperhatikan

| Input | Masalah umum | Solusi yang disarankan |
|------|----------------|-----------------|
| PDF | PDF besar dapat menghabiskan memori jika semua halaman dimuat sekaligus. | Gunakan `ocrEngine.getConfig().setMemoryOptimization(true);` (tersedia pada rilis terbaru). |
| TIFF multi‑halaman | Beberapa TIFF lama menggunakan kompresi yang tidak didukung. | Konversi ke format yang didukung terlebih dahulu, atau gunakan helper `TiffImage` dari Aspose. |

Berikut cuplikan singkat yang menunjukkan cara mendeteksi tipe file dan mencatat pesan yang ramah:

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

---

## Langkah 4: Memverifikasi Output – Apa yang Harus Anda Lihat?

Saat program selesai, Anda akan melihat teks mentah yang diekstrak dicetak ke konsol. Untuk faktur yang dipindai sederhana, outputnya mungkin terlihat seperti:

```
Invoice #12345
Date: 02/15/2026
Total Amount: $1,250.00
Thank you for your business!
```

Jika OCR kesulitan pada halaman tertentu, Aspose menyisipkan baris placeholder seperti `[Unrecognizable]`. Anda dapat menyaringnya nanti jika membutuhkan data bersih.

**Pemeriksaan cepat**

```java
if (ocrResult.getText().trim().isEmpty()) {
    System.err.println("No text detected – verify the image quality or try a different language.");
}
```

---

## Langkah 5: Menyesuaikan Kinerja – Kapan Mengatur Jumlah Thread

### Mengapa ini penting

Lebih banyak thread tidak selalu berarti hasil lebih cepat. Pada laptop 4‑core, meluncurkan 8 thread dapat menyebabkan overhead pergantian konteks. Sebaliknya, pada server 32‑core Anda mungkin ingin memanfaatkan seluruh kekuatan.

### Cara menemukan titik optimal

```java
int cores = Runtime.getRuntime().availableProcessors();
System.out.println("Available processors: " + cores);

// Experiment: set max threads to half the cores first
ocrEngine.getConfig().setMaxThreads(Math.max(1, cores / 2));
```

Jalankan program dengan pengaturan berbeda dan ukur waktunya:

```java
long start = System.nanoTime();
ocrEngine.processImage(inputPath);
long elapsed = System.nanoTime() - start;
System.out.println("Elapsed time (ms): " + elapsed / 1_000_000);
```

Catat waktu, pilih konfigurasi yang memberikan throughput terbaik, dan tetapkan untuk produksi.

---

## Langkah 6: Memperluas Demo – Pemrosesan Batch Banyak File

Jika Anda perlu **mengekstrak teks gambar java** dari seluruh folder, bungkus logika inti dalam loop:

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

Pola ini skalabel karena engine sudah menjalankan halaman tiap file secara paralel. Loop luar berjalan berurutan, tetapi Anda juga dapat mengirim tiap file ke `ExecutorService` jika ingin memanfaatkan CPU secara maksimal.

---

## Jebakan Umum & Cara Menghindarinya

| Gejala | Penyebab yang mungkin | Solusi |
|---------|--------------|-----|
| `OutOfMemoryError` | Terlalu banyak halaman dimuat sekaligus (terutama pada PDF besar). | Aktifkan optimasi memori (`setMemoryOptimization(true)`) atau proses PDF halaman‑per‑halaman menggunakan `processPage`. |
| Karakter kacau | Konfigurasi bahasa/charset yang salah. | Panggil `ocrEngine.getConfig().setLanguage(OcrLanguage.English);` atau enum bahasa yang sesuai. |
| Performa lambat meski flag paralel aktif | OS membatasi pembuatan thread atau JVM dijalankan dengan heap kecil. | Tingkatkan flag heap `-Xmx`, dan periksa batas thread OS (`ulimit -u`). |
| Output kosong | Resolusi gambar input < 300 dpi. | Perbesar gambar sebelum OCR atau gunakan scanner dengan resolusi lebih tinggi. |

---

## Ringkasan – Apa yang Telah Kita Bahas

- **Cara menggunakan OCR** di Java dengan `OcrEngine` milik Aspose.  
- Mengaktifkan **pemrosesan paralel** untuk mempercepat **melakukan OCR pada PDF** dan **mengekstrak teks dari TIFF**.  
- Menyesuaikan jumlah thread untuk kinerja optimal.  
- Menangani kasus tepi seperti PDF besar, TIFF multi‑halaman, dan pengaturan bahasa.  
- Memperluas demo satu‑file menjadi pemroses batch untuk beban kerja dunia nyata.

---

## Langkah Selanjutnya

Setelah menguasai dasar‑dasarnya, pertimbangkan mengeksplorasi topik terkait berikut:

- **Mengekstrak teks gambar java** dari catatan tulisan tangan (aktifkan `setHandwritingRecognition(true)`).  
- Mengintegrasikan output OCR dengan Apache Tika untuk ekstraksi metadata.  
- Menyimpan hasil di Elasticsearch untuk arsip dokumen yang dapat dicari.  
- Menggunakan OCR Aspose dengan bahasa lain seperti Python atau .NET—prinsipnya tetap sama.

Jangan ragu bereksperimen dengan batas thread yang berbeda, format gambar, dan paket bahasa. Semakin banyak Anda mencoba, semakin baik Anda memahami trade‑off antara kecepatan dan akurasi.

---

### Selamat coding!

Jika Anda menemui kendala atau memiliki ide untuk optimasi lebih lanjut, tinggalkan komentar di bawah. Saya selalu siap berdiskusi tentang trik OCR—tanpa ribet, hanya kode.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}