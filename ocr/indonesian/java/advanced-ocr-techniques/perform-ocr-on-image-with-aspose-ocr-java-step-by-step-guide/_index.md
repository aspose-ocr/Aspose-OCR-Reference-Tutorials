---
category: general
date: 2026-02-14
description: Pelajari cara melakukan OCR pada gambar dan mengekstrak teks dari gambar
  menggunakan Aspose OCR di Java. Termasuk memuat gambar untuk OCR, kamus khusus,
  dan koreksi ejaan.
draft: false
keywords:
- perform OCR on image
- extract text from image
- load image for OCR
- Aspose OCR Java
- spell correction OCR
language: id
og_description: Lakukan OCR pada gambar di Java dengan Aspose OCR. Panduan ini menunjukkan
  cara memuat gambar untuk OCR, mengekstrak teks dari gambar, dan mengaktifkan koreksi
  ejaan.
og_title: Lakukan OCR pada Gambar – Tutorial Java Lengkap
tags:
- OCR
- Java
- Aspose
title: Lakukan OCR pada Gambar dengan Aspose OCR – Panduan Langkah demi Langkah Java
url: /id/java/advanced-ocr-techniques/perform-ocr-on-image-with-aspose-ocr-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lakukan OCR pada Gambar – Tutorial Java Lengkap

Pernah membutuhkan untuk **perform OCR on image** file tetapi tidak yakin harus mulai dari mana? Anda tidak sendirian; banyak pengembang mengalami hal yang sama ketika pertama kali mencoba mengekstrak teks dari data gambar. Kabar baiknya, dengan Aspose OCR untuk Java Anda dapat mendapatkan hasil yang dapat diandalkan hanya dengan beberapa baris kode—tambahan lagi Anda dapat meningkatkan akurasi dengan kamus khusus dan pemeriksaan ejaan.

Dalam panduan ini kami akan membahas semua yang perlu Anda ketahui: mulai dari memuat gambar untuk OCR, mengaktifkan koreksi ejaan, hingga mencetak teks yang telah dibersihkan. Pada akhir panduan Anda akan dapat **perform OCR on image** aset dalam proyek Java Anda sendiri, dan Anda juga akan melihat cara **extract text from image** file dengan cara yang tetap berfungsi bahkan pada pemindaian yang berisik.

## Apa yang Anda Butuhkan

- **Java Development Kit (JDK) 8+** – kode menggunakan API Java standar.
- **Aspose OCR for Java** library (Anda dapat mengunduh JAR terbaru dari situs web Aspose atau Maven Central).
- Sebuah file gambar (misalnya `invoice.png`) yang ingin Anda proses.
- (Opsional) Sebuah file teks biasa `custom_dict.txt` yang berisi kata‑kata khusus domain, satu per baris.

Itu saja—tanpa kerangka kerja berat, tanpa layanan eksternal. Hanya Java biasa dan JAR Aspose OCR.

## Langkah 1: Siapkan Proyek dan Impor Dependensi

Pertama, buat proyek Maven (atau Gradle) baru dan tambahkan dependensi Aspose OCR. Jika Anda menggunakan Maven, `pom.xml` Anda harus berisi:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- Check for the latest version -->
</dependency>
```

Jika Anda lebih suka mengunduh JAR secara manual, letakkan di folder `libs` Anda dan tambahkan ke classpath.

> **Pro tip:** Selalu periksa nomor versi pada saat penulisan; rilis yang lebih baru mungkin memperkenalkan fitur tambahan seperti paket bahasa.

## Langkah 2: Muat Gambar untuk OCR

Langkah kode pertama yang sebenarnya adalah mengarahkan mesin OCR ke gambar yang ingin Anda analisis. Aspose OCR menggunakan pembungkus `ImageStream`, yang dapat membaca dari file, array byte, atau bahkan URL.

```java
import com.aspose.ocr.*;
import java.nio.file.Files;
import java.nio.file.Paths;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {

        // Step 2: Load the image you wish to process
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/invoice.png"));
```

Perhatikan bagaimana kami **load image for OCR** dengan satu pemanggilan metode—tanpa perlu melakukan akrobatik `BufferedImage` yang rumit. Jika gambar Anda berada di resources, cukup ganti path dengan `getClass().getResourceAsStream(...)`.

## Langkah 3: Aktifkan Koreksi Ejaan (Opsional tetapi Kuat)

Aspose OCR dapat secara otomatis memperbaiki kesalahan OCR umum (seperti “l” vs “1”). Mengaktifkan fitur ini semudah mengubah sebuah flag:

```java
        // Step 3: Turn on spell‑checking to improve result quality
        ocrEngine.getEngineOptions().setSpellCorrectionEnabled(true);
```

Mengapa repot? Bayangkan memindai faktur cetak di mana fontnya sangat kecil dan pemindai menambahkan bintik‑bintik. Koreksi ejaan sering kali akan mengubah “Inv0ice” kembali menjadi “Invoice” tanpa pekerjaan tambahan dari Anda.

## Langkah 4: Sediakan Kamus Kustom (Sesuaikan Mesin)

Jika Anda berurusan dengan terminologi khusus industri—misalnya kode medis, jargon hukum, atau SKU produk—kamus kustom dapat secara dramatis meningkatkan akurasi. Kamus tersebut hanyalah file teks dengan satu kata per baris.

```java
        // Step 4: Load a custom dictionary to boost recognition of domain terms
        ocrEngine.getEngineOptions().setCustomDictionary(
                Files.readAllLines(Paths.get("YOUR_DIRECTORY/custom_dict.txt")));
```

Pastikan file menggunakan enkoding UTF‑8; jika tidak, Anda mungkin melihat karakter yang rusak untuk kata‑kata non‑ASCII.

## Langkah 5: Jalankan Proses OCR

Sekarang kami akhirnya membiarkan mesin melakukan keajaibannya. Pemanggilan `process()` mengembalikan objek `OcrResult` yang berisi teks yang dikenali, skor kepercayaan, dan bahkan tata letak jika Anda membutuhkannya nanti.

```java
        // Step 5: Execute OCR and capture the result
        OcrResult ocrResult = ocrEngine.process();
```

Jika Anda pernah bertanya-tanya apakah mesin melemparkan pengecualian, bungkus pemanggilan ini dalam blok try‑catch dan periksa `ocrResult.getErrorMessage()` untuk detailnya.

## Langkah 6: Keluarkan Teks yang Diakui (dan Diperbaiki)

Langkah terakhir adalah menampilkan—atau menyimpan—string yang diekstrak. Untuk demo cepat kami akan mencetaknya ke konsol:

```java
        // Step 6: Print the corrected text to the console
        System.out.println(ocrResult.getText());
    }
}
```

Menjalankan program seharusnya mencetak sesuatu seperti:

```
Invoice Number: 12345
Date: 2023‑07‑15
Total Amount: $1,250.00
```

Jika Anda melihat karakter yang tidak diinginkan, periksa kembali kamus kustom Anda dan pertimbangkan untuk menyesuaikan kualitas gambar (mis., tingkatkan kontras sebelum memberi ke mesin).

### Contoh Lengkap yang Berfungsi

Menggabungkan semuanya, berikut kelas lengkap yang siap dijalankan:

```java
import com.aspose.ocr.*;
import java.nio.file.Files;
import java.nio.file.Paths;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image you wish to process
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/invoice.png"));

        // Step 3: Enable spell‑checking for the OCR result
        ocrEngine.getEngineOptions().setSpellCorrectionEnabled(true);

        // Step 4: Provide a custom dictionary (one word per line)
        ocrEngine.getEngineOptions().setCustomDictionary(
                Files.readAllLines(Paths.get("YOUR_DIRECTORY/custom_dict.txt")));

        // Step 5: Run the OCR process
        OcrResult ocrResult = ocrEngine.process();

        // Step 6: Output the recognized (and corrected) text
        System.out.println(ocrResult.getText());
    }
}
```

Simpan file ini sebagai `SpellCorrectDemo.java`, sesuaikan path, kompilasi dengan `javac`, dan jalankan dengan `java SpellCorrectDemo`. Sekarang Anda harus dapat **perform OCR on image** file dan melihat teks yang diekstrak tercetak.

## Pertanyaan Umum & Kasus Tepi

### Bagaimana jika gambar berada dalam format berbeda (PDF, TIFF, dll.)?

Aspose OCR dapat menangani banyak format raster secara langsung. Untuk PDF Anda perlu mengekstrak setiap halaman sebagai gambar terlebih dahulu—Aspose PDF untuk Java melakukannya dengan baik. Pemanggilan `setImage` yang sama berfungsi setelah Anda memiliki `BufferedImage` atau aliran byte.

### Bagaimana cara menangani dokumen multi‑halaman?

Lakukan loop pada setiap gambar halaman, jalankan langkah‑langkah OCR, dan gabungkan hasilnya. Ingat untuk mereset atau membuat `OcrEngine` baru untuk setiap halaman jika Anda menginginkan konteks pemeriksaan ejaan yang independen.

### Bisakah saya membatasi bahasa atau set karakter?

Ya. Gunakan `ocrEngine.getEngineOptions().setLanguage(Language.English);` (atau bahasa lain yang didukung) untuk mengurangi false positive dan mempercepat pemrosesan.

### Bagaimana dengan kinerja pada batch besar?

Aspose OCR aman untuk thread pada operasi baca‑saja. Anda dapat membuat thread pool dan memproses gambar secara bersamaan—hanya hindari berbagi instance `OcrEngine` yang sama di antara thread.

## Tips untuk Akurasi Lebih Baik

- **Pre‑process the image**: tingkatkan kontras, hapus noise latar belakang, atau konversi ke skala abu‑abu.
- **Use a high‑resolution scan** (300 dpi atau lebih). Resolusi lebih rendah sering menghasilkan karakter yang rusak.
- **Keep the custom dictionary lean**: terlalu banyak kata yang tidak terkait dapat membingungkan pemeriksa ejaan.
- **Validate the output**: jika Anda mengetahui format yang diharapkan (mis., tanggal, angka), jalankan proses regex setelahnya untuk menangkap anomali.

## Langkah Selanjutnya

Sekarang Anda dapat **perform OCR on image** file dan **extract text from image** menggunakan Aspose OCR, Anda mungkin ingin menjelajahi:

- **Saving the OCR output to a PDF** dengan lapisan teks yang dapat dicari.
- **Integrating with a database** untuk menyimpan data faktur yang diekstrak secara otomatis.
- **Applying machine‑learning post‑processing** untuk akurasi lebih tinggi pada catatan tulisan tangan.
- **Using the `load image for OCR` flag** dalam layanan web yang menerima gambar yang diunggah pengguna.

Setiap topik ini dibangun di atas langkah inti yang kami bahas, sehingga Anda akan menemukan transisinya mulus.

*Selamat coding! Jika Anda mengalami kendala, silakan tinggalkan komentar—tidak ada yang mengalahkan belajar dari contoh dunia nyata.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}