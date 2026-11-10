---
category: general
date: 2026-04-29
description: hoe je een afbeelding rechtzet en de OCR-nauwkeurigheid verbetert met
  Aspose OCR – leer ruis te verwijderen, het contrast van de afbeelding te verhogen
  en tekst uit afbeeldingen te extraheren.
draft: false
keywords:
- how to deskew image
- remove noise from image
- boost image contrast
- extract text from image
- improve ocr accuracy
language: nl
og_description: how to deskew image and improve OCR accuracy. This tutorial shows
  how to remove noise from image, boost image contrast, and extract text from image
  using Aspose OCR.
og_title: hoe een afbeelding rechtzetten – Complete Aspose OCR-gids
tags:
- Aspose OCR
- C#
- Image preprocessing
title: Hoe een afbeelding rechtzetten – Aspose OCR-preprocessengids
url: /nl/net/ocr-optimization/how-to-deskew-image-aspose-ocr-preprocessing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# hoe afbeelding rechtzetten – Complete Aspose OCR-gids

Heb je je ooit afgevraagd **hoe je een afbeelding rechtzet** voordat je deze aan een OCR‑engine voert? Je bent niet de enige. Een scheve scan of een foto die onder een hoek is genomen, kan de teksterkenning verstoren, waardoor je een onsamenhangende output krijgt.  

In deze tutorial lopen we een volledige, end‑to‑end oplossing door die niet alleen **hoe je een afbeelding rechtzet**, maar ook **ruis uit een afbeelding verwijdert**, **beeldcontrast verhoogt**, en uiteindelijk **tekst uit een afbeelding extraheert** met Aspose OCR. Aan het einde zie je hoe je **OCR‑nauwkeurigheid verbetert** zonder door de documentatie te hoeven speuren.

> **Wat je krijgt:** een kant‑klaar C# console‑applicatie, een duidelijke uitleg van elke preprocessing‑stap, en een reeks praktische tips die je kunt copy‑pasten in je eigen projecten.

## Vereisten

- .NET 6.0 of later (de code werkt ook met .NET Core en .NET Framework)  
- Aspose.OCR NuGet‑pakket (`Install-Package Aspose.OCR`)  
- Een voorbeeldafbeelding die scheef, ruisachtig of laag‑contrast is (bijv. `skewed_noisy.jpg`)  
- Visual Studio, VS Code, of elke C#‑editor die je verkiest  

Er zijn geen extra native libraries nodig – Aspose regelt alles in‑process.

---

## Hoe een afbeelding rechtzetten met Aspose OCR

Het eerste dat we nodig hebben is een deskew‑filter dat de rotatiehoek corrigeert. Aspose OCR wordt geleverd met `FilterDeskew`, die de tekstbaselines analyseert en de bitmap dienovereenkomstig roteert.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;

class PreprocessDemo
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine – this is the core object that will later recognize text.
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Build an image‑processing pipeline.
        //    The order matters: deskew → denoise → contrast boost.
        ImageProcessingPipeline processingPipeline = new ImageProcessingPipeline();
        processingPipeline.Add(new FilterDeskew());          // ✅ how to deskew image
        processingPipeline.Add(new FilterDenoise());         // ✅ remove noise from image
        processingPipeline.Add(new FilterContrastBoost());   // ✅ boost image contrast

        // 3️⃣ Load your source picture.
        var sourceImage = OcrEngine.LoadImage(@"YOUR_DIRECTORY/skewed_noisy.jpg");

        // 4️⃣ Apply the pipeline – the image is now straight, cleaner, and sharper.
        var processedImage = processingPipeline.Apply(sourceImage);

        // 5️⃣ Run OCR on the cleaned‑up bitmap.
        var ocrResult = ocrEngine.Recognize(processedImage);

        // 6️⃣ Print the extracted text.
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Waarom we beginnen met rechtzetten:**  
Als de tekstregels niet horizontaal zijn, zal de OCR‑engine schuine tekens interpreteren als andere glyphs, waardoor **OCR‑nauwkeurigheid** drastisch daalt. Rechtzetten brengt de baselines op één lijn, waardoor de recognizer een schoon canvas krijgt.

> *Pro tip:* Als je de rotatiehoek van tevoren kent (bijv. alle scans staan 90° scheef), kun je het filter overslaan en handmatig roteren – dat levert een kleine prestatie‑winst op.

---

## Ruis uit een afbeelding verwijderen – De scan schoonmaken

Ruis verschijnt als willekeurige zwarte of witte vlekjes (het klassieke “zout‑en‑peper” patroon) en kan karaktersegmentatie verwarren. `FilterDenoise` past een medianfilter toe dat deze gladstrijkt terwijl randen behouden blijven.

```csharp
// Inside the pipeline we already added FilterDenoise.
// If you need a custom strength, you can instantiate it like:
var denoise = new FilterDenoise { Strength = 2 }; // 1‑3 are typical values
processingPipeline.Add(denoise);
```

**Wanneer de sterkte aan te passen:**  
- **Strength = 1** – Lichte korrel, snelle verwerking.  
- **Strength = 3** – Zeer ruisende scans (bijv. gefaxte documenten).  

Het te sterk verhogen van de sterkte kan dunne streken vervagen, wat **OCR‑nauwkeurigheid** kan *schaden*. Test een paar waarden op een representatieve monster.

---

## Beeldcontrast verhogen – Zwakke tekens accentueren

Laag‑contrast afbeeldingen (denk aan vervaagde bonnen) zorgen er vaak voor dat de OCR‑engine lichte glyphs mist. `FilterContrastBoost` strekt het histogram uit zodat donkere pixels donkerder worden en lichte pixels lichter.

```csharp
var contrast = new FilterContrastBoost { ContrastLevel = 1.5f }; // 1.0 = no change
processingPipeline.Add(contrast);
```

**Waarom contrast belangrijk is:**  
Hoger contrast verbetert de signaal‑naar‑ruis‑verhouding, waardoor het voor Aspose’s neurale recognizer makkelijker wordt om “I” van “l” te onderscheiden. Over‑boosten kan echter de afbeelding verzadigen, waardoor gladde overgangen veranderen in harde randen die op artefacten lijken. Streef naar een balans; 1,5‑2,0 is een goed startpunt.

---

## Tekst uit een afbeelding extraheren – De laatste OCR‑stap

Nu de afbeelding recht, schoon en levendig is, kan de OCR‑engine zijn werk doen. De `Recognize`‑methode retourneert een `OcrResult`‑object dat de ruwe tekst, confidence‑scores en zelfs begrenzings‑boxen bevat indien nodig.

```csharp
var ocrResult = ocrEngine.Recognize(processedImage);
Console.WriteLine(ocrResult.Text);
```

**Voorbeeldoutput** (ervan uitgaande dat de bronafbeelding “Invoice #12345” bevat):

```
=== OCR Output ===
Invoice #12345
Date: 04/28/2026
Total: $1,234.56
```

Als je ontbrekende tekens ziet, controleer dan de preprocessing‑pipeline opnieuw – misschien heeft de afbeelding nog een sterkere denoise of een ander contrastniveau nodig.  

> *Veelgestelde vraag:* “Wat als ik een andere taal dan Engels moet herkennen?”  
> Stel gewoon `ocrEngine.Language = Language.English;` in op een andere ondersteunde taal (bijv. `Language.French`). De preprocessing‑stappen blijven hetzelfde.

---

## OCR‑nauwkeurigheid verbeteren – Extra aanpassingen

Zelfs met een perfecte pipeline kunnen een paar extra instellingen **OCR‑nauwkeurigheid** verder verbeteren:

| Tip | Wanneer te gebruiken | Hoe |
|-----|----------------------|-----|
| **Binary Thresholding** | Zeer donkere of zeer lichte scans | `processingPipeline.Add(new FilterBinarize());` |
| **Resize Image** | Kleine lettergroottes (<10 pt) | `processedImage = OcrEngine.Resize(processedImage, 2.0);` |
| **Specify Character Set** | Bekende alfabet (alleen cijfers, etc.) | `ocrEngine.Characters = "0123456789";` |
| **Multi‑page PDFs** | Batch‑verwerking | Loop over each page and reuse the same pipeline. |

Onthoud: elk extra filter voegt verwerkingstijd toe, dus schakel alleen in wat je echt nodig hebt.

---

## Volledig werkend voorbeeld (Klaar om te copy‑pasten)

Hieronder staat het volledige programma, klaar om te compileren. Vervang `YOUR_DIRECTORY` door de map die `skewed_noisy.jpg` bevat.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;

class PreprocessDemo
{
    static void Main()
    {
        // Create OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Build preprocessing pipeline
        ImageProcessingPipeline pipeline = new ImageProcessingPipeline();
        pipeline.Add(new FilterDeskew());                     // how to deskew image
        pipeline.Add(new FilterDenoise { Strength = 2 });    // remove noise from image
        pipeline.Add(new FilterContrastBoost { ContrastLevel = 1.8f }); // boost image contrast

        // Load source image
        var sourcePath = @"YOUR_DIRECTORY/skewed_noisy.jpg";
        var sourceImage = OcrEngine.LoadImage(sourcePath);

        // Apply pipeline
        var cleanImage = pipeline.Apply(sourceImage);

        // Perform OCR
        var result = ocrEngine.Recognize(cleanImage);

        // Output
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(result.Text);
    }
}
```

**Verwacht resultaat:** Schone, rechtgezette tekst die naar de console wordt geprint, met veel minder mis‑herkenningen dan wanneer je het ruwe bestand direct in `ocrEngine.Recognize` stopt.

---

## Conclusie

We hebben **hoe je een afbeelding rechtzet**, hoe je **ruis uit een afbeelding verwijdert**, hoe je **beeldcontrast verhoogt**, en uiteindelijk hoe je **tekst uit een afbeelding extraheert** met Aspose OCR behandeld. Door deze filters te combineren zie je een merkbare sprong in **OCR‑nauwkeurigheid**, vooral bij scans van lage kwaliteit.

Klaar voor de volgende uitdaging? Probeer een multi‑page PDF in dezelfde pipeline te voeren, of experimenteer met aangepaste drempels voor binarisatie. Dezelfde principes gelden – rechtzetten, schoonmaken, verhelderen, dan herkennen.

Heb je vragen of een vreemd randgeval? Laat een reactie achter, en laten we samen problemen oplossen. Veel programmeerplezier!  

![voorbeeld van hoe afbeelding rechtzetten](deskew-example.png "voorbeeld van hoe afbeelding rechtzetten")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}