---
category: general
date: 2026-05-25
description: Pelajari cara mengekstrak teks dari gambar dengan API ASP.NET Core minimal.
  Unggah gambar via POST, baca data formulir multipart, dan lakukan OCR pada gambar.
draft: false
keywords:
- extract text from image
- upload image via post
- read multipart form data
- how to recognize text from image
- perform OCR on image
language: id
og_description: Ekstrak teks dari gambar menggunakan API ASP.NET Core minimal. Panduan
  ini menunjukkan cara mengunggah gambar via POST, membaca data formulir multipart,
  dan melakukan OCR pada gambar.
og_title: Ekstrak Teks dari Gambar di ASP.NET Core – Langkah demi Langkah
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: Learn how to extract text from image with a minimal ASP.NET Core API.
    Upload image via POST, read multipart form data and perform OCR on image.
  headline: Extract Text from Image in ASP.NET Core Minimal API – Complete Guide
  type: TechArticle
- description: Learn how to extract text from image with a minimal ASP.NET Core API.
    Upload image via POST, read multipart form data and perform OCR on image.
  name: Extract Text from Image in ASP.NET Core Minimal API – Complete Guide
  steps:
  - name: Breaking Down the Logic
    text: '| Step | What Happens | Why It Matters | |------|--------------|----------------|
      | **ReadFormAsync** | Parses the incoming *multipart/form-data* request. | Without
      this, you can’t access the uploaded files. | | **form.Files["image"]** | Retrieves
      the file whose form‑field name is `image`. | Guarant'
  - name: 1. Large Files
    text: 'The default request body limit is 30 MB. For larger scans you might need
      to adjust:'
  - name: 2. Asynchronous OCR
    text: Some OCR libraries expose async methods (`RecognizeAsync`). If yours does,
      replace `ocr.Recognize(img)` with `await ocr.RecognizeAsync(img)` and mark the
      lambda as `async`.
  - name: 3. Security Considerations
    text: '- **Validate file size** before loading it into memory. - **Sanitize the
      filename** if you ever write it to disk. - **Rate‑limit** the endpoint to avoid
      denial‑of‑service attacks.'
  - name: 4. GPU Acceleration
    text: If you uncomment the `engine.GpuDevice = new GpuDevice(0);` line and your
      hardware supports CUDA or DirectML, you’ll see a noticeable speed boost, especially
      on high‑resolution images.
  type: HowTo
tags:
- ASP.NET Core
- OCR
- Minimal API
title: Ekstrak Teks dari Gambar di ASP.NET Core Minimal API – Panduan Lengkap
url: /id/net/text-recognition/extract-text-from-image-in-asp-net-core-minimal-api-complete/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ekstrak Teks dari Gambar di ASP.NET Core Minimal API – Panduan Lengkap

Pernah bertanya-tanya bagaimana cara **extract text from image** tanpa berurusan dengan kerangka kerja yang berat? Anda tidak sendirian. Banyak pengembang membutuhkan cara cepat agar pengguna dapat mengunggah gambar dan mendapatkan kembali karakter mentah, baik itu memindai struk, mendigitalkan catatan tulisan tangan, atau menggerakkan indeks pencarian.

Dalam tutorial ini kami akan membuat ASP.NET Core Minimal API kecil yang **uploads image via POST**, mengurai muatan *multipart/form‑data*, dan kemudian **perform OCR on image** menggunakan singleton `OcrEngine`. Pada akhir tutorial Anda akan memiliki aplikasi yang dapat dijalankan sepenuhnya yang dapat Anda masukkan ke proyek .NET 8 mana pun dan mulai mengekstrak teks dari gambar segera.

## Apa yang Akan Anda Bangun

- A minimal web app yang mendengarkan pada `/ocr`.
- Endpoint yang menerima file gambar yang dikirim dengan permintaan POST `multipart/form-data`.
- Logika yang membaca file yang diunggah, memberi ke OCR engine, dan mengembalikan hasil plain‑text.
- Potongan kode akselerasi GPU opsional (dikomentasikan) untuk mereka yang memiliki kartu yang kompatibel.

**Prasyarat**  
- .NET 8 SDK (atau lebih baru).  
- Familiaritas dasar dengan C# dan command line.  
- Pustaka OCR yang menyediakan kelas `OcrEngine` (contoh mengasumsikan paket NuGet hipotetik).  

Jika Anda sudah memiliki itu, mari kita mulai.

## Langkah 1: Siapkan Proyek dan Tambahkan Paket OCR

Pertama, buat proyek web baru dan tambahkan pustaka OCR.

```bash
dotnet new web -n ImageOcrApi
cd ImageOcrApi
dotnet add package Awesome.Ocr --version 1.3.0   # replace with your actual OCR package
```

> **Pro tip:** Jaga dependensi Anda tetap terbaru. Versi yang lebih baru sering memberikan peningkatan performa, terutama untuk inferensi yang dipercepat GPU.

## Langkah 2: Daftarkan Singleton OCR Engine (Layanan Utama)

Kami menginginkan satu instance `OcrEngine` untuk seluruh aplikasi—tidak perlu membuat engine baru per permintaan. Daftarkan di container layanan builder.

```csharp
using Awesome.Ocr;               // <-- the OCR library namespace
using Microsoft.AspNetCore.Builder;
using Microsoft.AspNetCore.Http;
using System.Drawing;            // System.Drawing.Common for Image handling

var builder = WebApplication.CreateBuilder(args);

// Register a singleton OCR engine (English language)
// Uncomment the GPU line if you have a compatible GPU and the library supports it.
builder.Services.AddSingleton<OcrEngine>(sp =>
{
    var engine = new OcrEngine { Language = OcrLanguage.English };
    // engine.GpuDevice = new GpuDevice(0); // enable GPU acceleration
    return engine;
});
```

**Mengapa singleton?**  
Membuat OCR engine dapat mahal—bayangkan memuat bobot jaringan saraf ke memori. Dengan menggunakan kembali instance yang sama, kita menghemat siklus CPU dan RAM, yang berarti waktu respons lebih cepat untuk setiap panggilan `/ocr`.

## Langkah 3: Bangun Aplikasi

Sekarang kami mematerialisasikan objek `WebApplication`.

```csharp
var app = builder.Build();
```

Baris itu terlihat hampir ajaib, tetapi di baliknya ia menghubungkan routing, middleware, dan container DI yang baru saja kami konfigurasikan.

## Langkah 4: Definisikan Endpoint POST – “Upload Image via POST”

Berikut inti tutorial: endpoint yang **upload image via POST**, membaca payload multipart, dan menyerahkan data ke OCR engine.

```csharp
app.MapPost("/ocr", async (HttpRequest request, OcrEngine ocr) =>
{
    // Step 5: Read multipart form data and extract the uploaded image
    var form = await request.ReadFormAsync();               // <-- read multipart/form-data
    var file = form.Files["image"];                         // expects a field named "image"

    if (file is null || file.Length == 0)
    {
        return Results.BadRequest("No image file provided.");
    }

    // Guard against unsupported content types
    if (!file.ContentType.StartsWith("image/"))
    {
        return Results.BadRequest("Uploaded file is not an image.");
    }

    // Load the image into a System.Drawing.Image
    using var img = Image.FromStream(file.OpenReadStream());

    // Step 6: Perform OCR on the image
    string text = ocr.Recognize(img);                       // <-- perform OCR on image

    // Step 7: Return the extracted text as plain‑text
    return Results.Text(text);
});
```

### Memecah Logika

| Langkah | Apa yang Terjadi | Mengapa Penting |
|---------|------------------|-----------------|
| **ReadFormAsync** | Menganalisis permintaan *multipart/form-data* yang masuk. | Tanpa ini, Anda tidak dapat mengakses file yang diunggah. |
| **form.Files["image"]** | Mengambil file yang nama bidang formulirnya adalah `image`. | Menjamin kontrak yang dapat diprediksi bagi pemanggil. |
| **Content‑type check** | Memverifikasi bahwa file tersebut adalah gambar (mis., `image/png`). | Mencegah OCR engine gagal pada data yang bukan gambar. |
| **Image.FromStream** | Mengonversi aliran mentah menjadi `System.Drawing.Image`. | Pustaka OCR mengharapkan objek `Image`, bukan array byte mentah. |
| **ocr.Recognize(img)** | Memanggil OCR engine untuk **how to recognize text from image**. | Ini adalah langkah inti **perform OCR on image**. |
| **Results.Text** | Mengirim kembali respons plain‑text. | Format sederhana yang dapat dikonsumsi oleh layanan hilir. |

## Langkah 5: Jalankan API

Akhirnya, jalankan server web.

```csharp
app.Run();
```

Saat Anda menjalankan `dotnet run`, API akan mendengarkan pada `http://localhost:5000` (atau port pilihan Anda). Anda dapat mengujinya dengan `curl`:

```bash
curl -X POST http://localhost:5000/ocr \
  -F "image=@/path/to/receipt.png" \
  -H "Accept: text/plain"
```

**Output yang diharapkan:** Konsol akan mencetak karakter yang dikenali, mis.:

```
Total: $23.45
Date: 2026-05-20
Item A  $12.00
Item B  $11.45
```

Jika gambar buram atau bahasa tidak didukung, OCR engine akan mengembalikan string kosong atau pesan error—tangani kasus tersebut dalam kode produksi.

## Kasus Edge & Praktik Terbaik

### 1. File Besar

Batas default body permintaan adalah 30 MB. Untuk pemindaian yang lebih besar Anda mungkin perlu menyesuaikan:

```csharp
builder.Services.Configure<FormOptions>(options =>
{
    options.MultipartBodyLengthLimit = 100 * 1024 * 1024; // 100 MB
});
```

### 2. OCR Asinkron

Beberapa pustaka OCR menyediakan metode async (`RecognizeAsync`). Jika milik Anda demikian, ganti `ocr.Recognize(img)` dengan `await ocr.RecognizeAsync(img)` dan tandai lambda sebagai `async`.

### 3. Pertimbangan Keamanan

- **Validasi ukuran file** sebelum memuatnya ke memori.  
- **Sanitasi nama file** jika Anda pernah menuliskannya ke disk.  
- **Rate‑limit** endpoint untuk menghindari serangan denial‑of‑service.  

### 4. Akselerasi GPU

Jika Anda menghapus komentar pada baris `engine.GpuDevice = new GpuDevice(0);` dan perangkat keras Anda mendukung CUDA atau DirectML, Anda akan melihat peningkatan kecepatan yang signifikan, terutama pada gambar beresolusi tinggi.

## Contoh Lengkap yang Berfungsi

Berikut adalah `Program.cs` lengkap yang dapat Anda copy‑paste ke proyek Minimal API baru.

```csharp
using Awesome.Ocr;
using Microsoft.AspNetCore.Builder;
using Microsoft.AspNetCore.Http;
using Microsoft.AspNetCore.Http.Features;
using System.Drawing;

var builder = WebApplication.CreateBuilder(args);

// Optional: increase multipart limit for big images
builder.Services.Configure<FormOptions>(options =>
{
    options.MultipartBodyLengthLimit = 50 * 1024 * 1024; // 50 MB
});

// Register the OCR engine as a singleton
builder.Services.AddSingleton<OcrEngine>(sp =>
{
    var engine = new OcrEngine { Language = OcrLanguage.English };
    // engine.GpuDevice = new GpuDevice(0); // enable GPU if available
    return engine;
});

var app = builder.Build();

app.MapPost("/ocr", async (HttpRequest request, OcrEngine ocr) =>
{
    var form = await request.ReadFormAsync();
    var file = form.Files["image"];

    if (file is null || file.Length == 0)
        return Results.BadRequest("No image file provided.");

    if (!file.ContentType.StartsWith("image/"))
        return Results.BadRequest("Uploaded file is not an image.");

    using var img = Image.FromStream(file.OpenReadStream());

    // Core OCR operation
    string text = ocr.Recognize(img);

    return Results.Text(text);
});

app.Run();
```

Simpan, jalankan `dotnet run`, dan Anda siap untuk **extract text from image** sesuai permintaan.

## Kesimpulan

Kami telah membahas **solusi lengkap, end‑to‑end** untuk mengekstrak teks dari gambar menggunakan ASP.NET Core Minimal API. Mulai dari scaffolding proyek, kami **mendaftarkan singleton OCR engine**, membangun endpoint yang **uploads image via POST**, **read multipart form data**, dan akhirnya **perform OCR on image** untuk mengembalikan plain‑text bersih.

Dari sini Anda dapat:

- Menambahkan pembungkus JSON untuk respons yang lebih kaya.  
- Menyambungkan basis data untuk menyimpan teks yang diekstrak.  
- Memperluas dukungan ke banyak bahasa (`OcrLanguage.Spanish`, dll.).  

Pola ini skalabel dengan baik—cukup letakkan endpoint yang sama ke dalam microservice yang lebih besar atau expose di belakang API gateway.

Ada pertanyaan tentang penanganan PDF, pemrosesan batch, atau penyetelan GPU? Tinggalkan komentar, dan selamat coding!

## Tutorial Terkait

- [Extract Text from Image Using Aspose.OCR .NET](/ocr/english/net/image-and-drawing-recognition/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}