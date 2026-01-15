---
category: general
date: 2026-01-15
description: c# ocr‑tutorial die laat zien hoe je tekst uit een afbeelding herkent,
  tekst uit een factuur extraheert en een afbeelding naar tekst converteert met Aspose
  OCR op de GPU.
draft: false
keywords:
- c# ocr tutorial
- recognize text from image
- extract text from invoice
- convert image to text
- load image for ocr
language: nl
og_description: c# OCR-tutorial die je leert tekst uit een afbeelding te herkennen,
  tekst uit een factuur te extraheren en een afbeelding naar tekst te converteren
  met Aspose OCR op de GPU.
og_title: c# OCR-tutorial – Snelle door GPU aangedreven tekstherkenning
tags:
- OCR
- C#
- Aspose
- GPU
title: c# OCR-tutorial – Tekst herkennen van afbeelding met GPU-versnelling
url: /nl/net/ocr-optimization/c-ocr-tutorial-recognize-text-from-image-with-gpu-accelerati/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr tutorial – Tekst herkennen van afbeelding met GPU-versnelling

Heb je ooit een **c# ocr tutorial** nodig gehad die het werk echt doet zonder eindeloze trial‑and‑error? Misschien sta je naar een hoge‑resolutie factuur te staren en vraag je je af hoe je **tekst uit factuur** bestanden in enkele seconden kunt extraheren. Het goede nieuws is dat je het wiel niet opnieuw hoeft uit te vinden—Aspose.OCR biedt je een schone, GPU‑versnelde API die het zware werk voor je doet.

In deze gids lopen we stap voor stap door een volledig, uitvoerbaar voorbeeld dat laat zien hoe je **tekst van afbeelding herkennen** bestanden kunt **afbeelding naar tekst converteren**, en de meest voorkomende valkuilen aanpakt. Aan het einde heb je een zelfstandige applicatie die elke foto van een document kan lezen, van bonnen tot gescande contracten, en schone, doorzoekbare tekst kan produceren.

## Wat je zult leren

- Hoe je het Aspose.OCR NuGet‑pakket installeert en ernaar verwijst.
- Hoe je de OCR‑engine configureert om op de GPU te draaien voor razendsnelle prestaties.
- De juiste manier om **afbeelding laden voor ocr** te gebruiken met `OcrImage.FromFile`.
- Hoe je `Recognize` aanroept met de gewenste taal en het resultaat ophaalt.
- Tips voor het omgaan met multi‑page PDF’s, scans met laag contrast, en foutafhandeling.

Ervaring met Aspose is niet vereist; alleen een werkende .NET‑ontwikkelomgeving (Visual Studio 2022 of VS Code) en een bescheiden GPU (zelfs een geïntegreerde Intel‑GPU volstaat).

## Stap 1 – Installeer Aspose.OCR en bereid je project voor

Allereerst: je hebt de Aspose.OCR‑bibliotheek nodig. De makkelijkste manier is via NuGet.

```bash
dotnet add package Aspose.OCR
```

> **Pro tip:** Als je .NET 6 of later target, zal het pakket automatisch de native GPU‑binaries voor Windows, Linux en macOS binnenhalen. Geen extra DLL’s om te kopiëren.

Zodra het pakket is toegevoegd, open je je projectbestand (`*.csproj`) en controleer je de referentie:

```xml
<ItemGroup>
  <PackageReference Include="Aspose.OCR" Version="23.12.0" />
</ItemGroup>
```

Nu heb je alles wat je nodig hebt om te beginnen met coderen.

## Stap 2 – Maak een GPU‑ingeschakelde OCR‑engine (c# ocr tutorial)

Het hart van de **c# ocr tutorial** is de `OcrEngine`. Door `Engine = Engine.Gpu` in te stellen, vertellen we Aspose de grafische kaart te gebruiken in plaats van de CPU.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

namespace GpuOcrDemo
{
    class Program
    {
        static void Main()
        {
            // Initialize the OCR engine with GPU acceleration.
            var ocrEngine = new OcrEngine
            {
                Engine = Engine.Gpu // GPU acceleration is selected; the library auto‑detects the device.
            };

            // The rest of the steps are broken out into separate methods for clarity.
            string imagePath = @"YOUR_DIRECTORY/high_res_invoice.png";
            PerformOcr(ocrEngine, imagePath);
        }
    }
}
```

> **Waarom GPU?** Een GPU kan duizenden pixels parallel verwerken, waardoor de OCR‑tijd van seconden naar fracties van een seconde wordt verkort bij grote, high‑DPI‑afbeeldingen.

## Stap 3 – Laad afbeelding voor OCR (load image for ocr)

Het correct laden van de afbeelding is belangrijker dan je zou denken. `OcrImage.FromFile` ondersteunt PNG, JPEG, BMP, TIFF en zelfs PDF‑pagina’s. Het leest ook de DPI van de afbeelding, wat de nauwkeurigheid beïnvloedt.

```csharp
static void PerformOcr(OcrEngine engine, string filePath)
{
    // Step 3: Load the image you want to recognize.
    // The FromFile method automatically detects the format.
    var image = OcrImage.FromFile(filePath);

    // Optional: Pre‑process the image for better results.
    // For example, you can increase contrast or convert to grayscale.
    image = ImagePreprocessor.AdjustContrast(image, 1.2);
    image = ImagePreprocessor.ConvertToGrayscale(image);
    
    // Continue to recognition...
    RecognizeAndDisplay(engine, image);
}
```

**Opmerking:** Als je met een PDF werkt, kun je elke pagina extraheren als een `OcrImage` en ze één voor één verwerken.

## Stap 4 – Tekst herkennen van afbeelding (recognize text from image)

Nu gebeurt de magie. We vragen de engine om Engelse tekst te herkennen, maar je kunt elke door Aspose ondersteunde taal doorgeven (Spaans, Duits, Chinees, enz.).

```csharp
static void RecognizeAndDisplay(OcrEngine engine, OcrImage image)
{
    // Step 4: Perform OCR on the image using the desired language.
    var result = engine.Recognize(image, Language.English);

    // Step 5: Output the recognized text.
    Console.WriteLine("=== OCR RESULT ===");
    Console.WriteLine(result.Text);
}
```

De eigenschap `result.Text` bevat de platte tekenreeks. Als je de vertrouwensscore voor elk woord nodig hebt, kun je `result.Regions` inspecteren.

### Verwachte output

```
=== OCR RESULT ===
Invoice #12345
Date: 2025‑12‑01
Total: $1,234.56
Thank you for your business!
```

Als de afbeelding onscherp is, kun je onleesbare tekens zien—hier helpt de preprocessing uit Stap 3.

## Stap 5 – Tekst extraheren uit factuur – Real‑World voorbeeld

Stel je hebt een map vol gescande facturen en je wilt het totaalbedrag eruit halen. Hieronder staat een snelle uitbreiding van de vorige code die een eenvoudige reguliere expressie gebruikt.

```csharp
using System.Text.RegularExpressions;

static void ExtractTotalAmount(string ocrText)
{
    // Look for a pattern like "$1,234.56"
    var match = Regex.Match(ocrText, @"\$\d{1,3}(,\d{3})*(\.\d{2})?");
    if (match.Success)
        Console.WriteLine($"Detected total: {match.Value}");
    else
        Console.WriteLine("Total amount not found.");
}
```

Je zou `ExtractTotalAmount(result.Text);` aanroepen direct na het afdrukken van het OCR‑resultaat. Dit toont hoe eenvoudig het is om **tekst uit factuur** bestanden te **extraheren** zodra je de ruwe tekenreeks hebt.

## Stap 6 – Afbeelding naar tekst converteren in bulk (convert image to text)

Het verwerken van één bestand is prima voor een demo, maar productcode moet vaak tientallen of honderden afbeeldingen afhandelen. Hier is een beknopte lus die een volledige map verwerkt:

```csharp
static void ProcessFolder(OcrEngine engine, string folderPath)
{
    foreach (var file in Directory.EnumerateFiles(folderPath, "*.*", SearchOption.TopDirectoryOnly)
                                 .Where(f => f.EndsWith(".png") || f.EndsWith(".jpg") || f.EndsWith(".tiff")))
    {
        Console.WriteLine($"\nProcessing: {Path.GetFileName(file)}");
        var img = OcrImage.FromFile(file);
        var res = engine.Recognize(img, Language.English);
        Console.WriteLine(res.Text);
        ExtractTotalAmount(res.Text); // optional invoice extraction
    }
}
```

Het uitvoeren van `ProcessFolder(ocrEngine, @"C:\Invoices")` zal **afbeelding naar tekst converteren** voor elk ondersteund bestand in de map, waarbij de GPU voor snelheid wordt benut.

## Randgevallen en veelvoorkomende valkuilen

| Situation | Why It Happens | Quick Fix |
|-----------|----------------|-----------|
| **Low‑contrast scan** | OCR heeft moeite om voorgrond van achtergrond te onderscheiden. | Verhoog het contrast (`ImagePreprocessor.AdjustContrast`) of pas adaptieve drempelwaarde toe. |
| **Multi‑page PDF** | `OcrImage.FromFile` leest alleen de eerste pagina. | Gebruik `PdfDocument` om elke pagina te extraheren als een `OcrImage` en doorloop ze. |
| **Unsupported language** | De standaard ingestelde taal is Engels. | Geef `Language.Spanish` of een andere ondersteunde enum‑waarde door. |
| **GPU not detected** | Ontbrekende native binaries of een verouderde driver. | Controleer of de GPU‑driver up‑to‑date is; herinstalleer het NuGet‑pakket met de `-runtime`‑vlag. |
| **Out‑of‑memory on huge images** | GPU‑geheugen is beperkt. | Verklein de afbeelding (`image = ImagePreprocessor.Resize(image, 2000, 0)`). |

## Volledig werkend voorbeeld

Hieronder staat het volledige programma dat je kunt kopiëren‑plakken in een nieuwe console‑applicatie. Het bevat alle hierboven besproken hulpfuncties.

```csharp
using System;
using System.IO;
using System.Linq;
using System.Text.RegularExpressions;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace GpuOcrDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Initialize GPU‑accelerated OCR engine.
            var ocrEngine = new OcrEngine { Engine = Engine.Gpu };

            // 2️⃣ Define the path to a single image or a folder.
            string imagePath = @"YOUR_DIRECTORY/high_res_invoice.png";
            // string folderPath = @"C:\Invoices";

            // Uncomment one of the following lines:
            PerformOcr(ocrEngine, imagePath);
            // ProcessFolder(ocrEngine, folderPath);
        }

        // -------------------------------------------------
        // Load image, preprocess, recognize, and display.
        // -------------------------------------------------
        static void PerformOcr(OcrEngine engine, string filePath)
        {
            var image = OcrImage.FromFile(filePath);
            image = ImagePreprocessor.AdjustContrast(image, 1.2);
            image = ImagePreprocessor.ConvertToGrayscale(image);

            var result = engine.Recognize(image, Language.English);
            Console.WriteLine("=== OCR RESULT ===");
            Console.WriteLine(result.Text);

            ExtractTotalAmount(result.Text);
        }

        // -------------------------------------------------
        // Bulk processing of a folder.
        // -------------------------------------------------
        static void ProcessFolder(OcrEngine engine, string folderPath)
        {
            foreach (var file in Directory.EnumerateFiles(folderPath, "*.*")
                                          .Where(f => f.EndsWith(".png") || f.EndsWith(".jpg") || f.EndsWith(".tiff")))
            {
                Console.WriteLine($"\nProcessing: {Path.GetFileName(file)}");
                var img = OcrImage.FromFile(file);
                var res = engine.Recognize(img, Language.English);
                Console.WriteLine(res.Text);
                ExtractTotalAmount(res.Text);
            }
        }

        // -------------------------------------------------
        // Simple regex to pull the total amount from an invoice.
        // -------------------------------------------------
        static void ExtractTotalAmount(string ocrText)
        {
            var match = Regex.Match(ocrText, @"\$\d{1,3}(,\d{3})*(\.\d{2})?");
            if (match.Success)
                Console.WriteLine($"Detected total: {match.Value}");
            else
                Console.WriteLine("Total amount not found.");
        }
    }
}
```

**Run it** (`

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}