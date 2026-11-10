---
category: general
date: 2026-06-22
description: 'Hoe een afbeelding te deskewen voor OCR: leer de stappen van beeldvoorverwerking
  voor OCR, verwijder zout‑peperruis en verhoog de nauwkeurigheid.'
draft: false
keywords:
- how to deskew image
- image preprocessing ocr
- remove salt pepper
- preprocess images OCR
language: nl
og_description: Hoe een afbeelding te deskewen voor OCR, zout‑en‑peper‑ruis te verwijderen
  en OCR‑preprocessortechnieken toe te passen in een compleet Java‑voorbeeld.
og_title: Hoe een afbeelding rechtzetten – Gids voor beeldvoorverwerking OCR
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: 'How to deskew image for OCR: learn image preprocessing OCR steps,
    remove salt pepper noise, and boost accuracy.'
  headline: How to Deskew Image – Image Preprocessing OCR Guide
  type: TechArticle
tags:
- OCR
- image-processing
- Java
title: Hoe een afbeelding rechtzetten – Gids voor beeldvoorbewerking bij OCR
url: /nl/java/ocr-operations/how-to-deskew-image-image-preprocessing-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe een afbeelding rechtzetten – Beeldvoorbewerking OCR-gids

Heb je je ooit afgevraagd **hoe je een afbeelding rechtzet** zodat je OCR-engine de tekst daadwerkelijk kan lezen? Je bent niet de enige. Een scheve scan kan een perfect document veranderen in een warboel, en de meeste ontwikkelaars lopen die hindernis minstens één keer tegen.

In deze tutorial lopen we een volledige **image preprocessing OCR**‑pipeline door die niet alleen rotatie corrigeert, maar ook **remove salt pepper**‑artefacten verwijdert en het contrast verhoogt – in feite alles wat je nodig hebt om **preprocess images OCR**‑stijl toe te passen voordat je ze aan de engine geeft. Aan het einde heb je een kant-en-klare Java‑snippet en een helder mentaal model van waarom elke stap belangrijk is.

## Hoe een afbeelding rechtzetten – De preprocessing‑pipeline bouwen

Het hart van elke OCR‑vriendelijke workflow is een **preprocess options**‑object dat een reeks filters aan elkaar koppelt. Zie het als een lopende band: elk filter voert één taak uit en geeft de afbeelding vervolgens door aan de volgende. Hieronder staat een minimaal maar volledig voorbeeld met een hypothetische OCR‑bibliotheek die `DeskewFilter`, `DenoiseFilter` en `ContrastBoostFilter` bevat.

```java
import com.example.ocr.Engine;
import com.example.ocr.ImagePreprocessOptions;
import com.example.ocr.filters.DeskewFilter;
import com.example.ocr.filters.DenoiseFilter;
import com.example.ocr.filters.ContrastBoostFilter;

/**
 * Demonstrates how to deskew image and apply common OCR preprocessing steps.
 */
public class OcrPreprocessDemo {

    public static void main(String[] args) {
        // 1️⃣ Create the OCR engine (replace with your actual implementation)
        Engine engine = new Engine();

        // 2️⃣ Build the preprocessing pipeline
        ImagePreprocessOptions preprocessOptions = new ImagePreprocessOptions();

        // 2a️⃣ Deskew – correct rotation up to ±15°
        preprocessOptions.addFilter(new DeskewFilter(15));

        // 2b️⃣ Denoise – remove salt‑and‑pepper noise
        preprocessOptions.addFilter(new DenoiseFilter());

        // 2c️⃣ Contrast boost – make low‑contrast scans more readable
        preprocessOptions.addFilter(new ContrastBoostFilter(1.5f));

        // 3️⃣ Attach the pipeline to the engine
        engine.setPreprocessOptions(preprocessOptions);

        // 4️⃣ Run OCR on a sample image
        String result = engine.recognizeText("sample-scanned-page.png");

        // 5️⃣ Output the recognized text
        System.out.println("=== OCR RESULT ===");
        System.out.println(result);
    }
}
```

### Waarom dit werkt

* **DeskewFilter** analyseert de dominante tekstregels van de afbeelding, schat de hoek en draait de bitmap terug naar horizontaal. De meeste bibliotheken beperken de correctie tot ±15°, omdat grotere hoeken meestal duiden op een slecht gescande pagina die handmatige interventie vereist.
* **DenoiseFilter** richt zich op het klassieke *salt‑and‑pepper*‑patroon — die geïsoleerde zwarte of witte pixels die lijken op statisch op een tv. Het verwijderen ervan voorkomt dat de OCR‑engine ruis verwart met tekens.
* **ContrastBoostFilter** strekt het histogram uit, waardoor zwakke streken beter zichtbaar worden. Een vermenigvuldiger van `1.5f` is een veilige standaard; je kunt deze verhogen als je scans bijzonder verbleekt zijn.

> **Pro tip:** Als je weet dat je documenten nooit meer dan 10° scheef staan, geef die kleinere limiet door aan `DeskewFilter` — het algoritme werkt sneller en zal minder snel over‑corrigeren.

## Image Preprocessing OCR: Filters in de juiste volgorde toevoegen

Volgorde is belangrijk. Stel je voor dat je ruis *voor* het rechtzetten verwijdert; de ruis kan de hoekdetectie verstoren, wat leidt tot een scheef resultaat. Omgekeerd zorgt het toepassen van contrastverhoging *na* het rechtzetten ervoor dat de rotatie geen nieuwe artefacten introduceert.

Hieronder staat een snelle checklist die je kunt kopiëren‑en‑plakken in elk project:

| Step | Filter | Reason |
|------|--------|--------|
| 1 | `DeskewFilter` | Lijnt de tekstbasis uit |
| 2 | `DenoiseFilter` | Verwijdert geïsoleerde pixelruis |
| 3 | `ContrastBoostFilter` | Verbetert de leesbaarheid voor OCR |

Als je extra stappen moet invoegen — bijvoorbeeld een **binarization**‑filter voor binaire OCR — plaats je die **na** het contrastverhogen, omdat een schone, hoog‑contrast afbeelding nauwkeuriger binariseert.

## Salt‑pepper‑ruis verwijderen met DenoiseFilter

Salt‑and‑pepper‑ruis is berucht bij scans van lage kwaliteit, vooral die van goedkope telefooncamera's. De `DenoiseFilter` in onze bibliotheek implementeert een median‑filterkernel, die elk pixel vervangt door de mediaan van de omliggende buurt. Het effect? Die stippen verdwijnen zonder de daadwerkelijke tekens te vervagen.

```java
// Example: customizing the median kernel size (default is 3x3)
preprocessOptions.addFilter(new DenoiseFilter(5)); // 5x5 kernel for heavy noise
```

*Wanneer de kernelgrootte vergroten?* Als je bronafbeeldingen vol zitten met grote stippen, zal een grotere kernel ze opruimen, maar wees voorzichtig: te groot en je begint fijne streken in kleine lettertypen te wissen.

## Preprocess Images OCR – De pipeline toepassen

Zodra je de filterketen hebt samengesteld, kun je deze met één regel aan de engine koppelen (`engine.setPreprocessOptions`). Vanaf dat moment wordt elke oproep naar `recognizeText` automatisch door de pipeline geleid. Je hoeft niet handmatig elk filter aan te roepen — je code blijft overzichtelijk, en toekomstige wijzigingen (een nieuw filter toevoegen, parameters aanpassen) zijn gecentraliseerd.

Dit is hoe een succesvolle uitvoering eruitziet met een voorbeeldscan die oorspronkelijk een kanteling van 12° en opvallende pepper‑ruis had:

```
=== OCR RESULT ===
Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
Thank you for your business!
```

Let op hoe de tekst schoon, correct georiënteerd en vrij van vreemde tekens is die anders zouden verschijnen als “I n v o i c e” of “$‑‑‑”.

## Randgevallen & Veelvoorkomende valkuilen

| Situation | What to watch for | Suggested fix |
|-----------|-------------------|---------------|
| Rotation > 15° | DeskewFilter kan opgeven | Vooraf handmatig roteren of een filter met een groter bereik gebruiken |
| Extremely low resolution ( < 100 dpi ) | Contrastverhoging kan geen details herstellen | Hersample de afbeelding eerst (bijv. `ResampleFilter`) |
| Mixed noise (Gaussian + salt‑pepper) | DenoiseFilter alleen is niet voldoende | Koppel een `GaussianBlurFilter` vóór de `DenoiseFilter` |
| Color scans with colored text | Grijswaardenconversie nodig | Voeg `GrayscaleFilter` toe vóór contrastverhoging |

Door deze scenario's te anticiperen bespaar je later uren aan debuggen.

## Volledig werkend voorbeeld (Alles‑in‑één)

Hieronder staat een zelfstandige Java‑klasse die je kunt toevoegen aan elk Maven‑ of Gradle‑project dat de `com.example.ocr`‑dependency bevat. Het demonstreert **hoe je een afbeelding rechtzet**, **remove salt pepper**‑ruis verwijdert, en **preprocess images OCR**‑stijl toepast.

```java
package com.myapp.demo;

import com.example.ocr.Engine;
import com.example.ocr.ImagePreprocessOptions;
import com.example.ocr.filters.*;

public class CompleteOcrPipeline {

    public static void main(String[] args) {
        // -------------------------------------------------
        // 1️⃣ Initialise OCR engine (replace with your own)
        // -------------------------------------------------
        Engine engine = new Engine();

        // -------------------------------------------------
        // 2️⃣ Configure preprocessing pipeline
        // -------------------------------------------------
        ImagePreprocessOptions options = new ImagePreprocessOptions();

        // Deskew up to ±15° – the core of "how to deskew image"
        options.addFilter(new DeskewFilter(15));

        // Remove salt‑and‑pepper artifacts
        options.addFilter(new DenoiseFilter());

        // Boost contrast by 1.5× to aid OCR recognition
        options.addFilter(new ContrastBoostFilter(1.5f));

        // (Optional) Convert to grayscale – often improves OCR accuracy
        options.addFilter(new GrayscaleFilter());

        // Attach the pipeline
        engine.setPreprocessOptions(options);

        // -------------------------------------------------
        // 3️⃣ Perform OCR on a test file
        // -------------------------------------------------
        String imagePath = "src/main/resources/scanned-document.png";
        String text = engine.recognizeText(imagePath);

        // -------------------------------------------------
        // 4️⃣ Show the result
        // -------------------------------------------------
        System.out.println("=== OCR RESULT ===");
        System.out.println(text);
    }
}
```

**Verwachte output** (ervan uitgaande dat `scanned-document.png` een duidelijke factuur bevat):

```
=== OCR RESULT ===
Invoice #98765
Date: 2024‑02‑28
Amount Due: $2,340.75
Please remit payment within 30 days.
```

Als je de afbeelding vervangt door één die al perfect uitgelijnd is, zul je merken dat de pipeline nog steeds draait — er gebeurt niets fout, en de OCR‑nauwkeurigheid blijft hoog.

## Conclusie

Je hebt nu een solide begrip van **hoe je een afbeelding rechtzet** en waarom elke voorbewerkingsstap — **image preprocessing OCR**, **remove salt pepper**, en **preprocess images OCR** — een cruciale rol speelt bij het leveren van schone, doorzoekbare tekst. Het bovenstaande voorbeeld is een compleet,

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [How to Use AspOCR: Preprocess Image OCR Filters for .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Calculate Skew Angle for OCR Image Preprocessing](/ocr/english/net/skew-angle-calculation/calculate-skew-angle/)
- [How to Set Threshold Value in OCR Image Recognition](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}