---
category: general
date: 2026-02-19
description: tutorial c# ocr yang menunjukkan cara mengekstrak teks dari gambar, mengenali
  teks dari jpg, dan mengonversi gambar menjadi teks dengan pustaka Aspose OCR.
draft: false
keywords:
- c# ocr tutorial
- extract text from image
- recognize text from jpg
- convert image to text
- extract text from jpg
language: id
og_description: tutorial OCR c# yang memandu Anda melalui ekstraksi teks dari gambar,
  mengenali teks dari jpg, dan mengonversi gambar menjadi teks menggunakan Aspose
  OCR.
og_title: tutorial OCR c# – Ekstrak Teks dari Gambar dengan Aspose OCR
tags:
- OCR
- C#
- Aspose
title: Tutorial OCR C# – Ekstrak Teks dari Gambar Menggunakan Aspose OCR
url: /id/net/text-recognition/c-ocr-tutorial-extract-text-from-image-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tutorial c# OCR – Ekstrak Teks dari Gambar dengan Aspose OCR

Pernah bertanya-tanya bagaimana cara **extract text from image** file tanpa membuat rambut Anda rontok? Dalam banyak aplikasi dunia nyata Anda perlu membaca faktur yang dipindai, mengambil nomor seri dari foto, atau sekadar mengubah JPG menjadi teks yang dapat dicari. **c# ocr tutorial** ini menunjukkan secara tepat cara melakukannya, menggunakan library Aspose OCR, dan bahkan membahas perbedaan halus antara *recognize text from jpg* dan *convert image to text*.

Dalam panduan ini Anda akan belajar cara menyiapkan paket NuGet Aspose OCR, menulis program console kecil yang membaca gambar, dan menangani jebakan paling umum (seperti format gambar yang tidak didukung atau pengaturan bahasa). Pada akhirnya Anda akan memiliki potongan kode yang dapat Anda masukkan ke proyek .NET mana pun dan mulai **extracting text from jpg** file dalam hitungan detik.

## Apa yang Anda Butuhkan

Sebelum kita mulai, pastikan Anda memiliki hal‑hal berikut siap:

| Prerequisite | Why it matters |
|--------------|----------------|
| .NET 6 SDK (or later) | Fitur C# modern dan kinerja yang lebih baik |
| Visual Studio 2022 or VS Code | Pengalaman pengeditan yang nyaman |
| An image file (`sample.jpg`) you want to process | Sumber sebenarnya untuk mesin OCR kami |
| Internet access to pull the Aspose.OCR NuGet package | Perpustakaan tidak built‑in, kita perlu mengunduhnya |

Jika ada yang terdengar asing, jangan panik – langkah‑langkah di bawah ini akan memandu Anda melalui setiap bagian, dan kode dapat berjalan bahkan pada editor teks biasa ditambah `dotnet` CLI.

## Langkah 1: Instal Paket NuGet Aspose.OCR

Pertama-tama, kita harus membawa mesin OCR ke dalam proyek kita. Buka terminal di folder proyek Anda dan jalankan:

```bash
dotnet add package Aspose.OCR
```

> **Pro tip:** Jika Anda menggunakan Visual Studio, Anda juga dapat klik kanan proyek → *Manage NuGet Packages* → cari “Aspose.OCR” dan tekan *Install*.

Perintah ini mengunduh versi stabil terbaru (per Februari 2026 versi 23.3) dan menambahkan referensi ke `.csproj` Anda. Tidak ada DLL tambahan yang perlu disalin—semua ditangani oleh runtime .NET.

## Langkah 2: Buat Kerangka Aplikasi Console Sederhana

Sekarang mari buat aplikasi console minimal yang akan menampung logika OCR kami. Buat file bernama `Program.cs` (atau ganti yang sudah ada) dan tempelkan kerangka berikut:

```csharp
using System;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll call the OCR routine from here.
            Console.WriteLine("Starting c# OCR tutorial...");
        }
    }
}
```

Perhatikan `using System;` di bagian atas – kita akan membutuhkannya untuk output console dan untuk menangani kemungkinan pengecualian nanti.

## Langkah 3: Inisialisasi Mesin OCR dan Atur Bahasa

Aspose OCR mendukung puluhan bahasa, tetapi untuk kebanyakan demo Bahasa Inggris sudah cukup. Mesin ini ringan, sehingga kita dapat menginstansiasinya langsung di dalam `Main`. Tambahkan kode berikut **setelah** `Console.WriteLine` pengantar:

```csharp
using Aspose.OCR;   // <-- add this using directive at the top of the file

// ...

// Step 3: Create an OCR engine and configure it for English
var ocrEngine = new OcrEngine
{
    Language = Language.English   // you can switch to Language.Spanish, etc.
};
```

Mengapa kita mengatur bahasa secara eksplisit? Karena algoritma pengenalan yang mendasarinya menggunakan kamus khusus bahasa untuk meningkatkan akurasi. Melewatkan langkah ini mungkin masih berfungsi, tetapi Anda sering akan mendapatkan hasil yang kacau pada teks non‑English.

## Langkah 4: Kenali Teks dari Gambar JPG

Berikut inti tutorial – memasukkan file gambar ke mesin dan mengambil hasil teks. Sisipkan kode di bawah ini tepat setelah inisialisasi mesin:

```csharp
// Step 4: Define the path to the image you want to process
string imagePath = @"YOUR_DIRECTORY/sample.jpg";   // <-- replace with your actual path

try
{
    // Recognize the image. This method returns an OcrResult object.
    OcrResult ocrResult = ocrEngine.RecognizeImage(imagePath);

    // Display the raw OCR output in the console
    Console.WriteLine("\n--- OCR Output ---");
    Console.WriteLine(ocrResult.Text);
}
catch (Exception ex)
{
    // If something goes wrong (file not found, unsupported format, etc.)
    Console.Error.WriteLine($"Error during OCR: {ex.Message}");
}
```

Beberapa hal yang perlu dicatat:

* **`RecognizeImage`** bekerja dengan sebagian besar format raster umum – JPEG, PNG, BMP, TIFF. Itulah mengapa tutorial ini dapat *recognize text from jpg* tanpa langkah konversi tambahan.
* Metode ini mengembalikan objek `OcrResult` yang berisi `Text`, `Confidence`, dan bahkan `BoundingBoxes` jika Anda membutuhkan data lokasi nanti.
* Membungkus pemanggilan dalam `try/catch` membuat program lebih tahan banting – file yang hilang tidak lagi menyebabkan seluruh aplikasi crash.

## Langkah 5: Jalankan Aplikasi dan Verifikasi Output

Simpan file, kembali ke terminal Anda, dan jalankan:

```bash
dotnet run
```

Anda akan melihat sesuatu seperti:

```
Starting c# OCR tutorial...

--- OCR Output ---
Hello, world!
This is a sample image containing text.
```

Jika console mencetak teks persis yang muncul di `sample.jpg`, selamat! Anda baru saja **converted image to text** menggunakan beberapa baris kode C#.

### Bagaimana Jika Output Terlihat Aneh?

* **Low confidence:** Coba tingkatkan resolusi gambar atau terapkan pra‑pemrosesan (mis., penajaman, binarisasi). Aspose OCR memiliki metode `PreprocessImage` yang dapat Anda jelajahi.
* **Wrong language:** Periksa kembali bahwa `ocrEngine.Language` cocok dengan bahasa gambar sumber.
* **Unsupported format:** Pastikan ekstensi file benar‑benar JPEG; terkadang PNG yang disimpan dengan ekstensi `.jpg` membingungkan parser.

## Langkah 6: Mengemas Contoh Lengkap untuk Digunakan Kembali

Di bawah ini adalah **program lengkap yang dapat dijalankan** yang dapat Anda salin‑tempel ke proyek console baru mana pun. Program ini mencakup semua pernyataan `using` yang diperlukan, penanganan pengecualian, dan komentar yang menjelaskan setiap baris.

```csharp
// Program.cs
using System;
using Aspose.OCR;   // Aspose OCR library

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("=== c# OCR Tutorial – Extract Text from Image ===");

            // 1️⃣ Create OCR engine and set language (English by default)
            var ocrEngine = new OcrEngine
            {
                Language = Language.English
            };

            // 2️⃣ Path to the image you want to process
            string imagePath = @"YOUR_DIRECTORY/sample.jpg"; // <-- update this

            try
            {
                // 3️⃣ Perform OCR – this both *recognizes text from jpg* and *extracts text from image*
                OcrResult result = ocrEngine.RecognizeImage(imagePath);

                // 4️⃣ Output the recognized string – you’ve now *converted image to text*
                Console.WriteLine("\n--- OCR Result ---");
                Console.WriteLine(result.Text);
            }
            catch (Exception ex)
            {
                // Friendly error message – helps when the file is missing or corrupted
                Console.Error.WriteLine($"Oops! Something went wrong: {ex.Message}");
            }

            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

Simpan ini sebagai `Program.cs`, jalankan `dotnet run`, dan Anda akan melihat demonstrasi langsung **extract text from jpg** dalam aksi.

## Bonus: Mengekstrak Teks dari Beberapa Gambar dalam Folder

Seringkali Anda perlu memproses batch seluruh direktori pemindaian. Berikut ekstensi cepat yang mengulangi setiap file `.jpg` dalam folder, menjalankan OCR, dan menulis setiap hasil ke file `.txt` dengan nama dasar yang sama.

```csharp
using System.IO;

// ...

string folderPath = @"YOUR_DIRECTORY"; // folder containing many jpg files

foreach (string file in Directory.GetFiles(folderPath, "*.jpg"))
{
    try
    {
        OcrResult batchResult = ocrEngine.RecognizeImage(file);
        string txtPath = Path.ChangeExtension(file, ".txt");
        File.WriteAllText(txtPath, batchResult.Text);
        Console.WriteLine($"Processed {Path.GetFileName(file)} → {Path.GetFileName(txtPath)}");
    }
    catch (Exception ex)
    {
        Console.Error.WriteLine($"Failed on {Path.GetFileName(file)}: {ex.Message}");
    }
}
```

Potongan kode ini menunjukkan skenario dunia nyata di mana Anda *extract text from image* file secara skala, kebutuhan umum untuk sistem manajemen dokumen.

## Ilustrasi Gambar (Opsional)

Jika Anda ingin petunjuk visual dalam artikel, Anda dapat menyisipkan screenshot output console:

![output console tutorial c# OCR yang menampilkan teks yang diekstrak](/images/ocr-console.png)

*Teks alt mencakup kata kunci utama untuk memenuhi SEO.*

## Pertanyaan Umum & Kasus Tepi

**Q: Apakah ini bekerja pada PDF?**  
A: Tidak secara langsung. Anda harus terlebih dahulu meraster setiap halaman PDF menjadi gambar (mis., menggunakan Aspose.PDF) dan kemudian memberi gambar tersebut ke mesin OCR.

**Q: Bagaimana dengan tulisan tangan?**  
A: Aspose OCR fokus pada teks cetak. Untuk tulisan kursif atau catatan tulisan tangan Anda memerlukan model khusus (mis., Azure Cognitive Services atau Google Vision).

**Q: Bisakah saya mengubah encoding output?**  
A: `OcrResult.Text` adalah `string` .NET, yang secara default UTF‑16, sehingga Anda dapat menuliskannya ke encoding file apa pun yang Anda inginkan menggunakan `File.WriteAllText(path, text, Encoding.UTF8)`.

**Q: Apakah perpustakaan ini gratis?**  
A: Aspose menawarkan mode evaluasi penuh fungsi dengan watermark. Untuk produksi Anda memerlukan lisensi, tetapi penggunaan API tetap sama.

## Kesimpulan

Anda baru saja menyelesaikan **c# OCR tutorial** yang memandu Anda melalui instalasi Aspose OCR, inisialisasi mesin, dan **extracting text from image** file—termasuk JPEG—sehingga Anda dapat *convert

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}