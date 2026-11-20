---
category: general
date: 2026-04-26
description: Buat PDF yang dapat dicari dari gambar yang dipindai menggunakan Aspose
  OCR di C#. Pelajari cara mengonversi gambar yang dipindai, mengekstrak teks, dan
  menghasilkan PDF yang dapat dicari dengan cepat.
draft: false
keywords:
- create searchable pdf
- convert scanned image
- extract text from image
- how to ocr document
- convert tiff to pdf
language: id
og_description: Buat PDF yang dapat dicari dari gambar yang dipindai menggunakan Aspose
  OCR. Kode C# langkah demi langkah untuk mengonversi, mengekstrak teks, dan menghasilkan
  PDF yang dapat dicari.
og_title: Buat PDF yang Dapat Dicari dari Gambar Pindai – Panduan C#
tags:
- Aspose OCR
- C#
- PDF
- OCR
title: Buat PDF yang Dapat Dicari dari Gambar Pindai – Panduan C#
url: /id/net/text-recognition/create-searchable-pdf-from-scanned-image-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat PDF yang Dapat Dicari dari Gambar Pindai – Panduan C#

Pernah perlu **membuat PDF yang dapat dicari** dari kontrak kertas, kwitansi, atau arsip lama? Anda tidak sendirian—kebanyakan pengembang mengalami kendala ini ketika klien menyerahkan tumpukan pemindaian TIFF dan mengharapkan PDF yang dapat dicari sebagai hasil akhir.  

Dalam tutorial ini kami akan menunjukkan secara tepat **cara melakukan OCR pada dokumen** dan mengubah gambar pindai menjadi **PDF yang dapat dicari** dengan Aspose OCR untuk .NET. Pada akhir tutorial Anda akan dapat **mengonversi gambar pindai**, **mengekstrak teks dari gambar**, dan bahkan menangani TIFF multi‑halaman tanpa kesulitan.

## Apa yang Anda Butuhkan

* .NET 6.0 atau lebih baru (API bekerja dengan .NET Core, .NET Framework, dan .NET 5+).  
* Lisensi Aspose OCR yang valid atau Anda puas dengan watermark evaluasi.  
* Paket NuGet `Aspose.OCR` terpasang (`dotnet add package Aspose.OCR`).  
* File TIFF contoh (misalnya `contract_scan.tif`) yang ingin Anda ubah menjadi PDF yang dapat dicari.

Itu saja—tanpa perpustakaan tambahan, tanpa konfigurasi rumit. Siap? Ayo mulai.

![Create searchable PDF example](create-searchable-pdf.png "create searchable pdf example")

## Langkah 1 – Inisialisasi Mesin OCR (Buat PDF yang Dapat Dicari)

Hal pertama yang harus dilakukan: Anda memerlukan instance `OcrEngine`. Objek ini adalah mesin utama yang membaca bitmap, mengidentifikasi karakter, dan mengembalikan teks kepada Anda.  

```csharp
using Aspose.OCR;
using Aspose.OCR.Output;

// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Tell the engine which language to look for – Latin works for most English documents
ocrEngine.Language = Language.Latin;
```

**Mengapa mengatur bahasa?**  
Jika Anda membiarkannya pada nilai default, Aspose akan mencoba semua paket bahasa, yang memperlambat proses. Menentukan `Language.Latin` memberi tahu mesin untuk fokus pada alfabet Latin, memberikan peningkatan kecepatan dan hasil yang lebih akurat untuk kontrak berbahasa Inggris.

## Langkah 2 – Muat Gambar Pindai Anda (Konversi Gambar Pindai)

Sekarang kita memberi mesin gambar yang ingin diproses. Aspose dapat membaca jalur file, stream, atau bahkan `byte[]`. Untuk kesederhanaan kita akan menggunakan `ImageStream.FromFile`.  

```csharp
// Load the TIFF (or any supported image format)
ocrEngine.Image = ImageStream.FromFile(@"C:\Docs\contract_scan.tif");
```

Jika Anda pernah perlu **mengonversi TIFF ke PDF** nanti, ingat bahwa TIFF multi‑halaman ditangani secara otomatis—setiap frame menjadi halaman PDF terpisah.

## Langkah 3 – Jalankan OCR dan Ambil Teks (Ekstrak Teks dari Gambar)

Menjalankan OCR semudah memanggil `Recognize`. Mesin akan mengembalikan `RecognitionResult` yang berisi teks polos, skor kepercayaan, dan informasi tata letak.  

```csharp
// Perform the OCR operation
RecognitionResult result = ocrEngine.Recognize();

// The raw text is available via the Text property
string extractedText = result.Text;

// Quick sanity check – print the first 200 characters
Console.WriteLine(extractedText.Substring(0, Math.Min(200, extractedText.Length)));
```

**Tips pro:** Jika Anda hanya membutuhkan teks (tanpa PDF), Anda dapat berhenti di sini dan menulis `extractedText` ke file `.txt`. Namun kebanyakan waktu tujuan kami adalah PDF yang dapat dicari, jadi kami akan melanjutkan.

## Langkah 4 – Simpan sebagai PDF yang Dapat Dicari (Buat PDF yang Dapat Dicari)

Aspose membuat langkah akhir menjadi sederhana: cukup panggil `Save` dengan `SaveFormat.PdfSearchable`. Di balik layar, perpustakaan menyisipkan teks yang diekstrak sebagai lapisan tak terlihat sambil mempertahankan tampilan gambar asli.  

```csharp
// Save the result as a searchable PDF
ocrEngine.Save(@"C:\Docs\contract_searchable.pdf", SaveFormat.PdfSearchable);
```

Saat Anda membuka `contract_searchable.pdf` di penampil PDF apa pun, Anda dapat memilih, menyalin, dan mencari teks—tepat seperti yang diharapkan klien dari “PDF yang dapat dicari”.

## Menangani TIFF Multi‑Halaman (Konversi TIFF ke PDF)

Jika file sumber Anda berisi beberapa halaman, Aspose akan memperlakukan setiap frame sebagai halaman terpisah secara otomatis. Tidak diperlukan loop tambahan. Namun, Anda mungkin ingin mengontrol DPI atau kualitas gambar untuk setiap halaman:

```csharp
// Optional: tweak image processing settings before OCR
ocrEngine.ImageProcessingOptions.Dpi = 300; // higher DPI improves accuracy
ocrEngine.ImageProcessingOptions.Compression = ImageCompression.Jpeg;
```

Setelah mengatur opsi-opsi ini, ulangi **Langkah 2** untuk setiap frame, atau cukup arahkan `ImageStream.FromFile` ke TIFF multi‑halaman dan biarkan Aspose melakukan pekerjaan berat.

## Kesalahan Umum dan Cara Memperbaikinya

| Gejala | Penyebab Kemungkinan | Solusi |
|---------|--------------|-----|
| Teks berantakan atau hilang | Bahasa yang diatur salah | Atur `ocrEngine.Language` ke paket bahasa yang tepat (misalnya `Language.German`). |
| PDF berukuran besar (10 MB untuk pemindaian satu halaman) | Kompresi gambar default rendah | Sesuaikan `ocrEngine.ImageProcessingOptions.Compression` menjadi `Jpeg` dan tetapkan nilai `Quality` yang wajar (0‑100). |
| OCR berjalan sangat lambat | Menggunakan deteksi bahasa `Auto` default | Tentukan secara eksplisit bahasa yang Anda harapkan. |
| Tidak ada lapisan yang dapat dicari muncul | Disimpan dengan `SaveFormat.Pdf` bukan `PdfSearchable` | Gunakan `PdfSearchable`. |

## Contoh Lengkap End‑to‑End

Menggabungkan semuanya, berikut adalah aplikasi konsol siap‑jalankan yang dapat Anda salin‑tempel ke Visual Studio:

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace SearchablePdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize OCR engine
            OcrEngine ocrEngine = new OcrEngine
            {
                Language = Language.Latin,
                // Optional: improve accuracy for low‑resolution scans
                ImageProcessingOptions = { Dpi = 300, Compression = ImageCompression.Jpeg }
            };

            // 2️⃣ Load the scanned image (convert scanned image)
            string inputPath = @"C:\Docs\contract_scan.tif";
            ocrEngine.Image = ImageStream.FromFile(inputPath);

            // 3️⃣ Run OCR and extract text (extract text from image)
            RecognitionResult result = ocrEngine.Recognize();
            Console.WriteLine("First 200 characters of extracted text:");
            Console.WriteLine(result.Text.Substring(0, Math.Min(200, result.Text.Length)));

            // 4️⃣ Save as searchable PDF (create searchable pdf)
            string outputPath = @"C:\Docs\contract_searchable.pdf";
            ocrEngine.Save(outputPath, SaveFormat.PdfSearchable);
            Console.WriteLine($"Searchable PDF created at: {outputPath}");
        }
    }
}
```

**Apa yang akan Anda lihat:**  
* Jendela konsol yang mencetak cuplikan teks hasil OCR.  
* File `contract_searchable.pdf` yang berada di samping TIFF asli Anda. Buka file tersebut, tekan **Ctrl + F**, dan cari kata apa pun yang muncul dalam pemindaian asli—voilà, berhasil.

## Langkah Selanjutnya & Topik Terkait

* **How to OCR document** batches – bungkus kode di atas dalam loop `foreach` dan proses seluruh folder.  
* **Convert scanned image** formats other than TIFF (PNG, JPEG) – API yang sama berfungsi; cukup ubah ekstensi file.  
* **Extract text from image** for further analysis – kirim `result.Text` ke pipeline pemrosesan bahasa alami.  
* **Optimize PDF size** – jelajahi `PdfSaveOptions` untuk mengompres gambar lebih lanjut atau menyematkan font hanya bila diperlukan.  

Cobalah ide-ide tersebut, dan Anda akan segera menjadi orang yang diandalkan untuk permintaan “ubah pemindaian ini menjadi PDF yang dapat dicari”.

---

### TL;DR

Anda sekarang tahu cara **membuat PDF yang dapat dicari** dari gambar pindai menggunakan Aspose OCR di C#. Prosesnya: inisialisasi mesin, muat gambar, jalankan OCR, dan simpan dengan `PdfSearchable`. Sesuaikan pengaturan bahasa, DPI, dan kompresi untuk menangani kasus khusus, dan Anda siap untuk **mengonversi gambar pindai**, **mengekstrak teks dari gambar**, dan bahkan **mengonversi TIFF ke PDF** secara skala. Selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}