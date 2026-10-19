---
category: general
date: 2026-04-26
description: Extraheer snel tekst uit PNG‑bestanden met C#. Leer hoe je afbeeldingen
  naar tekst converteert, PNG‑bestanden leest, door afbeeldingen loopt en batch‑OCR
  op afbeeldingen uitvoert in enkele minuten.
draft: false
keywords:
- extract text from png
- convert images to text
- read png files
- loop through images
- batch ocr images
language: nl
og_description: Haal snel tekst uit PNG‑bestanden met C#. Deze gids laat zien hoe
  je afbeeldingen naar tekst converteert, PNG‑bestanden leest, door afbeeldingen loopt
  en batch‑OCR op afbeeldingen toepast.
og_title: Tekst uit PNG extraheren – Complete C# batch OCR‑tutorial
tags:
- C#
- OCR
- Aspose
title: Tekst extraheren uit PNG – Complete C# batch OCR‑tutorial
url: /nl/net/text-recognition/extract-text-from-png-complete-c-batch-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tekst extraheren uit PNG – Complete C# Batch OCR Tutorial

Ever needed to **extract text from PNG** files but weren’t sure where to start? You’re not alone—many devs hit that wall when they first try OCR on a folder of screenshots. The good news is that with a few lines of C# and Aspose OCR you can convert images to text, read PNG files, loop through images, and batch‑process everything in one go.  

In this tutorial we’ll walk through a ready‑to‑run console app that does exactly that. By the end you’ll have a self‑contained solution that pulls text out of every PNG in a directory and drops a matching `.txt` file beside each image. No extra scripts, no manual copy‑pasting—just pure code.

## What You’ll Need

- **.NET 6 SDK** (of any newer .NET version). It’s free, it’s fast, and it works everywhere.
- **Aspose.OCR for .NET** (the NuGet package). The library includes GPU acceleration if you have a compatible GPU, but it also falls back to CPU automatically.
- A folder with a handful of **PNG images** you want to process.  
- A text editor or IDE—Visual Studio, VS Code, Rider—whatever you prefer.

That’s it. If you already have those, you’re ready to roll.

![extract text from png example](image.png "extract text from png demo screenshot")

*Image alt text: “extract text from png using C# batch OCR”*

## Step 1 – Set Up the Project and Install Aspose.OCR

First, create a new console project and pull in the Aspose OCR package.

```bash
dotnet new console -n PngOcrBatch
cd PngOcrBatch
dotnet add package Aspose.OCR
```

Why do we use a console app? It’s the simplest host for batch jobs, and you can run it from the command line or schedule it with a task runner. If you later need a UI, you can just move the core logic into a class library.

## Step 2 – Initialize a GPU‑Accelerated OCR Engine (or CPU fallback)

Aspose offers a `GpuOcrEngine` that automatically detects a supported GPU. If none is found, it reverts to the regular CPU engine—no extra code needed.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // Create the OCR engine – GPU if available, otherwise CPU
        OcrEngine ocrEngine = new GpuOcrEngine();
        ocrEngine.Language = Language.Latin;   // Latin covers most Western alphabets

        // The rest of the code lives in a separate method for clarity
        ProcessFolder(ocrEngine, @"C:\MyPngFolder");
    }

    // …
}
```

**Pro tip:** If you’re on a headless server without a GPU, you can replace `GpuOcrEngine` with `OcrEngine` and the code will behave exactly the same.

## Step 3 – Loop Through Images in the Target Directory

We need to **loop through images** and only pick PNG files. The `Directory.GetFiles` method does the heavy lifting, and we’ll guard against an empty folder.

```csharp
static void ProcessFolder(OcrEngine engine, string folderPath)
{
    if (!Directory.Exists(folderPath))
    {
        Console.WriteLine($"❌ Folder not found: {folderPath}");
        return;
    }

    // Grab every *.png file – this is the “read png files” part
    string[] pngFiles = Directory.GetFiles(folderPath, "*.png", SearchOption.TopDirectoryOnly);

    if (pngFiles.Length == 0)
    {
        Console.WriteLine("⚠️ No PNG files found. Make sure the folder contains .png images.");
        return;
    }

    foreach (var pngPath in pngFiles)
    {
        Console.WriteLine($"🔎 Processing: {Path.GetFileName(pngPath)}");
        ExtractAndSave(engine, pngPath);
    }
}
```

Notice the use of `SearchOption.TopDirectoryOnly`. If you later need to recurse into sub‑folders, just switch to `AllDirectories`. That small change lets you **convert images to text** in a whole tree with a single line.

## Step 4 – Perform OCR and Save the Result

Now comes the core of the **batch OCR images** workflow. We load each PNG, run `Recognize()`, and write the extracted string to a `.txt` file that shares the same base name.

```csharp
static void ExtractAndSave(OcrEngine engine, string imagePath)
{
    try
    {
        // Load the PNG into the engine
        engine.Image = ImageStream.FromFile(imagePath);

        // Run recognition – this returns a RecognitionResult object
        RecognitionResult result = engine.Recognize();

        // Build the output path (same name, .txt extension)
        string txtPath = Path.ChangeExtension(imagePath, ".txt");

        // Write the OCR text to disk
        File.WriteAllText(txtPath, result.Text);

        Console.WriteLine($"✅ Saved: {Path.GetFileName(txtPath)}");
    }
    catch (Exception ex)
    {
        // Edge case: corrupted PNG or unsupported format
        Console.WriteLine($"❗ Error processing {Path.GetFileName(imagePath)}: {ex.Message}");
    }
}
```

**Why wrap it in a try/catch?** Real‑world image batches often contain a broken file or a PNG that uses an uncommon color profile. Catching the exception prevents the whole run from crashing and lets you keep processing the remaining files.

## Step 5 – Run the Application and Verify Output

Build and launch the app:

```bash
dotnet run
```

You should see a console log similar to:

```
🔎 Processing: invoice1.png
✅ Saved: invoice1.txt
🔎 Processing: screenshot_2024.png
✅ Saved: screenshot_2024.txt
...
```

Open any of the generated `.txt` files—there’s your extracted text. If a file is empty, double‑check the image quality; OCR works best with clear, high‑contrast text.

### Quick Verification Script (optional)

If you want to make sure every PNG got a matching text file, run this tiny PowerShell one‑liner:

```powershell
Get-ChildItem -Path "C:\MyPngFolder" -Filter *.png |
  ForEach-Object { 
    $txt = $_.BaseName + ".txt"
    if (-Not (Test-Path $txt)) { Write-Host "Missing: $txt" }
  }
```

## Common Variations & Edge Cases

| Situation | What to Change |
|-----------|----------------|
| **Non‑Latin languages** (e.g., Cyrillic) | Set `ocrEngine.Language = Language.Cyrillic;` |
| **Large image set (>10 000 files)** | Use `Parallel.ForEach` to speed up processing, but watch GPU memory usage. |
| **Need to keep original image order** | Sort `pngFiles` before the `foreach` (`Array.Sort(pngFiles);`). |
| **Running on a CI server without a GPU** | Replace `GpuOcrEngine` with `OcrEngine` to avoid GPU initialization errors. |
| **You only want to process files that contain a specific keyword** | After `result.Text` is retrieved, check `result.Text.Contains("Invoice")` before writing the file. |

These tweaks let you adapt the **convert images to text** pipeline to almost any scenario you might encounter.

## Full Source Code (Copy‑Paste Ready)

```csharp
// ------------------------------------------------------------
// Extract Text from PNG – Batch OCR using Aspose.OCR (C#)
// ------------------------------------------------------------
using Aspose.OCR;
using Aspose.OCR.Gpu;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // 1️⃣ Create OCR engine (GPU if possible)
        OcrEngine ocrEngine = new GpuOcrEngine();
        ocrEngine.Language = Language.Latin;

        // 2️⃣ Define the folder that holds your PNG files
        string targetFolder = @"C:\MyPngFolder";   // <-- change to your path

        // 3️⃣ Process every PNG in the folder
        ProcessFolder(ocrEngine, targetFolder);
    }

    static void ProcessFolder(OcrEngine engine, string folderPath)
    {
        if (!Directory.Exists(folderPath))
        {
            Console.WriteLine($"❌ Folder not found: {folderPath}");
            return;
        }

        string[] pngFiles = Directory.GetFiles(folderPath, "*.png", SearchOption.TopDirectoryOnly);

        if (pngFiles.Length == 0)
        {
            Console.WriteLine("⚠️ No PNG files found.");
            return;
        }

        foreach (var pngPath in pngFiles)
        {
            Console.WriteLine($"🔎 Processing: {Path.GetFileName(pngPath)}");
            ExtractAndSave(engine, pngPath);
        }
    }

    static void ExtractAndSave(OcrEngine engine, string imagePath)
    {
        try
        {
            engine.Image = ImageStream.FromFile(imagePath);
            RecognitionResult result = engine.Recognize();

            string txtPath = Path.ChangeExtension(imagePath, ".txt");
            File.WriteAllText(txtPath, result.Text);

            Console.WriteLine($"✅ Saved: {Path.GetFileName(txtPath)}");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"❗ Error on {Path.GetFileName(imagePath)}: {ex.Message}");
        }
    }
}
```

Save this as `Program.cs`, run `dotnet run`, and watch the magic happen.

## Conclusion

You now have a **complete, production‑ready way to extract text from PNG** files using C#. The tutorial covered everything—from setting up the project, initializing a GPU‑accelerated OCR engine, **looping through images**, to **batch OCR images** and saving the results as plain text.  

If you’re curious about the next steps, try:

- **Afbeeldingen naar tekst converteren** voor andere formaten (JPG, BMP

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}