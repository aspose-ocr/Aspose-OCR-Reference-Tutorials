---
category: general
date: 2026-04-01
description: Leer hoe je snel tekst uit png‑bestanden kunt herkennen door de GPU‑apparaat‑ID
  in te stellen en GPU‑versnelling in Aspose OCR in te schakelen. Stapsgewijze C#‑handleiding.
draft: false
keywords:
- recognize text from png
- set gpu device id
- Aspose OCR GPU
- batch OCR C#
- OCR performance tips
language: nl
og_description: herken tekst uit png‑bestanden snel door de GPU‑apparaat‑ID in te
  stellen. Volg deze volledige C#‑gids om GPU‑versnelling in te schakelen met Aspose
  OCR.
og_title: tekst herkennen uit png – GPU-versnelde Aspose OCR‑tutorial
tags:
- C#
- OCR
- GPU
- Aspose
title: herken tekst van png met Aspose OCR – GPU-versnelde batchdemo
url: /nl/net/ocr-optimization/recognize-text-from-png-with-aspose-ocr-gpu-accelerated-batc/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# herken tekst van png – Volledige C# GPU‑Versnelde Batch Tutorial

Heb je ooit **tekst van png** afbeeldingen moeten **herkennen**, maar vond je het proces pijnlijk traag? Je bent niet de enige. De meeste ontwikkelaars beginnen met een eenvoudige OCR‑aanroep, en vervolgens staren ze naar een console die kruipt als een slak wanneer een map tientallen screenshots bevat.  

Het goede nieuws? Aspose OCR kan het zware werk uitbesteden aan je grafische kaart, en met slechts een paar regels kun je **set gpu device id** gebruiken om de exacte GPU te kiezen die je wilt. In deze gids lopen we een volledig, uitvoerbaar voorbeeld door dat elke PNG uit een map haalt, GPU‑versnelling inschakelt, de eerste GPU selecteert en het teken‑aantal voor elk bestand afdrukt.

Aan het einde heb je een zelf‑containend programma dat je in elk .NET‑project kunt plaatsen, en begrijp je waarom het inschakelen van de GPU belangrijk is, hoe je randgevallen afhandelt en wat je kunt aanpassen voor nog betere prestaties.

## Wat je nodig hebt

- **.NET 6.0** of later (de code compileert ook met .NET Core).  
- Het **Aspose.OCR** NuGet‑pakket – installeer het met `dotnet add package Aspose.OCR`.  
- Een machine met een CUDA‑compatibele GPU (NVIDIA is gebruikelijk) en het juiste stuurprogramma.  
- Een map vol met **PNG**‑afbeeldingen die je wilt verwerken.  

Als een van deze onbekend klinkt, geen paniek. De stappen hieronder bevatten de exacte commando’s die je nodig hebt, en we bespreken ook wat te doen wanneer er geen GPU aanwezig is.

## Stap 1: Initialiseer de OCR‑engine en schakel GPU‑versnelling in  

Het eerste wat je moet doen is een `OcrEngine`‑instantie maken en GPU‑ondersteuning inschakelen. Deze vlag vertelt Aspose om de native CUDA‑bibliotheken onder de motorkap te gebruiken.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU‑specific namespace
using System;

class GpuBatchDemo
{
    static void Main()
    {
        // Initialise the OCR engine
        var ocrEngine = new OcrEngine();

        // Enable GPU acceleration – huge speed boost for large batches
        ocrEngine.UseGpuAcceleration = true;
```

**Waarom dit belangrijk is:** Zonder `UseGpuAcceleration` wordt elke afbeelding op de CPU verwerkt, wat orders van grootte langzamer kan zijn, vooral voor high‑resolution PNG’s. Het inschakelen van de vlag bereidt de engine ook voor om later een specifiek GPU‑apparaat te accepteren.

## Stap 2: Stel GPU‑apparaat‑ID in (optioneel maar aanbevolen)  

Als je werkstation meer dan één GPU heeft, kun je bepalen welke je wilt gebruiken. De apparaat‑ID’s beginnen bij **0**, dus `0` kiest de eerste GPU, `1` de tweede, enzovoort.

```csharp
        // Optional: Choose the GPU device – 0 selects the first GPU
        ocrEngine.GpuDeviceId = 0;   // <-- set gpu device id
```

**Pro tip:** Wanneer je op een gedeelde server draait, kan het expliciet instellen van de GPU‑apparaat‑ID voorkomen dat je taak resources van andere processen steelt. Als je deze regel weglaten, kiest Aspose het standaardapparaat, wat meestal prima is voor een enkele‑GPU‑configuratie.

## Stap 3: Verzamel alle PNG‑bestanden uit je batch‑map  

Vervolgens moeten we elke PNG die je wilt OCR‑en lokaliseren. De `Directory.GetFiles`‑methode doet het zware werk.

```csharp
        // Retrieve all PNG images from the batch folder
        string[] imageFiles = System.IO.Directory.GetFiles(
            @"YOUR_DIRECTORY\Batch",   // <-- replace with your path
            "*.png",                  // only PNG files
            System.IO.SearchOption.TopDirectoryOnly);
```

**Randgeval:** Als de map leeg is, zal `imageFiles` een lege array zijn. We behandelen dat later met een vriendelijke melding.

## Stap 4: Verwerk elke afbeelding en geef het herkende teken‑aantal weer  

Nu de kernlus. Voor elke PNG roepen we `Recognize` aan, en drukken vervolgens de bestandsnaam en de lengte van de geëxtraheerde tekst af.

```csharp
        // Verify we actually found files
        if (imageFiles.Length == 0)
        {
            Console.WriteLine("No PNG files found in the specified folder.");
            return;
        }

        // Process each image and display the recognised character count
        foreach (var imagePath in imageFiles)
        {
            var ocrResult = ocrEngine.Recognize(imagePath);
            Console.WriteLine($"{System.IO.Path.GetFileName(imagePath)} → {ocrResult.Text.Length} chars");
        }
    }
}
```

**Wat je zult zien:**  
```
invoice1.png → 342 chars
receipt_2023.png → 127 chars
screenshot.png → 0 chars
```

Als een afbeelding geen tekst bevat, zal het aantal `0` zijn. Dat is volkomen normaal voor screenshots die puur grafisch zijn.

## Stap 5: Voer het programma uit en verifieer GPU‑gebruik  

Compileer het bestand (`dotnet build`) en voer het uit (`dotnet run`). Terwijl de console scrollt, kun je je GPU‑monitoringtool (zoals NVIDIA Smi) openen om de GPU‑benutting kortstondig te zien pieken voor elke afbeelding. Als je geen activiteit ziet, controleer dan:

1. Het CUDA‑stuurprogramma is geïnstalleerd.  
2. `UseGpuAcceleration` is ingesteld op `true`.  
3. De juiste `GpuDeviceId` overeenkomt met een fysieke GPU.

Als de GPU niet beschikbaar is, valt Aspose automatisch terug op de CPU, maar je verliest dan het snelheidsvoordeel.

## Veelvoorkomende variaties & tips  

| Situatie | Wat te wijzigen |
|-----------|----------------|
| **Ander afbeeldingsformaat** (bijv. JPEG) | Verander het zoekpatroon naar `*.jpg` of `*.*` en Aspose zal de tekst nog steeds herkennen. |
| **Batch‑grootte is enorm** (duizenden bestanden) | Verwerk in delen om geheugenbelasting te vermijden: splits `imageFiles` in kleinere arrays. |
| **De daadwerkelijke tekst nodig, niet alleen de lengte** | Vervang `ocrResult.Text.Length` door `ocrResult.Text` in de `WriteLine`. |
| **Uitvoeren op een headless server** | Zorg ervoor dat de server een GPU‑stuurprogramma heeft; anders, stel `UseGpuAcceleration = false` in om onnodige fouten te voorkomen. |
| **Meerdere GPU's, wil de belasting balanceren** | Loop over `ocrEngine.GpuDeviceId = i % gpuCount` binnen de `foreach` om apparaten te roteren. |

## Verwachte output & verificatie  

Wanneer alles werkt, drukt de console elke bestandsnaam af gevolgd door het teken‑aantal, zoals eerder getoond. Om de daadwerkelijke OCR‑output dubbel te controleren, kun je tijdelijk de tekst dumpen:

```csharp
Console.WriteLine($"{Path.GetFileName(imagePath)} → {ocrResult.Text}");
```

Vergeet niet die regel te verwijderen of te commentariëren voor grote batches; het afdrukken van duizenden regels kan je terminal overstromen.

## Volledig werkend voorbeeld (klaar om te kopiëren en plakken)

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU‑specific namespace
using System;

class GpuBatchDemo
{
    static void Main()
    {
        // Step 1: Initialise the OCR engine and enable GPU acceleration
        var ocrEngine = new OcrEngine();
        ocrEngine.UseGpuAcceleration = true;

        // Step 2: (Optional) Choose the GPU device – 0 selects the first GPU
        ocrEngine.GpuDeviceId = 0;   // <-- set gpu device id

        // Step 3: Retrieve all PNG images from the batch folder
        string[] imageFiles = System.IO.Directory.GetFiles(
            @"YOUR_DIRECTORY\Batch",   // replace with your folder path
            "*.png",
            System.IO.SearchOption.TopDirectoryOnly);

        // Guard clause if no files are found
        if (imageFiles.Length == 0)
        {
            Console.WriteLine("No PNG files found in the specified folder.");
            return;
        }

        // Step 4: Process each image and display the recognised character count
        foreach (var imagePath in imageFiles)
        {
            var ocrResult = ocrEngine.Recognize(imagePath);
            Console.WriteLine($"{System.IO.Path.GetFileName(imagePath)} → {ocrResult.Text.Length} chars");
        }
    }
}
```

Sla dit op als `GpuBatchDemo.cs`, voer `dotnet add package Aspose.OCR` uit, daarna `dotnet run`. Je zou de teken‑aantallen bijna onmiddellijk moeten zien verschijnen voor elke PNG, dankzij GPU‑versnelling.

## Conclusie  

Je weet nu hoe je **tekst van png** bestanden efficiënt kunt **herkennen** door GPU‑versnelling in te schakelen en expliciet **set gpu device id** te gebruiken in Aspose OCR. Het volledige, copy‑and‑paste‑programma behandelt mapdetectie, rand‑case controles, en geeft je directe feedback over OCR‑prestaties.  

Volgende stappen? Probeer de `Recognize`‑aanroep te vervangen door `ocrEngine.RecognizeAsync` als je niet‑blokerende verwerking nodig hebt, of experimenteer met verschillende beeld‑pre‑processingopties (bijv. binarisatie) die Aspose biedt. Je kunt de OCR‑resultaten ook doorsturen naar een database of een zoekindex voor een full‑text‑search‑oplossing.

Heb je vragen over het verwerken van multi‑page PDF’s, of wil je Aspose OCR vergelijken met Tesseract? Laat een reactie achter of verken onze andere tutorials over **batch OCR C#**, **OCR performance tips**, en **GPU‑gedreven beeldverwerking**. Veel programmeerplezier!  

![Console-uitvoer die herkende tekenaantallen voor PNG‑bestanden toont – tekst van png herkennen met GPU‑versnelling](image-placeholder.png "voorbeeld van console‑output voor herkenning van tekst van png")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}