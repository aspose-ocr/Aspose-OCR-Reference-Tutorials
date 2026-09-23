---
date: 2026-02-22
description: Leer hoe je layout-analyse-OCR kunt uitvoeren door tekstregels in een
  afbeelding te herkennen en regelrechthoeken te extraheren met Aspose.OCR voor .NET.
linktitle: Layout Analysis OCR – Get Line Rectangles from Images
second_title: Aspose.OCR .NET API
title: Lay-outanalyse OCR – Haal lijnrechthoeken uit afbeeldingen
url: /nl/net/image-and-drawing-recognition/get-rectangles-for-lines/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Layoutanalyse OCR – Verkrijg lijnrechthoeken uit afbeeldingen

## Inleiding

In deze tutorial ontdek je **hoe je OCR‑lijnrechthoeken** kunt verkrijgen met Aspose.OCR voor .NET. Aan het einde van de gids kun je **tekstregels in een afbeelding herkennen** en **lijncoördinaten extraheren** voor elke gedetecteerde regel — perfect voor downstream verwerking zoals **layoutanalyse OCR**, data‑extractie of aangepaste weergave.

## Snelle antwoorden
- **Wat betekent “get OCR line rectangles”?** Het retourneert de begrenzingskaders van elke tekstregel die in een afbeelding wordt gedetecteerd.  
- **Welke API‑methode wordt gebruikt?** `AsposeOcr.GetRectangles(..., AreasType.LINES, ...)`.  
- **Heb ik een licentie nodig?** Een gratis proefversie werkt voor ontwikkeling; een commerciële licentie is vereist voor productie.  
- **Ondersteunde afbeeldingsformaten?** PNG, JPEG, BMP, TIFF en meer.  
- **Kan ik dit uitvoeren op .NET Core?** Ja, Aspose.OCR ondersteunt volledig .NET Core en .NET 5/6.

## Vereisten

Voordat je aan de tutorial begint, zorg ervoor dat je de volgende vereisten hebt:

- Basiskennis van C# en .NET‑ontwikkeling.  
- Een geïntegreerde ontwikkelomgeving (IDE) zoals Visual Studio.  
- Aspose.OCR voor .NET‑bibliotheek geïnstalleerd. Je kunt deze downloaden [hier](https://releases.aspose.com/ocr/net/).  
- Een voorbeeldafbeelding met tekst voor OCR‑herkenning.

## Namespaces importeren

Zorg ervoor dat de benodigde namespaces in je project zijn geïmporteerd. Voeg de volgende regels toe aan de bovenkant van je C#‑bestand:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

Laten we nu het proces van het verkrijgen van rechthoeken voor regels in OCR‑afbeeldingsherkenning opsplitsen in gemakkelijk te volgen stappen.

## layoutanalyse ocr – Stapsgewijze gids

### Stap 1: Stel uw documentmap in

```csharp
// ExStart:3
string dataDir = "Your Document Directory";
// ExEnd:3
```

Vervang `"Your Document Directory"` door het daadwerkelijke pad naar de map die je voorbeeldafbeelding bevat.

### Stap 2: Initialiseer Aspose.OCR

```csharp
// ExStart:4
AsposeOcr api = new AsposeOcr();
// ExEnd:4
```

Maak een instantie van de `AsposeOcr`‑klasse om toegang te krijgen tot de OCR‑functionaliteit.

### Stap 3: Specificeer afbeeldingspad

```csharp
// ExStart:5
string fullPath = dataDir + "sample.png";
// ExEnd:5
```

Definieer het volledige pad naar de afbeelding waarop je OCR wilt uitvoeren.

### Stap 4: Herken afbeelding en verkrijg rechthoeken

```csharp
// ExStart:6
List<Rectangle> lines = api.GetRectangles(fullPath, AreasType.LINES, false);
// ExEnd:6
```

De `GetRectangles`‑methode retourneert een lijst van `Rectangle`‑objecten, elk met de coördinaten van een gedetecteerde tekstregel. Dit is de kern van **het verkrijgen van OCR‑lijnrechthoeken** en maakt **layoutanalyse OCR** mogelijk.

### Stap 5: Resultaat afdrukken

```csharp
// ExStart:7
Console.WriteLine("Areas coordinates:");
lines.ForEach(a => Console.WriteLine($"x:{a.X} y:{a.Y} width:{a.Width} height:{a.Height}"));
// ExEnd:7
```

Druk de coördinaten van de gedetecteerde gebieden af naar de console. Je ziet waarden die je later kunt gebruiken om **lijncoördinaten te extraheren** voor aangepaste verwerking.

## Waarom Aspose.OCR gebruiken voor lijnrechthoeken?

- **Hoge nauwkeurigheid** – Geavanceerde algoritmen detecteren regels zelfs in ruis‑ of scheve afbeeldingen.  
- **Cross‑platform** – Werkt op .NET Framework, .NET Core en .NET 5/6.  
- **Geen externe afhankelijkheden** – Pure .NET‑bibliotheek, geen native DLL‑s die meegeleverd moeten worden.  
- **Rijke output** – Naast lijnrechthoeken kun je ook woorden, tekens en vertrouwensscores ophalen.

## Veelvoorkomende problemen en oplossingen

| Probleem | Oplossing |
|----------|-----------|
| **Geen rechthoeken geretourneerd** | Zorg ervoor dat de afbeelding duidelijke, horizontale tekst bevat en dat `AreasType.LINES` is gespecificeerd. |
| **Onjuiste coördinaten** | Controleer de DPI van de afbeelding; afbeeldingen met lage resolutie kunnen onnauwkeurige grenzen veroorzaken. |
| **Prestatieknelpunt bij grote afbeeldingen** | Verklein de afbeelding tot een redelijke resolutie voordat `GetRectangles` wordt aangeroepen. |
| **Licentie‑exception** | Gebruik een proeflicentie voor testen; pas een volledige licentie toe voor productie om evaluatielimieten te vermijden. |

## Veelgestelde vragen

**V: Kan ik individuele woorden extraheren in plaats van volledige regels?**  
A: Ja, gebruik `AreasType.WORDS` met dezelfde `GetRectangles`‑methode om woord‑niveau begrenzingskaders te verkrijgen.

**V: Ondersteunt de API multi‑page PDF’s?**  
A: Converteer elke PDF‑pagina eerst naar een afbeelding, roep daarna `GetRectangles` aan voor elke afbeelding.

**V: Hoe ga ik om met gedraaide tekst?**  
A: Schakel de auto‑rotate‑optie in de OCR‑instellingen in of roteer de afbeelding vooraf voordat je deze verwerkt.

**V: Is er een manier om vertrouwensscores voor elke regel te krijgen?**  
A: Nadat je de rechthoeken hebt verkregen, roep je `api.RecognizeImage(...).Lines` aan om lijnobjecten met vertrouwenswaarden te benaderen.

**V: Welke .NET‑versies zijn compatibel?**  
A: De bibliotheek werkt met .NET Framework 4.5+, .NET Core 3.1+, en .NET 5/6.

## Praktische toepassingsgevallen

- **Document layoutanalyse OCR** – Voer lijnrechthoeken in een layout‑engine om kolomstructuren te reconstrueren.  
- **Geautomatiseerde data‑extractie** – Gebruik de coördinaten om individuele regels bij te snijden voor downstream NLP‑pijplijnen.  
- **Aangepaste weergave** – Overleg begrenzingskaders op de originele afbeelding voor visuele verificatie of UI‑overlays.  

## Conclusie

Gefeliciteerd! Je hebt met succes **OCR‑lijnrechthoeken** verkregen voor een afbeelding met behulp van Aspose.OCR voor .NET. Met de begrenzingskaders in de hand kun je nu lijncoördinaten invoeren in downstream‑workflows zoals aangepaste weergave, data‑extractie of **layoutanalyse OCR**.

---

**Laatst bijgewerkt:** 2026-02-22  
**Getest met:** Aspose.OCR 24.11 for .NET  
**Auteur:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}