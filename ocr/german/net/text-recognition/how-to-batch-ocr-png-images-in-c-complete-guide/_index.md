---
category: general
date: 2026-03-17
description: Wie man PNG‑Bilder in C# schnell stapelweise OCR verarbeitet. Erfahren
  Sie, wie Sie Text aus PNG‑Dateien extrahieren, PNG in Text konvertieren und Bilder
  aus einem Verzeichnis mit einem einfachen Skript lesen.
draft: false
keywords:
- how to batch OCR
- extract text png
- convert png to text
- read images from directory
language: de
og_description: Wie man PNG‑Bilder stapelweise mit OCR in C# verarbeitet – Schritt‑für‑Schritt‑Code.
  Text aus PNG‑Dateien extrahieren, PNG in Text konvertieren und Bilder mühelos aus
  einem Verzeichnis lesen.
og_title: Wie man PNG‑Bilder stapelweise OCR in C# durchführt – Vollständiger Leitfaden
tags:
- OCR
- C#
- Image Processing
title: Wie man PNG‑Bilder stapelweise OCR in C# durchführt – Vollständiger Leitfaden
url: /de/net/text-recognition/how-to-batch-ocr-png-images-in-c-complete-guide/
---

produce final content with translations, preserving all markdown.

Check for any missed items: The image alt text and title changed. Ensure code block placeholders remain unchanged.

Now produce final answer.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man PNG-Bilder in C# stapelweise OCR durchführt – Vollständige Anleitung

Haben Sie sich jemals gefragt, **wie man stapelweise OCR** auf einen Ordner voller Screenshots anwendet, ohne jede Datei manuell zu öffnen? Sie sind nicht der Einzige – Entwickler fragen ständig, wie man große PNG‑Sammlungen stapelweise OCR durchführt, besonders wenn das Ziel ist, Text‑PNG‑Dateien für nachgelagerte Analysen zu extrahieren.  

In diesem Tutorial führen wir ein sofort einsatzbereites C#‑Beispiel durch, das **Text‑PNG**‑Dateien extrahiert, **PNG in Text** konvertiert und Ihnen die beste Methode zeigt, **Bilder aus Verzeichnis zu lesen**. Am Ende haben Sie ein einzelnes Skript, das neben jedem Bild eine `.txt`‑Datei ablegt und Ihnen Stunden manuelles Kopieren‑Einfügen spart.

## Was Sie erreichen werden

- Einen OCR‑Engine einmal initialisieren und für den gesamten Batch wiederverwenden.  
- Jedes `*.png` in einem angegebenen Ordner scannen, ohne selbst eine Schleife zu schreiben.  
- Jeden OCR‑Ergebnis in eine eigene Textdatei schreiben und dabei den ursprünglichen Dateinamen beibehalten.  
- Häufige Randfälle wie leere Ordner oder Nicht‑Bild‑Dateien elegant behandeln.

### Voraussetzungen

- .NET 6.0 oder höher (der Code funktioniert auch auf .NET Core und .NET Framework).  
- Eine OCR‑Bibliothek, die die Typen `OcrEngine`, `ImageStream` und `OcrResult` bereitstellt (z. B. das fiktive **FastOCR** SDK, das in den Snippets verwendet wird).  
- Grundkenntnisse in C# – keine fortgeschrittenen Muster erforderlich.

---

## Wie man PNG-Bilder stapelweise OCR durchführt – Überblick

Unten finden Sie das **vollständige, ausführbare Programm**. Sie können es gerne in ein neues Konsolenprojekt kopieren, die Platzhalter‑Pfade ersetzen und **F5** drücken.

```csharp
using System;
using System.IO;
using System.Linq;
using FastOCR;               // <-- Replace with your actual OCR namespace

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Initialize the OCR engine (language = English)
        // -------------------------------------------------
        var ocrEngine = new OcrEngine();
        ocrEngine.Config.Language = Language.English;

        // -------------------------------------------------
        // Step 2: Locate every PNG file in the input folder
        // -------------------------------------------------
        string inputFolder = @"YOUR_DIRECTORY\images";
        string[] imagePaths = Directory.GetFiles(inputFolder, "*.png");

        if (imagePaths.Length == 0)
        {
            Console.WriteLine("No PNG files found – nothing to process.");
            return;
        }

        // -------------------------------------------------
        // Step 3: Convert file paths to ImageStream objects
        // -------------------------------------------------
        var imageStreams = imagePaths
            .Select(path => ImageStream.FromFile(path))
            .ToList();

        // -------------------------------------------------
        // Step 4: Recognize text in the entire batch
        // -------------------------------------------------
        IReadOnlyList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);

        // -------------------------------------------------
        // Step 5: Write each result to a .txt file next to the image
        // -------------------------------------------------
        string outputFolder = @"YOUR_DIRECTORY\output";
        Directory.CreateDirectory(outputFolder); // ensures the folder exists

        for (int i = 0; i < ocrResults.Count; i++)
        {
            string originalFileName = Path.GetFileNameWithoutExtension(imagePaths[i]);
            string outputPath = Path.Combine(outputFolder, $"{originalFileName}.txt");
            File.WriteAllText(outputPath, ocrResults[i].Text);
            Console.WriteLine($"✅ {originalFileName}.txt created");
        }

        Console.WriteLine("All done! Check the output folder for your text files.");
    }
}
```

> **Erwartete Ausgabe:** Für jedes `image01.png` finden Sie eine `image01.txt`‑Datei, die die erkannten Zeichen enthält. Die Konsole listet jede Datei auf, sobald sie geschrieben wird.

![Diagramm zum stapelweisen OCR](how-to-batch-ocr-diagram.png "Diagramm, das das stapelweise OCR von PNG‑Bildern mit C# veranschaulicht")

---

## Schritt‑für‑Schritt‑Erklärung

### 1. OCR‑Engine initialisieren – das Herz des Prozesses  

Die Zeile `var ocrEngine = new OcrEngine();` erstellt eine einzelne Engine‑Instanz, die für den gesamten Batch wiederverwendet wird. Das Wiederverwenden der Engine ist **entscheidend**, weil die meisten OCR‑Bibliotheken beim Erzeugen schwere Ressourcen (wie Sprachmodelle) allokieren. Einmalige Initialisierung verbessert die Leistung erheblich – besonders wenn Sie Dutzende oder Hunderte von PNGs haben.

> **Pro‑Tipp:** Wenn Sie eine andere Sprache als Englisch benötigen, setzen Sie `ocrEngine.Config.Language = Language.Spanish;` (oder ein beliebiges unterstütztes Enum).

### 2. Bilder aus Verzeichnis lesen – jedes PNG finden  

`Directory.GetFiles(@"YOUR_DIRECTORY\images", "*.png")` tut genau das, was das sekundäre Schlüsselwort *read images from directory* verspricht. Es gibt ein Array von absoluten Pfaden zurück, das wir später an die OCR‑Engine übergeben.  

> **Warum nicht `SearchOption.AllDirectories` verwenden?** Wenn Ihre Bilder verschachtelt sind, können Sie zu `GetFiles(path, "*.png", SearchOption.AllDirectories)` wechseln. Denken Sie jedoch daran, dass tiefere Scans unerwünschte Dateien einbeziehen können, also filtern Sie entsprechend.

### 3. Dateipfade in ImageStream‑Objekte konvertieren  

Die meisten OCR‑SDKs erwarten einen Stream statt eines rohen Pfads. Der LINQ‑Ausdruck `Select(path => ImageStream.FromFile(path)).ToList()` erstellt eine **Liste von Streams**, die der Batch‑Erkenner in einem Aufruf verarbeiten kann. Dieser Schritt stellt außerdem sicher, dass Dateihandles nur einmal geöffnet werden, wodurch der I/O‑Overhead reduziert wird.

> **Randfall:** Wenn eine Datei beschädigt ist, kann `ImageStream.FromFile` eine Ausnahme werfen. Wickeln Sie die Konvertierung in ein `try/catch`, falls Sie Resilienz benötigen.

### 4. Text im gesamten Batch erkennen  

`ocrEngine.RecognizeBatch(imageStreams)` ist der optimale Ansatz für *how to batch OCR*. Anstatt über jedes Bild zu iterieren und eine Einzelbild‑Methode aufzurufen, übergeben wir die gesamte Sammlung an die Engine. Intern kann die Bibliothek die Arbeit parallelisieren, was Ihnen auf Mehrkern‑Maschinen einen Geschwindigkeitsschub gibt.

> **Tipp:** Wenn Ihre OCR‑Bibliothek keine Batch‑Methode bereitstellt, können Sie dennoch eine ähnliche Leistung erzielen, indem Sie `Parallel.ForEach` um den Einzelbild‑`Recognize`‑Aufruf herum verwenden.

### 5. Jeden OCR‑Ergebnis schreiben – PNG in Text konvertieren  

Die abschließende `for`‑Schleife schreibt `ocrResults[i].Text` in eine `.txt`‑Datei, deren Name das ursprüngliche PNG spiegelt. Das entspricht genau dem sekundären Schlüsselwort *convert PNG to text*. Der Aufruf `Path.Combine` stellt sicher, dass das Ausgabeverzeichnis existiert und verhindert Pfad‑Traversal‑Fehler.

> **Häufiges Problem:** Wenn das Ausgabeverzeichnis nicht vorher erstellt wird, führt das zu einer `DirectoryNotFoundException`. Die Zeile `Directory.CreateDirectory(outputFolder);` löst das proaktiv.

---

## Umgang mit realen Variationen

| Situation | Was zu ändern ist | Warum |
|-----------|-------------------|-------|
| **Leerer Eingabeordner** | Behalten Sie die frühe `if (imagePaths.Length == 0)`‑Abfrage bei | Verhindert einen unnötigen OCR‑Aufruf und gibt eine freundliche Meldung aus |
| **Gemischte Dateitypen** | Verwenden Sie `Directory.EnumerateFiles(..., "*.*", SearchOption.TopDirectoryOnly).Where(f => f.EndsWith(".png", StringComparison.OrdinalIgnoreCase))` | Stellt sicher, dass nur PNGs verarbeitet werden, was *extract text png* ohne Fehler erfüllt |
| **Große Bilder ( > 5 MB )** | Skalieren Sie vor dem OCR‑Einspeisen herunter: `ImageStream.FromFile(path).Resize(1920, 1080)` (falls die API dies unterstützt) | Reduziert den Speicherbedarf und verbessert häufig die Erkennungsgenauigkeit |
| **Andere OCR‑Sprache** | Setzen Sie `ocrEngine.Config.Language = Language.French;` | Passt die Engine an die Sprache der Quellbilder an |

---

## Häufig gestellte Fragen (FAQ)

**F: Funktioniert das mit JPEG‑ oder TIFF‑Dateien?**  
A: Die Kernlogik bleibt gleich; ändern Sie einfach das Suchmuster zu `"*.jpg"` oder `"*.tif"` und stellen Sie sicher, dass die OCR‑Bibliothek diese Formate dekodieren kann.

**F: Wie kann ich Tausende von Bildern verarbeiten, ohne dass der Speicher ausgeht?**  
A: Ersetzen Sie den Batch‑Aufruf durch einen Streaming‑Ansatz – verarbeiten Sie beispielsweise jeweils 50 Bilder und geben Sie die Streams frei, bevor Sie den nächsten Block laden.

**F: Ich benötige den OCR‑Vertrauenswert. Wo finde ich ihn?**  
A: Die meisten `OcrResult`‑Objekte stellen eine `Confidence`‑Eigenschaft bereit. Sie können den Schreib‑Schritt erweitern:

```csharp
var result = ocrResults[i];
string content = $"Confidence: {result.Confidence:P2}\n{result.Text}";
File.WriteAllText(outputPath, content);
```

---

## Abschluss

Wir haben gerade **wie man stapelweise OCR** auf PNG‑Bilder in C# von Anfang bis Ende behandelt. Durch das Initialisieren einer einzelnen Engine, das Lesen von Bildern aus dem Verzeichnis, das Konvertieren in Streams, das Erkennen des gesamten Batches und schließlich das Schreiben jedes Ergebnisses in eine Textdatei haben Sie nun ein solides, produktionsreifes Muster für die Aufgaben **extract text PNG**, **convert PNG to text** und **read images from directory**.

Was kommt als Nächstes? Versuchen Sie, den OCR‑Anbieter zu wechseln, fügen Sie mehr‑threaded Nachverarbeitung hinzu (z. B. Rechtschreibprüfung) oder speisen Sie die `.txt`‑Dateien in einen Suchindex ein. Der Himmel ist die Grenze, sobald Sie den Batch‑Workflow gemeistert haben.

Haben Sie eine Variante, die Sie teilen möchten? Hinterlassen Sie einen Kommentar und happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}