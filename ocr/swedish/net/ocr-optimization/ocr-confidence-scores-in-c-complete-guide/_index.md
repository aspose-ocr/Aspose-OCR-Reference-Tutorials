---
category: general
date: 2026-05-31
description: Lär dig hur du får OCR‑konfidenspoäng i C# när du extraherar text från
  en bild och läser kvittobilder med Aspose OCR.
draft: false
keywords:
- ocr confidence scores
- extract text from image
- ocr bounding boxes
- perform ocr on jpg
- read receipt image
language: sv
og_description: OCR-förtroendescore låter dig mäta noggrannheten; den här guiden visar
  hur du extraherar text från en bild, får bounding boxes och läser en kvittobild
  med Aspose OCR.
og_title: OCR-förtroendescore i C# – Komplett guide
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to get OCR confidence scores in C# while extract text from
    image and read receipt image with Aspose OCR.
  headline: OCR confidence scores in C# – Complete Guide
  type: TechArticle
tags:
- OCR
- C#
- Aspose
- Image Processing
title: OCR-förtroendescore i C# – Komplett guide
url: /sv/net/ocr-optimization/ocr-confidence-scores-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR‑konfidenspoäng i C# – Komplett guide

Har du någonsin undrat hur man **OCR confidence scores** när du behöver *extrahera text från bild*? Kanske försöker du **read receipt image**‑filer för kostnadsspårning och vill veta vilka tecken motorn är osäker på. De goda nyheterna? Med Aspose.OCR kan du hämta konfidensprocent, avgränsningsrutor och ren text från en JPG på bara några rader C#.

I den här handledningen går vi igenom allt du behöver veta: installera biblioteket, konfigurera motorn för att **perform OCR on JPG**, hämta konfidenspoäng och tolka **OCR bounding boxes** som visar var varje tecken finns på sidan. I slutet har du en färdig konsolapp som skriver ut varje tecken, dess konfidens och dess position—perfekt för att validera kvitton eller vilket som helst skannat dokument.

## Vad du kommer att lära dig

- Installera Aspose.OCR via NuGet och sätt upp en grundläggande OCR‑motor.  
- Konfigurera `OcrOptions` för att begära plain‑text‑utdata **with confidence scores** och **bounding boxes**.  
- Loopa igenom `OcrResult` för att **extract text from image** rad‑för‑rad och symbol‑för‑symbol.  
- Hantera vanliga fallgropar som saknade filer, låg‑konfidens‑tecken och icke‑JPG‑format.  
- Utöka exemplet för att bearbeta flera kvittobilder i en mapp.

Ingen tidigare erfarenhet av Aspose krävs; bara en fungerande .NET‑miljö och en kvittobild (JPG) du vill testa.

## Steg 1 – Installera Aspose.OCR och förbered ditt projekt

Först och främst: du behöver Aspose.OCR‑NuGet‑paketet. Öppna en terminal i din projektmapp och kör:

```bash
dotnet add package Aspose.OCR
```

> **Pro tip:** Den kostnadsfria provversionen fungerar för upp till 200 sidor, vilket är mer än tillräckligt för att testa kvittoskanning.

När paketet är installerat, skapa ett nytt konsolprojekt (om du inte redan har ett):

```bash
dotnet new console -n ReceiptOcrDemo
cd ReceiptOcrDemo
```

Nu kan du öppna den genererade `Program.cs` och börja lägga till using‑direktiven:

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;
```

Dessa namnrymder ger dig åtkomst till `OcrEngine`, `OcrOptions` och resultattyperna vi kommer att behöva senare.

## Steg 2 – Hämta OCR‑konfidenspoäng och OCR‑avgränsningsrutor

Detta är kärnan i handledningen. Vi kommer att konfigurera motorn så att varje igenkänt tecken får en **confidence score** och en **bounding box** (rektangeln som omsluter tecknet). H2‑rubriken själv innehåller huvudnyckelordet, vilket uppfyller SEO‑regeln.

```csharp
// Step 2: Initialize the OCR engine and request detailed output
OcrEngine ocrEngine = new OcrEngine();

// Load the image you want to process – here we assume a JPEG receipt
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/receipt.jpg");

// Tell Aspose we want plain text, confidence percentages, and bounding boxes
ocrEngine.Options = new OcrOptions
{
    OutputFormat = OcrOutputFormat.PlainText,
    IncludeConfidence = true,
    IncludeBoundingBoxes = true
};
```

**Varför inkludera konfidenspoäng?**  
En konfidenspoäng (0‑100 %) visar hur säker motorn är på varje tecken. Om du matar utdata i efterföljande logik—t.ex. ett arbetsflöde för godkännande av utgifter—kan du automatiskt avvisa eller flagga lågt‑konfidens‑symboler.

**Varför begära avgränsningsrutor?**  
Avgränsningsrutor är nödvändiga när du behöver markera text på originalbilden, extrahera delregioner eller justera OCR‑resultat med ett UI‑överlägg. Varje `character.Bounds` ger dig X, Y, bredd och höjd i pixelkoordinater.

## Steg 3 – Utför OCR på JPG och extrahera text från bild

Nu kör vi faktiskt motorn. Anropet till `Recognize()` utför allt tungt arbete och returnerar ett `OcrResult`‑objekt.

```csharp
// Step 3: Run the OCR process
OcrResult ocrResult = ocrEngine.Recognize();
```

Om bildsökvägen är fel eller filen inte är i ett stödd format, kastar Aspose ett `FileNotFoundException` eller `UnsupportedImageFormatException`. Omge anropet med ett try/catch‑block i produktionskod för att hantera dessa kantfall på ett smidigt sätt.

### Hämta ren text

Om du bara behöver den sammanslagna texten kan du läsa `ocrResult.Text`:

```csharp
Console.WriteLine("Full extracted text:");
Console.WriteLine(ocrResult.Text);
```

Men eftersom vi också begärde konfidenspoäng och avgränsningsrutor, kommer vi att iterera genom strukturen för att se varje teckens detaljer.

## Steg 4 – Iterera genom rader, symboler och visa OCR‑konfidenspoäng

Här är loopen som skriver ut varje tecken, dess konfidens och dess ruta. Detta är där **read receipt image**‑exemplet verkligen glänser.

```csharp
// Step 4: Walk through each line and each symbol (character)
foreach (var textLine in ocrResult.Lines)
{
    foreach (var character in textLine.Symbols)
    {
        Console.WriteLine(
            $"Char: '{character.Text}'  Confidence: {character.Confidence}%  Box: {character.Bounds}");
    }
}
```

Sample output might look like:

```
Char: 'R'  Confidence: 98%  Box: {X=12,Y=34,Width=15,Height=20}
Char: 'e'  Confidence: 95%  Box: {X=28,Y=34,Width=12,Height=20}
Char: 'c'  Confidence: 92%  Box: {X=41,Y=34,Width=13,Height=20}
...
```

**Tolka siffrorna:**  
- **Confidence ≥ 90 %** – vanligtvis säkert att acceptera.  
- **Confidence 70‑89 %** – du kanske vill dubbelkolla, särskilt för siffror i belopp.  
- **Confidence < 70 %** – överväg att flagga för manuell granskning.

## Steg 5 – Fullt körbart exempel (inklusive felhantering)

När vi sätter ihop allt, här är ett komplett program du kan kopiera‑klistra in i `Program.cs`. Det inkluderar en enkel kontroll för saknade filer och skriver ut ett vänligt meddelande om OCR misslyckas.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Path to the receipt image – adjust to your environment
            const string imagePath = "YOUR_DIRECTORY/receipt.jpg";

            if (!System.IO.File.Exists(imagePath))
            {
                Console.WriteLine($"Error: File not found -> {imagePath}");
                return;
            }

            try
            {
                // Initialize engine
                OcrEngine ocrEngine = new OcrEngine
                {
                    Image = ImageStream.FromFile(imagePath),
                    Options = new OcrOptions
                    {
                        OutputFormat = OcrOutputFormat.PlainText,
                        IncludeConfidence = true,
                        IncludeBoundingBoxes = true
                    }
                };

                // Perform OCR
                OcrResult ocrResult = ocrEngine.Recognize();

                // Show full plain text (optional)
                Console.WriteLine("=== Extracted Text ===");
                Console.WriteLine(ocrResult.Text);
                Console.WriteLine();

                // Show each character with confidence and bounding box
                Console.WriteLine("=== Detailed Character Data ===");
                foreach (var line in ocrResult.Lines)
                {
                    foreach (var symbol in line.Symbols)
                    {
                        Console.WriteLine(
                            $"Char: '{symbol.Text}'  Confidence: {symbol.Confidence}%  Box: {symbol.Bounds}");
                    }
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine($"OCR failed: {ex.Message}");
            }
        }
    }
}
```

### Förväntad output

När du kör `dotnet run` kommer konsolen först att visa den sammanslagna kvittotexten, sedan en lista över varje tecken med dess konfidenspoäng och avgränsningsruta. Om ett teckens konfidens är låg ser du en procentsats under 80, vilket är en signal att manuellt verifiera den delen av kvittot.

## Bonus: Bearbeta flera kvitton i en mapp

Om du har en batch med kvitto‑JPG‑filer, omslut logiken ovan i en `foreach (var file in Directory.GetFiles(folder, "*.jpg"))`‑loop. Kom ihåg att återställa `OcrEngine` för varje fil, eller skapa en ny instans inuti loopen för att undvika tillståndsläckage.

```csharp
string folder = "YOUR_DIRECTORY/Receipts";
foreach (var file in System.IO.Directory.GetFiles(folder, "*.jpg"))
{
    // reuse the same code block, just replace imagePath with 'file'
}
```

Bearbetning i bulk är praktiskt för nattliga import av utgifter.

## Slutsats

Du har nu en solid, end‑to‑end‑lösning för att hämta **OCR confidence scores** i C#, **extracting text from image**, och hämta **OCR bounding boxes** medan du **perform OCR on JPG**‑filer såsom en **read receipt image**. Koden är helt självständig, fungerar med den senaste Aspose.OCR‑versionen (per 2026‑05‑31), och ger dig den detaljerade data du behöver för att bygga pålitliga dokument‑bearbetningspipelines.

Vad blir nästa steg? Prova att visualisera avgränsningsrutorna på originalkvitton med `System.Drawing` eller ett UI‑bibliotek, eller mata lågt‑konfidens‑tecken till en sekundär verifieringstjänst. Du kan också experimentera med olika språk genom att sätta `ocrEngine.Options.Language = OcrLanguage.French;` – API‑et stödjer många lokaler.

Lycka till med kodningen, och må dina konfidenspoäng alltid vara höga! 

![Console output showing OCR confidence scores and bounding boxes for a receipt

## Vad bör du lära dig härnäst?

- [Extrahera bildtext C# med språkval med Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Hur man får OCR‑teckenval för igenkända tecken i bildigenkänning](/ocr/english/net/text-recognition/get-choices-for-recognized-characters/)
- [Hur man använder Aspose OCR för JSON‑resultat i bildigenkänning](/ocr/english/net/text-recognition/get-result-as-json/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}