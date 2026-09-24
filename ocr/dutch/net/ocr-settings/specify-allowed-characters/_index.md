---
description: Leer hoe u toegestane tekens voor OCR kunt specificeren met Aspose.OCR
  voor .NET en cijfers in een afbeelding efficiënt kunt herkennen. Volg een stapsgewijze
  handleiding om OCR te beperken tot alleen cijfers.
linktitle: Specify Allowed Characters OCR – Using Aspose.OCR for .NET
second_title: Aspose.OCR .NET API
title: Specificeer toegestane tekens OCR – Gebruik Aspose.OCR voor .NET
url: /nl/net/ocr-settings/specify-allowed-characters/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Specificeer Toegestane Tekens OCR – Met Aspose.OCR voor .NET

In deze tutorial leer je hoe je **specify allowed characters ocr** kunt gebruiken met Aspose.OCR voor .NET, zodat je de OCR-uitvoer kunt beperken tot alleen de tekens die je nodig hebt. Dit is vooral handig wanneer je **recognize digits image**‑bestanden moet verwerken, zoals serienummers, factuur‑ID's of barcode‑achtige tekenreeksen. We lopen de installatie, code en een paar praktische scenario's door zodat je de techniek meteen kunt toepassen.

## Snelle Antwoorden
- **What does “specify allowed characters ocr” do?** Het beperkt OCR tot een vooraf gedefinieerde set tekens, waardoor de nauwkeurigheid voor gerichte gegevens verbetert.  
- **Which characters can I allow?** Elke combinatie die je nodig hebt—cijfers, letters of aangepaste symbolen (bijv. “0123456789”).  
- **Why limit characters?** Vermindert valse herkenningen en versnelt de verwerking wanneer de verwachte tekenreeks bekend is.  
- **Do I need a license?** Een gratis proefversie werkt voor ontwikkeling; een commerciële licentie is vereist voor productie.  
- **Which .NET versions are supported?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.

## Wat is “specify allowed characters ocr”?
Wanneer OCR een afbeelding scant, probeert het elk visueel patroon te matchen met het volledige alfabet van mogelijke tekens. Door **specify allowed characters ocr** te gebruiken, vertel je de engine alles buiten je whitelist te negeren, wat de herkenningsnauwkeurigheid voor beperkte datasets drastisch verbetert.

## Waarom Aspose.OCR gebruiken om digits image te herkennen?
Aspose.OCR biedt een schone, vloeiende API voor .NET‑ontwikkelaars. De ingebouwde `AllowedCharacters`‑optie stelt je in staat om je te concentreren op scenario's met alleen cijfers zonder aangepaste post‑processinglogica te schrijven. Dit is perfect voor:
- Het lezen van meterstanden, factuurnummers of productcodes.  
- Het valideren van door gebruikers ingevoerde gegevens die zijn vastgelegd van gescande formulieren.  
- Het versnellen van batchverwerking waarbij de tekenreeks van tevoren bekend is.

## Voorwaarden

Voordat je in de code duikt, zorg ervoor dat je het volgende hebt:

- Een werkende kennis van .NET‑ontwikkeling.  
- **Aspose.OCR for .NET**‑bibliotheek. Je kunt deze downloaden [hier](https://releases.aspose.com/ocr/net/).  
- Visual Studio (of een andere favoriete .NET‑IDE).  

## Namespaces importeren

Import in je .NET‑project de benodigde namespaces om de functionaliteit van Aspose.OCR te benutten:

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

Laten we nu de tutorial opsplitsen in een reeks uitgebreide stappen:

## Hoe specify allowed characters OCR – Stapsgewijze handleiding

### Stap 1: Stel het pad naar je afbeeldingsmap in

Definieer eerst waar je voorbeeldafbeeldingen zijn opgeslagen.

```csharp
string dataDir = "Your Document Directory";
```

### Stap 2: Initialise Aspose.OCR met een whitelist die alleen cijfers bevat

Maak een `AsposeOcr`‑instantie aan en geef de tekens door die je wilt toestaan — in dit geval alle cijfers.

```csharp
AsposeOcr api = new AsposeOcr("0123456789");
```

### Stap 3: Herken een enkele regel met cijfers

Gebruik de `RecognizeLine`‑methode om de tekst uit een afbeelding te halen die alleen cijfers bevat.

```csharp
string result = api.RecognizeLine(dataDir + "0001460985.Jpeg");
```

### Stap 4: Geef de herkende cijfers weer

Print het resultaat naar de console zodat je de uitvoer kunt verifiëren.

```csharp
Console.WriteLine(result);
```

### Stap 5: Gebruik RecognitionSettings voor meer controle

Als je fijnere controle nodig hebt — bijvoorbeeld het afdwingen van één‑regelige herkenning — kun je de overload gebruiken die `RecognitionSettings` accepteert.

```csharp
AsposeOcr api2 = new AsposeOcr();
RecognitionResult result2 = api2.RecognizeImage(dataDir + "0001460985.Jpeg", 
    new RecognitionSettings { 
        AllowedCharacters = CharactersAllowedType.DIGITS,
        RecognizeSingleLine = true
    });
```

### Stap 6: Toon het resultaat van het tweede geval

```csharp
Console.WriteLine(result2.RecognitionText);
```

### Stap 7: Bevestig succesvolle uitvoering

```csharp
Console.WriteLine("SpecifyAllowedCharacters executed successfully");
```

Door deze stappen te volgen, heb je geleerd hoe je **specify allowed characters ocr** kunt gebruiken en efficiënt **recognize digits image**‑inhoud kunt herkennen met Aspose.OCR voor .NET.

## Veelvoorkomende valkuilen en probleemoplossing
- **Empty result:** Zorg ervoor dat de beeldkwaliteit voldoende is (duidelijk contrast, minimale ruis).  
- **Wrong characters returned:** Controleer dubbel dat de whitelist‑string exact overeenkomt met de tekens die je verwacht.  
- **File not found:** Verifieer dat `dataDir` naar de juiste map wijst en dat de bestandsnaam hoofdlettergevoelig overeenkomt.

## Veelgestelde Vragen

### Q1: Is Aspose.OCR for .NET geschikt voor zowel beginners als ervaren ontwikkelaars?
**A:** Absoluut! De API is ontworpen om intuïtief te zijn voor nieuwkomers, terwijl het geavanceerde opties biedt voor power‑users.

### Q2: Kan ik Aspose.OCR for .NET gebruiken om tekens in meerdere talen te herkennen?
**A:** Ja, Aspose.OCR ondersteunt een breed scala aan talen. Je kunt taalpakketten combineren met de allowed‑characters‑functie voor meertalige scenario's.

### Q3: Hoe vaak wordt Aspose.OCR for .NET bijgewerkt?
**A:** Updates worden regelmatig uitgebracht om nieuwe functies toe te voegen, de nauwkeurigheid te verbeteren en compatibiliteit te waarborgen. Bekijk de [documentatie](https://reference.aspose.com/ocr/net/) voor de details van de nieuwste versie.

### Q4: Is er een gratis proefversie beschikbaar voor Aspose.OCR for .NET?
**A:** Ja, je kunt de mogelijkheden verkennen door de [gratis proefversie](https://releases.aspose.com/) te downloaden.

### Q5: Waar kan ik hulp zoeken of contact opnemen met de community voor ondersteuning?
**A:** Bezoek het [Aspose.OCR‑forum](https://forum.aspose.com/c/ocr/16) om vragen te stellen, ervaringen te delen en hulp te krijgen van zowel Aspose‑engineers als mede‑ontwikkelaars.

---

**Laatst bijgewerkt:** 2026-02-15  
**Getest met:** Aspose.OCR 24.11 for .NET  
**Auteur:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}