---
category: general
date: 2026-05-03
description: Pelajari cara mengenali teks dari gambar dan mengonversi gambar menjadi
  teks menggunakan Aspose OCR untuk Java. Termasuk tips untuk meningkatkan akurasi
  OCR dan menjalankan OCR pada file PNG.
draft: false
keywords:
- recognize text from image
- convert image to text
- improve ocr accuracy
- load image for ocr
- run ocr on png
language: id
og_description: Panduan langkah demi langkah untuk mengenali teks dari gambar menggunakan
  Aspose OCR untuk Java. Pelajari cara mengonversi gambar menjadi teks, meningkatkan
  akurasi OCR, dan menjalankan OCR pada PNG.
og_title: Mengenali teks dari gambar dengan Aspose OCR – Tutorial Java
tags:
- OCR
- Java
- Aspose
- Image Processing
title: Mengenali teks dari gambar dengan Aspose OCR – Panduan Lengkap Java
url: /id/python-java/general/recognize-text-from-image-with-aspose-ocr-complete-java-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# mengenali teks dari gambar dengan Aspose OCR – Panduan Lengkap Java

Pernah perlu **mengenali teks dari gambar** tetapi tidak yakin pustaka mana yang akan memberikan hasil yang dapat diandalkan? Anda tidak sendirian—banyak pengembang mengalami kebuntuan saat pertama kali mencoba mengekstrak data dari PDF yang dipindai, kwitansi, atau laporan laboratorium. Kabar baiknya, Aspose OCR untuk Java membuat seluruh proses menjadi sangat mudah, dan Anda bahkan dapat **mengonversi gambar ke teks** hanya dengan beberapa baris kode.

Dalam tutorial ini kami akan membahas semua yang perlu Anda ketahui: mulai dari memuat gambar untuk OCR, menyesuaikan pengaturan untuk **meningkatkan akurasi OCR**, hingga akhirnya **menjalankan OCR pada PNG** dan mencetak teks yang diekstrak. Tanpa basa‑basi, hanya contoh praktis yang dapat langsung dijalankan dalam proyek Anda hari ini.

---

## Apa yang Anda Butuhkan

Sebelum kita mulai, pastikan Anda memiliki hal‑hal berikut di mesin Anda:

| Prasyarat | Alasan |
|--------------|--------|
| Java 17 (atau lebih baru) | Aspose OCR mendukung Java 8+, tetapi JDK terbaru memberikan kinerja yang lebih baik. |
| Aspose OCR for Java library (`aspose-ocr.jar`) | Mesin inti yang melakukan semua pekerjaan berat. |
| File lisensi Aspose OCR yang valid (`Aspose.OCR.Java.lic`) | Mengaktifkan semua fitur; jika tidak, Anda akan mendapatkan watermark percobaan. |
| File gambar (PNG, JPEG, TIFF, dll.) yang berisi teks jelas | Kami akan menggunakan `lab_report.png` sebagai contoh konkret. |
| Kamus khusus (opsional) | Meningkatkan pengenalan untuk istilah khusus domain seperti “hemoglobin”. |

Jika ada yang terdengar asing, jangan panik—menginstal JAR dan membuat file teks sederhana adalah tugas trivial yang akan kami bahas sebentar lagi.

---

## Langkah 1 – Siapkan Proyek dan Impor Dependensi

Pertama, buat proyek Maven (atau Gradle) baru dan tambahkan dependensi Aspose OCR. Pengguna Maven dapat menempelkan cuplikan ini ke dalam `pom.xml` mereka:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- check the latest version on Maven Central -->
</dependency>
```

Jika Anda lebih suka Gradle, setaraannya adalah:

```groovy
implementation 'com.aspose:aspose-ocr:23.10'
```

> **Pro tip:** Perhatikan nomor versi; rilis terbaru sering berisi perbaikan bug yang secara langsung memengaruhi **meningkatkan akurasi OCR**.

Sekarang, buat kelas Java bernama `OcrDemo.java`. Di bagian atas file, impor kelas‑kelas yang diperlukan:

```java
import com.aspose.ocr.OcrEngine;
import com.aspose.ocr.License;
import com.aspose.ocr.Image;
import com.aspose.ocr.OcrResult;
```

---

## Langkah 2 – Inisialisasi Mesin OCR dan Terapkan Lisensi Anda

Anda tidak dapat **menjalankan OCR pada PNG** tanpa terlebih dahulu memberi tahu mesin bahwa ia telah dilisensikan. Begini caranya:

```java
public class OcrDemo {
    public static void main(String[] args) {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Apply your license – replace the path with your actual license location
        License lic = new License();
        lic.setLicense("YOUR_DIRECTORY/Aspose.OCR.Java.lic");
        ocrEngine.setLicense(lic);
```

Mengapa perlu objek `License` tambahan? Aspose memisahkan penanganan lisensi dari mesin agar Anda dapat mengganti lisensi secara dinamis, yang berguna dalam skenario SaaS multi‑tenant.

---

## Langkah 3 – Muat Kamus Khusus (Opsional namun Kuat)

Jika Anda berurusan dengan terminologi medis, formula kimia, atau nama merek, kamus khusus dapat **meningkatkan akurasi OCR** secara dramatis. Kamus tersebut adalah file teks biasa dengan satu kata per baris:

```java
        // Optional: improve accuracy with a custom dictionary
        // Create a file named custom_dictionary.txt in YOUR_DIRECTORY
        ocrEngine.getConfig().setCustomDictionary("YOUR_DIRECTORY/custom_dictionary.txt");
```

> **Mengapa ini berhasil:** Mesin OCR menggunakan kamus untuk memihak model bahasa ke kata‑kata yang Anda butuhkan, mengurangi kesalahan pengenalan seperti “hemo­globin” → “hemoglobin”.

Jika Anda tidak memiliki kamus, cukup lewati baris ini—Aspose tetap bekerja dengan baik menggunakan paket bahasa bawaan.

---

## Langkah 4 – Muat Gambar yang Ingin Diproses

Sekarang kita benar‑benar **memuat gambar untuk OCR**. Aspose mendukung banyak format, tetapi PNG khususnya lossless, menjadikannya pilihan aman untuk dokumen yang dipindai.

```java
        // Load the PNG image containing the text you want to extract
        Image inputImage = Image.fromFile("YOUR_DIRECTORY/lab_report.png");
```

> **Kasus khusus:** Jika gambar Anda sangat besar (lebih dari 5 MB), pertimbangkan untuk memperkecilnya terlebih dahulu agar pemrosesan lebih cepat. Kelas `Image` menyediakan metode `resize` yang dapat dipanggil sebelum pengenalan.

---

## Langkah 5 – Jalankan Proses OCR dan Dapatkan Teksnya

Setelah semuanya siap, jalankan mesin OCR. Metode `recognize` mengembalikan objek `OcrResult` yang berisi string hasil ekstraksi, skor kepercayaan, dan bahkan kotak pembatas jika Anda memerlukan informasi tata letak.

```java
        // Perform OCR on the loaded image
        OcrResult result = ocrEngine.recognize(inputImage);

        // Print the extracted text to the console
        System.out.println("=== Extracted Text ===");
        System.out.println(result.getText());
    }
}
```

Saat Anda menjalankan program, Anda akan melihat sesuatu seperti ini:

```
=== Extracted Text ===
Patient Name: John Doe
Hemoglobin: 13.5 g/dL
...
```

Itu saja—Anda telah berhasil **mengenali teks dari gambar** dan **mengonversi gambar ke teks** menggunakan Aspose OCR.

---

## Langkah 6 – Masalah Umum dan Cara Mengatasinya

Meskipun menggunakan pustaka yang solid, beberapa kendala kecil dapat menghambat Anda:

| Gejala | Penyebab Kemungkinan | Solusi |
|---------|----------------------|--------|
| Output kosong | Lisensi tidak diterapkan atau sudah kedaluwarsa | Periksa jalur ke `Aspose.OCR.Java.lic` dan pastikan cocok dengan versi. |
| Karakter kacau | Gambar beresolusi rendah atau terlalu terkompresi | Gunakan sumber beresolusi lebih tinggi atau pra‑proses gambar (binarisasi, deskew). |
| Kata‑kata domain tidak muncul | Tidak ada kamus khusus | Tambahkan file kamus dengan istilah yang hilang, satu per baris. |
| Pemrosesan lambat pada batch besar | Tidak ada multithreading | Buat pool instance `OcrEngine` (aman untuk thread) dan proses gambar secara paralel. |

---

## Langkah 7 – Memperluas Contoh: Menyimpan Hasil ke File

Jika Anda perlu menyimpan teks yang diekstrak untuk analisis selanjutnya, cukup tulis ke file:

```java
import java.nio.file.Files;
import java.nio.file.Paths;
import java.nio.charset.StandardCharsets;

// ...

        // Save the text to a .txt file
        Files.write(Paths.get("output.txt"),
                    result.getText().getBytes(StandardCharsets.UTF_8));
        System.out.println("Text saved to output.txt");
```

Sekarang Anda memiliki pipeline yang dapat digunakan kembali yang **memuat gambar untuk OCR**, mengekstrak kontennya, dan menyimpannya ke mana pun Anda inginkan.

---

## Bonus: Menjalankan OCR pada Banyak File PNG dalam Folder

Proyek dunia nyata sering harus memproses puluhan pemindaian. Berikut loop singkat yang mengambil setiap `.png` dalam sebuah direktori:

```java
import java.io.File;

// ...

        File folder = new File("YOUR_DIRECTORY/scans");
        File[] pngFiles = folder.listFiles((dir, name) -> name.toLowerCase().endsWith(".png"));

        for (File png : pngFiles) {
            Image img = Image.fromFile(png.getAbsolutePath());
            OcrResult res = ocrEngine.recognize(img);
            System.out.println("---- " + png.getName() + " ----");
            System.out.println(res.getText());
        }
```

Ingat untuk menggunakan kembali instance `ocrEngine` yang sama—membuat yang baru untuk setiap file menambah beban yang tidak perlu.

---

## Kesimpulan

Anda kini memiliki solusi lengkap, end‑to‑end yang **mengenali teks dari gambar** menggunakan Aspose OCR untuk Java. Mulai dari memuat gambar, secara opsional memperkaya mesin dengan kamus khusus untuk **meningkatkan akurasi OCR**, hingga **menjalankan OCR pada PNG** dan menyimpan output, kode ini siap disisipkan ke dalam proyek Java mana pun.

Apa selanjutnya? Cobalah mengalirkan teks yang diekstrak ke pipeline pemrosesan bahasa alami, atau bereksperimen dengan OCR pada catatan tulisan tangan (Aspose juga menyediakan mode tulisan tangan). Kemungkinannya tak terbatas, dan Anda baru saja membuka langkah pertama.

Selamat coding! Jika Anda mengalami kendala, silakan tinggalkan komentar di bawah—mari kita selesaikan bersama.

![Screenshot hasil OCR di konsol – mengenali teks dari gambar](/images/ocr_console_result.png "contoh mengenali teks dari gambar")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}