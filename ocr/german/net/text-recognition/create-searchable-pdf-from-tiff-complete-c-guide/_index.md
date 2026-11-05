---
category: general
date: 2025-12-30
description: Erstelle ein durchsuchbares PDF aus einem Bild in C# – lerne, wie man
  TIFF in PDF konvertiert, Text aus dem Bild extrahiert und die PDF-Erstellung automatisiert.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- convert tiff to pdf
- extract text from image
- how to create pdf
language: de
og_description: Erstellen Sie ein durchsuchbares PDF aus einem Bild mit Aspose OCR
  in C#. Dieser Leitfaden zeigt, wie man TIFF in PDF konvertiert, Text extrahiert
  und die PDF/A‑1b‑Konformität sicherstellt.
og_title: Durchsuchbares PDF aus TIFF erstellen – Schritt‑für‑Schritt C#‑Tutorial
tags:
- Aspose OCR
- C#
- PDF generation
title: Durchsuchbare PDF aus TIFF erstellen – Vollständiger C#‑Leitfaden
url: /de/net/text-recognition/create-searchable-pdf-from-tiff-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Durchsuchbare PDF aus TIFF erstellen – Vollständiger C# Leitfaden

Haben Sie jemals **durchsuchbare PDFs** aus einem gescannten TIFF erstellen müssen, wussten aber nicht, wo Sie anfangen sollen? Sie sind nicht allein. Viele Entwickler stoßen auf dieses Problem, wenn sie durchsuchbare PDFs für Archivierung oder Compliance benötigen, und die gute Nachricht ist, dass die Lösung mit Aspose OCR überraschend einfach ist.

In diesem Tutorial führen wir Sie durch die Konvertierung eines Bildes zu PDF, das Extrahieren von Text aus dem Bild und das Verfeinern der Ausgabe, sodass sie den PDF/A‑1b‑Standards entspricht. Am Ende können Sie **tiff zu pdf konvertieren**, **Text aus Bild extrahieren** und wissen genau **wie man pdf** erstellt, die sowohl durchsuchbar als auch archivierungsbereit sind.

## Was Sie benötigen

- .NET 6 (oder eine aktuelle .NET‑Version) – der Code funktioniert sowohl auf .NET Core als auch auf .NET Framework.  
- Aspose.OCR NuGet‑Paket – installieren Sie es mit `dotnet add package Aspose.OCR`.  
- Eine Beispiel‑TIFF‑Datei (`input.tif`), die Sie in ein durchsuchbares PDF umwandeln möchten.  
- Eine Entwicklungsumgebung (Visual Studio, VS Code, Rider … jede ist geeignet).  

Das war's. Keine zusätzlichen SDKs, keine externen Dienste und keine versteckten Konfigurationsschritte.

![Beispiel für durchsuchbare PDF](image-placeholder.png "Vorschau der erstellten durchsuchbaren PDF")

## Schritt 1 – OCR‑Engine initialisieren und das englische Modell laden

Bevor wir ein Bild in durchsuchbaren Text umwandeln können, muss die OCR‑Engine wissen, welche Sprache sie erkennen soll. Aspose OCR liefert Sprachpakete, die Sie bei Bedarf laden können.

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;

// Initialize the OCR engine
var ocrEngine = new OcrEngine();

// Load the English language model (you can swap this for other languages)
ocrEngine.LoadLanguage(LanguageModel.English);
```

**Warum das wichtig ist:** Das Laden des richtigen Sprachmodells verbessert die Erkennungsgenauigkeit erheblich. Wenn Sie diesen Schritt überspringen, greift die Engine auf ein generisches Modell zurück, das oft verzerrten Text liefert – insbesondere bei TIFFs mit niedriger Auflösung.

## Schritt 2 – Text aus dem Quellbild erkennen (optional, aber praktisch)

Das Ausführen von OCR liefert ein `OcrResult`‑Objekt, das Sie inspizieren, protokollieren oder sogar als Klartext speichern können. Dieser Schritt ist optional, wenn Sie nur am endgültigen PDF interessiert sind, ist aber hervorragend zum Debuggen.

```csharp
// Perform OCR on the input TIFF
var ocrResult = ocrEngine.Recognize("YOUR_DIRECTORY/input.tif");

// Dump the raw text to the console (useful for validation)
Console.WriteLine("Extracted text:");
Console.WriteLine(ocrResult.Text);
```

**Pro‑Tipp:** Wenn der extrahierte Text nicht korrekt aussieht, sollten Sie das Bild vor der Übergabe an die Engine vorverarbeiten (Entzerrung, Rauschentfernung). Aspose OCR bietet außerdem Bildverbesserungs‑Utilities, die Sie hier aneinanderreihen können.

## Schritt 3 – Suchbare PDF‑Exporter einrichten

Jetzt teilen wir Aspose mit, wie das endgültige PDF aussehen soll. Der `SearchablePdfExporter` ermöglicht es Ihnen, den Ausgabepfad, die PDF/A‑Konformität und einige weitere Optionen festzulegen.

```csharp
var pdfExporter = new SearchablePdfExporter
{
    // Where the searchable PDF will be saved
    OutputPath = "YOUR_DIRECTORY/output.pdf",

    // Enforce PDF/A‑1b compliance – ideal for long‑term archiving
    PdfACompliance = PdfACompliance.PdfA1b
};
```

**Warum PDF/A‑1b?** Viele Branchen (Recht, Medizin, Finanzen) verlangen PDFs, die den Archivierungsstandards entsprechen. Das Setzen von `PdfACompliance` stellt sicher, dass Schriften eingebettet, Farben geräteunabhängig sind und die Datei Validierungstools besteht.

## Schritt 4 – OCR‑Ergebnis direkt in ein durchsuchbares PDF exportieren

Mit der vorbereiteten Engine und dem Exporter ist die Hauptarbeit nur eine Zeile. Der Exporter erstellt intern eine PDF‑Seite, legt den erkannten Text als unsichtbare Ebene darüber und schreibt die Datei.

```csharp
// Export the OCR result to a searchable PDF
pdfExporter.Export(ocrEngine, "YOUR_DIRECTORY/input.tif");

// Confirmation message
Console.WriteLine("Searchable PDF created at YOUR_DIRECTORY/output.pdf");
```

**Was im Hintergrund passiert:**  
1. Das ursprüngliche TIFF wird als Rasterbild eingebettet.  
2. Der aus OCR stammende Text wird darüber gelegt, verborgen aber auswählbar.  
3. Metadaten (wie die Sprache) werden hinzugefügt, damit PDF‑Reader den Text indexieren können.

## Schritt 5 – Ausgabe überprüfen (manuelle Prüfung + programmgesteuerte Validierung)

Es ist stets gute Praxis, zu bestätigen, dass das PDF wirklich durchsuchbar ist.

```csharp
// Quick sanity check: open the PDF and try to extract its text
using var pdfReader = new Aspose.Pdf.Facades.PdfConverter();
pdfReader.BindPdf("YOUR_DIRECTORY/output.pdf");
var extracted = pdfReader.ExtractText();
Console.WriteLine("Text extracted from the PDF:");
Console.WriteLine(extracted);
```

Wenn Sie den Text aus dem PDF‑Betrachter kopieren‑und‑einfügen können oder ihn in der Konsolenausgabe oben sehen, haben Sie Erfolg.

## Randfälle & häufige Variationen

### Konvertierung anderer Bildformate

Der gleiche Code funktioniert für PNG, JPEG, BMP – ändern Sie einfach die Dateierweiterung in den Aufrufen von `Recognize` und `Export`. Keine zusätzliche Konfiguration erforderlich.

### Mehrseitige TIFF‑Dateien

Aspose OCR verarbeitet automatisch jede Seite einer mehrseitigen TIFF und der Exporter stapelt sie zu einem mehrseitigen PDF. Wenn Sie eine Seite überspringen müssen, filtern Sie `ocrResult.Pages` vor dem Export.

### Nicht‑englische Sprachen

Tauschen Sie `LanguageModel.English` gegen `LanguageModel.Spanish`, `LanguageModel.French` usw. aus oder laden Sie ein benutzerdefiniertes Sprachpaket. Denken Sie daran, die PDF‑Metadaten anzupassen, wenn Sie ein bestimmtes Gebietsschema anvisieren.

### PDF‑Größe reduzieren

Wenn die TIFFs hochauflösend sind, kann das resultierende PDF sehr groß werden. Sie können das Bild vor der OCR herunterskalieren:

```csharp
ocrEngine.ImageProcessingOptions = new ImageProcessingOptions
{
    Dpi = 150 // Lower DPI reduces size, but test for acceptable quality
};
```

### Umgang mit passwortgeschützten PDFs

Wenn Sie die Ausgabe schützen müssen, wickeln Sie den `SearchablePdfExporter` nach dem Export in die Verschlüsselungs‑API von Aspose.Pdf ein:

```csharp
var pdfDoc = new Aspose.Pdf.Document("YOUR_DIRECTORY/output.pdf");
pdfDoc.Encrypt("userPassword", "ownerPassword", 
    Aspose.Pdf.Permissions.All, Aspose.Pdf.EncryptionAlgorithms.AES256);
pdfDoc.Save("YOUR_DIRECTORY/output_protected.pdf");
```

## Vollständiges funktionierendes Beispiel

Unten finden Sie das vollständige, sofort kopier‑und‑einfüg‑bereite Programm, das alle oben besprochenen Schritte und optionalen Anpassungen enthält.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Export;
using Aspose.Pdf.Facades;

class Program
{
    static void Main()
    {
        // -----------------------------------------------------------------
        // 1️⃣ Initialize OCR engine and load language model
        // -----------------------------------------------------------------
        var ocrEngine = new OcrEngine();
        ocrEngine.LoadLanguage(LanguageModel.English);

        // Optional: lower DPI to shrink output size (adjust as needed)
        // ocrEngine.ImageProcessingOptions = new ImageProcessingOptions { Dpi = 150 };

        // -----------------------------------------------------------------
        // 2️⃣ Recognize text from the source TIFF
        // -----------------------------------------------------------------
        const string inputPath = @"YOUR_DIRECTORY/input.tif";
        var ocrResult = ocrEngine.Recognize(inputPath);
        Console.WriteLine("Extracted text from image:");
        Console.WriteLine(ocrResult.Text);

        // -----------------------------------------------------------------
        // 3️⃣ Configure the searchable PDF exporter
        // -----------------------------------------------------------------
        var pdfExporter = new SearchablePdfExporter
        {
            OutputPath = @"YOUR_DIRECTORY/output.pdf",
            PdfACompliance = PdfACompliance.PdfA1b // archival compliance
        };

        // -----------------------------------------------------------------
        // 4️⃣ Export OCR result to searchable PDF
        // -----------------------------------------------------------------
        pdfExporter.Export(ocrEngine, inputPath);
        Console.WriteLine("Searchable PDF created successfully.");

        // -----------------------------------------------------------------
        // 5️⃣ Verify by extracting text from the generated PDF
        // -----------------------------------------------------------------
        using var converter = new PdfConverter();
        converter.BindPdf(@"YOUR_DIRECTORY/output.pdf");
        var extractedFromPdf = converter.ExtractText();
        Console.WriteLine("Text extracted from the PDF:");
        Console.WriteLine(extractedFromPdf);
    }
}
```

**Erwartete Ausgabe:**  
- Die Konsole gibt den rohen OCR‑Text aus dem TIFF aus.  
- Eine Datei `output.pdf` erscheint in `YOUR_DIRECTORY`.  
- Beim Öffnen von `output.pdf` in Adobe Reader können Sie den Text auswählen und kopieren, was bestätigt, dass er durchsuchbar ist.

## Zusammenfassung

Wir haben alles behandelt, was Sie benötigen, um **durchsuchbare PDFs** aus TIFF‑Bildern mit Aspose OCR in C# zu **erstellen**. Von der Initialisierung der OCR‑Engine, dem Extrahieren von Text, der Konfiguration der PDF/A‑Konformität bis hin zur Überprüfung des Enddokuments wird jeder Schritt klar erklärt. Sie wissen jetzt auch, wie man **Bild zu PDF konvertiert**, **tiff zu pdf konvertiert**, **Text aus Bild extrahiert** und die übergeordnete Frage, **wie man PDFs** mit durchsuchbaren Ebenen **erstellt**.

## Was Sie als Nächstes erkunden können

- **Stapelverarbeitung:** Packen Sie die Logik in eine Schleife, um Dutzende von Bildern automatisch zu verarbeiten.  
- **Benutzerdefinierte Schriften:** Betten Sie Unternehmensschriften für konsistente Markenauftritte ein.  
- **Cloud‑Integration:** Speichern Sie die PDFs nach der Erstellung direkt in Azure Blob Storage oder AWS S3.  
- **UI‑Frontend:** Erstellen Sie eine einfache WinForms/WPF‑App, die Benutzern das Drag‑and‑Drop von Bildern für eine sofortige Konvertierung ermöglicht.  

Fühlen Sie sich frei, mit verschiedenen Sprachmodellen, DPI‑Einstellungen und PDF/A‑Stufen zu experimentieren. Die API ist flexibel genug, um sich an fast jeden erdenklichen Workflow anzupassen.

*Viel Spaß beim Programmieren und möge Ihre PDFs immer durchsuchbar sein!*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}