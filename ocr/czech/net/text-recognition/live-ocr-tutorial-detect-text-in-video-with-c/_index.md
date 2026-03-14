---
category: general
date: 2026-03-13
description: Živý OCR tutoriál ukazuje, jak nastavit jazyk OCR a v reálném čase detekovat
  text ve video streamu pomocí Aspose.OCR. Postupujte podle průvodce krok za krokem.
draft: false
keywords:
- live ocr tutorial
- set OCR language
- detect text video
- Aspose OCR live processing
- real‑time text detection
language: cs
og_description: Live OCR tutoriál vysvětluje, jak nastavit jazyk OCR a detekovat text
  ve video streamách pomocí Aspose.OCR Live v C#. Kompletní kód je zahrnut.
og_title: 'Živý OCR tutoriál: Detekce textu v reálném čase ve videu'
tags:
- OCR
- C#
- Aspose
- Video Processing
title: 'Živý OCR tutoriál: Detekce textu ve videu v C#'
url: /cs/net/text-recognition/live-ocr-tutorial-detect-text-in-video-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Live OCR tutoriál: Detekce textu ve videu pomocí C#

Už jste někdy potřebovali **live OCR tutorial**, který skutečně funguje na video kanálu? Možná vytváříte aplikaci pro chytrou kameru nebo překladový overlay v reálném čase a uvízli jste u otázky „jak získat text z každého snímku?“. Dobrá zpráva je, že nemusíte vymýšlet kolo znovu. V tomto průvodci projdeme kompletním, spustitelným příkladem, který **sets OCR language**, zachytává snímky z kamery a **detects text video** streamy za běhu.

Použijeme třídu `LiveOcr` z Aspose.OCR, která je speciálně vytvořena pro scénáře s nízkou latencí. Na konci tohoto článku budete mít konzolovou aplikaci, která vypíše první nalezený text a poté skončí – ideální jako výchozí bod pro složitější pipeline.

## Požadavky

- .NET 6.0 SDK (nebo jakákoli recentní verze .NET)  
- Visual Studio 2022 nebo VS Code (váš oblíbený IDE)  
- NuGet balíček `Aspose.OCR` (nainstalujte pomocí `dotnet add package Aspose.OCR`)  
- Webkamera nebo jakýkoli video zdroj, který může poskytovat `Bitmap` snímky  

Žádné další nativní knihovny nejsou potřeba; Aspose.OCR obsahuje vše, co potřebujete.

## Krok 1: Instalace Aspose.OCR a přidání jmenných prostorů

Než začnete psát kód, ujistěte se, že je knihovna Aspose OCR referencována. Otevřete terminál ve složce projektu a spusťte:

```bash
dotnet add package Aspose.OCR
```

Poté, na začátku souboru `Program.cs`, importujte jmenné prostory, které budeme používat:

```csharp
using Aspose.OCR;
using Aspose.OCR.Live;
using System.Drawing;
using System.Threading;
```

> **Tip:** Pokud používáte Visual Studio, IDE vám automaticky navrhne `using` direktivy poté, co napíšete názvy tříd.

## Krok 2: Vytvoření a konfigurace instance LiveOcr

Srdcem tutoriálu je objekt `LiveOcr`. Musíme mu sdělit, jaký jazyk má hledat, a případně aplikovat předzpracovatelské filtry (např. vyrovnání sklonu) pro zlepšení přesnosti.

```csharp
// Step 2: Initialize LiveOcr with English language and a deskew filter
LiveOcr liveOcr = new LiveOcr
{
    // This is where we **set OCR language** to English.
    Language = Language.English,

    // Pre‑processing helps when the camera isn’t perfectly aligned.
    PreProcessingFilters = new FilterPipeline { new DeskewFilter() }
};
```

Proč nastavit jazyk? OCR enginy používají jazykově specifické slovníky a modely znaků; nastavení angličtiny snižuje falešně pozitivní výsledky a zrychluje rozpoznávání. Pokud potřebujete jiný jazyk, stačí vyměnit `Language.English` za `Language.Spanish`, `Language.French` atd.

## Krok 3: Zachycení snímků z vaší kamery

V reálném projektu byste nahradili placeholder metodu `CaptureFrameFromCamera()` skutečnou logikou zachytávání – možná pomocí `AForge.Video`, `OpenCvSharp` nebo Windows Media Capture API. Pro potřeby tohoto tutoriálu ponecháme metodu abstraktní, ale ukážeme rychlý příklad s využitím `AForge`.

```csharp
// Simple wrapper that returns a Bitmap from the default webcam.
// You can replace this with any library that gives you a Bitmap.
static Bitmap CaptureFrameFromCamera()
{
    // NOTE: This is a minimal example. In production you should
    // manage the video source lifecycle and dispose objects properly.
    var videoSource = new AForge.Video.DirectShow.VideoCaptureDevice(
        new AForge.Video.DirectShow.FilterInfoCollection(
            AForge.Video.DirectShow.FilterCategory.VideoInputDevice)[0].MonikerString);

    Bitmap frame = null;
    var waitHandle = new AutoResetEvent(false);

    videoSource.NewFrame += (sender, eventArgs) =>
    {
        frame = (Bitmap)eventArgs.Frame.Clone();
        waitHandle.Set(); // signal that we have a frame
    };

    videoSource.Start();
    waitHandle.WaitOne(1000); // wait up to 1 second for a frame
    videoSource.SignalToStop();
    videoSource.WaitForStop();

    return frame;
}
```

> **Edge case:** Pokud kamera není dostupná, `CaptureFrameFromCamera` vrátí `null`. V produkčním kódu vždy tuto situaci ošetřete.

## Krok 4: Zpracování každého snímku až do nalezení textu

Nyní provádíme smyčku přes pevný počet snímků (nebo neomezeně) a předáváme každý bitmap do `LiveOcr.ProcessFrame`. Jakmile získáme neprázdný řetězec, vypíšeme jej a ukončíme smyčku.

```csharp
// Step 4: Scan up to 100 frames or until text appears
for (int frameIndex = 0; frameIndex < 100; frameIndex++)
{
    Bitmap cameraFrame = CaptureFrameFromCamera();

    // Guard against a failed capture
    if (cameraFrame == null)
    {
        Console.WriteLine("Failed to capture a frame. Retrying...");
        Thread.Sleep(100);
        continue;
    }

    // Run OCR on the current frame
    string recognizedText = liveOcr.ProcessFrame(cameraFrame);

    // If we detected something, show it and stop
    if (!string.IsNullOrEmpty(recognizedText))
    {
        Console.WriteLine($"Detected text: {recognizedText}");
        break;
    }

    // Small pause to avoid hammering the CPU
    Thread.Sleep(30);
}
```

### Proč pauza?

`Thread.Sleep(30)` dává ovladači kamery chvilku na oddech a snižuje zatížení CPU. Ve scénářích s vysokým výkonem můžete tuto pauzu nahradit sofistikovanějším regulátorem snímkové frekvence.

## Krok 5: Zabalte vše do konzolové aplikace

Spojením všech částí získáte kompletní program připravený ke zkopírování a vložení. Uložte jej jako `Program.cs` v novém konzolovém projektu (`dotnet new console`) a spusťte `dotnet run`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Live;
using System;
using System.Drawing;
using System.Threading;

// Optional: using AForge for demo capture (install AForge.Video via NuGet)
// using AForge.Video.DirectShow;

class Program
{
    static void Main()
    {
        // Initialize LiveOcr – **set OCR language** to English
        LiveOcr liveOcr = new LiveOcr
        {
            Language = Language.English,
            PreProcessingFilters = new FilterPipeline { new DeskewFilter() }
        };

        Console.WriteLine("Starting live OCR… Press Ctrl+C to abort.");

        // Loop through frames – **detect text video** in real time
        for (int i = 0; i < 100; i++)
        {
            Bitmap frame = CaptureFrameFromCamera();

            if (frame == null)
            {
                Console.WriteLine("No frame captured, retrying...");
                Thread.Sleep(100);
                continue;
            }

            string text = liveOcr.ProcessFrame(frame);

            if (!string.IsNullOrEmpty(text))
            {
                Console.WriteLine($"Detected text: {text}");
                break; // stop after first successful detection
            }

            Thread.Sleep(30); // throttle loop
        }

        Console.WriteLine("Live OCR session ended.");
    }

    // -----------------------------------------------------------------
    // Replace this stub with your own capture logic.
    // -----------------------------------------------------------------
    static Bitmap CaptureFrameFromCamera()
    {
        // Placeholder implementation – returns a solid‑color bitmap.
        // In a real app you would pull frames from a webcam or video file.
        Bitmap dummy = new Bitmap(640, 480);
        using (Graphics g = Graphics.FromImage(dummy))
        {
            g.Clear(Color.Black);
            g.DrawString(DateTime.Now.ToString("hh:mm:ss"), 
                new Font("Arial", 24), Brushes.White, new PointF(10, 10));
        }
        return dummy;
    }
}
```

### Očekávaný výstup

Když kamera zachytí čitelný anglický text (např. tištěný štítek), uvidíte něco jako:

```
Starting live OCR… Press Ctrl+C to abort.
Detected text: OpenAI
Live OCR session ended.
```

Pokud se nic neobjeví v zorném poli, smyčka skončí po 100 iteracích a vypíše „Live OCR session ended.“. Můžete zvýšit počet iterací nebo nahradit `for` smyčku za `while (true)` pro nekonečné sledování.

## Často kladené otázky a úskalí

| Otázka | Odpověď |
|----------|--------|
| **Mohu zpracovávat více jazyků současně?** | Ano. Nastavte `Language = Language.English | Language.Spanish;` (bitwise OR) pro povolení vícejazykového slovníku. |
| **Co když jsou mé snímky velké a OCR je pomalé?** | Zmenšete bitmapu před voláním `ProcessFrame`. Příklad: `Bitmap small = new Bitmap(frame, new Size(320, 240));` |
| **Potřebuji licenci pro Aspose.OCR?** | Dočasná evaluační licence funguje až 30 dní. Pro produkci zakupte licenci, která odstraní vodoznak. |
| **Jak zacházet s otočeným textem?** | `DeskewFilter` již koriguje menší rotace. Pro extrémní úhly přidejte do pipeline `RotateFilter`. |
| **Je tento přístup thread‑safe?** | Instance `LiveOcr` nejsou thread‑safe. Vytvořte jednu na vlákno nebo přístup chraňte pomocí zámku. |

## Rozšíření tutoriálu

Nyní, když máte základ **live OCR tutorial**, zvažte následující kroky:

1. **Stream to a UI** – zobrazte živé video s překrytými OCR výsledky pomocí `Windows Forms` nebo `WPF`.  
2. **Batch processing** – posílejte snímky do fronty a spouštějte OCR na poolu background workerů pro vyšší propustnost.  
3. **Language detection** – integrujte knihovnu pro identifikaci jazyka a během běhu přepínejte `LiveOcr.Language`.  
4. **Persist results** – zapisujte detekované řetězce do databáze nebo CSV souboru pro analytiku.  

Každé z těchto rozšíření stále vychází ze základních konceptů, které jsme probírali: inicializace `LiveOcr`, **setting OCR language** a **detecting text video** snímky v reálném čase.

---

### TL;DR

- Nainstalujte Aspose.OCR přes NuGet.  
- Vytvořte objekt `LiveOcr`, **set OCR language** (angličtina v příkladu).  
- Zachyťte `Bitmap` snímky z kamery.  
- Procházejte snímky, volejte `ProcessFrame` a zastavte se, když se objeví text.  
- Výše uvedený kompletní program je připraven ke spuštění a slouží jako solidní základ pro jakýkoli projekt detekce textu v reálném čase.

Vyzkoušejte to, dolaďte předzpracovatelnou pipeline a sledujte, jak vaše aplikace začne číst svět po jednom snímku. Šťastné programování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}