---
category: general
date: 2026-03-07
description: Pelajari cara membaca teks dari PNG dan mengekstrak teks Cyrillic menggunakan
  Aspose OCR, mengonversi gambar menjadi teks, serta mengunduh paket bahasa Cyrillic.
draft: false
keywords:
- read text from png
- extract cyrillic text
- convert image to text
- load image for ocr
- download cyrillic language pack
language: id
og_description: Pelajari cara membaca teks dari PNG, mengekstrak teks Cyrillic, dan
  mengonversi gambar menjadi teks menggunakan Aspose OCR dalam C#.
og_title: baca teks dari png – ekstrak teks Cyrillic dengan Aspose OCR
tags:
- Aspose OCR
- C#
- Image Processing
title: baca teks dari png – ekstrak teks Cyrillic dengan Aspose OCR
url: /id/net/ocr-configuration/read-text-from-png-extract-cyrillic-text-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# membaca teks dari png – mengekstrak teks Cyrillic dengan Aspose OCR

Perlu **membaca teks dari file png** dan mengambil karakter Cyrillic? Pada panduan ini kami akan menunjukkan cara membaca teks dari png menggunakan Aspose OCR, mengekstrak teks Cyrillic, dan **mengonversi gambar menjadi teks** hanya dalam beberapa baris C#.  

Jika Anda pernah melihat screenshot faktur Rusia dan bertanya‑tanya bagaimana cara mengubah kata‑kata itu menjadi string yang dapat dicari, Anda berada di tempat yang tepat. Kami juga akan membahas cara **mengunduh paket bahasa Cyrillic** secara otomatis, sehingga Anda tidak perlu mencari file tambahan.

## Apa yang akan Anda capai

Pada akhir tutorial ini Anda akan dapat:

* **Memuat gambar untuk OCR** langsung dari disk atau aliran.  
* Mengatur mesin ke **bahasa Cyrillic** tanpa mengunduh secara manual.  
* Menjalankan pengenalan dan **mengekstrak teks Cyrillic** dari file PNG.  
* Melihat teks yang dikenali dicetak ke konsol – hasil teks polos yang bersih yang dapat Anda masukkan ke basis data, indeks pencarian, atau alur kerja lainnya.

Tanpa layanan eksternal, tanpa kunci cloud, hanya paket NuGet Aspose OCR dan beberapa baris C#.

## Prasyarat

* .NET 6.0 atau lebih baru (kode ini bekerja pada .NET Core, .NET Framework, dan .NET 5+).  
* Visual Studio 2022 atau editor apa pun yang Anda suka.  
* Paket NuGet Aspose.OCR (`dotnet add package Aspose.OCR`).  
* Gambar PNG yang berisi karakter Cyrillic – misalnya `cyrillic_sample.png` yang ditempatkan dalam folder bernama `YOUR_DIRECTORY`.

> **Tips pro:** Jika Anda menggunakan Visual Studio, klik kanan proyek → **Manage NuGet Packages** → cari “Aspose.OCR” dan instal versi stabil terbaru.

---

## Langkah 1 – Instal Aspose OCR dan buat mesin

Pertama kita memerlukan instance mesin OCR. Kelas `OcrEngine` adalah titik masuk untuk semua operasi.

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;

// Create an OCR engine – this object holds all settings and results
var ocrEngine = new OcrEngine();
```

> **Mengapa ini penting:** Mesin mengenkapsulasi paket bahasa, data gambar, dan opsi pengenalan. Membuatnya satu kali dan menggunakannya kembali pada banyak gambar dapat meningkatkan kinerja.

---

## Langkah 2 – **memuat gambar untuk ocr** dan mengatur bahasa

Sekarang kita memberi tahu mesin gambar mana yang akan diproses dan bahasa apa yang dicari. Menetapkan `Language.Cyrillic` secara otomatis mengunduh paket bahasa yang diperlukan pada kali pertama dijalankan.

```csharp
// 1️⃣ Load the PNG that contains Cyrillic text
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/cyrillic_sample.png");

// 2️⃣ Tell Aspose we want to read Cyrillic characters
ocrEngine.Settings.Language = Language.Cyrillic;   // downloads pack if missing
```

> **Kasus khusus:** Jika PNG Anda sangat besar (lebih dari 5 MB) Anda mungkin ingin mengubah ukurannya terlebih dahulu untuk mempercepat pengenalan. Properti `Image` juga menerima `Stream`, sehingga Anda dapat memuat dari memori, permintaan web, atau Azure Blob tanpa menyentuh sistem file.

---

## Langkah 3 – **mengonversi gambar menjadi teks** dengan satu panggilan

Pengenalan semudah memanggil `Recognize()`. Setelah panggilan ini properti `Text` berisi string yang diekstrak.

```csharp
// Run the OCR engine – this does the heavy lifting
ocrEngine.Recognize();

// Grab the result; it’s plain Unicode text
string extractedText = ocrEngine.Text;
```

> **Apa yang terjadi di balik layar?** Aspose menjalankan classifier berbasis jaringan saraf yang dilatih dengan jutaan glif Cyrillic. Perpustakaan menyederhanakan semua kompleksitas itu, sehingga Anda mendapatkan Unicode yang bersih.

---

## Langkah 4 – Keluarkan hasil (atau alirkan ke tempat lain)

Untuk tujuan demo kami akan mencetak teks ke konsol, tetapi Anda dapat dengan mudah menuliskannya ke file, basis data, atau mengirimkannya ke indeks pencarian.

```csharp
// Show the OCR result in the console
Console.WriteLine("=== Recognized Cyrillic Text ===");
Console.WriteLine(extractedText);
```

**Output yang diharapkan** (asumsi `cyrillic_sample.png` berisi frasa “Привет мир”):

```
=== Recognized Cyrillic Text ===
Привет мир
```

Jika output terlihat berantakan, periksa kembali bahwa gambar jelas dan Anda telah mengatur `Language.Cyrillic`. Mesin secara default menggunakan bahasa Inggris, yang akan memperlakukan karakter Cyrillic sebagai simbol tidak dikenal.

---

## Langkah 5 – Contoh lengkap yang dapat dijalankan

Menggabungkan semuanya, berikut program mandiri yang dapat Anda salin‑tempel ke proyek konsol baru.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Create the OCR engine
        // -------------------------------------------------
        var ocrEngine = new OcrEngine();

        // -------------------------------------------------
        // 2️⃣ Load the PNG and select Cyrillic language
        // -------------------------------------------------
        // Replace the path with the location of your PNG
        ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/cyrillic_sample.png");
        ocrEngine.Settings.Language = Language.Cyrillic; // auto‑downloads pack

        // -------------------------------------------------
        // 3️⃣ Perform recognition
        // -------------------------------------------------
        ocrEngine.Recognize();

        // -------------------------------------------------
        // 4️⃣ Output the extracted text
        // -------------------------------------------------
        Console.WriteLine("=== Recognized Cyrillic Text ===");
        Console.WriteLine(ocrEngine.Text);
    }
}
```

Simpan file sebagai `Program.cs`, jalankan `dotnet run`, dan Anda akan melihat teks Cyrillic tercetak.

---

## Pertanyaan umum & pemecahan masalah

| Pertanyaan | Jawaban |
|------------|---------|
| **Bagaimana jika paket bahasa tidak terunduh?** | Pastikan mesin memiliki akses internet. Paket disimpan dalam `%USERPROFILE%\.Aspose\OCR\Languages`. Menghapus folder tersebut memaksa unduhan ulang. |
| **Bisakah saya membaca bahasa lain selain Cyrillic?** | Tentu – ganti `Language.Cyrillic` dengan `Language.English`, `Language.Arabic`, dll. Logika unduhan otomatis tetap berlaku. |
| **PNG saya berisik – hasilnya buruk. Apa yang dapat saya lakukan?** | Praproses gambar: tingkatkan kontras, ubah ke skala abu‑abu, atau terapkan filter median. Aspose OCR juga menyediakan opsi `Settings.ImagePreprocess`. |
| **Apakah ada cara mendapatkan kotak pembatas untuk setiap kata?** | Ya, setelah `Recognize()` Anda dapat memeriksa `ocrEngine.Regions` yang mengembalikan persegi panjang untuk setiap kata yang terdeteksi. |
| **Apakah saya memerlukan lisensi untuk penggunaan produksi?** | Evaluasi gratis berlaku hingga 100 halaman. Untuk proyek komersial beli lisensi – menghilangkan watermark evaluasi dan membuka pemrosesan batch berkecepatan tinggi. |

---

## Langkah selanjutnya – memperluas solusi

* **Pemrosesan batch:** Loop melalui folder PNG, kumpulkan semua teks ke file CSV.  
* **Integrasi dengan Azure Cognitive Search:** Indeks string Cyrillic yang diekstrak untuk pencarian cepat.  
* **Menggabungkan dengan konversi PDF:** Gunakan Aspose.PDF untuk mengonversi PDF yang dipindai menjadi PNG terlebih dahulu, lalu jalankan alur OCR yang sama.  

Semua skenario tersebut menggunakan pola inti yang baru saja kami bahas: **memuat gambar untuk OCR → mengatur bahasa → mengenali → menggunakan teks**.

---

## Kesimpulan

Anda kini tahu cara **membaca teks dari png**, **mengekstrak teks Cyrillic**, dan **mengonversi gambar menjadi teks** dengan Aspose OCR di C#. Langkah‑langkah kuncinya adalah membuat mesin, memuat gambar, memilih bahasa yang tepat (yang secara otomatis **mengunduh paket bahasa Cyrillic**), dan akhirnya memanggil `Recognize()`.

Cobalah dengan gambar yang berbeda, bereksperimen dengan opsi `Settings`, dan saksikan aplikasi Anda menjadi dapat dicari, multibahasa, dan jauh lebih cerdas.  

Selamat coding, dan jangan ragu meninggalkan komentar jika Anda mengalami kendala!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}