---
category: general
date: 2026-02-28
description: Buat PDF yang dapat dicari di C# dengan menggabungkan gambar secara vertikal.
  Pelajari cara menumpuk gambar secara vertikal dan mengonversi halaman PDF yang dipindai
  dengan Aspose OCR.
draft: false
keywords:
- create searchable pdf
- combine images vertically
- how to stack images vertically
- convert scanned pages pdf
language: id
og_description: Buat PDF yang dapat dicari di C# dengan menggabungkan gambar secara
  vertikal. Panduan ini menunjukkan cara menumpuk gambar secara vertikal dan mengonversi
  halaman PDF yang dipindai menggunakan Aspose OCR.
og_title: Buat PDF yang Dapat Dicari di C# – Gabungkan Gambar Secara Vertikal
tags:
- Aspose OCR
- C#
- PDF generation
title: Buat PDF yang Dapat Dicari di C# – Gabungkan Gambar Secara Vertikal
url: /id/net/text-recognition/create-searchable-pdf-in-c-combine-images-vertically/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat PDF yang Dapat Dicari di C# – Menggabungkan Gambar Secara Vertikal

Pernah perlu **membuat PDF yang dapat dicari** dari beberapa file PNG yang dipindai tetapi tidak yakin harus mulai dari mana? Anda tidak sendirian. Dalam banyak proyek otomatisasi dokumen, titik sakit terbesar adalah mengubah tumpukan file gambar menjadi satu PDF yang rapi, dapat dicari, yang dapat diindeks dan dibagikan.  

Dalam tutorial ini kami akan menelusuri contoh lengkap yang siap dijalankan yang menunjukkan **cara menumpuk gambar secara vertikal**, **menggabungkan gambar secara vertikal**, dan akhirnya **mengonversi halaman yang dipindai menjadi PDF** menjadi satu dokumen yang dapat dicari menggunakan mesin berakselerasi GPU Aspose.OCR. Pada akhir tutorial Anda akan memiliki program mandiri yang dapat ditempatkan ke dalam solusi .NET apa pun.

> **Apa yang akan Anda pelajari**
> - Menginisialisasi mesin OCR dengan dukungan GPU.
> - Memproses batch gambar secara paralel.
> - **Menggabungkan gambar secara vertikal** untuk meniru pemindaian multi‑halaman.
> - Mengekspor PDF yang dapat dicari dan laporan JSON terperinci untuk analisis lanjutan.

## Prasyarat

- .NET 6+ (kode dapat dikompilasi dengan .NET 6, .NET 7, atau .NET 8)
- Paket NuGet Aspose.OCR (`Install-Package Aspose.OCR`)
- Mesin dengan GPU jika Anda ingin mempertahankan pengaturan `ProcessingMode.Gpu` (fallback CPU juga berfungsi)
- Folder dengan beberapa file PNG/JPEG yang dipindai (demo menggunakan `page1.png`, `page2.png`, `page3.png`)

Tanpa layanan eksternal, tanpa file konfigurasi tersembunyi—hanya C# murni.

## Langkah 1 – Siapkan Mesin OCR untuk **Membuat PDF yang Dapat Dicari**

Pertama kami membuat `OcrEngine`, mengaktifkan akselerasi GPU, memilih bahasa Inggris, dan menambahkan beberapa filter pra‑pemrosesan. Filter‑filter ini meningkatkan akurasi dengan meluruskan halaman yang miring (`DeskewFilter`) dan menghilangkan noise (`DenoiseFilter`).

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;
using System.Collections.Generic;
using System.Drawing;

class AllInOneDemo
{
    static void Main()
    {
        // Initialize OCR engine – this is the heart of creating a searchable PDF
        var ocrEngine = new OcrEngine
        {
            ProcessingMode = ProcessingMode.Gpu,   // Switch to CPU if no GPU
            Language = OcrLanguage.English
        };
        // Pre‑processing improves OCR quality
        ocrEngine.Filters.Add(new DeskewFilter());
        ocrEngine.Filters.Add(new DenoiseFilter());
```

**Mengapa ini penting:** Mesin OCR melakukan pekerjaan berat dalam mengenali teks. Mengaktifkan `ProcessingMode.Gpu` dapat memotong waktu pengenalan hingga setengah pada kartu grafis modern, sementara filter mengurangi artefak pemindaian umum yang biasanya menghasilkan output berantakan.

## Langkah 2 – Konfigurasikan Batch Processor untuk **Mengonversi Halaman yang Dipindai menjadi PDF** Secara Efisien

Memproses setiap halaman satu per satu baik untuk beberapa gambar, tetapi proyek dunia nyata sering melibatkan puluhan atau ratusan halaman. `OcrBatchProcessor` dari Aspose.OCR memungkinkan kami menjalankan pengenalan secara paralel, mempercepat langkah **mengonversi halaman yang dipindai menjadi pdf** secara dramatis.

```csharp
        // Set up batch processor – ideal for converting many scanned pages to PDF
        var batchProcessor = new OcrBatchProcessor
        {
            MaxDegreeOfParallelism = 2,          // Adjust based on CPU/GPU cores
            Language = OcrLanguage.English,
            ProcessingMode = ProcessingMode.Gpu
        };

        // List the image files you want to turn into a searchable PDF
        List<string> imageFiles = new()
        {
            "YOUR_DIRECTORY/page1.png",
            "YOUR_DIRECTORY/page2.png",
            "YOUR_DIRECTORY/page3.png"
        };
```

**Tips pro:** Jika Anda berada di mesin hanya CPU, setel `ProcessingMode = ProcessingMode.Cpu`. Batch processor tetap menghormati `MaxDegreeOfParallelism`, sehingga Anda dapat menyesuaikannya agar tidak membebani mesin.

## Langkah 3 – Jalankan OCR pada Batch dan Kumpulkan Hasil

Sekarang kami benar‑benar mengenali teks. Metode `Recognize` mengembalikan daftar objek `OcrResult`, masing‑masing berisi gambar asli dan teks yang diekstrak.

```csharp
        // Run OCR on all images at once
        List<OcrResult> ocrResults = batchProcessor.Recognize(imageFiles);
```

Pada titik ini Anda memiliki semua yang diperlukan untuk **membuat PDF yang dapat dicari**: gambar‑gambar (masih di memori) dan lapisan teks yang terkait.

## Langkah 4 – **Menggabungkan Gambar Secara Vertikal** dan Hasilkan PDF yang Dapat Dicari

Sebagian besar dokumen yang dipindai adalah PDF multi‑halaman, jadi kami perlu menjahit gambar‑gambar halaman individu menjadi satu gambar tinggi yang meniru tumpukan fisik. Aspose.OCR menyediakan `Image.CombineVertical` untuk tujuan tersebut.

```csharp
        // Stitch the page images into one tall image – this is how we **combine images vertically**
        using var combinedImage = Image.CombineVertical(
            ocrResults.ConvertAll(r => r.Image));

        // Finally, create a searchable PDF from the combined image
        ocrEngine.RecognizeToPdf(combinedImage, "YOUR_DIRECTORY/combined_searchable.pdf");
```

File yang dihasilkan (`combined_searchable.pdf`) berisi teks yang dapat dipilih dan dicari di bawah setiap gambar halaman—tepat apa yang Anda butuhkan untuk **membuat PDF yang dapat dicari** dari sumber yang dipindai.

![Buat PDF yang dapat dicari contoh](/images/create-searchable-pdf.png "contoh pdf yang dapat dicari")

*Teks alt gambar: contoh pdf yang dapat dicari menampilkan PDF gabungan dengan teks yang dapat dicari.*

**Mengapa menumpuk secara vertikal?** Banyak pustaka OCR memperlakukan setiap gambar sebagai halaman terpisah. Dengan menumpuknya, kami menjaga urutan halaman PDF tetap utuh sambil tetap memanfaatkan satu proses OCR untuk seluruh dokumen.

## Langkah 5 – Ekspor JSON Terperinci untuk Halaman Pertama (Bagus untuk Alur Kerja Lanjutan)

Kadang‑kadang Anda membutuhkan lebih dari PDF; mungkin Anda ingin memasukkan data OCR ke dalam basis data atau pipeline pembelajaran mesin. Aspose.OCR memungkinkan Anda men-serialize setiap `OcrResult` ke JSON, mempertahankan kotak pembatas, skor kepercayaan, dan lainnya.

```csharp
        // Dump the first page’s OCR result to pretty‑printed JSON
        string jsonOutput = ocrResults[0].ToJson(prettyPrint: true);
        Console.WriteLine("--- JSON for first page ---");
        Console.WriteLine(jsonOutput);
    }
}
```

**Potongan JSON yang Diharapkan (dipotong):**

```json
{
  "Text": "Sample scanned text …",
  "Confidence": 0.97,
  "Blocks": [
    {
      "Text": "Header",
      "BoundingBox": { "X": 15, "Y": 10, "Width": 480, "Height": 30 }
    }
    // …
  ]
}
```

Sekarang Anda dapat mengirim JSON ini ke sistem downstream apa pun—baik Anda mengindeks teks di Elasticsearch atau mengirimnya ke dasbor analitik khusus.

---

## Cara **Menumpuk Gambar Secara Vertikal** – Ringkasan Cepat

Jika Anda bertanya‑tanya **cara menumpuk gambar secara vertikal** tanpa Aspose, Anda dapat menggunakan `System.Drawing` untuk membuat bitmap baru dan menggambar setiap halaman satu demi satu. Namun, `Image.CombineVertical` bawaan Aspose menangani DPI, format piksel, dan manajemen memori untuk Anda, menjadikannya pilihan paling dapat diandalkan untuk kode produksi.

### Alternatif: Menggunakan `System.Drawing` (hanya untuk rasa penasaran)

```csharp
int totalHeight = 0;
int maxWidth = 0;
foreach (var img in ocrResults)
{
    totalHeight += img.Image.Height;
    maxWidth = Math.Max(maxWidth, img.Image.Width);
}
var canvas = new Bitmap(maxWidth, totalHeight);
using var g = Graphics.FromImage(canvas);
int offset = 0;
foreach (var img in ocrResults)
{
    g.DrawImage(img.Image, 0, offset);
    offset += img.Image.Height;
}
canvas.Save("combined_manual.png");
```

Pendekatan manual berfungsi, tetapi Anda kehilangan kemudahan penanganan DPI otomatis dan kemampuan untuk langsung memberi hasil kembali ke `RecognizeToPdf`. Tetap gunakan `CombineVertical` kecuali Anda memiliki kebutuhan yang sangat khusus.

## Kesalahan Umum & Cara Menghindarinya

| Masalah | Mengapa Terjadi | Solusi |
|-------|----------------|-----|
| **Kesalahan out‑of‑memory** saat memproses puluhan pemindaian resolusi tinggi | Setiap gambar tetap berada di memori sampai PDF ditulis | Buang objek `Image` segera setelah selesai (`using` blocks) atau turunkan resolusi gambar sebelum menggabungkan |
| **Teks berantakan** setelah OCR | Pemindaian miring atau kontras rendah | Pertahankan `DeskewFilter` dan `DenoiseFilter`; pertimbangkan menambahkan `ContrastFilter` bila diperlukan |
| **Lapisan dapat dicari tidak muncul** | Menggunakan `Recognize` alih‑alih `RecognizeToPdf` | Pastikan Anda memanggil `ocrEngine.RecognizeToPdf` pada gambar yang digabung |
| **GPU fallback gagal** pada mesin tanpa driver yang tepat | `ProcessingMode.Gpu` melempar pengecualian | Bungkus pembuatan engine dalam try/catch dan fallback ke `ProcessingMode.Cpu` |

## Langkah Selanjutnya – Memperluas Alur Kerja

Setelah Anda tahu cara **membuat PDF yang dapat dicari**, Anda mungkin ingin:

- **Memproses batch seluruh folder** menggunakan `Directory.GetFiles` dan loop `foreach`.
- **Menambahkan watermark** ke setiap halaman sebelum menggabungkan (gunakan `ImageProcessor` dari Aspose.Imaging).
- **Membagi PDF yang dapat dicari kembali menjadi halaman terpisah** jika Anda membutuhkan PDF per‑halaman nanti (`PdfDocument.Split` dari Aspose.PDF).
- **Mengintegrasikan dengan Azure Blob Storage** untuk mengambil gambar dari cloud dan mengirim PDF akhir kembali.

Semua ekstensi ini secara alami melibatkan konsep inti yang sama: penyiapan OCR, penanganan gambar, dan ekspor PDF.

---

## Kesimpulan

Kami telah membahas semua yang Anda perlukan untuk **membuat PDF yang dapat dicari** dari kumpulan gambar yang dipindai menggunakan C#. Dengan menginisialisasi `OcrEngine` yang didukung GPU, menjalankan batch paralel dengan `OcrBatchProcessor`, **menggabungkan gambar secara vertikal**, dan akhirnya memanggil `RecognizeToPdf`, Anda akan mendapatkan dokumen yang rapi dan dapat dicari siap untuk pengarsipan atau pengindeksan. Ekspor JSON tambahan memberi Anda visibilitas penuh ke hasil OCR, membuka peluang untuk analitik atau alur kerja khusus.

Cobalah, eksperimen dengan filter yang berbeda, dan saksikan pipeline otomatisasi dokumen Anda menjadi jauh lebih mulus. Jika Anda menemukan kendala, tinggalkan komentar—selamat coding!

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}