---
category: general
date: 2026-03-29
description: Ekstrak teks dari gambar dengan Aspose OCR di C#. Pelajari OCR rotasi
  otomatis dan cara mengoreksi kemiringan gambar yang dipindai untuk hasil yang sempurna.
draft: false
keywords:
- extract text from image
- auto rotate ocr
- how to deskew scanned image
- Aspose OCR C#
- image preprocessing OCR
language: id
og_description: Ekstrak teks dari gambar menggunakan Aspose OCR. Panduan ini menunjukkan
  OCR auto‑rotate dan cara mengoreksi kemiringan gambar yang dipindai di C#.
og_title: Ekstrak Teks dari Gambar di C# – OCR Rotasi Otomatis & Perbaikan Kemiringan
tags:
- C#
- OCR
- Aspose
- Image Processing
title: Ekstrak Teks dari Gambar di C# – Panduan OCR Auto‑Rotate & Deskew
url: /id/net/ocr-optimization/extract-text-from-image-in-c-auto-rotate-ocr-deskew-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ekstrak Teks dari Gambar di C# – Panduan Auto‑Rotate OCR & Deskew

Pernahkah Anda perlu **ekstrak teks dari gambar** tetapi file-nya datang dengan sudut yang aneh? Ini adalah masalah umum—terutama ketika Anda menangani faktur yang dipindai, kwitansi yang difoto, atau PDF yang miring. Kabar baiknya, Anda tidak perlu menulis algoritma rotasi khusus sendiri. Dengan menggunakan fitur *auto rotate OCR* bawaan Aspose OCR, Anda dapat membiarkan mesin meluruskan gambar dan kemudian **ekstrak teks dari gambar** dalam satu langkah mulus.  

Dalam tutorial ini kami akan menelusuri program C# lengkap yang siap dijalankan yang:

* Menginisialisasi mesin OCR dengan orientasi otomatis dan deskewing,
* Mengenali gambar yang diputar atau miring,
* Mengembalikan baik sudut rotasi yang terdeteksi maupun teks yang diekstrak.

Tidak ada layanan eksternal, tidak ada matematika rumit—hanya beberapa baris kode dan penjelasan jelas tentang *how to deskew scanned image* bila diperlukan.

## Apa yang Anda Butuhkan

| Prasyarat | Mengapa penting |
|--------------|----------------|
| .NET 6.0 atau lebih baru (atau .NET Framework 4.6+) | Aspose OCR disediakan sebagai paket NuGet yang menargetkan runtime tersebut. |
| Visual Studio 2022 (atau editor C# apa saja) | Memudahkan penambahan paket NuGet dan menjalankan aplikasi console. |
| Contoh gambar (`rotated_document.jpg`) | File harus berupa JPEG, PNG, BMP, atau TIFF yang tidak sepenuhnya tegak. |
| Paket NuGet Aspose.OCR (`Install-Package Aspose.OCR`) | Menyediakan `OcrEngine`, `PreprocessingFilters`, dan tipe terkait. |

Jika Anda sudah mencentang kotak-kotak tersebut, Anda siap melanjutkan. Jika tidak, dapatkan Aspose OCR terbaru dari NuGet—​hanya satu klik untuk menginstal.

---

## Langkah 1 – Inisialisasi Mesin OCR (Kata Kunci Utama dalam Aksi)

Hal pertama yang kami lakukan adalah membuat instance `OcrEngine` dan memberitahukannya untuk **auto rotate OCR** dan **deskew** pada gambar yang masuk. Kedua flag tersebut digabungkan dengan operator OR bitwise (`|`) karena `PreprocessingFilters` adalah enum dengan atribut `[Flags]`.

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // Initialise the OCR engine with English language and preprocessing options
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = Language.English,
            // Enable both auto‑rotate and auto‑deskew
            Preprocessing = PreprocessingFilters.AutoRotate | PreprocessingFilters.AutoDeskew
        };
```

> **Mengapa ini penting:**  
> *Auto‑rotate OCR* memeriksa baseline teks pada gambar, menebak orientasi yang benar, dan memutar secara internal sebelum pengenalan. *Auto‑deskew* melakukan hal yang sama untuk kemiringan ringan yang sering muncul pada dokumen yang dipindai. Dengan mengaktifkan keduanya, Anda menjamin hasil **ekstrak teks dari gambar** yang terbaik tanpa penyuntingan gambar manual.

---

## Langkah 2 – Kenali Gambar dan Dapatkan Hasil

Sekarang kami memberikan mesin sebuah jalur file. Metode `RecognizeImage` mengembalikan objek `OcrResult` yang berisi sudut rotasi yang terdeteksi, skor kepercayaan, dan output teks polos.

```csharp
        // Recognise the image file and obtain the OCR result
        OcrResult ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/rotated_document.jpg");
```

> **Tip:** Jika Anda bekerja dengan stream (misalnya, file yang diunggah), gunakan `ocrEngine.RecognizeImage(Stream)` sebagai gantinya. Flag preprocessing yang sama tetap berlaku, sehingga Anda tetap mendapatkan manfaat **auto rotate OCR**.

---

## Langkah 3 – Tampilkan Sudut Rotasi dan Teks yang Diekstrak

Akhirnya, kami mencetak dua informasi ke konsol: sudut yang menurut mesin gambar perlu diputar, dan teks sebenarnya yang diambil.

```csharp
        // Show the detected rotation and the recognised text
        Console.WriteLine($"Detected rotation: {ocrResult.RotationAngle}°");
        Console.WriteLine("----- Extracted Text -----");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Output yang diharapkan** (angka Anda akan berbeda tergantung pada gambar input):

```
Detected rotation: 12.3°
----- Extracted Text -----
Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
Thank you for your business!
```

Jika gambar sudah tegak, sudut rotasi akan menjadi `0°`, dan Anda tetap akan mendapatkan teks bersih berkat algoritma *auto‑deskew*.

---

## Langkah 4 – Memahami Cara Deskew Gambar yang Dipindai (Pendalaman Kata Kunci Sekunder)

Anda mungkin bertanya-tanya *how to deskew scanned image* ketika mesin OCR melaporkan rotasi non‑nol. Di balik layar, Aspose OCR menerapkan **Hough transform** untuk mendeteksi orientasi garis teks dominan. Kemudian ia memutar bitmap dengan kebalikan dari sudut tersebut, secara efektif meluruskan teks.

**Kapan ini penting?**  

* Pemindai yang mengumpankan kertas dengan sudut sedikit (umum di lingkungan kantor).  
* Foto smartphone yang diambil secara manual—​horizon jarang sempurna.  

**Penanganan kasus tepi:**  

Jika `RotationAngle` pada hasilnya sangat besar (mis., > 45°), mesin mungkin salah menafsirkan gambar (mungkin itu logo atau grafik non‑teks). Dalam kasus itu Anda dapat:

1. Memutar gambar secara manual menggunakan `System.Drawing` sebelum memberikannya ke mesin, atau  
2. Menonaktifkan `AutoRotate` dan hanya mempertahankan `AutoDeskew` jika Anda tahu dokumen sudah tegak.

```csharp
// Example: manually rotate 90° clockwise before OCR
using (var img = Aspose.OCR.Image.Load("rotated_document.jpg"))
{
    img.Rotate(90);
    OcrResult result = ocrEngine.RecognizeImage(img);
    Console.WriteLine(result.Text);
}
```

---

## Langkah 5 – Kesalahan Umum & Tips Pro (E‑E‑A‑T dalam Aksi)

| Jebakan | Mengapa terjadi | Perbaikan |
|---------|----------------|-----|
| **Gambar buram atau beresolusi rendah** | Akurasi OCR turun drastis; deteksi rotasi dapat gagal. | Gunakan pemindaian setidaknya 300 dpi; terapkan filter penajaman sebelum OCR. |
| **Bahasa campuran** | Mesin default ke Bahasa Inggris; karakter asing menjadi rusak. | Set `Language = Language.English | Language.Spanish` (atau kombinasi yang sesuai). |
| **File besar (> 10 MB)** | Tekanan memori dapat menyebabkan `OutOfMemoryException`. | Turunkan resolusi gambar terlebih dahulu, atau proses dalam ubin menggunakan `OcrEngine.RecognizeRegion`. |
| **Jalur file tidak tepat** | `FileNotFoundException` menghentikan program. | Gunakan `Path.Combine(Environment.CurrentDirectory, "rotated_document.jpg")` untuk ketahanan. |

> **Tip pro:** Selalu catat `ocrResult.RotationAngle` dan `ocrResult.Confidence` (jika tersedia). Metri­k tersebut membantu Anda memutuskan apakah percobaan ulang dengan pengaturan preprocessing yang berbeda layak dilakukan.

---

## Langkah 6 – Memperluas Contoh (Apa Selanjutnya?)

Sekarang Anda dapat **ekstrak teks dari gambar** dengan auto‑rotation dan deskewing, pertimbangkan langkah selanjutnya berikut:

* **Pemrosesan batch** – Loop melalui folder gambar, simpan setiap hasil ke basis data, dan beri tanda pada yang memiliki `RotationAngle > 5°` untuk tinjauan manual.  
* **Konversi PDF** – Gabungkan teks yang diekstrak dengan gambar asli menjadi PDF yang dapat dicari menggunakan Aspose.PDF.  
* **Deteksi bahasa** – Gunakan flag `AutoDetectLanguage` dari Aspose.OCR untuk membiarkan mesin memilih bahasa terbaik secara otomatis.  

Setiap hal ini dibangun di atas prinsip inti yang sama: biarkan pustaka menangani orientasi, dan Anda fokus pada logika bisnis.

---

## Contoh Lengkap yang Berfungsi (Siap Salin‑Tempel)

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialise the OCR engine with auto‑rotate and auto‑deskew
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = Language.English,
            Preprocessing = PreprocessingFilters.AutoRotate | PreprocessingFilters.AutoDeskew
        };

        // 2️⃣ Recognise the image – replace the path with your own file
        string imagePath = "YOUR_DIRECTORY/rotated_document.jpg";
        OcrResult ocrResult = ocrEngine.RecognizeImage(imagePath);

        // 3️⃣ Output the rotation angle and the recognised text
        Console.WriteLine($"Detected rotation: {ocrResult.RotationAngle}°");
        Console.WriteLine("----- Extracted Text -----");
        Console.WriteLine(ocrResult.Text);
    }
}
```

Simpan file sebagai `Program.cs`, jalankan `dotnet add package Aspose.OCR`, lalu `dotnet run`. Anda akan melihat sudut dan teks bersih tercetak di konsol.

---

## Kesimpulan

Kami baru saja mendemonstrasikan cara **ekstrak teks dari gambar** di C# sambil membiarkan Aspose OCR menangani *auto rotate OCR* dan masalah rumit *how to deskew scanned image*. Dengan mengaktifkan dua flag preprocessing, mesin secara otomatis meluruskan gambar yang miring, mendeteksi orientasi yang benar, dan menghasilkan teks yang akurat—tanpa penyuntingan gambar manual.

Silakan bereksperimen dengan batch yang lebih besar, bahasa yang berbeda, atau bahkan mengintegrasikan output ke PDF yang dapat dicari. Langit adalah batasnya setelah mesin OCR menangani pekerjaan berat untuk Anda.

**Siap meningkatkan alur dokumen Anda?** Ambil kode, arahkan ke pemindaian Anda sendiri, dan saksikan sudut rotasi menghilang. Jika Anda mengalami kendala, tinggalkan komentar di bawah—selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}