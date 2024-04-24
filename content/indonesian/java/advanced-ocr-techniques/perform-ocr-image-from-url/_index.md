---
title: Melakukan OCR pada Gambar dari URL di Aspose.OCR untuk Java
linktitle: Melakukan OCR pada Gambar dari URL di Aspose.OCR untuk Java
second_title: Aspose.OCR Java API
description: Buka kunci ekstraksi teks gambar yang lancar di Java dengan Aspose.OCR. OCR akurasi tinggi dengan integrasi mudah.
type: docs
weight: 11
url: /id/java/advanced-ocr-techniques/perform-ocr-image-from-url/
---
## Perkenalan

Selamat datang di panduan langkah demi langkah kami dalam melakukan Pengenalan Karakter Optik (OCR) pada gambar dari URL menggunakan Aspose.OCR untuk Java. Tutorial ini dirancang untuk membantu Anda mengintegrasikan Aspose.OCR dengan lancar ke dalam aplikasi Java Anda, memungkinkan Anda mengekstrak teks dari gambar dengan mudah. Aspose.OCR adalah perpustakaan OCR yang kuat yang mendukung berbagai format gambar, menjadikannya alat yang berharga untuk aplikasi yang memerlukan ekstraksi teks.

## Prasyarat

Sebelum masuk ke tutorial, pastikan Anda memiliki prasyarat berikut:

1. Lingkungan Pengembangan Java: Pastikan Anda telah menyiapkan lingkungan pengembangan Java yang berfungsi di mesin Anda.

2.  Perpustakaan Aspose.OCR: Unduh dan instal perpustakaan Aspose.OCR untuk Java. Anda dapat menemukan perpustakaan dan dokumentasi terkait di[Situs web Aspose.OCR](https://reference.aspose.com/ocr/java/).

## Paket Impor

Di proyek Java Anda, impor paket yang diperlukan untuk Aspose.OCR:

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.License;
import com.aspose.ocr.RecognitionResult;
import com.aspose.ocr.RecognitionSettings;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

## Langkah 1: Buat Instans API

Inisialisasi instance kelas AsposeOCR:

```java
AsposeOCR api = new AsposeOCR();
```

## Langkah 2: Tentukan URL Gambar

Tentukan URL gambar yang ingin Anda lakukan OCR:

```java
String uri = "https://www.example.com/gambar-anda.png";
```

## Langkah 3: Tetapkan Opsi Pengenalan

Konfigurasikan pengaturan pengenalan, seperti menonaktifkan kemiringan otomatis dan menentukan area pengenalan:

```java
RecognitionSettings settings = new RecognitionSettings();
settings.setAutoSkew(false);

// Tentukan area pengenalan menggunakan persegi panjang
ArrayList<Rectangle> rectangles = new ArrayList<Rectangle>();
rectangles.add(new Rectangle(90, 186, 775, 95));
settings.setRecognitionAreas(rectangles);
```

## Langkah 4: Lakukan OCR

Aktifkan proses pengenalan OCR:

```java
RecognitionResult result = null;
try {
    result = api.RecognizePageFromUri(uri, settings);
} catch (IOException e) {
    e.printStackTrace();
}
```

## Langkah 5: Cetak Hasil

Tampilkan hasil pengenalan, termasuk teks yang diekstraksi, teks area pengenalan, keluaran JSON, dan peringatan apa pun:

```java
System.out.println("Result: \n" + result.recognitionText + "\n\n");
System.out.println("RecognitionAreasText: \n");
for (String text : result.recognitionAreasText) {
    System.out.println(text);
}
System.out.println("JSON: \n" + result.GetJson());
System.out.println("Warnings: \n");
for (String warning : result.warnings) {
    System.out.println(warning);
}
```

Ulangi langkah-langkah ini untuk mengintegrasikan Aspose.OCR ke dalam aplikasi Java Anda dan mengekstrak teks dari gambar dengan presisi.

## Kesimpulan

Kesimpulannya, memanfaatkan Aspose.OCR untuk Java memberikan solusi tangguh untuk tugas-tugas OCR, memungkinkan pengembang mengekstrak teks dari gambar dengan lancar. Panduan langkah demi langkah memastikan proses integrasi yang lancar, sehingga dapat diakses oleh pengembang dari semua tingkatan.

## FAQ

### Q1: Seberapa akurat Aspose.OCR dalam mengenali teks dari gambar?

A1: Aspose.OCR menawarkan akurasi tinggi dalam pengenalan teks, terutama bila dikonfigurasi dengan area pengenalan yang tepat.

### Q2: Bisakah Aspose.OCR menangani banyak bahasa selama pengenalan OCR?

A2: Ya, Aspose.OCR mendukung pengenalan teks dalam berbagai bahasa, memberikan fleksibilitas untuk beragam aplikasi.

### Q3: Apakah ada pertimbangan lisensi untuk menggunakan Aspose.OCR dalam proyek komersial?

A3: Ya, pastikan kepatuhan terhadap persyaratan lisensi Aspose.OCR untuk penggunaan komersial. Mengacu pada[pembelian.aspose.com](https://purchase.aspose.com/buy) untuk rincian perizinan.

### Q4: Bagaimana saya bisa mendapatkan dukungan untuk masalah terkait Aspose.OCR?

 A4: Kunjungi[Forum Aspose.OCR](https://forum.aspose.com/c/ocr/16) untuk dukungan dan diskusi komunitas. Untuk dukungan premium, pertimbangkan untuk mendapatkan lisensi sementara dari[Lisensi Sementara](https://purchase.aspose.com/temporary-license/).

### Q5: Apakah tersedia uji coba gratis untuk Aspose.OCR untuk Java?

 A5: Ya, jelajahi fitur Aspose.OCR dengan uji coba gratis yang tersedia di[rilis.aspose.com](https://releases.aspose.com/).
