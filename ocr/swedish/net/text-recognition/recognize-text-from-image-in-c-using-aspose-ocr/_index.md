---
category: general
date: 2026-05-31
description: Lär dig hur du känner igen text från en bild i C# med Aspose OCR, inklusive
  hur du extraherar text från tiff‑filer och laddar bild för OCR på ett effektivt
  sätt.
draft: false
keywords:
- recognize text from image
- extract text from tiff
- load image for OCR
- Aspose OCR C#
- GPU accelerated OCR
language: sv
og_description: Steg-för-steg-guide för att känna igen text från bild med Aspose OCR,
  som täcker extraktion från tiff och korrekt bildladdning för OCR.
og_title: igenkänna text från bild i C# med Aspose OCR
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to recognize text from image in C# with Aspose OCR, including
    how to extract text from tiff files and load image for OCR efficiently.
  headline: recognize text from image in C# using Aspose OCR
  type: TechArticle
- questions:
  - answer: Reduce its resolution before feeding it to the engine, or increase `GpuMemoryLimit`
      if you have enough VRAM.
    question: What if the image is huge (over 10 MB)?
  - answer: Absolutely. Just reuse the same `OcrEngine` instance and assign a new
      `ImageStream` each iteration.
    question: Can I process multiple images in a loop?
  - answer: '`OcrEngine` implements `IDisposable`. Wrap it in a `using` block for
      clean resource management, especially when working with GPU resources.'
    question: Do I need to dispose of anything?
  - answer: Set `engine.Language = OcrLanguage.Spanish` (or any supported language)
      before calling `Recognize()`.
    question: What about languages other than English?
  type: FAQPage
tags:
- OCR
- C#
- Aspose
title: Igenkänna text från bild i C# med Aspose OCR
url: /sv/net/text-recognition/recognize-text-from-image-in-c-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# igenkänna text från bild i C# med Aspose OCR

Har du någonsin behövt **recognize text from image** men var osäker på var du ska börja i C#? Du är inte ensam—många utvecklare stöter på den muren när de hanterar skannade dokument eller multi‑page TIFFs. I den här guiden går vi igenom ett komplett, färdigt exempel som **recognize text from image** med Aspose OCR‑biblioteket, och vi visar också hur du **extract text from tiff** och det bästa sättet att **load image for OCR** utan att rycka upp håret.

Vi täcker allt från att installera NuGet‑paketet till att hantera GPU‑acceleration och falla tillbaka till CPU när det behövs. I slutet av den här tutorialen har du en konsolapp som skriver ut den igenkända texten och bearbetningstiden—inga saknade delar, inga vaga referenser.

## Vad du kommer att bygga

- En enkel .NET‑konsolapplikation som laddar en bild (inklusive multi‑page TIFF)  
- En OCR‑motor konfigurerad för GPU‑användning, med smidig CPU‑fallback  
- Extraktion av ren text från bilden, utskriven i konsolen  
- Tidsinformation så att du kan se prestandapåverkan av GPU vs. CPU  

**Förutsättningar**

- .NET 6 SDK eller senare (koden fungerar med .NET Core och .NET Framework)  
- Grundläggande kunskap om C# och kommandoraden  
- Internetåtkomst för att hämta Aspose.OCR NuGet‑paketet  

Om du har detta, låt oss dyka ner.

![C#-kod för att känna igen text från bild med Aspose OCR](image.png "C#-kod för att känna igen text från bild med Aspose OCR")

## Steg 1 – Recognize text from image: Ställ in OCR‑motorn

Först och främst behöver vi en `OcrEngine`‑instans. Aspose OCR låter dig välja bearbetningsenhet—GPU för hastighet, CPU som en säkerhetsnät. Motorn accepterar också ett minnesgränsvink, vilket kan vara praktiskt på delade maskiner.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // Create the OCR engine and request GPU acceleration.
        // If no compatible GPU is found, Aspose silently falls back to CPU.
        OcrEngine engine = new OcrEngine
        {
            Device = OcrDevice.Gpu,      // Try GPU first
            GpuMemoryLimit = 1024        // Optional: cap GPU memory usage (MB)
        };
```

**Why this matters:**  
Att välja `OcrDevice.Gpu` kan spara sekunder på igenkänningstiden för stora bilder, särskilt multi‑page TIFFs. `GpuMemoryLimit` förhindrar att din app tar upp all GPU‑minne på en delad arbetsstation.

## Steg 2 – Load image for OCR (inklusive TIFF‑stöd)

Nu matar vi motorn med en bild. Aspose’s `ImageStream.FromFile` accepterar **any** format som biblioteket stödjer—TIFF, PNG, JPEG, du namnger det. Detta steg adresserar direkt kravet **load image for OCR**.

```csharp
        // Load the image you want to process.
        // Replace the path with the actual location of your TIFF or other image.
        engine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/sample_multi_page.tif");
```

**Pro tip:** Om du arbetar med en multi‑page TIFF, behandlar Aspose automatiskt varje sida som en separat ram, och motorn bearbetar dem sekventiellt. Ingen extra kod behövs.

## Steg 3 – Run the recognition and **extract text from tiff**

Med motorn förberedd och bilden laddad startar vi OCR‑operationen. `Recognize`‑metoden returnerar ett `OcrResult` som innehåller ren text, förtroendescore och tidsdetaljer.

```csharp
        // Perform the OCR operation.
        OcrResult result = engine.Recognize();
```

**Edge case handling:**  
Om GPU‑enheten inte är tillgänglig fungerar `engine.Recognize()` fortfarande eftersom motorn tyst byter till CPU. Du kan kontrollera `engine.Device` efter igenkänning om du behöver logga vilken enhet som faktiskt användes.

## Steg 4 – Retrieve the recognized plain text

Att extrahera texten är enkelt—läs bara `Text`‑egenskapen. Här **extract text from tiff** (eller någon annan bild) och presenterar den för användaren.

```csharp
        // Output the plain text that was extracted.
        Console.WriteLine($"Text:\n{result.Text}");
```

Du kommer att se de råa tecknen, radbrytningar bevarade som de visas i källbilden. För mer strukturerad output (som JSON eller CSV) kan du dyka ner i `result.Regions` och `result.Lines`, men ren text räcker oftast för snabba skript.

## Steg 5 – Measure processing time and handle GPU fallback

Prestanda är viktigt, särskilt när du bearbetar dussintals sidor. `ProcessingTime`‑egenskapen visar exakt hur lång tid OCR:n tog, oavsett om den kördes på GPU eller CPU.

```csharp
        // Show how long the recognition took.
        Console.WriteLine($"Time elapsed: {result.ProcessingTime.TotalSeconds}s");
    }
}
```

**Why you should care:**  
Om du märker att tiden skjuter i höjden kan du vilja justera `GpuMemoryLimit` eller explicit byta till CPU (`Device = OcrDevice.Cpu`). Omvänt betyder ett sub‑sekundresultat på en stor TIFF att din GPU‑acceleration gör sitt jobb.

## Fullt, färdigt‑att‑köra‑exempel

Kopiera koden nedan till ett nytt konsolprojekt (`dotnet new console -n OcrDemo`) och kör `dotnet add package Aspose.OCR`. Byt sedan ut `YOUR_DIRECTORY/sample_multi_page.tif` mot sökvägen till din bild.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // Step 1: Initialize the OCR engine with GPU preference.
        OcrEngine engine = new OcrEngine
        {
            Device = OcrDevice.Gpu,
            GpuMemoryLimit = 1024
        };

        // Step 2: Load image for OCR (supports TIFF, PNG, JPEG, etc.).
        engine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/sample_multi_page.tif");

        // Step 3: Run recognition – this will also **extract text from tiff**.
        OcrResult result = engine.Recognize();

        // Step 4: Retrieve and display the recognized plain text.
        Console.WriteLine($"Text:\n{result.Text}");

        // Step 5: Display how long the operation took.
        Console.WriteLine($"Time elapsed: {result.ProcessingTime.TotalSeconds}s");
    }
}
```

**Expected output (truncated for brevity):**

```
Text:
Invoice #12345
Date: 2026-05-01
Total: $1,250.00
...
Time elapsed: 1.42s
```

Om din maskin saknar en kapabel GPU kan den förflutna tiden vara några sekunder längre, men texten kommer fortfarande att extraheras korrekt.

## Vanliga frågor & fallgropar

- **What if the image is huge (over 10 MB)?**  
  Minska dess upplösning innan du matar den till motorn, eller öka `GpuMemoryLimit` om du har tillräckligt med VRAM.  
- **Can I process multiple images in a loop?**  
  Absolut. Återanvänd samma `OcrEngine`‑instans och tilldela ett nytt `ImageStream` för varje iteration.  
- **Do I need to dispose of anything?**  
  `OcrEngine` implementerar `IDisposable`. Wrappa den i ett `using`‑block för ren resurshantering, särskilt när du arbetar med GPU‑resurser.  

```csharp
using (OcrEngine engine = new OcrEngine { Device = OcrDevice.Gpu })
{
    // ... same steps as before
}
```

- **What about languages other than English?**  
  Ställ in `engine.Language = OcrLanguage.Spanish` (eller något annat stödd språk) innan du anropar `Recognize()`.  

## Slutsats

Du har nu en komplett, end‑to‑end‑lösning som **recognize text from image** i C# med Aspose OCR. Tutorialen täckte hur du **load image for OCR**, hur du **extract text from tiff**, och hur du mäter prestanda samtidigt som du hanterar GPU‑fallback på ett graciöst sätt.

Från här kan du:

- Experimentera med olika bildformat (BMP, PDF) för att se hur Aspose hanterar dem.  
- Dyka ner i `result.Regions` för bound‑box‑data om du behöver layout‑medveten information  

## Vad bör du lära dig härnäst?

- [Hur man använder Aspose för att känna igen bild från ström i OCR‑bildigenkänning](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [Extrahera text från bild – OCR‑optimering med Aspose.OCR för .NET](/ocr/english/net/ocr-optimization/)
- [Extrahera text från bild – känna igen rad med Aspose.OCR](/ocr/english/net/image-and-drawing-recognition/recognize-line/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}