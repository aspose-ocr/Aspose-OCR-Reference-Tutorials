---
title: Få rektanglar för linjer i OCR-bildigenkänning
linktitle: Få rektanglar för linjer i OCR-bildigenkänning
second_title: Aspose.OCR .NET API
description: Utforska Aspose.OCR för .NET, din nyckel till exakt OCR-bildigenkänning. Släpp lös kraften i textextraktion utan ansträngning.
weight: 10
url: /sv/net/image-and-drawing-recognition/get-rectangles-for-lines/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Få rektanglar för linjer i OCR-bildigenkänning

## Introduktion

Välkommen till Aspose.OCR-världen för .NET, ett kraftfullt verktyg som låter dig utnyttja potentialen hos Optical Character Recognition (OCR) i dina .NET-applikationer. Oavsett om du är en erfaren utvecklare eller en nyfiken entusiast, kommer den här guiden att leda dig genom processen att få rektanglar för linjer i OCR-bildigenkänning med Aspose.OCR.

## Förutsättningar

Innan du dyker in i handledningen, se till att du har följande förutsättningar på plats:

- Grundläggande kunskap om C# och .NET utveckling.
- En integrerad utvecklingsmiljö (IDE) som Visual Studio.
-  Aspose.OCR för .NET-biblioteket installerat. Du kan ladda ner den[här](https://releases.aspose.com/ocr/net/).
- En exempelbild som innehåller text för OCR-igenkänning.

## Importera namnområden

Se till att du har de nödvändiga namnrymden importerade till ditt projekt. Lägg till följande rader överst i din C#-fil:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

Låt oss nu dela upp processen för att få rektanglar för linjer i OCR-bildigenkänning i lätta att följa steg.

## Steg 1: Konfigurera din dokumentkatalog

```csharp
// ExStart:3
string dataDir = "Your Document Directory";
// Exend:3
```

 Byta ut`"Your Document Directory"` med den faktiska sökvägen till din dokumentkatalog.

## Steg 2: Initiera Aspose.OCR

```csharp
// ExStart:4
AsposeOcr api = new AsposeOcr();
// Exend:4
```

 Skapa en instans av`AsposeOcr` klass för att komma åt OCR-funktionen.

## Steg 3: Ange bildsökväg

```csharp
// ExStart:5
string fullPath = dataDir + "sample.png";
// Exend:5
```

Definiera hela sökvägen till bilden du vill utföra OCR på.

## Steg 4: Känn igen bild och få rektanglar

```csharp
// ExStart: 6
List<Rectangle> lines = api.GetRectangles(fullPath, AreasType.LINES, false);
// Exend:6
```

 Använd`GetRectangles` metod för att hämta rektanglar för linjer i den angivna bilden.

## Steg 5: Skriv ut resultat

```csharp
// ExStart:7
Console.WriteLine("Areas coordinates:");
lines.ForEach(a => Console.WriteLine($"x:{a.X} y:{a.Y} width:{a.Width} height:{a.Height}"));
// Exend:7
```

Skriv ut koordinaterna för de upptäckta områdena till konsolen.

## Slutsats

Grattis! Du har framgångsrikt erhållit rektanglar för linjer i OCR-bildigenkänning med Aspose.OCR för .NET. Detta mångsidiga verktyg öppnar upp en värld av möjligheter för textextraktion i dina applikationer.

## FAQ's

### F1: Kan jag använda Aspose.OCR för .NET med någon typ av bild?

S1: Aspose.OCR stöder ett brett utbud av bildformat, vilket säkerställer flexibilitet i dina OCR-applikationer.

### F2: Hur exakt är OCR-igenkänningen?

A2: Aspose.OCR utnyttjar avancerade algoritmer för hög noggrannhet, vilket gör den lämplig för olika scenarier för textigenkänning.

### F3: Finns det en testversion tillgänglig?

 S3: Ja, du kan utforska funktionerna i Aspose.OCR för .NET med[gratis provperiod](https://releases.aspose.com/).

### F4: Var kan jag hitta omfattande dokumentation?

 A4: Se[dokumentation](https://reference.aspose.com/ocr/net/) för detaljerad information och användningsriktlinjer.

### F5: Behöver du hjälp eller har specifika frågor?

 A5: Besök[Aspose.OCR-forum](https://forum.aspose.com/c/ocr/16) för samhällsstöd och diskussioner.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
