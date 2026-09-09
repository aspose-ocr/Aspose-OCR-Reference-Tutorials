---
category: general
date: 2026-01-10
description: Erfahren Sie, wie Sie Text aus einem Bild erkennen, Textkoordinaten extrahieren
  und einen Beleg mit Aspose OCR in C# in JSON konvertieren. Schritt‑für‑Schritt‑Tutorial.
draft: false
keywords:
- recognize text from image
- how to extract text
- extract text coordinates
- convert receipt to json
language: de
og_description: Texterkennung aus Bild in C# mit Aspose OCR. Dieser Leitfaden zeigt,
  wie man Text extrahiert, Koordinaten erhält und Quittungen in JSON konvertiert.
og_title: Text aus Bild erkennen – Vollständiges C# OCR‑Tutorial
tags:
- OCR
- C#
- Aspose
title: Text aus Bild in C# erkennen – Vollständiger Leitfaden zu OCR und JSON
url: /de/net/text-recognition/recognize-text-from-image-in-c-complete-guide-to-ocr-and-jso/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Texterkennung aus Bild – Vollständiges C# OCR‑Tutorial

Haben Sie jemals Text aus einem Bild erkennen müssen, waren sich aber nicht sicher, welche Bibliothek Sie wählen sollten? Sie sind nicht allein. In vielen realen Anwendungen – Ausgaben‑Tracker, Beleg‑Scanner oder Dokumenten‑Archivierer – ist das zuverlässige Extrahieren von Text die erste Hürde.  

In diesem Tutorial führen wir Sie durch **how to extract text**, holen die Begrenzungsrahmen und schließlich **convert receipt to JSON** mit Aspose.OCR für .NET. Am Ende haben Sie ein eigenständiges C#‑Projekt, das ein Foto eines Belegs nimmt und eine übersichtliche JSON‑Datei mit Vertrauenswerten und Koordinaten ausgibt.

## Was Sie benötigen

- **.NET 6.0 SDK** (oder eine neuere Version). Ältere Frameworks funktionieren ebenfalls, aber .NET 6 ist der optimale Punkt für moderne Bibliotheken.
- **Visual Studio 2022** oder VS Code mit der C#‑Erweiterung.
- **Aspose.OCR for .NET** NuGet‑Paket (`Aspose.OCR` und `Aspose.OCR.Output`). Sie können es über die Package Manager Console installieren:

```powershell
Install-Package Aspose.OCR
Install-Package Aspose.OCR.Output
```

- Ein Beispiel‑Beleg‑Bild (z. B. `receipt.jpg`), das in einem Ordner abgelegt wird, auf den Sie später verweisen.

Das war's – keine zusätzlichen SDKs, keine nativen Binärdateien, nur reiner verwalteter Code.

## Schritt 1: Neues Konsolenprojekt erstellen

Zuerst einmal ein Konsolen‑App erstellen. Das ist der schnellste Weg, OCR ohne UI‑Overhead zu testen.

```csharp
// Program.cs
using System;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll fill this in later.
        }
    }
}
```

> **Pro‑Tipp:** Halten Sie den Projektordner aufgeräumt; erstellen Sie einen Unterordner namens `Resources` und legen Sie dort `receipt.jpg` ab. Das macht die Pfadbehandlung mühelos.

## Schritt 2: Beleg‑Bild laden

Jetzt führen wir tatsächlich **recognize text from image** aus. Der erste Schritt besteht darin, die OCR‑Engine auf die Datei zu richten.

```csharp
// Inside Main()
string imagePath = @"Resources/receipt.jpg";
if (!System.IO.File.Exists(imagePath))
{
    Console.WriteLine($"❌ Image not found at {imagePath}");
    return;
}

// Initialise the OCR engine
OcrEngine ocrEngine = new OcrEngine
{
    Image = ImageStream.FromFile(imagePath)
};

Console.WriteLine("✅ Image loaded successfully.");
```

Warum wickeln wir das Laden in eine einfache Existenzprüfung? Weil Sie in der Produktion häufig mit Benutzer‑Uploads zu tun haben, die fehlen oder beschädigt sein können. Das frühzeitige Erkennen des Problems erspart Ihnen später kryptische Ausnahmen.

## Schritt 3: OCR ausführen – **recognize text from image**

Mit dem Bild im Speicher lassen wir Aspose **recognize text from image**. Dieser Vorgang ist synchron und liefert ein umfangreiches Ergebnis‑Set.

```csharp
// Still inside Main()
try
{
    ocrEngine.Recognize();
    Console.WriteLine("🧠 OCR completed.");
}
catch (Exception ex)
{
    Console.WriteLine($"❗ OCR failed: {ex.Message}");
    return;
}
```

Im Hintergrund führt Aspose ein neuronales Netzwerk aus, das auf Millionen von Zeichen trainiert wurde. Die Engine füllt `ocrEngine.Text`, `ocrEngine.RecognitionResult` und eine Sammlung von `OcrRegion`‑Objekten, die Koordinaten enthalten. Genau das benötigen wir für den nächsten Schritt.

## Schritt 4: **How to extract text** – Roh‑String erhalten

Wenn Sie nur am reinen Text interessiert sind (vielleicht für eine schnelle Suche), können Sie ihn direkt aus der Engine holen:

```csharp
string plainText = ocrEngine.Text;
Console.WriteLine("\n--- Extracted Text ---");
Console.WriteLine(plainText);
```

Sie werden Zeilenumbrüche dort sehen, wo die OCR Absatzgrenzen erkannt hat. In vielen Beleg‑Scanning‑Szenarien reicht der Roh‑String aus, um Summen, Daten oder Händlernamen mit einfachen Regexes zu extrahieren.

## Schritt 5: **extract text coordinates** – Begrenzungsrahmen für jedes Wort

Oft müssen Sie wissen, *wo* auf dem Bild ein bestimmter Textabschnitt liegt – zum Beispiel, um den Gesamtbetrag in einer UI hervorzuheben. Aspose liefert das über `OcrRegion`‑Objekte.

```csharp
Console.WriteLine("\n--- Text Coordinates (extract text coordinates) ---");
foreach (var region in ocrEngine.RecognitionResult.Regions)
{
    // Each region represents a word or a line depending on the engine settings.
    string word = region.Text;
    var bounds = region.BoundingBox; // X, Y, Width, Height
    Console.WriteLine($"Word: \"{word}\" | Box: X={bounds.X}, Y={bounds.Y}, W={bounds.Width}, H={bounds.Height}");
}
```

Beachten Sie, dass wir über **extract text coordinates** für jedes erkannte Segment iterieren. Die Koordinaten sind relativ zum Originalbild, sodass Sie sie in einer Grafik‑Canvas oder einem HTML‑`<canvas>`‑Element überlagern können.

## Schritt 6: **convert receipt to JSON** – Detaillierte Ergebnisse speichern

Jetzt kommt der Teil, der alles zusammenführt: Wir wollen eine maschinenlesbare Struktur, die den Text, Vertrauenswerte und die Begrenzungsrahmen enthält. Aspose liefert `JsonSaveOptions`, die das zum Kinderspiel machen.

```csharp
// Define where the JSON will be saved
string jsonPath = @"Resources/receipt.json";

// Configure JSON options to keep confidence and bounding boxes
JsonSaveOptions jsonOptions = new JsonSaveOptions
{
    IncludeConfidence = true,
    IncludeBoundingBoxes = true
};

// Save the OCR result
ocrEngine.Save(jsonPath, jsonOptions);
Console.WriteLine($"\n💾 Detailed OCR results saved to {jsonPath}");
```

Die resultierende Datei sieht etwa so aus (gekürzt für die Übersicht):

```json
{
  "Regions": [
    {
      "Text": "Store",
      "Confidence": 0.99,
      "BoundingBox": { "X": 45, "Y": 120, "Width": 80, "Height": 20 }
    },
    {
      "Text": "Total",
      "Confidence": 0.97,
      "BoundingBox": { "X": 300, "Y": 560, "Width": 70, "Height": 22 }
    }
    // ... more regions ...
  ]
}
```

Sie haben jetzt ein **convert receipt to JSON**‑Artefakt, das in nachgelagerte Dienste eingespeist werden kann – denken Sie an Expense‑Report‑APIs, Analyse‑Pipelines oder sogar eine einfache UI, die Rechtecke um jedes Wort zeichnet.

## Vollständiges funktionierendes Beispiel

Wenn wir alle Teile zusammenfügen, finden Sie hier das komplette `Program.cs`, das Sie in Ihr Projekt kopieren können:

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣ Load the image
            // -------------------------------------------------
            string imagePath = @"Resources/receipt.jpg";
            if (!System.IO.File.Exists(imagePath))
            {
                Console.WriteLine($"❌ Image not found at {imagePath}");
                return;
            }

            OcrEngine ocrEngine = new OcrEngine
            {
                Image = ImageStream.FromFile(imagePath)
            };
            Console.WriteLine("✅ Image loaded.");

            // -------------------------------------------------
            // 2️⃣ Run OCR – recognize text from image
            // -------------------------------------------------
            try
            {
                ocrEngine.Recognize();
                Console.WriteLine("🧠 OCR completed.");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"❗ OCR failed: {ex.Message}");
                return;
            }

            // -------------------------------------------------
            // 3️⃣ Extract plain text (how to extract text)
            // -------------------------------------------------
            Console.WriteLine("\n--- Extracted Text ---");
            Console.WriteLine(ocrEngine.Text);

            // -------------------------------------------------
            // 4️⃣ Get coordinates (extract text coordinates)
            // -------------------------------------------------
            Console.WriteLine("\n--- Text Coordinates ---");
            foreach (var region in ocrEngine.RecognitionResult.Regions)
            {
                var box = region.BoundingBox;
                Console.WriteLine($"Word: \"{region.Text}\" | Box: X={box.X}, Y={box.Y}, W={box.Width}, H={box.Height}");
            }

            // -------------------------------------------------
            // 5️⃣ Save detailed JSON (convert receipt to json)
            // -------------------------------------------------
            string jsonPath = @"Resources/receipt.json";
            JsonSaveOptions jsonOptions = new JsonSaveOptions
            {
                IncludeConfidence = true,
                IncludeBoundingBoxes = true
            };
            ocrEngine.Save(jsonPath, jsonOptions);
            Console.WriteLine($"\n💾 JSON saved at {jsonPath}");
        }
    }
}
```

Führen Sie das Programm (`dotnet run`) aus und beobachten Sie die Konsolenausgabe. Öffnen Sie `Resources/receipt.json`, um die Struktur zu überprüfen.

## Häufige Fragen & Sonderfälle

- **What if the image is blurry?**  
  Aspose OCR funktioniert am besten mit 300 dpi oder höher. Wenn Sie niedrige Vertrauenswerte erhalten, sollten Sie vor dem Übergeben des Bildes an die Engine einen Schärfungsfilter anwenden.

- **Can I recognize multiple languages?**  
  Ja. Setzen Sie `ocrEngine.Language = Language.English | Language.Spanish;` bevor Sie `Recognize()` aufrufen.

- **How do I limit output to only numbers (e.g., totals)?**  
  Nachdem Sie den reinen Text haben, führen Sie ein Regex wie `\d+\.\d{2}` auf `ocrEngine.Text` aus. Da wir bereits Koordinaten besitzen, können Sie die gefundene Zeichenkette zurück zu ihrer Region für visuelle Hervorhebung zuordnen.

- **Is the JSON format customizable?**  
  Die Klasse `JsonSaveOptions` stellt einige Flags bereit. Wenn Sie ein völlig benutzerdefiniertes Schema benötigen, können Sie über `ocrEngine.RecognitionResult.Regions` iterieren und die Objekte selbst mit `System.Text.Json` serialisieren.

## Fazit

Wir haben gerade gezeigt, wie man **recognize text from image** in C# mit Aspose.OCR durchführt, **how to extract text**, **extract text coordinates** abruft und schließlich **convert receipt to JSON**. Der gesamte Ablauf befindet sich in einer einzigen, leicht auszuführenden Konsolen‑App, was ihn perfekt für Prototypen oder als Baustein in größeren Systemen macht.

Nächste Schritte? Versuchen Sie, das JSON in ein Front‑End zu speisen, das die Begrenzungsrahmen zeichnet, oder schließen Sie die Ausgabe an einen Expense‑Report‑Dienst an. Sie können auch mit verschiedenen Bildformaten (PNG, TIFF) experimentieren oder einen Ordner mit Belegen stapelweise verarbeiten.

Haben Sie weitere Fragen zu OCR, Aspose oder JSON‑Verarbeitung? Hinterlassen Sie unten einen Kommentar, und viel Spaß beim Coden! 

![Belegbildbeispiel für recognize text from image](receipt.jpg "Belegbildbeispiel")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}