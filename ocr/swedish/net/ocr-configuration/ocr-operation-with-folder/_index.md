---
title: OCRoperation med mapp i OCR-bildigenkänning
linktitle: OCRoperation med mapp i OCR-bildigenkänning
second_title: Aspose.OCR .NET API
description: Lås upp kraften med OCR-bildigenkänning i .NET med Aspose.OCR. Extrahera text enkelt från bilder.
weight: 11
url: /sv/net/ocr-configuration/ocr-operation-with-folder/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCRoperation med mapp i OCR-bildigenkänning

## Introduktion

Välkommen till världen av Optical Character Recognition (OCR) med Aspose.OCR för .NET! Om du vill extrahera text från bilder sömlöst i dina .NET-applikationer är du på rätt plats. Denna handledning guidar dig genom processen för OCR-bildigenkänning med mappar, och utnyttjar de kraftfulla funktionerna i Aspose.OCR.

## Förutsättningar

Innan du dyker in i handledningen, se till att du har följande förutsättningar:

- En praktisk kunskap om C# och .NET utveckling.
- Visual Studio installerat på din dator.
-  Aspose.OCR för .NET-bibliotek, som du kan ladda ner[här](https://releases.aspose.com/ocr/net/).
- Grundläggande förståelse för OCR-koncept.

## Importera namnområden

I din C#-kod, se till att importera de nödvändiga namnrymden för att använda Aspose.OCR. Inkludera följande i början av ditt manus:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Steg 1: Ställ in dokumentkatalog

```csharp
// ExStart:1
// Sökvägen till dokumentkatalogen.
string dataDir = "Your Document Directory";
```

Se till att du ersätter "Din dokumentkatalog" med den faktiska sökvägen där dina bilder lagras.

## Steg 2: Initiera Aspose.OCR

```csharp
// Initiera en instans av AsposeOcr
AsposeOcr api = new AsposeOcr();
```

Skapa en instans av klassen AsposeOcr för att använda dess funktioner.

## Steg 3: Ange bildsökväg

```csharp
//Bildväg
string fullPath = dataDir + "OCR";
```

Sammanfoga sökvägen till dokumentkatalogen med den specifika mappen som innehåller dina bilder.

## Steg 4: Känna igen bilder

```csharp
// Känner igen bilden
RecognitionResult[] result = api.RecognizeMultipleImages(fullPath, new RecognitionSettings
{
    //standard eller anpassad
});
```

Använd metoden RecognizeMultipleImages för att utföra OCR på flera bilder i den angivna mappen.

## Steg 5: Skriv ut resultat

```csharp
// Skriv ut resultat
for (int i = 0; i < result.Length; i++)
{
    Console.WriteLine($"Image: {i}\n Result:\n {result[i].RecognitionText}");
}
```

Gå igenom resultaten och skriv ut den igenkända texten för varje bild.

## Steg 6: Slutsats

```csharp
// Exend:1
Console.WriteLine("OCROperationWithFolder executed successfully");
```

Se till att slutsatsen av ditt skript är nådd för att betyda framgångsrik exekvering av OCR-operationen med mappar.

## Slutsats

Grattis! Du har framgångsrikt lärt dig hur du implementerar OCR-bildigenkänning med mappar med Aspose.OCR för .NET. Detta kraftfulla verktyg öppnar upp en myriad av möjligheter för att extrahera text från bilder i dina .NET-program.

## FAQ's

### F1: Kan jag använda Aspose.OCR för .NET i kommersiella projekt?

 S1: Ja, Aspose.OCR för .NET är en kommersiell produkt. För licensinformation, besök[här](https://purchase.aspose.com/buy).

### Q2:. Finns det en gratis provperiod?

 A2: Ja, du kan utforska en gratis provperiod[här](https://releases.aspose.com/).

### F3: Var kan jag hitta dokumentationen?

 S3: Dokumentationen finns tillgänglig[här](https://reference.aspose.com/ocr/net/).

### F4: Hur kan jag få tillfällig licensiering?

 A4: Tillfälliga licenser kan erhållas[här](https://purchase.aspose.com/temporary-license/).

### F5: Behöver du support eller har frågor?

 A5: Besök[Aspose.OCR-forum](https://forum.aspose.com/c/ocr/16) för samhällsstöd.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
