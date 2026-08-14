---
category: general
date: 2026-07-05
description: Kompres gambar PDF saat mengonversi PNG ke PDF menggunakan Java. Pelajari
  pra‑pemrosesan gambar untuk OCR, kenali teks JPG, dan lakukan OCR batch ke PDF dalam
  satu tutorial.
draft: false
keywords:
- compress pdf images
- convert png to pdf
- image preprocessing for ocr
- recognize text jpg
- batch ocr to pdf
language: id
og_description: Kompres gambar PDF dan konversi PNG ke PDF menggunakan Java. Panduan
  ini mencakup pra‑pemrosesan gambar untuk OCR, mengenali teks JPG, dan OCR batch
  ke PDF.
og_title: Kompres Gambar PDF dengan Java – Tutorial OCR Batch Lengkap
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Compress PDF images while converting PNG to PDF using Java. Learn image
    preprocessing for OCR, recognize text JPG, and batch OCR to PDF in one tutorial.
  headline: Compress PDF Images with Java – Full Batch OCR to PDF Guide
  type: TechArticle
- description: Compress PDF images while converting PNG to PDF using Java. Learn image
    preprocessing for OCR, recognize text JPG, and batch OCR to PDF in one tutorial.
  name: Compress PDF Images with Java – Full Batch OCR to PDF Guide
  steps:
  - name: Expected Output
    text: 'Running the program prints a line for each image, e.g.:'
  - name: What if my server has no GPU?
    text: Just set `gpuSettings.setEnabled(false)`. The rest of the pipeline remains
      unchanged, and you still get multithreaded CPU processing.
  - name: My PDFs are still too large—can I lower the quality further?
    text: Yes. Adjust `options.setImageQuality(70)` or even `50`. Lower values shrink
      size more aggressively but may blur fine glyphs. Test with a representative
      sample.
  - name: How do I handle other image formats (TIFF, BMP)?
    text: 'Add the extensions to the filter lambda:'
  - name: Can I keep the original color images instead of binarizing?
    text: Replace `.addBinarize()` with `.addGrayscale()` in the preprocessor builder
      if you need color retention for downstream analysis.
  type: HowTo
tags:
- ocr
- java
- pdf
- image-processing
title: Kompres Gambar PDF dengan Java – Panduan Lengkap OCR Batch ke PDF
url: /id/java/advanced-ocr-techniques/compress-pdf-images-with-java-full-batch-ocr-to-pdf-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kompres Gambar PDF dengan Java – Panduan OCR Batch Lengkap ke PDF

Pernahkah Anda perlu **mengompres gambar PDF** sambil mengubah folder PNG menjadi PDF yang dapat dicari? Anda bukan satu‑satunya. Dalam banyak pipeline otomatisasi, titik sakit terbesar adalah menyeimbangkan kualitas gambar, akurasi OCR, dan ukuran PDF akhir—semua sekaligus.  

Dalam tutorial ini kita akan membahas solusi praktis yang **mengonversi PNG ke PDF**, menerapkan **praproses gambar untuk OCR**, dan akhirnya **mengompres gambar PDF** sehingga output tetap ringan. Pada akhir tutorial Anda akan tahu cara **mengenali teks JPG**, menyiapkan alur kerja **batch OCR ke PDF**, dan menjaga PDF Anda tetap rapi.

## Apa yang Akan Anda Pelajari

- Menyiapkan Aspose OCR untuk Java dan menerapkan lisensi.
- Mengonfigurasi mesin untuk multithreading, akselerasi GPU, dan koreksi ejaan.
- Membangun pipeline **praproses gambar untuk OCR** yang dapat digunakan kembali (denoise, kontras, binarisasi).
- Menggunakan **PdfSaveOptions** untuk **mengompres gambar PDF** tanpa mengorbankan keterbacaan.
- Melakukan loop melalui sebuah direktori untuk **mengonversi PNG ke PDF** dan **mengenali teks JPG** secara massal.
- Program Java lengkap yang siap dijalankan dan dapat dimasukkan ke proyek apa pun.

> **Prasyarat**: Java 8+, Maven atau Gradle, lisensi Aspose OCR untuk Java, dan folder berisi gambar PNG/JPG yang ingin Anda proses.

---

## Langkah 1: Terapkan Lisensi Aspose OCR (Wajib untuk Produksi)

Sebelum Anda dapat memanggil API OCR apa pun, Anda harus memuat lisensi yang valid; jika tidak, Anda akan terbatasi oleh batasan trial.

```java
import com.aspose.ocr.*;

public class LicenseSetup {
    public static void loadLicense() throws Exception {
        License license = new License();
        // Point to your license file – keep it out of source control!
        license.setLicense("Aspose.OCR.Java.lic");
    }
}
```

*Mengapa ini penting*: Mesin berlisensi membuka dukungan GPU, akurasi lebih tinggi, dan menghilangkan watermark yang biasanya membuat file PDF Anda menjadi lebih besar.

---

## Langkah 2: Konfigurasikan Mesin OCR – Thread, GPU, dan Koreksi Ejaan

Mesin OCR yang cepat adalah tulang punggung setiap pekerjaan **batch OCR ke PDF**. Kami akan memanfaatkan sebanyak mungkin thread yang dapat ditangani CPU host, mengaktifkan akselerasi GPU (jika Anda memiliki kartu yang kompatibel), dan memperketat koreksi ejaan untuk membersihkan kesalahan OCR.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.gpu.GPUSettings;
import com.aspose.ocr.spell.SpellCorrectionOptions;

public class EngineConfig {
    public static OcrEngine createEngine() {
        OcrEngine ocrEngine = new OcrEngine();

        // Use all available logical processors
        ocrEngine.setThreadCount(Runtime.getRuntime().availableProcessors());

        // Enable GPU – huge speedup for large batches
        GPUSettings gpu = new GPUSettings();
        gpu.setEnabled(true);
        ocrEngine.setGpuSettings(gpu);

        // Light spell correction: fix common typos without over‑correcting
        SpellCorrectionOptions spellOpts = new SpellCorrectionOptions();
        spellOpts.setMaxEditDistance(1);
        ocrEngine.getSpellCorrection().setOptions(spellOpts);

        return ocrEngine;
    }
}
```

*Tips pro*: Jika Anda menjalankan di server headless tanpa GPU, cukup setel `gpu.setEnabled(false)` – kode tetap akan berfungsi, hanya sedikit lebih lambat.

---

## Langkah 3: Bangun Pipeline Praproses Gambar

Pemindaian mentah sering kali mengandung noise, kontras rendah, atau pencahayaan tidak merata. **Praproses gambar untuk OCR** secara dramatis meningkatkan tingkat pengenalan, terutama untuk skenario **mengenali teks JPG**.

```java
import com.aspose.ocr.*;

public class PreprocessorSetup {
    public static ImagePreprocessor createPreprocessor() {
        return new ImagePreprocessor.Builder()
                .addDenoise(0.7)      // Reduce grain while preserving edges
                .addContrast(1.15)    // Boost contrast for clearer glyphs
                .addBinarize()        // Convert to black‑and‑white for OCR
                .build();
    }
}
```

*Mengapa kami menumpuk langkah ini*: Denoising pertama mencegah binarisasi memperkuat bintik‑bintik; kontras kemudian memastikan karakter menonjol; akhirnya, binarisasi memberikan mesin OCR gambar biner yang bersih untuk diproses.

---

## Langkah 4: Siapkan Opsi Penyimpanan PDF – **Kompres Gambar PDF** Secara Efisien

Aspose memungkinkan Anda menyesuaikan output PDF. Kami akan mengaktifkan kompresi gambar dan menetapkan tingkat kualitas yang menyeimbangkan ukuran dan keterbacaan.

```java
import com.aspose.ocr.pdf.PdfSaveOptions;

public class PdfOptions {
    public static PdfSaveOptions createOptions() {
        PdfSaveOptions options = new PdfSaveOptions();
        options.setCompressImages(true);   // This is the key to compress PDF images
        options.setImageQuality(90);       // 90% retains sharp text while shrinking file size
        return options;
    }
}
```

*Hasil*: Setiap PDF yang dapat dicari akan jauh lebih kecil—ideal untuk arsip atau pengiriman melalui email.

---

## Langkah 5: Proses Folder – **Konversi PNG ke PDF** dan **Mengenali Teks JPG** dalam Satu Loop

Sekarang semua komponen digabungkan. Loop ini menelusuri direktori input, menjalankan OCR pada setiap PNG atau JPG, dan menulis PDF yang dapat dicari ke folder output. Nama PDF meniru nama gambar sumber.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.pdf.PdfSaveOptions;
import java.io.File;

public class BatchOcrTutorial {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load license
        LicenseSetup.loadLicense();

        // 2️⃣ Engine & preprocessing
        OcrEngine ocrEngine = EngineConfig.createEngine();
        ocrEngine.setPreprocessor(PreprocessorSetup.createPreprocessor());

        // 3️⃣ PDF options (compress PDF images)
        PdfSaveOptions pdfOptions = PdfOptions.createOptions();

        // 4️⃣ Define input / output folders
        File inputFolder = new File("YOUR_DIRECTORY/input");
        File outputFolder = new File("YOUR_DIRECTORY/output");
        if (!outputFolder.exists()) outputFolder.mkdirs();

        // 5️⃣ Filter PNG & JPG files
        File[] imageFiles = inputFolder.listFiles((dir, name) ->
                name.toLowerCase().endsWith(".png") || name.toLowerCase().endsWith(".jpg"));

        if (imageFiles == null || imageFiles.length == 0) {
            System.out.println("No PNG or JPG files found in the input folder.");
            return;
        }

        // 6️⃣ Process each file
        for (File image : imageFiles) {
            // Recognize text – works for both PNG and JPG
            ocrEngine.recognizeImage(image.getAbsolutePath());

            // Build output PDF path (same base name)
            String pdfPath = outputFolder.getAbsolutePath() + File.separator +
                    image.getName().replaceAll("\\.(png|jpg)$", ".pdf");

            // Save as searchable PDF – this step also compresses images
            ocrEngine.saveAsSearchablePdf(pdfPath, pdfOptions);

            System.out.println("✅ Processed: " + image.getName() + " → " + pdfPath);
        }

        System.out.println("🎉 All files have been converted and compressed!");
    }
}
```

### Output yang Diharapkan

Menjalankan program akan mencetak satu baris untuk setiap gambar, misalnya:

```
✅ Processed: invoice1.png → /output/invoice1.pdf
✅ Processed: receipt23.jpg → /output/receipt23.pdf
🎉 All files have been converted and compressed!
```

Buka PDF hasil di penampil apa pun dan Anda akan melihat teks yang dapat dipilih serta dapat dicari, sementara ukuran file biasanya **30‑50 % lebih kecil** dibandingkan dengan versi yang tidak dikompres.

---

## Pertanyaan Umum & Kasus Tepi

### Bagaimana jika server saya tidak memiliki GPU?
Cukup setel `gpuSettings.setEnabled(false)`. Sisa pipeline tetap tidak berubah, dan Anda masih mendapatkan pemrosesan multithreaded di CPU.

### PDF saya masih terlalu besar—apakah saya bisa menurunkan kualitas lebih jauh?
Ya. Sesuaikan `options.setImageQuality(70)` atau bahkan `50`. Nilai yang lebih rendah memangkas ukuran lebih agresif tetapi dapat membuat glyph halus menjadi kabur. Uji dengan sampel representatif.

### Bagaimana cara menangani format gambar lain (TIFF, BMP)?
Tambahkan ekstensi tersebut ke lambda filter:

```java
name.toLowerCase().endsWith(".png") ||
name.toLowerCase().endsWith(".jpg") ||
name.toLowerCase().endsWith(".tif") ||
name.toLowerCase().endsWith(".bmp")
```

Pipeline praproses yang sama bekerja untuk kebanyakan format raster.

### Bisakah saya mempertahankan gambar berwarna asli alih‑alih binarisasi?
Ganti `.addBinarize()` dengan `.addGrayscale()` pada builder praprosesor jika Anda memerlukan retensi warna untuk analisis selanjutnya.

---

## Tips Pro untuk Batch OCR Siap Produksi

- **Manajemen memori**: Gunakan satu instance `OcrEngine` (seperti yang ditunjukkan) untuk menghindari overhead pembuatan/penghancuran objek per gambar.
- **Penanganan error**: Bungkus blok per‑file dengan `try/catch` untuk mencatat kegagalan tanpa menghentikan seluruh batch.
- **Logging**: Pakai kerangka logging yang tepat (SLF4J, Log4j) alih‑alih `System.out.println` untuk solusi yang dapat diskalakan.
- **Paralelisme**: Untuk folder yang sangat besar, pertimbangkan memproses sub‑direktori dengan parallel streams, namun perhatikan kontensi GPU.
- **Keamanan**: Simpan file lisensi di luar repositori dan lindungi dengan izin sistem file.

---

## Kesimpulan

Kami baru saja menunjukkan cara **mengompres gambar PDF** sambil melakukan konversi **batch OCR ke PDF** yang **mengonversi PNG ke PDF**, **mengenali teks JPG**, dan menerapkan pipeline **praproses gambar untuk OCR** yang kuat. Program Java lengkap bersifat mandiri, dapat dijalankan pada JDK modern apa pun, dan menghasilkan PDF yang dapat dicari serta ringan, siap untuk arsip atau analisis lanjutan.

Langkah selanjutnya? Bereksperimen dengan parameter praproses yang berbeda, coba bahasa OCR selain bahasa Inggris, atau integrasikan alur kerja ke dalam microservice Spring Boot yang memantau direktori dan memproses file secara real‑time. Konsep inti—pemuatan lisensi, konfigurasi mesin, praproses, dan kompresi PDF—tetap sama, memberi Anda fondasi yang solid untuk proyek berbasis OCR apa pun.

Punya pertanyaan atau ingin berbagi modifikasi? Tinggalkan komentar di bawah, dan selamat coding!

![Diagram of batch OCR workflow showing input images, preprocessing, OCR engine, and compressed PDF output](alt="Diagram of batch OCR workflow showing input images, preprocessing, OCR engine, and compressed PDF output")

## Apa yang Harus Anda Pelajari Selanjutnya?


Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Recognize PDF Text – OCR Operations with Aspose.OCR for Java](/ocr/english/java/ocr-operations/)
- [recognize text image with Aspose OCR – Full Java OCR Tutorial](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Convert Image to Text in Java using Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}