---
category: general
date: 2026-05-28
description: Cara melakukan OCR di ASP.NET Core—pelajari cara mengunggah gambar, mengekstrak
  teks dari gambar, dan menangani unggahan file secara efisien.
draft: false
keywords:
- how to perform OCR
- extract text from image
- handle file upload
- how to upload file
- upload image OCR
language: id
og_description: Cara melakukan OCR di ASP.NET Core. Pelajari langkah demi langkah
  cara mengunggah gambar, mengekstrak teks dari gambar, dan menangani unggahan file
  dengan Aspose OCR.
og_title: Cara Melakukan OCR di ASP.NET Core – Panduan Lengkap
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: How to perform OCR in ASP.NET Core—learn to upload image, extract text
    from image, and handle file upload efficiently.
  headline: How to Perform OCR in ASP.NET Core – Full Guide
  type: TechArticle
tags:
- OCR
- ASP.NET Core
- C#
- file upload
title: Cara Melakukan OCR di ASP.NET Core – Panduan Lengkap
url: /id/net/text-recognition/how-to-perform-ocr-in-asp-net-core-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Melakukan OCR di ASP.NET Core – Panduan Lengkap

Pernah bertanya‑tanya **bagaimana melakukan OCR** di dalam API web modern tanpa membuat rambut Anda rontok? Anda tidak sendirian. Pengembang terus‑menerus perlu membiarkan pengguna mengunggah gambar—mungkin struk, pemindaian paspor, atau catatan tulisan tangan—dan mendapatkan teks mentah kembali dalam format JSON.  

Dalam tutorial ini kami akan membahas solusi lengkap yang siap produksi yang menunjukkan **cara mengunggah file**, memvalidasinya, menjalankan Aspose OCR, dan akhirnya **mengekstrak teks dari gambar**. Pada akhir tutorial Anda akan memiliki controller siap‑tempel yang dapat dimasukkan ke proyek ASP.NET Core mana pun.

## Apa yang Akan Anda Bangun

- Sebuah `OcrController` yang menerima unggahan multipart/form‑data
- Validasi bahwa file memang ada dan tidak kosong
- Pemrosesan OCR secara asynchronous menggunakan mesin Aspose OCR
- Respons JSON bersih yang berisi teks yang dikenali

Tanpa layanan eksternal, tanpa sihir tersembunyi—hanya kode C# murni yang dapat Anda jalankan secara lokal.

## Prasyarat (Apa yang Anda Butuhkan Sebelum Memulai)

| Persyaratan | Mengapa Penting |
|-------------|-----------------|
| .NET 6 SDK atau yang lebih baru | ASP.NET Core 6+ memberikan fitur minimal API dan dukungan async. |
| Visual Studio 2022 (atau VS Code) | IDE memudahkan debugging, namun editor apa saja dapat digunakan. |
| Paket NuGet Aspose.OCR (`dotnet add package Aspose.OCR`) | Mesin yang benar‑benarnya melakukan pekerjaan OCR. |
| Pengetahuan dasar tentang ASP.NET Core MVC | Kita akan menggunakan `ControllerBase` dan atribut routing. |

Jika Anda sudah memiliki semua itu, bagus—ayo mulai.

## Langkah 1: Siapkan Proyek dan Instal Aspose OCR

Buka terminal dan buat proyek API web baru:

```bash
dotnet new webapi -n OcrDemo
cd OcrDemo
dotnet add package Aspose.OCR
```

Perintah tunggal itu menambahkan pustaka OCR beserta semua dependensinya. Tidak ada konfigurasi lain; Aspose berfungsi langsung untuk format gambar umum.

## Langkah 2: Tambahkan OCR Controller (Inti dari **cara melakukan OCR**)

Buat file baru `Controllers/OcrController.cs` dan tempelkan kode berikut. Ini contoh lengkap yang dapat dijalankan—tidak ada bagian yang hilang.

```csharp
using Aspose.OCR;
using Microsoft.AspNetCore.Mvc;
using System.Threading.Tasks;

namespace OcrDemo.Controllers
{
    [ApiController]
    [Route("[controller]")]
    public class OcrController : ControllerBase
    {
        // Step 1: Receive the uploaded file from the request
        [HttpPost("upload")]
        public async Task<IActionResult> Upload([FromForm] IFormFile uploadedFile)
        {
            // Step 2: Validate that a file was actually provided
            if (uploadedFile == null || uploadedFile.Length == 0)
                return BadRequest("No file supplied.");

            // Step 3: Open a read‑only stream for the file content
            await using var fileStream = uploadedFile.OpenReadStream();

            // Step 4: Create the OCR engine and load the image from the stream
            var ocrEngine = new OcrEngine();
            ocrEngine.Image = ImageStream.FromStream(fileStream);

            // Step 5: Perform asynchronous text recognition
            string extractedText = await ocrEngine.RecognizeAsync();

            // Step 6: Return the recognized text in the response
            return Ok(new { extractedText });
        }
    }
}
```

### Mengapa Ini Berfungsi

- **`[FromForm] IFormFile`** memberi tahu ASP.NET Core untuk mengikat bagian file multipart ke `uploadedFile`. Itu cara klasik **menangani unggahan file** di API web.
- Guard `if` memastikan kami **menangani kesalahan unggahan file** secara elegan, mengembalikan 400 Bad Request jika klien lupa mengirim file.
- `using var fileStream = uploadedFile.OpenReadStream();` membuka *stream* hanya‑baca, yang penting untuk file besar—tidak perlu memuat seluruh gambar ke memori sekaligus.
- `ocrEngine.Image = ImageStream.FromStream(fileStream);` memberi stream langsung ke Aspose OCR, menjaga alur tetap ramping.
- `await ocrEngine.RecognizeAsync();` menjalankan proses berat di thread latar belakang, sehingga API kami tetap responsif. Inilah inti dari **cara melakukan OCR** secara asynchronous.
- Akhirnya, kami membungkus hasil dalam objek JSON (`{ extractedText }`)—sempurna untuk konsumsi front‑end.

## Langkah 3: Konfigurasikan Batas Ukuran Permintaan (Opsional tapi Berguna)

Jika Anda mengharapkan pemindaian resolusi tinggi, tingkatkan batas ukuran permintaan default. Tambahkan ini ke `Program.cs`:

```csharp
builder.Services.Configure<FormOptions>(options =>
{
    options.MultipartBodyLengthLimit = 50 * 1024 * 1024; // 50 MB
});
```

Sekarang API tidak akan mogok pada gambar struk berukuran 10 MB. Sesuaikan batasnya sesuai kebutuhan Anda.

## Langkah 4: Uji Endpoint dengan cURL atau Postman

Berikut perintah cURL singkat yang dapat Anda jalankan dari terminal:

```bash
curl -X POST http://localhost:5000/ocr/upload \
  -F "uploadedFile=@/path/to/your/image.png"
```

Anda seharusnya melihat payload JSON serupa dengan:

```json
{
  "extractedText": "Sample text that was on the image."
}
```

Jika gambar tidak mengandung karakter yang dapat dikenali, string akan kosong—tidak ada yang crash, hanya hasil kosong. Itu adalah kasus tepi yang baik untuk diingat.

## Langkah 5: Konfirmasi Visual (Gambar Opsional)

Di bawah ini adalah screenshot placeholder yang menunjukkan respons JSON yang akan Anda terima setelah permintaan OCR berhasil.

![Hasil cara melakukan OCR – screenshot respons JSON yang menampilkan teks yang diekstrak](/images/ocr-result.png)

*Alt text:* **screenshot hasil cara melakukan OCR yang menampilkan teks yang diekstrak dari gambar**

## Kesalahan Umum & Tips Pro

| Kesalahan | Solusi |
|-----------|--------|
| **Format gambar tidak didukung** (misalnya TIFF dengan banyak halaman) | Konversi ke PNG/JPEG terlebih dahulu atau gunakan `ImageConverter` Aspose sebelum memberi ke `OcrEngine`. |
| **File besar menyebabkan tekanan memori** | Stream file seperti yang ditunjukkan; hindari `IFormFile.CopyToAsync` ke `MemoryStream`. |
| **OCR menghasilkan teks berantakan** | Pastikan gambar memiliki kontras tinggi dan orientasi yang tepat. Lakukan pra‑pemrosesan dengan `ocrEngine.Preprocess()` bila perlu. |
| **Beberapa permintaan bersamaan** | Aspose OCR bersifat thread‑safe, namun Anda mungkin ingin membatasi concurrency dengan semaphore jika server memiliki memori terbatas. |

## Memperluas Contoh: Unggah Massal & Pemrosesan Paralel

Jika Anda perlu **menangani unggahan file** untuk beberapa gambar sekaligus, ubah tanda tangan aksi untuk menerima daftar:

```csharp
[HttpPost("batch")]
public async Task<IActionResult> BatchUpload([FromForm] List<IFormFile> files)
{
    if (files == null || !files.Any())
        return BadRequest("No files supplied.");

    var results = new List<object>();

    foreach (var file in files)
    {
        await using var stream = file.OpenReadStream();
        var engine = new OcrEngine { Image = ImageStream.FromStream(stream) };
        var text = await engine.RecognizeAsync();
        results.Add(new { fileName = file.FileName, extractedText = text });
    }

    return Ok(results);
}
```

Sekarang Anda dapat **mengunggah OCR gambar** secara massal—ideal untuk memindai folder berisi banyak struk sekaligus.

## Pertimbangan Keamanan

- **Validasi ekstensi file** (`.png`, `.jpg`, `.jpeg`) sebelum diproses untuk menghindari unggahan berbahaya.
- **Pindai virus** jika API Anda terbuka ke internet; integrasikan dengan layanan seperti ClamAV.
- **Batasi laju** (rate‑limit) endpoint untuk mencegah serangan penolakan layanan (DoS).

## Output yang Diharapkan & Cara Memverifikasinya

Saat Anda memanggil endpoint `/ocr/upload` dengan gambar jelas yang berisi kata “Hello”, responsnya harus:

```json
{
  "extractedText": "Hello"
}
```

Anda dapat memverifikasinya dengan membuka alat pengembang browser → tab Network, atau dengan memeriksa output cURL.

## Ringkasan – Apa yang Telah Kita Bahas

- Menyiapkan proyek ASP.NET Core dan menambahkan paket NuGet Aspose OCR.
- Mengimplementasikan controller bersih yang menunjukkan **cara melakukan OCR**, **menangani unggahan file**, dan **mengekstrak teks dari gambar**.
- Membahas penanganan error, penyesuaian performa, dan praktik keamanan terbaik.
- Menyediakan contoh kode siap‑jalankan serta varian unggahan massal.

## Apa Selanjutnya?

- **Tambahkan dukungan bahasa**: Aspose OCR dapat dikonfigurasi untuk bahasa lain (`ocrEngine.Language = Language.English;`).
- **Integrasikan dengan basis data**: Simpan teks yang diekstrak bersama metadata untuk pencarian di masa mendatang.
- **UI Front‑end**: Bangun halaman React atau Blazor sederhana yang memungkinkan pengguna drag‑and‑drop gambar dan melihat hasil OCR secara instan.

Silakan bereksperimen—ganti mesin OCR, coba langkah pra‑pemrosesan gambar yang berbeda, atau hubungkan hasilnya ke model AI downstream. Langit adalah batasnya ketika Anda sudah tahu **cara melakukan OCR** dalam stack .NET modern.

Selamat coding, semoga teks Anda selalu terbaca!

## Tutorial Terkait

- [How to OCR Image – Perform OCR on Image in OCR Image Recognition](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)
- [How to Use Aspose to Recognize Image from Stream in OCR Image Recognition](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [How to Set Threshold Value in OCR Image Recognition](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}