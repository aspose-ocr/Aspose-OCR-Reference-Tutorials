---
category: general
date: 2026-06-03
description: Návod na OCR titulků ve videu, který ukazuje, jak extrahovat snímky z
  videa a číst text z video souborů jako MP4 pomocí Aspose.OCR.
draft: false
keywords:
- video subtitle ocr
- extract frames from video
- read text from video
- extract text from mp4
language: cs
og_description: Naučte se OCR titulků ve videu s Aspose.OCR. Extrahujte snímky z videa,
  čtěte text z videa a extrahujte text z MP4 během několika minut.
og_title: OCR titulků videa v C# – krok za krokem průvodce
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
title: OCR titulků videa v C# – Kompletní průvodce
url: /cs/net/text-recognition/video-subtitle-ocr-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR titulků ve videu v C# – Kompletní průvodce

Už jste někdy potřebovali **video subtitle ocr**, ale nebyli jste si jisti, kde začít? Nejste v tom sami. Ať už digitalizujete nahrávky přednášek, získáváte titulky z výukových videí, nebo jste jen zvědaví, jak číst text z videa, tento tutoriál vám přesně ukáže, jak to provést v C# a s Aspose.OCR.  

V následujících několika minutách extrahujeme snímky z videa, spustíme OCR na těchto snímcích a nakonec zobrazíme text titulků snímek po snímku. Na konci budete schopni **read text from video** soubory — včetně MP4 — bez hledání nástrojů třetích stran.

## Co vytvoříte

Vytvoříme malou konzolovou aplikaci, která:

1. Dekóduje MP4 (nebo jakýkoli podporovaný formát) do jednotlivých `Bitmap` snímků.  
2. Omezí oblast OCR na pás titulků, aby motor nebyl rozptýlený celým obrázkem.  
3. Zpracuje každý snímek pomocí `VideoOcrProcessor` od Aspose.  
4. Vytiskne rozpoznaný text titulků do konzole.

Žádné zbytečnosti, jen funkční end‑to‑end příklad, který můžete vložit do reálného projektu.

## Požadavky

- **.NET 6.0** nebo novější (kód také funguje na .NET Framework 4.7+).  
- **Aspose.OCR for .NET** – nainstalujte přes NuGet: `Install-Package Aspose.OCR`.  
- Video soubor (MP4 funguje skvěle).  
- Způsob dekódování video snímků – demo používá zástupnou metodu, ale můžete připojit FFmpeg, OpenCV nebo libovolnou knihovnu, která vrací objekty `Bitmap`.  

> Pro tip: Pokud používáte Windows, balíček `System.Drawing.Common` funguje dobře pro `Bitmap`. Na Linux/macOS budete potřebovat nativní závislost `libgdiplus`.

## Krok 1 – Extrahování snímků z videa

První překážkou je převést pohyblivý obrázek na statické snímky. Metoda `GetVideoFrames` níže je úmyslně prázdná; nahraďte ji svým oblíbeným dekodérem. Zde je rychlý náčrt pomocí FFmpeg‑Core (jen pro ilustraci tvaru dat):

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

> **Proč je to důležité:** Extrahování snímků poskytuje OCR motoru statický obrázek, se kterým může pracovat, což dramaticky zvyšuje přesnost ve srovnání s pokusem číst přímo z video proudu.

## Krok 2 – Nastavení VideoOcrProcessor

Nyní, když máme sekvenci objektů `Bitmap`, můžeme je předat Aspose.OCR. `VideoOcrProcessor` nám umožňuje definovat **Region of Interest (ROI)** – ideální pro titulky, které se obvykle nacházejí nahoře nebo dole ve snímku.

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

> **Proč omezit ROI?** Ignorováním zbytku obrázku snižujeme šum, zkracujeme dobu zpracování a vyhýbáme se falešným pozitivům z pozadí.

## Krok 3 – Spuštění OCR na sekvenci snímků

S připraveným procesorem je podávání snímků jednorázovým příkazem. Metoda `Process` vrací enumerable objektů `OcrResult`, z nichž každý obsahuje rozpoznaný text pro odpovídající snímek.

```csharp
IEnumerable<Bitmap> videoFrames = GetVideoFrames(@"C:\Videos\lecture.mp4");

// Execute OCR on every extracted frame
IEnumerable<OcrResult> ocrResults = ocrProcessor.Process(videoFrames);
```

> **Co se děje pod kapotou?** Aspose.OCR interně normalizuje každý bitmap, spouští rozpoznávač založený na neuronové síti a poté provádí post‑processing výstupu pro zlepšení interpunkce a zalomení řádků.

## Krok 4 – Zobrazení extrahovaného textu

Nakonec iterujeme přes výsledky a vytiskneme každou řádku titulků. Můžete je také zapsat do SRT souboru, databáze nebo předat překladatelskému API.

```csharp
int frameIndex = 0;
foreach (var result in ocrResults)
{
    // result.Text contains the plain‑text subtitle for this frame
    Console.WriteLine($"Frame {frameIndex++}: {result.Text}");
}
```

### Kompletní funkční příklad

Spojením všech částí získáme samostatný konzolový program:

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

**Očekávaný výstup (ukázka)**  

```
Frame 0: Welcome to the Introduction to Machine Learning.
Frame 1: In this lecture we will cover...
Frame 2: ...
```

Pokud OCR selže u konkrétního snímku, uvidíte prázdný řetězec – to je signál, že je potřeba upravit ROI nebo zvýšit frekvenci extrakce snímků.

## Časté problémy a jak je opravit

| Problém | Proč se to děje | Řešení |
|-------|----------------|-----|
| **Garbage characters** | Nízké rozlišení snímků nebo silná komprese | Extrahujte snímky při vyšším bitrate, nebo před OCR zvětšete bitmapu (`Bitmap.Clone(new Size(...), ...)`). |
| **No text returned** | ROI ve skutečnosti nepokrývá pás titulků | Ověřte souřadnice obdélníku (použijte nástroj pro snímání obrazovky). |
| **Performance bottleneck** | Zpracování každého snímku při 30 fps je přehnané | Down‑samplujte na 1‑2 fps pro většinu titulků; stále zachytíte každou změnu titulků. |
| **FFmpeg not found** | `ffmpeg.exe` není v `PATH` | Zadejte úplnou cestu v `ProcessStartInfo.FileName` nebo nainstalujte FFmpeg globálně. |

## Rozšíření řešení

- **Export do SRT** – spojte časové značky s OCR textem a zapište SubRip soubor.  
- **Podpora více jazyků** – nastavte `ocrProcessor.Language = OcrLanguage.Spanish` (nebo jakýkoli podporovaný jazyk).  
- **Zpracování v reálném čase** – přenášejte snímky přímo z živého proudu místo čtení z disku.  

Všechny tyto varianty stále obíhají kolem hlavních myšlenek **extract frames from video**, **read text from video** a **extract text from mp4**.

## Závěr

Právě jsme prošli kompletním **video subtitle ocr** pracovním postupem v C#. Extrahováním snímků z videa, zaměřením OCR na pás titulků a iterací přes výsledky můžete spolehlivě **read text from video** soubory jako MP4. Kód je připravený ke zkopírování a modulární design vám umožní vyměnit libovolný dekodér snímků, který preferujete.

Další kroky? Zkuste exportovat výsledky do SRT souboru, experimentujte s různými velikostmi ROI nebo předejte titulky do překladatelského API pro vícejazyčné popisky. Možnosti jsou neomezené, jakmile zvládnete základy extrakce textu z videa.

Šťastné programování a ať jsou vaše titulky vždy krystalicky čisté!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s krok‑za‑krokem vysvětleními, která vám pomohou zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vašich projektech.

- [Extrahování textu z obrázku v C# s výběrem jazyka pomocí Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Extrahování textu z obrázku pomocí Aspose.OCR .NET](/ocr/english/net/image-and-drawing-recognition/)
- [Extrahování textu z obrázku – optimalizace OCR s Aspose.OCR pro .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}