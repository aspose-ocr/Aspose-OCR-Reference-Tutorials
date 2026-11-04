---
category: general
date: 2026-06-06
description: Känn igen textbild med C# OCR – ett steg‑för‑steg C# OCR‑exempel som
  extraherar text från skanningar och konverterar skanningen till text på några minuter.
draft: false
keywords:
- recognize text image
- c# ocr example
- extract text scan
- convert scan to text
- image to text c#
language: sv
og_description: Känn igen textbilder med C# OCR. Lär dig ett praktiskt C# OCR‑exempel
  som extraherar text från skanningar, konverterar skanning till text och hanterar
  verkliga bilder.
og_title: Känn igen text på bild i C# – Komplett OCR-handledning
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: recognize text image using C# OCR – a step‑by‑step c# ocr example that
    extracts text from scans and convert scan to text in minutes.
  headline: recognize text image in C# – Full OCR Guide
  type: TechArticle
- questions:
  - answer: The `Windows.Media.Ocr` namespace is Windows‑only. On Linux or macOS you’d
      swap it for TesseractSharp or IronOcr—both expose a similar `Engine.Recognize`
      method, so the surrounding code stays virtually unchanged.
    question: Does this work on .NET Core on Linux?
  - answer: Handwriting recognition is still experimental. For best results, stick
      to printed fonts or consider a cloud service like Azure Cognitive Services if
      you need high accuracy.
    question: How accurate is the built‑in OCR for handwritten notes?
  - answer: 'Not out of the box. Convert each PDF page to an image first (using `PdfSharp`
      or `Ghostscript`) and then feed the bitmap to the OCR engine. --- ## Conclusion
      You now have a complete, production‑ready **c# ocr example** that can **recognize
      text image** files, **extract text scan** contents, and **co'
    question: Can I process PDFs directly?
  type: FAQPage
tags:
- OCR
- C#
- Image Processing
title: Igenkänna text i bild i C# – Fullständig OCR-guide
url: /sv/net/text-recognition/recognize-text-image-in-c-full-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# igenkänna textbild i C# – Komplett OCR-handledning

Har du någonsin undrat hur man **recognize text image** direkt från ett skannat foto med C#? Du är inte ensam. Oavsett om du digitaliserar gamla kvitton, hämtar data från ett visitkort, eller bara omvandlar en lågupplöst skanning till redigerbar text, är förmågan att extrahera text från en bild ett praktiskt trick som varje utvecklare bör ha i sin verktygslåda.

I den här guiden går vi igenom ett **c# ocr example** som laddar en bild, kör optisk teckenigenkänning och skriver ut resultatet i konsolen. I slutet kommer du kunna **extract text scan**‑filer, **convert scan to text**, och till och med finjustera processen för brusiga bilder. Inga avancerade tredjepartstjänster behövs—bara den inbyggda Windows.Media.Ocr‑API:n (eller någon kompatibel OcrEngine) och några få kodrader.

## Vad du kommer att lära dig

* Hur man sätter upp ett C#‑projekt för OCR.
* Den exakta koden som behövs för **recognize text image**‑filer.
* Tips för att hantera lågupplösta skanningar och flersidiga dokument.
* Sätt att utöka exemplet till ett återanvändbart bibliotek för dina egna appar.

### Förutsättningar

* .NET 6.0 eller senare (API‑et fungerar även på .NET 5+).
* Visual Studio 2022 (Community‑editionen är okej) eller någon IDE du föredrar.
* En exempelbild som `lowres_scan.jpg` placerad i en mapp du kan referera till.
* Grundläggande kunskap om async/await—OCR‑anrop är asynkrona i Windows‑API:t.

> **Pro tip:** Om du är på en icke‑Windows‑plattform, byt ut `Windows.Media.Ocr`‑namnutrymmet mot ett plattformsoberoende bibliotek som TesseractSharp; den omgivande logiken förblir densamma.

---

## Steg 1: Ställ in för **recognize text image** med en OCR‑motor

Först behöver vi en OCR‑motorinstans. Klassen `OcrEngine` är ingångspunkten för alla **image to text c#**‑operationer.

```csharp
using System;
using System.IO;
using Windows.Graphics.Imaging;
using Windows.Media.Ocr;
using Windows.Storage.Streams;

class Program
{
    static async Task Main(string[] args)
    {
        // Create the OCR engine – default language is English.
        OcrEngine engine = OcrEngine.TryCreateFromLanguage(new OcrLanguage("en"));
        if (engine == null)
        {
            Console.WriteLine("Failed to create OcrEngine. Make sure you are on Windows 10 version 1809 or later.");
            return;
        }

        // Continue with the rest of the pipeline...
```

**Varför detta är viktigt:** Motorn abstraherar det tunga arbetet med mönsterigenkänning. Genom att explicit skapa den får vi kontroll över språkinställningarna, vilket är avgörande när du senare vill **extract text scan**‑dokument på andra språk.

## Steg 2: Ladda bildfilen – kärnan i **convert scan to text**

Nästa steg läser vi bilden från disk och omvandlar den till en `SoftwareBitmap`, det format som OCR‑motorn förväntar sig.

```csharp
        // Load the image file into a SoftwareBitmap.
        string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "lowres_scan.jpg");
        using (FileStream fs = new FileStream(imagePath, FileMode.Open, FileAccess.Read))
        {
            // Decode the image (supports JPEG, PNG, BMP, etc.).
            BitmapDecoder decoder = await BitmapDecoder.CreateAsync(fs.AsRandomAccessStream());
            SoftwareBitmap bitmap = await decoder.GetSoftwareBitmapAsync();

            // Optional: upscale low‑resolution images for better accuracy.
            SoftwareBitmap upscaled = SoftwareBitmap.Convert(bitmap, bitmap.BitmapPixelFormat, bitmap.BitmapAlphaMode);
            // Pass the bitmap to OCR.
            await RecognizeAsync(engine, upscaled);
        }
    }
```

**Varför vi gör detta:** Att direkt mata in en rå filström i OCR ger ofta dåliga resultat, särskilt med lågupplösta skanningar. Genom att konvertera till en `SoftwareBitmap` kan vi manipulera DPI, färgdjup och till och med applicera filter innan igenkänning.

## Steg 3: Utför **recognize text image**‑operationen

Nu anropar vi äntligen motorns `RecognizeAsync`‑metod. Här sker magin.

```csharp
    private static async Task RecognizeAsync(OcrEngine engine, SoftwareBitmap bitmap)
    {
        // Run OCR – this returns an OcrResult object.
        OcrResult result = await engine.RecognizeAsync(bitmap);

        // The Result contains a collection of lines and words.
        Console.WriteLine("=== OCR Output ===");
        foreach (var line in result.Lines)
        {
            Console.WriteLine(line.Text);
        }

        // For a quick **image to text c#** check, also output the raw string.
        Console.WriteLine("\nFull Text:\n" + result.Text);
    }
}
```

**Vad du kommer att se:** Om `lowres_scan.jpg` innehåller frasen “Hello World”, kommer konsolen att skriva ut:

```
=== OCR Output ===
Hello World

Full Text:
Hello World
```

Det är hela **c# ocr example** i aktion—bara fyra logiska steg, men det täcker allt från filinläsning till slutligt resultat.

## Steg 4: Hantera kantfall – När skanningen inte är perfekt

Verkliga bilder är inte alltid skarpa. Här är några justeringar du kan göra utan att skriva om hela programmet:

| Problem | Snabb åtgärd |
|-------|-----------|
| **Mycket låg DPI (≤ 72)** | Skala upp bitmapen med `BitmapTransform` innan igenkänning. |
| **Snedvriden text** | Applicera en rotationstransform (`SoftwareBitmap.Rotate`) för att räta upp sidan. |
| **Flera språk** | Skapa `OcrEngine.TryCreateFromLanguage(new OcrLanguage("en-fr"))` och sätt `engine.Language` därefter. |
| **Stora filer** | Bearbeta bilden i rutor (`engine.RecognizeAsync(tileBitmap)`) och sammanfoga resultaten. |

Dessa justeringar säkerställer att din **extract text scan**‑rutin förblir pålitlig även när du hanterar brusiga kvitton eller foton tagna i vinkeln.

## Steg 5: Gör om exemplet till en återanvändbar hjälparklass (valfritt)

Om du planerar att **convert scan to text** i flera delar av en applikation, paketera logiken i en liten verktygsklass:

```csharp
public static class OcrHelper
{
    private static readonly OcrEngine _engine = OcrEngine.TryCreateFromLanguage(new OcrLanguage("en"));

    public static async Task<string> ImageToTextAsync(string filePath)
    {
        using var fs = new FileStream(filePath, FileMode.Open, FileAccess.Read);
        var decoder = await BitmapDecoder.CreateAsync(fs.AsRandomAccessStream());
        var bitmap = await decoder.GetSoftwareBitmapAsync();

        var result = await _engine.RecognizeAsync(bitmap);
        return result.Text;
    }
}
```

Nu kallar du helt enkelt:

```csharp
string text = await OcrHelper.ImageToTextAsync("YOUR_DIRECTORY/lowres_scan.jpg");
Console.WriteLine(text);
```

**Varför du kommer att älska detta:** Hjälparklassen isolerar OCR‑logiken, så att du kan fokusera på affärslogik—perfekt för ett **c# ocr example** som kommer att återanvändas i flera projekt.

---

![exempel på recognize text image](https://example.com/ocr-demo.png "Skärmbild av OCR-konsolutdata som visar resultatet av recognize text image")

*Alt text:* **recognize text image**‑utdata från en C# OCR‑konsolapplikation.

---

## Vanliga frågor

**Q: Fungerar detta på .NET Core på Linux?**  
A: `Windows.Media.Ocr`‑namnutrymmet är endast för Windows. På Linux eller macOS skulle du byta ut det mot TesseractSharp eller IronOcr—båda exponerar en liknande `Engine.Recognize`‑metod, så den omgivande koden förblir i stort sett oförändrad.

**Q: Hur exakt är den inbyggda OCR:n för handskrivna anteckningar?**  
A: Handstiftsigenkänning är fortfarande experimentell. För bästa resultat, håll dig till tryckta typsnitt eller överväg en molntjänst som Azure Cognitive Services om du behöver hög noggrannhet.

**Q: Kan jag bearbeta PDF-filer direkt?**  
A: Inte utan vidare. Konvertera varje PDF-sida till en bild först (med `PdfSharp` eller `Ghostscript`) och mata sedan bitmapen till OCR‑motorn.

---

## Slutsats

Du har nu ett komplett, produktionsklart **c# ocr example** som kan **recognize text image**‑filer, **extract text scan**‑innehåll och **convert scan to text** med bara några kodrader. Genom att förstå flödet—motorinstansiering, bildinläsning, asynkron igenkänning och resultat‑hantering—kan du anpassa mönstret till vilket C#‑projekt som helst som behöver omvandla bilder till sökbara strängar.

Redo för nästa steg? Prova att lägga till ett enkelt UI med WinForms eller WPF, experimentera med olika språk, eller koppla utdata till en databas för sökbara arkiv. Himlen är gränsen när du behärskar **image to text c#**‑tekniker.

Lycka till med kodningen, och må dina skanningar alltid vara skarpa!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstrerats i denna guide. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Extrahera bildtext i C# med språkval med Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Konvertera bild till text – Utför OCR på bild från URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [Hur man extraherar text från bild genom att förbereda rektanglar i OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}