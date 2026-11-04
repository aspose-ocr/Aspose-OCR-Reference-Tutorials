---
category: general
date: 2026-04-26
description: Buat PDF yang dapat dicari dari gambar menggunakan Aspose OCR di Java.
  Pelajari cara mengonversi gambar ke PDF, melakukan OCR gambar ke PDF, dan mengekstrak
  teks dari gambar dengan cepat.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- ocr image to pdf
- extract text from image
- how to set language
language: id
og_description: Buat PDF yang dapat dicari dari gambar menggunakan Aspose OCR. Panduan
  ini menunjukkan cara mengonversi gambar ke PDF, OCR gambar ke PDF, dan mengekstrak
  teks dari gambar.
og_title: Buat PDF yang dapat dicari dari gambar dengan Java OCR
tags:
- Java
- OCR
- PDF
title: Buat PDF yang dapat dicari dari gambar dengan Java OCR
url: /id/java/ocr-operations/create-searchable-pdf-from-image-with-java-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat PDF yang dapat dicari dari gambar dengan Java OCR

Pernah membutuhkan untuk **create searchable PDF** dari faktur yang dipindai tetapi tidak yakin harus mulai dari mana? Anda tidak sendirian—banyak pengembang mengalami hambatan ini ketika mereka menginginkan PDF yang sebenarnya dapat Anda cari. Kabar baik? Dengan Aspose OCR for Java Anda dapat **convert image to PDF**, menjalankan OCR secara langsung, dan menghasilkan file yang dapat dicari dengan rapi hanya dalam beberapa baris kode.

Dalam tutorial ini kami akan menelusuri seluruh proses: memuat gambar, memberi tahu mesin bahasa apa yang diharapkan, melakukan OCR, dan akhirnya menyimpan **searchable PDF**. Pada akhir Anda juga akan tahu cara **extract text from image** secara manual, menyesuaikan pengaturan bahasa, dan menangani beberapa kasus tepi umum. Tanpa layanan eksternal, tanpa alat baris perintah yang obscure—hanya Java murni.

## Apa yang Anda butuhkan

- Java 17 atau lebih baru (API juga bekerja dengan rilis lama, tetapi 17 adalah pilihan yang tepat).  
- Perpustakaan Aspose OCR for Java – Anda dapat mengambil JAR terbaru dari Maven Central (`com.aspose:aspose-ocr:23.10`).  
- File gambar yang berisi teks yang dapat dibaca (PNG, JPG, atau TIFF dapat digunakan).  
- Sedikit kesabaran IDE—IntelliJ IDEA atau VS Code sudah cukup.

Jika Anda sudah memiliki semua ini, bagus! Jika belum, cuplikan Maven di bawah ini akan menyiapkan semuanya:

```xml
<!-- Add to your pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version>
</dependency>
```

Sekarang setelah fondasi sudah siap, mari kita selami kode.

## Langkah 1: Inisialisasi mesin OCR – inti dari **create searchable pdf**

Sebelum konversi apa pun terjadi, Anda harus membuat instance `OcrEngine`. Anggaplah ini sebagai otak yang akan membaca piksel dan mengubahnya menjadi karakter.

```java
import com.aspose.ocr.*;

public class PdfExportDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
```

*Mengapa ini penting:* Mesin menyimpan semua pengaturan pengenalan (bahasa, mode akurasi, dll.). Menginstansiasinya sekali dan menggunakannya kembali pada banyak gambar lebih efisien daripada membuat mesin baru untuk setiap file.

## Langkah 2: **How to set language** – tingkatkan akurasi untuk bahasa Prancis, Jerman, atau skrip apa pun

Jika Anda mengetahui bahasa dokumen sumber, beri tahu mesin OCR. Ini mempercepat pemrosesan dan mengurangi kesalahan pengenalan.

```java
        // Step 2: (Optional) Specify the language to improve text extraction
        ocrEngine.getRecognitionSettings().setLanguage(OcrLanguage.FRENCH);
```

Anda dapat mengganti `OcrLanguage.FRENCH` dengan `ENGLISH`, `SPANISH`, `GERMAN`, dll. Jika Anda tidak yakin, biarkan baris tersebut kosong dan biarkan Aspose menebak—tetapi harapkan sedikit penurunan akurasi.

## Langkah 3: Muat gambar yang ingin Anda **convert image to pdf**

Metode `setImage` menerima jalur file, `InputStream`, atau bahkan objek `java.awt.Image`. Jika Anda memiliki array byte (misalnya, dari unggahan web), bungkus dalam `ByteArrayInputStream` dan berikan langsung.

```java
        // Step 3: Load the image that contains the text to be recognized
        ocrEngine.setImage("YOUR_DIRECTORY/french_invoice.png");
```

## Langkah 4: Lakukan OCR dan **ocr image to pdf** dalam satu panggilan

Aspose membuat langkah ini mudah: `recognizeToPdf` menjalankan mesin pengenalan dan menulis PDF yang dapat dicari dalam satu langkah.

```java
        // Step 4: Recognize the text and save it as a searchable PDF
        ocrEngine.recognizeToPdf("YOUR_DIRECTORY/french_invoice_searchable.pdf");
```

Di balik layar, perpustakaan membuat lapisan teks tak terlihat yang selaras dengan gambar asli. Saat Anda membuka file hasil di Adobe Reader, Anda dapat mengetik kata ke dalam kotak pencarian dan langsung melompat ke lokasi yang cocok.

## Langkah 5: Verifikasi hasil – seperti apa outputnya?

```java
        // Step 5: Inform the user that the PDF has been created
        System.out.println("Searchable PDF generated.");
    }
}
```

Jalankan program, lalu buka `french_invoice_searchable.pdf`. Coba cari kata yang Anda tahu ada di faktur (misalnya, “Total”). Jika sorotan muncul di tempat yang tepat, Anda telah berhasil **create searchable pdf**.  

![Contoh PDF yang dapat dicari](example.png)<!-- alt text includes primary keyword -->

### Output yang diharapkan

```
Searchable PDF generated.
```

Dan file PDF yang berada di `YOUR_DIRECTORY` yang dapat Anda bagikan, indeks, atau arsipkan.

## Langkah 6: Ekstrak teks mentah dari gambar (opsional)

Kadang-kadang Anda membutuhkan teks polos untuk pemrosesan lebih lanjut—mungkin untuk dimasukkan ke basis data atau menjalankan analisis sentimen. Aspose memungkinkan Anda menarik teks yang dikenali secara langsung:

```java
        // Optional: Get the extracted text as a String
        String extractedText = ocrEngine.getText();
        System.out.println("Extracted text:");
        System.out.println(extractedText);
```

Cuplikan ini menunjukkan **extract text from image** tanpa membuat PDF. Ini berguna ketika Anda hanya peduli pada konten, bukan tata letak visual.

## Menangani beberapa halaman atau gambar

Bagaimana jika sumber Anda adalah TIFF multi‑halaman atau folder JPEG? Anda dapat melakukan loop pada file-file tersebut dan memanggil `recognizeToPdf` untuk masing‑masing, lalu menggabungkan PDF menggunakan Aspose PDF atau perpustakaan lain. Berikut pola singkatnya:

```java
import java.io.File;
import com.aspose.pdf.*;

public class MultiPageDemo {
    public static void main(String[] args) throws Exception {
        OcrEngine engine = new OcrEngine();
        File folder = new File("YOUR_DIRECTORY/images");
        Document finalDoc = new Document();

        for (File img : folder.listFiles((d, n) -> n.matches(".*\\.(png|jpg|tif)"))) {
            engine.setImage(img.getAbsolutePath());
            // Save each page as a temporary PDF
            String tempPdf = img.getName() + ".pdf";
            engine.recognizeToPdf(tempPdf);
            // Append to final document
            Document pageDoc = new Document(tempPdf);
            finalDoc.getPages().add(pageDoc.getPages().get_Item(1));
        }
        finalDoc.save("YOUR_DIRECTORY/combined_searchable.pdf");
        System.out.println("All pages merged into searchable PDF.");
    }
}
```

**Pro tip:** Hapus PDF sementara setelah penggabungan untuk menjaga ruang kerja tetap rapi.

## Kesalahan umum dan cara menghindarinya

- **Low‑resolution images:** Akurasi OCR turun drastis di bawah 150 dpi. Perbesar atau minta pemindaian beresolusi lebih tinggi jika memungkinkan.  
- **Skewed pages:** Gambar yang diputar dapat membingungkan mesin. Gunakan `ocrEngine.getImagePreprocessingSettings().setDeskew(true)` untuk memperbaiki kemiringan ringan secara otomatis.  
- **Unsupported language:** Pastikan bahasa yang Anda atur termasuk dalam lisensi Aspose OCR Anda; jika tidak, mesin akan kembali ke bahasa Inggris.  
- **Large files:** Memproses TIFF 30 MB dapat memakan banyak memori. Pertimbangkan memecahnya menjadi bagian lebih kecil atau meningkatkan heap JVM (`-Xmx2g`).

## Langkah selanjutnya – ke mana melanjutkan

Sekarang Anda telah menguasai dasar-dasar **create searchable pdf**, Anda mungkin ingin mengeksplorasi:

- **Batch conversion:** Gabungkan pola multi‑halaman dengan penjadwal untuk memproses pemindaian masuk setiap malam.  
- **Metadata injection:** Gunakan Aspose PDF untuk menambahkan judul, penulis, atau tag khusus ke PDF yang dapat dicari.  
- **Digital signatures:** Amankan PDF dengan sertifikat setelah OCR, memastikan kepatuhan untuk dokumen legal.  

Semua ekstensi ini tetap bergantung pada konsep inti yang telah kami bahas: menginisialisasi mesin OCR, secara opsional mengatur bahasa, memuat gambar, dan memanggil `recognizeToPdf`.

---

### TL;DR

Kami telah menelusuri contoh lengkap yang dapat dijalankan yang menunjukkan cara **create searchable PDF** dari gambar menggunakan Aspose OCR for Java. Langkah‑langkahnya meliputi menginisialisasi mesin, secara opsional mengatur bahasa (menjawab “how to set language”), memuat gambar, melakukan OCR, menyimpan PDF yang dapat dicari, dan secara opsional mengekstrak teks polos. Kami juga membahas penanganan beberapa halaman, kesalahan umum, dan ide untuk otomatisasi lebih lanjut.

Cobalah dengan kwitansi, kontrak, atau catatan tulisan tangan Anda sendiri—ubah gambar statis menjadi dokumen yang sepenuhnya dapat dicari dalam hitungan detik. Selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}