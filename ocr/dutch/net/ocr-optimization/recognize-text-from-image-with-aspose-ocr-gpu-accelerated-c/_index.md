---
category: general
date: 2026-01-13
description: Leer hoe je tekst uit een afbeelding kunt herkennen en snel tekst van
  een bon kunt extraheren met Aspose OCR. Inclusief stappen voor het laden van een
  afbeelding voor OCR en het instellen van een GPU-apparaat‑ID.
draft: false
keywords:
- recognize text from image
- extract text from receipt
- load image for ocr
- set gpu device id
language: nl
og_description: herken direct tekst uit een afbeelding met Aspose OCR. Volg deze stapsgewijze
  handleiding om een afbeelding voor OCR te laden, de GPU-apparaat‑ID in te stellen
  en tekst van een bon te extraheren.
og_title: herken tekst van afbeelding – Complete GPU-versnelde C#-gids
tags:
- Aspose OCR
- C#
- GPU computing
title: herken tekst uit afbeelding met Aspose OCR – GPU‑versnelde C#‑tutorial
url: /nl/net/ocr-optimization/recognize-text-from-image-with-aspose-ocr-gpu-accelerated-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# herken tekst uit afbeelding – Complete GPU‑Versnelde C# Gids

Heb je ooit **herken tekst uit afbeelding** nodig gehad, maar vond je de CPU‑versie pijnlijk traag? Misschien probeer je **tekst uit bon** bestanden te **extraheren** en de latentie verpest de gebruikerservaring. Het goede nieuws is dat je niet hoeft te accepteren dat het traag is—het GPU‑pakket van Aspose OCR kan het proces een turbo‑boost geven, en de code is slechts een paar regels lang.

In deze tutorial lopen we een volledig, uitvoerbaar voorbeeld door dat laat zien hoe je **afbeelding laden voor OCR** configureert, de GPU instelt met **GPU‑apparaat‑ID instellen**, en uiteindelijk het platte‑tekstresultaat ophaalt. Aan het einde heb je een kant‑klaar fragment dat werkt op elke moderne Windows‑ of Linux‑machine met een ondersteunde NVIDIA‑kaart.

## Wat je nodig hebt

- **.NET 6+** (or .NET Framework 4.7.2+) – de API werkt met beide.
- **Aspose.OCR** NuGet‑pakket **plus** de **Aspose.OCR.Gpu** add‑on.
- Een NVIDIA‑GPU met minimaal 2 GB VRAM (de demo beperkt het gebruik tot 1 GB).
- Een voorbeeldafbeelding, bijv. een gescande bon (`receipt.jpg`).

Als je al een project hebt, voer dan gewoon `dotnet add package Aspose.OCR` en `dotnet add package Aspose.OCR.Gpu` uit. Er zijn geen extra native libraries nodig; de SDK levert de benodigde CUDA‑binaries.

## Stapsgewijze Implementatie

### ## Hoe tekst uit afbeelding herkennen met Aspose OCR en GPU

Hieronder staat het **volledige, zelfstandige programma**. Kopieer‑en‑plak het in een nieuw console‑project en druk op `Ctrl+F5`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU‑accelerated namespace

class GpuOcrDemo
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Initialize a GPU‑enabled OCR engine
        // -------------------------------------------------
        var ocrEngine = new GpuOcrEngine();

        // -------------------------------------------------
        // Step 2: (Optional) Select the GPU device and limit memory usage
        // -------------------------------------------------
        ocrEngine.DeviceId = 0;        // set GPU device ID – first GPU in the system
        ocrEngine.MaxMemoryMb = 1024;  // cap at 1 GB to avoid OOM on shared machines

        // -------------------------------------------------
        // Step 3: Load the image you want to recognize
        // -------------------------------------------------
        var receiptImage = OcrImage.FromFile(@"YOUR_DIRECTORY/receipt.jpg");

        // -------------------------------------------------
        // Step 4: Perform OCR – here we extract text from receipt (English)
        // -------------------------------------------------
        var ocrResult = ocrEngine.Recognize(receiptImage, OcrLanguage.English);

        // -------------------------------------------------
        // Step 5: Output the recognized plain text
        // -------------------------------------------------
        System.Console.WriteLine(ocrResult.Text);
    }
}
```

> **Pro tip:** Als je machine meerdere GPU's heeft, wijzig `DeviceId` naar `1`, `2`, enz., om de minder bezette kaart te kiezen. De SDK zal een duidelijke `GpuDeviceNotFoundException` werpen als de ID buiten het bereik valt.

### ### Stap 1: Afbeelding laden voor OCR

De `OcrImage.FromFile`‑aanroep doet meer dan alleen een bitmap lezen—het pre‑processen de afbeelding (kantcorrectie, binarisatie) op basis van interne heuristieken. Daarom is **afbeelding laden voor OCR** een afzonderlijke stap: je kunt een `MemoryStream` gebruiken als je afbeelding in een database staat.

```csharp
var receiptImage = OcrImage.FromFile(@"C:\Invoices\receipt.jpg");
```

Als je **tekst uit afbeelding moet herkennen** die al in het geheugen staat:

```csharp
using (var ms = new MemoryStream(File.ReadAllBytes(@"receipt.jpg")))
{
    var receiptImage = OcrImage.FromStream(ms);
}
```

### ### Stap 2: GPU‑apparaat‑ID instellen en geheugenlimieten

GPU‑bronnen zijn beperkt. Door `DeviceId` en `MaxMemoryMb` bloot te stellen, laat Aspose je **GPU‑apparaat‑ID instellen** op een veilige manier, waardoor één proces niet de hele kaart kan bezet houden.

```csharp
ocrEngine.DeviceId = 0;        // first GPU
ocrEngine.MaxMemoryMb = 1024; // 1 GB ceiling
```

Als je de geheugenlimiet overschrijdt, zal de engine automatisch overschakelen naar systeem‑RAM, wat trager is maar crashes voorkomt.

### ### Stap 3: Tekst uit bon extraheren (tekst uit afbeelding herkennen)

De `Recognize`‑methode doet het zware werk. Je kunt elke taal doorgeven die door Aspose OCR wordt ondersteund; voor bonnen werkt Engels meestal, maar je kunt ook `OcrLanguage.Spanish` of een aangepast taalpakket toevoegen.

```csharp
var ocrResult = ocrEngine.Recognize(receiptImage, OcrLanguage.English);
Console.WriteLine(ocrResult.Text);
```

**Verwachte output** (voorbeeld):

```
Store: QuickMart
Date: 2025-12-01
Total: $23.45
Thank you for shopping!
```

## Veelvoorkomende Variaties & Randgevallen

| Situatie | Wat te wijzigen | Waarom |
|-----------|----------------|-----|
| **Meerdere bonnen in één afbeelding** | Roep `ocrEngine.Recognize` aan op elk bijgesneden gebied (gebruik `OcrImage.Crop`) | Verbetert de nauwkeurigheid omdat de engine een kleiner, schoner gebied ziet. |
| **Scans met lage resolutie (<150 dpi)** | Voorvergroten met `receiptImage.Resize(2.0)` vóór herkenning | Hogere pixeldichtheid geeft de GPU meer data om mee te werken. |
| **Niet‑Engelse bonnen** | Geef `OcrLanguage.French` door (of een aangepast `.traineddata`) | Taalspecifieke modellen verminderen valse positieven. |
| **GPU niet beschikbaar** | Val terug op `OcrEngine` (CPU) binnen een try‑catch‑blok | Garandeert dat de app nog werkt op headless servers. |

```csharp
try
{
    var gpuEngine = new GpuOcrEngine();
    // configure GPU as shown earlier …
    var result = gpuEngine.Recognize(receiptImage, OcrLanguage.English);
    Console.WriteLine(result.Text);
}
catch (GpuDeviceNotFoundException)
{
    // Graceful fallback
    var cpuEngine = new OcrEngine();
    var result = cpuEngine.Recognize(receiptImage, OcrLanguage.English);
    Console.WriteLine(result.Text);
}
```

## Tips voor Productie‑Klaar OCR

- **Batchverwerking:** Plaats de herkenningslus in `Parallel.ForEach` maar beperk de graad van parallelisme tot het aantal GPU‑streams dat je kunt toewijzen (meestal 1‑2 per kaart).
- **Geheugenhygiëne:** Maak `OcrImage`‑objecten direct vrij (`receiptImage.Dispose()`), vooral bij het verwerken van duizenden bonnen.
- **Logging:** Leg `ocrResult.Confidence` vast voor elke regel; lage confidence kan een handmatige review‑workflow activeren.
- **Beveiliging:** Zorg ervoor dat bij het verwerken van gevoelige bonnen de afbeeldingsbestanden worden opgeslagen in versleutelde tijdelijke mappen en na verwerking worden verwijderd.

## Conclusie

Je hebt nu een **volledig, uitvoerbaar voorbeeld** dat laat zien hoe je **tekst uit afbeelding kunt herkennen** met de GPU‑versnelling van Aspose OCR, **afbeelding laden voor OCR**, **GPU‑apparaat‑ID instellen**, en uiteindelijk **tekst uit bon kunt extraheren** in een paar beknopte stappen. De code is klaar om te kopiëren‑en‑plakken, en de uitleg geeft je voldoende context om het aan te passen aan multi‑taal, multi‑GPU, of high‑throughput scenario's.

Klaar voor de volgende uitdaging? Probeer een live videostream aan `GpuOcrEngine` te voeren voor realtime bon‑scanning, of integreer het resultaat in een boekhoud‑API. De mogelijkheden zijn eindeloos wanneer je snelle GPU‑OCR combineert met een nette C#‑architectuur.

*Happy coding, en moge je OCR altijd snel zijn!*

![herken tekst uit afbeelding demo screenshot](placeholder-image.png "herken tekst uit afbeelding voorbeeld")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}