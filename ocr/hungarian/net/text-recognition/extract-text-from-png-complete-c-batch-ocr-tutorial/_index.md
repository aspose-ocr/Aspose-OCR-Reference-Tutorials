---
category: general
date: 2026-04-26
description: Gyorsan szöveget nyerjen ki PNG fájlokból C#-val. Tanulja meg, hogyan
  konvertálja a képeket szöveggé, olvassa be a PNG fájlokat, iteráljon a képeken,
  és percek alatt tömegesen OCR-eljék a képeket.
draft: false
keywords:
- extract text from png
- convert images to text
- read png files
- loop through images
- batch ocr images
language: hu
og_description: Gyorsan szöveget nyerj ki PNG-fájlokból C#-al. Ez az útmutató bemutatja,
  hogyan konvertálhatók a képek szöveggé, hogyan olvashatók be a PNG-fájlok, hogyan
  lehet végigmenni a képeken, és hogyan végezhető kötegelt OCR a képeken.
og_title: Szöveg kinyerése PNG-ből – Teljes C# kötegelt OCR útmutató
tags:
- C#
- OCR
- Aspose
title: Szöveg kinyerése PNG-ből – Teljes C# kötegelt OCR útmutató
url: /hu/net/text-recognition/extract-text-from-png-complete-c-batch-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Szöveg kinyerése PNG‑ből – Teljes C# kötegelt OCR útmutató

Valaha is szükséged volt **szöveg kinyerésére PNG** fájlokból, de nem tudtad, hol kezdjed? Nem vagy egyedül – sok fejlesztő ütközik ebbe a falba, amikor először próbál OCR‑t futtatni egy képernyőképekből álló mappán. A jó hír, hogy néhány C# sor és az Aspose OCR segítségével képeket szöveggé konvertálhatsz, PNG fájlokat olvashatsz, képeken végigiterálhatsz, és mindent egy lépésben kötegelt módon feldolgozhatsz.  

Ebben az útmutatóban egy azonnal futtatható konzolos alkalmazáson keresztül mutatjuk be, hogyan működik ez pontosan. A végére egy önálló megoldásod lesz, amely minden PNG‑t egy könyvtárban beolvassa, és a megfelelő `.txt` fájlt a kép mellé helyezi. Nincs extra szkript, nincs kézi másolás‑beillesztés – csak tiszta kód.

## Amire szükséged lesz

- **.NET 6 SDK** (vagy bármely újabb .NET verzió). Ingyenes, gyors, és mindenhol működik.
- **Aspose.OCR for .NET** (a NuGet csomag). A könyvtár GPU gyorsítást is tartalmaz, ha kompatibilis GPU‑d van, de automatikusan visszaesik CPU‑ra is.
- Egy mappa, amely néhány **PNG képet** tartalmaz, amelyet feldolgozni szeretnél.  
- Egy szövegszerkesztő vagy IDE – Visual Studio, VS Code, Rider – bármi, ami kényelmes.

Ennyi. Ha már megvannak ezek, készen állsz a munkára.

![extract text from png example](image.png "extract text from png demo screenshot")

*Image alt text: “extract text from png using C# batch OCR”*

## 1. lépés – Projekt létrehozása és az Aspose.OCR telepítése

Először hozz létre egy új konzolos projektet, és add hozzá az Aspose OCR csomagot.

```bash
dotnet new console -n PngOcrBatch
cd PngOcrBatch
dotnet add package Aspose.OCR
```

Miért konzolos alkalmazást használunk? Ez a legegyszerűbb környezet kötegelt feladatokhoz, és futtatható a parancssorból vagy ütemezhető feladatkezelővel. Ha később UI‑ra van szükséged, a logikát egyszerűen áthelyezheted egy osztálykönyvtárba.

## 2. lépés – GPU‑gyorsított OCR motor inicializálása (vagy CPU visszaesés)

Az Aspose egy `GpuOcrEngine`‑t kínál, amely automatikusan felismeri a támogatott GPU‑t. Ha nincs GPU, visszatér a szokásos CPU motorra – külön kód nélkül.

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

**Pro tipp:** Ha fej nélküli szerveren vagy GPU nélkül, cseréld le a `GpuOcrEngine`‑t `OcrEngine`‑re, és a kód ugyanúgy fog működni.

## 3. lépés – Képek bejárása a célkönyvtárban

**Be kell járnunk a képeket**, és csak a PNG fájlokat kell kiválasztanunk. A `Directory.GetFiles` metódus végzi a nehéz munkát, és ellenőrizzük, hogy a mappa ne legyen üres.

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

Vedd észre a `SearchOption.TopDirectoryOnly` használatát. Ha később rekurzívan szeretnél almappákba is menni, egyszerűen állítsd át `AllDirectories`‑re. Ez a kis változtatás lehetővé teszi, hogy **képeket szöveggé konvertálj** egy teljes fa struktúrában egyetlen sorral.

## 4. lépés – OCR végrehajtása és az eredmény mentése

Most következik a **kötegelt OCR képek** munkafolyamatának a központi része. Betöltjük az egyes PNG‑ket, meghívjuk a `Recognize()`‑t, és a kinyert sztringet egy `.txt` fájlba írjuk, amely ugyanazzal az alappal rendelkezik, mint a kép.

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

**Miért csomagoljuk try/catch‑be?** A valós képkötegek gyakran tartalmaznak hibás fájlokat vagy PNG‑ket, amelyek szokatlan színprofilt használnak. A kivétel elkapása megakadályozza, hogy az egész futás összeomoljon, és lehetővé teszi a maradék fájlok feldolgozását.

## 5. lépés – Alkalmazás futtatása és a kimenet ellenőrzése

Építsd fel és indítsd el az alkalmazást:

```bash
dotnet run
```

A konzolban valami hasonló logot kell látnod:

```
🔎 Processing: invoice1.png
✅ Saved: invoice1.txt
🔎 Processing: screenshot_2024.png
✅ Saved: screenshot_2024.txt
...
```

Nyisd meg bármelyik generált `.txt` fájlt – ott lesz a kinyert szöveg. Ha egy fájl üres, ellenőrizd a kép minőségét; az OCR a tiszta, nagy kontrasztú szöveggel működik a legjobban.

### Gyors ellenőrző szkript (opcionális)

Ha szeretnéd biztosra venni, hogy minden PNG-hez létrejött a megfelelő szövegfájl, futtasd ezt a kis PowerShell egy‑soros parancsot:

```powershell
Get-ChildItem -Path "C:\MyPngFolder" -Filter *.png |
  ForEach-Object { 
    $txt = $_.BaseName + ".txt"
    if (-Not (Test-Path $txt)) { Write-Host "Missing: $txt" }
  }
```

## Gyakori variációk és széljegyek

| Helyzet | Mit kell módosítani |
|-----------|----------------|
| **Nem latin nyelvek** (pl. cirill) | `ocrEngine.Language = Language.Cyrillic;` |
| **Nagy képmennyiség (>10 000 fájl)** | `Parallel.ForEach` használata a gyorsabb feldolgozáshoz, de figyelj a GPU memóriahasználatra. |
| **Az eredeti képsorrend megtartása** | A `foreach` előtt `Array.Sort(pngFiles);`‑t alkalmazz. |
| **CI szerveren futtatás GPU nélkül** | `GpuOcrEngine` helyett `OcrEngine` használata a GPU inicializációs hibák elkerüléséhez. |
| **Csak olyan fájlokat akarsz feldolgozni, amelyek egy adott kulcsszót tartalmaznak** | A `result.Text` lekérése után ellenőrizd `result.Text.Contains("Invoice")`‑t, mielőtt a fájlt írnád. |

Ezekkel a finomhangolásokkal a **képek szöveggé konvertálása** csővezetékét szinte bármilyen szituációhoz adaptálhatod.

## Teljes forráskód (másolás‑beillesztés kész)

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

Mentsd el `Program.cs`‑ként, futtasd a `dotnet run` parancsot, és nézd meg a varázslatot.

## Összegzés

Most már van egy **teljes, éles környezetben is használható megoldásod a szöveg kinyerésére PNG** fájlokból C#‑ben. Az útmutató mindent lefedett – a projekt beállításától a GPU‑gyorsított OCR motor inicializálásáig, a **képek bejárásáig**, a **kötegelt OCR képek** végrehajtásáig, és a plain text eredmények mentéséig.  

Ha kíváncsi vagy a következő lépésekre, próbáld ki:

- **Képek szöveggé konvertálása** más formátumokhoz (JPG, BMP

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}