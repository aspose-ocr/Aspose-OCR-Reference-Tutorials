---
category: general
date: 2026-06-16
description: Contoh OCR Java yang menunjukkan cara memuat gambar OCR, mengenali teks
  Java, dan mengekstrak teks Aspose dari file JPG hanya dalam beberapa baris.
draft: false
keywords:
- java ocr example
- load image ocr
- recognize text java
- recognize jpg text
- extract text aspose
language: id
og_description: Contoh OCR Java menunjukkan cara memuat gambar, mengenali teks JPG,
  dan mengekstraknya dengan pustaka Aspose OCR.
og_title: Contoh OCR Java – Muat Gambar dan Kenali Teks
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Java OCR example that shows how to load image OCR, recognize text Java,
    and extract text Aspose from a JPG file in just a few lines.
  headline: Java OCR Example – Load Image and Recognize Text with Aspose
  type: TechArticle
- questions:
  - answer: Absolutely. Just point `ImageStream.fromFile("image.png")` to the desired
      file; Aspose auto‑detects the format.
    question: Can I process PNG or TIFF files the same way?
  - answer: Check the image resolution (≥300 dpi is ideal) and consider enabling binarization.
      Also, verify that the correct language is set.
    question: What if the OCR returns garbled characters?
  - answer: 'Yes. `result.getWords()` returns a collection where each `OcrWord` has
      a `getConfidence()` method. ## Conclusion You now have a solid **java ocr example**
      that demonstrates how to **load image ocr**, **recognize text java**, and **extract
      text aspose** from a JPEG file. The snippet runs out‑of‑the‑b'
    question: Is there a way to get confidence scores for each word?
  type: FAQPage
tags:
- OCR
- Java
- Aspose
title: Contoh OCR Java – Muat Gambar dan Kenali Teks dengan Aspose
url: /id/java/ocr-basics/java-ocr-example-load-image-and-recognize-text-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Contoh Java OCR – Memuat Gambar dan Mengenali Teks dengan Aspose

Pernah bertanya-tanya bagaimana cara **java ocr example** dengan cepat mengambil teks dari sebuah gambar? Anda bukan satu-satunya—para pengembang terus-menerus perlu mengubah struk yang dipindai, kartu ID, atau bahkan tangkapan layar menjadi string yang dapat diedit. Kabar baiknya? Dengan Aspose.OCR untuk Java Anda dapat memuat gambar, menjalankan OCR, dan mendapatkan teks bersih hanya dalam beberapa baris.

Dalam panduan ini kami akan menelusuri program lengkap yang dapat dijalankan yang **load image ocr** dari JPEG, **recognize text java**, dan menunjukkan cara **extract text aspose** bahkan ketika Anda menggunakan versi evaluasi. Pada akhir panduan Anda akan memiliki templat solid yang dapat Anda masukkan ke dalam proyek apa pun.

## Apa yang Akan Anda Pelajari

- Cara menambahkan pustaka Aspose.OCR ke proyek Maven atau Gradle.  
- Kode tepat yang diperlukan untuk **recognize jpg text** dari file di disk.  
- Cara mendeteksi build evaluasi dan menangani peringatan watermark.  
- Tips untuk mengatasi jebakan umum seperti format gambar yang tidak didukung atau pemindaian beresolusi rendah.  

Tidak diperlukan pengalaman sebelumnya dengan Aspose; hanya diperlukan setup Java dasar dan file gambar untuk diuji.

## Prasyarat

| Persyaratan | Mengapa penting |
|-------------|-----------------|
| JDK 17 atau lebih baru (pustaka mendukung Java 8+ tetapi JDK yang lebih baru memberikan kinerja lebih baik) | Menjamin kompatibilitas dengan binary Aspose terbaru. |
| Maven 3.x atau Gradle 7+ (atau Anda dapat menambahkan JAR secara manual) | Menyederhanakan manajemen dependensi. |
| Gambar JPEG (`sample.jpg`) yang ingin Anda proses | Contoh menggunakan JPG, tetapi format yang didukung apa pun dapat digunakan. |
| Lisensi Aspose.OCR untuk Java (opsional) | Tanpa lisensi Anda akan melihat watermark evaluasi; kode memeriksa hal tersebut. |

Jika Anda sudah memiliki proyek, cukup tambahkan dependensi berikut dan Anda siap.

```xml
<!-- Maven -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version>
</dependency>
```

```gradle
// Gradle
implementation 'com.aspose:aspose-ocr:23.10'
```

> **Pro tip:** Jaga nomor versi tetap terbaru; Aspose merilis peningkatan setiap kuartal yang meningkatkan akurasi, terutama pada gambar dengan kontras rendah.

## Langkah 1: Buat Instance OCR Engine

Hal pertama yang Anda butuhkan adalah `OcrEngine`. Anggaplah itu sebagai otak yang akan menganalisis piksel dan mengubahnya menjadi karakter.

```java
// Step 1 – Initialize the OCR engine
OcrEngine engine = new OcrEngine();
```

Mengapa objek engine terpisah? Itu memungkinkan Anda menggunakan kembali konfigurasi yang sama pada beberapa gambar, menghemat memori dan waktu startup.

## Langkah 2: Muat Gambar untuk OCR

Sekarang kita sebenarnya **load image ocr** data dari disk. Aspose menyediakan pembungkus `ImageStream` yang nyaman yang mengabstraksi penanganan `InputStream` mentah.

```java
// Step 2 – Load the JPEG file you want to process
engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.jpg"));
```

Ganti `YOUR_DIRECTORY` dengan path absolut atau relatif tempat `sample.jpg` berada. Metode ini mendukung PNG, BMP, TIFF, dan bahkan PDF multi‑halaman—sehingga Anda tidak terbatas hanya pada JPG.

> **Pertanyaan umum:** *Bagaimana jika gambar saya berada dalam array byte?*  
> Gunakan `ImageStream.fromBytes(byteArray)` sebagai gantinya; sisa alur tetap sama.

## Langkah 3: Kenali Teks di Java

Dengan gambar di memori, kami meminta Aspose melakukan pekerjaan berat. Pemanggilan `recognize()` menjalankan algoritma OCR dan mengembalikan objek `OcrResult`.

```java
// Step 3 – Perform OCR and get the result object
OcrResult result = engine.recognize();
```

Pustaka secara otomatis mendeteksi bahasa, orientasi, dan bahkan melakukan pengurangan noise dasar. Jika Anda perlu memaksa bahasa (mis., Prancis), Anda dapat mengatur `engine.getLanguage().setLanguage(Language.French);` sebelum memanggil `recognize()`.

## Langkah 4: Tangani Peringatan Versi Evaluasi

Jika Anda menjalankan build evaluasi gratis, hasilnya mungkin mengandung watermark halus. Flag `isEvaluation()` memungkinkan Anda memberi peringatan kepada pengguna atau mencatat kondisi tersebut.

```java
// Step 4 – Check for evaluation mode
if (result.isEvaluation()) {
    System.out.println("[EVALUATION] Result may contain a watermark.");
}
```

Ketika Anda kemudian membeli lisensi dan menerapkannya melalui `License license = new License(); license.setLicense("Aspose.Total.Java.lic");`, blok ini tidak akan pernah dipicu.

## Langkah 5: Ekstrak Teks Aspose dan Cetak

Akhirnya, kami mengambil string yang dikenali dari hasil dan menampilkannya. Inilah bagian **extract text aspose** terjadi.

```java
// Step 5 – Output the recognized text
System.out.println(result.getText());
```

String yang dikembalikan mempertahankan jeda baris, sehingga Anda mendapatkan representasi yang cukup setia dari tata letak asli.

### Output yang Diharapkan

Dengan asumsi `sample.jpg` berisi kalimat “Hello, Aspose OCR!”, Anda akan melihat sesuatu seperti:

```
[EVALUATION] Result may contain a watermark.
Hello, Aspose OCR!
```

Jika gambar buram atau beresolusi rendah, Anda mungkin mendapatkan spasi tambahan atau karakter yang salah baca—kelainan OCR umum yang akan kami bahas selanjutnya.

## Langkah 6: Tips untuk Akurasi Lebih Baik (Peningkatan Opsional)

| Tips | Bagaimana membantu |
|------|--------------------|
| **Increase DPI** – Skala gambar ke 300 dpi sebelum memberi ke `engine` | Resolusi lebih tinggi memberi engine lebih banyak detail untuk diproses. |
| **Pre‑process with binarization** – Konversi ke hitam‑putih menggunakan `engine.getImageProcessingOptions().setBinarization(true);` | Menghilangkan noise latar belakang yang dapat membingungkan deteksi karakter. |
| **Specify a language** – `engine.getLanguage().setLanguage(Language.English);` | Mengarahkan engine OCR, mengurangi false positive pada glyph yang mirip. |
| **Batch processing** – Gunakan kembali instance `OcrEngine` yang sama untuk beberapa file | Mengurangi beban pembuatan objek. |

Penyesuaian ini sangat berguna ketika Anda **recognize jpg text** dari struk yang dipindai atau kartu nama yang sering datang dalam JPEG beresolusi rendah.

## Contoh Lengkap yang Berfungsi

Berikut adalah kelas Java lengkap yang berdiri sendiri yang dapat Anda salin‑tempel ke IDE Anda. Ini mencakup peningkatan opsional yang disebutkan di atas, tetapi Anda dapat mengomentarinya jika lebih suka contoh minimal.

```java
import com.aspose.ocr.*;

public class JavaOcrExample {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine
        OcrEngine engine = new OcrEngine();

        // OPTIONAL: Improve accuracy for low‑resolution JPEGs
        // engine.getImageProcessingOptions().setBinarization(true);
        // engine.getLanguage().setLanguage(Language.English);

        // Load the image (replace the path with your own)
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.jpg"));

        // Perform OCR
        OcrResult result = engine.recognize();

        // Detect evaluation mode
        if (result.isEvaluation()) {
            System.out.println("[EVALUATION] Result may contain a watermark.");
        }

        // Print the extracted text
        System.out.println(result.getText());
    }
}
```

> **Catatan:** Jika Anda menjalankan ini tanpa lisensi, output akan menyertakan pemberitahuan evaluasi. Setelah Anda menambahkan file lisensi yang valid, pemberitahuan tersebut menghilang dan Anda mendapatkan teks bersih.

## Pertanyaan yang Sering Diajukan

**T: Bisakah saya memproses file PNG atau TIFF dengan cara yang sama?**  
J: Tentu saja. Cukup arahkan `ImageStream.fromFile("image.png")` ke file yang diinginkan; Aspose secara otomatis mendeteksi format.

**T: Bagaimana jika OCR mengembalikan karakter yang kacau?**  
J: Periksa resolusi gambar (≥300 dpi ideal) dan pertimbangkan mengaktifkan binarization. Juga, pastikan bahasa yang tepat telah diatur.

**T: Apakah ada cara untuk mendapatkan skor kepercayaan untuk setiap kata?**  
J: Ya. `result.getWords()` mengembalikan koleksi di mana setiap `OcrWord` memiliki metode `getConfidence()`.

## Kesimpulan

Anda sekarang memiliki **java ocr example** yang solid yang menunjukkan cara **load image ocr**, **recognize text java**, dan **extract text aspose** dari file JPEG. Potongan kode ini dapat dijalankan langsung, menangani peringatan evaluasi, dan memberi Anda jalur yang jelas untuk meningkatkan akurasi pada gambar yang lebih sulit.

Langkah selanjutnya? Coba beri engine sekumpulan faktur, bereksperimen dengan pengaturan bahasa yang berbeda, atau hubungkan output ke basis data untuk arsip yang dapat dicari. Pustaka Aspose OCR cukup fleksibel untuk mendukung apa saja mulai dari utilitas desktop sederhana hingga pipeline pemrosesan dokumen berskala besar.

Ada pertanyaan lebih lanjut atau ingin berbagi kasus penggunaan menarik? Tinggalkan komentar di bawah, dan selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

- [mengenali gambar teks dengan Aspose OCR – Tutorial Java OCR Lengkap](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Ekstrak Teks dari Gambar Java dengan Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Konversi Gambar ke Teks di Java menggunakan Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}