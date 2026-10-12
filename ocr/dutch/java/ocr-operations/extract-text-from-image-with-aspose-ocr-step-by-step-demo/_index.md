---
category: general
date: 2026-02-14
description: Tekst extraheren uit een afbeelding met Aspose OCR. Leer hoe je een afbeelding
  laadt voor OCR, tekst leest uit een rechthoek, en volg deze Aspose OCR‑tutorial
  in enkele minuten.
draft: false
keywords:
- extract text from image
- load image for ocr
- read text from rectangle
- aspose ocr tutorial
language: nl
og_description: Haal direct tekst uit een afbeelding. Deze gids laat zien hoe je een
  afbeelding laadt voor OCR, tekst uit een rechthoek leest en een Aspose OCR‑tutorial
  voltooit.
og_title: Tekst uit afbeelding extraheren met Aspose OCR – Snelle gids
tags:
- Aspose
- OCR
- Java
title: Tekst extraheren uit afbeelding met Aspose OCR – Stapsgewijze demo
url: /nl/java/ocr-operations/extract-text-from-image-with-aspose-ocr-step-by-step-demo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tekst uit afbeelding extraheren met Aspose OCR – Stapsgewijze demo

Heb je ooit **tekst uit afbeelding** moeten extraheren maar wist je niet waar te beginnen? Je bent niet de enige—veel ontwikkelaars lopen tegen die muur aan wanneer ze voor het eerst bonnen scannen of ID‑verificatie doen. Het goede nieuws? Met Aspose OCR kun je een afbeelding laden, het exacte gebied waarin de tekst zich bevindt definiëren, en de tekens in een handvol regels eruit halen.

In deze **aspose ocr tutorial** lopen we alles door wat je nodig hebt: de afbeelding laden voor OCR, een rechthoek instellen die de engine vertelt waar te zoeken, en uiteindelijk de geëxtraheerde tekst lezen. Aan het einde heb je een uitvoerbaar Java‑programma dat de ROI‑tekst naar de console print—geen mysterie, gewoon een duidelijke, werkende oplossing.

## Wat je nodig hebt

| Voorvereiste | Waarom het belangrijk is |
|--------------|--------------------------|
| **Java JDK 8+** | Aspose OCR wordt geleverd als een Java‑bibliotheek; elke moderne JDK volstaat. |
| **Aspose.OCR for Java** (download from the Aspose website or add via Maven) | Biedt de `OcrEngine`, `ImageStream` en gerelateerde klassen. |
| **An image file** (e.g., `receipt.jpg`) that contains printable text | We wijzen de engine op een rechthoek binnen dit bestand. |
| **IDE or editor** (IntelliJ, Eclipse, VS Code…) | Helpt je de voorbeeldcode snel te compileren en uit te voeren. |

Als je Maven gebruikt, voeg dan deze afhankelijkheid toe aan je `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- check Aspose for the latest version -->
</dependency>
```

> **Pro tip:** Het versienummer hierboven is actueel vanaf februari 2026. Updaten naar de nieuwste release zorgt ervoor dat je bug‑fixes en prestatie‑verbeteringen krijgt.

## Stap 1 – Initialiseer de OCR‑engine

Allereerst heb je een instantie van `OcrEngine` nodig. Beschouw het als het brein dat de pixels analyseert.

```java
// Step 1: Create the OCR engine object
OcrEngine ocrEngine = new OcrEngine();
```

Waarom op deze manier maken? Aspose scheidt de engine (die de configuratie bevat) van de afbeeldingsdata, waardoor je de dezelfde engine voor meerdere afbeeldingen kunt hergebruiken als je dat wilt.

## Stap 2 – Laad afbeelding voor OCR

Nu **laden we de afbeelding voor OCR**. De helper `ImageStream.fromFile` leest het bestand in een stream die Aspose kan begrijpen.

```java
// Step 2: Load the target image (replace with your own path)
String imagePath = "YOUR_DIRECTORY/receipt.jpg";
ocrEngine.setImage(ImageStream.fromFile(imagePath));
```

Als het bestand niet gevonden kan worden, gooit de engine een uitzondering, dus je wilt dit misschien in een try‑catch‑blok plaatsen in productcode. Voor deze demo laten we de uitzondering omhoog bubbelen—houdt het voorbeeld netjes.

## Stap 3 – Definieer de rechthoek (Tekst lezen uit rechthoek)

Hier komt het **tekst lezen uit rechthoek**-gedeelte tot zijn recht. Je vertelt de engine precies waar te zoeken, wat de verwerking versnelt en valse positieven vermindert.

```java
// Step 3: Create a rectangle that covers the area with the receipt total
// Parameters: x, y, width, height (all in pixels)
Rectangle regionOfInterest = new Rectangle(120, 350, 600, 200);
ocrEngine.getEngineOptions().setRegionOfInterest(regionOfInterest);
```

> **Waarom een rechthoek?**  
> De meeste documenten hebben voorspelbare lay-outs—denk aan een bon waarbij het bedrag altijd onderaan staat. Door je op dat gedeelte te richten, negeert de OCR‑engine irrelevante grafische elementen en verbetert de nauwkeurigheid.

**Randgeval:** Als de rechthoek buiten de afbeelding valt, beperkt Aspose deze stilletjes, maar je verliest gegevens. Een snelle sanity‑check kan dat voorkomen:

```java
if (regionOfInterest.x + regionOfInterest.width > ocrEngine.getImage().getWidth() ||
    regionOfInterest.y + regionOfInterest.height > ocrEngine.getImage().getHeight()) {
    throw new IllegalArgumentException("ROI exceeds image dimensions.");
}
```

## Stap 4 – Verwerk de afbeelding

Met alles ingesteld, vragen we de engine om zijn magie te doen.

```java
// Step 4: Run OCR on the defined ROI
OcrResult ocrResult = ocrEngine.process();
```

De `process()`‑aanroep retourneert een `OcrResult`‑object dat de geëxtraheerde tekst, vertrouwensscores, en zelfs de begrenzingskaders voor elk woord bevat, mocht je die later nodig hebben.

## Stap 5 – Output de geëxtraheerde tekst

Print tenslotte het resultaat. In een echte app sla je het misschien op in een database of stuur je het door naar een andere service, maar voor deze tutorial is console‑output voldoende.

```java
// Step 5: Display the recognized text
System.out.println("ROI text:");
System.out.println(ocrResult.getText());
```

**Verwachte output** (ervan uitgaande dat de rechthoek het totale bedrag op een bon heeft vastgelegd):

```
ROI text:
$12.34
```

Als de ROI leeg is of de afbeelding onscherp, zie je een lege string of onleesbare tekens. Pas de rechthoek aan, verbeter de beeldkwaliteit, of schakel Aspose’s preprocessing‑opties in (bijv. `setAutoSkewCorrection(true)`).

## Volledig werkend voorbeeld

Hieronder staat het volledige, kant‑klaar programma. Kopieer‑en plak het in een bestand genaamd `RoiDemo.java`, pas het afbeeldingspad aan, en voer `javac RoiDemo.java && java RoiDemo` uit.

```java
import com.aspose.ocr.*;
import java.awt.Rectangle;

/**
 * Demo: Extract text from a specific rectangle (ROI) in an image using Aspose OCR.
 * Adjust the rectangle coordinates to match the area you want to read.
 */
public class RoiDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image for OCR
        // Replace YOUR_DIRECTORY with the actual folder containing receipt.jpg
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/receipt.jpg"));

        // Step 3: Define the region of interest where text is expected
        // (x, y, width, height) in pixels
        Rectangle regionOfInterest = new Rectangle(120, 350, 600, 200);
        ocrEngine.getEngineOptions().setRegionOfInterest(regionOfInterest);

        // Optional sanity check – ensures ROI fits inside the image
        if (regionOfInterest.x + regionOfInterest.width > ocrEngine.getImage().getWidth() ||
            regionOfInterest.y + regionOfInterest.height > ocrEngine.getImage().getHeight()) {
            throw new IllegalArgumentException("ROI exceeds image dimensions.");
        }

        // Step 4: Perform OCR on the defined ROI
        OcrResult ocrResult = ocrEngine.process();

        // Step 5: Output the extracted text
        System.out.println("ROI text:");
        System.out.println(ocrResult.getText());
    }
}
```

> **Resultaatverificatie:** Na het uitvoeren, vergelijk de console‑output met de daadwerkelijke tekst binnen de rechthoek. Als ze overeenkomen, heb je met succes **tekst uit afbeelding** geëxtraheerd met Aspose OCR.

## Veelgestelde vragen & tips

### Wat als ik meerdere ROI's in dezelfde afbeelding moet verwerken?
Maak voor elk gebied een nieuwe `Rectangle`, roep opnieuw `setRegionOfInterest` aan, en voer `process()` opnieuw uit. De engine hergebruikt dezelfde afbeeldingsdata, waardoor de prestaties snel blijven.

### Hoe gaat Aspose om met verschillende talen of lettertypen?
Je kunt het taalmodel wijzigen via `ocrEngine.getEngineOptions().setLanguage(OcrLanguage.English)`. Voor niet‑Latijnse scripts laad je het juiste taalpakket (beschikbaar op de Aspose‑downloadpagina).

### Ondersteunt de bibliotheek PDF‑invoer?
Ja—Aspose OCR kan PDF‑streams direct accepteren. Vervang gewoon `ImageStream.fromFile` door `ImageStream.fromPdfFile("doc.pdf")` en specificeer eventueel het paginanummer.

### Kan ik de nauwkeurigheid verbeteren bij scans van lage kwaliteit?
Schakel preprocessing in:

```java
ocrEngine.getEngineOptions().setAutoSkewCorrection(true);
ocrEngine.getEngineOptions().setBinarizationMethod(BinarizationMethod.Otsu);
```

## Conclusie

We hebben zojuist een volledige **aspose ocr tutorial** doorlopen die laat zien hoe je **tekst uit afbeelding** kunt **extraheren**, **afbeelding voor OCR** kunt **laden**, en **tekst uit rechthoek** kunt **lezen** met Java. De belangrijkste stappen zijn het initialiseren van de engine, het voeden van een afbeelding, het definiëren van een region of interest, verwerken, en tenslotte het resultaat afdrukken.

Vanaf hier kun je het volgende verkennen:

* **Batchverwerking** – loop over een map met bonnen en sla elk totaal op in een database.  
* **Dynamische ROI-detectie** – gebruik beeldverwerkingsbibliotheken (OpenCV) om tekstblokken automatisch te lokaliseren.  
* **Post‑processing** – pas regex of fuzzy matching toe om OCR‑eigenaardigheden op te schonen.

Probeer die ideeën uit, pas de rechthoek aan op jouw eigen documenten, en je hebt in een mum van tijd een robuuste tekst‑extractiepijplijn. Veel programmeerplezier!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}