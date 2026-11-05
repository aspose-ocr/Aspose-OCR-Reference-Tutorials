---
category: general
date: 2026-05-28
description: Erstellen Sie ein durchsuchbares PDF mit Aspose OCR in C#. Erfahren Sie,
  wie Sie OCR auf PDF anwenden, Text in PDF erkennen und ein mit OCR gescanntes PDF
  in ein durchsuchbares PDF umwandeln.
draft: false
keywords:
- create searchable pdf
- run ocr on pdf
- recognize text pdf
- ocr scanned pdf
- aspose ocr pdf
language: de
og_description: Erstellen Sie ein durchsuchbares PDF mit Aspose OCR in C#. Folgen
  Sie dieser Schritt‑für‑Schritt‑Anleitung, um OCR auf PDFs anzuwenden, Text in PDFs
  zu erkennen und gescannte PDF‑Dateien mit OCR zu verarbeiten.
og_title: Durchsuchbares PDF mit Aspose OCR erstellen – OCR auf PDF anwenden
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: Create searchable PDF using Aspose OCR in C#. Learn how to run OCR
    on PDF, recognize text PDF, and turn an OCR scanned PDF into a searchable PDF.
  headline: Create Searchable PDF with Aspose OCR – Run OCR on PDF
  type: TechArticle
- description: Create searchable PDF using Aspose OCR in C#. Learn how to run OCR
    on PDF, recognize text PDF, and turn an OCR scanned PDF into a searchable PDF.
  name: Create Searchable PDF with Aspose OCR – Run OCR on PDF
  steps:
  - name: Multiple Languages (OCR Scanned PDF)
    text: 'If your source PDF contains both English and Spanish text, combine languages:'
  - name: Password‑Protected PDFs
    text: 'When dealing with secured PDFs, supply the password before calling `Recognize`:'
  - name: Controlling Image Quality
    text: 'Higher DPI yields better OCR results but consumes more memory. Adjust the
      DPI if you notice garbled characters:'
  - name: License vs. Evaluation Mode
    text: 'In evaluation mode a watermark appears on each page. To remove it, apply
      your license before any OCR call:'
  - name: What’s Next?
    text: '- Explore the **aspose ocr pdf** API further: extract plain text, export
      to DOCX, or generate searchable PDFs in bulk. - Combine the searchable PDF output
      with Aspose.PDF to add bookmarks or watermarks. - Experiment with different
      DPI settings or custom OCR dictionaries for niche fonts.'
  type: HowTo
tags:
- Aspose
- OCR
- PDF
- C#
title: Durchsuchbares PDF mit Aspose OCR erstellen – OCR auf PDF anwenden
url: /de/net/text-recognition/create-searchable-pdf-with-aspose-ocr-run-ocr-on-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Durchsuchbares PDF mit Aspose OCR erstellen – OCR auf PDF ausführen

Haben Sie jemals **durchsuchbare PDF**‑Dateien aus einem Stapel gescannter Dokumente erstellen müssen? Sie sind nicht allein. In vielen Büroabläufen ist das Einzige, was Sie von einem vollständig durchsuchbaren Archiv trennt, ein paar Code‑Zeilen, die OCR auf PDF‑Seiten ausführen.  

In diesem Tutorial führen wir Sie durch ein komplettes, sofort ausführbares Beispiel, das genau zeigt, wie man **durchsuchbare PDF**‑Dateien mit der Aspose OCR für .NET‑Bibliothek erstellt. Am Ende wissen Sie, wie man *OCR auf PDF* ausführt, *Text‑PDF*‑Dateien erkennt und ein *OCR‑gescanntes PDF* in eine durchsuchbare Version umwandelt, ohne Drittanbieterdienste.

> **Voraussetzungen** – Ein aktuelles .NET‑SDK (empfohlen 6.0+), eine gültige Aspose.OCR für .NET‑Lizenz (oder ein temporärer Evaluierungsschlüssel) und ein PDF, das Sie verarbeiten möchten.

![Create searchable PDF diagram](alt="Diagram illustrating the create searchable pdf workflow using Aspose OCR")  

---

## Was dieser Leitfaden abdeckt

- Einrichten der Aspose OCR‑Bibliothek in einem C#‑Projekt.  
- Laden eines Quell‑PDFs (beliebige Seitenzahl).  
- Konfigurieren der Engine, um ein **durchsuchbares PDF** auszugeben.  
- Ausführen des OCR‑Prozesses und Speichern des Ergebnisses.  
- Tipps zum Umgang mit mehrseitigen Dokumenten, Sprachauswahl und häufigen Fallstricken.  

Wenn Sie jeden Schritt befolgen, erhalten Sie eine Datei, die Sie in Adobe Reader öffnen, **Strg + F** drücken und sofort nach jedem Wort suchen können, das in der Original‑Scannung vorkam.

## Schritt 1: Aspose OCR für .NET installieren

Bevor Sie Code schreiben, fügen Sie das NuGet‑Paket zu Ihrem Projekt hinzu:

```bash
dotnet add package Aspose.OCR
```

> **Pro‑Tipp:** Verwenden Sie das `--version`‑Flag, um auf die neueste stabile Version zu fixieren (z. B. `Aspose.OCR 23.10`). Das gewährleistet die Kompatibilität mit .NET 6 und neuer.

---

## Schritt 2: Eine OCR‑Engine‑Instanz erstellen

Das Herzstück des Prozesses ist die `OcrEngine`. Stellen Sie sich sie als das Gehirn vor, das Bilder liest und Text ausgibt. Die Initialisierung ist unkompliziert:

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

namespace PdfSearchableDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 2: Instantiate the OCR engine
            var ocrEngine = new OcrEngine();
```

Das `OcrEngine`‑Objekt enthält sowohl den Eingabebild‑Stream als auch die Konfiguration, die Aspose mitteilt, wie die Ausgabe aussehen soll.

## Schritt 3: Das Quell‑PDF laden (OCR auf PDF ausführen)

Aspose OCR kann ein PDF direkt einlesen; es extrahiert intern jede Seite als Bild. Ersetzen Sie den Platzhalterpfad durch den Speicherort Ihres gescannten Dokuments:

```csharp
            // Step 3: Load the source PDF – this is where we *run OCR on PDF*
            string inputPath = @"C:\Docs\handbook.pdf";
            ocrEngine.Image = ImageStream.FromFile(inputPath);
```

> **Warum das funktioniert:** Die Methode `ImageStream.FromFile` erkennt das PDF‑Format automatisch und bereitet eine Rasterdarstellung für OCR vor. Ein zusätzlicher Konvertierungsschritt ist nicht erforderlich.

## Schritt 4: Ausgabeformat und Sprache konfigurieren

Hier teilen wir Aspose mit, was wir zurückhaben wollen. Das Setzen von `OutputFormat` auf `SearchablePdf` weist die Engine an, den erkannten Text hinter den ursprünglichen Seitenbildern einzubetten und ein **durchsuchbares PDF** zu erzeugen. Sie können auch die Sprache auswählen, um die Genauigkeit zu verbessern – Englisch ist die Vorgabe, aber Sie können zu Französisch, Deutsch usw. wechseln.

```csharp
            // Step 4: Choose output format and language
            ocrEngine.Configuration.OutputFormat = OutputFormat.SearchablePdf; // creates searchable PDF
            ocrEngine.Configuration.Language = Language.English;               // *recognize text PDF* in English
```

Wenn Sie ein zweisprachiges Dokument verarbeiten müssen, können Sie Sprachen mit den `Language`‑Enum‑Flags kombinieren.

## Schritt 5: OCR‑Prozess ausführen – Text‑PDF erkennen

Jetzt findet die eigentliche Arbeit statt. Die Methode `Recognize` scannt jede Seite, extrahiert Glyphen und erstellt einen internen PDF‑Stream, der sowohl das Originalbild als auch eine unsichtbare Textebene enthält. Dies ist der Schritt, in dem wir *Text‑PDF erkennen*.

```csharp
            // Step 5: Execute OCR – this *recognizes text PDF* and builds the searchable stream
            ocrEngine.Recognize();
```

> **Häufige Frage:** *Was, wenn das PDF 200 Seiten hat?*  
> Die Engine verarbeitet die Seiten sequenziell und streamt die Ergebnisse, sodass der Speicherverbrauch moderat bleibt. Bei extrem großen Dateien sollten Sie jedoch die Einstellung `MemoryLimit` in `ocrEngine.Configuration` erhöhen.

## Schritt 6: Das durchsuchbare PDF speichern

Schließlich schreiben Sie die Ausgabe auf die Festplatte. Die Methode `Save` schreibt den internen Stream in eine neue Datei, die Sie mit jedem PDF‑Betrachter öffnen können.

```csharp
            // Step 6: Save the searchable PDF to disk
            string outputPath = @"C:\Docs\handbook_searchable.pdf";
            ocrEngine.Save(outputPath);

            Console.WriteLine($"Searchable PDF created at: {outputPath}");
        }
    }
}
```

Führen Sie das Programm (`dotnet run`) aus und beobachten Sie, wie die Konsole die Dateierstellung bestätigt. Öffnen Sie `handbook_searchable.pdf` und versuchen Sie, nach einem Wort zu suchen, von dem Sie wissen, dass es in der Original‑Scannung vorkommt – Sie sollten sofort Treffer sehen.

## Umgang mit Sonderfällen und erweiterten Szenarien

### Mehrere Sprachen (OCR‑gescanntes PDF)

Wenn Ihr Quell‑PDF sowohl englischen als auch spanischen Text enthält, kombinieren Sie die Sprachen:

```csharp
ocrEngine.Configuration.Language = Language.English | Language.Spanish;
```

### Passwortgeschützte PDFs

Wenn Sie mit gesicherten PDFs arbeiten, geben Sie das Passwort an, bevor Sie `Recognize` aufrufen:

```csharp
ocrEngine.Image = ImageStream.FromFile(inputPath, "MySecretPassword");
```

Ist das Passwort falsch, wirft `Recognize` eine `InvalidPasswordException`; das Abfangen ermöglicht es, den Benutzer nach dem korrekten Passwort zu fragen.

### Bildqualität steuern

Eine höhere DPI liefert bessere OCR‑Ergebnisse, verbraucht jedoch mehr Speicher. Passen Sie die DPI an, wenn Sie verzerrte Zeichen bemerken:

```csharp
ocrEngine.Configuration.Dpi = 300; // default is 200
```

### Lizenz‑ vs. Evaluierungsmodus

Im Evaluierungsmodus erscheint ein Wasserzeichen auf jeder Seite. Um es zu entfernen, wenden Sie Ihre Lizenz vor jedem OCR‑Aufruf an:

```csharp
var license = new License();
license.SetLicense(@"C:\Aspose\Aspose.OCR.lic");
```

## Pro‑Tipps für den Produktionseinsatz

- **Batch‑Verarbeitung:** Packen Sie die Kernlogik in eine `foreach`‑Schleife, die über eine Liste von PDFs iteriert. Entsorgen Sie die `OcrEngine` nach jeder Datei, um native Ressourcen freizugeben.  
- **Logging:** Verwenden Sie `ocrEngine.Configuration.Logger`, um detaillierte OCR‑Statistiken zu erfassen (z. B. erkannte Zeichen pro Sekunde). Das ist beim Troubleshooting niedriger Genauigkeit unverzichtbar.  
- **Performance‑Optimierung:** Für Multi‑Core‑Server instanziieren Sie separate `OcrEngine`‑Objekte pro Thread; die Bibliothek ist thread‑sicher, wenn jede Instanz isoliert ist.  
- **Fehlerbehandlung:** Umschließen Sie `Recognize` und `Save` stets mit `try/catch`‑Blöcken. Typische Ausnahmen sind `FileNotFoundException`, `OutOfMemoryException` und `UnsupportedFormatException`.

## Vollständiges funktionierendes Beispiel (zum Kopieren‑Einfügen bereit)

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

namespace PdfSearchableDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Apply license (optional – removes evaluation watermark)
            // var license = new License();
            // license.SetLicense(@"C:\Aspose\Aspose.OCR.lic");

            // 1️⃣ Create OCR engine
            var ocrEngine = new OcrEngine();

            // 2️⃣ Load PDF – this is where we *run OCR on PDF*
            string inputPath = @"C:\Docs\handbook.pdf";
            ocrEngine.Image = ImageStream.FromFile(inputPath);

            // 3️⃣ Configure output as searchable PDF and set language
            ocrEngine.Configuration.OutputFormat = OutputFormat.SearchablePdf;
            ocrEngine.Configuration.Language = Language.English;

            // 4️⃣ Run OCR – *recognize text PDF*
            ocrEngine.Recognize();

            // 5️⃣ Save the searchable PDF
            string outputPath = @"C:\Docs\handbook_searchable.pdf";
            ocrEngine.Save(outputPath);

            Console.WriteLine($"Searchable PDF created at: {outputPath}");
        }
    }
}
```

**Erwartete Ausgabe** (Konsole):

```
Searchable PDF created at: C:\Docs\handbook_searchable.pdf
```

Öffnen Sie die resultierende Datei, drücken Sie **Strg + F**, und Sie können jedes Wort finden, das in den ursprünglichen gescannten Seiten vorkam. Das ist die Magie, ein *OCR‑gescanntes PDF* in ein **durchsuchbares PDF** zu verwandeln.

## Fazit

Wir haben gerade gezeigt, wie man mit Aspose OCR für .NET **durchsuchbare PDF**‑Dateien erstellt, von der Installation des Pakets bis zum Umgang mit mehrsprachigen und passwortgeschützten PDFs. Wenn Sie diese Schritte befolgen, können Sie zuverlässig *OCR auf PDF*‑Dokumenten ausführen, *Text‑PDF*‑Inhalte erkennen und jedes *OCR‑gescannte PDF* in ein vollständig durchsuchbares Asset umwandeln.

### Was kommt als Nächstes?

- Erkunden Sie die **aspose ocr pdf**‑API weiter: extrahieren Sie Klartext, exportieren Sie nach DOCX oder erzeugen Sie durchsuchbare PDFs in großen Mengen.  
- Kombinieren Sie die Ausgabe des durchsuchbaren PDFs mit Aspose.PDF, um Lesezeichen oder Wasserzeichen hinzuzufügen.  
- Experimentieren Sie mit verschiedenen DPI‑Einstellungen oder benutzerdefinierten OCR‑Wörterbüchern für spezielle Schriftarten.

Passen Sie das Beispiel gerne an, integrieren Sie es in Ihre Dokumenten‑Management‑Pipeline oder stellen Sie Fragen in den Kommentaren. Viel Spaß beim Programmieren und beim Verwandeln dieser unlesbaren Scans in durchsuchbares Gold!

## Verwandte Tutorials

- [Wie man PDF in .NET mit Aspose.OCR OCR‑t](/ocr/english/net/text-recognition/recognize-pdf/)
- [Wie man OCR auf PDF in .NET mit Aspose.OCR macht](/ocr/spanish/net/text-recognition/recognize-pdf/)
- [Wie man OCR auf eine PDF‑Datei in .NET mit Aspose.OCR durchführt](/ocr/arabic/net/text-recognition/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}