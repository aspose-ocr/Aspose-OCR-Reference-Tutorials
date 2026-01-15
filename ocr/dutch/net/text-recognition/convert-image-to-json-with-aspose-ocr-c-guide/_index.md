---
category: general
date: 2026-01-15
description: Converteer afbeelding naar JSON met Aspose OCR in C#. Leer hoe je tekst
  uit een afbeelding kunt extraheren, JSON‑bounding boxes kunt verkrijgen en een bonafbeelding
  kunt herkennen.
draft: false
keywords:
- convert image to json
- extract text from image
- aspose ocr c# example
- recognize receipt image
- json bounding boxes
language: nl
og_description: Converteer afbeelding naar JSON met Aspose OCR in C#. Stapsgewijze
  handleiding om tekst uit een afbeelding te extraheren, een kassabonafbeelding te
  herkennen en JSON‑bounding boxes te verkrijgen.
og_title: Afbeelding converteren naar JSON met Aspose OCR C# gids
tags:
- Aspose OCR
- C#
- JSON
- Image Processing
title: Afbeelding naar JSON converteren met Aspose OCR C#‑gids
url: /nl/net/text-recognition/convert-image-to-json-with-aspose-ocr-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Afbeelding naar JSON converteren met Aspose OCR C# gids

Heb je ooit **afbeelding naar JSON** moeten converteren, maar wist je niet welke bibliotheek je zowel de ruwe tekst als de exacte woordcoördinaten kon geven? Je bent niet de enige. Veel ontwikkelaars lopen tegen dit probleem aan wanneer ze tekst uit afbeeldingsbestanden proberen te extraheren—met name bonnen—terwijl ze ook een machine‑leesbare JSON‑payload voor downstream verwerking nodig hebben.

In deze tutorial lopen we een volledig **Aspose OCR C# voorbeeld** door dat laat zien hoe je tekst uit een afbeelding haalt, een bonafbeelding herkent, en **JSON‑bounding boxes** voor elk woord uitvoert. Aan het einde heb je een kant‑klaar console‑applicatie die een mooi geformatteerde JSON‑string afdrukt die je kunt invoeren in elke API, database of analytics‑pipeline.

> **Wat je mee krijgt**  
> • Een volledig functioneel C#‑project dat **afbeelding naar JSON** converteert  
> • Inzicht waarom we `IncludeBoundingBoxes` inschakelen (het is de sleutel tot `json bounding boxes`)  
> • Tips voor het omgaan met verschillende afbeeldingsformaten en talen  

Laten we beginnen.

---

## Wat je nodig hebt

Voordat we in de code duiken, zorg ervoor dat je de volgende vereisten geïnstalleerd hebt:

- **.NET 6.0 SDK** (of een latere versie) – de code richt zich op .NET 6 maar werkt ook op .NET Framework 4.7+.
- **Aspose.OCR for .NET** NuGet‑pakket – je kunt het ophalen via `dotnet add package Aspose.OCR`.
- Een voorbeeld bonafbeelding (`receipt.jpg`) geplaatst in een map die je vanuit je project kunt refereren.
- Visual Studio 2022, VS Code, of elke IDE die je prefereert.

Er zijn geen andere externe services vereist; alles draait lokaal.

---

## Afbeelding naar JSON converteren – Overzicht

Het kernidee is simpel: laad een afbeelding, laat Aspose OCR Engels (of een andere ondersteunde taal) herkennen, vraag het om bounding boxes op te nemen, en vraag tenslotte om het resultaat in **JSON**‑formaat. De bibliotheek doet al het zware werk—OCR, lay‑outanalyse en JSON‑serialisatie.

Hier is een diagram op hoog niveau van de stroom (stel je een klein plaatje voor):

```
[Image File] → Aspose OCR Engine → Recognition Options (JSON + Bounding Boxes) → JSON Output
```

Dat kleine diagram vangt de volledige pijplijn die we gaan implementeren.

---

## Stap 1: Het project opzetten en Aspose OCR installeren

Maak eerst een nieuw console‑project aan en haal het Aspose OCR‑pakket binnen.

```bash
dotnet new console -n JsonOutputDemo
cd JsonOutputDemo
dotnet add package Aspose.OCR
```

> **Pro tip:** Als je Visual Studio gebruikt, klik met de rechtermuisknop op het project → *Manage NuGet Packages* → zoek naar **Aspose.OCR** en installeer de nieuwste stabiele versie (momenteel 23.12).

---

## Stap 2: Laad de afbeelding die je wilt herkennen

We gebruiken de `OcrImage.FromFile`‑methode om de bonafbeelding te lezen. Zorg ervoor dat het pad naar een bestaand bestand wijst; anders krijg je een `FileNotFoundException`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Output;

class JsonOutputDemo
{
    static void Main()
    {
        // Step 2: Load the image you want to recognize
        var receiptImage = OcrImage.FromFile("YOUR_DIRECTORY/receipt.jpg");
```

Als je afbeelding naast het `.csproj`‑bestand staat, kun je eenvoudig `"receipt.jpg"` gebruiken.

---

## Stap 3: OCR‑opties configureren voor JSON‑bounding boxes

De magie gebeurt wanneer we `OutputFormat = OutputFormat.Json` **en** `IncludeBoundingBoxes = true` inschakelen. Het eerste vertelt Aspose om het resultaat als JSON te serialiseren, terwijl het tweede `x`, `y`, `width` en `height` toevoegt voor elk woord—precies wat je nodig hebt voor `json bounding boxes`.

```csharp
        // Step 3: Configure OCR options
        var ocrOptions = new OcrOptions
        {
            OutputFormat = OutputFormat.Json,
            IncludeBoundingBoxes = true   // include coordinates for each recognized word
        };
```

Je kunt ook `ocrOptions.Dpi` of `ocrOptions.Language` aanpassen als je een hogere resolutie of een andere taal nodig hebt.

---

## Stap 4: Voer de herkenning uit – Tekst uit afbeelding extraheren

Nu roepen we `Recognize` aan. De methode retourneert een `OcrResult`‑object dat de JSON‑string, ruwe tekst en meer bevat.

```csharp
        // Step 4: Perform recognition using English language and the configured options
        var ocrEngine = new OcrEngine();
        var ocrResult = ocrEngine.Recognize(receiptImage, Language.English, ocrOptions);
```

Als je andere talen moet verwerken, vervang `Language.English` door `Language.Spanish`, `Language.French`, enz. Aspose ondersteunt meer dan 30 talen direct.

---

## Stap 5: Resultaat weergeven – Je JSON‑payload

Tot slot printen we de JSON naar de console. In een echte app zou je het waarschijnlijk naar een bestand schrijven of naar een service sturen.

```csharp
        // Step 5: Output the resulting JSON string
        System.Console.WriteLine(ocrResult.Json);
    }
}
```

Het uitvoeren van het programma zou een JSON‑document moeten produceren dat lijkt op de onderstaande snippet.

```json
{
  "Text": "Total $12.34\nDate 01/01/2024",
  "Words": [
    {
      "Text": "Total",
      "BoundingBox": { "X": 45, "Y": 112, "Width": 60, "Height": 20 }
    },
    {
      "Text": "$12.34",
      "BoundingBox": { "X": 110, "Y": 112, "Width": 70, "Height": 20 }
    },
    {
      "Text": "Date",
      "BoundingBox": { "X": 45, "Y": 140, "Width": 50, "Height": 20 }
    },
    {
      "Text": "01/01/2024",
      "BoundingBox": { "X": 100, "Y": 140, "Width": 120, "Height": 20 }
    }
  ]
}
```

Let op hoe elk woord nu zijn **JSON‑bounding box** draagt—perfect om in een UI‑overlay of een downstream‑parser te gebruiken.

---

## Volledig werkend voorbeeld

Hieronder staat het volledige, kant‑klaar programma. Geen verborgen delen, geen externe aanroepen—alleen pure C#.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Output;

class JsonOutputDemo
{
    static void Main()
    {
        // 1️⃣ Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // 2️⃣ Load the image you want to recognize
        var receiptImage = OcrImage.FromFile("YOUR_DIRECTORY/receipt.jpg");

        // 3️⃣ Configure OCR options to get detailed JSON output with word positions
        var ocrOptions = new OcrOptions
        {
            OutputFormat = OutputFormat.Json,
            IncludeBoundingBoxes = true   // include coordinates for each recognized word
        };

        // 4️⃣ Perform recognition using English language and the configured options
        var ocrResult = ocrEngine.Recognize(receiptImage, Language.English, ocrOptions);

        // 5️⃣ Output the resulting JSON string
        System.Console.WriteLine(ocrResult.Json);
    }
}
```

> **Let op:**  
> • **Bestandspad‑fouten** – controleer de afbeeldingslocatie dubbel.  
> • **Ontbrekend NuGet‑pakket** – zorg ervoor dat `Aspose.OCR` is verwezen.  
> • **Niet‑ondersteunde afbeeldingsformaten** – houd je aan JPEG, PNG, BMP of TIFF voor de beste resultaten.

---

## Veelgestelde vragen & randgevallen

### Kan ik een **PDF‑pagina** naar JSON converteren in plaats van een JPEG?

Ja. Converteer eerst de PDF‑pagina naar een afbeelding (bijv. met `Aspose.PDF`), en voer die afbeelding vervolgens in dezelfde OCR‑pijplijn. De JSON‑output zal identiek zijn omdat de OCR‑stap alleen rasterdata nodig heeft.

### Wat als de bon onscherp is?

Verhoog de DPI in `ocrOptions`. Bijvoorbeeld:

```csharp
ocrOptions.Dpi = 300; // higher DPI improves accuracy on low‑quality scans
```

Een hogere DPI kan het geheugenverbruik verhogen, dus balanceer kwaliteit versus prestaties.

### Ik heb **meerdere talen** nodig op dezelfde bon (bijv. Engels + Spaans).

Je kunt een array van talen doorgeven:

```csharp
var ocrResult = ocrEngine.Recognize(receiptImage, new[] { Language.English, Language.Spanish }, ocrOptions);
```

Aspose zal proberen elke taal in de opgegeven volgorde te herkennen.

### Hoe schrijf ik de JSON naar een bestand?

Vervang gewoon de `Console.WriteLine`‑regel door:

```csharp
System.IO.File.WriteAllText("receipt.json", ocrResult.Json);
```

Nu heb je een persistent bestand dat je naar andere services kunt verzenden.

---

## Visuele samenvatting

![convert image to json example](convert-image-to-json.png "convert image to json example")

*De screenshot toont de console‑output van de JSON‑payload na het uitvoeren van de demo.*

---

## Conclusie

We hebben je zojuist laten zien hoe je **afbeelding naar JSON** kunt **converteren** met Aspose OCR in C#. Door `OutputFormat` en `IncludeBoundingBoxes` te configureren, kun je **tekst uit afbeelding** extraheren, **bonafbeelding herkennen**, en nauwkeurige **JSON‑bounding boxes** voor elk woord verkrijgen. De volledige, uitvoerbare code staat in de snippet hierboven, zodat je deze direct in elk .NET‑project kunt plaatsen.

Wat is de volgende stap? Probeer de JSON te voeden aan een front‑end viewer die elk woord markeert, of stuur de data naar een machine‑learning‑model dat regelitems op bonnen classificeert. Je kunt ook experimenteren met andere talen, hogere DPI‑instellingen, of batch‑verwerking van meerdere afbeeldingen in een lus.

Als je tegen problemen aanloopt, onthoud dan de tips over bestandspaden, DPI en taal‑arrays. Voel je vrij om een reactie achter te laten of een issue te openen in de GitHub‑repo die je voor deze demo maakt. Veel plezier met coderen, en geniet van het omzetten van afbeeldingen naar gestructureerde JSON!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}