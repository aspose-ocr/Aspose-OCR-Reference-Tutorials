---
category: general
date: 2026-03-07
description: Kenali teks dari gambar dengan cepat menggunakan Aspose OCR. Pelajari
  cara mengonversi djvu ke teks, mengekstrak teks dari gambar, dan memuat gambar untuk
  OCR dalam tutorial C# langkah demi langkah.
draft: false
keywords:
- recognize text from image
- convert djvu to text
- how to extract text from image
- extract text from djvu
- load image for OCR
language: id
og_description: Mengenali teks dari gambar di C# menggunakan Aspose OCR. Panduan ini
  menunjukkan cara mengonversi DJVU ke teks, mengekstrak teks dari gambar, dan memuat
  gambar untuk OCR dengan tips praktis.
og_title: Mengenali teks dari gambar – Tutorial Lengkap OCR Aspose C#
tags:
- C#
- Aspose OCR
- Document Processing
title: Mengenali Teks dari Gambar di C# – Panduan Lengkap Aspose OCR
url: /id/net/text-recognition/recognize-text-from-image-in-c-complete-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# mengenali teks dari gambar – Tutorial Lengkap C# Aspose OCR

Pernah membutuhkan untuk **recognize text from image** tetapi tidak yakin perpustakaan mana yang memberikan hasil yang dapat diandalkan? Anda tidak sendirian. Baik Anda menangani faktur yang dipindai, file DJVU bersejarah, atau screenshot PNG sederhana, mengekstrak karakter yang tepat dapat terasa seperti memecahkan skrip kuno.

Begini—Aspose OCR membuat seluruh proses menjadi sangat mudah. Dalam panduan ini kami akan menjelaskan cara **convert djvu to text**, **extract text from image**, dan **load image for OCR** menggunakan program C# yang ringkas. Pada akhir tutorial Anda akan memiliki aplikasi console yang dapat dijalankan yang mencetak string yang dikenali ke konsol, dan Anda akan memahami “mengapa” di balik setiap baris.

## Apa yang Akan Anda Pelajari

- Cara menyiapkan mesin Aspose OCR dalam proyek .NET.  
- Kode tepat yang diperlukan untuk **load image for OCR** dari file DJVU.  
- Mengapa Anda harus memanggil `Recognize()` sebelum membaca `Text`.  
- Jebakan umum (DJVU multi‑halaman, format tidak didukung) dan cara menghindarinya.  
- Cara cepat untuk **convert djvu to text** untuk pemrosesan batch.

Yang Anda perlukan hanyalah .NET SDK terbaru (≥ 6.0) dan lisensi Aspose OCR (versi percobaan gratis cukup untuk pengujian). Tanpa layanan eksternal, tanpa panggilan REST—hanya C# murni.

## Prasyarat

| Persyaratan | Alasan |
|-------------|--------|
| .NET 6 SDK atau lebih baru | Fitur bahasa modern dan kinerja yang lebih baik. |
| Paket NuGet Aspose.OCR (`Install-Package Aspose.OCR`) | Menyediakan kelas `OcrEngine` yang akan kami gunakan. |
| File DJVU (mis., `sample.djvu`) | Menunjukkan **convert djvu to text**. |
| Pemahaman dasar tentang aplikasi console C# | Membuat langkah‑langkah mengalir secara alami. |

Jika ada yang belum ada, berhentilah sejenak dan instal sekarang; jika tidak, kode tidak akan dapat dikompilasi.

## Langkah 1 – Instal Aspose.OCR dan Buat Proyek

Pertama, buat proyek console baru dan tambahkan pustaka OCR.

```bash
dotnet new console -n OcrDemo
cd OcrDemo
dotnet add package Aspose.OCR
```

*Tip profesional:* Gunakan flag `--framework net6.0` jika Anda ingin mengunci target framework secara eksplisit.

## Langkah 2 – Inisialisasi Mesin OCR dan Muat Gambar DJVU

Mesin membutuhkan sumber gambar. Aspose.OCR dapat membaca banyak format, termasuk DJVU, jadi kami cukup menunjuk ke jalur file.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Image;

// Step 2: Create the OCR engine instance
var ocrEngine = new OcrEngine();

// Load the DJVU file – the first page is used by default
// This demonstrates “load image for OCR” and also “convert djvu to text”
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/input.djvu");
```

**Mengapa ini penting:**  
- `OcrEngine` adalah titik masuk; membuatnya sekali dan menggunakannya kembali mengurangi beban memori.  
- `ImageStream.FromFile` mengabstraksi format file, sehingga Anda dapat mengganti file DJVU dengan PNG atau TIFF nanti tanpa mengubah kode lain—sempurna untuk “how to extract text from image” dalam berbagai skenario.

## Langkah 3 – Jalankan Proses Pengenalan

Memanggil `Recognize()` memicu proses berat. Di balik layar Aspose menjalankan classifier berbasis jaringan saraf yang bekerja pada teks cetak maupun tulisan tangan.

```csharp
// Step 3: Perform OCR on the loaded image
ocrEngine.Recognize();
```

*Catatan kasus tepi:* Jika DJVU Anda berisi beberapa halaman, `ImageStream.FromFile` tetap hanya memuat halaman pertama. Untuk memproses semua halaman Anda harus melakukan loop pada `ImageStream.FromFile(...).Pages`. Untuk kebanyakan tugas cepat, halaman pertama sudah cukup.

## Langkah 4 – Ambil dan Tampilkan Teks yang Dikenali

Setelah pengenalan, mesin mengisi properti `Text` dengan string teks biasa. Anda kini dapat menuliskannya ke konsol, file, atau mengirimnya ke sistem lain.

```csharp
// Step 4: Get the OCR result
string recognizedText = ocrEngine.Text;

// Output the result
Console.WriteLine("=== Recognized Text ===");
Console.WriteLine(recognizedText);
```

Output tipikal terlihat seperti:

```
=== Recognized Text ===
This is a sample DJVU page.
It contains several lines of text,
including numbers like 12345.
```

Jika output terlihat berantakan, periksa kembali bahwa gambar sumber tidak beresolusi rendah; Aspose merekomendasikan 300 dpi atau lebih tinggi untuk akurasi terbaik.

## Contoh Lengkap yang Berfungsi

Menggabungkan semuanya, berikut satu file (`Program.cs`) yang dapat Anda tempel ke dalam proyek yang dibuat sebelumnya.

```csharp
// Program.cs
using System;
using Aspose.OCR;
using Aspose.OCR.Image;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create OCR engine
            var ocrEngine = new OcrEngine();

            // 2️⃣ Load the DJVU file (first page only)
            // Replace the path with your actual file location
            ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/input.djvu");

            // 3️⃣ Run the recognition
            ocrEngine.Recognize();

            // 4️⃣ Retrieve and print the text
            string recognizedText = ocrEngine.Text;

            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(recognizedText);
        }
    }
}
```

Jalankan dengan:

```bash
dotnet run
```

Anda akan melihat string yang diekstrak tercetak di terminal. Ini adalah cara paling sederhana untuk **recognize text from image** menggunakan Aspose OCR.

## Langkah 5 – Lanjutan: Mengonversi Beberapa Halaman DJVU ke File Teks

Jika Anda perlu **convert djvu to text** secara massal, perpanjang kode sebelumnya dengan loop:

```csharp
var djvuPath = @"YOUR_DIRECTORY/multi_page.djvu";
var stream = ImageStream.FromFile(djvuPath);

for (int i = 0; i < stream.PageCount; i++)
{
    ocrEngine.Image = stream.GetPage(i);
    ocrEngine.Recognize();

    var pageText = ocrEngine.Text;
    System.IO.File.WriteAllText(
        $"page_{i + 1}.txt",
        pageText);
}
```

*Mengapa ini berhasil:* `GetPage(i)` mengembalikan objek `Image` untuk halaman yang diminta, memungkinkan Anda menggunakan kembali instance `OcrEngine` yang sama. Teks setiap halaman disimpan dalam file `.txt` masing‑masing, memberikan pipeline **convert djvu to text** yang bersih.

## Pertanyaan Umum & Hal-hal yang Perlu Diwaspadai

- **Bisakah saya mengekstrak teks dari JPEG alih-alih DJVU?**  
  Tentu saja. Cukup ubah ekstensi file di `FromFile`. Kode yang sama **how to extract text from image** berlaku karena Aspose mengabstraksi formatnya.

- **Bagaimana jika hasil OCR mengandung baris baru berlebih?**  
  Gunakan `String.Replace("\r\n", " ")` atau ekspresi reguler untuk menormalkan spasi putih.

- **Apakah saya memerlukan lisensi untuk penggunaan produksi?**  
  Versi percobaan gratis berlaku hingga 100 halaman. Untuk penggunaan tak terbatas, beli lisensi dan panggil `License license = new License(); license.SetLicense("Aspose.OCR.lic");` sebelum membuat engine.

- **Apakah engine ini thread‑safe?**  
  Tidak. Buat `OcrEngine` terpisah per thread atau lindungi akses dengan kunci (lock).

## Tips untuk Akurasi Lebih Baik

1. **Tingkatkan DPI** – Jika Anda mengontrol konversi sumber, keluarkan gambar pada 300 dpi atau lebih tinggi.  
2. **Pra‑proses gambar** – Binarisasi sederhana (`ocrEngine.Image = ImageProcessing.Binarize(ocrEngine.Image)`) dapat meningkatkan hasil pada pemindaian yang berisik.  
3. **Tentukan bahasa** – `ocrEngine.Language = Language.English;` mempersempit set karakter dan mempercepat pengenalan.

## Kesimpulan

Anda kini memiliki contoh lengkap yang siap dijalankan untuk **recognize text from image** menggunakan Aspose OCR, dan Anda telah melihat cara **convert djvu to text**, **how to extract text from image**, serta cara yang tepat untuk **load image for OCR**. Kode ini mandiri, berfungsi pada runtime .NET 6+ apa pun, dan dapat diperluas untuk memproses batch dokumen DJVU multi‑halaman.

Selanjutnya, Anda mungkin ingin menjelajahi:

- Menambahkan **language detection** untuk file DJVU multibahasa.  
- Mengintegrasikan output OCR dengan indeks pencarian (mis., Elasticsearch).  
- Menggunakan konversi PDF Aspose untuk mengubah teks yang diekstrak menjadi PDF yang dapat dicari.

Cobalah, sesuaikan DPI, bereksperimen dengan format gambar yang berbeda, dan biarkan mesin OCR melakukan pekerjaan berat untuk Anda. Selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}