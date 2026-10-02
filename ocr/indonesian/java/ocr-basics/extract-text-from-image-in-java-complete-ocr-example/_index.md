---
category: general
date: 2026-01-12
description: Ekstrak teks dari gambar menggunakan Aspose OCR di Java. Pelajari cara
  mengekstrak teks dari gambar faktur dengan contoh OCR Java dan dapatkan teks OCR
  hasilnya.
draft: false
keywords:
- extract text from image
- how to extract text
- java ocr example
- process invoice image
- output ocr text
language: id
og_description: Ekstrak teks dari gambar menggunakan Aspose OCR di Java. Panduan ini
  menunjukkan cara mengekstrak teks dari gambar faktur, menyertakan contoh OCR Java,
  dan menghasilkan teks OCR.
og_title: Ekstrak Teks dari Gambar di Java – Contoh OCR Lengkap
tags:
- OCR
- Java
- Aspose
title: Ekstrak Teks dari Gambar di Java – Contoh OCR Lengkap
url: /id/java/ocr-basics/extract-text-from-image-in-java-complete-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ekstrak Teks dari Gambar di Java – Contoh OCR Lengkap

Pernah bertanya-tanya bagaimana cara **mengekstrak teks dari gambar** tanpa membuat kepala Anda berantakan? Mungkin Anda memiliki tumpukan faktur yang dipindai dan membutuhkan angka-angka dengan cepat. Menurut pengalaman saya, cara termudah adalah membiarkan perpustakaan OCR khusus melakukan pekerjaan berat. Tutorial ini menunjukkan *cara mengekstrak teks* dari gambar faktur tipikal menggunakan Aspose OCR untuk Java, dan bahkan memperlihatkan **java ocr example** yang menghasilkan teks OCR yang dapat Anda alirkan ke sistem hilir Anda.

Kami akan membahas semua yang perlu Anda ketahui: mulai dari menyiapkan proyek, mendefinisikan region of interest (ROI) yang memfokuskan pada header dan total jumlah, hingga akhirnya mencetak teks yang diekstrak. Pada akhir tutorial, Anda akan dapat **memproses gambar faktur** secara otomatis dan mendapatkan teks bersih yang dapat dicari.

> **Apa yang akan Anda dapatkan:** program Java siap‑jalankan, penjelasan jelas untuk setiap langkah, dan tip praktis untuk menangani faktur dunia nyata.

---

## Prasyarat

- Java Development Kit (JDK) 8 atau lebih baru terpasang.
- Maven atau Gradle untuk manajemen dependensi (contoh Maven ditampilkan).
- Lisensi Aspose OCR untuk Java (versi percobaan gratis cukup untuk pengujian).
- Gambar faktur (`invoice.png`) ditempatkan di direktori yang diketahui.

Jika ada yang terdengar asing, jangan khawatir—kebanyakan hanya tinggal diunduh, dan kode tetap dapat dikompilasi dengan edisi komunitas.

## Langkah 1: Siapkan Proyek Maven Anda

Pertama, buat proyek Maven baru (atau tambahkan ke proyek yang sudah ada). Di `pom.xml` Anda, tambahkan dependensi Aspose OCR:

```xml
<!-- pom.xml -->
<dependencies>
    <dependency>
        <groupId>com.aspose</groupId>
        <artifactId>aspose-ocr</artifactId>
        <version>23.9</version> <!-- Use the latest version available -->
    </dependency>
</dependencies>
```

> **Tip pro:** Jaga nomor versi tetap terbaru; rilis yang lebih baru sering meningkatkan akurasi untuk font rumit yang ditemukan pada faktur.

Setelah menyimpan file, jalankan `mvn clean install` untuk mengunduh perpustakaan ke repositori lokal Anda.

## Langkah 2: Muat Gambar Faktur

Sekarang perpustakaan siap, mari tulis kelas Java kecil. Hal pertama yang kami lakukan adalah membuat instance `OcrEngine` dan menunjukannya ke gambar yang ingin Anda baca.

```java
import com.aspose.ocr.*;

public class RoiExample {
    public static void main(String[] args) throws Exception {
        // Step 2: Load the source image
        OcrEngine engine = new OcrEngine();
        engine.setImage("YOUR_DIRECTORY/invoice.png"); // <-- replace with your path
```

Mengapa kami membuat engine **sebelum** memuat gambar? Engine menyimpan konfigurasi seperti bahasa, DPI, dan ROI. Menetapkan gambar lebih awal memastikan pengaturan tersebut diterapkan pada file yang akan diproses.

## Langkah 3: Definisikan Region of Interest (ROI)

Faktur sering berisi banyak noise—tabel, logo, dan cetakan kecil. Dengan mempersempit OCR hanya pada header dan total jumlah, Anda secara dramatis meningkatkan kecepatan dan akurasi. Aspose memungkinkan Anda mendeskripsikan zona ini dengan persegi panjang.

```java
        // Step 3: Define the regions of interest (header and total amount)
        OcrRegion region = OcrRegion.builder()
                .addRectangle(0, 0, 800, 150)      // header area
                .addRectangle(0, 1200, 800, 200)   // total amount area
                .build();

        // Apply ROI to the engine
        engine.setRegion(region);
```

Koordinat berada dalam piksel (`x`, `y`, `width`, `height`). Jika faktur Anda bervariasi ukuran, Anda dapat menghitung nilai ini secara dinamis—mungkin dengan memeriksa dimensi gambar terlebih dahulu. Itu merupakan ekstensi yang bagus jika Anda membutuhkan solusi **memproses gambar faktur** yang bekerja pada batch.

## Langkah 4: Jalankan OCR pada Region yang Ditentukan

Dengan ROI terpasang, engine OCR dapat memfokuskan perhatiannya pada bagian yang paling penting. Metode `recognize()` mengembalikan `OcrResult` yang berisi teks yang diekstrak.

```java
        // Step 4: Run OCR on the specified regions
        OcrResult result = engine.recognize();
```

Di balik layar, Aspose melakukan beberapa langkah pra‑pemrosesan: binarisasi, penghilangan noise, dan segmentasi karakter. Anda tidak perlu memanggilnya secara manual—biarkan `recognize()` melakukannya.

## Langkah 5: Keluarkan Teks yang Diekstrak

Akhirnya, kami mencetak teks ke konsol. Dalam aplikasi nyata Anda mungkin menyimpannya di basis data, mengirimnya ke pipeline analitik hilir, atau bahkan menghasilkan PDF yang dapat dicari.

```java
        // Step 5: Output the extracted text
        System.out.println("ROI text:");
        System.out.println(result.getText());
    }
}
```

Saat Anda menjalankan program, Anda akan melihat sesuatu seperti:

```
ROI text:
Acme Corp.
Invoice #12345
Date: 2025-12-31
Total Amount: $1,250.00
```

Jika output terlihat berantakan, periksa kembali koordinat persegi panjang atau tingkatkan resolusi gambar. Engine OCR menyukai pemindaian yang tajam dengan DPI tinggi.

## Contoh Lengkap yang Berfungsi

Berikut adalah file Java lengkap yang dapat Anda salin‑tempel ke `src/main/java/RoiExample.java`. Tidak diperlukan potongan kode eksternal—semua yang Anda butuhkan ada di sini.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.region.*;

public class RoiExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create the OCR engine and load the source image
        OcrEngine engine = new OcrEngine();
        engine.setImage("YOUR_DIRECTORY/invoice.png");

        // Step 2: Define the regions of interest (header and total amount)
        OcrRegion region = OcrRegion.builder()
                .addRectangle(0, 0, 800, 150)      // header area
                .addRectangle(0, 1200, 800, 200)   // total amount area
                .build();

        // Step 3: Apply the ROI configuration to the engine
        engine.setRegion(region);

        // Step 4: Run OCR on the specified regions
        OcrResult result = engine.recognize();

        // Step 5: Output the extracted text
        System.out.println("ROI text:");
        System.out.println(result.getText());
    }
}
```

> **Catatan:** Ganti `YOUR_DIRECTORY` dengan jalur absolut ke gambar faktur Anda. Jika Anda menggunakan jalur relatif, pastikan direktori kerja sesuai dengan tempat Anda menjalankan perintah `java`.

## Pertanyaan Umum & Kasus Tepi

### Bagaimana jika ukuran faktur berubah?

Anda dapat menghitung ROI secara dinamis:

```java
int imgWidth = engine.getImage().getWidth();
int imgHeight = engine.getImage().getHeight();

int headerHeight = imgHeight / 10;
int totalHeight = imgHeight / 8;

OcrRegion region = OcrRegion.builder()
        .addRectangle(0, 0, imgWidth, headerHeight)
        .addRectangle(0, imgHeight - totalHeight, imgWidth, totalHeight)
        .build();
```

### Bagaimana cara menangani banyak bahasa?

Aspose OCR mendukung paket bahasa. Cukup atur bahasa sebelum memanggil `recognize()`:

```java
engine.setLanguage(OcrLanguage.Spanish); // or OcrLanguage.English, etc.
```

### Bagaimana jika OCR mengembalikan string kosong?

Penyebab umum adalah:

- Resolusi gambar rendah (< 300 DPI). Perbesar atau minta pemindaian dengan kualitas lebih tinggi.
- Latar belakang terlalu gelap atau terlalu terang. Terapkan filter peningkatan kontras sederhana sebelum OCR.
- Koordinat ROI yang salah sehingga tidak menangkap teks sama sekali.

## Tips untuk OCR Siap Produksi

1. **Batch Processing:** Bungkus logika dalam loop yang mengiterasi direktori berkas faktur. Catat setiap hasil untuk auditabilitas.
2. **Error Handling:** Tangkap `OcrException` untuk melewati gambar yang rusak secara elegan tanpa menghentikan seluruh pekerjaan.
3. **Performance:** Gunakan kembali satu instance `OcrEngine` untuk beberapa gambar; membuat engine baru per file menambah beban yang tidak perlu.
4. **Validation:** Setelah ekstraksi, jalankan pemeriksaan regex pada total jumlah (`\$\d{1,3}(,\d{3})*(\.\d{2})?`) untuk memastikan angka terlihat realistis.

Menerapkan saran-saran ini mengubah **java ocr example** sederhana menjadi solusi yang kuat dan skalabel bagi bisnis mana pun yang perlu **memproses gambar faktur** setiap malam.

## Kesimpulan

Kami baru saja membahas cara **mengekstrak teks dari gambar** di Java menggunakan Aspose OCR, dengan fokus pada skenario pemrosesan faktur yang praktis. Dengan mendefinisikan region of interest, menjalankan engine OCR, dan mencetak **teks OCR output**, Anda kini memiliki fondasi yang kuat untuk membangun pipeline penangkapan data otomatis.

Langkah selanjutnya? Coba perluas ROI untuk mencakup tabel item baris, bereksperimen dengan pengaturan bahasa yang berbeda, atau alirkan string yang diekstrak ke perpustakaan pembuatan PDF untuk dokumen yang dapat dicari. Tidak ada batasan ketika Anda menggabungkan OCR dengan alat Java modern.

Ada pertanyaan lebih lanjut tentang **cara mengekstrak teks** dari tipe dokumen lain, atau butuh bantuan menyesuaikan ROI untuk tata letak yang tidak biasa? Tinggalkan komentar di bawah—selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}