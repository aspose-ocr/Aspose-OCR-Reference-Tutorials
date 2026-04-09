---
category: general
date: 2026-04-08
description: Ekstrak teks dari gambar menggunakan Aspose OCR dalam C#. Pelajari cara
  mempraproses gambar untuk OCR dan cara mempraproses gambar untuk meningkatkan akurasi.
draft: false
keywords:
- extract text from image
- preprocess image for ocr
- how to preprocess image
- Aspose OCR C#
- image preprocessing techniques
language: id
og_description: Ekstrak teks dari gambar menggunakan Aspose OCR di C#. Panduan ini
  menunjukkan cara menyiapkan gambar untuk OCR dan cara menyiapkan gambar untuk hasil
  terbaik.
og_title: Ekstrak Teks dari Gambar dengan Aspose OCR – Panduan Lengkap C#
tags:
- C#
- OCR
- Aspose
- Image Processing
title: Ekstrak Teks dari Gambar dengan Aspose OCR – Panduan Lengkap C#
url: /id/net/ocr-optimization/extract-text-from-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ekstrak Teks dari Gambar dengan Aspose OCR – Panduan Lengkap C#

Pernah membutuhkan untuk **ekstrak teks dari gambar** tetapi hasilnya penuh dengan kesalahan? Anda tidak sendirian—banyak pengembang mengalami hal yang sama ketika gambar sumber miring, berisik, atau kontras rendah. Kabar baiknya, rutinitas pra‑pemrosesan singkat dapat mengubah foto yang goyah menjadi sumber bersih untuk OCR, dan Aspose OCR membuat semuanya menjadi mudah.

Dalam tutorial ini kami akan menelusuri contoh dunia nyata yang menunjukkan **cara memproses gambar untuk OCR** menggunakan filter bawaan Aspose OCR, kemudian benar‑benarnya **ekstrak teks dari gambar** dengan hanya beberapa baris C#. Pada akhir Anda akan memiliki program siap‑jalankan, memahami mengapa setiap filter penting, dan tahu cara menyesuaikan pipeline untuk kasus tepi Anda sendiri.

## Apa yang Anda Butuhkan

- .NET 6.0 atau lebih baru (kode juga dapat dijalankan pada .NET Framework 4.7+)
- Paket NuGet Aspose.OCR (`Install-Package Aspose.OCR`)
- Contoh gambar yang miring, berisik, atau kontras rendah (misalnya `skewed_noisy.jpg`)
- IDE apa saja yang Anda suka—Visual Studio, Rider, atau VS Code sudah cukup

Tidak ada pustaka native tambahan, tidak ada layanan web, hanya C# biasa.

## Langkah 1: Siapkan Mesin OCR – Titik Awal untuk Mengekstrak Teks

Hal pertama yang harus dilakukan: buat instance `OcrEngine` dan beri tahu bahasa yang akan dicari. Bahasa Inggris paling umum, tetapi Anda dapat mengganti `"en"` dengan `"fr"`, `"de"` dan sebagainya.

```csharp
using Aspose.Ocr;
using Aspose.Ocr.Filters;
using System;

public static class ImageOcrDemo
{
    public static void PreprocessAndOcr()
    {
        // 1️⃣ Initialize the OCR engine – this is where we define the language.
        var ocrEngine = new OcrEngine { Language = "en" };
```

**Mengapa ini penting:** Mesin menyimpan kamus internal dan heuristik khusus bahasa. Jika Anda melewatkan pengaturan bahasa, Aspose secara default menggunakan bahasa Inggris, tetapi menyatakannya secara eksplisit menghindari kejutan saat Anda beralih ke locale lain.

## Langkah 2: Bangun Pipeline Pra‑Pemrosesan – Cara Memproses Gambar untuk Hasil Terbaik

Sekarang kita menambahkan filter. Anggaplah mereka sebagai suite pengeditan foto mini yang berjalan otomatis sebelum langkah OCR. Tiga filter di bawah ini mencakup masalah paling umum:

| Filter | Apa yang diperbaiki | Kapan digunakan |
|--------|---------------------|-----------------|
| `DeskewFilter` | Memutar gambar kembali ke horizontal | Gambar yang diambil dengan sudut |
| `DenoiseFilter` | Mengurangi bintik‑bintik acak dan grain | Foto cahaya rendah atau dokumen yang dipindai |
| `ContrastStretchFilter` | Meningkatkan kontras, membuat teks gelap menonjol | Cetakan pudar atau screenshot yang terlalu terang |

```csharp
        // 2️⃣ Add preprocessing steps – this is the core of “how to preprocess image”.
        ocrEngine.Preprocess.Add(new DeskewFilter());               // correct skew
        ocrEngine.Preprocess.Add(new DenoiseFilter());             // reduce noise
        ocrEngine.Preprocess.Add(new ContrastStretchFilter());     // enhance contrast
```

**Pro tip:** Urutan penting. Deskew dulu, kemudian denoise, dan terakhir stretch contrast. Jika Anda membalik urutannya, Anda mungkin memperkuat noise alih‑alih menghilangkannya.

## Langkah 3: Jalankan OCR – Akhirnya Ekstrak Teks dari Gambar

Dengan pipeline siap, serahkan path gambar ke mesin. Aspose secara otomatis akan menerapkan filter, lalu menjalankan algoritma pengenalan.

```csharp
        // 3️⃣ Recognize text from the pre‑processed image.
        var ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/skewed_noisy.jpg");
```

Jika file tidak ditemukan, Anda akan menerima `FileNotFoundException` yang jelas. Itulah mengapa kami menyarankan menggunakan path absolut selama pengembangan, kemudian beralih ke path relatif atau nilai konfigurasi untuk produksi.

## Langkah 4: Tampilkan Hasil – Lihat Apa yang Didapat

Objek `OcrResult` berisi teks mentah, skor kepercayaan, dan bahkan bounding box setiap kata. Untuk demo cepat kami hanya akan mencetak teks ke konsol.

```csharp
        // 4️⃣ Output the extracted text.
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

Saat Anda menjalankan program, Anda seharusnya melihat sesuatu seperti:

```
=== OCR Output ===
Invoice Number: 2023-0456
Date: 03/15/2024
Total: $1,234.56
```

Jika output terlihat berantakan, periksa kembali kualitas gambar atau coba filter tambahan (misalnya `BinarizationFilter` untuk gambar biner).

## Contoh Lengkap yang Berfungsi – Salin‑Tempel dan Jalankan

Berikut adalah program lengkap yang berdiri sendiri. Cukup ganti `YOUR_DIRECTORY/skewed_noisy.jpg` dengan path sebenarnya ke gambar uji Anda.

```csharp
using Aspose.Ocr;
using Aspose.Ocr.Filters;
using System;

public static class ImageOcrDemo
{
    public static void Main()
    {
        PreprocessAndOcr();
    }

    public static void PreprocessAndOcr()
    {
        // Step 1: Create OCR engine and set language
        var ocrEngine = new OcrEngine { Language = "en" };

        // Step 2: Build preprocessing pipeline
        ocrEngine.Preprocess.Add(new DeskewFilter());               // correct skew
        ocrEngine.Preprocess.Add(new DenoiseFilter());             // reduce noise
        ocrEngine.Preprocess.Add(new ContrastStretchFilter());     // enhance contrast

        // Step 3: Recognize text from the pre‑processed image
        var ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/skewed_noisy.jpg");

        // Step 4: Show the extracted text
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Output yang diharapkan** – Konsol akan mencetak representasi teks polos dari apa pun yang ada di gambar. Jika gambar berisi tanda sederhana yang bertuliskan “OpenAI”, Anda akan melihat tepat kata itu, tanpa simbol tambahan.

## Kasus Tepi & Cara Menyesuaikan Pipeline

### 1️⃣ Gambar Sangat Gelap

Jika filter kontras tidak cukup, tambahkan `BrightnessCorrectionFilter` di depan:

```csharp
ocrEngine.Preprocess.Add(new BrightnessCorrectionFilter(30)); // increase brightness by 30%
```

### 2️⃣ Dokumen Multi‑Bahasa

Set `Language = "en+fr"` (Aspose mendukung kode bahasa dipisahkan koma) dan tambahkan `LanguageDetectionFilter` jika Anda ingin mesin mendeteksi secara otomatis.

### 3️⃣ PDF Besar yang Dikonversi menjadi Gambar

Memproses PDF ribuan halaman satu gambar pada satu waktu dapat lambat. Gunakan `Parallel.ForEach` untuk menjalankan OCR pada beberapa gambar secara bersamaan, tetapi ingat bahwa `OcrEngine` tidak thread‑safe—buat instance terpisah per thread.

```csharp
Parallel.ForEach(imagePaths, path =>
{
    var engine = new OcrEngine { Language = "en" };
    // add same filters...
    var result = engine.RecognizeImage(path);
    // store result...
});
```

### 4️⃣ Mendapatkan Bounding Box

Jika Anda membutuhkan lokasi setiap kata (mis., untuk penyorotan), periksa `ocrResult.Regions`. Setiap region berisi koordinat `Rectangle` yang dapat Anda gunakan pada overlay UI.

```csharp
foreach (var region in ocrResult.Regions)
{
    Console.WriteLine($"{region.Text} at {region.Bounds}");
}
```

## Kesalahan Umum (Dan Cara Menghindarinya)

- **Melewatkan langkah Deskew** – Bahkan kemiringan 2 derajat dapat menurunkan kepercayaan hingga 20 %. Selalu tambahkan `DeskewFilter` ketika sumber tidak sejajar sempurna.
- **Menggunakan JPEG dengan kompresi berat** – Artefak kompresi terlihat seperti noise; beralihlah ke PNG atau TIFF untuk OCR yang lebih baik.
- **Hard‑coding path** – Path relatif bekerja secara lokal, tetapi dalam pipeline CI/CD Anda sebaiknya membaca lokasi gambar dari konfigurasi atau variabel lingkungan.

## Menguji Pengaturan Anda

1. Jalankan program dengan gambar bersih dan kontras tinggi. Anda harus mendapatkan teks hampir sempurna.
2. Ganti dengan foto berisik dan miring. Verifikasi bahwa output membaik setelah menambahkan ketiga filter.
3. Eksperimen dengan menghapus satu filter pada satu waktu untuk melihat dampaknya—ini membantu Anda memahami *mengapa* setiap langkah penting.

## Kesimpulan

Kami baru saja mendemonstrasikan cara **ekstrak teks dari gambar** menggunakan Aspose OCR, dan menunjukkan cara praktis **memproses gambar untuk OCR** yang bekerja dalam kebanyakan skenario dunia nyata. Dengan menautkan `DeskewFilter`, `DenoiseFilter`, dan `ContrastStretchFilter` Anda memberi mesin kanvas bersih, yang secara dramatis meningkatkan akurasi.

Dari sini Anda dapat menjelajahi filter yang lebih canggih, menangani dokumen multi‑halaman, atau mengintegrasikan hasil OCR ke dalam indeks pencarian. Apa pun yang Anda pilih, pola inti—inisialisasi, pra‑pemrosesan, pengenalan, dan konsumsi—tetap sama.

Siap meningkatkan level? Coba tambahkan `BinarizationFilter` untuk pemindaian hitam‑putih, atau hubungkan output ke basis data untuk PDF yang dapat dicari. Selamat coding, semoga setiap gambar yang Anda beri ke Aspose menghasilkan teks yang tajam dan dapat dibaca!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}