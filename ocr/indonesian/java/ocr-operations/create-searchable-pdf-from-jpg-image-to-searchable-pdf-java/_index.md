---
category: general
date: 2026-02-19
description: Buat PDF yang dapat dicari dari gambar JPG dengan Aspose OCR di Java.
  Konversi JPG ke PDF dan kenali teks dari gambar dengan cepat.
draft: false
keywords:
- create searchable pdf
- image to searchable pdf
- recognize text from image
- extract text from jpg
- convert jpg to pdf
language: id
og_description: Buat PDF yang dapat dicari dari gambar JPG dengan Aspose OCR. Pelajari
  cara mengonversi JPG ke PDF dan mengenali teks dari gambar dalam Java.
og_title: Buat PDF yang Dapat Dicari dari JPG – Tutorial OCR Java
tags:
- aspose-ocr
- java
- pdf
- ocr
title: Buat PDF yang Dapat Dicari dari JPG – Panduan Java Mengubah Gambar menjadi
  PDF yang Dapat Dicari
url: /id/java/ocr-operations/create-searchable-pdf-from-jpg-image-to-searchable-pdf-java/
---

part of content. So final output is the translated content only.

Let's assemble.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat PDF yang Dapat Dicari dari JPG – Panduan Java Mengubah Gambar menjadi PDF yang Dapat Dicari

Pernahkah Anda perlu **membuat PDF yang dapat dicari** dari gambar yang dipindai tetapi tidak yakin harus mulai dari mana? Anda bukan satu-satunya—banyak pengembang mengalami hal yang sama ketika mereka memiliki JPG yang perlu dapat dicari. Kabar baiknya, dengan Aspose OCR untuk Java Anda dapat mengubah gambar tersebut menjadi PDF yang sepenuhnya dapat dicari hanya dengan beberapa baris kode.

Dalam tutorial ini kami akan membahas seluruh proses: memuat JPG, mengenali teks, dan menyimpan hasilnya sebagai PDF yang dapat dicari. Pada akhir tutorial Anda akan tahu cara **convert jpg to pdf**, cara **extract text from jpg**, dan mengapa pendekatan ini sering lebih andal dibandingkan mencoba OCR pada PDF setelah dibuat.

## Apa yang Anda Butuhkan

* **Java Development Kit (JDK) 8 atau lebih baru** – kode menggunakan API Java standar.
* **Aspose OCR for Java** library – Anda dapat mengunduhnya dari Maven Central atau mengunduh JAR dari situs Aspose.
* Sebuah **sample JPG** yang berisi teks yang dapat dibaca (misalnya, faktur yang dipindai atau tangkapan layar dokumen).

Tidak diperlukan kerangka kerja tambahan; contoh ini bekerja dengan proyek Java biasa.

## Langkah 1 – Siapkan Proyek dan Tambahkan Aspose OCR

Pertama, buat proyek Maven baru (atau cukup folder dengan JAR di classpath). Jika Anda menggunakan Maven, tambahkan dependensi ini ke `pom.xml` Anda:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- check for the latest version -->
</dependency>
```

> **Pro tip:** Selalu periksa versi terbaru di repositori Maven Aspose; rilis yang lebih baru mencakup perbaikan kinerja dan perbaikan bug.

Setelah dependensi terpasang, Anda siap menulis kode Java yang akan **create searchable PDF**.

## Langkah 2 – Muat Gambar (image to searchable pdf)

Langkah nyata pertama adalah mengarahkan mesin OCR ke gambar sumber. Di sinilah transformasi **image to searchable pdf** benar‑benar dimulai.

```java
import com.aspose.ocr.*;

public class SearchablePdfExample {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Load the JPG you want to turn into a searchable PDF
        // Replace "YOUR_DIRECTORY/input.jpg" with the actual path to your file
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/input.jpg"));
```

> **Why this matters:** `setImage` memberi tahu Aspose bitmap mana yang akan dianalisis. Jika Anda memberikan gambar beresolusi rendah, kualitas OCR akan menurun, jadi pastikan JPG setidaknya 300 dpi untuk hasil terbaik.

## Langkah 3 – Kenali Teks dari Gambar

Sekarang mesin tahu gambar mana yang akan diproses, kita dapat memintanya untuk **recognize text from image**. Aspose OCR melakukan pekerjaan berat di balik layar, menangani deteksi bahasa, segmentasi karakter, dan penilaian kepercayaan.

```java
        // Perform OCR and directly output a searchable PDF
        ocrEngine.recognize()
                 .save("YOUR_DIRECTORY/output-searchable.pdf", OcrOutputFormat.SEARCHABLE_PDF);
```

Pemanggilan `recognize()` mengembalikan antarmuka fluent, memungkinkan kami men-chain metode `save`. Dengan menentukan `OcrOutputFormat.SEARCHABLE_PDF`, perpustakaan menyisipkan lapisan teks tak terlihat di dalam PDF sambil mempertahankan tampilan gambar asli.

> **Edge case:** Jika JPG Anda berisi beberapa halaman (misalnya, TIFF multi‑halaman yang disimpan sebagai JPG terpisah), Anda perlu melakukan loop pada setiap file dan menggabungkan PDF yang dihasilkan nanti. Mesin OCR yang sama dapat digunakan kembali untuk setiap iterasi.

## Langkah 4 – Verifikasi Hasil

Setelah operasi penyimpanan selesai, pesan konsol sederhana memberi tahu Anda bahwa semuanya berjalan lancar.

```java
        // Let the user know the PDF is ready
        System.out.println("Searchable PDF created.");
    }
}
```

Saat Anda membuka `output-searchable.pdf` di penampil seperti Adobe Acrobat, Anda seharusnya dapat memilih teks tersembunyi, menyalinnya, atau melakukan pencarian—tepat seperti yang Anda harapkan dari **searchable PDF**.

### Output yang Diharapkan

Menjalankan program mencetak:

```
Searchable PDF created.
```

Dan PDF yang dihasilkan akan menampilkan JPG asli sambil memungkinkan pemilihan teks. Jika Anda membuka “Properties → Description → PDF Producer” pada PDF, Anda akan melihat sesuatu seperti `Aspose.OCR for Java`.

## Contoh Lengkap yang Berfungsi

Berikut adalah file sumber lengkap yang siap dijalankan. Salin‑tempel ke IDE Anda, sesuaikan jalur file, dan jalankan.

```java
import com.aspose.ocr.*;

public class SearchablePdfExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the source image containing the text to be recognized
        // Make sure the path points to a real JPG on your disk
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/input.jpg"));

        // Step 3: Recognize the text and directly save it as a searchable PDF
        ocrEngine.recognize()
                 .save("YOUR_DIRECTORY/output-searchable.pdf", OcrOutputFormat.SEARCHABLE_PDF);

        // Step 4: Notify that the PDF has been created
        System.out.println("Searchable PDF created.");
    }
}
```

> **What if the OCR fails?**  
> * Biasanya ini terjadi karena gambar terlalu berisik atau bahasa tidak didukung secara default. Anda dapat meningkatkan akurasi dengan pra‑pemrosesan gambar (meningkatkan kontras, meluruskan) atau dengan secara eksplisit mengatur bahasa menggunakan `ocrEngine.getLanguage().setLanguage(OcrLanguage.English);`.

## Pertanyaan Umum & Hal-hal yang Perlu Diwaspadai

| Question | Answer |
|----------|--------|
| **Bisakah saya mengekstrak teks biasa alih-alih PDF?** | Yes. Use `ocrEngine.recognize().save("output.txt", OcrOutputFormat.TEXT);` |
| **Bagaimana jika saya perlu memproses PNG?** | The same API works; just change the file extension in `fromFile`. |
| **Apakah PDF yang dihasilkan benar‑benar dapat dicari di semua penampil?** | Modern viewers (Adobe Reader, Foxit, Chrome) honor the hidden text layer. Older tools might ignore it. |
| **Bagaimana cara mengontrol ukuran halaman PDF?** | Aspose OCR uses the image dimensions by default. For custom sizing, generate a PDF manually and overlay the OCR text layer—this is an advanced scenario. |

## Tips Kinerja

* **Batch processing:** Gunakan kembali satu instance `OcrEngine` untuk banyak gambar agar menghindari pemuatan perpustakaan native berulang.
* **Thread safety:** Mesin **tidak** thread‑safe; buat satu per thread jika Anda memparallelkan.
* **Memory usage:** Gambar besar dapat mengonsumsi banyak RAM. Jika Anda mengalami `OutOfMemoryError`, perkecil skala gambar sebelum memberikannya ke mesin.

## Langkah Selanjutnya

Sekarang Anda tahu cara **create searchable PDF**, Anda mungkin ingin menjelajahi tugas terkait:

* **Convert jpg to pdf** tanpa OCR (gunakan perpustakaan Aspose PDF untuk PDF gambar biasa).  
* **Extract text from jpg** ke file `.txt` untuk pengindeksan.  
* **Combine multiple searchable PDFs** menjadi satu dokumen menggunakan `PdfFileEditor` dari Aspose PDF.  

Semua ini dibangun di atas fondasi yang baru saja Anda siapkan.

---

### Ringkasan Cepat

* Kami **membuat PDF yang dapat dicari** dari JPG menggunakan Aspose OCR untuk Java.  
* Proses mencakup memuat gambar, mengenali teks, dan menyimpan sebagai PDF yang dapat dicari.  
* Anda kini memiliki pola yang dapat digunakan kembali untuk **image to searchable PDF**, **recognize text from image**, **extract text from jpg**, dan **convert jpg to pdf**.

Cobalah dengan dokumen Anda sendiri, sesuaikan pengaturan bahasa jika diperlukan, dan biarkan OCR melakukan pekerjaan berat untuk Anda. Selamat coding!  

![Create searchable PDF example](placeholder.png){alt="Contoh PDF yang dapat dicari"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}