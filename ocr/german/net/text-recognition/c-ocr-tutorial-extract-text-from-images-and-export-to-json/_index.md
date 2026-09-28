---
category: general
date: 2026-01-01
description: C# OCR‑Tutorial, das zeigt, wie man Text extrahiert, ein Bild für OCR
  lädt und JSON mit Aspose.OCR in eine Datei schreibt – Schritt‑für‑Schritt‑Anleitung.
draft: false
keywords:
- c# OCR tutorial
- how to extract text
- write json to file
- load image for OCR
- OCR image to JSON
language: de
og_description: C#‑OCR‑Tutorial, das Sie Schritt für Schritt durch das Extrahieren
  von Text aus Bildern, das Laden von Bildern für OCR und das Schreiben von JSON in
  eine Datei mit Aspose.OCR führt.
og_title: c# OCR‑Tutorial – Text extrahieren und als JSON exportieren
tags:
- Aspose.OCR
- C#
- Text Extraction
title: c# OCR‑Tutorial – Text aus Bildern extrahieren und in JSON exportieren
url: /de/net/text-recognition/c-ocr-tutorial-extract-text-from-images-and-export-to-json/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# OCR‑Tutorial – Text aus Bildern extrahieren und in JSON exportieren

Haben Sie sich jemals gefragt, wie man Text aus einer gescannten Rechnung extrahiert, ohne Stunden damit zu verbringen, eigene Parser zu schreiben? Sie sind nicht allein. In diesem **c# OCR tutorial** zeigen wir Ihnen genau, wie Sie ein Bild für OCR laden, die Erkennungs‑Engine ausführen und dann **JSON in Datei schreiben**, damit Sie die Daten in nachgelagerte Systeme einspeisen können.

Stellen Sie sich vor, Sie haben einen Ordner mit Belegen, jeder benannt `receipt1.png`, `receipt2.png`, und Sie benötigen eine schnelle Möglichkeit, sie in durchsuchbare JSON‑Datensätze zu verwandeln. Das ist das Problem, das wir lösen werden, und am Ende haben Sie eine einsatzbereite Konsolen‑App, die genau das tut. Keine zusätzlichen Abhängigkeiten außer Aspose.OCR und keine Magie – nur klare, reproduzierbare Schritte.

> **Was Sie lernen werden**
> - Wie man **Bild für OCR laden** mit Aspose.OCR verwendet.
> - Der beste Weg, **Text zu extrahieren** und Konfidenzwerte zu erhalten.
> - Konvertierung des OCR‑Ergebnisses in ein gut strukturiertes **OCR image to JSON**‑Payload.
> - Sicheres **Schreiben von JSON in Datei** und Überprüfung der Ausgabe.

## Voraussetzungen

- .NET 6 SDK oder neuer (der Code funktioniert auch mit .NET Core).  
- Visual Studio 2022 oder ein beliebiger Editor Ihrer Wahl.  
- Aspose.OCR NuGet‑Paket (`Install-Package Aspose.OCR`).  
- Eine Bilddatei (PNG, JPG, BMP), die Sie verarbeiten möchten – für die Demo verwenden wir `invoice.png`.

Falls Ihnen etwas davon fehlt, holen Sie sich das SDK von der Microsoft‑Website und fügen Sie das NuGet‑Paket über die Package‑Manager‑Konsole hinzu:

```powershell
Install-Package Aspose.OCR
```

Jetzt, da die Grundlagen gelegt sind, tauchen wir in die eigentliche Implementierung ein.

## Schritt 1: c# OCR‑Tutorial – OCR‑Engine initialisieren

Bevor wir **Bild für OCR laden** können, benötigen wir eine Instanz der Engine, die den Erkennungsprozess steuert. Die Klasse `OcrEngine` ist leichtgewichtig, aber es ist gute Praxis, sie in einem `using`‑Block zu kapseln, damit Ressourcen sofort freigegeben werden.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class JsonExportDemo
{
    static void Main()
    {
        // Step 1: Create the OCR engine – this is the heart of the c# OCR tutorial
        var ocrEngine = new OcrEngine();

        // The rest of the steps follow…
```

*Pro‑Tipp:* Wenn Sie viele Bilder stapelweise verarbeiten wollen, verwenden Sie dieselbe `OcrEngine`‑Instanz wieder, anstatt jedes Mal eine neue zu erstellen. Das reduziert den Speicherverbrauch und beschleunigt den Vorgang.

## Schritt 2: Bild für OCR laden

Jetzt **laden wir das Bild für OCR**. Aspose.OCR unterstützt verschiedene Formate, sodass Sie es auf ein PNG, JPEG oder sogar ein mehrseitiges TIFF zeigen können. Die Methode `OcrImage.FromFile` liest die Datei und bereitet sie für die Erkennung vor.

```csharp
        // Step 2: Load the image you want to recognize
        // Replace YOUR_DIRECTORY with the folder that holds your invoice.png
        var imagePath = @"YOUR_DIRECTORY/invoice.png";
        var ocrImage = OcrImage.FromFile(imagePath);
```

> **Warum das wichtig ist:** Das separate Laden des Bildes ermöglicht es Ihnen, seine Abmessungen, DPI oder sogar eine Vorverarbeitung (z. B. Binarisierung) zu prüfen, bevor Sie es an die Engine senden. Wenn das Bild beschädigt ist, wirft `FromFile` eine klare Ausnahme, die Sie abfangen und protokollieren können.

## Schritt 3: Text extrahieren – Erkennung ausführen

Mit dem Bild in der Hand können wir endlich **Text extrahieren**. Die Methode `Recognize` gibt ein `OcrResult`‑Objekt zurück, das nicht nur den Klartext, sondern auch Positionsdaten und Konfidenzwerte für jedes Wort enthält.

```csharp
        // Step 3: Perform OCR – this is the core of how to extract text
        var ocrResult = ocrEngine.Recognize(ocrImage);
```

*Sonderfall:* Einige PDFs enthalten unsichtbare Textebenen. Wenn Sie eine PDF‑Seite, die als Bild gerendert wurde, einspeisen, sieht die Engine möglicherweise nichts. In solchen Fällen sollten Sie zuerst Aspose.PDF verwenden, um die verborgene Ebene zu extrahieren, und erst bei Bedarf auf OCR zurückgreifen.

## Schritt 4: OCR‑Bild zu JSON – Ergebnis konvertieren

Die Klasse `OcrResult` bietet einen praktischen `ToJson()`‑Helper, der das gesamte Ergebnis‑Set – einschließlich des Begrenzungsrahmens und der Konfidenz jedes Wortes – in einen JSON‑String serialisiert. Das ist der sauberste Weg, **OCR image to JSON** zu erreichen, ohne einen eigenen Serializer zu schreiben.

```csharp
        // Step 4: Convert the OCR result to JSON (includes words, confidence, locations)
        string jsonResult = ocrResult.ToJson();
```

Wenn Sie ein benutzerdefiniertes Schema bevorzugen, können Sie über `ocrResult.Words` iterieren und Ihr eigenes Objekt erstellen, aber für die meisten Szenarien ist das integrierte JSON ausreichend und bereits gut strukturiert.

## Schritt 5: JSON in Datei schreiben

Jetzt kommt das letzte Puzzleteil: das Persistieren des JSON‑Payloads. Die Methode `File.WriteAllText` stellt sicher, dass die Datei atomisch erstellt (oder überschrieben) wird. Achten Sie darauf, dass das Zielverzeichnis existiert, sonst erhalten Sie eine `DirectoryNotFoundException`.

```csharp
        // Step 5: Save the JSON output – this demonstrates write JSON to file
        var jsonPath = @"YOUR_DIRECTORY/invoice.json";
        File.WriteAllText(jsonPath, jsonResult);
```

*Tipp:* Wenn Sie UTF‑8 mit BOM oder eine andere Kodierung benötigen, verwenden Sie die Überladung, die ein `Encoding`‑Argument akzeptiert.

## Schritt 6: Ausgabe überprüfen

Ein kurzer `Console.WriteLine` zeigt uns, dass der Prozess erfolgreich abgeschlossen wurde. Sie können die JSON‑Datei auch in einem Viewer öffnen, um die Struktur zu bestätigen.

```csharp
        // Step 6: Inform the user that the JSON file has been saved
        Console.WriteLine($"JSON saved to {jsonPath}");
    }
}
```

### Erwarteter JSON‑Auszug

```json
{
  "Text": "Invoice #12345\nDate: 2025-12-31\nTotal: $250.00",
  "Words": [
    { "Text": "Invoice", "Confidence": 0.98, "Location": { "X": 10, "Y": 15, "Width": 80, "Height": 20 } },
    { "Text": "#12345", "Confidence": 0.96, "Location": { "X": 95, "Y": 15, "Width": 60, "Height": 20 } }
    // … more words …
  ]
}
```

Das JSON enthält den Standort jedes Wortes, was praktisch ist, wenn Sie später Text in einer Benutzeroberfläche hervorheben möchten.

## Vollständiges funktionierendes Beispiel

Unten finden Sie das vollständige, copy‑and‑paste‑bereite Programm. Ersetzen Sie `YOUR_DIRECTORY` durch den tatsächlichen Pfad, in dem sich Ihr Bild befindet.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class JsonExportDemo
{
    static void Main()
    {
        // Step 1: Initialize the OCR engine
        var ocrEngine = new OcrEngine();

        // Step 2: Load the image you want to recognize
        var imagePath = @"YOUR_DIRECTORY/invoice.png";
        var ocrImage = OcrImage.FromFile(imagePath);

        // Step 3: Perform OCR – how to extract text
        var ocrResult = ocrEngine.Recognize(ocrImage);

        // Step 4: Convert the result to JSON (OCR image to JSON)
        string jsonResult = ocrResult.ToJson();

        // Step 5: Write JSON to file – write JSON to file
        var jsonPath = @"YOUR_DIRECTORY/invoice.json";
        File.WriteAllText(jsonPath, jsonResult);

        // Step 6: Verify
        Console.WriteLine($"JSON saved to {jsonPath}");
    }
}
```

Führen Sie das Programm aus (`dotnet run` im Projektordner) und Sie finden `invoice.json` neben Ihrem ursprünglichen PNG.

## Häufige Fallstricke & wie man sie vermeidet

| Problem | Warum es passiert | Lösung |
|-------|----------------|-----|
| **FileNotFoundException** beim Laden des Bildes | Pfad‑Tippfehler oder fehlende Datei | Verwenden Sie `Path.Combine` und prüfen Sie `File.Exists` bevor Sie `FromFile` aufrufen. |
| **Niedrige Konfidenzwerte** | Schlechte Bildqualität, niedrige DPI | Vorverarbeitung mit `ocrImage.AdjustContrast` oder das Bild auf 300 DPI hochskalieren. |
| **JSON‑Datei leer** | `ocrResult` gab null zurück (Engine fehlgeschlagen) | Verifizieren Sie, dass das Bildformat unterstützt wird und dass die Lizenz (falls vorhanden) korrekt angewendet wurde. |
| **Leistungsengpass bei großen Stapeln** | Erneutes Erstellen von `OcrEngine` bei jeder Iteration | Verwenden Sie eine einzige `OcrEngine`‑Instanz für den gesamten Stapel und entsorgen Sie sie erst am Ende. |

## Nächste Schritte

Jetzt, da Sie das **c# OCR tutorial** gemeistert haben, möchten Sie vielleicht:

- **Batch process** einen gesamten Ordner und die JSON‑Dateien zu einer einzigen Datenbank aggregieren.  
- **Integrate** die Ausgabe mit Azure Cognitive Search für durchsuchbare PDFs.  
- **Add language support** indem Sie `ocrEngine.Language = OcrLanguage.Spanish` setzen (oder jede unterstützte Sprache).  
- **Post‑process** das JSON, um Tabellen oder Schlüssel‑Wert‑Paare mit regulären Ausdrücken zu extrahieren.  

Jede dieser Erweiterungen baut auf den Kernkonzepten auf, die wir behandelt haben: Bilder für OCR laden, Text extrahieren, in JSON konvertieren und dieses JSON auf die Festplatte schreiben.

---

### Fazit

In diesem **c# OCR tutorial** haben wir jeden Schritt durchgegangen, der nötig ist, um **Bild für OCR zu laden**, **Text zu extrahieren**, das Ergebnis in ein **OCR image to JSON**‑Payload zu transformieren und schließlich **JSON in Datei zu schreiben**. Das vollständige Code‑Beispiel kann in jedes .NET‑Projekt übernommen werden, und die Erklärungen geben Ihnen den Kontext, den Sie benötigen, um die Lösung an reale Szenarien anzupassen.

Probieren Sie es mit Ihren eigenen Belegen oder Rechnungen aus – passen Sie die Bildvorverarbeitung an, experimentieren Sie mit verschiedenen Sprachen und beobachten Sie, wie die JSON‑Ausgabe wächst. Wenn Sie auf Probleme stoßen, schauen Sie erneut in die Tabelle der Fallstricke oder hinterlassen Sie unten einen Kommentar. Viel Spaß beim Coden!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}