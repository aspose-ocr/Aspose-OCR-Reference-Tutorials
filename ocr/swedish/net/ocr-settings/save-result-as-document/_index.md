---
title: Spara resultat som dokument i OCR-bildigenkänning
linktitle: Spara resultat som dokument i OCR-bildigenkänning
second_title: Aspose.OCR .NET API
description: Lås upp potentialen hos Aspose.OCR för .NET. Känn enkelt igen text i bilder och spara resultat i olika dokumentformat.
weight: 10
url: /sv/net/ocr-settings/save-result-as-document/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Spara resultat som dokument i OCR-bildigenkänning

## Introduktion

Välkommen till den spännande världen av optisk teckenigenkänning (OCR) med Aspose.OCR för .NET! I denna omfattande handledning kommer vi att fördjupa oss i krångligheterna med att använda Aspose.OCR för att känna igen text i bilder och visa hur man sparar resultaten i olika dokumentformat.

## Förutsättningar

Innan vi ger oss ut på denna OCR-resa, se till att du har följande förutsättningar på plats:

-  Aspose.OCR för .NET. Se till att du har Aspose.OCR-biblioteket installerat. Du kan ladda ner den[här](https://releases.aspose.com/ocr/net/).

-  Dokumentkatalog: Ha en utsedd katalog för dina dokument och uppdatera`dataDir` variabel i den angivna koden.

## Importera namnområden

Börja med att importera de nödvändiga namnrymden. Dessa är byggstenarna som ger din kod möjlighet att använda OCR.

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

Låt oss nu dela upp exemplet i flera steg:

## Steg 1: Initiera Aspose.OCR

```csharp
// Sökvägen till dokumentkatalogen.
string dataDir = "Your Document Directory";

// Initiera en instans av AsposeOcr
AsposeOcr api = new AsposeOcr();
```

Detta steg sätter scenen genom att initiera Aspose.OCR API.

## Steg 2: Känn igen bild

```csharp
// Känner igen bilden
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings { });
```

Här använder vi Aspose.OCR för att känna igen text i den angivna bilden (ersätt "sample.png" med din bildfil).

## Steg 3: Spara resultat i olika format

```csharp
// Spara resultatet i önskat format
result.Save(RunExamples.GetDataDir_OCR() + "sample.docx", SaveFormat.Docx);
result.Save(RunExamples.GetDataDir_OCR() + "sample.txt", SaveFormat.Text);
result.Save(RunExamples.GetDataDir_OCR() + "sample.pdf", SaveFormat.Pdf);
result.Save(RunExamples.GetDataDir_OCR() + "sample.xlsx", SaveFormat.Xlsx);
```

Anpassa detta steg baserat på dina behov. Aspose.OCR låter dig spara den igenkända texten i olika dokumentformat som DOCX, TXT, PDF och XLSX.

## Steg 4: Visa framgångsmeddelande

```csharp
Console.WriteLine("SaveResultAsDocument executed successfully");
```

Ett enkelt bekräftelsemeddelande för att låta dig veta att processen slutfördes utan problem.

Genom att följa dessa steg har du framgångsrikt utnyttjat kraften i Aspose.OCR för .NET för att känna igen text i bilder och spara resultaten i olika dokumentformat.

## Slutsats

Sammanfattningsvis öppnar Aspose.OCR för .NET upp en värld av möjligheter för textigenkänning i bilder. Oavsett om du extraherar data eller skapar sökbara dokument, förenklar Aspose.OCR processen med sitt intuitiva API.

## FAQ's

### Q1. Är Aspose.OCR kompatibel med olika bildformat?

S1: Ja, Aspose.OCR stöder ett brett utbud av bildformat, vilket säkerställer flexibilitet i dina OCR-uppgifter.

### F2: Kan jag anpassa igenkänningsinställningarna för bättre noggrannhet?

A2: Absolut! Aspose.OCR tillhandahåller igenkänningsinställningar för att finjustera OCR-processen enligt dina specifika krav.

### F3: Finns det en gratis provperiod?

 A3: Ja, du kan komma igång med en gratis provperiod[här](https://releases.aspose.com/).

### F4: Hur kan jag få tillfälliga licenser för Aspose.OCR?

 A4: Tillfälliga licenser kan erhållas[här](https://purchase.aspose.com/temporary-license/).

### F5: Var kan jag söka hjälp eller få kontakt med samhället?

 S5: Gå med i Aspose.OCR-communityt på[Aspose Forum](https://forum.aspose.com/c/ocr/16) för stöd och diskussioner.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
