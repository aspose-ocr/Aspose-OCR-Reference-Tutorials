---
category: general
date: 2026-02-20
description: c# OCR-handledning som visar hur du extraherar text från en bild, känner
  igen text från PNG och konverterar bilden till text på bara några rader kod.
draft: false
keywords:
- c# ocr tutorial
- extract text from image
- recognize text from png
- convert image to text
- how to extract text
language: sv
og_description: C# OCR-handledning som guidar dig genom att extrahera text från bildfiler,
  känna igen text från PNG och konvertera bilder till text med Aspose.OCR.
og_title: c# ocr handledning – Snabbguide för att extrahera text från bilder
tags:
- OCR
- C#
- Aspose
title: c# OCR-handledning – Extrahera text från bilder med Aspose.OCR
url: /sv/net/text-recognition/c-ocr-tutorial-extract-text-from-images-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr tutorial – Extrahera text från bilder med Aspose.OCR

Har du någonsin behövt ett **c# ocr tutorial** som faktiskt fungerar på en riktig PNG‑fil? Du är inte ensam. I många projekt—tänk fakturaskanning, kvittoarkivering eller enkel skärmdumpsanalys—stöter utvecklare på problem när de försöker **extrahera text från bild**‑filer utan ett pålitligt bibliotek.  

Den goda nyheten är att Aspose.OCR gör hela processen enkel som en barnlek. I den här guiden går vi igenom ett komplett, körbart exempel som visar **hur man extraherar text** från en PNG, förklarar *varför* varje rad är viktig, och berör även edge‑cases som licensiering och bildförbehandling. I slutet kommer du att kunna **läsa igenom text från png**‑filer och **konvertera bild till text** med bara några få C#‑satser.

## Vad den här handledningen täcker

- Ställa in Aspose.OCR‑motorn i en .NET‑konsolapp.  
- Ladda en PNG (eller någon annan stödd bitmap) från disk.  
- Köra OCR och skriva ut resultatet till konsolen.  
- Valfri licensiering, felhantering och prestandatips.  

Inga externa tjänster, ingen dold magi—bara ren C#‑kod som du kan kopiera‑klistra och köra. Om du någonsin har funderat **hur man extraherar text** från ett skannat dokument, häng kvar; vi kommer att svara på det och några “what if”‑frågor längs vägen.

## Förutsättningar

- .NET 6.0 SDK eller senare (koden fungerar också på .NET Framework 4.7+).  
- Visual Studio 2022 (eller någon annan editor du föredrar).  
- Ett gratis eller betalt Aspose.OCR för .NET NuGet‑paket.  
- En bildfil med namnet `sample.png` placerad i en mapp du kan referera till.  

Det är allt—inga andra tredjepartsverktyg behövs.

## c# OCR‑handledning: Installera Aspose.OCR

Först och främst: du behöver Aspose.OCR‑biblioteket. Öppna din terminal i projektmappen och kör:

```bash
dotnet add package Aspose.OCR
```

Det här hämtar den senaste stabila versionen och lägger till de nödvändiga DLL‑referenserna. Om du har en licensfil (`Aspose.OCR.lic`), ha den tillgänglig; annars fungerar gratisprovet, men med vattenstämplar på OCR‑resultatet.

### Varför en licens är viktig

Utan en licens körs motorn i evalueringsläge, vilket lägger in en “Powered by Aspose”‑rad i utskriften för vissa språk. För produktionskod vill du anropa `SetLicense` tidigt, som visas i koden nedan. Det är ett enradigt anrop, men det tar bort vattenstämpeln och låser upp full hastighetsbehandling.

## Extrahera text från bild med Aspose.OCR

Nu dyker vi ner i den faktiska OCR‑koden. Nedan är ett **komplett, fristående** program som du kan kompilera och köra omedelbart.

```csharp
using System;
using System.Drawing;          // Needed for Image class
using Aspose.OCR;               // Core OCR namespace
using Aspose.OCR.Models;       // For OCR settings (optional)

class LicenseCheck
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Initialize the OCR engine
        // -------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine();

        // -------------------------------------------------
        // Step 2 (Optional): Apply your Aspose.OCR license
        // -------------------------------------------------
        // Uncomment and set the correct path if you have a license file.
        // ocrEngine.SetLicense(@"C:\MyLicenses\Aspose.OCR.lic");

        // -------------------------------------------------
        // Step 3: Load the image you want to process
        // -------------------------------------------------
        // You can use any supported format (png, jpg, bmp, tiff, etc.)
        string imagePath = @"C:\Images\sample.png";
        Image inputImage = Image.FromFile(imagePath);

        // -------------------------------------------------
        // Step 4: Recognize text from the loaded image
        // -------------------------------------------------
        // The Recognize method returns a plain string.
        string recognizedText = ocrEngine.Recognize(inputImage);

        // -------------------------------------------------
        // Step 5: Display the extracted text
        // -------------------------------------------------
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(recognizedText);
    }
}
```

**Vad händer här?**  

1. **Motor‑skapande** – `OcrEngine` är huvudinkörningspunkten; den laddar språkdatan internt.  
2. **Licensladdning** – valfritt men rekommenderat; du pekar helt enkelt på din `.lic`‑fil.  
3. **Bildladdning** – `Image.FromFile` fungerar för alla bitmap‑format; vi använder en PNG eftersom den bevarar förlustfri kvalitet, vilket är avgörande för OCR‑noggrannhet.  
4. **Identifiering** – `ocrEngine.Recognize` gör allt tungt arbete och returnerar en sträng som innehåller de upptäckta tecknen.  
5. **Utdata** – vi skriver resultatet till konsolen, men du kan enkelt skicka det till en fil, databas eller UI‑kontroll.

### Förväntad utdata

Om `sample.png` innehåller texten “Hello World”, kommer konsolen att visa:

```
=== OCR Result ===
Hello World
```

Om bilden är suddig eller innehåller icke‑latinska tecken kan utskriften innehålla förvrängda symboler. Det är då förbehandling (kontrastjustering, binarisering) kommer in i bilden—det behandlas i nästa avsnitt.

## Läs igenom text från PNG‑filer – Tips & tricks

PNG är ett populärt format eftersom det lagrar pixlar utan komprimeringsartefakter. Ändå är inte alla PNG‑filer lika. Här är några praktiska tips som kan vara användbara:

- **Upplösning är viktig** – Sikta på minst 300 dpi. Lägre kan leda till missade tecken.  
- **Färg vs. Gråskala** – Att konvertera en färgad PNG till gråskala innan OCR kan förbättra hastigheten utan att försämra noggrannheten.  
- **Brusreducering** – Små fläckar förvirrar ofta motorn; ett enkelt medianfilter kan hjälpa.

Nedan är ett snabbt kodexempel som visar hur man förbehandlar en bild innan den matas till Aspose.OCR:

```csharp
using System.Drawing.Imaging;

// Convert to grayscale
Bitmap grayBitmap = new Bitmap(inputImage.Width, inputImage.Height);
using (Graphics g = Graphics.FromImage(grayBitmap))
{
    var colorMatrix = new ColorMatrix(
        new float[][]{
            new float[]{0.3f,0.3f,0.3f,0,0},
            new float[]{0.59f,0.59f,0.59f,0,0},
            new float[]{0.11f,0.11f,0.11f,0,0},
            new float[]{0,0,0,1,0},
            new float[]{0,0,0,0,1}});
    var attributes = new ImageAttributes();
    attributes.SetColorMatrix(colorMatrix);
    g.DrawImage(inputImage, new Rectangle(0,0,grayBitmap.Width,grayBitmap.Height),
                0,0,inputImage.Width,inputImage.Height, GraphicsUnit.Pixel, attributes);
}

// Optional: Apply a simple binary threshold
Bitmap binBitmap = new Bitmap(grayBitmap.Width, grayBitmap.Height);
for (int y = 0; y < grayBitmap.Height; y++)
{
    for (int x = 0; x < grayBitmap.Width; x++)
    {
        Color pixel = grayBitmap.GetPixel(x, y);
        int bw = pixel.R < 128 ? 0 : 255; // threshold at 128
        binBitmap.SetPixel(x, y, Color.FromArgb(bw, bw, bw));
    }
}

// Now run OCR on the cleaned bitmap
string cleanedText = ocrEngine.Recognize(binBitmap);
Console.WriteLine(cleanedText);
```

**Pro‑tips:** Om du bearbetar dussintals bilder, skapa en enda `OcrEngine` och återanvänd den. Att skapa en ny motor per bild ger onödig overhead.

## Konvertera bild till text – Avancerade alternativ

Aspose.OCR är inte begränsat till enkel textutvinning. Du kan be den returnera **strukturerad data** (som ordens avgränsningsrutor) eller ange **språktips** för att förbättra noggrannheten i flerspråkiga dokument.

```csharp
// Set language to English + Spanish (ISO codes)
ocrEngine.Language = Language.English | Language.Spanish;

// Request detailed OCR result
OcrResult result = ocrEngine.RecognizeImage(inputImage, OcrOptions.DetectTextBlocks);

// Iterate over detected words
foreach (var word in result.Words)
{
    Console.WriteLine($"{word.Text} (x:{word.Bounds.X}, y:{word.Bounds.Y})");
}
```

`OcrResult`‑objektet ger dig varje ords koordinater, vilket är praktiskt för att markera text i ett UI eller för efterbehandling (t.ex. rensa känslig information).

## Hur man extraherar text i verkliga scenarier

Låt oss ta upp några “what if”‑frågor som ofta dyker upp i produktionsmiljöer.

### Vad händer om bilden är en PDF‑sida?

Aspose.OCR kan läsa PDF‑filer direkt, men du behöver Aspose.PDF‑biblioteket för att rasterisera varje sida till en bild först. Arbetsflödet är:

1. Läs in PDF med `Aspose.Pdf.Document`.  
2. Konvertera en sida till en bitmap (`PdfConverter`).  
3. Mata bitmapen till `OcrEngine.Recognize`.

### Vad händer om OCR‑resultatet innehåller skräptecken?

Vanliga orsaker är låg upplösning, överdrivet brus eller ej stödda teckensnitt. Prova:

- Skala upp bilden (`Bitmap`‑ändring av storlek).  
- Applicera ett skärpande filter.  
- Ange rätt språk (som visat ovan).

### Vad händer om jag behöver bearbeta bilder parallellt?

Eftersom `OcrEngine` inte är trådsäker, skapa en **separat instans per tråd** eller använd en trådlokal pool. Exempel med `Parallel.ForEach`:

```csharp
Parallel.ForEach(imagePaths, path =>
{
    var engine = new OcrEngine(); // each thread gets its own engine
    var img = Image.FromFile(path);
    string text = engine.Recognize(img);
    // Store or log 'text' as needed
});
```

## Komplett fungerande exempel

När vi sätter ihop allt, här är en kompakt version som du kan klistra in i ett nytt konsolprojekt:

```csharp
using System;
using System.Drawing;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // Initialize OCR engine (single instance for this demo)
        OcrEngine engine = new OcrEngine();

        // Uncomment if you have a license file
        // engine.SetLicense(@"C:\Licenses\Aspose.OCR.lic");

        // Path to the PNG you want to read
        string file = @"C:\Images\sample.png";

        // Load, optionally preprocess, then recognize
        using (Image img = Image.FromFile(file))
        {
            string text = engine.Recognize(img);
            Console.WriteLine("=== OCR Output ===");
            Console.WriteLine(text);
        }
    }
}
```

Kompilera med `dotnet run` och se konsolen skriva ut den extraherade texten. Enkelt, eller? Det är skönheten med en väl‑des

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}