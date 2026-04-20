---
category: general
date: 2026-02-11
description: Pelajari cara menjalankan OCR pada file TIFF multi‑halaman di C# menggunakan
  Aspose OCR. Konversi TIFF ke teks, ekstrak teks dari TIFF, dan kenali teks dari
  gambar dengan cepat.
draft: false
keywords:
- how to run OCR
- recognize text from image
- convert tiff to text
- extract text from tiff
- perform OCR on image
language: id
og_description: Cara menjalankan OCR pada TIFF multi‑halaman menggunakan Aspose OCR
  di C#. Panduan langkah demi langkah untuk mengonversi TIFF menjadi teks, mengekstrak
  teks dari TIFF, dan mengenali teks dari gambar.
og_title: Cara Menjalankan OCR pada Gambar TIFF Multi‑Halaman – Tutorial C# Lengkap
tags:
- OCR
- C#
- Aspose
- TIFF
title: Cara Menjalankan OCR pada Gambar TIFF Multi‑Halaman dengan Aspose OCR – Panduan
  C#
url: /id/net/text-recognition/how-to-run-ocr-on-multi-page-tiff-images-with-aspose-ocr-c-g/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menjalankan OCR pada Gambar TIFF Multi‑Halaman dengan Aspose OCR

Pernah bertanya-tanya **bagaimana cara menjalankan OCR** pada sebuah TIFF yang dipindai dan berisi beberapa halaman? Anda tidak sendirian—banyak pengembang mengalami masalah ini ketika mereka perlu mengambil teks yang dapat dicari dari dokumen lama. Kabar baiknya? Dengan Aspose OCR Anda dapat mengenali teks dari file gambar hanya dengan beberapa baris kode C#, dan Anda akan mendapatkan teks biasa yang digabungkan siap untuk diindeks atau diproses lebih lanjut.

Pada tutorial ini kami akan membahas seluruh alur kerja: mulai dari menginstal paket Aspose OCR, memuat TIFF multi‑halaman, mengonversi TIFF ke teks, dan akhirnya menampilkan konten yang diekstrak. Pada akhir tutorial Anda akan dapat **mengekstrak teks dari file TIFF**, **mengenali teks dari sumber gambar**, dan bahkan mengotomatisasi proses untuk puluhan file dalam pekerjaan batch. Tidak ada sulap, hanya langkah-langkah yang jelas dan praktis.

## Apa yang Akan Anda Pelajari

- Cara menyiapkan mesin Aspose OCR untuk pengenalan bahasa Inggris.  
- Kode tepat yang diperlukan untuk **mengonversi TIFF ke teks** menggunakan kelas `OcrEngine`.  
- Tips menangani gambar multi‑halaman dan memastikan setiap halaman dipisahkan dengan benar.  
- Kesalahan umum (seperti ketergantungan native yang hilang) dan cara menghindarinya.  

**Prasyarat** – Anda memerlukan .NET 6 atau yang lebih baru, Visual Studio (atau editor C# apa pun), dan koneksi internet untuk fitur unduhan sumber daya otomatis. Itu saja; tidak ada pustaka native tambahan yang harus dihadapi.

---

## Langkah 1 – Instal Paket NuGet Aspose OCR

Sebelum Anda dapat **melakukan OCR pada file gambar** Anda harus menambahkan pustaka ke proyek Anda.

```bash
dotnet add package Aspose.OCR
```

> **Tips pro:** Jika Anda bekerja di dalam Visual Studio, Anda juga dapat klik kanan proyek → *Manage NuGet Packages* → cari “Aspose.OCR” dan klik *Install*.

Paket ini mencakup semua yang Anda butuhkan, dan dengan `AutomaticResourceDownload = true` mesin akan mengambil paket bahasa secara otomatis.

---

## Langkah 2 – Inisialisasi Mesin OCR (Cara Menjalankan OCR)

Sekarang paket sudah terpasang, kami membuat dan mengonfigurasi sebuah instance `OcrEngine`. Ini adalah inti dari **cara menjalankan OCR** dalam skenario kami.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System.Drawing;   // For Image class
using System;

// Step 2: Create and configure the OCR engine
var ocrEngine = new OcrEngine
{
    Language = OcrLanguage.English,          // Recognize English text
    AutomaticResourceDownload = true,        // Auto‑download language data
    OutputFormat = OcrOutputFormat.Text      // Get plain concatenated text
};
```

**Mengapa ini penting:** Menetapkan `Language` memberi tahu mesin set karakter apa yang diharapkan, sementara `AutomaticResourceDownload` menghindarkan Anda dari menempatkan file bahasa secara manual di server. `OutputFormat` sebagai `Text` memberi kita string sederhana—sempurna untuk alur kerja **mengonversi TIFF ke teks**.

---

## Langkah 3 – Muat TIFF Multi‑Halaman (Mengenali Teks dari Gambar)

Sebuah TIFF dapat berisi banyak frame, masing‑masing mewakili sebuah halaman. Kelas `System.Drawing.Image` mengabstraksikannya untuk kami.

```csharp
// Step 3: Load the multi‑page image to be processed
using (var image = Image.FromFile("YOUR_DIRECTORY/multi_page.tiff"))
{
    // Step 4: Run OCR on the image
    var ocrResult = ocrEngine.Recognize(image);

    // Step 5: Display the extracted text
    Console.WriteLine(ocrResult.Text);
}
```

> **Bagaimana jika file tidak berada di folder yang sama?** Cukup berikan path absolut lengkap atau gunakan `Path.Combine` dengan `AppContext.BaseDirectory`.  
> **Bagaimana dengan penggunaan memori?** Pernyataan `using` membuang gambar setelah diproses, mencegah kebocoran—penting saat Anda memproses batch puluhan TIFF besar.

Panggilan `Recognize` secara otomatis mengiterasi setiap halaman dalam TIFF, menggabungkan hasil dengan jeda baris. Itulah mengapa Anda akan melihat setiap halaman terpisah ketika mencetak `ocrResult.Text`.

---

## Langkah 4 – Contoh Kerja Penuh (Semua Langkah dalam Satu File)

Berikut ini adalah aplikasi konsol lengkap yang siap dijalankan. Salin‑tempel ke dalam proyek konsol .NET baru dan tekan **F5**.

```csharp
// File: Program.cs
using System;
using System.Drawing;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace TiffOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Configure the OCR engine
            var ocrEngine = new OcrEngine
            {
                Language = OcrLanguage.English,
                AutomaticResourceDownload = true,
                OutputFormat = OcrOutputFormat.Text
            };

            // 2️⃣ Load your multi‑page TIFF (replace with your actual path)
            const string tiffPath = @"YOUR_DIRECTORY\multi_page.tiff";

            if (!System.IO.File.Exists(tiffPath))
            {
                Console.WriteLine($"File not found: {tiffPath}");
                return;
            }

            // 3️⃣ Perform OCR
            using (var image = Image.FromFile(tiffPath))
            {
                var result = ocrEngine.Recognize(image);

                // 4️⃣ Output the extracted text
                Console.WriteLine("=== OCR RESULT ===");
                Console.WriteLine(result.Text);
                Console.WriteLine("==================");
            }

            // Keep console open
            Console.WriteLine("Press any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**Output yang diharapkan** (dipotong untuk singkat):

```
=== OCR RESULT ===
Page 1: The quick brown fox jumps over the lazy dog.
Page 2: Lorem ipsum dolor sit amet, consectetur adipiscing elit.
...
==================
Press any key to exit...
```

Setiap halaman muncul pada baris terpisah karena `OcrOutputFormat.Text` menyisipkan jeda baris antara frame. Jika Anda membutuhkan pemisah yang berbeda, Anda dapat memproses `result.Text` dengan `String.Replace`.

---

## Langkah 5 – Menangani Kasus Tepi Umum

### 5.1 File TIFF Besar  
Ketika menangani TIFF berukuran gigabyte, memuat seluruh file ke memori dapat menjadi masalah. Solusinya adalah memproses setiap frame secara terpisah:

```csharp
using (var image = Image.FromFile(tiffPath))
{
    for (int i = 0; i < image.GetFrameCount(FrameDimension.Page); i++)
    {
        image.SelectActiveFrame(FrameDimension.Page, i);
        var pageResult = ocrEngine.Recognize(image);
        Console.WriteLine($"--- Page {i + 1} ---");
        Console.WriteLine(pageResult.Text);
    }
}
```

### 5 Dokumen Non‑Inggris  
Jika Anda perlu **mengenali teks dari gambar** dalam bahasa Spanyol atau Prancis, cukup ubah properti `Language`:

```csharp
ocrEngine.Language = OcrLanguage.Spanish; // or OcrLanguage.French
```

Aspose akan secara otomatis mengunduh sumber daya bahasa yang sesuai.

### 5 Menyimpan Output  
Seringkali Anda ingin **mengonversi TIFF ke teks** dan menyimpan hasilnya dalam file `.txt`:

```csharp
System.IO.File.WriteAllText("output.txt", ocrResult.Text);
```

Anda juga dapat memisahkan output per halaman menggunakan `String.Split(Environment.NewLine)` dan menulis setiap bagian ke file terpisah.

---

## Tips Pro & Hal-hal yang Perlu Diwaspadai

- **AutomaticResourceDownload** berfungsi pada pertama kali Anda menjalankan aplikasi; run berikutnya dapat offline.  
- Jika Anda melihat karakter kacau, periksa kembali pengaturan `Language`; paket bahasa yang tidak cocok menyebabkan pengenalan yang salah.  
- Untuk PDF yang telah diraster menjadi TIFF, Anda mungkin ingin meningkatkan `ocrEngine.Dpi` (default 300) untuk akurasi lebih baik.  
- Selalu bungkus `Image.FromFile` dalam blok `using`; jika tidak, Anda akan mengunci file dan tidak dapat menghapus atau memindahkannya nanti.

---

## Pertanyaan yang Sering Diajukan

**Q: Apakah ini bekerja dengan TIFF satu‑halaman?**  
A: Tentu saja. Mesin memperlakukan TIFF satu‑frame dengan cara yang sama; Anda hanya akan mendapatkan satu baris teks.

**Q: Bisakah saya memproses file PNG atau JPEG dengan cara yang sama?**  
A: Ya—cukup ubah ekstensi file. Metode `Recognize` menerima format `System.Drawing.Image` apa pun.

**Q: Bagaimana jika saya membutuhkan hasil OCR sebagai PDF bukan teks biasa?**  
A: Atur `OutputFormat = OcrOutputFormat.Pdf` dan `ocrResult` akan berisi array byte PDF yang dapat Anda tulis ke disk.

---

## Kesimpulan

Anda kini memiliki solusi lengkap end‑to‑end untuk **cara menjalankan OCR** pada file TIFF multi‑halaman menggunakan Aspose OCR dalam C#. Dengan mengonfigurasi mesin, memuat gambar, dan memanggil `Recognize`, Anda dapat **mengekstrak teks dari TIFF**, **mengonversi TIFF ke teks**, dan **mengenali teks dari gambar** hanya dengan beberapa baris kode. Silakan menyesuaikan bahasa, format output, atau pemrosesan frame‑per‑frame sesuai kebutuhan batch‑processing Anda.

Siap untuk langkah selanjutnya? Cobalah menggabungkan pendekatan ini dengan layanan folder‑watcher untuk secara otomatis **melakukan OCR pada file gambar** saat mereka masuk ke folder drop, atau integrasikan output ke dalam indeks pencarian untuk pencarian teks penuh instan. Kemungkinannya tidak terbatas, dan kode yang baru saja Anda lihat adalah fondasi yang kuat.

Jika Anda mengalami kendala, tinggalkan komentar di bawah atau hubungi saya di GitHub. Selamat coding, dan nikmati mengubah TIFF yang membandel menjadi teks yang dapat dicari!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}