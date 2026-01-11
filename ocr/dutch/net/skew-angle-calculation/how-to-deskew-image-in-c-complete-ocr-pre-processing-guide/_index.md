---
category: general
date: 2026-01-10
description: Hoe een afbeelding rechtzetten en OCR-resultaten verbeteren met Aspose.OCR.
  Leer hoe je een afbeelding voor OCR kunt voorbewerken, ruis uit een scan kunt verwijderen
  en tekst uit een scan kunt herkennen.
draft: false
keywords:
- how to deskew image
- preprocess image for ocr
- recognize text from scan
- how to use ocr
- remove noise from scan
language: nl
og_description: Hoe een afbeelding rechtzetten en de OCR-nauwkeurigheid verbeteren.
  Deze gids laat zien hoe je een afbeelding voor OCR kunt voorbewerken, ruis uit een
  scan kunt verwijderen en tekst uit een scan kunt herkennen met Aspose.OCR.
og_title: Hoe een afbeelding rechtzetten in C# – Complete OCR-preprocessinggids
tags:
- OCR
- C#
- Image Processing
title: Hoe een afbeelding rechtzetten in C# – Complete gids voor OCR‑voorverwerking
url: /nl/net/skew-angle-calculation/how-to-deskew-image-in-c-complete-ocr-pre-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe een afbeelding rechtzetten in C# – Complete OCR‑preprocessinggids

Heb je je ooit afgevraagd **hoe je een afbeelding rechtzet** voordat je ze aan een OCR‑engine voert? Je bent niet de enige. Gescande documenten zijn vaak scheef, ruisachtig of hebben een laag contrast, en dat verstoort elke poging tot teksterkenning.  

In deze tutorial lopen we een volledig, uitvoerbaar voorbeeld door dat **afbeeldingen voor OCR preproceste**, ruis van de scan verwijdert, en uiteindelijk **tekst van de scan herkent** met behulp van de Aspose.OCR‑bibliotheek. Aan het einde heb je een duidelijk beeld van **hoe je OCR gebruikt** in C# terwijl de code kort en bondig blijft.

> **Pro tip:** Zelfs een kleine rotatie (5‑10°) kan de OCR‑nauwkeurigheid met 30 % of meer doen dalen. Het rechtzetten van de afbeelding is de eerste stap die je nooit moet overslaan.

---

## Wat je nodig hebt

- **.NET 6+** (de code werkt ook op .NET Framework, maar .NET 6 is de huidige LTS)
- **Aspose.OCR for .NET** – je kunt het ophalen via NuGet (`Install-Package Aspose.OCR`)
- Een voorbeeld‑TIFF/PNG/JPEG die gedraaid of ruisachtig is (we gebruiken `noisy_rotated.tif` in het voorbeeld)
- Elke IDE die je wilt – Visual Studio, Rider, of VS Code volstaat

Dat is alles. Geen extra bibliotheken, geen externe services.

---

## Stap 1 – Laad de bronafbeelding (Waarom het belangrijk is)

Voordat we **een afbeelding kunnen rechtzetten**, moeten we deze inlezen in een Aspose `ImageStream`. Dit object abstraheert bestands‑I/O en biedt de OCR‑engine een consistente interface.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

// Load the original scan – replace the path with your own file
var sourceImage = ImageStream.FromFile("YOUR_DIRECTORY/noisy_rotated.tif");

// Quick sanity check – make sure the image loaded
if (sourceImage == null)
{
    Console.WriteLine("Failed to load the image. Check the path and file permissions.");
    return;
}
```

*Waarom eerst laden?* Omdat alle volgende filters werken op een afbeelding in het geheugen. Als het bestand niet gelezen kan worden, stort de hele pijplijn in.

---

## Stap 2 – Bouw een pre‑processing‑pijplijn (rechtzetten + ruisverwijdering + contrast)

Een robuuste OCR‑workflow schakelt meestal meerdere filters aaneen. Hier **preprocessen we de afbeelding voor OCR** en, nog belangrijker, **hoe we de afbeelding automatisch rechtzetten**.

```csharp
// Create a pipeline that will run three filters in order
var preprocessPipeline = new PreprocessPipeline()
{
    // 1️⃣ DeskewFilter – detects rotation up to 30° and corrects it
    new DeskewFilter { MaxAngle = 30 },

    // 2️⃣ DenoiseFilter – smooths out speckles while keeping edges
    new DenoiseFilter { Strength = 0.8 },

    // 3️⃣ ContrastBoostFilter – makes faint characters pop
    new ContrastBoostFilter { Level = 1.3 }
};
```

**Waarom deze drie?**  
- **DeskewFilter** lost het “hoe je een afbeelding rechtzet” probleem automatisch op; je hoeft de hoek niet te raden.  
- **DenoiseFilter** pakt de eis “verwijder ruis van scan” aan, die anders fantoomtekens creëert.  
- **ContrastBoostFilter** helpt de OCR‑engine donkere tekst te onderscheiden van een lichte achtergrond, een klassiek probleem wanneer je *afbeeldingen voor OCR preprocesses*.

---

## Stap 3 – Pas de pijplijn toe (de transformatie zien)

Nu voeren we de filters daadwerkelijk uit. De geretourneerde `processedImage` is wat we aan de OCR‑engine gaan voeren.

```csharp
// Apply all filters – the result is a cleaned‑up bitmap
var processedImage = preprocessPipeline.Apply(sourceImage);

// Optional: Save the cleaned image for visual verification
processedImage.Save("cleaned_output.tif");
Console.WriteLine("Image preprocessing complete – cleaned_output.tif saved.");
```

Als je `cleaned_output.tif` opent, zul je merken dat de tekst recht is, minder korrelig en met hoger contrast. Deze visuele controle is handig wanneer je *ruis van scan verwijdert* en wilt bevestigen dat het rechtzetten heeft gewerkt.

---

## Stap 4 – Maak en configureer de OCR‑engine (hoe je OCR gebruikt)

Met een nette afbeelding in de hand, instantieren we `OcrEngine`. Dit is de kern van **hoe je OCR gebruikt** met Aspose.

```csharp
// Initialize the OCR engine
var ocrEngine = new OcrEngine
{
    // Assign the pre‑processed image
    Image = processedImage,

    // Optional: Set language (English is default)
    // Language = Language.English,
    
    // Enable automatic page segmentation (helps with multi‑column scans)
    AutoPageSegmentation = true
};
```

*Waarom `AutoPageSegmentation` instellen?* Omdat veel scans tabellen of meerdere kolommen bevatten. Het inschakelen laat de engine de pagina intelligent splitsen, waardoor het uiteindelijke **tekst van de scan herkennen** resultaat verbetert.

---

## Stap 5 – Voer het herkenningsproces uit (eindelijk tekst herkennen)

Nu het moment van de waarheid: we vragen de engine de tekst te lezen.

```csharp
// Kick off the OCR process
ocrEngine.Recognize();

// Retrieve the plain‑text result
string recognizedText = ocrEngine.Text;

// Show the output in the console
Console.WriteLine("=== Recognized Text ===");
Console.WriteLine(recognizedText);
```

Als alles soepel verliep, zie je een schoon tekstblok dat overeenkomt met het originele document. Dat is de beloning voor het correct **rechtzetten van de afbeelding**, **verwijderen van ruis**, en **preprocessen van de afbeelding voor OCR**.

---

## Stap 6 – Volledig werkend voorbeeld (klaar om te kopiëren‑en‑plakken)

Hieronder staat het volledige programma, klaar om te compileren. Vervang alleen het bestandspad en je bent klaar om te gaan.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Load the source image
        // -------------------------------------------------
        var sourceImage = ImageStream.FromFile("YOUR_DIRECTORY/noisy_rotated.tif");
        if (sourceImage == null)
        {
            Console.WriteLine("Unable to load image. Check the path.");
            return;
        }

        // -------------------------------------------------
        // 2️⃣ Build the preprocessing pipeline
        // -------------------------------------------------
        var preprocessPipeline = new PreprocessPipeline()
        {
            new DeskewFilter { MaxAngle = 30 },          // how to deskew image
            new DenoiseFilter { Strength = 0.8 },       // remove noise from scan
            new ContrastBoostFilter { Level = 1.3 }      // improves OCR accuracy
        };

        // -------------------------------------------------
        // 3️⃣ Apply the pipeline
        // -------------------------------------------------
        var processedImage = preprocessPipeline.Apply(sourceImage);
        processedImage.Save("cleaned_output.tif");
        Console.WriteLine("Preprocessing finished – cleaned_output.tif saved.");

        // -------------------------------------------------
        // 4️⃣ Configure the OCR engine
        // -------------------------------------------------
        var ocrEngine = new OcrEngine
        {
            Image = processedImage,
            AutoPageSegmentation = true   // how to use OCR effectively
        };

        // -------------------------------------------------
        // 5️⃣ Recognize text from scan
        // -------------------------------------------------
        ocrEngine.Recognize();
        string result = ocrEngine.Text;

        Console.WriteLine("\n=== Recognized Text ===");
        Console.WriteLine(result);
    }
}
```

**Verwachte output** (afgekapt voor beknoptheid):

```
=== Recognized Text ===
This is a sample scanned document.
It contains several lines of text,
and the OCR engine has correctly read them.
```

Als de output er onduidelijk uitziet, controleer dan of de bronafbeelding niet meer dan 30° gedraaid is, of vergroot `DeskewFilter.MaxAngle`.

---

## Veelgestelde vragen (randgevallen & variaties)

| Vraag | Antwoord |
|----------|--------|
| **Wat als mijn scan 45° gedraaid is?** | `DeskewFilter` beperkt zich tot `MaxAngle`. Verhoog deze (bijv. `MaxAngle = 60`) of pre‑draai de afbeelding met een grafische bibliotheek voordat je deze aan de pijplijn voert. |
| **Kan ik PDF's pagina‑voor‑pagina verwerken?** | Ja. Converteer elke PDF‑pagina naar een afbeelding (bijv. met `Aspose.Pdf`) en voer dezelfde pijplijn uit op elke bitmap. |
| **Mijn document is in het Frans – moet ik iets aanpassen?** | Stel `ocrEngine.Language = Language.French;` in of laad een aangepast taalpakket. De rest van de pijplijn blijft gelijk. |
| **Is er een manier om de originele resolutie te behouden?** | `PreprocessPipeline` werkt op de originele bitmap en behoudt de DPI. Vermijd alleen het aanroepen van `ImageStream.Resize` tenzij je moet downscalen voor prestaties. |
| **Hoe beïnvloedt contrastversterking gekleurde scans?** | `ContrastBoostFilter` werkt op elk kanaal; het is veilig voor grijswaarden- of kleurafbeeldingen, maar je kunt ook eerst naar grijswaarden converteren met `new GrayscaleFilter()`. |

---

## Afbeeldingsvoorbeeld (visuele hulp)

![voorbeeld hoe afbeelding rechtzetten](/images/deskew-example.png)

*De afbeelding toont een voor/na van een 12° gedraaide, ruisige scan die is rechtgezet en opgeschoond.*

---

## Conclusie

We hebben **hoe je een afbeelding rechtzet** met Aspose.OCR behandeld, een volledige **preprocess pipeline voor OCR** gedemonstreerd, laten zien hoe je **ruis van scan verwijdert**, en uiteindelijk **tekst van de scan herkent** met een paar regels C#. Door `DeskewFilter`, `DenoiseFilter` en `ContrastBoostFilter` te combineren krijg je een nette bitmap die de OCR‑engine haar werk laat doen zonder te haperen door artefacten.  

Volgende stappen? Probeer verschillende filtersterktes uit, voeg een `BinarizationFilter` toe voor pure zwart‑wit output, of voer de opgeschoonde afbeelding in een downstream NLP‑pipeline. Hetzelfde patroon werkt voor bonnen, paspoorten en historische documenten.  

Heb je meer vragen over **hoe je OCR gebruikt** in andere talen of frameworks? Laat een reactie achter, en happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}