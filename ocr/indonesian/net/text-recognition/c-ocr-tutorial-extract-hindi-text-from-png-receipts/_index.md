---
category: general
date: 2026-01-09
description: Tutorial OCR C# untuk membaca teks dari PNG, mengonversi gambar menjadi
  teks, dan mengenali teks Hindi pada struk menggunakan Aspose OCR.
draft: false
keywords:
- c# ocr tutorial
- read text from png
- convert image to text
- recognize hindi text
- extract text from receipt
language: id
og_description: Tutorial OCR C# yang mengajarkan cara membaca teks dari PNG, mengonversi
  gambar menjadi teks, dan mengenali teks Hindi pada struk dengan Aspose OCR.
og_title: tutorial OCR c# – Ekstrak Teks Hindi dari Resi PNG
tags:
- OCR
- C#
- Aspose
- Image Processing
title: tutorial OCR c# – Ekstrak Teks Hindi dari Resi PNG
url: /id/net/text-recognition/c-ocr-tutorial-extract-hindi-text-from-png-receipts/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr tutorial – Ekstrak Teks Hindi dari Resi PNG

Pernah bertanya-tanya bagaimana cara **membaca teks dari PNG** dalam aplikasi C#? Mungkin Anda memiliki sekumpulan resi Hindi dan perlu mengambil jumlah secara otomatis. Itulah tepatnya yang dibahas dalam tutorial c# ocr ini—mengubah gambar menjadi teks yang dapat dicari dengan hanya beberapa baris kode.

Dalam panduan ini kami akan melangkah melalui instalasi Aspose OCR, memuat resi PNG, mengenali karakter Hindi, dan akhirnya mencetak string yang diekstrak ke konsol. Pada akhir tutorial Anda akan dapat **mengonversi gambar menjadi teks**, **mengenali teks Hindi**, dan bahkan **mengekstrak teks dari gambar resi** tanpa meninggalkan IDE Anda.

> **Catatan Prasyarat:** Anda memerlukan lisensi Aspose OCR yang valid (atau Anda dapat menggunakan versi percobaan gratis) dan .NET 6+ terpasang. Jika Anda baru mengenal NuGet, jangan khawatir—kami akan membahasnya juga.

---

## Apa yang Anda Butuhkan

- **Visual Studio 2022** (atau editor yang kompatibel dengan C#)
- **.NET 6 SDK** (atau yang lebih baru)
- **Aspose.OCR** paket NuGet  
  ```bash
  dotnet add package Aspose.OCR
  ```
- Contoh gambar resi, misalnya `hindi-receipt.png`, disimpan di folder proyek Anda.

Menyiapkan hal‑hal ini berarti Anda dapat menyalin‑tempel kode akhir dan langsung menekan **F5**.

---

## Langkah 1: Siapkan Proyek dan Impor Namespace

Pertama, buat proyek konsol jika Anda belum memilikinya:

```bash
dotnet new console -n HindiReceiptOcr
cd HindiReceiptOcr
dotnet add package Aspose.OCR
```

Sekarang buka `Program.cs`. Di bagian atas, impor namespace Aspose OCR agar kompiler tahu di mana menemukan kelas-kelas tersebut:

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;
```

> **Mengapa ini penting:** `OcrEngine` berada di `Aspose.OCR`, sementara enum terkait bahasa berada di `Aspose.OCR.Settings`. Lupa mengimpor salah satunya akan menyebabkan kesalahan pada waktu kompilasi.

---

## Langkah 2: Inisialisasi Mesin OCR dan Pilih Model Bahasa

Mesin OCR perlu mengetahui **bahasa apa** yang harus dicari. Aspose menyediakan banyak paket bahasa; menentukan `OcrLanguage.Hindi` memberi tahu mesin untuk mengunduh (jika belum ada) dan menggunakan model Hindi.

```csharp
// Step 2: Create and configure the OCR engine
var ocrEngine = new OcrEngine
{
    // The library will auto‑download the model the first time it runs.
    Language = OcrLanguage.Hindi
};
```

> **Tip Pro:** Jika Anda berencana memproses resi dalam beberapa bahasa, Anda dapat mengubah `Language` saat runtime atau bahkan mengaktifkan mode `MultiLanguage`.

---

## Langkah 3: Berikan Resi PNG ke Mesin

Di sinilah kita **membaca teks dari PNG**. Berikan jalur lengkap (relatif terhadap executable juga dapat). Metode ini mengembalikan string biasa yang berisi semua yang dapat diuraikan oleh mesin.

```csharp
// Step 3: Perform OCR on the target image file
string imagePath = @"hindi-receipt.png";   // adjust if your file lives elsewhere
string recognizedText = ocrEngine.RecognizeImage(imagePath);
```

Jika gambar beresolusi tinggi dan teksnya bersih, Anda akan mendapatkan hasil hampir sempurna. Untuk pemindaian yang berisik, pertimbangkan pra‑pemrosesan (misalnya, binarisasi) – Aspose menyediakan metode `PreprocessImage` yang dapat Anda jelajahi nanti.

---

## Langkah 4: Tampilkan atau Simpan Teks yang Diekstrak

Sebagian besar pengembang cukup mencetak hasil ke konsol saat pengujian. Dalam skenario produksi Anda mungkin menulis ke basis data atau file CSV.

```csharp
// Step 4: Show the OCR result
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(recognizedText);
```

Menjalankan program dengan contoh resi akan mencetak sesuatu seperti:

```
=== OCR Output ===
दिनांक: 09/01/2026
बिल no: 12345
रक्कम: ₹ 1,250.00
धन्यवाद!
```

Itulah bagian **mengonversi gambar menjadi teks** yang beraksi—tanpa transkripsi manual.

---

## Contoh Lengkap yang Berfungsi (Siap Salin‑Tempel)

Berikut adalah program lengkap yang berdiri sendiri. Tempelkan ke `Program.cs`, letakkan `hindi-receipt.png` di samping file `.exe` yang telah dikompilasi, dan tekan **Ctrl + F5**.

```csharp
// Program.cs
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

namespace HindiReceiptOcr
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize the OCR engine with Hindi language
            var ocrEngine = new OcrEngine
            {
                Language = OcrLanguage.Hindi
            };

            // 2️⃣ Path to the PNG receipt (adjust if needed)
            string imagePath = @"hindi-receipt.png";

            // 3️⃣ Run OCR – this will download the Hindi model on first run
            string recognizedText = ocrEngine.RecognizeImage(imagePath);

            // 4️⃣ Output the result – you can also write to a file or DB
            Console.WriteLine("=== OCR Output ===");
            Console.WriteLine(recognizedText);
        }
    }
}
```

### Output yang Diharapkan

Ketika gambar resi berisi karakter Hindi yang jelas, konsol akan menampilkan baris‑baris yang diekstrak, mempertahankan jeda baris. Jika OCR gagal mengenali sebuah kata, Anda akan melihat fragmen yang kacau—sebagai petunjuk untuk meningkatkan kualitas gambar atau menyesuaikan pra‑pemrosesan.

---

## Langkah 5: Lebih Lanjut – Ekstrak Teks dari Resi Secara Programatik

Jika tujuan Anda adalah **mengekstrak teks dari bidang resi** (tanggal, total, nomor faktur), Anda dapat memproses string OCR dengan ekspresi reguler:

```csharp
using System.Text.RegularExpressions;

// Example: pull the amount (₹) from the OCR result
var amountMatch = Regex.Match(recognizedText, @"रक्कम:\s*₹\s*([\d,]+\.\d{2})");
if (amountMatch.Success)
{
    Console.WriteLine($"Detected amount: {amountMatch.Groups[1].Value}");
}
```

---

## Kesalahan Umum & Cara Menghindarinya

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **Output kosong** | Jalur gambar salah atau file tidak disalin ke folder output. | Gunakan `Path.GetFullPath` dan pastikan file ada (`File.Exists`). |
| **Karakter sampah** | PNG beresolusi rendah atau warna terkompresi. | Perbesar gambar, atur DPI ke 300+, atau gunakan `ocrEngine.ImagePreprocessor`. |
| **Model bahasa tidak diunduh** | Tidak ada koneksi internet pada run pertama. | Pra‑unduh model Hindi melalui portal Aspose atau host secara lokal. |
| **Keterlambatan kinerja** | Memproses banyak halaman dalam loop tanpa membuang (dispose) objek. | Bungkus `OcrEngine` dalam blok `using` atau gunakan satu instance kembali. |

---

## Ilustrasi Gambar

![c# ocr tutorial reading Hindi text from PNG receipt](https://example.com/placeholder-image.png "c# ocr tutorial – read text from png receipt")

*The screenshot shows a Hindi receipt before and after OCR conversion.*

*Tangkap layar menunjukkan resi Hindi sebelum dan sesudah konversi OCR.*

---

## Ringkasan: Apa yang Telah Dibahas

- Siapkan aplikasi konsol C# dan tambahkan paket NuGet Aspose OCR.  
- Inisialisasi `OcrEngine` dengan model bahasa **recognize hindi text**.  
- **Read text from PNG** menggunakan `RecognizeImage`.  
- **Convert image to text** dan cetak hasilnya.  
- Menunjukkan pola sederhana untuk **extract text from receipt** fields.  

Semua ini disampaikan dalam satu file yang dapat dijalankan—tepat seperti yang seharusnya diberikan oleh **c# ocr tutorial**.

---

## Langkah Selanjutnya & Topik Terkait

1. **Batch processing** – iterasi melalui folder gambar resi dan simpan hasilnya ke CSV.  
2. **Pre‑processing** – jelajahi `ocrEngine.ImagePreprocessor` untuk penghilangan noise, koreksi kemiringan, atau peningkatan kontras.  
3. **Multi‑language OCR** – aktifkan `OcrLanguage.Multilingual` untuk menangani resi yang mencampur Hindi dan Inggris.  
4. **Integration** – dorong data yang diekstrak ke model Entity Framework Core untuk penyimpanan persisten.  

Jika Anda penasaran dengan salah satu topik ini, lihat tutorial kami tentang **convert image to text in C#** dan **extract structured data from OCR results**.

### Selamat Coding!

Jangan ragu meninggalkan komentar jika Anda mengalami kendala, atau bagikan bagaimana Anda memperluas **c# ocr tutorial** ini dalam proyek Anda sendiri. Ingat, OCR hanyalah langkah pertama—data bersih adalah tempat keajaiban sebenarnya terjadi. 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}