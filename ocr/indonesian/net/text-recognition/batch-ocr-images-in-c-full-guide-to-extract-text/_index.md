---
category: general
date: 2026-02-24
description: Lakukan OCR gambar secara batch dengan cepat menggunakan Aspose.OCR di
  C#. Pelajari cara membaca file dari direktori, mengenali teks dari gambar, dan mengonversi
  gambar menjadi teks dalam beberapa langkah.
draft: false
keywords:
- batch OCR images
- extract text from images
- read files from directory
- recognize text from image
- convert image to text
language: id
og_description: Lakukan OCR batch pada gambar di C# menggunakan Aspose.OCR. Tutorial
  ini menunjukkan cara membaca file dari direktori, mengenali teks dari gambar, dan
  mengonversi gambar menjadi teks secara efisien.
og_title: Batch OCR Gambar di C# – Panduan Lengkap Langkah demi Langkah
tags:
- C#
- OCR
- Aspose
title: Pemrosesan OCR Gambar secara Batch di C# – Panduan Lengkap untuk Mengekstrak
  Teks
url: /id/net/text-recognition/batch-ocr-images-in-c-full-guide-to-extract-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Batch OCR Images di C# – Panduan Lengkap untuk Mengekstrak Teks

Pernah butuh **batch OCR images** tetapi tidak yakin harus mulai dari mana? Anda tidak sendirian—banyak pengembang mengalami hal yang sama ketika pertama kali mencoba **extract text from images** secara massal. Kabar baiknya, dengan beberapa baris C# dan Aspose.OCR Anda dapat mengubah folder penuh gambar menjadi file `.txt` yang rapi dalam sekejap.

Dalam tutorial ini kami akan membahas seluruh proses: membaca file dari direktori, memberi setiap gambar ke mesin OCR, dan akhirnya **convert image to text** file yang dapat Anda indeks, cari, atau masukkan ke dalam pipeline hilir. Pada akhir tutorial Anda akan memiliki aplikasi console mandiri yang dapat Anda tempatkan di solusi .NET mana pun.

## Apa yang Anda Butuhkan

- **.NET 6+** (contoh ini dikompilasi dengan .NET 6, tetapi versi terbaru mana pun dapat digunakan)
- **Aspose.OCR** paket NuGet (`Install-Package Aspose.OCR`)
- Sebuah folder berisi file gambar (`.png`, `.jpg`, dll.) yang ingin Anda proses
- Visual Studio, Rider, atau editor favorit Anda

Tidak ada file konfigurasi tambahan, tidak ada layanan eksternal—hanya kode C# murni yang berjalan secara lokal.

## Batch OCR Images – Menyiapkan Proyek

Pertama, buat proyek console baru:

```bash
dotnet new console -n BatchOcrDemo
cd BatchOcrDemo
dotnet add package Aspose.OCR
```

Perintah tersebut membuat proyek minimal dan mengunduh pustaka OCR. Setelah proses restore selesai, Anda siap menambahkan logika inti.

### Membaca File dari Direktori

Kita perlu memberi tahu aplikasi di mana gambar sumber berada dan ke mana file teks hasil harus disimpan. Menggunakan `System.IO` membuat ini sangat mudah.

```csharp
using System;
using System.IO;
using Aspose.OCR;

class BatchExample
{
    static void Main()
    {
        // 1️⃣ Define input and output folders
        string inputFolder  = @"C:\Images\ToProcess";   // <-- change to your source folder
        string outputFolder = @"C:\Images\OcrResults"; // <-- change to your target folder

        // 2️⃣ Ensure the output folder exists
        Directory.CreateDirectory(outputFolder);
```

> **Mengapa langkah ini penting:** Jika direktori output tidak ada, program akan melemparkan pengecualian saat mencoba menulis file `.txt`. `CreateDirectory` bersifat idempotent—tidak melakukan apa‑apa jika folder sudah ada, sehingga aman dipanggil setiap kali dijalankan.

### Mengenali Teks dari Gambar dan Mengonversi Gambar ke Teks

Sekarang kita menginisialisasi mesin OCR dan melakukan iterasi pada setiap file yang ditemukan. Loop menggunakan `Directory.GetFiles` dengan wildcard (`*.*`) sehingga mengambil *semua* file, tetapi Anda dapat memperketat filter menjadi `*.png` atau `*.jpg` jika diinginkan.

```csharp
        // 3️⃣ Initialise the OCR engine
        var ocrEngine = new OcrEngine();

        // 4️⃣ Process each image file in the input folder
        foreach (var imagePath in Directory.GetFiles(inputFolder, "*.*", SearchOption.TopDirectoryOnly))
        {
            // 5️⃣ Recognise text from the current image
            var ocrResult = ocrEngine.RecognizeImage(imagePath);

            // 6️⃣ Save the recognised text to a .txt file in the output folder
            string textFilePath = Path.Combine(
                outputFolder,
                Path.GetFileNameWithoutExtension(imagePath) + ".txt");

            File.WriteAllText(textFilePath, ocrResult.Text);
        }

        Console.WriteLine("✅ All images processed. Check the output folder!");
    }
}
```

**Apa yang terjadi di sini?**  
- `ocrEngine.RecognizeImage(imagePath)` membaca bitmap, menjalankan algoritma OCR, dan mengembalikan objek `OcrResult`.  
- `ocrResult.Text` berisi representasi teks polos dari semua yang dapat dibaca mesin.  
- `File.WriteAllText` membuat file baru (atau menimpa yang sudah ada) dengan teks yang diekstrak.

Itulah seluruh pipeline **batch OCR images** dalam kurang dari 30 baris kode.

## Tips Pro & Kasus Tepi

| Situasi | Rekomendasi |
|-----------|----------------|
| Gambar berukuran besar ( > 5 MB ) | Skala ulang ke lebar ~1500 px untuk mempercepat pengenalan tanpa mengurangi akurasi. |
| Anda perlu mendukung PDF | Konversi setiap halaman PDF menjadi gambar terlebih dahulu (misalnya, menggunakan `Aspose.PDF`) lalu masukkan ke dalam loop yang sama. |
| Beberapa file bukan gambar (mis., `.txt`) | Tambahkan filter sederhana: `if (!imagePath.EndsWith(".png") && !imagePath.EndsWith(".jpg")) continue;` |
| Anda menginginkan dukungan multibahasa | Setel `ocrEngine.Language = Language.English | Language.Spanish;` sebelum loop. |
| Anda memerlukan pelaporan kemajuan | Tuliskan `Console.WriteLine($"Processing {Path.GetFileName(imagePath)}...");` di dalam foreach. |

> **Tip pro:** Bungkus pemanggilan OCR dalam `try/catch`. Kadang-kadang gambar yang rusak akan menyebabkan `RecognizeImage` melempar pengecualian; menanganinya mencegah seluruh batch berhenti.

## Output yang Diharapkan

Setelah program selesai, `outputFolder` akan berisi file `.txt` untuk setiap gambar asli:

```
C:\Images\OcrResults\invoice1.txt
C:\Images\OcrResults\receipt_2024-01-15.txt
C:\Images\OcrResults\signage.png.txt   <-- note the .txt extension
```

Setiap file berisi teks mentah yang diekstrak oleh mesin, misalnya:

```
Invoice #12345
Date: 01/15/2024
Total: $1,250.00
Thank you for your business!
```

Anda kini dapat memasukkan file-file ini ke dalam indeks pencarian, menjalankan analisis sentimen, atau sekadar mengarsipkannya untuk kepatuhan.

## Pertanyaan yang Sering Diajukan

**Q: Apakah ini bekerja di Linux?**  
A: Tentu saja. Aspose.OCR bersifat lintas‑platform, dan API `System.IO` yang digunakan di sini bersifat OS‑agnostik. Cukup sesuaikan jalur folder (`/home/user/images`).

**Q: Bagaimana jika saya perlu **read files from directory** secara rekursif?**  
A: Ubah `SearchOption.TopDirectoryOnly` menjadi `SearchOption.AllDirectories`. Perhatikan masalah izin pada folder yang lebih dalam.

**Q: Seberapa akurat OCR?**  
A: Akurasi tergantung pada kualitas gambar, jenis font, dan bahasa. Untuk hasil terbaik, gunakan pemindaian resolusi tinggi dan latar belakang bersih. Anda juga dapat menyesuaikan `ocrEngine.Config` untuk mengaktifkan deskewing atau pengurangan noise.

## Kesimpulan

Anda baru saja mempelajari cara **batch OCR images** di C# menggunakan Aspose.OCR, mulai dari membaca file dari direktori hingga **recognize text from image** dan akhirnya **convert image to text** file yang dapat Anda simpan atau proses lebih lanjut. Contoh lengkap yang dapat dijalankan di atas seharusnya langsung berfungsi, dan bagian tips memberikan panduan untuk memperluas atau menyesuaikan solusi.

Langkah selanjutnya? Coba tambahkan UI sederhana dengan WinForms atau WPF, integrasikan output dengan Azure Cognitive Search, atau bereksperimen dengan bahasa lain yang didukung oleh Aspose.OCR. Langit adalah batasnya setelah Anda menguasai loop inti.

Selamat coding, semoga batch OCR Anda bebas error!  

![Diagram of batch OCR images process](batch-ocr-images-diagram.png "Batch OCR images workflow")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}