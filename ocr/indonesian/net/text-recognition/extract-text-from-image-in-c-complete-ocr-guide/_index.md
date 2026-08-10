---
category: general
date: 2026-07-21
description: Ekstrak teks dari gambar menggunakan C# OCR – pelajari cara mengonversi
  PNG menjadi teks, memuat gambar untuk OCR, dan mengenali teks Sirilik dengan Aspose.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- extract text from image
- convert png to text
- c# ocr example
- load image for ocr
- recognize cyrillic text
language: id
lastmod: 2026-07-21
og_description: Ekstrak teks dari gambar dengan C# OCR. Panduan ini menunjukkan cara
  mengonversi PNG ke teks, memuat gambar untuk OCR, dan mengenali teks Cyrillic menggunakan
  Aspose.OCR.
og_image_alt: Screenshot of C# code extracting text from an image using Aspose OCR
og_title: Ekstrak Teks dari Gambar di C# – Panduan Lengkap OCR
schemas:
- author: Aspose
  dateModified: '2026-07-21'
  description: Extract text from image using C# OCR – learn to convert PNG to text,
    load image for OCR, and recognize Cyrillic text with Aspose.
  headline: Extract Text from Image in C# – Complete OCR Guide
  type: TechArticle
tags:
- OCR
- C#
- Aspose
- Image Processing
- Cyrillic
title: Ekstrak Teks dari Gambar di C# – Panduan OCR Lengkap
url: /id/net/text-recognition/extract-text-from-image-in-c-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ekstrak Teks dari Gambar di C# – Panduan OCR Lengkap

Pernah bertanya-tanya bagaimana cara **mengekstrak teks dari gambar** tanpa meninggalkan proyek C# Anda? Mungkin Anda memiliki sekumpulan struk yang dipindai, sekumpulan tanda Cyrillic, atau hanya screenshot PNG yang perlu diubah menjadi teks yang dapat dicari. Singkatnya, Anda menginginkan mesin OCR yang handal yang dapat *mengonversi PNG ke teks* secara langsung.  

Kabar baik—Aspose.OCR membuat hal itu menjadi mungkin dengan hanya beberapa baris kode. Di bawah ini Anda akan melihat **contoh OCR C#** yang memuat gambar untuk OCR, menjalankan pengenalan, dan mencetak hasilnya, bahkan ketika bahasa sumbernya Cyrillic.

## Apa yang Dibahas dalam Tutorial Ini

- Menyiapkan mesin Aspose.OCR untuk pengenalan Cyrillic.  
- **Muat gambar untuk OCR** dari jalur file atau stream.  
- **Konversi PNG ke teks** dan keluarkan string biasa.  
- Menangani kegagalan dan jebakan umum saat Anda **mengenali teks Cyrillic**.  

Pada akhir panduan ini Anda akan memiliki program mandiri yang dapat dijalankan hari ini, plus beberapa tips yang membuat pipeline OCR Anda tetap kuat.

> **Prasyarat**  
> - .NET 6.0 atau lebih baru (kode ini juga bekerja pada .NET Framework 4.7+).  
> - Lisensi Aspose.OCR yang valid atau kunci evaluasi 30‑hari.  
> - Paket NuGet `Aspose.OCR` terpasang (`dotnet add package Aspose.OCR`).  

Jika Anda belum memiliki salah satu dari itu, dapatkan dulu—tidak ada hal lain yang diperlukan.

---

## Ekstrak Teks dari Gambar – Langkah 1: Instal & Inisialisasi Mesin OCR

Pertama-tama, kita memerlukan instance mesin OCR dan harus memberi tahu bahasa yang diharapkan. Aspose mendukung lebih dari 70 bahasa, dan untuk Cyrillic kita gunakan `OcrLanguage.Cyrillic`.

```csharp
using Aspose.OCR;
using System;

// Step 1: Create the engine and set the language to Cyrillic.
OcrEngine engine = new OcrEngine
{
    Language = OcrLanguage.Cyrillic
};
```

> **Mengapa mengatur bahasa?**  
> Akurasi OCR turun drastis jika mesin menebak skrip yang salah. Dengan secara eksplisit menentukan Cyrillic, kita memberi mesin *head start*—ia mempersempit set karakter yang harus dipertimbangkan, yang mempercepat pemrosesan dan mengurangi kesalahan pengenalan.

---

## Konversi PNG ke Teks – Langkah 2: Muat Gambar untuk OCR

Sekarang kita benar‑benarnya **memuat gambar untuk OCR**. Contoh ini menggunakan file PNG, tetapi Aspose menerima JPEG, BMP, TIFF, dan bahkan halaman PDF.

```csharp
// Step 2: Load the PNG you want to convert to text.
engine.Image = ImageStream.FromFile("YOUR_DIRECTORY/sample_cyrillic.png");
```

Jika Anda lebih suka bekerja dengan `MemoryStream` (misalnya, ketika gambar datang dari permintaan web), cukup ganti baris di atas dengan:

```csharp
using (var ms = new MemoryStream(File.ReadAllBytes("sample_cyrillic.png")))
{
    engine.Image = ImageStream.FromStream(ms);
}
```

> **Tip:** Pertahankan resolusi gambar setidaknya 300 dpi untuk hasil terbaik. Screenshot beresolusi rendah sering menghasilkan output yang berantakan, terutama dengan alfabet non‑Latin.

---

## Contoh OCR C# – Langkah 3: Lakukan Pengenalan

Dengan mesin siap dan gambar sudah dimuat, pekerjaan OCR sebenarnya hanyalah satu pemanggilan metode.

```csharp
// Step 3: Run the recognition engine.
bool success = engine.Recognize();
```

Metode `Recognize()` mengembalikan `true` ketika menemukan teks yang dapat dikenali. Jika mengembalikan `false`, Anda perlu menyelidiki penyebabnya—mungkin gambar terlalu buram atau bahasa belum diatur dengan benar.

---

## Mengenali Teks Cyrillic – Langkah 4: Ambil dan Gunakan Hasilnya

Dengan asumsi pengenalan berhasil, Anda kini dapat **mengekstrak teks dari gambar** dan melakukan apa saja yang Anda perlukan: menyimpannya ke basis data, mengirimnya ke indeks pencarian, atau sekadar menampilkannya.

```csharp
if (success)
{
    // Step 4: Grab the plain text.
    string plainText = engine.Text;
    Console.WriteLine("=== OCR RESULT ===");
    Console.WriteLine(plainText);
}
else
{
    // Step 5: Handle recognition failure gracefully.
    Console.WriteLine("Recognition failed. Check image quality or language settings.");
}
```

### Output yang Diharapkan

Menjalankan program lengkap terhadap PNG Cyrillic yang jelas menghasilkan sesuatu seperti:

```
=== OCR RESULT ===
Пример текста на кириллице
```

Jika gambar berisi bahasa Inggris yang dicampur dengan Cyrillic, Aspose akan mengeluarkan kedua skrip selama bahasa diatur ke Cyrillic (ia mencakup subset Latin).

---

## Jebakan Umum dan Pro Tip

| Masalah | Mengapa Terjadi | Cara Memperbaikinya |
|---------|----------------|---------------------|
| **PNG buram atau beresolusi rendah** | Mesin OCR bergantung pada tepi karakter yang jelas. | Tingkatkan gambar ke 300 dpi atau terapkan filter penajaman sebelum memberi ke Aspose. |
| **Pengaturan bahasa yang salah** | Mesin mencoba mencocokkan karakter dengan skrip yang tidak tepat. | Selalu atur `engine.Language` ke bahasa yang Anda harapkan, misalnya `OcrLanguage.Cyrillic`. |
| **File besar menyebabkan tekanan memori** | Memuat gambar besar ke dalam `MemoryStream` dapat menghabiskan heap. | Gunakan `engine.Image = ImageStream.FromFile(path)` untuk pemrosesan langsung dari disk, atau proses halaman secara bertahap. |
| **Pengenalan mengembalikan string kosong** | Mesin mungkin tidak mendeteksi zona teks. | Panggil `engine.SetImageProcessingOptions(new ImageProcessingOptions { DetectTextRegions = true })` sebelum `Recognize()`. |

> **Pro tip:** Jika Anda perlu *mengekstrak teks dari gambar* secara massal, bungkus logika di atas dalam loop `Parallel.ForEach`—pastikan setiap thread membuat instance `OcrEngine`‑nya sendiri. Mesin tidak bersifat thread‑safe.

---

## Memperluas Contoh: Banyak Bahasa & Panggilan Async

Kode yang ditampilkan bersifat sinkron dan berfokus pada Cyrillic. Pada aplikasi dunia nyata Anda mungkin perlu mendukung bahasa Inggris dan Cyrillic dalam dokumen yang sama. Aspose memungkinkan Anda mengatur *array bahasa*:

```csharp
engine.Language = OcrLanguage.Cyrillic | OcrLanguage.English;
```

Untuk aplikasi yang responsif, panggil `RecognizeAsync()` sebagai gantinya:

```csharp
await engine.RecognizeAsync();
string result = engine.Text; // same property, now filled after await
```

Ingat untuk menandai metode `Main` Anda sebagai `async Task` jika Anda memilih jalur ini.

---

## Contoh Lengkap yang Siap Pakai

Berikut adalah program lengkap yang siap disalin‑tempel. Simpan sebagai `Program.cs`, tambahkan paket NuGet Aspose.OCR, dan jalankan dari command line.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine and set language to Cyrillic.
        OcrEngine engine = new OcrEngine
        {
            Language = OcrLanguage.Cyrillic
        };

        // 2️⃣ Load the PNG you want to convert to text.
        //    Replace the path with your actual file location.
        string imagePath = "YOUR_DIRECTORY/sample_cyrillic.png";

        if (!File.Exists(imagePath))
        {
            Console.WriteLine($"File not found: {imagePath}");
            return;
        }

        engine.Image = ImageStream.FromFile(imagePath);

        // 3️⃣ Perform the recognition.
        bool success = engine.Recognize();

        // 4️⃣ Retrieve and display the result.
        if (success)
        {
            string plainText = engine.Text;
            Console.WriteLine("=== OCR RESULT ===");
            Console.WriteLine(plainText);
        }
        else
        {
            Console.WriteLine("Recognition failed. Verify image quality and language settings.");
        }
    }
}
```

**Jalankan:**  

```bash
dotnet run
```

Anda akan melihat teks Cyrillic yang diekstrak tercetak di konsol.

---

## Kesimpulan

Kami telah menelusuri **contoh OCR C#** yang menunjukkan cara **mengekstrak teks dari gambar** file, khususnya PNG, menggunakan Aspose.OCR. Dengan mengatur bahasa ke Cyrillic, memuat gambar dengan benar, dan menangani jalur sukses serta kegagalan, Anda kini memiliki fondasi yang kuat untuk tugas ekstraksi teks apa pun—baik Anda mengonversi PNG ke teks untuk indeks pencarian atau membangun pemindai dokumen multibahasa.

Siap untuk langkah berikutnya? Coba ganti `OcrLanguage.Cyrillic` dengan `OcrLanguage.English` untuk melihat perbedaannya, atau bereksperimen dengan `ImageProcessingOptions` untuk meningkatkan akurasi pada pemindaian yang berisik. Dan jika Anda menemui kendala, dokumentasi Aspose serta forum komunitas adalah tempat yang bagus untuk menggali lebih dalam.

Selamat coding, semoga hasil OCR Anda selalu jernih!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Ekstrak teks gambar C# dengan pemilihan bahasa menggunakan Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Ekstrak Teks dari Gambar – Optimasi OCR dengan Aspose.OCR untuk .NET](/ocr/english/net/ocr-optimization/)
- [Cara Mengekstrak Teks dari Gambar Menggunakan Aspose.OCR untuk .NET](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}