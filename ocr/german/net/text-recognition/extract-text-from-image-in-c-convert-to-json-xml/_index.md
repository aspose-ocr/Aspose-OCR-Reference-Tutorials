---
category: general
date: 2026-04-26
description: Extrahiere Text aus einem Bild in C# mit Aspose.OCR und lerne, wie du
  ein Bild in JSON‑ und XML‑Formate in wenigen Minuten konvertierst.
draft: false
keywords:
- extract text from image
- convert image to json
- convert image to xml
- Aspose OCR C#
- image to JSON C#
- image to XML C#
language: de
og_description: Extrahieren Sie Text aus einem Bild in C# mit Aspose.OCR. Lernen Sie
  Schritt für Schritt, wie Sie das Ergebnis sofort in JSON und XML konvertieren.
og_title: Text aus Bild in C# extrahieren – in JSON und XML umwandeln
tags:
- OCR
- C#
- Aspose
- JSON
- XML
title: Text aus Bild in C# extrahieren – in JSON & XML konvertieren
url: /de/net/text-recognition/extract-text-from-image-in-c-convert-to-json-xml/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Text aus Bild in C# extrahieren – In JSON & XML konvertieren

Haben Sie jemals **Text aus einem Bild** in einem .NET‑Projekt extrahieren müssen, wussten aber nicht, wie Sie die Daten tatsächlich herausbekommen? Sie sind nicht allein. In vielen realen Anwendungen – denken Sie an Rechnungsverarbeitung, Beleg‑Scanning oder Ausweis‑Verifizierung – ist das Herausziehen der rohen Zeichen aus einem Bild der erste, entscheidende Schritt.  

Die gute Nachricht? Mit Aspose.OCR können Sie das in wenigen Zeilen erledigen und dann sofort **Bild in JSON konvertieren** oder **Bild in XML konvertieren** für nachgelagerte Systeme. In diesem Leitfaden gehen wir den vollständigen, sofort ausführbaren Code durch, erklären, warum jedes Teil wichtig ist, und zeigen Ihnen ein paar Tricks, um häufige Fallstricke zu vermeiden.

---

## Was Sie benötigen

- **.NET 6+** (beliebiges aktuelles SDK funktioniert; das Beispiel zielt auf .NET 6 ab)
- **Aspose.OCR for .NET** NuGet‑Paket  
  ```bash
  dotnet add package Aspose.OCR
  ```
- Eine Bilddatei (PNG, JPG usw.), die druckbaren Text enthält; wir verwenden `invoice.png` als Beispiel.
- Ein Code‑Editor – Visual Studio, VS Code oder Rider – ganz wie Sie möchten.

Das war’s. Keine zusätzlichen OCR‑Engines, keine externen Dienste, nur ein einziges NuGet‑Paket.

---

## Schritt 1: OCR‑Engine einrichten – Wie man Text aus einem Bild extrahiert

Zuerst erstellen wir eine `OcrEngine`‑Instanz und verweisen sie auf die Bilddatei. Dieser Schritt ist die Grundlage; ohne ein korrekt geladenes Bild kann die Engine nichts erkennen.

```csharp
using Aspose.OCR;
using System.IO;

// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Load the image you want to process
// Replace YOUR_DIRECTORY with the actual folder path
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/invoice.png");

// Optional: verify the image was loaded
if (ocrEngine.Image == null)
{
    throw new FileNotFoundException("Image not found. Check the path and filename.");
}
```

**Warum das wichtig ist:**  
- `OcrEngine` kapselt alle Low‑Level‑Bildvorverarbeitungen (Binarisierung, Entzerrung).  
- Das Laden des Bildes über `ImageStream.FromFile` stellt sicher, dass die Engine die genauen Bytes liest und DPI sowie Farbtiefe beibehält – beides kann die Erkennungsgenauigkeit beeinflussen.  

> **Pro‑Tipp:** Wenn Ihre Quellbilder in einem Stream vorliegen (z. B. über eine Web‑API hochgeladen), verwenden Sie `ImageStream.FromStream(yourStream)` anstelle von `FromFile`.

---

## Schritt 2: Der Engine die erwartete Sprache mitteilen – Text aus Bild genau extrahieren

Aspose.OCR unterstützt viele Alphabete. Die Angabe der richtigen Sprache schränkt den Zeichensatz ein und erhöht die Genauigkeit.

```csharp
// Set the language; Latin covers English, French, German, etc.
ocrEngine.Language = Language.Latin;
```

**Warum:**  
Wenn Sie `Language.Latin` setzen, ignoriert die OCR‑Engine kyrillische oder asiatische Glyphen, was Fehlalarme reduziert. Wenn Sie später mehrsprachige Dokumente verarbeiten müssen, können Sie zu `Language.Multilingual` wechseln oder mehrere Sprachen kombinieren.

---

## Schritt 3: Erkennungsprozess ausführen – Text aus Bild in einem Aufruf extrahieren

Jetzt erkennen wir tatsächlich den Text. Die Methode `Recognize` gibt ein `RecognitionResult`‑Objekt zurück, das den Rohtext, Konfidenzwerte und sogar Layout‑Daten enthält.

```csharp
// Perform OCR
RecognitionResult recognitionResult = ocrEngine.Recognize();

// Quick sanity check
if (recognitionResult == null || string.IsNullOrWhiteSpace(recognitionResult.Text))
{
    Console.WriteLine("No text was detected. Verify the image quality.");
    return;
}

// Print the raw extracted text to the console
Console.WriteLine("=== Extracted Text ===");
Console.WriteLine(recognitionResult.Text);
```

**Warum:**  
Ein Aufruf von `Recognize` reicht aus, da die Engine intern Vorverarbeitung, Segmentierung und Zeichenklassifizierung durchführt. Die Eigenschaft `Text` liefert eine reine Zeichenkette, ideal für Logging oder schnelle Validierung.

---

## Schritt 4: Ergebnis in JSON konvertieren – Bild einfach in JSON umwandeln

Viele moderne Dienste bevorzugen JSON‑Payloads. Aspose.OCR stellt eine praktische `ToJson`‑Methode bereit, die das gesamte `RecognitionResult` serialisiert, einschließlich Konfidenzwerte und Begrenzungsrahmen.

```csharp
// Serialize the result to JSON
string jsonResult = recognitionResult.ToJson();

// Save the JSON to a file
File.WriteAllText("YOUR_DIRECTORY/invoice.json", jsonResult);

Console.WriteLine("JSON file saved at YOUR_DIRECTORY/invoice.json");
```

**Warum Sie JSON wollen könnten:**  
- **Interoperabilität:** Front‑End‑Apps (React, Angular) können das JSON direkt nutzen.  
- **Debugging:** Das JSON enthält die Konfidenz pro Zeichen, sodass Sie Wörter mit niedriger Konfidenz für eine manuelle Überprüfung markieren können.  

> **Sonderfall:** Wenn Ihr nachgelagertes System nur den reinen Text benötigt, können Sie `recognitionResult.Text` extrahieren und in ein benutzerdefiniertes JSON‑Objekt einbetten, anstatt die gesamte Aspose‑Payload zu verwenden.

---

## Schritt 5: Ergebnis in XML konvertieren – Bild für Altsysteme in XML umwandeln

Einige Unternehmen nutzen noch XML‑Schemata für den Datenaustausch. Die Methode `ToXml` entspricht `ToJson`, gibt jedoch XML aus.

```csharp
// Serialize the result to XML
string xmlResult = recognitionResult.ToXml();

// Save the XML to a file
File.WriteAllText("YOUR_DIRECTORY/invoice.xml", xmlResult);

Console.WriteLine("XML file saved at YOUR_DIRECTORY/invoice.xml");
```

**Warum XML:**  
- **Schema‑Validierung:** Sie können ein XSD definieren, das der von Aspose erzeugten Struktur entspricht und so die Vertragstreue sicherstellt.  
- **Integration:** Ältere ERP‑ oder Dokumenten‑Management‑Systeme können XML häufig sofort verarbeiten.

---

## Vollständiges funktionierendes Beispiel – Alles‑in‑einem‑Code

Unten finden Sie das vollständige Programm, das alles zusammenführt. Kopieren Sie es in ein neues Konsolenprojekt (`dotnet new console`) und führen Sie es aus.

```csharp
using Aspose.OCR;
using System;
using System.IO;

namespace ImageOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Initialize OCR engine and load the image
            // -------------------------------------------------
            OcrEngine ocrEngine = new OcrEngine();
            // Adjust the path to point at your PNG/JPG file
            string imagePath = "YOUR_DIRECTORY/invoice.png";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            if (ocrEngine.Image == null)
            {
                Console.WriteLine($"Unable to load image at {imagePath}");
                return;
            }

            // -------------------------------------------------
            // Step 2: Specify language (Latin for most European scripts)
            // -------------------------------------------------
            ocrEngine.Language = Language.Latin;

            // -------------------------------------------------
            // Step 3: Run OCR and get the result
            // -------------------------------------------------
            RecognitionResult result = ocrEngine.Recognize();

            if (result == null || string.IsNullOrWhiteSpace(result.Text))
            {
                Console.WriteLine("No text detected – check image quality or language setting.");
                return;
            }

            Console.WriteLine("=== Extracted Text ===");
            Console.WriteLine(result.Text);
            Console.WriteLine();

            // -------------------------------------------------
            // Step 4: Convert to JSON (convert image to json)
            // -------------------------------------------------
            string json = result.ToJson();
            string jsonPath = "YOUR_DIRECTORY/invoice.json";
            File.WriteAllText(jsonPath, json);
            Console.WriteLine($"JSON output written to {jsonPath}");

            // -------------------------------------------------
            // Step 5: Convert to XML (convert image to xml)
            // -------------------------------------------------
            string xml = result.ToXml();
            string xmlPath = "YOUR_DIRECTORY/invoice.xml";
            File.WriteAllText(xmlPath, xml);
            Console.WriteLine($"XML output written to {xmlPath}");
        }
    }
}
```

**Erwartete Ausgabe (Konsole):**

```
=== Extracted Text ===
Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
...

JSON file saved at YOUR_DIRECTORY/invoice.json
XML file saved at YOUR_DIRECTORY/invoice.xml
```

Die JSON‑ und XML‑Dateien enthalten eine umfangreichere Struktur, zum Beispiel:

```json
{
  "Text": "Invoice #12345\nDate: 2024‑03‑15\nTotal: $1,250.00",
  "Confidence": 0.96,
  "Blocks": [
    { "Text": "Invoice #12345", "Confidence": 0.98, "Rectangle": { "X": 12, "Y": 30, "Width": 200, "Height": 20 } },
    ...
  ]
}
```

```xml
<RecognitionResult>
  <Text>Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00</Text>
  <Confidence>0.96</Confidence>
  <Blocks>
    <Block>
      <Text>Invoice #12345</Text>
      <Confidence>0.98</Confidence>
      <Rectangle X="12" Y="30" Width="200" Height="20"/>
    </Block>
    ...
  </Blocks>
</RecognitionResult>
```

---

## Häufige Fragen & Sonderfälle

### Was ist, wenn das Bild unscharf oder gedreht ist?
Aspose.OCR entzerrt die meisten Bilder automatisch, aber bei extremen Fällen möchten Sie möglicherweise vorher mit `ocrEngine.Image = ImageProcessor.Deskew(ocrEngine.Image)` vorverarbeiten. Ein leichter Kontrast‑Boost (`ImageProcessor.AdjustContrast`) kann ebenfalls den Konfidenzwert verbessern.

### Kann ich Text aus PDFs extrahieren?
Ja – konvertieren Sie zunächst jede PDF‑Seite in ein Bild (z. B. mit Aspose.PDF oder einer freien Bibliothek wie PDFium) und geben Sie diese Bilder dann in denselben OCR‑Ablauf.

### Wie gehe ich mit mehreren Sprachen in einem Dokument um?
Setzen Sie `ocrEngine.Language = Language.Multilingual;` oder kombinieren Sie bestimmte Sprachen:

```csharp
ocrEngine.Language = Language.English | Language.French | Language.German;
```

Be aware that broader language sets may

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}