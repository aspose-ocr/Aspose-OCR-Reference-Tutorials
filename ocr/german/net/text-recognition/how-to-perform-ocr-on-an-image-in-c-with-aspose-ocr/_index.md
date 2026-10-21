---
category: general
date: 2026-10-21
description: Erfahren Sie, wie Sie OCR auf einer JPG durchführen, Text aus dem Bild
  extrahieren und das Bild für OCR mit Aspose.OCR in C# laden. Vollständige Schritt‑für‑Schritt‑Anleitung.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to perform OCR
- extract text from image
- recognize text from jpg
- load image for OCR
- perform OCR on image
language: de
lastmod: 2026-10-21
og_description: Wie man OCR auf einem Bild in C# mit Aspose.OCR durchführt. Folgen
  Sie dieser Anleitung, um ein Bild für OCR zu laden, Text aus einer JPG zu erkennen
  und Text aus dem Bild zu extrahieren.
og_image_alt: Screenshot showing how to perform OCR on a Cyrillic image in C#
og_title: Wie man OCR in C# auf einem Bild durchführt – Schritt‑für‑Schritt‑Anleitung
schemas:
- author: Aspose
  dateModified: '2026-10-21'
  description: Learn how to perform OCR on a JPG, extract text from image and load
    image for OCR using Aspose.OCR in C#. Complete step‑by‑step guide.
  headline: How to perform OCR on an image in C# with Aspose.OCR
  type: TechArticle
tags:
- OCR
- C#
- Aspose.OCR
- Image processing
- Text extraction
title: Wie man OCR auf einem Bild in C# mit Aspose.OCR durchführt
url: /de/net/text-recognition/how-to-perform-ocr-on-an-image-in-c-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR auf einem Bild in C# mit Aspose.OCR durchführen

Wenn Sie **wie man OCR durchführt** auf einem Bild benötigen, zeigt Ihnen dieses Tutorial eine komplette, sofort ausführbare Lösung. Sie lernen, wie man ein Bild für OCR lädt, Text aus JPG‑Dateien erkennt und Text aus einem Bild mit der Aspose.OCR‑Bibliothek extrahiert.

Der Leitfaden deckt alles ab, von der Installation des NuGet‑Pakets über die Handhabung von Sprachmodellen bis hin zum Ausgeben des erkannten Ergebnisses. Am Ende können Sie OCR in jedes .NET‑Projekt integrieren und kyrillische oder andere Sprachtexte verarbeiten, ohne die IDE zu verlassen.

## Was Sie benötigen

- .NET 6.0 oder höher (der Code funktioniert auch unter .NET Framework 4.7+)
- Visual Studio 2022 (oder jeder C#‑Editor)
- Internetzugang für den ersten Durchlauf (Aspose.OCR lädt das Sprachmodell automatisch herunter)
- Ein Beispielbild, z. B. `cyrillic_sample.jpg`, in einem Ordner, den Sie im Code referenzieren können

## Schritt 1: Aspose.OCR installieren

Öffnen Sie den NuGet‑Paket‑Manager und fügen Sie **Aspose.OCR** zu Ihrem Projekt hinzu:

```bash
dotnet add package Aspose.OCR
```

Das Paket enthält die OCR‑Engine, Sprachmodelle und Hilfsklassen, die für die Bildverarbeitung benötigt werden. Keine zusätzlichen DLLs sind erforderlich.

## Schritt 2: Die OCR‑Engine erstellen – wie man OCR durchführt

Die erste eigentliche Aufgabe bei **wie man OCR durchführt** besteht darin, die Engine zu instanziieren. Dieses Objekt verwaltet die gesamte Erkennungspipeline.

```csharp
using Aspose.OCR;

// Create an OCR engine instance
OcrEngine engine = new OcrEngine();
```

`OcrEngine` ist leichtgewichtig; Sie können dieselbe Instanz für mehrere Bilder wiederverwenden, was die Leistung bei der Stapelverarbeitung verbessert.

## Schritt 3: Bild für OCR laden

Vor der Erkennung müssen Sie die Bilddaten bereitstellen. Der Schritt **Bild für OCR laden** akzeptiert viele Formate, aber dieses Beispiel konzentriert sich auf eine JPEG‑Datei.

```csharp
// Load the image you want to process
engine.Image = OcrImage.FromFile(@"C:\Images\cyrillic_sample.jpg");
```

`OcrImage.FromFile` liest die Datei in den Speicher und bereitet sie für die Engine vor. Ist der Dateipfad ungültig, wird eine `ArgumentException` ausgelöst, stellen Sie also sicher, dass der Pfad korrekt ist.

## Schritt 4: Die passende Sprache auswählen (optional, aber empfohlen)

Enthält Ihr Bild kyrillische Zeichen, setzen Sie die Sprache auf `Cyrillic`. Das benötigte Modell wird beim ersten Durchlauf automatisch heruntergeladen.

```csharp
// Choose the language model
engine.Language = OcrLanguage.Cyrillic;
```

Sie können zu anderen Sprachen wechseln (z. B. `OcrLanguage.English`), indem Sie diese Eigenschaft ändern. Die Bibliothek unterstützt über 60 Sprachen.

## Schritt 5: Text aus JPG erkennen – wie man OCR auf einem JPEG durchführt

Rufen Sie nun die Methode `Recognize` auf. Dies ist der Kern von **wie man OCR durchführt** und übersetzt das Bitmap in Unicode‑Text.

```csharp
// Perform the recognition
engine.Recognize();
```

Die Methode blockiert, bis der OCR‑Vorgang abgeschlossen ist. Bei großen Bildern sollten Sie sie möglicherweise in einem Hintergrund‑Thread ausführen, um die UI reaktionsfähig zu halten.

## Schritt 6: Text aus Bild extrahieren

Nach der Erkennung speichert die Engine das Ergebnis in der Eigenschaft `Text`. Damit ist der Schritt **Text aus Bild extrahieren** abgeschlossen.

```csharp
// Retrieve the extracted text
string extractedText = engine.Text;

// Output the recognized text to the console
Console.WriteLine(extractedText);
```

Die Ausgabe enthält die genauen Zeichen, die im Bild gefunden wurden, wobei Zeilenumbrüche und Satzzeichen erhalten bleiben.

## Vollständiges, ausführbares Beispiel

Wenn Sie alle Schritte zusammenfügen, erhalten Sie ein einzelnes Programm, das Sie kopieren, einfügen und ausführen können:

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // Step 1: Create the OCR engine
        OcrEngine engine = new OcrEngine();

        // Step 2: Load the image for OCR
        engine.Image = OcrImage.FromFile(@"C:\Images\cyrillic_sample.jpg");

        // Step 3: Choose the language model (Cyrillic in this case)
        engine.Language = OcrLanguage.Cyrillic;

        // Step 4: Perform OCR on the image
        engine.Recognize();

        // Step 5: Extract text from image
        string extractedText = engine.Text;

        // Step 6: Output the recognized text
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(extractedText);
    }
}
```

### Erwartete Ausgabe

Wenn `cyrillic_sample.jpg` den Satz „Привет мир“ (Hello world) enthält, wird die Konsole anzeigen:

```
=== OCR Result ===
Привет мир
```

Verschiedene Schriftarten oder Bildqualität können die Genauigkeit beeinflussen, aber Aspose.OCR erreicht in der Regel >95 % Erkennung bei klaren Drucken.

## Häufige Fallstricke und praktische Tipps

- **Bildqualität ist wichtig** – niedrig aufgelöste oder verrauschte JPEGs verringern die Genauigkeit. Verarbeiten Sie das Bild ggf. vor (z. B. Kontrast erhöhen) mit `engine.Image.AdjustContrast()`.
- **Sprachmodell‑Download** – die erste Ausführung lädt das Modell nach `%USERPROFILE%\.Aspose\OCR` herunter. Stellen Sie sicher, dass der Prozess Schreibrechte hat.
- **Stapelverarbeitung** – verwenden Sie dieselbe `OcrEngine`‑Instanz erneut und ändern Sie nur `engine.Image` zwischen den Dateien. So vermeiden Sie wiederholtes Laden des Modells.
- **Speichernutzung** – große Bilder verbrauchen mehr RAM. Rufen Sie `engine.Image.Dispose()` nach jeder Erkennung auf, wenn Sie viele Dateien in einer Schleife verarbeiten.
- **Thread‑Sicherheit** – `OcrEngine` ist nicht thread‑sicher. Erstellen Sie bei Parallelisierung pro Thread eine separate Instanz.

## Fazit

Sie wissen jetzt, **wie man OCR** auf einem JPEG durchführt, **Bild für OCR lädt** und **Text aus Bild extrahiert** mit Aspose.OCR in C#. Die vollständige Lösung zeigt das Einstellen der Sprache, das Erkennen von Text aus JPG und das Ausgeben des Ergebnisses und bietet Ihnen eine solide Grundlage für jedes Text‑Extraktions‑Projekt.

Als Nächstes erkunden Sie verwandte Themen wie **OCR auf Bild‑Stapel** durchführen, OCR in ASP.NET Core APIs integrieren oder den extrahierten Text in durchsuchbare PDFs umwandeln. Experimentieren Sie mit verschiedenen Sprachen und Bildvorverarbeitung, um die Erkennungsqualität zu maximieren.

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige funktionierende Codebeispiele mit Schritt‑für‑Schritt‑Erklärungen, die Ihnen helfen, zusätzliche API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Wie man OCR in C# durchführt – Bild in Text konvertieren mit Aspose OCR](/ocr/english/net/text-recognition/how-to-perform-ocr-in-c-convert-image-to-text-with-aspose-oc/)
- [Wie man OCR in C# durchführt – Text aus Bild erkennen](/ocr/english/net/text-recognition/how-to-perform-ocr-in-c-recognize-text-from-image/)
- [Wie man Text aus Bild extrahiert mit Aspose.OCR für .NET](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}