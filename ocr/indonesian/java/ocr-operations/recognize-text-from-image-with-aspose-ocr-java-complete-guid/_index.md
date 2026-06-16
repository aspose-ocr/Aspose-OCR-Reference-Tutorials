---
category: general
date: 2026-03-18
description: Pelajari cara mengenali teks dari gambar di Java menggunakan Aspose OCR.
  Tutorial langkah demi langkah ini menunjukkan cara memuat gambar untuk OCR dan mematikan
  korektor ejaan.
draft: false
keywords:
- recognize text from image
- load image for ocr
- aspose ocr java example
- extract text from image
- turn off spell corrector
language: id
og_description: Mengenali teks dari gambar di Java menggunakan Aspose OCR. Pelajari
  cara memuat gambar untuk OCR dan menonaktifkan korektor ejaan dalam tutorial praktis
  ini.
og_title: Mengenali Teks dari Gambar dengan Aspose OCR Java – Panduan Lengkap
tags:
- Aspose OCR
- Java
- Image Processing
title: Mengenali Teks dari Gambar dengan Aspose OCR Java – Panduan Lengkap
url: /id/java/ocr-operations/recognize-text-from-image-with-aspose-ocr-java-complete-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Mengenali Teks dari Gambar dengan Aspose OCR Java – Panduan Lengkap

Pernah membutuhkan untuk **mengenali teks dari gambar** tetapi tidak yakin pustaka mana yang harus dipilih? Anda tidak sendirian. Dalam banyak proyek dunia nyata—misalnya memindai struk, mendigitalisasi formulir, atau mengambil keterangan dari tangkapan layar—mendapatkan teks mentah yang bersih dari bitmap adalah pekerjaan harian.  

Dalam tutorial ini kami akan membimbing Anda melalui contoh **Aspose OCR Java** yang praktis yang menunjukkan secara tepat cara **memuat gambar untuk OCR**, menjalankan mesin, dan bahkan **menonaktifkan spell corrector** ketika Anda memerlukan karakter yang tidak diubah. Pada akhir tutorial Anda akan memiliki program yang dapat dijalankan yang mengekstrak teks dari gambar tanpa modifikasi yang tidak diinginkan.

## Apa yang Akan Anda Dapatkan

- Gambaran jelas tentang alur kerja **Aspose OCR** untuk Java.
- Kode tepat yang diperlukan untuk **mengenali teks dari gambar** dan **mengekstrak teks dari gambar** dalam bentuk aslinya.
- Tips kapan Anda mungkin ingin menonaktifkan spell corrector bawaan dan cara melakukannya dengan aman.
- Pemeriksaan cepat yang dapat Anda jalankan untuk memverifikasi output sesuai harapan.

### Prasyarat (minimum yang diperlukan)

- Java 8 atau lebih baru terpasang di mesin Anda.
- Maven atau Gradle untuk manajemen dependensi (kami akan menunjukkan cuplikan Maven).
- File JAR `Aspose.OCR` (Anda dapat mengunduh trial gratis dari situs Aspose).
- File gambar (PNG, JPG, BMP, dll.) yang berisi teks yang ingin Anda baca. Untuk demo kami akan menggunakan `mixed-lang.png`.

> **Tip pro:** Jika Anda berencana memproses banyak gambar, pertimbangkan memuatnya sebagai stream untuk menghindari kebocoran handle file.

![Diagram yang menunjukkan alur OCR – mengenali teks dari gambar](ocr-pipeline.png)

*Alt text: diagram illustrating the steps to recognize text from image using Aspose OCR.*

## Langkah 1 – Siapkan Proyek dan Tambahkan Dependensi Aspose OCR

Sebelum kita dapat memanggil metode OCR apa pun, pustaka harus berada di classpath. Jika Anda menggunakan Maven, letakkan ini di dalam `pom.xml` Anda:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- Use the latest stable version -->
</dependency>
```

Jika Anda lebih suka Gradle, setaraannya adalah:

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

Setelah dependensi terresolusi, Anda dapat mengimpor dua kelas yang akan kita gunakan:

```java
import com.aspose.ocr.OcrEngine;
import com.aspose.ocr.Image;
```

> **Mengapa ini penting:** Menambahkan JAR melalui alat build menjamin versi yang tepat digunakan di semua lingkungan, yang menghilangkan masalah “class not found” di kemudian hari.

## Langkah 2 – Buat Engine OCR dan Nonaktifkan Spell Corrector

Aspose OCR dilengkapi dengan spell corrector bawaan yang mencoba menebak apa yang Anda maksudkan. Itu bagus untuk dokumen bersih, tetapi jika Anda memindai tanda multibahasa atau potongan kode, Anda akan mendapatkan “koreksi” yang tidak diinginkan. Berikut cara menonaktifkannya:

```java
// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Disable the automatic spell correction
ocrEngine.getSpellCorrector().setEnabled(false);
```

**Apa yang terjadi di balik layar?** Objek `SpellCorrector` menjalankan proses berbasis kamus setelah glyph mentah didekode. Dengan memanggil `setEnabled(false)`, kami memberi tahu mesin untuk melewatkan proses tersebut, sehingga urutan karakter yang terdeteksi tetap dipertahankan.

## Langkah 3 – Muat Gambar untuk OCR

Sekarang kita benar‑benar **memuat gambar untuk OCR**. Metode `Image.load` milik Aspose menerima jalur file, `InputStream`, atau bahkan array byte. Untuk kesederhanaan kita akan menggunakan jalur file:

```java
// Replace the path with the location of your image file
Image inputImage = Image.load("YOUR_DIRECTORY/mixed-lang.png");
```

> **Kasus khusus:** Jika gambar lebih besar dari 5 MB, pertimbangkan untuk memperkecilnya terlebih dahulu. Gambar besar meningkatkan konsumsi memori dan dapat memperlambat mesin pengenalan.

## Langkah 4 – Kenali Teks dan Tangkap Output Mentah

Dengan engine siap dan gambar berada di memori, pengenalan sebenarnya cukup satu baris:

```java
// Perform OCR and store the raw text
String rawText = ocrEngine.recognize(inputImage);
```

Metode `recognize` mengembalikan `String` yang berisi **mengekstrak teks dari gambar** persis seperti yang dilihat mesin—tanpa spell‑checking, tanpa pasca‑pemrosesan.

## Langkah 5 – Tampilkan Hasil (Tanpa Spell‑Check)

Akhirnya, mari cetak output OCR mentah ke konsol sehingga Anda dapat memverifikasinya:

```java
System.out.println("Raw OCR (no spell‑check):\n" + rawText);
```

Saat Anda menjalankan program, Anda akan melihat sesuatu seperti:

```
Raw OCR (no spell‑check):
Hello, 世界!
12345
```

Jika gambar berisi bahasa campuran atau simbol khusus, mereka akan muncul tidak berubah karena kami menonaktifkan spell corrector.

## Contoh Lengkap yang Dapat Dijalankan

Menggabungkan semua bagian, berikut **contoh lengkap Aspose OCR Java** yang dapat Anda salin‑tempel ke file `SpellCorrectionDemo.java`:

```java
import com.aspose.ocr.OcrEngine;
import com.aspose.ocr.Image;

public class SpellCorrectionDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Turn off the built‑in spell corrector
        ocrEngine.getSpellCorrector().setEnabled(false);

        // Step 3: Load the image you want to recognize
        Image inputImage = Image.load("YOUR_DIRECTORY/mixed-lang.png");

        // Step 4: Run OCR on the image and obtain the raw text
        String rawText = ocrEngine.recognize(inputImage);

        // Step 5: Display the OCR result without spell‑checking
        System.out.println("Raw OCR (no spell‑check):\n" + rawText);
    }
}
```

### Cara Menjalankan

1. Simpan file sebagai `SpellCorrectionDemo.java`.
2. Kompilasi: `javac -cp "path/to/aspose-ocr-23.9.jar" SpellCorrectionDemo.java`
3. Jalankan: `java -cp ".;path/to/aspose-ocr-23.9.jar" SpellCorrectionDemo`

Ganti `path/to` dengan lokasi sebenarnya dari file JAR Aspose di sistem Anda.

## Pertanyaan Umum & Hal-hal yang Perlu Diwaspadai

### Bagaimana jika gambar berada dalam format berbeda (misalnya PDF)?

Aspose OCR juga dapat membaca halaman PDF secara langsung, tetapi Anda harus mengonversi halaman PDF ke gambar terlebih dahulu atau menggunakan overload `OcrEngine.recognizePdf`. Itu merupakan tutorial terpisah, namun prinsip **mengenali teks dari gambar** tetap berlaku.

### Apakah menonaktifkan spell corrector memengaruhi kinerja?

Sedikit. Melewatkan proses kamus menghemat beberapa milidetik per halaman, yang dapat terakumulasi saat memproses ribuan file. Trade‑off‑nya adalah kehilangan perbaikan typo otomatis—jadi putuskan berdasarkan kualitas data Anda.

### Bisakah saya tetap mendapatkan hasil spesifik bahasa?

Ya. Engine secara otomatis mendeteksi skrip, tetapi Anda dapat memaksa bahasa dengan memanggil `ocrEngine.setLanguage(OcrEngine.Language.English)`, misalnya. Ini berguna ketika Anda tahu gambar hanya berisi satu bahasa dan ingin meningkatkan akurasi.

### Bagaimana cara menangani TIFF multi‑halaman?

Anggap setiap halaman sebagai objek `Image` terpisah: `Image.load("file.tif", pageIndex)`. Loop melalui halaman‑halaman, kenali masing‑masing, dan gabungkan hasilnya.

## Tips Pro untuk Proyek Dunia Nyata

- **Batch processing:** Bungkus logika OCR dalam metode yang menerima `InputStream`. Ini memungkinkan Anda streaming gambar dari S3, Azure Blob, atau penyimpanan lain tanpa menyentuh sistem file.
- **Memory management:** Panggil `ocrEngine.dispose()` setelah selesai untuk membebaskan sumber daya native.
- **Logging:** Tangkap output mentah ke file log untuk jejak audit—terutama penting ketika Anda telah menonaktifkan spell correction.
- **Testing:** Tulis unit test yang memberi gambar known dan memeriksa string mentah yang diharapkan. Ini menjamin upgrade pustaka di masa depan tidak mengubah perilaku secara diam‑diam.

## Kesimpulan

Kami baru saja menunjukkan cara **mengenali teks dari gambar** menggunakan Aspose OCR untuk Java, cara **memuat gambar untuk OCR**, dan langkah tepat untuk **menonaktifkan spell corrector** ketika Anda memerlukan karakter yang tidak diubah. Potongan kode singkat dan mandiri di atas siap disisipkan ke proyek Java apa pun, dan penjelasannya memberi Anda “mengapa” di balik setiap baris.

Selanjutnya, Anda mungkin ingin menjelajahi **mengekstrak teks dari gambar** secara massal, bereksperimen dengan petunjuk bahasa, atau mengintegrasikan output ke indeks pencarian. Apa pun yang Anda pilih, dasar‑dasar yang dibahas di sini akan menjaga pipeline OCR Anda andal dan mudah dipelihara.

Ada variasi yang Anda coba? Silakan tinggalkan komentar atau bagikan **contoh Aspose OCR Java** Anda sendiri. Selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}