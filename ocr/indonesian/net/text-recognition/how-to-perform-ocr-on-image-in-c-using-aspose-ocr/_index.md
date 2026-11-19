---
category: general
date: 2026-10-11
description: Pelajari cara melakukan OCR pada gambar di C# dengan Aspose.OCR, termasuk
  menginstal System.Drawing.Common dan mengekstrak teks dari file JPG.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- perform OCR on image
- extract text from JPG
- recognize text from picture
- load image for OCR
- install System.Drawing.Common package
language: id
lastmod: 2026-10-11
og_description: Lakukan OCR pada gambar di C# menggunakan Aspose.OCR. Panduan ini
  menunjukkan cara menginstal System.Drawing.Common, memuat gambar untuk OCR, dan
  mengekstrak teks dari JPG.
og_image_alt: Screenshot of C# console output displaying recognized text after performing
  OCR on image
og_title: Lakukan OCR pada gambar di C# – panduan langkah demi langkah
schemas:
- author: Aspose
  dateModified: '2026-10-11'
  description: Learn how to perform OCR on image in C# with Aspose.OCR, including
    installing System.Drawing.Common and extracting text from JPG files.
  headline: How to perform OCR on image in C# using Aspose.OCR
  type: TechArticle
tags:
- OCR
- C#
- Aspose
title: Cara melakukan OCR pada gambar di C# menggunakan Aspose.OCR
url: /id/net/text-recognition/how-to-perform-ocr-on-image-in-c-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara melakukan OCR pada gambar di C# menggunakan Aspose.OCR

Jika Anda perlu **melakukan OCR pada file gambar** dalam aplikasi .NET, panduan ini menunjukkan solusi lengkap. Dengan menggunakan Aspose.OCR Anda dapat dengan cepat **mengenali teks dari gambar** seperti JPG dan menampilkan hasilnya di jendela konsol.

Anda akan mempelajari cara:

* **menginstal paket System.Drawing.Common** – perpustakaan yang menyediakan kelas `Image`,
* **memuat gambar untuk OCR** – membaca JPEG atau PNG ke memori,
* mengkonfigurasi model bahasa,
* **melakukan OCR pada gambar** dan akhirnya,
* **mengekstrak teks dari JPG** serta menampilkannya.

Langkah‑langkah ini ditulis untuk .NET 6+, namun juga berfungsi dengan .NET Framework 4.6.1 atau yang lebih baru.

---

## Prasyarat

| Persyaratan | Mengapa penting |
|-------------|----------------|
| .NET 6 SDK (atau .NET Framework 4.6.1+) | Menyediakan runtime untuk aplikasi konsol C#. |
| Visual Studio 2022 (atau IDE apa saja) | Memudahkan penambahan paket NuGet dan menjalankan program. |
| Koneksi internet (hanya saat pertama kali dijalankan) | Aspose.OCR mengunduh modul bahasa secara otomatis. |
| Contoh gambar yang berisi teks Cyrillic atau Latin (misalnya `sample_cyrillic.jpg`) | Digunakan untuk mendemonstrasikan **mengekstrak teks dari JPG**. |

---

## Langkah 1: Instal paket System.Drawing.Common

Paket NuGet `System.Drawing.Common` menyediakan kelas `Image` yang akan Anda **muat gambar untuk OCR**. Buka Package Manager Console dan jalankan:

```powershell
Install-Package System.Drawing.Common
```

> **Tip profesional:** Targetkan `net6.0-windows` atau tambahkan `<UseWindowsForms>true</UseWindowsForms>` ke file proyek jika Anda menemukan peringatan khusus platform pada Linux/macOS.

---

## Langkah 2: Tambahkan paket NuGet Aspose.OCR

Aspose.OCR berisi mesin OCR dan model bahasa. Instal dengan:

```powershell
Install-Package Aspose.OCR
```

Paket ini ringan; data bahasa yang diperlukan (misalnya Cyrillic) diunduh pada pertama kali Anda menetapkan `OcrEngine.Language`.

---

## Langkah 3: Cara memuat gambar untuk OCR

Memuat gambar adalah langkah konkret pertama sebelum Anda dapat **melakukan OCR pada gambar**. Metode `Image.FromFile` membaca format apa pun yang didukung GDI+, termasuk JPG, PNG, BMP, dan TIFF.

```csharp
using System.Drawing; // Requires System.Drawing.Common

// Replace the path with the location of your test picture.
string imagePath = @"YOUR_DIRECTORY/sample_cyrillic.jpg";
Image ocrImage = Image.FromFile(imagePath);
```

*Jika file tidak ada, `FileNotFoundException` akan dilempar – bungkus pemanggilan dalam blok try/catch untuk kode produksi.*

---

## Langkah 4: Konfigurasikan mesin dan **melakukan OCR pada gambar**

Buat instance `OcrEngine`, pilih model bahasa, tetapkan gambar yang telah dimuat, dan panggil `Recognize()`.

```csharp
using Aspose.OCR;

// Step 4: Initialize OCR engine and set language
var ocrEngine = new OcrEngine
{
    // Choose the language you need; Cyrillic is used in this example.
    Language = OcrLanguage.Cyrillic,
    Image = ocrImage
};

// Execute the OCR operation
OcrResult ocrResult = ocrEngine.Recognize();
```

Metode `Recognize()` mengembalikan objek `OcrResult` yang berisi teks yang diekstrak, skor kepercayaan, dan kotak pembatas. Modul bahasa diunduh secara otomatis pada penggunaan pertama, jadi tidak diperlukan file tambahan.

---

## Langkah 5: **Mengekstrak teks dari JPG** dan menampilkannya

Sekarang Anda dapat **mengenali teks dari gambar** dan mengeluarkan hasilnya. Properti `Text` dari `OcrResult` berisi string polos.

```csharp
// Step 5: Output recognized text
Console.WriteLine("Recognized text:");
Console.WriteLine(ocrResult.Text);
```

### Output konsol yang diharapkan

```
Recognized text:
Пример текста на кириллице
```

Jika gambar sumber berisi teks bahasa Inggris, outputnya akan menjadi kalimat bahasa Inggris yang Anda letakkan di gambar.

---

## Kasus khusus dan tip praktik terbaik

| Situasi | Rekomendasi |
|-----------|----------------|
| **Gambar besar ( > 5 MB )** | Ubah ukuran gambar menjadi ≤ 2000 px pada sisi terpanjang sebelum OCR untuk mengurangi penggunaan memori dan meningkatkan kecepatan. |
| **Beberapa bahasa dalam satu gambar** | Panggil `ocrEngine.AddLanguage(OcrLanguage.English)` selain Cyrillic, lalu setel `ocrEngine.Language = OcrLanguage.Multilingual`. |
| **Pemindaian kontras rendah** | Tingkatkan kontras dengan `System.Drawing.Graphics` sebelum mengirim bitmap ke mesin. |
| **Menjalankan di Linux/macOS** | Pastikan dependensi native `libgdiplus` terpasang (`sudo apt-get install -y libgdiplus`). |
| **Pemanggilan OCR berulang** | Gunakan kembali instance `OcrEngine` yang sama dan hanya ganti `ocrEngine.Image` untuk menghindari pemuatan modul berulang. |

---

## Program lengkap yang dapat dijalankan

Berikut adalah aplikasi konsol lengkap yang menggabungkan semua langkah sebelumnya. Salin kode ke proyek konsol C# baru, ganti jalur gambar, dan jalankan.

```csharp
using System;
using System.Drawing;                 // Install System.Drawing.Common if needed
using Aspose.OCR;                     // NuGet package: Aspose.OCR

class Program
{
    static void Main()
    {
        // Step 1: Install System.Drawing.Common (handled via NuGet)
        // Step 2: Install Aspose.OCR (handled via NuGet)

        // Step 3: Load the image that contains the text to be recognized
        // Replace the placeholder with the actual path to your JPG or PNG file.
        string imagePath = @"YOUR_DIRECTORY/sample_cyrillic.jpg";
        Image ocrImage;
        try
        {
            ocrImage = Image.FromFile(imagePath);
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Failed to load image: {ex.Message}");
            return;
        }

        // Step 4: Create the OCR engine and choose the language model
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.Cyrillic, // Change to OcrLanguage.English for Latin scripts
            Image = ocrImage
        };

        // Step 5: Perform OCR on the loaded picture
        OcrResult ocrResult = ocrEngine.Recognize();

        // Step 6: Display the extracted text
        Console.WriteLine("Recognized text:");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Menjalankan program** mencetak string yang dikenali ke konsol, mengonfirmasi bahwa Anda telah berhasil **melakukan OCR pada gambar** dan **mengekstrak teks dari JPG**.

---

## Kesimpulan

Anda kini tahu cara **melakukan OCR pada file gambar** di C# menggunakan Aspose.OCR, mulai dari menginstal paket **System.Drawing.Common** yang diperlukan hingga **memuat gambar untuk OCR**, memilih bahasa yang tepat, dan akhirnya **mengekstrak teks dari JPG**. Contoh end‑to‑end ini memberi Anda dasar yang kuat untuk membangun pipeline pemrosesan dokumen yang lebih canggih, seperti memproses batch folder gambar atau mengintegrasikan OCR ke dalam API web.

### Apa selanjutnya?

* Jelajahi **mengenali teks dari gambar** dalam PDF dengan mengonversi tiap halaman menjadi gambar terlebih dahulu.  
* Bereksperimen dengan properti `OcrEngine` seperti `Resolution`, `Threshold`, dan `MaxProcessingTime` untuk menyempurnakan akurasi pada pemindaian berisik.  
* Gabungkan output OCR dengan perpustakaan pemrosesan bahasa alami untuk secara otomatis mengkategorikan konten yang diekstrak.

Silakan sesuaikan kode untuk format gambar lain, tambahkan penanganan error, atau integrasikan ke dalam aplikasi yang lebih besar. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Extract Text from Image in C# – Complete Aspose OCR Guide](/ocr/english/net/text-recognition/extract-text-from-image-in-c-complete-aspose-ocr-guide/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [How to Perform Image Text Extraction from Stream Using Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}