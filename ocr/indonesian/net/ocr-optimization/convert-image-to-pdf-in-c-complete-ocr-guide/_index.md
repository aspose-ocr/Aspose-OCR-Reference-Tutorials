---
category: general
date: 2025-12-30
description: Mengonversi gambar ke PDF menggunakan Aspose OCR dalam C#. Pelajari cara
  memproses gambar untuk OCR, mengenali gambar teks Korea, dan membuat PDF yang dapat
  dicari dengan cepat.
draft: false
keywords:
- convert image to pdf
- preprocess image for ocr
- recognize korean text image
- create searchable pdf image
language: id
og_description: Ubah gambar menjadi PDF dengan Aspose OCR. Tutorial ini menunjukkan
  cara memproses gambar untuk OCR, mengenali gambar teks Korea, dan membuat PDF yang
  dapat dicari.
og_title: Konversi Gambar ke PDF di C# – Panduan OCR Lengkap
tags:
- C#
- OCR
- Aspose
- PDF
title: Mengonversi Gambar ke PDF dengan C# – Panduan OCR Lengkap
url: /id/net/ocr-optimization/convert-image-to-pdf-in-c-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Mengonversi Gambar ke PDF dalam C# – Panduan OCR Lengkap

Pernah membutuhkan untuk **mengonversi gambar ke PDF** tetapi juga ingin teks di dalamnya dapat dicari? Anda tidak sendirian. Banyak pengembang mengalami hal yang sama ketika menangani halaman yang dipindai, terutama yang berbahasa Korea. Kabar baiknya, dengan Aspose OCR Anda dapat **memproses gambar untuk OCR**, **mengenali gambar teks Korea**, dan akhirnya **membuat gambar PDF yang dapat dicari** hanya dengan beberapa baris kode.

Dalam tutorial ini kami akan melewati seluruh alur—dari memuat JPEG mentah halaman buku Korea, membersihkannya, mengekstrak teks, dan membungkus semuanya menjadi PDF yang dapat dicari. Pada akhir tutorial Anda akan memiliki aplikasi konsol C# siap‑jalankan yang dapat Anda masukkan ke proyek .NET mana pun.

## Apa yang Anda Butuhkan

- **.NET 6.0 atau lebih baru** (kode ini bekerja di .NET Core dan .NET Framework)  
- **Aspose.OCR untuk .NET** paket NuGet (`Aspose.OCR`) – kunci percobaan gratis tersedia di situs Aspose.  
- Contoh gambar yang berisi teks Korea (misalnya `korean_book_page.jpg`).  
- Lingkungan pengembangan pilihan Anda (Visual Studio, VS Code, Rider – saya menggunakan VS 2022).

> **Pro tip:** Simpan file gambar Anda di folder khusus seperti `Resources/` agar jalur tetap konsisten di semua mesin.

## Ikhtisar Proses

1. **Inisialisasi mesin OCR** dengan dukungan GPU untuk kecepatan.  
2. **Tambahkan filter pra‑pemrosesan** (deskew, denoise) untuk meningkatkan akurasi pengenalan.  
3. **Unduh dan muat model bahasa Korea** – Aspose melakukannya secara otomatis bila diperlukan.  
4. **Jalankan pengenalan** pada gambar masukan.  
5. **Ekspor hasil sebagai PDF yang dapat dicari** menggunakan exporter bawaan.  
6. **Opsional, serialisasikan hasil ke JSON** untuk analisis atau pencatatan lebih lanjut.

Di bawah ini kami akan memecah setiap langkah, menjelaskan *mengapa* penting, dan memberi Anda kode yang dapat langsung disalin‑tempel.

---

## ## Mengonversi Gambar ke PDF – Alur Kerja Lengkap

Cuplikan berikut adalah program *lengkap*. Silakan buat proyek konsol baru (`dotnet new console -n OcrPdfDemo`) dan ganti `Program.cs` yang dihasilkan secara otomatis dengan kode ini.

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

### Mengapa Ini Berhasil

- **Akselerasi GPU** memotong waktu pengenalan hampir setengah dibandingkan mode CPU‑only.  
- **Deskew** dan **Denoise** adalah teknik *memproses gambar untuk OCR* klasik; mereka memperbaiki cacat pemindaian umum yang biasanya membuat mesin melewatkan karakter.  
- **Pemuatan model bahasa** penting untuk **mengenali gambar teks Korea** – tanpa model Korea mesin akan kembali ke alfabet Latin generik dan menghasilkan sampah.  
- **SearchablePdfExporter** menggabungkan bitmap asli dan lapisan teks tak terlihat, memberi Anda hasil **membuat gambar PDF yang dapat dicari** yang dapat diindeks di semua pembaca PDF.

---

## ## Memproses Gambar untuk OCR – Tips & Trik

Meskipun dua filter yang kami tambahkan biasanya cukup, Anda mungkin menemui gambar yang keras kepala. Berikut beberapa langkah ekstra yang dapat dicoba:

| Masalah | Filter Tambahan | Cara Menambahkan |
|-------|-------------------|------------|
| Kontras rendah | `ContrastFilter { Level = 30 }` | `ocrEngine.Filters.Add(new ContrastFilter { Level = 30 });` |
| Noise latar belakang berat | `BinarizationFilter { Threshold = 128 }` | `ocrEngine.Filters.Add(new BinarizationFilter { Threshold = 128 });` |
| Orientasi campuran (potret & lanskap) | `OrientationFilter()` | `ocrEngine.Filters.Add(new OrientationFilter());` |

> **Catatan:** Menambahkan terlalu banyak filter dapat memperlambat proses. Uji setiap perubahan pada satu halaman sebelum memperluasnya.

---

## ## Mengenali Gambar Teks Korea – Kesalahan Umum

Skrip Korea mengandung suku kata Hangul yang padat secara visual. Jika Anda melihat output yang berantakan:

1. **Pastikan model bahasa sudah terunduh sepenuhnya** – periksa konsol untuk pesan seperti “Downloading Korean model…”.  
2. **Tingkatkan `MaxAngle`** pada `DeskewFilter` bila pemindaian Anda berputar lebih dari 12°.  
3. **Tingkatkan memori GPU** dengan mengatur `ocrEngine.GpuMemoryLimit = 2048;` (nilai dalam MB).  

Penyesuaian ini secara langsung memengaruhi keberhasilan **mengenali gambar teks Korea**.

---

## ## Membuat Gambar PDF yang Dapat Dicari – Memverifikasi Hasil

Setelah program selesai, buka `korean_page.pdf` di pembaca PDF apa pun (Adobe Acrobat Reader, Foxit, bahkan Chrome). Anda seharusnya dapat:

- **Memilih teks** dengan mouse seolah‑olah itu PDF asli.  
- **Mencari** kata‑kata Korea menggunakan kotak pencarian bawaan.  

Jika lapisan teks muncul kosong, periksa kembali bahwa metode `Export` menerima jalur gambar yang benar dan bahwa hasil OCR berisi `RecognitionResult.Text` yang tidak kosong.

---

## ## Output JSON Lengkap – Apa yang Diharapkan

Konsol mencetak payload JSON yang diformat rapi. Contoh yang dipangkas terlihat seperti ini:

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

Anda dapat mengirim JSON ini ke layanan hilir (misalnya pipeline indeksasi, API terjemahan) tanpa harus menjalankan OCR lagi.

---

## ## Pemecahan Masalah & FAQ

**T: PDF saya sangat besar dibandingkan gambar aslinya.**  
J: Exporter menyematkan bitmap asli dengan resolusi aslinya. Jika ukuran menjadi masalah, perkecil gambar *sebelum* pengenalan:

```csharp
ocrEngine.Filters.Add(new ResizeFilter { MaxWidth = 1240, MaxHeight = 1754 });
```

**T: OCR mengembalikan string kosong.**  
J: Pastikan jalur gambar benar dan file tidak rusak. Juga, pastikan driver GPU Anda terbaru; driver lama dapat menyebabkan kegagalan diam‑diam.

**T: Bisakah saya memproses beberapa halaman dalam loop?**  
J: Tentu. Bungkus langkah 4‑6 dalam loop `foreach (var file in Directory.GetFiles("Resources", "*.jpg"))` dan ubah jalur output PDF sesuai kebutuhan.

---

## ## Kesimpulan

Kami baru saja **mengonversi gambar ke PDF** sambil mempertahankan teks yang dapat dicari, semua berkat pipeline kuat Aspose OCR. Dengan **memproses gambar untuk OCR**, Anda meningkatkan akurasi; dengan **mengenali gambar teks Korea**, Anda menangani skrip kompleks; dan dengan **membuat gambar PDF yang dapat dicari**, Anda memperoleh dokumen portabel yang dapat diindeks.

Ambil kode, arahkan ke pemindaian Anda sendiri, dan bereksperimen dengan filter atau model bahasa tambahan. Pola yang sama berlaku untuk Cina, Jepang, atau bahasa berbasis Latin apa pun—cukup ganti `LanguageModel.Korean` dengan enum yang sesuai.

Ada pertanyaan lebih lanjut? Tinggalkan komentar, dan selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}