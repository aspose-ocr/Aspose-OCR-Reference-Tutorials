---
category: general
date: 2026-02-09
description: Hoe gebruik je Aspose OCR met GPU-versnelling in C#. Leer tekst herkennen
  uit jpg, tekst uit een afbeelding extraheren en GPU in slechts enkele minuten inschakelen.
draft: false
keywords:
- how to use aspose
- recognize text from jpg
- extract text from image
- how to enable gpu
- how to set gpu
language: nl
og_description: Hoe gebruik je Aspose OCR met GPU in C#. Deze gids laat zien hoe je
  tekst uit een jpg herkent en tekst uit een afbeelding extraheert met GPU-versnelling.
og_title: Hoe Aspose OCR met GPU te gebruiken – Complete programmeergids
tags:
- Aspose
- OCR
- C#
- GPU Acceleration
title: Hoe gebruik je Aspose OCR met GPU – Stapsgewijze handleiding
url: /nl/net/ocr-optimization/how-to-use-aspose-ocr-with-gpu-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe Aspose OCR met GPU te gebruiken – Complete programmeergids

Heb je ooit een stapel gescande facturen in een oogwenk moeten verwerken, maar bleef de CPU haperen? Dat is een klassiek pijnpunt wanneer je probeert **how to use aspose** voor OCR op schaal te gebruiken. In deze tutorial lopen we een real‑world voorbeeld door dat laat zien **how to use aspose** tekst te herkennen uit jpg‑bestanden, tekst uit een afbeelding te extraheren, en het maximale uit je GPU te halen.

Beschouw het als een koffiepauze‑walkthrough—geen poespas, alleen de stukjes die je kunt copy‑paste in Visual Studio en de magie kunt zien gebeuren. Aan het einde heb je een zelfstandige C# console‑app die draait op elke moderne Windows‑machine met een NVIDIA‑ of AMD‑GPU.

![how to use aspose OCR with GPU](/images/aspose-gpu-example.png)

## Wat je nodig hebt

- **.NET 6.0** (of later) – de code richt zich op .NET 6 maar werkt met .NET 5 en .NET Framework 4.8 met kleine aanpassingen.
- **Aspose.OCR for .NET** NuGet‑pakket – installeer het via `dotnet add package Aspose.OCR`.
- Een **GPU‑enabled machine** – de tutorial laat zien hoe je **how to enable gpu** en **how to set gpu** geheugenlimieten instelt, maar de code valt elegant terug op CPU als er geen compatibele GPU wordt gevonden.
- Een afbeelding zoals `invoice_01.jpg` geplaatst in een map die je kunt refereren.

Heb je die? Geweldig, laten we erin duiken.

## Hoe Aspose OCR met GPU te gebruiken – Initiële setup

Het eerste wat je moet doen is een instantie van de OCR‑engine maken en aangeven dat deze de GPU moet gebruiken. Deze stap is cruciaal omdat zonder de vlag Aspose standaard CPU‑verwerking gebruikt, wat het doel van onze prestatie‑boost ondermijnt.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System;

// Step 1: Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Enable GPU acceleration – this is the core of **how to use aspose** with a graphics card
ocrEngine.Configuration.UseGpu = true;

// Optional: limit GPU memory to avoid OOM on low‑end cards
ocrEngine.Configuration.GpuMemoryLimit = 1024; // in MB
```

**Waarom dit belangrijk is:** Het inschakelen van de GPU verplaatst de zware image‑processing kernels naar de grafische processor, die 10‑20× sneller kan zijn dan de CPU voor grote afbeeldingen. De `GpuMemoryLimit` is een veiligheidsventiel; instellen op 1024 MB werkt voor de meeste mid‑range kaarten terwijl de app responsief blijft.

> **Pro tip:** Als je de app op een machine zonder compatibele GPU draait, zal Aspose automatisch terugschakelen naar CPU‑modus en een waarschuwing loggen. Geen crash, alleen een tragere uitvoering.

## Tekst herkennen uit JPG – Afbeelding laden

Nu de engine klaar is, moeten we er een afbeelding aan voeren. Het voorbeeld gebruikt een JPEG omdat **recognize text from jpg** een veelvoorkomend scenario is voor facturen, bonnetjes en paspoorten.

```csharp
// Step 2: Load the JPEG image you want to process
// Replace the path with the location of your own image
var inputImage = ImageStream.FromFile(@"C:\OCR\Samples\invoice_01.jpg");

// Verify that the file exists (helps avoid a FileNotFoundException)
if (!System.IO.File.Exists(@"C:\OCR\Samples\invoice_01.jpg"))
{
    Console.WriteLine("Image file not found. Check the path and try again.");
    return;
}
```

**Waarom we het bestand controleren:** Een ontbrekend bestand is de meest voorkomende oorzaak van runtime‑fouten in snelle demo's. Door het vroeg af te handelen, houd je de tutorial beginnersvriendelijk.

## Tekst extraheren uit afbeelding – OCR‑engine uitvoeren

Met de afbeelding in de hand, is de volgende stap het daadwerkelijk uitvoeren van het OCR‑proces. Hier doet Aspose het zware werk en retourneert een `OcrResult`‑object dat de platte tekst, confidence‑scores, en zelfs bounding boxes bevat als je die later nodig hebt.

```csharp
// Step 3: Perform OCR on the loaded image
OcrResult ocrResult = ocrEngine.Recognize(inputImage);

// Step 4: Output the extracted plain‑text
Console.WriteLine("=== Extracted Text ===");
Console.WriteLine(ocrResult.PlainText);
```

**Wat je zult zien:** De console print de ruwe karakters die Aspose heeft gedetecteerd. Voor een nette factuur krijg je iets als:

```
=== Extracted Text ===
Invoice #: 2023‑00123
Date: 02/08/2023
Total: $1,245.67
...
```

Als de output er rommelig uitziet, moet je waarschijnlijk de beeldkwaliteit aanpassen of extra preprocessing‑opties inschakelen (bijv. deskew, binarisatie). Dat valt buiten de reikwijdte van deze snelle gids, maar staat gedocumenteerd in de API‑referentie van Aspose.

## Hoe GPU in te schakelen – Engine configureren

Je vraagt je misschien af **how to enable gpu** voor Aspose als je de eerste stap gemist hebt. Het antwoord is simpelweg het schakelen van de `UseGpu`‑vlag op het configuratie‑object van de engine, zoals eerder getoond. Hier is een beknopt fragment dat je in elk bestaand project kunt plaatsen:

```csharp
ocrEngine.Configuration.UseGpu = true;   // Enables GPU
```

Achter de schermen laadt Aspose native CUDA/OpenCL‑bibliotheken die passen bij je hardware. Als de runtime ze niet kan vinden, logt het een waarschuwing en schakelt terug naar CPU. Voor de meeste Windows‑installaties zijn geen extra installatie‑stappen nodig.

## Hoe GPU in te stellen – Geheugengebruik fijn afstellen

Soms krijg je een “out of memory”‑fout op een low‑end GPU. Dan komen **how to set gpu** geheugenlimieten van pas. De eigenschap `GpuMemoryLimit` accepteert een integer die megabytes vertegenwoordigt.

```csharp
// Example: restrict GPU usage to 512 MB
ocrEngine.Configuration.GpuMemoryLimit = 512;
```

**Wanneer aan te passen:** Als je veel afbeeldingen parallel verwerkt, verlaag dan de limiet om te voorkomen dat de kaart verzadigd raakt. Omgekeerd, op een workstation met 8 GB VRAM kun je het veilig verhogen tot 4096 MB voor snellere batch‑verwerking.

## Volledig, uitvoerbaar voorbeeld

Hieronder staat het volledige programma dat je kunt kopiëren naar een nieuw console‑project (`dotnet new console`). Het bevat alle besproken onderdelen, plus een klein beetje foutafhandeling om het robuust te maken.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System;

class GpuExample
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Create the OCR engine and enable GPU
        // -------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.Configuration.UseGpu = true;            // how to enable gpu
        ocrEngine.Configuration.GpuMemoryLimit = 1024;   // how to set gpu

        // -------------------------------------------------
        // Step 2: Load the JPEG image you want to process
        // -------------------------------------------------
        string imagePath = @"C:\OCR\Samples\invoice_01.jpg";

        if (!System.IO.File.Exists(imagePath))
        {
            Console.WriteLine($"File not found: {imagePath}");
            return;
        }

        var inputImage = ImageStream.FromFile(imagePath);

        // -------------------------------------------------
        // Step 3: Run the OCR engine
        // -------------------------------------------------
        OcrResult ocrResult = ocrEngine.Recognize(inputImage);

        // -------------------------------------------------
        // Step 4: Display the extracted text
        // -------------------------------------------------
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.PlainText);
    }
}
```

**Verwachte output:** Na het uitvoeren van `dotnet run` zal de console de ruwe tekst afdrukken die is geëxtraheerd uit `invoice_01.jpg`. Als de afbeelding duidelijke gedrukte tekst bevat, zou het resultaat bijna identiek moeten zijn aan het originele document.

## Veelvoorkomende valkuilen & hoe ze te vermijden

| Issue | Why it Happens | Quick Fix |
|-------|----------------|-----------|
| **GPU niet gedetecteerd** | Ontbrekende CUDA‑drivers of niet‑ondersteunde GPU | Installeer de nieuwste NVIDIA/AMD driver; controleer met `nvidia-smi` of equivalent |
| **Out‑of‑memory fout** | `GpuMemoryLimit` te hoog voor de kaart | Verlaag de limiet tot 512 MB of minder |
| **Rommelige output** | Lage resolutie JPG of zware compressie | Gebruik een bronafbeelding van hogere kwaliteit of schakel `ocrEngine.Preprocessing.Deskew = true` in |
| **Null `ocrResult`** | Afbeeldings‑stream kon niet geladen worden | Controleer het bestandspad nogmaals en zorg dat het bestand niet vergrendeld is |

Deze problemen vooraf aanpakken bespaart je later het najagen van cryptische stack‑traces.

## Volgende stappen

Nu je **how to use aspose** voor snelle OCR onder de knie hebt, wil je misschien verkennen:

- **Batch processing** – loop over een map met JPG‑bestanden en schrijf elk resultaat naar een `.txt`‑bestand.
- **Structured extraction** – gebruik `ocrResult.Regions` om bounding boxes te krijgen en specifieke velden zoals factuurnummers eruit te halen.
- **Hybrid CPU/GPU mode** – gebruik CPU voor kleine afbeeldingen en schakel alleen naar GPU voor grote bestanden om snelheid en geheugen in balans te houden.

Al deze uitbreidingen bouwen voort op dezelfde basis die je zojuist hebt opgezet, en ze zijn perfecte onderwerpen voor je volgende tutorial‑avontuur.

---

*Veel plezier met coderen! Als je ergens vastloopt, laat dan een reactie achter of ping de Aspose community‑forums. De GPU staat klaar—laten we OCR bliksemsnel maken.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}