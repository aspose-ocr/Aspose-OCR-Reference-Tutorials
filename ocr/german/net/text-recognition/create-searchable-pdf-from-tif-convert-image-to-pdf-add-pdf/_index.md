---
category: general
date: 2026-04-04
description: Erstellen Sie ein durchsuchbares PDF aus einem TIF‑Bild in C# – erfahren
  Sie, wie Sie ein Bild in PDF konvertieren, PDF‑Metadaten hinzufügen und ein durchsuchbares
  Dokument mit Aspose.OCR erzeugen.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- add metadata to pdf
- add pdf metadata
- create pdf from tif
language: de
og_description: Create searchable PDF from a TIF file with C#. Convert image to PDF,
  add PDF metadata, and produce a searchable document using Aspose.OCR.
og_title: Durchsuchbares PDF aus TIF erstellen – Schritt‑für‑Schritt‑Anleitung
tags:
- Aspose.OCR
- C#
- PDF generation
title: Durchsuchbares PDF aus TIF erstellen – Bild in PDF konvertieren, PDF‑Metadaten
  hinzufügen
url: /de/net/text-recognition/create-searchable-pdf-from-tif-convert-image-to-pdf-add-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Durchsuchbares PDF aus TIF erstellen – Vollständige C#‑Anleitung

Haben Sie jemals **ein durchsuchbares PDF** aus einer gescannten Rechnung erstellen müssen, waren sich aber nicht sicher, wie Sie den Text durchsuchbar und die Dateimetadaten ordentlich halten können? Sie sind nicht allein. In vielen Automatisierungsprojekten muss das PDF sowohl maschinenlesbar als auch korrekt mit Informationen wie Titel, Autor und Vertrauensschwellen versehen sein.  

In diesem Leitfaden gehen wir Schritt für Schritt durch eine komplette Lösung, die **ein Bild in PDF konvertiert**, **PDF‑Metadaten einfügt** und OCR‑Ergebnisse mit niedriger Sicherheit filtert – alles mit der Aspose.OCR‑Bibliothek. Am Ende haben Sie ein einsatzbereites Snippet, das Sie in jedes .NET‑Projekt einbinden können, sowie einige Tipps zum Umgang mit Sonderfällen.

## Voraussetzungen

- .NET 6.0 oder höher (der Code funktioniert auch mit .NET Framework 4.6+)  
- Aspose.OCR NuGet‑Paket (`Install-Package Aspose.OCR`)  
- Ein TIF‑Bild, das Sie in ein durchsuchbares PDF umwandeln möchten (z. B. `input.tif`)  
- Grundlegende Kenntnisse in C# und Visual Studio (oder Ihrer bevorzugten IDE)

Es werden keine externen Dienste benötigt – der gesamte Prozess läuft lokal.

## Schritt 1 – OCR‑Engine einrichten (Kern für durchsuchbares PDF)

Das Erste, was wir benötigen, ist eine `OcrEngine`‑Instanz, die weiß, welche Sprache erkannt werden soll. In den meisten geschäftlichen Szenarien reicht Englisch aus, aber Sie können `Language.English` durch jede unterstützte Sprache ersetzen.

```csharp
using Aspose.OCR;
using Aspose.OCR.Pdf;   // PDF‑related extensions

// Initialize OCR engine with English language
OcrEngine ocrEngine = new OcrEngine
{
    Language = Language.English
};
```

**Warum das wichtig ist:** Die OCR‑Engine übernimmt die schwere Arbeit, Rasterpixel in Unicode‑Text zu verwandeln. Die korrekte Spracheinstellung verbessert die Genauigkeit und reduziert die Anzahl von Wörtern mit niedriger Sicherheit, die später herausgefiltert werden.

> **Pro‑Tipp:** Wenn Sie mehrsprachige Dokumente verarbeiten, instanziieren Sie mehrere Engines oder verwenden Sie `Language.Multilingual`, damit Aspose die Spracherkennung automatisch übernimmt.

## Schritt 2 – TIF‑Bild laden (PDF aus TIF erstellen)

Jetzt zeigen wir der Engine die Quelldatei. Der Helfer `ImageStream.FromFile` liest das Bild in einen Stream, den die OCR‑Engine verarbeiten kann.

```csharp
// Load the TIF image you want to make searchable
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/input.tif");
```

Vielleicht fragen Sie sich, *„Kann ich stattdessen ein JPEG oder PNG verwenden?“* Absolut – Aspose.OCR unterstützt die meisten Rasterformate. Ändern Sie einfach die Dateierweiterung und Sie sind startklar.

## Schritt 3 – PDF‑Optionen konfigurieren (Metadaten zum PDF hinzufügen)

Bevor wir konvertieren, definieren wir ein `PdfOptions`‑Objekt. Hier fügen wir **PDF‑Metadaten** wie Titel und Autor hinzu und geben der Engine gleichzeitig an, Wörter zu verwerfen, deren Sicherheit unter einem Schwellenwert liegt.

```csharp
PdfOptions searchablePdfOptions = new PdfOptions
{
    Title = "Invoice #12345",
    Author = "MyCompany",
    // Hide words with confidence lower than 0.8 (80%)
    MinConfidence = 0.8f
};
```

**Was passiert hier?**  
- `Title` und `Author` werden Teil des Dokumenten‑Informations‑Dictionaries des PDFs und erleichtern das Indexieren in Dokumenten‑Management‑Systemen.  
- `MinConfidence` ist ein Sicherheitsnetz: OCR liest häufig schwache Zeichen falsch; das Filtern dieser Wörter hält die durchsuchbare Ebene sauber und verbessert die nachfolgende Textextraktion.

Falls Sie benutzerdefinierte Metadaten benötigen (z. B. `Subject`, `Keywords`), können Sie diese über `PdfOptions.CustomProperties` setzen.

## Schritt 4 – Bild in ein durchsuchbares PDF konvertieren (Bild zu PDF)

Mit der vorbereiteten Engine und den gesetzten Optionen führt der abschließende Aufruf die Konvertierung aus. Er schreibt ein durchsuchbares PDF auf die Festplatte und bettet die OCR‑Textebene unter das Originalbild ein.

```csharp
ocrEngine.ConvertToSearchablePdf(
    outputPath: @"YOUR_DIRECTORY/output.pdf",
    pdfOptions: searchablePdfOptions);
```

Nach Ausführung dieser Zeile enthält `output.pdf`:
- Das ursprüngliche TIF‑Bild als visuellen Hintergrund  
- Eine unsichtbare Textebene, die von Suchmaschinen und Kopier‑Einfüge‑Operationen gelesen werden kann  
- Die zuvor definierten Metadaten (Titel, Autor usw.)

### Erwartetes Ergebnis

Öffnen Sie das erzeugte PDF in Adobe Reader oder einem anderen PDF‑Betrachter und versuchen Sie, Text zu markieren. Sie sollten Sätze kopieren können, die dem Original‑Scan entsprechen. Im Dialog **Eigenschaften** des Dokuments wird der Titel „Invoice #12345“ und der Autor „MyCompany“ angezeigt.

## Schritt 5 – Filterung der Sicherheit prüfen (Warum MinConfidence hilft)

Es ist sinnvoll zu überprüfen, ob Wörter mit niedriger Sicherheit tatsächlich entfernt wurden. Sie können den versteckten Text des PDFs mit einem Tool wie `pdftotext` inspizieren:

```bash
pdftotext output.pdf - | grep -i "unlikelyword"
```

Wenn das Wort nie erscheint, hat der `MinConfidence`‑Filter wie vorgesehen funktioniert. Passen Sie den Schwellenwert (z. B. `0.7f`) an, wenn Sie einen aggressiveren oder milderen Filter benötigen.

## Schritt 6 – Mehrere Seiten verarbeiten (Durchsuchbares PDF aus mehrseitigem TIF)

Viele Rechnungen liegen als mehrseitige TIFFs vor. Aspose.OCR behandelt jeden Frame automatisch als separate Seite. Zeigen Sie einfach die Engine auf die mehrseitige Datei; derselbe Aufruf `ConvertToSearchablePdf` erzeugt ein mehrseitiges durchsuchbares PDF.

```csharp
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/multi_page.tif");
ocrEngine.ConvertToSearchablePdf(@"YOUR_DIRECTORY/multi_output.pdf", searchablePdfOptions);
```

**Sonderfall:** Wenn eine Seite leer ist, kann OCR trotzdem eine leere Textebene erzeugen, was harmlos ist. Sie können leere Seiten jedoch überspringen, indem Sie vor der Konvertierung `ocrEngine.HasText` prüfen.

## Schritt 7 – Vollständiges Beispiel paketieren (Alle Schritte zusammen)

Unten finden Sie ein einzelnes, sofort ausführbares Programm, das alles zusammenführt. Ersetzen Sie `YOUR_DIRECTORY` durch den tatsächlichen Ordnerpfad auf Ihrem Rechner.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Pdf;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = Language.English
        };

        // 2️⃣ Load the TIF image (create pdf from tif)
        string inputPath = @"YOUR_DIRECTORY/input.tif";
        ocrEngine.Image = ImageStream.FromFile(inputPath);

        // 3️⃣ Set PDF metadata and confidence filter
        PdfOptions pdfOptions = new PdfOptions
        {
            Title = "Invoice #12345",
            Author = "MyCompany",
            MinConfidence = 0.8f
        };

        // 4️⃣ Convert to searchable PDF (convert image to pdf)
        string outputPath = @"YOUR_DIRECTORY/output.pdf";
        ocrEngine.ConvertToSearchablePdf(outputPath, pdfOptions);

        Console.WriteLine($"✅ Searchable PDF created at: {outputPath}");
    }
}
```

Führen Sie das Programm aus (`dotnet run` oder drücken Sie **F5** in Visual Studio) und Sie sehen die Bestätigungsnachricht. Das erzeugte PDF liegt neben Ihrem Quellbild und ist bereit für Indexierung oder Archivierung.

## Häufige Fragen & Stolperfallen

| Frage | Antwort |
|----------|--------|
| **Kann ich eine benutzerdefinierte Schriftart zur durchsuchbaren Ebene hinzufügen?** | Die OCR‑Ebene verwendet Unicode; das visuelle Erscheinungsbild wird vom zugrunde liegenden Bild bestimmt, sodass kein zusätzliches Einbetten von Schriftarten nötig ist. |
| **Was, wenn mein TIF farbig ist?** | Aspose.OCR konvertiert Farbbilder automatisch in Graustufen für die OCR, Sie können jedoch die Originalfarben im PDF beibehalten, indem Sie `PdfOptions.PreserveColor = true` setzen. |
| **Ist die Bibliothek thread‑sicher?** | Jede `OcrEngine`‑Instanz sollte nur von einem einzelnen Thread verwendet werden. Für parallele Verarbeitung erstellen Sie pro Thread eine separate Engine. |
| **Wie verschlüssele ich das PDF?** | Verwenden Sie `PdfOptions.Security`, um nach der OCR‑Konvertierung ein Passwort und Berechtigungen festzulegen. |

## Nächste Schritte (Ihr PDF‑Toolkit erweitern)

- **Batch‑Verarbeitung:** Durchlaufen Sie einen Ordner mit TIFFs und erzeugen Sie für jede Datei ein durchsuchbares PDF.  
- **Nachbearbeitung:** Nutzen Sie Aspose.PDF, um die erzeugten PDFs zu einem einzigen Master‑Dokument zusammenzuführen.  
- **Erweiterte Metadaten:** Befüllen Sie benutzerdefinierte XMP‑Felder für eine bessere Integration mit SharePoint oder ECM‑Systemen.  

All diese Erweiterungen bauen auf dem Kernmuster auf, das wir gerade behandelt haben: **durchsuchbares PDF erstellen**, **Bild zu PDF konvertieren** und **PDF‑Metadaten hinzufügen**.

---

*Viel Spaß beim Coden! Wenn Sie auf Probleme stoßen, hinterlassen Sie einen Kommentar unten oder schauen Sie in die Aspose.OCR‑Dokumentation für die neuesten API‑Updates.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}