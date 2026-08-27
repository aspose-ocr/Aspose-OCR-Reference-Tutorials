---
date: 2026-02-20
description: Pelajari cara mengekstrak teks dari gambar menggunakan Aspose.OCR untuk
  Java, mengatur karakter yang diizinkan, dan menerapkan lisensi sementara – tutorial
  lengkap Aspose OCR Java.
linktitle: Specifying Allowed Characters in Aspose.OCR
second_title: Aspose.OCR Java API
title: Ekstrak Teks dari Gambar Menggunakan Aspose.OCR – Karakter yang Diizinkan
url: /id/java/advanced-ocr-techniques/specify-allowed-characters/
weight: 15
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ekstrak Teks dari Gambar Menggunakan Aspose.OCR – Karakter yang Diizinkan

## Introduction

Mengekstrak teks dari gambar adalah kebutuhan umum dalam aplikasi modern—baik Anda memproses faktur, memindai struk, atau mendigitalkan dokumen cetak. Dalam tutorial ini kami akan membahas **aspose ocr java tutorial** lengkap yang menunjukkan cara **mengekstrak teks dari gambar** dengan Aspose.OCR untuk Java, mengatur karakter yang diizinkan, dan menerapkan lisensi sementara saat Anda hanya menguji pustaka.

## Quick Answers
- **Apa yang dilakukan Aspose.OCR?** Ia mengekstrak teks dari gambar dengan akurasi tinggi dan mendukung set karakter khusus.  
- **Apakah saya memerlukan lisensi?** Lisensi sementara atau permanen diperlukan untuk penggunaan produksi.  
- **Versi JDK mana yang didukung?** Rilis JDK terbaru sepenuhnya kompatibel.  
- **Bisakah saya membatasi karakter yang dikenali?** Ya—gunakan API `setAllowedCharacters` untuk membatasi output.  
- **Berapa lama waktu pemasangan?** Sekitar 10‑15 menit untuk implementasi dasar.

## What is “extract text from images”?

Ekstrak teks dari gambar mengacu pada proses mengubah teks visual (misalnya cetak atau tulisan tangan) menjadi string yang dapat dibaca mesin. Ini memungkinkan tugas-tugas lanjutan seperti pencarian, pengindeksan, atau analisis data.

## Why Use Aspose.OCR for Java?

- **Akurasi tinggi** di berbagai bahasa dan font.  
- **API sederhana** yang dapat diintegrasikan dengan proyek Java apa pun.  
- **Dapat disesuaikan** set karakter, paket bahasa, dan pra‑pemrosesan gambar.  
- **Tanpa dependensi eksternal**—pustaka ini berdiri sendiri.

## Prerequisites

Sebelum memulai, pastikan Anda memiliki hal berikut:

### Java Development Kit (JDK)

Pastikan Anda memiliki Java Development Kit terbaru yang terpasang di sistem Anda. Anda dapat mengunduhnya dari [di sini](https://www.oracle.com/java/technologies/javase-downloads.html).

### Aspose.OCR for Java Library

Unduh dan instal pustaka Aspose.OCR untuk Java dari [tautan unduhan](https://releases.aspose.com/ocr/java/).

### Aspose.OCR License

Untuk mengakses potensi penuh Aspose.OCR, dapatkan lisensi yang valid. Anda dapat memperoleh satu dari [di sini](https://purchase.aspose.com/buy) atau menjelajahi [lisensi sementara](https://purchase.aspose.com/temporary-license/) untuk periode percobaan.

## How to apply temporary license

Saat Anda mengevaluasi produk, lisensi sementara menghapus watermark evaluasi dan membuka semua fungsi untuk periode terbatas. Buat string lisensi di portal Aspose, lalu berikan ke konstruktor `AsposeOCR` seperti yang ditunjukkan pada contoh kode di bawah ini. Untuk penyebaran produksi, ganti kunci sementara dengan lisensi permanen Anda.

## OCR image preprocessing tips

Kualitas gambar yang baik secara dramatis meningkatkan hasil pengenalan. Sebelum memanggil mesin OCR, pertimbangkan:

- Mengonversi gambar ke skala abu‑abu.
- Meningkatkan kontras agar karakter lebih menonjol.
- Menghapus noise latar belakang dengan filter binarisasi.
- Mengubah ukuran gambar beresolusi rendah menjadi setidaknya 300 dpi.

Langkah-langkah ini merupakan bagian dari **ocr image preprocessing** dan dapat dilakukan dengan pustaka pengolahan gambar Java standar mana pun sebelum memanggil Aspose.OCR.

## Import Packages

Setelah prasyarat siap, impor paket yang diperlukan ke dalam proyek Java Anda:

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.examples.Utils;

import java.io.IOException;
```

## Step‑by‑Step Guide

### Step 1: Set Your Document Directory

Tentukan folder tempat Anda akan menyimpan hasil OCR. Path ini akan digunakan nanti untuk menemukan file gambar.

```java
String dataDir = "Your Document Directory";
```

### Step 2: Specify the Image Path

Arahkan API ke gambar yang ingin Anda analisis.

```java
String imagePath = dataDir + "0001460985.Jpeg";
```

### Step 3: Create an Aspose.OCR Instance

Instansiasi mesin OCR dengan kunci lisensi Anda. Kunci dapat berupa string lisensi sementara atau permanen.

```java
AsposeOCR api = new AsposeOCR("YourLicenseKey");
```

### Step 4: Perform OCR Recognition

Panggil metode `RecognizeLine` untuk mengekstrak satu baris teks dari gambar. Hasilnya adalah string biasa yang dapat Anda proses atau simpan lebih lanjut.

```java
try {
    String result = api.RecognizeLine(imagePath);
    System.out.println("File: " + imagePath);
    System.out.println("Result line: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

> **Pro tip:** Jika Anda perlu membatasi output ke set karakter tertentu (misalnya hanya digit), gunakan metode `setAllowedCharacters` pada instance `AsposeOCR` sebelum memanggil `RecognizeLine`. Ini memastikan mesin mengabaikan karakter apa pun di luar set yang ditentukan.

## Common Issues and Solutions

| Masalah | Alasan | Solusi |
|-------|--------|-----|
| **Tidak ada output atau string kosong** | Path gambar tidak tepat atau format gambar tidak didukung | Verifikasi `imagePath` dan gunakan format yang didukung (JPEG, PNG, BMP) |
| **Kesalahan pengenalan** | Gambar beresolusi rendah atau latar belakang berisik | Pra‑proses gambar (tingkatkan kontras, binarisasi) sebelum OCR |
| **Lisensi tidak diterapkan** | Kunci lisensi hilang atau tidak valid | Pastikan string lisensi benar dan ditempatkan di konstruktor `AsposeOCR` |

## Frequently Asked Questions

**T: Bagaimana saya dapat memperoleh lisensi sementara untuk Aspose.OCR?**  
J: Kunjungi [halaman lisensi sementara](https://purchase.aspose.com/temporary-license/) untuk meminta lisensi percobaan.

**T: Di mana saya dapat menemukan dukungan untuk Aspose.OCR?**  
J: Bergabunglah dengan komunitas di [Forum Aspose.OCR](https://forum.aspose.com/c/ocr/16) untuk bantuan dan diskusi.

**T: Bisakah saya menentukan karakter yang diizinkan di Aspose.OCR?**  
J: Ya, Anda dapat menyesuaikan set karakter menggunakan API `setAllowedCharacters`. Lihat dokumentasi resmi untuk detailnya.

**T: Apakah Aspose.OCR kompatibel dengan versi JDK terbaru?**  
J: Tentu—Aspose.OCR secara rutin diperbarui agar tetap kompatibel dengan rilis Java terbaru.

**T: Apakah ada fitur OCR tambahan selain pengenalan baris?**  
J: Ya, pustaka ini mendukung pengenalan blok, paragraf, dan halaman penuh, serta paket bahasa dan opsi pra‑pemrosesan gambar.

## Conclusion

Dengan mengikuti **aspose ocr java tutorial** ini, Anda kini memiliki solusi yang berfungsi untuk **mengekstrak teks dari gambar** dan mengontrol karakter mana yang dikenali. Jelajahi [dokumentasi](https://reference.aspose.com/ocr/java/) lengkap untuk menemukan fitur lanjutan seperti dukungan multi‑bahasa, pra‑pemrosesan khusus, dan pemrosesan batch.

---

**Terakhir Diperbarui:** 2026-02-20  
**Diuji Dengan:** Aspose.OCR for Java 24.11  
**Penulis:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}