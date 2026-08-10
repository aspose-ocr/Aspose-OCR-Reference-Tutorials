---
category: general
date: 2026-02-14
description: Erfahren Sie, wie Sie OCR auf einer TIFF‑Datei oder einem Bild durchführen
  und PDFs mithilfe von OCR in durchsuchbare PDFs umwandeln – Schritt‑für‑Schritt‑C#‑Anleitung.
draft: false
keywords:
- how to perform OCR
- convert pdf using OCR
- make searchable pdf
- tiff to searchable pdf
- searchable pdf from image
language: de
og_description: Entdecken Sie, wie Sie OCR auf Bildern durchführen, PDFs mit OCR konvertieren
  und ein durchsuchbares PDF mit Aspose OCR in einem prägnanten C#‑Tutorial erstellen.
og_title: Wie man OCR durchführt und ein durchsuchbares PDF in C# erstellt
tags:
- OCR
- C#
- Aspose
- PDF conversion
title: Wie man OCR durchführt und ein durchsuchbares PDF in C# erstellt
url: /de/net/text-recognition/how-to-perform-ocr-and-create-a-searchable-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man OCR durchführt und ein durchsuchbares PDF in C# erstellt

Haben Sie schon einmal **OCR durchführen** müssen, um ein gescanntes Dokument zu verarbeiten, waren sich aber nicht sicher, wie Sie das Ergebnis in ein durchsuchbares PDF verwandeln können? Sie sind nicht allein – viele Entwickler stoßen auf dieses Problem, wenn sie mit alten TIFF‑Archiven oder PDFs, die nur aus Bildern bestehen, arbeiten. Die gute Nachricht? Mit ein paar Zeilen C#‑Code und der Aspose.OCR‑Bibliothek können Sie ein TIFF oder jedes andere Bild in Sekundenschnelle in ein vollständig durchsuchbares PDF umwandeln.

In diesem Tutorial führen wir Sie durch alles, was Sie wissen müssen: von der Installation der Bibliothek, dem Laden eines mehrseitigen TIFFs, bis zum Aufruf von `RecognizeToPdf`, sodass Sie **PDF mit OCR konvertieren** und **durchsuchbare PDF**‑Dateien erstellen können, die Ihre Benutzer tatsächlich durchsuchen können. Am Ende haben Sie eine lauffähige Konsolenanwendung, die aus einer Bildquelle ein durchsuchbares PDF erzeugt.

## Voraussetzungen

- **.NET 6.0** oder höher (der Code funktioniert auch mit .NET Framework 4.7+).
- Eine gültige **Aspose.OCR**‑Lizenz oder ein temporärer Evaluierungsschlüssel (die kostenlose Testversion reicht für Tests aus).
- Visual Studio 2022 (oder ein beliebiger anderer Editor) mit dem **NuGet**‑Paket‑Manager.
- Eine Eingabedatei namens `input.tif`, die Sie in einem Ordner Ihrer Wahl abgelegt haben – mehrseitige TIFFs funktionieren sofort.

> **Pro‑Tipp:** Wenn Sie Windows verwenden, kopieren Sie das TIFF in denselben Ordner wie die kompilierte `.exe`, um Pfad‑Probleme zu vermeiden.

## Schritt 1: Das Aspose.OCR‑NuGet‑Paket installieren

Öffnen Sie Ihr Projektverzeichnis in einem Terminal und führen Sie aus:

```bash
dotnet add package Aspose.OCR
```

Damit wird die neueste stabile Version (Stand Februar 2026 ist das 23.10) heruntergeladen und alle erforderlichen Abhängigkeiten hinzugefügt. Nach Abschluss der Wiederherstellung sehen Sie `Aspose.OCR` unter **Dependencies** im Solution Explorer.

## Schritt 2: Eine minimale Konsolenanwendung erstellen

Erstellen Sie ein neues Konsolenprojekt, falls Sie noch keines haben:

```bash
dotnet new console -n OcrSearchablePdfDemo
cd OcrSearchablePdfDemo
```

Ersetzen Sie die automatisch erzeugte `Program.cs` durch den vollständigen Code aus **Schritt 3**. Das Programm wird:

1. Die OCR‑Engine instanziieren.  
2. Das Quellbild (oder das mehrseitige TIFF) laden.  
3. OCR ausführen und die Ausgabe direkt in ein durchsuchbares PDF schreiben.  
4. Den Benutzer darüber informieren, dass der Vorgang erfolgreich war.

## Schritt 3: Vollständiger Beispielcode – Von Bild zu durchsuchbarem PDF

Unten finden Sie die **gesamte** Quelldatei. Kopieren Sie sie in `Program.cs`. Kommentare erklären die weniger offensichtlichen Teile.

```csharp
using System;
using Aspose.OCR;          // Core OCR namespace
using Aspose.OCR.Image;   // Provides ImageStream helpers

namespace OcrSearchablePdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣ Initialise the OCR engine.
            // -------------------------------------------------
            // The Engine class is the entry point for all OCR operations.
            // You can optionally pass a license object here if you have one.
            var ocrEngine = new Engine();

            // -------------------------------------------------
            // 2️⃣ Load the source image.
            // -------------------------------------------------
            // ImageStream.FromFile supports TIFF, PDF, JPEG, PNG, etc.
            // For multi‑page TIFFs the stream automatically contains all pages.
            string inputPath = "YOUR_DIRECTORY/input.tif";
            var imageStream = ImageStream.FromFile(inputPath);

            // -------------------------------------------------
            // 3️⃣ Perform OCR and write a searchable PDF.
            // -------------------------------------------------
            // RecognizeToPdf does the heavy lifting:
            // • It runs the OCR engine on every page.
            // • It embeds the extracted text as an invisible layer.
            // • The visual appearance of the original image is preserved.
            string outputPath = "YOUR_DIRECTORY/searchable.pdf";
            ocrEngine.RecognizeToPdf(imageStream, outputPath);

            // -------------------------------------------------
            // 4️⃣ Inform the user.
            // -------------------------------------------------
            Console.WriteLine("Searchable PDF created at: " + outputPath);
        }
    }
}
```

**Was Sie sehen werden:** Nach dem Ausführen des Programms erscheint im Zielordner eine Datei namens `searchable.pdf`. Öffnen Sie sie in Adobe Reader oder einem anderen PDF‑Betrachter und suchen Sie nach einem Wort, das im ursprünglichen TIFF vorkommt. Der Text sollte sofort gefunden werden, was beweist, dass Sie erfolgreich **durchsuchbare PDF** aus einem Bild erstellt haben.

### Die Anwendung ausführen

```bash
dotnet run
```

Wenn alles korrekt eingerichtet ist, erhalten Sie:

```
Searchable PDF created at: YOUR_DIRECTORY/searchable.pdf
```

Öffnen Sie das PDF, drücken Sie `Ctrl+F`, geben Sie ein Wort aus der Quelle ein und beobachten Sie, wie die Hervorhebung zur richtigen Stelle springt.

## Schritt 4: Häufige Varianten und Sonderfälle

### Ein reguläres PDF (nur Bild) in ein durchsuchbares PDF umwandeln

Wenn Ihre Quelle ein PDF ist, das gescannte Bilder statt Text enthält, können Sie dieselbe Methode verwenden – ändern Sie lediglich die Quelle des `ImageStream`:

```csharp
var pdfStream = ImageStream.FromFile("YOUR_DIRECTORY/input.pdf");
ocrEngine.RecognizeToPdf(pdfStream, "YOUR_DIRECTORY/searchable_from_pdf.pdf");
```

Damit decken Sie das Szenario **PDF mit OCR konvertieren** ab, ohne zusätzlichen Code.

### Verarbeitung großer mehrseitiger Dokumente

Für Dokumente mit mehreren hundert Seiten sollten Sie Folgendes berücksichtigen:

- **Speicherlimits erhöhen** (`Engine.MemoryLimit = 2_000; // MB`).  
- **In Teilen verarbeiten**: Laden Sie einen Teil der Seiten, schreiben Sie Zwischenergebnisse als PDFs und fügen Sie sie anschließend mit einer PDF‑Bibliothek (z. B. Aspose.PDF) zusammen.

### Umgang mit anderen Sprachen als Englisch

Aspose.OCR unterstützt viele Sprachen out of the box. Setzen Sie die Sprache vor der Erkennung:

```csharp
ocrEngine.Language = OcrLanguage.French; // or OcrLanguage.Spanish, etc.
```

Wenn Sie **tiff zu durchsuchbarem pdf** in einer nicht‑lateinischen Schrift benötigen, stellen Sie sicher, dass das passende Sprachpaket installiert ist.

### Was tun, wenn das Ausgabepdf leer ist?

- Prüfen Sie, ob die Eingabedatei beschädigt ist.  
- Stellen Sie sicher, dass die OCR‑Engine über eine gültige Lizenz verfügt – im Evaluierungsmodus können Seitenlimits gelten.  
- Vergewissern Sie sich, dass die Bildauflösung mindestens 300 dpi beträgt; niedrigere Auflösungen führen zu schlechter Erkennung.

## Schritt 5: Das Ergebnis programmgesteuert verifizieren (optional)

Manchmal möchte man sicherstellen, dass das PDF tatsächlich eine Textebene enthält. Dafür können Sie Aspose.PDF zum Extrahieren von Text verwenden:

```csharp
using Aspose.Pdf;

var pdfDoc = new Document("YOUR_DIRECTORY/searchable.pdf");
string extracted = pdfDoc.Pages[1].ExtractText();
Console.WriteLine("First page text snippet: " + extracted.Substring(0, 100));
```

Wenn `extracted` nicht leer ist, haben Sie erfolgreich **durchsuchbare pdf** erstellt.

## Fazit

Wir haben gezeigt, **wie man OCR** auf ein TIFF (oder jedes Bild) anwendet und nahtlos **PDF mit OCR konvertiert**, um ein **durchsuchbares PDF** zu erzeugen, das sich wie ein natives Dokument verhält. Die wichtigsten Schritte sind:

1. Aspose.OCR installieren.  
2. `Engine` initialisieren.  
3. Das Bild über `ImageStream` laden.  
4. `RecognizeToPdf` aufrufen.  

Ab hier können Sie mit Spracheinstellungen experimentieren, große Stapel verarbeiten oder die Ausgabe mit anderen PDF‑Manipulationen kombinieren. Das gleiche Muster funktioniert für **tiff zu durchsuchbarem pdf**, **durchsuchbare pdf aus Bild** und sogar für gescannte PDFs.

Bereit für die nächste Herausforderung? Versuchen Sie, OCR in eine Web‑API einzubetten, sodass Benutzer Scans hochladen und sofort durchsuchbare PDFs erhalten, oder erkunden Sie OCR für handschriftliche Notizen mithilfe der erweiterten Einstellungen des `OcrEngine`. Die Möglichkeiten sind endlos – happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}