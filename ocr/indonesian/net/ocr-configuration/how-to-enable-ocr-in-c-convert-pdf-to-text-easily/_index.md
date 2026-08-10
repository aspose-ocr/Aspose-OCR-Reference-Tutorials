---
category: general
date: 2026-02-27
description: Cara mengaktifkan OCR di C# untuk mengonversi PDF menjadi teks. Pelajari
  cara mengekstrak teks dari PDF multi‑bahasa menggunakan Aspose OCR.
draft: false
keywords:
- how to enable ocr
- convert pdf to text
- how to extract text
- how to recognize pdf
- recognize pdf text c#
language: id
og_description: Cara mengaktifkan OCR di C# dan mengonversi PDF ke teks. Panduan langkah
  demi langkah untuk mengekstrak dan mengenali teks PDF menggunakan Aspose OCR.
og_title: Cara Mengaktifkan OCR di C# – Mengonversi PDF ke Teks
tags:
- OCR
- C#
- PDF
- Aspose
title: Cara Mengaktifkan OCR di C# – Mengonversi PDF ke Teks dengan Mudah
url: /id/net/ocr-configuration/how-to-enable-ocr-in-c-convert-pdf-to-text-easily/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Mengaktifkan OCR di C# – Mengonversi PDF ke Teks dengan Mudah

Cara mengaktifkan OCR di C# adalah pertanyaan yang sering diajukan oleh banyak pengembang ketika mereka perlu mengekstrak teks dari PDF. Jika Anda pernah menatap faktur yang dipindai dan bertanya *“Bagaimana saya bisa mengekstrak teks itu tanpa mengetik ulang semuanya?”* maka Anda berada di tempat yang tepat. Dalam tutorial ini kami akan membimbing Anda melalui solusi lengkap yang siap dijalankan, yang tidak hanya menunjukkan **cara mengaktifkan OCR** tetapi juga mendemonstrasikan **cara mengonversi PDF ke teks**, **cara mengekstrak teks** dari dokumen multibahasa, dan **cara mengenali konten PDF** menggunakan C#.

Kami akan menggunakan pustaka Aspose.OCR, yang mendukung puluhan bahasa secara bawaan, sehingga Anda tidak perlu mengelola mesin terpisah untuk bahasa Inggris, Arab, Jepang, atau skrip lainnya. Pada akhir panduan ini Anda akan memiliki satu metode yang **mengenali teks PDF C#**, mencetaknya ke konsol, dan dapat disisipkan ke proyek .NET apa pun.

## Prasyarat – Apa yang Anda Butuhkan Sebelum Memulai

- .NET 6.0 SDK atau yang lebih baru (kode ini juga bekerja dengan .NET Core dan .NET Framework)
- Visual Studio 2022 (atau editor lain yang Anda sukai)
- Lisensi atau percobaan gratis **Aspose.OCR untuk .NET** – Anda dapat mengambil kunci sementara dari situs web Aspose.
- Contoh PDF yang berisi beberapa bahasa (kami akan menyebutnya `multilang.pdf`).

Jika Anda belum memiliki salah satu dari ini, unduh SDK dari situs Microsoft dan instal paket NuGet:

```bash
dotnet add package Aspose.OCR
```

Itu saja persiapannya. Siap? Mari kita mulai.

## Cara Mengaktifkan OCR di C# – Penyiapan dan Konfigurasi

Hal pertama yang harus Anda lakukan adalah membuat instance mesin OCR dan memberi tahu bahasa apa yang Anda harapkan. Inilah langkah **cara mengaktifkan OCR** yang menjadi dasar alur kerja selanjutnya.

```csharp
using Aspose.OCR;
using System;

public class OcrDemo
{
    public static void Main()
    {
        // Step 1: Instantiate the OCR engine
        var ocrEngine = new OcrEngine();

        // Step 2: Enable the languages you need (English, Arabic, Japanese)
        ocrEngine.Language = OcrLanguage.English |
                             OcrLanguage.Arabic |
                             OcrLanguage.Japanese;

        // Step 3: Recognize text from the PDF file
        string recognizedText = ocrEngine.RecognizeFromFile("YOUR_DIRECTORY/multilang.pdf");

        // Step 4: Output the extracted text
        Console.WriteLine(recognizedText);
    }
}
```

**Mengapa ini penting:** Dengan secara eksplisit mengatur properti `Language` Anda memberi petunjuk kepada mesin untuk mengalokasikan model karakter yang tepat, yang secara dramatis meningkatkan akurasi—terutama untuk PDF dengan skrip campuran. Melewatkan langkah ini (atau membiarkannya pada nilai default) akan membuat mesin menebak, yang sering menghasilkan output berantakan.

> **Tips profesional:** Jika Anda tahu dokumen Anda hanya berisi satu bahasa, batasi flag hanya pada bahasa tersebut. Ini dapat mempercepat pemrosesan hingga 30 %.

### Gambar – Ikhtisar Visual Mengaktifkan OCR  
![Tangkapan layar konfigurasi mesin OCR yang menunjukkan cara mengaktifkan OCR di C#](/images/enable-ocr-csharp.png)

*Alt text: Diagram yang menggambarkan cara mengaktifkan OCR di C# menggunakan Aspose.OCR.*

## Mengonversi PDF ke Teks dengan Aspose OCR

Setelah **cara mengaktifkan OCR** selesai, mari bahas konversi sebenarnya. Metode `RecognizeFromFile` melakukan pekerjaan berat: ia membuka PDF, menjalankan mesin OCR pada setiap halaman, dan mengembalikan satu string yang berisi semua karakter yang diekstrak.

### Apa yang Terjadi di Balik Layar?

1. **Rasterisasi halaman** – Setiap halaman PDF diubah menjadi bitmap, karena OCR bekerja pada gambar.
2. **Pemilihan model bahasa** – Berdasarkan flag yang Anda setel sebelumnya, mesin memilih jaringan saraf yang sesuai.
3. **Deteksi baris teks** – Mesin menemukan baris teks, bahkan ketika teks miring.
4. **Dekode karakter** – Akhirnya, pola piksel dipetakan ke karakter Unicode.

Karena metode ini mengembalikan string biasa, Anda dapat **mengonversi PDF ke teks** dalam satu baris kode. Jika Anda memerlukan pendekatan yang lebih terperinci (misalnya pemrosesan per halaman), Anda dapat memanggil `RecognizeFromStream` di dalam loop.

## Cara Mengekstrak Teks dari PDF Multi‑Bahasa

Misalkan PDF Anda berisi judul dalam bahasa Inggris, teks utama dalam bahasa Arab, dan catatan kaki dalam bahasa Jepang. Kode yang kami tunjukkan sebelumnya sudah menangani skenario tersebut, tetapi Anda mungkin bertanya **cara mengekstrak teks** hanya dari segmen bahasa tertentu.

Anda dapat memfilter hasil menggunakan operasi string sederhana atau ekspresi reguler. Berikut contoh cepat yang mengambil hanya bagian bahasa Inggris:

```csharp
using System.Text.RegularExpressions;

// After recognizing the whole document...
string allText = ocrEngine.RecognizeFromFile("YOUR_DIRECTORY/multilang.pdf");

// Regex to keep only ASCII characters (roughly English)
string englishOnly = Regex.Replace(allText, @"[^\u0000-\u007F]+", string.Empty);

Console.WriteLine("English extracted:");
Console.WriteLine(englishOnly);
```

**Mengapa memfilter?** Dalam banyak alur kerja bisnis Anda hanya membutuhkan bagian skrip Latin untuk pengindeksan, sementara sisanya disimpan di tempat lain. Pola ini menunjukkan **cara mengekstrak teks** secara efisien tanpa perlu melakukan OCR kedua.

## Cara Mengenali PDF – Menangani Kasus Edge

Bahkan mesin OCR terbaik sekalipun mengalami kesulitan pada PDF tertentu. Berikut adalah beberapa jebakan umum dan cara mengatasinya:

| Masalah | Gejala | Solusi |
|-------|---------|-----|
| Scan beresolusi rendah (<150 dpi) | Karakter hilang, kata berantakan | Praproses PDF dengan `ocrEngine.ImageProcessingOptions.Dpi = 300;` |
| Halaman terrotasi | Teks muncul miring | Atur `ocrEngine.PageSegmentationMode = PageSegmentationMode.AutoRotate;` |
| PDF dilindungi kata sandi | `RecognizeFromFile` melempar pengecualian | Sertakan kata sandi: `ocrEngine.RecognizeFromFile(path, "myPassword");` |
| File besar (>100 halaman) | Crash karena kehabisan memori | Proses secara bertahap: muat 10 halaman sekaligus dan gabungkan hasilnya. |

Menerapkan penyesuaian ini memastikan solusi Anda **mengenali PDF** secara andal, terlepas dari keanehan file.

```csharp
// Example of handling low‑resolution and rotation
ocrEngine.ImageProcessingOptions.Dpi = 300;
ocrEngine.PageSegmentationMode = PageSegmentationMode.AutoRotate;
```

## Recognize PDF Text C# – Contoh Lengkap yang Siap Pakai

Menggabungkan semua bagian, berikut program mandiri yang dapat Anda salin‑tempel ke aplikasi konsol. Program ini mendemonstrasikan **cara mengaktifkan OCR**, **mengonversi PDF ke teks**, **mengekstrak bagian bahasa tertentu**, dan **menangani kasus edge umum**.

```csharp
using Aspose.OCR;
using System;
using System.Text.RegularExpressions;

namespace PdfOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create OCR engine instance
            var ocrEngine = new OcrEngine();

            // 2️⃣ Enable languages (English, Arabic, Japanese)
            ocrEngine.Language = OcrLanguage.English |
                                 OcrLanguage.Arabic |
                                 OcrLanguage.Japanese;

            // Optional: improve accuracy for low‑res PDFs
            ocrEngine.ImageProcessingOptions.Dpi = 300;
            ocrEngine.PageSegmentationMode = PageSegmentationMode.AutoRotate;

            // 3️⃣ Path to your multi‑language PDF
            string pdfPath = @"C:\Docs\multilang.pdf";

            // 4️⃣ Recognize all text
            string fullText = ocrEngine.RecognizeFromFile(pdfPath);
            Console.WriteLine("=== Full extracted text ===");
            Console.WriteLine(fullText);
            Console.WriteLine();

            // 5️⃣ Extract only English (as an example of how to extract text)
            string englishOnly = Regex.Replace(fullText, @"[^\u0000-\u007F]+", string.Empty);
            Console.WriteLine("=== English‑only excerpt ===");
            Console.WriteLine(englishOnly);
        }
    }
}
```

**Output yang diharapkan** (dipotong untuk singkat):

```
=== Full extracted text ===
Welcome to our report…
مرحبا بكم في تقريرنا…
ようこそ、私たちのレポートへ…

=== English‑only excerpt ===
Welcome to our report...
```

Jalankan program, arahkan ke PDF Anda, dan Anda akan melihat konsol mencetak teks multibahasa lengkap serta potongan teks bahasa Inggris yang telah difilter.

## Pertanyaan Umum (dan Jawaban Cepat)

- **Apakah ini bekerja dengan .NET Framework 4.7?**  
  Ya. Paket NuGet Aspose.OCR menargetkan .NET Standard 2.0, yang kompatibel dengan .NET Core maupun .NET Framework.

- **Bagaimana jika saya perlu OCR gambar bukan PDF?**  
  Gunakan `ocrEngine.RecognizeFromImage("image.png")`. Flag bahasa yang sama tetap berlaku, jadi Anda tetap **cara mengaktifkan OCR** sekali saja.

- **Bisakah saya menulis output ke file .txt?**  
  Tentu. Ganti `Console.WriteLine(fullText);` dengan `File.WriteAllText("output.txt", fullText);`.

- **Apakah ada cara mendapatkan skor kepercayaan?**  
  Aspose.OCR menyediakan objek `OcrResult` dimana Anda dapat membaca `Confidence` per kata. Lihat dokumentasi API untuk `RecognizeFromFile(..., out OcrResult result)`.

## Kesimpulan

Kami telah membahas **cara mengaktifkan OCR** di C#, menunjukkan **cara mengonversi PDF ke teks**, menjelaskan **cara mengekstrak teks** dari bagian bahasa tertentu, dan mendemonstrasikan **cara mengenali PDF** secara andal menggunakan Aspose OCR. Kode lengkap yang dapat dijalankan di atas memberi Anda fondasi kuat untuk mengintegrasikan OCR ke dalam aplikasi .NET apa pun—baik Anda sedang membangun sistem manajemen dokumen, proses otomatis faktur, atau indeks pencarian multibahasa.

Langkah selanjutnya? Coba ubah flag bahasa untuk menyertakan Cina atau Korea, eksperimen dengan `ImageProcessingOptions` untuk pemindaian berisik, atau alirkan teks yang diekstrak ke pipeline pemrosesan bahasa alami. Semua ekstensi tersebut tetap bergantung pada prinsip inti yang sama: **cara mengaktifkan OCR** dengan benar di awal.

Selamat coding, semoga PDF Anda selalu dapat dicari!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}