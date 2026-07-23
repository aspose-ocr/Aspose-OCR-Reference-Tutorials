---
date: 2026-07-23
description: Lär dig hur du extraherar text från bild med Aspose.OCR för .NET, förbereder
  rektanglar för att förbättra OCR‑noggrannheten och konverterar bild till text effektivt.
keywords:
- extract text from image
- convert image to text
- improve ocr accuracy
lastmod: 2026-07-23
linktitle: Förbered rektanglar i OCR‑bildigenkänning
og_description: Extrahera text från bild med Aspose.OCR för .NET. Lär dig att förbereda
  rektanglar, öka OCR‑noggrannheten och konvertera bild till text effektivt.
og_image_alt: Guide to extract text from image using rectangles with Aspose.OCR for
  .NET
og_title: Extrahera text från bild med rektanglar – OCR‑guide
schemas:
- author: Aspose
  dateModified: '2026-07-23'
  description: Learn how to extract text from image using Aspose.OCR for .NET, preparing
    rectangles to improve OCR accuracy and convert image to text efficiently.
  headline: Extract Text from Image with Rectangles – OCR Guide
  type: TechArticle
- questions:
  - answer: It converts visual characters in a picture into machine‑readable strings.
    question: What does “extract text from image” mean?
  - answer: Aspose.OCR for .NET provides a full‑featured OCR engine.
    question: Which library handles this in .NET?
  - answer: A free trial works for development; a commercial license is required for
      deployment.
    question: Do I need a license for production?
  - answer: Yes—define rectangles to target only the areas that contain useful text.
    question: Can I limit OCR to specific zones?
  - answer: .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.
    question: What .NET versions are supported?
  type: FAQPage
second_title: Aspose.OCR .NET API
tags:
- ocr
- Aspire.OCR
- .NET image processing
- extract text from image
title: Extrahera text från bild med rektanglar – OCR‑guide
url: /sv/net/ocr-optimization/prepare-rectangles/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahera text från bild med rektanglar – OCR-guide

## Introduktion

Optisk teckenigenkänning (OCR) låter dig **extrahera text från bild**‑filer så att de blir sökbara och redigerbara. I den här handledningen visar vi hur du förbättrar OCR‑noggrannheten genom att förbereda anpassade rektanglar som fokuserar motorn på exakt de zoner du behöver. Med Aspose.OCR för .NET ser du hela arbetsflödet—från projektuppsättning till att hämta de igenkända strängarna—så att du kan integrera pålitlig bild‑till‑text‑konvertering i vilken .NET‑applikation som helst.

## Snabba svar
- **Vad betyder “extrahera text från bild”?** Den konverterar visuella tecken i en bild till maskinläsbara strängar.  
- **Vilket bibliotek hanterar detta i .NET?** Aspose.OCR för .NET tillhandahåller en fullutrustad OCR‑motor.  
- **Behöver jag en licens för produktion?** En gratis provversion fungerar för utveckling; en kommersiell licens krävs för distribution.  
- **Kan jag begränsa OCR till specifika zoner?** Ja—definiera rektanglar för att rikta in dig på endast de områden som innehåller användbar text.  
- **Vilka .NET‑versioner stöds?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.

## Vad är “extrahera text från bild” med rektanglar?
`extract text from image`‑processen läser tecken inom definierade rektangulära zoner och ignorerar allt annat. Genom att begränsa OCR till dessa zoner får du högre noggrannhet, snabbare bearbetning och mindre efterbearbetning. Detta tillvägagångssätt isolerar den text du är intresserad av samtidigt som bakgrundsgrafik, dekorativa element och annat visuellt brus som kan förvirra OCR‑motorn tas bort.

## Varför förbereda rektanglar före OCR?
Att förbereda rektanglar låter dig koncentrera OCR‑motorn på de mest relevanta delarna av en bild, vilket förbättrar både hastighet och precision. Genom att begränsa analysområdet minskar du mängden data som motorn måste granska, vilket leder till snabbare resultat och färre felaktiga igenkänningar orsakade av onödigt visuellt brus.

- **Fokusera på relevant innehåll:** Hoppa över rubriker, sidfötter eller dekorativ grafik som kan förvirra motorn.  
- **Öka prestanda:** Mindre regioner kräver färre beräkningar, vilket minskar körtiden med upp till 40 % på stora skanningar.  
- **Förbättra noggrannhet:** Genom att minska visuellt brus ökar teckenigenkänningsgraden från ~85 % till >95 % på brusiga dokument.

## Varför detta är viktigt för verkliga projekt
Många affärsdokument—kvitton, fakturor, ID‑kort—blandar text med logotyper eller streckkoder. Genom att rita rektanglar runt de fält du faktiskt behöver, extraherar du endast den värdefulla datan, minskar efterföljande rengöringsarbete och ökar tillförlitligheten i automatiserade arbetsflöden. Denna målmedvetna extraktion minskar efterbearbetningsinsatsen och hjälper till att upprätthålla efterlevnad av databehandlingsstandarder.

## Vanliga användningsfall
- **Automatisering av datainmatning:** Hämta specifika fält från skannade formulär eller utgiftskvitton.  
- **Efterlevnadskontroller:** Isolera juridiska klausuler eller regulatoriska uttalanden för verifiering.  
- **Innehållsindexering:** Indexera endast rubriken eller bildtexten på en bild för sökmotorsynlighet.

## Förutsättningar

- Grundläggande kunskap i C# och .NET‑utveckling.  
- Aspose.OCR för .NET‑biblioteket installerat – ladda ner det **[här](https://releases.aspose.com/ocr/net/)** eller bläddra bland alla versioner **[här](https://releases.aspose.com/)**.  
- En exempelbild (t.ex. `sample.png`) som innehåller den text du vill extrahera.

## Importera namnrymder

`using`‑satserna importerar OCR‑motorn och geometriklasserna till räckvidd.

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Steg 1: Ställ in din dokumentkatalog

Ange mappen som innehåller dina bilder och skapa en instans av OCR‑motorn.

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Hur man extraherar text från bild med flera rektanglar
Läs in bilden en gång, och skicka sedan en lista med rektanglar till OCR‑motorn. Varje rektangel definierar ett intresseområde, och motorn returnerar en separat sträng för varje område, vilket låter dig hantera fält individuellt och kombinera resultat efter behov.

### Definiera rektanglarna

`Rectangle`‑objekt beskriver X‑Y‑koordinaterna och storleken på varje zon du vill skanna.  

```csharp
List<Rectangle> rects = new List<Rectangle>()
{
    new Rectangle(138, 352, 2033, 537),
    new Rectangle(147, 890, 2033, 1157),
    new Rectangle(923, 2045, 465, 102),
    new Rectangle(104, 2147, 2076, 819)
};
```

### Utför OCR‑igenkänning

`RecognizeImage`‑metoden bearbetar bilden med den medföljande rektangel‑listan och returnerar igenkänd text för varje region.  

```csharp
// first case
List<string> listResult = api.RecognizeImage(dataDir + "sample.png", rects);

// Display the recognized text
foreach (string s in listResult)
{
    Console.WriteLine(s);
}
```

## Hur man extraherar text från bild med RecognitionSettings (alternativ metod)
Om du föredrar ett inställningsbaserat anrop kan du uppnå samma resultat med `RecognitionSettings`. Detta objekt låter dig samla rektangeldefinitioner tillsammans med språk, DPI och andra OCR‑alternativ, vilket ger ett rent API‑anrop med en enda parameter.

### Definiera igenkänningsinställningar

`RecognitionSettings` låter dig samla rektangel‑listan och ytterligare alternativ (t.ex. språk, DPI) i ett enda objekt.  

```csharp
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings
{
    RecognitionAreas = rects
});
```

### Visa igenkänd text

Iterera över de returnerade strängarna och skriv ut varje regions text.  

```csharp
// Display the recognized text
foreach (string s in result.RecognitionAreasText)
{
    Console.WriteLine(s);
}
```

## Vanliga problem & tips

- **Felaktiga rektangelkoordinater:** Verifiera att `X`, `Y`, `Width` och `Height` motsvarar det avsedda området.  
- **Bildkvalitet:** Låg upplösning eller kraftigt komprimerade bilder försämrar OCR‑resultaten; överväg förbehandling såsom binarisering.  
- **Tomma resultat:** Se till att rektanglarna faktiskt innehåller läsbar text; annars returnerar motorn tomma strängar.

## Felsökning och bästa praxis

| Symtom | Trolig orsak | Åtgärd |
|--------|--------------|--------|
| Ingen output eller tomma strängar | Rektanglar utanför bildens gränser | Dubbelkolla bildens dimensioner och rektangelkoordinater |
| Förvrängda tecken | Dålig kontrast eller brus | Applicera gråskalakonvertering och tröskelvärde före OCR |
| Långsam prestanda på stora filer | För många rektanglar eller mycket stor bild | Dela upp bilden eller minska antalet rektanglar där det är möjligt |

## Slutsats

Du vet nu hur du **extraherar text från bild** genom att förbereda anpassade rektanglar med Aspose.OCR för .NET. Detta tillvägagångssätt ger dig exakt kontroll över OCR‑bearbetning och levererar snabbare, mer exakta text‑extraktionsfunktioner för vilken .NET‑lösning som helst.

## Vanliga frågor

**Q:** Kan jag använda Aspose.OCR för .NET med andra .NET‑ramverk?  
**A:** Ja, Aspose.OCR för .NET fungerar med .NET Framework 4.5+, .NET Core 3.1+, och .NET 5/6/7.

**Q:** Finns det en gratis provversion tillgänglig?  
**A:** Absolut! Ladda ner provversionen **[här](https://releases.aspose.com/)**.

**Q:** Var kan jag få support för Aspose.OCR för .NET?  
**A:** Besök **[Aspose.OCR‑forumet](https://forum.aspose.com/c/ocr/16)** för dedikerad hjälp.

**Q:** Kan jag få en tillfällig licens för testning?  
**A:** Ja, en tillfällig licens finns tillgänglig **[här](https://purchase.aspose.com/temporary-license/)**.

**Q:** Var finns den officiella dokumentationen?  
**A:** Den fullständiga API‑referensen finns **[här](https://reference.aspose.com/ocr/net/)**.

---

**Senast uppdaterad:** 2026-07-23  
**Testad med:** Aspose.OCR 24.11 for .NET  
**Författare:** Aspose  

{{< blocks/products/products-backtop-button >}}

## Relaterade handledningar

- [Hur man extraherar rektanglar för stycken i OCR‑bildigenkänning](/ocr/net/image-and-drawing-recognition/get-rectangles-for-paragraphs/)
- [Hur man OCR‑bild – Utför OCR på bild i OCR‑bildigenkänning](/ocr/net/image-and-drawing-recognition/perform-ocr-on-image/)
- [Hur man extraherar text från bild med Aspose.OCR för .NET](/ocr/net/text-recognition/get-recognition-result/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}