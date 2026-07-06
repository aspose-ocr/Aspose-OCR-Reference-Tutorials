---
category: general
date: 2026-03-13
description: Hoe OCR in C# te gebruiken om tekst uit scans te extraheren. Leer hoe
  je TIFF naar tekst converteert met Aspose OCR, GPU-versnelling en stapsgewijze code.
draft: false
keywords:
- how to use OCR
- extract text from scans
- convert tiff to text
- c# ocr tutorial
language: nl
og_description: Hoe OCR in C# te gebruiken om tekst uit scans te extraheren. Deze
  gids laat zien hoe je TIFF naar tekst converteert met Aspose OCR en GPU‑versnelling.
og_title: Hoe OCR in C# te gebruiken – Haal snel tekst uit scans
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Hoe OCR in C# te gebruiken – Haal snel tekst uit scans
url: /nl/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-scans-fast/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe OCR te gebruiken in C# – Tekst snel extraheren uit scans

Heb je je ooit afgevraagd **hoe je OCR kunt gebruiken** om leesbare tekst uit een stapel gescande TIFF‑bestanden te halen? Je bent niet de enige. In veel real‑world projecten—denk aan factuurdigitalisering, archivering van historische documenten, of simpelweg PDF’s doorzoekbaar maken—hebben ontwikkelaars een betrouwbare manier nodig om **tekst uit scans te extraheren** zonder al te veel gedoe.

Het goede nieuws? Met Aspose OCR en een paar regels C# kun je TIFF naar tekst omzetten in een kwestie van seconden, zelfs op een bescheiden workstation. Hieronder vind je een compleet, kant‑klaar voorbeeld, plus de reden achter elke keuze zodat je het kunt aanpassen aan je eigen workflow.

## Wat je nodig hebt

Voordat we beginnen, zorg dat je het volgende bij de hand hebt:

| Voorwaarde | Waarom het belangrijk is |
|------------|--------------------------|
| .NET 6+ (of .NET Framework 4.7+) | Het Aspose OCR NuGet‑pakket richt zich op moderne .NET‑runtime‑omgevingen. |
| Visual Studio 2022 (of elke IDE die je wilt) | Biedt IntelliSense en eenvoudige debugging. |
| Een CUDA‑compatibele GPU & driver (optioneel) | Schakelt `ocrEngine.UseGpu = true` in voor een merkbare snelheidswinst bij grote batches. |
| Een map met TIFF‑afbeeldingen die je wilt verwerken | Deze tutorial gebruikt `*.tif`‑bestanden, maar je kunt het patroon aanpassen. |
| Aspose.OCR NuGet‑pakket (`Install-Package Aspose.OCR`) | De kernbibliotheek die het zware werk doet. |

Als je een van deze mist, pak ze nu—het heeft geen zin om verder te lezen alleen om later een ontbrekende afhankelijkheid tegen te komen.

## Overzicht van de oplossing

Op een hoog niveau doet het programma drie dingen:

1. **Maak een OCR‑engine** en schakel optioneel GPU‑versnelling in.  
2. **Itereer over elk TIFF‑bestand** in een map, voer herkenning uit en vang de resulterende platte tekst op.  
3. **Schrijf de tekst** naar een `.txt`‑bestand naast de originele afbeelding.

Dat is alles. De code is bewust klein, maar laat best practices zien zoals expliciete taalkeuze, juiste resource‑disposal en foutafhandeling voor de meest voorkomende randgevallen.

![Voorbeeld van OCR gebruiken in C#](/images/how-to-use-ocr-csharp.png "Illustratie van hoe OCR in C# te gebruiken om tekst uit scans te extraheren")

## Stap 1: Initialiseer de OCR‑engine (Hoe OCR te gebruiken)

Het eerste wat je nodig hebt is een instantie van `OcrEngine`. Dit object is de poort naar alle Aspose OCR‑functionaliteit. Standaard werkt het op de CPU, maar door `UseGpu = true` in te stellen vertelt je de bibliotheek de zware matrixberekeningen uit te besteden aan je grafische kaart—mits je een CUDA‑compatibele driver geïnstalleerd hebt.

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

**Waarom dit belangrijk is:**  
- **GPU‑versnelling** kan de verwerkingstijd met tot 70 % verkorten voor scans met hoge resolutie.  
- **Expliciete taalkeuze** voorkomt dat de engine raadt en verbetert de nauwkeurigheid, vooral voor niet‑Latijnse scripts.

## Stap 2: Richt de engine op uw scans (TIFF naar tekst converteren)

Vervolgens vertellen we het programma waar het de afbeeldingen moet zoeken. Het gebruik van `Directory.GetFiles` met een `*.tif`‑filter houdt de logica simpel en voorkomt dat ongewenste bestanden zoals `.jpg` of `.png` worden meegenomen.

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

**Opmerking over randgeval:** Als de map leeg is, wordt de onderstaande lus simpelweg nooit uitgevoerd, wat prima is. Later zie je een vriendelijk “No files found”‑bericht.

## Stap 3: Verwerk elk TIFF‑bestand (Tekst extraheren uit scans)

Nu het hart van het programma: elk beeld laden, OCR uitvoeren en de output opslaan. De `ImageStream.FromFile`‑helper streamt het bestand direct naar het geheugen, wat efficiënter is dan eerst een `Bitmap` te laden.

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

**Waarom we elke iteratie in een `try/catch` wikkelen:**  
Het scannen van een batch documenten is rommelig; een beschadigde TIFF of een out‑of‑memory‑hapering mag de hele run niet afbreken. Het catch‑blok logt het probleem en gaat verder, waardoor de pipeline robuust blijft.

### Verwachte uitvoer

Voor elk `example.tif` vind je een sibling `example.txt` met iets als:

```
Invoice #12345
Date: 2024‑01‑15
Total: $1,250.00
Thank you for your business!
```

Als de OCR‑engine een regel niet kan lezen, laat hij simpelweg een lege regel of een onsamenhangend teken staan—er valt niets.

## Stap 4: Opruimen en vrijgeven (Best practice)

`OcrEngine` implementeert `IDisposable`, dus het is beleefd om native resources vrij te geven wanneer je klaar bent. In een korte console‑app kun je op de GC vertrouwen, maar expliciete disposal is een gewoonte die de moeite waard is.

```csharp
// Dispose the engine when everything is finished -------------------------
ocrEngine.Dispose();
Console.WriteLine("🎉 All done! OCR engine released.");
```

## Volledig werkend voorbeeld (Klaar om te kopiëren en plakken)

Hieronder staat het complete programma dat je kunt plakken in een nieuw Console App‑project. Het compileert zoals het is, ervan uitgaande dat je het Aspose.OCR NuGet‑pakket hebt toegevoegd.

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

### Snelle checklist

- **GPU‑vlag** – verwijder of zet op `false` als je geen CUDA‑driver hebt.  
- **Taal** – vervang `Language.English` door een andere ondersteunde taal.  
- **Bestandspatroon** – wijzig `"*.tif"` naar `"*.png"` of `"*.*"` als je scans in een ander formaat zijn.  

## Veelvoorkomende valkuilen & pro‑tips (c# OCR‑tutorial)

| Valkuil | Hoe te vermijden |
|---------|------------------|
| **Out‑of‑memory‑fouten** bij enorme batches | Verwerk bestanden in kleinere delen of roep `GC.Collect()` aan na elke 50 bestanden (zelden nodig). |
| **GPU niet gedetecteerd** maar `UseGpu = true` | De engine schakelt stilzwijgend terug naar CPU, maar je kunt `ocrEngine.IsGpuAvailable` controleren na constructie. |
| **Verkeerd taalpakket** leidt tot onsamenhangende output | Stel `ocrEngine.Language` altijd expliciet in; de standaard kan `Language.Unknown` zijn. |
| **Bestandspad bevat Unicode‑tekens** | Gebruik `Path.GetFullPath` om te normaliseren, of voorzie met `@"\\?\"` op Windows als paden de limiet overschrijden |

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}