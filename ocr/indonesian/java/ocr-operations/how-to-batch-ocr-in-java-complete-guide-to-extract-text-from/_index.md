---
category: general
date: 2026-09-18
description: Pelajari cara mengekstrak teks dari gambar di Java menggunakan Aspose
  OCR. Proses batch file PNG, JPG, dan TIFF secara efisien dalam satu panggilan.
keywords:
- extract text from images
- convert images to text
- how to batch ocr
- extract text from png
- extract text from jpg
- extract text from tiff
lastmod: 2026-09-18
og_description: Kuasi cara mengekstrak teks dari gambar di Java dengan batch OCR.
  Gunakan Aspose OCR untuk mengonversi file PNG, JPG, dan TIFF dalam satu panggilan.
og_image_alt: Diagram showing multiple image files processed together for batch OCR
og_title: Mengekstrak teks dari gambar di Java – panduan batch OCR
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: Learn how to extract text from images in Java using Aspose OCR. Batch
    process PNG, JPG, and TIFF files efficiently in a single call.
  headline: How to extract text from images in Java by batch OCR
  type: TechArticle
- questions:
  - answer: Yes, Aspose OCR is pure Java and requires no UI components, so it works
      perfectly on headless environments.
    question: Can I run this on a headless server?
  - answer: A commercial license is needed for production deployments; a free trial
      is available for evaluation.
    question: Is a license required for production use?
  - answer: Any OS that can run Java 17+, including Windows, Linux, and macOS.
    question: Which operating systems are supported?
  - answer: Over 60 languages are supported out of the box, ranging from English and
      Spanish to Arabic and Chinese.
    question: How many languages can Aspose OCR recognise?
  - answer: Individual image files up to 200 MB are supported; larger files should
      be split before processing.
    question: What is the maximum file size Aspose OCR can handle?
  type: FAQPage
tags:
- OCR
- Java
- Aspose
title: Cara mengekstrak teks dari gambar di Java dengan batch OCR
url: /id/java/ocr-operations/how-to-batch-ocr-in-java-complete-guide-to-extract-text-from/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara mengekstrak teks dari gambar di Java dengan batch OCR

Jika Anda perlu **mengekstrak teks dari gambar** dengan cepat dan tanpa menulis loop untuk setiap file, batch OCR adalah jawabannya. Dalam banyak proyek dunia nyata Anda menerima folder penuh pemindaian—struk PNG, screenshot JPG, atau TIFF multi‑halaman—dan Anda harus mengubahnya menjadi teks yang dapat dicari. Aspose OCR memungkinkan Anda melakukan hal itu dengan satu pemanggilan metode yang memproses file PNG, JPG, dan TIFF secara bersamaan, menghemat waktu pengembangan serta siklus CPU.

## Jawaban singkat
- **Apa yang dilakukan batch OCR?** Memproses beberapa file gambar dalam satu permintaan, mengembalikan teks untuk setiap file.
- **Format apa yang didukung?** PNG, JPG/JPEG, dan TIFF multi‑halaman didukung secara default.
- **Apakah saya memerlukan pustaka native terpisah?** Tidak, JAR Aspose OCR berisi semua yang Anda perlukan.
- **Bisakah saya mengontrol berapa banyak thread yang berjalan?** Ya, gunakan `setMaxParallelism` pada batch processor.
- **Versi Java apa yang diperlukan?** Java 17 atau yang lebih baru.

## Apa itu Aspose OCR?
Aspose OCR adalah pustaka Java yang mengenali teks cetak dan tulisan tangan dalam file gambar tanpa ketergantungan eksternal. Ia mendukung lebih dari 60 bahasa dan dapat memproses hingga 100 gambar per batch, menjadikannya ideal untuk digitalisasi dokumen berskala besar.

## Apa yang dibahas dalam tutorial ini
Muat daftar jalur gambar, buat `OcrBatchProcessor`, sesuaikan paralelisme, jalankan satu panggilan `recognize`, dan cetak string yang diekstrak. Pada akhir tutorial Anda akan memiliki program Java siap‑jalankan yang mengekstrak teks dari file PNG, JPG, dan TIFF secara massal.

- **Cara melakukan batch OCR** menggunakan `OcrBatchProcessor` milik Aspose.
- Cara **mengekstrak teks dari gambar** dengan berbagai format (PNG, JPG, TIFF).
- Tips mengontrol paralelisme agar aplikasi tetap responsif.
- Program Java lengkap yang dapat Anda salin‑tempel dan jalankan langsung.

Tidak diperlukan pengalaman sebelumnya dengan Aspose—hanya instalasi Java dasar dan IDE pilihan Anda. Pada akhir tutorial, Anda akan memiliki fondasi kuat untuk mengenali teks dari file PNG, JPG, dan TIFF secara massal.

---

![Diagram illustrating how to batch OCR multiple image files](/images/batch-ocr-diagram.png "cara melakukan batch OCR")

*Teks alt gambar: diagram cara melakukan batch OCR yang menunjukkan beberapa file gambar diproses bersama.*

## Prasyarat

| Persyaratan | Mengapa penting |
|-------------|-----------------|
| Java 17 atau lebih baru | Aspose OCR menargetkan JVM modern. |
| Maven atau Gradle | Mempermudah penambahan pustaka Aspose OCR. |
| Pengetahuan dasar Java | Diperlukan untuk memahami alur kode. |
| Sekumpulan gambar contoh (`.png`, `.jpg`, `.tif`) | Untuk melihat proses ekstraksi secara langsung. |

Jika Anda sudah memiliki semua ini, bagus—mari kita mulai.

## Langkah 1: tambahkan Aspose OCR ke proyek Anda

Hal pertama yang Anda perlukan adalah JAR Aspose OCR. Dengan Maven, tambahkan ini ke `pom.xml` Anda:

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

Menambahkan dependensi ini akan menarik semua yang diperlukan untuk **mengekstrak teks dari png**, **mengekstrak teks dari jpg**, dan **mengekstrak teks dari tiff**. Tidak ada pustaka native tambahan yang dibutuhkan.

## Langkah 2: definisikan file gambar yang ingin diproses

Sekarang kita beri tahu mesin OCR file mana yang akan ditangani. Di sinilah **cara melakukan batch OCR** benar‑benar bersinar—cukup berikan daftar jalur dan biarkan pustaka melakukan pekerjaan berat.

```java
import java.util.Arrays;
import java.util.List;

// Step 2: List your image files (PNG, JPG, TIFF)
List<String> imageFiles = Arrays.asList(
        "YOUR_DIRECTORY/img1.png",   // PNG file – recognize text from png
        "YOUR_DIRECTORY/img2.jpg",   // JPG file – recognize text from jpg
        "YOUR_DIRECTORY/img3.tif");  // TIFF file – recognize text from tiff
```

> **Tip profesional:** Gunakan jalur file absolut atau `Paths.get(...)` untuk menghindari kejutan pada OS yang berbeda.

## Langkah 3: buat batch processor dan sesuaikan paralelisme

Aspose OCR menyertakan `OcrBatchProcessor`, yang dapat menjalankan beberapa pengenalan secara paralel. Mengontrol jumlah thread mencegah aplikasi Anda menghabiskan CPU ketika Anda memiliki puluhan gambar.

```java
import com.aspose.ocr.OcrBatchProcessor;

// Step 3: Initialise the batch processor
OcrBatchProcessor ocrProcessor = new OcrBatchProcessor();

// Limit to 4 concurrent threads – a sweet spot for most desktops
ocrProcessor.setMaxParallelism(4);
```

Mengapa membatasi paralelisme? Jika Anda menjalankan terlalu banyak thread pada laptop dengan spesifikasi modest, Anda mungkin melihat penurunan kinerja alih‑alih percepatan. Menetapkan `setMaxParallelism` memungkinkan Anda menyeimbangkan kecepatan dan stabilitas.

## Langkah 4: jalankan panggilan batch OCR

Berikut inti **cara melakukan batch OCR**: satu panggilan `recognize` yang mengembalikan daftar objek `RecognitionResult`, satu per gambar.  
`recognize` memproses gambar yang diberikan dan mengembalikan daftar objek `RecognitionResult`, masing‑masing berisi teks yang diekstrak.

```java
import com.aspose.ocr.RecognitionResult;
import java.util.List;

// Step 4: Execute batch OCR
List<RecognitionResult> recognitionResults = ocrProcessor.recognize(imageFiles);
```

Metode ini akan blok hingga semua gambar selesai diproses, kemudian mengembalikan teks. Jika Anda memerlukan perilaku non‑blocking, Anda dapat membungkusnya dalam `CompletableFuture`, tetapi untuk kebanyakan skrip panggilan sinkron membuat kode tetap rapi.

## Langkah 5: cetak teks yang diekstrak

Akhirnya, iterasi hasil dan tampilkan string yang dikenali. Ini menunjukkan bahwa kita berhasil **mengekstrak teks dari gambar** dengan berbagai format.  
`RecognitionResult` menyimpan output OCR untuk satu gambar, termasuk teks yang diekstrak dan skor kepercayaan.

```java
// Step 5: Output the recognized text for each file
for (int i = 0; i < recognitionResults.size(); i++) {
    System.out.println("File: " + imageFiles.get(i));
    System.out.println(recognitionResults.get(i).getText());
    System.out.println("---");
}
```

### Output yang diharapkan

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

## Contoh lengkap yang dapat dijalankan

Menggabungkan semuanya, berikut kelas Java lengkap yang siap dijalankan. Salin ke file bernama `BatchOcrTutorial.java`, sesuaikan jalur gambar, dan jalankan `javac && java`.

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

Jalankan, dan Anda akan melihat konsol mencetak teks yang diekstrak untuk setiap file PNG, JPG, dan TIFF—tepat apa yang Anda butuhkan ketika **cara melakukan batch OCR** menjadi pertanyaan utama.

## Pertanyaan umum & kasus tepi

### Bagaimana jika saya memiliki lebih dari tiga gambar?
Cukup tambahkan lebih banyak entri ke daftar `imageFiles`. Batch processor akan otomatis membagi pekerjaan di antara thread yang Anda konfigurasikan dengan `setMaxParallelism`.

### Gambar saya berada di sub‑folder—apakah saya harus mencantumkan masing‑masing secara manual?
`Files.list` mengembalikan stream jalur yang diisi secara lazy dalam sebuah direktori.

```java
try (Stream<Path> paths = Files.walk(Paths.get("YOUR_DIRECTORY"))) {
    List<String> imageFiles = paths
        .filter(Files::isRegularFile)
        .filter(p -> p.toString().matches(".*\\.(png|jpg|tif|tiff)$"))
        .map(Path::toString)
        .collect(Collectors.toList());
}
```

Ini membuat kode tetap fleksibel dan tetap menghormati **cara melakukan batch OCR**.

### Bagaimana menangani hasil dengan kepercayaan rendah?
`getConfidence()` mengembalikan nilai numerik yang menunjukkan seberapa besar kemungkinan teks yang dikenali benar.

```java
ocrProcessor.setResolution(300); // increase DPI for better accuracy
```

### Apakah Aspose OCR mendukung bahasa lain?
Ya—panggil `ocrProcessor.setLanguage(OcrLanguage.Spanish)` (atau enum yang didukung lainnya) sebelum panggilan `recognize`. Ini memperluas kegunaan di luar bahasa Inggris, menjadikan **mengekstrak teks dari gambar** benar‑benar multibahasa.

## Tips performa

* **Ukuran batch penting** – Batch yang lebih besar mengurangi overhead, tetapi daftar yang sangat besar dapat mengonsumsi lebih banyak memori. Uji dengan 50–200 gambar per batch.
* **Paralelisme** – Pada CPU 4‑core, `setMaxParallelism(4)` biasanya memberikan throughput terbaik. Sesuaikan berdasarkan beban kerja server Anda.
* **Pra‑pemrosesan gambar** – Mengonversi gambar ke skala abu‑abu atau meningkatkan kontras sebelum OCR dapat meningkatkan akurasi, terutama untuk pemindaian yang berisik.

## Kesimpulan

Anda kini tahu **cara melakukan batch OCR** di Java menggunakan Aspose OCR, cara **mengekstrak teks dari gambar** dengan berbagai format, dan mengapa mengontrol paralelisme itu penting. Contoh kode lengkap menunjukkan cara mengenali teks dari file PNG, JPG, dan TIFF dalam satu panggilan efisien.

Siap untuk langkah selanjutnya? Salurkan output OCR ke indeks pencarian, basis data, atau rangkuman AI. Anda juga dapat bereksperimen dengan input PDF (Aspose OCR mendukungnya) atau menggabungkannya dengan pustaka pra‑pemrosesan gambar seperti OpenCV untuk akurasi yang lebih tinggi.

Selamat coding, dan ingat—batch OCR tidak harus menjadi sakit kepala. Dengan alat yang tepat dan pola yang jelas, Anda akan mengubah tumpukan gambar menjadi teks yang dapat dicari dalam sekejap.

## Pertanyaan yang sering diajukan

**T: Bisakah saya menjalankannya di server tanpa tampilan?**  
J: Ya, Aspose OCR murni Java dan tidak memerlukan komponen UI, sehingga berfungsi sempurna di lingkungan headless.

**T: Apakah lisensi diperlukan untuk penggunaan produksi?**  
J: Lisensi komersial diperlukan untuk deployment produksi; versi percobaan gratis tersedia untuk evaluasi.

**T: Sistem operasi apa yang didukung?**  
J: Semua OS yang dapat menjalankan Java 17+, termasuk Windows, Linux, dan macOS.

**T: Berapa banyak bahasa yang dapat dikenali Aspose OCR?**  
J: Lebih dari 60 bahasa didukung secara default, mulai dari Inggris dan Spanyol hingga Arab dan Mandarin.

**T: Ukuran file maksimum apa yang dapat ditangani Aspose OCR?**  
J: File gambar individu hingga 200 MB didukung; file yang lebih besar sebaiknya dipotong sebelum diproses.

---

**Terakhir diperbarui:** 2026-09-18  
**Diuji dengan:** Aspose OCR 24.9 untuk Java  
**Penulis:** Aspose

## Tutorial terkait

- [Extract Text from Images – OCR Basics for Java](/ocr/java/ocr-basics/)
- [How To Batch Ocr In Java Complete Guide To Extract Text From](/ocr/java/ocr-operations/how-to-batch-ocr-in-java-complete-guide-to-extract-text-from/)
- [Preprocess Image Ocr In Java Boost Accuracy Extract Text](/ocr/java/advanced-ocr-techniques/preprocess-image-ocr-in-java-boost-accuracy-extract-text/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}