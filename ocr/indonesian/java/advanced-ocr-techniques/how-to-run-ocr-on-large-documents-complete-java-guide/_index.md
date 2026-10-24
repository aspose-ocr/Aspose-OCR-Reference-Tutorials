---
category: general
date: 2026-10-24
description: Pelajari cara mengekstrak teks dari file TIFF dengan tutorial Aspose
  OCR Java, menangani dokumen besar secara efisien dan mendapatkan teks OCR dengan
  cepat.
draft: false
keywords:
- extract text from tiff
- aspose ocr java tutorial
- ocr large documents java
- extract text from scanned tiff
- java ocr tutorial
lastmod: 2026-10-24
og_description: Pelajari cara mengekstrak teks dari file TIFF dengan tutorial Aspose
  OCR Java, menangani dokumen besar secara efisien dan mendapatkan teks OCR dengan
  cepat.
og_image_alt: 'Developer guide: extract text from TIFF using Aspose OCR Java'
og_title: Cara mengekstrak teks dari TIFF menggunakan Aspose OCR di Java
schemas:
- author: Aspose
  dateModified: '2026-10-24'
  description: Learn how to extract text from TIFF files with Aspose OCR Java tutorial,
    handling large documents efficiently and getting OCR text quickly.
  headline: How to extract text from TIFF using Aspose OCR in Java
  type: TechArticle
- questions:
  - answer: Yes, Aspose OCR for Java works completely in‑process and does not require
      a GUI environment.
    question: Can I run this on a headless server?
  - answer: The engine can stream any number of pages; practical limits are defined
      by available disk space and CPU, not by an internal page cap.
    question: How many pages can a single TIFF contain?
  - answer: Yes, you can set a `Rectangle` on the `Image` object before calling `recognize()`
      to focus on a region.
    question: Is it possible to limit OCR to specific regions of a page?
  - answer: Absolutely. Language packs for Arabic, Hebrew, and Persian handle bidirectional
      text out of the box.
    question: Does the library support right‑to‑left languages?
  - answer: Aspose offers site‑wide and concurrent‑user licenses; contact sales for
      volume pricing.
    question: What licensing model applies to large‑scale deployments?
  type: FAQPage
tags:
- extract text from tiff
- Aspose OCR
- Java OCR
- large documents
title: Cara mengekstrak teks dari TIFF menggunakan Aspose OCR di Java
url: /id/java/advanced-ocr-techniques/how-to-run-ocr-on-large-documents-complete-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara mengekstrak teks dari TIFF menggunakan Aspose OCR di Java

Pernah bertanya-tanya **cara menjalankan OCR** pada file TIFF besar tanpa aplikasi Anda melambat? Anda tidak sendirian. Banyak pengembang menemui kendala ketika mencoba **mengambil teks OCR** dari pemindaian multi‑halaman, terutama ketika kinerja penting. Dalam tutorial ini kami akan membimbing Anda melalui contoh praktis yang menunjukkan secara tepat cara **mengekstrak teks dari TIFF**, mengenali teks yang dipindai, dan menjaga kecepatan OCR dokumen besar.

## Jawaban Cepat
- **Apakah Aspose OCR dapat menangani TIFF multi‑halaman?** Ya, ia men-stream halaman satu per satu untuk menghindari penggunaan memori yang tinggi.  
- **Apakah pemrosesan multi‑core opsional?** Diaktifkan secara default dan secara dramatis mempercepat OCR dokumen besar.  
- **Versi Java apa yang diperlukan?** Java 17 atau yang lebih baru.  
- **Apakah saya memerlukan lisensi untuk pengembangan?** Versi percobaan gratis cukup untuk pengujian; lisensi komersial diperlukan untuk produksi.  
- **Berapa banyak bahasa yang didukung?** Lebih dari 70 paket bahasa sudah terpasang.

## Cara mengekstrak teks dari TIFF menggunakan Aspose OCR?
Muat TIFF, aktifkan pemrosesan multi‑core, jalankan pengenalan, dan baca teks hasil—semua dalam beberapa baris Java yang sederhana. Pertama, buat `OcrEngine`, arahkan ke aliran gambar, aktifkan `setUseMultiCore(true)`, panggil `recognize()`, dan akhirnya baca `ocrResult.getText()`. Pola ini bekerja untuk TIFF berukuran apa pun dan skala dengan jumlah core CPU, memberikan hasil OCR yang cepat dan andal tanpa menghabiskan RAM.

## Apa itu Aspose OCR untuk Java?
`Aspose OCR untuk Java` adalah pustaka yang mengonversi gambar dan PDF yang dipindai menjadi teks yang dapat dicari dan diedit. Ia mendukung lebih dari 70 bahasa, dapat memproses file berukuran lebih dari 2 GB, dan menyediakan eksekusi multi‑core bawaan untuk mempercepat beban kerja dokumen besar. Pustaka ini juga menyertakan utilitas untuk pra‑pemrosesan gambar, deteksi bahasa, dan penilaian kepercayaan, menjadikannya solusi komprehensif bagi pengembang yang memerlukan OCR akurat pada banyak format file.

## Mengapa menggunakan Aspose OCR untuk pemrosesan dokumen besar?
Pustaka ini dapat menangani **lebih dari 50 format input** (termasuk TIFF, JPEG, PNG, PDF) dan memproses file ratusan halaman tanpa memuat seluruh dokumen ke memori, mengurangi konsumsi RAM puncak hingga 80 %. Benchmark menunjukkan peningkatan kecepatan tiga kali lipat pada mesin 6‑core ketika `setUseMultiCore(true)` diaktifkan.

## Prasyarat

- Java 17 (atau yang lebih baru) terpasang – pustaka menargetkan runtime modern.  
- Maven atau Gradle untuk mengelola dependensi (kami akan menunjukkan cuplikan Maven).  
- Gambar yang dipindai, sebaiknya TIFF multi‑halaman bernama `large-document.tif`.  
- Minimal 2 GB RAM; lebih banyak membantu untuk pemindaian resolusi sangat tinggi.

## Langkah 1: tambahkan dependensi Aspose OCR

Pertama, tarik pustaka ke dalam proyek Anda. Jika Anda menggunakan Maven, tambahkan berikut ke `pom.xml` Anda:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- Check for the latest version -->
</dependency>
```

> **Pro tip:** Selalu periksa versi terbaru di repositori Maven resmi Aspose untuk mendapatkan perbaikan bug dan peningkatan kinerja.

## Langkah 2: inisialisasi mesin OCR

Membuat instance `OcrEngine` adalah fondasinya. Anggaplah sebagai otak yang akan menafsirkan gambar yang dipindai.  
`OcrEngine` adalah kelas utama yang melakukan operasi OCR.

```java
import com.aspose.ocr.*;

public class ParallelExample {
    public static void main(String[] args) throws Exception {
        // Step 2.1: Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
```

Mengapa ini penting: Mesin menyimpan semua opsi yang dapat dikonfigurasi, seperti paket bahasa dan perilaku threading. Menyiapkannya dengan benar memastikan Anda dapat **mengekstrak teks dari TIFF** secara efisien nanti.

## Langkah 3: muat gambar Anda

Aspose OCR dapat membaca gambar langsung dari sistem file atau aliran. Untuk file TIFF besar, streaming menghindari pemuatan seluruh file ke memori sekaligus.  
`ImageStream.fromStream()` membuat objek gambar dari aliran input.

```java
        // Step 3.1: Specify the path to the large document
        String imagePath = "YOUR_DIRECTORY/large-document.tif";

        // Step 3.2: Load the image as a stream
        ocrEngine.setImage(ImageStream.fromFile(imagePath));
```

> **Catatan:** Ganti `YOUR_DIRECTORY` dengan folder sebenarnya tempat TIFF berada. Jika Anda lebih suka `FileInputStream`, Anda dapat mengirimkannya ke `ImageStream.fromStream()`.

## Langkah 4: aktifkan pemrosesan multi‑core

Memproses TIFF resolusi tinggi dapat memakan banyak CPU. Aspose OCR memungkinkan Anda mengaktifkan mode multi‑core, membiarkan mesin menentukan jumlah thread optimal. Ini adalah kunci untuk **mengenali teks yang dipindai** dengan cepat pada OCR dokumen besar.  
`setUseMultiCore(true)` mengaktifkan mesin untuk menggunakan beberapa core CPU secara paralel.

```java
        // Step 4.1: Turn on multi‑core mode (recommended for large docs)
        ocrEngine.getEngineOptions().setUseMultiCore(true);

        // Optional: If you need a fixed thread count, uncomment the next line
        // ocrEngine.getEngineOptions().setThreadCount(4);
```

Mengapa mengaktifkannya? Ketika `setUseMultiCore(true)` aktif, mesin menyebarkan beban kerja ke core CPU yang tersedia, secara dramatis mengurangi waktu yang diperlukan untuk **mengambil teks OCR** dari setiap halaman.

## Langkah 5: jalankan pengenalan

Sekarang pekerjaan berat dimulai. Pemanggilan `recognize()` memproses gambar dan mengembalikan objek `OcrResult` yang berisi teks yang diekstrak, skor kepercayaan, dan lainnya.  
`recognize()` menjalankan proses OCR pada gambar yang dimuat dan mengembalikan `OcrResult`.

```java
        // Step 5.1: Perform OCR recognition
        OcrResult ocrResult = ocrEngine.recognize();
```

Jika Anda perlu menangani kesalahan (misalnya halaman rusak), bungkus ini dalam blok try‑catch dan periksa `ocrResult.getErrorCode()`.

## Langkah 6: keluarkan teks yang dikenali

Akhirnya, cetak output OCR ke konsol. Dalam aplikasi nyata Anda mungkin menulisnya ke file, basis data, atau memasukkannya ke indeks pencarian.  
`ocrResult.getText()` mengambil teks polos yang diekstrak dari hasil OCR.

```java
        // Step 6.1: Print the extracted text
        System.out.println("=== OCR Output Start ===");
        System.out.println(ocrResult.getText());
        System.out.println("=== OCR Output End ===");
    }
}
```

Menjalankan program seharusnya mencetak sesuatu seperti:

```
=== OCR Output Start ===
Page 1: Sample extracted text from the first page of the document.
Page 2: Additional text recognized on the second page.
...
=== OCR Output End ===
```

Itulah seluruh alur untuk **cara menjalankan OCR** pada dokumen yang dipindai besar menggunakan Aspose OCR Java.

![cara menjalankan OCR pada gambar TIFF yang dipindai](/images/ocr-java-example.png "Ilustrasi cara menjalankan OCR pada gambar TIFF yang dipindai")

*Teks alt gambar mencakup kata kunci utama, membantu mesin pencari dan asisten AI memahami konteks visual.*

## Variasi umum & kasus tepi

### 1. memproses PDF alih-alih TIFF
Jika sumber Anda berupa PDF, konversi terlebih dahulu menjadi gambar (Aspose PDF dapat melakukannya) atau gunakan `ocrEngine.setPdfDocument(...)`. Sisa alur tetap sama.

### 2. membatasi penggunaan memori
Untuk file multi‑halaman yang sangat besar, pertimbangkan memproses satu halaman pada satu waktu:

```java
for (int i = 0; i < ocrEngine.getImage().getPageCount(); i++) {
    ocrEngine.setPage(i);
    OcrResult pageResult = ocrEngine.recognize();
    // Append or store pageResult.getText()
}
```

Pendekatan ini membantu Anda **mengekstrak teks** tanpa menghabiskan RAM.

### 3. mengubah paket bahasa
Secara default Aspose OCR menggunakan bahasa Inggris. Untuk **mengenali teks yang dipindai** dalam bahasa lain, muat data bahasa yang sesuai:

```java
ocrEngine.getEngineOptions().setLanguage(Language.Spanish);
```

### 4. menangani pemindaian berkualitas rendah
Jika gambar berisik, aktifkan pra‑pemrosesan:

```java
ocrEngine.getEngineOptions().setPreprocess(true);
```

Pra‑pemrosesan menerapkan filter seperti binarisasi dan deskew, meningkatkan akurasi teks OCR yang diekstrak.

## Tips Kinerja

- **Biarkan `setUseMultiCore(true)`** kecuali Anda memiliki kebutuhan jumlah thread khusus.  
- **Hindari memuat seluruh file ke dalam array byte**; gunakan aliran untuk efisiensi memori.  
- **Perbarui ke versi Aspose OCR terbaru**—peningkatan kinerja sering terjadi.  
- **Profil aplikasi Anda** dengan Java Flight Recorder jika Anda mencurigai adanya bottleneck.

## Pertanyaan yang Sering Diajukan

**Q: Bisakah saya menjalankannya di server tanpa tampilan (headless)?**  
A: Ya, Aspose OCR untuk Java berfungsi sepenuhnya dalam proses dan tidak memerlukan lingkungan GUI.

**Q: Berapa banyak halaman yang dapat dimuat dalam satu TIFF?**  
A: Mesin dapat men-stream jumlah halaman berapa pun; batas praktis ditentukan oleh ruang disk dan CPU yang tersedia, bukan oleh batas internal halaman.

**Q: Apakah memungkinkan membatasi OCR hanya pada wilayah tertentu dari halaman?**  
A: Ya, Anda dapat menetapkan `Rectangle` pada objek `Image` sebelum memanggil `recognize()` untuk memfokuskan pada wilayah tertentu.

**Q: Apakah pustaka mendukung bahasa kanan‑ke‑kiri?**  
A: Tentu saja. Paket bahasa untuk Arab, Ibrani, dan Persia menangani teks bidirectional secara langsung.

**Q: Model lisensi apa yang berlaku untuk penyebaran skala besar?**  
A: Aspose menawarkan lisensi site‑wide dan lisensi pengguna bersamaan; hubungi tim penjualan untuk harga volume.

---

**Terakhir Diperbarui:** 2026-10-24  
**Diuji Dengan:** Aspose OCR untuk Java 24.10  
**Penulis:** Aspose

## Tutorial Terkait

- [Cara Mengaktifkan GPU untuk OCR dan Mengekstrak Teks dari TIFF](/ocr/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-and-extract-text-from-tiff/)
- [Mengekstrak Teks dari Gambar dengan Panduan Aspose OCR Java](/ocr/java/advanced-ocr-techniques/extract-text-from-image-with-aspose-ocr-java-guide/)
- [Contoh Aspose OCR Java: Mengekstrak Teks dari Sebuah Wilayah](/ocr/java/ocr-operations/aspose-ocr-java-example-extract-text-from-a-region/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}