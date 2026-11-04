---
category: general
date: 2026-03-05
description: Cara menggunakan OCR di C# untuk mengekstrak teks dari gambar. Pelajari
  cara mengonversi gambar menjadi teks, membaca karakter Korea, dan memuat gambar
  untuk OCR dengan cepat.
draft: false
keywords:
- how to use OCR
- extract text from image
- convert image to text
- read korean characters
- load image for OCR
language: id
og_description: Cara menggunakan OCR di C# dan langsung mengekstrak teks dari gambar.
  Panduan ini menunjukkan cara mengubah gambar menjadi teks, membaca karakter Korea,
  dan memuat gambar untuk OCR.
og_title: Cara Menggunakan OCR di C# – Ekstrak Teks dari Gambar
tags:
- OCR
- C#
- Aspose
title: Cara Menggunakan OCR di C# – Ekstrak Teks dari Gambar
url: /id/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menggunakan OCR di C# – Ekstrak Teks dari Gambar

Pernah bertanya-tanya **cara menggunakan OCR** ketika Anda memiliki screenshot yang penuh dengan teks Korea dan Anda membutuhkan string polos kembali? Anda bukan satu-satunya yang kebingungan tentang ini. Dalam tutorial ini kami akan membahas contoh lengkap yang siap‑jalan yang **mengekstrak teks dari gambar**, **mengonversi gambar menjadi teks**, dan bahkan menunjukkan cara **membaca karakter Korea** dengan Aspose.OCR.

Kami juga akan membahas langkah yang sering terlewatkan yaitu **memuat gambar untuk OCR** sehingga Anda tidak akan mendapatkan kejutan “file tidak ditemukan” nanti. Pada akhir tutorial Anda akan memiliki program mandiri yang dapat Anda masukkan ke dalam proyek .NET mana pun.

## Apa yang Anda Butuhkan

- .NET 6+ (atau .NET Framework 4.7.2 dan yang lebih baru) – kode ini bekerja pada keduanya.
- Aspose.OCR untuk .NET – Anda dapat mengunduh trial gratis dari situs web Aspose.
- Contoh gambar (`korean_doc.png`) yang berisi teks Korea.
- IDE favorit Anda (Visual Studio, Rider, VS Code – apa pun yang Anda suka).

Tidak ada pustaka pihak ketiga lain yang diperlukan.

## Langkah 1: Siapkan Proyek dan Tambahkan Aspose.OCR

First, create a new console app:

```bash
dotnet new console -n OcrDemo
cd OcrDemo
```

Then add the Aspose.OCR NuGet package:

```bash
dotnet add package Aspose.OCR
```

> **Tips pro:** Jika Anda memiliki file lisensi, letakkan di root proyek; jika tidak, trial gratis akan berfungsi tetapi akan menambahkan watermark pada output.

## Langkah 2: Cara Menggunakan OCR – Inisialisasi Engine

Sekarang kita akan menulis kode C#. Hal pertama yang harus dilakukan ketika **cara menggunakan OCR** adalah menginstansiasi `OcrEngine`. Objek ini adalah inti dari pustaka; ia menyimpan semua pengaturan yang akan Anda perlukan nanti.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 2: Initialize the OCR engine
            var ocrEngine = new OcrEngine();

            // Optional: apply your license to remove trial limitations
            // Replace the path with the actual location of your .lic file
            ocrEngine.SetLicense("YOUR_DIRECTORY/Aspose.OCR.lic");
```

**Mengapa ini penting:** Tanpa instance engine yang tepat Anda tidak dapat mengatur bahasa, memuat gambar, atau mengambil hasil. Engine juga mengelola sumber daya internal, sehingga membuatnya sekali dan menggunakannya kembali lebih efisien daripada terus‑menerus membuat objek baru.

## Langkah 3: Pilih Bahasa – Baca Karakter Korea

Baris berikut memberi tahu engine bahasa apa yang harus dicari. Karena tujuan kami adalah **membaca karakter Korea**, kami mengatur `OcrLanguage.Korean`. Anda dapat menggantinya dengan Arabic, Thai, Gujarati, dll., tergantung pada kasus penggunaan Anda.

```csharp
            // Step 3: Tell the engine which language to recognize
            ocrEngine.Language = OcrLanguage.Korean; // alternatives: Arabic, Thai, Gujarati, etc.
```

**Mengapa ini penting:** Pemilihan bahasa secara signifikan meningkatkan akurasi. Engine OCR menggunakan kamus dan model karakter khusus bahasa; memberi bahasa yang salah dapat menghasilkan output yang berantakan.

## Langkah 4: Muat Gambar untuk OCR – Mengonversi Gambar menjadi Teks

Sebelum engine dapat melakukan pekerjaan apa pun, Anda perlu **memuat gambar untuk OCR**. Metode `ImageStream.FromFile` membaca file ke dalam format yang dipahami engine.

```csharp
            // Step 4: Load the image that contains the text
            ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/korean_doc.png");
```

Jika gambar berada di folder yang berbeda, cukup sesuaikan path-nya. Ingat untuk mengatur *Build Action* file menjadi “Copy if newer” agar executable dapat menemukannya saat runtime.

> **Kesalahan umum:** Menyediakan path dengan backslash (`\`) dalam string literal tanpa meng-escape-nya akan menyebabkan error kompilasi. Gunakan double backslash (`\\`) atau string verbatim (`@"C:\path\file.png"`).

## Langkah 5: Lakukan OCR – Ekstrak Teks dari Gambar

Sekarang proses berat terjadi. Memanggil `Recognize()` menjalankan algoritma OCR, dan properti `Text` memberikan Anda string mentah.

```csharp
            // Step 5: Run OCR and get the recognized text
            string recognizedText = ocrEngine.Recognize().Text;
```

Pada titik ini Anda telah **mengekstrak teks dari gambar** dan secara efektif **mengonversi gambar menjadi teks**. Hasilnya mungkin berisi karakter newline jika tata letak asli memiliki pemisah baris.

## Langkah 6: Tampilkan Hasil – Verifikasi Output

Akhirnya, mari cetak hasil ke console sehingga Anda dapat memverifikasi bahwa itu berhasil.

```csharp
            // Step 6: Output the result to the console
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(recognizedText);
        }
    }
}
```

Run the program:

```bash
dotnet run
```

### Output yang Diharapkan

```
=== Recognized Text ===
안녕하세요. 이것은 OCR 테스트 문서입니다.
```

Jika Anda melihat karakter Korea yang mirip dengan gambar, selamat—Anda telah menguasai **cara menggunakan OCR** dengan Aspose.OCR!

![diagram contoh cara menggunakan OCR](image.png)

*Teks alt gambar: diagram contoh cara menggunakan OCR yang menunjukkan alur dari memuat gambar hingga mencetak teks yang dikenali.*

## Kasus Pinggir & Variasi

### 1. Menangani Banyak Halaman

Jika Anda perlu **mengekstrak teks dari gambar** yang berisi beberapa halaman (misalnya, TIFF multi‑halaman), lakukan loop pada setiap halaman dan panggil `Recognize()` untuk setiap instance `ImageStream`.

### 2. Menangani Scan Berkualitas Rendah

Gambar beresolusi rendah dapat menurunkan akurasi. Sebelum memanggil `Recognize()`, Anda dapat memperbaiki gambar dengan alat pra‑pemrosesan Aspose:

```csharp
ocrEngine.Image = ImageProcessing.Preprocess(ocrEngine.Image, ImageProcessingOptions.Deskew);
```

### 3. Mengganti Bahasa Secara Dinamis

Misalkan Anda memiliki dokumen campuran bahasa. Anda dapat mengubah `ocrEngine.Language` di antara proses pengenalan:

```csharp
ocrEngine.Language = OcrLanguage.English;
string english = ocrEngine.Recognize().Text;

ocrEngine.Language = OcrLanguage.Korean;
string korean = ocrEngine.Recognize().Text;
```

### 4. Menyimpan Hasil ke File

Jika Anda lebih suka **mengonversi gambar menjadi teks** dan menyimpannya, cukup tulis string ke file `.txt`:

```csharp
System.IO.File.WriteAllText("output.txt", recognizedText);
```

## Pertanyaan yang Sering Diajukan

- **Apakah saya memerlukan lisensi untuk menjalankan kode ini?**  
  Tidak. Trial gratis berfungsi dengan baik untuk percobaan, tetapi menambahkan watermark pada output. Lisensi yang dibeli menghapus watermark dan membuka kinerja penuh.

- **Apakah saya dapat menggunakan ini di Linux?**  
  Tentu saja. Aspose.OCR bersifat lintas‑platform; pastikan Anda memiliki dependensi native yang diperlukan (libgdiplus untuk .NET Core di Linux).

- **Bagaimana jika gambar saya berada dalam stream bukan file?**  
  Gunakan `ImageStream.FromStream(yourStream)` – API menerima semua `System.IO.Stream`.

## Kesimpulan

Kami telah memandu Anda langkah demi langkah melalui **cara menggunakan OCR** di C# untuk **mengekstrak teks dari gambar**, **mengonversi gambar menjadi teks**, dan **membaca karakter Korea** sambil **memuat gambar untuk OCR** dengan benar. Contoh lengkap yang dapat dijalankan di atas seharusnya berfungsi langsung, dan tips tambahan memberikan panduan untuk skenario yang lebih maju.

Siap untuk tantangan berikutnya? Cobalah mengganti dengan bahasa lain, memproses PDF halaman per halaman, atau mengintegrasikan panggilan OCR ke dalam web API sehingga pengguna dapat mengunggah gambar dan mendapatkan hasil teks secara instan. Kemungkinannya tak terbatas, dan kini Anda memiliki fondasi yang kuat untuk membangunnya.

Selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}