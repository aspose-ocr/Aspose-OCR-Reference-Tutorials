---
category: general
date: 2026-04-17
description: Pelajari cara melakukan OCR di C# untuk mengenali teks dari gambar, mengekstrak
  teks dari JPG, dan mengubah gambar menjadi teks dengan cepat.
draft: false
keywords:
- how to perform OCR
- recognize text from image
- extract text from jpg
- convert image to text
- how to extract text
language: id
og_description: Bagaimana melakukan OCR di C#? Panduan ini menunjukkan cara mengenali
  teks dari gambar, mengekstrak teks dari JPG, dan mengonversi gambar menjadi teks
  dalam hitungan menit.
og_title: Cara Melakukan OCR di C# – Mengenali Teks dari Gambar
tags:
- OCR
- C#
- Aspose
title: Cara Melakukan OCR di C# – Mengenali Teks dari Gambar
url: /id/net/text-recognition/how-to-perform-ocr-in-c-recognize-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Melakukan OCR di C# – Mengenali Teks dari Gambar

Pernah bertanya‑tanya **bagaimana melakukan OCR** pada gambar yang Anda dapatkan dari pemindai atau ponsel? Dalam banyak proyek Anda akan perlu **mengenali teks dari gambar**—baik itu struk, catatan tulisan tangan, atau halaman PDF yang diubah menjadi JPEG. Kabar baiknya, dengan Aspose.OCR Anda dapat **mengekstrak teks dari jpg** dan **mengubah gambar menjadi teks** hanya dengan beberapa baris C#.

Dalam tutorial ini kami akan membahas seluruh proses, mulai dari menginstal pustaka hingga menangani kasus‑tepi seperti bahasa yang tidak tersedia. Pada akhir tutorial Anda akan tahu persis **bagaimana melakukan OCR**, dan Anda akan memiliki program siap‑jalankan yang mencetak string yang diekstrak ke konsol. Tanpa jalan pintas “lihat dokumen”—hanya solusi lengkap yang berdiri sendiri.

## Apa yang Anda Perlukan

- **.NET 6+** (kode ini juga bekerja di .NET Framework, tetapi .NET 6 adalah LTS saat ini)
- Paket NuGet **Aspose.OCR for .NET** – instal dengan `dotnet add package Aspose.OCR`
- File gambar (JPEG, PNG, BMP) yang ingin Anda uji – kami akan menyebutnya `input.jpg`
- IDE apa saja yang Anda suka (Visual Studio, Rider, VS Code)

Itu saja. Tanpa konfigurasi tambahan, tanpa layanan eksternal, dan tanpa langkah tersembunyi.

## Langkah 1: Instal Aspose.OCR dan Tambahkan Referensi

Pertama, bawa pustaka OCR ke dalam proyek Anda. Buka terminal di folder proyek dan jalankan:

```bash
dotnet add package Aspose.OCR
```

Perintah ini mengambil versi stabil terbaru (pada April 2026 adalah **23.9.0**) dan memperbarui file `.csproj` Anda. Setelah itu, tambahkan direktif `using` di bagian atas file Anda:

```csharp
using Aspose.OCR;
```

> **Pro tip:** Jika Anda menggunakan Visual Studio, UI NuGet Package Manager bekerja sama baiknya—cukup cari *Aspose.OCR*.

## Langkah 2: Muat Gambar yang Ingin Di‑recognize

Sekarang kita perlu memberi tahu mesin OCR gambar mana yang akan dibaca. Aspose menyediakan metode praktis `OcrImage.FromFile` yang mendukung sebagian besar format umum.

```csharp
// Step 2: Load the image you want to recognize
var ocrImage = OcrImage.FromFile(@"YOUR_DIRECTORY/input.jpg");
```

Ganti `YOUR_DIRECTORY` dengan jalur yang sebenarnya atau biarkan gambar berada di samping executable dan gunakan jalur relatif. Jika file tidak ada, metode ini akan melempar `FileNotFoundException`, yang dapat Anda tangkap nanti.

## Langkah 3: Buat OCR Engine (Platform‑Aware)

Aspose.OCR secara otomatis memilih mesin dasar terbaik untuk OS yang Anda jalankan (Windows, Linux, macOS). Membuatnya di dalam blok `using` menjamin pembuangan yang tepat.

```csharp
// Step 3: Create the OCR engine (auto‑selects best engine for the platform)
using var ocrEngine = new OcrEngine();
```

Kenapa pakai `using`? Engine menyimpan sumber daya native (seperti memori tak terkelola) yang harus dibebaskan. Lupa membuangnya dapat menyebabkan kebocoran memori, terutama saat memproses banyak gambar dalam loop.

## Langkah 4: (Opsional) Atur Bahasa – Bahasa Inggris sebagai Default

Jika gambar Anda berisi teks berbahasa Inggris, Anda dapat melewatkan langkah ini karena `OcrLanguage.English` adalah default. Untuk bahasa lain, cukup tetapkan nilai enum yang sesuai.

```csharp
// Step 4: (Optional) Specify the language – English is the default
ocrEngine.Language = OcrLanguage.English;
```

> **Tahukah Anda?** Aspose.OCR mendukung lebih dari 30 bahasa, termasuk Arab, Cina, dan Rusia. Mengganti bahasa semudah mengubah enum.

## Langkah 5: Jalankan Proses Recognize

Memanggil `Recognize` melakukan pekerjaan berat—analisis piksel, segmentasi karakter, dan pencarian kamus terjadi di balik layar.

```csharp
// Step 5: Run the recognition process on the loaded image
var ocrResult = ocrEngine.Recognize(ocrImage);
```

Jika engine tidak menemukan teks apa pun, `ocrResult.Text` akan menjadi string kosong. Anda mungkin ingin memeriksa `ocrResult.HasText` (Boolean) sebelum melanjutkan.

## Langkah 6: Ambil dan Tampilkan Hasil Plain‑Text

Akhirnya, ekstrak string dan tulis ke konsol. Di sinilah Anda **mengubah gambar menjadi teks**.

```csharp
// Step 6: Retrieve the plain‑text result and display it
string recognizedText = ocrResult.Text;
Console.WriteLine("Recognized text:");
Console.WriteLine(recognizedText);
```

Outputnya akan terlihat seperti berikut:

```
Recognized text:
Invoice #12345
Date: 04/15/2026
Total: $256.78
```

Jika Anda memerlukan teks untuk pemrosesan lebih lanjut (misalnya, menyimpan ke file, memasukkan ke basis data, atau menjalankan regex), Anda sudah memilikinya di variabel `recognizedText`.

## Contoh Lengkap yang Berfungsi

Berikut adalah program lengkap yang dapat Anda salin‑tempel ke aplikasi konsol baru (`dotnet new console`). Program ini mencakup penanganan error untuk jebakan paling umum.

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        try
        {
            // 1️⃣ Load the image you want to recognize
            var ocrImage = OcrImage.FromFile(@"YOUR_DIRECTORY/input.jpg");

            // 2️⃣ Create the OCR engine (auto‑selects best engine for the platform)
            using var ocrEngine = new OcrEngine();

            // 3️⃣ (Optional) Set language – English is default
            ocrEngine.Language = OcrLanguage.English;

            // 4️⃣ Run the recognition process
            var ocrResult = ocrEngine.Recognize(ocrImage);

            // 5️⃣ Check if any text was found
            if (!ocrResult.HasText || string.IsNullOrWhiteSpace(ocrResult.Text))
            {
                Console.WriteLine("No text could be extracted from the image.");
                return;
            }

            // 6️⃣ Retrieve and display the plain‑text result
            string recognizedText = ocrResult.Text;
            Console.WriteLine("Recognized text:");
            Console.WriteLine(recognizedText);
        }
        catch (FileNotFoundException)
        {
            Console.WriteLine("The specified image file was not found. Double‑check the path.");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"An unexpected error occurred: {ex.Message}");
        }
    }
}
```

> **Output yang diharapkan:** Konsol mencetak karakter persis yang dideteksi oleh engine OCR. Jika gambar sumber jelas dan beresolusi tinggi, akurasi biasanya melebihi 95 %.

## Menangani Kasus‑tepi Umum

### 1️⃣ Gambar dengan Banyak Bahasa  
Jika Anda memiliki struk dwibahasa, setel `ocrEngine.Language` ke `OcrLanguage.Multilingual`. Engine akan mencoba mendeteksi setiap bahasa secara otomatis.

```csharp
ocrEngine.Language = OcrLanguage.Multilingual;
```

### 2️⃣ Gambar Resolusi Rendah atau Miring  
Pra‑proses gambar (rotasi, ubah ukuran, tingkatkan kontras) sebelum memberikannya ke Aspose. Pustaka ini menyediakan metode `OcrImage` seperti `Resize` dan `Rotate`.

```csharp
ocrImage = ocrImage.Rotate(0.0); // placeholder – replace with actual angle if needed
```

### 3️⃣ Batch Besar  
Saat memproses puluhan file, gunakan kembali instance `OcrEngine` yang sama alih‑alih membuat yang baru pada setiap iterasi. Ingat untuk membuangnya setelah batch selesai.

```csharp
using var batchEngine = new OcrEngine();
foreach (var file in Directory.GetFiles(@"images", "*.jpg"))
{
    var img = OcrImage.FromFile(file);
    var result = batchEngine.Recognize(img);
    // handle result…
}
```

### 4️⃣ Keterbatasan Memori pada Kontainer Linux  
Jika Anda menjalankan di dalam kontainer Docker dengan RAM terbatas, setel `ocrEngine.MaxMemoryUsage` (jika API menyediakan properti tersebut) untuk menghindari crash OOM.

## Pro Tips & Gotchas

- **Encoding File:** String yang dikembalikan adalah UTF‑16 (`string` di .NET). Jika Anda membutuhkan UTF‑8 untuk menulis ke file, gunakan `Encoding.UTF8.GetBytes(recognizedText)`.
- **Performa:** Untuk satu gambar, overhead inisialisasi engine dapat diabaikan. Untuk pekerjaan massal, inisialisasi sekali (lihat contoh batch) dapat mengurangi waktu proses sekitar ~30 %.
- **Debugging:** Jika hasil OCR terlihat berantakan, periksa `ocrResult.Words` (koleksi objek kata individual) untuk melihat skor kepercayaan. Kepercayaan rendah biasanya berarti gambar blur.
- **Lisensi:** Aspose.OCR berfungsi dalam mode evaluasi tanpa lisensi, tetapi menambahkan watermark pada teks output. Daftarkan file lisensi (`Aspose.OCR.lic`) untuk penggunaan produksi.

## Visual Overview

![how to perform OCR example in C#](ocr-example.png "how to perform OCR example in C#")

*The screenshot shows the complete console output after running the sample code.*

## Kesimpulan

Anda kini memiliki pemahaman yang kuat tentang **bagaimana melakukan OCR** di C# menggunakan Aspose.OCR, dan Anda dapat dengan percaya diri **mengenali teks dari gambar**, **mengekstrak teks dari jpg**, serta **mengubah gambar menjadi teks** untuk pemrosesan lanjutan apa pun. Contoh ini mencakup langkah‑langkah esensial, menjelaskan mengapa setiap bagian penting, dan bahkan memberi petunjuk tentang skenario lanjutan seperti dukungan multibahasa dan pemrosesan batch.

Apa selanjutnya? Coba ganti JPEG dengan PNG, eksperimen dengan `OcrLanguage.Multilingual`, atau alirkan teks yang diekstrak ke pipeline pemrosesan bahasa alami. Langit adalah batasnya ketika Anda dapat mengubah gambar menjadi string yang dapat dicari dan diedit.

Punya pertanyaan atau mengalami kendala? Tinggalkan komentar di bawah, dan selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}