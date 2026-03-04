---
category: general
date: 2026-03-04
description: Tekst extraheren uit afbeelding met Aspose OCR in C#. Leer hoe je een
  afbeelding laadt voor OCR en efficiënt tekst herkent uit TIFF‑bestanden.
draft: false
keywords:
- extract text from image
- load image for ocr
- recognize text from tiff
- Aspose OCR C#
- GPU OCR engine
language: nl
og_description: Tekst extraheren uit een afbeelding met Aspose OCR in C#. Deze gids
  laat zien hoe je een afbeelding laadt voor OCR en tekst herkent uit TIFF‑bestanden
  met een GPU‑engine.
og_title: Tekst uit afbeelding halen met Aspose OCR – C#‑tutorial
tags:
- OCR
- C#
- Aspose
- GPU
title: Tekst extraheren uit afbeelding met Aspose OCR – Complete C#-gids
url: /nl/net/text-recognition/extract-text-from-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tekst uit afbeelding extraheren met Aspose OCR – Complete C# Gids

Heb je ooit **tekst uit afbeelding** moeten extraheren maar wist je niet welke bibliotheek zowel snelheid als nauwkeurigheid biedt? Je bent niet de enige—veel ontwikkelaars lopen tegen die muur aan bij het verwerken van gescande PDF's of TIFF-archieven. Het goede nieuws is dat Aspose OCR, gecombineerd met een GPU‑enabled engine, het hele proces als een fluitje van een cent laat aanvoelen.

In deze tutorial laten we je precies zien hoe je **afbeelding laadt voor OCR**, een GPU-engine instelt, en uiteindelijk **tekst uit TIFF** bestanden herkent in slechts een handvol regels. Aan het einde heb je een uitvoerbare console‑app die de geëxtraheerde tekst naar de console print, en begrijp je het “waarom” achter elke stap.

## Wat je zult leren

- Hoe je het Aspose.OCR NuGet‑pakket installeert en referentieert.
- Waarom een GPU‑versnelde `GpuOcrEngine` de verwerkingstijd drastisch kan verkorten.
- De juiste manier om **afbeelding te laden voor OCR** te gebruiken met `ImageInfo`.
- Hoe je taalinstellingen en geheugenlimieten configureert.
- Hoe je **tekst uit TIFF** herkent en veelvoorkomende valkuilen afhandelt.

Ervaring met Aspose is niet vereist; een basiskennis van C# en .NET is voldoende. Laten we beginnen.

---

## Stap 1: Tekst uit afbeelding extraheren – Initialiseer de GPU OCR-engine

Het eerste dat we nodig hebben is een OCR‑engine die daadwerkelijk de pixels kan lezen. Aspose biedt een `GpuOcrEngine` die het zware werk naar je grafische kaart uitbesteedt. Dit is vooral handig wanneer je tientallen high‑resolution TIFF‑bestanden in een wachtrij hebt staan.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;

// Create a GPU‑enabled OCR engine.
// Setting GpuMemoryLimit helps avoid out‑of‑memory crashes on modest GPUs.
GpuOcrEngine ocrEngine = new GpuOcrEngine
{
    GpuMemoryLimit = 1024 // limit to 1024 MB
};
```

**Waarom dit belangrijk is:**  
Een alleen‑CPU‑engine zou elke pixel sequentieel scannen, wat pijnlijk traag kan zijn voor grote afbeeldingen. Door het GPU‑geheugen te beperken, houd je het proces lichtgewicht terwijl je toch profiteert van de prestatieboost.

> **Pro tip:** Als je op een server zonder GPU draait, schakel dan terug naar `OcrEngine`—de API is identiek, vervang alleen de klassenaam.

---

## Stap 2: Afbeelding laden voor OCR – Het TIFF‑bestand voorbereiden

Nu de engine klaar is, moeten we **afbeelding laden voor OCR**. Aspose’s `ImageInfo.Load` begrijpt een breed scala aan formaten, inclusief multi‑page TIFF‑bestanden. Wijs het op je bestand en laat de bibliotheek de rest afhandelen.

```csharp
// Replace the path with the location of your TIFF file.
string imagePath = @"YOUR_DIRECTORY/english_page.tif";

// Load the image into an ImageInfo object.
// ImageInfo abstracts away format specifics, giving you a uniform API.
ImageInfo image = ImageInfo.Load(imagePath);
```

**Randgeval:**  
Als je TIFF meerdere pagina's bevat, kun je itereren over `image.Pages` en elke pagina afzonderlijk verwerken. Voor de meeste single‑page scans is de bovenstaande regel alles wat je nodig hebt.

---

## Stap 3: Tekst uit TIFF herkennen – Het OCR‑proces uitvoeren

Met de afbeelding in het geheugen en de engine klaar, herkennen we eindelijk **tekst uit TIFF**. De `Recognize`‑methode retourneert een `OcrResult`‑object dat de geëxtraheerde string, vertrouwensscores, en zelfs begrenzingskaders bevat als je die later nodig hebt.

```csharp
// Set the language you expect in the image.
// English is the default, but you can combine languages like Language.English | Language.Spanish.
ocrEngine.Language = Language.English;

// Run the OCR process.
OcrResult ocrResult = ocrEngine.Recognize(image);
```

**Waarom taal belangrijk is:**  
Het specificeren van de juiste taal verbetert de nauwkeurigheid drastisch omdat de engine taal‑specifieke woordenboeken en tekensmodellen kan toepassen.

---

## Stap 4: De geëxtraheerde tekst weergeven

De laatste stap is triviaal—schrijf het resultaat gewoon naar de console, een bestand, of een database. Hier houden we het simpel en tonen we de tekst op het scherm.

```csharp
// Print the recognized text.
Console.WriteLine("=== Extracted Text ===");
Console.WriteLine(ocrResult.Text);
```

**Verwachte output:**  
Als `english_page.tif` een afgedrukte alinea bevat, zie je iets als:

```
=== Extracted Text ===
The quick brown fox jumps over the lazy dog.
```

Als de OCR moeite heeft, kan de tekst vreemde tekens bevatten; het aanpassen van `GpuMemoryLimit` of het leveren van een bronafbeelding met hogere resolutie helpt meestal.

---

## Volledig werkend voorbeeld

Hieronder staat het volledige, zelfstandige programma dat je kunt kopiëren en plakken in een nieuw Console‑App‑project. Het compileert met .NET 6 of later.

```csharp
// ------------------------------------------------------------
// Complete C# program to extract text from image using Aspose OCR.
// ------------------------------------------------------------
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize GPU OCR engine with a memory cap.
        GpuOcrEngine ocrEngine = new GpuOcrEngine
        {
            GpuMemoryLimit = 1024 // MB
        };

        // 2️⃣ Choose the language for recognition.
        ocrEngine.Language = Language.English;

        // 3️⃣ Load the image you want to process.
        // Make sure the path points to a valid TIFF file.
        string imagePath = @"YOUR_DIRECTORY/english_page.tif";
        ImageInfo image = ImageInfo.Load(imagePath);

        // 4️⃣ Perform OCR – this returns the recognized text.
        OcrResult ocrResult = ocrEngine.Recognize(image);

        // 5️⃣ Display the result.
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);

        // Keep the console window open when debugging.
        Console.WriteLine("\nPress any key to exit...");
        Console.ReadKey();
    }
}
```

Sla het bestand op, voer `dotnet run` uit, en zie hoe de console de geëxtraheerde inhoud uitspuwt. Simpel, toch?

---

## Veelgestelde vragen & randgevallen

**Wat als mijn afbeelding een PNG of JPEG is in plaats van TIFF?**  
`ImageInfo.Load` werkt met vrijwel elk rasterformaat, dus je kunt de extensie wijzigen en de rest van de code blijft hetzelfde. Geen extra aanpassingen nodig.

**Mijn OCR geeft onleesbare tekens terug—wat moet ik controleren?**  
1. Controleer de afbeeldingsresolutie (300 dpi of hoger is ideaal).  
2. Zorg ervoor dat de juiste `Language` is ingesteld; een mismatching taal vermindert de ondersteuning van woordenboeken.  
3. Verhoog `GpuMemoryLimit` als de afbeelding zeer groot is; de engine kan zichzelf beperken.

**Kan ik meerdere bestanden in één batch verwerken?**  
Zeker. Plaats de laad‑ en herkenningsstappen in een `foreach (var file in Directory.GetFiles(...))`‑lus. Vergeet niet elke `ImageInfo` te disposen als je honderden bestanden verwerkt om native resources vrij te geven.

**Heb ik een GPU nodig om deze code uit te voeren?**  
Nee. Als er geen compatibele GPU aanwezig is, vervang je `GpuOcrEngine` door de reguliere `OcrEngine`. De API‑aanroepen (`Recognize`, `Language`, etc.) blijven ongewijzigd.

---

## Prestatie‑tips – Haal het maximale uit GPU OCR

- **Herbruik de engine:** Een nieuwe `GpuOcrEngine` voor elke afbeelding maken voegt overhead toe. Instantieer deze één keer en hergebruik hem voor veel bestanden.  
- **Batchverwerking:** Laad meerdere afbeeldingen in het geheugen, roep dan `Recognize` opeenvolgend aan; de GPU blijft warm en verwerkt sneller.  
- **Pas geheugenlimiet aan:** Op machines met 4 GB VRAM is een limiet van 1024 MB veilig. Op high‑end werkstations kun je deze verhogen naar 4096 MB voor grotere batches.

---

## Conclusie

Je hebt zojuist geleerd hoe je **tekst uit afbeelding** kunt extraheren met de GPU‑engine van Aspose OCR, hoe je correct **afbeelding laadt voor OCR**, en hoe je **tekst uit TIFF** bestanden herkent in een nette, productie‑klare C# console‑app. De code is volledig uitvoerbaar, de uitleg behandelt zowel het “hoe” als het “waarom”, en je hebt nu een solide basis om complexere OCR‑scenario’s aan te pakken—zoals meertalige documenten of realtime camerafeeds.

Klaar voor de volgende uitdaging? Probeer het voorbeeld uit te breiden om de output naar een CSV te schrijven, of experimenteer met de `BoundingBox`‑gegevens om herkende woorden in de originele afbeelding te markeren. De mogelijkheden zijn eindeloos, en de prestatie‑winst door GPU‑versnelling houdt je pipelines snel.

Als je deze gids nuttig vond, geef hem een ster op GitHub, deel hem met een collega, of laat hieronder een reactie achter met je eigen tips. Happy coding!  

![extract text from image using Aspose OCR](placeholder.png){alt="tekst uit afbeelding extraheren met Aspose OCR"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}