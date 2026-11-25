---
category: general
date: 2026-05-06
description: Cara menggunakan Aspose OCR untuk mengenali teks dari gambar, mengaktifkan
  deteksi bahasa otomatis, dan meningkatkan kecepatan OCR di Java.
draft: false
keywords:
- how to use aspose
- recognize text from image
- improve ocr speed
- load image for ocr
- enable automatic language detection
language: id
og_description: Cara menggunakan Aspose OCR untuk dengan cepat mengenali teks dari
  gambar, mengaktifkan deteksi bahasa otomatis, dan meningkatkan kecepatan OCR di
  Java.
og_title: Cara Menggunakan Aspose OCR untuk Gambar Berbahasa Campuran
tags:
- Aspose
- OCR
- Java
- Image Processing
title: Cara Menggunakan Aspose OCR untuk Gambar Campuran Bahasa
url: /id/java/advanced-ocr-techniques/how-to-use-aspose-ocr-for-mixed-language-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menggunakan Aspose OCR untuk Gambar Campuran Bahasa

Pernah bertanya-tanya **how to use Aspose** untuk mengambil teks dari gambar yang berisi beberapa bahasa sekaligus? Anda tidak sendirian—para pengembang sering menemui kendala ketika sebuah gambar mencampur bahasa Inggris, Rusia, Hindi, atau skrip lainnya. Kabar baiknya, Aspose OCR menangani hal ini dengan baik, dan Anda bahkan dapat **recognize text from image** lebih cepat dengan mempersempit set bahasa.

Dalam tutorial ini kami akan menelusuri contoh Java lengkap yang siap‑jalankan yang **loads image for OCR**, mengaktifkan **automatic language detection**, dan menunjukkan trik sederhana untuk **improve OCR speed**. Pada akhir tutorial Anda akan memiliki program mandiri yang mencetak teks yang diekstrak ke konsol, dan Anda akan memahami mengapa setiap pengaturan penting.

> **Prasyarat** – Java 17+ terinstal, Maven atau Gradle untuk manajemen dependensi, dan lisensi Aspose OCR (versi percobaan gratis dapat digunakan untuk evaluasi). Tidak ada pustaka lain yang diperlukan.

---

## Langkah 1 – Tambahkan Aspose OCR ke Proyek Anda

Sebelum Anda dapat **use Aspose**, Anda memerlukan pustaka tersebut di classpath Anda. Dengan Maven tampilannya seperti ini:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- check for the latest version -->
</dependency>
```

Jika Anda lebih suka Gradle:

```groovy
implementation 'com.aspose:aspose-ocr:23.12'
```

> **Pro tip:** Tetap gunakan rilis stabil terbaru; versi yang lebih baru sering menyertakan perbaikan kinerja yang secara langsung memengaruhi **improve OCR speed**.

---

## Langkah 2 – Buat Instance OCR Engine  

Inti dari setiap alur kerja Aspose OCR adalah `OcrEngine`. Membuat instance-nya sederhana, namun perlu dicatat bahwa engine menyimpan cache internal. Menggunakan kembali satu instance untuk banyak gambar sebenarnya dapat **improve OCR speed** karena pustaka menghindari inisialisasi native berulang.

```java
import com.aspose.ocr.*;

public class MixedLanguageDemo {
    public static void main(String[] args) throws Exception {
        // Step 2: Initialise the OCR engine – one instance per application is ideal
        OcrEngine ocrEngine = new OcrEngine();
```

---

## Langkah 3 – **Load Image for OCR**  

Aspose menerima banyak format gambar (PNG, JPEG, TIFF, BMP). Di sini kami mendemonstrasikan pemuatan PNG yang berisi teks bahasa Inggris, Rusia, dan Hindi. Helper `ImageStream.fromFile` mengabstraksi detail file‑I/O dan memastikan gambar dialirkan dengan benar ke engine.

```java
        // Step 3: Load the picture that holds mixed languages
        // Replace the path with the actual location of your image file
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/mixed-lang.png"));
```

> **Bagaimana jika gambar berada di memori?** Gunakan `ImageStream.fromByteArray(byte[])` sebagai gantinya—sempurna untuk layanan web yang menerima gambar sebagai aliran byte.

---

## Langkah 4 – Aktifkan Deteksi Bahasa Otomatis  

Secara default Aspose OCR mengasumsikan satu bahasa, yang dapat menghasilkan output berantakan pada gambar multibahasa. Mengaktifkan deteksi otomatis memberi tahu engine untuk mendeteksi skrip setiap blok teks sebelum pengenalan.

```java
        // Step 4: Turn on auto‑detect – this is the key to handling mixed‑language images
        ocrEngine.getSettings().setAutoDetectLanguage(true);
```

---

## Langkah 5 – **Improve OCR Speed** dengan Membatasi Pool Bahasa  

Deteksi otomatis penuh memindai semua bahasa yang didukung Aspose (lebih dari 70). Jika Anda mengetahui bahasa yang mungkin sebelumnya, Anda dapat memberi petunjuk kepada engine. Menyediakan array yang lebih kecil mengurangi ruang pencarian dan oleh karena itu **improves OCR speed**.

```java
        // Step 5 (optional but recommended): Limit detection to known languages
        // "en" = English, "ru" = Russian, "hi" = Hindi
        ocrEngine.getSettings().setPossibleLanguages(new String[] { "en", "ru", "hi" });
```

> **Mengapa ini membantu?** Engine melewatkan model bahasa yang tidak diperlukan, menghemat siklus CPU dan memori. Jika Anda kemudian menambahkan lebih banyak bahasa, cukup perbarui array—tanpa perlu menulis ulang kode.

---

## Langkah 6 – Lakukan Pengakuan dan **Recognize Text from Image**

Sekarang proses berat terjadi. `recognize()` mengembalikan objek `OcrResult` yang berisi teks polos, skor kepercayaan, dan bahkan informasi tata letak jika Anda membutuhkannya nanti.

```java
        // Step 6: Run the OCR process
        OcrResult ocrResult = ocrEngine.recognize();

        // Step 7: Output the recognized text to the console
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

### Output Konsol yang Diharapkan

```
=== Extracted Text ===
Hello world!
Привет мир!
नमस्ते दुनिया!
```

Jika gambar mengandung noise tambahan atau teks yang miring, Anda mungkin melihat kepercayaan yang lebih rendah untuk baris tersebut. Dalam kasus itu, pertimbangkan pra‑pemrosesan gambar (deskew, binarisasi) sebelum memberikannya ke Aspose.

---

## Pertanyaan Umum & Kasus Tepi

### Bagaimana jika gambar sangat besar (mis., >10 MP)?

Gambar besar mengonsumsi lebih banyak memori dan dapat memperlambat pemrosesan. Cara cepat untuk **improve OCR speed** adalah menurunkan skala gambar sambil mempertahankan keterbacaan:

```java
// Example using java.awt for simple resizing (optional)
BufferedImage original = ImageIO.read(new File("large.png"));
int targetWidth = 2000; // adjust based on your needs
BufferedImage resized = new BufferedImage(targetWidth,
        (original.getHeight() * targetWidth) / original.getWidth(),
        BufferedImage.TYPE_INT_RGB);
Graphics2D g = resized.createGraphics();
g.drawImage(original, 0, 0, targetWidth, resized.getHeight(), null);
g.dispose();
ocrEngine.setImage(ImageStream.fromImage(resized));
```

### Bagaimana saya menangani skrip kanan‑ke‑kiri seperti Arab?

Aspose OCR secara otomatis menghormati arah skrip, tetapi Anda mungkin ingin mengatur flag `RightToLeft` untuk pasca‑pemrosesan:

```java
ocrEngine.getSettings().setRightToLeft(true);
```

### Bisakah saya mengekstrak teks dari PDF alih-alih gambar?

Ya—konversi setiap halaman PDF menjadi gambar (menggunakan Aspose PDF atau rasterizer apa pun) dan berikan hasilnya ke pipeline OCR yang sama. Logika **recognize text from image** yang sama berlaku.

---

## Contoh Lengkap yang Berfungsi (Siap Salin‑Tempel)

```java
import com.aspose.ocr.*;
import java.io.File;

/**
 * Demonstrates how to use Aspose OCR to recognize text from an image
 * that contains multiple languages, with automatic language detection
 * and a speed‑optimising language whitelist.
 */
public class MixedLanguageDemo {
    public static void main(String[] args) throws Exception {
        // Initialise the OCR engine – reuse this instance for many images
        OcrEngine ocrEngine = new OcrEngine();

        // Load the image that holds mixed languages (replace with your path)
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/mixed-lang.png"));

        // Enable automatic detection of language per text block
        ocrEngine.getSettings().setAutoDetectLanguage(true);

        // OPTIONAL: Restrict detection to English, Russian, and Hindi to boost speed
        ocrEngine.getSettings().setPossibleLanguages(new String[] { "en", "ru", "hi" });

        // Run OCR and capture the result
        OcrResult ocrResult = ocrEngine.recognize();

        // Print the extracted text
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

Simpan file sebagai `MixedLanguageDemo.java`, kompilasi dengan `javac`, dan jalankan dengan `java MixedLanguageDemo`. Jika semuanya telah diatur dengan benar, Anda akan melihat teks multibahasa dicetak ke konsol.

---

## Kesimpulan

Anda sekarang tahu **how to use Aspose** untuk **recognize text from image** file yang berisi beberapa bahasa, cara **enable automatic language detection**, dan tip praktis untuk **improve OCR speed** dengan membatasi pool bahasa. Kode lengkap di atas siap untuk disalin‑tempel, dan penjelasannya seharusnya memberi Anda kepercayaan untuk menyesuaikan solusi—apakah Anda perlu **load image for OCR** dari aliran, array byte, atau bahkan snapshot webcam.

Langkah selanjutnya? Cobalah bereksperimen dengan:

* Menambahkan pra‑pemrosesan gambar (menghilangkan noise, binarisasi) untuk pemindaian kualitas rendah.  
* Mengekspor `OcrResult` sebagai JSON untuk layanan hilir.  
* Mengintegrasikan engine ke endpoint REST Spring Boot sehingga klien dapat mengunggah gambar dan menerima teks yang diekstrak secara instan.

Selamat coding, semoga pipeline OCR Anda cepat, akurat, dan multibahasa!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}