---
date: 2026-04-12
description: Lär dig hur du extraherar text från zip-filer genom att utföra OCR på
  arkivbilder med Aspose.OCR för .NET, inklusive installation, kod och felsökning.
keywords:
- extract text from zip
- read images from zip
- Aspose OCR .NET
linktitle: Hur man extraherar text från ZIP‑arkiv med Aspose.OCR för .NET
second_title: Aspose.OCR .NET API
title: Hur man extraherar text från ZIP‑arkiv med Aspose.OCR för .NET
url: /sv/net/ocr-configuration/ocr-operation-with-archive/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man extraherar text från ZIP‑arkiv med Aspose.OCR för .NET

## Introduktion

I den här omfattande handledningen kommer du att lära dig **hur man extraherar text från zip**‑arkiv genom att tillämpa OCR på varje bild i arkivet. Oavsett om du behöver **konvertera bilder till text**, **läsa bilder från zip**, eller bygga ett sökbart dokumentarkiv, så guidar den steg‑för‑steg‑instruktionen nedan dig genom allt—från installation av Aspose.OCR för .NET till utskrift av den igenkända texten för varje bild i en ZIP‑fil.

## Snabba svar
- **Vad täcker den här handledningen?** Extrahera text från ZIP‑arkiv med Aspose.OCR för .NET.  
- **Vilket primärt nyckelord är inriktat?** *extract text from zip*.  
- **Behöver jag en licens?** En gratis provversion fungerar för utvärdering; en kommersiell licens krävs för produktion.  
- **Vilka .NET‑versioner stöds?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6+.  
- **Kan jag anpassa igenkänningsinställningarna?** Ja—använd `RecognitionSettings` för att finjustera noggrannheten för olika språk eller bildkvaliteter.

## Vad är OCR och varför använda det på ZIP‑arkiv?

Optisk teckenigenkänning (OCR) omvandlar skannade bilder eller PDF‑filer till sökbar, redigerbar text. När dessa bilder är paketerade i en ZIP‑fil sparar det tid och minskar kodkomplexiteten att extrahera och känna igen varje bild i ett enda steg. Aspose.OCR:s `RecognizeMultipleImages`‑metod gör processen enkel, så att du kan **läsa bilder från zip** och omedelbart få den textuella innehållet.

## Förutsättningar

- Visual Studio 2019 eller senare (eller någon .NET‑kompatibel IDE).  
- .NET Framework 4.5 + eller .NET Core 3.1 + installerat.  
- Tillgång till Aspose.OCR för .NET‑biblioteket (nedladdningslänk nedan).  
- En giltig Aspose.OCR‑licens för produktionsanvändning (provversion tillgänglig).

## Importera namnrymder

I ditt .NET‑projekt, importera de nödvändiga namnrymderna för att få åtkomst till funktionaliteten som tillhandahålls av Aspose.OCR:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Ladda ner och installera Aspose.OCR för .NET

Hämta det senaste paketet från releasesidan **[här](https://releases.aspose.com/ocr/net/)** och följ de vanliga NuGet‑ eller manuella installationsstegen.

## Skaffa en licens

Skaffa en licens från **[köpsida](https://purchase.aspose.com/buy)** eller prova **[gratis provversion](https://releases.aspose.com/)**. Placera licensfilen i ditt projektrot och ladda den vid körning enligt beskrivningen i Aspose‑dokumentationen.

## Steg 1: Ställ in din dokumentkatalog

Börja med att initiera sökvägen till din dokumentkatalog. Denna mapp kommer att innehålla ZIP‑arkivet du vill bearbeta:

```csharp
// ExStart:1
// The path to the documents directory.
string dataDir = "Your Document Directory";
// ExEnd:1
```

> **Proffstips:** Använd `Path.Combine` för plattformsoberoende hantering av sökvägar.

## Steg 2: Initiera Aspose.OCR

Skapa en instans av Aspose.OCR‑klassen för att starta OCR‑operationerna:

```csharp
// ExStart:3
AsposeOcr api = new AsposeOcr();
// ExEnd:3
```

## Steg 3: Ange sökvägen till ZIP‑arkivet

Definiera den fullständiga sökvägen till ditt arkiv (ZIP‑fil som innehåller bilderna du vill läsa):

```csharp
// ExStart:4
string fullPath = dataDir + "OCR.zip";
// ExEnd:4
```

## Steg 4: Känn igen bilder i ZIP‑filen

Utför OCR‑igenkänning på det angivna arkivet med standard‑ eller anpassade inställningar. Detta anrop extraherar automatiskt varje bild från ZIP‑filen och kör OCR på den:

```csharp
// ExStart:5
RecognitionResult[] result = api.RecognizeMultipleImages(fullPath, new RecognitionSettings
{
   //default or custom settings
});
// ExEnd:5
```

> Du kan justera `RecognitionSettings` för att förbättra noggrannheten för specifika språk, DPI, eller för att aktivera handskriftigenkänning.

## Steg 5: Skriv ut den extraherade texten

Loopa igenom resultaten och skriv ut den igenkända texten för varje bild i arkivet. Här extraherar du faktiskt **text från zip**:

```csharp
// ExStart:6
for (int i = 0; i < result.Length; i++)
{
	 Console.WriteLine($"Image: {i}\n Result:\n {result[i].RecognitionText}");
}
// ExEnd:6
```

Utdata visar varje bildindex följt av den extraherade strängen, vilket effektivt **konverterar bilder till text** och **extraherar text från arkiv**‑filer i ett enda steg.

## Varför detta tillvägagångssätt är viktigt

- **Batch‑behandling:** Hanterar valfritt antal bilder i en ZIP utan manuell extrahering.  
- **Prestanda:** Minskar I/O‑överhead genom att läsa direkt från arkivet.  
- **Skalbarhet:** Fungerar med stora ZIP‑filer och kan kombineras med async‑mönster för hög‑genomströmning.

## Vanliga problem & felsökning

| Problem | Orsak | Lösning |
|---------|-------|----------|
| Ingen text returnerad | Bildkvaliteten är för låg | Förbehandla bilder (t.ex. binarisering) eller justera `RecognitionSettings.Dpi` |
| Undantag vid ZIP‑läsning | Ogiltig arkivsökväg | Verifiera att `fullPath` pekar på en giltig `.zip`‑fil och att appen har läsbehörighet |
| Licens inte tillämpad | Licensfil saknas eller är inte laddad | Anropa `License license = new License(); license.SetLicense("Aspose.OCR.lic");` innan du skapar `AsposeOcr`‑instansen |

## Vanliga frågor

**Q: Kan jag använda Aspose.OCR för .NET utan licens?**  
A: Ja, en gratis provversion finns för utvärdering, men en licensierad version krävs för produktionsdistributioner.

**Q: Stöder biblioteket lösenordsskyddade ZIP‑arkiv?**  
A: För närvarande fungerar `RecognizeMultipleImages` med standard‑ZIP‑filer. För krypterade arkiv, extrahera bilderna först med ett tredjepartsbibliotek och skicka sedan bildarrayen till OCR‑motorn.

**Q: Hur kan jag förbättra noggrannheten för handskriven text?**  
A: Aktivera flaggan `RecognitionSettings.EnableHandwritingRecognition` och ange en högre DPI‑inställning (t.ex. 300).

**Q: Finns det ett sätt att få förtroendesiffror för varje igenkänd rad?**  
A: Varje `RecognitionResult` innehåller en `Confidence`‑egenskap som du kan logga eller använda för att filtrera resultat med låg förtroendegrad.

## Ytterligare resurser

- **Aspose.OCR‑forum:** För community‑support och avancerade scenarier, besök [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16).  
- **Tillfällig licens:** Om du behöver en korttidsutvärdering, begär en [temporary license](https://purchase.aspose.com/temporary-license/).  
- **Officiell dokumentation:** Håll dig uppdaterad med de senaste API‑ändringarna genom att granska [documentation](https://reference.aspose.com/ocr/net/).

---

**Senast uppdaterad:** 2026-04-12  
**Testad med:** Aspose.OCR 24.11 för .NET  
**Författare:** Aspose

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}