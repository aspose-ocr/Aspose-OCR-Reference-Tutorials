---
category: general
date: 2026-01-01
description: Känn igen rysk text omedelbart med Aspose OCR C#. Lär dig att känna igen
  kinesisk text, läsa antalet sidor i en PDF och konvertera PDF-sidans text i en handledning.
draft: false
keywords:
- recognize russian text
- aspose ocr c#
- recognize chinese text
- read pdf page count
- convert pdf page text
language: sv
og_description: Känn igen rysk text snabbt med Aspose OCR C#. Denna handledning täcker
  också hur man känner igen kinesisk text, läser antalet sidor i en PDF och konverterar
  PDF-sidans text.
og_title: Känn igen rysk text med Aspose OCR C# – Komplett guide
tags:
- Aspose OCR
- C#
- PDF processing
title: Känn igen rysk text med Aspose OCR C# – Fullständig guide för flersidiga PDF-filer
url: /sv/net/text-recognition/recognize-russian-text-with-aspose-ocr-c-full-multi-page-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# känna igen rysk text med Aspose OCR C# – Komplett flersidig PDF‑handledning

Har du någonsin behövt **igenkänna rysk text** i en PDF som blandar språk, och undrat hur du gör det utan att behöva ett separat verktyg för varje sida? Du är inte ensam. I många verkliga projekt får du en enda PDF som innehåller engelska, ryska och till och med kinesiska på olika sidor, och du vill ändå ha en enhetlig, ren textutmatning.

I den här guiden visar vi exakt hur du **igenkänner rysk text** (och andra språk) med **Aspose OCR C#**, samtidigt som vi demonstrerar hur du **läser PDF‑sidantalet**, **igenkänner kinesisk text**, och **konverterar PDF‑sidans text** till en praktisk konsolutskrift. Inga externa tjänster, inga dolda steg – bara ren C#‑kod som du kan kopiera, klistra in och köra.

> **Vad du får med dig**  
> * En körbar C#‑konsolapp som bearbetar en flersidig PDF.  
> * Språkval per sida (ryska, kinesiska, engelska).  
> * Tekniker för att fråga PDF‑filens sidantal och extrahera varje sidas text.  
> * Tips, fallgropar och utökningar du kan tillämpa i egna projekt.

---

## Förutsättningar

- .NET 6.0 eller senare (koden fungerar också på .NET Framework 4.7+).  
- **Aspose.OCR for .NET** NuGet‑paket installerat (`dotnet add package Aspose.OCR`).  
- En PDF‑fil som innehåller blandade språk; i demonstrationen refererar vi till `mixed_lang.pdf`.  
- Grundläggande kunskap om C#‑konsolapplikationer.

Om du saknar någon av dessa, hämta den senaste Aspose OCR från NuGet och placera din PDF någonstans som är åtkomlig från projektmappen.

---

## Steg 1 – Initiera Aspose OCR‑motorn

Det allra första du behöver är en instans av `OcrEngine`. Detta objekt innehåller alla inställningar (som språk) och utför det tunga arbetet.

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;

class MultiPageDemo
{
    static void Main()
    {
        // Create the OCR engine – this is where we’ll set language per page
        OcrEngine ocrEngine = new OcrEngine();
```

> **Varför detta är viktigt:**  
> Motorn är återanvändbar, så vi slösar inte minne genom att skapa en ny instans för varje sida. Genom att återanvända den kan vi också byta språk i farten, vilket är avgörande för att **igenkänna rysk text** på en sida och **igenkänna kinesisk text** på en annan.

---

## Steg 2 – Läs in PDF‑filen och ta reda på hur många sidor den har

Innan vi börjar igenkänna behöver vi PDF‑objektet och dess sidantal. Aspose OCR behandlar varje sida som en `OcrImage`.

```csharp
        // Load the multi‑page PDF
        OcrImage multiPageImage = OcrImage.FromFile(@"YOUR_DIRECTORY/mixed_lang.pdf");

        // Print the total number of pages – this answers the “read pdf page count” question
        Console.WriteLine($"PDF contains {multiPageImage.PageCount} pages.");
```

> **Tips:** Om PDF‑filen är stor kan du vilja läsa antalet sidor först och bestämma om du ska bearbeta alla sidor eller bara ett urval.

---

## Steg 3 – Mappa varje sida till önskat språk

Aspose OCR stödjer många språk, men du måste tala om för den vilket som ska användas för varje sida. Nedan skapar vi en `Dictionary<int, OcrLanguage>` där nyckeln är det noll‑baserade sidindexet.

```csharp
        // Define which language each page should be read with
        var languageMap = new Dictionary<int, OcrLanguage>
        {
            { 0, OcrLanguage.English },   // Page 1 – English
            { 1, OcrLanguage.Russian },   // Page 2 – Russian (our primary focus)
            { 2, OcrLanguage.Chinese }    // Page 3 – Chinese
        };
```

> **Varför detta är avgörande:**  
> Utan denna karta skulle OCR‑motorn försöka med ett enda standardspråk för varje sida, vilket ger förvrängd utskrift för rysk eller kinesisk text. Detta steg möjliggör direkt **igenkänna rysk text** och **igenkänna kinesisk text** korrekt.

---

## Steg 4 – Loopa igenom alla sidor, sätt språk och igenkänn text

Nu itererar vi över varje sida, byter språk enligt vår karta och anropar `Recognize`. Resultatet lagras i `OcrResult`, varifrån vi extraherar ren text.

```csharp
        // Process each page one by one
        for (int pageIndex = 0; pageIndex < multiPageImage.PageCount; pageIndex++)
        {
            // Choose language – default to English if we haven’t specified one
            ocrEngine.Settings.Language = languageMap.ContainsKey(pageIndex)
                                          ? languageMap[pageIndex]
                                          : OcrLanguage.English;

            // Perform OCR on the current page
            var pageResult = ocrEngine.Recognize(multiPageImage.GetPage(pageIndex));

            // Output the recognized text – this is the “convert pdf page text” step
            Console.WriteLine($"--- Page {pageIndex + 1} ({ocrEngine.Settings.Language}) ---");
            Console.WriteLine(pageResult.Text);
            Console.WriteLine(); // Blank line for readability
        }
    }
}
```

### Förväntad konsolutskrift

```
PDF contains 3 pages.
--- Page 1 (English) ---
This is an English paragraph on the first page.

--- Page 2 (Russian) ---
Это русский текст на второй странице.

--- Page 3 (Chinese) ---
这是第三页的中文文本。
```

> **Förklaring av flödet:**  
> * Loopen respekterar **läsa PDF‑sidantalet** som vi skrev ut tidigare.  
> * Genom att byta `ocrEngine.Settings.Language` varje iteration garanterar vi korrekt **igenkänna rysk text** på sida 2 och **igenkänna kinesisk text** på sida 3.  
> * `Console.WriteLine`‑satserna konverterar effektivt **PDF‑sidans text** till en mänskligt läsbar sträng.

---

## Steg 5 – Kör, verifiera och justera

1. Bygg projektet (`dotnet build`).  
2. Kör det (`dotnet run`).  
3. Jämför konsolutskriften med den ursprungliga PDF‑filen.  

Om du märker saknade tecken, överväg:

- **Öka OCR‑noggrannheten** genom att sätta `ocrEngine.Settings.DetectTextOrientation = true;`.  
- **Tillhandahålla ett anpassat språkpaket** om de inbyggda ryska eller kinesiska ordböckerna är föråldrade.  
- **Justera DPI** när du läser in PDF‑filen (`OcrImage.FromFile(path, 300)`), vilket kan förbättra igenkänning på lågupplösta skanningar.

---

## Bonus: Hantera kantfall

### Vad händer om en sidas språk inte finns i kartan?

Koden faller redan tillbaka till engelska, men du kan också lägga till en fallback som loggar en varning:

```csharp
if (!languageMap.TryGetValue(pageIndex, out var lang))
{
    Console.WriteLine($"Warning: No language defined for page {pageIndex + 1}. Using English.");
    lang = OcrLanguage.English;
}
ocrEngine.Settings.Language = lang;
```

### Kan vi bearbeta PDF‑filer med fler än tre språk?

Absolut. Utöka `languageMap` med ytterligare index och stödjade `OcrLanguage`‑värden (t.ex. `OcrLanguage.French`). Loopen hanterar vilket antal sidor som helst.

### Hur exporterar vi resultaten till en fil istället för konsolen?

Byt ut `Console.WriteLine`‑anropen mot `File.AppendAllText("output.txt", …)` eller använd en `StringBuilder` som du skriver ut en gång efter loopen.

---

## Bildillustration

![igenkänna rysk text exempel](/images/recognize-russian-text.png "Skärmbild som visar OCR‑utdata för rysk text")

*Bilden ovan demonstrerar konsolutskriften när **igenkänna rysk text** utförs på en PDF med blandade språk.*

---

## Slutsats

Vi har gått igenom ett komplett, end‑to‑end‑exempel som visar hur du **igenkänner rysk text** (och även **igenkänner kinesisk text**) från en flersidig PDF med **Aspose OCR C#**. Genom att läsa PDF‑filens sidantal, mappa varje sida till rätt språk och loopa igenom dokumentet kan du **konvertera PDF‑sidans text** till rena strängar redo för lagring, indexering eller vidare analys.

Sammanfattningsvis:

- **Initiera** en enda `OcrEngine`.  
- **Läs** in PDF‑filen och **läsa PDF‑sidantalet**.  
- **Mappa** sidor till språk (ryska, kinesiska osv.).  
- **Iterera**, sätt `ocrEngine.Settings.Language` och **igenkänn** varje sida.  
- **Skriv ut** eller spara den extraherade texten.

Känn dig fri att anpassa detta mönster till större dokument, lägga till felhantering eller koppla resultaten till ett sökindex. Kärnidén – språkval per sida – förblir densamma, och den gör pålitlig **igenkänna rysk text** möjlig i PDF‑filer med blandade språk.

Har du ett annat scenario, som att skanna bilder istället för PDF‑filer? Samma motor fungerar; byt bara ut `OcrImage.FromFile` mot `OcrImage.FromStream` eller `FromBitmap`. Lycka till med kodandet, och må din OCR alltid vara exakt!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}