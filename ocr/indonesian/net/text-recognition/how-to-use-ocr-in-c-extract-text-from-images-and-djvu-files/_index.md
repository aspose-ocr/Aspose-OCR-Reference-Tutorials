---
category: general
date: 2026-04-04
description: Cara menggunakan OCR dengan cepat dan aman. Pelajari cara mengekstrak
  teks dari gambar, mengonversi DJVU ke teks, dan memuat gambar untuk OCR dengan Aspose.OCR.
draft: false
keywords:
- how to use OCR
- extract text from image
- convert djvu to text
- load image for OCR
- extract text from djvu
language: id
og_description: Cara menggunakan OCR di C# untuk mengekstrak teks dari file gambar
  dan dokumen DJVU. Tutorial langkah demi langkah dengan kode lengkap.
og_title: Cara Menggunakan OCR di C# – Panduan Lengkap
tags:
- OCR
- C#
- Aspose
title: Cara Menggunakan OCR di C# – Mengekstrak Teks dari Gambar dan File DJVU
url: /id/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-images-and-djvu-files/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menggunakan OCR di C# – Mengekstrak Teks dari Gambar dan File DJVU

Pernah bertanya-tanya **bagaimana cara menggunakan OCR** untuk mengambil kata‑kata dari halaman yang dipindai tanpa harus mengetik manual? Anda bukan satu‑satunya. Dalam banyak proyek—baik Anda mendigitalkan buku lama atau mengekstrak data dari kwitansi—mendapatkan teks dari gambar adalah masalah harian. Kabar baiknya? Dengan Aspose.OCR Anda dapat melakukannya dalam beberapa baris kode, bahkan ketika sumbernya adalah file DJVU.

Di panduan ini kami akan membahas semua yang Anda perlukan untuk **mengekstrak teks dari gambar**, **memuat gambar untuk OCR**, dan bahkan **mengonversi DJVU ke teks** menggunakan C#. Pada akhir tutorial Anda akan memiliki aplikasi konsol siap‑jalankan yang mencetak teks yang dikenali langsung ke konsol. Tanpa misteri, tanpa dependensi tambahan, hanya C# murni dan Aspose.

## Apa yang Akan Anda Pelajari

- Cara menginstal dan mereferensikan pustaka Aspose.OCR.
- Kode tepat yang diperlukan untuk **memuat gambar untuk OCR**, baik itu PNG, JPEG, atau halaman DJVU.
- Cara memanggil engine dan mengambil hasilnya.
- Tips untuk menangani dokumen besar dan jebakan umum.
- Contoh lengkap yang dapat dijalankan yang dapat Anda salin‑tempel ke Visual Studio.

> **Prasyarat:** .NET 6.0 atau yang lebih baru dan lisensi Aspose.OCR yang valid (atau percobaan gratis). Jika Anda belum memiliki pustaka tersebut, dapatkan dari NuGet dengan `dotnet add package Aspose.OCR`.

---

## Cara Menggunakan OCR dengan Aspose di C#

Ini adalah langkah inti di mana kami benar‑benar menjawab pertanyaan **bagaimana cara menggunakan OCR** dalam proyek C#. Kode di bawah ini adalah program lengkap; Anda dapat menempelkannya ke aplikasi konsol baru dan menekan F5.

```csharp
using System;
using Aspose.OCR;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create the OCR engine instance.
            var ocrEngine = new OcrEngine();

            // Step 2: Load the image (or DJVU page) you want to analyze.
            // Replace the path with your own file location.
            ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/book-page.djvu");

            // Step 3: Run the recognition process.
            OcrResult ocrResult = ocrEngine.Recognize();

            // Step 4: Output the extracted text.
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

**Mengapa ini berhasil:**  
- `OcrEngine` adalah titik masuk; ia menyederhanakan proses berat pra‑pemrosesan gambar, deteksi bahasa, dan klasifikasi karakter.  
- `ImageStream.FromFile` dapat menangani banyak format, termasuk DJVU, yang berarti Anda dapat **mengonversi DJVU ke teks** tanpa langkah konversi tambahan.  
- `Recognize()` mengembalikan objek `OcrResult` yang berisi output teks biasa, skor kepercayaan, dan bahkan kotak pembatas jika Anda membutuhkannya nanti.

Menjalankan program mencetak sesuatu seperti:

```
=== OCR Result ===
In the beginning God created the heavens and the earth.
```

Itu saja—operasi **mengekstrak teks dari DJVU** pertama Anda yang berhasil.

![contoh cara menggunakan OCR](/images/ocr-demo.png "Tangkapan layar yang menunjukkan cara menggunakan OCR dalam aplikasi konsol C#")

*Teks alternatif: “cara menggunakan OCR” tangkapan layar output konsol.*

## Memuat Gambar untuk OCR

Sebelum engine dapat membaca apa pun, Anda harus **memuat gambar untuk OCR** dengan benar. Aspose mendukung sebagian besar format raster secara bawaan, namun beberapa tips dapat membuat pengenalan lebih lancar:

- **Ubah ukuran gambar besar** menjadi maksimum 2000 px pada sisi terpanjang. File yang terlalu besar meningkatkan penggunaan memori dan dapat memperlambat engine.
- **Konversi gambar berwarna ke grayscale** jika Anda melihat latar belakang berisik. Gunakan `ocrEngine.Image = ImageStream.FromFile(path).ConvertToGrayscale();`.
- **Atur DPI secara manual** untuk pemindaian beresolusi rendah (`ocrEngine.Image.DpiX = 300; ocrEngine.Image.DpiY = 300;`).

Penyesuaian ini opsional namun sering meningkatkan akurasi saat Anda **mengekstrak teks dari gambar** seperti kwitansi yang dipindai.

## Mengekstrak Teks dari Gambar – Praktik Terbaik

Ketika Anda menangani format gambar umum (PNG, JPEG, BMP), langkah‑langkahnya tetap sama, namun Anda dapat menyetel engine secara halus:

```csharp
ocrEngine.Image = ImageStream.FromFile("sample.png");

// Optional: enable language packs for better accuracy.
ocrEngine.Language = Language.English;

// Optional: set recognition mode to auto.
ocrEngine.RecognitionMode = RecognitionMode.Auto;
```

- **Pemilihan bahasa** penting. Jika Anda memproses dokumen multibahasa, atur `ocrEngine.Language = Language.Multilingual;`.
- **RecognitionMode** dapat berupa `Auto`, `Fast`, atau `Accurate`. `Accurate` menghasilkan kualitas lebih tinggi dengan mengorbankan kecepatan—gunakan untuk tugas arsip.

## Mengonversi DJVU ke Teks – Menangani File Multi‑Halaman

File DJVU sering berisi beberapa halaman. Aspose memperlakukan setiap halaman sebagai aliran gambar terpisah, sehingga Anda dapat mengulanginya:

```csharp
using Aspose.OCR;
using System.Collections.Generic;

var ocrEngine = new OcrEngine();
List<string> allPagesText = new List<string>();

int pageCount = ImageStream.GetPageCount("book.djvu");
for (int i = 1; i <= pageCount; i++)
{
    ocrEngine.Image = ImageStream.FromFile("book.djvu", i); // Load page i
    OcrResult result = ocrEngine.Recognize();
    allPagesText.Add(result.Text);
}

// Combine all pages into a single string.
string fullText = string.Join("\n--- Page Break ---\n", allPagesText);
Console.WriteLine(fullText);
```

**Mengapa loop?**  
File DJVU pada dasarnya adalah tumpukan gambar. Dengan mengiterasi setiap halaman Anda **mengekstrak teks dari DJVU** secara berurutan, mempertahankan alur dokumen asli.

## Kesalahan Umum dan Tips Pro

| Masalah | Mengapa Terjadi | Solusi |
|------|----------------|-----|
| **Karakter sampah** | DPI rendah atau kompresi berat | Perbesar gambar, atur `ocrEngine.Image.DpiX/Y = 300` |
| **Pemrosesan lambat** | Menggunakan mode `Accurate` pada file besar | Beralih ke mode `Fast` untuk pekerjaan massal |
| **Tidak ada dukungan bahasa** | Bahasa default hanya Inggris | Muat paket bahasa tambahan (`ocrEngine.Language = Language.Spanish;`) |
| **Kesalahan out‑of‑memory** | Memuat banyak halaman resolusi tinggi sekaligus | Proses halaman satu‑per‑satu dan lepaskan sumber daya (`ocrEngine.Dispose();`) |

Tips **pro** cepat: selalu panggil `ocrEngine.Dispose()` setelah selesai dengan sebuah halaman. Ini membebaskan sumber daya native dan mencegah kebocoran memori halus yang dapat menyebabkan layanan yang berjalan lama crash.

## Menguji Pipeline OCR Anda

Untuk memverifikasi semuanya berfungsi, coba pemeriksaan sederhana berikut:

1. **Cetak panjang** string yang dikenali: `Console.WriteLine($"Characters recognized: {ocrResult.Text.Length}");`
2. **Bandingkan dengan teks yang diketahui** menggunakan pustaka diff sederhana jika Anda memiliki data referensi.
3. **Catat skor kepercayaan** (`ocrResult.Confidence`) untuk secara otomatis mendeteksi halaman berkualitas rendah.

Jika skor kepercayaan secara konsisten di bawah 0.7, tinjau kembali langkah pra‑pemrosesan gambar yang disebutkan sebelumnya.

## Langkah Selanjutnya

Sekarang Anda sudah tahu **bagaimana cara menggunakan OCR**, pertimbangkan untuk memperluas alur kerja Anda:

- **Pemrosesan batch**: Bungkus loop dalam `Parallel.ForEach` untuk mempercepat koleksi besar.
- **Ekspor ke PDF**: Gunakan Aspose.PDF untuk menyematkan teks yang dikenali sebagai lapisan tersembunyi untuk PDF yang dapat dicari.
- **Integrasi dengan AI**: Kirimkan string yang diekstrak ke model bahasa untuk rangkuman atau ekstraksi entitas.

Semua ini dibangun di atas fondasi yang baru saja Anda siapkan, dan setiap langkah mendapat manfaat dari prinsip **mengekstrak teks dari gambar** yang sama yang telah kami bahas.

## Kesimpulan

Kami telah menyelami secara mendalam **bagaimana cara menggunakan OCR** di C# dengan Aspose, mencakup semua hal mulai dari memuat gambar, **mengekstrak teks dari gambar**, menangani file **DJVU**, dan memecahkan masalah umum. Contoh lengkap yang dapat dijalankan di atas memberi Anda titik awal yang kuat, dan tips yang tersebar di seluruh tutorial seharusnya membantu Anda menyesuaikan solusi untuk proyek dunia nyata.  

Cobalah, sesuaikan pengaturan untuk dokumen spesifik Anda, dan Anda akan mengubah halaman yang dipindai menjadi teks yang dapat dicari dalam sekejap. Ada pertanyaan atau file sulit yang tidak mau bekerja? Tinggalkan komentar—selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}