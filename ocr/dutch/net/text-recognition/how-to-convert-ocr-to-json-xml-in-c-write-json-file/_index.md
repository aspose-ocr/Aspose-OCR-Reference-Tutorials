---
category: general
date: 2026-04-01
description: Hoe OCR‑uitvoer omzetten naar JSON en XML in C# – leer tekst uit een
  afbeelding te extraheren en een JSON‑bestand te schrijven in C# met Aspose.OCR.
draft: false
keywords:
- how to convert ocr
- extract text from image
- write json file c#
- write xml file c#
- how to extract text
language: nl
og_description: Hoe OCR-resultaten omzetten naar gestructureerde JSON- en XML-bestanden
  met C#. Stapsgewijze handleiding om tekst uit een afbeelding te extraheren en een
  JSON‑bestand te schrijven in C#.
og_title: Hoe OCR naar JSON & XML te converteren in C# – JSON-bestand schrijven
tags:
- OCR
- C#
- Aspose
title: Hoe OCR omzetten naar JSON & XML in C# – JSON‑bestand schrijven
url: /nl/net/text-recognition/how-to-convert-ocr-to-json-xml-in-c-write-json-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe OCR te converteren naar JSON & XML in C# – JSON‑bestand schrijven

**Hoe OCR te converteren** resultaten naar iets dat je daadwerkelijk kunt gebruiken is een vraag die veel ontwikkelaars stellen. In deze gids laten we je zien hoe je tekst uit een afbeelding haalt, die OCR‑uitvoer omzet in mooi opgemaakte JSON en XML, en vervolgens die bestanden naar schijf schrijft met C#.

Als je ooit naar een ruwe OCR‑string hebt gekeken en dacht: “Er moet een betere manier zijn om dit op te slaan,” dan ben je op de juiste plek. Aan het einde heb je een compleet, uitvoerbaar programma dat niet alleen **tekst uit afbeelding**‑bestanden extraheert, maar ook weet hoe je **JSON‑bestand schrijft C#** en **XML‑bestand schrijft C#** zonder moeite.

## Wat je nodig hebt

- **.NET 6.0** of later (de code werkt ook met .NET Framework 4.6+).  
- **Aspose.OCR** NuGet‑pakket – installeer het met `dotnet add package Aspose.OCR`.  
- Een afbeelding met tekst (bijv. `invoice.png`).  
- Elke IDE die je wilt – Visual Studio, Rider, of VS Code volstaat.

> **Pro tip:** Houd je afbeeldingsbestanden in een speciale map (bijv. `Resources/`) zodat de paden overzichtelijk blijven.

## Stap 1: OCR‑engine instellen – Hoe OCR te converteren

Eerst maken we een `OcrEngine`‑instance aan en geven we aan welke taal gezocht moet worden. In de meeste gevallen is Engels voldoende, maar je kunt `Language.English` vervangen door elke ondersteunde taal.

```csharp
using Aspose.OCR;
using System.IO;

class JsonXmlOcrDemo
{
    static void Main()
    {
        // Step 1: Initialise the OCR engine for English text
        var ocrEngine = new OcrEngine { Language = Language.English };
```

> **Waarom dit belangrijk is:** Het initialiseren van de engine met de juiste taal verbetert de nauwkeurigheid aanzienlijk, vooral voor niet‑Latijnse scripts.

## Stap 2: Tekst herkennen – Tekst uit afbeelding extraheren

Nu voeren we de afbeelding in de engine. De `Recognize`‑methode retourneert een `OcrResult`‑object dat de ruwe tekst en locatiegegevens bevat.

```csharp
        // Step 2: Recognise text from the supplied image
        // Replace "YOUR_DIRECTORY/invoice.png" with your actual file path
        var ocrResult = ocrEngine.Recognize("YOUR_DIRECTORY/invoice.png");
```

Als de afbeelding niet gevonden kan worden, gooit `Recognize` een `FileNotFoundException`. Om de demo eenvoudig te houden gaan we ervan uit dat het pad correct is, maar in productie zou je dit in een try‑catch‑blok willen plaatsen.

## Stap 3: Het resultaat naar JSON converteren – JSON‑bestand schrijven C#

Aspose.OCR maakt serialisatie een fluitje van een cent. De `ToJson`‑methode accepteert een `indent`‑vlag om mooi opgemaakte output te produceren, wat perfect is wanneer je het bestand in een teksteditor wilt openen.

```csharp
        // Step 3: Convert OCR result to formatted JSON
        string jsonOutput = ocrResult.ToJson(indent: true);
```

### Verwacht JSON‑voorbeeld

```json
{
  "Text": "Invoice #12345\nDate: 2024‑03‑31\nTotal: $250.00",
  "Regions": [
    {
      "Bounds": { "X": 10, "Y": 20, "Width": 200, "Height": 30 },
      "Text": "Invoice #12345"
    }
    // … more regions …
  ]
}
```

> **Hoe tekst te extraheren:** De `Text`‑eigenschap geeft je de platte string die je kunt doorgeven aan andere services (zoekindexen, databases, enz.).

## Stap 4: JSON opslaan – JSON‑bestand schrijven C# (Vervolg)

Met de JSON‑string klaar, schrijven we deze eenvoudig naar een bestand met `File.WriteAllText`. Dit zorgt standaard voor UTF‑8‑codering.

```csharp
        // Step 4: Save JSON to disk
        File.WriteAllText("YOUR_DIRECTORY/invoice.json", jsonOutput);
```

Nu heb je een `invoice.json` naast je afbeelding, klaar voor verdere verwerking.

## Stap 5: Het resultaat naar XML converteren – XML‑bestand schrijven C#

Als je XML verkiest voor legacy‑systemen, doet de `ToXml`‑methode het zware werk. Net als `ToJson` ondersteunt het ook mooi opmaken.

```csharp
        // Step 5: Convert OCR result to formatted XML
        string xmlOutput = ocrResult.ToXml(indent: true);
```

### Verwacht XML‑voorbeeld

```xml
<OcrResult>
  <Text>Invoice #12345
Date: 2024-03-31
Total: $250.00</Text>
  <Regions>
    <Region>
      <Bounds X="10" Y="20" Width="200" Height="30" />
      <Text>Invoice #12345</Text>
    </Region>
    <!-- … more regions … -->
  </Regions>
</OcrResult>
```

## Stap 6: XML opslaan – XML‑bestand schrijven C# (Vervolg)

Het opslaan van de XML is identiek aan de JSON‑stap; geef gewoon een `.xml`‑extensie op.

```csharp
        // Step 6: Save XML to disk
        File.WriteAllText("YOUR_DIRECTORY/invoice.xml", xmlOutput);
    }
}
```

### Volledig werkend voorbeeld

Alles bij elkaar, hier is het volledige programma dat je kunt kopiëren‑plakken in een console‑applicatie:

```csharp
using Aspose.OCR;
using System.IO;

class JsonXmlOcrDemo
{
    static void Main()
    {
        // Initialise OCR engine for English
        var ocrEngine = new OcrEngine { Language = Language.English };

        // Recognise text from image
        var ocrResult = ocrEngine.Recognize("YOUR_DIRECTORY/invoice.png");

        // Convert to JSON and save
        string jsonOutput = ocrResult.ToJson(indent: true);
        File.WriteAllText("YOUR_DIRECTORY/invoice.json", jsonOutput);

        // Convert to XML and save
        string xmlOutput = ocrResult.ToXml(indent: true);
        File.WriteAllText("YOUR_DIRECTORY/invoice.xml", xmlOutput);
    }
}
```

Voer het programma uit, en je zult twee nieuwe bestanden vinden — `invoice.json` en `invoice.xml` — precies op de opgegeven locatie. Open ze om te verifiëren dat de structuur overeenkomt met de bovenstaande voorbeelden.

## Veelgestelde vragen & randgevallen

| Vraag | Antwoord |
|----------|--------|
| **Wat als de afbeelding meerdere talen bevat?** | Maak aparte `OcrEngine`‑instances voor elke taal of gebruik `Language.Multi` indien ondersteund. |
| **Kan ik het uitvoerformaat regelen (bijv. regio‑gegevens uitsluiten)?** | Ja. Zowel `ToJson` als `ToXml` accepteren optionele parameters om velden te filteren; raadpleeg de Aspose.OCR‑documentatie voor `ExportOptions`. |
| **Hoe ga ik om met grote PDF's met veel pagina's?** | Verwerk elke pagina afzonderlijk, aggregeer de resultaten en serialiseer vervolgens één keer. |
| **Is de uitvoer UTF‑8 veilig?** | Absoluut—Aspose.OCR gebruikt intern Unicode, en `File.WriteAllText` schrijft standaard UTF‑8. |
| **Hoe zit het met prestaties?** | OCR is CPU‑intensief. Voor batch‑taken overweeg parallelisatie over cores of gebruik de cloud‑API van Aspose. |

## Conclusie

Je weet nu **hoe OCR**‑resultaten om te zetten naar zowel JSON als XML met C#. Door de bovenstaande stappen te volgen kun je **tekst uit afbeelding** extraheren, vervolgens **JSON‑bestand schrijven C#** en **XML‑bestand schrijven C#** met slechts een handvol regels. Deze aanpak is snel, betrouwbaar, en werkt met elk afbeeldingstype dat Aspose.OCR ondersteunt.

Klaar voor de volgende uitdaging? Probeer de

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}