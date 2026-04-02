---
category: general
date: 2026-04-01
description: Leer hoe je een bonafbeelding naar tekst omzet met Aspose OCR. Deze gids
  laat zien hoe je Cyrillische tekst kunt extraheren, een afbeelding kunt laden voor
  OCR, en Cyrillische tekens efficiënt kunt herkennen.
draft: false
keywords:
- receipt image to text
- extract cyrillic text
- load image for ocr
- recognize cyrillic characters
- create OCR engine
language: nl
og_description: Zet een bonafbeelding om naar tekst met Aspose OCR. Leer Cyrillische
  tekst extraheren, afbeelding laden voor OCR en Cyrillische tekens herkennen in C#.
og_title: bonafbeelding naar tekst – Cyrillische OCR met Aspose
tags:
- OCR
- C#
- Aspose
- Cyrillic
title: bonafbeelding naar tekst – Cyrillische OCR met Aspose
url: /nl/net/text-recognition/receipt-image-to-text-cyrillic-ocr-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# receipt image to text – Cyrillische OCR met Aspose

Heb je ooit een **receipt image to text** moeten omzetten, maar zijn de tekens allemaal Cyrillisch? Je bent niet de enige die zich hier zorgen over maakt. In veel detailhandels‑ of boekhoudapps komen bonnen in het Russisch, Bulgaars of Servisch schrift, en wil je toch een schone, doorzoekbare string.  

In deze tutorial laten we je precies zien hoe je **Cyrillische tekst kunt extraheren** uit een bonfoto, **een afbeelding kunt laden voor OCR**, en **Cyrillische tekens kunt herkennen** met de Aspose OCR‑bibliotheek. Aan het einde heb je een kant‑klaar C#‑programma dat het OCR‑resultaat naar een `.txt`‑bestand schrijft.

## Wat je nodig hebt

- **.NET 6** (of een recente .NET‑versie) – de code werkt ook op .NET Framework 4.7+.
- **Aspose.OCR for .NET** NuGet‑pakket – `Install-Package Aspose.OCR`.
- Een voorbeeldbonafbeelding die Cyrillische tekst bevat (bijv. `cyrillic_receipt.jpg`).
- Een ontwikkelomgeving – Visual Studio, VS Code, of Rider volstaat.  

Er zijn geen extra native afhankelijkheden nodig; Aspose levert de taalmodellen mee en behandelt het zware werk intern.

## receipt image to text – OCR‑engine instellen

Het eerste dat we moeten doen is een **OCR‑engine**‑instantie maken en aangeven welke taal we nodig hebben. Aspose maakt dit eenvoudig:

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;   // language and resource handling
using System.Drawing;      // Image class
using System.IO;

class CyrillicDemo
{
    static void Main()
    {
        // Step 1: Instantiate the OCR engine
        var ocrEngine = new OcrEngine();

        // Step 2: Tell Aspose we want Cyrillic support
        ocrEngine.Language = Language.Cyrillic;

        // Optional: Pre‑load the model if you’ll run offline later
        // ResourceManager.Preload(Language.Cyrillic);
```

> **Pro tip:** Het vooraf laden van het model voorkomt een netwerkaanroep de eerste keer dat je het programma uitvoert, wat handig is voor desktop‑ of embedded‑scenario's.

## Hoe Cyrillische tekst extraheren – De bonafbeelding laden

Nu de engine klaar is, moeten we de **afbeelding laden voor OCR**. De `System.Drawing.Image`‑klasse werkt perfect voor de meeste bitmap‑formaten.

```csharp
        // Step 3: Point to your receipt image
        string imagePath = @"YOUR_DIRECTORY\cyrillic_receipt.jpg";

        // Step 4: Load the image inside a using block (ensures disposal)
        using (var image = Image.FromFile(imagePath))
        {
            // Step 5: Run the OCR process
            var recognitionResult = ocrEngine.Recognize(image);
```

Als het bestand niet wordt gevonden, gooit `Image.FromFile` een `FileNotFoundException`. Het kan verstandig zijn om het geheel in een `try…catch`‑blok te plaatsen voor productiecodel.

## Cyrillische tekens herkennen – De tekst ophalen

Het `recognitionResult`‑object bevat de ruwe tekst, vertrouwensscores en zelfs begrenzingsvakken als je die later nodig hebt. Voor een eenvoudige “receipt image to text”‑conversie schrijven we gewoon de `Text`‑eigenschap naar een bestand:

```csharp
            // Step 6: Write the extracted text to a .txt file
            string outputPath = @"YOUR_DIRECTORY\cyrillic.txt";
            File.WriteAllText(outputPath, recognitionResult.Text);

            // Quick verification: print to console
            Console.WriteLine("OCR completed. Extracted text:");
            Console.WriteLine(recognitionResult.Text);
        }
    }
}
```

Wanneer je het programma uitvoert, zou je iets moeten zien als:

```
OCR completed. Extracted text:
СЧЕТ № 12345
Дата: 01/04/2026
Товар      Кол-во   Цена
Хлеб       2        30,00
Молоко     1        45,00
Итого:               105,00
```

Dat is het **receipt image to text**‑resultaat waar je naar op zoek was.

![receipt image to text example](receipt-ocr-example.png "Example of a receipt image being converted to text")

*Afbeeldings‑alt‑tekst: receipt image to text‑conversie die Cyrillische tekens toont die door Aspose OCR zijn geëxtraheerd.*

## Randgevallen & Veelgestelde vragen

### Wat als het taalmodel nog niet is gedownload?

Aspose downloadt automatisch het benodigde model de eerste keer dat je `ocrEngine.Language = Language.Cyrillic;` instelt. Als de machine geen internet heeft, zal de optionele pre‑load stap falen. In dat geval kun je het model handmatig leveren (zie Aspose‑documentatie) of ervoor zorgen dat het apparaat `download.aspose.com` kan bereiken.

### Hoe ga ik om met meerdere talen op dezelfde bon?

Je kunt een door komma's gescheiden lijst doorgeven:

```csharp
ocrEngine.Language = Language.Cyrillic | Language.English;
```

Aspose zal proberen tekens uit beide sets te herkennen.

### Mijn bon is onscherp – kan ik de nauwkeurigheid verbeteren?

Aspose OCR biedt basis‑image‑preprocessing:

```csharp
ocrEngine.ImagePreprocessor = new ImagePreprocessor
{
    Sharpen = true,
    Binarize = true,
    Denoise = true
};
```

Pas dit toe voordat je `Recognize` aanroept.

### Hoe zit het met grootschalige batchverwerking?

Wikkel de herkenningslus in een `Parallel.ForEach` en hergebruik dezelfde `OcrEngine`‑instantie (deze is thread‑safe nadat het model is geladen). Vergeet niet de engine te vergrendelen als je thread‑safety‑problemen tegenkomt.

## Volledig werkend voorbeeld (Alle stappen gecombineerd)

Hieronder staat het volledige, kant‑klaar te kopiëren programma dat de optionele pre‑load en basis‑foutafhandeling bevat:

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System;
using System.Drawing;
using System.IO;

class CyrillicDemo
{
    static void Main()
    {
        try
        {
            // Create OCR engine and select Cyrillic language
            var ocrEngine = new OcrEngine();
            ocrEngine.Language = Language.Cyrillic;

            // Optional: preload model for offline use
            // ResourceManager.Preload(Language.Cyrillic);

            // Path to the receipt image
            string imagePath = @"YOUR_DIRECTORY\cyrillic_receipt.jpg";

            // Verify the file exists
            if (!File.Exists(imagePath))
                throw new FileNotFoundException("Receipt image not found.", imagePath);

            using (var image = Image.FromFile(imagePath))
            {
                // Perform OCR
                var result = ocrEngine.Recognize(image);

                // Output path for extracted text
                string outputPath = @"YOUR_DIRECTORY\cyrillic.txt";
                File.WriteAllText(outputPath, result.Text);

                Console.WriteLine("✅ receipt image to text conversion succeeded.");
                Console.WriteLine("Extracted text saved to: " + outputPath);
                Console.WriteLine("\n--- Extracted Text ---\n");
                Console.WriteLine(result.Text);
            }
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine("❌ An error occurred: " + ex.Message);
        }
    }
}
```

Voer het programma uit (`dotnet run` vanuit de projectmap) en je krijgt een `.txt`‑bestand met de **receipt image to text**‑output.

## Conclusie

Je hebt nu een solide, end‑to‑end‑oplossing voor het omzetten van een **receipt image to text**—specifiek voor Cyrillische scripts—met Aspose OCR. We hebben behandeld hoe je **OCR‑engine maakt**, **afbeelding laadt voor OCR**, **Cyrillische tekst extraheert**, en **Cyrillische tekens herkent** in slechts een paar regels C#.  

Volgende stappen? Probeer een map met bonnen te verwerken, experimenteer met de `ImagePreprocessor` om de nauwkeurigheid te verhogen, of combineer de OCR‑output met een database voor geautomatiseerde boekhouding. Als je andere alfabetten moet verwerken, verwissel dan `

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}