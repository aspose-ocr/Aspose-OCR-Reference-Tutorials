---
category: general
date: 2026-03-05
description: Cara menggunakan OCR di C# untuk mengekstrak teks dari gambar struk.
  Pelajari cara memuat gambar untuk OCR dan mengenali gambar struk dalam hitungan
  menit.
draft: false
keywords:
- how to use OCR
- extract text from receipt
- load image for OCR
- recognize receipt image
language: id
og_description: Cara menggunakan OCR di C# untuk mengekstrak teks dari struk. Ikuti
  panduan langkah demi langkah ini untuk memuat gambar ke OCR dan mengenali gambar
  struk secara efisien.
og_title: Cara menggunakan OCR di C# – Ekstraksi Teks Resi Cepat
tags:
- OCR
- C#
- Aspose
- Receipt Processing
title: Cara Menggunakan OCR di C# – Ekstrak Teks dari Resi dengan Cepat
url: /id/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-receipts-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# cara menggunakan OCR di C# – Ekstrak Teks dari Resi dengan Cepat

Pernah bertanya-tanya **cara menggunakan OCR** untuk mengambil data langsung dari foto resi belanja? Anda tidak sendirian. Dalam banyak aplikasi usaha kecil, kendala utama adalah mengubah PNG yang buram menjadi teks terstruktur yang dapat Anda gunakan.

Kabar baik? Dengan beberapa baris C# dan Aspose.OCR Anda dapat **memuat gambar untuk OCR**, menjalankan mesin, dan **mengenali gambar resi** dalam kurang dari satu menit. Di bawah ini Anda akan melihat contoh lengkap yang siap dijalankan, plus tips untuk bagian‑bagian rumit yang sering dilewatkan tutorial lain.

## Apa yang Dibahas dalam Panduan Ini

Kami akan membahas semua yang perlu Anda ketahui:

* Menginstal paket NuGet Aspose.OCR.  
* Menyiapkan mesin OCR – inti dari **cara menggunakan OCR** dengan benar.  
* Memuat file resi (itu adalah langkah **memuat gambar untuk OCR**).  
* Menjalankan proses pengenalan dan mengambil data tata letak JSON serta XML.  
* Menangani jebakan umum seperti lisensi yang hilang atau format gambar yang tidak didukung.  

Pada akhir tutorial Anda akan memiliki program mandiri yang mengekstrak teks dari setiap resi yang Anda letakkan di folder. Tanpa layanan eksternal, tanpa keajaiban tersembunyi.

## Prasyarat

* .NET 6 SDK atau yang lebih baru (kode dapat dikompilasi dengan .NET Core juga).  
* File lisensi Aspose.OCR yang valid (`Aspose.OCR.lic`). Anda dapat mendapatkan trial gratis dari Aspose jika belum memilikinya.  
* Contoh gambar resi – `receipt.png` sudah cukup, tetapi format raster umum apa pun dapat digunakan.  

Jika Anda sudah memiliki semua itu, bagus – mari kita mulai.

![how to use OCR example](https://example.com/ocr-receipt.png "how to use OCR example")

## Langkah 1: Instal Aspose.OCR dan Buat Proyek Baru

Hal pertama yang harus dilakukan: Anda memerlukan pustaka yang benar‑benar melakukan pekerjaan berat. Buka terminal di folder proyek Anda dan jalankan:

```bash
dotnet new console -n ReceiptOcrDemo
cd ReceiptOcrDemo
dotnet add package Aspose.OCR
```

Perintah tersebut membuat aplikasi konsol dan mengunduh paket Aspose.OCR terbaru. Menurut pengalaman saya, memberi nama proyek yang singkat membuat jalur yang dihasilkan lebih mudah dibaca, terutama saat Anda mulai mengelola beberapa aplikasi demo.

## Langkah 2: Inisialisasi Mesin OCR – Inti dari **cara menggunakan OCR**

Sekarang kita akan menulis kode yang menjawab pertanyaan “**cara menggunakan OCR** di C#”. Buka `Program.cs` dan ganti isinya dengan cuplikan di bawah ini. Perhatikan komentar – mereka menjelaskan *mengapa* di balik setiap baris, bukan hanya *apa* yang dilakukan.

```csharp
using System;
using System.IO;
using Aspose.OCR;          // Aspose OCR namespace
using Aspose.OCR.Image;   // For loading images

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Create and configure the OCR engine.
        // -------------------------------------------------
        var ocrEngine = new OcrEngine();

        // Why set a license? Without it the engine runs in evaluation mode,
        // which adds a watermark to the output and limits batch size.
        ocrEngine.SetLicense("Aspose.OCR.lic");

        // -------------------------------------------------
        // 2️⃣ Load the receipt image – this is the **load image for OCR** step.
        // -------------------------------------------------
        // Change the path to point at your own receipt file.
        string imagePath = Path.Combine(
            Environment.CurrentDirectory, "receipt.png");

        // The ImageStream class abstracts file I/O and supports many formats.
        ocrEngine.Image = ImageStream.FromFile(imagePath);

        // -------------------------------------------------
        // 3️⃣ Run the recognition process – this is where we **recognize receipt image**.
        // -------------------------------------------------
        var ocrResult = ocrEngine.Recognize();

        // -------------------------------------------------
        // 4️⃣ Export the layout information as JSON.
        // -------------------------------------------------
        string jsonResult = ocrResult.ToJson();
        File.WriteAllText("receipt.json", jsonResult);
        Console.WriteLine("✅ JSON saved to receipt.json");

        // -------------------------------------------------
        // 5️⃣ Export the same layout information as XML.
        // -------------------------------------------------
        string xmlResult = ocrResult.ToXml();
        File.WriteAllText("receipt.xml", xmlResult);
        Console.WriteLine("✅ XML saved to receipt.xml");

        // -------------------------------------------------
        // 6️⃣ Quick preview – print the plain text to console.
        // -------------------------------------------------
        Console.WriteLine("\n--- Extracted Text ---");
        Console.WriteLine(ocrResult.Text);
    }
}
```

### Mengapa Ini Berfungsi

* **`OcrEngine`** adalah titik masuk; ia menyimpan semua konfigurasi yang dapat Anda ubah nanti (bahasa, DPI, dll.).  
* **`SetLicense`** menghapus watermark evaluasi – langkah penting ketika Anda berencana mendistribusikan kode.  
* **`ImageStream.FromFile`** melakukan pekerjaan **memuat gambar untuk OCR**, menangani PNG, JPEG, BMP, TIFF, dan lainnya.  
* **`Recognize()`** adalah metode yang sebenarnya **mengenali gambar resi**. Di baliknya, ia melakukan binarisasi, segmentasi, dan klasifikasi karakter.  
* Mengekspor ke JSON dan XML memberi Anda dump yang dapat dibaca manusia serta struktur yang ramah mesin yang dapat Anda masukkan ke parser selanjutnya.

## Langkah 3: Jalankan Demo dan Verifikasi Output

Kompilasi dan jalankan:

```bash
dotnet run
```

Jika semuanya terhubung dengan benar, Anda akan melihat sesuatu seperti:

```
✅ JSON saved to receipt.json
✅ XML saved to receipt.xml

--- Extracted Text ---
Walmart Supercenter
Date: 03/04/2026
Item    Qty   Price
Milk    2     2.58
Bread   1     1.99
Total   4.57
```

Konsol mencetak teks polos, sementara `receipt.json` dan `receipt.xml` berisi informasi tata letak terperinci (koordinat, skor kepercayaan, dll.). File‑file tersebut berguna jika Anda perlu memetakan setiap baris ke bidang basis data nanti.

## Kasus Khusus & Tips Profesional

### 1️⃣ Lisensi Hilang atau Tidak Valid
Jika `SetLicense` gagal, mesin akan beralih ke mode trial dan Anda akan mendapatkan watermark pada output. Bungkus pemanggilan dalam try/catch dan catat pesan yang ramah:

```csharp
try { ocrEngine.SetLicense("Aspose.OCR.lic"); }
catch (Exception ex)
{
    Console.WriteLine("⚠️ License not found – running in trial mode.");
    Console.WriteLine(ex.Message);
}
```

### 2️⃣ Format Gambar Tidak Didukung
Aspose.OCR mendukung sebagian besar format raster, tetapi jika Anda memberi PDF atau TIFF multi‑halaman, Anda harus mengonversi halaman yang diinginkan menjadi gambar terlebih dahulu. Pustaka `Aspose.PDF` dapat menangani konversi tersebut.

### 3️⃣ Resi Besar & Kinerja
Memproses gambar 10 MB dapat lambat. Kurangi resolusi sebelum memberikannya ke mesin:

```csharp
ocrEngine.Image = ImageStream.FromFile(imagePath).Resize(1024, 0);
```

Metode `Resize` menjaga rasio aspek (`0` untuk tinggi) dan mengurangi ukuran file secara dramatis tanpa mengorbankan akurasi OCR untuk resi tipikal.

### 4️⃣ Masalah Bahasa & Font
Resi dapat berisi karakter khusus (€, ¥, dll.). Atur bahasa secara eksplisit jika Anda mengetahui locale‑nya:

```csharp
ocrEngine.Language = Language.English; // or Language.Spanish, etc.
```

Untuk resi dengan bahasa campuran, Anda dapat mengaktifkan mode multibahasa:

```csharp
ocrEngine.Language = Language.English | Language.French;
```

### 5️⃣ Mengekstrak Data Terstruktur
Teks mentah berguna, tetapi kebanyakan aplikasi memerlukan bidang terstruktur (tanggal, total, item). Tata letak JSON mencakup koordinat `BoundingBox` untuk setiap kata. Anda dapat memprosesnya lebih lanjut seperti ini:

```csharp
var layout = Newtonsoft.Json.Linq.JObject.Parse(jsonResult);
foreach (var word in layout["Words"])
{
    string text = (string)word["Text"];
    // Simple heuristics: look for "$" or "Total"
}
```

Cuplikan tersebut menunjukkan idenya; dalam produksi Anda mungkin akan menggunakan ekspresi reguler atau mesin aturan kecil.

## Pertanyaan yang Sering Diajukan

**Q: Bisakah saya menjalankannya di Linux?**  
A: Tentu saja. Aspose.OCR bersifat lintas‑platform; cukup instal runtime .NET di mesin Linux Anda dan kode yang sama akan bekerja.

**Q: Bagaimana jika saya harus memproses puluhan resi per menit?**  
A: Buat loop `Parallel.ForEach` dan gunakan satu instance `OcrEngine` – ia thread‑safe untuk operasi baca‑saja. Ingat untuk menangani batasan lisensi pada concurrency.

**Q: Apakah ini bekerja dengan foto ponsel yang diambil dengan sudut miring?**  
A: Mesin sudah menyertakan deskewing dasar, tetapi untuk gambar yang sangat miring Anda mungkin perlu pra‑proses dengan pustaka pemrosesan gambar (mis., OpenCV) untuk meluruskan resi terlebih dahulu.

## Contoh Lengkap yang Siap Pakai (Copy‑Paste)

Berikut adalah program *seluruhnya* yang dapat Anda letakkan di `Program.cs`. Tidak ada file lain yang diperlukan selain lisensi dan gambar resi.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Image;

class Program
{
    static void Main()
    {
        // Create and configure the OCR engine
        var ocrEngine = new OcrEngine();
        try
        {
            ocrEngine.SetLicense("Aspose.OCR.lic");
        }
        catch (Exception)
        {
            Console.WriteLine("⚠️ Running in trial mode – license not found.");
        }

        // Load the image to be processed (load image for OCR)
        string imagePath = Path.Combine(Environment.CurrentDirectory, "

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}