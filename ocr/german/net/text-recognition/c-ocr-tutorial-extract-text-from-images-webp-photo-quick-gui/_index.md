---
category: general
date: 2026-03-17
description: c# OCR‑Tutorial – entdecken Sie, wie Sie Text aus Bilddateien extrahieren,
  Text aus WebP‑Fotos lesen und Bilder mit einem einfachen OcrEngine in Text umwandeln.
draft: false
keywords:
- c# OCR tutorial
- extract text from image
- read text from webp
- recognize text from photo
- convert image to text
language: de
og_description: Das C#‑OCR‑Tutorial zeigt Ihnen, wie Sie Text aus Bilddateien extrahieren,
  Text aus WebP‑Fotos lesen und Bilder mit wenigen Codezeilen in Text umwandeln.
og_title: c# OCR‑Tutorial – Text aus Bildern in Minuten extrahieren
tags:
- C#
- OCR
- Image Processing
title: 'c# OCR‑Tutorial: Text aus Bildern extrahieren (WebP, Foto) – Schnellleitfaden'
url: /de/net/text-recognition/c-ocr-tutorial-extract-text-from-images-webp-photo-quick-gui/
---

German, but maybe should keep English. Let's revert to original bold phrase unchanged: **convert image to text**. So keep that.

Similarly **extract text from image** earlier we translated; maybe keep original phrase. Keep original bold phrase unchanged.

Thus revert those.

Now produce final content.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# OCR tutorial – Text aus Bildern extrahieren (WebP, Foto)

Haben Sie jemals **extract text from image**‑Dateien extrahieren müssen, wussten aber nicht, wo Sie in C# anfangen sollen? Vielleicht haben Sie einen WebP‑Screenshot, ein JPEG einer Quittung oder eine gescannte PDF‑Seite und möchten einfach die darin enthaltenen Wörter. In diesem **c# OCR tutorial** führen wir Sie durch ein komplettes, sofort ausführbares Beispiel, das Text aus einem Foto liest, WebP und andere moderne Formate verarbeitet und das Bild in Klartext umwandelt – alles in wenigen Zeilen.

**What’s the payoff?** Sie können jedes Bild mit Text in durchsuchbare Zeichenketten umwandeln, in Datenbanken einspeisen oder an nachgelagerte KI‑Pipelines weitergeben. Kein Zauber, nur eine solide OCR‑Engine, ein paar .NET‑APIs und klare Erklärungen zum „Warum“ jedes Schrittes.

## What You’ll Need

- **.NET 6 SDK** (oder neuer). Der untenstehende Code kompiliert mit .NET 6+ und läuft unter Windows, Linux oder macOS.
- **Visual Studio 2022** oder ein beliebiger Editor Ihrer Wahl (VS Code funktioniert ebenfalls).
- Das **`Microsoft.Windows.SDK.Contracts`** NuGet‑Paket (stellt `Windows.Media.Ocr` bereit). Installieren Sie mit:

```bash
dotnet add package Microsoft.Windows.SDK.Contracts
```

- Eine Bilddatei, die Sie verarbeiten möchten – für dieses Tutorial verwenden wir ein **WebP**‑Foto namens `photo.webp`, das in einem Ordner namens `YOUR_DIRECTORY` liegt.

> Pro tip: Wenn Sie sich auf einer Nicht‑Windows‑Plattform befinden, können Sie die `OcrEngine` durch eine plattformübergreifende Bibliothek wie **Tesseract** ersetzen. Der umgebende Code bleibt praktisch unverändert.

## Step 1: Set Up a C# OCR Tutorial Project

Zuerst erstellen Sie eine neue Konsolen‑App. Öffnen Sie ein Terminal und führen Sie aus:

```bash
dotnet new console -n OcrDemo
cd OcrDemo
```

Fügen Sie das erforderliche Paket hinzu (wie oben gezeigt) und öffnen Sie das Projekt in Ihrer IDE. Dieses Gerüst gibt uns eine saubere Basis für das **c# OCR tutorial**.

## Step 2: Import Namespaces and Prepare the Image

Wir benötigen ein paar `using`‑Direktiven, damit der Compiler weiß, wo er `OcrEngine`, `SoftwareBitmap` und Bild‑Lade‑Hilfsfunktionen findet.

```csharp
using System;
using System.IO;
using Windows.Graphics.Imaging;
using Windows.Media.Ocr;
using Windows.Storage.Streams;
```

> **Why these namespaces?**  
> `Windows.Media.Ocr` enthält die Klasse `OcrEngine`, die die eigentliche Erkennung durchführt. `Windows.Graphics.Imaging` ermöglicht das Dekodieren des Bildes (einschließlich WebP) in ein `SoftwareBitmap`, das die Engine verstehen kann. Die Hilfsfunktionen aus `System.IO` und `Windows.Storage.Streams` erleichtern das Laden von Dateien.

Jetzt laden wir das Bild. Der integrierte Decoder kann WebP, HEIF, PNG, JPEG und mehr verarbeiten, sodass Sie **read text from WebP** ohne zusätzliche Plugins lesen können.

```csharp
// Step 2: Load the image file into a SoftwareBitmap
string imagePath = Path.Combine("YOUR_DIRECTORY", "photo.webp");

// Open the file as a random access stream
using (IRandomAccessStream stream = File.OpenRead(imagePath).AsRandomAccessStream())
{
    // Decode the image (auto-detects format)
    BitmapDecoder decoder = await BitmapDecoder.CreateAsync(stream);
    SoftwareBitmap bitmap = await decoder.GetSoftwareBitmapAsync();
    
    // Optional: Convert to grayscale for better OCR accuracy
    SoftwareBitmap grayBitmap = SoftwareBitmap.Convert(bitmap, BitmapPixelFormat.Gray8);
    
    // Pass the bitmap to the next step
    await RecognizeTextAsync(grayBitmap);
}
```

> **Edge case:** Wenn Ihr Bild bereits schwarz‑weiß ist, können Sie den Konvertierungsschritt überspringen. Die Graustufen‑Umwandlung ist ein kleiner Performance‑Gewinn und verbessert oft die Erkennung bei verrauschten Fotos.

## Step 3: Run the OCR Engine – Recognize Text from Photo

Hier ist das Herzstück des **c# OCR tutorial**. Wir erstellen eine Instanz von `OcrEngine`, übergeben ihr das Bitmap und holen den erkannten Text heraus.

```csharp
static async Task RecognizeTextAsync(SoftwareBitmap bitmap)
{
    // Step 3: Create the OCR engine instance – it automatically picks the best language
    OcrEngine ocrEngine = OcrEngine.TryCreateFromUserProfileLanguages();

    if (ocrEngine == null)
    {
        Console.WriteLine("❌ No OCR engine available for the current language.");
        return;
    }

    // Perform recognition
    OcrResult ocrResult = await ocrEngine.RecognizeAsync(bitmap);

    // Step 4: Display the extracted text – this is the “convert image to text” part
    Console.WriteLine("📝 Recognized text:");
    Console.WriteLine(ocrResult.Text);
}
```

**What’s happening?**  
- `TryCreateFromUserProfileLanguages()` wählt die Sprache(n) aus, die in Ihrem Windows‑Benutzerprofil eingestellt sind, was in der Regel Englisch, Spanisch usw. abdeckt. Wenn Sie eine bestimmte Sprache benötigen, verwenden Sie `OcrEngine.TryCreateFromLanguage(new Language("fr-FR"))`.
- `RecognizeAsync` erledigt die schwere Arbeit in einem Hintergrund‑Thread und gibt ein `OcrResult` zurück, das den Roh‑String, Wort‑Bounding‑Boxes und Vertrauenswerte enthält.
- Schließlich geben wir `ocrResult.Text` aus, was Ihnen das Ergebnis **convert image to text** liefert, das Sie weiterverwenden können.

## Step 4: Full, Runnable Example

Alles zusammengefügt, hier ein eigenständiges Programm, das Sie in `Program.cs` einfügen können. Es kompiliert, läuft und gibt den aus `photo.webp` extrahierten Text aus.

```csharp
// Program.cs – Complete c# OCR tutorial example
using System;
using System.IO;
using System.Threading.Tasks;
using Windows.Graphics.Imaging;
using Windows.Media.Ocr;
using Windows.Storage.Streams;

class Program
{
    static async Task Main(string[] args)
    {
        // Replace with your actual directory and file name
        string imagePath = Path.Combine("YOUR_DIRECTORY", "photo.webp");

        if (!File.Exists(imagePath))
        {
            Console.WriteLine($"❗ Image not found: {imagePath}");
            return;
        }

        // Load and optionally preprocess the image
        using (IRandomAccessStream stream = File.OpenRead(imagePath).AsRandomAccessStream())
        {
            BitmapDecoder decoder = await BitmapDecoder.CreateAsync(stream);
            SoftwareBitmap bitmap = await decoder.GetSoftwareBitmapAsync();

            // Convert to grayscale – improves OCR accuracy on many photos
            SoftwareBitmap grayBitmap = SoftwareBitmap.Convert(bitmap, BitmapPixelFormat.Gray8);

            // Run OCR
            await RecognizeTextAsync(grayBitmap);
        }
    }

    static async Task RecognizeTextAsync(SoftwareBitmap bitmap)
    {
        // Create OCR engine (auto‑detect language)
        OcrEngine ocrEngine = OcrEngine.TryCreateFromUserProfileLanguages();

        if (ocrEngine == null)
        {
            Console.WriteLine("❌ Unable to create OCR engine. Ensure language packs are installed.");
            return;
        }

        // Perform recognition
        OcrResult result = await ocrEngine.RecognizeAsync(bitmap);

        // Output the extracted text
        Console.WriteLine("\n--- OCR Output ---");
        Console.WriteLine(result.Text);
        Console.WriteLine("--- End of Output ---\n");
    }
}
```

### Expected Output

Wenn `photo.webp` den Satz „Hello, world! This is a test.“ enthält, sehen Sie etwa Folgendes:

```
--- OCR Output ---
Hello, world!
This is a test.
--- End of Output ---
```

Die genauen Zeilenumbrüche hängen vom Layout des Quellbildes ab, aber das Ergebnis **extract text from image** wird immer ein Klartext‑String sein, den Sie weiter verarbeiten können.

## Common Questions & Edge Cases

### Does this work with other image formats?

Absolut. Der verwendete Decoder (`BitmapDecoder`) erkennt JPEG, PNG, BMP, GIF, **WebP**, HEIF und mehr automatisch. So können Sie **read text from WebP**, JPEG oder sogar einem TIFF lesen, ohne den Code zu ändern.

### What if the OCR engine returns low confidence?

Sie können `ocrResult.Lines` und jedes `OcrWord` auf einen `ConfidenceScore` prüfen. Wenn der Wert unter einem Schwellenwert liegt (z. B. 0,6), sollten Sie erwägen:

- Das Bild vorzuverarbeiten (Kontrast erhöhen, schärfen, entzerren).
- Ein Bild mit höherer Auflösung zu verwenden.
- Auf eine dedizierte Bibliothek wie **Tesseract** für mehrsprachige Unterstützung umzusteigen.

### How to handle multiple languages in the same image?

Erstellen Sie separate `OcrEngine`‑Instanzen für jede Sprache und führen Sie sie nacheinander aus, oder verwenden Sie eine Bibliothek, die die Erkennung gemischter Sprachen unterstützt. Für die eingebaute Engine können Sie ein `Language`‑Objekt übergeben:

```csharp
var spanishEngine = OcrEngine.TryCreateFromLanguage(new Language("es-ES"));
```

### Can I run this on Linux/macOS?

Die `Windows.Media.Ocr`‑API ist nur für Windows verfügbar. Auf Nicht‑Windows‑Plattformen ersetzen Sie den OCR‑Abschnitt durch **Tesseract** (via `Tesseract.Net.SDK`). Der Lade‑ und Vorverarbeitungscode bleibt identisch, sodass der Rest dieses **c# OCR tutorial** weiterhin gilt.

## Pro Tips for Better Accuracy

- **Resize** große Bilder auf maximal 2000 px auf der längsten Seite verkleinern – OCR‑Engines arbeiten schneller bei moderaten Größen.
- **Denoise**: Verwenden Sie einen einfachen Gauß‑Weichzeichner, wenn das Foto körnig ist.
- **Deskew**: Drehen Sie das Bitmap, wenn der Text nicht perfekt horizontal ist; `SoftwareBitmap` kann vor dem Übergeben an `OcrEngine` rotiert werden.
- **Cache** die `OcrEngine`‑Instanz, wenn Sie viele Bilder stapelweise verarbeiten; das wiederholte Erzeugen verursacht zusätzlichen Aufwand.

## Related Topics to Explore

- **Convert image to text** mit **Tesseract** für plattformübergreifende Projekte.
- **Extract text from PDF** indem Sie jede Seite zuerst in ein Bild rendern.
- **Batch OCR**

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}