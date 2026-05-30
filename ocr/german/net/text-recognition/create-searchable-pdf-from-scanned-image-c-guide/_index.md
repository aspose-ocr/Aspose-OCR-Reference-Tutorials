---
category: general
date: 2026-04-26
description: Erstellen Sie ein durchsuchbares PDF aus einem gescannten Bild mit Aspose
  OCR in C#. Erfahren Sie, wie Sie ein gescanntes Bild konvertieren, Text extrahieren
  und schnell ein durchsuchbares PDF erzeugen.
draft: false
keywords:
- create searchable pdf
- convert scanned image
- extract text from image
- how to ocr document
- convert tiff to pdf
language: de
og_description: Erstellen Sie ein durchsuchbares PDF aus einem gescannten Bild mit
  Aspose OCR. Schritt‑für‑Schritt C#‑Code zum Konvertieren, Extrahieren von Text und
  Generieren eines durchsuchbaren PDFs.
og_title: Erstelle durchsuchbare PDF aus gescanntem Bild – C#‑Leitfaden
tags:
- Aspose OCR
- C#
- PDF
- OCR
title: Durchsuchbares PDF aus gescanntem Bild erstellen – C#‑Leitfaden
url: /de/net/text-recognition/create-searchable-pdf-from-scanned-image-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Durchsuchbares PDF aus gescanntem Bild erstellen – C#‑Leitfaden

Haben Sie jemals **durchsuchbare PDFs** aus Papierverträgen, Quittungen oder alten Archiven erstellen müssen? Sie sind nicht allein – die meisten Entwickler stoßen auf dieses Problem, wenn ein Kunde einen Stapel TIFF‑Scans übergibt und ein durchsuchbares PDF als Endprodukt erwartet.  

In diesem Tutorial zeigen wir Ihnen genau **wie man ein Dokument OCR‑t** und ein gescanntes Bild mit Aspose OCR für .NET in ein **durchsuchbares PDF** verwandelt. Am Ende können Sie **gescannte Bild**‑Dateien **konvertieren**, **Text aus Bild**‑Daten **extrahieren** und sogar mehrseitige TIFFs ohne Aufwand verarbeiten.

## Was Sie benötigen

Bevor wir loslegen, stellen Sie sicher, dass Sie Folgendes haben:

* .NET 6.0 oder höher (die API funktioniert mit .NET Core, .NET Framework und .NET 5+).  
* Eine gültige Aspose OCR‑Lizenz oder Sie sind mit dem Evaluations‑Wasserzeichen einverstanden.  
* Das NuGet‑Paket `Aspose.OCR` installiert (`dotnet add package Aspose.OCR`).  
* Eine Beispiel‑TIFF‑Datei (z. B. `contract_scan.tif`), die Sie in ein durchsuchbares PDF umwandeln möchten.

Das war’s – keine zusätzlichen Bibliotheken, keine verrückte Konfiguration. Bereit? Los geht’s.

![Durchsuchbares PDF Beispiel](create-searchable-pdf.png "Durchsuchbares PDF Beispiel")

## Schritt 1 – OCR‑Engine initialisieren (Durchsuchbares PDF erstellen)

Zuerst benötigen Sie eine Instanz von `OcrEngine`. Dieses Objekt ist das Arbeitspferd, das das Bitmap liest, Zeichen erkennt und Ihnen den Text zurückgibt.  

```csharp
using Aspose.OCR;
using Aspose.OCR.Output;

// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Tell the engine which language to look for – Latin works for most English documents
ocrEngine.Language = Language.Latin;
```

**Warum die Sprache festlegen?**  
Wenn Sie die Standardeinstellung beibehalten, versucht Aspose jedes Sprachpaket, was die Verarbeitung verlangsamt. Durch Angabe von `Language.Latin` wird die Engine auf das lateinische Alphabet fokussiert, was Ihnen einen Geschwindigkeitsvorteil und genauere Ergebnisse für englischsprachige Verträge liefert.

## Schritt 2 – Gescanntes Bild laden (Gescanntes Bild konvertieren)

Jetzt übergeben wir der Engine das Bild, das wir verarbeiten wollen. Aspose kann einen Dateipfad, einen Stream oder sogar ein `byte[]` lesen. Der Einfachheit halber verwenden wir `ImageStream.FromFile`.  

```csharp
// Load the TIFF (or any supported image format)
ocrEngine.Image = ImageStream.FromFile(@"C:\Docs\contract_scan.tif");
```

Falls Sie später **TIFF in PDF konvertieren** müssen, beachten Sie, dass mehrseitige TIFFs automatisch verarbeitet werden – jeder Frame wird zu einer eigenen PDF‑Seite.

## Schritt 3 – OCR ausführen und Text extrahieren (Text aus Bild extrahieren)

OCR auszuführen ist so einfach wie das Aufrufen von `Recognize`. Die Engine gibt ein `RecognitionResult` zurück, das den Klartext, Vertrauenswerte und Layout‑Informationen enthält.  

```csharp
// Perform the OCR operation
RecognitionResult result = ocrEngine.Recognize();

// The raw text is available via the Text property
string extractedText = result.Text;

// Quick sanity check – print the first 200 characters
Console.WriteLine(extractedText.Substring(0, Math.Min(200, extractedText.Length)));
```

**Pro‑Tipp:** Wenn Sie nur den Text benötigen (kein PDF), können Sie hier stoppen und `extractedText` in eine `.txt`‑Datei schreiben. In den meisten Fällen ist unser Ziel jedoch ein durchsuchbares PDF, also fahren wir fort.

## Schritt 4 – Als durchsuchbares PDF speichern (Durchsuchbares PDF erstellen)

Aspose macht den letzten Schritt trivial: Rufen Sie einfach `Save` mit `SaveFormat.PdfSearchable` auf. Im Hintergrund bettet die Bibliothek den extrahierten Text als unsichtbare Ebene ein, während das ursprüngliche Bild unverändert bleibt.  

```csharp
// Save the result as a searchable PDF
ocrEngine.Save(@"C:\Docs\contract_searchable.pdf", SaveFormat.PdfSearchable);
```

Wenn Sie `contract_searchable.pdf` in einem beliebigen PDF‑Betrachter öffnen, können Sie den Text auswählen, kopieren und durchsuchen – genau das, was ein Kunde von einem „durchsuchbaren PDF“ erwartet.

## Umgang mit mehrseitigen TIFFs (TIFF in PDF konvertieren)

Enthält Ihre Quelldatei mehrere Seiten, behandelt Aspose jeden Frame automatisch als separate Seite. Keine zusätzlichen Schleifen nötig. Sie können jedoch DPI oder Bildqualität für jede Seite steuern:  

```csharp
// Optional: tweak image processing settings before OCR
ocrEngine.ImageProcessingOptions.Dpi = 300; // higher DPI improves accuracy
ocrEngine.ImageProcessingOptions.Compression = ImageCompression.Jpeg;
```

Nachdem Sie diese Optionen gesetzt haben, wiederholen Sie **Schritt 2** für jeden Frame oder verweisen Sie einfach `ImageStream.FromFile` auf das mehrseitige TIFF und lassen Aspose die Arbeit erledigen.

## Häufige Stolperfallen und wie man sie behebt

| Symptom | Wahrscheinliche Ursache | Lösung |
|---------|--------------------------|--------|
| Text ist verzerrt oder fehlt | Falsche Sprache eingestellt | Setzen Sie `ocrEngine.Language` auf das korrekte Sprachpaket (z. B. `Language.German`). |
| PDF ist riesig (10 MB für einen einseitigen Scan) | Standard‑Bildkompression ist niedrig | Passen Sie `ocrEngine.ImageProcessingOptions.Compression` auf `Jpeg` an und setzen Sie einen angemessenen `Quality`‑Wert (0‑100). |
| OCR läuft sehr langsam | Verwendung der Standard‑`Auto`‑Spracherkennung | Legen Sie die erwartete Sprache explizit fest. |
| Keine durchsuchbare Ebene sichtbar | Gespeichert mit `SaveFormat.Pdf` anstatt `PdfSearchable` | Verwenden Sie `PdfSearchable`. |

## Vollständiges End‑zu‑Ende‑Beispiel

Alles zusammengefügt, hier ist eine sofort ausführbare Konsolen‑App, die Sie in Visual Studio kopieren und einfügen können:

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace SearchablePdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize OCR engine
            OcrEngine ocrEngine = new OcrEngine
            {
                Language = Language.Latin,
                // Optional: improve accuracy for low‑resolution scans
                ImageProcessingOptions = { Dpi = 300, Compression = ImageCompression.Jpeg }
            };

            // 2️⃣ Load the scanned image (convert scanned image)
            string inputPath = @"C:\Docs\contract_scan.tif";
            ocrEngine.Image = ImageStream.FromFile(inputPath);

            // 3️⃣ Run OCR and extract text (extract text from image)
            RecognitionResult result = ocrEngine.Recognize();
            Console.WriteLine("First 200 characters of extracted text:");
            Console.WriteLine(result.Text.Substring(0, Math.Min(200, result.Text.Length)));

            // 4️⃣ Save as searchable PDF (create searchable pdf)
            string outputPath = @"C:\Docs\contract_searchable.pdf";
            ocrEngine.Save(outputPath, SaveFormat.PdfSearchable);
            Console.WriteLine($"Searchable PDF created at: {outputPath}");
        }
    }
}
```

**Was Sie sehen werden:**  
* Ein Konsolenfenster, das einen Ausschnitt des OCR‑Textes ausgibt.  
* Eine `contract_searchable.pdf`‑Datei, die neben Ihrem ursprünglichen TIFF liegt. Öffnen Sie sie, drücken Sie **Strg + F** und suchen Sie nach einem Wort, das im Original‑Scan vorkam – voilà, es funktioniert.

## Nächste Schritte & verwandte Themen

* **Wie man Dokumente stapelweise OCR‑t** – wickeln Sie den obigen Code in eine `foreach`‑Schleife und verarbeiten Sie einen gesamten Ordner.  
* **Gescannte Bild‑Formate außer TIFF konvertieren** (PNG, JPEG) – dieselbe API funktioniert; ändern Sie einfach die Dateierweiterung.  
* **Text aus Bild extrahieren** für weitere Analysen – geben Sie `result.Text` in eine Natural‑Language‑Processing‑Pipeline ein.  
* **PDF‑Größe optimieren** – untersuchen Sie `PdfSaveOptions`, um Bilder weiter zu komprimieren oder Schriftarten nur bei Bedarf einzubetten.  

Experimentieren Sie mit diesen Ideen, und Sie werden schnell zur Ansprechperson für jede Anfrage „Scans in durchsuchbare PDFs umwandeln“.

---

### TL;DR

Sie wissen jetzt, wie man mit Aspose OCR in C# **durchsuchbare PDFs** aus gescannten Bildern erstellt. Der Prozess lautet: Engine initialisieren, Bild laden, OCR ausführen und mit `PdfSearchable` speichern. Passen Sie Spracheinstellungen, DPI und Kompression an, um Sonderfälle zu bewältigen, und Sie sind bereit, **gescannte Bilder zu konvertieren**, **Text aus Bildern zu extrahieren** und sogar **TIFF in PDF** in großem Umfang zu **konvertieren**. Viel Spaß beim Coden!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}