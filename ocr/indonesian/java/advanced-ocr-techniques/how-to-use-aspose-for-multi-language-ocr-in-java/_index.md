---
category: general
date: 2026-10-24
description: Pelajari cara mengekstrak teks dari gambar menggunakan Aspose OCR di
  Java, mendukung bahasa Inggris, Ukraina, dan Arab. Panduan langkah demi langkah
  untuk memuat gambar untuk OCR dan menjalankan OCR pada gambar.
draft: false
keywords:
- extract text from image
- load image for ocr
- run ocr on image
- Aspose OCR Java
- multi language OCR
lastmod: 2026-10-24
og_description: Pelajari cara mengekstrak teks dari gambar menggunakan Aspose OCR
  di Java, mendukung bahasa Inggris, Ukraina, dan Arab. Langkah-langkah untuk memuat
  gambar untuk OCR dan menjalankan OCR pada gambar.
og_image_alt: 'Developer guide: extract text from image using Aspose OCR in Java'
og_title: Cara mengekstrak teks dari gambar dengan Aspose OCR di Java
schemas:
- author: Aspose
  dateModified: '2026-10-24'
  description: Learn how to extract text from image using Aspose OCR in Java, supporting
    English, Ukrainian and Arabic. Step‑by‑step guide to load image for OCR and run
    OCR on image.
  headline: How to extract text from image with Aspose OCR in Java
  type: TechArticle
- questions:
  - answer: No, a single Aspose OCR license covers all bundled language packs.
    question: Do I need a separate license for each language pack?
  - answer: The only practical limit is memory; Aspose processes each image sequentially,
      so you can add hundreds of files without issue.
    question: Is there a limit on the number of images I can add to `OcrInput`?
  - answer: The engine analyses each text block independently, so it can switch languages
      mid‑line and still produce accurate results.
    question: How does auto‑detection handle mixed scripts on the same line?
  - answer: Yes, `OcrResult` provides a `getConfidence()` method for granular quality
      metrics.
    question: Can I get confidence scores for each recognized word?
  - answer: Aspose OCR works with Java 8 through Java 21, including LTS releases.
    question: What Java versions are supported?
  type: FAQPage
tags:
- Aspose
- OCR
- Java
- extract text from image
- multi language OCR
title: Cara mengekstrak teks dari gambar dengan Aspose OCR di Java
url: /id/java/advanced-ocr-techniques/how-to-use-aspose-for-multi-language-ocr-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara mengekstrak teks dari gambar dengan Aspose OCR di Java

Jika Anda perlu **mengekstrak teks dari gambar** yang berisi campuran karakter Bahasa Inggris, Ukraina, dan Arab, Aspose OCR membuatnya sederhana. Dalam tutorial ini Anda akan melihat contoh lengkap yang siap dijalankan yang menunjukkan cara **memuat gambar untuk OCR**, mengaktifkan *multi‑language OCR*, dan akhirnya **menjalankan OCR pada gambar** untuk mendapatkan teks yang bersih dan dapat dibaca. Langkah‑langkah dijelaskan dengan bahasa yang sederhana, sehingga Anda memahami baik *apa* yang harus dilakukan maupun *mengapa* hal itu penting.

## Jawaban cepat
- **Apa baris kode pertama?** `OcrEngine engine = new OcrEngine();`
- **Bahasa apa yang didukung secara default?** English (`en`), Ukrainian (`uk`), Arabic (`ar`) dan 27 bahasa tambahan.
- **Apakah saya memerlukan lisensi untuk pengujian?** Tidak, percobaan gratis berfungsi, tetapi lisensi menghapus watermark.
- **Bisakah saya memproses beberapa gambar sekaligus?** Ya, gunakan `OcrInput` untuk menambahkan beberapa file sebelum memanggil `recognize`.
- **Versi Java apa yang diperlukan?** Java 8 atau lebih baru.

## Cara mengekstrak teks dari gambar menggunakan Aspose OCR di Java?

Muat gambar Anda dengan `OcrInput`, konfigurasikan `OcrEngine` untuk bahasa yang diperlukan, dan panggil `engine.recognize(input)`. Mesin secara otomatis mendeteksi blok bahasa, menerapkan model OCR yang tepat, dan mengembalikan `OcrResult` yang berisi teks yang dikenali. Alur satu‑langkah ini bekerja untuk ukuran gambar apa pun hingga 10 000 × 10 000 piksel dan mendukung lebih dari 30 paket bahasa.

## Apa yang akan Anda pelajari

- Tambahkan pustaka Aspose OCR ke proyek Java (Maven atau Gradle).  
- Inisialisasi mesin OCR dengan benar.  
- Konfigurasikan mesin untuk *multi‑language OCR* dan aktifkan deteksi otomatis.  
- Muat gambar yang berisi skrip campuran.  
- Jalankan pengenalan dan **mengekstrak teks dari gambar**.  
- Tangani jebakan umum seperti bahasa yang tidak didukung atau file yang hilang.

Pada akhir tutorial Anda akan memiliki kelas Java mandiri yang dapat Anda masukkan ke proyek apa pun dan mulai memproses gambar secara instan.

## Prasyarat

| Persyaratan | Mengapa penting |
|-------------|----------------|
| Java 8 atau lebih baru | Aspose OCR menargetkan Java 8+. |
| Maven atau Gradle (alat build apa pun) | Secara otomatis mengunduh JAR Aspose OCR. |
| File gambar dengan teks campuran bahasa (misalnya `mixed_script.jpg`) | Ini adalah yang akan kita **memuat gambar untuk OCR**. |
| Lisensi Aspose OCR yang valid (opsional) | Tanpa lisensi Anda akan mendapatkan output berwatermark, tetapi kode tetap berfungsi sama. |

Sudah siap? Bagus—mari kita mulai.

## Langkah 1: tambahkan Aspose OCR ke proyek Anda

### Maven

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- latest as of Feb 2026 -->
</dependency>
```

### Gradle

```groovy
// build.gradle
implementation 'com.aspose:aspose-ocr:23.12'
```

> **Pro tip:** Aspose OCR mendukung lebih dari 30 paket bahasa dan dapat memproses gambar hingga 10 000 × 10 000 piksel tanpa memuat seluruh file ke memori, sehingga Anda dapat menangani pemindaian resolusi tinggi secara efisien.

Menambahkan dependensi adalah langkah konkret pertama dalam **cara menggunakan Aspose**—pustaka ini menyediakan kelas `OcrEngine`, `OcrInput`, dan `OcrResult` yang akan kita perlukan nanti.

## Langkah 2: inisialisasi mesin OCR

Kelas `OcrEngine` adalah komponen inti Aspose OCR yang melakukan proses pengenalan.  

```java
import com.aspose.ocr.*;

public class MultiLangOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 2.1: Create the OCR engine – the core object that does all the heavy lifting.
        OcrEngine engine = new OcrEngine();

        // Step 2.2: (Optional) Apply your license to avoid watermarks.
        // engine.setLicense("Aspose.Total.lic");
```

**Mengapa ini penting:**  
Jika Anda melewatkan inisialisasi mesin, tidak ada yang dapat *menjalankan OCR pada gambar* nanti, dan Anda akan mengalami `NullPointerException`.

## Langkah 3: konfigurasikan dukungan multi‑bahasa dan deteksi otomatis

`OcrEngine` menyediakan metode `setRecognitionLanguages` untuk menentukan model bahasa mana yang akan dimuat, dan `setAutoDetectLanguage` mengaktifkan deteksi bahasa otomatis per blok teks.  

```java
        // Step 3.1: Tell the engine which languages you expect.
        engine.setRecognitionLanguages(new String[] { "en", "uk", "ar" });

        // Step 3.2: Enable automatic language detection – crucial for mixed‑script images.
        engine.setAutoDetectLanguage(true);
```

**Penjelasan:**  
- `"en"` = Bahasa Inggris, `"uk"` = Bahasa Ukraina, `"ar"` = Bahasa Arab.  
- Deteksi otomatis memungkinkan Aspose memindai gambar, menentukan bahasa mana setiap segmen, dan menerapkan model OCR yang tepat. Tanpa itu Anda harus menjalankan tiga pengenalan terpisah—menyakitkan dan rawan kesalahan.

## Langkah 4: muat gambar untuk OCR

`OcrInput` adalah kontainer Aspose OCR yang menyimpan satu atau lebih aliran gambar untuk diproses.  

```java
        // Step 4.1: Prepare an OcrInput container.
        OcrInput input = new OcrInput();

        // Step 4.2: Add the image file. Replace the path with your actual location.
        input.add("YOUR_DIRECTORY/mixed_script.jpg");
```

> **Mengapa kami menggunakan `OcrInput`:** Ia dapat menampung beberapa halaman atau gambar, memberi Anda fleksibilitas untuk **memuat gambar untuk OCR** dalam mode batch nanti. Jika file tidak ditemukan, Aspose melempar `FileNotFoundException`. Pemeriksaan cepat (`if (!new File(path).exists())`) menghemat waktu debugging.

## Langkah 5: jalankan OCR pada gambar

Metode `recognize` menganalisis gambar, mendeteksi blok bahasa, dan menghasilkan objek `OcrResult` yang berisi teks yang dikenali.  

```java
        // Step 5.1: Execute the recognition process.
        OcrResult result = engine.recognize(input);
```

## Langkah 6: mengekstrak teks dari gambar dan menampilkannya

`OcrResult` membungkus output teks akhir, termasuk jeda baris dan skor kepercayaan.  

```java
        // Step 6.1: Pull the plain text out of the result.
        String extractedText = result.getText();

        // Step 6.2: Print it to the console – you could also write it to a file.
        System.out.println("=== Extracted Text ===");
        System.out.println(extractedText);
    }
}
```

**Apa yang akan Anda lihat:**  
Jika `mixed_script.jpg` berisi “Hello мир مرحبا”, output konsol akan menjadi:

```
=== Extracted Text ===
Hello мир مرحبا
```

Itulah solusi lengkap untuk **cara menggunakan Aspose** untuk **mengekstrak teks dari gambar** dengan banyak bahasa.

## Kasus tepi & pertanyaan umum

### Bagaimana jika sebuah bahasa tidak dikenali?

Aspose hanya mendukung bahasa yang memiliki model OCR. Untuk menambahkan bahasa Jepang, sertakan `"ja"` dalam `setRecognitionLanguages`. Jika model tidak tersedia, mesin akan kembali ke default (Inggris) dan Anda akan mendapatkan karakter yang kacau.

### Bagaimana meningkatkan akurasi pada gambar beresolusi rendah?

`setResolution` menetapkan nilai DPI yang diasumsikan mesin untuk gambar masukan, yang membantu pada pemindaian beresolusi rendah.  
`setPreprocessOptions` memilih tindakan pra‑pemrosesan seperti rotasi otomatis sebelum OCR.  

- Pra‑proses gambar (tingkatkan DPI, terapkan binarisasi).  
- Gunakan `engine.setResolution(300)` untuk memberi tahu mesin DPI yang diharapkan.  
- Aktifkan `engine.setPreprocessOptions(OcrEngine.PreprocessOptions.AutoRotate)` untuk pemindaian yang diputar.

### Bisakah saya memproses folder berisi gambar?

Tentu saja. Bungkus pemanggilan `input.add()` dalam loop yang mengiterasi semua file dalam sebuah direktori. Pemanggilan `engine.recognize(input)` yang sama akan mengembalikan teks yang digabungkan untuk setiap halaman.

## Contoh lengkap yang dapat dijalankan (siap salin‑tempel)

```java
import com.aspose.ocr.*;

public class MultiLangOcrDemo {
    public static void main(String[] args) throws Exception {

        // Create the OCR engine
        OcrEngine engine = new OcrEngine();

        // Optional: apply your license to avoid watermarks
        // engine.setLicense("Aspose.Total.lic");

        // Configure languages (English, Ukrainian, Arabic) and enable auto‑detect
        engine.setRecognitionLanguages(new String[] { "en", "uk", "ar" });
        engine.setAutoDetectLanguage(true);

        // Load the image that contains mixed‑language text
        OcrInput input = new OcrInput();
        input.add("YOUR_DIRECTORY/mixed_script.jpg"); // <-- replace with your path

        // Run the recognition process
        OcrResult result = engine.recognize(input);

        // Print the extracted text
        System.out.println("=== Extracted Text ===");
        System.out.println(result.getText());
    }
}
```

Simpan ini sebagai `MultiLangOcrDemo.java`, kompilasi dengan `javac`, dan jalankan `java MultiLangOcrDemo`. Jika semuanya telah diatur dengan benar, Anda akan melihat teks yang dikenali dicetak ke konsol.

## Pertanyaan yang sering diajukan

**Q: Apakah saya memerlukan lisensi terpisah untuk setiap paket bahasa?**  
A: Tidak, satu lisensi Aspose OCR mencakup semua paket bahasa yang disertakan.

**Q: Apakah ada batasan jumlah gambar yang dapat saya tambahkan ke `OcrInput`?**  
A: Satu‑satunya batas praktis adalah memori; Aspose memproses setiap gambar secara berurutan, sehingga Anda dapat menambahkan ratusan file tanpa masalah.

**Q: Bagaimana deteksi otomatis menangani skrip campuran pada baris yang sama?**  
A: Mesin menganalisis setiap blok teks secara independen, sehingga dapat beralih bahasa di tengah baris dan tetap menghasilkan hasil yang akurat.

**Q: Bisakah saya mendapatkan skor kepercayaan untuk setiap kata yang dikenali?**  
A: Ya, `OcrResult` menyediakan metode `getConfidence()` untuk metrik kualitas yang terperinci.

**Q: Versi Java apa yang didukung?**  
A: Aspose OCR bekerja dengan Java 8 hingga Java 21, termasuk rilis LTS.

## Kesimpulan

Kami telah membahas **cara menggunakan Aspose** secara menyeluruh: mulai dari menambahkan pustaka, melalui konfigurasi *multi‑language OCR*, hingga **memuat gambar untuk OCR**, **menjalankan OCR pada gambar**, dan akhirnya **mengekstrak teks dari gambar**. Pendekatan ini dapat diskalakan—cukup tambahkan lebih banyak kode bahasa atau berikan daftar file, dan Anda akan memiliki pipeline OCR yang kuat dalam hitungan menit.

Apa selanjutnya? Coba ide‑ide berikut:

- **Pemrosesan batch:** Loop melalui direktori dan tulis setiap hasil ke file `.txt` terpisah.  
- **Pasca‑pemrosesan:** Gunakan regex atau pustaka NLP untuk membersihkan output (menghapus jeda baris yang tidak diinginkan, memperbaiki kesalahan OCR umum).  
- **Integrasi:** Ekspos langkah OCR melalui endpoint REST Spring Boot sehingga layanan lain dapat mengirim gambar dan menerima teks berformat JSON.

Silakan bereksperimen, memecahkan masalah, dan kemudian memperbaikinya—itulah cara Anda benar‑benar menguasai OCR dengan Aspose. Jika Anda mengalami kendala, tinggalkan komentar di bawah. Selamat coding!  

---

![tangkapan layar cara menggunakan aspose OCR](/images/aspose-ocr-demo.png){alt="contoh cara menggunakan aspose OCR yang menampilkan kode Java"}

[tangkapan layar cara menggunakan aspose OCR](/images/aspose-ocr-demo.png)

**Terakhir Diperbarui:** 2026-10-24  
**Diuji Dengan:** Aspose OCR 24.11 for Java  
**Penulis:** Aspose

## Tutorial Terkait

- [Panduan Langkah demi Langkah Memuat Gambar untuk OCR di Java](/ocr/java/ocr-operations/load-image-for-ocr-in-java-step-by-step-guide/)
- [Panduan Langkah demi Langkah Deteksi Bahasa Otomatis dalam OCR Java](/ocr/java/advanced-ocr-techniques/automatic-language-detection-in-java-ocr-step-by-step-guide/)
- [Cara Mengaktifkan GPU untuk OCR di Java Ekstrak Teks dari Gambar](/ocr/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-extract-text-from-image/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}