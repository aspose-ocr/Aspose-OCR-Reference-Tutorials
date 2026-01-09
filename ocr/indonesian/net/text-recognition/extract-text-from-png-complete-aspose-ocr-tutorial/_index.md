---
category: general
date: 2026-01-09
description: Ekstrak teks dari PNG dengan cepat menggunakan Aspose OCR. Pelajari cara
  membaca teks gambar, meningkatkan akurasi OCR, dan mendapatkan hasil bersih di C#.
draft: false
keywords:
- extract text from png
- read image text
- improve ocr accuracy
- extract text from image
- aspose ocr tutorial
language: id
og_description: Ekstrak teks dari PNG dengan cepat menggunakan Aspose OCR. Pelajari
  cara membaca teks gambar, meningkatkan akurasi OCR, dan mendapatkan hasil yang bersih
  di C#.
og_title: Ekstrak Teks dari PNG – Tutorial OCR Aspose Lengkap
tags:
- Aspose OCR
- C#
- Image Processing
title: Ekstrak Teks dari PNG – Tutorial OCR Aspose Lengkap
url: /id/net/text-recognition/extract-text-from-png-complete-aspose-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ekstrak Teks dari PNG – Tutorial Lengkap Aspose OCR

Pernah perlu **mengekstrak teks dari file PNG** tetapi hasilnya penuh dengan karakter tak terbaca? Anda tidak sendirian. Dalam banyak proyek dunia nyata – faktur, kwitansi, atau formulir yang dipindai – kualitas output OCR dapat menentukan keberhasilan atau kegagalan alur otomatisasi.  

Dalam panduan ini kami akan menunjukkan cara **langkah‑demi‑langkah** untuk membaca teks gambar menggunakan Aspose OCR, menambahkan kamus khusus untuk **meningkatkan akurasi OCR**, membersihkan noise, dan akhirnya mencetak string yang rapi. Pada akhir tutorial Anda akan memiliki aplikasi konsol C# yang siap dijalankan dan dapat mengekstrak teks dari gambar PNG secara andal.

> **Apa yang akan Anda dapatkan**  
> * Contoh kode lengkap yang dapat dijalankan.  
> * Pemahaman mengapa kamus khusus penting.  
> * Tips menangani kasus tepi seperti pemindaian dengan kontras rendah.  

## Prerequisites

- .NET 6 SDK atau yang lebih baru (kode menargetkan .NET 6, tetapi .NET 5 juga dapat digunakan).  
- Visual Studio 2022 atau editor pilihan Anda.  
- Gambar **PNG** yang ingin Anda proses – misalnya `invoice.png`.  
- Paket NuGet **Aspose.OCR** (`dotnet add package Aspose.OCR`).  

Tidak diperlukan file konfigurasi tambahan; semuanya berada dalam satu file `.cs`.

## Step 1 – Install and Reference Aspose OCR

Pertama, tarik pustaka ke dalam proyek Anda. Buka terminal di folder solusi dan jalankan:

```bash
dotnet add package Aspose.OCR
```

Baris tunggal itu mengunduh versi stabil terbaru (per Jan 2026, versi 23.9). Paket tersebut menyertakan kelas `OcrEngine` yang akan kita gunakan sepanjang tutorial.

## Step 2 – Initialize the OCR Engine

Membuat instance `OcrEngine` adalah fondasi. Anggaplah ini seperti menyalakan pemindai yang siap menafsirkan piksel.

```csharp
using Aspose.OCR;

// Initialize the OCR engine
var ocrEngine = new OcrEngine();
```

> **Pro tip:** Jika Anda berencana memproses banyak gambar dalam sebuah loop, gunakan kembali instance `OcrEngine` yang sama. Ia menyimpan cache sumber daya internal dan mempercepat panggilan berikutnya.

## Step 3 – Boost Accuracy with a Custom Dictionary

OCR bawaan sudah bagus, tetapi dapat kesulitan dengan kata‑kata khusus domain seperti “Aspose”, “OCR”, atau “SDK”. Menambahkan istilah‑istilah tersebut ke **kamus khusus** memberi tahu mesin bahwa string‑string itu sah, sehingga mengurangi kesalahan pengenalan.

```csharp
// Define domain‑specific terms that the engine should recognize
ocrEngine.CustomDictionary = new HashSet<string>
{
    "Aspose",
    "OCR",
    "SDK",
    "invoice"
};
```

### Mengapa kamus khusus membantu

- **Model statistik** di balik OCR sangat memperhatikan pola bahasa umum. Kata‑kata yang jarang muncul memiliki probabilitas rendah dan dapat digantikan oleh karakter yang terlihat mirip.  
- Dengan mencantumkannya secara eksplisit, Anda menimpa tebakan model.  
- Ini sangat berguna untuk **membaca teks gambar** yang berisi kode produk, singkatan, atau nama merek.

## Step 4 – Recognize Text from the PNG File

Sekarang kita beri mesin jalur gambar. Metode `RecognizeImage` mengembalikan string mentah yang masih berisi token tidak dikenal (misalnya “#@!”) yang tidak dapat dipetakan oleh mesin.

```csharp
// Path to the PNG you want to process
string imagePath = @"YOUR_DIRECTORY/invoice.png";

// Perform OCR
string rawText = ocrEngine.RecognizeImage(imagePath);
```

> **Kasus tepi:** Jika file tidak ditemukan, `RecognizeImage` akan melempar `FileNotFoundException`. Bungkus pemanggilan dalam blok try‑catch untuk kode produksi.

## Step 5 – Clean the Result with `CleanText`

Aspose OCR menyediakan helper yang menghapus karakter yang ditandai sebagai “tidak dikenal”. Langkah ini penting untuk proyek **ekstrak teks dari gambar** di mana parser downstream mengharapkan hanya alfanumerik dan tanda baca dasar.

```csharp
// Remove unknown tokens and extra whitespace
string cleanedText = ocrEngine.CleanText(rawText);
```

Metode `CleanText` juga menormalkan akhir baris, sehingga output aman disimpan di basis data atau diteruskan ke layanan lain.

## Step 6 – Output the Cleaned Text

Akhirnya, tampilkan atau simpan hasilnya. Pada aplikasi konsol, `Console.WriteLine` sudah cukup.

```csharp
Console.WriteLine("=== Cleaned OCR Output ===");
Console.WriteLine(cleanedText);
```

Saat Anda menjalankan program, Anda akan melihat blok teks rapi yang mencerminkan isi `invoice.png`. Jika gambar berisi kata “Aspose”, kamus khusus memastikan kata tersebut muncul dengan benar, bukan sesuatu seperti “A5p0se”.

## Full Working Example

Menggabungkan semuanya, berikut adalah `Program.cs` lengkap yang dapat Anda salin‑tempel ke proyek konsol baru:

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize the OCR engine
        var ocrEngine = new OcrEngine();

        // 2️⃣ Add domain‑specific terms to improve OCR accuracy
        ocrEngine.CustomDictionary = new HashSet<string>
        {
            "Aspose",
            "OCR",
            "SDK",
            "invoice"
        };

        // 3️⃣ Path to your PNG file (adjust as needed)
        string imagePath = @"YOUR_DIRECTORY/invoice.png";

        try
        {
            // 4️⃣ Recognize raw text from the image
            string rawText = ocrEngine.RecognizeImage(imagePath);

            // 5️⃣ Clean up unknown tokens
            string cleanedText = ocrEngine.CleanText(rawText);

            // 6️⃣ Show the result
            Console.WriteLine("=== Cleaned OCR Output ===");
            Console.WriteLine(cleanedText);
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error processing image: {ex.Message}");
        }
    }
}
```

**Output yang diharapkan** (asumsi PNG berisi faktur sederhana):

```
=== Cleaned OCR Output ===
Invoice #12345
Date: 01/08/2026
Total: $1,250.00
Thank you for your business!
```

Jika Anda melihat simbol aneh, periksa kembali kualitas gambar atau tambahkan lebih banyak istilah ke kamus khusus.

## Bonus: Handling Low‑Quality Scans

Kadang PNG dipindai pada 72 dpi atau memiliki artefak kompresi berat. Berikut beberapa trik cepat untuk **meningkatkan akurasi OCR** tanpa meninggalkan C#:

1. **Pra‑proses gambar** dengan pustaka seperti `SixLabors.ImageSharp` – tingkatkan kontras, konversi ke grayscale, atau terapkan blur ringan untuk mengurangi noise.  
2. **Set properti `Resolution`** pada `OcrEngine` (misalnya `ocrEngine.Resolution = 300;`) untuk memberi tahu mesin memperlakukan gambar sebagai resolusi lebih tinggi.  
3. **Aktifkan paket bahasa** jika Anda menangani teks non‑Inggris (`ocrEngine.Language = Language.English;`).

Ketiga pendekatan dapat ditambahkan sebelum pemanggilan `RecognizeImage`.

## Frequently Asked Questions

- **Apakah ini bekerja dengan format gambar lain?**  
  Ya. `RecognizeImage` menerima JPEG, BMP, TIFF, dan bahkan PDF (sebagai kontainer gambar). Langkah‑langkahnya sama.

- **Bisakah saya mengekstrak teks dari banyak PNG dalam satu folder?**  
  Tentu. Bungkus logika inti dalam loop `foreach (var file in Directory.GetFiles(folder, "*.png"))` dan simpan setiap hasil dalam daftar atau tulis ke file terpisah.

- **Bagaimana jika saya membutuhkan koordinat teks?**  
  Aspose OCR juga menyediakan objek `OcrResult` yang mencakup bounding box. Gunakan `ocrEngine.RecognizeImageToResult(imagePath)` untuk skenario lanjutan tersebut.

## Conclusion

Kami telah menelusuri solusi **lengkap, end‑to‑end** untuk **mengekstrak teks dari file PNG** menggunakan Aspose OCR. Dengan menginisialisasi mesin, memberi kamus khusus, membersihkan output mentah, dan menangani beberapa jebakan umum, Anda dapat secara andal **membaca teks gambar** dan **meningkatkan akurasi OCR** dalam aplikasi C# Anda sendiri.

Siap untuk langkah selanjutnya? Coba ganti PNG dengan kwitansi yang dipindai, tambahkan lebih banyak kata domain ke kamus, atau integrasikan output dengan basis data untuk pemrosesan faktur otomatis. Langit adalah batasnya ketika Anda menggabungkan Aspose OCR dengan ekosistem .NET yang kaya.

Selamat coding, semoga OCR Anda selalu tepat! 

![Ekstrak teks dari contoh png](/images/extract-text-from-png.png "ekstrak teks dari png – demo Aspose OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}