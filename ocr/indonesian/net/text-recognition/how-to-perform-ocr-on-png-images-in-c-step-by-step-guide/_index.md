---
category: general
date: 2026-03-29
description: Cara melakukan OCR di C# dan membaca teks dari file PNG. Pelajari cara
  mengekstrak teks Rusia, membaca teks dari PNG, dan cara mengekstrak teks menggunakan
  Aspose OCR.
draft: false
keywords:
- how to perform ocr
- read text from png
- how to extract text
- extract russian text
- c# ocr tutorial
language: id
og_description: Cara melakukan OCR di C# dengan Aspose OCR. Panduan ini menunjukkan
  cara membaca teks dari PNG, mengekstrak teks Rusia, dan mengimplementasikan solusi
  OCR C# lengkap.
og_title: Cara Melakukan OCR di C# – Ekstraksi Teks PNG Lengkap
tags:
- OCR
- C#
- Aspose
title: Cara Melakukan OCR pada Gambar PNG di C# – Panduan Langkah demi Langkah
url: /id/net/text-recognition/how-to-perform-ocr-on-png-images-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Melakukan OCR pada Gambar PNG di C# – Tutorial Lengkap

Pernah perlu **melakukan OCR** pada screenshot atau dokumen yang dipindai tetapi tidak yakin harus mulai dari mana di C#? Anda tidak sendirian. Para pengembang sering bertanya, “Bagaimana cara membaca teks dari file PNG tanpa mengirimnya ke layanan eksternal?” Kabar baiknya, dengan Aspose.OCR Anda dapat **mengekstrak teks Rusia**, **membaca teks dari png**, dan mendapatkan string bersih kembali hanya dalam beberapa baris kode.

Dalam tutorial ini kami akan membahas semua yang Anda perlukan: menyiapkan pustaka, memilih model bahasa yang tepat, menjalankan pengenalan, dan menangani jebakan umum. Pada akhir tutorial Anda akan dapat **cara mengekstrak teks** dari gambar PNG apa pun, baik itu bahasa Inggris, Rusia, atau salah satu dari 70+ bahasa yang didukung Aspose. Tanpa basa‑basi, hanya contoh praktis yang dapat dijalankan langsung di aplikasi console Anda.

---

## Apa yang Akan Anda Pelajari

- Menginstal dan mereferensikan paket NuGet Aspose.OCR.
- Menginisialisasi mesin OCR dalam mode auto‑download default.
- Mengonfigurasi mesin untuk **mengekstrak teks Rusia** menggunakan model bahasa Cyrillic.
- Menjalankan OCR pada file PNG lokal dan menampilkan hasilnya.
- Tips untuk memecahkan masalah file bahasa yang hilang dan meningkatkan akurasi.

**Prasyarat**: .NET 6+ (atau .NET Framework 4.7.2+), Visual Studio 2022 atau VS Code, dan koneksi internet untuk menjalankan pertama kali (model bahasa diunduh secara otomatis).

---

## Langkah 1 – Instal Paket Aspose.OCR

Untuk memulai, tambahkan pustaka Aspose.OCR ke proyek Anda. Buka terminal di folder proyek dan jalankan:

```bash
dotnet add package Aspose.OCR
```

Atau, jika Anda lebih suka UI Visual Studio, klik kanan **Dependencies → Manage NuGet Packages**, cari **Aspose.OCR**, dan klik **Install**.

> **Pro tip**: Paket ini hanya berukuran beberapa megabyte, dan model bahasa diunduh sesuai permintaan, sehingga Anda tidak akan menambah beban aplikasi dengan file yang tidak diperlukan.

---

## Langkah 2 – Inisialisasi Mesin OCR (Kata Kunci Utama dalam Aksi)

Membuat mesin sangat mudah. Konstruktor secara otomatis mengaktifkan *mode auto‑download*, yang berarti pertama kali Anda meminta bahasa yang belum ada secara lokal, Aspose akan mengunduhnya untuk Anda.

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize the OCR engine – it will download missing models automatically.
        var ocrEngine = new OcrEngine();

        // 2️⃣ Choose the language model – Russian Cyrillic (downloads if missing).
        ocrEngine.Language = Language.RussianCyrillic;

        // 3️⃣ Run OCR on the PNG image.
        var ocrResult = ocrEngine.RecognizeImage("sample_russian.png");

        // 4️⃣ Output the recognized text.
        Console.WriteLine(ocrResult.Text);
    }
}
```

> **Mengapa ini penting**: Dengan menggunakan mode auto‑download default Anda menghindari penanganan file manual. Jika nanti Anda perlu **membaca teks dari png** dalam bahasa lain, cukup ubah `Language.RussianCyrillic` ke nilai enum yang sesuai.

---

## Langkah 3 – Siapkan Gambar PNG Anda

Pastikan gambar yang ingin diproses dapat diakses saat runtime. Letakkan `sample_russian.png` di folder yang sama dengan file `.exe` yang telah dikompilasi, atau gunakan path absolut jika Anda lebih suka. Gambar harus berupa pemindaian atau screenshot yang jelas; akurasi OCR turun drastis pada PNG yang buram atau terlalu terkompresi.

**Kasus tepi umum**: Jika PNG berisi beberapa bahasa, Anda dapat mengatur `ocrEngine.Language = Language.Multilingual;` agar mesin mendeteksi setiap blok secara otomatis.

---

## Langkah 4 – Jalankan Aplikasi dan Verifikasi Output

Kompilasi dan jalankan program:

```bash
dotnet run
```

Anda akan melihat teks Rusia yang diekstrak tercetak di console, misalnya:

```
Привет, мир! Это пример текста на русском языке.
```

Jika Anda mendapatkan string kosong, periksa kembali:

1. Path file sudah benar.
2. Gambar tidak seluruhnya putih atau seluruhnya hitam.
3. Model bahasa berhasil diunduh (cari folder `Aspose.OCR` di bawah profil pengguna Anda).

---

## Langkah 5 – Penyesuaian Lanjutan untuk Akurasi Lebih Baik

Meskipun pengaturan default bekerja untuk kebanyakan kasus, Anda mungkin ingin menyempurnakan mesin:

| Pengaturan | Fungsinya | Kapan digunakan |
|------------|-----------|-----------------|
| `ocrEngine.PreprocessOptions.Deskew = true;` | Mengoreksi rotasi ringan | Dokumen yang dipindai tidak sejajar sempurna |
| `ocrEngine.PreprocessOptions.RemoveNoise = true;` | Menyaring bintik latar belakang | PNG berkualitas rendah dari kamera ponsel |
| `ocrEngine.RecognitionOptions.CharWhitelist = "0123456789";` | Membatasi karakter hanya angka | Mengekstrak nomor dari faktur |

Tambahkan salah satu atau semua sebelum memanggil `RecognizeImage`:

```csharp
ocrEngine.PreprocessOptions.Deskew = true;
ocrEngine.PreprocessOptions.RemoveNoise = true;
```

---

## Langkah 6 – Mengekspor Hasil ke File (Opsional)

Jika Anda perlu **cara mengekstrak teks** ke dalam file untuk diproses nanti, cukup tulis hasilnya ke disk:

```csharp
System.IO.File.WriteAllText("ocr_output.txt", ocrResult.Text);
Console.WriteLine("OCR output saved to ocr_output.txt");
```

Sekarang Anda memiliki salinan persisten yang dapat dimasukkan ke basis data, indeks pencarian, atau mesin terjemahan.

---

## Pertanyaan yang Sering Diajukan

**T: Apakah ini bekerja dengan format gambar lain seperti JPEG atau BMP?**  
J: Tentu saja. `RecognizeImage` menerima format apa pun yang didukung oleh pustaka `System.Drawing` .NET, termasuk JPEG, BMP, dan TIFF.

**T: Bagaimana jika saya perlu mengekstrak teks Inggris dalam satu proses yang sama?**  
J: Buat instance `OcrEngine` kedua dengan `Language.English` atau ubah properti bahasa di antara pemanggilan.

**T: Bisakah saya menjalankan OCR di API web tanpa memblokir thread utama?**  
J: Ya. Bungkus panggilan pengenalan dalam `Task.Run` atau gunakan overload async `RecognizeImageAsync` (tersedia pada versi Aspose yang lebih baru).

**T: Apakah ada batas ukuran PNG?**  
J: Pustaka dapat menangani gambar berukuran besar, tetapi penggunaan memori meningkat seiring resolusi. Jika Anda menemui `OutOfMemoryException`, pertimbangkan untuk menurunkan skala gambar terlebih dahulu.

---

## Contoh Lengkap yang Siap Pakai (Copy‑Paste)

Berikut program lengkap yang dapat Anda tempel ke proyek console baru (`dotnet new console`) dan jalankan segera setelah menginstal paket NuGet.

```csharp
// File: Program.cs
using System;
using Aspose.OCR;

namespace OcrDemo
{
    class Program
    {
        static void Main()
        {
            // Initialize OCR engine – auto‑download enabled.
            var ocrEngine = new OcrEngine();

            // Choose Russian Cyrillic language model.
            ocrEngine.Language = Language.RussianCyrillic;

            // Optional: improve accuracy for skewed or noisy images.
            ocrEngine.PreprocessOptions.Deskew = true;
            ocrEngine.PreprocessOptions.RemoveNoise = true;

            // Path to the PNG file you want to read.
            string imagePath = "sample_russian.png";

            // Perform OCR.
            OcrResult result = ocrEngine.RecognizeImage(imagePath);

            // Output the recognized text.
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(result.Text);

            // Save to a text file for later use.
            System.IO.File.WriteAllText("ocr_output.txt", result.Text);
            Console.WriteLine("Result saved to ocr_output.txt");
        }
    }
}
```

**Output console yang diharapkan** (asumsi contoh berisi frasa “Привет, мир!”):

```
=== OCR Result ===
Привет, мир! Это пример текста на русском языке.
Result saved to ocr_output.txt
```

---

## Kesimpulan

Kami telah membahas **cara melakukan OCR** pada gambar PNG menggunakan C#, mulai dari instalasi Aspose.OCR hingga menyesuaikan opsi pra‑pemrosesan dan mengekspor hasil. Sekarang Anda tahu cara **membaca teks dari png**, **cara mengekstrak teks** dalam berbagai bahasa, dan khususnya **mengekstrak teks Rusia** dengan kode yang minimal.

Siap untuk tantangan berikutnya? Cobalah mengirim output OCR ke pustaka deteksi bahasa, atau gabungkan dengan Azure Cognitive Services untuk terjemahan. Langit adalah batasnya ketika Anda memadukan mesin OCR yang handal dengan ekosistem kuat C#.

Jika Anda menemukan **tutorial c# ocr** ini bermanfaat, beri bintang, bagikan kepada rekan tim, atau tinggalkan komentar dengan tips Anda sendiri. Selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}