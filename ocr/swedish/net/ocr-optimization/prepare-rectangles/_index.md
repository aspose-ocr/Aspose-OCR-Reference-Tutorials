---
date: 2025-12-22
description: Lär dig hur du extraherar text från en bild med Aspose.OCR för .NET.
  Den här guiden visar dig hur du förbereder rektanglar för OCR‑bildigenkänning och
  förbättrar noggrannheten.
linktitle: Prepare Rectangles in OCR Image Recognition
second_title: Aspose.OCR .NET API
title: Hur man extraherar text från bild genom att förbereda rektanglar i OCR
url: /sv/net/ocr-optimization/prepare-rectangles/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Förbered rektanglar i OCR-bildigenkänning

## Introduktion

Optisk teckenigenkänning (OCR) är avgörande för att konvertera visuellt innehåll till sökbar, redigerbar text. I den här handledningen kommer du att **extrahera text från bild** genom att förbereda anpassade rektanglar som fokuserar OCR-motorn på specifika områden. Med Aspose.OCR för .NET går vi igenom varje steg—från att konfigurera ditt projekt till att hämta den igenkända texten—så att du kan integrera kraftfull bild‑till‑text‑funktionalitet i dina .NET‑applikationer.

## Snabba svar
- **Vad betyder “extrahera text från bild”?** Det betyder att konvertera de visuella tecknen i en bild till maskinläsbara strängar.  
- **Vilket bibliotek hjälper med detta i .NET?** Aspose.OCR för .NET.  
- **Behöver jag en licens för utveckling?** En gratis provversion fungerar för testning; en licens krävs för produktion.  
- **Kan jag rikta in mig på specifika områden?** Ja, genom att definiera rektanglar som begränsar OCR‑omfånget.  
- **Vilka .NET‑versioner stöds?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.

## Vad är “extrahera text från bild” med rektanglar?
När du definierar rektangulära zoner på en bild bearbetar OCR‑motorn endast dessa zoner. Detta förbättrar noggrannheten, minskar bearbetningstiden och låter dig ignorera brusiga bakgrunder eller irrelevanta sektioner.

## Varför förbereda rektanglar före OCR?
- **Fokusera på relevant innehåll:** Hoppa över rubriker, sidfötter eller dekorativa grafik.  
- **Öka prestanda:** Mindre regioner betyder snabbare igenkänning.  
- **Förbättra noggrannhet:** Mindre visuellt brus ger renare resultat.

## Förutsättningar

- Bekantskap med C# och .NET‑utveckling.  
- Aspose.OCR för .NET‑biblioteket installerat – du kan ladda ner det **[här](https://releases.aspose.com/ocr/net/)**.  
- En exempelbild (t.ex. `sample.png`) som innehåller den text du vill extrahera.

## Importera namnrymder

Först, importera de nödvändiga namnrymderna:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Steg 1: Ställ in din dokumentkatalog

Ange var dina bildfiler finns och skapa en instans av OCR‑motorn.

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Hur man extraherar text från bild med flera rektanglar

### Steg 2: Känn igen bild med flera rektanglar

#### 2.1 Definiera rektanglarna

Skapa en lista med `Rectangle`‑objekt som markerar de områden du vill att OCR‑motorn ska skanna.

```csharp
List<Rectangle> rects = new List<Rectangle>()
{
    new Rectangle(138, 352, 2033, 537),
    new Rectangle(147, 890, 2033, 1157),
    new Rectangle(923, 2045, 465, 102),
    new Rectangle(104, 2147, 2076, 819)
};
```

#### 2.2 Utför OCR‑igenkänning

Skicka bildens sökväg och rektangel‑listan till `RecognizeImage`. Metoden returnerar en samling strängar—varje post motsvarar en rektangel.

```csharp
// first case
List<string> listResult = api.RecognizeImage(dataDir + "sample.png", rects);

// Display the recognized text
foreach (string s in listResult)
{
    Console.WriteLine(s);
}
```

### Steg 3: Känn igen bild med Recognition Settings (alternativ metod)

Om du föredrar att använda `RecognitionSettings` kan du uppnå samma resultat med ett något annorlunda API‑anrop.

#### 3.1 Definiera igenkänningsinställningar

```csharp
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings
{
    RecognitionAreas = rects
});
```

#### 3.2 Visa igenkänd text

```csharp
// Display the recognized text
foreach (string s in result.RecognitionAreasText)
{
    Console.WriteLine(s);
}
```

## Vanliga problem & tips

- **Felaktiga rektangelkoordinater:** Se till att värdena `X`, `Y`, `Width` och `Height` korrekt motsvarar den region du vill ha.  
- **Bildkvalitet:** Lågrelösningsbilder kan ge dåliga OCR‑resultat; överväg förbehandling (t.ex. binarisering).  
- **Tomma resultat:** Verifiera att rektanglarna faktiskt innehåller text; annars returnerar motorn tomma strängar.

## Slutsats

Du har nu lärt dig hur du **extraherar text från bild** genom att förbereda anpassade rektanglar med Aspose.OCR för .NET. Denna teknik ger dig fin‑granulär kontroll över OCR‑bearbetning, vilket hjälper dig att bygga snabbare, mer exakta text‑extraktionsfunktioner i dina applikationer.

## Vanliga frågor

**Q:** Kan jag använda Aspose.OCR för .NET med andra .NET‑ramverk?  
**A:** Ja, Aspose.OCR för .NET är kompatibel med olika .NET‑ramverk.

**Q:** Finns det en gratis provversion tillgänglig för Aspose.OCR för .NET?  
**A:** Absolut! Du kan komma åt den gratis provversionen **[här](https://releases.aspose.com/)**.

**Q:** Hur får jag support för Aspose.OCR för .NET?  
**A:** Besök **[Aspose.OCR forum](https://forum.aspose.com/c/ocr/16)** för dedikerad support.

**Q:** Kan jag få en tillfällig licens för teständamål?  
**A:** Ja, du kan skaffa en tillfällig licens **[här](https://purchase.aspose.com/temporary-license/)**.

**Q:** Var kan jag hitta dokumentationen för Aspose.OCR för .NET?  
**A:** Dokumentationen finns **[här](https://reference.aspose.com/ocr/net/)**.

---

**Senast uppdaterad:** 2025-12-22  
**Testat med:** Aspose.OCR 24.11 för .NET  
**Författare:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}