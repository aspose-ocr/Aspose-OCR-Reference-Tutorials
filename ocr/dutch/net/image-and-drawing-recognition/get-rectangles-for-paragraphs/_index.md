---
date: 2025-12-17
description: Leer hoe je rechthoeken voor alinea's in OCR‑afbeeldingen kunt extraheren
  met Aspose.OCR voor .NET – de ultieme gids over het extraheren van rechthoeken en
  het ophalen van alinea‑coördinaten.
linktitle: Get Rectangles for Paragraphs in OCR Image Recognition
second_title: Aspose.OCR .NET API
title: Hoe rechthoeken voor alinea's te extraheren in OCR-beeldherkenning
url: /nl/net/image-and-drawing-recognition/get-rectangles-for-paragraphs/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe rechthoeken voor alinea's te extraheren in OCR-beeldherkenning

## Introductie

Welkom bij onze uitgebreide gids over **hoe rechthoeken te extraheren** voor alinea's in OCR-beeldherkenning met Aspose.OCR voor .NET. Als je je document‑verwerkingspipeline wilt verbeteren, alinea‑grenzen wilt ophalen en gegevensautomatisering wilt realiseren, ben je hier op het juiste adres. We lopen elke stap door — van het opzetten van de omgeving tot het afdrukken van de rechthoekcoördinaten — zodat je de OCR‑resultaten meteen kunt gebruiken.

## Snelle antwoorden
- **Wat betekent “rechthoeken extraheren”?** Het retourneert de begrenzende vakken (x, y, breedte, hoogte) van gedetecteerde tekstgebieden.  
- **Welke API‑methode levert de rechthoeken?** `AsposeOcr.GetRectangles` met `AreasType.PARAGRAPHS`.  
- **Heb ik een licentie nodig voor ontwikkeling?** Een gratis proefversie werkt voor testen; een commerciële licentie is vereist voor productie.  
- **Kan ik meerdere afbeeldingen tegelijk verwerken?** Ja — loop over je afbeeldingslijst en roep `GetRectangles` aan voor elk bestand.  
- **Welke formaten worden ondersteund?** PNG, JPEG, TIFF, BMP en nog veel meer.

## Wat betekent “hoe rechthoeken te extraheren” in OCR?
In OCR‑terminologie betekent het extraheren van rechthoeken het identificeren van de geometrische grenzen die elke alinea of regel tekst binnen een afbeelding omsluiten. Deze coördinaten stellen je in staat om specifieke delen van een gescand document te markeren, bij te snijden of verder te analyseren.

## Waarom alinea‑coördinaten extraheren?
- **Precieze post‑processing** – je kunt elke rechthoek invoeren in downstream‑workflows (bijv. vertaling, redactie).  
- **Verbeterde UI/UX** – overlay begrenzende vakken op de originele afbeelding om gebruikers te laten zien waar tekst is gevonden.  
- **Batch‑automatisering** – snel alinea's lokaliseren en isoleren in grote documentenverzamelingen.

## Voorvereisten

- Basiskennis van C# en .NET‑ontwikkeling.  
- Een ontwikkelomgeving met Aspose.OCR voor .NET geïnstalleerd – je kunt het downloaden [hier](https://releases.aspose.com/ocr/net/).  
- Vertrouwdheid met beeldverwerkingconcepten en waarom OCR essentieel is voor het extraheren van tekst uit gescande bestanden.

## Namespaces importeren

Importeer in je C#‑bestand de benodigde namespaces zodat de OCR‑klassen beschikbaar zijn:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Stap 1: Stel je documentmap in

Definieer de map die de afbeeldingen bevat die je wilt analyseren:

```csharp
string dataDir = "Your Document Directory";
```

## Stap 2: Initialiseert AsposeOcr‑instantie

Maak een `AsposeOcr`‑object — dit geeft je toegang tot alle OCR‑functies:

```csharp
AsposeOcr api = new AsposeOcr();
```

## Stap 3: Specificeer het afbeeldingspad

Verwijs naar het exacte afbeeldingsbestand dat je wilt verwerken:

```csharp
string fullPath = dataDir + "sample.png";
```

## Stap 4: Herken afbeelding en haal alinea‑rechthoeken op

Roep de `GetRectangles`‑methode aan. Het instellen van `detect_areas` op `true` vertelt de engine om **alinea**‑rechthoeken te retourneren:

```csharp
List<Rectangle> rectangles = api.GetRectangles(fullPath, AreasType.PARAGRAPHS, true);
```

## Stap 5: Resultaten afdrukken

Geef de coördinaten weer zodat je de **extracted paragraph coordinates** kunt zien die zijn gedetecteerd:

```csharp
Console.WriteLine("Areas coordinates:");
rectangles.ForEach(a => Console.WriteLine($"x:{a.X} y:{a.Y} width:{a.Width} height:{a.Height}"));
```

## Veelvoorkomende problemen en oplossingen

| Probleem | Reden | Oplossing |
|----------|-------|-----------|
| Geen rechthoeken geretourneerd | Afbeeldingskwaliteit te laag of verkeerde `AreasType` | Zorg dat de afbeelding duidelijk is en gebruik `AreasType.PARAGRAPHS`. |
| Coördinaten zijn één pixel verschoven | DPI‑schalingsmismatch | Stel de juiste DPI in bij het laden van de afbeelding of gebruik `api.Config.Dpi`. |
| Licentie‑exception | Werken zonder geldige licentie in productie | Pas een tijdelijke of permanente licentie toe via `api.SetLicense`. |

## Veelgestelde vragen

**V: Is Aspose.OCR compatibel met verschillende afbeeldingsformaten?**  
A: Ja, Aspose.OCR ondersteunt PNG, JPEG, TIFF, BMP en vele andere gangbare formaten.

**V: Kan ik Aspose.OCR gebruiken voor batch‑verwerking van meerdere afbeeldingen?**  
A: Absoluut! Loop door een collectie bestands‑paden en roep `GetRectangles` aan voor elke afbeelding.

**V: Is er een gratis proefversie beschikbaar voor Aspose.OCR voor .NET?**  
A: Ja, je kunt een gratis proefversie verkennen [hier](https://releases.aspose.com/).

**V: Hoe kan ik een tijdelijke licentie voor Aspose.OCR verkrijgen?**  
A: Je kunt een tijdelijke licentie verkrijgen [hier](https://purchase.aspose.com/temporary-license/).

**V: Waar vind ik extra ondersteuning en discussies over Aspose.OCR?**  
A: Ga naar het [Aspose.OCR‑forum](https://forum.aspose.com/c/ocr/16) voor community‑ondersteuning en discussies.

## Conclusie

In deze tutorial hebben we **hoe rechthoeken te extraheren** voor alinea's met Aspose.OCR voor .NET laten zien, elke code‑snippet doorgenomen en uitgelegd hoe je de geretourneerde coördinaten moet interpreteren. Door deze stappen in je applicatie te integreren, kun je betrouwbaar alinea‑grenzen ophalen, document‑workflows verbeteren en slimmere OCR‑gedreven oplossingen bouwen.

---

**Laatst bijgewerkt:** 2025-12-17  
**Getest met:** Aspose.OCR 24.11 voor .NET  
**Auteur:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}