---
date: 2026-02-09
description: Pelajari cara mengonversi gambar menjadi teks dan mengekstrak persegi
  panjang area teks menggunakan pustaka Aspose OCR Java. Panduan langkah demi langkah
  dengan contoh kode.
linktitle: Recognize Text from Image and Retrieve Text Area Rectangles
second_title: Aspose.OCR Java API
title: Ubah Gambar menjadi Teks – Kenali Teks dari Gambar dan Dapatkan Persegi Panjang
  Area Teks
url: /id/java/ocr-basics/get-rectangles-with-text-areas/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Mengonversi Gambar ke Teks – Mengenali Teks dari Gambar dan Mengambil Persegi Panjang Area Teks

## Pendahuluan

Jika Anda perlu **mengonversi gambar ke teks** dan **mengenali teks dari file gambar** dalam aplikasi Java, Aspose.OCR untuk Java menyediakan cara yang cepat dan akurat untuk melakukannya. Pada tutorial ini kami akan memandu Anda melalui langkah‑langkah tepat untuk mengekstrak paragraf dari sebuah gambar, memperoleh persegi panjang pembatas untuk setiap area teks, dan mencetak koordinat tersebut ke konsol. Pada akhir tutorial Anda akan memahami mengapa pendekatan ini berhasil, cara mengintegrasikan pustaka, dan di mana Anda dapat memperluasnya untuk kasus penggunaan Anda sendiri.

## Jawaban Cepat
- **Apa arti “mengenali teks dari gambar”?** Itu berarti mengubah karakter visual dalam sebuah gambar menjadi data string yang dapat diedit.  
- **Pustaka mana yang menangani ini di Java?** Aspose.OCR untuk Java.  
- **Apakah saya memerlukan lisensi untuk pengembangan?** Lisensi sementara tersedia untuk pengujian; lisensi penuh diperlukan untuk produksi.  
- **Bisakah saya mengekstrak paragraf alih‑alih kata tunggal?** Ya – gunakan `AreasType.PARAGRAPHS` untuk mendapatkan persegi panjang tingkat paragraf.  
- **Apakah kode ini kompatibel dengan Java 11+?** Tentu saja, API bekerja dengan Java 11 dan versi selanjutnya.

## Apa itu “mengonversi gambar ke teks” di Aspose.OCR?
Metode `RecognizePage` milik Aspose.OCR menganalisis bitmap, menerapkan algoritma OCR, dan mengembalikan string yang dikenali. Ketika Anda meminta area teks, pustaka juga menghitung koordinat `Rectangle` yang tepat untuk setiap blok teks, memudahkan penyorotan atau pemrosesan bagian tertentu nanti.

## Mengapa menggunakan **java ocr library** ini?
- **Akurasi tinggi** – mendukung banyak bahasa dan font yang kompleks.  
- **Integrasi mudah** – satu file JAR menambahkan kemampuan OCR lengkap.  
- **Output fleksibel** – Anda dapat mengambil teks mentah, HTML terformat, atau persegi panjang area teks yang tepat.  
- **Thread‑safe** – cocok untuk lingkungan server dengan throughput tinggi.

## Prasyarat

- **Java Development Kit** (JDK 11 atau lebih baru) terpasang di mesin Anda.  
- **Pustaka Aspose.OCR untuk Java** – unduh dari situs resmi [di sini](https://releases.aspose.com/ocr/java/).  
- IDE atau alat build (Maven/Gradle) untuk mengelola dependensi JAR.

## Mengimpor Paket

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

## Panduan Langkah‑per‑Langkah

### Langkah 1: Siapkan Proyek Anda
Buat proyek Java baru (atau tambahkan ke yang sudah ada) dan letakkan JAR Aspose.OCR pada classpath. Jika Anda menggunakan Maven, tambahkan dependensi seperti yang dijelaskan dalam paket unduhan.

### Langkah 2: Tentukan Direktori Dokumen dan Jalur Gambar
Tentukan lokasi gambar contoh Anda:

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";

// The image path
String imagePath = dataDir + "p3.png";
```

### Langkah 3: Buat Instance Aspose.OCR
Instansiasi mesin OCR:

```java
// Create AsposeOCR instance
AsposeOCR api = new AsposeOCR();
```

### Langkah 4: Kenali Teks dalam Gambar
Panggil `RecognizePage` untuk mengonversi gambar menjadi teks biasa. Langkah ini memperlihatkan kemampuan inti **recognize text image java**:

```java
try {
    // Recognize page by full path to file
    String result = api.RecognizePage(imagePath);
    System.out.println("Result: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

### Langkah 5: Dapatkan Persegi Panjang dengan Area Teks
Sekarang ambil persegi panjang pembatas untuk setiap paragraf (atau tipe area lain). Di sinilah Anda **mengekstrak paragraf dari gambar** dan memperoleh koordinatnya:

```java
// Get rectangles with text areas in the image.
ArrayList<Rectangle> rectResult = api.getTextAreas(imagePath, AreasType.PARAGRAPHS, true);

// Print each text area rectangle
for (Rectangle r : rectResult) {
    System.out.println("Text area:" + r);
}
```

## Masalah Umum & Pemecahan Masalah

| Gejala | Penyebab Kemungkinan | Perbaikan |
|--------|----------------------|-----------|
| `IOException` pada `RecognizePage` | Jalur file salah atau izin baca tidak ada | Pastikan `imagePath` mengarah ke PNG/JPG yang ada dan aplikasi memiliki akses ke sistem file. |
| String hasil kosong | Gambar berkualitas rendah atau bahasa tidak didukung | Praproses gambar (tingkatkan kontras, binarisasi) atau tentukan bahasa yang tepat dengan `api.setLanguage("eng")`. |
| Tidak ada persegi panjang yang dikembalikan | Menggunakan `AreasType` yang salah (misalnya `WORDS` padahal mengharapkan paragraf) | Ganti ke `AreasType.PARAGRAPHS` atau `AreasType.LINES` sesuai kebutuhan. |

## Pertanyaan yang Sering Diajukan

**T: Apakah Aspose.OCR kompatibel dengan Java 11?**  
J: Ya, Aspose.OCR bekerja dengan Java 11 dan versi selanjutnya.

**T: Bisakah saya menggunakan Aspose.OCR untuk proyek pribadi maupun komersial?**  
J: Ya, Anda dapat menggunakannya dalam jenis proyek apa pun. Untuk detail lisensi, kunjungi [di sini](https://purchase.aspose.com/buy).

**T: Bagaimana cara mendapatkan lisensi sementara untuk evaluasi?**  
J: Anda dapat memperoleh lisensi sementara [di sini](https://purchase.aspose.com/temporary-license/).

**T: Di mana saya dapat menemukan dukungan komunitas atau bantuan resmi?**  
J: Untuk dukungan dan diskusi, kunjungi [forum Aspose.OCR](https://forum.aspose.com/c/ocr/16).

**T: Apakah Aspose.OCR mendukung multithreading?**  
J: Ya, pustaka ini thread‑safe dan dapat digunakan dalam lingkungan bersamaan untuk kinerja yang lebih baik.

## Kesimpulan

Dalam **aspose ocr java tutorial** ini Anda telah mempelajari cara **mengonversi gambar ke teks** menggunakan Aspose.OCR untuk Java, mengekstrak paragraf, dan mengambil persegi panjang yang tepat mengelilingi setiap blok teks. Kemampuan ini memungkinkan Anda membangun PDF yang dapat dicari, menyorot teks dalam overlay UI, atau memasukkan data terstruktur ke proses selanjutnya. Jelajahi API lebih lanjut untuk menyesuaikan pengaturan bahasa, menangani format gambar lain, atau mengintegrasikan dengan penyimpanan cloud.

---

**Terakhir Diperbarui:** 2026-02-09  
**Diuji Dengan:** Aspose.OCR 23.10 untuk Java  
**Penulis:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}