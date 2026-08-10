---
category: general
date: 2026-02-13
description: Buat PDF yang dapat dicari dari gambar menggunakan Aspose.OCR. Pelajari
  cara mengonversi gambar ke PDF, mengekstrak teks dari gambar, menyematkan font dalam
  PDF, dan mengenali teks dari PNG.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- extract text from image
- embed fonts in pdf
- recognize text from png
language: id
og_description: Buat PDF yang dapat dicari dari gambar dengan Aspose.OCR. Panduan
  ini menunjukkan cara mengonversi gambar ke PDF, menyematkan font, dan mengekstrak
  teks dari PNG dengan mudah.
og_title: Buat PDF yang Dapat Dicari dari Gambar – Tutorial C# Langkah demi Langkah
tags:
- C#
- OCR
- Aspose
- PDF generation
title: Buat PDF yang Dapat Dicari dari Gambar – Panduan Lengkap C#
url: /id/net/text-recognition/create-searchable-pdf-from-image-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat PDF yang Dapat Dicari dari Gambar – Panduan Lengkap C#

Pernahkah Anda perlu **membuat PDF yang dapat dicari** dari PNG yang dipindai tetapi tidak yakin harus mulai dari mana? Anda tidak sendirian. Dalam banyak proyek—misalnya digitalisasi faktur atau pengarsipan manual lama—kemampuan mengubah gambar menjadi PDF yang dapat Anda cari benar‑benar merupakan perubahan besar.  

Dalam tutorial ini kami akan memandu Anda melalui langkah‑langkah tepat untuk **mengonversi gambar ke PDF**, **mengekstrak teks dari gambar**, menyematkan font yang diperlukan, dan akhirnya menghasilkan file PDF yang sepenuhnya dapat dicari. Tanpa referensi yang samar, hanya contoh lengkap yang dapat dijalankan yang dapat Anda salin‑tempel ke Visual Studio hari ini.

> **Apa yang akan Anda dapatkan:** aplikasi konsol C# yang membaca `input.png`, menjalankan OCR, menyematkan font, mempertahankan gambar raster asli sebagai latar belakang, dan menulis `output.pdf`. Pada akhirnya Anda akan memahami *mengapa* setiap baris penting dan bagaimana menyesuaikannya untuk skenario Anda sendiri.

---

## Prasyarat

- .NET 6.0 SDK atau yang lebih baru (kode ini juga berfungsi dengan .NET Framework 4.7+).  
- Aspose.OCR untuk .NET – Anda dapat mengunduhnya dari NuGet (`Install-Package Aspose.OCR`).  
- Sebuah contoh gambar PNG (`input.png`) yang ditempatkan di folder yang Anda kontrol.  
- Pengetahuan dasar tentang proyek konsol C# (jika Anda belum pernah membuatnya, cukup buka Visual Studio → **Create a new project** → **Console App** → **C#**).

> **Tip:** Aspose menawarkan lisensi percobaan gratis; cukup letakkan file `.lic` di samping executable Anda dan pustaka akan berfungsi tanpa watermark.

---

## Langkah 1: Siapkan Mesin OCR – Kenali Teks dari PNG

Hal pertama yang kita butuhkan adalah mesin OCR yang dapat benar‑benar membaca karakter dalam file PNG. Aspose.OCR membuat hal ini sederhana.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Output;

// Initialize the OCR engine with English language support
OcrEngine ocrEngine = new OcrEngine
{
    // Primary language – you can add more if needed
    Language = OcrLanguage.English
};
```

**Mengapa ini penting:**  
Menetapkan `Language` memberi tahu mesin set karakter apa yang diharapkan. Jika Anda melewatkannya, mesin akan menggunakan mode umum yang mungkin salah mengartikan karakter aksen atau angka. Untuk dokumen multibahasa, Anda dapat memberikan daftar dipisahkan koma seperti `OcrLanguage.English | OcrLanguage.French`.

---

## Langkah 2: Muat dan Kenali Gambar – Ekstrak Teks dari Gambar

Setelah mesin siap, kami memberinya PNG yang ingin diproses.

```csharp
// Path to the source image; adjust as needed
string inputPath = @"YOUR_DIRECTORY/input.png";

// Perform OCR – this populates the engine's internal text representation
ocrEngine.RecognizeImage(inputPath);
```

**Apa yang terjadi di balik layar?**  
`RecognizeImage` memindai bitmap, mengidentifikasi blok teks, dan menyimpan hasilnya di `ocrEngine`. Anda dapat mengakses `ocrEngine.Text` nanti jika hanya membutuhkan string mentah, tetapi untuk PDF yang dapat dicari kami akan membiarkan Aspose menangani konversinya secara langsung.

> **Kasus khusus:** Jika PNG Anda sangat besar (lebih dari 10 MB) Anda mungkin kehabisan memori. Dalam hal ini, pertimbangkan untuk mengubah ukuran gambar terlebih dahulu atau menggunakan `OcrEngine.RecognizeImage(Stream)` untuk men-stream data.

---

## Langkah 3: Konfigurasikan Opsi Ekspor PDF – Sematkan Font dalam PDF

PDF yang dapat dicari tidak berguna jika font tidak disematkan; dokumen akan terlihat rusak pada mesin yang tidak memiliki jenis huruf yang diperlukan. Aspose memungkinkan kami mengatur ini dengan objek opsi sederhana.

```csharp
// Define how the searchable PDF should be built
SearchablePdfOptions pdfOptions = new SearchablePdfOptions
{
    // Guarantees the PDF renders correctly everywhere
    EmbedFonts = true,

    // Keeps the original raster image as a visual background
    KeepOriginalImage = true
};
```

**Mengapa menyematkan font?**  
Ketika `EmbedFonts` bernilai `true`, PDF membawa data font di dalam file. Ini memastikan bahwa setiap penampil—Chrome, Adobe Reader, atau aplikasi seluler—menampilkan teks persis seperti yang dimaksud, bahkan ketika sistem target tidak memiliki font tersebut.

**Kapan Anda akan mengatur `KeepOriginalImage` menjadi `false`?**  
Jika Anda hanya membutuhkan teks yang diekstrak dan menginginkan file yang lebih kecil, mematikan opsi ini akan menghapus gambar latar belakang, meninggalkan PDF “bersih” hanya teks.

---

## Langkah 4: Ekspor ke PDF yang Dapat Dicari – Konversi Gambar ke PDF

Dengan hasil OCR dan opsi PDF yang sudah disiapkan, langkah terakhir adalah satu baris kode yang menulis PDF yang dapat dicari ke disk.

```csharp
// Destination path for the generated PDF
string outputPath = @"YOUR_DIRECTORY/output.pdf";

// Export the OCR result as a searchable PDF
ocrEngine.ExportToSearchablePdf(outputPath, pdfOptions);

// Let the user know we’re done
Console.WriteLine("Searchable PDF created.");
```

**Apa yang akan Anda lihat:**  
Membuka `output.pdf` di penampil apa pun, Anda dapat memilih teks, menyalin‑tempelnya, dan bahkan menjalankan pencarian (`Ctrl + F`) untuk menemukan kata‑kata yang awalnya hanya berupa piksel dalam PNG.

---

## Contoh Lengkap yang Berfungsi

Berikut adalah program lengkap yang dapat Anda kompilasi dan jalankan segera. Ganti `YOUR_DIRECTORY` dengan folder yang berisi `input.png`.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Output;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine – set language to English
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.English
        };

        // 2️⃣ Recognize text from the PNG image
        string inputPath = @"YOUR_DIRECTORY/input.png";
        ocrEngine.RecognizeImage(inputPath);

        // 3️⃣ Prepare PDF options – embed fonts & keep raster background
        SearchablePdfOptions pdfOptions = new SearchablePdfOptions
        {
            EmbedFonts = true,
            KeepOriginalImage = true
        };

        // 4️⃣ Export to a searchable PDF file
        string outputPath = @"YOUR_DIRECTORY/output.pdf";
        ocrEngine.ExportToSearchablePdf(outputPath, pdfOptions);

        // 5️⃣ Notify the user
        Console.WriteLine("Searchable PDF created.");
    }
}
```

**Output yang diharapkan di konsol:**

```
Searchable PDF created.
```

Buka `output.pdf` dan coba cari kata yang Anda tahu muncul di `input.png`. Jika kata tersebut disorot, Anda telah berhasil **membuat PDF yang dapat dicari** dari sebuah gambar.

---

## Pertanyaan Umum & Tips Pro

### “Bisakah saya memproses banyak gambar dalam satu kali jalankan?”

Tentu saja. Bungkus logika pengenalan dan ekspor dalam sebuah loop, mungkin menggunakan `Directory.GetFiles(..., "*.png")`. Ingatlah untuk memberi setiap PDF nama yang unik, misalnya `Path.GetFileNameWithoutExtension(img) + ".pdf"`.

### “Bagaimana jika dokumen saya berisi teks dalam bahasa Inggris dan Spanyol?”

Atur properti bahasa ke flag gabungan:

```csharp
ocrEngine.Language = OcrLanguage.English | OcrLanguage.Spanish;
```

Aspose kemudian akan mencoba mendeteksi karakter dari kedua alfabet.

### “File PDF terlalu besar—bagaimana cara memperkecilnya?”

Dua trik cepat:

1. Atur `pdfOptions.KeepOriginalImage = false` untuk menghilangkan latar belakang raster.  
2. Gunakan `pdfOptions.ImageCompression = ImageCompression.Jpeg;` (Anda perlu menambahkan properti ini) untuk mengompres gambar yang disematkan.

### “Apakah saya memerlukan lisensi untuk penggunaan produksi?”

Versi percobaan berfungsi baik untuk pengujian, tetapi untuk penyebaran komersial Anda harus membeli lisensi dan mendaftarkannya di awal aplikasi Anda:

```csharp
Aspose.OCR.License license = new Aspose.OCR.License();
license.SetLicense("Aspose.OCR.lic");
```

---

## Memperluas Solusi

Sekarang Anda tahu cara **membuat PDF yang dapat dicari**, Anda mungkin ingin:

- **Menambahkan watermark** – gunakan `PdfDocument` dari Aspose.PDF untuk menimpa teks setelah OCR.  
- **Memproses PDF secara batch** – gabungkan beberapa PDF yang dapat dicari menjadi satu menggunakan `PdfFileEditor`.  
- **Integrasikan dengan Azure Blob Storage** – baca/tulis aliran gambar dan PDF langsung dari cloud, menghilangkan I/O file lokal.

Setiap ekstensi ini mengikuti pola yang sama: dapatkan hasil OCR, konfigurasikan pustaka berikutnya, dan rangkaian operasi.

---

## Kesimpulan

Anda baru saja belajar cara **membuat PDF yang dapat dicari** dari gambar PNG menggunakan Aspose.OCR di C#. Dengan menginisialisasi mesin OCR, mengenali teks, mengkonfigurasi `SearchablePdfOptions` untuk **menyematkan font dalam PDF**, dan mengekspor, Anda mendapatkan file yang secara visual identik dengan aslinya dan sepenuhnya dapat dicari.  

Mulai dari sini, silakan bereksperimen dengan konversi batch, bahasa yang berbeda, atau kompresi yang lebih ketat—apa pun yang sesuai dengan alur kerja Anda. Jika Anda menemukan kejanggalan, forum Aspose dan dokumentasi API adalah sumber yang solid, tetapi langkah‑langkah inti di atas akan mencakup 90 % dari kasus penggunaan umum.

Selamat coding, dan semoga PDF Anda selalu dapat dicari!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}