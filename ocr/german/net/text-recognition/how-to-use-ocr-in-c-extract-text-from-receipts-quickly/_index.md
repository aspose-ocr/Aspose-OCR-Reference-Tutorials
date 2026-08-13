---
category: general
date: 2026-03-05
description: Wie man OCR in C# verwendet, um Text aus Quittungsbildern zu extrahieren.
  Lernen Sie, wie man ein Bild für OCR lädt und ein Quittungsbild in Minuten erkennt.
draft: false
keywords:
- how to use OCR
- extract text from receipt
- load image for OCR
- recognize receipt image
language: de
og_description: Wie man OCR in C# verwendet, um Text aus Quittungen zu extrahieren.
  Folgen Sie dieser Schritt‑für‑Schritt‑Anleitung, um ein Bild für OCR zu laden und
  das Quittungsbild effizient zu erkennen.
og_title: Wie man OCR in C# verwendet – Schnelle Beleg‑Text‑Extraktion
tags:
- OCR
- C#
- Aspose
- Receipt Processing
title: Wie man OCR in C# verwendet – Text schnell aus Quittungen extrahieren
url: /de/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-receipts-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man OCR in C# verwendet – Text schnell aus Quittungen extrahieren

Haben Sie sich jemals gefragt, **wie man OCR** verwendet, um Daten direkt aus einem Foto einer Supermarktquittung zu extrahieren? Sie sind nicht der Einzige. In vielen Kleinunternehmens‑Apps ist der Engpass, ein verschwommenes PNG in strukturierten Text zu verwandeln, den Sie tatsächlich nutzen können.  

Die gute Nachricht? Mit ein paar Zeilen C# und Aspose.OCR können Sie **load image for OCR**, die Engine ausführen und **recognize receipt image** in weniger als einer Minute. Im Folgenden sehen Sie ein vollständiges, sofort ausführbares Beispiel sowie Tipps für die kniffligen Punkte, die die meisten Tutorials überspringen.

## Was dieser Leitfaden abdeckt

* Installation des Aspose.OCR NuGet-Pakets.  
* Einrichten der OCR-Engine – das Kernstück von **how to use OCR** korrekt.  
* Laden einer Quittungsdatei (das ist der **load image for OCR** Schritt).  
* Ausführen des Erkennungsprozesses und Extrahieren von JSON- und XML‑Layoutdaten.  
* Umgang mit häufigen Fallstricken wie fehlenden Lizenzen oder nicht unterstützten Bildformaten.  

Am Ende haben Sie ein eigenständiges Programm, das den Text aus jeder Quittung extrahiert, die Sie in einen Ordner legen. Keine externen Dienste, keine versteckte Magie.

## Voraussetzungen

* .NET 6 SDK oder neuer (der Code kompiliert auch mit .NET Core).  
* Eine gültige Aspose.OCR-Lizenzdatei (`Aspose.OCR.lic`). Sie können eine kostenlose Testversion von Aspose erhalten, falls Sie noch keine haben.  
* Ein Beispiel‑Quittungsbild – `receipt.png` funktioniert, aber jedes gängige Rasterformat ist geeignet.  

Wenn Sie das bereits haben, großartig – lassen Sie uns loslegen.

![how to use OCR example](https://example.com/ocr-receipt.png "how to use OCR example")

## Schritt 1: Aspose.OCR installieren und ein neues Projekt erstellen

Zuerst das Wichtigste: Sie benötigen die Bibliothek, die die eigentliche Schwerarbeit übernimmt. Öffnen Sie ein Terminal in Ihrem Projektordner und führen Sie aus:

```bash
dotnet new console -n ReceiptOcrDemo
cd ReceiptOcrDemo
dotnet add package Aspose.OCR
```

Dieser Befehl erzeugt eine Konsolenanwendung und bindet das neueste Aspose.OCR‑Paket ein. Nach meiner Erfahrung macht ein kurzer Projektname die generierten Pfade leichter lesbar, besonders wenn Sie mehrere Demo‑Apps jonglieren.

## Schritt 2: Initialisieren der OCR-Engine – das Herzstück von **how to use OCR**

Jetzt schreiben wir den Code, der die Frage “**how to use OCR** in C#” beantwortet. Öffnen Sie `Program.cs` und ersetzen Sie dessen Inhalt durch das untenstehende Snippet. Achten Sie auf die Kommentare – sie erklären das *Warum* hinter jeder Zeile, nicht nur das *Was*.

```csharp
using System;
using System.IO;
using Aspose.OCR;          // Aspose OCR namespace
using Aspose.OCR.Image;   // For loading images

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Create and configure the OCR engine.
        // -------------------------------------------------
        var ocrEngine = new OcrEngine();

        // Why set a license? Without it the engine runs in evaluation mode,
        // which adds a watermark to the output and limits batch size.
        ocrEngine.SetLicense("Aspose.OCR.lic");

        // -------------------------------------------------
        // 2️⃣ Load the receipt image – this is the **load image for OCR** step.
        // -------------------------------------------------
        // Change the path to point at your own receipt file.
        string imagePath = Path.Combine(
            Environment.CurrentDirectory, "receipt.png");

        // The ImageStream class abstracts file I/O and supports many formats.
        ocrEngine.Image = ImageStream.FromFile(imagePath);

        // -------------------------------------------------
        // 3️⃣ Run the recognition process – this is where we **recognize receipt image**.
        // -------------------------------------------------
        var ocrResult = ocrEngine.Recognize();

        // -------------------------------------------------
        // 4️⃣ Export the layout information as JSON.
        // -------------------------------------------------
        string jsonResult = ocrResult.ToJson();
        File.WriteAllText("receipt.json", jsonResult);
        Console.WriteLine("✅ JSON saved to receipt.json");

        // -------------------------------------------------
        // 5️⃣ Export the same layout information as XML.
        // -------------------------------------------------
        string xmlResult = ocrResult.ToXml();
        File.WriteAllText("receipt.xml", xmlResult);
        Console.WriteLine("✅ XML saved to receipt.xml");

        // -------------------------------------------------
        // 6️⃣ Quick preview – print the plain text to console.
        // -------------------------------------------------
        Console.WriteLine("\n--- Extracted Text ---");
        Console.WriteLine(ocrResult.Text);
    }
}
```

### Warum das funktioniert

* **`OcrEngine`** ist der Einstiegspunkt; er enthält alle Konfigurationen, die Sie später anpassen können (Sprache, DPI usw.).  
* **`SetLicense`** entfernt das Evaluations‑Wasserzeichen – ein entscheidender Schritt, wenn Sie den Code veröffentlichen wollen.  
* **`ImageStream.FromFile`** erledigt die **load image for OCR** Arbeit und unterstützt PNG, JPEG, BMP, TIFF und mehr.  
* **`Recognize()`** ist die Methode, die tatsächlich **recognize receipt image** ausführt. Im Hintergrund führt sie Binarisierung, Segmentierung und Zeichenklassifizierung durch.  
* Der Export nach JSON und XML liefert sowohl einen menschenlesbaren Dump als auch eine maschinenfreundliche Struktur, die Sie in nachgelagerte Parser einspeisen können.

## Schritt 3: Demo ausführen und Ausgabe überprüfen

Kompilieren und ausführen:

```bash
dotnet run
```

Wenn alles korrekt verkabelt ist, sehen Sie etwa Folgendes:

```
✅ JSON saved to receipt.json
✅ XML saved to receipt.xml

--- Extracted Text ---
Walmart Supercenter
Date: 03/04/2026
Item    Qty   Price
Milk    2     2.58
Bread   1     1.99
Total   4.57
```

Die Konsole gibt den Klartext aus, während `receipt.json` und `receipt.xml` detaillierte Layout‑Informationen (Koordinaten, Vertrauenswerte usw.) enthalten. Diese Dateien sind praktisch, wenn Sie später jede Zeile einem Datenbankfeld zuordnen müssen.

## Sonderfälle & Profi‑Tipps

### 1️⃣ Fehlende oder ungültige Lizenz

Falls `SetLicense` fehlschlägt, wechselt die Engine in den Testmodus und Sie erhalten ein Wasserzeichen in der Ausgabe. Umgeben Sie den Aufruf mit einem try/catch und protokollieren Sie eine freundliche Meldung:

```csharp
try { ocrEngine.SetLicense("Aspose.OCR.lic"); }
catch (Exception ex)
{
    Console.WriteLine("⚠️ License not found – running in trial mode.");
    Console.WriteLine(ex.Message);
}
```

### 2️⃣ Nicht unterstützte Bildformate

Aspose.OCR unterstützt die meisten Rasterformate, aber wenn Sie ein PDF oder ein mehrseitiges TIFF einspeisen, müssen Sie die gewünschte Seite zuerst in ein Bild konvertieren. Die Bibliothek `Aspose.PDF` kann diese Konvertierung übernehmen.

### 3️⃣ Große Quittungen & Leistung

Die Verarbeitung eines 10 MB‑Bildes kann langsam sein. Reduzieren Sie die Auflösung, bevor Sie es an die Engine übergeben:

```csharp
ocrEngine.Image = ImageStream.FromFile(imagePath).Resize(1024, 0);
```

Die Methode `Resize` behält das Seitenverhältnis bei (`0` für die Höhe) und reduziert die Dateigröße drastisch, ohne die OCR‑Genauigkeit für typische Quittungen zu beeinträchtigen.

### 4️⃣ Sprach‑ und Schriftart‑Probleme

Quittungen können Sonderzeichen enthalten (€, ¥ usw.). Setzen Sie die Sprache explizit, wenn Sie das Gebietsschema kennen:

```csharp
ocrEngine.Language = Language.English; // or Language.Spanish, etc.
```

Für mehrsprachige Quittungen können Sie den mehrsprachigen Modus aktivieren:

```csharp
ocrEngine.Language = Language.English | Language.French;
```

### 5️⃣ Extrahieren strukturierter Daten

Der Rohtext ist nützlich, aber die meisten Apps benötigen strukturierte Felder (Datum, Gesamtbetrag, Artikel). Das JSON‑Layout enthält `BoundingBox`‑Koordinaten für jedes Wort. Sie können es so nachverarbeiten:

```csharp
var layout = Newtonsoft.Json.Linq.JObject.Parse(jsonResult);
foreach (var word in layout["Words"])
{
    string text = (string)word["Text"];
    // Simple heuristics: look for "$" or "Total"
}
```

Dieses Snippet veranschaulicht die Idee; in der Produktion würden Sie wahrscheinlich einen regulären Ausdruck oder eine kleine Regel‑Engine verwenden.

## Häufig gestellte Fragen

**Q: Kann ich das unter Linux ausführen?**  
A: Absolut. Aspose.OCR ist plattformübergreifend; installieren Sie einfach die .NET‑Runtime auf Ihrem Linux‑System und derselbe Code funktioniert.

**Q: Was ist, wenn ich Dutzende von Quittungen pro Minute verarbeiten muss?**  
A: Starten Sie eine `Parallel.ForEach`‑Schleife und verwenden Sie eine einzelne `OcrEngine`‑Instanz wieder – sie ist für Lese‑Operationen thread‑sicher. Denken Sie daran, Lizenz‑Parallelitätsgrenzen zu berücksichtigen.

**Q: Funktioniert das mit mobilen Fotos, die schräg aufgenommen wurden?**  
A: Die Engine enthält eine grundlegende Entzerrung, aber bei stark verzerrten Bildern sollten Sie sie zunächst mit einer Bildverarbeitungsbibliothek (z. B. OpenCV) vorverarbeiten, um die Quittung zu begradigen.

## Vollständiges funktionierendes Beispiel (Copy‑Paste)

Unten finden Sie das *gesamte* Programm, das Sie in `Program.cs` einfügen können. Keine weiteren Dateien sind erforderlich, außer der Lizenz und einem Quittungsbild.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Image;

class Program
{
    static void Main()
    {
        // Create and configure the OCR engine
        var ocrEngine = new OcrEngine();
        try
        {
            ocrEngine.SetLicense("Aspose.OCR.lic");
        }
        catch (Exception)
        {
            Console.WriteLine("⚠️ Running in trial mode – license not found.");
        }

        // Load the image to be processed (load image for OCR)
        string imagePath = Path.Combine(Environment.CurrentDirectory, "

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}