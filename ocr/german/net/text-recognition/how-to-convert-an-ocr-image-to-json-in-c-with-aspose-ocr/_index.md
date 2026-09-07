---
category: general
date: 2026-09-06
description: OCR-Bild zu JSON-Konvertierung in C# mit Aspose.OCR – Schritt‑für‑Schritt‑Anleitung
  zum Extrahieren von Text aus einem Bild und zum Erhalten einer JSON‑Ausgabe.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- ocr image to json
- extract text from image
- convert image to text
- recognize text from photo
- load image for ocr
language: de
lastmod: 2026-09-06
og_description: OCR-Bild zu JSON in C# mit Aspose.OCR. Erfahren Sie, wie Sie ein Bild
  für OCR laden, Text aus einem Foto erkennen und das Ergebnis in JSON konvertieren.
og_image_alt: Screenshot of C# code that converts an OCR image to JSON using Aspose.OCR
og_title: OCR-Bild in JSON konvertieren in C# – vollständige Aspose.OCR-Anleitung
schemas:
- author: Aspose
  dateModified: '2026-09-06'
  description: ocr image to json conversion in C# using Aspose.OCR – step‑by‑step
    guide to extract text from image and get JSON output.
  headline: How to convert an OCR image to JSON in C# with Aspose.OCR
  type: TechArticle
- description: ocr image to json conversion in C# using Aspose.OCR – step‑by‑step
    guide to extract text from image and get JSON output.
  name: How to convert an OCR image to JSON in C# with Aspose.OCR
  steps:
  - name: Place an image named `input.jpg` in the project root.
    text: Place an image named `input.jpg` in the project root.
  - name: Execute `dotnet run`.
    text: Execute `dotnet run`.
  - name: Observe the console output and open `output.json` to see the structured
      data.
    text: Observe the console output and open `output.json` to see the structured
      data.
  type: HowTo
- questions:
  - answer: Yes. Use `ocrEngine.SaveJson(Stream)` to write directly to a `MemoryStream`,
      then call `stream.ToArray()`.
    question: Can I get the OCR result as a byte array instead of a file?
  - answer: Aspose.OCR can accept PDF pages converted to images via Aspose.PDF, but
      the OCR engine itself works on raster images. Convert PDFs to images first,
      then **load image for ocr**.
    question: Does the engine support PDF input?
  - answer: 'Set `ocrEngine.Language = OcrLanguage.Arabic`. The JSON includes the
      correct text direction, which you can render in UI frameworks that support RTL.
      ## Conclusion You now have a complete solution for **ocr image to json** in
      C#. By loading an image, configuring the language, running the OCR engine, '
    question: How do I handle right‑to‑left scripts like Arabic?
  type: FAQPage
tags:
- Aspose.OCR
- C#
- JSON
- Image processing
title: Wie man ein OCR‑Bild in JSON in C# mit Aspose.OCR konvertiert
url: /de/net/text-recognition/how-to-convert-an-ocr-image-to-json-in-c-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man ein OCR‑Bild in JSON in C# mit Aspose.OCR konvertiert

Wenn Sie **ocr image to json** in einer .NET‑Anwendung benötigen, zeigt Ihnen dieses Handbuch, wie Sie das mit Aspose.OCR erledigen. Wir führen Sie durch das Laden eines Bildes für OCR, das Erkennen von Text aus einem Foto und das Konvertieren des Ergebnisses in JSON, sodass Sie die Daten in APIs oder Datenbanken nutzen können.

Das Extrahieren von Text aus Bilddateien ist ein häufiges Anliegen bei der Rechnungsverarbeitung, Beleg‑Scanning und Archivierungsprojekten. Am Ende dieses Tutorials können Sie **convert image to text**, das reine Text‑Ergebnis abrufen und ein strukturiertes JSON‑Payload erzeugen, das Layout‑Informationen bewahrt.

## Voraussetzungen

Bevor Sie beginnen, stellen Sie sicher, dass Sie Folgendes haben:

- .NET 6.0 SDK oder neuer installiert  
- Visual Studio 2022 (oder ein beliebiger Editor, der .NET unterstützt)  
- Das Aspose.OCR NuGet‑Paket (`Aspose.OCR`) zu Ihrem Projekt hinzugefügt  
- Ein Beispielbild (`input.jpg`) in einem Ordner, den Sie im Code referenzieren können  

Sie benötigen keine zusätzlichen OCR‑Engines; Aspose.OCR übernimmt die schwere Arbeit intern.

## Schritt 1: Das Aspose.OCR NuGet‑Paket installieren

Öffnen Sie ein Terminal im Projektordner und führen Sie aus:

```bash
dotnet add package Aspose.OCR
```

Das Paket enthält die Klasse `Aspose.OCR.OcrEngine`, die Methoden für **load image for ocr**, Sprachauswahl und Ergebnis‑Export bereitstellt.

## Schritt 2: Ein neues C#‑Konsolenprojekt erstellen

Falls Sie noch kein Projekt haben, erstellen Sie eines:

```bash
dotnet new console -n OcrToJsonDemo
cd OcrToJsonDemo
```

Fügen Sie die benötigten `using`‑Direktiven hinzu:

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;
using System.IO;
```

## Schritt 3: Das Bild laden und die OCR‑Engine konfigurieren

Der folgende Code demonstriert, wie Sie **load image for ocr**, die Sprache setzen und die Engine für die Verarbeitung vorbereiten. In diesem Beispiel verwenden wir Kyrillisch, Sie können jedoch zu `OcrLanguage.English`, `OcrLanguage.French` usw. wechseln, je nach Ausgangssprache.

```csharp
// Step 3: Initialize the OCR engine
var ocrEngine = new OcrEngine();

// Choose the language that matches the text in the image.
// Replace OcrLanguage.Cyrillic with the language you need.
ocrEngine.Language = OcrLanguage.Cyrillic;

// Load the image file. The ImageStream class abstracts file, stream, or byte[] sources.
string imagePath = Path.Combine(Environment.CurrentDirectory, "input.jpg");
ocrEngine.Image = ImageStream.FromFile(imagePath);
```

> **Warum das wichtig ist:** Die korrekte Spracheinstellung verbessert die Genauigkeit erheblich, wenn Sie **recognize text from photo**. Die Engine nutzt sprachspezifische Wörterbücher und Zeichensätze.

## Schritt 4: Den OCR‑Prozess ausführen und Ergebnisse abrufen

Jetzt führen Sie die OCR‑Engine aus. Wenn der Vorgang erfolgreich ist, können Sie **extract text from image** als Klartext, HTML oder JSON erhalten. Aspose.OCR stellt die Methode `SaveJson` bereit, die das strukturierte Ergebnis in einer Datei speichert.

```csharp
// Step 4: Execute the OCR process
if (ocrEngine.Process())
{
    // Plain‑text output
    string plainText = ocrEngine.Text;
    Console.WriteLine("=== Plain Text ===");
    Console.WriteLine(plainText);

    // JSON output – includes bounding boxes, confidence scores, and line information
    string jsonPath = Path.Combine(Environment.CurrentDirectory, "output.json");
    ocrEngine.SaveJson(jsonPath);
    Console.WriteLine($"\nJSON result saved to: {jsonPath}");
}
else
{
    Console.WriteLine("OCR processing failed. Check the image path and format.");
}
```

### Erwartete JSON‑Struktur

Eine typische `output.json`‑Datei sieht so aus (zur besseren Lesbarkeit formatiert):

```json
{
  "Pages": [
    {
      "PageNumber": 1,
      "Lines": [
        {
          "Text": "Пример текста",
          "Confidence": 0.96,
          "Rect": { "X": 45, "Y": 120, "Width": 210, "Height": 30 }
        },
        {
          "Text": "Еще одна строка",
          "Confidence": 0.93,
          "Rect": { "X": 45, "Y": 160, "Width": 230, "Height": 28 }
        }
      ]
    }
  ]
}
```

Das JSON‑Payload enthält den Text jeder Zeile, einen Vertrauens‑Score und das Rechteck, das die Zeile im Originalfoto umschließt. Das erleichtert das Zuordnen des OCR‑Ergebnisses zu UI‑Elementen oder Datenbankfeldern.

## Schritt 5: Vollständiger Quellcode für die Demo

Unten finden Sie das komplette, sofort lauffähige Programm, das den **ocr image to json**‑Workflow ausführt. Kopieren Sie es in `Program.cs` und führen Sie `dotnet run` aus.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace OcrToJsonDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize the OCR engine
            var ocrEngine = new OcrEngine();

            // 2️⃣ Select the language (Cyrillic in this example)
            ocrEngine.Language = OcrLanguage.Cyrillic;

            // 3️⃣ Load the image you want to process
            string imagePath = Path.Combine(Environment.CurrentDirectory, "input.jpg");
            if (!File.Exists(imagePath))
            {
                Console.WriteLine($"Image not found: {imagePath}");
                return;
            }
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // 4️⃣ Run the OCR process
            if (ocrEngine.Process())
            {
                // 5️⃣ Retrieve plain text (optional)
                string plainText = ocrEngine.Text;
                Console.WriteLine("=== Plain Text ===");
                Console.WriteLine(plainText);

                // 6️⃣ Save the result as JSON
                string jsonPath = Path.Combine(Environment.CurrentDirectory, "output.json");
                ocrEngine.SaveJson(jsonPath);
                Console.WriteLine($"\nJSON result saved to: {jsonPath}");
            }
            else
            {
                Console.WriteLine("OCR processing failed. Verify the image format and language settings.");
            }
        }
    }
}
```

### Ausführen des Beispiels

1. Legen Sie ein Bild mit dem Namen `input.jpg` im Projekt‑Root ab.  
2. Führen Sie `dotnet run` aus.  
3. Beobachten Sie die Konsolenausgabe und öffnen Sie `output.json`, um die strukturierten Daten zu sehen.

## Profi‑Tipps und häufige Stolperfallen

| Situation | Empfehlung |
|-----------|------------|
| **Low‑resolution photos** | DPI vor der Verarbeitung erhöhen oder `ocrEngine.Image = ImageStream.FromFile(path, 300)` verwenden, um 300 DPI zu erzwingen. |
| **Mixed languages** | `ocrEngine.Language = OcrLanguage.Multilingual` setzen und optional eine Sprachliste via `ocrEngine.Language = new[] { OcrLanguage.English, OcrLanguage.Cyrillic }` bereitstellen. |
| **Large documents** | Seite für Seite verarbeiten, um den Speicherverbrauch gering zu halten; die Engine unterstützt mehrseitige TIFFs. |
| **Incorrect characters** | Sicherstellen, dass das richtige `OcrLanguage` ausgewählt ist; die falsche Sprache reduziert die Genauigkeit, wenn Sie **convert image to text**. |
| **JSON missing fields** | Verwenden Sie Aspose.OCR Version 23.6 oder neuer; ältere Versionen boten die `SaveJson`‑Methode nicht. |

## Häufig gestellte Fragen

**F: Kann ich das OCR‑Ergebnis als Byte‑Array statt als Datei erhalten?**  
A: Ja. Verwenden Sie `ocrEngine.SaveJson(Stream)`, um direkt in einen `MemoryStream` zu schreiben, und rufen Sie anschließend `stream.ToArray()` auf.

**F: Unterstützt die Engine PDF‑Eingaben?**  
A: Aspose.OCR kann PDF‑Seiten akzeptieren, die zuvor über Aspose.PDF in Bilder konvertiert wurden, aber die OCR‑Engine selbst arbeitet mit Rasterbildern. Konvertieren Sie PDFs zuerst in Bilder und dann **load image for ocr**.

**F: Wie gehe ich mit rechts‑nach‑links‑Schriften wie Arabisch um?**  
A: Setzen Sie `ocrEngine.Language = OcrLanguage.Arabic`. Das JSON enthält die korrekte Text‑Richtung, die Sie in UI‑Frameworks mit RTL‑Unterstützung rendern können.

## Fazit

Sie haben nun eine komplette Lösung für **ocr image to json** in C#. Durch das Laden eines Bildes, das Konfigurieren der Sprache, das Ausführen der OCR‑Engine und das Exportieren des Ergebnisses als JSON können Sie **extract text from image**, **convert image to text** und **recognize text from photo** in einem einzigen, optimierten Workflow.

Von hier aus können Sie:

- Das JSON‑Output in eine Web‑API (`ASP.NET Core`) integrieren  
- Das Ergebnis in einer NoSQL‑Datenbank wie MongoDB speichern  
- Eine Nachbearbeitung hinzufügen, um typische OCR‑Fehler zu korrigieren  

Experimentieren Sie gern mit verschiedenen Sprachen, Bildformaten und Ausgabeoptionen, um sie an die Bedürfnisse Ihres Projekts anzupassen. Viel Spaß beim Coden!

## Was sollten Sie als Nächstes lernen?


Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [recognize text from image in C# – Complete Guide to OCR and JSON](/ocr/english/net/text-recognition/recognize-text-from-image-in-c-complete-guide-to-ocr-and-jso/)
- [Convert Image to Text in C# with Aspose OCR – Step‑by‑Step Guide](/ocr/english/net/text-recognition/convert-image-to-text-in-c-with-aspose-ocr-step-by-step-guid/)
- [How to Extract Text from Image Using Aspose.OCR for .NET](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}