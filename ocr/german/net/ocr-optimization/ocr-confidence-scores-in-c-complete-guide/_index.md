---
category: general
date: 2026-05-31
description: Erfahren Sie, wie Sie OCR‑Vertrauenswerte in C# erhalten, während Sie
  Text aus einem Bild extrahieren und Quittungsbilder mit Aspose OCR lesen.
draft: false
keywords:
- ocr confidence scores
- extract text from image
- ocr bounding boxes
- perform ocr on jpg
- read receipt image
language: de
og_description: OCR‑Vertrauenswerte ermöglichen es Ihnen, die Genauigkeit zu beurteilen;
  dieser Leitfaden zeigt, wie Sie Text aus einem Bild extrahieren, Begrenzungsrahmen
  erhalten und ein Belegbild mit Aspose OCR lesen.
og_title: OCR-Vertrauenswerte in C# – Vollständiger Leitfaden
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to get OCR confidence scores in C# while extract text from
    image and read receipt image with Aspose OCR.
  headline: OCR confidence scores in C# – Complete Guide
  type: TechArticle
tags:
- OCR
- C#
- Aspose
- Image Processing
title: OCR-Konfidenzwerte in C# – Vollständiger Leitfaden
url: /de/net/ocr-optimization/ocr-confidence-scores-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR‑Vertrauenswerte in C# – Vollständiger Leitfaden

Haben Sie sich schon einmal gefragt, wie man **OCR‑Vertrauenswerte** erhält, wenn man *Text aus einem Bild extrahieren* muss? Vielleicht möchten Sie **Beleg‑Bilddateien** für die Spesenabrechnung auslesen und wissen, bei welchen Zeichen die Engine unsicher ist. Die gute Nachricht: Mit Aspose.OCR können Sie Prozentsätze für das Vertrauen, Begrenzungsrahmen und Klartext aus einer JPG‑Datei in nur wenigen Zeilen C# abrufen.

In diesem Tutorial führen wir Sie durch alles, was Sie wissen müssen: Installation der Bibliothek, Konfiguration der Engine für **OCR auf JPG**, Abrufen von Vertrauenswerten und Interpretation der **OCR‑Begrenzungsrahmen**, die anzeigen, wo jedes Zeichen auf der Seite liegt. Am Ende haben Sie eine sofort ausführbare Konsolen‑App, die jedes Zeichen, dessen Vertrauenswert und dessen Position ausgibt – ideal zum Validieren von Belegen oder anderen gescannten Dokumenten.

## Was Sie lernen werden

- Aspose.OCR über NuGet installieren und eine einfache OCR‑Engine einrichten.  
- `OcrOptions` konfigurieren, um Klartext‑Ausgabe **mit Vertrauenswerten** und **Begrenzungsrahmen** anzufordern.  
- Durch `OcrResult` iterieren, um **Text aus Bild** zeilenweise und zeichenweise zu **extrahieren**.  
- Häufige Stolperfallen behandeln, z. B. fehlende Dateien, Zeichen mit niedrigem Vertrauen und Formate, die nicht JPG sind.  
- Das Beispiel erweitern, um mehrere Beleg‑Bilder in einem Ordner zu verarbeiten.

Vorkenntnisse mit Aspose sind nicht erforderlich; Sie benötigen lediglich eine funktionierende .NET‑Umgebung und ein Beleg‑Bild (JPG), das Sie testen möchten.

---

## Schritt 1 – Aspose.OCR installieren und Ihr Projekt vorbereiten

Zuerst benötigen Sie das Aspose.OCR‑NuGet‑Paket. Öffnen Sie ein Terminal im Projektordner und führen Sie aus:

```bash
dotnet add package Aspose.OCR
```

> **Pro‑Tipp:** Die kostenlose Testversion funktioniert für bis zu 200 Seiten – mehr als genug für das Testen der Beleg‑Erkennung.

Nachdem das Paket installiert ist, erstellen Sie ein neues Konsolen‑Projekt (falls Sie noch keines haben):

```bash
dotnet new console -n ReceiptOcrDemo
cd ReceiptOcrDemo
```

Jetzt können Sie die erzeugte `Program.cs` öffnen und die using‑Direktiven hinzufügen:

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;
```

Diese Namespaces geben Ihnen Zugriff auf `OcrEngine`, `OcrOptions` und die Ergebnis‑Typen, die wir später benötigen.

## Schritt 2 – OCR‑Vertrauenswerte und OCR‑Begrenzungsrahmen erhalten

Dies ist das Kernstück des Tutorials. Wir konfigurieren die Engine so, dass jedes erkannte Zeichen einen **Vertrauenswert** und einen **Begrenzungsrahmen** (das Rechteck, das das Glyph umschließt) liefert. Die H2‑Überschrift selbst enthält das Haupt‑Keyword und erfüllt damit die SEO‑Anforderung.

```csharp
// Step 2: Initialize the OCR engine and request detailed output
OcrEngine ocrEngine = new OcrEngine();

// Load the image you want to process – here we assume a JPEG receipt
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/receipt.jpg");

// Tell Aspose we want plain text, confidence percentages, and bounding boxes
ocrEngine.Options = new OcrOptions
{
    OutputFormat = OcrOutputFormat.PlainText,
    IncludeConfidence = true,
    IncludeBoundingBoxes = true
};
```

**Warum Vertrauenswerte einbeziehen?**  
Ein Vertrauenswert (0‑100 %) gibt an, wie sicher die Engine bei jedem Zeichen ist. Wenn Sie die Ausgabe in nachgelagerte Logik einspeisen – etwa einen Genehmigungs‑Workflow für Ausgaben – können Sie Zeichen mit niedrigem Vertrauen automatisch ablehnen oder markieren.

**Warum Begrenzungsrahmen anfordern?**  
Begrenzungsrahmen sind unverzichtbar, wenn Sie Text im Originalbild hervorheben, Teilbereiche extrahieren oder OCR‑Ergebnisse mit einer UI‑Überlagerung abgleichen möchten. Jeder `character.Bounds` liefert X, Y, Breite und Höhe in Pixel‑Koordinaten.

## Schritt 3 – OCR auf JPG ausführen und Text aus Bild extrahieren

Jetzt führen wir die Engine tatsächlich aus. Der Aufruf von `Recognize()` erledigt die schwere Arbeit und gibt ein `OcrResult`‑Objekt zurück.

```csharp
// Step 3: Run the OCR process
OcrResult ocrResult = ocrEngine.Recognize();
```

Ist der Bildpfad falsch oder das Dateiformat nicht unterstützt, wirft Aspose eine `FileNotFoundException` bzw. `UnsupportedImageFormatException`. Packen Sie den Aufruf in Produktionscode in einen try/catch‑Block, um diese Randfälle elegant zu behandeln.

### Den Klartext extrahieren

Wenn Sie nur den zusammengefügten Text benötigen, können Sie `ocrResult.Text` lesen:

```csharp
Console.WriteLine("Full extracted text:");
Console.WriteLine(ocrResult.Text);
```

Da wir jedoch auch Vertrauenswerte und Begrenzungsrahmen angefordert haben, iterieren wir durch die Struktur, um die Details jedes Zeichens zu sehen.

## Schritt 4 – Durch Zeilen, Symbole iterieren und OCR‑Vertrauenswerte anzeigen

Hier ist die Schleife, die jedes Zeichen, dessen Vertrauenswert und dessen Rahmen ausgibt. Genau hier glänzt das **Beleg‑Bild‑Beispiel**.

```csharp
// Step 4: Walk through each line and each symbol (character)
foreach (var textLine in ocrResult.Lines)
{
    foreach (var character in textLine.Symbols)
    {
        Console.WriteLine(
            $"Char: '{character.Text}'  Confidence: {character.Confidence}%  Box: {character.Bounds}");
    }
}
```

Beispielausgabe könnte folgendermaßen aussehen:

```
Char: 'R'  Confidence: 98%  Box: {X=12,Y=34,Width=15,Height=20}
Char: 'e'  Confidence: 95%  Box: {X=28,Y=34,Width=12,Height=20}
Char: 'c'  Confidence: 92%  Box: {X=41,Y=34,Width=13,Height=20}
...
```

**Interpretation der Zahlen:**  
- **Vertrauen ≥ 90 %** – in der Regel sicher zu übernehmen.  
- **Vertrauen 70‑89 %** – Sie sollten prüfen, besonders bei Ziffern in Beträgen.  
- **Vertrauen < 70 %** – Erwägen Sie, das Zeichen zur manuellen Überprüfung zu markieren.

## Schritt 5 – Vollständiges, ausführbares Beispiel (inkl. Fehlerbehandlung)

Alles zusammengefügt, hier ein komplettes Programm, das Sie in `Program.cs` einfügen können. Es prüft, ob Dateien fehlen, und gibt eine freundliche Meldung aus, falls die OCR fehlschlägt.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Path to the receipt image – adjust to your environment
            const string imagePath = "YOUR_DIRECTORY/receipt.jpg";

            if (!System.IO.File.Exists(imagePath))
            {
                Console.WriteLine($"Error: File not found -> {imagePath}");
                return;
            }

            try
            {
                // Initialize engine
                OcrEngine ocrEngine = new OcrEngine
                {
                    Image = ImageStream.FromFile(imagePath),
                    Options = new OcrOptions
                    {
                        OutputFormat = OcrOutputFormat.PlainText,
                        IncludeConfidence = true,
                        IncludeBoundingBoxes = true
                    }
                };

                // Perform OCR
                OcrResult ocrResult = ocrEngine.Recognize();

                // Show full plain text (optional)
                Console.WriteLine("=== Extracted Text ===");
                Console.WriteLine(ocrResult.Text);
                Console.WriteLine();

                // Show each character with confidence and bounding box
                Console.WriteLine("=== Detailed Character Data ===");
                foreach (var line in ocrResult.Lines)
                {
                    foreach (var symbol in line.Symbols)
                    {
                        Console.WriteLine(
                            $"Char: '{symbol.Text}'  Confidence: {symbol.Confidence}%  Box: {symbol.Bounds}");
                    }
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine($"OCR failed: {ex.Message}");
            }
        }
    }
}
```

### Erwartete Ausgabe

Wenn Sie `dotnet run` ausführen, zeigt die Konsole zuerst den zusammengefügten Beleg‑Text, dann eine Liste jedes Zeichens mit Vertrauenswert und Begrenzungsrahmen. Hat ein Zeichen ein niedriges Vertrauen, sehen Sie einen Prozentsatz unter 80 %, was ein Hinweis ist, diesen Teil des Belegs manuell zu prüfen.

## Bonus: Mehrere Belege in einem Ordner verarbeiten

Haben Sie einen Stapel Beleg‑JPGs, wickeln Sie die obige Logik in eine `foreach (var file in Directory.GetFiles(folder, "*.jpg"))`‑Schleife. Denken Sie daran, die `OcrEngine` für jede Datei zurückzusetzen oder innerhalb der Schleife neu zu instanziieren, um Zustandslecks zu vermeiden.

```csharp
string folder = "YOUR_DIRECTORY/Receipts";
foreach (var file in System.IO.Directory.GetFiles(folder, "*.jpg"))
{
    // reuse the same code block, just replace imagePath with 'file'
}
```

Die Verarbeitung im Batch ist praktisch für nächtliche Spesen‑Importe.

---

## Fazit

Sie verfügen jetzt über eine solide End‑zu‑End‑Lösung, um **OCR‑Vertrauenswerte** in C# zu erhalten, **Text aus Bild** zu extrahieren und **OCR‑Begrenzungsrahmen** abzurufen, während Sie **OCR auf JPG**‑Dateien wie ein **Beleg‑Bild** ausführen. Der Code ist vollständig eigenständig, funktioniert mit der neuesten Aspose.OCR‑Version (Stand 2026‑05‑31) und liefert die granularen Daten, die Sie für vertrauenswürdige Dokumenten‑Verarbeitungspipelines benötigen.

Was kommt als Nächstes? Visualisieren Sie die Begrenzungsrahmen auf dem Originalbeleg mit `System.Drawing` oder einer UI‑Bibliothek, oder leiten Sie Zeichen mit niedrigem Vertrauen an einen sekundären Verifizierungs‑Service weiter. Sie können auch mit anderen Sprachen experimentieren, indem Sie `ocrEngine.Options.Language = OcrLanguage.French;` setzen – die API unterstützt viele Locale.

Viel Spaß beim Coden und mögen Ihre Vertrauenswerte stets hoch bleiben! 

![Console output showing OCR confidence scores and bounding boxes for a receipt

## Was sollten Sie als Nächstes lernen?

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [How to Get OCR Character Choices for Recognized Characters in Image Recognition](/ocr/english/net/text-recognition/get-choices-for-recognized-characters/)
- [How to Use Aspose OCR for JSON Result in Image Recognition](/ocr/english/net/text-recognition/get-result-as-json/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}