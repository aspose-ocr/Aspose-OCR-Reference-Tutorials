---
category: general
date: 2026-02-09
description: Pelajari cara melakukan OCR batch di Java dengan Aspose OCR. Ekstrak
  teks dari gambar, kenali teks dari file PNG, JPG, dan TIFF dalam satu panggilan.
draft: false
keywords:
- how to batch ocr
- extract text from images
- recognize text from png
- recognize text from jpg
- recognize text from tiff
language: id
og_description: Kuasi cara melakukan OCR batch di Java. Tutorial ini menunjukkan cara
  mengekstrak teks dari gambar PNG, JPG, dan TIFF menggunakan Aspose OCR dengan contoh
  kode yang jelas.
og_title: Cara Batch OCR di Java – Ekstrak Teks dari Gambar Secara Efisien
tags:
- OCR
- Java
- Aspose
title: Cara Batch OCR di Java – Panduan Lengkap untuk Mengekstrak Teks dari Gambar
url: /id/java/ocr-operations/how-to-batch-ocr-in-java-complete-guide-to-extract-text-from/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Batch OCR di Java – Panduan Lengkap untuk Mengekstrak Teks dari Gambar

Pernah bertanya-tanya **bagaimana cara batch OCR** beberapa gambar tanpa menulis loop untuk setiap file? Anda tidak sendirian. Dalam banyak proyek dunia nyata Anda mendapatkan folder penuh pemindaian—struk PNG, screenshot JPG, atau bahkan TIFF multi‑halaman—dan Anda membutuhkan teks dengan cepat.  

Kabar baiknya, Aspose OCR memungkinkan Anda melakukan hal itu: satu panggilan metode yang mengenali teks dari file PNG, JPG, dan TIFF sekaligus. Dalam tutorial ini kami akan membahas seluruh proses, mulai dari menyiapkan proyek hingga mencetak hasil, sehingga Anda dapat mulai mengekstrak teks dari gambar hari ini.

## Apa yang Dibahas dalam Tutorial Ini

* **Bagaimana cara batch OCR** menggunakan `OcrBatchProcessor` milik Aspose.
* Cara **mengekstrak teks dari gambar** dengan format berbeda (PNG, JPG, TIFF).
* Tips untuk mengontrol paralelisme agar aplikasi Anda tetap responsif.
* Program Java lengkap yang dapat dijalankan, yang dapat Anda salin‑tempel dan jalankan segera.

Tanpa pengalaman sebelumnya dengan Aspose—hanya instalasi Java dasar dan IDE pilihan Anda. Pada akhir tutorial, Anda akan memiliki fondasi yang kuat untuk mengenali teks dari file PNG, JPG, dan TIFF secara massal.

---

![Diagram yang menggambarkan cara batch OCR beberapa file gambar](/images/batch-ocr-diagram.png "how to batch ocr")

*Teks alt gambar: diagram cara batch OCR yang menunjukkan beberapa file gambar diproses bersama.*

## Prasyarat

| Persyaratan | Mengapa penting |
|-------------|-----------------|
| Java 17 atau lebih baru | Aspose OCR menargetkan JVM modern. |
| Maven atau Gradle | Menyederhanakan penambahan pustaka Aspose OCR. |
| Pengetahuan dasar Java | Diperlukan untuk memahami alur kode. |
| Sekumpulan gambar contoh (`.png`, `.jpg`, `.tif`) | Untuk melihat ekstraksi secara langsung. |

Jika Anda sudah memiliki semua ini, bagus—mari kita mulai.

## Langkah 1: Tambahkan Aspose OCR ke Proyek Anda

Hal pertama yang Anda butuhkan adalah JAR Aspose OCR. Dengan Maven, tambahkan ini ke `pom.xml` Anda:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- use the latest stable version -->
</dependency>
```

Jika Anda lebih suka Gradle, setaraannya adalah:

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

Menambahkan dependensi ini akan mengunduh semua yang diperlukan untuk **recognize text from png**, **recognize text from jpg**, dan **recognize text from tiff**. Tidak diperlukan pustaka native tambahan.

## Langkah 2: Tentukan File Gambar yang Ingin Diproses

Sekarang kami akan memberi tahu mesin OCR file mana yang harus diproses. Di sinilah **how to batch OCR** benar‑benar bersinar—cukup berikan daftar path dan biarkan pustaka melakukan pekerjaan berat.

```java
import java.util.Arrays;
import java.util.List;

// Step 2: List your image files (PNG, JPG, TIFF)
List<String> imageFiles = Arrays.asList(
        "YOUR_DIRECTORY/img1.png",   // PNG file – recognize text from png
        "YOUR_DIRECTORY/img2.jpg",   // JPG file – recognize text from jpg
        "YOUR_DIRECTORY/img3.tif");  // TIFF file – recognize text from tiff
```

> **Pro tip:** Simpan path file Anda secara absolut atau gunakan `Paths.get(...)` untuk menghindari kejutan pada sistem operasi yang berbeda.

## Langkah 3: Buat Batch Processor dan Atur Paralelisme

Aspose OCR dilengkapi dengan `OcrBatchProcessor`, yang dapat menjalankan beberapa proses pengenalan secara paralel. Mengontrol jumlah thread mencegah aplikasi Anda menghabiskan CPU ketika Anda memiliki puluhan gambar.

```java
import com.aspose.ocr.OcrBatchProcessor;

// Step 3: Initialise the batch processor
OcrBatchProcessor ocrProcessor = new OcrBatchProcessor();

// Limit to 4 concurrent threads – a sweet spot for most desktops
ocrProcessor.setMaxParallelism(4);
```

Mengapa membatasi paralelisme? Jika Anda menjalankan terlalu banyak thread pada laptop standar, Anda mungkin melihat penurunan kecepatan alih‑alih percepatan. Mengatur `setMaxParallelism` memungkinkan Anda menyeimbangkan kecepatan dan stabilitas.

## Langkah 4: Jalankan Panggilan Batch OCR

Berikut inti dari **how to batch OCR**: satu panggilan `recognize` yang mengembalikan daftar objek `RecognitionResult`, satu per gambar.

```java
import com.aspose.ocr.RecognitionResult;
import java.util.List;

// Step 4: Execute batch OCR
List<RecognitionResult> recognitionResults = ocrProcessor.recognize(imageFiles);
```

Metode ini akan menunggu hingga semua gambar diproses, kemudian mengembalikan teks. Jika Anda membutuhkan perilaku non‑blocking, Anda dapat membungkusnya dalam `CompletableFuture`, namun untuk kebanyakan skrip panggilan sinkron menjaga kode tetap rapi.

## Langkah 5: Cetak Teks yang Diekstrak

Akhirnya, iterasi hasil dan tampilkan string yang dikenali. Ini menunjukkan bahwa kami berhasil **extract text from images** dengan berbagai format.

```java
// Step 5: Output the recognized text for each file
for (int i = 0; i < recognitionResults.size(); i++) {
    System.out.println("File: " + imageFiles.get(i));
    System.out.println(recognitionResults.get(i).getText());
    System.out.println("---");
}
```

### Output yang Diharapkan

```
File: YOUR_DIRECTORY/img1.png
The quick brown fox jumps over the lazy dog.
---
File: YOUR_DIRECTORY/img2.jpg
Invoice #12345
Total: $567.89
---
File: YOUR_DIRECTORY/img3.tif
Page 1 of 3
Report generated on 2026-02-09
---
```

Jika mesin OCR tidak dapat membaca sebuah file, metode `getText()` mengembalikan string kosong, sehingga Anda dapat menambahkan pemeriksaan sederhana untuk mencatat peringatan.

## Contoh Lengkap yang Berfungsi

Menggabungkan semuanya, berikut kelas Java lengkap yang siap dijalankan. Salin ke file bernama `BatchOcrTutorial.java`, sesuaikan path gambar, dan jalankan `javac && java`.

```java
import com.aspose.ocr.*;
import java.util.Arrays;
import java.util.List;

public class BatchOcrTutorial {
    public static void main(String[] args) throws Exception {

        // Step 1: Define the image files to be processed
        List<String> imageFiles = Arrays.asList(
                "YOUR_DIRECTORY/img1.png",
                "YOUR_DIRECTORY/img2.jpg",
                "YOUR_DIRECTORY/img3.tif");

        // Step 2: Create the batch OCR processor and optionally limit parallelism
        OcrBatchProcessor ocrProcessor = new OcrBatchProcessor();
        ocrProcessor.setMaxParallelism(4); // limit to 4 concurrent threads

        // Step 3: Perform OCR on all images in a single batch call
        List<RecognitionResult> recognitionResults = ocrProcessor.recognize(imageFiles);

        // Step 4: Output the recognized text for each file
        for (int i = 0; i < recognitionResults.size(); i++) {
            System.out.println("File: " + imageFiles.get(i));
            System.out.println(recognitionResults.get(i).getText());
            System.out.println("---");
        }
    }
}
```

Jalankan, dan Anda akan melihat konsol mencetak teks yang diekstrak untuk setiap file PNG, JPG, dan TIFF—tepat apa yang Anda butuhkan ketika **how to batch OCR** menjadi pertanyaan di benak Anda.

## Pertanyaan Umum & Kasus Tepi

### Bagaimana jika saya memiliki lebih dari tiga gambar?

Cukup tambahkan entri lebih banyak ke daftar `imageFiles`. Batch processor akan otomatis membagi pekerjaan ke thread yang Anda konfigurasi dengan `setMaxParallelism`.

### Gambar saya berada di sub‑folder—apakah saya harus mencantumkan masing‑masing secara manual?

Anda dapat mengumpulkan semua file secara programatik dengan ekstensi tertentu:

```java
try (Stream<Path> paths = Files.walk(Paths.get("YOUR_DIRECTORY"))) {
    List<String> imageFiles = paths
        .filter(Files::isRegularFile)
        .filter(p -> p.toString().matches(".*\\.(png|jpg|tif|tiff)$"))
        .map(Path::toString)
        .collect(Collectors.toList());
}
```

Ini membuat kode fleksibel dan tetap menghormati **how to batch OCR**.

### Bagaimana cara menangani hasil dengan kepercayaan rendah?

`RecognitionResult` menyediakan metode `getConfidence()`. Anda dapat menyaring hasil di bawah ambang tertentu dan mencoba lagi dengan pengaturan DPI yang lebih tinggi:

```java
ocrProcessor.setResolution(300); // increase DPI for better accuracy
```

### Apakah Aspose OCR mendukung bahasa lain?

Ya—cukup panggil `ocrProcessor.setLanguage(OcrLanguage.Spanish)` (atau enum yang didukung) sebelum panggilan `recognize`. Ini memperluas kegunaan di luar bahasa Inggris, menjadikan **extract text from images** benar‑benar multibahasa.

## Tips Kinerja

* **Ukuran batch penting** – Batch yang lebih besar mengurangi overhead, tetapi daftar yang sangat besar dapat mengonsumsi lebih banyak memori. Uji dengan 50–200 gambar per batch.
* **Paralelisme** – Pada CPU 4‑core, `setMaxParallelism(4)` biasanya memberikan throughput terbaik. Sesuaikan berdasarkan beban kerja server Anda.
* **Pra‑pemrosesan gambar** – Mengonversi gambar ke grayscale atau meningkatkan kontras sebelum OCR dapat meningkatkan akurasi, terutama untuk pemindaian yang berisik.

## Kesimpulan

Anda sekarang tahu **how to batch OCR** di Java menggunakan Aspose OCR, cara **extract text from images** dengan berbagai format, dan mengapa mengontrol paralelisme penting. Contoh kode lengkap menunjukkan pengenalan teks dari file PNG, JPG, dan TIFF dalam satu panggilan yang efisien.

Siap untuk langkah selanjutnya? Cobalah mengirimkan output OCR ke indeks pencarian, basis data, atau bahkan ringkas AI. Anda juga dapat bereksperimen dengan input PDF (Aspose OCR mendukungnya) atau menggabungkannya dengan pustaka pra‑pemrosesan gambar seperti OpenCV untuk akurasi yang lebih tinggi.

Selamat coding, dan ingat—batch OCR tidak harus menjadi sakit kepala. Dengan alat yang tepat dan pola yang jelas, Anda akan mengubah tumpukan gambar menjadi teks yang dapat dicari dalam sekejap.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}