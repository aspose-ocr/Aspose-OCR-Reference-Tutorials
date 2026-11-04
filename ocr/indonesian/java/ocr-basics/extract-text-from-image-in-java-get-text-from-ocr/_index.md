---
category: general
date: 2026-05-25
description: Ekstrak teks dari gambar di Java menggunakan OCR. Pelajari cara memuat
  gambar untuk OCR, mengenali teks dari foto, dan mendapatkan teks dari OCR dengan
  contoh kode sederhana.
draft: false
keywords:
- extract text from image
- get text from ocr
- recognize text from photo
- java image to text
- load image for ocr
language: id
og_description: Ekstrak teks dari gambar dalam Java dengan panduan langkah demi langkah.
  Pelajari cara memuat gambar untuk OCR, mengenali teks dari foto, dan mendapatkan
  teks dari OCR secara efisien.
og_title: Ekstrak Teks dari Gambar dalam Java – Dapatkan Teks dari OCR
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: Extract text from image in Java using OCR. Learn how to load image
    for OCR, recognize text from photo, and get text from OCR with a simple code example.
  headline: Extract Text from Image in Java – Get Text from OCR
  type: TechArticle
- description: Extract text from image in Java using OCR. Learn how to load image
    for OCR, recognize text from photo, and get text from OCR with a simple code example.
  name: Extract Text from Image in Java – Get Text from OCR
  steps:
  - name: '**Wrong language setting** – If you forget step 2, the engine defaults
      to English, turning Cyrillic characters into gibberish. Always double‑check
      the language code.'
    text: '**Wrong language setting** – If you forget step 2, the engine defaults
      to English, turning Cyrillic characters into gibberish. Always double‑check
      the language code.'
  - name: '**Image quality matters** – Low‑resolution or blurry photos will degrade
      accuracy. Pre‑process with contrast enhancement or binarization if needed.'
    text: '**Image quality matters** – Low‑resolution or blurry photos will degrade
      accuracy. Pre‑process with contrast enhancement or binarization if needed.'
  - name: '**File path quirks** – On Windows, backslashes need escaping (`C:\images\file.jpg`).
      Using `Path.of(...)` from `java.nio.file` sidesteps this.'
    text: '**File path quirks** – On Windows, backslashes need escaping (`C:\images\file.jpg`).
      Using `Path.of(...)` from `java.nio.file` sidesteps this.'
  - name: '**Memory leaks** – `OcrEngine` holds native resources. Call `ocrEngine.dispose()`
      when you’re done, especially in long‑running services.'
    text: '**Memory leaks** – `OcrEngine` holds native resources. Call `ocrEngine.dispose()`
      when you’re done, especially in long‑running services.'
  - name: '**Thread safety** – The engine isn’t thread‑safe out of the box. Create
      a separate instance per thread or synchronize access.'
    text: '**Thread safety** – The engine isn’t thread‑safe out of the box. Create
      a separate instance per thread or synchronize access.'
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: Ekstrak Teks dari Gambar di Java – Dapatkan Teks dari OCR
url: /id/java/ocr-basics/extract-text-from-image-in-java-get-text-from-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ekstrak Teks dari Gambar di Java – Dapatkan Teks dari OCR

Pernah perlu **mengekstrak teks dari gambar** tetapi tidak yakin pustaka Java mana yang harus dipilih? Anda tidak sendirian. Baik Anda mendigitalkan kwitansi, mengambil nomor seri dari foto produk, atau sekadar bermain dengan proyek sampingan yang menyenangkan, mengubah gambar menjadi teks yang dapat diedit adalah tantangan umum.

Dalam tutorial ini kami akan membahas contoh lengkap yang siap dijalankan yang menunjukkan cara **memuat gambar untuk OCR**, mengonfigurasi mesin, dan akhirnya **mengenali teks dari foto** sehingga Anda dapat **mendapatkan teks dari OCR** dengan hanya beberapa baris kode. Tidak ada referensi yang samar—semua yang Anda butuhkan ada di sini.

## Apa yang Akan Anda Pelajari

* Cara menyiapkan mesin OCR ringan di Java.  
* Langkah‑langkah tepat untuk **memuat gambar untuk OCR** dan menangani berbagai jalur file.  
* Mengapa mengonfigurasi bahasa penting ketika Anda ingin **mengekstrak teks dari gambar** yang bukan bahasa Inggris.  
* Cara menampilkan hasil dengan aman dan apa yang harus dilakukan ketika mesin tidak mengembalikan apa‑apa.  
* Beberapa tips profesional untuk menghindari jebakan paling umum.

Pada akhir panduan ini Anda akan memiliki program mandiri yang membaca file JPEG (atau PNG) yang berisi karakter Ukraina dan mencetak string yang dikenali ke konsol. Silakan ganti bahasa atau gambar—semuanya modular.

---

![Diagram showing the flow of extracting text from image using Java OCR engine](/images/extract-text-from-image-java.png)

*Alt text: Diagram alur proses mengekstrak teks dari gambar dalam Java.*

## Prasyarat

* **Java Development Kit (JDK) 11+** – kode menggunakan sistem modul modern, tetapi versi lama dapat bekerja dengan sedikit penyesuaian.  
* **Maven atau Gradle** – untuk mengunduh pustaka OCR (kami akan menggunakan **Asprise OCR** sebagai opsi ringan dan gratis untuk pengembangan).  
* File gambar contoh (misalnya `ukrainian_sign.jpg`) ditempatkan di lokasi yang dapat dibaca program Anda.  
* Familiaritas dasar dengan metode `main` Java dan penanganan pengecualian.

Jika Anda sudah memiliki semua ini, Anda siap melanjutkan. Jika tidak, unduh JDK dari Oracle atau AdoptOpenJDK dan siapkan proyek Maven sederhana—tidak perlu yang rumit.

---

## Langkah 1: Tambahkan Dependensi OCR

Pertama, beri tahu alat build Anda untuk mengambil mesin OCR. Untuk Maven, letakkan ini ke dalam `pom.xml`:

```xml
<dependency>
    <groupId>com.asprise.ocr</groupId>
    <artifactId>asprise-ocr</artifactId>
    <version>1.0.2</version>
</dependency>
```

Jika Anda lebih suka Gradle, setaraannya adalah:

```gradle
implementation 'com.asprise.ocr:asprise-ocr:1.0.2'
```

Koordinat ini mengunduh JAR kompak yang mencakup `OcrEngine`, `OcrLanguage`, dan kelas pembantu yang akan kami gunakan. Tidak diperlukan binari native tambahan untuk skrip Latin dan Cyrillic dasar.

---

## Langkah 2: Buat Kelas Java untuk **Ekstrak Teks dari Gambar**

Sekarang kita akan menulis program sebenarnya. Simpan yang berikut sebagai `ExtractTextDemo.java` di dalam `src/main/java/com/example/ocr/`.

```java
package com.example.ocr;

import com.asprise.ocr.OcrEngine;
import com.asprise.ocr.OcrLanguage;

/**
 * Demonstrates how to extract text from image using Asprise OCR.
 * The example loads a JPEG, sets the language to Ukrainian,
 * runs recognition, and prints the result.
 */
public class ExtractTextDemo {

    public static void main(String[] args) {
        // ---- 1️⃣  Initialize the OCR engine ---------------------------------
        OcrEngine ocrEngine = new OcrEngine();

        // ---- 2️⃣  Configure the engine to recognize Ukrainian text -----------
        // This is crucial if your image contains non‑Latin characters.
        ocrEngine.getEngineOptions().setLanguage(OcrLanguage.UKRAINIAN);

        // ---- 3️⃣  Load the image that contains Ukrainian characters ----------
        // Replace the path with the location of your own picture.
        String imagePath = "YOUR_DIRECTORY/ukrainian_sign.jpg";
        try {
            ocrEngine.getImage().loadFromFile(imagePath);
        } catch (Exception e) {
            System.err.println("Failed to load image: " + e.getMessage());
            return;
        }

        // ---- 4️⃣  Perform OCR recognition and obtain the extracted text -------
        String recognizedText;
        try {
            recognizedText = ocrEngine.recognize().getText();
        } catch (Exception e) {
            System.err.println("Recognition error: " + e.getMessage());
            return;
        }

        // ---- 5️⃣  Output the recognized text to the console -------------------
        System.out.println("=== OCR Result ===");
        System.out.println(recognizedText);
    }
}
```

### Mengapa Struktur Ini Berfungsi

* **Blok bernomor terpisah** memudahkan alur untuk diikuti, terutama ketika Anda mencari tempat **memuat gambar untuk OCR** atau **mengenali teks dari foto**.  
* `try/catch` di sekitar pemuatan gambar dan pengenalan memastikan program gagal dengan elegan—berguna ketika jalur file salah atau mesin OCR tidak dapat menemukan data bahasa.  
* Menetapkan bahasa di awal (langkah 2) secara dramatis meningkatkan akurasi untuk skrip non‑Inggris. Jika Anda kemudian membutuhkan **java image to text** untuk bahasa lain, cukup ganti `OcrLanguage.UKRAINIAN` dengan `OcrLanguage.ENGLISH`, `FRENCH`, dll.

---

## Langkah 3: Bangun dan Jalankan Program

Dari root proyek, jalankan:

```bash
mvn clean compile exec:java -Dexec.mainClass="com.example.ocr.ExtractTextDemo"
```

Atau, jika Anda menggunakan Gradle:

```bash
./gradlew run --args="com.example.ocr.ExtractTextDemo"
```

Dengan asumsi `ukrainian_sign.jpg` berisi teks *«Ласкаво просимо»* (Ukraina untuk “Welcome”), Anda akan melihat sesuatu seperti:

```
=== OCR Result ===
Ласкаво просимо
```

Output tersebut mengonfirmasi Anda berhasil **mengekstrak teks dari gambar** dan **mendapatkan teks dari OCR** dalam satu kali jalankan.

---

## Langkah 4: Sesuaikan Alur Kerja – Dari **Java Image to Text** dalam Proyek Nyata

Meskipun demo ini minimal, aplikasi dunia nyata sering membutuhkan sedikit lebih banyak:

| Scenario | What to Adjust | Reason |
|----------|----------------|--------|
| **Pemrosesan batch** | Loop over a `List<Path>` and store each result in a database. | Mengurangi pekerjaan manual ketika Anda memiliki ratusan foto. |
| **Format gambar berbeda** | Use `ImageIO.read(new File(path))` to pre‑process, then pass the `BufferedImage` to `ocrEngine.getImage().loadFromBufferedImage(bufImg)`. | Menangani PNG, BMP, atau bahkan PDF setelah konversi. |
| **Penyetelan kinerja** | Call `ocrEngine.getEngineOptions().setSpeed(OcrEngine.Speed.FAST)` if you’re okay with slightly lower accuracy. | Mempercepat pengenalan pada perangkat keras kelas rendah. |
| **Pasca‑pemrosesan** | Trim whitespace, replace common OCR mis‑reads (`0` → `O`, `1` → `I`). | Meningkatkan kualitas data di tahap selanjutnya. |

Variasi ini menjaga gagasan inti—**mengenali teks dari foto**—tetap utuh sambil memberi Anda fleksibilitas untuk beban kerja produksi.

---

## Kesalahan Umum & Tips Profesional

1. **Pengaturan bahasa yang salah** – Jika Anda lupa langkah 2, mesin akan default ke bahasa Inggris, mengubah karakter Cyrillic menjadi sampah. Selalu periksa kembali kode bahasa.  
2. **Kualitas gambar penting** – Foto beresolusi rendah atau blur akan menurunkan akurasi. Lakukan pra‑pemrosesan dengan peningkatan kontras atau binarisasi bila diperlukan.  
3. **Keanehan jalur file** – Di Windows, backslash harus di‑escape (`C:\\images\\file.jpg`). Menggunakan `Path.of(...)` dari `java.nio.file` menghindari masalah ini.  
4. **Memory leak** – `OcrEngine` menyimpan sumber daya native. Panggil `ocrEngine.dispose()` saat selesai, terutama pada layanan yang berjalan lama.  
5. **Keamanan thread** – Mesin tidak thread‑safe secara default. Buat instance terpisah per thread atau sinkronkan akses.

---

## Contoh Lengkap yang Berfungsi (Semua‑Dalam‑Satu)

Berikut adalah satu file tunggal yang dapat Anda salin‑tempel ke IDE apa pun. File ini menyertakan pemanggilan `dispose()` dan metode pembantu kecil untuk membuat kode lebih bersih.

```java
package com.example.ocr;

import com.asprise.ocr.OcrEngine;
import com.asprise.ocr.OcrLanguage;
import java.nio.file.Path;

/**
 * Complete, runnable demo that extracts text from an image using Java OCR.
 */
public class FullDemo {

    public static void main(String[] args) {
        // Path to the image – change this to your own file.
        Path imgPath = Path.of("YOUR_DIRECTORY/ukrainian_sign.jpg");

        // Run the OCR workflow and capture the output.
        String result = extractTextFromImage(imgPath, OcrLanguage.UKRAINIAN);
        if (result != null) {
            System.out.println("=== OCR Result ===");
            System.out.println(result);
        }
    }

    /**
     * Core method that encapsulates the 5‑step OCR process.
     *
     * @param imagePath Path to the image file.
     * @param language  Desired OCR language.
     * @return Recognized text, or {@code null} if something went wrong.
     */
    private static String extractTextFromImage(Path imagePath, OcrLanguage language) {
        OcrEngine engine = new OcrEngine();
        try {
            // 1️⃣ Set language
            engine.getEngineOptions().setLanguage(language);

            // 2️⃣ Load image
            engine.getImage().loadFromFile(imagePath.toString());

            // 3️⃣ Recognize and return text
            return engine.recognize().getText();
        } catch (Exception e) {
            System.err.println("Error during OCR: " + e.getMessage());
            return null;
        } finally {
            // 4️⃣ Release native resources
            engine.dispose();
        }
    }
}
```

Menjalankan program ini menghasilkan output konsol yang sama seperti yang ditunjukkan sebelumnya. Silakan ganti `OcrLanguage.UKRAINIAN` dengan `OcrLanguage.ENGLISH` atau bahasa lain yang didukung untuk melihat bagaimana mesin menyesuaikan.

## Kesimpulan

Kami telah membahas semua yang Anda perlukan untuk **mengekstrak teks dari gambar** menggunakan Java: mulai dari menambahkan dependensi OCR, hingga **memuat gambar untuk OCR**, 

## Tutorial Terkait

- [Mengenali gambar teks dengan Aspose OCR – Tutorial OCR Java Lengkap](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Cara OCR Teks Gambar dengan Bahasa Menggunakan Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Konversi Gambar ke Teks di Java menggunakan Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}