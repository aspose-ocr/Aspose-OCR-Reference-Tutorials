---
category: general
date: 2026-01-07
description: Tekst extraheren uit afbeelding met Aspose OCR in C#. Leer hoe je tekst
  van een foto herkent, de OCR-nauwkeurigheid verbetert, een afbeelding laadt voor
  OCR en de OCR-taal instelt.
draft: false
keywords:
- extract text from image
- recognize text from photo
- improve ocr accuracy
- load image for ocr
- set ocr language
language: nl
og_description: Tekst extraheren uit afbeelding met Aspose OCR. Deze gids laat zien
  hoe je tekst uit een foto herkent, de OCR-nauwkeurigheid verbetert, een afbeelding
  laadt voor OCR en de OCR-taal instelt.
og_title: Tekst extraheren uit afbeelding met Aspose OCR – C#‑tutorial
tags:
- Aspose OCR
- C#
- Image Processing
title: Tekst extraheren uit afbeelding met Aspose OCR – Complete C#-gids
url: /nl/net/text-recognition/extract-text-from-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tekst uit afbeelding extraheren – Volledige C#‑implementatie met Aspose OCR

Heb je ooit **tekst uit een afbeelding** moeten halen, maar wist je niet welke bibliotheek betrouwbare resultaten levert? Je bent niet de enige. In veel real‑world apps—bon‑scanners, ID‑verificaties, of gewoon een snelle notitie‑tool—is het kunnen **herkennen van tekst van een foto** een onmisbare functie.

In deze tutorial lopen we stap voor stap door een compleet, kant‑klaar voorbeeld dat laat zien hoe je **een afbeelding laadt voor OCR**, de engine **instelt op OCR‑taal**, en een paar preprocessing‑trucs toepast om **de OCR‑nauwkeurigheid te verbeteren**. Aan het einde heb je één C#‑bestand dat de geëxtraheerde tekst naar de console schrijft, en begrijp je waarom elke instelling belangrijk is.

> **Tip:** De code werkt met Aspose.OCR ≥ 23.5, .NET 6+ en elke Windows, Linux, of macOS‑omgeving die .NET Core kan uitvoeren.

## Voorwaarden

- .NET 6 SDK (of nieuwer) geïnstalleerd  
- Visual Studio 2022, VS Code, of een andere editor naar keuze  
- NuGet‑pakket `Aspose.OCR` (installeren via `dotnet add package Aspose.OCR`)  
- Een afbeeldingsbestand (JPEG/PNG) met duidelijke gedrukte of getypte tekst  

Als je dit hebt, duiken we erin.

![voorbeeld tekst uit afbeelding](/images/ocr-example.png "tekst uit afbeelding – Aspose OCR output")

## Stap 1: Maak en vernietig de OCR‑engine – “Tekst uit afbeelding extraheren” kern

Het eerste wat je nodig hebt is een instantie van `OcrEngine`. Deze in een `using`‑blok plaatsen garandeert een correcte vrijgave van native resources.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

/// <summary>
/// Demonstrates how to extract text from image using Aspose OCR.
/// </summary>
class Program
{
    static void Main()
    {
        // Step 1 – Initialize the OCR engine (the heart of the process)
        using (var ocrEngine = new OcrEngine())
        {
            // The rest of the workflow lives inside this block.
```

**Waarom dit belangrijk is:** `OcrEngine` houdt onbeheerste geheugenbronnen voor de native OCR‑DLL's. Het tijdig disposen voorkomt geheugenlekken, vooral wanneer je veel afbeeldingen in één batch verwerkt.

## Stap 2: Definieer herkenningsinstellingen – Verbeter OCR‑nauwkeurigheid

Vervolgens maken we een `RecognitionSettings`‑object aan. Hier **stel je de OCR‑taal in** en voeg je preprocessing‑filters toe die vaak het verschil maken tussen een onsamenhangende string en nette output.

```csharp
            // Step 2 – Configure recognition settings
            var recognitionSettings = new RecognitionSettings
            {
                // Set the language to English; other languages are available via Language enum.
                Language = Language.English,

                // PreprocessFilters help the engine deal with real‑world photo issues.
                PreprocessFilters = new[]
                {
                    PreprocessFilter.Deskew,          // Corrects slight rotation
                    PreprocessFilter.Denoise,         // Reduces grainy noise
                    PreprocessFilter.ContrastEnhance // Boosts text visibility
                }
            };
```

**Waarom deze filters?**  
- **Deskew** lost het veelvoorkomende probleem op dat een foto van een telefoon een paar graden scheef staat.  
- **Denoise** verwijdert vlekjes die als tekens kunnen worden geïnterpreteerd.  
- **ContrastEnhance** laat vage inkt opvallen, wat essentieel is voor **het verbeteren van OCR‑nauwkeurigheid**.

## Stap 3: Laad de afbeelding – Laad afbeelding efficiënt voor OCR

Aspose biedt `ImageStream.FromFile` voor snel laden. Je kunt ook een `MemoryStream` gebruiken als de afbeelding afkomstig is van een web‑request of een database.

```csharp
            // Step 3 – Load the image you want to analyze
            var imagePath = @"YOUR_DIRECTORY/phone_photo.jpg";
            var imageStream = ImageStream.FromFile(imagePath);
```

**Veelvoorkomende valkuil:** Een pad met schuine strepen (`/`) werkt op Windows, maar `Path.Combine` gebruiken is veiliger voor cross‑platform projecten.

## Stap 4: Voer de herkenning uit – Herken tekst van foto

Nu roepen we `Recognize` aan, waarbij we zowel de afbeelding‑stream als onze instellingen doorgeven. De methode retourneert een gewone string met de geëxtraheerde tekst.

```csharp
            // Step 4 – Run OCR and capture the result
            string recognizedText = ocrEngine.Recognize(imageStream, recognitionSettings);
```

Bevat de afbeelding meerdere tekstblokken, dan concateneert Aspose ze met regeleinden, zodat de oorspronkelijke lay‑out zoveel mogelijk behouden blijft.

## Stap 5: Geef het resultaat weer – Controleer extractie

Tot slot schrijven we het resultaat naar de console. In een echte applicatie sla je het misschien op in een database, stuur je het naar een andere service, of toon je het in een UI.

```csharp
            // Step 5 – Show the extracted text
            Console.WriteLine("=== Extracted Text Start ===");
            Console.WriteLine(recognizedText);
            Console.WriteLine("=== Extracted Text End ===");
        } // End of using block – OcrEngine disposed
    }
}
```

### Verwachte console‑output

```
=== Extracted Text Start ===
This is a sample receipt.
Total: $23.45
Thank you for shopping!
=== Extracted Text End ===
```

Zie je onsamenhangende tekens, controleer dan of de afbeelding duidelijk is, de taal overeenkomt met de tekst, en de preprocessing‑filters passend zijn.

## Stap 6: Optionele aanpassingen – Fijn afstellen voor randgevallen

### a. Talen wisselen

```csharp
recognitionSettings.Language = Language.Spanish; // For Spanish receipts
```

### b. Aangepaste filters toevoegen

Aspose biedt ook `PreprocessFilter.Sharpen` of `PreprocessFilter.Binarize`. Experimenteer hiermee wanneer de standaard drie niet volstaan.

### c. Grote afbeeldingen verwerken

Voor zeer hoge resolutie‑foto's kun je eerst verkleinen om het geheugenverbruik laag te houden:

```csharp
var resizedStream = ImageProcessor.Resize(imageStream, 1024, 768);
string text = ocrEngine.Recognize(resizedStream, recognitionSettings);
```

## Veelgestelde vragen

**Q: Werkt dit met handgeschreven notities?**  
A: Aspose OCR is afgestemd op gedrukte tekst. Handgeschreven herkenning vereist een andere engine (bijv. Aspose.OCR for Handwriting of een machine‑learning‑model).

**Q: Kan ik meerdere afbeeldingen in een lus verwerken?**  
A: Zeker. Plaats gewoon het `using (var ocrEngine = new OcrEngine())`‑blok buiten de lus en hergebruik de engine voor betere prestaties.

**Q: Wat als de afbeelding een PDF‑pagina is?**  
A: Converteer de PDF‑pagina eerst naar een afbeelding (Aspose.PDF kan pagina’s renderen als PNG/JPEG), en geef die vervolgens aan de OCR‑engine.

## Samenvatting – Wat we hebben bereikt

- **Tekst uit afbeelding geëxtraheerd** met een enkel, zelf‑voorzienend C#‑programma.  
- Gedemonstreerd hoe je **tekst van een foto herkent** met preprocessing die **OCR‑nauwkeurigheid verbetert**.  
- De juiste manier laten zien om **afbeelding te laden voor OCR** en **OCR‑taal in te stellen** voor meertalige scenario’s.  

## Volgende stappen & gerelateerde onderwerpen

- **Batchverwerking:** Combineer dit fragment met `Directory.GetFiles` om een volledige map te OCR‑en.  
- **Post‑processing:** Gebruik reguliere expressies om data, bedragen of ID’s op te schonen na extractie.  
- **Integraties:** Stuur de geëxtraheerde tekst naar Azure Cognitive Search of Elastic voor doorzoekbare documenten.  

Voel je vrij om te experimenteren met verschillende filtercombinaties, talen en afbeeldingsbronnen. Het kernpatroon blijft hetzelfde: maak de engine, configureer instellingen, laad de afbeelding, herken, en geef het resultaat weer. Veel programmeerplezier!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}