---
category: general
date: 2026-03-13
description: Hogyan használjunk OCR-t C#-ban a beolvasott dokumentumok szövegének
  kinyeréséhez. Tanulja meg a TIFF fájlok szöveggé alakítását az Aspose OCR segítségével,
  GPU gyorsítással és lépésről lépésre bemutatott kóddal.
draft: false
keywords:
- how to use OCR
- extract text from scans
- convert tiff to text
- c# ocr tutorial
language: hu
og_description: Hogyan használjuk az OCR-t C#-ban a beolvasott dokumentumok szövegének
  kinyeréséhez. Ez az útmutató megmutatja, hogyan konvertálhatunk TIFF-et szöveggé
  az Aspose OCR és a GPU gyorsítás segítségével.
og_title: Hogyan használjuk az OCR-t C#-ban – Szöveg gyors kinyerése a beolvasott
  képekből
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Hogyan használjunk OCR-t C#-ban – Szöveg gyors kinyerése szkennelésekből
url: /hu/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-scans-fast/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan használjunk OCR-t C#‑ban – Szöveg kinyerése a szkennelésekből gyorsan

Gondolkodtál már azon, **hogyan használjunk OCR-t**, hogy olvasható szöveget nyerjünk ki egy halom beolvasott TIFF fájlból? Nem vagy egyedül. Sok valós projektben—gondolj csak a számlák digitalizálására, történelmi dokumentumok archiválására, vagy egyszerűen a PDF‑ek kereshetővé tételére—fejlesztőknek megbízható módra van szükségük a **szkennelésekből szöveg kinyerésére**, anélkül, hogy izzadnának.

A jó hír? Az Aspose OCR és néhány C# sor segítségével néhány másodperc alatt konvertálhatod a TIFF‑et szöveggé, még egy szerény munkaállomáson is. Az alábbiakban egy teljes, azonnal futtatható példát találsz, valamint a döntések mögötti indoklást, hogy saját munkafolyamatodba illeszthesd.

## Amire szükséged lesz

Mielőtt belevágunk, győződj meg róla, hogy a következőkkel rendelkezel:

| Előfeltétel | Miért fontos |
|--------------|----------------|
| .NET 6+ (vagy .NET Framework 4.7+) | Az Aspose OCR NuGet csomag a modern .NET futtatókörnyezeteket célozza meg. |
| Visual Studio 2022 (vagy bármely kedvenc IDE) | IntelliSense‑t és egyszerű hibakeresést biztosít. |
| CUDA‑kompatibilis GPU és driver (opcionális) | `ocrEngine.UseGpu = true` engedélyezése jelentős sebességnövekedést biztosít nagy kötegek esetén. |
| Egy mappa a feldolgozni kívánt TIFF képekkel | Ez a bemutató `*.tif` fájlokat használ, de a mintát módosíthatod. |
| Aspose.OCR NuGet csomag (`Install-Package Aspose.OCR`) | A fő könyvtár, amely a nehéz munkát végzi. |

Ha valamelyik hiányzik, szerezd be most—nincs értelme tovább olvasni, csak hogy később hiányzó függőségre ütközz.

## A megoldás áttekintése

Áttekintésként a program három dolgot csinál:

1. **Hozz létre egy OCR motor** és opcionálisan kapcsold be a GPU gyorsítást.  
2. **Iterálj minden TIFF fájlon** egy könyvtárban, futtasd a felismerést, és rögzítsd a kapott egyszerű szöveget.  
3. **Írd ki a szöveget** egy `.txt` fájlba, amely az eredeti kép mellett helyezkedik el.

Ennyi. A kód szándékosan apró, mégis bemutatja a legjobb gyakorlatokat, mint például az explicit nyelvválasztás, a megfelelő erőforrás‑felszabadítás és a hibakezelés a leggyakoribb szélső esetekhez.

![How to use OCR in C# example](/images/how-to-use-ocr-csharp.png "Illustration of how to use OCR in C# to extract text from scans")

## 1. lépés: Az OCR motor inicializálása (Hogyan használjunk OCR-t)

Az első dolog, amire szükséged van, egy `OcrEngine` példány. Ez az objektum a kapu minden Aspose OCR funkcióhoz. Alapértelmezés szerint a CPU‑t használja, de a `UseGpu = true` beállítás azt mondja a könyvtárnak, hogy a nehéz mátrix számításokat a grafikus kártyádra terhelje—feltéve, hogy van CUDA‑kompatibilis driver telepítve.

```csharp
using Aspose.OCR;
using System.IO;

// Initialise the engine ----------------------------------------------------
OcrEngine ocrEngine = new OcrEngine
{
    // Enable GPU acceleration if a compatible card is present.
    // If you don’t have a GPU, just leave this as false – the code will still run.
    UseGpu = true,

    // Choose English as the recognition language. Change this if you need
    // another language pack (e.g., Language.French, Language.Spanish, etc.).
    Language = Language.English
};
```

**Miért fontos ez:**  
- **GPU gyorsítás** akár 70 %-kal csökkentheti a feldolgozási időt nagy felbontású szkenneléseknél.  
- **Explicit nyelvválasztás** megakadályozza, hogy a motor találgat, és javítja a pontosságot, különösen a nem latin írásrendszerek esetén.

## 2. lépés: Mutasd meg a motorral a szkenneléseidet (TIFF konvertálása szöveggé)

Ezután megadjuk a programnak, hol keresse a képeket. A `Directory.GetFiles` `*.tif` szűrővel való használata egyszerűvé teszi a logikát, és elkerüli a nem kapcsolódó fájlok, például a `.jpg` vagy `.png` betöltését.

```csharp
// Define the folder that contains the scanned TIFF images -----------------
string inputFolder = @"C:\ScannedDocs"; // <-- replace with your actual path

// Verify the folder exists before we start looping
if (!Directory.Exists(inputFolder))
{
    Console.WriteLine($"❌ Folder not found: {inputFolder}");
    return;
}
```

**Szél eset megjegyzés:** Ha a könyvtár üres, az alábbi ciklus egyszerűen nem fut le, ami teljesen rendben van. Később egy barátságos „No files found” üzenetet fogsz látni.

## 3. lépés: Minden TIFF fájl feldolgozása (Szöveg kinyerése a szkennelésekből)

Most a program szíve: minden kép betöltése, OCR futtatása, és a kimenet mentése. Az `ImageStream.FromFile` segédfüggvény a fájlt közvetlenül memóriába streameli, ami hatékonyabb, mint először egy `Bitmap` betöltése.

```csharp
// Step 3: Iterate over every .tif file in the folder --------------------
string[] tiffFiles = Directory.GetFiles(inputFolder, "*.tif");

if (tiffFiles.Length == 0)
{
    Console.WriteLine("⚠️ No TIFF files found in the specified folder.");
}
else
{
    foreach (var imagePath in tiffFiles)
    {
        try
        {
            // Load the current image into the engine
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // Perform OCR on the image
            ocrEngine.Recognize();

            // Build the output .txt file path (same name, different extension)
            string textPath = Path.ChangeExtension(imagePath, ".txt");

            // Save the extracted text
            File.WriteAllText(textPath, ocrEngine.Text);

            Console.WriteLine($"✅ Processed: {Path.GetFileName(imagePath)} → {Path.GetFileName(textPath)}");
        }
        catch (Exception ex)
        {
            // Log the error but continue with the next file
            Console.WriteLine($"❌ Failed on {Path.GetFileName(imagePath)}: {ex.Message}");
        }
    }
}
```

**Miért csomagoljuk minden iterációt egy `try/catch` blokkba:**  
Dokumentumcsoport szkennelése zavaros lehet; egy sérült TIFF vagy memóriahiány nem szabad, hogy leállítsa az egész futást. A catch blokk naplózza a problémát és továbbhalad, így a folyamat robusztus marad.

### Várható kimenet

Minden `example.tif` fájl mellett megtalálod a hozzá tartozó `example.txt` fájlt, amely valami ilyesmit tartalmaz:

```
Invoice #12345
Date: 2024‑01‑15
Total: $1,250.00
Thank you for your business!
```

Ha az OCR motor nem tud egy sort olvasni, egyszerűen egy üres sort vagy torz karaktert hagy – semmi sem omlik össze.

## 4. lépés: Tisztítás és felszabadítás (Legjobb gyakorlat)

`OcrEngine` implementálja az `IDisposable` interfészt, ezért udvarias, ha a befejezéskor felszabadítod a natív erőforrásokat. Egy rövid konzolos alkalmazásban támaszkodhatsz a GC‑re, de az explicit felszabadítás egy olyan szokás, amelyet érdemes kialakítani.

```csharp
// Dispose the engine when everything is finished -------------------------
ocrEngine.Dispose();
Console.WriteLine("🎉 All done! OCR engine released.");
```

## Teljes működő példa (másolás‑beillesztés kész)

Az alábbiakban a teljes programot találod, amelyet beilleszthetsz egy új Console App projektbe. Úgy fordul, ahogy van, feltéve, hogy hozzáadtad az Aspose.OCR NuGet csomagot.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // --------------------------------------------------------------------
        // Step 1: Initialise the OCR engine (how to use OCR)
        // --------------------------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine
        {
            UseGpu = true,               // Enable GPU if available
            Language = Language.English  // Set language for recognition
        };

        // --------------------------------------------------------------------
        // Step 2: Define the folder containing TIFF scans (convert TIFF to text)
        // --------------------------------------------------------------------
        string inputFolder = @"C:\ScannedDocs"; // <-- adjust this path

        if (!Directory.Exists(inputFolder))
        {
            Console.WriteLine($"❌ Folder not found: {inputFolder}");
            return;
        }

        // --------------------------------------------------------------------
        // Step 3: Process each TIFF file (extract text from scans)
        // --------------------------------------------------------------------
        string[] tiffFiles = Directory.GetFiles(inputFolder, "*.tif");

        if (tiffFiles.Length == 0)
        {
            Console.WriteLine("⚠️ No TIFF files found in the specified folder.");
        }
        else
        {
            foreach (var imagePath in tiffFiles)
            {
                try
                {
                    // Load image
                    ocrEngine.Image = ImageStream.FromFile(imagePath);

                    // Run OCR
                    ocrEngine.Recognize();

                    // Save result next to source image
                    string textPath = Path.ChangeExtension(imagePath, ".txt");
                    File.WriteAllText(textPath, ocrEngine.Text);

                    Console.WriteLine($"✅ Processed: {Path.GetFileName(imagePath)} → {Path.GetFileName(textPath)}");
                }
                catch (Exception ex)
                {
                    Console.WriteLine($"❌ Failed on {Path.GetFileName(imagePath)}: {ex.Message}");
                }
            }
        }

        // --------------------------------------------------------------------
        // Step 4: Clean‑up (c# OCR tutorial best practice)
        // --------------------------------------------------------------------
        ocrEngine.Dispose();
        Console.WriteLine("🎉 All done! OCR engine released.");
    }
}
```

### Gyors ellenőrzőlista

- **GPU jelző** – távolítsd el vagy állítsd `false`‑ra, ha nincs CUDA driver.  
- **Nyelv** – cseréld a `Language.English`‑t bármely más támogatott nyelvre.  
- **Fájl minta** – módosítsd a `"*.tif"`‑t `"*.png"`‑ra vagy `"*.*"`‑ra, ha a szkenneléseid más formátumban vannak.  

## Gyakori buktatók és profi tippek (c# OCR tutorial)

| Buktató | Hogyan kerülhető el |
|---------|---------------------|
| **Memóriahiány hibák** nagy kötegeknél | Fájlok feldolgozása kisebb darabokban, vagy `GC.Collect()` hívása minden 50 fájl után (ritkán szükséges). |
| **GPU nem észlelhető**, de `UseGpu = true` | A motor csendben visszatér a CPU‑hoz, de a konstrukció után ellenőrizheted az `ocrEngine.IsGpuAvailable` értéket. |
| **Helytelen nyelvi csomag** torz kimenetet eredményez | Mindig állítsd be explicit módon az `ocrEngine.Language`‑t; az alapértelmezett lehet `Language.Unknown`. |
| **A fájl útvonal Unicode karaktereket tartalmaz** | Használd a `Path.GetFullPath`‑t a normalizáláshoz, vagy Windows‑on előtagként add hozzá a `@"\\?\"`‑t, ha az útvonalak meghaladják |

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}