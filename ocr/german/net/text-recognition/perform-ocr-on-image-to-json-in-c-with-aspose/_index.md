---
category: general
date: 2026-04-08
description: Erfahren Sie, wie Sie OCR auf Bildern durchführen und JSON‑Dateien in
  C# mit Aspose OCR schreiben. Dieses Aspose OCR C#‑Tutorial zeigt die OCR‑Bild‑zu‑JSON‑Konvertierung
  mit Vertrauenswerten.
draft: false
keywords:
- perform OCR on image
- write JSON file C#
- OCR image to JSON
- Aspose OCR C# tutorial
language: de
og_description: Führen Sie OCR auf einem Bild durch und exportieren Sie die Ergebnisse
  in eine JSON‑Datei in C#. Dieses Tutorial behandelt den vollständigen Aspose OCR
  C#‑Workflow, einschließlich der Konfidenzwerte.
og_title: OCR auf Bild zu JSON in C# ausführen – Aspose OCR‑Leitfaden
tags:
- Aspose
- OCR
- C#
- JSON
title: OCR auf Bild zu JSON in C# mit Aspose durchführen
url: /de/net/text-recognition/perform-ocr-on-image-to-json-in-c-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR auf Bild zu JSON in C# mit Aspose

Haben Sie schon einmal **OCR auf Bild**‑Dateien durchführen wollen, waren sich aber nicht sicher, wie Sie die Ergebnisse in ein strukturiertes Format bringen? Sie sind nicht allein – Entwickler fragen ständig: „Wie verwandle ich ein gescanntes Bild in nutzbare Daten?“ Die gute Nachricht: Aspose.OCR macht das kinderleicht, und Sie können sogar **JSON‑Datei C#**‑stil schreiben, inklusive Confidence‑Werten.

In diesem Leitfaden gehen wir Schritt für Schritt durch ein komplettes **aspose OCR C# tutorial**, das alles abdeckt – vom Laden eines Bildes bis zum Export des erkannten Textes als JSON. Am Ende haben Sie eine lauffähige Konsolen‑App, die **OCR auf Bild** ausführt, die Ausgabe in JSON (inklusive Confidence‑Werten) konvertiert und mit einer einzigen Code‑Zeile speichert. Keine versteckten Schritte, keine externen Skripte – reines C#.

## Voraussetzungen

Bevor wir starten, stellen Sie sicher, dass Sie Folgendes haben:

- .NET 6.0 SDK oder neuer (der Code funktioniert auch mit .NET Core und .NET Framework)
- Visual Studio 2022 (oder ein beliebiger Editor Ihrer Wahl)
- Eine gültige **Aspose.OCR for .NET**‑Lizenz oder eine kostenlose temporäre Lizenz (die kostenlose Testversion reicht für Tests)
- Eine Bilddatei (`input.png`), die Sie verarbeiten möchten (jedes gängige Format – PNG, JPG, BMP – ist geeignet)

Das war’s. Wenn Ihnen etwas fehlt, holen Sie es jetzt; der Rest des Tutorials geht davon aus, dass alles bereits vorhanden ist.

## Schritt 1: Das Aspose.OCR‑NuGet‑Paket installieren

Zuerst das Bibliothekspaket zum Projekt hinzufügen. Öffnen Sie ein Terminal im Projektordner und führen Sie aus:

```bash
dotnet add package Aspose.OCR
```

Damit wird die neueste Version (Stand April 2026 ist das 23.12) heruntergeladen und die benötigten DLLs in den `bin`‑Ordner kopiert. Keine zusätzliche Konfiguration nötig.

## Schritt 2: Die OCR‑Engine initialisieren (OCR auf Bild ausführen)

Jetzt erstellen wir eine `OcrEngine`‑Instanz und geben ihr die gewünschte Sprache an. Englisch (`"en"`) ist am häufigsten, Sie können sie aber durch `"fr"`, `"de"` oder jede andere unterstützte Sprache ersetzen.

```csharp
using Aspose.Ocr;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // Path to your input image – change as needed
        string inputPath = Path.Combine(Environment.CurrentDirectory, "input.png");
        // Path where the JSON will be saved
        string outputPath = Path.Combine(Environment.CurrentDirectory, "output.json");

        // Step 2: Initialize the OCR engine – this is where we **perform OCR on image**
        var ocrEngine = new OcrEngine
        {
            Language = "en"               // Set language; you can use ISO‑639‑1 codes
        };

        // Optional: tweak recognition options (speed vs. accuracy)
        // ocrEngine.RecognitionMode = RecognitionMode.LargeText; // Uncomment for large blocks
```

**Warum wir hier initialisieren:** Die `OcrEngine` enthält alle Konfigurationen, die für den Erkennungsprozess nötig sind. Die Sprache im Vorfeld festzulegen sorgt dafür, dass die Engine den richtigen Zeichensatz verwendet, was die Genauigkeit erheblich steigert.

## Schritt 3: Das Bild erkennen und Confidence erfassen

Mit der bereitstehenden Engine übergeben wir ihr die Bilddatei. Die Methode `RecognizeImage` liefert ein `OcrResult`‑Objekt, das sowohl den extrahierten Text als auch einen Confidence‑Wert für jedes Wort enthält.

```csharp
        // Step 3: Perform OCR on the image file
        OcrResult ocrResult = ocrEngine.RecognizeImage(inputPath);

        // Verify that the result is not null
        if (ocrResult == null)
        {
            Console.WriteLine("OCR failed – check the file path and format.");
            return;
        }

        // For debugging: print the plain text to the console
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
```

**Was passiert im Hintergrund?** Aspose nutzt einen neuronalen Netzwerk‑basierten Erkenner, der jeden Pixel‑Block analysiert, ihn mit seinem Sprachmodell abgleicht und einen Confidence‑Wert (0‑100) anhängt, der angibt, wie sicher die Erkennung für jedes Wort ist.

## Schritt 4: Das Ergebnis in JSON konvertieren (OCR Bild zu JSON)

Aspose macht die Konvertierung mühelos. Durch das Setzen von `includeConfidence: true` erhalten wir ein JSON‑Payload, das etwa so aussieht:

```json
{
  "Text": "Hello world",
  "Words": [
    { "Value": "Hello", "Confidence": 97.3 },
    { "Value": "world", "Confidence": 95.8 }
  ]
}
```

Hier der Code, der den JSON‑String erzeugt:

```csharp
        // Step 4: Convert OCR result to JSON, including confidence values
        string jsonResult = ocrResult.ToJson(includeConfidence: true);
```

**Warum Confidence einbeziehen?** Wenn Sie die Daten in nachgelagerte Prozesse einspeisen (z. B. Validierung, UI‑Hervorhebung), hilft Ihnen das Wissen, welche Wörter unsicher sind, zu entscheiden, ob Sie den Nutzer um Bestätigung bitten sollten.

## Schritt 5: Die JSON‑Datei C#‑stil schreiben

Jetzt schreiben wir tatsächlich **JSON file C#**. Die Methode `File.WriteAllText` ist atomar und plattformübergreifend, ideal für Konsolen‑Apps.

```csharp
        // Step 5: Save the JSON output to a file
        File.WriteAllText(outputPath, jsonResult);
        Console.WriteLine($"✅ JSON with confidence saved to: {outputPath}");
    }
}
```

Das ist der komplette Ablauf – fünf knappe Schritte, die **OCR auf Bild** ausführen, die Ausgabe nach JSON umwandeln und persistieren.

## Vollständiges Beispiel

Unten finden Sie das komplette Programm, das Sie in `Program.cs` einfügen können. Stellen Sie sicher, dass `input.png` im selben Ordner wie die kompilierte Binärdatei liegt oder passen Sie die Pfade entsprechend an.

```csharp
using Aspose.Ocr;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // -------------------------------------------------------
        // 1️⃣ Set up file locations (feel free to change paths)
        // -------------------------------------------------------
        string inputPath = Path.Combine(Environment.CurrentDirectory, "input.png");
        string outputPath = Path.Combine(Environment.CurrentDirectory, "output.json");

        // -------------------------------------------------------
        // 2️⃣ Initialize the OCR engine – this is where we **perform OCR on image**
        // -------------------------------------------------------
        var ocrEngine = new OcrEngine
        {
            Language = "en" // English – replace with "fr", "es", etc. as needed
        };

        // -------------------------------------------------------
        // 3️⃣ Recognize the image and obtain confidence values
        // -------------------------------------------------------
        OcrResult ocrResult = ocrEngine.RecognizeImage(inputPath);

        if (ocrResult == null)
        {
            Console.WriteLine("❌ OCR failed – verify the image path and format.");
            return;
        }

        // Show plain text (optional)
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
        Console.WriteLine();

        // -------------------------------------------------------
        // 4️⃣ Convert the result to JSON – **OCR image to JSON**
        // -------------------------------------------------------
        string jsonResult = ocrResult.ToJson(includeConfidence: true);

        // -------------------------------------------------------
        // 5️⃣ Write the JSON file – **write JSON file C#** style
        // -------------------------------------------------------
        File.WriteAllText(outputPath, jsonResult);
        Console.WriteLine($"✅ JSON with confidence saved to: {outputPath}");
    }
}
```

### Erwartete Ausgabe

Wenn Sie das Programm (`dotnet run`) ausführen, sehen Sie etwa Folgendes:

```
=== Extracted Text ===
Hello world

✅ JSON with confidence saved to: C:\YourProject\output.json
```

Und `output.json` enthält das zuvor gezeigte strukturierte JSON, komplett mit Confidence‑Prozenten für jedes Wort.

## Profi‑Tipps & Sonderfälle

- **Fehlende Datei behandeln:** Wickeln Sie den Aufruf von `RecognizeImage` in ein `try/catch` für `FileNotFoundException`, wenn Sie dynamische Pfade erwarten.
- **Verschiedene Sprachen:** Setzen Sie `ocrEngine.Language = "fr"` für Französisch oder laden Sie ein benutzerdefiniertes Sprachpaket via `ocrEngine.LoadLanguage("custom.lang")`.
- **Große Dokumente:** Für mehrseitige PDFs zuerst jede Seite in ein Bild konvertieren (z. B. mit `Aspose.PDF`) und dann die OCR‑Schritte in einer Schleife ausführen.
- **Performance‑Optimierung:** Wenn Sie schnelle Ergebnisse benötigen, wechseln Sie zu `RecognitionMode.Fast` – Sie verlieren etwas Genauigkeit, gewinnen aber Geschwindigkeit.
- **JSON‑Formatierung:** Möchten Sie hübsch formatiertes JSON? Nutzen Sie `JsonConvert.SerializeObject` aus Newtonsoft mit `Formatting.Indented` nach dem Deserialisieren des Aspose‑JSON‑Strings.

## Häufig gestellte Fragen

**Q: Funktioniert das mit .NET Framework?**  
A: Absolut. Das gleiche NuGet‑Paket zielt auf .NET Standard 2.0, sodass Sie es von .NET Framework 4.6.1 und neuer referenzieren können.

**Q: Was, wenn ich die Confidence für das gesamte Dokument statt pro Wort brauche?**  
A: Das `OcrResult` stellt zudem `OverallConfidence` bereit. Sie können diesen Wert manuell zum JSON hinzufügen:

```csharp
var customObj = new
{
    Text = ocrResult.Text,
    OverallConfidence = ocrResult.OverallConfidence,
    Words = ocrResult.Words
};
string json = JsonConvert.SerializeObject(customObj, Formatting.Indented);
```

**Q: Kann ich das JSON direkt an eine Web‑API streamen?**  
A: Ja. Ersetzen Sie `File.WriteAllText` durch einen `HttpClient`‑POST, der `jsonResult` sendet.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}