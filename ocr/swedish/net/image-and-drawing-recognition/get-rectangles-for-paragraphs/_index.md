---
date: 2025-12-17
description: Lär dig hur du extraherar rektanglar för stycken i OCR‑bilder med Aspose.OCR
  för .NET – den ultimata guiden för hur du extraherar rektanglar och hämtar styckekoordinater.
linktitle: Get Rectangles for Paragraphs in OCR Image Recognition
second_title: Aspose.OCR .NET API
title: Hur man extraherar rektanglar för stycken i OCR‑bildigenkänning
url: /sv/net/image-and-drawing-recognition/get-rectangles-for-paragraphs/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man extraherar rektanglar för stycken i OCR‑bildigenkänning

## Introduktion

Välkommen till vår omfattande guide om **hur man extraherar rektanglar** för stycken i OCR‑bildigenkänning med Aspose.OCR för .NET. Om du vill förbättra din dokument‑bearbetningspipeline, hämta styckesgränser och automatisera datautvinning, är du på rätt plats. Vi går igenom varje steg – från att konfigurera miljön till att skriva ut rektangelkoordinaterna – så att du kan börja använda OCR‑resultaten omedelbart.

## Snabba svar
- **Vad betyder “extrahera rektanglar”?** Det returnerar begränsningsrutorna (x, y, bredd, höjd) för upptäckta textområden.  
- **Vilken API‑metod tillhandahåller rektanglarna?** `AsposeOcr.GetRectangles` med `AreasType.PARAGRAPHS`.  
- **Behöver jag en licens för utveckling?** En gratis provversion fungerar för testning; en kommersiell licens krävs för produktion.  
- **Kan jag bearbeta flera bilder samtidigt?** Ja – loopa över din bildlista och anropa `GetRectangles` för varje fil.  
- **Vilka format stöds?** PNG, JPEG, TIFF, BMP och många fler.

## Vad betyder “hur man extraherar rektanglar” i OCR?
I OCR‑terminologi innebär att extrahera rektanglar att identifiera de geometriska gränser som omsluter varje stycke eller rad text i en bild. Dessa koordinater låter dig markera, beskära eller vidare analysera specifika sektioner av ett skannat dokument.

## Varför extrahera styckekoordinater?
- **Precise post‑processing** – du kan skicka varje rektangel till efterföljande arbetsflöden (t.ex. översättning, maskering).  
- **Improved UI/UX** – överlagra begränsningsrutor på originalbilden för att visa användarna var texten hittades.  
- **Batch automation** – snabbt lokalisera och isolera stycken i stora dokumentuppsättningar.

## Förutsättningar

- Grundläggande kunskap i C# och .NET‑utveckling.  
- En utvecklingsmiljö med Aspose.OCR för .NET installerad – du kan ladda ner den [here](https://releases.aspose.com/ocr/net/).  
- Bekantskap med bildbehandlingskoncept och varför OCR är avgörande för att extrahera text från skannade filer.

## Importera namnrymder

I din C#‑fil, importera de nödvändiga namnrymderna så att OCR‑klasserna är tillgängliga:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Steg 1: Ställ in din dokumentkatalog

Definiera mappen som innehåller de bilder du vill analysera:

```csharp
string dataDir = "Your Document Directory";
```

## Steg 2: Initiera AsposeOcr‑instans

Skapa ett `AsposeOcr`‑objekt – detta ger dig åtkomst till alla OCR‑funktioner:

```csharp
AsposeOcr api = new AsposeOcr();
```

## Steg 3: Ange bildens sökväg

Peka på den exakta bildfilen du vill bearbeta:

```csharp
string fullPath = dataDir + "sample.png";
```

## Steg 4: Känn igen bilden och hämta styckerektanglar

Anropa `GetRectangles`‑metoden. Att sätta `detect_areas` till `true` instruerar motorn att returnera **stycke**‑rektanglar:

```csharp
List<Rectangle> rectangles = api.GetRectangles(fullPath, AreasType.PARAGRAPHS, true);
```

## Steg 5: Skriv ut resultat

Skriv ut koordinaterna så att du kan se de **extraherade styckekoordinaterna** som upptäcktes:

```csharp
Console.WriteLine("Areas coordinates:");
rectangles.ForEach(a => Console.WriteLine($"x:{a.X} y:{a.Y} width:{a.Width} height:{a.Height}"));
```

## Vanliga problem och lösningar

| Problem | Orsak | Lösning |
|-------|--------|-----|
| Inga rektanglar returnerades | Bildkvaliteten är för låg eller fel `AreasType` | Se till att bilden är tydlig och använd `AreasType.PARAGRAPHS`. |
| Koordinaterna är fel med ett steg | DPI‑skalan matchar inte | Ställ in korrekt DPI när du laddar bilden eller använd `api.Config.Dpi`. |
| Licensundantag | Kör utan en giltig licens i produktion | Applicera en tillfällig eller permanent licens via `api.SetLicense`. |

## Vanliga frågor

**Q: Är Aspose.OCR kompatibel med olika bildformat?**  
A: Ja, Aspose.OCR stödjer PNG, JPEG, TIFF, BMP och många andra vanliga format.

**Q: Kan jag använda Aspose.OCR för batch‑bearbetning av flera bilder?**  
A: Absolut! Loop igenom en samling av filsökvägar och anropa `GetRectangles` för varje bild.

**Q: Finns det en gratis provversion av Aspose.OCR för .NET?**  
A: Ja, du kan utforska en gratis provversion [here](https://releases.aspose.com/).

**Q: Hur kan jag skaffa en tillfällig licens för Aspose.OCR?**  
A: Du kan erhålla en tillfällig licens [here](https://purchase.aspose.com/temporary-license/).

**Q: Var kan jag hitta ytterligare support och diskussioner relaterade till Aspose.OCR?**  
A: Gå till [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16) för community‑support och diskussioner.

## Slutsats

I den här handledningen har vi visat **hur man extraherar rektanglar** för stycken med Aspose.OCR för .NET, gått igenom varje kodexempel och förklarat hur man tolkar de returnerade koordinaterna. Genom att integrera dessa steg i din applikation kan du på ett pålitligt sätt hämta styckesgränser, förbättra dokumentarbetsflöden och bygga smartare OCR‑drivna lösningar.

---

**Senast uppdaterad:** 2025-12-17  
**Testad med:** Aspose.OCR 24.11 för .NET  
**Författare:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}