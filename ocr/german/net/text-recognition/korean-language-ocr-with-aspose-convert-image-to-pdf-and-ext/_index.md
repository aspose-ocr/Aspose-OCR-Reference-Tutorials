---
category: general
date: 2026-05-28
description: Koreanisch-OCR‑Tutorial mit Aspose in C#. Erfahren Sie, wie Sie ein Bild
  aus einem Stream laden, Klartext extrahieren, das Bild in PDF konvertieren und ein
  durchsuchbares PDF exportieren.
draft: false
keywords:
- korean language ocr
- convert image to pdf
- load image from stream
- extract plain text
- export searchable pdf
language: de
og_description: Koreanische OCR in C# mit Aspose. Schritt‑für‑Schritt‑Anleitung zum
  Laden eines Bildes aus einem Stream, zum Extrahieren von Klartext, zum Konvertieren
  des Bildes in PDF und zum Exportieren eines durchsuchbaren PDFs.
og_title: Koreanisch OCR – Bild in PDF umwandeln & Text extrahieren (C#‑Leitfaden)
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: Korean Language OCR tutorial using Aspose in C#. Learn how to load
    image from stream, extract plain text, convert image to PDF and export searchable
    PDF.
  headline: 'Korean Language OCR with Aspose: Convert Image to PDF and Extract Text
    in C#'
  type: TechArticle
tags:
- Aspose OCR
- C#
- Image Processing
title: 'Koreanische Sprache OCR mit Aspose: Bild in PDF konvertieren und Text in C#
  extrahieren'
url: /de/net/text-recognition/korean-language-ocr-with-aspose-convert-image-to-pdf-and-ext/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Koreanische Sprach-OCR mit Aspose: Bild in PDF konvertieren und Text in C# extrahieren

Haben Sie sich jemals gefragt, wie man **Korean Language OCR** auf einem Bild ausführt, ohne etwas in die Cloud zu senden? Sie sind nicht der Einzige. Ob Sie Straßenschilder digitalisieren, Belege verarbeiten oder einen mehrsprachigen Suchindex erstellen, die lokale Erkennung koreanischer Zeichen kann Ihnen Zeit, Geld und Datenschutzprobleme ersparen.

In diesem Tutorial führen wir Sie durch ein vollständiges, ausführbares Beispiel, das zeigt, wie man **load image from stream**, **extract plain text**, **convert image to PDF** und schließlich **export searchable PDF** – alles mit Aspose.OCR und ein paar Zeilen C#. Keine externen Dienste, keine versteckte Magie – nur reiner .NET‑Code, den Sie in jede Konsolenanwendung einbinden können.

## Was Sie am Ende erhalten

- Ein funktionierendes Konsolenprogramm, das eine JPEG‑Datei über einen Dateistream liest.  
- Koreanischer Text, extrahiert als reine Unicode‑Zeichenketten.  
- Ein detaillierter JSON‑Bericht des OCR‑Durchlaufs für Debugging oder Analysen.  
- Ein durchsuchbares PDF, das Sie in jedem PDF‑Reader öffnen und die koreanischen Wörter tatsächlich auswählen können.  

**Voraussetzungen**  
- .NET 6.0 oder höher (der Code funktioniert auch mit .NET Framework 4.7+).  
- Aspose.OCR für .NET NuGet‑Paket installiert (`Install-Package Aspose.OCR`).  
- Ein Ordner, der `korean_sign.jpg` enthält, und ein beschreibbarer Ort für die Ausgabedateien.  

Wenn Sie diese Komponenten bereits haben, großartig – lassen Sie uns loslegen.

## Schritt 1: OCR‑Engine für Korean Language OCR initialisieren

Das Erste, was Sie benötigen, ist eine `OcrEngine`‑Instanz. Das Aktivieren der GPU (falls vorhanden) beschleunigt die Erkennung dramatisch, und das Deaktivieren des automatischen Ressourcen‑Downloads zwingt die Bibliothek, die von Ihnen bereitgestellten Offline‑Sprachpakete zu verwenden.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Enums;

// Create the OCR engine
var ocrEngine = new OcrEngine();

// Enable GPU acceleration – optional but fast
ocrEngine.Configuration.EnableGpu = true;

// We’ll supply the Korean language pack ourselves
ocrEngine.Configuration.AutomaticResourceDownload = false;
ocrEngine.Configuration.ResourcesFolder = @"YOUR_DIRECTORY/Resources";
```

> **Warum das wichtig ist:**  
> *GPU‑Beschleunigung* kann die Verarbeitungszeit von Sekunden auf Millisekunden für große Stapel reduzieren. Das Setzen von `AutomaticResourceDownload` auf `false` stellt sicher, dass das Demo offline funktioniert – eine entscheidende Anforderung für viele Unternehmensumgebungen.

## Schritt 2: Bild aus Stream laden

Das Lesen des Bildes über einen Stream bietet Ihnen Flexibilität: Sie können Dateien von der Festplatte, Netzwerkfreigaben oder sogar speicher‑gecachete Blobs abrufen. Hier öffnen wir eine lokale JPEG‑Datei, aber dasselbe Muster funktioniert für jeden `Stream`.

```csharp
using System.IO;

// Open the image file as a read‑only stream
using var imageStream = File.OpenRead(@"YOUR_DIRECTORY/korean_sign.jpg");

// Feed the stream to the OCR engine
ocrEngine.Image = ImageStream.FromStream(imageStream);
```

> **Pro‑Tipp:** Wenn Sie jemals Bilder verarbeiten müssen, die über eine Web‑API hochgeladen wurden, ersetzen Sie einfach `File.OpenRead` durch das eingehende `IFormFile.OpenReadStream()` – der Rest bleibt identisch.

## Schritt 3: Korean Language auswählen und Vorverarbeitungsfilter anwenden

Aspose.OCR unterstützt eine Handvoll von Vorverarbeitungsschritten, die das Bild vor der Erkennung bereinigen. Für koreanische Schilder reichen in der Regel Deskewing und Denoising aus.

```csharp
using Aspose.OCR.Enums;

// Tell the engine we’re dealing with Korean text
ocrEngine.Configuration.Language = Language.Korean;

// Apply deskew and denoise filters
ocrEngine.Configuration.PreprocessFilters = PreprocessFilter.Deskew |
                                            PreprocessFilter.Denoise;
```

> **Was im Hintergrund passiert:**  
> Der `Deskew`‑Filter richtet gedrehten Text aus, während `Denoise` Körnung entfernt, die den Zeichenklassifikator verwirren kann. Das Überspringen dieser Schritte führt häufig zu fehlerhaften Ausgaben, besonders bei Fotos mit niedriger Auflösung.

## Schritt 4: Klartext asynchron extrahieren

Jetzt kommt der entscheidende Moment – die Engine zu bitten, die Zeichen zu erkennen und uns eine saubere Zeichenkette zu liefern. Die Verwendung von `RecognizeAsync` hält die UI reaktionsfähig, wenn Sie dies in eine Desktop‑ oder Web‑App einbetten.

```csharp
// Run OCR and get the plain text result
string plainText = await ocrEngine.RecognizeAsync();
```

Wenn Sie das Programm ausführen, sollten Sie etwas Ähnliches sehen:

```
OCR complete. Extracted text:
서울시청
```

> **Warum async?**  
> OCR kann CPU‑intensiv sein. Asynchrone Ausführung verhindert, dass Ihr Thread blockiert, was besonders in ASP.NET Core nützlich ist, wo Thread‑Verhungern ein echtes Problem darstellt.

## Schritt 5: Detailliertes Erkennungsergebnis erhalten und als JSON speichern

Manchmal benötigen Sie mehr als nur die rohe Zeichenkette – vielleicht wollen Sie Konfidenzwerte, Begrenzungsrahmen oder die Original‑Bilddaten. Die Methode `RecognizeDetailed` gibt ein `RecognitionResult`‑Objekt zurück, das für spätere Analysen in JSON serialisiert werden kann.

```csharp
// Detailed result includes confidence, coordinates, etc.
RecognitionResult detailedResult = ocrEngine.RecognizeDetailed();

// Convert to nicely indented JSON
string jsonResult = detailedResult.ToJson(indent: true);

// Persist the JSON to disk
File.WriteAllText(@"YOUR_DIRECTORY/korean_ocr.json", jsonResult);
```

Das Öffnen von `korean_ocr.json` zeigt eine Struktur ähnlich wie:

```json
{
  "Pages": [
    {
      "Text": "서울시청",
      "Confidence": 0.98,
      "Words": [
        {
          "Text": "서울시청",
          "BoundingBox": [12,34,56,78],
          "Confidence": 0.98
        }
      ]
    }
  ]
}
```

> **Wann das zu verwenden ist:**  
> Wenn Sie einen Suchindex erstellen, ermöglichen Ihnen die Konfidenzwerte, minderwertige Ergebnisse zu filtern. Wenn Sie Text in einer UI hervorheben müssen, sind die Begrenzungsrahmen Ihre Karte.

## Schritt 6: Bild in PDF konvertieren und durchsuchbares PDF exportieren

Aspose macht den Sprung von Raster zu Vektor mühelos. Durch das Setzen von `OutputFormat` auf `SearchablePdf` bettet die Bibliothek das Originalbild ein und legt eine unsichtbare Textebene mit dem OCR‑Ergebnis darüber. Das resultierende PDF kann durchsucht, kopiert und indiziert werden wie jedes native PDF.

```csharp
using Aspose.OCR.Enums;

// Tell the engine to produce a searchable PDF
ocrEngine.Configuration.OutputFormat = OutputFormat.SearchablePdf;

// Save the PDF to the target folder
ocrEngine.Save(@"YOUR_DIRECTORY/korean_searchable.pdf");
```

Öffnen Sie `korean_searchable.pdf` in Adobe Reader oder einem beliebigen PDF‑Betrachter, drücken Sie **Strg+F**, geben Sie ein koreanisches Wort ein und sehen Sie, wie es zur genauen Stelle auf der Seite springt. Das ist die Kraft eines durchsuchbaren PDFs.

> **Zusätzlicher Tipp:** Wenn Sie nur ein visuelles PDF ohne die versteckte Textebene benötigen, setzen Sie `OutputFormat` stattdessen auf `Pdf`.

## Vollständiges funktionierendes Beispiel

Unten finden Sie das vollständige Programm – kopieren, einfügen, `YOUR_DIRECTORY` durch einen tatsächlichen Pfad ersetzen und **F5** drücken.

```csharp
using System;
using System.IO;
using System.Threading.Tasks;
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Enums;

class OcrDemo
{
    static async Task Main()
    {
        // Step 1: Create the OCR engine and enable GPU with offline resources
        var ocrEngine = new OcrEngine();
        ocrEngine.Configuration.EnableGpu = true;
        ocrEngine.Configuration.AutomaticResourceDownload = false;
        ocrEngine.Configuration.ResourcesFolder = @"YOUR_DIRECTORY/Resources";

        // Step 2: Select the language and apply preprocessing filters
        ocrEngine.Configuration.Language = Language.Korean;
        ocrEngine.Configuration.PreprocessFilters = PreprocessFilter.Deskew |
                                                    PreprocessFilter.Denoise;

        // Step 3: Load the image to be recognized from a file stream
        using var imageStream = File.OpenRead(@"YOUR_DIRECTORY/korean_sign.jpg");
        ocrEngine.Image = ImageStream.FromStream(imageStream);

        // Step 4: Run OCR asynchronously and obtain the plain text result
        string plainText = await ocrEngine.RecognizeAsync();

        // Step 5: Get a detailed recognition result, convert it to JSON, and save it
        RecognitionResult detailedResult = ocrEngine.RecognizeDetailed();
        string jsonResult = detailedResult.ToJson(indent: true);
        File.WriteAllText(@"YOUR_DIRECTORY/korean_ocr.json", jsonResult);

        // Step 6: Export the recognized page as a searchable PDF
        ocrEngine.Configuration.OutputFormat = OutputFormat.SearchablePdf;
        ocrEngine.Save(@"YOUR_DIRECTORY/korean_searchable.pdf");

        Console.WriteLine("OCR complete. Extracted text:");
        Console.WriteLine(plainText);
    }
}
```

### Erwartete Konsolenausgabe

```
OCR complete. Extracted text:
서울시청
```

Und Sie finden drei neue Dateien neben Ihrem Quellbild:

- `korean_ocr.json` – vollständige Erkennungsdaten.  
- `korean_searchable.pdf` – ein PDF, das Sie durchsuchen können.  
- (optional) beliebige Zwischennotizen, die Sie hinzufügen möchten.

## Häufige Fragen & Sonderfälle

**Was, wenn ich keine GPU habe?**  
Setzen Sie `EnableGpu = false`; das CPU‑Fallback ist für kleine Stapel völlig ausreichend.

**Kann ich mehrere Bilder in einem Durchlauf verarbeiten?**  
Absolut. Wickeln Sie die Kernlogik in eine `foreach (var file in Directory.GetFiles(...))`‑Schleife und weisen Sie `ocrEngine.Image` in jeder Iteration neu zu.

**Wie gehe ich mit anderen Sprachen zusammen mit Koreanisch um?**  
Aspose.OCR ermöglicht das Setzen von `Language = Language.AutoDetect` oder das Kombinieren von Sprachen mit dem bitweisen ODER‑Operator (z. B. `Language.Korean | Language.English`).

**Was, wenn die OCR‑Konfidenz niedrig ist?**  
Untersuchen Sie `detailedResult.Pages[0].Words` und filtern Sie Einträge mit `Confidence < 0.7` heraus. Sie können auch die Vorverarbeitungsfilter anpassen – versuchen Sie, `PreprocessFilter.ContrastEnhancement` hinzuzufügen.

## Fazit

Sie haben gerade gesehen, wie man **Korean Language OCR** von Anfang bis Ende durchführt, von **loading image from stream** über **extract plain text** bis hin zu **convert image to PDF** und schließlich **export searchable PDF**. Der Ansatz ist modular, sodass Sie die Bildquelle austauschen, das Ausgabeformat ändern oder das JSON in jede nachgelagerte Pipeline einbinden können.

Was kommt als Nächstes

## Verwandte Tutorials

- [Bildtext in C# mit Sprachauswahl mithilfe von Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Text in Bild mit Aspose OCR für mehrere Sprachen erkennen](/ocr/english/net/ocr-settings/working-with-different-languages/)
- [Text aus Bild extrahieren – OCR-Optimierung mit Aspose.OCR für .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}