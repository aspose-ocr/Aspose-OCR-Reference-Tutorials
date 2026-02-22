---
category: general
date: 2026-02-22
description: herken tekst van een afbeelding met Aspose OCR in C#. Leer hoe je een
  tiff‑afbeelding laadt, een OCR‑engine maakt en efficiënt tekst uit een afbeelding
  haalt.
draft: false
keywords:
- recognize text from image
- load tiff image
- extract text from image
- create OCR engine
language: nl
og_description: herken tekst van afbeelding stap‑voor‑stap. leer hoe je een tiff‑afbeelding
  laadt, een OCR‑engine maakt en tekst uit een afbeelding haalt met Aspose OCR in
  C#.
og_title: tekst herkennen van afbeelding – Volledige C# Aspose OCR-tutorial
tags:
- C#
- Aspose OCR
- Image Processing
title: herken tekst van afbeelding met Aspose OCR – Complete C#‑gids
url: /nl/net/text-recognition/recognize-text-from-image-with-aspose-ocr-complete-c-guide/
---

exactly as they appear.

Now produce final output with all content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# tekst herkennen uit afbeelding – Volledige C# Aspose OCR Tutorial

Heb je ooit **tekst moeten herkennen uit een afbeelding** maar liep je vast bij de eerste regel code? Je bent niet de enige. In veel projecten—factuurscanning, archieven digitaliseren, of het bouwen van een doorzoekbare PDF-bibliotheek—het verkrijgen van schone tekst uit een foto is de eerste hindernis.  

Goed nieuws: met Aspose OCR kun je een TIFF‑afbeelding laden, een OCR‑engine opstarten, en **tekst uit een afbeelding extraheren** in slechts een paar regels code. In deze tutorial lopen we het volledige proces door, van het laden van een high‑resolution TIFF‑bestand tot het afdrukken van de herkende tekst en de verwerkingstijd.

We behandelen ook een paar “wat als” scenario's, zoals het uitschakelen van GPU‑versnelling of het verwerken van multi‑page TIFF‑s, zodat je niet verrast wordt als je real‑world data er iets anders uitziet. Aan het einde heb je een kant‑klaar console‑applicatie die **tekst uit een afbeelding herkent** betrouwbaar.

## Prerequisites

- .NET 6.0 SDK of later (de code werkt ook met .NET Core en .NET Framework)
- Aspose.OCR NuGet‑pakket (`dotnet add package Aspose.OCR`)
- Een TIFF‑bestand dat je wilt verwerken (het voorbeeld gebruikt `high_res_page.tif`)
- Elke IDE die je wilt—Visual Studio, Rider, of VS Code volstaat

Er zijn geen extra native libraries nodig; Aspose behandelt alles intern, inclusief optionele GPU‑ondersteuning.

## Stap 1: Een TIFF‑afbeelding laden

Het eerste wat je moet doen is de afbeeldingsgegevens in het geheugen laden. Aspose biedt een statische `Image.Load`‑methode die werkt met de meeste gangbare formaten, inclusief TIFF.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// Load the TIFF file – replace the path with your own image location
var inputImage = Image.Load(@"YOUR_DIRECTORY/high_res_page.tif");
```

**Waarom dit belangrijk is:** TIFF‑bestanden bevatten vaak meerdere pagina's of high‑resolution data waar andere libraries moeite mee hebben. De loader van Aspose leest het bestand correct en behoudt de pixeldiepte, wat cruciaal is voor nauwkeurige OCR later.

*Pro tip:* Als je een multi‑page TIFF verwerkt, kun je door `inputImage.Frames` itereren en elk frame afzonderlijk verwerken. Zo mis je geen tekst die op latere pagina's verborgen zit.

## Stap 2: Een OCR‑engine maken

Nu de afbeelding in het geheugen staat, heb je een engine nodig die karakters kan lezen. De `OcrEngine`‑klasse is waar je taal, GPU‑gebruik en andere opties configureert.

```csharp
// Initialize the OCR engine with desired settings
var ocrEngine = new OcrEngine
{
    // Enable GPU acceleration for faster processing (optional, requires compatible hardware)
    UseGpu = true,
    // Set the language to English – you can change this to Language.French, etc.
    Language = Language.English
};
```

**Waarom dit belangrijk is:** GPU inschakelen (`UseGpu = true`) kan de verwerkingstijd drastisch verkorten op ondersteunde machines, maar het is volkomen veilig om het uit te laten als je draait op een CI‑server of een low‑end laptop. Ook verbetert het kiezen van de juiste taal de tekenherkenning omdat de engine taalspecifieke woordenboeken laadt.

*Let op:* Als je vergeet `Language` in te stellen, valt de engine terug op Engels, wat vreemde resultaten kan geven bij niet‑Latijnse scripts.

## Stap 3: Tekst uit afbeelding herkennen

Met de engine klaar, is de daadwerkelijke OCR‑aanroep een enkele methode: `Recognize`. Deze retourneert een `OcrResult`‑object dat de geëxtraheerde tekst en prestatiestatistieken bevat.

```csharp
// Perform OCR on the loaded image
var ocrResult = ocrEngine.Recognize(inputImage);
```

Het `OcrResult` biedt twee handige eigenschappen:

- `Text` – de platte‑tekstrepresentatie van alles wat de engine kon lezen.
- `ProcessingTime` – hoe lang de OCR duurde, gemeten in milliseconden.

## Stap 4: De resultaten bekijken

Tot slot, laten we de verkregen gegevens weergeven. In een echte applicatie zou je de tekst naar een database kunnen schrijven, maar voor demonstratiedoeleinden is een console‑output voldoende.

```csharp
// Show how long the OCR took and the recognized text
Console.WriteLine($"Recognized in {ocrResult.ProcessingTime} ms");
Console.WriteLine("=== Extracted Text Start ===");
Console.WriteLine(ocrResult.Text);
Console.WriteLine("=== Extracted Text End ===");
```

**Verwachte output** (je tekst zal uiteraard verschillen):

```
Recognized in 842 ms
=== Extracted Text Start ===
Invoice #12345
Date: 2024‑01‑15
Total: $1,250.00
...
=== Extracted Text End ===
```

Als de output er rommelig uitziet, controleer dan of de afbeelding duidelijk is en of je de juiste taal hebt geselecteerd. Je kunt ook `ocrEngine`‑eigenschappen aanpassen, zoals `PreprocessOptions` voor ruisreductie.

## Randgevallen afhandelen

### 1. Geen GPU? Geen probleem.

```csharp
ocrEngine.UseGpu = false; // fallback to CPU‑only processing
```

CPU‑verwerking is langzamer (vaak 2‑3×), maar werkt op elke Windows-, Linux- of macOS‑machine.

### 2. Multi‑page TIFF‑s

```csharp
foreach (var frame in inputImage.Frames)
{
    var pageResult = ocrEngine.Recognize(frame);
    Console.WriteLine(pageResult.Text);
}
```

Elk frame wordt behandeld als een afzonderlijke afbeelding, dus je krijgt een tekstblok per pagina.

### 3. Verschillende talen

```csharp
ocrEngine.Language = Language.Spanish; // or Language.French, Language.German, etc.
```

Het wisselen van talen laadt de juiste tekenset en woordenboek, wat de nauwkeurigheid voor niet‑Engelse documenten drastisch verbetert.

## Volledig werkend voorbeeld

Hieronder staat het volledige programma dat je kunt kopiëren‑en‑plakken in een nieuw console‑project (`dotnet new console`). Het bevat alle besproken onderdelen, plus een paar veiligheidscontroles.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Load the TIFF image you want to process
        // -------------------------------------------------
        const string imagePath = @"YOUR_DIRECTORY/high_res_page.tif";

        if (!System.IO.File.Exists(imagePath))
        {
            Console.WriteLine($"Error: File not found at {imagePath}");
            return;
        }

        var inputImage = Image.Load(imagePath);

        // -------------------------------------------------
        // Step 2: Create and configure the OCR engine
        // -------------------------------------------------
        var ocrEngine = new OcrEngine
        {
            UseGpu = true,                 // optional – set to false if GPU not available
            Language = Language.English    // change if you need another language
        };

        // -------------------------------------------------
        // Step 3: Perform OCR on the loaded image
        // -------------------------------------------------
        var ocrResult = ocrEngine.Recognize(inputImage);

        // -------------------------------------------------
        // Step 4: Display processing time and extracted text
        // -------------------------------------------------
        Console.WriteLine($"Recognized in {ocrResult.ProcessingTime} ms");
        Console.WriteLine("=== Extracted Text Start ===");
        Console.WriteLine(ocrResult.Text);
        Console.WriteLine("=== Extracted Text End ===");

        // Keep console window open when debugging
        Console.WriteLine("\nPress any key to exit...");
        Console.ReadKey();
    }
}
```

Sla het bestand op, voer `dotnet run` uit, en zie de console de herkende tekst weergeven. Dat is alles—je **tekst‑herkennings‑pipeline** is operationeel.

## Veelgestelde vragen

**Q: Werkt dit met PNG of JPEG?**  
A: Absoluut. `Image.Load` detecteert het formaat automatisch, dus je kunt de `.tif`‑extensie vervangen door `.png`, `.jpg`, of zelfs `.bmp`. De OCR‑engine behandelt ze op dezelfde manier.

**Q: Mijn output bevat veel vreemde symbolen.**  
A: Probeer pre‑processing in te schakelen: `ocrEngine.PreprocessOptions = new PreprocessOptions { RemoveNoise = true, Deskew = true };`. Dit maakt de afbeelding schoon vóór herkenning.

**Q: Kan ik de begrenzingskaders voor elk woord krijgen?**  
A: Ja. `ocrResult.Regions` bevat `OcrRegion`‑objecten met coördinaten. Loop erdoorheen als je woorden in een UI wilt markeren.

## Conclusie

We hebben je net laten zien hoe je **tekst uit een afbeelding herkent** met Aspose OCR in C#. Beginnend met het laden van een TIFF‑bestand, vervolgens **een OCR‑engine maken**, de herkenning uitvoeren, en tenslotte de resultaten weergeven—elke stap is beknopt, volledig uitgelegd, en klaar om in je eigen project te kopiëren.

Vanaf hier kun je batch‑verwerking van mappen verkennen, resultaten opslaan in een doorzoekbare index, of OCR combineren met vertaal‑API’s. Wat je ook kiest, het kernpatroon blijft hetzelfde: laad de afbeelding, configureer de engine, herken, en verwerk de output.

Heb je meer vragen over het laden van TIFF‑afbeeldingen, het extraheren van tekst uit een afbeelding, of het afstemmen van de OCR‑engine? Laat een reactie achter hieronder, en happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}