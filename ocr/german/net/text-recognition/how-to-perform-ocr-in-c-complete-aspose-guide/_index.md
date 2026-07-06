---
category: general
date: 2026-02-16
description: Erfahren Sie, wie Sie OCR in C# mit Aspose.OCR durchführen – Text aus
  Fotos erkennen, Text aus Scans lesen und Text aus Quittungen mit hoher Genauigkeit
  extrahieren.
draft: false
keywords:
- how to perform OCR
- recognize text from photo
- read text from scan
- extract text from receipt
- improve OCR accuracy
language: de
og_description: Erfahren Sie, wie Sie OCR in C# mit Aspose.OCR durchführen. Dieser
  Leitfaden zeigt Ihnen, wie Sie Text aus einem Foto erkennen, Text aus einem Scan
  lesen und Text aus einer Quittung extrahieren.
og_title: Wie man OCR in C# ausführt – Vollständiger Aspose-Leitfaden
tags:
- C#
- Aspose.OCR
- Image Processing
title: Wie man OCR in C# ausführt – Vollständiger Aspose-Leitfaden
url: /de/net/text-recognition/how-to-perform-ocr-in-c-complete-aspose-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man OCR in C# durchführt – Vollständiger Aspose‑Leitfaden

Haben Sie sich jemals gefragt, **wie man OCR** auf einer verschwommenen Quittung oder einem zufälligen Foto, das Sie mit Ihrem Handy aufgenommen haben, durchführt? Sie sind nicht allein. In vielen realen Anwendungen müssen wir **Text aus Foto**‑Dateien erkennen, **Text aus Scan**‑Dokumenten lesen oder **Text aus Quittung**‑Bilder extrahieren, ohne Daten an einen Cloud‑Dienst zu senden.  

In diesem Tutorial gehen wir Schritt für Schritt durch ein eigenständiges Beispiel, das Ihnen zeigt, **wie man OCR** mit Aspose.OCR durchführt, und geben Tipps, wie Sie **die OCR‑Genauigkeit verbessern** können. Am Ende haben Sie ein sofort ausführbares C#‑Konsolenprogramm, das aus jedem Bild, das Sie ihm geben, Klartext extrahiert.

> **Was Sie benötigen**  
> * .NET 6 SDK (oder jede aktuelle .NET‑Version)  
> * Aspose.OCR NuGet‑Paket (`Install-Package Aspose.OCR`)  
> * Ein Beispielbild – zum Beispiel ein Foto einer Quittung namens `photo_receipt.jpg`  

Wenn das vertraut klingt, los geht's.

![how to perform OCR example](image.png){alt="how to perform OCR"}

## Wie man OCR mit Aspose.OCR in C# durchführt

Der erste Schritt besteht darin, die OCR‑Engine einzurichten und ein englisches Sprachmodell zu laden. Das ist das Kernstück von **wie man OCR** mit Aspose; ohne ein Sprachmodell wüsste die Engine nicht, nach welchen Zeichen sie suchen soll.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Load the English language model – change this if you need another language
ocrEngine.LoadLanguage(LanguageModel.English);
```

*Warum das wichtig ist*: Das Laden des richtigen Sprachmodells beeinflusst direkt die Erkennungs‑Geschwindigkeit und -Genauigkeit. Englisch ist der häufigste Fall, aber Aspose liefert Dutzende weitere Modelle, falls Sie **Text aus Scan**‑Dokumenten in Französisch, Deutsch usw. lesen müssen.

## Text aus Foto erkennen

Fotos, die mit einem Handy aufgenommen wurden, leiden häufig unter Rotation, Rauschen oder geringem Kontrast. Bevor wir die Engine bitten, **Text aus Foto** zu **erkennen**, konfigurieren wir einige Vorverarbeitungs‑Optionen, die das Bild säubern.

```csharp
// Configure preprocessing to boost OCR results
PreprocessingOptions preprocessingOptions = new PreprocessingOptions
{
    Deskew = true,                     // Auto‑correct rotation (helps with tilted receipts)
    Denoise = DenoiseLevel.Medium,    // Reduce graininess
    Binarize = BinarizeMethod.Otsu,   // Convert to black‑and‑white for sharper edges
    ContrastEnhancement = true        // Boost contrast for faint characters
};

// Apply the preprocessing configuration
ocrEngine.Preprocessing = preprocessingOptions;
```

*Pro‑Tipp*: Wenn Zeichen fehlen, versuchen Sie, `DenoiseLevel` auf `High` zu setzen oder `BinarizeMethod.Sauvola` zu verwenden. Diese Anpassungen sind Teil von **die OCR‑Genauigkeit verbessern**‑Strategien.

## Text aus Scan lesen

Jetzt, wo die Engine vorbereitet ist, laden wir das Bild. Egal, ob es sich um eine gescannte PDF‑Seite handelt, die als JPEG gespeichert ist, oder um ein Foto eines gedruckten Formulars – der Code bleibt gleich.

```csharp
// Load the image you want to process
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/photo_receipt.jpg");
```

Wenn Sie einen `Stream` anstelle eines Dateipfads haben, ersetzen Sie einfach `FromFile` durch `FromStream`. Diese Flexibilität ist praktisch, wenn Sie **Text aus Scan**‑Bilder verarbeiten, die aus einem Web‑Upload stammen.

## Text aus Quittung extrahieren

Wenn alles eingestellt ist, besteht der eigentliche OCR‑Aufruf aus einer einzigen Zeile. Die Methode gibt den extrahierten Klartext‑String zurück, den wir dann anzeigen, speichern oder an ein anderes System weitergeben können.

```csharp
// Perform OCR and capture the result
string extractedText = ocrEngine.Recognize();

// Output the text to the console
Console.WriteLine("=== OCR RESULT ===");
Console.WriteLine(extractedText);
```

**Erwartete Ausgabe** (Beispiel für eine einfache Quittung):

```
=== OCR RESULT ===
Store: CoffeeShop
Date: 2024-02-15
Item      Qty   Price
Latte      2    4.50
Bagel      1    2.75
Total            7.25
```

Wenn die Ausgabe wirr aussieht, überprüfen Sie den Vorverarbeitungs‑Abschnitt – das ist der häufigste Ort, um **die OCR‑Genauigkeit zu verbessern**.

## OCR‑Genauigkeit verbessern – Erweiterte Anpassungen

Während die Standardeinstellungen für viele Fälle funktionieren, benötigen produktionsreife Pipelines oft zusätzlichen Feinschliff:

| Situation | Anpassung | Grund |
|-----------|------------|--------|
| Sehr dunkler Hintergrund | `ContrastEnhancement = true` + `Binarize = BinarizeMethod.Sauvola` | Erhöht die Trennung zwischen Text und Hintergrund |
| Handschriftliche Notizen | `ocrEngine.LoadLanguage(LanguageModel.EnglishHandwritten)` | Spezialisiertes Modell für kursiven Schreibstil |
| Mehrseitige Scans | Schleife über jedes Seiten‑Bild und Aufruf von `Recognize()` pro Iteration | Hält den Speicherverbrauch gering |
| Große Bilder (> 2000 px) | Größe vor dem OCR‑Aufruf ändern (`Image.Resize(width, height)`) | Schnellere Verarbeitung, weniger Speicherbelastung |

Denken Sie daran, **wie man OCR** ist kein Einheitsrezept – Sie werden oft mit diesen Reglern experimentieren, bis die Ausgabe Ihren Qualitätsansprüchen genügt.

## Vollständiges funktionierendes Beispiel

Unten finden Sie das komplette, copy‑and‑paste‑bereite Programm. Es enthält alle besprochenen Bausteine sowie einen kleinen Helfer, der prüft, ob die Datei existiert, bevor sie gelesen wird.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine and load language
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.LoadLanguage(LanguageModel.English);

        // 2️⃣ Set up preprocessing to improve OCR accuracy
        ocrEngine.Preprocessing = new PreprocessingOptions
        {
            Deskew = true,
            Denoise = DenoiseLevel.Medium,
            Binarize = BinarizeMethod.Otsu,
            ContrastEnhancement = true
        };

        // 3️⃣ Path to the image – change this to your own file
        string imagePath = Path.Combine("YOUR_DIRECTORY", "photo_receipt.jpg");

        if (!File.Exists(imagePath))
        {
            Console.WriteLine($"⚠️  Image not found: {imagePath}");
            return;
        }

        // 4️⃣ Load the image (recognize text from photo / read text from scan)
        ocrEngine.Image = ImageStream.FromFile(imagePath);

        // 5️⃣ Perform OCR – this is the core of how to perform OCR
        string extractedText = ocrEngine.Recognize();

        // 6️⃣ Show the result – you can now extract text from receipt, invoice, etc.
        Console.WriteLine("=== OCR RESULT ===");
        Console.WriteLine(extractedText);
    }
}
```

Führen Sie das Programm mit `dotnet run` aus. Wenn alles korrekt eingerichtet ist, sehen Sie den extrahierten Text in der Konsole ausgegeben.

## Häufige Fragen & Randfälle

**F: Was ist, wenn das Bild ein PDF ist?**  
A: Konvertieren Sie jede PDF‑Seite zuerst in ein Bild (z. B. mit `Aspose.Pdf` oder `PdfSharp`) und übergeben Sie das resultierende Bitmap an `ocrEngine.Image`.

**F: Kann ich Bilder parallel verarbeiten?**  
A: Ja, aber instanziieren Sie für jeden Thread ein separates `OcrEngine`. Die Engine ist nicht thread‑sicher, sodass das Teilen einer einzigen Instanz zu Rennbedingungen führen kann.

**F: Funktioniert das unter Linux?**  
A: Absolut. Aspose.OCR ist plattformübergreifend; stellen Sie nur sicher, dass die nativen Abhängigkeiten installiert sind (`libgdiplus` für .NET Core unter Linux).

**F: Wie gehe ich mit mehrsprachigen Quittungen um?**  
A: Laden Sie mehrere Sprachmodelle, bevor Sie erkennen:  
```csharp
ocrEngine.LoadLanguage(LanguageModel.English);
ocrEngine.LoadLanguage(LanguageModel.Spanish);
```  
Die Engine versucht jedes Modell der Reihe nach.

## Fazit

Sie haben nun eine solide, End‑zu‑End‑Lösung für **wie man OCR** in C# mit Aspose.OCR. Das Tutorial behandelte alles von der Initialisierung der Engine, **Text aus Foto** zu **erkennen**, **Text aus Scan** zu **lesen**, bis zum **Extrahieren von Text aus Quittungen**, und zeigte Ihnen praktische Wege, **die OCR‑Genauigkeit zu verbessern**.  

Nächste Schritte? Tauschen Sie das englische Modell gegen ein handschriftliches aus, experimentieren Sie mit verschiedenen `BinarizeMethod`‑Werten oder integrieren Sie den OCR‑Aufruf in eine ASP.NET‑API, die Uploads on‑the‑fly verarbeitet. Die Möglichkeiten sind so vielfältig wie die Bilder, die Sie ihr zuführen.

Haben Sie weitere Fragen zu OCR, Bildvorverarbeitung oder den Aspose‑Bibliotheken? Hinterlassen Sie einen Kommentar oder stöbern Sie in der offiziellen Aspose.OCR‑Dokumentation für tiefere Einblicke. Viel Spaß beim Coden!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}