---
category: general
date: 2026-04-29
description: Cara melakukan OCR di C# menggunakan Aspose OCR – mengekstrak teks Hindi,
  mengenali teks dari PNG, dan mengubah bahasa OCR secara dinamis.
draft: false
keywords:
- how to perform OCR
- extract Hindi text
- multi language OCR
- recognize text from PNG
- change OCR language
language: id
og_description: Cara melakukan OCR di C# dengan Aspose OCR. Pelajari cara mengekstrak
  teks Hindi, mengenali teks dari file PNG, dan mengubah bahasa OCR secara dinamis.
og_title: Cara Melakukan OCR di C# – Tutorial Lengkap Multi‑Bahasa
tags:
- OCR
- C#
- Aspose
title: Cara Melakukan OCR di C# – Panduan Multi‑Bahasa
url: /id/net/ocr-configuration/how-to-perform-ocr-in-c-multi-language-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Melakukan OCR di C# – Panduan Multi‑Bahasa

Pernah bertanya‑tanya **bagaimana melakukan OCR** pada gambar yang berisi lebih dari satu bahasa? Mungkin Anda memiliki kwitansi Rusia dan selebaran Hindi yang berdampingan, dan Anda membutuhkan teks dari keduanya tanpa harus menggunakan alat terpisah. Itu adalah masalah umum bagi siapa saja yang menangani dokumen internasional.  

Dalam tutorial ini kami akan menunjukkan cara bersih, end‑to‑end untuk **melakukan OCR** dengan Aspose OCR, mengekstrak teks Hindi, mengenali teks dari file PNG, dan bahkan **mengubah bahasa OCR** secara dinamis. Pada akhir tutorial Anda akan memiliki potongan kode yang dapat digunakan kembali dan bekerja untuk kombinasi bahasa yang didukung apa pun.

## Apa yang Akan Anda Pelajari

- Cara menyiapkan mesin Aspose OCR dalam proyek .NET.  
- Perbedaan antara mengonfigurasi bahasa statis versus menukar bahasa pada runtime.  
- Cara mengekstrak teks Hindi dari sebuah gambar dan mengapa perpustakaan dapat mengunduh paket bahasa secara otomatis.  
- Tips menangani file PNG, mengatasi modul bahasa yang hilang, dan memecahkan masalah umum.

> **Pro tip:** Jika Anda sudah menggunakan Aspose OCR untuk satu bahasa, Anda hanya perlu menyesuaikan beberapa baris kode untuk mengubahnya menjadi solusi **OCR multi bahasa**.

---

## Prasyarat

| Persyaratan | Mengapa penting |
|-------------|-----------------|
| .NET 6 atau lebih baru (atau .NET Framework 4.7+) | Aspose OCR menargetkan runtime modern; versi lama mungkin tidak mendukung unduhan otomatis paket bahasa. |
| Paket NuGet Aspose.OCR (`Install-Package Aspose.OCR`) | Menyediakan kelas `OcrEngine` dan enum bahasa. |
| Dua contoh gambar PNG (`russian.png` dan `hindi.png`) yang ditempatkan di folder yang diketahui | Menunjukkan **mengenali teks dari PNG** dan **mengekstrak teks Hindi** dalam satu kali jalankan. |
| Koneksi internet (untuk pertama kalinya Anda meminta bahasa baru) | Perpustakaan mengambil modul bahasa yang diperlukan secara on‑demand. |

Tidak ada binari OCR tambahan atau alat eksternal yang diperlukan—Aspose melakukan semua pekerjaan berat.

---

## Langkah 1 – Instal Aspose  OCR dan Buat Engine

Pertama‑tama: tambahkan paket Aspose OCR ke proyek Anda. Buka Package Manager Console dan jalankan:

```powershell
Install-Package Aspose.OCR
```

Sekarang kita dapat membuat instance `OcrEngine`. Anggap engine sebagai pemindai pintar yang dapat dikonfigurasi ulang pada runtime.

```csharp
using Aspose.OCR;
using System;

class MultiLanguageOcrDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        var ocrEngine = new OcrEngine();
```

Mengapa kita membuat engine hanya sekali? Menggunakan kembali instance yang sama menghindari beban memuat pustaka OCR native berulang‑ulang, yang dapat terasa pada batch besar.

---

## Langkah 2 – Kenali Teks Rusia (Bahasa Pertama)

Sebelum beralih ke Hindi, mari buktikan engine berfungsi dengan bahasa yang sudah diketahui. Kami mengatur bahasa ke Russian, memberi PNG, dan mencetak hasilnya.

```csharp
        // Step 2: Configure the engine for Russian and recognize the image
        ocrEngine.Config.Language = OcrLanguage.Russian;
        var russianImagePath = @"YOUR_DIRECTORY/russian.png";
        var russianOcrResult = ocrEngine.Recognize(OcrEngine.LoadImage(russianImagePath));
        Console.WriteLine("Russian: " + russianOcrResult.Text);
```

**Apa yang terjadi di balik layar?**  
`OcrEngine.LoadImage` membaca PNG ke dalam format bitmap internal Aspose. Properti `Config.Language` memberi tahu engine OCR kamus dan set karakter mana yang harus diterapkan. Saat Anda memanggil `Recognize`, engine menjalankan model jaringan saraf yang disetel untuk karakter Cyrillic dan mengembalikan objek `OcrResult` yang berisi output teks polos.

> **Output yang diharapkan (contoh)**  
> `Russian: Привет, мир! Это тестовое изображение.`

Jika Anda melihat karakter yang kacau, periksa kembali apakah gambar tidak rusak dan modul bahasa Rusia tersedia (termasuk dalam paket dasar).

---

## Langkah 3 – Beralih ke Hindi – **Ubah Bahasa OCR** Secara Dinamis

Sekarang bagian yang menyenangkan: menukar bahasa tanpa membuat ulang engine. Aspose OCR akan mengunduh modul Hindi pada pertama kali Anda memintanya, jadi Anda hanya membutuhkan koneksi internet satu kali.

```csharp
        // Step 3: Switch the engine to Hindi (the language module will be downloaded automatically) and recognize the image
        ocrEngine.Config.Language = OcrLanguage.Hindi;
        var hindiImagePath = @"YOUR_DIRECTORY/hindi.png";
        var hindiOcrResult = ocrEngine.Recognize(OcrEngine.LoadImage(hindiImagePath));
        Console.WriteLine("Hindi: " + hindiOcrResult.Text);
    }
}
```

**Mengapa ini berhasil?**  
Setter `Config.Language` memicu rutin lazy‑load. Jika paket bahasa yang diminta tidak ada di disk, Aspose akan menghubungi CDN-nya, mengambil modul terkompresi, menyimpannya di cache, dan kemudian melanjutkan pengenalan. Desain ini memungkinkan Anda membangun pipeline **OCR multi bahasa** yang menyesuaikan dengan konten pada runtime.

> **Contoh output Hindi**  
> `Hindi: नमस्ते दुनिया! यह एक परीक्षण छवि है।`

Perhatikan bagaimana objek `ocrEngine` yang sama menangani skrip Cyrillic dan Devanagari secara mulus. Itulah kekuatan **mengubah bahasa OCR** secara dinamis.

---

## Langkah 4 – Menangani File PNG Secara Efisien

Kedua contoh di atas menggunakan gambar PNG, yang merupakan format umum untuk screenshot dan dokumen yang dipindai. PNG bersifat lossless, artinya data piksel tetap murni—sempurna untuk OCR. Namun, PNG berukuran besar dapat mengonsumsi memori. Berikut beberapa tips cepat:

1. **Resize jika diperlukan** – Jika lebar gambar melebihi 2000 px, perkecil dengan `System.Drawing.Image` sebelum memberikannya ke Aspose.  
2. **Set DPI** – Beberapa engine OCR mendapat manfaat dari DPI 300. Anda dapat menyematkannya melalui overload `OcrEngine.LoadImage` yang menerima `Bitmap` dengan resolusi khusus.

```csharp
using System.Drawing;

// Example of downscaling a huge PNG
Bitmap original = new Bitmap(@"YOUR_DIRECTORY/large.png");
int maxWidth = 2000;
if (original.Width > maxWidth)
{
    int newHeight = (int)((double)original.Height / original.Width * maxWidth);
    Bitmap resized = new Bitmap(original, new Size(maxWidth, newHeight));
    original.Dispose(); // free original memory
    original = resized;
}
var result = ocrEngine.Recognize(OcrEngine.LoadImage(original));
```

Penyesuaian ini menjaga penggunaan memori tetap rendah dan sering meningkatkan akurasi karena engine OCR bekerja dengan grid piksel yang lebih mudah dikelola.

---

## Langkah 5 – Menggabungkan Semua – Contoh Lengkap yang Berjalan

Berikut adalah program lengkap yang siap dijalankan yang mendemonstrasikan **cara melakukan OCR**, **mengekstrak teks Hindi**, **mengenali teks dari PNG**, dan **mengubah bahasa OCR** tanpa memulai ulang engine.

```csharp
using Aspose.OCR;
using System;
using System.Drawing;

class MultiLanguageOcrDemo
{
    static void Main()
    {
        // Create a single OCR engine instance (re‑use it for all languages)
        var ocrEngine = new OcrEngine();

        // ----------- Russian ----------
        ocrEngine.Config.Language = OcrLanguage.Russian;
        var russianPath = @"YOUR_DIRECTORY/russian.png";
        var russianResult = ocrEngine.Recognize(OcrEngine.LoadImage(russianPath));
        Console.WriteLine("Russian: " + russianResult.Text);

        // ----------- Hindi ------------
        // The first time this runs, the Hindi language pack will be downloaded automatically.
        ocrEngine.Config.Language = OcrLanguage.Hindi;
        var hindiPath = @"YOUR_DIRECTORY/hindi.png";
        var hindiResult = ocrEngine.Recognize(OcrEngine.LoadImage(hindiPath));
        Console.WriteLine("Hindi: " + hindiResult.Text);

        // ----------- Optional PNG optimization ----------
        // If you have very large PNGs, resize them before recognition (example shown earlier).
        // This block is optional and can be removed if your images are already sized appropriately.
    }
}
```

**Menjalankan kode** mencetak sesuatu seperti:

```
Russian: Привет, мир! Это тестовое изображение.
Hindi: नमस्ते दुनिया! यह एक परीक्षण छवि है।
```

Jika Anda melihat baris‑baris tersebut, selamat—Anda telah berhasil membangun solusi **OCR multi bahasa** yang dapat **mengekstrak teks Hindi** dan **mengenali teks dari file PNG** dengan satu engine.

---

## Pertanyaan yang Sering Diajukan (FAQ)

| Pertanyaan | Jawaban |
|------------|---------|
| *Apakah saya memerlukan lisensi untuk Aspose OCR?* | Kunci evaluasi gratis dapat digunakan untuk pengujian, tetapi penggunaan produksi memerlukan lisensi komersial. |
| *Bisakah saya mengenali lebih dari dua bahasa dalam satu gambar?* | Ya. Atur `Config.Language` ke `OcrLanguage.Multiple` dan berikan daftar dipisahkan koma (misalnya, `Russian, Hindi`). |
| *Bagaimana jika modul bahasa gagal diunduh?* | Periksa pengaturan firewall atau proxy Anda. Anda juga dapat mengunduh modul sebelumnya dari portal Aspose dan menaruhnya di folder `Data`. |
| *Apakah PNG satu‑satunya format yang didukung?* | Tidak. Aspose OCR juga menangani JPEG, BMP, TIFF, dan PDF (sebagai gambar). PNG hanyalah pilihan umum untuk kualitas lossless. |

---

## Langkah Selanjutnya & Topik Terkait

- **Pemrosesan batch** – Loop melalui direktori PNG dan simpan hasilnya ke file CSV.  
- **Ekstraksi PDF** – Gunakan `OcrEngine.RecognizePdf` untuk mengambil teks dari PDF yang dipindai.  
- **Kamus khusus** – Perluas paket bahasa bawaan dengan daftar kata yang disediakan pengguna untuk kosakata domain‑spesifik.  
- **Pengoptimalan performa** – Paralelisasi panggilan dengan `Parallel.ForEach` saat bekerja dengan kumpulan gambar besar.  

Mengeksplorasi area‑area ini akan memperdalam penguasaan Anda tentang **cara melakukan OCR** dalam berbagai skenario.

---

## Kesimpulan

Anda baru saja mempelajari **cara melakukan OCR** di C# menggunakan Aspose OCR, beralih bahasa secara dinamis, dan berhasil **mengekstrak teks Hindi** dari gambar PNG. Inti pentingnya adalah satu instance `OcrEngine` dapat berfungsi sebagai mesin **OCR multi bahasa** yang serbaguna—cukup atur `Config.Language` dan biarkan perpustakaan menangani sisanya.

Cobalah kode tersebut, ganti gambar contoh dengan milik Anda, dan bereksperimen dengan bahasa tambahan. Fleksibilitas Aspose OCR berarti Anda dapat meningkatkan dari prototipe cepat ke pipeline pemrosesan dokumen tingkat produksi dengan perubahan minimal.

Selamat coding, semoga petualangan ekstraksi teks Anda bebas error! 

![contoh cara melakukan OCR](/images/ocr-demo.png "contoh cara melakukan OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}