---
category: general
date: 2026-06-28
description: Mengenali teks dari gambar di ASP.NET Core – pelajari cara mengunggah
  gambar untuk OCR dan memproses gambar OCR dari aliran secara efisien.
draft: false
keywords:
- recognize text from image
- upload image for ocr
- ocr image from stream
language: id
og_description: Mengenali teks dari gambar menggunakan Aspose OCR di ASP.NET Core.
  Unggah gambar untuk OCR, proses gambar OCR dari stream, dan kembalikan teks bersih.
og_title: Mengenali Teks dari Gambar di ASP.NET Core – Panduan Lengkap
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: recognize text from image in ASP.NET Core – learn how to upload image
    for OCR and process ocr image from stream efficiently.
  headline: recognize text from image in ASP.NET Core – upload for OCR
  type: TechArticle
- description: recognize text from image in ASP.NET Core – learn how to upload image
    for OCR and process ocr image from stream efficiently.
  name: recognize text from image in ASP.NET Core – upload for OCR
  steps:
  - name: Why This Pattern Works
    text: '- **Single `OcrEngine` instance**: Instantiating the engine once avoids
      the overhead of loading language data on every request. - **Async everything**:
      By using `await` on `FromStreamAsync` and `RecognizeAsync`, the ASP.NET Core
      thread pool stays free to serve other callers. - **`IFormFile` binding*'
  - name: Edge Cases to Watch
    text: '- **Corrupt files**: If the uploaded file isn’t a valid image, `FromStreamAsync`
      throws an exception. Wrap the call in a try/catch if you need graceful error
      messages. - **Unsupported formats**: Aspose supports PNG, JPEG, BMP, TIFF, etc.
      If you need PDF input, you’ll have to convert it to an image f'
  - name: Why Not Use `Recognize` (Sync)?
    text: The synchronous version would block the ASP.NET Core thread pool until the
      CPU‑intensive OCR finishes. On a busy server that quickly becomes a bottleneck,
      leading to 504 timeouts. The async variant keeps the API snappy.
  type: HowTo
tags:
- ASP.NET Core
- OCR
- Aspose.OCR
title: Mengenali teks dari gambar di ASP.NET Core – unggah untuk OCR
url: /id/net/ocr-optimization/recognize-text-from-image-in-asp-net-core-upload-for-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Mengenali Teks dari Gambar di ASP.NET Core – Tutorial Lengkap

Pernah membutuhkan untuk **mengenali teks dari gambar** di dalam sebuah web API dan tidak yakin harus mulai dari mana? Anda tidak sendirian. Dalam banyak proyek—pikirkan pemindai faktur, pelacak kwitansi, atau bahkan fitur sederhana “baca‑saya”—mendapatkan hasil OCR yang dapat diandalkan adalah keterampilan yang wajib dimiliki.

Dalam panduan ini kami akan membahas contoh lengkap yang siap dijalankan yang menunjukkan cara **mengunggah gambar untuk OCR**, mengubah unggahan tersebut menjadi **ocr image from stream**, dan akhirnya mengembalikan teks yang diekstrak sebagai JSON bersih. Tanpa bagian yang hilang, tanpa referensi yang samar—hanya solusi mandiri yang dapat Anda masukkan ke dalam proyek ASP.NET Core mana pun hari ini.

## Apa yang Akan Anda Dapatkan

- Sebuah `OcrController` yang berfungsi penuh dan menerima unggahan multipart form.  
- Penjelasan langkah‑demi‑langkah setiap baris, sehingga Anda memahami *mengapa* kami melakukan apa yang kami lakukan.  
- Tips untuk menangani file besar, menghindari pemblokiran thread, dan menjaga API Anda tetap responsif.  
- Sekilas tentang cara memperluas solusi (banyak bahasa, pra‑pemrosesan gambar, dll.).  

**Prasyarat**: .NET 6 atau lebih baru, Visual Studio 2022 (atau VS Code), dan lisensi Aspose.OCR (versi percobaan gratis dapat digunakan untuk pengujian). Jika Anda sudah memiliki semuanya, mari kita mulai.

![diagram alur mengenali teks dari gambar](https://example.com/ocr-workflow.png "alur mengenali teks dari gambar")

## Cara Mengenali Teks dari Gambar di ASP.NET Core

Inti dari solusi ini berada dalam satu controller. Di bawah ini adalah **kode lengkap yang dapat dijalankan**; setiap impor, setiap direktif `using`, dan setiap panggilan async disertakan sehingga Anda dapat menyalin‑tempelnya langsung ke dalam proyek ASP.NET Core Web API baru.

```csharp
using Aspose.OCR;
using Microsoft.AspNetCore.Mvc;
using System.Threading.Tasks;

[ApiController]
[Route("api/ocr")]
public class OcrController : ControllerBase
{
    // Step 1: Create a reusable OCR engine instance
    // Reusing the same OcrEngine across requests saves memory and speeds up init.
    private readonly OcrEngine _ocrEngine = new OcrEngine();

    // Step 2: Define the endpoint that accepts a file upload
    [HttpPost("recognize")]
    public async Task<IActionResult> Recognize([FromForm] IFormFile uploadedFile)
    {
        // Guard clause – make sure we actually got a file
        if (uploadedFile == null || uploadedFile.Length == 0)
            return BadRequest(new { error = "No file uploaded." });

        // Step 3: Open the uploaded file as a read‑only stream
        // This is the **ocr image from stream** part.
        await using var imageStream = uploadedFile.OpenReadStream();

        // Step 4: Load the image asynchronously for OCR processing
        // Aspose.OCR provides FromStreamAsync which off‑loads the I/O work.
        var ocrImage = await OcrImage.FromStreamAsync(imageStream);

        // Step 5: Run OCR recognition without blocking the request thread
        // RecognizeAsync runs the heavy lifting on a background thread.
        var ocrResult = await _ocrEngine.RecognizeAsync(ocrImage);

        // Step 6: Return the extracted text as a JSON response
        return Ok(new { text = ocrResult.Text });
    }
}
```

### Mengapa Pola Ini Berfungsi

- **Single `OcrEngine` instance**: Membuat instance engine sekali menghindari beban memuat data bahasa pada setiap permintaan.  
- **Async everything**: Dengan menggunakan `await` pada `FromStreamAsync` dan `RecognizeAsync`, thread pool ASP.NET Core tetap bebas melayani pemanggil lain.  
- `IFormFile` binding: Atribut `[FromForm]` memungkinkan klien cukup melakukan POST permintaan multipart/form‑data—tepat seperti yang sudah diketahui oleh browser dan alat seperti Postman.  

Sekarang kode berada di depan Anda, mari kita uraikan setiap bagian logis.

## Unggah Gambar untuk OCR – Menangani Permintaan Multipart

Ketika klien mengirimkan file, ASP.NET Core mengikatnya ke `IFormFile`. Objek ini memberi kami pegangan aman ke byte mentah tanpa memuat seluruh file ke memori sekaligus.

```csharp
[HttpPost("recognize")]
public async Task<IActionResult> Recognize([FromForm] IFormFile uploadedFile)
{
    if (uploadedFile == null || uploadedFile.Length == 0)
        return BadRequest(new { error = "No file uploaded." });

    // …
}
```

**Tips Pro**: Jika Anda mengharapkan gambar berukuran besar (misalnya >10 MB), pertimbangkan menambahkan pemeriksaan ukuran di sini dan mengembalikan 413 Payload Too Large. Ini melindungi server Anda dari crash OOM yang tidak disengaja.

## Proses OCR Image dari Stream Secara Asinkron

Baris `await OcrImage.FromStreamAsync(imageStream)` melakukan pekerjaan berat dalam mendekode byte gambar ke format yang dapat dipahami Aspose.OCR. Karena bersifat async, I/O yang mendasarinya (disk atau jaringan) tidak akan memblokir thread permintaan.

```csharp
await using var imageStream = uploadedFile.OpenReadStream();
var ocrImage = await OcrImage.FromStreamAsync(imageStream);
```

### Kasus Pinggir yang Perlu Diwaspadai

- **Corrupt files**: Jika file yang diunggah bukan gambar yang valid, `FromStreamAsync` akan melemparkan pengecualian. Bungkus panggilan tersebut dalam try/catch jika Anda memerlukan pesan error yang elegan.  
- **Unsupported formats**: Aspose mendukung PNG, JPEG, BMP, TIFF, dll. Jika Anda memerlukan input PDF, Anda harus mengonversinya ke gambar terlebih dahulu (Aspose.PDF dapat membantu).

## Jalankan OCR Engine Tanpa Memblokir

`_ocrEngine.RecognizeAsync(ocrImage)` menjalankan algoritma OCR pada thread latar belakang. Inilah saat operasi **mengenali teks dari gambar** benar‑benar terjadi.

```csharp
var ocrResult = await _ocrEngine.RecognizeAsync(ocrImage);
```

`ocrResult` yang dikembalikan berisi properti `Text` dengan string mentah yang diekstrak. Anda dapat memprosesnya lebih lanjut (memangkas spasi, memperbaiki kesalahan OCR umum, dll.) sebelum mengirimkannya kembali.

### Mengapa Tidak Menggunakan `Recognize` (Sinkron)?

Versi sinkron akan memblokir thread pool ASP.NET Core hingga OCR yang intensif CPU selesai. Pada server yang sibuk, hal ini cepat menjadi bottleneck, menyebabkan timeout 504. Varian async menjaga API tetap responsif.

## Kembalikan JSON Bersih – Bagian Akhir

```csharp
return Ok(new { text = ocrResult.Text });
```

Klien menerima payload JSON yang rapi:

```json
{
  "text": "Sample extracted text from the uploaded image."
}
```

Jika Anda memerlukan metadata tambahan—skor kepercayaan, deteksi bahasa, kotak pembatas—cukup perluas objek anonim atau definisikan DTO yang tepat.

## Menguji Endpoint

Anda dapat memverifikasi semuanya berfungsi dengan **cURL**, **Postman**, atau bahkan formulir HTML sederhana.

```bash
curl -X POST https://localhost:5001/api/ocr/recognize \
     -F "uploadedFile=@/path/to/your/image.png"
```

Respons berhasil terlihat seperti:

```
{"text":"Hello World"}
```

Jika Anda lupa mengirim file, Anda akan mendapatkan:

```
{"error":"No file uploaded."}
```

## Melangkah Lebih Jauh – Peningkatan Umum

| Peningkatan | Mengapa Membantu | Contoh Kode Cepat |
|------------|------------------|-------------------|
| **Pemilihan bahasa** | Akurasi OCR meningkat ketika Anda memberi tahu engine bahasa yang diharapkan. | `_ocrEngine.Language = OcrLanguage.English;` |
| **Pra‑pemrosesan gambar** | Penyesuaian kecerahan/kontras dapat menyelamatkan pemindaian ber kualitas rendah. | `ocrImage = OcrImage.FromBitmap(ImageProcessor`


## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Cara Melakukan Ekstraksi Teks Gambar dari Stream Menggunakan Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [Ekstrak Teks dari Gambar – Optimasi OCR dengan Aspose.OCR untuk .NET](/ocr/english/net/ocr-optimization/)
- [Ekstrak teks gambar C# dengan pemilihan bahasa menggunakan Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}