---
category: general
date: 2026-01-04
description: Pelajari cara mengaktifkan formulir dan mengekstrak tabel dari gambar
  menggunakan OCR di C#. Tutorial langkah demi langkah ini juga menunjukkan cara menjalankan
  OCR pada gambar dan mendeteksi tabel dengan OCR.
draft: false
keywords:
- how to enable forms
- how to extract tables
- run OCR image
- use OCR C#
- detect tables OCR
language: id
og_description: Panduan langkah demi langkah tentang cara mengaktifkan formulir, mengekstrak
  tabel, menjalankan OCR gambar, dan mendeteksi tabel OCR menggunakan C#.
og_title: Cara Mengaktifkan Formulir dan Mengekstrak Tabel dengan OCR di C#
tags:
- OCR
- C#
- Computer Vision
title: Cara Mengaktifkan Formulir dan Mengekstrak Tabel dengan OCR di C# – Panduan
  Lengkap
url: /id/net/image-and-drawing-recognition/how-to-enable-forms-and-extract-tables-with-ocr-in-c-complet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Mengaktifkan Formulir dan Mengekstrak Tabel dengan OCR di C# – Panduan Lengkap

Pernah bertanya‑tanya **bagaimana cara mengaktifkan formulir** saat memindai faktur, kwitansi, atau dokumen terstruktur lainnya? Anda tidak sendirian. Pada banyak proyek dunia nyata, titik gesekan terbesar adalah membuat OCR memahami baik bidang formulir **maupun** tabel tanpa harus menulis jutaan baris parsing khusus.  

Dalam tutorial ini kami akan membahas solusi praktis end‑to‑end yang menunjukkan **cara mengaktifkan formulir**, **cara mengekstrak tabel**, dan bahkan **cara menjalankan pemrosesan gambar OCR** dalam satu program C#. Pada akhir tutorial Anda akan memiliki cuplikan kode siap‑jalankan yang mendeteksi tabel ala OCR, mengambil pasangan kunci‑nilai, dan mencetaknya ke konsol.

> **Prasyarat** – .NET 6+ (atau .NET Framework 4.7+), referensi ke SDK OCR yang Anda gunakan (contoh mengasumsikan kelas `OcrEngine` generik), dan file gambar (`invoice_table.png`) yang berisi tabel atau formulir. Tidak diperlukan pustaka eksternal lain.

![cara mengaktifkan formulir dengan OCR C#](image.png)

## Apa yang Dibahas dalam Tutorial Ini

- **Mengaktifkan pengenalan formulir** sehingga bidang seperti “Invoice Number” atau “Date” secara otomatis teridentifikasi.  
- **Mengekstrak tabel** dari dokumen yang dipindai, memberikan Anda jumlah baris/kolom serta isi sel.  
- **Menjalankan pemrosesan gambar OCR** dalam satu panggilan dan menangani hasilnya secara programatik.  
- Tips untuk **mendeteksi tabel OCR** pada kasus tepi, seperti sel yang digabung atau batas yang hilang.  

Mari kita mulai.

## Langkah 1: Siapkan OCR Engine – cara mengaktifkan formulir

Sebelum pengenalan apa pun dapat terjadi, Anda memerlukan instance OCR engine. Sebagian besar SDK menyediakan konstruktor sederhana; kami juga akan menunjukkan di mana Anda dapat menyesuaikan opsi konfigurasi nanti.

```csharp
using System;
using System.Linq;

// Assume the OCR SDK namespace is OcrSdk
using OcrSdk;

public class OcrDemo
{
    public static void Main()
    {
        // Create the OCR engine – this is where “how to enable forms” starts.
        OcrEngine ocrEngine = new OcrEngine();

        // Load the image that contains a table or form.
        // Replace the path with the actual location of your PNG/JPEG/TIFF file.
        ocrEngine.LoadImage(@"YOUR_DIRECTORY/invoice_table.png");
```

**Mengapa ini penting:** Membuat instance engine mengalokasikan sumber daya internal (seperti model bahasa). Jika Anda melewatkan langkah ini, pemanggilan `Recognize` berikutnya akan melempar `NullReferenceException`.

## Langkah 2: Aktifkan Ekstraksi Terstruktur – cara mengekstrak tabel & mendeteksi tabel OCR

Sekarang kami mengaktifkan dua fitur inti: pengenalan tabel dan ekstraksi bidang formulir. Kebanyakan OCR modern menyediakan flag boolean atau objek `Config` yang lebih terperinci.

```csharp
        // Enable structured extraction features.
        ocrEngine.Config.EnableTableRecognition = true;   // detect tables OCR
        ocrEngine.Config.EnableFormRecognition = true;    // how to enable forms
```

**Tips profesional:** Jika Anda hanya membutuhkan satu fitur, menonaktifkan yang lain dapat meningkatkan kinerja hingga 20 %.

## Langkah 3: Jalankan OCR Image dan Dapatkan Hasilnya – run OCR image

Dengan engine yang sudah dikonfigurasi, satu pemanggilan metode melakukan semua pekerjaan berat. `OcrResult` yang dikembalikan berisi koleksi untuk tabel dan bidang formulir.

```csharp
        // Run OCR – this is the “run OCR image” step.
        OcrResult ocrResult = ocrEngine.Recognize();

        // -----------------------------------------------------------------
        // Step 4: Process Detected Tables – how to extract tables
        // -----------------------------------------------------------------
        foreach (var table in ocrResult.Tables)
        {
            Console.WriteLine($"Table {table.Id}: {table.Rows.Count} rows, {table.Columns.Count} columns");

            // Show the first row for a quick sanity check.
            if (table.Rows.Count > 0)
            {
                var firstRow = table.Rows[0];
                Console.WriteLine(string.Join(" | ", firstRow.Cells.Select(c => c.Text)));
            }
        }

        // -----------------------------------------------------------------
        // Step 5: Process Detected Form Fields – how to enable forms
        // -----------------------------------------------------------------
        foreach (var field in ocrResult.FormFields)
        {
            Console.WriteLine($"{field.Key}: {field.Value}");
        }
    }
}
```

### Output Konsol yang Diharapkan

```
Table 1: 5 rows, 4 columns
Item | Qty | Price | Total
InvoiceNumber: INV-2025-001
Date: 2025-12-31
Customer: Acme Corp.
```

Angka-angka yang tepat akan berbeda tergantung pada gambar sumber Anda, tetapi Anda akan melihat baris ringkasan untuk setiap tabel diikuti oleh nilai sel baris pertama, dan kemudian daftar pasangan kunci‑nilai untuk bidang formulir.

## Langkah 4: Menangani Kasus Tepi Saat Mendeteksi Tabel OCR

Bahkan dengan `EnableTableRecognition = true`, OCR dapat mengalami kesulitan pada:

| Masalah | Mengapa Terjadi | Solusi Cepat |
|---------|----------------|--------------|
| **Sel yang digabung** | Engine memperlakukan area yang digabung sebagai satu sel. | Proses pasca‑baris: cari sel yang terlalu lebar dan bagi berdasarkan spasi. |
| **Batas yang hilang** | Garis tabel lemah atau terputus. | Tingkatkan kontras gambar sebelum memberi ke engine (`ocrEngine.PreprocessImage`). |
| **Tabel yang diputar** | Dokumen dipindai dengan sudut. | Gunakan `ocrEngine.Config.AutoRotate = true` (jika tersedia). |

**Tip:** Selalu validasi `table.Rows.Count` dan `table.Columns.Count` sebelum mengakses indeks untuk menghindari `IndexOutOfRangeException`.

## Langkah 5: Menggabungkan Semua – Contoh Lengkap yang Dapat Dijalanin

Berikut adalah program lengkap yang dapat Anda salin‑tempel ke proyek konsol baru. Program ini mencakup direktif `using`, penyiapan engine, dan logika pemrosesan yang ditunjukkan sebelumnya.

```csharp
using System;
using System.Linq;
using OcrSdk;   // Replace with your actual OCR SDK namespace

public class OcrDemo
{
    public static void Main()
    {
        // 1️⃣ Create OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Load the target image
        ocrEngine.LoadImage(@"YOUR_DIRECTORY/invoice_table.png");

        // 3️⃣ Enable structured extraction (forms + tables)
        ocrEngine.Config.EnableTableRecognition = true;   // detect tables OCR
        ocrEngine.Config.EnableFormRecognition = true;    // how to enable forms

        // 4️⃣ Run OCR – “run OCR image”
        OcrResult ocrResult = ocrEngine.Recognize();

        // 5️⃣ Process tables – “how to extract tables”
        foreach (var table in ocrResult.Tables)
        {
            Console.WriteLine($"Table {table.Id}: {table.Rows.Count} rows, {table.Columns.Count} columns");
            if (table.Rows.Count > 0)
            {
                var firstRow = table.Rows[0];
                Console.WriteLine(string.Join(" | ", firstRow.Cells.Select(c => c.Text)));
            }
        }

        // 6️⃣ Process form fields – “how to enable forms”
        foreach (var field in ocrResult.FormFields)
        {
            Console.WriteLine($"{field.Key}: {field.Value}");
        }
    }
}
```

Jalankan program (`dotnet run` atau `Ctrl+F5` di Visual Studio) dan Anda akan melihat output konsol yang telah dijelaskan sebelumnya.

## Pertanyaan yang Sering Diajukan (FAQ)

**T: Apakah ini bekerja dengan input PDF?**  
J: Sebagian besar SDK OCR menerima PDF dengan meraster setiap halaman secara internal. Cukup panggil `ocrEngine.LoadPdf("file.pdf")` alih‑alih `LoadImage`.

**T: Bagaimana jika gambar saya berisi tabel *dan* tanda tangan?**  
J: Tanda tangan akan muncul sebagai wilayah gambar terpisah. Anda dapat mengabaikannya dengan memeriksa `ocrResult.Images` untuk teks dengan kepercayaan rendah.

**T: Bisakah saya mengekspor tabel ke CSV?**  
J: Tentu saja. Setelah iterasi `table.Rows`, tulis setiap `cell.Text` ke `StringBuilder` dipisahkan koma, lalu simpan string tersebut ke file `.csv`.

## Kesimpulan

Sekarang Anda tahu **cara mengaktifkan formulir**, **cara mengekstrak tabel**, dan langkah‑langkah tepat untuk **menjalankan pemrosesan OCR image** menggunakan C#. Contoh ini memperlihatkan alur kerja lengkap—dari pembuatan engine, melalui konfigurasi, hingga penanganan hasil—sehingga Anda dapat menyalinnya langsung ke proyek Anda sendiri.  

Selanjutnya, coba ganti gambar contoh dengan PDF faktur multi‑halaman, eksperimen dengan `ocrEngine.Config.AutoRotate`, atau alirkan data yang diekstrak ke basis data. Ekstensi‑ekstensi tersebut akan memperdalam penguasaan Anda atas **mendeteksi tabel OCR** dan **menggunakan OCR C#** dalam skenario produksi.

Jika Anda mengalami kendala, silakan tinggalkan komentar di bawah. Selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}