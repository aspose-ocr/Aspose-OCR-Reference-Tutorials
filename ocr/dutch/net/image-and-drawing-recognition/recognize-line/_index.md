---
date: 2026-02-22
description: Leer hoe je tekst uit een afbeelding kunt extraheren met Aspose.OCR voor
  .NET, PNG naar tekst kunt converteren en de OCR-nauwkeurigheid in C#-toepassingen
  kunt verbeteren.
linktitle: Extract Text from Image – Recognize Line with Aspose.OCR
second_title: Aspose.OCR .NET API
title: Tekst uit afbeelding extraheren – Regel herkennen met Aspose.OCR
url: /nl/net/image-and-drawing-recognition/recognize-line/
weight: 14
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tekst uit afbeelding extraheren – Regel herkennen met Aspose.OCR

## Introductie

Optical character recognition (OCR) is de standaardoplossing geworden om afbeeldingen met tekst om te zetten in doorzoekbare, bewerkbare inhoud. Als u **tekst uit afbeelding** bestanden snel en betrouwbaar wilt **extraheren**, biedt Aspose.OCR voor .NET een krachtige, ontwikkelaar‑vriendelijke API die werkt zowel op het volledige .NET Framework als **ASP OCR .NET Core** projecten. In deze tutorial lopen we alles door wat u moet weten om regels in een afbeelding te herkennen, die regels om te zetten naar platte tekst en het resultaat weer te geven — alles met nette, gemakkelijk te volgen C#‑code.

## Snelle antwoorden
- **Wat doet Aspose.OCR?** Het leest gedrukte of handgeschreven tekst uit afbeeldingsformaten en retourneert platte strings.  
- **Welke afbeeldingsformaten worden ondersteund?** PNG, JPEG, BMP, GIF, TIFF en meer.  
- **Heb ik een licentie nodig voor testen?** Een gratis proefversie werkt voor ontwikkeling; een licentie is vereist voor productie.  
- **Kan ik dit draaien op .NET Core?** Ja – de bibliotheek ondersteunt .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6.  
- **Hoe lang duurt een eenvoudige regelherkenning?** Meestal minder dan een seconde voor een standaard PNG.

## Wat is “tekst uit afbeelding extraheren”?

Tekst uit een afbeelding extraheren betekent dat je OCR‑technologie gebruikt om de visuele pixels te analyseren, tekens te identificeren en deze als machinaal leesbare tekst uit te voeren. Dit maakt scenario's mogelijk zoals het digitaliseren van gescande documenten, het automatiseren van gegevensinvoer van bonnetjes, of het bouwen van doorzoekbare archieven.

## Waarom Aspose.OCR voor .NET gebruiken?

- **Hoge nauwkeurigheid** over meerdere talen en lettertypen.  
- **Geen externe afhankelijkheden** – pure managed code, gemakkelijk te integreren.  
- **Uitgebreide formaatondersteuning** – werkt met PNG, JPEG, BMP en meer.  
- **Eenvoudige API** – een paar regels code brengen je van afbeelding naar tekst.  

### Hoe helpt dit je **PNG naar tekst converteren**?

Omdat Aspose.OCR PNG‑bestanden direct kan lezen, kun je een gescande PNG‑afbeelding aan de `RecognizeLine`‑methode voeren en een schone string ontvangen zonder tussenliggende conversiestappen.

## Vereisten

Voor we beginnen, zorg dat u het volgende heeft:

- **Ontwikkelomgeving** – Visual Studio 2022 (of een andere gewenste .NET‑IDE).  
- **Aspose.OCR voor .NET** – download het via de [downloadlink](https://releases.aspose.com/ocr/net/).  
- **Documentmap** – een map op uw computer waar de voorbeeldafbeelding (`sample_line.png`) zich bevindt. Vervang “Your Document Directory” in de code door het daadwerkelijke pad.

## Namespaces importeren

In .NET geven namespaces u toegang tot de benodigde klassen. Voeg deze using‑statements toe aan de bovenkant van uw C#‑bestand:

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

## Hoe tekst uit afbeelding extraheren met Aspose.OCR

Hieronder staat de stap‑voor‑stap implementatie. Elk code‑blok is ongewijzigd ten opzichte van de originele tutorial, zodat de exacte logica behouden blijft.

### Stap 1: Aspose.OCR initialiseren

```csharp
// ExStart:1
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
// ExEnd:1
```

> **Pro tip:** Gebruik een absoluut pad of `Path.Combine` om pad‑scheidingstekenproblemen tussen besturingssystemen te vermijden.

### Stap 2: Regels in afbeelding herkennen

```csharp
// ExStart:3
// Recognize image
string result = api.RecognizeLine(dataDir + "sample_line.png");
// ExEnd:3
```

De `RecognizeLine`‑methode richt zich op één regel tekst, waardoor hij ideaal is wanneer u de lay-out van uw afbeelding kent. Het is ook een uitstekende manier om **gescande afbeeldings‑tekst te lezen** wanneer het document één regel met belangrijke gegevens bevat.

### Stap 3: Herkende tekst weergeven

```csharp
// ExStart:4
// Display the recognized text
Console.WriteLine(result);
// ExEnd:4
```

Het uitvoeren van het programma zal de geëxtraheerde regel naar de console afdrukken, waarmee wordt bevestigd dat de **tekst‑extractie uit afbeelding** operatie geslaagd is.

### Stap 4: Voltooiingsbericht

```csharp
Console.WriteLine("RecognizeLine executed successfully");
```

Het zien van dit bericht betekent dat het OCR‑proces zonder fouten is voltooid.

## Hoe OCR‑nauwkeurigheid te verbeteren met Aspose.OCR?

- **Gebruik hoge resolutie‑afbeeldingen** (300 dpi of hoger).  
- **Pas beeld‑preprocessing toe** zoals binarisatie of ruisverwijdering met `api.PreprocessImage`.  
- **Selecteer de juiste taal** met `api.Language = OcrLanguage.English;` (of de juiste taal‑enum).  
- **Snijd randen bij** om irrelevante achtergrond te verwijderen.

## Veelvoorkomende problemen & oplossingen

| Probleem | Reden | Oplossing |
|----------|-------|-----------|
| `FileNotFoundException` | Onjuist `dataDir`‑pad | Controleer het mappad en zorg ervoor dat `sample_line.png` bestaat. |
| Slechte nauwkeurigheid | Afbeelding met lage resolutie | Gebruik een bron met hogere resolutie of pre‑process de afbeelding (bijv. binarisatie). |
| Niet‑ondersteund formaat | Afbeelding niet in ondersteunde lijst | Converteer de afbeelding naar PNG of JPEG voordat `RecognizeLine` wordt aangeroepen. |

## Veelgestelde vragen

### V1: Is Aspose.OCR compatibel met alle afbeeldingsformaten?

A1: Aspose.OCR ondersteunt een breed scala aan afbeeldingsformaten, waaronder PNG, JPEG, GIF, BMP en meer. Zie de [documentatie](https://reference.aspose.com/ocr/net/) voor een gedetailleerde lijst.

### V2: Kan ik Aspose.OCR gebruiken voor commerciële projecten tijdens de proefperiode?

A2: Ja, u kunt de mogelijkheden van Aspose.OCR verkennen in commerciële projecten tijdens de proefperiode. Voor langdurig gebruik, overweeg het [kopen van een licentie](https://purchase.aspose.com/buy).

### V3: Hoe kan ik hulp zoeken of bijdragen aan de Aspose.OCR‑gemeenschap?

A3: Neem contact op met de levendige Aspose.OCR‑gemeenschap op het [ondersteuningsforum](https://forum.aspose.com/c/ocr/16) voor hulp en samenwerking.

### V4: Zijn tijdelijke licenties beschikbaar voor Aspose.OCR?

A4: Ja, u kunt tijdelijke licenties voor Aspose.OCR verkrijgen om de functies te evalueren. Bezoek [hier](https://purchase.aspose.com/temporary-license/) voor meer details.

### V5: Wat zijn de systeemvereisten voor Aspose.OCR voor .NET?

A5: Zie de [documentatie](https://reference.aspose.com/ocr/net/) voor uitgebreide systeemvereisten.

## Conclusie

Door deze stappen te volgen heeft u geleerd hoe u **tekst uit afbeelding** bestanden kunt extraheren met Aspose.OCR voor .NET, specifiek door individuele regels te herkennen. Deze mogelijkheid opent de deur naar geautomatiseerde gegevensverzameling, het bouwen van doorzoekbare archieven en het integreren van OCR in elke .NET‑applicatie—of u nu het volledige framework of **ASP OCR .NET Core** target.

---

**Laatst bijgewerkt:** 2026-02-22  
**Getest met:** Aspose.OCR 24.12 for .NET  
**Auteur:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}