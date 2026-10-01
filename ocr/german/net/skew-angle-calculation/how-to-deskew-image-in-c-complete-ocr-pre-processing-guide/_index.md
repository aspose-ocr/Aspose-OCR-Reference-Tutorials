---
category: general
date: 2026-01-10
description: Wie man ein Bild entneigt und OCR‑Ergebnisse mit Aspose.OCR verbessert.
  Lernen Sie, das Bild für OCR vorzubereiten, Rauschen aus dem Scan zu entfernen und
  Text aus dem Scan zu erkennen.
draft: false
keywords:
- how to deskew image
- preprocess image for ocr
- recognize text from scan
- how to use ocr
- remove noise from scan
language: de
og_description: Wie man ein Bild entsteilt und die OCR‑Genauigkeit verbessert. Dieser
  Leitfaden zeigt, wie man ein Bild für OCR vorverarbeitet, Rauschen aus dem Scan
  entfernt und Text aus dem Scan mit Aspose.OCR erkennt.
og_title: Wie man ein Bild in C# entzerrt – Vollständiger Leitfaden zur OCR‑Vorverarbeitung
tags:
- OCR
- C#
- Image Processing
title: Wie man ein Bild in C# entzerrt – Vollständiger Leitfaden zur OCR‑Vorverarbeitung
url: /de/net/skew-angle-calculation/how-to-deskew-image-in-c-complete-ocr-pre-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man Bilder in C# entneigt – Vollständiger OCR‑Vorverarbeitungs‑Leitfaden

Haben Sie sich jemals gefragt, **wie man Bilddateien entneigt**, bevor man sie an eine OCR‑Engine übergibt? Sie sind nicht der Einzige. Gescannte Dokumente sind oft schief, verrauscht oder haben geringen Kontrast, und das beeinträchtigt jede Texterkennungs‑Versuch.  

In diesem Tutorial führen wir ein vollständiges, ausführbares Beispiel durch, das **Bild für OCR vorverarbeitet**, Rauschen aus dem Scan entfernt und schließlich **Text aus dem Scan erkennt** mithilfe der Aspose.OCR‑Bibliothek. Am Ende haben Sie ein klares Bild davon, **wie man OCR** in C# verwendet, während der Code kurz und prägnant bleibt.

> **Profi‑Tipp:** Schon eine kleine Drehung (5‑10°) kann die OCR‑Genauigkeit um 30 % oder mehr reduzieren. Das Entneigen ist der erste Schritt, den Sie niemals überspringen sollten.

---

## Was Sie benötigen

- **.NET 6+** (der Code funktioniert auch unter .NET Framework, aber .NET 6 ist das aktuelle LTS)
- **Aspose.OCR für .NET** – Sie können es von NuGet holen (`Install-Package Aspose.OCR`)
- Eine Beispiel‑TIFF/PNG/JPEG, die gedreht oder verrauscht ist (wir verwenden `noisy_rotated.tif` im Beispiel)
- Beliebige IDE – Visual Studio, Rider oder VS Code reicht aus

Das war’s. Keine zusätzlichen Bibliotheken, keine externen Dienste.

---

## Schritt 1 – Quellbild laden (Warum das wichtig ist)

Bevor wir **Bild entneigen** können, müssen wir es in einen Aspose `ImageStream` einlesen. Dieses Objekt abstrahiert die Dateiein‑ und -ausgabe und stellt der OCR‑Engine eine konsistente Schnittstelle bereit.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

// Load the original scan – replace the path with your own file
var sourceImage = ImageStream.FromFile("YOUR_DIRECTORY/noisy_rotated.tif");

// Quick sanity check – make sure the image loaded
if (sourceImage == null)
{
    Console.WriteLine("Failed to load the image. Check the path and file permissions.");
    return;
}
```

*Warum zuerst laden?* Weil alle nachfolgenden Filter auf einem Bild im Speicher arbeiten. Wenn die Datei nicht gelesen werden kann, bricht die gesamte Pipeline zusammen.

---

## Schritt 2 – Vorverarbeitungspipeline erstellen (Entneigen + Rauschentfernung + Kontrast)

Ein robustes OCR‑Workflow verkettet normalerweise mehrere Filter. Hier **verarbeiten wir das Bild für OCR vor** und, noch wichtiger, **wie man Bild automatisch entneigt**.

```csharp
// Create a pipeline that will run three filters in order
var preprocessPipeline = new PreprocessPipeline()
{
    // 1️⃣ DeskewFilter – detects rotation up to 30° and corrects it
    new DeskewFilter { MaxAngle = 30 },

    // 2️⃣ DenoiseFilter – smooths out speckles while keeping edges
    new DenoiseFilter { Strength = 0.8 },

    // 3️⃣ ContrastBoostFilter – makes faint characters pop
    new ContrastBoostFilter { Level = 1.3 }
};
```

**Warum diese drei?**  
- **DeskewFilter** löst das Problem „wie man Bild entneigt“ automatisch; Sie müssen den Winkel nicht schätzen.  
- **DenoiseFilter** adressiert die Anforderung „Rauschen aus dem Scan entfernen“, das sonst Phantom‑Zeichen erzeugt.  
- **ContrastBoostFilter** hilft der OCR‑Engine, dunklen Text von einem hellen Hintergrund zu unterscheiden, ein klassisches Problem, wenn Sie *Bild für OCR vorverarbeiten*.

---

## Schritt 3 – Pipeline anwenden (Transformation sehen)

Jetzt führen wir die Filter tatsächlich aus. Das zurückgegebene `processedImage` ist das, was wir an die OCR‑Engine übergeben.

```csharp
// Apply all filters – the result is a cleaned‑up bitmap
var processedImage = preprocessPipeline.Apply(sourceImage);

// Optional: Save the cleaned image for visual verification
processedImage.Save("cleaned_output.tif");
Console.WriteLine("Image preprocessing complete – cleaned_output.tif saved.");
```

Wenn Sie `cleaned_output.tif` öffnen, sollten Sie feststellen, dass der Text gerade, weniger körnig und mit höherem Kontrast ist. Diese visuelle Kontrolle ist praktisch, wenn Sie *Rauschen aus dem Scan entfernen* und bestätigen möchten, dass das Entneigen funktioniert hat.

---

## Schritt 4 – OCR‑Engine erstellen und konfigurieren (Wie man OCR verwendet)

Mit einem bereinigten Bild in der Hand instanziieren wir `OcrEngine`. Dies ist das Kernstück von **wie man OCR** mit Aspose verwendet.

```csharp
// Initialize the OCR engine
var ocrEngine = new OcrEngine
{
    // Assign the pre‑processed image
    Image = processedImage,

    // Optional: Set language (English is default)
    // Language = Language.English,
    
    // Enable automatic page segmentation (helps with multi‑column scans)
    AutoPageSegmentation = true
};
```

*Warum `AutoPageSegmentation` setzen?* Weil viele Scans Tabellen oder mehrere Spalten enthalten. Das Einschalten lässt die Engine die Seite intelligent aufteilen, was das Endergebnis von **Text aus dem Scan erkennen** verbessert.

---

## Schritt 5 – Erkennungsprozess ausführen (Endlich Text erkennen)

Jetzt der entscheidende Moment: Wir lassen die Engine den Text lesen.

```csharp
// Kick off the OCR process
ocrEngine.Recognize();

// Retrieve the plain‑text result
string recognizedText = ocrEngine.Text;

// Show the output in the console
Console.WriteLine("=== Recognized Text ===");
Console.WriteLine(recognizedText);
```

Wenn alles reibungslos verlief, sehen Sie einen sauberen Textblock, der dem Originaldokument entspricht. Das ist die Belohnung für korrektes **Entneigen des Bildes**, **Entfernen von Rauschen** und **Vorverarbeiten des Bildes für OCR**.

---

## Schritt 6 – Vollständiges funktionierendes Beispiel (Kopier‑ und Einfüge‑bereit)

Unten finden Sie das komplette Programm, bereit zum Kompilieren. Ersetzen Sie einfach den Dateipfad und Sie können loslegen.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Load the source image
        // -------------------------------------------------
        var sourceImage = ImageStream.FromFile("YOUR_DIRECTORY/noisy_rotated.tif");
        if (sourceImage == null)
        {
            Console.WriteLine("Unable to load image. Check the path.");
            return;
        }

        // -------------------------------------------------
        // 2️⃣ Build the preprocessing pipeline
        // -------------------------------------------------
        var preprocessPipeline = new PreprocessPipeline()
        {
            new DeskewFilter { MaxAngle = 30 },          // how to deskew image
            new DenoiseFilter { Strength = 0.8 },       // remove noise from scan
            new ContrastBoostFilter { Level = 1.3 }      // improves OCR accuracy
        };

        // -------------------------------------------------
        // 3️⃣ Apply the pipeline
        // -------------------------------------------------
        var processedImage = preprocessPipeline.Apply(sourceImage);
        processedImage.Save("cleaned_output.tif");
        Console.WriteLine("Preprocessing finished – cleaned_output.tif saved.");

        // -------------------------------------------------
        // 4️⃣ Configure the OCR engine
        // -------------------------------------------------
        var ocrEngine = new OcrEngine
        {
            Image = processedImage,
            AutoPageSegmentation = true   // how to use OCR effectively
        };

        // -------------------------------------------------
        // 5️⃣ Recognize text from scan
        // -------------------------------------------------
        ocrEngine.Recognize();
        string result = ocrEngine.Text;

        Console.WriteLine("\n=== Recognized Text ===");
        Console.WriteLine(result);
    }
}
```

**Erwartete Ausgabe** (aus Gründen der Kürze gekürzt):

```
=== Recognized Text ===
This is a sample scanned document.
It contains several lines of text,
and the OCR engine has correctly read them.
```

Wenn die Ausgabe unleserlich aussieht, prüfen Sie, ob das Quellbild nicht um mehr als 30° gedreht ist, oder erhöhen Sie `DeskewFilter.MaxAngle`.

---

## Häufig gestellte Fragen (Randfälle & Variationen)

| Frage | Antwort |
|----------|--------|
| **Was, wenn mein Scan um 45° gedreht ist?** | `DeskewFilter` begrenzt sich auf `MaxAngle`. Erhöhen Sie ihn (z. B. `MaxAngle = 60`) oder drehen Sie das Bild vorab mit einer Grafikbibliothek, bevor Sie es in die Pipeline geben. |
| **Kann ich PDFs seitenweise verarbeiten?** | Ja. Konvertieren Sie jede PDF‑Seite in ein Bild (z. B. mit `Aspose.Pdf`) und führen Sie die gleiche Pipeline für jedes Bitmap aus. |
| **Mein Dokument ist auf Französisch – muss ich etwas ändern?** | Setzen Sie `ocrEngine.Language = Language.French;` oder laden Sie ein benutzerdefiniertes Sprachpaket. Der Rest der Pipeline bleibt unverändert. |
| **Gibt es eine Möglichkeit, die Originalauflösung beizubehalten?** | `PreprocessPipeline` arbeitet mit dem Original‑Bitmap und bewahrt die DPI. Vermeiden Sie einfach den Aufruf von `ImageStream.Resize`, es sei denn, Sie müssen aus Leistungsgründen verkleinern. |
| **Wie wirkt sich das Kontrast‑Boosting auf farbige Scans aus?** | `ContrastBoostFilter` arbeitet auf jedem Kanal; es ist sicher für Graustufen‑ oder Farbbilder, Sie können das Bild jedoch auch zuerst mit `new GrayscaleFilter()` in Graustufen konvertieren. |

---

## Bildbeispiel (Visuelle Hilfe)

![Beispiel zum Entneigen von Bildern](/images/deskew-example.png)

*Das Bild zeigt ein Vorher/Nachher einer um 12° gedrehten, verrauschten Aufnahme, die entneigt und bereinigt wurde.*

---

## Fazit

Wir haben **wie man Bild entneigt** mit Aspose.OCR behandelt, eine vollständige **Bild‑vorverarbeitung für OCR**‑Pipeline demonstriert, gezeigt, wie man **Rauschen aus dem Scan entfernt**, und schließlich **Text aus dem Scan erkennt** mit wenigen Zeilen C#. Durch die Verkettung von `DeskewFilter`, `DenoiseFilter` und `ContrastBoostFilter` erhalten Sie ein bereinigtes Bitmap, das der OCR‑Engine ermöglicht, ihre Arbeit zu erledigen, ohne an Artefakten zu ersticken.  

Nächste Schritte? Experimentieren Sie mit unterschiedlichen Filterstärken, fügen Sie einen `BinarizationFilter` für reine Schwarz‑Weiß‑Ausgabe hinzu oder geben Sie das bereinigte Bild an eine nachgelagerte NLP‑Pipeline weiter. Das gleiche Muster funktioniert ebenso für Quittungen, Reisepässe und historische Dokumente.  

Haben Sie weitere Fragen zu **wie man OCR verwendet** in anderen Sprachen oder Frameworks? Hinterlassen Sie einen Kommentar, und viel Spaß beim Coden!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}