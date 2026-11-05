---
category: general
date: 2026-04-06
description: Cara menggunakan OCR di C# untuk mengekstrak teks biasa dari gambar JPG,
  termasuk karakter Cyrillic. Pelajari cara memuat gambar untuk OCR, mengenali teks
  JPG, dan mendapatkan hasil yang dapat diandalkan.
draft: false
keywords:
- how to use OCR
- extract plain text
- extract cyrillic text
- recognize text jpg
- load image for OCR
language: id
og_description: Cara menggunakan OCR di C# untuk mengekstrak teks biasa dari file
  JPG. Panduan ini menunjukkan cara memuat gambar untuk OCR, mengenali teks JPG, dan
  menangani teks Cyrillic.
og_title: Cara Menggunakan OCR di C# – Ekstrak Teks Biasa dari Gambar
tags:
- C#
- OCR
- Aspose
- Image Processing
title: Cara Menggunakan OCR di C# – Ekstrak Teks Polos dari Gambar
url: /id/net/text-recognition/how-to-use-ocr-in-c-extract-plain-text-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menggunakan OCR di C# – Mengekstrak Teks Biasa dari Gambar

Pernah bertanya-tanya **cara menggunakan OCR** dalam proyek .NET tanpa harus berurusan dengan pustaka native? Mungkin Anda memiliki folder berisi kuitansi yang dipindai, beberapa tangkapan layar dengan keterangan Cyrillic, atau hanya perlu mengambil teks dari sebuah JPEG untuk analisis cepat. Kabar baiknya, Aspose OCR membuat seluruh proses itu menjadi sangat mudah.

Dalam tutorial ini kami akan menelusuri contoh lengkap yang dapat dijalankan yang menunjukkan **cara menggunakan OCR** untuk **mengekstrak teks biasa** dari gambar JPEG, cara **memuat gambar untuk OCR**, dan bahkan cara **mengekstrak teks Cyrillic** ketika bahasa sumber bukan Latin. Pada akhir tutorial Anda akan memiliki aplikasi konsol kecil yang mencetak teks yang dikenali langsung ke konsol—tanpa file tambahan, tanpa efek samping yang misterius.

> **Apa yang akan Anda dapatkan**  
> * Panduan langkah‑demi‑langkah yang dapat Anda salin‑tempel ke Visual Studio.  
> * Penjelasan *mengapa* setiap baris penting, bukan hanya *apa* yang dilakukannya.  
> * Tips untuk menangani gambar besar, banyak bahasa, dan jebakan umum.

## Prasyarat

Sebelum kita mulai, pastikan Anda memiliki:

* .NET 6 SDK atau yang lebih baru (kode ini juga bekerja dengan .NET Core dan .NET Framework).  
* Visual Studio 2022 (atau editor apa pun yang Anda sukai).  
* Akses internet pada kali pertama Anda menjalankan contoh—Aspose OCR mengunduh paket bahasa sesuai permintaan.  

Jika Anda belum memiliki paket NuGet Aspose OCR, kami akan membahasnya pada langkah pertama.

## Langkah 1 – Instal Aspose OCR via NuGet (dan mengapa itu penting)

Langkah **memuat gambar untuk OCR** tidak dapat terjadi sampai pustaka tersedia. Menggunakan NuGet menjamin Anda mendapatkan binary terbaru yang telah dipatch keamanannya dan secara otomatis menarik semua dependensi yang diperlukan.

```bash
dotnet add package Aspose.OCR
```

*Mengapa ini penting*: Aspose OCR menyediakan satu DLL inti yang sangat kecil dan hanya menarik data bahasa ketika Anda memintanya. Hal ini membuat aplikasi Anda ringan dan menghindari penyertaan megabyte file bahasa yang tidak terpakai.

## Langkah 2 – Inisialisasi OCR Engine (inti dari **cara menggunakan OCR**)

Membuat instance `OcrEngine` adalah baris kode pertama yang benar‑benar penting untuk **cara menggunakan OCR**. Engine secara default berada dalam mode “on‑demand”, artinya ia akan mengunduh paket bahasa pada kali pertama Anda meminta bahasa tertentu.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// Step 2: Create the engine – it will fetch language data when needed.
var ocrEngine = new OcrEngine();
```

> **Pro tip**: Jika Anda berada di belakang proxy perusahaan, atur `OcrEngine.Proxy` sebelum panggilan pengenalan pertama agar unduhan berhasil.

## Langkah 3 – Pilih Bahasa – **Ekstrak Teks Cyrillic** bila diperlukan

Aspose OCR mendukung puluhan skrip. Untuk **mengekstrak teks Cyrillic**, cukup set properti `Language` ke `OcrLanguage.Cyrillic`. Pada kali pertama baris ini dijalankan, modul Cyrillic (≈ 5 MB) diunduh dari CDN Aspose.

```csharp
// Step 3: Tell the engine which language to look for.
// This will automatically download the Cyrillic language pack on first use.
ocrEngine.Language = OcrLanguage.Cyrillic;
```

Jika gambar Anda hanya berisi karakter Latin, Anda dapat mengganti `Cyrillic` dengan `English`. Pola yang sama berlaku untuk bahasa lain yang didukung.

## Langkah 4 – **Muat Gambar untuk OCR** – Dari Disk atau Stream

Sekarang kita benar‑benar **memuat gambar untuk OCR**. Kelas `System.Drawing.Image` menangani kebanyakan format umum (JPG, PNG, BMP). Jika Anda berada di platform non‑Windows, pertimbangkan menggunakan `ImageSharp` sebagai gantinya, tetapi untuk tutorial ini tipe bawaan sudah cukup.

```csharp
using System.Drawing;

// Step 4: Load the picture that holds the text.
using var image = Image.FromFile(@"C:\Images\cyrillic_sample.jpg");
```

> **Mengapa ini penting**: Memuat gambar di dalam blok `using` menjamin sumber daya GDI+ yang tidak dikelola dilepaskan segera, mencegah kebocoran memori pada layanan yang berjalan lama.

## Langkah 5 – **Kenali Teks JPG** – Jalankan Proses OCR

Dengan engine yang sudah dikonfigurasi dan gambar yang sudah dimuat, kita akhirnya **mengenali teks jpg**. Metode `Recognize` mengembalikan `OcrResult` yang berisi string biasa, skor kepercayaan, dan bahkan kotak pembatas jika Anda membutuhkannya nanti.

```csharp
// Step 5: Perform the recognition.
var ocrResult = ocrEngine.Recognize(image);
```

Jika Anda ingin menyesuaikan akurasi, Anda dapat mengubah `ocrEngine.Config` (misalnya, mengaktifkan `AutoRotate` atau mengatur `TextOrientation`). Untuk kebanyakan skenario sederhana, nilai default sudah bekerja dengan sangat baik.

## Langkah 6 – **Ekstrak Teks Biasa** – Tampilkan Hasil

Bagian akhir dari **cara menggunakan OCR** adalah mengambil string yang dikenali dari `ocrResult` dan melakukan sesuatu dengannya. Di sini kami cukup menuliskannya ke konsol, yang juga memperlihatkan cara **mengekstrak teks biasa** dari objek hasil.

```csharp
// Step 6: Output the plain text to the console.
Console.WriteLine("=== Recognized Text ===");
Console.WriteLine(ocrResult.Text);
```

### Output yang Diharapkan

Jika `cyrillic_sample.jpg` berisi frasa “Привет мир” (Hello world), Anda akan melihat:

```
=== Recognized Text ===
Привет мир
```

Jika gambar buram atau teks terlalu kecil, output mungkin mengandung kesalahan; Anda dapat memeriksa `ocrResult.Confidence` untuk memutuskan apakah perlu mencoba lagi dengan sumber beresolusi lebih tinggi.

## Contoh Lengkap yang Siap‑Jalankan

Berikut adalah program lengkapnya. Salin ke proyek Console App baru (`dotnet new console`) dan jalankan. Tidak ada file tambahan yang diperlukan selain gambar yang Anda tunjuk.

```csharp
// ---------------------------------------------------------------
// How to Use OCR in C# – Complete Example
// ---------------------------------------------------------------
using System;
using System.Drawing;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // 1️⃣ Install Aspose.OCR via NuGet first (dotnet add package Aspose.OCR)

        // 2️⃣ Initialize the OCR engine – on‑demand language download.
        var ocrEngine = new OcrEngine();

        // 3️⃣ Select Cyrillic to **extract Cyrillic text**.
        ocrEngine.Language = OcrLanguage.Cyrillic;

        // 4️⃣ **Load image for OCR** – change the path to your own file.
        using var image = Image.FromFile(@"YOUR_DIRECTORY\cyrillic_sample.jpg");

        // 5️⃣ **Recognize text jpg** – run the engine.
        var ocrResult = ocrEngine.Recognize(image);

        // 6️⃣ **Extract plain text** – display it.
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

> **Catatan**: Ganti `YOUR_DIRECTORY\cyrillic_sample.jpg` dengan jalur sebenarnya ke file JPEG Anda.

## Pertanyaan Umum & Kasus Tepi

### Bagaimana jika saya perlu **mengenali teks jpg** dari stream alih‑alih file?

Anda dapat langsung memberi `MemoryStream`:

```csharp
using var ms = new MemoryStream(File.ReadAllBytes("myImage.jpg"));
using var img = Image.FromStream(ms);
var result = ocrEngine.Recognize(img);
```

### Bagaimana cara menangani banyak bahasa dalam satu gambar?

Setel `ocrEngine.Language` ke `OcrLanguage.Multilingual`. Engine akan berusaha mendeteksi setiap skrip secara otomatis, yang berguna ketika kuitansi mencampur bahasa Inggris dan Cyrillic.

```csharp
ocrEngine.Language = OcrLanguage.Multilingual;
```

### Gambar saya sangat besar (lebih dari 5 MP). Apakah engine akan kesulitan?

Gambar besar meningkatkan penggunaan memori dan dapat memperlambat proses pengenalan. Mengubah ukuran terlebih dahulu secara cepat membantu:

```csharp
var resized = new Bitmap(image, new Size(image.Width / 2, image.Height / 2));
var result = ocrEngine.Recognize(resized);
```

### Bisakah saya mendapatkan skor kepercayaan untuk setiap baris?

Ya—`ocrResult.Lines` berisi properti `Confidence` per baris. Mengiterasi mereka memungkinkan Anda menyaring hasil dengan kepercayaan rendah.

```csharp
foreach (var line in ocrResult.Lines)
{
    if (line.Confidence > 0.8)
        Console.WriteLine(line.Text);
}
```

## Tips Pro untuk OCR Siap Produksi

* **Cache paket bahasa** – unduhan pertama dapat memakan beberapa detik; simpan file‑file tersebut di folder yang diketahui dan set `ocrEngine.LanguageDataPath` untuk menggunakan kembali.  
* **Pemrosesan batch** – gunakan satu instance `OcrEngine` untuk banyak gambar; membuat engine baru untuk tiap file menambah beban yang tidak perlu.  
* **Penanganan error** – bungkus pemanggilan `Recognize` dalam blok try/catch. Aspose melempar `OcrException` untuk gambar rusak atau format yang tidak didukung.  
* **Logging** – catat `ocrResult.Confidence` sehingga Anda dapat meninjau nanti halaman‑halaman mana yang memerlukan peninjauan manual.

## Kesimpulan

Kami baru saja membahas **cara menggunakan OCR** di C# untuk **mengekstrak teks biasa** dari JPEG, menunjukkan langkah‑langkah **memuat gambar untuk OCR**, memperlihatkan cara **mengenali teks jpg**, dan bahkan mengekstrak **teks Cyrillic** dari gambar. Contoh ini sepenuhnya fungsional, hanya memerlukan satu paket NuGet, dan dapat diperluas untuk menangani dokumen multibahasa, pekerjaan batch, atau skenario pemindaian waktu nyata.

Siap untuk tantangan berikutnya? Coba ganti bahasa Cyrillic dengan Arab, eksperimen dengan flag `AutoRotate`, atau integrasikan output ke dalam indeks pencarian. Kemungkinannya tidak terbatas.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}