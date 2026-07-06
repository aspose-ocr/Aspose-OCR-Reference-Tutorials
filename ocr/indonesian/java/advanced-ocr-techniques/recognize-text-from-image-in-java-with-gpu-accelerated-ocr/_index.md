---
category: general
date: 2026-06-19
description: Mengenali teks dari gambar menggunakan tutorial OCR Java – temukan OCR
  yang dipercepat GPU dan dengan cepat mengekstrak teks dari file PNG.
draft: false
keywords:
- recognize text from image
- extract text from png
- how to recognize text
- gpu accelerated ocr
- java ocr tutorial
language: id
og_description: Mengenali teks dari gambar di Java dengan percepatan GPU. Tutorial
  ini menunjukkan cara mengekstrak teks dari PNG menggunakan Aspose OCR.
og_title: Mengenali teks dari gambar di Java – Panduan OCR yang Dipercepat GPU
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: recognize text from image using a Java OCR tutorial – discover GPU
    accelerated OCR and quickly extract text from png files.
  headline: recognize text from image in Java with GPU‑accelerated OCR
  type: TechArticle
- description: recognize text from image using a Java OCR tutorial – discover GPU
    accelerated OCR and quickly extract text from png files.
  name: recognize text from image in Java with GPU‑accelerated OCR
  steps:
  - name: 1. *What if my image is a JPEG or TIFF?*
    text: The same `recognizeImage` call works for JPEG, BMP, TIFF, and even PDF.
      No code change needed—just pass the correct file path.
  - name: 2. *Can I process multiple images in a loop?*
    text: Absolutely. Create the `OcrEngine` once, then call `recognizeImage` repeatedly.
      Re‑using the engine saves memory and keeps the GPU context alive.
  - name: 3. *My GPU isn’t detected—what gives?*
    text: Make sure you have a recent graphics driver installed. Aspose OCR supports
      CUDA 11+ and OpenCL 2.0+. If the driver is missing, the engine automatically
      falls back to CPU, which is slower but still functional.
  - name: 4. *How do I improve accuracy on noisy scans?*
    text: 'Pre‑process the image: increase contrast, apply binarization, or use the
      `PreprocessOptions` class that Aspose provides. Example:'
  - name: 5. *Is there a way to get bounding boxes for each word?*
    text: Yes—`OcrResult` contains a collection of `OcrRegion` objects. Iterate over
      them to retrieve coordinates, useful for highlighting text in UI.
  type: HowTo
tags:
- OCR
- Java
- GPU
title: Mengenali teks dari gambar di Java dengan OCR yang dipercepat GPU
url: /id/java/advanced-ocr-techniques/recognize-text-from-image-in-java-with-gpu-accelerated-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# mengenali teks dari gambar di Java dengan GPU‑accelerated OCR

Pernah bertanya-tanya bagaimana cara **recognize text from image** file tanpa menulis ribuan baris kode? Anda bukan satu-satunya—para pengembang terus bertanya, *“bagaimana cara mengenali teks* dalam gambar secara efisien?” Kabar baiknya, Aspose OCR memberikan Anda mesin siap pakai yang bahkan dapat memanfaatkan GPU Anda, mengubah pekerjaan CPU yang lambat menjadi operasi super cepat.  

Dalam **java ocr tutorial** ini kami akan membahas setiap langkah, mulai dari lisensi hingga mencetak string akhir, dan kami juga akan menunjukkan cara **extract text from png** file dengan hanya beberapa baris. Pada akhir Anda akan memiliki program yang dapat dijalankan yang mendemonstrasikan **gpu accelerated ocr** dalam aksi, plus beberapa tip yang dapat Anda terapkan pada format gambar lainnya.

## Apa yang Anda Butuhkan

- Java 17 (atau JDK terbaru) terinstal dan `JAVA_HOME` sudah diset.
- File lisensi Aspose OCR untuk Java (`Aspose.OCR.lic`). Versi percobaan gratis berfungsi, tetapi lisensi yang tepat menghapus watermark evaluasi.
- Gambar PNG resolusi tinggi yang ingin Anda uji, misalnya `sample-highres.png`.
- Maven atau Gradle untuk mengambil dependensi Aspose OCR (kami akan menunjukkan cuplikan Maven).

Itu saja—tidak ada pustaka native tambahan, tidak ada pengaturan toolkit CUDA. SDK secara otomatis mendeteksi GPU dan melakukan pekerjaan berat untuk Anda.

## Langkah 1: Tambahkan Aspose OCR ke Proyek Anda

Jika Anda menggunakan Maven, tambahkan ini ke `pom.xml` Anda:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version>
</dependency>
```

Pengguna Gradle dapat menambahkan:

```groovy
implementation 'com.aspose:aspose-ocr:23.10'
```

> **Pro tip:** Jaga nomor versi tetap terbaru; rilis yang lebih baru meningkatkan deteksi GPU dan menambahkan paket bahasa.

## Langkah 2: Terapkan Lisensi Aspose OCR

Lisensi adalah hal pertama yang diperiksa SDK, jadi lakukan di awal `main`. Jika Anda melewatkan langkah ini, mesin akan berjalan dalam mode evaluasi dan menambahkan watermark pada output.

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {
        // Apply your Aspose OCR license
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");
```

Perhatikan betapa kecilnya kode—hanya dua baris, namun membuka seluruh set fitur, termasuk **gpu accelerated ocr**.

## Langkah 3: Aktifkan Akselerasi GPU

Objek `Device` di dalam `OcrEngine` mengetahui apakah GPU yang kompatibel tersedia. Mengatur `useGpu` ke `true` memberi tahu mesin untuk secara otomatis mendeteksi perangkat terbaik (CUDA, OpenCL, atau kembali ke CPU).

```java
        // Create the OCR engine and turn on GPU support
        OcrEngine engine = new OcrEngine();
        engine.getDevice().setUseGpu(true);
```

Jika mesin Anda tidak memiliki GPU, pemanggilan ini tidak berbahaya—mesin hanya tetap menggunakan CPU. Ini membuat potongan kode dapat dipindahkan antara laptop dan server.

## Langkah 4: Pilih Bahasa Pengakuan

Anda dapat memilih bahasa apa pun yang didukung oleh Aspose OCR. Untuk sebagian besar demo Bahasa Inggris sudah cukup, tetapi API memudahkan beralih ke Prancis, Jerman, atau bahkan Mandarin.

```java
        // Set the language (English in this example)
        engine.setLanguage(Language.English);
```

> **Mengapa bahasa penting?** Model OCR dilatih per bahasa; memilih yang tepat meningkatkan akurasi, terutama pada karakter dengan diakritik.

## Langkah 5: Kenali Teks dari Gambar

Sekarang kita sampai pada inti masalah—**recognize text from image**. Metode `recognizeImage` menerima jalur file (atau `InputStream`) dan mengembalikan `OcrResult` yang berisi string mentah.

```java
        // Recognize text from a PNG file
        OcrResult result = engine.recognizeImage("YOUR_DIRECTORY/sample-highres.png");
```

Karena kita menangani PNG, baris ini juga menunjukkan cara **extract text from png** tanpa langkah konversi tambahan. SDK secara internal menangani decoding PNG, jadi Anda tidak perlu khawatir tentang `ImageIO`.

## Langkah 6: Keluarkan Teks yang Diakui

Akhirnya, cetak hasil ke konsol atau alirkan ke layanan lain. Metode `getText()` mengembalikan `String` teks biasa.

```java
        // Print the extracted text
        System.out.println(result.getText());
    }
}
```

Menjalankan program harus menampilkan karakter yang ada di `sample-highres.png`. Jika gambar jelas dan bahasa cocok, Anda akan melihat transkripsi hampir sempurna.

## Contoh Lengkap yang Berfungsi

Menggabungkan semuanya, berikut kelas lengkap yang siap dijalankan:

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Apply the Aspose OCR license
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");

        // 2️⃣ Create OCR engine & enable GPU acceleration
        OcrEngine engine = new OcrEngine();
        engine.getDevice().setUseGpu(true);

        // 3️⃣ Set the language for recognition
        engine.setLanguage(Language.English);

        // 4️⃣ Recognize text from image (PNG in this case)
        OcrResult result = engine.recognizeImage("YOUR_DIRECTORY/sample-highres.png");

        // 5️⃣ Output the recognized text
        System.out.println("=== Extracted Text ===");
        System.out.println(result.getText());
    }
}
```

**Output yang diharapkan** (asumsi PNG berisi “Hello, World!”):

```
=== Extracted Text ===
Hello, World!
```

Jika hasilnya terlihat kacau, periksa kembali kualitas gambar dan pengaturan bahasa.

## Pertanyaan Umum & Kasus Tepi

### 1. *Bagaimana jika gambar saya JPEG atau TIFF?*  
Pemanggilan `recognizeImage` yang sama bekerja untuk JPEG, BMP, TIFF, dan bahkan PDF. Tidak perlu mengubah kode—cukup berikan jalur file yang tepat.

### 2. *Bisakah saya memproses banyak gambar dalam loop?*  
Tentu saja. Buat `OcrEngine` sekali, lalu panggil `recognizeImage` berulang kali. Menggunakan kembali mesin menghemat memori dan menjaga konteks GPU tetap hidup.

```java
String[] files = {"img1.png", "img2.png"};
for (String f : files) {
    OcrResult r = engine.recognizeImage(f);
    System.out.println(r.getText());
}
```

### 3. *GPU saya tidak terdeteksi—kenapa?*  
Pastikan Anda memiliki driver grafis terbaru terinstal. Aspose OCR mendukung CUDA 11+ dan OpenCL 2.0+. Jika driver tidak ada, mesin secara otomatis kembali ke CPU, yang lebih lambat tetapi tetap berfungsi.

### 4. *Bagaimana cara meningkatkan akurasi pada pemindaian berisik?*  
Pra‑proses gambar: tingkatkan kontras, terapkan binarisasi, atau gunakan kelas `PreprocessOptions` yang disediakan Aspose. Contoh:

```java
engine.getPreprocessOptions().setAutoContrast(true);
engine.getPreprocessOptions().setDenoise(true);
```

### 5. *Apakah ada cara untuk mendapatkan kotak pembatas untuk setiap kata?*  
Ya—`OcrResult` berisi koleksi objek `OcrRegion`. Iterasi melalui mereka untuk mendapatkan koordinat, berguna untuk menyorot teks di UI.

```java
for (OcrRegion region : result.getRegions()) {
    System.out.println(region.getText() + " → " + region.getBoundingBox());
}
```

## Tips Kinerja untuk GPU‑Accelerated OCR

- **Batch processing:** Berikan batch gambar ke mesin sebelum memanggil `flush()`; ini mengurangi overhead peluncuran kernel GPU.
- **Image size:** GPU menyukai dimensi pangkat‑dua. Mengubah ukuran gambar besar ke 1024×1024 terdekat (dengan mempertahankan rasio aspek) dapat mengurangi milidetik pada setiap pemanggilan.
- **Memory management:** Panggil `engine.dispose()` saat selesai, terutama pada layanan yang berjalan lama, untuk membebaskan memori GPU.

## Langkah Selanjutnya

Sekarang Anda dapat **recognize text from image** dan **extract text from png** dengan **gpu accelerated ocr**, pertimbangkan untuk menjelajahi:

- **Multi‑language OCR** (`engine.setLanguage(Language.Multilingual)`) untuk aplikasi global.
- **PDF text extraction** menggunakan `engine.recognizePdf`.
- **Integrating with Spring Boot** untuk mengekspos endpoint HTTP yang menerima unggahan gambar dan mengembalikan JSON dengan teks yang dikenali.

Ekstensi ini dibangun langsung pada konsep yang dibahas dalam **java ocr tutorial** ini, memungkinkan Anda mengubah demo konsol sederhana menjadi layanan lengkap.

---

*Selamat coding! Jika Anda mengalami kendala, tinggalkan komentar di bawah—saya senang membantu Anda memanfaatkan Aspose OCR dan akselerasi GPU sebaik mungkin.*

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [mengenali teks gambar dengan Aspose OCR – Tutorial Java OCR Lengkap](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Ekstrak Teks dari Gambar Java dengan Aspose.OCR Deteksi Mode Area](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Cara OCR Teks Gambar dengan Bahasa Menggunakan Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}