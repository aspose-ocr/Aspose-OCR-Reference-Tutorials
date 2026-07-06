---
category: general
date: 2026-03-05
description: Konvertieren Sie TIFF in Text in C# mit Aspose OCR – extrahieren Sie
  schnell Text aus gescannten Bilddateien und lernen Sie, wie Sie Bilddateien in C#
  für die OCR‑Verarbeitung laden.
draft: false
keywords:
- convert TIFF to text
- extract text scanned image
- load image file C#
language: de
og_description: Konvertieren Sie TIFF in Text in C# mit Aspose OCR. Erfahren Sie den
  kompletten Workflow zum Extrahieren von Text aus gescannten Bildern und zum effizienten
  Laden von Bilddateien.
og_title: TIFF in Text konvertieren in C# – Gescannten Bildtext extrahieren
tags:
- OCR
- C#
- Aspose
title: TIFF in Text konvertieren in C# – Gescannten Bildtext extrahieren
url: /de/net/text-recognition/convert-tiff-to-text-in-c-extract-scanned-image-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# TIFF in Text konvertieren in C# – Gescannten Bildtext extrahieren

Müssen Sie **TIFF in Text in C# konvertieren**? Sie sind nicht der Einzige, der mit mehrseitigen gescannten Bildern kämpft, die sich hartnäckig weigern, in durchsuchbare Zeichenketten umzuwandeln.  
In diesem Leitfaden führen wir Sie durch eine vollständige, sofort einsatzbereite Lösung, die eine TIFF‑Datei nimmt, sie an Aspose OCR übergibt und reinen Text ausgibt – ohne zusätzliche Dienste, ohne versteckte Magie.

> **Profi‑Tipp:** Wenn Sie hochauflösende Scans verarbeiten, kann das Aktivieren der GPU‑Verarbeitung Sekunden pro Seite einsparen.

Wir zeigen Ihnen außerdem, wie Sie **gescannte Bilddateien extrahieren** und den besten Weg, **Bilddatei in C# zu laden** in die OCR‑Engine, sodass Sie diese Logik noch heute in jedes .NET‑Projekt einbetten können.

---

## Was Sie benötigen

Bevor wir starten, stellen Sie sicher, dass Sie Folgendes auf Ihrem Rechner haben:

| Anforderung | Grund |
|-------------|-------|
| .NET 6.0+ (oder .NET Framework 4.7.2+) | Moderne Laufzeit, unterstützt `Span<T>` und asynchrones I/O |
| Aspose.OCR for .NET (NuGet‑Paket `Aspose.OCR`) | Die OCR‑Engine, die wir verwenden |
| Eine gültige Aspose OCR‑Lizenzdatei (`Aspose.OCR.lic`) | Ohne sie stoßen Sie auf Evaluationsbeschränkungen |
| Eine TIFF‑Datei (ein‑ oder mehrseitig) zum Testen | Verwendetes Beispiel: `scanned_multi_page.tif` |
| GPU mit CUDA 11+ (optional) | Beschleunigt die Erkennung, wenn `EngineMode = Gpu` |

Wenn Ihnen etwas davon fehlt, holen Sie sich jetzt das NuGet‑Paket:

```bash
dotnet add package Aspose.OCR
```

---

## Schritt 1: Projekt einrichten und Namespaces importieren

Erstellen Sie eine neue Konsolenanwendung (oder fügen Sie den Code zu einem bestehenden Projekt hinzu). Das Erste, was wir tun, ist die Klassen zu importieren, die wir benötigen.

```csharp
using System;
using Aspose.OCR;          // Core OCR classes
using Aspose.OCR.Image;   // ImageStream helper
```

> **Warum das wichtig ist:** Das Importieren von `Aspose.OCR.Image` liefert uns die `ImageStream`‑Factory, die TIFF‑Dateien direkt von der Festplatte oder einem Stream lesen kann. Das Überspringen dieses Schrittes führt zu einem Kompilierfehler.

---

## Schritt 2: OCR‑Engine initialisieren und Verarbeitungsmodus wählen

Die OCR‑Engine muss **vor** der Zuweisung eines Bildes konfiguriert werden. Hier entscheiden wir, ob wir auf der CPU laufen oder die GPU nutzen.

```csharp
// Step 2: Initialize the OCR engine and enable GPU processing (must be set before any OCR work)
OcrEngine ocrEngine = new OcrEngine();

// Choose the processing mode that fits your environment.
// Options: Cpu (default) | Gpu | Auto
ocrEngine.EngineMode = OcrEngineMode.Gpu;   // Switch to Cpu if you don’t have a compatible GPU
```

*Wenn Sie auf einem headless‑Server ohne Grafikkarte arbeiten, ändern Sie `Gpu` zu `Cpu` oder `Auto`.*  
Der Engine‑Modus beeinflusst die Speicherzuweisung und Geschwindigkeit; der GPU‑Modus kann bei großen, hochauflösenden TIFFs 2‑3× schneller sein.

---

## Schritt 3: Ihre Aspose OCR‑Lizenz anwenden

Der Betrieb ohne Lizenz beschränkt Sie auf wenige Seiten und Wasserzeichen. Laden Sie Ihre Lizenz früh, damit jede nachfolgende Operation uneingeschränkt ist.

```csharp
// Step 3: Apply the Aspose OCR license (replace with your own license file if needed)
ocrEngine.SetLicense("Aspose.OCR.lic");
```

> **Häufiges Problem:** Wenn `SetLicense` nach `Recognize()` platziert wird, fällt die Engine für diesen Aufruf in den Testmodus zurück.

---

## Schritt 4: TIFF‑Datei laden – Umgang mit ein‑ und mehrseitigen Bildern

Aspose OCR kann mehrseitige TIFFs sofort lesen, aber Sie müssen den richtigen Stream übergeben. Hier ein robustes Muster, das für beide Szenarien funktioniert.

```csharp
// Step 4: Load the image to be recognized
string tiffPath = @"YOUR_DIRECTORY\scanned_multi_page.tif";

using (var imageStream = ImageStream.FromFile(tiffPath))
{
    // Step 5: Assign the image to the engine
    ocrEngine.Image = imageStream;

    // Step 6: Perform the OCR operation
    OcrResult ocrResult = ocrEngine.Recognize();

    // Step 7: Output the recognized text
    Console.WriteLine("=== OCR Output ===");
    Console.WriteLine(ocrResult.Text);
}
```

### Warum `ImageStream.FromFile` verwenden?

- Es abstrahiert den zugrunde liegenden `FileStream` und behandelt die TIFF‑Seitenaufzählung intern.  
- Es funktioniert auch mit `MemoryStream`, sodass Sie Bilder aus einer Datenbank oder einer Web‑API laden können, ohne das Dateisystem zu berühren.

### Randfall: Sehr große TIFFs

Wenn Ihr TIFF 200 MB überschreitet, sollten Sie es seitenweise laden, um Out‑of‑Memory‑Ausnahmen zu vermeiden:

```csharp
int pageCount = ImageInfo.GetPageCount(tiffPath);
for (int i = 0; i < pageCount; i++)
{
    using var pageStream = ImageStream.FromFile(tiffPath, i);
    ocrEngine.Image = pageStream;
    var pageResult = ocrEngine.Recognize();
    Console.WriteLine($"--- Page {i + 1} ---");
    Console.WriteLine(pageResult.Text);
}
```

---

## Schritt 5: Ausgabe überprüfen

Wenn Sie das Programm ausführen, sollten Sie etwa Folgendes sehen:

```
=== OCR Output ===
Invoice #12345
Date: 2024‑12‑01
Total: $1,250.00
Thank you for your business!
```

Wenn der Text unleserlich aussieht, prüfen Sie Folgendes:

1. **Auflösung** – OCR funktioniert am besten mit 300 dpi oder höher.  
2. **EngineMode** – Wechseln Sie zu `Cpu`, wenn der GPU‑Treiber veraltet ist.  
3. **Lizenz** – Stellen Sie sicher, dass der Pfad zur Lizenzdatei korrekt ist und die Datei lesbar ist.

---

## Häufig gestellte Fragen (FAQ)

### Funktioniert das mit anderen Bildformaten?

Absolut. `ImageStream.FromFile` unterstützt JPEG, PNG, BMP und sogar PDF (via Aspose.PDF). Ersetzen Sie einfach die Dateierweiterung.

### Was, wenn ich Bilder verarbeiten muss, die in einer Datenbank gespeichert sind?

Lesen Sie das BLOB in einen `MemoryStream` und übergeben Sie es an `ImageStream.FromStream(memoryStream)`. Die OCR‑Engine behandelt es genauso wie einen dateibasierten Stream.

### Kann ich das unter Linux ausführen?

Ja – Aspose OCR ist plattformübergreifend. Installieren Sie das passende .NET‑Runtime und stellen Sie sicher, dass die erforderlichen nativen Bibliotheken für die GPU (falls verwendet) verfügbar sind.

---

## Vollständiges funktionierendes Beispiel (Copy‑Paste‑bereit)

Unten finden Sie das gesamte Programm, bereit zum Kompilieren. Ersetzen Sie `YOUR_DIRECTORY` und den Pfad zur Lizenzdatei durch Ihre tatsächlichen Pfade.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Image;

namespace TiffToTextDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Initialize OCR engine
            OcrEngine ocrEngine = new OcrEngine();

            // Choose processing mode: Gpu, Cpu, or Auto
            ocrEngine.EngineMode = OcrEngineMode.Gpu; // Change to Cpu if no GPU

            // Apply license (skip if you only need a trial)
            ocrEngine.SetLicense("Aspose.OCR.lic");

            // Path to the TIFF file
            string tiffPath = @"YOUR_DIRECTORY\scanned_multi_page.tif";

            // Load the TIFF (handles multi‑page automatically)
            using (var imageStream = ImageStream.FromFile(tiffPath))
            {
                // Assign image to engine
                ocrEngine.Image = imageStream;

                // Run OCR
                OcrResult result = ocrEngine.Recognize();

                // Display result
                Console.WriteLine("=== OCR Output ===");
                Console.WriteLine(result.Text);
            }

            // Optional: Process each page individually for huge files
            // int pages = ImageInfo.GetPageCount(tiffPath);
            // for (int i = 0; i < pages; i++) { ... }
        }
    }
}
```

Speichern Sie dies als `Program.cs`, führen Sie `dotnet run` aus und beobachten Sie den Text

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}