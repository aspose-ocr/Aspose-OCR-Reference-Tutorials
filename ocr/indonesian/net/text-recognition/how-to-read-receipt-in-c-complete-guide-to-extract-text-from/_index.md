---
category: general
date: 2026-02-20
description: Pelajari cara membaca struk dalam C# dengan mengekstrak teks dari gambar
  dan mengonversinya ke JSON. Kode langkah demi langkah menggunakan Aspose OCR.
draft: false
keywords:
- how to read receipt
- extract text from image
- convert image to json
- load image file c#
- OCR receipt C#
- Aspose OCR tutorial
language: id
og_description: Temukan cara membaca struk di C# dengan memuat file gambar, mengekstrak
  teks menggunakan Aspose OCR, dan mengonversi hasilnya ke JSON. Contoh kode lengkap.
og_title: Cara Membaca Resi di C# – Ekstrak Teks, Konversi ke JSON
tags:
- C#
- OCR
- Image Processing
- JSON
title: Cara Membaca Resi di C# – Panduan Lengkap untuk Mengekstrak Teks dari Gambar
url: /id/net/text-recognition/how-to-read-receipt-in-c-complete-guide-to-extract-text-from/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Membaca Struk dalam C# – Panduan Lengkap

Pernah bertanya-tanya **bagaimana cara membaca struk** secara programatis? Mungkin Anda sedang membangun aplikasi pelacakan pengeluaran dan perlu mengambil item baris dari foto struk belanja. Menurut pengalaman saya, titik sakit terbesar adalah mengubah JPEG yang buram menjadi data terstruktur yang dapat Anda gunakan. Kabar baik? Dengan beberapa baris kode C# dan Aspose OCR Anda dapat **extract text from image**, lalu **convert image to JSON** dengan cara yang hampir terasa ajaib.

Dalam tutorial ini Anda akan mendapatkan solusi siap‑jalankan yang **loads an image file C#**, menjalankan OCR, dan menghasilkan payload JSON yang detail. Tanpa layanan eksternal, tanpa panggilan REST yang rumit—hanya kode .NET murni yang dapat Anda sisipkan ke dalam proyek console atau ASP.NET apa pun. Pada akhir tutorial Anda akan memahami mengapa setiap langkah penting, cara menangani kasus tepi umum (seperti ukuran struk yang tidak standar), dan seperti apa output JSON sebenarnya.

## Apa yang Anda Butuhkan

- **.NET 6.0 atau lebih baru** – kode menggunakan `System.Drawing.Common` yang didukung di Windows, Linux, dan macOS.
- **Aspose.OCR untuk .NET** – Anda dapat mengambil paket NuGet trial gratis (`Aspose.OCR`) atau menggunakan salinan berlisensi jika Anda memilikinya.
- Sebuah **sample receipt image** (`receipt.jpg`) yang ditempatkan di suatu tempat yang dapat dibaca aplikasi Anda.
- IDE apa pun yang Anda suka (Visual Studio, Rider, VS Code).  

Itu saja. Tidak ada konfigurasi tambahan, tidak ada kunci API.

---

## Langkah 1 – Load the Image File C# (Primary Keyword in Action)

Sebelum mesin OCR dapat melakukan keajaibannya, Anda harus memuat gambar ke memori. Ini adalah langkah klasik “load image file C#” yang sering diabaikan banyak pengembang.

```csharp
using System.Drawing;          // Required for Image
using Aspose.OCR;
using Aspose.OCR.Models;

// Path to your receipt image – adjust as needed
string imagePath = @"C:\Receipts\receipt.jpg";

// Load the image into a System.Drawing.Image object
Image receiptImage = Image.FromFile(imagePath);
```

**Mengapa ini penting:**  
`Image.FromFile` membaca file *sekali* dan menjaga handle tetap terbuka, yang sempurna untuk proses OCR cepat. Jika Anda memproses banyak struk dalam sebuah loop, pertimbangkan menggunakan `Image.FromStream` untuk menghindari penguncian file.

> **Pro tip:** Jika Anda mengalami *FileNotFoundException*, periksa kembali path dan pastikan gambar memang ada. Path relatif juga berfungsi (`"./receipt.jpg"`), tetapi path absolut lebih aman untuk pekerjaan produksi.

---

## Langkah 2 – Create and Configure the OCR Engine

Aspose OCR dilengkapi dengan `OcrEngine` siap pakai. Anda tidak perlu melatih model; perpustakaan ini sudah tahu cara membaca teks cetak, yang persis dengan yang digunakan kebanyakan struk.

```csharp
// Instantiate the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Optional: tweak recognition settings if your receipts are low‑contrast
ocrEngine.Config.Language = OcrLanguage.English;
ocrEngine.Config.DetectOrientation = true;   // Handles rotated receipts
```

**Mengapa kami mengatur opsi ini:**  
`DetectOrientation` memberi tahu mesin untuk secara otomatis memutar gambar jika struk dipindai terbalik. Menetapkan bahasa mempersempit set karakter, yang dapat meningkatkan akurasi—terutama ketika Anda hanya membutuhkan data alfanumerik bahasa Inggris.

---

## Langkah 3 – Recognize the Image and Convert to JSON

Sekarang tiba bagian yang menyenangkan: **extract text from image** dan **convert image to JSON** dalam satu panggilan.

```csharp
// Perform OCR and get the result as a JSON string
string jsonResult = ocrEngine.RecognizeToJson(receiptImage);
```

Metode `RecognizeToJson` mengembalikan struktur JSON yang kaya yang mencakup:

- `Text`: teks gabungan biasa.
- `Lines`: array objek baris dengan koordinat.
- `Words`: setiap kata dengan skor kepercayaan.
- `Regions`: kotak pembatas untuk blok teks yang terdeteksi.

Anda dapat mendeserialisasi JSON ini ke objek C# jika memerlukan akses bertipe, tetapi untuk banyak skenario mencetak JSON mentah sudah cukup.

---

## Langkah 4 – Output the JSON (or Store It)

Mari lihat outputnya dan bahas apa yang harus dilakukan dengan itu.

```csharp
// Write the JSON to the console – perfect for quick debugging
Console.WriteLine(jsonResult);

// Bonus: Save the JSON to a file for later processing
File.WriteAllText("receipt_output.json", jsonResult);
```

### Contoh Output

```json
{
  "Text":"Walmart\n123 Main St\nItem A  $2.99\nItem B  $5.49\nTotal   $8.48",
  "Lines":[
    {"Text":"Walmart","BoundingBox":{"X":10,"Y":15,"Width":200,"Height":30}},
    {"Text":"123 Main St","BoundingBox":{"X":10,"Y":50,"Width":180,"Height":25}},
    {"Text":"Item A  $2.99","BoundingBox":{"X":10,"Y":85,"Width":210,"Height":28}},
    {"Text":"Item B  $5.49","BoundingBox":{"X":10,"Y":120,"Width":210,"Height":28}},
    {"Text":"Total   $8.48","BoundingBox":{"X":10,"Y":155,"Width":210,"Height":30}}
  ],
  "Words":[
    {"Text":"Walmart","Confidence":0.99,"BoundingBox":{...}},
    …
  ]
}
```

**Apa yang harus dilakukan selanjutnya?**  
Parse array `Lines` untuk mengambil nilai `Total`, atau kirim JSON ke layanan hilir yang menyimpan entri pengeluaran. Karena hasilnya sudah berupa JSON, Anda dapat langsung menghubungkannya ke database NoSQL apa pun, Azure Function, atau alur Power Automate.

---

## Langkah 5 – Handling Common Edge Cases

Bahkan mesin OCR terbaik mengalami kesulitan pada beberapa hal. Berikut adalah skenario yang mungkin Anda temui saat mempelajari **how to read receipt** images.

| Situation | Fix / Recommendation |
|-----------|----------------------|
| **Struk beresolusi rendah (≤ 150 dpi)** | Upscale gambar terlebih dahulu menggunakan `Bitmap` dan `Graphics` (`InterpolationMode.HighQualityBicubic`). |
| **Struk yang diputar atau miring** | Pertahankan `DetectOrientation = true`. Untuk kemiringan parah, pra‑proses dengan `Image.RotateFlip` atau perpustakaan pihak ketiga seperti OpenCV. |
| **Latar belakang berwarna (mis., struk di atas meja)** | Konversi ke grayscale dan tingkatkan kontras sebelum OCR (`ImageAttributes`). |
| **Beberapa struk dalam satu foto** | Potong setiap wilayah struk secara manual atau gunakan `ocrEngine.Config.RecognizeMultipleRegions = true`. |
| **File besar menyebabkan OutOfMemory** | Gunakan pernyataan `using` untuk segera membuang objek `Image`, atau proses secara bertahap. |

```csharp
// Example: simple grayscale conversion
using (Bitmap bmp = new Bitmap(receiptImage))
{
    for (int y = 0; y < bmp.Height; y++)
        for (int x = 0; x < bmp.Width; x++)
        {
            Color c = bmp.GetPixel(x, y);
            int gray = (int)(c.R * 0.3 + c.G * 0.59 + c.B * 0.11);
            bmp.SetPixel(x, y, Color.FromArgb(gray, gray, gray));
        }
    receiptImage = (Image)bmp.Clone();
}
```

---

## Langkah 6 – Full Working Example (Copy‑Paste Ready)

Berikut adalah program *lengkap* yang dapat Anda kompilasi sekarang. Program ini mencakup semua langkah, direktif `using` yang tepat, dan penanganan error yang elegan.

```csharp
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace ReceiptReaderDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣ Load the image file C#
            // -------------------------------------------------
            string imagePath = @"YOUR_DIRECTORY\receipt.jpg";

            if (!File.Exists(imagePath))
            {
                Console.WriteLine($"❌ Image not found: {imagePath}");
                return;
            }

            Image receiptImage;
            try
            {
                receiptImage = Image.FromFile(imagePath);
            }
            catch (Exception ex)
            {
                Console.WriteLine($"⚠️ Failed to load image: {ex.Message}");
                return;
            }

            // -------------------------------------------------
            // 2️⃣ Create and configure OCR engine
            // -------------------------------------------------
            OcrEngine ocrEngine = new OcrEngine
            {
                Config =
                {
                    Language = OcrLanguage.English,
                    DetectOrientation = true
                }
            };

            // -------------------------------------------------
            // 3️⃣ Recognize and convert to JSON
            // -------------------------------------------------
            string jsonResult;
            try
            {
                jsonResult = ocrEngine.RecognizeToJson(receiptImage);
            }
            catch (Exception ex)
            {
                Console.WriteLine($"🛑 OCR failed: {ex.Message}");
                return;
            }

            // -------------------------------------------------
            // 4️⃣ Output results
            // -------------------------------------------------
            Console.WriteLine("🗂️ OCR JSON Result:");
            Console.WriteLine(jsonResult);

            // Optionally persist the JSON
            string outputPath = Path.Combine(
                Path.GetDirectoryName(imagePath) ?? ".", "receipt_output.json");
            File.WriteAllText(outputPath, jsonResult);
            Console.WriteLine($"✅ JSON saved to {outputPath}");
        }
    }
}
```

**Jalankan:**  
`dotnet run` dari folder proyek. Jika semuanya telah diatur dengan benar, Anda akan melihat JSON tercetak di konsol dan disimpan di samping gambar struk Anda.

---

## Kesimpulan

Kami baru saja membahas **how to read receipt** images dalam C# dari awal hingga akhir. Dengan memuat gambar, mengonfigurasi Aspose OCR, dan memanggil `RecognizeToJson`, Anda dapat **extract text from image** dan **convert image to JSON** dengan hampir tidak ada boilerplate. Pendekatan ini dapat diskalakan—dari demo satu struk hingga pemroses batch yang menangani ratusan struk setiap malam.

Langkah selanjutnya yang mungkin Anda jelajahi:

- **Parse the JSON** untuk mengambil tanggal, total, dan item baris (gunakan `System.Text.Json` atau `Newtonsoft.Json`).
- **Integrate with a database** (SQL, Cosmos DB) untuk menyimpan catatan pengeluaran secara otomatis.
- **Add a UI** (WinForms, WPF, atau Blazor) sehingga pengguna dapat drag‑and‑drop struk.
- **Swap Aspose OCR** dengan mesin lain (Tesseract, Microsoft Azure OCR) jika lisensi menjadi masalah—tetap gunakan pola “load image file C#” yang sama.

Silakan bereksperimen, memecahkan masalah, dan kemudian kembali ke sini untuk menyegarkan kembali. Jika Anda mengalami kendala, komunitas (dan forum Aspose) adalah tempat yang bagus untuk bertanya. Selamat coding, dan nikmati mengubah struk kertas menjadi data bersih yang dapat dicari!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}