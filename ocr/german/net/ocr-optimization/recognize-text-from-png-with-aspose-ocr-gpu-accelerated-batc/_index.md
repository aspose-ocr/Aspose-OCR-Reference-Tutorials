---
category: general
date: 2026-04-01
description: Erfahren Sie, wie Sie Text aus PNG-Dateien schnell erkennen, indem Sie
  die GPU‑Geräte‑ID festlegen und die GPU‑Beschleunigung in Aspose OCR aktivieren.
  Schritt‑für‑Schritt‑C#‑Anleitung.
draft: false
keywords:
- recognize text from png
- set gpu device id
- Aspose OCR GPU
- batch OCR C#
- OCR performance tips
language: de
og_description: Erkennen Sie Text aus PNG-Dateien schnell, indem Sie die GPU-Geräte-ID
  festlegen. Folgen Sie diesem vollständigen C#‑Leitfaden, um die GPU‑Beschleunigung
  mit Aspose OCR zu aktivieren.
og_title: Text aus PNG erkennen – GPU‑beschleunigtes Aspose OCR Tutorial
tags:
- C#
- OCR
- GPU
- Aspose
title: Text aus PNG mit Aspose OCR erkennen – GPU‑beschleunigtes Batch‑Demo
url: /de/net/ocr-optimization/recognize-text-from-png-with-aspose-ocr-gpu-accelerated-batc/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Text aus PNG erkennen – Vollständiges C# GPU‑beschleunigtes Batch‑Tutorial

Haben Sie jemals **Text aus PNG**‑Bildern erkennen müssen, fanden den Prozess aber quälend langsam? Sie sind nicht allein. Die meisten Entwickler starten mit einem einfachen OCR‑Aufruf und starren dann auf eine Konsole, die sich wie eine Schnecke bewegt, wenn ein Ordner Dutzende von Screenshots enthält.  

Die gute Nachricht? Aspose OCR kann die schwere Arbeit auf Ihre Grafikkarte auslagern, und mit nur ein paar Zeilen können Sie **set gpu device id** setzen, um die gewünschte GPU auszuwählen. In diesem Leitfaden gehen wir Schritt für Schritt durch ein vollständiges, ausführbares Beispiel, das jedes PNG aus einem Ordner holt, GPU‑Beschleunigung aktiviert, die erste GPU auswählt und die Zeichenanzahl für jede Datei ausgibt.

Am Ende haben Sie ein eigenständiges Programm, das Sie in jedes .NET‑Projekt einbinden können, und Sie verstehen, warum das Aktivieren der GPU wichtig ist, wie Sie Randfälle behandeln und was Sie für noch bessere Leistung anpassen können.

## Was Sie benötigen

- **.NET 6.0** oder höher (der Code kompiliert auch mit .NET Core).  
- Das **Aspose.OCR**‑NuGet‑Paket – installieren Sie es mit `dotnet add package Aspose.OCR`.  
- Einen Rechner mit einer CUDA‑kompatiblen GPU (typischerweise NVIDIA) und dem passenden Treiber.  
- Einen Ordner voller **PNG**‑Bilder, die Sie verarbeiten möchten.  

Falls Ihnen eines dieser Elemente unbekannt ist, keine Panik. Die nachfolgenden Schritte enthalten die genauen Befehle, die Sie benötigen, und wir besprechen auch, was zu tun ist, wenn keine GPU vorhanden ist.

## Schritt 1: OCR‑Engine initialisieren und GPU‑Beschleunigung aktivieren  

Das Erste, was Sie tun müssen, ist eine `OcrEngine`‑Instanz zu erstellen und die GPU‑Unterstützung zu aktivieren. Dieses Flag weist Aspose an, die nativen CUDA‑Bibliotheken im Hintergrund zu verwenden.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU‑specific namespace
using System;

class GpuBatchDemo
{
    static void Main()
    {
        // Initialise the OCR engine
        var ocrEngine = new OcrEngine();

        // Enable GPU acceleration – huge speed boost for large batches
        ocrEngine.UseGpuAcceleration = true;
```

**Warum das wichtig ist:** Ohne `UseGpuAcceleration` wird jedes Bild auf der CPU verarbeitet, was insbesondere bei hochauflösenden PNGs um Größenordnungen langsamer sein kann. Das Aktivieren des Flags bereitet die Engine außerdem darauf vor, später ein bestimmtes GPU‑Gerät zu akzeptieren.

## Schritt 2: GPU‑Geräte‑ID setzen (optional, aber empfohlen)  

Wenn Ihr Arbeitsplatz mehr als eine GPU hat, können Sie entscheiden, welche verwendet werden soll. Die Geräte‑IDs beginnen bei **0**, sodass `0` die erste GPU, `1` die zweite usw. auswählt.

```csharp
        // Optional: Choose the GPU device – 0 selects the first GPU
        ocrEngine.GpuDeviceId = 0;   // <-- set gpu device id
```

**Pro‑Tipp:** Auf einem gemeinsam genutzten Server kann das explizite Setzen der GPU‑Geräte‑ID verhindern, dass Ihr Job Ressourcen von anderen Prozessen übernimmt. Wenn Sie diese Zeile weglassen, wählt Aspose das Standardgerät, was bei einer Einzel‑GPU‑Konfiguration normalerweise in Ordnung ist.

## Schritt 3: Alle PNG‑Dateien aus Ihrem Batch‑Ordner sammeln  

Als Nächstes müssen wir jedes PNG finden, das Sie mit OCR verarbeiten wollen. Die Methode `Directory.GetFiles` übernimmt die schwere Arbeit.

```csharp
        // Retrieve all PNG images from the batch folder
        string[] imageFiles = System.IO.Directory.GetFiles(
            @"YOUR_DIRECTORY\Batch",   // <-- replace with your path
            "*.png",                  // only PNG files
            System.IO.SearchOption.TopDirectoryOnly);
```

**Randfall:** Wenn der Ordner leer ist, ist `imageFiles` ein leeres Array. Das behandeln wir später mit einer freundlichen Meldung.

## Schritt 4: Jede Bilddatei verarbeiten und die erkannte Zeichenanzahl ausgeben  

Jetzt die Kernschleife. Für jedes PNG rufen wir `Recognize` auf und geben dann den Dateinamen sowie die Länge des extrahierten Textes aus.

```csharp
        // Verify we actually found files
        if (imageFiles.Length == 0)
        {
            Console.WriteLine("No PNG files found in the specified folder.");
            return;
        }

        // Process each image and display the recognised character count
        foreach (var imagePath in imageFiles)
        {
            var ocrResult = ocrEngine.Recognize(imagePath);
            Console.WriteLine($"{System.IO.Path.GetFileName(imagePath)} → {ocrResult.Text.Length} chars");
        }
    }
}
```

**Was Sie sehen werden:**  
```
invoice1.png → 342 chars
receipt_2023.png → 127 chars
screenshot.png → 0 chars
```

Enthält ein Bild keinen Text, ist die Anzahl `0`. Das ist völlig normal für Screenshots, die rein grafisch sind.

## Schritt 5: Das Programm ausführen und GPU‑Nutzung überprüfen  

Kompilieren Sie die Datei (`dotnet build`) und führen Sie sie aus (`dotnet run`). Während die Konsole scrollt, können Sie Ihr GPU‑Monitoring‑Tool (wie NVIDIA Smi) öffnen, um den kurzen Nutzungssprung der GPU für jedes Bild zu sehen. Wenn Sie keine Aktivität sehen, prüfen Sie folgendes:

1. Der CUDA‑Treiber ist installiert.  
2. `UseGpuAcceleration` ist auf `true` gesetzt.  
3. Die korrekte `GpuDeviceId` entspricht einer physischen GPU.

Ist die GPU nicht verfügbar, fällt Aspose automatisch auf die CPU zurück, wobei Sie den Geschwindigkeitsvorteil verlieren.

## Häufige Varianten & Tipps  

| Situation | Was zu ändern ist |
|-----------|-------------------|
| **Anderes Bildformat** (z. B. JPEG) | Ändern Sie das Suchmuster zu `*.jpg` oder `*.*` und Aspose erkennt den Text weiterhin. |
| **Batch‑Größe ist riesig** (tausende Dateien) | Verarbeiten Sie in Chunks, um Speicherdruck zu vermeiden: teilen Sie `imageFiles` in kleinere Arrays. |
| **Benötigen Sie den eigentlichen Text, nicht nur die Länge** | Ersetzen Sie `ocrResult.Text.Length` durch `ocrResult.Text` im `WriteLine`. |
| **Ausführung auf einem headless Server** | Stellen Sie sicher, dass der Server einen GPU‑Treiber hat; andernfalls setzen Sie `UseGpuAcceleration = false`, um unnötige Fehler zu vermeiden. |
| **Mehrere GPUs, Last ausbalancieren** | Schleifen Sie über `ocrEngine.GpuDeviceId = i % gpuCount` innerhalb des `foreach`, um Geräte zu rotieren. |

## Erwartete Ausgabe & Verifizierung  

Wenn alles funktioniert, gibt die Konsole für jede Datei den Dateinamen gefolgt von der Zeichenanzahl aus, wie oben gezeigt. Um die eigentliche OCR‑Ausgabe zu prüfen, können Sie temporär den Text ausgeben:

```csharp
Console.WriteLine($"{Path.GetFileName(imagePath)} → {ocrResult.Text}");
```

Denken Sie daran, diese Zeile für große Batches zu entfernen oder zu kommentieren; das Ausgeben von tausenden Zeilen kann Ihr Terminal überfluten.

## Vollständiges, lauffähiges Beispiel (Copy‑Paste‑bereit)

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU‑specific namespace
using System;

class GpuBatchDemo
{
    static void Main()
    {
        // Step 1: Initialise the OCR engine and enable GPU acceleration
        var ocrEngine = new OcrEngine();
        ocrEngine.UseGpuAcceleration = true;

        // Step 2: (Optional) Choose the GPU device – 0 selects the first GPU
        ocrEngine.GpuDeviceId = 0;   // <-- set gpu device id

        // Step 3: Retrieve all PNG images from the batch folder
        string[] imageFiles = System.IO.Directory.GetFiles(
            @"YOUR_DIRECTORY\Batch",   // replace with your folder path
            "*.png",
            System.IO.SearchOption.TopDirectoryOnly);

        // Guard clause if no files are found
        if (imageFiles.Length == 0)
        {
            Console.WriteLine("No PNG files found in the specified folder.");
            return;
        }

        // Step 4: Process each image and display the recognised character count
        foreach (var imagePath in imageFiles)
        {
            var ocrResult = ocrEngine.Recognize(imagePath);
            Console.WriteLine($"{System.IO.Path.GetFileName(imagePath)} → {ocrResult.Text.Length} chars");
        }
    }
}
```

Speichern Sie dies als `GpuBatchDemo.cs`, führen Sie `dotnet add package Aspose.OCR` aus und dann `dotnet run`. Sie sollten die Zeichenanzahlen fast sofort für jedes PNG sehen, dank GPU‑Beschleunigung.

## Fazit  

Sie wissen jetzt, wie Sie **Text aus PNG**‑Dateien effizient erkennen, indem Sie GPU‑Beschleunigung aktivieren und explizit **set gpu device id** in Aspose OCR setzen. Das komplette Copy‑and‑Paste‑Programm übernimmt die Ordnererkennung, Randfall‑Prüfungen und gibt Ihnen sofortiges Feedback zur OCR‑Leistung.  

Nächste Schritte? Ersetzen Sie den Aufruf `Recognize` durch `ocrEngine.RecognizeAsync`, wenn Sie eine nicht‑blockierende Verarbeitung benötigen, oder experimentieren Sie mit verschiedenen Bild‑Vorverarbeitungsoptionen (z. B. Binarisierung), die Aspose bereitstellt. Sie könnten die OCR‑Ergebnisse auch in eine Datenbank oder einen Suchindex einspeisen, um eine Volltextsuche zu ermöglichen.

Haben Sie Fragen zur Verarbeitung von mehrseitigen PDFs oder möchten Sie Aspose OCR mit Tesseract vergleichen? Hinterlassen Sie einen Kommentar oder erkunden Sie unsere anderen Tutorials zu **batch OCR C#**, **OCR performance tips** und **GPU‑gesteuerter Bildverarbeitung**. Viel Spaß beim Coden!  

![Console output showing recognised character counts for PNG files – recognize text from png using GPU acceleration](image-placeholder.png "recognize text from png output example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}