---
category: general
date: 2026-03-13
description: Live OCR‑handledning visar hur du ställer in OCR‑språk och upptäcker
  text i videoströmmar i realtid med Aspose.OCR. Följ steg‑för‑steg‑guiden.
draft: false
keywords:
- live ocr tutorial
- set OCR language
- detect text video
- Aspose OCR live processing
- real‑time text detection
language: sv
og_description: Live OCR-handledning förklarar hur man ställer in OCR-språk och upptäcker
  text i videoströmmar med Aspose.OCR Live i C#. Komplett kod medföljer.
og_title: 'Live OCR-handledning: Realtidsdetektering av text i video'
tags:
- OCR
- C#
- Aspose
- Video Processing
title: 'Live OCR-handledning: Detektera text i video med C#'
url: /sv/net/text-recognition/live-ocr-tutorial-detect-text-in-video-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Live OCR‑handledning: Detektera text i video med C#

Behöver du en **live OCR‑handledning** som faktiskt fungerar på en videoström? Kanske bygger du en smart‑kamerapp eller ett real‑tids‑översättningslager och fastnar på “hur får jag text från varje bildruta?” Det goda nyheten är att du inte behöver uppfinna hjulet på nytt. I den här guiden går vi igenom ett komplett, körbart exempel som **ställer in OCR‑språk**, hämtar bildrutor från en kamera och **detekterar text i videoströmmar** i realtid.

Vi använder Aspose.OCR:s `LiveOcr`‑klass, som är byggd för låg latens. När du är klar med den här artikeln har du en konsolapp som skriver ut den första texten den ser och sedan avslutas – perfekt som utgångspunkt för mer avancerade pipelines.

## Förutsättningar

- .NET 6.0 SDK (eller någon nyare .NET‑version)  
- Visual Studio 2022 eller VS Code (din favorit‑IDE)  
- NuGet‑paketet `Aspose.OCR` (installera via `dotnet add package Aspose.OCR`)  
- En webbkamera eller någon videokälla som kan leverera `Bitmap`‑ramar  

Inga extra inhemska bibliotek behövs; Aspose.OCR levereras med allt du behöver.

## Steg 1: Installera Aspose.OCR och lägg till namnrymder

Innan du skriver någon kod, se till att Aspose OCR‑biblioteket är refererat. Öppna en terminal i din projektmapp och kör:

```bash
dotnet add package Aspose.OCR
```

Sedan, högst upp i din `Program.cs`, importera namnrymderna vi kommer att använda:

```csharp
using Aspose.OCR;
using Aspose.OCR.Live;
using System.Drawing;
using System.Threading;
```

> **Proffstips:** Om du använder Visual Studio föreslår IDE‑t automatiskt `using`‑satserna när du skriver klassnamnen.

## Steg 2: Skapa och konfigurera LiveOcr‑instansen

Kärnan i handledningen är `LiveOcr`‑objektet. Vi måste tala om för det vilket språk som ska sökas efter och eventuellt applicera förbehandlingsfilter (som deskew) för att förbättra noggrannheten.

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

Varför ange språk? OCR‑motorer använder språk‑specifika ordböcker och teckenmodeller; att specificera engelska minskar falska positiva och snabbar upp igenkänningen. Om du behöver ett annat språk, byt bara ut `Language.English` mot `Language.Spanish`, `Language.French` osv.

## Steg 3: Fånga bildrutor från din kamera

I ett riktigt projekt skulle du ersätta platshållarmetoden `CaptureFrameFromCamera()` med faktisk fångstlogik – kanske med `AForge.Video`, `OpenCvSharp` eller Windows Media Capture‑API:t. För den här handledningen håller vi metoden abstrakt, men vi visar ett snabbt exempel med `AForge`.

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

> **Edge case:** Om kameran inte är tillgänglig returnerar `CaptureFrameFromCamera` `null`. Se alltid till att hantera detta i produktionskod.

## Steg 4: Bearbeta varje bildruta tills text hittas

Nu loopar vi över ett fast antal bildrutor (eller oändligt) och matar varje bitmap till `LiveOcr.ProcessFrame`. Så snart vi får en icke‑tom sträng skriver vi ut den och bryter loopen.

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

### Varför en paus?

`Thread.Sleep(30)` ger kameradrivrutinen en liten paus och minskar CPU‑användningen. I högpresterande scenarier kan du ersätta den med en mer sofistikerad bildfrekvens‑kontroller.

## Steg 5: Packa allt i en konsolapplikation

Sätt ihop allt, så här ser det kompletta, kopiera‑och‑klistra‑klara programmet ut. Spara det som `Program.cs` i ett nytt konsolprojekt (`dotnet new console`) och kör `dotnet run`.

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

### Förväntad utdata

När kameran ser läsbar engelsk text (t.ex. en tryckt etikett) får du något i stil med:

```
Starting live OCR… Press Ctrl+C to abort.
Detected text: OpenAI
Live OCR session ended.
```

Om inget syns i bildrutan avslutas loopen efter 100 iterationer och skriver “Live OCR session ended.” Du kan öka antalet iterationer eller ersätta `for`‑loopen med en `while (true)` för oändlig övervakning.

## Vanliga frågor & fallgropar

| Fråga | Svar |
|----------|--------|
| **Kan jag bearbeta flera språk samtidigt?** | Ja. Sätt `Language = Language.English | Language.Spanish;` (bitvis OR) för att aktivera en flerspråkig ordbok. |
| **Vad händer om mina bildrutor är stora och OCR känns långsam?** | Skala ner bitmapen innan du anropar `ProcessFrame`. Exempel: `Bitmap small = new Bitmap(frame, new Size(320, 240));` |
| **Behöver jag en licens för Aspose.OCR?** | En temporär evalueringslicens fungerar i upp till 30 dagar. För produktion, köp en licens för att ta bort vattenstämpeln. |
| **Hur hanterar jag roterad text?** | `DeskewFilter` korrigerar redan mindre rotationer. För extrema vinklar, lägg till ett `RotateFilter` i pipelinen. |
| **Är detta tillvägagångssätt trådsäkert?** | `LiveOcr`‑instanser är inte trådsäkra. Skapa en per tråd eller skydda åtkomst med en lock. |

## Utöka handledningen

Nu när du har en **live OCR‑handledning** som grund, överväg följande nästa steg:

1. **Strömma till ett UI** – visa live‑videon med överlagrad OCR‑resultat med `Windows Forms` eller `WPF`.  
2. **Batch‑bearbetning** – skicka bildrutor till en kö och kör OCR i en bakgrunds‑worker‑pool för högre genomströmning.  
3. **Språkdetection** – integrera ett språk‑identifieringsbibliotek för att byta `LiveOcr.Language` dynamiskt.  
4. **Spara resultat** – skriv de upptäckta strängarna till en databas eller en CSV‑fil för analys.  

Var och en av dessa utökningar bygger fortfarande på de grundläggande koncept vi gått igenom: initiera `LiveOcr`, **ställa in OCR‑språk**, och **detektera text i videobildrutor** i realtid.

---

### TL;DR

- Installera Aspose.OCR via NuGet.  
- Skapa ett `LiveOcr`‑objekt, **ställ in OCR‑språk** (engelska i exemplet).  
- Fånga `Bitmap`‑ramar från en kamera.  
- Loopa genom ramarna, anropa `ProcessFrame`, och stoppa när text dyker upp.  
- Programmet ovan är färdigt att köras och fungerar som en solid bas för alla real‑tids‑textdetekteringsprojekt.

Prova det, justera förbehandlingspipen, och se din app börja läsa världen, en bildruta i taget. Lycka till med kodandet!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}