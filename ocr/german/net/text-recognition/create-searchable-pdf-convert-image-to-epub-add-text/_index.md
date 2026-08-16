---
category: general
date: 2026-03-13
description: Erstellen Sie ein durchsuchbares PDF aus jedem Bild mit Aspose OCR. Erfahren
  Sie, wie Sie ein Bild in EPUB konvertieren, durchsuchbaren Text hinzufügen und ein
  durchsuchbares PDF in C# erzeugen.
draft: false
keywords:
- create searchable pdf
- convert image to epub
- ocr image to pdf
- add searchable text
- generate searchable pdf
language: de
og_description: Erstellen Sie ein durchsuchbares PDF aus jedem Bild mit Aspose OCR.
  Dieser Leitfaden zeigt, wie man ein Bild in EPUB konvertiert, durchsuchbaren Text
  hinzufügt und ein durchsuchbares PDF in C# erzeugt.
og_title: Durchsuchbare PDF erstellen – Bild in EPUB konvertieren & Text hinzufügen
tags:
- Aspose OCR
- C#
- PDF
- EPUB
title: Durchsuchbare PDF erstellen – Bild in EPUB konvertieren & Text hinzufügen
url: /de/net/text-recognition/create-searchable-pdf-convert-image-to-epub-add-text/
---

.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Erstelle durchsuchbare PDF – Bild in EPUB konvertieren & Text hinzufügen

Möchten Sie **durchsuchbare PDF** aus einem gescannten Beleg oder einem beliebigen Bild erstellen? In diesem Tutorial zeigen wir Ihnen, wie Sie mit Aspose OCR durchsuchbare PDF erstellen, gleichzeitig **Bild in EPUB konvertieren** und **durchsuchbare Text**‑Ebenen hinzufügen – alles in einem einzigen C#‑Projekt.  

Wenn Sie jemals PDFs hatten, die gut aussehen, aber nicht durchsucht werden können, sind Sie nicht allein. Die gute Nachricht ist, dass eine versteckte Textebene ein flaches Bild in ein vollständig durchsuchbares Dokument verwandeln kann, und Aspose macht das fast schmerzfrei.

## Was Sie lernen werden

* Wie man die Aspose OCR‑Engine initialisiert und die Sprache festlegt.  
* Die genauen Schritte, um **Bild in EPUB** für die E‑Book‑Verteilung zu **konvertieren**.  
* Wie man den PDF‑Writer konfiguriert, sodass die Ausgabe eine versteckte, durchsuchbare Textebene enthält.  
* Tipps zum Umgang mit Sonderfällen wie mehrseitigen Belegen oder nicht‑englischen Sprachen.  

Alles, was Sie vorher benötigen, ist eine .NET‑Entwicklungsumgebung (Visual Studio 2022 oder neuer) und ein Aspose OCR‑NuGet‑Paket. Keine externen Dienste, keine obskuren Konfigurationsdateien – nur reines C#, das Sie kopieren‑einfügen und ausführen können.

## Voraussetzungen

| Requirement | Why it matters |
|-------------|----------------|
| .NET 6.0+   | Aspose OCR zielt auf .NET Standard 2.0+ ab, daher liefert .NET 6 die neuesten Laufzeitverbesserungen. |
| Aspose.OCR NuGet package | Stellt die Klassen `OcrEngine`, `EpubWriter` und `PdfWriter` bereit, die im Code verwendet werden. |
| An image file (e.g., `receipt.jpg`) | Die Quelle, auf die Sie OCR anwenden. Jede Rastergrafik (PNG, JPEG, BMP) funktioniert. |
| Basic C# knowledge | Sie werden Code‑Snippets lesen und anpassen, nicht die Sprache von Grund auf lernen. |

Sie können das Paket mit folgendem Befehl installieren:

```bash
dotnet add package Aspose.OCR
```

> **Pro Tipp:** Wenn Sie Visual Studio verwenden, erledigt die NuGet Package Manager‑UI dieselbe Aufgabe – suchen Sie einfach nach „Aspose.OCR“.

## Schritt 1 – Durchsuchbare PDF mit Aspose OCR erstellen

Das Erste, was wir benötigen, ist eine `OcrEngine`‑Instanz, die weiß, welche Sprache erkannt werden soll. Englisch ist die Vorgabe, aber Sie können sie durch Französisch, Deutsch usw. ersetzen, indem Sie `ocrEngine.Language` setzen.

```csharp
using Aspose.OCR;
using Aspose.OCR.Output;

// Initialise the OCR engine and set the language
OcrEngine ocrEngine = new OcrEngine
{
    Language = Language.English          // Change this if your document isn’t English
};
```

Warum die Engine zuerst initialisieren? Die Engine hält das Erkennungsmodell im Speicher, sodass das einmalige Erstellen und Wiederverwenden über mehrere Bilder hinweg sowohl CPU als auch RAM spart. Bei größeren Batch‑Jobs würden Sie dieselbe Instanz für den gesamten Durchlauf am Leben erhalten.

## Schritt 2 – Bild laden und OCR ausführen

Als Nächstes zeigen wir der Engine die Datei, die wir verarbeiten wollen. `ImageStream.FromFile` liest das Bild in ein Format ein, das die OCR‑Engine versteht.

```csharp
// Load the image you want to process
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/receipt.jpg");

// Run the recognition engine – this populates the internal text buffer
ocrEngine.Recognize();
```

> **Was, wenn das Bild mehrseitig ist?**  
> Aspose OCR kann mehrseitige TIFFs sofort verarbeiten. Übergeben Sie einfach den Pfad zur TIFF‑Datei; die Engine iteriert automatisch über jede Seite.

## Schritt 3 – Bild in EPUB konvertieren

Falls Sie zusätzlich eine E‑Book‑Version des gescannten Dokuments benötigen, macht Aspose das mit einer einzigen Zeile möglich. Der `EpubWriter` nutzt dieselbe `OcrEngine`‑Instanz, sodass die OCR‑Ergebnisse ohne zusätzliche Verarbeitung wiederverwendet werden.

```csharp
// Export the recognised content to an ePub file
EpubWriter epubWriter = new EpubWriter();
epubWriter.Save(ocrEngine, "YOUR_DIRECTORY/receipt.epub");
```

Warum nach EPUB exportieren? EPUB ist ein fließendes Format – perfekt für mobile Leser. Der OCR‑Text wird auswählbar, und das Originalbild bleibt als Hintergrund erhalten, wodurch das Aussehen des Originalscans bewahrt wird.

## Schritt 4 – Durchsuchbare Textebene zum PDF hinzufügen

Jetzt kommt der Teil, der tatsächlich **durchsuchbare PDF** **erstellt**. Durch Aktivieren von `AddSearchableTextLayer` bettet der PDF‑Writer eine unsichtbare Textebene ein, die die OCR‑Ausgabe spiegelt. Benutzer können suchen, kopieren oder Text hervorheben, genau wie bei einem nativen PDF.

```csharp
// Configure PDF writer to include a hidden searchable text layer
PdfWriter pdfWriter = new PdfWriter
{
    AddSearchableTextLayer = true   // Enables the hidden text layer for searchability
};

// Save the OCR result as a searchable PDF
pdfWriter.Save(ocrEngine, "YOUR_DIRECTORY/receipt_searchable.pdf");
```

> **Häufiger Stolperstein:** Wenn `AddSearchableTextLayer` nicht gesetzt wird, entsteht ein PDF, das identisch aussieht, aber keinen durchsuchbaren Text enthält. Überprüfen Sie dieses Flag immer, wenn Sie ein durchsuchbares Dokument benötigen.

## Schritt 5 – Vollständiges funktionierendes Beispiel

Wenn wir alles zusammenfügen, erhalten Sie eine eigenständige Konsolen‑App, die Sie in ein neues .NET‑Projekt einfügen und sofort ausführen können.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace OcrToPdfAndEpub
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialise OCR engine
            OcrEngine ocrEngine = new OcrEngine
            {
                Language = Language.English
            };

            // 2️⃣ Load the source image
            string imagePath = "YOUR_DIRECTORY/receipt.jpg";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // 3️⃣ Perform OCR
            ocrEngine.Recognize();

            // 4️⃣ Convert to EPUB (optional but handy)
            EpubWriter epubWriter = new EpubWriter();
            string epubPath = "YOUR_DIRECTORY/receipt.epub";
            epubWriter.Save(ocrEngine, epubPath);
            Console.WriteLine($"EPUB saved to {epubPath}");

            // 5️⃣ Create searchable PDF
            PdfWriter pdfWriter = new PdfWriter
            {
                AddSearchableTextLayer = true
            };
            string pdfPath = "YOUR_DIRECTORY/receipt_searchable.pdf";
            pdfWriter.Save(ocrEngine, pdfPath);
            Console.WriteLine($"Searchable PDF saved to {pdfPath}");
        }
    }
}
```

### Erwartete Ausgabe

* `receipt.epub` – eine EPUB‑Datei, die Sie in Calibre, Apple Books oder jedem anderen E‑Reader öffnen können.  
* `receipt_searchable.pdf` – ein PDF, bei dem Sie **Strg + F** drücken können, um jedes Wort zu finden, das im Originalbild vorkam.

Wenn Sie das PDF in Adobe Acrobat öffnen und **Datei → Eigenschaften → Beschreibung** ansehen, sehen Sie einen versteckten Text‑Stream unter dem Reiter **Schriften**, was bestätigt, dass die durchsuchbare Ebene vorhanden ist.

## Häufige Fragen & Randfälle

**F: Funktioniert das mit nicht‑englischen Sprachen?**

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}