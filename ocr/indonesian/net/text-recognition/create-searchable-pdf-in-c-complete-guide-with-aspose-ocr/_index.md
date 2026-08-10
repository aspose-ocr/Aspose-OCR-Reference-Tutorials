---
category: general
date: 2026-06-28
description: Buat PDF yang dapat dicari dari gambar menggunakan C#. Pelajari cara
  mengonversi gambar ke PDF, mengekstrak teks dari gambar, dan mengenali banyak bahasa
  dalam satu alur.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- extract text from image
- how to recognize multiple languages
- how to generate searchable pdf
language: id
og_description: Buat PDF yang dapat dicari dengan C#. Panduan ini menunjukkan cara
  mengonversi gambar ke PDF, mengekstrak teks dari gambar, dan mengenali banyak bahasa
  secara programatik.
og_title: Buat PDF yang Dapat Dicari di C# – Tutorial Langkah demi Langkah
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: Create searchable PDF from images using C#. Learn how to convert image
    to PDF, extract text from image, and recognize multiple languages in one flow.
  headline: Create Searchable PDF in C# – Complete Guide with Aspose OCR
  type: TechArticle
- description: Create searchable PDF from images using C#. Learn how to convert image
    to PDF, extract text from image, and recognize multiple languages in one flow.
  name: Create Searchable PDF in C# – Complete Guide with Aspose OCR
  steps:
  - name: Prerequisites
    text: '- .NET 6.0 SDK or later (the code compiles with .NET Core as well). - An
      Aspose.OCR license (you can start with a free trial; the API works without a
      license but adds a watermark). - A sample image that contains English, Arabic,
      and Korean text (or any languages you need). - Visual Studio 2022 or yo'
  - name: What If a Language Isn't Recognized?
    text: If you add a language that the engine doesn’t have a model for, it will
      simply ignore it and fall back to the others. To avoid surprises, double‑check
      the supported language list in the Aspose documentation.
  - name: Expected Output
    text: '``` Plain text: Hello World! مرحبا بالعالم! 안녕하세요 세계! Searchable PDF saved.
      ```'
  type: HowTo
tags:
- OCR
- PDF
- C#
- Aspose
title: Buat PDF yang Dapat Dicari di C# – Panduan Lengkap dengan Aspose OCR
url: /id/net/text-recognition/create-searchable-pdf-in-c-complete-guide-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat PDF yang Dapat Dicari di C# – Panduan Lengkap dengan Aspose OCR

Pernah bertanya-tanya bagaimana cara **membuat PDF yang dapat dicari** langsung dari sebuah gambar tanpa meninggalkan proyek C# Anda? Anda tidak sendirian. Baik Anda sedang mendigitalkan dokumen multibahasa atau membangun aplikasi pemindaian struk, mengubah gambar menjadi PDF yang dapat Anda cari adalah kemampuan yang mengubah permainan.

Di tutorial ini kami akan membahas langkah‑langkah tepat untuk **membuat PDF yang dapat dicari** menggunakan Aspose.OCR, mencakup semua hal mulai dari memuat gambar hingga mengekspor dokumen yang sepenuhnya dapat dicari. Sepanjang proses kami juga akan menunjukkan cara **mengonversi gambar ke PDF**, **mengekstrak teks dari gambar**, dan **mengenali banyak bahasa**—semua dalam satu metode yang ramah async.

## Apa yang Akan Anda Dapatkan

- Aplikasi konsol C# yang dapat dijalankan yang membaca gambar, menjalankan OCR dalam mode percepatan GPU, dan menulis PDF yang dapat dicari.
- Pemahaman mengapa mengaktifkan GPU penting untuk kinerja.
- Teknik untuk **mengekstrak teks dari gambar** untuk pemrosesan selanjutnya.
- Pola yang jelas untuk **cara mengenali banyak bahasa** dalam satu kali proses.
- Tips untuk memperluas kode agar menangani format lain atau pengaturan OCR khusus.

### Prasyarat

- .NET 6.0 SDK atau yang lebih baru (kode juga dapat dikompilasi dengan .NET Core).
- Lisensi Aspose.OCR (Anda dapat memulai dengan percobaan gratis; API berfungsi tanpa lisensi tetapi menambahkan watermark).
- Gambar contoh yang berisi teks Bahasa Inggris, Arab, dan Korea (atau bahasa apa pun yang Anda butuhkan).
- Visual Studio 2022 atau IDE favorit Anda.

Sudah siap? Bagus—mari kita mulai.

---

## Langkah 1: Siapkan Proyek dan Instal Aspose.OCR

Pertama, buat proyek konsol baru:

```bash
dotnet new console -n SearchablePdfDemo
cd SearchablePdfDemo
```

Kemudian tambahkan paket NuGet Aspose.OCR:

```bash
dotnet add package Aspose.OCR
```

> **Pro tip:** Jika Anda berencana menjalankan OCR pada mesin yang mendukung GPU, juga instal paket `Aspose.OCR.Gpu`. Paket ini secara otomatis mengunduh pustaka CUDA native.

## Langkah 2: Buat OCR Engine dan Aktifkan Akselerasi GPU

Inti dari operasi ini adalah `OcrEngine`. Mengaktifkan GPU dapat mengurangi beberapa detik dari waktu pemrosesan untuk gambar beresolusi tinggi.

```csharp
using Aspose.OCR;
using Aspose.OCR.Output;

// ...

// Step 2: Create an OCR engine and turn on GPU support
var ocrEngine = new OcrEngine();
ocrEngine.Settings.EnableGpu = true;   // ← speeds up large images dramatically
```

Mengapa mengaktifkan GPU? Karena OCR pada dasarnya adalah masalah perkalian matriks besar; GPU menangani tugas paralel tersebut jauh lebih efisien daripada CPU. Jika Anda berada di server tanpa GPU, biarkan `EnableGpu` tetap `false`—engine akan kembali ke pemrosesan CPU.

## Langkah 3: Muat Gambar Secara Asinkron

I/O async menjaga UI Anda tetap responsif dan mencegah kelaparan thread‑pool dalam skenario server. Helper `OcrImage.FromFileAsync` menyederhanakan penanganan stream.

```csharp
using Aspose.OCR;

// ...

// Step 3: Load the image to be processed (async)
var imagePath = @"C:\Docs\multilingual_sample.jpg";
var image = await OcrImage.FromFileAsync(imagePath);
```

Jika Anda perlu **mengonversi gambar ke PDF** nanti, simpan instance `OcrImage` ini; Anda akan mengirimkannya langsung ke pengekspor PDF.

## Langkah 4: Kenali Teks dalam Banyak Bahasa

Aspose.OCR memungkinkan Anda menentukan daftar kode bahasa yang dipisahkan koma. Ini adalah jawaban untuk **cara mengenali banyak bahasa** dalam satu kali proses.

```csharp
using Aspose.OCR;

// ...

// Step 4: Run OCR with English, Arabic, and Korean support
var ocrResult = await ocrEngine.RecognizeAsync(image, new OcrOptions
{
    Language = "en,ar,ko"   // ← multiple languages, order doesn’t matter
});
```

Properti `ocrResult.Text` kini berisi representasi teks polos dari semua yang dapat diuraikan oleh Aspose. Ini adalah inti dari **mengekstrak teks dari gambar**.

```csharp
Console.WriteLine("Plain text extracted:");
Console.WriteLine(ocrResult.Text);
```

### Bagaimana Jika Sebuah Bahasa Tidak Dikenali?

Jika Anda menambahkan bahasa yang tidak memiliki model di engine, engine akan mengabaikannya dan kembali ke bahasa lain. Untuk menghindari kejutan, periksa kembali daftar bahasa yang didukung dalam dokumentasi Aspose.

## Langkah 5: Ekspor PDF yang Dapat Dicari Secara Langsung

Alih-alih membuat PDF secara manual dan menambahkan teks di atasnya, Aspose.OCR menyediakan satu baris kode untuk **cara menghasilkan PDF yang dapat dicari**. Metode ini menyematkan teks OCR sebagai lapisan tak terlihat, membuat PDF dapat dicari sambil mempertahankan gambar asli.

```csharp
using Aspose.OCR.Output;

// ...

// Step 5: Export the recognized content as a searchable PDF
await ocrEngine.RecognizeToPdfAsync(image, new PdfExportOptions
{
    Language = "en,ar,ko",               // keep language consistency
    OutputPath = @"C:\Docs\sample_searchable.pdf"
});

Console.WriteLine("Searchable PDF saved at C:\\Docs\\sample_searchable.pdf");
```

Di balik layar, Aspose membuat halaman PDF dengan bitmap asli sebagai latar belakang yang terlihat dan menambahkan lapisan teks tersembunyi yang sesuai dengan koordinat gambar. Saat Anda membuka file di Adobe Reader dan menekan **Ctrl + F**, Anda dapat menemukan kata‑kata dari ketiga bahasa tersebut.

## Langkah 6: Gabungkan Semua – `Main` Async Lengkap

Berikut adalah program lengkap yang siap dijalankan. Tempelkan ke dalam `Program.cs`, ganti jalur file, dan tekan **F5**.

```csharp
using System;
using System.Threading.Tasks;
using Aspose.OCR;
using Aspose.OCR.Output;

class AllInOne
{
    static async Task Main()
    {
        // Step 2: Create an OCR engine and enable GPU acceleration
        var ocrEngine = new OcrEngine();
        ocrEngine.Settings.EnableGpu = true;

        // Step 3: Load the image to be processed (async)
        var image = await OcrImage.FromFileAsync(@"C:\Docs\multilingual_sample.jpg");

        // Step 4: Recognize text in the image using multiple languages
        var ocrResult = await ocrEngine.RecognizeAsync(image, new OcrOptions
        {
            Language = "en,ar,ko"
        });

        Console.WriteLine("Plain text:");
        Console.WriteLine(ocrResult.Text);

        // Step 5: Export the recognized content as a searchable PDF
        await ocrEngine.RecognizeToPdfAsync(image, new PdfExportOptions
        {
            Language = "en,ar,ko",
            OutputPath = @"C:\Docs\sample_searchable.pdf"
        });

        Console.WriteLine("Searchable PDF saved.");
    }
}
```

### Output yang Diharapkan

```
Plain text:
Hello World!
مرحبا بالعالم!
안녕하세요 세계!
Searchable PDF saved.
```

Saat Anda membuka `sample_searchable.pdf` dan mencari “Hello”, “العالم”, atau “세계”, engine akan menemukan kata yang sesuai meskipun mereka ditampilkan sebagai bagian dari gambar.

## Langkah 7: Kesalahan Umum & Cara Memperbaikinya

| Masalah | Mengapa Terjadi | Solusi |
|-------|----------------|-----|
| **GPU tidak terdeteksi** | Mesin tidak memiliki driver CUDA atau paket `Aspose.OCR.Gpu` belum diinstal. | Instal driver NVIDIA, verifikasi versi CUDA, atau set `EnableGpu = false`. |
| **Dukungan bahasa tidak tersedia** | Kode bahasa tidak ada dalam set model bawaan. | Unduh paket bahasa tambahan dari Aspose atau batasi pada kode yang didukung. |
| **PDF muncul kosong** | Jalur output tidak valid atau proses tidak memiliki izin menulis. | Gunakan jalur absolut dengan izin yang tepat, misalnya `C:\Temp\output.pdf`. |
| **Penurunan kinerja** | Gambar besar (>5 MP) menyebabkan tekanan memori. | Kurangi resolusi gambar sebelum OCR atau tingkatkan batas memori proses. |

## Memperluas Contoh

- **Pemrosesan batch:** Bungkus logika inti dalam loop `foreach` yang mengiterasi folder berisi gambar.
- **Pengaturan OCR khusus:** Sesuaikan `ocrEngine.Settings.PageSegMode` untuk tata letak satu kolom atau multi‑kolom.
- **Penyisipan metadata:** Gunakan `PdfExportOptions` untuk menyematkan penulis, judul, atau tanggal pembuatan ke dalam PDF yang dapat dicari.

---

## Kesimpulan

Anda kini memiliki resep lengkap yang solid untuk **membuat PDF yang dapat dicari** langsung dari gambar menggunakan C#. Dengan mengikuti langkah‑langkah di atas Anda telah belajar cara **mengonversi gambar ke pdf**, **mengekstrak teks dari gambar**, dan **mengenali banyak bahasa**—semua sambil menjaga kode tetap bersih dan siap async.

Mulai dari sini Anda dapat bereksperimen dengan paket bahasa yang berbeda, menambahkan post‑processing OCR (seperti pemeriksaan ejaan), atau mengintegrasikan alur ini ke dalam API web yang menyajikan PDF yang dapat dicari sesuai permintaan. Tidak ada batasnya, dan kode yang baru saja Anda tulis merupakan fondasi yang kuat untuk proyek otomatisasi dokumen apa pun.

Ada pertanyaan tentang penyesuaian kinerja atau lisensi? Tinggalkan komentar, dan mari teruskan diskusi. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Convert Images to PDF C# – Save Multipage OCR Result](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)
- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}