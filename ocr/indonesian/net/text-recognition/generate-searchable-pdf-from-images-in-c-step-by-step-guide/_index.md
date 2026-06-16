---
category: general
date: 2026-02-22
description: Hasilkan PDF yang dapat dicari dan ekstrak teks dari gambar menggunakan
  Aspose OCR. Pelajari cara mengonversi gambar ke PDF dan menghasilkan teks biasa
  dalam satu tutorial.
draft: false
keywords:
- generate searchable pdf
- extract text from image
- convert image to pdf
- output plain text
- convert scanned image pdf
language: id
og_description: Buat PDF yang dapat dicari dari gambar yang dipindai dengan Aspose
  OCR. Panduan ini menunjukkan cara mengekstrak teks dari gambar, menghasilkan teks
  biasa, dan mengonversi gambar menjadi PDF.
og_title: Buat PDF yang Dapat Dicari dari Gambar – Tutorial C# Lengkap
tags:
- C#
- OCR
- PDF generation
- Aspose
title: Buat PDF yang Dapat Dicari dari Gambar di C# – Panduan Langkah demi Langkah
url: /id/net/text-recognition/generate-searchable-pdf-from-images-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hasilkan PDF yang Dapat Dicari dari Gambar dalam C# – Tutorial Lengkap

Pernahkah Anda perlu **menghasilkan PDF yang dapat dicari** dari gambar yang dipindai tetapi tidak yakin harus mulai dari mana? Anda tidak sendirian—banyak pengembang mengalami kebuntuan saat pertama kali bertemu OCR. Kabar baik? Dengan Aspose OCR Anda dapat **mengekstrak teks dari gambar**, **menghasilkan teks biasa**, dan **mengonversi gambar ke PDF** hanya dalam beberapa baris C#.

Dalam panduan ini kami akan membahas seluruh proses, mulai dari memuat file PNG hingga menyimpan PDF yang dapat dicari dan file teks biasa. Pada akhir tutorial Anda akan memiliki potongan kode yang dapat digunakan kembali dan dapat dimasukkan ke proyek .NET mana pun. Tanpa basa‑basi, hanya hal-hal yang menyelesaikan pekerjaan.

## Apa yang Akan Anda Pelajari

- Cara menyiapkan **Aspose.OCR** dalam aplikasi konsol .NET.  
- Perbedaan antara mode **output plain text** dan **searchable PDF**.  
- Cara **extract text from image** dan menuliskannya ke file `.txt`.  
- Cara **convert image to PDF** yang mempertahankan bitmap asli sambil menambahkan lapisan teks tersembunyi.  
- Tips untuk menangani batch besar, jebakan umum, dan tempat menyesuaikan pengaturan untuk akurasi yang lebih baik.

> **Prerequisites** – Anda memerlukan .NET 6+ (atau .NET Framework 4.7+), Visual Studio 2022 (atau editor apa pun), dan lisensi Aspose OCR (atau percobaan gratis). Tidak diperlukan pustaka pihak ketiga lainnya.

![generate searchable pdf example](image-placeholder.png "Example of a generated searchable PDF")

## Langkah 1: Instal Aspose OCR dan Buat Engine

Pertama-tama—tambahkan paket NuGet ke proyek Anda:

```bash
dotnet add package Aspose.OCR
```

Sekarang kita dapat memulai OCR engine dan memberi tahu bahasa yang digunakan. Bahasa Inggris adalah default, tetapi Anda dapat beralih ke bahasa Perancis, Spanyol, dll., dengan mengubah enum `Language`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System.IO;

class Program
{
    static void Main()
    {
        // Initialize the OCR engine for English
        OcrEngine ocrEngine = new OcrEngine { Language = Language.English };
```

**Why this matters:** Engine menyimpan semua konfigurasi—bahasa, format output, dan flag pra‑pemrosesan opsional. Mengaturnya sekali dan menggunakannya kembali menghindari beban membuat instance baru untuk setiap file.

## Langkah 2: Ekstrak Teks dan Simpan sebagai Teks Biasa

Jika Anda hanya membutuhkan karakter mentah, ubah engine ke `OutputFormat.Text`. Ini memberi tahu Aspose OCR untuk melewatkan pembuatan PDF sepenuhnya dan memberikan Anda sebuah string.

```csharp
        // Tell the engine to return plain text
        ocrEngine.OutputFormat = OutputFormat.Text;

        // Path to your source image (PNG, JPEG, BMP, etc.)
        string inputImagePath = @"YOUR_DIRECTORY/input.png";

        // Perform recognition – the result contains the extracted string
        OcrResult plainTextResult = ocrEngine.Recognize(Image.Load(inputImagePath));

        // Write the text to a .txt file
        string textOutputPath = @"YOUR_DIRECTORY/output.txt";
        File.WriteAllText(textOutputPath, plainTextResult.Text);
```

**Pro tip:** `plainTextResult.Text` sudah menghapus jeda baris yang merupakan bagian dari tata letak OCR. Jika Anda membutuhkan spasi asli, periksa `plainTextResult.TextBlocks` sebagai gantinya.

### Hasil yang Diharapkan

Buka `output.txt` dan Anda akan melihat sesuatu seperti:

```
Hello, world!
This is a sample scanned document.
```

Itulah bagian **output plain text** dari tutorial—cepat, ringan, dan sempurna untuk pemrosesan lanjutan (mis., pengindeksan).

## Langkah 3: Beralih ke Mode Searchable PDF

Sekarang mari buat **searchable PDF**. Engine akan menyematkan bitmap asli dan menambahkan lapisan teks yang dihasilkan OCR di bawahnya, membuat dokumen dapat dicari di semua penampil PDF.

```csharp
        // Change the output format to searchable PDF
        ocrEngine.OutputFormat = OutputFormat.SearchablePdf;

        // Recognize the same image again – this time we get PDF bytes
        OcrResult pdfResult = ocrEngine.Recognize(Image.Load(inputImagePath));

        // Save the PDF bytes to a file
        string pdfOutputPath = @"YOUR_DIRECTORY/output.pdf";
        File.WriteAllBytes(pdfOutputPath, pdfResult.RawData);
    }
}
```

**Why we re‑recognize:** Engine OCR menyimpan cache gambar terakhir, tetapi format output menentukan data apa yang dikembalikan. Mengubah format memaksa proses baru yang menyertakan lapisan teks tersembunyi.

### Seperti Apa PDF-nya

Buka `output.pdf` di Adobe Reader atau penampil apa pun dan coba pilih teks. Anda akan melihat bahwa Anda dapat menyalin, mencari, dan menyorot konten—meskipun tampilan visualnya masih bitmap asli. Itu adalah ciri khas **convert scanned image pdf**.

## Langkah 4: Menangani Banyak File (Opsional)

Proyek dunia nyata jarang hanya menangani satu gambar. Di bawah ini ada loop cepat yang memproses setiap PNG dalam folder, menghasilkan file `.txt` dan `.pdf` yang cocok.

```csharp
        string folder = @"YOUR_DIRECTORY";
        foreach (var file in Directory.GetFiles(folder, "*.png"))
        {
            // Plain‑text extraction
            ocrEngine.OutputFormat = OutputFormat.Text;
            var txtResult = ocrEngine.Recognize(Image.Load(file));
            File.WriteAllText(Path.ChangeExtension(file, ".txt"), txtResult.Text);

            // Searchable PDF generation
            ocrEngine.OutputFormat = OutputFormat.SearchablePdf;
            var pdfResult = ocrEngine.Recognize(Image.Load(file));
            File.WriteAllBytes(Path.ChangeExtension(file, ".pdf"), pdfResult.RawData);
        }
```

**Edge case note:** Gambar besar dapat menghabiskan memori. Jika Anda mengalami `OutOfMemoryException`, pertimbangkan untuk memperkecil ukuran dengan `Image.Resize` sebelum pengenalan, atau proses file dalam batch yang lebih kecil.

## Langkah 5: Menyetel Akurasi OCR

Aspose OCR menawarkan beberapa pengaturan yang dapat Anda ubah:

| Setting | What it does | When to use |
|---------|--------------|-------------|
| `ocrEngine.PageSegmentationMode` | Mengontrol bagaimana engine memisahkan gambar menjadi blok teks. | Berguna untuk tata letak multi‑kolom. |
| `ocrEngine.Deskew` | Memutar otomatis halaman yang sedikit miring. | Dokumen yang dipindai tidak sepenuhnya rata. |
| `ocrEngine.RemoveNoise` | Mencoba membersihkan bintik‑bintik dan artefak latar belakang. | Scan berkualitas rendah atau halaman faks. |

Example:

```csharp
ocrEngine.Deskew = true;
ocrEngine.RemoveNoise = true;
```

Mengaktifkan opsi-opsi ini dapat meningkatkan waktu pemrosesan, tetapi peningkatan kualitas **extract text from image** sering kali sepadan.

## Langkah 6: Memverifikasi Output Secara Programatik

Kadang‑kadang Anda perlu memastikan bahwa PDF benar‑benar berisi teks yang dapat dicari (mis., dalam pengujian otomatis). Pemeriksaan termudah adalah memverifikasi bahwa array byte PDF tidak kosong dan bahwa panjang `RawData` melebihi ukuran gambar.

```csharp
if (pdfResult.RawData.Length > Image.Load(inputImagePath).Data.Length)
{
    Console.WriteLine("Searchable PDF generated successfully!");
}
else
{
    Console.WriteLine("Warning: PDF may not contain hidden text.");
}
```

Untuk validasi yang lebih mendalam, Anda dapat menggunakan pustaka PDF (seperti iTextSharp) untuk mengekstrak aliran teks dan membandingkannya dengan `plainTextResult.Text`.

## Kesalahan Umum & Cara Menghindarinya

- **Missing License** – Tanpa lisensi Aspose yang valid, pustaka berjalan dalam mode evaluasi, menambahkan watermark pada PDF. Daftarkan lisensi Anda lebih awal (`License license = new License(); license.SetLicense("Aspose.OCR.lic");`).  
- **Incorrect Path** – Menuliskan path absolut secara keras berfungsi di mesin Anda tetapi gagal di tempat lain. Gunakan `Path.Combine` dengan `AppDomain.CurrentDomain.BaseDirectory` untuk portabilitas.  
- **Unsupported Image Formats** – GIF dan TIFF dengan banyak frame memerlukan penanganan khusus (`Image.LoadMultiPage`). Konversi terlebih dahulu ke PNG/JPEG jika Anda hanya membutuhkan halaman pertama.  
- **Performance Bottlenecks** – Membuat ulang `OcrEngine` di dalam loop memakan biaya. Pertahankan satu instance dan hanya ubah `OutputFormat` seperti yang ditunjukkan.

## Ringkasan

Kami telah membahas seluruh alur kerja untuk **generate searchable PDF** dari gambar yang dipindai menggunakan Aspose OCR:

1. Instal paket NuGet dan buat `OcrEngine`.  
2. Set `OutputFormat.Text` ke **output plain text** dan tulis ke file `.txt`.  
3. Ubah ke `OutputFormat.SearchablePdf` untuk **convert image to PDF** dengan lapisan teks tak terlihat.  
4. Simpan byte PDF dan opsional lakukan loop pada direktori untuk pemrosesan batch.  
5. Setel akurasi dengan deskew, penghapusan noise, dan opsi segmentasi halaman.  

Semua itu masuk dalam program yang ringkas dan mandiri yang dapat Anda salin‑tempel ke Visual Studio.

## Apa yang Bisa Dicoba Selanjutnya?

- **Batch processing** dengan antarmuka UI (WinForms atau WPF) sehingga pengguna dapat menyeret‑dan‑menjatuhkan file.  
- **Language detection** – Aspose OCR dapat mendeteksi bahasa secara otomatis; coba `ocrEngine.Language = Language.AutoDetect`.  
- **Post‑processing** – Masukkan teks yang diekstrak ke indeks pencarian (ElasticSearch, Azure Cognitive Search) untuk pengambilan dokumen secara instan.  
- **Alternative outputs** – Gunakan `OutputFormat.Hocr` untuk hasil OCR berbasis HTML, berguna untuk pratinjau web.

Silakan bereksperimen dengan resolusi gambar yang berbeda, mode warna, dan pengaturan OCR. Semakin banyak Anda mencoba, semakin baik Anda akan memahami kompromi antara kecepatan dan akurasi.

---

**Happy coding!** Jika Anda menemukan kejanggalan, tinggalkan komentar di bawah atau periksa dokumentasi Aspose OCR untuk penjelasan lebih mendalam. Proyek Anda berikutnya—apakah itu penagihan, pengarsipan, atau membangun basis pengetahuan yang dapat dicari—baru saja menjadi jauh lebih mudah.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}