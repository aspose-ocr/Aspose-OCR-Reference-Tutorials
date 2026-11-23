---
category: general
date: 2026-10-11
description: Erfahren Sie, wie Sie OCR für Bilder in C# mit Aspose.OCR durchführen,
  einschließlich der Installation von System.Drawing.Common und dem Extrahieren von
  Text aus JPG‑Dateien.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- perform OCR on image
- extract text from JPG
- recognize text from picture
- load image for OCR
- install System.Drawing.Common package
language: de
lastmod: 2026-10-11
og_description: Führen Sie OCR auf einem Bild in C# mit Aspose.OCR durch. Dieser Leitfaden
  zeigt Ihnen, wie Sie System.Drawing.Common installieren, ein Bild für OCR laden
  und Text aus einer JPG extrahieren.
og_image_alt: Screenshot of C# console output displaying recognized text after performing
  OCR on image
og_title: OCR in C# auf Bild ausführen – Schritt‑für‑Schritt‑Anleitung
schemas:
- author: Aspose
  dateModified: '2026-10-11'
  description: Learn how to perform OCR on image in C# with Aspose.OCR, including
    installing System.Drawing.Common and extracting text from JPG files.
  headline: How to perform OCR on image in C# using Aspose.OCR
  type: TechArticle
tags:
- OCR
- C#
- Aspose
title: Wie man OCR auf einem Bild in C# mit Aspose.OCR durchführt
url: /de/net/text-recognition/how-to-perform-ocr-on-image-in-c-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man OCR auf Bildern in C# mit Aspose.OCR durchführt

Wenn Sie **OCR auf Bilddateien** in einer .NET‑Anwendung ausführen müssen, zeigt Ihnen diese Anleitung eine vollständige Lösung. Mit Aspose.OCR können Sie schnell **Text aus Bildern** wie JPGs erkennen und das Ergebnis in einem Konsolenfenster anzeigen.

Sie lernen, wie man:

* **das System.Drawing.Common‑Paket installiert** – die Bibliothek, die die Klasse `Image` bereitstellt,
* **ein Bild für OCR lädt** – ein JPEG oder PNG in den Speicher einliest,
* das Sprachmodell konfiguriert,
* **OCR auf dem Bild ausführt** und schließlich,
* **Text aus JPG extrahiert** und ausgibt.

Die Schritte sind für .NET 6+ geschrieben, funktionieren aber auch mit .NET Framework 4.6.1 oder höher.

---

## Voraussetzungen

| Anforderung | Warum das wichtig ist |
|-------------|-----------------------|
| .NET 6 SDK (oder .NET Framework 4.6.1+) | Stellt die Laufzeit für die C#‑Konsolen‑App bereit. |
| Visual Studio 2022 (oder jede IDE) | Erleichtert das Hinzufügen von NuGet‑Paketen und das Ausführen des Programms. |
| Internetverbindung (nur beim ersten Ausführen) | Aspose.OCR lädt das Sprachmodul automatisch herunter. |
| Ein Beispielbild mit kyrillischem oder lateinischem Text (z. B. `sample_cyrillic.jpg`) | Wird verwendet, um **Text aus JPG zu extrahieren** zu demonstrieren. |

---

## Schritt 1: System.Drawing.Common‑Paket installieren

Das NuGet‑Paket `System.Drawing.Common` stellt die Klasse `Image` bereit, mit der Sie **ein Bild für OCR laden**. Öffnen Sie die Package Manager Console und führen Sie aus:

```powershell
Install-Package System.Drawing.Common
```

> **Pro‑Tipp:** Ziel‑Framework `net6.0-windows` verwenden oder `<UseWindowsForms>true</UseWindowsForms>` zur Projektdatei hinzufügen, falls Sie plattformspezifische Warnungen unter Linux/macOS erhalten.

---

## Schritt 2: Das Aspose.OCR‑NuGet‑Paket hinzufügen

Aspose.OCR enthält die OCR‑Engine und die Sprachmodelle. Installieren Sie es mit:

```powershell
Install-Package Aspose.OCR
```

Das Paket ist leichtgewichtig; die benötigten Sprachdaten (z. B. Kyrillisch) werden beim ersten Setzen von `OcrEngine.Language` automatisch heruntergeladen.

---

## Schritt 3: Bild für OCR laden

Das Laden des Bildes ist der erste konkrete Schritt, bevor Sie **OCR auf dem Bild ausführen** können. Die Methode `Image.FromFile` liest jedes von GDI+ unterstützte Format, einschließlich JPG, PNG, BMP und TIFF.

```csharp
using System.Drawing; // Requires System.Drawing.Common

// Replace the path with the location of your test picture.
string imagePath = @"YOUR_DIRECTORY/sample_cyrillic.jpg";
Image ocrImage = Image.FromFile(imagePath);
```

*Falls die Datei nicht existiert, wird eine `FileNotFoundException` ausgelöst – wickeln Sie den Aufruf in einen try/catch‑Block für Produktionscode ein.*

---

## Schritt 4: Engine konfigurieren und **OCR auf dem Bild ausführen**

Erzeugen Sie eine `OcrEngine`‑Instanz, wählen Sie das Sprachmodell, weisen Sie das geladene Bild zu und rufen Sie `Recognize()` auf.

```csharp
using Aspose.OCR;

// Step 4: Initialize OCR engine and set language
var ocrEngine = new OcrEngine
{
    // Choose the language you need; Cyrillic is used in this example.
    Language = OcrLanguage.Cyrillic,
    Image = ocrImage
};

// Execute the OCR operation
OcrResult ocrResult = ocrEngine.Recognize();
```

Die Methode `Recognize()` liefert ein `OcrResult`‑Objekt, das den extrahierten Text, Konfidenzwerte und Begrenzungsrahmen enthält. Das Sprachmodul wird beim ersten Gebrauch automatisch heruntergeladen, sodass keine zusätzlichen Dateien nötig sind.

---

## Schritt 5: **Text aus JPG extrahieren** und anzeigen

Jetzt können Sie **Text aus Bildern erkennen** und das Ergebnis ausgeben. Die Eigenschaft `Text` von `OcrResult` enthält den reinen Zeichenstring.

```csharp
// Step 5: Output recognized text
Console.WriteLine("Recognized text:");
Console.WriteLine(ocrResult.Text);
```

### Erwartete Konsolenausgabe

```
Recognized text:
Пример текста на кириллице
```

Enthält das Quellbild englischen Text, wird die englische Satz‑Zeichenfolge, die Sie im Bild platziert haben, ausgegeben.

---

## Sonderfälle und bewährte Vorgehensweisen

| Situation | Empfehlung |
|-----------|------------|
| **Große Bilder ( > 5 MB )** | Bild auf ≤ 2000 px an der längsten Seite verkleinern, bevor OCR durchgeführt wird, um Speicherverbrauch zu reduzieren und die Geschwindigkeit zu erhöhen. |
| **Mehrere Sprachen in einem Bild** | `ocrEngine.AddLanguage(OcrLanguage.English)` zusätzlich zu Kyrillisch aufrufen und dann `ocrEngine.Language = OcrLanguage.Multilingual` setzen. |
| **Scans mit geringem Kontrast** | Kontrast mit `System.Drawing.Graphics` erhöhen, bevor das Bitmap an die Engine übergeben wird. |
| **Ausführung unter Linux/macOS** | Sicherstellen, dass die native Abhängigkeit `libgdiplus` installiert ist (`sudo apt-get install -y libgdiplus`). |
| **Wiederholte OCR‑Aufrufe** | dieselbe `OcrEngine`‑Instanz wiederverwenden und nur `ocrEngine.Image` austauschen, um wiederholtes Laden des Moduls zu vermeiden. |

---

## Vollständiges, ausführbares Programm

Im Folgenden finden Sie die komplette Konsolen‑Anwendung, die alle vorherigen Schritte integriert. Kopieren Sie den Code in ein neues C#‑Konsolen‑Projekt, passen Sie den Bildpfad an und führen Sie das Programm aus.

```csharp
using System;
using System.Drawing;                 // Install System.Drawing.Common if needed
using Aspose.OCR;                     // NuGet package: Aspose.OCR

class Program
{
    static void Main()
    {
        // Step 1: Install System.Drawing.Common (handled via NuGet)
        // Step 2: Install Aspose.OCR (handled via NuGet)

        // Step 3: Load the image that contains the text to be recognized
        // Replace the placeholder with the actual path to your JPG or PNG file.
        string imagePath = @"YOUR_DIRECTORY/sample_cyrillic.jpg";
        Image ocrImage;
        try
        {
            ocrImage = Image.FromFile(imagePath);
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Failed to load image: {ex.Message}");
            return;
        }

        // Step 4: Create the OCR engine and choose the language model
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.Cyrillic, // Change to OcrLanguage.English for Latin scripts
            Image = ocrImage
        };

        // Step 5: Perform OCR on the loaded picture
        OcrResult ocrResult = ocrEngine.Recognize();

        // Step 6: Display the extracted text
        Console.WriteLine("Recognized text:");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Beim Ausführen des Programms** wird die erkannte Zeichenfolge in der Konsole ausgegeben, was bestätigt, dass Sie **OCR auf dem Bild erfolgreich durchgeführt** und **Text aus JPG extrahiert** haben.

---

## Fazit

Sie wissen jetzt, wie man **OCR auf Bilddateien** in C# mit Aspose.OCR ausführt – von der Installation des erforderlichen **System.Drawing.Common‑Pakets** über das **Laden des Bildes für OCR**, die Auswahl des passenden Sprachmodells bis hin zum **Extrahieren von Text aus JPG**. Dieses End‑to‑End‑Beispiel bietet Ihnen eine solide Basis für den Aufbau fortgeschrittener Dokumenten‑Verarbeitungspipelines, etwa das Stapel‑Verarbeiten von Bildordnern oder die Integration von OCR in eine Web‑API.

### Was kommt als Nächstes?

* Erkunden Sie **Text aus Bildern in PDFs erkennen**, indem Sie jede Seite zuerst in ein Bild konvertieren.
* Experimentieren Sie mit den Eigenschaften `Resolution`, `Threshold` und `MaxProcessingTime` der `OcrEngine`, um die Genauigkeit bei verrauschten Scans fein abzustimmen.
* Kombinieren Sie die OCR‑Ausgabe mit einer Natural‑Language‑Processing‑Bibliothek, um extrahierten Inhalt automatisch zu kategorisieren.

Passen Sie den Code gern für weitere Bildformate an, ergänzen Sie Fehlerbehandlung oder integrieren Sie ihn in größere Anwendungen. Viel Spaß beim Coden!

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, damit Sie weitere API‑Funktionen meistern und alternative Implementierungsansätze in Ihren Projekten erkunden können.

- [Text aus Bild in C# extrahieren – Vollständiger Aspose OCR‑Leitfaden](/ocr/english/net/text-recognition/extract-text-from-image-in-c-complete-aspose-ocr-guide/)
- [Bildtext in C# mit Sprachauswahl mittels Aspose.OCR extrahieren](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Wie man Texterkennung aus einem Stream mit Aspose OCR durchführt](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}