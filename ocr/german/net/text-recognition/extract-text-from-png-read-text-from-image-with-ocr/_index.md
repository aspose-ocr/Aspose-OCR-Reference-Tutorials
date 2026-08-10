---
category: general
date: 2026-03-17
description: Extrahiere Text aus PNG mit Aspose OCR in C#. Lerne, Text aus Bildern
  zu lesen, Beleg‑OCR zu verarbeiten und eine OCR‑Engine mit GPU‑Beschleunigung zu
  erstellen.
draft: false
keywords:
- extract text from png
- read text from image
- ocr receipt image
- process receipt ocr
- create ocr engine
language: de
og_description: Extrahieren Sie Text aus PNG mit Aspose OCR. Dieser Leitfaden zeigt,
  wie man Text aus einem Bild liest, die Beleg‑OCR verarbeitet und eine OCR‑Engine
  effizient erstellt.
og_title: Text aus PNG extrahieren – Text aus Bild mit OCR lesen
tags:
- OCR
- CSharp
- Aspose
title: Text aus PNG extrahieren – Text aus Bild mit OCR lesen
url: /de/net/text-recognition/extract-text-from-png-read-text-from-image-with-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Text aus PNG extrahieren – Text aus Bild mit OCR lesen

Haben Sie schon einmal **Text aus PNG** extrahieren müssen, waren sich aber nicht sicher, welche Bibliothek zuverlässige Ergebnisse liefert? Sie sind nicht allein – Entwickler fragen ständig: „Wie lese ich Text aus Bilddateien wie Quittungen, ohne ein eigenes neuronales Netz zu schreiben?“ Die gute Nachricht: Aspose OCR übernimmt die schwere Arbeit für Sie, und Sie können sogar die GPU aktivieren, um die Geschwindigkeit zu erhöhen.

In diesem Tutorial gehen wir Schritt für Schritt durch alles, was Sie für die **Verarbeitung von Quittungs‑OCR** benötigen – von der Installation des NuGet‑Pakets bis hin zur Erstellung einer OCR‑Engine, die Ihre PNG‑Datei versteht. Am Ende haben Sie eine eigenständige Konsolen‑App, die ein Quittungs‑Bild liest, den erkannten Text ausgibt und Ihnen zeigt, wie Sie die Engine für verschiedene Szenarien anpassen können. Keine externen Dokumente, nur reiner Code und klare Erklärungen.

## Voraussetzungen

- .NET 6.0 SDK (oder eine aktuelle .NET‑Version)  
- Visual Studio 2022 oder VS Code mit C#‑Erweiterungen  
- Eine unterstützte NVIDIA‑GPU mit dem neuesten Treiber (optional, aber empfohlen für den GPU‑Modus)  
- Das **Aspose.OCR** NuGet‑Paket (`dotnet add package Aspose.OCR`)  

Wenn Sie keine GPU haben, können Sie das Beispiel weiterhin im CPU‑Modus ausführen – überspringen Sie einfach die Zeilen zur GPU‑Konfiguration.

## Schritt 1: Aspose.OCR installieren und Projekt einrichten

Erstellen Sie zunächst ein neues Konsolen‑Projekt und binden Sie die Aspose‑OCR‑Bibliothek ein.

```bash
dotnet new console -n ReceiptOcrDemo
cd ReceiptOcrDemo
dotnet add package Aspose.OCR
```

Warum das wichtig ist: Das `Aspose.OCR`‑Paket enthält die OCR‑Engine, Bild‑Loader und optionale GPU‑Unterstützung. Die Installation über NuGet stellt sicher, dass Sie die neueste stabile Version erhalten (Stand März 2026 ist das 23.10).

## Schritt 2: Namespaces importieren und die OCR‑Engine erstellen

Öffnen Sie nun **Program.cs** und fügen Sie die erforderlichen `using`‑Direktiven hinzu. Anschließend instanziieren Sie die Engine.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 2: Create an OCR engine instance
            var ocrEngine = new OcrEngine();

            // Optional: Enable GPU acceleration if a compatible GPU is present
            // This dramatically speeds up processing of high‑resolution PNGs
            ocrEngine.Config.EngineMode = EngineMode.Gpu;   // <-- primary way to "process receipt ocr" fast
            ocrEngine.Config.GpuDeviceId = 0; // selects the first GPU in the system

            // The rest of the code follows...
```

**Pro‑Tipp:** Wenn Sie auf `System.DllNotFoundException` auf Maschinen ohne GPU stoßen, kommentieren Sie einfach die beiden Zeilen aus, die `EngineMode` und `GpuDeviceId` setzen. Die Engine fällt automatisch auf die CPU zurück.

## Schritt 3: Das PNG‑Bild laden, aus dem Sie Text extrahieren möchten

Aspose OCR kann Bilder direkt von einem Dateipfad, einem Stream oder sogar einem Byte‑Array lesen. Für diese Demo laden wir ein lokales Quittungs‑Bild.

```csharp
            // Step 3: Load the image (replace the path with your own PNG file)
            string imagePath = @"C:\Images\receipt.png";

            // Validate the file exists to avoid runtime surprises
            if (!System.IO.File.Exists(imagePath))
            {
                Console.WriteLine($"Error: File not found – {imagePath}");
                return;
            }

            // Load the image into the engine
            ocrEngine.Image = ImageStream.FromFile(imagePath);
```

Beachten Sie, dass wir gegen eine fehlende Datei absichern. In realen Anwendungen würden Sie wahrscheinlich eine benutzerfreundliche UI‑Meldung anzeigen, anstatt einfach zu beenden.

## Schritt 4: Die OCR‑Erkennung ausführen

Die eigentliche Textextraktion erfolgt mit einem einzigen Methodenaufruf. Die Engine gibt ein `OcrResult`‑Objekt zurück, das den Roh‑String, Konfidenzwerte und Layout‑Informationen enthält.

```csharp
            // Step 4: Run the OCR process
            OcrResult ocrResult = ocrEngine.Recognize();

            // Check if the engine succeeded
            if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
            {
                Console.WriteLine("No text could be recognized.");
                return;
            }
```

Warum wir `ocrResult.Text` prüfen: Manchmal liefert ein PNG niedriger Qualität einen leeren String, und es ist besser, den Benutzer zu informieren, als stillschweigend nichts auszugeben.

## Schritt 5: Den erkannten Text ausgeben

Zum Schluss geben wir den extrahierten String in der Konsole aus. Sie können ihn auch in eine Datei, eine Datenbank schreiben oder an einen anderen Service weiterleiten.

```csharp
            // Step 5: Display the recognized text
            Console.WriteLine("=== Extracted Text from PNG ===");
            Console.WriteLine(ocrResult.Text);
            Console.WriteLine("=== End of Output ===");
        }
    }
}
```

Wenn Sie das Programm ausführen (`dotnet run`), sollten Sie etwa Folgendes sehen:

```
=== Extracted Text from PNG ===
Store: Coffee Corner
Date: 03/15/2026
Item      Qty   Price
Latte      2    $5.40
Muffin     1    $2.30
Total            $7.70
=== End of Output ===
```

Das ist die **vollständige Lösung, um Text aus PNG**‑Dateien mit Aspose OCR zu extrahieren, und Sie haben gerade gelernt, **Text aus Bild**‑Dateien zu lesen, die wie Quittungen aussehen.

## Optional: Feinabstimmung der OCR‑Engine (Fortgeschritten)

Falls Sie höhere Genauigkeit für bestimmte Schriftarten oder verrauschte Hintergründe benötigen, sollten Sie diese Einstellungen anpassen:

```csharp
// Enable language detection (default is English)
ocrEngine.Config.Language = Language.English;

// Turn on automatic image preprocessing (deskew, binarization)
ocrEngine.Config.EnableImagePreprocessing = true;

// Set a confidence threshold if you only want high‑certainty results
ocrEngine.Config.ConfidenceThreshold = 0.75f;
```

Diese Anpassungen sind besonders nützlich, wenn Sie **Quittungs‑OCR** in Batch‑Jobs verarbeiten, bei denen einige Scans weniger als perfekt sind.

## Häufige Stolperfallen & wie man sie vermeidet

| Problem | Warum es passiert | Lösung |
|-------|----------------|-----|
| **GPU‑Treiber fehlt** | Die Engine versucht, CUDA zu laden, findet die DLL aber nicht. | Installieren Sie den neuesten NVIDIA‑Treiber oder wechseln Sie in den CPU‑Modus, indem Sie die Zeile `EngineMode.Gpu` entfernen. |
| **Falscher Bildpfad** | `ImageStream.FromFile` wirft, wenn die Datei nicht gefunden wird. | Validieren Sie immer den Pfad (siehe Schritt 3) oder verwenden Sie `Path.Combine` für plattformübergreifende Sicherheit. |
| **Niedrige Konfidenz bei unscharfen Quittungen** | Die OCR‑Engine kann die Zeichen nicht unterscheiden. | Aktivieren Sie `EnableImagePreprocessing` und erhöhen Sie optional die DPI des Bildes, bevor Sie es an die Engine übergeben. |
| **Speicherleck in langlaufenden Diensten** | Jede `OcrEngine` hält nicht verwaltete Ressourcen. | Entsorgen Sie die Engine nach Gebrauch: `using var ocrEngine = new OcrEngine();` |

## Vollständiges funktionierendes Beispiel (Copy‑Paste)

Unten finden Sie das **gesamte Programm**, das Sie in `Program.cs` einfügen können. Alle optionalen Anpassungen sind auskommentiert, um sie bei Bedarf leicht zu aktivieren.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Create OCR engine
            using var ocrEngine = new OcrEngine();

            // Enable GPU acceleration if you have a supported card
            ocrEngine.Config.EngineMode = EngineMode.Gpu;
            ocrEngine.Config.GpuDeviceId = 0;

            // Optional fine‑tuning (uncomment as needed)
            //ocrEngine.Config.Language = Language.English;
            //ocrEngine.Config.EnableImagePreprocessing = true;
            //ocrEngine.Config.ConfidenceThreshold = 0.75f;

            // Load PNG image
            string imagePath = @"C:\Images\receipt.png";
            if (!System.IO.File.Exists(imagePath))
            {
                Console.WriteLine($"Error: File not found – {imagePath}");
                return;
            }
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // Perform OCR
            OcrResult ocrResult = ocrEngine.Recognize();

            // Verify result
            if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
            {
                Console.WriteLine("No text could be recognized.");
                return;
            }

            // Output the extracted text
            Console.WriteLine("=== Extracted Text from PNG ===");
            Console.WriteLine(ocrResult.Text);
            Console.WriteLine("=== End of Output ===");
        }
    }
}
```

Speichern, `dotnet run` ausführen, und Sie sehen den Inhalt der Quittung in der Konsole.

![extract text from png example](receipt.png "extract text from png example")

*Das obige Bild zeigt ein Beispiel‑Quittungs‑PNG, das der Code verarbeiten kann.*

## Zusammenfassung

Wir haben behandelt, wie man **Text aus PNG**‑Dateien mit Aspose OCR extrahiert, gezeigt, wie man **Text aus Bild**‑Dateien liest, und eine komplette **Quittungs‑OCR**‑Pipeline inklusive optionaler GPU‑Beschleunigung durchlaufen. Durch das **Erstellen einer eigenen OCR‑Engine** erhalten Sie volle Kontrolle über Konfiguration, Leistung und Fehlerbehandlung.

## Was können Sie als Nächstes erkunden?

- **Batch‑Verarbeitung**: Durchlaufen Sie ein Verzeichnis mit PNG‑Quittungen und schreiben Sie jedes Ergebnis in eine CSV‑Datei.  
- **Integration mit Azure Functions**: Verwandeln Sie diese Konsolen‑App in einen serverlosen Endpunkt, der Bild‑Uploads entgegennimmt.  
- **Mehrsprachige Unterstützung**: Ersetzen Sie `Language.English` durch `Language.Spanish` oder fügen Sie eigene Wörterbücher hinzu.  
- **Nachbearbeitung**: Verwenden Sie reguläre Ausdrücke, um Felder wie Gesamtbetrag, Datum oder Steuernummer aus dem rohen OCR‑String zu extrahieren.

Probieren Sie es aus – OCR ist ein überraschend flexibles Werkzeug, sobald Sie die richtigen Regler kennen. Wenn Sie auf Probleme stoßen, hinterlassen Sie einen Kommentar unten oder schauen Sie in die Aspose OCR API‑Referenz für tiefere Einblicke.

Viel Spaß beim Coden und beim Umwandeln dieser hartnäckigen PNG‑Quittungen in durchsuchbaren Text!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}