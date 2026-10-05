---
category: general
date: 2026-01-12
description: Tekst uit afbeelding extraheren met Aspose OCR in Java. Leer hoe je tekst
  uit een factuurafbeelding kunt extraheren met een Java OCR‑voorbeeld en verkrijg
  de OCR‑tekst als output.
draft: false
keywords:
- extract text from image
- how to extract text
- java ocr example
- process invoice image
- output ocr text
language: nl
og_description: Tekst extraheren uit afbeelding met Aspose OCR in Java. Deze gids
  toont hoe je tekst uit een factuurafbeelding kunt extraheren, bevat een Java OCR‑voorbeeld
  en geeft OCR‑tekst weer.
og_title: Tekst uit afbeelding extraheren in Java – Volledig OCR‑voorbeeld
tags:
- OCR
- Java
- Aspose
title: Tekst extraheren uit afbeelding in Java – Volledig OCR‑voorbeeld
url: /nl/java/ocr-basics/extract-text-from-image-in-java-complete-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tekst extraheren uit afbeelding in Java – Volledig OCR-voorbeeld

Heb je je ooit afgevraagd hoe je **tekst uit afbeelding** bestanden kunt extraheren zonder je haar uit je hoofd te trekken? Misschien heb je een stapel gescande facturen en heb je de cijfers snel nodig. Naar mijn ervaring is de eenvoudigste manier om een speciale OCR-bibliotheek het zware werk te laten doen. Deze tutorial laat *zien hoe je tekst* kunt extraheren uit een typische factuurafbeelding met Aspose OCR voor Java, en het demonstreert zelfs een **java ocr example** die de OCR-tekst uitvoert die je kunt doorsturen naar je downstream‑systeem.

We lopen alles door wat je moet weten: van het opzetten van het project, het definiëren van de region of interest (ROI) die zich richt op de koptekst en het totaalbedrag, tot het uiteindelijk afdrukken van de geëxtraheerde tekst. Aan het einde kun je **process invoice image** bestanden automatisch verwerken en schone, doorzoekbare tekst ophalen.

> **What you’ll get:** een kant‑klaar Java‑programma, duidelijke uitleg van elke stap, en praktische tips voor het omgaan met facturen uit de echte wereld.

---

## Vereisten

Before we dive in, make sure you have the following:

- Java Development Kit (JDK) 8 of nieuwer geïnstalleerd.
- Maven of Gradle voor afhankelijkheidsbeheer (Maven‑voorbeeld getoond).
- Een Aspose OCR for Java‑licentie (de gratis proefversie werkt voor testen).
- Een factuurafbeelding (`invoice.png`) geplaatst in een bekende map.

Als een van deze onbekend klinkt, geen zorgen—de meeste zijn slechts een download verwijderd, en de code zal nog steeds compileren met de community‑edition.

---

## Stap 1: Zet je Maven‑project op

Eerst, maak een nieuw Maven‑project (of voeg toe aan een bestaand project). In je `pom.xml`, voeg de Aspose OCR‑dependency toe:

```xml
<!-- pom.xml -->
<dependencies>
    <dependency>
        <groupId>com.aspose</groupId>
        <artifactId>aspose-ocr</artifactId>
        <version>23.9</version> <!-- Use the latest version available -->
    </dependency>
</dependencies>
```

> **Pro tip:** Houd het versienummer up‑to‑date; nieuwere releases verbeteren vaak de nauwkeurigheid voor lastige lettertypen die op facturen voorkomen.

Na het opslaan van het bestand, voer `mvn clean install` uit om de bibliotheek naar je lokale repository te halen.

---

## Stap 2: Laad de factuurafbeelding

Nu de bibliotheek klaar is, laten we een kleine Java‑klasse schrijven. Het eerste wat we doen is een `OcrEngine`‑instantie maken en deze wijzen op de afbeelding die je wilt lezen.

```java
import com.aspose.ocr.*;

public class RoiExample {
    public static void main(String[] args) throws Exception {
        // Step 2: Load the source image
        OcrEngine engine = new OcrEngine();
        engine.setImage("YOUR_DIRECTORY/invoice.png"); // <-- replace with your path
```

Waarom maken we de engine **voor** het laden van de afbeelding? De engine bevat configuratie zoals taal, DPI en ROI. Het vroeg instellen van de afbeelding zorgt ervoor dat die instellingen van toepassing zijn op het exacte bestand dat je gaat verwerken.

---

## Stap 3: Definieer Regions of Interest (ROI)

Facturen bevatten vaak veel ruis—tabellen, logo's en kleine lettertjes. Door de OCR te beperken tot alleen de koptekst en het totaalbedrag, verhoog je zowel snelheid als nauwkeurigheid aanzienlijk. Aspose laat je deze zones beschrijven met rechthoeken.

```java
        // Step 3: Define the regions of interest (header and total amount)
        OcrRegion region = OcrRegion.builder()
                .addRectangle(0, 0, 800, 150)      // header area
                .addRectangle(0, 1200, 800, 200)   // total amount area
                .build();

        // Apply ROI to the engine
        engine.setRegion(region);
```

De coördinaten zijn in pixels (`x`, `y`, `width`, `height`). Als je facturen in grootte variëren, kun je deze waarden dynamisch berekenen—misschien door eerst de afbeeldingsdimensies te controleren. Dat is een mooie uitbreiding als je een **process invoice image**‑oplossing nodig hebt die werkt op batches.

---

## Stap 4: Voer OCR uit op de gespecificeerde regio's

Met de ROI ingesteld, kan de OCR‑engine zijn aandacht richten waar het het meest telt. De `recognize()`‑methode retourneert een `OcrResult` met de geëxtraheerde tekst.

```java
        // Step 4: Run OCR on the specified regions
        OcrResult result = engine.recognize();
```

Achter de schermen voert Aspose verschillende preprocessing‑stappen uit: binarisatie, ruisverwijdering en karaktersegmentatie. Je hoeft die niet handmatig aan te roepen—laat `recognize()` gewoon zijn werk doen.

---

## Stap 5: Output de geëxtraheerde tekst

Tot slot printen we de tekst naar de console. In een echte applicatie kun je deze opslaan in een database, invoeren in een downstream‑analytics‑pipeline, of zelfs een doorzoekbare PDF genereren.

```java
        // Step 5: Output the extracted text
        System.out.println("ROI text:");
        System.out.println(result.getText());
    }
}
```

Wanneer je het programma uitvoert, zou je iets moeten zien als:

```
ROI text:
Acme Corp.
Invoice #12345
Date: 2025-12-31
Total Amount: $1,250.00
```

Als de output er onduidelijk uitziet, controleer dan de rechthoekcoördinaten opnieuw of verhoog de afbeeldingsresolutie. OCR‑engines houden van scherpe, hoge‑DPI‑scans.

---

## Volledig werkend voorbeeld

Hieronder staat het volledige, zelfstandige Java‑bestand dat je kunt kopiëren en plakken in `src/main/java/RoiExample.java`. Geen externe fragmenten nodig—alles wat je nodig hebt staat hier.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.region.*;

public class RoiExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create the OCR engine and load the source image
        OcrEngine engine = new OcrEngine();
        engine.setImage("YOUR_DIRECTORY/invoice.png");

        // Step 2: Define the regions of interest (header and total amount)
        OcrRegion region = OcrRegion.builder()
                .addRectangle(0, 0, 800, 150)      // header area
                .addRectangle(0, 1200, 800, 200)   // total amount area
                .build();

        // Step 3: Apply the ROI configuration to the engine
        engine.setRegion(region);

        // Step 4: Run OCR on the specified regions
        OcrResult result = engine.recognize();

        // Step 5: Output the extracted text
        System.out.println("ROI text:");
        System.out.println(result.getText());
    }
}
```

> **Note:** Vervang `YOUR_DIRECTORY` door het absolute pad naar je factuurafbeelding. Als je een relatief pad gebruikt, zorg er dan voor dat de werkdirectory overeenkomt met de locatie waar je het `java`‑commando uitvoert.

---

## Veelgestelde vragen & randgevallen

### Wat als de factuurgrootte verandert?

Je kunt ROI dynamisch berekenen:

```java
int imgWidth = engine.getImage().getWidth();
int imgHeight = engine.getImage().getHeight();

int headerHeight = imgHeight / 10;
int totalHeight = imgHeight / 8;

OcrRegion region = OcrRegion.builder()
        .addRectangle(0, 0, imgWidth, headerHeight)
        .addRectangle(0, imgHeight - totalHeight, imgWidth, totalHeight)
        .build();
```

### Hoe ga ik om met meerdere talen?

Aspose OCR ondersteunt taalpakketten. Stel gewoon de taal in voordat je `recognize()` aanroept:

```java
engine.setLanguage(OcrLanguage.Spanish); // or OcrLanguage.English, etc.
```

### Wat als de OCR lege strings retourneert?

Typische boosdoeners zijn:

- Lage afbeeldingsresolutie (< 300 DPI). Upscale of vraag om scans van hogere kwaliteit.
- Te donkere of te lichte achtergronden. Pas een eenvoudige contrast‑verbeteringsfilter toe vóór OCR.
- Onjuiste ROI‑coördinaten die de tekst volledig missen.

---

## Tips voor productie‑klare OCR

1. **Batchverwerking:** Plaats de logica in een lus die over een map met factuurbestanden itereren. Log elk resultaat voor auditabiliteit.
2. **Foutafhandeling:** Vang `OcrException` op om beschadigde afbeeldingen elegant over te slaan zonder de hele taak te stoppen.
3. **Prestaties:** Hergebruik een enkele `OcrEngine`‑instantie over meerdere afbeeldingen; een nieuwe engine per bestand creëert onnodige overhead.
4. **Validatie:** Na extractie, voer een regex‑check uit op het totaalbedrag (`\$\d{1,3}(,\d{3})*(\.\d{2})?`) om te verzekeren dat het getal realistisch lijkt.

Het implementeren van deze suggesties maakt van een eenvoudige **java ocr example** een robuuste, schaalbare oplossing voor elk bedrijf dat 's nachts **process invoice image** bestanden moet verwerken.

---

## Conclusie

We hebben zojuist behandeld hoe je **extract text from image** bestanden in Java kunt gebruiken met Aspose OCR, met focus op een praktisch factuur‑verwerkingssituatie. Door een region of interest te definiëren, de OCR‑engine uit te voeren en de **output OCR text** af te drukken, heb je nu een solide basis voor het bouwen van geautomatiseerde data‑capture‑pijplijnen.

Volgende stappen? Probeer de ROI uit te breiden om regel‑item tabellen op te nemen, experimenteer met verschillende taalinstellingen, of voer de geëxtraheerde strings in een PDF‑generatie‑bibliotheek voor doorzoekbare documenten. De mogelijkheden zijn eindeloos wanneer je OCR combineert met moderne Java‑tools.

Heb je meer vragen over **how to extract text** uit andere documenttypen, of heb je hulp nodig bij het afstemmen van de ROI voor ongebruikelijke lay-outs? Laat een reactie achter—veel plezier met coderen!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}