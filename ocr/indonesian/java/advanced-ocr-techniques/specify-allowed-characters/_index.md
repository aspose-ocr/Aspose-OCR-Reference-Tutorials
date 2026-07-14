---
date: 2026-05-24
description: Temukan cara menggunakan OCR dengan Aspose.OCR untuk Java, mengekstrak
  teks dari gambar, mengatur karakter yang diizinkan, dan menerapkan lisensi sementara
  dalam hitungan menit.
keywords:
- how to use OCR
- extract text from images
- how to apply license
- how to set characters
linktitle: Menentukan Karakter yang Diizinkan dalam Aspose.OCR
schemas:
- author: Aspose
  dateModified: '2026-05-24'
  description: Discover how to use OCR with Aspose.OCR for Java, extract text from
    images, set allowed characters, and apply a temporary license in minutes.
  headline: How to Use OCR – Extract Text from Images with Aspose.OCR
  type: TechArticle
- description: Discover how to use OCR with Aspose.OCR for Java, extract text from
    images, set allowed characters, and apply a temporary license in minutes.
  name: How to Use OCR – Extract Text from Images with Aspose.OCR
  steps:
  - name: Set Your Document Directory
    text: Choose a folder where OCR results and temporary files will be stored. This
      path is later used to locate the image you want to process.
  - name: Specify the Image Path
    text: Provide the full file system path or a class‑path resource location that
      points to the image you wish to analyse.
  - name: Create an Aspose.OCR Instance
    text: '`AsposeOCR` is the core engine that performs optical character recognition.
      Instantiate it with either a temporary or permanent license string.'
  - name: Perform OCR Recognition
    text: '`RecognizeLine` extracts a single line of text from the supplied image
      and returns it as a plain Java `String`. You can call this method repeatedly
      for multi‑line documents. > **Pro tip:** If you need to restrict the output
      to digits only (e.g., for invoice numbers), call `setAllowedCharacters("0123'
  type: HowTo
- questions:
  - answer: Visit the [temporary license page](https://purchase.aspose.com/temporary-license/)
      to request a trial key that removes evaluation watermarks.
    question: How can I obtain a temporary license for Aspose.OCR?
  - answer: Join the community at the [Aspose.OCR Forum](https://forum.aspose.com/c/ocr/16)
      for help and discussions.
    question: Where can I find support for Aspose.OCR?
  - answer: Yes, use the `setAllowedCharacters` API to define a custom whitelist of
      characters. This is ideal for numeric‑only fields.
    question: Can I specify allowed characters in Aspose.OCR?
  - answer: Absolutely—Aspose.OCR is regularly updated to stay compatible with the
      newest Java releases.
    question: Is Aspose.OCR compatible with the latest JDK versions?
  - answer: The library also supports block, paragraph, and full‑page recognition,
      language packs, and advanced image preprocessing.
    question: Are there additional OCR features beyond line recognition?
  type: FAQPage
second_title: Aspose.OCR Java API
title: Cara Menggunakan OCR – Ekstrak Teks dari Gambar dengan Aspose.OCR
url: /id/java/advanced-ocr-techniques/specify-allowed-characters/
weight: 15
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menggunakan OCR – Ekstrak Teks dari Gambar dengan Aspose.OCR

Dalam aplikasi Java modern, **cara menggunakan OCR** sering menjadi pertanyaan, terutama ketika Anda perlu mengubah faktur, kwitansi, atau formulir cetak yang dipindai menjadi teks yang dapat dicari. Tutorial ini memandu Anda melalui contoh lengkap **Aspose.OCR untuk Java**: mengekstrak teks dari gambar, membatasi output ke set karakter khusus, dan menerapkan lisensi sementara untuk evaluasi cepat.

## Jawaban Cepat
- **Apa yang dilakukan Aspose.OCR?** Ia mengekstrak teks dari gambar dengan akurasi tinggi dan memungkinkan Anda membatasi karakter yang dikenali.  
- **Apakah saya memerlukan lisensi?** Lisensi sementara atau permanen diperlukan untuk penggunaan produksi; kunci sementara menghilangkan watermark.  
- **Versi JDK mana yang didukung?** Perpustakaan ini bekerja dengan rilis JDK terbaru (JDK 17, 19, 21).  
- **Bisakah saya membatasi karakter yang dikenali?** Ya—gunakan metode `setAllowedCharacters` untuk membatasi output.  
- **Berapa lama waktu pemasangan?** Sekitar 10‑15 menit untuk implementasi end‑to‑end dasar.

## Apa itu “ekstrak teks dari gambar”?
Mengekstrak teks dari gambar, yang juga dikenal sebagai optical character recognition (OCR), mengubah karakter visual—baik tercetak, tulisan tangan, atau diketik—menjadi string yang dapat dibaca mesin. Transformasi ini memungkinkan aplikasi untuk mencari, mengindeks, mengedit, dan menganalisis konten secara programatik, mendukung alur kerja seperti pemrosesan faktur, pengarsipan dokumen, dan otomatisasi entri data.

## Mengapa Menggunakan Aspose.OCR untuk Java?
Aspose.OCR mendukung **lebih dari 60 bahasa**, dapat memproses gambar hingga **10 MB** tanpa memuat seluruh file ke memori, dan memberikan **>95 % akurasi** pada pemindaian bersih. Perpustakaan ini berdiri sendiri, tidak memerlukan mesin OCR eksternal, sehingga penyebaran menjadi lebih sederhana dan beban lisensi berkurang.

## Prasyarat

### Java Development Kit (JDK)

Pastikan Anda telah menginstal Java Development Kit terbaru. Anda dapat mengunduhnya dari [sini](https://www.oracle.com/java/technologies/javase-downloads.html).

### Aspose.OCR untuk Java Library

Unduh dan instal perpustakaan Aspose.OCR untuk Java dari [tautan unduhan](https://releases.aspose.com/ocr/java/).

### Lisensi Aspose.OCR

Untuk membuka semua fungsi, dapatkan lisensi. Anda dapat membelinya dari [sini](https://purchase.aspose.com/buy) atau meminta [lisensi sementara](https://purchase.aspose.com/temporary-license/) untuk tujuan percobaan.

## Cara Menggunakan OCR dengan Aspose.OCR untuk Java?

Muat gambar Anda, konfigurasikan mesin OCR, dan panggil metode pengenalan—semua dalam beberapa baris kode sederhana. Paragraf jawaban langsung ini memberi tahu Anda langkah demi langkah: buat instance `AsposeOCR` dengan string lisensi Anda, atur karakter yang diizinkan (jika ada), dan panggil `RecognizeLine` pada gambar target untuk menerima teks yang diekstrak. API menangani pra‑pemrosesan gambar secara internal, sehingga Anda mendapatkan hasil bersih tanpa kode tambahan.

### Impor Paket

Kelas `AsposeOCR` berada di paket `com.aspose.ocr`. Impor kelas yang diperlukan sebelum mulai menulis kode.

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.examples.Utils;

import java.io.IOException;
```

## Panduan Langkah‑per‑Langkah

### Langkah 1: Atur Direktori Dokumen Anda

Pilih folder tempat hasil OCR dan file sementara akan disimpan. Jalur ini nanti akan digunakan untuk menemukan gambar yang ingin Anda proses.

```java
String dataDir = "Your Document Directory";
```

### Langkah 2: Tentukan Jalur Gambar

Berikan jalur sistem file lengkap atau lokasi sumber daya class‑path yang menunjuk ke gambar yang ingin Anda analisis.

```java
String imagePath = dataDir + "0001460985.Jpeg";
```

### Langkah 3: Buat Instance Aspose.OCR

`AsposeOCR` adalah mesin inti yang melakukan pengenalan karakter optik. Instansiasikan dengan string lisensi sementara atau permanen.

```java
AsposeOCR api = new AsposeOCR("YourLicenseKey");
```

### Langkah 4: Lakukan Pengenalan OCR

`RecognizeLine` mengekstrak satu baris teks dari gambar yang diberikan dan mengembalikannya sebagai `String` Java biasa. Anda dapat memanggil metode ini berulang kali untuk dokumen multi‑baris.

```java
try {
    String result = api.RecognizeLine(imagePath);
    System.out.println("File: " + imagePath);
    System.out.println("Result line: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

> **Tip pro:** Jika Anda perlu membatasi output hanya pada digit (misalnya untuk nomor faktur), panggil `setAllowedCharacters("0123456789")` pada instance `AsposeOCR` sebelum memanggil `RecognizeLine`. Ini memaksa mesin mengabaikan simbol non‑numerik apa pun.  
> `setAllowedCharacters` adalah metode dari `AsposeOCR` yang membatasi output OCR ke whitelist karakter yang ditentukan.

## Masalah Umum dan Solusinya

| Masalah | Penyebab | Solusi |
|-------|--------|-----|
| **Tidak ada output atau string kosong** | Jalur gambar salah atau format tidak didukung | Verifikasi `imagePath` dan gunakan format yang didukung (JPEG, PNG, BMP) |
| **Kesalahan pengenalan** | Gambar resolusi rendah atau latar belakang berisik | Pra‑proses gambar (tingkatkan kontras, binarisasi) sebelum OCR |
| **Lisensi tidak diterapkan** | Kunci lisensi hilang atau tidak valid | Pastikan string lisensi benar dan diteruskan ke konstruktor `AsposeOCR` |

## Pertanyaan yang Sering Diajukan

**T: Bagaimana cara mendapatkan lisensi sementara untuk Aspose.OCR?**  
J: Kunjungi [halaman lisensi sementara](https://purchase.aspose.com/temporary-license/) untuk meminta kunci percobaan yang menghilangkan watermark evaluasi.

**T: Di mana saya dapat menemukan dukungan untuk Aspose.OCR?**  
J: Bergabunglah dengan komunitas di [Forum Aspose.OCR](https://forum.aspose.com/c/ocr/16) untuk bantuan dan diskusi.

**T: Bisakah saya menentukan karakter yang diizinkan di Aspose.OCR?**  
J: Ya, gunakan API `setAllowedCharacters` untuk mendefinisikan whitelist karakter khusus. Ini ideal untuk bidang yang hanya berisi angka.

**T: Apakah Aspose.OCR kompatibel dengan versi JDK terbaru?**  
J: Tentu—Aspose.OCR secara rutin diperbarui agar tetap kompatibel dengan rilis Java terbaru.

**T: Apakah ada fitur OCR tambahan selain pengenalan baris?**  
J: Perpustakaan ini juga mendukung pengenalan blok, paragraf, dan halaman penuh, paket bahasa, serta pra‑pemrosesan gambar lanjutan.

## Kesimpulan

Dengan mengikuti **tutorial Aspose OCR Java** ini, Anda kini tahu **cara menggunakan OCR** untuk mengekstrak teks dari gambar, membatasi set karakter, dan menerapkan lisensi sementara untuk pengujian cepat. Selami lebih dalam dokumentasi lengkap di [dokumentasi](https://reference.aspose.com/ocr/java/) untuk mengeksplorasi dukungan multi‑bahasa, pemrosesan batch, dan pipeline pra‑pemrosesan khusus.

---

**Terakhir Diperbarui:** 2026-05-24  
**Diuji Dengan:** Aspose.OCR untuk Java 24.11  
**Penulis:** Aspose  

{{< blocks/products/products-backtop-button >}}

## Tutorial Terkait

- [Cara Mengatur Lisensi dan Memverifikasi Lisensi Aspose.OCR di Java](/ocr/java/ocr-basics/set-license/)
- [Konversi Gambar ke Teks di Java menggunakan Aspose.OCR BufferedImage](/ocr/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [Contoh Aspose OCR Java – Mengenali Baris dalam Gambar](/ocr/java/advanced-ocr-techniques/recognize-lines/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}