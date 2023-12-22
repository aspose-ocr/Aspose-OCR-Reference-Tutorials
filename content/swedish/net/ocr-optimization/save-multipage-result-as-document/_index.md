---
title: Spara flersidigt resultat som dokument i OCR-bildigenkänning
linktitle: Spara flersidigt resultat som dokument i OCR-bildigenkänning
second_title: Aspose.OCR .NET API
description: Lås upp potentialen hos Aspose.OCR för .NET. Spara enkelt flersidiga OCR-resultat som dokument med denna omfattande steg-för-steg-guide.
type: docs
weight: 14
url: /sv/net/ocr-optimization/save-multipage-result-as-document/
---
## Introduktion

Välkommen till den fascinerande världen av optisk teckenigenkänning (OCR) med Aspose.OCR för .NET! I den här självstudien kommer vi att utforska hur man kan utnyttja funktionerna i Aspose.OCR för att spara flersidiga OCR-resultat som dokument. Oavsett om du är en erfaren utvecklare eller precis har börjat med OCR, kommer den här guiden att leda dig genom varje steg, vilket säkerställer att du får ut det mesta av detta kraftfulla verktyg.

## Förutsättningar

Innan vi dyker in i handledningen, låt oss se till att du har allt konfigurerat:

1.  Installera Aspose.OCR för .NET: Börja med att ladda ner och installera Aspose.OCR för .NET. Du kan hitta de nödvändiga filerna[här](https://releases.aspose.com/ocr/net/).

2.  Få din gratis provperiod eller licens: Om du inte redan har gjort det kan du få en gratis provperiod[här](https://releases.aspose.com/) eller köp en licens[här](https://purchase.aspose.com/buy).

3.  Utforska dokumentationen: Bekanta dig med[dokumentation](https://reference.aspose.com/ocr/net/)för Aspose.OCR för .NET. Det är din bästa resurs för detaljerad information.

4.  Få tillgång till supportforum: Om du stöter på några problem eller har frågor kan du[supportforum](https://forum.aspose.com/c/ocr/16) är en värdefull gemenskapsresurs.

Nu när du är klar, låt oss hoppa in i steg-för-steg-guiden.

## Importera namnområden

Börja ditt projekt genom att importera de nödvändiga namnrymden:

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using Aspose.OCR;
```

## Steg 1: Ställ in din dokumentkatalog

```csharp
// Sökvägen till dokumentkatalogen.
string dataDir = "Your Document Directory";
```

 Se till att byta ut`"Your Document Directory"` med den faktiska sökvägen till din dokumentkatalog.

## Steg 2: Initiera Aspose.OCR

```csharp
// Initiera en instans av AsposeOcr
AsposeOcr api = new AsposeOcr();
```

 Skapa en instans av`AsposeOcr` för att komma åt OCR-funktionerna.

## Steg 3: Känna igen bilder

```csharp
// Känner igen bilden
List<RecognitionResult> result = api.RecognizeMultipleImages(
    new List<string> { dataDir + "sample.png", dataDir + "sample_bad.png" },
    new RecognitionSettings { }
).ToList();
```

Använd Aspose.OCR för att känna igen text från flera bilder. Justera filsökvägarna efter dina bildfiler.

## Steg 4: Spara resultat i önskade format

```csharp
// Spara resultatet i önskat format
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR()+"sample.docx", SaveFormat.Docx, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.txt", SaveFormat.Text, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.pdf", SaveFormat.Pdf, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.xlsx", SaveFormat.Xlsx, result);
```

Välj önskat format (Docx, Text, Pdf eller Xlsx) och spara OCR-resultaten som ett flersidigt dokument.

## Slutsats

Grattis! Du har framgångsrikt lärt dig hur du sparar flersidiga OCR-resultat som dokument med Aspose.OCR för .NET. Detta mångsidiga verktyg öppnar upp en värld av möjligheter för textigenkänning i dina projekt.

## FAQ's

### F1: Är en tillfällig licens tillgänglig för teständamål?

 A1: Ja, du kan få en tillfällig licens[här](https://purchase.aspose.com/temporary-license/) för att testa Aspose.OCR.

### F2: Kan jag känna igen text från bilder i olika format?

A2: Absolut! Aspose.OCR stöder olika bildformat, vilket säkerställer flexibilitet i dina OCR-uppgifter.

### F3: Finns det några begränsningar för antalet bilder för igenkänning?

S3: Antalet bilder du kan bearbeta beror på din licens. Se dokumentationen för detaljer.

### F4: Hur kan jag hantera fel under OCR-igenkänning?

S4: Se dokumentationen för bästa praxis för felhantering eller sök hjälp i supportforumen.

### F5: Stöder Aspose.OCR andra språk än engelska?

S5: Ja, Aspose.OCR stöder flera språk. Utforska dokumentationen för information om språksupport.