---
category: general
date: 2026-04-04
description: Erfahren Sie, wie Sie Text aus TIFF‑Dateien mit einem OCR‑Engine‑Beispiel
  in C# extrahieren. Schritt‑für‑Schritt‑Anleitung mit JSON‑ und XML‑Ausgabe.
draft: false
keywords:
- extract text from tiff
- ocr engine example
- Aspose OCR C#
- multi‑page TIFF OCR
- JSON OCR result
language: de
og_description: Text aus TIFF‑Dateien mit einer OCR‑Engine extrahieren – Beispiel
  in C#. Detaillierte Schritte, vollständiger Code und Tipps für JSON/XML‑Ausgabe.
og_title: Text aus TIFF mit Aspose OCR‑Engine extrahieren – Vollständige Anleitung
tags:
- C#
- OCR
- Aspose
- Image Processing
title: Text aus TIFF mit Aspose OCR‑Engine extrahieren – komplettes Beispiel
url: /de/net/text-recognition/extract-text-from-tiff-with-aspose-ocr-engine-complete-examp/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Text aus TIFF extrahieren – Vollständiges OCR‑Engine‑Beispiel in C#

Haben Sie jemals **Text aus TIFF**‑Bildern extrahieren müssen, waren sich aber nicht sicher, welche Bibliothek mehrseitige Dateien ohne ein Flickwerk von Workarounds verarbeiten kann? Sie sind nicht allein. In vielen Altsystemen kommen Dokumente als mehrseitige TIFF‑Scans an, und das Herausziehen des Rohtexts ist eine unverzichtbare Funktion für Suche, Compliance oder Daten‑Entry‑Automatisierung.

Die gute Nachricht? Mit Aspose OCR können Sie das in ein paar Zeilen erledigen – ohne mit Low‑Level‑Pixel‑Puffern zu hantieren. Dieses Tutorial führt Sie durch ein **komplettes OCR‑Engine‑Beispiel**, das ein mehrseitiges TIFF lädt, jede Seite erkennt und sowohl hübsch formatiertes JSON als auch optionales XML ausgibt. Am Ende haben Sie eine sofort ausführbare C#‑Konsolen‑App, die Text aus TIFF‑Dateien in Sekunden extrahiert.

## Was Sie lernen werden

- Wie Sie die Aspose OCR‑Engine in einem .NET‑Projekt einrichten.  
- Den genauen Code, um **Text aus TIFF**‑Dateien zu **extrahieren**, inklusive Mehrseiten‑Verarbeitung.  
- Warum Sie JSON statt XML wählen könnten und wie Sie beide erzeugen.  
- Tipps zur Fehlersuche bei gängigen Stolperfallen (z. B. Bild‑DPI, Speicherverbrauch).  

### Voraussetzungen

- .NET 6.0 SDK oder höher (der Code funktioniert mit .NET Core und .NET Framework).  
- Eine gültige Aspose OCR‑Lizenz (oder ein kostenloser Testschlüssel).  
- Visual Studio 2022 oder ein beliebiger C#‑Editor Ihrer Wahl.  
- Eine Beispiel‑Mehrseiten‑TIFF‑Datei (im Beispiel `multi-page.tiff` genannt).  

> **Pro‑Tipp:** Wenn Sie ein knappes Budget haben, lässt Sie die kostenlose Testversion trotzdem Text aus bis zu 100 Seiten pro Monat extrahieren – perfekt zum Testen.

---

## Schritt 1 – OCR‑Engine initialisieren (ocr engine example)

Bevor wir **Text aus TIFF** extrahieren können, benötigen wir eine Instanz der OCR‑Engine. Dieses Objekt enthält alle Konfigurationen, die Sie später (Sprache, Auflösung usw.) anpassen können.

```csharp
using Aspose.OCR;
using System.IO;

// Create a new OCR engine – this is the core of our ocr engine example
var ocrEngine = new OcrEngine();

// Optional: set language if you know the document’s language
// ocrEngine.Language = Language.English;
```

*Warum das wichtig ist:* Die Klasse `OcrEngine` übernimmt die schwere Arbeit. Sie einmal zu instanziieren und für mehrere Bilder wiederzuverwenden ist speichereffizienter, als für jede Seite eine neue Engine zu erzeugen.

---

## Schritt 2 – Mehrseitiges TIFF laden (extract text from TIFF)

Jetzt zeigen wir der Engine, wo die Quelldatei liegt. `ImageStream.FromFile` unterstützt TIFF, JPEG, PNG und viele weitere Formate, aber für dieses Tutorial konzentrieren wir uns auf TIFF.

```csharp
// Load the multi‑page TIFF you want to process
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/multi-page.tiff");
```

> **Hinweis:** Ersetzen Sie `YOUR_DIRECTORY` durch den tatsächlichen Ordnerpfad auf Ihrem Rechner.  
> **Tipp:** Hat Ihr TIFF eine niedrige DPI (unter 150), sollten Sie es vorverarbeiten, um die OCR‑Genauigkeit zu verbessern.

---

## Schritt 3 – Alle Seiten erkennen

Ein Aufruf von `Recognize()` führt den OCR‑Algorithmus über **jede Seite** im TIFF aus. Das Ergebnis‑Objekt enthält den Rohtext, Konfidenzwerte und die segmentierte Aufteilung pro Seite.

```csharp
// Run OCR on the loaded image – this extracts text from all pages
var ocrResult = ocrEngine.Recognize();
```

*Was Sie zurückbekommen:* `ocrResult` enthält eine Sammlung von `PageResult`‑Objekten. Auf den Text jeder Seite können Sie über `ocrResult.Pages[i].Text` zugreifen. Die Engine liefert zudem Konfidenz‑Levels, die für Qualitätsprüfungen nützlich sein können.

---

## Schritt 4 – Ergebnisse als JSON speichern (und optional als XML)

Die meisten modernen Pipelines bevorzugen JSON, während Altsysteme noch XML verarbeiten. So erzeugen Sie beide, schön formatiert.

```csharp
// Convert the recognition result to pretty‑printed JSON
string jsonResult = ocrResult.ToJson(prettyPrint: true);
File.WriteAllText(@"YOUR_DIRECTORY/result.json", jsonResult);

// Optional: also output XML for older workflows
string xmlResult = ocrResult.ToXml();
File.WriteAllText(@"YOUR_DIRECTORY/result.xml", xmlResult);
```

### Beispiel‑JSON‑Ausgabe (gekürzt)

```json
{
  "Pages": [
    {
      "PageNumber": 1,
      "Text": "Invoice #12345\nDate: 2024‑03‑15\nTotal: $1,250.00",
      "Confidence": 0.97
    },
    {
      "PageNumber": 2,
      "Text": "Itemized List\n1. Widget A – $500.00\n2. Widget B – $750.00",
      "Confidence": 0.95
    }
  ]
}
```

Das JSON ist menschenlesbar und erleichtert das Debuggen. Das XML spiegelt dieselbe Struktur wider, falls Sie es benötigen.

---

## Schritt 5 – Extraktion verifizieren (extract text from TIFF)

Nachdem die Dateien geschrieben wurden, hilft ein kurzer Plausibilitäts‑Check, sicherzustellen, dass nichts schiefgelaufen ist.

```csharp
// Load the JSON back just to confirm it was saved correctly
string loadedJson = File.ReadAllText(@"YOUR_DIRECTORY/result.json");
Console.WriteLine("First 200 characters of JSON output:");
Console.WriteLine(loadedJson.Substring(0, Math.Min(200, loadedJson.Length)));
```

Wenn Sie den Ausschnitt in der Konsole sehen, haben Sie **Text aus TIFF** erfolgreich extrahiert und gespeichert. Von hier aus können Sie das JSON in einen Suchindex, eine Datenbank oder einen anderen Downstream‑Service einspeisen.

---

## Warum Aspose OCR zum Extrahieren von Text aus TIFF verwenden?

- **Mehrseitige Unterstützung out‑of‑the‑box** – kein manuelles Aufteilen des TIFF nötig.  
- **Hohe Genauigkeit** dank proprietärer neuronaler Netzwerk‑Modelle.  
- **Plattformübergreifend** – funktioniert auf Windows, Linux und macOS .NET‑Runtimes.  
- **Reiche Ausgabeformate** (JSON, XML, Plain Text), die sowohl moderne als auch alte Stacks bedienen.  

Falls Sie noch unsicher sind, probieren Sie die kostenlose Testversion an einem Beispieldokument. Sie werden die Geschwindigkeit und Einfachheit im Vergleich zu Open‑Source‑Alternativen bemerken, die häufig zusätzliche Bild‑Vorverarbeitung erfordern.

---

## Häufige Stolperfallen & wie man sie vermeidet

| Problem | Symptom | Lösung |
|-------|---------|-----|
| Niedrige Auflösung des TIFF | Fehlende Zeichen, niedrige Konfidenz | Bild auf ≥150 DPI hochskalieren vor OCR (`ocrEngine.Image = ImageStream.FromFile(...).Resize(150)` ) |
| Falsche Sprache | Verzerrte Wörter, besonders bei Nicht‑Englisch | `ocrEngine.Language = Language.Spanish` (oder passende Sprache) vor `Recognize()` setzen |
| Speicher‑Ausnahme bei riesigen Dateien | `OutOfMemoryException` | Seiten stapelweise verarbeiten: Schleife über `ocrEngine.Image.Pages` und `RecognizePage(i)` aufrufen |
| Lizenz nicht angewendet | Wasserzeichen „Evaluation“ in der Ausgabe | Lizenz registrieren: `License license = new License(); license.SetLicense("Aspose.OCR.lic");` |

---

## Vollständiges Beispiel (Copy‑Paste‑bereit)

Unten finden Sie das komplette Programm, das Sie in ein neues Konsolen‑Projekt einfügen können. Es enthält alle besprochenen Bausteine – Initialisierung, Laden, Erkennung und Speichern.

```csharp
using Aspose.OCR;
using System;
using System.IO;

namespace TiffOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣  Initialize the OCR engine (ocr engine example)
            // -------------------------------------------------
            var ocrEngine = new OcrEngine();

            // Optional: set license if you have one
            // var license = new License();
            // license.SetLicense("Aspose.OCR.lic");

            // -------------------------------------------------
            // 2️⃣  Load the multi‑page TIFF (extract text from TIFF)
            // -------------------------------------------------
            string tiffPath = @"YOUR_DIRECTORY/multi-page.tiff";
            if (!File.Exists(tiffPath))
            {
                Console.WriteLine($"File not found: {tiffPath}");
                return;
            }

            ocrEngine.Image = ImageStream.FromFile(tiffPath);

            // -------------------------------------------------
            // 3️⃣  Recognize every page
            // -------------------------------------------------
            var ocrResult = ocrEngine.Recognize();

            // -------------------------------------------------
            // 4️⃣  Save JSON (pretty) and optional XML
            // -------------------------------------------------
            string jsonPath = @"YOUR_DIRECTORY/result.json";
            string jsonResult = ocrResult.ToJson(prettyPrint: true);
            File.WriteAllText(jsonPath, jsonResult);
            Console.WriteLine($"JSON saved to {jsonPath}");

            // Optional XML output
            string xmlPath = @"YOUR_DIRECTORY/result.xml";
            string xmlResult = ocrResult.ToXml();
            File.WriteAllText(xmlPath, xmlResult);
            Console.WriteLine($"XML saved to {xmlPath}");

            // -------------------------------------------------
            // 5️⃣  Quick verification (extract text from TIFF)
            // -------------------------------------------------
            string preview = jsonResult.Length > 200 ? jsonResult.Substring(0, 200) + "..." : jsonResult;
            Console.WriteLine("\nPreview of JSON output:");
            Console.WriteLine(preview);
        }
    }
}
```

Speichern Sie die Datei als `Program.cs`, führen Sie `dotnet run` aus und beobachten Sie, wie die Konsole Ihnen den Speicherort von JSON und XML anzeigt. Das war’s – Sie haben gerade ein **OCR‑Engine‑Beispiel** abgeschlossen, das Text aus TIFF extrahiert.

---

## Nächste Schritte & verwandte Themen

- **Batch‑Verarbeitung:** Packen Sie die obige Logik in eine `foreach`‑Schleife, um Dutzende von TIFF‑Dateien automatisch zu bearbeiten.  
- **Such‑Integration:** Schieben Sie das JSON in Elasticsearch oder Azure Cognitive Search, um Volltextsuche über gescannte Dokumente zu ermöglichen.  
- **Bild‑Vorverarbeitung:** Erkunden Sie Asposes `ImageProcessing`‑API, um Schräglagen zu korrigieren, Rauschen zu entfernen oder den Kontrast vor der OCR anzupassen.  
- **Alternatives Ausgabeformat:** Verwenden Sie `ocrResult.ToPlainText()`, wenn Sie nur rohe Zeichenketten ohne Metadaten benötigen.  

Wenn Sie neugierig auf andere Bildformate sind, funktioniert das gleiche Muster für PDFs (einfach die Quelldatei ändern) oder PNGs. Die zentrale Erkenntnis: Sobald die Engine eingerichtet ist, ist der Rest eine wiederholbare Pipeline.

---

## Fazit

Wir haben ein **komplettes OCR‑Engine‑Beispiel** durchgearbeitet, das Ihnen ermöglicht, **Text aus TIFF**‑Dateien mit Aspose OCR zu extrahieren und sauberes JSON sowie optionales XML für jeden nachgelagerten Workflow zu erzeugen. Der Code ist eigenständig, die Erklärungen decken das „Warum“ jedes Schrittes ab.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}