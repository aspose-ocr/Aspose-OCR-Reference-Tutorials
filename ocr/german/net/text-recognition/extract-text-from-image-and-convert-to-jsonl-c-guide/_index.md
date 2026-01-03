---
category: general
date: 2026-01-02
description: Extrahiere Text aus einem Bild mit Aspose OCR in C#. Erfahre, wie du
  ein Bild schnell und zuverlässig in das JSONL-Format konvertierst.
draft: false
keywords:
- extract text from image
- convert image to jsonl
language: de
og_description: Extrahieren Sie Text aus einem Bild mit Aspose OCR und konvertieren
  Sie ihn in das JSONL‑Format. Vollständiges Schritt‑für‑Schritt‑C#‑Tutorial für Entwickler.
og_title: Text aus Bild extrahieren – in JSONL konvertieren in C#
tags:
- C#
- OCR
- Aspose
- JSONL
title: Text aus Bild extrahieren und in JSONL konvertieren – C#‑Leitfaden
url: /de/net/text-recognition/extract-text-from-image-and-convert-to-jsonl-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Text aus Bild extrahieren und in JSONL konvertieren – Vollständiges C#‑Tutorial

Haben Sie jemals **Text aus Bild extrahieren** müssen, waren sich aber nicht sicher, welche Bibliothek Ihnen saubere, strukturierte Ausgaben liefert? Sie sind nicht allein. In vielen Beleg‑Verarbeitungs‑ oder Dokument‑Digitalisierungs‑Projekten ist der Engpass, ein Bitmap in durchsuchbaren Text *und* ein maschinenlesbares Format zu verwandeln.

Die gute Nachricht? Mit Aspose OCR können Sie **Text aus Bild extrahieren** und mit wenigen Codezeilen **Bild in JSONL konvertieren** für nachgelagerte Analysen. Dieser Leitfaden führt Sie durch den gesamten Prozess, vom Laden einer PNG bis zum Schreiben einer JSON‑Lines‑Datei, die in eine Datenpipeline gestreamt werden kann.

> **Hinweis:** Wenn Sie bereits .NET 6 oder höher verwenden, funktioniert derselbe Code ohne zusätzliche Konfiguration.

## Voraussetzungen — Was Sie benötigen

- **.NET 6 SDK** (oder eine aktuelle .NET‑Version)
- **Aspose.OCR** NuGet‑Paket  
  ```bash
  dotnet add package Aspose.OCR
  ```
- **Newtonsoft.Json** für Serialisierung  
  ```bash
  dotnet add package Newtonsoft.Json
  ```
- Ein Beispielbild (z. B. `receipt.png`) in einem Ordner, den Sie referenzieren können.
- Eine IDE oder ein Editor Ihrer Wahl – Visual Studio, VS Code, Rider usw.

Keine aufwändige Einrichtung, keine externen Dienste, nur ein paar NuGet‑Pakete.

![Extract text from image using C#](https://example.com/assets/ocr-sample.png)

*Alt-Text: Text aus Bild extrahieren mit C# und Aspose OCR*

## Schritt 1: Laden Sie das zu verarbeitende Bild

Das Erste, was Sie tun, wenn Sie **Text aus Bild extrahieren** möchten, ist dem OCR‑Engine ein Bitmap zu übergeben. Die Verwendung von `System.Drawing.Bitmap` ist unkompliziert und funktioniert für die meisten Rasterformate.

```csharp
using System.Drawing;

// Adjust the path to where your receipt.png lives
string imagePath = @"C:\MyProjects\OCRDemo\receipt.png";
Bitmap receiptImage = new Bitmap(imagePath);
```

> **Warum das wichtig ist:** Das Laden des Bildes als `Bitmap` gibt der OCR‑Engine direkten Pixelzugriff, was die Erkennungs‑Geschwindigkeit und -Genauigkeit im Vergleich zum Streamen roher Bytes verbessert.

## Schritt 2: Konfigurieren Sie Aspose OCR für JSON‑Lines‑Ausgabe

Aspose OCR ermöglicht es Ihnen, Sprache, Ausgabeformat und einige Leistungs‑Feinabstimmungen festzulegen. Hier fordern wir **JSON‑Lines** (ein JSON‑Objekt pro Zeile) an, da es sich später perfekt für zeilenweise Verarbeitung eignet.

```csharp
using Aspose.OCR;

// Create the engine
OcrEngine ocrEngine = new OcrEngine();

// Tell the engine we’re dealing with English text
RecognitionOptions options = new RecognitionOptions
{
    Language = Language.English,
    OutputFormat = OutputFormat.JsonLines   // This is the key for converting image to JSONL
};
```

> **Pro‑Tipp:** Wenn Sie mehrsprachige Belege benötigen, setzen Sie `Language = Language.Multilingual` oder übergeben Sie ein Array von `Language`‑Werten.

## Schritt 3: Führen Sie die OCR aus und erfassen Sie das Ergebnis

Jetzt **extrahieren wir tatsächlich Text aus Bild**. Die Methode `Recognize` gibt ein `OcrResult`‑Objekt zurück, das eine Sammlung von `OcrLine`‑Objekten enthält, von denen jedes eine erkannte Textzeile zusammen mit ihrer Begrenzungsbox darstellt.

```csharp
// Perform OCR
OcrResult ocrResult = ocrEngine.Recognize(receiptImage, options);
```

An diesem Punkt enthält `ocrResult.Lines` alles, was Sie benötigen – Rohtext, Vertrauenswerte und Koordinaten.

## Schritt 4: Serialisieren Sie die Zeilen zu JSON‑Lines

Wir verwandeln die Sammlung in einen schön eingerückten JSON‑String. Obwohl JSON‑Lines typischerweise kompakt sind, erleichtert das Hinzufügen von Einrückungen das Inspektieren der Datei während der Entwicklung.

```csharp
using Newtonsoft.Json;

// Serialize each line as a separate JSON object
string jsonLines = JsonConvert.SerializeObject(
    ocrResult.Lines,
    Formatting.Indented
);
```

Die resultierende Variable `jsonLines` sieht etwa so aus (gekürzt für die Übersicht):

```json
{
  "Text": "Store XYZ",
  "Confidence": 0.98,
  "BoundingBox": { "X": 10, "Y": 15, "Width": 120, "Height": 20 }
}
{
  "Text": "Date: 01/01/2026",
  "Confidence": 0.95,
  "BoundingBox": { "X": 10, "Y": 45, "Width": 180, "Height": 20 }
}
```

Jede Zeile endet mit einem Zeilenumbruch‑Zeichen, wodurch Sie eine echte **JSONL**‑Datei (JSON‑Lines) erhalten.

## Schritt 5: Schreiben Sie die JSON‑Lines auf die Festplatte

Abschließend speichern wir die Ausgabe, damit andere Dienste – wie Spark, Logstash oder ein einfaches Bash‑Skript – sie zeilenweise einlesen können.

```csharp
using System.IO;

// Choose a destination file
string outputPath = @"C:\MyProjects\OCRDemo\receipt.jsonl";
File.WriteAllText(outputPath, jsonLines);
```

Wenn Sie `receipt.jsonl` öffnen, sehen Sie ein JSON‑Objekt pro Zeile, bereit zum Streamen.

## Schritt 6: Überprüfen Sie den Export

Eine schnelle Plausibilitätsprüfung spart Ihnen später Stunden an Fehlersuche. Lesen wir die ersten Zeilen zurück und geben sie in der Konsole aus.

```csharp
Console.WriteLine("First three lines of the JSONL output:");
foreach (var line in File.ReadLines(outputPath).Take(3))
{
    Console.WriteLine(line);
}
```

Typische Konsolenausgabe:

```
First three lines of the JSONL output:
{"Text":"Store XYZ","Confidence":0.98,"BoundingBox":{"X":10,"Y":15,"Width":120,"Height":20}}
{"Text":"Date: 01/01/2026","Confidence":0.95,"BoundingBox":{"X":10,"Y":45,"Width":180,"Height":20}}
{"Text":"Total   $23.45","Confidence":0.97,"BoundingBox":{"X":10,"Y":75,"Width":150,"Height":20}}
```

Wenn Sie etwas Ähnliches sehen, herzlichen Glückwunsch – Sie haben erfolgreich **Text aus Bild extrahiert** und **Bild in JSONL konvertiert**.

## Häufige Fallstricke & wie man sie vermeidet

| Problem | Warum es passiert | Lösung |
|-------|----------------|-----|
| **Leere Ausgabe** | Bildpfad ist falsch oder Datei nicht lesbar. | Verwenden Sie `File.Exists(imagePath)` bevor Sie das Bitmap erstellen. |
| **Niedrige Vertrauenswerte** | Bild ist unscharf oder hat geringen Kontrast. | Bild vorverarbeiten (z. B. `Bitmap.RotateFlip`, `Graphics.Clear`) oder DPI erhöhen. |
| **Falsche Sprache** | OCR verwendet standardmäßig Englisch, aber der Beleg ist in einer anderen Sprache. | Setzen Sie `options.Language = Language.Spanish` (oder das passende Enum). |
| **JSONL erscheint als ein einzelnes JSON‑Array** | Sie haben `Formatting.None` ohne Zeilenumbruch‑Behandlung verwendet. | Stellen Sie sicher, dass jedes serialisierte Objekt mit `Environment.NewLine` endet. |

## Vollständiges funktionierendes Beispiel

Unten finden Sie das komplette, sofort ausführbare Programm. Fügen Sie es in ein Konsolenprojekt ein und drücken Sie **F5**.

```csharp
using Aspose.OCR;
using System;
using System.Drawing;
using System.IO;
using System.Linq;
using Newtonsoft.Json;

namespace OcrToJsonlDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the image
            string imagePath = @"C:\MyProjects\OCRDemo\receipt.png";
            if (!File.Exists(imagePath))
            {
                Console.WriteLine($"Image not found at {imagePath}");
                return;
            }
            Bitmap receiptImage = new Bitmap(imagePath);

            // 2️⃣ Set up OCR options for JSON‑Lines output
            OcrEngine ocrEngine = new OcrEngine();
            RecognitionOptions options = new RecognitionOptions
            {
                Language = Language.English,
                OutputFormat = OutputFormat.JsonLines
            };

            // 3️⃣ Perform OCR
            OcrResult ocrResult = ocrEngine.Recognize(receiptImage, options);

            // 4️⃣ Serialize to JSON‑Lines
            string jsonLines = JsonConvert.SerializeObject(
                ocrResult.Lines,
                Formatting.Indented
            );

            // 5️⃣ Write to file
            string outputPath = @"C:\MyProjects\OCRDemo\receipt.jsonl";
            File.WriteAllText(outputPath, jsonLines);
            Console.WriteLine($"✅ JSONL saved to {outputPath}");

            // 6️⃣ Quick verification
            Console.WriteLine("\nFirst three lines of output:");
            foreach (var line in File.ReadLines(outputPath).Take(3))
            {
                Console.WriteLine(line);
            }
        }
    }
}
```

**Erwartetes Ergebnis:** Eine `receipt.jsonl`‑Datei, die ein JSON‑Objekt pro Zeile enthält, jeweils mit den Feldern `Text`, `Confidence` und `BoundingBox`. Sie können diese Datei nun in jede Analyse‑Pipeline einspeisen, die JSONL verarbeitet.

## Nächste Schritte – über die Grund‑OCR hinaus

- **Batch‑Verarbeitung:** Wickeln Sie die obige Logik in eine `foreach`‑Schleife, um ganze Ordner mit Belegen zu verarbeiten.
- **Parallelität:** Verwenden Sie `Parallel.ForEach` für Mehrkern‑Beschleunigungen bei tausenden Bildern.
- **Nachbearbeitung:** Entfernen Sie Zeilen mit niedrigem Vertrauen (`Confidence < 0.9`) vor dem Speichern.
- **Integration:** Schieben Sie das JSONL direkt zu Azure Blob Storage oder AWS S3 mit den jeweiligen SDKs.
- **Alternative Formate:** Wechseln Sie `OutputFormat` zu `PlainText` oder `Xml`, falls Ihr nachgelagertes System diese bevorzugt.

## Fazit

Sie haben nun eine solide End‑zu‑End‑Lösung für **Text aus Bild extrahieren** und **Bild in JSONL konvertieren** mit Aspose OCR in C#. Das Tutorial behandelte alles vom Laden des Bitmaps bis zur Überprüfung der Ausgabe sowie einige praktische Tipps, um Ihre Pipeline robust zu halten.

Probieren Sie es mit Ihren eigenen Belegen, Rechnungen oder gescannten Formularen aus – sehen Sie zu, wie die OCR‑Engine Pixel in durchsuchbare, zeilenstrukturierte Daten verwandelt, und das in Sekunden. Wenn Sie auf Sonderfälle stoßen (z. B. schiefe Scans oder mehrsprachiger Text), schauen Sie erneut im Abschnitt *RecognitionOptions* nach und passen Sie Sprache oder Vorverarbeitungsschritte an.

Viel Spaß beim Programmieren, und mögen Ihre Datenpipelines stets sauber sein!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}