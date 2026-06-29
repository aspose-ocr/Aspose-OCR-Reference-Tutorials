---
category: general
date: 2026-06-28
description: Hur man räta upp en bild med Aspose.OCR. Lär dig förbehandla bilden för
  OCR, förbättra OCR‑noggrannheten och räta upp en skannad bild med ett komplett C#‑exempel.
draft: false
keywords:
- how to deskew image
- preprocess image for ocr
- how to improve ocr
- deskew scanned image
language: sv
og_description: Hur man räta upp en bild med Aspose.OCR. Den här handledningen visar
  hur du förbehandlar bilden för OCR, förbättrar noggrannheten och räta upp en skannad
  bild steg för steg.
og_title: Hur man räta upp en bild i C# – Komplett Aspose.OCR-guide
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: How to deskew image using Aspose.OCR. Learn to preprocess image for
    OCR, improve OCR accuracy, and deskew scanned image with a full C# example.
  headline: How to Deskew Image in C# – Complete Aspose.OCR Guide
  type: TechArticle
- description: How to deskew image using Aspose.OCR. Learn to preprocess image for
    OCR, improve OCR accuracy, and deskew scanned image with a full C# example.
  name: How to Deskew Image in C# – Complete Aspose.OCR Guide
  steps:
  - name: Why a Deskew Filter First?
    text: 'When a document is rotated even a few degrees, the OCR engine misinterprets
      line baselines, leading to garbled output. The `DeskewFilter` automatically
      estimates the rotation angle (up to `MaxAngle` degrees) and rotates the bitmap
      back to a horizontal baseline. The returned `DeskewConfidence` tells '
  - name: 1️⃣ DeskewFilter (Primary Step)
    text: '- **What it does:** Detects the dominant text line direction and rotates
      the image. - **Why it matters:** A straight baseline maximizes character segmentation
      accuracy. - **Tip:** If your documents never exceed 10°, set `MaxAngle = 10`
      to speed up detection.'
  - name: 2️⃣ DenoiseFilter (Secondary Cleanup)
    text: '- **What it does:** Reduces random pixel noise that can appear after scanning.
      - **Why it matters:** Noise often creates false edges, confusing the OCR''s
      segmentation. - **Tip:** Adjust `Strength` between 0.3 (light) and 0.8 (aggressive)
      based on scan quality.'
  - name: 3️⃣ ContrastBoostFilter (Final Polish)
    text: '- **What it does:** Increases the difference between foreground text and
      background. - **Why it matters:** Low contrast can make faint characters invisible
      to the recognition engine. - **Tip:** A `Level` of 1.2 works for most black‑on‑white
      scans; for colored documents, experiment with values up to '
  type: HowTo
tags:
- OCR
- Aspose
- Image Processing
title: Hur man räta upp en bild i C# – Komplett Aspose.OCR-guide
url: /sv/net/ocr-optimization/how-to-deskew-image-in-c-complete-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Så här räta upp bild i C# – Komplett Aspose.OCR-guide

Har du någonsin undrat **how to deskew image** filer innan du matar dem till en OCR-motor? Du är inte ensam. Skannade dokument kommer ofta snett, och den lilla rotationen kan förstöra igenkänningsresultaten. Den goda nyheten? Med Aspose.OCR kan du räta upp (deskew) och rengöra bilder med bara några rader C#.

I den här handledningen går vi igenom ett komplett, körbart exempel som **preprocesses image for OCR**, lägger till ett deskew-filter och visar dig **how to improve OCR**‑noggrannhet. I slutet kommer du kunna **deskew scanned image** filer automatiskt och se förtroendesiffrorna själv.

> **Obs:** Koden fungerar med Aspose.OCR ≥ 22.10 och .NET 6+, men koncepten gäller även för tidigare versioner.

## Vad du behöver

- **Aspose.OCR for .NET** (NuGet package `Aspose.OCR`)
- En **skewed TIFF** eller JPEG som du vill räta upp
- Visual Studio 2022 (eller någon C#‑IDE)
- Grundläggande kunskap om C# och konsolprogram

Inga extra tredjepartsbibliotek krävs; hela pipeline‑kedjan finns i Aspose.OCR.

## Så räta du upp bild med Aspose.OCR

Kärnan i lösningen är en **filter pipeline**. Tänk på den som ett produktionslinje där varje filter åtgärdar ett specifikt problem: först korrigerar vi rotationen, sedan minskar vi brus, och slutligen ökar vi kontrasten så OCR‑motorn tydligt ser tecknen.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

class DeskewExample
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        var engine = new OcrEngine();

        // Step 2: Load the skewed image to be processed
        var img = OcrImage.FromFile(@"YOUR_DIRECTORY/skewed_doc.tif");

        // Step 3: Build a filter pipeline – deskew, then denoise, then boost contrast
        var pipeline = new OcrFilter[]
        {
            new DeskewFilter { MaxAngle = 30 },   // auto‑detect rotation up to 30°
            new DenoiseFilter { Strength = 0.5 },
            new ContrastBoostFilter { Level = 1.2 }
        };

        // Step 4: Apply the filters to the image before OCR
        var preprocessed = engine.ApplyFilters(img, pipeline);

        // Step 5: Perform OCR on the pre‑processed image
        var result = engine.Recognize(preprocessed);

        // Step 6: Output the deskew confidence and recognized text
        System.Console.WriteLine($"Deskew confidence: {result.DeskewConfidence:P2}");
        System.Console.WriteLine(result.Text);
    }
}
```

> **Bildexempel**  
> ![how to deskew image example](/images/deskew-example.png "how to deskew image example")

### Varför ett Deskew-filter först?

När ett dokument roteras bara några grader, missförstår OCR‑motorn radbaslinjer, vilket leder till förvrängd utskrift. `DeskewFilter` uppskattar automatiskt rotationsvinkeln (upp till `MaxAngle` grader) och roterar bitmapen tillbaka till en horisontell baslinje. Det returnerade `DeskewConfidence` visar hur säker algoritmen är på korrigeringen – användbart för loggning eller reservstrategier.

## Förbehandla bild för OCR – Bygga filter‑pipeline

### 1️⃣ DeskewFilter (Primärt steg)

- **Vad den gör:** Detekterar den dominerande textradens riktning och roterar bilden.  
- **Varför det är viktigt:** En rak baslinje maximerar teckensegmenteringens noggrannhet.  
- **Tips:** Om dina dokument aldrig överstiger 10°, sätt `MaxAngle = 10` för att snabba upp detektionen.

### 2️⃣ DenoiseFilter (Sekundär rengöring)

- **Vad den gör:** Minskar slumpmässigt pixelbrus som kan uppstå efter skanning.  
- **Varför det är viktigt:** Brus skapar ofta falska kanter, vilket förvirrar OCR:s segmentering.  
- **Tips:** Justera `Strength` mellan 0.3 (lätt) och 0.8 (aggressivt) beroende på skanningskvaliteten.

### 3️⃣ ContrastBoostFilter (Sista poleringen)

- **Vad den gör:** Ökar skillnaden mellan förgrundstext och bakgrund.  
- **Varför det är viktigt:** Låg kontrast kan göra svaga tecken osynliga för igenkänningsmotorn.  
- **Tips:** Ett `Level` på 1.2 fungerar för de flesta svart‑på‑vitt‑skanningar; för färgade dokument, experimentera med värden upp till 2.0.

Genom att kedja dessa tre filter **preprocesses image for OCR** på ett sätt som hanterar de vanligaste problemen: snedhet, brus och låg kontrast.

## Så förbättrar du OCR‑noggrannhet med Deskew och Denoise

Du kanske undrar, “Om jag redan har ett deskew-filter, varför bry sig om denoise och contrast boost?” Svaret ligger i **cumulative improvement**. Varje filter åtgärdar ett annat fel, och tillsammans höjer de den totala förtroendet.

#### Verklighetstest

| Test | Ursprunglig OCR‑noggrannhet | Efter Deskew | Efter full pipeline |
|------|----------------------------|--------------|----------------------|
| Simple invoice (5° tilt) | 78 % | 92 % | 96 % |
| Old newspaper scan (15° tilt, grainy) | 61 % | 78 % | 88 % |
| Low‑contrast form (no tilt) | 70 % | 71 % | 84 % |

*​Siffrorna är illustrativa men speglar typiska vinster som rapporterats av Aspose‑användare.*

**Viktig slutsats:** Även om ditt huvudmål är att **deskew scanned image**, ger tillägg av denoise‑ och kontraststeg ofta ett märkbart hopp i den slutgiltiga textkvaliteten.

## Deskew skannad bild: Verifiera resultat

När pipeline‑kedjan har körts får du två användbara informationsbitar:

```csharp
Console.WriteLine($"Deskew confidence: {result.DeskewConfidence:P2}");
Console.WriteLine(result.Text);
```

- **Deskew confidence** (`result.DeskewConfidence`) är en procentandel. Värden över 90 % betyder vanligtvis att rotationen korrigerades korrekt.  
- **Recognized text** (`result.Text`) låter dig omedelbart verifiera om resultatet ser rimligt ut.

Om förtroendet är lågt (< 70 %), överväg:

1. **Öka `MaxAngle`** – kanske dokumentet är roterat mer än förväntat.  
2. **Lägg till ett `BinarizationFilter`** före deskew för att förenkla bilden.  
3. **Rotera manuellt** bilden med `OcrImage.Rotate(angle)` som en reservlösning.

## Fullständigt end‑to‑end‑exempel (klart att köra)

Nedan är det **kompletta, självständiga programmet** som du kan kopiera‑klistra in i ett nytt Console App‑projekt. Kom ihåg att ersätta `YOUR_DIRECTORY` med mappen som innehåller din sneda TIFF.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

namespace DeskewDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Initialize the OCR engine
            var engine = new OcrEngine();

            // 2️⃣ Load the image you want to straighten
            var imgPath = @"C:\Images\skewed_doc.tif"; // <-- update this path
            var img = OcrImage.FromFile(imgPath);

            // 3️⃣ Define the preprocessing pipeline
            var pipeline = new OcrFilter[]
            {
                new DeskewFilter { MaxAngle = 30 },   // auto‑detect up to 30°
                new DenoiseFilter { Strength = 0.5 }, // moderate noise reduction
                new ContrastBoostFilter { Level = 1.2 } // brighten the text
            };

            // 4️⃣ Apply the pipeline – this returns a new image instance
            var preprocessed = engine.ApplyFilters(img, pipeline);

            // 5️⃣ Run OCR on the cleaned‑up image
            var result = engine.Recognize(preprocessed);

            // 6️⃣ Show confidence and the extracted text
            Console.WriteLine($"Deskew confidence: {result.DeskewConfidence:P2}");
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(result.Text);
        }
    }
}
```

**Förväntad output** (förutsatt en rimligt ren skanning):

```
Deskew confidence: 96.45%
=== Recognized Text ===
Invoice #12345
Date: 2024‑04‑01
Total: $1,250.00
...
```

Om du ser förvrängda tecken, gå tillbaka och justera filterstyrkorna eller lägg till ett `BinarizationFilter` som nämnts tidigare.

## Vanliga fallgropar & pro‑tips

- **Fallgrop:** Använda en TIFF med flera sidor. `OcrImage.FromFile` läser bara den första ramen. Använd `OcrImage.FromMultiPageFile` om du behöver alla sidor.  
- **Fallgrop:** Glömma att avyttra `OcrEngine`. Inslut den i ett `using`‑block i produktionskod för att frigöra inhemska resurser.  
- **Pro‑tips:** Cacha pipeline‑kedjan om du bearbetar många bilder med identiska inställningar – minskar overhead.  
- **Pro‑tips:** Logga `DeskewConfidence` till ett övervakningssystem; plötsliga droppar kan indikera en förändring i skannerns kalibrering.

## Nästa steg – Utöka arbetsflödet

Nu när du vet **how to deskew image** och **preprocess image for OCR**, kan du utforska:

- **Batch‑bearbetning** – loopa igenom en mapp med skannade PDF‑filer, konvertera varje sida till en bild och tillämpa samma pipeline.  
- **Språkstöd** – sätt `engine.Language = OcrLanguage.English;` eller andra språk för att förbättra igenkänning.  
- **Anpassad efterbehandling** – använd reguljära uttryck för att rensa vanliga OCR‑fel (t.ex. “0” vs “O”).

Varje av dessa ämnen knyter naturligt tillbaka till de sekundära nyckelorden **how to improve ocr** och **deskew scanned image**.

## Slutsats

Vi har gått igenom allt du behöver veta om **how to deskew image** med Aspose.OCR, från att bygga en robust filter‑pipeline till att verifiera förtroendesiffror. Genom att **preprocess image for OCR** med deskew, denoise och contrast boost kommer du se en mätbar förbättring i **how to improve OCR**‑resultat, särskilt på sneda eller brusiga skanningar.

Prova det på din egen dokumentuppsättning, justera filterparametrarna och se OCR‑noggrannheten stiga. Har du frågor eller en knepig fil som vägrar räta upp? lämna en kommentar nedan—vi felsöker tillsammans. Lycka till med kodandet!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närliggande ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Hur man använder AspOCR: Förbehandla bild‑OCR‑filter för .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Hur man OCR‑ar bild – Utför OCR på bild i OCR‑bildigenkänning](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)
- [Hur man ställer in tröskelvärde i OCR‑bildigenkänning](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}