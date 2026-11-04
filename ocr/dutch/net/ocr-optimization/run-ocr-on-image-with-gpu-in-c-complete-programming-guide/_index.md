---
category: general
date: 2026-03-26
description: Voer OCR uit op een afbeelding met Aspose OCR GPU‑ondersteuning in C#.
  Leer hoe je een afbeelding laadt voor OCR, de GPU‑apparaat‑ID instelt en snel tekst
  uit de afbeelding extraheert.
draft: false
keywords:
- run OCR on image
- extract text from image
- load image for OCR
- recognize text from document
- set GPU device ID
language: nl
og_description: Voer OCR uit op een afbeelding met Aspose OCR GPU in C#. Deze gids
  laat zien hoe je een afbeelding laadt voor OCR, de GPU‑apparaat‑ID instelt en efficiënt
  tekst uit de afbeelding extraheert.
og_title: OCR uitvoeren op afbeelding met GPU in C# – Complete gids
tags:
- C#
- OCR
- GPU
- Aspose
title: OCR uitvoeren op afbeelding met GPU in C# – Complete programmeergids
url: /nl/net/ocr-optimization/run-ocr-on-image-with-gpu-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR uitvoeren op afbeelding met GPU in C# – Complete programmeergids

Heb je ooit **run OCR on image** bestanden moeten verwerken, maar vond je de CPU‑versie ondraaglijk traag? Je bent niet de enige. In veel real‑world apps—denk aan factuurscanners of grootschalige documentarchieven—ligt de bottleneck bij de OCR‑engine zelf.  

In deze tutorial lopen we een **volledig, uitvoerbaar voorbeeld** door die laat zien hoe je **load image for OCR**, optioneel **set GPU device ID**, en uiteindelijk **extract text from image** gebruikt met de GPU‑versnelde API van Aspose OCR. Aan het einde kun je **recognize text from document** afbeeldingen in een fractie van de tijd die een pure‑CPU aanpak zou kosten.

## Wat je zult leren

- Hoe je de Aspose.OCR en Aspose.OCR.Gpu pakketten installeert en referentieert.  
- De exacte stappen om **run OCR on image** met GPU‑versnelling uit te voeren.  
- Waarom het kiezen van de juiste **GPU device ID** belangrijk is op multi‑GPU machines.  
- Tips voor het verwerken van grote bestanden, fallback‑strategieën en veelvoorkomende valkuilen.  

### Vereisten

| Vereiste | Reden |
|----------|-------|
| .NET 6.0 of later | Moderne taalfeatures en betere prestaties |
| Visual Studio 2022 (of elke C# IDE) | Voor eenvoudige projectopzet |
| NVIDIA GPU met CUDA-ondersteuning (optioneel) | Alleen vereist als je GPU-versnelling wilt |
| Aspose.OCR & Aspose.OCR.Gpu NuGet packages | Biedt de `GpuOcrEngine` class |

Als je geen GPU hebt, geen paniek—de code valt elegant terug op de CPU‑engine, die we later behandelen.

---

## Stap 1: Installeer Aspose OCR-pakketten

Voordat je **run OCR on image** kunt uitvoeren, heb je de bibliotheken nodig. Open je terminal (of Package Manager Console) en voer uit:

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Gpu
```

Deze twee pakketten brengen de kern‑OCR‑engine en de GPU‑specifieke extensies binnen. Na de installatie zie je de volgende referenties in je `.csproj`:

```xml
<ItemGroup>
  <PackageReference Include="Aspose.OCR" Version="23.10.0" />
  <PackageReference Include="Aspose.OCR.Gpu" Version="23.10.0" />
</ItemGroup>
```

> **Pro tip:** Houd de pakketversies gesynchroniseerd; niet‑overeenkomende versies kunnen runtime‑fouten veroorzaken.

---

## Stap 2: Maak een GPU‑enabled OCR‑engine

Nu de bibliotheken aanwezig zijn, laten we **run OCR on image** gebruiken met de GPU. De `GpuOcrEngine`‑klasse is het toegangspunt voor versnelde verwerking.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;   // Namespace for GPU support

class GpuExample
{
    static void Main()
    {
        // Step 2.1: Instantiate the GPU OCR engine
        var gpuEngine = new GpuOcrEngine();

        // Step 2.2 (optional): Choose which GPU to use – 0 = first GPU
        // This is where the "set GPU device ID" keyword comes into play.
        gpuEngine.DeviceId = 0;

        // The rest of the workflow continues in the following steps...
```

**Waarom een GPU?**  
GPU‑kernen blinken uit in parallelle pixelbewerkingen, precies wat OCR nodig heeft bij het scannen van hoge‑resolutie scans. Door `DeviceId` in te stellen, vertel je de bibliotheek welke fysieke kaart te gebruiken—handig op werkstations met meerdere GPU's.

---

## Stap 3: Laad afbeelding voor OCR

Voor herkenning moet je **load image for OCR**. Aspose biedt een handige statische factory‑methode die veel formaten ondersteunt (JPEG, PNG, TIFF, enz.).

```csharp
        // Step 3: Load the image you want to recognize
        // Replace the path with your actual file location.
        var ocrImage = OcrImage.FromFile(@"C:\Images\large_document.jpg");

        // Quick sanity check – ensure the image was loaded.
        if (ocrImage == null)
        {
            Console.WriteLine("Failed to load image. Check the file path.");
            return;
        }
```

> **Edge case:** Als de afbeelding groter is dan 10 MB, overweeg dan eerst te down‑samplen om GPU‑geheugentekort te voorkomen. Je kunt dit doen met `ocrImage.Resize(width, height)` vóór herkenning.

---

## Stap 4: Herken tekst uit document

Met de engine klaar en de afbeelding geladen, is het tijd om **recognize text from document**. De `Recognize`‑methode retourneert een `OcrResult`‑object met de platte‑tekstoutput en extra metadata.

```csharp
        // Step 4: Run the OCR process on the image
        OcrResult ocrResult = gpuEngine.Recognize(ocrImage);

        // Verify that OCR succeeded
        if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
        {
            Console.WriteLine("OCR failed or returned empty result.");
            return;
        }
```

**Wat gebeurt er onder de motorkap?**  
De GPU‑engine streamt de pixeldata naar CUDA‑kernels, die binarisatie, karaktersegmentatie en neurale‑netwerk‑inference uitvoeren—allemaal parallel. Daarom kun je **run OCR on image** bestanden die anders seconden op de CPU zouden duren.

---

## Stap 5: Extraheer tekst uit afbeelding en output

Tot slot **extract text from image** en tonen we het. Je kunt het resultaat ook naar een bestand, een database schrijven, of het voeden in downstream NLP‑pijplijnen.

```csharp
        // Step 5: Output the recognized plain‑text
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(ocrResult.Text);

        // Optional: Save to a .txt file for later processing
        System.IO.File.WriteAllText(@"C:\Output\ocr_result.txt", ocrResult.Text);
    }
}
```

**Verwachte output** (afgekapt voor beknoptheid):

```
=== OCR Result ===
Invoice #12345
Date: 03/15/2026
Total: $1,234.56
...
```

Als je het programma uitvoert en een vergelijkbaar blok ziet, gefeliciteerd—je hebt succesvol **run OCR on image** uitgevoerd met GPU‑versnelling!

---

## Omgaan met situaties zonder GPU (fallback)

Wat als de machine waarop je implementeert geen compatibele GPU heeft? De `GpuOcrEngine`‑constructor zal een `GpuNotSupportedException` gooien. Plaats de initialisatie in een try‑catch en val terug op `OcrEngine` (CPU) als volgt:

```csharp
        try
        {
            var gpuEngine = new GpuOcrEngine { DeviceId = 0 };
            // Continue with GPU workflow...
        }
        catch (GpuNotSupportedException)
        {
            Console.WriteLine("GPU not available – switching to CPU OCR.");
            var cpuEngine = new OcrEngine();
            OcrResult result = cpuEngine.Recognize(ocrImage);
            Console.WriteLine(result.Text);
        }
```

Dit patroon zorgt ervoor dat je app functioneel blijft ongeacht de hardware, een cruciale overweging voor cloud‑implementaties.

---

## Volledig werkend voorbeeld (klaar om te kopiëren en plakken)

Hieronder staat het **entire program**—geen ontbrekende onderdelen, vervang alleen de bestandspaden door die van jou.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;   // Namespace for GPU support

class GpuExample
{
    static void Main()
    {
        // 1️⃣ Create a GPU‑enabled OCR engine
        GpuOcrEngine gpuEngine;
        try
        {
            gpuEngine = new GpuOcrEngine { DeviceId = 0 }; // set GPU device ID
        }
        catch (GpuNotSupportedException)
        {
            Console.WriteLine("GPU not detected. Falling back to CPU engine.");
            var cpuEngine = new OcrEngine();
            RunCpuOcr(cpuEngine);
            return;
        }

        // 2️⃣ Load image for OCR
        var ocrImage = OcrImage.FromFile(@"C:\Images\large_document.jpg");
        if (ocrImage == null)
        {
            Console.WriteLine("Unable to load image – check the path.");
            return;
        }

        // 3️⃣ Recognize text from document
        OcrResult ocrResult = gpuEngine.Recognize(ocrImage);
        if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
        {
            Console.WriteLine("OCR returned no text.");
            return;
        }

        // 4️⃣ Extract text from image and output
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(ocrResult.Text);
        System.IO.File.WriteAllText(@"C:\Output\ocr_result.txt", ocrResult.Text);
    }

    // Helper for CPU fallback
    static void RunCpuOcr(OcrEngine cpuEngine)
    {
        var img = OcrImage.FromFile(@"C:\Images\large_document.jpg");
        var result = cpuEngine.Recognize(img);
        Console.WriteLine("=== CPU OCR Result ===");
        Console.WriteLine(result.Text);
    }
}
```

> **Opmerking:** De bovenstaande code extraheert automatisch **extract text from image** en schrijft het naar `ocr_result.txt`. Pas de paden aan indien nodig.

---

## Veelgestelde vragen & tips

| Vraag | Antwoord |
|-------|----------|
| *Heb ik een specifieke NVIDIA driver nodig?* | Ja—CUDA 11.x of nieuwer wordt aanbevolen. Controleer de release‑notes van Aspose voor exacte compatibiliteit. |
| *Kan ik meerdere afbeeldingen gelijktijdig verwerken?* | Absoluut. Plaats de OCR‑aanroep in een `Parallel.ForEach`‑lus, maar houd rekening met GPU‑geheugenlimieten. |
| *Wat als het OCR‑resultaat onleesbare tekens bevat?* | Probeer de beeldvoorbewerking aan te passen: `ocrImage.Binarize()` of `ocrImage.Deskew()` vóór herkenning. |
| *Is er een manier om het taalmodel te beperken?* | Stel `gpuEngine.Language = OcrLanguage.English;` in om de verwerking te versnellen als je alleen Engels nodig hebt. |

## Conclusie

Je hebt nu een **complete, end‑to‑end solution** om **run OCR on image**

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}