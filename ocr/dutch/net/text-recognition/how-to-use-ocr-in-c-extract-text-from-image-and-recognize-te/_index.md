---
category: general
date: 2026-02-13
description: Hoe OCR te gebruiken in C# om tekst uit een afbeelding te extraheren,
  tekst te herkennen van een foto of JPG, en OCR op een afbeelding uit te voeren zonder
  internet.
draft: false
keywords:
- how to use OCR
- extract text from image
- recognize text from photo
- recognize text from jpg
- run OCR on image
language: nl
og_description: Hoe OCR in C# te gebruiken om tekst uit een afbeelding te extraheren,
  tekst van een foto te herkennen en OCR op een afbeelding uit te voeren met een compleet,
  uitvoerbaar voorbeeld.
og_title: Hoe OCR in C# te gebruiken – Tekst uit afbeelding extraheren
tags:
- OCR
- C#
- Image Processing
title: Hoe OCR te gebruiken in C# – Tekst extraheren uit afbeelding en tekst herkennen
  op foto
url: /nl/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-image-and-recognize-te/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe OCR te gebruiken in C# – Tekst extraheren uit afbeelding en tekst herkennen van foto

Heb je je ooit afgevraagd **hoe je OCR kunt gebruiken** om woorden uit een screenshot, een gescande bon of een willekeurige foto die je met je telefoon hebt gemaakt te halen? Je bent niet de enige. In veel real‑world apps moeten we afbeeldingen omzetten naar doorzoekbare tekst, en dit lokaal doen—zonder een onstabiele internetverbinding—kan aanvoelen als een puzzel.

Daarom laat deze gids je stap‑voor‑stap zien hoe je **tekst uit afbeelding kunt extraheren** met een C# OCR‑engine, en behandelt ook hoe je **tekst van foto kunt herkennen**, **tekst van JPG kunt herkennen**, en **OCR op afbeelding kunt uitvoeren** op bestanden die direct op je schijf staan. Aan het einde heb je een compleet, kant‑klaar programma dat direct werkt.

## Wat je zult leren

- Hoe je een OCR‑engine configureert voor Vereenvoudigd Chinees (of elke andere taal die je toevoegt).  
- De exacte code die nodig is om **resources te laden** vanuit een lokale map—geen netwerkverzoeken nodig.  
- Hoe je **tekst van foto** kunt herkennen in bestanden zoals JPEG, PNG of BMP.  
- Tips voor het omgaan met veelvoorkomende randgevallen zoals ontbrekende modelbestanden of niet‑ondersteunde afbeeldingsformaten.  
- Een volledig, uitvoerbaar voorbeeld dat je in Visual Studio kunt plakken en direct resultaten ziet.

### Vereisten

- .NET 6.0 of later (de hier gebruikte API richt zich op .NET Standard 2.0, dus oudere versies werken ook).  
- Basiskennis van C# en Visual Studio (of een andere IDE naar keuze).  
- De OCR‑bibliotheek die je gebruikt (de snippet gaat uit van een fictieve `OcrEngine`‑klasse die met taalmodellen wordt geleverd).  
- Een map met de benodigde taalmodelbestanden—beschouw dit als het “brein” dat de engine gebruikt om Chinese tekens te lezen.

> **Pro tip:** Als je de Chinese modelbestanden nog niet hebt, download ze dan één keer van de website van de leverancier en plaats ze in een map zoals `C:\OcrResources`. De engine hoeft daarna nooit meer online te gaan.

---

![Diagram showing OCR process on a photo](path/to/ocr-diagram.png "Diagram van OCR‑proces op een foto")

## Hoe OCR te gebruiken: De engine instellen

Het eerste wat je nodig hebt is een instantie van de OCR‑engine, geconfigureerd voor de taal die je wilt. In deze tutorial richten we ons op **Vereenvoudigd Chinees**, maar het vervangen van `OcrLanguage.ChineseSimplified` door `OcrLanguage.English` (of een andere enum‑waarde) is slechts één regel code.

```csharp
using System;
using YourOcrLibrary;   // Replace with the actual namespace of your OCR SDK

// Step 1: Create and configure the OCR engine for Simplified Chinese
var ocrEngine = new OcrEngine
{
    // Primary keyword appears here naturally
    Language = OcrLanguage.ChineseSimplified,

    // Point to a folder that already contains the Chinese model files
    ResourceFolder = @"C:\OcrResources"
};
```

**Waarom dit belangrijk is:**  
Het instellen van de eigenschap `Language` vertelt de engine welke tekenset verwacht moet worden. `ResourceFolder` is de map waar de engine zoekt naar de neurale‑netwerk‑gewichten en taaldictionaries—beschouw het als het geheugen van het brein. Als je naar de verkeerde map wijst, gooit de engine een `FileNotFoundException` en zit je vast.

## Tekst extraheren uit afbeelding – Resources laden

Voordat de engine iets kan lezen, moet je die modelbestanden in het geheugen laden. Deze stap is **cruciaal** omdat hij een netwerkverzoek bij elke afbeelding voorkomt.

```csharp
// Step 2: Load the language resources from the specified folder (no internet required)
try
{
    ocrEngine.LoadResources();
    Console.WriteLine("Resources loaded successfully.");
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Failed to load OCR resources: {ex.Message}");
    // In a real app you might fallback to a default language or abort gracefully
}
```

**Wat kan er misgaan?**  
Als het mappad onjuist is of de bestanden corrupt, zal `LoadResources()` een uitzondering veroorzaken. Het `try/catch`‑blok hierboven laat zien hoe je fouten elegant afhandelt—iets wat je vaak nodig hebt in productie.

## Tekst herkennen van foto – OCR uitvoeren

Nu het leuke deel: een afbeeldingsbestand aan de engine geven en de herkende tekst terugkrijgen. Dit is de kern van **OCR op afbeelding**‑scenario’s, of de afbeelding nu een JPEG, PNG of zelfs een BMP is.

```csharp
// Step 3: Recognize text from an image file
string imagePath = @"C:\OcrResources\photo.jpg";

try
{
    var recognitionResult = ocrEngine.RecognizeImage(imagePath);
    Console.WriteLine("=== OCR Output ===");
    Console.WriteLine(recognitionResult.Text);
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Error during OCR processing: {ex.Message}");
}
```

De methode `RecognizeImage` retourneert een `RecognitionResult` (of hoe jouw SDK het ook noemt) die doorgaans bevat:

- `Text` – de platte‑tekst transcriptie.  
- `Confidence` – een numerieke score die aangeeft hoe zeker de engine is over elke regel.  
- `BoundingBoxes` – optionele coördinaten van waar elk woord zich op de foto bevindt.

**Waarom je om confidence zou kunnen geven:**  
Als je een data‑invoertool bouwt, kun je een drempelwaarde (bijv. 0.85) instellen en de gebruiker laten bevestigen bij lage‑confidence regels. Dat verbetert de algehele nauwkeurigheid drastisch.

## Tekst herkennen van JPG – Omgaan met verschillende formaten

Veel ontwikkelaars gaan ervan uit dat OCR alleen werkt met PNG’s, maar moderne engines verwerken **JPG**‑bestanden prima. Het enige obstakel is dat JPEG‑compressie artefacten kan introduceren die het model verwarren.

```csharp
// Bonus: Recognize text from a JPG with optional preprocessing
string jpgPath = @"C:\OcrResources\scanned_doc.jpg";

// Optional: use a simple image‑preprocess step to improve accuracy
var preprocessed = ImageHelper.DenoiseAndDeskew(jpgPath); // pseudo‑method
var result = ocrEngine.RecognizeImage(preprocessed);
Console.WriteLine($"Detected text ({result.Confidence:P0} confidence):");
Console.WriteLine(result.Text);
```

Als je geen `DenoiseAndDeskew`‑helper hebt, bieden veel bibliotheken (bijv. OpenCvSharp) die functies al aan. De belangrijkste les is: **OCR op afbeelding**‑bestanden uitvoeren na een kleine opschoning als ze van een scanner of telefooncamera komen.

## OCR op afbeelding uitvoeren – Tips, randgevallen en best practices

### 1. Geheugenbeheer
Het laden van grote taalmodellen kan honderden megabytes verbruiken. Verwijder de engine wanneer je klaar bent:

```csharp
ocrEngine.Dispose(); // or using statement if the SDK implements IDisposable
```

### 2. Batchverwerking
Als je tientallen foto’s moet verwerken, laad de resources één keer en loop vervolgens:

```csharp
string[] files = Directory.GetFiles(@"C:\BatchPhotos", "*.jpg");
foreach (var file in files)
{
    var res = ocrEngine.RecognizeImage(file);
    File.WriteAllText(Path.ChangeExtension(file, ".txt"), res.Text);
}
```

### 3. Multi‑taal scenario’s
Je kunt talen dynamisch wisselen door `ocrEngine.Language` opnieuw toe te wijzen en `LoadResources()` opnieuw aan te roepen. Let wel op de extra laadtijd.

### 4. Lege resultaten afhandelen
Soms retourneert de engine een lege string. Dat betekent meestal dat de afbeelding te onscherp is of dat de tekstkleur opgaat in de achtergrond. Een snelle controle:

```csharp
if (string.IsNullOrWhiteSpace(recognitionResult.Text))
{
    Console.WriteLine("No text detected – consider increasing image contrast.");
}
```

### 5. Veiligheidsaspecten
Voer nooit door gebruikers geüploade bestanden direct in de OCR‑engine zonder validatie. Controleer minimaal de bestandsextensie en -grootte, en overweeg een malware‑scan.

---

## Volledig werkend voorbeeld

Hieronder vind je een enkel, zelf‑voorzienend programma dat je kunt kopiëren naar een nieuw Console‑App‑project. Het demonstreert **hoe je OCR gebruikt**, **tekst uit afbeelding extraheren**, **tekst van foto herkennen**, **tekst van JPG herkennen**, en **OCR op afbeelding uitvoeren**—alles in één keer.

```csharp
// File: Program.cs
using System;
using System.IO;
using YourOcrLibrary; // Replace with actual namespace

namespace OcrDemo
{
    class Program
    {
        static void Main()
        {
            // ------------------------------
            // 1️⃣ Configure the OCR engine
            // ------------------------------
            var ocrEngine = new OcrEngine
            {
                Language = OcrLanguage.ChineseSimplified,
                ResourceFolder = @"C:\OcrResources"
            };

            // Load language resources (no internet needed)
            try
            {
                ocrEngine.LoadResources();
                Console.WriteLine("Resources loaded.");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"Failed to load resources: {ex.Message}");
                return;
            }

            // -------------------------------------------------
            // 2️⃣ Recognize text from a photo (JPG in this case)
            // -------------------------------------------------
            string imagePath = @"C:\OcrResources\photo.jpg";

            if (!File.Exists(imagePath))
            {
                Console.Error.WriteLine($"Image not found: {imagePath}");
                return;
            }

            try
            {
                var result = ocrEngine.RecognizeImage(imagePath);
                Console.WriteLine("\n=== OCR Output ===");
                Console.WriteLine(result.Text);
                Console.WriteLine($"\nConfidence: {result.Confidence:P2}");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"OCR error: {ex.Message}");
            }

            // Clean up
            ocrEngine.Dispose();
        }
    }
}
```

**Verwachte output (voorbeeld):**

```
Resources loaded.

=== OCR Output ===
中华人民共和国
北京
2026年02月13日

Confidence: 92.45%
```

Je eigen tekst zal verschillen afhankelijk van de inhoud van de afbeelding, maar je zou een blok Unicode‑tekens moeten zien die naar de console worden geschreven, samen met een confidence‑percentage.

---

## Conclusie

We hebben stap voor stap **hoe je OCR gebruikt** in C# doorgenomen—from het configureren van de engine, het laden van taalresources, tot het **herkennen van tekst van foto** of **JPG**‑bestanden zonder ooit internet te gebruiken. Door de bovenstaande stappen te volgen kun je **tekst uit afbeelding**‑bestanden extraheren, **OCR op afbeelding**‑assets uitvoeren, en de meest voorkomende valkuilen vermijden die beginners vaak tegenkomen.

Klaar voor de volgende uitdaging? Probeer de engine een PDF‑pagina te laten verwerken die eerst naar een afbeelding is geconverteerd, of experimenteer met een ander taalpakket om te zien hoe de confidence‑scores verschuiven. Je zou

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}