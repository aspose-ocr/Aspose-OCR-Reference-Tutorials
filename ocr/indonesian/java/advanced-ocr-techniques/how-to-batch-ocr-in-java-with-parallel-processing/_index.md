---
category: general
date: 2026-04-26
description: Cara melakukan OCR batch menggunakan Java dan Aspose OCR – mengenali
  teks dari gambar, mengekstrak teks dari PNG, dan menggunakan semua core CPU untuk
  pemrosesan OCR paralel.
draft: false
keywords:
- how to batch OCR
- recognize text from images
- extract text from PNG
- use all CPU cores
- parallel OCR processing
language: id
og_description: Cara melakukan OCR batch di Java. Pelajari cara mengenali teks dari
  gambar, mengekstrak teks dari PNG, dan menggunakan semua inti CPU untuk pemrosesan
  OCR paralel yang cepat.
og_title: Cara Batch OCR di Java – Panduan Pemrosesan Paralel
tags:
- OCR
- Java
- Aspose
- Performance
title: Cara Melakukan OCR Batch di Java dengan Pemrosesan Paralel
url: /id/java/advanced-ocr-techniques/how-to-batch-ocr-in-java-with-parallel-processing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Batch OCR di Java – Panduan Lengkap

Pernah bertanya-tanya **bagaimana cara batch OCR** ketika Anda memiliki puluhan tangkapan layar PNG yang menatap kembali? Anda tidak sendirian. Kebanyakan pengembang menemui hambatan begitu demo satu‑gambar berhasil dan beban kerja nyata—ratusan file—mulai membebani CPU.  

Dalam tutorial ini kami akan membahas solusi praktis, end‑to‑end yang **mengenali teks dari gambar**, mengekstrak konten setiap PNG, dan **menggunakan semua core CPU** untuk mempercepat pekerjaan. Pada akhir tutorial Anda akan memiliki kelas Java yang dapat digunakan kembali yang memproses folder gambar secara paralel, memberi Anda kecepatan mesin multi‑threaded tanpa kerepotan mengelola thread pool secara manual.

> **Apa yang akan Anda dapatkan:** program Java yang dapat dijalankan sepenuhnya (Aspose OCR), penjelasan langkah‑demi‑langkah, tip untuk kasus tepi, dan pratinjau output konsol yang diharapkan.

---

## Prasyarat

Sebelum kita menyelam lebih dalam, pastikan Anda memiliki:

- **Java 17** (atau JDK terbaru) terinstal dan `JAVA_HOME` dikonfigurasi.  
- **Aspose OCR for Java** library (versi 23.10 atau lebih baru). Anda dapat mengunduhnya dari Maven Central:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version>
</dependency>
```

- Sebuah folder yang berisi beberapa **gambar PNG** yang ingin Anda proses.  
- Familiaritas dasar dengan sintaks Java—tidak memerlukan hal yang rumit.

Jika ada yang belum Anda kenal, berhenti sejenak dan siapkan terlebih dahulu; sisanya mengasumsikan semuanya sudah siap.

## Langkah 1 – Buat OCR Engine Single‑Threaded (Baseline)

Pertama-tama: buat instance `OcrEngine`. Objek ini melakukan pekerjaan berat—memuat gambar, menjalankan jaringan saraf, dan mengembalikan teks biasa.

```java
import com.aspose.ocr.*;

public class ParallelOcrDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();
```

> **Mengapa ini penting:** Menggunakan kembali engine yang sama untuk banyak file menghindari overhead memuat model bahasa berulang kali, yang dapat menjadi pembunuh kinerja saat Anda **memproses batch**.

## Langkah 2 – Aktifkan Pemrosesan Paralel dengan Semua Core yang Tersedia

Sekarang kami memberi tahu Aspose OCR untuk menyebarkan pekerjaan ke setiap prosesor logis yang tersedia pada mesin Anda. Pemanggilan `Runtime.getRuntime().availableProcessors()` mengembalikan angka tersebut, baik Anda memiliki laptop 4‑core atau server 32‑core.

```java
        // Step 2: Enable parallel processing by using all available logical processors
        ocrEngine.getRecognitionSettings()
                 .setNumberOfThreads(Runtime.getRuntime().availableProcessors());
```

> **Tip pro:** Pada CPU hyper‑threaded Anda akan melihat jumlah core dua kali lipat, tetapi library secara cerdas membatasi thread pool, sehingga Anda tidak perlu menyesuaikannya secara manual.

## Langkah 3 – Kumpulkan Gambar yang Ingin Diproses

Hard‑coding array kecil bekerja untuk demo, tetapi dalam pekerjaan batch dunia nyata Anda kemungkinan akan memindai sebuah direktori. Di bawah ini kami menunjukkan kedua pendekatan.

```java
        // Step 3a: Define a static list (quick demo)
        String[] imageFiles = {
            "YOUR_DIRECTORY/image1.png",
            "YOUR_DIRECTORY/image2.png",
            "YOUR_DIRECTORY/image3.png"
        };

        // Step 3b: Or, dynamically load every PNG in a folder
        // File folder = new File("YOUR_DIRECTORY");
        // String[] imageFiles = folder.list((dir, name) -> name.toLowerCase().endsWith(".png"));
```

> **Mengapa Anda mungkin membutuhkan ini:** Jika Anda perlu **mengekstrak teks dari file PNG** yang datang melalui pipeline unggahan, versi dinamis secara otomatis mengambil file baru tanpa perubahan kode.

## Langkah 4 – Jalankan OCR pada Setiap Gambar Menggunakan Engine yang Sama

Loop di bawah ini menetapkan gambar saat ini, menjalankan `recognize()`, dan mencetak hasilnya. Karena kami mengaktifkan multi‑threading sebelumnya, setiap pemanggilan dapat berjalan pada thread pekerja terpisah di belakang layar.

```java
        // Step 4: Recognize text from each image (reusing the same engine instance)
        for (String imagePath : imageFiles) {
            ocrEngine.setImage(imagePath);
            String recognizedText = ocrEngine.recognize().getText();
            System.out.println("Result for " + imagePath + ":\n" + recognizedText);
        }
    }
}
```

### Output Konsol yang Diharapkan

```
Result for YOUR_DIRECTORY/image1.png:
Welcome to the OCR demo.
Result for YOUR_DIRECTORY/image2.png:
Invoice #12345
Total: $567.89
Result for YOUR_DIRECTORY/image3.png:
© 2026 MyCompany. All rights reserved.
```

Jika gambar berisi skrip non‑Latin atau tangkapan layar beresolusi rendah, Anda mungkin melihat karakter kacau—sesuaikan DPI engine atau pengaturan pengurangan noise secara tepat (lihat bagian “Advanced Tweaks” di bawah).

## Penyesuaian Lanjutan – Penyempurnaan untuk Batch Dunia Nyata

| Situasi | Pengaturan yang Disarankan | Potongan Kode |
|-----------|-------------------|--------------|
| PNG beresolusi rendah | Tingkatkan `setResolution` | `ocrEngine.getRecognitionSettings().setResolution(300);` |
| Dokumen multibahasa | Tambahkan paket bahasa | `ocrEngine.getRecognitionSettings().addLanguage(OcrLanguage.Spanish);` |
| Batch sangat besar (10rb+ file) | Stream file alih-alih memuat semua nama sekaligus | Use `Files.walk(Paths.get("YOUR_DIRECTORY"))` with a filter. |
| Keterbatasan memori | Buang engine setelah setiap N file | `if (counter % 500 == 0) ocrEngine.dispose();` |

> **Ingat:** Meskipun kami **menggunakan semua core CPU**, OS tetap mengelola penjadwalan thread. Jika Anda melihat mesin menjadi lambat, pertimbangkan membatasi thread ke `availableProcessors() - 1`.

## Kesalahan Umum & Cara Menghindarinya

1. **Kehabisan handle file** – Java membatasi jumlah file terbuka per proses. Tutup setiap gambar secara eksplisit jika Anda menemui error `Too many open files`:

   ```java
   ocrEngine.setImage(imagePath);
   String text = ocrEngine.recognize().getText();
   ocrEngine.getImage().close(); // releases the handle
   ```

2. **Pemilih pemisah path yang salah pada Windows** – Gunakan `File.separator` atau `Paths.get()` untuk tetap platform‑agnostic.

3. **Callback kustom yang tidak thread‑safe** – Jika Anda menambahkan listener progres, pastikan thread‑safe (misalnya, `AtomicInteger`).

## Contoh Lengkap yang Berfungsi (Siap Salin‑Tempel)

```java
import com.aspose.ocr.*;
import java.io.File;

public class ParallelOcrDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Enable parallelism – use every logical CPU core
        ocrEngine.getRecognitionSettings()
                 .setNumberOfThreads(Runtime.getRuntime().availableProcessors());

        // 3️⃣ Locate PNG files (adjust the folder path)
        File folder = new File("YOUR_DIRECTORY");
        String[] imageFiles = folder.list((dir, name) ->
                name.toLowerCase().endsWith(".png"));

        if (imageFiles == null || imageFiles.length == 0) {
            System.out.println("No PNG files found in the directory.");
            return;
        }

        // 4️⃣ Process each image – same engine, multi‑threaded under the hood
        for (String imageName : imageFiles) {
            String imagePath = folder.getAbsolutePath() + File.separator + imageName;
            ocrEngine.setImage(imagePath);
            String recognizedText = ocrEngine.recognize().getText();

            System.out.println("Result for " + imagePath + ":\n" + recognizedText);
            // Optional: free the image handle (good for huge batches)
            ocrEngine.getImage().close();
        }

        // Clean up
        ocrEngine.dispose();
    }
}
```

> **Apa yang dilakukan ini:** Memindai `YOUR_DIRECTORY` untuk setiap `.png`, menjalankan OCR secara paralel, mencetak setiap hasil, dan akhirnya melepaskan sumber daya. Anda dapat menambahkan kelas ini ke proyek Maven apa pun, menjalankan `mvn exec:java`, dan melihat peningkatan kecepatan dibandingkan loop single‑threaded.

## Kesimpulan

Anda sekarang memiliki pola yang solid dan siap produksi untuk **bagaimana cara batch OCR** di Java. Dengan menggunakan kembali satu `OcrEngine`, mengaktifkan **pemrosesan OCR paralel**, dan memanfaatkan **semua core CPU**, Anda dapat **mengenali teks dari gambar** dalam sebagian kecil waktu dibandingkan loop naïf.  

Dari sini Anda dapat:

- Menghubungkan output ke indeks pencarian (Elasticsearch) untuk pencarian cepat.  
- Menggabungkan dengan konverter PDF‑to‑PNG untuk **mengekstrak teks dari PNG** yang tertanam dalam dokumen hasil scan.  
- Menambahkan penanganan error dan logika retry untuk drive jaringan yang tidak stabil.

Terus bereksperimen—ganti dengan JPEG, sesuaikan DPI, atau bahkan alirkan frame video untuk transkripsi real‑time. Ide inti tetap sama, dan peningkatan performa biasanya dramatis.

Selamat coding, semoga pipeline OCR Anda berjalan secepat mesin kopi Anda! 🚀

![Diagram yang menunjukkan alur kerja OCR paralel – cara batch OCR di beberapa core CPU]

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}