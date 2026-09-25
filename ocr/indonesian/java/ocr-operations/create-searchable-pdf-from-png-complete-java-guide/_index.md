---
category: general
date: 2026-01-07
description: Buat PDF yang dapat dicari dari gambar di Java. Pelajari cara mengonversi
  gambar ke PDF, mengekstrak teks dari gambar, dan mengenali teks dari PNG menggunakan
  Aspose OCR.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- extract text from image
- image to searchable pdf
- recognize text from png
language: id
og_description: Buat PDF yang dapat dicari di Java dengan Aspose OCR. Panduan ini
  menunjukkan cara mengonversi gambar ke PDF, mengekstrak teks dari gambar, dan mengenali
  teks dari PNG.
og_title: Buat PDF yang Dapat Dicari dari PNG – Tutorial Java
tags:
- OCR
- Java
- PDF
title: Buat PDF yang Dapat Dicari dari PNG – Panduan Java Lengkap
url: /id/java/ocr-operations/create-searchable-pdf-from-png-complete-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat PDF yang Dapat Dicari dari PNG – Panduan Java Lengkap

Pernahkah Anda perlu **create searchable pdf** dari gambar yang dipindai tetapi tidak yakin harus mulai dari mana? Anda tidak sendirian—para pengembang sering menemui hal ini saat membangun alur kerja manajemen dokumen. Kabar baik? Dengan beberapa baris Java dan Aspose OCR Anda dapat **convert image to pdf**, menyematkan teks tersembunyi, dan menghasilkan dokumen yang sepenuhnya dapat dicari.

Dalam tutorial ini kami akan membahas seluruh proses: memuat PNG, menjalankan OCR, dan menyimpan hasilnya sebagai PDF yang dapat dicari. Pada akhir tutorial Anda akan dapat **extract text from image** file, mengubahnya menjadi aset **image to searchable pdf**, dan bahkan menangani kasus khusus seperti TIFF multi‑halaman. Tanpa layanan eksternal, hanya kode Java murni yang dapat Anda jalankan hari ini.

## Buat PDF yang Dapat Dicari – Ikhtisar

Sebelum masuk ke kode, mari klarifikasi apa arti “searchable PDF”. PDF yang dapat dicari memiliki dua lapisan:

1. **Visible image layer** – gambar asli (PNG, JPEG, dll.).
2. **Hidden text layer** – teks yang dihasilkan OCR yang berada di belakang gambar, membuat dokumen dapat dicari di semua penampil PDF.

Mengapa perlu kedua lapisan? Gambar mempertahankan tampilan asli, sementara lapisan teks memungkinkan salin‑tempel, pengindeksan, dan pencarian teks penuh. Itulah titik manis untuk pengarsipan, kepatuhan hukum, dan membangun arsip yang dapat dicari.

## Langkah 1: Siapkan Aspose OCR di Proyek Java Anda

Hal pertama yang perlu Anda lakukan—dapatkan pustaka Aspose OCR. Cara termudah adalah menambahkan dependensi Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Check the latest version on Maven Central -->
</dependency>
```

Jika Anda tidak menggunakan Maven, cukup unduh JAR dari situs Aspose dan tambahkan ke classpath Anda. **Pro tip:** pastikan versi pustaka selaras dengan runtime Java Anda (Java 8+ berfungsi baik).

### Mengapa ini penting
Aspose OCR menangani berbagai format gambar dan bahasa secara langsung, jadi Anda tidak perlu menulis kode pemrosesan piksel sendiri. Ia juga menyediakan enum `OcrOutputFormat.PDF` yang akan kita gunakan nanti untuk membuat PDF yang dapat dicari.

## Langkah 2: Muat Gambar yang Ingin Diproses

Selanjutnya, beri tahu mesin OCR file mana yang harus dibaca. API menerima `ImageStream`, yang dapat dibuat dari jalur file, `java.io.InputStream`, atau bahkan array byte.

```java
import com.aspose.ocr.*;

public class PdfOutputExample {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Load the PNG (or any supported image) from disk
        String inputPath = "YOUR_DIRECTORY/input.png"; // replace with your actual path
        ocrEngine.setImage(ImageStream.fromFile(inputPath));
```

Perhatikan kami menggunakan `ImageStream.fromFile`. Jika Anda perlu **convert image to pdf** dari aliran (misalnya, file yang diunggah), Anda dapat mengganti pemanggilan itu dengan `ImageStream.fromInputStream(yourInputStream)`.

### Peringatan kasus tepi
Jika gambar Anda lebih besar dari 10 MB, pertimbangkan untuk memperkecilnya terlebih dahulu. Gambar besar meningkatkan waktu OCR secara dramatis dan dapat menyebabkan error out‑of‑memory pada server dengan sumber daya terbatas.

## Langkah 3: Jalankan OCR dan Tangkap Hasilnya

Sekarang keajaiban terjadi. Memanggil `recognize()` menjalankan algoritma OCR dan mengembalikan objek `OcrResult` yang berisi teks yang dikenali serta informasi tata letak.

```java
        // Perform OCR recognition
        OcrResult ocrResult = ocrEngine.recognize();

        // Optional: print extracted text to console (useful for debugging)
        System.out.println("Extracted Text:");
        System.out.println(ocrResult.getText());
```

Di sini kami juga **extracting text from image** dan mencetaknya. Langkah ini berguna ketika Anda hanya membutuhkan teks mentah tanpa menghasilkan PDF. Objek `ocrResult` yang sama akan dipakai lagi nanti untuk membuat PDF yang dapat dicari.

### Mengapa langkah ini penting
Mesin OCR tidak hanya membaca karakter tetapi juga mempertahankan posisi mereka, yang memungkinkan lapisan teks tersembunyi pada PDF akhir. Melewatkan langkah ini berarti Anda kehilangan kemampuan pencarian.

## Langkah 4: Simpan Hasil sebagai PDF yang Dapat Dicari

Akhirnya, kami memberi tahu Aspose OCR untuk menulis output dalam format PDF. Metode `save` menerima nama file target dan enum `OcrOutputFormat`.

```java
        // Save the OCR result as a searchable PDF (image + hidden text layer)
        String outputPath = "YOUR_DIRECTORY/output.pdf"; // replace with your desired output
        ocrResult.save(outputPath, OcrOutputFormat.PDF);

        System.out.println("Searchable PDF created at: " + outputPath);
    }
}
```

Saat Anda membuka `output.pdf` di Adobe Reader atau penampil PDF modern lainnya, Anda akan melihat PNG asli, tetapi Anda juga dapat mencari kata apa pun yang muncul dalam gambar. Itulah inti dari **create searchable pdf**.

### Variasi yang mungkin Anda butuhkan
- **Beberapa halaman:** Jika Anda memiliki TIFF multi‑halaman, cukup lakukan loop pada setiap halaman, panggil `ocrEngine.setImage` untuk masing‑masing, dan tambahkan hasilnya ke `OcrResult` yang sama sebelum menyimpan.
- **Bahasa berbeda:** Gunakan `ocrEngine.getLanguage().setLanguage(OcrLanguage.FRENCH);` (atau bahasa lain yang didukung) sebelum memanggil `recognize()`.
- **DPI khusus:** Untuk pemindaian yang buram, Anda dapat meningkatkan akurasi dengan mengatur `ocrEngine.getImage().setResolution(300);`.

## Langkah 5: Verifikasi Output (Apa yang Diharapkan)

Setelah program dijalankan, periksa file `output.pdf`:

1. **Lapisan visual:** PDF menampilkan PNG persis seperti yang Anda berikan.
2. **Lapisan teks:** Tekan `Ctrl+F` (atau Cmd+F) dan cari kata yang Anda tahu ada dalam gambar. Kata tersebut harus langsung ditemukan.
3. **Salin‑tempel:** Coba pilih sebuah paragraf dan salin ke editor teks; Anda akan mendapatkan teks bersih yang dapat dicari.

Jika pencarian gagal, periksa kembali apakah gambar terlalu beresolusi rendah atau bahasa yang tepat sudah disetel. Seringkali, meningkatkan DPI sedikit saja memperbaiki masalah.

## Pertanyaan Umum & Tips Pro

- **Apakah saya memerlukan lisensi?**  
  Aspose OCR berfungsi dalam mode percobaan dengan watermark. Untuk produksi, beli lisensi dan atur dengan `License license = new License(); license.setLicense("Aspose.OCR.lic");`.

- **Bisakah saya **convert image to pdf** tanpa OCR?**  
  Ya—gunakan `OcrOutputFormat.PDF` dengan `ocrEngine.setRecognizeText(false);` sebelum `recognize()`. Ini menghasilkan PDF hanya berisi gambar.

- **Bagaimana jika saya hanya menginginkan teks yang diekstrak?**  
  Lewati pemanggilan `save` dan gunakan `ocrResult.getText()`; Anda dapat menuliskannya ke file `.txt` atau mengirimkannya ke indeks pencarian.

- **Tips performa:**  
  Gunakan kembali instance `OcrEngine` yang sama untuk beberapa gambar; ini mengurangi overhead inisialisasi.

## Contoh Lengkap yang Siap Jalan (Semua Bersatu)

Berikut adalah program Java lengkap yang siap dijalankan. Ganti jalur placeholder dengan direktori Anda sendiri, tambahkan dependensi Maven, dan Anda siap.

```java
import com.aspose.ocr.*;

public class PdfOutputExample {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Initialize OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Load the image (PNG, JPG, TIFF, etc.)
        String inputPath = "YOUR_DIRECTORY/input.png"; // <-- change this
        ocrEngine.setImage(ImageStream.fromFile(inputPath));

        // 3️⃣ Run OCR to get text and layout
        OcrResult ocrResult = ocrEngine.recognize();

        // Optional: display extracted text in console
        System.out.println("Extracted Text:");
        System.out.println(ocrResult.getText());

        // 4️⃣ Save as searchable PDF (image + hidden text layer)
        String outputPath = "YOUR_DIRECTORY/output.pdf"; // <-- change this
        ocrResult.save(outputPath, OcrOutputFormat.PDF);

        System.out.println("Searchable PDF created at: " + outputPath);
    }
}
```

**Output yang diharapkan:**  
```
Extracted Text:
[...the plain text that was recognized from the PNG...]
Searchable PDF created at: YOUR_DIRECTORY/output.pdf
```

Buka `output.pdf` di penampil PDF apa pun dan coba cari kata dari teks yang diekstrak—Anda akan melihatnya disorot, mengonfirmasi bahwa Anda berhasil **create searchable pdf**.

## Kesimpulan

Kami baru saja menunjukkan cara **create searchable pdf** dari PNG menggunakan Java dan Aspose OCR. Langkah‑langkahnya sederhana: siapkan pustaka, muat gambar, jalankan OCR, dan simpan hasilnya sebagai PDF. Sepanjang proses Anda juga belajar cara **convert image to pdf**, **extract text from image**, dan bahkan **recognize text from png** untuk skenario yang lebih maju.

Apa selanjutnya? Coba proses batch faktur yang dipindai dalam loop, simpan teks tersembunyi ke basis data untuk pencarian teks penuh, atau bereksperimen dengan bahasa dan teknik pra‑pemrosesan gambar yang berbeda. Pola yang sama berlaku untuk format lain—ganti saja file input dan Anda akan dapat **image to searchable pdf** dalam sekejap.

Ada pertanyaan atau mengalami kendala? Tinggalkan komentar di bawah, dan selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}