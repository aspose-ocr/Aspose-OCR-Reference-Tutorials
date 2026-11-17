---
date: 2026-05-24
description: Ontdek hoe u OCR met Aspose.OCR voor Java kunt gebruiken, tekst uit afbeeldingen
  kunt extraheren, toegestane tekens kunt instellen en binnen enkele minuten een tijdelijke
  licentie toepast.
keywords:
- how to use OCR
- extract text from images
- how to apply license
- how to set characters
linktitle: Toegestane tekens specificeren in Aspose.OCR
schemas:
- author: Aspose
  dateModified: '2026-05-24'
  description: Discover how to use OCR with Aspose.OCR for Java, extract text from
    images, set allowed characters, and apply a temporary license in minutes.
  headline: How to Use OCR – Extract Text from Images with Aspose.OCR
  type: TechArticle
- description: Discover how to use OCR with Aspose.OCR for Java, extract text from
    images, set allowed characters, and apply a temporary license in minutes.
  name: How to Use OCR – Extract Text from Images with Aspose.OCR
  steps:
  - name: Set Your Document Directory
    text: Choose a folder where OCR results and temporary files will be stored. This
      path is later used to locate the image you want to process.
  - name: Specify the Image Path
    text: Provide the full file system path or a class‑path resource location that
      points to the image you wish to analyse.
  - name: Create an Aspose.OCR Instance
    text: '`AsposeOCR` is the core engine that performs optical character recognition.
      Instantiate it with either a temporary or permanent license string.'
  - name: Perform OCR Recognition
    text: '`RecognizeLine` extracts a single line of text from the supplied image
      and returns it as a plain Java `String`. You can call this method repeatedly
      for multi‑line documents. > **Pro tip:** If you need to restrict the output
      to digits only (e.g., for invoice numbers), call `setAllowedCharacters("0123'
  type: HowTo
- questions:
  - answer: Visit the [temporary license page](https://purchase.aspose.com/temporary-license/)
      to request a trial key that removes evaluation watermarks.
    question: How can I obtain a temporary license for Aspose.OCR?
  - answer: Join the community at the [Aspose.OCR Forum](https://forum.aspose.com/c/ocr/16)
      for help and discussions.
    question: Where can I find support for Aspose.OCR?
  - answer: Yes, use the `setAllowedCharacters` API to define a custom whitelist of
      characters. This is ideal for numeric‑only fields.
    question: Can I specify allowed characters in Aspose.OCR?
  - answer: Absolutely—Aspose.OCR is regularly updated to stay compatible with the
      newest Java releases.
    question: Is Aspose.OCR compatible with the latest JDK versions?
  - answer: The library also supports block, paragraph, and full‑page recognition,
      language packs, and advanced image preprocessing.
    question: Are there additional OCR features beyond line recognition?
  type: FAQPage
second_title: Aspose.OCR Java API
title: Hoe OCR te gebruiken – Tekst extraheren uit afbeeldingen met Aspose.OCR
url: /nl/java/advanced-ocr-techniques/specify-allowed-characters/
weight: 15
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe OCR te gebruiken – Tekst extraheren uit afbeeldingen met Aspose.OCR

In moderne Java‑toepassingen is **hoe OCR te gebruiken** een veelgestelde vraag, vooral wanneer je gescande facturen, bonnetjes of afgedrukte formulieren wilt omzetten naar doorzoekbare tekst. Deze tutorial leidt je door een compleet **Aspose.OCR for Java**‑voorbeeld: tekst extraheren uit afbeeldingen, de uitvoer beperken tot een aangepaste tekenset, en een tijdelijke licentie toepassen voor snelle evaluatie.

## Snelle antwoorden
- **Wat doet Aspose.OCR?** Het extrahert tekst uit afbeeldingen met hoge nauwkeurigheid en laat je herkende tekens beperken.  
- **Heb ik een licentie nodig?** Een tijdelijke of permanente licentie is vereist voor productiegebruik; de tijdelijke sleutel verwijdert watermerken.  
- **Welke JDK‑versie wordt ondersteund?** De bibliotheek werkt met de nieuwste JDK‑releases (JDK 17, 19, 21).  
- **Kan ik herkende tekens beperken?** Ja—gebruik de `setAllowedCharacters`‑methode om de uitvoer te beperken.  
- **Hoe lang duurt de installatie?** Ongeveer 10‑15 minuten voor een basis‑end‑to‑end‑implementatie.

## Wat betekent “tekst extraheren uit afbeeldingen”?
Tekst extraheren uit afbeeldingen, ook wel optische tekenherkenning (OCR) genoemd, zet visuele tekens—of ze nu gedrukt, handgeschreven of getypt zijn—om in machine‑leesbare strings. Deze transformatie maakt het mogelijk om applicaties te laten zoeken, indexeren, bewerken en analyseren, wat workflows ondersteunt zoals factuurverwerking, documentarchivering en geautomatiseerde gegevensinvoer.

## Waarom Aspose.OCR voor Java gebruiken?
Aspose.OCR ondersteunt **60+ talen**, kan afbeeldingen tot **10 MB** verwerken zonder het volledige bestand in het geheugen te laden, en levert **>95 % nauwkeurigheid** op schone scans. De bibliotheek is zelf‑voorzienend, vereist geen externe OCR‑engines, wat implementatie vereenvoudigt en licentiekosten verlaagt.

## Vereisten

### Java Development Kit (JDK)

Zorg ervoor dat je de nieuwste Java Development Kit geïnstalleerd hebt. Je kunt deze downloaden via [hier](https://www.oracle.com/java/technologies/javase-downloads.html).

### Aspose.OCR for Java Library

Download en installeer de Aspose.OCR for Java‑bibliotheek vanaf de [downloadlink](https://releases.aspose.com/ocr/java/).

### Aspose.OCR License

Om de volledige functionaliteit te ontgrendelen, verkrijg je een licentie. Je kunt er een kopen via [hier](https://purchase.aspose.com/buy) of een [tijdelijke licentie](https://purchase.aspose.com/temporary-license/) aanvragen voor proefdoeleinden.

## Hoe OCR te gebruiken met Aspose.OCR for Java?

Laad je afbeelding, configureer de OCR‑engine en roep de herkenningsmethode aan—alles in een paar eenvoudige regels. Deze directe‑antwoord‑paragraaf vertelt je precies wat je moet doen: maak een `AsposeOCR`‑instantie met je licentiestring, stel eventuele toegestane tekens in, en roep `RecognizeLine` aan op de doelafbeelding om de geëxtraheerde tekst te ontvangen. De API verwerkt intern beeldvoorbewerking, zodat je schone resultaten krijgt zonder extra code.

### Import Packages

De `AsposeOCR`‑klasse bevindt zich in het `com.aspose.ocr`‑pakket. Importeer de benodigde klassen voordat je begint met coderen.

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.examples.Utils;

import java.io.IOException;
```

## Stapsgewijze handleiding

### Stap 1: Stel je documentmap in

Kies een map waarin OCR‑resultaten en tijdelijke bestanden worden opgeslagen. Dit pad wordt later gebruikt om de afbeelding te vinden die je wilt verwerken.

```java
String dataDir = "Your Document Directory";
```

### Stap 2: Specificeer het afbeeldingspad

Geef het volledige bestandssysteem‑pad of een class‑path‑resource‑locatie op die naar de afbeelding wijst die je wilt analyseren.

```java
String imagePath = dataDir + "0001460985.Jpeg";
```

### Stap 3: Maak een Aspose.OCR‑instantie

`AsposeOCR` is de kernengine die optische tekenherkenning uitvoert. Instantieer deze met een tijdelijke of permanente licentiestring.

```java
AsposeOCR api = new AsposeOCR("YourLicenseKey");
```

### Stap 4: Voer OCR‑herkenning uit

`RecognizeLine` extrahert een enkele regel tekst uit de opgegeven afbeelding en retourneert deze als een gewone Java `String`. Je kunt deze methode herhaaldelijk aanroepen voor documenten met meerdere regels.

```java
try {
    String result = api.RecognizeLine(imagePath);
    System.out.println("File: " + imagePath);
    System.out.println("Result line: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

> **Pro tip:** Als je de uitvoer wilt beperken tot alleen cijfers (bijvoorbeeld voor factuurnummers), roep dan `setAllowedCharacters("0123456789")` aan op de `AsposeOCR`‑instantie voordat je `RecognizeLine` aanroept. Dit dwingt de engine om alle niet‑numerieke symbolen te negeren.  
> `setAllowedCharacters` is een methode van `AsposeOCR` die de OCR‑uitvoer beperkt tot een opgegeven whitelist van tekens.

## Veelvoorkomende problemen en oplossingen

| Probleem | Reden | Oplossing |
|----------|-------|-----------|
| **Geen uitvoer of lege string** | Onjuist afbeeldingspad of niet‑ondersteund formaat | Controleer `imagePath` en gebruik een ondersteund formaat (JPEG, PNG, BMP) |
| **Herkenningsfouten** | Lage resolutie of ruisachtige achtergrond | Pre‑process de afbeelding (verhoog contrast, binariseer) vóór OCR |
| **Licentie niet toegepast** | Ontbrekende of ongeldige licentiesleutel | Zorg dat de licentiestring correct is en wordt doorgegeven aan de `AsposeOCR`‑constructor |

## Veelgestelde vragen

**V: Hoe kan ik een tijdelijke licentie voor Aspose.OCR verkrijgen?**  
A: Bezoek de [pagina voor tijdelijke licenties](https://purchase.aspose.com/temporary-license/) om een proef‑sleutel aan te vragen die evaluatiewatermerken verwijdert.

**V: Waar vind ik ondersteuning voor Aspose.OCR?**  
A: Word lid van de community op het [Aspose.OCR‑forum](https://forum.aspose.com/c/ocr/16) voor hulp en discussies.

**V: Kan ik toegestane tekens specificeren in Aspose.OCR?**  
A: Ja, gebruik de `setAllowedCharacters`‑API om een aangepaste whitelist van tekens te definiëren. Ideaal voor velden die alleen numeriek zijn.

**V: Is Aspose.OCR compatibel met de nieuwste JDK‑versies?**  
A: Absoluut—Aspose.OCR wordt regelmatig bijgewerkt om compatibel te blijven met de nieuwste Java‑releases.

**V: Zijn er extra OCR‑functies naast regelherkenning?**  
A: De bibliotheek ondersteunt ook blok‑, alinea‑ en volledige‑pagina‑herkenning, taalpakketten en geavanceerde beeldvoorbewerking.

## Conclusie

Door deze **Aspose OCR Java‑tutorial** te volgen, weet je nu **hoe OCR te gebruiken** om tekst uit afbeeldingen te extraheren, de tekenset te beperken en een tijdelijke licentie toe te passen voor snelle tests. Duik dieper in de volledige [documentatie](https://reference.aspose.com/ocr/java/) om meer‑taalondersteuning, batchverwerking en aangepaste voorbewerkings‑pipelines te ontdekken.

---

**Laatst bijgewerkt:** 2026-05-24  
**Getest met:** Aspose.OCR for Java 24.11  
**Auteur:** Aspose  

{{< blocks/products/products-backtop-button >}}

## Gerelateerde tutorials

- [Hoe licentie instellen en Aspose.OCR‑licentie verifiëren in Java](/ocr/java/ocr-basics/set-license/)
- [Afbeelding naar tekst converteren in Java met Aspose.OCR BufferedImage](/ocr/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [Aspose OCR Java‑voorbeeld – Regels herkennen in afbeeldingen](/ocr/java/advanced-ocr-techniques/recognize-lines/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}