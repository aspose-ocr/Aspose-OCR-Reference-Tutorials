---
category: general
date: 2026-01-02
description: Voer OCR snel uit op PNG met Aspose OCR en GPU-ondersteuning. Leer hoe
  je tekst uit een afbeelding herkent, tekst uit een afbeelding extraheert en de GPU‑geheugenlimiet
  instelt.
draft: false
keywords:
- run OCR on PNG
- recognize text from image
- extract text from image
- how to extract text
- set GPU memory limit
language: nl
og_description: Voer OCR uit op PNG's efficiënt door gebruik te maken van Aspose OCR
  en GPU-versnelling. Deze tutorial laat zien hoe je tekst uit een afbeelding herkent,
  tekst uit een afbeelding extraheert en het GPU-geheugenbeheer regelt.
og_title: OCR uitvoeren op PNG met GPU – Complete C#‑gids
tags:
- OCR
- C#
- GPU
title: OCR uitvoeren op PNG met GPU – Complete C#-gids
url: /nl/net/ocr-optimization/run-ocr-on-png-with-gpu-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR uitvoeren op PNG met GPU – Complete C#‑gids

Heb je ooit **OCR op PNG**‑bestanden moeten uitvoeren maar liep je tegen prestatieproblemen aan? Je bent niet de enige. In veel real‑world pipelines kan één enkele high‑resolution PNG een CPU‑enige OCR‑engine vertragen, waardoor een snelle lookup verandert in een minuut‑lange wachttijd.  

Het goede nieuws is dat Aspose OCR wordt geleverd met GPU‑extensies waarmee je **tekst uit afbeelding** kunt herkennen in een fractie van de tijd. In deze tutorial lopen we stap voor stap door een hands‑on voorbeeld dat precies laat zien hoe je **OCR op PNG** uitvoert met C#, hoe je **tekst uit afbeelding** extraheert, en zelfs hoe je **GPU‑geheugenlimiet instelt** zodat je binnen je hardwarebudget blijft.

We behandelen ook het “hoe” en het “waarom” achter elke stap, zodat je niet alleen een copy‑paste snippet krijgt, maar een solide mentaal model ontwikkelt.

## Wat je zult leren

- De vereisten voor het gebruik van Aspose OCR’s GPU‑ondersteuning.  
- Hoe je een PNG laadt in een `Bitmap` en deze aan de OCR‑engine voedt.  
- Hoe je `GpuDevice` en `GpuMemoryLimitMb` configureert voor optimale prestaties.  
- Hoe je **tekst uit afbeelding** herkent en het platte‑tekst resultaat ophaalt.  
- Tips voor het omgaan met veelvoorkomende randgevallen zoals GPU’s met weinig geheugen of multi‑page PNG’s.  

Aan het einde van deze gids kun je **OCR op PNG**‑bestanden uitvoeren met GPU‑snelheid en de geheugenvoetafdruk van je OCR‑taken zelfverzekerd beheren.

![Diagram dat OCR op PNG met GPU‑versnelling toont](run-ocr-on-png-diagram.png "voorbeeld van OCR op PNG")

## Vereisten

Voordat we beginnen, zorg dat je het volgende hebt:

1. .NET 6.0 of later (de code werkt ook met .NET Core en .NET Framework).  
2. Een NVIDIA‑GPU met CUDA‑ondersteuning (het voorbeeld kiest apparaat‑index 0).  
3. Het Aspose.OCR NuGet‑pakket en de GPU‑extensies (`Aspose.OCR.Extensions`).  
4. Een voorbeeld‑PNG (`input.png`) geplaatst in een map die je vanuit je project kunt refereren.  

Als een van deze onbekend klinkt, geen zorgen — we vermelden alternatieven waar relevant.

---

## Stap 1 – Installeer Aspose OCR en GPU‑extensies

Allereerst. Zonder de juiste bibliotheken compileert de rest van de code niet.

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Extensions
```

Het `Aspose.OCR.Extensions`‑pakket haalt de native CUDA‑binaries binnen die nodig zijn voor GPU‑versnelling.  
*Pro tip:* Als je op een machine zonder GPU werkt, kun je het project nog steeds compileren; stel later gewoon `PreferGpu = false` in.

---

## Stap 2 – Laad de PNG die je wilt verwerken

Nu voeren we daadwerkelijk **OCR op PNG** uit door deze te laden in een `Bitmap`. Deze stap is eenvoudig maar verdient een korte opmerking: `Bitmap` verwacht een bestandspad, dus zorg dat het pad correct is ten opzichte van je uitvoerbare bestand.

```csharp
using System.Drawing;        // Bitmap handling
using Aspose.OCR;
using Aspose.OCR.Extensions; // GPU support extensions

// ...

// Step 2: Load the PNG image
string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "YOUR_DIRECTORY", "input.png");
Bitmap imageBitmap = new Bitmap(imagePath);
```

Als de PNG ongewoon groot is (bijv. > 5000 px aan één kant), wil je deze eerst verkleinen om GPU‑geheugenuitputting te voorkomen. Daar komt later de **GPU‑geheugenlimiet instellen** optie van pas.

---

## Stap 3 – Maak de OCR‑engine aan en configureer deze voor GPU‑gebruik

Hier is het hart van de tutorial: de OCR‑engine configureren om **tekst uit afbeelding** te **herkennen** met de GPU. Twee eigenschappen zijn cruciaal:

- `GpuDevice` – selecteert welk CUDA‑apparaat gebruikt wordt.  
- `GpuMemoryLimitMb` – stelt een maximum in voor het GPU‑geheugen dat de engine mag toewijzen.

```csharp
// Step 3: Initialize OCR engine with GPU settings
OcrEngine ocrEngine = new OcrEngine()
{
    // Pick the first CUDA device (index 0)
    GpuDevice = GpuDeviceInfo.GetDevice(0),

    // Optional: limit GPU memory consumption (in MB)
    GpuMemoryLimitMb = 2048   // Adjust based on your GPU's VRAM
};
```

**Waarom een geheugenlimiet instellen?** Sommige GPU’s delen geheugen met het display of draaien meerdere workloads tegelijk. Door de toewijzing te begrenzen voorkom je out‑of‑memory‑crashes, vooral bij het parallel verwerken van veel PNG’s.

---

## Stap 4 – Definieer herkenningsopties (taal & GPU‑voorkeur)

Het `RecognitionOptions`‑object vertelt de engine welke taal gezocht moet worden en of **GPU geprefereerd** moet worden, zelfs voor kleine afbeeldingen. Voor de meeste Engelse documenten is dit voldoende, maar je kunt `Language.English` vervangen door andere ondersteunde locales.

```csharp
// Step 4: Set recognition options
RecognitionOptions recognitionOptions = new RecognitionOptions
{
    Language = Language.English,
    PreferGpu = true // Force GPU path even for smaller images
};
```

Mocht je ooit **tekst uit afbeelding** in een andere taal dan Engels moeten **extraheren**, wijzig dan simpelweg de `Language`‑enum. De bibliotheek ondersteunt tientallen talen out‑of‑the‑box.

---

## Stap 5 – Voer de OCR uit en haal het resultaat op

Met alles aangesloten is de uiteindelijke aanroep één regel die daadwerkelijk **OCR op PNG** uitvoert en een rijk resultaatobject teruggeeft.

```csharp
// Step 5: Perform OCR
OcrResult ocrResult = ocrEngine.Recognize(imageBitmap, recognitionOptions);

// Output the extracted text
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);
```

Het `OcrResult` bevat niet alleen platte tekst (`ocrResult.Text`) maar ook confidence‑scores, bounding boxes en zelfs de originele afbeelding met gemarkeerde woorden — handig als je de extractie wilt debuggen of visualiseren.

**Verwacht resultaat** (voor een voorbeeld‑PNG met “Hello World”):

```
=== OCR Output ===
Hello World
```

Als de tekst er onleesbaar uitziet, controleer dan of de PNG niet corrupt is en of de GPU‑geheugenlimiet niet te laag staat voor de afbeeldingsgrootte.

---

## Stap 6 – Randgevallen en best‑practice tips

### GPU’s met weinig geheugen

Zie je een uitzondering zoals `CudaException: out of memory`, verlaag dan `GpuMemoryLimitMb` of split de PNG in tegels voordat je verwerkt. Tegelen kan met `Graphics.DrawImage` op een `Bitmap`‑clone.

### Meerdere PNG’s in een batch

Wanneer je een map met PNG’s verwerkt, hergebruik dan dezelfde `OcrEngine`‑instantie — éénmalig initialiseren bespaart GPU‑context‑wisselingen.

```csharp
foreach (var file in Directory.GetFiles("images", "*.png"))
{
    using var bmp = new Bitmap(file);
    var result = ocrEngine.Recognize(bmp, recognitionOptions);
    Console.WriteLine($"{Path.GetFileName(file)}: {result.Text}");
}
```

### Terugvallen op CPU

Als er geen GPU beschikbaar is, stel simpelweg `PreferGpu = false`. De engine schakelt automatisch over naar CPU zonder code‑wijzigingen.

```csharp
recognitionOptions.PreferGpu = false; // Safe CPU path
```

---

## Volledig werkend voorbeeld

Hieronder vind je het complete programma dat je kunt copy‑pasten in een nieuw console‑project. Het bevat alle bovenstaande stappen, plus een paar veiligheidscontroles.

```csharp
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Extensions; // GPU support extensions

class GpuExample
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Load the PNG image
        // -------------------------------------------------
        string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory,
                                         "YOUR_DIRECTORY", "input.png");

        if (!File.Exists(imagePath))
        {
            Console.Error.WriteLine($"File not found: {imagePath}");
            return;
        }

        using Bitmap imageBitmap = new Bitmap(imagePath);

        // -------------------------------------------------
        // Step 2: Initialize OCR engine with GPU settings
        // -------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine()
        {
            GpuDevice = GpuDeviceInfo.GetDevice(0), // First CUDA device
            GpuMemoryLimitMb = 2048                  // Adjust as needed
        };

        // -------------------------------------------------
        // Step 3: Set recognition options
        // -------------------------------------------------
        RecognitionOptions recognitionOptions = new RecognitionOptions
        {
            Language = Language.English,
            PreferGpu = true // Force GPU even for small images
        };

        // -------------------------------------------------
        // Step 4: Perform OCR
        // -------------------------------------------------
        OcrResult ocrResult = ocrEngine.Recognize(imageBitmap, recognitionOptions);

        // -------------------------------------------------
        // Step 5: Output the extracted text
        // -------------------------------------------------
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

Sla het bestand op als `Program.cs`, voer `dotnet run` uit, en je zou de geëxtraheerde tekst in de console moeten zien.

---

## Conclusie

We hebben zojuist laten zien hoe je **OCR op PNG**‑bestanden uitvoert met Aspose OCR’s GPU‑extensies, hoe je **tekst uit afbeelding** herkent, en hoe je **tekst uit afbeelding** extraheert terwijl je de **GPU‑geheugenlimiet** beheert. Door `GpuDevice` en `GpuMemoryLimitMb` te configureren houd je je applicatie snel en stabiel, zelfs op bescheiden GPU’s.

Vanaf hier kun je:

- Experimenteren met andere talen (`Language.French`, `Language.Spanish`).  
- De OCR‑stap integreren in een grotere document‑verwerkings‑pipeline.  
- Post‑processing toevoegen zoals spell‑checking of entity‑extractie om de ruwe tekst te verfijnen.  

Onthoud, de sleutel is niet alleen de code maar ook het begrijpen waarom elke instelling belangrijk is. Als je weet hoe je **GPU‑geheugenlimiet** moet instellen en wanneer je moet terugvallen op CPU, bouw je OCR‑oplossingen die elegant schalen.

Heb je vragen over een specifieke PNG‑grootte, multi‑page TIFF’s, of het troubleshooten van GPU‑fouten? Laat een reactie achter, en happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}