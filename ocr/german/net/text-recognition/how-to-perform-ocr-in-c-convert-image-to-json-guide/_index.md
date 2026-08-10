---
category: general
date: 2026-02-17
description: Wie man OCR in C# durchführt und ein Bild schnell in JSON konvertiert.
  Folgen Sie diesem C#‑OCR‑Tutorial, um Text aus Bildern zu extrahieren und das Layout
  als JSON zu speichern.
draft: false
keywords:
- how to perform OCR
- convert image to json
- c# ocr tutorial
- extract text image c#
- load image file c#
language: de
og_description: Wie führt man OCR in C# durch? Dieser Leitfaden zeigt, wie man ein
  Bild in JSON konvertiert, Text aus einem Bild in C# extrahiert und eine Bilddatei
  für OCR lädt.
og_title: Wie man OCR in C# durchführt – Bild in JSON konvertieren
tags:
- OCR
- C#
- Aspose
title: Wie man OCR in C# durchführt – Leitfaden zur Umwandlung von Bildern in JSON
url: /de/net/text-recognition/how-to-perform-ocr-in-c-convert-image-to-json-guide/
---

crEngine** | Sets up default language (English) and prepares internal models. |
...

We replaced with German. Keep same number of hyphens.

Now final output: all content with translations.

Let's produce final.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man OCR in C# durchführt – Bild in JSON konvertieren Anleitung

Haben Sie sich jemals gefragt, **wie man OCR** auf einer Quittung, Rechnung oder einem beliebigen gescannten Dokument mit C# durchführt? Sie sind nicht allein. Viele Entwickler stoßen an Grenzen, wenn sie Text *und* das Layout extrahieren müssen, ohne Stunden damit zu verbringen, eigene Parser zu schreiben.  

In diesem Tutorial führen wir Sie durch ein vollständiges **c# ocr tutorial**, das Ihnen genau zeigt, wie man OCR durchführt, **Bild in JSON konvertiert**, und das Ergebnis für spätere Analysen speichert. Am Ende haben Sie eine sofort einsatzbereite Konsolen‑App, die eine Bilddatei in C# lädt, den Text extrahiert und eine detaillierte JSON‑Datei mit Koordinaten, Vertrauenswerten und dem Rohtext schreibt.

## Voraussetzungen — Was Sie benötigen

- .NET 6 SDK oder neuer (der Code funktioniert auch unter .NET Core)  
- Visual Studio 2022 oder ein beliebiger Editor Ihrer Wahl  
- Eine Aspose OCR‑Lizenz (Sie können mit einer kostenlosen Testversion beginnen)  
- Ein Beispielbild, z. B. `receipt.png`, in einem Ordner, auf den Sie verweisen können  

Das war's – keine zusätzlichen NuGet‑Pakete außer `Aspose.OCR`. Wenn Sie diese Komponenten haben, können Sie loslegen.

## Wie man OCR durchführt und JSON‑Ausgabe erhält

Der Kern von **wie man OCR durchführt** mit Aspose ist einfach: Erstellen Sie eine `OcrEngine`, übergeben ihr einen Bild‑Stream, rufen `Recognize` auf und serialisieren anschließend das `OcrResult` nach JSON. Lassen Sie uns das Schritt für Schritt aufschlüsseln.

### Schritt 1: Installieren Sie das Aspose OCR NuGet‑Paket

Öffnen Sie Ihr Terminal im Projektordner und führen Sie aus:

```bash
dotnet add package Aspose.OCR
```

> **Pro‑Tipp:** Verwenden Sie das Flag `--version`, um auf die neueste stabile Version zu fixieren (z. B. `23.9.0`). So bleibt Ihr Build reproduzierbar.

### Schritt 2: Erstellen Sie das Grundgerüst des Konsolenprojekts

Falls Sie noch kein Projekt haben, erstellen Sie eines:

```bash
dotnet new console -n OcrJsonDemo
cd OcrJsonDemo
```

Jetzt haben Sie eine `Program.cs`‑Datei, bereit für den Code, der **load image file c#** lädt und den OCR‑Prozess startet.

### Schritt 3: Schreiben Sie den vollständigen OCR‑zu‑JSON‑Code

Unten finden Sie das komplette, sofort ausführbare Programm. Kopieren Sie es in `Program.cs`. Jede Zeile ist kommentiert, damit Sie sehen können, *warum* jedes Element wichtig ist.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class JsonOutput
{
    static void Main()
    {
        // ---------------------------------------------------------
        // 1️⃣  Initialize the OCR engine – this object holds
        //     language settings, recognition options, etc.
        // ---------------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine();

        // ---------------------------------------------------------
        // 2️⃣  Load the image you want to analyze.
        //     This demonstrates **load image file c#** in a clean way.
        // ---------------------------------------------------------
        // Replace the path with the actual location of your receipt.png
        string imagePath = Path.Combine(
            Environment.CurrentDirectory, "receipt.png");
        ImageStream image = ImageStream.FromFile(imagePath);

        // ---------------------------------------------------------
        // 3️⃣  Perform the recognition.
        //     The engine returns an OcrResult containing text,
        //     confidence scores, and layout information.
        // ---------------------------------------------------------
        OcrResult ocrResult = ocrEngine.Recognize(image);

        // ---------------------------------------------------------
        // 4️⃣  Convert the result to a detailed JSON string.
        //     This is the heart of **convert image to json**.
        // ---------------------------------------------------------
        string jsonResult = ocrResult.ToJson();

        // ---------------------------------------------------------
        // 5️⃣  Save the JSON to disk – you can later import this into
        //     databases, analytics pipelines, or UI components.
        // ---------------------------------------------------------
        string jsonPath = Path.Combine(
            Environment.CurrentDirectory, "receipt.json");
        File.WriteAllText(jsonPath, jsonResult);

        // ---------------------------------------------------------
        // 6️⃣  Let the user know we’re done.
        // ---------------------------------------------------------
        Console.WriteLine("JSON with layout saved to " + jsonPath);
    }
}
```

#### Was der Code macht

| Schritt | Warum es wichtig ist |
|------|----------------|
| **Initialize OcrEngine** | Richtet die Standardsprache (Englisch) ein und bereitet interne Modelle vor. |
| **Load image file** | Durch die Verwendung von `ImageStream.FromFile` wird sichergestellt, dass das Bild in einem von Aspose erwarteten Format gelesen wird. |
| **Recognize** | Die schwere Arbeit – Pixelanalyse, Zeichen­segmentierung und Wörterbuch‑Lookup. |
| **ToJson** | Erzeugt eine strukturierte Ausgabe, die Begrenzungsrahmen, Vertrauenswerte und den Rohtext enthält. |
| **WriteAllText** | Speichert das JSON, sodass Sie es mit anderen Diensten teilen können. |
| **Console.WriteLine** | Gibt sofortiges Feedback – praktisch beim Ausführen im Terminal. |

> **Achtung:** Wenn Ihr Bild groß ist, sollten Sie es zuerst verkleinern, um Geschwindigkeit und Speicherverbrauch zu verbessern. Aspose stellt `Resize`‑Methoden bereit, die Sie auf `ImageStream` aufrufen können.

### Schritt 4: Anwendung ausführen und Ausgabe überprüfen

Im Terminal:

```bash
dotnet run
```

Sie sollten sehen:

```
JSON with layout saved to C:\Path\To\OcrJsonDemo\receipt.json
```

Öffnen Sie `receipt.json` in einem beliebigen Editor; Sie finden etwas Ähnliches:

```json
{
  "Pages": [
    {
      "Blocks": [
        {
          "Text": "Total: $12.34",
          "Confidence": 0.98,
          "BoundingBox": { "X": 120, "Y": 340, "Width": 150, "Height": 30 }
        }
      ]
    }
  ]
}
```

Dieses JSON erfasst **extract text image c#** plus Layout‑Metadaten, perfekt für die nachgelagerte Verarbeitung.

## Bild in JSON konvertieren – über die Grundlagen hinaus

Jetzt, wo Sie **wie man OCR durchführt** kennen, lassen Sie uns ein paar Varianten untersuchen, die Sie in realen Projekten benötigen könnten.

### Mehrere Seiten verarbeiten

Wenn Ihre Quelle ein mehrseitiges PDF oder TIFF ist, iterieren Sie einfach über jede Seite:

```csharp
foreach (var pageStream in multiPageImageStreams)
{
    OcrResult result = ocrEngine.Recognize(pageStream);
    // Append each page's JSON to a master list
}
```

### Sprache und Genauigkeit anpassen

Aspose unterstützt über 40 Sprachen. Um zu Spanisch zu wechseln:

```csharp
ocrEngine.Language = Language.Spanish;
```

Sie können außerdem `ocrEngine.Settings` anpassen, um **auto‑rotate**, **noise removal** oder **dictionary‑based correction** zu aktivieren – alles verbessert die Qualität des erhaltenen JSON.

### JSON im lesbaren Format speichern

Wenn Sie eingerücktes JSON für bessere Lesbarkeit bevorzugen:

```csharp
string prettyJson = ocrResult.ToJson(true); // true = formatted
File.WriteAllText(jsonPath, prettyJson);
```

## Bilddatei laden C# – Häufige Fallstricke und Tipps

Wenn Sie **load image file c#** ausführen, können folgende Probleme auftreten:

- **File not found** – Stellen Sie sicher, dass der Pfad absolut ist oder verwenden Sie `Path.Combine` mit `Environment.CurrentDirectory`.  
- **Unsupported format** – Aspose unterstützt PNG, JPEG, BMP, TIFF und PDF. Für RAW‑Formate konvertieren Sie diese zuerst.  
- **Large file memory pressure** – Verwenden Sie `ImageStream.FromFile(path, maxSizeInKB)`, um beim Laden die Größe zu reduzieren.

Das frühzeitige Beheben dieser Probleme erspart Ihnen später kryptische Ausnahmen in der OCR‑Pipeline.

## Text aus Bild extrahieren C# – Ergebnisse verifizieren

Nachdem Sie das JSON haben, möchten Sie möglicherweise nur den reinen Text:

```csharp
var ocrResult = ocrEngine.Recognize(image);
string plainText = ocrResult.Text; // Simple string with line breaks
Console.WriteLine(plainText);
```

Dieses Snippet demonstriert **extract text image c#** ohne Layout‑Details – praktisch für schnelle Suchen oder Protokollierung.

![Diagramm, das den OCR‑Arbeitsablauf – wie man OCR durchführt, Bild in JSON konvertiert und Text aus Bild extrahiert](/images/ocr-workflow.png "wie man OCR‑Arbeitsablauf")

*Bild‑Alt‑Text: "wie man OCR‑Arbeitsablauf‑Diagramm, das die Konvertierung von Bild zu JSON und das Extrahieren von Text aus Bild illustriert"*  
*(Das Bild ist ein Platzhalter; ersetzen Sie es durch ein echtes Diagramm beim Veröffentlichen.)*

## Fazit

Wir haben **wie man OCR** in C# von Anfang bis Ende behandelt, Ihnen gezeigt, wie man **Bild in JSON konvertiert**, und die Nuancen von **load image file c#** und **extract text image c#** erklärt. Das vollständige Code‑Beispiel kann in jedes .NET‑Projekt übernommen werden, und die JSON‑Ausgabe liefert sowohl Rohtext als auch präzise Layout‑Daten für nachgelagerte Analysen.

Was kommt als Nächstes? Versuchen Sie, das JSON in eine Datenbank zu speisen, Begrenzungsrahmen in einer UI zu visualisieren oder mehrere OCR‑Durchläufe für die Stapelverarbeitung zu verketten. Sie können auch mit anderen Aspose‑Funktionen wie Handschriftenerkennung oder Barcode‑Erkennung experimentieren – beide passen natürlich in dieselbe Pipeline.

Wenn Sie auf Probleme stoßen, schauen Sie sich die Fehlertipps im Abschnitt „Load Image File C#“ erneut an oder erkunden Sie Asposes umfangreiche Dokumentation für erweiterte Einstellungen. Viel Spaß beim Programmieren und beim Umwandeln von Bildern in strukturierte Daten!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}