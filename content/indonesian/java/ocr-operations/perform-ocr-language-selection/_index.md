---
title: Melakukan OCR dengan Pemilihan Bahasa di Aspose.OCR
linktitle: Melakukan OCR dengan Pemilihan Bahasa di Aspose.OCR
second_title: Aspose.OCR Java API
description: Buka kunci ekstraksi teks yang tepat dari gambar dengan Aspose.OCR untuk Java. Ikuti panduan langkah demi langkah kami untuk OCR yang akurat dengan pemilihan bahasa.
type: docs
weight: 11
url: /id/java/ocr-operations/perform-ocr-language-selection/
---
## Perkenalan

Dalam lanskap teknologi yang terus berkembang, Pengenalan Karakter Optik (OCR) memainkan peran penting dalam mengekstraksi informasi bermakna dari gambar. Aspose.OCR untuk Java menonjol sebagai alat canggih yang memungkinkan pengembang mengintegrasikan kemampuan OCR secara mulus ke dalam aplikasi Java mereka. Dalam panduan langkah demi langkah ini, kita akan mempelajari cara melakukan OCR dengan pemilihan bahasa menggunakan Aspose.OCR, sehingga membuka potensi untuk memproses beragam konten dengan presisi.

## Prasyarat

Sebelum masuk ke tutorial, pastikan Anda memiliki prasyarat berikut:

- Lingkungan Pengembangan Java: Pastikan Anda telah menginstal Java di sistem Anda, dan lingkungan pengembangan Anda sudah diatur.

-  Perpustakaan Aspose.OCR: Unduh dan instal perpustakaan Aspose.OCR untuk Java. Anda dapat menemukan perpustakaan dan dokumentasi terkait[Di Sini](https://reference.aspose.com/ocr/java/).

- File Gambar: Siapkan file gambar berisi teks yang ingin Anda ekstrak. Misalnya, mari kita gunakan file bernama "p3.png."

## Paket Impor

Di proyek Java Anda, impor paket yang diperlukan untuk memanfaatkan fungsionalitas Aspose.OCR. Tambahkan baris berikut di awal file Java Anda:

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.Language;
import com.aspose.ocr.License;
import com.aspose.ocr.RecognitionResult;
import com.aspose.ocr.RecognitionSettings;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

## Langkah 1: Siapkan Direktori Dokumen Anda

```java
// Jalur ke direktori dokumen.
String dataDir = "Your Document Directory";
```

Ganti "Direktori Dokumen Anda" dengan jalur sebenarnya ke direktori tempat file gambar Anda berada.

## Langkah 2: Tentukan Jalur Gambar

```java
// Jalur gambar
String file = dataDir + "p3.png";
```

Sesuaikan variabel file agar mengarah ke file gambar spesifik Anda.

## Langkah 3: Buat Instans API Aspose.OCR

```java
// Buat contoh API
AsposeOCR api = new AsposeOCR();
```

Inisialisasi objek AsposeOCR untuk mengakses fitur-fiturnya.

## Langkah 4: Tetapkan Opsi Pengenalan

```java
// Tetapkan opsi pengenalan
RecognitionSettings settings = new RecognitionSettings();
settings.setAutoSkew(false);
ArrayList<Rectangle> rectangles = new ArrayList<Rectangle>();
rectangles.add(new Rectangle(90, 186, 775, 95));
settings.setRecognitionAreas(rectangles);
settings.setSkew(0.5);
settings.setLanguage(Language.Eng);
```

Sesuaikan pengaturan pengenalan berdasarkan kebutuhan Anda. Sesuaikan parameter seperti kemiringan, bahasa, dan area pengenalan.

## Langkah 5: Lakukan OCR dan Ambil Hasil

```java
// Dapatkan objek hasil
RecognitionResult result = null;
try {
    result = api.RecognizePage(file, settings);
} catch (IOException e) {
    e.printStackTrace();
}
```

Jalankan operasi OCR menggunakan file gambar dan pengaturan yang ditentukan. Tangkap hasilnya di objek RecognitionResult.

## Langkah 6: Cetak dan Manfaatkan Hasil

```java
// Hasil cetak
System.out.println("Result: \n" + result.recognitionText + "\n\n");
for (String n : result.recognitionAreasText) {
    System.out.println(n);
}
for (Rectangle n : result.recognitionAreasRectangles) {
    System.out.println(n.height + ":" + n.width + ":" + n.x + ":" + n.y);
}
System.out.println("\nJSON:" + result.GetJson());
System.out.println("Angle:" + result.skew);
for (String n : result.warnings) {
    System.out.println(n);
}

System.out.println("OCROperationWithLanguageSelection: execution complete");
```

Cetak teks yang diekstraksi, area pengenalan, representasi JSON, sudut kemiringan, dan peringatan apa pun. Gunakan hasilnya sesuai kebutuhan dalam aplikasi Anda.

## Kesimpulan

Dalam tutorial ini, kita telah mempelajari integrasi Aspose.OCR untuk Java untuk melakukan OCR dengan pemilihan bahasa. Pustaka yang kuat ini membuka banyak kemungkinan bagi pengembang yang ingin mengekstrak teks dari gambar secara akurat.

## FAQ

### Q1: Bisakah saya menggunakan Aspose.OCR untuk beberapa bahasa dalam satu proses pengenalan?

A1: Ya, Anda dapat mengatur beberapa bahasa di Pengaturan Pengakuan untuk meningkatkan akurasi pengenalan untuk konten multibahasa.

### Q2: Bagaimana cara menangani format gambar yang berbeda dengan Aspose.OCR?

A2: Aspose.OCR mendukung berbagai format gambar, termasuk PNG, JPEG, dan TIFF. Cukup berikan jalur file yang benar dalam variabel jalur gambar.

### Q3: Apakah ada batasan ukuran gambar yang dapat diproses oleh Aspose.OCR?

A3: Aspose.OCR dapat menangani gambar dengan berbagai ukuran, namun gambar yang lebih besar mungkin memerlukan lebih banyak waktu pemrosesan dan sumber daya.

### Q4: Dapatkah saya menyempurnakan pengaturan pengenalan untuk wilayah tertentu dalam gambar?

A4: Tentu saja. Manfaatkan fitur RecognitionAreas untuk menentukan persegi panjang tertentu dalam gambar untuk pengenalan yang ditargetkan.

### Q5: Apakah Aspose.OCR cocok untuk proyek pribadi dan komersial?

A5: Ya, Aspose.OCR menawarkan opsi lisensi yang fleksibel, sehingga cocok untuk penggunaan pribadi dan komersial.