---
date: 2026-02-25
description: Leer hoe u tekst uit een afbeelding kunt extraheren met Aspose.OCR voor
  .NET. Deze gids leidt u door het voorbereiden van rechthoeken voor OCR-beeldherkenning
  en het verbeteren van de nauwkeurigheid.
linktitle: Prepare Rectangles in OCR Image Recognition
second_title: Aspose.OCR .NET API
title: Hoe tekst uit een afbeelding te extraheren door rechthoeken voor te bereiden
  in OCR
url: /nl/net/ocr-optimization/prepare-rectangles/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Rechthoeken voorbereiden in OCR-beeldherkenning

## Introductie

Optical Character Recognition (OCR) is essentieel voor het omzetten van visuele inhoud naar doorzoekbare, bewerkbare tekst. In deze tutorial **haal je tekst uit een afbeelding** door aangepaste rechthoeken te definiëren die de OCR‑engine richten op specifieke gebieden. Met Aspose.OCR voor .NET lopen we elke stap door – van het opzetten van je project tot het ophalen van de herkende tekst – zodat je krachtige afbeelding‑naar‑tekst functionaliteit kunt integreren in je .NET‑applicaties.

## Snelle antwoorden
- **Wat betekent “tekst uit afbeelding halen”?** Het betekent het omzetten van de visuele tekens in een afbeelding naar machinaal leesbare strings.  
- **Welke bibliotheek helpt hierbij in .NET?** Aspose.OCR voor .NET.  
- **Heb ik een licentie nodig voor ontwikkeling?** Een gratis proefversie werkt voor testen; een licentie is vereist voor productie.  
- **Kan ik specifieke gebieden targeten?** Ja, door rechthoeken te definiëren die de OCR‑scope beperken.  
- **Welke .NET‑versies worden ondersteund?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.

## Wat is “tekst uit afbeelding halen” met rechthoeken?
Wanneer je rechthoekige zones op een afbeelding definieert, verwerkt de OCR‑engine alleen die zones. Dit verbetert de nauwkeurigheid, verkort de verwerkingstijd en laat je storende achtergronden of irrelevante delen negeren.

## Waarom rechthoeken voorbereiden vóór OCR?
- **Focus op relevante inhoud:** Sla kopteksten, voetteksten of decoratieve grafieken over.  
- **Verbeterde prestaties:** Kleinere gebieden betekenen snellere herkenning.  
- **Verbeterde nauwkeurigheid:** Minder visueel lawaai leidt tot schonere resultaten.

## Waarom dit belangrijk is voor real‑world projecten
Veel zakelijke documenten – bonnen, facturen, ID‑kaarten – hebben gemengde lay‑outs waarbij alleen bepaalde delen waardevolle tekst bevatten. Door rechthoeken te gebruiken, kun je alleen de benodigde velden extraheren, waardoor de nabewerking drastisch wordt verminderd en de betrouwbaarheid van je automatiseringspipeline toeneemt.

## Veelvoorkomende use‑cases
- **Gegevensinvoerautomatisering:** Haal specifieke velden uit gescande formulieren.  
- **Compliance‑controles:** Isoleer en verifieer juridische tekstblokken.  
- **Inhouds‑indexering:** Index alleen de kop of bijschrift van een afbeelding voor zoekmachines.  

## Voorvereisten

- Vertrouwdheid met C# en .NET‑ontwikkeling.  
- Aspose.OCR voor .NET bibliotheek geïnstalleerd – je kunt deze **[hier](https://releases.aspose.com/ocr/net/)** downloaden.  
- Een voorbeeldafbeelding (bijv. `sample.png`) die de tekst bevat die je wilt extraheren.

## Namespaces importeren

Breng eerst de benodigde namespaces in scope:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Stap 1: Stel je documentmap in

Geef aan waar je afbeeldingsbestanden staan en maak een instantie van de OCR‑engine.

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Hoe tekst uit afbeelding halen met meerdere rechthoeken

### Stap 2: Herken afbeelding met meerdere rechthoeken

#### 2.1 Definieer de rechthoeken

Maak een lijst van `Rectangle`‑objecten die de gebieden omschrijven die de OCR‑engine moet scannen.

```csharp
List<Rectangle> rects = new List<Rectangle>()
{
    new Rectangle(138, 352, 2033, 537),
    new Rectangle(147, 890, 2033, 1157),
    new Rectangle(923, 2045, 465, 102),
    new Rectangle(104, 2147, 2076, 819)
};
```

#### 2.2 Voer OCR‑herkenning uit

Geef het afbeeldingspad en de lijst met rechthoeken door aan `RecognizeImage`. De methode retourneert een collectie strings – elk item komt overeen met één rechthoek.

```csharp
// first case
List<string> listResult = api.RecognizeImage(dataDir + "sample.png", rects);

// Display the recognized text
foreach (string s in listResult)
{
    Console.WriteLine(s);
}
```

### Stap 3: Herken afbeelding met Recognition Settings (alternatieve aanpak)

Als je liever `RecognitionSettings` gebruikt, kun je hetzelfde resultaat behalen met een iets andere API‑aanroep.

#### 3.1 Definieer herkenningsinstellingen

```csharp
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings
{
    RecognitionAreas = rects
});
```

#### 3.2 Toon herkende tekst

```csharp
// Display the recognized text
foreach (string s in result.RecognitionAreasText)
{
    Console.WriteLine(s);
}
```

## Veelvoorkomende problemen & tips

- **Onjuiste rechthoekcoördinaten:** Zorg ervoor dat de waarden `X`, `Y`, `Width` en `Height` correct overeenkomen met het gewenste gebied.  
- **Afbeeldingskwaliteit:** Lage resolutie kan slechte OCR‑resultaten geven; overweeg pre‑processing (bijv. binarisatie).  
- **Lege resultaten:** Controleer of de rechthoeken daadwerkelijk tekst bevatten; anders geeft de engine lege strings terug.

## Probleemoplossing en best practices

| Symptoom | Waarschijnlijke oorzaak | Oplossing |
|----------|--------------------------|-----------|
| Geen output of lege strings | Rechthoeken buiten de afbeeldingsgrenzen | Controleer de afmetingen van de afbeelding en de rechthoekcoördinaten |
| Vervormde tekens | Slecht contrast of ruis | Pas beeldreiniging toe (grijstinten, drempel) vóór OCR |
| Trage prestaties bij grote bestanden | Te veel rechthoeken of zeer grote afbeelding | Splits de afbeelding of verminder het aantal rechthoeken waar mogelijk |

## Conclusie

Je hebt nu geleerd hoe je **tekst uit afbeelding haalt** door aangepaste rechthoeken voor te bereiden met Aspose.OCR voor .NET. Deze techniek geeft je fijnmazige controle over OCR‑verwerking, waardoor je snellere, nauwkeurigere tekst‑extractiefuncties in je applicaties kunt bouwen.

## Veelgestelde vragen

**V:** Kan ik Aspose.OCR voor .NET gebruiken met andere .NET‑frameworks?  
**A:** Ja, Aspose.OCR voor .NET is compatibel met diverse .NET‑frameworks.

**V:** Is er een gratis proefversie beschikbaar voor Aspose.OCR voor .NET?  
**A:** Absoluut! Je kunt de gratis proefversie **[hier](https://releases.aspose.com/)** verkrijgen.

**V:** Hoe krijg ik ondersteuning voor Aspose.OCR voor .NET?  
**A:** Bezoek het **[Aspose.OCR‑forum](https://forum.aspose.com/c/ocr/16)** voor toegewijde ondersteuning.

**V:** Kan ik een tijdelijke licentie krijgen voor testdoeleinden?  
**A:** Ja, je kunt een tijdelijke licentie **[hier](https://purchase.aspose.com/temporary-license/)** aanschaffen.

**V:** Waar vind ik de documentatie voor Aspose.OCR voor .NET?  
**A:** De documentatie is beschikbaar **[hier](https://reference.aspose.com/ocr/net/)**.

---

**Laatst bijgewerkt:** 2026-02-25  
**Getest met:** Aspose.OCR 24.11 voor .NET  
**Auteur:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}