---
date: 2025-12-10
description: Pelajari cara mengenali teks dari gambar dan mengekstrak paragraf dari
  gambar menggunakan Aspose.OCR untuk Java. Panduan langkah demi langkah dengan contoh
  kode.
linktitle: Recognize Text from Image and Retrieve Text Area Rectangles
second_title: Aspose.OCR Java API
title: Mengenali Teks dari Gambar dan Mengambil Persegi Panjang Area Teks
url: /id/java/ocr-basics/get-rectangles-with-text-areas/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Mengenali Teks dari Gambar dan Mengambil Persegi Panjang Area Teks

## Introduction

Jika Anda perlu **mengenali teks dari gambar** dalam aplikasi Java, Aspose.OCR untuk Java menyediakan cara yang cepat dan akurat untuk melakukannya. Dalam tutorial ini kami akan menelusuri langkah‑langkah tepat yang diperlukan untuk mengekstrak paragraf dari sebuah gambar, memperoleh persegi panjang pembatas untuk setiap area teks, dan mencetak koordinat tersebut ke konsol. Pada akhirnya Anda akan memahami mengapa pendekatan ini berhasil, cara mengintegrasikan perpustakaan, dan di mana Anda dapat memperluasnya untuk kasus penggunaan Anda sendiri.

## Quick Answers
- **Apa arti “recognize text from image”?** Itu berarti mengubah karakter visual dalam sebuah gambar menjadi data string yang dapat diedit.  
- **Perpustakaan mana yang menangani ini di Java?** Aspose.OCR untuk Java.  
- **Apakah saya memerlukan lisensi untuk pengembangan?** Lisensi sementara tersedia untuk pengujian; lisensi penuh diperlukan untuk produksi.  
- **Bisakah saya mengekstrak paragraf alih‑alih kata tunggal?** Ya – gunakan `AreasType.PARAGRAPHS` untuk mendapatkan persegi panjang tingkat paragraf.  
- **Apakah kode ini kompatibel dengan Java 11+?** Tentu saja, API bekerja dengan Java 11 dan versi selanjutnya.

## What is “recognize text from image” in Aspose.OCR?
Metode `RecognizePage` Aspose.OCR menganalisis bitmap, menerapkan algoritma OCR, dan mengembalikan string yang dikenali. Ketika Anda meminta area teks, perpustakaan juga menghitung koordinat `Rectangle` yang tepat untuk setiap blok teks, memudahkan penyorotan atau pemrosesan bagian tertentu nanti.

## Why use Aspose.OCR for Java?
- **Akurasi tinggi** – mendukung banyak bahasa dan font yang kompleks.  
- **Integrasi mudah** – satu JAR menambahkan kemampuan OCR lengkap.  
- **Output fleksibel** – Anda dapat mengambil teks mentah, HTML terformat, atau persegi panjang area‑teks yang presisi.  
- **Thread‑safe** – cocok untuk lingkungan server dengan throughput tinggi.

## Prerequisites

- **Java Development Kit** (JDK 11 atau lebih baru) terpasang di mesin Anda.  
- **Aspose.OCR untuk Java** – unduh dari situs resmi [here](https://releases.aspose.com/ocr/java/).  
- IDE atau alat build (Maven/Gradle) untuk mengelola dependensi JAR.

## Import Packages

Di proyek Java Anda, impor kelas‑kelas yang diperlukan:

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

## Step‑by‑Step Guide

### Step 1: Set Up Your Project
Buat proyek Java baru (atau tambahkan ke proyek yang sudah ada) dan letakkan JAR Aspose.OCR pada classpath. Jika Anda menggunakan Maven, tambahkan dependensi sebagaimana dijelaskan dalam paket unduhan.

### Step 2: Define Document Directory and Image Path
Tentukan lokasi gambar contoh Anda:

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";

// The image path
String imagePath = dataDir + "p3.png";
```

### Step 3: Create Aspose.OCR Instance
Instansiasi mesin OCR:

```java
// Create Aspose.OCR instance
AsposeOCR api = new AsposeOCR();
```

### Step 4: Recognize Text in the Image
Panggil `RecognizePage` untuk mengubah gambar menjadi teks biasa. Langkah ini memperlihatkan kemampuan inti **recognize text from image**:

```java
try {
    // Recognize page by full path to file
    String result = api.RecognizePage(imagePath);
    System.out.println("Result: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

### Step 5: Get Rectangles with Text Areas
Sekarang ambil persegi panjang pembatas untuk setiap paragraf (atau tipe area lainnya). Di sinilah Anda **extract paragraphs from image** dan memperoleh koordinatnya:

```java
// Get rectangles with text areas in the image.
ArrayList<Rectangle> rectResult = api.getTextAreas(imagePath, AreasType.PARAGRAPHS, true);

// Print each text area rectangle
for (Rectangle r : rectResult) {
    System.out.println("Text area:" + r);
}
```

## Common Issues & Troubleshooting

| Symptom | Likely Cause | Fix |
|---------|--------------|-----|
| `IOException` on `RecognizePage` | Jalur file tidak tepat atau izin baca tidak ada | Pastikan `imagePath` mengarah ke PNG/JPG yang ada dan aplikasi memiliki akses ke sistem berkas. |
| Empty result string | Gambar berkualitas rendah atau bahasa tidak didukung | Praproses gambar (tingkatkan kontras, binarisasi) atau tentukan bahasa yang tepat dengan `api.setLanguage("eng")`. |
| No rectangles returned | Menggunakan `AreasType` yang salah (misalnya `WORDS` padahal mengharapkan paragraf) | Ganti ke `AreasType.PARAGRAPHS` atau `AreasType.LINES` sesuai kebutuhan. |

## Frequently Asked Questions

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

## Conclusion

Dalam tutorial ini Anda belajar cara **recognize text from image** menggunakan Aspose.OCR untuk Java, mengekstrak paragraf, dan mengambil persegi panjang yang tepat mengelilingi setiap blok teks. Kemampuan ini memungkinkan Anda membangun PDF yang dapat dicari, menyorot teks dalam overlay UI, atau mengalirkan data terstruktur ke proses selanjutnya. Jelajahi API lebih lanjut untuk menyesuaikan pengaturan bahasa, menangani format gambar lain, atau mengintegrasikan dengan penyimpanan cloud.

---

**Last Updated:** 2025-12-10  
**Tested With:** Aspose.OCR 23.10 for Java  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}