---
category: general
date: 2026-03-26
description: Mengenali teks dari PNG dan mengekstrak data struk menggunakan Aspose
  OCR dalam C#. Mengonversi gambar ke JSON‑L dan memproses struk dengan OCR dalam
  contoh lengkap.
draft: false
keywords:
- recognize text from png
- extract text from receipt
- convert image to jsonl
- process receipt with ocr
- aspose ocr example c#
language: id
og_description: Mengenali teks dari PNG dan mengubah struk menjadi JSON‑L dengan Aspose
  OCR di C#. Kode lengkap langkah demi langkah dan tips.
og_title: Mengenali teks dari PNG – Panduan Aspose OCR C#
tags:
- Aspose OCR
- C#
- JSONL
- Receipt Processing
title: Mengenali teks dari PNG – Tutorial Aspose OCR C# JSON‑L
url: /id/net/text-recognition/recognize-text-from-png-aspose-ocr-c-json-l-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Mengenali teks dari png – Panduan Lengkap Aspose OCR C# 

Pernahkah Anda perlu **recognize text from png** file tetapi tidak yakin perpustakaan mana yang akan memberi Anda hasil bersih, baris‑per‑baris? Anda tidak sendirian. Dalam banyak aplikasi usaha kecil, kwitansi berada sebagai gambar PNG, dan mengekstrak jumlah, tanggal, atau nama pedagang adalah masalah harian.  

Berita baik? Dengan beberapa baris C# dan perpustakaan **Aspose OCR** Anda dapat **extract text from receipt**, lalu **convert image to jsonl** untuk analitik selanjutnya. Dalam tutorial ini kami akan membahas seluruh alur—memuat PNG, menjalankan OCR, dan menulis setiap baris ke file JSON‑L—sehingga Anda dapat **process receipt with OCR** segera.

Kami akan membahas semua yang Anda butuhkan: paket NuGet yang diperlukan, program lengkap yang dapat dijalankan, penjelasan mengapa setiap langkah penting, dan beberapa tips praktis yang akan Anda hargai ketika kwitansi menjadi berantakan. Tidak diperlukan dokumentasi eksternal; cukup salin‑tempel, jalankan, dan sesuaikan.

---

## Apa yang Akan Anda Pelajari

- Bagaimana cara **recognize text from png** menggunakan `Aspose.OCR`.
- Bagaimana cara **extract text from receipt** objek baris dan menangkap skor kepercayaan.
- Bagaimana cara **convert image to jsonl** sehingga setiap baris OCR menjadi objek JSON terpisah.
- Bagaimana cara **process receipt with OCR** end‑to‑end, menangani kasus tepi seperti gambar kosong atau baris dengan kepercayaan rendah.
- Tips untuk memecahkan masalah OCR umum dan meningkatkan akurasi.

### Prasyarat

- .NET 6.0 atau lebih baru (kode ini bekerja dengan .NET Core dan .NET Framework juga).
- Visual Studio 2022 atau IDE apa pun yang Anda sukai.
- Lisensi Aspose OCR yang valid (Anda dapat memulai dengan lisensi sementara gratis dari Aspose.com).
- Contoh kwitansi yang disimpan sebagai `receipt.png` dalam folder yang Anda kontrol.

---

## Langkah 1: Recognize text from png dengan Aspose OCR

Hal pertama yang kita butuhkan adalah `OcrEngine` yang sudah diinisialisasi. Objek ini menyimpan pengaturan mesin OCR (bahasa, mode deteksi, dll.). Secara default menggunakan bahasa Inggris dan secara otomatis mendeteksi tata letak halaman, yang bekerja baik untuk kebanyakan kwitansi.

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;
using System;
using System.IO;

class JsonLExample
{
    static void Main()
    {
        // Initialize the OCR engine – this is where Aspose loads its models.
        OcrEngine ocrEngine = new OcrEngine();

        // Load the PNG image that contains the receipt.
        string imagePath = @"YOUR_DIRECTORY\receipt.png";
        OcrImage receiptImage = OcrImage.FromFile(imagePath);

        // Run OCR and get the result object.
        OcrResult ocrResult = ocrEngine.Recognize(receiptImage);
```

**Mengapa ini penting:**  
`OcrEngine` adalah komponen utama; membuatnya sekali dan menggunakan kembali pada banyak gambar mengurangi beban memori. Jika Anda membutuhkan bahasa lain (mis., kwitansi bahasa Spanyol), Anda dapat mengatur `ocrEngine.Language = OcrLanguage.Spanish;` sebelum memanggil `Recognize`.

---

## Langkah 2: Extract text from receipt lines

`OcrResult` berisi koleksi bernama `Lines`. Setiap baris menyimpan teks mentah dan skor kepercayaan (0‑100). Mengambilnya memberi Anda kontrol granular—Anda dapat membuang baris dengan kepercayaan rendah atau menandainya untuk tinjauan manual.

```csharp
        // Prepare to write each line as a JSON‑L record.
        string jsonlPath = @"YOUR_DIRECTORY\receipt.jsonl";

        using (StreamWriter jsonLineWriter = new StreamWriter(jsonlPath))
        {
            foreach (var line in ocrResult.Lines)
            {
                // Build a simple JSON object for the line.
                string json = $"{{\"text\":\"{EscapeJson(line.Text)}\",\"confidence\":{line.Confidence}}}";
                jsonLineWriter.WriteLine(json);
            }
        }

        Console.WriteLine("JSON‑L file written to " + jsonlPath);
    }

    // Helper to escape quotes and backslashes in JSON strings.
    private static string EscapeJson(string s) => s.Replace("\\", "\\\\").Replace("\"", "\\\"");
}
```

**Mengapa kami escape JSON:**  
Teks kwitansi dapat berisi kutipan (`"`) atau backslash (`\`) yang dapat merusak string JSON sederhana. Metode `EscapeJson` menjamin baris JSON yang valid.

**Seperti apa outputnya:**  

```
{"text":"Store XYZ","confidence":98.5}
{"text":"Date: 2024-07-15","confidence":97.2}
{"text":"Total $23.45","confidence":99.1}
```

Setiap baris adalah catatan terpisah, sempurna untuk streaming ke data lake atau memberi model machine‑learning.

---

## Langkah 3: Convert image to JSONL – menangani kasus tepi

Saat Anda memproses sekumpulan kwitansi, beberapa gambar mungkin kosong, rusak, atau memiliki skor kepercayaan yang sangat rendah. Mari buat alur kerja lebih kuat.

```csharp
        // After OCR, check if any lines were detected.
        if (ocrResult.Lines.Count == 0)
        {
            Console.WriteLine("Warning: No text detected. Verify the image path and quality.");
            return;
        }

        // Optional: filter out lines with confidence below a threshold.
        const double minConfidence = 80.0;
        foreach (var line in ocrResult.Lines)
        {
            if (line.Confidence < minConfidence)
                continue; // skip noisy line
            // write as before...
        }
```

**Mengapa filter:**  
Kwitansi yang dicetak pada kertas pudar dapat menghasilkan karakter acak dengan kepercayaan rendah. Menghapus apa pun di bawah 80 % biasanya menghilangkan noise sambil mempertahankan data berguna.

---

## Langkah 4: Process receipt with OCR – contoh end‑to‑end

Menggabungkan semuanya, berikut program **lengkap, siap‑jalankan**. Ganti `YOUR_DIRECTORY` dengan folder yang berisi file PNG Anda.

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;
using System;
using System.IO;

class JsonLExample
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Load receipt PNG
        string imagePath = @"YOUR_DIRECTORY\receipt.png";
        OcrImage receiptImage = OcrImage.FromFile(imagePath);

        // 3️⃣ Perform OCR
        OcrResult ocrResult = ocrEngine.Recognize(receiptImage);

        // 4️⃣ Verify we got something back
        if (ocrResult.Lines.Count == 0)
        {
            Console.WriteLine("❗ No text found – check the image quality.");
            return;
        }

        // 5️⃣ Write each line to a JSON‑L file
        string jsonlPath = @"YOUR_DIRECTORY\receipt.jsonl";
        using (StreamWriter writer = new StreamWriter(jsonlPath))
        {
            const double minConfidence = 80.0;
            foreach (var line in ocrResult.Lines)
            {
                if (line.Confidence < minConfidence) continue; // skip low‑confidence

                string json = $"{{\"text\":\"{EscapeJson(line.Text)}\",\"confidence\":{line.Confidence}}}";
                writer.WriteLine(json);
            }
        }

        Console.WriteLine($"✅ JSON‑L written to: {jsonlPath}");
    }

    // Helper to make JSON safe
    private static string EscapeJson(string s) => s.Replace("\\", "\\\\").Replace("\"", "\\\"");
}
```

**Menjalankan kode:**  
1. Buka terminal di folder proyek.  
2. `dotnet add package Aspose.OCR` – menginstal perpustakaan.  
3. `dotnet run` – Anda akan melihat pesan sukses dan file `receipt.jsonl` muncul.

**Hasil yang diharapkan:** File JSON berbaris di mana setiap baris mencerminkan baris kwitansi, lengkap dengan skor kepercayaan. Anda kini dapat mengalirkan file ini ke Power BI, Elastic, atau alat analitik apa pun yang memahami JSON‑L.

---

## Kesalahan Umum & Tips Pro

| Issue | Why it Happens | Quick Fix |
|-------|----------------|-----------|
| **Blank output** | Path gambar salah atau file bukan PNG. | Periksa kembali path, gunakan `File.Exists(imagePath)`. |
| **Garbage characters** | DPI rendah atau PNG yang terlalu terkompresi. | Gunakan pemindaian setidaknya 300 dpi; hindari kompresi JPEG yang agresif. |
| **Too many low‑confidence lines** | Kwitansi dicetak pada kertas termal yang memudar. | Tingkatkan ambang `minConfidence` atau pra‑proses gambar (kontras/threshold). |
| **JSON parsing errors** | Kutipan yang tidak di‑escape dalam teks kwitansi. | Pertahankan helper `EscapeJson` atau beralih ke `System.Text.Json` untuk serialisasi yang kuat. |

**Tips Pro:** Jika Anda perlu mengekstrak bidang spesifik (mis., total amount), jalankan regex sederhana pada setiap `line.Text` setelah Anda memiliki file JSON‑L. Ini menjaga OCR terpisah dari logika bisnis dan memudahkan debugging.

---

## Memperluas Solusi

- **Batch processing:** Bungkus logika `Main` dalam `foreach` untuk semua file PNG di sebuah direktori.
- **Multi‑language support:** Set `ocrEngine.Language = OcrLanguage.Spanish;` (atau bahasa lain yang didukung) sebelum `Recognize`.
- **Structured output:** Alih-alih JSON baris‑per‑baris, bangun objek `Receipt` dengan properti `Date`, `Merchant`, `Total`, kemudian serialisasi sekali.

Semua variasi ini tetap **convert image to jsonl** di inti, sehingga Anda dapat mengganti konsumen downstream tanpa menyentuh bagian OCR.

---

## Kesimpulan

Kami baru saja menunjukkan cara **recognize text from png** file menggunakan Aspose OCR, **extract text from receipt**, dan **convert image to jsonl** untuk pemrosesan downstream yang mudah. Program C# lengkap dan mandiri ini memperlihatkan seluruh alur kerja—dari memuat PNG, menangani kasus tepi, hingga menulis file JSON‑L yang bersih—sehingga Anda dapat segera **process receipt with OCR** dalam proyek Anda.

Cobalah dengan beberapa contoh kwitansi, sesuaikan ambang kepercayaan, dan Anda akan melihat seberapa cepat tumpukan gambar berisik berubah menjadi data terstruktur siap untuk analitik. Setelah Anda nyaman, jelajahi batch processing atau tambahkan model ML kecil untuk mengklasifikasikan kategori pengeluaran secara otomatis.

Ada pertanyaan, atau menemukan trik cerdas? Tinggalkan komentar di bawah—selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}