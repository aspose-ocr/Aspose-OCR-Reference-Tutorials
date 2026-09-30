---
category: general
date: 2026-01-15
description: Lär dig hur du OCR:ar arabisk text och känner igen hindi‑text med Aspose
  OCR. Denna steg‑för‑steg‑guide visar dig hur du extraherar text från en bild och
  konverterar bild till text på ett effektivt sätt.
draft: false
keywords:
- how to ocr arabic
- recognize arabic text
- extract text from image
- convert image to text
- recognize hindi text
language: sv
og_description: hur man OCR:ar arabisk text och känner igen hindi‑text i ett enda
  C#‑program. Följ den här kompletta guiden för att extrahera text från en bild och
  konvertera bilden till text.
og_title: hur man OCR:ar arabiska och hindi-texter med Aspose OCR
tags:
- Aspose OCR
- C#
- Multilingual OCR
title: hur man OCR:ar arabisk och hindi‑text med Aspose OCR
url: /sv/net/text-recognition/how-to-ocr-arabic-and-hindi-text-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# hur man ocr arabisk och hindi text med Aspose OCR

Har du någonsin undrat **how to ocr arabic** tecken som flödar från höger till vänster, samtidigt som du hämtar hindi‑glyfer från ett kvitto? Du är inte ensam. Många utvecklare stöter på samma problem när de behöver **recognize arabic text** och **recognize hindi text** i samma arbetsflöde.  

I den här handledningen går vi igenom ett komplett, körbart C#‑exempel som visar dig hur du **extract text from image** filer, **convert image to text**, och hanterar både arabiska och hindi‑skript med Aspose OCR. Inga vaga referenser—bara koden du kan kopiera‑klistra in, plus resonemanget bakom varje rad.

> **Pro tip:** Om du aldrig har använt Aspose OCR tidigare, installera NuGet‑paketet `Aspose.OCR` först. Det är en ett‑klick‑operation i Visual Studio, och det hämtar alla de inhemska binärerna du behöver för CPU‑baserad igenkänning.

---

![hur man ocr arabisk exempel](/images/arabic-ocr-sample.png "hur man ocr arabisk – exempel på arabisk skylt")

*Bildtext:* **hur man ocr arabisk – exempel på arabisk skylt**  

---

## hur man ocr arabisk – Inställning av miljön

Innan vi dyker ner i koden, låt oss försäkra oss om att utvecklingsmiljön är klar.

1. **Target framework** – .NET 6.0 eller senare. Äldre versioner kompilerar fortfarande, men du går miste om de senaste språkfunktionerna.  
2. **Package** – Kör `dotnet add package Aspose.OCR` i terminalen, eller använd NuGet Package Manager‑gränssnittet.  
3. **Images** – Placera två exempelbilder i en mapp du kan referera till, t.ex. `C:\OCRSamples\arabic_sign.jpg` och `C:\OCRSamples\hindi_receipt.png`. Den arabiska bilden bör innehålla tydliga, högkontrastarabiska tecken; den hindi‑bilden kan vara ett skannat kvitto eller ett fotografi av en skylt.  

Det är allt—inga extra konfigurationsfiler, inga GPU‑drivrutiner, bara en enkel CPU‑baserad OCR‑motor.

## Känn igen arabisk text – Laddning och bearbetning

Nu ska vi faktiskt **recognize arabic text**. Nyckeln är att tala om för motorn vilket språk som förväntas; annars använder motorn latin tecken och du får förvrängd output.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

class MultiLangDemo
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine (CPU‑based by default)
        var ocrEngine = new OcrEngine();

        // 2️⃣ Load an image that contains Arabic script
        var arabicImage = OcrImage.FromFile(@"C:\OCRSamples\arabic_sign.jpg");

        // 3️⃣ Recognize the Arabic text – note the Language.Arabic enum
        var arabicResult = ocrEngine.Recognize(arabicImage, Language.Arabic);

        // 4️⃣ Print the result to the console
        System.Console.WriteLine("Arabic: " + arabicResult.Text);
```

**Varför detta fungerar:**  
* `OcrEngine` hanterar all tungt arbete—förbehandling, segmentering och teckenklassificering.  
* Genom att skicka `Language.Arabic` aktiverar vi layoutmotorn för höger‑till‑vänster och den arabiska teckenuppsättningen. Utan detta skulle motorn behandla bilden som vänster‑till‑höger latin text, vilket leder till saknade diakritiska tecken och trasiga ord.  

**Förväntad output** (din faktiska text kommer att skilja sig beroende på bilden):

```
Arabic: مرحبا بكم في متجرنا
```

Om du ser tomma strängar, dubbelkolla att bilden inte är för mörk och att filvägen är korrekt.  

## extrahera text från bild – Hantera höger‑till‑vänster‑skript

Arabisk är inte det enda skriptet som kräver speciell hantering. Höger‑till‑vänster (RTL) språk kräver att OCR‑motorn vänder den visuella ordningen efter igenkänning. Aspose gör detta automatiskt när du specificerar `Language.Arabic`, men det är värt att notera för framtida utökningar (t.ex. hebreiska).

*Tips:* När du senare visar OCR‑resultatet i ett UI, se till att kontrollen stödjer RTL‑rendering; annars kommer texten att visas förvrängd.

## konvertera bild till text – Arbeta med hindi

Vi byter spår, låt oss **convert image to text** för ett hindi‑kvitto. Processen speglar den arabiska flödet, men vi använder `Language.Hindi` istället.

```csharp
        // 5️⃣ Load the Hindi (Devanagari) image
        var hindiImage = OcrImage.FromFile(@"C:\OCRSamples\hindi_receipt.png");

        // 6️⃣ Recognize Hindi text – Language.Hindi tells the engine to use Devanagari models
        var hindiResult = ocrEngine.Recognize(hindiImage, Language.Hindi);

        // 7️⃣ Output the Hindi OCR result
        System.Console.WriteLine("Hindi: " + hindiResult.Text);
    }
}
```

**Varför vi återanvänder samma `ocrEngine`‑instans:**  
Att skapa en ny motor för varje språk skulle slösa minne och initieringstid. Asposes motor är trådsäker för sekventiella anrop, så återanvändning är både effektiv och ren.

**Exempel på konsolutdata** (återigen, beror på din bild):

```
Hindi: कुल राशि: ₹ 1,250.00
```

Om hindi‑texten ser ut som förvrängda latin‑tecken, har du förmodligen utelämnat språk‑enum eller så är bildens upplösning för låg (<300 dpi). Att skala upp bilden eller applicera ett enkelt binarisering‑filter kan dramatiskt förbättra noggrannheten.

## känna igen hindi text – Vanliga fallgropar och kantfall

Även med rätt språkflagga kan några små problem få dig att snubbla:

| Problem | Symtom | Lösning |
|-------|---------|-----|
| Låg kontrast | Många tecken blir “?” eller utelämnas | Förbehandla med `OcrImage.AdjustContrast(1.5)` |
| Sned bild | Texten visas roterad, OCR returnerar tom sträng | Anropa `ocrEngine.PreprocessImage(arabicImage, ImageProcessingOptions.Rotate)` |
| Blandade språk | Arabisk rad följd av engelska siffror | Kör två pass: först med `Language.Arabic`, sedan med `Language.English` på samma bild och sammanfoga resultaten |
| Stor filstorlek | Långsam igenkänning eller minnesbristfel | Nedskala till max 2000 px bredd med `OcrImage.Resize(2000, 0)` |

Dessa tips hjälper dig att **extract text from image** filer som inte är perfekt skannade, vilket är vanligt i verkliga projekt.

## Sätt ihop allt – Fullt fungerande exempel

Nedan är det kompletta programmet som du kan kopiera direkt in i ett nytt konsolprojekt. Inga dolda beroenden, ingen extra konfiguration—bara ren C#.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

class MultiLangDemo
{
    static void Main()
    {
        // Initialize the OCR engine (CPU‑based)
        var ocrEngine = new OcrEngine();

        // -------------------- Arabic --------------------
        var arabicPath = @"C:\OCRSamples\arabic_sign.jpg";
        var arabicImage = OcrImage.FromFile(arabicPath);
        var arabicResult = ocrEngine.Recognize(arabicImage, Language.Arabic);
        System.Console.WriteLine("Arabic: " + arabicResult.Text);

        // -------------------- Hindi --------------------
        var hindiPath = @"C:\OCRSamples\hindi_receipt.png";
        var hindiImage = OcrImage.FromFile(hindiPath);
        var hindiResult = ocrEngine.Recognize(hindiImage, Language.Hindi);
        System.Console.WriteLine("Hindi: " + hindiResult.Text);
    }
}
```

**Kör programmet** kommer att skriva ut både arabiska och hindi‑strängar till konsolen, vilket bekräftar att du framgångsrikt har **recognize arabic text** och **recognize hindi text** i ett enda körning.  

## Slutsats

Du har nu ett robust, end‑to‑end‑svar på frågan **how to ocr arabic** samtidigt som du hanterar Hindi. Genom att skapa en enda `OcrEngine`, ladda varje bild och skicka rätt `Language`‑enum, kan du **extract text from image**, **convert image to text**, och **recognize arabic text** samt **recognize hindi text** utan några extra bibliotek.

Från här kan du utforska:

* **Batch processing** – loopa över en mapp med bilder och lagra resultat i en databas.  
* **Post‑processing** – använd reguljära uttryck för att rensa upp valutasymboler i hindi‑kvitton.  
* **Hybrid language detection** – mata in den råa bitmapen till en språk‑identifieringsmodell innan du väljer enum.  

Prova det, justera förbehandlingsstegen, så kommer du snabbt se OCR‑noggrannheten öka. Om du stöter på några konstigheter, släng

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}