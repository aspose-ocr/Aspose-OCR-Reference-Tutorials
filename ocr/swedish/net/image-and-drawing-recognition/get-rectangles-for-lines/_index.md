---
date: 2025-12-17
description: Lär dig hur du får OCR‑radrektanglar med Aspose.OCR för .NET för att
  känna igen textrader i bilder och enkelt extrahera radkoordinater.
linktitle: Get OCR Line Rectangles for Image Text Lines
second_title: Aspose.OCR .NET API
title: Hämta OCR‑linjerektanglar för bildtextlinjer
url: /sv/net/image-and-drawing-recognition/get-rectangles-for-lines/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hämta OCR‑radrektanglar för bildtextlinjer

## Introduktion

I den här handledningen kommer du att upptäcka **hur du får OCR‑radrektanglar** med Aspose.OCR för .NET. I slutet av guiden kommer du att kunna **identifiera textlinjer i en bild** och **extrahera radkoordinater** för varje upptäckt rad — perfekt för efterföljande bearbetning såsom layoutanalys, dataextraktion eller anpassad rendering.

## Snabba svar
- **Vad betyder “get OCR line rectangles”?** Det returnerar omgivningsrutorna för varje textlinje som upptäcks i en bild.  
- **Vilken API‑metod används?** `AsposeOcr.GetRectangles(..., AreasType.LINES, ...)`.  
- **Behöver jag en licens?** En gratis provversion fungerar för utveckling; en kommersiell licens krävs för produktion.  
- **Vilka bildformat stöds?** PNG, JPEG, BMP, TIFF och fler.  
- **Kan jag köra detta på .NET Core?** Ja, Aspose.OCR stödjer fullt ut .NET Core och .NET 5/6.

## Förutsättningar

Innan du dyker ner i handledningen, se till att du har följande förutsättningar på plats:

- Grundläggande kunskap om C# och .NET‑utveckling.  
- En integrerad utvecklingsmiljö (IDE) såsom Visual Studio.  
- Aspose.OCR för .NET‑biblioteket installerat. Du kan ladda ner det [här](https://releases.aspose.com/ocr/net/).  
- En exempelbild som innehåller text för OCR‑igenkänning.

## Importera namnrymder

Se till att du har de nödvändiga namnrymderna importerade till ditt projekt. Lägg till följande rader högst upp i din C#‑fil:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

Nu ska vi gå igenom processen för att hämta rektanglar för rader i OCR‑bildigenkänning i enkla steg.

## Steg 1: Ställ in din dokumentkatalog

```csharp
// ExStart:3
string dataDir = "Your Document Directory";
// ExEnd:3
```

Byt ut `"Your Document Directory"` mot den faktiska sökvägen till mappen som innehåller din exempelbild.

## Steg 2: Initiera Aspose.OCR

```csharp
// ExStart:4
AsposeOcr api = new AsposeOcr();
// ExEnd:4
```

Skapa en instans av klassen `AsposeOcr` för att komma åt OCR‑funktionaliteten.

## Steg 3: Ange bildsökväg

```csharp
// ExStart:5
string fullPath = dataDir + "sample.png";
// ExEnd:5
```

Definiera den fullständiga sökvägen till bilden du vill köra OCR på.

## Steg 4: Känn igen bild och hämta rektanglar

```csharp
// ExStart:6
List<Rectangle> lines = api.GetRectangles(fullPath, AreasType.LINES, false);
// ExEnd:6
```

`GetRectangles`‑metoden returnerar en lista med `Rectangle`‑objekt, där varje objekt representerar koordinaterna för en upptäckt textlinje. Detta är kärnan i **att hämta OCR‑radrektanglar**.

## Steg 5: Skriv ut resultatet

```csharp
// ExStart:7
Console.WriteLine("Areas coordinates:");
lines.ForEach(a => Console.WriteLine($"x:{a.X} y:{a.Y} width:{a.Width} height:{a.Height}"));
// ExEnd:7
```

Skriv ut koordinaterna för de upptäckta områdena till konsolen. Du kommer att se värden som du senare kan använda för att **extrahera radkoordinater** för anpassad bearbetning.

## Varför använda Aspose.OCR för radrektanglar?

- **Hög noggrannhet** – Avancerade algoritmer upptäcker rader även i brusiga eller snedvridna bilder.  
- **Plattformsoberoende** – Fungerar på .NET Framework, .NET Core och .NET 5/6.  
- **Inga externa beroenden** – Ren .NET‑bibliotek, inga inhemska DLL‑filer att distribuera.  
- **Rikligt resultat** – Förutom radrektanglar kan du också hämta ord, tecken och förtroendescore.

## Vanliga problem och lösningar

| Problem | Lösning |
|-------|----------|
| **Inga rektanglar returnerades** | Se till att bilden innehåller tydlig, horisontell text och att `AreasType.LINES` är specificerat. |
| **Felaktiga koordinater** | Verifiera bildens DPI; lågupplösta bilder kan orsaka inexakta gränser. |
| **Prestandaflaskhals på stora bilder** | Ändra storleken på bilden till en rimlig upplösning innan du anropar `GetRectangles`. |
| **Licensundantag** | Använd en provlicens för testning; tillämpa en full licens för produktion för att undvika utvärderingsgränser. |

## Vanliga frågor

**Q: Kan jag extrahera enskilda ord istället för hela rader?**  
A: Ja, använd `AreasType.WORDS` med samma `GetRectangles`‑metod för att få ordnivå‑omgivningsrutor.

**Q: Stöder API:et flersidiga PDF‑filer?**  
A: Konvertera varje PDF‑sida till en bild först, och anropa sedan `GetRectangles` på varje bild.

**Q: Hur hanterar jag roterad text?**  
A: Aktivera auto‑roteringsalternativet i OCR‑inställningarna eller förrotera bilden innan bearbetning.

**Q: Finns det ett sätt att få förtroendescore för varje rad?**  
A: Efter att ha fått rektanglar, anropa `api.RecognizeImage(...).Lines` för att komma åt radobjekt som inkluderar förtroendevärden.

**Q: Vilka .NET‑versioner är kompatibla?**  
A: Biblioteket fungerar med .NET Framework 4.5+, .NET Core 3.1+, och .NET 5/6.

## Slutsats

Grattis! Du har framgångsrikt **hämtat OCR‑radrektanglar** för en bild med Aspose.OCR för .NET. Med omgivningsrutorna i handen kan du nu mata radkoaterna in i efterföljande arbetsflöden såsom anpassad rendering, dataextraktion eller layoutanalys.

---

**Senast uppdaterad:** 2025-12-17  
**Testad med:** Aspose.OCR 24.11 för .NET  
**Författare:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}