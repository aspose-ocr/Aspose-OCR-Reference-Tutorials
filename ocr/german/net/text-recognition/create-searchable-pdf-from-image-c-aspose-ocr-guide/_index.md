---
category: general
date: 2026-05-06
description: Erstellen Sie ein durchsuchbares PDF aus einem Bild mit Aspose OCR in
  C#. Lernen Sie, PNG in PDF zu konvertieren, Text aus dem Bild zu extrahieren und
  ein durchsuchbares PDF zu erzeugen.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- extract text from image
- convert png to pdf
- ocr image to pdf
language: de
og_description: Erstellen Sie ein durchsuchbares PDF aus einem Bild mit Aspose OCR
  in C#. Dieses Schritt‑für‑Schritt‑Tutorial zeigt, wie man PNG in PDF konvertiert,
  Text aus dem Bild extrahiert und ein durchsuchbares PDF erstellt.
og_title: Erstellen einer durchsuchbaren PDF aus Bild – C# Aspose OCR‑Leitfaden
tags:
- Aspose
- C#
- OCR
- PDF
title: Durchsuchbares PDF aus Bild erstellen – C# Aspose OCR‑Leitfaden
url: /de/net/text-recognition/create-searchable-pdf-from-image-c-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Durchsuchbares PDF aus Bild erstellen – C# Aspose OCR Anleitung

Haben Sie jemals **ein durchsuchbares PDF** aus einem gescannten Bild erstellen müssen, wussten aber nicht, wo Sie anfangen sollen? Vielleicht haben Sie einen PNG‑Beleg, ein JPEG eines Vertrags oder irgendeine Bitmap, die Sie in ein PDF umwandeln möchten, das Sie tatsächlich durchsuchen können. Das ist ein häufiges Problem, besonders wenn Sie mit alten Scans zu tun haben, die unbeachtet in einem Ordner liegen.

Die gute Nachricht ist, dass Sie mit Aspose OCR **ein Bild in PDF konvertieren**, den versteckten Text extrahieren und ein vollständig durchsuchbares Dokument erhalten können – und das in nur wenigen Zeilen C#. In diesem Leitfaden zeigen wir Ihnen außerdem, wie Sie **PNG in PDF konvertieren**, **Text aus Bild extrahieren** und sogar den Sonderfall von mehrseitigen TIFFs behandeln. Am Ende haben Sie eine eigenständige Lösung, die Sie in jedes .NET‑Projekt einbinden können.

## Was Sie benötigen

- **.NET 6+** (der Code funktioniert auch mit .NET Framework 4.6+)
- **Visual Studio 2022** oder eine IDE Ihrer Wahl
- **Aspose.OCR** NuGet‑Paket (es zieht Aspose.PDF automatisch mit)
- Eine Bilddatei (PNG, JPEG, BMP, TIFF), die Sie in ein durchsuchbares PDF umwandeln möchten

Keine zusätzlichen Lizenztricks, keine externen Dienste – nur ein einzelner NuGet‑Verweis und ein paar Minuten Programmierzeit.

## Schritt 1: Das Aspose.OCR NuGet‑Paket installieren

Zuerst fügen Sie die Bibliothek Ihrem Projekt hinzu. Öffnen Sie die Package Manager Console und führen Sie aus:

```powershell
Install-Package Aspose.OCR
```

Dieser einzelne Befehl lädt sowohl **Aspose.OCR** als auch die davon abhängige **Aspose.Pdf**‑Assembly, sodass Sie sowohl das Bild lesen als auch das PDF schreiben können.

> **Pro‑Tipp:** Wenn Sie die .NET‑CLI verwenden, lautet das Äquivalent `dotnet add package Aspose.OCR`.

## Schritt 2: Die OCR‑Engine initialisieren

Eine Instanz von `OcrEngine` zu erstellen ist das Tor zu allen OCR‑Aufgaben. Denken Sie daran als das Gehirn, das Ihr Bild betrachtet und die Zeichen „liest“.

```csharp
using Aspose.OCR;
using Aspose.Pdf;   // pulled in by the OCR package

// Create an OCR engine instance – this object holds configuration and state
var ocrEngine = new OcrEngine();
```

Sie fragen sich vielleicht, *warum nicht einfach eine statische Methode aufrufen?* Der objektorientierte Ansatz ermöglicht es Ihnen, später Einstellungen (Sprache, Auflösung usw.) zu ändern, ohne den gesamten Ablauf zu verändern.

## Schritt 3: Das Bild laden, das Sie konvertieren möchten

Hier **konvertieren wir das Bild in ein PDF** im Geiste – indem wir das Bitmap in die OCR‑Engine einspeisen. Ersetzen Sie `"YOUR_DIRECTORY/input.png"` durch den tatsächlichen Pfad zu Ihrer Datei.

```csharp
// Load the source image (PNG, JPEG, BMP, or multi‑page TIFF)
ocrEngine.SetImage("YOUR_DIRECTORY/input.png");
```

Wenn Sie ein **PNG‑zu‑PDF‑Szenario** haben, verweisen Sie einfach auf die PNG‑Datei. Bei mehrseitigen TIFFs behandelt Aspose.OCR jedes Frame automatisch als separate Seite.

## Schritt 4: OCR ausführen und optional den Text holen

`Recognize()` übernimmt die schwere Arbeit: Es analysiert das Bild, erkennt Zeichen und liefert ein strukturiertes Ergebnis. Sie können den Text für Protokollierung, Suchindizierung oder Anzeige behalten.

```csharp
// Perform OCR – this extracts the textual content from the image
var ocrResult = ocrEngine.Recognize();

// Optional: show the extracted text in the console
Console.WriteLine("Extracted text:");
Console.WriteLine(ocrResult.Text);
```

> **Warum Text extrahieren?** Auch wenn wir ihn im finalen PDF einbetten, kann die rohe Zeichenkette für Validierung oder Analysen nützlich sein.

## Schritt 5: PDF‑Optionen für ein durchsuchbares Dokument konfigurieren

Aspose.PDF stellt uns einen speziellen `PdfSaveOptions`‑Modus namens **CreateSearchablePdf** zur Verfügung. Er weist die Bibliothek an, den OCR‑Text als unsichtbare Ebene hinter dem Bild einzubetten, wodurch das PDF durchsuchbar wird.

```csharp
// Prepare PDF save options – this tells Aspose to embed OCR text
var pdfOptions = PdfSaveOptions.CreateSearchablePdf();
```

Falls Sie jemals ein reines Bild‑PDF (ohne versteckten Text) benötigen, könnten Sie stattdessen zu `PdfSaveOptions.CreatePdf()` wechseln. Für unser Ziel – **durchsuchbares PDF erstellen** – ist jedoch der durchsuchbare Modus das Highlight.

## Schritt 6: Das durchsuchbare PDF auf Festplatte speichern

Jetzt fügen wir alles zusammen. Die Methode `SavePdf` schreibt Bild und versteckten Text in eine einzige Datei.

```csharp
// Save the searchable PDF file
ocrEngine.SavePdf("YOUR_DIRECTORY/output.pdf", pdfOptions);

Console.WriteLine("Searchable PDF created successfully.");
```

An diesem Punkt besitzen Sie ein **durchsuchbares PDF**, das Sie in Adobe Reader öffnen, ein Wort in das Suchfeld eingeben und sofort zur passenden Stelle springen können – obwohl die sichtbare Seite immer noch das ursprüngliche Bild ist.

## Vollständiges funktionierendes Beispiel

Alle Bausteine zusammengefügt, hier eine sofort ausführbare Konsolen‑App. Kopieren Sie den Code in ein neues C#‑Projekt, passen Sie die Dateipfade an und drücken Sie **F5**.

```csharp
using System;
using Aspose.OCR;
using Aspose.Pdf; // included automatically with Aspose.OCR

class Program
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // Step 2: Load the image that contains the scanned document
        // Replace with your actual image path
        ocrEngine.SetImage("YOUR_DIRECTORY/input.png");

        // Step 3: Run the OCR process to extract text (optional but useful)
        var ocrResult = ocrEngine.Recognize();

        // Show extracted text – helpful for debugging
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
        Console.WriteLine("======================");

        // Step 4: Prepare to export the recognized content as a searchable PDF
        var pdfOptions = PdfSaveOptions.CreateSearchablePdf();

        // Step 5: Save the searchable PDF to disk
        // Replace with your desired output path
        ocrEngine.SavePdf("YOUR_DIRECTORY/output.pdf", pdfOptions);

        // Step 6: Inform the user that the PDF has been created
        Console.WriteLine("Searchable PDF created successfully.");
    }
}
```

### Erwartete Ausgabe

Wenn Sie das Programm starten, zeigt die Konsole etwa Folgendes an:

```
=== Extracted Text ===
Invoice #12345
Date: 2024‑04‑30
Total: $1,250.00
...
======================
Searchable PDF created successfully.
```

Und in `YOUR_DIRECTORY` finden Sie `output.pdf`. Öffnen Sie die Datei, drücken Sie **Strg F**, geben Sie „Invoice“ ein und Sie springen direkt zum Wort – obwohl die Seite wie ein flacher Scan aussieht.

## Häufige Variationen behandeln

### Mehrere Bilder auf einmal konvertieren

Wenn Sie einen Ordner voller PNGs haben und ein einzelnes durchsuchbares PDF wollen, iterieren Sie über die Dateien und fügen jede als separate Seite hinzu:

```csharp
var allImages = Directory.GetFiles("YOUR_DIRECTORY", "*.png");
var ocrEngine = new OcrEngine();
var pdfOptions = PdfSaveOptions.CreateSearchablePdf();

foreach (var imgPath in allImages)
{
    ocrEngine.SetImage(imgPath);
    ocrEngine.Recognize(); // extracts text for the current page
    ocrEngine.SavePdf("temp_page.pdf", pdfOptions);

    // Merge temp_page.pdf into the final document (omitted for brevity)
}
```

Sie können außerdem `PdfFileEditor` aus Aspose.PDF verwenden, um die temporären PDFs zu einer finalen Datei zusammenzuführen.

### Umgang mit niedrig aufgelösten Scans

Die OCR‑Genauigkeit sinkt, wenn die Bild‑DPI unter 150 liegt. Vor dem Einspeisen des Bildes können Sie es hochskalieren:

```csharp
ocrEngine.ImageProcessingOptions.Dpi = 300; // forces 300 DPI for better recognition
```

### Auswahl einer bestimmten Sprache

Wenn Ihr Dokument nicht Englisch ist, setzen Sie die Sprache vor `Recognize()`:

```csharp
ocrEngine.Language = Language.Spanish; // or Language.French, etc.
```

Diese Anpassungen stellen sicher, dass **Text aus Bild extrahieren** zuverlässig in verschiedenen Szenarien funktioniert.

## Visuelles Ergebnis

![Searchable PDF created with Aspose OCR – create searchable PDF](https://example.com/images/searchable-pdf.png)

*Der obige Screenshot zeigt ein PDF, bei dem das Bild sichtbar ist, die Textebene jedoch durchsucht werden kann.*

## Fazit

Sie haben nun ein komplettes, produktionsreifes Rezept, um **durchsuchbare PDFs** aus beliebigen Bildern mit Aspose OCR und C# zu erstellen. Wir haben gezeigt, wie man **ein Bild in PDF konvertiert**, **Text aus Bild extrahiert** und sogar die Sonderfälle **PNG in PDF konvertieren** und **OCR‑Bild zu PDF** behandelt. Der Code ist vollständig eigenständig, läuft auf jeder .NET‑Runtime und lässt sich leicht für Batch‑Verarbeitung oder benutzerdefinierte Sprachunterstützung erweitern.

Was kommt als Nächstes? Versuchen Sie, ein Wasserzeichen hinzuzufügen, das PDF zu verschlüsseln oder den extrahierten Text in einen Suchindex wie Elasticsearch zu speisen. Die Möglichkeiten sind endlos, und das gleiche Muster – laden → erkennen → speichern – wird Ihnen bei jedem OCR‑basierten Workflow gute Dienste leisten.

Wenn Sie auf Probleme stoßen oder einen interessanten Anwendungsfall teilen möchten, hinterlassen Sie unten einen Kommentar. Viel Spaß beim Coden und beim Verwandeln dieser hartnäckigen Scans in durchsuchbares Gold!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}