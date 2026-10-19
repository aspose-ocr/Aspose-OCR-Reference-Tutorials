---
category: general
date: 2026-04-04
description: Hur man använder OCR snabbt och säkert. Lär dig att extrahera text från
  bild, konvertera DJVU till text och ladda bild för OCR med Aspose.OCR.
draft: false
keywords:
- how to use OCR
- extract text from image
- convert djvu to text
- load image for OCR
- extract text from djvu
language: sv
og_description: Hur man använder OCR i C# för att extrahera text från bildfiler och
  DJVU‑dokument. Steg‑för‑steg‑handledning med fullständig kod.
og_title: Hur man använder OCR i C# – Komplett guide
tags:
- OCR
- C#
- Aspose
title: Hur man använder OCR i C# – Extrahera text från bilder och DJVU‑filer
url: /sv/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-images-and-djvu-files/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Så använder du OCR i C# – Extrahera text från bilder och DJVU-filer

Har du någonsin funderat **hur man använder OCR** för att dra ut ord från en skannad sida utan att skriva in dem manuellt? Du är inte ensam. I många projekt—oavsett om du digitaliserar gamla böcker eller extraherar data från kvitton—är det en daglig smärta att få text från en bild. Den goda nyheten? Med Aspose.OCR kan du göra det på några få rader, även när källan är en DJVU‑fil.

I den här guiden går vi igenom allt du behöver för att **extrahera text från bild**‑filer, **ladda bild för OCR**, och till och med **konvertera DJVU till text** med C#. När du är klar har du en färdig konsolapp som skriver ut den igenkända texten direkt i konsolen. Ingen magi, inga extra beroenden, bara ren C# och Aspose.

## Vad du kommer att lära dig

- Hur du installerar och refererar Aspose.OCR‑biblioteket.
- Den exakta koden som behövs för att **ladda bild för OCR**, oavsett om det är en PNG, JPEG eller en DJVU‑sida.
- Hur du anropar motorn och hämtar resultatet.
- Tips för att hantera stora dokument och vanliga fallgropar.
- Ett komplett, körbart exempel som du kan kopiera‑klistra in i Visual Studio.

> **Förutsättning:** .NET 6.0 eller senare och en giltig Aspose.OCR‑licens (eller en gratis provversion). Om du ännu inte har biblioteket, hämta det från NuGet med `dotnet add package Aspose.OCR`.

---

## Hur man använder OCR med Aspose i C#

Det här är kärnsteg där vi faktiskt svarar på frågan **hur man använder OCR** i ett C#‑projekt. Koden nedan är ett komplett program; du kan klistra in den i en ny konsolapp och trycka F5.

```csharp
using System;
using Aspose.OCR;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create the OCR engine instance.
            var ocrEngine = new OcrEngine();

            // Step 2: Load the image (or DJVU page) you want to analyze.
            // Replace the path with your own file location.
            ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/book-page.djvu");

            // Step 3: Run the recognition process.
            OcrResult ocrResult = ocrEngine.Recognize();

            // Step 4: Output the extracted text.
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

**Varför detta fungerar:**  
- `OcrEngine` är ingångspunkten; den abstraherar det tunga arbetet med bildförbehandling, språkdetection och teckenklassificering.  
- `ImageStream.FromFile` kan hantera många format, inklusive DJVU, vilket betyder att du kan **konvertera DJVU till text** utan ett extra konverteringssteg.  
- `Recognize()` returnerar ett `OcrResult`‑objekt som innehåller ren‑text‑utdata, förtroendesiffror och till och med avgränsningsrutor om du behöver dem senare.

Kör programmet så får du något i stil med:

```
=== OCR Result ===
In the beginning God created the heavens and the earth.
```

Det var allt—din första lyckade **extrahera text från DJVU**‑operation.

![exempel på hur man använder OCR](/images/ocr-demo.png "Skärmbild som visar hur man använder OCR i en C#‑konsolapp")

*Alt text: “exempel på hur man använder OCR” skärmbild av konsolutdata.*

---

## Ladda bild för OCR

Innan motorn kan läsa något måste du **ladda bild för OCR** korrekt. Aspose stöder de flesta rasterformat direkt, men några tips kan göra igenkänningen smidigare:

- **Ändra storlek på stora bilder** till maximalt 2000 px på den längsta sidan. Överdimensionerade filer ökar minnesanvändningen och kan sakta ner motorn.  
- **Konvertera färgbilder till gråskala** om du märker brusiga bakgrunder. Använd `ocrEngine.Image = ImageStream.FromFile(path).ConvertToGrayscale();`.  
- **Ställ in DPI manuellt** för lågupplösta skanningar (`ocrEngine.Image.DpiX = 300; ocrEngine.Image.DpiY = 300;`).

Dessa justeringar är valfria men förbättrar ofta noggrannheten när du **extraherar text från bild**‑filer som skannade kvitton.

---

## Extrahera text från bild – Bästa praxis

När du arbetar med vanliga bildformat (PNG, JPEG, BMP) är stegen desamma, men du kan finjustera motorn:

```csharp
ocrEngine.Image = ImageStream.FromFile("sample.png");

// Optional: enable language packs for better accuracy.
ocrEngine.Language = Language.English;

// Optional: set recognition mode to auto.
ocrEngine.RecognitionMode = RecognitionMode.Auto;
```

- **Språkval** är viktigt. Om du bearbetar flerspråkiga dokument, sätt `ocrEngine.Language = Language.Multilingual;`.  
- **RecognitionMode** kan vara `Auto`, `Fast` eller `Accurate`. `Accurate` ger högre kvalitet på bekostnad av hastighet—använd den för arkiveringsuppgifter.

---

## Konvertera DJVU till text – Hantera flersidiga filer

DJVU‑filer innehåller ofta flera sidor. Aspose behandlar varje sida som ett separat bildflöde, så du kan loopa igenom dem:

```csharp
using Aspose.OCR;
using System.Collections.Generic;

var ocrEngine = new OcrEngine();
List<string> allPagesText = new List<string>();

int pageCount = ImageStream.GetPageCount("book.djvu");
for (int i = 1; i <= pageCount; i++)
{
    ocrEngine.Image = ImageStream.FromFile("book.djvu", i); // Load page i
    OcrResult result = ocrEngine.Recognize();
    allPagesText.Add(result.Text);
}

// Combine all pages into a single string.
string fullText = string.Join("\n--- Page Break ---\n", allPagesText);
Console.WriteLine(fullText);
```

**Varför loopa?**  
DJVU‑filer är i princip en stapel av bilder. Genom att iterera över varje sida **extraherar du text från DJVU** i rätt ordning och bevarar det ursprungliga dokumentflödet.

---

## Vanliga fallgropar och pro‑tips

| Problem | Varför det händer | Lösning |
|------|----------------|-----|
| **Skräptecken** | Låg DPI eller hög kompression | Skala upp bilden, sätt `ocrEngine.Image.DpiX/Y = 300` |
| **Långsam bearbetning** | Användning av `Accurate`‑läge på stora filer | Byt till `Fast`‑läge för massjobb |
| **Saknad språkstöd** | Standardspråket är bara engelska | Ladda ytterligare språkpaket (`ocrEngine.Language = Language.Spanish;`) |
| **Minnesbrist** | Laddar många högupplösta sidor samtidigt | Bearbeta sidor en efter en och frigör resurser (`ocrEngine.Dispose();`) |

Ett snabbt **pro‑tips**: anropa alltid `ocrEngine.Dispose()` när du är klar med en sida. Det frigör inhemska resurser och förhindrar subtila minnesläckor som kan krascha långvariga tjänster.

---

## Testa din OCR‑pipeline

För att verifiera att allt fungerar, prova dessa enkla kontroller:

1. **Skriv ut längden** på den igenkända strängen: `Console.WriteLine($"Characters recognized: {ocrResult.Text.Length}");`  
2. **Jämför mot känd text** med ett enkelt diff‑bibliotek om du har en sanningsgrund.  
3. **Logga förtroendesiffror** (`ocrResult.Confidence`) för att automatiskt upptäcka lågkvalitetssidor.

Om förtroendet konsekvent ligger under 0,7, gå tillbaka till bildförbehandlingsstegen som nämndes tidigare.

---

## Nästa steg

Nu när du vet **hur man använder OCR**, fundera på att utöka ditt arbetsflöde:

- **Batch‑bearbetning**: Packa in loopen i en `Parallel.ForEach` för att snabba upp stora samlingar.  
- **Export till PDF**: Använd Aspose.PDF för att bädda in den igenkända texten som ett dolt lager för sökbara PDF‑filer.  
- **Integrera med AI**: Skicka de extraherade strängarna till en språkmodell för sammanfattning eller entitetsutvinning.

Alla dessa bygger på samma grund du just har lagt, och varje steg drar nytta av samma **extrahera text från bild**‑principer som vi gått igenom.

---

## Slutsats

Vi har gjort en djupdykning i **hur man använder OCR** i C# med Aspose, och täckt allt från att ladda en bild, **extrahera text från bild**, hantera **DJVU**‑filer och felsöka vanliga problem. Det kompletta, körbara exemplet ovan ger dig en solid startpunkt, och tipsen som sprids genom texten bör hjälpa dig att anpassa lösningen till verkliga projekt.  

Prova det, justera inställningarna för dina specifika dokument, så förvandlar du skannade sidor till sökbar text på nolltid. Har du frågor eller en knepig fil som vägrar samarbeta? Lämna en kommentar—lycka till med kodandet!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}