---
category: general
date: 2026-11-26
description: Leer hoe je OCR uitvoert op PNG‑bestanden, PNG naar tekst converteert
  en Cyrillische tekst extraheert met Aspose.OCR – stapsgewijze gids voor ontwikkelaars.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to perform OCR
- convert PNG to text
- recognize text from PNG
- extract Cyrillic text
- load image for OCR
language: nl
lastmod: 2026-11-26
og_description: Hoe OCR uit te voeren op PNG‑bestanden en Cyrillische tekst te extraheren
  met Aspose.OCR in C#. Volg deze volledige tutorial om PNG naar tekst te converteren.
og_image_alt: how to perform OCR on a PNG image using Aspose.OCR
og_title: Hoe OCR uit te voeren op PNG-afbeeldingen met Aspose.OCR – C#-handleiding
schemas:
- author: Aspose
  dateModified: '2026-11-26'
  description: Learn how to perform OCR on PNG files, convert PNG to text, and extract
    Cyrillic text using Aspose.OCR – step‑by‑step guide for developers.
  headline: How to perform OCR on PNG images with Aspose.OCR in C#
  type: TechArticle
- description: Learn how to perform OCR on PNG files, convert PNG to text, and extract
    Cyrillic text using Aspose.OCR – step‑by‑step guide for developers.
  name: How to perform OCR on PNG images with Aspose.OCR in C#
  steps:
  - name: Handling large images
    text: 'If the PNG is larger than 2 MB, consider down‑scaling it before recognition
      to speed up processing:'
  - name: 'Edge case: Missing language module'
    text: 'If the download fails (e.g., offline environment), the engine throws an
      `OcrException`. Catch it to provide a graceful fallback:'
  - name: Expected output
    text: 'If `sample_image.png` contains the Cyrillic phrase “Привет мир”, the console
      will display:'
  - name: How it works
    text: 1. **Engine creation** – prepares the OCR pipeline. 2. **Image loading**
      – supports both raw PNG and down‑scaled versions for performance. 3. **Language
      selection** – demonstrates **extract Cyrillic text** while handling missing
      modules. 4. **Recognition** – the core **recognize text from PNG** call
  type: HowTo
tags:
- OCR
- C#
- Aspose.OCR
title: Hoe OCR uit te voeren op PNG-afbeeldingen met Aspose.OCR in C#
url: /nl/net/text-recognition/how-to-perform-ocr-on-png-images-with-aspose-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe OCR uit te voeren op PNG‑afbeeldingen met Aspose.OCR in C#

Als je **hoe OCR uit te voeren** op een PNG‑bestand moet uitvoeren, laat deze gids je de exacte stappen zien om PNG naar tekst te converteren met Aspose.OCR. Of je nu Cyrillische tekst uit gescande documenten haalt of simpelweg tekst van PNG‑schermafbeeldingen herkent, de oplossing werkt direct uit de doos en vereist slechts een paar regels C#‑code.

In deze tutorial leer je hoe je:

* **load image for OCR** van een lokale map,
* de engine configureert om **extract Cyrillic text**,
* **recognize text from PNG** en een schone string verkrijgt,
* veelvoorkomende valkuilen aanpakt zoals ontbrekende taalmodule en grote afbeeldingen.

Ervaring met Aspose.OCR is niet vereist—alleen een .NET‑ontwikkelomgeving en een PNG‑afbeelding die je wilt verwerken.

## Vereisten

* .NET 6.0 (of later) geïnstalleerd.
* Een gelicentieerde of proefkopie van **Aspose.OCR for .NET**. Je kunt een gratis proefversie krijgen op de Aspose‑website.
* Visual Studio 2022 (of een IDE die .NET ondersteunt).
* Een PNG‑bestand dat de tekst bevat die je wilt extraheren (het voorbeeld gebruikt `sample_image.png`).

## Stap 1: Installeer het Aspose.OCR NuGet‑pakket

Open een terminal in je projectmap en voer uit:

```bash
dotnet add package Aspose.OCR
```

Het pakket bevat de kern‑OCR‑engine en alle taalmodule­s. Wanneer je een taal aanvraagt die lokaal niet aanwezig is, downloadt Aspose.OCR automatisch de benodigde module.

## Stap 2: Maak een OCR‑engine‑instantie (how to perform OCR)

De eerste concrete stap in elke OCR‑workflow is het instantieren van de engine. Dit object beheert alle volgende bewerkingen, zoals het laden van de afbeelding en het uitvoeren van herkenning.

```csharp
using Aspose.OCR;

// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();
```

**Waarom dit belangrijk is:** De `OcrEngine`‑klasse omsluit de OCR‑pipeline. Het maken van één instantie en deze hergebruiken voor meerdere afbeeldingen vermindert het geheugenverbruik en verbetert de prestaties.

## Stap 3: Laad afbeelding voor OCR – specificeer het bron‑PNG‑bestand

Het laden van de afbeelding is het punt waarop je **load image for OCR**. Aspose.OCR accepteert verschillende invoertypen; de meest eenvoudige is `ImageStream.FromFile`.

```csharp
// Load the PNG image from disk
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/sample_image.png");
```

> **Pro tip:** Gebruik een absoluut pad of `Path.Combine` om runtime‑fouten op verschillende omgevingen te voorkomen.

### Grote afbeeldingen verwerken

Als de PNG groter is dan 2 MB, overweeg dan om deze vóór herkenning te verkleinen om de verwerking te versnellen:

```csharp
using System.Drawing;

// Downscale large images to a maximum width of 1200 pixels
Bitmap original = new Bitmap(@"YOUR_DIRECTORY/sample_image.png");
int maxWidth = 1200;
int newHeight = (int)(original.Height * (maxWidth / (double)original.Width));
Bitmap resized = new Bitmap(original, new Size(maxWidth, newHeight));

using (var ms = new MemoryStream())
{
    resized.Save(ms, System.Drawing.Imaging.ImageFormat.Png);
    ocrEngine.Image = ImageStream.FromStream(ms);
}
```

## Stap 4: Configureer taal – extract Cyrillic text

Standaard gaat Aspose.OCR uit van Engels. Om **extract Cyrillic text** te doen, stel je de `Language`‑eigenschap in op `Language.Cyrillic`. De benodigde module wordt automatisch gedownload bij de eerste uitvoering van de code.

```csharp
// Set the OCR language to Cyrillic
ocrEngine.Language = Language.Cyrillic;
```

Als je meerdere talen moet herkennen (bijv. Engels en Cyrillisch), kun je ze combineren:

```csharp
ocrEngine.Language = Language.English | Language.Cyrillic;
```

### Randgeval: Ontbrekende taalmodule

Als de download mislukt (bijv. offline omgeving), gooit de engine een `OcrException`. Vang deze op om een elegante fallback te bieden:

```csharp
try
{
    ocrEngine.Language = Language.Cyrillic;
}
catch (OcrException ex)
{
    Console.WriteLine($"Language module could not be loaded: {ex.Message}");
    // Optionally, fall back to English or abort the process
}
```

## Stap 5: Voer de herkenningsoperatie uit (recognize text from PNG)

Nu de afbeelding en taal zijn ingesteld, kun je **recognize text from PNG**. De `Recognize`‑methode voert de OCR‑pipeline synchroon uit.

```csharp
// Run OCR
ocrEngine.Recognize();
```

**Waarom het werkt:** Intern past Aspose.OCR voorverwerking toe (binarisatie, ruisverwijdering) voordat de afbeelding wordt gevoed aan een op neurale netwerken gebaseerde herkenner die is afgestemd op de geselecteerde taal.

## Stap 6: Haal de herkende tekst op en toon deze (convert PNG to text)

Na herkenning is de geëxtraheerde string beschikbaar via de `Text`‑eigenschap. Dit is de laatste stap in **convert PNG to text**.

```csharp
// Get the recognized text
string recognizedText = ocrEngine.Text;

// Output the result
Console.WriteLine("=== OCR Result ===");
Console.WriteLine(recognizedText);
```

### Verwachte output

Als `sample_image.png` de Cyrillische zin “Привет мир” bevat, zal de console het volgende weergeven:

```
=== OCR Result ===
Привет мир
```

De output kan precies zoals in de afbeelding regelafbrekingen en interpunctie bevatten. Je kunt de string nabewerken met `String.Trim()`, `Regex` of andere tekst‑opschoon‑hulpmiddelen indien nodig.

## Stap 7: Optioneel – Sla het resultaat op in een bestand

Het opslaan van het OCR‑resultaat maakt downstream‑verwerking mogelijk (bijv. indexeren, vertalen). Hier is een snelle manier om de tekst naar een UTF‑8‑bestand te schrijven:

```csharp
File.WriteAllText(@"YOUR_DIRECTORY/ocr_output.txt", recognizedText, Encoding.UTF8);
Console.WriteLine("OCR text saved to ocr_output.txt");
```

## Veelvoorkomende valkuilen en hoe ze te vermijden

| Probleem | Symptoom | Oplossing |
|----------|----------|-----------|
| **Missing language module** | `OcrException` bij `Language = Language.Cyrillic` | Zorg voor internetconnectiviteit bij de eerste uitvoering of download modules vooraf via Aspose’s offline‑pakket. |
| **Blurry or low‑contrast image** | Slechte nauwkeurigheid, veel “?”‑tekens | Pre‑process de afbeelding: verhoog contrast, pas verscherping toe, of converteer naar grijstinten voordat je deze aan de engine geeft. |
| **Very large PNG** | Lange verwerkingstijd, mogelijke `OutOfMemoryException` | Verklein zoals getoond in Stap 3, of splits een meer‑pagina afbeelding in afzonderlijke tegels. |
| **Non‑UTF‑8 characters** | Vervormde output | Controleer of de console of bestandswriter UTF‑8‑codering gebruikt (`Encoding.UTF8`). |

## Volledig, uitvoerbaar voorbeeld

Hieronder staat het complete programma dat alle bovenstaande stappen combineert. Kopieer het naar een nieuw console‑project en voer het uit nadat je de bestands‑paden hebt aangepast.

```csharp
using System;
using System.Drawing;
using System.IO;
using System.Text;
using Aspose.OCR;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1. Create OCR engine
            OcrEngine ocrEngine = new OcrEngine();

            // 2. Load PNG image (with optional down‑scaling for large files)
            string imagePath = @"YOUR_DIRECTORY/sample_image.png";
            Bitmap original = new Bitmap(imagePath);
            const int maxWidth = 1200;

            if (original.Width > maxWidth)
            {
                int newHeight = (int)(original.Height * (maxWidth / (double)original.Width));
                Bitmap resized = new Bitmap(original, new Size(maxWidth, newHeight));

                using (var ms = new MemoryStream())
                {
                    resized.Save(ms, System.Drawing.Imaging.ImageFormat.Png);
                    ocrEngine.Image = ImageStream.FromStream(ms);
                }
            }
            else
            {
                ocrEngine.Image = ImageStream.FromFile(imagePath);
            }

            // 3. Set language to Cyrillic (fallback to English if needed)
            try
            {
                ocrEngine.Language = Language.Cyrillic;
            }
            catch (OcrException ex)
            {
                Console.WriteLine($"Failed to load Cyrillic module: {ex.Message}");
                Console.WriteLine("Falling back to English.");
                ocrEngine.Language = Language.English;
            }

            // 4. Recognize text
            ocrEngine.Recognize();

            // 5. Retrieve and display the text (convert PNG to text)
            string recognizedText = ocrEngine.Text;
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(recognizedText);

            // 6. Save result to a UTF‑8 file
            string outputPath = @"YOUR_DIRECTORY/ocr_output.txt";
            File.WriteAllText(outputPath, recognizedText, Encoding.UTF8);
            Console.WriteLine($"OCR text saved to {outputPath}");
        }
    }
}
```

### Hoe het werkt

1. **Engine creation** – bereidt de OCR‑pipeline voor.  
2. **Image loading** – ondersteunt zowel ruwe PNG‑ als down‑scaled versies voor prestaties.  
3. **Language selection** – toont **extract Cyrillic text** terwijl ontbrekende modules worden afgehandeld.  
4. **Recognition** – de kern **recognize text from PNG** oproep.  
5. **Result handling** – toont **convert PNG to text** en schrijft de output naar een bestand.

Voer het programma uit met `dotnet run`. Als alles correct is ingesteld, zie je de herkende tekst in de console en opgeslagen in `ocr_output.txt`.

## Conclusie

In deze tutorial heb je **hoe OCR uit te voeren** op PNG‑bestanden geleerd met Aspose.OCR voor .NET, van **load image for OCR** tot **extract Cyrillic text** en **convert PNG to text**. Het volledige, uitvoerbare voorbeeld toont de standaard workflow, veelvoorkomende randgevallen en praktische tips die je OCR‑pipeline betrouwbaar houden.

**Next steps**

* Verken **recognize text from PNG** met extra talen (Arabisch, Chinees) door `Language`‑vlaggen te combineren.  
* Integreer het OCR‑resultaat met Azure Cognitive Search voor doorzoekbare documentarchieven.  
* Experimenteer met de instellingen van Aspose.OCR’s `OcrEngine` zoals `Resolution`

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Hoe Aspose.OCR‑model te downloaden en tekst uit PNG te extraheren in C#](/ocr/english/net/text-recognition/how-to-download-ocr-model-and-extract-text-from-png-using-as/)
- [Hoe OCR uit te voeren in C# – Cyrillische tekst herkennen met Aspose](/ocr/english/net/text-recognition/how-to-perform-ocr-in-c-recognize-cyrillic-text-with-aspose/)
- [Hoe batch‑OCR in C# – Snelle manier om tekst uit PNG‑bestanden te extraheren](/ocr/english/net/ocr-optimization/how-to-batch-ocr-in-c-fast-way-to-extract-text-png-files/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}