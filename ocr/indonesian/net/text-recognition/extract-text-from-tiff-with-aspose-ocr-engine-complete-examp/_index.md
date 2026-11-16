---
category: general
date: 2026-04-04
description: Pelajari cara mengekstrak teks dari file TIFF menggunakan contoh mesin
  OCR dalam C#. Panduan langkah demi langkah dengan output JSON dan XML.
draft: false
keywords:
- extract text from tiff
- ocr engine example
- Aspose OCR C#
- multi‑page TIFF OCR
- JSON OCR result
language: id
og_description: Ekstrak teks dari file TIFF menggunakan contoh mesin OCR dalam C#.
  Langkah‑langkah detail, kode lengkap, dan tips untuk output JSON/XML.
og_title: Ekstrak Teks dari TIFF dengan Mesin OCR Aspose – Panduan Lengkap
tags:
- C#
- OCR
- Aspose
- Image Processing
title: Ekstrak Teks dari TIFF dengan Mesin OCR Aspose – Contoh Lengkap
url: /id/net/text-recognition/extract-text-from-tiff-with-aspose-ocr-engine-complete-examp/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ekstrak Teks dari TIFF – Contoh Lengkap Mesin OCR dalam C#

Pernahkah Anda perlu **mengekstrak teks dari TIFF** gambar tetapi tidak yakin perpustakaan mana yang dapat menangani file multi‑halaman tanpa serangkaian solusi rumit? Anda tidak sendirian. Dalam banyak sistem legacy, dokumen datang sebagai pemindaian TIFF multi‑halaman, dan mengekstrak teks mentah adalah fitur yang wajib dimiliki untuk pencarian, kepatuhan, atau otomatisasi entri data.

Kabar baiknya? Dengan Aspose OCR Anda dapat melakukannya dalam beberapa baris kode—tanpa harus mengutak‑atik buffer piksel tingkat rendah. Tutorial ini memandu Anda melalui **contoh lengkap mesin OCR** yang memuat TIFF multi‑halaman, mengenali setiap halaman, dan menghasilkan JSON yang diformat cantik serta XML opsional. Pada akhir tutorial Anda akan memiliki aplikasi konsol C# siap jalankan yang mengekstrak teks dari file TIFF dalam hitungan detik.

## Apa yang Akan Anda Pelajari

- Cara menyiapkan mesin Aspose OCR dalam proyek .NET.  
- Kode tepat untuk **mengekstrak teks dari TIFF** file, termasuk penanganan multi‑halaman.  
- Mengapa Anda mungkin menginginkan output JSON dibandingkan XML dan cara menghasilkan keduanya.  
- Tips memecahkan masalah umum (misalnya DPI gambar, penggunaan memori).  

### Prasyarat

- .NET 6.0 SDK atau yang lebih baru (kode ini bekerja dengan .NET Core dan .NET Framework).  
- Lisensi Aspose OCR yang valid (atau kunci percobaan gratis).  
- Visual Studio 2022 atau editor C# pilihan Anda.  
- File TIFF multi‑halaman contoh (dengan nama `multi-page.tiff` dalam contoh).  

> **Pro tip:** Jika Anda memiliki anggaran terbatas, percobaan gratis tetap memungkinkan Anda mengekstrak teks hingga 100 halaman per bulan—sempurna untuk pengujian.

---

## Langkah 1 – Inisialisasi Mesin OCR (ocr engine example)

Sebelum kita dapat **mengekstrak teks dari TIFF**, kita memerlukan sebuah instance mesin OCR. Objek ini menyimpan semua konfigurasi yang mungkin Anda ubah nanti (bahasa, resolusi, dll.).

```csharp
using Aspose.OCR;
using System.IO;

// Create a new OCR engine – this is the core of our ocr engine example
var ocrEngine = new OcrEngine();

// Optional: set language if you know the document’s language
// ocrEngine.Language = Language.English;
```

*Mengapa ini penting:* Kelas `OcrEngine` mengabstraksi kerja berat. Menginstansiasinya sekali dan menggunakannya kembali untuk beberapa gambar lebih efisien memori dibandingkan membuat mesin baru untuk setiap halaman.

---

## Langkah 2 – Muat TIFF Multi‑Halaman (extract text from TIFF)

Sekarang kita mengarahkan mesin ke file sumber kita. `ImageStream.FromFile` mendukung TIFF, JPEG, PNG, dan banyak format lainnya, tetapi untuk tutorial ini kita fokus pada TIFF.

```csharp
// Load the multi‑page TIFF you want to process
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/multi-page.tiff");
```

> **Catatan:** Ganti `YOUR_DIRECTORY` dengan jalur folder yang sebenarnya di mesin Anda.  
> **Tip:** Jika TIFF Anda memiliki DPI rendah (di bawah 150), pertimbangkan pra‑pemrosesan untuk meningkatkan akurasi OCR.

---

## Langkah 3 – Kenali Semua Halaman

Memanggil `Recognize()` menjalankan algoritma OCR pada **setiap halaman** dalam TIFF. Objek hasil berisi teks mentah, skor kepercayaan, dan segmentasi per halaman.

```csharp
// Run OCR on the loaded image – this extracts text from all pages
var ocrResult = ocrEngine.Recognize();
```

*Apa yang Anda dapatkan:* `ocrResult` berisi koleksi objek `PageResult`. Teks tiap halaman dapat diakses melalui `ocrResult.Pages[i].Text`. Mesin juga menyediakan tingkat kepercayaan, yang berguna untuk pemeriksaan kualitas.

---

## Langkah 4 – Simpan Hasil sebagai JSON (dan XML opsional)

Sebagian besar pipeline modern lebih menyukai JSON, tetapi sistem legacy masih mengandalkan XML. Berikut cara menghasilkan keduanya dengan format yang rapi.

```csharp
// Convert the recognition result to pretty‑printed JSON
string jsonResult = ocrResult.ToJson(prettyPrint: true);
File.WriteAllText(@"YOUR_DIRECTORY/result.json", jsonResult);

// Optional: also output XML for older workflows
string xmlResult = ocrResult.ToXml();
File.WriteAllText(@"YOUR_DIRECTORY/result.xml", xmlResult);
```

### Contoh Output JSON (dipotong)

```json
{
  "Pages": [
    {
      "PageNumber": 1,
      "Text": "Invoice #12345\nDate: 2024‑03‑15\nTotal: $1,250.00",
      "Confidence": 0.97
    },
    {
      "PageNumber": 2,
      "Text": "Itemized List\n1. Widget A – $500.00\n2. Widget B – $750.00",
      "Confidence": 0.95
    }
  ]
}
```

JSON mudah dibaca manusia, sehingga debugging menjadi sangat mudah. XML mencerminkan struktur yang sama jika Anda membutuhkannya.

---

## Langkah 5 – Verifikasi Ekstraksi (extract text from TIFF)

Setelah file ditulis, pemeriksaan cepat membantu memastikan tidak ada yang salah.

```csharp
// Load the JSON back just to confirm it was saved correctly
string loadedJson = File.ReadAllText(@"YOUR_DIRECTORY/result.json");
Console.WriteLine("First 200 characters of JSON output:");
Console.WriteLine(loadedJson.Substring(0, Math.Min(200, loadedJson.Length)));
```

Jika Anda melihat potongan teks yang dicetak, Anda telah berhasil **mengekstrak teks dari TIFF** dan menyimpannya. Dari sini Anda dapat mengirim JSON ke indeks pencarian, basis data, atau layanan downstream lainnya.

---

## Mengapa Menggunakan Aspose OCR untuk mengekstrak teks dari TIFF?

- **Dukungan multi‑halaman langsung** – tidak perlu memecah TIFF secara manual.  
- **Akurasi tinggi** berkat model jaringan saraf proprietari.  
- **Lintas‑platform** – bekerja pada runtime .NET Windows, Linux, dan macOS.  
- **Format output kaya** (JSON, XML, plain text) yang cocok untuk stack modern maupun legacy.  

Jika Anda masih ragu, coba percobaan gratis pada dokumen contoh. Anda akan merasakan kecepatan dan kesederhanaannya dibandingkan alternatif open‑source yang sering memerlukan pra‑pemrosesan gambar tambahan.

---

## Kesalahan Umum & Cara Menghindarinya

| Masalah | Gejala | Solusi |
|-------|---------|-----|
| TIFF resolusi rendah | Karakter hilang, kepercayaan rendah | Tingkatkan DPI gambar menjadi ≥150 DPI sebelum OCR (`ocrEngine.Image = ImageStream.FromFile(...).Resize(150)` ) |
| Bahasa salah | Kata-kata berantakan, terutama untuk teks non‑Inggris | Set `ocrEngine.Language = Language.Spanish` (atau yang sesuai) sebelum `Recognize()` |
| Kehabisan memori pada file besar | `OutOfMemoryException` | Proses halaman dalam batch: loop melalui `ocrEngine.Image.Pages` dan panggil `RecognizePage(i)` |
| Lisensi belum diterapkan | Watermark “Evaluation” pada output | Daftarkan lisensi Anda: `License license = new License(); license.SetLicense("Aspose.OCR.lic");` |

---

## Contoh Lengkap yang Siap Pakai (Copy‑Paste Ready)

Berikut adalah program lengkap yang dapat Anda masukkan ke proyek konsol baru. Ia mencakup semua bagian yang telah dibahas—inisialisasi, pemuatan, pengenalan, dan penyimpanan.

```csharp
using Aspose.OCR;
using System;
using System.IO;

namespace TiffOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣  Initialize the OCR engine (ocr engine example)
            // -------------------------------------------------
            var ocrEngine = new OcrEngine();

            // Optional: set license if you have one
            // var license = new License();
            // license.SetLicense("Aspose.OCR.lic");

            // -------------------------------------------------
            // 2️⃣  Load the multi‑page TIFF (extract text from TIFF)
            // -------------------------------------------------
            string tiffPath = @"YOUR_DIRECTORY/multi-page.tiff";
            if (!File.Exists(tiffPath))
            {
                Console.WriteLine($"File not found: {tiffPath}");
                return;
            }

            ocrEngine.Image = ImageStream.FromFile(tiffPath);

            // -------------------------------------------------
            // 3️⃣  Recognize every page
            // -------------------------------------------------
            var ocrResult = ocrEngine.Recognize();

            // -------------------------------------------------
            // 4️⃣  Save JSON (pretty) and optional XML
            // -------------------------------------------------
            string jsonPath = @"YOUR_DIRECTORY/result.json";
            string jsonResult = ocrResult.ToJson(prettyPrint: true);
            File.WriteAllText(jsonPath, jsonResult);
            Console.WriteLine($"JSON saved to {jsonPath}");

            // Optional XML output
            string xmlPath = @"YOUR_DIRECTORY/result.xml";
            string xmlResult = ocrResult.ToXml();
            File.WriteAllText(xmlPath, xmlResult);
            Console.WriteLine($"XML saved to {xmlPath}");

            // -------------------------------------------------
            // 5️⃣  Quick verification (extract text from TIFF)
            // -------------------------------------------------
            string preview = jsonResult.Length > 200 ? jsonResult.Substring(0, 200) + "..." : jsonResult;
            Console.WriteLine("\nPreview of JSON output:");
            Console.WriteLine(preview);
        }
    }
}
```

Simpan file sebagai `Program.cs`, jalankan `dotnet run`, dan perhatikan konsol yang memberi tahu Anda lokasi JSON dan XML disimpan. Itu saja—Anda baru saja menyelesaikan **contoh mesin OCR** yang mengekstrak teks dari TIFF.

---

## Langkah Selanjutnya & Topik Terkait

- **Pemrosesan batch:** Bungkus logika di atas dalam loop `foreach` untuk menangani puluhan file TIFF secara otomatis.  
- **Integrasi pencarian:** Kirim JSON ke Elasticsearch atau Azure Cognitive Search untuk mengaktifkan pencarian teks penuh pada dokumen yang dipindai.  
- **Pra‑pemrosesan gambar:** Jelajahi API `ImageProcessing` Aspose untuk mengoreksi kemiringan, menghilangkan noise, atau menyesuaikan kontras sebelum OCR.  
- **Output alternatif:** Gunakan `ocrResult.ToPlainText()` jika Anda hanya membutuhkan string mentah tanpa metadata.  

Jika Anda penasaran dengan format gambar lain, pola yang sama berlaku untuk PDF (cukup ganti file sumber) atau PNG. Inti pentingnya adalah setelah mesin disiapkan, sisanya menjadi pipeline yang dapat diulang.

---

## Kesimpulan

Kami telah menelusuri **contoh lengkap mesin OCR** yang memungkinkan Anda **mengekstrak teks dari TIFF** menggunakan Aspose OCR, menghasilkan JSON bersih dan XML opsional untuk alur kerja downstream apa pun. Kode ini berdiri sendiri, penjelasannya mencakup “mengapa” di balik setiap langkah.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}