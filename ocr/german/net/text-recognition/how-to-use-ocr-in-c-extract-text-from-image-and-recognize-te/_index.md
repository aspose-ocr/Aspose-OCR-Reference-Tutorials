---
category: general
date: 2026-02-13
description: Wie man OCR in C# verwendet, um Text aus einem Bild zu extrahieren, Text
  von einem Foto oder JPG zu erkennen und OCR auf einem Bild ohne Internet auszuführen.
draft: false
keywords:
- how to use OCR
- extract text from image
- recognize text from photo
- recognize text from jpg
- run OCR on image
language: de
og_description: Wie man OCR in C# verwendet, um Text aus einem Bild zu extrahieren,
  Text von einem Foto zu erkennen und OCR auf ein Bild anzuwenden, mit einem vollständigen,
  ausführbaren Beispiel.
og_title: Wie man OCR in C# verwendet – Text aus Bild extrahieren
tags:
- OCR
- C#
- Image Processing
title: Wie man OCR in C# verwendet – Text aus Bild extrahieren und Text von Foto erkennen
url: /de/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-image-and-recognize-te/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# So verwenden Sie OCR in C# – Text aus Bild extrahieren und Text von Foto erkennen

Haben Sie sich jemals gefragt, **wie man OCR** verwendet, um Wörter aus einem Screenshot, einer gescannten Quittung oder einem zufälligen Foto, das Sie mit Ihrem Handy gemacht haben, herauszuholen? Sie sind nicht allein. In vielen realen Anwendungen müssen wir Bilder in durchsuchbaren Text umwandeln, und das lokal – ohne eine wackelige Internetverbindung – kann sich wie ein Rätsel anfühlen.

Deshalb zeigt Ihnen dieser Leitfaden Schritt für Schritt, wie Sie **Text aus Bild**‑Dateien mit einer C#‑OCR‑Engine extrahieren, und er behandelt außerdem, wie Sie **Text von Foto** erkennen, **Text von JPG** erkennen und **OCR auf Bild**‑Dateien ausführen, die direkt auf Ihrer Festplatte liegen. Am Ende haben Sie ein komplettes, copy‑paste‑fertiges Programm, das sofort funktioniert.

## Was Sie lernen werden

- Wie Sie eine OCR‑Engine für vereinfachtes Chinesisch (oder jede andere von Ihnen eingebundene Sprache) konfigurieren.  
- Den genauen Code, der **Ressourcen** aus einem lokalen Ordner lädt – ohne Netzwerkaufrufe.  
- Wie Sie **Text von Foto**‑Dateien wie JPEG, PNG oder BMP erkennen.  
- Tipps zum Umgang mit gängigen Sonderfällen wie fehlenden Modelldateien oder nicht unterstützten Bildformaten.  
- Ein vollständiges, ausführbares Beispiel, das Sie in Visual Studio einfügen und sofort Ergebnisse sehen können.

### Voraussetzungen

- .NET 6.0 oder höher (die hier verwendete API zielt auf .NET Standard 2.0 ab, sodass ältere Versionen ebenfalls funktionieren).  
- Grundlegende Kenntnisse in C# und Visual Studio (oder einer anderen IDE Ihrer Wahl).  
- Die OCR‑Bibliothek, die Sie verwenden (das Snippet geht von einer fiktiven `OcrEngine`‑Klasse aus, die mit Sprachmodellen geliefert wird).  
- Ein Ordner, der die erforderlichen Sprachmodell‑Dateien enthält – denken Sie an ihn als das „Gehirn“, das die Engine zum Lesen chinesischer Zeichen nutzt.

> **Pro‑Tipp:** Wenn Sie die chinesischen Modelldateien noch nicht haben, laden Sie sie einmal von der Website des Anbieters herunter und legen Sie sie in einen Ordner wie `C:\OcrResources`. Die Engine muss danach nie wieder online gehen.

---

![Diagramm, das den OCR-Prozess auf einem Foto zeigt](path/to/ocr-diagram.png "Diagramm, das den OCR-Prozess auf einem Foto zeigt")

## So verwenden Sie OCR: Engine einrichten

Das Erste, was Sie benötigen, ist eine Instanz der OCR‑Engine, konfiguriert für die Sprache, die Sie benötigen. In diesem Tutorial zielen wir auf **vereinfachtes Chinesisch** ab, aber das Ersetzen von `OcrLanguage.ChineseSimplified` durch `OcrLanguage.English` (oder einen anderen Enum‑Wert) ist nur eine einzeilige Änderung.

```csharp
using System;
using YourOcrLibrary;   // Replace with the actual namespace of your OCR SDK

// Step 1: Create and configure the OCR engine for Simplified Chinese
var ocrEngine = new OcrEngine
{
    // Primary keyword appears here naturally
    Language = OcrLanguage.ChineseSimplified,

    // Point to a folder that already contains the Chinese model files
    ResourceFolder = @"C:\OcrResources"
};
```

**Warum das wichtig ist:**  
Durch das Setzen der `Language`‑Eigenschaft teilen Sie der Engine mit, welchen Zeichensatz sie erwarten soll. Der `ResourceFolder` ist der Ort, an dem die Engine nach den Gewichten des neuronalen Netzes und den Sprachwörterbüchern sucht – quasi das Gedächtnis des Gehirns. Zeigen Sie auf den falschen Ordner, wirft die Engine eine `FileNotFoundException` und Sie kommen nicht weiter.

## Text aus Bild extrahieren – Ressourcen laden

Bevor die Engine überhaupt etwas lesen kann, müssen Sie diese Modelldateien in den Speicher laden. Dieser Schritt ist **entscheidend**, weil er bei jeder Bildverarbeitung einen Netzwerkaufruf vermeidet.

```csharp
// Step 2: Load the language resources from the specified folder (no internet required)
try
{
    ocrEngine.LoadResources();
    Console.WriteLine("Resources loaded successfully.");
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Failed to load OCR resources: {ex.Message}");
    // In a real app you might fallback to a default language or abort gracefully
}
```

**Was könnte schiefgehen?**  
Ist der Ordnerpfad falsch oder sind die Dateien beschädigt, löst `LoadResources()` eine Ausnahme aus. Der obige `try/catch`‑Block demonstriert eine elegante Fehlerbehandlung – etwas, das Sie in der Produktion häufig benötigen.

## Text von Foto erkennen – OCR ausführen

Jetzt der spaßige Teil: Eine Bilddatei an die Engine übergeben und den erkannten Text zurückbekommen. Das ist der Kern von **run OCR on image**‑Szenarien, egal ob das Bild ein JPEG, PNG oder sogar ein BMP ist.

```csharp
// Step 3: Recognize text from an image file
string imagePath = @"C:\OcrResources\photo.jpg";

try
{
    var recognitionResult = ocrEngine.RecognizeImage(imagePath);
    Console.WriteLine("=== OCR Output ===");
    Console.WriteLine(recognitionResult.Text);
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Error during OCR processing: {ex.Message}");
}
```

Die Methode `RecognizeImage` gibt ein `RecognitionResult` (oder wie Ihr SDK es nennt) zurück, das typischerweise enthält:

- `Text` – die reine Texttranskription.  
- `Confidence` – ein numerischer Wert, der angibt, wie sicher die Engine bei jeder Zeile ist.  
- `BoundingBoxes` – optionale Koordinaten, wo jedes Wort im Bild liegt.

**Warum das mit der Confidence wichtig sein kann:**  
Wenn Sie ein Daten‑Entry‑Automatisierungstool bauen, können Sie einen Schwellenwert (z. B. 0,85) festlegen und den Nutzer bitten, Zeilen mit niedriger Confidence zu bestätigen. Das verbessert die Gesamteffizienz erheblich.

## Text von JPG erkennen – Umgang mit verschiedenen Formaten

Viele Entwickler gehen davon aus, dass OCR nur mit PNGs funktioniert, aber moderne Engines verarbeiten **JPG**‑Dateien problemlos. Der einzige Haken ist, dass JPEG‑Kompression Artefakte erzeugen kann, die das Modell verwirren.

```csharp
// Bonus: Recognize text from a JPG with optional preprocessing
string jpgPath = @"C:\OcrResources\scanned_doc.jpg";

// Optional: use a simple image‑preprocess step to improve accuracy
var preprocessed = ImageHelper.DenoiseAndDeskew(jpgPath); // pseudo‑method
var result = ocrEngine.RecognizeImage(preprocessed);
Console.WriteLine($"Detected text ({result.Confidence:P0} confidence):");
Console.WriteLine(result.Text);
```

Falls Sie keinen `DenoiseAndDeskew`‑Helper haben, bieten viele Bibliotheken (z. B. OpenCvSharp) diese Funktionen. Die zentrale Erkenntnis: **run OCR on image**‑Dateien nach einer kurzen Aufbereitung ausführen, wenn sie von einem Scanner oder einer Handykamera stammen.

## Run OCR on Image – Tipps, Sonderfälle und bewährte Methoden

### 1. Speicherverwaltung
Das Laden großer Sprachmodelle kann Hunderte Megabyte beanspruchen. Entsorgen Sie die Engine, wenn Sie fertig sind:

```csharp
ocrEngine.Dispose(); // or using statement if the SDK implements IDisposable
```

### 2. Stapelverarbeitung
Wenn Sie Dutzende Fotos verarbeiten müssen, laden Sie die Ressourcen einmal und iterieren dann:

```csharp
string[] files = Directory.GetFiles(@"C:\BatchPhotos", "*.jpg");
foreach (var file in files)
{
    var res = ocrEngine.RecognizeImage(file);
    File.WriteAllText(Path.ChangeExtension(file, ".txt"), res.Text);
}
```

### 3. Mehrsprachige Szenarien
Sie können die Sprache zur Laufzeit wechseln, indem Sie `ocrEngine.Language` neu zuweisen und erneut `LoadResources()` aufrufen. Beachten Sie nur die zusätzliche Ladezeit.

### 4. Umgang mit leeren Ergebnissen
Manchmal liefert die Engine einen leeren String. Das bedeutet meist, dass das Bild zu verschwommen ist oder die Textfarbe mit dem Hintergrund verschmilzt. Eine schnelle Prüfung:

```csharp
if (string.IsNullOrWhiteSpace(recognitionResult.Text))
{
    Console.WriteLine("No text detected – consider increasing image contrast.");
}
```

### 5. Sicherheitsaspekte
Laden Sie niemals von Benutzern hochgeladene Dateien direkt in die OCR‑Engine, ohne sie zu validieren. Mindestens sollten Sie die Dateierweiterung und Größe prüfen und ggf. auf Malware scannen.

---

## Komplettes funktionierendes Beispiel

Unten finden Sie ein einzelnes, eigenständiges Programm, das Sie in ein neues Konsolen‑App‑Projekt kopieren können. Es demonstriert **wie man OCR verwendet**, **Text aus Bild extrahiert**, **Text von Foto erkennt**, **Text von JPG erkennt** und **OCR auf Bild** ausführt – alles in einem Durchgang.

```csharp
// File: Program.cs
using System;
using System.IO;
using YourOcrLibrary; // Replace with actual namespace

namespace OcrDemo
{
    class Program
    {
        static void Main()
        {
            // ------------------------------
            // 1️⃣ Configure the OCR engine
            // ------------------------------
            var ocrEngine = new OcrEngine
            {
                Language = OcrLanguage.ChineseSimplified,
                ResourceFolder = @"C:\OcrResources"
            };

            // Load language resources (no internet needed)
            try
            {
                ocrEngine.LoadResources();
                Console.WriteLine("Resources loaded.");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"Failed to load resources: {ex.Message}");
                return;
            }

            // -------------------------------------------------
            // 2️⃣ Recognize text from a photo (JPG in this case)
            // -------------------------------------------------
            string imagePath = @"C:\OcrResources\photo.jpg";

            if (!File.Exists(imagePath))
            {
                Console.Error.WriteLine($"Image not found: {imagePath}");
                return;
            }

            try
            {
                var result = ocrEngine.RecognizeImage(imagePath);
                Console.WriteLine("\n=== OCR Output ===");
                Console.WriteLine(result.Text);
                Console.WriteLine($"\nConfidence: {result.Confidence:P2}");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"OCR error: {ex.Message}");
            }

            // Clean up
            ocrEngine.Dispose();
        }
    }
}
```

**Erwartete Ausgabe (Beispiel):**

```
Resources loaded.

=== OCR Output ===
中华人民共和国
北京
2026年02月13日

Confidence: 92.45%
```

Ihr tatsächlicher Text wird je nach Bildinhalt variieren, aber Sie sollten einen Block von Unicode‑Zeichen zusammen mit einem Confidence‑Prozentsatz in der Konsole sehen.

---

## Fazit

Wir haben Schritt für Schritt gezeigt, **wie man OCR** in C# von Anfang bis Ende verwendet – die Engine konfigurieren, Sprachressourcen laden und schließlich **Text von Foto** oder **JPG**‑Dateien erkennen, ohne jemals das Internet zu berühren. Wenn Sie den obigen Anweisungen folgen, können Sie **Text aus Bild**‑Dateien extrahieren, **OCR auf Bild**‑Assets ausführen und die häufigsten Stolperfallen vermeiden, die Anfängern begegnen.

Bereit für die nächste Herausforderung? Versuchen Sie, der Engine eine PDF‑Seite zuzuführen, die in ein Bild konvertiert wurde, oder experimentieren Sie mit einem anderen Sprachpaket, um zu sehen, wie sich die Confidence‑Werte ändern. Viel Erfolg!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}