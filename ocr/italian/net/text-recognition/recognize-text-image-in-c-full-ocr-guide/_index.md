---
category: general
date: 2026-06-06
description: Riconosci l'immagine di testo usando C# OCR – un esempio passo‑passo
  di OCR in C# che estrae il testo dalle scansioni e converte la scansione in testo
  in pochi minuti.
draft: false
keywords:
- recognize text image
- c# ocr example
- extract text scan
- convert scan to text
- image to text c#
language: it
og_description: Riconosci il testo nelle immagini con C# OCR. Scopri un esempio pratico
  di OCR in C# che estrae il testo dalle scansioni, converte la scansione in testo
  e gestisce immagini del mondo reale.
og_title: Riconoscere il testo da immagine in C# – Tutorial completo di OCR
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: recognize text image using C# OCR – a step‑by‑step c# ocr example that
    extracts text from scans and convert scan to text in minutes.
  headline: recognize text image in C# – Full OCR Guide
  type: TechArticle
- questions:
  - answer: The `Windows.Media.Ocr` namespace is Windows‑only. On Linux or macOS you’d
      swap it for TesseractSharp or IronOcr—both expose a similar `Engine.Recognize`
      method, so the surrounding code stays virtually unchanged.
    question: Does this work on .NET Core on Linux?
  - answer: Handwriting recognition is still experimental. For best results, stick
      to printed fonts or consider a cloud service like Azure Cognitive Services if
      you need high accuracy.
    question: How accurate is the built‑in OCR for handwritten notes?
  - answer: 'Not out of the box. Convert each PDF page to an image first (using `PdfSharp`
      or `Ghostscript`) and then feed the bitmap to the OCR engine. --- ## Conclusion
      You now have a complete, production‑ready **c# ocr example** that can **recognize
      text image** files, **extract text scan** contents, and **co'
    question: Can I process PDFs directly?
  type: FAQPage
tags:
- OCR
- C#
- Image Processing
title: Riconoscere testo da immagine in C# – Guida completa all'OCR
url: /it/net/text-recognition/recognize-text-image-in-c-full-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# riconoscere immagine di testo in C# – Tutorial OCR completo

Ti sei mai chiesto come **recognize text image** direttamente da una foto scansionata usando C#? Non sei l’unico. Che tu stia digitalizzando vecchie ricevute, estraendo dati da un biglietto da visita, o semplicemente trasformando una scansione a bassa risoluzione in testo modificabile, la capacità di estrarre testo da un’immagine è un trucco utile che ogni sviluppatore dovrebbe avere nella propria cassetta degli attrezzi.

In questa guida percorreremo un **c# ocr example** che carica un’immagine, esegue il riconoscimento ottico dei caratteri e stampa il risultato sulla console. Alla fine sarai in grado di **extract text scan** file, **convert scan to text**, e persino di ottimizzare il processo per immagini rumorose. Nessun servizio di terze parti sofisticato necessario—solo l’API integrata Windows.Media.Ocr (o qualsiasi OcrEngine compatibile) e poche righe di codice.

## What You’ll Learn

* Come configurare un progetto C# per l’OCR.
* Il codice esatto necessario per **recognize text image** file.
* Suggerimenti per gestire scansioni a bassa risoluzione e documenti multipagina.
* Modi per estendere l’esempio in una libreria riutilizzabile per le tue app.

### Prerequisites

* .NET 6.0 o successivo (l’API funziona anche su .NET 5+).
* Visual Studio 2022 (l’edizione Community va bene) o qualsiasi IDE tu preferisca.
* Un’immagine di esempio come `lowres_scan.jpg` collocata in una cartella a cui puoi fare riferimento.
* Familiarità di base con async/await—le chiamate OCR sono asincrone nell’API Windows.

> **Pro tip:** Se sei su una piattaforma non‑Windows, sostituisci lo spazio dei nomi `Windows.Media.Ocr` con una libreria cross‑platform come TesseractSharp; la logica circostante rimane la stessa.

---

## Step 1: Set Up to **recognize text image** with an OCR Engine

First, we need an OCR engine instance. The `OcrEngine` class is the entry point for any **image to text c#** operation.

```csharp
using System;
using System.IO;
using Windows.Graphics.Imaging;
using Windows.Media.Ocr;
using Windows.Storage.Streams;

class Program
{
    static async Task Main(string[] args)
    {
        // Create the OCR engine – default language is English.
        OcrEngine engine = OcrEngine.TryCreateFromLanguage(new OcrLanguage("en"));
        if (engine == null)
        {
            Console.WriteLine("Failed to create OcrEngine. Make sure you are on Windows 10 version 1809 or later.");
            return;
        }

        // Continue with the rest of the pipeline...
```

**Why this matters:** The engine abstracts the heavy‑lifting of pattern recognition. By explicitly creating it we gain control over language settings, which is essential when you later want to **extract text scan** documents in other languages.

## Step 2: Load the Image File – the Core of **convert scan to text**

Next, we read the image from disk and turn it into a `SoftwareBitmap`, the format the OCR engine expects.

```csharp
        // Load the image file into a SoftwareBitmap.
        string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "lowres_scan.jpg");
        using (FileStream fs = new FileStream(imagePath, FileMode.Open, FileAccess.Read))
        {
            // Decode the image (supports JPEG, PNG, BMP, etc.).
            BitmapDecoder decoder = await BitmapDecoder.CreateAsync(fs.AsRandomAccessStream());
            SoftwareBitmap bitmap = await decoder.GetSoftwareBitmapAsync();

            // Optional: upscale low‑resolution images for better accuracy.
            SoftwareBitmap upscaled = SoftwareBitmap.Convert(bitmap, bitmap.BitmapPixelFormat, bitmap.BitmapAlphaMode);
            // Pass the bitmap to OCR.
            await RecognizeAsync(engine, upscaled);
        }
    }
```

**Why we do this:** Directly feeding a raw file stream into OCR often yields poor results, especially with low‑resolution scans. Converting to a `SoftwareBitmap` lets us manipulate DPI, color depth, and even apply filters before recognition.

## Step 3: Perform the **recognize text image** Operation

Now we finally call the engine’s `RecognizeAsync` method. This is where the magic happens.

```csharp
    private static async Task RecognizeAsync(OcrEngine engine, SoftwareBitmap bitmap)
    {
        // Run OCR – this returns an OcrResult object.
        OcrResult result = await engine.RecognizeAsync(bitmap);

        // The Result contains a collection of lines and words.
        Console.WriteLine("=== OCR Output ===");
        foreach (var line in result.Lines)
        {
            Console.WriteLine(line.Text);
        }

        // For a quick **image to text c#** check, also output the raw string.
        Console.WriteLine("\nFull Text:\n" + result.Text);
    }
}
```

**What you’ll see:** If `lowres_scan.jpg` contains the phrase “Hello World”, the console will print:

```
=== OCR Output ===
Hello World

Full Text:
Hello World
```

That’s the entire **c# ocr example** in action—just four logical steps, yet it covers everything from file loading to final output.

## Step 4: Handling Edge Cases – When the Scan Isn’t Perfect

Real‑world images aren’t always crisp. Here are a few adjustments you can make without rewriting the whole program:

| Problema | Soluzione rapida |
|----------|-------------------|
| **Very low DPI (≤ 72)** | Upscale the bitmap using `BitmapTransform` before recognition. |
| **Skewed text** | Apply a rotation transform (`SoftwareBitmap.Rotate`) to straighten the page. |
| **Multiple languages** | Create `OcrEngine.TryCreateFromLanguage(new OcrLanguage("en-fr"))` and set `engine.Language` accordingly. |
| **Large files** | Process the image in tiles (`engine.RecognizeAsync(tileBitmap)`) and concatenate results. |

These tweaks ensure your **extract text scan** routine stays reliable even when dealing with noisy receipts or photos taken at an angle.

## Step 5: Turning the Example into a Reusable Helper (Optional)

If you plan to **convert scan to text** in several parts of an application, wrap the logic in a small utility class:

```csharp
public static class OcrHelper
{
    private static readonly OcrEngine _engine = OcrEngine.TryCreateFromLanguage(new OcrLanguage("en"));

    public static async Task<string> ImageToTextAsync(string filePath)
    {
        using var fs = new FileStream(filePath, FileMode.Open, FileAccess.Read);
        var decoder = await BitmapDecoder.CreateAsync(fs.AsRandomAccessStream());
        var bitmap = await decoder.GetSoftwareBitmapAsync();

        var result = await _engine.RecognizeAsync(bitmap);
        return result.Text;
    }
}
```

Now you simply call:

```csharp
string text = await OcrHelper.ImageToTextAsync("YOUR_DIRECTORY/lowres_scan.jpg");
Console.WriteLine(text);
```

**Why you’ll love this:** The helper isolates the OCR plumbing, letting you focus on business logic—perfect for a **c# ocr example** that will be reused across projects.

---

![recognize text image example](https://example.com/ocr-demo.png "Screenshot of OCR console output showing recognize text image result")

*Alt text:* **recognize text image** output from a C# OCR console application.

---

## Frequently Asked Questions

**Q: Does this work on .NET Core on Linux?**  
A: The `Windows.Media.Ocr` namespace is Windows‑only. On Linux or macOS you’d swap it for TesseractSharp or IronOcr—both expose a similar `Engine.Recognize` method, so the surrounding code stays virtually unchanged.

**Q: How accurate is the built‑in OCR for handwritten notes?**  
A: Handwriting recognition is still experimental. For best results, stick to printed fonts or consider a cloud service like Azure Cognitive Services if you need high accuracy.

**Q: Can I process PDFs directly?**  
A: Not out of the box. Convert each PDF page to an image first (using `PdfSharp` or `Ghostscript`) and then feed the bitmap to the OCR engine.

---

## Conclusion

You now have a complete, production‑ready **c# ocr example** that can **recognize text image** files, **extract text scan** contents, and **convert scan to text** in just a few lines of code. By understanding the flow—engine creation, image loading, asynchronous recognition, and result handling—you can adapt the pattern to any C# project that needs to turn pictures into searchable strings.

Ready for the next step? Try adding a simple UI with WinForms or WPF, experiment with different languages, or hook the output into a database for searchable archives. The sky’s the limit when you master **image to text c#** techniques.

Happy coding, and may your scans always be crisp!

## What Should You Learn Next?

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Estrai testo da immagine C# con selezione della lingua usando Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Converti immagine in testo – Esegui OCR su immagine da URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [Come estrarre testo da immagine preparando rettangoli in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}