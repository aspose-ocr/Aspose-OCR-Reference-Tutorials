---
category: general
date: 2026-01-12
description: c# ocr‑tutorial die laat zien hoe je tekst in een afbeelding herkent,
  tekst uit een afbeelding haalt met c# en een afbeelding naar pdf‑ocr‑bestand genereert
  met vertrouwensscores.
draft: false
keywords:
- c# ocr tutorial
- image to pdf ocr
- recognize text image
- ocr confidence scores
- extract text image c#
language: nl
og_description: Leer een complete C# OCR‑tutorial om tekstafbeeldingen te herkennen,
  tekst uit afbeeldingen te extraheren met C# en een afbeelding‑naar‑PDF OCR‑document
  te maken met vertrouwensscores.
og_title: c# ocr tutorial – Converteer afbeeldingen naar doorzoekbare pdf's
tags:
- OCR
- C#
- PDF
title: c# OCR‑tutorial – Zet afbeeldingen om in doorzoekbare PDF‑bestanden
url: /nl/net/text-recognition/c-ocr-tutorial-turn-images-into-searchable-pdfs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr tutorial – Zet afbeeldingen om in doorzoekbare PDF's

Heb je je ooit afgevraagd hoe je **tekst in afbeelding** bestanden kunt herkennen in een C# project zonder op zoek te gaan naar diensten van derden? Je bent niet de enige. In veel real‑world apps—denk aan factuurscanners, bonregistraties of meertalige documentarchieven—hebben ontwikkelaars een betrouwbare, on‑premise OCR‑engine nodig die ook vertrouwensscores levert.  

Deze **c# ocr tutorial** leidt je stap voor stap door alles wat je nodig hebt: van het laden van een afbeelding, het selecteren van taalmodellen, het schakelen van GPU‑versnelling, tot het opslaan van het resultaat als een doorzoekbare PDF. Aan het einde heb je een kant‑klaar code‑voorbeeld dat tekst extraheert, OCR‑vertrouwen rapporteert, en optioneel een *image to pdf ocr* bestand maakt—alles in minder dan een minuut coderen.

## Wat je gaat bouwen

- Laad een meertalige afbeelding (`sample_multi_lang.jpg` wordt als voorbeeld gebruikt).  
- Kies Arabische, Hindi‑ en Russische taalmodellen (je kunt er meer toevoegen).  
- Schakel GPU‑verwerking in als je machine dat ondersteunt.  
- Verkrijg het ruwe OCR‑resultaat **met vertrouwensscores**.  
- Serialiseer het resultaat naar mooi opgemaakte JSON **of** schrijf een doorzoekbare PDF.  

Geen externe webservices, geen verborgen magie—alleen Aspose.OCR voor .NET, een paar regels C#, en een duidelijke uitleg **waarom** elke regel belangrijk is.

## Vereisten

- .NET 6.0 of later (de code compileert op .NET Core en .NET Framework).  
- Visual Studio 2022 (of elke IDE die je wilt).  
- Een Aspose.OCR for .NET‑licentie (de gratis proefversie werkt voor testen).  
- Optioneel: een CUDA‑compatibele GPU als je de herkenning wilt versnellen.

> **Pro tip:** Als je geen GPU hebt, stel dan `UseGpu = false` in en de engine schakelt automatisch over naar CPU zonder code‑aanpassingen.

## Stap 1: Installeer de vereiste NuGet‑pakketten

Open de **Package Manager Console** en voer uit:

```powershell
Install-Package Aspose.OCR
Install-Package Aspose.OCR.Gpu
Install-Package Newtonsoft.Json
```

Deze drie pakketten geven je de OCR‑engine, GPU‑versnelling en een nette JSON‑serializer voor de vertrouwensoutput.

## Stap 2: Zet de projectstructuur op

Maak een nieuw console‑project (`dotnet new console -n AsposeOcrDemo`) en vervang de gegenereerde `Program.cs` door de code hieronder.  
Alle logica zit in de `Program`‑klasse; het enige extra type is een kleine extensiemethode die het OCR‑resultaat formatteert voor JSON.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Gpu;
using Aspose.OCR.Models;
using Newtonsoft.Json;

namespace AsposeOcrDemo
{
    class Program
    {
        // Step 1: Input image and language models
        private const string InputImagePath = @"YOUR_DIRECTORY/sample_multi_lang.jpg";
        private static readonly string[] Languages = { LanguageModel.Arabic, LanguageModel.Hindi, LanguageModel.Russian };

        // Step 2: Processing options (GPU toggle & output format)
        private const bool UseGpu = true;               // set false if no GPU
        private const string OutputFormat = "Json";     // change to "Pdf" for PDF output

        static void Main()
        {
            // Step 3: Initialise the appropriate OCR engine
            IOcrEngine engine = UseGpu ? (IOcrEngine)new GpuOcrEngine() : new OcrEngine();

            // Step 4: Run OCR – language models are auto‑downloaded if missing
            OcrResult result = engine.Recognize(
                InputImagePath,
                new OcrOptions { LanguageModels = Languages, AutoDownloadResources = true });

            // Step 5: Emit the result in the chosen format
            if (OutputFormat.Equals("json", StringComparison.OrdinalIgnoreCase))
            {
                string json = JsonConvert.SerializeObject(
                    result.GetWordsWithConfidence(),
                    Formatting.Indented);
                Console.WriteLine(json);
            }
            else if (OutputFormat.Equals("pdf", StringComparison.OrdinalIgnoreCase))
            {
                string pdfPath = Path.ChangeExtension(InputImagePath, ".pdf");
                File.WriteAllBytes(pdfPath, result.Pdf);
                Console.WriteLine($"PDF saved to: {pdfPath}");
            }
        }
    }

    // Helper that flattens OcrResult into a JSON‑friendly structure
    internal static class OcrResultExtensions
    {
        public static object GetWordsWithConfidence(this OcrResult result)
        {
            var words = new System.Collections.Generic.List<object>();
            foreach (var w in result.Words)
                words.Add(new
                {
                    Text = w.Text,
                    Confidence = w.Confidence,
                    BoundingBox = new { w.Bounds.X, w.Bounds.Y, w.Bounds.Width, w.Bounds.Height }
                });

            return new
            {
                RecognizedText = result.Text,
                LanguageModels = result.UsedLanguageModels,
                Words = words,
                ProcessingTimeMs = result.ProcessingTime.TotalMilliseconds
            };
        }
    }
}
```

### Waarom deze code werkt

1. **GPU‑schakelaar** – `GpuOcrEngine` maakt gebruik van CUDA‑kernen; de ternary‑operator maakt het omschakelen moeiteloos.  
2. **Automatisch taal‑download** – `AutoDownloadResources = true` zorgt ervoor dat de Arabische, Hindi‑ en Russische modellen bij de eerste uitvoering van de app worden opgehaald.  
3. **Vertrouwensscores** – `result.Words` bevat een `Confidence` voor elk herkend woord; de extensiemethode formatteert ze naar een nette JSON‑object.  
4. **Doorzoekbare PDF** – `result.Pdf` is al een volledig doorzoekbare PDF, dus we schrijven simpelweg de byte‑array naar schijf. Geen extra bibliotheken nodig.

## Stap 6: Voer het voorbeeld uit

Open een terminal, navigeer naar de projectmap en voer uit:

```bash
dotnet run
```

Als je **JSON**‑output hebt gekozen, zie je iets als:

```json
{
  "RecognizedText": "مرحبا Hello Привет",
  "LanguageModels": [
    "Arabic",
    "Hindi",
    "Russian"
  ],
  "Words": [
    {
      "Text": "مرحبا",
      "Confidence": 0.98,
      "BoundingBox": { "X": 45, "Y": 12, "Width": 120, "Height": 30 }
    },
    {
      "Text": "Hello",
      "Confidence": 0.99,
      "BoundingBox": { "X": 180, "Y": 12, "Width": 80, "Height": 30 }
    },
    {
      "Text": "Привет",
      "Confidence": 0.97,
      "BoundingBox": { "X": 280, "Y": 12, "Width": 110, "Height": 30 }
    }
  ],
  "ProcessingTimeMs": 312
}
```

Als je bent overgeschakeld naar **PDF**, print de console het pad en vind je een doorzoekbare PDF direct naast de bronafbeelding.

## Veelgestelde vragen & randgevallen

- **Wat als een taalmodel niet beschikbaar is?**  
  De OCR‑engine gooit een duidelijke `ResourceNotFoundException`. Omdat we `AutoDownloadResources = true` hebben ingesteld, wordt het ontbrekende model automatisch opgehaald bij de eerste uitvoering, waardoor de uitzondering zelden in productie voorkomt.

- **Kan ik een batch van afbeeldingen verwerken?**  
  Zeker. Plaats de `engine.Recognize`‑aanroep in een `foreach`‑lus over een map met bestanden. Dezelfde `OcrResultExtensions` werkt voor elke afbeelding.

- **Heb ik een licentie voor GPU nodig?**  
  Nee. De gratis proefversie werkt zowel voor CPU als GPU. Een volledige licentie verwijdert het proef‑watermerk en heft de paginalimietbeperkingen op.

- **Hoe nauwkeurig zijn de vertrouwensscores?**  
  Scores variëren van 0.0 (geen vertrouwen) tot 1.0 (volledig vertrouwen). In de praktijk is alles boven 0.90 betrouwbaar voor downstream‑verwerking; je kunt woorden met een lagere score filteren als je strengere validatie nodig hebt.

## Stap 7: Volgende stappen (Breid je OCR‑toolkit uit)

1. **Voeg meer talen toe** – voeg simpelweg `LanguageModel.French` (of elk ondersteund model) toe aan de `Languages`‑array.  
2. **Combineer OCR met PDF/A‑conversie** – Aspose.PDF kan de OCR‑laag in een PDF/A‑2b‑conform document embedden voor archivering.  
3. **Integreer met Azure Functions** – verpak de logica in een serverless‑endpoint om uploads on‑the‑fly te verwerken.  
4. **Fijn‑afstemmen van vertrouwensdrempels** – gebruik `result.Words.Where(w => w.Confidence < 0.85)` om onzekere woorden te markeren voor handmatige controle.

---

### TL;DR

Deze **c# ocr tutorial** laat je zien hoe je:

- Een afbeelding laadt en meerdere taalmodellen selecteert.  
- GPU‑versnelling inschakelt met één booleaanse vlag.  
- OCR‑resultaten **met vertrouwensscores** ophaalt en naar JSON serialiseert.  
- Optioneel een doorzoekbare PDF schrijft (**image to pdf ocr**).  

Al dit is haalbaar met slechts een handvol regels, een gratis Aspose.OCR‑proefversie, en de bovenstaande code. Probeer het, pas de talenlijst aan, en je hebt binnen enkele minuten een productie‑klare OCR‑pipeline.

---

![c# ocr tutorial example image](https://example.com/placeholder-image.jpg "c# ocr tutorial example image")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}