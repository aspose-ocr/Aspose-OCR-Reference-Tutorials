---
category: general
date: 2026-01-01
description: Kenali teks Rusia secara instan menggunakan Aspose OCR C#. Pelajari cara
  mengenali teks Cina, membaca jumlah halaman PDF, dan mengonversi teks halaman PDF
  dalam satu tutorial.
draft: false
keywords:
- recognize russian text
- aspose ocr c#
- recognize chinese text
- read pdf page count
- convert pdf page text
language: id
og_description: Mengenali teks Rusia dengan cepat menggunakan Aspose OCR C#. Tutorial
  ini juga mencakup cara mengenali teks Cina, membaca jumlah halaman PDF, dan mengonversi
  teks halaman PDF.
og_title: Mengenali teks Rusia dengan Aspose OCR C# – Panduan Lengkap
tags:
- Aspose OCR
- C#
- PDF processing
title: Mengenali teks Rusia dengan Aspose OCR C# – Panduan PDF Multi‑Halaman Lengkap
url: /id/net/text-recognition/recognize-russian-text-with-aspose-ocr-c-full-multi-page-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# mengenali teks Rusia dengan Aspose OCR C# – Tutorial PDF Multi‑Halaman Lengkap

Pernahkah Anda perlu **mengenali teks Rusia** dalam PDF yang mencampur bahasa, dan bertanya‑tanya bagaimana melakukannya tanpa harus menggunakan alat terpisah untuk setiap halaman? Anda tidak sendirian. Dalam banyak proyek dunia nyata, Anda akan mendapatkan satu PDF yang berisi bahasa Inggris, Rusia, bahkan Mandarin pada halaman‑halaman yang berbeda, dan Anda tetap menginginkan output teks yang bersih dan tunggal.

Dalam panduan ini kami akan menunjukkan secara tepat cara **mengenali teks Rusia** (dan bahasa lain) menggunakan **Aspose OCR C#**, sekaligus mendemonstrasikan cara **membaca jumlah halaman PDF**, **mengenali teks Mandarin**, dan **mengonversi teks halaman PDF** menjadi dump konsol yang praktis. Tanpa layanan eksternal, tanpa langkah tersembunyi—hanya kode C# murni yang dapat Anda salin‑tempel dan jalankan.

> **Apa yang akan Anda dapatkan**  
> * Aplikasi konsol C# yang dapat dijalankan dan memproses PDF multi‑halaman.  
> * Pemilihan bahasa per halaman (Rusia, Mandarin, Inggris).  
> * Teknik untuk menanyakan jumlah halaman PDF dan mengekstrak teks tiap halaman.  
> * Tips, jebakan, dan ekstensi yang dapat Anda terapkan pada proyek Anda sendiri.

---

## Prasyarat

- .NET 6.0 atau lebih baru (kode ini juga bekerja pada .NET Framework 4.7+).  
- Paket NuGet **Aspose.OCR for .NET** terpasang (`dotnet add package Aspose.OCR`).  
- File PDF yang berisi bahasa campuran; untuk demo kami akan menggunakan `mixed_lang.pdf`.  
- Familiaritas dasar dengan aplikasi konsol C#.

Jika Anda belum memiliki salah satu dari ini, unduh Aspose OCR terbaru dari NuGet dan letakkan PDF Anda di lokasi yang dapat dijangkau dari folder proyek.

---

## Langkah 1 – Inisialisasi Mesin Aspose OCR

Hal pertama yang Anda butuhkan adalah sebuah instance dari `OcrEngine`. Objek ini menyimpan semua pengaturan (seperti bahasa) dan melakukan pekerjaan berat.

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;

class MultiPageDemo
{
    static void Main()
    {
        // Create the OCR engine – this is where we’ll set language per page
        OcrEngine ocrEngine = new OcrEngine();
```

> **Mengapa ini penting:**  
> Mesin dapat dipakai ulang, sehingga kita tidak membuang memori dengan membuat instance baru untuk setiap halaman. Menggunakannya kembali juga memungkinkan kita mengubah bahasa secara dinamis, yang sangat penting untuk **mengenali teks Rusia** pada satu halaman dan **mengenali teks Mandarin** pada halaman lain.

---

## Langkah 2 – Muat PDF dan Cari Tahu Berapa Banyak Halamannya

Sebelum mulai mengenali, kita perlu objek PDF dan jumlah halamannya. Aspose OCR memperlakukan setiap halaman sebagai `OcrImage`.

```csharp
        // Load the multi‑page PDF
        OcrImage multiPageImage = OcrImage.FromFile(@"YOUR_DIRECTORY/mixed_lang.pdf");

        // Print the total number of pages – this answers the “read pdf page count” question
        Console.WriteLine($"PDF contains {multiPageImage.PageCount} pages.");
```

> **Tip:** Jika PDF sangat besar, Anda mungkin ingin membaca jumlah halaman terlebih dahulu dan memutuskan apakah akan memproses semua halaman atau hanya sebagian.

---

## Langkah 3 – Pemetaan Setiap Halaman ke Bahasa yang Diinginkan

Aspose OCR mendukung banyak bahasa, tetapi Anda harus memberi tahu bahasa mana yang akan dipakai untuk tiap halaman. Di bawah ini kami membuat `Dictionary<int, OcrLanguage>` di mana kuncinya adalah indeks halaman berbasis nol.

```csharp
        // Define which language each page should be read with
        var languageMap = new Dictionary<int, OcrLanguage>
        {
            { 0, OcrLanguage.English },   // Page 1 – English
            { 1, OcrLanguage.Russian },   // Page 2 – Russian (our primary focus)
            { 2, OcrLanguage.Chinese }    // Page 3 – Chinese
        };
```

> **Mengapa ini krusial:**  
> Tanpa peta ini, mesin OCR akan mencoba satu bahasa default untuk semua halaman, menghasilkan output yang berantakan untuk teks Rusia atau Mandarin. Langkah ini secara langsung memungkinkan **mengenali teks Rusia** dan **mengenali teks Mandarin** dengan benar.

---

## Langkah 4 – Loop Melalui Semua Halaman, Atur Bahasa, dan Kenali Teks

Sekarang kami iterasi setiap halaman, mengganti bahasa berdasarkan peta, dan memanggil `Recognize`. Hasilnya disimpan dalam `OcrResult`, dari mana kami mengekstrak teks polos.

```csharp
        // Process each page one by one
        for (int pageIndex = 0; pageIndex < multiPageImage.PageCount; pageIndex++)
        {
            // Choose language – default to English if we haven’t specified one
            ocrEngine.Settings.Language = languageMap.ContainsKey(pageIndex)
                                          ? languageMap[pageIndex]
                                          : OcrLanguage.English;

            // Perform OCR on the current page
            var pageResult = ocrEngine.Recognize(multiPageImage.GetPage(pageIndex));

            // Output the recognized text – this is the “convert pdf page text” step
            Console.WriteLine($"--- Page {pageIndex + 1} ({ocrEngine.Settings.Language}) ---");
            Console.WriteLine(pageResult.Text);
            Console.WriteLine(); // Blank line for readability
        }
    }
}
```

### Output Konsol yang Diharapkan

```
PDF contains 3 pages.
--- Page 1 (English) ---
This is an English paragraph on the first page.

--- Page 2 (Russian) ---
Это русский текст на второй странице.

--- Page 3 (Chinese) ---
这是第三页的中文文本。
```

> **Penjelasan alur:**  
> * Loop menghormati **membaca jumlah halaman PDF** yang kami cetak sebelumnya.  
> * Dengan menukar `ocrEngine.Settings.Language` setiap iterasi, kami menjamin **mengenali teks Rusia** pada halaman 2 dan **mengenali teks Mandarin** pada halaman 3 secara akurat.  
> * Pernyataan `Console.WriteLine` secara efektif **mengonversi teks halaman PDF** menjadi string yang dapat dibaca manusia.

---

## Langkah 5 – Jalankan, Verifikasi, dan Sesuaikan

1. Bangun proyek (`dotnet build`).  
2. Jalankan (`dotnet run`).  
3. Bandingkan output konsol dengan PDF asli.  

Jika Anda menemukan karakter yang hilang, pertimbangkan:

- **Meningkatkan akurasi OCR** dengan mengatur `ocrEngine.Settings.DetectTextOrientation = true;`.  
- **Menyediakan paket bahasa khusus** jika kamus Rusia atau Mandarin bawaan sudah usang.  
- **Menyesuaikan DPI** saat memuat PDF (`OcrImage.FromFile(path, 300)`), yang dapat meningkatkan pengenalan pada pemindaian beresolusi rendah.

---

## Bonus: Menangani Kasus Pinggir

### Bagaimana jika bahasa sebuah halaman tidak ada dalam peta?

Kode sudah kembali ke bahasa Inggris, tetapi Anda juga dapat menambahkan fallback yang mencatat peringatan:

```csharp
if (!languageMap.TryGetValue(pageIndex, out var lang))
{
    Console.WriteLine($"Warning: No language defined for page {pageIndex + 1}. Using English.");
    lang = OcrLanguage.English;
}
ocrEngine.Settings.Language = lang;
```

### Bisakah kami memproses PDF dengan lebih dari tiga bahasa?

Tentu saja. Perluas `languageMap` dengan indeks tambahan dan nilai `OcrLanguage` yang didukung (misalnya, `OcrLanguage.French`). Loop akan menangani berapa pun jumlah halaman.

### Bagaimana cara mengekspor hasil ke file alih‑alih konsol?

Ganti pemanggilan `Console.WriteLine` dengan `File.AppendAllText("output.txt", …)` atau gunakan `StringBuilder` yang Anda tulis sekali setelah loop selesai.

---

## Ilustrasi Gambar

![contoh mengenali teks Rusia](/images/recognize-russian-text.png "Tangkapan layar yang menunjukkan output OCR untuk teks Rusia")

*Gambar di atas memperlihatkan output konsol ketika **mengenali teks Rusia** dilakukan pada PDF berbahasa campuran.*

---

## Kesimpulan

Kami telah menelusuri contoh lengkap end‑to‑end yang menunjukkan cara **mengenali teks Rusia** (dan juga **mengenali teks Mandarin**) dari PDF multi‑halaman menggunakan **Aspose OCR C#**. Dengan membaca jumlah halaman PDF, memetakan tiap halaman ke bahasa yang tepat, dan melakukan iterasi melalui dokumen, Anda dapat **mengonversi teks halaman PDF** menjadi string polos yang siap disimpan, diindeks, atau dianalisis lebih lanjut.

Singkatnya:

- **Inisialisasi** satu `OcrEngine`.  
- **Muat** PDF dan **baca jumlah halaman PDF**.  
- **Peta** halaman ke bahasa (Rusia, Mandarin, dll.).  
- **Iterasi**, atur `ocrEngine.Settings.Language`, dan **kenali** tiap halaman.  
- **Keluarkan** atau simpan teks yang diekstrak.

Silakan sesuaikan pola ini untuk dokumen yang lebih besar, tambahkan penanganan error, atau hubungkan hasilnya ke indeks pencarian. Ide utama—pemilihan bahasa per halaman—tetap sama, dan itulah yang membuat **mengenali teks Rusia** menjadi dapat diandalkan pada PDF berbahasa campuran.

Punya skenario berbeda, seperti memindai gambar alih‑alih PDF? Mesin yang sama bekerja; cukup ganti `OcrImage.FromFile` dengan `OcrImage.FromStream` atau `FromBitmap`. Selamat coding, semoga OCR Anda selalu akurat!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}