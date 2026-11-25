---
category: general
date: 2026-05-31
description: Ekstrak tabel dari gambar menggunakan Aspose OCR dalam C#. Pelajari cara
  mengonversi gambar menjadi tabel, mengaktifkan deteksi tabel, dan menghasilkan hasil
  secara efisien.
draft: false
keywords:
- extract tables from image
- convert image to table
- OCR table extraction
- Aspose OCR C#
- image to spreadsheet conversion
- table detection in OCR
language: id
og_description: Ekstrak tabel dari gambar dengan Aspose OCR. Panduan ini menunjukkan
  cara mengonversi gambar menjadi tabel, mengaktifkan deteksi tabel, dan menangani
  hasilnya di C#.
og_title: Ekstrak Tabel dari Gambar – Tutorial C# Langkah demi Langkah
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Extract tables from image using Aspose OCR in C#. Learn how to convert
    image to table, enable table detection, and output results efficiently.
  headline: Extract Tables from Image with Aspose OCR – Complete C# Guide
  type: TechArticle
- description: Extract tables from image using Aspose OCR in C#. Learn how to convert
    image to table, enable table detection, and output results efficiently.
  name: Extract Tables from Image with Aspose OCR – Complete C# Guide
  steps:
  - name: Expected Output
    text: 'Assuming the source image contains a 3 × 4 table of invoice line items,
      you might see something like:'
  - name: Low‑Resolution Images
    text: 'When your source picture is under 150 dpi, the table detection algorithm
      may miss cell boundaries. A quick fix is to upscale the image using `System.Drawing`
      before feeding it to Aspose:'
  - name: Skewed Tables
    text: 'If the table is rotated even a few degrees, enable auto‑deskew:'
  - name: Multiple Tables on One Page
    text: Aspose OCR returns each table as a separate object in `result.Tables`. You
      can treat them individually, or merge them into a single DataTable if you need
      a unified view.
  - name: Exporting to Excel
    text: 'Once you have a `DataTable`, exporting to an `.xlsx` file is a breeze with
      `ClosedXML`:'
  type: HowTo
- questions:
  - answer: Yes. Convert each PDF page to an image first (`PdfRenderer` or `Ghostscript`),
      then feed the bitmap to Aspose OCR.
    question: Does this work with PDFs?
  - answer: Absolutely. The `ImageStream.FromFile` method accepts JPEG, PNG, BMP,
      and TIFF out of the box.
    question: Can I extract tables from a JPG?
  - answer: Aspose OCR treats merged cells as separate logical cells; you may need
      to post‑process the output to combine them based on confidence or content patterns.
    question: What if my table has merged cells?
  - answer: Practically, the engine handles tables up to several hundred rows. Performance
      degrades linearly, so consider chunking very large scans.
    question: Is there a limit on table size?
  type: FAQPage
tags:
- OCR
- C#
- Aspose
- Data Extraction
title: Ekstrak Tabel dari Gambar dengan Aspose OCR – Panduan Lengkap C#
url: /id/net/image-and-drawing-recognition/extract-tables-from-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ekstrak Tabel dari Gambar – Panduan Lengkap C#

Pernah perlu **mengekstrak tabel dari gambar** tetapi tidak tahu harus mulai dari mana? Anda tidak sendirian; banyak pengembang mengalami hal ini saat mencoba mengubah faktur atau kwitansi yang dipindai menjadi data yang dapat dipakai. Kabar baiknya? Dengan Aspose OCR Anda dapat **mengonversi gambar menjadi tabel** hanya dengan beberapa baris kode C#.

Dalam tutorial ini kita akan membahas contoh dunia nyata: memuat PNG yang berisi tabel, mengubah tata letak visual menjadi grid terstruktur, dan mencetak konten setiap sel beserta skor kepercayaan. Pada akhir tutorial Anda akan memiliki potongan kode yang siap pakai untuk proyek .NET apa pun, plus tips untuk menangani kasus tepi dan menskalakan solusi.

## Apa yang Anda Butuhkan

Sebelum kita mulai, pastikan Anda memiliki:

- **.NET 6.0** atau lebih baru (kode ini juga bekerja dengan .NET Framework 4.6+)
- Paket NuGet **Aspose.OCR** (`Install-Package Aspose.OCR`)
- File gambar yang memang berisi tabel (misalnya `invoice_with_table.png`)
- IDE C# dasar (Visual Studio, Rider, atau VS Code dengan ekstensi C#)

Itu saja—tanpa mesin OCR tambahan, tanpa dependensi berat. Siap? Mari kita mulai.

## Langkah 1: Inisialisasi OCR Engine untuk **Ekstrak Tabel dari Gambar**

Pertama, kita buat instance `OcrEngine` dan arahkan ke gambar sumber kita. Anggap engine sebagai otak yang akan membaca setiap piksel dan mencoba memahami tata letaknya.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// Initialize the OCR engine with the input image
OcrEngine engine = new OcrEngine
{
    // ImageStream.FromFile loads the image from disk
    Image = ImageStream.FromFile(@"YOUR_DIRECTORY/invoice_with_table.png")
};
```

> **Mengapa ini penting:** Tanpa menginisialisasi engine dengan benar, OCR engine tidak memiliki apa‑apa untuk dianalisis, dan Anda tidak akan mendapatkan tabel apa pun dari gambar. Pemanggilan `ImageStream.FromFile` juga menangani masalah format umum (PNG, JPEG, BMP) sehingga Anda tidak memerlukan langkah konversi tambahan.

## Langkah 2: Aktifkan Deteksi Tabel – Kunci untuk **Mengonversi Gambar menjadi Tabel**

Aspose OCR dapat membaca teks biasa dari gambar, tetapi tidak akan secara otomatis memahami baris dan kolom kecuali Anda memberi tahu untuk mencari tabel. Di sinilah flag `DetectTables` berperan.

```csharp
// Turn on table detection in the OCR options
engine.Options = new OcrOptions
{
    DetectTables = true   // This activates the table extraction algorithm
};
```

> **Tip pro:** Jika Anda hanya membutuhkan teks mentah, biarkan `DetectTables` tetap `false`. Mengaktifkannya menambah sedikit overhead, tetapi hasilnya adalah data terstruktur bersih yang dapat langsung dimasukkan ke spreadsheet atau basis data.

## Langkah 3: Lakukan OCR Recognition – Saatnya Menguji

Sekarang kita meminta engine untuk benar‑benar membaca gambar. Metode `Recognize` mengembalikan objek `OcrResult` yang berisi teks biasa serta tabel yang terdeteksi.

```csharp
// Execute the OCR process
OcrResult result = engine.Recognize();
```

> **Apa yang terjadi di balik layar?** Aspose menjalankan serangkaian langkah pra‑pemrosesan gambar (deskewing, binarisasi) sebelum menerapkan pengenalan teks berbasis jaringan saraf. Ketika `DetectTables` bernilai true, ia juga menjalankan analisis tata letak yang mengelompokkan karakter ke dalam baris dan kolom.

## Langkah 4: Iterasi Melalui Tabel yang Terdeteksi – **Ekstrak Tabel dari Gambar** dalam Aksi

Jika engine menemukan tabel, mereka akan muncul di `result.Tables`. Kita akan melintasi setiap tabel, lalu setiap baris dan kolom, mencetak teks sel serta persentase kepercayaan.

```csharp
// Loop over every detected table
foreach (var table in result.Tables)
{
    Console.WriteLine("Table found:");
    for (int r = 0; r < table.Rows; r++)
    {
        for (int c = 0; c < table.Columns; c++)
        {
            var cell = table[r, c];
            // Show cell text and its confidence level
            Console.Write($"{cell.Text} (conf:{cell.Confidence}%)\t");
        }
        Console.WriteLine(); // New line after each row
    }
}
```

> **Mengapa memeriksa kepercayaan?** OCR tidak sempurna, terutama pada pemindaian beresolusi rendah. Nilai `Confidence` (0‑100) memungkinkan Anda memutuskan apakah menerima sel apa adanya atau menandainya untuk tinjauan manual. Ambang umum adalah 80 % untuk data penting.

### Output yang Diharapkan

Dengan asumsi gambar sumber berisi tabel 3 × 4 item baris faktur, Anda mungkin melihat sesuatu seperti:

```
Table found:
Item (conf:96%)   Qty (conf:94%)   Price (conf:97%)   Total (conf:95%)
Pen (conf:99%)    10 (conf:98%)    1.20 (conf:97%)    12.00 (conf:96%)
Notebook (conf:95%) 5 (conf:93%)  3.50 (conf:94%)    17.50 (conf:92%)
...
```

Jika tidak ada tabel yang terdeteksi, `result.Tables` akan kosong—tidak ada yang dicetak, tetapi program tetap akan keluar dengan mulus.

## Langkah 5: Menangani Kasus Tepi dan Kesalahan Umum

### Gambar Resolusi Rendah

Ketika gambar sumber di bawah 150 dpi, algoritma deteksi tabel dapat melewatkan batas sel. Solusi cepat adalah memperbesar gambar menggunakan `System.Drawing` sebelum memberikannya ke Aspose:

```csharp
using System.Drawing;
using System.Drawing.Imaging;

// Load and upscale
Bitmap bmp = new Bitmap(@"YOUR_DIRECTORY/invoice_with_table.png");
Bitmap resized = new Bitmap(bmp, new Size(bmp.Width * 2, bmp.Height * 2));
engine.Image = ImageStream.FromBitmap(resized);
```

### Tabel Miring

Jika tabel diputar beberapa derajat, aktifkan auto‑deskew:

```csharp
engine.Options.Deskew = true; // Turns on automatic deskewing
```

### Beberapa Tabel pada Satu Halaman

Aspose OCR mengembalikan setiap tabel sebagai objek terpisah di `result.Tables`. Anda dapat memperlakukan masing‑masing secara individual, atau menggabungkannya menjadi satu `DataTable` bila memerlukan tampilan terpadu.

```csharp
// Example: Merge all tables into one DataTable
var merged = new System.Data.DataTable();
foreach (var tbl in result.Tables)
{
    // Simple merge logic – assumes same column count
    // Add rows from each table
    for (int r = 0; r < tbl.Rows; r++)
    {
        var row = merged.NewRow();
        for (int c = 0; c < tbl.Columns; c++)
        {
            row[c] = tbl[r, c].Text;
        }
        merged.Rows.Add(row);
    }
}
```

### Mengekspor ke Excel

Setelah Anda memiliki `DataTable`, mengekspor ke file `.xlsx` sangat mudah dengan `ClosedXML`:

```csharp
using ClosedXML.Excel;

var workbook = new XLWorkbook();
var worksheet = workbook.Worksheets.Add(merged, "ExtractedTable");
workbook.SaveAs("ExtractedTable.xlsx");
```

Sekarang Anda benar‑benar **mengonversi gambar menjadi tabel** dan dapat menyerahkan spreadsheet tersebut ke proses selanjutnya.

## Contoh Lengkap yang Berfungsi – Dari Awal hingga Selesai

Berikut adalah program lengkap yang siap dijalankan. Tempelkan ke proyek konsol baru, ganti jalur file, dan tekan **F5**.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;
using System.Drawing;
using System.Data;
using ClosedXML.Excel;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine with the image
        OcrEngine engine = new OcrEngine
        {
            Image = ImageStream.FromFile(@"YOUR_DIRECTORY/invoice_with_table.png")
        };

        // 2️⃣ Enable table detection (key to convert image to table)
        engine.Options = new OcrOptions
        {
            DetectTables = true,
            Deskew = true // Helps with slightly rotated scans
        };

        // 3️⃣ Perform recognition
        OcrResult result = engine.Recognize();

        // 4️⃣ Process each detected table
        DataTable merged = new DataTable();
        bool firstTable = true;

        foreach (var table in result.Tables)
        {
            Console.WriteLine("Table found:");
            for (int r = 0; r < table.Rows; r++)
            {
                // Ensure DataTable has enough columns
                if (firstTable && merged.Columns.Count < table.Columns)
                {
                    for (int i = merged.Columns.Count; i < table.Columns; i++)
                        merged.Columns.Add($"Col{i + 1}");
                }

                DataRow dr = merged.NewRow();
                for (int c = 0; c < table.Columns; c++)
                {
                    var cell = table[r, c];
                    Console.Write($"{cell.Text} (conf:{cell.Confidence}%)\t");
                    dr[c] = cell.Text; // Populate DataTable for Excel export
                }
                Console.WriteLine();
                merged.Rows.Add(dr);
            }
            firstTable = false;
            Console.WriteLine(); // Blank line between tables
        }

        // 5️⃣ Optional: Export merged result to Excel
        if (merged.Rows.Count > 0)
        {
            using var wb = new XLWorkbook();
            wb.Worksheets.Add(merged, "ExtractedTables");
            wb.SaveAs("ExtractedTables.xlsx");
            Console.WriteLine("\nExcel file 'ExtractedTables.xlsx' created successfully.");
        }
        else
        {
            Console.WriteLine("\nNo tables were detected in the image.");
        }
    }
}
```

**Penjelasan alur**

1. **Pengaturan engine** – Memuat gambar dan memberi tahu Aspose untuk mencari tabel.
2. **Penyetelan opsi** – `DetectTables` melakukan pekerjaan berat; `Deskew` meningkatkan akurasi pada pemindaian miring.
3. **Recognition** – Mengembalikan teks biasa serta koleksi objek `Table`.
4. **Iterasi** – Mencetak setiap sel dengan kepercayaan, sekaligus membangun `DataTable` untuk ekspor nanti.
5. **Ekspor** – Menggunakan `ClosedXML` (perpustakaan ringan tanpa interop) untuk menulis file `.xlsx`—sempurna untuk analitik atau pelaporan lanjutan.

## Pertanyaan yang Sering Diajukan

- **Apakah ini bekerja dengan PDF?**  
  Ya. Konversi setiap halaman PDF menjadi gambar terlebih dahulu (`PdfRenderer` atau `Ghostscript`), lalu berikan bitmap ke Aspose OCR.

- **Bisakah saya mengekstrak tabel dari JPG?**  
  Tentu. Metode `ImageStream.FromFile` menerima JPEG, PNG, BMP, dan TIFF secara langsung.

- **Bagaimana jika tabel saya memiliki sel yang digabung?**  
  Aspose OCR memperlakukan sel yang digabung sebagai sel logis terpisah; Anda mungkin perlu memproses output lebih lanjut untuk menggabungkannya berdasarkan kepercayaan atau pola konten.

- **Apakah ada batas ukuran tabel?**  
  Secara praktis, engine menangani tabel hingga beberapa ratus baris. Kinerja menurun secara linier, jadi pertimbangkan memecah pemindaian yang sangat besar.

## Penutup

Kami baru saja menunjukkan cara


## Apa yang Harus Anda Pelajari Selanjutnya?

- [How to extract table from image using Aspose.OCR for .NET](/ocr/english/net/text-recognition/recognize-table/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}