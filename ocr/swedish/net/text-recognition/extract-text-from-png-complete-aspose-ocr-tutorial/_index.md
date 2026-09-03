---
category: general
date: 2026-01-09
description: Extrahera text från PNG snabbt med Aspose OCR. Lär dig hur du läser bildtext,
  förbättrar OCR‑noggrannheten och får rena resultat i C#.
draft: false
keywords:
- extract text from png
- read image text
- improve ocr accuracy
- extract text from image
- aspose ocr tutorial
language: sv
og_description: Extrahera text från PNG snabbt med Aspose OCR. Lär dig hur du läser
  bildtext, förbättrar OCR‑noggrannheten och får rena resultat i C#.
og_title: Extrahera text från PNG – Komplett Aspose OCR-handledning
tags:
- Aspose OCR
- C#
- Image Processing
title: Extrahera text från PNG – Komplett Aspose OCR-handledning
url: /sv/net/text-recognition/extract-text-from-png-complete-aspose-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahera text från PNG – Komplett Aspose OCR‑handledning

Har du någonsin behövt **extrahera text från PNG**‑filer men resultaten var fyllda med nonsens? Du är inte ensam. I många verkliga projekt – fakturor, kvitton eller skannade formulär – kan kvaliteten på OCR‑utdata avgöra om automatiseringspipeline lyckas eller misslyckas.  

I den här guiden visar vi dig ett **steg‑för‑steg**‑sätt för att läsa bildtext med Aspose OCR, lägga till en anpassad ordlista för att **förbättra OCR‑noggrannheten**, rensa bort brus och slutligen skriva ut en prydlig sträng. När du är klar har du en färdig C#‑konsolapp som på ett pålitligt sätt extraherar text från PNG‑bilder.

> **Vad du får med dig**  
> * Ett komplett, körbart kodexempel.  
> * Förståelse för varför en anpassad ordlista är viktig.  
> * Tips för att hantera kantfall som lågkontrast‑skanningar.  

## Förutsättningar

- .NET 6 SDK eller senare (koden riktar sig mot .NET 6, men .NET 5 fungerar också).  
- Visual Studio 2022 eller någon annan editor du föredrar.  
- En **PNG**‑bild du vill bearbeta – till exempel `invoice.png`.  
- **Aspose.OCR**‑NuGet‑paketet (`dotnet add package Aspose.OCR`).  

Inga extra konfigurationsfiler behövs; allt lever i en enda `.cs`‑fil.

## Steg 1 – Installera och referera Aspose OCR

Först hämtar du biblioteket till ditt projekt. Öppna en terminal i din lösningsmapp och kör:

```bash
dotnet add package Aspose.OCR
```

Den enda raden hämtar den senaste stabila versionen (från och med jan 2026, version 23.9). Paketet innehåller klassen `OcrEngine` som vi kommer att använda genom hela handledningen.

## Steg 2 – Initiera OCR‑motorn

Att skapa en `OcrEngine`‑instans är grunden. Tänk på det som att slå på en skanner som är redo att tolka pixlar.

```csharp
using Aspose.OCR;

// Initialize the OCR engine
var ocrEngine = new OcrEngine();
```

> **Proffstips:** Om du planerar att bearbeta många bilder i en loop, återanvänd samma `OcrEngine`‑instans. Den cachar interna resurser och snabbar upp efterföljande anrop.

## Steg 3 – Höj noggrannheten med en anpassad ordlista

Standard‑OCR är bra, men den kan snubbla på domänspecifika ord som “Aspose”, “OCR” eller “SDK”. Genom att lägga till dessa termer i en **anpassad ordlista** talar du om för motorn att dessa strängar är giltiga, vilket minskar felaktiga igenkänningar.

```csharp
// Define domain‑specific terms that the engine should recognize
ocrEngine.CustomDictionary = new HashSet<string>
{
    "Aspose",
    "OCR",
    "SDK",
    "invoice"
};
```

### Varför en anpassad ordlista hjälper

- **Statistiska modeller** bakom OCR väger vanliga språkmönster tungt. Ovanliga ord får låg sannolikhet och kan ersättas av liknande tecken.  
- Genom att explicit lista dem åsidosätter du modellens gissningar.  
- Det är särskilt praktiskt för **läsa bildtext** som innehåller produktkoder, förkortningar eller varumärkesnamn.

## Steg 4 – Känn igen text från PNG‑filen

Nu matar vi motorn med bildens sökväg. Metoden `RecognizeImage` returnerar en råsträng som fortfarande kan innehålla okända tecken (t.ex. “#@!”) som motorn inte kunde mappa.

```csharp
// Path to the PNG you want to process
string imagePath = @"YOUR_DIRECTORY/invoice.png";

// Perform OCR
string rawText = ocrEngine.RecognizeImage(imagePath);
```

> **Kantfall:** Om filen inte hittas kastar `RecognizeImage` ett `FileNotFoundException`. Omslut anropet med en try‑catch‑block i produktionskod.

## Steg 5 – Rensa resultatet med `CleanText`

Aspose OCR levereras med ett verktyg som tar bort tecken som flaggas som “okända”. Detta steg är avgörande för **extrahera text från bild**‑projekt där efterföljande parsers förväntar sig enbart alfanumeriska tecken och grundläggande skiljetecken.

```csharp
// Remove unknown tokens and extra whitespace
string cleanedText = ocrEngine.CleanText(rawText);
```

`CleanText`‑metoden normaliserar också radslut, vilket gör utdata säkra att lagra i databaser eller skicka till andra tjänster.

## Steg 6 – Skriv ut den rensade texten

Till sist visar eller sparar du resultatet. I en konsolapp gör `Console.WriteLine` jobbet.

```csharp
Console.WriteLine("=== Cleaned OCR Output ===");
Console.WriteLine(cleanedText);
```

När du kör programmet bör du se ett prydligt textblock som speglar innehållet i `invoice.png`. Om bilden innehåller ordet “Aspose” säkerställer den anpassade ordlistan att det visas korrekt istället för något som “A5p0se”.

## Fullt fungerande exempel

Sätter vi ihop allt får vi den kompletta `Program.cs` som du kan kopiera‑klistra in i ett nytt konsolprojekt:

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize the OCR engine
        var ocrEngine = new OcrEngine();

        // 2️⃣ Add domain‑specific terms to improve OCR accuracy
        ocrEngine.CustomDictionary = new HashSet<string>
        {
            "Aspose",
            "OCR",
            "SDK",
            "invoice"
        };

        // 3️⃣ Path to your PNG file (adjust as needed)
        string imagePath = @"YOUR_DIRECTORY/invoice.png";

        try
        {
            // 4️⃣ Recognize raw text from the image
            string rawText = ocrEngine.RecognizeImage(imagePath);

            // 5️⃣ Clean up unknown tokens
            string cleanedText = ocrEngine.CleanText(rawText);

            // 6️⃣ Show the result
            Console.WriteLine("=== Cleaned OCR Output ===");
            Console.WriteLine(cleanedText);
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error processing image: {ex.Message}");
        }
    }
}
```

**Förväntad utdata** (förutsatt att PNG‑filen innehåller en enkel faktura):

```
=== Cleaned OCR Output ===
Invoice #12345
Date: 01/08/2026
Total: $1,250.00
Thank you for your business!
```

Om du ser främmande symboler, dubbelkolla bildkvaliteten eller utöka den anpassade ordlistan med fler termer.

## Bonus: Hantera lågkvalitativa skanningar

Ibland är PNG‑filer skannade med 72 dpi eller har kraftiga komprimeringsartefakter. Här är några snabba knep för att **förbättra OCR‑noggrannheten** utan att lämna C#:

1. **Förbehandla bilden** med ett bibliotek som `SixLabors.ImageSharp` – öka kontrast, konvertera till gråskala eller applicera en lätt oskärpa för att minska brus.  
2. **Ställ in egenskapen `Resolution`** på `OcrEngine` (t.ex. `ocrEngine.Resolution = 300;`) för att tala om för motorn att behandla bilden som högupplöst.  
3. **Aktivera språkpaket** om du arbetar med icke‑engelsk text (`ocrEngine.Language = Language.English;`).

Alla tre metoder kan läggas till innan anropet till `RecognizeImage`.

## Vanliga frågor

- **Fungerar detta med andra bildformat?**  
  Ja. `RecognizeImage` accepterar JPEG, BMP, TIFF och till och med PDF (som en bildbehållare). Samma steg gäller.

- **Kan jag extrahera text från flera PNG‑filer i en mapp?**  
  Absolut. Lägg in kärnlogiken i en `foreach (var file in Directory.GetFiles(folder, "*.png"))`‑loop och lagra varje resultat i en lista eller skriv till separata filer.

- **Vad händer om jag behöver textens koordinater?**  
  Aspose OCR erbjuder även `OcrResult`‑objekt som innehåller avgränsningsrutor. Använd `ocrEngine.RecognizeImageToResult(imagePath)` för det avancerade scenariot.

## Slutsats

Vi har gått igenom en **komplett, end‑to‑end**‑lösning för **extrahera text från PNG**‑filer med Aspose OCR. Genom att initiera motorn, mata in en **anpassad ordlista**, rensa den råa utdata och hantera några vanliga fallgropar kan du på ett pålitligt sätt **läsa bildtext** och **förbättra OCR‑noggrannheten** i dina egna C#‑applikationer.

Redo för nästa steg? Prova att byta PNG mot ett skannat kvitto, lägg till fler domänspecifika ord i ordlistan eller integrera utdata med en databas för automatiserad fakturabehandling. Himlen är gränsen när du kombinerar Aspose OCR med .NET:s rika ekosystem.

Happy coding, and may your OCR always be spot‑on!  

![Exempel på extraherad text från png](/images/extract-text-from-png.png "extrahera text från png – Aspose OCR‑demo")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}