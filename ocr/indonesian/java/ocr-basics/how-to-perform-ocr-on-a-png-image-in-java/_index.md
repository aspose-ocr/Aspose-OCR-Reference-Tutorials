---
category: general
date: 2026-10-11
description: Pelajari cara melakukan OCR pada gambar PNG di Java, mengekstrak teks
  dari gambar, dan mengonversi gambar menjadi teks dengan contoh OcrEngine sederhana.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to perform OCR
- extract text from image
- recognize text from PNG
- load image java
- convert image to text
language: id
lastmod: 2026-10-11
og_description: Cara melakukan OCR pada gambar PNG di Java, mengekstrak teks dari
  gambar, dan mengonversi gambar menjadi teks menggunakan contoh singkat yang siap
  dijalankan.
og_image_alt: Diagram showing how to perform OCR on a PNG image using Java
og_title: Cara melakukan OCR pada gambar PNG di Java – panduan lengkap
schemas:
- author: Aspose
  dateModified: '2026-10-11'
  description: Learn how to perform OCR on a PNG image in Java, extract text from
    image and convert image to text with a simple OcrEngine example.
  headline: How to perform OCR on a PNG image in Java
  type: TechArticle
- description: Learn how to perform OCR on a PNG image in Java, extract text from
    image and convert image to text with a simple OcrEngine example.
  name: How to perform OCR on a PNG image in Java
  steps:
  - name: 4.1 Handling low‑resolution PNGs
    text: 'Tesseract performs best on images with at least 300 DPI. If your source
      PNG is smaller, upscale it before OCR:'
  - name: 4.2 Extracting non‑English text
    text: 'To **extract text from image** that contains other languages, download
      the appropriate `.traineddata` files and set the language code:'
  - name: 4.3 Batch processing multiple PNGs
    text: 'If you need to **recognize text from PNG** files in a folder, iterate over
      the directory:'
  - name: 4.4 Dealing with OCR errors
    text: 'Typical OCR mistakes include misreading `0` (zero) as `O` or `1` as `l`.
      Post‑processing with regular expressions can clean the result:'
  type: HowTo
tags:
- OCR
- Java
- Image Processing
- Text Extraction
title: Cara melakukan OCR pada gambar PNG di Java
url: /id/java/ocr-basics/how-to-perform-ocr-on-a-png-image-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara melakukan OCR pada gambar PNG di Java

Jika Anda perlu **perform OCR** pada file gambar, mempelajari **how to perform OCR** di Java sangat penting untuk banyak tugas otomatisasi. Baik Anda sedang mendigitalkan kwitansi, mengindeks dokumen yang dipindai, atau membangun arsip foto yang dapat dicari, kemampuan untuk **extract text from image** file menghemat banyak jam kerja manual.

Tutorial ini menunjukkan solusi lengkap yang dapat dijalankan yang memuat PNG, menjalankan mesin OCR, dan **recognize text from PNG** file. Anda juga akan melihat cara **convert image to text** dan menangani jebakan umum seperti input beresolusi rendah atau karakter non‑ASCII.

## Apa yang akan Anda capai

* kode **load image java** yang membaca PNG dari disk,
* inisialisasi mesin OCR ringan,
* **extract text from image** dan mencetak hasilnya ke konsol,
* menyesuaikan solusi untuk format gambar lain atau pemrosesan batch.

Tidak diperlukan layanan eksternal—hanya satu pustaka OCR sumber terbuka (Tess4J) dan runtime Java SE.

---

## Prasyarat

* Java 17 atau lebih baru (kode ini dikompilasi dengan JDK 17).
* Maven atau Gradle untuk manajemen dependensi.
* Familiaritas dasar dengan baris perintah dan IDE pilihan Anda.
* Pustaka `tess4j` (wrapper Java untuk Tesseract). Tambahkan dependensi Maven berikut:

```xml
<dependency>
    <groupId>net.sourceforge.tess4j</groupId>
    <artifactId>tess4j</artifactId>
    <version>5.4.0</version>
</dependency>
```

Jika Anda menggunakan Gradle, setaraannya adalah:

```gradle
implementation 'net.sourceforge.tess4j:tess4j:5.4.0'
```

Anda juga memerlukan file data Tesseract (`.traineddata`). Unduh paket data bahasa Inggris dari repositori resmi dan letakkan di folder bernama `tessdata` di root proyek.

## Langkah 1: Memuat gambar di Java

Memuat PNG sangat mudah dengan kelas standar `ImageIO`. Kode di bawah ini menunjukkan **load image java** dengan cara yang aman dan memperhatikan pengecualian:

```java
import java.awt.image.BufferedImage;
import java.io.File;
import javax.imageio.ImageIO;

/**
 * Reads a PNG file from the given path and returns a BufferedImage.
 *
 * @param path absolute or relative path to the PNG file
 * @return BufferedImage representation of the file
 * @throws Exception if the file cannot be read or is not a PNG
 */
private static BufferedImage loadPng(String path) throws Exception {
    File imgFile = new File(path);
    if (!imgFile.exists()) {
        throw new IllegalArgumentException("File not found: " + path);
    }
    BufferedImage img = ImageIO.read(imgFile);
    if (img == null) {
        throw new IllegalArgumentException("Unsupported image format or corrupt file: " + path);
    }
    return img;
}
```

**Mengapa ini penting:** `ImageIO.read` secara otomatis mendeteksi format gambar, tetapi kami secara eksplisit memeriksa `null` untuk menghindari kegagalan diam ketika PNG rusak. Pola ini merupakan praktik terbaik saat Anda **load image java** untuk OCR.

## Langkah 2: Inisialisasi mesin OCR

Tess4J membungkus binary native Tesseract, menyediakan API Java yang sederhana. Metode berikut membuat instance `Tesseract`, menunjuk ke folder `tessdata`, dan mengatur bahasa ke English:

```java
import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.Tesseract;

/**
 * Configures and returns a ready‑to‑use Tesseract instance.
 *
 * @return configured ITesseract object
 */
private static ITesseract createOcrEngine() {
    ITesseract tesseract = new Tesseract();
    // Path to the folder that contains .traineddata files
    tesseract.setDatapath("tessdata");
    // Language code – "eng" for English; you can add more languages later
    tesseract.setLanguage("eng");
    // Optional: increase OCR accuracy for PNGs with low DPI
    tesseract.setOcrEngineMode(ITesseract.OEM_DEFAULT);
    return tesseract;
}
```

**Mengapa kami melakukan ini:** Menginisialisasi mesin sekali dan menggunakannya kembali untuk beberapa gambar mengurangi overhead startup. Pemanggilan `setOcrEngineMode` memilih mode default, yang bekerja baik untuk kebanyakan PNG. Jika Anda menemukan pemindaian yang berisik, Anda dapat bereksperimen dengan mode lain (mis., `OEM_LSTM_ONLY`).

## Langkah 3: Lakukan OCR dan **recognize text from PNG**

Sekarang kami menggabungkan pemuat gambar dan mesin OCR. Metode di bawah ini menjalankan OCR pada `BufferedImage` dan mengembalikan string yang diekstrak:

```java
/**
 * Runs OCR on the supplied image and returns the recognized text.
 *
 * @param image BufferedImage containing the PNG to process
 * @param tesseract configured OCR engine
 * @return plain‑text result of OCR
 * @throws Exception if OCR fails
 */
private static String extractText(BufferedImage image, ITesseract tesseract) throws Exception {
    // Tess4J can directly accept a BufferedImage
    return tesseract.doOCR(image);
}
```

**Contoh lengkap yang dapat dijalankan**

```java
import java.awt.image.BufferedImage;
import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.TesseractException;

public class OcrDemo {

    public static void main(String[] args) {
        try {
            // 1️⃣ Load the PNG file
            BufferedImage image = loadPng("sample.png");

            // 2️⃣ Create and configure the OCR engine
            ITesseract ocrEngine = createOcrEngine();

            // 3️⃣ Recognize text from PNG
            String recognizedText = extractText(image, ocrEngine);

            // 4️⃣ Display the result – this is the **convert image to text** step
            System.out.println("=== OCR RESULT ===");
            System.out.println(recognizedText);
        } catch (Exception e) {
            System.err.println("Error during OCR processing:");
            e.printStackTrace();
        }
    }

    // ----- Helper methods from previous steps -----
    // loadPng, createOcrEngine, extractText (copy-pasted here for completeness)
    // ... (methods omitted for brevity; see the sections above) ...
}
```

**Output yang diharapkan**

```
=== OCR RESULT ===
Invoice #12345
Date: 2024‑09‑30
Total: $1,234.56
Thank you for your business!
```

Konsol akan menampilkan karakter tepat yang diekstrak mesin dari `sample.png`. Jika PNG hanya berisi satu kata, output akan menjadi kata tersebut diikuti newline.

## Langkah 4: Variasi umum dan kasus tepi

### 4.1 Menangani PNG beresolusi rendah

Tesseract bekerja paling baik pada gambar dengan setidaknya 300 DPI. Jika PNG sumber Anda lebih kecil, tingkatkan ukurannya sebelum OCR:

```java
import java.awt.Graphics2D;
import java.awt.Image;
import java.awt.RenderingHints;

private static BufferedImage upscale(BufferedImage src, int scaleFactor) {
    int width = src.getWidth() * scaleFactor;
    int height = src.getHeight() * scaleFactor;
    Image tmp = src.getScaledInstance(width, height, Image.SCALE_SMOOTH);
    BufferedImage resized = new BufferedImage(width, height, BufferedImage.TYPE_INT_ARGB);
    Graphics2D g2d = resized.createGraphics();
    g2d.setRenderingHint(RenderingHints.KEY_INTERPOLATION,
                         RenderingHints.VALUE_INTERPOLATION_BICUBIC);
    g2d.drawImage(tmp, 0, 0, null);
    g2d.dispose();
    return resized;
}
```

Terapkan `upscale(image, 2)` sebelum memanggil `extractText` untuk meningkatkan akurasi.

### 4.2 Mengekstrak teks non‑English

Untuk **extract text from image** yang berisi bahasa lain, unduh file `.traineddata` yang sesuai dan atur kode bahasa:

```java
tesseract.setLanguage("eng+deu"); // English + German
```

### 4.3 Pemrosesan batch banyak PNG

Jika Anda perlu **recognize text from PNG** file dalam sebuah folder, iterasi melalui direktori:

```java
File folder = new File("pngs/");
for (File file : folder.listFiles((d, name) -> name.toLowerCase().endsWith(".png"))) {
    BufferedImage img = loadPng(file.getPath());
    String text = extractText(img, ocrEngine);
    System.out.println("File: " + file.getName());
    System.out.println(text);
}
```

### 4.4 Menangani kesalahan OCR

Kesalahan OCR umum meliputi membaca `0` (nol) sebagai `O` atau `1` sebagai `l`. Pemrosesan lanjutan dengan ekspresi reguler dapat membersihkan hasil:

```java
String cleaned = recognizedText.replaceAll("[\\r\\n]+", " ").trim();
```

## Tips profesional untuk OCR yang andal di Java

| Tip | Reason |
|-----|--------|
| **Use a lossless PNG** | Artefak kompresi pada JPEG dapat membingungkan mesin. |
| **Trim white borders** | Whitespace berlebih meningkatkan waktu pemrosesan dan dapat menyebabkan positif palsu. |
| **Set `tesseract.setPageSegMode(ITesseract.PSM_AUTO)`** only when layout is unknown; otherwise choose a specific mode (e.g., `PSM_SINGLE_BLOCK`). | |
| **Cache the `ITesseract` instance** | |

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Cara Membaca Teks dari Gambar di Java Menggunakan Aspose OCR – Panduan Lengkap](/ocr/english/java/ocr-basics/read-text-from-image-in-java-complete-aspose-ocr-guide/)
- [Cara Menggunakan OCR di Java – Mengenali Teks dari Gambar dengan Cepat](/ocr/english/java/ocr-operations/how-to-use-ocr-in-java-recognize-text-from-image-quickly/)
- [OCR Gambar Batch di Java – Ekstrak Teks dari File PNG dengan Cepat](/ocr/english/java/ocr-operations/batch-image-ocr-in-java-extract-text-from-png-files-fast/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}