---
category: general
date: 2026-03-18
description: Wie man ein Bild begradigt und Rauschen in gescannten Dateien reduziert.
  Lernen Sie, ein Bild aus einer Datei zu laden, Text aus TIFF zu extrahieren und
  Text aus einem Bild mit Aspose OCR zu erkennen.
draft: false
keywords:
- how to deskew image
- how to reduce noise
- recognize text from image
- load image from file
- extract text from tiff
language: de
og_description: Wie man ein Bild schnell mit Aspose OCR begradigt. Dieser Leitfaden
  zeigt, wie man Rauschen reduziert, ein Bild aus einer Datei lädt und Text aus einer
  TIFF-Datei in C# extrahiert.
og_title: Wie man ein Bild entzerrt – Vollständiges C# OCR‑Tutorial
tags:
- OCR
- C#
- Image Processing
title: Wie man Bilder entneigt und Scans bereinigt – Vollständiger C#‑Leitfaden
url: /de/net/skew-angle-calculation/how-to-deskew-image-and-clean-up-scans-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Bild entzerren – Vollständiges C# OCR‑Tutorial

Haben Sie sich schon einmal gefragt, **wie man ein Bild entzerrt**, das aussieht, als wäre es von einem wackeligen Scanner aufgenommen worden? Sie sind nicht allein. Die meisten Entwickler stoßen auf dieses Problem, wenn das Quell‑TIFF leicht schief ist und die OCR‑Ergebnisse ein Chaos ergeben. Die gute Nachricht? Mit ein paar Zeilen C# können Sie das Bild begradigen, den körnigen Hintergrund entfernen und sauberen, durchsuchbaren Text direkt aus der Datei extrahieren.

In diesem Leitfaden gehen wir Schritt für Schritt durch **wie man Rauschen reduziert**, **wie man ein Bild aus einer Datei lädt** und schließlich **wie man Text aus einem Bild erkennt** mit Aspose OCR. Am Ende können Sie **Text aus TIFF**‑Dokumenten extrahieren, ohne ins Schwitzen zu geraten.

> **Pro‑Tipp:** Wenn Sie Aspose OCR bereits in anderen Projekten einsetzen, können Sie diese Filter ohne zusätzliche Lizenzprobleme einbinden.

---

## Was Sie benötigen

- .NET 6 oder höher (der Code funktioniert auch unter .NET Core)  
- Aspose.OCR NuGet‑Paket (`Install-Package Aspose.OCR`)  
- Ein gescanntes TIFF, das leicht gedreht oder verrauscht ist (wir verwenden `skewed_scanned_doc.tif` als Beispiel)  
- Ein Text‑Editor oder eine IDE (Visual Studio, VS Code, Rider – wählen Sie Ihr Lieblingswerkzeug)

Weitere Bibliotheken sind nicht nötig; die Filter, die wir verwenden, sind in Aspose OCR integriert.

---

## Schritt 1 – OCR‑Engine erstellen (Wie man ein Bild entzerrt)

Der erste Schritt besteht darin, eine `OcrEngine` zu initialisieren. Denken Sie daran als das Gehirn, das später die Zeichen für Sie liest.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Filters;

class PreprocessDemo
{
    static void Main()
    {
        // Initialize the OCR engine – this object holds all settings
        var ocrEngine = new OcrEngine();
```

Warum die Engine im Voraus erstellen? Sie bietet einen zentralen Ort, um Vorverarbeitungsfilter, Sprachpakete und Ausgabeeinstellungen anzuhängen. Wenn Sie diesen Schritt überspringen und `OcrEngine.Recognize` direkt aufrufen, verlieren Sie die Möglichkeit, das Bild vorher zu bereinigen – genau das ist der Grund, warum wir das Entzerren benötigen.

---

## Schritt 2 – Deskew‑ und Rauschunterdrückungs‑Filter hinzufügen (Wie man Rauschen reduziert)

Jetzt fügen wir zwei Filter hinzu:

| Filter | Was er tut | Warum das wichtig ist |
|--------|------------|-----------------------|
| `AutoDeskewFilter` | Erkennt und korrigiert Drehungen | Richten Sie Textzeilen aus, damit die OCR‑Engine sie korrekt lesen kann |
| `NoiseReductionFilterV2` | Entfernt Sprenkel und Hintergrundrauschen | Sauberere Pixel bedeuten weniger Fehlinterpretationen |

```csharp
        // Add filters to improve OCR accuracy
        ocrEngine.Settings.Filters.Add(new AutoDeskewFilter());          // corrects rotation
        ocrEngine.Settings.Filters.Add(new NoiseReductionFilterV2());   // reduces background noise
```

Sie könnten `NoiseReductionFilterV2` durch die ältere Version ersetzen, aber der v2‑Algorithmus funktioniert mit modernen Scannern besser. Wenn Ihr Dokument bereits völlig flach ist, lässt der Deskew‑Filter das Bild unverändert durch – kein Schaden entsteht.

---

## Schritt 3 – Bild aus Datei laden (Bild aus Datei laden)

Aspose stellt einen praktischen Helfer `ImageStream.FromFile` bereit, der eine Vielzahl von Formaten liest, darunter TIFF, JPEG, PNG und BMP. So laden wir die Datei in den Speicher:

```csharp
        // Load the scanned image you want to preprocess
        var image = ImageStream.FromFile(@"YOUR_DIRECTORY/skewed_scanned_doc.tif");
```

Ersetzen Sie `YOUR_DIRECTORY` durch den tatsächlichen Pfad auf Ihrem Rechner. Arbeiten Sie mit einem relativen Pfad, stellen Sie sicher, dass die Datei neben Ihrer ausführbaren Datei liegt oder setzen Sie das Arbeitsverzeichnis entsprechend.

---

## Schritt 4 – OCR auf dem vorverarbeiteten Bild ausführen (Text aus Bild erkennen)

Mit den Filtern im Einsatz und dem Bild geladen, lassen wir Aspose schließlich die Zeichen lesen:

```csharp
        // Perform OCR – the engine will automatically apply the filters first
        var ocrResult = ocrEngine.Recognize(image);
```

Im Hintergrund führt die Engine den Deskew‑Algorithmus aus, glättet das Rauschen und nutzt anschließend einen neuronalen‑Netz‑basierten Erkenner. Das Ergebnis wird in einem `OcrResult`‑Objekt verpackt, das Ihnen den Rohtext, Vertrauenswerte und sogar Begrenzungsrahmen liefert, falls Sie diese später benötigen.

---

## Schritt 5 – Extrahierten Text anzeigen oder speichern (Text aus TIFF extrahieren)

Für eine schnelle Demo geben wir den Text einfach in die Konsole aus, Sie könnten ihn aber auch in eine Datei, eine Datenbank schreiben oder in einen nachgelagerten Workflow einspeisen.

```csharp
        // Show the recognized text in the console
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Erwartete Ausgabe** (Beispiel, variiert je nach Dokument):

```
Invoice #12345
Date: 2023‑04‑01
Total: $1,250.00
Thank you for your business!
```

Wenn die Ausgabe noch verzerrte Zeichen enthält, prüfen Sie, ob das ursprüngliche TIFF nicht zu niedrig aufgelöst ist (mindestens 300 dpi empfohlen) und ob die Sprache korrekt in `ocrEngine.Settings.Language` eingestellt ist.

---

## Vollständiges Beispiel (Alle Schritte an einem Ort)

Unten finden Sie das komplette Programm, das Sie in ein neues Konsolenprojekt kopieren und sofort ausführen können.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Filters;

class PreprocessDemo
{
    static void Main()
    {
        // 1️⃣ Create OCR engine
        var ocrEngine = new OcrEngine();

        // 2️⃣ Add preprocessing filters
        ocrEngine.Settings.Filters.Add(new AutoDeskewFilter());          // deskew image
        ocrEngine.Settings.Filters.Add(new NoiseReductionFilterV2());   // reduce noise

        // 3️⃣ Load the image file (TIFF, JPEG, etc.)
        var image = ImageStream.FromFile(@"YOUR_DIRECTORY/skewed_scanned_doc.tif");

        // 4️⃣ Recognize text – filters run automatically
        var ocrResult = ocrEngine.Recognize(image);

        // 5️⃣ Output the extracted text
        Console.WriteLine(ocrResult.Text);
    }
}
```

Speichern Sie die Datei als `Program.cs`, führen Sie `dotnet run` aus, und Sie sollten den bereinigten Text in Ihrem Terminal sehen.

---

## Häufige Fragen & Sonderfälle

### Was, wenn mein TIFF mehrere Seiten hat?
Aspose OCR kann mehrseitige Bilder verarbeiten, indem Sie über `image.GetPages()` (oder `image.Pages`) iterieren. Jede Seite liefert ihr eigenes `OcrResult`. Kombinieren Sie sie mit `StringBuilder`, wenn Sie einen einzigen String benötigen.

### Funktioniert der Deskew‑Filter bei stark gedrehten Bildern?
Er verarbeitet Drehungen bis etwa ±15°. Darüber hinaus müssen Sie das Bild möglicherweise manuell mit einer Grafikbibliothek (z. B. `System.Drawing` oder `SkiaSharp`) vorrotieren, bevor Sie es an Aspose übergeben.

### Wie kann ich die Genauigkeit für nicht‑englischen Text verbessern?
Setzen Sie die Sprache explizit:

```csharp
ocrEngine.Settings.Language = Language.English; // or Language.French, etc.
```

Sie können auch benutzerdefinierte Sprachpakete laden, falls die integrierten nicht Ihr Alphabet abdecken.

### Kann ich das unter Linux ausführen?
Absolut. Aspose OCR ist plattformübergreifend; stellen Sie nur sicher, dass die nativen Abhängigkeiten vorhanden sind (bei der reinen .NET‑Version normalerweise keine). Verwenden Sie `dotnet publish -r linux-x64` für ein eigenständiges Binary.

---

## Bonus: Visualisierung des entzerrten Bildes

Wenn Sie das korrigierte Bild vor der OCR sehen möchten, können Sie es wieder auf die Festplatte speichern:

```csharp
// After OCR, the filtered image is stored in ocrEngine.Settings.FiltersResult
var corrected = ocrEngine.Settings.FiltersResult;
corrected.Save(@"output/deskewed_cleaned.tif");
```

![Beispiel für Bildentzerrung](https://example.com/deskew-demo.png "Beispiel für Bildentzerrung")

*Image alt text:* **Beispiel für Bildentzerrung** – zeigt ein Vorher/Nachher eines gedrehten TIFFs, das von AutoDeskewFilter korrigiert wurde.

---

## Fazit

Wir haben behandelt, **wie man ein Bild entzerrt**, **wie man Rauschen reduziert** und die gesamte Pipeline, um **Text aus einem Bild zu erkennen**, **ein Bild aus einer Datei zu laden** und **Text aus TIFF** mit Aspose OCR in C# zu extrahieren. Die zentrale Erkenntnis? Durch das Hinzufügen von nur zwei Vorverarbeitungsfiltern lässt sich ein wackeliges, körniges Scan‑Dokument in ein klares, durchsuchbares Dokument verwandeln – ganz ohne externe Werkzeuge.

Bereit für den nächsten Schritt? Versuchen Sie, `AutoDeskewFilter` durch `AutoRotateFilter` zu ersetzen, wenn Ihre Dokumente verkehrt herum sind, oder experimentieren Sie mit `ContrastEnhancementFilter` für verblasste Drucke. Das gleiche Muster – Engine → Filter → Laden → Erkennen – gilt für alle Aspose OCR‑Szenarien, sodass Sie dieses Gerüst für PDFs, PNGs oder sogar Kamerafotos wiederverwenden können.

Viel Spaß beim Coden und möge Ihre OCR stets präzise sein!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}