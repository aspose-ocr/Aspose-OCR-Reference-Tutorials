---
category: general
date: 2026-03-18
description: Ekstrak tabel dari gambar menggunakan Aspose OCR di C#. Pelajari cara
  mengonversi tabel ke JSON, mendapatkan JSON tabel, dan mengekstrak teks dari gambar
  dalam hitungan menit.
draft: false
keywords:
- extract table from image
- convert table to json
- convert image to json
- extract text from image
- get table json
language: id
og_description: Ekstrak tabel dari gambar menggunakan Aspose OCR di C#. Pelajari cara
  mengonversi tabel ke JSON, dapatkan JSON tabel, dan ekstrak teks dari gambar dengan
  cepat.
og_title: Ekstrak Tabel dari Gambar dengan Aspose OCR – Panduan Lengkap C#
tags:
- Aspose OCR
- C#
- Table Extraction
title: Ekstrak Tabel dari Gambar dengan Aspose OCR – Panduan Lengkap C#
url: /id/net/text-recognition/extract-table-from-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ekstrak Tabel dari Gambar – Panduan Lengkap C#

Pernahkah Anda perlu **extract table from image** tetapi tidak yakin pustaka mana yang dapat melakukannya tanpa harus melakukan parsing manual yang rumit? Anda tidak sendirian. Dalam banyak proyek pemrosesan faktur atau pemindaian struk, titik sakit yang sebenarnya adalah mengubah bitmap yang berisik menjadi tabel terstruktur yang dapat dikonsumsi oleh sistem hilir Anda.  

Kabar baiknya? Dengan Aspose OCR Anda dapat **convert table to JSON** dalam beberapa baris kode, dan Anda juga mendapatkan teks polos dari seluruh gambar, jadi **extract text from image** menjadi bonus. Dalam tutorial ini kami akan membimbing Anda melalui seluruh alur – mulai dari memuat gambar hingga mendapatkan representasi JSON yang rapi dari tabel yang terdeteksi.

> **Quick win:** Pada akhir tutorial Anda akan memiliki aplikasi konsol C# yang dapat dijalankan dan mencetak baik teks OCR mentah maupun string JSON yang dapat langsung Anda masukkan ke basis data atau API.

## Prerequisites

Sebelum kita mulai, pastikan Anda memiliki:

- .NET 6.0 SDK (atau versi .NET terbaru) terpasang.  
- Lisensi Aspose OCR yang valid atau trial gratis (pustaka tetap berfungsi tanpa lisensi tetapi akan menambahkan watermark).  
- Sebuah gambar yang memang berisi tabel – misalnya `invoice_table.png`.  
- Visual Studio 2022, VS Code, atau editor apa pun yang Anda sukai.

Tidak ada paket NuGet tambahan selain `Aspose.OCR` yang diperlukan.

## Step 1: Set Up the Project and Install Aspose  OCR

Pertama, buat proyek konsol baru dan tambahkan pustaka OCR.

```bash
dotnet new console -n TableJsonDemo
cd TableJsonDemo
dotnet add package Aspose.OCR
```

> **Pro tip:** Jika Anda menggunakan proxy perusahaan, tambahkan flag `--no-restore` dan jalankan `dotnet restore` nanti dengan variabel lingkungan yang tepat.

## Step 2: Initialize the OCR Engine and Enable Table Recognition

Inti dari solusi ini adalah `OcrEngine`. Dengan mengaktifkan `EnableTableRecognition` kita memberi tahu Aspose OCR untuk mencari struktur seperti grid alih‑alih memperlakukan semuanya sebagai teks biasa.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Structure;

class TableJsonDemo
{
    static void Main()
    {
        // Create the OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Enable table detection – this is what lets us get a JSON table later
        ocrEngine.Settings.EnableTableRecognition = true;
```

Mengapa langkah ini penting? Tanpa pengenalan tabel, mesin akan meratakan gambar menjadi satu string tunggal, sehingga tidak mungkin merekonstruksi baris dan kolom nanti. Mengaktifkannya menambahkan fase analisis tata letak ringan yang hampir tidak mempengaruhi kinerja tetapi memberikan manfaat besar di hilir.

## Step 3: Load Your Image and Run the Recognition

Sekarang kita arahkan mesin ke file yang berisi tabel. `ImageStream.FromFile` mendukung sebagian besar format umum (PNG, JPEG, TIFF).

```csharp
        // Load the image that contains the table
        ImageStream image = ImageStream.FromFile("YOUR_DIRECTORY/invoice_table.png");

        // Perform OCR – this returns an OcrResult object with multiple helpers
        OcrResult ocrResult = ocrEngine.Recognize(image);
```

Jika gambar berukuran besar, pertimbangkan untuk mengubah ukurannya terlebih dahulu agar pemrosesan lebih cepat. Aspose OCR secara otomatis mendeteksi DPI, tetapi pemindaian 300 DPI biasanya merupakan titik optimal untuk kebanyakan tabel.

## Step 4: Extract the Plain Text – “extract text from image”

Meskipun tujuan utama kita adalah tabel, Anda sering tetap memerlukan teks mentah untuk pencatatan atau pemrosesan cadangan.

```csharp
        // Output the full recognized text
        Console.WriteLine("Full text:");
        Console.WriteLine(ocrResult.Text);
```

Properti `Text` menggabungkan semua yang dilihat mesin, mempertahankan jeda baris. Ini berguna ketika Anda perlu memverifikasi bahwa OCR telah membaca header atau footer di luar area tabel dengan benar.

## Step 5: Get the Detected Table as JSON – “convert table to json” & “get table json”

Inilah saat keajaiban terjadi. `GetTableAsJson()` menyerialisasi baris, kolom, dan isi sel yang terdeteksi ke dalam string JSON yang bersih.

```csharp
        // Retrieve the table structure as a JSON string
        string tableJson = ocrResult.GetTableAsJson();

        Console.WriteLine("\nDetected table (JSON):");
        Console.WriteLine(tableJson);
    }
}
```

JSON yang dihasilkan kira‑kira seperti ini (diformat untuk keterbacaan):

```json
{
  "Rows": [
    {
      "Cells": [
        { "Text": "Item", "ColumnIndex": 0 },
        { "Text": "Quantity", "ColumnIndex": 1 },
        { "Text": "Price", "ColumnIndex": 2 }
      ]
    },
    {
      "Cells": [
        { "Text": "Widget A", "ColumnIndex": 0 },
        { "Text": "10", "ColumnIndex": 1 },
        { "Text": "$5.00", "ColumnIndex": 2 }
      ]
    },
    {
      "Cells": [
        { "Text": "Widget B", "ColumnIndex": 0 },
        { "Text": "7", "ColumnIndex": 1 },
        { "Text": "$8.50", "ColumnIndex": 2 }
      ]
    }
  ]
}
```

Mengapa JSON menjadi format pilihan? JSON bersifat bahasa‑agnostik, mudah dideserialisasi menjadi objek, dan bekerja dengan baik bersama API web modern. Jika Anda memerlukan CSV, cukup iterasi baris dan gabungkan teks sel dengan koma.

## Step 6: (Optional) Convert the JSON to a .NET Object – “convert image to json”

Jika Anda lebih suka bekerja dengan tipe kuat, deserialisasikan JSON menggunakan `System.Text.Json`.

```csharp
using System.Text.Json;

...

        // Deserialize into a C# class (optional)
        var table = JsonSerializer.Deserialize<TableModel>(tableJson);
        Console.WriteLine("\nFirst cell value: " + table.Rows[0].Cells[0].Text);
```

Anda akan mendefinisikan `TableModel`, `RowModel`, dan `CellModel` agar sesuai dengan skema JSON. Langkah ini menunjukkan bagaimana Anda dapat pergi dari **convert image to json** hingga objek bertipe, memudahkan validasi di hilir.

## Full Working Example

Menggabungkan semuanya, berikut program lengkap yang siap dijalankan. Simpan sebagai `Program.cs` di dalam folder proyek yang telah dibuat sebelumnya.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Structure;
using System.Text.Json;

class TableJsonDemo
{
    static void Main()
    {
        // Step 1: Create OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Enable table recognition
        ocrEngine.Settings.EnableTableRecognition = true;

        // Step 3: Load image containing a table
        ImageStream image = ImageStream.FromFile("YOUR_DIRECTORY/invoice_table.png");

        // Step 4: Run OCR
        OcrResult ocrResult = ocrEngine.Recognize(image);

        // Step 5: Print full text (extract text from image)
        Console.WriteLine("Full text:");
        Console.WriteLine(ocrResult.Text);

        // Step 6: Get table as JSON (convert table to json, get table json)
        string tableJson = ocrResult.GetTableAsJson();
        Console.WriteLine("\nDetected table (JSON):");
        Console.WriteLine(tableJson);

        // Optional: Deserialize JSON to C# objects (convert image to json)
        var table = JsonSerializer.Deserialize<TableModel>(tableJson);
        Console.WriteLine("\nFirst cell value: " + table.Rows[0].Cells[0].Text);
    }
}

// Helper classes matching Aspose's JSON structure
public class TableModel
{
    public RowModel[] Rows { get; set; }
}
public class RowModel
{
    public CellModel[] Cells { get; set; }
}
public class CellModel
{
    public string Text { get; set; }
    public int ColumnIndex { get; set; }
}
```

### Expected Output

Saat Anda menjalankan `dotnet run`, Anda akan melihat sesuatu seperti:

```
Full text:
Item Quantity Price
Widget A 10 $5.00
Widget B 7 $8.50

Detected table (JSON):
{
  "Rows":[
    {"Cells":[{"Text":"Item","ColumnIndex":0},{"Text":"Quantity","ColumnIndex":1},{"Text":"Price","ColumnIndex":2}]},
    {"Cells":[{"Text":"Widget A","ColumnIndex":0},{"Text":"10","ColumnIndex":1},{"Text":"$5.00","ColumnIndex":2}]},
    {"Cells":[{"Text":"Widget B","ColumnIndex":0},{"Text":"7","ColumnIndex":1},{"Text":"$8.50","ColumnIndex":2}]}
  ]
}

First cell value: Item
```

Jika output terlihat kosong, periksa kembali bahwa `EnableTableRecognition` sudah diset ke `true` dan gambar memang berisi garis‑garis grid yang jelas.

## Common Pitfalls & How to Avoid Them

| Masalah | Mengapa Terjadi | Solusi |
|-------|----------------|-----|
| **Tidak ada JSON yang dikembalikan** | Deteksi tabel dinonaktifkan atau gambar terlalu rendah kontrasnya. | Pastikan `ocrEngine.Settings.EnableTableRecognition = true` dan tingkatkan kualitas gambar (tingkatkan kontras, binarisasi). |
| **Baris sebagian hilang** | OCR kebingungan karena sel yang digabung atau teks yang diputar. | Praproses gambar: luruskan (`ImageProcessor.Rotate`) atau pisahkan sel yang digabung secara manual. |
| **Karakter Unicode tidak terbaca** | Font tidak dikenali (misalnya tulisan tangan). | Ganti paket bahasa melalui `ocrEngine.Language = Language.English;` atau gunakan mesin OCR lain untuk tulisan tangan. |
| **Performa melambat** | Gambar sangat besar (>5 MP). | Turunkan resolusi menjadi ~1500 px lebar sambil mempertahankan DPI. |

## Next Steps: Going Beyond the Basics

Sekarang Anda dapat **extract table from image** dan **convert table to JSON**, pertimbangkan ekstensi berikut:

- **Simpan JSON** ke basis data dengan Entity Framework.  
- **Pasca‑proses** JSON untuk menormalkan format mata uang (misalnya menghapus `$`).  
- **Proses batch** folder faktur menggunakan `Directory.GetFiles` dan paralelkan dengan `Parallel.ForEach`.  
- **Integrasikan** dengan Azure Functions atau AWS Lambda untuk pipeline OCR tanpa server.

Setiap topik tersebut secara alami membawa kata kunci sekunder seperti **convert image to json** (ketika Anda mengirim seluruh hasil OCR ke endpoint cloud) dan **get table json** untuk analitik di hilir.

---

### Conclusion

Kami baru saja menunjukkan cara **extract table from image** menggunakan Aspose OCR, mengubah tabel tersebut menjadi JSON bersih, dan bahkan mendeserialisasikannya menjadi objek C#. Pola yang sama

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}