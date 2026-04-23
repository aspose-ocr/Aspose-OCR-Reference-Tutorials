---
category: general
date: 2026-03-20
description: 'Buat PDF yang dapat dicari dengan cepat: konversi gambar ke PDF, ekstrak
  teks dari gambar, dan tambahkan lapisan teks tersembunyi untuk pencarian penuh.'
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- extract text from image
- pdf with hidden text
- scan image to pdf
language: id
og_description: Buat PDF yang dapat dicari di C# dengan mengonversi gambar menjadi
  PDF, mengekstrak teks, dan menyematkan lapisan tersembunyi untuk pencarian instan.
og_title: Buat PDF yang Dapat Dicari dari Gambar – Tutorial Lengkap C#
tags:
- Aspose
- C#
- OCR
- PDF generation
title: Buat PDF yang Dapat Dicari dari Gambar di C# – Panduan Langkah demi Langkah
url: /id/net/text-recognition/create-searchable-pdf-from-image-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat PDF yang Dapat Dicari dari Gambar di C# – Panduan Lengkap

Pernah perlu **membuat PDF yang dapat dicari** dari faktur yang dipindai tetapi tidak ingin mengetik semuanya secara manual? Anda bukan satu-satunya. Dalam banyak alur kerja kantor, mengubah pemindaian bitmap menjadi PDF yang sebenarnya dapat dicari adalah masalah harian. Kabar baik? Dengan beberapa baris C# dan pustaka OCR & PDF dari Aspose, Anda dapat mengotomatisasi seluruh proses—tanpa perlu menyalin‑tempel manual.

Dalam tutorial ini kami akan menjelaskan cara **mengonversi gambar ke PDF**, mengekstrak teks dari gambar tersebut, dan kemudian menumpuk teks secara tak terlihat sehingga file akhir berperilaku seperti PDF asli. Pada akhir tutorial Anda akan memiliki metode siap pakai untuk membuat **pdf dengan teks tersembunyi** yang berfungsi untuk dokumen hasil pemindaian apa pun, baik itu faktur, kontrak, atau kwitansi.

## Apa yang Anda Butuhkan

- .NET 6.0 atau lebih baru (kode menggunakan pernyataan `using var`, jadi SDK terbaru memudahkan)
- Paket NuGet Aspose.OCR dan Aspose.Pdf (`Install-Package Aspose.OCR` dan `Install-Package Aspose.Pdf`)
- File gambar contoh (PNG, JPG, atau TIFF) yang berisi teks yang ingin Anda indeks
- Visual Studio 2022 atau IDE apa pun yang Anda sukai

> **Pro tip:** Jika Anda bekerja dengan pemindaian multi‑halaman, cukup lakukan loop pada setiap gambar dan ulangi langkah‑langkahnya – logika yang sama berlaku.

---

## Langkah 1 – Inisialisasi Mesin OCR (Ekstrak Teks dari Gambar)

Sebelum kita dapat menyematkan teks yang dapat dicari, kita harus benar‑benar membaca karakter dari gambar. `OcrEngine` milik Aspose melakukan pekerjaan berat tersebut.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// Create the OCR engine and tell it which language to look for.
// English works for most invoices, but you can set Language.French, etc.
using var ocrEngine = new OcrEngine
{
    Language = Language.English
};
```

**Mengapa ini penting:** Menginisialisasi mesin dengan bahasa yang tepat secara dramatis meningkatkan akurasi. Jika Anda melewatkannya, OCR dapat salah mengenali angka—sesuatu yang pasti ingin Anda hindari pada dokumen keuangan.

---

## Langkah 2 – Muat Gambar Hasil Pindai Anda (Konversi Gambar ke PDF)

Sekarang kami memuat bitmap ke memori. Aspose bekerja langsung dengan `System.Drawing.Image`, jadi format apa pun yang didukung .NET dapat digunakan.

```csharp
using System.Drawing;

// Replace the path with the location of your scanned file.
var inputImage = Image.FromFile(@"C:\Docs\invoice.png");
```

Jika Anda memiliki alur kerja **scan image to PDF** yang sudah menghasilkan TIFF multi‑halaman, cukup ubah ekstensi file dan ulangi langkah pemuatan untuk setiap halaman.

---

## Langkah 3 – Jalankan OCR dan Tangkap Teks yang Diakui

Dengan gambar siap, kami meminta mesin OCR untuk melakukan magisnya.

```csharp
// Perform OCR – the result contains the raw text and confidence scores.
var ocrResult = ocrEngine.Recognize(inputImage);

// For debugging, you might want to see what was read.
Console.WriteLine("OCR Output:");
Console.WriteLine(ocrResult.Text);
```

**Kasus khusus:** Jika gambar beresolusi rendah (< 300 dpi), tingkat kepercayaan menurun. Pertimbangkan untuk memperbesar atau memindai ulang dengan DPI yang lebih tinggi sebelum memberikannya ke mesin.

---

## Langkah 4 – Buat PDF dan Tempatkan Gambar Asli sebagai Latar Belakang

Sebuah **pdf dengan teks tersembunyi** tetap memerlukan representasi visual dari hasil pindai. Kami akan menambahkan gambar sebagai latar belakang halaman.

```csharp
using Aspose.Pdf;

// Start a fresh PDF document.
var pdfDocument = new Document();

// Add a new page.
var pdfPage = pdfDocument.Pages.Add();

// Insert the image; it will fill the page by default.
pdfPage.Paragraphs.Add(new Aspose.Pdf.Image
{
    ImageInfo = new ImageInfo(@"C:\Docs\invoice.png")
});
```

**Mengapa kami menggunakan gambar sebagai latar belakang:** Pengguna masih dapat melihat hasil pindai asli secara tepat, mempertahankan tanda tangan dan stempel, sementara lapisan teks tersembunyi memberikan kemampuan pencarian.

---

## Langkah 5 – Lapisi Teks OCR sebagai Lapisan Tak Terlihat (PDF dengan Teks Tersembunyi)

Berikut bagian penting: kami menambahkan `TextFragment` yang berada di atas gambar tetapi diatur menjadi tak terlihat. Aspose.Pdf membuat ini menjadi sederhana.

```csharp
using Aspose.Pdf.Text;

// Create a text fragment from the OCR result.
var searchableText = new TextFragment(ocrResult.Text)
{
    // Position (0,0) aligns with the bottom‑left of the page.
    Position = new Position(0, 0),

    // Make the text invisible – it still participates in search.
    TextState = { Font = FontRepository.FindFont("Arial"), FontSize = 0.1f, IsHidden = true }
};

// Add the invisible text to the same page.
pdfPage.Paragraphs.Add(searchableText);
```

**Penjelasan:** Mengatur ukuran font yang sangat kecil dan menandai fragmen sebagai tersembunyi menjaga output visual tetap bersih sekaligus memastikan lapisan teks PDF berisi hasil OCR. Mesin pencari dan pembaca PDF akan mengindeksnya.

---

## Langkah 6 – Simpan PDF yang Dapat Dicari

Akhirnya, tulis dokumen ke disk.

```csharp
// Choose a destination path.
string outputPath = @"C:\Docs\invoice_searchable.pdf";

// Save the PDF. The file now contains both the image and searchable text.
pdfDocument.Save(outputPath);

Console.WriteLine($"Searchable PDF created at: {outputPath}");
```

Buka file hasilnya di Adobe Reader, tekan **Ctrl + F**, ketik kata yang Anda lihat di faktur, dan Anda akan melihat hasil pencarian disorot—meskipun teks tersebut tidak pernah terlihat.

---

## Contoh Lengkap yang Berfungsi (Semua Langkah Bersama)

Berikut adalah program lengkap yang dapat Anda salin‑tempel ke aplikasi konsol. Program ini dapat dikompilasi dan dijalankan apa adanya, dengan asumsi paket NuGet telah terpasang dan jalur file sudah benar.

```csharp
// ------------------------------------------------------------
// Create Searchable PDF from Image – Complete C# Example
// ------------------------------------------------------------
using System;
using System.Drawing;
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine
        using var ocrEngine = new OcrEngine
        {
            Language = Language.English
        };

        // 2️⃣ Load scanned image
        var inputImagePath = @"C:\Docs\invoice.png";
        var inputImage = Image.FromFile(inputImagePath);

        // 3️⃣ Perform OCR
        var ocrResult = ocrEngine.Recognize(inputImage);
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(ocrResult.Text);

        // 4️⃣ Create PDF and add image as background
        var pdfDocument = new Document();
        var pdfPage = pdfDocument.Pages.Add();
        pdfPage.Paragraphs.Add(new Aspose.Pdf.Image
        {
            ImageInfo = new ImageInfo(inputImagePath)
        });

        // 5️⃣ Add invisible searchable text layer
        var searchableText = new TextFragment(ocrResult.Text)
        {
            Position = new Position(0, 0),
            TextState = { Font = FontRepository.FindFont("Arial"), FontSize = 0.1f, IsHidden = true }
        };
        pdfPage.Paragraphs.Add(searchableText);

        // 6️⃣ Save the searchable PDF
        var outputPath = @"C:\Docs\invoice_searchable.pdf";
        pdfDocument.Save(outputPath);
        Console.WriteLine($"✅ Searchable PDF saved to: {outputPath}");
    }
}
```

**Hasil yang diharapkan:**  
- `invoice_searchable.pdf` tampak identik dengan `invoice.png`.  
- Pencarian teks berfungsi untuk kata apa pun yang muncul dalam hasil pindai asli.  
- Ukuran file hanya bertambah sedikit (teks tersembunyi menambah beberapa kilobyte).

---

## Pertanyaan yang Sering Diajukan & Kasus Khusus

### Bisakah saya memproses banyak halaman dalam satu PDF?

Tentu saja. Bungkus logika OCR‑dan‑PDF di dalam loop `foreach (string imagePath in imageFiles)`, membuat `Page` baru untuk setiap iterasi. Lapisan teks tersembunyi ditambahkan per halaman, sehingga pencarian berfungsi di seluruh dokumen.

### Bagaimana jika dokumen saya berisi banyak bahasa?

Setel `ocrEngine.Language` ke `Language.Multilingual` atau buat mesin terpisah untuk setiap segmen bahasa. Aspose akan mengembalikan hasil campuran bahasa, yang kemudian dapat Anda masukkan ke halaman PDF yang sama.

### Bagaimana cara mengontrol DPI atau skala gambar?

Sebelum menambahkan gambar ke PDF, Anda dapat mengubah ukurannya dengan `System.Drawing`:

```csharp
var resized = new Bitmap(inputImage, new Size(1240, 1754)); // A4 at 150 dpi
```

Kemudian berikan `resized` ke konstruktor gambar PDF.

### Apakah teks tersembunyi benar‑benar tak terlihat di semua penampil?

Sebagian besar penampil modern menghormati flag `IsHidden`. Jika Anda menemukan penampil yang masih menampilkan teks kecil, turunkan ukuran font lebih jauh (misalnya, `0.01f`) atau atur warna teks menjadi sepenuhnya transparan menggunakan `TextState.FillColor = Color.Transparent`.

### Bagaimana dengan keamanan—apakah saya dapat melindungi PDF dengan kata sandi?

Ya. Setelah Anda selesai menambahkan konten, panggil:

```csharp
pdfDocument.Encrypt("ownerPwd", "userPwd", EncryptionAlgorithms.AES256);
```

Sekarang PDF yang dapat dicari juga menghormati kebijakan kerahasiaan organisasi Anda.

---

## Tips untuk Implementasi Siap Produksi

- **Batch processing:** Gunakan `Parallel.ForEach` untuk kumpulan gambar besar, tetapi waspadai instance `OcrEngine` yang tidak thread‑safe—buat satu per thread.
- **Error handling:** Bungkus pemanggilan OCR dalam try/catch; periksa `ocrResult.IsRecognized` untuk melewatkan halaman yang gagal.
- **Logging:** Simpan nilai `ocrResult.Confidence`; kepercayaan rendah dapat menunjukkan kebutuhan pra‑pemrosesan gambar (deskew, despeckle).
- **Performance:** Gunakan kembali objek `Document` yang sama untuk semua halaman agar tidak terus‑menerus membuka/menutup file.
- **Testing:** Bandingkan teks yang diekstrak dari PDF yang dapat dicari (`pdfDocument.Pages[1].ExtractText()`) dengan output OCR untuk memastikan tidak ada pemotongan.

---

## Kesimpulan

Kami baru saja menunjukkan cara **membuat PDF yang dapat dicari** dari gambar biasa menggunakan C#. Dengan mengekstrak teks menggunakan Aspose.OCR, menumpuknya secara tak terlihat pada halaman PDF, dan menyimpan hasilnya, Anda mendapatkan dokumen yang tampak persis seperti hasil pindai asli namun berperilaku seperti PDF asli. Teknik ini mencakup alur kerja klasik **convert image to PDF**, menambahkan **pdf dengan teks tersembunyi**, dan menyelesaikan kebutuhan sehari-hari untuk **scan image to PDF** yang sebenarnya dapat dicari.

Siap untuk langkah selanjutnya? Cobalah memperluas kode untuk memproses batch folder kwitansi, atau mengintegrasikannya ke dalam API web yang mengembalikan PDF yang dapat dicari secara langsung. Anda juga dapat bereksperimen dengan font berbeda, menambahkan metadata, atau bahkan menyematkan skor kepercayaan OCR sebagai anotasi PDF untuk jejak audit.

Jika Anda menemukan panduan ini berguna, beri bintang, bagikan kepada rekan tim, atau tinggalkan komentar dengan modifikasi Anda sendiri. Selamat coding, dan semoga PDF Anda selalu dapat dicari!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}