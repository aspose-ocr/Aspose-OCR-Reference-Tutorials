---
date: 2025-12-21
description: Leer hoe u OCR kunt uitvoeren en tekst uit een afbeelding kunt extraheren
  met Aspose.OCR voor .NET. Deze stapsgewijze handleiding toont meertalige teksterkenning
  en taalkeuze.
linktitle: How to Perform OCR with Language Selection in Aspose.OCR
second_title: Aspose.OCR .NET API
title: Hoe OCR uit te voeren met taalselectie in Aspose.OCR
url: /nl/net/ocr-configuration/ocr-operation-with-language-selection/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe OCR uit te voeren met taalkeuze in Aspose.OCR

## Inleiding

Als je **hoe OCR uit te voeren** op afbeeldingen en tekst uit afbeeldingsbestanden in een .NET‑applicatie wilt extraheren, biedt Aspose.OCR voor .NET een snelle, nauwkeurige en taal‑bewuste oplossing. In deze tutorial lopen we een praktisch voorbeeld door dat OCR‑beeldherkenning met taalkeuze demonstreert, zodat je meertalige tekst uit afbeeldingen kunt halen met slechts een paar regels code.

## Snelle antwoorden
- **Wat doet Aspose.OCR?** Het herkent gedrukte en handgeschreven tekst in afbeeldingen en retourneert de geëxtraheerde tekst.  
- **Kan ik de taal kiezen?** Ja – je kunt elke ondersteunde taal opgeven, zoals Engels, Duits, Spaans, Chinees, enz.  
- **Heb ik een licentie nodig voor ontwikkeling?** Een gratis proefversie werkt voor evaluatie; een licentie is vereist voor productiegebruik.  
- **Welke .NET‑versies worden ondersteund?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6+.  
- **Is scheefstandcorrectie automatisch?** Je kunt `AutoSkew` inschakelen en de `SkewAngle`‑instelling fijn afstellen.

## Waarom Aspose.OCR kiezen voor OCR‑taken?

- **Hoge nauwkeurigheid** over meerdere lettertypen en afbeeldingskwaliteiten.  
- **Ingebouwde taalkeuze** elimineert de noodzaak voor externe taalpakketten.  
- **Eenvoudige API** die naadloos integreert met bestaande C#‑projecten.  
- **Geen externe afhankelijkheden** – alles draait lokaal, waardoor je gegevens veilig blijven.

## Voorvereisten

Voordat we in de code duiken, zorg ervoor dat je de volgende zaken gereed hebt:

- Aspose.OCR voor .NET: Zorg dat je de Aspose.OCR‑bibliotheek geïnstalleerd hebt. Je kunt deze downloaden van de [Aspose.OCR for .NET downloadpagina](https://releases.aspose.com/ocr/net/).

- Ontwikkelomgeving: Stel een werkende omgeving in met een .NET‑applicatie. Als je dit nog niet hebt gedaan, raadpleeg dan de [documentatie](https://reference.aspose.com/ocr/net/) voor gedetailleerde instructies.

## Importeren van namespaces

In je .NET‑applicatie begin je met het importeren van de benodigde namespaces:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Stap 1: Initialiseer Aspose.OCR

Begin met het initialiseren van een instantie van de Aspose.OCR‑klasse. Dit bereidt de OCR‑functionaliteit voor in je applicatie.

```csharp
// ExStart:1
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Stap 2: Specificeer afbeeldingspad

Definieer vervolgens het pad naar de afbeelding waarop je OCR wilt uitvoeren. Zorg ervoor dat de afbeelding toegankelijk is vanuit je applicatie.

```csharp
// Image Path
string fullPath = dataDir + "sample.png";
```

## Stap 3: Herken afbeelding met taalkeuze

Nu volgt de kern‑OCR‑bewerking. Gebruik de Aspose.OCR‑bibliotheek om tekst te herkennen uit de opgegeven afbeelding. Pas de herkenningsinstellingen aan, inclusief de taalkeuze.

```csharp
// Recognize image           
RecognitionResult result = api.RecognizeImage(fullPath, new RecognitionSettings
{
    DetectAreas = true,
    RecognizeSingleLine = false,
    AutoSkew = true,
    SkewAngle = 0.2F,
    Language = Language.Eng, // Choose the language: none, eng, deu, por, spa, fra, ita, cze, dan, dum, est, fin, lav, lit, nor, pol, rum, srp_hrv, slk, slv, swe, chi
});
```

## Stap 4: Print en toon resultaten

Na de OCR‑bewerking, print en toon je de resultaten, inclusief herkende tekst, gebieden, waarschuwingen en de JSON‑representatie.

```csharp
// Print result
Console.WriteLine($"Text:\n {result.RecognitionText}");
Console.WriteLine("Areas:");
result.RecognitionAreasText.ForEach(a => Console.WriteLine($"{a}"));
Console.WriteLine("Warnings:");
result.Warnings.ForEach(w => Console.WriteLine($"{w}"));
Console.WriteLine($"JSON: {result.GetJson()}");
// ExEnd:1
```

## Veelvoorkomende problemen en tips

- **Onjuiste taalkeuze** – Als de output er onleesbaar uitziet, controleer dan of de `Language`‑eigenschap overeenkomt met de taal van de bronafbeelding.  
- **Scheefstaande afbeeldingen** – Schakel `AutoSkew` in of pas handmatig `SkewAngle` aan voor betere nauwkeurigheid bij gekantelde scans.  
- **Grote bestanden** – Verwerk grote afbeeldingen in delen of verlaag de resolutie voordat je ze aan `RecognizeImage` doorgeeft om geheugen te besparen.

## Conclusie

Gefeliciteerd! Je hebt geleerd **hoe OCR uit te voeren** met taalkeuze met behulp van Aspose.OCR voor .NET. Deze tutorial heeft je laten zien hoe je tekst uit afbeeldingsbestanden kunt extraheren, herkenningsinstellingen kunt aanpassen en moeiteloos met meertalige inhoud omgaat.

## Veelgestelde vragen

### Q1: Is Aspose.OCR geschikt voor meertalige teksterkenning?

A1: Ja, Aspose.OCR ondersteunt verschillende talen en biedt flexibiliteit voor meertalige OCR‑taken.

### Q2: Kan ik OCR‑instellingen fijn afstemmen voor specifieke afbeeldingskenmerken?

A2: Absoluut! Pas parameters zoals scheefstandhoek, lijnherkenning en gebiedsdetectie aan om OCR te optimaliseren voor verschillende scenario's.

### Q3: Waar vind ik extra ondersteuning of community‑discussies?

A3: Bezoek het [Aspose.OCR‑forum](https://forum.aspose.com/c/ocr/16) voor ondersteuning en discussies met de community.

### Q4: Is er een gratis proefversie beschikbaar?

A4: Ja, verken de [gratis proefversie](https://releases.aspose.com/) om de mogelijkheden van Aspose.OCR te ervaren.

### Q5: Hoe kan ik Aspose.OCR voor .NET aanschaffen?

A5: Ga naar de [aankooppagina](https://purchase.aspose.com/buy) om te kopen.

---

**Laatst bijgewerkt:** 2025-12-21  
**Getest met:** Aspose.OCR 24.11 voor .NET  
**Auteur:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}