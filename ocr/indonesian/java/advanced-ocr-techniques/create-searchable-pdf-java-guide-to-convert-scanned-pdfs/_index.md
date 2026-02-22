---
category: general
date: 2026-02-22
description: Buat PDF yang dapat dicari dari PDF yang dipindai menggunakan Aspose
  OCR di Java. Pelajari cara mengonversi PDF yang dipindai, mengompres gambar PDF,
  dan mengenali OCR PDF secara efisien.
draft: false
keywords:
- create searchable pdf
- convert scanned pdf
- compress pdf images
- recognize pdf ocr
- image pdf to text
language: id
og_description: Buat PDF yang dapat dicari dari PDF yang dipindai menggunakan Aspose
  OCR di Java. Tutorial langkah demi langkah ini menunjukkan cara mengonversi PDF
  yang dipindai, mengompres gambar PDF, dan mengenali OCR pada PDF.
og_title: Buat PDF yang Dapat Dicari – Panduan Java untuk Mengonversi PDF yang Dipindai
tags:
- Java
- OCR
- PDF
- Aspose
title: Buat PDF yang Dapat Dicari – Panduan Java untuk Mengonversi PDF yang Dipindai
url: /id/java/advanced-ocr-techniques/create-searchable-pdf-java-guide-to-convert-scanned-pdfs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat PDF yang Dapat Dicari – Panduan Java untuk Mengonversi PDF yang Dipindai

Pernah membutuhkan **create searchable PDF** dari tumpukan dokumen yang dipindai? Ini adalah masalah umum—PDF Anda terlihat baik, tetapi Anda tidak dapat menekan *Ctrl + F* untuk menemukan apa pun. Kabar baiknya? Dengan beberapa baris Java dan Aspose OCR Anda dapat mengubah PDF yang hanya berisi gambar menjadi file yang sepenuhnya dapat dicari, **convert scanned PDF** menjadi teks, dan bahkan memperkecil hasilnya dengan **compressing PDF images**.  

Dalam tutorial ini kami akan membahas contoh lengkap yang dapat dijalankan, menjelaskan mengapa setiap pengaturan penting, dan menunjukkan cara menyesuaikan proses untuk kasus khusus seperti pemindaian multi‑halaman atau gambar beresolusi rendah. Pada akhir tutorial Anda akan memiliki potongan kode yang solid dan siap produksi yang **recognize pdf ocr** secara andal serta menghasilkan dokumen yang dapat dicari dengan rapi.

---

## Apa yang Anda Butuhkan

- **Java 17** (atau JDK terbaru apa pun; API bersifat JDK‑agnostic)  
- **Aspose.OCR for Java** library – Anda dapat mengambilnya dari Maven Central (`com.aspose:aspose-ocr`)  
- PDF yang dipindai (hanya gambar) yang ingin Anda jadikan dapat dicari  
- IDE atau editor teks yang Anda sukai (IntelliJ, VS Code, Eclipse…)

Tidak ada kerangka kerja berat, tidak ada layanan eksternal—hanya Java murni dan satu JAR pihak ketiga.  

---

![contoh pdf yang dapat dicari](placeholder-image.png "Ilustrasi PDF yang dapat dicari yang dibuat dari dokumen yang dipindai")

*Teks alt gambar:* **create searchable pdf** ilustrasi yang menunjukkan sebelum‑dan‑sesudah PDF yang dipindai diubah menjadi teks yang dapat dicari.

---

## Langkah 1 – Inisialisasi OCR Engine  

Hal pertama yang harus Anda lakukan adalah membuat instance `OcrEngine`. Anggaplah itu sebagai otak yang akan menganalisis setiap bitmap di dalam PDF dan menghasilkan karakter Unicode.  

```java
import com.aspose.ocr.*;

public class PdfToSearchableDemo {
    public static void main(String[] args) throws Exception {

        // Initialise the OCR engine – this object holds licensing info and global settings
        OcrEngine ocrEngine = new OcrEngine();
```

> **Pro tip:** Jika Anda berencana memproses banyak PDF secara berurutan, gunakan kembali `OcrEngine` yang sama daripada membuat yang baru setiap kali. Ini menghemat beberapa milidetik dan mengurangi beban memori.

---

## Langkah 2 – Konfigurasi Opsi OCR Khusus PDF  

Aspose memungkinkan Anda menyesuaikan secara detail bagaimana PDF output dibangun. Tiga pengaturan di bawah ini paling berpengaruh untuk **compress pdf images** sambil mempertahankan kemampuan pencarian.

```java
        // Configure PDF‑specific options
        PdfOcrOptions pdfOcrOptions = new PdfOcrOptions();
        pdfOcrOptions.setOutputDpi(300);                 // Higher DPI = better text recognition
        pdfOcrOptions.setCompressImages(true);           // Shrinks the final file size
        pdfOcrOptions.setEmbedOriginalImages(true);      // Keeps the visual look of the original scan
```

- **Output DPI** – 300 dpi adalah titik optimal; nilai yang lebih rendah mempercepat proses tetapi dapat melewatkan huruf kecil.  
- **CompressImages** – mengaktifkan kompresi PNG lossless di balik layar; PDF yang dapat dicari tetap tajam namun lebih ringan.  
- **EmbedOriginalImages** – tanpa flag ini mesin akan membuang raster asli, meninggalkan hanya teks tak terlihat. Menyimpan gambar memastikan PDF terlihat persis seperti hasil pemindaian, yang banyak diminta oleh tim kepatuhan.

---

## Langkah 3 – Muat PDF yang Dipindai ke dalam `OcrInput`  

Aspose membaca file sumber melalui pembungkus `OcrInput`. Anda dapat menambahkan beberapa file, tetapi untuk demo ini kami fokus pada satu **image PDF**.

```java
        // Load the scanned PDF (image‑only) into an OcrInput object
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/input.pdf");   // <- replace with the path to your file
```

> **Mengapa tidak langsung melewatkan `File`?** Menggunakan `OcrInput` memberi Anda fleksibilitas untuk menggabungkan beberapa PDF atau bahkan mencampur file gambar (PNG, JPEG) sebelum OCR. Ini adalah pola yang direkomendasikan ketika Anda **convert scanned pdf** yang mungkin terbagi di beberapa sumber.

---

## Langkah 4 – Lakukan OCR dan Dapatkan PDF yang Dapat Dicari sebagai Byte Array  

Sekarang keajaiban terjadi. Mesin menganalisis setiap halaman, menjalankan OCR-nya, dan membangun PDF baru yang berisi gambar asli serta lapisan teks tersembunyi.

```java
        // Perform OCR – the result is a byte array representing the searchable PDF
        byte[] searchablePdfBytes = ocrEngine.recognizePdf(ocrInput, pdfOcrOptions);
```

Jika Anda memerlukan teks mentah untuk keperluan lain (mis., pengindeksan), Anda juga dapat memanggil `ocrEngine.recognize(ocrInput)` yang mengembalikan sebuah `String`. Tetapi untuk tujuan **create searchable pdf**, byte array adalah yang akan Anda tulis ke disk.

---

## Langkah 5 – Simpan PDF yang Dapat Dicari ke Disk  

Akhirnya, tulis byte array ke sebuah file. NIO Java membuat ini menjadi satu baris kode.

```java
        // Write the searchable PDF to disk
        java.nio.file.Files.write(
                java.nio.file.Paths.get("YOUR_DIRECTORY/searchable_output.pdf"),
                searchablePdfBytes
        );

        System.out.println("Searchable PDF created.");
    }
}
```

Saat Anda membuka `searchable_output.pdf` di Adobe Acrobat atau penampil modern lainnya, Anda akan melihat bahwa kini Anda dapat memilih, menyalin, dan mencari teks—tepat seperti yang dijanjikan oleh transformasi **image pdf to text**.

---

## Mengonversi PDF yang Dipindai ke Teks dengan OCR (Opsional)

Terkadang Anda hanya membutuhkan teks polos yang diekstrak, bukan PDF baru. Anda dapat menggunakan kembali mesin yang sama:

```java
        // Optional: extract plain text from the scanned PDF
        String extractedText = ocrEngine.recognize(ocrInput).getText();
        java.nio.file.Files.write(
                java.nio.file.Paths.get("YOUR_DIRECTORY/extracted_text.txt"),
                extractedText.getBytes()
        );
```

Potongan kode ini menunjukkan betapa mudahnya **recognize pdf ocr** untuk pemrosesan lanjutan seperti mengisi indeks pencarian atau melakukan analisis bahasa alami.

---

## Kompres Gambar PDF untuk File Lebih Kecil  

Jika pemindaian sumber Anda sangat besar (mis., pemindaian warna 600 dpi), PDF yang dapat dicari yang dihasilkan masih dapat berukuran besar. Selain flag `setCompressImages(true)`, Anda dapat menurunkan skala secara manual sebelum OCR:

```java
        // Downscale each page image to 150 dpi before OCR (reduces size dramatically)
        pdfOcrOptions.setOutputDpi(150);
```

Menurunkan DPI akan mengurangi ukuran file kira-kira setengah, tetapi uji keterbacaan—beberapa huruf menjadi tidak terbaca di bawah 150 dpi. Pertukaran antara **compress pdf images** dan akurasi OCR adalah hal yang akan Anda putuskan berdasarkan batasan penyimpanan Anda.

---

## Penjelasan Pengaturan OCR PDF  

| Setting                | Effect on Output                         | Typical Use‑Case                                   |
|------------------------|------------------------------------------|----------------------------------------------------|
| `setOutputDpi(int)`    | Mengontrol resolusi raster output OCR    | Arsip berkualitas tinggi (300 dpi) vs. PDF web ringan (150 dpi) |
| `setCompressImages`    | Mengaktifkan kompresi PNG                | Saat Anda perlu mengirim PDF lewat email atau menyimpannya di cloud |
| `setEmbedOriginalImages`| Menjaga agar pemindaian asli tetap terlihat | Dokumen hukum atau kepatuhan yang harus mempertahankan tampilan asli |
| `setLanguage` (optional) | Memaksa model bahasa (mis., "eng")      | Korpus multibahasa di mana deteksi otomatis default dapat gagal |

Memahami pengaturan ini membantu Anda **recognize pdf ocr** secara lebih cerdas dan menghindari jebakan “teks buram”.

---

## Image PDF to Text – Kendala Umum dan Cara Mengatasinya  

1. **Pemindaian beresolusi rendah** – akurasi OCR turun drastis di bawah 150 dpi. Tingkatkan skala sumber sebelum memberikannya ke Aspose, atau minta DPI lebih tinggi dari pemindai.  
2. **Halaman terrotasi** – Jika halaman dipindai miring, aktifkan auto‑rotate: `pdfOcrOptions.setAutoRotate(true);`.  
3. **PDF terenkripsi** – Mesin tidak dapat membaca file yang dilindungi kata sandi; dekripsi terlebih dahulu menggunakan `PdfDocument` dari Aspose.PDF.  
4. **Raster dan teks campur** – Beberapa PDF sudah memiliki lapisan teks tersembunyi. Menjalankan OCR lagi dapat menggandakan teks. Gunakan `PdfOcrOptions.setSkipExistingText(true);` untuk mempertahankan lapisan asli.  

Menangani masalah ini memastikan alur kerja **create searchable pdf** Anda kuat di seluruh koleksi dokumen dunia nyata.

---

## Contoh Lengkap yang Berfungsi (Semua Langkah dalam Satu File)

Berikut adalah kelas Java lengkap yang dapat Anda salin‑tempel ke IDE Anda. Ganti `YOUR_DIRECTORY` dengan jalur folder yang sebenarnya.

```java
import com.aspose.ocr.*;
import java.nio.file.Files;
import java.nio.file.Paths;

public class PdfToSearchableDemo {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Initialise the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Configure PDF‑specific OCR options
        PdfOcrOptions pdfOcrOptions = new PdfOcrOptions();
        pdfOcrOptions.setOutputDpi(300);                 // higher DPI improves accuracy
        pdfOcrOptions.setCompressImages(true);           // reduce output size
        pdfOcrOptions.setEmbedOriginalImages(true);      // keep original visual fidelity

        // 3️⃣ Load the scanned PDF (image‑only) into an OcrInput object
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/input.pdf");        // <-- your source file

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}