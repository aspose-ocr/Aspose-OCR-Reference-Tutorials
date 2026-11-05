---
category: general
date: 2026-05-21
description: Aspose OCR GPU stelt je in staat om tekst in afbeeldingen snel te herkennen.
  Leer hoe je een afbeelding laadt voor OCR, tekst uit TIFF's extraheert en de prestaties
  verbetert.
draft: false
keywords:
- aspose ocr gpu
- recognize text image
- ocr tiff image
- load image for ocr
- extract text from tiff
language: nl
og_description: Aspose OCR GPU versnelt tekstdetectie. Deze gids laat zien hoe je
  een afbeelding laadt voor OCR, tekst in een afbeelding herkent en efficiënt tekst
  uit TIFF extraheert.
og_title: Aspose OCR GPU – Tekst uit TIFF-afbeelding herkennen in C#
schemas:
- author: Aspose
  dateModified: '2026-05-21'
  description: Aspose OCR GPU lets you recognize text image quickly. Learn how to
    load image for OCR, extract text from TIFF and boost performance.
  headline: 'Aspose OCR GPU: Recognize Text Image from TIFF with C#'
  type: TechArticle
- description: Aspose OCR GPU lets you recognize text image quickly. Learn how to
    load image for OCR, extract text from TIFF and boost performance.
  name: 'Aspose OCR GPU: Recognize Text Image from TIFF with C#'
  steps:
  - name: Enables GPU acceleration (optional, with automatic CPU fallback).
    text: Enables GPU acceleration (optional, with automatic CPU fallback).
  - name: Creates an `OcrEngine` configured for English.
    text: Creates an `OcrEngine` configured for English.
  - name: Loads a large **OCR TIFF image** from disk.
    text: Loads a large **OCR TIFF image** from disk.
  - name: Runs the recognition and prints the result.
    text: Runs the recognition and prints the result.
  type: HowTo
tags:
- aspose
- ocr
- csharp
title: 'Aspose OCR GPU: Tekstherkenning van TIFF‑afbeelding met C#'
url: /nl/net/ocr-optimization/aspose-ocr-gpu-recognize-text-image-from-tiff-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR GPU: Tekst uit TIFF‑afbeelding herkennen met C#

Heb je je ooit afgevraagd hoe je **tekst uit een afbeelding** kunt herkennen uit een enorme TIFF‑bestand zonder je CPU te overbelasten? Je bent niet de enige. In veel document‑verwerkingspijplijnen is de OCR‑stap de knelpunt, vooral wanneer je gigabytes aan gescande pagina’s aan een eenvoudige engine geeft.  

Het goede nieuws? **Aspose OCR GPU** kan het proces een enorme boost geven, en het code‑voorbeeld hieronder laat precies zien hoe je **een afbeelding laadt voor OCR**, **tekst uit een TIFF haalt**, en netjes terugvalt als er geen GPU aanwezig is. Laten we beginnen.

## Wat deze tutorial behandelt

We lopen stap voor stap door een compleet, kant‑klaar C#‑programma dat:

1. GPU‑versnelling inschakelt (optioneel, met automatische CPU‑fallback).  
2. Een `OcrEngine` maakt die is geconfigureerd voor Engels.  
3. Een grote **OCR‑TIFF‑afbeelding** van de schijf laadt.  
4. De herkenning uitvoert en het resultaat afdrukt.  

Aan het einde begrijp je **waarom** elke stap belangrijk is, hoe je veelvoorkomende randgevallen afhandelt, en heb je een werkend voorbeeld dat je kunt aanpassen voor PDF’s, multi‑page TIFF’s of zelfs realtime camerastreams.

> **Prerequisites** – .NET 6+ (of .NET Framework 4.7+), het Aspose.OCR NuGet‑pakket, en een GPU‑enabled machine als je de snelheidswinst wilt zien. Er is geen speciale hardware vereist; de code gebruikt simpelweg de CPU wanneer er geen GPU wordt gedetecteerd.

---

![Aspose OCR GPU processing diagram showing CPU fallback](/images/aspose-ocr-gpu-diagram.png){: .align-center alt="aspose ocr gpu"}

## Stap 1: GPU‑versnelling inschakelen (optioneel)

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // adds GPU support

// Enable GPU if a compatible device is present.
// The call is safe – if no GPU is found Aspose falls back to CPU.
OcrEngine.EnableGpu(true);
```

**Waarom dit belangrijk is:**  
GPU‑kernen blinken uit in de massale paralleliteit die nodig is voor beeldvoorbewerking (binarisatie, ruisverwijdering) en neurale‑netwerk‑inference. Door `EnableGpu(true)` aan te zetten geef je de engine het groene licht om die taken uit te besteden. Als de machine geen CUDA‑compatibele kaart heeft, schakelt Aspose stilletjes terug naar de CPU, zodat je nooit een harde crash krijgt.

**Pro tip:** Op Windows moet je mogelijk de nieuwste NVIDIA‑driver en de CUDA‑toolkit geïnstalleerd hebben. Op Linux zorg je ervoor dat `nvidia‑driver` en `libcuda.so` in je bibliotheek‑pad staan.

## Stap 2: De OCR‑engine maken en configureren

```csharp
// Step 2: Instantiate the OCR engine and set the language.
var ocrEngine = new OcrEngine
{
    // English works for most scanned docs; you can pick other languages here.
    Language = OcrLanguage.English
};
```

**Waarom dit belangrijk is:**  
`OcrEngine` is het hart van **Aspose OCR GPU**. Het instellen van `Language` vertelt het onderliggende neurale model welke tekenset verwacht wordt, wat de nauwkeurigheid drastisch verbetert. Je kunt ook `Resolution`, `PreprocessOptions` of `RecognitionMode` aanpassen voor moeilijkere documenten.

## Stap 3: De afbeelding laden voor OCR

```csharp
// Step 3: Load a large TIFF image from disk.
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/large_doc.tif");
```

**Waarom dit belangrijk is:**  
Een TIFF kan meerdere pagina’s, hoge resolutie en lossless compressie bevatten – perfect voor archiefscans maar zwaar voor het geheugen. `ImageStream.FromFile` streamt het bestand, waardoor een volledige in‑memory‑load voor zeer grote afbeeldingen wordt vermeden.  

**Randgeval:** Als je een multi‑page TIFF moet verwerken, roep je `ocrEngine.Image = ImageStream.FromFile(path, pageIndex);` aan binnen een lus, waarbij je `pageIndex` verhoogt tot `ocrEngine.Image.IsNull` `true` teruggeeft.

## Stap 4: De herkenning uitvoeren

```csharp
// Step 4: Run the OCR process.
ocrEngine.Recognize();
```

**Waarom dit belangrijk is:**  
`Recognize()` doet al het zware werk: voorbewerking, lay‑out‑analyse, karaktersegmentatie en uiteindelijk neurale‑netwerk‑inference. Wanneer de GPU actief is, draait de inference‑stap op de GPU, vaak 50‑80 % tijdsbesparing oplevend voor grote TIFF’s.

## Stap 5: De resultaten weergeven

```csharp
// Step 5: Show how many characters were extracted and how long it took.
Console.WriteLine($"Recognized {ocrEngine.Text.Length} characters in {ocrEngine.ProcessingTime} ms");

// Optional: print the extracted text (be careful with huge strings!)
Console.WriteLine("--- Extracted Text Start ---");
Console.WriteLine(ocrEngine.Text);
Console.WriteLine("--- Extracted Text End ---");
```

**Waarom dit belangrijk is:**  
`ocrEngine.Text` bevat de volledig samengevoegde string uit de afbeelding, terwijl `ProcessingTime` je een snelle benchmark geeft om CPU‑ versus GPU‑runs te vergelijken. De console‑output is handig voor snelle debugging; in productie zou je de tekst waarschijnlijk naar een database of bestand schrijven.

**Verwachte output (voorbeeld voor een factuur van 2 pagina’s):**

```
Recognized 1342 characters in 842 ms
--- Extracted Text Start ---
Invoice #12345
Date: 2026‑04‑30
...
Total: $1,234.56
--- Extracted Text End ---
```

Als de GPU niet beschikbaar is, kan de tijd oplopen tot ~1800 ms op dezelfde hardware, wat duidelijk het voordeel van **aspose ocr gpu** aantoont.

---

## Veelvoorkomende valkuilen behandelen

| Situatie | Waar op letten | Hoe op te lossen |
|----------|----------------|------------------|
| **GPU niet gedetecteerd** | `EnableGpu(true)` valt stilletjes terug, maar je denkt dat de GPU nog steeds wordt gebruikt. | Controleer `OcrEngine.IsGpuEnabled` na de aanroep; log het resultaat. |
| **Out‑of‑memory bij enorme TIFF** | Het laden van een afbeelding van 10 000 × 10 000 pixels kan het RAM overschrijden. | Gebruik `ImageStream.FromFile(path, pageIndex, maxResolution: 300)` om bij het laden te down‑samplen. |
| **Verkeerde taal** | Engels model op een Frans document levert onleesbare output op. | Stel `Language = OcrLanguage.French` in of schakel meertalige modus in. |
| **Multi‑page TIFF** | Alleen de eerste pagina wordt verwerkt. | Loop over pagina’s met `ImageStream.FromFile(path, pageNumber)`. |

---

## Volledig werkend voorbeeld

Hieronder staat het complete programma dat je in een console‑app kunt plakken. Het bevat foutafhandeling, GPU‑statuslogging en een eenvoudige timer voor je eigen benchmarks.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;   // adds GPU support

namespace AsposeOcrGpuDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Enable GPU acceleration (if available)
            OcrEngine.EnableGpu(true);
            Console.WriteLine($"GPU enabled: {OcrEngine.IsGpuEnabled}");

            // 2️⃣ Create the OCR engine and set language
            var ocrEngine = new OcrEngine
            {
                Language = OcrLanguage.English
            };

            // 3️⃣ Load the TIFF image (replace with your actual path)
            string imagePath = @"YOUR_DIRECTORY\large_doc.tif";
            try
            {
                ocrEngine.Image = ImageStream.FromFile(imagePath);
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Failed to load image: {ex.Message}");
                return;
            }

            // 4️⃣ Perform recognition
            try
            {
                ocrEngine.Recognize();
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Recognition error: {ex.Message}");
                return;
            }

            // 5️⃣ Output results
            Console.WriteLine($"Recognized {ocrEngine.Text.Length} characters in {ocrEngine.ProcessingTime} ms");
            Console.WriteLine("--- Extracted Text Start ---");
            Console.WriteLine(ocrEngine.Text);
            Console.WriteLine("--- Extracted Text End ---");
        }
    }
}
```

Kopiëren, plakken, **F5** indrukken, en zie hoe de console het aantal tekens en de geëxtraheerde tekst weergeeft. Vervang `OcrLanguage.English` door een andere door Aspose ondersteunde taal als je **tekst uit een afbeelding** in het Spaans, Duits, enz. wilt herkennen.

---

## Samenvatting & vervolgstappen

We hebben net behandeld hoe je **aspose ocr gpu** kunt gebruiken om **tekst uit een afbeelding** te **herkennen uit een OCR‑TIFF‑afbeelding**, hoe je **een afbeelding laadt voor OCR**, en hoe je **tekst uit TIFF** efficiënt extraheert. De kernideeën – GPU inschakelen, taal configureren, de TIFF streamen, en het resultaat lezen – zijn overdraagbaar naar andere bestandsformaten zoals JPEG of PNG.

### Wat je hierna kunt proberen

- **Batchverwerking**: Loop door een map met TIFF‑bestanden en schrijf elke `ocrEngine.Text` naar een `.txt`‑bestand.  
- **Multi‑page handling**: Gebruik `ImageStream.FromFile(path, pageIndex)` binnen een `while`‑lus om elke pagina van een multi‑page document te verwerken.  
- **Aangepaste voorbewerking**: Pas `ocrEngine.PreprocessOptions` (bijv. `Denoise`, `Deskew`) aan voor ruisende scans.  
- **GPU‑benchmarking**: Registreer `ProcessingTime` met en zonder `EnableGpu(true)` op dezelfde machine om de snelheidswinst te kwantificeren.

Experimenteer gerust – GPU‑versnelling levert het meeste op bij hoge resolutie, multi‑page TIFF’s, maar zelfs een bescheiden 1080 Ti zal de herkenningstijd aanzienlijk verkorten.

Heb je vragen over een specifiek documenttype of hulp nodig bij het integreren van de output in een database? Laat een reactie achter hieronder, en happy coding!

## Gerelateerde tutorials

- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Extract Text from Image – Recognize Line with Aspose.OCR](/ocr/english/net/image-and-drawing-recognition/recognize-line/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}