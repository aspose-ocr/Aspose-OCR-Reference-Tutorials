---
category: general
date: 2026-08-18
description: Cara mengaktifkan GPU untuk OCR di Java dan dengan cepat mengenali teks
  gambar, mengekstrak teks JPG, menambahkan filter, serta mengatur bahasa dengan Aspose.OCR.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to enable gpu
- recognize image text
- extract text jpg
- how to add filter
- how to set language
language: id
lastmod: 2026-08-18
og_description: Cara mengaktifkan GPU untuk OCR di Java dan langsung mengenali teks
  gambar, mengekstrak teks JPG, menambahkan filter, serta mengatur bahasa menggunakan
  Aspose.OCR.
og_image_alt: Screenshot showing Java code that enables GPU for OCR with Aspose.OCR
og_title: Cara mengaktifkan GPU untuk OCR di Java – panduan lengkap Aspose.OCR
schemas:
- author: Aspose
  dateModified: '2026-08-18'
  description: How to enable GPU for OCR in Java and quickly recognize image text,
    extract text JPG, add filter, and set language with Aspose.OCR.
  headline: How to enable GPU for OCR in Java using Aspose.OCR
  type: TechArticle
- description: How to enable GPU for OCR in Java and quickly recognize image text,
    extract text JPG, add filter, and set language with Aspose.OCR.
  name: How to enable GPU for OCR in Java using Aspose.OCR
  steps:
  - name: 3.1 Set the OCR language
    text: '```java // Choose the language for recognition – this is the “how to set
      language” step engine.setLanguage(OcrLanguage.ENGLISH); ```'
  - name: 3.2 Add a preprocessing filter
    text: 'Noise, compression artifacts, or uneven lighting can hurt accuracy. Adding
      a denoise filter is the typical **how to add filter** approach:'
  - name: Expected output
    text: '``` Recognized text: The quick brown fox jumps over the lazy dog. ```'
  type: HowTo
tags:
- OCR
- Java
- Aspose
- GPU acceleration
title: Cara mengaktifkan GPU untuk OCR di Java menggunakan Aspose.OCR
url: /id/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Mengaktifkan GPU untuk OCR di Java menggunakan Aspose.OCR

Jika Anda perlu **cara mengaktifkan GPU** untuk OCR di Java, panduan ini akan memandu Anda melalui langkah‑langkah yang tepat. Mengaktifkan akselerasi GPU memungkinkan Anda **mengenali teks gambar** hingga beberapa kali lebih cepat, yang penting ketika Anda harus **mengekstrak teks JPG** secara massal. Kami juga akan membahas **cara menambahkan filter**, **cara mengatur bahasa**, dan cara mengambil hasil akhir.

Pada akhir tutorial ini Anda akan memiliki program lengkap yang dapat dijalankan yang:

* Memulai mesin Aspose.OCR dengan dukungan GPU.  
* Mengonfigurasi bahasa OCR (misalnya, Inggris).  
* Menerapkan filter denoising untuk meningkatkan akurasi.  
* Memuat gambar JPEG, menjalankan pengenalan, dan mencetak teks yang diekstrak.

> **Prasyarat:** Java 17 atau lebih baru, Maven, dan lisensi Aspose.OCR untuk Java (versi percobaan gratis dapat digunakan untuk evaluasi).

---

![How to enable GPU for OCR in Java](/images/ocr-gpu.png){alt="Cara mengaktifkan GPU untuk OCR di Java"}

## Apa yang Anda Butuhkan

| Item | Alasan |
|------|--------|
| **Java Development Kit (JDK) 17+** | Diperlukan untuk mengompilasi dan menjalankan contoh. |
| **Maven** | Mempermudah manajemen dependensi untuk Aspose.OCR. |
| **Aspose.OCR untuk Java** | Menyediakan kelas `OcrEngine` dan dukungan GPU. |
| **Contoh gambar JPEG** (`sample.jpg`) | Digunakan untuk mendemonstrasikan **mengekstrak teks JPG**. |
| **Perangkat keras yang kompatibel dengan GPU** (opsional tetapi disarankan) | Mengaktifkan peningkatan performa yang akan kami konfigurasikan. |

---

## Langkah 1: Siapkan proyek Maven

Buat proyek Maven baru (atau tambahkan ke proyek yang sudah ada) dan sertakan dependensi Aspose.OCR:

```xml
<!-- pom.xml -->
<project xmlns="http://maven.apache.org/POM/4.0.0" ...>
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>ocr-gpu-demo</artifactId>
    <version>1.0.0</version>
    <properties>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
    </properties>

    <dependencies>
        <!-- Aspose.OCR for Java -->
        <dependency>
            <groupId>com.aspose</groupId>
            <artifactId>aspose-ocr</artifactId>
            <version>23.12</version> <!-- Use the latest stable version -->
        </dependency>
    </dependencies>
</project>
```

> **Tips pro:** Pastikan nomor versi selalu terbaru; rilis yang lebih baru meningkatkan penanganan GPU dan menambahkan paket bahasa.

---

## Langkah 2: Inisialisasi mesin OCR dan **cara mengaktifkan GPU**

Inti solusi adalah `OcrEngine`. Membuat instansinya sangat sederhana, tetapi Anda harus secara eksplisit mengaktifkan akselerasi GPU:

```java
import com.aspose.ocr.*;

public class HelloWorldOcr {
    public static void main(String[] args) throws Exception {
        // Step 2.1: Initialize the OCR engine
        OcrEngine engine = new OcrEngine();

        // Step 2.2: Enable GPU acceleration (this is the “how to enable GPU” part)
        engine.setUseGpu(true); // <-- GPU is now active

        // Step 2.3: Configure language and preprocessing filter (covered later)
```

**Mengapa mengaktifkan GPU?**  
Saat `setUseGpu(true)` dipanggil, Aspose.OCR memindahkan kernel pemrosesan gambar yang berat ke kartu grafis. Pada GPU NVIDIA/AMD modern kecepatan pengenalan dapat meningkat dari ~200 ms per halaman menjadi < 80 ms, yang secara dramatis mengurangi total waktu pemrosesan untuk batch besar.

---

## Langkah 3: **Cara mengatur bahasa** dan **cara menambahkan filter**

### 3.1 Atur bahasa OCR

```java
        // Choose the language for recognition – this is the “how to set language” step
        engine.setLanguage(OcrLanguage.ENGLISH);
```

Aspose.OCR dilengkapi dengan paket bahasa untuk lebih dari 100 bahasa. Ganti `ENGLISH` dengan `FRENCH`, `CHINESE_SIMPLIFIED`, dll., sesuai dengan materi sumber Anda.

### 3.2 Tambahkan filter pra‑pemrosesan

Noise, artefak kompresi, atau pencahayaan tidak merata dapat menurunkan akurasi. Menambahkan filter denoise adalah pendekatan **cara menambahkan filter** yang umum:

```java
        // Add a denoising filter to improve OCR quality – “how to add filter”
        engine.addPreprocessFilter(FilterType.DENOISE);
```

Filter berguna lainnya meliputi `FilterType.CONTRAST`, `FilterType.BRIGHTNESS`, dan `FilterType.BINARIZE`. Anda dapat menambahkan beberapa filter secara berurutan dengan memanggil `addPreprocessFilter` berulang kali.

---

## Langkah 4: Muat gambar – **mengekstrak teks JPG**

Sekarang kita arahkan mesin ke file JPEG yang ingin diproses:

```java
        // Load the JPEG image – this demonstrates “extract text JPG”
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.jpg"));
```

Ganti `YOUR_DIRECTORY` dengan jalur aktual tempat `sample.jpg` berada. Aspose.OCR juga mendukung PNG, BMP, TIFF, dan PDF; pemanggilan yang sama bekerja untuk format tersebut.

---

## Langkah 5: Lakukan OCR dan **mengenali teks gambar**

Dengan mesin yang telah dikonfigurasi, panggil prosedur pengenalan:

```java
        // Run the OCR operation – “recognize image text”
        engine.recognize();

        // Retrieve the recognized text
        String text = engine.getText();
        System.out.println("Recognized text: " + text);
    }
}
```

Metode `recognize()` memproses gambar di GPU (jika diaktifkan) dan mengisi buffer teks internal. `getText()` mengembalikan `String` teks biasa, yang dapat Anda tulis ke file, basis data, atau diteruskan ke pipeline NLP selanjutnya.

### Output yang diharapkan

```
Recognized text: The quick brown fox jumps over the lazy dog.
```

Jika gambar berisi beberapa baris, string yang dikembalikan mencakup karakter baris baru (`\n`) yang mempertahankan tata letak asli.

---

## Langkah 6: Verifikasi penggunaan GPU (opsional)

Untuk memastikan GPU memang digunakan, aktifkan logging Aspose:

```java
        // Enable diagnostic logging (optional)
        engine.setLogLevel(com.aspose.ocr.logging.LogLevel.DEBUG);
        engine.setLogFile("ocr-debug.log");
```

Periksa `ocr-debug.log` setelah menjalankan; Anda harus melihat entri seperti `GPU device: NVIDIA GeForce RTX 3080` dan `Processing time (GPU): 78 ms`. Jika log menyebut **CPU**, periksa kembali instalasi driver Anda dan pastikan pemanggilan `setUseGpu(true)` ada.

---

## Kesalahan umum dan cara menghindarinya

| Gejala | Penyebab yang Mungkin | Solusi |
|--------|-----------------------|--------|
| **`java.lang.UnsatisfiedLinkError: no aspose_ocr_native`** | Hilangnya pustaka native GPU | Instal driver GPU terbaru dan pastikan binary native `aspose-ocr` berada di `java.library.path`. |
| **Akurasi buruk pada gambar gelap** | Tidak ada filter pra‑pemrosesan | Tambahkan `engine.addPreprocessFilter(FilterType.BRIGHTNESS)` atau tingkatkan `FilterType.CONTRAST`. |
| **`OutOfMemoryError` pada batch besar** | Kehabisan memori GPU | Proses gambar dalam batch lebih kecil atau nonaktifkan GPU (`engine.setUseGpu(false)`) untuk resolusi sangat besar. |
| **Output bahasa tidak tepat** | Bahasa yang diatur salah | Verifikasi `engine.setLanguage(OcrLanguage.YOUR_LANGUAGE)` sesuai dengan teks sumber. |

---

## Contoh lengkap yang dapat dijalankan

Berikut adalah kelas Java lengkap yang dapat Anda salin‑tempel ke `src/main/java/com/example/HelloWorldOcr.java`. Kelas ini mencakup semua langkah, penanganan error, dan logging opsional.

```java
package com.example;

import com.aspose.ocr.*;

public class HelloWorldOcr {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine
        OcrEngine engine = new OcrEngine();

        // -------------------------------------------------
        // 1️⃣ Enable GPU acceleration – how to enable GPU
        // -------------------------------------------------
        engine.setUseGpu(true);

        // -------------------------------------------------
        // 2️⃣ Set language – how to set language
        // -------------------------------------------------
        engine.setLanguage(OcrLanguage.ENGLISH); // Change if needed

        // -------------------------------------------------
        // 3️⃣ Add preprocessing filter – how to add filter
        // -------------------------------------------------
        engine.addPreprocessFilter(FilterType.DENOISE);
        // Optional: engine.addPreprocessFilter(FilterType.CONTRAST);

        // -------------------------------------------------
        // 4️⃣ Load the JPEG image – extract text JPG
        // -------------------------------------------------
        String imagePath = "YOUR_DIRECTORY/sample.jpg";
        engine.setImage(ImageStream.fromFile(imagePath));

        // -------------------------------------------------
        // 5️⃣ Perform OCR – recognize image text
        // -------------------------------------------------
        engine.recognize();

        // Retrieve and display the recognized text
        String text = engine.getText();
        System.out.println("Recognized text: " + text);

        // -------------------------------------------------
        // 6️⃣ Optional: write output to a file
        // -------------------------------------------------
        java.nio.file.Files.writeString(
                java.nio.file.Paths.get("output.txt"),
                text,
                java.nio.charset.StandardCharsets.UTF_8
        );

        // -------------------------------------------------
        // 7️⃣ Optional: enable debug logging to verify GPU usage
        // -------------------------------------------------
        engine.setLogLevel(com.aspose.ocr.logging.LogLevel.DEBUG);
        engine.setLogFile("ocr-debug.log");
    }
}
```

**Menjalankan program**

```bash
mvn compile exec:java -Dexec.mainClass=com.example.HelloWorldOcr
```

Anda akan melihat teks yang dikenali dicetak ke konsol dan disimpan di `output.txt`. File `ocr-debug.log` akan mengonfirmasi pemanfaatan GPU.

---

## Kesimpulan

Dalam tutorial ini kami menunjukkan **cara mengaktifkan GPU** untuk Aspose.OCR di Java, cara **mengenali teks gambar**, **mengekstrak teks JPG**, **cara menambahkan filter**, dan **cara mengatur bahasa**—semua dalam satu program mandiri. Dengan mengaktifkan GPU Anda mendapatkan peningkatan kecepatan yang signifikan, sementara filter dan pengaturan bahasa memastikan akurasi tinggi pada berbagai sumber gambar.

**Langkah selanjutnya**

* Bereksperimen dengan filter tambahan seperti `FilterType.BINARIZE` untuk dokumen yang dipindai.  
* Beralih ke bahasa lain (`OcrLanguage.SPANISH`, `OcrLanguage.CHINESE_SIMPLIFIED`) untuk memperluas dukungan multibahasa.  
* Gabungkan pipeline OCR ini dengan Apache PDFBox untuk mengekstrak teks langsung dari halaman PDF.  

Silakan sesuaikan kode untuk pemrosesan batch, integrasikan ke layanan Spring Boot, atau hubungkan ke antrian pesan untuk beban kerja OCR real‑time. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [How to Read Text from an Image in Java Using Aspose OCR – Complete Guide](/ocr/english/java/ocr-basics/read-text-from-image-in-java-complete-aspose-ocr-guide/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Preprocess Image OCR in Java with Aspose OCR – Boost Accuracy & Extract Text](/ocr/english/java/advanced-ocr-techniques/preprocess-image-ocr-in-java-boost-accuracy-extract-text/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}