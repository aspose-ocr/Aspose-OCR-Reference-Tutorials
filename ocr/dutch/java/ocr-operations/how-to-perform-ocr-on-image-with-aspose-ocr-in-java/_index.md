---
category: general
date: 2026-09-10
description: Voer OCR uit op een afbeelding met Aspose OCR Java. Leer tekst te herkennen
  uit JPEG, tekst uit een afbeelding te extraheren en afbeelding efficiënt naar tekst
  te converteren.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- perform OCR on image
- recognize text from JPEG
- extract text from image
- convert image to text
- load image for OCR
language: nl
lastmod: 2026-09-10
og_description: Voer OCR uit op een afbeelding met Aspose OCR Java. Deze tutorial
  laat zien hoe je tekst uit een JPEG herkent, tekst uit een afbeelding extraheert
  en een afbeelding naar tekst converteert in een paar regels code.
og_image_alt: Screenshot of Java code that performs OCR on an image using Aspose OCR
og_title: Voer OCR uit op afbeelding met Aspose OCR – Java-gids
schemas:
- author: Aspose
  dateModified: '2026-09-10'
  description: perform OCR on image using Aspose OCR Java. Learn to recognize text
    from JPEG, extract text from image, and convert image to text efficiently.
  headline: How to perform OCR on image with Aspose OCR in Java
  type: TechArticle
- description: perform OCR on image using Aspose OCR Java. Learn to recognize text
    from JPEG, extract text from image, and convert image to text efficiently.
  name: How to perform OCR on image with Aspose OCR in Java
  steps:
  - name: Prerequisites
    text: '* Java Development Kit (JDK) 8 or later. * Maven or Gradle to manage dependencies
      (the example uses Maven). * A valid Aspose OCR for Java license (or a temporary
      evaluation key). * An image file named `sample.jpg` placed in a known directory.'
  - name: Load image for OCR
    text: '```java // Step 1: Load the image you want to process String imagePath
      = "YOUR_DIRECTORY/sample.jpg"; ImageStream imageStream = ImageStream.fromFile(imagePath);
      ```'
  - name: Create and configure the OCR engine
    text: '```java // Step 2: Create an OCR engine instance OcrEngine engine = new
      OcrEngine();'
  - name: Recognize text from JPEG
    text: '```java // Step 3: Attach the image to the engine engine.setImage(imageStream);'
  - name: Extract text from image and output
    text: '```java // Step 5: Output the recognized text System.out.println("=== Recognized
      Text ==="); System.out.println(result.getText()); ```'
  - name: Expected output
    text: 'Assuming `sample.jpg` contains the text “Hello World”, the console will
      display:'
  type: HowTo
tags:
- OCR
- Java
- Aspose
title: Hoe OCR op een afbeelding uit te voeren met Aspose OCR in Java
url: /nl/java/ocr-operations/how-to-perform-ocr-on-image-with-aspose-ocr-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe OCR op een afbeelding uit te voeren met Aspose OCR in Java

Als je **OCR op afbeelding** bestanden moet uitvoeren in een Java‑applicatie, biedt deze gids een complete, kant‑klaar oplossing. Je ziet hoe je **tekst uit JPEG** bestanden kunt **herkennen**, **tekst uit afbeelding** gegevens kunt **extraheren**, en **afbeelding naar tekst** kunt **converteren** met de moderne API van Aspose OCR.

De tutorial loopt stap voor stap door alles wat nodig is – van het laden van de afbeelding tot het afdrukken van de herkende tekst – zodat je OCR‑functionaliteit kunt integreren zonder extra bronnen te zoeken. Er zijn geen externe tools nodig, behalve de Aspose OCR voor Java‑bibliotheek.

## Wat je zult bereiken

* **Laad een afbeelding voor OCR** direct vanaf het bestandssysteem.  
* Schakel de preprocessing van Aspose OCR in (bijv. denoising) om de nauwkeurigheid te verbeteren.  
* **Tekst herkennen uit JPEG** en andere rasterformaten.  
* **Tekst extraheren uit afbeelding** en deze naar de console outputten.  
* Begrijpen hoe je **afbeelding naar tekst** kunt **converteren** in een productie‑klaar code‑voorbeeld.

### Vereisten

* Java Development Kit (JDK) 8 of hoger.  
* Maven of Gradle om afhankelijkheden te beheren (het voorbeeld gebruikt Maven).  
* Een geldige Aspose OCR voor Java‑licentie (of een tijdelijke evaluatiesleutel).  
* Een afbeeldingsbestand genaamd `sample.jpg` geplaatst in een bekende map.

> **Pro tip:** Gebruik hoge‑resolutie JPEG’s (300 dpi of hoger) voor de beste herkenningspercentages.  

## Stap 1: Voeg Aspose OCR toe aan je project

Als je afhankelijkheden beheert met Maven, voeg dan het volgende fragment toe aan je `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version>
</dependency>
```

Voor Gradle, voeg toe:

```gradle
implementation 'com.aspose:aspose-ocr:23.12'
```

Deze coördinaten halen de nieuwste stabiele Aspose OCR‑bibliotheek op, die de later gebruikte preprocessing‑functies bevat.

## OCR op afbeelding uitvoeren – stap‑voor‑stap

De volgende secties splitsen het volledige programma op. Elk blok is een zelfstandige eenheid die je kunt kopiëren, plakken en uitvoeren.

### Afbeelding laden voor OCR

```java
// Step 1: Load the image you want to process
String imagePath = "YOUR_DIRECTORY/sample.jpg";
ImageStream imageStream = ImageStream.fromFile(imagePath);
```

*Waarom dit belangrijk is:*  
`ImageStream.fromFile` leest de ruwe bytes van de JPEG en maakt ze klaar voor de OCR‑engine. De methode werkt met elk rasterformaat dat door Aspose OCR wordt ondersteund, zodat je de JPEG kunt vervangen door PNG of BMP zonder code‑wijzigingen.

### Maak en configureer de OCR‑engine

```java
// Step 2: Create an OCR engine instance
OcrEngine engine = new OcrEngine();

// Enable preprocessing to improve accuracy (e.g., denoising)
engine.getPreprocessing().setDenoise(true);
```

*Waarom dit belangrijk is:*  
Het instantieren van `OcrEngine` reserveert de kernherkenningsengine. Het inschakelen van de **denoise**‑vlag verwijdert visueel ruis dat vaak de tekenherkenning belemmert, vooral bij gescande JPEG’s.

### Tekst herkennen uit JPEG

```java
// Step 3: Attach the image to the engine
engine.setImage(imageStream);

// Step 4: Perform OCR recognition
OcrResult result = engine.recognize();
```

*Waarom dit belangrijk is:*  
`engine.setImage` koppelt de afbeeldingsdata aan de OCR‑pipeline. `engine.recognize()` voert het volledige herkenningsproces uit en retourneert een `OcrResult` die de geëxtraheerde tekst en vertrouwensstatistieken bevat.

### Tekst extraheren uit afbeelding en weergeven

```java
// Step 5: Output the recognized text
System.out.println("=== Recognized Text ===");
System.out.println(result.getText());
```

*Waarom dit belangrijk is:*  
`result.getText()` levert de platte‑tekstrepresentatie van de afbeeldingsinhoud. Het naar de console afdrukken toont aan dat **afbeelding naar tekst** succesvol is uitgevoerd, en je kunt deze string doorsturen naar bestanden, databases of downstream‑services.

## Volledig, uitvoerbaar voorbeeld

Hieronder staat de volledige Java‑klasse die alle stappen bevat. Vervang `YOUR_DIRECTORY` door het absolute pad naar je JPEG‑bestand.

```java
import com.aspose.ocr.*;

public class OcrDemo {
    public static void main(String[] args) throws Exception {
        // Load the image for OCR
        String imagePath = "YOUR_DIRECTORY/sample.jpg";
        ImageStream imageStream = ImageStream.fromFile(imagePath);

        // Create and configure the OCR engine
        OcrEngine engine = new OcrEngine();
        engine.getPreprocessing().setDenoise(true); // improve accuracy

        // Attach the image and run recognition
        engine.setImage(imageStream);
        OcrResult result = engine.recognize();

        // Print the extracted text
        System.out.println("=== Recognized Text ===");
        System.out.println(result.getText());
    }
}
```

### Verwachte output

Aangenomen dat `sample.jpg` de tekst “Hello World” bevat, zal de console het volgende weergeven:

```
=== Recognized Text ===
Hello World
```

Als de afbeelding meerdere regels bevat, verschijnt elke regel op een eigen regel in de output.

## Veelvoorkomende variaties en randgevallen

| Situatie                                 | Aanbevolen aanpassing |
|------------------------------------------|-----------------------|
| **Low‑resolution JPEG** (≤150 dpi)       | Verhoog `engine.getPreprocessing().setUpsample(true);` zodat Aspose opschaalt vóór herkenning. |
| **Colored background** (bijv. gescande formulieren) | Schakel `engine.getPreprocessing().setBinarize(true);` in om de afbeelding naar zwart‑wit te converteren. |
| **Non‑Latin script** (bijv. Cyrillisch) | Stel de taal in: `engine.getLanguage().setLanguage(OcrLanguage.RUSSIAN);`. |
| **Large batch processing**               | Herbruik één `OcrEngine`‑instantie voor meerdere afbeeldingen om opstartkosten te verminderen. |
| **Need confidence scores**               | Gebruik `result.getConfidence()` voor per‑karakter vertrouwenswaarden. |

Deze aanpassingen laten zien hoe je **afbeelding voor OCR** kunt **laden** onder verschillende omstandigheden terwijl je nog steeds **OCR op afbeelding** betrouwbaar kunt uitvoeren.

## Prestatieoverwegingen

* **Memory usage:** Elke `ImageStream` houdt de volledige afbeelding in het geheugen. Voor zeer grote bestanden (bijv. >10 MB) kun je overwegen de afbeelding in stukken te streamen met `ImageStream.fromByteArray`.  
* **Thread safety:** `OcrEngine` is *niet* thread‑safe. Maak een aparte instantie per thread aan als je OCR‑taken wilt paralleliseren.  
* **License mode:** Evaluatiemodus beperkt het aantal pagina’s dat per sessie wordt verwerkt. Zet een gelicentieerde versie in voor productie‑workloads.

## Conclusie

Je weet nu hoe je **OCR op afbeelding** bestanden in Java kunt uitvoeren met Aspose OCR. De tutorial behandelde het laden van een afbeelding, het inschakelen van preprocessing, het herkennen van tekst uit JPEG, het extraheren van de tekst, en het converteren van de afbeelding naar tekst – alles in één beknopt programma.

Vanaf hier kun je gerelateerde onderwerpen verkennen, zoals **tekst uit JPEG** in bulk herkennen, de output integreren met een zoekindex, of OCR combineren met natural‑language processing voor slimmere document‑pijplijnen. Experimenteer met de preprocessing‑opties om de beste nauwkeurigheid te behalen voor jouw specifieke afbeeldingsbronnen.

--- 

*Afbeelding die de code‑output illustreert*  
![perform OCR on image Java example](image-placeholder.png){alt="OCR op afbeelding uitvoeren met Aspose OCR Java"}

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [tekst in afbeelding herkennen met Aspose OCR – Volledige Java OCR Tutorial](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Hoe OCR-beeldtekst met taal te gebruiken met Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Afbeelding voor OCR pre-processen in Java met Aspose OCR – Verhoog nauwkeurigheid & tekst extraheren](/ocr/english/java/advanced-ocr-techniques/preprocess-image-ocr-in-java-boost-accuracy-extract-text/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}