---
category: general
date: 2026-06-16
description: Tutorial bounding box OCR dalam Java menunjukkan cara mengekstrak teks
  dari gambar, membaca teks dari gambar, dan mendapatkan skor kepercayaan OCR untuk
  file JPG.
draft: false
keywords:
- ocr bounding box
- extract text from image
- ocr confidence score
- recognize text from jpg
- read text from image
language: id
og_description: Kotak pembatas OCR dalam Java memungkinkan Anda mengenali teks dari
  file JPG, mengekstrak teks dari gambar, dan melihat skor kepercayaan OCR—semua dalam
  contoh kode sederhana.
og_title: Kotak Pembatas OCR dalam Java – Ekstrak Teks dari Gambar
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: OCR bounding box tutorial in Java shows how to extract text from image,
    read text from image, and get OCR confidence score for JPG files.
  headline: OCR Bounding Box in Java – Extract Text from Image
  type: TechArticle
tags:
- OCR
- Java
- image-processing
- text-recognition
title: Kotak Pembatas OCR di Java – Ekstrak Teks dari Gambar
url: /id/java/advanced-ocr-techniques/ocr-bounding-box-in-java-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR Bounding Box di Java – Ekstrak Teks dari Gambar

Pernah bertanya-tanya bagaimana cara mendapatkan **ocr bounding box** untuk setiap potongan teks dalam gambar Java? Dalam tutorial ini kami akan menunjukkan cara **extract text from image** file, **read text from image**, dan bahkan melihat **ocr confidence score** saat Anda **recognize text from jpg** file. Jawaban singkatnya? Beberapa baris kode menggunakan perpustakaan OCR modern, plus sedikit penjelasan mengapa setiap pemanggilan penting.

Di bawah ini Anda akan menemukan contoh lengkap yang siap dijalankan, penjelasan langkah demi langkah, dan beberapa tip praktis yang dapat Anda salin langsung ke proyek Anda. Pada akhir tutorial, Anda akan dapat menghasilkan output seperti berikut:

```
Text: "Hello World"  Confidence: 0.97  Box: (x=12, y=45, width=210, height=30)
```

## Apa yang Anda Butuhkan

- **Java 11** atau lebih baru (sintaks di bawah menggunakan keyword `var` untuk singkat, tetapi Anda dapat menghilangkannya untuk JDK lama).  
- Sebuah perpustakaan OCR yang menyediakan API Java – untuk panduan ini kami akan menggunakan **[Tesseract4J](https://github.com/nguyenq/tess4j)**, sebuah wrapper tipis di atas mesin Tesseract yang populer.  
- Gambar JPEG (`.jpg`) yang berisi teks cetak yang jelas.  
- IDE favorit Anda (IntelliJ IDEA, Eclipse, VS Code…) – apa saja dapat digunakan.

Jika Anda belum memiliki perpustakaan tersebut, cukup tambahkan dependensi Maven berikut:

```xml
<dependency>
    <groupId>net.sourceforge.tess4j</groupId>
    <artifactId>tess4j</artifactId>
    <version>5.4.0</version>
</dependency>
```

Sekarang mari kita mulai.

![OCR bounding box example](ocr-bounding-box.png "OCR bounding box example")

## OCR Bounding Box: Menyiapkan Engine

Hal pertama yang harus Anda lakukan adalah membuat instance engine OCR. Anggaplah ini seperti menyalakan pemindai yang nantinya akan membaca piksel.

```java
import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;

ITesseract ocrEngine = new Tesseract();          // Step 1 – create the OCR engine
ocrEngine.setDatapath("tessdata");               // point to the language data files
ocrEngine.setLanguage("eng");                    // we’ll work with English for now
```

**Mengapa ini penting:**  
Tanpa mengatur `datapath`, Tesseract tidak akan tahu di mana paket bahasa berada, dan Anda akan mendapatkan error “Failed loading language” yang membingungkan. Pemanggilan `setLanguage` bersifat opsional jika Anda hanya membutuhkan paket bahasa Inggris default, tetapi menjadi eksplisit membuat kode lebih jelas bagi pembaca di masa depan.

## Muat Gambar yang Ingin Anda Proses

Selanjutnya, berikan JPEG yang ingin Anda analisis ke engine. Perpustakaan menerima `File` atau `BufferedImage`; kami akan menggunakan `File` untuk kesederhanaan.

```java
import java.io.File;

File imageFile = new File("YOUR_DIRECTORY/text_page.jpg");   // Step 2 – load the image
```

**Tip pro:**  
Jika gambar Anda berada di resources (misalnya, di dalam JAR), gunakan `getResourceAsStream` dan bungkus dengan `ImageIO.read`. Dengan cara itu tutorial dapat berjalan baik secara lokal maupun dalam aplikasi yang dipaketkan.

## Lakukan Pengakuan OCR

Sekarang kami benar‑benar meminta engine untuk membaca gambar. Hasilnya adalah string teks biasa, tetapi kami juga menginginkan **ocr confidence score** dan **ocr bounding box** untuk setiap baris.

```java
try {
    // Step 3 – run OCR and get a result object with layout data
    var result = ocrEngine.doOCR(imageFile, null);
    // The simple doOCR call returns only text; to get boxes we need the
    // getWords method with a specific page iterator level.
    var words = ocrEngine.getWords(imageFile, ITesseract.PageIteratorLevel.RIL_WORD);
    
    // Step 4 – iterate over each detected word
    for (var word : words) {
        System.out.printf(
            "Text: \"%s\"  Confidence: %.2f  Box: %s%n",
            word.getText(),
            word.getConfidence(),
            word.getBoundingBox().toString()
        );
    }
} catch (TesseractException e) {
    System.err.println("OCR failed: " + e.getMessage());
}
```

**Mengapa kami menggunakan `getWords` alih-alih `doOCR` biasa:**  
`doOCR` memberikan Anda string mentah tetapi mengabaikan informasi spasial. Dengan memanggil `getWords` dengan `RIL_WORD` (atau `RIL_TEXTLINE` jika Anda lebih suka kotak tingkat baris), kami memperoleh daftar objek `Word` yang masing‑masing membawa teks, confidence, dan persegi panjang pembatas. Itulah inti dari fitur **ocr bounding box**.

## Memahami Output

Menjalankan potongan kode di atas pada JPEG yang bersih menghasilkan output serupa dengan:

```
Text: "Hello"  Confidence: 0.99  Box: java.awt.Rectangle[x=34,y=12,width=112,height=28]
Text: "World"  Confidence: 0.97  Box: java.awt.Rectangle[x=156,y=12,width=98,height=28]
```

- **Text** – karakter yang dikenali.  
- **Confidence** – nilai floating‑point antara 0 dan 1; semakin tinggi berarti engine lebih yakin.  
- **Box** – persegi panjang yang membatasi kata dalam koordinat piksel (x, y, lebar, tinggi).  

Sekarang Anda dapat **read text from image** dan juga mengetahui persis di mana setiap potongan berada di kanvas—sempurna untuk menyorot, memotong, atau memasukkannya ke dalam pipeline NLP selanjutnya.

## Kasus Tepi & Kesalahan Umum

| Situasi | Hal yang Perlu Diperhatikan | Perbaikan / Solusi |
|-----------|-------------------|-------------------|
| Gambar buram atau kontras rendah | Skor confidence turun drastis (sering di bawah 0.6). | Pra‑proses dengan OpenCV: tingkatkan kontras, terapkan thresholding. |
| JPEG berisi teks yang diputar | Kotak pembatas tampak miring atau hilang. | Gunakan `ocrEngine.setPageSegMode(ITesseract.PageSegMode.PSM_AUTO_OSD)` agar Tesseract mendeteksi orientasi secara otomatis. |
| Gambar besar menyebabkan OutOfMemoryError | Heap Java penuh saat memuat gambar besar. | Ukur ulang gambar sebelum OCR (`ImageIO.read` → `BufferedImage.getScaledInstance`). |
| Anda membutuhkan kotak tingkat baris bukan tingkat kata | `RIL_WORD` mengembalikan kotak per‑kata. | Beralih ke `ITesseract.PageIteratorLevel.RIL_TEXTLINE`. |
| Karakter non‑Inggris muncul sebagai � | Data bahasa tidak dimuat. | Unduh file `.traineddata` yang sesuai dan arahkan `setDatapath` ke foldernya. |

Menangani masalah ini lebih awal menghemat Anda berjam‑jam debugging di kemudian hari.

## Contoh Lengkap yang Berfungsi (Semua Langkah dalam Satu File)

Berikut adalah kelas Java mandiri yang dapat Anda salin‑tempel ke folder `src/main/java` dan jalankan dengan `mvn exec:java`. Kelas ini menggabungkan semua yang telah kami bahas.

```java
package com.example.ocrdemo;

import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.ITesseract.RenderedFormat;
import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;
import net.sourceforge.tess4j.Word;

import java.io.File;
import java.util.List;

public class OcrBoundingBoxDemo {

    public static void main(String[] args) {
        // ==== Step 1: Initialize the OCR engine ====
        ITesseract ocrEngine = new Tesseract();
        ocrEngine.setDatapath("tessdata"); // folder containing .traineddata files
        ocrEngine.setLanguage("eng");      // English language pack

        // Optional: improve accuracy for printed text
        ocrEngine.setPageSegMode(ITesseract.PageSegMode.PSM_AUTO);
        ocrEngine.setOcrEngineMode(ITesseract.OEM_TESSERACT_ONLY);

        // ==== Step 2: Load the JPEG you want to read ====
        File imageFile = new File("YOUR_DIRECTORY


## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Ekstrak Teks dari Gambar Java dengan Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Ekstrak Gambar Teks – Dasar OCR dengan Aspose.OCR untuk Java](/ocr/english/java/ocr-basics/)
- [Cara OCR Teks Gambar dengan Bahasa Menggunakan Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}