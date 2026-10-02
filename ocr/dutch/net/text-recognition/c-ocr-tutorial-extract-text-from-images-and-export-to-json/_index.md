---
category: general
date: 2026-01-01
description: c# OCR‑tutorial die laat zien hoe je tekst extraheert, een afbeelding
  laadt voor OCR en JSON naar een bestand schrijft met Aspose.OCR – stapsgewijze gids.
draft: false
keywords:
- c# OCR tutorial
- how to extract text
- write json to file
- load image for OCR
- OCR image to JSON
language: nl
og_description: c# OCR-tutorial die je stap voor stap laat zien hoe je tekst uit afbeeldingen
  kunt extraheren, een afbeelding kunt laden voor OCR, en JSON naar een bestand kunt
  schrijven met Aspose.OCR.
og_title: c# OCR‑tutorial – Tekst extraheren en exporteren naar JSON
tags:
- Aspose.OCR
- C#
- Text Extraction
title: c# OCR-tutorial – Tekst uit afbeeldingen extraheren en exporteren naar JSON
url: /nl/net/text-recognition/c-ocr-tutorial-extract-text-from-images-and-export-to-json/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# OCR tutorial – Tekst extraheren uit afbeeldingen en exporteren naar JSON

Heb je je ooit afgevraagd hoe je tekst uit een gescande factuur kunt extraheren zonder uren te besteden aan het schrijven van aangepaste parsers? Je bent niet de enige. In deze **c# OCR tutorial** laten we je precies zien hoe je een afbeelding laadt voor OCR, de herkenningsengine uitvoert, en vervolgens **JSON naar bestand schrijft** zodat je de gegevens kunt doorvoeren naar downstream‑systemen.

Stel je voor dat je een map met bonnen hebt, elk genaamd `receipt1.png`, `receipt2.png`, en je een snelle manier nodig hebt om ze om te zetten in doorzoekbare JSON‑records. Dat is het probleem dat we gaan oplossen, en aan het einde heb je een kant‑klaar console‑applicatie die precies dat doet. Geen extra afhankelijkheden buiten Aspose.OCR, en geen magie—alleen duidelijke, reproduceerbare stappen.

> **Wat je zult leren**
> - Hoe je **image for OCR laadt** met Aspose.OCR.
> - De beste manier om **tekst te extraheren** en vertrouwensscores te krijgen.
> - Het OCR‑resultaat omzetten in een netjes gestructureerde **OCR image to JSON** payload.
> - Veilig **JSON naar bestand schrijven** en de output verifiëren.

## Vereisten

- .NET 6 SDK of later (de code werkt ook op .NET Core).  
- Visual Studio 2022 of een editor naar keuze.  
- Aspose.OCR NuGet‑pakket (`Install-Package Aspose.OCR`).  
- Een afbeeldingsbestand (PNG, JPG, BMP) dat je wilt verwerken – voor de demo gebruiken we `invoice.png`.

Als je een van deze mist, haal dan de SDK van de Microsoft‑site en voeg het NuGet‑pakket toe via de Package Manager Console:

```powershell
Install-Package Aspose.OCR
```

Nu de basis is gelegd, duiken we in de daadwerkelijke implementatie.

## Stap 1: c# OCR tutorial – Initialiseer de OCR‑engine

Voordat we **image for OCR kunnen laden**, hebben we een instantie van de engine nodig die het herkenningsproces aanstuurt. De `OcrEngine`‑klasse is lichtgewicht, maar het is goed om deze in een `using`‑block te plaatsen zodat bronnen direct worden vrijgegeven.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class JsonExportDemo
{
    static void Main()
    {
        // Step 1: Create the OCR engine – this is the heart of the c# OCR tutorial
        var ocrEngine = new OcrEngine();

        // The rest of the steps follow…
```

*Pro tip:* Als je van plan bent om veel afbeeldingen in één batch te verwerken, hergebruik dan dezelfde `OcrEngine`‑instantie in plaats van elke keer een nieuwe te maken. Dit vermindert geheugen‑churn en versnelt het proces.

## Stap 2: Afbeelding laden voor OCR

Nu **laden we daadwerkelijk de afbeelding voor OCR**. Aspose.OCR ondersteunt diverse formaten, zodat je een PNG, JPEG of zelfs een multi‑page TIFF kunt aanwijzen. De `OcrImage.FromFile`‑methode leest het bestand en maakt het klaar voor herkenning.

```csharp
        // Step 2: Load the image you want to recognize
        // Replace YOUR_DIRECTORY with the folder that holds your invoice.png
        var imagePath = @"YOUR_DIRECTORY/invoice.png";
        var ocrImage = OcrImage.FromFile(imagePath);
```

> **Waarom dit belangrijk is:** Het apart laden van de afbeelding laat je de afmetingen, DPI of zelfs een pre‑processing stap (bijv. binarisatie) inspecteren voordat je het naar de engine stuurt. Als de afbeelding corrupt is, zal `FromFile` een duidelijke uitzondering gooien, die je kunt opvangen en loggen.

## Stap 3: Hoe tekst extraheren – Voer de herkenning uit

Met de afbeelding in de hand kunnen we eindelijk **tekst extraheren**. De `Recognize`‑methode retourneert een `OcrResult`‑object dat niet alleen de platte tekst bevat, maar ook positionele data en vertrouwensscores voor elk woord.

```csharp
        // Step 3: Perform OCR – this is the core of how to extract text
        var ocrResult = ocrEngine.Recognize(ocrImage);
```

*Edge case:* Sommige PDF’s bevatten onzichtbare tekstlagen. Als je een PDF‑pagina als afbeelding invoert, ziet de engine mogelijk niets. Overweeg in dat geval eerst Aspose.PDF te gebruiken om de verborgen laag te extraheren, en alleen terug te vallen op OCR wanneer dat nodig is.

## Stap 4: OCR image to JSON – Converteer het resultaat

De `OcrResult`‑klasse biedt een handige `ToJson()`‑helper die de volledige resultaatsset – inclusief de omhullende box en confidence van elk woord – serialiseert naar een JSON‑string. Dit is de schoonste manier om **OCR image to JSON** te bereiken zonder een eigen serializer te schrijven.

```csharp
        // Step 4: Convert the OCR result to JSON (includes words, confidence, locations)
        string jsonResult = ocrResult.ToJson();
```

Als je een aangepast schema wilt, kun je over `ocrResult.Words` itereren en je eigen object bouwen, maar voor de meeste scenario’s is de ingebouwde JSON voldoende en al goed gestructureerd.

## Stap 5: JSON naar bestand schrijven

Nu komt het laatste puzzelstukje: het JSON‑payload opslaan. De `File.WriteAllText`‑methode zorgt ervoor dat het bestand atomisch wordt aangemaakt (of overschreven). Zorg dat de doelmap bestaat, anders krijg je een `DirectoryNotFoundException`.

```csharp
        // Step 5: Save the JSON output – this demonstrates write JSON to file
        var jsonPath = @"YOUR_DIRECTORY/invoice.json";
        File.WriteAllText(jsonPath, jsonResult);
```

*Tip:* Als je UTF‑8 met BOM of een andere codering nodig hebt, gebruik dan de overload die een `Encoding`‑argument accepteert.

## Stap 6: Controleer de output

Een snelle `Console.WriteLine` vertelt ons dat het proces succesvol is afgerond. Je kunt het JSON‑bestand ook openen in een viewer om de structuur te bevestigen.

```csharp
        // Step 6: Inform the user that the JSON file has been saved
        Console.WriteLine($"JSON saved to {jsonPath}");
    }
}
```

### Verwachte JSON‑fragment

```json
{
  "Text": "Invoice #12345\nDate: 2025-12-31\nTotal: $250.00",
  "Words": [
    { "Text": "Invoice", "Confidence": 0.98, "Location": { "X": 10, "Y": 15, "Width": 80, "Height": 20 } },
    { "Text": "#12345", "Confidence": 0.96, "Location": { "X": 95, "Y": 15, "Width": 60, "Height": 20 } }
    // … more words …
  ]
}
```

De JSON bevat de locatie van elk woord, wat handig is als je later tekst in een UI wilt markeren.

## Volledig werkend voorbeeld

Hieronder staat het complete, kant‑en‑klare programma. Vervang `YOUR_DIRECTORY` door het daadwerkelijke pad waar je afbeelding zich bevindt.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class JsonExportDemo
{
    static void Main()
    {
        // Step 1: Initialize the OCR engine
        var ocrEngine = new OcrEngine();

        // Step 2: Load the image you want to recognize
        var imagePath = @"YOUR_DIRECTORY/invoice.png";
        var ocrImage = OcrImage.FromFile(imagePath);

        // Step 3: Perform OCR – how to extract text
        var ocrResult = ocrEngine.Recognize(ocrImage);

        // Step 4: Convert the result to JSON (OCR image to JSON)
        string jsonResult = ocrResult.ToJson();

        // Step 5: Write JSON to file – write JSON to file
        var jsonPath = @"YOUR_DIRECTORY/invoice.json";
        File.WriteAllText(jsonPath, jsonResult);

        // Step 6: Verify
        Console.WriteLine($"JSON saved to {jsonPath}");
    }
}
```

Voer het programma uit (`dotnet run` vanuit de projectmap) en je vindt `invoice.json` naast je originele PNG.

## Veelvoorkomende valkuilen & hoe ze te vermijden

| Probleem | Waarom het gebeurt | Oplossing |
|----------|-------------------|-----------|
| **FileNotFoundException** bij het laden van de afbeelding | Typfout in pad of bestand ontbreekt | Gebruik `Path.Combine` en controleer `File.Exists` voordat je `FromFile` aanroept. |
| **Lage confidence‑scores** | Slechte beeldkwaliteit, lage DPI | Pre‑process met `ocrImage.AdjustContrast` of schaal de afbeelding op naar 300 DPI. |
| **JSON‑bestand leeg** | `ocrResult` retourneerde null (engine faalde) | Controleer of het afbeeldingsformaat wordt ondersteund en of de licentie (indien aanwezig) correct is toegepast. |
| **Prestatie‑knelpunt bij grote batches** | `OcrEngine` elke iteratie opnieuw aanmaken | Hergebruik één enkele `OcrEngine`‑instantie voor de hele batch en dispose pas aan het einde. |

## Volgende stappen

Nu je de **c# OCR tutorial** onder de knie hebt, kun je overwegen om:

- **Batch‑verwerking** van een volledige map en de JSON‑bestanden te aggregeren in één database.
- **Integratie** van de output met Azure Cognitive Search voor doorzoekbare PDF’s.
- **Taalondersteuning toe te voegen** door `ocrEngine.Language = OcrLanguage.Spanish` in te stellen (of een andere ondersteunde taal).
- **Post‑processing** van de JSON om tabellen of sleutel‑waarde‑paren te extraheren met reguliere expressies.

Al deze uitbreidingen bouwen voort op de kernconcepten die we hebben behandeld: afbeeldingen laden voor OCR, tekst extraheren, omzetten naar JSON, en die JSON naar schijf schrijven.

### Conclusie

In deze **c# OCR tutorial** hebben we elke stap doorlopen die nodig is om **image for OCR te laden**, **tekst te extraheren**, het resultaat te transformeren naar een **OCR image to JSON** payload, en uiteindelijk **JSON naar bestand te schrijven**. Het volledige code‑voorbeeld staat klaar om in elk .NET‑project te worden geplakt, en de toelichtingen geven je de context die je nodig hebt om de oplossing aan te passen aan real‑world scenario’s.

Probeer het met je eigen set bonnen of facturen—pas de beeld‑pre‑processing aan, experimenteer met verschillende talen, en zie hoe de JSON‑output groeit. Als je ergens tegenaan loopt, raadpleeg dan de tabel met valkuilen of laat een commentaar achter. Veel programmeerplezier!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}