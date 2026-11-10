---
category: general
date: 2026-09-13
description: Pelajari cara mengubah halaman yang dipindai menjadi PDF di C# menggunakan
  Aspose OCR. Panduan ini menampilkan preprocessing, pengenalan teks Korean, dan pembuatan
  searchable PDF.
keywords:
- scanned page to pdf
- preprocess image for OCR
- generate pdf with text
- convert image to searchable pdf
- gpu accelerated OCR
- recognize Korean text image
lastmod: 2026-09-13
og_description: Pelajari cara mengubah halaman yang dipindai menjadi PDF di C# dengan
  Aspose OCR. Tutorial ini mencakup preprocessing gambar, GPU‑accelerated OCR untuk
  teks Korean, dan menghasilkan searchable PDF dalam hitungan menit.
og_image_alt: Screenshot of C# console app converting a scanned Korean page to searchable
  PDF using Aspose OCR
og_title: Cara mengubah halaman yang dipindai menjadi PDF di C# dengan OCR
schemas:
- author: Aspose
  dateModified: '2026-09-13'
  description: Learn how to turn a scanned page to PDF in C# using Aspose OCR. This
    guide shows preprocessing, Korean text recognition, and creating a searchable
    PDF.
  headline: How to turn a scanned page to PDF in C# with OCR
  type: TechArticle
- description: Learn how to turn a scanned page to PDF in C# using Aspose OCR. This
    guide shows preprocessing, Korean text recognition, and creating a searchable
    PDF.
  name: How to turn a scanned page to PDF in C# with OCR
  steps:
  - name: Initialise the OCR engine with GPU support.
    text: Initialise the OCR engine with GPU support.
  - name: Add **preprocess image for OCR** filters such as deskew and denoise.
    text: Add **preprocess image for OCR** filters such as deskew and denoise.
  - name: Download and load the Korean language model (handled automatically).
    text: Download and load the Korean language model (handled automatically).
  - name: Run the OCR on the image.
    text: Run the OCR on the image.
  - name: Export the result with **SearchablePdfExporter** to **create searchable
      PDF image**.
    text: Export the result with **SearchablePdfExporter** to **create searchable
      PDF image**.
  - name: (Optional) Serialize the OCR output to JSON for downstream pipelines.
    text: (Optional) Serialize the OCR output to JSON for downstream pipelines.
  - name: '**Ensure the language model is fully downloaded** – check the console for
      a message like “Downloading Korean model…”.'
    text: '**Ensure the language model is fully downloaded** – check the console for
      a message like “Downloading Korean model…”.'
  - name: '**Increase the `MaxAngle`** in `DeskewFilter` if your scans are rotated
      beyond 12°.'
    text: '**Increase the `MaxAngle`** in `DeskewFilter` if your scans are rotated
      beyond 12°.'
  - name: '**Boost GPU memory** by setting `ocrEngine.GpuMemoryLimit = 2048;` (value
      in MB).'
    text: '**Boost GPU memory** by setting `ocrEngine.GpuMemoryLimit = 2048;` (value
      in MB).'
  type: HowTo
- questions:
  - answer: 'The exporter embeds the original bitmap at its native resolution. If
      size is a concern, downscale the image *before* recognition:'
    question: My PDF is huge compared to the original image.
  - answer: Verify that the image path is correct and that the file is not corrupted.
      Also, make sure the GPU driver is up‑to‑date; older drivers can cause silent
      failures.
    question: The OCR returns empty strings.
  - answer: Absolutely. Wrap steps 4‑6 in a `foreach (var file in Directory.GetFiles("Resources",
      "*.jpg"))` loop and change the output PDF path accordingly.
    question: Can I process multiple pages in a loop?
  type: FAQPage
tags:
- scanned page to pdf
- OCR
- Aspose
- C#
title: Cara mengubah halaman yang dipindai menjadi PDF di C# dengan OCR
url: /id/net/ocr-optimization/convert-image-to-pdf-in-c-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara mengubah halaman yang dipindai menjadi PDF di C# dengan OCR

Jika Anda perlu **mengonversi halaman yang dipindai menjadi PDF** sambil menjaga teks dapat dicari, Anda berada di tempat yang tepat. Tutorial ini memandu Anda menggunakan Aspose OCR untuk **preprocess image for OCR**, **recognize Korean text image**, dan akhirnya **create searchable PDF image** – semuanya dari aplikasi konsol C# sederhana.

## Jawaban Cepat
- **Apa perpustakaan yang menangani OCR?** Aspose.OCR for .NET  
- **Apakah saya dapat menggunakan GPU?** Yes – enable GPU acceleration for up to 2× faster processing  
- **Apakah saya memerlukan paket bahasa Korea?** It downloads automatically on first use  
- **Apakah output dapat dicari?** The generated PDF contains an invisible text layer  
- **Versi .NET apa yang didukung?** .NET 6.0 and later (including .NET Core and .NET Framework)

## Persyaratan

- **.NET 6.0 atau lebih baru** – works on .NET Core, .NET Framework, dan .NET 5/6+  
- **Aspose.OCR for .NET** paket NuGet (`Aspose.OCR`) – trial keys are free on the Aspose site  
- Gambar contoh dengan karakter Korea, misalnya `korean_book_page.jpg`  
- IDE favorit Anda (Visual Studio 2022, VS Code, Rider, dll.)

> **Pro tip:** Simpan gambar di folder `Resources/` agar jalur tetap konsisten di semua mesin.

## Ikhtisar Proses

1. Inisialisasi mesin OCR dengan dukungan GPU.  
2. Tambahkan filter **preprocess image for OCR** seperti deskew dan denoise.  
3. Unduh dan muat model bahasa Korea (ditangani secara otomatis).  
4. Jalankan OCR pada gambar.  
5. Ekspor hasil dengan **SearchablePdfExporter** ke **create searchable PDF image**.  
6. (Opsional) Serialisasi output OCR ke JSON untuk pipeline hilir.

Di bawah ini kami memperluas setiap langkah, menjelaskan *mengapa* itu penting, dan memberi Anda kode tepat yang dapat Anda salin‑tempel.

## Bagaimana cara kerja konversi halaman yang dipindai menjadi PDF?

`OcrEngine` adalah kelas utama di Aspose.OCR yang melakukan pengenalan karakter optik pada gambar.  
`SearchablePdfExporter` membuat PDF yang berisi gambar asli dan lapisan teks tak terlihat untuk pencarian.  
`RecognitionResult` menyimpan teks dan data kepercayaan yang dikembalikan oleh mesin OCR.

Muat gambar Anda dengan `new OcrEngine()` dan panggil `engine.Recognize("korean_book_page.jpg")`, lalu berikan `RecognitionResult` ke `SearchablePdfExporter.Export`. Alur dua langkah ini membaca bitmap, mengekstrak teks Unicode, dan menyematkan keduanya ke dalam satu PDF di mana lapisan teks tidak terlihat tetapi dapat dicari. Akselerasi GPU memotong waktu pengenalan sekitar setengah, sementara filter deskew dan denoise meningkatkan akurasi hingga 15 % pada pemindaian yang berisik.

## Mengonversi gambar ke PDF – alur kerja lengkap

Potongan kode berikut adalah program *lengkap*. Buat proyek konsol baru (`dotnet new console -n OcrPdfDemo`) dan ganti `Program.cs` yang dihasilkan secara otomatis dengan kode yang ditampilkan di placeholder.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;
using Aspose.OCR.Export;
using Aspose.OCR.Result;   // for JsonResult

namespace OcrPdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // Step 1: Initialise the OCR engine (GPU enabled, offline mode off)
            // -----------------------------------------------------------------
            var ocrEngine = new OcrEngine
            {
                UseGpu = true,          // leverages your graphics card for faster inference
                OfflineMode = false    // allows on‑the‑fly language model download
            };

            // --------------------------------------------------------------
            // Step 2: Add preprocessing filters to improve accuracy
            // --------------------------------------------------------------
            // Deskew corrects slight rotations; MaxAngle = 12° is a safe default.
            ocrEngine.Filters.Add(new DeskewFilter { MaxAngle = 12 });

            // Denoise removes isolated speckles that often appear in scanned books.
            ocrEngine.Filters.Add(new DenoiseFilter());

            // --------------------------------------------------------------
            // Step 3: Load the Korean language model
            // --------------------------------------------------------------
            // Aspose will download the model the first time you run this on a new machine.
            ocrEngine.LoadLanguage(LanguageModel.Korean);

            // --------------------------------------------------------------
            // Step 4: Recognise text from the input image
            // --------------------------------------------------------------
            // Replace the path with your actual image location.
            string imagePath = "Resources/korean_book_page.jpg";
            var recognitionResult = ocrEngine.Recognize(imagePath);

            // --------------------------------------------------------------
            // Step 5: Export the recognised page as a searchable PDF
            // --------------------------------------------------------------
            string pdfPath = "Resources/korean_page.pdf";
            var exporter = new SearchablePdfExporter { OutputPath = pdfPath };
            exporter.Export(ocrEngine, imagePath);

            // --------------------------------------------------------------
            // Step 6: Obtain a structured JSON representation of the result
            // --------------------------------------------------------------
            string json = JsonResult.FromRecognitionResult(recognitionResult).ToString(true);
            Console.WriteLine("=== OCR JSON Result ===");
            Console.WriteLine(json);

            Console.WriteLine("\n✅ Conversion complete!");
            Console.WriteLine($"PDF saved to: {pdfPath}");
        }
    }
}
```

### Mengapa ini berhasil

- **GPU acceleration** memotong waktu pengenalan sekitar setengah dibandingkan mode hanya CPU.  
- **Deskew** dan **Denoise** adalah teknik *preprocess image for OCR* klasik; mereka memperbaiki cacat pemindaian umum yang sebaliknya menyebabkan mesin melewatkan karakter.  
- **Language model loading** penting untuk **recognize Korean text image** – tanpa model Korea mesin akan kembali ke alfabet Latin umum dan menghasilkan sampah.  
- **SearchablePdfExporter** menggabungkan bitmap asli dan lapisan teks tak terlihat, memberi Anda hasil **create searchable pdf image** yang dapat Anda indeks di penampil PDF apa pun.

## Mengapa ini berhasil

- **GPU acceleration** memotong waktu pengenalan sekitar setengah dibandingkan mode hanya CPU.  
- **Deskew** dan **Denoise** adalah teknik *preprocess image for OCR* klasik; mereka memperbaiki cacat pemindaian umum yang sebaliknya menyebabkan mesin melewatkan karakter.  
- **Language model loading** penting untuk **recognize Korean text image** – tanpa model Korea mesin akan kembali ke alfabet Latin umum dan menghasilkan sampah.  
- **SearchablePdfExporter** menggabungkan bitmap asli dan lapisan teks tak terlihat, memberi Anda hasil **create searchable pdf image** yang dapat Anda indeks di penampil PDF apa pun.

## Preprocess image for OCR – tips & trik

`DeskewFilter` memperbaiki rotasi halaman yang dipindai.  
`ContrastFilter` menyesuaikan kontras gambar untuk meningkatkan akurasi OCR.  
`BinarizationFilter` mengubah gambar menjadi hitam‑putih berdasarkan ambang, mengurangi noise latar belakang.  
`OrientationFilter` mendeteksi dan memperbaiki halaman dengan orientasi campuran potret/lanskap.  

| Masalah | Filter tambahan | Cara menambahkan |
|-------|-------------------|------------|
| Kontras rendah | `ContrastFilter { Level = 30 }` | `ocrEngine.Filters.Add(new ContrastFilter { Level = 30 });` |
| Noise latar belakang berat | `BinarizationFilter { Threshold = 128 }` | `ocrEngine.Filters.Add(new BinarizationFilter { Threshold = 128 });` |
| Orientasi campuran (potret & lanskap) | `OrientationFilter()` | `ocrEngine.Filters.Add(new OrientationFilter());` |

> **Catatan:** Menambahkan terlalu banyak filter dapat memperlambat pemrosesan. Uji setiap perubahan pada satu halaman sebelum memperbesar skala.

## Recognize Korean text image – jebakan umum

Skrip Korea mengandung suku kata Hangul yang padat secara visual. Jika Anda melihat output yang berantakan:

1. **Pastikan model bahasa telah diunduh sepenuhnya** – periksa konsol untuk pesan seperti “Downloading Korean model…”.  
2. **Tingkatkan `MaxAngle`** di `DeskewFilter` jika pemindaian Anda berputar lebih dari 12°.  
3. **Tingkatkan memori GPU** dengan mengatur `ocrEngine.GpuMemoryLimit = 2048;` (nilai dalam MB).  

`LanguageModel.Korean` memuat data bahasa Korea untuk OCR, memungkinkan pengenalan Hangul yang akurat.  

Penyesuaian ini secara langsung memengaruhi keberhasilan **recognize Korean text image**.

## Create searchable PDF image – memverifikasi hasil

Setelah program selesai, buka `korean_page.pdf` di pembaca PDF apa pun (Adobe Acrobat Reader, Foxit, bahkan Chrome). Anda harus dapat:

- **Memilih teks** dengan mouse seolah itu PDF asli.  
- **Mencari** kata-kata Korea menggunakan kotak pencarian bawaan.  

Jika lapisan teks muncul kosong, periksa kembali bahwa metode `Export` menerima jalur gambar yang benar dan bahwa hasil OCR berisi `RecognitionResult.Text` yang tidak kosong.

## Output JSON lengkap – apa yang diharapkan

Konsol mencetak payload JSON yang diformat dengan rapi. Contoh yang dipangkas terlihat seperti ini:

```json
{
  "Text": "첫 번째 페이지의 내용...",
  "Blocks": [
    {
      "Text": "첫 번째 페이지의 내용...",
      "BoundingBox": { "X": 12, "Y": 34, "Width": 560, "Height": 780 },
      "Confidence": 0.98
    }
  ],
  "Language": "Korean",
  "ProcessingTimeMs": 842
}
```

## Pemecahan Masalah & FAQ

**Q: PDF saya sangat besar dibandingkan gambar asli.**  
A: Exporter menyematkan bitmap asli pada resolusi aslinya. Jika ukuran menjadi masalah, turunkan skala gambar *sebelum* pengenalan:

```csharp
ocrEngine.Filters.Add(new ResizeFilter { MaxWidth = 1240, MaxHeight = 1754 });
```

**Q: OCR mengembalikan string kosong.**  
A: Verifikasi bahwa jalur gambar benar dan file tidak rusak. Juga, pastikan driver GPU terbaru; driver lama dapat menyebabkan kegagalan diam.

**Q: Bisakah saya memproses banyak halaman dalam loop?**  
A: Tentu saja. Bungkus langkah 4‑6 dalam loop `foreach (var file in Directory.GetFiles("Resources", "*.jpg"))` dan ubah jalur PDF output sesuai kebutuhan.

## Kesimpulan

Kami baru saja **mengonversi gambar menjadi PDF** sambil mempertahankan teks yang dapat dicari, semua berkat pipeline kuat Aspose OCR. Dengan **preprocess image for OCR**, Anda meningkatkan akurasi; dengan **recognize Korean text image**, Anda menangani skrip kompleks; dan dengan **create searchable pdf image**, Anda mendapatkan dokumen yang portabel dan dapat diindeks.

Dapatkan kode, arahkan ke pemindaian Anda sendiri, dan bereksperimen dengan filter atau model bahasa tambahan. Pola yang sama bekerja untuk bahasa Cina, Jepang, atau bahasa berbasis Latin apa pun—cukup ganti `LanguageModel.Korean` dengan enum yang sesuai.

Punya pertanyaan lebih lanjut? Tinggalkan komentar, dan selamat coding!

---

**Terakhir Diperbarui:** 2026-09-13  
**Diuji dengan:** Aspose.OCR 24.11 for .NET  
**Penulis:** Aspose

## Tutorial Terkait

- [Buat PDF Dapat Dicari Dari File yang Dipindai Menggunakan Aspose Ocr](/ocr/net/ocr-optimization/create-searchable-pdf-from-scanned-files-using-aspose-ocr/)
- [Pipeline Pra-pemrosesan OCR Cara Mengenali Teks Dari Gambar](/ocr/net/ocr-optimization/ocr-preprocessing-pipeline-how-to-recognize-text-from-image/)
- [Mengenali Teks Dari Gambar Dengan Aspose Ocr Panduan C Lengkap](/ocr/net/ocr-configuration/recognize-text-from-image-with-aspose-ocr-complete-c-guide/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}