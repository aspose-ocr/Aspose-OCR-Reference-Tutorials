---
category: general
date: 2026-03-05
description: Konvertera TIFF till text i C# snabbt med Aspose OCR. Lär dig hur du
  visar OCR‑text från flersidiga TIFF‑filer på några minuter.
draft: false
keywords:
- convert tiff to text
- aspose ocr c#
- display ocr text
language: sv
og_description: Konvertera TIFF till text i C# med Aspose OCR. Den här guiden visar
  hur du steg för steg visar OCR‑text från flersidiga TIFF‑bilder.
og_title: Konvertera TIFF till text i C# – Komplett Aspose OCR‑guide
tags:
- Aspose
- OCR
- C#
- TIFF
title: Konvertera TIFF till text i C# med Aspose OCR
url: /sv/net/text-recognition/convert-tiff-to-text-in-c-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Konvertera TIFF till text i C# med Aspose OCR

Behöver du **konvertera TIFF till text** i C#? Du är inte ensam—många utvecklare kämpar med att extrahera läsbara strängar från flersidiga TIFF‑filer. Den goda nyheten är att Aspose OCR C# gör jobbet nästan smärtfritt, och du kan **visa OCR‑text** i konsolen eller skicka den till ett annat system på några sekunder.

I den här handledningen går vi igenom ett komplett, färdigt exempel som visar exakt hur du laddar en flersidig TIFF, kör OCR och skriver ut varje sidas text. Inga dolda steg, inga “se dokumentationen”-genvägar. När du är klar har du ett självständigt program som du kan släppa in i vilket .NET‑projekt som helst.

## Vad du behöver

- .NET 6.0 eller senare (exemplet riktar sig mot .NET 6, men .NET 5 fungerar också)  
- En giltig Aspose OCR‑licensfil (`Aspose.OCR.lic`). Biblioteket fungerar utan licens, men du får ett 20‑sekunders provvattenstämpel.  
- En flersidig TIFF‑fil som du vill bearbeta (vi kallar den `multipage.tif`).  
- Visual Studio 2022 eller någon annan editor du föredrar—inget exotiskt.

Om du har markerat alla rutor, låt oss dyka ner.

## Steg 1: Installera Aspose OCR NuGet‑paketet

Innan någon kod körs behöver du själva biblioteket. Öppna en terminal i din projektmapp och kör:

```bash
dotnet add package Aspose.OCR
```

Det här enkla kommandot hämtar den senaste stabila versionen (från och med mars 2026 är det 23.9).  

> **Proffstips:** Håll dina paket uppdaterade; nyare versioner innehåller ofta prestandaförbättringar för stora TIFF‑filer.

## Steg 2: Ställ in Aspose OCR C#‑licensen (Valfritt men rekommenderat)

Att köra OCR‑motorn utan licens är möjligt, men resultatet kommer att föregås av en provvarning. För att undvika det pekar du mot din `.lic`‑fil:

```csharp
using Aspose.OCR;

// ...

// Step 2: Apply your Aspose OCR license (optional but recommended)
var ocrEngine = new OcrEngine();
ocrEngine.SetLicense(@"C:\Licenses\Aspose.OCR.lic");
```

Om du hoppar över detta steg fungerar koden fortfarande—kom bara ihåg den extra texten i resultaten.

## Steg 3: Ladda och känna igen den flersidiga TIFF‑filen

Nu konverterar vi faktiskt **TIFF till text**. Hjälpfunktionen `ImageStream.FromFile` läser in filen i ett format som motorn förstår. Därefter anropar vi `Recognize()` som returnerar ett `OcrResult`‑objekt som innehåller varje sidas text.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

// ...

// Step 3: Load the multi‑page TIFF image to be processed
ocrEngine.Image = ImageStream.FromFile(@"C:\Images\multipage.tif");

// Step 4: Perform OCR on the loaded image
OcrResult ocrResult = ocrEngine.Recognize();
```

> **Varför detta är viktigt:** `Recognize()` gör det tunga arbetet—pixelanalys, språkdetection och återuppbyggnad av textrader—allt i ren C#‑kod. Resultatobjektet ger dig åtkomst sida‑för‑sida, vilket är perfekt för att **visa OCR‑text** senare.

## Steg 4: Iterera genom sidorna och **visa OCR‑text**

Med resultatet i handen loopar vi helt enkelt över sidorna och skriver ut varje. Detta är delen där du faktiskt ser konverteringen från bild till ren text.

```csharp
// Step 5: Iterate through each page of the result and display the recognized text
for (int pageIndex = 0; pageIndex < ocrResult.PageCount; pageIndex++)
{
    Console.WriteLine($"--- Page {pageIndex + 1} ---");
    Console.WriteLine(ocrResult.GetPageText(pageIndex));
    Console.WriteLine(); // Blank line for readability
}
```

När du kör programmet får du en output som liknar följande (din faktiska text kommer att skilja sig beroende på TIFF‑innehållet):

```
--- Page 1 ---
Hello, world!
This is the first page of our multi‑page TIFF.

--- Page 2 ---
Second page starts here.
More sample text follows.
```

Det var allt—du har framgångsrikt **konverterat TIFF till text** och **visat OCR‑text** för varje sida.

## Fullt fungerande exempel

Nedan är hela programmet som du kan kopiera‑och‑klistra in i ett nytt konsolprojekt (`dotnet new console`). Det inkluderar alla `using`‑direktiv, licenshantering och felkontroll.

```csharp
// ConvertTiffToText.cs
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace ConvertTiffToText
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // Step 1: Create an OCR engine instance
            // -----------------------------------------------------------------
            var ocrEngine = new OcrEngine();

            // -----------------------------------------------------------------
            // Step 2: Apply your Aspose OCR license (optional but recommended)
            // -----------------------------------------------------------------
            try
            {
                ocrEngine.SetLicense(@"C:\Licenses\Aspose.OCR.lic");
            }
            catch (Exception ex)
            {
                Console.WriteLine("License file not found or invalid. Running in trial mode.");
                Console.WriteLine($"Details: {ex.Message}");
            }

            // -----------------------------------------------------------------
            // Step 3: Load the multi‑page TIFF image to be processed
            // -----------------------------------------------------------------
            const string tiffPath = @"C:\Images\multipage.tif";

            if (!System.IO.File.Exists(tiffPath))
            {
                Console.WriteLine($"Error: TIFF file not found at {tiffPath}");
                return;
            }

            ocrEngine.Image = ImageStream.FromFile(tiffPath);

            // -----------------------------------------------------------------
            // Step 4: Perform OCR – this is where we convert TIFF to text
            // -----------------------------------------------------------------
            OcrResult ocrResult = ocrEngine.Recognize();

            // -----------------------------------------------------------------
            // Step 5: Iterate through each page and display OCR text
            // -----------------------------------------------------------------
            Console.WriteLine($"Successfully processed {ocrResult.PageCount} page(s).");
            for (int i = 0; i < ocrResult.PageCount; i++)
            {
                Console.WriteLine($"--- Page {i + 1} ---");
                Console.WriteLine(ocrResult.GetPageText(i));
                Console.WriteLine(); // Add spacing between pages
            }

            // Keep the console window open when debugging
            Console.WriteLine("Press any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**Förväntad output** (avkortad för korthet) visas tidigare. Om du ser provvattenstämpeln, dubbelkolla att licensvägen är korrekt.

## Vanliga fallgropar vid konvertering av TIFF till text

| Problem | Varför det händer | Hur du åtgärdar |
|-------|----------------|------------|
| **Minnesbrist på enorma TIFF‑filer** | Motorn läser in hela bilden i RAM. | Använd `ImageStream.FromFile(..., loadOnlyFirstPage: false)` och bearbeta sidor i batcher, eller öka processens minnesgräns. |
| **Skräptecken** | Lågre lösning på källbilder förvirrar OCR‑motorn. | Förbehandla TIFF‑filen (t.ex. öka DPI till 300) innan du skickar den till Aspose OCR. |
| **Licens ej tillämpad** | `SetLicense` kastar ett undantag som du ignorerar. | Omge anropet med try/catch (som visat) och logga felet. |
| **Saknad språkdata** | Som standard antar OCR engelska. | Sätt `ocrEngine.Language = OcrLanguage.French;` (eller något annat stödjande språk) före `Recognize()`. |

Genom att hantera dessa edge‑cases säkerställer du att din konvertering fungerar smidigt i produktion.

## Nästa steg: Gå bortom enkel visning

Nu när du kan **konvertera TIFF till text** och **visa OCR‑text**, kanske du vill:

- **Spara den extraherade texten** till en `.txt`‑fil eller en databas för senare analys.  
- **Kombinera flera TIFF‑filer** till en enda sökbar PDF med Aspose.PDF.  
- **Applicera efterbehandling** (stavningskontroll, regex‑rengöring) för att förbättra noggrannheten.  

Alla dessa utökningar bygger på samma grundmönster som vi just gått igenom.

---

### TL;DR

Vi har gått igenom en komplett C#‑lösning som **konverterar TIFF till text** med Aspose OCR C#. Koden skapar en `OcrEngine`, laddar eventuellt en licens, läser en flersidig TIFF, kör OCR och **visar OCR‑text** sida för sida. Med det medföljande fullständiga exemplet kan du släppa in detta i vilket .NET‑projekt som helst och börja extrahera text omedelbart.

Har du frågor om prestanda, språkstöd eller integration med andra Aspose‑produkter? Lämna en kommentar nedan—lycka till med kodandet!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}