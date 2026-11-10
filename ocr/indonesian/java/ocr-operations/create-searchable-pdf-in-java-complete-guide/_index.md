---
category: general
date: 2026-07-05
description: Buat PDF yang dapat dicari di Java menggunakan Aspose OCR. Pelajari cara
  mengompres gambar dalam PDF, mengonversi gambar yang dipindai menjadi PDF, dan menonaktifkan
  penyematan font pada PDF untuk menghasilkan file yang lebih kecil.
draft: false
keywords:
- create searchable pdf
- compress images in pdf
- convert scanned image to pdf
- disable font embedding pdf
language: id
og_description: Buat PDF yang dapat dicari di Java dengan Aspose OCR. Tutorial ini
  menunjukkan cara mengompres gambar dalam PDF, mengonversi gambar yang dipindai menjadi
  PDF, dan menonaktifkan penyematan font PDF.
og_title: Buat PDF yang Dapat Dicari di Java – Panduan Langkah demi Langkah
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Create searchable PDF in Java using Aspose OCR. Learn how to compress
    images in PDF, convert scanned image to PDF, and disable font embedding PDF for
    smaller files.
  headline: Create Searchable PDF in Java – Complete Guide
  type: TechArticle
tags:
- Java
- OCR
- PDF
title: Buat PDF yang Dapat Dicari di Java – Panduan Lengkap
url: /id/java/ocr-operations/create-searchable-pdf-in-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Membuat PDF yang Dapat Dicari di Java – Panduan Lengkap

Pernah perlu **create searchable PDF** dari dokumen yang dipindai tetapi merasa terhambat pada bagian “bagaimana‑saya‑melakukannya”? Anda tidak sendirian. Dalam banyak proyek, mengubah TIFF atau JPEG menjadi PDF yang dapat Anda cari adalah fitur *must‑have*, terutama ketika Anda juga ingin **compress images in PDF** untuk menjaga ukuran file tetap terkendali.  

Dalam tutorial ini kami akan membahas contoh langsung menggunakan Aspose OCR untuk Java. Pada akhir tutorial Anda akan tahu persis cara **convert scanned image to PDF**, menyesuaikan pengaturan **compress images in PDF**, dan bahkan **disable font embedding PDF** untuk mengurangi beberapa kilobyte tambahan. Tanpa basa‑basi—hanya solusi lengkap yang dapat dijalankan dan dapat Anda masukkan ke dalam basis kode Anda hari ini.

## Apa yang Akan Anda Pelajari

- Siapkan mesin Aspose OCR dalam proyek Java.  
- Lakukan OCR pada TIFF (atau gambar raster apa pun).  
- Konfigurasikan `PdfSaveOptions` untuk **compress images in PDF** dan **disable font embedding PDF**.  
- Simpan hasilnya sebagai **searchable PDF** yang dapat Anda indeks atau cari secara instan.  

**Prasyarat**  
- Java 8 atau yang lebih baru terpasang.  
- Maven atau Gradle untuk manajemen dependensi (kami akan menunjukkan cuplikan Maven).  
- File gambar yang dipindai (TIFF, PNG, atau JPEG) siap untuk diproses.  

Jika Anda sudah memiliki semuanya, mari kita mulai.

![Alur kerja membuat PDF yang dapat dicari – Konversi OCR Java ke PDF](/images/create-searchable-pdf-workflow.png "Diagram yang menunjukkan langkah‑langkah membuat PDF yang dapat dicari dengan Aspose OCR")

## Langkah 1: Tambahkan Dependensi Aspose OCR

Pertama, tarik pustaka Aspose OCR ke dalam proyek Anda. Dengan Maven, tambahkan ini ke `pom.xml` Anda:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- Use the latest stable version -->
</dependency>
```

Jika Anda lebih suka Gradle, yang setara adalah:

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

> **Pro tip:** Pantau catatan rilis Aspose; versi yang lebih baru seringkali meningkatkan kinerja untuk akurasi OCR.

## Langkah 2: Inisialisasi Mesin OCR

Membuat mesin OCR semudah menginstansiasi `OcrEngine`. Objek ini akan menangani semua hal mulai dari memuat gambar hingga mengekstrak teks.

```java
import com.aspose.ocr.OcrEngine;

// ...

// Step 2: Create an OCR engine instance
OcrEngine engine = new OcrEngine();
```

Mengapa kita membutuhkan mesin khusus? Aspose memisahkan proses berat (praproses gambar, model bahasa) dari bagian lain aplikasi Anda, sehingga Anda dapat menggunakan kembali `engine` yang sama untuk banyak file tanpa harus menginisialisasi ulang sumber daya berat.

## Langkah 3: Lakukan OCR pada Gambar yang Dipindai

Sekarang kami memberi mesin file yang dipindai. Metode `recognizeImage` mengembalikan `RecognitionResult` yang berisi teks yang diekstrak dan informasi tata letak.

```java
import com.aspose.ocr.RecognitionResult;

// ...

// Step 3: Perform OCR on the source image
String sourcePath = "YOUR_DIRECTORY/document_scan.tif"; // could be .png or .jpg too
RecognitionResult result = engine.recognizeImage(sourcePath);
```

> **Bagaimana jika gambar bukan TIFF?**  
> Aspose OCR secara otomatis mendeteksi format raster umum, sehingga Anda dapat menunjukkannya ke JPEG, PNG, atau BMP tanpa mengubah kode.

## Langkah 4: Konfigurasikan Opsi Penyimpanan PDF (Kompres Gambar & Nonaktifkan Penyematan Font)

Di sinilah kata kunci sekunder bersinar. Kami akan memberi tahu Aspose untuk **compress images in PDF** dan **disable font embedding PDF**. Kedua pengaturan ini mengurangi ukuran file akhir—berguna saat Anda mengirim puluhan dokumen.

```java
import com.aspose.ocr.pdf.PdfSaveOptions;

// ...

// Step 4: Set up PDF save options
PdfSaveOptions pdfOpts = new PdfSaveOptions();

// Reduce PDF size by compressing images
pdfOpts.setCompressImages(true);
pdfOpts.setImageQuality(80); // 0‑100, 80 is a good balance

// Prevent fonts from being embedded – saves a few KB per page
pdfOpts.setEmbedFonts(false);
```

**Mengapa mengompres gambar?**  
Halaman yang dipindai seringkali beresolusi tinggi; mengompresnya menjadi kualitas 80 % dapat mengecilkan PDF 10‑halaman dari 12 MB menjadi kurang dari 3 MB tanpa kehilangan visual yang terlihat.

**Mengapa menonaktifkan penyematan font?**  
Jika mesin OCR menggunakan font sistem standar (seperti Arial atau Times New Roman), menyematkannya menjadi redundan. Mematikannya memangkas ukuran file lebih jauh, terutama untuk batch besar.

## Langkah 5: Simpan Hasil OCR sebagai PDF yang Dapat Dicari

Langkah akhir menyatukan semuanya: gambar mentah, lapisan teks yang diekstrak, dan opsi PDF yang baru saja kami atur.

```java
// Step 5: Save the OCR result as a searchable PDF
String outputPath = "YOUR_DIRECTORY/document.pdf";
engine.saveAsSearchablePdf(outputPath, pdfOpts);

System.out.println("Searchable PDF created at: " + outputPath);
```

Saat Anda membuka `document.pdf` di Adobe Reader atau penampil modern apa pun, Anda akan melihat gambar yang dipindai asli **plus** lapisan teks tak terlihat. Mengetik kata di kotak pencarian akan menyorot kecocokan—tepat seperti yang dijanjikan oleh “create searchable pdf”.

### Output yang Diharapkan

Menjalankan program dengan TIFF yang valid menghasilkan sesuatu seperti:

```
Searchable PDF created at: YOUR_DIRECTORY/document.pdf
```

Buka PDF, tekan `Ctrl+F`, ketik kata yang muncul di halaman yang dipindai, dan lihat ia melompat ke posisi yang tepat. Itu adalah tanda keberhasilan alur kerja **create searchable pdf**.

## Kesalahan Umum & Cara Menghindarinya

| Masalah | Mengapa Terjadi | Solusi |
|-------|----------------|-----|
| **Blank PDF** | `PdfSaveOptions` tidak diberikan ke `saveAsSearchablePdf`. | Pastikan Anda memanggil overload yang menerima `PdfSaveOptions`. |
| **Garbage characters** | Bahasa OCR tidak diatur (default adalah English). | Gunakan `engine.getLanguage().setLanguage(OcrLanguage.FRENCH);` sebelum `recognizeImage`. |
| **Huge file size** | `setCompressImages(false)` atau `setEmbedFonts(true)`. | Biarkan kedua flag tetap seperti yang ditunjukkan di atas. |
| **Image distortion** | `setImageQuality` disetel terlalu rendah (<50). | Gunakan 70‑90 untuk kompromi yang baik. |

## Memperluas Contoh

Sekarang Anda dapat **convert scanned image to PDF** dan mengontrol ukuran, Anda mungkin ingin:

- **Batch process** folder pemindaian dengan loop sederhana `for(File f : folder.listFiles())`.  
- Tambahkan **watermarks** menggunakan Aspose PDF (`PdfDocument.addWatermarkText`).  
- Ekspor teks OCR ke file **plain .txt** untuk sistem pengindeksan (`result.getText().writeToFile("doc.txt")`).  

Semua ekstensi ini menggunakan kembali instance `OcrEngine` yang sama, menjaga penggunaan memori tetap rendah.

## Kode Lengkap, Siap‑Jalankan

```java
import com.aspose.ocr.OcrEngine;
import com.aspose.ocr.RecognitionResult;
import com.aspose.ocr.pdf.PdfSaveOptions;

public class PdfOcrDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine instance
        OcrEngine engine = new OcrEngine();

        // Step 2: Perform OCR on the source image
        String source = "YOUR_DIRECTORY/document_scan.tif";
        RecognitionResult result = engine.recognizeImage(source);

        // Step 3: Configure PDF save options (compress images & disable fonts)
        PdfSaveOptions pdfOpts = new PdfSaveOptions();
        pdfOpts.setCompressImages(true);      // Reduce PDF size by compressing images
        pdfOpts.setImageQuality(80);          // Image quality (0‑100)
        pdfOpts.setEmbedFonts(false);         // Do not embed fonts to keep file size small

        // Step 4: Save the OCR result as a searchable PDF
        String output = "YOUR_DIRECTORY/document.pdf";
        engine.saveAsSearchablePdf(output, pdfOpts);

        // Step 5: Inform the user that the PDF has been created
        System.out.println("Searchable PDF created at: " + output);
    }
}
```

Salin‑tempel ini ke IDE Anda, ganti `YOUR_DIRECTORY` dengan jalur yang sebenarnya, dan jalankan. Jika semuanya telah diatur dengan benar, Anda akan memiliki **searchable PDF** yang juga ringan berkat kompresi gambar dan penyematan font yang dinonaktifkan.

## Kesimpulan

Kami baru saja membahas semua yang Anda butuhkan untuk **create searchable pdf** di Java menggunakan Aspose OCR. Dari menginisialisasi mesin, melakukan OCR, menyesuaikan **compress images in pdf**, dan **disable font embedding pdf**, hingga akhirnya menyimpan dokumen yang dapat dicari—setiap langkah dijelaskan dengan *mengapa* di baliknya.

Siap untuk tantangan berikutnya? Coba tambahkan paket bahasa OCR, proses batch seluruh folder, atau lapisi PDF dengan anotasi. Dasar‑dasar yang baru saja Anda kuasai akan memudahkan ekstensi tersebut.

Ada pertanyaan atau ingin berbagi trik Anda? Tinggalkan komentar di bawah, dan selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Mengenali Teks PDF – Operasi OCR dengan Aspose.OCR untuk Java](/ocr/english/java/ocr-operations/)
- [OCR Mengenali Dokumen PDF dalam Aspose.OCR untuk Java](/ocr/english/java/ocr-operations/recognize-pdf/)
- [Cara OCR PDF di .NET dengan Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}