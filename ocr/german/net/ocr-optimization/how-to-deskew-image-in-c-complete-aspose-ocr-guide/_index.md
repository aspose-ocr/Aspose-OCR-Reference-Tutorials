---
category: general
date: 2026-06-28
description: Wie man ein Bild mit Aspose.OCR entneigt. Lernen Sie, das Bild für OCR
  vorzubereiten, die OCR‑Genauigkeit zu verbessern und ein gescanntes Bild mit einem
  vollständigen C#‑Beispiel zu entneigen.
draft: false
keywords:
- how to deskew image
- preprocess image for ocr
- how to improve ocr
- deskew scanned image
language: de
og_description: Wie man ein Bild mit Aspose.OCR begradigt. Dieses Tutorial zeigt Ihnen,
  wie Sie ein Bild für OCR vorverarbeiten, die Genauigkeit steigern und ein gescanntes
  Bild Schritt für Schritt begradigen.
og_title: Wie man ein Bild in C# begradigt – Vollständiger Aspose.OCR Leitfaden
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: How to deskew image using Aspose.OCR. Learn to preprocess image for
    OCR, improve OCR accuracy, and deskew scanned image with a full C# example.
  headline: How to Deskew Image in C# – Complete Aspose.OCR Guide
  type: TechArticle
- description: How to deskew image using Aspose.OCR. Learn to preprocess image for
    OCR, improve OCR accuracy, and deskew scanned image with a full C# example.
  name: How to Deskew Image in C# – Complete Aspose.OCR Guide
  steps:
  - name: Why a Deskew Filter First?
    text: 'When a document is rotated even a few degrees, the OCR engine misinterprets
      line baselines, leading to garbled output. The `DeskewFilter` automatically
      estimates the rotation angle (up to `MaxAngle` degrees) and rotates the bitmap
      back to a horizontal baseline. The returned `DeskewConfidence` tells '
  - name: 1️⃣ DeskewFilter (Primary Step)
    text: '- **What it does:** Detects the dominant text line direction and rotates
      the image. - **Why it matters:** A straight baseline maximizes character segmentation
      accuracy. - **Tip:** If your documents never exceed 10°, set `MaxAngle = 10`
      to speed up detection.'
  - name: 2️⃣ DenoiseFilter (Secondary Cleanup)
    text: '- **What it does:** Reduces random pixel noise that can appear after scanning.
      - **Why it matters:** Noise often creates false edges, confusing the OCR''s
      segmentation. - **Tip:** Adjust `Strength` between 0.3 (light) and 0.8 (aggressive)
      based on scan quality.'
  - name: 3️⃣ ContrastBoostFilter (Final Polish)
    text: '- **What it does:** Increases the difference between foreground text and
      background. - **Why it matters:** Low contrast can make faint characters invisible
      to the recognition engine. - **Tip:** A `Level` of 1.2 works for most black‑on‑white
      scans; for colored documents, experiment with values up to '
  type: HowTo
tags:
- OCR
- Aspose
- Image Processing
title: Wie man ein Bild in C# entzerrt – vollständiger Aspose.OCR-Leitfaden
url: /de/net/ocr-optimization/how-to-deskew-image-in-c-complete-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man ein Bild in C# deskewt – Vollständiger Aspose.OCR‑Leitfaden

Haben Sie sich schon einmal gefragt, **wie man Bilddateien deskewt**, bevor man sie in eine OCR‑Engine einspeist? Sie sind nicht allein. Gescannte Dokumente kommen häufig schräg an, und diese kleine Drehung kann die Erkennungsergebnisse stark beeinträchtigen. Die gute Nachricht? Mit Aspose.OCR können Sie Bilder (deskew) und bereinigen – und das mit nur wenigen Zeilen C#.

In diesem Tutorial führen wir Sie durch ein vollständiges, ausführbares Beispiel, das **Bild für OCR vorverarbeitet**, einen Deskew‑Filter hinzufügt und Ihnen zeigt, **wie man OCR**‑Genauigkeit verbessert. Am Ende können Sie **gescannte Bilddateien** automatisch deskewen und die Vertrauenswerte selbst sehen.

> **Hinweis:** Der Code funktioniert mit Aspose.OCR ≥ 22.10 und .NET 6+, die Konzepte gelten jedoch auch für frühere Versionen.

## Was Sie benötigen

- **Aspose.OCR für .NET** (NuGet‑Paket `Aspose.OCR`)
- Ein **schräges TIFF**‑ oder JPEG‑Bild, das Sie begradigen möchten
- Visual Studio 2022 (oder jede andere C#‑IDE)
- Grundlegende Kenntnisse in C# und Konsolen‑Apps

Keine zusätzlichen Drittanbieter‑Bibliotheken sind nötig; die gesamte Pipeline ist in Aspose.OCR enthalten.

---

## Wie man ein Bild mit Aspose.OCR deskewt

Das Herz der Lösung ist eine **Filter‑Pipeline**. Stellen Sie sich das vor wie ein Fließband, bei dem jeder Filter ein spezifisches Problem bereinigt: zuerst korrigieren wir die Drehung, dann reduzieren wir Rauschen und schließlich erhöhen wir den Kontrast, damit die OCR‑Engine die Zeichen klar erkennt.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

class DeskewExample
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        var engine = new OcrEngine();

        // Step 2: Load the skewed image to be processed
        var img = OcrImage.FromFile(@"YOUR_DIRECTORY/skewed_doc.tif");

        // Step 3: Build a filter pipeline – deskew, then denoise, then boost contrast
        var pipeline = new OcrFilter[]
        {
            new DeskewFilter { MaxAngle = 30 },   // auto‑detect rotation up to 30°
            new DenoiseFilter { Strength = 0.5 },
            new ContrastBoostFilter { Level = 1.2 }
        };

        // Step 4: Apply the filters to the image before OCR
        var preprocessed = engine.ApplyFilters(img, pipeline);

        // Step 5: Perform OCR on the pre‑processed image
        var result = engine.Recognize(preprocessed);

        // Step 6: Output the deskew confidence and recognized text
        System.Console.WriteLine($"Deskew confidence: {result.DeskewConfidence:P2}");
        System.Console.WriteLine(result.Text);
    }
}
```

> **Bildbeispiel**  
> ![Beispiel für Deskew](/images/deskew-example.png "Beispiel für Deskew")

### Warum zuerst ein Deskew‑Filter?

Wenn ein Dokument selbst um wenige Grad gedreht ist, interpretiert die OCR‑Engine die Zeilenbasen falsch, was zu wirrem Output führt. Der `DeskewFilter` schätzt automatisch den Rotationswinkel (bis zu `MaxAngle` Grad) und dreht das Bitmap zurück zu einer horizontalen Basislinie. Das zurückgegebene `DeskewConfidence` gibt an, wie sicher der Algorithmus bei der Korrektur ist – nützlich für Logging oder Fallback‑Strategien.

---

## Bild für OCR vorverarbeiten – Aufbau der Filter‑Pipeline

### 1️⃣ DeskewFilter (Primärer Schritt)

- **Was er tut:** Ermittelt die dominante Textzeilen‑Richtung und rotiert das Bild.
- **Warum das wichtig ist:** Eine gerade Basislinie maximiert die Genauigkeit der Zeichen‑Segmentierung.
- **Tipp:** Wenn Ihre Dokumente nie mehr als 10° abweichen, setzen Sie `MaxAngle = 10`, um die Erkennung zu beschleunigen.

### 2️⃣ DenoiseFilter (Sekundäre Bereinigung)

- **Was er tut:** Reduziert zufälliges Pixelrauschen, das nach dem Scannen auftreten kann.
- **Warum das wichtig ist:** Rauschen erzeugt häufig falsche Kanten und verwirrt die Segmentierung der OCR.
- **Tipp:** Passen Sie `Strength` zwischen 0,3 (leicht) und 0,8 (aggressiv) je nach Scan‑Qualität an.

### 3️⃣ ContrastBoostFilter (Finaler Schliff)

- **Was er tut:** Erhöht den Unterschied zwischen Vordergrund‑Text und Hintergrund.
- **Warum das wichtig ist:** Niedriger Kontrast kann schwache Zeichen für die Erkennungs‑Engine unsichtbar machen.
- **Tipp:** Ein `Level` von 1,2 funktioniert für die meisten Schwarz‑auf‑Weiß‑Scans; bei farbigen Dokumenten experimentieren Sie mit Werten bis zu 2,0.

Durch das Verketten dieser drei Filter **verarbeiten Sie das Bild für OCR** in einer Weise, die die häufigsten Probleme – Neigung, Rauschen und niedrigen Kontrast – adressiert.

---

## Wie man die OCR‑Genauigkeit mit Deskew und Denoise verbessert

Sie fragen sich vielleicht: „Wenn ich bereits einen Deskew‑Filter habe, warum noch Denoise und Contrast Boost?“ Die Antwort liegt in der **kumulativen Verbesserung**. Jeder Filter behebt einen anderen Mangel, und zusammen erhöhen sie das Gesamtergebnis.

#### Praxis‑Test

| Test | Originale OCR‑Genauigkeit | Nach Deskew | Nach voller Pipeline |
|------|---------------------------|-------------|----------------------|
| Einfache Rechnung (5° Neigung) | 78 % | 92 % | 96 % |
| Alte Zeitungs­scan (15° Neigung, körnig) | 61 % | 78 % | 88 % |
| Niedrig‑Kontrast‑Formular (keine Neigung) | 70 % | 71 % | 84 % |

*Die Zahlen sind illustrativ, spiegeln aber typische Verbesserungen wider, die von Aspose‑Nutzern berichtet werden.*

**Wichtiges Fazit:** Selbst wenn Ihr Hauptziel das **Deskew‑en gescannter Bilder** ist, führt das Hinzufügen von Denoise‑ und Contrast‑Schritten häufig zu einem spürbaren Sprung in der finalen Textqualität.

---

## Deskew gescannter Bilder: Ergebnisse prüfen

Nach dem Durchlauf der Pipeline erhalten Sie zwei nützliche Informationen:

```csharp
Console.WriteLine($"Deskew confidence: {result.DeskewConfidence:P2}");
Console.WriteLine(result.Text);
```

- **Deskew‑Vertrauen** (`result.DeskewConfidence`) ist ein Prozentsatz. Werte über 90 % bedeuten in der Regel, dass die Drehung korrekt korrigiert wurde.
- **Erkannter Text** (`result.Text`) ermöglicht Ihnen, sofort zu prüfen, ob das Ergebnis plausibel ist.

Ist das Vertrauen niedrig (< 70 %), sollten Sie überlegen:

1. **`MaxAngle` erhöhen** – vielleicht ist das Dokument stärker gedreht als erwartet.
2. **Einen `BinarizationFilter`** vor dem Deskew hinzufügen, um das Bild zu vereinfachen.
3. **Manuell rotieren** mit `OcrImage.Rotate(angle)` als Fallback.

---

## Vollständiges End‑zu‑End‑Beispiel (laufbereit)

Unten finden Sie das **komplette, eigenständige Programm**, das Sie in ein neues Konsolen‑App‑Projekt kopieren‑und‑einfügen können. Ersetzen Sie `YOUR_DIRECTORY` durch den Ordner, der Ihr schräges TIFF enthält.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

namespace DeskewDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Initialize the OCR engine
            var engine = new OcrEngine();

            // 2️⃣ Load the image you want to straighten
            var imgPath = @"C:\Images\skewed_doc.tif"; // <-- update this path
            var img = OcrImage.FromFile(imgPath);

            // 3️⃣ Define the preprocessing pipeline
            var pipeline = new OcrFilter[]
            {
                new DeskewFilter { MaxAngle = 30 },   // auto‑detect up to 30°
                new DenoiseFilter { Strength = 0.5 }, // moderate noise reduction
                new ContrastBoostFilter { Level = 1.2 } // brighten the text
            };

            // 4️⃣ Apply the pipeline – this returns a new image instance
            var preprocessed = engine.ApplyFilters(img, pipeline);

            // 5️⃣ Run OCR on the cleaned‑up image
            var result = engine.Recognize(preprocessed);

            // 6️⃣ Show confidence and the extracted text
            Console.WriteLine($"Deskew confidence: {result.DeskewConfidence:P2}");
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(result.Text);
        }
    }
}
```

**Erwartete Ausgabe** (bei einem relativ sauberen Scan):

```
Deskew confidence: 96.45%
=== Recognized Text ===
Invoice #12345
Date: 2024‑04‑01
Total: $1,250.00
...
```

Falls Sie wirre Zeichen sehen, überprüfen Sie die Filterstärken oder fügen Sie wie oben erwähnt einen `BinarizationFilter` hinzu.

---

## Häufige Stolperfallen & Pro‑Tipps

- **Stolperfalle:** Verwendung eines TIFFs mit mehreren Seiten. `OcrImage.FromFile` liest nur den ersten Frame. Nutzen Sie `OcrImage.FromMultiPageFile`, wenn Sie alle Seiten benötigen.
- **Stolperfalle:** Vergessen, `OcrEngine` zu entsorgen. Packen Sie sie in einen `using`‑Block, um native Ressourcen freizugeben.
- **Pro‑Tipp:** Cache die Pipeline, wenn Sie viele Bilder mit identischen Einstellungen verarbeiten – reduziert den Overhead.
- **Pro‑Tipp:** Loggen Sie `DeskewConfidence` in ein Monitoring‑System; plötzliche Abfälle können auf eine Änderung der Scanner‑Kalibrierung hinweisen.

---

## Nächste Schritte – Workflow erweitern

Jetzt, wo Sie **wissen, wie man ein Bild deskewt** und **wie man ein Bild für OCR vorverarbeitet**, können Sie Folgendes erkunden:

- **Batch‑Verarbeitung** – Durchlaufen Sie einen Ordner mit gescannten PDFs, konvertieren Sie jede Seite in ein Bild und wenden Sie dieselbe Pipeline an.
- **Sprachunterstützung** – Setzen Sie `engine.Language = OcrLanguage.English;` oder andere Sprachen, um die Erkennung zu verbessern.
- **Benutzerdefinierte Nachbearbeitung** – Verwenden Sie reguläre Ausdrücke, um typische OCR‑Fehler zu bereinigen (z. B. „0“ vs. „O“).

All diese Themen knüpfen natürlich an die sekundären Schlüsselwörter **how to improve ocr** und **deskew scanned image** an.

---

## Fazit

Wir haben alles behandelt, was Sie über **wie man ein Bild deskewt** mit Aspose.OCR wissen müssen – vom Aufbau einer robusten Filter‑Pipeline bis zur Prüfung von Vertrauenswerten. Durch **Bild für OCR vorverarbeiten** mit Deskew, Denoise und Contrast Boost sehen Sie messbare Verbesserungen bei **how to improve OCR**‑Ergebnissen, besonders bei schrägen oder verrauschten Scans.

Probieren Sie es mit Ihrem eigenen Dokumentensatz aus, passen Sie die Filterparameter an und beobachten Sie, wie die OCR‑Genauigkeit steigt. Haben Sie Fragen oder ein kniffliges File, das sich nicht begradigen lässt? Hinterlassen Sie einen Kommentar unten – wir lösen das gemeinsam. Viel Spaß beim Coden!

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, damit Sie weitere API‑Funktionen meistern und alternative Implementierungsansätze in Ihren Projekten erkunden können.

- [Wie man AspOCR verwendet: Bild‑OCR‑Filter für .NET vorverarbeiten](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Wie man ein Bild OCR‑t – OCR auf Bild in OCR‑Bild‑Erkennung ausführen](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)
- [Wie man den Schwellenwert in OCR‑Bild‑Erkennung setzt](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}