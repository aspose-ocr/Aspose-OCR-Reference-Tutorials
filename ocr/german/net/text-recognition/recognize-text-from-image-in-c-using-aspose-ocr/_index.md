---
category: general
date: 2026-05-31
description: Erfahren Sie, wie Sie Text aus Bildern in C# mit Aspose OCR erkennen,
  einschließlich der Extraktion von Text aus Tiff‑Dateien und dem effizienten Laden
  von Bildern für OCR.
draft: false
keywords:
- recognize text from image
- extract text from tiff
- load image for OCR
- Aspose OCR C#
- GPU accelerated OCR
language: de
og_description: Schritt-für-Schritt-Anleitung zur Texterkennung aus Bildern mit Aspose
  OCR, einschließlich der Extraktion aus TIFF-Dateien und dem korrekten Laden von
  Bildern für OCR.
og_title: Text aus Bild in C# mit Aspose OCR erkennen
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to recognize text from image in C# with Aspose OCR, including
    how to extract text from tiff files and load image for OCR efficiently.
  headline: recognize text from image in C# using Aspose OCR
  type: TechArticle
- questions:
  - answer: Reduce its resolution before feeding it to the engine, or increase `GpuMemoryLimit`
      if you have enough VRAM.
    question: What if the image is huge (over 10 MB)?
  - answer: Absolutely. Just reuse the same `OcrEngine` instance and assign a new
      `ImageStream` each iteration.
    question: Can I process multiple images in a loop?
  - answer: '`OcrEngine` implements `IDisposable`. Wrap it in a `using` block for
      clean resource management, especially when working with GPU resources.'
    question: Do I need to dispose of anything?
  - answer: Set `engine.Language = OcrLanguage.Spanish` (or any supported language)
      before calling `Recognize()`.
    question: What about languages other than English?
  type: FAQPage
tags:
- OCR
- C#
- Aspose
title: Text aus Bild in C# mit Aspose OCR erkennen
url: /de/net/text-recognition/recognize-text-from-image-in-c-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Text aus Bild in C# mit Aspose OCR erkennen

Haben Sie jemals **Text aus Bild** erkennen müssen, wussten aber nicht, wo Sie in C# anfangen sollen? Sie sind nicht allein – viele Entwickler stoßen an diese Grenze, wenn sie mit gescannten Dokumenten oder mehrseitigen TIFFs arbeiten. In diesem Leitfaden führen wir Sie durch ein vollständiges, sofort ausführbares Beispiel, das **Text aus Bild** mithilfe der Aspose OCR-Bibliothek erkennt, und wir zeigen Ihnen auch, wie Sie **Text aus TIFF extrahieren** und die beste Methode, **Bild für OCR zu laden**, ohne sich die Haare zu raufen.

Wir behandeln alles, von der Installation des NuGet-Pakets bis zur Handhabung von GPU-Beschleunigung und dem Rückgriff auf die CPU, wenn nötig. Am Ende dieses Tutorials haben Sie eine Konsolenanwendung, die den erkannten Text und die Verarbeitungszeit ausgibt – keine fehlenden Teile, keine vagen Verweise.

## Was Sie bauen werden

- Eine einfache .NET-Konsolenanwendung, die ein Bild lädt (einschließlich mehrseitigem TIFF)  
- Eine OCR-Engine, die für GPU‑Nutzung konfiguriert ist, mit elegantem CPU‑Fallback  
- Extraktion von Klartext aus dem Bild, ausgegeben in der Konsole  
- Zeitinformationen, damit Sie die Leistungsunterschiede zwischen GPU und CPU sehen können  

**Voraussetzungen**

- .NET 6 SDK oder neuer (der Code funktioniert mit .NET Core und .NET Framework)  
- Grundlegende Kenntnisse in C# und der Befehlszeile  
- Internetzugang, um das Aspose.OCR NuGet-Paket zu beziehen  

Wenn Sie das haben, lassen Sie uns eintauchen.

![C#-Code zum Erkennen von Text aus Bild mit Aspose OCR](image.png "C#-Code zum Erkennen von Text aus Bild mit Aspose OCR")

## Schritt 1 – Text aus Bild erkennen: OCR-Engine einrichten

Zuerst benötigen wir eine `OcrEngine`-Instanz. Aspose OCR lässt Sie das Verarbeitungsgerät wählen – GPU für Geschwindigkeit, CPU als Sicherheitsnetz. Die Engine akzeptiert außerdem einen Hinweis auf das Speicher‑Limit, was auf gemeinsam genutzten Rechnern praktisch sein kann.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // Create the OCR engine and request GPU acceleration.
        // If no compatible GPU is found, Aspose silently falls back to CPU.
        OcrEngine engine = new OcrEngine
        {
            Device = OcrDevice.Gpu,      // Try GPU first
            GpuMemoryLimit = 1024        // Optional: cap GPU memory usage (MB)
        };
```

**Warum das wichtig ist:**  
Die Wahl von `OcrDevice.Gpu` kann Sekunden von der Erkennungszeit großer Bilder abziehen, besonders bei mehrseitigen TIFFs. `GpuMemoryLimit` verhindert, dass Ihre Anwendung den gesamten GPU‑Speicher auf einem gemeinsam genutzten Arbeitsplatz belegt.

## Schritt 2 – Bild für OCR laden (einschließlich TIFF‑Unterstützung)

Jetzt übergeben wir der Engine ein Bild. Asposes `ImageStream.FromFile` akzeptiert **jedes** Format, das die Bibliothek unterstützt – TIFF, PNG, JPEG, was Sie wollen. Dieser Schritt erfüllt direkt die Anforderung **Bild für OCR zu laden**.

```csharp
        // Load the image you want to process.
        // Replace the path with the actual location of your TIFF or other image.
        engine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/sample_multi_page.tif");
```

**Profi‑Tipp:** Wenn Sie mit einem mehrseitigen TIFF arbeiten, behandelt Aspose jede Seite automatisch als separates Frame, und die Engine verarbeitet sie nacheinander. Kein zusätzlicher Code nötig.

## Schritt 3 – Erkennung ausführen und **Text aus TIFF extrahieren**

Mit der vorbereiteten Engine und dem geladenen Bild starten wir die OCR‑Operation. Die Methode `Recognize` gibt ein `OcrResult` zurück, das den Klartext, Konfidenzwerte und Zeitdetails enthält.

```csharp
        // Perform the OCR operation.
        OcrResult result = engine.Recognize();
```

**Umgang mit Randfällen:**  
Wenn die GPU nicht verfügbar ist, funktioniert `engine.Recognize()` weiterhin, weil die Engine stillschweigend auf die CPU umschaltet. Sie können `engine.Device` nach der Erkennung prüfen, falls Sie protokollieren möchten, welches Gerät tatsächlich verwendet wurde.

## Schritt 4 – Erkannten Klartext abrufen

Das Extrahieren des Textes ist einfach – lesen Sie einfach die `Text`‑Eigenschaft. Hier **extrahieren wir schließlich Text aus TIFF** (oder jedem anderen Bild) und präsentieren ihn dem Benutzer.

```csharp
        // Output the plain text that was extracted.
        Console.WriteLine($"Text:\n{result.Text}");
```

Sie sehen die rohen Zeichen, Zeilenumbrüche werden wie im Quellbild beibehalten. Für strukturiertere Ausgaben (wie JSON oder CSV) können Sie `result.Regions` und `result.Lines` untersuchen, aber der Klartext reicht meist für schnelle Skripte aus.

## Schritt 5 – Verarbeitungszeit messen und GPU‑Fallback handhaben

Leistung ist wichtig, besonders wenn Sie Dutzende von Seiten verarbeiten. Die Eigenschaft `ProcessingTime` gibt genau an, wie lange die OCR gedauert hat, unabhängig davon, ob sie auf GPU oder CPU lief.

```csharp
        // Show how long the recognition took.
        Console.WriteLine($"Time elapsed: {result.ProcessingTime.TotalSeconds}s");
    }
}
```

**Warum das wichtig ist:**  
Wenn Sie feststellen, dass die Zeit stark ansteigt, sollten Sie `GpuMemoryLimit` anpassen oder explizit zur CPU wechseln (`Device = OcrDevice.Cpu`). Umgekehrt bedeutet ein Ergebnis unter einer Sekunde bei einem großen TIFF, dass Ihre GPU‑Beschleunigung ihre Arbeit tut.

## Vollständiges, sofort ausführbares Beispiel

Kopieren Sie den untenstehenden Code in ein neues Konsolenprojekt (`dotnet new console -n OcrDemo`) und führen Sie `dotnet add package Aspose.OCR` aus. Ersetzen Sie anschließend `YOUR_DIRECTORY/sample_multi_page.tif` durch den Pfad zu Ihrem Bild.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // Step 1: Initialize the OCR engine with GPU preference.
        OcrEngine engine = new OcrEngine
        {
            Device = OcrDevice.Gpu,
            GpuMemoryLimit = 1024
        };

        // Step 2: Load image for OCR (supports TIFF, PNG, JPEG, etc.).
        engine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/sample_multi_page.tif");

        // Step 3: Run recognition – this will also **extract text from tiff**.
        OcrResult result = engine.Recognize();

        // Step 4: Retrieve and display the recognized plain text.
        Console.WriteLine($"Text:\n{result.Text}");

        // Step 5: Display how long the operation took.
        Console.WriteLine($"Time elapsed: {result.ProcessingTime.TotalSeconds}s");
    }
}
```

**Erwartete Ausgabe (gekürzt zur Übersicht):**

```
Text:
Invoice #12345
Date: 2026-05-01
Total: $1,250.00
...
Time elapsed: 1.42s
```

Wenn Ihr Rechner keine geeignete GPU hat, kann die verstrichene Zeit ein paar Sekunden länger sein, aber der Text wird weiterhin korrekt extrahiert.

## Häufige Fragen & Stolperfallen

- **Was, wenn das Bild riesig ist (über 10 MB)?**  
  Reduzieren Sie die Auflösung, bevor Sie es an die Engine übergeben, oder erhöhen Sie `GpuMemoryLimit`, wenn Sie genug VRAM haben.  
- **Kann ich mehrere Bilder in einer Schleife verarbeiten?**  
  Absolut. Verwenden Sie einfach dieselbe `OcrEngine`‑Instanz erneut und weisen Sie jeder Iteration einen neuen `ImageStream` zu.  
- **Muss ich etwas freigeben?**  
  `OcrEngine` implementiert `IDisposable`. Packen Sie sie in einen `using`‑Block für eine saubere Ressourcenverwaltung, besonders beim Arbeiten mit GPU‑Ressourcen.  

```csharp
using (OcrEngine engine = new OcrEngine { Device = OcrDevice.Gpu })
{
    // ... same steps as before
}
```

- **Wie sieht es mit anderen Sprachen als Englisch aus?**  
  Setzen Sie `engine.Language = OcrLanguage.Spanish` (oder eine andere unterstützte Sprache) bevor Sie `Recognize()` aufrufen.  

## Fazit

Sie haben jetzt eine vollständige End‑zu‑End‑Lösung, die **Text aus Bild** in C# mit Aspose OCR erkennt. Das Tutorial behandelte, wie man **Bild für OCR lädt**, wie man **Text aus TIFF extrahiert** und wie man die Leistung misst, während man elegant den GPU‑Fallback handhabt. 

Von hier aus könnten Sie:

- Experimentieren Sie mit verschiedenen Bildformaten (BMP, PDF), um zu sehen, wie Aspose sie verarbeitet.  
- Tauchen Sie in `result.Regions` ein, um Begrenzungs‑Box‑Daten zu erhalten, falls Sie layout‑aware arbeiten müssen  

## Was sollten Sie als Nächstes lernen?

- [Wie man Aspose verwendet, um ein Bild aus einem Stream in der OCR-Bilderkennung zu erkennen](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [Text aus Bild extrahieren – OCR-Optimierung mit Aspose.OCR für .NET](/ocr/english/net/ocr-optimization/)
- [Text aus Bild extrahieren – Zeile mit Aspose.OCR erkennen](/ocr/english/net/image-and-drawing-recognition/recognize-line/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}