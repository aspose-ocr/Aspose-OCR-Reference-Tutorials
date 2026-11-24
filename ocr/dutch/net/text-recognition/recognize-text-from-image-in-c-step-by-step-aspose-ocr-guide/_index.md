---
category: general
date: 2026-08-12
description: Herken tekst uit een afbeelding met Aspose OCR voor C#. Leer hoe je tekst
  uit een PNG kunt extraheren, een afbeelding naar tekst kunt converteren en Cyrillische
  tekst kunt verwerken.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- recognize text from image
- extract text from png
- convert image to text
- c# image ocr
- aspose ocr c#
language: nl
lastmod: 2026-08-12
og_description: herken tekst van afbeelding met Aspose OCR in C#. Deze gids laat zien
  hoe je tekst uit PNG kunt extraheren, afbeelding naar tekst kunt converteren en
  met de Cyrillische taal kunt werken.
og_image_alt: Diagram showing the OCR processing flow from image file to recognized
  text output
og_title: tekst herkennen uit afbeelding in C# – volledige Aspose OCR‑tutorial
schemas:
- author: Aspose
  dateModified: '2026-08-12'
  description: recognize text from image using Aspose OCR for C#. Learn how to extract
    text from PNG, convert image to text, and handle Cyrillic language.
  headline: recognize text from image in C# – step‑by‑step Aspose OCR guide
  type: TechArticle
- description: recognize text from image using Aspose OCR for C#. Learn how to extract
    text from PNG, convert image to text, and handle Cyrillic language.
  name: recognize text from image in C# – step‑by‑step Aspose OCR guide
  steps:
  - name: Expected console output
    text: '``` === Recognized Text === Привет мир! Это пример текста на кириллице.
      ```'
  - name: Recognize text from JPEG or BMP
    text: Replace the PNG file path with a JPEG or BMP file; the same `engine.Image`
      assignment works because Aspose.OCR auto‑detects the format.
  - name: Extract text from multiple pages
    text: 'If you need to **extract text from png** files that represent scanned pages,
      loop over the file list and concatenate the results:'
  - name: Convert image to text in an ASP.NET API
    text: 'Expose the OCR logic through a controller action:'
  type: HowTo
tags:
- Aspose OCR
- C#
- OCR
- Image processing
title: tekst herkennen uit afbeelding in C# – stapsgewijze Aspose OCR‑gids
url: /nl/net/text-recognition/recognize-text-from-image-in-c-step-by-step-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# tekst herkennen van afbeelding in C# – stap‑voor‑stap Aspose OCR gids

Als je **tekst uit een afbeelding wilt herkennen** in een .NET‑applicatie, biedt deze tutorial een complete, kant‑klaar oplossing. Je ziet hoe je tekst uit PNG‑bestanden kunt extraheren, afbeelding naar tekst kunt converteren en Cyrillische tekens kunt verwerken – allemaal met de Aspose.OCR‑bibliotheek voor C#.

De gids behandelt alles wat je nodig hebt om vandaag nog OCR te gebruiken: vereiste NuGet‑pakketten, taalconfiguratie, het laden van afbeeldingen en foutafhandeling. Aan het einde heb je een console‑programma dat de herkende string naar de console print, en begrijp je hoe je de code kunt aanpassen voor andere afbeeldingsformaten of talen.

## Vereisten

- .NET 6 SDK of later (de code werkt ook met .NET Framework 4.7.2)
- Visual Studio 2022 of een andere C#‑editor naar keuze
- Internettoegang de eerste keer dat je het programma uitvoert (Aspose.OCR downloadt taalmodules automatisch)
- Een PNG‑afbeelding die leesbare tekst bevat (het voorbeeld gebruikt *cyrillic_sample.png*)

> **Pro tip:** Houd je PNG‑bestanden onder de 2 MB voor snellere verwerking. Grotere afbeeldingen kunnen vóór OCR worden verkleind om de nauwkeurigheid te verbeteren.

## Stap 1: Installeer het Aspose.OCR NuGet‑pakket

Open een terminal in je projectmap en voer uit:

```bash
dotnet add package Aspose.OCR
```

Het pakket bevat de kern‑OCR‑engine en de standaardtaalmodules. Wanneer je een taal aanvraagt die lokaal niet aanwezig is, downloadt Aspose deze automatisch.

## Stap 2: Maak de OCR‑engine en selecteer de taal

De OCR‑engine is het centrale object dat de conversie van afbeelding naar tekst uitvoert. Voor Cyrillische tekst stel je de eigenschap `Language` in op `Language.Cyrillic`. Dezelfde eigenschap werkt voor andere talen, zoals `Language.English`.

```csharp
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // Step 2.1: Instantiate the OCR engine
        OcrEngine engine = new OcrEngine();

        // Step 2.2: Choose the language module – Cyrillic in this example
        engine.Language = Language.Cyrillic;
```

**Waarom dit belangrijk is:** Het selecteren van de juiste taal verbetert de tekenherkenning omdat de engine taalspecifieke woordenboeken en lettertypen laadt. Als je deze stap overslaat, valt de engine terug op Engels en worden Cyrillische tekens onleesbaar.

## Stap 3: Laad de afbeelding die je wilt verwerken

Aspose.OCR ondersteunt veel afbeeldingsformaten, maar PNG is een veelgebruikt lossless‑formaat dat tekstranden behoudt. Gebruik `ImageStream.FromFile` om het bestand in de engine te lezen.

```csharp
        // Step 3: Load the PNG image that contains the text
        engine.Image = ImageStream.FromFile("YOUR_DIRECTORY/cyrillic_sample.png");
```

Vervang `YOUR_DIRECTORY` door het daadwerkelijke pad naar je PNG‑bestand. Als je **tekst uit png‑bestanden** wilt extraheren die zich in een andere map bevinden, pas dan eenvoudigweg het pad aan.

## Stap 4: Voer de OCR‑bewerking uit

Het aanroepen van `engine.Recognize()` start de OCR‑pipeline en retourneert een eenvoudige string. Dit is de kern van de **afbeelding naar tekst converteren** functionaliteit.

```csharp
        // Step 4: Run OCR and get the recognized string
        string recognizedText = engine.Recognize();
```

De methode gooit een uitzondering als de afbeelding niet kan worden geladen of als de taalmodule niet kan worden gedownload. Omring de aanroep met een try‑catch‑blok voor productiecodelogica.

## Stap 5: Toon of sla de herkende output op

Voor een snelle demo kun je het resultaat naar de console schrijven. In echte toepassingen sla je het misschien op in een database, een tekstbestand, of geef je het door aan een andere service.

```csharp
        // Step 5: Output the recognized text
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(recognizedText);
    }
}
```

### Verwachte console‑output

```
=== Recognized Text ===
Привет мир! Это пример текста на кириллице.
```

Als de afbeelding Engelse tekst bevat, zal de output de overeenkomstige Engelse zin zijn. dezelfde code werkt voor **c# image ocr**‑taken in meerdere talen.

## Volledige broncode – klaar om te kopiëren

Hieronder staat het volledige programma, inclusief de `using`‑directive en alle stappen in één bestand. Kopieer het naar `Program.cs` en voer `dotnet run` uit.

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        try
        {
            // Create an OCR engine instance
            OcrEngine engine = new OcrEngine();

            // Select the Cyrillic language module (downloaded automatically if missing)
            engine.Language = Language.Cyrillic;

            // Load the image that contains Cyrillic text
            engine.Image = ImageStream.FromFile("YOUR_DIRECTORY/cyrillic_sample.png");

            // Perform the OCR recognition
            string recognizedText = engine.Recognize();

            // Display the recognized text
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(recognizedText);
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"OCR failed: {ex.Message}");
        }
    }
}
```

## Veelvoorkomende variaties afhandelen

### Tekst herkennen van JPEG of BMP

Vervang het PNG‑pad door een JPEG‑ of BMP‑bestand; dezelfde `engine.Image`‑toewijzing werkt omdat Aspose.OCR het formaat automatisch detecteert.

```csharp
engine.Image = ImageStream.FromFile("photo.jpg");
```

### Tekst extraheren van meerdere pagina’s

Als je **tekst uit png‑bestanden** wilt extraheren die gescande pagina’s voorstellen, doorloop dan de bestandslijst en concateneer de resultaten:

```csharp
string[] files = Directory.GetFiles("scans", "*.png");
var allText = new StringBuilder();

foreach (var file in files)
{
    engine.Image = ImageStream.FromFile(file);
    allText.AppendLine(engine.Recognize());
}
Console.WriteLine(allText.ToString());
```

### Afbeelding naar tekst converteren in een ASP.NET API

Expose de OCR‑logica via een controller‑actie:

```csharp
[HttpPost("api/ocr")]
public async Task<IActionResult> Ocr(IFormFile image)
{
    using var stream = image.OpenReadStream();
    OcrEngine engine = new OcrEngine { Language = Language.English };
    engine.Image = ImageStream.FromStream(stream);
    string text = engine.Recognize();
    return Ok(new { text });
}
```

Dit demonstreert **c# image ocr** binnen een webservice, waardoor clients elke rasterafbeelding kunnen uploaden en de geëxtraheerde tekst als JSON ontvangen.

## Prestatietips en randgevallen

- **Afbeeldingskwaliteit:** OCR‑nauwkeurigheid daalt sterk wanneer de afbeelding onscherp is of een laag contrast heeft. Gebruik beeldvoorbewerking (bijv. verscherpen, binariseren) vóór je het aan de engine geeft.
- **Grote bestanden:** Voor afbeeldingen groter dan 5 MP, verklein ze tot maximaal 2000 px aan de langste zijde. Dit vermindert het geheugenverbruik zonder de herkenning te schaden.
- **Taalfallback:** Als je een taal instelt die niet wordt ondersteund, valt de engine terug op Engels. Controleer altijd `engine.Language` na initialisatie als je taalmodules dynamisch laadt.
- **Thread‑veiligheid:** `OcrEngine`‑instanties zijn niet thread‑safe. Maak per verzoek een nieuwe engine aan in multi‑threaded omgevingen (bijv. ASP.NET Core).

## Conclusie

Je weet nu hoe je **tekst uit een afbeelding** kunt herkennen in C# met Aspose.OCR. De tutorial heeft je stap voor stap door het installeren van het pakket, het configureren van de taal, het laden van een PNG, het uitvoeren van OCR en het afhandelen van de output geleid. Met deze bouwblokken kun je ook **tekst uit png** extraheren, **afbeelding naar tekst converteren**, en robuuste **c# image ocr**‑oplossingen bouwen voor desktop, web of cloud scenario’s.

Ga vervolgens andere taalmodules verkennen (bijv. `Language.Spanish`) of integreer de OCR‑resultaten met natural‑language‑processing‑bibliotheken. Voor diepere prestatie‑optimalisaties, lees de Aspose.OCR‑documentatie over beeldvoorbewerking en aangepaste woordenboeken.

Happy coding!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat complete werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [How to Extract Text from Image Using Aspose.OCR for .NET](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}