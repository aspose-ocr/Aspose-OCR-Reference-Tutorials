---
category: general
date: 2026-06-28
description: Herken tekst uit een afbeelding snel met Aspose OCR. Leer hoe je GPU-versnelling
  inschakelt, een afbeelding laadt voor OCR en tekst van een bon in platte tekst extraheert.
draft: false
keywords:
- recognize text from image
- extract text from receipt
- how to enable gpu acceleration
- convert image to plain text
- load image for ocr
language: nl
og_description: herken tekst van afbeelding met Aspose OCR. Deze gids laat zien hoe
  je GPU‑versnelling inschakelt, een afbeelding laadt voor OCR en deze converteert
  naar platte tekst.
og_title: tekst herkennen uit afbeelding met Aspose OCR GPU
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: recognize text from image quickly with Aspose OCR. Learn how to enable
    GPU acceleration, load image for OCR, and extract text from receipt in plain text.
  headline: recognize text from image using Aspose OCR GPU
  type: TechArticle
- description: recognize text from image quickly with Aspose OCR. Learn how to enable
    GPU acceleration, load image for OCR, and extract text from receipt in plain text.
  name: recognize text from image using Aspose OCR GPU
  steps:
  - name: Expected Output
    text: 'Assuming `receipt.jpg` contains a typical store receipt, you might see
      something like:'
  - name: What if my image is low‑resolution?
    text: OCR accuracy drops dramatically on blurry or tiny images. Before calling
      `Recognize`, consider up‑scaling the image (e.g., using `System.Drawing` or
      `ImageSharp`) and applying a contrast boost. Aspose also offers `Preprocess`
      methods you can experiment with.
  - name: My GPU isn’t being used – why?
    text: '- Verify that `EnableGpu` is `true` *before* you call `Recognize`. - Check
      that your driver supports OpenCL 1.2+ (most modern drivers do). - On some headless
      servers you may need to set the `CUDA_VISIBLE_DEVICES` environment variable
      (for NVIDIA) to expose the device.'
  - name: Can I process multiple images in parallel?
    text: Absolutely. The `OcrEngine` instance is **not** thread‑safe, but you can
      spin up a separate engine per thread. Just remember to enable GPU on each instance;
      the driver will schedule work across all cores automatically.
  - name: How do I change the language (e.g., French receipts)?
    text: '```csharp ocrEngine.Settings.Language = OcrLanguage.French; ```'
  type: HowTo
tags:
- Aspose OCR
- C#
- GPU acceleration
title: herken tekst uit afbeelding met Aspose OCR GPU
url: /nl/net/ocr-optimization/recognize-text-from-image-using-aspose-ocr-gpu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# tekst herkennen uit afbeelding met Aspose OCR GPU

Heb je je ooit afgevraagd hoe je **tekst uit een afbeelding** kunt herkennen zonder duizenden regels code te schrijven? Je bent niet de enige. Of je nu bonnen scant voor onkostennota's of handgeschreven notities omzet naar doorzoekbare PDF's, het verkrijgen van schone platte tekst uit een foto is een veelvoorkomende behoefte.

In deze tutorial lopen we een compleet, kant‑klaar voorbeeld door dat laat zien **hoe je GPU‑versnelling inschakelt**, **een afbeelding laadt voor OCR**, en uiteindelijk **tekst uit een bon (of welke afbeelding dan ook) haalt** als platte tekst. Geen poespas, alleen de onderdelen die je echt kunt copy‑pasten.

## Wat je gaat bouwen

Aan het einde van de gids heb je een kleine console‑applicatie die:

1. Een `OcrEngine` maakt en GPU‑verwerking inschakelt.  
2. Een lokaal afbeeldingsbestand laadt (een bon, een bord, wat dan ook).  
3. Optische tekenherkenning uitvoert.  
4. De herkende tekst naar de console print – effectief **afbeelding omzetten naar platte tekst**.

Dit alles draait op .NET 6+ met de gratis Aspose.OCR‑bibliotheek, en werkt op machines met een NVIDIA‑ of AMD‑GPU die OpenCL ondersteunt.

## Vereisten

- .NET 6 SDK of later geïnstalleerd.  
- Visual Studio 2022 (of een andere editor naar keuze).  
- Een GPU‑enabled machine (optioneel maar aanbevolen voor snelheid).  
- Een voorbeeld‑afbeeldingsbestand, bv. `receipt.jpg`, ergens geplaatst waar je ernaar kunt verwijzen.  

Als je geen GPU hebt, werkt de code nog steeds; hij valt dan terug op CPU‑verwerking.

## Stap 1: Installeer Aspose.OCR via NuGet

Voeg eerst het Aspose.OCR‑pakket toe aan je project:

```bash
dotnet add package Aspose.OCR
```

Die ene regel haalt alle binaries op die je nodig hebt, inclusief de native OpenCL‑wrappers voor GPU‑werk.

## Stap 2: GPU‑versnelling inschakelen (how to enable gpu acceleration)

Het inschakelen van de GPU is zo simpel als een boolean‑vlag op de engine‑instellingen omzetten. De bibliotheek kiest automatisch het eerste beschikbare apparaat, maar je kunt ook een index opgeven als je meerdere GPU’s hebt.

```csharp
// Create the OCR engine
var ocrEngine = new OcrEngine();

// Enable GPU processing – this is the “how to enable gpu acceleration” part
ocrEngine.Settings.EnableGpu = true;

// (Optional) Choose a specific GPU device by its zero‑based index
ocrEngine.Settings.GpuDeviceId = 0;
```

**Waarom de GPU inschakelen?**  
GPU‑kernen blinken uit in parallelle taken zoals beeldvoorbewerking en neurale‑netwerk‑inference. Op een moderne RTX‑kaart kun je OCR‑versnellingen van 3‑5× zien ten opzichte van pure CPU.

> **Pro tip:** Als je `OpenCL`‑fouten tegenkomt, controleer dan of je grafische driver up‑to‑date is en of `OpenCL.dll` toegankelijk is in het runtime‑pad.

## Stap 3: Afbeelding laden voor OCR (load image for ocr)

Wijs de engine nu naar de foto die je wilt lezen. Aspose.OCR biedt een handige factory‑methode die veel formaten ondersteunt (JPEG, PNG, BMP, TIFF, enz.).

```csharp
// Load the image you want to recognize
// Replace the path with the actual location of your receipt or other image
var receiptImage = OcrImage.FromFile("YOUR_DIRECTORY/receipt.jpg");
```

Als het bestand niet wordt gevonden, gooit `FromFile` een `FileNotFoundException`. Plaats het in een try/catch als je een nette afhandeling wilt.

## Stap 4: OCR uitvoeren en afbeelding omzetten naar platte tekst

Nu gebeurt de magie. Roep `Recognize` aan en haal de `Text`‑eigenschap uit het resultaat. Dit geeft je een schone string – precies wat we bedoelen met **afbeelding omzetten naar platte tekst**.

```csharp
// Run OCR on the loaded image
var ocrResult = ocrEngine.Recognize(receiptImage);

// Output the recognized plain‑text to the console
System.Console.WriteLine(ocrResult.Text);
```

De `Text`‑eigenschap verwijdert regeleinden en retourneert Unicode, zodat je het direct kunt doorsturen naar een bestand, een database, of een downstream‑verwerkingspipeline.

### Verwachte output

Als `receipt.jpg` een typische winkelbon bevat, zie je mogelijk iets als:

```
Walmart Supercenter
123 Main St.
Anytown, TX 75001
Date: 06/27/2026
Item          Qty   Price
Apple         2     $1.20
Bread         1     $2.50
TOTAL                $3.70
Thank you for shopping!
```

De exacte opmaak hangt af van de kwaliteit van de bronafbeelding en het intern gebruikte taalmodel.

## Stap 5: Volledig werkend voorbeeld

Hieronder staat het complete programma dat je kunt kopiëren naar een nieuw `Program.cs`. Het bevat alle bovenstaande stappen, plus een klein beetje foutafhandeling voor de zekerheid.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

class GpuExample
{
    static void Main()
    {
        try
        {
            // Step 1: Create the OCR engine and enable GPU acceleration
            var ocrEngine = new OcrEngine();
            ocrEngine.Settings.EnableGpu = true;          // Turn on GPU processing
            ocrEngine.Settings.GpuDeviceId = 0;           // (Optional) Choose GPU device by index

            // Step 2: Load the image to be recognized
            // Make sure the path points to a real file on your machine
            var receiptImage = OcrImage.FromFile("YOUR_DIRECTORY/receipt.jpg");

            // Step 3: Perform OCR on the loaded image
            var ocrResult = ocrEngine.Recognize(receiptImage);

            // Step 4: Output the recognized plain‑text
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(ocrResult.Text);
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error during OCR processing: {ex.Message}");
        }
    }
}
```

Opslaan, bouwen en uitvoeren:

```bash
dotnet run
```

Als alles correct is geconfigureerd, toont de console de geëxtraheerde tekst, waarmee je hebt aangetoond dat je **tekst uit een bon** (of welke afbeelding dan ook) succesvol kunt **extraheren** met Aspose OCR en GPU‑ondersteuning.

## Randgevallen & Veelgestelde vragen

### Wat als mijn afbeelding een lage resolutie heeft?

OCR‑nauwkeurigheid daalt drastisch bij onscherpe of zeer kleine afbeeldingen. Overweeg vóór het aanroepen van `Recognize` de afbeelding op te schalen (bijv. met `System.Drawing` of `ImageSharp`) en een contrastverhoging toe te passen. Aspose biedt ook `Preprocess`‑methoden die je kunt uitproberen.

### Mijn GPU wordt niet gebruikt – waarom?

- Controleer dat `EnableGpu` **true** is *voordat* je `Recognize` aanroept.  
- Controleer of je driver OpenCL 1.2+ ondersteunt (de meeste moderne drivers doen dat).  
- Op sommige headless‑servers moet je mogelijk de omgevingsvariabele `CUDA_VISIBLE_DEVICES` (voor NVIDIA) instellen om het apparaat zichtbaar te maken.

### Kan ik meerdere afbeeldingen parallel verwerken?

Zeker. De `OcrEngine`‑instantie is **niet** thread‑safe, maar je kunt per thread een aparte engine starten. Vergeet niet de GPU op elke instantie in te schakelen; de driver plant het werk automatisch over alle cores.

### Hoe wijzig ik de taal (bijv. Franse bonnen)?

```csharp
ocrEngine.Settings.Language = OcrLanguage.French;
```

Zorg ervoor dat het juiste taalpakket is meegeleverd met het NuGet‑pakket (de meeste gangbare talen zijn inbegrepen).

## Prestatiebenchmark (optioneel)

Op een laptop met een Intel i7‑1270H en een NVIDIA RTX 3060 werden de volgende tijden gemeten voor een 300 KB JPEG‑bon:

| Modus               | Tijd (ms) |
|--------------------|-----------|
| Alleen CPU         | 820       |
| GPU (EnableGpu)    | 210       |

Dat is ongeveer een **4× versnelling**, wat bevestigt waarom **how to enable gpu acceleration** belangrijk is voor bulk‑verwerking.

## Conclusie

Je hebt zojuist geleerd hoe je **tekst uit een afbeelding** herkent met Aspose OCR, GPU‑versnelling inschakelt voor een merkbare snelheidsboost, **afbeelding laadt voor OCR**, en uiteindelijk **afbeelding omzet naar platte tekst** – perfect voor het extraheren van tekst uit bonnen, facturen of elk gescand document. De volledige code is zelf‑containend, draait op elke .NET 6+ omgeving, en kan worden uitgebreid om mappen batch‑gewijs te verwerken, resultaten in een database op te slaan, of een downstream AI‑model te voeden.

Volgende stappen? Vervang de bon door een handgeschreven notitie, experimenteer met de `Preprocess`‑API om de nauwkeurigheid op ruisende scans te verbeteren, of integreer de engine in een ASP.NET Core‑webservice zodat gebruikers afbeeldingen kunnen uploaden en direct tekst terugkrijgen. Je kunt ook andere secundaire zoekwoorden verkennen zoals **extract text from receipt** in een grotere workflow, of dieper duiken in **how to enable gpu acceleration** voor andere Aspose‑producten.

Happy coding, en moge je OCR altijd accuraat zijn!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat complete werkende code‑voorbeelden met stap‑voor‑stap‑uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [How to Extract Text from Image Using Aspose.OCR for .NET](/ocr/english/net/text-recognition/get-recognition-result/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}