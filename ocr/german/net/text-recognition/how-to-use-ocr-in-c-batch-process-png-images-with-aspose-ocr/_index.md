---
category: general
date: 2026-02-14
description: Wie man OCR in C# verwendet, um Text aus PNG-Dateien schnell zu extrahieren.
  Lernen Sie die Batch-OCR von Bildern, verarbeiten Sie mehrere Bilder und nutzen
  Sie Aspose OCR C# in einem einzigen Leitfaden.
draft: false
keywords:
- how to use OCR
- extract text png
- batch OCR images
- process multiple images
- aspose OCR c#
language: de
og_description: Wie man OCR in C# mit Aspose OCR C# verwendet. Dieses Tutorial zeigt,
  wie man Text aus PNG‑Dateien extrahiert, OCR‑Bilder stapelweise verarbeitet und
  mehrere Bilder effizient bearbeitet.
og_title: Wie man OCR in C# verwendet – Stapelweise PNG-Text extrahieren
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Wie man OCR in C# verwendet – PNG‑Bilder stapelweise mit Aspose OCR verarbeiten
url: /de/net/text-recognition/how-to-use-ocr-in-c-batch-process-png-images-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man OCR in C# verwendet – PNG‑Bilder stapelweise mit Aspose OCR verarbeiten

Haben Sie sich jemals gefragt, **wie man OCR** einsetzt, um Text aus einer Menge von PNG‑Dateien zu extrahieren, ohne für jede Datei eine separate Routine zu schreiben? Sie sind nicht allein. Viele Entwickler stoßen an ihre Grenzen, wenn sie **Text aus PNG**‑Assets in großem Umfang extrahieren müssen, insbesondere wenn die Bilder in einem Ordner liegen und die OCR‑Engine für jede Datei gestartet werden muss.  

In diesem Leitfaden gehen wir Schritt für Schritt durch eine komplette, sofort ausführbare Lösung, die **Bilder stapelweise OCR‑verarbeitet**, **mehrere Bilder parallel** verarbeitet und die leistungsstarke **Aspose OCR C#**‑Bibliothek nutzt. Am Ende haben Sie eine einzige ausführbare Datei, die beliebig viele PNGs einliest, deren Text extrahiert und die Ergebnisse in der Konsole ausgibt – und das mit nur wenigen Code‑Zeilen.

## Voraussetzungen

- .NET 6.0 oder höher (der Code funktioniert auch mit .NET Core und .NET Framework)  
- Eine gültige Aspose.OCR‑für‑.NET‑Lizenz (oder die kostenlose Testversion) – Sie erhalten sie auf der Aspose‑Website.  
- Ein Ordner, der die PNG‑Dateien enthält, die Sie lesen möchten.  
- Visual Studio 2022 (oder jede andere C#‑kompatible IDE).  

Keine zusätzlichen NuGet‑Pakete sind über `Aspose.OCR` hinaus erforderlich.

## Schritt 1: Wie man OCR verwendet – Initialisieren der Aspose OCR‑Engine

Das Erste, was Sie benötigen, ist eine Instanz der Klasse `Engine`. Dieses Objekt kapselt die zugrunde liegende OCR‑Technologie und kann je nach Hardware und Lizenz auf CPU oder GPU laufen.

```csharp
using System;
using System.Collections.Generic;
using System.Collections.Concurrent;
using System.Threading.Tasks;
using Aspose.OCR;

// Create an OCR engine (CPU by default; GPU can be enabled via EngineSettings if licensed)
var ocrEngine = new Engine();
```

*Warum das wichtig ist:* Die Engine einmal zu initialisieren und über Threads hinweg wiederzuverwenden spart Speicher und vermeidet den Overhead, OCR‑Modelle wiederholt zu laden. Außerdem garantiert es konsistente Einstellungen für alle Bilder.

## Schritt 2: Text aus PNG extrahieren – Bildpfade sammeln

Als Nächstes benötigen wir eine Sammlung von Dateipfaden. In einem echten Projekt würden Sie das Verzeichnis dynamisch auslesen, aber zur Übersichtlichkeit listen wir hier ein paar Beispiel‑Dateien auf.

```csharp
// List the PNG files you want to process
var imagePaths = new List<string>
{
    "YOUR_DIRECTORY/img1.png",
    "YOUR_DIRECTORY/img2.png",
    "YOUR_DIRECTORY/img3.png"
};
```

*Tipp:* Ersetzen Sie `YOUR_DIRECTORY` durch den absoluten oder relativen Pfad zu Ihren Bildern. Wenn Sie Dutzende von Dateien haben, können Sie die manuelle Auflistung durch `Directory.GetFiles("YOUR_DIRECTORY", "*.png")` ersetzen.

## Schritt 3: Bilder stapelweise OCR‑verarbeiten – Erkennung parallel ausführen

Bilder nacheinander zu verarbeiten ist einfach, aber langsam. Mit `Parallel.ForEach` können wir **mehrere Bilder gleichzeitig** verarbeiten und so die Vorteile von Mehrkern‑CPUs nutzen.

```csharp
// Helper method that performs the parallel recognition
static IReadOnlyList<OcrResult> RecognizeImagesInParallel(Engine engine, IEnumerable<string> paths)
{
    var resultsBag = new ConcurrentBag<OcrResult>();

    Parallel.ForEach(paths, path =>
    {
        // Load the image stream (Aspose handles various formats)
        var image = ImageStream.FromFile(path);
        // Perform OCR
        OcrResult result = engine.Recognize(image);
        // Store the result safely for later use
        resultsBag.Add(result);
    });

    return resultsBag.ToArray();
}

// Execute the parallel OCR
var ocrResults = RecognizeImagesInParallel(ocrEngine, imagePaths);
```

*Warum parallel?* Jeder OCR‑Aufruf ist CPU‑intensiv, aber unabhängig, sodass ein gleichzeitiges Ausführen die Gesamtlaufzeit erheblich verkürzen kann, besonders auf Maschinen mit 4 Kernen oder mehr.

## Schritt 4: Mehrere Bilder verarbeiten – Extrahierten Text anzeigen

Jetzt, wo wir eine Sammlung von `OcrResult`‑Objekten haben, können wir über sie iterieren und den erkannten Text ausgeben. Normalerweise würden Sie die Ausgabe in einer Datenbank speichern oder in Dateien schreiben, aber die Konsolenausgabe hält das Beispiel kompakt.

```csharp
int index = 1;
foreach (var result in ocrResults)
{
    Console.WriteLine($"--- Image {index++} ---");
    Console.WriteLine(result.Text);
}
```

**Erwartete Konsolenausgabe (Beispiel):**

```
--- Image 1 ---
Hello world! This is the first image.
--- Image 2 ---
Invoice #12345
Total: $250.00
--- Image 3 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
```

Falls ein Bild nicht geladen werden kann, wirft Aspose eine Ausnahme; Sie können den Aufruf `engine.Recognize` in einen try/catch‑Block einbetten, um Fehler zu protokollieren, ohne den gesamten Stapel abzubrechen.

## Schritt 5: Vollständiges Beispiel – Alle Teile zusammen

Unten finden Sie das komplette Programm, das Sie in ein neues C#‑Konsolenprojekt kopieren können. Es enthält alles von den `using`‑Anweisungen bis zur abschließenden Ausgabeschleife.

```csharp
using System;
using System.Collections.Generic;
using System.Collections.Concurrent;
using System.Threading.Tasks;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // Step 1: Initialize the OCR engine
        var ocrEngine = new Engine();

        // Step 2: Define the PNG files to process
        var imagePaths = new List<string>
        {
            "YOUR_DIRECTORY/img1.png",
            "YOUR_DIRECTORY/img2.png",
            "YOUR_DIRECTORY/img3.png"
        };

        // Step 3: Run OCR in parallel
        var ocrResults = RecognizeImagesInParallel(ocrEngine, imagePaths);

        // Step 4: Output the recognized text
        int index = 1;
        foreach (var result in ocrResults)
        {
            Console.WriteLine($"--- Image {index++} ---");
            Console.WriteLine(result.Text);
        }
    }

    // Helper method for parallel OCR
    static IReadOnlyList<OcrResult> RecognizeImagesInParallel(Engine engine, IEnumerable<string> paths)
    {
        var resultsBag = new ConcurrentBag<OcrResult>();

        Parallel.ForEach(paths, path =>
        {
            try
            {
                var image = ImageStream.FromFile(path);
                OcrResult result = engine.Recognize(image);
                resultsBag.Add(result);
            }
            catch (Exception ex)
            {
                // Log the error but keep the batch running
                Console.Error.WriteLine($"Error processing {path}: {ex.Message}");
            }
        });

        return resultsBag.ToArray();
    }
}
```

### Ausführen des Beispiels

1. Erstellen Sie ein neues **Console App**‑Projekt in Visual Studio.  
2. Fügen Sie das **Aspose.OCR**‑NuGet‑Paket hinzu (`Install-Package Aspose.OCR`).  
3. Ersetzen Sie `YOUR_DIRECTORY` durch den Pfad, der Ihre PNG‑Dateien enthält.  
4. Builden und starten Sie das Projekt – Sie sollten den extrahierten Text in der Konsole sehen.

## Profi‑Tipps & Sonderfälle

- **GPU‑Beschleunigung:** Wenn Sie eine kompatible GPU und eine lizenzierte Aspose OCR besitzen, aktivieren Sie sie über `EngineSettings`, bevor Sie die Engine erstellen. Das kann Sekunden pro Bild einsparen.  
- **Große Dateien:** Für Bilder größer als 10 MB sollten Sie sie zuerst verkleinern, um den Speicherverbrauch zu reduzieren.  
- **Sprachunterstützung:** Standardmäßig geht die Engine von Englisch aus. Setzen Sie `engine.Language = Language.French;` (oder eine andere unterstützte Sprache), um die Genauigkeit bei nicht‑englischem Text zu erhöhen.  
- **Fehlerbehandlung:** Der `try/catch`‑Block innerhalb der parallelen Schleife sorgt dafür, dass eine beschädigte Datei nicht den gesamten Stapel abbricht. Sie können Fehlermeldungen auch in eine Datei protokollieren, um sie später zu prüfen.  
- **Ergebnis‑Speicherung:** Anstatt die Ausgabe zu drucken, können Sie `result.Text` in eine `.txt`‑Datei schreiben mit `File.WriteAllText(Path.ChangeExtension(path, ".txt"))`.

## Fazit

Sie wissen jetzt, **wie man OCR** in C# einsetzt, um **Text aus PNG**‑Dateien zu **extrahieren**, **Bilder stapelweise OCR‑zu verarbeiten** und **mehrere Bilder** effizient mit Aspose OCR C# zu bearbeiten. Die Lösung ist komplett eigenständig, läuft parallel und lässt sich leicht erweitern, um Hunderte oder Tausende von Dateien mit minimalen Änderungen zu verarbeiten.

Bereit für den nächsten Schritt? Ersetzen Sie die Konsolenausgabe durch einen CSV‑Report, experimentieren Sie mit GPU‑Beschleunigung oder speisen Sie den OCR‑Text in einen Suchindex ein. Die Möglichkeiten sind endlos, und das Kernmuster — einmal initialisieren, parallel ausführen, Fehler elegant behandeln — wird Ihnen in jeder Bild‑Verarbeitungspipeline gute Dienste leisten.

Viel Spaß beim Coden und mögen Ihre OCR‑Jobs schnell und fehlerfrei sein!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}