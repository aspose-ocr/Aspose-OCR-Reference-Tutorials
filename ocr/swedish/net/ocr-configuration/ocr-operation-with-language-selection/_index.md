---
date: 2026-07-23
description: Lär dig hur ocr-biblioteket för .net extraherar bildtext C# med Aspose.OCR.
  Denna guide täcker flerspråkig OCR, språkval och praktiska tips.
keywords:
- ocr library for .net
- extract image text c#
- Aspose.OCR
- multilingual OCR
lastmod: 2026-07-23
linktitle: Extrahera bildtext C# med språkval med Aspose.OCR
og_description: ocr-biblioteket för .net möjliggör att extrahera bildtext C# med Aspose.OCR.
  Få flerspråkig OCR, språkval och steg‑för‑steg kodexempel.
og_image_alt: 'Guide: Extract image text C# using Aspose.OCR OCR library for .NET'
og_title: ocr-bibliotek för .net – Extrahera bildtext C#
schemas:
- author: Aspose
  dateModified: '2026-07-23'
  description: Learn how the ocr library for .net extracts image text C# using Aspose.OCR.
    This guide covers multilingual OCR, language selection, and practical tips.
  headline: ocr library for .net – Extract image text C#
  type: TechArticle
- questions:
  - answer: Yes, Aspose.OCR supports over 30 languages, providing flexibility for
      multilingual OCR tasks.
    question: Is Aspose.OCR suitable for multilingual text recognition?
  - answer: Absolutely! Adjust parameters like `AutoSkew`, `SkewAngle`, and `LineDetectionMode`
      to optimise results for different scenarios.
    question: Can I fine‑tune OCR settings for specific image characteristics?
  - answer: Visit the [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16) for support
      and discussions with the community.
    question: Where can I find additional support or community discussions?
  - answer: Yes, explore the [free trial](https://releases.aspose.com/) to experience
      the capabilities of Aspose.OCR.
    question: Is there a free trial available?
  - answer: To purchase, visit the [purchase page](https://purchase.aspose.com/buy).
    question: How can I purchase Aspose.OCR for .NET?
  type: FAQPage
second_title: Aspose.OCR .NET API
tags:
- ocr library
- Aspose.OCR
- C# OCR
- image text extraction
title: ocr-bibliotek för .net – Extrahera bildtext C#
url: /sv/net/ocr-configuration/ocr-operation-with-language-selection/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahera bildtext C# med språkval med Aspose.OCR

## Introduktion

Om du behöver **extrahera bildtext C#** från bilder eller PDF‑filer i en .NET‑applikation, är Aspose.OCR ett kraftfullt **ocr library for .net** som levererar snabb, exakt och språkmedveten igenkänning. I den här handledningen går vi igenom ett verkligt exempel som demonstrerar OCR‑bildigenkänning med språkval, så att du kan hämta flerspråkig text från bilder med bara några rader kod. När du är klar ser du varför detta tillvägagångssätt är ett stabilt val för produktionsarbetsbelastningar och hur enkelt det är att integrera OCR i dina C#‑projekt.

## Snabba svar
- **Vad gör Aspose.OCR?** Det känner igen tryckt och handskriven text i bilder och returnerar den extraherade texten.  
- **Kan jag välja språk?** Ja – du kan ange vilket som helst av de stödjade språken, t.ex. engelska, tyska, spanska, kinesiska osv.  
- **Behöver jag en licens för utveckling?** En gratis provversion fungerar för utvärdering; en licens krävs för produktionsanvändning.  
- **Vilka .NET‑versioner stöds?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6+.  
- **Är skevkorrektion automatisk?** Du kan aktivera `AutoSkew` och finjustera inställningen `SkewAngle`.  

`AutoSkew` upptäcker och korrigerar automatiskt bildskevhet. `SkewAngle` möjliggör manuell justering av rotationsvinkeln.

## Vad är “extrahera bildtext C#”?

Att extrahera bildtext i C# innebär att använda ett bibliotek för att läsa det visuella innehållet i en bild (PNG, JPEG, TIFF osv.) och konvertera det till sökbar, redigerbar text. **ocr library for .net** Aspose.OCR utför denna konvertering lokalt, håller data på plats och undviker externa tjänstekall.

## Varför välja Aspose.OCR för OCR‑uppgifter?

Aspose.OCR levererar **95 %+ noggrannhet** på vanliga tryckta teckensnitt och kan bearbeta **upp till 300 sidor per minut** på en typisk 2,5 GHz‑server, vilket gör det till en av de snabbaste **ocr library for .net**‑lösningarna. Det innehåller också inbyggda språkpaket, så du aldrig behöver tredjepartsresurser, och det körs helt offline för maximal säkerhet.

## Förutsättningar

Innan vi dyker ner i koden, se till att du har följande förutsättningar på plats:

- Aspose.OCR för .NET: Säkerställ att du har Aspose.OCR‑biblioteket installerat. Du kan ladda ner det från [Aspose.OCR for .NET download page](https://releases.aspose.com/ocr/net/).

- Utvecklingsmiljö: Ställ in en fungerande miljö med en .NET‑applikation. Om du ännu inte har gjort detta, se [documentation](https://reference.aspose.com/ocr/net/) för detaljerade instruktioner.

## Importera namnrymder

I din .NET‑applikation, börja med att importera de nödvändiga namnrymderna:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Steg 1: Initiera Aspose.OCR

`OcrEngine` är Aspose.OCR:s kärnklass som utför optisk teckenigenkänning på bilder. Börja med att skapa en instans av denna klass; detta lägger grunden för alla efterföljande OCR‑operationer.

```csharp
// ExStart:1
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Steg 2: Ange bildsökväg

Definiera den absoluta eller relativa sökvägen till bilden du vill bearbeta. Sökvägen måste peka på en läsbar fil; annars kommer motorn att kasta ett undantag.

```csharp
// Image Path
string fullPath = dataDir + "sample.png";
```

## Steg 3: Känn igen bild med språkval

`RecognizeImage` är metoden som skannar den angivna bitmapen, tillämpar språkmodeller och returnerar ett `RecognitionResult`‑objekt som innehåller den extraherade texten. Genom att sätta egenskapen `Language` talar du om för motorn vilka språkliga regler som ska tillämpas, vilket dramatiskt förbättrar noggrannheten för icke‑engelsk text.

Egenskapen `Language` väljer OCR‑språkmodellen som ska användas.

```csharp
// Recognize image           
RecognitionResult result = api.RecognizeImage(fullPath, new RecognitionSettings
{
    DetectAreas = true,
    RecognizeSingleLine = false,
    AutoSkew = true,
    SkewAngle = 0.2F,
    Language = Language.Eng, // Choose the language: none, eng, deu, por, spa, fra, ita, cze, dan, dum, est, fin, lav, lit, nor, pol, rum, srp_hrv, slk, slv, swe, chi
});
```

## Steg 4: Skriv ut och visa resultat

Efter OCR‑operationen kan du komma åt den igenkända texten, avgränsningsrutorna för varje ord, eventuella varningar och till och med en JSON‑dump för vidare bearbetning.

```csharp
// Print result
Console.WriteLine($"Text:\n {result.RecognitionText}");
Console.WriteLine("Areas:");
result.RecognitionAreasText.ForEach(a => Console.WriteLine($"{a}"));
Console.WriteLine("Warnings:");
result.Warnings.ForEach(w => Console.WriteLine($"{w}"));
Console.WriteLine($"JSON: {result.GetJson()}");
// ExEnd:1
```

## Hur extraherar man bildtext C# med språkval?

Läs in din bild med `new OcrEngine()` och sätt `engine.Language = Language.English` (eller vilket stödjat språk som helst) innan du anropar `engine.RecognizeImage(imagePath)`. Metoden returnerar hela texten i en enda sträng, som du sedan kan skriva ut, lagra eller skicka till andra tjänster. Detta tvåstegs‑mönster fungerar för alla stödjade språk och kräver inga externa beroenden.

## Vanliga problem och tips

- **Fel språkval** – Om resultatet ser förvrängt ut, dubbelkolla att `Language`‑egenskapen matchar språket i källbilden.  
- **Skevade bilder** – Aktivera `AutoSkew` eller justera manuellt `SkewAngle` för bättre noggrannhet på lutande skanningar.  
- **Stora filer** – Bearbeta stora bilder i delar eller minska upplösningen innan du skickar dem till `RecognizeImage` för att spara minne.  

## Vanliga frågor

**Q: Är Aspose.OCR lämplig för flerspråkig textigenkänning?**  
A: Ja, Aspose.OCR stödjer över 30 språk och ger flexibilitet för flerspråkiga OCR‑uppgifter.

**Q: Kan jag finjustera OCR‑inställningar för specifika bildegenskaper?**  
A: Absolut! Justera parametrar som `AutoSkew`, `SkewAngle` och `LineDetectionMode` för att optimera resultat för olika scenarier.

**Q: Var kan jag hitta ytterligare support eller community‑diskussioner?**  
A: Besök [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16) för support och diskussioner med communityn.

**Q: Finns det en gratis provversion?**  
A: Ja, utforska [free trial](https://releases.aspose.com/) för att uppleva Aspose.OCR:s funktioner.

**Q: Hur kan jag köpa Aspose.OCR för .NET?**  
A: För att köpa, gå till [purchase page](https://purchase.aspose.com/buy).

## Slutsats

Grattis! Du har lärt dig **hur man extraherar bildtext C#** med språkval med hjälp av Aspose.OCR för .NET. Denna handledning visade hur du konfigurerar OCR‑motorn, väljer rätt språk och hanterar resultaten, vilket ger dig en solid grund för att bygga flerspråkiga text‑extraktionsfunktioner i dina applikationer.

---

**Senast uppdaterad:** 2026-07-23  
**Testad med:** Aspose.OCR 24.11 för .NET  
**Författare:** Aspose  

{{< blocks/products/products-backtop-button >}}

## Relaterade handledningar

- [recognize text image with Aspose OCR for multiple languages](/ocr/net/ocr-settings/working-with-different-languages/)
- [Extract Text from Images – OCR Settings with Aspose.OCR](/ocr/net/ocr-settings/)
- [How to Extract Text from Image Using Aspose.OCR for .NET](/ocr/net/text-recognition/get-recognition-result/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}