---
date: 2026-04-23
description: Lär dig hur du konverterar bilder till PDF i C# med Aspose.OCR, sparar
  flersidiga OCR-resultat som dokument och extraherar text från bilder.
keywords:
- extract text from images
- batch image to pdf
- convert scanned images pdf
linktitle: Konvertera bilder till PDF C# – Spara OCR‑resultat med flera sidor
second_title: Aspose.OCR .NET API
title: Extrahera text från bilder – Konvertera bilder till PDF C#
url: /sv/net/ocr-optimization/save-multipage-result-as-document/
weight: 14
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahera text från bilder – Konvertera bilder till PDF C#

## Introduktion

I den här handledningen kommer du att upptäcka hur du **extraherar text från bilder** samtidigt som du **konverterar bilder till PDF C#** med Aspose.OCR för .NET, och sedan sparar det flersidiga OCR‑resultatet som ett dokument. Oavsett om du behöver **batch image to pdf** för arkivering, **convert scanned images pdf** för efterlevnad, eller helt enkelt hämta sökbar text från bilder, kommer vi att gå igenom varje steg med tydliga förklaringar, praktiska tips och rekommendationer för bästa praxis.

## Snabba svar
- **Vad täcker den här handledningen?** Konvertera flera bilder till PDF/Docx/Txt/Xlsx och extrahera text från bilder med Aspose.OCR i C#.
- **Vilka utdataformat stöds?** Docx, Text, Pdf, och Xlsx (du kan också generera PDF direkt).
- **Behöver jag en licens?** En gratis provversion fungerar för utvärdering; en permanent licens krävs för produktion.
- **Vilka .NET‑versioner är kompatibla?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.
- **Kan jag extrahera text samtidigt som jag konverterar?** Ja—använd OCR‑resultaten för att hämta text innan du sparar.

## Vad är “extrahera text från bilder” och varför kombinera det med PDF‑konvertering?

Att extrahera text från bilder innebär att använda OCR (Optical Character Recognition) för att omvandla visuella tecken till sökbara, redigerbara strängar. När du **konverterar bilder till PDF C#**, bäddar du in dessa strängar i PDF‑filen så att dokumentet blir sökbart och indexerbart—perfekt för digital arkivering och datamining.

## Varför använda Aspose.OCR för denna uppgift?

- **Hög noggrannhet** över dussintals språk.  
- **Multipagesstöd** – hantera bildbatchar i ett enda anrop (idealiskt för **batch image to pdf**‑scenarier).  
- **Direkt sparande** till populära kontorsformat utan extra konverteringssteg.  
- **Full .NET‑integration** – inga inhemska beroenden, fungerar på Windows, Linux och molnruntider.

## Förutsättningar

1. Installerat Aspose.OCR för .NET. Du kan ladda ner det [här](https://releases.aspose.com/ocr/net/).  
2. Skaffat en gratis provversion eller en köpt licens – få en provversion [här](https://releases.aspose.com/) eller köp en [här](https://purchase.aspose.com/buy).  
3. Granskat den officiella [dokumentationen](https://reference.aspose.com/ocr/net/) för att bli bekant med API‑ytan.  
4. Gått med i gemenskapen på [supportforumet](https://forum.aspose.com/c/ocr/16) för hjälp med eventuella hinder.  

Nu när allt är klart, låt oss börja koda.

## Importera namnrymder

Börja med att lägga till de nödvändiga namnrymderna i din C#‑fil:

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using Aspose.OCR;
```

Dessa importeringar ger dig åtkomst till samlingar, filhantering, LINQ och Aspose OCR‑klasserna.

## Steg 1: Ange din dokumentkatalog

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";
```

Byt ut `"Your Document Directory"` mot den absoluta eller relativa sökvägen där dina källbilder finns och där du vill spara utdatafilerna.

## Steg 2: Initiera Aspose.OCR

```csharp
// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

Att skapa ett `AsposeOcr`‑objekt ger dig åtkomst till alla OCR‑operationer, inklusive arbetsflödet **convert images to PDF C#**.

## Steg 3: Känna igen bilder

```csharp
// Recognize image
List<RecognitionResult> result = api.RecognizeMultipleImages(
    new List<string> { dataDir + "sample.png", dataDir + "sample_bad.png" },
    new RecognitionSettings { }
).ToList();
```

Metoden `RecognizeMultipleImages` bearbetar varje fil i listan och returnerar en samling av `RecognitionResult`. Du kan mata in valfritt antal bilder, vilket är perfekt för scenarier med **convert scanned images pdf**.

## Steg 4: Spara resultat i föredragna format

```csharp
// Save the result in your preferred format
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR()+"sample.docx", SaveFormat.Docx, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.txt", SaveFormat.Text, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.pdf", SaveFormat.Pdf, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.xlsx", SaveFormat.Xlsx, result);
```

Välj det format som bäst passar ditt efterföljande arbetsflöde:

- **Docx** – redigerbart Word‑dokument med sökbar text.  
- **Text** – ren text‑extraktion för snabb datamining (**extract text from images**).  
- **Pdf** – den klassiska PDF‑utmatningen, idealisk för arkivering.  
- **Xlsx** – kalkylbladsrepresentation för tabulär data.

## Vanliga användningsfall

- **Digital arkivering:** Konvertera skannade papperskontrakt till sökbara PDF‑filer.  
- **Automatisering av datainmatning:** Extrahera text från kvitton eller fakturor och mata in den i en databas.  
- **Batch‑bearbetning:** Hantera tusentals bilder i ett enda jobb med minimal kod—perfekt för behov av **batch image to pdf**.

## Felsökning & tips

- **Stora bilduppsättningar:** Bearbeta bilder i mindre batchar för att undvika minnesökningar.  
- **Bildkvalitet:** Se till att bilderna har minst 300 dpi för optimal OCR‑noggrannhet.  
- **Licensfel:** Verifiera att din licensfil är korrekt laddad innan du anropar OCR‑metoder.  
- **Tomma resultat:** OCR‑motorn returnerar ett tomt `RecognitionResult` för oläsbara sidor; kontrollera `result[i].Text` för null eller tomma strängar och hantera därefter.

## Vanliga frågor

**Q: Kan jag konvertera bilder till PDF C# utan att använda OCR?**  
A: Ja, du kan använda Aspose.PDF eller andra bibliotek för ren bild‑till‑PDF‑konvertering, men OCR lägger till sökbar text.

**Q: Hur extraherar jag text från bilder i C# efter konvertering?**  
A: Listan `result` som returneras av `RecognizeMultipleImages` innehåller `Text`‑egenskaper som du kan skriva till en `.txt`‑fil eller bearbeta direkt.

**Q: Är det möjligt att ange anpassade sidmarginaler eller orientering?**  
A: När du sparar till PDF eller Docx kan du ändra dokumentlayouten via Aspose.Words‑ eller Aspose.PDF‑API:er innan du anropar `SaveMultipageDocument`.

**Q: Vad händer om en bild inte kan läsas?**  
A: OCR‑motorn returnerar ett tomt `RecognitionResult` för den sidan; du kan kontrollera `result[i].Text` för null eller tomma strängar och hantera därefter.

**Q: Stöder API:et molnimplementering?**  
A: Ja, biblioteket fungerar på alla .NET‑runtime‑miljöer, inklusive Azure Functions och AWS Lambda, så länge runtime‑versionen uppfyller kraven.

---

**Senast uppdaterad:** 2026-04-23  
**Testat med:** Aspose.OCR 24.11 för .NET  
**Författare:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}