---
category: general
date: 2026-01-04
description: Erstellen Sie schnell ein durchsuchbares PDF aus einem gescannten PDF.
  Erfahren Sie, wie Sie gescannte PDFs konvertieren, OCR zu PDFs hinzufügen und die
  Bildqualität mit Aspose OCR in C# anpassen.
draft: false
keywords:
- create searchable pdf
- convert scanned pdf
- add ocr to pdf
- adjust image quality
- how to use ocr
language: de
og_description: Erstellen Sie schnell ein durchsuchbares PDF aus einem gescannten
  PDF. Folgen Sie dieser Schritt‑für‑Schritt‑Anleitung, um gescannte PDFs zu konvertieren,
  OCR zum PDF hinzuzufügen und die Bildqualität anzupassen.
og_title: Durchsuchbare PDF aus gescannten Dateien mit Aspose OCR erstellen
tags:
- Aspose OCR
- C#
- PDF processing
title: Durchsuchbares PDF aus gescannten Dateien mit Aspose OCR erstellen
url: /de/net/ocr-optimization/create-searchable-pdf-from-scanned-files-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Durchsuchbare PDF aus gescannten Dateien mit Aspose OCR erstellen

Haben Sie schon einmal **durchsuchbare PDFs** aus einem Stapel gescannter Dokumente erstellen wollen, wussten aber nicht, wo Sie anfangen sollen? Sie sind nicht allein – viele Entwickler stoßen an diese Hürde, wenn sie Dokumenten‑Management‑Pipelines aufbauen. Die gute Nachricht? Mit Aspose OCR können Sie **gescannte PDFs konvertieren**, OCR hinzufügen und die Bildqualität in nur wenigen Zeilen C# feinjustieren.

In diesem Tutorial führen wir Sie durch den gesamten Prozess, vom Laden eines gescannten PDFs bis zum Speichern einer vollständig durchsuchbaren Version. Am Ende wissen Sie genau **wie man OCR** mit Aspose verwendet, warum jede Einstellung wichtig ist und was Sie anpassen können, wenn etwas nicht wie geplant funktioniert. Keine vagen Verweise – nur ein komplettes, ausführbares Beispiel, das Sie noch heute in Ihr Projekt übernehmen können.

## Voraussetzungen

Bevor wir starten, stellen Sie sicher, dass Sie Folgendes haben:

- .NET 6.0 oder höher (der Code funktioniert auch mit .NET Core und .NET Framework)
- Eine gültige Aspose OCR‑Lizenz (die kostenlose Testversion reicht für Tests)
- Ein Eingabe‑PDF namens `input.pdf` in einem Ordner Ihrer Wahl
- Visual Studio 2022 oder einen anderen C#‑Editor Ihrer Präferenz

Das war’s. Wenn Ihnen etwas davon unbekannt ist, pausieren Sie und installieren Sie das fehlende Element – sonst wird nichts weiter benötigt.

## Schritt 1: OCR‑Engine initialisieren und das gescannte PDF laden  
**(Hier fügen wir das **OCR zum PDF** zum ersten Mal hinzu.)**

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// Create the OCR engine instance
OcrEngine ocrEngine = new OcrEngine();

// Load the scanned PDF from disk
ocrEngine.LoadPdf(@"C:\Docs\input.pdf");
```

*Warum dieser Schritt?*  
Der `OcrEngine` ist das Herzstück von Aspose OCR. Das Laden des PDFs teilt der Engine mit, wo sie die Rasterbilder findet, die später analysiert werden sollen. Überspringen Sie diesen Schritt, gibt es nichts zu konvertieren, und die nachfolgenden Schritte werfen eine Ausnahme.

> **Pro‑Tipp:** Wenn Ihr PDF passwortgeschützt ist, verwenden Sie `ocrEngine.LoadPdf(path, password)`, um einen Laufzeitfehler zu vermeiden.

## Schritt 2: Primäre und zusätzliche Sprachen festlegen  
**(Wir **konvertieren das gescannte PDF** in Englisch, Französisch und Deutsch.)**

```csharp
// Primary language – the most common language in the document
ocrEngine.Config.Language = Language.English;

// Add extra languages if the document contains multilingual text
ocrEngine.Config.AdditionalLanguages = new[] { Language.French, Language.German };
```

*Warum ist die Sprache wichtig?*  
Die OCR‑Genauigkeit hängt vom erwarteten Zeichensatz ab. Durch die Angabe von Englisch als Primärsprache und das Hinzufügen von Französisch/Deutsch kann die Engine Akzentzeichen und Sonderglyphen korrekt interpretieren. Wird dies vergessen, führt das häufig zu unleserlichem Text.

## Schritt 3: Bildqualität anpassen – PDF‑Ausgabe feinjustieren  
**(Hier **passen wir die Bildqualität** an, um Dateigröße und Lesbarkeit auszubalancieren.)**

```csharp
PdfSaveOptions pdfOptions = new PdfSaveOptions
{
    ImageQuality = 90,          // JPEG quality for embedded images (0‑100)
    Compress = true,            // Enable PDF compression to shrink file size
    PreserveOriginalLayout = true // Keep the scanned layout intact
};
```

*Warum `ImageQuality` anpassen?*  
Ein höherer Wert (90‑100) bewahrt die Schärfe, was für die OCR‑Genauigkeit entscheidend ist, vergrößert jedoch die Dateigröße. Wenn Sie Millionen von Seiten archivieren, reduzieren Sie den Wert auf 70‑80 für ein schlankeres PDF, ohne die Lesbarkeit zu stark zu beeinträchtigen.

## Schritt 4: Ergebnis als durchsuchbares PDF speichern  
**(Jetzt **erstellen wir das durchsuchbare PDF**, das Sie indexieren können.)**

```csharp
// Export the OCR result as a searchable PDF
ocrEngine.SaveAsSearchablePdf(@"C:\Docs\output.pdf", pdfOptions);

// Let the user know we’re done
Console.WriteLine("Searchable PDF created at C:\\Docs\\output.pdf");
```

*Was passiert dabei eigentlich?*  
Aspose OCR extrahiert die Textebene jeder Seite und bettet sie hinter dem Originalbild ein. Das PDF sieht visuell unverändert aus, Sie können jedoch jetzt Text auswählen, kopieren und durchsuchen – ein großer Gewinn für nachgelagerte Workflows.

## Schritt 5: Ausgabe prüfen (optional, aber empfohlen)  
Es ist leicht anzunehmen, dass alles funktioniert hat, aber ein kurzer Plausibilitätstest spart später Kopfschmerzen.

```csharp
using System.Diagnostics;

// Open the generated PDF automatically (Windows only)
Process.Start(new ProcessStartInfo
{
    FileName = @"C:\Docs\output.pdf",
    UseShellExecute = true
});
```

Öffnen Sie die Datei, versuchen Sie ein Wort zu markieren oder drücken Sie `Ctrl+F` und geben Sie einen Ausdruck ein, von dem Sie wissen, dass er im Originalscan vorkommt. Wenn der Text auswählbar ist, haben Sie erfolgreich **durchsuchbare PDFs erstellt**.

## Häufige Sonderfälle & deren Behandlung  

| Situation | Warum es passiert | Schnelllösung |
|-----------|-------------------|---------------|
| **Seiten mit gemischter Auflösung** (einige 150 dpi, andere 300 dpi) | OCR‑Qualität variiert pro Seite, was zu ungleichmäßiger Durchsuchbarkeit führt. | `ocrEngine.Config.Dpi = 300;` vor dem Laden setzen, um Upsampling zu erzwingen, oder mit `ImageProcessor` die DPI normalisieren. |
| **Verschlüsseltes PDF** | Aspose OCR kann ohne Passwort nicht lesen. | Das Passwort wie oben bei `LoadPdf` übergeben. |
| **Große PDFs (>500 MB)** | Der Speicherverbrauch steigt stark, was zu `OutOfMemoryException` führt. | Dokument in Teilen verarbeiten: `ocrEngine.SplitPdfIntoPages();` dann jede Seite einzeln OCR‑verarbeiten und die Ergebnisse zusammenführen. |
| **Nicht‑lateinische Zeichen** (z. B. Kyrillisch) | Sprache nicht hinzugefügt, Zeichen werden zu “?” | `Language.Russian` (oder andere benötigte Sprache) zu `AdditionalLanguages` hinzufügen. |
| **Zu niedrige Bildqualität** | Text wird unscharf, OCR schlägt fehl. | `ImageQuality` erhöhen oder `pdfOptions.Dpi = 300;` setzen, um hochauflösende Bilder einzubetten. |

## Vollständiges, lauffähiges Beispiel  

Unten finden Sie das komplette Programm, das Sie in ein neues Konsolen‑App‑Projekt kopieren können. Es enthält alle Schritte, Fehlerbehandlung und Kommentare zur Klarheit.

```csharp
using System;
using System.Diagnostics;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace SearchablePdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Paths – adjust to your environment
            string inputPath = @"C:\Docs\input.pdf";
            string outputPath = @"C:\Docs\output.pdf";

            try
            {
                // 1️⃣ Initialize OCR engine and load scanned PDF
                OcrEngine ocrEngine = new OcrEngine();
                ocrEngine.LoadPdf(inputPath);

                // 2️⃣ Configure languages (primary + additional)
                ocrEngine.Config.Language = Language.English;
                ocrEngine.Config.AdditionalLanguages = new[] { Language.French, Language.German };

                // 3️⃣ Set PDF save options – adjust image quality as needed
                PdfSaveOptions pdfOptions = new PdfSaveOptions
                {
                    ImageQuality = 90,
                    Compress = true,
                    PreserveOriginalLayout = true
                };

                // 4️⃣ Save as searchable PDF
                ocrEngine.SaveAsSearchablePdf(outputPath, pdfOptions);
                Console.WriteLine($"✅ Searchable PDF created at {outputPath}");

                // 5️⃣ Optional: open the file to verify
                Process.Start(new ProcessStartInfo
                {
                    FileName = outputPath,
                    UseShellExecute = true
                });
            }
            catch (Exception ex)
            {
                // Friendly error message – helps during debugging
                Console.WriteLine($"❌ Oops! Something went wrong: {ex.Message}");
                // For real‑world apps, consider logging the stack trace
            }
        }
    }
}
```

**Erwartete Ausgabe:**  
```
✅ Searchable PDF created at C:\Docs\output.pdf
```

Wenn Sie `output.pdf` öffnen, sollten Sie in der Lage sein, jeden im Originalscan vorhandenen Text zu markieren und zu durchsuchen.

---

## Häufig gestellte Fragen (FAQs)

**F: Funktioniert das auch mit PDFs, die sowohl gescannte Bilder als auch nativen Text enthalten?**  
A: Absolut. Aspose OCR fügt nur dort, wo nötig, eine versteckte Textebene hinzu und lässt bestehenden Text unverändert.

**F: Kann ich einen Ordner mit PDFs stapelweise verarbeiten?**  
A: Ja. Wickeln Sie den obigen Code in eine `foreach (var file in Directory.GetFiles(folder, "*.pdf"))`‑Schleife und passen Sie den Ausgabepfad entsprechend an.

**F: Wie kann ich die endgültige PDF‑Größe weiter reduzieren?**  
A: `ImageQuality` auf 70‑80 senken, `Compress` aktivieren oder `pdfOptions.Dpi = 150` setzen, um Bilder vor dem Einbetten herunterzusampeln.

**F: Gibt es eine Möglichkeit, den OCR‑Text zu extrahieren, ohne ein PDF zu erstellen?**  
A: Rufen Sie `ocrEngine.ExtractText();` nach dem Laden des PDFs auf. Das liefert einen Klartext‑String, den Sie speichern oder indexieren können.

---

## Fazit  

Wir haben gerade **wie man OCR** mit Aspose verwendet, um **durchsuchbare PDFs** aus gescannten Dokumenten zu **erstellen**, gezeigt, **wie man gescannte PDFs konvertiert**, **OCR zu PDFs hinzufügt** und erklärt, **wie man die Bildqualität** für optimale Ergebnisse **anpasst**. Der vollständige Code‑Beispiel ist einsatzbereit, und die Fehler‑Tabelle sollte Ihnen helfen, wenn unerwartete Probleme auftreten.

Was kommt als Nächstes? Experimentieren Sie mit:

- Verschiedenen Sprachpaketen für mehrsprachige Archive
- Benutzerdefinierter Bildvorverarbeitung (Entzerrung, Rauschentfernung) via `ImageProcessor`
- Integration des durchsuchbaren PDFs in eine SharePoint‑ oder ElasticSearch‑Pipeline

Hinterlassen Sie gern einen Kommentar, wenn Sie auf ein Problem stoßen oder einen cleveren Trick entdeckt haben. Viel Spaß beim Coden und genießen Sie die sofort durchsuchbaren PDFs! 

![Durchsuchbares PDF‑Flussdiagramm, das OCR‑Engine → Sprachkonfiguration → PDF‑Speicheroptionen → durchsuchbares PDF‑Ergebnis zeigt](create-searchable-pdf-flow.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}