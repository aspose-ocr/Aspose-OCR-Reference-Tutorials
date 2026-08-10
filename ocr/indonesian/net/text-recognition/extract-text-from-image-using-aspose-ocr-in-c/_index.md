---
category: general
date: 2026-08-09
description: Ekstrak teks dari gambar dengan Aspose OCR di C#. Pelajari cara memuat
  gambar untuk OCR, mengatur bahasa OCR, memproses OCR gambar, dan mengonversi gambar
  menjadi teks secara efisien.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- extract text from image
- convert image to text
- load image for ocr
- process image ocr
- set ocr language
language: id
lastmod: 2026-08-09
og_description: Ekstrak teks dari gambar menggunakan Aspose OCR di C#. Tutorial ini
  menunjukkan cara memuat gambar untuk OCR, mengatur bahasa OCR, memproses OCR gambar,
  dan mengonversi gambar menjadi teks dalam beberapa baris kode.
og_image_alt: Screenshot of C# console output showing extracted text from an image
  using Aspose OCR
og_title: Ekstrak teks dari gambar dengan Aspose OCR – Panduan C#
schemas:
- author: Aspose
  dateModified: '2026-08-09'
  description: Extract text from image with Aspose OCR in C#. Learn how to load image
    for OCR, set OCR language, process image OCR, and convert image to text efficiently.
  headline: Extract text from image using Aspose OCR in C#
  type: TechArticle
- description: Extract text from image with Aspose OCR in C#. Learn how to load image
    for OCR, set OCR language, process image OCR, and convert image to text efficiently.
  name: Extract text from image using Aspose OCR in C#
  steps:
  - name: '**Create an OCR engine instance** – The `OcrEngine` encapsulates all OCR
      functionality. Disposing it promptly frees native resources, which is critical
      for long‑running services.'
    text: '**Create an OCR engine instance** – The `OcrEngine` encapsulates all OCR
      functionality. Disposing it promptly frees native resources, which is critical
      for long‑running services.'
  - name: '**Set OCR language** – Selecting the correct language module dramatically
      improves accuracy. Aspose provides over 30 language packs; the default is English.
      The example uses Cyrillic to demonstrate a non‑Latin script.'
    text: '**Set OCR language** – Selecting the correct language module dramatically
      improves accuracy. Aspose provides over 30 language packs; the default is English.
      The example uses Cyrillic to demonstrate a non‑Latin script.'
  - name: '**Load image for OCR** – The engine works with an `ImageStream`. Supplying
      a high‑resolution image (≥300 dpi) reduces misrecognition, especially for complex
      scripts.'
    text: '**Load image for OCR** – The engine works with an `ImageStream`. Supplying
      a high‑resolution image (≥300 dpi) reduces misrecognition, especially for complex
      scripts.'
  - name: '**Process image OCR** – This is where the heavy lifting occurs. The method
      returns an `OcrResult` containing the extracted text, confidence scores, and
      optional layout data.'
    text: '**Process image OCR** – This is where the heavy lifting occurs. The method
      returns an `OcrResult` containing the extracted text, confidence scores, and
      optional layout data.'
  - name: '**Convert image to text** – `result.Text` is a plain `string`. You can
      write it to a file, feed it into a search index, or pass it to downstream NLP
      pipelines.'
    text: '**Convert image to text** – `result.Text` is a plain `string`. You can
      write it to a file, feed it into a search index, or pass it to downstream NLP
      pipelines.'
  - name: Instantiates `OcrEngine`.
    text: Instantiates `OcrEngine`.
  - name: '**Sets OCR language** to Cyrillic (or any language you choose).'
    text: '**Sets OCR language** to Cyrillic (or any language you choose).'
  - name: '**Loads image for OCR** from disk.'
    text: '**Loads image for OCR** from disk.'
  - name: '**Processes image OCR** to obtain the textual result.'
    text: '**Processes image OCR** to obtain the textual result.'
  - name: '**Converts image to text** and prints it.'
    text: '**Converts image to text** and prints it.'
  type: HowTo
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Ekstrak teks dari gambar menggunakan Aspose OCR di C#
url: /id/net/text-recognition/extract-text-from-image-using-aspose-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ekstrak teks dari gambar menggunakan Aspose OCR di C#

Jika Anda perlu **mengekstrak teks dari gambar** dalam aplikasi .NET, panduan ini akan menuntun Anda melalui solusi lengkap yang siap dijalankan. Anda akan melihat cara **memuat gambar untuk OCR**, memilih modul bahasa yang tepat, menjalankan mesin OCR, dan akhirnya **mengonversi gambar menjadi teks** dengan hanya beberapa baris C#.

Tutorial ini mencakup semua yang diperlukan untuk mendapatkan hasil yang dapat diandalkan dengan Aspose.OCR, termasuk jebakan umum seperti format gambar yang tidak didukung dan nuansa bahasa‑spesifik. Pada akhir tutorial, Anda akan memiliki program mandiri yang mencetak teks yang dikenali ke konsol.

## Apa yang akan Anda capai

* Memuat file gambar ke dalam mesin Aspose OCR.  
* **Menetapkan bahasa OCR** (Cyrillic dalam contoh, tetapi bahasa apa pun yang didukung dapat digunakan).  
* **Memproses gambar dengan OCR** dan memperoleh representasi teksnya.  
* **Mengonversi gambar menjadi teks** dan menampilkannya, siap untuk diproses lebih lanjut atau disimpan.  

**Prasyarat**

* .NET 6.0 atau lebih baru (kode ini juga berfungsi pada .NET Framework 4.6+).  
* Visual Studio 2022 (atau IDE apa pun yang mendukung C#).  
* Paket NuGet Aspose.OCR (`Install-Package Aspose.OCR`).  

---

## Ekstrak teks dari gambar – penjelasan kode lengkap

Berikut adalah program lengkap yang dapat dijalankan. Salin ke proyek konsol baru dan ganti `YOUR_DIRECTORY/sample_cyrillic.jpg` dengan path ke gambar Anda sendiri.

```csharp
using System;
using Aspose.OCR;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create an OCR engine instance.
            // The using block ensures the engine is disposed correctly.
            using (var engine = new OcrEngine())
            {
                // Step 2: Set OCR language.
                // Change OcrLanguage.Cyrillic to any other supported language,
                // e.g., OcrLanguage.English, OcrLanguage.Chinese, OcrLanguage.Hindi.
                engine.Language = OcrLanguage.Cyrillic;

                // Step 3: Load image for OCR.
                // ImageStream.FromFile reads the image from disk.
                // Supported formats: JPEG, PNG, BMP, TIFF, GIF.
                engine.Image = ImageStream.FromFile("YOUR_DIRECTORY/sample_cyrillic.jpg");

                // Step 4: Process image OCR.
                // The Process method runs the recognition engine and returns an OcrResult.
                var result = engine.Process();

                // Step 5: Convert image to text.
                // The recognized text is available via result.Text.
                Console.WriteLine("=== Recognized Text ===");
                Console.WriteLine(result.Text);
            }
        }
    }
}
```

### Mengapa setiap langkah penting

1. **Buat instance mesin OCR** – `OcrEngine` mengenkapsulasi semua fungsi OCR. Membuangnya (dispose) dengan cepat membebaskan sumber daya native, yang penting untuk layanan yang berjalan lama.  
2. **Tetapkan bahasa OCR** – Memilih modul bahasa yang tepat secara dramatis meningkatkan akurasi. Aspose menyediakan lebih dari 30 paket bahasa; defaultnya adalah English. Contoh ini menggunakan Cyrillic untuk memperlihatkan skrip non‑Latin.  
3. **Muat gambar untuk OCR** – Mesin bekerja dengan `ImageStream`. Menyediakan gambar beresolusi tinggi (≥300 dpi) mengurangi kesalahan pengenalan, terutama untuk skrip yang kompleks.  
4. **Proses gambar dengan OCR** – Di sinilah pekerjaan berat dilakukan. Metode ini mengembalikan `OcrResult` yang berisi teks yang diekstrak, skor kepercayaan, dan data tata letak opsional.  
5. **Konversi gambar menjadi teks** – `result.Text` adalah `string` biasa. Anda dapat menuliskannya ke file, memasukkannya ke indeks pencarian, atau meneruskannya ke pipeline NLP selanjutnya.

---

## Muat gambar untuk OCR

Metode `ImageStream.FromFile` mendukung format raster umum. Jika Anda menerima gambar sebagai byte array (misalnya, dari API web), gunakan `ImageStream.FromBytes(byte[])` sebagai gantinya:

```csharp
byte[] imageBytes = File.ReadAllBytes("path/to/image.png");
engine.Image = ImageStream.FromBytes(imageBytes);
```

**Tips pro:** Selalu pastikan gambar tidak rusak sebelum diberikan ke mesin. Guard `try { Image.FromFile(...); } catch { ... }` yang cepat dapat mencegah pengecualian runtime.

---

## Tetapkan bahasa OCR

Aspose.OCR menyertakan paket bahasa yang dapat diaktifkan pada waktu berjalan. Untuk menampilkan semua bahasa yang tersedia:

```csharp
foreach (var lang in Enum.GetValues(typeof(OcrLanguage)))
{
    Console.WriteLine(lang);
}
```

Jika Anda perlu mengenali beberapa bahasa dalam dokumen yang sama, gabungkan mereka dengan operator bitwise OR:

```csharp
engine.Language = OcrLanguage.English | OcrLanguage.Russian;
```

**Kasus khusus:** Menggabungkan bahasa right‑to‑left (RTL) (misalnya Arabic) dengan skrip left‑to‑right dapat memerlukan penanganan tata letak tambahan. Aspose secara otomatis mendeteksi arah, tetapi Anda dapat menyesuaikannya melalui `engine.PageSegmentationMode`.

---

## Proses gambar dengan OCR

Pemanggilan `Process` bersifat sinkron dan memblokir hingga mesin selesai. Untuk batch besar atau aplikasi UI, pertimbangkan overload asynchronous:

```csharp
var task = engine.ProcessAsync();
OcrResult result = await task;
```

**Jebakan umum:** Lupa menetapkan `engine.Image` sebelum memanggil `Process` akan menimbulkan `InvalidOperationException`. Selalu tetapkan gambar terlebih dahulu.

---

## Konversi gambar menjadi teks

String yang diekstrak dapat diperlakukan seperti `string` .NET lainnya. Misalnya, untuk menuliskan output ke file:

```csharp
File.WriteAllText("output.txt", result.Text);
```

Jika Anda perlu mempertahankan jeda baris persis seperti yang muncul pada gambar, gunakan `result.Text` secara langsung. Untuk pasca‑pemrosesan (misalnya menghapus spasi berlebih), terapkan metode string standar:

```csharp
string cleaned = result.Text
    .Replace("\r\n", "\n")
    .Trim();
```

---

## Ringkasan contoh lengkap

Menggabungkan semua langkah, program:

1. Menginstansiasi `OcrEngine`.  
2. **Menetapkan bahasa OCR** ke Cyrillic (atau bahasa apa pun yang Anda pilih).  
3. **Muat gambar untuk OCR** dari disk.  
4. **Proses gambar dengan OCR** untuk memperoleh hasil teks.  
5. **Konversi gambar menjadi teks** dan mencetaknya.

Menjalankan contoh dengan gambar Cyrillic yang jelas menghasilkan output serupa dengan:

```
=== Recognized Text ===
Пример текста на кириллице
```

Jika gambar berisi teks bahasa Inggris, cukup ubah `engine.Language = OcrLanguage.English;` dan kode yang sama akan **mengekstrak teks dari gambar** dengan benar.

---

## Kesimpulan

Anda kini tahu cara **mengekstrak teks dari gambar** menggunakan Aspose OCR di C#. Tutorial ini mencakup pemuatan gambar, pemilihan bahasa yang tepat, menjalankan proses OCR, dan **mengonversi gambar menjadi teks** untuk penggunaan selanjutnya.  

Selanjutnya Anda dapat:

* Bereksperimen dengan bahasa lain (`load image for OCR` → `set OCR language` → `process image OCR`).  
* Mengintegrasikan langkah OCR ke dalam pipeline yang lebih besar (misalnya ingest dokumen, PDF yang dapat dicari).  
* Mengoptimalkan kinerja dengan memproses gambar secara batch atau menggunakan API asynchronous.

Jelajahi dokumentasi Aspose.OCR untuk fitur lanjutan seperti kamus khusus, mode segmentasi halaman, dan penyesuaian akurasi OCR. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [How to Perform Image Text Extraction from Stream Using Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}