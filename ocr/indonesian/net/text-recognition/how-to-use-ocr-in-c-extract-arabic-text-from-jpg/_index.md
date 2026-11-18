---
category: general
date: 2026-03-21
description: Cara menggunakan OCR di C# untuk mengenali teks dari file gambar. Pelajari
  cara mengekstrak teks Arab dari JPG dan mengubahnya menjadi teks biasa.
draft: false
keywords:
- how to use OCR
- extract arabic text
- recognize text from image
- image to text c#
- convert jpg to text
language: id
og_description: Cara menggunakan OCR di C# untuk mengenali teks dari file gambar.
  Panduan ini menunjukkan cara mengekstrak teks Arab dari file JPG dan mengubahnya
  menjadi teks yang dapat diedit.
og_title: Cara Menggunakan OCR di C# – Ekstrak Teks Arab dari JPG
tags:
- OCR
- C#
- Aspose
- Arabic
title: Cara Menggunakan OCR di C# – Ekstrak Teks Arab dari JPG
url: /id/net/text-recognition/how-to-use-ocr-in-c-extract-arabic-text-from-jpg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menggunakan OCR di C# – Ekstrak Teks Arab dari JPG

Pernah bertanya-tanya **bagaimana cara menggunakan OCR** ketika Anda memiliki gambar teks Arab yang tersimpan di hard drive Anda? Anda bukan satu-satunya. Banyak pengembang mengalami hal yang sama: mereka memiliki file JPEG, mereka membutuhkan kata‑kata di dalamnya, dan mereka tidak ingin menulis kode jaringan saraf dari nol.  

Berita baik? Dengan beberapa baris C# Anda dapat **mengenali teks dari gambar** file, mengambil setiap karakter Arab, dan menghasilkan string bersih yang dapat Anda simpan, cari, atau tampilkan. Dalam tutorial ini kami akan membahas seluruh proses—menginstal pustaka, mengonfigurasi model bahasa, menjalankan pemindaian, dan akhirnya mencetak hasilnya. Pada akhir Anda akan dapat **mengonversi JPG ke teks** dalam hitungan detik.

## Apa yang Akan Anda Pelajari

- Instal paket NuGet Aspose.OCR untuk .NET.
- Inisialisasi mesin OCR dalam mode CPU (sempurna untuk pekerjaan kecil).
- Muat model bahasa Arab secara otomatis.
- Jalankan OCR pada gambar JPEG dan ambil teks yang dikenali.
- Tangani jebakan umum seperti file besar atau data bahasa yang hilang.

Tidak diperlukan pengalaman sebelumnya dengan OCR; cukup pemahaman dasar tentang C# dan Visual Studio saja. Siap? Mari kita mulai.

## Instal Aspose OCR untuk .NET

Sebelum kode apa pun dijalankan Anda memerlukan pustaka Aspose.OCR. Pustaka ini tersedia sebagai paket NuGet, jadi instalasinya hanya satu perintah:

```bash
dotnet add package Aspose.OCR
```

Atau, jika Anda lebih suka UI Visual Studio, buka **Tools → NuGet Package Manager → Manage NuGet Packages for Solution**, cari **Aspose.OCR**, dan klik **Install**. Paket ini mengunduh semua yang Anda perlukan, termasuk file data bahasa yang akan diunduh mesin pada penggunaan pertama.

> **Pro tip:** Pastikan proyek Anda menargetkan .NET 6 atau lebih baru; kerangka kerja yang lebih lama masih berfungsi tetapi Anda akan kehilangan peningkatan kinerja.

## Inisialisasi Mesin OCR

Sekarang pustaka sudah tersedia, kita dapat membuat instance `OcrEngine`. Untuk kebanyakan tugas skala kecil mode CPU default sudah lebih dari cukup—ia menggunakan prosesor host dan menghindari konfigurasi tambahan yang diperlukan untuk akselerasi GPU.

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;

// Initialise the OCR engine (CPU mode is sufficient for small jobs)
var ocrEngine = new OcrEngine();
```

Mengapa membuat mesin baru setiap kali? Objek `OcrEngine` menyimpan konfigurasi seperti bahasa, DPI, dan format output. Dengan membatasinya pada satu operasi Anda menjamin keadaan bersih dan menghindari tumpang tindih tidak sengaja antara model bahasa yang berbeda.

## Muat Model Bahasa Arab

Aspose menyediakan paket bahasa sesuai permintaan. Kali pertama Anda menetapkan `Language.Arabic` pustaka akan mengunduh sekitar 30 MB data ke folder cache di mesin Anda. Unduhan satu kali ini membuat eksekusi berikutnya sangat cepat.

```csharp
// Choose the language model to load.
// The first assignment triggers an automatic download of the language data (~30 MB).
ocrEngine.Settings.Language = Language.Arabic;
```

Jika Anda perlu mendukung skrip tambahan (misalnya, Inggris atau Hindi), cukup ubah nilai enum—tidak diperlukan kode tambahan. Mesin akan menyimpan cache setiap bahasa secara terpisah.

## Jalankan OCR pada Gambar JPG

Dengan mesin siap dan model Arab dimuat, arahkan ke gambar yang ingin Anda proses. Path dapat berupa absolut atau relatif; pastikan file ada dan dapat dibaca.

```csharp
// Run OCR on the input image.
var recognitionResult = ocrEngine.Recognize(@"YOUR_DIRECTORY/arabic_doc.jpg");
```

**Kasus khusus:** Jika JPEG Anda sangat besar (lebih dari 5 MB) Anda mungkin ingin memperkecilnya terlebih dahulu. Gambar besar meningkatkan penggunaan memori dan dapat memperlambat pengenalan. Pra‑ukuran cepat menggunakan `System.Drawing` atau `ImageSharp` dapat memotong waktu pemrosesan secara signifikan.

## Ambil dan Tampilkan Teks yang Dikenali

Metode `Recognize` mengembalikan objek `OcrResult`. Properti `Text`-nya berisi representasi teks biasa dari semua yang dapat dibaca mesin.

```csharp
// Retrieve the recognised text and output it.
string extractedText = recognitionResult.Text;
Console.WriteLine(extractedText);
```

Saat Anda menjalankan program, Anda akan melihat karakter Arab dicetak ke konsol, mempertahankan urutan dan baris asli. Jika Anda membutuhkan teks dalam file, cukup tulis dengan `File.WriteAllText`.

### Contoh Lengkap yang Berfungsi

Menggabungkan semuanya, berikut contoh aplikasi konsol lengkap yang siap dijalankan:

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialise the OCR engine (CPU mode works fine for most cases)
        var ocrEngine = new OcrEngine();

        // 2️⃣ Load the Arabic language pack – triggers a one‑time download (~30 MB)
        ocrEngine.Settings.Language = Language.Arabic;

        // 3️⃣ Specify the image path – replace with your actual file location
        string imagePath = @"YOUR_DIRECTORY/arabic_doc.jpg";

        // 4️⃣ Run OCR and capture the result
        var result = ocrEngine.Recognize(imagePath);

        // 5️⃣ Extract the text and display it
        string extractedText = result.Text;
        Console.WriteLine("=== Extracted Arabic Text ===");
        Console.WriteLine(extractedText);
    }
}
```

**Output yang diharapkan (contoh):**

```
=== Extracted Arabic Text ===
هذا نص تجريبي باللغة العربية
تم استخراج هذا النص بنجاح
```

Jika output terlihat berantakan, periksa kembali bahwa gambar jelas dan bahasa telah diatur ke `Arabic`. Pemindaian yang buram atau halaman yang diputar adalah alasan umum mengapa OCR dapat gagal.

## Pertanyaan Umum & Tips

- **Bagaimana jika gambar berisi Arab dan Inggris?**  
  Set `ocrEngine.Settings.Language = Language.Multilingual;` untuk membiarkan Aspose mendeteksi beberapa skrip secara otomatis.

- **Bisakah saya mempercepat pemrosesan dengan GPU?**  
  Ya—ganti mesin default dengan `new OcrEngine(OcrEngineMode.Gpu)` jika Anda memiliki kartu grafis yang kompatibel dan runtime CUDA terpasang.

- **Bagaimana cara menangani rendering kanan‑ke‑kiri di UI?**  
  String mentahnya adalah Unicode; sebagian besar kerangka kerja UI modern (WinForms, WPF, ASP.NET) mendukung tata letak RTL secara otomatis ketika Anda mengatur `FlowDirection` yang sesuai.

- **Apakah ada batas ukuran gambar?**  
  Secara teknis tidak, tetapi konsumsi memori meningkat seiring resolusi. Untuk pemindaian besar (mis., buku yang dipindai), pertimbangkan memproses satu halaman pada satu waktu.

## Gambaran Visual

Di bawah ini diagram sederhana yang menggambarkan alur dari file gambar ke teks yang diekstrak.  

![How to use OCR flow diagram – image to text conversion](/images/ocr-flow.png)

*Alt text:* *Diagram alur cara menggunakan OCR yang menunjukkan konversi gambar ke teks dalam C#.*

## Langkah Selanjutnya

Sekarang Anda telah menguasai **cara menggunakan OCR** untuk JPEG Arab, Anda dapat memperluas solusi:

- **Pemrosesan batch:** Loop melalui folder gambar dan tulis setiap hasil ke file `.txt` terpisah.
- **Pasca‑pemrosesan:** Gunakan ekspresi reguler untuk membersihkan tanda baca atau baris yang tidak diinginkan.
- **Integrasi:** Masukkan string yang diekstrak ke dalam indeks pencarian (mis., Azure Cognitive Search) untuk pencarian full‑text pada dokumen yang dipindai.

Jika Anda penasaran dengan bahasa lain, cukup ganti nilai enum `Language`. Ingin mengekstrak tabel atau catatan tulisan tangan? Aspose.OCR juga menawarkan fitur `LayoutAnalysis` yang dapat memsegmentasi blok sebelum pengenalan.

---

### TL;DR

Anda sekarang tahu **cara menggunakan OCR** di C# untuk **mengekstrak teks Arab** dari JPEG, secara efektif **mengenali teks dari gambar** file dan **mengonversi JPG ke teks**. Contoh lengkap yang dapat dijalankan di atas menunjukkan setiap langkah, mulai dari menginstal paket NuGet hingga mencetak string akhir. Ambil gambar contoh, tempelkan kode, dan saksikan keajaibannya—tanpa layanan eksternal diperlukan. Selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}