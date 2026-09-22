---
category: general
date: 2026-02-13
description: Cara menggunakan OCR di C# untuk mengekstrak teks dari gambar, mengenali
  teks dari foto atau JPG, dan menjalankan OCR pada gambar tanpa internet.
draft: false
keywords:
- how to use OCR
- extract text from image
- recognize text from photo
- recognize text from jpg
- run OCR on image
language: id
og_description: Cara menggunakan OCR di C# untuk mengekstrak teks dari gambar, mengenali
  teks dari foto, dan menjalankan OCR pada gambar dengan contoh lengkap yang dapat
  dijalankan.
og_title: Cara Menggunakan OCR di C# – Ekstrak Teks dari Gambar
tags:
- OCR
- C#
- Image Processing
title: Cara Menggunakan OCR di C# – Ekstrak Teks dari Gambar dan Mengenali Teks dari
  Foto
url: /id/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-image-and-recognize-te/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menggunakan OCR di C# – Ekstrak Teks dari Gambar dan Mengenali Teks dari Foto

Pernah bertanya-tanya **cara menggunakan OCR** untuk mengambil kata‑kata dari screenshot, struk yang dipindai, atau foto acak yang Anda ambil dengan ponsel? Anda tidak sendirian. Dalam banyak aplikasi dunia nyata kita perlu mengubah gambar menjadi teks yang dapat dicari, dan melakukannya secara lokal—tanpa koneksi internet yang tidak stabil—bisa terasa seperti teka‑teki.

Itulah mengapa panduan ini menunjukkan cara langkah‑demi‑langkah untuk **mengekstrak teks dari file gambar** menggunakan mesin OCR C#, dan juga mencakup cara **mengenali teks dari foto**, **mengenali teks dari JPG**, serta **menjalankan OCR pada gambar** yang berada langsung di disk Anda. Pada akhir tutorial Anda akan memiliki program lengkap yang siap disalin‑tempel dan langsung berfungsi.

## Apa yang Akan Anda Pelajari

- Cara mengonfigurasi mesin OCR untuk Bahasa Mandarin Sederhana (atau bahasa apa pun yang Anda masukkan).  
- Kode tepat yang diperlukan untuk **memuat sumber daya** dari folder lokal—tanpa panggilan jaringan.  
- Cara **mengenali teks dari foto** seperti file JPEG, PNG, atau BMP.  
- Tips menangani kasus tepi umum seperti file model yang hilang atau format gambar yang tidak didukung.  
- Contoh lengkap yang dapat dijalankan, yang dapat Anda masukkan ke Visual Studio dan melihat hasilnya secara instan.

### Prasyarat

- .NET 6.0 atau lebih baru (API yang digunakan di sini menargetkan .NET Standard 2.0, jadi versi yang lebih lama juga dapat bekerja).  
- Familiaritas dasar dengan C# dan Visual Studio (atau IDE apa pun yang Anda suka).  
- Perpustakaan OCR yang Anda gunakan (potongan kode mengasumsikan kelas fiktif `OcrEngine` yang dilengkapi dengan model bahasa).  
- Sebuah folder yang berisi file model bahasa yang diperlukan—anggap saja ini sebagai “otak” yang dipakai mesin untuk membaca karakter Mandarin.

> **Pro tip:** Jika Anda belum memiliki file model bahasa Mandarin, unduh sekali dari situs vendor dan letakkan di folder seperti `C:\OcrResources`. Mesin tidak akan pernah perlu terhubung ke internet lagi.

---

![Diagram proses OCR pada foto](path/to/ocr-diagram.png "Diagram proses OCR pada foto")

## Cara Menggunakan OCR: Menyiapkan Mesin

Hal pertama yang Anda butuhkan adalah sebuah instance mesin OCR, yang dikonfigurasi untuk bahasa yang Anda inginkan. Dalam tutorial ini kami menargetkan **Mandarin Sederhana**, tetapi mengganti `OcrLanguage.ChineseSimplified` dengan `OcrLanguage.English` (atau nilai enum lain) hanya memerlukan satu baris perubahan.

```csharp
using System;
using YourOcrLibrary;   // Replace with the actual namespace of your OCR SDK

// Step 1: Create and configure the OCR engine for Simplified Chinese
var ocrEngine = new OcrEngine
{
    // Primary keyword appears here naturally
    Language = OcrLanguage.ChineseSimplified,

    // Point to a folder that already contains the Chinese model files
    ResourceFolder = @"C:\OcrResources"
};
```

**Mengapa ini penting:**  
Menetapkan properti `Language` memberi tahu mesin set karakter apa yang diharapkan. `ResourceFolder` adalah tempat mesin mencari bobot jaringan saraf dan kamus bahasa—anggap saja ini sebagai bank memori otak. Jika Anda menunjuk ke folder yang salah, mesin akan melempar `FileNotFoundException` dan Anda akan terhenti.

## Ekstrak Teks dari Gambar – Memuat Sumber Daya

Sebelum mesin dapat benar‑benar membaca apa pun, Anda harus memuat file model tersebut ke memori. Langkah ini **krusial** karena menghindari panggilan jaringan setiap kali Anda memproses sebuah gambar.

```csharp
// Step 2: Load the language resources from the specified folder (no internet required)
try
{
    ocrEngine.LoadResources();
    Console.WriteLine("Resources loaded successfully.");
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Failed to load OCR resources: {ex.Message}");
    // In a real app you might fallback to a default language or abort gracefully
}
```

**Apa yang bisa salah?**  
Jika jalur folder salah atau file rusak, `LoadResources()` akan menghasilkan pengecualian. Blok `try/catch` di atas menunjukkan penanganan error yang elegan—sesuatu yang sering Anda perlukan di produksi.

## Mengenali Teks dari Foto – Menjalankan OCR

Sekarang bagian yang menyenangkan: memberi file gambar ke mesin dan mendapatkan kembali teks yang dikenali. Inilah inti dari skenario **menjalankan OCR pada gambar**, baik gambar tersebut JPEG, PNG, atau bahkan BMP.

```csharp
// Step 3: Recognize text from an image file
string imagePath = @"C:\OcrResources\photo.jpg";

try
{
    var recognitionResult = ocrEngine.RecognizeImage(imagePath);
    Console.WriteLine("=== OCR Output ===");
    Console.WriteLine(recognitionResult.Text);
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Error during OCR processing: {ex.Message}");
}
```

Metode `RecognizeImage` mengembalikan sebuah `RecognitionResult` (atau apa pun yang disebut dalam SDK Anda) yang biasanya berisi:

- `Text` – transkripsi teks polos.  
- `Confidence` – skor numerik yang menunjukkan seberapa yakin mesin terhadap tiap baris.  
- `BoundingBoxes` – koordinat opsional untuk posisi masing‑masing kata pada gambar.

**Mengapa Anda mungkin peduli pada confidence:**  
Jika Anda membangun alat otomasi entri data, Anda dapat menetapkan ambang batas (misalnya, 0.85) dan meminta pengguna mengonfirmasi baris dengan confidence rendah. Hal ini secara dramatis meningkatkan akurasi keseluruhan.

## Mengenali Teks dari JPG – Menangani Berbagai Format

Banyak pengembang berasumsi OCR hanya bekerja dengan PNG, tetapi mesin modern juga menangani **JPG** dengan baik. Satu‑satunya hal yang perlu diwaspadai adalah kompresi JPEG yang dapat menimbulkan artefak yang membingungkan model.

```csharp
// Bonus: Recognize text from a JPG with optional preprocessing
string jpgPath = @"C:\OcrResources\scanned_doc.jpg";

// Optional: use a simple image‑preprocess step to improve accuracy
var preprocessed = ImageHelper.DenoiseAndDeskew(jpgPath); // pseudo‑method
var result = ocrEngine.RecognizeImage(preprocessed);
Console.WriteLine($"Detected text ({result.Confidence:P0} confidence):");
Console.WriteLine(result.Text);
```

Jika Anda tidak memiliki helper `DenoiseAndDeskew`, banyak perpustakaan (misalnya OpenCvSharp) menyediakan fungsi tersebut. Inti yang perlu diingat: **menjalankan OCR pada gambar** setelah sedikit pembersihan bila gambar berasal dari scanner atau kamera ponsel.

## Menjalankan OCR pada Gambar – Tips, Kasus Tepi, dan Praktik Terbaik

### 1. Manajemen Memori
Memuat model bahasa besar dapat mengonsumsi ratusan megabyte. Buang (dispose) mesin ketika selesai:

```csharp
ocrEngine.Dispose(); // or using statement if the SDK implements IDisposable
```

### 2. Pemrosesan Batch
Jika Anda perlu memproses puluhan foto, muat sumber daya sekali, lalu lakukan perulangan:

```csharp
string[] files = Directory.GetFiles(@"C:\BatchPhotos", "*.jpg");
foreach (var file in files)
{
    var res = ocrEngine.RecognizeImage(file);
    File.WriteAllText(Path.ChangeExtension(file, ".txt"), res.Text);
}
```

### 3. Skenario Multi‑Bahasa
Anda dapat mengganti bahasa secara dinamis dengan menetapkan kembali `ocrEngine.Language` dan memanggil `LoadResources()` lagi. Hanya saja, bersiaplah untuk waktu pemuatan tambahan.

### 4. Menangani Hasil Kosong
Kadang‑kadang mesin mengembalikan string kosong. Itu biasanya berarti gambar terlalu buram atau warna teks menyatu dengan latar belakang. Pemeriksaan cepat:

```csharp
if (string.IsNullOrWhiteSpace(recognitionResult.Text))
{
    Console.WriteLine("No text detected – consider increasing image contrast.");
}
```

### 5. Pertimbangan Keamanan
Jangan pernah langsung memberi file yang di‑upload pengguna ke mesin OCR tanpa validasi. Minimal, verifikasi ekstensi file dan ukuran, serta pertimbangkan pemindaian malware.

---

## Contoh Program Lengkap yang Berfungsi

Berikut adalah program tunggal yang berdiri sendiri yang dapat Anda salin ke proyek Console App baru. Program ini mendemonstrasikan **cara menggunakan OCR**, **mengekstrak teks dari gambar**, **mengenali teks dari foto**, **mengenali teks dari JPG**, dan **menjalankan OCR pada gambar**—semuanya dalam satu langkah.

```csharp
// File: Program.cs
using System;
using System.IO;
using YourOcrLibrary; // Replace with actual namespace

namespace OcrDemo
{
    class Program
    {
        static void Main()
        {
            // ------------------------------
            // 1️⃣ Configure the OCR engine
            // ------------------------------
            var ocrEngine = new OcrEngine
            {
                Language = OcrLanguage.ChineseSimplified,
                ResourceFolder = @"C:\OcrResources"
            };

            // Load language resources (no internet needed)
            try
            {
                ocrEngine.LoadResources();
                Console.WriteLine("Resources loaded.");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"Failed to load resources: {ex.Message}");
                return;
            }

            // -------------------------------------------------
            // 2️⃣ Recognize text from a photo (JPG in this case)
            // -------------------------------------------------
            string imagePath = @"C:\OcrResources\photo.jpg";

            if (!File.Exists(imagePath))
            {
                Console.Error.WriteLine($"Image not found: {imagePath}");
                return;
            }

            try
            {
                var result = ocrEngine.RecognizeImage(imagePath);
                Console.WriteLine("\n=== OCR Output ===");
                Console.WriteLine(result.Text);
                Console.WriteLine($"\nConfidence: {result.Confidence:P2}");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"OCR error: {ex.Message}");
            }

            // Clean up
            ocrEngine.Dispose();
        }
    }
}
```

**Output yang diharapkan (contoh):**

```
Resources loaded.

=== OCR Output ===
中华人民共和国
北京
2026年02月13日

Confidence: 92.45%
```

Teks sebenarnya akan berbeda tergantung pada konten gambar, tetapi Anda seharusnya melihat sekumpulan karakter Unicode tercetak di konsol bersama persentase confidence.

---

## Kesimpulan

Kami telah membahas **cara menggunakan OCR** di C# dari awal hingga akhir—mengonfigurasi mesin, memuat sumber daya bahasa, dan akhirnya **mengenali teks dari foto** atau **JPG** tanpa pernah menyentuh internet. Dengan mengikuti langkah‑langkah di atas Anda dapat **mengekstrak teks dari gambar**, **menjalankan OCR pada aset gambar**, dan menangani jebakan umum yang sering membuat pemula kebingungan.

Siap untuk tantangan berikutnya? Cobalah memberi mesin halaman PDF yang telah dikonversi menjadi gambar, atau bereksperimen dengan paket bahasa lain untuk melihat bagaimana skor confidence berubah. Anda mungkin

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}