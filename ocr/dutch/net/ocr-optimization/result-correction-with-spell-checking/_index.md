---
date: 2025-12-25
description: Verbeter de OCR‑nauwkeurigheid met Aspose OCR voor .NET, maak gebruik
  van spellingscontrole en taalondersteuning om spelfouten te corrigeren en pas woordenboeken
  aan voor foutloze teksterkenning.
linktitle: Improve OCR Accuracy with Spell Checking in Images
second_title: Aspose.OCR .NET API
title: Verbeter OCR-nauwkeurigheid met spellingscontrole in afbeeldingen
url: /nl/net/ocr-optimization/result-correction-with-spell-checking/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Verbeter OCR-nauwkeurigheid met spellingscontrole in afbeeldingen

## Inleiding

Wanneer je werkt met Optical Character Recognition (OCR), is het uiteindelijke doel om **OCR-nauwkeurigheid te verbeteren** zodat de geëxtraheerde tekst perfect overeenkomt met de oorspronkelijke afbeelding. Fout gespelde woorden zijn een veelvoorkomende bron van fouten, vooral wanneer de bronafbeelding ruis bevat of ongebruikelijke lettertypen heeft. Aspose.OCR voor .NET biedt ingebouwde spellingscontrole‑functionaliteit die niet alleen die fouten corrigeert, maar je ook in staat stelt de engine uit te breiden met aangepaste woordenboeken. In deze tutorial leer je hoe je spellingscontrole gebruikt om OCR‑resultaten te verbeteren, zie je de voor‑en‑na‑output, en ontdek je hoe je het correctieproces kunt afstemmen op jouw specifieke taalbehoeften.

## Snelle antwoorden
- **Wat doet spellingscontrole voor OCR?** Het detecteert automatisch fout gespelde woorden in de OCR‑output en vervangt ze door de meest waarschijnlijke correcte alternatieven.  
- **Welke bibliotheek biedt deze functie?** Aspose.OCR voor .NET bevat een kant‑en‑klare spellingscontrole‑API.  
- **Heb ik een internetverbinding nodig?** Nee, de spellingscontrole‑engine werkt volledig offline.  
- **Kan ik mijn eigen terminologie toevoegen?** Ja, je kunt een aangepast gebruikerswoordenboek leveren om domeinspecifieke woorden af te handelen.  
- **Welke talen worden ondersteund?** Zie de sectie “aspose ocr language support” voor details.

## Wat is spellingscontrole in OCR?

Spellingscontrole onderzoekt de ruwe tekst die door de OCR‑engine wordt geretourneerd, identificeert tokens die niet overeenkomen met bekende woorden in het geselecteerde taaldictionary, en stelt correcties voor of past ze toe. Deze stap is essentieel om **OCR-nauwkeurigheid te verbeteren**, vooral bij het verwerken van gescande documenten, bonnen of formulieren waar OCR tekens kan misinterpreteren.

## Waarom Aspose OCR Language Support gebruiken?

Aspose.OCR wordt geleverd met uitgebreide taalpakketten en stelt je in staat extra woordenboeken toe te voegen. Het benutten van **aspose ocr language support** betekent dat je meertalige documenten kunt afhandelen zonder eigen parsers te schrijven, en je krijgt toegang tot taalspecifieke regels die de herkenningskwaliteit verder verbeteren.

## Voorvereisten

Voordat we de magie van spellingscontrole induiken, zorg ervoor dat je de volgende zaken klaar hebt staan:

- Aspose.OCR voor .NET Bibliotheek: Download en installeer de Aspose.OCR‑bibliotheek vanaf de [release page](https://releases.aspose.com/ocr/net/).

- Documentenmap: Zorg voor een aangewezen map voor je documenten. Vervang `"Your Document Directory"` in de code‑fragmenten door het daadwerkelijke pad.

## Namespaces importeren

Laten we beginnen met het importeren van de benodigde namespaces in je .NET‑project:

```csharp
using System;
using Aspose.OCR.SpellChecker;
using System.Collections.Generic;
```

## Stap 1: Aspose.OCR initialiseren

Initialiseer een instantie van Aspose.OCR om het OCR‑proces te starten.

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Stap 2: Afbeelding herkennen

Herken vervolgens de tekst in een afbeelding met Aspose.OCR. Hieronder vind je een fragment dat dit proces demonstreert:

```csharp
// Recognize image
RecognitionResult result = api.RecognizeImage(dataDir + "sample_bad.png", new RecognitionSettings(Language.Eng));
```

## Stap 3: Voor correctie

Haal het OCR‑resultaat op vóór correctie om te vergelijken met de gecorrigeerde versie.

```csharp
// Get result
Console.WriteLine("BEFORE CORRECTION:\n" + result.RecognitionText);
```

## Stap 4: Na correctie

Pas spellingscontrole toe om het gecorrigeerde resultaat te krijgen. Het volgende code‑fragment illustreert deze stap:

```csharp
// Get corrected result
string correctedResult = result.GetSpellCheckCorrectedText(SpellCheckLanguage.Eng);
Console.WriteLine("AFTER CORRECTION:\n" + correctedResult);
```

## Stap 5: Fout gespelde woorden en suggesties

Verkrijg een lijst met fout gespelde woorden en de voorgestelde correcties met de volgende code:

```csharp
// Get list of misspelled words with suggestions
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

## Stap 6: Gebruikerstekst corrigeren

Corrigeer specifieke door de gebruiker geleverde tekst met de Aspose.OCR‑bibliotheek:

```csharp
// Correct user text
Console.WriteLine("recogniition -> " + api.CorrectSpelling("recogniition"));
```

## Stap 7: Correctie met gebruikerswoordenboek

Verbeter de correctie verder door een aangepast gebruikerswoordenboek te integreren:

```csharp
// Get corrected result with user dictionary
string correctedResultUserDict = result.GetSpellCheckCorrectedText(SpellCheckLanguage.Eng, dataDir+"dictionary.txt");
Console.WriteLine("AFTER CORRECTION WITH USER DICTIONARY:\n" + correctedResultUserDict);
```

## Veelvoorkomende problemen en oplossingen

| Probleem | Waarom het gebeurt | Hoe op te lossen |
|----------|--------------------|------------------|
| Geen suggesties teruggegeven | Het taalpakket is niet geladen of de tekst is te kort. | Zorg ervoor dat `RecognitionSettings(Language.Eng)` overeenkomt met de taal van de bronafbeelding en dat het OCR‑resultaat voldoende tekens bevat. |
| Aangepast woordenboek niet toegepast | Onjuist pad of bestandsformaat. | Controleer of `dictionary.txt` bestaat op de opgegeven locatie en één woord per regel gebruikt. |
| Spellingscontrole vertraagt bij grote documenten | Het verwerken van elk woord afzonderlijk veroorzaakt extra overhead. | Verwerk pagina's in batches of vergroot de geheugenallocatie bij .NET Core. |

## Veelgestelde vragen

### Q1: Kan ik Aspose.OCR gebruiken voor andere talen dan Engels?

A1: Ja, Aspose.OCR ondersteunt meerdere talen. Pas de taalinstellingen dienovereenkomstig aan.

### Q2: Hoe integreer ik Aspose.OCR in mijn .NET‑project?

A2: Zie de [documentatie](https://reference.aspose.com/ocr/net/) voor gedetailleerde integratiestappen.

### Q3: Is er een proefversie beschikbaar voor Aspose.OCR?

A3: Ja, je kunt de functies verkennen met de [gratis proefversie](https://releases.aspose.com/).

### Q4: Kan ik een aangepast woordenboek uploaden voor spellingscontrole?

A4: Absoluut! De tutorial laat zien hoe je correctie kunt verbeteren met een door de gebruiker geleverd woordenboek.

### Q5: Waar kan ik ondersteuning vinden voor Aspose.OCR?

A5: Bezoek het [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16) voor community‑ondersteuning en begeleiding.

---

**Laatst bijgewerkt:** 2025-12-25  
**Getest met:** Aspose.OCR voor .NET latest version  
**Auteur:** Aspose

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
