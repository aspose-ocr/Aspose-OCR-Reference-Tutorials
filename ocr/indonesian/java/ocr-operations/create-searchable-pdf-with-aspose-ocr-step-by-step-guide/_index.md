---
category: general
date: 2026-01-02
description: Buat PDF yang dapat dicari dari PDF gambar yang dipindai menggunakan
  Aspose OCR. Pelajari cara mengatur bahasa OCR, menyematkan lapisan teks PDF, dan
  menerapkan opsi kompresi tinggi pada PDF.
draft: false
keywords:
- create searchable pdf
- convert scanned image pdf
- high compression pdf
- embed text layer pdf
- set OCR language
language: id
og_description: Buat PDF yang dapat dicari dengan cepat. Panduan ini menunjukkan cara
  mengonversi PDF gambar hasil pemindaian, menyematkan lapisan teks, mengatur bahasa
  OCR, dan mengaktifkan kompresi PDF tinggi.
og_title: Buat PDF yang Dapat Dicari dengan Aspose OCR – Panduan Lengkap
tags:
- Aspose OCR
- Java PDF
- Document Automation
title: Buat PDF yang Dapat Dicari dengan Aspose OCR – Panduan Langkah demi Langkah
url: /id/java/ocr-operations/create-searchable-pdf-with-aspose-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Membuat PDF yang Dapat Dicari – Tutorial Pemrograman Lengkap

Pernah perlu **membuat PDF yang dapat dicari** dari gambar hasil pemindaian tetapi tidak tahu harus mulai dari mana? Anda tidak sendirian. Dalam banyak alur kerja yang berisi dokumen, PDF yang hanya berisi gambar saja adalah jalan buntu untuk pencarian dan pengindeksan.  

Kabar baiknya, dengan Aspose OCR Anda dapat **mengonversi PDF gambar hasil pemindaian** menjadi dokumen yang sepenuhnya dapat dicari hanya dengan beberapa baris kode Java. Tutorial ini memandu Anda melalui setiap langkah—menginisialisasi mesin OCR, mengonfigurasi pengaturan PDF dengan kompresi tinggi, menyematkan lapisan teks tersembunyi, dan bahkan memilih bahasa OCR yang tepat.

Pada akhir panduan ini Anda akan memiliki program yang dapat dijalankan dan menghasilkan PDF yang dapat dicari, sebuah file yang dapat Anda masukkan ke mesin pencari atau sistem manajemen dokumen mana pun tanpa masalah.

---

## Membuat PDF yang Dapat Dicari – Ikhtisar

Sebelum kita masuk ke kode, mari klarifikasi apa arti “membuat PDF yang dapat dicari”. PDF yang dapat dicari memiliki dua lapisan paralel:

1. **Lapisan visual** – gambar hasil pemindaian asli (atau halaman yang dirender).  
2. **Lapisan teks** – karakter tak terlihat namun dapat dibaca mesin yang diekstrak oleh OCR.

Saat Anda membuka PDF semacam itu di Adobe Reader dan memilih teks, yang Anda interaksikan sebenarnya adalah lapisan teks tersembunyi, bukan gambar. Pendekatan dua lapisan inilah yang memungkinkan fungsi **embed text layer PDF**.

---

## Mengonversi PDF Gambar Hasil Pemindaian Menggunakan Aspose OCR

Hal pertama yang Anda butuhkan adalah gambar hasil pemindaian (PNG, JPEG, TIFF) yang ingin Anda ubah menjadi PDF. Aspose OCR dapat membaca gambar tersebut, menjalankan OCR, dan menyerahkan hasilnya ke penulis PDF.

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.PdfSaveOptions;
import com.aspose.ocr.RecognitionLanguage;

public class PdfSearchableExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Initialize the OCR engine
        AsposeOCR ocrEngine = new AsposeOCR();

        // Step 2: Configure PDF save options to embed a searchable text layer
        PdfSaveOptions pdfSaveOptions = new PdfSaveOptions();
        pdfSaveOptions.setCreateSearchablePdf(true);   // enable searchable PDF
        pdfSaveOptions.setCompressionLevel(9);        // optional: high compression

        // Step 3: Perform OCR on the scanned image and save the result as a searchable PDF
        ocrEngine.recognizeImageAndSave(
                "YOUR_DIRECTORY/input.png",                 // path to scanned image
                RecognitionLanguage.ENGLISH,                // set OCR language
                "YOUR_DIRECTORY/output.pdf",                // output PDF file
                pdfSaveOptions);                            // options defined above

        // Step 4: Indicate that the PDF has been created
        System.out.println("Searchable PDF created.");
    }
}
```

**Mengapa ini berhasil:**  
- `setCreateSearchablePdf(true)` memberi tahu Aspose untuk menghasilkan lapisan teks tersembunyi, memenuhi persyaratan **embed text layer pdf**.  
- `setCompressionLevel(9)` menempatkan file ke dalam rentang **high compression pdf**, memperkecil ukuran akhir tanpa mengorbankan akurasi OCR.  
- Argumen `RecognitionLanguage.ENGLISH` menunjukkan cara **set OCR language**; Anda dapat menggantinya dengan bahasa Prancis, Jerman, dll., tergantung pada materi sumber Anda.

---

## Pengaturan PDF dengan Kompresi Tinggi

PDF hasil pemindaian berukuran besar dapat dengan cepat membengkak menjadi ratusan megabyte. Aspose menawarkan API kompresi sederhana yang bekerja pada tingkat PDF. Metode `setCompressionLevel` menerima nilai dari 0 (tanpa kompresi) hingga 9 (kompresi maksimum).  

```java
PdfSaveOptions pdfSaveOptions = new PdfSaveOptions();
pdfSaveOptions.setCompressionLevel(9); // 9 = strongest compression
```

Beberapa tips:

- **Gunakan format gambar lossless** (PNG) untuk pemindaian yang banyak mengandung teks; JPEG lebih cocok untuk foto.  
- **Aktifkan font subsetting** jika Anda menyematkan font khusus—Aspose melakukannya secara otomatis saat Anda membuat PDF yang dapat dicari.  
- **Uji ukuran output** setelah setiap perubahan; kadang‑kadang kompresi level‑8 memberi Anda pengurangan ukuran 10 % dengan kehilangan kualitas yang dapat diabaikan dibandingkan level 9.

---

## Menyematkan Lapisan Teks PDF untuk Kemampuan Pencarian

Jika Anda melewatkan pemanggilan `setCreateSearchablePdf(true)`, file yang dihasilkan akan terlihat baik tetapi Anda tidak akan dapat mencari isinya. Lapisan teks tersembunyi dibuat dengan memetakan setiap karakter yang dikenali ke lokasinya pada halaman.  

```java
pdfSaveOptions.setCreateSearchablePdf(true);
```

**Hal yang perlu diwaspadai:**  

- **Dokumen multibahasa** – Anda mungkin perlu menjalankan OCR dua kali, sekali per bahasa, lalu menggabungkan lapisan teks.  
- **Tata letak kompleks** (tabel, multi‑kolom) – Aspose melakukan pekerjaan yang cukup baik, tetapi periksa kembali output dengan penampil PDF yang menampilkan teks tersembunyi (misalnya mode “Edit PDF” di Adobe Acrobat).

---

## Menetapkan Bahasa OCR untuk Pengakuan yang Akurat

Akurasi mesin OCR bergantung pada bahasa yang Anda beri tahu untuk diharapkan. Aspose menyertakan sekumpulan bahasa bawaan, dan Anda juga dapat menambahkan paket bahasa khusus.

```java
ocrEngine.recognizeImageAndSave(
        "input.png",
        RecognitionLanguage.ENGLISH, // change to RecognitionLanguage.FRENCH, etc.
        "output.pdf",
        pdfSaveOptions);
```

**Kapan mengganti bahasa:**  

- Dokumen mengandung **skrip non‑Latin** (Cyrillic, Arab) – beralih ke `RecognitionLanguage` yang sesuai.  
- Halaman dengan bahasa campuran – Anda dapat memanggil `recognizeImageAndSave` dua kali, masing‑masing dengan bahasa yang berbeda, lalu menggabungkan PDF‑nya.

---

## Menjalankan Contoh Lengkap

Berikut adalah program lengkap yang siap dijalankan. Ganti jalur placeholder dengan lokasi file yang sebenarnya, pastikan JAR Aspose OCR berada di classpath Anda, dan eksekusi.

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.PdfSaveOptions;
import com.aspose.ocr.RecognitionLanguage;

public class PdfSearchableExample {
    public static void main(String[] args) throws Exception {

        // Initialize OCR engine
        AsposeOCR ocrEngine = new AsposeOCR();

        // Configure PDF save options
        PdfSaveOptions pdfSaveOptions = new PdfSaveOptions();
        pdfSaveOptions.setCreateSearchablePdf(true);   // embed text layer PDF
        pdfSaveOptions.setCompressionLevel(9);        // high compression PDF

        // Perform OCR and save searchable PDF
        ocrEngine.recognizeImageAndSave(
                "C:/scans/input.png",                 // path to scanned image
                RecognitionLanguage.ENGLISH,          // set OCR language
                "C:/output/searchable.pdf",           // output PDF
                pdfSaveOptions);                      // options defined above

        System.out.println("Searchable PDF created.");
    }
}
```

**Output yang diharapkan:** Saat Anda menjalankan program, konsol akan mencetak:

```
Searchable PDF created.
```

Buka `searchable.pdf` di penampil PDF apa pun, coba pilih teks, dan Anda akan melihat lapisan tak terlihat beraksi. Anda telah berhasil **create searchable pdf** dari gambar hasil pemindaian.

---

![contoh membuat searchable pdf](image-placeholder.png "contoh membuat searchable pdf")

*Screenshot di atas (placeholder) biasanya akan menampilkan penampil PDF dengan teks yang dapat dipilih di atas halaman yang dipindai.*

---

## Kesimpulan

Kami telah membahas semua yang Anda perlukan untuk **create searchable PDF** menggunakan Aspose OCR:

- Inisialisasi mesin OCR.  
- **Convert scanned image PDF** dengan memberi PNG/JPEG ke `recognizeImageAndSave`.  
- Gunakan `setCreateSearchablePdf(true)` untuk **embed text layer PDF**.  
- Terapkan `setCompressionLevel(9)` untuk **high compression PDF** yang tetap ringan.  
- Pilih `RecognitionLanguage` yang tepat untuk **set OCR language** demi akurasi maksimal.

Dari sini Anda dapat bereksperimen dengan pemrosesan batch, bahasa yang berbeda, atau bahkan menggabungkan beberapa halaman hasil pemindaian menjadi satu PDF yang dapat dicari. Pola yang sama berlaku untuk bahasa lain seperti Spanyol atau Jepang—cukup ganti enum `RecognitionLanguage`.

Silakan tinggalkan komentar jika Anda mengalami kendala, dan selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}