---
category: general
date: 2025-12-30
description: Hoe GPU in Aspose OCR in te schakelen voor batch‑OCR‑verwerking en OCR‑tekstekstractie.
  Leer hoe je het GPU‑apparaat instelt en hoe je Aspose efficiënt gebruikt.
draft: false
keywords:
- how to enable gpu
- batch ocr processing
- ocr text extraction
- set gpu device
- how to use aspose
language: nl
og_description: Hoe GPU in Aspose OCR in te schakelen. Volg deze gids voor batch‑OCR‑verwerking,
  OCR‑tekstextractie, het instellen van een GPU‑apparaat en leer hoe je Aspose gebruikt.
og_title: Hoe GPU voor Aspose OCR in te schakelen – Complete tutorial
tags:
- Aspose
- OCR
- GPU
- C#
title: Hoe GPU voor Aspose OCR inschakelen – Stapsgewijze handleiding
url: /nl/net/ocr-configuration/how-to-enable-gpu-for-aspose-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe GPU in te schakelen voor Aspose OCR – Complete tutorial

Heb je je ooit afgevraagd **hoe je GPU kunt inschakelen** bij het gebruik van Aspose OCR? Je bent niet de enige—ontwikkelaars die enorme documentvolumes verwerken, lopen vaak tegen prestatiebeperkingen aan omdat de OCR‑engine op de CPU blijft hangen. Het goede nieuws? Het inschakelen van GPU‑versnelling is vrij eenvoudig en kan enkele seconden per pagina schelen. In deze gids lopen we **hoe je GPU inschakelt**, **batch‑OCR‑verwerking** uitvoert, de herkende tekst extraheert en zelfs het juiste GPU‑apparaat kiest. Aan het einde weet je **hoe je Aspose** kunt gebruiken voor razendsnelle OCR‑tekstekstractie.

## Wat deze tutorial behandelt

We beginnen met het installeren van de Aspose OCR‑bibliotheek, schakelen daarna GPU‑ondersteuning in en voeren ten slotte een batch van TIFF‑afbeeldingen door de engine. Onderweg leggen we uit waarom je **GPU‑apparaat handmatig** zou willen instellen, welke valkuilen je moet vermijden en hoe je verifieert dat de tekstekstractie daadwerkelijk heeft gewerkt. Geen externe documentatie, alleen een complete copy‑and‑paste‑oplossing die je vandaag nog kunt uitvoeren.

> **Prerequisites**  
> - .NET 6.0 of later (de code maakt gebruik van moderne C#‑syntaxis)  
> - Aspose.OCR voor .NET NuGet‑pakket (versie 23.10 of nieuwer)  
> - Een CUDA‑compatibele GPU met het juiste stuurprogramma geïnstalleerd  
> - Een map met een paar voorbeeld‑`.tif`‑bestanden voor de batch‑run  

Als je deze basis hebt, laten we dan beginnen.

## Hoe GPU in te schakelen in Aspose OCR

Het eerste wat je moet doen is de `OcrEngine` vertellen dat hij de GPU moet gebruiken. Dit gebeurt via twee eenvoudige eigenschappen: `UseGpu` en optioneel `GpuDeviceId`. Het instellen van `UseGpu` op `true` schakelt de engine over naar GPU‑modus, terwijl `GpuDeviceId` je laat kiezen welke GPU (als je er meer dan één hebt) het zware werk moet doen.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU‑specific namespace
using System;
using System.Collections.Generic;

// Step 1: Create the OCR engine and enable GPU acceleration
var ocrEngine = new OcrEngine
{
    // Turn on GPU support – this is the core of “how to enable gpu”
    UseGpu = true,

    // (optional) Choose GPU index 0; change if you have multiple devices
    GpuDeviceId = 0
};
```

> **Why this matters** – De CPU‑versie verwerkt elke pixel sequentieel, wat een knelpunt kan zijn voor afbeeldingen met hoge resolutie. De GPU‑versie draait duizenden threads parallel, waardoor de tijd per pagina drastisch wordt verkort.

### Visueel overzicht  

![Diagram showing how the OCR engine offloads work to the GPU when “how to enable gpu” is set](/images/enable-gpu-diagram.png){: .center .responsive alt="hoe GPU in te schakelen"}

*(Als je de afbeelding niet kunt zien, stel je je een stroomdiagram voor waarin de OCR‑engine de afbeeldingsbuffer doorgeeft aan de CUDA‑core.)*

## Batch‑OCR‑verwerking met Aspose

Nu de engine GPU‑klaar is, laten we een lijst met bestanden invoeren. Batch‑verwerking is zo simpel als een `List<string>` doorlopen die je afbeeldingspaden bevat. Omdat we de GPU gebruiken, zal de engine automatisch elke afbeelding naar het apparaat queue‑en, waardoor de pijplijn bezet blijft.

```csharp
// Step 2: Define the image files you want to process
var imageFiles = new List<string>
{
    @"C:\OCRSamples\page1.tif",
    @"C:\OCRSamples\page2.tif",
    @"C:\OCRSamples\page3.tif"
};

// Step 3: Process each image and report the character count
foreach (var imagePath in imageFiles)
{
    // Recognize the image – the GPU does the heavy lifting behind the scenes
    var ocrResult = ocrEngine.Recognize(imagePath);

    // Show how many characters were extracted – a quick sanity check
    Console.WriteLine($"{imagePath}: {ocrResult.Text.Length} characters");
}
```

> **Pro tip** – Voor echt enorme batches kun je overwegen `Parallel.ForEach` te gebruiken in combinatie met `ocrEngine.Clone()` om thread‑safety‑problemen te vermijden. De `Clone`‑methode maakt een oppervlakkige kopie van de engine die nog steeds naar dezelfde GPU‑context wijst.

### Verwachte output

```
C:\OCRSamples\page1.tif: 1245 characters
C:\OCRSamples\page2.tif: 1130 characters
C:\OCRSamples\page3.tif: 1389 characters
```

Als de cijfers er redelijk uitzien, werkt je **batch OCR‑verwerking** en wordt de GPU benut.

## OCR‑tekstekstractie – De resultaten ophalen

De `Recognize`‑methode retourneert een `OcrResult`‑object dat de ruwe tekst, confidence‑scores en zelfs bounding boxes bevat als je die nodig hebt. Laten we de platte tekst eruit halen en naar een bestand schrijven zodat je de extractie kunt verifiëren.

```csharp
foreach (var imagePath in imageFiles)
{
    var ocrResult = ocrEngine.Recognize(imagePath);
    var extractedText = ocrResult.Text;

    // Save the text to a .txt file with the same base name
    var outputPath = System.IO.Path.ChangeExtension(imagePath, ".txt");
    System.IO.File.WriteAllText(outputPath, extractedText);

    Console.WriteLine($"Extracted text saved to {outputPath}");
}
```

> **Why extract to a file?** – Het opslaan van de OCR‑tekst maakt downstream‑verwerking (zoekindexering, data‑mining, enz.) mogelijk zonder de engine opnieuw te draaien. Het geeft je ook een permanent record voor debugging.

## GPU‑apparaat instellen voor optimale prestaties

Als je werkstation meerdere GPU's host—bijvoorbeeld een dedicated RTX voor ML en een geïntegreerde grafische kaart—wil je ervoor zorgen dat je de juiste gebruikt. De eigenschap `GpuDeviceId` accepteert een integer die overeenkomt met de apparaatindex gerapporteerd door `CudaDeviceInfo.GetDevices()`.

```csharp
using Aspose.OCR.Gpu;

// List all available GPU devices
var devices = CudaDeviceInfo.GetDevices();
for (int i = 0; i < devices.Length; i++)
{
    Console.WriteLine($"Device {i}: {devices[i].Name} (Compute Capability {devices[i].ComputeCapability})");
}

// Suppose you want to use the second GPU (index 1)
ocrEngine.GpuDeviceId = 1;
Console.WriteLine($"Switched to GPU device {ocrEngine.GpuDeviceId}");
```

> **Edge case** – Sommige oudere GPU's ondersteunen de vereiste CUDA‑versie niet. In dat scenario valt `UseGpu = true` stilletjes terug op de CPU, dus controleer altijd `ocrEngine.IsGpuEnabled` na initialisatie.

## Hoe Aspose OCR te gebruiken in een real‑world project

Alles bij elkaar, hier is een compacte, kant‑klaar console‑applicatie die **hoe GPU in te schakelen** demonstreert, **batch OCR‑verwerking** uitvoert, tekst extraheert en je laat het GPU‑apparaat kiezen.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;
using System;
using System.Collections.Generic;
using System.IO;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Initialize OCR engine with GPU support
        // -------------------------------------------------
        var ocrEngine = new OcrEngine
        {
            UseGpu = true,
            GpuDeviceId = 0 // change if you have multiple GPUs
        };

        // -------------------------------------------------
        // 2️⃣ (Optional) Show available GPU devices
        // -------------------------------------------------
        var devices = CudaDeviceInfo.GetDevices();
        Console.WriteLine("Available GPU devices:");
        for (int i = 0; i < devices.Length; i++)
        {
            Console.WriteLine($"  [{i}] {devices[i].Name} – Compute {devices[i].ComputeCapability}");
        }

        // -------------------------------------------------
        // 3️⃣ Define the batch of images to process
        // -------------------------------------------------
        var imageFiles = new List<string>
        {
            @"C:\OCRSamples\page1.tif",
            @"C:\OCRSamples\page2.tif",
            @"C:\OCRSamples\page3.tif"
        };

        // -------------------------------------------------
        // 4️⃣ Process each image, extract text, and save it
        // -------------------------------------------------
        foreach (var imagePath in imageFiles)
        {
            var result = ocrEngine.Recognize(imagePath);
            var text = result.Text;

            var txtPath = Path.ChangeExtension(imagePath, ".txt");
            File.WriteAllText(txtPath, text);

            Console.WriteLine($"{Path.GetFileName(imagePath)} → {Path.GetFileName(txtPath)} ({text.Length} chars)");
        }

        Console.WriteLine("All done! GPU‑accelerated OCR batch completed.");
    }
}
```

### Het voorbeeld uitvoeren

1. Installeer het NuGet‑pakket: `dotnet add package Aspose.OCR --version 23.10.0`  
2. Vervang de paden in `imageFiles` door de locatie van je eigen `.tif`‑bestanden.  
3. Build en run: `dotnet run`.  

Je zou een lijst met GPU's moeten zien, gevolgd door een regel per afbeelding met het aantal tekens en het pad van het gegenereerde `.txt`‑bestand.

## Veelgestelde vragen & valkuilen

- **Werkt dit op een machine zonder GPU?**  
  Ja—als `UseGpu` `true` is maar er geen compatibele GPU wordt gevonden, valt Aspose terug op de CPU. Je kunt de modus verifiëren via `ocrEngine.IsGpuEnabled`.

- **Wat als ik een “CUDA driver version is insufficient” fout krijg?**  
  Update je NVIDIA‑stuurprogramma naar de nieuwste versie die overeenkomt met de CUDA‑toolkit die met Aspose wordt meegeleverd. De bibliotheek vereist minimaal CUDA 11.0 voor recente GPU‑functies.

- **Kan ik PDF's direct verwerken?**  
  Aspose OCR werkt op rasterafbeeldingen. Converteer PDF‑pagina's eerst naar afbeeldingen (bijv. met Aspose.PDF) en voer ze vervolgens in de OCR‑engine.

- **Hoe verbeter ik de nauwkeurigheid bij ruisende scans?**  
  Schakel preprocessing‑opties in zoals `ocrEngine.Preprocess = true` of gebruik afbeeldingen met een hogere resolutie (300 dpi of meer). GPU‑versnelling blijft van toepassing.

## Conclusie

We hebben **hoe GPU in te schakelen** voor Aspose OCR behandeld, **batch OCR‑verwerking** doorlopen, **OCR‑tekstekstractie** gedemonstreerd en laten zien hoe je **GPU‑apparaat** instelt voor optimale prestaties. Met de volledige code‑voorbeeld kun je nu snelle, GPU‑aangedreven OCR integreren in elk .NET‑project en met vertrouwen de eeuwige “hoe gebruik ik Aspose” vraag beantwoorden.

Klaar voor de volgende stap? Probeer taalherkenning toe te voegen, de geëxtraheerde tekst in een zoekindex te voeren, of experimenteer met multi‑GPU‑scaling voor enorme documentarchieven. De mogelijkheden zijn eindeloos wanneer je Aspose’s robuuste API combineert met de ruwe kracht van moderne GPU's.

Happy coding, en moge je OCR‑taken net zo snel lopen als je GPU aankan!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}