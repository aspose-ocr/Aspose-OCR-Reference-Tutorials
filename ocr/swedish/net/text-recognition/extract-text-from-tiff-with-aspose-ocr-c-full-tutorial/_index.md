---
category: general
date: 2026-01-09
description: Extrahera text från TIFF‑filer med Aspose OCR i C#. Lär dig hur du får
  de första 50 tecknen i varje resultat i den här steg‑för‑steg‑handledningen.
draft: false
keywords:
- extract text from tiff
- get first 50 characters
- aspose ocr c# tutorial
language: sv
og_description: Extrahera text från TIFF med Aspose OCR i C#. Den här guiden visar
  hur du får de första 50 tecknen i varje OCR‑resultat, steg för steg.
og_title: Extrahera text från TIFF med Aspose OCR – Komplett C#‑guide
tags:
- Aspose OCR
- C#
- TIFF processing
title: Extrahera text från TIFF med Aspose OCR C# – Fullständig handledning
url: /sv/net/text-recognition/extract-text-from-tiff-with-aspose-ocr-c-full-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahera text från TIFF – Komplett Aspose OCR C# handledning

Har du någonsin behövt **extrahera text från TIFF**‑bilder men varit osäker på vilket bibliotek du ska lita på? Du är inte ensam. Många utvecklare stöter på problem när de försöker hämta sökbar text från flersidiga TIFF‑filer, särskilt när prestanda är viktigt.

I den här **aspose ocr c# tutorial** går vi igenom ett färdigt exempel som inte bara extraherar hela texten utan också visar hur du **hämtar de första 50 tecknen** på varje sida för snabba förhandsvisningar. När du är klar har du ett självständigt program som du kan lägga in i vilket .NET‑projekt som helst.

## Vad du behöver

- .NET 6 (eller någon nyare .NET‑version) – koden kompileras med både .NET Core och .NET Framework.  
- En aktiv Aspose.OCR för .NET‑licens (du kan börja med en gratis provperiod).  
- En mapp som innehåller en eller flera `.tif`‑filer du vill bearbeta.  
- Visual Studio, VS Code eller någon annan IDE du föredrar – exemplet är ren C# så valet av editor är irrelevant.

> **Proffstips:** Om du kör på en CI‑server, lägg till Aspose.OCR NuGet‑paketet (`Aspose.OCR`) i din projektfil; biblioteket är helt hanterat och har inga inhemska beroenden.

## Steg 1: Installera Aspose OCR NuGet‑paketet

Först och främst, låt oss lägga till OCR‑motorn i projektet. Öppna en terminal i din lösningsmapp och kör:

```bash
dotnet add package Aspose.OCR
```

Detta kommando hämtar den senaste stabila versionen (från och med jan 2026 är den 23.9) och uppdaterar automatiskt din `.csproj`. Ingen manuell DLL‑hantering behövs.

## Steg 2: Initiera OCR‑motorn

Nu skapar vi en instans av `OcrEngine`. Tänk på den som “hjärnan” som kommer att läsa varje TIFF‑sida.

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;
using System.IO;

namespace TiffOcrDemo
{
    class Program
    {
        static void Main()
        {
            // Step 2: Initialize the OCR engine
            var ocrEngine = new OcrEngine();

            // Optional: tweak recognition settings if you know the language
            // ocrEngine.Language = Language.English;
            // ocrEngine.Dpi = 300; // higher DPI can improve accuracy
```

Varför instansierar vi motorn bara en gång? Eftersom `RecognizeImages` kan ta emot en samling av filsökvägar, vilket låter motorn återanvända interna buffertar och dramatiskt snabba upp batch‑bearbetning.

## Steg 3: Samla alla TIFF‑filer i ett anrop

Istället för att själv loopa över katalogen låter vi .NET göra det tunga arbetet. Metoden `Directory.GetFiles` returnerar ett `IEnumerable<string>` som vi kan skicka direkt till OCR‑anropet.

```csharp
            // Step 3: Collect all TIFF images from the batch folder
            IEnumerable<string> imageFiles = Directory.GetFiles(@"YOUR_DIRECTORY/Batch", "*.tif");

            if (!imageFiles.Any())
            {
                Console.WriteLine("No TIFF files found in the specified folder.");
                return;
            }
```

> **Vad händer om mina bilder är JPEG eller PNG?** Ändra bara sökmönstret (`"*.jpg"` eller `"*.*"`). Aspose OCR fungerar med alla vanliga rasterformat.

## Steg 4: Kör OCR på hela samlingen

Här är den magiska raden som bearbetar varje fil i ett enda anrop. Metoden returnerar en dictionary där nyckeln är filsökvägen och värdet är ett `OcrResult`‑objekt som innehåller den igenkända texten.

```csharp
            // Step 4: Perform OCR on the entire collection in one call
            var ocrResults = ocrEngine.RecognizeImages(imageFiles);
```

Varför batch‑processa? Det minskar overheaden av att upprepade gånger ladda OCR‑motorn, och på maskiner med flera kärnor parallelliserar Aspose arbetet internt, vilket ger en märkbar hastighetsökning.

## Steg 5: Visa en förhandsvisning – Hämta de första 50 tecknen

De flesta UI‑scenarier behöver bara ett utdrag, inte hela dokumentet. Vi extraherar de första 50 tecknen (eller färre om sidan är kort) och skriver ut dem tillsammans med filnamnet.

```csharp
            // Step 5: Display each file name with a preview of the recognized text
            foreach (var entry in ocrResults) // entry.Key = file path, entry.Value = OcrResult
            {
                string fileName = Path.GetFileName(entry.Key);
                string fullText = entry.Value.Text ?? string.Empty;
                string preview = fullText.Substring(0, Math.Min(50, fullText.Length));

                Console.WriteLine($"{fileName} → {preview}...");
            }
        }
    }
}
```

Raden `Math.Min(50, fullText.Length)` garanterar att vi aldrig överskrider strängens gränser – en liten skyddsåtgärd som förhindrar ett `ArgumentOutOfRangeException` när OCR‑resultatet är kortare än 50 tecken.

### Förväntad konsolutmatning

Om du har två TIFF‑filer (`invoice1.tif` och `receipt2.tif`) kan konsolen visa:

```
invoice1.tif → Invoice Number: 2025-07-14 Date: 07/14/...
receipt2.tif → Store: QuickMart Total: $23.45 Date: ...
```

Varje rad avslutas med en ellipsis (`...`) för att indikera att förhandsvisningen bara är början på ett längre textblock.

## Steg 6: Hantera kantfall och vanliga fallgropar

### Tomma eller korrupta filer

Om en fil inte kan läsas returnerar `RecognizeImages` fortfarande en post med en tom `Text`‑egenskap. Du kan filtrera bort dem:

```csharp
if (string.IsNullOrWhiteSpace(fullText))
{
    Console.WriteLine($"{fileName} → (No recognizable text)");
    continue;
}
```

### Stora batcher

Att bearbeta tusentals TIFF‑filer kan förbruka mycket minne. I sådana fall, använd överlagringen som accepterar en `Stream` per bild, eller bearbeta listan i mindre delar:

```csharp
var batches = imageFiles.Chunk(100); // .NET 6+ extension
foreach (var batch in batches)
{
    var batchResults = ocrEngine.RecognizeImages(batch);
    // handle batchResults...
}
```

### Språk‑ och teckensnittsstöd

Om dina dokument innehåller icke‑latinska tecken, ange språket innan du anropar `RecognizeImages`:

```csharp
ocrEngine.Language = Language.Spanish; // or Language.MultiLanguage
```

Denna lilla justering kan öka noggrannheten avsevärt.

## Steg 7: Fullt fungerande exempel (Klar‑för‑kopiering)

Nedan är det kompletta programmet som du kan klistra in i ett nytt konsolprojekt (`dotnet new console`) och köra som det är (byt bara ut `YOUR_DIRECTORY/Batch` mot den faktiska sökvägen).

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;

namespace TiffOcrDemo
{
    class Program
    {
        static void Main()
        {
            // Initialize the OCR engine
            var ocrEngine = new OcrEngine();

            // Optional: set language or DPI for better accuracy
            // ocrEngine.Language = Language.English;
            // ocrEngine.Dpi = 300;

            // Collect all TIFF files from the batch folder
            IEnumerable<string> imageFiles = Directory.GetFiles(@"YOUR_DIRECTORY/Batch", "*.tif");

            if (!imageFiles.Any())
            {
                Console.WriteLine("No TIFF files found in the specified folder.");
                return;
            }

            // Perform OCR on the entire collection
            var ocrResults = ocrEngine.RecognizeImages(imageFiles);

            // Show a preview – get first 50 characters of each result
            foreach (var entry in ocrResults)
            {
                string fileName = Path.GetFileName(entry.Key);
                string fullText = entry.Value.Text ?? string.Empty;

                if (string.IsNullOrWhiteSpace(fullText))
                {
                    Console.WriteLine($"{fileName} → (No recognizable text)");
                    continue;
                }

                string preview = fullText.Substring(0, Math.Min(50, fullText.Length));
                Console.WriteLine($"{fileName} → {preview}...");
            }
        }
    }
}
```

Kör programmet med `dotnet run`. Du bör se en kort förhandsvisning för varje TIFF‑fil, vilket bekräftar att du framgångsrikt **extraherat text från TIFF**‑bilder med Aspose OCR.

## Vanliga frågor (FAQ)

**Q: Fungerar detta med flersidiga TIFF‑filer?**  
A: Ja. Aspose OCR behandlar varje sida som en separat bild internt, så en flersidig TIFF ger en enda sammansatt sträng per fil. Du kan dela upp den senare om så behövs.

**Q: Hur exakt är OCR:n direkt ur lådan?**  
A: För rena, högupplösta skanningar (300 DPI eller högre) kan du förvänta dig >95 % noggrannhet på engelsk text. Förbehandling (rättning, binarisering) kan öka den ännu mer.

**Q: Kan jag skriva ut resultaten till en CSV‑fil?**  
A: Absolut. Byt ut `Console.WriteLine` mot en `StreamWriter` och skriv raderna `fileName,preview`. Kom ihåg att escapera kommatecken i förhandsvisningstexten.

## Nästa steg och relaterade ämnen

- **Spara OCR‑resultat** – Lagra hela texten i en databas för sökbara arkiv.  
- **Kombinera med PDF‑konvertering** – Använd Aspose.PDF för att bädda in den extraherade texten tillbaka i sökbara PDF‑filer.  
- **Batch‑bearbetning på Azure Functions** – Skala ut OCR‑arbetet utan att hantera servrar.  

Alla dessa tillägg knyter tillbaka till huvudidén att **extrahera text från TIFF** effektivt, samtidigt som du fortfarande kan **hämta de första 50 tecknen** för snabba UI‑förhandsvisningar.

---

*Lycka till med kodandet! Om du stöter på några konstigheter, lämna en kommentar nedan – jag gör mitt bästa för att hjälpa dig finjustera OCR‑pipeline:n.* 

![Extract text from TIFF using Aspose OCR](https://example.com/images/extract-text-from-tiff.png "Extract text from TIFF using Aspose OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}