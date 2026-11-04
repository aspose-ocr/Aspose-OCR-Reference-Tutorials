---
category: general
date: 2026-03-18
description: Hoe een afbeelding rechtzetten en ruis verminderen in gescande bestanden.
  Leer hoe je een afbeelding uit een bestand laadt, tekst uit een TIFF extraheert
  en tekst uit een afbeelding herkent met Aspose OCR.
draft: false
keywords:
- how to deskew image
- how to reduce noise
- recognize text from image
- load image from file
- extract text from tiff
language: nl
og_description: Hoe je een afbeelding snel kunt rechtzetten met Aspose OCR. Deze gids
  laat zien hoe je ruis kunt verminderen, een afbeelding uit een bestand kunt laden
  en tekst uit een TIFF kunt extraheren in C#.
og_title: Hoe een afbeelding rechtzetten – Volledige C# OCR-handleiding
tags:
- OCR
- C#
- Image Processing
title: Hoe een afbeelding rechtzetten en scans opschonen – Complete C#‑gids
url: /nl/net/skew-angle-calculation/how-to-deskew-image-and-clean-up-scans-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe een afbeelding rechtzetten – Volledige C# OCR Tutorial

Heb je je ooit afgevraagd **hoe je een afbeelding kunt rechtzetten** die eruitziet alsof ze van een wiebelige scanner is genomen? Je bent niet de enige. De meeste ontwikkelaars lopen tegen dit probleem aan wanneer de bron‑TIFF een beetje scheef staat, en de OCR‑resultaten een rommel worden. Het goede nieuws? Met een paar regels C# kun je de foto rechtzetten, de korrelige achtergrond onderdrukken en schone, doorzoekbare tekst rechtstreeks uit het bestand halen.

In deze gids lopen we stap voor stap door **hoe je ruis vermindert**, **een afbeelding laadt vanuit een bestand**, en uiteindelijk **tekst herkent uit een afbeelding** met Aspose OCR. Aan het einde kun je **tekst uit tiff**‑documenten extraheren zonder moeite.

> **Pro tip:** Als je Aspose OCR al voor andere projecten gebruikt, kun je deze filters toevoegen zonder extra licentie‑problemen.

---

## Wat je nodig hebt

- .NET 6 of later (de code werkt ook op .NET Core)  
- Aspose.OCR NuGet‑pakket (`Install-Package Aspose.OCR`)  
- Een gescande TIFF die een beetje gedraaid of ruisig is (we gebruiken `skewed_scanned_doc.tif` als voorbeeld)  
- Een teksteditor of IDE (Visual Studio, VS Code, Rider – kies er één)

Er zijn geen extra bibliotheken nodig; de filters die we gebruiken zijn ingebouwd in Aspose OCR.

## Stap 1 – Maak de OCR‑engine (Hoe een afbeelding rechtzetten)

Het eerste wat je doet is een `OcrEngine` opzetten. Zie het als het brein dat later de tekens voor je zal lezen.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Filters;

class PreprocessDemo
{
    static void Main()
    {
        // Initialize the OCR engine – this object holds all settings
        var ocrEngine = new OcrEngine();
```

Waarom de engine van tevoren aanmaken? Het geeft je één plek om preprocessing‑filters, taal‑pakketten en uitvoeropties toe te voegen. Als je deze stap overslaat en direct `OcrEngine.Recognize` aanroept, verlies je de mogelijkheid om de afbeelding eerst schoon te maken, en dat is precies waarom we rechtzetten belangrijk vinden.

## Stap 2 – Voeg Deskew‑ en Ruisreductie‑filters toe (Hoe ruis te verminderen)

Now we attach two filters:

| Filter | Wat het doet | Waarom het belangrijk is |
|--------|--------------|--------------------------|
| `AutoDeskewFilter` | Detecteert en corrigeert rotatie | Rechtzet tekstregels zodat de OCR‑engine ze correct kan lezen |
| `NoiseReductionFilterV2` | Verwijdert vlekjes en achtergrondkorrel | Schonere pixels betekenen minder verkeerde herkenningen |

```csharp
        // Add filters to improve OCR accuracy
        ocrEngine.Settings.Filters.Add(new AutoDeskewFilter());          // corrects rotation
        ocrEngine.Settings.Filters.Add(new NoiseReductionFilterV2());   // reduces background noise
```

Je kunt `NoiseReductionFilterV2` vervangen door de oudere versie, maar het v2‑algoritme werkt beter met moderne scanners. Als je document al perfect vlak is, zal het deskew‑filter de afbeelding simpelweg onveranderd doorgeven — geen schade.

## Stap 3 – Laad de afbeelding vanuit een bestand (Afbeelding laden vanuit bestand)

Aspose biedt een handige `ImageStream.FromFile`‑helper die verschillende formaten kan lezen, waaronder TIFF, JPEG, PNG en BMP. Zo halen we het bestand in het geheugen:

```csharp
        // Load the scanned image you want to preprocess
        var image = ImageStream.FromFile(@"YOUR_DIRECTORY/skewed_scanned_doc.tif");
```

Vervang `YOUR_DIRECTORY` door het daadwerkelijke pad op jouw machine. Als je met een relatief pad werkt, zorg er dan voor dat het bestand naast je uitvoerbare bestand staat of stel de werkmap overeenkomstig in.

## Stap 4 – Voer OCR uit op de voorbewerkte afbeelding (Tekst herkennen uit afbeelding)

Met de filters op hun plaats en de afbeelding geladen, vragen we Aspose eindelijk om de tekens te lezen:

```csharp
        // Perform OCR – the engine will automatically apply the filters first
        var ocrResult = ocrEngine.Recognize(image);
```

Achter de schermen voert de engine het deskew‑algoritme uit, verwijdert ruis en draait vervolgens een op neurale netwerken gebaseerde herkenner. Het resultaat wordt verpakt in een `OcrResult`‑object dat je de ruwe tekst, vertrouwensscores en zelfs begrenzings‑boxen geeft als je die later nodig hebt.

## Stap 5 – Toon of sla de geëxtraheerde tekst op (Tekst extraheren uit TIFF)

Voor een snelle demo dumpen we de tekst gewoon naar de console, maar je kunt het ook naar een bestand, een database schrijven, of in een downstream‑workflow gebruiken.

```csharp
        // Show the recognized text in the console
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Verwachte output** (voorbeeld, kan variëren per document):

```
Invoice #12345
Date: 2023‑04‑01
Total: $1,250.00
Thank you for your business!
```

Als de output nog steeds onduidelijke tekens bevat, controleer dan of de originele TIFF niet te lage resolutie heeft (minimaal 300 dpi wordt aanbevolen) en of de taal correct is ingesteld in `ocrEngine.Settings.Language`.

## Volledig werkend voorbeeld (Alle stappen op één plek)

Hieronder staat het volledige programma dat je kunt kopiëren‑plakken in een nieuw console‑project en direct kunt uitvoeren.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Filters;

class PreprocessDemo
{
    static void Main()
    {
        // 1️⃣ Create OCR engine
        var ocrEngine = new OcrEngine();

        // 2️⃣ Add preprocessing filters
        ocrEngine.Settings.Filters.Add(new AutoDeskewFilter());          // deskew image
        ocrEngine.Settings.Filters.Add(new NoiseReductionFilterV2());   // reduce noise

        // 3️⃣ Load the image file (TIFF, JPEG, etc.)
        var image = ImageStream.FromFile(@"YOUR_DIRECTORY/skewed_scanned_doc.tif");

        // 4️⃣ Recognize text – filters run automatically
        var ocrResult = ocrEngine.Recognize(image);

        // 5️⃣ Output the extracted text
        Console.WriteLine(ocrResult.Text);
    }
}
```

Sla het bestand op als `Program.cs`, voer `dotnet run` uit, en je zou de opgeschoonde tekst in je terminal moeten zien verschijnen.

## Veelgestelde vragen & randgevallen

### Wat als mijn TIFF meerdere pagina’s heeft?

Aspose OCR kan meer‑pagina‑afbeeldingen verwerken door te itereren over `image.GetPages()` (of `image.Pages`). Elke pagina geeft zijn eigen `OcrResult` terug. Combineer ze met `StringBuilder` als je één enkele string nodig hebt.

### Werkt het deskew‑filter op sterk gedraaide afbeeldingen?

Het verwerkt rotaties tot ongeveer ±15°. Daarboven kun je de afbeelding handmatig moeten voor‑draaien met een grafische bibliotheek (bijv. `System.Drawing` of `SkiaSharp`) voordat je deze aan Aspose geeft.

### Hoe kan ik de nauwkeurigheid verbeteren voor niet‑Engelse tekst?

Stel de taal expliciet in:

```csharp
ocrEngine.Settings.Language = Language.English; // or Language.French, etc.
```

Je kunt ook aangepaste taal‑pakketten laden als de ingebouwde pakketten je alfabet niet dekken.

### Kan ik dit op Linux draaien?

Zeker. Aspose OCR is cross‑platform; zorg er alleen voor dat de native afhankelijkheden aanwezig zijn (meestal geen voor de pure .NET‑versie). Gebruik `dotnet publish -r linux-x64` voor een zelfstandige binary.

## Bonus: De rechtgezette afbeelding visualiseren

Als je de gecorrigeerde afbeelding vóór OCR wilt zien, kun je deze terug opslaan op schijf:

```csharp
// After OCR, the filtered image is stored in ocrEngine.Settings.FiltersResult
var corrected = ocrEngine.Settings.FiltersResult;
corrected.Save(@"output/deskewed_cleaned.tif");
```

![voorbeeld van afbeelding rechtzetten](https://example.com/deskew-demo.png "voorbeeld van afbeelding rechtzetten")

*Afbeeldings‑alt‑tekst:* **voorbeeld van afbeelding rechtzetten** – toont een vóór/na van een gedraaide TIFF gecorrigeerd door AutoDeskewFilter.

## Conclusie

We hebben **hoe je een afbeelding rechtzet**, **hoe je ruis vermindert**, en de volledige pipeline om **tekst te herkennen uit een afbeelding**, **een afbeelding te laden vanuit een bestand**, en **tekst uit tiff te extraheren** met Aspose OCR in C# behandeld. De belangrijkste conclusie? Het toevoegen van slechts twee preprocessing‑filters kan een wobbelige, korrelige scan omzetten in een scherp, doorzoekbaar document zonder externe tools.

Klaar voor de volgende stap? Probeer `AutoDeskewFilter` te vervangen door `AutoRotateFilter` als je documenten ondersteboven staan, of experimenteer met `ContrastEnhancementFilter` voor vervaagde afdrukken. Hetzelfde patroon—engine → filters → load → recognize—geldt voor alle Aspose OCR‑scenario's, zodat je dit skelet kunt hergebruiken voor PDF’s, PNG’s of zelfs camerafoto’s.

Veel plezier met coderen, en moge je OCR altijd nauwkeurig zijn!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}