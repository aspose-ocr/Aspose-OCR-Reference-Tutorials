---
category: general
date: 2026-04-26
description: Extrahiere Text schnell aus PNG-Dateien mit C#. Erfahre, wie du Bilder
  in Text umwandelst, PNG-Dateien liest, durch Bilder iterierst und OCR-Bilder in
  Minuten stapelweise verarbeitest.
draft: false
keywords:
- extract text from png
- convert images to text
- read png files
- loop through images
- batch ocr images
language: de
og_description: Extrahiere Text aus PNG‑Dateien schnell mit C#. Dieser Leitfaden zeigt,
  wie man Bilder in Text umwandelt, PNG‑Dateien liest, durch Bilder iteriert und Bilder
  stapelweise per OCR verarbeitet.
og_title: Text aus PNG extrahieren – Vollständiges C# Batch-OCR‑Tutorial
tags:
- C#
- OCR
- Aspose
title: Text aus PNG extrahieren – Vollständiges C#‑Batch‑OCR‑Tutorial
url: /de/net/text-recognition/extract-text-from-png-complete-c-batch-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Text aus PNG extrahieren – Komplettes C# Batch‑OCR‑Tutorial

Haben Sie schon einmal **Text aus PNG**‑Dateien extrahieren müssen, wussten aber nicht, wo Sie anfangen sollen? Sie sind nicht allein – viele Entwickler stoßen an diese Hürde, wenn sie zum ersten Mal OCR auf einem Ordner mit Screenshots anwenden. Die gute Nachricht: Mit ein paar Zeilen C# und Aspose OCR können Sie Bilder in Text umwandeln, PNG‑Dateien lesen, über Bilder iterieren und alles in einem Durchgang stapelweise verarbeiten.  

In diesem Tutorial führen wir Sie durch eine sofort lauffähige Konsolen‑App, die genau das tut. Am Ende haben Sie eine eigenständige Lösung, die den Text aus jedem PNG in einem Verzeichnis extrahiert und eine passende `.txt`‑Datei neben jedem Bild ablegt. Keine zusätzlichen Skripte, kein manuelles Kopieren – nur reiner Code.

## Was Sie benötigen

- **.NET 6 SDK** (oder jede neuere .NET‑Version). Es ist kostenlos, schnell und funktioniert überall.
- **Aspose.OCR für .NET** (das NuGet‑Paket). Die Bibliothek unterstützt GPU‑Beschleunigung, wenn Sie über eine kompatible GPU verfügen, fällt aber automatisch auf die CPU zurück.
- Ein Ordner mit ein paar **PNG‑Bildern**, die Sie verarbeiten möchten.  
- Ein Text‑Editor oder eine IDE – Visual Studio, VS Code, Rider – ganz nach Ihrem Geschmack.

Das war’s. Wenn Sie das bereits haben, können Sie loslegen.

![extract text from png example](image.png "extract text from png demo screenshot")

*Bild‑Alt‑Text: „Text aus PNG mit C# Batch‑OCR extrahieren“*

## Schritt 1 – Projekt einrichten und Aspose.OCR installieren

Zuerst ein neues Konsolen‑Projekt erstellen und das Aspose‑OCR‑Paket hinzufügen.

```bash
dotnet new console -n PngOcrBatch
cd PngOcrBatch
dotnet add package Aspose.OCR
```

Warum eine Konsolen‑App? Sie ist der einfachste Host für Batch‑Jobs und lässt sich über die Befehlszeile ausführen oder mit einem Task‑Runner planen. Wenn Sie später eine UI benötigen, können Sie die Kernlogik einfach in eine Klassenbibliothek auslagern.

## Schritt 2 – GPU‑beschleunigte OCR‑Engine initialisieren (oder CPU‑Fallback)

Aspose bietet eine `GpuOcrEngine`, die automatisch eine unterstützte GPU erkennt. Wird keine gefunden, wechselt sie zur regulären CPU‑Engine – kein zusätzlicher Code nötig.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // Create the OCR engine – GPU if available, otherwise CPU
        OcrEngine ocrEngine = new GpuOcrEngine();
        ocrEngine.Language = Language.Latin;   // Latin covers most Western alphabets

        // The rest of the code lives in a separate method for clarity
        ProcessFolder(ocrEngine, @"C:\MyPngFolder");
    }

    // …
}
```

**Pro‑Tipp:** Auf einem headless Server ohne GPU können Sie `GpuOcrEngine` durch `OcrEngine` ersetzen; das Verhalten bleibt identisch.

## Schritt 3 – Durch Bilder im Zielverzeichnis iterieren

Wir müssen **Bilder durchlaufen** und nur PNG‑Dateien auswählen. Die Methode `Directory.GetFiles` übernimmt die schwere Arbeit, und wir schützen uns gegen einen leeren Ordner.

```csharp
static void ProcessFolder(OcrEngine engine, string folderPath)
{
    if (!Directory.Exists(folderPath))
    {
        Console.WriteLine($"❌ Folder not found: {folderPath}");
        return;
    }

    // Grab every *.png file – this is the “read png files” part
    string[] pngFiles = Directory.GetFiles(folderPath, "*.png", SearchOption.TopDirectoryOnly);

    if (pngFiles.Length == 0)
    {
        Console.WriteLine("⚠️ No PNG files found. Make sure the folder contains .png images.");
        return;
    }

    foreach (var pngPath in pngFiles)
    {
        Console.WriteLine($"🔎 Processing: {Path.GetFileName(pngPath)}");
        ExtractAndSave(engine, pngPath);
    }
}
```

Beachten Sie die Verwendung von `SearchOption.TopDirectoryOnly`. Wenn Sie später Unterordner rekursiv durchsuchen wollen, wechseln Sie einfach zu `AllDirectories`. Diese kleine Änderung ermöglicht es Ihnen, **Bilder in Text zu konvertieren** in einem gesamten Verzeichnisbaum mit nur einer Zeile.

## Schritt 4 – OCR ausführen und Ergebnis speichern

Jetzt kommt der Kern des **Batch‑OCR‑Bilder**‑Workflows. Wir laden jedes PNG, führen `Recognize()` aus und schreiben den extrahierten String in eine `.txt`‑Datei mit gleichem Basisnamen.

```csharp
static void ExtractAndSave(OcrEngine engine, string imagePath)
{
    try
    {
        // Load the PNG into the engine
        engine.Image = ImageStream.FromFile(imagePath);

        // Run recognition – this returns a RecognitionResult object
        RecognitionResult result = engine.Recognize();

        // Build the output path (same name, .txt extension)
        string txtPath = Path.ChangeExtension(imagePath, ".txt");

        // Write the OCR text to disk
        File.WriteAllText(txtPath, result.Text);

        Console.WriteLine($"✅ Saved: {Path.GetFileName(txtPath)}");
    }
    catch (Exception ex)
    {
        // Edge case: corrupted PNG or unsupported format
        Console.WriteLine($"❗ Error processing {Path.GetFileName(imagePath)}: {ex.Message}");
    }
}
```

**Warum in try/catch einbetten?** In realen Bild‑Batches kommt häufig eine beschädigte Datei oder ein PNG mit ungewöhnlichem Farbprofil vor. Das Abfangen der Ausnahme verhindert, dass der gesamte Durchlauf abstürzt, und ermöglicht das Weiterverarbeiten der restlichen Dateien.

## Schritt 5 – Anwendung ausführen und Ausgabe prüfen

Projekt bauen und starten:

```bash
dotnet run
```

Sie sollten eine Konsolen‑Ausgabe ähnlich der folgenden sehen:

```
🔎 Processing: invoice1.png
✅ Saved: invoice1.txt
🔎 Processing: screenshot_2024.png
✅ Saved: screenshot_2024.txt
...
```

Öffnen Sie eine der erzeugten `.txt`‑Dateien – dort steht Ihr extrahierter Text. Ist eine Datei leer, prüfen Sie die Bildqualität; OCR funktioniert am besten bei klaren, kontrastreichen Texten.

### Schnelles Verifikations‑Skript (optional)

Wenn Sie sicherstellen wollen, dass jede PNG‑Datei eine passende Textdatei erhalten hat, führen Sie diesen kleinen PowerShell‑Einzeiler aus:

```powershell
Get-ChildItem -Path "C:\MyPngFolder" -Filter *.png |
  ForEach-Object { 
    $txt = $_.BaseName + ".txt"
    if (-Not (Test-Path $txt)) { Write-Host "Missing: $txt" }
  }
```

## Häufige Varianten & Sonderfälle

| Situation | Was zu ändern ist |
|-----------|-------------------|
| **Nicht‑lateinische Sprachen** (z. B. Kyrillisch) | `ocrEngine.Language = Language.Cyrillic;` |
| **Großer Bild‑Datensatz (>10 000 Dateien)** | `Parallel.ForEach` verwenden, um die Verarbeitung zu beschleunigen, aber GPU‑Speichernutzung im Auge behalten. |
| **Originale Bildreihenfolge beibehalten** | `pngFiles` vor dem `foreach` sortieren (`Array.Sort(pngFiles);`). |
| **Ausführung auf einem CI‑Server ohne GPU** | `GpuOcrEngine` durch `OcrEngine` ersetzen, um GPU‑Initialisierungsfehler zu vermeiden. |
| **Nur Dateien mit einem bestimmten Schlüsselwort verarbeiten** | Nach dem Abrufen von `result.Text` prüfen, ob `result.Text.Contains("Invoice")` ist, bevor die Datei geschrieben wird. |

Diese Anpassungen ermöglichen es Ihnen, die **Bilder‑zu‑Text‑Konvertierung** fast an jede Situation anzupassen, die Ihnen begegnet.

## Vollständiger Quellcode (Copy‑Paste‑bereit)

```csharp
// ------------------------------------------------------------
// Extract Text from PNG – Batch OCR using Aspose.OCR (C#)
// ------------------------------------------------------------
using Aspose.OCR;
using Aspose.OCR.Gpu;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // 1️⃣ Create OCR engine (GPU if possible)
        OcrEngine ocrEngine = new GpuOcrEngine();
        ocrEngine.Language = Language.Latin;

        // 2️⃣ Define the folder that holds your PNG files
        string targetFolder = @"C:\MyPngFolder";   // <-- change to your path

        // 3️⃣ Process every PNG in the folder
        ProcessFolder(ocrEngine, targetFolder);
    }

    static void ProcessFolder(OcrEngine engine, string folderPath)
    {
        if (!Directory.Exists(folderPath))
        {
            Console.WriteLine($"❌ Folder not found: {folderPath}");
            return;
        }

        string[] pngFiles = Directory.GetFiles(folderPath, "*.png", SearchOption.TopDirectoryOnly);

        if (pngFiles.Length == 0)
        {
            Console.WriteLine("⚠️ No PNG files found.");
            return;
        }

        foreach (var pngPath in pngFiles)
        {
            Console.WriteLine($"🔎 Processing: {Path.GetFileName(pngPath)}");
            ExtractAndSave(engine, pngPath);
        }
    }

    static void ExtractAndSave(OcrEngine engine, string imagePath)
    {
        try
        {
            engine.Image = ImageStream.FromFile(imagePath);
            RecognitionResult result = engine.Recognize();

            string txtPath = Path.ChangeExtension(imagePath, ".txt");
            File.WriteAllText(txtPath, result.Text);

            Console.WriteLine($"✅ Saved: {Path.GetFileName(txtPath)}");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"❗ Error on {Path.GetFileName(imagePath)}: {ex.Message}");
        }
    }
}
```

Speichern Sie dies als `Program.cs`, führen Sie `dotnet run` aus und beobachten Sie, wie die Magie geschieht.

## Fazit

Sie haben jetzt eine **komplette, produktionsreife Methode**, um Text aus PNG‑Dateien mit C# zu extrahieren. Das Tutorial hat alles abgedeckt – vom Einrichten des Projekts, Initialisieren einer GPU‑beschleunigten OCR‑Engine, **Durchlaufen von Bildern**, bis zum **Batch‑OCR von Bildern** und dem Speichern der Ergebnisse als Klartext.  

Wenn Sie neugierig auf die nächsten Schritte sind, probieren Sie:

- **Bilder in Text umwandeln** für andere Formate (JPG, BMP

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}