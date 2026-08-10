---
category: general
date: 2026-06-16
description: Muat gambar untuk OCR dan dengan cepat mengekstrak teks dari area menggunakan
  Aspose OCR di Java. Panduan langkah demi langkah dengan kode lengkap, tips, dan
  penanganan kasus tepi.
draft: false
keywords:
- load image for OCR
- extract text from region
- Aspose OCR Java
- OCR region processing
- Java image recognition
language: id
og_description: Memuat gambar untuk OCR di Java dan mengekstrak teks dari wilayah
  dengan Aspose OCR. Tutorial lengkap dengan kode, penjelasan, dan praktik terbaik.
og_title: Muat gambar untuk OCR – Panduan Ekstraksi Region Java
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: load image for OCR and quickly extract text from region using Aspose
    OCR in Java. Step‑by‑step guide with full code, tips, and edge‑case handling.
  headline: load image for OCR, extract text from region – Java
  type: TechArticle
- description: load image for OCR and quickly extract text from region using Aspose
    OCR in Java. Step‑by‑step guide with full code, tips, and edge‑case handling.
  name: load image for OCR, extract text from region – Java
  steps:
  - name: Create the OCR engine and **load image for OCR**
    text: First we instantiate `OcrEngine` and point it at the file we want to process.
      The `ImageStream.fromFile` helper takes care of reading the bytes and wrapping
      them in a format the engine understands.
  - name: Define the **region** you want to **extract text from region**
    text: A `java.awt.Rectangle` describes the X/Y offset and the width/height of
      the area you care about. The numbers are pixel‑based, so you may need to experiment
      a bit with your particular document.
  - name: Apply the region to the engine
    text: The `RecognitionSettings` object holds all the knobs you can turn. Here
      we simply set the region we just created.
  - name: Run the OCR – the engine will also deskew the region automatically
    text: 'Calling `recognize()` does the heavy lifting: it deskews, binarizes, and
      runs the character recognizer on the defined rectangle.'
  - name: '**Extract text from region** and display it'
    text: Finally we pull the plain‑text representation out of the `OcrResult`. Trimming
      removes stray line breaks and spaces.
  type: HowTo
tags:
- Java
- OCR
- Aspose
- Image Processing
title: Memuat gambar untuk OCR, mengekstrak teks dari wilayah – Java
url: /id/java/ocr-operations/load-image-for-ocr-extract-text-from-region-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# memuat gambar untuk OCR, mengekstrak teks dari wilayah – Java

Pernah membutuhkan **memuat gambar untuk OCR** tetapi tidak yakin bagaimana membatasi pemindaian hanya pada bagian yang Anda butuhkan? Anda tidak sendirian. Dalam banyak proyek dunia nyata—seperti faktur, formulir, atau kartu identitas—Anda hanya ingin **mengekstrak teks dari wilayah** yang benar‑benar berisi data, bukan seluruh gambar.

Dalam tutorial ini kami akan membahas contoh lengkap yang dapat dijalankan yang menunjukkan cara memuat gambar untuk OCR menggunakan Aspose OCR, mendefinisikan wilayah persegi panjang, dan kemudian mengekstrak teks dari wilayah tersebut. Pada akhir tutorial Anda akan memiliki program Java mandiri yang dapat Anda masukkan ke dalam proyek Maven atau Gradle mana pun, serta beberapa tip praktis untuk menangani jebakan umum.

## Apa yang Anda perlukan

Sebelum kita mulai, pastikan Anda memiliki:

| Prasyarat | Mengapa penting |
|--------------|----------------|
| **Java 17** (atau JDK terbaru) | Aspose OCR disediakan sebagai JAR yang kompatibel dengan Java 17. |
| **Aspose OCR untuk Java** (unduh dari Aspose atau tambahkan via Maven) | Menyediakan kelas `OcrEngine` dan kelas terkait lainnya. |
| **Sebuah file gambar** (misalnya `form.jpg`) yang berisi bidang yang ingin Anda baca | Mesin hanya dapat memproses apa yang Anda berikan. |
| **IDE yang memadai** (IntelliJ, Eclipse, VS Code) – opsional tetapi membantu | Mempermudah debugging dan menjalankan kode. |

Jika Anda menggunakan Maven, tambahkan dependensi ini ke `pom.xml` Anda:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- check Aspose for the latest version -->
</dependency>
```

*Pro tip:* Versi evaluasi gratis sudah cukup untuk pengujian, tetapi menambahkan watermark pada output. Dapatkan lisensi penuh jika Anda berencana mendistribusikan solusi.

## memuat gambar untuk OCR – Implementasi Langkah‑per‑Langkah

Berikut kami membagi proses menjadi lima langkah jelas. Setiap langkah menyertakan cuplikan kode, penjelasan singkat **mengapa** kami melakukannya, dan tip cepat untuk menghindari perangkap umum.

### Langkah 1: Buat mesin OCR dan **memuat gambar untuk OCR**

Pertama kami menginstansiasi `OcrEngine` dan menunjuk ke file yang ingin diproses. Pembantu `ImageStream.fromFile` menangani pembacaan byte dan membungkusnya dalam format yang dipahami mesin.

```java
import com.aspose.ocr.*;
import java.awt.Rectangle;

public class RoiOcr {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine and load the source image
        OcrEngine engine = new OcrEngine();
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/form.jpg"));
```

> **Mengapa ini penting:**  
> Mesin membutuhkan bitmap untuk diproses. Memberikan jalur yang salah akan memicu `FileNotFoundException`, jadi periksa kembali lokasi absolut atau relatifnya. Jika gambar berada di folder resources, gunakan `ClassLoader.getResourceAsStream` sebagai gantinya.

### Langkah 2: Definisikan **wilayah** yang ingin Anda **ekstrak teks dari wilayah**

`java.awt.Rectangle` menggambarkan offset X/Y serta lebar/tinggi area yang Anda inginkan. Angka‑angka tersebut berbasis piksel, jadi Anda mungkin perlu bereksperimen sedikit dengan dokumen spesifik Anda.

```java
        // Step 2: Define the rectangular region that contains the field to read
        Rectangle region = new Rectangle(120, 340, 560, 80); // x, y, width, height
```

> **Mengapa ini penting:**  
> Dengan membatasi mesin OCR ke wilayah tertentu, Anda secara dramatis meningkatkan akurasi dan kecepatan. Mesin tidak akan membuang waktu mencoba membaca seluruh halaman, dan menghindari latar belakang berisik yang dapat merusak hasil.

### Langkah 3: Terapkan wilayah ke mesin

Objek `RecognitionSettings` menyimpan semua pengaturan yang dapat Anda ubah. Di sini kami cukup menetapkan wilayah yang baru saja dibuat.

```java
        // Step 3: Apply the region to the engine so only this area is processed
        engine.getRecognitionSettings().setRegion(region);
```

> **Tip:** Jika Anda perlu memproses beberapa bidang, Anda dapat memanggil `setRegion` berulang kali di dalam loop, memperbarui persegi panjang setiap kali sebelum memanggil `recognize()`.

### Langkah 4: Jalankan OCR – mesin juga akan secara otomatis mengoreksi kemiringan wilayah

Memanggil `recognize()` melakukan pekerjaan berat: mengoreksi kemiringan, melakukan binarisasi, dan menjalankan pengenalan karakter pada persegi panjang yang ditentukan.

```java
        // Step 4: Perform recognition (the engine will deskew the region automatically)
        OcrResult result = engine.recognize();
```

> **Mengapa ini penting:**  
> Koreksi kemiringan memperbaiki masalah umum ketika formulir yang dipindai tidak sejajar sempurna. Tanpa itu, Anda mungkin mendapatkan karakter yang kacau meskipun wilayahnya sudah benar.

### Langkah 5: **Ekstrak teks dari wilayah** dan tampilkan

Akhirnya kami mengambil representasi teks polos dari `OcrResult`. Metode `trim` menghilangkan baris kosong dan spasi yang tidak diinginkan.

```java
        // Step 5: Output the extracted text
        System.out.println("Field value: " + result.getText().trim());
    }
}
```

Menjalankan program akan mencetak sesuatu seperti:

```
Field value: 12345-AB
```

Itulah seluruh siklus: **memuat gambar untuk OCR**, membatasi pemindaian, dan **mengekstrak teks dari wilayah**.

## Contoh lengkap yang dapat dijalankan (tanpa bagian yang hilang)

Jika Anda lebih suka menyalin‑tempel semuanya sekaligus, berikut kelas lengkapnya, termasuk pernyataan impor dan cuplikan `pom.xml` minimal untuk pengguna Maven.

```java
// File: RoiOcr.java
import com.aspose.ocr.*;
import java.awt.Rectangle;

public class RoiOcr {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine and load the source image
        OcrEngine engine = new OcrEngine();
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/form.jpg"));

        // Step 2: Define the rectangular region that contains the field to read
        Rectangle region = new Rectangle(120, 340, 560, 80); // x, y, width, height

        // Step 3: Apply the region to the engine so only this area is processed
        engine.getRecognitionSettings().setRegion(region);

        // Step 4: Perform recognition (the engine will deskew the region automatically)
        OcrResult result = engine.recognize();

        // Step 5: Output the extracted text
        System.out.println("Field value: " + result.getText().trim());
    }
}
```

```xml
<!-- pom.xml excerpt -->
<project>
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>ocr-demo</artifactId>
    <version>1.0.0</version>
    <dependencies>
        <dependency>
            <groupId>com.aspose</groupId>
            <artifactId>aspose-ocr</artifactId>
            <version>23.10</version>
        </dependency>
    </dependencies>
</project>
```

Simpan file Java, jalankan `mvn compile exec:java -Dexec.mainClass=RoiOcr`, dan Anda akan melihat nilai yang diekstrak tercetak di konsol.

![Diagram yang menunjukkan cara memuat gambar untuk OCR dan mendefinisikan wilayah](/images/ocr-region-diagram.png "contoh memuat gambar untuk OCR")

*Ilustrasi di atas memvisualisasikan persegi panjang (120, 340, 560, 80) pada contoh formulir.*

## Menangani kasus tepi umum

| Situasi | Hal yang perlu diperhatikan | Solusi cepat |
|-----------|-------------------|-----------|
| **Gambar diputar lebih dari 15°** | Koreksi kemiringan paling efektif untuk sudut ringan. | Putar gambar terlebih dahulu dengan `java.awt.Image` sebelum memberikannya ke mesin. |
| **Wilayah berada di luar batas gambar** | `IllegalArgumentException` akan dilempar. | Validasi `region.x + region.width <= imageWidth` dan serupa untuk Y. |
| **Teks dengan kontras rendah** | Akurasi OCR menurun. | Tingkatkan kontras secara programatis atau gunakan `engine.getRecognitionSettings().setPreprocessOptions(PreprocessOptions.CONTRAST_ENHANCEMENT)`. |
| **Beberapa bahasa** | Bahasa default adalah Inggris. | Panggil `engine.getRecognitionSettings().setLanguage(Language.FRENCH)` atau berikan daftar bahasa. |

## Pro tip untuk OCR tingkat produksi

1. **Cache mesin** – membuat `OcrEngine` baru untuk setiap gambar memakan biaya tinggi. Gunakan satu instance yang sama saat memproses banyak gambar.

## Apa yang Harus Anda Pelajari Selanjutnya?


Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah‑per‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Extract Text Images – OCR Basics with Aspose.OCR for Java](/ocr/english/java/ocr-basics/)
- [Extract Text from Image Java with Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}