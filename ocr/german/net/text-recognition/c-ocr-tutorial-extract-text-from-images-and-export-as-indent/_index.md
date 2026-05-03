---
category: general
date: 2026-05-02
description: c# OCR‑Tutorial, das zeigt, wie man Text aus einem Bild in c# extrahiert
  und PNG‑Text erkennt, dann mit JsonSerializer c# eingerücktes JSON schreibt. Schritt‑für‑Schritt‑Anleitung
  für Entwickler.
draft: false
keywords:
- c# ocr tutorial
- extract text image c#
- recognize png text
- write indented json
- use jsonserializer c#
language: de
og_description: c# OCR‑Tutorial, das zeigt, wie man Text aus einem Bild in C# extrahiert
  und PNG‑Text erkennt, dann mit JsonSerializer in C# eingerücktes JSON schreibt.
  Vollständiges, ausführbares Beispiel.
og_title: c# OCR‑Tutorial – Text extrahieren und als eingerücktes JSON exportieren
tags:
- OCR
- C#
- Aspose
- JSON
title: c# OCR‑Tutorial – Text aus Bildern extrahieren und als eingerücktes JSON exportieren
url: /de/net/text-recognition/c-ocr-tutorial-extract-text-from-images-and-export-as-indent/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr tutorial – Text aus Bildern extrahieren und als eingerücktes JSON exportieren

Haben Sie schon einmal ein **c# ocr tutorial** gebraucht, das von einem Bild mit Text direkt zu einer schön formatierten JSON‑Datei führt? Sie sind nicht der Einzige. In vielen Projekten – denken Sie an Rechnungsscan, Belegauswertung oder sogar einfache Meme‑Textextraktion – endet man mit einer PNG‑Datei und fragt sich, wie man die Wörter extrahiert, ohne einen eigenen Erkenner zu schreiben.  

Dieser Leitfaden bietet Ihnen eine praxisnahe Lösung: Wir **extrahieren Text aus Bild c#** mit Aspose.OCR, **erkennen png‑Text** und schreiben dann **eingebettetes JSON** mit `JsonSerializer` in C#. Am Ende haben Sie eine eigenständige Konsolen‑App, die Sie in jede .NET‑Lösung einbinden können. Keine vagen „siehe Dokumentation“-Links, sondern ein vollständiges, copy‑and‑paste‑fertiges Beispiel.

## Was Sie benötigen

- **.NET 6** (oder jede aktuelle .NET‑Version). Ältere Frameworks funktionieren, aber die gezeigte Syntax zielt auf .NET 6+ ab.  
- **Aspose.OCR for .NET** – Installation via NuGet: `dotnet add package Aspose.OCR`.  
- Ein Beispiel‑PNG‑Bild (`text.png`) mit klarem, maschinenlesbarem Text.  
- Eine IDE oder ein Editor Ihrer Wahl – Visual Studio, VS Code, Rider usw.

> **Pro‑Tipp:** Wenn Sie viele Bilder verarbeiten wollen, sollten Sie eine einzelne `OcrEngine`‑Instanz wiederverwenden, anstatt für jede Datei eine neue zu erstellen. Das reduziert den Overhead und erhöht den Durchsatz.

## Schritt 1: Ein c# ocr tutorial‑Projekt einrichten

Zuerst ein Konsolen‑Projekt anlegen. Die folgenden Befehle erzeugen das Grundgerüst und binden die OCR‑Bibliothek ein:

```bash
dotnet new console -n OcrJsonDemo
cd OcrJsonDemo
dotnet add package Aspose.OCR
```

Öffnen Sie nun die erzeugte `Program.cs`. Wir ersetzen den Inhalt später durch das vollständige Beispiel, aber stellen Sie jetzt sicher, dass das Projekt kompiliert:

```bash
dotnet build
```

Wenn keine Fehler auftreten, können Sie weitermachen.

## Schritt 2: PNG‑Text aus einem Bild erkennen

Das Herz jedes **c# ocr tutorial** ist die OCR‑Engine selbst. Aspose.OCR verbirgt die Low‑Level‑Details und stellt Ihnen eine saubere `OcrEngine`‑Klasse zur Verfügung. Im Folgenden erstellen wir die Engine, weisen ihr eine PNG‑Datei zu und lassen sie den Text erkennen.

```csharp
using Aspose.OCR;
using System;
using System.Text.Json;

class JsonExportExample
{
    public static void Run()
    {
        // 1️⃣ Create an OCR engine instance – this is the entry point for all OCR work.
        var ocrEngine = new OcrEngine();

        // 2️⃣ Recognize text from the input image. 
        //    The method automatically detects the language (default is English) and returns an OcrResult.
        var ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/text.png");

        // If the image couldn't be read, handle it gracefully.
        if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
        {
            Console.WriteLine("No text detected – double‑check the file path and image quality.");
            return;
        }

        // Continue to serialization...
```

### Warum das funktioniert

- **`RecognizeImage`** unterstützt viele Formate (PNG, JPEG, BMP). Wir **erkennen png‑Text**, weil PNG verlustfreie Details bewahrt – ideal für OCR.  
- Das zurückgegebene `OcrResult` enthält nicht nur den reinen Text, sondern auch einen Confidence‑Score pro Glyph, nützlich, wenn Sie später Zeichen mit niedriger Sicherheit herausfiltern wollen.

## Schritt 3: Eingebettetes JSON mit JsonSerializer c# schreiben

Jetzt, wo wir `ocrResult` haben, ist der nächste logische Schritt in unserem **c# ocr tutorial**, dieses Objekt in menschenlesbares JSON zu verwandeln. Der integrierte `System.Text.Json`‑Serializer erledigt das, und wir konfigurieren ihn, **eingebettetes json** für bessere Lesbarkeit zu erzeugen.

```csharp
        // 3️⃣ Serialize the OCR result (including confidence per glyph) to indented JSON.
        var jsonOptions = new JsonSerializerOptions
        {
            WriteIndented = true // This makes the output pretty‑printed.
        };

        string jsonOutput = JsonSerializer.Serialize(ocrResult, jsonOptions);

        // 4️⃣ Display the JSON result – you could also write it to a file if you prefer.
        Console.WriteLine(jsonOutput);
    }
}
```

### `JsonSerializer` korrekt verwenden

- Der `WriteIndented`‑Schalter ist der einfachste Weg, **eingebettetes json** zu erzeugen, ohne Drittanbieter‑Bibliotheken zu nutzen.  
- Wenn Sie camel‑Case‑Eigenschaftsnamen benötigen, fügen Sie `PropertyNamingPolicy = JsonNamingPolicy.CamelCase` zu den Optionen hinzu.  
- Der String `jsonOutput` kann mit `File.WriteAllText("result.json", jsonOutput);` gespeichert werden – ein praktischer Hinweis für reale Pipelines.

## Schritt 4: Ausführen und Ausgabe prüfen

Kompilieren und starten Sie das Programm:

```bash
dotnet run
```

Angenommen, `text.png` enthält den Satz *„Hello, OCR World!“*, dann sollte etwa Folgendes erscheinen:

```json
{
  "Text": "Hello, OCR World!",
  "Confidence": 0.9875,
  "Lines": [
    {
      "Text": "Hello, OCR World!",
      "Confidence": 0.9875,
      "Words": [
        {
          "Text": "Hello,",
          "Confidence": 0.9921,
          "BoundingBox": { "X": 12, "Y": 34, "Width": 58, "Height": 20 }
        },
        {
          "Text": "OCR",
          "Confidence": 0.9812,
          "BoundingBox": { "X": 78, "Y": 34, "Width": 34, "Height": 20 }
        },
        {
          "Text": "World!",
          "Confidence": 0.9890,
          "BoundingBox": { "X": 118, "Y": 34, "Width": 62, "Height": 20 }
        }
      ]
    }
  ]
}
```

Dieses JSON ist **eingebettet**, was das Lesen in Logs oder das Weitergeben an nachgelagerte Services erleichtert.

### Randfälle & Tipps

| Situation | Was zu tun ist |
|-----------|----------------|
| **Bild ist unscharf** | Erhöhen Sie `ocrEngine.Config.Dpi` (z. B. `ocrEngine.Config.Dpi = 300`) bevor Sie `RecognizeImage` aufrufen. |
| **Nicht‑englische Sprache** | Setzen Sie `ocrEngine.Config.Language = OcrLanguage.German` (oder eine andere unterstützte Sprache). |
| **Große Menge an Dateien** | Durchlaufen Sie ein Verzeichnis, wiederverwenden Sie dieselbe `OcrEngine`‑Instanz; speichern Sie jedes JSON‑Ergebnis unter einem eindeutigen Dateinamen. |
| **Nur hoch‑vertrauenswürdigen Text benötigen** | Filtern Sie `ocrResult.Lines`, bei denen `Confidence` ≥ 0.95 ist, bevor Sie serialisieren. |

## Vollständiges funktionierendes Beispiel (Copy‑Paste‑bereit)

Unten finden Sie das *gesamte* Programm, das Sie direkt in `Program.cs` einfügen können. Es enthält alle Schritte, Fehlerbehandlung und Kommentare, die den Code selbsterklärend machen.

```csharp
using Aspose.OCR;
using System;
using System.IO;
using System.Text.Json;

class JsonExportExample
{
    public static void Main()
    {
        // 👉 Step 1: Initialize the OCR engine.
        var ocrEngine = new OcrEngine();

        // 👉 Step 2: Path to the PNG image you want to process.
        string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "text.png");

        if (!File.Exists(imagePath))
        {
            Console.WriteLine($"Image not found at {imagePath}");
            return;
        }

        // 👉 Step 3: Perform OCR – this is where we **recognize png text**.
        var ocrResult = ocrEngine.RecognizeImage(imagePath);

        // 👉 Step 4: Validate the result.
        if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
        {
            Console.WriteLine("No recognizable text found. Try a clearer image or adjust DPI settings.");
            return;
        }

        // 👉 Step 5: Configure JsonSerializer to **write indented json**.
        var jsonOptions = new JsonSerializerOptions
        {
            WriteIndented = true // Pretty‑print the JSON.
        };

        // 👉 Step 6: Serialize the OCR result – this demonstrates **use jsonserializer c#**.
        string jsonOutput = JsonSerializer.Serialize(ocrResult, jsonOptions);

        // 👉 Step 7: Output to console (or write to a file).
        Console.WriteLine(jsonOutput);

        // Optional: Save to disk.
        string outputPath = Path.ChangeExtension(imagePath, ".json");
        File.WriteAllText(outputPath, jsonOutput);
        Console.WriteLine($"JSON saved to {outputPath}");
    }
}
```

Führen Sie den Code aus, prüfen Sie die Konsole oder die erzeugte `.json`‑Datei, und Sie sehen den extrahierten Text zusammen mit den Confidence‑Scores, alles sauber **eingebettet**.

## Fazit

Sie haben nun ein solides **c# ocr tutorial**, das zeigt, wie man **Text aus Bild c#** extrahiert, **png‑Text** erkennt und **eingebettetes json** mit `JsonSerializer` schreibt. Das Beispiel ist vollständig, ausführbar und enthält praxisnahe Tipps für reale Szenarien.  

Nächste Schritte? Ersetzen Sie Aspose.OCR durch eine andere Engine (z. B. Tesseract) und beobachten Sie, wie sich die Struktur von `OcrResult` ändert, oder leiten Sie das JSON an eine nachgelagerte API weiter, die OCR‑Daten in einer Datenbank speichert. Sie können außerdem mit **use jsonserializer c#**‑Optionen experimentieren, etwa benutzerdefinierte Converter für Datumsformatierung oder Enum‑Handhabung.

Viel Spaß beim Coden, und mögen Ihre OCR‑Pipelines stets präzise sein!  

---  

![c# ocr tutorial Diagramm](image.png "Diagramm, das den OCR‑Ablauf veranschaulicht")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}