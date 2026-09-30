---
category: general
date: 2026-02-09
description: Extrahera text från bilder snabbt med C# genom att ställa in maximal
  parallellism för batch‑OCR – lär dig konvertera skannade sidor, hantera OCR för
  flera bilder och läsa PNG‑text effektivt.
draft: false
keywords:
- extract text images
- set max parallelism
- convert scanned pages
- multiple image ocr
- read png text
language: sv
og_description: Extrahera text från bilder i C# genom att ange maximal parallellism.
  Den här handledningen visar hur man konverterar skannade sidor, kör flera bild‑OCR
  och läser PNG‑text med Aspose OCR.
og_title: Extrahera textbilder från PNG-filer med C# – Komplett batch-OCR-guide
tags:
- OCR
- C#
- Aspose
- Batch Processing
title: Extrahera textbilder från PNG-filer med C# – batch-OCR med Aspose OCR
url: /sv/net/ocr-optimization/extract-text-images-from-pngs-with-c-batch-ocr-using-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# extrahera textbilder från PNG-filer med C# – Batch OCR med Aspose OCR

Har du någonsin behövt **extrahera textbilder** från en mapp med skannade PNG-filer men känt dig fast vid frågan “hur gör jag det snabbt?”? Du är inte ensam. I många verkliga projekt måste utvecklare **sätta max parallelism** så att dussintals sidor bearbetas på sekunder istället för minuter.  

I den här guiden går vi igenom ett komplett, körbart exempel som **konverterar skannade sidor**, kör **flera bild‑OCR**, och slutligen **läser png‑text** utan att svettas. Inga vaga “se dokumentationen”-länkar – bara kod du kan kopiera‑klistra, förklaringar till varför varje rad är viktig, och tips för att undvika vanliga fallgropar.

> **Pro tip:** Om du redan använder Aspose OCR någon annanstans kommer du att märka att samma `OcrEngine`‑klass dyker upp här, men vi kommer att justera dess konfiguration för sann parallell bearbetning.

---

## Vad du behöver

- **.NET 6+** (eller .NET Framework 4.6+). API‑et fungerar likadant, men nyare runtime‑versioner ger bättre trådhante­ring.  
- **Aspose.OCR for .NET** – installera via NuGet: `Install-Package Aspose.OCR`.  
- En mapp som innehåller några PNG‑skanningar (`page1.png`, `page2.png`, …).  
- En IDE eller editor du är bekväm med (Visual Studio, Rider, VS Code …).

Det är allt. Inga extra tjänster, inga moln‑nycklar, bara ren lokal bearbetning.

---

## extrahera textbilder – Ställa in Max Parallelism för Batch OCR

När du startar OCR på flera filer använder motorn som standard en enda tråd. Det är säkert men fruktansvärt långsamt. Genom att konfigurera `MaxDegreeOfParallelism` talar du om för motorn hur många trådar den får starta samtidigt.

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.Models;

class BatchExample
{
    static void Main()
    {
        // 1️⃣ Create an OCR engine and allow up to 4 parallel threads
        var ocrEngine = new OcrEngine
        {
            Configuration = { MaxDegreeOfParallelism = 4 }
        };
```

**Varför 4?**  
Fyra är en bra balans på de flesta moderna bärbara datorer – tillräckligt med kärnor för att hålla CPU:n sysselsatt, men inte så många att du kväver andra processer. Om du kör detta på en server med 16 kärnor, öka siffran till 12 eller 14 för en märkbar hastighetsökning.

---

## Konvertera skannade sidor – Bygga Image Stream‑samlingen

Aspose förväntar sig varje bild som ett `ImageStream`. Hjälp‑metoden `FromFile` läser filen, behåller den i minnet och överlämnar den till OCR‑motorn. Du kan också mata in ett `MemoryStream` om dina bilder kommer från en databas eller ett HTTP‑svar.

```csharp
        // 2️⃣ Build a collection of image streams to be processed
        List<ImageStream> imageStreams = new List<ImageStream>
        {
            ImageStream.FromFile(@"YOUR_DIRECTORY/page1.png"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/page2.png"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/page3.png")
        };
```

**Edge case:** Om någon fil saknas eller är korrupt kommer `FromFile` att kasta ett `FileNotFoundException`. Omslut konstruktionen med ett `try/catch` om du förväntar dig opålitlig indata.

---

## flera bild‑ocr – Utföra Batch OCR

Nu sker det tunga arbetet. `RecognizeBatch` startar upp till det antal trådar du angav tidigare, bearbetar varje bild och returnerar en lista med `OcrResult`‑objekt.

```csharp
        // 3️⃣ Perform batch OCR on the prepared images
        IList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);
```

Bakom kulisserna laddar varje tråd sin bild, kör det neurala nätverket och extraherar ren text. Resultatens ordning matchar ordningen i inmatningslistan, så du säkert kan mappa sida 1 → resultat 0, osv.

---

## läs png‑text – Visa det extraherade innehållet

Till sist loopar vi igenom resultaten och skriver ut den rena texten till konsolen. Här kan du skicka utdata till en fil, en databas eller till och med en efterföljande NLP‑tjänst.

```csharp
        // 4️⃣ Display the extracted text for each page
        for (int i = 0; i < ocrResults.Count; i++)
        {
            Console.WriteLine($"--- Page {i + 1} ---");
            Console.WriteLine(ocrResults[i].PlainText);
        }
    }
}
```

### Förväntad konsolutskrift

```
--- Page 1 ---
This is the first scanned line of text.
Another line appears here.

--- Page 2 ---
Second page starts with a header.
More content follows…

--- Page 3 ---
Final page ends with a signature.
```

Om du ser tomma sektioner, dubbelkolla att PNG‑filerna inte är helt vita – OCR kräver någon kontrast.

---

## Praktiska tips & vanliga fallgropar

| Situation | Vad du ska göra |
|-----------|-----------------|
| **Minnespåverkan** vid stora batcher | Bearbeta bilder i omgångar om 10‑20 filer, och anropa `GC.Collect()` om du märker toppar. |
| **Felaktig språkdete­ktion** | Sätt `ocrEngine.Configuration.Language = OcrLanguage.English;` (eller ditt målspråk) innan du anropar `RecognizeBatch`. |
| **Långsam prestanda trots parallellism** | Kontrollera att din SSD inte begränsar I/O; läs in alla filer i minnet först (som vi gör med `ImageStream.FromFile`). |
| **Saknade tecken** | Öka `ocrEngine.Configuration.DPI = 300;` för högre upplösning. |

---

## Utöka exemplet – Från PNG till PDF eller DOCX

Om du så småningom behöver **konvertera skannade sidor** till sökbara PDF‑filer, mata helt enkelt samma `ocrResults[i].PlainText` till ett PDF‑bibliotek (t.ex. Aspose.PDF) och lägg över texten som ett osynligt lager. Samma parallellism‑trick fungerar där också.

---

## Fullständig källkod (Klar att kopiera‑klistra)

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.Models;

class BatchExample
{
    static void Main()
    {
        // Step 1: Create an OCR engine and allow up to 4 parallel threads
        var ocrEngine = new OcrEngine
        {
            Configuration = { MaxDegreeOfParallelism = 4 }
        };

        // Step 2: Build a collection of image streams to be processed
        List<ImageStream> imageStreams = new List<ImageStream>
        {
            ImageStream.FromFile(@"YOUR_DIRECTORY/page1.png"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/page2.png"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/page3.png")
        };

        // Step 3: Perform batch OCR on the prepared images
        IList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);

        // Step 4: Display the extracted text for each page
        for (int i = 0; i < ocrResults.Count; i++)
        {
            Console.WriteLine($"--- Page {i + 1} ---");
            Console.WriteLine(ocrResults[i].PlainText);
        }
    }
}
```

Spara detta som `BatchExample.cs`, kör `dotnet run`, och se hur din konsol fylls med den text som tidigare var gömd i PNG‑skanningarna.

---

## Visuell sammanfattning

![extract text images example](images/ocr-batch.png){alt="exempel på extrahera textbilder"}

Diagrammet visar flödet: **PNG‑filer → ImageStream‑samling → OcrEngine (max parallelism) → OCR‑resultat → Konsol / efterföljande lagring**.

---

## Slutsats

Du har nu ett gediget, end‑to‑end‑recept för hur du **extraherar textbilder** i C# medan du **sätter max parallelism**, **konverterar skannade sidor**, hanterar **flera bild‑OCR**, och **läser png‑text** effektivt. Koden är självständig, förklaringarna täcker både “hur” och “varför”, och tipsen skyddar dig mot vanliga huvudvärk.

Vad blir nästa steg? Prova att byta ut PNG‑listan mot en dynamisk `Directory.GetFiles`‑loop, experimentera med olika trådtal, eller skicka utdata till en sökbar PDF. Samma mönster skalar till hundratals sidor med knappt någon extra kodrad.

Har du frågor eller ett knepigt edge‑case? lämna en kommentar nedan, och lycka till med kodandet!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}