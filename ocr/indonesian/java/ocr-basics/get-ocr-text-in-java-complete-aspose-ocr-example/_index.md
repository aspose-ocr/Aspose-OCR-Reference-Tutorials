---
category: general
date: 2026-01-07
description: Dapatkan teks OCR dari gambar menggunakan Aspose OCR Java. Pelajari cara
  mengekstrak teks gambar, memuat OCR gambar, dan menjalankan contoh OCR Java dalam
  hitungan menit.
draft: false
keywords:
- get OCR text
- extract text image
- java OCR example
- aspose OCR Java
- load image OCR
language: id
og_description: Dapatkan teks OCR dari gambar dengan Aspose OCR Java. Panduan ini
  menunjukkan contoh OCR Java, cara mengekstrak teks dari gambar, dan cara memuat
  OCR gambar secara efisien.
og_title: Dapatkan Teks OCR di Java – Tutorial Lengkap Aspose OCR
tags:
- OCR
- Java
- Aspose
- Image Processing
title: Dapatkan Teks OCR di Java – Contoh Lengkap Aspose OCR
url: /id/java/ocr-basics/get-ocr-text-in-java-complete-aspose-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Dapatkan Teks OCR di Java – Contoh Lengkap Aspose OCR

Pernahkah Anda perlu **mengambil teks OCR** dari dokumen yang dipindai tetapi tidak yakin pustaka mana yang harus dipilih? Anda tidak sendirian. Dalam banyak proyek dunia nyata—seperti otomatisasi faktur, pemrosesan kwitansi, atau digitalisasi formulir multibahasa—mengekstrak teks dari gambar adalah langkah pertama menuju otomatisasi.  

Dalam tutorial ini kami akan membahas **contoh java OCR** yang menggunakan pustaka Aspose OCR untuk Java. Pada akhir tutorial Anda akan tahu cara **memuat OCR gambar**, menjalankan engine, dan **mengekstrak teks gambar** dengan hanya beberapa baris kode. Tanpa basa‑basi, hanya solusi praktis yang dapat Anda salin‑tempel ke dalam proyek Anda sendiri.

## Apa yang Akan Anda Pelajari

- Cara menyiapkan Aspose OCR untuk Java (termasuk koordinat Maven).  
- Langkah tepat untuk **memuat OCR gambar** dan menentukan bahasa.  
- Cara **mengambil teks OCR** sebagai string biasa dan mencetaknya ke konsol.  
- Tips menangani gambar multibahasa dan deteksi otomatis bahasa.  

*Prasyarat*: Java 8 atau lebih baru, IDE yang kompatibel dengan Maven (IntelliJ IDEA, Eclipse, atau VS Code), dan lisensi Aspose OCR untuk Java yang valid (versi percobaan gratis dapat digunakan untuk evaluasi).

---

![Flowchart showing how to get OCR text from an image using Aspose OCR Java](https://example.com/ocr-flowchart.png "Get OCR text flow diagram")

## Langkah 1 – Tambahkan Dependensi Aspose OCR (Memuat OCR Gambar)

Pertama, beri tahu Maven untuk mengunduh pustaka Aspose OCR. Buka file `pom.xml` Anda dan sisipkan blok `<dependency>` berikut di dalam `<dependencies>`:

```xml
<!-- Aspose OCR for Java -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- Use the latest version available -->
</dependency>
```

> **Tip pro**: Jika Anda menggunakan Gradle, setaraannya adalah `implementation 'com.aspose:aspose-ocr:23.9'`. Menambahkan dependensi adalah cara termurah untuk **memuat kemampuan OCR gambar** ke dalam proyek Anda.

## Langkah 2 – Buat Engine OCR dan Muat Gambar Anda

Sekarang kami akan menulis kelas Java kecil yang membuat instance `OcrEngine`, menunjuk ke file gambar, dan memberi tahu engine bahasa apa yang harus dikenali. Bahasa diidentifikasi dengan kode ISO‑639‑2‑nya (misalnya `"tam"` untuk Tamil).

```java
package com.example.ocr;

import com.aspose.ocr.*;

public class LanguageExample {

    public static void main(String[] args) throws Exception {
        // 2️⃣ Initialize the OCR engine
        OcrEngine engine = new OcrEngine();

        // 2️⃣ Load the image you want to process – this is the "load image OCR" step
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/multilingual.png"));

        // 2️⃣ Choose the language (ISO‑639‑2). Change "tam" to any supported code.
        engine.getEngineOptions().setLanguage("tam");
        // If you prefer automatic detection, uncomment the next line:
        // engine.getEngineOptions().setAutoDetectLanguage(true);
```

### Mengapa mengatur bahasa secara eksplisit?

Menentukan bahasa mengurangi hasil positif palsu dan mempercepat proses pengenalan. Untuk PDF multibahasa Anda dapat melakukan loop pada array kode bahasa, atau mengaktifkan deteksi otomatis untuk kemudahan.

## Langkah 3 – Jalankan Proses OCR dan **Dapatkan Teks OCR**

Dengan engine yang sudah dikonfigurasi, baris berikutnya benar‑benarnya melakukan pengenalan. Objek hasil berisi string yang diekstrak serta metadata tambahan.

```java
        // 3️⃣ Perform OCR – this is where we finally **get OCR text**
        OcrResult result = engine.recognize();

        // 3️⃣ Output the recognized text to the console
        System.out.println("=== Extracted Text ===");
        System.out.println(result.getText());
    }
}
```

Saat Anda menjalankan `LanguageExample`, Anda akan melihat sesuatu seperti:

```
=== Extracted Text ===
தமிழ் உரை இங்கு வருகிறது...
```

Jika Anda menggunakan `setAutoDetectLanguage(true)`, engine akan mencoba menebak bahasa untuk Anda, yang sangat berguna saat menangani dokumen yang tidak diketahui.

## Langkah 4 – Menangani Kasus Pinggiran Umum (Variasi Ekstraksi Teks Gambar)

### Menangani Gambar Resolusi Rendah

Akurasi OCR turun drastis di bawah 300 dpi. Jika gambar sumber Anda beresolusi rendah, pertimbangkan untuk meningkatkan resolusinya terlebih dahulu:

```java
engine.getEngineOptions().setResolution(300); // forces 300 DPI
```

### Menghapus Noise Latar Belakang

Kadang‑kadang formulir yang dipindai memiliki bintik‑bintik yang membingungkan engine. Anda dapat mengaktifkan pra‑pemrosesan:

```java
engine.getEngineOptions().setPreprocessMode(EngineOptions.PreprocessMode.Auto);
```

### Mengekstrak Teks Dari Region Spesifik

Jika Anda hanya membutuhkan teks dari persegi panjang tertentu (misalnya sel tabel), atur `Rectangle` sebelum memanggil `recognize()`:

```java
engine.setRegion(new Rectangle(50, 100, 400, 200));
```

Penyesuaian ini membuat **contoh java OCR** Anda cukup kuat untuk beban kerja produksi.

## Langkah 5 – Verifikasi Output (Apa yang Harus Anda Harapkan?)

Eksekusi yang berhasil akan mencetak versi teks biasa dari gambar. Untuk gambar multibahasa Anda mungkin melihat campuran skrip:

```
Hello World
こんにちは世界
مرحبا بالعالم
```

Jika output kosong atau berantakan, periksa kembali:

1. Jalur file di `setImage` (apakah sudah benar?).  
2. Kode bahasa cocok dengan skrip di gambar.  
3. Kualitas gambar (kontras, DPI) cukup memadai.

## Contoh Lengkap yang Berfungsi (Siap Salin‑Tempel)

Berikut adalah seluruh file, siap untuk dikompilasi dan dijalankan. Ganti `YOUR_DIRECTORY/multilingual.png` dengan jalur aktual ke gambar uji Anda.

```java
package com.example.ocr;

import com.aspose.ocr.*;

public class LanguageExample {
    public static void main(String[] args) throws Exception {
        // Initialize OCR engine
        OcrEngine engine = new OcrEngine();

        // Load the image – this is the core "load image OCR" step
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/multilingual.png"));

        // Set language (ISO‑639‑2). For Tamil use "tam". Change as needed.
        engine.getEngineOptions().setLanguage("tam");
        // Uncomment for auto‑detect:
        // engine.getEngineOptions().setAutoDetectLanguage(true);

        // Optional: improve accuracy on low‑res images
        // engine.getEngineOptions().setResolution(300);
        // engine.getEngineOptions().setPreprocessMode(EngineOptions.PreprocessMode.Auto);

        // Perform OCR and retrieve text
        OcrResult result = engine.recognize();

        // Print the extracted text – this is how we **get OCR text**
        System.out.println("=== Extracted Text ===");
        System.out.println(result.getText());
    }
}
```

Kompilasi dan jalankan:

```bash
mvn compile exec:java -Dexec.mainClass="com.example.ocr.LanguageExample"
```

Anda sekarang seharusnya melihat konten yang diekstrak tercetak di konsol Anda.

---

## Kesimpulan

Kami baru saja menunjukkan kepada Anda **cara mendapatkan teks OCR** dari sebuah gambar menggunakan Aspose OCR untuk Java. Dengan mengikuti **contoh java OCR** ini, Anda dapat **mengekstrak data teks gambar**, **memuat OCR gambar**, dan bahkan menyesuaikan engine untuk input multibahasa atau berisik.  

Dari sini Anda dapat:

- Mengintegrasikan langkah OCR ke dalam alur kerja yang lebih besar (misalnya, menyimpan teks ke dalam basis data).  
- Menggabungkannya dengan API terjemahan untuk mengubah pemindaian multibahasa menjadi satu bahasa.  
- Bereksperimen dengan fitur Aspose OCR lainnya seperti konversi PDF atau deteksi barcode.

Cobalah, pecahkan beberapa hal, lalu sesuaikan pengaturan hingga outputnya sempurna. Selamat coding, semoga OCR Anda selalu jernih!  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}