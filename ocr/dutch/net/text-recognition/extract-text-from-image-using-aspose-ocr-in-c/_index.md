---
category: general
date: 2026-08-09
description: Tekst extraheren uit een afbeelding met Aspose OCR in C#. Leer hoe je
  een afbeelding laadt voor OCR, de OCR-taal instelt, de afbeelding OCR verwerkt en
  efficiënt afbeelding naar tekst converteert.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- extract text from image
- convert image to text
- load image for ocr
- process image ocr
- set ocr language
language: nl
lastmod: 2026-08-09
og_description: Tekst extraheren uit afbeelding met Aspose OCR in C#. Deze tutorial
  laat zien hoe je een afbeelding laadt voor OCR, de OCR-taal instelt, de afbeelding
  OCR verwerkt en de afbeelding naar tekst converteert in een paar regels code.
og_image_alt: Screenshot of C# console output showing extracted text from an image
  using Aspose OCR
og_title: Tekst extraheren uit afbeelding met Aspose OCR – C#‑gids
schemas:
- author: Aspose
  dateModified: '2026-08-09'
  description: Extract text from image with Aspose OCR in C#. Learn how to load image
    for OCR, set OCR language, process image OCR, and convert image to text efficiently.
  headline: Extract text from image using Aspose OCR in C#
  type: TechArticle
- description: Extract text from image with Aspose OCR in C#. Learn how to load image
    for OCR, set OCR language, process image OCR, and convert image to text efficiently.
  name: Extract text from image using Aspose OCR in C#
  steps:
  - name: '**Create an OCR engine instance** – The `OcrEngine` encapsulates all OCR
      functionality. Disposing it promptly frees native resources, which is critical
      for long‑running services.'
    text: '**Create an OCR engine instance** – The `OcrEngine` encapsulates all OCR
      functionality. Disposing it promptly frees native resources, which is critical
      for long‑running services.'
  - name: '**Set OCR language** – Selecting the correct language module dramatically
      improves accuracy. Aspose provides over 30 language packs; the default is English.
      The example uses Cyrillic to demonstrate a non‑Latin script.'
    text: '**Set OCR language** – Selecting the correct language module dramatically
      improves accuracy. Aspose provides over 30 language packs; the default is English.
      The example uses Cyrillic to demonstrate a non‑Latin script.'
  - name: '**Load image for OCR** – The engine works with an `ImageStream`. Supplying
      a high‑resolution image (≥300 dpi) reduces misrecognition, especially for complex
      scripts.'
    text: '**Load image for OCR** – The engine works with an `ImageStream`. Supplying
      a high‑resolution image (≥300 dpi) reduces misrecognition, especially for complex
      scripts.'
  - name: '**Process image OCR** – This is where the heavy lifting occurs. The method
      returns an `OcrResult` containing the extracted text, confidence scores, and
      optional layout data.'
    text: '**Process image OCR** – This is where the heavy lifting occurs. The method
      returns an `OcrResult` containing the extracted text, confidence scores, and
      optional layout data.'
  - name: '**Convert image to text** – `result.Text` is a plain `string`. You can
      write it to a file, feed it into a search index, or pass it to downstream NLP
      pipelines.'
    text: '**Convert image to text** – `result.Text` is a plain `string`. You can
      write it to a file, feed it into a search index, or pass it to downstream NLP
      pipelines.'
  - name: Instantiates `OcrEngine`.
    text: Instantiates `OcrEngine`.
  - name: '**Sets OCR language** to Cyrillic (or any language you choose).'
    text: '**Sets OCR language** to Cyrillic (or any language you choose).'
  - name: '**Loads image for OCR** from disk.'
    text: '**Loads image for OCR** from disk.'
  - name: '**Processes image OCR** to obtain the textual result.'
    text: '**Processes image OCR** to obtain the textual result.'
  - name: '**Converts image to text** and prints it.'
    text: '**Converts image to text** and prints it.'
  type: HowTo
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Tekst uit afbeelding extraheren met Aspose OCR in C#
url: /nl/net/text-recognition/extract-text-from-image-using-aspose-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tekst extraheren uit afbeelding met Aspose OCR in C#

Als je **tekst uit een afbeelding moet extraheren** in een .NET‑applicatie, leidt deze gids je door een complete, kant‑klaar oplossing. Je ziet hoe je **een afbeelding laadt voor OCR**, het juiste taalmodule kiest, de OCR‑engine uitvoert en uiteindelijk **afbeelding naar tekst converteert** met slechts een paar regels C#.

De tutorial behandelt alles wat nodig is om betrouwbare resultaten te krijgen met Aspose.OCR, inclusief veelvoorkomende valkuilen zoals niet‑ondersteunde afbeeldingsformaten en taalspecifieke nuances. Aan het einde heb je een zelfstandige applicatie die de herkende tekst naar de console schrijft.

## Wat je zult bereiken

* Een afbeeldingsbestand laden in de Aspose OCR‑engine.  
* **OCR‑taal instellen** (Cyrillisch in het voorbeeld, maar elke ondersteunde taal werkt).  
* **Afbeelding OCR verwerken** en de tekstuele weergave verkrijgen.  
* **Afbeelding naar tekst converteren** en weergeven, klaar voor verdere verwerking of opslag.  

**Prerequisites**

* .NET 6.0 of later (de code werkt ook op .NET Framework 4.6+).  
* Visual Studio 2022 (of elke IDE die C# ondersteunt).  
* Aspose.OCR NuGet‑package (`Install-Package Aspose.OCR`).  

---

## Tekst uit afbeelding extraheren – volledige code‑doorloop

Hieronder staat het complete, uitvoerbare programma. Kopieer het naar een nieuw console‑project en vervang `YOUR_DIRECTORY/sample_cyrillic.jpg` door het pad naar jouw eigen afbeelding.

```csharp
using System;
using Aspose.OCR;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create an OCR engine instance.
            // The using block ensures the engine is disposed correctly.
            using (var engine = new OcrEngine())
            {
                // Step 2: Set OCR language.
                // Change OcrLanguage.Cyrillic to any other supported language,
                // e.g., OcrLanguage.English, OcrLanguage.Chinese, OcrLanguage.Hindi.
                engine.Language = OcrLanguage.Cyrillic;

                // Step 3: Load image for OCR.
                // ImageStream.FromFile reads the image from disk.
                // Supported formats: JPEG, PNG, BMP, TIFF, GIF.
                engine.Image = ImageStream.FromFile("YOUR_DIRECTORY/sample_cyrillic.jpg");

                // Step 4: Process image OCR.
                // The Process method runs the recognition engine and returns an OcrResult.
                var result = engine.Process();

                // Step 5: Convert image to text.
                // The recognized text is available via result.Text.
                Console.WriteLine("=== Recognized Text ===");
                Console.WriteLine(result.Text);
            }
        }
    }
}
```

### Waarom elke stap belangrijk is

1. **Maak een OCR‑engine‑instantie** – De `OcrEngine` omsluit alle OCR‑functionaliteit. Het tijdig vrijgeven ervan maakt native resources vrij, wat cruciaal is voor langdurige services.
2. **Stel OCR‑taal in** – Het kiezen van de juiste taalmodule verbetert de nauwkeurigheid drastisch. Aspose biedt meer dan 30 taalpakketten; standaard is Engels. Het voorbeeld gebruikt Cyrillisch om een niet‑Latijns schrift te demonstreren.
3. **Laad afbeelding voor OCR** – De engine werkt met een `ImageStream`. Het leveren van een afbeelding met hoge resolutie (≥300 dpi) vermindert fouten, vooral bij complexe scripts.
4. **Verwerk afbeelding OCR** – Hier gebeurt het zware werk. De methode retourneert een `OcrResult` met de geëxtraheerde tekst, vertrouwensscores en optionele lay-outgegevens.
5. **Converteer afbeelding naar tekst** – `result.Text` is een gewone `string`. Je kunt deze naar een bestand schrijven, invoeren in een zoekindex, of doorgeven aan downstream NLP‑pijplijnen.

---

## Afbeelding laden voor OCR

De methode `ImageStream.FromFile` ondersteunt gangbare rasterformaten. Als je afbeeldingen ontvangt als byte‑arrays (bijv. van een web‑API), gebruik dan `ImageStream.FromBytes(byte[])` in plaats daarvan:

```csharp
byte[] imageBytes = File.ReadAllBytes("path/to/image.png");
engine.Image = ImageStream.FromBytes(imageBytes);
```

**Pro tip:** Controleer altijd of de afbeelding niet corrupt is voordat je deze aan de engine doorgeeft. Een snelle `try { Image.FromFile(...); } catch { ... }`‑guard voorkomt runtime‑exceptions.

---

## OCR‑taal instellen

Aspose.OCR wordt geleverd met taalpakketten die je tijdens runtime kunt inschakelen. Om alle beschikbare talen weer te geven:

```csharp
foreach (var lang in Enum.GetValues(typeof(OcrLanguage)))
{
    Console.WriteLine(lang);
}
```

Als je meerdere talen in hetzelfde document wilt herkennen, combineer ze dan met de bitwise OR‑operator:

```csharp
engine.Language = OcrLanguage.English | OcrLanguage.Russian;
```

**Edge case:** Het combineren van right‑to‑left (RTL) talen (bijv. Arabisch) met left‑to‑right scripts kan extra lay‑outhantering vereisen. Aspose detecteert de richting automatisch, maar je kunt dit fijn afstellen via `engine.PageSegmentationMode`.

---

## Afbeelding OCR verwerken

De `Process`‑aanroep is synchroon en blokkeert tot de engine klaar is. Voor grote batches of UI‑applicaties kun je de asynchrone overload overwegen:

```csharp
var task = engine.ProcessAsync();
OcrResult result = await task;
```

**Veelvoorkomende valkuil:** Het vergeten om `engine.Image` in te stellen vóór het aanroepen van `Process` veroorzaakt een `InvalidOperationException`. Wijs altijd eerst de afbeelding toe.

---

## Afbeelding naar tekst converteren

De geëxtraheerde string kun je behandelen als elke andere .NET `string`. Bijvoorbeeld, om de output naar een bestand te schrijven:

```csharp
File.WriteAllText("output.txt", result.Text);
```

Als je de regeleinden exact wilt behouden zoals ze in de afbeelding staan, gebruik dan direct `result.Text`. Voor post‑processing (bijv. het verwijderen van extra witruimte) kun je standaard string‑methoden toepassen:

```csharp
string cleaned = result.Text
    .Replace("\r\n", "\n")
    .Trim();
```

---

## Samenvatting van het volledige voorbeeld

Alles samengevoegd doet het programma het volgende:

1. Instantieert `OcrEngine`.
2. **Stelt OCR‑taal in** op Cyrillisch (of elke gewenste taal).
3. **Laadt afbeelding voor OCR** vanaf schijf.
4. **Verwerkt afbeelding OCR** om het tekstresultaat te verkrijgen.
5. **Converteert afbeelding naar tekst** en print het.

Het uitvoeren van het voorbeeld met een duidelijke Cyrillische afbeelding levert een output vergelijkbaar met:

```
=== Recognized Text ===
Пример текста на кириллице
```

Bevat de afbeelding Engelse tekst, wijzig dan simpelweg `engine.Language = OcrLanguage.English;` en dezelfde code zal **tekst uit afbeelding extraheren** correct.

---

## Conclusie

Je weet nu hoe je **tekst uit een afbeelding kunt extraheren** met Aspose OCR in C#. De tutorial behandelde het laden van de afbeelding, het selecteren van de juiste taal, het uitvoeren van het OCR‑proces, en **het converteren van afbeelding naar tekst** voor downstream gebruik.  

Vanaf hier kun je:

* Experimenteren met andere talen (`load image for OCR` → `set OCR language` → `process image OCR`).  
* De OCR‑stap integreren in een grotere pijplijn (bijv. document‑inname, doorzoekbare PDF’s).  
* De prestaties optimaliseren door afbeeldingen te batchen of de asynchrone API te gebruiken.

Verken gerust de Aspose.OCR‑documentatie voor geavanceerde functies zoals aangepaste woordenboeken, paginasegmentatiemodi en OCR‑nauwkeurigheidstuning. Veel programmeerplezier!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids zijn gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑features onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [How to Perform Image Text Extraction from Stream Using Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}