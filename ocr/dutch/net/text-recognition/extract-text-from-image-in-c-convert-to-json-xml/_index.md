---
category: general
date: 2026-04-26
description: Tekst extraheren uit een afbeelding in C# met Aspose.OCR en leer hoe
  je een afbeelding in enkele minuten naar JSON- en XML-formaten kunt converteren.
draft: false
keywords:
- extract text from image
- convert image to json
- convert image to xml
- Aspose OCR C#
- image to JSON C#
- image to XML C#
language: nl
og_description: Haal tekst uit afbeelding in C# met Aspose.OCR. Leer stap voor stap
  hoe je het resultaat direct naar JSON en XML kunt converteren.
og_title: Tekst uit afbeelding extraheren in C# – Converteren naar JSON & XML
tags:
- OCR
- C#
- Aspose
- JSON
- XML
title: Tekst uit afbeelding extraheren in C# – Converteren naar JSON & XML
url: /nl/net/text-recognition/extract-text-from-image-in-c-convert-to-json-xml/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tekst uit afbeelding halen in C# – Omzetten naar JSON & XML

Heb je ooit **tekst uit een afbeelding** moeten halen in een .NET‑project, maar zat je vast bij de vraag “hoe krijg ik die gegevens nu eigenlijk eruit?” Je bent niet de enige. In veel real‑world toepassingen—denk aan factuurverwerking, bon‑scannen of badge‑verificatie—is het ophalen van de ruwe tekens uit een foto de eerste, cruciale stap.  

Het goede nieuws? Met Aspose.OCR kun je dat in een handvol regels doen, en vervolgens direct **afbeelding naar JSON** of **afbeelding naar XML** omzetten voor downstream‑systemen. In deze gids lopen we de volledige, kant‑klaar code door, leggen we uit waarom elk onderdeel belangrijk is, en laten we je een paar trucjes zien om veelvoorkomende valkuilen te vermijden.

---

## Wat je nodig hebt

- **.NET 6+** (elke recente SDK werkt; het voorbeeld richt zich op .NET 6)
- **Aspose.OCR for .NET** NuGet‑package  
  ```bash
  dotnet add package Aspose.OCR
  ```
- Een afbeeldingsbestand (PNG, JPG, etc.) dat afdrukbare tekst bevat; we gebruiken `invoice.png` als voorbeeld.
- Een code‑editor—Visual Studio, VS Code, of Rider—wat je maar prettig vindt.

Dat is alles. Geen extra OCR‑engines, geen externe services, alleen één NuGet‑package.

---

## Stap 1: OCR‑engine instellen – Hoe tekst uit afbeelding te halen

Eerst maken we een `OcrEngine`‑instance aan en wijzen we deze op het afbeeldingsbestand. Deze stap is de basis; zonder een correct geladen afbeelding kan de engine niets herkennen.

```csharp
using Aspose.OCR;
using System.IO;

// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Load the image you want to process
// Replace YOUR_DIRECTORY with the actual folder path
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/invoice.png");

// Optional: verify the image was loaded
if (ocrEngine.Image == null)
{
    throw new FileNotFoundException("Image not found. Check the path and filename.");
}
```

**Waarom dit belangrijk is:**  
- `OcrEngine` omvat alle low‑level beeldvoorbewerking (binarisatie, deskewing).  
- Het laden van de afbeelding via `ImageStream.FromFile` zorgt ervoor dat de engine de exacte bytes leest, waardoor DPI en kleurdiepte behouden blijven—beide kunnen de herkenningsnauwkeurigheid beïnvloeden.  

> **Pro tip:** Als je bronafbeeldingen in een stream zitten (bijv. geüpload via een web‑API), gebruik dan `ImageStream.FromStream(yourStream)` in plaats van `FromFile`.

---

## Stap 2: De engine vertellen welke taal verwacht wordt – tekst uit afbeelding nauwkeurig halen

Aspose.OCR ondersteunt veel alfabetten. Het specificeren van de juiste taal beperkt de tekenset en verhoogt de nauwkeurigheid.

```csharp
// Set the language; Latin covers English, French, German, etc.
ocrEngine.Language = Language.Latin;
```

**Waarom:**  
Wanneer je `Language.Latin` instelt, negeert de OCR‑engine Cyrillische of Aziatische glyphs, waardoor valse positieven afnemen. Als je later documenten met meerdere talen moet verwerken, kun je overschakelen naar `Language.Multilingual` of talen combineren.

---

## Stap 3: Het herkenningsproces uitvoeren – tekst uit afbeelding in één stap

Nu herkennen we daadwerkelijk de tekst. De `Recognize`‑methode retourneert een `RecognitionResult`‑object dat de ruwe tekst, confidence‑scores en zelfs layout‑data bevat.

```csharp
// Perform OCR
RecognitionResult recognitionResult = ocrEngine.Recognize();

// Quick sanity check
if (recognitionResult == null || string.IsNullOrWhiteSpace(recognitionResult.Text))
{
    Console.WriteLine("No text was detected. Verify the image quality.");
    return;
}

// Print the raw extracted text to the console
Console.WriteLine("=== Extracted Text ===");
Console.WriteLine(recognitionResult.Text);
```

**Waarom:**  
Eén keer `Recognize` aanroepen is voldoende omdat de engine intern preprocessing, segmentatie en karakterclassificatie uitvoert. De `Text`‑eigenschap geeft je een platte string‑representatie, perfect voor logging of snelle validatie.

---

## Stap 4: Het resultaat naar JSON omzetten – afbeelding gemakkelijk naar json converteren

Veel moderne services geven de voorkeur aan JSON‑payloads. Aspose.OCR biedt een handige `ToJson`‑methode die het volledige `RecognitionResult` serialiseert, inclusief confidence‑waarden en bounding boxes.

```csharp
// Serialize the result to JSON
string jsonResult = recognitionResult.ToJson();

// Save the JSON to a file
File.WriteAllText("YOUR_DIRECTORY/invoice.json", jsonResult);

Console.WriteLine("JSON file saved at YOUR_DIRECTORY/invoice.json");
```

**Waarom je JSON wilt:**  
- **Interoperabiliteit:** Front‑end apps (React, Angular) kunnen de JSON direct consumeren.  
- **Debuggen:** De JSON bevat per‑karakter confidence, zodat je woorden met lage zekerheid kunt markeren voor handmatige controle.  

> **Edge case:** Als je downstream‑systeem alleen de platte tekst nodig heeft, kun je `recognitionResult.Text` extraheren en in een eigen JSON‑object plaatsen in plaats van de volledige Aspose‑payload.

---

## Stap 5: Het resultaat naar XML omzetten – afbeelding naar xml voor legacy‑systemen

Sommige organisaties vertrouwen nog steeds op XML‑schema’s voor gegevensuitwisseling. De `ToXml`‑methode werkt gelijk aan `ToJson`, maar levert XML op.

```csharp
// Serialize the result to XML
string xmlResult = recognitionResult.ToXml();

// Save the XML to a file
File.WriteAllText("YOUR_DIRECTORY/invoice.xml", xmlResult);

Console.WriteLine("XML file saved at YOUR_DIRECTORY/invoice.xml");
```

**Waarom XML:**  
- **Schema‑validatie:** Je kunt een XSD definiëren die overeenkomt met de structuur die Aspose genereert, waardoor contract‑compliance gegarandeerd is.  
- **Integratie:** Oudere ERP‑ of document‑managementsystemen parseren vaak XML out‑of‑the‑box.

---

## Volledig werkend voorbeeld – Alles‑in‑één code

Hieronder vind je het complete programma dat alles samenbrengt. Kopieer‑en‑plak het in een nieuw console‑project (`dotnet new console`) en voer het uit.

```csharp
using Aspose.OCR;
using System;
using System.IO;

namespace ImageOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Initialize OCR engine and load the image
            // -------------------------------------------------
            OcrEngine ocrEngine = new OcrEngine();
            // Adjust the path to point at your PNG/JPG file
            string imagePath = "YOUR_DIRECTORY/invoice.png";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            if (ocrEngine.Image == null)
            {
                Console.WriteLine($"Unable to load image at {imagePath}");
                return;
            }

            // -------------------------------------------------
            // Step 2: Specify language (Latin for most European scripts)
            // -------------------------------------------------
            ocrEngine.Language = Language.Latin;

            // -------------------------------------------------
            // Step 3: Run OCR and get the result
            // -------------------------------------------------
            RecognitionResult result = ocrEngine.Recognize();

            if (result == null || string.IsNullOrWhiteSpace(result.Text))
            {
                Console.WriteLine("No text detected – check image quality or language setting.");
                return;
            }

            Console.WriteLine("=== Extracted Text ===");
            Console.WriteLine(result.Text);
            Console.WriteLine();

            // -------------------------------------------------
            // Step 4: Convert to JSON (convert image to json)
            // -------------------------------------------------
            string json = result.ToJson();
            string jsonPath = "YOUR_DIRECTORY/invoice.json";
            File.WriteAllText(jsonPath, json);
            Console.WriteLine($"JSON output written to {jsonPath}");

            // -------------------------------------------------
            // Step 5: Convert to XML (convert image to xml)
            // -------------------------------------------------
            string xml = result.ToXml();
            string xmlPath = "YOUR_DIRECTORY/invoice.xml";
            File.WriteAllText(xmlPath, xml);
            Console.WriteLine($"XML output written to {xmlPath}");
        }
    }
}
```

**Verwachte output (console):**

```
=== Extracted Text ===
Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
...

JSON file saved at YOUR_DIRECTORY/invoice.json
XML file saved at YOUR_DIRECTORY/invoice.xml
```

De JSON‑ en XML‑bestanden bevatten een rijkere structuur, bijvoorbeeld:

```json
{
  "Text": "Invoice #12345\nDate: 2024‑03‑15\nTotal: $1,250.00",
  "Confidence": 0.96,
  "Blocks": [
    { "Text": "Invoice #12345", "Confidence": 0.98, "Rectangle": { "X": 12, "Y": 30, "Width": 200, "Height": 20 } },
    ...
  ]
}
```

```xml
<RecognitionResult>
  <Text>Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00</Text>
  <Confidence>0.96</Confidence>
  <Blocks>
    <Block>
      <Text>Invoice #12345</Text>
      <Confidence>0.98</Confidence>
      <Rectangle X="12" Y="30" Width="200" Height="20"/>
    </Block>
    ...
  </Blocks>
</RecognitionResult>
```

---

## Veelgestelde vragen & randgevallen

### Wat als de afbeelding onscherp of gedraaid is?
Aspose.OCR deskewt de meeste afbeeldingen automatisch, maar bij extreme gevallen kun je vooraf verwerken met `ocrEngine.Image = ImageProcessor.Deskew(ocrEngine.Image)`. Een beetje contrast verhogen (`ImageProcessor.AdjustContrast`) kan ook de confidence‑score verbeteren.

### Kan ik tekst uit PDF’s halen?
Ja—zet elke PDF‑pagina eerst om naar een afbeelding (bijv. met Aspose.PDF of een gratis bibliotheek zoals PDFium) en voer die afbeeldingen vervolgens door dezelfde OCR‑flow.

### Hoe ga ik om met meerdere talen in één document?
Stel `ocrEngine.Language = Language.Multilingual;` of combineer specifieke talen:

```csharp
ocrEngine.Language = Language.English | Language.French | Language.German;
```

Wees je ervan bewust dat bredere taalkolommen de herkenningsnauwkeurigheid kunnen beïnvloeden.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}