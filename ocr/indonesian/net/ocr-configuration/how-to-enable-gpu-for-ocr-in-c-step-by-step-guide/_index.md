---
category: general
date: 2026-04-04
description: Cara mengaktifkan GPU di Aspose OCR dengan cepat. Pelajari cara mengekstrak
  teks dari gambar, memuat gambar untuk OCR, dan mengenali teks menggunakan C#.
draft: false
keywords:
- how to enable gpu
- extract text from image
- how to extract text
- how to recognize text
- load image for ocr
language: id
og_description: Cara mengaktifkan GPU di Aspose OCR dengan cepat. Ikuti tutorial ini
  untuk mengekstrak teks dari gambar, memuat gambar untuk OCR, dan mengenali teks
  dengan C#.
og_title: Cara mengaktifkan GPU untuk OCR di C# – Panduan Lengkap
tags:
- Aspose OCR
- C#
- GPU acceleration
title: Cara Mengaktifkan GPU untuk OCR di C# – Panduan Langkah demi Langkah
url: /id/net/ocr-configuration/how-to-enable-gpu-for-ocr-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Mengaktifkan GPU untuk OCR di C# – Panduan Lengkap

Pernah bertanya‑tanya **cara mengaktifkan GPU** saat menggunakan Aspose OCR? Mungkin Anda menemui batas performa saat memproses ratusan kwitansi, dan CPU tidak dapat mengimbanginya. Kabar baiknya, mengaktifkan akselerasi GPU sangat mudah, dan begitu diaktifkan Anda akan melihat mesin OCR melesat melalui gambar.

Dalam tutorial ini kami tidak hanya akan menyalakan saklar GPU, tetapi juga menunjukkan **cara memuat gambar untuk OCR**, **cara mengenali teks**, dan pada akhirnya **cara mengekstrak teks dari gambar** menggunakan contoh C# yang bersih. Pada akhir tutorial Anda akan memiliki program siap‑jalankan yang mengambil teks polos dari gambar apa pun yang didukung—tanpa layanan eksternal.

## Apa yang Anda Butuhkan

- .NET 6+ (atau .NET Framework 4.7.2 ke atas).  
- Aspose.OCR for .NET, versi 24.2.0 atau lebih baru (bendera GPU ditambahkan pada rilis ini).  
- Mesin dengan GPU yang diaktifkan serta driver yang sesuai (NVIDIA CUDA 11+ bekerja dengan baik).  
- File gambar yang ingin Anda proses—misalnya kwitansi yang dipindai, faktur yang difoto, atau catatan tulisan tangan.

Jika Anda sudah memiliki semua itu, bagus—mari kita mulai.

## Langkah 1: Cara mengaktifkan GPU – Konfigurasi OcrEngine

Hal pertama yang harus Anda lakukan adalah memberi tahu Aspose OCR untuk menggunakan GPU. Ini dilakukan dengan mengatur properti `UseGpu` pada instance `OcrEngine`. Properti ini defaultnya `false`, jadi kita secara eksplisit mengaktifkannya.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // <-- GPU module namespace

// Create the OCR engine and enable GPU acceleration (available from version 24.2.0)
var ocrEngine = new OcrEngine
{
    // Enabling GPU can speed up recognition by 2‑5× on a modern card
    UseGpu = true
};
```

**Mengapa ini penting:** Ketika `UseGpu` bernilai `true`, perpustakaan memindahkan perhitungan matriks berat ke prosesor grafis. Pada RTX 3060 yang sederhana, Anda akan melihat penurunan latensi dari beberapa detik per gambar menjadi sebagian detik.

> **Tips profesional:** Jika Anda menjalankan di lingkungan CI tanpa tampilan (headless), pastikan driver GPU terpasang dan akun layanan memiliki izin untuk mengakses perangkat. Jika tidak, mesin akan diam‑diam kembali ke mode CPU.

## Langkah 2: Memuat Gambar untuk OCR – Arahkan Engine ke File Anda

Selanjutnya kita perlu **memuat gambar untuk OCR**. Aspose OCR menerima format gambar apa pun yang didukung oleh System.Drawing (PNG, JPEG, BMP, TIFF, dll.). Helper `ImageStream.FromFile` membungkus file ke dalam objek stream yang diperlukan.

```csharp
// Replace the path with the location of your receipt or document
string imagePath = @"C:\MyImages\receipt.jpg";

ocrEngine.Image = ImageStream.FromFile(imagePath);
```

Jika Anda lebih suka memuat dari `byte[]` (misalnya ketika gambar berasal dari basis data), Anda dapat menggunakan `ImageStream.FromBytes(byteArray)` sebagai gantinya—hasilnya sama, hanya sumbernya berbeda.

## Langkah 3: Cara mengenali teks – Jalankan Proses OCR

Setelah engine dikonfigurasi dan gambar dimuat, saatnya **mengenali teks**. Metode `Recognize` melakukan semua pekerjaan berat dan mengembalikan objek `OcrResult` yang berisi teks polos, skor kepercayaan, dan bahkan kotak pembatas jika Anda membutuhkannya nanti.

```csharp
// Run the recognition process (English is the default language)
OcrResult ocrResult = ocrEngine.Recognize();
```

Anda juga dapat mengubah bahasa dengan mengatur `ocrEngine.Language = OcrLanguage.French;` sebelum memanggil `Recognize()`. Akselerasi GPU berfungsi terlepas dari paket bahasa yang Anda muat.

## Langkah 4: Cara mengekstrak teks dari gambar – Output Hasil

Akhirnya kami **mengekstrak teks dari gambar** dengan membaca properti `Text` dari objek hasil. Untuk tujuan demo kami hanya mencetaknya ke konsol, tetapi Anda bisa menuliskannya ke file, basis data, atau mengirimnya ke layanan lain.

```csharp
// Output the extracted plain‑text to the console
Console.WriteLine("=== OCR RESULT ===");
Console.WriteLine(ocrResult.Text);
```

**Output yang diharapkan** (teks Anda akan berbeda tergantung gambar):

```
=== OCR RESULT ===
Store: Coffee Corner
Date: 03/28/2026
Item          Qty   Price
Latte          2    $5.00
Muffin         1    $2.50
Total                 $12.50
```

Jika Anda memerlukan nilai kepercayaan mentah, Anda dapat mengiterasi `ocrResult.Regions` dan memeriksa setiap `Region.Confidence`.

## Contoh Lengkap yang Berfungsi – Satu File, Siap Jalankan

Berikut adalah program lengkapnya. Salin‑tempel ke proyek konsol baru, pulihkan paket NuGet Aspose.OCR, dan tekan **F5**.

```csharp
// ------------------------------------------------------------
// How to enable gpu for OCR in C# – Complete Example
// ------------------------------------------------------------
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU module namespace

class Program
{
    static void Main()
    {
        // -------- Step 1: Enable GPU ----------
        var ocrEngine = new OcrEngine
        {
            UseGpu = true   // <-- crucial for acceleration
        };

        // -------- Step 2: Load image ----------
        // Make sure the file exists; otherwise an exception is thrown.
        string imagePath = @"YOUR_DIRECTORY/receipt.jpg";
        ocrEngine.Image = ImageStream.FromFile(imagePath);

        // -------- Step 3: Recognize text -------
        OcrResult ocrResult = ocrEngine.Recognize();

        // -------- Step 4: Extract text ----------
        Console.WriteLine("=== OCR RESULT ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

> **Catatan:** Ganti `YOUR_DIRECTORY/receipt.jpg` dengan jalur sebenarnya ke gambar Anda. Jika program melempar `FileNotFoundException`, periksa kembali jalur dan izin file.

## Pertanyaan Umum & Kasus Pinggir

### Bagaimana jika GPU tidak terdeteksi?

Aspose OCR secara otomatis akan kembali ke mode CPU dan mencatat peringatan. Untuk memverifikasi mode yang aktif, periksa `ocrEngine.IsGpuEnabled` setelah konstruksi—nilai `true` hanya muncul ketika driver GPU berhasil dimuat.

### Bisakah saya memproses banyak gambar dalam loop?

Tentu saja. Pindahkan baris `ocrEngine.Image = …` ke dalam loop `foreach (var file in files)`. Gunakan instance `OcrEngine` yang sama; menggunakannya kembali menghindari overhead alokasi sumber daya GPU berulang kali.

```csharp
foreach (var file in Directory.GetFiles(@"C:\MyImages", "*.jpg"))
{
    ocrEngine.Image = ImageStream.FromFile(file);
    var result = ocrEngine.Recognize();
    Console.WriteLine($"{Path.GetFileName(file)} → {result.Text.Length} characters");
}
```

### Bagaimana cara menangani bahasa non‑Inggris?

Atur bahasa sebelum memanggil `Recognize()`:

```csharp
ocrEngine.Language = OcrLanguage.Spanish;   // or any supported language enum
```

Akselerasi GPU bekerja dengan cara yang sama; hanya model bahasa yang berubah.

### Bagaimana dengan foto beresolusi tinggi dan besar?

Jika Anda mengalami kesalahan out‑of‑memory, perkecil gambar terlebih dahulu. Aspose OCR menyediakan `ImageHelper.Resize` – cara cepat mengecilkan tanpa kehilangan terlalu banyak detail.

```csharp
ocrEngine.Image = ImageHelper.Resize(
    ImageStream.FromFile(imagePath), 
    maxWidth: 2000, 
    maxHeight: 2000);
```

## Kesimpulan

Kami telah membahas **cara mengaktifkan GPU** untuk Aspose OCR, menunjukkan **cara memuat gambar untuk OCR**, menjelaskan **cara mengenali teks**, dan mendemonstrasikan **cara mengekstrak teks dari gambar** dengan program C# yang ringkas dan siap produksi. Dengan menyalakan flag `UseGpu` Anda membuka peningkatan kecepatan yang signifikan, terutama saat memproses batch kwitansi, faktur, atau aliran dokumen bervolume tinggi.

Siap untuk langkah selanjutnya? Cobalah menggabungkan pipeline OCR ini dengan basis data untuk menyimpan kwitansi yang diekstrak, atau alirkan teks polos ke model pemrosesan bahasa alami untuk kategorisasi pengeluaran. Anda juga dapat menjelajahi koleksi `OcrResult.Regions` untuk mendapatkan koordinat kotak pembatas dan membangun UI yang menyorot setiap kata pada gambar asli.

Selamat coding, dan nikmati tenaga ekstra yang dibawa akselerasi GPU ke beban kerja OCR Anda!

---

![ilustrasi cara mengaktifkan gpu](gpu-ocr-diagram.png "ilustrasi cara mengaktifkan gpu")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}