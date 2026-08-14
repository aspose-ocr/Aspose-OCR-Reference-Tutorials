---
category: general
date: 2026-07-05
description: Tutorial OCR bahasa campuran untuk pengembang Java. Pelajari cara mendapatkan
  teks OCR dari gambar ke proyek Java dengan contoh OCR multibahasa.
draft: false
keywords:
- mixed language OCR
- get OCR text
- image to text Java
- java OCR example
- multi language OCR
language: id
og_description: OCR multibahasa dalam Java dijelaskan. Dapatkan teks OCR dari gambar
  menggunakan contoh OCR multibahasa yang dapat Anda salin‑tempel hari ini.
og_title: OCR Bahasa Campuran di Java – Panduan Pemrograman Lengkap
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Mixed language OCR tutorial for Java developers. Learn how to get OCR
    text from images to text Java projects with a multi language OCR example.
  headline: Mixed Language OCR in Java – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Mixed language OCR tutorial for Java developers. Learn how to get OCR
    text from images to text Java projects with a multi language OCR example.
  name: Mixed Language OCR in Java – Complete Step‑by‑Step Guide
  steps:
  - name: 1. Create a Maven Project
    text: 'Open a terminal and run:'
  - name: 2. Add the Aspose.OCR Dependency
    text: 'Edit the generated `pom.xml` and insert the following inside the `<dependencies>`
      block:'
  - name: How It Works
    text: '| Step | What Happens | Why It Matters | |------|--------------|----------------|
      | **1** | `OcrEngine` object is created. | The engine encapsulates all OCR functionality;
      without it you can’t call any methods. | | **2** | `setRecognitionLanguage`
      receives `ENGLISH` and `MALAYALAM`. | Supplying both'
  - name: Low‑Quality Images
    text: 'If the image is blurry or has poor contrast, OCR accuracy drops dramatically.
      Consider these remedies:'
  - name: Unsupported Languages
    text: Aspose currently supports over 70 scripts, but Malayalam may require a language
      pack. If `RecognitionLanguage.MALAYALAM` throws an exception, download the additional
      language data from Aspose’s portal and place it in `resources/ocr-data`.
  - name: Large PDFs
    text: When processing multi‑page PDFs, feed each page as a separate image or use
      `OcrEngine.recognizePdf`. The same `setRecognitionLanguage` call applies to
      every page, giving you a seamless **multi language OCR** experience across a
      whole document.
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: OCR Bahasa Campuran di Java – Panduan Lengkap Langkah demi Langkah
url: /id/java/advanced-ocr-techniques/mixed-language-ocr-in-java-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR Bahasa Campuran di Java – Panduan Lengkap Langkah‑per‑Langkah

Pernah membutuhkan **mixed language OCR** tetapi tidak yakin bagaimana melakukannya di Java? Anda bukan satu-satunya. Baik Anda sedang mendigitalkan dokumen lama yang beralih antara English dan Malayalam, atau membangun aplikasi pemindai yang mendukung beberapa skrip, tantangannya nyata. Dalam tutorial ini kami akan menunjukkan secara tepat cara **get OCR text** dari bitmap yang berisi kedua bahasa, menggunakan alur kerja **image to text Java** yang ringkas.

Kami akan menelusuri **java OCR example** yang siap dijalankan, menjelaskan mengapa setiap baris penting, dan membahas keanehan **multi language OCR** sehingga Anda dapat menghindari jebakan umum. Pada akhir tutorial Anda akan memiliki program yang berfungsi dan mencetak teks yang diekstrak ke konsol – tanpa pustaka misterius yang tidak dijelaskan.

## Apa yang Anda Butuhkan

* **Java Development Kit (JDK) 17** atau yang lebih baru – kode ini menggunakan sistem modul modern tetapi juga berfungsi pada JDK 11+.
* **Maven** (atau Gradle) – untuk mengambil pustaka OCR secara otomatis.
* Mesin OCR yang mendukung banyak bahasa – untuk panduan ini kami akan menggunakan **Aspose.OCR for Java**, yang menyediakan dukungan English dan Malayalam secara langsung. (Jika Anda lebih suka Tesseract, langkah-langkahnya serupa; cukup ganti pernyataan import.)
* Sebuah gambar contoh bernama `mixed_english_malayalam.png` ditempatkan dalam folder bernama `resources` di dalam proyek Anda.
* Sedikit rasa ingin tahu – sisanya dibahas di bawah.

> **Pro tip:** Jika Anda menggunakan Windows, jalankan `mvn -v` dari Command Prompt untuk memverifikasi Maven ada di PATH Anda.

## Menyiapkan Proyek

### 1. Buat Proyek Maven

Buka terminal dan jalankan:

```bash
mvn archetype:generate -DgroupId=com.example.ocr \
    -DartifactId=mixed-ocr-demo -DarchetypeArtifactId=maven-archetype-quickstart \
    -DinteractiveMode=false
```

### 2. Tambahkan Dependensi Aspose.OCR

Edit `pom.xml` yang dihasilkan dan sisipkan berikut ini di dalam blok `<dependencies>`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- latest as of July 2026 -->
</dependency>
```

Jalankan `mvn clean install` untuk mengunduh JAR. Maven akan menangani semuanya, jadi Anda tidak perlu mencari DLL native.

## Menulis Kode OCR Bahasa Campuran

Buat kelas baru `MixedLanguageOcrDemo.java` di bawah `src/main/java/com/example/ocr/` dan tempelkan kode lengkap di bawah ini. Setiap baris dikomentari sehingga Anda dapat melihat **mengapa** kami melakukan apa yang kami lakukan.

```java
package com.example.ocr;

import com.aspose.ocr.*;
import com.aspose.ocr.recognition.*;

public class MixedLanguageOcrDemo {

    public static void main(String[] args) {
        // Step 1: Initialise the OCR engine – this is the entry point for all operations.
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Tell the engine which languages to look for.
        // We pass both English and Malayalam; the engine will automatically switch
        // between scripts as it encounters them.
        ocrEngine.setRecognitionLanguage(
                RecognitionLanguage.ENGLISH,
                RecognitionLanguage.MALAYALAM);

        // Step 3: Load the image that contains mixed text.
        // Using a relative path keeps the example portable across machines.
        String imagePath = "resources/mixed_english_malayalam.png";

        // Optional: improve accuracy on low‑resolution scans.
        // Uncomment the next line if your image is under 300 DPI.
        // ocrEngine.setResolution(300);

        // Step 4: Perform the actual OCR operation.
        RecognitionResult result = ocrEngine.recognizeImage(imagePath);

        // Step 5: Extract the plain text – this is the "get OCR text" part.
        String extractedText = result.getText();

        // Step 6: Output the result to the console.
        System.out.println("=== Extracted Text ===");
        System.out.println(extractedText);
    }
}
```

### Cara Kerjanya

| Langkah | Apa yang Terjadi | Mengapa Penting |
|------|--------------|----------------|
| **1** | `OcrEngine` object dibuat. | Engine ini mengenkapsulasi semua fungsionalitas OCR; tanpa itu Anda tidak dapat memanggil metode apa pun. |
| **2** | `setRecognitionLanguage` menerima `ENGLISH` dan `MALAYALAM`. | Menyediakan kedua bahasa mengaktifkan **multi language OCR**; engine akan mendeteksi perubahan skrip secara otomatis. |
| **3** | Jalur gambar didefinisikan. | Menjaga jalur relatif menghindari hard‑coding lokasi absolut, membuat **java OCR example** dapat digunakan kembali. |
| **4** | `recognizeImage` memproses bitmap. | Di sinilah proses berat terjadi – engine menganalisis piksel, menjalankan jaringan saraf, dan mengembalikan `RecognitionResult`. |
| **5** | `getText()` mengekstrak string biasa. | Ini adalah metode tepat yang Anda butuhkan untuk **get OCR text** untuk pemrosesan lebih lanjut (mis., menyimpan ke DB). |
| **6** | `System.out.println` mencetak string. | Umpan balik visual langsung membantu Anda memverifikasi bahwa pipeline **image to text Java** berfungsi. |

> **Catatan:** Jika Anda menemukan `java.lang.UnsatisfiedLinkError`, pastikan folder pustaka native berada di `java.library.path` Anda. Aspose menyediakan binary yang diperlukan untuk Windows, macOS, dan Linux.

## Menjalankan Demo

Kompilasi dan eksekusi dengan Maven:

```bash
mvn compile exec:java -Dexec.mainClass="com.example.ocr.MixedLanguageOcrDemo"
```

Anda akan melihat output serupa dengan:

```
=== Extracted Text ===
Welcome to the conference.
സ്വാഗതം
```

Baris pertama berbahasa English, baris kedua berbahasa Malayalam – bukti bahwa **mixed language OCR** kami berhasil.

## Menangani Kasus Tepi Umum

### Gambar Berkualitas Rendah

Jika gambar buram atau memiliki kontras yang buruk, akurasi OCR turun drastis. Pertimbangkan solusi berikut:

* **Pre‑process** gambar dengan pustaka seperti OpenCV – konversi ke grayscale, terapkan adaptive thresholding, dan tingkatkan skala setidaknya ke 300 DPI.  
* Aktifkan `ocrEngine.setAutoSkewCorrection(true)` agar engine meluruskan teks yang diputar.  
* Tingkatkan `ocrEngine.setConfidenceThreshold(0.6f)` jika Anda memerlukan penyaringan kepercayaan yang lebih ketat.

### Bahasa yang Tidak Didukung

Aspose saat ini mendukung lebih dari 70 skrip, tetapi Malayalam mungkin memerlukan paket bahasa. Jika `RecognitionLanguage.MALAYALAM` melemparkan pengecualian, unduh data bahasa tambahan dari portal Aspose dan letakkan di `resources/ocr-data`.

### PDF Besar

Saat memproses PDF multi‑halaman, berikan setiap halaman sebagai gambar terpisah atau gunakan `OcrEngine.recognizePdf`. Pemanggilan `setRecognitionLanguage` yang sama berlaku untuk setiap halaman, memberikan pengalaman **multi language OCR** yang mulus di seluruh dokumen.

## Memperluas Contoh: Dari Konsol ke Layanan Web

Jika Anda ingin mengekspos fungsionalitas ini melalui endpoint REST, tambahkan Spring Boot:

```java
@RestController
@RequestMapping("/api/ocr")
public class OcrController {

    @PostMapping(value = "/extract", consumes = MediaType.MULTIPART_FORM_DATA_VALUE)
    public String extractText(@RequestParam("file") MultipartFile file) throws IOException {
        OcrEngine engine = new OcrEngine();
        engine.setRecognitionLanguage(RecognitionLanguage.ENGLISH, RecognitionLanguage.MALAYALM);
        // Save multipart file to a temporary location
        Path temp = Files.createTempFile("upload-", ".png");
        Files.write(temp, file.getBytes());
        RecognitionResult res = engine.recognizeImage(temp.toString());
        return res.getText();
    }
}
```

Sekarang klien mana pun dapat `POST` sebuah gambar dan menerima hasil **get OCR text** sebagai JSON biasa. Ekstensi kecil ini menunjukkan bagaimana **java OCR example** yang sama dapat berkembang dari demo satu‑file menjadi layanan siap produksi.

## Snapshot Pohon Sumber Lengkap

```
mixed-ocr-demo/
├─ pom.xml
└─ src/
   └─ main/
      ├─ java/
      │  └─ com/example/ocr/
      │     └─ MixedLanguageOcrDemo.java
      └─ resources/
         └─ mixed_english_malayalam.png
```

Menyertakan seluruh tata letak proyek dalam artikel memudahkan pembaca menyalin struktur ke IDE mereka dan menjalankannya secara instan.

![output contoh OCR bahasa campuran](https://example.com/assets/mixed-ocr-output.png "output contoh OCR bahasa campuran")

*Teks alt gambar:* output contoh OCR bahasa campuran – menampilkan teks English dan Malayalam yang diekstrak dari gambar yang sama.

## Ringkasan & Langkah Selanjutnya

Kami telah membahas pipeline **mixed language OCR** di Java dari awal hingga akhir:

* Menyiapkan proyek Maven dan menambahkan dependensi Aspose OCR.  
* Mengonfigurasi engine untuk English + Malayalam, melakukan pengenalan, dan **got OCR text**.  
* Membahas kualitas gambar, paket bahasa, dan cara mengubah aplikasi konsol menjadi layanan web.

Jika Anda siap melangkah lebih jauh, coba ide-ide berikut:

* Ganti Aspose dengan **Tesseract** untuk melihat bagaimana engine open‑source menangani **multi language OCR**.  
* Bereksperimen dengan bahasa tambahan seperti Hindi atau Tamil – cukup tambahkan ke `setRecognitionLanguage`.  
* Integrasikan hasil dengan indeks pencarian (mis., Elasticsearch) untuk mengaktifkan pencarian berbasis **image to text Java** pada arsip yang dipindai.

Jangan ragu meninggalkan komentar jika ada yang tidak berjalan seperti yang diharapkan, atau bagikan penyesuaian Anda sendiri. Selamat coding, semoga pemindaian Anda selalu jernih!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Ekstrak Teks Gambar – Dasar OCR dengan Aspose.OCR untuk Java](/ocr/english/java/ocr-basics/)
- [Cara OCR Teks Gambar dengan Bahasa Menggunakan Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [mengenali gambar teks dengan Aspose OCR – Tutorial OCR Java Lengkap](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}