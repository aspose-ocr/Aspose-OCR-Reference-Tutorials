---
category: general
date: 2026-06-03
description: Dapatkan versi Aspose OCR di C# dengan potongan kode sederhana. Pelajari
  cara mengambil versi perpustakaan Aspose OCR menggunakan OcrEngine GetVersion.
draft: false
keywords:
- get aspose ocr version
- aspose ocr library
- ocrengine getversion
- c# ocr example
- retrieve aspose version
language: id
og_description: Dapatkan versi Aspose OCR di C# dengan cepat. Tutorial ini menunjukkan
  secara tepat cara mengambil versi perpustakaan Aspose OCR menggunakan OcrEngine
  GetVersion.
og_title: Dapatkan Versi Aspose OCR di C# – Panduan Lengkap
schemas:
- author: Aspose
  dateModified: '2026-06-03'
  description: Get Aspose OCR version in C# with a simple snippet. Learn how to retrieve
    the Aspose OCR library version using OcrEngine GetVersion.
  headline: Get Aspose OCR Version in C# – Complete Guide
  type: TechArticle
- description: Get Aspose OCR version in C# with a simple snippet. Learn how to retrieve
    the Aspose OCR library version using OcrEngine GetVersion.
  name: Get Aspose OCR Version in C# – Complete Guide
  steps:
  - name: Why this matters
    text: When you install the package, the assembly version on disk may differ from
      the version reported by the library at runtime. Querying the version via code
      ensures you’re reading the exact build that the CLR loaded, which is crucial
      for debugging and for compliance audits.
  - name: Expected output
    text: 'When you run `dotnet run` inside the project folder, you should see something
      similar to:'
  - name: What if `GetVersion()` returns an empty string?
    text: That usually signals a corrupted installation or a missing native dependency.
      Re‑install the NuGet package and verify that the `Aspose.OCR.Native.dll` (or
      the appropriate platform‑specific binary) sits alongside your executable.
  - name: Does the method work on .NET Core 2.0?
    text: Yes, **Aspose OCR** supports .NET Standard 2.0 and higher, so any .NET Core
      version that implements that standard can call `OcrEngine.GetVersion()`. Just
      make sure you reference the correct runtime identifiers (`win-x64`, `linux-x64`,
      etc.) if you’re publishing a self‑contained app.
  - name: Can I retrieve the version without a license file?
    text: Absolutely. `GetVersion()` does **not** require a license; it simply reports
      the library build number. However, if you attempt to perform OCR without a valid
      license, you’ll get a runtime exception. That’s why the `try/catch` in our snippet
      is valuable—it isolates the version check from the OCR exec
  type: HowTo
tags:
- Aspose
- OCR
- C#
- .NET
title: Dapatkan Versi Aspose OCR di C# – Panduan Lengkap
url: /id/net/ocr-configuration/get-aspose-ocr-version-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Dapatkan Versi Aspose OCR di C# – Panduan Lengkap

Pernah bertanya-tanya bagaimana cara **get Aspose OCR version** dari dalam proyek .NET Anda? Mungkin Anda sedang memecahkan masalah ketidakcocokan, atau Anda hanya ingin mencatat build perpustakaan yang tepat yang berjalan di produksi. Apa pun alasannya, Anda berada di tempat yang tepat.

Dalam tutorial ini kami akan membahas sebuah program C# kecil yang berdiri sendiri yang memanggil `OcrEngine.GetVersion()` dan mencetak hasilnya. Pada akhir tutorial Anda akan tahu tidak hanya *bagaimana* mengambil versi, tetapi juga *mengapa* memeriksa versi dapat menghindarkan Anda dari masalah saat memperbarui **Aspose OCR library**.

## Apa yang Akan Anda Pelajari

- Tambahkan paket NuGet Aspose.OCR ke proyek C#  
- Gunakan metode `OcrEngine.GetVersion()` (titik masuk **ocrengine getversion**)  
- Tangani kemungkinan pengecualian dan verifikasi output  
- Perluas potongan kode untuk skenario dunia nyata seperti pencatatan atau pengalihan fitur bersyarat  

Tidak diperlukan pengalaman sebelumnya dengan OCR—hanya pemahaman dasar tentang C# dan Visual Studio (atau IDE favorit Anda). Mari kita mulai.

---

## Langkah 1: Siapkan Proyek dan Tarik Perpustakaan Aspose OCR

Sebelum Anda dapat memanggil API terkait OCR apa pun, Anda perlu **Aspose OCR library** direferensikan dalam proyek Anda.

1. Buka terminal atau Package Manager Console di Visual Studio.  
2. Jalankan perintah berikut untuk menginstal versi stabil terbaru:

```bash
dotnet add package Aspose.OCR
```

> **Pro tip:** Jika Anda menargetkan .NET Framework alih-alih .NET Core, gunakan UI NuGet Package Manager dan pilih versi yang cocok dengan runtime Anda. Paket tersebut menyertakan kelas `OcrEngine` yang akan kami gunakan nanti.

### Mengapa ini penting

Saat Anda menginstal paket, versi assembly di disk mungkin berbeda dari versi yang dilaporkan oleh perpustakaan pada runtime. Menanyakan versi melalui kode memastikan Anda membaca build yang tepat yang dimuat CLR, yang penting untuk debugging dan audit kepatuhan.

## Langkah 2: Tulis Kode Minimal untuk **Get Aspose OCR Version**

Buat aplikasi konsol baru (`dotnet new console -n OcrVersionDemo`) dan ganti `Program.cs` default dengan yang berikut:

```csharp
using System;
using Aspose.OCR;

namespace OcrVersionDemo
{
    class Program
    {
        static void Main()
        {
            try
            {
                // Step 2a: Retrieve the Aspose OCR library version.
                // This is the core of the get aspose ocr version operation.
                string version = OcrEngine.GetVersion();   // e.g., "24.5.7"

                // Step 2b: Display the version information to the console.
                Console.WriteLine($"Aspose OCR version: {version}");
            }
            catch (Exception ex)
            {
                // If something goes wrong (missing DLL, license issue, etc.)
                Console.Error.WriteLine($"Failed to get Aspose OCR version: {ex.Message}");
            }
        }
    }
}
```

**Penjelasan setiap bagian**

- `using Aspose.OCR;` membawa namespace OCR ke dalam cakupan, memungkinkan kami memanggil `OcrEngine`.  
- `OcrEngine.GetVersion()` adalah metode statik **ocrengine getversion** yang mengembalikan string seperti `"24.5.7"`.  
- Membungkus pemanggilan dalam blok `try/catch` melindungi Anda dari kejutan runtime—mungkin binary native tidak ditemukan di mesin target.  
- String interpolasi `$"Aspose OCR version: {version}"` mencetak baris yang jelas dan dapat dibaca manusia.  

### Output yang Diharapkan

Saat Anda menjalankan `dotnet run` di dalam folder proyek, Anda harus melihat sesuatu yang mirip dengan:

```
Aspose OCR version: 24.5.7
```

Jika perpustakaan tidak dapat dimuat, cabang error akan mengeluarkan pesan singkat, membantu Anda mengidentifikasi masalah dengan cepat.

## Langkah 3: Verifikasi Versi Sesuai dengan Paket NuGet Anda

Mudah mengasumsikan versi NuGet yang Anda instal adalah yang digunakan pada runtime, tetapi keanehan lingkungan dapat mengganggu. Untuk memeriksa kembali:

```csharp
// After retrieving the version, compare it to the package metadata.
var assembly = typeof(OcrEngine).Assembly;
var fileVersion = System.Diagnostics.FileVersionInfo.GetVersionInfo(assembly.Location).FileVersion;

Console.WriteLine($"Assembly file version: {fileVersion}");
```

Menjalankan potongan tambahan ini akan mencetak sesuatu yang mirip dengan:

```
Assembly file version: 24.5.7.0
```

Jika kedua nilai berbeda, Anda mungkin memuat DLL lama dari Global Assembly Cache (GAC) atau dari folder build sebelumnya. Dalam kasus itu, bersihkan solusi Anda (`dotnet clean`) dan bangun kembali.

## Langkah 4: Masukkan Pemeriksaan Versi ke dalam Logging Produksi

Sebagian besar aplikasi dunia nyata tidak hanya mencetak ke konsol; mereka menulis ke file log atau sistem telemetri. Berikut contoh cepat menggunakan `Microsoft.Extensions.Logging`:

```csharp
using Microsoft.Extensions.Logging;
using Microsoft.Extensions.DependencyInjection;

// Set up a minimal logger.
var serviceProvider = new ServiceCollection()
    .AddLogging(builder => builder.AddConsole())
    .BuildServiceProvider();

var logger = serviceProvider.GetService<ILogger<Program>>();

try
{
    string version = OcrEngine.GetVersion();
    logger.LogInformation("Aspose OCR version: {Version}", version);
}
catch (Exception ex)
{
    logger.LogError(ex, "Unable to retrieve Aspose OCR version");
}
```

Sekarang versi muncul di log terstruktur Anda, memudahkan penyaringan berdasarkan `{Version}` nanti. Pola ini sangat berguna ketika Anda memiliki beberapa micro‑services yang masing‑masing menarik OCR DLL yang mungkin berbeda.

## Pertanyaan Umum & Kasus Tepi

### Bagaimana jika `GetVersion()` mengembalikan string kosong?

Itu biasanya menandakan instalasi yang rusak atau ketergantungan native yang hilang. Instal ulang paket NuGet dan pastikan `Aspose.OCR.Native.dll` (atau binary spesifik platform yang sesuai) berada di samping executable Anda.

### Apakah metode ini bekerja pada .NET Core 2.0?

Ya, **Aspose OCR** mendukung .NET Standard 2.0 dan lebih tinggi, jadi versi .NET Core apa pun yang mengimplementasikan standar tersebut dapat memanggil `OcrEngine.GetVersion()`. Pastikan Anda merujuk pada identifier runtime yang tepat (`win‑x64`, `linux‑x64`, dll.) jika Anda mempublikasikan aplikasi self‑contained.

### Bisakah saya mengambil versi tanpa file lisensi?

Tentu saja. `GetVersion()` **tidak** memerlukan lisensi; ia hanya melaporkan nomor build perpustakaan. Namun, jika Anda mencoba melakukan OCR tanpa lisensi yang valid, Anda akan mendapatkan pengecualian runtime. Itulah mengapa `try/catch` dalam potongan kode kami berharga—ia memisahkan pemeriksaan versi dari alur eksekusi OCR.

## Contoh Lengkap yang Berfungsi (Siap Salin‑Tempel)

Berikut seluruh program, siap dimasukkan ke dalam proyek konsol baru. Ini mencakup blok logging opsional, sehingga Anda dapat melihat output konsol dan log terstruktur secara bersamaan.

```csharp
using System;
using Aspose.OCR;
using Microsoft.Extensions.Logging;
using Microsoft.Extensions.DependencyInjection;

namespace OcrVersionDemo
{
    class Program
    {
        static void Main()
        {
            // Set up a simple console logger.
            var services = new ServiceCollection()
                .AddLogging(builder => builder.AddConsole())
                .BuildServiceProvider();

            var logger = services.GetService<ILogger<Program>>();

            try
            {
                // Retrieve the Aspose OCR library version.
                string version = OcrEngine.GetVersion();   // get aspose ocr version

                // Log and display the version.
                logger.LogInformation("Aspose OCR version: {Version}", version);
                Console.WriteLine($"Aspose OCR version: {version}");

                // Extra verification – compare with assembly file version.
                var assembly = typeof(OcrEngine).Assembly;
                var fileVersion = System.Diagnostics.FileVersionInfo
                    .GetVersionInfo(assembly.Location).FileVersion;
                logger.LogDebug("Assembly file version: {FileVersion}", fileVersion);
                Console.WriteLine($"Assembly file version: {fileVersion}");
            }
            catch (Exception ex)
            {
                logger.LogError(ex, "Failed to get Aspose OCR version");
                Console.Error.WriteLine($"Error: {ex.Message}");
            }
        }
    }
}
```

Jalankan dengan `dotnet run` dan Anda akan melihat dua baris yang mengonfirmasi versi, plus baris debug jika Anda mengaktifkan `LogLevel.Debug`.

## Kesimpulan

Kami telah membahas semua yang Anda perlukan untuk **get Aspose OCR version** di lingkungan C#—dari menginstal **Aspose OCR library**, memanggil metode **ocrengine getversion**, menangani kesalahan, hingga menyematkan hasil dalam logging tingkat produksi. Dengan pengetahuan ini, Anda kini dapat memverifikasi secara andal build OCR yang tepat yang digunakan aplikasi Anda, menghindari bug terkait versi, dan memenuhi persyaratan kepatuhan tanpa kesulitan.

Langkah selanjutnya? Coba gabungkan pemeriksaan versi ini dengan panggilan OCR sebenarnya (`OcrEngine` → `RecognizeImage`) dan catat baik versi maupun hasil pengenalan. Anda juga dapat menjelajahi pola **retrieve aspose version** untuk produk Aspose lainnya (PDF, Slides, Cells) agar seluruh suite Anda tetap sinkron.

Selamat coding, dan semoga pipeline OCR Anda tetap tajam!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan menjelajahi pendekatan implementasi alternatif dalam proyek Anda.

- [Cara Mendapatkan Hasil OCR dengan Aspose.OCR untuk .NET](/ocr/english/net/text-recognition/get-recognition-result/)
- [Ekstrak teks gambar C# dengan pemilihan bahasa menggunakan Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Cara Memproses Batch Gambar OCR dengan List di Aspose.OCR untuk .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}