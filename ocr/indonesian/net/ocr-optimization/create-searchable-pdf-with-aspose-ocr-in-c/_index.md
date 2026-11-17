---
category: general
date: 2026-04-01
description: Buat PDF yang dapat dicari dalam C# menggunakan Aspose OCR – pelajari
  cara mengonversi PDF yang dipindai, menambahkan OCR ke PDF, dan mengaktifkan akselerasi
  GPU untuk hasil yang cepat.
draft: false
keywords:
- create searchable pdf
- convert scanned pdf
- convert pdf to searchable
- add OCR to pdf
- enable GPU acceleration
language: id
og_description: Buat PDF yang dapat dicari dalam C# dengan cepat—konversi PDF yang
  dipindai, tambahkan OCR ke PDF, dan aktifkan percepatan GPU untuk pemrosesan berperforma
  tinggi.
og_title: Buat PDF yang Dapat Dicari dengan Aspose OCR di C#
tags:
- Aspose OCR
- C#
- PDF processing
title: Buat PDF yang Dapat Dicari dengan Aspose OCR di C#
url: /id/net/ocr-optimization/create-searchable-pdf-with-aspose-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Membuat PDF yang Dapat Dicari dengan Aspose OCR di C#

Pernah perlu **membuat file PDF yang dapat dicari** dari tumpukan dokumen yang dipindai? Anda bukan satu‑satunya—banyak tim berjuang mengubah PDF yang hanya berisi gambar menjadi aset yang dapat dicari teksnya. Kabar baik? Dengan Aspose OCR Anda dapat **mengonversi PDF yang dipindai** menjadi versi yang sepenuhnya dapat dicari hanya dengan beberapa baris kode C#. Dalam panduan ini kami akan menelusuri seluruh proses, mulai dari menambahkan OCR ke PDF hingga secara opsional **mengaktifkan percepatan GPU** untuk meningkatkan kecepatan.

Kami juga akan menunjukkan cara **mengonversi pdf ke format yang dapat dicari**, membahas mengapa Anda mungkin ingin **menambahkan OCR ke PDF**, dan memberikan tip praktis untuk menangani batch besar. Pada akhir tutorial Anda akan memiliki aplikasi console siap‑jalankan yang menghasilkan PDF yang dapat dicari dan dapat langsung dimasukkan ke sistem manajemen dokumen apa pun.

---

## Apa yang Anda Butuhkan

Sebelum kita mulai, pastikan Anda memiliki hal‑hal berikut:

- **.NET 6.0** atau yang lebih baru (API juga bekerja dengan .NET Framework, tetapi .NET 6+ adalah pilihan terbaik).
- Paket NuGet **Aspose.OCR for .NET** (`Install-Package Aspose.OCR`).
- File PDF yang dipindai (hanya gambar) untuk dijadikan input.
- Opsional: mesin yang kompatibel dengan GPU dan memiliki CUDA® terpasang jika Anda ingin **mengaktifkan percepatan GPU**.

Itu saja—tanpa mesin OCR berat, tanpa layanan eksternal. Semua berjalan secara lokal.

---

## Membuat PDF yang Dapat Dicari – Ikhtisar Langkah‑per‑Langkah

Berikut alur tingkat tinggi yang akan kita ikuti:

1. **Inisialisasi mesin OCR** – beri tahu Aspose bahasa yang akan dicari dan apakah akan menggunakan GPU.
2. **Arahkan mesin ke PDF yang dipindai** – tentukan jalur input dan output.
3. **Jalankan konversi** – Aspose melakukan pekerjaan berat dan menulis PDF yang dapat dicari.
4. **Verifikasi hasil** – buka file output dan coba lakukan pencarian teks.

Setiap langkah dijelaskan di bagian masing‑masing, sehingga Anda dapat memilih bagian yang paling relevan.

---

## Mengonversi PDF yang Dipindai ke PDF yang Dapat Dicari

Hal pertama yang harus Anda lakukan adalah membuat instance `OcrEngine`. Objek ini adalah tenaga kerja yang membaca gambar raster di dalam PDF Anda dan mengekstrak teks.

```csharp
using Aspose.OCR;
using System;

class PdfSearchableDemo
{
    static void Main()
    {
        // Step 1: Create and configure the OCR engine
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = Language.English,
            // Optional: enable GPU for faster processing
            UseGpuAcceleration = true
        };

        // Step 2: Specify the input scanned PDF and the output searchable PDF paths
        string sourcePdfPath = @"C:\Docs\input.pdf";
        string searchablePdfPath = @"C:\Docs\output.pdf";

        // Step 3: Convert the scanned PDF into a searchable PDF
        ocrEngine.ConvertToSearchablePdf(sourcePdfPath, searchablePdfPath);

        // Step 4: Notify the user where the searchable PDF was saved
        Console.WriteLine("Searchable PDF created at: " + searchablePdfPath);
    }
}
```

**Mengapa ini berhasil:** `ConvertToSearchablePdf` membaca tiap halaman, menjalankan OCR pada konten raster, lalu menyisipkan lapisan teks tak terlihat di belakang gambar asli. Hasilnya tampak persis seperti dokumen yang dipindai, tetapi kini Anda dapat menyalin, memilih, dan mencari teksnya.

---

## Menambahkan OCR ke PDF Menggunakan Aspose

Jika Anda sudah memiliki PDF dan hanya ingin **menambahkan OCR ke PDF** tanpa mengonversi seluruh file, Anda dapat memanggil metode yang sama—Aspose memperlakukan operasi ini sebagai “menambahkan OCR”. Kode di atas sudah melakukannya, tetapi berikut varian singkat yang menunjukkan cara memproses banyak file dalam sebuah loop:

```csharp
string[] pdfFiles = Directory.GetFiles(@"C:\Docs\Scanned", "*.pdf");
foreach (var file in pdfFiles)
{
    string output = Path.Combine(@"C:\Docs\Searchable", Path.GetFileNameWithoutExtension(file) + "_searchable.pdf");
    ocrEngine.ConvertToSearchablePdf(file, output);
    Console.WriteLine($"Processed {Path.GetFileName(file)} → {Path.GetFileName(output)}");
}
```

**Tip:** Gunakan instance `OcrEngine` yang sama untuk seluruh batch. Membuat ulang setiap kali menambah overhead yang tidak perlu, terutama ketika Anda **mengaktifkan percepatan GPU**.

---

## Mengaktifkan Percepatan GPU untuk OCR Lebih Cepat

Percepatan GPU dapat mengurangi waktu pemrosesan batch besar beberapa menit. Aspose OCR memanfaatkan NVIDIA CUDA di balik layar, jadi Anda hanya perlu mengubah sebuah flag boolean:

```csharp
ocrEngine.UseGpuAcceleration = true; // set to false if no compatible GPU
```

**Kapan menggunakannya:** Jika Anda memproses PDF berukuran lebih dari 10 MB atau menangani lebih dari beberapa lusin file, GPU biasanya memberikan peningkatan kecepatan 2‑3×. Pada laptop standar tanpa GPU yang mendukung CUDA, biarkan `false`—perpustakaan akan otomatis beralih ke CPU.

**Kesalahan umum:** Lupa menginstal versi driver CUDA yang tepat dapat menyebabkan pengecualian runtime (`CudaException`). Pastikan driver Anda cocok dengan versi yang diharapkan Aspose (cek catatan rilis di halaman NuGet).

---

## Contoh Lengkap yang Berfungsi (Semua Langkah Digabung)

Berikut adalah aplikasi console yang berdiri sendiri yang dapat Anda salin‑tempel ke proyek .NET baru. Ia mencakup komentar berguna, penanganan error, dan langkah verifikasi akhir yang mencetak jumlah halaman yang diproses.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class PdfSearchableDemo
{
    static void Main()
    {
        try
        {
            // 1️⃣ Initialize OCR engine – English language, GPU on if available
            OcrEngine ocrEngine = new OcrEngine
            {
                Language = Language.English,
                UseGpuAcceleration = true // set to false on non‑GPU machines
            };

            // 2️⃣ Define input and output paths
            string sourcePdfPath = @"C:\Docs\input.pdf";
            string searchablePdfPath = @"C:\Docs\output.pdf";

            // 3️⃣ Perform the conversion – this creates a searchable PDF
            ocrEngine.ConvertToSearchablePdf(sourcePdfPath, searchablePdfPath);

            // 4️⃣ Simple verification – count pages in the new file
            int pageCount = new Aspose.Pdf.Facades.PdfFileInfo(searchablePdfPath).NumberOfPages;
            Console.WriteLine($"✅ Searchable PDF created at: {searchablePdfPath}");
            Console.WriteLine($"📄 The new file contains {pageCount} pages.");

            // 5️⃣ Optional: open the file automatically (Windows only)
            // System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo(searchablePdfPath) { UseShellExecute = true });
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"❌ Oops! Something went wrong: {ex.Message}");
        }
    }
}
```

**Output yang diharapkan**

```
✅ Searchable PDF created at: C:\Docs\output.pdf
📄 The new file contains 12 pages.
```

Buka `output.pdf` di penampil PDF apa pun dan coba ketikkan kata yang muncul di gambar yang dipindai. Jika teksnya disorot, Anda telah berhasil **create searchable pdf**.

---

## Kesalahan Umum dan Pro Tip

| Masalah | Mengapa Terjadi | Cara Memperbaiki / Menghindari |
|---------|-----------------|--------------------------------|
| **GPU tidak terdeteksi** | Driver CUDA hilang atau tidak cocok. | Instal versi driver yang tercantum di catatan rilis Aspose; set `UseGpuAcceleration = false` sebagai cadangan. |
| **Bahasa salah** | OCR default ke Bahasa Inggris; bahasa lain memerlukan pengaturan eksplisit. | Set `Language = Language.Spanish` (atau enum lain yang didukung) sebelum konversi. |
| **PDF besar menyebabkan OutOfMemory** | Mesin memuat seluruh halaman ke memori. | Proses PDF dalam potongan menggunakan `ocrEngine.PageRange = new PageRange(1, 5)` untuk tiap batch. |
| **File output rusak** | Folder tujuan tidak memiliki izin menulis. | Jalankan aplikasi dengan hak istimewa atau pilih jalur yang dapat ditulis. |
| **Lapisan teks tidak dapat dicari** | Penampil menyimpan versi lama dalam cache. | Segarkan penampil PDF atau buka kembali file tersebut. |

**Pro tip:** Saat Anda menangani campuran PDF yang dipindai dan PDF asli, periksa flag `HasText` tiap halaman (`PdfPageInfo.HasText`) sebelum menjalankan OCR. Itu menghemat siklus CPU dan menghindari OCR ganda pada halaman yang sudah dapat dicari.

---

## Memverifikasi Hasil Secara Programatis (Opsional)

Jika Anda ingin mengotomatiskan verifikasi, Aspose.PDF dapat mengekstrak teks tersembunyi:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Load the searchable PDF
Document doc = new Document(searchablePdfPath);
TextAbsorber absorber = new TextAbsorber();
doc.Pages.Accept(absorber);
string extracted = absorber.Text;

// Simple check – does the word "Invoice" appear?
if (extracted.Contains("Invoice"))
    Console.WriteLine("✅ OCR succeeded – 'Invoice' found.");
else
    Console.WriteLine("⚠️ OCR may have missed some text.");
```

Potongan kode ini membuktikan bahwa Anda benar‑benar **convert pdf to searchable** format, bukan sekadar menumpuk gambar.

---

## Contoh Gambar

![Create searchable PDF output example](https://example.com/images/searchable-pdf.png "Create searchable PDF using Aspose OCR")

*Alt text:* **create searchable pdf** contoh yang menampilkan tampilan sebelum (dipindai) dan sesudah (dapat dicari).

---

## Langkah Selanjutnya & Topik Terkait

- **Pemrosesan batch:** Bungkus loop dari bagian “Add OCR to PDF” ke dalam Windows Service atau Azure Function untuk pekerjaan semalam.
- **Dukungan bahasa lanjutan:** Jelajahi `ocrEngine.Language = Language.Multilingual` untuk dokumen yang berisi skrip campuran.
- **Pembersihan pasca‑OCR:** Gunakan `TextFragmentAbsorber` dari Aspose.PDF untuk memperbaiki kesalahan OCR umum (misalnya “0” vs “O”).
- **Keamanan

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}