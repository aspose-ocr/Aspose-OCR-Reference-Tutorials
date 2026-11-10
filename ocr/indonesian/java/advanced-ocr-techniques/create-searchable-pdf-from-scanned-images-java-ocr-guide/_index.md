---
category: general
date: 2026-06-22
description: Buat PDF yang dapat dicari di Java dengan Aspose OCR. Pelajari cara mengonversi
  PDF yang dipindai, menangani OCR bahasa campuran, dan meningkatkan akurasi.
draft: false
keywords:
- create searchable pdf
- convert scanned pdf
- how to ocr document
- mixed language ocr
- aspose ocr java
language: id
og_description: Buat PDF yang dapat dicari di Java menggunakan Aspose OCR. Tutorial
  ini menunjukkan cara melakukan OCR pada dokumen, menangani teks dengan bahasa campuran,
  dan menghasilkan PDF yang dapat dicari.
og_title: Buat PDF yang Dapat Dicari dari Gambar Pindai – Panduan OCR Java
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Create searchable PDF in Java with Aspose OCR. Learn how to convert
    scanned PDF, handle mixed language OCR and boost accuracy.
  headline: Create Searchable PDF from Scanned Images – Java OCR Guide
  type: TechArticle
- description: Create searchable PDF in Java with Aspose OCR. Learn how to convert
    scanned PDF, handle mixed language OCR and boost accuracy.
  name: Create Searchable PDF from Scanned Images – Java OCR Guide
  steps:
  - name: Expected Output
    text: 'When you open `processed.pdf` in Adobe Reader (or any PDF viewer), you
      should be able to:'
  - name: 1. What if my document contains more than two languages?
    text: '`config.setLanguage` accepts a var‑args list, so you can pass as many `OcrLanguage`
      constants as you need:'
  - name: 2. Can I run this on a headless server without a GPU?
    text: Absolutely. Set `config.setUseGpu(false)` or simply omit the call. The engine
      will fall back to multi‑core CPU processing, which is still fast thanks to the
      thread pool we configured.
  - name: 3. How do I handle huge PDFs (hundreds of pages)?
    text: Aspose OCR streams pages one‑by‑one, so memory usage stays modest. However,
      you might want to split the PDF into smaller chunks using Aspose PDF’s `split`
      method, process each chunk, then merge the results back together.
  - name: 4. Is there a way to keep the original PDF’s metadata (author, creation
      date)?
    text: 'Yes. After you obtain `searchablePdf`, you can copy metadata from the original
      PDF:'
  type: HowTo
tags:
- OCR
- Java
- PDF
title: Buat PDF yang Dapat Dicari dari Gambar Pindai – Panduan OCR Java
url: /id/java/advanced-ocr-techniques/create-searchable-pdf-from-scanned-images-java-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Membuat PDF yang Dapat Dicari dari Gambar yang Dipindai – Panduan OCR Java

Pernah bertanya-tanya bagaimana cara **membuat PDF yang dapat dicari** dari tumpukan halaman yang dipindai tanpa mengeluarkan banyak uang untuk layanan pihak ketiga? Anda tidak sendirian. Banyak pengembang mengalami hal yang sama ketika mereka perlu **mengonversi PDF yang dipindai** menjadi sesuatu yang dapat dicari oleh pengguna mereka.  

Dalam panduan ini kami akan menelusuri contoh lengkap yang dapat dijalankan yang menggunakan **Aspose OCR untuk Java** untuk **cara OCR dokumen**‑level, menangani **OCR bahasa campuran**, dan akhirnya menghasilkan PDF yang dapat dicari dengan rapi. Pada akhir tutorial Anda akan memiliki program mandiri yang dapat dimasukkan ke dalam proyek Maven atau Gradle mana pun dan mulai memproses dokumen hari ini.

## Prasyarat – Apa yang Anda Butuhkan

Sebelum kita masuk ke kode, pastikan Anda memiliki hal‑hal berikut:

- Java 17 (atau JDK terbaru lainnya) terpasang dan dikonfigurasi pada PATH Anda.  
- IDE atau editor yang Anda nyaman gunakan (IntelliJ IDEA, Eclipse, VS Code…).  
- Pustaka Aspose.OCR untuk Java – Anda dapat mengunduh JAR terbaru dari [Aspose Maven repository](https://repo.aspose.com/repo/com/aspose/aspose-ocr/).  
- PDF yang dipindai multi‑halaman yang ingin Anda ubah menjadi dapat dicari.  
- (Opsional) Mesin dengan GPU jika Anda berencana menggunakan `setUseGpu(true)` untuk pemrosesan lebih cepat.

Memiliki semua komponen ini siap berarti Anda dapat menyalin‑tempel kode di bawah ini dan menekan **Run** tanpa harus mencari ketergantungan yang hilang.

## Langkah 1: Siapkan Proyek dan Impor Aspose OCR

Pertama, buat modul Maven baru (atau proyek Gradle) dan tambahkan dependensi Aspose OCR:

```xml
<!-- pom.xml snippet -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- replace with the latest version -->
</dependency>
```

Jika Anda lebih suka Gradle, baris yang setara adalah:

```gradle
implementation 'com.aspose:aspose-ocr:23.10'
```

Setelah proses sinkronisasi build selesai, Anda akan dapat mengimpor kelas‑kelas yang diperlukan.

## Langkah 2: Inisialisasi Mesin OCR

Membuat mesin ini sangat sederhana, namun penting untuk memahami mengapa kita melakukannya di awal. Objek `OcrEngine` menyimpan konfigurasi, threading, dan pengaturan GPU yang memengaruhi setiap operasi selanjutnya.

```java
import com.aspose.ocr.*;

public class AdvancedOcr {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine – this is the heart of the create searchable pdf process
        OcrEngine ocrEngine = new OcrEngine();
```

> **Pro tip:** Menginstansiasi mesin sekali dan menggunakannya kembali untuk banyak file mengurangi overhead, terutama saat Anda memproses batch PDF.

## Langkah 3: Muat PDF yang Dipindai (atau Stream Gambar)

Aspose OCR bekerja dengan stream gambar, jadi kami memberi masukan PDF yang dipindai secara langsung. Pustaka ini secara internal meraster setiap halaman, itulah mengapa Anda dapat memulai dari PDF dan berakhir dengan PDF yang dapat dicari dalam satu langkah.

```java
        // Load the source PDF – replace the path with your actual file location
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/multi_page_scanned.pdf"));
```

Jika Anda memiliki koleksi TIFF atau JPEG sebagai gantinya, cukup arahkan `ImageStream.fromFile` ke file‑file tersebut; sisa pipeline tetap sama.

## Langkah 4: Sesuaikan Pengaturan OCR untuk Dukungan Bahasa Campuran

Di sinilah **OCR bahasa campuran** bersinar. Dengan memberikan beberapa enum `OcrLanguage` Anda memberi tahu mesin untuk mencari bahasa Inggris dan Rusia (atau kombinasi lain) pada halaman yang sama.

```java
        // Grab the mutable config object
        OcrConfig config = ocrEngine.getConfig();

        // Enable English + Russian detection – you can add more languages as needed
        config.setLanguage(OcrLanguage.ENGLISH, OcrLanguage.RUSSIAN);

        // Speed vs. accuracy trade‑off: use all available cores
        config.setThreadCount(Runtime.getRuntime().availableProcessors());

        // Turn on GPU acceleration if the runtime detects a compatible device
        config.setUseGpu(true);

        // Spell‑check improves accuracy for noisy scans
        config.setEnableSpellCorrection(true);

        // Tell Aspose we want a searchable PDF as the final output
        config.setOutputFormat(OcrOutputFormat.PDF_SEARCHABLE);
```

> **Mengapa ini penting:** Tanpa menentukan bahasa, mesin secara default hanya menggunakan bahasa Inggris, yang secara drastis menurunkan tingkat pengenalan untuk dokumen yang mengandung Cyrillic atau skrip lain.

## Langkah 5: Tambahkan Filter Pra‑Pemrosesan untuk Membersihkan Hasil Pindai

PDF yang dipindai sering mengalami kemiringan, bintik‑bintik, atau kontras rendah. Menambahkan `DeskewFilter` dan `DenoiseFilter` membantu mesin OCR melihat karakter dengan lebih jelas.

```java
        // Set up image preprocessing
        ImagePreprocessOptions preprocess = new ImagePreprocessOptions();
        preprocess.addFilter(new DeskewFilter());   // Straighten tilted pages
        preprocess.addFilter(new DenoiseFilter()); // Reduce background noise
        ocrEngine.setPreprocessOptions(preprocess);
```

Anda dapat menambahkan filter lain—seperti `ContrastFilter` atau `BinarizationFilter`—jika materi sumber Anda sangat kotor.

## Langkah 6: Jalankan OCR dan Hasilkan PDF yang Dapat Dicari

Sekarang pekerjaan berat dimulai. Pemanggilan `recognizeToPdf()` menjalankan pipeline OCR, menerapkan langkah pra‑pemrosesan, dan menulis teks yang dikenali ke dalam lapisan teks tak terlihat di dalam PDF.

```java
        // Perform OCR and retrieve a searchable PDF document object
        PdfDocument searchablePdf = ocrEngine.recognizeToPdf();
```

Objek `PdfDocument` yang dikembalikan adalah objek Aspose PDF lengkap, artinya Anda dapat mengedit metadata lebih lanjut, menambahkan bookmark, atau menggabungkannya dengan PDF lain sebelum menyimpan.

## Langkah 7: Simpan Hasil dan Verifikasi

Akhirnya, simpan output ke disk. Pesan di konsol memberi Anda petunjuk visual cepat bahwa semuanya berhasil.

```java
        // Save the searchable PDF to the desired location
        searchablePdf.save("YOUR_DIRECTORY/processed.pdf");
        System.out.println("OCR completed – searchable PDF saved at YOUR_DIRECTORY/processed.pdf");
    }
}
```

### Output yang Diharapkan

Saat Anda membuka `processed.pdf` di Adobe Reader (atau penampil PDF apa pun), Anda seharusnya dapat:

1. **Memilih teks** – klik dan seret pada kata apa pun lalu salin.  
2. **Mencari** – tekan `Ctrl+F` dan ketik frasa yang muncul di salah satu scan asli.  
3. **Mempertahankan tata letak asli** – tampilan visual tetap identik dengan sumber yang dipindai; hanya lapisan teks tak terlihat yang ditambahkan.

Jika Anda melihat karakter yang rusak atau halaman yang hilang, periksa kembali pengaturan bahasa dan pastikan PDF sumber tidak diproteksi dengan kata sandi.

## Pertanyaan Umum & Kasus Tepi

### 1. Bagaimana jika dokumen saya berisi lebih dari dua bahasa?

`config.setLanguage` menerima daftar var‑args, jadi Anda dapat memasukkan sebanyak mungkin konstanta `OcrLanguage` yang diperlukan:

```java
config.setLanguage(OcrLanguage.ENGLISH, OcrLanguage.RUSSIAN, OcrLanguage.CHINESE_SIMPLIFIED);
```

Ingat bahwa setiap bahasa tambahan sedikit meningkatkan waktu pemrosesan.

### 2. Bisakah saya menjalankan ini di server tanpa tampilan (headless) tanpa GPU?

Tentu saja. Setel `config.setUseGpu(false)` atau cukup hilangkan pemanggilan tersebut. Mesin akan beralih ke pemrosesan CPU multi‑core, yang tetap cepat berkat thread pool yang kami konfigurasikan.

### 3. Bagaimana cara menangani PDF besar (ratusan halaman)?

Aspose OCR mem‑stream halaman satu‑per‑satu, sehingga penggunaan memori tetap wajar. Namun, Anda mungkin ingin membagi PDF menjadi bagian‑bagian lebih kecil menggunakan metode `split` pada Aspose PDF, memproses tiap bagian, lalu menggabungkan hasilnya kembali.

### 4. Apakah ada cara untuk mempertahankan metadata PDF asli (penulis, tanggal pembuatan)?

Ya. Setelah Anda memperoleh `searchablePdf`, Anda dapat menyalin metadata dari PDF asli:

```java
PdfDocument original = new PdfDocument("YOUR_DIRECTORY/multi_page_scanned.pdf");
searchablePdf.getInfo().setAuthor(original.getInfo().getAuthor());
// repeat for other metadata fields
```

## Tips Pro untuk OCR Siap Produksi

- **Pemrosesan batch:** Bungkus seluruh alur dalam loop yang mengiterasi direktori berisi file. Gunakan satu instance `OcrEngine` untuk menghindari inisialisasi berulang.  
- **Penanganan error:** Tangkap `OcrException` untuk mencatat file yang gagal, lalu lanjutkan ke dokumen berikutnya.  
- **Pemantauan kinerja:** Gunakan `System.nanoTime()` sebelum dan sesudah `recognizeToPdf()` untuk mencatat waktu pemrosesan per file; ini membantu Anda memutuskan apakah perlu menambah worker pool di cloud.  
- **Keamanan:** Jika Anda menangani dokumen sensitif, pertimbangkan mengenkripsi PDF output dengan `searchablePdf.encrypt(...)` sebelum menyimpan.

## Kesimpulan

Kami baru saja membahas semua yang Anda perlukan untuk **membuat PDF yang dapat dicari** dari sumber yang dipindai menggunakan **Aspose OCR untuk Java**. Tutorial ini menunjukkan cara **mengonversi PDF yang dipindai**, mengonfigurasi **OCR bahasa campuran**, dan menyesuaikan filter pra‑pemrosesan—semua sambil menjaga kode tetap ringkas dan siap produksi.  

Selanjutnya Anda dapat mengeksplorasi menambahkan thumbnail yang dihasilkan OCR, mengintegrasikan dengan sistem manajemen dokumen, atau bahkan mengirim teks yang diekstrak ke indeks pencarian seperti Elasticsearch. Kemungkinannya seluas dokumen yang perlu Anda digitalisasi.

Punya pertanyaan lebih lanjut tentang **cara OCR dokumen** di Java, atau ingin melihat pembahasan lebih mendalam tentang manipulasi PDF? Tinggalkan komentar di bawah, dan selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Mengenali Teks PDF – Operasi OCR dengan Aspose.OCR untuk Java](/ocr/english/java/ocr-operations/)
- [OCR Mengenali Dokumen PDF dalam Aspose.OCR untuk Java](/ocr/english/java/ocr-operations/recognize-pdf/)
- [Cara OCR PDF di .NET dengan Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}