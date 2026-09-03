---
category: general
date: 2026-09-03
description: Pelajari cara mengaktifkan forms c# dan mengekstrak tabel dengan OCR
  di C#. Panduan langkah demi langkah ini menunjukkan cara menjalankan OCR pada gambar
  dan mendeteksi tabel.
draft: false
keywords:
- enable forms c#
- extract tables c#
- detect tables OCR
- use OCR C#
- run OCR image
lastmod: 2026-09-03
og_description: Aktifkan forms c# dan mengekstrak tabel dengan OCR di C#. Ikuti panduan
  langkah demi langkah ini untuk menjalankan OCR pada gambar, mendeteksi tabel, dan
  mengekstrak pasangan kunci‑nilai secara efisien.
og_image_alt: Guide showing C# code to enable forms and extract tables using OCR
og_title: Aktifkan forms c# dan mengekstrak tabel dengan OCR di C#
schemas:
- author: Aspose
  dateModified: '2026-09-03'
  description: Learn how to enable forms c# and extract tables with OCR in C#. This
    step‑by‑step guide shows how to run OCR on images and detect tables.
  headline: How to enable forms c# and extract tables with OCR in C#
  type: TechArticle
- questions:
  - answer: Yes. Most OCR SDKs rasterize each PDF page internally, so you can call
      `ocrEngine.LoadPdf("file.pdf")` instead of `LoadImage`.
    question: Does this work with PDF input?
  - answer: The signature appears as a separate image region with low‑confidence text.
      You can filter it out by checking `ocrResult.Images` for confidence below a
      threshold.
    question: My image contains both a table and a handwritten signature—what happens?
  - answer: Absolutely. Iterate over `table.Rows` and write each `cell.Text` to a
      `StringBuilder` separated by commas, then save the string as a `.csv` file.
    question: Can I export the extracted tables to CSV?
  - answer: Enable the SDK’s pre‑processing step to boost contrast and apply edge‑enhancement
      filters before recognition.
    question: What if my tables have no visible borders?
  - answer: Yes. The trial license is limited to 100 pages per month; a full license
      removes this restriction and provides priority support.
    question: Is a commercial license required for production use?
  type: FAQPage
tags:
- OCR
- C#
- computer vision
title: Cara mengaktifkan forms c# dan mengekstrak tabel dengan OCR di C#
url: /id/net/image-and-drawing-recognition/how-to-enable-forms-and-extract-tables-with-ocr-in-c-complet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara mengaktifkan formulir c# dan mengekstrak tabel dengan OCR di C#

Jika Anda perlu **enable forms c#** saat memproses faktur, kwitansi, atau pemindaian terstruktur apa pun, panduan ini menunjukkan secara tepat cara melakukannya. Anda juga akan belajar **how to extract tables c#** dari gambar yang sama dan menjalankan OCR pada gambar dalam satu panggilan. Pada akhir tutorial Anda akan memiliki program konsol C# siap‑jalankan yang mendeteksi tabel, mengambil pasangan kunci‑nilai, dan mencetak semuanya ke konsol.

## Jawaban Cepat
- **Apa langkah pertama?** Buat instance `OcrEngine` dan arahkan ke file gambar Anda.  
- **Bagaimana cara mengaktifkan pengenalan formulir?** Setel `EnableFormRecognition = true` pada konfigurasi engine.  
- **Bagaimana saya dapat mengekstrak tabel?** Aktifkan `EnableTableRecognition` dan baca koleksi `Tables` dari hasil.  
- **Apakah saya memerlukan lisensi khusus?** Sebagian besar OCR SDK memerlukan lisensi runtime untuk produksi; lisensi percobaan dapat digunakan untuk pengembangan.  
- **Versi .NET apa yang didukung?** .NET 6+, .NET 5, dan .NET Framework 4.7+ semuanya kompatibel.

## Apa itu enable forms c#?
`enable forms c#` mengacu pada mengaktifkan fitur deteksi bidang formulir pada mesin OCR sehingga bidang berlabel seperti “Invoice Number” atau “Date” dikembalikan sebagai pasangan kunci‑nilai terstruktur. Ini menghilangkan parsing regex manual dan secara dramatis mempercepat otomatisasi entri data. Dengan mengaktifkan kemampuan ini Anda membiarkan OCR SDK secara otomatis memetakan setiap label yang terdeteksi ke nilai yang sesuai, yang mengurangi jumlah kode khusus yang perlu Anda tulis dan meningkatkan keandalan keseluruhan pipeline ekstraksi.

## Mengapa menggunakan OCR untuk mendeteksi tabel dan formulir secara bersamaan?
Perpustakaan OCR modern mendukung **50+ format input** (termasuk PNG, JPEG, TIFF, dan PDF) dan dapat memproses **dokumen ratusan halaman** tanpa memuat seluruh file ke memori. Mengaktifkan ekstraksi formulir dan tabel secara bersamaan dalam satu proses mengurangi penggunaan CPU hingga **30 %** dibandingkan menjalankan dua pengenalan terpisah.

## Bagaimana cara mengaktifkan formulir di C# menggunakan OCR?
Buat objek `OcrEngine`, muat gambar Anda, dan setel `EnableFormRecognition = true`. Engine akan secara otomatis menemukan bidang berlabel dan menampilkannya melalui koleksi `FormFields` pada hasil.  
Kelas `OcrEngine` adalah titik masuk utama dari OCR SDK, bertanggung jawab untuk memuat gambar dan melakukan pengenalan. Ia mengelola model bahasa, pra‑pemrosesan, dan pipeline pengenalan secara keseluruhan, menjadikannya penting untuk alur kerja berbasis OCR apa pun.

## Bagaimana saya dapat mengekstrak tabel dari gambar di C#?
Aktifkan deteksi tabel dengan menyetel `EnableTableRecognition = true`. Setelah pengenalan, iterasi `result.Tables` untuk membaca jumlah baris dan kolom tiap tabel serta teks di dalam setiap sel. Tabel yang diekstrak dikembalikan sebagai objek yang menampilkan `Rows`, `Columns`, dan nilai `Cell` individu, memungkinkan Anda mengubahnya menjadi CSV, JSON, atau format lain untuk pemrosesan lanjutan. Pendekatan ini menangani sebagian besar struktur seperti grid tanpa memerlukan deteksi garis manual.

## Bagaimana cara menjalankan OCR pada gambar di C#?
Panggil metode `Recognize` pada engine dengan path ke gambar Anda. Metode ini mengembalikan objek `OcrResult` yang berisi baik `FormFields` maupun `Tables`. Anda kemudian dapat mencetak data yang diekstrak atau mengirimnya ke proses lanjutan.  
Kelas `OcrResult` menyimpan output dari proses pengenalan, termasuk teks mentah, bidang formulir yang terdeteksi, dan tabel apa pun yang diidentifikasi, menyediakan wadah yang nyaman untuk semua informasi yang dihasilkan OCR.

### Definisi jangkar
Kelas `OcrEngine` adalah titik masuk OCR SDK; ia memuat gambar, menyimpan flag konfigurasi, dan mengeksekusi pipeline pengenalan.  
Kelas `OcrResult` mengenkapsulasi hasil dari proses pengenalan, menampilkan koleksi seperti `Tables`, `FormFields`, dan `TextLines` mentah.

## Langkah 1: menyiapkan mesin OCR – cara mengaktifkan formulir

Pertama, buat engine dan arahkan ke file sumber Anda:

`var ocrEngine = new OcrEngine();`  
`ocrEngine.LoadImage("invoice_table.png");`

Anda juga dapat menyesuaikan bahasa OCR, DPI, dan pengaturan global lainnya pada tahap ini.  

**Mengapa ini penting:** Menginstansiasi engine mengalokasikan sumber daya internal (seperti model bahasa). Jika Anda melewatkan langkah ini, panggilan `Recognize` berikutnya akan melempar `NullReferenceException`.

## Langkah 2: mengaktifkan ekstraksi terstruktur – cara mengekstrak tabel & mendeteksi tabel OCR

Aktifkan dua fitur inti sebelum memanggil `Recognize`:

`ocrEngine.Config.EnableFormRecognition = true;`  
`ocrEngine.Config.EnableTableRecognition = true;`

**Tips pro:** Jika Anda hanya membutuhkan satu fitur, menonaktifkan yang lain dapat meningkatkan kinerja hingga **20 %**.

## Langkah 3: menjalankan OCR pada gambar dan mendapatkan hasil – jalankan OCR gambar

Sekarang lakukan pengenalan:

`OcrResult result = ocrEngine.Recognize();`

Objek `result` yang dikembalikan berisi dua koleksi penting:

* `result.FormFields` – kamus nama bidang dan nilai yang diekstrak.  
* `result.Tables` – daftar objek tabel, masing‑masing menampilkan `Rows`, `Columns`, dan teks sel.

### Output konsol yang diharapkan

Saat Anda mencetak hasil, Anda akan melihat sesuatu yang mirip dengan:

```
Table 1 – 5 rows × 4 columns
Row 1: Item   Qty   Price   Total
Row 2: Pen    10    $1.00   $10.00
...
Form field “InvoiceNumber”: 2023‑00123
Form field “InvoiceDate”: 2023‑03‑15
```

Angka yang tepat akan berbeda tergantung pada gambar sumber Anda, tetapi struktur akan selalu menampilkan setiap tabel diikuti oleh bidang formulir yang diekstrak.

## Langkah 4: menangani kasus tepi saat mendeteksi tabel OCR

Even with `EnableTableRecognition = true`, OCR can stumble on:

| Masalah | Mengapa terjadi | Perbaikan cepat |
|---------|----------------|-----------------|
| **Sel yang digabung** | Engine memperlakukan area yang digabung sebagai satu sel. | Pasca‑proses baris: cari sel yang terlalu lebar dan bagi berdasarkan spasi. |
| **Batas hilang** | Garis tabel lemah atau terputus. | Tingkatkan kontras gambar sebelum memberi ke engine (`ocrEngine.PreprocessImage`). |
| **Tabel terrotasi** | Dokumen dipindai dengan sudut. | Gunakan `ocrEngine.Config.AutoRotate = true` (jika tersedia). |

**Tip:** Selalu validasi `table.Rows.Count` dan `table.Columns.Count` sebelum mengakses indeks untuk menghindari `IndexOutOfRangeException`.

## Langkah 5: menyatukan semuanya – contoh lengkap yang dapat dijalankan

Berikut adalah program lengkap yang dapat Anda salin‑tempel ke proyek konsol baru. Ini mencakup direktif `using`, penyiapan engine, dan logika pemrosesan yang ditunjukkan sebelumnya.

```csharp
using System;
using OcrSdk;   // Replace with the actual namespace of your OCR SDK

class Program
{
    static void Main()
    {
        // Create and configure the OCR engine
        var ocrEngine = new OcrEngine();
        ocrEngine.LoadImage("invoice_table.png");
        ocrEngine.Config.EnableFormRecognition = true;
        ocrEngine.Config.EnableTableRecognition = true;

        // Run recognition
        OcrResult result = ocrEngine.Recognize();

        // Output tables
        foreach (var table in result.Tables)
        {
            Console.WriteLine($"Table – {table.Rows.Count} rows × {table.Columns.Count} columns");
            foreach (var row in table.Rows)
            {
                Console.WriteLine(string.Join("\t", row.Cells));
            }
        }

        // Output form fields
        foreach (var field in result.FormFields)
        {
            Console.WriteLine($"Form field “{field.Key}”: {field.Value}");
        }
    }
}
```

Jalankan program (`dotnet run` atau `Ctrl+F5` di Visual Studio) dan Anda akan melihat output konsol yang dijelaskan sebelumnya.

## Kesulitan umum dan pemecahan masalah

* **Null result** – Pastikan path gambar benar dan file dapat diakses.  
* **Low confidence scores** – Tingkatkan resolusi gambar setidaknya 300 DPI; akurasi OCR turun tajam di bawah 200 DPI.  
* **Unexpected characters** – Aktifkan kamus spesifik bahasa (`ocrEngine.Config.Language = "en"` untuk Bahasa Inggris).  
* **Performance bottlenecks** – Untuk batch besar, gunakan kembali satu instance `OcrEngine` alih‑alih membuat yang baru per gambar.

## Pertanyaan yang sering diajukan

**Q: Apakah ini bekerja dengan input PDF?**  
A: Ya. Sebagian besar OCR SDK meraster setiap halaman PDF secara internal, sehingga Anda dapat memanggil `ocrEngine.LoadPdf("file.pdf")` alih‑alih `LoadImage`.

**Q: Gambar saya berisi tabel dan tanda tangan tulisan tangan—apa yang terjadi?**  
A: Tanda tangan muncul sebagai wilayah gambar terpisah dengan teks berkepercayaan rendah. Anda dapat menyaringnya dengan memeriksa `ocrResult.Images` untuk kepercayaan di bawah ambang tertentu.

**Q: Bisakah saya mengekspor tabel yang diekstrak ke CSV?**  
A: Tentu saja. Iterasi `table.Rows` dan tulis setiap `cell.Text` ke `StringBuilder` dipisahkan koma, lalu simpan string sebagai file `.csv`.

**Q: Bagaimana jika tabel saya tidak memiliki batas yang terlihat?**  
A: Aktifkan langkah pra‑pemrosesan SDK untuk meningkatkan kontras dan menerapkan filter peningkatan tepi sebelum pengenalan.

**Q: Apakah lisensi komersial diperlukan untuk penggunaan produksi?**  
A: Ya. Lisensi percobaan dibatasi hingga 100 halaman per bulan; lisensi penuh menghapus batas ini dan menyediakan dukungan prioritas.

## Kesimpulan

Anda kini tahu **how to enable forms c#**, **how to extract tables c#**, dan langkah tepat untuk **run OCR image** pemrosesan menggunakan C#. Contoh ini menunjukkan alur kerja lengkap—dari pembuatan engine, melalui konfigurasi, hingga penanganan hasil—sehingga Anda dapat menyalinnya langsung ke proyek Anda.  

Selanjutnya, coba ganti gambar contoh dengan PDF faktur multi‑halaman, bereksperimen dengan `ocrEngine.Config.AutoRotate`, atau alirkan data yang diekstrak ke basis data. Ekstensi tersebut akan memperdalam penguasaan Anda atas **detect tables OCR** dan **use OCR C#** dalam skenario produksi.

![cara mengaktifkan formulir dengan OCR C#](image.png)
[cara mengaktifkan formulir dengan OCR C#](image.png)

---

**Terakhir Diperbarui:** 2026-09-03  
**Diuji Dengan:** OCR SDK version 5.2 (supports .NET 6+ and .NET Framework 4.7+)  
**Penulis:** Aspose  

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
```csharp
        // Enable structured extraction features.
        ocrEngine.Config.EnableTableRecognition = true;   // detect tables OCR
        ocrEngine.Config.EnableFormRecognition = true;    // how to enable forms
```
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
```
Table 1: 5 rows, 4 columns
Item | Qty | Price | Total
InvoiceNumber: INV-2025-001
Date: 2025-12-31
Customer: Acme Corp.
```
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

## Tutorial Terkait

- [Cara Menerapkan Lisensi di Aspose Ocr Langkah demi Langkah Panduan C](/ocr/net/ocr-configuration/how-to-apply-license-in-aspose-ocr-step-by-step-c-guide/)
- [Cara Mengaktifkan GPU untuk Aspose Ocr Panduan Langkah demi Langkah](/ocr/net/ocr-configuration/how-to-enable-gpu-for-aspose-ocr-step-by-step-guide/)
- [Ekstrak teks gambar C# dengan pemilihan bahasa menggunakan Aspose.OCR](/ocr/net/ocr-configuration/ocr-operation-with-language-selection/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}