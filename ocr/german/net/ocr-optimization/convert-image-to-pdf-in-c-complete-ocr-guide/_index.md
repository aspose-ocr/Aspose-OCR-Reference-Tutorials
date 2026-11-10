---
category: general
date: 2026-09-13
description: Erfahren Sie, wie Sie eine gescannte Seite in PDF mit C# und Aspose OCR
  umwandeln. Dieser Leitfaden zeigt die Vorverarbeitung, die Erkennung koreanischen
  Textes und das Erstellen eines durchsuchbaren PDFs.
keywords:
- scanned page to pdf
- preprocess image for OCR
- generate pdf with text
- convert image to searchable pdf
- gpu accelerated OCR
- recognize Korean text image
lastmod: 2026-09-13
og_description: Erfahren Sie, wie Sie eine gescannte Seite in PDF mit C# und Aspose
  OCR umwandeln. Das Tutorial behandelt die Bildvorverarbeitung, GPU‑beschleunigtes
  OCR für koreanischen Text und das Erzeugen eines durchsuchbaren PDFs in wenigen
  Minuten.
og_image_alt: Screenshot of C# console app converting a scanned Korean page to searchable
  PDF using Aspose OCR
og_title: Wie man eine gescannte Seite in PDF mit C# und OCR umwandelt
schemas:
- author: Aspose
  dateModified: '2026-09-13'
  description: Learn how to turn a scanned page to PDF in C# using Aspose OCR. This
    guide shows preprocessing, Korean text recognition, and creating a searchable
    PDF.
  headline: How to turn a scanned page to PDF in C# with OCR
  type: TechArticle
- description: Learn how to turn a scanned page to PDF in C# using Aspose OCR. This
    guide shows preprocessing, Korean text recognition, and creating a searchable
    PDF.
  name: How to turn a scanned page to PDF in C# with OCR
  steps:
  - name: Initialise the OCR engine with GPU support.
    text: Initialise the OCR engine with GPU support.
  - name: Add **preprocess image for OCR** filters such as deskew and denoise.
    text: Add **preprocess image for OCR** filters such as deskew and denoise.
  - name: Download and load the Korean language model (handled automatically).
    text: Download and load the Korean language model (handled automatically).
  - name: Run the OCR on the image.
    text: Run the OCR on the image.
  - name: Export the result with **SearchablePdfExporter** to **create searchable
      PDF image**.
    text: Export the result with **SearchablePdfExporter** to **create searchable
      PDF image**.
  - name: (Optional) Serialize the OCR output to JSON for downstream pipelines.
    text: (Optional) Serialize the OCR output to JSON for downstream pipelines.
  - name: '**Ensure the language model is fully downloaded** – check the console for
      a message like “Downloading Korean model…”.'
    text: '**Ensure the language model is fully downloaded** – check the console for
      a message like “Downloading Korean model…”.'
  - name: '**Increase the `MaxAngle`** in `DeskewFilter` if your scans are rotated
      beyond 12°.'
    text: '**Increase the `MaxAngle`** in `DeskewFilter` if your scans are rotated
      beyond 12°.'
  - name: '**Boost GPU memory** by setting `ocrEngine.GpuMemoryLimit = 2048;` (value
      in MB).'
    text: '**Boost GPU memory** by setting `ocrEngine.GpuMemoryLimit = 2048;` (value
      in MB).'
  type: HowTo
- questions:
  - answer: 'The exporter embeds the original bitmap at its native resolution. If
      size is a concern, downscale the image *before* recognition:'
    question: My PDF is huge compared to the original image.
  - answer: Verify that the image path is correct and that the file is not corrupted.
      Also, make sure the GPU driver is up‑to‑date; older drivers can cause silent
      failures.
    question: The OCR returns empty strings.
  - answer: Absolutely. Wrap steps 4‑6 in a `foreach (var file in Directory.GetFiles("Resources",
      "*.jpg"))` loop and change the output PDF path accordingly.
    question: Can I process multiple pages in a loop?
  type: FAQPage
tags:
- scanned page to pdf
- OCR
- Aspose
- C#
title: Wie man eine gescannte Seite in PDF mit C# und OCR umwandelt
url: /de/net/ocr-optimization/convert-image-to-pdf-in-c-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man eine gescannte Seite in PDF in C# mit OCR umwandelt

Wenn Sie **eine gescannte Seite in PDF konvertieren** möchten, während der Text durchsuchbar bleibt, sind Sie hier genau richtig. Dieses Tutorial führt Sie durch die Verwendung von Aspose OCR zum **preprocess image for OCR**, **recognize Korean text image** und schließlich **create searchable PDF image** – alles aus einer einfachen C# Konsolenanwendung.

## Schnelle Antworten
- **Welche Bibliothek übernimmt OCR?** Aspose.OCR for .NET  
- **Kann ich die GPU nutzen?** Yes – enable GPU acceleration for up to 2× faster processing  
- **Benötige ich ein Koreanisch-Sprachpaket?** It downloads automatically on first use  
- **Wird die Ausgabe durchsuchbar sein?** The generated PDF contains an invisible text layer  
- **Welche .NET-Versionen werden unterstützt?** .NET 6.0 and later (including .NET Core and .NET Framework)

## Voraussetzungen

- **.NET 6.0 oder höher** – funktioniert auf .NET Core, .NET Framework und .NET 5/6+  
- **Aspose.OCR for .NET** NuGet‑Paket (`Aspose.OCR`) – Testschlüssel sind kostenlos auf der Aspose‑Website  
- Ein Beispielbild mit koreanischen Zeichen, z. B. `korean_book_page.jpg`  
- Ihre bevorzugte IDE (Visual Studio 2022, VS Code, Rider usw.)

> **Pro Tipp:** Bilder in einem `Resources/`‑Ordner speichern, damit Pfade auf verschiedenen Rechnern konsistent bleiben.

## Überblick über den Prozess

1. Initialisieren Sie die OCR‑Engine mit GPU‑Unterstützung.  
2. Fügen Sie **preprocess image for OCR**‑Filter wie Deskew und Denoise hinzu.  
3. Laden Sie das koreanische Sprachmodell herunter und laden es (automatisch).  
4. Führen Sie die OCR auf dem Bild aus.  
5. Exportieren Sie das Ergebnis mit **SearchablePdfExporter** zu **create searchable PDF image**.  
6. (Optional) Serialisieren Sie die OCR‑Ausgabe nach JSON für nachgelagerte Pipelines.

Im Folgenden erweitern wir jeden Schritt, erklären *warum* er wichtig ist und geben Ihnen den genauen Code, den Sie kopieren‑und‑einfügen können.

## Wie funktioniert die Umwandlung einer gescannten Seite in PDF?

`OcrEngine` ist die Hauptklasse in Aspose.OCR, die optische Zeichenerkennung auf Bildern durchführt.  
`SearchablePdfExporter` erstellt ein PDF, das das Originalbild und eine unsichtbare Textebene für die Suche enthält.  
`RecognitionResult` enthält den Text und die Vertrauenswerte, die von der OCR‑Engine zurückgegeben werden.

Laden Sie Ihr Bild mit `new OcrEngine()` und rufen Sie `engine.Recognize("korean_book_page.jpg")` auf, dann übergeben Sie das `RecognitionResult` an `SearchablePdfExporter.Export`. Dieser zweistufige Ablauf liest das Bitmap, extrahiert Unicode‑Text und bettet beides in ein einzelnes PDF ein, wobei die Textebene unsichtbar, aber durchsuchbar ist. GPU‑Beschleunigung verkürzt die Erkennungszeit etwa um die Hälfte, während Deskew‑ und Denoise‑Filter die Genauigkeit bei verrauschten Scans um bis zu 15 % erhöhen.

## Bild in PDF konvertieren – vollständiger Workflow

Der folgende Ausschnitt ist das *vollständige* Programm. Erstellen Sie ein neues Konsolenprojekt (`dotnet new console -n OcrPdfDemo`) und ersetzen Sie die automatisch erzeugte `Program.cs` durch den im Platzhalter gezeigten Code.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;
using Aspose.OCR.Export;
using Aspose.OCR.Result;   // for JsonResult

namespace OcrPdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // Step 1: Initialise the OCR engine (GPU enabled, offline mode off)
            // -----------------------------------------------------------------
            var ocrEngine = new OcrEngine
            {
                UseGpu = true,          // leverages your graphics card for faster inference
                OfflineMode = false    // allows on‑the‑fly language model download
            };

            // --------------------------------------------------------------
            // Step 2: Add preprocessing filters to improve accuracy
            // --------------------------------------------------------------
            // Deskew corrects slight rotations; MaxAngle = 12° is a safe default.
            ocrEngine.Filters.Add(new DeskewFilter { MaxAngle = 12 });

            // Denoise removes isolated speckles that often appear in scanned books.
            ocrEngine.Filters.Add(new DenoiseFilter());

            // --------------------------------------------------------------
            // Step 3: Load the Korean language model
            // --------------------------------------------------------------
            // Aspose will download the model the first time you run this on a new machine.
            ocrEngine.LoadLanguage(LanguageModel.Korean);

            // --------------------------------------------------------------
            // Step 4: Recognise text from the input image
            // --------------------------------------------------------------
            // Replace the path with your actual image location.
            string imagePath = "Resources/korean_book_page.jpg";
            var recognitionResult = ocrEngine.Recognize(imagePath);

            // --------------------------------------------------------------
            // Step 5: Export the recognised page as a searchable PDF
            // --------------------------------------------------------------
            string pdfPath = "Resources/korean_page.pdf";
            var exporter = new SearchablePdfExporter { OutputPath = pdfPath };
            exporter.Export(ocrEngine, imagePath);

            // --------------------------------------------------------------
            // Step 6: Obtain a structured JSON representation of the result
            // --------------------------------------------------------------
            string json = JsonResult.FromRecognitionResult(recognitionResult).ToString(true);
            Console.WriteLine("=== OCR JSON Result ===");
            Console.WriteLine(json);

            Console.WriteLine("\n✅ Conversion complete!");
            Console.WriteLine($"PDF saved to: {pdfPath}");
        }
    }
}
```

### Warum das funktioniert

- **GPU acceleration** verkürzt die Erkennungszeit etwa um die Hälfte im Vergleich zum reinen CPU‑Modus.  
- **Deskew** und **Denoise** sind klassische *preprocess image for OCR*‑Techniken; sie korrigieren häufige Scan‑Defekte, die sonst dazu führen, dass die Engine Zeichen übersieht.  
- **Language model loading** ist entscheidend für **recognize Korean text image** – ohne das koreanische Modell würde die Engine auf ein generisches lateinisches Alphabet zurückgreifen und Kauderwelsch erzeugen.  
- Der **SearchablePdfExporter** bündelt das Original‑Bitmap und ein unsichtbares Text‑Overlay und liefert Ihnen ein **create searchable pdf image**‑Ergebnis, das Sie in jedem PDF‑Betrachter indizieren können.

## Warum das funktioniert

- **GPU acceleration** verkürzt die Erkennungszeit etwa um die Hälfte im Vergleich zum reinen CPU‑Modus.  
- **Deskew** und **Denoise** sind klassische *preprocess image for OCR*‑Techniken; sie korrigieren häufige Scan‑Defekte, die sonst dazu führen, dass die Engine Zeichen übersieht.  
- **Language model loading** ist entscheidend für **recognize Korean text image** – ohne das koreanische Modell würde die Engine auf ein generisches lateinisches Alphabet zurückgreifen und Kauderwelsch erzeugen.  
- Der **SearchablePdfExporter** bündelt das Original‑Bitmap und ein unsichtbares Text‑Overlay und liefert Ihnen ein **create searchable pdf image**‑Ergebnis, das Sie in jedem PDF‑Betrachter indizieren können.

## Bild für OCR vorverarbeiten – Tipps & Tricks

`DeskewFilter` korrigiert die Rotation gescannter Seiten.  
`ContrastFilter` passt den Bildkontrast an, um die OCR‑Genauigkeit zu verbessern.  
`BinarizationFilter` wandelt das Bild basierend auf einem Schwellenwert in Schwarz‑Weiß um und reduziert Hintergrundrauschen.  
`OrientationFilter` erkennt und korrigiert gemischte Hoch‑/Querformat‑Seiten.

| Problem | Zusätzlicher Filter | Wie hinzufügen |
|-------|-------------------|------------|
| Geringer Kontrast | `ContrastFilter { Level = 30 }` | `ocrEngine.Filters.Add(new ContrastFilter { Level = 30 });` |
| Starkes Hintergrundrauschen | `BinarizationFilter { Threshold = 128 }` | `ocrEngine.Filters.Add(new BinarizationFilter { Threshold = 128 });` |
| Gemischte Ausrichtung (Hochformat & Querformat) | `OrientationFilter()` | `ocrEngine.Filters.Add(new OrientationFilter());` |

> **Hinweis:** Das Hinzufügen zu vieler Filter kann die Verarbeitung verlangsamen. Testen Sie jede Änderung an einer einzelnen Seite, bevor Sie skalieren.

## Koreanischen Text aus Bild erkennen – häufige Stolperfallen

Koreanische Schriften enthalten Hangul‑Silben, die visuell dicht sind. Wenn Sie fehlerhafte Ausgaben bemerken:

1. **Stellen Sie sicher, dass das Sprachmodell vollständig heruntergeladen ist** – prüfen Sie die Konsole auf eine Meldung wie „Downloading Korean model…“.  
2. **Erhöhen Sie `MaxAngle`** im `DeskewFilter`, wenn Ihre Scans um mehr als 12° gedreht sind.  
3. **Erhöhen Sie den GPU‑Speicher**, indem Sie `ocrEngine.GpuMemoryLimit = 2048;` setzen (Wert in MB).

`LanguageModel.Korean` lädt die koreanischen Sprachdaten für die OCR und ermöglicht eine genaue Hangul‑Erkennung.  

Diese Anpassungen beeinflussen direkt den Erfolg von **recognize Korean text image**.

## Durchsuchbares PDF‑Bild erstellen – Ergebnis überprüfen

Nach Abschluss des Programms öffnen Sie `korean_page.pdf` in einem beliebigen PDF‑Reader (Adobe Acrobat Reader, Foxit, sogar Chrome). Sie sollten in der Lage sein:

- **Text auswählen** mit der Maus, als wäre es ein natives PDF.  
- **Suchen** nach koreanischen Wörtern über das integrierte Suchfeld.  

Wenn die Textebene leer erscheint, prüfen Sie erneut, ob die `Export`‑Methode den korrekten Bildpfad erhalten hat und ob das OCR‑Ergebnis ein nicht leeres `RecognitionResult.Text` enthält.

## Vollständige JSON‑Ausgabe – was zu erwarten ist

Die Konsole gibt eine schön formatierte JSON‑Payload aus. Ein gekürztes Beispiel sieht so aus:

```json
{
  "Text": "첫 번째 페이지의 내용...",
  "Blocks": [
    {
      "Text": "첫 번째 페이지의 내용...",
      "BoundingBox": { "X": 12, "Y": 34, "Width": 560, "Height": 780 },
      "Confidence": 0.98
    }
  ],
  "Language": "Korean",
  "ProcessingTimeMs": 842
}
```

## Fehlersuche & FAQ

**Q: Mein PDF ist im Vergleich zum Originalbild riesig.**  
A: Der Exporter bettet das Original‑Bitmap in seiner nativen Auflösung ein. Wenn die Größe ein Problem darstellt, skalieren Sie das Bild *vor* der Erkennung herunter:

```csharp
ocrEngine.Filters.Add(new ResizeFilter { MaxWidth = 1240, MaxHeight = 1754 });
```

**Q: Die OCR gibt leere Zeichenketten zurück.**  
A: Überprüfen Sie, ob der Bildpfad korrekt ist und die Datei nicht beschädigt ist. Stellen Sie außerdem sicher, dass der GPU‑Treiber aktuell ist; ältere Treiber können stille Fehler verursachen.

**Q: Kann ich mehrere Seiten in einer Schleife verarbeiten?**  
A: Absolut. Packen Sie die Schritte 4‑6 in eine `foreach (var file in Directory.GetFiles("Resources", "*.jpg"))`‑Schleife und passen Sie den Ausgabepfad des PDFs entsprechend an.

## Fazit

Wir haben gerade **image to PDF** **konvertiert**, während wir durchsuchbaren Text beibehalten, dank Aspose OCRs leistungsstarker Pipeline. Durch **preprocess image for OCR** steigern Sie die Genauigkeit; durch **recognize Korean text image** können Sie komplexe Schriften verarbeiten; und durch **create searchable pdf image** erhalten Sie ein portables, indexierbares Dokument.

Holen Sie sich den Code, richten Sie ihn auf Ihre eigenen Scans aus und experimentieren Sie mit zusätzlichen Filtern oder Sprachmodellen. Das gleiche Muster funktioniert für Chinesisch, Japanisch oder jede latinbasierte Sprache – ersetzen Sie einfach `LanguageModel.Korean` durch das passende Enum.

Haben Sie weitere Fragen? Hinterlassen Sie einen Kommentar, und viel Spaß beim Coden!

---

**Letzte Aktualisierung:** 2026-09-13  
**Getestet mit:** Aspose.OCR 24.11 for .NET  
**Autor:** Aspose

## Verwandte Tutorials

- [Erstelle durchsuchbares PDF aus gescannten Dateien mit Aspose OCR](/ocr/net/ocr-optimization/create-searchable-pdf-from-scanned-files-using-aspose-ocr/)
- [OCR-Vorverarbeitungspipeline – Wie man Text aus Bild erkennt](/ocr/net/ocr-optimization/ocr-preprocessing-pipeline-how-to-recognize-text-from-image/)
- [Text aus Bild mit Aspose OCR erkennen – vollständiger C‑Leitfaden](/ocr/net/ocr-configuration/recognize-text-from-image-with-aspose-ocr-complete-c-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}