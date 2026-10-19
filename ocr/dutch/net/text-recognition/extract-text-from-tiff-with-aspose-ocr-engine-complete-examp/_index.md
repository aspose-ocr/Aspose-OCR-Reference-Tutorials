---
category: general
date: 2026-04-04
description: Leer hoe je tekst uit TIFF‑bestanden kunt extraheren met een OCR‑engine‑voorbeeld
  in C#. Stapsgewijze handleiding met JSON‑ en XML‑output.
draft: false
keywords:
- extract text from tiff
- ocr engine example
- Aspose OCR C#
- multi‑page TIFF OCR
- JSON OCR result
language: nl
og_description: Tekst extraheren uit TIFF‑bestanden met een OCR‑engine – voorbeeld
  in C#. Gedetailleerde stappen, volledige code en tips voor JSON/XML‑uitvoer.
og_title: Tekst extraheren uit TIFF met Aspose OCR‑engine – volledige gids
tags:
- C#
- OCR
- Aspose
- Image Processing
title: Tekst uit TIFF extraheren met Aspose OCR-engine – Volledig voorbeeld
url: /nl/net/text-recognition/extract-text-from-tiff-with-aspose-ocr-engine-complete-examp/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tekst extraheren uit TIFF – Volledig OCR‑engine voorbeeld in C#

Heb je ooit **tekst uit TIFF**‑afbeeldingen moeten halen, maar wist je niet welke bibliotheek multi‑page bestanden aankan zonder een wirwar aan workarounds? Je bent niet de enige. In veel legacy‑systemen komen documenten binnen als multi‑page TIFF‑scans, en de ruwe tekst eruit halen is een onmisbare functie voor zoeken, compliance of automatisering van gegevensinvoer.

Het goede nieuws? Met Aspose OCR kun je het in een handvol regels doen—zonder te rommelen met low‑level pixel‑buffers. Deze tutorial leidt je door een **volledig OCR‑engine voorbeeld** dat een multi‑page TIFF laadt, elke pagina herkent en zowel mooi opgemaakte JSON als optionele XML produceert. Aan het einde heb je een kant‑klaar C# console‑applicatie die tekst uit TIFF‑bestanden haalt in enkele seconden.

## Wat je zult leren

- Hoe je de Aspose OCR‑engine instelt in een .NET‑project.  
- De exacte code die nodig is om **tekst uit TIFF**‑bestanden te **extraheren**, inclusief multi‑page handling.  
- Waarom je JSON in plaats van XML zou willen en hoe je beide genereert.  
- Tips voor het oplossen van veelvoorkomende valkuilen (bijv. DPI van de afbeelding, geheugenverbruik).  

### Vereisten

- .NET 6.0 SDK of later (de code werkt met .NET Core en .NET Framework).  
- Een geldige Aspose OCR‑licentie (of een gratis trial‑sleutel).  
- Visual Studio 2022 of een andere C#‑editor naar keuze.  
- Een voorbeeld‑multi‑page TIFF‑bestand (genaamd `multi-page.tiff` in het voorbeeld).  

> **Pro tip:** Als je een krap budget hebt, laat de gratis trial je nog steeds tekst extraheren uit maximaal 100 pagina’s per maand—perfect voor testen.

---

## Stap 1 – Initialiseer de OCR‑engine (ocr engine example)

Voordat we **tekst uit TIFF** kunnen **extraheren**, hebben we een instantie van de OCR‑engine nodig. Dit object bevat alle configuraties die je later eventueel kunt aanpassen (taal, resolutie, enz.).

```csharp
using Aspose.OCR;
using System.IO;

// Create a new OCR engine – this is the core of our ocr engine example
var ocrEngine = new OcrEngine();

// Optional: set language if you know the document’s language
// ocrEngine.Language = Language.English;
```

*Waarom dit belangrijk is:* De `OcrEngine`‑klasse abstraheert het zware werk. Eén keer instantiëren en hergebruiken voor meerdere afbeeldingen is geheugen‑efficiënter dan voor elke pagina een nieuwe engine te maken.

---

## Stap 2 – Laad de multi‑page TIFF (extract text from TIFF)

Nu wijzen we de engine op ons bronbestand. `ImageStream.FromFile` ondersteunt TIFF, JPEG, PNG en vele anderen, maar voor deze tutorial focussen we op TIFF.

```csharp
// Load the multi‑page TIFF you want to process
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/multi-page.tiff");
```

> **Opmerking:** Vervang `YOUR_DIRECTORY` door het daadwerkelijke mappad op jouw machine.  
> **Tip:** Als je TIFF een lage DPI heeft (onder 150), overweeg dan pre‑processing om de OCR‑nauwkeurigheid te verbeteren.

---

## Stap 3 – Herken alle pagina’s

Het aanroepen van `Recognize()` voert het OCR‑algoritme uit over **elke pagina** in de TIFF. Het resultaatobject bevat de ruwe tekst, confidence‑scores en paginawijze segmentatie.

```csharp
// Run OCR on the loaded image – this extracts text from all pages
var ocrResult = ocrEngine.Recognize();
```

*Wat je terugkrijgt:* `ocrResult` bevat een collectie van `PageResult`‑objecten. De tekst van elke pagina kun je benaderen via `ocrResult.Pages[i].Text`. De engine levert ook confidence‑niveaus, wat handig kan zijn voor kwaliteitscontroles.

---

## Stap 4 – Sla resultaten op als JSON (en optionele XML)

De meeste moderne pipelines geven de voorkeur aan JSON, maar legacy‑systemen blijven XML gebruiken. Zo genereer je beide, netjes opgemaakt.

```csharp
// Convert the recognition result to pretty‑printed JSON
string jsonResult = ocrResult.ToJson(prettyPrint: true);
File.WriteAllText(@"YOUR_DIRECTORY/result.json", jsonResult);

// Optional: also output XML for older workflows
string xmlResult = ocrResult.ToXml();
File.WriteAllText(@"YOUR_DIRECTORY/result.xml", xmlResult);
```

### Voorbeeld JSON‑output (afgekapt)

```json
{
  "Pages": [
    {
      "PageNumber": 1,
      "Text": "Invoice #12345\nDate: 2024‑03‑15\nTotal: $1,250.00",
      "Confidence": 0.97
    },
    {
      "PageNumber": 2,
      "Text": "Itemized List\n1. Widget A – $500.00\n2. Widget B – $750.00",
      "Confidence": 0.95
    }
  ]
}
```

De JSON is mens‑leesbaar, waardoor debuggen een fluitje van een cent is. De XML spiegelt dezelfde structuur als je die nodig hebt.

---

## Stap 5 – Verifieer de extractie (extract text from TIFF)

Nadat de bestanden zijn weggeschreven, helpt een snelle sanity‑check om te bevestigen dat er niets mis is gegaan.

```csharp
// Load the JSON back just to confirm it was saved correctly
string loadedJson = File.ReadAllText(@"YOUR_DIRECTORY/result.json");
Console.WriteLine("First 200 characters of JSON output:");
Console.WriteLine(loadedJson.Substring(0, Math.Min(200, loadedJson.Length)));
```

Als je het fragment ziet afgedrukt, heb je met succes **tekst uit TIFF** geëxtraheerd en opgeslagen. Vanaf hier kun je de JSON in een zoekindex, een database of een andere downstream‑service voeden.

---

## Waarom Aspose OCR gebruiken om tekst uit TIFF te extraheren?

- **Multi‑page ondersteuning out‑of‑the‑box** – geen handmatig splitsen van de TIFF nodig.  
- **Hoge nauwkeurigheid** dankzij propriëtaire neurale‑netwerkmodellen.  
- **Cross‑platform** – werkt op Windows, Linux en macOS .NET‑runtimes.  
- **Rijke outputformaten** (JSON, XML, plain text) die zowel moderne als legacy‑stacks bedienen.  

Als je nog twijfelt, probeer dan de gratis trial op een voorbeeld‑document. Je zult de snelheid en eenvoud merken ten opzichte van open‑source alternatieven die vaak extra beeld‑pre‑processing vereisen.

---

## Veelvoorkomende valkuilen & hoe ze te vermijden

| Probleem | Symptoom | Oplossing |
|----------|----------|-----------|
| Lage resolutie TIFF | Ontbrekende tekens, lage confidence | Schaal de afbeelding op naar ≥150 DPI vóór OCR (`ocrEngine.Image = ImageStream.FromFile(...).Resize(150)` ) |
| Verkeerde taal | Vervormde woorden, vooral bij niet‑Engelse tekst | Stel `ocrEngine.Language = Language.Spanish` (of passend) in vóór `Recognize()` |
| Out‑of‑memory bij grote bestanden | `OutOfMemoryException` | Verwerk pagina’s in batches: loop door `ocrEngine.Image.Pages` en roep `RecognizePage(i)` aan |
| Licentie niet toegepast | Watermerk “Evaluation” in output | Registreer je licentie: `License license = new License(); license.SetLicense("Aspose.OCR.lic");` |

---

## Volledig werkend voorbeeld (Kopieer‑en‑Plak klaar)

Hieronder staat het complete programma dat je in een nieuw console‑project kunt plakken. Het bevat alle besproken onderdelen—initialisatie, laden, herkenning en opslaan.

```csharp
using Aspose.OCR;
using System;
using System.IO;

namespace TiffOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣  Initialize the OCR engine (ocr engine example)
            // -------------------------------------------------
            var ocrEngine = new OcrEngine();

            // Optional: set license if you have one
            // var license = new License();
            // license.SetLicense("Aspose.OCR.lic");

            // -------------------------------------------------
            // 2️⃣  Load the multi‑page TIFF (extract text from TIFF)
            // -------------------------------------------------
            string tiffPath = @"YOUR_DIRECTORY/multi-page.tiff";
            if (!File.Exists(tiffPath))
            {
                Console.WriteLine($"File not found: {tiffPath}");
                return;
            }

            ocrEngine.Image = ImageStream.FromFile(tiffPath);

            // -------------------------------------------------
            // 3️⃣  Recognize every page
            // -------------------------------------------------
            var ocrResult = ocrEngine.Recognize();

            // -------------------------------------------------
            // 4️⃣  Save JSON (pretty) and optional XML
            // -------------------------------------------------
            string jsonPath = @"YOUR_DIRECTORY/result.json";
            string jsonResult = ocrResult.ToJson(prettyPrint: true);
            File.WriteAllText(jsonPath, jsonResult);
            Console.WriteLine($"JSON saved to {jsonPath}");

            // Optional XML output
            string xmlPath = @"YOUR_DIRECTORY/result.xml";
            string xmlResult = ocrResult.ToXml();
            File.WriteAllText(xmlPath, xmlResult);
            Console.WriteLine($"XML saved to {xmlPath}");

            // -------------------------------------------------
            // 5️⃣  Quick verification (extract text from TIFF)
            // -------------------------------------------------
            string preview = jsonResult.Length > 200 ? jsonResult.Substring(0, 200) + "..." : jsonResult;
            Console.WriteLine("\nPreview of JSON output:");
            Console.WriteLine(preview);
        }
    }
}
```

Sla het bestand op als `Program.cs`, voer `dotnet run` uit, en zie in de console waar de JSON en XML zijn opgeslagen. Dat is alles—je hebt zojuist een **ocr‑engine voorbeeld** voltooid dat tekst uit TIFF extrahert.

---

## Volgende stappen & gerelateerde onderwerpen

- **Batchverwerking:** Verpak de bovenstaande logica in een `foreach`‑loop om tientallen TIFF‑bestanden automatisch te verwerken.  
- **Zoekintegratie:** Stuur de JSON naar Elasticsearch of Azure Cognitive Search om full‑text zoeken over gescande documenten mogelijk te maken.  
- **Beeld‑pre‑processing:** Verken Aspose’s `ImageProcessing`‑API om te deskew, despeckle of het contrast aan te passen vóór OCR.  
- **Alternatieve output:** Gebruik `ocrResult.ToPlainText()` als je alleen ruwe strings zonder metadata nodig hebt.  

Als je nieuwsgierig bent naar andere afbeeldingsformaten, werkt hetzelfde patroon voor PDF’s (verander simpelweg het bronbestand) of PNG’s. Het belangrijkste inzicht is dat zodra de engine is opgezet, de rest een herhaalbare pipeline is.

---

## Conclusie

We hebben een **volledig OCR‑engine voorbeeld** doorlopen waarmee je **tekst uit TIFF**‑bestanden kunt **extraheren** met Aspose OCR, en nette JSON en optionele XML kunt genereren voor elke downstream‑workflow. De code staat op zichzelf, de uitleg behandelt het “waarom” achter elke stap.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}