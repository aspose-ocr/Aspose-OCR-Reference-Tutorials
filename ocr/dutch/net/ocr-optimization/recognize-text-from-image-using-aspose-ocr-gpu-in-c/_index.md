---
category: general
date: 2026-02-20
description: Herken tekst van een afbeelding snel met de GPU-versnelling van Aspose
  OCR. Leer hoe je tekst uit een scan kunt extraheren in C# met een volledig, uitvoerbaar
  voorbeeld.
draft: false
keywords:
- recognize text from image
- extract text from scan
- Aspose OCR GPU
- C# OCR tutorial
- image to text conversion
language: nl
og_description: herken tekst van afbeelding met GPU-versnelling. Deze tutorial laat
  zien hoe je tekst uit een scan kunt extraheren in C# met Aspose OCR, compleet met
  code en tips.
og_title: tekst herkennen uit afbeelding met Aspose OCR GPU – C# gids
tags:
- Aspose
- OCR
- C#
- GPU
title: tekst herkennen uit afbeelding met Aspose OCR GPU in C#
url: /nl/net/ocr-optimization/recognize-text-from-image-using-aspose-ocr-gpu-in-c/
---

.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# tekst herkennen uit afbeelding met Aspose OCR GPU in C#

Heb je ooit **tekst uit een afbeelding moeten herkennen** terwijl het bestand enorm was en je CPU hapte? Misschien heb je een ouderwetse OCR‑bibliotheek geprobeerd en duurde het eeuwig, of waren de resultaten spotty. Het goede nieuws? Met de GPU‑versnelling van Aspose OCR kun je een gigantische gescande TIFF in enkele seconden omzetten naar schone, doorzoekbare tekst.

In deze gids lopen we stap voor stap door een volledig, kant‑en‑klaar voorbeeld dat laat zien hoe je **tekst uit scan‑bestanden** kunt **extraheren** op een GPU‑ingeschakelde machine. Geen vage verwijzingen, alleen de code die je nodig hebt, waarom elke regel belangrijk is, en een paar valkuilen om te voorkomen dat je je haar uittrekt.

## Wat je nodig hebt

- **.NET 6+** (of .NET Framework 4.7+ – de API werkt hetzelfde)
- **Aspose.OCR for .NET** NuGet‑pakket (versie 23.12 of hoger)
- Een **GPU** met CUDA‑ondersteuning (optioneel, maar veel sneller)
- Een hoge‑resolutie gescande afbeelding (bijv. `large_doc.tif`)

Als je geen GPU hebt, valt de engine automatisch terug op de CPU – zodat je het voorbeeld nog steeds kunt uitvoeren, alleen iets trager.

## Stap 1 – Installeer het Aspose.OCR‑pakket

Open je terminal of Package Manager Console en voer uit:

```bash
dotnet add package Aspose.OCR
```

Of, in Visual Studio’s NuGet‑UI, zoek naar **Aspose.OCR** en klik op *Install*. Dit haalt de kern‑OCR‑bibliotheek op plus de optionele GPU‑versnellingsassembly.

> **Pro tip:** Na de installatie, controleer de `packages`‑map op `Aspose.OCR.Acceleration.dll`. Deze is vereist voor GPU‑ondersteuning; als je op een headless server werkt, kun je deze weglaten en de code compileert nog steeds.

## Stap 2 – Initialiseert de GPU‑versnelde OCR‑engine

De `GpuOcrEngine`‑klasse detecteert automatisch elke compatibele GPU. Als je meer dan één apparaat hebt kun je een specifieke kiezen, maar de meeste ontwikkelaars laten het gewoon beslissen.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Acceleration;   // <-- enables GPU support

class GpuExample
{
    static void Main()
    {
        // Step 2.1: Create the OCR engine. It will look for a CUDA‑compatible GPU.
        GpuOcrEngine ocrEngine = new GpuOcrEngine();

        // Step 2.2 (optional): Force a particular GPU device.
        // Uncomment the line below if you know the device ID you want to use.
        // ocrEngine.Device = GpuDevice.GetById(0);
```

**Waarom dit belangrijk is:** Het éénmalig initialiseren van de GPU‑engine houdt de overhead laag. Als je de engine steeds opnieuw maakt en vernietigt binnen een lus, verlies je de prestatie‑voordelen.

## Stap 3 – Laad je hoge‑resolutie gescande afbeelding

Aspose OCR werkt met `System.Drawing.Image`. Zorg dat het bestandspad naar een echte afbeelding wijst; anders krijg je een `FileNotFoundException`.

```csharp
        // Step 3: Load the image you want to process.
        // Replace YOUR_DIRECTORY with the actual folder on your machine.
        var scannedImage = Image.FromFile(@"YOUR_DIRECTORY/large_doc.tif");
```

> **Randgeval:** Als de afbeelding groter is dan 10 000 × 10 000 px, overweeg dan eerst te down‑samplen. GPU‑geheugen is beperkt, en het proberen te laden van een enorme bitmap kan een `OutOfMemoryException` veroorzaken.

## Stap 4 – Voer OCR uit met de standaard (Latijnse) taalinstellingen

De `Recognize`‑methode retourneert een eenvoudige string. Je kunt een `OcrOptions`‑object doorgeven als je een andere taal of aangepaste preprocessing nodig hebt.

```csharp
        // Step 4: Run OCR. By default it assumes Latin script.
        string recognizedText = ocrEngine.Recognize(scannedImage);
```

**Waarom de standaard werkt:** De meeste gescande documenten – contracten, facturen, rapporten – gebruiken Latijn‑gebaseerde alfabetten. Als je Cyrillisch, Arabisch of Chinees nodig hebt, stel dan `ocrEngine.Language = "ru"` (of de juiste ISO‑code) in vóór het aanroepen van `Recognize`.

## Stap 5 – Toon of bewaar de geëxtraheerde tekst

Voor een snelle sanity‑check schrijven we het resultaat gewoon naar de console. In een echte app sla je het misschien op in een database, een `.txt`‑bestand, of voer je het in een zoekindex.

```csharp
        // Step 5: Output the OCR result.
        Console.WriteLine(recognizedText);

        // Optional: Save to a file.
        // File.WriteAllText(@"output.txt", recognizedText);
    }
}
```

### Verwachte uitvoer

Als `large_doc.tif` een eenvoudige alinea bevat zoals “Hello, world!”, zie je:

```
Hello, world!
```

Voor scans met meerdere pagina's concateneert de engine de tekst in leesvolgorde. Je kunt later splitsen met regeleinden (`\n`) als je paginagrens nodig hebt.

## Veelvoorkomende valkuilen behandelen

| Probleem | Symptoom | Oplossing |
|----------|----------|-----------|
| **Geen GPU gedetecteerd** | `ocrEngine.Device` is `null` en de verwerking is traag. | Installeer de nieuwste NVIDIA‑driver en de CUDA Toolkit (v11+). Controleer met `nvidia-smi`. |
| **Garbage collection vertragingen** | Geheugenspieken na het verwerken van veel afbeeldingen. | Roep `scannedImage.Dispose()` aan na OCR, of plaats de afbeelding in een `using`‑block. |
| **Verkeerde taal** | Vervormde tekens voor niet‑Latijnse tekst. | Stel `ocrEngine.Language` in op de juiste ISO 639‑1 code vóór `Recognize`. |
| **Zeer grote bestanden** | `OutOfMemoryException`. | Down‑sample met `Image.GetThumbnailImage` of splits de scan in tegels. |

## Volledig, kant‑en‑klaar voorbeeld

Hieronder staat het volledige programma – inclusief `using`‑directives, foutafhandeling, en een nette `using`‑block voor de afbeelding:

```csharp
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Acceleration; // GPU support

class GpuOcrDemo
{
    static void Main()
    {
        try
        {
            // Initialize the GPU‑accelerated OCR engine.
            GpuOcrEngine ocrEngine = new GpuOcrEngine();

            // OPTIONAL: Choose a specific GPU device.
            // ocrEngine.Device = GpuDevice.GetById(0);

            // Load the high‑resolution scanned image.
            string imagePath = @"YOUR_DIRECTORY/large_doc.tif";
            if (!File.Exists(imagePath))
                throw new FileNotFoundException($"Image not found: {imagePath}");

            using (Image scannedImage = Image.FromFile(imagePath))
            {
                // Perform OCR (defaults to Latin script).
                string text = ocrEngine.Recognize(scannedImage);

                // Output the extracted text.
                Console.WriteLine("=== OCR Result ===");
                Console.WriteLine(text);

                // Save to a text file (optional).
                string outputPath = Path.ChangeExtension(imagePath, ".txt");
                File.WriteAllText(outputPath, text);
                Console.WriteLine($"Text saved to {outputPath}");
            }
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error: {ex.Message}");
        }
    }
}
```

### Wat deze code doet

1. **Maakt** een `GpuOcrEngine` die automatisch de beste GPU kiest.  
2. **Laadt** de doel‑TIFF binnen een `using`‑block om gegarandeerd vrij te geven.  
3. **Roept** `Recognize` aan om de bitmap om te zetten naar een string.  
4. **Schrijft** het resultaat zowel naar de console als naar een `.txt`‑bestand naast de bronafbeelding.  
5. **Vangt** eventuele uitzonderingen af en print een vriendelijke foutmelding.

## Verder gaan – Van “tekst herkennen uit afbeelding” naar volledige document‑pijplijnen

Nu je **tekst uit scan‑bestanden** kunt **extraheren**, overweeg dan de volgende stappen:

- **Batch‑verwerking:** Loop over een map met TIFF‑bestanden en bundel de resultaten in één doorzoekbare index.  
- **Taaldetectie:** Gebruik `ocrEngine.DetectLanguage()` (indien beschikbaar) om automatisch van taal te wisselen.  
- **Post‑processing:** Laat de output door een spell‑checker of regex‑filter gaan om OCR‑artefacten op te schonen.  
- **Integratie met Azure Cognitive Search:** Stuur de geëxtraheerde tekst naar een doorzoekbare cloud‑index voor directe lookup.

Elk van deze uitbreidingen bouwt voort op hetzelfde kernpatroon dat je net zag – één keer initialiseren, afbeeldingen voeden, tekst verzamelen.

## Conclusie

Je hebt zojuist geleerd hoe je **tekst uit een afbeelding** kunt **herkennen** met de GPU‑versnelde engine van Aspose OCR in C#. Het complete, uitvoerbare voorbeeld laat zien hoe je de engine instelt, een hoge‑resolutie scan laadt, OCR uitvoert en de output afhandelt. Door de bovenstaande tips en randgeval‑afhandeling te volgen, vermijd je veelvoorkomende valkuilen en krijg je betrouwbare resultaten, of je nu werkt op een ontwikkelaar‑laptop of een productie‑server.

Klaar om meer scans om te zetten naar doorzoekbare data? Probeer een hele map te verwerken, experimenteer met niet‑Latijnse talen, of stuur de resultaten naar een full‑text zoekmachine. De mogelijkheden zijn eindeloos, en de code die je net hebt geschreven is de stevige basis die je nodig hebt.

Happy coding! 🚀

![recognize text from image example](/images/ocr-gpu

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}