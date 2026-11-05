---
category: general
date: 2026-03-18
description: Extrahieren Sie eine Tabelle aus einem Bild mit Aspose OCR in C#. Erfahren
  Sie, wie Sie die Tabelle in JSON konvertieren, das Tabellen‑JSON erhalten und Text
  aus dem Bild in wenigen Minuten extrahieren.
draft: false
keywords:
- extract table from image
- convert table to json
- convert image to json
- extract text from image
- get table json
language: de
og_description: Tabelle aus Bild mit Aspose OCR in C# extrahieren. Lernen Sie, die
  Tabelle in JSON zu konvertieren, das Tabellen‑JSON zu erhalten und Text schnell
  aus dem Bild zu extrahieren.
og_title: Tabelle aus Bild mit Aspose OCR extrahieren – Vollständiger C#‑Leitfaden
tags:
- Aspose OCR
- C#
- Table Extraction
title: Tabelle aus Bild mit Aspose OCR extrahieren – Vollständiger C#‑Leitfaden
url: /de/net/text-recognition/extract-table-from-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tabelle aus Bild extrahieren – Vollständiger C# Leitfaden

Hatten Sie jemals das Bedürfnis, **extract table from image** zu verwenden, waren sich aber nicht sicher, welche Bibliothek das ohne ein Berg von manuellem Parsen erledigen kann? Sie sind nicht allein. In vielen Rechnung‑Verarbeitungs‑ oder Beleg‑Scanning‑Projekten besteht das eigentliche Problem darin, ein verrauschtes Bitmap in eine strukturierte Tabelle zu verwandeln, die Ihr nachgelagertes System verarbeiten kann.  

Die gute Nachricht? Mit Aspose OCR können Sie **convert table to JSON** in wenigen Zeilen ausführen und erhalten außerdem den reinen Text des gesamten Bildes, sodass **extract text from image** ein Bonus ist. In diesem Tutorial führen wir Sie durch den gesamten Ablauf – vom Laden eines Bildes bis hin zur sauberen JSON‑Darstellung der erkannten Tabelle.

> **Schneller Erfolg:** Am Ende haben Sie eine ausführbare C#‑Konsolenanwendung, die sowohl den rohen OCR‑Text als auch einen JSON‑String ausgibt, den Sie direkt in eine Datenbank oder eine API einspeisen können.

## Voraussetzungen

- .NET 6.0 SDK (oder eine aktuelle .NET‑Version) installiert.  
- Eine gültige Aspose OCR‑Lizenz oder ein kostenloser Test (die Bibliothek funktioniert ohne Lizenz, fügt jedoch ein Wasserzeichen hinzu).  
- Ein Bild, das tatsächlich eine Tabelle enthält – zum Beispiel `invoice_table.png`.  
- Visual Studio 2022, VS Code oder ein beliebiger Editor Ihrer Wahl.

Keine zusätzlichen NuGet‑Pakete über `Aspose.OCR` hinaus werden benötigt.

## Schritt 1: Projekt einrichten und Aspose  OCR installieren

Zuerst erstellen Sie ein neues Konsolenprojekt und binden die OCR‑Bibliothek ein.

```bash
dotnet new console -n TableJsonDemo
cd TableJsonDemo
dotnet add package Aspose.OCR
```

> **Profi‑Tipp:** Wenn Sie einen Unternehmens‑Proxy verwenden, fügen Sie das Flag `--no-restore` hinzu und führen Sie später `dotnet restore` mit den entsprechenden Umgebungsvariablen aus.

## Schritt 2: OCR‑Engine initialisieren und Tabellenerkennung aktivieren

Das Herzstück der Lösung ist die `OcrEngine`. Durch das Umschalten von `EnableTableRecognition` teilen wir Aspose  OCR mit, nach gitterähnlichen Strukturen zu suchen, anstatt alles als reinen Text zu behandeln.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Structure;

class TableJsonDemo
{
    static void Main()
    {
        // Create the OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Enable table detection – this is what lets us get a JSON table later
        ocrEngine.Settings.EnableTableRecognition = true;
```

Warum ist dieser Schritt entscheidend? Ohne Tabellenerkennung würde die Engine das Bild zu einer einzigen Zeichenkette flachlegen, was es unmöglich macht, später Zeilen und Spalten zu rekonstruieren. Das Aktivieren fügt eine leichte Layout‑Analyse‑Phase hinzu, die kaum Performance kostet, aber enorme Vorteile für nachgelagerte Prozesse liefert.

## Schritt 3: Bild laden und Erkennung ausführen

Jetzt zeigen wir der Engine auf die Datei, die die Tabelle enthält. `ImageStream.FromFile` unterstützt die gängigsten Formate (PNG, JPEG, TIFF).

```csharp
        // Load the image that contains the table
        ImageStream image = ImageStream.FromFile("YOUR_DIRECTORY/invoice_table.png");

        // Perform OCR – this returns an OcrResult object with multiple helpers
        OcrResult ocrResult = ocrEngine.Recognize(image);
```

Ist das Bild groß, sollten Sie es zuerst verkleinern, um die Verarbeitung zu beschleunigen. Aspose  OCR erkennt DPI automatisch, aber ein Scan mit 300 DPI ist für die meisten Tabellen ideal.

## Schritt 4: Klartext extrahieren – “extract text from image”

Obwohl unser Hauptziel die Tabelle ist, benötigen Sie häufig den Rohtext für Protokollierung oder Fallback‑Verarbeitung.

```csharp
        // Output the full recognized text
        Console.WriteLine("Full text:");
        Console.WriteLine(ocrResult.Text);
```

Die Eigenschaft `Text` verkettet alles, was die Engine sieht, und bewahrt Zeilenumbrüche. Das ist praktisch, wenn Sie überprüfen müssen, ob die OCR Überschriften oder Fußzeilen außerhalb des Tabellenbereichs korrekt gelesen hat.

## Schritt 5: Erkannten Tabelle als JSON erhalten – “convert table to json” & “get table json”

Hier passiert die Magie. `GetTableAsJson()` serialisiert die erkannten Zeilen, Spalten und Zellinhalte in einen sauberen JSON‑String.

```csharp
        // Retrieve the table structure as a JSON string
        string tableJson = ocrResult.GetTableAsJson();

        Console.WriteLine("\nDetected table (JSON):");
        Console.WriteLine(tableJson);
    }
}
```

Das resultierende JSON sieht etwa so aus (zur besseren Lesbarkeit formatiert):

```json
{
  "Rows": [
    {
      "Cells": [
        { "Text": "Item", "ColumnIndex": 0 },
        { "Text": "Quantity", "ColumnIndex": 1 },
        { "Text": "Price", "ColumnIndex": 2 }
      ]
    },
    {
      "Cells": [
        { "Text": "Widget A", "ColumnIndex": 0 },
        { "Text": "10", "ColumnIndex": 1 },
        { "Text": "$5.00", "ColumnIndex": 2 }
      ]
    },
    {
      "Cells": [
        { "Text": "Widget B", "ColumnIndex": 0 },
        { "Text": "7", "ColumnIndex": 1 },
        { "Text": "$8.50", "ColumnIndex": 2 }
      ]
    }
  ]
}
```

Warum ist JSON das bevorzugte Format? Es ist sprachunabhängig, lässt sich leicht in Objekte deserialisieren und funktioniert hervorragend mit modernen Web‑APIs. Wenn Sie stattdessen ein CSV benötigen, iterieren Sie einfach über die Zeilen und verbinden die Zelltexte mit Kommas.

## Schritt 6: (Optional) JSON in ein .NET‑Objekt konvertieren – “convert image to json”

Wenn Sie lieber mit stark typisierten Objekten arbeiten, deserialisieren Sie das JSON mit `System.Text.Json`.

```csharp
using System.Text.Json;

...

        // Deserialize into a C# class (optional)
        var table = JsonSerializer.Deserialize<TableModel>(tableJson);
        Console.WriteLine("\nFirst cell value: " + table.Rows[0].Cells[0].Text);
```

Sie würden `TableModel`, `RowModel` und `CellModel` definieren, um dem JSON‑Schema zu entsprechen. Dieser Schritt zeigt, wie Sie von **convert image to json** bis hin zu einem typisierten Objekt gelangen, wodurch die nachgelagerte Validierung zum Kinderspiel wird.

## Vollständiges funktionierendes Beispiel

Wenn wir alles zusammenfügen, erhalten Sie das komplette, sofort ausführbare Programm. Speichern Sie es als `Program.cs` im zuvor erstellten Projektordner.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Structure;
using System.Text.Json;

class TableJsonDemo
{
    static void Main()
    {
        // Step 1: Create OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Enable table recognition
        ocrEngine.Settings.EnableTableRecognition = true;

        // Step 3: Load image containing a table
        ImageStream image = ImageStream.FromFile("YOUR_DIRECTORY/invoice_table.png");

        // Step 4: Run OCR
        OcrResult ocrResult = ocrEngine.Recognize(image);

        // Step 5: Print full text (extract text from image)
        Console.WriteLine("Full text:");
        Console.WriteLine(ocrResult.Text);

        // Step 6: Get table as JSON (convert table to json, get table json)
        string tableJson = ocrResult.GetTableAsJson();
        Console.WriteLine("\nDetected table (JSON):");
        Console.WriteLine(tableJson);

        // Optional: Deserialize JSON to C# objects (convert image to json)
        var table = JsonSerializer.Deserialize<TableModel>(tableJson);
        Console.WriteLine("\nFirst cell value: " + table.Rows[0].Cells[0].Text);
    }
}

// Helper classes matching Aspose's JSON structure
public class TableModel
{
    public RowModel[] Rows { get; set; }
}
public class RowModel
{
    public CellModel[] Cells { get; set; }
}
public class CellModel
{
    public string Text { get; set; }
    public int ColumnIndex { get; set; }
}
```

### Erwartete Ausgabe

Wenn Sie `dotnet run` ausführen, sollten Sie etwas Ähnliches sehen:

```
Full text:
Item Quantity Price
Widget A 10 $5.00
Widget B 7 $8.50

Detected table (JSON):
{
  "Rows":[
    {"Cells":[{"Text":"Item","ColumnIndex":0},{"Text":"Quantity","ColumnIndex":1},{"Text":"Price","ColumnIndex":2}]},
    {"Cells":[{"Text":"Widget A","ColumnIndex":0},{"Text":"10","ColumnIndex":1},{"Text":"$5.00","ColumnIndex":2}]},
    {"Cells":[{"Text":"Widget B","ColumnIndex":0},{"Text":"7","ColumnIndex":1},{"Text":"$8.50","ColumnIndex":2}]}
  ]
}

First cell value: Item
```

Wenn die Ausgabe leer erscheint, prüfen Sie, ob `EnableTableRecognition` auf `true` gesetzt ist und das Bild tatsächlich klare Gitterlinien enthält.

## Häufige Fallstricke & wie man sie vermeidet

| Problem | Warum es passiert | Lösung |
|-------|----------------|-----|
| **Kein JSON zurückgegeben** | Tabellenerkennung deaktiviert oder Bild zu kontrastarm. | Stellen Sie sicher, dass `ocrEngine.Settings.EnableTableRecognition = true` und verbessern Sie die Bildqualität (Kontrast erhöhen, binarisieren). |
| **Unvollständige Zeilen** | OCR verwirrt durch zusammengeführte Zellen oder gedrehten Text. | Bild vorverarbeiten: Entzerren (`ImageProcessor.Rotate`) oder zusammengeführte Zellen manuell aufteilen. |
| **Unicode‑Kauderwelsch** | Schriftart nicht erkannt (z. B. handschriftlich). | Sprachpakete wechseln via `ocrEngine.Language = Language.English;` oder eine andere OCR‑Engine für Handschrift verwenden. |
| **Leistungsabfall** | Sehr großes Bild (>5 MP). | Auf etwa 1500 px Breite herunter skalieren, DPI beibehalten. |

## Nächste Schritte: Über die Grundlagen hinaus

Jetzt, da Sie **extract table from image** und **convert table to JSON** können, denken Sie an diese Erweiterungen:

- **JSON persistieren** in einer Datenbank mit Entity Framework.  
- **JSON nachbearbeiten**, um Währungsformate zu normalisieren (z. B. `$` entfernen).  
- **Stapelverarbeitung** eines Ordners mit Rechnungen mittels `Directory.GetFiles` und Parallelisierung mit `Parallel.ForEach`.  
- **Integration** mit Azure Functions oder AWS Lambda für serverlose OCR‑Pipelines.

Jedes dieser Themen bringt natürlich die anderen sekundären Schlüsselwörter wie **convert image to json** (wenn Sie das gesamte OCR‑Ergebnis an einen Cloud‑Endpunkt senden) und **get table json** für nachgelagerte Analysen ein.

---

### Fazit

Wir haben Ihnen gerade gezeigt, wie Sie mit Aspose  OCR **extract table from image** durchführen, diese Tabelle in sauberes JSON umwandeln und sogar in C#‑Objekte deserialisieren. Das gleiche Muster

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}