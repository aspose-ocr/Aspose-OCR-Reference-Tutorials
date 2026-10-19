---
category: general
date: 2026-03-28
description: Erfahren Sie, wie Sie Tabellen aus Bildern mit Aspose OCR in C# extrahieren.
  Dieser Leitfaden behandelt, wie man Tabellen im Bild erkennt, das Bild für OCR lädt
  und Tabellen aus PNG‑Dateien extrahiert.
draft: false
keywords:
- how to extract tables
- extract table from image
- detect tables in image
- load image for ocr
- extract tables from png
language: de
og_description: Schritt‑für‑Schritt‑Anleitung, wie man Tabellen aus Bildern mit Aspose
  OCR in C# extrahiert. Enthält Code, Erklärungen und Tipps zur Erkennung von Tabellen
  in Bilddateien.
og_title: Wie man Tabellen aus Bildern mit Aspose OCR (C#) extrahiert
tags:
- Aspose OCR
- C#
- Table Extraction
title: Wie man Tabellen aus Bildern mit Aspose OCR (C#) extrahiert
url: /de/net/image-and-drawing-recognition/how-to-extract-tables-from-images-using-aspose-ocr-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man Tabellen aus Bildern mit Aspose OCR (C#) extrahiert

Haben Sie sich jemals gefragt, **wie man Tabellen** aus einer gescannten Rechnung oder einem Screenshot einer Kalkulationstabelle extrahiert? Sie sind nicht allein. In vielen real‑world Projekten müssen wir ein Bild einer Tabelle in etwas umwandeln, das wir abfragen können – meist eine CSV oder ein DataTable. Die gute Nachricht? Aspose OCR macht das kinderleicht, und Sie können es mit nur wenigen Zeilen C# erledigen.

In diesem Tutorial führen wir Sie durch den gesamten Prozess: von **load image for OCR**, über **detect tables in image** bis hin zu **extract table from image**, und speichern das Ergebnis als CSV‑Datei. Am Ende haben Sie eine sofort einsatzbereite Konsolen‑App, die **extract tables from PNG**‑Dateien (oder jede unterstützte Bitmap) ohne Aufwand extrahieren kann.

## Voraussetzungen

- .NET 6.0 SDK oder neuer (der Code funktioniert auch mit .NET Framework)
- Visual Studio 2022 (oder jede IDE Ihrer Wahl)
- Eine Aspose.OCR für .NET Lizenzdatei (Sie können mit einer kostenlosen Testversion beginnen)
- Ein Beispielbild, das eine Tabelle enthält (z. B. `invoice_table.png`)

Falls Ihnen etwas davon unbekannt ist, keine Sorge – installieren Sie einfach das .NET SDK, holen Sie das NuGet‑Paket, und Sie können loslegen.

## Überblick über die Lösung

Auf hoher Ebene sieht der Workflow so aus:

1. **Load the image** die Sie verarbeiten möchten.
2. **Run OCR recognition**, damit die Engine weiß, wo sich der Text befindet.
3. **Create a TableExtractor**, der die OCR‑Ergebnisse nach rasterähnlichen Strukturen durchsucht.
4. **Extract all detected tables** und wählen Sie die gewünschte aus.
5. **Save the table** als CSV (oder ein anderes gewünschtes Format).

Jeder Schritt wird im Folgenden ausführlich erklärt, mit vollständigen Code‑Snippets, die Sie kopieren‑und‑einfügen können.

<img src="table_extraction_example.png" alt="Beispiel zum Extrahieren von Tabellen aus einem Bild" width="600">

*(Das obige Bild zeigt eine Beispiel‑Rechnungstabelle, die wir extrahieren werden.)*

## Schritt 1 – Bild für OCR laden

Das Erste, was Sie tun müssen, ist Aspose OCR mitzuteilen, welche Datei gelesen werden soll. Die Bibliothek unterstützt PNG, JPEG, BMP, TIFF und einige weitere Formate. Hier ist der minimale Code:

```csharp
using Aspose.OCR;
using System.Drawing;   // Required for Image.FromFile

// ...

// Load the image that contains the table
var ocrEngine = new OcrEngine
{
    Image = Image.FromFile(@"C:\Images\invoice_table.png") // <-- adjust the path
};
```

**Warum das wichtig ist:**  
`Image.FromFile` übernimmt das schwere Heben beim Dekodieren des PNG (oder einer anderen Bitmap) in ein Format, das die OCR‑Engine verstehen kann. Wenn Sie diesen Schritt überspringen oder eine beschädigte Datei übergeben, wirft der nachfolgende Aufruf `Recognize()` eine Ausnahme.

> **Profi‑Tipp:** Wenn Sie mit großen PDFs arbeiten, extrahieren Sie zuerst jede Seite als Bild – sonst läuft der OCR‑Engine der Speicher aus.

## Schritt 2 – Seite erkennen (erforderlich vor der Tabellenerkennung)

Die Erkennung wandelt die rohen Pixeldaten in ein durchsuchbares Textlayout um. Ohne diesen Schritt hat der `TableExtractor` nichts, womit er arbeiten kann.

```csharp
// Perform OCR recognition – this populates internal structures
ocrEngine.Recognize();
```

**Was im Hintergrund passiert:**  
Aspose OCR führt einen neuronalen‑Netz‑basierten Textdetektor aus und erstellt anschließend eine Hierarchie von `Page`, `Paragraph` und `Word` Objekten. Der Tabellendetektor untersucht später die räumlichen Beziehungen zwischen diesen Wörtern.

Wenn Sie viele Bilder in einer Schleife verarbeiten, sollten Sie dieselbe `OcrEngine`‑Instanz wiederverwenden und nur die `Image`‑Eigenschaft austauschen – das reduziert den Speicher‑Overhead.

## Schritt 3 – TableExtractor erstellen und Tabellen im Bild erkennen

Jetzt, da die OCR‑Daten vorhanden sind, können wir Aspose bitten, Tabellen zu finden. Die Klasse `TableExtractor` erledigt genau das.

```csharp
using Aspose.OCR.Table;

// ...

// Initialize the TableExtractor with the recognized engine
var tableExtractor = new TableExtractor(ocrEngine);

// Extract all tables detected on the page
List<Table> extractedTables = tableExtractor.ExtractAll();
```

**Warum `ExtractAll()` verwenden?**  
Ein einzelnes Bild kann mehrere Tabellen enthalten (denken Sie an einen mehrteiligen Bericht). `ExtractAll()` gibt eine `List<Table>` zurück, sodass Sie iterieren, die richtige auswählen oder sie später sogar zusammenführen können.

Wenn Sie nur die erste Tabelle benötigen, können Sie sicher `extractedTables[0]` verwenden, aber achten Sie immer darauf, eine leere Liste zu prüfen, um `IndexOutOfRangeException` zu vermeiden.

```csharp
if (extractedTables.Count == 0)
{
    Console.WriteLine("No tables were detected. Check the image quality or try adjusting OCR settings.");
    return;
}
```

## Schritt 4 – Extrahierte Tabelle als CSV speichern (oder ein anderes Format)

Aspose macht das Exportieren trivial. Die Klasse `Table` verfügt über integrierte Methoden `SaveCsv`, `SaveXls` und `SaveJson`. So schreiben Sie eine CSV‑Datei:

```csharp
// Save the first detected table to CSV
string outputPath = @"C:\Output\invoice_table.csv";
extractedTables[0].SaveCsv(outputPath);

Console.WriteLine($"Table extraction completed. CSV saved to {outputPath}");
```

**Wie sieht die CSV aus?**  
Angenommen, das Quellbild enthielt ein 4 × 3‑Raster, dann könnte die CSV wie folgt aussehen:

```
Item,Quantity,Price
Widget A,2,19.99
Widget B,5,9.50
Service C,1,150.00
```

Sie können diese Datei in Excel, Power BI öffnen oder direkt in Ihre Datenpipeline einspeisen.

## Vollständiges End‑zu‑End‑Beispiel

Unten finden Sie das komplette, eigenständige Programm. Kopieren Sie es in ein neues Konsolenprojekt (`dotnet new console`) und führen Sie es aus. Stellen Sie sicher, dass das NuGet‑Paket `Aspose.OCR` installiert ist (`dotnet add package Aspose.OCR`).

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;          // For Image
using Aspose.OCR;
using Aspose.OCR.Table;

namespace TableExtractTutorial
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Load the image that contains the table
            // -------------------------------------------------
            var ocrEngine = new OcrEngine
            {
                Image = Image.FromFile(@"C:\Images\invoice_table.png")
            };

            // -------------------------------------------------
            // Step 2: Recognize the page (required before table detection)
            // -------------------------------------------------
            ocrEngine.Recognize();

            // -------------------------------------------------
            // Step 3: Create a TableExtractor and detect tables
            // -------------------------------------------------
            var tableExtractor = new TableExtractor(ocrEngine);
            List<Table> extractedTables = tableExtractor.ExtractAll();

            // Guard against no tables found
            if (extractedTables.Count == 0)
            {
                Console.WriteLine("No tables detected. Verify image quality or OCR settings.");
                return;
            }

            // -------------------------------------------------
            // Step 4: Save the first extracted table as CSV
            // -------------------------------------------------
            string csvPath = @"C:\Output\invoice_table.csv";
            extractedTables[0].SaveCsv(csvPath);

            Console.WriteLine($"Table extraction completed. CSV saved at: {csvPath}");
        }
    }
}
```

### Erwartete Ausgabe

```
Table extraction completed. CSV saved at: C:\Output\invoice_table.csv
```

Öffnen Sie `invoice_table.csv` und Sie werden die Zeilen und Spalten sehen, die das Originalbild spiegeln.

## Häufige Fragen & Sonderfälle

### Was ist, wenn das Bild ein JPEG statt eines PNG ist?

Der gleiche Code funktioniert – ändern Sie einfach die Dateierweiterung in `Image.FromFile`. Aspose OCR erkennt das Format automatisch, daher ist **extract tables from png** keine zwingende Voraussetzung; es funktioniert mit jeder unterstützten Bitmap.

### Meine Tabelle hat zusammengeführte Zellen. Werden sie erhalten bleiben?

Zusammengeführte Zellen werden im CSV‑Ausgabeformat als separate Spalten behandelt, da CSV kein Spannen unterstützt. Wenn Sie ein umfangreicheres Format benötigen (z. B. Excel mit zusammengeführten Zellen), verwenden Sie stattdessen `SaveXls`:

```csharp
extractedTables[0].SaveXls(@"C:\Output\invoice_table.xls");
```

### Die Erkennung hat eine Spalte übersehen. Wie kann ich die Genauigkeit verbessern?

- Erhöhen Sie die Bildauflösung (≥300 dpi ist ideal).
- Bildvorverarbeitung: in Graustufen konvertieren, Kontrast erhöhen oder einen Deskew‑Filter anwenden.
- Passen Sie Aspose OCR‑Einstellungen wie `PageSegMode` oder `Language` an, falls die Tabelle nicht‑lateinische Zeichen enthält.

### Kann ich Tabellen direkt aus einem PDF extrahieren?

Ja. Konvertieren Sie zunächst jede PDF‑Seite in ein Bild (mit `Aspose.PDF` oder einer beliebigen PDF‑zu‑Bild‑Bibliothek) und geben Sie diese Bilder dann in denselben Workflow ein.

## Tipps für produktionsreife Implementierungen

1. **Wrap OCR in a try/catch** – Netzwerk‑lizenzierte Umgebungen können Lizenz‑Ausnahmen werfen.
2. **Dispose of `Image` objects** – wickeln Sie sie in `using`‑Blöcke, um native Ressourcen freizugeben.
3. **Log the confidence scores** – `TableExtractor` stellt `Table.Confidence` bereit, das Sie zur Qualitätsüberwachung speichern können.
4. **Batch processing** – Beim Verarbeiten von Hunderten von Rechnungen sollten Sie die OCR‑Aufrufe parallelisieren, jedoch die Thread‑Safety‑Richtlinien der Lizenz beachten.

## Nächste Schritte

Jetzt, da Sie wissen, **how to extract tables** aus Bildern zu extrahieren, möchten Sie vielleicht Folgendes erkunden:

- **Detect tables in image** Videos (unter Verwendung von Aspose’s `TableExtractor` für jedes Frame).
- **Load image for OCR** von einer Web‑API, um cloud‑basierte Tabellenerkennungs‑Dienste zu ermöglichen.
- **Extract tables from PNG**‑Dateien, die in Azure Blob Storage gespeichert sind, und diese mit Azure Functions für serverlose Verarbeitung zu integrieren.

Fühlen Sie sich frei, mit verschiedenen Dateiformaten zu experimentieren, OCR‑Einstellungen anzupassen oder die CSV‑Ausgabe direkt in eine Datenbank zu leiten. Der Himmel ist die Grenze.

---

*Viel Spaß beim Coden! Wenn Sie auf Probleme stoßen oder Ideen zur Verbesserung haben, hinterlassen Sie unten einen Kommentar. Wir finden gemeinsam eine Lösung.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}