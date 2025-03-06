---
title: Få rektanglar för stycken i OCR-bildigenkänning
linktitle: Få rektanglar för stycken i OCR-bildigenkänning
second_title: Aspose.OCR .NET API
description: Lås upp avancerade OCR-funktioner med Aspose.OCR för .NET. Extrahera styckerektanglar utan ansträngning.
weight: 11
url: /sv/net/image-and-drawing-recognition/get-rectangles-for-paragraphs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Få rektanglar för stycken i OCR-bildigenkänning

## Introduktion

Välkommen till vår omfattande guide om hur du använder Aspose.OCR för .NET för att extrahera styckerektanglar i OCR-bildigenkänning. Om du vill förbättra dina dokumentbearbetningsmöjligheter och utnyttja kraften i Optical Character Recognition (OCR) i dina .NET-applikationer, är du på rätt plats.

## Förutsättningar

Innan vi dyker in i handledningen, se till att du har följande förutsättningar på plats:

- Grundläggande kunskap om C# och .NET utveckling.
-  En utvecklingsmiljö inrättad med Aspose.OCR för .NET. Om du inte redan har gjort det kan du ladda ner den[här](https://releases.aspose.com/ocr/net/).
- En förståelse för bildbehandlingskoncept och betydelsen av OCR för att extrahera text från bilder.

## Importera namnområden

Se till att du har importerat de nödvändiga namnrymden i din C#-kod för att kunna använda Aspose.OCR effektivt. Inkludera följande överst i filen:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Steg 1: Konfigurera din dokumentkatalog

Börja med att initiera sökvägen till din dokumentkatalog där bilderna för OCR-bearbetning lagras:

```csharp
string dataDir = "Your Document Directory";
```

## Steg 2: Initiera AsposeOcr-instansen

Skapa en instans av klassen AsposeOcr för att få tillgång till OCR-funktioner:

```csharp
AsposeOcr api = new AsposeOcr();
```

## Steg 3: Ange bildsökvägen

Definiera hela sökvägen till bilden du vill bearbeta:

```csharp
string fullPath = dataDir + "sample.png";
```

## Steg 4: Känn igen bild och få styckerektanglar

 Åberopa`GetRectangles` metod för att få rektanglar för stycken i OCR-bilden. Uppsättning`detect_areas` till`true` om du vill extrahera stycken:

```csharp
List<Rectangle> rectangles = api.GetRectangles(fullPath, AreasType.PARAGRAPHS, true);
```

## Steg 5: Skriv ut resultat

Skriv ut koordinaterna för de identifierade områdena:

```csharp
Console.WriteLine("Areas coordinates:");
rectangles.ForEach(a => Console.WriteLine($"x:{a.X} y:{a.Y} width:{a.Width} height:{a.Height}"));
```

## Steg 6: Slutsats

Grattis! Du har framgångsrikt utfört OCR-bildigenkänningsprocessen för att få rektanglar för stycken med Aspose.OCR för .NET.

## Slutsats

I den här handledningen har vi utforskat de grundläggande stegen för att integrera Aspose.OCR för .NET i dina applikationer, så att du kan extrahera styckerektanglar från OCR-behandlade bilder. Aspose.OCR förenklar implementeringen av OCR, vilket gör det till ett värdefullt verktyg för dokumentbearbetning och textextraktion.

## FAQ's

### F1: Är Aspose.OCR kompatibel med olika bildformat?

S1: Ja, Aspose.OCR stöder olika bildformat, inklusive PNG, JPEG och TIFF.

### F2: Kan jag använda Aspose.OCR för batchbehandling av flera bilder?

A2: Absolut! Aspose.OCR underlättar batchbehandling för att hantera flera bilder sömlöst.

### F3: Finns det en gratis testversion tillgänglig för Aspose.OCR för .NET?

 A3: Ja, du kan utforska en gratis provperiod[här](https://releases.aspose.com/).

### F4: Hur kan jag få en tillfällig licens för Aspose.OCR?

 S4: Du kan skaffa en tillfällig licens[här](https://purchase.aspose.com/temporary-license/).

### F5: Var kan jag hitta ytterligare stöd och diskussioner relaterade till Aspose.OCR?

 A5: Gå över till[Aspose.OCR-forum](https://forum.aspose.com/c/ocr/16) för samhällsstöd och diskussioner.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
