---
title: Mendapatkan Persegi Panjang dengan Area Teks di Aspose.OCR
linktitle: Mendapatkan Persegi Panjang dengan Area Teks di Aspose.OCR
second_title: Aspose.OCR Java API
description: Buka kekuatan Aspose.OCR untuk Java. Pelajari cara mengekstrak teks dari gambar dengan lancar dalam panduan langkah demi langkah ini. Unduh sekarang untuk pengenalan teks yang efisien.
weight: 12
url: /id/java/ocr-basics/get-rectangles-with-text-areas/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Mendapatkan Persegi Panjang dengan Area Teks di Aspose.OCR

## Perkenalan

Apakah Anda ingin mengintegrasikan kemampuan pengenalan karakter optik (OCR) yang kuat ke dalam aplikasi Java Anda? Aspose.OCR untuk Java adalah solusi tepat Anda untuk ekstraksi teks dari gambar secara akurat dan efisien. Tutorial ini akan memandu Anda melalui proses mendapatkan persegi panjang dengan area teks menggunakan Aspose.OCR, membantu Anda memanfaatkan potensi penuh dari perpustakaan Java OCR ini.

## Prasyarat

Sebelum masuk ke tutorial, pastikan Anda memiliki prasyarat berikut:

- Lingkungan Pengembangan Java: Pastikan Anda telah menginstal Java di sistem Anda.
-  Aspose.OCR untuk Perpustakaan Java: Unduh dan atur perpustakaan Aspose.OCR. Anda dapat menemukan tautan unduhan[Di Sini](https://releases.aspose.com/ocr/java/).

## Paket Impor

Di proyek Java Anda, impor paket yang diperlukan untuk memanfaatkan fungsionalitas Aspose.OCR:

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

## Langkah 1: Siapkan Proyek Anda

Pastikan Anda memiliki proyek Java yang siap, dan perpustakaan Aspose.OCR terintegrasi.

## Langkah 2: Tentukan Direktori Dokumen dan Jalur Gambar

```java
// Jalur ke direktori dokumen.
String dataDir = "Your Document Directory";

// Jalur gambar
String imagePath = dataDir + "p3.png";
```

## Langkah 3: Buat Instans Aspose.OCR

```java
// Buat instans Aspose.OCR
AsposeOCR api = new AsposeOCR();
```

## Langkah 4: Kenali Teks dalam Gambar

```java
try {
    // Kenali halaman dengan jalur lengkap ke file
    String result = api.RecognizePage(imagePath);
    System.out.println("Result: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

## Langkah 5: Dapatkan Persegi Panjang dengan Area Teks

```java
// Dapatkan persegi panjang dengan area teks pada gambar.
ArrayList<Rectangle> rectResult = api.getTextAreas(imagePath, AreasType.PARAGRAPHS, true);

// Cetak setiap persegi panjang area teks
for (Rectangle r : rectResult) {
    System.out.println("Text area:" + r);
}
```

## Kesimpulan

Dalam tutorial ini, Anda telah mempelajari cara mengintegrasikan Aspose.OCR untuk Java ke dalam proyek Anda untuk mengekstrak teks dari gambar secara efisien. Aspose.OCR menyederhanakan tugas OCR, memberikan hasil yang akurat untuk pengalaman pengguna yang lancar.

## FAQ

### Q1: Apakah Aspose.OCR kompatibel dengan Java 11?

A1: Ya, Aspose.OCR kompatibel dengan Java 11 dan versi yang lebih baru.

### Q2: Bisakah saya menggunakan Aspose.OCR untuk proyek pribadi dan komersial?

 A2: Ya, Aspose.OCR dapat digunakan untuk proyek pribadi dan komersial. Untuk detail lisensi, kunjungi[Di Sini](https://purchase.aspose.com/buy).

### Q3: Bagaimana cara mendapatkan lisensi sementara untuk Aspose.OCR?

 A3: Anda bisa mendapatkan lisensi sementara[Di Sini](https://purchase.aspose.com/temporary-license/).

### Q4: Di mana saya dapat menemukan dukungan untuk Aspose.OCR?

 A4: Untuk dukungan dan diskusi, kunjungi[Forum Aspose.OCR](https://forum.aspose.com/c/ocr/16).

### Q5: Apakah Aspose.OCR mendukung multithreading?

A5: Ya, Aspose.OCR mendukung multithreading untuk meningkatkan kinerja di lingkungan bersamaan.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
