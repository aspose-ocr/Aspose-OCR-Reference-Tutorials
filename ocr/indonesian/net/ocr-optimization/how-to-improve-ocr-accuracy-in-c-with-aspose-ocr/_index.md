---
category: general
date: 2026-04-11
description: Pelajari cara meningkatkan OCR di C# dengan mengenali teks dari JPG,
  meluruskan gambar, dan menghilangkan noise menggunakan Aspose OCR.
draft: false
keywords:
- how to improve OCR
- recognize text from jpg
- extract text from image
- how to deskew image
- how to remove noise
language: id
og_description: Temukan cara meningkatkan OCR dengan mengenali teks dari JPG, memperbaiki
  kemiringan gambar, dan menghilangkan noise—panduan lengkap C#.
og_title: Cara Meningkatkan Akurasi OCR di C# dengan Aspose OCR
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Cara Meningkatkan Akurasi OCR di C# dengan Aspose OCR
url: /id/net/ocr-optimization/how-to-improve-ocr-accuracy-in-c-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Meningkatkan Akurasi OCR di C# dengan Aspose OCR

Pernah bertanya-tanya **how to improve OCR** hasil ketika pemindaian Anda terlihat lebih seperti seni abstrak daripada teks yang dapat dibaca? Anda bukan satu-satunya. Dalam banyak proyek dunia nyata—seperti faktur, kwitansi, atau catatan tulisan tangan—gambar sumber sering miring, berbutir, atau hanya berisik. Kabar baiknya? Aspose OCR memberi Anda beberapa pengaturan pra‑pemrosesan yang dapat mengubah kekacauan itu menjadi karakter bersih yang dapat dibaca mesin. Dalam tutorial ini kami akan membahas contoh lengkap yang siap dijalankan yang menunjukkan **how to improve OCR** dengan **recognize text from JPG**, meluruskan gambar, dan menghilangkan noise yang tidak diinginkan.

> *Pro tip:* Jika Anda melewatkan pra‑pemrosesan, kemungkinan besar Anda akan mendapatkan output yang berantakan seperti teka‑teki silang yang misterius. Mari hindari itu.

![Cara meningkatkan OCR dengan pra‑pemrosesan Aspose OCR](https://example.com/ocr-preprocess.png "cara meningkatkan OCR dengan Aspose OCR")

## Apa yang Akan Anda Pelajari

Dalam beberapa menit ke depan Anda akan melihat:

1. Cara menyiapkan mesin Aspose OCR untuk akurasi optimal.  
2. Kode tepat yang diperlukan untuk **recognize text from JPG** file.  
3. Mengapa mengaktifkan *AutoDeskew* dan *RemoveNoise* penting dan cara menyesuaikannya.  
4. Cara **extract text from image** file tanpa menulis filter khusus.  
5. Jebakan umum (file hilang, format tidak didukung) dan perbaikan cepat.

Pada akhir Anda akan memiliki satu aplikasi konsol C# yang dapat mengambil JPG apa pun, membersihkannya, dan mengeluarkan string yang diekstrak—siap untuk pemrosesan lanjutan atau penyimpanan.

## Prasyarat

- .NET 6.0 SDK atau lebih baru (contoh menggunakan pernyataan tingkat atas untuk singkat).  
- Paket NuGet Aspose.OCR (`dotnet add package Aspose.OCR`).  
- Contoh gambar JPG (dengan nama `input.jpg`) ditempatkan di folder yang sama dengan executable.  
- Pemahaman dasar tentang C#—tidak memerlukan konsep lanjutan.

Jika Anda sudah memiliki proyek, cukup tempelkan kode di dalamnya; jika tidak, buat aplikasi konsol baru:

```bash
dotnet new console -n OcrDemo
cd OcrDemo
dotnet add package Aspose.OCR
```

Sekarang mari kita selami kode.

## Cara Meningkatkan OCR: Ikhtisar Pengaturan Pra‑Pemrosesan

Inti dari **how to improve OCR** terletak pada objek `PreprocessSettings`. Anggaplah sebagai editor gambar mini yang berjalan *sebelum* mesin pengenalan karakter yang sebenarnya dijalankan. Berikut adalah rangkuman cepat dari flag paling berpengaruh:

| Setting                | Apa yang dilakukannya                                            | Kasus penggunaan umum |
|------------------------|-------------------------------------------------------------------|-----------------------|
| `AutoDeskew`           | Menerapkan algoritma de‑skew berbasis deep‑learning.             | Halaman yang dipindai sedikit miring. |
| `AdaptiveThreshold`    | Meningkatkan kontras pada gambar dengan cahaya rendah atau pudar.| Kwitansi lama dengan tinta yang pudar. |
| `RemoveNoise`          | Menjalankan filter Gaussian‑blur untuk mengurangi bintik‑bintik. | Foto yang diambil dengan lampu kilat smartphone. |
| `NoiseRemovalStrength`| Mengontrol tingkat agresivitas (1 = rendah, 3 = tinggi).          | Sesuaikan berdasarkan seberapa berbutir sumbernya. |

Mengaktifkan opsi-opsi ini pada dasarnya adalah “bumbu rahasia” untuk **how to improve OCR** pada masukan yang tidak sempurna.

## Mengenali Teks dari JPG dengan Aspose OCR

Berikut adalah program lengkap yang siap dijalankan. Setiap baris diberi anotasi sehingga Anda dapat melihat *mengapa* setiap bagian ada, bukan hanya *apa* yang dilakukannya.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

class PreprocessDemo
{
    static void Main()
    {
        // ------------------------------------------------------------
        // Step 1: Create an OCR engine instance.
        // ------------------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine();

        // ------------------------------------------------------------
        // Step 2: Fine‑tune preprocessing to improve accuracy.
        // ------------------------------------------------------------
        ocrEngine.Settings.Preprocess = new PreprocessSettings
        {
            AutoDeskew = true,               // How to deskew image automatically.
            AdaptiveThreshold = true,        // Improves contrast for better recognition.
            RemoveNoise = true,              // How to remove noise before OCR.
            NoiseRemovalStrength = 2         // Medium strength; adjust 1‑3 as needed.
        };

        // ------------------------------------------------------------
        // Step 3: Load the JPG image you want to process.
        // ------------------------------------------------------------
        // If the file is missing, Aspose will throw a FileNotFoundException.
        // Wrap it in a try/catch if you need graceful fallback.
        ImageStream image;
        try
        {
            image = ImageStream.FromFile("input.jpg");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Error loading image: {ex.Message}");
            return;
        }

        // ------------------------------------------------------------
        // Step 4: Run the OCR engine on the preprocessed image.
        // ------------------------------------------------------------
        OcrResult ocrResult = ocrEngine.Recognize(image);

        // ------------------------------------------------------------
        // Step 5: Display the extracted text.
        // ------------------------------------------------------------
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

### Output yang Diharapkan

Jika `input.jpg` berisi frasa “Invoice #12345 – Total: $256.78”, konsol akan mencetak:

```
=== Extracted Text ===
Invoice #12345 – Total: $256.78
```

Perhatikan bagaimana outputnya bersih, dengan tanda hubung dan simbol dolar tetap—tepat seperti yang Anda harapkan saat **extracting text from image** file.

## Cara Meluruskan Gambar Menggunakan Pengaturan Pra‑Pemrosesan

Mengapa pelurusan penting? Bahkan kemiringan 2‑derajat pun dapat membingungkan tahap segmentasi karakter, menyebabkan huruf teridentifikasi salah. Flag `AutoDeskew` menjalankan jaringan saraf konvolusional di balik layar yang mendeteksi sudut dominan dan memutar gambar kembali ke posisi dasar.

Jika Anda membutuhkan kontrol lebih, Anda dapat mengatur sudut secara manual:

```csharp
ocrEngine.Settings.Preprocess = new PreprocessSettings
{
    AutoDeskew = false,          // Turn off automatic detection.
    // Manually specify a rotation angle (in degrees):
    DeskewAngle = -1.8           // Positive = clockwise, negative = counter‑clockwise.
};
```

> **Kapan menggunakan deskew manual:** Jika Anda tahu kamera secara konsisten memiringkan gambar dengan jumlah tetap (misalnya, scanner yang dipasang), mengkodekan sudut secara keras menghemat sedikit waktu pemrosesan.

## Cara Menghilangkan Noise untuk Ekstraksi yang Lebih Bersih

Noise muncul sebagai bintik‑bintik acak atau butir, terutama pada foto dengan cahaya rendah. Flag `RemoveNoise` menerapkan filter bilateral yang menghaluskan latar belakang sambil mempertahankan tepi (karakter sebenarnya). Properti `NoiseRemovalStrength` memungkinkan Anda mengatur tingkat agresivitas:

| Kekuatan | Efek |
|----------|------|
| 1        | Penghalusan ringan—baik untuk gambar yang sedikit berbutir. |
| 2        | Seimbang—berfungsi untuk sebagian besar foto smartphone. |
| 3        | Penghalusan berat—gunakan ketika gambar sangat berisik, tetapi hati-hati mengaburkan goresan tipis. |

Jika Anda menemukan situasi di mana font kecil menjadi tidak terbaca setelah penghalusan berat, cukup turunkan kekuatan atau nonaktifkan filter sepenuhnya.

## Ekstrak Teks dari Gambar: Lebih dari JPG

Meskipun demo kami berfokus pada JPG, Aspose OCR mendukung PNG, BMP, TIFF, dan bahkan halaman PDF. Untuk **extract text from image** format selain JPG, cukup ubah ekstensi file di `ImageStream.FromFile`. Untuk TIFF multi‑halaman Anda dapat melakukan loop melalui setiap halaman:

```csharp
for (int i = 0; i < tiffPageCount; i++)
{
    ImageStream page = ImageStream.FromFile($"input_{i}.tiff");
    OcrResult result = ocrEngine.Recognize(page);
    Console.WriteLine($"--- Page {i + 1} ---");
    Console.WriteLine(result.Text);
}
```

Potongan kode itu menunjukkan bagaimana Anda dapat memperluas alur kerja **how to improve OCR** yang sama untuk memproses batch seluruh tumpukan dokumen yang dipindai.

## Jebakan Umum & Cara Memperbaikinya

| Gejala | Penyebab Kemungkinan | Perbaikan Cepat |
|--------|----------------------|-----------------|
| Output kosong | Gambar menjadi sepenuhnya putih setelah pra‑pemrosesan (threshold terlalu agresif) | Kurangi `NoiseRemovalStrength` atau set `AdaptiveThreshold = false`. |
| Karakter berantakan | Model bahasa salah (default adalah English) | Set `ocrEngine.Settings.Language = Language.English;` atau muat paket bahasa khusus. |
| Crash pada file besar | Kekurangan memori karena gambar beresolusi tinggi | Turunkan skala dengan `ocrEngine.Settings.ImageResizeFactor = 0.5;` sebelum pengenalan. |
| Tidak ada output untuk pemindaian yang diputar | `AutoDeskew` tidak sengaja dinonaktifkan | Aktifkan `AutoDeskew = true` atau berikan `DeskewAngle` yang benar. |

Menyimpan hal ini dalam pikiran akan menghemat berjam-jam debugging ketika Anda mencoba **how to improve OCR** dalam pipeline produksi.

## Bonus: Menyesuaikan untuk Kecepatan vs. Akurasi

Jika Anda memproses ribuan kwitansi per hari, Anda mungkin memprioritaskan kecepatan. Matikan `AdaptiveThreshold` dan set `NoiseRemovalStrength = 1`. Sebaliknya, untuk dokumen hukum di mana satu karakter yang terlewat dapat mahal, biarkan semua flag aktif dan pertimbangkan meningkatkan `NoiseRemovalStrength` menjadi 3.

## Kesimpulan

Kami telah membahas seluruh perjalanan **how to improve OCR** di C# menggunakan Aspose OCR: mulai dari membuat mesin, mengonfigurasi pra‑pemrosesan (fondasi dari *how to deskew image* dan *how to remove noise*), memuat JPG, mengenali teks, dan menangani kasus tepi. Kode ini berdiri sendiri, dapat dijalankan langsung, dan menunjukkan langkah tepat yang Anda perlukan untuk **recognize text from jpg** dan **extract text from image** file.

### Apa Selanjutnya?

- Bereksperimen dengan format gambar lain (PNG, TIFF) untuk melihat bagaimana pengaturan yang sama berperilaku.  
- Integrasikan output OCR ke dalam basis data atau

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}