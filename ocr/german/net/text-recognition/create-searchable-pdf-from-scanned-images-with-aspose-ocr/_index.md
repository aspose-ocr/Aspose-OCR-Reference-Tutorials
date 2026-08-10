---
category: general
date: 2026-02-27
description: Erstellen Sie in Sekunden ein durchsuchbares PDF aus einem gescannten
  PDF mit Aspose OCR. Erfahren Sie, wie Sie gescannte PDFs konvertieren, PDFs per
  OCR umwandeln und Text aus PDFs mühelos extrahieren.
draft: false
keywords:
- create searchable pdf
- convert scanned pdf
- ocr convert pdf
- extract text from pdf
- convert image pdf
language: de
og_description: Erstellen Sie sofort ein durchsuchbares PDF. Dieses Tutorial zeigt,
  wie man gescannte PDFs konvertiert, PDFs per OCR verarbeitet und Text aus PDFs mit
  Aspose OCR extrahiert.
og_title: Durchsuchbare PDF erstellen – Schnellstart-Anleitung für Aspose OCR
tags:
- Aspose OCR
- C#
- PDF processing
title: Durchsuchbares PDF aus gescannten Bildern mit Aspose OCR erstellen
url: /de/net/text-recognition/create-searchable-pdf-from-scanned-images-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Durchsuchbares PDF aus gescannten Bildern mit Aspose OCR erstellen

Haben Sie jemals versucht, ein **durchsuchbares PDF** aus einer rein papierbasierten Rechnung zu erstellen, wussten aber nicht, wo Sie anfangen sollen? Mit Aspose OCR können Sie **durchsuchbare PDFs** in nur wenigen Zeilen C# erstellen – ohne externe Dienste, ohne manuelles Kopieren‑Einfügen.  

In diesem Leitfaden führen wir Sie durch alles, was Sie benötigen, um **gescannte PDFs** in vollständig durchsuchbare PDFs zu **konvertieren**, erklären, warum jeder Schritt wichtig ist, und zeigen sogar, wie man **Text aus PDF extrahiert**, wenn Sie Rohzeichenketten statt einer PDF‑Ausgabe bevorzugen. Am Ende haben Sie ein wiederverwendbares Snippet, das das häufige „Nur‑Bild‑PDF“-Problem löst, sowie einige Tipps für Randfälle.

![Durchsuchbares PDF mit Aspose OCR erstellen](image-placeholder.png "Durchsuchbares PDF mit Aspose OCR erstellen")

## Was Sie benötigen

- .NET 6.0 oder höher (die API funktioniert auf .NET Core, .NET Framework und .NET 5+)
- Visual Studio 2022 (oder jeder andere Editor Ihrer Wahl)
- Ein Aspose OCR NuGet‑Paket (`Aspose.OCR`) – wir installieren es im ersten Schritt
- Eine gescannte PDF‑Datei (nur Bild), die Sie in ein **durchsuchbares PDF** umwandeln möchten

Das war’s – keine zusätzlichen OCR‑Engines, keine Lizenzprobleme für einen Testlauf.  

Jetzt legen wir los.

## Schritt 1: Installieren der Aspose OCR‑Bibliothek (und ein kurzer Hinweis)

Bevor irgendein Code ausgeführt wird, muss die Bibliothek referenziert werden. Öffnen Sie ein Terminal in Ihrem Projektordner und führen Sie aus:

```bash
dotnet add package Aspose.OCR
```

> **Profi‑Tipp:** Wenn Sie den Package Manager von Visual Studio verwenden, suchen Sie nach „Aspose.OCR“ und klicken Sie auf **Install**. Die kostenlose Testversion funktioniert für bis zu 20 Seiten, was ideal zum Testen ist.

Durch die Installation des Pakets erhalten Sie Zugriff auf `OcrEngine`, `OcrLanguage` und `OcrOutputFormat` – die drei Klassen, die wir zum **OCR‑Konvertieren von PDFs** verwenden werden.

## Schritt 2: Konfigurieren der OCR‑Engine (Durchsuchbares PDF erstellen – Kerneinstellungen)

Die Engine muss wissen, welche Sprache sie erkennen soll und welches Ausgabeformat Sie erwarten. In unserem Fall wollen wir ein englischsprachiges PDF, das durchsuchbar ist.

```csharp
using Aspose.OCR;
using System;

// Step 2: Set up the OCR engine
var ocrEngine = new OcrEngine
{
    // Choose the language of the source document
    Language = OcrLanguage.English,

    // Tell Aspose we want a searchable PDF as the result
    OutputFormat = OcrOutputFormat.SearchablePdf
};
```

Warum `Language` explizit setzen? Die OCR‑Genauigkeit sinkt dramatisch, wenn die Engine die Sprache rät, besonders bei Dokumenten mit Zahlen oder gemischten Schriften. Durch das Festlegen auf Englisch erhalten wir sauberere Textebenen, was wiederum den späteren Schritt **Text aus PDF extrahieren** verbessert.

## Schritt 3: Gescanntes PDF in ein durchsuchbares PDF konvertieren

Jetzt, wo die Engine bereit ist, geben Sie ihr die Quelldatei und den Zielort für das Ergebnis an. Dieser einzige Aufruf erledigt die schwere Arbeit: Er rastert jede Seite, führt OCR aus und schreibt ein neues PDF mit einer unsichtbaren Textebene.

```csharp
// Step 3: Perform the conversion
ocrEngine.RecognizePdf(
    @"C:\Docs\invoice_scanned.pdf",   // input – image‑only PDF
    @"C:\Docs\invoice_searchable.pdf" // output – searchable PDF
);
```

Wenn das Quell‑PDF mehrere Seiten enthält, verarbeitet Aspose OCR sie sequenziell und bewahrt das ursprüngliche Layout. Die Ausgabedatei kann in jedem PDF‑Betrachter geöffnet werden; Sie werden feststellen, dass Sie nun Wörter auswählen und suchen können, die vorher nur Bilder waren.

### Ergebnis überprüfen (Text aus PDF extrahieren)

Um absolut sicher zu sein, dass die Konvertierung erfolgreich war, möchten Sie möglicherweise den Text programmgesteuert extrahieren:

```csharp
using Aspose.Pdf;           // Add Aspose.PDF if you also need text extraction
using System.Text;

// Load the newly created searchable PDF
var doc = new Document(@"C:\Docs\invoice_searchable.pdf");
var sb = new StringBuilder();

foreach (Page page in doc.Pages)
{
    // Extract the hidden text layer
    sb.Append(page.Text);
}

Console.WriteLine("Extracted text:\n" + sb.ToString());
```

Dieses Snippet zeigt, wie Sie **Text aus PDF extrahieren** können, nachdem der OCR‑Schritt abgeschlossen ist – praktisch für die Indexierung oder das Einspeisen des Inhalts in eine Suchmaschine. Beachten Sie, dass Sie dafür das separate `Aspose.PDF`‑Paket benötigen; es ist ein leichtgewichtiges Add‑On.

## Schritt 4: Häufige Randfälle beim **Konvertieren von Bild‑PDFs** behandeln

Obwohl der grundlegende Ablauf für die meisten PDFs funktioniert, können reale Dateien unerwartete Probleme verursachen:

| Situation | Warum es passiert | Wie man es handhabt |
|-----------|-------------------|----------------------|
| **Gedrehte Seiten** | Scanner drehen Seiten manchmal automatisch um 90°. | Setzen Sie `ocrEngine.RotatePages = true` bevor Sie `RecognizePdf` aufrufen. |
| **Gemischte Sprachen** | Rechnungen können französische oder deutsche Begriffe enthalten. | Verwenden Sie `OcrLanguage.Multilingual` oder kombinieren Sie mehrere Sprachen mit `|` (z. B. `OcrLanguage.English \| OcrLanguage.French`). |
| **Große Dateien (> 100 Seiten)** | Die Beschränkungen der kostenlosen Testversion können die Verarbeitung mitten in der Datei stoppen. | Kaufen Sie eine Lizenz oder teilen Sie das PDF vor dem OCR mit `Aspose.Pdf` in Stücke. |
| **Niedrigauflösende Scans** | Der Text wird unscharf, die OCR‑Genauigkeit sinkt. | Erhöhen Sie die DPI mit `ocrEngine.ImageResolution = 300` (Standard ist 200). |

Die Behandlung dieser Szenarien stellt sicher, dass Ihre **OCR‑Konvertierung von PDFs**‑Pipeline in der Produktion robust bleibt.

## Schritt 5: Den gesamten Prozess automatisieren (in einer Methode kapseln)

Wenn Sie einen Rechnungsverarbeitungs‑Service bauen, möchten Sie wahrscheinlich eine wiederverwendbare Methode. Hier ist eine kompakte Version, die Eingabe‑ und Ausgabepfade akzeptiert, die Drehung behandelt und den extrahierten Text zurückgibt.

```csharp
using Aspose.OCR;
using Aspose.Pdf;
using System;
using System.Text;

public static class PdfSearchableHelper
{
    /// <summary>
    /// Converts an image‑only PDF to a searchable PDF and returns the hidden text.
    /// </summary>
    /// <param name="inputPath">Path to the scanned PDF.</param>
    /// <param name="outputPath">Path where the searchable PDF will be saved.</param>
    /// <returns>All extracted text as a single string.</returns>
    public static string ConvertAndExtract(string inputPath, string outputPath)
    {
        // 1️⃣ Initialize OCR engine
        var ocr = new OcrEngine
        {
            Language = OcrLanguage.English,
            OutputFormat = OcrOutputFormat.SearchablePdf,
            RotatePages = true,            // fixes rotated scans automatically
            ImageResolution = 300          // improve accuracy on low‑res scans
        };

        // 2️⃣ Perform conversion
        ocr.RecognizePdf(inputPath, outputPath);

        // 3️⃣ Load result and pull out hidden text
        var doc = new Document(outputPath);
        var sb = new StringBuilder();

        foreach (Page page in doc.Pages)
            sb.Append(page.Text);

        return sb.ToString();
    }
}
```

Sie können nun aufrufen:

```csharp
string extracted = PdfSearchableHelper.ConvertAndExtract(
    @"C:\Docs\contract_scanned.pdf",
    @"C:\Docs\contract_searchable.pdf");

Console.WriteLine("OCR completed. Extracted text length: " + extracted.Length);
```

Das ist ein vollständiger **Bild‑PDF‑Konvertierungs** → **durchsuchbares PDF**‑Workflow, alles in einer einzigen Methode verpackt, die Sie in jeden ASP.NET Core‑Service oder Konsolen‑App einbinden können.

## Häufig gestellte Fragen (FAQ)

**F: Funktioniert das auf macOS/Linux?**  
**A:** Absolut. Die .NET 6‑Runtime und Aspose OCR sind plattformübergreifend, sodass derselbe Code unter Windows, macOS und Linux‑Containern läuft.

**F: Was, wenn ich nur den Text brauche und das durchsuchbare PDF nicht benötige?**  
**A:** Überspringen Sie den `OutputFormat`‑Schritt und setzen Sie `OutputFormat = OcrOutputFormat.Text`. Die Engine gibt dann direkt reinen Text zurück.

**F: Kann ich die Metadaten des Original‑PDFs erhalten?**  
**A:** Ja. Nach der Konvertierung können Sie die Metadaten des Quell‑`Document`‑Objekts mit `doc.Info.Title`, `doc.Info.Author` usw. in das neue Objekt kopieren.

**F: Gibt es ein Limit für die Seitenzahl?**  
**A:** Die kostenlose Testversion begrenzt die Dokumente auf 20 Seiten. Eine Voll‑Lizenz hebt diese Beschränkung auf.

## Fazit

Sie wissen jetzt, wie man **durchsuchbare PDFs** erstellt

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}