---
category: general
date: 2026-04-26
description: Wie man PNG‑Bilder schnell stapelweise per OCR verarbeitet. Erfahren
  Sie, wie Sie Text aus PNG extrahieren, Bilder in Text umwandeln, erkannten Text
  schreiben und ein PNG‑Verzeichnis mit Aspose OCR lesen.
draft: false
keywords:
- how to batch OCR
- extract text from png
- convert images to text
- write recognized text
- read png directory
language: de
og_description: Wie man PNG‑Bilder in C# stapelweise mit Aspose OCR verarbeitet. Dieser
  Leitfaden zeigt, wie man Text aus PNG extrahiert, Bilder in Text umwandelt und den
  erkannten Text effizient schreibt.
og_title: Wie man PNG‑Bilder stapelweise mit OCR in C# verarbeitet – Schritt für Schritt
tags:
- OCR
- C#
- Aspose
title: Wie man PNG‑Bilder stapelweise in C# OCRt – Vollständige Anleitung
url: /de/net/text-recognition/how-to-batch-ocr-png-images-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man PNG-Bilder in C# stapelweise OCR durchführt – Komplettanleitung

Haben Sie sich jemals gefragt, **wie man stapelweise OCR** für einen ganzen Ordner von PNG‑Dateien durchführt, ohne für jedes Bild ein separates Programm zu schreiben? Sie sind nicht der Einzige, der Dutzende von Screenshots, gescannte Quittungen oder Grafiken jongliert, die in durchsuchbaren Text umgewandelt werden müssen. In diesem Tutorial führen wir Sie durch eine praxisnahe Lösung, die **Text aus PNG extrahiert**, **Bilder in Text umwandelt** und **erkannten Text** in einzelne Dateien schreibt – und dabei das PNG‑Verzeichnis automatisch ausliest.

Am Ende dieses Leitfadens haben Sie eine sofort einsatzbereite C#‑Konsolen‑App, die beliebig viele Bilder in einem Durchgang verarbeitet. Keine zusätzlichen Skripte, kein manuelles Kopieren‑Einfügen – nur reiner Code, der die schwere Arbeit für Sie übernimmt.

## Was Sie benötigen

- **.NET 6.0** oder höher (der Code funktioniert auch auf .NET Framework).  
- **Aspose.OCR for .NET** NuGet‑Paket (die kostenlose Testversion funktioniert zum Testen).  
- Ein Ordner mit einer Handvoll *.png*-Dateien, die Sie OCR‑verarbeiten möchten.  
- Visual Studio 2022 oder jede andere C#‑IDE Ihrer Wahl.

Wenn Sie das haben, können wir direkt mit der Implementierung beginnen.

## Schritt 1 – Bereiten Sie Ihre Eingabe‑ und Ausgabeverzeichnisse vor *(PNG‑Verzeichnis lesen)*

Das Erste, was wir tun, ist das Programm auf den Ordner zu verweisen, der die Bilder enthält, und festzulegen, wo die resultierenden *.txt*-Dateien abgelegt werden sollen. Die Verwendung von `Directory.GetFiles` liefert uns ein sauberes Enumerable aller PNG‑Dateien im Verzeichnis.

```csharp
using System;
using System.Collections.Generic;
using System.IO;

// Define where the source PNGs are and where the OCR results will be saved
string inputFolder = @"C:\MyProject\BatchImages";   // <-- change to your path
string outputFolder = @"C:\MyProject\BatchOutput";

// Ensure the output folder exists; create it if it doesn’t
if (!Directory.Exists(outputFolder))
{
    Directory.CreateDirectory(outputFolder);
}

// Grab every *.png* file – this is the “read png directory” part
IEnumerable<string> inputImageFiles = Directory.GetFiles(inputFolder, "*.png");
```

**Warum das wichtig ist:**  
- Die Verwendung eines Wildcards (`*.png`) stellt sicher, dass nur Bilddateien verarbeitet werden und andere Dokumente ignoriert werden.  
- Das Erstellen des Ausgabeverzeichnisses zur Laufzeit verhindert später eine `DirectoryNotFoundException`.

> **Pro‑Tipp:** Wenn Sie weitere Formate unterstützen müssen (JPEG, BMP), erweitern Sie einfach das Suchmuster oder rufen Sie `Directory.EnumerateFiles` mit mehreren Erweiterungen auf.

## Schritt 2 – Initialisieren Sie die OCR‑Engine *(Bilder in Text umwandeln)*

Aspose.OCR liefert zwei Engine‑Typen: eine CPU‑basierte `OcrEngine` und eine GPU‑beschleunigte `GpuOcrEngine`. Für die meisten Stapelaufgaben ist die CPU‑Engine völlig ausreichend, aber Sie können den Klassennamen austauschen, wenn Sie über eine geeignete GPU verfügen.

```csharp
using Aspose.OCR;

// Initialise the OCR engine – CPU version
OcrEngine ocrEngine = new OcrEngine();   // Use new GpuOcrEngine() for GPU acceleration

// Set the language to Latin (covers English, French, Spanish, etc.)
ocrEngine.Language = Language.Latin;
```

**Warum das wichtig ist:**  
- Die Angabe der Sprache verbessert die Genauigkeit erheblich, da die Engine weiß, welchen Zeichensatz sie erwarten soll.  
- Der Wechsel zu `GpuOcrEngine` ist eine einzeilige Änderung, falls Sie bei großen Stapeln Leistungsengpässe feststellen.

## Schritt 3 – Erstellen Sie einen Batch‑Recognizer

Aspose stellt einen praktischen `BatchRecognizer` bereit, der ein Enumerable von Dateipfaden akzeptiert und die Ergebnisse einzeln zurückliefert. Dadurch wird vermieden, dass alle Bilder gleichzeitig in den Speicher geladen werden – ein entscheidendes Detail für große Ordner.

```csharp
// Build a batch recogniser that will use the previously configured engine
BatchRecognizer batchRecognizer = new BatchRecognizer(ocrEngine);
```

**Warum das wichtig ist:**  
- Der Batch‑Recognizer kapselt die Schleifenlogik, sodass wir uns darauf konzentrieren können, was mit jedem Ergebnis geschehen soll, anstatt wie man sicher iteriert.

## Schritt 4 – OCR auf allen Bildern ausführen und die Ausgabe schreiben *(Erkannten Text schreiben)*

Jetzt führen wir das OCR tatsächlich aus. Die Methode `Recognize` gibt ein `IEnumerable<RecognitionResult>` zurück, wobei jedes Ergebnis den extrahierten Text und weitere Metadaten enthält.

```csharp
// Perform OCR on the entire collection of PNG files
IEnumerable<RecognitionResult> recognitionResults = batchRecognizer.Recognize(inputImageFiles);

// Write each recognised text to a separate *.txt* file
int fileIndex = 0;
foreach (RecognitionResult result in recognitionResults)
{
    // Build a unique output filename – out_0.txt, out_1.txt, …
    string outputPath = Path.Combine(outputFolder, $"out_{fileIndex++}.txt");

    // Save the plain text to disk
    File.WriteAllText(outputPath, result.Text);
}
```

**Warum das wichtig ist:**  
- Die Verwendung von `File.WriteAllText` stellt sicher, dass der Text standardmäßig mit UTF‑8‑Kodierung gespeichert wird, wodurch Sonderzeichen erhalten bleiben.  
- Die inkrementelle Benennung (`out_0.txt`, `out_1.txt`) entspricht der Verarbeitungsreihenfolge, was beim Debuggen hilfreich ist.

> **Randfall:** Wenn ein Bild nicht OCR‑verarbeitet werden kann (z. B. beschädigte Datei), ist `RecognitionResult.Text` leer. Sie können innerhalb der Schleife eine einfache Prüfung hinzufügen, um Fehler zu protokollieren:

```csharp
if (string.IsNullOrWhiteSpace(result.Text))
{
    Console.WriteLine($"Warning: No text extracted from {inputImageFiles.ElementAt(fileIndex - 1)}");
}
```

## Schritt 5 – Alles zusammenführen – Vollständiges funktionierendes Beispiel

Unten finden Sie das vollständige Programm, das Sie in ein neues Konsolenprojekt kopieren‑und‑einfügen können. Es enthält die `using`‑Direktiven, Ordner‑Validierung und eine kleine Konsolen‑UI, damit Sie wissen, wann der Stapel abgeschlossen ist.

```csharp
// ---------------------------------------------------------------
// Batch OCR for PNG files using Aspose.OCR
// ---------------------------------------------------------------
using System;
using System.Collections.Generic;
using System.IO;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // 1️⃣ Define input & output directories
        string inputFolder = @"C:\MyProject\BatchImages";   // <-- adjust
        string outputFolder = @"C:\MyProject\BatchOutput";

        if (!Directory.Exists(inputFolder))
        {
            Console.WriteLine($"Error: Input folder does not exist -> {inputFolder}");
            return;
        }

        if (!Directory.Exists(outputFolder))
            Directory.CreateDirectory(outputFolder);

        // 2️⃣ Gather all PNG files
        IEnumerable<string> inputImageFiles = Directory.GetFiles(inputFolder, "*.png");
        Console.WriteLine($"Found {inputImageFiles?.Count() ?? 0} PNG files to process.");

        // 3️⃣ Initialise OCR engine (CPU) and set language
        OcrEngine ocrEngine = new OcrEngine();   // Swap with GpuOcrEngine() if needed
        ocrEngine.Language = Language.Latin;

        // 4️⃣ Create batch recogniser
        BatchRecognizer batchRecognizer = new BatchRecognizer(ocrEngine);

        // 5️⃣ Run OCR and write results
        IEnumerable<RecognitionResult> results = batchRecognizer.Recognize(inputImageFiles);
        int index = 0;
        foreach (RecognitionResult result in results)
        {
            string outPath = Path.Combine(outputFolder, $"out_{index++}.txt");
            File.WriteAllText(outPath, result.Text);
        }

        Console.WriteLine($"✅ OCR complete! Text files saved to {outputFolder}");
    }
}
```

**Erwartete Ausgabe:**  
Beim Ausführen des Programms wird etwa Folgendes ausgegeben:

```
Found 12 PNG files to process.
✅ OCR complete! Text files saved to C:\MyProject\BatchOutput
```

Und Sie sehen `out_0.txt` … `out_11.txt` im Ausgabeverzeichnis, wobei jede Datei die reine Textversion des jeweiligen Bildes enthält.

## Häufige Fragen & Tipps

| Frage | Antwort |
|----------|--------|
| *Kann ich auch Unterordner OCR‑verarbeiten?* | Ja – ersetzen Sie `Directory.GetFiles` durch `Directory.EnumerateFiles(inputFolder, "*.png", SearchOption.AllDirectories)`. |
| *Was, wenn ich eine andere Sprache benötige?* | Setzen Sie `ocrEngine.Language = Language.Spanish;` (oder ein beliebiges unterstütztes Enum). |
| *Wie gehe ich mit riesigen Stapeln (tausende Dateien) um?* | Erwägen Sie die Verarbeitung in Chunks oder die Verwendung von `Parallel.ForEach` mit einer gedrosselten Parallelitätsgrad, um Speicherüberlastungen zu vermeiden. |
| *Ist die Ausgabe immer UTF‑8?* | `File.WriteAllText` verwendet standardmäßig UTF‑8 ohne BOM, was für die meisten latinbasierten Sprachen funktioniert. Für asiatische Schriften müssen Sie ggf. `Encoding.UTF8` explizit setzen. |
| *Kann ich Vertrauenswerte erhalten?* | `RecognitionResult` stellt `Confidence` bereit – Sie können diesen zusammen mit dem Text protokollieren, um die Qualität zu kontrollieren. |

## Visuelle Übersicht *(Wie man stapelweise OCR durchführt – Diagramm)*

![Wie der Batch‑OCR‑Workflow aussieht: Eingabeordner → OCR‑Engine → Batch‑Recognizer → Ausgabedateien](https://example.com/diagram-how-to-batch-ocr.png "Wie man stapelweise OCR")

*Der Alt‑Text enthält das Haupt‑Keyword und erfüllt die SEO‑Bildanforderungen.*

## Fazit

Wir haben gerade **wie man stapelweise OCR** für ein Verzeichnis von PNG‑Dateien mit Aspose.OCR durchführt, vom Auslesen des PNG‑Verzeichnisses bis zum Schreiben jeder erkannten Textdatei, behandelt. Die Lösung ist vollständig eigenständig, funktioniert auf jeder modernen .NET‑Runtime und kann für GPU‑Beschleunigung, Mehrsprachunterstützung oder Parallelverarbeitung erweitert werden.

Bereit für den nächsten Schritt? Versuchen Sie, `Language.Latin` durch eine andere Sprache zu ersetzen, oder integrieren Sie die Ausgabe in einen Suchindex, damit Ihre Dokumente sofort durchsuchbar werden. Der Himmel ist die Grenze, sobald Sie stapelweise OCR gemeistert haben.

Viel Spaß beim Coden, und lassen Sie mich in den Kommentaren wissen, falls Sie auf Probleme stoßen!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}