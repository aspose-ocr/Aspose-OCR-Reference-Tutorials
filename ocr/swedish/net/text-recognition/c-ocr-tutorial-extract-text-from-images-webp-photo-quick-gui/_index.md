---
category: general
date: 2026-03-17
description: c# OCR-handledning – upptäck hur du extraherar text från bildfiler, läser
  text från WebP-foton och konverterar bild till text med en enkel OcrEngine.
draft: false
keywords:
- c# OCR tutorial
- extract text from image
- read text from webp
- recognize text from photo
- convert image to text
language: sv
og_description: c# OCR-handledning visar hur du extraherar text från bildfiler, läser
  text från WebP-foton och konverterar bild till text med några rader kod.
og_title: c# OCR-handledning – Extrahera text från bilder på några minuter
tags:
- C#
- OCR
- Image Processing
title: 'c# OCR-handledning: Extrahera text från bilder (WebP, foto) – Snabbguide'
url: /sv/net/text-recognition/c-ocr-tutorial-extract-text-from-images-webp-photo-quick-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# OCR‑handledning – Extrahera text från bilder (WebP, foto)

Har du någonsin behövt **extrahera text från bild**‑filer men varit osäker på var du ska börja i C#? Kanske har du en WebP‑skärmdump, en JPEG‑kvitto eller en skannad PDF‑sida och du bara vill ha orden inuti. I den här **c# OCR‑handledningen** går vi igenom ett komplett, färdigt‑att‑köra exempel som läser text från ett foto, hanterar WebP och andra moderna format, och konverterar bilden till ren text – allt på några få rader.

**Vad får du ut av det?** Du kommer kunna omvandla vilken bild av text som helst till sökbara strängar, mata in dem i databaser, eller skicka dem till efterföljande AI‑pipelines. Ingen magi, bara en robust OCR‑motor, några .NET‑API:er och tydliga förklaringar av “varför” bakom varje steg.

## Vad du behöver

- **.NET 6 SDK** (eller senare). Koden nedan kompileras med .NET 6+ och körs på Windows, Linux eller macOS.
- **Visual Studio 2022** eller någon annan editor du föredrar (VS Code fungerar bra).
- NuGet‑paketet **`Microsoft.Windows.SDK.Contracts`** (tillhandahåller `Windows.Media.Ocr`). Installera med:

```bash
dotnet add package Microsoft.Windows.SDK.Contracts
```

- En bildfil du vill bearbeta – i den här handledningen använder vi ett **WebP**‑foto med namnet `photo.webp` placerat i en mapp som heter `YOUR_DIRECTORY`.

> Proffstips: Om du är på en icke‑Windows‑plattform kan du byta ut `OcrEngine` mot ett plattformsoberoende bibliotek som **Tesseract**. Den omgivande koden förblir i stort sett densamma.

## Steg 1: Skapa ett C# OCR‑handledningsprojekt

Först, skapa en ny konsolapp. Öppna en terminal och kör:

```bash
dotnet new console -n OcrDemo
cd OcrDemo
```

Lägg till det nödvändiga paketet (som visas ovan) och öppna projektet i din IDE. Denna grundstruktur ger oss en ren start för **c# OCR‑handledningen**.

## Steg 2: Importera namnrymder och förbered bilden

Vi behöver några `using`‑direktiv så kompilatorn vet var den ska hitta `OcrEngine`, `SoftwareBitmap` och hjälpfunktioner för bildladdning.

```csharp
using System;
using System.IO;
using Windows.Graphics.Imaging;
using Windows.Media.Ocr;
using Windows.Storage.Streams;
```

> **Varför dessa namnrymder?**  
> `Windows.Media.Ocr` innehåller `OcrEngine`‑klassen som faktiskt utför igenkänningen. `Windows.Graphics.Imaging` låter oss avkoda bilden (inklusive WebP) till en `SoftwareBitmap` som motorn kan förstå. Hjälpfunktionerna `System.IO` och `Windows.Storage.Streams` gör filinläsning smidig.

Läs nu in bilden. Den inbyggda avkodaren kan hantera WebP, HEIF, PNG, JPEG och mer, så du kan **läsa text från WebP** utan extra plugins.

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

> **Edge case:** Om din bild redan är svart‑vit kan du hoppa över konverteringssteget. Gråskalakonverteringen ger en liten prestandaförbättring och förbättrar ofta igenkänning på brusiga foton.

## Steg 3: Kör OCR‑motorn – känna igen text från foto

Här är kärnan i **c# OCR‑handledningen**. Vi skapar en instans av `OcrEngine`, matar in bitmapen och hämtar den igenkända texten.

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

**Vad händer?**  
- `TryCreateFromUserProfileLanguages()` väljer de språk som din Windows‑användarprofil är inställd på, vilket vanligtvis täcker engelska, spanska osv. Om du behöver ett specifikt språk, använd `OcrEngine.TryCreateFromLanguage(new Language("fr-FR"))`.  
- `RecognizeAsync` utför det tunga arbetet på en bakgrundstråd och returnerar ett `OcrResult` som innehåller den råa strängen, ordens avgränsningsrutor och förtroendesiffror.  
- Till sist skriver vi ut `ocrResult.Text`, vilket ger dig resultatet **convert image to text** som du kan skicka vidare.

## Steg 4: Fullt, körbart exempel

När vi sätter ihop allt, här är ett fristående program som du kan kopiera och klistra in i `Program.cs`. Det kompileras, körs och skriver ut texten som extraherats från `photo.webp`.

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

### Förväntad utdata

Om `photo.webp` innehåller meningen “Hello, world! This is a test.” kommer du att se något liknande:

```
--- OCR Output ---
Hello, world!
This is a test.
--- End of Output ---
```

De exakta radbrytena beror på layouten i källbilden, men resultatet **extract text from image** kommer alltid att vara en ren sträng som du kan manipulera vidare.

## Vanliga frågor & edge cases

### Fungerar detta med andra bildformat?

Absolut. Avkodaren som används (`BitmapDecoder`) upptäcker automatiskt JPEG, PNG, BMP, GIF, **WebP**, HEIF och mer. Så du kan **read text from WebP**, JPEG eller till och med en TIFF utan att ändra koden.

### Vad händer om OCR‑motorn returnerar låg förtroendegrad?

Du kan inspektera `ocrResult.Lines` och varje `OcrWord` för ett `ConfidenceScore`. Om poängen är under en tröskel (t.ex. 0,6), överväg:

- Förbehandla bilden (öka kontrast, skärpa, räta upp).  
- Använda en bild med högre upplösning.  
- Byta till ett dedikerat bibliotek som **Tesseract** för flerspråkigt stöd.

### Hur hanterar man flera språk i samma bild?

Skapa separata `OcrEngine`‑instanser för varje språk och kör dem sekventiellt, eller använd ett bibliotek som stödjer blandad språkdetektering. För den inbyggda motorn kan du skicka ett `Language`‑objekt:

```csharp
var spanishEngine = OcrEngine.TryCreateFromLanguage(new Language("es-ES"));
```

### Kan jag köra detta på Linux/macOS?

`Windows.Media.Ocr`‑API:et är endast för Windows. På icke‑Windows‑plattformar ersätter du OCR‑delen med **Tesseract** (via `Tesseract.Net.SDK`). Laddnings‑ och förbehandlingskoden förblir identisk, så resten av denna **c# OCR‑handledning** gäller fortfarande.

## Proffstips för bättre noggrannhet

- **Ändra storlek** på stora bilder till maximalt 2000 px på den längsta sidan – OCR‑motorer fungerar snabbare på måttliga storlekar.  
- **Denoisa** med en enkel Gaussisk oskärpa om fotot är kornigt.  
- **Räta upp** bitmapen om texten inte är helt horisontell; `SoftwareBitmap` kan roteras innan den skickas till `OcrEngine`.  
- **Cacha** `OcrEngine`‑instansen om du bearbetar många bilder i en batch; att skapa den upprepade gånger ger extra overhead.

## Relaterade ämnen att utforska

- **Convert image to text** med **Tesseract** för plattformsoberoende projekt.  
- **Extract text from PDF** genom att rendera varje sida till en bild först.  
- **Batch OCR**

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}