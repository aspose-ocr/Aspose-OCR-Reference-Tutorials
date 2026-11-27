---
category: general
date: 2026-11-26
description: Erfahren Sie, wie Sie OCR für PNG‑Dateien durchführen, PNG in Text konvertieren
  und kyrillischen Text mit Aspose.OCR extrahieren – Schritt‑für‑Schritt‑Anleitung
  für Entwickler.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to perform OCR
- convert PNG to text
- recognize text from PNG
- extract Cyrillic text
- load image for OCR
language: de
lastmod: 2026-11-26
og_description: Wie man OCR auf PNG-Dateien durchführt und kyrillischen Text mit Aspose.OCR
  in C# extrahiert. Folgen Sie diesem vollständigen Tutorial, um PNG in Text zu konvertieren.
og_image_alt: how to perform OCR on a PNG image using Aspose.OCR
og_title: Wie man OCR auf PNG-Bildern mit Aspose.OCR durchführt – C#‑Leitfaden
schemas:
- author: Aspose
  dateModified: '2026-11-26'
  description: Learn how to perform OCR on PNG files, convert PNG to text, and extract
    Cyrillic text using Aspose.OCR – step‑by‑step guide for developers.
  headline: How to perform OCR on PNG images with Aspose.OCR in C#
  type: TechArticle
- description: Learn how to perform OCR on PNG files, convert PNG to text, and extract
    Cyrillic text using Aspose.OCR – step‑by‑step guide for developers.
  name: How to perform OCR on PNG images with Aspose.OCR in C#
  steps:
  - name: Handling large images
    text: 'If the PNG is larger than 2 MB, consider down‑scaling it before recognition
      to speed up processing:'
  - name: 'Edge case: Missing language module'
    text: 'If the download fails (e.g., offline environment), the engine throws an
      `OcrException`. Catch it to provide a graceful fallback:'
  - name: Expected output
    text: 'If `sample_image.png` contains the Cyrillic phrase “Привет мир”, the console
      will display:'
  - name: How it works
    text: 1. **Engine creation** – prepares the OCR pipeline. 2. **Image loading**
      – supports both raw PNG and down‑scaled versions for performance. 3. **Language
      selection** – demonstrates **extract Cyrillic text** while handling missing
      modules. 4. **Recognition** – the core **recognize text from PNG** call
  type: HowTo
tags:
- OCR
- C#
- Aspose.OCR
title: Wie man OCR auf PNG‑Bildern mit Aspose.OCR in C# durchführt
url: /de/net/text-recognition/how-to-perform-ocr-on-png-images-with-aspose-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# So führen Sie OCR auf PNG-Bildern mit Aspose.OCR in C# durch

Wenn Sie **wie man OCR durchführt** auf einer PNG‑Datei benötigen, zeigt Ihnen dieser Leitfaden die genauen Schritte, um PNG in Text mit Aspose.OCR zu konvertieren. Egal, ob Sie kyrillischen Text aus gescannten Dokumenten extrahieren oder einfach Text aus PNG‑Screenshots erkennen, die Lösung funktioniert sofort einsatzbereit und erfordert nur wenige Zeilen C#‑Code.

In diesem Tutorial lernen Sie, wie Sie:

* **Bild für OCR laden** aus einem lokalen Ordner,
* die Engine konfigurieren, um **kyrillischen Text zu extrahieren**,
* **Text aus PNG erkennen** und einen sauberen String erhalten,
* gängige Stolperfallen wie fehlende Sprachmodule und große Bilder behandeln.

Keine Vorkenntnisse mit Aspose.OCR sind erforderlich – nur eine .NET‑Entwicklungsumgebung und ein PNG‑Bild, das Sie verarbeiten möchten.

## Voraussetzungen

Bevor Sie beginnen, stellen Sie sicher, dass Sie Folgendes haben:

* .NET 6.0 (oder höher) installiert.
* Eine lizenzierte oder Testkopie von **Aspose.OCR for .NET**. Sie können eine kostenlose Testversion von der Aspose-Website erhalten.
* Visual Studio 2022 (oder jede IDE, die .NET unterstützt).
* Eine PNG‑Datei, die den Text enthält, den Sie extrahieren möchten (im Beispiel wird `sample_image.png` verwendet).

## Schritt 1: Installieren Sie das Aspose.OCR NuGet‑Paket

Öffnen Sie ein Terminal in Ihrem Projektordner und führen Sie aus:

```bash
dotnet add package Aspose.OCR
```

Das Paket enthält die Kern‑OCR‑Engine und alle Sprachmodule. Wenn Sie eine Sprache anfordern, die lokal nicht vorhanden ist, lädt Aspose.OCR das erforderliche Modul automatisch herunter.

## Schritt 2: Erstellen Sie eine OCR‑Engine‑Instanz (wie man OCR durchführt)

Der erste umsetzbare Schritt in jedem OCR‑Workflow besteht darin, die Engine zu instanziieren. Dieses Objekt verwaltet alle nachfolgenden Vorgänge wie das Laden des Bildes und die Durchführung der Erkennung.

```csharp
using Aspose.OCR;

// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();
```

**Warum das wichtig ist:** Die Klasse `OcrEngine` kapselt die OCR‑Pipeline. Das Erstellen einer einzelnen Instanz und deren Wiederverwendung über mehrere Bilder hinweg reduziert den Speicherverbrauch und verbessert die Leistung.

## Schritt 3: Bild für OCR laden – geben Sie die Quell‑PNG‑Datei an

Das Laden des Bildes ist der Punkt, an dem Sie **Bild für OCR laden**. Aspose.OCR akzeptiert mehrere Eingabetypen; am einfachsten ist `ImageStream.FromFile`.

```csharp
// Load the PNG image from disk
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/sample_image.png");
```

> **Pro Tipp:** Verwenden Sie einen absoluten Pfad oder `Path.Combine`, um Laufzeitfehler in unterschiedlichen Umgebungen zu vermeiden.

### Umgang mit großen Bildern

Wenn das PNG größer als 2 MB ist, sollten Sie es vor der Erkennung verkleinern, um die Verarbeitung zu beschleunigen:

```csharp
using System.Drawing;

// Downscale large images to a maximum width of 1200 pixels
Bitmap original = new Bitmap(@"YOUR_DIRECTORY/sample_image.png");
int maxWidth = 1200;
int newHeight = (int)(original.Height * (maxWidth / (double)original.Width));
Bitmap resized = new Bitmap(original, new Size(maxWidth, newHeight));

using (var ms = new MemoryStream())
{
    resized.Save(ms, System.Drawing.Imaging.ImageFormat.Png);
    ocrEngine.Image = ImageStream.FromStream(ms);
}
```

## Schritt 4: Sprache konfigurieren – kyrillischen Text extrahieren

Standardmäßig geht Aspose.OCR von Englisch aus. Um **kyrillischen Text zu extrahieren**, setzen Sie die Eigenschaft `Language` auf `Language.Cyrillic`. Das erforderliche Modul wird beim ersten Ausführen des Codes automatisch heruntergeladen.

```csharp
// Set the OCR language to Cyrillic
ocrEngine.Language = Language.Cyrillic;
```

Wenn Sie mehrere Sprachen erkennen müssen (z. B. Englisch und Kyrillisch), können Sie sie kombinieren:

```csharp
ocrEngine.Language = Language.English | Language.Cyrillic;
```

### Sonderfall: Fehlendes Sprachmodul

Falls der Download fehlschlägt (z. B. in einer Offline‑Umgebung), wirft die Engine eine `OcrException`. Fangen Sie sie ab, um eine elegante Rückfalllösung zu bieten:

```csharp
try
{
    ocrEngine.Language = Language.Cyrillic;
}
catch (OcrException ex)
{
    Console.WriteLine($"Language module could not be loaded: {ex.Message}");
    // Optionally, fall back to English or abort the process
}
```

## Schritt 5: Führen Sie die Erkennungsoperation aus (Text aus PNG erkennen)

Jetzt, wo Bild und Sprache festgelegt sind, können Sie **Text aus PNG erkennen**. Die Methode `Recognize` führt die OCR‑Pipeline synchron aus.

```csharp
// Run OCR
ocrEngine.Recognize();
```

**Warum es funktioniert:** Intern wendet Aspose.OCR Vorverarbeitung (Binarisierung, Rauschunterdrückung) an, bevor das Bild an einen neuronalen Netzwerk‑Erkenner übergeben wird, der für die ausgewählte Sprache optimiert ist.

## Schritt 6: Rufen Sie den erkannten Text ab und zeigen Sie ihn an (PNG in Text konvertieren)

Nach der Erkennung ist der extrahierte String über die Eigenschaft `Text` verfügbar. Dies ist der letzte Schritt in **PNG in Text konvertieren**.

```csharp
// Get the recognized text
string recognizedText = ocrEngine.Text;

// Output the result
Console.WriteLine("=== OCR Result ===");
Console.WriteLine(recognizedText);
```

### Erwartete Ausgabe

Enthält `sample_image.png` die kyrillische Phrase „Привет мир“, wird die Konsole anzeigen:

```
=== OCR Result ===
Привет мир
```

Die Ausgabe kann Zeilenumbrüche und Interpunktion exakt so enthalten, wie sie im Bild erscheinen. Sie können den String bei Bedarf mit `String.Trim()`, `Regex` oder anderen Text‑Bereinigungs‑Utilities nachbearbeiten.

## Schritt 7: Optional – Speichern Sie das Ergebnis in einer Datei

Das Speichern des OCR‑Ergebnisses ermöglicht nachgelagerte Verarbeitung (z. B. Indexierung, Übersetzung). Hier ein schneller Weg, den Text in eine UTF‑8‑Datei zu schreiben:

```csharp
File.WriteAllText(@"YOUR_DIRECTORY/ocr_output.txt", recognizedText, Encoding.UTF8);
Console.WriteLine("OCR text saved to ocr_output.txt");
```

## Häufige Fallstricke und wie man sie vermeidet

| Problem | Symptom | Lösung |
|---------|----------|--------|
| **Fehlendes Sprachmodul** | `OcrException` bei `Language = Language.Cyrillic` | Stellen Sie beim ersten Ausführen sicher, dass eine Internetverbindung besteht, oder laden Sie die Module im Voraus über Asposes Offline‑Paket herunter. |
| **Unscharfes oder kontrastarmes Bild** | Schlechte Genauigkeit, viele „?“‑Zeichen | Bild vorverarbeiten: Kontrast erhöhen, Schärfen anwenden oder in Graustufen konvertieren, bevor es an die Engine übergeben wird. |
| **Sehr große PNG** | Lange Verarbeitungszeit, mögliche `OutOfMemoryException` | Wie in Schritt 3 verkleinern oder ein mehrseitiges Bild in separate Kacheln aufteilen. |
| **Nicht‑UTF‑8‑Zeichen** | Verzerrte Ausgabe | Stellen Sie sicher, dass die Konsole oder der Dateischreiber UTF‑8‑Kodierung verwendet (`Encoding.UTF8`). |

## Vollständiges, ausführbares Beispiel

Unten finden Sie das komplette Programm, das alle oben genannten Schritte integriert. Kopieren Sie es in ein neues Konsolenprojekt und führen Sie es nach Anpassung der Dateipfade aus.

```csharp
using System;
using System.Drawing;
using System.IO;
using System.Text;
using Aspose.OCR;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1. Create OCR engine
            OcrEngine ocrEngine = new OcrEngine();

            // 2. Load PNG image (with optional down‑scaling for large files)
            string imagePath = @"YOUR_DIRECTORY/sample_image.png";
            Bitmap original = new Bitmap(imagePath);
            const int maxWidth = 1200;

            if (original.Width > maxWidth)
            {
                int newHeight = (int)(original.Height * (maxWidth / (double)original.Width));
                Bitmap resized = new Bitmap(original, new Size(maxWidth, newHeight));

                using (var ms = new MemoryStream())
                {
                    resized.Save(ms, System.Drawing.Imaging.ImageFormat.Png);
                    ocrEngine.Image = ImageStream.FromStream(ms);
                }
            }
            else
            {
                ocrEngine.Image = ImageStream.FromFile(imagePath);
            }

            // 3. Set language to Cyrillic (fallback to English if needed)
            try
            {
                ocrEngine.Language = Language.Cyrillic;
            }
            catch (OcrException ex)
            {
                Console.WriteLine($"Failed to load Cyrillic module: {ex.Message}");
                Console.WriteLine("Falling back to English.");
                ocrEngine.Language = Language.English;
            }

            // 4. Recognize text
            ocrEngine.Recognize();

            // 5. Retrieve and display the text (convert PNG to text)
            string recognizedText = ocrEngine.Text;
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(recognizedText);

            // 6. Save result to a UTF‑8 file
            string outputPath = @"YOUR_DIRECTORY/ocr_output.txt";
            File.WriteAllText(outputPath, recognizedText, Encoding.UTF8);
            Console.WriteLine($"OCR text saved to {outputPath}");
        }
    }
}
```

### Wie es funktioniert

1. **Engine-Erstellung** – bereitet die OCR‑Pipeline vor.  
2. **Bildladen** – unterstützt sowohl rohe PNG‑ als auch herunter skalierte Versionen für die Leistung.  
3. **Sprachauswahl** – demonstriert **kyrillischen Text extrahieren**, während fehlende Module behandelt werden.  
4. **Erkennung** – der Kernaufruf **Text aus PNG erkennen**.  
5. **Ergebnisverarbeitung** – zeigt **PNG in Text konvertieren** und schreibt die Ausgabe in eine Datei.

Führen Sie das Programm mit `dotnet run` aus. Wenn alles korrekt eingerichtet ist, sehen Sie den erkannten Text in der Konsole und in `ocr_output.txt` gespeichert.

## Fazit

In diesem Tutorial haben Sie **wie man OCR durchführt** auf PNG‑Dateien mit Aspose.OCR für .NET gelernt, von **Bild für OCR laden** über **kyrillischen Text extrahieren** bis hin zu **PNG in Text konvertieren**. Das vollständige, ausführbare Beispiel demonstriert den Standard‑Workflow, gängige Randfälle und praktische Tipps, die Ihre OCR‑Pipeline zuverlässig halten.

**Nächste Schritte**

* Erkunden Sie **Text aus PNG erkennen** mit zusätzlichen Sprachen (Arabisch, Chinesisch), indem Sie `Language`‑Flags kombinieren.  
* Integrieren Sie das OCR‑Ergebnis mit Azure Cognitive Search für durchsuchbare Dokumentenarchive.  
* Experimentieren Sie mit den Einstellungen von Aspose.OCR’s `OcrEngine` wie `Resolution`

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, zusätzliche API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Wie man das Aspose.OCR‑Modell herunterlädt und Text aus PNG in C# extrahiert](/ocr/english/net/text-recognition/how-to-download-ocr-model-and-extract-text-from-png-using-as/)
- [Wie man OCR in C# durchführt – Kyrillischen Text mit Aspose erkennen](/ocr/english/net/text-recognition/how-to-perform-ocr-in-c-recognize-cyrillic-text-with-aspose/)
- [Wie man Batch‑OCR in C# durchführt – Schneller Weg, Text aus PNG‑Dateien zu extrahieren](/ocr/english/net/ocr-optimization/how-to-batch-ocr-in-c-fast-way-to-extract-text-png-files/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}