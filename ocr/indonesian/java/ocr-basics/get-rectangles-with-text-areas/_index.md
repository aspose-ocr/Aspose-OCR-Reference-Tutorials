---
date: 2026-06-19
description: Pelajari cara mengonversi gambar ke teks dalam Java, mengekstrak paragraf
  dari gambar, dan mengambil persegi panjang area teks menggunakan Aspose OCR Java
  library.
keywords:
- image to text java
- convert scanned image text
- extract paragraphs from image
- aspose ocr java tutorial
linktitle: Image to Text Java – Mengenali Teks dari Gambar dan Mengambil Persegi Panjang
  Area Teks
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Learn how to convert image to text in Java, extract paragraphs from
    image, and retrieve text area rectangles using Aspose OCR Java library.
  headline: Image to Text Java – Convert Image to Text and Retrieve Text Area Rectangles
  type: TechArticle
- description: Learn how to convert image to text in Java, extract paragraphs from
    image, and retrieve text area rectangles using Aspose OCR Java library.
  name: Image to Text Java – Convert Image to Text and Retrieve Text Area Rectangles
  steps:
  - name: Set Up Your Project
    text: Create a new Java project (or add to an existing one) and place the Aspose.OCR
      JAR on the classpath. If you use Maven, add the dependency as described in the
      download package.
  - name: Define Document Directory and Image Path
    text: 'Specify where your sample image resides:'
  - name: Create AsposeOCR Instance
    text: '`AsposeOCR` is the main class that provides OCR functionality. Instantiate
      the OCR engine:'
  - name: Recognize Text in the Image
    text: Load your image and call `RecognizePage` to convert the picture into plain
      text. This single method call performs image preprocessing, character segmentation,
      and language‑specific recognition in one step.
  - name: Get Rectangles with Text Areas
    text: Retrieve the bounding rectangles for each paragraph (or other area types).
      This step returns a collection of `Rectangle` objects that precisely enclose
      the detected text blocks, enabling you to highlight or further process individual
      sections. CODE_BLOCK_PLACEHOLDER_5_END
  type: HowTo
- questions:
  - answer: Yes, Aspose.OCR works with Java 11 and later versions.
    question: Is Aspose.OCR compatible with Java 11?
  - answer: Yes, you can use it in any type of project. For licensing details, visit
      [here](https://purchase.aspose.com/buy).
    question: Can I use Aspose.OCR for both personal and commercial projects?
  - answer: You can obtain a temporary license [here](https://purchase.aspose.com/temporary-license/).
    question: How do I obtain a temporary license for evaluation?
  - answer: For support and discussions, visit the [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16).
    question: Where can I find community support or official assistance?
  - answer: Yes, the library is thread‑safe and can be used in concurrent environments
      for better performance.
    question: Does Aspose.OCR support multithreading?
  type: FAQPage
second_title: Aspose.OCR Java API
title: Image to Text Java – Mengonversi Gambar ke Teks dan Mengambil Persegi Panjang
  Area Teks
url: /id/java/ocr-basics/get-rectangles-with-text-areas/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Gambar ke Teks Java – Mengonversi Gambar ke Teks dan Mengambil Persegi Panjang Area Teks

## Pendahuluan

Jika Anda perlu **convert image to text** dalam aplikasi Java, Aspose.OCR untuk Java menyediakan solusi yang cepat dan akurat. Dalam tutorial ini kami akan menjelaskan langkah‑langkah tepat yang diperlukan untuk mengekstrak paragraf dari sebuah gambar, memperoleh persegi panjang pembatas untuk setiap area teks, dan mencetak koordinat tersebut ke konsol. Pada akhir tutorial Anda akan memahami mengapa pendekatan ini berhasil, cara mengintegrasikan perpustakaan, dan di mana Anda dapat memperluasnya untuk kasus penggunaan Anda sendiri.

## Jawaban Cepat

`AreasType` adalah enumerasi yang menentukan tingkat segmentasi teks (kata, baris, paragraf).

- **Apa arti “recognize text from image”?** Artinya mengonversi karakter visual dalam sebuah gambar menjadi data string yang dapat diedit.  
- **Perpustakaan mana yang menangani ini di Java?** Aspose.OCR untuk Java.  
- **Apakah saya memerlukan lisensi untuk pengembangan?** Lisensi sementara tersedia untuk pengujian; lisensi penuh diperlukan untuk produksi.  
- **Bisakah saya mengekstrak paragraf alih‑alih kata tunggal?** Ya – gunakan `AreasType.PARAGRAPHS` untuk mendapatkan persegi panjang tingkat paragraf.  
- **Apakah kode ini kompatibel dengan Java 11+?** Tentu saja, API bekerja dengan Java 11 dan versi selanjutnya.

## Apa itu “convert image to text” dalam Aspose.OCR?

`convert image to text` mengacu pada proses menganalisis bitmap, menerapkan algoritma OCR, dan mengembalikan karakter yang dikenali sebagai string. Metode `RecognizePage` milik Aspose.OCR melakukan konversi ini sambil secara opsional menyediakan koordinat `Rectangle` yang tepat untuk setiap blok teks yang terdeteksi.

## Mengapa menggunakan **java ocr library** ini?

Aspose.OCR mendukung **30+ bahasa** dan dapat memproses gambar hingga **50 MB** tanpa memuat seluruh file ke memori, memberikan waktu respons sub‑detik pada perangkat keras server tipikal. Perpustakaan ini thread‑safe, hanya memerlukan satu JAR, dan menawarkan format output yang fleksibel—termasuk teks mentah, HTML, dan persegi panjang area teks yang tepat—menjadikannya ideal untuk skenario perusahaan dengan throughput tinggi.

## Prasyarat

- **Java Development Kit** (JDK 11 atau lebih baru) terpasang di mesin Anda.  
- **Aspose.OCR for Java** library – download dari situs resmi [here](https://releases.aspose.com/ocr/java/).  
- Sebuah IDE atau alat build (Maven/Gradle) untuk mengelola dependensi JAR.

## Impor Paket

Dalam proyek Java Anda, impor kelas‑kelas yang diperlukan:

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AreasType;
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

## Panduan Langkah‑per‑Langkah

### Langkah 1: Siapkan Proyek Anda
Buat proyek Java baru (atau tambahkan ke proyek yang sudah ada) dan letakkan JAR Aspose.OCR pada classpath. Jika Anda menggunakan Maven, tambahkan dependensi seperti yang dijelaskan dalam paket unduhan.

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";

// The image path
String imagePath = dataDir + "p3.png";
```

### Langkah 2: Tentukan Direktori Dokumen dan Jalur Gambar
Tentukan di mana gambar contoh Anda berada:

```java
// Create AsposeOCR instance
AsposeOCR api = new AsposeOCR();
```

### Langkah 3: Buat Instance AsposeOCR
`AsposeOCR` adalah kelas utama yang menyediakan fungsionalitas OCR.

Instansiasi mesin OCR:

```java
try {
    // Recognize page by full path to file
    String result = api.RecognizePage(imagePath);
    System.out.println("Result: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

### Langkah 4: Kenali Teks dalam Gambar
Muat gambar Anda dan panggil `RecognizePage` untuk mengonversi gambar menjadi teks biasa. Pemanggilan metode tunggal ini melakukan pra‑pemrosesan gambar, segmentasi karakter, dan pengenalan bahasa secara spesifik dalam satu langkah.

```java
// Get rectangles with text areas in the image.
ArrayList<Rectangle> rectResult = api.getTextAreas(imagePath, AreasType.PARAGRAPHS, true);

// Print each text area rectangle
for (Rectangle r : rectResult) {
    System.out.println("Text area:" + r);
}
```

### Langkah 5: Dapatkan Persegi Panjang dengan Area Teks
Ambil persegi panjang pembatas untuk setiap paragraf (atau tipe area lainnya). Langkah ini mengembalikan koleksi objek `Rectangle` yang secara tepat melingkupi blok teks yang terdeteksi, memungkinkan Anda menyorot atau memproses lebih lanjut bagian‑bagian individual.

CODE_BLOCK_PLACEHOLDER_5_END

## Masalah Umum & Pemecahan Masalah

| Gejala | Penyebab Kemungkinan | Solusi |
|--------|----------------------|--------|
| `IOException` pada `RecognizePage` | Jalur file tidak tepat atau izin baca tidak ada | Verifikasi bahwa `imagePath` mengarah ke PNG/JPG yang ada dan aplikasi memiliki akses sistem file. |
| String hasil kosong | Gambar berkualitas rendah atau bahasa tidak didukung | Pra‑proses gambar (tingkatkan kontras, binarisasi) atau tentukan bahasa yang tepat menggunakan `api.setLanguage("eng")`. |
| Tidak ada persegi panjang yang dikembalikan | Menggunakan `AreasType` yang salah (misalnya `WORDS` ketika mengharapkan paragraf) | Ganti ke `AreasType.PARAGRAPHS` atau `AreasType.LINES` sesuai kebutuhan. |

## Pertanyaan yang Sering Diajukan

**Q: Apakah Aspose.OCR kompatibel dengan Java 11?**  
A: Ya, Aspose.OCR bekerja dengan Java 11 dan versi selanjutnya.

**Q: Bisakah saya menggunakan Aspose.OCR untuk proyek pribadi maupun komersial?**  
A: Ya, Anda dapat menggunakannya dalam jenis proyek apa pun. Untuk detail lisensi, kunjungi [here](https://purchase.aspose.com/buy).

**Q: Bagaimana cara mendapatkan lisensi sementara untuk evaluasi?**  
A: Anda dapat memperoleh lisensi sementara [here](https://purchase.aspose.com/temporary-license/).

**Q: Di mana saya dapat menemukan dukungan komunitas atau bantuan resmi?**  
A: Untuk dukungan dan diskusi, kunjungi [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16).

**Q: Apakah Aspose.OCR mendukung multithreading?**  
A: Ya, perpustakaan ini thread‑safe dan dapat digunakan dalam lingkungan bersamaan untuk kinerja yang lebih baik.

## Kesimpulan

Dalam **aspose ocr java tutorial** ini Anda belajar cara **convert image to text** menggunakan Aspose.OCR untuk Java, mengekstrak paragraf, dan mengambil persegi panjang yang tepat yang mengelilingi setiap blok teks. Kemampuan ini memungkinkan Anda membangun PDF yang dapat dicari, menyorot teks dalam overlay UI, atau memasukkan data terstruktur ke proses hilir. Jelajahi API lebih lanjut untuk menyesuaikan pengaturan bahasa, menangani format gambar berbeda, atau mengintegrasikan dengan penyimpanan cloud.

---

**Terakhir Diperbarui:** 2026-06-19  
**Diuji Dengan:** Aspose.OCR 23.10 untuk Java  
**Penulis:** Aspose  

{{< blocks/products/products-backtop-button >}}

## Tutorial Terkait

- [Ekstrak Gambar Teks – Dasar OCR dengan Aspose.OCR untuk Java](/ocr/java/ocr-basics/)
- [Ekstrak Teks dari Gambar Java dengan Mode Deteksi Area Aspose.OCR](/ocr/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Konversi Gambar ke Teks di Java menggunakan Aspose.OCR BufferedImage](/ocr/java/advanced-ocr-techniques/perform-ocr-buffered-image/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}