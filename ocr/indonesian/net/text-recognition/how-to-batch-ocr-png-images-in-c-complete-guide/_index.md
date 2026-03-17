---
category: general
date: 2026-03-17
description: Cara melakukan OCR batch pada gambar PNG di C# dengan cepat. Pelajari
  cara mengekstrak teks dari file PNG, mengonversi PNG ke teks, dan membaca gambar
  dari direktori dengan skrip sederhana.
draft: false
keywords:
- how to batch OCR
- extract text png
- convert png to text
- read images from directory
language: id
og_description: Cara melakukan OCR batch pada gambar PNG di C# dengan kode langkah
  demi langkah. Ekstrak teks dari file PNG, konversi PNG ke teks, dan baca gambar
  dari direktori dengan mudah.
og_title: Cara Memproses OCR Gambar PNG Secara Batch di C# – Panduan Lengkap
tags:
- OCR
- C#
- Image Processing
title: Cara Memproses OCR PNG Secara Batch di C# – Panduan Lengkap
url: /id/net/text-recognition/how-to-batch-ocr-png-images-in-c-complete-guide/
---

Now produce final output with all content translated.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Batch OCR Gambar PNG di C# – Panduan Lengkap

Pernah bertanya-tanya **bagaimana cara batch OCR** sebuah folder penuh screenshot tanpa membuka setiap file secara manual? Anda bukan satu-satunya—para pengembang terus-menerus menanyakan cara batch OCR koleksi PNG yang besar, terutama ketika tujuannya adalah mengekstrak teks dari file PNG untuk analisis lanjutan.  

Dalam tutorial ini kami akan membahas contoh C# yang siap‑jalankan yang **mengekstrak teks PNG** file, **mengonversi PNG ke teks**, dan menunjukkan cara terbaik untuk **membaca gambar dari direktori**. Pada akhir tutorial Anda akan memiliki satu skrip yang menempatkan file `.txt` di samping setiap gambar, menghemat berjam‑jam penyalinan manual.

## Apa yang Akan Anda Capai

- Menginisialisasi mesin OCR sekali dan menggunakannya kembali untuk seluruh batch.  
- Memindai setiap `*.png` dalam folder yang diberikan tanpa menulis loop sendiri.  
- Menulis setiap hasil OCR ke file teks masing‑masing, mempertahankan nama file asli.  
- Menangani kasus tepi umum seperti folder kosong atau file bukan gambar dengan elegan.

### Prasyarat

- .NET 6.0 atau lebih baru (kode ini juga bekerja pada .NET Core dan .NET Framework).  
- Sebuah perpustakaan OCR yang menyediakan tipe `OcrEngine`, `ImageStream`, dan `OcrResult` (misalnya, SDK fiktif **FastOCR** yang digunakan dalam potongan kode).  
- Pengetahuan dasar C#—tidak memerlukan pola lanjutan.

---

## Cara Batch OCR Gambar PNG – Ikhtisar

Berikut adalah **program lengkap yang dapat dijalankan**. Silakan salin‑tempel ke dalam proyek konsol baru, ganti jalur placeholder, dan tekan **F5**.

```csharp
using System;
using System.IO;
using System.Linq;
using FastOCR;               // <-- Replace with your actual OCR namespace

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Initialize the OCR engine (language = English)
        // -------------------------------------------------
        var ocrEngine = new OcrEngine();
        ocrEngine.Config.Language = Language.English;

        // -------------------------------------------------
        // Step 2: Locate every PNG file in the input folder
        // -------------------------------------------------
        string inputFolder = @"YOUR_DIRECTORY\images";
        string[] imagePaths = Directory.GetFiles(inputFolder, "*.png");

        if (imagePaths.Length == 0)
        {
            Console.WriteLine("No PNG files found – nothing to process.");
            return;
        }

        // -------------------------------------------------
        // Step 3: Convert file paths to ImageStream objects
        // -------------------------------------------------
        var imageStreams = imagePaths
            .Select(path => ImageStream.FromFile(path))
            .ToList();

        // -------------------------------------------------
        // Step 4: Recognize text in the entire batch
        // -------------------------------------------------
        IReadOnlyList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);

        // -------------------------------------------------
        // Step 5: Write each result to a .txt file next to the image
        // -------------------------------------------------
        string outputFolder = @"YOUR_DIRECTORY\output";
        Directory.CreateDirectory(outputFolder); // ensures the folder exists

        for (int i = 0; i < ocrResults.Count; i++)
        {
            string originalFileName = Path.GetFileNameWithoutExtension(imagePaths[i]);
            string outputPath = Path.Combine(outputFolder, $"{originalFileName}.txt");
            File.WriteAllText(outputPath, ocrResults[i].Text);
            Console.WriteLine($"✅ {originalFileName}.txt created");
        }

        Console.WriteLine("All done! Check the output folder for your text files.");
    }
}
```

> **Output yang diharapkan:** Untuk setiap `image01.png` Anda akan menemukan `image01.txt` yang berisi karakter yang dikenali. Konsol akan menampilkan setiap file saat ditulis.

![Diagram cara batch OCR](how-to-batch-ocr-diagram.png "Diagram yang menggambarkan cara batch OCR gambar PNG menggunakan C#")

---

## Penjelasan Langkah‑per‑Langkah

### 1. Inisialisasi Mesin OCR – Inti Proses  

Baris `var ocrEngine = new OcrEngine();` membuat satu instance mesin yang akan digunakan kembali untuk seluruh batch. Menggunakan kembali mesin **sangat penting** karena kebanyakan perpustakaan OCR mengalokasikan sumber daya berat (seperti model bahasa) pada saat konstruksi. Menginisialisasi sekali meningkatkan kinerja secara dramatis—terutama ketika Anda memiliki puluhan atau ratusan PNG.  

> **Tip Pro:** Jika Anda membutuhkan bahasa selain Inggris, setel `ocrEngine.Config.Language = Language.Spanish;` (atau enum yang didukung lainnya).  

### 2. Baca Gambar dari Direktori – menemukan setiap PNG  

`Directory.GetFiles(@"YOUR_DIRECTORY\images", "*.png")` melakukan tepat apa yang dijanjikan oleh kata kunci sekunder *read images from directory*. Ia mengembalikan array jalur absolut, yang kemudian kami berikan ke mesin OCR.  

> **Mengapa tidak menggunakan `SearchOption.AllDirectories`?** Jika gambar Anda berada dalam sub‑folder, Anda dapat beralih ke `GetFiles(path, "*.png", SearchOption.AllDirectories)`. Ingatlah bahwa pemindaian yang lebih dalam dapat membawa file yang tidak diinginkan, jadi filterlah sesuai kebutuhan.

### 3. Konversi Jalur File menjadi Objek ImageStream  

Sebagian besar SDK OCR mengharapkan sebuah stream bukan jalur mentah. Ekspresi LINQ `Select(path => ImageStream.FromFile(path)).ToList()` membangun **daftar stream** yang dapat dikonsumsi oleh pengenalan batch dalam satu panggilan. Langkah ini juga memastikan bahwa handle file dibuka hanya sekali, mengurangi overhead I/O.  

> **Kasus tepi:** Jika sebuah file rusak, `ImageStream.FromFile` dapat melempar pengecualian. Bungkus konversi dalam `try/catch` jika Anda memerlukan ketahanan.

### 4. Kenali Teks dalam Seluruh Batch  

`ocrEngine.RecognizeBatch(imageStreams)` adalah titik optimal untuk *how to batch OCR*. Alih‑alih mengulang setiap gambar dan memanggil metode satu‑gambar, kami menyerahkan seluruh koleksi ke mesin. Secara internal perpustakaan dapat memparalelkan pekerjaan, memberikan peningkatan kecepatan pada mesin multi‑core.  

> **Tip:** Jika perpustakaan OCR Anda tidak menyediakan metode batch, Anda masih dapat mencapai kinerja serupa dengan menggunakan `Parallel.ForEach` di sekitar pemanggilan `Recognize` satu‑gambar.

### 5. Tulis Setiap Hasil OCR – mengonversi PNG ke teks  

Loop `for` terakhir menulis `ocrResults[i].Text` ke file `.txt` yang namanya mencerminkan PNG asli. Ini persis seperti yang dijelaskan oleh kata kunci sekunder *convert PNG to text*. Pemanggilan `Path.Combine` menjamin folder output ada dan mencegah bug traversal jalur.  

> **Jebakan umum:** Lupa membuat folder output terlebih dahulu akan menyebabkan `DirectoryNotFoundException`. Baris `Directory.CreateDirectory(outputFolder);` menyelesaikannya secara preventif.

## Menangani Variasi Dunia‑Nyata

| Situation | What to Change | Why |
|-----------|----------------|-----|
| **Empty input folder** | Biarkan guard awal `if (imagePaths.Length == 0)` | Mencegah pemanggilan OCR yang tidak perlu dan memberikan pesan yang ramah |
| **Mixed file types** | Gunakan `Directory.EnumerateFiles(..., "*.*", SearchOption.TopDirectoryOnly).Where(f => f.EndsWith(".png", StringComparison.OrdinalIgnoreCase))` | Menjamin Anda hanya memproses PNG, memenuhi *extract text png* tanpa error |
| **Huge images ( > 5 MB )** | Downscale sebelum memberi ke OCR: `ImageStream.FromFile(path).Resize(1920, 1080)` (jika API mendukung) | Mengurangi tekanan memori dan sering meningkatkan akurasi pengenalan |
| **Different OCR language** | Set `ocrEngine.Config.Language = Language.French;` | Menyelaraskan mesin dengan bahasa gambar sumber |

## Pertanyaan yang Sering Diajukan (FAQ)

**Q: Apakah ini bekerja dengan file JPEG atau TIFF?**  
A: Logika inti tetap sama; cukup ubah pola pencarian menjadi `"*.jpg"` atau `"*.tif"` dan pastikan perpustakaan OCR dapat mendekode format tersebut.

**Q: Bagaimana saya dapat memproses ribuan gambar tanpa kehabisan memori?**  
A: Ganti pemanggilan batch dengan pendekatan streaming—proses sekumpulan, misalnya 50 gambar sekaligus, lalu lepaskan stream sebelum memuat kumpulan berikutnya.

**Q: Saya membutuhkan skor kepercayaan OCR. Di mana saya dapat menemukannya?**  
A: Sebagian besar objek `OcrResult` menyediakan properti `Confidence`. Anda dapat memperluas langkah penulisan:

```csharp
var result = ocrResults[i];
string content = $"Confidence: {result.Confidence:P2}\n{result.Text}";
File.WriteAllText(outputPath, content);
```

## Kesimpulan

Kami baru saja membahas **cara batch OCR** gambar PNG di C# dari awal hingga akhir. Dengan menginisialisasi satu mesin, membaca gambar dari direktori, mengonversinya menjadi stream, mengenali seluruh batch, dan akhirnya menulis setiap hasil ke file teks, Anda kini memiliki pola yang kuat dan siap produksi untuk tugas **extract text PNG**, **convert PNG to text**, dan **read images from directory**.

Apa selanjutnya? Coba ganti penyedia OCR, tambahkan pemrosesan pasca‑multithread (mis., pemeriksaan ejaan), atau masukkan file `.txt` ke dalam indeks pencarian. Langit adalah batasnya setelah Anda menguasai alur kerja batch.

Punya variasi yang ingin dibagikan? Tinggalkan komentar, dan selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}