---
category: general
date: 2026-05-03
description: 'cara menjalankan OCR dengan cepat: pelajari cara mengekstrak teks dari
  gambar dan mengenali teks dari formulir menggunakan Aspose OCR Java. Langkah sederhana
  untuk membaca gambar untuk OCR.'
draft: false
keywords:
- how to run ocr
- extract text from image
- recognize text from form
- read image for ocr
language: id
og_description: 'cara menjalankan OCR dengan cepat: pelajari cara mengekstrak teks
  dari gambar dan mengenali teks dari formulir menggunakan Aspose OCR Java. langkah
  sederhana untuk membaca gambar untuk OCR.'
og_title: cara menjalankan OCR pada formulir – mengekstrak teks dari gambar
tags:
- ocr
- java
- image-processing
title: cara menjalankan OCR pada formulir – mengekstrak teks dari gambar
url: /id/python-java/general/how-to-run-ocr-on-a-form-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# cara menjalankan ocr pada formulir – mengekstrak teks dari gambar

Pernah bertanya-tanya **cara menjalankan ocr** pada dokumen yang dipindai tanpa menghabiskan berjam‑jam bermain‑main dengan perpustakaan yang tidak jelas? Anda tidak sendirian. Dalam banyak proyek—baik itu mendigitalkan faktur, mengarsipkan kontrak, atau mengambil data dari formulir tulisan tangan—kemampuan **mengekstrak teks dari gambar** menjadi titik sakit harian.

Begini: Aspose OCR untuk Java membuat seluruh alur kerja hampir tanpa rasa sakit. Dalam tutorial ini kami akan menelusuri setiap baris kode yang Anda perlukan untuk **mengenali teks dari formulir**, menjelaskan mengapa setiap langkah penting, dan menunjukkan cara **membaca gambar untuk ocr** dengan skor kepercayaan. Pada akhir tutorial Anda akan memiliki kelas Java siap‑jalankan yang dapat Anda masukkan ke proyek Maven atau Gradle mana pun.

## Apa yang Akan Anda Pelajari

- Menyiapkan mesin Aspose OCR dan menerapkan lisensi Anda.
- Memuat JPEG, PNG, atau TIFF ke dalam memori.
- Menjalankan OCR dan mengiterasi setiap baris teks yang dikenali.
- Menemukan baris dengan kepercayaan rendah untuk ditinjau secara manual.
- Memperluas contoh ke PDF multi‑halaman atau format gambar lainnya.

Tidak diperlukan pengalaman sebelumnya dengan Aspose, cukup lingkungan pengembangan Java dasar (JDK 11+ dan IDE pilihan Anda). Mari kita mulai.

![how to run ocr example](/images/ocr-demo.png){alt="contoh cara menjalankan ocr pada formulir yang dipindai"}

## Langkah 1: Inisialisasi Mesin OCR – **cara menjalankan ocr**

Hal pertama yang harus Anda lakukan sebelum operasi OCR apa pun adalah membuat instance `OcrEngine` dan melampirkan lisensi yang valid. Tanpa lisensi, perpustakaan berjalan dalam mode demo, yang membatasi jumlah halaman yang dapat diproses.

```java
// Step 1: Initialize the OCR engine and set the license
import com.aspose.ocr.*;

public class OcrDemo {
    public static void main(String[] args) {
        // Create the engine
        OcrEngine engine = new OcrEngine();

        // Load your license – replace the path with your actual .lic file
        License lic = new License();
        lic.setLicense("Aspose.OCR.Java.lic");   // <-- ensure the file is on the classpath

        // From here on the engine is ready to process images
```

**Mengapa ini penting:**  
`OcrEngine` menyimpan semua konfigurasi—bahasa, mode deteksi, dan penyesuaian kinerja. Dengan menetapkan lisensi di awal, Anda menghindari fallback diam‑diam ke mode percobaan yang akan memotong output Anda.

## Langkah 2: Memuat Gambar – **mengekstrak teks dari gambar**

Selanjutnya kita memerlukan objek `Image` yang menunjuk ke file yang ingin Anda pindai. Aspose mendukung berbagai format, sehingga Anda dapat memasukkan halaman PDF yang sudah dipindai dan dikonversi ke PNG, JPEG mentah, atau bahkan TIFF multi‑halaman.

```java
        // Step 2: Load the image to be processed
        // Replace the path with the location of your scanned form
        Image image = Image.fromFile("YOUR_DIRECTORY/scanned_form.jpg");

        // Optional: If you’re dealing with a PDF, you could use
        // Image image = Image.fromPdf("document.pdf", 1); // page 1
```

**Mengapa ini penting:**  
Memuat gambar sebagai objek `Image` memberi mesin akses ke data piksel, informasi DPI, dan kedalaman warna—semua faktor yang memengaruhi akurasi OCR. Jika Anda melewatkan langkah ini dan langsung memberikan array byte mentah, Anda akan kehilangan petunjuk berguna tersebut.

## Langkah 3: Menjalankan OCR – **mengenali teks dari formulir**

Sekarang bagian yang menyenangkan: benar‑benarnya mengenali karakter. Metode `recognize` mengembalikan `RecognitionResult` yang berisi koleksi objek `Line`, masing‑masing dengan skor kepercayaan sendiri.

```java
        // Step 3: Run OCR on the loaded image
        RecognitionResult result = engine.recognize(image);
```

**Mengapa ini penting:**  
Memanggil `recognize` memicu rangkaian proses internal—pra‑pemrosesan (deskew, penghilangan noise), segmentasi, klasifikasi karakter, dan pasca‑pemrosesan (pemeriksaan ejaan, model bahasa). Objek hasil menyederhanakan semua kompleksitas itu.

## Langkah 4: Memproses Hasil – **membaca gambar untuk ocr** output

Setelah Anda memiliki `RecognitionResult`, Anda dapat mengiterasi setiap baris, memutuskan apa yang disimpan secara otomatis, dan menandai apa pun yang tampak tidak pasti. Ambang kepercayaan 85 % adalah titik awal yang baik untuk kebanyakan formulir cetak.

```java
        // Step 4: Examine each recognized line
        for (Line line : result.getLines()) {
            // Highlight lines with low confidence for manual review
            if (line.getConfidence() < 85) {
                System.out.println(
                    String.format("Low‑confidence line (%.2f%%): %s", line.getConfidence(), line.getText()));
            } else {
                // High‑confidence lines can be used directly
                System.out.println(line.getText());
            }
        }
    }
}
```

**Output yang diharapkan (contoh):**

```
Invoice Number: 2023‑00123
Date: 2023‑04‑15
Customer: Acme Corp.
Low‑confidence line (72.34%): Total Amount: $1,23O.00
```

Pada contoh di atas mesin tidak yakin tentang digit terakhir dari total jumlah, sehingga kami mencetak peringatan. Anda dapat mengalirkan baris‑baris tersebut ke UI untuk koreksi manual atau mencatatnya untuk ditinjau nanti.

### Kasus Tepi & Tips

- **Beberapa halaman:** Jika Anda memiliki PDF multi‑halaman, lakukan loop pada setiap indeks halaman dan panggil `Image.fromPdf(pdfPath, pageIndex)`.
- **Berbagai bahasa:** Tetapkan `engine.getLanguage().setLanguage(Language.Spanish);` sebelum memanggil `recognize`.
- **Kualitas gambar:** Pemindaian beresolusi rendah (< 150 DPI) sering menghasilkan kepercayaan di bawah 80 %. Upscaling dengan `image.resize(300, 300)` dapat membantu, tetapi perbaikan terbaik adalah pemindaian yang lebih baik.
- **Kinerja:** Menggunakan kembali instance `OcrEngine` yang sama untuk banyak gambar mengurangi overhead dibandingkan membuat yang baru setiap kali.

## Pertanyaan yang Sering Diajukan

**Apakah saya dapat menjalankannya di server tanpa tampilan (headless)?**  
Tentu saja. Perpustakaan tidak memiliki ketergantungan GUI, sehingga berjalan baik di dalam kontainer Docker atau pipeline CI.

**Bagaimana jika saya belum memiliki lisensi?**  
Anda masih dapat memanggil `engine.recognize`, tetapi mode demo akan berhenti setelah 2 halaman pertama dan menambahkan watermark pada output. Ini cocok untuk percobaan cepat.

**Apakah ada cara mengekstrak data terstruktur (misalnya tabel)?**  
Aspose OCR menyediakan kelas `TableRecognizer`, tetapi itu berada di luar cakupan panduan pemula ini. Setelah Anda menguasai dasar‑dasarnya, lihat dokumentasi resmi untuk `TableRecognizer`.

## Menyimpulkan Semua – **cara menjalankan ocr** secara singkat

Kami telah membahas semua yang Anda perlukan untuk **cara menjalankan ocr** pada formulir yang dipindai: inisialisasi mesin, memuat gambar, mengeksekusi pengenalan, dan menangani hasil secara cerdas. Dengan hanya beberapa baris Java, Anda dapat **mengekstrak teks dari gambar**, **mengenali teks dari formulir**, dan **membaca gambar untuk ocr** dengan skor kepercayaan yang memungkinkan Anda memutuskan kapan tinjauan manusia diperlukan.

Langkah selanjutnya? Coba ganti JPEG dengan TIFF multi‑halaman, bereksperimen dengan ambang kepercayaan yang berbeda, atau integrasikan output ke basis data untuk entri data otomatis. Kemungkinannya seluas dokumen yang harus Anda proses.

Ada pertanyaan lebih lanjut tentang OCR, pra‑pemrosesan gambar, atau lisensi? Tinggalkan komentar di bawah, dan selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}