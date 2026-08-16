---
category: general
date: 2026-04-03
description: Lär dig hur du utför OCR i C# och extraherar text från en bild med Aspose
  OCR, med stavningskontroll för ryska språket.
draft: false
keywords:
- how to perform OCR
- extract text from image
- convert image to text
- how to spell check
- ocr russian language
language: sv
og_description: Lär dig hur du utför OCR i C# och extraherar text från en bild med
  Aspose OCR, med stavningskontroll för ryska språket.
og_title: Hur man utför OCR i C# – Extrahera text från bild
tags:
- OCR
- C#
- Aspose
- SpellCheck
title: Hur man utför OCR i C# – Extrahera text från en bild
url: /sv/net/text-recognition/how-to-perform-ocr-in-c-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man utför OCR i C# – Extrahera text från bild

Har du någonsin undrat **hur man utför OCR** på ett foto av en handskriven lapp? Kanske har du en skannad kvitto, en skylt på ett främmande språk, eller en PDF‑sida som vägrar att kopiera‑klistra. Den goda nyheten? Med några rader C# och Aspose OCR‑biblioteket kan du förvandla den bilden till redigerbar text på ett ögonblick.  

I den här guiden kommer vi inte bara att visa dig **hur man utför OCR**, vi kommer också att gå igenom **extrahera text från bild**, **konvertera bild till text**, och till och med **hur man stavningskontrollerar** resultatet när du arbetar med ryska dokument. Låter det som mycket? Häng kvar – vi kommer att bryta ner allt steg för steg.

## Vad du kommer att lära dig

Vid slutet av den här tutorialen kommer du att kunna:

* Konfigurera Aspose OCR för stöd av ryska språket.  
* Ladda en bildfil och kör optisk teckenigenkänning för att **extrahera text från bild**.  
* Använd den inbyggda stavningskontrollen för att automatiskt korrigera felstavade ord – det perfekta svaret på “**hur man stavningskontrollerar**” OCR‑utdata.  
* Skriv ut den rensade strängen till konsolen, redo för vidare bearbetning eller lagring.

**Förutsättningar** – du behöver:

* .NET 6.0 eller senare (koden fungerar även med .NET Framework 4.8).  
* En giltig Aspose OCR‑licens eller en tillfällig utvärderingsnyckel.  
* En bildfil som innehåller rysk text (för demonstrationen kallar vi den `russian_note.jpg`).  

Om något av detta låter obekant, inga problem. Stegen nedan inkluderar det exakta NuGet‑kommandot för att hämta Aspose OCR, och koden är helt självständig.

![exempel på hur man utför OCR](/images/ocr-demo.png "exempel på hur man utför OCR i C# example")

## Steg 1 – Installera Aspose OCR och lägg till namnrymder

Först och främst, du behöver biblioteket. Öppna en terminal i din projektmapp och kör:

```bash
dotnet add package Aspose.OCR
```

Det kommandot hämtar den senaste stabila versionen (i april 2026 är den 22.9). Efter att paketet har återställts, lägg till de nödvändiga `using`‑direktiven högst upp i din C#‑fil:

```csharp
using Aspose.OCR;
using Aspose.OCR.SpellCheck;
using System.Drawing;
```

*Proffstips:* Om du använder Visual Studio kommer IDE:n föreslå att lägga till dem automatiskt så snart du skriver det första klassnamnet.

## Steg 2 – Initiera OCR‑motorn för ryskt språk

Delarna **hur man utför OCR** börjar med att skapa en `OcrEngine`‑instans. Genom att ange `OcrLanguage.Russian` talar vi om för motorn att ladda den kyrilliska teckenuppsättningen och språk‑specifika heuristiker.

```csharp
// Step 2: Initialise OCR engine for Russian
OcrEngine ocrEngine = new OcrEngine
{
    Language = OcrLanguage.Russian   // Enables Russian language support
};
```

Varför är detta viktigt? Utan att ange språket använder motorn som standard engelska och kommer att misstolka många kyrilliska tecken, vilket leder till förvrängd output. Att explicit konfigurera språket förbättrar noggrannheten avsevärt.

## Steg 3 – Ladda bilden och **konvertera bild till text**

Nu laddar vi in bilden i minnet. Metoden `Image.FromFile` fungerar med de flesta vanliga format (JPG, PNG, BMP). Efter inläsning anropar vi `Recognize` för att **konvertera bild till text**.

```csharp
// Step 3: Load the image that contains Russian text
Image sourceImage = Image.FromFile(@"YOUR_DIRECTORY/russian_note.jpg");

// Step 4: Perform OCR – this is the core “how to perform OCR” call
string rawText = ocrEngine.Recognize(sourceImage);
```

`rawText`‑variabeln innehåller nu den råa OCR‑outputen, som fortfarande kan innehålla stavfel eller felaktigt igenkända tecken. Du kan skriva ut den för att se vad motorn fångade:

```csharp
Console.WriteLine("Raw OCR output:");
Console.WriteLine(rawText);
```

## Steg 4 – **Hur man stavningskontrollerar** OCR‑resultatet

Rysk OCR kan vara brusig, särskilt med lågupplösta skanningar. Aspose tillhandahåller en `SpellChecker`‑klass som förstår ryska ordböcker direkt. Så här anropar du den:

```csharp
// Step 5: Initialise the spell checker
SpellChecker spellChecker = new SpellChecker();

// Step 6: Correct spelling mistakes in the recognized text
string correctedText = spellChecker.CheckAndCorrect(rawText, OcrLanguage.Russian);
```

Metoden `CheckAndCorrect` returnerar en ny sträng där felstavade ord ersätts med de mest sannolika korrekta alternativen. Den respekterar också interpunktion, så du får inte en vägg av text.

*Edge case:* Om OCR‑outputen är tom (t.ex. bilden är helt vit) kommer `CheckAndCorrect` helt enkelt att returnera en tom sträng. Det är en bra idé att skydda mot detta om du planerar att skriva resultatet till en fil.

## Steg 5 – Visa det rensade resultatet

Till sist skriver vi ut den korrigerade strängen. I en verklig applikation kan du skriva den till en databas, ett JSON‑API eller ett Word‑dokument. För den här demonstrationen räcker en konsolutskrift:

```csharp
// Step 7: Show the corrected result
Console.WriteLine("\nCorrected text:");
Console.WriteLine(correctedText);
```

När du kör programmet bör du se något liknande:

```
Raw OCR output:
Привeт мир! Этo тeкcт c русcкoй оcнoвнoй.

Corrected text:
Привет мир! Это текст с русской основой.
```

Lägg märke till hur stavningskontrollen omvandlade “Привeт” (blandat latinskt ‘e’) till korrekt kyrillisk “Привет”. Det är magin med **hur man stavningskontrollerar** OCR‑output.

## Fullt fungerande exempel

Nedan är det kompletta, körbara programmet som binder ihop alla stegen. Kopiera‑klistra in det i ett nytt konsolprojekt och tryck **F5**.

```csharp
using Aspose.OCR;
using Aspose.OCR.SpellCheck;
using System.Drawing;

class SpellCheckDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine configured for Russian language
        OcrEngine ocrEngine = new OcrEngine { Language = OcrLanguage.Russian };

        // Step 2: Load the image that contains the text to be recognized
        Image sourceImage = Image.FromFile(@"YOUR_DIRECTORY/russian_note.jpg");

        // Step 3: Perform OCR to extract raw text from the image
        string rawText = ocrEngine.Recognize(sourceImage);

        // Optional: Show raw OCR output
        System.Console.WriteLine("Raw OCR output:");
        System.Console.WriteLine(rawText);

        // Step 4: Initialise the spell checker
        SpellChecker spellChecker = new SpellChecker();

        // Step 5: Correct spelling mistakes in the recognized text
        string correctedText = spellChecker.CheckAndCorrect(rawText, OcrLanguage.Russian);

        // Step 6: Display the corrected result
        System.Console.WriteLine("\nCorrected text:");
        System.Console.WriteLine(correctedText);
    }
}
```

### Förväntad output

Att köra programmet med ett tydligt, högupplöst foto av rysk handskrift ger vanligtvis en ren, mänskligt läsbar mening. Om bilden är suddig kan du fortfarande få delvis korrekta ord, men stavningskontrollen kommer att jämna ut de flesta uppenbara felen.

## Vanliga fallgropar & tips

| Problem | Varför det händer | Hur man åtgärdar / undviker |
|-------|----------------|--------------------|
| **Skräptecken** | Låg DPI eller bullrigt bakgrund | Förbehandla bilden (öka kontrast, ändra storlek till ≥300 dpi) innan du skickar den till `Recognize`. |
| **Tom output** | Fel filväg eller format som inte stöds | Verifiera sökvägen och använd `Image.FromFile` inom ett `try/catch`‑block för att visa fel. |
| **Stavningskontrollen missar fel** | Sällsynta ord som saknas i ordboken | Utöka ordboken genom att ladda en anpassad ordlista via `spellChecker.AddUserDictionary("mywords.txt")`. |
| **Prestandafördröjning vid stora batcher** | OCR är CPU‑intensivt | Kör OCR på en bakgrundstråd eller använd `Parallel.ForEach` för flera bilder. |
| **Licensundantag** | Användning av utvärderingsversion utanför provperioden | Köp en licens och anropa `License license = new License(); license.SetLicense("Aspose.Total.lic");` innan du skapar `OcrEngine`. |

## Nästa steg – Gå bortom enkel OCR

Nu när du har bemästrat **hur man utför OCR**, överväg dessa tillägg:

* **Batch processing** – Loopa igenom en mapp med bilder och skriv varje korrigerade text till en `.txt`‑fil.  
* **PDF conversion** – Använd Aspose PDF för att bädda in den extraherade texten tillbaka i en sökbar PDF.  
* **Language detection** – Om du behöver hantera flera språk, inspektera OCR‑resultatet först och byt `OcrLanguage` därefter.  
* **Integration with Azure Cognitive Services** – Jämför Asposes resultat med Microsofts OCR‑API för ett hybridt tillvägagångssätt.

Alla dessa ämnen involverar naturligt de sekundära nyckelorden **extrahera text från bild**, **konvertera bild till text**, och **hur man stavningskontrollerar**, så

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}