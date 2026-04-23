---
category: general
date: 2026-03-17
description: c# OCR-tutorial – ontdek hoe je tekst uit afbeeldingsbestanden kunt extraheren,
  tekst uit WebP-foto's kunt lezen en een afbeelding naar tekst kunt omzetten met
  een eenvoudige OcrEngine.
draft: false
keywords:
- c# OCR tutorial
- extract text from image
- read text from webp
- recognize text from photo
- convert image to text
language: nl
og_description: c# OCR‑tutorial laat zien hoe je tekst uit afbeeldingsbestanden kunt
  extraheren, tekst uit WebP‑foto’s kunt lezen en een afbeelding naar tekst kunt omzetten
  met een paar regels code.
og_title: c# OCR‑tutorial – Haal tekst uit afbeeldingen in enkele minuten
tags:
- C#
- OCR
- Image Processing
title: 'c# OCR-tutorial: Tekst extraheren uit afbeeldingen (WebP, foto) – Snelle gids'
url: /nl/net/text-recognition/c-ocr-tutorial-extract-text-from-images-webp-photo-quick-gui/
---

for any other code blocks: placeholders only.

Check for any bold phrases: we translated accordingly.

Now produce final content with same structure.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# OCR tutorial – Tekst extraheren uit afbeeldingen (WebP, foto)

Heb je ooit **tekst uit afbeelding** bestanden moeten extraheren maar wist je niet waar te beginnen in C#? Misschien heb je een WebP screenshot, een JPEG van een bon, of een gescande PDF-pagina en wil je gewoon de woorden erin. In deze **c# OCR tutorial** lopen we een compleet, kant‑klaar voorbeeld door dat tekst leest uit een foto, WebP en andere moderne formaten verwerkt, en de afbeelding converteert naar platte tekst—alles in een handvol regels.

**Wat is het voordeel?** Je kunt elke foto van tekst omzetten in doorzoekbare strings, ze in databases invoeren, of ze doorgeven aan downstream AI‑pijplijnen. Geen magie, gewoon een solide OCR‑engine, een paar .NET‑API’s, en duidelijke uitleg over het “waarom” achter elke stap.

## Wat je nodig hebt

- **.NET 6 SDK** (of later). De onderstaande code compileert met .NET 6+ en draait op Windows, Linux of macOS.
- **Visual Studio 2022** of een editor naar keuze (VS Code werkt prima).
- Het **`Microsoft.Windows.SDK.Contracts`** NuGet‑pakket (biedt `Windows.Media.Ocr`). Installeer met:

```bash
dotnet add package Microsoft.Windows.SDK.Contracts
```

- Een afbeeldingsbestand dat je wilt verwerken – voor deze tutorial gebruiken we een **WebP** foto genaamd `photo.webp` geplaatst in een map genaamd `YOUR_DIRECTORY`.

> Pro tip: Als je op een non‑Windows platform werkt, kun je de `OcrEngine` vervangen door een cross‑platform bibliotheek zoals **Tesseract**. De omringende code blijft vrijwel hetzelfde.

## Stap 1: Een C# OCR‑tutorialproject opzetten

Eerst, maak een nieuwe console‑app. Open een terminal en voer uit:

```bash
dotnet new console -n OcrDemo
cd OcrDemo
```

Voeg het vereiste pakket toe (zoals hierboven getoond) en open het project in je IDE. Deze scaffolding geeft ons een schone basis voor de **c# OCR tutorial**.

## Stap 2: Namespaces importeren en de afbeelding voorbereiden

We hebben een paar `using`‑directieven nodig zodat de compiler weet waar `OcrEngine`, `SoftwareBitmap` en image‑loading helpers te vinden zijn.

```csharp
using System;
using System.IO;
using Windows.Graphics.Imaging;
using Windows.Media.Ocr;
using Windows.Storage.Streams;
```

> **Waarom deze namespaces?**  
> `Windows.Media.Ocr` bevat de `OcrEngine`‑klasse die de herkenning daadwerkelijk uitvoert. `Windows.Graphics.Imaging` laat ons de afbeelding (inclusief WebP) decoderen naar een `SoftwareBitmap` die de engine kan begrijpen. De helpers `System.IO` en `Windows.Storage.Streams` maken het laden van bestanden moeiteloos.

Laad nu de afbeelding. De ingebouwde decoder kan WebP, HEIF, PNG, JPEG en meer aan, zodat je **tekst uit WebP** kunt lezen zonder extra plugins.

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

> **Randgeval:** Als je afbeelding al zwart‑wit is, kun je de conversiestap overslaan. De grijstinten‑conversie levert een kleine prestatie‑winst op en verbetert vaak de herkenning op ruisende foto’s.

## Stap 3: De OCR‑engine uitvoeren – Tekst herkennen uit foto

Hier is het hart van de **c# OCR tutorial**. We maken een instantie van `OcrEngine`, voeren de bitmap in, en halen de herkende tekst eruit.

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

**Wat gebeurt er?**  
- `TryCreateFromUserProfileLanguages()` kiest de taal/talen die in je Windows‑gebruikersprofiel zijn ingesteld, wat meestal Engels, Spaans, enz. omvat. Als je een specifieke taal nodig hebt, gebruik dan `OcrEngine.TryCreateFromLanguage(new Language("fr-FR"))`.  
- `RecognizeAsync` voert het zware werk uit op een achtergrondthread en retourneert een `OcrResult` die de ruwe string, woord‑bounding‑boxes en confidence‑scores bevat.  
- Ten slotte printen we `ocrResult.Text`, waardoor je het **afbeelding naar tekst converteren** resultaat krijgt dat je elders kunt gebruiken.

## Stap 4: Volledig, uitvoerbaar voorbeeld

Alles bij elkaar, hier is een zelfstandige programma dat je kunt copy‑pasten in `Program.cs`. Het compileert, draait, en print de tekst die is geëxtraheerd uit `photo.webp`.

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

### Verwachte uitvoer

Als `photo.webp` de zin “Hello, world! This is a test.” bevat, zie je iets als:

```
--- OCR Output ---
Hello, world!
This is a test.
--- End of Output ---
```

De exacte regeleinden hangen af van de lay-out van de bronafbeelding, maar het **tekst uit afbeelding extraheren** resultaat zal altijd een platte string zijn die je verder kunt manipuleren.

## Veelgestelde vragen & randgevallen

### Werkt dit met andere afbeeldingsformaten?

Absoluut. De gebruikte decoder (`BitmapDecoder`) detecteert automatisch JPEG, PNG, BMP, GIF, **WebP**, HEIF en meer. Dus je kunt **tekst uit WebP** lezen, JPEG, of zelfs een TIFF zonder de code te wijzigen.

### Wat als de OCR‑engine lage confidence retourneert?

Je kunt `ocrResult.Lines` en elk `OcrWord` inspecteren voor een `ConfidenceScore`. Als de score onder een drempel ligt (bijv. 0.6), overweeg dan:

- De afbeelding voor‑verwerken (contrast verhogen, verscherpen, rechtzetten).
- Een bronafbeelding met hogere resolutie gebruiken.
- Overschakelen naar een speciale bibliotheek zoals **Tesseract** voor meertalige ondersteuning.

### Hoe meerdere talen in dezelfde afbeelding te verwerken?

Maak aparte `OcrEngine`‑instanties voor elke taal en voer ze opeenvolgend uit, of gebruik een bibliotheek die detectie van gemengde talen ondersteunt. Voor de ingebouwde engine kun je een `Language`‑object doorgeven:

```csharp
var spanishEngine = OcrEngine.TryCreateFromLanguage(new Language("es-ES"));
```

### Kan ik dit draaien op Linux/macOS?

De `Windows.Media.Ocr`‑API is alleen voor Windows. Op non‑Windows platforms vervang je het OCR‑gedeelte door **Tesseract** (via `Tesseract.Net.SDK`). De laad‑ en voorverwerkingscode blijft identiek, dus de rest van deze **c# OCR tutorial** blijft van toepassing.

## Pro‑tips voor betere nauwkeurigheid

- **Resize** grote afbeeldingen naar maximaal 2000 px aan de langste zijde – OCR‑engines werken sneller op matige groottes.
- **Denoise** met een eenvoudige Gaussian blur als de foto korrelig is.
- **Deskew** de bitmap als de tekst niet perfect horizontaal staat; `SoftwareBitmap` kan worden geroteerd voordat deze aan `OcrEngine` wordt doorgegeven.
- **Cache** de `OcrEngine`‑instantie als je veel afbeeldingen in een batch verwerkt; herhaaldelijk aanmaken voegt overhead toe.

## Gerelateerde onderwerpen om te verkennen

- **Afbeelding naar tekst converteren** met **Tesseract** voor cross‑platform projecten.
- **Tekst extraheren uit PDF** door elke pagina eerst naar een afbeelding te renderen.
- **Batch OCR**

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}