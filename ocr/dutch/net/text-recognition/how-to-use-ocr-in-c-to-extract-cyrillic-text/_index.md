---
category: general
date: 2026-09-10
description: Hoe OCR in C# te gebruiken om Cyrillische tekst te extraheren, afbeeldingen
  voor te bewerken en ze om te zetten naar PDF- of HTML-bestanden in één uitvoerbaar
  voorbeeld.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use OCR
- preprocess image for OCR
- convert image to PDF
- convert image to HTML
- extract Cyrillic text
language: nl
lastmod: 2026-09-10
og_description: Hoe OCR in C# te gebruiken om Cyrillische tekst te extraheren, afbeeldingen
  voor te verwerken en de resultaten te exporteren als PDF of HTML. Volg deze stapsgewijze
  handleiding.
og_image_alt: Diagram illustrating how to use OCR to extract Cyrillic text and convert
  images
og_title: Hoe OCR te gebruiken in C# – Cyrillische tekst extraheren en afbeeldingen
  converteren
schemas:
- author: Aspose
  dateModified: '2026-09-10'
  description: How to use OCR in C# to extract Cyrillic text, preprocess images, and
    convert them to PDF or HTML files in a single, runnable example.
  headline: How to use OCR in C# to extract Cyrillic text
  type: TechArticle
tags:
- OCR
- C#
- Cyrillic
- Image processing
- PDF conversion
title: Hoe OCR in C# te gebruiken om Cyrillische tekst te extraheren
url: /nl/net/text-recognition/how-to-use-ocr-in-c-to-extract-cyrillic-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe OCR te gebruiken in C# om Cyrillische tekst te extraheren

Als je **how to use OCR** in C# nodig hebt om Cyrillische tekst uit gescande documenten te extraheren, laat deze gids je een complete, kant‑klaar oplossing zien. Je leert ook hoe je **preprocess image for OCR** kunt doen, en hoe je **convert image to PDF** of **convert image to HTML** kunt uitvoeren zodra de tekst is herkend.

Documentdigitaliseringsprojecten lopen vaak tegen twee problemen aan: scans van lage kwaliteit en de noodzaak om resultaten in meerdere formaten op te slaan. Deze tutorial lost beide op door gebruik te maken van de Aspose.OCR‑bibliotheek, die automatisch ontbrekende taalpakketten downloadt, ingebouwde beeldverwerkings‑helpers biedt, en het OCR‑resultaat met één oproep kan exporteren naar PDF of HTML.

## Vereisten

* .NET 6.0 SDK of later (de code werkt ook met .NET Framework 4.7+).
* Visual Studio 2022 of een editor die C#‑projecten ondersteunt.
* Het **Aspose.OCR** NuGet‑pakket. Installeer het met:

```bash
dotnet add package Aspose.OCR
```

* Een afbeeldingsbestand dat Cyrillische tekens bevat (bijv. `sample_cyrillic.jpg`).  
  Plaats het bestand in een map die je kunt refereren als `YOUR_DIRECTORY`.

De bibliotheek downloadt het Cyrillische taalpakket de eerste keer dat je `ocrEngine.Language = Language.Cyrillic;` instelt, dus handmatig downloaden is niet nodig.

## Stap 1 – Initialiseer de OCR‑engine (how to use OCR)

Het maken van een `OcrEngine`‑instance bereidt de engine voor alle volgende bewerkingen voor.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;

class Program
{
    static void Main()
    {
        // Initialize the OCR engine – the first step in how to use OCR with Aspose
        var ocrEngine = new OcrEngine();
```

**Waarom dit belangrijk is:** De engine bevat configuratie zoals taal, beeldverwerkingsinstellingen en uitvoeropties. Eenmalig initialiseren houdt de rest van de code schoon en thread‑safe.

## Stap 2 – Kies de Cyrillische taal (extract Cyrillic text)

```csharp
        // Select Cyrillic language; the pack is fetched automatically if missing
        ocrEngine.Language = Language.Cyrillic;
```

**Waarom dit belangrijk is:** De OCR‑nauwkeurigheid hangt sterk af van het juiste taalmodel. Door expliciet `Language.Cyrillic` te selecteren, past de engine teken‑frequentietabellen toe die geschikt zijn voor Russisch, Oekraïens, Bulgaars, enz.

## Stap 3 – Preprocess the image for OCR

Scans van lage kwaliteit bevatten scheefstand, vlekjes of ongelijke belichting. De ingebouwde `ImageProcessor` kan de herkenningspercentages verbeteren met slechts twee aanroepen.

```csharp
        // Optional but strongly recommended: deskew and despeckle the image
        ocrEngine.ImageProcessor.Deskew();      // Aligns rotated text
        ocrEngine.ImageProcessor.Despeckle();  // Removes isolated noise pixels
```

**Waarom dit belangrijk is:** Pre‑processing vermindert foutieve tekens en verhoogt de vertrouwensscore. Scheve tekst levert vaak onsamenhangende output op; deskewing maakt het recht. Despeckling verwijdert kleine artefacten die de OCR‑engine anders als letters zou kunnen interpreteren.

> **Pro tip:** Als je bronafbeeldingen al schoon zijn, kun je deze aanroepen overslaan. Voor sterk verslechterde scans, overweeg extra stappen zoals `Binarize()` of `ContrastStretch()`.

## Stap 4 – Voer OCR uit op de invoerafbeelding

```csharp
        // The image path can be absolute or relative to the executable
        string inputPath = Path.Combine("YOUR_DIRECTORY", "sample_cyrillic.jpg");
        ocrEngine.Process(inputPath);
```

**Waarom dit belangrijk is:** `Process` voert de herkenningspipeline uit op de meegegeven bitmap. Het retourneert `void`; de herkende tekst wordt beschikbaar via de `Text`‑eigenschap.

## Stap 5 – Haal de herkende tekst op en sla deze op in een bestand

```csharp
        // Access the recognized string
        string recognizedText = ocrEngine.Text;

        // Save the plain‑text result
        string txtOutput = Path.Combine("YOUR_DIRECTORY", "result.txt");
        File.WriteAllText(txtOutput, recognizedText);
        Console.WriteLine("Text saved to: " + txtOutput);
```

**Waarom dit belangrijk is:** Het opslaan van de ruwe tekst maakt downstream verwerking mogelijk, zoals zoeken, indexeren of invoeren in vertaaldiensten.

## Stap 6 – Exporteer het OCR‑resultaat naar andere formaten (convert image to PDF & convert image to HTML)

```csharp
        // Export as PDF – useful for archival or sharing with non‑technical users
        string pdfOutput = Path.Combine("YOUR_DIRECTORY", "result.pdf");
        ocrEngine.SaveResultAsPdf(pdfOutput);
        Console.WriteLine("PDF saved to: " + pdfOutput);

        // Export as HTML – retains basic layout and can be displayed in browsers
        string htmlOutput = Path.Combine("YOUR_DIRECTORY", "result.html");
        ocrEngine.SaveResultAsHtml(htmlOutput);
        Console.WriteLine("HTML saved to: " + htmlOutput);
    }
}
```

**Waarom dit belangrijk is:** Het converteren van het OCR‑resultaat naar PDF of HTML laat je de visuele context van de originele afbeelding behouden terwijl je doorzoekbare tekst biedt. Dit is vooral waardevol voor juridische of archiveringsprocessen.

### Verwachte output

Het uitvoeren van het programma met een duidelijke Cyrillische scan produceert drie bestanden:

* `result.txt` – platte Unicode‑tekst, bijv. `Пример текста на кириллице`.
* `result.pdf` – een PDF die de afbeelding bevat met een onzichtbare tekstlaag voor zoeken.
* `result.html` – een HTML‑pagina die de afbeelding en selecteerbare tekst toont.

Open een van de bestanden om te verifiëren dat de Cyrillische tekens correct zijn geëxtraheerd.

## Veelgestelde vragen en randgevallen

| Vraag | Antwoord |
|----------|--------|
| **Wat als het taalpakket niet kan worden gedownload?** | Zorg ervoor dat de machine internettoegang heeft. Je kunt het pakket ook vooraf downloaden van de site van Aspose en plaatsen in de `bin`‑map. |
| **Kan ik andere alfabetten in dezelfde run herkennen?** | Ja. Roep `ocrEngine.Language = Language.English;` (of een andere ondersteunde enum) aan vóór `Process`. Mogelijk moet je `Process` apart uitvoeren voor elke taal als de afbeelding verschillende scripts bevat. |
| **Mijn afbeelding is een multi‑page TIFF – werkt dit?** | `OcrEngine` verwerkt één bitmap per keer. Laad elke pagina in een `Bitmap` en roep `Process` in een lus aan, waarbij je de resultaten samenvoegt. |
| **Hoe verhoog ik de prestaties voor grote batches?** | Herbruik een enkele `OcrEngine`‑instance en stel `ocrEngine.OptimizeMemory = true;` in. Overweeg ook parallelle verwerking met afzonderlijke engine‑instances per thread. |

## Conclusie

Je weet nu **how to use OCR** in C# om **extract Cyrillic text**, **preprocess image for OCR**, en **convert image to PDF** of **convert image to HTML** uit te voeren in een paar beknopte stappen. Het volledige voorbeeld toont een productie‑

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Hoe AspOCR te gebruiken: Preprocess Image OCR Filters voor .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Hoe OCR‑tekst te extraheren in C# – Complete stap‑voor‑stap gids](/ocr/english/net/text-recognition/how-to-extract-ocr-text-in-c-complete-step-by-step-guide/)
- [Hoe Aspose OCR te gebruiken voor JSON‑resultaat in beeldherkenning](/ocr/english/net/text-recognition/get-result-as-json/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}