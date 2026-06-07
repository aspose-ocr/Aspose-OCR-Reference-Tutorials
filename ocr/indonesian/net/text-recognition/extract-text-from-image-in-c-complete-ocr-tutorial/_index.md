---
category: general
date: 2026-06-06
description: Ekstrak teks dari gambar menggunakan C# OCR. Pelajari cara memuat gambar
  untuk OCR, mengenali dokumen yang dipindai, dan mendapatkan hasil yang akurat dalam
  hitungan menit.
draft: false
keywords:
- extract text from image
- load image for OCR
- recognize scanned document
- c# OCR tutorial
language: id
og_description: Ekstrak teks dari gambar dengan C#. Tutorial ini menunjukkan cara
  memuat gambar untuk OCR, mengenali dokumen yang dipindai, dan menguasai tutorial
  OCR C# langkah demi langkah.
og_title: Ekstrak Teks dari Gambar di C# – Panduan OCR Lengkap
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Extract text from image using C# OCR. Learn how to load image for OCR,
    recognize scanned document, and get accurate results in minutes.
  headline: Extract Text from Image in C# – Complete OCR Tutorial
  type: TechArticle
- description: Extract text from image using C# OCR. Learn how to load image for OCR,
    recognize scanned document, and get accurate results in minutes.
  name: Extract Text from Image in C# – Complete OCR Tutorial
  steps:
  - name: Save the code as `Program.cs` inside a new console project.
    text: Save the code as `Program.cs` inside a new console project.
  - name: Open a terminal at the project root.
    text: Open a terminal at the project root.
  - name: Run `dotnet add package Aspose.OCR` (if you haven’t already).
    text: Run `dotnet add package Aspose.OCR` (if you haven’t already).
  - name: 'Build and execute:'
    text: 'Build and execute:'
  type: HowTo
- questions:
  - answer: Yes—most OCR libraries let you load a PDF page as an image stream or expose
      a `PdfDocument` API. Convert each page to an image first, then follow the same
      steps.
    question: Can I process PDFs directly?
  - answer: The `ImageStream.FromFile` method supports JPEG, PNG, BMP, and TIFF out
      of the box. No extra conversion required.
    question: What if my image is in PNG format?
  - answer: Handwriting is a tougher nut to crack. Look for a library that offers
      a “handwriting” model, or pre‑process the image with binarization and noise
      removal before feeding it to the engine.
    question: How do I improve accuracy for handwritten notes?
  - answer: 'Absolutely. Most engines expose a `Rect` or `Region` property where you
      can limit OCR to a bounding box—great for forms with fixed fields. --- ## Next
      Steps & Related Topics Now that you’ve mastered the basics of **extract text
      from image** with a **c# OCR tutorial**, consider exploring: - **Batch p'
    question: Is there a way to extract text in a specific region?
  type: FAQPage
tags:
- OCR
- C#
- Image Processing
title: Ekstrak Teks dari Gambar di C# – Tutorial OCR Lengkap
url: /id/net/text-recognition/extract-text-from-image-in-c-complete-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ekstrak Teks dari Gambar di C# – Tutorial OCR Lengkap

Pernah bertanya-tanya bagaimana cara **mengekstrak teks dari gambar** hanya dengan beberapa baris kode C#? Anda tidak sendirian. Banyak pengembang mengalami kebuntuan ketika harus mengambil kata‑kata dari pemindaian yang berisik dan miring, dan trik “salin‑tempel” biasa tidak cukup.  

Pada panduan ini kami akan membahas **tutorial OCR c#** praktis yang menunjukkan cara **memuat gambar untuk OCR**, mengaktifkan pra‑pemrosesan cerdas, dan akhirnya **mengenali dokumen yang dipindai** dengan akurasi yang sangat jelas. Pada akhir tutorial Anda akan memiliki program yang dapat dijalankan dan dapat dimasukkan ke proyek .NET mana pun.

## Apa yang Dibahas dalam Tutorial Ini

- Menginstal paket NuGet Aspose.OCR (atau yang kompatibel)  
- Membuat dan mengonfigurasi instance mesin OCR  
- **Memuat gambar untuk OCR** – menangani jalur file, aliran, dan jebakan umum  
- Mengaktifkan pra‑pemrosesan otomatis untuk memperbaiki kemiringan, mengurangi noise, dan masalah kontras  
- **Mengenali dokumen yang dipindai** – mengambil hasil teks polos  
- Kode sumber lengkap yang dapat Anda salin‑tempel dan jalankan segera  

Pengalaman OCR sebelumnya tidak diperlukan; cukup pemahaman dasar tentang C# dan Visual Studio (atau IDE favorit Anda).  

> **Mengapa penting?** Mengotomatisasi ekstraksi teks membuka peluang untuk pemrosesan faktur, PDF yang dapat dicari, pengurangan entri data, dan bahkan dataset siap AI.  

![ekstrak teks dari gambar menggunakan C# OCR](/images/extract-text-from-image-csharp.png "ekstrak teks dari gambar")

## Prasyarat

- .NET 6.0 SDK atau yang lebih baru (kode ini juga bekerja dengan .NET Framework 4.8)  
- Visual Studio 2022 (edisi Community sudah cukup)  
- Paket NuGet `Aspose.OCR` (atau perpustakaan apa pun yang menyediakan `OcrEngine`, `OcrResult`, dll.)  

Jika Anda belum menginstal paket tersebut, jalankan:

```bash
dotnet add package Aspose.OCR
```

---

## Langkah 1: Buat Instance Mesin OCR

Hal pertama yang Anda lakukan adalah memulai mesin yang akan melakukan pekerjaan berat. Anggap `OcrEngine` sebagai otak di balik operasi—setelah aktif, Anda dapat memberi gambar kepadanya dan meminta teks.

```csharp
using Aspose.OCR;          // Namespace for OCR classes
using Aspose.OCR.Image;    // For ImageStream helper

// Step 1: Create an OCR engine instance
OcrEngine ocrEngine = new OcrEngine();
```

> **Tips pro:** Simpan mesin sebagai singleton jika Anda memproses banyak gambar dalam satu batch; mesin akan menggunakan kembali sumber daya internal dan mempercepat proses.

## Langkah 2: Aktifkan Pra‑Pemrosesan Otomatis

Pindai dunia nyata jarang sempurna. Mereka sering miring, berisik, atau memiliki kontras yang buruk. Mengaktifkan `AutoPreprocess` memberi tahu mesin untuk secara otomatis memperbaiki kemiringan, mengurangi noise, dan menyesuaikan kontras sebelum melihat karakter.

```csharp
// Step 2: Enable automatic preprocessing (deskew, denoise, contrast adjustment)
ocrEngine.Config.AutoPreprocess = true;
```

Mengapa ini penting? Tanpa pra‑pemrosesan, mesin OCR dapat salah membaca “8” menjadi “B” atau bahkan melewatkan seluruh baris. Langkah otomatis ini menghemat Anda dari menulis kode pembersihan gambar khusus.

## Langkah 3: Atur Bahasa Pengakuan

Sebagian besar perpustakaan OCR dilengkapi dengan paket bahasa. Di sini kami mengatur bahasa Inggris, tetapi Anda dapat beralih ke `OcrLanguage.French`, `OcrLanguage.Spanish`, dll., tergantung pada dokumen Anda.

```csharp
// Step 3: Set the language for recognition
ocrEngine.Language = OcrLanguage.English;
```

Jika dokumen yang dipindai berisi bahasa campuran, Anda dapat menjalankan mesin dua kali atau menggunakan model multibahasa—sesuatu yang dapat dieksplorasi nanti.

## Langkah 4: Muat Gambar untuk OCR

Sekarang kita **memuat gambar untuk OCR**. Pembantu `ImageStream.FromFile` membaca file ke dalam format yang dipahami mesin. Pastikan jalur mengarah ke file yang sebenarnya; jalur relatif berfungsi saat Anda menjalankan dari folder proyek.

```csharp
// Step 4: Load the image to be processed
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/skewed_noisy.jpg");
```

> **Kesalahan umum:** Menggunakan jalur dengan spasi tanpa mengutipnya dapat menyebabkan `FileNotFoundException`. Selalu pastikan file ada dengan `File.Exists` sebelum memberikannya ke mesin.

## Langkah 5: Lakukan Pengakuan OCR

Dengan semua konfigurasi selesai, akhirnya kita **mengenali konten dokumen yang dipindai**. Metode `Recognize` melakukan pekerjaan berat dan mengembalikan objek `OcrResult` yang berisi teks yang diekstrak serta skor kepercayaan.

```csharp
// Step 5: Perform OCR recognition
OcrResult ocrResult = ocrEngine.Recognize();
```

Jika Anda memerlukan tingkat kepercayaan untuk setiap baris, Anda dapat memeriksa `ocrResult.Confidence` (float antara 0 dan 1). Kepercayaan rendah? Pertimbangkan mengubah pengaturan pra‑pemrosesan atau menyediakan gambar dengan resolusi lebih tinggi.

## Langkah 6: Keluarkan Teks yang Dikenali

Cara paling sederhana untuk memverifikasi keberhasilan adalah mencetak teks ke konsol. Dalam aplikasi nyata Anda mungkin akan menulisnya ke file, basis data, atau mengirimnya ke layanan lain.

```csharp
// Step 6: Output the recognized text
Console.WriteLine(ocrResult.Text);
```

Menjalankan program seharusnya mencetak sesuatu seperti:

```
The quick brown fox jumps over the lazy dog.
```

Bahkan jika gambar asli sedikit miring atau berisik, pra‑pemrosesan otomatis seharusnya sudah membersihkannya cukup untuk menghasilkan output yang bersih.

---

## Kode Sumber Lengkap – Contoh Siap‑Jalankan

Berikut adalah program lengkap yang dapat Anda salin ke proyek konsol baru (`dotnet new console`). Program ini mencakup semua langkah di atas, plus sedikit penanganan error agar tutorial lebih kuat.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Image;

namespace ExtractTextFromImageDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Validate input argument
            if (args.Length == 0)
            {
                Console.WriteLine("Usage: dotnet run <image-path>");
                return;
            }

            string imagePath = args[0];

            if (!File.Exists(imagePath))
            {
                Console.WriteLine($"Error: File not found at '{imagePath}'");
                return;
            }

            try
            {
                // Step 1: Create OCR engine
                OcrEngine ocrEngine = new OcrEngine();

                // Step 2: Enable auto‑preprocess (deskew, denoise, contrast)
                ocrEngine.Config.AutoPreprocess = true;

                // Step 3: Choose language (English in this case)
                ocrEngine.Language = OcrLanguage.English;

                // Step 4: Load image for OCR
                ocrEngine.Image = ImageStream.FromFile(imagePath);

                // Step 5: Recognize scanned document
                OcrResult result = ocrEngine.Recognize();

                // Step 6: Output the extracted text
                Console.WriteLine("\n--- Extracted Text ---\n");
                Console.WriteLine(result.Text);
                Console.WriteLine("\n--- End of Output ---\n");

                // Optional: Show confidence if you need it
                Console.WriteLine($"Overall confidence: {result.Confidence:P2}");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"OCR failed: {ex.Message}");
            }
        }
    }
}
```

### Cara Menjalankan

1. Simpan kode sebagai `Program.cs` di dalam proyek konsol baru.  
2. Buka terminal di root proyek.  
3. Jalankan `dotnet add package Aspose.OCR` (jika belum melakukannya).  
4. Bangun dan jalankan:  

   ```bash
   dotnet run "C:\Images\invoice_scanned.jpg"
   ```

Anda akan melihat teks yang diekstrak dicetak ke konsol, bersama persentase kepercayaan keseluruhan.

---

## Pertanyaan yang Sering Diajukan (FAQ)

**Q: Bisakah saya memproses PDF secara langsung?**  
A: Ya—sebagian besar perpustakaan OCR memungkinkan Anda memuat halaman PDF sebagai aliran gambar atau menyediakan API `PdfDocument`. Konversi setiap halaman menjadi gambar terlebih dahulu, lalu ikuti langkah yang sama.

**Q: Bagaimana jika gambar saya berformat PNG?**  
A: Metode `ImageStream.FromFile` mendukung JPEG, PNG, BMP, dan TIFF secara langsung. Tidak memerlukan konversi tambahan.

**Q: Bagaimana cara meningkatkan akurasi untuk catatan tulisan tangan?**  
A: Tulisan tangan lebih sulit dipecahkan. Cari perpustakaan yang menawarkan model “handwriting”, atau pra‑proses gambar dengan binarisasi dan penghilangan noise sebelum memberikannya ke mesin.

**Q: Apakah ada cara untuk mengekstrak teks pada wilayah tertentu?**  
A: Tentu saja. Sebagian besar mesin menyediakan properti `Rect` atau `Region` dimana Anda dapat membatasi OCR pada kotak pembatas—berguna untuk formulir dengan bidang tetap.

---

## Langkah Selanjutnya & Topik Terkait

Sekarang Anda telah menguasai dasar **mengekstrak teks dari gambar** dengan **tutorial OCR c#**, pertimbangkan untuk menjelajahi:

- **Pemrosesan batch** – iterasi melalui direktori gambar dan menulis setiap hasil ke file CSV.  
- **Pembuatan PDF** – gabungkan teks yang diekstrak dengan perpustakaan PDF untuk membuat PDF yang dapat dicari.  
- **Pemrosesan pasca‑machine‑learning** – gunakan pemeriksa ejaan atau model bahasa untuk membersihkan kesalahan OCR.  

Setiap hal ini dibangun di atas konsep inti yang kami bahas: memuat gambar untuk OCR, mengonfigurasi mesin, dan mengenali dokumen yang dipindai.

---

## Kesimpulan

Kami baru saja melewati contoh lengkap end‑to‑end yang menunjukkan cara **mengekstrak teks dari gambar** dalam C#. Dari membuat `OcrEngine` hingga mengeluarkan string akhir, setiap baris kode dijelaskan dan siap dijalankan.

Jika Anda mengikuti langkah‑langkah tersebut, Anda dapat mengubah pemindaian berisik, kwitansi, atau catatan tulisan tangan menjadi teks yang dapat dicari dan diedit dalam hitungan detik. Terus bereksperimen—ubah flag pra‑pemrosesan, ganti bahasa, atau beri mesin sekumpulan file. Dunia pemrosesan dokumen otomatis ada di tangan Anda untuk dijelajahi.

Punya pertanyaan lebih lanjut atau contoh penggunaan menarik? Tinggalkan komentar di bawah, dan selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Ekstrak Teks dari Gambar Menggunakan Aspose.OCR .NET](/ocr/english/net/image-and-drawing-recognition/)
- [Ekstrak teks gambar C# dengan pemilihan bahasa menggunakan Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Ekstrak Teks dari Gambar – Optimasi OCR dengan Aspose.OCR untuk .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}