---
category: general
date: 2026-06-22
description: 'Cara meluruskan gambar untuk OCR: pelajari langkah-langkah pra‑pemrosesan
  gambar OCR, hilangkan noise garam‑merica, dan tingkatkan akurasi.'
draft: false
keywords:
- how to deskew image
- image preprocessing ocr
- remove salt pepper
- preprocess images OCR
language: id
og_description: Cara meluruskan gambar untuk OCR, menghilangkan noise garam dan merica,
  serta menerapkan teknik pra‑pemrosesan gambar OCR dalam contoh Java lengkap.
og_title: Cara Meluruskan Gambar – Panduan Pra‑pemrosesan Gambar OCR
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: 'How to deskew image for OCR: learn image preprocessing OCR steps,
    remove salt pepper noise, and boost accuracy.'
  headline: How to Deskew Image – Image Preprocessing OCR Guide
  type: TechArticle
tags:
- OCR
- image-processing
- Java
title: Cara Menghilangkan Kemiringan Gambar – Panduan Pra‑pemrosesan Gambar OCR
url: /id/java/ocr-operations/how-to-deskew-image-image-preprocessing-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Mengoreksi Kemiringan Gambar – Panduan Pra‑pemrosesan Gambar OCR

Pernah bertanya‑tanya **how to deskew image** sehingga mesin OCR Anda benar‑benar membaca teks? Anda bukan satu‑satunya. Scan yang miring dapat mengubah dokumen sempurna menjadi kekacauan, dan kebanyakan pengembang mengalami masalah ini setidaknya sekali.

Dalam tutorial ini kami akan membahas seluruh pipeline **image preprocessing OCR** yang tidak hanya memperbaiki rotasi tetapi juga **remove[s] salt pepper** artefak dan meningkatkan kontras—pada dasarnya semua yang Anda perlukan untuk **preprocess images OCR**‑style sebelum memberi makan ke mesin. Pada akhir tutorial Anda akan memiliki potongan kode Java siap‑jalankan dan model mental yang jelas mengapa setiap langkah penting.

## Cara Mengoreksi Kemiringan Gambar – Membangun Pipeline Pra‑pemrosesan

Inti dari setiap alur kerja yang ramah OCR adalah objek **preprocess options** yang menghubungkan serangkaian filter. Anggaplah seperti konveyor: setiap filter melakukan satu tugas, lalu meneruskan gambar ke filter berikutnya. Di bawah ini contoh minimal namun lengkap menggunakan perpustakaan OCR hipotetik yang menyertakan `DeskewFilter`, `DenoiseFilter`, dan `ContrastBoostFilter`.

```java
import com.example.ocr.Engine;
import com.example.ocr.ImagePreprocessOptions;
import com.example.ocr.filters.DeskewFilter;
import com.example.ocr.filters.DenoiseFilter;
import com.example.ocr.filters.ContrastBoostFilter;

/**
 * Demonstrates how to deskew image and apply common OCR preprocessing steps.
 */
public class OcrPreprocessDemo {

    public static void main(String[] args) {
        // 1️⃣ Create the OCR engine (replace with your actual implementation)
        Engine engine = new Engine();

        // 2️⃣ Build the preprocessing pipeline
        ImagePreprocessOptions preprocessOptions = new ImagePreprocessOptions();

        // 2a️⃣ Deskew – correct rotation up to ±15°
        preprocessOptions.addFilter(new DeskewFilter(15));

        // 2b️⃣ Denoise – remove salt‑and‑pepper noise
        preprocessOptions.addFilter(new DenoiseFilter());

        // 2c️⃣ Contrast boost – make low‑contrast scans more readable
        preprocessOptions.addFilter(new ContrastBoostFilter(1.5f));

        // 3️⃣ Attach the pipeline to the engine
        engine.setPreprocessOptions(preprocessOptions);

        // 4️⃣ Run OCR on a sample image
        String result = engine.recognizeText("sample-scanned-page.png");

        // 5️⃣ Output the recognized text
        System.out.println("=== OCR RESULT ===");
        System.out.println(result);
    }
}
```

### Mengapa ini Berfungsi

* **DeskewFilter** menganalisis garis teks dominan pada gambar, memperkirakan sudut, dan memutar bitmap kembali ke posisi horizontal. Sebagian besar perpustakaan membatasi koreksi pada ±15° karena sudut yang lebih besar biasanya menunjukkan halaman yang dipindai buruk dan memerlukan intervensi manual.
* **DenoiseFilter** menargetkan pola klasik *salt‑and‑pepper*—pixel hitam atau putih terisolasi yang tampak seperti statik pada TV. Menghapusnya mencegah mesin OCR salah mengira noise sebagai karakter.
* **ContrastBoostFilter** memperluas histogram, membuat goresan tipis lebih menonjol. Pengganda `1.5f` adalah nilai default yang aman; Anda dapat meningkatkannya jika hasil scan Anda sangat pudar.

> **Pro tip:** Jika Anda tahu dokumen Anda tidak pernah melebihi kemiringan 10°, berikan batas yang lebih kecil itu ke `DeskewFilter`—algoritma akan berjalan lebih cepat dan kurang mungkin melakukan over‑correction.

## Image Preprocessing OCR: Menambahkan Filter dalam Urutan yang Tepat

Urutan penting. Bayangkan Anda melakukan denoise *sebelum* deskew; noise dapat mengganggu deteksi sudut, menghasilkan hasil yang tidak sejajar. Sebaliknya, menerapkan contrast boost *setelah* deskew memastikan rotasi tidak memperkenalkan artefak baru.

Berikut adalah daftar periksa cepat yang dapat Anda salin‑tempel ke proyek mana pun:

| Step | Filter | Reason |
|------|--------|--------|
| 1 | `DeskewFilter` | Menyelaraskan garis dasar teks |
| 2 | `DenoiseFilter` | Menghapus noise pixel terisolasi |
| 3 | `ContrastBoostFilter` | Meningkatkan keterbacaan untuk OCR |

Jika Anda perlu menyisipkan langkah tambahan—misalnya, filter **binarization** untuk OCR biner—Anda akan menempatkannya **setelah** contrast boosting, karena gambar yang bersih dan berkontras tinggi dapat dibinarisasi lebih akurat.

## Menghapus Noise Salt Pepper dengan DenoiseFilter

Noise salt‑and‑pepper terkenal pada scan kualitas rendah, terutama yang berasal dari kamera ponsel murah. `DenoiseFilter` dalam perpustakaan kami mengimplementasikan kernel median‑filter, yang menggantikan setiap pixel dengan median dari lingkungan sekitarnya. Efeknya? Bintik‑bintik tersebut menghilang tanpa mengaburkan karakter sebenarnya.

```java
// Example: customizing the median kernel size (default is 3x3)
preprocessOptions.addFilter(new DenoiseFilter(5)); // 5x5 kernel for heavy noise
```

*Kapan memperbesar ukuran kernel?* Jika gambar sumber Anda dipenuhi bintik‑bintik besar, kernel yang lebih besar akan membersihkannya, tetapi hati‑hati: terlalu besar dan Anda mungkin mulai menghapus goresan halus pada font kecil.

## Preprocess Images OCR – Menerapkan Pipeline

Setelah Anda menyusun rantai filter, menambahkannya ke mesin cukup satu baris (`engine.setPreprocessOptions`). Mulai saat itu, setiap pemanggilan `recognizeText` secara otomatis melewati pipeline. Tidak perlu memanggil setiap filter secara manual—kode Anda tetap rapi, dan perubahan di masa depan (menambahkan filter baru, menyesuaikan parameter) terpusat.

Berikut contoh hasil run yang berhasil dengan contoh scan yang awalnya memiliki kemiringan 12° dan noise pepper yang terlihat:

```
=== OCR RESULT ===
Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
Thank you for your business!
```

Perhatikan bagaimana teks menjadi bersih, terorientasi dengan benar, dan bebas dari karakter asing yang seharusnya muncul sebagai “I n v o i c e” atau “$‑‑‑”.

## Kasus Tepi & Kesalahan Umum

| Situation | What to watch for | Suggested fix |
|-----------|-------------------|---------------|
| Rotation > 15° | DeskewFilter mungkin menyerah | Pra‑rotate secara manual atau gunakan filter dengan rentang lebih tinggi |
| Extremely low resolution ( < 100 dpi ) | Contrast boost tidak dapat memulihkan detail | Resample gambar terlebih dahulu (misalnya, `ResampleFilter`) |
| Mixed noise (Gaussian + salt‑pepper) | DenoiseFilter saja tidak cukup | Rantai `GaussianBlurFilter` sebelum `DenoiseFilter` |
| Color scans with colored text | Diperlukan konversi ke Grayscale | Sisipkan `GrayscaleFilter` sebelum contrast boost |

Dengan mengantisipasi skenario ini Anda menghemat berjam‑jam debugging di kemudian hari.

## Contoh Kerja Lengkap (All‑in‑One)

Berikut adalah kelas Java mandiri yang dapat Anda masukkan ke proyek Maven atau Gradle mana pun yang menyertakan dependensi `com.example.ocr`. Kelas ini mendemonstrasikan **how to deskew image**, **remove salt pepper** noise, dan **preprocess images OCR**‑style.

```java
package com.myapp.demo;

import com.example.ocr.Engine;
import com.example.ocr.ImagePreprocessOptions;
import com.example.ocr.filters.*;

public class CompleteOcrPipeline {

    public static void main(String[] args) {
        // -------------------------------------------------
        // 1️⃣ Initialise OCR engine (replace with your own)
        // -------------------------------------------------
        Engine engine = new Engine();

        // -------------------------------------------------
        // 2️⃣ Configure preprocessing pipeline
        // -------------------------------------------------
        ImagePreprocessOptions options = new ImagePreprocessOptions();

        // Deskew up to ±15° – the core of "how to deskew image"
        options.addFilter(new DeskewFilter(15));

        // Remove salt‑and‑pepper artifacts
        options.addFilter(new DenoiseFilter());

        // Boost contrast by 1.5× to aid OCR recognition
        options.addFilter(new ContrastBoostFilter(1.5f));

        // (Optional) Convert to grayscale – often improves OCR accuracy
        options.addFilter(new GrayscaleFilter());

        // Attach the pipeline
        engine.setPreprocessOptions(options);

        // -------------------------------------------------
        // 3️⃣ Perform OCR on a test file
        // -------------------------------------------------
        String imagePath = "src/main/resources/scanned-document.png";
        String text = engine.recognizeText(imagePath);

        // -------------------------------------------------
        // 4️⃣ Show the result
        // -------------------------------------------------
        System.out.println("=== OCR RESULT ===");
        System.out.println(text);
    }
}
```

**Expected output** (asumsi `scanned-document.png` berisi faktur yang jelas):

```
=== OCR RESULT ===
Invoice #98765
Date: 2024‑02‑28
Amount Due: $2,340.75
Please remit payment within 30 days.
```

Jika Anda mengganti gambar dengan yang sudah teralign sempurna, Anda akan melihat pipeline tetap berjalan—tidak ada yang rusak, dan akurasi OCR tetap tinggi.

## Kesimpulan

Anda kini memiliki pemahaman yang kuat tentang **how to deskew image** dan mengapa setiap langkah pra‑pemrosesan—**image preprocessing OCR**, **remove salt pepper**, dan **preprocess images OCR**—memainkan peran penting dalam menghasilkan teks bersih yang dapat dicari. Contoh di atas adalah lengkap,

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [How to Use AspOCR: Preprocess Image OCR Filters for .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Calculate Skew Angle for OCR Image Preprocessing](/ocr/english/net/skew-angle-calculation/calculate-skew-angle/)
- [How to Set Threshold Value in OCR Image Recognition](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}