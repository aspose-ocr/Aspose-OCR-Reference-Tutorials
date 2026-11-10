---
category: general
date: 2026-01-01
description: Tutorial OCR C# yang menunjukkan cara mengekstrak teks, memuat gambar
  untuk OCR, dan menulis JSON ke file menggunakan Aspose.OCR – panduan langkah demi
  langkah.
draft: false
keywords:
- c# OCR tutorial
- how to extract text
- write json to file
- load image for OCR
- OCR image to JSON
language: id
og_description: Tutorial OCR c# yang memandu Anda melalui cara mengekstrak teks dari
  gambar, memuat gambar untuk OCR, dan menulis JSON ke file menggunakan Aspose.OCR.
og_title: tutorial OCR c# – Ekstrak Teks dan Ekspor ke JSON
tags:
- Aspose.OCR
- C#
- Text Extraction
title: Tutorial OCR c# – Ekstrak Teks dari Gambar dan Ekspor ke JSON
url: /id/net/text-recognition/c-ocr-tutorial-extract-text-from-images-and-export-to-json/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# OCR tutorial – Ekstrak Teks dari Gambar dan Ekspor ke JSON

ern bertanya‑tanya bagaimana cara mengekstrak teks dari faktur yang dipindai tanpa menghabiskan berjam‑jam menulis parser khusus? Anda tidak sendirian. Dalam **c# OCR tutorial** ini kami akan menunjukkan secara tepat cara memuat gambar untuk OCR, menjalankan mesin pengenalan, dan kemudian **menulis JSON ke file** sehingga Anda dapat mengirim data ke sistem hilir.

Bayangkan Anda memiliki folder berisi kwitansi, masing‑masing bernama `receipt1.png`, `receipt2.png`, dan Anda membutuhkan cara cepat untuk mengubahnya menjadi catatan JSON yang dapat dicari. Itulah masalah yang akan kami selesaikan, dan pada akhir Anda akan memiliki aplikasi konsol siap‑jalankan yang melakukan hal itu. Tanpa dependensi tambahan selain Aspose.OCR, dan tanpa sulap—hanya langkah‑langkah yang jelas dan dapat direproduksi.

> **Apa yang akan Anda pelajari**
> - Cara **load image for OCR** menggunakan Aspose.OCR.
> - Cara terbaik untuk **how to extract text** dan mendapatkan skor kepercayaan.
> - Mengonversi hasil OCR menjadi payload **OCR image to JSON** yang terstruktur rapi.
> - Aman **write JSON to file** dan memverifikasi output.

## Prasyarat

- .NET 6 SDK atau yang lebih baru (kode ini juga berfungsi di .NET Core).  
- Visual Studio 2022 atau editor apa pun yang Anda sukai.  
- Paket NuGet Aspose.OCR (`Install-Package Aspose.OCR`).  
- File gambar (PNG, JPG, BMP) yang ingin Anda proses – untuk demo kami akan menggunakan `invoice.png`.

Jika Anda kekurangan salah satu dari ini, unduh SDK dari situs Microsoft dan tambahkan paket NuGet melalui Package Manager Console:

```powershell
Install-Package Aspose.OCR
```

Sekarang dasar‑dasarnya sudah siap, mari kita selami implementasi sebenarnya.

## Langkah 1: c# OCR tutorial – Inisialisasi Mesin OCR

Sebelum kita dapat **load image for OCR**, kita memerlukan sebuah instance mesin yang akan menggerakkan proses pengenalan. Kelas `OcrEngine` ringan, namun praktik yang baik adalah membungkusnya dalam blok `using` sehingga sumber daya dilepaskan dengan cepat.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class JsonExportDemo
{
    static void Main()
    {
        // Step 1: Create the OCR engine – this is the heart of the c# OCR tutorial
        var ocrEngine = new OcrEngine();

        // The rest of the steps follow…
```

*Pro tip:* Jika Anda berencana memproses banyak gambar dalam satu batch, gunakan kembali instance `OcrEngine` yang sama alih‑alih membuat yang baru setiap kali. Ini mengurangi beban memori dan mempercepat proses.

## Langkah 2: Muat gambar untuk OCR

Sekarang kita benar‑benar **load image for OCR**. Aspose.OCR mendukung berbagai format, sehingga Anda dapat menunjuk ke PNG, JPEG, atau bahkan TIFF multi‑halaman. Metode `OcrImage.FromFile` membaca file dan menyiapkannya untuk pengenalan.

```csharp
        // Step 2: Load the image you want to recognize
        // Replace YOUR_DIRECTORY with the folder that holds your invoice.png
        var imagePath = @"YOUR_DIRECTORY/invoice.png";
        var ocrImage = OcrImage.FromFile(imagePath);
```

> **Mengapa ini penting:** Memuat gambar secara terpisah memungkinkan Anda memeriksa dimensi, DPI, atau bahkan melakukan pra‑proses (misalnya binarisasi) sebelum mengirimnya ke mesin. Jika gambar rusak, `FromFile` akan melempar pengecualian yang jelas, yang dapat Anda tangkap dan log.

## Langkah 3: Cara mengekstrak teks – Jalankan pengenalan

Dengan gambar di tangan, kita akhirnya dapat **how to extract text** darinya. Metode `Recognize` mengembalikan objek `OcrResult` yang berisi tidak hanya teks biasa tetapi juga data posisi dan skor kepercayaan untuk setiap kata.

```csharp
        // Step 3: Perform OCR – this is the core of how to extract text
        var ocrResult = ocrEngine.Recognize(ocrImage);
```

*Edge case:* Beberapa PDF mengandung lapisan teks tak terlihat. Jika Anda memberi halaman PDF yang dirender sebagai gambar, mesin mungkin tidak melihat apa‑apa. Dalam kasus tersebut, pertimbangkan menggunakan Aspose.PDF untuk mengekstrak lapisan tersembunyi terlebih dahulu, kemudian baru beralih ke OCR bila diperlukan.

## Langkah 4: OCR image to JSON – Konversi hasil

Kelas `OcrResult` menyediakan helper `ToJson()` yang nyaman untuk menyerialkan seluruh set hasil—termasuk kotak pembatas setiap kata dan skor kepercayaan—ke dalam string JSON. Ini cara paling bersih untuk mencapai **OCR image to JSON** tanpa menulis serializer sendiri.

```csharp
        // Step 4: Convert the OCR result to JSON (includes words, confidence, locations)
        string jsonResult = ocrResult.ToJson();
```

Jika Anda lebih suka skema khusus, Anda dapat mengiterasi `ocrResult.Words` dan membangun objek Anda sendiri, tetapi untuk kebanyakan skenario JSON bawaan sudah cukup dan sudah terstruktur dengan baik.

## Langkah 5: Tulis JSON ke file

Kini tiba bagian akhir dari puzzle: menyimpan payload JSON. Metode `File.WriteAllText` memastikan file dibuat (atau ditimpa) secara atomik. Pastikan direktori target ada, bila tidak Anda akan mendapat `DirectoryNotFoundException`.

```csharp
        // Step 5: Save the JSON output – this demonstrates write JSON to file
        var jsonPath = @"YOUR_DIRECTORY/invoice.json";
        File.WriteAllText(jsonPath, jsonResult);
```

*Tip:* Jika Anda membutuhkan UTF‑8 dengan BOM atau encoding lain, gunakan overload yang menerima argumen `Encoding`.

## Langkah 6: Verifikasi output

Sebuah `Console.WriteLine` singkat memberi tahu kita proses selesai dengan sukses. Anda juga dapat membuka file JSON di penampil untuk mengonfirmasi strukturnya.

```csharp
        // Step 6: Inform the user that the JSON file has been saved
        Console.WriteLine($"JSON saved to {jsonPath}");
    }
}
```

### Potongan JSON yang Diharapkan

```json
{
  "Text": "Invoice #12345\nDate: 2025-12-31\nTotal: $250.00",
  "Words": [
    { "Text": "Invoice", "Confidence": 0.98, "Location": { "X": 10, "Y": 15, "Width": 80, "Height": 20 } },
    { "Text": "#12345", "Confidence": 0.96, "Location": { "X": 95, "Y": 15, "Width": 60, "Height": 20 } }
    // … more words …
  ]
}
```

JSON mencakup lokasi setiap kata, yang berguna bila Anda nanti ingin menyorot teks dalam UI.

## Contoh Lengkap yang Berfungsi

Berikut adalah program lengkap yang siap disalin‑tempel. Ganti `YOUR_DIRECTORY` dengan jalur sebenarnya tempat gambar Anda berada.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class JsonExportDemo
{
    static void Main()
    {
        // Step 1: Initialize the OCR engine
        var ocrEngine = new OcrEngine();

        // Step 2: Load the image you want to recognize
        var imagePath = @"YOUR_DIRECTORY/invoice.png";
        var ocrImage = OcrImage.FromFile(imagePath);

        // Step 3: Perform OCR – how to extract text
        var ocrResult = ocrEngine.Recognize(ocrImage);

        // Step 4: Convert the result to JSON (OCR image to JSON)
        string jsonResult = ocrResult.ToJson();

        // Step 5: Write JSON to file – write JSON to file
        var jsonPath = @"YOUR_DIRECTORY/invoice.json";
        File.WriteAllText(jsonPath, jsonResult);

        // Step 6: Verify
        Console.WriteLine($"JSON saved to {jsonPath}");
    }
}
```

Jalankan program (`dotnet run` dari folder proyek) dan Anda akan menemukan `invoice.json` berdampingan dengan PNG asli Anda.

## Kesalahan Umum & Cara Menghindarinya

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **FileNotFoundException** saat memuat gambar | Salah ketik jalur atau file tidak ada | Gunakan `Path.Combine` dan periksa `File.Exists` sebelum memanggil `FromFile`. |
| **Low confidence scores** | Kualitas gambar buruk, DPI rendah | Pra‑proses dengan `ocrImage.AdjustContrast` atau tingkatkan gambar ke 300 DPI. |
| **JSON file empty** | `ocrResult` mengembalikan null (mesin gagal) | Pastikan format gambar didukung dan lisensi (jika ada) diterapkan dengan benar. |
| **Performance bottleneck on large batches** | Membuat ulang `OcrEngine` tiap iterasi | Gunakan kembali satu instance `OcrEngine` untuk seluruh batch, disposes hanya di akhir. |

## Langkah Selanjutnya

Sekarang Anda telah menguasai **c# OCR tutorial**, Anda mungkin ingin:

- **Batch process** seluruh folder dan menggabungkan file JSON menjadi satu basis data.
- **Integrate** output dengan Azure Cognitive Search untuk PDF yang dapat dicari.
- **Add language support** dengan mengatur `ocrEngine.Language = OcrLanguage.Spanish` (atau bahasa lain yang didukung).
- **Post‑process** JSON untuk mengekstrak tabel atau pasangan kunci‑nilai menggunakan ekspresi reguler.

Setiap ekstensi ini dibangun di atas konsep inti yang telah kami bahas: memuat gambar untuk OCR, mengekstrak teks, mengonversi ke JSON, dan menulis JSON ke disk.

---

### Kesimpulan

Dalam **c# OCR tutorial** ini kami menelusuri setiap langkah yang diperlukan untuk **load image for OCR**, **how to extract text**, mengubah hasil menjadi payload **OCR image to JSON**, dan akhirnya **write JSON to file**. Contoh kode lengkap siap disisipkan ke proyek .NET apa pun, dan penjelasan memberi Anda konteks untuk menyesuaikan solusi dengan skenario dunia nyata.

Cobalah dengan kumpulan kwitansi atau faktur Anda sendiri—sesuaikan pra‑proses gambar, bereksperimen dengan bahasa berbeda, dan saksikan output JSON berkembang. Jika Anda menemui kendala, tinjau kembali tabel kesalahan atau tinggalkan komentar di bawah. Selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}