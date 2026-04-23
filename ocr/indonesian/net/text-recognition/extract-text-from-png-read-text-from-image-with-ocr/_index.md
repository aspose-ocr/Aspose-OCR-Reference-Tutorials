---
category: general
date: 2026-03-17
description: Ekstrak teks dari PNG menggunakan Aspose OCR di C#. Pelajari cara membaca
  teks dari gambar, memproses OCR struk, dan membuat mesin OCR dengan percepatan GPU.
draft: false
keywords:
- extract text from png
- read text from image
- ocr receipt image
- process receipt ocr
- create ocr engine
language: id
og_description: Ekstrak teks dari PNG menggunakan Aspose OCR. Panduan ini menunjukkan
  cara membaca teks dari gambar, memproses OCR struk, dan membuat mesin OCR secara
  efisien.
og_title: Ekstrak Teks dari PNG – Baca Teks dari Gambar dengan OCR
tags:
- OCR
- CSharp
- Aspose
title: Ekstrak Teks dari PNG – Baca Teks dari Gambar dengan OCR
url: /id/net/text-recognition/extract-text-from-png-read-text-from-image-with-ocr/
---

"## Langkah 1: Instal Aspose.OCR dan Siapkan Proyek". Keep colon.

Proceed.

Let's craft final output.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ekstrak Teks dari PNG – Baca Teks dari Gambar dengan OCR

Pernah perlu **mengekstrak teks dari PNG** tetapi tidak yakin perpustakaan mana yang memberikan hasil yang dapat diandalkan? Anda bukan satu‑satunya—para pengembang terus bertanya, “Bagaimana cara membaca teks dari file gambar seperti kwitansi tanpa menulis jaringan saraf khusus?” Kabar baiknya, Aspose OCR melakukan pekerjaan berat untuk Anda, dan Anda bahkan dapat mengaktifkan GPU untuk meningkatkan kecepatan.

Dalam tutorial ini kami akan membahas semua yang Anda perlukan untuk **memproses OCR kwitansi**, mulai dari menginstal paket NuGet hingga membuat mesin OCR yang memahami file PNG Anda. Pada akhir tutorial Anda akan memiliki aplikasi konsol mandiri yang membaca gambar kwitansi, mencetak teks yang dikenali, dan menunjukkan cara menyesuaikan mesin untuk berbagai skenario. Tanpa dokumentasi eksternal, hanya kode murni dan penjelasan yang jelas.

## Prasyarat

- .NET 6.0 SDK (atau versi .NET terbaru)  
- Visual Studio 2022 atau VS Code dengan ekstensi C#  
- GPU NVIDIA yang didukung dengan driver terbaru (opsional, tetapi disarankan untuk mode GPU)  
- Paket NuGet **Aspose.OCR** (`dotnet add package Aspose.OCR`)  

Jika Anda tidak memiliki GPU, Anda masih dapat menjalankan contoh dalam mode CPU—cukup lewati baris konfigurasi GPU.

## Langkah 1: Instal Aspose.OCR dan Siapkan Proyek

Pertama, buat proyek konsol baru dan tambahkan pustaka Aspose OCR.

```bash
dotnet new console -n ReceiptOcrDemo
cd ReceiptOcrDemo
dotnet add package Aspose.OCR
```

Mengapa ini penting: paket `Aspose.OCR` menyertakan mesin OCR, pemuat gambar, dan dukungan GPU opsional. Menambahkannya melalui NuGet memastikan Anda mendapatkan versi stabil terbaru (pada Maret 2026 versi 23.10).

## Langkah 2: Impor Namespace dan Buat Mesin OCR

Sekarang buka **Program.cs** dan tambahkan `using` yang diperlukan. Kemudian buat instance mesin.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 2: Create an OCR engine instance
            var ocrEngine = new OcrEngine();

            // Optional: Enable GPU acceleration if a compatible GPU is present
            // This dramatically speeds up processing of high‑resolution PNGs
            ocrEngine.Config.EngineMode = EngineMode.Gpu;   // <-- primary way to "process receipt ocr" fast
            ocrEngine.Config.GpuDeviceId = 0; // selects the first GPU in the system

            // The rest of the code follows...
```

**Tips profesional:** Jika Anda menemui `System.DllNotFoundException` pada mesin tanpa GPU, cukup beri komentar pada dua baris yang mengatur `EngineMode` dan `GpuDeviceId`. Mesin akan otomatis beralih ke CPU.

## Langkah 3: Muat Gambar PNG yang Ingin Anda Ekstrak Teksnya

Aspose OCR dapat membaca gambar langsung dari jalur file, stream, atau bahkan array byte. Untuk demo ini kami akan memuat gambar kwitansi lokal.

```csharp
            // Step 3: Load the image (replace the path with your own PNG file)
            string imagePath = @"C:\Images\receipt.png";

            // Validate the file exists to avoid runtime surprises
            if (!System.IO.File.Exists(imagePath))
            {
                Console.WriteLine($"Error: File not found – {imagePath}");
                return;
            }

            // Load the image into the engine
            ocrEngine.Image = ImageStream.FromFile(imagePath);
```

Perhatikan bagaimana kami memeriksa keberadaan file. Pada aplikasi dunia nyata Anda mungkin menampilkan pesan UI yang ramah alih‑alih hanya keluar.

## Langkah 4: Lakukan Pengakuan OCR

Ekstraksi teks sebenarnya terjadi dengan satu pemanggilan metode. Mesin mengembalikan objek `OcrResult` yang berisi string mentah, skor kepercayaan, dan informasi tata letak.

```csharp
            // Step 4: Run the OCR process
            OcrResult ocrResult = ocrEngine.Recognize();

            // Check if the engine succeeded
            if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
            {
                Console.WriteLine("No text could be recognized.");
                return;
            }
```

Mengapa kami memeriksa `ocrResult.Text`: terkadang PNG beresolusi rendah menghasilkan string kosong, dan lebih baik memberi tahu pengguna daripada tidak menghasilkan apa‑apa secara diam‑diam.

## Langkah 5: Tampilkan Teks yang Dikenali

Akhirnya, cetak string yang diekstrak ke konsol. Anda juga dapat menuliskannya ke file, basis data, atau mengirimkannya ke layanan lain.

```csharp
            // Step 5: Display the recognized text
            Console.WriteLine("=== Extracted Text from PNG ===");
            Console.WriteLine(ocrResult.Text);
            Console.WriteLine("=== End of Output ===");
        }
    }
}
```

Saat Anda menjalankan program (`dotnet run`), Anda akan melihat sesuatu seperti:

```
=== Extracted Text from PNG ===
Store: Coffee Corner
Date: 03/15/2026
Item      Qty   Price
Latte      2    $5.40
Muffin     1    $2.30
Total            $7.70
=== End of Output ===
```

Itulah **solusi lengkap untuk mengekstrak teks dari file PNG** dengan Aspose OCR, dan Anda baru saja belajar cara **membaca teks dari gambar** yang tampak seperti kwitansi.

## Opsional: Penyetelan Halus Mesin OCR (Lanjutan)

Jika Anda memerlukan akurasi lebih tinggi untuk font tertentu atau latar belakang berisik, pertimbangkan menyesuaikan pengaturan berikut:

```csharp
// Enable language detection (default is English)
ocrEngine.Config.Language = Language.English;

// Turn on automatic image preprocessing (deskew, binarization)
ocrEngine.Config.EnableImagePreprocessing = true;

// Set a confidence threshold if you only want high‑certainty results
ocrEngine.Config.ConfidenceThreshold = 0.75f;
```

Penyesuaian ini sangat berguna ketika Anda **memproses OCR kwitansi** dalam pekerjaan batch di mana beberapa pemindaian tidak sempurna.

## Kesalahan Umum & Cara Menghindarinya

| Masalah | Mengapa Terjadi | Solusi |
|---------|----------------|--------|
| **Driver GPU tidak ada** | Mesin mencoba memuat CUDA tetapi tidak menemukan DLL. | Instal driver NVIDIA terbaru atau beralih ke mode CPU dengan menghapus baris `EngineMode.Gpu`. |
| **Jalur gambar salah** | `ImageStream.FromFile` melempar jika file tidak ditemukan. | Selalu validasi jalur (lihat Langkah 3) atau gunakan `Path.Combine` untuk keamanan lintas‑platform. |
| **Kepercayaan rendah pada kwitansi blur** | Mesin OCR tidak dapat membedakan karakter. | Aktifkan `EnableImagePreprocessing` dan opsional tingkatkan DPI gambar sebelum memberi ke mesin. |
| **Kebocoran memori pada layanan yang berjalan lama** | Setiap `OcrEngine` menyimpan sumber daya tidak terkelola. | Buang mesin setelah selesai: `using var ocrEngine = new OcrEngine();` |

## Contoh Lengkap yang Dapat Dijalankan (Copy‑Paste)

Berikut adalah **seluruh program** yang dapat Anda tempelkan ke `Program.cs`. Ia mencakup semua penyesuaian opsional yang dikomentari untuk aktivasi mudah.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Create OCR engine
            using var ocrEngine = new OcrEngine();

            // Enable GPU acceleration if you have a supported card
            ocrEngine.Config.EngineMode = EngineMode.Gpu;
            ocrEngine.Config.GpuDeviceId = 0;

            // Optional fine‑tuning (uncomment as needed)
            //ocrEngine.Config.Language = Language.English;
            //ocrEngine.Config.EnableImagePreprocessing = true;
            //ocrEngine.Config.ConfidenceThreshold = 0.75f;

            // Load PNG image
            string imagePath = @"C:\Images\receipt.png";
            if (!System.IO.File.Exists(imagePath))
            {
                Console.WriteLine($"Error: File not found – {imagePath}");
                return;
            }
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // Perform OCR
            OcrResult ocrResult = ocrEngine.Recognize();

            // Verify result
            if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
            {
                Console.WriteLine("No text could be recognized.");
                return;
            }

            // Output the extracted text
            Console.WriteLine("=== Extracted Text from PNG ===");
            Console.WriteLine(ocrResult.Text);
            Console.WriteLine("=== End of Output ===");
        }
    }
}
```

Simpan, jalankan `dotnet run`, dan Anda akan melihat isi kwitansi tercetak di konsol.

![contoh ekstrak teks dari png](receipt.png "contoh ekstrak teks dari png")

*Gambar di atas menunjukkan contoh PNG kwitansi yang dapat diproses oleh kode.*

## Ringkasan

Kami telah membahas cara **mengekstrak teks dari PNG** menggunakan Aspose OCR, mendemonstrasikan cara **membaca teks dari gambar**, dan menelusuri pipeline **memproses OCR kwitansi** lengkap yang mencakup akselerasi GPU opsional. Dengan **membuat mesin OCR** sendiri, Anda memperoleh kontrol penuh atas konfigurasi, kinerja, dan penanganan kesalahan.

## Apa yang Bisa Dijelajahi Selanjutnya?

- **Pemrosesan batch**: Loop melalui direktori berisi kwitansi PNG dan tulis setiap hasil ke file CSV.  
- **Integrasi dengan Azure Functions**: Ubah aplikasi konsol ini menjadi endpoint serverless yang menerima unggahan gambar.  
- **Dukungan multi‑bahasa**: Ganti `Language.English` dengan `Language.Spanish` atau tambahkan kamus khusus.  
- **Pasca‑pemrosesan**: Gunakan ekspresi reguler untuk mengekstrak bidang seperti total, tanggal, atau NPWP dari string OCR mentah.

Silakan bereksperimen—OCR adalah alat yang sangat fleksibel begitu Anda mengetahui pengaturan yang tepat. Jika mengalami kendala, tinggalkan komentar di bawah atau periksa referensi API Aspose OCR untuk penjelasan lebih mendalam.

Selamat coding, dan nikmati mengubah kwitansi PNG yang membandel menjadi teks yang dapat dicari!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}