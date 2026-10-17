---
category: general
date: 2026-03-18
description: Stel het GPU-apparaat in Aspose OCR in om snel tekst uit een afbeelding
  te extraheren. Leer hoe je een afbeelding laadt voor OCR, een bonafbeelding herkent
  en nauwkeurige resultaten krijgt.
draft: false
keywords:
- set GPU device
- extract text from image
- how to extract text
- load image for OCR
- recognize receipt image
language: nl
og_description: Stel GPU-apparaat in Aspose OCR in om snel tekst uit een afbeelding
  te extraheren. Volg deze stapsgewijze handleiding om een afbeelding te laden voor
  OCR en een bonafbeelding te herkennen.
og_title: GPU-apparaat instellen voor OCR in C# – Complete programmeergids
tags:
- OCR
- C#
- GPU
- Aspose
title: GPU-apparaat instellen voor OCR in C# – Complete programmeergids
url: /nl/net/ocr-configuration/set-gpu-device-for-ocr-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# GPU‑apparaat instellen voor OCR in C# – Complete programmeergids

Moet u **set GPU device** voor snellere OCR-verwerking? In deze gids laten we u stap voor stap zien hoe u **set GPU device** gebruikt met Aspose OCR, en vervolgens tekst uit een afbeelding van een bon haalt in slechts een paar regels code.  

Als u ooit moeite heeft gehad met **load image for OCR** of zich afvroeg *hoe tekst te extraheren* uit scans met hoge resolutie, dan bent u op de juiste plek. Aan het einde heeft u een uitvoerbaar programma dat een bonafbeelding herkent, de platte tekst afdrukt, en elegant terugvalt als de GPU niet beschikbaar is.

## Wat deze tutorial behandelt

* Het installeren van het Aspose OCR NuGet‑pakket (de enige externe afhankelijkheid).  
* Het instellen van het GPU‑apparaat (`set GPU device`) en eventueel een andere GPU‑index kiezen.  
* Het laden van een afbeeldingsbestand voor OCR – ja, dat omvat de gevreesde “load image for OCR” stap die veel beginners tegenkomt.  
* Het uitvoeren van de herkenningsengine om **recognize receipt image** inhoud te verwerken.  
* Het extraheren van de resulterende string zodat u **extract text from image** kunt gebruiken in uw app.  

Geen magie, geen verborgen documentatielinks – gewoon een complete, zelfstandige oplossing die u kunt kopiëren‑plakken in Visual Studio en vandaag nog kunt uitvoeren.

## Vereisten

* .NET 6.0 of later (de code werkt ook op .NET Core en .NET Framework).  
* Een GPU‑capabele machine met de juiste drivers geïnstalleerd – anders schakelt de bibliotheek automatisch over naar CPU‑modus.  
* Een voorbeeldbonafbeelding (bijv. `receipt_highres.png`) ergens geplaatst die u met een volledig pad kunt refereren.  

Dat is alles. Als u het NuGet‑pakket mist, voer dan `dotnet add package Aspose.OCR` uit in uw projectmap.

---

## Stap 1 – GPU‑apparaat instellen in Aspose OCR

Het eerste dat u moet doen is **set GPU device** op de OCR‑engine. Dit vertelt Aspose om het zware werk over te dragen aan de grafische kaart in plaats van de CPU.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;

class GpuDemo
{
    static void Main()
    {
        // Create the OCR engine instance
        var ocrEngine = new OcrEngine();

        // Enable GPU processing – this is where we set the GPU device
        ocrEngine.Settings.ProcessingMode = ProcessingMode.Gpu;

        // (Optional) Choose a specific GPU if you have more than one.
        // The default is device 0, but you can set it to 1, 2, etc.
        ocrEngine.Settings.GpuDeviceId = 0;
```

**Waarom dit belangrijk is:**  
Wanneer de engine draait in `ProcessingMode.Gpu`, kunnen de onderliggende CUDA‑kernels de karaktersegmentatie en neurale‑netwerk‑inference aanzienlijk versnellen. Op een moderne RTX 3080 ziet u OCR‑tijden dalen van seconden naar sub‑seconden voor bonnen met hoge resolutie.

> **Pro tip:** Als u niet zeker weet welke GPU‑index u moet gebruiken, roep dan `OcrEngine.GetAvailableGpuDevices()` aan (beschikbaar in nieuwere versies) en kies degene met het meeste vrije geheugen.

## Stap 2 – Afbeelding laden voor OCR

Nu de engine is geconfigureerd, moeten we **load image for OCR**. Aspose biedt een handige `ImageStream`‑wrapper die bestands‑I/O abstraheert en streams ondersteunt vanuit geheugen, netwerk of schijf.

```csharp
        // Load the receipt image you want to recognize
        var imagePath = @"C:\OCR\Samples\receipt_highres.png";
        var imageStream = ImageStream.FromFile(imagePath);
```

**Wat kan er misgaan?**  
Als het bestandspad onjuist is of de afbeelding corrupt, zal `FromFile` een `FileNotFoundException` werpen. Een snelle `File.Exists(imagePath)`‑controle vóór het aanmaken van de stream voorkomt een nare crash.

## Stap 3 – Bonafbeelding herkennen

Met de afbeelding in de hand roepen we `Recognize` aan. Dit is de stap die daadwerkelijk **recognize receipt image** inhoud verwerkt met de eerder ingestelde GPU‑versnelde pipeline.

```csharp
        // Perform OCR – this returns an OcrResult object
        var ocrResult = ocrEngine.Recognize(imageStream);
```

**Achter de schermen:**  
De engine converteert eerst de afbeelding naar een genormaliseerde grijstinten‑bitmap, waarna een deep‑learning‑model wordt uitgevoerd dat karakter‑probabilities voorspelt. Omdat we op GPU werken, verwerkt het model de volledige bitmap parallel, waardoor grote bonnen snel worden afgerond.

## Stap 4 – Tekst uit afbeelding extraheren en output verifiëren

Tot slot halen we het platte‑tekstresultaat uit de `OcrResult` en schrijven het naar de console. Dit is het moment waarop u **extract text from image** uitvoert en het kunt doorgeven aan downstream‑logica (bijv. het parseren van regelitems).

```csharp
        // Output the recognized plain text
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(ocrResult.Text);
        Console.WriteLine("==================");
    }
}
```

**Verwachte output:**  

```
=== OCR Result ===
Store Name
Date: 03/15/2026
Item A   $12.99
Item B   $5.49
Total    $18.48
==================
```

Als de tekst er onduidelijk uitziet, controleer dan of de afbeelding een hoge resolutie heeft en of de GPU‑driver up‑to‑date is. U kunt ook `ocrEngine.Settings.PreprocessMode` schakelen om het contrast te verbeteren bij slecht verlichte bonnen.

## Stap 5 – Terugvallen op CPU (afhandeling van randgevallen)

Wat als de doelmachine geen compatibele GPU heeft? In plaats van te crashen, kunt u de situatie detecteren en overschakelen naar CPU‑verwerking.

```csharp
        // Detect GPU availability – fallback if needed
        if (!ocrEngine.IsGpuAvailable)
        {
            Console.WriteLine("GPU not detected, falling back to CPU mode.");
            ocrEngine.Settings.ProcessingMode = ProcessingMode.Cpu;
        }
```

**Waarom dit opnemen?**  
In CI‑pipelines of cloud‑containers draait u vaak op headless‑servers zonder GPU. Gracieuze degradatie zorgt ervoor dat dezelfde code overal werkt.

## Veelvoorkomende valkuilen en praktische tips

| Valkuil | Hoe te vermijden |
|---------|-------------------|
| Vergeten om `ProcessingMode` in te stellen vóór het laden van de afbeelding. | Configureer altijd eerst de engine (Stap 1). |
| De verkeerde GPU‑index gebruiken (`GpuDeviceId`). | Vraag beschikbare apparaten op of blijf bij de standaard `0`. |
| Een afbeelding met lage resolutie laden, wat de OCR‑nauwkeurigheid vermindert. | Streef naar minimaal 300 DPI voor bonnen. |
| `ImageStream` niet vrijgeven – leidt tot bestandsvergrendelingen. | Plaats de stream in een `using`‑blok of roep handmatig `Dispose()` aan. |
| De `IsGpuAvailable`‑vlag negeren op machines zonder CUDA. | Voeg de fallback‑logica toe uit Stap 5. |

## Volledig werkend voorbeeld (klaar om te kopiëren‑plakken)

Hieronder staat het volledige programma, klaar om te compileren. Sla het op als `Program.cs`, voeg het Aspose OCR NuGet‑pakket toe, en voer het uit.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;

class GpuDemo
{
    static void Main()
    {
        // ---------- Step 1: Set GPU device ----------
        var ocrEngine = new OcrEngine();
        ocrEngine.Settings.ProcessingMode = ProcessingMode.Gpu; // set GPU device
        ocrEngine.Settings.GpuDeviceId = 0; // use the first GPU (change if needed)

        // Optional: fallback if GPU isn't present
        if (!ocrEngine.IsGpuAvailable)
        {
            Console.WriteLine("GPU not detected, switching to CPU.");
            ocrEngine.Settings.ProcessingMode = ProcessingMode.Cpu;
        }

        // ---------- Step 2: Load image for OCR ----------
        var imagePath = @"C:\OCR\Samples\receipt_highres.png";
        if (!System.IO.File.Exists(imagePath))
        {
            Console.WriteLine($"File not found: {imagePath}");
            return;
        }
        var imageStream = ImageStream.FromFile(imagePath);

        // ---------- Step 3: Recognize receipt image ----------
        var ocrResult = ocrEngine.Recognize(imageStream);

        // ---------- Step 4: Extract text from image ----------
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(ocrResult.Text);
        Console.WriteLine("==================");
    }
}
```

Het uitvoeren van het programma drukt de geëxtraheerde bontekst af naar de console, precies zoals eerder getoond. U kunt die string nu doorsturen naar een parser, een database, of elke andere bedrijfslogica die u nodig heeft.

## Conclusie

We hebben u laten zien hoe u **set GPU device** in Aspose OCR, **load image for OCR**, en **recognize receipt image** kunt uitvoeren zodat u **extract text from image** met razendsnelle snelheid kunt doen. Het volledige, uitvoerbare voorbeeld toont zowel het “hoe” als het “waarom”, en biedt u een solide basis voor elk C# OCR‑project dat GPU‑versnelling nodig heeft.

Klaar voor de volgende stap? Probeer te experimenteren met:

* Meerdere afbeeldingen parallel verwerken met `Parallel.ForEach`.  
* Het aanpassen van `ocrEngine.Settings.PreprocessMode` om resultaten te verbeteren bij scans met laag contrast.  
* De OCR‑output exporteren naar JSON voor downstream‑analyse.  

Voel u vrij om een reactie achter te laten als u tegen problemen aanloopt, en happy coding!

![Diagram dat laat zien hoe GPU‑apparaat in te stellen voor OCR‑verwerking](set-gpu-device.png "GPU‑apparaat instellen")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}