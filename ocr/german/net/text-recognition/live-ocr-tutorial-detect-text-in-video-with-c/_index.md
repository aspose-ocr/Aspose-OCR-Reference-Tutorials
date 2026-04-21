---
category: general
date: 2026-03-13
description: Das Live‑OCR‑Tutorial zeigt, wie man die OCR‑Sprache einstellt und Text‑Videostreams
  in Echtzeit mit Aspose.OCR erkennt. Folgen Sie der Schritt‑für‑Schritt‑Anleitung.
draft: false
keywords:
- live ocr tutorial
- set OCR language
- detect text video
- Aspose OCR live processing
- real‑time text detection
language: de
og_description: Live-OCR-Tutorial erklärt, wie man die OCR-Sprache einstellt und Text
  in Video-Streams mit Aspose.OCR Live in C# erkennt. Vollständiger Code enthalten.
og_title: 'Live-OCR-Tutorial: Echtzeit-Text-Erkennung im Video'
tags:
- OCR
- C#
- Aspose
- Video Processing
title: 'Live-OCR‑Tutorial: Text im Video mit C# erkennen'
url: /de/net/text-recognition/live-ocr-tutorial-detect-text-in-video-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Live-OCR-Tutorial: Text in Video mit C# erkennen

Haben Sie jemals ein **Live-OCR-Tutorial** gebraucht, das tatsächlich auf einem Video-Feed funktioniert? Vielleicht bauen Sie eine Smart‑Camera‑App oder ein Echtzeit‑Übersetzungs‑Overlay und stecken bei „Wie bekomme ich Text aus jedem Frame?“ fest. Die gute Nachricht ist, dass Sie das Rad nicht neu erfinden müssen. In diesem Leitfaden gehen wir ein komplettes, ausführbares Beispiel durch, das **die OCR‑Sprache festlegt**, Frames von einer Kamera abruft und **Text in Videostreams** in Echtzeit erkennt.

Wir verwenden die `LiveOcr`‑Klasse von Aspose.OCR, die speziell für Low‑Latency‑Szenarien entwickelt wurde. Am Ende dieses Artikels haben Sie eine Konsolen‑App, die das erste erkannte Textstück ausgibt und dann beendet – perfekt als Ausgangspunkt für anspruchsvollere Pipelines.

## Voraussetzungen

- .NET 6.0 SDK (oder eine aktuelle .NET‑Version)  
- Visual Studio 2022 oder VS Code (Ihre bevorzugte IDE)  
- NuGet‑Paket `Aspose.OCR` (installieren Sie es via `dotnet add package Aspose.OCR`)  
- Eine Webcam oder jede Videoquelle, die `Bitmap`‑Frames liefern kann  

Keine zusätzlichen nativen Bibliotheken sind erforderlich; Aspose.OCR liefert alles, was Sie benötigen.

## Schritt 1: Aspose.OCR installieren und Namespaces hinzufügen

Bevor Sie Code schreiben, stellen Sie sicher, dass die Aspose‑OCR‑Bibliothek referenziert ist. Öffnen Sie ein Terminal in Ihrem Projektordner und führen Sie aus:

```bash
dotnet add package Aspose.OCR
```

Dann importieren Sie am Anfang Ihrer `Program.cs` die Namespaces, die wir verwenden werden:

```csharp
using Aspose.OCR;
using Aspose.OCR.Live;
using System.Drawing;
using System.Threading;
```

> **Pro‑Tipp:** Wenn Sie Visual Studio verwenden, schlägt die IDE die `using`‑Anweisungen automatisch vor, sobald Sie die Klassennamen eingeben.

## Schritt 2: Das LiveOcr‑Objekt erstellen und konfigurieren

Das Herzstück des Tutorials ist das `LiveOcr`‑Objekt. Wir müssen ihm mitteilen, welche Sprache es erkennen soll, und optional Vorverarbeitungs‑Filter (wie Deskewing) anwenden, um die Genauigkeit zu verbessern.

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

Warum die Sprache festlegen? OCR‑Engines verwenden sprachspezifische Wörterbücher und Zeichenmodelle; die Angabe von Englisch reduziert Fehlalarme und beschleunigt die Erkennung. Wenn Sie eine andere Sprache benötigen, ersetzen Sie einfach `Language.English` durch `Language.Spanish`, `Language.French` usw.

## Schritt 3: Frames von Ihrer Kamera erfassen

In einem echten Projekt würden Sie die Platzhaltermethode `CaptureFrameFromCamera()` durch tatsächliche Erfassungslogik ersetzen – vielleicht mit `AForge.Video`, `OpenCvSharp` oder der Windows‑Media‑Capture‑API. Für dieses Tutorial behalten wir die Methode abstrakt, zeigen aber ein kurzes Beispiel mit `AForge`.

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

> **Randfall:** Wenn die Kamera nicht verfügbar ist, gibt `CaptureFrameFromCamera` `null` zurück. Schützen Sie sich in Produktionscode immer davor.

## Schritt 4: Jeden Frame verarbeiten, bis Text gefunden wird

Jetzt iterieren wir über eine feste Anzahl von Frames (oder unendlich) und übergeben jedes Bitmap an `LiveOcr.ProcessFrame`. Sobald wir einen nicht‑leeren String erhalten, geben wir ihn aus und brechen die Schleife ab.

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

### Warum eine Pause?

`Thread.Sleep(30)` gibt dem Kameratreiber eine kurze Pause und reduziert die CPU‑Auslastung. In Hochleistungsszenarien könnten Sie es durch einen anspruchsvolleren Bildraten‑Controller ersetzen.

## Schritt 5: Alles in einer Konsolenanwendung zusammenfassen

Alles zusammengeführt, hier das vollständige, sofort kopier‑und‑einfüge‑bereite Programm. Speichern Sie es als `Program.cs` in einem neuen Konsolenprojekt (`dotnet new console`) und führen Sie `dotnet run` aus.

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

### Erwartete Ausgabe

Wenn die Kamera lesbaren englischen Text erkennt (z. B. ein gedrucktes Etikett), sehen Sie etwa Folgendes:

```
Starting live OCR… Press Ctrl+C to abort.
Detected text: OpenAI
Live OCR session ended.
```

Wenn nichts im Sichtfeld ist, beendet die Schleife nach 100 Durchläufen und gibt „Live OCR session ended.“ aus. Sie können die Iterationszahl erhöhen oder die `for`‑Schleife durch ein `while (true)` ersetzen, um endlos zu überwachen.

## Häufige Fragen & Stolperfallen

| Frage | Antwort |
|----------|--------|
| **Kann ich mehrere Sprachen gleichzeitig verarbeiten?** | Ja. Setzen Sie `Language = Language.English | Language.Spanish;` (Bitweise‑ODER), um ein mehrsprachiges Wörterbuch zu aktivieren. |
| **Was ist, wenn meine Frames groß sind und OCR langsam wirkt?** | Skalieren Sie das Bitmap vor dem Aufruf von `ProcessFrame` herunter. Beispiel: `Bitmap small = new Bitmap(frame, new Size(320, 240));` |
| **Benötige ich eine Lizenz für Aspose.OCR?** | Eine temporäre Evaluationslizenz funktioniert bis zu 30 Tage. Für die Produktion kaufen Sie eine Lizenz, um das Wasserzeichen zu entfernen. |
| **Wie gehe ich mit rotiertem Text um?** | Der `DeskewFilter` korrigiert bereits kleinere Rotationen. Für extreme Winkel fügen Sie der Pipeline einen `RotateFilter` hinzu. |
| **Ist dieser Ansatz thread‑sicher?** | `LiveOcr`‑Instanzen sind nicht thread‑sicher. Erstellen Sie pro Thread eine Instanz oder schützen Sie den Zugriff mit einem Lock. |

## Erweiterung des Tutorials

Jetzt, wo Sie eine **Live-OCR-Tutorial**‑Basis haben, denken Sie an die folgenden nächsten Schritte:

1. **Stream zu einer UI** – zeigen Sie das Live‑Video mit überlagerten OCR‑Ergebnissen mittels `Windows Forms` oder `WPF` an.  
2. **Batch‑Verarbeitung** – leiten Sie Frames in eine Warteschlange und führen Sie OCR in einem Hintergrund‑Worker‑Pool für höhere Durchsatzrate aus.  
3. **Spracherkennung** – integrieren Sie eine Sprachidentifikations‑Bibliothek, um `LiveOcr.Language` dynamisch zu wechseln.  
4. **Ergebnisse persistieren** – schreiben Sie erkannte Zeichenketten in eine Datenbank oder eine CSV‑Datei für Analysen.  

Jede dieser Erweiterungen beruht weiterhin auf den Kernkonzepten, die wir behandelt haben: Initialisierung von `LiveOcr`, **Festlegen der OCR‑Sprache** und **Erkennen von Text‑Video‑Frames** in Echtzeit.

---

### TL;DR

- Installieren Sie Aspose.OCR über NuGet.  
- Erstellen Sie ein `LiveOcr`‑Objekt, **setzen Sie die OCR‑Sprache** (Englisch im Beispiel).  
- Erfassen Sie `Bitmap`‑Frames von einer Kamera.  
- Durchlaufen Sie die Frames, rufen Sie `ProcessFrame` auf und stoppen Sie, sobald Text erscheint.  
- Das obige vollständige Programm ist sofort ausführbar und dient als solide Basis für jedes Echtzeit‑Texterkennungs‑Projekt.

Probieren Sie es aus, passen Sie die Vorverarbeitungspipeline an und sehen Sie zu, wie Ihre App die Welt Bild für Bild zu lesen beginnt. Viel Spaß beim Coden!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}