---
date: 2025-12-10
description: Leer hoe je tekst uit een afbeelding herkent en alinea's uit een afbeelding
  extraheert met Aspose.OCR voor Java. Stapsgewijze handleiding met codevoorbeelden.
linktitle: Recognize Text from Image and Retrieve Text Area Rectangles
second_title: Aspose.OCR Java API
title: Tekst herkennen uit afbeelding en rechthoeken van tekstgebieden ophalen
url: /nl/java/ocr-basics/get-rectangles-with-text-areas/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tekst herkennen uit afbeelding en tekstgebied rechthoeken ophalen

## Inleiding

Als je **tekst herkennen uit afbeelding** bestanden in een Java‑applicatie moet doen, biedt Aspose.OCR voor Java een snelle, nauwkeurige manier om dit te realiseren. In deze tutorial lopen we stap voor stap door de exacte handelingen die nodig zijn om alinea’s uit een afbeelding te extraheren, de begrenzende rechthoeken voor elk tekstgebied te verkrijgen, en die coördinaten naar de console te printen. Aan het einde begrijp je waarom deze aanpak werkt, hoe je de bibliotheek integreert, en waar je deze kunt uitbreiden voor je eigen use‑cases.

## Snelle antwoorden
- **Wat betekent “tekst herkennen uit afbeelding”?** Het betekent het omzetten van visuele tekens in een afbeelding naar bewerkbare tekenreeksgegevens.  
- **Welke bibliotheek behandelt dit in Java?** Aspose.OCR voor Java.  
- **Heb ik een licentie nodig voor ontwikkeling?** Een tijdelijke licentie is beschikbaar voor testen; een volledige licentie is vereist voor productie.  
- **Kan ik alinea’s extraheren in plaats van losse woorden?** Ja – gebruik `AreasType.PARAGRAPHS` om alinea‑niveau rechthoeken te krijgen.  
- **Is de code compatibel met Java 11+?** Absoluut, de API werkt met Java 11 en later.

## Wat is “tekst herkennen uit afbeelding” in Aspose.OCR?
De `RecognizePage`‑methode van Aspose.OCR analyseert de bitmap, past OCR‑algoritmen toe, en retourneert de herkende tekenreeks. Wanneer je tekstgebieden opvraagt, berekent de bibliotheek ook de exacte `Rectangle`‑coördinaten voor elk tekstblok, waardoor het eenvoudig is om later specifieke secties te markeren of te verwerken.

## Waarom Aspose.OCR voor Java gebruiken?
- **Hoge nauwkeurigheid** – ondersteunt meerdere talen en complexe lettertypen.  
- **Eenvoudige integratie** – één JAR voegt volledige OCR‑functionaliteit toe.  
- **Flexibele output** – je kunt ruwe tekst, opgemaakte HTML, of precieze tekst‑gebied rechthoeken ophalen.  
- **Thread‑safe** – geschikt voor high‑throughput serveromgevingen.

## Vereisten

- **Java Development Kit** (JDK 11 of nieuwer) geïnstalleerd op je machine.  
- **Aspose.OCR voor Java** bibliotheek – download deze van de officiële site [hier](https://releases.aspose.com/ocr/java/).  
- Een IDE of build‑tool (Maven/Gradle) om de JAR‑dependency te beheren.

## Importeer pakketten

Importeer in je Java‑project de benodigde klassen:

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AreasType;
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

## Stapsgewijze handleiding

### Stap 1: Stel uw project in
Maak een nieuw Java‑project (of voeg toe aan een bestaand project) en plaats de Aspose.OCR‑JAR op de classpath. Als je Maven gebruikt, voeg je de dependency toe zoals beschreven in het download‑pakket.

### Stap 2: Definieer documentmap en afbeeldingspad
Geef aan waar je voorbeeldafbeelding zich bevindt:

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";

// The image path
String imagePath = dataDir + "p3.png";
```

### Stap 3: Maak een Aspose.OCR‑instantie
Instantieer de OCR‑engine:

```java
// Create Aspose.OCR instance
AsposeOCR api = new AsposeOCR();
```

### Stap 4: Tekst herkennen in de afbeelding
Roep `RecognizePage` aan om de afbeelding om te zetten naar platte tekst. Deze stap demonstreert de kernfunctionaliteit **tekst herkennen uit afbeelding**:

```java
try {
    // Recognize page by full path to file
    String result = api.RecognizePage(imagePath);
    System.out.println("Result: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

### Stap 5: Verkrijg rechthoeken met tekstgebieden
Haal nu de begrenzende rechthoeken op voor elke alinea (of andere gebiedstypen). Dit is waar je **alinea’s uit afbeelding** extraheert en hun coördinaten verkrijgt:

```java
// Get rectangles with text areas in the image.
ArrayList<Rectangle> rectResult = api.getTextAreas(imagePath, AreasType.PARAGRAPHS, true);

// Print each text area rectangle
for (Rectangle r : rectResult) {
    System.out.println("Text area:" + r);
}
```

## Veelvoorkomende problemen & probleemoplossing

| Symptom | Likely Cause | Fix |
|---------|--------------|-----|
| `IOException` on `RecognizePage` | Onjuist bestandspad of ontbrekende leesrechten | Controleer of `imagePath` verwijst naar een bestaande PNG/JPG en dat de app toegang heeft tot het bestandssysteem. |
| Empty result string | Lage kwaliteit van de afbeelding of niet‑ondersteunde taal | Pre‑process de afbeelding (verhoog contrast, binariseer) of specificeer de juiste taal met `api.setLanguage("eng")`. |
| No rectangles returned | Verkeerd `AreasType` gebruikt (bijv. `WORDS` terwijl alinea’s verwacht worden) | Schakel over naar `AreasType.PARAGRAPHS` of `AreasType.LINES` indien nodig. |

## Veelgestelde vragen

**Q: Is Aspose.OCR compatibel met Java 11?**  
A: Ja, Aspose.OCR werkt met Java 11 en latere versies.

**Q: Kan ik Aspose.OCR gebruiken voor zowel persoonlijke als commerciële projecten?**  
A: Ja, je kunt het in elk type project gebruiken. Voor licentie‑details, bezoek [hier](https://purchase.aspose.com/buy).

**Q: Hoe verkrijg ik een tijdelijke licentie voor evaluatie?**  
A: Je kunt een tijdelijke licentie verkrijgen [hier](https://purchase.aspose.com/temporary-license/).

**Q: Waar vind ik community‑ondersteuning of officiële assistentie?**  
A: Voor ondersteuning en discussies, bezoek het [Aspose.OCR‑forum](https://forum.aspose.com/c/ocr/16).

**Q: Ondersteunt Aspose.OCR multithreading?**  
A: Ja, de bibliotheek is thread‑safe en kan in gelijktijdige omgevingen worden gebruikt voor betere prestaties.

## Conclusie

In deze tutorial heb je geleerd hoe je **tekst herkennen uit afbeelding** bestanden kunt uitvoeren met Aspose.OCR voor Java, alinea’s kunt extraheren, en de exacte rechthoeken die elk tekstblok omringen kunt ophalen. Deze mogelijkheden stellen je in staat om doorzoekbare PDF’s te bouwen, tekst te markeren in UI‑overlays, of gestructureerde data aan downstream‑processen te leveren. Verken de API verder om taalinstellingen aan te passen, verschillende afbeeldingsformaten te verwerken, of integratie met cloud‑opslag te realiseren.

---

**Last Updated:** 2025-12-10  
**Tested With:** Aspose.OCR 23.10 for Java  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}