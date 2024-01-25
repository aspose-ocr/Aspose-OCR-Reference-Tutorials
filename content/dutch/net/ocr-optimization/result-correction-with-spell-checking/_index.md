---
title: Resultaatcorrectie met spellingcontrole in OCR-beeldherkenning
linktitle: Resultaatcorrectie met spellingcontrole in OCR-beeldherkenning
second_title: Aspose.OCR .NET-API
description: Verbeter de OCR-nauwkeurigheid met Aspose.OCR voor .NET. Corrigeer spellingen, pas woordenboeken aan en bereik moeiteloos foutloze tekstherkenning.
type: docs
weight: 13
url: /nl/net/ocr-optimization/result-correction-with-spell-checking/
---
## Invoering

Op het gebied van Optical Character Recognition (OCR) is het behalen van nauwkeurige resultaten cruciaal voor het extraheren van betekenisvolle informatie uit afbeeldingen. Een veel voorkomende uitdaging is het omgaan met verkeerd gespelde woorden tijdens het herkenningsproces. Gelukkig biedt Aspose.OCR voor .NET een krachtige oplossing om de OCR-resultaten te verbeteren door middel van spellingcontrole.

Deze tutorial leidt u door het proces van resultaatcorrectie met spellingcontrole met behulp van Aspose.OCR voor .NET. Uiteindelijk zult u in staat zijn om de nauwkeurigheid van OCR-afgeleide tekst te verbeteren, waardoor een verfijndere en foutloze uitvoer wordt gegarandeerd.

## Vereisten

Voordat we ingaan op de magie van spellingcontrole, moet je ervoor zorgen dat je aan de volgende vereisten voldoet:

-  Aspose.OCR voor .NET-bibliotheek: Download en installeer de Aspose.OCR-bibliotheek van de .NET-bibliotheek[pagina vrijgeven](https://releases.aspose.com/ocr/net/).

- Documentmap: Zorg ervoor dat u een aangewezen map voor uw documenten heeft. Vervang "Uw documentenmap" in de codefragmenten door het daadwerkelijke pad.

## Naamruimten importeren

Laten we beginnen met het importeren van de benodigde naamruimten in uw .NET-project:

```csharp
using System;
using Aspose.OCR.SpellChecker;
using System.Collections.Generic;
```

## Stap 1: Initialiseer Aspose.OCR

Initialiseer een exemplaar van Aspose.OCR om het OCR-proces een vliegende start te geven.

```csharp
// Het pad naar de documentenmap.
string dataDir = "Your Document Directory";

// Initialiseer een exemplaar van AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Stap 2: Herken afbeelding

Herken vervolgens de tekst in een afbeelding met Aspose.OCR. Hier is een fragment dat dit proces demonstreert:

```csharp
// Herken beeld
RecognitionResult result = api.RecognizeImage(dataDir + "sample_bad.png", new RecognitionSettings(Language.Eng));
```

## Stap 3: Vóór correctie

Haal het OCR-resultaat vóór correctie op om te vergelijken met de gecorrigeerde versie.

```csharp
// Resultaat verkrijgen
Console.WriteLine("BEFORE CORRECTION:\n" + result.RecognitionText);
```

## Stap 4: Na correctie

Pas spellingcontrole toe om het gecorrigeerde resultaat te krijgen. Het volgende codefragment illustreert deze stap:

```csharp
// Krijg een gecorrigeerd resultaat
string correctedResult = result.GetSpellCheckCorrectedText(SpellCheckLanguage.Eng);
Console.WriteLine("AFTER CORRECTION:\n" + correctedResult);
```

## Stap 5: Verkeerd gespelde woorden en suggesties

Verkrijg een lijst met verkeerd gespelde woorden samen met voorgestelde correcties met behulp van de volgende code:

```csharp
// Ontvang een lijst met verkeerd gespelde woorden met suggesties
List<SpellCheckError> errorsList = result.GetSpellCheckErrorList(SpellCheckLanguage.Eng);
foreach (var word in errorsList)
{
	Console.Write("Word:" + word.Word);
	Console.Write(" StartPosition:" + word.StartPosition);
	Console.WriteLine(" Length:" + word.Length);
	Console.WriteLine("SuggestedWords:");
	foreach (var suggest in word.SuggestedWords)
	{
		Console.Write(suggest.Word + " ");
	}
	Console.WriteLine();
}
```

## Stap 6: Corrigeer de gebruikerstekst

Corrigeer specifieke, door de gebruiker aangeleverde tekst met behulp van de Aspose.OCR-bibliotheek:

```csharp
// Correcte gebruikerstekst
Console.WriteLine("recogniition -> " + api.CorrectSpelling("recogniition"));
```

## Stap 7: Correctie met gebruikerswoordenboek

Verbeter de correctie verder door een aangepast gebruikerswoordenboek op te nemen:

```csharp
// Krijg gecorrigeerd resultaat met gebruikerswoordenboek
string correctedResultUserDict = result.GetSpellCheckCorrectedText(SpellCheckLanguage.Eng, dataDir+"dictionary.txt");
Console.WriteLine("AFTER CORRECTION WITH USER DICTIONARY:\n" + correctedResultUserDict);
```

## Conclusie

Gefeliciteerd! U heeft met succes door de spellingcontrolemogelijkheden van Aspose.OCR voor .NET genavigeerd. Met deze functie kunt u de OCR-resultaten verfijnen, waardoor nauwkeurigheid wordt gegarandeerd en fouten worden geëlimineerd.

## Veelgestelde vragen

### V1: Kan ik Aspose.OCR gebruiken voor andere talen dan Engels?

A1: Ja, Aspose.OCR ondersteunt meerdere talen. Pas de taalinstellingen dienovereenkomstig aan.

### V2: Hoe integreer ik Aspose.OCR in mijn .NET-project?

 A2: Raadpleeg de[documentatie](https://reference.aspose.com/ocr/net/) voor gedetailleerde integratiestappen.

### V3: Is er een proefversie beschikbaar voor Aspose.OCR?

 A3: Ja, u kunt de functies verkennen met de[gratis proefversie](https://releases.aspose.com/).

### V4: Kan ik een aangepast woordenboek uploaden voor spellingcontrole?

A4: Absoluut! De tutorial laat zien hoe u de correctie kunt verbeteren met behulp van een door de gebruiker aangeleverd woordenboek.

### V5: Waar kan ik ondersteuning zoeken voor Aspose.OCR?

 A5: Bezoek de[Aspose.OCR-forum](https://forum.aspose.com/c/ocr/16) voor gemeenschapsondersteuning en begeleiding.