---
category: general
date: 2026-03-17
description: Tutorial OCR c# – temukan cara mengekstrak teks dari file gambar, membaca
  teks dari foto WebP, dan mengonversi gambar menjadi teks menggunakan OcrEngine sederhana.
draft: false
keywords:
- c# OCR tutorial
- extract text from image
- read text from webp
- recognize text from photo
- convert image to text
language: id
og_description: Tutorial OCR c# menunjukkan cara mengekstrak teks dari file gambar,
  membaca teks dari foto WebP, dan mengonversi gambar menjadi teks dengan beberapa
  baris kode.
og_title: tutorial c# OCR – Ekstrak Teks dari Gambar dalam Hitungan Menit
tags:
- C#
- OCR
- Image Processing
title: 'Tutorial OCR c#: Ekstrak Teks dari Gambar (WebP, Foto) – Panduan Cepat'
url: /id/net/text-recognition/c-ocr-tutorial-extract-text-from-images-webp-photo-quick-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# tutorial c# OCR – Ekstrak Teks dari Gambar (WebP, Foto)

Pernah membutuhkan untuk **mengekstrak teks dari gambar** file tetapi tidak yakin harus mulai dari mana di C#? Mungkin Anda memiliki screenshot WebP, JPEG dari kwitansi, atau halaman PDF yang dipindai dan Anda hanya ingin kata‑katanya. Dalam **c# OCR tutorial** ini kami akan membahas contoh lengkap yang siap‑jalan yang membaca teks dari foto, menangani WebP dan format modern lainnya, dan mengonversi gambar menjadi teks biasa—semua dalam beberapa baris.

**Apa keuntungannya?** Anda akan dapat mengubah gambar apa pun yang berisi teks menjadi string yang dapat dicari, memasukkannya ke dalam basis data, atau mengirimnya ke alur kerja AI berikutnya. Tidak ada sihir, hanya mesin OCR yang solid, beberapa API .NET, dan penjelasan jelas tentang “mengapa” di balik setiap langkah.

## Apa yang Anda Butuhkan

- **.NET 6 SDK** (atau yang lebih baru). Kode di bawah ini dikompilasi dengan .NET 6+ dan berjalan di Windows, Linux, atau macOS.
- **Visual Studio 2022** atau editor apa pun yang Anda suka (VS Code juga dapat digunakan).
- Paket NuGet **`Microsoft.Windows.SDK.Contracts`** (menyediakan `Windows.Media.Ocr`). Instal dengan:

```bash
dotnet add package Microsoft.Windows.SDK.Contracts
```

- Sebuah file gambar yang ingin Anda proses – untuk tutorial ini kami akan menggunakan foto **WebP** bernama `photo.webp` yang ditempatkan di folder bernama `YOUR_DIRECTORY`.

> Tips pro: Jika Anda berada di platform non‑Windows, Anda dapat mengganti `OcrEngine` dengan pustaka lintas‑platform seperti **Tesseract**. Kode di sekitarnya tetap hampir sama.

## Langkah 1: Siapkan Proyek Tutorial OCR C#

Pertama, buat aplikasi console baru. Buka terminal dan jalankan:

```bash
dotnet new console -n OcrDemo
cd OcrDemo
```

Tambahkan paket yang diperlukan (seperti yang ditunjukkan di atas) dan buka proyek di IDE Anda. Kerangka kerja ini memberi kami kanvas bersih untuk **c# OCR tutorial**.

## Langkah 2: Impor Namespace dan Siapkan Gambar

Kita memerlukan beberapa arahan `using` agar kompilator tahu di mana menemukan `OcrEngine`, `SoftwareBitmap`, dan pembantu pemuatan gambar.

```csharp
using System;
using System.IO;
using Windows.Graphics.Imaging;
using Windows.Media.Ocr;
using Windows.Storage.Streams;
```

> **Mengapa namespace ini?**  
> `Windows.Media.Ocr` berisi kelas `OcrEngine` yang sebenarnya melakukan pengenalan. `Windows.Graphics.Imaging` memungkinkan kami mendekode gambar (termasuk WebP) menjadi `SoftwareBitmap` yang dapat dipahami mesin. Pembantu `System.IO` dan `Windows.Storage.Streams` memudahkan pemuatan file.

Sekarang, muat gambar. Decoder bawaan dapat menangani WebP, HEIF, PNG, JPEG, dan lainnya, sehingga Anda dapat **membaca teks dari WebP** tanpa plugin tambahan.

```csharp
// Step 2: Load the image file into a SoftwareBitmap
string imagePath = Path.Combine("YOUR_DIRECTORY", "photo.webp");

// Open the file as a random access stream
using (IRandomAccessStream stream = File.OpenRead(imagePath).AsRandomAccessStream())
{
    // Decode the image (auto-detects format)
    BitmapDecoder decoder = await BitmapDecoder.CreateAsync(stream);
    SoftwareBitmap bitmap = await decoder.GetSoftwareBitmapAsync();
    
    // Optional: Convert to grayscale for better OCR accuracy
    SoftwareBitmap grayBitmap = SoftwareBitmap.Convert(bitmap, BitmapPixelFormat.Gray8);
    
    // Pass the bitmap to the next step
    await RecognizeTextAsync(grayBitmap);
}
```

> **Kasus khusus:** Jika gambar Anda sudah hitam‑putih, Anda dapat melewatkan langkah konversi. Konversi ke skala abu‑abu memberikan peningkatan kinerja kecil dan sering meningkatkan pengenalan pada foto yang berisik.

## Langkah 3: Jalankan Mesin OCR – Kenali Teks dari Foto

Berikut inti dari **c# OCR tutorial**. Kami membuat instance `OcrEngine`, memberinya bitmap, dan mengambil teks yang dikenali.

```csharp
static async Task RecognizeTextAsync(SoftwareBitmap bitmap)
{
    // Step 3: Create the OCR engine instance – it automatically picks the best language
    OcrEngine ocrEngine = OcrEngine.TryCreateFromUserProfileLanguages();

    if (ocrEngine == null)
    {
        Console.WriteLine("❌ No OCR engine available for the current language.");
        return;
    }

    // Perform recognition
    OcrResult ocrResult = await ocrEngine.RecognizeAsync(bitmap);

    // Step 4: Display the extracted text – this is the “convert image to text” part
    Console.WriteLine("📝 Recognized text:");
    Console.WriteLine(ocrResult.Text);
}
```

**Apa yang terjadi?**  
- `TryCreateFromUserProfileLanguages()` memilih bahasa yang diatur pada profil pengguna Windows Anda, yang biasanya mencakup Inggris, Spanyol, dll. Jika Anda membutuhkan bahasa tertentu, gunakan `OcrEngine.TryCreateFromLanguage(new Language("fr-FR"))`.
- `RecognizeAsync` melakukan pekerjaan berat pada thread latar belakang, mengembalikan `OcrResult` yang berisi string mentah, kotak pembatas kata, dan skor kepercayaan.
- Akhirnya, kami mencetak `ocrResult.Text`, memberikan Anda hasil **mengonversi gambar menjadi teks** yang dapat Anda alirkan ke tempat lain.

## Langkah 4: Contoh Lengkap yang Dapat Dijalankan

Menggabungkan semuanya, berikut program mandiri yang dapat Anda salin‑tempel ke `Program.cs`. Program ini mengompilasi, berjalan, dan mencetak teks yang diekstrak dari `photo.webp`.

```csharp
// Program.cs – Complete c# OCR tutorial example
using System;
using System.IO;
using System.Threading.Tasks;
using Windows.Graphics.Imaging;
using Windows.Media.Ocr;
using Windows.Storage.Streams;

class Program
{
    static async Task Main(string[] args)
    {
        // Replace with your actual directory and file name
        string imagePath = Path.Combine("YOUR_DIRECTORY", "photo.webp");

        if (!File.Exists(imagePath))
        {
            Console.WriteLine($"❗ Image not found: {imagePath}");
            return;
        }

        // Load and optionally preprocess the image
        using (IRandomAccessStream stream = File.OpenRead(imagePath).AsRandomAccessStream())
        {
            BitmapDecoder decoder = await BitmapDecoder.CreateAsync(stream);
            SoftwareBitmap bitmap = await decoder.GetSoftwareBitmapAsync();

            // Convert to grayscale – improves OCR accuracy on many photos
            SoftwareBitmap grayBitmap = SoftwareBitmap.Convert(bitmap, BitmapPixelFormat.Gray8);

            // Run OCR
            await RecognizeTextAsync(grayBitmap);
        }
    }

    static async Task RecognizeTextAsync(SoftwareBitmap bitmap)
    {
        // Create OCR engine (auto‑detect language)
        OcrEngine ocrEngine = OcrEngine.TryCreateFromUserProfileLanguages();

        if (ocrEngine == null)
        {
            Console.WriteLine("❌ Unable to create OCR engine. Ensure language packs are installed.");
            return;
        }

        // Perform recognition
        OcrResult result = await ocrEngine.RecognizeAsync(bitmap);

        // Output the extracted text
        Console.WriteLine("\n--- OCR Output ---");
        Console.WriteLine(result.Text);
        Console.WriteLine("--- End of Output ---\n");
    }
}
```

### Output yang Diharapkan

Jika `photo.webp` berisi kalimat “Hello, world! This is a test.” Anda akan melihat sesuatu seperti:

```
--- OCR Output ---
Hello, world!
This is a test.
--- End of Output ---
```

Pemecahan baris yang tepat tergantung pada tata letak gambar sumber, tetapi hasil **extract text from image** akan selalu berupa string biasa yang dapat Anda manipulasi lebih lanjut.

## Pertanyaan Umum & Kasus Khusus

### Apakah ini bekerja dengan format gambar lain?

Tentu saja. Decoder yang digunakan (`BitmapDecoder`) secara otomatis mendeteksi JPEG, PNG, BMP, GIF, **WebP**, HEIF, dan lainnya. Jadi Anda dapat **read text from WebP**, JPEG, atau bahkan TIFF tanpa mengubah kode.

### Bagaimana jika mesin OCR mengembalikan kepercayaan rendah?

Anda dapat memeriksa `ocrResult.Lines` dan setiap `OcrWord` untuk `ConfidenceScore`. Jika skor di bawah ambang batas (mis., 0.6), pertimbangkan:

- Pra‑pemrosesan gambar (meningkatkan kontras, menajamkan, meluruskan).
- Menggunakan gambar sumber dengan resolusi lebih tinggi.
- Beralih ke pustaka khusus seperti **Tesseract** untuk dukungan multibahasa.

### Bagaimana menangani banyak bahasa dalam satu gambar?

Buat instance `OcrEngine` terpisah untuk setiap bahasa dan jalankan secara berurutan, atau gunakan pustaka yang mendukung deteksi bahasa campuran. Untuk mesin bawaan, Anda dapat melewatkan objek `Language`:

```csharp
var spanishEngine = OcrEngine.TryCreateFromLanguage(new Language("es-ES"));
```

### Bisakah saya menjalankannya di Linux/macOS?

API `Windows.Media.Ocr` hanya tersedia di Windows. Pada platform non‑Windows, ganti bagian OCR dengan **Tesseract** (melalui `Tesseract.Net.SDK`). Kode pemuatan dan pra‑pemrosesan tetap sama, sehingga bagian lain dari **c# OCR tutorial** ini tetap berlaku.

## Tips Pro untuk Akurasi Lebih Baik

- **Resize** gambar besar hingga maksimum 2000 px pada sisi terpanjang – mesin OCR bekerja lebih cepat pada ukuran sedang.
- **Denoise** menggunakan blur Gaussian sederhana jika foto berbutir.
- **Deskew** bitmap jika teks tidak sepenuhnya horizontal; `SoftwareBitmap` dapat diputar sebelum diberikan ke `OcrEngine`.
- **Cache** instance `OcrEngine` jika Anda memproses banyak gambar dalam satu batch; membuatnya berulang‑ulang menambah beban.

## Topik Terkait untuk Dijelajahi

- **Convert image to text** menggunakan **Tesseract** untuk proyek lintas‑platform.
- **Extract text from PDF** dengan merender setiap halaman menjadi gambar terlebih dahulu.
- **Batch OCR**

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}