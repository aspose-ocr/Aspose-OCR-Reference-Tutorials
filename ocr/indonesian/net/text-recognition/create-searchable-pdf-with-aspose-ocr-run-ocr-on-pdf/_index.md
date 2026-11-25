---
category: general
date: 2026-05-28
description: Buat PDF yang dapat dicari menggunakan Aspose OCR di C#. Pelajari cara
  menjalankan OCR pada PDF, mengenali teks PDF, dan mengubah PDF hasil pemindaian
  OCR menjadi PDF yang dapat dicari.
draft: false
keywords:
- create searchable pdf
- run ocr on pdf
- recognize text pdf
- ocr scanned pdf
- aspose ocr pdf
language: id
og_description: Buat PDF yang dapat dicari menggunakan Aspose OCR di C#. Ikuti panduan
  langkah demi langkah ini untuk menjalankan OCR pada PDF, mengenali teks PDF, dan
  menangani file PDF hasil pemindaian OCR.
og_title: Buat PDF yang Dapat Dicari dengan Aspose OCR – Jalankan OCR pada PDF
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: Create searchable PDF using Aspose OCR in C#. Learn how to run OCR
    on PDF, recognize text PDF, and turn an OCR scanned PDF into a searchable PDF.
  headline: Create Searchable PDF with Aspose OCR – Run OCR on PDF
  type: TechArticle
- description: Create searchable PDF using Aspose OCR in C#. Learn how to run OCR
    on PDF, recognize text PDF, and turn an OCR scanned PDF into a searchable PDF.
  name: Create Searchable PDF with Aspose OCR – Run OCR on PDF
  steps:
  - name: Multiple Languages (OCR Scanned PDF)
    text: 'If your source PDF contains both English and Spanish text, combine languages:'
  - name: Password‑Protected PDFs
    text: 'When dealing with secured PDFs, supply the password before calling `Recognize`:'
  - name: Controlling Image Quality
    text: 'Higher DPI yields better OCR results but consumes more memory. Adjust the
      DPI if you notice garbled characters:'
  - name: License vs. Evaluation Mode
    text: 'In evaluation mode a watermark appears on each page. To remove it, apply
      your license before any OCR call:'
  - name: What’s Next?
    text: '- Explore the **aspose ocr pdf** API further: extract plain text, export
      to DOCX, or generate searchable PDFs in bulk. - Combine the searchable PDF output
      with Aspose.PDF to add bookmarks or watermarks. - Experiment with different
      DPI settings or custom OCR dictionaries for niche fonts.'
  type: HowTo
tags:
- Aspose
- OCR
- PDF
- C#
title: Buat PDF yang Dapat Dicari dengan Aspose OCR – Jalankan OCR pada PDF
url: /id/net/text-recognition/create-searchable-pdf-with-aspose-ocr-run-ocr-on-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Membuat PDF yang Dapat Dicari dengan Aspose OCR – Jalankan OCR pada PDF

Pernahkah Anda perlu **membuat PDF yang dapat dicari** dari sekumpulan dokumen yang dipindai? Anda tidak sendirian. Dalam banyak alur kerja kantor, satu‑satunya hal yang menghalangi Anda memiliki arsip yang sepenuhnya dapat dicari hanyalah beberapa baris kode yang menjalankan OCR pada halaman PDF.  

Dalam tutorial ini kami akan menelusuri contoh lengkap yang siap dijalankan yang menunjukkan secara tepat cara **membuat PDF yang dapat dicari** menggunakan pustaka Aspose OCR untuk .NET. Pada akhir tutorial Anda akan tahu cara *menjalankan OCR pada PDF*, *mengenali teks PDF*, dan mengubah *PDF yang dipindai dengan OCR* menjadi versi yang dapat dicari tanpa layanan pihak ketiga apa pun.

> **Prasyarat** – .NET SDK terbaru (disarankan 6.0+), lisensi Aspose.OCR untuk .NET yang valid (atau kunci evaluasi sementara), dan sebuah PDF yang ingin Anda proses.

![Create searchable PDF diagram](alt="Diagram illustrating the create searchable pdf workflow using Aspose OCR")  

---

## Apa yang Dibahas dalam Panduan Ini

- Menyiapkan pustaka Aspose OCR dalam proyek C#.  
- Memuat PDF sumber (dengan jumlah halaman berapa pun).  
- Mengonfigurasi mesin agar menghasilkan **PDF yang dapat dicari**.  
- Menjalankan proses OCR dan menyimpan hasilnya.  
- Tips untuk menangani dokumen multi‑halaman, pemilihan bahasa, dan jebakan umum.  

Jika Anda mengikuti setiap langkah, Anda akan mendapatkan file yang dapat dibuka di Adobe Reader, menekan **Ctrl + F**, dan langsung mencari kata apa pun yang muncul dalam pemindaian asli.

---

## Langkah 1: Instal Aspose OCR untuk .NET

Sebelum menulis kode apa pun, tambahkan paket NuGet ke proyek Anda:

```bash
dotnet add package Aspose.OCR
```

> **Pro tip:** Gunakan flag `--version` untuk mengunci ke rilis stabil terbaru (misalnya, `Aspose.OCR 23.10`). Ini memastikan kompatibilitas dengan .NET 6 dan yang lebih baru.

---

## Langkah 2: Buat Instance OcrEngine

Inti dari proses ini adalah `OcrEngine`. Anggaplah sebagai otak yang membaca gambar dan menghasilkan teks. Inisialisasinya sangat sederhana:

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

namespace PdfSearchableDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 2: Instantiate the OCR engine
            var ocrEngine = new OcrEngine();
```

Objek `OcrEngine` akan menampung aliran gambar masukan serta konfigurasi yang memberi tahu Aspose bagaimana Anda menginginkan output.

---

## Langkah 3: Muat PDF Sumber (Jalankan OCR pada PDF)

Aspose OCR dapat mengonsumsi PDF secara langsung; ia mengekstrak setiap halaman sebagai gambar secara internal. Ganti jalur placeholder dengan lokasi dokumen yang dipindai:

```csharp
            // Step 3: Load the source PDF – this is where we *run OCR on PDF*
            string inputPath = @"C:\Docs\handbook.pdf";
            ocrEngine.Image = ImageStream.FromFile(inputPath);
```

> **Mengapa ini berhasil:** Metode `ImageStream.FromFile` secara otomatis mendeteksi format PDF dan menyiapkan representasi raster untuk OCR. Tidak diperlukan langkah konversi tambahan.

---

## Langkah 4: Konfigurasikan Format Output dan Bahasa

Di sini kami memberi tahu Aspose apa yang kami inginkan kembali. Menetapkan `OutputFormat` ke `SearchablePdf` memberi instruksi pada mesin untuk menyematkan teks yang dikenali di belakang gambar halaman asli, menghasilkan **PDF yang dapat dicari**. Anda juga dapat memilih bahasa untuk meningkatkan akurasi—bahasa Inggris adalah default, tetapi Anda dapat beralih ke Prancis, Jerman, dll.

```csharp
            // Step 4: Choose output format and language
            ocrEngine.Configuration.OutputFormat = OutputFormat.SearchablePdf; // creates searchable PDF
            ocrEngine.Configuration.Language = Language.English;               // *recognize text PDF* in English
```

Jika Anda perlu memproses dokumen dwibahasa, Anda dapat menggabungkan bahasa menggunakan flag enum `Language`.

---

## Langkah 5: Jalankan Proses OCR – Mengenali Teks PDF

Sekarang pekerjaan berat terjadi. Metode `Recognize` memindai setiap halaman, mengekstrak glif, dan membangun aliran PDF internal yang berisi gambar asli serta lapisan teks tak terlihat. Inilah langkah di mana kami *mengenali teks PDF*.

```csharp
            // Step 5: Execute OCR – this *recognizes text PDF* and builds the searchable stream
            ocrEngine.Recognize();
```

> **Pertanyaan umum:** *Bagaimana jika PDF memiliki 200 halaman?*  
> Mesin memproses halaman secara berurutan dan men-stream hasil, sehingga konsumsi memori tetap wajar. Namun, untuk file yang sangat besar Anda mungkin ingin meningkatkan pengaturan `MemoryLimit` pada `ocrEngine.Configuration`.

---

## Langkah 6: Simpan PDF yang Dapat Dicari

Akhirnya, tulis output ke disk. Metode `Save` menuliskan aliran internal ke file baru yang dapat Anda buka dengan penampil PDF apa pun.

```csharp
            // Step 6: Save the searchable PDF to disk
            string outputPath = @"C:\Docs\handbook_searchable.pdf";
            ocrEngine.Save(outputPath);

            Console.WriteLine($"Searchable PDF created at: {outputPath}");
        }
    }
}
```

Jalankan program (`dotnet run`) dan perhatikan konsol yang mengonfirmasi pembuatan file. Buka `handbook_searchable.pdf` dan coba cari kata yang Anda tahu ada dalam pemindaian asli – Anda akan melihat kecocokan secara instan.

---

## Menangani Kasus Tepi dan Skenario Lanjutan

### Banyak Bahasa (OCR Scanned PDF)

Jika PDF sumber Anda berisi teks dalam bahasa Inggris dan Spanyol, gabungkan bahasa:

```csharp
ocrEngine.Configuration.Language = Language.English | Language.Spanish;
```

Aspose OCR akan beralih kamus secara dinamis, meningkatkan akurasi untuk dokumen berbahasa campuran.

### PDF yang Dilindungi Kata Sandi

Saat menangani PDF yang diamankan, berikan kata sandi sebelum memanggil `Recognize`:

```csharp
ocrEngine.Image = ImageStream.FromFile(inputPath, "MySecretPassword");
```

Jika kata sandi salah, `Recognize` akan melempar `InvalidPasswordException`; menanganinya memungkinkan Anda meminta pengguna memasukkan kata sandi yang benar.

### Mengontrol Kualitas Gambar

DPI yang lebih tinggi menghasilkan hasil OCR yang lebih baik tetapi memakan lebih banyak memori. Sesuaikan DPI jika Anda melihat karakter yang kacau:

```csharp
ocrEngine.Configuration.Dpi = 300; // default is 200
```

### Lisensi vs. Mode Evaluasi

Dalam mode evaluasi, watermark muncul pada setiap halaman. Untuk menghilangkannya, terapkan lisensi Anda sebelum pemanggilan OCR apa pun:

```csharp
var license = new License();
license.SetLicense(@"C:\Aspose\Aspose.OCR.lic");
```

---

## Tips Pro untuk Penggunaan Produksi

- **Pemrosesan batch:** Bungkus logika inti dalam loop `foreach` yang mengiterasi daftar PDF. Buang (`Dispose`) `OcrEngine` setelah setiap file untuk membebaskan sumber daya native.  
- **Logging:** Gunakan `ocrEngine.Configuration.Logger` untuk menangkap statistik OCR terperinci (mis., karakter yang dikenali per detik). Ini sangat berharga saat memecahkan masalah akurasi rendah.  
- **Optimasi performa:** Untuk server multi‑core, buat objek `OcrEngine` terpisah per thread; pustaka bersifat thread‑safe bila setiap instance terisolasi.  
- **Penanganan error:** Selalu bungkus `Recognize` dan `Save` dengan blok `try/catch`. Pengecualian umum meliputi `FileNotFoundException`, `OutOfMemoryException`, dan `UnsupportedFormatException`.

---

## Contoh Lengkap yang Siap Pakai (Copy‑Paste)

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

namespace PdfSearchableDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Apply license (optional – removes evaluation watermark)
            // var license = new License();
            // license.SetLicense(@"C:\Aspose\Aspose.OCR.lic");

            // 1️⃣ Create OCR engine
            var ocrEngine = new OcrEngine();

            // 2️⃣ Load PDF – this is where we *run OCR on PDF*
            string inputPath = @"C:\Docs\handbook.pdf";
            ocrEngine.Image = ImageStream.FromFile(inputPath);

            // 3️⃣ Configure output as searchable PDF and set language
            ocrEngine.Configuration.OutputFormat = OutputFormat.SearchablePdf;
            ocrEngine.Configuration.Language = Language.English;

            // 4️⃣ Run OCR – *recognize text PDF*
            ocrEngine.Recognize();

            // 5️⃣ Save the searchable PDF
            string outputPath = @"C:\Docs\handbook_searchable.pdf";
            ocrEngine.Save(outputPath);

            Console.WriteLine($"Searchable PDF created at: {outputPath}");
        }
    }
}
```

**Output yang diharapkan** (konsol):

```
Searchable PDF created at: C:\Docs\handbook_searchable.pdf
```

Buka file yang dihasilkan, tekan **Ctrl + F**, dan Anda akan dapat menemukan kata apa pun yang muncul dalam halaman yang dipindai sebelumnya. Itulah keajaiban mengubah *OCR scanned PDF* menjadi **PDF yang dapat dicari**.

---

## Kesimpulan

Kami baru saja mendemonstrasikan cara **membuat PDF yang dapat dicari** dengan Aspose OCR untuk .NET, mencakup semua hal mulai dari instalasi paket hingga penanganan PDF multi‑bahasa dan yang dilindungi kata sandi. Dengan mengikuti langkah‑langkah ini Anda dapat secara andal *menjalankan OCR pada PDF*, *mengenali teks PDF*, dan mengonversi *OCR scanned PDF* apa pun menjadi aset yang sepenuhnya dapat dicari.

### Apa Selanjutnya?

- Jelajahi lebih jauh API **aspose ocr pdf**: ekstrak teks biasa, ekspor ke DOCX, atau hasilkan PDF yang dapat dicari secara massal.  
- Gabungkan output PDF yang dapat dicari dengan Aspose.PDF untuk menambahkan bookmark atau watermark.  
- Bereksperimen dengan pengaturan DPI yang berbeda atau kamus OCR khusus untuk font khusus.

Silakan ubah contoh, integrasikan ke dalam pipeline manajemen dokumen Anda, atau ajukan pertanyaan di kolom komentar. Selamat coding, dan nikmati mengubah pemindaian yang tak terbaca menjadi emas yang dapat dicari!

## Tutorial Terkait

- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Cómo hacer OCR a PDF en .NET con Aspose.OCR](/ocr/spanish/net/text-recognition/recognize-pdf/)
- [كيفية إجراء OCR لملف PDF في .NET باستخدام Aspose.OCR](/ocr/arabic/net/text-recognition/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}