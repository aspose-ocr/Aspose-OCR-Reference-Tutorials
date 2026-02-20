---
date: 2026-02-20
description: Leer hoe je tekst uit afbeeldingen kunt extraheren met Aspose.OCR voor
  Java, toegestane tekens kunt instellen en een tijdelijke licentie kunt toepassen
  – een volledige Aspose OCR Java‑tutorial.
linktitle: Specifying Allowed Characters in Aspose.OCR
second_title: Aspose.OCR Java API
title: Tekst extraheren uit afbeeldingen met Aspose.OCR – Toegestane tekens
url: /nl/java/advanced-ocr-techniques/specify-allowed-characters/
weight: 15
---

.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tekst uit afbeeldingen extraheren met Aspose.OCR – Toegestane tekens

## Inleiding

Het extraheren van tekst uit afbeeldingen is een veelvoorkomende vereiste in moderne applicaties—of je nu facturen verwerkt, bonnen scant of gedrukte documenten digitaliseert. In deze tutorial lopen we een volledige **aspose ocr java tutorial** door die laat zien hoe je **tekst uit afbeeldingen** kunt extraheren met Aspose.OCR voor Java, toegestane tekens kunt instellen en een tijdelijke licentie toepast wanneer je de bibliotheek alleen test.

## Snelle antwoorden
- **Wat doet Aspose.OCR?** Het extraheren van tekst uit afbeeldingen met hoge nauwkeurigheid en ondersteunt aangepaste tekenreeksen.  
- **Heb ik een licentie nodig?** Een tijdelijke of permanente licentie is vereist voor productiegebruik.  
- **Welke JDK‑versie wordt ondersteund?** De nieuwste JDK‑releases zijn volledig compatibel.  
- **Kan ik herkende tekens beperken?** Ja—gebruik de `setAllowedCharacters`‑API om de output te beperken.  
- **Hoe lang duurt de installatie?** Ongeveer 10‑15 minuten voor een basisimplementatie.

## Wat is “tekst uit afbeeldingen extraheren”?
Tekst uit afbeeldingen extraheren verwijst naar het proces waarbij visuele tekst (bijvoorbeeld gedrukt of handgeschreven) wordt omgezet in machinaal leesbare strings. Dit maakt downstream‑taken mogelijk zoals zoeken, indexeren of data‑analyse.

## Waarom Aspose.OCR voor Java gebruiken?
- **Hoge nauwkeurigheid** over meerdere talen en lettertypen.  
- **Eenvoudige API** die integreert met elk Java‑project.  
- **Aanpasbaar** tekenreeksen, taalpakketten en beeld‑preprocessing.  
- **Geen externe afhankelijkheden**—de bibliotheek is zelf‑voorzienend.

## Voorvereisten

Zorg ervoor dat je het volgende hebt voordat je begint:

### Java Development Kit (JDK)

Zorg ervoor dat je de nieuwste Java Development Kit op je systeem hebt geïnstalleerd. Je kunt deze downloaden van [hier](https://www.oracle.com/java/technologies/javase-downloads.html).

### Aspose.OCR for Java Library

Download en installeer de Aspose.OCR voor Java‑bibliotheek vanaf de [downloadlink](https://releases.aspose.com/ocr/java/).

### Aspose.OCR License

Om het volledige potentieel van Aspose.OCR te benutten, verkrijg je een geldige licentie. Je kunt er een krijgen via [hier](https://purchase.aspose.com/buy) of een [tijdelijke licentie](https://purchase.aspose.com/temporary-license/) verkennen voor een proefperiode.

## Hoe een tijdelijke licentie toe te passen

Wanneer je het product evalueert, verwijdert een tijdelijke licentie het evaluatiewatermerk en ontgrendelt volledige functionaliteit voor een beperkte periode. Maak de licentiestring aan in het Aspose‑portaal en geef deze door aan de `AsposeOCR`‑constructor zoals weergegeven in het code‑voorbeeld hieronder. Voor productie‑implementaties vervang je de tijdelijke sleutel door je permanente licentie.

## OCR‑beeld‑preprocessing tips

Goede beeldkwaliteit verbetert de herkenningsresultaten aanzienlijk. Overweeg vóór het aanroepen van de OCR‑engine:

- Het beeld omzetten naar grijstinten.
- Het contrast verhogen zodat tekens beter opvallen.
- Achtergrondruis verwijderen met een binarisatiefilter.
- Low‑resolution beelden schalen naar minimaal 300 dpi.

Deze stappen maken deel uit van **ocr image preprocessing** en kunnen met elke standaard Java‑beeldverwerkingsbibliotheek worden uitgevoerd vóór het aanroepen van Aspose.OCR.

## Importeer pakketten

Zodra de voorvereisten klaar zijn, importeer je de benodigde pakketten in je Java‑project:

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.examples.Utils;

import java.io.IOException;
```

## Stapsgewijze gids

### Stap 1: Stel je documentmap in

Definieer een map waarin je de OCR‑verwerkte resultaten opslaat. Dit pad wordt later gebruikt om het afbeeldingsbestand te vinden.

```java
String dataDir = "Your Document Directory";
```

### Stap 2: Specificeer het afbeeldingspad

Wijs de API naar de afbeelding die je wilt analyseren.

```java
String imagePath = dataDir + "0001460985.Jpeg";
```

### Stap 3: Maak een Aspose.OCR‑instantie

Instantieer de OCR‑engine met je licentiesleutel. De sleutel kan een tijdelijke of permanente licentiestring zijn.

```java
AsposeOCR api = new AsposeOCR("YourLicenseKey");
```

### Stap 4: Voer OCR‑herkenning uit

Roep de `RecognizeLine`‑methode aan om een regel tekst uit de afbeelding te extraheren. Het resultaat is een eenvoudige string die je verder kunt verwerken of opslaan.

```java
try {
    String result = api.RecognizeLine(imagePath);
    System.out.println("File: " + imagePath);
    System.out.println("Result line: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

> **Pro tip:** Als je de output wilt beperken tot een specifieke set tekens (bijv. alleen cijfers), gebruik dan de `setAllowedCharacters`‑methode op de `AsposeOCR`‑instantie vóór het aanroepen van `RecognizeLine`. Dit zorgt ervoor dat de engine tekens buiten de gedefinieerde set negeert.

## Veelvoorkomende problemen en oplossingen

| Probleem | Reden | Oplossing |
|----------|-------|-----------|
| **Geen output of lege string** | Onjuist afbeeldingspad of niet‑ondersteund afbeeldingsformaat | Controleer `imagePath` en gebruik een ondersteund formaat (JPEG, PNG, BMP) |
| **Herkenningsfouten** | Low‑resolution afbeelding of ruisrijke achtergrond | Pre‑process het beeld (contrast verhogen, binariseren) vóór OCR |
| **Licentie niet toegepast** | Ontbrekende of ongeldige licentiesleutel | Zorg ervoor dat de licentiestring correct is en geplaatst in de `AsposeOCR`‑constructor |

## Veelgestelde vragen

**Q: Hoe kan ik een tijdelijke licentie voor Aspose.OCR verkrijgen?**  
A: Bezoek de [tijdelijke licentiepagina](https://purchase.aspose.com/temporary-license/) om een proeflicentie aan te vragen.

**Q: Waar kan ik ondersteuning voor Aspose.OCR vinden?**  
A: Word lid van de community op het [Aspose.OCR‑forum](https://forum.aspose.com/c/ocr/16) voor hulp en discussies.

**Q: Kan ik toegestane tekens specificeren in Aspose.OCR?**  
A: Ja, je kunt de tekenreeks aanpassen met de `setAllowedCharacters`‑API. Raadpleeg de officiële documentatie voor details.

**Q: Is Aspose.OCR compatibel met de nieuwste JDK‑versies?**  
A: Absoluut—Aspose.OCR wordt regelmatig bijgewerkt om compatibel te blijven met de nieuwste Java‑releases.

**Q: Zijn er extra OCR‑functies naast regelherkenning?**  
A: Ja, de bibliotheek ondersteunt blok-, alinea- en volledige‑pagina‑herkenning, evenals taalpakketten en opties voor beeld‑preprocessing.

## Conclusie

Door deze **aspose ocr java tutorial** te volgen, heb je nu een werkende oplossing om **tekst uit afbeeldingen** te extraheren en te bepalen welke tekens worden herkend. Verken de volledige [documentatie](https://reference.aspose.com/ocr/java/) om geavanceerde functies te ontdekken, zoals ondersteuning voor meerdere talen, aangepaste preprocessing en batchverwerking.

---

**Last Updated:** 2026-02-20  
**Tested With:** Aspose.OCR for Java 24.11  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}