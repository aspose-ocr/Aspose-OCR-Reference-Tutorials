---
category: general
date: 2026-01-01
description: praproses gambar OCR untuk meningkatkan akurasi. Pelajari cara mengenali
  teks pada gambar, meningkatkan akurasi OCR, memuat gambar OCR, dan menampilkan teks
  OCR menggunakan Aspose OCR.
draft: false
keywords:
- preprocess image ocr
- recognize text image
- improve ocr accuracy
- display ocr text
- load image ocr
language: id
og_description: praproses OCR gambar untuk meningkatkan akurasi. Panduan ini menunjukkan
  cara mengenali teks pada gambar, memuat OCR gambar, menerapkan filter, dan menampilkan
  teks OCR.
og_title: praproses OCR gambar di C# – Tingkatkan Akurasi dengan Aspose OCR
tags:
- Aspose OCR
- C#
- Image preprocessing
title: praproses gambar OCR di C# – Tingkatkan akurasi dengan Aspose OCR
url: /id/net/ocr-optimization/preprocess-image-ocr-in-c-boost-accuracy-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# preprocess image ocr in C# – Tingkatkan Akurasi dengan Aspose OCR

Pernah bertanya-tanya bagaimana **preprocess image ocr** sehingga mesin benar‑benar membaca apa yang ada di halaman? Anda tidak sendirian—banyak pengembang menemui kebuntuan ketika pemindaian yang berisik dan miring menolak bekerja. Kabar baiknya, beberapa langkah pra‑pemrosesan cerdas dapat mengubah gambar zona bencana menjadi teks bersih yang dapat dibaca.

Dalam tutorial ini kita akan menelusuri contoh lengkap yang siap dijalankan untuk **recognize text image** file, **improve OCR accuracy**, dan akhirnya **display OCR text** di konsol. Pada akhir tutorial Anda akan tahu cara **load image OCR** aset, menambahkan filter seperti koreksi kemiringan dan pengurangan noise, serta mendapatkan hasil yang dapat diandalkan—semua dengan Aspose.OCR untuk .NET.

## Apa yang Akan Anda Pelajari

- Cara membuat instance `OcrEngine` dan mengonfigurasi filter pra‑pemrosesan.  
- Mengapa filter koreksi kemiringan dan pengurangan noise penting untuk **improve OCR accuracy**.  
- Kode tepat untuk **load image ocr** file dan menjalankan pengenalan.  
- Cara **display OCR text** dengan cara yang ramah pengguna.  
- Tips, jebakan, dan penyesuaian opsional yang dapat Anda terapkan dalam proyek dunia nyata.

### Prasyarat

- .NET 6+ (atau .NET Framework 4.7+) terpasang di mesin Anda.  
- Lisensi Aspose.OCR (versi percobaan gratis cukup untuk demo ini).  
- Pengetahuan dasar C#—tidak memerlukan trik lanjutan.  

Jika ada yang belum familiar, cukup jeda dan pasang komponen yang kurang; sisanya mengasumsikan semuanya sudah siap.

---

## preprocess image ocr – Menyiapkan Filter

Hal pertama yang perlu Anda pahami adalah **mengapa preprocessing penting**. Mesin OCR hebat dalam membaca teks yang tajam dan lurus, tetapi pemindaian dunia nyata sering mengalami rotasi, blur, atau noise latar belakang. Dengan memberi mesin gambar yang sudah dibersihkan, peluang transkripsi yang benar meningkat secara signifikan.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;

class PreprocessDemo
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine.
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Add preprocessing filters.
        //    • SkewCorrectionFilter: straightens tilted text.
        //    • DenoiseFilter: removes speckles and grain.
        ocrEngine.Settings.PreprocessingFilters.Add(new SkewCorrectionFilter());
        ocrEngine.Settings.PreprocessingFilters.Add(new DenoiseFilter());

        // 3️⃣ (Optional) Fine‑tune filter parameters.
        // ((SkewCorrectionFilter)ocrEngine.Settings.PreprocessingFilters[0]).MaxAngle = 25;

        // 4️⃣ Load the image you want to run OCR on.
        OcrImage inputImage = OcrImage.FromFile(@"YOUR_DIRECTORY/skewed_noisy.jpg");

        // 5️⃣ Run the recognition.
        OcrResult ocrResult = ocrEngine.Recognize(inputImage);

        // 6️⃣ Show the recognized text.
        Console.WriteLine("Corrected text:");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Apa yang terjadi di sini?**  
- **Langkah 1** membuat engine—inti dari pustaka Aspose OCR.  
- **Langkah 2** menambahkan dua filter. `SkewCorrectionFilter` memutar gambar kembali ke posisi horizontal, sementara `DenoiseFilter` menghaluskan noise pada tingkat piksel.  
- **Langkah 3** bersifat opsional namun berguna; Anda dapat membatasi sudut maksimum yang akan dikoreksi engine, sehingga menghindari over‑rotation pada halaman yang sudah lurus.  
- **Langkah 4** adalah tempat Anda **load image OCR** data. Ganti `YOUR_DIRECTORY/skewed_noisy.jpg` dengan path ke file uji Anda.  
- **Langkah 5** menjalankan OCR dan menghasilkan `OcrResult`.  
- **Langkah 6** **display OCR text** di konsol, memberikan umpan balik langsung.

> **Pro tip:** Jika output masih berisi karakter kacau, coba tingkatkan `MaxAngle` atau tambahkan `ContrastFilter` sebelum langkah denoise.

---

## recognize text image – Memuat File dengan Benar

Salah satu hal yang sering membuat bingung adalah **load image ocr** dengan format atau DPI yang salah. Aspose.OCR mendukung PNG, JPEG, TIFF, BMP, dan bahkan gambar berbasis PDF. Namun, engine bekerja paling baik dengan DPI 300 atau lebih tinggi untuk dokumen cetak.

```csharp
// Example: loading a high‑resolution PNG
string imagePath = @"C:\Images\invoice_300dpi.png";
OcrImage highRes = OcrImage.FromFile(imagePath);
```

Jika Anda menangani TIFF multi‑halaman, Anda dapat melakukan loop pada setiap frame:

```csharp
var tiff = Aspose.OCR.ImageProcessing.TiffImage.FromFile(@"multi_page.tif");
foreach (var frame in tiff.Frames)
{
    OcrResult pageResult = ocrEngine.Recognize(frame);
    Console.WriteLine(pageResult.Text);
}
```

**Mengapa ini penting untuk improve OCR accuracy?** Resolusi yang lebih tinggi mempertahankan bentuk setiap karakter, memberi pengenalan lebih banyak titik data. Gambar dengan DPI rendah sering menghasilkan glyph yang menyatu atau terputus, yang akan disalahartikan engine.

---

## improve OCR accuracy – Menyesuaikan Parameter Filter

Pengaturan filter default adalah titik awal yang baik, tetapi Anda dapat mengoptimalkan kinerjanya lebih jauh.

| Filter | Properti Kunci | Nilai Tipikal | Kapan Disesuaikan |
|--------|----------------|---------------|-------------------|
| `SkewCorrectionFilter` | `MaxAngle` | `15` (derajat) | Gambar yang sangat miring (hingga 30°). |
| `DenoiseFilter` | `Strength` | `0.5` (0‑1) | Scan sangat berisik; naikkan menjadi `0.8`. |
| `ContrastFilter` (opsional) | `Level` | `1.2` | Screenshot dengan kontras rendah. |

Contoh menyesuaikan keduanya:

```csharp
var skew = new SkewCorrectionFilter { MaxAngle = 25 };
var denoise = new DenoiseFilter { Strength = 0.8 };
ocrEngine.Settings.PreprocessingFilters.Clear(); // start fresh
ocrEngine.Settings.PreprocessingFilters.Add(skew);
ocrEngine.Settings.PreprocessingFilters.Add(denoise);
```

**Kasus khusus:** Jika gambar Anda berisi catatan tulisan tangan dan teks cetak, Anda mungkin ingin menambahkan `BinarizationFilter` sebelum denoise untuk memisahkan latar depan dari latar belakang.

---

## display OCR text – Memformat Output

Output konsol biasa cukup untuk demo, tetapi kode produksi sering memerlukan string yang dibersihkan, baris baru, atau bahkan JSON.

```csharp
// Remove extra whitespace and line breaks
string cleaned = System.Text.RegularExpressions.Regex
    .Replace(ocrResult.Text, @"\s+", " ")
    .Trim();

Console.WriteLine("📝 Recognized Text:");
Console.WriteLine(cleaned);
```

Jika Anda memerlukan JSON untuk respons API:

```csharp
var payload = new {
    source = imagePath,
    text = cleaned,
    confidence = ocrResult.Confidence // overall confidence score
};
string json = System.Text.Json.JsonSerializer.Serialize(payload, new JsonSerializerOptions { WriteIndented = true });
Console.WriteLine(json);
```

Sekarang Anda telah **display OCR text** dalam format yang dapat dikonsumsi layanan hilir.

---

## Contoh Lengkap yang Berfungsi – Menggabungkan Semua

Berikut adalah program akhir yang berdiri sendiri, dapat Anda salin‑tempel ke proyek konsol baru. Program ini mencakup filter opsional, pemuatan gambar resolusi tinggi, dan output bersih.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;
using System.Text.Json;
using System.Text.RegularExpressions;

class PreprocessDemo
{
    static void Main()
    {
        // ---------- 1️⃣ Initialize OCR engine ----------
        OcrEngine ocrEngine = new OcrEngine();

        // ---------- 2️⃣ Configure preprocessing ----------
        // Skew correction (up to 25°) + strong denoise
        var skew = new SkewCorrectionFilter { MaxAngle = 25 };
        var denoise = new DenoiseFilter { Strength = 0.8 };
        ocrEngine.Settings.PreprocessingFilters.Add(skew);
        ocrEngine.Settings.PreprocessingFilters.Add(denoise);

        // Optional: increase contrast for low‑visibility scans
        // ocrEngine.Settings.PreprocessingFilters.Add(new ContrastFilter { Level = 1.3 });

        // ---------- 3️⃣ Load the image ----------
        string imagePath = @"YOUR_DIRECTORY/skewed_noisy.jpg";
        OcrImage inputImage = OcrImage.FromFile(imagePath);

        // ---------- 4️⃣ Run OCR ----------
        OcrResult result = ocrEngine.Recognize(inputImage);

        // ---------- 5️⃣ Clean & display ----------
        string cleaned = Regex.Replace(result.Text, @"\s+", " ").Trim();
        Console.WriteLine("✅ Corrected text:");
        Console.WriteLine(cleaned);

        // ---------- 6️⃣ JSON payload (if needed) ----------
        var payload = new {
            source = imagePath,
            text = cleaned,
            confidence = result.Confidence
        };
        string json = JsonSerializer.Serialize(payload, new JsonSerializerOptions { WriteIndented = true });
        Console.WriteLine("\n📦 JSON output:");
        Console.WriteLine(json);
    }
}
```

**Output konsol yang diharapkan (contoh):**

```
✅ Corrected text:
Invoice #12345 Date: 01/15/2026 Total: $1,250.00

📦 JSON output:
{
  "source": "YOUR_DIRECTORY/skewed_noisy.jpg",
  "text": "Invoice #12345 Date: 01/15/2026 Total: $1,250.00",
  "confidence": 0.97
}
```

Jika Anda menjalankan program dengan file yang berbeda, teks dan tingkat kepercayaan akan berubah sesuai.

---

## Pertanyaan Umum & Jawaban

**T: Bagaimana jika gambar saya sudah lurus?**  
J: Filter kemiringan akan mendeteksi sudut mendekati nol dan pada dasarnya tidak melakukan apa‑apa, sehingga Anda dapat membiarkannya tetap aktif.

**T: Apakah Aspose.OCR mendukung bahasa selain Inggris?**  
J: Ya—cukup atur `ocrEngine.Settings.Language = OcrLanguage.Spanish;` (atau bahasa lain yang didukung) sebelum memanggil `Recognize`.

**T: Bagaimana cara menangani PDF multi‑halaman?**  
J: Konversi setiap halaman menjadi gambar (Aspose.PDF dapat melakukannya) dan berikan satu per satu ke instance `OcrEngine` yang sama.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}