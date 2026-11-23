---
category: general
date: 2026-10-18
description: Voer snel OCR uit op een afbeelding in C#. Leer hoe je tekst uit een
  JPG kunt extraheren, een afbeelding naar tekst kunt converteren en tekst uit een
  afbeelding kunt lezen met Aspose.OCR.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- perform OCR on image
- extract text from JPG
- convert image to text
- read text from image
- load image for OCR
language: nl
lastmod: 2026-10-18
og_description: Voer OCR uit op een afbeelding in C# met Aspose.OCR. Deze tutorial
  laat zien hoe je tekst uit een JPG kunt extraheren, een afbeelding naar tekst kunt
  converteren en tekst uit een afbeelding kunt lezen in enkele minuten.
og_image_alt: Console output displaying recognized Cyrillic text after performing
  OCR on an image
og_title: OCR uitvoeren op een afbeelding in C# – volledige gids
schemas:
- author: Aspose
  dateModified: '2026-10-18'
  description: Perform OCR on an image in C# quickly. Learn to extract text from JPG,
    convert image to text and read text from image using Aspose.OCR.
  headline: How to perform OCR on an image in C# with Aspose.OCR
  type: TechArticle
tags:
- OCR
- C#
- Aspose.OCR
title: Hoe OCR op een afbeelding uit te voeren in C# met Aspose.OCR
url: /nl/net/text-recognition/how-to-perform-ocr-on-an-image-in-c-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe OCR uit te voeren op een afbeelding in C# met Aspose.OCR

Als je **OCR wilt uitvoeren op een afbeelding** in een .NET‑applicatie, laat deze gids je een complete, kant‑klaar oplossing zien. Je ziet hoe je **een afbeelding laadt voor OCR**, Cyrillische tekens herkent, en **tekst uit JPG**‑bestanden haalt zonder enige low‑level beeldverwerkingscode te schrijven.

In deze tutorial zul je:

* Installeer het Aspose.OCR NuGet‑pakket.  
* Laad een afbeeldingsbestand (JPG, PNG, BMP, enz.).  
* Voer de OCR‑engine uit om **afbeelding naar tekst te converteren**.  
* **Lees tekst uit afbeelding** in de console.  

De stappen werken met elke .NET‑compatibele afbeelding, zodat je ze kunt aanpassen voor PDF‑bestanden, gescande bonnen of screenshots.

## Vereisten

* .NET 6.0 SDK of later (de code werkt ook met .NET Framework 4.7+).  
* Visual Studio 2022 of een andere C#‑editor naar keuze.  
* Internettoegang voor de eerste uitvoering – Aspose.OCR downloadt automatisch de Cyrillische taalmodule.  

> **Pro tip:** Houd het NuGet‑pakket up‑to‑date; nieuwere versies verbeteren de herkenningsnauwkeurigheid en voegen taalpakketten toe.

## Stap 1: Installeer Aspose.OCR

Open een terminal in je projectmap en voer uit:

```bash
dotnet add package Aspose.OCR
```

Het pakket bevat de `OcrEngine`‑klasse die wordt gebruikt om **OCR uit te voeren op afbeeldings**‑bestanden. Nadat het commando is voltooid, verschijnt de pakketreferentie in je *.csproj*‑bestand.

## Stap 2: Maak een console‑programmaskelet

Maak een nieuw console‑project aan als je er nog geen hebt:

```bash
dotnet new console -n OcrDemo
cd OcrDemo
```

Vervang de gegenereerde *Program.cs* door de code die in de volgende secties wordt getoond. Het skelet bevat de vereiste `using`‑directieven en een `Main`‑methode die het OCR‑proces aanstuurt.

## Stap 3: Laad afbeelding voor OCR

De eerste functionele code‑regel **laadt de afbeelding** die je wilt analyseren. Aspose.OCR accepteert elke stream, zodat je een bestand van schijf, een web‑URL of een ingebedde resource kunt laden.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;

class Program
{
    static void Main()
    {
        // Step 3: Load the image containing Cyrillic text
        // Replace the path with the location of your JPG file.
        string imagePath = @"YOUR_DIRECTORY\cyrillic-sample.jpg";
        using var image = ImageStream.FromFile(imagePath);
```

*Waarom dit belangrijk is*: Het gebruik van `ImageStream.FromFile` abstraheert de formatafhandeling, waardoor de OCR‑engine een consistente bitmap ontvangt ongeacht het oorspronkelijke bestandstype. Het sluit de stream ook automatisch dankzij de `using`‑statement.

## Stap 4: Initialiseert de OCR‑engine en stel taal in (optioneel)

Standaard probeert Aspose.OCR de taal automatisch te detecteren. Voor Cyrillische tekst kun je expliciet het `Language.Cyrillic`‑module aanvragen, wat de eerste download versnelt.

```csharp
        // Step 4: Initialize the OCR engine
        var engine = new OcrEngine();

        // Optional: force Cyrillic language to avoid auto‑detection overhead
        engine.Language = Language.Cyrillic;
```

Als je de taaltoewijzing weglaten, downloadt de engine de benodigde module de eerste keer dat je `Recognize` aanroept. De download gebeurt via HTTPS en wordt lokaal gecached voor volgende uitvoeringen.

## Stap 5: Voer OCR uit en converteer afbeelding naar tekst

Nu voer je daadwerkelijk **OCR uit op afbeelding** en verkrijg je een platte‑tekst‑string. De `Recognize`‑methode doet al het zware werk: pre‑processing, lay-outanalyse en tekenclassificatie.

```csharp
        // Step 5: Perform OCR – convert image to text
        engine.Image = image;
        string recognizedText = engine.Recognize();
```

De geretourneerde `recognizedText` bevat regeleinden die overeenkomen met de oorspronkelijke lay-out, waardoor het eenvoudig is om na te bewerken of op te slaan in een database.

## Stap 6: Toon het resultaat – lees tekst uit afbeelding

Tot slot **lees je tekst uit afbeelding** door het resultaat naar de console te schrijven. Deze stap verifieert dat de OCR geslaagd is en toont je precies wat er is geëxtraheerd.

```csharp
        // Step 6: Display the recognized text – read text from image
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(recognizedText);
    }
}
```

Wanneer je het programma uitvoert (`dotnet run`), zou je een output moeten zien die lijkt op:

```
=== OCR Result ===
Пример текста на кириллице
```

> **Opmerking:** De exacte output hangt af van de kwaliteit van de bron‑JPG. Duidelijke, hoge‑resolutie‑afbeeldingen leveren de beste resultaten op.

## Volledige, uitvoerbare broncode

Hieronder staat het volledige programma dat je kunt kopiëren‑en‑plakken in *Program.cs* en kunt uitvoeren zonder aanpassingen (behalve het afbeeldingspad).

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;

class Program
{
    static void Main()
    {
        // Load the image containing Cyrillic text
        string imagePath = @"YOUR_DIRECTORY\cyrillic-sample.jpg";
        using var image = ImageStream.FromFile(imagePath);

        // Initialize the OCR engine
        var engine = new OcrEngine
        {
            // Force Cyrillic language; optional but speeds up first run
            Language = Language.Cyrillic,
            Image = image
        };

        // Recognize the text – this converts the image to text
        string recognizedText = engine.Recognize();

        // Display the recognized text
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(recognizedText);
    }
}
```

Het uitvoeren van het programma drukt de geëxtraheerde tekens af naar de console, waarmee bewezen wordt dat je succesvol **tekst uit JPG** hebt **geëxtraheerd** en **afbeelding naar tekst hebt geconverteerd**.

## Veelvoorkomende variaties afhandelen

| Scenario | Adjustment |
|----------|------------|
| **Andere taal** | Stelt `engine.Language = Language.English;` in of een andere ondersteunde enum. |
| **Meerdere‑pagina PDF** | Converteer elke pagina naar een afbeelding (bijv. met `Aspose.PDF`) en roep de OCR‑lus aan voor elke afbeelding. |
| **Grote batch** | Wikkel de OCR‑aanroep in een `Parallel.ForEach`‑lus; hergebruik één `OcrEngine`‑instantie om het geheugenverbruik te verminderen. |
| **Laag‑resolutie afbeelding** | Pre‑process met `engine.Image = ImageProcessing.Filters.GaussianBlur(image, 1.5);` om ruis te verminderen vóór herkenning. |

## Prestatie‑tips

* **Cache taalmodules** – de eerste download kan enkele seconden duren; volgende uitvoeringen zijn onmiddellijk. |
* **Herbruik de `OcrEngine`**‑instantie voor meerdere afbeeldingen om herhaalde initialisatiekosten te vermijden. |
* **Beperk de afbeeldingsgrootte** – extreem grote foto’s verhogen het geheugenverbruik. Schaal naar maximaal 2000 px in breedte voordat je ze aan de engine doorgeeft.

## Conclusie

Je weet nu hoe je **OCR kunt uitvoeren op afbeeldings**‑bestanden in C# met Aspose.OCR. Door een afbeelding te laden, de engine te configureren en `Recognize` aan te roepen, kun je **tekst uit JPG** extraheren, **afbeelding naar tekst converteren**, en **tekst uit afbeelding lezen** met slechts een paar regels code.  

Vanaf hier kun je het volgende verkennen:

* Het opslaan van de OCR‑resultaten in een database voor doorzoekbare archieven.  
* Het integreren van de workflow in een web‑API die geüploade afbeeldingen accepteert.  
* Het gebruiken van andere taalmodule­s (Arabisch, Hindi, enz.) om het bereik van je applicatie te vergroten.

Voel je vrij om te experimenteren met verschillende afbeeldingsformaten, talen en batch‑verwerkingsstrategieën. Het kernpatroon — **afbeelding laden voor OCR → herkennen → de platte‑tekst‑output verwerken** — blijft hetzelfde, en biedt je een solide basis voor elk tekst‑extractie‑project.

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat complete werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [How to extract text from image using Aspose.OCR for .NET](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}