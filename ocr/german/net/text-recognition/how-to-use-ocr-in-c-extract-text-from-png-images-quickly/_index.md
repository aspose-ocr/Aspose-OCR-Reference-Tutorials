---
category: general
date: 2026-03-29
description: Wie man OCR mit Aspose verwendet, um Text aus PNG‑Dateien zu extrahieren
  und Bilder in Text zu konvertieren. Lernen Sie Schritt für Schritt asynchrones OCR
  in C#.
draft: false
keywords:
- how to use OCR
- extract text from png
- convert images to text
- extract text from images
language: de
og_description: Wie man OCR mit Aspose in C# verwendet, um Text aus PNG‑Dateien zu
  extrahieren. Dieser Leitfaden führt Sie durch asynchrones OCR, Code und Tipps.
og_title: Wie man OCR in C# verwendet – Text aus PNG-Bildern extrahieren
tags:
- OCR
- C#
- Aspose
title: Wie man OCR in C# verwendet – Text schnell aus PNG-Bildern extrahieren
url: /de/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-png-images-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man OCR in C# verwendet – Text schnell aus PNG‑Bildern extrahieren

Haben Sie sich jemals gefragt, **wie man OCR** verwendet, um Text aus ein paar PNG‑Screenshots zu extrahieren? Vielleicht haben Sie gescannte Quittungen, Rechnungen oder UI‑Mock‑Ups und benötigen den Text in einem durchsuchbaren Format. Die gute Nachricht? Mit Aspose.OCR können Sie Bilder in Text umwandeln – und das mit nur wenigen Zeilen asynchronen C#‑Codes.  

In diesem Tutorial zeigen wir Ihnen genau, wie Sie Text aus PNG‑Dateien extrahieren, erklären, warum jeder Schritt wichtig ist, und geben Ihnen ein sofort ausführbares Programm, das den erkannten Text für jede Seite ausgibt. Am Ende können Sie **Text aus Bildern** extrahieren, ohne durch die Dokumentation zu wühlen.

## Was Sie lernen werden

- Installieren und referenzieren Sie das Aspose.OCR‑NuGet‑Paket.  
- Initialisieren Sie die OCR‑Engine und setzen Sie die Sprache (Englisch in diesem Beispiel).  
- Übergeben Sie ein Array von PNG‑Dateien an `RecognizeImagesAsync` für schnelle, nicht blockierende Verarbeitung.  
- Durchlaufen Sie die `OcrResult`‑Objekte und geben Sie die extrahierten Zeichenketten aus.  

Keine externen Dienste, keine komplizierten Callbacks — nur sauberer, async C#‑Code, der auf .NET 6+ funktioniert.

---

## Voraussetzungen

| Anforderung | Grund |
|-------------|-------|
| .NET 6 SDK (oder später) | Moderne Sprachfeatures wie `async Main`. |
| Visual Studio 2022 oder VS Code | IDE zum Kompilieren und Ausführen des Codes. |
| Aspose.OCR NuGet‑Paket (`Aspose.OCR`) | Stellt die im Beispiel verwendete Klasse `OcrEngine` bereit. |
| Einige PNG‑Bilder (`page1.png`, `page2.png`, …) | Eingabedateien für den OCR‑Prozess. |

Wenn Sie bereits ein .NET‑Projekt haben, führen Sie einfach `dotnet add package Aspose.OCR` aus. Andernfalls erstellen Sie eine neue Konsolen‑App mit `dotnet new console -n OcrDemo`.

---

## Schritt 1: Aspose.OCR installieren und das Projekt einrichten

Zuerst fügen Sie die OCR‑Bibliothek zu Ihrem Projekt hinzu:

```bash
dotnet add package Aspose.OCR
```

Warum das wichtig ist: Aspose.OCR bündelt die native OCR‑Engine, Sprachpakete und eine einfache API. Durch die Installation via NuGet stellen Sie Versionskompatibilität und automatische Updates sicher.

---

## Schritt 2: Die OCR‑Engine initialisieren und eine Sprache wählen

Die Engine muss wissen, nach welcher Sprache sie suchen soll. Englisch ist am häufigsten, aber Sie können `Language.Spanish`, `Language.French` usw. austauschen.

```csharp
using Aspose.OCR;

// ...

// Step 2: Create the engine and set the language to English
var ocrEngine = new OcrEngine
{
    Language = Language.English   // Change this if you need a different language
};
```

> **Pro‑Tipp:** Setzen Sie die Sprache immer explizit; das Belassen beim Standard kann die Genauigkeit verringern und die Verarbeitungszeit erhöhen.

---

## Schritt 3: Die Liste der PNG‑Dateien vorbereiten

Sie können eine einzelne Datei oder ein Array übergeben. Ein Array ermöglicht der Engine, sie asynchron stapelweise zu verarbeiten – ideal für ein paar Seiten.

```csharp
// Step 3: Define the image files you want to process
string[] imagePaths = { "page1.png", "page2.png", "page3.png" };
```

Wenn Ihre Bilder in einem Unterordner liegen, hängen Sie einfach den relativen Pfad an (`"images/page1.png"`). Die Engine wirft eine klare `FileNotFoundException`, wenn ein Pfad falsch ist — also prüfen Sie die Dateinamen doppelt.

---

## Schritt 4: Asynchrones OCR für alle Bilder ausführen

Die Methode `RecognizeImagesAsync` gibt ein Array von `OcrResult` zurück. Da sie async ist, bleibt Ihre UI (oder Konsole) responsiv, während das OCR im Hintergrund läuft.

```csharp
// Step 4: Perform async OCR on every image
OcrResult[] ocrResults = await ocrEngine.RecognizeImagesAsync(imagePaths);
```

**Warum async?**  
Wenn Sie OCR in eine Web‑API oder eine Desktop‑App integrieren, wollen Sie nicht, dass der Thread blockiert, während die Engine jedes Pixel scannt. `await` gibt den Thread zurück an den Thread‑Pool und verbessert die Skalierbarkeit.

---

## Schritt 5: Den extrahierten Text für jede Seite anzeigen

Jetzt, wo wir die Ergebnisse haben, iterieren wir darüber und geben den erkannten Text aus. Die Eigenschaft `Text` enthält die reine Textausgabe, bereit für weitere Verarbeitung (z. B. Speicherung in einer Datenbank).

```csharp
// Step 5: Output the recognized text for every page
for (int i = 0; i < ocrResults.Length; i++)
{
    Console.WriteLine($"--- Page {i + 1} ---");
    Console.WriteLine(ocrResults[i].Text);
}
```

### Erwartete Ausgabe

Angenommen, `page1.png` enthält „Invoice #12345“ und `page2.png` enthält „Total: $89.99“, dann sehen Sie etwa Folgendes:

```
--- Page 1 ---
Invoice #12345
Date: 03/28/2026
--- Page 2 ---
Total: $89.99
Paid by: Credit Card
```

Falls das OCR keinen Text findet, ist die Eigenschaft `Text` ein leerer String — behandeln Sie diesen Fall im Produktionscode, indem Sie `string.IsNullOrWhiteSpace` prüfen.

---

## Vollständiges funktionierendes Beispiel

Unten finden Sie das komplette Programm, das Sie in `Program.cs` kopieren‑und‑einfügen können. Es enthält alle using‑Direktiven, das async `Main` und Kommentare, die jeden Schritt erläutern.

```csharp
using System;
using System.Threading.Tasks;
using Aspose.OCR;

class Program
{
    // Async Main is supported from C# 7.1 onward
    static async Task Main()
    {
        // Step 1: Initialize the OCR engine and set the language to English
        var ocrEngine = new OcrEngine { Language = Language.English };

        // Step 2: Define the image files to be processed
        string[] imagePaths = { "page1.png", "page2.png", "page3.png" };

        // Step 3: Perform asynchronous OCR on all images
        OcrResult[] ocrResults = await ocrEngine.RecognizeImagesAsync(imagePaths);

        // Step 4: Output the recognized text for each page
        for (int i = 0; i < ocrResults.Length; i++)
        {
            Console.WriteLine($"--- Page {i + 1} ---");
            Console.WriteLine(ocrResults[i].Text);
        }
    }
}
```

Speichern Sie die Datei, legen Sie Ihre PNGs neben die ausführbare Datei (oder passen Sie die Pfade an) und führen Sie aus:

```bash
dotnet run
```

Sie sollten den extrahierten Text in der Konsole sehen, was bestätigt, dass Sie erfolgreich **Bilder in Text** umgewandelt haben.

---

## Häufige Sonderfälle behandeln

| Situation | Was zu tun ist |
|-----------|----------------|
| **Low‑resolution PNG** | Erhöhen Sie `ocrEngine.ImageProcessingOptions.Dpi` vor der Erkennung. |
| **Mehrere Sprachen** | Setzen Sie `ocrEngine.Language = Language.English | Language.Spanish;` (bitweises OR). |
| **Große Stapel (Hunderte von Dateien)** | Verarbeiten Sie in Chunks (z. B. 20 Dateien pro `RecognizeImagesAsync`‑Aufruf), um Speicherspitzen zu vermeiden. |
| **Benötigen Sie den Vertrauensscore** | Verwenden Sie `ocrResults[i].Confidence` (ein Float zwischen 0 und 1), um Ergebnisse niedriger Qualität zu filtern. |

Diese Anpassungen halten Ihre OCR‑Pipeline robust, besonders wenn Sie von einer Demo in die Produktion wechseln.

---

## Bonus: Ergebnisse in eine Textdatei speichern

Wenn Sie eine persistente Kopie statt der Konsolenausgabe bevorzugen, fügen Sie einen kleinen Helfer hinzu:

```csharp
using System.IO;

// After the for‑loop:
File.WriteAllLines("OcrOutput.txt", ocrResults.Select(r => r.Text));
Console.WriteLine("All pages saved to OcrOutput.txt");
```

Jetzt haben Sie eine einzelne Datei, die **Text aus Bildern** extrahiert für nachgelagerte Verarbeitung — perfekt zum Indexieren, Durchsuchen oder für die Eingabe in ein Sprachmodell.

---

## Fazit

Wir haben Schritt für Schritt gezeigt, **wie man OCR** in C# mit Aspose verwendet, um **Text aus PNG**‑Dateien zu **extrahieren** und **Bilder in Text** effizient zu konvertieren. Der async‑Ansatz sorgt dafür, dass Ihre Anwendung responsiv bleibt, während die unkomplizierte API den Code lesbar und wartbar hält.  

Probieren Sie es mit Ihren eigenen Dokumenten, experimentieren Sie mit verschiedenen Sprachen und verketten Sie die Ausgabe vielleicht mit einem Suchindex oder einem Zusammenfassungs‑Service. Der Himmel ist die Grenze, wenn Sie zuverlässig Bilder in durchsuchbare Zeichenketten verwandeln können.

---

### Nächste Schritte & verwandte Themen

- **Text aus Bildern** in anderen Formaten (JPEG, TIFF) extrahieren – einfach die Dateierweiterungen ändern.  
- **Batch‑Verarbeitung mit Parallel.ForEach** für massive Arbeitslasten.  
- **Post‑OCR‑Bereinigung** mit regulären Ausdrücken, um Daten, Beträge oder IDs zu normalisieren.  
- **Integration mit Azure Cognitive Services**, falls Sie cloud‑basiertes OCR mit zusätzlichen Funktionen benötigen.  

Fühlen Sie sich frei, einen Kommentar zu hinterlassen, wenn Sie auf Probleme stoßen, oder zu teilen, wie Sie diesen Basis‑Workflow erweitert haben. Viel Spaß beim Coden!   (Image: ![Beispielausgabe zur Verwendung von OCR](/images/ocr-result.png){.align-center alt="Beispielausgabe zur Verwendung von OCR"} )

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}