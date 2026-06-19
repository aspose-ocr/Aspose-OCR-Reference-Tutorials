---
date: 2026-04-29
description: Lär dig hur du konverterar bilder till PDF i C# med Aspose.OCR, sparar
  flersidiga OCR‑resultat som dokument och extraherar text från bilder i C#.
keywords:
- convert images to pdf
- extract text from images
- c# ocr library
- convert images to xlsx
- generate pdf from tiff
linktitle: Konvertera bilder till PDF C# – Spara flersidigt OCR‑resultat
second_title: Aspose.OCR .NET API
title: Konvertera bilder till PDF C# – Spara flersidigt OCR‑resultat
url: /sv/net/ocr-optimization/save-multipage-result-as-document/
weight: 14
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Konvertera bilder till PDF C# – Spara flersidig OCR-resultat

## Introduktion

I den här handledningen kommer du att upptäcka hur du **konverterar bilder till PDF C#** med det kraftfulla **Aspose.OCR**‑biblioteket för .NET. Oavsett om du behöver **konvertera skannade TIFF‑filer till sökbara PDF‑filer**, extrahera text från bilder för datamining, eller generera en Excel‑arbetsbok från en mängd bilder, guidar den här artikeln dig genom varje steg med tydliga förklaringar, praktiska tips och rekommendationer för bästa praxis.

## Snabba svar
- **Vad täcker den här handledningen?** Konvertera flera bilder till PDF, Docx, Text och Xlsx med Aspose.OCR i C# och spara OCR‑resultatet som ett flersidigt dokument.  
- **Vilka utdataformat stöds?** Docx, Text, Pdf och Xlsx (du kan också exportera PDF direkt).  
- **Behöver jag en licens?** En gratis provversion fungerar för utvärdering; en permanent licens krävs för produktion.  
- **Vilka .NET‑versioner är kompatibla?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.  
- **Kan jag extrahera text samtidigt som jag konverterar?** Ja – använd OCR‑resultaten för att hämta sökbar text innan du sparar.

## Vad är “convert images to PDF C#”?

Att konvertera bilder till PDF i C# innebär att programmässigt ta en eller flera bitmap‑filer (PNG, JPEG, TIFF osv.) och generera ett PDF‑dokument som bevarar den visuella layouten samtidigt som sökbar text kan inbäddas via OCR. Aspose.OCR tillhandahåller ett **c# ocr library** som hanterar detta från början till slut, inklusive stöd för flersidiga dokument och direkt sparande till populära kontorsformat.

## Varför använda Aspose.OCR för denna uppgift?

- **Hög noggrannhet i OCR** som stödjer dussintals språk.  
- **Flersidig bearbetning** – mata in en hel mapp med bilder och få en enda sökbar PDF.  
- **Direkt export** till Docx, Text, Pdf och Xlsx utan ett extra konverteringssteg.  
- **Ren .NET** – inga inhemska beroenden, fungerar på Windows, Linux och molnruntimes.  

## Förutsättningar

1. Installera Aspose.OCR för .NET. Du kan ladda ner det [here](https://releases.aspose.com/ocr/net/).  
2. Skaffa en gratis provlicens eller en köpt licens – få en provlicens [here](https://releases.aspose.com/) eller köp en [here](https://purchase.aspose.com/buy).  
3. Läs den officiella [documentation](https://reference.aspose.com/ocr/net/) för att bli bekant med API‑ytan.  
4. Gå med i communityn på [support forums](https://forum.aspose.com/c/ocr/16) för hjälp med eventuella hinder.  

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

## Steg 3: Känn igen bilder

```csharp
// Recognize image
List<RecognitionResult> result = api.RecognizeMultipleImages(
    new List<string> { dataDir + "sample.png", dataDir + "sample_bad.png" },
    new RecognitionSettings { }
).ToList();
```

Metoden `RecognizeMultipleImages` bearbetar varje fil i listan och returnerar en samling av `RecognitionResult`. Du kan mata in valfritt antal bilder, vilket är perfekt för scenarier som **convert scanned images to PDF**.

## Steg 4: Spara resultat i önskat format

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
- **Pdf** – den klassiska PDF‑utgången, idealisk för arkivering.  
- **Xlsx** – kalkylbladsrepresentation för tabulär data (**convert images to xlsx**).

## Så konverterar du bilder till PDF C# – Steg‑för‑steg‑sammanfattning

1. **Förbered mappen** med de bilder du vill konvertera.  
2. **Skapa en `AsposeOcr`‑instans** för att komma åt OCR‑funktionerna.  
3. **Anropa `RecognizeMultipleImages`** för att få OCR‑resultat för varje fil.  
4. **Spara det flersidiga resultatet** med `SaveMultipageDocument` i det format du behöver.

## Vanliga användningsområden

- **Digital arkivering:** Konvertera skannade papperskontrakt till sökbara PDF‑filer.  
- **Automatisering av datainmatning:** Extrahera text från kvitton eller fakturor och mata in den i en databas.  
- **Batch‑bearbetning:** Hantera tusentals bilder i ett enda jobb med minimal kod.  
- **Generera PDF från TIFF:** Perfekt för högupplösta skannade dokument som måste behålla originalets kvalitet.

## Felsökning & Tips

- **Stora bildsamlingar:** Bearbeta bilder i mindre batcher för att undvika minnesspikar.  
- **Bildkvalitet:** Säkerställ att bilder är minst 300 dpi för optimal OCR‑noggrannhet.  
- **Licensfel:** Verifiera att din licensfil är korrekt laddad innan du anropar OCR‑metoder.  
- **Tomma resultat:** Om en bild inte kan läsas kommer motsvarande `RecognitionResult` ha en tom `Text`‑egenskap – kontrollera null eller tomma strängar innan du sparar.  

## Vanliga frågor

**Q: Kan jag konvertera bilder till PDF C# utan att använda OCR?**  
A: Ja, du kan använda Aspose.PDF eller andra bibliotek för ren bild‑till‑PDF‑konvertering, men OCR lägger till sökbar text som gör PDF‑filen mycket mer användbar.

**Q: Hur extraherar jag text från bilder C# efter konvertering?**  
A: Listan `result` som returneras av `RecognizeMultipleImages` innehåller en `Text`‑egenskap för varje sida. Du kan skriva dessa strängar till en `.txt`‑fil eller bearbeta dem direkt i din applikation.

**Q: Är det möjligt att ange anpassade sidmarginaler eller orientering?**  
A: När du sparar till PDF eller Docx kan du ändra dokumentlayouten via Aspose.Words eller Aspose.PDF‑API:er innan du anropar `SaveMultipageDocument`.

**Q: Vad händer om en bild inte kan läsas?**  
A: OCR‑motorn returnerar ett tomt `RecognitionResult` för den sidan; du kan upptäcka detta och hoppa över eller logga den problematiska filen.

**Q: Stöder API‑et moln‑distribution?**  
A: Ja, biblioteket fungerar på alla .NET‑runtime, inklusive Azure Functions och AWS Lambda, så länge runtime‑kraven uppfylls.

## Slutsats

Du har nu ett komplett, produktionsklart arbetsflöde för att **konvertera bilder till PDF C#**, extrahera sökbar text och till och med generera Word-, ren‑text‑ eller Excel‑filer från en mängd bilder. Känn dig fri att experimentera med olika utdataformat, justera OCR‑inställningar för specifika språk eller integrera koden i större dokument‑bearbetningspipelines.

---

**Senast uppdaterad:** 2026-04-29  
**Testat med:** Aspose.OCR 24.11 för .NET  
**Författare:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}