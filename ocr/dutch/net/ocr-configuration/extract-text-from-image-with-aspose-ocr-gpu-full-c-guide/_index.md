---
category: general
date: 2026-04-06
description: Tekst extraheren uit afbeelding met Aspose OCR GPU in C#. Leer hoe je
  een afbeelding uit een bestand laadt en de GPU‑geheugenlimiet instelt in deze stapsgewijze
  handleiding.
draft: false
keywords:
- extract text from image
- load image from file
- set gpu memory limit
- aspose ocr example
- aspose ocr gpu
language: nl
og_description: Tekst extraheren uit afbeelding met Aspose OCR GPU in C#. Leer hoe
  je een afbeelding uit een bestand laadt en de GPU‑geheugenlimiet instelt in deze
  stapsgewijze handleiding.
og_title: Tekst extraheren uit afbeelding met Aspose OCR GPU – Volledige C#‑gids
tags:
- Aspose OCR
- C#
- GPU
- OCR
title: Tekst extraheren uit afbeelding met Aspose OCR GPU – Volledige C#‑gids
url: /nl/net/ocr-configuration/extract-text-from-image-with-aspose-ocr-gpu-full-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tekst uit afbeelding extraheren met Aspose OCR GPU – Volledige C#‑gids

Heb je ooit **tekst uit een afbeelding** moeten extraheren, maar liep je vast op het moment dat prestaties belangrijk werden? Je bent niet de enige—veel ontwikkelaars stuiten op dezelfde muur wanneer OCR een knelpunt wordt. In deze tutorial laten we je precies zien hoe je tekst uit een afbeelding haalt met de GPU‑runtime van Aspose OCR, een afbeelding uit een bestand laadt, en zelfs een GPU‑geheugenlimiet instelt voor strakkere resource‑controle.

We lopen stap voor stap door een compleet, kant‑klaar C#‑voorbeeld, leggen uit waarom elke regel belangrijk is, en wijzen op veelvoorkomende valkuilen. Aan het einde heb je een solide basis om snelle, schaalbare OCR‑pijplijnen te bouwen die op de GPU draaien.

## Wat deze gids behandelt

- **Prerequisites**: .NET 6+ (of .NET Framework 4.6+), Aspose.OCR NuGet‑package, een compatibele GPU‑driver.
- **Stap‑voor‑stap code** die een afbeelding uit een bestand laadt, de Aspose OCR GPU‑engine configureert, en tekst extraheert.
- **Waarom** je een GPU‑geheugenlimiet zou willen instellen en hoe je dat veilig doet.
- **Edge‑case handling**: lage‑resolutie‑afbeeldingen, ontbrekende GPU, en het troubleshooten van confidence‑scores.
- **Volgende stappen**: batch‑verwerking, integratie met ASP.NET Core, en terugschakelen naar CPU indien nodig.

> **Pro tip:** Als je niet zeker weet of je GPU wordt gebruikt, controleer dan de GPU‑activiteitsmonitor (bijv. NVIDIA‑SMI) terwijl de OCR draait. Je ziet een piek in geheugengebruik die overeenkomt met de ingestelde limiet.

---

![Diagram dat de stroom van het extraheren van tekst uit een afbeelding met de Aspose OCR GPU‑engine toont](extract-text-from-image-aspose-ocr-gpu.png "tekst uit afbeelding extraheren met Aspose OCR GPU")

## Stap 1: De Aspose OCR‑engine initialiseren voor GPU‑verwerking

Het eerste wat je nodig hebt is een `OcrEngine`‑instance die weet dat hij op de GPU moet draaien. Aspose biedt een nette `OcrEngineSettings`‑object waarin je de runtime kunt specificeren.

```csharp
using Aspose.OCR;
using Aspose.OCR.Runtime;
using System;
using System.Drawing;

// Create the OCR engine and tell it to use the GPU runtime
var ocrEngine = new OcrEngine(new OcrEngineSettings
{
    Runtime = OcrRuntime.Gpu   // Switches processing to the GPU
});
```

**Waarom dit belangrijk is:** Standaard valt Aspose OCR terug op CPU, wat prima is voor kleine afbeeldingen maar pijnlijk traag kan zijn voor hoge‑resolutie‑foto's. Door expliciet `Runtime = OcrRuntime.Gpu` in te stellen, wordt het zware werk naar de grafische kaart verplaatst, wat een merkbare snelheidswinst oplevert.

## Stap 2: (Optioneel) Een GPU‑geheugenlimiet instellen

Als je werkt op een gedeelde workstation of een container met beperkte GPU‑resources, kun je de hoeveelheid geheugen die de OCR‑engine gebruikt beperken. Dit voorkomt out‑of‑memory‑crashes en houdt andere processen tevreden.

```csharp
// Limit the GPU memory usage to 1024 MB (1 GB)
ocrEngine.Settings.GpuMemoryLimit = 1024;
```

**Wanneer te gebruiken:**  
- **Multi‑tenant omgevingen** waar meerdere services dezelfde GPU delen.  
- **CI/CD‑pipelines** die een vaste hoeveelheid GPU‑geheugen per job toewijzen.  

Als je deze regel weglaten, gebruikt Aspose zoveel geheugen als nodig is, wat prima is op een dedicated workstation.

## Stap 3: Afbeelding uit bestand laden

Nu moeten we de foto in het geheugen brengen. Aspose OCR werkt met `System.Drawing.Image`, dus gebruiken we `Image.FromFile`. Zorg ervoor dat het pad naar een bestaand bestand wijst; anders wordt er een uitzondering gegooid.

```csharp
// Replace with the actual path to your high‑resolution image
string imagePath = @"YOUR_DIRECTORY/high_res_photo.png";

using (var image = Image.FromFile(imagePath))
{
    // The image is now ready for OCR processing
    // (the next step will happen inside this using block)
}
```

**Waarom laden uit bestand belangrijk is:** Veel ontwikkelaars proberen direct een byte‑array te voeden, wat werkt maar een onnodige conversiestap toevoegt. `Image.FromFile` gebruiken is eenvoudig, en de `using`‑statement zorgt ervoor dat de bestandshandle snel wordt vrijgegeven.

## Stap 4: OCR uitvoeren en het resultaat ophalen

Met de engine geconfigureerd en de afbeelding geladen, kunnen we eindelijk de tekst extraheren. De `Recognize`‑methode retourneert een `OcrResult` met zowel de ruwe tekst als een confidence‑score.

```csharp
using (var image = Image.FromFile(imagePath))
{
    // Perform OCR on the loaded image
    var ocrResult = ocrEngine.Recognize(image);

    // Display the confidence and the extracted text
    Console.WriteLine($"GPU OCR confidence: {ocrResult.Confidence:P2}");
    Console.WriteLine("Extracted text:");
    Console.WriteLine(ocrResult.Text);
}
```

**Het resultaat begrijpen:**  
- `Confidence` is een waarde tussen 0 en 1. Een confidence van 0,95 (of 95 %) betekent meestal dat de OCR spot‑on is.  
- `Text` bevat regeleinden zoals ze in de afbeelding voorkomen, wat handig is voor verdere verwerking.

## Stap 5: Output verifiëren en edge‑cases afhandelen

### Confidence‑niveaus controleren

Als de confidence onder, zeg, 80 % daalt, wil je misschien terugschakelen naar CPU‑verwerking of beeld‑pre‑processing toepassen (bijv. binarisatie).

```csharp
if (ocrResult.Confidence < 0.80)
{
    Console.WriteLine("Low confidence detected – consider preprocessing or CPU fallback.");
    // Example fallback: switch to CPU runtime temporarily
    ocrEngine.Settings.Runtime = OcrRuntime.Cpu;
    var cpuResult = ocrEngine.Recognize(image);
    Console.WriteLine($"CPU OCR confidence: {cpuResult.Confidence:P2}");
    Console.WriteLine(cpuResult.Text);
}
```

### Omgaan met ontbrekende GPU

Niet elke machine heeft een compatibele GPU. Aspose gooit een `OcrException` als de GPU‑runtime niet kan worden geïnitialiseerd.

```csharp
try
{
    var ocrResult = ocrEngine.Recognize(image);
    // Normal processing...
}
catch (OcrException ex) when (ex.Message.Contains("GPU"))
{
    Console.WriteLine("GPU not available – falling back to CPU.");
    ocrEngine.Settings.Runtime = OcrRuntime.Cpu;
    var cpuResult = ocrEngine.Recognize(image);
    Console.WriteLine(cpuResult.Text);
}
```

### Hoge‑resolutie‑afbeeldingen

Zeer grote afbeeldingen (bijv. > 4000 px breed) kunnen veel GPU‑geheugen verbruiken. Als je de eerder ingestelde limiet bereikt, zal Aspose de verwerking afkappen. Schaal in dat geval de afbeelding eerst down:

```csharp
using (var original = Image.FromFile(imagePath))
{
    int maxWidth = 2000;
    var resized = new Bitmap(original, new Size(maxWidth, original.Height * maxWidth / original.Width));
    var ocrResult = ocrEngine.Recognize(resized);
    // Continue as before
}
```

## Volledig werkend voorbeeld

Hieronder vind je het complete programma dat je kunt kopiëren‑plakken in een nieuw console‑project. Het bevat alle stappen, foutafhandeling, en optionele fallback‑logica.

```csharp
// Program.cs
using Aspose.OCR;
using Aspose.OCR.Runtime;
using System;
using System.Drawing;

class Program
{
    static void Main()
    {
        // Step 1: Initialize OCR engine to use GPU
        var ocrEngine = new OcrEngine(new OcrEngineSettings
        {
            Runtime = OcrRuntime.Gpu   // Switches processing to the GPU
        });

        // Step 2: (Optional) Limit GPU memory usage to 1 GB
        ocrEngine.Settings.GpuMemoryLimit = 1024;

        // Path to the image you want to process
        string imagePath = @"YOUR_DIRECTORY/high_res_photo.png";

        // Step 3: Load image from file
        using (var image = Image.FromFile(imagePath))
        {
            try
            {
                // Step 4: Run OCR on the image
                var ocrResult = ocrEngine.Recognize(image);

                // Step 5: Output confidence and extracted text
                Console.WriteLine($"GPU OCR confidence: {ocrResult.Confidence:P2}");
                Console.WriteLine("Extracted text:");
                Console.WriteLine(ocrResult.Text);

                // Edge‑case: low confidence handling
                if (ocrResult.Confidence < 0.80)
                {
                    Console.WriteLine("\nLow confidence detected – trying CPU fallback...");
                    ocrEngine.Settings.Runtime = OcrRuntime.Cpu;
                    var cpuResult = ocrEngine.Recognize(image);
                    Console.WriteLine($"CPU OCR confidence: {cpuResult.Confidence:P2}");
                    Console.WriteLine(cpuResult.Text);
                }
            }
            catch (OcrException ex) when (ex.Message.Contains("GPU"))
            {
                Console.WriteLine("GPU not available – falling back to CPU runtime.");
                ocrEngine.Settings.Runtime = OcrRuntime.Cpu;
                var cpuResult = ocrEngine.Recognize(image);
                Console.WriteLine($"CPU OCR confidence: {cpuResult.Confidence:P2}");
                Console.WriteLine(cpuResult.Text);
            }
        }
    }
}
```

### Verwachte output

```
GPU OCR confidence: 96.45%
Extracted text:
This is the text that was
found in the high‑resolution
image you supplied.

```

Als de confidence onder de drempel valt, zie je de extra CPU‑fallback‑berichten.

---

## Conclusie

Je weet nu **hoe je tekst uit een afbeelding** kunt extraheren met de GPU‑engine van Aspose OCR, **hoe je een afbeelding uit een bestand laadt**, en waarom je **een GPU‑geheugenlimiet** zou willen instellen voor productie‑workloads. Het bovenstaande voorbeeld is een volledig functionele, citeer‑waardige oplossing die je in elk .NET‑project kunt gebruiken.

Wat is de volgende stap? Overweeg:

- **Batch‑verwerking**: loop over een map met afbeeldingen en schrijf resultaten naar een CSV.  
- **ASP.NET Core‑integratie**: exposeer een API‑endpoint dat een geüploade afbeelding accepteert en de OCR‑tekst retourneert.  
- **Performance‑tuning**: experimenteer met verschillende `GpuMemoryLimit`‑waarden en monitor GPU‑gebruik voor het optimale punt.

Voel je vrij de code aan te passen aan jouw scenario—of je nu een document‑digitaliserings‑pipeline bouwt, een realtime vertaal‑app, of een bon‑scanservice. De basis blijft hetzelfde: initialiseert de GPU‑engine, beheer het geheugen verstandig, en controleer altijd de confidence.

Heb je vragen of loop je tegen een probleem aan? Laat een reactie achter, en laten we samen troubleshootten. Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}