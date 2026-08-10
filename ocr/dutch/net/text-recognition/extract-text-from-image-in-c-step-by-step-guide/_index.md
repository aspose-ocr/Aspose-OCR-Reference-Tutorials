---
category: general
date: 2026-05-06
description: Tekst extraheren uit afbeelding met Aspose OCR in C#. Leer hoe je JPG
  naar tekst converteert, de OCR-taal instelt en efficiënt tekst uit JPG leest.
draft: false
keywords:
- extract text from image
- convert jpg to text
- image to text c#
- read text from jpg
- set OCR language
language: nl
og_description: Tekst extraheren uit afbeelding in C# met Aspose OCR. Deze gids laat
  zien hoe je JPG naar tekst converteert, OCR-taal instelt en tekst uit JPG leest.
og_title: Tekst uit afbeelding extraheren in C# – Complete tutorial
tags:
- OCR
- C#
- Aspose
title: Tekst uit afbeelding extraheren in C# – Stapsgewijze handleiding
url: /nl/net/text-recognition/extract-text-from-image-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tekst uit afbeelding extraheren in C# – Complete programmeerhandleiding

Heb je ooit **tekst uit een afbeelding moeten extraheren** maar wist je niet welke bibliotheek je moest kiezen? Je bent niet de enige—ontwikkelaars vragen voortdurend: “Hoe zet ik een JPG om naar tekst zonder gegevens naar de cloud te sturen?” Het goede nieuws is dat Aspose OCR je een volledig offline oplossing biedt die direct in je .NET‑app werkt.

In deze tutorial lopen we alles door wat je moet weten: van het installeren van het Aspose OCR NuGet‑pakket, tot het **instellen van de OCR‑taal** voor Russische tekst, en uiteindelijk **tekst lezen uit JPG**‑bestanden. Aan het einde heb je een herbruikbare snippet die je in elk C#‑project kunt plaatsen en direct tekst uit afbeeldingen kunt extraheren.

> **Wat je mee krijgt**  
> • Een duidelijk, uitvoerbaar voorbeeld dat **tekst uit afbeelding**‑bestanden extrahert.  
> • Kennis over hoe je **JPG naar tekst** kunt converteren met de Aspose OCR‑engine.  
> • Tips voor het configureren van **set OCR language** voor meertalige scenario’s.  
> • Afhandeling van randgevallen voor onleesbare afbeeldingen en ontbrekende taal‑packs.

## Prerequisites

Voordat we beginnen, zorg dat je het volgende hebt:

| Vereiste | Waarom het belangrijk is |
|----------|--------------------------|
| .NET 6.0 of later (een recente .NET runtime) | Aspose OCR richt zich op .NET Standard 2.0+, dus nieuwere runtimes bieden de beste prestaties. |
| Visual Studio 2022 (of VS Code met C#‑extensies) | Een gebruiksvriendelijke IDE helpt je de OCR‑stroom snel te debuggen. |
| Internettoegang **eenmalig** om het Aspose OCR NuGet‑pakket te downloaden | Na de eerste installatie kun je **offline resources** inschakelen om verdere downloads te vermijden. |
| Een voorbeeld‑JPG‑afbeelding (`input.jpg`) die Russische tekst bevat (of een andere taal die je wilt gebruiken) | De tutorial gebruikt een Russisch voorbeeld, maar je kunt elke geïnstalleerde taal‑pack gebruiken. |

Als een van deze onbekend klinkt, geen paniek. Een NuGet‑pakket installeren is zo simpel als één commando typen, en de rest van de stappen werkt hetzelfde voor elk door Aspose ondersteund afbeeldingsformaat.

## Overview of the Solution

Op een hoog niveau ziet het proces er als volgt uit:

1. **Maak** een `OcrEngine` met offline resources zodat de bibliotheek geen taaldata downloadt tijdens runtime.  
2. **Stel** de gewenste taal in (bijv. Russisch) met de `OcrLanguage`‑enum.  
3. **Roep** `RecognizeImage` aan op een lokaal JPG‑bestand.  
4. **Print** de geëxtraheerde string naar de console of leid het door naar je eigen workflow.

![Extract text from image using Aspose OCR in C#](https://example.com/placeholder-image.png){.align-center alt="extract text from image using Aspose OCR in C#"}

*Het diagram is puur illustratief; de code doet het zware werk.*

## Extract Text from Image – Core Concepts

Voordat we code gaan typen, laten we een paar concepten ontleden die ontwikkelaars vaak laten struikelen:

- **OfflineResources** – Wanneer `true`, zoekt Aspose OCR naar taal‑packs die je vooraf hebt gedownload. Dit elimineert de “auto‑download” stap die de opstarttijd in productie‑omgevingen kan vertragen.  
- **OcrLanguage** – De enum bevat tientallen taal‑identifiers (`English`, `Russian`, `Japanese`, …). Het kiezen van de juiste verbetert de nauwkeurigheid aanzienlijk omdat de engine taal‑specifieke heuristieken kan toepassen.  
- **Image quality** – OCR werkt het best op hoge‑contrast, ruis‑vrije afbeeldingen. Als je rommelige resultaten krijgt, overweeg dan pre‑processing (bijv. binarisatie) vóór je de afbeelding aan de engine geeft.

Deze punten helpen je te bepalen wanneer je **set OCR language** handmatig moet instellen versus automatisch laten detecteren, en waarom **convert JPG to text** geen één‑regelige oplossing is.

## Step 1: Install Aspose OCR NuGet Package

Open een terminal in je projectmap en voer uit:

```bash
dotnet add package Aspose.OCR
```

*Pro tip:* Na de eerste installatie, voeg `-v latest` toe om altijd de nieuwste stabiele build te krijgen. De pakketgrootte is ongeveer 15 MB, wat redelijk is voor de meeste desktop‑ of server‑implementaties.

## Step 2: Convert JPG to Text – Initialize the Engine

Nu de bibliotheek op je machine staat, laten we een `OcrEngine` maken die offline werkt.

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // Step 2.1: Create an OCR engine with offline resources.
        // This prevents the SDK from trying to download language data at runtime.
        var ocrEngine = new OcrEngine(new OcrEngineSettings
        {
            OfflineResources = true   // <-- crucial for production stability
        });

        // Step 2.2: Choose the language pack you need.
        // Here we use Russian; replace with OcrLanguage.English for English text.
        ocrEngine.Language = OcrLanguage.Russian;

        // Step 2.3: Perform OCR on a local JPG file.
        // The file path can be absolute or relative to the executable.
        var result = ocrEngine.RecognizeImage("YOUR_DIRECTORY/input.jpg");

        // Step 2.4: Output the extracted text.
        Console.WriteLine("=== OCR RESULT ===");
        Console.WriteLine(result.Text);
    }
}
```

### Waarom dit belangrijk is

- **Offline‑modus** garandeert deterministische opstarttijden—geen onverwachte netwerk‑calls wanneer je naar een afgesloten server deployt.  
- **De taal instellen** (`OcrLanguage.Russian`) vertelt de engine om de Russische tekenset te gebruiken, wat de herkenningsnauwkeurigheid van ~70 % naar >95 % brengt voor schone afbeeldingen.  
- De methode `RecognizeImage` accepteert elk afbeeldingsformaat dat Aspose ondersteunt (`.jpg`, `.png`, `.tiff`, …). Daarom kunnen we **tekst lezen uit JPG** zonder extra conversiestappen.

## Step 3: Set OCR Language – Handling Multiple Languages

Soms moet je documenten verwerken die gemengde talen bevatten (bijv. Russisch en Engels). Aspose OCR laat je een *fallback* taal‑array opgeven:

```csharp
// Example: Russian primary, English secondary
ocrEngine.Language = OcrLanguage.Russian;
ocrEngine.AdditionalLanguages = new[] { OcrLanguage.English };
```

Wanneer de primaire taal een teken niet herkent, controleert de engine automatisch de aanvullende lijst. Deze techniek is bijzonder handig voor facturen die Cyrillische bedrijfsnamen combineren met Engelse productcodes.

> **Opmerking:** De taal‑packs moeten aanwezig zijn in de `Resources`‑map van je project. Als je een `FileNotFoundException` krijgt, download dan de ontbrekende pack van het Aspose‑portaal en plaats deze naast het uitvoerbare bestand.

## Step 4: Read Text from JPG – Common Pitfalls & Fixes

Zelfs met de juiste taal‑pack kun je tegen de volgende problemen aanlopen:

| Probleem | Typisch symptoom | Snelle oplossing |
|----------|------------------|-------------------|
| Lage contrast | Vervormde of lege output | Pas een eenvoudige contrast‑stretch filter toe met `System.Drawing` vóór OCR. |
| Gedraaide afbeelding | Tekst verschijnt zijwaarts | Gebruik `ocrEngine.ImageRotation = OcrRotation.Rotate90;` (of 180/270) vóór het aanroepen van `RecognizeImage`. |
| Groot bestand | Trage herkenning, hoog geheugenverbruik | Verklein de afbeelding tot maximaal 2000 px aan de langste zijde; OCR‑kwaliteit blijft hoog. |

Hier is een compacte helper die een afbeelding verkleint en verbetert voordat hij aan de engine wordt doorgegeven:

```csharp
using System.Drawing;
using System.Drawing.Imaging;

static string PreprocessAndRead(string jpgPath)
{
    // Load the original image
    using var original = new Bitmap(jpgPath);

    // Resize while preserving aspect ratio (max 2000px)
    int maxDim = 2000;
    int newWidth, newHeight;
    if (original.Width > original.Height)
    {
        newWidth = maxDim;
        newHeight = original.Height * maxDim / original.Width;
    }
    else
    {
        newHeight = maxDim;
        newWidth = original.Width * maxDim / original.Height;
    }

    using var resized = new Bitmap(original, new Size(newWidth, newHeight));

    // Optional: increase contrast (simple linear stretch)
    var contrast = new ImageAttributes();
    float[][] matrix = {
        new float[] {1.2f, 0, 0, 0, 0},
        new float[] {0, 1.2f, 0, 0, 0},
        new float[] {0, 0, 1.2f, 0, 0},
        new float[] {0, 0, 0, 1, 0},
        new float[] {0, 0, 0, 0, 1}
    };
    contrast.SetColorMatrix(new ColorMatrix(matrix));

    using var graphics = Graphics.FromImage(resized);
    graphics.DrawImage(resized, new Rectangle(0, 0, newWidth, newHeight), 0, 0, newWidth, newHeight, GraphicsUnit.Pixel, contrast);

    // Save to a temporary file (Aspose OCR works with file paths)
    string tempPath = Path.GetTempFileName() + ".jpg";
    resized.Save(tempPath, ImageFormat.Jpeg);

    // Run OCR
    var engine = new OcrEngine(new OcrEngineSettings { OfflineResources = true });
    engine.Language = OcrLanguage.Russian;
    var res = engine.RecognizeImage(tempPath);
    File.Delete(tempPath); // clean up
    return res.Text;
}
```

Je kunt nu `Console.WriteLine(PreprocessAndRead("YOUR_DIRECTORY/input.jpg"));` aanroepen en een schoner resultaat krijgen.

## Full Working Example – All Steps in One File

Hieronder staat het *complete* programma dat je kunt kopiëren‑plakken in `Program.cs`. Het bevat installatie‑notities, taalconfiguratie, pre‑processing en foutafhandeling.

```csharp
using System;
using System.Drawing;
using System.Drawing.Imaging;
using System.IO;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        string imagePath = "YOUR_DIRECTORY/input.jpg";

        try
        {

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}