---
category: general
date: 2026-02-16
description: Lär dig hur du utför OCR i C# med Aspose.OCR – känna igen text från foto,
  läsa text från skanning och extrahera text från kvitto med hög noggrannhet.
draft: false
keywords:
- how to perform OCR
- recognize text from photo
- read text from scan
- extract text from receipt
- improve OCR accuracy
language: sv
og_description: Lär dig hur du utför OCR i C# med Aspose.OCR. Den här guiden visar
  hur du känner igen text från foto, läser text från skanning och extraherar text
  från kvitto.
og_title: Hur man utför OCR i C# – Komplett Aspose-guide
tags:
- C#
- Aspose.OCR
- Image Processing
title: Hur man utför OCR i C# – Komplett Aspose‑guide
url: /sv/net/text-recognition/how-to-perform-ocr-in-c-complete-aspose-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man utför OCR i C# – Komplett Aspose-guide

Har du någonsin undrat **hur man utför OCR** på ett suddigt kvitto eller ett slumpmässigt foto du tog med telefonen? Du är inte ensam. I många verkliga appar måste vi **känna igen text från foto**‑filer, **läsa text från skanning**‑dokument, eller **extrahera text från kvitto**‑bilder utan att skicka data till en molntjänst.  

I den här handledningen går vi igenom ett självständigt exempel som visar dig **hur man utför OCR** med Aspose.OCR, och vi strör in tips om hur du **förbättrar OCR‑noggrannhet** längs vägen. I slutet har du ett färdigt C#‑konsolprogram som drar ut vanlig text från vilken bild du pekar på.

> **Vad du behöver**  
> * .NET 6 SDK (eller någon nyare .NET‑version)  
> * Aspose.OCR NuGet‑paket (`Install-Package Aspose.OCR`)  
> * En exempelbild – till exempel ett foto av ett kvitto med namnet `photo_receipt.jpg`  

Om det låter bekant, bra – låt oss dyka ner.

![how to perform OCR example](image.png){alt="hur man utför OCR"}

## Hur man utför OCR med Aspose.OCR i C#

Det första steget är att konfigurera OCR‑motorn och ladda en engelsk språkmodell. Detta är kärnan i **hur man utför OCR** med Aspose; utan en språkmodell skulle motorn inte veta vilka tecken den ska leta efter.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Load the English language model – change this if you need another language
ocrEngine.LoadLanguage(LanguageModel.English);
```

*Varför detta är viktigt*: Att ladda rätt språkmodell påverkar direkt igenkänningshastigheten och noggrannheten. Engelska är det vanligaste fallet, men Aspose levereras med dussintals andra om du någonsin behöver **läsa text från skanning**‑dokument på franska, tyska osv.

## Känn igen text från foto

Foton tagna med en telefon lider ofta av rotation, brus eller låg kontrast. Innan vi ber motorn att **känna igen text från foto** konfigurerar vi några förbehandlingsalternativ som rensar bilden.

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

*Proffstips*: Om du märker saknade tecken, prova att byta `DenoiseLevel` till `High` eller använda `BinarizeMethod.Sauvola`. Dessa justeringar är en del av **förbättra OCR‑noggrannhet**‑strategierna.

## Läs text från skanning

Nu när motorn är förberedd laddar vi bilden. Oavsett om det är en skannad PDF‑sida sparad som JPEG eller ett foto av ett utskrivet formulär, förblir koden densamma.

```csharp
// Load the image you want to process
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/photo_receipt.jpg");
```

Om du har en `Stream` istället för en filsökväg, ersätt bara `FromFile` med `FromStream`. Denna flexibilitet är praktisk när du **läser text från skanning**‑bilder som kommer från en webbuppladdning.

## Extrahera text från kvitto

När allt är på plats är själva OCR‑anropet en enda rad. Metoden returnerar den extraherade vanlig‑text‑strängen, som vi sedan kan visa, lagra eller skicka vidare till ett annat system.

```csharp
// Perform OCR and capture the result
string extractedText = ocrEngine.Recognize();

// Output the text to the console
Console.WriteLine("=== OCR RESULT ===");
Console.WriteLine(extractedText);
```

**Förväntad utdata** (exempel för ett enkelt kvitto):

```
=== OCR RESULT ===
Store: CoffeeShop
Date: 2024-02-15
Item      Qty   Price
Latte      2    4.50
Bagel      1    2.75
Total            7.25
```

Om utdata ser förvrängd ut, gå tillbaka till förbehandlingsavsnittet – det är den vanligaste platsen för att **förbättra OCR‑noggrannhet**.

## Förbättra OCR‑noggrannhet – avancerade justeringar

Medan standardinställningarna fungerar för många fall, kräver produktionspipeline ofta extra omsorg:

| Situation | Justering | Orsak |
|-----------|-----------|-------|
| Mycket mörk bakgrund | `ContrastEnhancement = true` + `Binarize = BinarizeMethod.Sauvola` | Ökar separationen mellan text och bakgrund |
| Handskrivna anteckningar | `ocrEngine.LoadLanguage(LanguageModel.EnglishHandwritten)` | Specialiserad modell för kursiva streck |
| Fler‑sidiga skanningar | Loop över varje sidbild och anropa `Recognize()` per iteration | Håller minnesfotavtrycket lågt |
| Stora bilder (> 2000 px) | Ändra storlek innan du matar in i OCR (`Image.Resize(width, height)`) | Snabbare bearbetning, mindre minnesanvändning |

Kom ihåg, **hur man utför OCR** är inte ett recept som passar alla – du kommer ofta att experimentera med dessa reglage tills utdata möter din kvalitetsnivå.

## Fullt fungerande exempel

Nedan är det kompletta, kopiera‑och‑klistra‑klara programmet. Det innehåller alla delar vi diskuterat, plus en liten hjälpfunktion som kontrollerar om filen finns innan den läses.

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

Kör programmet med `dotnet run`. Om allt är korrekt konfigurerat ser du den extraherade texten skriven i konsolen.

## Vanliga frågor & specialfall

**Q: Vad händer om bilden är en PDF?**  
A: Konvertera varje PDF‑sida till en bild först (t.ex. med `Aspose.Pdf` eller `PdfSharp`) och mata sedan den resulterande bitmapen till `ocrEngine.Image`.

**Q: Kan jag bearbeta bilder parallellt?**  
A: Ja, men skapa en separat `OcrEngine` per tråd. Motorn är inte trådsäker, så delning av en enda instans kan leda till race‑conditions.

**Q: Fungerar detta på Linux?**  
A: Absolut. Aspose.OCR är plattformsoberoende; se bara till att de inhemska beroendena är installerade (`libgdiplus` för .NET Core på Linux).

**Q: Hur hanterar jag flerspråkiga kvitton?**  
A: Ladda flera språkmodeller innan du känner igen:  
```csharp
ocrEngine.LoadLanguage(LanguageModel.English);
ocrEngine.LoadLanguage(LanguageModel.Spanish);
```  
Motorn kommer att prova varje modell i tur och ordning.

## Slutsats

Du har nu ett gediget, end‑to‑end‑svar på **hur man utför OCR** i C# med Aspose.OCR. Handledningen täckte allt från att initiera motorn, **känna igen text från foto**, **läsa text från skanning**, till **extrahera text från kvitto**, och gav dig praktiska sätt att **förbättra OCR‑noggrannhet**.  

Nästa steg? Prova att byta den engelska modellen mot en handskriven, experimentera med olika `BinarizeMethod`‑värden, eller integrera OCR‑anropet i ett ASP.NET‑API som bearbetar uppladdningar i realtid. Möjligheterna är lika breda som bilderna du matar in.

Har du fler frågor om OCR, bildförbehandling eller Aspose‑bibliotek? Lämna en kommentar eller utforska den officiella Aspose.OCR‑dokumentationen för djupare insikter. Lycka till med kodandet!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}