---
category: general
date: 2026-01-07
description: Buat PDF yang dapat dicari dari gambar menggunakan Aspose OCR di Java.
  Pelajari cara mengonversi gambar ke PDF, mengenali teks dari gambar, dan menghasilkan
  PDF dari JPG.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- recognize text from image
- how to use ocr
- generate pdf from jpg
language: id
og_description: Buat PDF yang dapat dicari dari gambar dengan Aspose OCR di Java.
  Panduan langkah demi langkah untuk mengonversi gambar ke PDF, mengenali teks dari
  gambar, dan menghasilkan PDF dari JPG.
og_title: Buat PDF yang Dapat Dicari dari Gambar – Panduan OCR Java
tags:
- OCR
- Java
- PDF
- Aspose
title: Buat PDF yang Dapat Dicari dari Gambar dengan OCR – Tutorial Java
url: /id/java/ocr-operations/create-searchable-pdf-from-image-with-ocr-java-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Membuat PDF yang Dapat Dicari dari Gambar dengan OCR – Tutorial Java

Pernah perlu **create searchable PDF** dari gambar yang dipindai tetapi tidak yakin harus mulai dari mana? Anda tidak sendirian—banyak pengembang mengalami kebuntuan saat pertama kali mencoba mengubah JPEG menjadi PDF yang sebenarnya dapat Anda cari.  

Dalam panduan ini kami akan membahas contoh lengkap yang dapat dijalankan yang menunjukkan cara **convert image to PDF**, **recognize text from image**, dan akhirnya **generate PDF from JPG** menggunakan Aspose OCR untuk Java. Tidak ada referensi samar, hanya kode yang dapat Anda salin‑tempel dan jalankan hari ini.

## Apa yang Anda Butuhkan

* **Java 17** atau yang lebih baru (API bekerja dengan JDK terbaru apa pun).  
* **Aspose.OCR for Java** library – Anda dapat mengambil JAR terbaru dari Maven Central atau situs Aspose.  
* Sebuah gambar contoh, misalnya `sample.jpg`, ditempatkan dalam folder yang dapat Anda referensikan.  
* IDE atau editor teks sederhana plus terminal—apa pun yang Anda nyaman gunakan.

Itu saja. Tidak ada kerangka kerja berat, tidak ada dependensi native tambahan. Mari kita mulai.

## Langkah 1 – Buat PDF yang Dapat Dicari: Inisialisasi Mesin OCR

Hal pertama yang kita lakukan adalah membuat instance `OcrEngine` dan menunjukkannya ke gambar sumber. Objek ini adalah inti dari Aspose OCR; ia menangani segala hal mulai dari memuat bitmap hingga menampilkan teks yang dikenali.

```java
import com.aspose.ocr.*;

public class HelloOcrTutorial {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the image you want to turn into a searchable PDF
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.jpg"));
```

> **Mengapa ini penting:** Menginisialisasi mesin dengan benar memastikan perpustakaan dapat membaca format gambar yang Anda berikan. Jika jalurnya salah, Anda akan mendapatkan `FileNotFoundException` dan seluruh alur berhenti.

## Langkah 2 – Tingkatkan Performa: Aktifkan GPU, CPU Multi‑core, dan Koreksi Ejaan

OCR dapat mengonsumsi banyak CPU, terutama pada dokumen besar. Aspose menyediakan beberapa pengaturan yang dapat Anda ubah untuk membuat proses lebih cepat dan lebih akurat.

```java
        // 2️⃣ Turn on performance helpers – GPU, multi‑core CPU, and spell correction
        ocrEngine.getEngineOptions()
                 .setUseGpu(true)                 // uses GPU if one is available
                 .setUseMultiCore(true)           // spreads work across CPU cores
                 .setEnableSpellCorrection(true); // cleans up common OCR mistakes
```

> **Tips pro:** Jika Anda menjalankan di server tanpa GPU, `setUseGpu(false)` tidak akan merugikan—Anda hanya akan kembali ke pemrosesan CPU multi‑core.

## Langkah 3 – Tingkatkan Kualitas Gambar: Deskew dan Despeckle (Opsional tetapi Disarankan)

Pemindaian jarang sempurna. Sedikit kemiringan atau noise bintik dapat mengacaukan pengenalan. Kelas `ImageProcessingOptions` memungkinkan Anda membersihkan gambar sebelum mesin mencoba membacanya.

```java
        // 3️⃣ Pre‑process the image – straighten it and remove noise
        ocrEngine.getImageProcessingOptions()
                 .setDeskew(true)   // automatically rotates tilted text
                 .setDespeckle(true); // reduces background speckles
```

> **Kasus khusus:** Jika gambar sumber Anda sudah bersih, Anda dapat melewati langkah ini. Tidak akan merugikan, tetapi menambah beberapa milidetik overhead.

## Langkah 4 – Kenali Teks dari Gambar dan Hasilkan PDF

Sekarang keajaiban terjadi. Kami memanggil `recognize()` dan mesin mengembalikan `OcrResult`. Dari situ kami dapat menyimpan output dalam berbagai format—PDF menjadi yang paling umum untuk dokumen yang dapat dicari.

```java
        // 4️⃣ Perform OCR and get the result object
        OcrResult ocrResult = ocrEngine.recognize();

        // 5️⃣ Save the result as a searchable PDF (you could also choose TXT, DOCX, etc.)
        ocrResult.save("YOUR_DIRECTORY/sample-output.pdf", OcrOutputFormat.PDF);
    }
}
```

> **Apa yang akan Anda lihat:** `sample-output.pdf` berisi gambar asli sebagai lapisan latar belakang, sementara teks yang dikenali berada di atas sebagai lapisan tak terlihat. Buka di Adobe Reader dan coba pilih teks—Anda akan terkejut.

## Langkah 5 – Verifikasi Output PDF yang Dapat Dicari

Setelah file ditulis, sebaiknya periksa kembali bahwa PDF benar‑benar dapat dicari.

```java
import java.awt.Desktop;
import java.io.File;

public class VerifyPdf {
    public static void main(String[] args) throws Exception {
        File pdf = new File("YOUR_DIRECTORY/sample-output.pdf");
        if (pdf.exists() && Desktop.isDesktopSupported()) {
            Desktop.getDesktop().open(pdf); // opens the PDF in the default viewer
        } else {
            System.out.println("PDF not found or cannot be opened on this platform.");
        }
    }
}
```

Buka PDF, tekan **Ctrl F**, ketik kata yang Anda tahu muncul di gambar—jika pencarian menemukannya, Anda telah berhasil **create searchable pdf**!

## Cara Menggunakan OCR dalam Skenario Dunia Nyata (Bonus)

* **Batch processing:** Bungkus kode dalam loop yang mengiterasi folder berisi JPG. Ingat untuk menggunakan kembali satu instance `OcrEngine` agar penggunaan memori tetap rendah.  
* **Language support:** Aspose OCR mendukung lebih dari 60 bahasa. Cukup panggil `ocrEngine.getEngineOptions().setLanguage(Language.English);` (atau nilai enum lainnya).  
* **Error handling:** Tangkap `OcrException` untuk menangani file yang rusak secara elegan.  

Penyesuaian ini membuat solusi cukup kuat untuk alur produksi.

## Contoh Java Lengkap – Membuat PDF yang Dapat Dicari dari JPG

Berikut adalah program lengkap yang berdiri sendiri yang dapat Anda kompilasi dan jalankan apa adanya. Ganti `YOUR_DIRECTORY` dengan jalur sebenarnya di mesin Anda.

```java
import com.aspose.ocr.*;

public class CreateSearchablePdf {
    public static void main(String[] args) throws Exception {
        // -------------------------------------------------
        // 1️⃣ Load the source image
        // -------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.jpg"));

        // -------------------------------------------------
        // 2️⃣ Performance helpers
        // -------------------------------------------------
        ocrEngine.getEngineOptions()
                 .setUseGpu(true)
                 .setUseMultiCore(true)
                 .setEnableSpellCorrection(true);

        // -------------------------------------------------
        // 3️⃣ Image pre‑processing (optional but helpful)
        // -------------------------------------------------
        ocrEngine.getImageProcessingOptions()
                 .setDeskew(true)
                 .setDespeckle(true);

        // -------------------------------------------------
        // 4️⃣ Run OCR and save as searchable PDF
        // -------------------------------------------------
        OcrResult result = ocrEngine.recognize();
        result.save("YOUR_DIRECTORY/sample-output.pdf", OcrOutputFormat.PDF);

        System.out.println("✅ Searchable PDF created at YOUR_DIRECTORY/sample-output.pdf");
    }
}
```

**Output yang diharapkan:**  

```
✅ Searchable PDF created at YOUR_DIRECTORY/sample-output.pdf
```

Buka PDF yang dihasilkan dan Anda seharusnya dapat mencari kata apa pun yang muncul di `sample.jpg`. Jika Anda tidak melihat lapisan teks, periksa kembali jalur gambar dan pastikan mesin OCR tidak melemparkan pengecualian tersembunyi.

## Kesimpulan

Kami baru saja menunjukkan cara **create searchable PDF** dari JPEG menggunakan Aspose OCR untuk Java. Dari memuat gambar, menyesuaikan pengaturan performa, membersihkan gambar, hingga akhirnya mengenali teks dan menyimpan PDF yang dapat dicari—setiap langkah dijelaskan dengan *mengapa* dan *bagaimana*.  

Sekarang Anda dapat **convert image to PDF**, **recognize text from image**, dan **generate PDF from JPG** dalam aplikasi Anda sendiri. Selanjutnya, coba proses seluruh folder pemindaian, bereksperimen dengan bahasa yang berbeda, atau tambahkan perlindungan kata sandi pada PDF output. Tidak ada batasnya.

Ada pertanyaan tentang kasus khusus, lisensi, atau penyetelan performa? Tinggalkan komentar di bawah, dan selamat coding! 

![Diagram yang menggambarkan alur OCR – create searchable pdf](/images/ocr-pipeline.png "Diagram PDF yang dapat dicari")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}