---
date: 2026-04-12
description: Leer hoe u tekstextractie uit afbeeldingen vanuit streams kunt uitvoeren
  met Aspose OCR voor .NET. Dit stapsgewijze voorbeeld toont eenvoudige OCR-tekstextractie.
keywords:
- image text extraction
- image to memorystream
- ocr png file
- image stream ocr
- read image stream c#
linktitle: Herken afbeelding vanuit stream in OCR‑afbeeldingsherkenning
second_title: Aspose.OCR .NET API
title: Hoe tekst uit een afbeelding extraheren uit een stream met Aspose OCR
url: /nl/net/image-and-drawing-recognition/recognize-image-from-stream/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe voer je afbeeldingstekstextractie uit vanuit een stream met Aspose OCR

Welkom in de wereld van **image text extraction** met **Aspose.OCR for .NET**. In deze tutorial zie je hoe je een afbeeldingstream leest, OCR uitvoert op een PNG‑bestand en de herkende tekst in je C#‑applicatie haalt. Of je nu een documentverwerkings‑pipeline bouwt, een data‑invoerautomatiseringstool, of gewoon met OCR experimenteert, de onderstaande stappen brengen je in enkele minuten van een ruwe afbeelding naar doorzoekbare tekst.

## Snelle antwoorden
- **Wat laat deze tutorial zien?** Tekst extraheren uit een afbeelding die als stream wordt aangeleverd met Aspose OCR.  
- **Welk primair trefwoord is gericht?** *image text extraction* (door de hele gids gebruikt).  
- **Heb ik een licentie nodig voor ontwikkeling?** Een gratis proefversie werkt voor testen; een commerciële licentie is vereist voor productiegebruik.  
- **Kan ik PNG‑bestanden direct verwerken?** Ja – Aspose OCR verwerkt **ocr png file**‑formaten zonder extra conversie.  
- **Welke .NET‑versies worden ondersteund?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.

## Wat is afbeeldingstekstextractie?
Afbeeldingstekstextractie (ook wel OCR genoemd) zet de visuele tekens in een afbeelding om in bewerkbare, doorzoekbare tekst. Met Aspose OCR kun je een `MemoryStream` met een ondersteunde afbeelding (PNG, JPEG, BMP, enz.) voeden en de herkende tekenreeks in één oproep ontvangen.

## Waarom Aspose OCR kiezen voor afbeeldingstekstextractie?
- **Brede taalondersteuning** – werkt direct met tientallen talen.  
- **Eenvoudige API** – een paar regels C# veranderen een **image to memorystream** in leesbare tekst.  
- **Hoge nauwkeurigheid** – geavanceerde algoritmen verwerken ruisende scans en PNG's met lage resolutie.  
- **Cross‑platform** – draait op Windows, Linux en macOS met .NET Core.

## Voorwaarden

Voordat we beginnen, zorg ervoor dat je het volgende hebt:

- Aspose.OCR for .NET geïnstalleerd (download van de [Aspose.OCR for .NET Documentation](https://reference.aspose.com/ocr/net/)).  
- Een voorbeeldafbeeldingsbestand (bijv. **sample.png**) geplaatst in een map die je vanuit code kunt refereren.

## Namespaces importeren

Voeg de vereiste namespaces toe aan je C#‑bestand:

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

## Stapsgewijze handleiding

### Stap 1: Stel de documentdirectory in
```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";
```
Vervang **"Your Document Directory"** door de daadwerkelijke map die *sample.png* bevat.

### Stap 2: Initialiseert de Aspose OCR‑engine
```csharp
// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```
Het aanmaken van een `AsposeOcr`‑object geeft je toegang tot alle OCR‑methoden.

### Stap 3: Lees afbeeldingstream en herken tekst
```csharp
// Recognize image
using (MemoryStream ms = new MemoryStream())
using (FileStream file = new FileStream(dataDir + "sample.png", FileMode.Open, FileAccess.Read))
{
    file.CopyTo(ms);
    result = api.RecognizeImage(ms);
}
```
Hier openen we **sample.png**, kopiëren we de bytes naar een `MemoryStream` en geven we die stream door aan `RecognizeImage`. Dit demonstreert **image stream ocr** en het **read image stream c#**‑patroon in één doorloop.

### Stap 4: Toon de herkende tekst
```csharp
// Display the recognized text
Console.WriteLine(result);
```
Het OCR‑resultaat wordt naar de console geprint; je kunt het ook opslaan in een database of bestand.

### Stap 5: Bevestig succesvolle uitvoering
```csharp
Console.WriteLine("RecognizeImageFromStream executed successfully");
```
Een eenvoudige bevestiging laat je weten dat het proces zonder uitzonderingen is voltooid.

## Veelvoorkomende problemen en oplossingen

| Probleem | Oplossing |
|----------|-----------|
| *Result is empty* | Controleer het afbeeldingspad, zorg dat het bestand leesbaar is, en bevestig dat de afbeelding duidelijke, hoog‑contrast tekst bevat. |
| *Unsupported image format* | Converteer de bron naar PNG of JPEG voordat je `RecognizeImage` aanroept. |
| *License exception* | Pas een tijdelijke licentie toe tijdens ontwikkeling of koop een volledige licentie voor productie (zie hieronder). |

## Veelgestelde vragen

**V: Kan Aspose.OCR meerdere talen verwerken?**  
**A:** Ja, Aspose.OCR ondersteunt een breed scala aan talen, waardoor het geschikt is voor wereldwijde OCR‑projecten.

**V: Is er een proefversie die ik kan gebruiken?**  
**A:** Absoluut! Je kunt Aspose.OCR voor .NET verkennen met een gratis proefversie [hier](https://releases.aspose.com/).

**V: Waar kan ik hulp krijgen als ik tegen problemen aanloop?**  
**A:** Bezoek het [Aspose.OCR Forum](https://forum.aspose.com/c/ocr/16) voor community‑ en expertsupport.

**V: Hoe krijg ik een tijdelijke licentie voor testen?**  
**A:** Een tijdelijke licentie is beschikbaar [hier](https://purchase.aspose.com/temporary-license/) voor evaluatiedoeleinden.

**V: Waar kan ik een permanente licentie kopen?**  
**A:** Om Aspose.OCR aan je productietoolkit toe te voegen, ga naar de [aankooppagina](https://purchase.aspose.com/buy).

## Conclusie

Je hebt nu **image text extraction** vanuit een stream onder de knie met Aspose OCR voor .NET. De beknopte API stelt je in staat elke ondersteunde afbeelding – zoals een **ocr png file** – om te zetten in doorzoekbare tekst met slechts een paar regels code. Experimenteer met verschillende afbeeldingsbronnen, taalpakketten en geavanceerde instellingen om de OCR‑output af te stemmen op jouw specifieke scenario.

---

**Laatst bijgewerkt:** 2026-04-12  
**Getest met:** Aspose.OCR 24.12 for .NET  
**Auteur:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}