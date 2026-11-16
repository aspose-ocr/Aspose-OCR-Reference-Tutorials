---
category: general
date: 2026-03-26
description: Erkennen Sie Text aus PNG und extrahieren Sie Belegdaten mit Aspose OCR
  in C#. Konvertieren Sie das Bild in JSON‑L und verarbeiten Sie den Beleg mit OCR
  in einem vollständigen Beispiel.
draft: false
keywords:
- recognize text from png
- extract text from receipt
- convert image to jsonl
- process receipt with ocr
- aspose ocr example c#
language: de
og_description: Texterkennung aus PNG und Umwandlung von Belegen in JSON‑L mit Aspose
  OCR in C#. Vollständiger Schritt‑für‑Schritt‑Code und Tipps.
og_title: Text aus PNG erkennen – Aspose OCR C#‑Leitfaden
tags:
- Aspose OCR
- C#
- JSONL
- Receipt Processing
title: Text aus PNG erkennen – Aspose OCR C# JSON‑L‑Tutorial
url: /de/net/text-recognition/recognize-text-from-png-aspose-ocr-c-json-l-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Texterkennung aus PNG – Vollständiger Aspose OCR C# Leitfaden

Haben Sie jemals **Texte aus PNG**-Dateien erkennen müssen, waren sich aber nicht sicher, welche Bibliothek Ihnen saubere, zeilenweise Ergebnisse liefert? Sie sind nicht allein. In vielen Kleinunternehmens‑Apps liegt der Beleg als PNG‑Bild vor, und das Extrahieren von Betrag, Datum oder Händlernamen ist ein tägliches Problem.  

Die gute Nachricht? Mit ein paar Zeilen C# und der **Aspose OCR**‑Bibliothek können Sie **Texte aus dem Beleg extrahieren**, dann **Bild in JSONL konvertieren** für nachgelagerte Analysen. In diesem Tutorial führen wir Sie durch die gesamte Pipeline – Laden eines PNG, Ausführen von OCR und Schreiben jeder Zeile in eine JSON‑L‑Datei – sodass Sie sofort **Belege mit OCR verarbeiten** können.

Wir decken alles ab, was Sie benötigen: erforderliche NuGet‑Pakete, ein vollständiges ausführbares Programm, Erklärungen, warum jeder Schritt wichtig ist, und eine Handvoll praktischer Tipps, die Sie zu schätzen wissen werden, wenn die Belege unordentlich werden. Keine externe Dokumentation nötig; einfach kopieren‑einfügen, ausführen und anpassen.

---

## Was Sie lernen werden

- How to **Texte aus PNG erkennen** using `Aspose.OCR`.
- How to **Texte aus dem Beleg extrahieren** line objects and capture confidence scores.
- How to **Bild in JSONL konvertieren** so each OCR line becomes a separate JSON object.
- How to **Beleg mit OCR verarbeiten** end‑to‑end, handling edge cases like empty images or low‑confidence lines.
- Tips for troubleshooting common OCR hiccups and improving accuracy.

### Voraussetzungen

- .NET 6.0 oder höher (der Code funktioniert auch mit .NET Core und .NET Framework).
- Visual Studio 2022 oder jede IDE Ihrer Wahl.
- Eine gültige Aspose OCR‑Lizenz (Sie können mit einer kostenlosen temporären Lizenz von Aspose.com beginnen).
- Ein Beispielbeleg, gespeichert als `receipt.png` in einem Ordner Ihrer Wahl.

---

## Schritt 1: Texterkennung aus PNG mit Aspose OCR

Das Erste, was wir benötigen, ist ein initialisierter `OcrEngine`. Dieses Objekt enthält die OCR‑Engine‑Einstellungen (Sprache, Erkennungsmodus usw.). Standardmäßig verwendet es Englisch und erkennt das Seitenlayout automatisch, was für die meisten Belege gut funktioniert.

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;
using System;
using System.IO;

class JsonLExample
{
    static void Main()
    {
        // Initialize the OCR engine – this is where Aspose loads its models.
        OcrEngine ocrEngine = new OcrEngine();

        // Load the PNG image that contains the receipt.
        string imagePath = @"YOUR_DIRECTORY\receipt.png";
        OcrImage receiptImage = OcrImage.FromFile(imagePath);

        // Run OCR and get the result object.
        OcrResult ocrResult = ocrEngine.Recognize(receiptImage);
```

**Warum das wichtig ist:**  
`OcrEngine` ist die leistungshungrige Komponente; wenn Sie sie einmal erstellen und über viele Bilder hinweg wiederverwenden, reduziert das den Speicherverbrauch. Wenn Sie eine andere Sprache benötigen (z. B. spanische Belege), können Sie `ocrEngine.Language = OcrLanguage.Spanish;` setzen, bevor Sie `Recognize` aufrufen.

---

## Schritt 2: Texte aus Belegzeilen extrahieren

`OcrResult` enthält eine Sammlung namens `Lines`. Jede Zeile enthält den Rohtext und einen Vertrauenswert (0‑100). Das Herausziehen ermöglicht Ihnen eine feinkörnige Kontrolle – Sie können Zeilen mit geringer Vertrauenswürdigkeit verwerfen oder für eine manuelle Überprüfung markieren.

```csharp
        // Prepare to write each line as a JSON‑L record.
        string jsonlPath = @"YOUR_DIRECTORY\receipt.jsonl";

        using (StreamWriter jsonLineWriter = new StreamWriter(jsonlPath))
        {
            foreach (var line in ocrResult.Lines)
            {
                // Build a simple JSON object for the line.
                string json = $"{{\"text\":\"{EscapeJson(line.Text)}\",\"confidence\":{line.Confidence}}}";
                jsonLineWriter.WriteLine(json);
            }
        }

        Console.WriteLine("JSON‑L file written to " + jsonlPath);
    }

    // Helper to escape quotes and backslashes in JSON strings.
    private static string EscapeJson(string s) => s.Replace("\\", "\\\\").Replace("\"", "\\\"");
}
```

**Warum wir JSON escapen:**  
Belegtext kann Anführungszeichen (`"`) oder Backslashes (`\`) enthalten, die einen naiven JSON‑String zerstören würden. Die Methode `EscapeJson` garantiert eine gültige JSON‑Zeile.

**Wie die Ausgabe aussieht:**  

```
{"text":"Store XYZ","confidence":98.5}
{"text":"Date: 2024-07-15","confidence":97.2}
{"text":"Total $23.45","confidence":99.1}
```

Jede Zeile ist ein separater Datensatz, ideal zum Streamen in einen Data Lake oder zum Einspeisen in ein Machine‑Learning‑Modell.

---

## Schritt 3: Bild in JSONL konvertieren – Umgang mit Randfällen

Wenn Sie einen Stapel von Belegen verarbeiten, können einige Bilder leer, beschädigt oder mit extrem niedrigen Vertrauenswerten sein. Lassen Sie uns die Pipeline etwas robuster machen.

```csharp
        // After OCR, check if any lines were detected.
        if (ocrResult.Lines.Count == 0)
        {
            Console.WriteLine("Warning: No text detected. Verify the image path and quality.");
            return;
        }

        // Optional: filter out lines with confidence below a threshold.
        const double minConfidence = 80.0;
        foreach (var line in ocrResult.Lines)
        {
            if (line.Confidence < minConfidence)
                continue; // skip noisy line
            // write as before...
        }
```

**Warum filtern:**  
Auf verblasstem Papier gedruckte Belege können Zeichen mit niedriger Vertrauenswürdigkeit erzeugen. Das Entfernen von allem unter 80 % beseitigt in der Regel das Rauschen und behält die nützlichen Daten.

---

## Schritt 4: Beleg mit OCR verarbeiten – End‑to‑End‑Beispiel

Alles zusammengeführt, hier das **vollständige, sofort ausführbare** Programm. Ersetzen Sie `YOUR_DIRECTORY` durch den Ordner, der Ihre PNG‑Datei enthält.

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;
using System;
using System.IO;

class JsonLExample
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Load receipt PNG
        string imagePath = @"YOUR_DIRECTORY\receipt.png";
        OcrImage receiptImage = OcrImage.FromFile(imagePath);

        // 3️⃣ Perform OCR
        OcrResult ocrResult = ocrEngine.Recognize(receiptImage);

        // 4️⃣ Verify we got something back
        if (ocrResult.Lines.Count == 0)
        {
            Console.WriteLine("❗ No text found – check the image quality.");
            return;
        }

        // 5️⃣ Write each line to a JSON‑L file
        string jsonlPath = @"YOUR_DIRECTORY\receipt.jsonl";
        using (StreamWriter writer = new StreamWriter(jsonlPath))
        {
            const double minConfidence = 80.0;
            foreach (var line in ocrResult.Lines)
            {
                if (line.Confidence < minConfidence) continue; // skip low‑confidence

                string json = $"{{\"text\":\"{EscapeJson(line.Text)}\",\"confidence\":{line.Confidence}}}";
                writer.WriteLine(json);
            }
        }

        Console.WriteLine($"✅ JSON‑L written to: {jsonlPath}");
    }

    // Helper to make JSON safe
    private static string EscapeJson(string s) => s.Replace("\\", "\\\\").Replace("\"", "\\\"");
}
```

**Ausführen des Codes:**  
1. Öffnen Sie ein Terminal im Projektordner.  
2. `dotnet add package Aspose.OCR` – installiert die Bibliothek.  
3. `dotnet run` – Sie sollten die Erfolgsmeldung sehen und eine `receipt.jsonl`‑Datei erscheint.

**Erwartetes Ergebnis:** Eine zeilenweise getrennte JSON‑Datei, bei der jede Zeile einer Belegzeile entspricht, inklusive Vertrauenswerten. Sie können diese Datei nun in Power BI, Elastic oder jedes Analyse‑Tool, das JSON‑L versteht, einspeisen.

---

## Häufige Fallstricke & Pro‑Tipps

| Issue | Why it Happens | Quick Fix |
|-------|----------------|-----------|
| **Leere Ausgabe** | Bildpfad falsch oder Datei ist kein PNG. | Pfad überprüfen, `File.Exists(imagePath)` verwenden. |
| **Fehlerhafte Zeichen** | Niedrige DPI oder stark komprimiertes PNG. | Mindestens 300 dpi Scans verwenden; aggressive JPEG‑Kompression vermeiden. |
| **Zu viele Zeilen mit niedriger Vertrauenswürdigkeit** | Beleg auf Thermopapier mit Verblassen gedruckt. | `minConfidence`‑Schwelle erhöhen oder Bild vorverarbeiten (Kontrast/Schwellenwert). |
| **JSON‑Parsing‑Fehler** | Nicht escapte Anführungszeichen im Belegtext. | `EscapeJson`‑Hilfsfunktion beibehalten oder zu `System.Text.Json` für robuste Serialisierung wechseln. |

**Pro‑Tipp:** Wenn Sie bestimmte Felder extrahieren müssen (z. B. Gesamtbetrag), führen Sie ein einfaches Regex auf jedem `line.Text` aus, nachdem Sie die JSON‑L‑Datei haben. Das hält OCR getrennt von der Geschäftslogik und erleichtert das Debuggen.

---

## Erweiterung der Lösung

- **Batchverarbeitung:** Wickeln Sie die `Main`‑Logik in ein `foreach` über alle PNG‑Dateien in einem Verzeichnis.
- **Mehrsprachige Unterstützung:** Setzen Sie `ocrEngine.Language = OcrLanguage.Spanish;` (oder jede unterstützte Sprache) vor `Recognize`.
- **Strukturierte Ausgabe:** Anstatt zeilenweiser JSON, erstellen Sie ein `Receipt`‑Objekt mit den Eigenschaften `Date`, `Merchant`, `Total` und serialisieren es einmal.

All diese Varianten **Bild in JSONL konvertieren** im Kern, sodass Sie den nachgelagerten Verbraucher austauschen können, ohne den OCR‑Teil zu ändern.

---

## Fazit

Wir haben Ihnen gerade gezeigt, wie Sie **Texte aus PNG**‑Dateien mit Aspose OCR **extrahieren**, **Texte aus dem Beleg extrahieren** und **Bild in JSONL konvertieren** für eine einfache nachgelagerte Verarbeitung. Das vollständige, eigenständige C#‑Programm demonstriert den gesamten Workflow – vom Laden eines PNG, über den Umgang mit Randfällen, bis zum Schreiben einer sauberen JSON‑L‑Datei – sodass Sie sofort **Belege mit OCR verarbeiten** können.

Probieren Sie es mit ein paar Beispielbelegen aus, passen Sie die Vertrauensschwelle an, und Sie werden sehen, wie schnell ein unordentlicher Stapel Bilder in strukturierte Daten für Analysen umgewandelt wird. Sobald Sie sich sicher fühlen, erkunden Sie die Batch‑Verarbeitung oder fügen Sie ein kleines ML‑Modell hinzu, das Ausgabenkategorien automatisch klassifiziert.

Haben Sie Fragen oder eine clevere Optimierung entdeckt? Hinterlassen Sie unten einen Kommentar – happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}