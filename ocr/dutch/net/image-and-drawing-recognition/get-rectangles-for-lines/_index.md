---
date: 2025-12-17
description: Leer hoe u OCR‑lijnrechthoeken kunt verkrijgen met Aspose.OCR voor .NET
  om tekstregels in afbeeldingen te herkennen en eenvoudig lijncoördinaten te extraheren.
linktitle: Get OCR Line Rectangles for Image Text Lines
second_title: Aspose.OCR .NET API
title: Verkrijg OCR‑lijnrechthoeken voor tekstregels in afbeelding
url: /nl/net/image-and-drawing-recognition/get-rectangles-for-lines/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR‑lijnrechthoeken ophalen voor afbeeldings‑tekstregels

## Introductie

In deze tutorial ontdek je **hoe je OCR‑lijnrechthoeken** kunt verkrijgen met Aspose.OCR voor .NET. Aan het einde van de gids kun je **tekstregels in een afbeelding** herkennen en **lijncoördinaten** extraheren voor elke gedetecteerde regel — perfect voor downstream verwerking zoals lay‑outanalyse, gegevensextractie of aangepaste weergave.

## Snelle antwoorden
- **Wat betekent “get OCR line rectangles”?** Het retourneert de begrenzingskaders van elke tekstregel die in een afbeelding wordt gedetecteerd.  
- **Welke API‑methode wordt gebruikt?** `AsposeOcr.GetRectangles(..., AreasType.LINES, ...)`.  
- **Heb ik een licentie nodig?** Een gratis proefversie werkt voor ontwikkeling; een commerciële licentie is vereist voor productie.  
- **Ondersteunde afbeeldingsformaten?** PNG, JPEG, BMP, TIFF en meer.  
- **Kan ik dit uitvoeren op .NET Core?** Ja, Aspose.OCR ondersteunt volledig .NET Core en .NET 5/6.

## Voorvereisten

Voordat je aan de tutorial begint, zorg ervoor dat je de volgende voorvereisten hebt:

- Basiskennis van C# en .NET‑ontwikkeling.  
- Een geïntegreerde ontwikkelomgeving (IDE) zoals Visual Studio.  
- Aspose.OCR voor .NET bibliotheek geïnstalleerd. Je kunt het downloaden [hier](https://releases.aspose.com/ocr/net/).  
- Een voorbeeldafbeelding met tekst voor OCR‑herkenning.

## Namespaces importeren

Zorg ervoor dat je de benodigde namespaces in je project importeert. Voeg de volgende regels toe aan de bovenkant van je C#‑bestand:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

Now, let's break down the process of getting rectangles for lines in OCR image recognition into easy‑to‑follow steps.

## Stap 1: Stel uw documentmap in

```csharp
// ExStart:3
string dataDir = "Your Document Directory";
// ExEnd:3
```

Vervang `"Your Document Directory"` door het daadwerkelijke pad naar de map die je voorbeeldafbeelding bevat.

## Stap 2: Initialiseert Aspose.OCR

```csharp
// ExStart:4
AsposeOcr api = new AsposeOcr();
// ExEnd:4
```

Maak een instantie van de `AsposeOcr`‑klasse om toegang te krijgen tot de OCR‑functionaliteit.

## Stap 3: Specificeer afbeeldingspad

```csharp
// ExStart:5
string fullPath = dataDir + "sample.png";
// ExEnd:5
```

Definieer het volledige pad naar de afbeelding waarop je OCR wilt uitvoeren.

## Stap 4: Herken afbeelding en verkrijg rechthoeken

```csharp
// ExStart:6
List<Rectangle> lines = api.GetRectangles(fullPath, AreasType.LINES, false);
// ExEnd:6
```

De `GetRectangles`‑methode retourneert een lijst van `Rectangle`‑objecten, elk representerend de coördinaten van een gedetecteerde tekstregel. Dit is de kern van **het verkrijgen van OCR‑lijnrechthoeken**.

## Stap 5: Resultaat afdrukken

```csharp
// ExStart:7
Console.WriteLine("Areas coordinates:");
lines.ForEach(a => Console.WriteLine($"x:{a.X} y:{a.Y} width:{a.Width} height:{a.Height}"));
// ExEnd:7
```

Print de coördinaten van de gedetecteerde gebieden naar de console. Je ziet waarden die je later kunt gebruiken om **lijncoördinaten** te extraheren voor aangepaste verwerking.

## Waarom Aspose.OCR gebruiken voor lijnrechthoeken?

- **Hoge nauwkeurigheid** – Geavanceerde algoritmen detecteren lijnen zelfs in ruis‑ of scheve afbeeldingen.  
- **Cross‑platform** – Werkt op .NET Framework, .NET Core en .NET 5/6.  
- **Geen externe afhankelijkheden** – Pure .NET‑bibliotheek, geen native DLL's om mee te leveren.  
- **Rijke output** – Naast lijnrechthoeken kun je ook woorden, tekens en vertrouwensscores ophalen.

## Veelvoorkomende problemen en oplossingen

| Probleem | Oplossing |
|----------|-----------|
| **Geen rechthoeken geretourneerd** | Zorg ervoor dat de afbeelding duidelijke, horizontale tekst bevat en dat `AreasType.LINES` is gespecificeerd. |
| **Onjuiste coördinaten** | Controleer de DPI van de afbeelding; afbeeldingen met lage resolutie kunnen onnauwkeurige grenzen veroorzaken. |
| **Prestatieknelpunt bij grote afbeeldingen** | Verklein de afbeelding tot een redelijke resolutie voordat je `GetRectangles` aanroept. |
| **Licentie‑exceptie** | Gebruik een proeflicentie voor testen; pas een volledige licentie toe voor productie om evaluatielimieten te vermijden. |

## Veelgestelde vragen

### V1: Kan ik Aspose.OCR voor .NET gebruiken met elk type afbeelding?

A1: Aspose.OCR ondersteunt een breed scala aan afbeeldingsformaten, wat flexibiliteit biedt in je OCR‑toepassingen.

### V2: Hoe nauwkeurig is de OCR‑herkenning?

A2: Aspose.OCR maakt gebruik van geavanceerde algoritmen voor hoge nauwkeurigheid, waardoor het geschikt is voor verschillende tekstherkenningsscenario's.

### V3: Is er een proefversie beschikbaar?

A3: Ja, je kunt de mogelijkheden van Aspose.OCR voor .NET verkennen met de [gratis proefversie](https://releases.aspose.com/).

### V4: Waar kan ik uitgebreide documentatie vinden?

A4: Raadpleeg de [documentatie](https://reference.aspose.com/ocr/net/) voor gedetailleerde informatie en gebruiksrichtlijnen.

### V5: Hulp nodig of specifieke vragen?

A5: Bezoek het [Aspose.OCR‑forum](https://forum.aspose.com/c/ocr/16) voor community‑ondersteuning en discussies.

## Veelgestelde vragen

**V: Kan ik individuele woorden extraheren in plaats van volledige regels?**  
A: Ja, gebruik `AreasType.WORDS` met dezelfde `GetRectangles`‑methode om woord‑niveau begrenzingskaders te verkrijgen.

**V: Ondersteunt de API multi‑page PDF's?**  
A: Converteer eerst elke PDF‑pagina naar een afbeelding, en roep vervolgens `GetRectangles` aan voor elke afbeelding.

**V: Hoe ga ik om met gedraaide tekst?**  
A: Schakel de auto‑rotate‑optie in de OCR‑instellingen in of roteer de afbeelding vooraf voordat je deze verwerkt.

**V: Is er een manier om vertrouwensscores voor elke regel te krijgen?**  
A: Na het verkrijgen van de rechthoeken, roep `api.RecognizeImage(...).Lines` aan om lijnobjecten te benaderen die vertrouwenswaarden bevatten.

**V: Welke .NET‑versies zijn compatibel?**  
A: De bibliotheek werkt met .NET Framework 4.5+, .NET Core 3.1+, en .NET 5/6.

## Conclusie

Gefeliciteerd! Je hebt met succes **OCR‑lijnrechthoeken** verkregen voor een afbeelding met behulp van Aspose.OCR voor .NET. Met de begrenzingskaders kun je nu lijncoördinaten invoeren in downstream‑werkstromen zoals aangepaste weergave, gegevensextractie of lay‑outanalyse.

---

**Laatst bijgewerkt:** 2025-12-17  
**Getest met:** Aspose.OCR 24.11 for .NET  
**Auteur:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}