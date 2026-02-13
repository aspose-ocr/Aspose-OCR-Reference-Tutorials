---
category: general
date: 2026-02-13
description: Erfahren Sie, wie Sie OCR in C# verwenden, um Text aus Bilddateien zu
  extrahieren, GPU‑Verarbeitung zu aktivieren und Scans schnell in Text umzuwandeln.
draft: false
keywords:
- how to use OCR
- extract text from image
- how to extract text
- convert scan to text
- enable gpu processing
language: de
og_description: Wie verwendet man OCR in C#? Dieser Leitfaden zeigt, wie man Text
  aus Bilddateien extrahiert, GPU‑Verarbeitung aktiviert und Scans in Text umwandelt.
og_title: Wie man OCR in C# verwendet – Text aus Bildern mit GPU extrahieren
tags:
- OCR
- C#
- Aspose
- GPU
- Image Processing
title: Wie man OCR in C# verwendet – Text aus Bildern mit GPU extrahieren
url: /de/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-images-with-gpu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man OCR in C# verwendet – Text aus Bildern mit GPU extrahieren

Haben Sie sich jemals gefragt, **wie man OCR** nutzt, um Text aus einem gescannten Dokument zu holen, ohne ins Schwitzen zu geraten? Sie sind nicht allein – Entwickler fragen ständig: „Wie kann ich Text aus Bilddateien effizient extrahieren?“ Die gute Nachricht: Mit Aspose.OCR können Sie genau das tun und sogar **GPU‑Verarbeitung aktivieren**, um auf unterstützter Hardware einen spürbaren Geschwindigkeitsvorteil zu erzielen.

In diesem Tutorial führen wir Sie durch ein vollständiges, End‑to‑End‑Beispiel, das zeigt, **wie man OCR verwendet**, wie man **Text aus Bild extrahiert**, wie man **Scan zu Text konvertiert** und was zu tun ist, wenn die GPU nicht verfügbar ist. Am Ende haben Sie eine lauffähige C#‑Konsolen‑App, die den erkannten Text ausgibt und anzeigt, ob die GPU tatsächlich verwendet wurde.

## Was Sie benötigen

- .NET 6 SDK oder neuer (der Code funktioniert auch mit .NET Core)  
- Visual Studio 2022 oder ein beliebiger Editor Ihrer Wahl  
- Aspose.OCR für .NET‑Paket (verfügbar über NuGet)  
- Eine hochauflösende Bilddatei (z. B. `highres_scan.tif`) zum Testen  

Keine aufwändige Einrichtung nötig – nur ein paar NuGet‑Befehle und Sie können loslegen.

## Schritt 1: Aspose.OCR installieren und das Projekt vorbereiten

Zuerst müssen Sie die OCR‑Bibliothek in Ihr Projekt einbinden. Öffnen Sie ein Terminal im Ordner Ihrer Lösung und führen Sie aus:

```bash
dotnet new console -n OcrDemo
cd OcrDemo
dotnet add package Aspose.OCR
```

Damit wird ein frisches Konsolenprojekt namens **OcrDemo** erstellt und das NuGet‑Paket `Aspose.OCR` hinzugefügt. Die Bibliothek enthält die Klasse `OcrEngine`, die wir verwenden werden.

> **Profi‑Tipp:** Wenn Sie an einem Rechner mit dedizierter GPU arbeiten, stellen Sie sicher, dass der neueste Grafiktreiber installiert ist; andernfalls fällt die Bibliothek automatisch in den CPU‑Modus zurück.

## Schritt 2: Den vollständigen OCR‑Code schreiben

Öffnen Sie nun `Program.cs` und ersetzen Sie den Inhalt durch das Folgende. Jede Zeile ist kommentiert, damit Sie *warum* wir etwas tun, nachvollziehen können.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Enums;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣  Create an OCR engine and request GPU processing.
            //    If the GPU isn’t present, Aspose.OCR will silently
            //    switch to CPU mode – no crash, no extra code needed.
            // -------------------------------------------------
            var ocrEngine = new OcrEngine
            {
                ProcessingMode = OcrProcessingMode.Gpu
            };

            // -------------------------------------------------
            // 2️⃣  Define the path to the image you want to process.
            //    Replace the placeholder with the actual file location.
            // -------------------------------------------------
            string imagePath = @"YOUR_DIRECTORY/highres_scan.tif";

            // -------------------------------------------------
            // 3️⃣  Perform the recognition. The method returns an
            //    OcrResult object that contains the extracted text,
            //    confidence scores, and more.
            // -------------------------------------------------
            OcrResult ocrResult = ocrEngine.RecognizeImage(imagePath);

            // -------------------------------------------------
            // 4️⃣  Report whether the GPU was really used.
            //    This is handy for debugging performance issues.
            // -------------------------------------------------
            Console.WriteLine($"GPU used: {ocrEngine.IsGpuEnabled}");

            // -------------------------------------------------
            // 5️⃣  Output the recognized text to the console.
            //    In a real app you might write this to a file,
            //    a database, or feed it into another workflow.
            // -------------------------------------------------
            Console.WriteLine("=== Extracted Text ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

### Warum das funktioniert

- **ProcessingMode = Gpu** weist die Engine an, zuerst die GPU zu versuchen. Die Bibliothek abstrahiert die low‑level CUDA/OpenCL‑Aufrufe, sodass Sie keine Geräte‑Kontexte selbst verwalten müssen.  
- **IsGpuEnabled** ist ein boolescher Wert, der bestätigt, ob der GPU‑Pfad erfolgreich war. Wenn Sie `false` sehen, ist die Engine automatisch auf die CPU zurückgefallen – kein Grund zur Panik.  
- **RecognizeImage** erledigt die schwere Arbeit: Sie lädt das Bild, führt das OCR‑Modell aus und gibt das reine Text‑Ergebnis zurück. Keine manuelle Vorverarbeitung des Bitmaps nötig, es sei denn, Sie haben spezielle Anforderungen (z. B. Deskewing).

## Schritt 3: Die Anwendung ausführen und die Ausgabe prüfen

Kompilieren und ausführen:

```bash
dotnet run
```

Wenn alles korrekt eingerichtet ist, sehen Sie etwa Folgendes:

```
GPU used: True
=== Extracted Text ===
This is the first line of the scanned document.
Here is the second line, and so on…
```

Ist die GPU nicht verfügbar, lautet die erste Zeile `GPU used: False`, aber der extrahierte Text wird trotzdem angezeigt – dank des eleganten Fallbacks.

> **Häufige Frage:** *Was, wenn mein Bild ein JPEG statt eines TIFF ist?*  
> Die Methode `RecognizeImage` akzeptiert jedes Format, das von .NETs `System.Drawing` unterstützt wird (JPEG, PNG, BMP usw.). Ändern Sie einfach die Dateierweiterung in `imagePath`.

## Schritt 4: Optional – Einstellungen für bessere Genauigkeit anpassen

Aspose.OCR bietet ein paar Stellschrauben, die Sie drehen können:

| Einstellung | Was sie bewirkt | Wann zu verwenden |
|------------|----------------|-------------------|
| `ocrEngine.Language` | Erzwingt eine bestimmte Sprache (z. B. `OcrLanguage.English`) | Wenn Sie die Sprache des Dokuments kennen |
| `ocrEngine.PageSegMode` | Steuert, wie die Engine Seiten in Blöcke aufteilt | Für mehrspaltige Layouts |
| `ocrEngine.DetectOrientation` | Dreht Text automatisch, der nicht aufrecht ist | Scans, die eventuell verkehrt herum sind |

Sie können diese Eigenschaften setzen, bevor Sie `RecognizeImage` aufrufen. Beispiel:

```csharp
ocrEngine.Language = OcrLanguage.English;
ocrEngine.DetectOrientation = true;
```

## Schritt 5: Ablauf visualisieren (Bild mit Alt‑Text)

Unten finden Sie ein einfaches Diagramm, das **wie man OCR** mit optionaler GPU‑Beschleunigung verwendet, veranschaulicht. Es ist nicht erforderlich, damit der Code läuft, hilft aber, das Gesamtbild zu verstehen.

![Diagram showing how to use OCR with GPU processing](/images/ocr-gpu-flow.png)

*Alt‑Text:* *Diagramm, das zeigt, wie OCR mit GPU‑Verarbeitung verwendet wird und den Fallback zur CPU bei Bedarf hervorhebt.*

## Randfälle & Fehlersuche

1. **Out‑of‑Memory auf der GPU** – Sehr große Bilder können den GPU‑Speicher überschreiten. In diesem Fall wechselt die Bibliothek automatisch zur CPU. Sie können das Bild vorher skalieren, um den Speicherverbrauch gering zu halten.  
2. **Nicht unterstütztes Bildformat** – Wenn `RecognizeImage` eine *NotSupportedException* wirft, prüfen Sie die Dateierweiterung und stellen Sie sicher, dass das Bild nicht beschädigt ist. Das Konvertieren zu PNG löst das Problem häufig.  
3. **Niedrige Konfidenzwerte** – Enthält das OCR‑Ergebnis viele unlesbare Zeichen, sollten Sie eine Vorverarbeitung (Binarisierung, Rauschunterdrückung) in Betracht ziehen oder zu einem hochauflösenderen Scan wechseln.  

## Zusammenfassung: Was wir erreicht haben

Wir haben gerade **wie man OCR** in einer C#‑Konsolen‑App verwendet, gezeigt, wie man **Text aus Bild**‑Dateien **extrahiert**, und demonstriert, wie man **GPU‑Verarbeitung** für schnellere Ergebnisse **aktiviert**. Sie wissen jetzt, wie man **Scan zu Text** **konvertiert**, prüft, ob die GPU tatsächlich eingesetzt wurde, und ein paar Einstellungen für Randfall‑Szenarien anpasst.

### Nächste Schritte

- Versuchen Sie, die Ausgabe in einen **Suchindex** (z. B. Elasticsearch) zu speisen, damit Ihre gescannten PDFs durchsuchbar werden.  
- Experimentieren Sie mit **Batch‑Verarbeitung** – iterieren Sie über einen Ordner mit Bildern und schreiben Sie jedes Ergebnis in eine `.txt`‑Datei.  
- Kombinieren Sie OCR mit **Übersetzungs‑APIs**, um gescannte Fremdsprachen‑Dokumente automatisch zu übersetzen.  

Haben Sie weitere Fragen? Hinterlassen Sie einen Kommentar, und happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}