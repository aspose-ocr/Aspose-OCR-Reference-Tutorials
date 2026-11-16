---
category: general
date: 2026-02-28
description: Erstellen Sie ein durchsuchbares PDF in C# durch vertikales Kombinieren
  von Bildern. Erfahren Sie, wie Sie Bilder vertikal stapeln und gescannte PDF‑Seiten
  mit Aspose OCR konvertieren.
draft: false
keywords:
- create searchable pdf
- combine images vertically
- how to stack images vertically
- convert scanned pages pdf
language: de
og_description: Erstellen Sie ein durchsuchbares PDF in C# durch vertikales Kombinieren
  von Bildern. Diese Anleitung zeigt, wie man Bilder vertikal stapelt und gescannte
  PDF‑Seiten mit Aspose OCR konvertiert.
og_title: Durchsuchbares PDF in C# erstellen – Bilder vertikal kombinieren
tags:
- Aspose OCR
- C#
- PDF generation
title: Durchsuchbares PDF in C# erstellen – Bilder vertikal kombinieren
url: /de/net/text-recognition/create-searchable-pdf-in-c-combine-images-vertically/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Durchsuchbares PDF in C# erstellen – Bilder vertikal kombinieren

Haben Sie jemals **ein durchsuchbares PDF** aus ein paar gescannten PNGs erstellen müssen, wussten aber nicht, wo Sie anfangen sollen? Sie sind nicht allein. In vielen Dokument‑Automatisierungsprojekten ist das größte Problem, einen Stapel Bilddateien in ein übersichtliches, durchsuchbares PDF zu verwandeln, das Sie indexieren und teilen können.  

In diesem Tutorial führen wir Sie durch ein vollständiges, sofort ausführbares Beispiel, das Ihnen zeigt, **wie man Bilder vertikal stapelt**, **Bilder vertikal kombiniert** und schließlich **gescannte Seiten in ein PDF konvertiert**, um ein einziges durchsuchbares Dokument mit der GPU‑beschleunigten Engine von Aspose.OCR zu erstellen. Am Ende haben Sie ein eigenständiges Programm, das Sie in jede .NET‑Lösung einbinden können.

> **Was Sie lernen werden**
> - Initialisieren einer OCR‑Engine mit GPU‑Unterstützung.
> - Verarbeiten eines Bildbatches parallel.
> - **Bilder vertikal kombinieren**, um einen mehrseitigen Scan zu simulieren.
> - Exportieren eines durchsuchbaren PDFs und eines detaillierten JSON‑Berichts für nachgelagerte Analysen.

## Voraussetzungen

- .NET 6+ (der Code kompiliert mit .NET 6, .NET 7 oder .NET 8)
- Aspose.OCR NuGet‑Paket (`Install-Package Aspose.OCR`)
- Ein GPU‑fähiger Rechner, wenn Sie die Einstellung `ProcessingMode.Gpu` beibehalten möchten (CPU‑Fallback funktioniert ebenfalls)
- Ein Ordner mit einigen gescannten PNG/JPEG‑Dateien (das Demo verwendet `page1.png`, `page2.png`, `page3.png`)

Keine externen Dienste, keine versteckten Konfigurationsdateien – nur reines C#.

## Schritt 1 – OCR‑Engine einrichten, um **durchsuchbares PDF** zu erstellen

Zuerst erstellen wir eine `OcrEngine`, aktivieren die GPU‑Beschleunigung, wählen Englisch als Sprache und fügen ein paar Vorverarbeitungsfilter hinzu. Diese Filter verbessern die Genauigkeit, indem sie schiefe Seiten begradigen (`DeskewFilter`) und Rauschen entfernen (`DenoiseFilter`).

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;
using System.Collections.Generic;
using System.Drawing;

class AllInOneDemo
{
    static void Main()
    {
        // Initialize OCR engine – this is the heart of creating a searchable PDF
        var ocrEngine = new OcrEngine
        {
            ProcessingMode = ProcessingMode.Gpu,   // Switch to CPU if no GPU
            Language = OcrLanguage.English
        };
        // Pre‑processing improves OCR quality
        ocrEngine.Filters.Add(new DeskewFilter());
        ocrEngine.Filters.Add(new DenoiseFilter());
```

**Warum das wichtig ist:** Die OCR‑Engine übernimmt die schwere Arbeit der Texterkennung. Das Aktivieren von `ProcessingMode.Gpu` kann die Erkennungszeit auf einer modernen Grafikkarte halbieren, während die Filter gängige Scan‑Artefakte reduzieren, die sonst fehlerhafte Ausgaben erzeugen würden.

## Schritt 2 – Batch‑Prozessor konfigurieren, um **gescannte Seiten PDF** effizient zu konvertieren

Das Verarbeiten jeder Seite einzeln ist für ein paar Bilder in Ordnung, aber reale Projekte umfassen oft Dutzende oder Hunderte von Seiten. Aspose.OCRs `OcrBatchProcessor` ermöglicht es uns, Erkennungen parallel auszuführen und beschleunigt den Schritt **gescannte Seiten PDF konvertieren** erheblich.

```csharp
        // Set up batch processor – ideal for converting many scanned pages to PDF
        var batchProcessor = new OcrBatchProcessor
        {
            MaxDegreeOfParallelism = 2,          // Adjust based on CPU/GPU cores
            Language = OcrLanguage.English,
            ProcessingMode = ProcessingMode.Gpu
        };

        // List the image files you want to turn into a searchable PDF
        List<string> imageFiles = new()
        {
            "YOUR_DIRECTORY/page1.png",
            "YOUR_DIRECTORY/page2.png",
            "YOUR_DIRECTORY/page3.png"
        };
```

**Profi‑Tipp:** Wenn Sie nur eine CPU‑Box haben, setzen Sie `ProcessingMode = ProcessingMode.Cpu`. Der Batch‑Prozessor respektiert weiterhin `MaxDegreeOfParallelism`, sodass Sie ihn anpassen können, um eine Überlastung des Rechners zu vermeiden.

## Schritt 3 – OCR auf dem Batch ausführen und Ergebnisse sammeln

Jetzt erkennen wir tatsächlich den Text. Die Methode `Recognize` gibt eine Liste von `OcrResult`‑Objekten zurück, die jeweils das Originalbild und den extrahierten Text enthalten.

```csharp
        // Run OCR on all images at once
        List<OcrResult> ocrResults = batchProcessor.Recognize(imageFiles);
```

An diesem Punkt haben Sie alles, was Sie benötigen, um **ein durchsuchbares PDF** zu erstellen: die Bilder (noch im Speicher) und die zugehörigen Textebenen.

## Schritt 4 – **Bilder vertikal kombinieren** und das durchsuchbare PDF erzeugen

Die meisten gescannten Dokumente sind mehrseitige PDFs, daher müssen wir die einzelnen Seitenbilder zu einem hohen Bild zusammenfügen, das einen physischen Stapel nachbildet. Aspose.OCR stellt dafür `Image.CombineVertical` bereit.

```csharp
        // Stitch the page images into one tall image – this is how we **combine images vertically**
        using var combinedImage = Image.CombineVertical(
            ocrResults.ConvertAll(r => r.Image));

        // Finally, create a searchable PDF from the combined image
        ocrEngine.RecognizeToPdf(combinedImage, "YOUR_DIRECTORY/combined_searchable.pdf");
```

Die resultierende Datei (`combined_searchable.pdf`) enthält auswählbaren, durchsuchbaren Text unter jedem Seitenbild – genau das, was Sie benötigen, um **ein durchsuchbares PDF** aus gescannten Quellen zu erstellen.

![Beispiel für durchsuchbares PDF](/images/create-searchable-pdf.png "Beispiel für durchsuchbares PDF")

*Bildbeschreibung: Beispiel für durchsuchbares PDF, das ein kombiniertes PDF mit durchsuchbarem Text zeigt.*

**Warum vertikales Stapeln?** Viele OCR‑Bibliotheken behandeln jedes Bild als separate Seite. Durch das Stapeln behalten wir die Seitenreihenfolge des PDFs bei, während wir dennoch einen einzigen OCR‑Durchlauf für das gesamte Dokument nutzen.

## Schritt 5 – Detailliertes JSON für die erste Seite exportieren (ideal für nachgelagerte Workflows)

Manchmal benötigen Sie mehr als ein PDF; vielleicht möchten Sie die OCR‑Daten in eine Datenbank oder eine Machine‑Learning‑Pipeline einspeisen. Aspose.OCR ermöglicht es, jedes `OcrResult` in JSON zu serialisieren und dabei Begrenzungsrahmen, Vertrauenswerte und mehr zu erhalten.

```csharp
        // Dump the first page’s OCR result to pretty‑printed JSON
        string jsonOutput = ocrResults[0].ToJson(prettyPrint: true);
        Console.WriteLine("--- JSON for first page ---");
        Console.WriteLine(jsonOutput);
    }
}
```

**Erwarteter JSON‑Auszug (gekürzt):**

```json
{
  "Text": "Sample scanned text …",
  "Confidence": 0.97,
  "Blocks": [
    {
      "Text": "Header",
      "BoundingBox": { "X": 15, "Y": 10, "Width": 480, "Height": 30 }
    }
    // …
  ]
}
```

Sie können dieses JSON nun in jedes nachgelagerte System einspeisen – egal, ob Sie den Text in Elasticsearch indexieren oder es in ein benutzerdefiniertes Analyse‑Dashboard einbinden.

---

## Wie man **Bilder vertikal stapelt** – Eine kurze Zusammenfassung

Wenn Sie sich fragen, **wie man Bilder vertikal stapelt** ohne Aspose, könnten Sie `System.Drawing` verwenden, um ein neues Bitmap zu erstellen und jede Seite nacheinander zu zeichnen. Allerdings kümmert sich Aspose’s integrierte `Image.CombineVertical` um DPI, Pixelformat und Speicherverwaltung, was sie zur zuverlässigsten Wahl für Produktionscode macht.

### Alternative: Verwendung von `System.Drawing` (nur aus Neugierde)

```csharp
int totalHeight = 0;
int maxWidth = 0;
foreach (var img in ocrResults)
{
    totalHeight += img.Image.Height;
    maxWidth = Math.Max(maxWidth, img.Image.Width);
}
var canvas = new Bitmap(maxWidth, totalHeight);
using var g = Graphics.FromImage(canvas);
int offset = 0;
foreach (var img in ocrResults)
{
    g.DrawImage(img.Image, 0, offset);
    offset += img.Image.Height;
}
canvas.Save("combined_manual.png");
```

Der manuelle Ansatz funktioniert, aber Sie verlieren die Bequemlichkeit der automatischen DPI‑Verarbeitung und die Möglichkeit, das Ergebnis direkt zurück in `RecognizeToPdf` zu speisen. Bleiben Sie bei `CombineVertical`, es sei denn, Sie haben eine sehr spezielle Anforderung.

## Häufige Fallstricke & wie man sie vermeidet

| Problem | Warum es passiert | Lösung |
|-------|----------------|-----|
| **Out‑of‑Memory‑Fehler** beim Verarbeiten von Dutzenden hochauflösenden Scans | Jedes Bild bleibt im Speicher, bis das PDF geschrieben wird | Entsorgen Sie `Image`‑Objekte sofort nach Gebrauch (`using`‑Blöcke) oder reduzieren Sie die Bildgröße vor dem Kombinieren |
| **Unsinniger Text** nach OCR | Schiefe Scans oder geringer Kontrast | Behalten Sie den `DeskewFilter` und `DenoiseFilter`; erwägen Sie bei Bedarf das Hinzufügen von `ContrastFilter` |
| **Fehlende durchsuchbare Ebene** | `Recognize` anstelle von `RecognizeToPdf` verwendet | Stellen Sie sicher, dass Sie `ocrEngine.RecognizeToPdf` auf dem kombinierten Bild aufrufen |
| **GPU‑Fallback schlägt fehl** auf Maschinen ohne passende Treiber | `ProcessingMode.Gpu` wirft eine Ausnahme | Umschließen Sie die Engine‑Erstellung in einem try/catch und fallen Sie auf `ProcessingMode.Cpu` zurück |

## Nächste Schritte – Workflow erweitern

Jetzt, da Sie wissen, wie man **ein durchsuchbares PDF** erstellt, möchten Sie vielleicht:

- **Batch‑Verarbeitung ganzer Ordner** mit `Directory.GetFiles` und einer `foreach`‑Schleife.
- **Wasserzeichen hinzufügen** zu jeder Seite vor dem Kombinieren (verwenden Sie `ImageProcessor` aus Aspose.Imaging).
- **Das durchsuchbare PDF wieder in einzelne Seiten aufteilen**, falls Sie später PDFs pro Seite benötigen (`PdfDocument.Split` aus Aspose.PDF).
- **Integration mit Azure Blob Storage**, um Bilder aus der Cloud zu holen und das finale PDF zurückzuschieben.

All diese Erweiterungen basieren natürlich auf denselben Kernkonzepten: OCR‑Einrichtung, Bildverarbeitung und PDF‑Export.

---

## Fazit

Wir haben alles behandelt, was Sie benötigen, um **ein durchsuchbares PDF** aus einer Sammlung gescannter Bilder in C# zu **erstellen**. Durch das Initialisieren einer GPU‑fähigen `OcrEngine`, das Ausführen eines parallelen Batches mit `OcrBatchProcessor`, **vertikales Kombinieren von Bildern** und schließlich das Aufrufen von `RecognizeToPdf` erhalten Sie ein übersichtliches, durchsuchbares Dokument, das bereit für Archivierung oder Indexierung ist. Der zusätzliche JSON‑Export verschafft Ihnen volle Transparenz über die OCR‑Ergebnisse und eröffnet Möglichkeiten für Analysen oder benutzerdefinierte Workflows.

Probieren Sie es aus, experimentieren Sie mit verschiedenen Filtern und beobachten Sie, wie Ihre Dokument‑Automatisierungspipeline deutlich reibungsloser wird. Wenn Sie auf Probleme stoßen, hinterlassen Sie einen Kommentar – happy coding!

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}