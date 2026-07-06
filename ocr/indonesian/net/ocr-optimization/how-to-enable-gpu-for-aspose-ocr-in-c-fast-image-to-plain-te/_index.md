---
category: general
date: 2026-02-24
description: Cara mengaktifkan GPU dalam contoh Aspose OCR C# – mengonversi gambar
  menjadi teks biasa dengan cepat. Termasuk cara mengatur ID perangkat GPU dan panduan
  membaca teks gambar dengan C#.
draft: false
keywords:
- how to enable gpu
- image to plain text
- aspose ocr example
- set gpu device id
- read image text c#
language: id
og_description: Cara mengaktifkan GPU dalam contoh Aspose OCR C#. Pelajari cara mengatur
  ID perangkat GPU dan membaca teks gambar dengan C# secara efisien.
og_title: Cara Mengaktifkan GPU untuk Aspose OCR di C# – Cepat Mengubah Gambar menjadi
  Teks Biasa
tags:
- Aspose OCR
- C#
- GPU acceleration
title: Cara Mengaktifkan GPU untuk Aspose OCR di C# – Konversi Cepat Gambar ke Teks
  Biasa
url: /id/net/ocr-optimization/how-to-enable-gpu-for-aspose-ocr-in-c-fast-image-to-plain-te/
---

.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Mengaktifkan GPU untuk Aspose OCR di C# – Mengonversi Gambar ke Teks Biasa dengan Cepat

Pernah bertanya-tanya **bagaimana cara mengaktifkan GPU** saat menggunakan Aspose OCR untuk mengubah gambar menjadi teks yang dapat diedit? Anda tidak sendirian—banyak pengembang mengalami hambatan kinerja saat memproses faktur besar atau kontrak yang dipindai. Kabar baik? Mengubah gambar menjadi teks biasa dapat menjadi sangat cepat begitu Anda memanfaatkan kartu grafis Anda.

Dalam panduan ini kami akan membahas contoh **Aspose OCR** lengkap yang menunjukkan secara tepat cara mengaktifkan GPU, mengatur ID perangkat GPU, dan **membaca teks gambar C#**. Pada akhir panduan Anda akan memiliki program yang dapat dijalankan yang mengekstrak teks dari gambar apa pun yang didukung dalam sebagian kecil waktu dibandingkan pendekatan hanya CPU.

## Apa yang Anda Butuhkan

- .NET 6.0 atau yang lebih baru (API bekerja dengan .NET Core dan .NET Framework)
- GPU yang kompatibel dengan CUDA dengan driver terbaru terpasang
- Lisensi Aspose.OCR untuk .NET (atau percobaan gratis, yang dapat digunakan untuk pengembangan)
- Visual Studio 2022 (atau editor C# apa pun yang Anda sukai)

Tidak diperlukan paket NuGet tambahan selain `Aspose.OCR`—hanya pustaka itu saja.

---

## Langkah 1 – Instal Paket NuGet Aspose OCR

Pertama-tama, tambahkan pustaka resmi Aspose OCR ke proyek Anda. Buka Package Manager Console dan jalankan:

```powershell
Install-Package Aspose.OCR
```

Itu akan mengunduh `Aspose.OCR.dll` dan semua dependensinya. Jika Anda lebih suka GUI, klik kanan proyek Anda → **Manage NuGet Packages** → cari *Aspose.OCR* dan klik **Install**.  
*Pro tip:* Setelah instalasi, pastikan folder `Aspose.OCR` muncul di bawah **Dependencies** di Solution Explorer.

---

## Langkah 2 – Buat Kerangka Aplikasi Konsol Sederhana

Kami akan membuat aplikasi konsol kecil yang mendemonstrasikan seluruh alur. Buat proyek baru:

```bash
dotnet new console -n GpuOcrDemo
cd GpuOcrDemo
```

Ganti `Program.cs` yang dihasilkan dengan kode lengkap yang ditunjukkan nanti. Kerangka ini memberi kami titik masuk yang bersih dan memungkinkan kami fokus pada logika OCR.

---

## Langkah 3 – Cara Mengaktifkan GPU dan Mengatur ID Perangkat GPU

Sekarang untuk bintang utama: **cara mengaktifkan GPU** di Aspose OCR. Pustaka ini menyediakan objek `OcrSettings` di mana Anda dapat mengatur `UseGpu` dan secara opsional memilih perangkat CUDA tertentu melalui `GpuDeviceId`. Di bawah ini cuplikan kode yang tepat yang akan Anda sematkan dalam program Anda:

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;

class GpuExample
{
    static void Main()
    {
        // 1️⃣ Initialise the OCR engine
        var ocrEngine = new OcrEngine();

        // 2️⃣ Enable GPU acceleration – this is the crucial “how to enable gpu” step
        ocrEngine.Settings = new OcrSettings()
        {
            UseGpu = true,          // Turn on GPU processing
            GpuDeviceId = 0         // Optional: select the first CUDA‑compatible device
        };

        // 3️⃣ Recognise text from an image (any supported format)
        var ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/large_invoice.png");

        // 4️⃣ Output the plain‑text result to the console
        Console.WriteLine(ocrResult.Text);
    }
}
```

### Mengapa Mengaktifkan GPU?

Mengaktifkan GPU memindahkan beban kerja berat—praproses piksel, segmentasi karakter, dan inferensi jaringan saraf—ke kartu grafis. Pada GTX 1650 yang sederhana, Anda dapat melihat **peningkatan kecepatan 2‑3×** dibandingkan mode hanya CPU, terutama dengan dokumen beresolusi tinggi.

### Memilih ID Perangkat

Jika mesin Anda memiliki beberapa GPU, `GpuDeviceId` memungkinkan Anda menargetkan GPU tertentu. `0` memilih perangkat pertama; `1` akan memilih yang kedua, dan seterusnya. Anda dapat menemukan ID yang tersedia menggunakan alat NVIDIA `nvidia-smi` atau dengan menanyakan kelas `GpuInfo` milik Aspose (tidak ditampilkan di sini untuk singkat).

---

## Langkah 4 – Contoh Lengkap yang Siap Jalan (Salin‑Tempel)

Di bawah ini adalah program lengkap yang siap dijalankan. Tempelkan ke `Program.cs`, ganti path gambar dengan file sebenarnya di disk Anda, dan tekan **F5**.

```csharp
// Program.cs – Complete Aspose OCR GPU example
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

namespace GpuOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Validate the input argument (optional but handy)
            if (args.Length == 0)
            {
                Console.WriteLine("Usage: dotnet run <image_path>");
                return;
            }

            string imagePath = args[0];

            // Initialise the OCR engine
            var ocrEngine = new OcrEngine();

            // -------------------- How to Enable GPU --------------------
            // Turn on GPU acceleration and optionally pick a device
            ocrEngine.Settings = new OcrSettings()
            {
                UseGpu = true,          // Enables GPU processing
                GpuDeviceId = 0         // Selects the first CUDA‑compatible GPU
            };
            // ---------------------------------------------------------

            try
            {
                // Recognise the image – this is the “image to plain text” core
                var ocrResult = ocrEngine.RecognizeImage(imagePath);

                // Display the extracted text
                Console.WriteLine("=== Extracted Text ===");
                Console.WriteLine(ocrResult.Text);
            }
            catch (Exception ex)
            {
                // Graceful error handling – helpful when the GPU is unavailable
                Console.WriteLine($"Error during OCR: {ex.Message}");
            }
        }
    }
}
```

### Output yang Diharapkan

Jika gambar yang diberikan berisi baris *“Invoice #12345 – Total $1,250.00”*, konsol akan mencetak:

```
=== Extracted Text ===
Invoice #12345 – Total $1,250.00
```

Hasilnya adalah teks biasa, siap untuk diproses lebih lanjut (misalnya, dimasukkan ke basis data atau parser bahasa alami).

---

## Langkah 5 – Verifikasi Pemanfaatan GPU (Opsional)

Untuk memastikan GPU benar‑benar digunakan, buka alat pemantauan GPU Anda (seperti **NVIDIA‑Smi** atau **GPU‑Z**) saat program berjalan. Anda harus melihat lonjakan penggunaan komputasi pada perangkat yang dipilih. Jika Anda hanya melihat aktivitas CPU, periksa kembali bahwa:

- Driver GPU sudah terbaru.
- Flag `UseGpu` disetel ke `true`.
- Format gambar Anda didukung (PNG, JPEG, TIFF, dll.).

---

## Kesalahan Umum & Cara Menghindarinya

| Masalah | Mengapa Terjadi | Perbaikan Cepat |
|-------|----------------|-----------|
| **GPU tidak terdeteksi** | Driver yang usang atau runtime CUDA tidak ada | Instal driver NVIDIA terbaru dan toolkit CUDA |
| **`Aspose.OCR` melempar “GPU not supported”** | Berjalan pada GPU non‑CUDA (misalnya AMD lama) | Set `UseGpu = false` atau beralih ke GPU yang kompatibel |
| **Path gambar tidak benar** | Path relatif mengarah ke folder yang salah | Gunakan path absolut atau berikan path sebagai argumen baris perintah |
| **Lisensi tidak diterapkan** | Mode evaluasi mungkin membatasi penggunaan GPU | Register a license with `License license = new License(); license.SetLicense("Aspose.OCR.lic");` |

---

## Memperluas Contoh: Pemrosesan Batch dengan GPU

Jika Anda perlu memproses puluhan faktur, bungkus panggilan pengenalan dalam sebuah loop. Karena GPU tetap hangat, gambar berikutnya mendapat manfaat dari **caching pemanasan**, mengurangi beberapa milidetik lagi pada setiap eksekusi.

```csharp
string[] files = Directory.GetFiles(@"C:\Invoices\", "*.png");
foreach (var file in files)
{
    var result = ocrEngine.RecognizeImage(file);
    Console.WriteLine($"{Path.GetFileName(file)} → {result.Text.Trim()}");
}
```

Ingat untuk tetap menggunakan instance `OcrEngine` yang sama—membuat engine baru per file akan menginisialisasi ulang konteks GPU dan menurunkan kinerja.

---

## Kesimpulan

Anda kini memiliki contoh **Aspose OCR** yang solid, end‑to‑end yang menunjukkan **cara mengaktifkan GPU**, cara **mengatur ID perangkat GPU**, dan cara **membaca teks gambar C#**. Dengan mengaktifkan `UseGpu` dan menunjuk ke perangkat yang tepat, Anda mengubah pekerjaan OCR yang lambat berbasis CPU menjadi pipeline berkecepatan tinggi yang dapat menangani faktur besar, kwitansi, atau dokumen yang dipindai apa pun.

Silakan bereksperimen: coba format gambar yang berbeda, sesuaikan `GpuDeviceId` pada sistem multi‑GPU, atau gabungkan ini dengan pustaka Aspose lainnya untuk pembuatan PDF. Tidak ada batasan setelah GPU berperan.

---

<img src="gpu-ocr.png" alt="cara mengaktifkan gpu dengan Aspose OCR di C# – mengonversi gambar ke teks biasa dengan cepat">

*Selamat coding! Jika Anda mengalami kendala, tinggalkan komentar di bawah atau kunjungi forum resmi Aspose untuk penjelasan lebih mendalam.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}