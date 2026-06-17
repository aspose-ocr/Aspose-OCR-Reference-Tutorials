---
category: general
date: 2026-06-06
description: Erfahren Sie, wie Sie ein durchsuchbares PDF erstellen und ein Bild mit
  OCR in ein PDF konvertieren. Enthält das Hinzufügen von Ebenen, Kompressionseinstellungen
  und den vollständigen C#‑Code.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- how to ocr image
- how to add layer
- how to set compression
language: de
og_description: Erstellen Sie ein durchsuchbares PDF aus einem Bild mithilfe von OCR.
  Diese Anleitung zeigt, wie man eine versteckte Textebene hinzufügt, die Kompression
  einstellt und das Bild in ein PDF konvertiert.
og_title: Erstelle durchsuchbare PDF – Komplettes C#‑Tutorial
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Learn how to create searchable PDF and convert image to PDF with OCR.
    Includes layer addition, compression settings, and full C# code.
  headline: Create Searchable PDF from an Image – Full Step‑by‑Step Guide
  type: TechArticle
- description: Learn how to create searchable PDF and convert image to PDF with OCR.
    Includes layer addition, compression settings, and full C# code.
  name: Create Searchable PDF from an Image – Full Step‑by‑Step Guide
  steps:
  - name: Prerequisites
    text: '- .NET 6.0 or later (the code also works on .NET Framework 4.7+). - The
      Aspose.OCR and Aspose.Pdf NuGet packages (or any equivalent library that offers
      `OcrEngine` and `PdfSaveOptions`). - A sample image, e.g., `invoice.png`, placed
      in a folder you can reference. - A basic understanding of C# syntax'
  - name: Full Working Example
    text: 'Putting it all together, here’s the complete, ready‑to‑run program:'
  - name: Pro tip
    text: If you need to **convert image to PDF** without OCR (just a plain image
      PDF), set `AddTextLayer = false`. The same `PdfSaveOptions` still lets you control
      compression, which is handy for archiving scanned documents that don’t need
      searchability.
  type: HowTo
tags:
- OCR
- PDF
- C#
- Aspose
title: Erstelle ein durchsuchbares PDF aus einem Bild – Vollständige Schritt‑für‑Schritt‑Anleitung
url: /de/net/ocr-configuration/create-searchable-pdf-from-an-image-full-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Durchsuchbare PDF erstellen – Komplettes C#‑Tutorial

Haben Sie sich jemals gefragt, wie man **durchsuchbare PDFs** aus einer gescannten Rechnung erstellt, ohne Stunden in einem GUI‑Tool zu verbringen? Sie sind nicht allein. Viele Entwickler stoßen an ihre Grenzen, wenn sie ein Bild in ein PDF umwandeln müssen, das sowohl wie das Original aussieht als auch das Kopieren oder Suchen von Text ermöglicht.  

In diesem Tutorial gehen wir die genauen Schritte durch, um **Bild in PDF zu konvertieren**, OCR darauf anzuwenden, eine versteckte Textebene hinzuzufügen und sogar die Kompressionseinstellungen anzupassen. Am Ende haben Sie ein einsatzbereites C#‑Snippet, das Sie in jedes .NET‑Projekt einbinden können.

## Was Sie lernen werden

- Richten Sie eine OCR‑Engine ein und verstehen Sie **how to OCR image** Dateien.
- Verwenden Sie die **how to add layer**‑Optionen, um eine durchsuchbare Textebene einzubetten.
- Wenden Sie **how to set compression** an, um kleinere, zip‑komprimierte PDFs zu erhalten.
- Verwandeln Sie ein einfaches Bild in einen **create searchable pdf**‑Workflow, den Sie automatisieren können.
- Häufige Stolperfallen und Profi‑Tipps, um Ihre PDFs klar und schnell zu halten.

### Voraussetzungen

- .NET 6.0 oder höher (der Code funktioniert auch mit .NET Framework 4.7+).
- Die NuGet‑Pakete Aspose.OCR und Aspose.Pdf (oder jede gleichwertige Bibliothek, die `OcrEngine` und `PdfSaveOptions` bereitstellt).
- Ein Beispielbild, z. B. `invoice.png`, in einem Ordner, den Sie referenzieren können.
- Ein grundlegendes Verständnis der C#‑Syntax – tiefgehende OCR‑Kenntnisse sind nicht erforderlich.

> **Pro‑Tipp:** Wenn Sie Visual Studio verwenden, installieren Sie die Pakete über die Package Manager Console:  
> `Install-Package Aspose.OCR`  
> `Install-Package Aspose.Pdf`

---

![Beispiel für durchsuchbare PDF, das ein Rechnungsbild in ein PDF mit versteckter Textebene umwandelt](/images/create-searchable-pdf.png)

## Schritt 1: OCR‑Engine initialisieren – **how to ocr image**

Zuerst benötigen wir eine OCR‑Engine, die englischen Text aus unserem Bild lesen kann. Die Klasse `OcrEngine` ist der Einstiegspunkt; Sie setzen einfach die Sprache und übergeben ihr später ein Bild.

```csharp
using Aspose.OCR;
using Aspose.Pdf;

// Create and configure the OCR engine
OcrEngine engine = new OcrEngine
{
    Language = OcrLanguage.English
};
```

*Warum das wichtig ist:* Die Initialisierung der Engine mit der richtigen Sprache verbessert die Genauigkeit erheblich. Wenn Sie das überspringen, erhalten Sie möglicherweise fehlerhafte Zeichen.

## Schritt 2: Bild laden – **convert image to pdf**

Jetzt zeigen wir die Engine auf die Datei, die wir verarbeiten wollen. `ImageStream.FromFile` liest die Bytes und bereitet sie für die OCR vor.

```csharp
// Load the image you want to turn into a searchable PDF
engine.Image = ImageStream.FromFile(@"C:\Docs\invoice.png");
```

Sie können auch aus einem `MemoryStream` laden, wenn das Bild aus einer Web‑Anfrage oder Datenbank stammt.

## Schritt 3: OCR‑Erkennung ausführen – **how to ocr image**

Mit dem geladenen Bild erfolgt die eigentliche Arbeit in einem einzigen Aufruf. Die Methode `Recognize` gibt ein `OcrResult` zurück, das sowohl den extrahierten Text als auch das ursprüngliche Bitmap enthält.

```csharp
// Perform OCR on the loaded image
OcrResult ocrResult = engine.Recognize();
```

*Im Hintergrund:* Die Engine analysiert jedes Pixel, erkennt Zeichen und erstellt einen Unicode‑String. Sie speichert außerdem die Positionsdaten, die später für die versteckte Textebene benötigt werden.

## Schritt 4: PDF‑Speicheroptionen konfigurieren – **how to add layer** & **how to set compression**

Hier geschieht die Magie einer durchsuchbaren PDF. Wir erstellen ein `PdfSaveOptions`‑Objekt, das Aspose.Pdf mitteilt, wie das Originalbild eingebettet, eine versteckte Textebene hinzugefügt und die endgültige Datei komprimiert werden soll.

```csharp
// Set up PDF options for a searchable PDF
PdfSaveOptions pdfOptions = new PdfSaveOptions
{
    IncludeImage = true,          // Keep the original image in the PDF
    AddTextLayer = true,          // Add a hidden text layer with OCR results
    Compression = PdfCompression.Zip   // Use ZIP compression for smaller size
};
```

- **IncludeImage** stellt die visuelle Treue des Originalscans sicher.
- **AddTextLayer** erstellt eine unsichtbare Ebene, die Browser und PDF‑Reader für die Suche indexieren können.
- **Compression** reduziert die Dateigröße, ohne die Qualität zu beeinträchtigen; ZIP ist für die meisten Dokumente eine gute Standardeinstellung.

## Schritt 5: Ergebnis speichern – **create searchable pdf**

Abschließend schreiben wir das OCR‑Ergebnis mit den gerade definierten Optionen auf die Festplatte. Die Methode `Save` nimmt den Zielpfad und die Instanz von `PdfSaveOptions` entgegen.

```csharp
// Save the OCR result as a searchable PDF
ocrResult.Save(@"C:\Docs\invoice_searchable.pdf", pdfOptions);
```

Wenn Sie `invoice_searchable.pdf` in Adobe Reader oder einem modernen Viewer öffnen, sehen Sie das Originalbild, können jedoch jetzt den Text auswählen, kopieren und durchsuchen, als wäre es ein natives PDF.

### Vollständiges funktionierendes Beispiel

Alles zusammengefügt, hier das komplette, sofort ausführbare Programm:

```csharp
using System;
using Aspose.OCR;
using Aspose.Pdf;

namespace SearchablePdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize OCR engine
            OcrEngine engine = new OcrEngine
            {
                Language = OcrLanguage.English
            };

            // 2️⃣ Load the source image
            string imagePath = @"C:\Docs\invoice.png";
            engine.Image = ImageStream.FromFile(imagePath);

            // 3️⃣ Perform OCR
            OcrResult result = engine.Recognize();

            // 4️⃣ Configure PDF options (layer + compression)
            PdfSaveOptions pdfOptions = new PdfSaveOptions
            {
                IncludeImage = true,
                AddTextLayer = true,
                Compression = PdfCompression.Zip
            };

            // 5️⃣ Save as searchable PDF
            string pdfPath = @"C:\Docs\invoice_searchable.pdf";
            result.Save(pdfPath, pdfOptions);

            Console.WriteLine($"Searchable PDF created at: {pdfPath}");
        }
    }
}
```

**Erwartete Ausgabe** (in der Konsole):  
`Searchable PDF created at: C:\Docs\invoice_searchable.pdf`

Öffnen Sie die resultierende Datei, drücken Sie **Strg F**, geben Sie ein Wort ein, das Sie auf der Rechnung sehen, und beobachten Sie, wie der Viewer sofort dorthin springt. Das ist das Kernstück von **create searchable pdf** in Aktion.

## Häufige Stolperfallen & wie man sie vermeidet

| Problem | Warum es passiert | Lösung |
|---------|-------------------|--------|
| Text nicht durchsuchbar | `AddTextLayer` auf `false` gesetzt oder eine ältere Aspose‑Version verwendet | Stellen Sie sicher, dass `AddTextLayer = true` ist und aktualisieren Sie auf das neueste NuGet‑Paket |
| PDF sehr groß (Megabytes) | Kompression auf `PdfCompression.None` gesetzt | Wechseln Sie zu `PdfCompression.Zip` oder `PdfCompression.Jpeg` für Bilder |
| Verzerrte Zeichen | Falsche Sprache oder Bild mit niedriger Auflösung | Setzen Sie `engine.Language` korrekt und verwenden Sie mindestens 300 dpi‑Bilder |
| Versteckte Ebene in einigen Viewern unsichtbar | PDF mit einer nicht‑standardmäßigen PDF‑Version erzeugt | Verwenden Sie `PdfSaveOptions.PdfVersion = PdfVersion.PDF_1_7` (Standard) oder aktualisieren Sie den Viewer |

### Pro‑Tipp

Wenn Sie **convert image to PDF** ohne OCR benötigen (nur ein einfaches Bild‑PDF), setzen Sie `AddTextLayer = false`. Die gleichen `PdfSaveOptions` ermöglichen weiterhin die Steuerung der Kompression, was praktisch ist, um gescannte Dokumente zu archivieren, die keine Durchsuchbarkeit benötigen.

## Erweiterung der Lösung

- **Multiple pages**: Durchlaufen Sie eine Liste von Bilddateien, rufen Sie jedes Mal `engine.Image = ...` auf und sammeln Sie die Ergebnisse zu einem einzigen PDF mithilfe der `PdfDocument`‑Aggregation.
- **Different languages**: Ändern Sie `engine.Language = OcrLanguage.Spanish` (oder eine andere unterstützte Sprache), um mehrsprachige Rechnungen zu verarbeiten.
- **Custom compression**: Für farbreiche Bilder kann `PdfCompression.Jpeg` mit einer Qualitäts‑Einstellung (`pdfOptions.JpegQuality = 80`) die Dateien weiter verkleinern.

## Fazit

Wir haben gerade alles behandelt, was Sie benötigen, um **durchsuchbare PDF**‑Dateien aus Bildern mit C# zu erstellen. Von der Initialisierung der OCR‑Engine, dem Laden des Bildes, der Durchführung der Erkennung, der Konfiguration einer versteckten Textebene bis hin zur Einstellung der Kompression – jedes Element spielt eine entscheidende Rolle, um ein schnelles, durchsuchbares Dokument zu liefern.  

Jetzt können Sie die Rechnungsverarbeitung automatisieren, Verträge archivieren oder ein Bulk‑Scan‑Werkzeug erstellen, das Papierstapel in sofort durchsuchbare PDFs verwandelt.  

Bereit für die nächste Herausforderung? Versuchen Sie, Wasserzeichen hinzuzufügen, mehrere durchsuchbare PDFs zusammenzuführen oder diese Logik über eine Web‑API bereitzustellen, sodass Ihre gesamte Organisation Bilder hochladen und sofort durchsuchbare PDFs erhalten kann.

---

*Wenn Ihnen dieser Leitfaden geholfen hat, geben Sie ihm einen ⭐, teilen Sie ihn mit Teamkollegen oder hinterlassen Sie einen Kommentar mit Ihren eigenen Anpassungen. Viel Spaß beim Coden!*

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Codebeispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, zusätzliche API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Wie man PDF in .NET mit Aspose.OCR OCR‑t](/ocr/english/net/text-recognition/recognize-pdf/)
- [Bilder zu PDF in C# konvertieren – Mehrseitiges OCR‑Ergebnis speichern](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)
- [Wie man Bild OCR‑t – OCR auf Bild in OCR‑Bild­erkennung anwenden](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}