---
category: general
date: 2026-03-07
description: Aspose OCR‑exempel som visar hur man aktiverar stavningskontroll, lägger
  till en anpassad ordlista, laddar bild‑OCR och snabbt rättar OCR‑fel.
draft: false
keywords:
- aspose ocr example
- how to enable spellcheck
- how to add dictionary
- load image ocr
- how to fix ocr errors
language: sv
og_description: Aspose OCR‑exempel som guidar dig genom att aktivera stavningskontroll,
  lägga till en anpassad ordlista, ladda en bild för OCR och åtgärda vanliga OCR‑fel.
og_title: Aspose OCR-exempel – Aktivera stavningskontroll och rätta fel
tags:
- Aspose
- OCR
- C#
- SpellCheck
title: Aspose OCR-exempel – Aktivera stavningskontroll och rätta fel i C#
url: /sv/net/ocr-optimization/aspose-ocr-example-enable-spellcheck-and-fix-errors-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR-exempel – Aktivera stavningskontroll och rätta fel i C#

Har du någonsin behövt ett **Aspose OCR example** som inte bara läser text från en bild utan också rensar bort de irriterande stavningsfelen? Du är inte ensam. I många verkliga projekt är den råa OCR‑utdata full av stavfel, särskilt när källbilden innehåller lågkontrastteckensnitt eller handskrivna anteckningar.  

De goda nyheterna? Med Aspose.OCR kan du **enable spellcheck**, ansluta ditt eget lexikon och få en polerad sträng på bara några kodrader. Nedan ser du exakt **how to enable spellcheck**, **how to add a dictionary**, och **how to load image OCR** så att du äntligen kan **fix OCR errors** utan att rycka ur håret.

I den här handledningen täcker vi allt du behöver – från NuGet‑installation till ett komplett, körbart program som skriver ut korrigerad text. I slutet har du ett gediget **Aspose OCR example** som du kan klistra in direkt i vilket .NET‑projekt som helst.

## Förutsättningar

- .NET 6.0 SDK eller senare (koden fungerar även med .NET Core och .NET Framework)
- Visual Studio 2022 eller någon C#‑kompatibel IDE
- En bildfil (`typed_text.png`) som innehåller tydlig, maskinskriven engelsk text
- Internetåtkomst för att hämta Aspose.OCR NuGet‑paketet

Inga andra tredjepartsbibliotek krävs.

---

## Steg 1 – Installera Aspose.OCR NuGet‑paketet (Load Image OCR)

Innan vi kan skriva någon kod behöver vi biblioteket som driver OCR‑motorn.

```bash
dotnet add package Aspose.OCR
```

> **Pro tip:** Om du använder Visual Studio, högerklicka på projektet → *Manage NuGet Packages* → sök efter **Aspose.OCR** och klicka på *Install*.  

Att installera paketet ger dig tillgång till `OcrEngine`, `ImageStream` och de inbyggda stavningskontrollverktygen som vi kommer att använda senare. När paketet är på plats är du redo att **load image OCR**.

## Steg 2 – Skapa OCR‑motorinstansen

Att skapa motorn är det första konkreta steget i varje **Aspose OCR example**. Tänk på `OcrEngine` som hjärnan som analyserar bitmapen och spottar ut text.

```csharp
using Aspose.OCR;
using Aspose.OCR.SpellCheck;

// Step 2: Initialize the OCR engine
var ocrEngine = new OcrEngine();
```

`OcrEngine`‑konstruktorn kräver inga parametrar, vilket gör den enkel och prydlig för snabba prototyper.

## Steg 3 – Hur man aktiverar stavningskontroll (och varför det är viktigt)

Rå OCR‑utdata innehåller ofta felaktigt igenkända ord som “teh” istället för “the”. Att aktivera den inbyggda stavningskontrollen låter Aspose automatiskt ersätta dessa fel med den mest sannolika korrekta stavningen.

```csharp
// Step 3: Turn on spell checking and set the language to English
ocrEngine.Settings.SpellCheck.Enabled = true;
ocrEngine.Settings.SpellCheck.Language = SpellCheckLanguage.English;
```

> **Varför aktivera stavningskontroll?**  
> - **Noggrannhet:** En efterbearbetnings‑stavningskontroll kan öka den totala textnoggrannheten med 10‑15 % för tryckta dokument.  
> - **Användarupplevelse:** Ren text betyder mindre efterföljande rengöring när du matar resultatet i sökindex eller analys‑pipeline.

## Steg 4 – Hur man lägger till ett lexikon (anpassade ord)

Ibland känner inte standardlexikonet till dina varumärkesnamn, produktkoder eller domänspecifika facktermer. Det är då **how to add dictionary** blir relevant.

```csharp
// Step 4: Add custom words that the spell checker should accept
ocrEngine.Settings.SpellCheck.CustomDictionary.AddWords(new[]
{
    "AsposeOCR",   // our library name
    "OCRify",      // a fictional product
    "CSharpify"    // another custom term
});
```

Du kan mata in en array, en lista eller till och med läsa från en fil om du har ett stort anpassat ordförråd. Stavningskontrollen kommer nu att behandla dessa poster som giltiga, vilket förhindrar felaktiga korrigeringar.

## Steg 5 – Ladda bilden för OCR (Load Image OCR)

Nu när motorn är konfigurerad måste vi peka den på bilden vi vill läsa. Hjälpmetoden `ImageStream.FromFile` abstraherar bort fil‑läsningsdetaljerna.

```csharp
// Step 5: Load the image that contains the text to be recognized
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/typed_text.png");
```

> **Tips:** Om din bild finns i en undermapp i projektet, ställ in dess *Copy to Output Directory*-egenskap till *Copy always* så att sökvägen löses upp vid körning.

## Steg 6 – Utför igenkänning och rätta OCR‑fel

När allt är inställt kör ett enda anrop till `Recognize()` OCR‑pipeline, tillämpar stavningskontroll och lagrar det rensade resultatet i `ocrEngine.Text`.

```csharp
// Step 6: Run OCR and let the spell checker clean the output
ocrEngine.Recognize();

// Step 7: Output the corrected text to the console
Console.WriteLine("Corrected text:");
Console.WriteLine(ocrEngine.Text);
```

### Förväntad utdata

Om vi antar att `typed_text.png` innehåller meningen `The quick brown fox jumps over teh lazy dog`, kommer konsolen att visa:

```
Corrected text:
The quick brown fox jumps over the lazy dog
```

Observera hur “teh” automatiskt korrigerades till “the”. Om du hade lagt till “OCRify” i det anpassade lexikonet och bilden innehöll det ordet, skulle motorn låta det vara oförändrat.

---

## Fullt fungerande exempel (Klar att kopiera‑klistra in)

Nedan är det kompletta programmet som du kan klistra in i ett nytt konsolprojekt. Det innehåller alla stegen ovan, samt några kommentarer för tydlighet.

```csharp
// ---------------------------------------------------------------
// Aspose OCR Example – Enable Spellcheck and Fix Errors
// ---------------------------------------------------------------

using System;
using Aspose.OCR;
using Aspose.OCR.SpellCheck;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create the OCR engine
            var ocrEngine = new OcrEngine();

            // 2️⃣ Enable spell checking (how to enable spellcheck)
            ocrEngine.Settings.SpellCheck.Enabled = true;
            ocrEngine.Settings.SpellCheck.Language = SpellCheckLanguage.English;

            // 3️⃣ Add custom words (how to add dictionary)
            ocrEngine.Settings.SpellCheck.CustomDictionary.AddWords(new[]
            {
                "AsposeOCR",
                "OCRify",
                "CSharpify"
            });

            // 4️⃣ Load the image (load image OCR)
            // Replace the path with the actual location of your image file
            ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/typed_text.png");

            // 5️⃣ Run OCR – this also fixes common OCR errors (how to fix ocr errors)
            ocrEngine.Recognize();

            // 6️⃣ Show the corrected result
            Console.WriteLine("Corrected text:");
            Console.WriteLine(ocrEngine.Text);
        }
    }
}
```

Spara detta som `Program.cs`, kör `dotnet run`, så bör du se den korrigerade meningen skriven i konsolen.

---

## Vanliga frågor & specialfall

| Question | Answer |
|----------|--------|
| **Vad händer om bilden är en flersidig PDF?** | Aspose.OCR kan hantera PDF‑sidor som bilder. Använd `ocrEngine.Image = ImageStream.FromPdf("file.pdf", pageNumber: 1);` och loopa igenom sidorna. |
| **Kan jag byta språk till något annat än engelska?** | Absolut. Ställ in `ocrEngine.Settings.SpellCheck.Language = SpellCheckLanguage.French;` (eller vilket stödjande språk som helst). |
| **Mitt anpassade lexikon är enormt—kommer det att påverka prestandan?** | Att lägga till tusentals ord medför en liten initial kostnad, men uppslagning är O(1) tack vare en hash‑set under huven. För enorma ordförråd, överväg att ladda dem en gång vid applikationens start. |
| **Vad händer om OCR‑motorn kastar ett undantag på en korrupt bild?** | Omslut `Recognize()` i ett try‑catch‑block och inspektera `ocrEngine.LastError`. Du kan också förvalidera bildens dimensioner med `ocrEngine.Image.Width` och `Height`. |
| **Behöver jag en licens för produktionsanvändning?** | Den fria utvärderingen fungerar för testning, men en kommersiell licens tar bort vattenstämpeln för utvärdering och låser upp full prestanda. |

## Slutsats

Du har nu ett **complete Aspose OCR example** som demonstrerar **how to enable spellcheck**, **how to add a dictionary**, **load image OCR**, och **how to fix OCR errors** på ett rent, produktionsklart sätt. Genom att konfigurera stavningskontrollen och mata in en anpassad ordlista förbättrar du avsevärt kvaliteten på den extraherade texten utan att själv skriva någon efterbearbetningslogik.

Redo för nästa steg? Prova att byta språk till spanska, mata in en flersidig PDF, eller integrera resultatet i ett sökbart Azure Cognitive Search‑index. Samma mönster gäller – justera bara språkflaggan och eventuellt expandera det anpassade lexikonet.

Om du fann den här guiden hjälpsam, ge den en stjärna på GitHub, dela den med kollegor, eller lämna en kommentar nedan. Lycka till med kodandet, och må dina OCR‑resultat alltid vara felfria!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}