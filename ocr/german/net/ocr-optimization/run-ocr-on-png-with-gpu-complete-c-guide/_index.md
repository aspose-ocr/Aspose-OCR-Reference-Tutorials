---
category: general
date: 2026-01-02
description: Führen Sie OCR auf PNG schnell mit Aspose OCR und GPU‑Unterstützung aus.
  Erfahren Sie, wie Sie Text aus einem Bild erkennen, Text aus einem Bild extrahieren
  und das GPU‑Speicherlimit festlegen.
draft: false
keywords:
- run OCR on PNG
- recognize text from image
- extract text from image
- how to extract text
- set GPU memory limit
language: de
og_description: Führen Sie OCR auf PNG effizient mit Aspose OCR und GPU-Beschleunigung
  aus. Dieses Tutorial zeigt Ihnen, wie Sie Text aus einem Bild erkennen, Text aus
  einem Bild extrahieren und die GPU-Speichernutzung steuern.
og_title: OCR auf PNG mit GPU ausführen – Vollständiger C# Leitfaden
tags:
- OCR
- C#
- GPU
title: OCR auf PNG mit GPU ausführen – Vollständiger C#‑Leitfaden
url: /de/net/ocr-optimization/run-ocr-on-png-with-gpu-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR auf PNG mit GPU ausführen – Vollständiger C#‑Leitfaden

Haben Sie jemals **OCR auf PNG**‑Dateien ausführen müssen, aber sind an die Leistungsgrenze gestoßen? Sie sind nicht allein. In vielen realen Pipelines kann ein einzelnes hochauflösendes PNG einen rein CPU‑basierten OCR‑Engine ausbremsen und aus einer schnellen Abfrage eine minute‑lange Wartezeit machen.

Die gute Nachricht ist, dass Aspose OCR mit GPU‑Erweiterungen geliefert wird, die es Ihnen ermöglichen, **recognize text from image**‑Dateien in einem Bruchteil der Zeit zu verarbeiten. In diesem Tutorial führen wir Sie durch ein praktisches Beispiel, das genau zeigt, wie Sie **run OCR on PNG** mit C# ausführen, wie Sie **extract text from image** durchführen und sogar, wie Sie **set GPU memory limit** festlegen, damit Sie im Rahmen Ihres Hardware‑Budgets bleiben.

Wir werden außerdem das „Wie“ und das „Warum“ jedes Schrittes behandeln, sodass Sie mit einem soliden mentalen Modell davon gehen – nicht nur mit einem Copy‑Paste‑Snippet.

## Was Sie lernen werden

- Die Voraussetzungen für die Nutzung der GPU‑Unterstützung von Aspose OCR.  
- Wie man ein PNG in ein `Bitmap` lädt und es an die OCR‑Engine übergibt.  
- Wie man `GpuDevice` und `GpuMemoryLimitMb` für optimale Leistung konfiguriert.  
- Wie man **recognize text from image** durchführt und das Klartext‑Ergebnis abruft.  
- Tipps zum Umgang mit gängigen Randfällen wie GPUs mit wenig Speicher oder mehrseitigen PNGs.  

Am Ende dieses Leitfadens können Sie **run OCR on PNG**‑Dateien mit GPU‑Geschwindigkeit ausführen und den Speicherverbrauch Ihrer OCR‑Aufgaben sicher steuern.

![Diagramm, das OCR auf PNG mit GPU‑Beschleunigung zeigt](run-ocr-on-png-diagram.png "Beispiel für OCR auf PNG")

## Voraussetzungen

Bevor wir beginnen, stellen Sie sicher, dass Sie Folgendes haben:

1. .NET 6.0 oder höher (der Code funktioniert auch mit .NET Core und .NET Framework).  
2. Eine NVIDIA‑GPU mit CUDA‑Unterstützung (das Beispiel wählt Geräte‑Index 0).  
3. Das Aspose.OCR‑NuGet‑Paket und seine GPU‑Erweiterungen (`Aspose.OCR.Extensions`).  
4. Ein Beispiel‑PNG (`input.png`) in einem Ordner, den Sie aus Ihrem Projekt referenzieren können.  

Falls Ihnen etwas davon unbekannt ist, keine Sorge – wir werden an den relevanten Stellen Alternativen erwähnen.

---

## Schritt 1 – Aspose OCR und GPU‑Erweiterungen installieren

Zuerst das Wichtigste. Ohne die richtigen Bibliotheken lässt sich der restliche Code nicht kompilieren.

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Extensions
```

Das Paket `Aspose.OCR.Extensions` zieht die nativen CUDA‑Binärdateien, die für die GPU‑Beschleunigung erforderlich sind, mit ein.  
*Pro‑Tipp:* Wenn Sie auf einem Rechner ohne GPU arbeiten, können Sie das Projekt trotzdem kompilieren; setzen Sie später einfach `PreferGpu = false`.

---

## Schritt 2 – Das zu verarbeitende PNG laden

Jetzt führen wir tatsächlich **run OCR on PNG** aus, indem wir es in ein `Bitmap` laden. Dieser Schritt ist einfach, aber einen kurzen Hinweis wert: `Bitmap` erwartet einen Dateipfad, also stellen Sie sicher, dass der Pfad relativ zu Ihrer ausführbaren Datei korrekt ist.

```csharp
using System.Drawing;        // Bitmap handling
using Aspose.OCR;
using Aspose.OCR.Extensions; // GPU support extensions

// ...

// Step 2: Load the PNG image
string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "YOUR_DIRECTORY", "input.png");
Bitmap imageBitmap = new Bitmap(imagePath);
```

Falls das PNG ungewöhnlich groß ist (z. B. > 5000 px pro Seite), sollten Sie es zuerst verkleinern, um das Auslasten des GPU‑Speichers zu vermeiden. Dort kommt später die Option **set GPU memory limit** ins Spiel.

---

## Schritt 3 – OCR‑Engine für GPU‑Nutzung erstellen und konfigurieren

Hier ist das Herzstück des Tutorials: die OCR‑Engine so zu konfigurieren, dass sie **recognize text from image** mit der GPU verwendet. Zwei Eigenschaften sind entscheidend:

- `GpuDevice` – wählt das zu verwendende CUDA‑Gerät aus.  
- `GpuMemoryLimitMb` – begrenzt die Menge des GPU‑Speichers, die die Engine zuweisen darf.

```csharp
// Step 3: Initialize OCR engine with GPU settings
OcrEngine ocrEngine = new OcrEngine()
{
    // Pick the first CUDA device (index 0)
    GpuDevice = GpuDeviceInfo.GetDevice(0),

    // Optional: limit GPU memory consumption (in MB)
    GpuMemoryLimitMb = 2048   // Adjust based on your GPU's VRAM
};
```

**Warum ein Speicherlimit setzen?** Einige GPUs teilen den Speicher mit dem Display oder führen mehrere Workloads gleichzeitig aus. Durch das Begrenzen der Zuweisung verhindern Sie Out‑of‑Memory‑Abstürze, besonders beim parallelen Verarbeiten vieler PNGs.

---

## Schritt 4 – Erkennungsoptionen festlegen (Sprache & GPU‑Präferenz)

Das Objekt `RecognitionOptions` teilt der Engine mit, nach welcher Sprache gesucht werden soll und ob **prefer GPU** selbst für kleine Bilder verwendet werden soll. Für die meisten englischen Dokumente ist das ausreichend, aber Sie können `Language.English` durch andere unterstützte Locale ersetzen.

```csharp
// Step 4: Set recognition options
RecognitionOptions recognitionOptions = new RecognitionOptions
{
    Language = Language.English,
    PreferGpu = true // Force GPU path even for smaller images
};
```

Falls Sie jemals **extract text from image** in einer anderen Sprache als Englisch benötigen, ändern Sie einfach das `Language`‑Enum. Die Bibliothek unterstützt von Haus aus Dutzende von Sprachen.

---

## Schritt 5 – OCR ausführen und Ergebnis abrufen

Wenn alles verkabelt ist, besteht der abschließende Aufruf aus einer einzigen Zeile, die tatsächlich **run OCR on PNG** ausführt und ein umfangreiches Ergebnisobjekt zurückgibt.

```csharp
// Step 5: Perform OCR
OcrResult ocrResult = ocrEngine.Recognize(imageBitmap, recognitionOptions);

// Output the extracted text
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);
```

Das `OcrResult` enthält nicht nur den Klartext (`ocrResult.Text`), sondern auch Konfidenzwerte, Begrenzungsrahmen und sogar das Originalbild mit hervorgehobenen Wörtern – nützlich, wenn Sie die Extraktion debuggen oder visualisieren müssen.

**Erwartete Ausgabe** (für ein Beispiel‑PNG, das „Hello World“ sagt):

```
=== OCR Output ===
Hello World
```

Falls der Text verzerrt erscheint, prüfen Sie, ob das PNG nicht beschädigt ist und ob das GPU‑Speicherlimit nicht zu niedrig für die Bildgröße ist.

---

## Schritt 6 – Umgang mit Randfällen und bewährte Vorgehensweisen

### GPUs mit wenig Speicher

Wenn Sie eine Ausnahme wie `CudaException: out of memory` sehen, reduzieren Sie `GpuMemoryLimitMb` oder teilen Sie das PNG vor der Verarbeitung in Kacheln auf. Das Kacheln kann mit `Graphics.DrawImage` auf einem `Bitmap`‑Klon durchgeführt werden.

### Mehrere PNGs im Batch

Beim Verarbeiten eines Ordners mit PNGs sollten Sie dieselbe `OcrEngine`‑Instanz wiederverwenden – die einmalige Initialisierung spart GPU‑Kontextwechsel.

```csharp
foreach (var file in Directory.GetFiles("images", "*.png"))
{
    using var bmp = new Bitmap(file);
    var result = ocrEngine.Recognize(bmp, recognitionOptions);
    Console.WriteLine($"{Path.GetFileName(file)}: {result.Text}");
}
```

### Rückgriff auf CPU

Falls keine GPU verfügbar ist, setzen Sie einfach `PreferGpu = false`. Die Engine wechselt automatisch ohne Codeänderungen zur CPU zurück.

```csharp
recognitionOptions.PreferGpu = false; // Safe CPU path
```

---

## Vollständiges funktionierendes Beispiel

Unten finden Sie das komplette Programm, das Sie in ein neues Konsolenprojekt kopieren‑und‑einfügen können. Es enthält alle oben genannten Schritte sowie einige Sicherheitsprüfungen.

```csharp
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Extensions; // GPU support extensions

class GpuExample
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Load the PNG image
        // -------------------------------------------------
        string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory,
                                         "YOUR_DIRECTORY", "input.png");

        if (!File.Exists(imagePath))
        {
            Console.Error.WriteLine($"File not found: {imagePath}");
            return;
        }

        using Bitmap imageBitmap = new Bitmap(imagePath);

        // -------------------------------------------------
        // Step 2: Initialize OCR engine with GPU settings
        // -------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine()
        {
            GpuDevice = GpuDeviceInfo.GetDevice(0), // First CUDA device
            GpuMemoryLimitMb = 2048                  // Adjust as needed
        };

        // -------------------------------------------------
        // Step 3: Set recognition options
        // -------------------------------------------------
        RecognitionOptions recognitionOptions = new RecognitionOptions
        {
            Language = Language.English,
            PreferGpu = true // Force GPU even for small images
        };

        // -------------------------------------------------
        // Step 4: Perform OCR
        // -------------------------------------------------
        OcrResult ocrResult = ocrEngine.Recognize(imageBitmap, recognitionOptions);

        // -------------------------------------------------
        // Step 5: Output the extracted text
        // -------------------------------------------------
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

Speichern Sie die Datei als `Program.cs`, führen Sie `dotnet run` aus, und Sie sollten den extrahierten Text in der Konsole sehen.

---

## Fazit

Wir haben gerade gezeigt, wie man **run OCR on PNG**‑Dateien mit den GPU‑Erweiterungen von Aspose OCR ausführt, wie man **recognize text from image** durchführt und wie man **extract text from image** ausführt, während man das **set GPU memory limit** kontrolliert. Durch die Konfiguration von `GpuDevice` und `GpuMemoryLimitMb` bleibt Ihre Anwendung schnell und stabil, selbst auf bescheidenen GPUs.

Ab hier könnten Sie:

- Mit anderen Sprachen experimentieren (`Language.French`, `Language.Spanish`).  
- Den OCR‑Schritt in eine größere Dokument‑Verarbeitungspipeline integrieren.  
- Nachbearbeitung hinzufügen, z. B. Rechtschreibprüfung oder Entitätsextraktion, um den Rohtext zu verfeinern.  

Denken Sie daran, der Schlüssel liegt nicht nur im Code, sondern im Verständnis, warum jede Einstellung wichtig ist. Wenn Sie wissen, wie man **set GPU memory limit** verwendet und wann man zur CPU zurückkehrt, bauen Sie OCR‑Lösungen, die sich elegant skalieren.

Haben Sie Fragen zu einer bestimmten PNG‑Größe, mehrseitigen TIFFs oder zur Fehlersuche bei GPU‑Fehlern? Hinterlassen Sie unten einen Kommentar, und viel Spaß beim Programmieren!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}