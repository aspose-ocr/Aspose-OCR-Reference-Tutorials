---
category: general
date: 2026-02-09
description: Tekst extraheren uit een afbeelding met C# offline OCR. Een volledig
  C# OCR‑voorbeeld laat zien hoe je een afbeelding laadt voor OCR, Cyrillische tekst
  herkent en tekst uit een paspoort extraheert.
draft: false
keywords:
- extract text from image
- c# ocr example
- load image for ocr
- recognize cyrillic text
- recognize text from passport
language: nl
og_description: Haal tekst uit een afbeelding met C# offline OCR. Leer een stapsgewijs
  C# OCR‑voorbeeld dat een afbeelding laadt voor OCR, Cyrillische tekst herkent en
  tekst uit een paspoort extraheert.
og_title: Tekst uit afbeelding extraheren in C# – Offline OCR-gids
tags:
- OCR
- C#
- Aspose
title: Tekst uit afbeelding extraheren in C# – Offline OCR-voorbeeld
url: /nl/net/text-recognition/extract-text-from-image-in-c-offline-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tekst uit afbeelding extraheren in C# – Offline OCR‑voorbeeld

Heb je ooit **tekst uit een afbeelding** moeten halen, maar liep je vast op netwerk‑afhankelijke API’s? Je bent niet de enige. Veel ontwikkelaars komen tegen problemen wanneer de OCR‑service runtime taalpakketten probeert te downloaden, vooral in beperkte omgevingen.

In deze gids lopen we een **c# ocr example** stap voor stap door die volledig offline draait, een afbeelding laadt voor OCR, en Cyrillische tekst van een paspoort herkent. Aan het einde heb je een kant‑klaar programma dat de platte‑tekstinhoud van elke ondersteunde afbeelding direct naar de console print.

## Wat je zult leren

- Hoe je Aspose.OCR instelt voor offline verwerking.  
- De exacte code om **afbeelding te laden voor OCR** vanaf schijf.  
- Hoe je de engine configureert om **Cyrillische tekst** te herkennen.  
- Een volledige, copy‑paste‑klare **c# ocr example** die tekst uit een paspoort‑stijl foto haalt.  

Ervaring met Aspose is niet vereist; een .NET 6 (of later) SDK en Visual Studio 2022 (of VS Code) zijn voldoende.

---

![Tekst uit afbeelding extraheren met Aspose OCR op een paspoortfoto](/images/ocr-passport.jpg "tekst uit afbeelding extraheren")

## Stap 1: Het project configureren om tekst uit afbeelding te extraheren

Voordat je code schrijft, zorg dat het Aspose.OCR NuGet‑pakket aan je project is toegevoegd:

```bash
dotnet add package Aspose.OCR
```

> **Pro tip:** Gebruik de `--version`‑vlag om te vergrendelen op de nieuwste stabiele release (bijv. `13.9.0`). Dit garandeert compatibiliteit met .NET 6.

Een nieuwe console‑app maken is zo simpel:

```bash
dotnet new console -n OfflineOcrDemo
cd OfflineOcrDemo
```

Nu heb je een schone basis waarin we **tekst uit afbeelding** extraheren zonder ooit internet te gebruiken.

## Stap 2: Afbeelding laden voor OCR – Het paspoortfoto lezen

Het eerste wat de OCR‑engine nodig heeft, is een bitmap of stream die de foto voorstelt. In ons scenario **laden we afbeelding voor OCR** vanaf een lokaal bestand genaamd `cyrillic_passport.jpg`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System;

// Step 2: Load the image file (this is the “load image for ocr” part)
var imagePath = @"YOUR_DIRECTORY\cyrillic_passport.jpg";

// Validate the file exists – helpful when the path is wrong.
if (!System.IO.File.Exists(imagePath))
{
    Console.WriteLine($"❌ Image not found at {imagePath}");
    return;
}

// ImageStream abstracts the underlying format; it works with JPEG, PNG, etc.
var image = ImageStream.FromFile(imagePath);
```

> **Waarom dit belangrijk is:** Een stream leveren in plaats van een ruwe `Bitmap` laat Aspose de formaatdetectie intern afhandelen, waardoor boilerplate en mogelijke bugs verminderen.

## Stap 3: Offline‑modus configureren en Cyrillische taal kiezen

Aspose.OCR kan taalmodellen on‑the‑fly downloaden, maar dat ondermijnt een offline oplossing. Schakel netwerkaanroepen uit en geef expliciet aan welke taal de engine moet gebruiken.

```csharp
// Step 3: Create the OCR engine and switch to offline mode
var ocrEngine = new OcrEngine
{
    Configuration =
    {
        OfflineMode = true,               // No network traffic – perfect for secure environments
        Language = new[] { OcrLanguage.Cyrillic } // We want to **recognize cyrillic text**
    }
};
```

> **Randgeval:** Als je later Latijnse tekens in hetzelfde document moet herkennen, voeg dan `OcrLanguage.English` toe aan de array. De engine handelt multi‑taaldetectie automatisch af.

## Stap 4: De OCR‑engine uitvoeren en Cyrillische tekst herkennen

Nu **herkennen we tekst van paspoort**‑stijl afbeeldingen. De `Recognize`‑methode retourneert een rijk resultaatobject met platte tekst, vertrouwensscores en begrenzingsvakken.

```csharp
// Step 4: Perform the OCR operation
OcrResult result = ocrEngine.Recognize(image);

// Step 5: Output the plain text – this is where we finally **extract text from image**
Console.WriteLine("📝 Extracted Text:");
Console.WriteLine("-------------------");
Console.WriteLine(result.PlainText);
```

### Verwachte console‑output

```
📝 Extracted Text:
-------------------
ПАСПОРТ РФ
Иванов Иван Иванович
01.01.1990
...
```

Als het resultaat onleesbaar is, controleer dan of de bronafbeelding duidelijk is en of het `OfflineMode`‑taalpakket voor Cyrillisch aanwezig is in de Aspose‑installatiemap (meestal `\Aspose.OCR\resources\languages`).

## Volledig C# OCR‑voorbeeld – Complete broncode

Hieronder staat het **c# ocr example** in zijn geheel. Kopieer‑en‑plak het in `Program.cs` en voer `dotnet run` uit. Alles wat je nodig hebt om **tekst uit afbeelding** te extraheren staat hier.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System;

class OfflineExample
{
    static void Main()
    {
        // --------------------------------------------------------------
        // Step 1: Create the OCR engine (offline mode)
        // --------------------------------------------------------------
        var ocrEngine = new OcrEngine
        {
            Configuration =
            {
                OfflineMode = true,                     // No network calls
                Language = new[] { OcrLanguage.Cyrillic } // Recognize Cyrillic text
            }
        };

        // --------------------------------------------------------------
        // Step 2: Load the image for OCR (passport photo)
        // --------------------------------------------------------------
        var imagePath = @"YOUR_DIRECTORY\cyrillic_passport.jpg";

        if (!System.IO.File.Exists(imagePath))
        {
            Console.WriteLine($"❌ Image not found at {imagePath}");
            return;
        }

        var image = ImageStream.FromFile(imagePath);

        // --------------------------------------------------------------
        // Step 3: Recognize the text
        // --------------------------------------------------------------
        var result = ocrEngine.Recognize(image);

        // --------------------------------------------------------------
        // Step 4: Output the plain text (the final extraction)
        // --------------------------------------------------------------
        Console.WriteLine("📝 Extracted Text:");
        Console.WriteLine("-------------------");
        Console.WriteLine(result.PlainText);
    }
}
```

### Het voorbeeld uitvoeren

```bash
dotnet run
```

Je zou nu de console de paspoortgegevens in het Cyrillisch moeten zien afdrukken. Dat is het moment waarop je weet dat je **tekst uit afbeelding**‑pipeline werkt.

## Veelvoorkomende valkuilen & hoe ze op te lossen

| Symptoom | Waarschijnlijke oorzaak | Oplossing |
|----------|--------------------------|-----------|
| Lege `PlainText` | Verkeerd taalmodel of afbeelding te donker | Zorg dat het `OfflineMode`‑taalpakket `Cyrillic` bevat en verhoog het contrast van de afbeelding |
| `System.DllNotFoundException` | Ontbrekende native Aspose OCR‑binaries | Installeer het NuGet‑pakket opnieuw of kopieer `Aspose.OCR.Native.dll` naar de output‑map |
| Trage prestaties bij grote afbeeldingen | Engine verwerkt volledige resolutie | Schaal de afbeelding naar ≤ 1500 px breed voordat je deze aan `ImageStream` doorgeeft |
| Vervormde tekens | Afbeelding verkeerd gedraaid | Gebruik `Image.RotateFlip(RotateFlipType.Rotate90FlipNone)` vóór het aanmaken van de stream |

## Volgende stappen – Het offline OCR‑werkproces uitbreiden

- **Afbeelding laden voor OCR** vanuit een `MemoryStream` bij het verwerken van geüploade bestanden in ASP.NET Core.  
- Overschakelen naar **tekst herkennen van paspoort** in batch‑modus door over een map met paspoort‑scans te itereren.  
- Het resultaat combineren met **regular expressions** om velden zoals paspoortnummer of geboortedatum te extraheren.  
- Experimenteren met `ocrEngine.Configuration.UseParallelProcessing = true` voor multi‑core snelheidswinst.

---

### Conclusie

We hebben zojuist laten zien hoe je **tekst uit afbeelding** kunt halen met een volledig offline C# OCR‑pipeline. Het korte, zelfstandige **c# ocr example** laadt een afbeelding, configureert de engine om **Cyrillische tekst** te herkennen, en print de geëxtraheerde paspoortgegevens – allemaal zonder één enkele netwerkaanvraag.

Voel je vrij om de code aan te passen, meer talen toe te voegen, of de output in een database te steken. De mogelijkheden zijn onbeperkt zodra je de basis beheerst van een afbeelding laden voor OCR en tekst van een paspoort‑stijl foto herkennen.

Heb je vragen of wil je je eigen tweaks delen? Laat een reactie achter, en happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}