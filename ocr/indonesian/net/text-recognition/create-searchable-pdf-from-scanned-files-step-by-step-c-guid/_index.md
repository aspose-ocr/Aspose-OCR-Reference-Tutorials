---
category: general
date: 2026-03-17
description: Buat PDF yang dapat dicari dengan cepat dengan mengonversi PDF yang dipindai
  menggunakan OCR. Pelajari cara menjalankan OCR, mengekstrak teks dari PDF, dan lainnya.
draft: false
keywords:
- create searchable pdf
- convert scanned pdf
- ocr to searchable pdf
- extract text from pdf
- how to run ocr
language: id
og_description: Buat PDF yang dapat dicari dari dokumen yang dipindai. Panduan ini
  menunjukkan cara mengonversi PDF yang dipindai, menjalankan OCR, dan mengekstrak
  teks menggunakan C#.
og_title: Buat PDF yang Dapat Dicari – Tutorial OCR C# Lengkap
tags:
- OCR
- PDF
- C#
- .NET
title: Buat PDF yang dapat dicari dari file hasil pemindaian – Panduan C# langkah
  demi langkah
url: /id/net/text-recognition/create-searchable-pdf-from-scanned-files-step-by-step-c-guid/
---

final answer.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat PDF yang Dapat Dicari – Tutorial Lengkap C#

Pernahkah Anda perlu **membuat PDF yang dapat dicari** dari tumpukan halaman yang dipindai? Mungkin Anda sedang mendigitalkan kontrak lama, atau Anda hanya ingin PDF Anda dapat dicari di Windows Explorer. Bagaimanapun, Anda mungkin bertanya-tanya bagaimana cara **mengonversi pdf yang dipindai** menjadi sesuatu yang benar‑benar dapat Anda cari.  

Berita baik? Dengan beberapa baris C# dan mesin OCR, Anda dapat mengubah PDF berbasis gambar apa pun menjadi PDF yang sepenuhnya dapat dicari—tanpa layanan eksternal. Dalam tutorial ini kami akan membahas seluruh proses, mulai dari menginstal pustaka hingga mengekstrak teks, dan kami akan menjelaskan “mengapa” di balik setiap langkah sehingga Anda benar‑benar mengerti apa yang terjadi di balik layar.

> **Jawaban cepat:** cukup atur `PdfConversionMode = PdfConversionMode.SearchablePdf`, beri file yang dipindai, panggil `Recognize()`, dan simpan hasilnya.  

Di bawah ini Anda akan menemukan semua yang Anda butuhkan untuk membuatnya berfungsi hari ini.

---

## Apa yang Anda Butuhkan

| Prasyarat | Mengapa penting |
|--------------|----------------|
| .NET 6 or later (or .NET Framework 4.7+) | SDK OCR yang akan kami gunakan menargetkan runtime ini. |
| Visual Studio 2022 (or any C# IDE) | Mempermudah debugging dan manajemen NuGet. |
| A NuGet‑compatible OCR library (e.g., **Aspose.OCR** or **Tesseract.NET**) | Menyediakan kelas `OcrEngine` yang ditampilkan dalam kode. |
| A scanned PDF file to test with | Kami akan mengonversinya menjadi PDF yang dapat dicari. |

Jika Anda sudah memiliki proyek, cukup tambahkan paket OCR melalui Package Manager Console:

```powershell
Install-Package Aspose.OCR
```

*(Ganti `Aspose.OCR` dengan pustaka pilihan Anda; API yang kami tunjukkan cukup umum.)*

## Implementasi Langkah‑per‑Langkah

Di bawah setiap langkah kami menyertakan kode C# tepat yang dapat Anda salin‑tempel, plus penjelasan singkat tentang **mengapa** baris tersebut ada.

### Langkah 1: Inisialisasi Mesin OCR  

Membuat mesin adalah hal pertama yang Anda lakukan karena mesin menyimpan semua konfigurasi dan status untuk proses pengenalan.

```csharp
using Aspose.OCR;          // <-- OCR library namespace
using System.IO;           // needed for file handling

// Step 1: Create an OCR engine instance
var ocrEngine = new OcrEngine();
```

> **Tip pro:** Menggunakan kembali satu instance `OcrEngine` untuk banyak file mengurangi penggunaan memori, terutama saat memproses batch besar.

### Langkah 2: Konfigurasikan Mesin untuk PDF yang Dapat Dicari  

Mesin dapat menghasilkan teks biasa, gambar, atau PDF yang dapat dicari. Mengatur mode yang tepat memberi tahu pustaka untuk menyematkan lapisan teks tak terlihat di belakang gambar halaman asli.

```csharp
// Step 2: Tell the engine to produce a searchable PDF
ocrEngine.Config.PdfConversionMode = PdfConversionMode.SearchablePdf;
```

*Mengapa?* Tanpa flag ini proses OCR hanya akan memberi Anda `string` teks yang dikenali, yang tidak berguna jika Anda masih memerlukan tata letak halaman asli.

### Langkah 3: Muat Dokumen yang Dipindai  

Sebagian besar SDK OCR menerima `Image` atau `ImageStream`. Di sini kami menggunakan pembantu yang membaca file PDF dan memperlakukan setiap halaman sebagai gambar.

```csharp
// Step 3: Load the scanned PDF you want to convert
ocrEngine.Image = ImageStream.FromFile(@"C:\Docs\scanned.pdf");
```

> **Kasus khusus:** Jika PDF Anda berisi halaman raster dan vektor campuran, beberapa mesin mungkin melewatkan halaman vektor. Dalam skenario itu, konversi dulu PDF ke gambar (mis., menggunakan Ghostscript) sebelum memberikannya ke mesin OCR.

### Langkah 4: Jalankan Pengenalan OCR  

Memanggil `Recognize()` melakukan pekerjaan berat—deteksi teks, pemodelan bahasa, dan pembuatan PDF semuanya terjadi di balik layar.

```csharp
// Step 4: Run OCR; the result includes the searchable PDF object
var ocrResult = ocrEngine.Recognize();
```

Jika Anda juga perlu **mengekstrak teks dari pdf**, Anda dapat mengambilnya dari `ocrResult.Text`:

```csharp
string extractedText = ocrResult.Text;   // plain text version
```

### Langkah 5: Simpan PDF yang Dapat Dicari  

Akhirnya, tulis output ke disk. Properti `PdfDocument` menyimpan PDF lengkap dengan lapisan teks tak terlihat.

```csharp
// Step 5: Persist the searchable PDF
ocrResult.PdfDocument.Save(@"C:\Docs\searchable.pdf");
```

Saat Anda membuka `searchable.pdf` di Adobe Reader atau Edge, Anda dapat mengetikkan kata di kotak Find dan langsung melompat ke lokasi yang cocok—seperti PDF asli.

## Memverifikasi Hasil

1. Buka file yang dihasilkan di penampil PDF apa pun.  
2. Tekan **Ctrl + F** dan ketikkan kata yang Anda ketahui muncul di halaman yang dipindai.  
3. Jika penampil menyorot istilah tersebut, Anda telah berhasil **membuat pdf yang dapat dicari**.

Jika tidak ada yang ditemukan, periksa kembali bahwa PDF sumber memang berisi teks yang dapat dibaca (beberapa pemindaian begitu beresolusi rendah sehingga OCR tidak dapat mengenali apa pun). Meningkatkan DPI sebelum OCR (mis., `ocrEngine.Config.Dpi = 300`) sering membantu.

## Kesalahan Umum & Cara Memperbaikinya

| Gejala | Penyebab kemungkinan | Perbaikan |
|---------|--------------|-----|
| PDF dapat dicari kosong | `PdfConversionMode` dibiarkan pada default (hanya gambar) | Atur `PdfConversionMode = PdfConversionMode.SearchablePdf`. |
| Karakter kacau | Model bahasa salah | `ocrEngine.Config.Language = Language.English;` (atau bahasa yang sesuai). |
| Pemrosesan lambat pada file besar | Mesin diinisialisasi ulang per halaman | Gunakan kembali instance `OcrEngine` yang sama, atau aktifkan multi‑threading jika pustaka mendukungnya. |
| Tidak ada teks yang dapat dicari setelah konversi | PDF input hanya vektor (tidak ada gambar raster) | Render halaman PDF ke gambar terlebih dahulu (mis., `PdfRenderer` dari Aspose.PDF). |

## Bonus: Ekstrak Teks Langsung dari PDF yang Dapat Dicari  

Terkadang Anda memerlukan teks mentah untuk pengindeksan atau analitik. Karena `ocrResult` sudah memberikan Anda `Text`, Anda dapat melewatkan membuka PDF lagi. Namun, jika Anda hanya memiliki file PDF nanti, gunakan ekstraktor teks PDF:

```csharp
using Aspose.Pdf;   // PDF library for reading

var pdfDoc = new Document(@"C:\Docs\searchable.pdf");
var textAbsorber = new TextAbsorber();
pdfDoc.Pages.Accept(textAbsorber);
string fullText = textAbsorber.Text;
```

Sekarang Anda memiliki **mengekstrak teks dari pdf** tanpa menjalankan OCR lagi—jalan pintas yang berguna saat memproses banyak file.

## Contoh Kerja Lengkap (Semua Langkah dalam Satu File)

```csharp
// ------------------------------------------------------------
// Full C# example: Convert a scanned PDF into a searchable PDF
// ------------------------------------------------------------
using System;
using Aspose.OCR;
using Aspose.Pdf;               // For optional text extraction
using Aspose.Pdf.Text;          // TextAbsorber class

namespace SearchablePdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize OCR engine
            var ocrEngine = new OcrEngine();

            // 2️⃣ Configure for searchable PDF output
            ocrEngine.Config.PdfConversionMode = PdfConversionMode.SearchablePdf;
            // Optional: set language and DPI for better accuracy
            ocrEngine.Config.Language = Language.English;
            ocrEngine.Config.Dpi = 300;

            // 3️⃣ Load the scanned document (replace path as needed)
            string inputPath = @"C:\Docs\scanned.pdf";
            ocrEngine.Image = ImageStream.FromFile(inputPath);

            // 4️⃣ Run OCR – this creates both PDF and plain‑text results
            var ocrResult = ocrEngine.Recognize();

            // 5️⃣ Save the searchable PDF
            string outputPath = @"C:\Docs\searchable.pdf";
            ocrResult.PdfDocument.Save(outputPath);
            Console.WriteLine($"Searchable PDF saved to: {outputPath}");

            // 🎉 Bonus: Extract plain text without opening the PDF again
            string extractedText = ocrResult.Text;
            Console.WriteLine("\n--- Extracted Text Preview ---");
            Console.WriteLine(extractedText.Substring(0,
                Math.Min(300, extractedText.Length)) + "...");

            // Optional: Verify by re‑reading the PDF
            var pdfDoc = new Document(outputPath);
            var absorber = new TextAbsorber();
            pdfDoc.Pages.Accept(absorber);
            Console.WriteLine("\nText extracted from saved PDF:");
            Console.WriteLine(absorber.Text.Substring(0,
                Math.Min(300, absorber.Text.Length)) + "...");
        }
    }
}
```

**Output yang diharapkan** (dipotong untuk singkat):

```
Searchable PDF saved to: C:\Docs\searchable.pdf

--- Extracted Text Preview ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit...

Text extracted from saved PDF:
Lorem ipsum dolor sit amet, consectetur adipiscing elit...
```

Jika Anda melihat potongan yang sama dua kali, OCR berhasil dan PDF kini berisi lapisan teks yang dapat dicari.

## Langkah Selanjutnya & Topik Terkait

- **Pemrosesan batch:** Loop melalui folder PDF yang dipindai, menggunakan kembali instance `OcrEngine` yang sama untuk meningkatkan throughput.  
- **Deteksi bahasa:** Untuk arsip multibahasa, ubah `ocrEngine.Config.Language` secara dinamis berdasarkan metadata file.  
- **Kepatuhan PDF/A:** Beberapa industri memerlukan PDF arsip; atur `PdfConversionMode = PdfConversionMode.SearchablePdfA` jika SDK Anda mendukungnya.  
- **Pengoptimalan kinerja:** Bereksperimen dengan `ocrEngine.Config.UseParallelProcessing = true` (jika tersedia) untuk mempercepat pekerjaan besar.  

Semua ini dibangun di atas konsep inti **cara menjalankan OCR** secara efisien sambil **membuat pdf yang dapat dicari** yang dapat diindeks secara langsung.

## Kesimpulan

Anda kini memiliki resep lengkap dan siap produksi untuk mengubah dokumen yang dipindai menjadi karya **membuat pdf yang dapat dicari**. Dengan mengonfigurasi mesin OCR, memuat sumber, menjalankan pengenalan, dan menyimpan hasil, Anda telah mencakup seluruh alur—dari gambar mentah hingga PDF yang dapat dicari dan dapat diekstrak teksnya.  

Berikan coba dengan file Anda sendiri, sesuaikan pengaturan DPI atau bahasa, dan Anda akan

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}