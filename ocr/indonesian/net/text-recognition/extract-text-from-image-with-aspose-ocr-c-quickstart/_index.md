---
category: general
date: 2026-02-13
description: Ekstrak teks dari gambar menggunakan Aspose OCR di C#. Pelajari cara
  membaca teks dari JPG dan menjalankan OCR pada gambar dengan contoh lengkap yang
  dapat dijalankan.
draft: false
keywords:
- extract text from image
- read text from jpg
- run OCR on image
- Aspose OCR C#
- OCR language packs
language: id
og_description: Ekstrak teks dari gambar menggunakan Aspose OCR di C#. Panduan ini
  menunjukkan cara membaca teks dari JPG dan menjalankan OCR pada gambar dengan contoh
  kode lengkap.
og_title: Ekstrak Teks dari Gambar dengan Aspose OCR – Panduan Cepat C#
tags:
- C#
- OCR
- Aspose
title: Ekstrak Teks dari Gambar dengan Aspose OCR – Panduan Cepat C#
url: /id/net/text-recognition/extract-text-from-image-with-aspose-ocr-c-quickstart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ekstrak Teks dari Gambar dengan Aspose OCR – Panduan Cepat C#

Pernah membutuhkan untuk **extract text from image** tetapi tidak yakin pustaka mana yang harus dipilih? Anda tidak sendirian—para pengembang terus‑menerus berjuang dengan membaca teks dari file jpg, terutama ketika kontennya dalam skrip non‑Latin. Kabar baik? Dengan Aspose OCR Anda dapat menjalankan OCR pada file gambar hanya dengan beberapa baris kode C#, dan pustaka tersebut mengurus pengunduhan paket bahasa secara otomatis.

Dalam tutorial ini kami akan membahas contoh lengkap end‑to‑end yang menunjukkan cara **extract text from image** menggunakan Aspose OCR, membatasi pengenalan ke bahasa Rusia, dan mencetak hasilnya ke konsol. Pada akhir tutorial Anda akan dapat membaca teks dari file jpg, menjalankan OCR pada aset gambar dengan ukuran apa pun, dan menyesuaikan kode untuk bahasa lain dengan perubahan minimal.

> **Apa yang akan Anda pelajari**
> * Cara menginstal dan mereferensikan Aspose OCR dalam proyek .NET.  
> * Langkah‑langkah tepat untuk **extract text from image**—menginisialisasi engine, memilih bahasa, dan memanggil `RecognizeImage`.  
> * Mengapa Anda mungkin ingin mengunci engine ke satu paket bahasa (kecepatan, akurasi).  
> * Kesulitan umum seperti file yang hilang atau format yang tidak didukung, serta cara menanganinya dengan elegan.  

## Prasyarat

Sebelum kita mulai, pastikan Anda memiliki hal‑hal berikut di mesin Anda:

| Persyaratan | Alasan |
|-------------|--------|
| .NET 6.0 SDK atau lebih baru | Aspose OCR menargetkan .NET Standard 2.0+, jadi .NET 6 memberi Anda fitur runtime terbaru. |
| Visual Studio 2022 (atau IDE apa pun yang Anda suka) | Berguna untuk debugging, tetapi tidak wajib. |
| File gambar (`cyrillic_sample.jpg`) yang berisi teks Cyrillic | Kami akan menggunakan file ini untuk mendemonstrasikan **read text from jpg**. |
| Koneksi internet (hanya pada run pertama) | Aspose OCR mengunduh paket bahasa sesuai kebutuhan. |

Jika Anda belum memiliki salah satu dari ini, dapatkan sekarang—tidak perlu memulai ulang setelah menginstal SDK.

## Langkah 1: Instal Paket NuGet Aspose OCR

Hal pertama yang Anda butuhkan adalah pustaka Aspose OCR. Buka terminal di folder proyek Anda dan jalankan:

```bash
dotnet add package Aspose.OCR
```

Perintah ini mengambil versi stabil terbaru (pada Februari 2026 versi 23.12) dan menambahkannya ke `.csproj` Anda. Paket ini mencakup engine OCR inti dan pengunduh ringan untuk paket bahasa, sehingga Anda tidak perlu menyertakan file besar dalam aplikasi Anda.

> **Pro tip:** Jika Anda bekerja di belakang proxy perusahaan, atur variabel lingkungan `http_proxy` sebelum menjalankan perintah untuk menghindari kesalahan unduhan.

## Langkah 2: Buat Kerangka Aplikasi Konsol

Mari siapkan aplikasi konsol minimal yang akan menampung logika OCR kami. Buka `Program.cs` (atau buat file baru) dan tempelkan kerangka di bawah ini. Perhatikan direktif `using` di bagian atas—ini membawa namespace Aspose OCR ke dalam ruang lingkup.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Enums;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll fill this in in the next steps.
        }
    }
}
```

Pada titik ini proyek berhasil dikompilasi, tetapi belum melakukan apa‑apa. Bagian‑bagian berikutnya akan mengembangkan alur kerja **run OCR on image**.

## Langkah 3: Inisialisasi Engine OCR (Extract Text from Image)

Untuk **extract text from image**, pertama-tama Anda memerlukan instance `OcrEngine`. Aspose OCR secara malas mengunduh sumber daya bahasa pada pertama kali diperlukan, sehingga binary awal tetap kecil.

```csharp
// Step 3: Initialize the OCR engine (resources are downloaded on demand)
var ocrEngine = new OcrEngine();
```

Mengapa inisialisasi di sini bukan di field statis? Melakukannya di dalam `Main` menjamin bahwa setiap pengecualian (seperti ketergantungan native yang hilang) muncul lebih awal, memudahkan proses debugging.

## Langkah 4: Batasi Pengenalan ke Bahasa yang Diinginkan (Read Text from JPG)

Jika Anda mengetahui bahasa teks yang Anda pindai—misalnya Rusia—Anda dapat meningkatkan kecepatan dan akurasi dengan mengatur properti `Language`. Ini sangat berguna ketika Anda **read text from jpg** file yang berisi karakter Cyrillic.

```csharp
// Step 4: Limit recognition to the Russian language pack (ISO code "ru")
ocrEngine.Language = OcrLanguage.Russian;
```

Di balik layar Aspose OCR akan mengunduh paket bahasa Rusia pada pertama kali Anda mengeksekusi baris ini. Jalankan selanjutnya akan menggunakan paket yang sudah di‑cache, sehingga tidak ada penalti jaringan setelah unduhan pertama.

> **Mengapa mengunci bahasa?**  
> * **Kinerja:** Engine melewatkan pemindaian karakter di luar alfabet yang dipilih.  
> * **Akurasi:** Heuristik khusus bahasa (seperti frekuensi kata umum) diterapkan, mengurangi kesalahan pengenalan.  

Jika Anda perlu mendukung banyak bahasa, Anda dapat memberikan daftar dipisahkan koma, misalnya `OcrLanguage.English | OcrLanguage.Russian`.

## Langkah 5: Lakukan OCR pada JPG Target (Run OCR on Image)

Sekarang kita benar‑benar **run OCR on image**. Berikan path lengkap ke file JPG Anda—Aspose OCR menerima banyak format (`.png`, `.bmp`, `.tif`, dll.), tetapi kami akan tetap menggunakan `.jpg` untuk demo ini.

```csharp
// Step 5: Perform OCR on the image containing Cyrillic text
string imagePath = @"YOUR_DIRECTORY/cyrillic_sample.jpg";
var recognizedResult = ocrEngine.RecognizeImage(imagePath);
```

Jika file tidak ditemukan, `RecognizeImage` akan melempar `FileNotFoundException`. Untuk membuat tutorial ini kuat, bungkus pemanggilan dalam blok try‑catch:

```csharp
try
{
    var recognizedResult = ocrEngine.RecognizeImage(imagePath);
    Console.WriteLine("✅ OCR succeeded!");
    Console.WriteLine("Extracted text:");
    Console.WriteLine(recognizedResult.Text);
}
catch (Exception ex)
{
    Console.Error.WriteLine($"❌ Error during OCR: {ex.Message}");
}
```

Metode `RecognizeImage` mengembalikan objek `OcrResult` yang properti `Text`‑nya berisi hasil ekstraksi teks polos. Anda juga dapat mengakses `Boxes` untuk data kotak pembatas jika membutuhkan informasi tata letak nanti.

## Langkah 6: Verifikasi Output

Saat Anda menjalankan program (`dotnet run`), Anda akan melihat sesuatu seperti:

```
✅ OCR succeeded!
Extracted text:
Пример текста на кириллице
```

Jika output terlihat berantakan, periksa kembali bahwa gambar jelas dan Anda telah memilih bahasa yang tepat. Gambar yang buram atau kontras rendah adalah penyebab paling umum hasil OCR yang buruk.

### Kasus Pinggir & Pertanyaan Umum

| Situasi | Apa yang Harus Dilakukan |
|-----------|------------|
| **Gambar berisi banyak bahasa** | Set `ocrEngine.Language` ke kombinasi, misalnya `OcrLanguage.English | OcrLanguage.Russian`. |
| **Batch besar gambar** | Gunakan kembali instance `OcrEngine` yang sama untuk semua file; ia menyimpan data bahasa di cache. |
| **Menjalankan di server tanpa UI** | Tidak diperlukan UI—Aspose OCR berfungsi baik di Docker atau Azure Functions. |
| **Butuh akurasi lebih tinggi** | Sesuaikan `ocrEngine.Options` (mis., `ocrEngine.Options.Denoise = true`). |
| **Format file tidak didukung** | Konversi gambar ke format yang didukung (PNG atau JPG) sebelum memanggil `RecognizeImage`. |

## Contoh Lengkap yang Berfungsi

Berikut adalah program lengkap yang siap disalin‑tempel yang menggabungkan semua langkah di atas. Simpan sebagai `Program.cs` dan jalankan dari baris perintah.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Enums;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize the OCR engine (downloads language packs on first use)
            var ocrEngine = new OcrEngine();

            // 2️⃣ Restrict recognition to Russian – speeds up processing and boosts accuracy
            ocrEngine.Language = OcrLanguage.Russian;

            // 3️⃣ Path to the JPG you want to read text from
            string imagePath = @"YOUR_DIRECTORY/cyrillic_sample.jpg";

            // 4️⃣ Perform OCR and handle possible errors
            try
            {
                var result = ocrEngine.RecognizeImage(imagePath);
                Console.WriteLine("✅ OCR completed successfully.");
                Console.WriteLine("🖼️ Extracted text:");
                Console.WriteLine(result.Text);
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"❌ Failed to extract text from image: {ex.Message}");
            }
        }
    }
}
```

**Output konsol yang diharapkan** (asumsi gambar contoh berisi frasa “Пример текста на кириллице”):

```
✅ OCR completed successfully.
🖼️ Extracted text:
Пример текста на кириллице
```

Jika Anda mengganti gambar dengan foto berbahasa Inggris dan mengubah `ocrEngine.Language = OcrLanguage.English;`, kode yang sama akan **read text from jpg** dalam bahasa Inggris tanpa perubahan lebih lanjut.

## Bonus: Menjalankan OCR pada Banyak File

Seringkali Anda perlu **run OCR on image** koleksi. Berikut cuplikan cepat yang mengulangi folder:

```csharp
string folder = @"YOUR_DIRECTORY";
foreach (var file in System.IO.Directory.GetFiles(folder, "*.jpg"))
{
    try
    {
        var result = ocrEngine.RecognizeImage(file);
        Console.WriteLine($"[{System.IO.Path.GetFileName(file)}] => {result.Text}");
    }
    catch (Exception ex)
    {
        Console.Error.WriteLine($"Error processing {file}: {ex.Message}");
    }
}
```

Engine menggunakan kembali paket bahasa yang sudah diunduh sebelumnya, sehingga batch berjalan efisien.

## Kesimpulan

Anda kini memiliki pola yang solid dan siap produksi untuk **extract text from image** menggunakan Aspose OCR di C#. Tutorial ini mencakup semua hal mulai dari menginstal paket NuGet hingga menangani kesalahan dan menskalakan ke banyak file. Baik Anda **reading text from jpg** aset, memindai PDF, atau membangun pipeline otomatisasi dokumen, pendekatan yang sama berlaku—cukup ganti paket bahasa atau sesuaikan opsi OCR.

Siap untuk langkah selanjutnya? Coba:

* Mencoba bahasa lain (misalnya `OcrLanguage.ChineseSimplified`).  
* Mengekstrak informasi tata letak melalui `recognizedResult.Boxes`.  
* Mengintegrasikan alur OCR ke dalam API ASP.NET Core sehingga layanan lain dapat meminta ekstraksi teks sesuai permintaan.  

Selamat coding, semoga gambar Anda selalu cukup tajam untuk OCR yang sempurna!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}