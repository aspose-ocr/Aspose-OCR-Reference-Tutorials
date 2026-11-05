---
category: general
date: 2026-03-21
description: Pelajari cara mengoreksi kemiringan file gambar dan mengenali teks gambar
  dengan Aspose OCR. Konversi jpg ke teks dan perbaiki rotasi gambar dalam beberapa
  baris kode C#.
draft: false
keywords:
- how to deskew image
- recognize text image
- convert jpg to text
- correct image rotation
- recognize text jpg
language: id
og_description: Cara menghilangkan kemiringan gambar dan mengekstrak teks dari JPEG
  menggunakan Aspose OCR. Ikuti panduan langkah demi langkah ini untuk mengubah jpg
  menjadi teks dan memperbaiki rotasi gambar.
og_title: Cara Mengoreksi Kemiringan Gambar di C# – Tutorial Cepat Aspose OCR
tags:
- OCR
- C#
- Aspose
title: Cara Menghilangkan Kemiringan Gambar di C# – Panduan Lengkap Menggunakan Aspose
  OCR
url: /id/net/skew-angle-calculation/how-to-deskew-image-in-c-complete-guide-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Mengoreksi Kemiringan Gambar di C# – Panduan Lengkap Menggunakan Aspose OCR

Pernah bertanya-tanya **bagaimana cara mengoreksi kemiringan gambar** yang dihasilkan dari pemindai dengan sudut aneh? Anda tidak sendirian—banyak pengembang mengalami masalah ini ketika mencoba mengekstrak teks dari kwitansi, faktur, atau catatan tulisan tangan. Kabar baiknya, dengan Aspose OCR Anda dapat memperbaiki rotasi gambar dan mengambil teks bersih yang dapat dicari hanya dalam beberapa baris kode.

Dalam tutorial ini kami akan membahas seluruh proses: mulai dari menginstal pustaka, mengaktifkan koreksi kemiringan otomatis, hingga mengenali gambar teks dan akhirnya mengonversi JPG menjadi teks. Pada akhir tutorial Anda akan memiliki aplikasi konsol siap‑jalankan yang **mengenali file jpg teks** tanpa harus memutar secara manual terlebih dahulu.

## Apa yang Anda Butuhkan

- **.NET 6.0** atau lebih baru (kode ini bekerja pada .NET Core dan .NET Framework)  
- Paket NuGet **Aspose.OCR for .NET** – versi 23.12 atau yang lebih baru disarankan  
- Contoh **JPEG miring** (misalnya `skewed_receipt.jpg`) yang ditempatkan di lokasi yang dapat dibaca aplikasi Anda  
- Visual Studio, VS Code, atau editor C# apa pun yang Anda sukai  

Tidak diperlukan alat pihak ketiga lainnya. Pustaka ini menangani koreksi kemiringan, OCR, dan bahkan deteksi bahasa secara internal.

![how to deskew image example](/images/deskew-example.png "how to deskew image using Aspose OCR")

## Langkah 1: Siapkan Proyek dan Instal Aspose.OCR

Agar tetap rapi, mulailah proyek konsol baru:

```bash
dotnet new console -n DeskewDemo
cd DeskewDemo
dotnet add package Aspose.OCR --version 23.12.0
```

Baris `dotnet add package` akan mengunduh binary **Aspose.OCR** beserta semua dependensi native. Jika Anda menggunakan Windows, DLL native akan diunduh secara otomatis; pada Linux/macOS Anda mungkin perlu paket `libgdiplus`, namun itu hanya instalasi satu kali.

## Langkah 2: Aktifkan Koreksi Kemiringan Otomatis (Perbaiki Rotasi Gambar)

Sekarang buka `Program.cs` dan ganti isinya dengan kode di bawah ini. Baris kunci di sini adalah `ocrEngine.Settings.Deskew = true;` – itu adalah flag yang memberi tahu mesin **bagaimana cara mengoreksi kemiringan gambar** secara otomatis.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

namespace DeskewDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // 1️⃣ Create an OCR engine (CPU mode is fine for most desktop apps)
            // -----------------------------------------------------------------
            var ocrEngine = new OcrEngine();

            // ---------------------------------------------------------------
            // 2️⃣ Turn on deskewing – this corrects image rotation for us
            // ---------------------------------------------------------------
            ocrEngine.Settings.Deskew = true;   // <-- how to deskew image is handled here

            // ---------------------------------------------------------------
            // 3️⃣ Point the engine at the JPEG you want to process
            // ---------------------------------------------------------------
            string imagePath = "YOUR_DIRECTORY/skewed_receipt.jpg";

            // ---------------------------------------------------------------
            // 4️⃣ Run OCR – the result already contains the corrected text
            // ---------------------------------------------------------------
            OcrResult ocrResult = ocrEngine.Recognize(imagePath);

            // ---------------------------------------------------------------
            // 5️⃣ Output the text – this is your “convert jpg to text” step
            // ---------------------------------------------------------------
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

### Mengapa Mengaktifkan Deskew?

Ketika pemindai memindai halaman dengan sudut, garis dasar teks menjadi miring. Mesin OCR tradisional akan membaca setiap karakter sebagai versi miring, yang secara dramatis menurunkan akurasi. Dengan mengatur `Deskew = true`, Aspose OCR menjalankan transformasi Hough cepat di balik layar, memutar bitmap kembali ke posisi horizontal, dan kemudian melakukan pengenalan. Hasilnya sama seperti jika Anda memutar gambar secara manual di Photoshop—hanya lebih cepat dan sepenuhnya otomatis.

## Langkah 3: Kenali Gambar Teks dan Konversi JPG menjadi Teks

Panggilan `Recognize` melakukan dua hal sekaligus:

1. **Mengoreksi kemiringan** gambar (karena flag telah diaktifkan).  
2. **Mengekstrak** konten teks, mengembalikannya dalam objek `OcrResult`.

Anda dapat memperlakukan `ocrResult.Text` sebagai string biasa, menuliskannya ke file, atau memasukkannya ke alur pemrosesan selanjutnya. Jika Anda membutuhkan skor kepercayaan mentah per kata, `ocrResult.Words` memberikan koleksi dengan nilai `Confidence`.

### Contoh Output

Dengan asumsi `skewed_receipt.jpg` berisi kwitansi sederhana, Anda mungkin melihat sesuatu seperti:

```
=== Recognized Text ===
Store: Coffee Corner
Date: 2026-03-20
Item   Qty   Price
Latte   2    5.00
Bagel   1    2.50
Total          12.50
```

Perhatikan bagaimana angka-angka teratur meskipun gambar asli diputar sekitar 7°. Itulah keajaiban **perbaikan rotasi gambar** yang dibangun dalam pustaka.

## Langkah 4: Menjalankan Contoh dan Memverifikasi Hasil

Kompilasi dan jalankan:

```bash
dotnet run
```

Jika semuanya terhubung dengan benar, Anda akan melihat teks yang diekstrak dicetak ke konsol. Jika Anda mendapatkan pengecualian seperti `FileNotFoundException`, periksa kembali jalur ke file JPEG Anda dan pastikan file dapat dibaca.

### Kesalahan Umum & Tips Pro

- **Gambar Besar** – Penggunaan memori OCR meningkat seiring dimensi gambar. Ubah ukuran file yang terlalu besar (mis., > 3000 px lebar) sebelum memasukkannya ke mesin.  
- **Skrip Non‑Latin** – Secara default mesin mengasumsikan bahasa Inggris. Atur `ocrEngine.Settings.Language = OcrLanguage.French;` (atau bahasa lain yang didukung) jika Anda perlu **mengenali gambar teks** dalam alfabet lain.  
- **Pemrosesan Batch** – Untuk banyak file, gunakan kembali instance `OcrEngine` yang sama; membuat mesin baru per file menambah beban yang tidak perlu.  
- **Pemeriksaan Kualitas** – Setelah koreksi kemiringan, Anda dapat mengekspor bitmap yang telah diperbaiki melalui `ocrEngine.Settings.DeskewedImage.Save("corrected.jpg");` untuk memverifikasi perbaikan rotasi secara visual.

## Contoh Lengkap yang Berfungsi (Semua Bersatu)

Berikut adalah program lengkap yang berdiri sendiri yang dapat Anda salin‑tempel ke `Program.cs`. Program ini mencakup komentar, penanganan error, dan langkah opsional untuk menyimpan gambar yang telah dikoreksi.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Settings;

namespace DeskewDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Path to the input JPEG – change this to your actual file location
            string inputPath = @"YOUR_DIRECTORY\skewed_receipt.jpg";

            if (!File.Exists(inputPath))
            {
                Console.WriteLine($"Error: File not found – {inputPath}");
                return;
            }

            try
            {
                // 1️⃣ Create OCR engine (CPU mode is sufficient for most scenarios)
                var ocrEngine = new OcrEngine();

                // 2️⃣ Enable automatic deskewing – this is the core of how to deskew image
                ocrEngine.Settings.Deskew = true;

                // Optional: Save the corrected image to verify the rotation fix
                // ocrEngine.Settings.DeskewedImagePath = "corrected.jpg";

                // 3️⃣ Perform OCR – this simultaneously deskews and extracts text
                OcrResult result = ocrEngine.Recognize(inputPath);

                // 4️⃣ Output the recognized text – effectively convert jpg to text
                Console.WriteLine("=== Recognized Text ===");
                Console.WriteLine(result.Text);
            }
            catch (Exception ex)
            {
                Console.WriteLine("An unexpected error occurred:");
                Console.WriteLine(ex.Message);
            }
        }
    }
}
```

Menjalankan program akan **mengenali file jpg teks**, secara otomatis memperbaiki kemiringan apa pun, dan mencetak teks bersih yang dapat dicari ke konsol.

## Kesimpulan

Anda kini memiliki potongan kode yang solid dan siap produksi yang menunjukkan **cara mengoreksi kemiringan gambar** dan mengekstrak isinya menggunakan Aspose OCR. Pendekatan ini bekerja untuk kwitansi, faktur, kontrak yang dipindai, atau JPEG apa pun di mana teks tidak sepenuhnya horizontal.

Langkah selanjutnya yang dapat Anda jelajahi:

- **Pemrosesan batch** folder JPEG dan menulis setiap hasil ke file `.txt` (kembali ke *konversi jpg ke teks*).  
- Mengintegrasikan langkah OCR ke dalam API ASP.NET Core sehingga klien dapat mengunggah gambar dan menerima teks berformat JSON.  
- Bereksperimen dengan pengaturan OCR yang berbeda seperti `ocrEngine.Settings.Language` atau `ocrEngine.Settings.RecognitionMode` untuk meningkatkan akurasi dokumen non‑Inggris.

Cobalah, sesuaikan pengaturannya, dan biarkan mesin melakukan pekerjaan berat. Seperti biasa, jika Anda menemui masalah atau memiliki optimasi cerdas untuk dibagikan, tinggalkan komentar di bawah. Selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}