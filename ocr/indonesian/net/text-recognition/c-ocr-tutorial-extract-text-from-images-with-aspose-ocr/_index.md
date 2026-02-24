---
category: general
date: 2026-02-24
description: Tutorial OCR C# yang menunjukkan cara mengekstrak teks dari gambar menggunakan
  Aspose OCR – panduan lengkap, langkah demi langkah untuk pengembang .NET.
draft: false
keywords:
- c# ocr tutorial
- how to extract text from image
- Aspose OCR C#
- OCR region of interest
- image text extraction C#
language: id
og_description: tutorial c# ocr yang menunjukkan cara mengekstrak teks dari gambar
  menggunakan Aspose OCR – panduan lengkap, langkah demi langkah untuk pengembang
  .NET
og_title: 'tutorial OCR c#: Ekstrak Teks dari Gambar dengan Aspose OCR'
tags:
- C#
- OCR
- Aspose
- Image Processing
title: 'c# tutorial OCR: Ekstrak Teks dari Gambar dengan Aspose OCR'
url: /id/net/text-recognition/c-ocr-tutorial-extract-text-from-images-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr tutorial – Ekstrak Teks dari Gambar Menggunakan Aspose OCR

Pernah bertanya-tanya bagaimana cara mengekstrak teks dari file gambar dalam aplikasi C#? Anda tidak sendirian. Dalam banyak proyek dunia nyata—misalnya pemindai paspor, pemroses faktur, atau bahkan pembaca struk sederhana—mendapatkan hasil OCR yang dapat diandalkan adalah tantangan harian.  

Tutorial **c# ocr tutorial** ini akan memandu Anda melalui solusi praktis dengan Aspose OCR, menunjukkan secara tepat **cara mengekstrak teks dari gambar**, membatasi pemindaian ke area yang diinginkan, dan menampilkan hasilnya—semua dalam beberapa baris kode.  

Kami akan membahas semua yang Anda perlukan: paket NuGet, pernyataan `using` yang diperlukan, penyiapan ROI, konfigurasi opsi, dan pemeriksaan cepat atas output. Pada akhir tutorial, Anda akan memiliki aplikasi console yang dapat dijalankan untuk mengambil nama dari pemindaian paspor (atau gambar apa pun yang Anda tunjuk). Tanpa basa‑basi, hanya jawaban yang jelas dan lengkap yang dapat Anda salin‑tempel dan jalankan.

## Prasyarat

Sebelum kita mulai, pastikan Anda memiliki:

- .NET 6+ SDK (atau .NET Framework 4.7+ jika Anda lebih suka runtime lama)
- Visual Studio 2022 atau editor apa pun yang mendukung C#
- Akses internet untuk mengunduh paket NuGet **Aspose.OCR**
- File gambar (misalnya `passport_scan.png`) yang berisi teks yang dapat dibaca

> **Pro tip:** Jika Anda bereksperimen secara lokal, letakkan file PNG atau JPEG kecil ke dalam folder bernama `Images` di dalam proyek Anda – ini membuat path pendek dan kode lebih rapi.

## Langkah 1: Instal Aspose OCR dan Tambahkan Namespace

Hal pertama yang harus dilakukan adalah menginstal pustaka OCR. Buka terminal Anda (atau Package Manager Console) dan jalankan:

```bash
dotnet add package Aspose.OCR
```

Setelah paket terpasang, tambahkan direktif `using` yang diperlukan di bagian atas `Program.cs` Anda:

```csharp
using Aspose.OCR;          // Core OCR engine
using System.Drawing;     // Rectangle struct for ROI
```

Kedua baris ini memberi Anda akses ke `OcrEngine`, `OcrOptions`, dan tipe `Rectangle` yang akan kita gunakan untuk membatasi area pemindaian.

## Langkah 2: Buat Instance OcrEngine

Engine adalah inti dari proses. Anggaplah sebagai “otak” yang membaca piksel dan mengubahnya menjadi karakter. Inisialisasinya sangat sederhana:

```csharp
// Step 2: Instantiate the OCR engine – this object does the heavy lifting.
OcrEngine ocrEngine = new OcrEngine();
```

> **Mengapa ini penting:** Satu `OcrEngine` dapat dipakai ulang untuk beberapa gambar, yang menghemat memori dan menghindari pemeriksaan lisensi berulang.

## Langkah 3: Definisikan Region of Interest (ROI)

Memindai seluruh gambar resolusi tinggi dapat sia‑sia, terutama bila Anda sudah tahu persis di mana teks berada (misalnya, bidang nama pada paspor). Dengan menentukan **region of interest**, Anda memberi tahu engine untuk mengabaikan semua yang berada di luar persegi panjang.

```csharp
// Step 3: Set the ROI – adjust X, Y, Width, Height to match your image layout.
Rectangle regionOfInterest = new Rectangle(150, 300, 800, 200);
```

- **X** dan **Y** mewakili sudut kiri‑atas persegi panjang.
- **Width** dan **Height** menentukan ukuran kotak.

Jika Anda tidak yakin dengan angka pastinya, lakukan tes visual cepat dengan editor gambar apa pun (seperti Paint.NET) untuk menemukan koordinatnya.

## Langkah 4: Konfigurasikan OcrOptions dan Lampirkan ROI

Sekarang kita mengikat ROI ke objek `OcrOptions`. Objek ini juga memungkinkan Anda menyesuaikan bahasa, kecepatan deteksi, dan lain‑lain, tetapi untuk tutorial ini kita tetap minimal.

```csharp
// Step 4: Prepare OCR options and assign the ROI we just defined.
OcrOptions ocrOptions = new OcrOptions { Roi = regionOfInterest };
```

> **Kasus tepi:** Jika Anda menghilangkan ROI, Aspose OCR akan memindai seluruh gambar, yang dapat meningkatkan waktu pemrosesan dan menghasilkan noise tambahan pada hasil.

## Langkah 5: Jalankan OcrEngine pada Gambar Anda

Setelah semuanya terhubung, saatnya melakukan pengenalan teks sebenarnya. Berikan path ke gambar Anda dan opsi yang baru saja kita buat.

```csharp
// Step 5: Perform OCR on the target image using the configured options.
OcrResult ocrResult = ocrEngine.RecognizeImage(
    "Images/passport_scan.png", // Adjust this path to your file location
    ocrOptions);
```

Metode ini mengembalikan objek `OcrResult` yang berisi string yang diekstrak, skor kepercayaan, dan bahkan kotak pembatas untuk setiap kata (jika Anda membutuhkannya nanti).

## Langkah 6: Tampilkan Teks yang Diekstrak

Akhirnya, tampilkan hasilnya. Dalam aplikasi nyata Anda mungkin menyimpannya ke basis data, tetapi untuk tutorial ini output console sederhana sudah cukup.

```csharp
// Step 6: Show the extracted text in the console.
Console.WriteLine("Extracted name: " + ocrResult.Text);
```

Saat Anda menjalankan program, Anda akan melihat sesuatu seperti:

```
Extracted name: JOHN DOE
```

Jika output kosong atau berantakan, periksa kembali koordinat ROI dan pastikan gambar sumber jelas (kontras tinggi, blur minimal).

## Contoh Lengkap yang Berfungsi

Berikut adalah seluruh file `Program.cs` yang siap dikompilasi. Simpan dalam proyek console, letakkan gambar Anda di folder `Images`, dan tekan **F5**.

```csharp
using Aspose.OCR;
using System.Drawing;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create an OCR engine instance
            OcrEngine ocrEngine = new OcrEngine();

            // Step 2: Define the region of interest (ROI) where the text is expected
            // (x, y, width, height) – adjust these values for your own image
            Rectangle regionOfInterest = new Rectangle(150, 300, 800, 200);

            // Step 3: Prepare OCR options and assign the ROI
            OcrOptions ocrOptions = new OcrOptions { Roi = regionOfInterest };

            // Step 4: Perform OCR on the target image using the configured options
            OcrResult ocrResult = ocrEngine.RecognizeImage(
                "Images/passport_scan.png",
                ocrOptions);

            // Step 5: Display the extracted text
            Console.WriteLine("Extracted name: " + ocrResult.Text);
        }
    }
}
```

> **Output yang diharapkan:**  
> `Extracted name: JOHN DOE` (atau teks apa pun yang berada di ROI yang Anda tentukan).

## Pertanyaan Umum & Kasus Tepi

### Bagaimana jika gambar saya berformat berbeda?

Aspose OCR mendukung PNG, JPEG, BMP, TIFF, bahkan PDF. Cukup ubah ekstensi file pada path; engine akan mendeteksi format secara otomatis.

### Bisakah saya memproses banyak gambar dalam loop?

Tentu saja. `OcrEngine` dapat dipakai ulang:

```csharp
foreach (var file in Directory.GetFiles("Images", "*.png"))
{
    var result = ocrEngine.RecognizeImage(file, ocrOptions);
    Console.WriteLine($"{Path.GetFileName(file)} → {result.Text}");
}
```

### Bagaimana cara meningkatkan akurasi untuk skrip non‑Latin?

Setel properti bahasa pada `OcrOptions`:

```csharp
ocrOptions.Language = Language.English; // or Language.Russian, Language.ChineseSimplified, etc.
```

### Bagaimana jika ROI salah dan saya kehilangan teks?

Anda dapat memperbesar persegi panjang atau menghilangkan ROI sepenuhnya agar engine memindai seluruh gambar. Ingat bahwa memindai gambar penuh dapat meningkatkan waktu pemrosesan.

## Pro Tips untuk Pengalaman Lancar

- **Cache engine:** Membuat `OcrEngine` baru untuk setiap gambar menambah overhead. Pertahankan satu instance selama aplikasi berjalan.
- **Pra‑proses gambar:** Langkah sederhana seperti mengubah ke grayscale atau meningkatkan kontras dapat secara dramatis meningkatkan tingkat pengenalan.
- **Tangani hasil null:** Selalu periksa `ocrResult?.Text` sebelum menggunakannya untuk menghindari `NullReferenceException`.
- **Lisensi penting:** Versi gratis menambahkan watermark setelah 200 karakter pertama. Daftarkan lisensi percobaan atau komersial jika Anda membutuhkan output produksi.

## Langkah Selanjutnya

Setelah menguasai dasar‑dasar **c# ocr tutorial**, pertimbangkan untuk mengeksplor:

- **Cara mengekstrak teks dari gambar** secara massal (pemrosesan batch)
- Menggunakan **Aspose OCR** untuk mendeteksi tabel atau data terstruktur
- Mengintegrasikan hasil OCR dengan basis data atau API web
- Menggabungkan OCR dengan pustaka **pra‑proses gambar** seperti `OpenCvSharp`

Masing‑masing topik ini membangun di atas fondasi yang baru saja Anda buat, memungkinkan Anda mengubah pemindaian mentah menjadi data yang dapat dicari dan diproses.

---

*Siap menerapkan ini ke produksi? Ambil source lengkap dari repositori GitHub saya, sesuaikan ROI untuk dokumen Anda, dan saksikan teks muncul seolah‑olah sihir.*  

Selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}