---
category: general
date: 2026-06-03
description: Utför OCR på bild och extrahera text från bilden med Aspose.OCR. Lär
  dig hur du upptäcker felstavade ord och får stavningsförslag i en enda C#‑demo.
draft: false
keywords:
- perform OCR on image
- extract text from image
- detect misspelled words
- get spelling suggestions
- how to extract text
language: sv
og_description: Utför OCR på en bild för att extrahera text från bilden, upptäck sedan
  felstavade ord och få stavningsförslag med Aspose.OCR i C#.
og_title: Utför OCR på bild och upptäck felstavade ord i C#
schemas:
- author: Aspose
  dateModified: '2026-06-03'
  description: Perform OCR on image and extract text from image using Aspose.OCR.
    Learn how to detect misspelled words and get spelling suggestions in a single
    C# demo.
  headline: Perform OCR on Image and Detect Misspelled Words in C#
  type: TechArticle
tags:
- Aspose OCR
- C#
- Spell Checking
title: Utför OCR på bild och upptäck felstavade ord i C#
url: /sv/net/text-recognition/perform-ocr-on-image-and-detect-misspelled-words-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Utför OCR på bild och upptäck felstavade ord i C#

Har du någonsin funderat på hur man **perform OCR on image**‑filer utan att dra i håret? Du är inte ensam. Oavsett om du digitaliserar gamla brev, skannar kvitton eller bygger ett smart dokumentflöde, är det första hindret att extrahera ren text från bilder. Den goda nyheten? Med Aspose.OCR kan du sätta ihop en lösning på några minuter, och bonusen är att du också kan **detect misspelled words** och **get spelling suggestions** i samma körning.

I den här handledningen går vi igenom en komplett, färdig‑körbar C#‑konsolapp som **extracts text from image**, kör en engelsk stavningskontroll och skriver ut varje fel med praktiska korrigeringsförslag. När du är klar vet du exakt **how to extract text**, hur du ansluter stavnings‑API:t och hur den förväntade konsolutmatningen ser ut.

## Vad du kommer att bygga

- Ladda en bitmap (eller PNG) som innehåller typografiska fel.  
- Kör Aspose.OCR för att **perform OCR on image** och få råa strängdata.  
- Initiera den inbyggda engelska stavningskontrollen.  
- **Detect misspelled words** och **get spelling suggestions** för varje ord.  
- Skriv en snygg rapport till konsolen.

Inga externa tjänster, inga krångliga HTTP‑anrop—bara ett enda NuGet‑paket och ett fåtal kodrader.

## Förutsättningar

- .NET 6.0 SDK eller senare (koden fungerar också på .NET Framework 4.7+).  
- Visual Studio 2022 (eller någon annan editor du föredrar).  
- Aspose.OCR för .NET NuGet‑paket (`Aspose.OCR`).  
- En bildfil (`letter_with_typos.png`) placerad någonstans där du kan referera till den från projektet.

Om du aldrig har använt Aspose tidigare, oroa dig inte—installationen av paketet är lika enkelt som att köra:

```bash
dotnet add package Aspose.OCR
```

Nu dyker vi ner i implementationen.

## Steg 1: Skapa projektet och installera Aspose.OCR

Skapa ett nytt konsolprojekt och hämta OCR‑biblioteket:

```bash
dotnet new console -n OcrSpellDemo
cd OcrSpellDemo
dotnet add package Aspose.OCR
```

När återställningen är klar, öppna `Program.cs`. Vi kommer att ersätta standardinnehållet med hela demokoden senare, men först förklarar vi varför varje namnrymd är viktig.

- `Aspose.OCR` – Kärnmotorn för OCR och bildhantering.  
- `Aspose.OCR.SpellCheck` – Stavningskontrollverktyg som följer med biblioteket.  
- `System` – Standard‑.NET‑basklasser (t.ex. `Console`).

## Steg 2: Ladda bilden och utför OCR på bild

Det första riktiga arbetet är att mata in bilden i OCR‑motorn. Aspose.OCR läser många format (PNG, JPEG, TIFF). Här är kodsnutten som gör det tunga lyftet:

```csharp
// Step 2: Load the image that contains the text to be recognized
var image = OcrImage.FromFile(@"YOUR_DIRECTORY/letter_with_typos.png");

// Step 3: Perform OCR to extract the raw text from the image
var ocrEngine = new OcrEngine();
var ocrResult = ocrEngine.Recognize(image);
```

> **Varför detta är viktigt:** `OcrImage.FromFile` abstraherar bort pixel‑nivådetaljer, medan `OcrEngine.Recognize` kör den tränade neurala modellen som översätter visuella glyfer till Unicode‑tecken. `ocrResult.Text`‑egenskapen innehåller nu den råa strängen—precis vad du behöver för att **extract text from image**.

> **Proffstips:** Om din bild innehåller flera språk kan du sätta `ocrEngine.Language = OcrLanguage.Multilingual;` innan du anropar `Recognize`.

## Steg 3: Initiera den engelska stavningskontrollen

Aspose.OCR levereras med en inbyggd stavningskontroll som förstår engelska direkt ur lådan. Initieringen är en enradare:

```csharp
// Step 4: Initialise the English spell‑checker
var spellChecker = new SpellChecker(OcrLanguage.English);
```

> **Varför detta steg är avgörande:** OCR‑utdata kan innehålla felaktigt igenkända tecken (t.ex. “l” vs “1”) eller faktiska skrivfel från källdokumentet. Stavningskontrollen skannar strängen, lokaliserar misstänkta token och föreslår alternativ.

## Steg 4: Upptäck felstavade ord och hämta stavningsförslag

Nu matar vi OCR‑texten till kontrollen:

```csharp
// Step 5: Check the recognized text for misspelled words and obtain suggestions
var misspellings = spellChecker.Check(ocrResult.Text);
```

`misspellings` är en samling där varje post innehåller det felaktiga ordet och en array med möjliga korrigeringar.

## Steg 5: Skriv ut resultaten

Till sist itererar vi över samlingen och skriver en mänskligt läsbar rapport:

```csharp
// Step 6: Output each misspelled word together with its suggested corrections
foreach (var entry in misspellings)
{
    Console.WriteLine($"Misspelled: {entry.Word}");
    Console.WriteLine("  Suggestions: " + string.Join(", ", entry.Suggestions));
}
```

### Förväntad konsolutmatning

Om `letter_with_typos.png` innehåller meningen:

```
Ths is an exampel of a lettter with som misspelled wrds.
```

Kommer demon att producera något i stil med:

```
Misspelled: Ths
  Suggestions: This, Thus, The
Misspelled: exampel
  Suggestions: example, exemplar, exampell
Misspelled: lettter
  Suggestions: letter, litter, lett
Misspelled: som
  Suggestions: some, sum, son
Misspelled: wrds
  Suggestions: words, wards, wryds
```

Lägg märke till hur varje felstavning paras ihop med ett antal rimliga korrigeringar—precis vad du behöver när du bygger ett användarvänligt korrigerings‑UI.

## Fullt fungerande exempel

Nedan är det **kompletta, kopiera‑och‑klistra‑klara** programmet. Ersätt `YOUR_DIRECTORY` med den faktiska sökvägen till din bildfil.

```csharp
using Aspose.OCR;
using Aspose.OCR.SpellCheck;
using System;

class SpellCheckDemo
{
    static void Main()
    {
        // Step 1: Load the image that contains the text to be recognized
        var image = OcrImage.FromFile(@"YOUR_DIRECTORY/letter_with_typos.png");

        // Step 2: Perform OCR to extract the raw text from the image
        var ocrEngine = new OcrEngine();
        var ocrResult = ocrEngine.Recognize(image);

        // Step 3: Initialise the English spell‑checker
        var spellChecker = new SpellChecker(OcrLanguage.English);

        // Step 4: Check the recognized text for misspelled words and obtain suggestions
        var misspellings = spellChecker.Check(ocrResult.Text);

        // Step 5: Output each misspelled word together with its suggested corrections
        foreach (var entry in misspellings)
        {
            Console.WriteLine($"Misspelled: {entry.Word}");
            Console.WriteLine("  Suggestions: " + string.Join(", ", entry.Suggestions));
        }

        // Optional: Keep console window open when debugging
        Console.WriteLine("\nPress any key to exit...");
        Console.ReadKey();
    }
}
```

> **Edge Cases att beakta**  
> - **Tom bild:** Om OCR‑motorn returnerar en tom sträng kommer `spellChecker.Check` helt enkelt att returnera en tom samling—ingen krasch.  
> - **Icke‑engelsk text:** Byt `OcrLanguage.English` mot `OcrLanguage.French` (eller något annat stödjert språk) för att **detect misspelled words** på andra språk.  
> - **Stora dokument:** För flersidiga PDF‑filer skulle du loopa över varje sida, utföra OCR och sedan samla resultaten innan stavningskontrollen.

## Visuell översikt (Bild‑alt‑text)

![Diagram showing the flow to perform OCR on image, extract text from image, and then detect misspelled words with spelling suggestions](perform-ocr-on-image-flow.png)

*Diagrammet ovan illustrerar den end‑to‑end‑pipeline som går från bild → OCR‑motor → råtext → stavningskontroll → förslag.*

## Vanliga frågor & Proffstips

| Fråga | Svar |
|----------|--------|
| **Behöver jag internetuppkoppling?** | Nej. Aspose.OCR körs helt lokalt; perfekt för offline‑ eller säkra miljöer. |
| **Hur exakt är stavningskontrollen?** | Den använder en ordlista med ~150 000 engelska ord och fuzzy‑matching, så de flesta vanliga skrivfel fångas. |
| **Kan jag anpassa ordlistan?** | Ja. `SpellChecker.AddUserDictionary("custom.txt")` låter dig ladda domänspecifika termer (t.ex. produktnamn). |
| **Vad händer om bilden är sned?** | OCR‑motorn upptäcker automatiskt orientering, men du kan manuellt anropa `ocrEngine.ImagePreprocessing.Rotate(angle)` för envisa fall. |
| **Finns det ett sätt att markera förslag i UI?** | När du har `misspellings`‑samlingen kan du mappa varje `entry.Word` tillbaka till dess position i `ocrResult.Text` och understryka det i en RichTextBox eller webbvy. |

## Slutsats

Vi har just visat dig **how to perform OCR on image**, **extract text from image**, och sedan **detect misspelled words** samt **get spelling suggestions**—allt med en koncis C#‑konsolapp. Kärnidén är enkel: låt Aspose.OCR göra det tunga arbetet med att känna igen tecken, och låt den inbyggda stavningskontrollen rensa upp resultatet. Därefter kan du bygga vidare till en fullständig dokumentbehandlingstjänst, integrera med ett webb‑API eller koppla in i en skrivbordsredigerare.

Redo för nästa steg? Prova att byta språk till spanska, mata in en flersidig PDF eller bygga ett litet WPF‑gränssnitt som låter användare klicka på ett ord för att acceptera ett förslag. Byggstenarna finns redan på plats—fortsätt bara experimentera.

Om du stöter på problem eller har idéer för utökningar, lämna en kommentar nedan. Lycka till med kodandet!


## Vad bör du lära dig härnäst?


Följande handledningar täcker närliggande ämnen som bygger vidare på teknikerna i den här guiden. Varje resurs innehåller kompletta kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra fler API‑funktioner och utforska alternativa implementeringssätt i dina egna projekt.

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Extract Text from Image Using Aspose.OCR .NET](/ocr/english/net/image-and-drawing-recognition/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}