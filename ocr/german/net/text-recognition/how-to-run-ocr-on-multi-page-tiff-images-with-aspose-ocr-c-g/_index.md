---
category: general
date: 2026-02-11
description: Lernen Sie, wie Sie OCR auf ein mehrseitiges TIFF in C# mit Aspose OCR
  ausführen. Konvertieren Sie TIFF in Text, extrahieren Sie Text aus TIFF und erkennen
  Sie Text aus Bildern schnell.
draft: false
keywords:
- how to run OCR
- recognize text from image
- convert tiff to text
- extract text from tiff
- perform OCR on image
language: de
og_description: Wie man OCR auf einer mehrseitigen TIFF mit Aspose OCR in C# ausführt.
  Schritt‑für‑Schritt‑Anleitung zum Konvertieren von TIFF in Text, zum Extrahieren
  von Text aus TIFF und zum Erkennen von Text aus einem Bild.
og_title: Wie man OCR auf mehrseitigen TIFF‑Bildern ausführt – komplettes C#‑Tutorial
tags:
- OCR
- C#
- Aspose
- TIFF
title: Wie man OCR auf mehrseitigen TIFF‑Bildern mit Aspose OCR ausführt – C#‑Leitfaden
url: /de/net/text-recognition/how-to-run-ocr-on-multi-page-tiff-images-with-aspose-ocr-c-g/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR auf mehrseitigen TIFF‑Bildern mit Aspose OCR ausführen

Haben Sie sich jemals gefragt, **wie man OCR** auf einem gescannten TIFF ausführt, das mehrere Seiten enthält? Sie sind nicht allein – viele Entwickler stoßen auf dieses Problem, wenn sie durchsuchbaren Text aus alten Dokumenten extrahieren müssen. Die gute Nachricht? Mit Aspose OCR können Sie Text aus Bilddateien in nur wenigen Zeilen C#‑Code erkennen und erhalten einfachen zusammengefügten Text, der für die Indizierung oder weitere Verarbeitung bereitsteht.

In diesem Tutorial gehen wir den gesamten Workflow durch: von der Installation des Aspose OCR‑Pakets, über das Laden eines mehrseitigen TIFFs, bis hin zur Umwandlung von TIFF in Text und schließlich der Anzeige des extrahierten Inhalts. Am Ende können Sie **Text aus TIFF**‑Dateien **extrahieren**, **Text aus Bild**‑Quellen **erkennen** und den Prozess sogar für Dutzende von Dateien in einem Batch‑Job automatisieren. Keine Magie, nur klare, praktische Schritte.

## Was Sie lernen werden

- Wie Sie die Aspose OCR‑Engine für die Erkennung der englischen Sprache einrichten.  
- Der genaue Code, der zum **Konvertieren von TIFF zu Text** mit der `OcrEngine`‑Klasse benötigt wird.  
- Tipps zum Umgang mit mehrseitigen Bildern und zur korrekten Trennung jeder Seite.  
- Häufige Stolperfallen (wie fehlende native Abhängigkeiten) und wie Sie diese vermeiden können.  

**Voraussetzungen** – Sie benötigen .NET 6 oder höher, Visual Studio (oder einen beliebigen C#‑Editor) und eine Internetverbindung für die automatische Ressourcendownload‑Funktion. Das war’s; keine zusätzlichen nativen Bibliotheken, mit denen Sie kämpfen müssten.

---

## Schritt 1 – Aspose OCR NuGet‑Paket installieren

Bevor Sie **OCR auf Bild**‑Dateien ausführen können, müssen Sie die Bibliothek zu Ihrem Projekt hinzufügen.

```bash
dotnet add package Aspose.OCR
```

> **Pro‑Tipp:** Wenn Sie in Visual Studio arbeiten, können Sie auch mit der rechten Maustaste auf das Projekt klicken → *Manage NuGet Packages* → nach „Aspose.OCR“ suchen und *Install* klicken.

Das Paket enthält alles, was Sie benötigen, und mit `AutomaticResourceDownload = true` lädt die Engine Sprachpakete bei Bedarf nach.

---

## Schritt 2 – OCR‑Engine initialisieren (Wie man OCR ausführt)

Jetzt, wo das Paket vorhanden ist, erstellen und konfigurieren wir eine `OcrEngine`‑Instanz. Das ist das Herzstück von **wie man OCR** in unserem Szenario.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System.Drawing;   // For Image class
using System;

// Step 2: Create and configure the OCR engine
var ocrEngine = new OcrEngine
{
    Language = OcrLanguage.English,          // Recognize English text
    AutomaticResourceDownload = true,        // Auto‑download language data
    OutputFormat = OcrOutputFormat.Text      // Get plain concatenated text
};
```

**Warum das wichtig ist:** Durch das Setzen von `Language` teilen Sie der Engine mit, welchen Zeichensatz sie erwarten soll, während `AutomaticResourceDownload` Sie davon befreit, Sprachdateien manuell auf dem Server abzulegen. `OutputFormat` als `Text` liefert uns einen einfachen String – perfekt für **Konvertieren‑von‑TIFF‑zu‑Text**‑Pipelines.

---

## Schritt 3 – Mehrseitiges TIFF laden (Text aus Bild erkennen)

Ein TIFF kann viele Frames enthalten, von denen jeder eine Seite darstellt. Die Klasse `System.Drawing.Image` abstrahiert das für uns.

```csharp
// Step 3: Load the multi‑page image to be processed
using (var image = Image.FromFile("YOUR_DIRECTORY/multi_page.tiff"))
{
    // Step 4: Run OCR on the image
    var ocrResult = ocrEngine.Recognize(image);

    // Step 5: Display the extracted text
    Console.WriteLine(ocrResult.Text);
}
```

> **Was, wenn die Datei nicht im selben Ordner liegt?** Geben Sie einfach einen vollständigen absoluten Pfad an oder verwenden Sie `Path.Combine` mit `AppContext.BaseDirectory`.  
> **Wie steht es um die Speichernutzung?** Die `using`‑Anweisung gibt das Bild nach der Verarbeitung frei und verhindert Lecks – entscheidend, wenn Sie Dutzende großer TIFFs im Batch verarbeiten.

Der Aufruf `Recognize` iteriert automatisch über jede Seite im TIFF und verkettet die Ergebnisse mit Zeilenumbrüchen. Deshalb sehen Sie jede Seite getrennt, wenn Sie `ocrResult.Text` ausgeben.

---

## Schritt 4 – Vollständiges Beispiel (Alle Schritte in einer Datei)

Unten finden Sie eine komplette, sofort ausführbare Konsolenanwendung. Kopieren Sie sie in ein neues .NET‑Konsolenprojekt und drücken Sie **F5**.

```csharp
// File: Program.cs
using System;
using System.Drawing;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace TiffOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Configure the OCR engine
            var ocrEngine = new OcrEngine
            {
                Language = OcrLanguage.English,
                AutomaticResourceDownload = true,
                OutputFormat = OcrOutputFormat.Text
            };

            // 2️⃣ Load your multi‑page TIFF (replace with your actual path)
            const string tiffPath = @"YOUR_DIRECTORY\multi_page.tiff";

            if (!System.IO.File.Exists(tiffPath))
            {
                Console.WriteLine($"File not found: {tiffPath}");
                return;
            }

            // 3️⃣ Perform OCR
            using (var image = Image.FromFile(tiffPath))
            {
                var result = ocrEngine.Recognize(image);

                // 4️⃣ Output the extracted text
                Console.WriteLine("=== OCR RESULT ===");
                Console.WriteLine(result.Text);
                Console.WriteLine("==================");
            }

            // Keep console open
            Console.WriteLine("Press any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**Erwartete Ausgabe** (gekürzt zur Übersicht):

```
=== OCR RESULT ===
Page 1: The quick brown fox jumps over the lazy dog.
Page 2: Lorem ipsum dolor sit amet, consectetur adipiscing elit.
...
==================
Press any key to exit...
```

Jede Seite erscheint in einer eigenen Zeile, weil `OcrOutputFormat.Text` einen Zeilenumbruch zwischen den Frames einfügt. Wenn Sie ein anderes Trennzeichen benötigen, können Sie `result.Text` mit `String.Replace` nachbearbeiten.

---

## Schritt 5 – Umgang mit gängigen Sonderfällen

### 5.1 Große TIFF‑Dateien  
Wenn Sie mit TIFFs im Gigabyte‑Bereich arbeiten, kann das Laden der gesamten Datei in den Speicher problematisch sein. Eine Lösung besteht darin, jeden Frame einzeln zu verarbeiten:

```csharp
using (var image = Image.FromFile(tiffPath))
{
    for (int i = 0; i < image.GetFrameCount(FrameDimension.Page); i++)
    {
        image.SelectActiveFrame(FrameDimension.Page, i);
        var pageResult = ocrEngine.Recognize(image);
        Console.WriteLine($"--- Page {i + 1} ---");
        Console.WriteLine(pageResult.Text);
    }
}
```

### 5. Nicht‑englische Dokumente  
Wenn Sie **Text aus Bild** auf Spanisch oder Französisch erkennen müssen, ändern Sie einfach die Eigenschaft `Language`:

```csharp
ocrEngine.Language = OcrLanguage.Spanish; // or OcrLanguage.French
```

Aspose lädt automatisch die passenden Sprachressourcen herunter.

### 5. Ausgabe speichern  
Oft möchten Sie **TIFF zu Text** konvertieren und das Ergebnis in einer `.txt`‑Datei speichern:

```csharp
System.IO.File.WriteAllText("output.txt", ocrResult.Text);
```

Sie können die Ausgabe auch pro Seite mit `String.Split(Environment.NewLine)` aufteilen und jede Teilmenge in eine separate Datei schreiben.

---

## Pro‑Tipps & Fallstricke

- **AutomaticResourceDownload** funktioniert beim ersten Ausführen der Anwendung; nachfolgende Läufe arbeiten offline.  
- Wenn Sie fehlerhafte Zeichen sehen, überprüfen Sie die Einstellung `Language`; nicht passende Sprachpakete führen zu Fehlinterpretationen.  
- Für PDFs, die in TIFFs gerastert wurden, sollten Sie `ocrEngine.Dpi` (Standard ist 300) erhöhen, um die Genauigkeit zu verbessern.  
- Verpacken Sie `Image.FromFile` immer in einen `using`‑Block; sonst sperren Sie die Datei und können sie später nicht mehr löschen oder verschieben.

---

## Häufig gestellte Fragen

**Q: Funktioniert das auch mit einseitigen TIFFs?**  
A: Absolut. Die Engine behandelt ein ein‑Frame‑TIFF genauso; Sie erhalten einfach eine Zeile Text.

**Q: Kann ich PNG‑ oder JPEG‑Dateien auf dieselbe Weise verarbeiten?**  
A: Ja – ändern Sie einfach die Dateierweiterung. Die Methode `Recognize` akzeptiert jedes `System.Drawing.Image`‑Format.

**Q: Was, wenn ich das OCR‑Ergebnis als PDF statt als Klartext benötige?**  
A: Setzen Sie `OutputFormat = OcrOutputFormat.Pdf` und `ocrResult` enthält ein PDF‑Byte‑Array, das Sie auf die Festplatte schreiben können.

---

## Fazit

Sie haben nun eine vollständige End‑zu‑End‑Lösung für **wie man OCR** auf mehrseitigen TIFF‑Dateien mit Aspose OCR in C# besitzt. Durch das Konfigurieren der Engine, das Laden des Bildes und das Aufrufen von `Recognize` können Sie **Text aus TIFF** **extrahieren**, **TIFF zu Text** **konvertieren** und **Text aus Bild** **erkennen** – alles mit nur wenigen Codezeilen. Passen Sie Sprache, Ausgabeformat oder die Frame‑für‑Frame‑Verarbeitung gern an Ihre eigenen Batch‑Verarbeitungsanforderungen an.

Bereit für den nächsten Schritt? Kombinieren Sie diesen Ansatz mit einem Ordner‑Watcher‑Dienst, um automatisch **OCR auf Bild**‑Dateien auszuführen, sobald sie in einem Drop‑Ordner landen, oder integrieren Sie die Ausgabe in einen Suchindex für sofortige Volltextsuche. Die Möglichkeiten sind endlos, und der Code, den Sie gerade gesehen haben, bildet ein solides Fundament.

Wenn Sie auf Probleme stoßen, hinterlassen Sie einen Kommentar unten oder schreiben Sie mir auf GitHub. Viel Spaß beim Coden und beim Umwandeln dieser hartnäckigen TIFFs in durchsuchbaren Text!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}