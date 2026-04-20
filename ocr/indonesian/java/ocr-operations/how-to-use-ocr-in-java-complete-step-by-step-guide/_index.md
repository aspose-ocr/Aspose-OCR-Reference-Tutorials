---
category: general
date: 2026-02-22
description: Cara menggunakan OCR di Java untuk mengekstrak teks dari gambar, meningkatkan
  akurasi OCR, dan memuat gambar untuk OCR dengan contoh kode praktis.
draft: false
keywords:
- how to use OCR
- extract text from image
- improve OCR accuracy
- load image for OCR
- OCR preprocessing
language: id
og_description: Cara menggunakan OCR di Java untuk mengekstrak teks dari gambar dan
  meningkatkan akurasi OCR. Ikuti panduan ini untuk contoh yang siap dijalankan.
og_title: Cara Menggunakan OCR di Java – Panduan Lengkap Langkah demi Langkah
tags:
- OCR
- Java
- Image Processing
title: Cara Menggunakan OCR di Java – Panduan Lengkap Langkah demi Langkah
url: /id/java/ocr-operations/how-to-use-ocr-in-java-complete-step-by-step-guide/
---

with all translations.

Check for any missed items: The "step‑by‑step" hyphen; keep same.

Make sure to keep the code block placeholders exactly as they are.

Now produce final answer.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menggunakan OCR di Java – Panduan Lengkap Langkah‑per‑Langkah

Pernahkah Anda perlu **how to use OCR** pada screenshot yang miring dan bertanya-tanya mengapa outputnya terlihat seperti omong kosong? Anda bukan satu-satunya. Dalam banyak aplikasi dunia nyata—memindai struk, mendigitalkan formulir, atau mengambil teks dari meme—mendapatkan hasil yang dapat diandalkan bergantung pada beberapa pengaturan sederhana.

Dalam tutorial ini kami akan menjelaskan **how to use OCR** untuk *extract text from image* file, menunjukkan cara **improve OCR accuracy**, dan mendemonstrasikan cara yang benar untuk **load image for OCR** menggunakan pustaka OCR Java yang populer. Pada akhir tutorial Anda akan memiliki program mandiri yang dapat Anda masukkan ke dalam proyek apa pun.

## Apa yang Akan Anda Pelajari

- Kode tepat yang Anda butuhkan untuk **load image for OCR** (tanpa dependensi tersembunyi).
- Flag preprocessing mana yang meningkatkan **improve OCR accuracy** dan mengapa mereka penting.
- Cara membaca hasil OCR dan mencetaknya ke konsol.
- Jebakan umum—seperti lupa mengatur region of interest atau mengabaikan noise reduction—dan cara menghindarinya.

### Prasyarat

- Java 17 atau lebih baru (kode ini dapat dikompilasi dengan JDK terbaru apa pun).
- Sebuah pustaka OCR yang menyediakan kelas `OcrEngine`, `ImagePreprocessingOptions`, `OcrInput`, dan `OcrResult` (misalnya paket fiktif `com.example.ocr` yang digunakan dalam potongan kode). Ganti dengan pustaka nyata yang Anda gunakan.
- Sebuah gambar contoh (`skewed_noisy.png`) yang ditempatkan di folder yang dapat Anda referensikan.

> **Pro tip:** Jika Anda menggunakan SDK komersial, pastikan file lisensi berada di classpath Anda; jika tidak, engine akan melempar error inisialisasi.

---

## Langkah 1: Buat Instance OCR Engine – **how to use OCR** secara efektif

Hal pertama yang Anda butuhkan adalah objek `OcrEngine`. Anggaplah itu sebagai otak yang akan menafsirkan piksel.

```java
// Step 1: Initialize the OCR engine
import com.example.ocr.OcrEngine;

OcrEngine ocrEngine = new OcrEngine();
```

*Mengapa ini penting:* Tanpa engine Anda tidak memiliki konteks untuk model bahasa, set karakter, atau heuristik gambar. Membuatnya lebih awal juga memungkinkan Anda menambahkan opsi preprocessing nanti.

---

## Langkah 2: Konfigurasikan Image Preprocessing – **improve OCR accuracy**

Preprocessing adalah bumbu rahasia yang mengubah pemindaian berisik menjadi teks bersih yang dapat dibaca mesin. Di bawah ini kami mengaktifkan deskew, noise reduction tingkat tinggi, auto‑contrast, dan region of interest (ROI) untuk memfokuskan pada bagian gambar yang relevan.

```java
import com.example.ocr.ImagePreprocessingOptions;
import java.awt.Rectangle;

// Step 2: Set up preprocessing to improve OCR accuracy
ImagePreprocessingOptions preprocessing = new ImagePreprocessingOptions();
preprocessing.setDeskewEnabled(true); // Correct image rotation
preprocessing.setNoiseReductionLevel(
        ImagePreprocessingOptions.NoiseReduction.HIGH); // Reduce speckles
preprocessing.setAutoContrastEnabled(true); // Boost contrast
preprocessing.setRegionOfInterest(new Rectangle(100, 200, 800, 600)); // Process a sub‑region only

ocrEngine.setPreprocessingOptions(preprocessing);
```

*Mengapa ini penting:*  
- **Deskew** menyelaraskan teks yang diputar, yang penting saat memindai struk yang tidak sepenuhnya rata.  
- **Noise reduction** menghapus piksel stray yang sebaliknya akan diinterpretasikan sebagai karakter.  
- **Auto‑contrast** memperluas rentang tonal, membuat huruf yang pudar lebih menonjol.  
- **ROI** memberi tahu engine untuk mengabaikan tepi yang tidak relevan, menghemat waktu dan memori.

Jika Anda melewatkan salah satu dari ini, kemungkinan besar Anda akan melihat penurunan hasil **improve OCR accuracy**.

---

## Langkah 3: Muat Gambar untuk OCR – **load image for OCR** dengan benar

Sekarang kami benar‑benarnya mengarahkan engine ke file yang ingin dibaca. Kelas `OcrInput` dapat menerima beberapa gambar, tetapi untuk contoh ini kami menyederhanakannya.

```java
import com.example.ocr.OcrInput;

// Step 3: Load the image you want to extract text from
OcrInput ocrInput = new OcrInput();
ocrInput.add("YOUR_DIRECTORY/skewed_noisy.png"); // replace with your real path
```

*Mengapa ini penting:* Path harus absolut atau relatif terhadap direktori kerja; jika tidak, engine akan melempar `FileNotFoundException`. Juga, perhatikan bahwa nama metode `add` menunjukkan Anda dapat mengantri beberapa gambar—berguna untuk pemrosesan batch.

---

## Langkah 4: Lakukan OCR dan Keluarkan Teks yang Diakui – **how to use OCR** end‑to‑end

Akhirnya, kami meminta engine untuk mengenali teks dan mencetaknya. Objek `OcrResult` berisi string mentah, skor kepercayaan, dan metadata baris‑per‑baris (jika Anda membutuhkannya nanti).

```java
import com.example.ocr.OcrResult;

// Step 4: Run OCR and print the extracted text
OcrResult ocrResult = ocrEngine.recognize(ocrInput);
System.out.println("=== OCR Output ===");
System.out.println(ocrResult.getText());
```

**Output yang diharapkan** (asumsi gambar contoh berisi “Hello, OCR World!”):

```
=== OCR Output ===
Hello, OCR World!
```

Jika hasilnya terlihat berantakan, kembali ke Langkah 2 dan sesuaikan opsi preprocessing—mungkin turunkan level noise reduction atau ubah persegi ROI.

---

## Contoh Lengkap yang Dapat Dijalankan

Berikut adalah program Java lengkap yang dapat Anda salin‑tempel ke dalam file bernama `OcrDemo.java`. Program ini menggabungkan semua langkah yang telah dibahas.

```java
// OcrDemo.java – A complete, runnable example showing how to use OCR in Java
import com.example.ocr.OcrEngine;
import com.example.ocr.ImagePreprocessingOptions;
import com.example.ocr.OcrInput;
import com.example.ocr.OcrResult;
import java.awt.Rectangle;

public class OcrDemo {
    public static void main(String[] args) {
        // 1️⃣ Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Configure preprocessing (this is the key to improve OCR accuracy)
        ImagePreprocessingOptions preprocessing = new ImagePreprocessingOptions();
        preprocessing.setDeskewEnabled(true);
        preprocessing.setNoiseReductionLevel(
                ImagePreprocessingOptions.NoiseReduction.HIGH);
        preprocessing.setAutoContrastEnabled(true);
        preprocessing.setRegionOfInterest(new Rectangle(100, 200, 800, 600));
        ocrEngine.setPreprocessingOptions(preprocessing);

        // 3️⃣ Load the image you want to extract text from
        OcrInput ocrInput = new OcrInput();
        // 👉 Replace the path with your own image location
        ocrInput.add("YOUR_DIRECTORY/skewed_noisy.png");

        // 4️⃣ Run the OCR engine and print the result
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);
        System.out.println("=== OCR Output ===");
        System.out.println(ocrResult.getText());
    }
}
```

Simpan file, kompilasi dengan `javac OcrDemo.java`, dan jalankan `java OcrDemo`. Jika semuanya telah disiapkan dengan benar, Anda akan melihat teks yang diekstrak dicetak ke konsol.

---

## Pertanyaan Umum & Kasus Tepi

| Question | Answer |
|----------|--------|
| **Bagaimana jika gambar saya berformat JPEG?** | Metode `OcrInput.add()` menerima format raster yang didukung apa pun—PNG, JPEG, BMP, TIFF. Cukup ubah ekstensi file pada path. |
| **Bisakah saya memproses beberapa halaman sekaligus?** | Tentu saja. Panggil `ocrInput.add()` untuk setiap file, lalu berikan `ocrInput` yang sama ke `recognize()`. Engine akan mengembalikan `OcrResult` yang digabungkan. |
| **Bagaimana jika hasil OCR kosong?** | Periksa kembali bahwa ROI memang berisi teks. Juga pastikan `setDeskewEnabled(true)` aktif; rotasi 90° akan membuat engine mengira gambar kosong. |
| **Bagaimana cara mengubah model bahasa?** | Sebagian besar pustaka menyediakan metode `setLanguage(String)` pada `OcrEngine`. Panggil sebelum `recognize()`, misalnya `ocrEngine.setLanguage("eng")`. |
| **Apakah ada cara untuk mendapatkan skor kepercayaan?** | Ya, `OcrResult` biasanya menyediakan `getConfidence()` per baris atau per karakter. Gunakan untuk menyaring hasil dengan kepercayaan rendah. |

---

## Kesimpulan

Kami telah membahas **how to use OCR** di Java dari awal hingga akhir: membuat engine, mengonfigurasi preprocessing untuk **improve OCR accuracy**, **load image for OCR** dengan benar, dan akhirnya mencetak teks yang diekstrak. Potongan kode lengkap siap dijalankan, dan penjelasannya menjawab “mengapa” di balik setiap baris.

Siap untuk langkah selanjutnya? Coba ganti persegi ROI untuk memfokuskan pada bagian gambar yang berbeda, bereksperimen dengan `NoiseReduction.MEDIUM`, atau integrasikan output ke PDF yang dapat dicari. Anda juga dapat menjelajahi topik terkait seperti **extract text from image** menggunakan layanan cloud, atau memproses ribuan file secara batch dengan antrian multithread.

Ada pertanyaan lebih lanjut tentang OCR, preprocessing gambar, atau integrasi Java? Tinggalkan komentar, dan selamat coding! 

![How to use OCR example](/images/ocr-demo.png "how to use OCR – Java example showing preprocessing and result")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}