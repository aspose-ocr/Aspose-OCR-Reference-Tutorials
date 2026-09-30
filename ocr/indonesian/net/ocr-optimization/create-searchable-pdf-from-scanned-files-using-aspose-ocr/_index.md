---
category: general
date: 2026-01-04
description: Buat PDF yang dapat dicari dari PDF yang dipindai dengan cepat. Pelajari
  cara mengonversi PDF yang dipindai, menambahkan OCR ke PDF, dan menyesuaikan kualitas
  gambar dengan Aspose OCR di C#.
draft: false
keywords:
- create searchable pdf
- convert scanned pdf
- add ocr to pdf
- adjust image quality
- how to use ocr
language: id
og_description: Buat PDF yang dapat dicari dari PDF yang dipindai dengan cepat. Ikuti
  panduan langkah demi langkah ini untuk mengonversi PDF yang dipindai, menambahkan
  OCR ke PDF, dan menyesuaikan kualitas gambar.
og_title: Buat PDF yang Dapat Dicari dari File Pindai Menggunakan Aspose OCR
tags:
- Aspose OCR
- C#
- PDF processing
title: Buat PDF yang Dapat Dicari dari File yang Dipindai Menggunakan Aspose OCR
url: /id/net/ocr-optimization/create-searchable-pdf-from-scanned-files-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Membuat PDF yang Dapat Dicari dari File yang Dipindai Menggunakan Aspose OCR

Pernah perlu **membuat PDF yang dapat dicari** dari tumpukan dokumen yang dipindai tetapi tidak yakin harus mulai dari mana? Anda tidak sendirian—banyak pengembang menemui hambatan ini saat membangun pipeline manajemen dokumen. Kabar baiknya? Dengan Aspose OCR Anda dapat **mengonversi PDF yang dipindai**, menambahkan OCR, dan menyesuaikan kualitas gambar hanya dengan beberapa baris C#.

Dalam tutorial ini kita akan membahas seluruh proses, mulai dari memuat PDF yang dipindai hingga menyimpan versi yang sepenuhnya dapat dicari. Pada akhir tutorial Anda akan tahu persis **cara menggunakan OCR** dengan Aspose, mengapa setiap pengaturan penting, dan apa yang harus disesuaikan ketika sesuatu tidak berjalan sesuai rencana. Tanpa referensi yang samar—hanya contoh lengkap yang dapat dijalankan dan langsung Anda masukkan ke dalam proyek hari ini.

## Prasyarat

Sebelum kita mulai, pastikan Anda memiliki:

- .NET 6.0 atau yang lebih baru (kode ini juga bekerja dengan .NET Core dan .NET Framework)
- Lisensi Aspose OCR yang valid (versi trial gratis cukup untuk pengujian)
- File PDF input bernama `input.pdf` yang ditempatkan di folder yang Anda kontrol
- Visual Studio 2022 atau editor C# pilihan Anda

Itu saja. Jika ada yang belum familiar, berhentilah sejenak dan instal komponen yang belum ada—tidak ada hal lain yang diperlukan.

## Langkah 1: Inisialisasi OCR Engine dan Muat PDF yang Dipindai  
**(Di sinilah kita **menambahkan OCR ke PDF** untuk pertama kalinya.)**

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// Create the OCR engine instance
OcrEngine ocrEngine = new OcrEngine();

// Load the scanned PDF from disk
ocrEngine.LoadPdf(@"C:\Docs\input.pdf");
```

*Mengapa langkah ini?*  
`OcrEngine` adalah inti dari Aspose OCR. Memuat PDF memberi tahu engine di mana mencari gambar raster yang akan dianalisis nanti. Jika Anda melewatkannya, tidak ada yang dapat dikonversi, dan langkah‑langkah berikutnya akan menghasilkan exception.

> **Tip pro:** Jika PDF Anda dilindungi password, gunakan `ocrEngine.LoadPdf(path, password)` untuk menghindari error runtime.

## Langkah 2: Atur Bahasa Utama dan Bahasa Tambahan  
**(Kita akan **mengonversi PDF yang dipindai** dalam bahasa Inggris, Prancis, dan Jerman.)**

```csharp
// Primary language – the most common language in the document
ocrEngine.Config.Language = Language.English;

// Add extra languages if the document contains multilingual text
ocrEngine.Config.AdditionalLanguages = new[] { Language.French, Language.German };
```

*Mengapa bahasa penting?*  
Akurasi OCR bergantung pada set karakter yang diharapkan. Dengan mendeklarasikan bahasa Inggris sebagai bahasa utama dan menambahkan Prancis/Jerman, engine dapat menafsirkan karakter aksen dan glyph khusus dengan benar. Lupa mengatur ini biasanya menghasilkan teks yang berantakan.

## Langkah 3: Sesuaikan Kualitas Gambar – Fine‑tune Output PDF  
**(Di sini kita **menyesuaikan kualitas gambar** untuk menyeimbangkan ukuran file dan keterbacaan.)**

```csharp
PdfSaveOptions pdfOptions = new PdfSaveOptions
{
    ImageQuality = 90,          // JPEG quality for embedded images (0‑100)
    Compress = true,            // Enable PDF compression to shrink file size
    PreserveOriginalLayout = true // Keep the scanned layout intact
};
```

*Mengapa mengubah `ImageQuality`?*  
Nilai yang lebih tinggi (90‑100) mempertahankan ketajaman, yang krusial untuk akurasi OCR, tetapi juga memperbesar ukuran file. Jika Anda mengarsipkan jutaan halaman, turunkan menjadi 70‑80 untuk PDF yang lebih ringan tanpa mengorbankan terlalu banyak keterbacaan.

## Langkah 4: Simpan Hasil sebagai PDF yang Dapat Dicari  
**(Sekarang kita akhirnya **membuat PDF yang dapat dicari** yang dapat Anda indeks.)**

```csharp
// Export the OCR result as a searchable PDF
ocrEngine.SaveAsSearchablePdf(@"C:\Docs\output.pdf", pdfOptions);

// Let the user know we’re done
Console.WriteLine("Searchable PDF created at C:\\Docs\\output.pdf");
```

*Apa yang sebenarnya terjadi?*  
Aspose OCR mengekstrak lapisan teks dari setiap halaman dan menyematkannya di belakang gambar asli. PDF tetap tampak sama, tetapi kini Anda dapat memilih, menyalin, dan mencari teks—keuntungan besar untuk alur kerja selanjutnya.

## Langkah 5: Verifikasi Output (Opsional tetapi Disarankan)  
Mudah menganggap semuanya berhasil, tetapi pemeriksaan singkat dapat menghindarkan Anda dari masalah di kemudian hari.

```csharp
using System.Diagnostics;

// Open the generated PDF automatically (Windows only)
Process.Start(new ProcessStartInfo
{
    FileName = @"C:\Docs\output.pdf",
    UseShellExecute = true
});
```

Buka file, coba pilih sebuah kata, atau tekan `Ctrl+F` dan ketik frasa yang Anda tahu ada di pemindaian asli. Jika teks dapat dipilih, Anda telah berhasil **membuat PDF yang dapat dicari**.

## Kasus Edge Umum & Cara Menanganinya  

| Situasi | Mengapa Terjadi | Solusi Cepat |
|-----------|----------------|-----------|
| **Halaman dengan resolusi campuran** (beberapa 150 dpi, lainnya 300 dpi) | Kualitas OCR bervariasi per halaman, menghasilkan kemampuan pencarian yang tidak merata. | Set `ocrEngine.Config.Dpi = 300;` sebelum memuat untuk memaksa up‑sampling, atau pra‑proses dengan `ImageProcessor` untuk menormalkan DPI. |
| **PDF terenkripsi** | Aspose OCR tidak dapat membaca tanpa password. | Kirim password ke `LoadPdf` seperti pada contoh sebelumnya. |
| **PDF besar (>500 MB)** | Konsumsi memori melonjak, menyebabkan `OutOfMemoryException`. | Proses dokumen secara bertahap: `ocrEngine.SplitPdfIntoPages();` lalu OCR tiap halaman secara terpisah dan gabungkan hasilnya. |
| **Karakter non‑Latin** (misalnya Cyrillic) | Bahasa tidak ditambahkan, sehingga karakter menjadi “?” | Tambahkan `Language.Russian` (atau bahasa lain yang diperlukan) ke `AdditionalLanguages`. |
| **Kualitas gambar terlalu rendah** | Teks menjadi buram, OCR gagal. | Tingkatkan `ImageQuality` atau gunakan `pdfOptions.Dpi = 300;` untuk menyematkan gambar beresolusi lebih tinggi. |

## Contoh Lengkap yang Siap Dijalanin  

Berikut adalah program lengkap yang dapat Anda salin‑tempel ke aplikasi console baru. Termasuk semua langkah, penanganan error, dan komentar untuk kejelasan.

```csharp
using System;
using System.Diagnostics;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace SearchablePdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Paths – adjust to your environment
            string inputPath = @"C:\Docs\input.pdf";
            string outputPath = @"C:\Docs\output.pdf";

            try
            {
                // 1️⃣ Initialize OCR engine and load scanned PDF
                OcrEngine ocrEngine = new OcrEngine();
                ocrEngine.LoadPdf(inputPath);

                // 2️⃣ Configure languages (primary + additional)
                ocrEngine.Config.Language = Language.English;
                ocrEngine.Config.AdditionalLanguages = new[] { Language.French, Language.German };

                // 3️⃣ Set PDF save options – adjust image quality as needed
                PdfSaveOptions pdfOptions = new PdfSaveOptions
                {
                    ImageQuality = 90,
                    Compress = true,
                    PreserveOriginalLayout = true
                };

                // 4️⃣ Save as searchable PDF
                ocrEngine.SaveAsSearchablePdf(outputPath, pdfOptions);
                Console.WriteLine($"✅ Searchable PDF created at {outputPath}");

                // 5️⃣ Optional: open the file to verify
                Process.Start(new ProcessStartInfo
                {
                    FileName = outputPath,
                    UseShellExecute = true
                });
            }
            catch (Exception ex)
            {
                // Friendly error message – helps during debugging
                Console.WriteLine($"❌ Oops! Something went wrong: {ex.Message}");
                // For real‑world apps, consider logging the stack trace
            }
        }
    }
}
```

**Output yang diharapkan:**  
```
✅ Searchable PDF created at C:\Docs\output.pdf
```

Saat Anda membuka `output.pdf`, Anda harus dapat memilih dan mencari teks apa pun yang ada di pemindaian asli.

---

## Pertanyaan yang Sering Diajukan (FAQ)

**T: Apakah ini bekerja dengan PDF yang berisi gambar hasil scan dan teks asli?**  
J: Tentu saja. Aspose OCR hanya menambahkan lapisan teks tersembunyi bila diperlukan, meninggalkan teks yang sudah ada tidak berubah.

**T: Bisakah saya memproses batch folder PDF?**  
J: Ya. Bungkus kode di atas dalam loop `foreach (var file in Directory.GetFiles(folder, "*.pdf"))` dan sesuaikan jalur outputnya.

**T: Bagaimana cara mengurangi ukuran akhir PDF lebih jauh?**  
J: Turunkan `ImageQuality` ke 70‑80, aktifkan `Compress`, atau gunakan `pdfOptions.Dpi = 150` untuk menurunkan resolusi gambar sebelum disematkan.

**T: Apakah ada cara mengekstrak teks OCR tanpa membuat PDF?**  
J: Panggil `ocrEngine.ExtractText();` setelah memuat PDF. Metode ini mengembalikan string teks biasa yang dapat Anda simpan atau indeks.

---

## Penutup  

Kami baru saja membahas **cara menggunakan OCR** dengan Aspose untuk **membuat PDF yang dapat dicari** dari dokumen yang dipindai, menunjukkan **cara mengonversi PDF yang dipindai**, mendemonstrasikan **menambahkan OCR ke PDF**, dan menjelaskan **cara menyesuaikan kualitas gambar** untuk hasil optimal. Contoh kode lengkap siap dijalankan, dan tabel pemecahan masalah akan membantu Anda tetap bergerak ketika hal tak terduga muncul.

Apa selanjutnya? Cobalah bereksperimen dengan:

- Paket bahasa berbeda untuk arsip multibahasa
- Pra‑pemrosesan gambar khusus (deskew, despeckle) via `ImageProcessor`
- Mengintegrasikan PDF yang dapat dicari ke pipeline SharePoint atau ElasticSearch

Jangan ragu meninggalkan komentar jika Anda menemukan kendala atau menemukan trik cerdas. Selamat coding, dan nikmati PDF yang langsung dapat dicari!

![Diagram alur membuat PDF yang dapat dicari menunjukkan OCR engine → konfigurasi bahasa → opsi penyimpanan PDF → output PDF yang dapat dicari](create-searchable-pdf-flow.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}