---
category: general
date: 2026-02-16
description: Cara melakukan OCR di C# dengan cepat – pelajari cara mengekstrak teks
  dari gambar dengan pustaka Aspose OCR dalam beberapa langkah sederhana.
draft: false
keywords:
- how to perform OCR
- extract text from image
- Aspose OCR C#
- OCR JSON output
- image text extraction
language: id
og_description: Bagaimana melakukan OCR di C#? Ikuti tutorial langkah demi langkah
  ini untuk mengekstrak teks dari gambar menggunakan Aspose OCR dan mendapatkan hasil
  JSON.
og_title: Cara Melakukan OCR di C# – Panduan Cepat
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Cara Melakukan OCR di C# – Ekstrak Teks dari Gambar Menggunakan Aspose OCR
url: /id/net/text-recognition/how-to-perform-ocr-in-c-extract-text-from-image-using-aspose/
---

unchanged placeholders.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Melakukan OCR di C# – Ekstrak Teks dari Gambar Menggunakan Aspose OCR

Pernah bertanya-tanya **cara melakukan OCR** di C# tanpa membuat frustasi? Anda tidak sendirian. Banyak pengembang menemui kesulitan ketika harus mengambil teks dari formulir yang dipindai, kwitansi, atau catatan tulisan tangan. Kabar baiknya? Dengan Aspose OCR Anda dapat **mengekstrak teks dari gambar** dalam hanya beberapa baris kode.

Dalam tutorial ini kami akan membimbing Anda melalui contoh lengkap yang siap dijalankan, yang menunjukkan secara tepat cara memuat model bahasa, memberi gambar, menjalankan mesin pengenalan, dan menyerialkan hasilnya ke JSON. Pada akhir tutorial Anda akan memiliki potongan kode yang dapat digunakan kembali dan dapat dimasukkan ke proyek .NET mana pun, serta beberapa tip berguna untuk skenario dunia nyata.

## Apa yang Anda Butuhkan

- .NET 6.0 atau lebih baru (kode berfungsi pada .NET Framework juga, tetapi .NET 6+ disarankan)
- Paket NuGet Aspose.OCR yang valid (`Install-Package Aspose.OCR`)
- File gambar (JPEG, PNG, BMP, dll.) yang berisi teks yang ingin Anda baca
- Lingkungan pengembangan C# dasar (Visual Studio, Rider, atau VS Code)

Itu saja—tidak ada mesin OCR tambahan, tidak ada DLL native, hanya pustaka managed yang bersih.

## Langkah 1: Buat Instance OCR Engine – Cara Melakukan OCR

Hal pertama yang Anda butuhkan adalah objek `OcrEngine`. Anggaplah itu sebagai otak yang akan melakukan pekerjaan berat.

```csharp
using Aspose.OCR;
using Aspose.OCR.Output;

// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();
```

> **Mengapa langkah ini penting:** `OcrEngine` mengenkapsulasi semua opsi konfigurasi. Tanpanya Anda tidak dapat memberi tahu pustaka bahasa mana yang akan digunakan atau di mana menemukan gambar.

## Langkah 2: Muat Model Bahasa – Ekstrak Teks dari Gambar

Aspose OCR dilengkapi dengan beberapa paket bahasa. Untuk kebanyakan dokumen berbahasa Inggris, Anda akan memuat model Inggris bawaan.

```csharp
// Load the English language model
ocrEngine.LoadLanguage(LanguageModel.English);
```

> **Tip pro:** Jika Anda perlu mengenali bahasa Prancis, Jerman, atau bahasa khusus, ganti `LanguageModel.English` dengan nilai enum yang sesuai atau muat file model khusus.

## Langkah 3: Berikan Gambar yang Akan Diproses – Cara Melakukan OCR

Sekarang arahkan mesin ke file yang ingin Anda baca. Pembantu `ImageStream.FromFile` membaca gambar ke dalam format yang dipahami oleh OCR engine.

```csharp
// Supply the image (replace the path with your own file location)
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/form.jpg");
```

> **Kasus khusus:** Gambar berukuran besar (>5 MB) dapat memperlambat proses. Pertimbangkan untuk mengubah ukuran atau mengompresnya sebelum memberi ke mesin.

## Langkah 4: Jalankan Pengenalan – Ekstrak Teks dari Gambar

Setelah semuanya disiapkan, Anda akhirnya dapat menjalankan operasi OCR. Metode `Recognize` mengembalikan objek `OcrResult` yang berisi teks, kotak pembatas, dan skor kepercayaan.

```csharp
// Perform OCR and capture the result
OcrResult ocrResult = ocrEngine.Recognize();
```

> **Apa yang terjadi di balik layar?** Mesin menjalankan jaringan saraf yang dilatih pada jutaan karakter, kemudian memetakan setiap glyph yang terdeteksi ke teks Unicode.

## Langkah 5: Konversi Hasil ke JSON – Cara Melakukan OCR

Sebagian besar API modern mengharapkan JSON, jadi mari kita serialisasikan hasilnya. Metode ekstensi `ToJson` memberikan Anda string yang diformat dengan baik.

```csharp
// Serialize the OCR result to JSON
string jsonResult = ocrResult.ToJson();
```

Payload JSON tipikal terlihat seperti ini (dipotong untuk singkat):

```json
{
  "Text": "Invoice #12345\nDate: 01/02/2026\nTotal: $250.00",
  "Words": [
    {
      "Value": "Invoice",
      "BoundingBox": { "X": 12, "Y": 34, "Width": 80, "Height": 20 },
      "Confidence": 0.98
    },
    // ... more words ...
  ]
}
```

> **Mengapa JSON?** JSON bersifat netral bahasa, mudah dicatat, dan sempurna untuk dikirim ke layanan hilir seperti Elasticsearch atau REST API.

## Langkah 6: Output JSON – Ekstrak Teks dari Gambar

Akhirnya, tulis JSON ke konsol (atau ke file, atau ke basis data—sesuai pilihan Anda).

```csharp
// Print the JSON result to the console
Console.WriteLine(jsonResult);
```

Menjalankan program harus menampilkan struktur JSON lengkap, mengonfirmasi bahwa Anda telah berhasil **mengekstrak teks dari gambar**.

## Contoh Lengkap yang Berfungsi

Berikut adalah kode lengkap yang dapat Anda salin‑tempel ke proyek konsol baru. Tidak ada bagian yang hilang—semua yang Anda butuhkan ada di sini.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create an OCR engine instance
            OcrEngine ocrEngine = new OcrEngine();

            // Step 2: Load the English language model for recognition
            ocrEngine.LoadLanguage(LanguageModel.English);

            // Step 3: Provide the image to be processed
            // Replace the path with the actual location of your image file
            ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/form.jpg");

            // Step 4: Perform OCR on the image
            OcrResult ocrResult = ocrEngine.Recognize();

            // Step 5: Convert the recognition result to JSON (includes text, bounding boxes, confidence scores)
            string jsonResult = ocrResult.ToJson();

            // Step 6: Output the JSON result
            Console.WriteLine(jsonResult);
        }
    }
}
```

> **Output yang diharapkan:** String JSON yang berisi teks yang dikenali, kotak pembatas setiap kata, dan nilai kepercayaan. Jika gambar jelas dan model bahasa cocok, skor kepercayaan biasanya di atas 0,90.

## Pertanyaan Umum & Hal-hal yang Perlu Diwaspadai

- **Bagaimana jika gambar diputar?**  
  Aspose OCR dapat mendeteksi orientasi secara otomatis, tetapi untuk hasil terbaik Anda mungkin memutar gambar terlebih dahulu menggunakan `System.Drawing` atau `ImageSharp` sebelum memberikannya ke mesin.

- **Bisakah saya memproses PDF secara langsung?**  
  Tidak secara langsung. Konversi setiap halaman PDF menjadi gambar (misalnya, menggunakan Aspose.PDF) lalu beri gambar tersebut ke OCR engine.

- **Bagaimana cara menangani formulir multi‑halaman?**  
  Lakukan loop pada setiap gambar halaman, jalankan langkah yang sama, dan gabungkan hasil JSON ke dalam satu koleksi.

- **Apakah ada cara membatasi output hanya ke teks biasa?**  
  Ya—gunakan properti `ocrResult.Text` alih-alih `ToJson()` jika Anda hanya membutuhkan string yang digabungkan.

## Tips Pro untuk OCR Siap Produksi

1. **Cache model bahasa** – Memuat model tidak mahal, tetapi jika Anda memproses ratusan gambar per detik, pertahankan satu instance `OcrEngine` tetap hidup daripada membuatnya kembali setiap kali.
2. **Sesuaikan ambang kepercayaan** – Filter kata dengan `Confidence < 0.80` untuk mengurangi noise.
3. **Pemrosesan batch** – Untuk beban kerja besar, pertimbangkan untuk mengantri jalur gambar dan memprosesnya secara asynchronous dengan `Task.Run`.
4. **Logging** – Simpan JSON mentah bersama gambar asli untuk jejak audit; ini sangat berharga saat men-debug kesalahan pengenalan.

## Kesimpulan

Anda kini memiliki solusi end‑to‑end yang jelas untuk **cara melakukan OCR** di C# dan **mengekstrak teks dari file gambar** menggunakan pustaka Aspose OCR. Contoh ini memandu Anda melalui pembuatan engine, pemuatan bahasa, pemberian gambar, pengenalan, serialisasi JSON, dan output—semuanya dalam satu program yang dapat dijalankan.

Apa selanjutnya? Cobalah mengganti model Inggris dengan bahasa lain, bereksperimen dengan format gambar yang berbeda, atau integrasikan payload JSON ke dalam indeks pencarian. Tidak ada batasan, dan dengan blok bangunan ini Anda siap menghadapi tantangan ekstraksi teks apa pun yang datang.

Selamat coding, semoga hasil OCR Anda selalu akurat! 

![Diagram illustrating how to perform OCR in C# with Aspose OCR library](https://example.com/ocr-diagram.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}