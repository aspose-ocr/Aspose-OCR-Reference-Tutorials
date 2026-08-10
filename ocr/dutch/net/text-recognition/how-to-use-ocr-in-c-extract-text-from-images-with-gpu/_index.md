---
category: general
date: 2026-02-13
description: Leer hoe je OCR in C# kunt gebruiken om tekst uit afbeeldingsbestanden
  te extraheren, GPU-verwerking in te schakelen en scans snel naar tekst te converteren.
draft: false
keywords:
- how to use OCR
- extract text from image
- how to extract text
- convert scan to text
- enable gpu processing
language: nl
og_description: Hoe OCR te gebruiken in C#? Deze gids laat zien hoe je tekst uit afbeeldingsbestanden
  kunt extraheren, GPU-verwerking kunt inschakelen en scans naar tekst kunt converteren.
og_title: Hoe OCR in C# te gebruiken – Tekst uit afbeeldingen halen met GPU
tags:
- OCR
- C#
- Aspose
- GPU
- Image Processing
title: Hoe OCR in C# te gebruiken – Tekst uit afbeeldingen halen met GPU
url: /nl/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-images-with-gpu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe OCR te gebruiken in C# – Tekst extraheren uit afbeeldingen met GPU

Heb je je ooit afgevraagd **hoe je OCR** kunt gebruiken om tekst uit een gescand document te halen zonder al te veel moeite? Je bent niet de enige—ontwikkelaars vragen constant: “Hoe kan ik efficiënt tekst uit afbeeldingsbestanden extraheren?” Het goede nieuws is dat je met Aspose.OCR precies dat kunt doen, en je kunt zelfs **GPU-verwerking inschakelen** voor een merkbare snelheidsboost op ondersteunde hardware.

In deze tutorial lopen we stap voor stap door een compleet end‑to‑end voorbeeld dat laat zien **hoe je OCR gebruikt**, hoe je **tekst uit een afbeelding** kunt **extraheren**, hoe je **scan naar tekst** converteert, en wat je moet doen als de GPU niet beschikbaar is. Aan het einde heb je een kant‑klaar C# console‑applicatie die de herkende tekst afdrukt en aangeeft of de GPU daadwerkelijk is gebruikt.

## Wat je nodig hebt

- .NET 6 SDK of later (de code werkt ook met .NET Core)  
- Visual Studio 2022 of een andere editor naar keuze  
- Aspose.OCR for .NET package (beschikbaar via NuGet)  
- Een hoge‑resolutie afbeelding (bijv. `highres_scan.tif`) om mee te testen  

Geen ingewikkelde setup nodig—slechts een paar NuGet‑commando’s en je bent er klaar voor.

## Stap 1: Installeer Aspose.OCR en bereid het project voor

Allereerst moet je de OCR‑bibliotheek in je project brengen. Open een terminal in de map van je solution en voer uit:

```bash
dotnet new console -n OcrDemo
cd OcrDemo
dotnet add package Aspose.OCR
```

Dit maakt een nieuw console‑project aan met de naam **OcrDemo** en voegt het `Aspose.OCR` NuGet‑pakket toe. De bibliotheek bevat de `OcrEngine`‑klasse die we gaan gebruiken.

> **Pro tip:** Als je op een machine met een dedicated GPU werkt, zorg er dan voor dat de nieuwste grafische driver geïnstalleerd is; anders valt de bibliotheek automatisch terug op CPU‑modus.

## Stap 2: Schrijf de volledige OCR‑code

Open nu `Program.cs` en vervang de inhoud door het volgende. Elke regel is becommentarieerd zodat je kunt zien *waarom* we doen wat we doen.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Enums;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣  Create an OCR engine and request GPU processing.
            //    If the GPU isn’t present, Aspose.OCR will silently
            //    switch to CPU mode – no crash, no extra code needed.
            // -------------------------------------------------
            var ocrEngine = new OcrEngine
            {
                ProcessingMode = OcrProcessingMode.Gpu
            };

            // -------------------------------------------------
            // 2️⃣  Define the path to the image you want to process.
            //    Replace the placeholder with the actual file location.
            // -------------------------------------------------
            string imagePath = @"YOUR_DIRECTORY/highres_scan.tif";

            // -------------------------------------------------
            // 3️⃣  Perform the recognition. The method returns an
            //    OcrResult object that contains the extracted text,
            //    confidence scores, and more.
            // -------------------------------------------------
            OcrResult ocrResult = ocrEngine.RecognizeImage(imagePath);

            // -------------------------------------------------
            // 4️⃣  Report whether the GPU was really used.
            //    This is handy for debugging performance issues.
            // -------------------------------------------------
            Console.WriteLine($"GPU used: {ocrEngine.IsGpuEnabled}");

            // -------------------------------------------------
            // 5️⃣  Output the recognized text to the console.
            //    In a real app you might write this to a file,
            //    a database, or feed it into another workflow.
            // -------------------------------------------------
            Console.WriteLine("=== Extracted Text ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

### Waarom dit werkt

- **ProcessingMode = Gpu** vertelt de engine eerst de GPU te proberen. De bibliotheek abstraheert de low‑level CUDA/OpenCL‑aanroepen, zodat je zelf geen device‑contexts hoeft te beheren.  
- **IsGpuEnabled** is een boolean die bevestigt of het GPU‑pad geslaagd is. Als je `false` ziet, is de engine automatisch teruggevallen op CPU—geen reden tot paniek.  
- **RecognizeImage** doet al het zware werk: het laadt de afbeelding, voert het OCR‑model uit en retourneert het platte‑tekst resultaat. Handmatige preprocessing van de bitmap is niet nodig tenzij je speciale eisen hebt (bijv. deskewing).

## Stap 3: Voer de applicatie uit en controleer de output

Compileer en start:

```bash
dotnet run
```

Als alles correct is ingesteld, zie je iets als:

```
GPU used: True
=== Extracted Text ===
This is the first line of the scanned document.
Here is the second line, and so on…
```

Als de GPU niet beschikbaar is, zal de eerste regel `GPU used: False` tonen, maar de geëxtraheerde tekst verschijnt nog steeds—dankzij de elegante fallback.

> **Veelgestelde vraag:** *Wat als mijn afbeelding een JPEG is in plaats van een TIFF?*  
> De `RecognizeImage`‑methode accepteert elk formaat dat door .NET’s `System.Drawing` wordt ondersteund (JPEG, PNG, BMP, enz.). Pas gewoon de bestandsextensie aan in `imagePath`.

## Stap 4: Optioneel – Pas instellingen aan voor betere nauwkeurigheid

Aspose.OCR biedt een paar instellingen die je kunt aanpassen:

| Instelling | Wat het doet | Wanneer te gebruiken |
|------------|--------------|----------------------|
| `ocrEngine.Language` | Forceert een specifieke taal (bijv. `OcrLanguage.English`) | Als je de taal van het document kent |
| `ocrEngine.PageSegMode` | Bepaalt hoe de engine pagina’s in blokken splitst | Voor lay‑outs met meerdere kolommen |
| `ocrEngine.DetectOrientation` | Roteert tekst automatisch die niet rechtop staat | Scans die mogelijk ondersteboven zijn |

Je kunt deze properties instellen vóór het aanroepen van `RecognizeImage`. Bijvoorbeeld:

```csharp
ocrEngine.Language = OcrLanguage.English;
ocrEngine.DetectOrientation = true;
```

## Stap 5: Visualiseer de flow (Afbeelding met alt‑tekst)

Hieronder staat een eenvoudige diagram die **hoe OCR te gebruiken** met optionele GPU‑versnelling illustreert. Het is niet vereist voor het uitvoeren van de code, maar helpt je het overzicht te behouden.

![Diagram showing how to use OCR with GPU processing](/images/ocr-gpu-flow.png)

*Alt‑tekst:* *Diagram dat laat zien hoe OCR met GPU‑verwerking werkt, met de fallback naar CPU wanneer nodig.*

## Randgevallen & Probleemoplossing

1. **Out‑of‑Memory op GPU** – Zeer grote afbeeldingen kunnen het GPU‑geheugen overschrijden. In dat geval valt de bibliotheek automatisch terug op CPU. Je kunt de afbeelding vooraf schalen om het geheugenverbruik laag te houden.  
2. **Niet‑ondersteund afbeeldingsformaat** – Als `RecognizeImage` een *NotSupportedException* gooit, controleer dan de bestandsextensie en zorg dat de afbeelding niet corrupt is. Omzetten naar PNG lost het vaak op.  
3. **Lage confidence‑scores** – Wanneer het OCR‑resultaat veel onleesbare tekens bevat, overweeg dan preprocessing (binarisatie, ruisverwijdering) of een scan met hogere resolutie.

## Samenvatting: Wat we hebben bereikt

We hebben net **hoe OCR te gebruiken** in een C# console‑applicatie behandeld, laten zien hoe je **tekst uit afbeelding**‑bestanden **extrahert**, en hoe je **GPU‑verwerking inschakelt** voor snellere resultaten. Je weet nu hoe je **scan naar tekst** converteert, controleert of de GPU daadwerkelijk is ingezet, en een paar instellingen aanpast voor rand‑situaties.

### Volgende stappen

- Probeer de output te voeden aan een **search index** (bijv. Elasticsearch) zodat je gescande PDF’s doorzoekbaar worden.  
- Experimenteer met **batch processing**—loop over een map met afbeeldingen en schrijf elk resultaat naar een `.txt`‑bestand.  
- Combineer OCR met **vertalings‑API’s** om automatisch gescande documenten in vreemde talen te vertalen.  

Heb je meer vragen? Laat een reactie achter, en happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}