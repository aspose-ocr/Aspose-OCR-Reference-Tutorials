---
category: general
date: 2026-03-23
description: Ekstrak teks dari gambar menggunakan Aspose OCR di C# dan pelajari cara
  menambahkan logger konsol untuk umpan balik waktu nyata.
draft: false
keywords:
- extract text from image
- add console logger
language: id
og_description: Ekstrak teks dari gambar dengan Aspose OCR dan tambahkan logger konsol
  untuk memantau proses. Tutorial C# langkah demi langkah.
og_title: Ekstrak Teks dari Gambar di C# – Panduan Pemrograman Lengkap
tags:
- OCR
- C#
- logging
title: Ekstrak Teks dari Gambar di C# – Panduan Lengkap
url: /id/net/text-recognition/extract-text-from-image-in-c-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ekstrak Teks dari Gambar di C# – Panduan Lengkap

Butuh **ekstrak teks dari gambar** dengan cepat dan andal? Dengan Aspose OCR Anda dapat melakukannya dalam beberapa baris C#.  
Kami juga akan menunjukkan cara **menambahkan logger konsol** sehingga Anda dapat melihat mesin OCR mengirimkan progresnya langsung ke terminal Anda.

Bayangkan Anda memiliki struk yang dipindai, catatan tulisan tangan, atau halaman PDF yang disimpan sebagai PNG. Anda menginginkan karakter mentah tanpa membuka UI yang berat. Tutorial ini memandu Anda melalui solusi lengkap, copy‑and‑paste yang berfungsi saat ini dengan .NET 6+ dan perpustakaan Aspose OCR terbaru.

Dengan akhir panduan ini Anda akan dapat:

* Muat file gambar dan jalankan OCR untuk **ekstrak teks dari gambar**.
* Sambungkan logger konsol ke Aspose AI sehingga Anda dapat melihat apa yang dilakukan perpustakaan di balik layar.
* Terapkan post‑processor pemeriksaan ejaan bawaan untuk membersihkan kesalahan OCR.

**Prerequisites** – Lingkungan pengembangan .NET yang berfungsi (Visual Studio 2022, VS Code, atau Rider), .NET 6 SDK atau yang lebih baru, dan lisensi Aspose OCR (atau percobaan gratis). Tidak diperlukan paket pihak ketiga lainnya.

---

## What You’ll Need

| Item | Mengapa penting |
|------|-----------------|
| **Aspose.OCR** NuGet package | Menyediakan kelas `OcrEngine` yang sebenarnya membaca gambar. |
| **Aspose.OCR.AI** NuGet package | Memberikan kerangka kerja post‑processor `AsposeAI`, termasuk pemeriksaan ejaan. |
| **Microsoft.Extensions.Logging** (optional) | Menyediakan antarmuka `ILogger` untuk langkah **add console logger**. |
| **An input image** (`input.png`) | File sumber dari mana kami akan **ekstrak teks dari gambar**. |

Anda dapat menginstal paket-paket tersebut melalui terminal:

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.AI
dotnet add package Microsoft.Extensions.Logging.Abstractions
```

---

## Langkah 1 – Ekstrak Teks dari Gambar dengan Aspose OCR

Hal pertama yang kita lakukan adalah memberikan gambar ke mesin OCR. Blok ini melakukan pekerjaan berat dan mengembalikan string mentah yang mungkin masih mengandung kesalahan ejaan.

```csharp
using Aspose.OCR;
using System;

class OcrDemo
{
    static string PerformOcr(string imagePath)
    {
        // Initialise the OCR engine
        using (OcrEngine ocr = new OcrEngine())
        {
            // Load the image – replace with your own path if needed
            ocr.Image = ImageStream.FromFile(imagePath);

            // Run recognition; if it fails we return an empty string
            if (!ocr.Recognize())
            {
                Console.WriteLine("OCR failed – check the image path and format.");
                return string.Empty;
            }

            // The engine populates the Text property with the recognised characters
            string rawText = ocr.Text;
            Console.WriteLine("Raw OCR output:\n" + rawText);
            return rawText;
        }
    }
}
```

**Mengapa ini berhasil:** `OcrEngine` menyembunyikan semua pra‑pemrosesan gambar tingkat rendah (binarisasi, koreksi kemiringan, dll.). Ketika `Recognize()` mengembalikan `true`, properti `Text` sudah berisi karakter perkiraan terbaik.  

**Tip:** Jika gambar Anda besar, pertimbangkan untuk mengubah ukurannya menjadi ≤ 2000 px pada sisi terpanjang sebelum memberi ke mesin. Ini mempercepat pemrosesan tanpa mengurangi akurasi.

---

## Langkah 2 – Tambahkan Logger Konsol untuk Wawasan Real‑Time

Sekarang kita menambahkan bagian **add console logger**. Logging bukan hanya untuk debugging; ia memberi Anda visibilitas ke unduhan model, langkah‑langkah AI‑processor, dan peringatan apa pun yang mungkin dikeluarkan perpustakaan.

```csharp
using Microsoft.Extensions.Logging;
using System;

public class ConsoleLogger : ILogger
{
    // Minimal ILogger implementation that writes to the console.
    public IDisposable BeginScope<TState>(TState state) => null;
    public bool IsEnabled(LogLevel logLevel) => true;

    public void Log<TState>(LogLevel logLevel, EventId eventId,
        TState state, Exception exception, Func<TState, Exception, string> formatter)
    {
        Console.WriteLine($"[{logLevel}] {formatter(state, exception)}");
    }
}
```

Anda sekarang dapat menyambungkan logger ini ke Aspose AI:

```csharp
using Aspose.OCR.AI;
using Aspose.OCR.AI.PostProcessors;

// ...

ILogger consoleLogger = new ConsoleLogger();   // Implements ILogger
AsposeAI ai = new AsposeAI(consoleLogger);
```

**What you’ll see:** When the spell‑check model is auto‑downloaded, the console will print a line like:

```
[Information] Downloading model to YOUR_DIRECTORY/Models/spellcheck.onnx …
```

Itulah keuntungan **add console logger** – Anda tidak pernah bertanya-tanya apakah operasi latar belakang berhasil.

---

## Langkah 3 – Konfigurasi dan Daftarkan Post‑Processor Pemeriksaan Ejaan

Aspose AI dilengkapi dengan post‑processor pemeriksaan ejaan yang berguna yang membersihkan kesalahan OCR umum (mis., “rec0gn1ze” → “recognize”). Kami akan mengkonfigurasinya, opsional memberi perpustakaan lokasi penyimpanan model, dan kemudian mendaftarkannya.

```csharp
// Create the built‑in spell‑check processor
SpellCheckAIProcessor spellProcessor = new SpellCheckAIProcessor();

// Optional: tell AsposeAI where to keep downloaded models
AsposeAIModelConfig modelConfig = new AsposeAIModelConfig
{
    AllowAutoDownload = true,
    DirectoryModelPath = "YOUR_DIRECTORY/Models"
};

// Register the processor with the AI engine
ai.SetPostProcessor(spellProcessor, modelConfig);
```

**Mengapa Anda mungkin menginginkan jalur khusus:** Dalam pipeline CI/CD Anda sering ingin menyimpan model di direktori yang diketahui untuk menghindari unduhan berulang. Flag `AllowAutoDownload` memastikan model diunduh pertama kali Anda menjalankan kode.

---

## Langkah 4 – Jalankan Post‑Processor pada Hasil OCR

Dengan teks OCR di tangan dan processor pemeriksaan ejaan siap, kami memberikan string mentah ke `AsposeAI`. Mesin menjalankan model, dan processor menyimpan teks yang telah diperbaiki secara internal.

```csharp
// Assume ocrResult contains the raw OCR output from Step 1
string ocrResult = PerformOcr("YOUR_DIRECTORY/input.png");

// Run the post‑processor – it expects an IEnumerable<string>
ai.RunPostprocessor(new[] { ocrResult });
```

Setelah pemanggilan ini, `spellProcessor` menyimpan koleksi objek `RecognitionResult`, masing‑masing dengan properti `RecognitionText` yang berisi versi yang telah dibersihkan.

---

## Langkah 5 – Ambil dan Tampilkan Teks yang Diperbaiki

Akhirnya kami mengambil string yang diperbaiki dari processor dan mencetaknya. Ini adalah momen di mana Anda benar‑benar melihat manfaat OCR dan alur kerja **add console logger**.

```csharp
// Grab the first (and only) result
string correctedText = spellProcessor.GetResult()[0].RecognitionText;
Console.WriteLine("\nCorrected OCR output:\n" + correctedText);
```

**Output yang diharapkan** (asumsi gambar berisi frasa “Aspose OCR demo” dengan beberapa gangguan OCR):

```
Raw OCR output:
Asp0se OCR d3mo

[Information] Model downloaded successfully.
[Information] Spell‑check completed.

Corrected OCR output:
Aspose OCR demo
```

Perhatikan bagaimana logger memberi tahu kami model sudah siap, dan baris yang diperbaiki terbaca bersih.

---

## Langkah 6 – Bersihkan Sumber Daya

Baik `AsposeAI` maupun `OcrEngine` mengimplementasikan `IDisposable`. Membuang (dispose) keduanya melepaskan memori native dan handle file, yang sangat penting dalam layanan yang berjalan lama.

```csharp
// At the end of Main()
ai.Dispose();   // Releases AI resources
// OcrEngine is already disposed via the using‑statement in PerformOcr()
```

---

## Contoh Lengkap yang Berfungsi

Berikut adalah seluruh program yang dapat Anda salin‑tempel ke proyek konsol baru (`dotnet new console`). Ganti `"YOUR_DIRECTORY"` dengan folder sebenarnya di mesin Anda.

```csharp
using Aspose.OCR;
using Aspose.OCR.AI;
using Aspose.OCR.AI.PostProcessors;
using Microsoft.Extensions.Logging; // optional logger
using System;

class SpellCheckDemo
{
    static void Main()
    {
        // ---------- Step 1: OCR ----------
        string ocrResult = PerformOcr("YOUR_DIRECTORY/input.png");
        if (string.IsNullOrEmpty(ocrResult)) return;

        // ---------- Step 2: Initialise AI with console logger ----------
        ILogger consoleLogger = new ConsoleLogger(); // implements ILogger
        AsposeAI ai = new AsposeAI(consoleLogger);

        // ---------- Step 3: Spell‑check processor ----------
        SpellCheckAIProcessor spellProcessor = new SpellCheckAIProcessor();

        // ---------- Step 4: Model configuration (optional) ----------
        AsposeAIModelConfig modelConfig = new AsposeAIModelConfig
        {
            AllowAutoDownload = true,
            DirectoryModelPath = "YOUR_DIRECTORY/Models"
        };

        // ---------- Step 5: Register and run ----------
        ai.SetPostProcessor(spellProcessor, modelConfig);
        ai.RunPostprocessor(new[] { ocrResult });

        // ---------- Step 6: Show corrected text ----------
        string correctedText = spellProcessor.GetResult()[0].RecognitionText;
        Console.WriteLine("\nCorrected OCR output:\n" + correctedText);

        // ---------- Clean up ----------
        ai.Dispose();
    }

    static string PerformOcr(string imagePath)
    {
        using (OcrEngine ocr = new OcrEngine())
        {
            ocr.Image = ImageStream.FromFile(imagePath);
            if (!ocr.Recognize())
            {
                Console.WriteLine("OCR failed – check the image path and format.");
                return string.Empty;
            }
            string raw = ocr.Text;
            Console.WriteLine("Raw OCR output:\n" + raw);
            return raw;
        }
    }
}

// Minimal console logger implementation
public class ConsoleLogger : ILogger
{
    public IDisposable BeginScope<TState>(TState state) => null;
    public bool

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}