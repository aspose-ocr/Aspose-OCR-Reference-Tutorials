---
category: general
date: 2026-09-22
description: Ekstrak teks dari gambar dengan Aspose.OCR di C#. Pelajari cara mengubah
  gambar menjadi teks, memuat gambar untuk OCR, dan mengenali teks Cyrillic secara
  efisien.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- extract text from image
- convert image to text
- load image for OCR
- recognize text image
- recognize Cyrillic text
language: id
lastmod: 2026-09-22
og_description: Ekstrak teks dari gambar menggunakan Aspose.OCR di C#. Tutorial ini
  menunjukkan cara mengubah gambar menjadi teks, memuat gambar untuk OCR, dan mengenali
  teks Cyrillic hanya dalam beberapa baris kode.
og_image_alt: Diagram showing extract text from image workflow using Aspose.OCR
og_title: Ekstrak teks dari gambar dengan Aspose.OCR – panduan langkah demi langkah
  C#
schemas:
- author: Aspose
  dateModified: '2026-09-22'
  description: Extract text from image with Aspose.OCR in C#. Learn how to convert
    image to text, load image for OCR, and recognize Cyrillic text efficiently.
  headline: How to extract text from image using Aspose.OCR in C#
  type: TechArticle
- description: Extract text from image with Aspose.OCR in C#. Learn how to convert
    image to text, load image for OCR, and recognize Cyrillic text efficiently.
  name: How to extract text from image using Aspose.OCR in C#
  steps:
  - name: Install the Aspose.OCR package
    text: 'Open a terminal in your solution folder and run:'
  - name: Create the OCR engine instance
    text: '```csharp using Aspose.OCR; using System.Drawing; // Required for Image
      handling'
  - name: Choose the language to recognize
    text: '```csharp // Step 3: Select Cyrillic as the target language engine.Language
      = OcrLanguage.Cyrillic; ```'
  - name: Load image for OCR
    text: '```csharp // Step 4: Load the image that contains the text engine.Image
      = Image.FromFile(@"YOUR_DIRECTORY\sample_cyrillic.png"); ```'
  - name: Perform the recognition and get the result
    text: '```csharp // Step 5: Run the recognition process string recognizedText
      = engine.Recognize(); ```'
  - name: Output the extracted text
    text: '```csharp // Step 6: Display the extracted text Console.WriteLine("Recognized
      text:"); Console.WriteLine(recognizedText); ```'
  type: HowTo
tags:
- OCR
- C#
- Aspose
- Image processing
title: Cara mengekstrak teks dari gambar menggunakan Aspose.OCR di C#
url: /id/net/text-recognition/how-to-extract-text-from-image-using-aspose-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara mengekstrak teks dari gambar menggunakan Aspose.OCR di C#

Jika Anda perlu **mengekstrak teks dari gambar** dalam aplikasi .NET, panduan ini akan memandu Anda melalui solusi lengkap yang siap dijalankan. Anda akan melihat cara **mengonversi gambar menjadi teks**, memuat gambar untuk OCR, dan menangani karakter Cyrillic tanpa konfigurasi tambahan.

Tutorial ini mencakup semua yang Anda butuhkan: paket NuGet yang diperlukan, contoh kode lengkap, penjelasan setiap langkah, dan tip untuk jebakan umum. Pada akhir tutorial Anda dapat menempelkan beberapa baris ke dalam proyek Anda dan mulai mengenali teks secara langsung.

## Apa yang Anda butuhkan

- .NET 6.0 SDK atau yang lebih baru (kode juga berfungsi dengan .NET Framework 4.7+)
- Visual Studio 2022 atau IDE apa pun yang mendukung C#
- Paket NuGet Aspose.OCR (`Aspose.OCR`) yang terpasang di proyek Anda
- Gambar contoh yang berisi teks Cyrillic (misalnya, `sample_cyrillic.png`)

> **Pro tip:** Pada pertama kali Anda meminta bahasa yang tidak termasuk dalam paket, Aspose.OCR secara otomatis mengunduh modul yang diperlukan. Perilaku ini memungkinkan **mengenali teks Cyrillic** secara mulus.

## Mengekstrak teks dari gambar dengan Aspose.OCR

Inti solusi adalah membuat `OcrEngine`, mengonfigurasi bahasa, memuat gambar, dan memanggil `Recognize()`. Bagian-bagian berikut menjelaskan setiap langkah.

### Langkah 1: Instal paket Aspose.OCR

Buka terminal di folder solusi Anda dan jalankan:

```bash
dotnet add package Aspose.OCR
```

Perintah ini menambahkan versi stabil terbaru dari Aspose.OCR ke file proyek Anda, memastikan bahwa mesin OCR dan modul bahasa tersedia saat runtime.

### Langkah 2: Buat instance mesin OCR

```csharp
using Aspose.OCR;
using System.Drawing;   // Required for Image handling

// ...

// Step 2: Initialize the OCR engine
OcrEngine engine = new OcrEngine();
```

`OcrEngine` adalah titik masuk untuk semua operasi OCR. Membuat instance-nya mengalokasikan sumber daya internal yang diperlukan untuk analisis gambar.

### Langkah 3: Pilih bahasa untuk dikenali

```csharp
// Step 3: Select Cyrillic as the target language
engine.Language = OcrLanguage.Cyrillic;
```

Menetapkan `engine.Language` memberi tahu Aspose.OCR set karakter apa yang harus dicari. **Mengenali teks Cyrillic** memicu pengunduhan otomatis paket bahasa Cyrillic jika belum ada di mesin.

### Langkah 4: Muat gambar untuk OCR

```csharp
// Step 4: Load the image that contains the text
engine.Image = Image.FromFile(@"YOUR_DIRECTORY\sample_cyrillic.png");
```

Baris ini **memuat gambar untuk OCR** menggunakan `System.Drawing.Image`. Ganti `YOUR_DIRECTORY` dengan jalur sebenarnya ke file PNG atau JPEG Anda. Mesin kini memegang bitmap yang siap untuk analisis.

### Langkah 5: Lakukan pengenalan dan dapatkan hasilnya

```csharp
// Step 5: Run the recognition process
string recognizedText = engine.Recognize();
```

`Recognize()` memindai bitmap, menerapkan model khusus bahasa, dan mengembalikan string yang diekstrak. Jika gambar jelas dan bahasa telah diatur dengan benar, metode ini mengembalikan hasil dengan akurasi tinggi.

### Langkah 6: Keluarkan teks yang diekstrak

```csharp
// Step 6: Display the extracted text
Console.WriteLine("Recognized text:");
Console.WriteLine(recognizedText);
```

Mencetak hasil ke konsol memungkinkan Anda memverifikasi bahwa **mengekstrak teks dari gambar** berfungsi sebagaimana mestinya. Anda juga dapat menulis teks ke file, basis data, atau mengirimnya ke layanan lain.

## Contoh lengkap yang dapat dijalankan

Berikut adalah program mandiri yang mencakup semua langkah di atas. Salin kode ke dalam proyek konsol baru (`dotnet new console`) dan jalankan.

```csharp
using System;
using System.Drawing;          // Provides Image class
using Aspose.OCR;              // Aspose OCR namespace

namespace ImageToTextDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Create OCR engine
            OcrEngine engine = new OcrEngine();

            // Select the language – Cyrillic triggers module download if needed
            engine.Language = OcrLanguage.Cyrillic;

            // Load the image file (adjust the path to your environment)
            string imagePath = @"YOUR_DIRECTORY\sample_cyrillic.png";
            engine.Image = Image.FromFile(imagePath);

            // Perform recognition
            string recognizedText = engine.Recognize();

            // Output the result
            Console.WriteLine("Recognized text:");
            Console.WriteLine(recognizedText);
        }
    }
}
```

**Expected output**

```
Recognized text:
Пример текста на кириллице
```

Jika gambar contoh berisi frasa “Пример текста на кириллице”, konsol akan menampilkannya persis seperti yang ditunjukkan. Variasi dalam font, ukuran, atau noise dapat memengaruhi akurasi, tetapi pra‑pemrosesan bawaan Aspose.OCR menangani sebagian besar kasus umum.

## Menangani kasus tepi umum

| Skenario | Apa yang harus dilakukan | Mengapa penting |
|----------|--------------------------|-----------------|
| Gambar tidak ditemukan | Bungkus `Image.FromFile` dalam blok `try / catch (FileNotFoundException)` dan tampilkan pesan yang ramah. | Mencegah aplikasi crash dan membantu pengguna menemukan file yang benar. |
| Gambar dengan kontras rendah | Setel `engine.ImagePreprocessingOptions` ke `ImagePreprocessingOptions.Auto` atau sesuaikan kecerahan/kontras secara manual sebelum pengenalan. | Meningkatkan akurasi OCR ketika gambar sumber redup. |
| Perlu mengenali banyak bahasa | Tetapkan `engine.Language = OcrLanguage.Multilingual;` dan secara opsional tambahkan `engine.AdditionalLanguages.Add(OcrLanguage.English);`. | Memungkinkan deteksi dokumen dengan skrip campuran (mis., Cyrillic campur Latin). |
| Banyak gambar dalam batch | Gunakan kembali satu instance `OcrEngine` dan panggil `engine.Recognize()` dalam loop. Buang (dispose) engine setelah pemrosesan. | Mengurangi alokasi memori dan mempercepat pemrosesan. |

## Praktik terbaik untuk OCR yang dapat diandalkan

- **Gunakan format gambar lossless** (PNG atau TIFF) bila memungkinkan; kompresi JPEG dapat menghasilkan artefak yang membingungkan pengenalan.
- **Pertahankan resolusi gambar** pada 300 dpi atau lebih tinggi untuk teks cetak; resolusi lebih rendah dapat melewatkan karakter kecil.
- **Potong batas yang tidak perlu** sebelum memuat gambar; ruang putih tambahan meningkatkan waktu pemrosesan tanpa menambah nilai.
- **Validasi output** dengan memeriksa string kosong atau karakter tak terduga, terutama saat memproses dokumen yang dipindai dengan noise.

## Langkah selanjutnya

Sekarang Anda dapat **mengekstrak teks dari gambar**, pertimbangkan untuk memperluas solusi:

- **Mengonversi gambar menjadi teks secara massal**: baca direktori gambar, proses tiap file, dan tulis hasil ke file CSV.
- **Integrasikan dengan penyimpanan cloud**: ambil gambar dari Azure Blob Storage atau Amazon S3, jalankan OCR, dan simpan teks yang diekstrak kembali ke cloud.
- **Gabungkan dengan API terjemahan**: setelah mengenali teks Cyrillic, panggil Azure Translator atau Google Cloud Translation untuk menghasilkan output dalam bahasa Inggris.
- **Jelajahi analisis tata letak lanjutan**: Aspose.OCR menyediakan objek `OcrPage` yang menampilkan koordinat teks, berguna untuk membuat ulang PDF atau dokumen yang dapat dicari.

Dengan mengikuti langkah-langkah dalam tutorial ini, Anda memiliki fondasi yang kuat untuk proyek apa pun yang perlu **mengonversi gambar menjadi teks** atau **mengenali gambar teks** dalam berbagai bahasa.

---

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Cara Mengekstrak Teks dari Gambar Menggunakan Aspose.OCR untuk .NET](/ocr/english/net/text-recognition/get-recognition-result/)
- [Ekstrak teks gambar C# dengan pemilihan bahasa menggunakan Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Ekstrak Teks dari Gambar dengan Aspose OCR – Panduan Cepat C#](/ocr/english/net/text-recognition/extract-text-from-image-with-aspose-ocr-c-quickstart/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}