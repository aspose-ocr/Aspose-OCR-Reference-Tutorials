---
category: general
date: 2026-01-15
description: Konversi gambar ke JSON menggunakan Aspose OCR di C#. Pelajari cara mengekstrak
  teks dari gambar, mendapatkan kotak pembatas JSON, dan mengenali gambar struk.
draft: false
keywords:
- convert image to json
- extract text from image
- aspose ocr c# example
- recognize receipt image
- json bounding boxes
language: id
og_description: Konversi gambar ke JSON menggunakan Aspose OCR di C#. Panduan langkah
  demi langkah untuk mengekstrak teks dari gambar, mengenali gambar struk, dan mendapatkan
  kotak pembatas JSON.
og_title: Konversi Gambar ke JSON dengan Panduan Aspose OCR C#
tags:
- Aspose OCR
- C#
- JSON
- Image Processing
title: Konversi Gambar ke JSON dengan Panduan Aspose OCR C#
url: /id/net/text-recognition/convert-image-to-json-with-aspose-ocr-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Mengonversi Gambar ke JSON dengan Panduan Aspose OCR C#

Pernah membutuhkan untuk **convert image to JSON** tetapi tidak yakin pustaka mana yang dapat memberikan Anda teks mentah sekaligus koordinat kata yang tepat? Anda tidak sendirian. Banyak pengembang mengalami kendala ini ketika mencoba mengekstrak teks dari file gambar—terutama kwitansi—sementara juga membutuhkan payload JSON yang dapat dibaca mesin untuk pemrosesan selanjutnya.

> **Apa yang akan Anda dapatkan**  
> • Proyek C# yang berfungsi penuh yang **converts image to JSON**  
> • Pemahaman mengapa kami mengaktifkan `IncludeBoundingBoxes` (ini kunci untuk `json bounding boxes`)  
> • Tips untuk menangani berbagai format gambar dan bahasa  

Mari kita mulai.

---

## Apa yang Anda Butuhkan

Sebelum kita menyelam ke kode, pastikan Anda telah menginstal prasyarat berikut:

- **.NET 6.0 SDK** (atau versi yang lebih baru) – kode menargetkan .NET 6 tetapi juga dapat berjalan pada .NET Framework 4.7+.
- **Aspose.OCR for .NET** paket NuGet – Anda dapat menginstalnya melalui `dotnet add package Aspose.OCR`.
- Gambar contoh kwitansi (`receipt.jpg`) ditempatkan di folder yang dapat Anda referensikan dari proyek Anda.
- Visual Studio 2022, VS Code, atau IDE apa pun yang Anda sukai.

Tidak ada layanan eksternal lain yang diperlukan; semuanya berjalan secara lokal.

## Mengonversi Gambar ke JSON – Ikhtisar

Ide dasarnya sederhana: muat sebuah gambar, beri tahu Aspose OCR untuk mengenali bahasa Inggris (atau bahasa lain yang didukung), minta agar menyertakan bounding boxes, dan akhirnya minta hasil dalam format **JSON**. Pustaka ini melakukan semua pekerjaan berat—OCR, analisis tata letak, dan serialisasi JSON.

Berikut diagram tingkat tinggi alur proses (bayangkan gambar kecil):

```
[Image File] → Aspose OCR Engine → Recognition Options (JSON + Bounding Boxes) → JSON Output
```

Diagram kecil itu menangkap seluruh pipeline yang akan kami implementasikan.

## Langkah 1: Siapkan Proyek dan Instal Aspose OCR

Pertama, buat proyek konsol baru dan tambahkan paket Aspose OCR.

```bash
dotnet new console -n JsonOutputDemo
cd JsonOutputDemo
dotnet add package Aspose.OCR
```

> **Pro tip:** Jika Anda menggunakan Visual Studio, klik kanan proyek → *Manage NuGet Packages* → cari **Aspose.OCR** dan instal versi stabil terbaru (saat ini 23.12).

## Langkah 2: Muat Gambar yang Ingin Anda Kenali

Kami akan menggunakan metode `OcrImage.FromFile` untuk membaca gambar kwitansi. Pastikan jalur mengarah ke file yang nyata; jika tidak, Anda akan mendapatkan `FileNotFoundException`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Output;

class JsonOutputDemo
{
    static void Main()
    {
        // Step 2: Load the image you want to recognize
        var receiptImage = OcrImage.FromFile("YOUR_DIRECTORY/receipt.jpg");
```

Jika gambar Anda berada di samping file `.csproj`, Anda cukup menggunakan `"receipt.jpg"`.

## Langkah 3: Konfigurasikan Opsi OCR untuk JSON Bounding Boxes

Keajaiban terjadi ketika kami mengaktifkan `OutputFormat = OutputFormat.Json` **dan** `IncludeBoundingBoxes = true`. Yang pertama memberi tahu Aspose untuk menyerialisasi hasil sebagai JSON, sementara yang kedua menambahkan `x`, `y`, `width`, dan `height` untuk setiap kata—tepat apa yang Anda butuhkan untuk `json bounding boxes`.

```csharp
        // Step 3: Configure OCR options
        var ocrOptions = new OcrOptions
        {
            OutputFormat = OutputFormat.Json,
            IncludeBoundingBoxes = true   // include coordinates for each recognized word
        };
```

Anda juga dapat menyesuaikan `ocrOptions.Dpi` atau `ocrOptions.Language` jika memerlukan resolusi lebih tinggi atau bahasa yang berbeda.

## Langkah 4: Lakukan Pengakuan – Ekstrak Teks dari Gambar

Sekarang kami memanggil `Recognize`. Metode ini mengembalikan objek `OcrResult` yang berisi string JSON, teks mentah, dan lainnya.

```csharp
        // Step 4: Perform recognition using English language and the configured options
        var ocrEngine = new OcrEngine();
        var ocrResult = ocrEngine.Recognize(receiptImage, Language.English, ocrOptions);
```

Jika Anda perlu menangani bahasa lain, ganti `Language.English` dengan `Language.Spanish`, `Language.French`, dll. Aspose mendukung lebih dari 30 bahasa secara default.

## Langkah 5: Keluarkan Hasil – Payload JSON Anda

Akhirnya, kami mencetak JSON ke konsol. Dalam aplikasi nyata Anda mungkin akan menuliskannya ke file atau mengirimnya ke layanan.

```csharp
        // Step 5: Output the resulting JSON string
        System.Console.WriteLine(ocrResult.Json);
    }
}
```

Menjalankan program seharusnya menghasilkan dokumen JSON yang mirip dengan potongan di bawah ini.

```json
{
  "Text": "Total $12.34\nDate 01/01/2024",
  "Words": [
    {
      "Text": "Total",
      "BoundingBox": { "X": 45, "Y": 112, "Width": 60, "Height": 20 }
    },
    {
      "Text": "$12.34",
      "BoundingBox": { "X": 110, "Y": 112, "Width": 70, "Height": 20 }
    },
    {
      "Text": "Date",
      "BoundingBox": { "X": 45, "Y": 140, "Width": 50, "Height": 20 }
    },
    {
      "Text": "01/01/2024",
      "BoundingBox": { "X": 100, "Y": 140, "Width": 120, "Height": 20 }
    }
  ]
}
```

Perhatikan bagaimana setiap kata kini membawa **JSON bounding box**‑nya—sempurna untuk dimasukkan ke overlay UI atau parser selanjutnya.

## Contoh Lengkap yang Berfungsi

Berikut adalah program lengkap yang siap disalin‑tempel. Tidak ada bagian tersembunyi, tidak ada panggilan eksternal—hanya C# murni.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Output;

class JsonOutputDemo
{
    static void Main()
    {
        // 1️⃣ Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // 2️⃣ Load the image you want to recognize
        var receiptImage = OcrImage.FromFile("YOUR_DIRECTORY/receipt.jpg");

        // 3️⃣ Configure OCR options to get detailed JSON output with word positions
        var ocrOptions = new OcrOptions
        {
            OutputFormat = OutputFormat.Json,
            IncludeBoundingBoxes = true   // include coordinates for each recognized word
        };

        // 4️⃣ Perform recognition using English language and the configured options
        var ocrResult = ocrEngine.Recognize(receiptImage, Language.English, ocrOptions);

        // 5️⃣ Output the resulting JSON string
        System.Console.WriteLine(ocrResult.Json);
    }
}
```

> **Perhatikan:**  
> • **Kesalahan jalur file** – periksa kembali lokasi gambar.  
> • **Paket NuGet yang hilang** – pastikan `Aspose.OCR` direferensikan.  
> • **Format gambar tidak didukung** – gunakan JPEG, PNG, BMP, atau TIFF untuk hasil terbaik.

## Pertanyaan Umum & Kasus Tepi

### Apakah saya dapat mengonversi **halaman PDF** ke JSON alih-alih JPEG?

Ya. Konversikan halaman PDF ke gambar terlebih dahulu (misalnya, menggunakan `Aspose.PDF`), kemudian masukkan gambar tersebut ke pipeline OCR yang sama. Output JSON akan identik karena langkah OCR hanya memperhatikan data raster.

### Bagaimana jika kwitansi buram?

Tingkatkan DPI di `ocrOptions`. Misalnya:

```csharp
ocrOptions.Dpi = 300; // higher DPI improves accuracy on low‑quality scans
```

DPI yang lebih tinggi dapat meningkatkan penggunaan memori, jadi seimbangkan kualitas dengan kinerja.

### Saya membutuhkan **banyak bahasa** pada kwitansi yang sama (mis., English + Spanish).

Anda dapat mengirimkan array bahasa:

```csharp
var ocrResult = ocrEngine.Recognize(receiptImage, new[] { Language.English, Language.Spanish }, ocrOptions);
```

Aspose akan mencoba mengenali setiap bahasa dalam urutan yang ditentukan.

### Bagaimana cara menulis JSON ke file?

Cukup ganti baris `Console.WriteLine` dengan:

```csharp
System.IO.File.WriteAllText("receipt.json", ocrResult.Json);
```

Sekarang Anda memiliki file persisten yang dapat Anda kirim ke layanan lain.

## Ringkasan Visual

![contoh mengonversi gambar ke json](convert-image-to-json.png "contoh mengonversi gambar ke json")

*Tangkapan layar menunjukkan output konsol dari payload JSON setelah menjalankan demo.*

## Kesimpulan

Kami baru saja menunjukkan cara **convert image to JSON** menggunakan Aspose OCR di C#. Dengan mengonfigurasi `OutputFormat` dan `IncludeBoundingBoxes`, Anda dapat **extract text from image**, **recognize receipt image**, dan memperoleh **JSON bounding boxes** yang tepat untuk setiap kata. Kode lengkap yang dapat dijalankan ada di potongan di atas, sehingga Anda dapat menambahkannya ke proyek .NET mana pun sekarang juga.

Apa selanjutnya? Cobalah mengirim JSON ke penampil front‑end yang menyorot setiap kata, atau dorong data ke model machine‑learning yang mengklasifikasikan item baris pada kwitansi. Anda juga dapat bereksperimen dengan bahasa lain, pengaturan DPI lebih tinggi, atau pemrosesan batch beberapa gambar dalam loop.

Jika Anda mengalami kendala, ingatlah tips tentang jalur file, DPI, dan array bahasa. Jangan ragu untuk meninggalkan komentar atau membuka issue di repositori GitHub yang Anda buat untuk demo ini. Selamat coding, dan nikmati mengubah gambar menjadi JSON terstruktur!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}