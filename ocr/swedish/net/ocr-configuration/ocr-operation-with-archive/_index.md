---
date: 2025-12-19
description: Lär dig hur du utför OCR på arkivbilder, konverterar bilder till text
  och extraherar text från arkivfiler med Aspose.OCR för .NET.
linktitle: How to Perform OCR on Archive Images with Aspose.OCR for .NET
second_title: Aspose.OCR .NET API
title: Hur man utför OCR på arkivbilder med Aspose.OCR för .NET
url: /sv/net/ocr-configuration/ocr-operation-with-archive/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man utför OCR på arkivbilder med Aspose.OCR för .NET

## Introduktion

I den här omfattande handledningen kommer du att upptäcka **hur man utför OCR** på arkiverade bildfiler med Aspose.OCR‑biblioteket för .NET. Oavsett om du behöver **konvertera bilder till text** eller **extrahera text från arkiv**‑filer, så guidar den steg‑för‑steg‑instruktion som följer dig genom allt – från att konfigurera din utvecklingsmiljö till att hämta den igenkända texten från varje bild i ett ZIP‑arkiv.

## Snabba svar
- **Vad täcker handledningen?** Utföra OCR på arkiv (ZIP) bilder med Aspose.OCR för .NET.  
- **Vilket primärt nyckelord är inriktat?** *how to perform ocr*.  
- **Behöver jag en licens?** En gratis provversion fungerar för utvärdering; en kommersiell licens krävs för produktion.  
- **Vilka .NET‑versioner stöds?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6+.  
- **Kan jag anpassa igenkänningsinställningarna?** Ja—använd `RecognitionSettings` för att finjustera noggrannheten.

## Vad är OCR och varför använda det på arkiv?

Optical Character Recognition (OCR) omvandlar skannade bilder eller PDF‑filer till sökbar, redigerbar text. När bilder är samlade i ett arkiv (t.ex. en ZIP‑fil) sparar det tid och minskar kodkomplexiteten att extrahera och känna igen varje bild i ett svep. Aspose.OCR:s `RecognizeMultipleImages`‑metod gör denna process enkel.

## Förutsättningar

- Visual Studio 2019 eller senare (eller någon .NET‑kompatibel IDE).  
- .NET Framework 4.5 + eller .NET Core 3.1 + installerat.  
- Tillgång till Aspose.OCR för .NET‑biblioteket (nedladdningslänk nedan).  
- En giltig Aspose.OCR‑licens för produktionsanvändning (provversion tillgänglig).

## Importera namnrymder

I ditt .NET‑projekt, se till att importera de nödvändiga namnrymderna för att få åtkomst till funktionaliteten som tillhandahålls av Aspose.OCR:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Ladda ner och installera Aspose.OCR för .NET

Hämta det senaste paketet från releasesidan **[here](https://releases.aspose.com/ocr/net/)** och följ de vanliga NuGet‑ eller manuella installationsstegen.

## Skaffa en licens

Skaffa en licens från **[purchase page](https://purchase.aspose.com/buy)** eller prova den **[free trial](https://releases.aspose.com/)**. Placera licensfilen i projektets rotkatalog och ladda den vid körning enligt beskrivningen i Aspose‑dokumentationen.

## Steg 1: Ställ in din dokumentkatalog

Börja med att initiera sökvägen till din dokumentkatalog:

```csharp
// ExStart:1
// The path to the documents directory.
string dataDir = "Your Document Directory";
// ExEnd:1
```

> **Pro tip:** Använd `Path.Combine` för plattformsoberoende hantering av sökvägar.

## Steg 2: Initiera Aspose.OCR

Skapa en instans av Aspose.OCR‑klassen för att kick‑starta OCR‑operationerna:

```csharp
// ExStart:3
AsposeOcr api = new AsposeOcr();
// ExEnd:3
```

## Steg 3: Ange bildsökväg

Definiera den fullständiga sökvägen till din arkivbild (ZIP‑fil som innehåller de bilder du vill läsa):

```csharp
// ExStart:4
string fullPath = dataDir + "OCR.zip";
// ExEnd:4
```

## Steg 4: Känn igen bild

Utför OCR‑igenkänning på det angivna arkivet med standard‑ eller anpassade inställningar. Detta anrop extraherar automatiskt varje bild från ZIP‑filen och kör OCR på den:

```csharp
// ExStart:5
RecognitionResult[] result = api.RecognizeMultipleImages(fullPath, new RecognitionSettings
{
   //default or custom settings
});
// ExEnd:5
```

> Du kan justera `RecognitionSettings` för att förbättra noggrannheten för specifika språk eller bildkvaliteter.

## Steg 5: Skriv ut resultat

Loopa igenom resultaten och skriv ut den igenkända texten för varje bild i arkivet:

```csharp
// ExStart:6
for (int i = 0; i < result.Length; i++)
{
	 Console.WriteLine($"Image: {i}\n Result:\n {result[i].RecognitionText}");
}
// ExEnd:6
```

Utdata visar varje bildindex följt av den extraherade strängen, vilket effektivt **konverterar bilder till text** och **extraherar text från arkiv**‑filer.

## Vanliga problem & felsökning

| Problem | Orsak | Lösning |
|-------|-------|----------|
| Ingen text returneras | Bildkvaliteten är för låg | Förbehandla bilder (t.ex. binarisering) eller justera `RecognitionSettings.Dpi` |
| Undantag vid ZIP‑läsning | Ogiltig arkivsökväg | Verifiera att `fullPath` pekar på en giltig `.zip`‑fil och att appen har läsbehörighet |
| Licens inte tillämpad | Licensfil saknas eller har inte laddats | Anropa `License license = new License(); license.SetLicense("Aspose.OCR.lic");` innan du skapar `AsposeOcr`‑instans |

## Vanliga frågor

**Q: Kan jag använda Aspose.OCR för .NET utan licens?**  
A: Ja, en gratis provversion finns för utvärdering, men en licensierad version krävs för produktionsdistributioner.

**Q: Stöder biblioteket lösenordsskyddade ZIP‑arkiv?**  
A: För närvarande fungerar `RecognizeMultipleImages` med standard‑ZIP‑filer. För krypterade arkiv, extrahera bilderna först med ett tredjepartsbibliotek och skicka sedan bildarrayen till OCR‑motorn.

**Q: Hur kan jag förbättra noggrannheten för handskriven text?**  
A: Aktivera flaggan `RecognitionSettings.EnableHandwritingRecognition` och ange en högre DPI‑inställning (t.ex. 300).

**Q: Finns det ett sätt att få förtroendescore för varje igenkänd rad?**  
A: Varje `RecognitionResult` innehåller en `Confidence`‑egenskap som du kan logga eller använda för att filtrera resultat med låg förtroendegrad.

## Slutsats

Du har nu ett komplett, produktionsklart arbetsflöde för att **utföra OCR på arkivbilder**, **konvertera bilder till text** och **extrahera text från arkiv**‑filer med Aspose.OCR för .NET. Integrera detta i dina applikationer för att möjliggöra sökbara dokumentarkiv, automatiserad datainmatning eller vilket scenario som helst där massutdrag av bildtext krävs.

## Ytterligare resurser

- **Aspose.OCR Forum:** För community‑support och avancerade scenarier, besök [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16).  
- **Tillfällig licens:** Om du behöver en korttidsutvärdering, begär en [temporary license](https://purchase.aspose.com/temporary-license/).  
- **Officiell dokumentation:** Håll dig uppdaterad med de senaste API‑ändringarna genom att granska [documentation](https://reference.aspose.com/ocr/net/).

---

**Senast uppdaterad:** 2025-12-19  
**Testad med:** Aspose.OCR 24.11 for .NET  
**Författare:** Aspose

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
