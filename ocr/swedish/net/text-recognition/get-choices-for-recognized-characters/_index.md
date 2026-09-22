---
date: 2026-08-12
description: Lär dig hur du utför OCR‑efterbehandling med Aspose.OCR for .NET, hämtar
  teckenalternativ och förbättrar OCR‑noggrannheten med hjälp av listan över igenkända
  tecken.
keywords:
- ocr post processing
- improve ocr accuracy
- aspose ocr .net
lastmod: 2026-08-12
linktitle: Hämta alternativ för igenkända tecken i OCR‑bildigenkänning
og_description: Lär dig OCR‑efterbehandling med Aspose.OCR for .NET för att hämta
  teckenalternativ och förbättra OCR‑noggrannheten. Snabb guide för utvecklare.
og_image_alt: Aspose OCR tutorial showing character choices retrieval in a .NET application
og_title: OCR efterbehandling – hämta teckenalternativ i .NET
schemas:
- author: Aspose
  dateModified: '2026-08-12'
  description: Learn how to perform OCR post processing with Aspose.OCR for .NET,
    retrieve character alternatives, and improve OCR accuracy using the recognition
    characters list.
  headline: OCR post processing – get character choices
  type: TechArticle
- questions:
  - answer: By examining the alternative characters returned in the recognition characters
      list, you can apply context‑aware rules (e.g., dictionary checks) to select
      the most likely glyph, reducing mis‑recognitions.
    question: How does OCR post processing improve OCR accuracy?
  - answer: Yes, iterate over each `char[]` and use the first three elements, which
      represent the highest‑confidence alternatives.
    question: Can I filter the recognition characters list to only the top three choices?
  - answer: The list is populated for all supported languages; however, the richness
      of alternatives may vary depending on the language model configured in `RecognitionSettings`.
    question: Is the `RecognitionCharactersList` available for all languages?
  - answer: The code works with .NET Framework 4.6+, .NET Core 3.1, .NET 5, and .NET
      6+.
    question: What .NET versions are compatible with this tutorial?
  - answer: The official Aspose documentation and the GitHub repository contain additional
      examples and the full **Aspose OCR tutorial** collection.
    question: Where can I find more Aspose OCR samples?
  type: FAQPage
second_title: Aspose.OCR .NET API
tags:
- ocr post processing
- aspose ocr
- .net ocr
- character choices
title: OCR efterbehandling – hämta teckenalternativ
url: /sv/net/text-recognition/get-choices-for-recognized-characters/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR‑efterbehandling – hämta teckenalternativ

## Introduktion

Utnyttja kraften i **OCR‑efterbehandling** i moderna .NET‑applikationer och lär dig **hur du får OCR‑teckenalternativ** för varje igenkänt tecken. Aspose.OCR för .NET gör detta enkelt och ger dig inte bara den bästa gissade texten utan även alternativa tecken som motorn övervägde. I slutet av den här handledningen kommer du att kunna integrera den här funktionen i vilket C#‑projekt som helst och förbättra hanteringen av tvetydiga glyfer, vilket i slutändan **förbättrar OCR‑noggrannheten**.

## Snabba svar
- **Vad betyder “get OCR character choices”?** Det returnerar en lista med alternativa tecken för varje igenkänt glyf.  
- **Varför använda teckenalternativ?** För att hantera osäkra igenkänningar, utföra efterbehandling eller implementera anpassad validering.  
- **Vad behöver jag i förväg?** .NET‑utvecklingsmiljö, Visual Studio och Aspose.OCR för .NET‑biblioteket.  
- **Krävs en licens?** En gratis provversion fungerar för testning; en kommersiell licens behövs för produktion. Köp en licens [här](https://purchase.aspose.com/buy).  
- **Kan jag köra detta på .NET Core / .NET 6?** Ja, Aspose.OCR stöder alla moderna .NET‑runtime.  
- **Hur hjälper OCR‑efterbehandling?** Den låter dig välja mellan alternativ, vilket minskar fel och **förbättrar OCR‑noggrannheten**.

## Vad är OCR‑efterbehandling?
OCR‑efterbehandling avser den uppsättning tekniker som tillämpas efter den initiala textutvinningen för att förfina resultat, korrigera fel och utnyttja ytterligare data såsom förtroendescore, språkmodeller och listor med alternativa tecken. Genom att tillämpa dessa tekniker kan utvecklare avsevärt höja den övergripande kvaliteten på OCR‑utdata.

## Varför använda Aspose.OCR för .NET?
Aspose.OCR levererar **hög noggrannhet över 30+ språk** och kan bearbeta ett 500‑sidigt dokument på under 5 sekunder på en vanlig server, tack vare sin inbyggda motor. Biblioteket erbjuder ett **enradigt API**, fungerar **utan extra konfiguration på Windows, Linux och macOS** (tre stora plattformar) och ger direkt åtkomst till `RecognitionCharactersList` för efterbehandling av teckenalternativ.

## Förutsättningar

Innan du dyker ner i handledningen, se till att du har följande förutsättningar:

- Grundläggande kunskap om C# och .NET‑utveckling.  
- Visual Studio installerat på din maskin.  
- Aspose.OCR för .NET‑biblioteket, som du kan ladda ner Aspose OCR för .NET [här](https://releases.aspose.com/ocr/net/). Du kan också utforska andra Aspose‑utgåvor [här](https://releases.aspose.com/).

## Importera namnrymder

I ditt C#‑projekt, börja med att importera de nödvändiga namnrymderna:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Steg 1: initiera Aspose.OCR

Börja med att initiera en instans av Aspose.OCR:

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Steg 2: ange bildens sökväg

Ange sökvägen för bilden du vill analysera:

```csharp
// Image Path
string fullPath = dataDir + "sample.png";
```

## Steg 3: känna igen bild

Utför bildigenkänningsprocessen:

```csharp
// Recognize image           
RecognitionResult result = api.RecognizeImage(fullPath, new RecognitionSettings
{
    // Default or custom settings
});
```

## Hämta OCR‑teckenalternativ – översikt

`RecognitionCharactersList` är Aspose.OCR:s samling som lagrar alternativa teckenkandidater för varje igenkänt position. Efter att bilden har identifierats kan du hämta den här listan för att se vilka glyfer motorn övervägde och deras förtroendescore.

## Varför använda Aspose.OCR för .NET? 

Du bör välja Aspose.OCR när du behöver **deterministisk, hög‑snabb OCR** som fungerar över plattformar utan externa beroenden. Dess inbyggda motor levererar >95 % noggrannhet på standardbenchmark‑datamängder, och den inbyggda tecken‑alternativlistan möjliggör anpassade valideringsregler som kan öka noggrannheten ännu mer i domänspecifika scenarier.

## Steg 4: hämta alternativ för igenkända tecken

Hämta alternativ för igenkända tecken:

```csharp
List<char[]> resultWithChoices = result.RecognitionCharactersList;
```

## Steg 5: skriv ut resultaten

Visa igenkänningstexten och alternativen:

```csharp
// Print result
Console.WriteLine($"Text:\n {result.RecognitionText}");
Console.WriteLine("Choices:");
resultWithChoices.ForEach(a => Console.WriteLine($"character: {a[0]} . Choices: {a[1]} {a[2]} {a[3]} {a[4]}"));

Console.WriteLine("GetChoiceForRecognizedCharacters executed successfully");
```

## Vanliga problem och lösningar

`RecognitionSettings` konfigurerar OCR‑motorns parametrar såsom språk, ordbok och andra bearbetningsalternativ.

- **Tom `RecognitionCharactersList`** – Säkerställ att bilden har tillräcklig upplösning (minst 300 dpi) och god kontrast.  
- **Oväntade tecken** – Justera `RecognitionSettings` (t.ex. språk, ordbok) för att förbättra noggrannheten.  
- **Prestandaproblem** – Bearbeta bilder asynkront eller batcha flera bilder för att hålla UI responsivt.

## Vanliga frågor

### Q1: Är Aspose.OCR för .NET lämplig för storskalig dokumentbehandling?
Aspose.OCR är byggt för hög‑genomströmning; det kan hantera tusentals sidor per timme på en modest server, utnyttjar fler‑kärnors parallellism och håller minnesanvändningen låg genom att strömma sidor istället för att ladda hela dokumentet i minnet. Det erbjuder också batch‑bearbetnings‑API:er som låter dig köa stora jobb effektivt.

### Q2: Kan jag använda Aspose.OCR för .NET i en webbapplikation?
Ja, du kan integrera Aspose.OCR i ASP.NET Core, MVC eller Web API‑projekt. Biblioteket körs säkert i en servermiljö, och du kan exponera OCR‑slutpunkter som tar emot bilduppladdningar och returnerar både den igenkända texten och tecken‑alternativlistan. Det stödjer asynkron körning för att undvika blockering av webb‑förfrågningar.

### Q3: Finns det licensalternativ för Aspose.OCR för .NET?
Aspose erbjuder flera licensmodeller, inklusive **per‑developer**, **site‑wide** och **cloud‑based** alternativ. Alla licenser tar bort utvärderings‑vattenstämplar och låser upp hela funktionsuppsättningen, inklusive `RecognitionCharactersList`‑API:et, prioriterat stöd och åtkomst till framtida uppdateringar utan extra kostnad.

### Q4: Hur kan jag få support eller ställa frågor om Aspose.OCR för .NET?
Du kan få hjälp via det officiella Aspose‑community‑forumet på [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16), där produktingenjörer och community‑medlemmar svarar på tekniska frågor och delar bästa praxis‑tips. Dessutom erbjuder Aspose e‑postsupport för licensierade kunder.

### Q5: Finns det en gratis provversion för Aspose.OCR för .NET?
Ja, en fullt funktionell gratis provversion finns att ladda ner från Aspose‑webbplatsen. Provversionen innehåller alla funktioner, så att du kan utvärdera tecken‑alternativsfunktionerna utan begränsning, och den är endast vattenmärkt i resultatet för att indikera utvärderingsstatus.

## Ytterligare FAQ (AI‑vänlig)

**Q: Hur förbättrar OCR‑efterbehandling OCR‑noggrannheten?**  
A: Genom att granska de alternativa tecken som returneras i listan över igenkännings‑tecken kan du tillämpa kontext‑medvetna regler (t.ex. ordboks‑kontroller) för att välja den mest sannolika glyfen, vilket minskar felaktiga igenkänningar.

**Q: Kan jag filtrera listan över igenkännings‑tecken till endast de tre bästa alternativen?**  
A: Ja, iterera över varje `char[]` och använd de tre första elementen, som representerar de högst‑trovärdiga alternativen.

**Q: Är `RecognitionCharactersList` tillgänglig för alla språk?**  
A: Listan fylls för alla stödda språk; dock kan variationen i alternativ variera beroende på språkmodellen som konfigurerats i `RecognitionSettings`.

**Q: Vilka .NET‑versioner är kompatibla med den här handledningen?**  
A: Koden fungerar med .NET Framework 4.6+, .NET Core 3.1, .NET 5 och .NET 6+.

**Q: Var kan jag hitta fler Aspose OCR‑exempel?**  
A: Den officiella Aspose‑dokumentationen och GitHub‑repoet innehåller ytterligare exempel och hela **Aspose OCR‑handlednings**‑samlingen.

## Slutsats

I den här **Aspose OCR‑handledningen** har vi utforskat hur man **hämtar OCR‑teckenalternativ** med Aspose.OCR för .NET. Denna funktion lägger till en ny dimension i ditt OCR‑efterbehandlings‑arbetsflöde, vilket möjliggör smartare hantering av tvetydiga tecken och rikare logik som kan **förbättra OCR‑noggrannheten** i dina applikationer.

---

**Senast uppdaterad:** 2026-08-12  
**Testad med:** Aspose.OCR 24.11 for .NET  
**Författare:** Aspose  

{{< blocks/products/products-backtop-button >}}

## Relaterade handledningar

- [Hur man extraherar text från bild med Aspose.OCR för .NET](/ocr/net/text-recognition/get-recognition-result/)
- [Extrahera text från bild – OCR‑optimering med Aspose.OCR för .NET](/ocr/net/ocr-optimization/)
- [Ange tillåtna tecken OCR – Använd Aspose.OCR för .NET](/ocr/net/ocr-settings/specify-allowed-characters/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}