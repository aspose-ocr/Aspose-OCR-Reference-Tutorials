---
category: general
date: 2025-12-30
description: Hoe een afbeelding snel rechtzetten en leren hoe je het contrast kunt
  verhogen tijdens het extraheren van tekst uit een afbeelding voor verbeterde OCR-nauwkeurigheid.
draft: false
keywords:
- how to deskew image
- how to boost contrast
- extract text from image
- recognize text image
- improve ocr accuracy
language: nl
og_description: Hoe je een afbeelding snel kunt rechtzetten en leert hoe je het contrast
  kunt verhogen tijdens het extraheren van tekst uit een afbeelding voor verbeterde
  OCR-nauwkeurigheid.
og_title: Hoe een afbeelding rechtzetten en het contrast verhogen voor betere OCR‑nauwkeurigheid
tags:
- OCR
- C#
- Image Processing
title: Hoe een afbeelding rechtzetten en het contrast verhogen voor betere OCR-nauwkeurigheid
url: /nl/net/ocr-optimization/how-to-deskew-image-and-boost-contrast-for-better-ocr-accura/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe een afbeelding rechtzetten en het contrast verhogen voor betere OCR-nauwkeurigheid

Heb je je ooit afgevraagd **hoe je een afbeelding kunt rechtzetten** die afkomstig is van een scanner of een smartphone?  
Je bent niet de enige—de meeste ontwikkelaars lopen tegen dit probleem aan wanneer de bronafbeelding een beetje scheef of ruisig is, en de OCR-uitvoer eindigt als een warboel.  

Het goede nieuws is dat je met een paar regels C# de afbeelding kunt rechtzetten, de achtergrond kunt opschonen en zelfs het contrast kunt verhogen zodat de engine de tekst als een professional leest. In deze gids laten we je ook zien hoe je **tekst uit een afbeelding kunt extraheren** en **tekstafbeelding kunt herkennen** met Aspose.OCR, terwijl je **OCR-nauwkeurigheid verbeteren** altijd in gedachten houdt.

## Wat je nodig hebt

- **.NET 6.0** of later (de code compileert ook op .NET Framework 4.7+)  
- **Aspose.OCR** NuGet‑pakket (versie 23.12 of nieuwer) – installeer via `dotnet add package Aspose.OCR`  
- Een voorbeeldafbeelding die zowel gedraaid als ruisig is (bijv. `noisy_rotated.jpg`)  
- Visual Studio, VS Code, of elke IDE die je verkiest  

Dat is alles—geen extra native libraries, geen zware OpenCV‑bindings. Gewoon pure managed code.

---

## Stap 1: Het project instellen en namespaces importeren

Maak eerst een nieuwe console‑applicatie aan en breng de benodigde namespaces in scope. Deze stap vormt de basis voor alles wat volgt.

```csharp
// Program.cs
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll fill this in later
        }
    }
}
```

**Waarom dit belangrijk is:**  
`Aspose.OCR` levert de `OcrEngine`‑klasse, terwijl `Aspose.OCR.Filters` handige pre‑processing filters biedt zoals `DeskewFilter` en `ContrastBoostFilter`. Ze vooraf importeren houdt de code overzichtelijk en geeft de compiler aan wat we gaan gebruiken.

---

## Stap 2: Initialiseer de OCR‑engine en voeg een Deskew‑filter toe

Nu gaan we daadwerkelijk **hoe je een afbeelding kunt rechtzetten**. Het `DeskewFilter` detecteert automatisch de rotatiehoek (tot een maximum dat je instelt) en roteert de bitmap terug naar horizontaal.

```csharp
// Inside Main()
var ocrEngine = new OcrEngine();

// Deskew: correct up to 15 degrees of rotation
ocrEngine.Filters.Add(new DeskewFilter { MaxAngle = 15 });
```

**Wat er onder de motorkap gebeurt:**  
Het filter scant de afbeelding op de langste horizontale tekstregel, schat de kanteling in en past een inverse rotatie toe. Door `MaxAngle` te beperken tot 15° voorkomen we over‑correctie van afbeeldingen die al recht zijn.

> **Pro tip:** Als je bronafbeeldingen mogelijk ondersteboven zijn, verhoog `MaxAngle` naar 180°—het filter zal nog steeds de juiste oriëntatie vinden.

---

## Stap 3: Ruis verminderen met een Denoise‑filter

Een ruisige scan kan zelfs de slimste OCR‑engine misleiden. Het toevoegen van een `DenoiseFilter` maakt vlekjes glad zonder fijne details te wissen.

```csharp
// Denoise: strength ranges from 0 (off) to 1 (max)
ocrEngine.Filters.Add(new DenoiseFilter { Strength = 0.7 });
```

**Waarom je het nodig hebt:**  
Ruis creëert valse randen die het OCR‑algoritme als tekens interpreteert. Een sterkte van `0.7` is een goede balans voor de meeste gescande documenten; voel je vrij om het aan te passen voor zeer schone of zeer vuile invoer.

---

## Stap 4: Contrast verhogen – “Hoe contrast te verhogen” in actie

Hier beantwoorden we het secundaire zoekwoord **hoe contrast te verhogen**. Het `ContrastBoostFilter` vergroot het verschil tussen donkere tekst en de lichte achtergrond, waardoor de letters opvallen.

```csharp
// Contrast boost: level > 1 increases contrast
ocrEngine.Filters.Add(new ContrastBoostFilter { Level = 1.3 });
```

**De reden:**  
Hoger contrast verkleint de kans dat vage streken gemist worden. Een niveau van `1.3` werkt goed voor typische zwart‑op‑wit documenten; voor kleurenfoto's heb je misschien `1.5` of meer nodig.

---

## Stap 5: Voer OCR uit en extraheer de tekst

Met de afbeelding voorbewerkt, **extraheren we tekst uit een afbeelding** met de `Recognize`‑methode. De methode retourneert een `OcrResult`‑object dat de ruwe string en vertrouwensscores bevat.

```csharp
// Perform OCR on the prepared image
var ocrResult = ocrEngine.Recognize("YOUR_DIRECTORY/noisy_rotated.jpg");

// Output the recognized text
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);
```

**Wat je krijgt:**  
`ocrResult.Text` bevat de platte‑tekstrepresentatie van alles wat de engine kon lezen. Als je woord‑niveau vertrouwen nodig hebt, bekijk dan `ocrResult.Regions`—elke regio bevat een `Confidence`‑eigenschap.

---

## Volledig werkend voorbeeld (klaar om te kopiëren en plakken)

Hieronder staat het volledige programma dat je in `Program.cs` kunt plakken. Zorg ervoor dat het afbeeldingspad naar een echt bestand op je machine wijst.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize OCR engine
            var ocrEngine = new OcrEngine();

            // 2️⃣ Deskew – correct up to 15° rotation
            ocrEngine.Filters.Add(new DeskewFilter { MaxAngle = 15 });

            // 3️⃣ Denoise – smooth out speckles (strength 0.7)
            ocrEngine.Filters.Add(new DenoiseFilter { Strength = 0.7 });

            // 4️⃣ Contrast boost – make text pop (level 1.3)
            ocrEngine.Filters.Add(new ContrastBoostFilter { Level = 1.3 });

            // 5️⃣ Recognize the image
            var imagePath = @"YOUR_DIRECTORY\noisy_rotated.jpg";
            var ocrResult = ocrEngine.Recognize(imagePath);

            // 6️⃣ Show the result
            Console.WriteLine("=== OCR Output ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

**Verwachte output (voorbeeld):**

```
=== OCR Output ===
Invoice #12345
Date: 2024-09-30
Total Amount: $1,250.00
Thank you for your business!
```

Als het resultaat er rommelig uitziet, controleer dan de beeldkwaliteit, pas `Strength` of `Level` aan, of verhoog `MaxAngle` voor agressievere rechtzetting.

---

## Veelgestelde vragen & randgevallen

### Wat als de afbeelding ondersteboven is?

Stel `MaxAngle = 180` in het `DeskewFilter`. Het filter detecteert een rotatie van 180° en draait de afbeelding correct.

### Mijn document is gekleurd (bijv. een gescand formulier met blauwe markeringen).

Probeer een `ColorFilter` toe te voegen vóór de contrastverhoging, of converteer de afbeelding handmatig naar grijstinten:

```csharp
ocrEngine.Filters.Add(new GrayscaleFilter());
```

### Ik moet veel bestanden in één batch verwerken.

Wrap de OCR‑logica in een `foreach`‑loop die over een map iterereert:

```csharp
foreach (var file in Directory.GetFiles(@"C:\Scans", "*.jpg"))
{
    var result = ocrEngine.Recognize(file);
    File.WriteAllText(Path.ChangeExtension(file, ".txt"), result.Text);
}
```

### Hoe weet ik de OCR‑vertrouwen?

Inspecteer `ocrResult.Regions`:

```csharp
foreach (var region in ocrResult.Regions)
{
    Console.WriteLine($"Text: {region.Text} – Confidence: {region.Confidence:P2}");
}
```

Hogere vertrouwenswaarden (dicht bij 100%) betekenen meestal dat de voorbewerkingsstappen geslaagd zijn.

---

## Tips voor het maximaliseren van OCR‑nauwkeurigheid

| Tip | Waarom het helpt |
|-----|-------------------|
| **Gebruik verliesvrije beeldformaten** (PNG, TIFF) | JPEG‑compressie kan randen vervagen, wat de herkenning schaadt. |
| **Houd de DPI op 300+** | Meer pixels per teken geven de engine meer gegevens om mee te werken. |
| **Snijd irrelevante marges bij** | Vermindert ruis en versnelt de verwerking. |
| **Pas een binaire drempel toe** (zwart/wit) na contrastverhoging voor pure tekstdocumenten | Vereenvoudigt de afbeelding tot twee kleuren, wat de meeste OCR‑engines waarderen. |
| **Test eerst met een kleine steekproef** | Staat je toe `Strength` en `Level` fijn af te stellen voordat je opschaalt. |

---

## Conclusie

We hebben stap voor stap **hoe je een afbeelding kunt rechtzetten**, **hoe je contrast kunt verhogen**, en de volledige pipeline om **tekst uit een afbeelding te extraheren** met Aspose.OCR behandeld. Door een `DeskewFilter`, `DenoiseFilter` en `ContrastBoostFilter` te combineren vóór het aanroepen van `Recognize`, zul je een merkbare verbetering zien in **OCR‑nauwkeurigheid verbeteren** voor de meeste scans uit de praktijk.

Probeer de code uit, pas de filterparameters aan op jouw documenteigenschappen, en je zult moeiteloos schone tekst halen uit zelfs de rommeligste foto’s. Wil je verder gaan? Voeg taalspecifieke woordenboeken toe, of voer de output in een spellingscontrole voor nabewerking.

Veel programmeerplezier, en moge je OCR‑resultaten altijd kristalhelder zijn!

---

![how to deskew image example](deskew_example.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}