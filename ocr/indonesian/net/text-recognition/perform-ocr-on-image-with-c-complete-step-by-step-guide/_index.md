---
category: general
date: 2026-05-21
description: Lakukan OCR pada gambar menggunakan C#. Pelajari cara memuat gambar untuk
  OCR, mengekstrak teks dari PNG, dan mengenali teks dari gambar dengan contoh kode
  kecil.
draft: false
keywords:
- perform OCR on image
- extract text from PNG
- recognize text from image
- load image for OCR
language: id
og_description: Lakukan OCR pada gambar di C# dengan cepat. Panduan ini menunjukkan
  cara memuat gambar untuk OCR, mengekstrak teks dari PNG, dan mengenali teks dari
  gambar dengan output HTML yang memperhatikan tata letak.
og_title: Lakukan OCR pada Gambar dengan C# – Tutorial Pemrograman Lengkap
schemas:
- author: Aspose
  dateModified: '2026-05-21'
  description: Perform OCR on image using C#. Learn how to load image for OCR, extract
    text from PNG, and recognize text from image with a tiny code sample.
  headline: Perform OCR on Image with C# – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Perform OCR on image using C#. Learn how to load image for OCR, extract
    text from PNG, and recognize text from image with a tiny code sample.
  name: Perform OCR on Image with C# – Complete Step‑by‑Step Guide
  steps:
  - name: Load Image for OCR
    text: The line `engine.Image = ImageStream.FromFile("YOUR_DIRECTORY/form.png");`
      is where we **load image for OCR**. The `ImageStream` helper abstracts away
      file‑format details, so you can feed JPEG, BMP, or TIFF without changing code.
  - name: Extract Text from PNG
    text: 'Once `engine.Recognize()` finishes, the OCR engine holds the recognized
      text internally. You can pull it out as a string if you only need raw text:'
  - name: Recognize Text from Image
    text: 'The `Recognize()` call does the heavy lifting. Under the hood the engine:'
  - name: Handling Layout‑Aware HTML Output
    text: 'Most developers stop at plain text, but the `HtmlSaveOptions` we used let
      you **perform OCR on image** and keep the visual structure intact. Two flags
      matter:'
  - name: Scaling to Multiple Files
    text: 'If you need to **perform OCR on image** files in a folder, wrap the core
      logic in a simple loop:'
  type: HowTo
tags:
- OCR
- C#
- Image Processing
- Aspose.OCR
title: Lakukan OCR pada Gambar dengan C# – Panduan Lengkap Langkah demi Langkah
url: /id/net/text-recognition/perform-ocr-on-image-with-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lakukan OCR pada Gambar dengan C# – Panduan Lengkap Langkah‑per‑Langkah

Pernah bertanya‑tanya bagaimana **melakukan OCR pada gambar** tanpa harus berurusan dengan GUI yang berat? Anda tidak sendirian. Baik Anda sedang mendigitalkan struk, mengambil data dari formulir yang dipindai, atau hanya ingin mengubah PNG menjadi teks yang dapat dicari, beberapa baris kode C# dapat menyelesaikannya.

Dalam tutorial ini kita akan membahas cara memuat gambar untuk OCR, mengenali teks dari gambar, dan akhirnya mengekstrak teks dari PNG menjadi HTML bersih. Pada akhir tutorial Anda akan memiliki aplikasi konsol siap‑jalankan yang **melakukan OCR pada gambar** dan mempertahankan tata letak aslinya.

## Apa yang Akan Anda Bangun

- Program konsol minimal yang membaca PNG (atau gambar lain yang didukung)  
- Menggunakan mesin OCR untuk **mengenali teks dari gambar**  
- Menyimpan hasil sebagai HTML yang memperhatikan tata letak, menyisipkan gambar asli  
- Menunjukkan cara **memuat gambar untuk OCR**, **mengekstrak teks dari PNG**, dan menangani kasus tepi umum  

> **Prasyarat**  
> - .NET 6.0 SDK atau yang lebih baru (Anda juga dapat menargetkan .NET Framework 4.7+)  
> - Perpustakaan OCR yang kompatibel dengan NuGet – contoh menggunakan *Aspose.OCR* tetapi perpustakaan apa pun dengan API serupa akan bekerja  
> - Pengetahuan dasar C# (tidak ada yang rumit)  

Sudah siap? Baik—mari kita mulai.

## Lakukan OCR pada Gambar – Penjelasan Kode Lengkap

Berikut adalah program **lengkap, dapat dijalankan**. Salin‑tempel ke proyek konsol baru (`dotnet new console`) dan tekan **F5**.

```csharp
using System;
using Aspose.OCR;               // OCR engine namespace
using Aspose.OCR.Models;        // Save options namespace
using Aspose.OCR.ImageProcessing; // Image loading helpers

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Create an OCR engine and set the language
            // -------------------------------------------------
            var engine = new OcrEngine
            {
                Language = OcrLanguage.English   // You can change to French, German, etc.
            };

            // -------------------------------------------------
            // Step 2: Load the image for OCR
            // -------------------------------------------------
            // Replace the path with your actual PNG/JPEG/TIFF file.
            engine.Image = ImageStream.FromFile("YOUR_DIRECTORY/form.png");

            // -------------------------------------------------
            // Step 3: Perform OCR recognition
            // -------------------------------------------------
            engine.Recognize();

            // -------------------------------------------------
            // Step 4: Configure HTML save options – keep layout
            // -------------------------------------------------
            var htmlOptions = new HtmlSaveOptions
            {
                PreserveLayout = true,   // Keep columns, tables, and spacing
                EmbedImages = true       // Embed the original PNG inside the HTML
            };

            // -------------------------------------------------
            // Step 5: Save the recognized content as layout‑aware HTML
            // -------------------------------------------------
            engine.Save("YOUR_DIRECTORY/form.html", htmlOptions);

            Console.WriteLine("HTML with layout saved.");
        }
    }
}
```

> **Output yang diharapkan**  
> ```
> HTML with layout saved.
> ```  
> Setelah dijalankan Anda akan menemukan `form.html` di samping PNG Anda. Buka di peramban dan Anda akan melihat tata letak yang persis sama, tetapi kini teks dapat dipilih dan dicari.

### Memuat Gambar untuk OCR

Baris `engine.Image = ImageStream.FromFile("YOUR_DIRECTORY/form.png");` adalah tempat kita **memuat gambar untuk OCR**. Pembantu `ImageStream` menyembunyikan detail format file, sehingga Anda dapat memberi JPEG, BMP, atau TIFF tanpa mengubah kode.  

**Mengapa tidak langsung memakai `Bitmap`?**  
Karena banyak SDK OCR mengharapkan aliran (stream) yang juga membawa metadata DPI. Menggunakan pemuat bawaan perpustakaan memastikan mesin melihat gambar persis seperti yang terlihat di layar, yang meningkatkan akurasi.

#### Pro tip
Jika Anda memproses sekumpulan file, bungkus langkah pemuatan dalam `try/catch` dan catat setiap `FileNotFoundException`. Hal ini mencegah seluruh batch crash karena satu file yang hilang.

### Mengekstrak Teks dari PNG

Setelah `engine.Recognize()` selesai, mesin OCR menyimpan teks yang dikenali secara internal. Anda dapat mengambilnya sebagai string jika hanya membutuhkan teks mentah:

```csharp
string plainText = engine.Text;   // Returns the whole document as plain text
Console.WriteLine(plainText);
```

Ini adalah cara tercepat untuk **mengekstrak teks dari PNG** ketika Anda tidak peduli dengan tata letak. Untuk kebanyakan pekerjaan entri data, teks biasa sudah cukup—ingat untuk memangkas baris baru jika Anda berencana mengimpor ke CSV.

### Mengenali Teks dari Gambar

Pemanggilan `Recognize()` melakukan pekerjaan berat. Di balik layar mesin:

1. Menormalkan gambar (mengoreksi kemiringan, menghilangkan noise)  
2. Membagi menjadi baris dan kata  
3. Menjalankan klasifikasi jaringan saraf yang dilatih pada jutaan glif  

Karena kami menyetel `Language = OcrLanguage.English`, mesin menerapkan kamus khusus bahasa Inggris, yang secara signifikan mengurangi false positive. Jika Anda membutuhkan dukungan multibahasa, cukup berikan array bahasa:

```csharp
engine.Language = OcrLanguage.English | OcrLanguage.Spanish;
```

### Menangani Output HTML yang Memperhatikan Tata Letak

Sebagian besar pengembang berhenti pada teks biasa, tetapi `HtmlSaveOptions` yang kami gunakan memungkinkan Anda **melakukan OCR pada gambar** dan tetap mempertahankan struktur visual. Dua flag penting:

- `PreserveLayout = true` – mempertahankan kolom, tabel, dan spasi.  
- `EmbedImages = true` – menyisipkan PNG asli sebagai elemen `<img>` yang di‑encode Base64, sehingga HTML bersifat mandiri.

Jika Anda menginginkan file yang lebih ringan, setel `EmbedImages = false` dan HTML akan merujuk ke PNG asli di disk.

#### Kasus tepi: File besar

Untuk gambar lebih besar dari 5 MB, penyisipan dapat membuat ukuran HTML membengkak. Dalam situasi tersebut, beralihlah ke referensi gambar eksternal dan pertimbangkan mengompres PNG terlebih dahulu dengan `ImageProcessor.Compress`.

## Kesulitan Umum dan Pro Tips

| Gejala | Penyebab Kemungkinan | Perbaikan |
|--------|----------------------|-----------|
| Karakter kacau | Bahasa yang salah atau paket bahasa tidak ada | Instal file data bahasa yang tepat dan setel `engine.Language` dengan benar |
| Tidak ada teks di output | Gambar terlalu gelap atau resolusi rendah | Pralakukan dengan `engine.Image = ImageProcessor.AdjustContrast(engine.Image, 1.2)` |
| Tata letak rusak di HTML | `PreserveLayout` dibiarkan pada nilai default `false` | Setel `PreserveLayout = true` di `HtmlSaveOptions` |
| Proses lambat pada banyak halaman | Mesin di‑inisialisasi ulang per file | Gunakan kembali instance `OcrEngine` yang sama dan hanya ubah `engine.Image` tiap iterasi |

### Skalasi ke Banyak File

Jika Anda perlu **melakukan OCR pada gambar** dalam sebuah folder, bungkus logika inti dalam loop sederhana:

```csharp
foreach (var file in Directory.GetFiles("YOUR_DIRECTORY", "*.png"))
{
    engine.Image = ImageStream.FromFile(file);
    engine.Recognize();
    var htmlPath = Path.ChangeExtension(file, ".html");
    engine.Save(htmlPath, htmlOptions);
    Console.WriteLine($"Processed {Path.GetFileName(file)}");
}
```

Perhatikan bahwa kami **memuat gambar untuk OCR** di dalam loop, tetapi tetap menggunakan objek `engine` dan `htmlOptions` yang sama. Ini mengurangi churn memori dan mempercepat pekerjaan batch.

## Lebih Lanjut: Mengekspor ke PDF atau DOCX

`engine` yang sama dapat menyimpan ke format lain:

```csharp
engine.Save("output.pdf", new PdfSaveOptions { PreserveLayout = true });
engine.Save("output.docx", new WordSaveOptions { PreserveLayout = true });
```

Jika sistem hilir Anda mengharapkan PDF yang dapat dicari, ini hanya satu baris perubahan—tidak perlu menulis pipeline konversi terpisah.

## Kesimpulan

Kami baru saja menunjukkan cara **melakukan OCR pada gambar** dengan C#, mulai dari memuat gambar hingga **mengekstrak teks dari PNG** dan akhirnya **mengenali teks dari gambar** ke dalam file HTML yang memperhatikan tata letak. Contoh lengkap siap dijalankan, dan Anda kini mengerti mengapa setiap langkah penting, cara menyesuaikannya untuk bahasa lain, serta jebakan apa yang harus diwaspadai.

Selanjutnya, coba ganti bahasa Inggris dengan locale lain, bereksperimen dengan `PreserveLayout = false` untuk mendapatkan HTML yang lebih ramping, atau alirkan output teks biasa ke basis data untuk arsip yang dapat dicari. Langit adalah batasnya ketika Anda menggabungkan mesin OCR yang solid dengan beberapa baris C#.

Punya pertanyaan tentang menangani TIFF multi‑halaman, atau ingin tahu cara mengintegrasikannya ke API ASP.NET Core? Tinggalkan komentar di bawah, dan selamat coding!

## Tutorial Terkait

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Extract Text from Image – Recognize Line with Aspose.OCR](/ocr/english/net/image-and-drawing-recognition/recognize-line/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}