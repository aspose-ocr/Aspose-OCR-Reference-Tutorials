---
category: general
date: 2026-03-17
description: Tekst extraheren uit PNG met Aspose OCR in C#. Leer tekst uit een afbeelding
  te lezen, verwerk bon‑OCR en maak een OCR‑engine met GPU‑versnelling.
draft: false
keywords:
- extract text from png
- read text from image
- ocr receipt image
- process receipt ocr
- create ocr engine
language: nl
og_description: Tekst extraheren uit PNG met Aspose OCR. Deze gids laat zien hoe je
  tekst uit een afbeelding leest, bon‑OCR verwerkt en een OCR‑engine efficiënt maakt.
og_title: Tekst extraheren uit PNG – Tekst lezen van afbeelding met OCR
tags:
- OCR
- CSharp
- Aspose
title: Tekst extraheren uit PNG – Tekst lezen uit afbeelding met OCR
url: /nl/net/text-recognition/extract-text-from-png-read-text-from-image-with-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tekst extraheren uit PNG – Tekst lezen uit afbeelding met OCR

Heb je ooit **tekst uit PNG** moeten extraheren maar wist je niet welke bibliotheek betrouwbare resultaten levert? Je bent niet de enige—ontwikkelaars vragen voortdurend: “Hoe lees ik tekst uit afbeeldingsbestanden zoals bonnetjes zonder een eigen neuraal netwerk te schrijven?” Het goede nieuws is dat Aspose OCR het zware werk voor je doet, en je kunt zelfs de GPU inschakelen voor een snelheidsboost.

In deze tutorial lopen we alles door wat je nodig hebt om **receipt OCR te verwerken**, van het installeren van het NuGet‑pakket tot het maken van een OCR‑engine die je PNG‑bestand begrijpt. Aan het einde heb je een zelfstandige console‑app die een bonafbeelding leest, de herkende tekst afdrukt, en je laat zien hoe je de engine kunt afstemmen voor verschillende scenario's. Geen externe documentatie, alleen pure code en duidelijke uitleg.

## Vereisten

- .NET 6.0 SDK (of een recente .NET‑versie)  
- Visual Studio 2022 of VS Code met C#‑extensies  
- Een ondersteunde NVIDIA‑GPU met de nieuwste driver (optioneel, maar aanbevolen voor GPU‑modus)  
- Het **Aspose.OCR** NuGet‑pakket (`dotnet add package Aspose.OCR`)  

Als je geen GPU hebt, kun je het voorbeeld nog steeds uitvoeren in CPU‑modus—sla gewoon de GPU‑configuratieregels over.

## Stap 1: Installeer Aspose.OCR en zet het project op

Maak eerst een nieuw console‑project aan en voeg de Aspose OCR‑bibliotheek toe.

```bash
dotnet new console -n ReceiptOcrDemo
cd ReceiptOcrDemo
dotnet add package Aspose.OCR
```

Waarom dit belangrijk is: het `Aspose.OCR`‑pakket bevat de OCR‑engine, afbeeldingsladers en optionele GPU‑ondersteuning. Het via NuGet toevoegen zorgt ervoor dat je de nieuwste stabiele versie krijgt (vanaf maart 2026 is dat 23.10).

## Stap 2: Importeer namespaces en maak de OCR‑engine

Open nu **Program.cs** en voeg de vereiste `using`‑directieven toe. Instantieer vervolgens de engine.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 2: Create an OCR engine instance
            var ocrEngine = new OcrEngine();

            // Optional: Enable GPU acceleration if a compatible GPU is present
            // This dramatically speeds up processing of high‑resolution PNGs
            ocrEngine.Config.EngineMode = EngineMode.Gpu;   // <-- primary way to "process receipt ocr" fast
            ocrEngine.Config.GpuDeviceId = 0; // selects the first GPU in the system

            // The rest of the code follows...
```

**Pro tip:** Als je een `System.DllNotFoundException` tegenkomt op machines zonder GPU, commentaar dan gewoon de twee regels die `EngineMode` en `GpuDeviceId` instellen uit. De engine schakelt automatisch over naar CPU.

## Stap 3: Laad de PNG‑afbeelding die je wilt gebruiken voor tekstextractie

Aspose OCR kan afbeeldingen direct lezen vanaf een bestandspad, een stream, of zelfs een byte‑array. Voor deze demo laden we een lokaal bon‑beeld.

```csharp
            // Step 3: Load the image (replace the path with your own PNG file)
            string imagePath = @"C:\Images\receipt.png";

            // Validate the file exists to avoid runtime surprises
            if (!System.IO.File.Exists(imagePath))
            {
                Console.WriteLine($"Error: File not found – {imagePath}");
                return;
            }

            // Load the image into the engine
            ocrEngine.Image = ImageStream.FromFile(imagePath);
```

Let op hoe we controleren op een ontbrekend bestand. In echte toepassingen zou je waarschijnlijk een vriendelijke UI‑melding tonen in plaats van simpelweg af te sluiten.

## Stap 4: Voer de OCR‑herkenning uit

De daadwerkelijke tekstextractie gebeurt met één methode‑aanroep. De engine retourneert een `OcrResult`‑object dat de ruwe string, vertrouwensscores en lay‑outinformatie bevat.

```csharp
            // Step 4: Run the OCR process
            OcrResult ocrResult = ocrEngine.Recognize();

            // Check if the engine succeeded
            if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
            {
                Console.WriteLine("No text could be recognized.");
                return;
            }
```

Waarom we `ocrResult.Text` controleren: soms levert een PNG van lage kwaliteit een lege string op, en het is beter de gebruiker te informeren dan stilletjes niets uit te voeren.

## Stap 5: Output de herkende tekst

Print tenslotte de geëxtraheerde string naar de console. Je kunt deze ook naar een bestand, een database schrijven, of doorgeven aan een andere service.

```csharp
            // Step 5: Display the recognized text
            Console.WriteLine("=== Extracted Text from PNG ===");
            Console.WriteLine(ocrResult.Text);
            Console.WriteLine("=== End of Output ===");
        }
    }
}
```

Wanneer je het programma uitvoert (`dotnet run`), zou je iets moeten zien als:

```
=== Extracted Text from PNG ===
Store: Coffee Corner
Date: 03/15/2026
Item      Qty   Price
Latte      2    $5.40
Muffin     1    $2.30
Total            $7.70
=== End of Output ===
```

Dat is de **complete oplossing om tekst uit PNG**‑bestanden te extraheren met Aspose OCR, en je hebt zojuist geleerd hoe je **tekst uit afbeelding**‑bestanden kunt lezen die op bonnetjes lijken.

## Optioneel: Fijn afstellen van de OCR‑engine (Geavanceerd)

Als je een hogere nauwkeurigheid nodig hebt voor specifieke lettertypen of ruisige achtergronden, overweeg dan deze instellingen aan te passen:

```csharp
// Enable language detection (default is English)
ocrEngine.Config.Language = Language.English;

// Turn on automatic image preprocessing (deskew, binarization)
ocrEngine.Config.EnableImagePreprocessing = true;

// Set a confidence threshold if you only want high‑certainty results
ocrEngine.Config.ConfidenceThreshold = 0.75f;
```

Deze aanpassingen zijn vooral nuttig wanneer je **receipt OCR verwerkt** in batch‑taken waarbij sommige scans minder dan perfect zijn.

## Veelvoorkomende valkuilen & hoe ze te vermijden

| Probleem | Waarom het gebeurt | Oplossing |
|----------|--------------------|-----------|
| **GPU-driver ontbreekt** | De engine probeert CUDA te laden maar kan de DLL niet vinden. | Installeer de nieuwste NVIDIA-driver of schakel over naar CPU-modus door de regel `EngineMode.Gpu` te verwijderen. |
| **Onjuist afbeeldingspad** | `ImageStream.FromFile` geeft een fout als het bestand niet wordt gevonden. | Valideer altijd het pad (zie Stap 3) of gebruik `Path.Combine` voor cross‑platform veiligheid. |
| **Lage betrouwbaarheid bij onscherpe bonnetjes** | De OCR-engine kan de tekens niet onderscheiden. | Schakel `EnableImagePreprocessing` in en verhoog eventueel de DPI van de afbeelding voordat je deze aan de engine doorgeeft. |
| **Geheugenlek in langdurige services** | Elke `OcrEngine` houdt onbeheerste resources vast. | Dispose de engine na gebruik: `using var ocrEngine = new OcrEngine();` |

## Volledig werkend voorbeeld (Kopie‑Plak)

Hieronder staat het **volledige programma** dat je in `Program.cs` kunt plakken. Het bevat alle optionele aanpassingen, uitgecommentarieerd voor eenvoudige activering.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Create OCR engine
            using var ocrEngine = new OcrEngine();

            // Enable GPU acceleration if you have a supported card
            ocrEngine.Config.EngineMode = EngineMode.Gpu;
            ocrEngine.Config.GpuDeviceId = 0;

            // Optional fine‑tuning (uncomment as needed)
            //ocrEngine.Config.Language = Language.English;
            //ocrEngine.Config.EnableImagePreprocessing = true;
            //ocrEngine.Config.ConfidenceThreshold = 0.75f;

            // Load PNG image
            string imagePath = @"C:\Images\receipt.png";
            if (!System.IO.File.Exists(imagePath))
            {
                Console.WriteLine($"Error: File not found – {imagePath}");
                return;
            }
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // Perform OCR
            OcrResult ocrResult = ocrEngine.Recognize();

            // Verify result
            if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
            {
                Console.WriteLine("No text could be recognized.");
                return;
            }

            // Output the extracted text
            Console.WriteLine("=== Extracted Text from PNG ===");
            Console.WriteLine(ocrResult.Text);
            Console.WriteLine("=== End of Output ===");
        }
    }
}
```

![voorbeeld van tekst extraheren uit png](receipt.png "voorbeeld van tekst extraheren uit png")

*De afbeelding hierboven toont een voorbeeld van een bon‑PNG die de code kan verwerken.*

## Samenvatting

We hebben behandeld hoe je **tekst uit PNG**‑bestanden kunt extraheren met Aspose OCR, laten zien hoe je **tekst uit afbeelding**‑bestanden kunt lezen, en een volledige **receipt OCR verwerkings**‑pipeline doorlopen die optionele GPU‑versnelling bevat. Door zelf een **OCR‑engine te maken**, krijg je volledige controle over configuratie, prestaties en foutafhandeling.

## Wat kun je hierna verkennen?

- **Batchverwerking**: Loop over een map met PNG‑bonnetjes en schrijf elk resultaat naar een CSV‑bestand.  
- **Integratie met Azure Functions**: Zet deze console‑app om in een serverloze endpoint die afbeeldingsuploads accepteert.  
- **Meertalige ondersteuning**: Vervang `Language.English` door `Language.Spanish` of voeg aangepaste woordenboeken toe.  
- **Post‑processing**: Gebruik reguliere expressies om velden zoals totaalbedrag, datum of btw‑nummer uit de ruwe OCR‑string te extraheren.

Voel je vrij om te experimenteren—OCR is een verrassend flexibel hulpmiddel zodra je de juiste instellingen kent. Als je ergens tegenaan loopt, laat dan een reactie achter of raadpleeg de Aspose OCR API‑referentie voor meer verdieping.

Veel plezier met coderen, en geniet van het omzetten van die koppige PNG‑bonnetjes naar doorzoekbare tekst!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}