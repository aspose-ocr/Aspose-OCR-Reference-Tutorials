---
category: general
date: 2026-01-04
description: Tutorial OCR C# yang menunjukkan cara mengekstrak teks dari JPEG, melakukan
  OCR pada gambar, dan mengenali teks dari struk menggunakan percepatan GPU.
draft: false
keywords:
- c# OCR tutorial
- extract text from JPEG
- perform OCR on image
- load image for OCR
- recognize text from receipt
language: id
og_description: Tutorial OCR C# memandu Anda memuat gambar untuk OCR, mengekstrak
  teks dari JPEG, dan mengenali teks dari struk dengan dukungan GPU.
og_title: Tutorial OCR c# – Ekstrak Teks dari Gambar JPEG
tags:
- C#
- OCR
- Image Processing
title: Tutorial OCR c# – Ekstrak Teks dari Gambar JPEG
url: /id/net/text-recognition/c-ocr-tutorial-extract-text-from-jpeg-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# OCR tutorial – Ekstrak Teks dari Gambar JPEG

Pernah membutuhkan **c# OCR tutorial** untuk mengambil teks dari struk yang dipindai atau foto dokumen? Anda tidak sendirian. Dalam banyak aplikasi dunia nyata—pelacak pengeluaran, entri data otomatis, atau bahkan alat pencatatan cepat—Anda akan menemukan diri Anda perlu **mengekstrak teks dari JPEG** secara langsung.

Dalam panduan ini kami akan memberi Anda solusi lengkap yang siap dijalankan. Anda akan belajar cara **memuat gambar untuk OCR**, **melakukan OCR pada gambar**, dan akhirnya **mengenali teks dari struk** menggunakan mesin yang dipercepat GPU. Tanpa jalan pintas “lihat dokumen”—hanya kode lengkap, penjelasan mengapa setiap baris penting, dan tips menghindari jebakan umum.

## Apa yang Anda Butuhkan

- .NET 6.0 atau lebih baru (kode menggunakan sintaks C# modern).  
- Sebuah perpustakaan OCR yang menyediakan kelas `OcrEngine` dengan objek `Config`—kebanyakan SDK komersial mengikuti pola ini.  
- GPU yang kompatibel dengan CUDA jika Anda menginginkan percepatan opsional (sebaliknya fallback CPU berfungsi dengan baik).  
- Sebuah contoh gambar JPEG, misalnya `receipt.jpg`, ditempatkan di folder yang dapat Anda referensikan.

Itu saja. Jika Anda sudah memiliki Visual Studio, buka proyek konsol baru dan Anda siap menyalin‑tempel.

![contoh tutorial c# OCR yang menampilkan gambar struk yang diproses](https://example.com/placeholder.jpg "contoh tutorial c# OCR")

*(Teks alternatif: c# OCR tutorial – tangkapan layar mesin OCR memproses gambar struk)*

## Langkah 1 – Buat dan Konfigurasikan OCR Engine (dasar tutorial c# OCR)

Pertama kami menginstansiasi mesin dan mengaktifkan mode GPU. Mengaktifkan GPU dapat mengurangi beberapa detik dari waktu pengenalan untuk batch besar, tetapi bersifat opsional.

```csharp
using System;

// Assume the OCR SDK namespace is OcrSdk
using OcrSdk;

class Program
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Enable GPU acceleration (requires a CUDA‑compatible GPU)
        ocrEngine.Config.EnableGPU = true;   // Turn on GPU mode
        ocrEngine.Config.GpuDeviceId = 0;    // Optional: select GPU index (0 = first GPU)

        // The rest of the steps follow...
```

**Mengapa ini penting:** Mesin menyimpan semua logika berat—model bahasa, pra‑pemrosesan gambar, dan pipeline inferensi. Mengaktifkan `EnableGPU` memberi tahu SDK untuk memindahkan perhitungan tersebut ke kartu grafis, yang sangat membantu saat Anda memproses JPEG beresolusi tinggi atau puluhan struk sekaligus.

## Langkah 2 – Muat Gambar untuk OCR (langkah “load image for OCR”)

Selanjutnya kami menunjuk mesin ke file yang ingin dibaca. Jalur dapat bersifat absolut atau relatif; pastikan file tersebut ada.

```csharp
        // Step 2: Load the image you want to recognize
        // Replace YOUR_DIRECTORY with the actual folder containing receipt.jpg
        string imagePath = @"YOUR_DIRECTORY/receipt.jpg";
        ocrEngine.LoadImage(imagePath);
```

**Tips profesional:** Jika Anda menangani file yang diunggah pengguna, validasi ekstensi dan ukuran sebelum memanggil `LoadImage`. Mesin OCR biasanya mengharapkan bitmap dalam memori, sehingga mengirim JPEG yang rusak akan menimbulkan pengecualian.

## Langkah 3 – Lakukan OCR pada Gambar (aksi inti “perform OCR on image”)

Sekarang mesin melakukan pekerjaan berat. Metode `Recognize` mengembalikan objek `OcrResult` yang berisi output teks polos dan, secara opsional, skor kepercayaan.

```csharp
        // Step 3: Perform the recognition and retrieve the text
        OcrResult ocrResult = ocrEngine.Recognize();
```

**Apa yang terjadi di balik layar?** SDK biasanya menjalankan serangkaian tahap:  
1. **Pra‑pemrosesan** – de‑skewing, binarisasi, penghilangan noise.  
2. **Deteksi baris teks** – menemukan di mana kata‑kata mulai dan berakhir.  
3. **Klasifikasi karakter** – jaringan saraf memprediksi setiap glyph.  

Memahami alur ini membantu Anda memecahkan masalah—jika output terlihat berantakan, periksa kualitas gambar sebelum mengubah pengaturan mesin.

## Langkah 4 – Ekstrak Teks dari JPEG (menampilkan hasil)

Akhirnya kami mencetak string yang dikenali ke konsol. Dalam aplikasi nyata Anda mungkin menyimpannya ke basis data, mengirimnya ke API, atau memasukkannya ke pipeline NLP lain.

```csharp
        // Step 4: Display the recognized text
        Console.WriteLine("Recognized Text:");
        Console.WriteLine(ocrResult.Text);

        // Keep the console window open (useful when running from VS)
        Console.WriteLine("\nPress any key to exit...");
        Console.ReadKey();
    }
}
```

**Output yang diharapkan:**  
Jika `receipt.jpg` berisi struk belanja biasa, Anda akan melihat sesuatu seperti:

```
Recognized Text:
WALMART
123 Main St.
Date: 01/03/2026
Item   Qty   Price
Milk    2    $4.58
Bread   1    $2.99
Total          $7.57
```

Perhatikan bagaimana jeda baris dan spasi dipertahankan—kebanyakan SDK OCR berusaha menjaga tata letak, yang berguna ketika Anda kemudian mem-parsing bidang seperti “Total”.

## Langkah 5 – Kasus Tepi Umum dan Tips (meningkatkan tutorial c# OCR Anda)

- **JPEG beresolusi rendah:** Jika gambar di bawah 300 dpi, pertimbangkan memperbesar dengan filter bikubik sebelum memanggil `LoadImage`.  
- **Banyak bahasa:** Beberapa mesin memungkinkan Anda mengatur `ocrEngine.Config.Language = "en,es";`. Ini berguna ketika struk berisi teks bahasa Inggris dan Spanyol.  
- **Pemrosesan batch:** Bungkus langkah‑langkah dalam loop `foreach` atas daftar jalur file. Ingat untuk menggunakan kembali instance `OcrEngine` yang sama agar tidak menanggung overhead inisialisasi ulang konteks GPU.  
- **Penanganan error:** Bungkus pemanggilan pengenalan dengan `try…catch (OcrException ex)` untuk menangkap masalah seperti “GPU tidak tersedia” atau “format gambar tidak didukung”.  

```csharp
        try
        {
            OcrResult result = ocrEngine.Recognize();
            Console.WriteLine(result.Text);
        }
        catch (OcrException ex)
        {
            Console.Error.WriteLine($"OCR failed: {ex.Message}");
        }
```

## Ringkasan – Apa yang Telah Kita Capai

Anda kini memiliki **c# OCR tutorial** yang memandu Anda melalui setiap fase mengekstrak teks dari struk JPEG: membuat mesin, memuat gambar, melakukan OCR, dan akhirnya mengambil hasil teks polos. Contoh ini menunjukkan cara **melakukan OCR pada gambar** secara efisien dengan percepatan GPU opsional, dan memperlihatkan alur kerja tipikal untuk skenario **mengenali teks dari struk**.

## Langkah Selanjutnya dan Topik Terkait

- **Fine‑tune pra‑pemrosesan** – bereksperimen dengan `ocrEngine.Config.DenoiseLevel` atau binarisasi khusus untuk meningkatkan akurasi pada pemindaian berisik.  
- **Integrasi dengan basis data** – simpan `ocrResult.Text` bersama metadata seperti `imagePath` dan timestamp pemrosesan.  
- **Jelajahi kata kunci sekunder** – coba “extract text from JPEG” dalam konteks layanan web, atau bangun API kecil yang menerima gambar yang diunggah dan mengembalikan teks yang dikenali.  
- **Beralih ke penyedia OCR lain** – kebanyakan SDK komersial menyediakan kelas serupa (`Engine`, `Config`, `Result`), sehingga pola yang Anda pelajari dapat dengan mudah dipindahkan.

Cobalah, ubah pengaturan, dan Anda akan melihat betapa cepatnya OCR dapat menjadi bagian andal dari kotak peralatan C# Anda. Selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}