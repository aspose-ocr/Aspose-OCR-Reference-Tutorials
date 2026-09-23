---
date: 2026-02-22
description: Lär dig hur du utför layoutanalys‑OCR genom att känna igen textrader
  i en bild och extrahera radrektanglar med Aspose.OCR för .NET.
linktitle: Layout Analysis OCR – Get Line Rectangles from Images
second_title: Aspose.OCR .NET API
title: Layoutanalys OCR – Hämta linjerektanglar från bilder
url: /sv/net/image-and-drawing-recognition/get-rectangles-for-lines/
weight: 10
---

.11 for .NET

**Author:** Aspose

Now ensure we keep all shortcodes at start and end.

Now produce final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Layoutanalys OCR – Hämta linjerektanglar från bilder

## Introduction

I den här handledningen kommer du att upptäcka **hur man får OCR-linjerektanglar** med Aspose.OCR för .NET. I slutet av guiden kommer du att kunna **igenkänna textrader i en bild** och **extrahera linjekoordinater** för varje upptäckt rad—perfekt för efterföljande bearbetning såsom **layoutanalys OCR**, dataextraktion eller anpassad rendering.

## Quick Answers
- **What does “get OCR line rectangles” mean?** Vad betyder “hämta OCR-linjerektanglar”? Den returnerar avgränsningsrutorna för varje textrad som upptäcks i en bild.  
- **Which API method is used?** Vilken API‑metod används? `AsposeOcr.GetRectangles(..., AreasType.LINES, ...)`.  
- **Do I need a license?** Behöver jag en licens? En gratis provversion fungerar för utveckling; en kommersiell licens krävs för produktion.  
- **Supported image formats?** Vilka bildformat stöds? PNG, JPEG, BMP, TIFF, and more.  
- **Can I run this on .NET Core?** Kan jag köra detta på .NET Core? Ja, Aspose.OCR fullt stödjer .NET Core och .NET 5/6.

## Prerequisites

Innan du dyker ner i handledningen, se till att du har följande förutsättningar på plats:

- Grundläggande kunskaper i C# och .NET‑utveckling.  
- En integrerad utvecklingsmiljö (IDE) såsom Visual Studio.  
- Aspose.OCR för .NET‑biblioteket installerat. Du kan ladda ner det [here](https://releases.aspose.com/ocr/net/).  
- En exempelbild som innehåller text för OCR‑igenkänning.

## Import Namespaces

Se till att du har de nödvändiga namnutrymmena importerade till ditt projekt. Lägg till följande rader högst upp i din C#‑fil:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

Nu ska vi bryta ner processen för att hämta rektanglar för rader i OCR‑bildigenkänning i enkla steg.

## layout analysis ocr – Step‑by‑Step Guide

### Step 1: Set Up Your Document Directory

```csharp
// ExStart:3
string dataDir = "Your Document Directory";
// ExEnd:3
```

Byt ut `"Your Document Directory"` mot den faktiska sökvägen till mappen som innehåller din exempelbild.

### Step 2: Initialize Aspose.OCR

```csharp
// ExStart:4
AsposeOcr api = new AsposeOcr();
// ExEnd:4
```

Skapa en instans av klassen `AsposeOcr` för att komma åt OCR‑funktionaliteten.

### Step 3: Specify Image Path

```csharp
// ExStart:5
string fullPath = dataDir + "sample.png";
// ExEnd:5
```

Definiera den fullständiga sökvägen till bilden du vill utföra OCR på.

### Step 4: Recognize Image and Get Rectangles

```csharp
// ExStart:6
List<Rectangle> lines = api.GetRectangles(fullPath, AreasType.LINES, false);
// ExEnd:6
```

Metoden `GetRectangles` returnerar en lista med `Rectangle`‑objekt, där varje objekt representerar koordinaterna för en upptäckt textrad. Detta är kärnan i **att hämta OCR‑linjerektanglar** och möjliggör **layoutanalys OCR**.

### Step 5: Print Result

```csharp
// ExStart:7
Console.WriteLine("Areas coordinates:");
lines.ForEach(a => Console.WriteLine($"x:{a.X} y:{a.Y} width:{a.Width} height:{a.Height}"));
// ExEnd:7
```

Skriv ut koordinaterna för de upptäckta områdena till konsolen. Du kommer att se värden som du senare kan använda för att **extrahera linjekoordinater** för anpassad bearbetning.

## Why Use Aspose.OCR for Line Rectangles?

- **High accuracy** – **Hög noggrannhet** – Avancerade algoritmer upptäcker rader även i brusiga eller skeva bilder.  
- **Cross‑platform** – **Cross‑platform** – Fungerar på .NET Framework, .NET Core och .NET 5/6.  
- **No external dependencies** – **Inga externa beroenden** – Ren .NET‑bibliotek, inga inhemska DLL‑filer att distribuera.  
- **Rich output** – **Rik output** – Förutom linjerektanglar kan du även hämta ord, tecken och förtroendescore.

## Common Issues and Solutions

| Problem | Lösning |
|-------|----------|
| **No rectangles returned** | **Inga rektanglar returnerade** – Se till att bilden innehåller tydlig, horisontell text och att `AreasType.LINES` är specificerat. |
| **Incorrect coordinates** | **Felaktiga koordinater** – Verifiera bildens DPI; lågupplösta bilder kan orsaka inexakta gränser. |
| **Performance bottleneck on large images** | **Prestandaflaskhals på stora bilder** – Ändra storlek på bilden till en rimlig upplösning innan du anropar `GetRectangles`. |
| **License exception** | **Licensundantag** – Använd en provlicens för testning; applicera en full licens för produktion för att undvika utvärderingsgränser. |

## Frequently Asked Questions

**Q: Can I extract individual words instead of whole lines?**  
A: Ja, använd `AreasType.WORDS` med samma `GetRectangles`‑metod för att få ordnivå‑avgränsningsrutor.

**Q: Does the API support multi‑page PDFs?**  
A: Konvertera varje PDF‑sida till en bild först, och anropa sedan `GetRectangles` på varje bild.

**Q: How do I handle rotated text?**  
A: Aktivera auto‑roteringsalternativet i OCR‑inställningarna eller förrotera bilden innan bearbetning.

**Q: Is there a way to get confidence scores for each line?**  
A: Efter att ha fått rektanglar, anropa `api.RecognizeImage(...).Lines` för att komma åt radobjekt som inkluderar förtroendevärden.

**Q: What .NET versions are compatible?**  
A: Biblioteket fungerar med .NET Framework 4.5+, .NET Core 3.1+ och .NET 5/6.

## Real‑World Use Cases

- **Document layout analysis OCR** – **Dokumentlayoutanalys OCR** – Mata in linjerektanglar i en layout‑motor för att rekonstruera kolumnstrukturer.  
- **Automated data extraction** – **Automatiserad dataextraktion** – Använd koordinaterna för att beskära enskilda rader för efterföljande NLP‑pipelines.  
- **Custom rendering** – **Anpassad rendering** – Överlagra avgränsningsrutor på originalbilden för visuell verifiering eller UI‑överlägg.  

## Conclusion

Grattis! Du har framgångsrikt **hämtat OCR‑linjerektanglar** för en bild med Aspose.OCR för .NET. Med avgränsningsrutorna i handen kan du nu mata in linjekoordinater i efterföljande arbetsflöden såsom anpassad rendering, dataextraktion eller **layoutanalys OCR**.

---

**Last Updated:** 2026-02-22  
**Tested With:** Aspose.OCR 24.11 for .NET  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}