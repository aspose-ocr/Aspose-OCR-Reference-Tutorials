---
category: general
date: 2026-03-05
description: Cara mendapatkan OCR dengan cepat menggunakan Aspose.OCR dan mengenali
  teks dari aliran dalam beberapa langkah sederhana. Pelajari kode C# lengkap serta
  tips untuk streaming data gambar.
draft: false
keywords:
- how to get OCR
- recognize text from stream
- Aspose OCR
- streaming OCR C#
- image chunk processing
language: id
og_description: Cara mendapatkan OCR di C# dan mengenali teks dari aliran menggunakan
  Aspose.OCR. Ikuti tutorial langkah demi langkah ini untuk solusi siap pakai.
og_title: Cara Mendapatkan OCR di C# – Panduan Lengkap Pengenalan Aliran
tags:
- OCR
- C#
- Aspose
title: Cara Mendapatkan OCR di C# – Mengenali Teks dari Stream
url: /id/net/text-recognition/how-to-get-ocr-in-c-recognize-text-from-stream/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Mendapatkan OCR di C# – Mengenali Teks dari Stream

Pernah bertanya-tanya **bagaimana cara mendapatkan OCR** yang berfungsi dalam aplikasi .NET tanpa harus menyimpan seluruh gambar ke disk terlebih dahulu? Anda tidak sendirian. Banyak pengembang perlu **mengenali teks dari stream**—misalnya saat memproses gambar yang datang melalui jaringan, umpan kamera, atau API penyimpanan cloud.  

Dalam tutorial ini kami akan membahas contoh lengkap yang siap dijalankan yang menunjukkan hal tersebut. Pada akhir tutorial Anda akan memiliki program C# yang berdiri sendiri yang membuat mesin Aspose OCR, mengalirkan potongan gambar ke dalamnya, dan mencetak teks yang diekstrak ke konsol. Tanpa alat eksternal yang misterius, hanya kode yang jelas dan beberapa tips praktis.

## Apa yang Akan Anda Pelajari

- Cara menginstal dan melisensikan library Aspose.OCR.
- Cara memasukkan data gambar potongan demi potongan menggunakan metode `AppendChunk`.
- Cara memulai dan menyelesaikan siklus pengenalan (`BeginRecognize` / `EndRecognize`).
- Cara menangani kasus tepi umum seperti potongan tidak lengkap atau kesalahan lisensi.
- Seperti apa outputnya dan cara memverifikasinya.

### Prasyarat

- .NET 6.0 atau lebih baru (kode ini juga bekerja dengan .NET Core dan .NET Framework).
- File lisensi Aspose OCR yang valid (`Aspose.OCR.lic`). Anda dapat memperoleh percobaan gratis dari situs web Aspose.
- Pemahaman dasar tentang C# dan `async`/`await` jika Anda ingin membaca dari stream asynchronous (contoh ini menggunakan stub sinkron untuk kejelasan).

> **Mengapa ini penting:** OCR streaming memungkinkan Anda menjaga penggunaan memori tetap rendah dan mengurangi latensi saat menangani gambar besar atau umpan video terus-menerus. Ini adalah pola yang akan Anda temui pada pemindai dokumen waktu nyata, aplikasi seluler, dan pipeline pemrosesan sisi server.

## Langkah 1: Siapkan Proyek dan Tambahkan Aspose.OCR

Pertama, buat proyek konsol baru dan tambahkan paket NuGet Aspose.OCR.

```bash
dotnet new console -n StreamOcrDemo
cd StreamOcrDemo
dotnet add package Aspose.OCR
```

> **Tips pro:** Jika Anda menggunakan Visual Studio, klik kanan proyek → *Manage NuGet Packages* → cari “Aspose.OCR” dan instal versi stabil terbaru.

Sekarang tambahkan file lisensi ke root proyek dan atur properti **Copy to Output Directory** menjadi **Copy always**. Ini memastikan file tersedia saat runtime.

```csharp
// Program.cs – top of the file
using System;
using System.IO;
using Aspose.OCR;
```

## Langkah 2: Inisialisasi Mesin OCR dan Terapkan Lisensi

Membuat mesin cukup sederhana, tetapi menerapkan lisensi **harus** dilakukan sebelum panggilan pengenalan apa pun; jika tidak, Anda akan terkena pembatasan mode percobaan.

```csharp
static OcrEngine InitializeOcrEngine()
{
    var engine = new OcrEngine();

    // Load the license – adjust the path if your file lives elsewhere
    string licensePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "Aspose.OCR.lic");
    if (!File.Exists(licensePath))
    {
        Console.Error.WriteLine("License file not found at " + licensePath);
        Environment.Exit(1);
    }

    engine.SetLicense(licensePath);
    return engine;
}
```

> **Mengapa kami melakukannya:** Menetapkan lisensi lebih awal menjamin semua panggilan API berikutnya berjalan dalam mode fitur penuh, menghindari watermark “versi evaluasi”.

## Langkah 3: Simulasikan Sumber Streaming

Dalam aplikasi nyata Anda akan membaca dari `NetworkStream`, `FileStream`, atau SDK kamera. Untuk demonstrasi, kami akan meniru sebuah stream dengan pembantu yang mengembalikan array byte yang mewakili potongan gambar JPEG.

```csharp
static byte[] GetNextChunk()
{
    // Replace this with your actual streaming logic.
    // Here we simply read the whole file and pretend it’s a single chunk.
    string sampleImagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "sample.jpg");
    if (!File.Exists(sampleImagePath))
    {
        Console.Error.WriteLine("Sample image not found at " + sampleImagePath);
        Environment.Exit(1);
    }

    return File.ReadAllBytes(sampleImagePath);
}
```

> **Catatan kasus tepi:** Jika Anda menerima banyak potongan kecil, Anda dapat memanggil `engine.Image.AppendChunk(chunk)` berulang kali sebelum mengakhiri pengenalan. Mesin akan menampung secara internal sampai memiliki cukup data untuk memulai pemrosesan.

## Langkah 4: Masukkan Data Gambar Potongan demi Potongan dan Jalankan OCR

Sekarang kita menggabungkan semuanya. Urutannya adalah:

1. `BeginRecognize()` – memberi tahu mesin bahwa kami akan memasukkan data.
2. `AppendChunk()` – menambahkan setiap array byte (Anda dapat melakukan loop pada banyak potongan).
3. `EndRecognize()` – menandakan bahwa potongan terakhir telah dikirim dan memicu pengenalan sebenarnya.

```csharp
static string PerformOcr(OcrEngine engine, byte[] imageChunk)
{
    // Start the recognition session
    engine.BeginRecognize();

    // Feed the image data. If you have multiple chunks, call this in a loop.
    engine.Image.AppendChunk(imageChunk);

    // End the session – the engine now processes the accumulated data.
    engine.EndRecognize();

    // Retrieve the result object; .Text holds the plain string.
    return engine.GetResult().Text;
}
```

## Langkah 5: Gabungkan Semua dalam `Main`

Berikut adalah metode `Main` lengkap yang menghubungkan semuanya, mencetak teks yang dikenali, dan membersihkan mesin dengan benar.

```csharp
static void Main(string[] args)
{
    // 1️⃣ Initialize OCR engine with license
    var ocrEngine = InitializeOcrEngine();

    try
    {
        // 2️⃣ Get a chunk of image data (replace with your streaming source)
        byte[] imageChunk = GetNextChunk();

        // 3️⃣ Run OCR on the streamed data
        string recognizedText = PerformOcr(ocrEngine, imageChunk);

        // 4️⃣ Output the result
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(recognizedText);
    }
    catch (Exception ex)
    {
        // Helpful error handling – you’ll often see OCR exceptions when the image is corrupted.
        Console.Error.WriteLine("OCR failed: " + ex.Message);
    }
    finally
    {
        // Release any native resources held by the engine.
        ocrEngine.Dispose();
    }
}
```

### Output yang Diharapkan

Jika `sample.jpg` berisi frasa “Hello, World!” Anda akan melihat:

```
=== Recognized Text ===
Hello, World!
```

Jika gambar buram atau potongan tidak lengkap, output mungkin kosong atau berisi karakter kacau – itulah mengapa penanganan potongan yang tepat (memastikan potongan terakhir dikirim) sangat penting.

## Menangani Banyak Potongan (Lanjutan)

Saat menangani data streaming yang sesungguhnya, Anda kemungkinan akan menerima banyak potongan kecil. Pola di bawah menunjukkan cara melakukan loop hingga sumber berakhir.

```csharp
static string OcrFromStream(OcrEngine engine, Stream source)
{
    engine.BeginRecognize();

    byte[] buffer = new byte[8192]; // 8 KB per read – adjust as needed
    int bytesRead;
    while ((bytesRead = source.Read(buffer, 0, buffer.Length)) > 0)
    {
        // If the last read returned fewer bytes, copy only that many.
        if (bytesRead < buffer.Length)
        {
            byte[] chunk = new byte[bytesRead];
            Array.Copy(buffer, chunk, bytesRead);
            engine.Image.AppendChunk(chunk);
        }
        else
        {
            engine.Image.AppendChunk(buffer);
        }
    }

    engine.EndRecognize();
    return engine.GetResult().Text;
}
```

> **Mengapa ini membantu:** Dengan streaming langsung dari `NetworkStream` atau `FileStream`, Anda tidak pernah memuat seluruh gambar ke memori, yang sangat menguntungkan untuk PDF besar atau foto beresolusi tinggi.

## Kesalahan Umum & Cara Menghindarinya

| Masalah | Gejala | Solusi |
|---------|--------|--------|
| Lisensi tidak ditemukan | `SetLicense` melempar `FileNotFoundException` | Verifikasi jalur dan atur *Copy to Output Directory* menjadi *Copy always*. |
| Hasil kosong | Tidak ada teks yang dicetak | Pastikan Anda memanggil `BeginRecognize` **sebelum** `AppendChunk` dan `EndRecognize` **setelah** potongan terakhir. |
| Kebocoran memori | Aplikasi melambat setelah banyak panggilan OCR | Dispose `OcrEngine` setelah setiap penggunaan atau gunakan kembali satu instance dengan pemanggilan `Dispose` yang tepat. |
| Potongan rusak | Karakter kacau | Validasi ukuran potongan; untuk JPEG/PNG beberapa byte pertama harus dimulai dengan `0xFF 0xD8` atau `0x89 0x50`. |

## Bonus: Menggunakan Stream Asynchronous

Jika sumber Anda adalah stream respons `HttpClient`, Anda dapat menyesuaikan loop untuk membaca dengan `await`:

```csharp
static async Task<string> OcrFromAsyncStream(OcrEngine engine, Stream asyncSource)
{
    engine.BeginRecognize();

    byte[] buffer = new byte[8192];
    int bytesRead;
    while ((bytesRead = await asyncSource.ReadAsync(buffer, 0, buffer.Length)) > 0)
    {
        if (bytesRead < buffer.Length)
        {
            var chunk = new byte[bytesRead];
            Array.Copy(buffer, chunk, bytesRead);
            engine.Image.AppendChunk(chunk);
        }
        else
        {
            engine.Image.AppendChunk(buffer);
        }
    }

    engine.EndRecognize();
    return engine.GetResult().Text;
}
```

Ini menjaga UI tetap responsif pada aplikasi desktop atau seluler dan memaksimalkan throughput pada server.

## Kesimpulan

Anda kini memiliki **solusi lengkap dan berdiri sendiri untuk cara mendapatkan OCR** di C# dan **mengenali teks dari stream** menggunakan Aspose.OCR. Tutorial ini mencakup semuanya mulai dari pelisensian dan inisialisasi hingga memasukkan potongan gambar, menangani kasus tepi, dan bahkan varian asynchronous.

Cobalah—ganti `sample.jpg` dengan umpan kamera langsung, gambar yang disimpan di cloud, atau unggahan HTTP multipart. Setelah Anda merasa nyaman, jelajahi fitur lanjutan seperti paket bahasa, pra‑pemrosesan khusus, atau pemrosesan batch dari banyak stream.

**Langkah selanjutnya:**  
- Coba OCR pada PDF dengan mengonversi setiap halaman menjadi gambar terlebih dahulu.  
- Eksperimen dengan `engine.Config` untuk meningkatkan akurasi pada font tertentu.  
- Gabungkan ini dengan Azure Functions atau AWS Lambda untuk pipeline ekstraksi teks tanpa server.

Selamat coding, semoga stream Anda selalu jernih dan hasil OCR Anda sempurna!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}