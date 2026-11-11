---
category: general
date: 2026-09-10
description: Lakukan OCR pada gambar menggunakan Aspose OCR Java. Pelajari cara mengenali
  teks dari JPEG, mengekstrak teks dari gambar, dan mengonversi gambar menjadi teks
  secara efisien.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- perform OCR on image
- recognize text from JPEG
- extract text from image
- convert image to text
- load image for OCR
language: id
lastmod: 2026-09-10
og_description: Lakukan OCR pada gambar dengan Aspose OCR Java. Tutorial ini menunjukkan
  cara mengenali teks dari JPEG, mengekstrak teks dari gambar, dan mengonversi gambar
  menjadi teks dalam beberapa baris kode.
og_image_alt: Screenshot of Java code that performs OCR on an image using Aspose OCR
og_title: Lakukan OCR pada gambar dengan Aspose OCR – Panduan Java
schemas:
- author: Aspose
  dateModified: '2026-09-10'
  description: perform OCR on image using Aspose OCR Java. Learn to recognize text
    from JPEG, extract text from image, and convert image to text efficiently.
  headline: How to perform OCR on image with Aspose OCR in Java
  type: TechArticle
- description: perform OCR on image using Aspose OCR Java. Learn to recognize text
    from JPEG, extract text from image, and convert image to text efficiently.
  name: How to perform OCR on image with Aspose OCR in Java
  steps:
  - name: Prerequisites
    text: '* Java Development Kit (JDK) 8 or later. * Maven or Gradle to manage dependencies
      (the example uses Maven). * A valid Aspose OCR for Java license (or a temporary
      evaluation key). * An image file named `sample.jpg` placed in a known directory.'
  - name: Load image for OCR
    text: '```java // Step 1: Load the image you want to process String imagePath
      = "YOUR_DIRECTORY/sample.jpg"; ImageStream imageStream = ImageStream.fromFile(imagePath);
      ```'
  - name: Create and configure the OCR engine
    text: '```java // Step 2: Create an OCR engine instance OcrEngine engine = new
      OcrEngine();'
  - name: Recognize text from JPEG
    text: '```java // Step 3: Attach the image to the engine engine.setImage(imageStream);'
  - name: Extract text from image and output
    text: '```java // Step 5: Output the recognized text System.out.println("=== Recognized
      Text ==="); System.out.println(result.getText()); ```'
  - name: Expected output
    text: 'Assuming `sample.jpg` contains the text “Hello World”, the console will
      display:'
  type: HowTo
tags:
- OCR
- Java
- Aspose
title: Cara melakukan OCR pada gambar dengan Aspose OCR di Java
url: /id/java/ocr-operations/how-to-perform-ocr-on-image-with-aspose-ocr-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara melakukan OCR pada gambar dengan Aspose OCR di Java

Jika Anda perlu **melakukan OCR pada gambar** dalam aplikasi Java, panduan ini menyediakan solusi lengkap yang siap dijalankan. Anda akan melihat cara **mengenali teks dari file JPEG**, **mengekstrak teks dari data gambar**, dan **mengonversi gambar menjadi teks** menggunakan API modern Aspose OCR.

Tutorial ini menjelaskan setiap langkah yang diperlukan—dari memuat gambar hingga mencetak teks yang dikenali—sehingga Anda dapat mengintegrasikan fungsi OCR tanpa mencari sumber tambahan. Tidak ada alat eksternal yang diperlukan selain pustaka Aspose OCR untuk Java.

## Apa yang akan Anda capai

* **Muat gambar untuk OCR** langsung dari sistem file.  
* Aktifkan preprocessing Aspose OCR (misalnya, denoising) untuk meningkatkan akurasi.  
* **Mengenali teks dari JPEG** dan format raster lainnya.  
* **Ekstrak teks dari gambar** dan keluarkan ke konsol.  
* Pahami cara **mengonversi gambar menjadi teks** dalam contoh kode siap produksi.

### Prasyarat

* Java Development Kit (JDK) 8 atau yang lebih baru.  
* Maven atau Gradle untuk mengelola dependensi (contoh menggunakan Maven).  
* Lisensi Aspose OCR untuk Java yang valid (atau kunci evaluasi sementara).  
* File gambar bernama `sample.jpg` ditempatkan di direktori yang diketahui.

> **Pro tip:** Gunakan JPEG beresolusi tinggi (300 dpi atau lebih) untuk tingkat pengenalan terbaik.  

## Langkah 1: Tambahkan Aspose OCR ke proyek Anda

Jika Anda mengelola dependensi dengan Maven, sisipkan potongan kode berikut ke dalam `pom.xml` Anda:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version>
</dependency>
```

Untuk Gradle, tambahkan:

```gradle
implementation 'com.aspose:aspose-ocr:23.12'
```

Koordinat ini mengambil pustaka Aspose OCR stabil terbaru, yang mencakup fitur preprocessing yang digunakan nanti.

## Lakukan OCR pada gambar – langkah demi langkah

Bagian berikut memecah program lengkap. Setiap blok adalah potongan mandiri yang dapat Anda salin, tempel, dan jalankan.

### Muat gambar untuk OCR

```java
// Step 1: Load the image you want to process
String imagePath = "YOUR_DIRECTORY/sample.jpg";
ImageStream imageStream = ImageStream.fromFile(imagePath);
```

*Mengapa ini penting:*  
`ImageStream.fromFile` membaca byte mentah JPEG dan menyiapkannya untuk mesin OCR. Metode ini bekerja dengan format raster apa pun yang didukung oleh Aspose OCR, sehingga Anda dapat mengganti JPEG dengan PNG atau BMP tanpa mengubah kode.

### Buat dan konfigurasikan mesin OCR

```java
// Step 2: Create an OCR engine instance
OcrEngine engine = new OcrEngine();

// Enable preprocessing to improve accuracy (e.g., denoising)
engine.getPreprocessing().setDenoise(true);
```

*Mengapa ini penting:*  
Membuat instance `OcrEngine` mengalokasikan mesin pengenalan inti. Mengaktifkan flag **denoise** menghilangkan noise visual yang sering mengganggu deteksi karakter, terutama pada JPEG yang dipindai.

### Kenali teks dari JPEG

```java
// Step 3: Attach the image to the engine
engine.setImage(imageStream);

// Step 4: Perform OCR recognition
OcrResult result = engine.recognize();
```

*Mengapa ini penting:*  
`engine.setImage` mengikat data gambar ke pipeline OCR. `engine.recognize()` menjalankan proses pengenalan penuh, mengembalikan `OcrResult` yang berisi teks yang diekstrak dan metrik kepercayaan.

### Ekstrak teks dari gambar dan keluarkan

```java
// Step 5: Output the recognized text
System.out.println("=== Recognized Text ===");
System.out.println(result.getText());
```

*Mengapa ini penting:*  
`result.getText()` memberikan representasi teks biasa dari konten gambar. Mencetaknya ke konsol menunjukkan bahwa **mengonversi gambar menjadi teks** telah berhasil, dan Anda dapat mengarahkan string ini ke file, basis data, atau layanan hilir.

## Contoh lengkap yang dapat dijalankan

Berikut adalah kelas Java lengkap yang menggabungkan semua langkah. Ganti `YOUR_DIRECTORY` dengan path absolut ke file JPEG Anda.

```java
import com.aspose.ocr.*;

public class OcrDemo {
    public static void main(String[] args) throws Exception {
        // Load the image for OCR
        String imagePath = "YOUR_DIRECTORY/sample.jpg";
        ImageStream imageStream = ImageStream.fromFile(imagePath);

        // Create and configure the OCR engine
        OcrEngine engine = new OcrEngine();
        engine.getPreprocessing().setDenoise(true); // improve accuracy

        // Attach the image and run recognition
        engine.setImage(imageStream);
        OcrResult result = engine.recognize();

        // Print the extracted text
        System.out.println("=== Recognized Text ===");
        System.out.println(result.getText());
    }
}
```

### Output yang diharapkan

Dengan asumsi `sample.jpg` berisi teks “Hello World”, konsol akan menampilkan:

```
=== Recognized Text ===
Hello World
```

Jika gambar berisi beberapa baris, setiap baris akan muncul pada baris terpisah di output.

## Variasi umum dan kasus tepi

| Situasi                                 | Penyesuaian yang direkomendasikan |
|-----------------------------------------|-----------------------------------|
| **JPEG resolusi rendah** (≤150 dpi)    | Tingkatkan `engine.getPreprocessing().setUpsample(true);` agar Aspose memperbesar gambar sebelum pengenalan. |
| **Latar belakang berwarna** (mis., formulir yang dipindai) | Aktifkan `engine.getPreprocessing().setBinarize(true);` untuk mengubah gambar menjadi hitam‑putih. |
| **Skrip non‑Latin** (mis., Cyrillic)   | Atur bahasa: `engine.getLanguage().setLanguage(OcrLanguage.RUSSIAN);`. |
| **Pemrosesan batch besar**              | Gunakan kembali satu instance `OcrEngine` untuk beberapa gambar guna mengurangi overhead startup. |
| **Butuh skor kepercayaan**              | Akses `result.getConfidence()` untuk nilai kepercayaan per karakter. |

Penyesuaian ini menggambarkan bagaimana Anda dapat **memuat gambar untuk OCR** dalam berbagai kondisi sambil tetap **melakukan OCR pada gambar** secara andal.

## Pertimbangan kinerja

* **Penggunaan memori:** Setiap `ImageStream` menyimpan seluruh gambar di memori. Untuk file yang sangat besar (mis., >10 MB), pertimbangkan streaming gambar dalam potongan menggunakan `ImageStream.fromByteArray`.  
* **Keamanan thread:** `OcrEngine` *tidak* aman untuk thread. Buat instance terpisah per thread jika Anda berencana memparallelkan tugas OCR.  
* **Mode lisensi:** Mode evaluasi membatasi jumlah halaman yang diproses per sesi. Gunakan versi berlisensi untuk beban kerja produksi.

## Kesimpulan

Anda sekarang tahu cara **melakukan OCR pada gambar** dalam file Java menggunakan Aspose OCR. Tutorial ini mencakup memuat gambar, mengaktifkan preprocessing, mengenali teks dari JPEG, mengekstrak teks, dan mengonversi gambar menjadi teks—semua dalam satu program singkat.

Dari sini Anda dapat menjelajahi topik terkait seperti **mengenali teks dari JPEG** secara massal, mengintegrasikan output dengan indeks pencarian, atau menggabungkan OCR dengan pemrosesan bahasa alami untuk alur dokumen yang lebih cerdas. Bereksperimenlah dengan opsi preprocessing untuk mencapai akurasi terbaik bagi sumber gambar spesifik Anda.

--- 

*Image illustrating the code output*  
![perform OCR on image Java example](image-placeholder.png){alt="perform OCR on image using Aspose OCR Java"}

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [recognize text image with Aspose OCR – Full Java OCR Tutorial](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Preprocess Image OCR in Java with Aspose OCR – Boost Accuracy & Extract Text](/ocr/english/java/advanced-ocr-techniques/preprocess-image-ocr-in-java-boost-accuracy-extract-text/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}