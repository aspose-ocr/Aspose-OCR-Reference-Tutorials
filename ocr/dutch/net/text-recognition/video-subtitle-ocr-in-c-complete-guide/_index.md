---
category: general
date: 2026-06-03
description: Video‑ondertitel OCR‑tutorial die laat zien hoe je frames uit een video
  kunt extraheren en tekst uit videobestanden zoals MP4 kunt lezen met Aspose.OCR.
draft: false
keywords:
- video subtitle ocr
- extract frames from video
- read text from video
- extract text from mp4
language: nl
og_description: Leer video‑ondertiteling OCR met Aspose.OCR. Haal frames uit een video,
  lees tekst uit een video en extraheer tekst uit MP4 in enkele minuten.
og_title: Video-ondertiteling OCR in C# – Stapsgewijze handleiding
schemas:
- author: Aspose
  dateModified: '2026-06-03'
  description: Video subtitle OCR tutorial showing how to extract frames from video
    and read text from video files like MP4 using Aspose.OCR.
  headline: Video Subtitle OCR in C# – Complete Guide
  type: TechArticle
- description: Video subtitle OCR tutorial showing how to extract frames from video
    and read text from video files like MP4 using Aspose.OCR.
  name: Video Subtitle OCR in C# – Complete Guide
  steps:
  - name: Decodes an MP4 (or any supported format) into individual `Bitmap` frames.
    text: Decodes an MP4 (or any supported format) into individual `Bitmap` frames.
  - name: Limits the OCR region to the subtitle band so the engine isn’t distracted
      by the whole picture.
    text: Limits the OCR region to the subtitle band so the engine isn’t distracted
      by the whole picture.
  - name: Processes each frame with Aspose’s `VideoOcrProcessor`.
    text: Processes each frame with Aspose’s `VideoOcrProcessor`.
  - name: Prints the recognized subtitle text to the console.
    text: Prints the recognized subtitle text to the console.
  type: HowTo
tags:
- C#
- Aspose.OCR
- video-processing
title: Video-ondertiteling OCR in C# – Complete gids
url: /nl/net/text-recognition/video-subtitle-ocr-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Video-ondertitel OCR in C# – Complete gids

Heb je ooit **video subtitle ocr** nodig gehad maar wist je niet waar te beginnen? Je bent niet de enige. Of je nu college‑opnames digitaliseert, ondertitels uit trainingsvideo's haalt, of gewoon nieuwsgierig bent naar het lezen van tekst uit video, deze tutorial laat je precies zien hoe je het doet met C# en Aspose.OCR.  

In de komende paar minuten zullen we frames uit een video extraheren, OCR op die frames uitvoeren en uiteindelijk de ondertiteltekst frame‑voor‑frame weergeven. Aan het einde kun je **tekst uit video** bestanden lezen — inclusief MP4 — zonder op zoek te gaan naar tools van derden.

## Wat je gaat bouwen

We zullen een kleine console‑app maken die:

1. Decodeert een MP4 (of elk ondersteund formaat) naar afzonderlijke `Bitmap`‑frames.  
2. Beperkt het OCR‑gebied tot de ondertitelband zodat de engine niet wordt afgeleid door de volledige afbeelding.  
3. Verwerkt elk frame met Aspose’s `VideoOcrProcessor`.  
4. Print de herkende ondertiteltekst naar de console.

Geen poespas, alleen een werkend end‑to‑end voorbeeld dat je in een echt project kunt gebruiken.

## Vereisten

- **.NET 6.0** of later (de code werkt ook op .NET Framework 4.7+).  
- **Aspose.OCR for .NET** – installeer via NuGet: `Install-Package Aspose.OCR`.  
- Een videobestand (MP4 werkt uitstekend).  
- Een manier om videoframes te decoderen – de demo gebruikt een placeholder‑methode, maar je kunt FFmpeg, OpenCV of een andere bibliotheek die `Bitmap`‑objecten retourneert, gebruiken.

> Pro tip: Als je op Windows werkt, werkt het `System.Drawing.Common`‑pakket prima voor `Bitmap`. Op Linux/macOS heb je de native `libgdiplus`‑dependency nodig.

## Stap 1 – Frames uit video extraheren

De eerste hindernis is het omzetten van een bewegend beeld naar stilstaande afbeeldingen. De methode `GetVideoFrames` hieronder is opzettelijk leeg gelaten; vervang deze door je favoriete decoder. Hier is een snelle schets met FFmpeg‑Core (alleen om de vorm van de data te illustreren):

```csharp
using System.Collections.Generic;
using System.Drawing;
using System.Diagnostics;
using System.IO;

/// <summary>
/// Extracts every frame from the supplied video file and yields it as a Bitmap.
/// You can swap this implementation for OpenCV, MediaToolkit, etc.
/// </summary>
static IEnumerable<Bitmap> GetVideoFrames(string videoPath)
{
    // Create a temporary folder for the extracted PNGs
    string tempDir = Path.Combine(Path.GetTempPath(), Guid.NewGuid().ToString());
    Directory.CreateDirectory(tempDir);

    // FFmpeg command: -i input -vf fps=1 output_%04d.png (1 fps for demo)
    var startInfo = new ProcessStartInfo
    {
        FileName = "ffmpeg",
        Arguments = $"-i \"{videoPath}\" -vf fps=1 \"{tempDir}\\frame_%04d.png\" -hide_banner -loglevel error",
        RedirectStandardOutput = true,
        UseShellExecute = false,
        CreateNoWindow = true
    };
    Process ffmpeg = Process.Start(startInfo);
    ffmpeg.WaitForExit();

    foreach (var file in Directory.GetFiles(tempDir, "frame_*.png"))
    {
        using var bmp = new Bitmap(file);
        // Clone the bitmap so the file can be deleted later
        yield return new Bitmap(bmp);
    }

    // Clean up
    Directory.Delete(tempDir, true);
}
```

> **Waarom dit belangrijk is:** Het extraheren van frames geeft de OCR‑engine een statisch beeld om mee te werken, wat de nauwkeurigheid aanzienlijk verbetert vergeleken met direct uit een videostream proberen te lezen.

## Stap 2 – VideoOcrProcessor instellen

Nu we een reeks `Bitmap`‑objecten hebben, kunnen we ze aan Aspose.OCR geven. De `VideoOcrProcessor` stelt ons in staat een **Region of Interest (ROI)** te definiëren – perfect voor ondertitels die meestal bovenaan of onderaan het frame staan.

```csharp
using Aspose.OCR.Video;
using System.Drawing;

// Create the processor and focus on the top 200 pixels (typical subtitle band)
var ocrProcessor = new VideoOcrProcessor
{
    // ROI = new Rectangle(x, y, width, height)
    Roi = new Rectangle(0, 0, 1920, 200)   // adjust width/height to your video resolution
};
```

> **Waarom de ROI beperken?** Door de rest van de afbeelding te negeren verminderen we ruis, verkorten we de verwerkingstijd en voorkomen we valse positieven van achtergrondgrafieken.

## Stap 3 – OCR uitvoeren op de frame‑reeks

Met de processor klaar, is het voeden van de frames een één‑regel‑code. De `Process`‑methode retourneert een enumerable van `OcrResult`‑objecten, elk met de herkende tekst voor het bijbehorende frame.

```csharp
IEnumerable<Bitmap> videoFrames = GetVideoFrames(@"C:\Videos\lecture.mp4");

// Execute OCR on every extracted frame
IEnumerable<OcrResult> ocrResults = ocrProcessor.Process(videoFrames);
```

> **Wat gebeurt er onder de motorkap?** Aspose.OCR normaliseert intern elke bitmap, voert een op neurale netwerken gebaseerde herkenner uit, en verwerkt vervolgens de output naverwerking om interpunctie en regeleinden te verbeteren.

## Stap 4 – De geëxtraheerde tekst weergeven

Tot slot itereren we over de resultaten en printen we elke ondertitelregel. Je kunt ze ook naar een SRT‑bestand schrijven, naar een database, of ze doorvoeren naar een vertaaldienst.

```csharp
int frameIndex = 0;
foreach (var result in ocrResults)
{
    // result.Text contains the plain‑text subtitle for this frame
    Console.WriteLine($"Frame {frameIndex++}: {result.Text}");
}
```

### Volledig werkend voorbeeld

Alles samenvoegen levert een zelfstandige console‑applicatie op:

```csharp
using Aspose.OCR.Video;
using System;
using System.Collections.Generic;
using System.Drawing;
using System.Diagnostics;
using System.IO;

class VideoSubtitleOcrDemo
{
    static void Main()
    {
        // 1️⃣ Extract frames from the MP4 (replace with your own decoder)
        IEnumerable<Bitmap> videoFrames = GetVideoFrames(@"C:\Videos\lecture.mp4");

        // 2️⃣ Configure OCR – focus on the subtitle band
        var ocrProcessor = new VideoOcrProcessor
        {
            Roi = new Rectangle(0, 0, 1920, 200) // tweak for your video size
        };

        // 3️⃣ Run OCR across all frames
        IEnumerable<OcrResult> ocrResults = ocrProcessor.Process(videoFrames);

        // 4️⃣ Output the recognized subtitle text
        int frameIndex = 0;
        foreach (var result in ocrResults)
        {
            Console.WriteLine($"Frame {frameIndex++}: {result.Text}");
        }
    }

    // --------------------------------------------------------------------
    // Helper: extract one‑frame‑per‑second PNGs using FFmpeg.
    // Replace this with any library that can return Bitmap objects.
    // --------------------------------------------------------------------
    static IEnumerable<Bitmap> GetVideoFrames(string videoPath)
    {
        string tempDir = Path.Combine(Path.GetTempPath(), Guid.NewGuid().ToString());
        Directory.CreateDirectory(tempDir);

        var startInfo = new ProcessStartInfo
        {
            FileName = "ffmpeg",
            Arguments = $"-i \"{videoPath}\" -vf fps=1 \"{tempDir}\\frame_%04d.png\" -hide_banner -loglevel error",
            RedirectStandardOutput = true,
            UseShellExecute = false,
            CreateNoWindow = true
        };
        using var ffmpeg = Process.Start(startInfo);
        ffmpeg.WaitForExit();

        foreach (var file in Directory.GetFiles(tempDir, "frame_*.png"))
        {
            using var bmp = new Bitmap(file);
            yield return new Bitmap(bmp);
        }

        Directory.Delete(tempDir, true);
    }
}
```

**Verwachte output (voorbeeld)**  

```
Frame 0: Welcome to the Introduction to Machine Learning.
Frame 1: In this lecture we will cover...
Frame 2: ...
```

Als de OCR moeite heeft met een bepaald frame, zie je een lege string – dat is een signaal om de ROI aan te passen of de frame‑extractiesnelheid te verhogen.

## Veelvoorkomende valkuilen & hoe ze op te lossen

| Probleem | Waarom het gebeurt | Oplossing |
|-------|----------------|-----|
| **Garbage characters** | Frames met lage resolutie of zware compressie | Extraheer frames met een hogere bitrate, of schaal de bitmap op vóór OCR (`Bitmap.Clone(new Size(...), ...)`). |
| **No text returned** | ROI dekt de ondertitelband niet | Controleer de rechthoekcoördinaten (gebruik een screenshot‑tool om te meten). |
| **Performance bottleneck** | Elke frame verwerken op 30 fps is overbodig | Down‑sample naar 1‑2 fps voor de meeste ondertitel‑streams; je kunt nog steeds elke ondertitelwijziging vastleggen. |
| **FFmpeg not found** | `ffmpeg.exe` staat niet in de `PATH` | Geef het volledige pad op in `ProcessStartInfo.FileName` of installeer FFmpeg globaal. |

## De oplossing uitbreiden

- **Exporteren naar SRT** – concateneer de tijdstempels met de OCR‑tekst en schrijf een SubRip‑bestand.  
- **Meertalige ondersteuning** – stel `ocrProcessor.Language = OcrLanguage.Spanish` in (of een andere ondersteunde taal).  
- **Realtime verwerking** – pipe frames direct van een live‑stream in plaats van van schijf te lezen.  

Al deze variaties draaien nog steeds om de kernideeën van **frames uit video extraheren**, **tekst uit video lezen**, en **tekst uit mp4 extraheren**.

## Conclusie

We hebben zojuist een volledige **video subtitle ocr**‑workflow in C# doorlopen. Door frames uit video te extraheren, de OCR te richten op de ondertitelband, en over de resultaten te itereren, kun je betrouwbaar **tekst uit video** bestanden zoals MP4 lezen. De code is klaar om te copy‑pasten, en het modulaire ontwerp laat je elke gewenste frame‑decoder gebruiken.

Volgende stappen? Probeer de resultaten naar een SRT‑bestand te exporteren, experimenteer met verschillende ROI‑groottes, of voer de ondertitels in een vertaal‑API voor meertalige captions. De mogelijkheden zijn eindeloos zodra je de basis van tekst uit video extraheren onder de knie hebt.

Veel plezier met coderen, en moge je ondertitels altijd kristalhelder zijn!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Afbeeldingstekst extraheren C# met taalkeuze via Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Tekst extraheren uit afbeelding met Aspose.OCR .NET](/ocr/english/net/image-and-drawing-recognition/)
- [Tekst extraheren uit afbeelding – OCR‑optimalisatie met Aspose.OCR voor .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}