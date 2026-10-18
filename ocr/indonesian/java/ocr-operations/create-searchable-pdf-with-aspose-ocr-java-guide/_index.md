---
category: general
date: 2026-03-26
description: Buat PDF yang dapat dicari menggunakan Aspose.OCR Java – pelajari cara
  memuat gambar OCR, mengatur bahasa utama, mengekstrak teks dari gambar, dan menyimpan
  PDF OCR.
draft: false
keywords:
- create searchable pdf
- set primary language
- extract text from image
- load image ocr
- save ocr pdf
language: id
og_description: Buat PDF yang dapat dicari dengan Aspose.OCR Java. Panduan langkah
  demi langkah untuk memuat OCR gambar, mengatur bahasa utama, mengekstrak teks dari
  gambar, dan menyimpan PDF OCR.
og_title: Buat PDF yang Dapat Dicari dengan Aspose.OCR – Panduan Java
tags:
- Aspose.OCR
- Java
- PDF
- OCR
title: Buat PDF yang Dapat Dicari dengan Aspose.OCR – Panduan Java
url: /id/java/ocr-operations/create-searchable-pdf-with-aspose-ocr-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat PDF yang Dapat Dicari dengan Aspose.OCR – Panduan Java

Pernah membutuhkan untuk **create searchable pdf** dari dokumen yang dipindai tetapi tidak yakin harus mulai dari mana? Anda tidak sendirian—banyak pengembang mengalami hal yang sama saat pertama kali menangani OCR di Java. Kabar baiknya, Aspose.OCR membuat seluruh alur—dari memuat gambar hingga mengatur bahasa utama dan akhirnya menyimpan PDF yang mendukung OCR—sangat mudah. Dalam tutorial ini kami akan membahas contoh lengkap yang dapat dijalankan yang **extracts text from image**, memungkinkan Anda **set primary language**, dan berakhir dengan **save OCR pdf** yang dapat Anda buka di pembaca apa pun.

Kami juga akan membahas beberapa tips praktis, seperti mengaktifkan akselerasi GPU untuk pemrosesan yang lebih cepat dan menangani dokumen berbahasa campuran (Tamil + English dalam kasus kami). Pada akhir tutorial, Anda akan memiliki potongan kode yang solid dan siap produksi yang dapat Anda masukkan ke dalam proyek Anda.

## Apa yang Anda Butuhkan

- **Java 17** (atau JDK terbaru; Aspose.OCR mendukung Java 8+)
- **Aspose.OCR for Java** library (unduh dari situs resmi atau tambahkan via Maven)
- Sebuah **license file** (atau trial 30‑hari)
- File gambar yang berisi teks (demo menggunakan `sample-mixed-tamil-eng.jpg`)

Tidak ada kerangka kerja tambahan, tidak ada dependensi native—hanya Java murni dan Aspose.JARs.

---

## Langkah 1: Buat PDF yang Dapat Dicari – Menyiapkan Proyek

Sebelum kita masuk ke kode, pastikan proyek siap untuk membuat file **create searchable pdf**.

```bash
# Maven dependency (add to pom.xml)
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- check the latest version -->
</dependency>
```

> **Pro tip:** Jaga nomor versi tetap terbaru; rilis yang lebih baru sering menyertakan perbaikan kinerja untuk penggunaan GPU.

Sekarang buat kelas Java sederhana bernama `RecentFeaturesDemo`. Kelas ini akan menampung semua logika yang kita perlukan untuk **load image OCR**, mengonfigurasi pengaturan bahasa, dan akhirnya **save OCR pdf**.

---

## Langkah 2: Muat Image OCR dan Inisialisasi Engine

Langkah nyata pertama dalam alur adalah **load image OCR**. Ini memberi tahu Aspose.OCR file mana yang akan dianalisis.

```java
import com.aspose.ocr.*;

public class RecentFeaturesDemo {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Load your Aspose.OCR license (or use the 30‑day trial)
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.Java.lic");

        // 2️⃣ Create and configure the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Enable GPU acceleration – speeds up recognition dramatically
        ocrEngine.getEngineSettings().setUseGpu(true);
        // Use all available CPU cores for parallel processing
        ocrEngine.getEngineSettings().setUseParallelProcessing(true);
```

> **Why this matters:** Mengaktifkan GPU (`setUseGpu(true)`) dapat memotong waktu pemrosesan hingga 70 % pada perangkat keras modern, sementara pemrosesan paralel memastikan CPU tidak menganggur ketika GPU sibuk.

---

## Langkah 3: Atur Bahasa Utama (dan Bahasa Sekunder)

Jika Anda melewatkan langkah ini, Aspose.OCR akan mencoba menebak bahasa, yang lebih lambat dan kurang akurat. Berikut cara **set primary language** ke Tamil dan menambahkan English sebagai cadangan.

```java
        // 3️⃣ Define languages – primary is Tamil, secondary is English
        ocrEngine.getLanguageSettings().setLanguage(Language.Tamil);
        ocrEngine.getLanguageSettings().setSecondaryLanguage(Language.English);
```

> **Explanation:** Bahasa utama memengaruhi set karakter dan kamus yang digunakan selama pengenalan. Menambahkan bahasa sekunder sangat penting untuk dokumen dengan skrip campuran (bayangkan sebuah kwitansi dengan teks Tamil dan English).  
> **Edge case:** Jika dokumen Anda berisi lebih dari dua bahasa, Anda dapat memanggil `addAdditionalLanguage(...)` untuk setiap bahasa tambahan.

---

## Langkah 4: Praproses Gambar – Deskew & Denoise

Gambar yang dipindai sering mengalami rotasi atau noise latar belakang. Praproses membantu mesin OCR **extract text from image** dengan lebih andal.

```java
        // 4️⃣ Pre‑processing options
        ocrEngine.getPreprocessingSettings()
                 .setDeskew(true)   // auto‑rotate tilted pages
                 .setDenoise(true); // suppress speckles and background patterns
```

> **Tip:** Jika Anda tahu gambar sudah bersih, Anda dapat melewatkan `setDenoise(true)` untuk menghemat beberapa milidetik.

---

## Langkah 5: Muat File Gambar

Setelah engine siap, kami menunjukannya ke file yang ingin dianalisis.

```java
        // 5️⃣ Load the image you want to recognize
        String imagePath = "YOUR_DIRECTORY/sample-mixed-tamil-eng.jpg";
        ocrEngine.setImage(ImageStream.fromFile(imagePath));
```

> **What if the path is wrong?** Aspose.OCR melempar `FileNotFoundException` yang jelas. Bungkus pemanggilan dalam try‑catch jika Anda memerlukan penanganan error yang elegan.

---

## Langkah 6: Jalankan OCR dan Extract Text from Image

Dengan semua konfigurasi selesai, saatnya menjalankan pengenalan. Langkah ini **extracts text from image** sekaligus menyiapkan data yang diperlukan untuk pembuatan PDF.

```java
        // 6️⃣ Perform recognition
        if (ocrEngine.recognize()) {
            String recognizedText = ocrEngine.getText();

            // Print the raw OCR output – handy for debugging
            System.out.println("Recognized text:");
            System.out.println(recognizedText);
```

Output konsol tipikal untuk gambar demo terlihat seperti:

```
வணக்கம் World
This is a mixed language sample.
```

Anda akan melihat baris Tamil ditampilkan dengan benar, diikuti oleh English. Itulah hasil dari **set primary language** yang tepat.

---

## Langkah 7: Save OCR PDF – Bagian Akhir

Bagian terakhir dari puzzle adalah **save OCR pdf**. Aspose.OCR dapat menyematkan lapisan teks tak terlihat di atas gambar asli, menjadikan PDF dapat dicari.

```java
            // 7️⃣ (Optional) Save a searchable PDF with an OCR layer
            String pdfPath = "YOUR_DIRECTORY/searchable.pdf";
            ocrEngine.save(pdfPath, SaveFormat.PdfSearchable);

            System.out.println("\nSearchable PDF saved to: " + pdfPath);
        } else {
            System.err.println("Recognition failed: " + ocrEngine.getErrorMessage());
        }
    }
}
```

Buka `searchable.pdf` di Adobe Reader, tekan **Ctrl + F**, dan Anda dapat mencari kata-kata Tamil maupun English—tepat seperti yang dijanjikan oleh alur kerja **create searchable pdf**.

---

## Contoh Kerja Penuh (Copy‑Paste)

Berikut adalah program lengkap yang dapat Anda kompilasi dan jalankan apa adanya. Ganti jalur placeholder dengan direktori Anda sendiri.

```java
import com.aspose.ocr.*;

public class RecentFeaturesDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Load your Aspose.OCR license (or use the 30‑day trial)
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.Java.lic");

        // Step 2: Create and configure the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getEngineSettings().setUseGpu(true);                     // enable CUDA GPU acceleration
        ocrEngine.getEngineSettings().setUseParallelProcessing(true);     // use multiple CPU cores
        ocrEngine.getLanguageSettings().setLanguage(Language.Tamil);      // primary language
        ocrEngine.getLanguageSettings().setSecondaryLanguage(Language.English); // secondary language
        ocrEngine.getPreprocessingSettings()
                 .setDeskew(true)   // correct image rotation
                 .setDenoise(true); // reduce background noise

        // Step 3: Load the image you want to recognize
        String imagePath = "YOUR_DIRECTORY/sample-mixed-tamil-eng.jpg";
        ocrEngine.setImage(ImageStream.fromFile(imagePath));

        // Step 4: Run OCR and obtain the plain‑text result
        if (ocrEngine.recognize()) {
            String recognizedText = ocrEngine.getText();

            // Step 5: (Optional) Save a searchable PDF with an OCR layer
            String pdfPath = "YOUR_DIRECTORY/searchable.pdf";
            ocrEngine.save(pdfPath, SaveFormat.PdfSearchable);

            System.out.println("Recognized text:");
            System.out.println(recognizedText);
            System.out.println("\nSearchable PDF saved to: " + pdfPath);
        } else {
            System.err.println("Recognition failed: " + ocrEngine.getErrorMessage());
        }
    }
}
```

Jalankan dengan:

```bash
javac -cp "path/to/aspose-ocr.jar" RecentFeaturesDemo.java
java -cp ".:path/to/aspose-ocr.jar" RecentFeaturesDemo
```

Anda akan melihat teks yang diekstrak dicetak ke konsol, diikuti konfirmasi bahwa **searchable pdf** telah ditulis ke disk.

---

## Pertanyaan Umum & Kasus Edge

### Bagaimana jika saya perlu **load image OCR** dari array byte?

Anda dapat mengganti `ImageStream.fromFile(imagePath)` dengan `ImageStream.fromBytes(byteArray)`. Ini berguna ketika gambar berasal dari basis data atau layanan web.

### Bagaimana cara menangani PDF yang sudah berisi gambar?

Aspose.OCR dapat bekerja langsung pada halaman PDF: `ocrEngine.setDocument(PdfDocument.fromFile("input.pdf"))`. Engine akan meraster setiap halaman secara internal sebelum pengenalan.

### GPU saya tidak terdeteksi—haruskah saya tetap menggunakan `setUseGpu(true)`?

Jika `setUseGpu(true)` gagal, Aspose.OCR secara otomatis beralih ke CPU. Anda dapat memeriksa `ocrEngine.getEngineSettings().isGpuAvailable()` sebelum mengaktifkannya.

### Bisakah saya **save OCR pdf** dengan metadata khusus?

Ya. Setelah pengenalan, gunakan `ocrEngine.getPdfSaveOptions().setTitle("My Document")` atau `setAuthor("John Doe")` sebelum memanggil `save`.

---

## Tips Kinerja untuk Batch Besar

- **Batch processing:** Gunakan kembali instance `OcrEngine` yang sama untuk beberapa gambar. Hanya panggil `ocrEngine.clear()` di antara proses.
- **Thread pool:** Bungkus setiap tugas gambar dalam `Callable` dan kirim ke `ExecutorService`. Karena kami mengaktifkan pemrosesan paralel, setiap thread akan memanfaatkan penggunaan multi‑core.
- **Memory management:** Untuk gambar gigapiksel, pertimbangkan down‑sampling dengan `ocrEngine.getPreprocessingSettings().setResizeFactor(0.5)` agar penggunaan RAM tetap wajar.

---

## Kesimpulan

Kami baru saja melewati alur kerja lengkap **create searchable pdf** menggunakan Aspose.OCR untuk Java. Dimulai dari **load image OCR**, kami

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}