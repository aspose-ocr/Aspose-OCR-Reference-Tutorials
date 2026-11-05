---
category: general
date: 2026-04-01
description: Wie man OCR‑Ausgabe in JSON und XML in C# konvertiert – lerne, Text aus
  einem Bild zu extrahieren und eine JSON‑Datei in C# mit Aspose.OCR zu schreiben.
draft: false
keywords:
- how to convert ocr
- extract text from image
- write json file c#
- write xml file c#
- how to extract text
language: de
og_description: Wie man OCR‑Ergebnisse mit C# in strukturierte JSON‑ und XML‑Dateien
  konvertiert. Schritt‑für‑Schritt‑Anleitung zum Extrahieren von Text aus einem Bild
  und zum Schreiben einer JSON‑Datei in C#.
og_title: Wie man OCR in JSON & XML in C# konvertiert – JSON-Datei schreiben
tags:
- OCR
- C#
- Aspose
title: Wie man OCR in JSON und XML in C# konvertiert – JSON-Datei schreiben
url: /de/net/text-recognition/how-to-convert-ocr-to-json-xml-in-c-write-json-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Convert OCR to JSON & XML in C# – Write JSON File

**Wie man OCR‑Ergebnisse** in etwas umwandelt, das man tatsächlich nutzen kann, ist eine Frage, die sich viele Entwickler stellen. In diesem Leitfaden zeigen wir Ihnen, wie Sie Text aus einem Bild extrahieren, die OCR‑Ausgabe in schön formatiertes JSON und XML umwandeln und diese Dateien anschließend mit C# auf die Festplatte schreiben.

Wenn Sie jemals auf einen rohen OCR‑String gestarrt haben und gedacht haben: „Da muss es doch einen besseren Weg geben, das zu speichern“, dann sind Sie hier genau richtig. Am Ende haben Sie ein vollständiges, ausführbares Programm, das nicht nur **Text aus Bilddateien extrahiert**, sondern auch weiß, **wie man JSON‑Datei in C# schreibt** und **wie man XML‑Datei in C# schreibt**, ohne ins Schwitzen zu geraten.

## What You’ll Need

- **.NET 6.0** oder neuer (der Code funktioniert auch mit .NET Framework 4.6+).  
- **Aspose.OCR** NuGet‑Paket – installieren Sie es mit `dotnet add package Aspose.OCR`.  
- Ein Bild, das Text enthält (z. B. `invoice.png`).  
- Eine IDE Ihrer Wahl – Visual Studio, Rider oder VS Code reichen aus.

> **Pro‑Tipp:** Legen Sie Ihre Bilddateien in einem eigenen Ordner ab (z. B. `Resources/`), damit die Pfade übersichtlich bleiben.

## Step 1: Set Up the OCR Engine – How to Convert OCR

Zuerst erstellen wir eine `OcrEngine`‑Instanz und geben ihr an, welche Sprache sie erkennen soll. In den meisten Fällen reicht Englisch aus, aber Sie können `Language.English` durch jede unterstützte Sprache ersetzen.

```csharp
using Aspose.OCR;
using System.IO;

class JsonXmlOcrDemo
{
    static void Main()
    {
        // Step 1: Initialise the OCR engine for English text
        var ocrEngine = new OcrEngine { Language = Language.English };
```

> **Why this matters:** Das Initialisieren der Engine mit der richtigen Sprache verbessert die Genauigkeit erheblich, besonders bei nicht‑lateinischen Schriften.

## Step 2: Recognise Text – Extract Text from Image

Jetzt übergeben wir das Bild an die Engine. Die Methode `Recognize` liefert ein `OcrResult`‑Objekt, das den Rohtext sowie Positionsdaten enthält.

```csharp
        // Step 2: Recognise text from the supplied image
        // Replace "YOUR_DIRECTORY/invoice.png" with your actual file path
        var ocrResult = ocrEngine.Recognize("YOUR_DIRECTORY/invoice.png");
```

Wenn das Bild nicht gefunden wird, wirft `Recognize` eine `FileNotFoundException`. Um das Beispiel einfach zu halten, gehen wir davon aus, dass der Pfad korrekt ist; in einer Produktionsumgebung sollten Sie das in einen try‑catch‑Block einbetten.

## Step 3: Convert the Result to JSON – Write JSON File C#

Aspose.OCR macht die Serialisierung zum Kinderspiel. Die Methode `ToJson` akzeptiert ein `indent`‑Flag, um hübsch formatierten Output zu erzeugen – ideal, wenn Sie die Datei in einem Texteditor öffnen wollen.

```csharp
        // Step 3: Convert OCR result to formatted JSON
        string jsonOutput = ocrResult.ToJson(indent: true);
```

### Expected JSON Sample

```json
{
  "Text": "Invoice #12345\nDate: 2024‑03‑31\nTotal: $250.00",
  "Regions": [
    {
      "Bounds": { "X": 10, "Y": 20, "Width": 200, "Height": 30 },
      "Text": "Invoice #12345"
    }
    // … more regions …
  ]
}
```

> **How to extract text**: Die Eigenschaft `Text` liefert Ihnen den reinen String, den Sie an andere Services weitergeben können (Suchindizes, Datenbanken usw.).

## Step 4: Persist the JSON – Write JSON File C# (Continued)

Mit dem fertigen JSON‑String schreiben wir ihn einfach mit `File.WriteAllText` in eine Datei. Dadurch wird standardmäßig UTF‑8 verwendet.

```csharp
        // Step 4: Save JSON to disk
        File.WriteAllText("YOUR_DIRECTORY/invoice.json", jsonOutput);
```

Jetzt liegt eine `invoice.json` neben Ihrem Bild und ist bereit für die Weiterverarbeitung.

## Step 5: Convert the Result to XML – Write XML File C#

Falls Sie XML für Altsysteme bevorzugen, übernimmt die Methode `ToXml` die schwere Arbeit. Wie `ToJson` unterstützt sie ebenfalls das pretty‑Printing.

```csharp
        // Step 5: Convert OCR result to formatted XML
        string xmlOutput = ocrResult.ToXml(indent: true);
```

### Expected XML Sample

```xml
<OcrResult>
  <Text>Invoice #12345
Date: 2024-03-31
Total: $250.00</Text>
  <Regions>
    <Region>
      <Bounds X="10" Y="20" Width="200" Height="30" />
      <Text>Invoice #12345</Text>
    </Region>
    <!-- … more regions … -->
  </Regions>
</OcrResult>
```

## Step 6: Persist the XML – Write XML File C# (Continued)

Das Speichern des XML ist identisch zum JSON‑Schritt; Sie geben lediglich die Endung `.xml` an.

```csharp
        // Step 6: Save XML to disk
        File.WriteAllText("YOUR_DIRECTORY/invoice.xml", xmlOutput);
    }
}
```

### Full Working Example

Alles zusammengefügt, hier das komplette Programm, das Sie in eine Konsolen‑App kopieren können:

```csharp
using Aspose.OCR;
using System.IO;

class JsonXmlOcrDemo
{
    static void Main()
    {
        // Initialise OCR engine for English
        var ocrEngine = new OcrEngine { Language = Language.English };

        // Recognise text from image
        var ocrResult = ocrEngine.Recognize("YOUR_DIRECTORY/invoice.png");

        // Convert to JSON and save
        string jsonOutput = ocrResult.ToJson(indent: true);
        File.WriteAllText("YOUR_DIRECTORY/invoice.json", jsonOutput);

        // Convert to XML and save
        string xmlOutput = ocrResult.ToXml(indent: true);
        File.WriteAllText("YOUR_DIRECTORY/invoice.xml", xmlOutput);
    }
}
```

Führen Sie das Programm aus, und Sie finden zwei neue Dateien — `invoice.json` und `invoice.xml` — genau dort, wo Sie sie angegeben haben. Öffnen Sie sie, um zu prüfen, ob die Struktur den obigen Beispielen entspricht.

## Common Questions & Edge Cases

| Question | Answer |
|----------|--------|
| **What if the image contains multiple languages?** | Erstellen Sie separate `OcrEngine`‑Instanzen für jede Sprache oder verwenden Sie `Language.Multi`, falls unterstützt. |
| **Can I control the output format (e.g., exclude region data)?** | Ja. Sowohl `ToJson` als auch `ToXml` akzeptieren optionale Parameter zum Filtern von Feldern; siehe die Aspose.OCR‑Dokumentation zu `ExportOptions`. |
| **How do I handle large PDFs with many pages?** | Verarbeiten Sie jede Seite einzeln, aggregieren Sie die Ergebnisse und serialisieren Sie anschließend einmal. |
| **Is the output UTF‑8 safe?** | Absolut — Aspose.OCR arbeitet intern mit Unicode, und `File.WriteAllText` schreibt standardmäßig UTF‑8. |
| **What about performance?** | OCR ist CPU‑intensiv. Für Batch‑Jobs sollten Sie Parallelisierung über mehrere Kerne in Betracht ziehen oder die Cloud‑API von Aspose nutzen. |

## Conclusion

Sie wissen jetzt **wie man OCR‑Ergebnisse** in sowohl JSON als auch XML mit C# umwandelt. Indem Sie die obigen Schritte befolgen, können Sie **Text aus Bild** extrahieren und dann **JSON‑Datei in C# schreiben** sowie **XML‑Datei in C# schreiben** mit nur wenigen Zeilen Code. Dieser Ansatz ist schnell, zuverlässig und funktioniert mit jedem Bildtyp, den Aspose.OCR unterstützt.

Bereit für die nächste Herausforderung? Versuchen Sie, die

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}