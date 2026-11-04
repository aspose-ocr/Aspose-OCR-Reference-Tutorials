---
category: general
date: 2026-02-28
description: Buat PDF yang dapat dicari dari file TIFF multi‑halaman menggunakan C#.
  Panduan ini menunjukkan cara mengonversi gambar menjadi PDF yang dapat dicari dengan
  contoh OCR lengkap dalam C#.
draft: false
keywords:
- create searchable pdf
- image to searchable pdf
- convert tiff to pdf
- c# ocr example
- c# image to pdf
language: id
og_description: Buat PDF yang dapat dicari dari file TIFF menggunakan Aspose.OCR.
  Ikuti contoh OCR C# langkah demi langkah ini untuk mengubah gambar menjadi PDF yang
  dapat dicari.
og_title: Buat PDF yang Dapat Dicari di C# – Gambar ke PDF OCR
tags:
- OCR
- PDF
- C#
- Aspose
title: Buat PDF yang Dapat Dicari di C# – Gambar ke PDF OCR
url: /id/net/text-recognition/create-searchable-pdf-in-c-image-to-pdf-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat PDF yang Dapat Dicari di C# – Gambar ke PDF OCR

Pernah perlu **membuat PDF yang dapat dicari** dari dokumen yang dipindai tetapi tidak yakin harus mulai dari mana? Anda bukan satu-satunya. Dalam banyak alur kerja kantor, PDF yang dapat dicari adalah perbedaan antara file yang buntu dan arsip yang dapat dicari.  

Dalam tutorial ini kami akan membahas contoh **c# ocr example** lengkap yang mengubah TIFF multi‑halaman menjadi PDF yang dapat dicari, semuanya dengan Aspose.OCR. Pada akhir tutorial Anda akan tahu persis cara **image to searchable pdf**, cara **convert tiff to pdf**, dan Anda akan memiliki potongan kode siap‑jalankan yang dapat Anda masukkan ke proyek .NET mana pun.

## Apa yang Akan Anda Pelajari

* Cara menginstal dan merujuk Aspose.OCR dalam proyek C#.
* Langkah tepat untuk memuat TIFF, mengatur bahasa, dan memanggil `RecognizeToPdf`.
* Mengapa setiap langkah penting – mulai dari penanganan memori hingga pemilihan bahasa.
* Tips untuk menangani dokumen besar, memecahkan masalah umum OCR, dan memperluas solusi ke format gambar lain.

**Prerequisites** – .NET SDK terbaru (4.6+ atau .NET Core 3.1+), Visual Studio (atau IDE favorit Anda), dan lisensi Aspose.OCR (versi percobaan gratis dapat digunakan untuk pengujian). Tidak ada pustaka eksternal lain yang diperlukan.

---

## Membuat PDF yang Dapat Dicari – Ikhtisar

Secara umum prosesnya terlihat seperti ini:

1. **Initialize** `OcrEngine`.  
2. **Load** gambar sumber (TIFF dalam kasus kami).  
3. **Configure** pengaturan bahasa untuk akurasi yang lebih baik.  
4. **Run** OCR dan **save** hasilnya langsung sebagai PDF yang dapat dicari.  

Itu saja. Aspose API melakukan pekerjaan berat, sehingga Anda tidak perlu menggabungkan pustaka OCR dan PDF secara terpisah.

---

## Langkah 1: Instal Aspose.OCR dan Siapkan Proyek Anda

First, add the Aspose.OCR NuGet package:

```bash
dotnet add package Aspose.OCR
```

Or, if you prefer the Package Manager Console in Visual Studio:

```powershell
Install-Package Aspose.OCR
```

After the package restores, open your project file and verify the reference:

```xml
<ItemGroup>
  <PackageReference Include="Aspose.OCR" Version="23.10.0" />
</ItemGroup>
```

> **Pro tip:** Gunakan versi stabil terbaru (periksa situs web Aspose) untuk mendapatkan perbaikan bug dan paket bahasa terbaru.

---

## Langkah 2: Konversi TIFF ke PDF – Memuat Gambar

Sekarang kami akan memuat TIFF yang ingin Anda jadikan dapat dicari. Metode `Image.Load` milik Aspose mendukung TIFF multi‑halaman secara langsung.

```csharp
using Aspose.OCR;
using System.Drawing;

// Load the multi‑page TIFF. Replace the path with your actual file.
using var tiffImage = Image.Load(@"YOUR_DIRECTORY/input.tif");
```

> **Why this matters:** Memuat gambar di dalam blok `using` menjamin sumber daya tak terkelola dilepaskan dengan cepat—penting saat memproses dokumen besar.

---

## Langkah 3: Gambar ke PDF yang Dapat Dicari – Konfigurasi Mesin OCR

Sebelum menjalankan OCR, kami akan memberi tahu mesin bahasa apa yang diharapkan. Bahasa Inggris berfungsi untuk kebanyakan kasus, tetapi Anda dapat mengganti dengan nilai enum `OcrLanguage` apa pun.

```csharp
// Create the OCR engine instance
var ocrEngine = new OcrEngine();

// (Optional) Specify language for better accuracy
ocrEngine.Language = OcrLanguage.English;
```

> **Expert note:** Memilih bahasa yang tepat secara dramatis mengurangi kesalahan pengenalan. Jika Anda memiliki bahasa campuran, Anda dapat menggabungkannya dengan operator `|`, misalnya `OcrLanguage.English | OcrLanguage.French`.

---

## Langkah 4: Contoh OCR C# – Kenali dan Simpan

Dengan mesin siap, panggil `RecognizeToPdf`. Metode ini menulis PDF yang dapat dicari langsung ke disk, menyematkan lapisan teks tak terlihat di belakang gambar asli.

```csharp
// Define the output path for the searchable PDF
string outputPdfPath = @"YOUR_DIRECTORY/output.pdf";

// Perform OCR and write the searchable PDF
ocrEngine.RecognizeToPdf(tiffImage, outputPdfPath);
```

Setelah baris ini dijalankan, `output.pdf` akan berisi halaman TIFF asli ditambah lapisan teks tersembunyi yang dapat dicari oleh pembaca PDF mana pun.

---

## Langkah 5: Gambar C# ke PDF – Verifikasi Hasil

Mari pastikan semuanya berhasil. Buka PDF yang dihasilkan di Adobe Reader (atau penampil apa pun) dan coba cari kata yang Anda tahu ada di TIFF sumber.

```csharp
Console.WriteLine("Searchable PDF created at: " + outputPdfPath);
```

Jika pencarian menghasilkan temuan, Anda telah berhasil **create searchable pdf** dari sebuah gambar. Jika tidak, periksa kembali pengaturan bahasa atau kualitas TIFF sumber.

---

## Contoh Kerja Lengkap

Menggabungkan semua bagian, berikut aplikasi konsol mandiri yang dapat Anda kompilasi dan jalankan:

```csharp
using Aspose.OCR;
using System.Drawing;

class SearchablePdfDemo
{
    static void Main()
    {
        // Step 1: Initialize OCR engine
        var ocrEngine = new OcrEngine();

        // Step 2: Load the multi‑page TIFF
        using var tiffImage = Image.Load(@"YOUR_DIRECTORY/input.tif");

        // Step 3: (Optional) Set language for better accuracy
        ocrEngine.Language = OcrLanguage.English;

        // Step 4: Convert the image to a searchable PDF
        string outputPdfPath = @"YOUR_DIRECTORY/output.pdf";
        ocrEngine.RecognizeToPdf(tiffImage, outputPdfPath);

        // Step 5: Inform the user
        System.Console.WriteLine("Searchable PDF created at: " + outputPdfPath);
    }
}
```

**Expected output** (di konsol):

```
Searchable PDF created at: C:\MyFolder\output.pdf
```

Buka `output.pdf` dan Anda seharusnya dapat mengetik kata apa pun dari TIFF asli ke kotak pencarian penampil dan melihat kecocokan yang disorot.

---

![Create searchable PDF example](placeholder-image.png){: .align-center alt="contoh pdf yang dapat dicari"}

*Tangkapan layar di atas menunjukkan PDF yang dapat dicari dibuka di penampil dengan lapisan teks tersembunyi yang aktif.*

---

## Pertanyaan Umum & Kasus Tepi

### Bagaimana jika TIFF saya sangat besar (ratusan halaman)?

Aspose.OCR memproses halaman satu per satu, tetapi Anda masih mungkin mencapai batas memori. Pertimbangkan memproses TIFF dalam batch:

```csharp
for (int i = 0; i < tiffImage.PageCount; i++)
{
    using var singlePage = tiffImage.ExtractPage(i);
    ocrEngine.RecognizeToPdf(singlePage, $"page_{i}.pdf");
}
```

Nanti, gabungkan PDF per‑halaman dengan pustaka PDF (mis., Aspose.PDF).

### Bisakah saya mengeluarkan ke format lain, seperti DOCX yang dapat dicari?

Ya—gunakan `RecognizeToDocument` alih-alih `RecognizeToPdf`. API meniru metode PDF, cukup ubah ekstensi file target.

### Bagaimana cara menangani bahasa selain Bahasa Inggris?

Ganti `OcrLanguage.English` dengan enum yang sesuai, misalnya `OcrLanguage.Spanish`. Anda juga dapat menggabungkan bahasa:

```csharp
ocrEngine.Language = OcrLanguage.English | OcrLanguage.German;
```

### Bagaimana dengan PDF yang dilindungi kata sandi?

Setelah langkah OCR, Anda dapat membuka PDF yang dihasilkan dengan Aspose.PDF dan menerapkan enkripsi:

```csharp
var pdfDoc = new Aspose.Pdf.Document(outputPdfPath);
pdfDoc.Encrypt("ownerPassword", "userPassword", 
    Aspose.Pdf.Permissions.All, Aspose.Pdf.EncryptionAlgorithms.AES256);
pdfDoc.Save(outputPdfPath);
```

---

## Ringkasan

Kami telah membahas semua yang Anda perlukan untuk **create searchable PDF** dari gambar TIFF menggunakan C#. Mulai dari menginstal Aspose.OCR, memuat gambar, mengonfigurasi bahasa, menjalankan OCR, dan akhirnya memverifikasi output yang dapat dicari, Anda kini memiliki **c# ocr example** yang solid yang dapat Anda sesuaikan ke format lain.

Jika Anda siap melangkah lebih jauh, coba:

* **Convert TIFF to PDF** untuk arsip non‑searchable (cukup lewati langkah OCR).  
* Bereksperimen dengan **image to searchable pdf**

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}