---
category: general
date: 2026-06-16
description: OCR-boundingbox-tutorial in Java laat zien hoe je tekst uit een afbeelding
  kunt extraheren, tekst uit een afbeelding kunt lezen en de OCR‑betrouwbaarheidscore
  voor JPG‑bestanden kunt verkrijgen.
draft: false
keywords:
- ocr bounding box
- extract text from image
- ocr confidence score
- recognize text from jpg
- read text from image
language: nl
og_description: OCR-bounding box in Java stelt je in staat om tekst te herkennen uit
  JPG‑bestanden, tekst uit een afbeelding te extraheren en OCR‑vertrouwensscores te
  bekijken — allemaal in een eenvoudig codevoorbeeld.
og_title: OCR-boundingbox in Java – Tekst uit afbeelding extraheren
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: OCR bounding box tutorial in Java shows how to extract text from image,
    read text from image, and get OCR confidence score for JPG files.
  headline: OCR Bounding Box in Java – Extract Text from Image
  type: TechArticle
tags:
- OCR
- Java
- image-processing
- text-recognition
title: OCR-bounding box in Java – Tekst uit afbeelding halen
url: /nl/java/advanced-ocr-techniques/ocr-bounding-box-in-java-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR-boundingbox in Java – Tekst extraheren uit afbeelding

Heb je je ooit afgevraagd hoe je de **ocr bounding box** voor elk stuk tekst in een Java‑afbeelding kunt krijgen? In deze tutorial laten we je zien hoe je **extract text from image** bestanden kunt **read text from image**, en zelfs de **ocr confidence score** kunt zien terwijl je **recognize text from jpg** bestanden. Het korte antwoord? Een paar regels code met een moderne OCR‑bibliotheek, plus een beetje uitleg over waarom elke aanroep belangrijk is.

Hieronder vind je een compleet, kant‑klaar voorbeeld, een stap‑voor‑stap‑uitleg, en een reeks praktische tips die je direct in je eigen project kunt kopiëren. Aan het einde kun je iets als volgt weergeven:

```
Text: "Hello World"  Confidence: 0.97  Box: (x=12, y=45, width=210, height=30)
```

## Wat je nodig hebt

- **Java 11** of nieuwer (de syntaxis hieronder gebruikt het `var`‑keyword voor beknoptheid, maar je kunt het weglaten voor oudere JDK’s).  
- Een OCR‑bibliotheek die een Java‑API biedt – voor deze gids gebruiken we **[Tesseract4J](https://github.com/nguyenq/tess4j)**, een dunne wrapper rond de populaire Tesseract‑engine.  
- Een JPEG‑afbeelding (`.jpg`) die duidelijke, gedrukte tekst bevat.  
- Je favoriete IDE (IntelliJ IDEA, Eclipse, VS Code…) – elke werkt.

Als je de bibliotheek mist, voeg dan gewoon deze Maven‑dependency toe:

```xml
<dependency>
    <groupId>net.sourceforge.tess4j</groupId>
    <artifactId>tess4j</artifactId>
    <version>5.4.0</version>
</dependency>
```

Laten we nu beginnen.

![OCR bounding box example](ocr-bounding-box.png "OCR bounding box example")

## OCR-boundingbox: De engine instellen

Het eerste wat je moet doen is een OCR‑engine‑instantie maken. Beschouw het als het inschakelen van de scanner die later de pixels zal lezen.

```java
import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;

ITesseract ocrEngine = new Tesseract();          // Step 1 – create the OCR engine
ocrEngine.setDatapath("tessdata");               // point to the language data files
ocrEngine.setLanguage("eng");                    // we’ll work with English for now
```

**Waarom dit belangrijk is:**  
Zonder het instellen van `datapath` weet Tesseract niet waar zijn taalpakketten zich bevinden, en krijg je een cryptische “Failed loading language”‑fout. De `setLanguage`‑aanroep is optioneel als je alleen het standaard Engelse pakket nodig hebt, maar expliciet zijn maakt de code duidelijker voor toekomstige lezers.

## Laad de afbeelding die je wilt verwerken

Vervolgens geef je de engine de JPEG die je wilt analyseren. De bibliotheek accepteert een `File` of `BufferedImage`; we gebruiken een `File` voor de eenvoud.

```java
import java.io.File;

File imageFile = new File("YOUR_DIRECTORY/text_page.jpg");   // Step 2 – load the image
```

**Pro tip:**  
Als je afbeelding zich in resources bevindt (bijv. binnen een JAR), gebruik dan `getResourceAsStream` en wikkel het in `ImageIO.read`. Op die manier werkt de tutorial zowel lokaal als in een verpakte app.

## Voer OCR‑herkenning uit

Nu vragen we de engine daadwerkelijk om de afbeelding te lezen. Het resultaat is een platte‑tekst‑string, maar we willen ook de **ocr confidence score** en de **ocr bounding box** voor elke regel.

```java
try {
    // Step 3 – run OCR and get a result object with layout data
    var result = ocrEngine.doOCR(imageFile, null);
    // The simple doOCR call returns only text; to get boxes we need the
    // getWords method with a specific page iterator level.
    var words = ocrEngine.getWords(imageFile, ITesseract.PageIteratorLevel.RIL_WORD);
    
    // Step 4 – iterate over each detected word
    for (var word : words) {
        System.out.printf(
            "Text: \"%s\"  Confidence: %.2f  Box: %s%n",
            word.getText(),
            word.getConfidence(),
            word.getBoundingBox().toString()
        );
    }
} catch (TesseractException e) {
    System.err.println("OCR failed: " + e.getMessage());
}
```

**Waarom we `getWords` gebruiken in plaats van de eenvoudige `doOCR`:**  
`doOCR` geeft je de ruwe string maar gooit ruimtelijke informatie weg. Door `getWords` aan te roepen met `RIL_WORD` (of `RIL_TEXTLINE` als je liever boxen op regelniveau wilt), krijgen we een lijst van `Word`‑objecten die elk de tekst, het vertrouwen en de omhullende rechthoek bevatten. Dat is de kern van de **ocr bounding box**‑functionaliteit.

## De output begrijpen

Het uitvoeren van de bovenstaande code op een schone JPEG levert een output op die lijkt op:

```
Text: "Hello"  Confidence: 0.99  Box: java.awt.Rectangle[x=34,y=12,width=112,height=28]
Text: "World"  Confidence: 0.97  Box: java.awt.Rectangle[x=156,y=12,width=98,height=28]
```

- **Text** – de herkende tekens.  
- **Confidence** – een zwevend‑kommagetal tussen 0 en 1; hoger betekent dat de engine zekerder is.  
- **Box** – de rechthoek die het woord omsluit in pixelcoördinaten (x, y, breedte, hoogte).

Je kunt nu **read text from image** en bovendien precies weten waar elk fragment zich op het canvas bevindt — perfect voor markeren, bijsnijden, of invoeren in downstream‑NLP‑pijplijnen.

## Randgevallen & Veelvoorkomende valkuilen

| Situatie | Waar op te letten | Oplossing / Work‑around |
|-----------|-------------------|-------------------|
| Afbeelding is onscherp of heeft weinig contrast | Vertrouwensscores dalen drastisch (vaak onder 0,6). | Pre‑process met OpenCV: contrast verhogen, drempelwaarde toepassen. |
| JPEG bevat gedraaide tekst | Bounding boxes lijken scheef of ontbreken. | Gebruik `ocrEngine.setPageSegMode(ITesseract.PageSegMode.PSM_AUTO_OSD)` om Tesseract de oriëntatie automatisch te laten detecteren. |
| Grote afbeeldingen veroorzaken OutOfMemoryError | Java‑heap raakt vol bij het laden van grote afbeeldingen. | Schaal de afbeelding eerst verkleinen vóór OCR (`ImageIO.read` → `BufferedImage.getScaledInstance`). |
| Je hebt boxen op regelniveau nodig in plaats van op woordniveau | `RIL_WORD` geeft boxen per woord. | Schakel over naar `ITesseract.PageIteratorLevel.RIL_TEXTLINE`. |
| Niet‑Engelse tekens verschijnen als � | Taalgegevens niet geladen. | Download het juiste `.traineddata`‑bestand en wijs `setDatapath` naar de map. |

Deze problemen vroeg aanpakken bespaart je later uren aan debuggen.

## Volledig werkend voorbeeld (Alle stappen in één bestand)

Hieronder staat een zelfstandige Java‑klasse die je kunt copy‑paste naar een `src/main/java`‑map en kunt uitvoeren met `mvn exec:java`. Het bundelt alles wat we hebben besproken.

```java
package com.example.ocrdemo;

import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.ITesseract.RenderedFormat;
import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;
import net.sourceforge.tess4j.Word;

import java.io.File;
import java.util.List;

public class OcrBoundingBoxDemo {

    public static void main(String[] args) {
        // ==== Step 1: Initialize the OCR engine ====
        ITesseract ocrEngine = new Tesseract();
        ocrEngine.setDatapath("tessdata"); // folder containing .traineddata files
        ocrEngine.setLanguage("eng");      // English language pack

        // Optional: improve accuracy for printed text
        ocrEngine.setPageSegMode(ITesseract.PageSegMode.PSM_AUTO);
        ocrEngine.setOcrEngineMode(ITesseract.OEM_TESSERACT_ONLY);

        // ==== Step 2: Load the JPEG you want to read ====
        File imageFile = new File("YOUR_DIRECTORY


## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap‑uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Tekst extraheren uit afbeelding Java met Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Tekstafbeeldingen extraheren – OCR‑basis met Aspose.OCR voor Java](/ocr/english/java/ocr-basics/)
- [Hoe OCR‑afbeeldingstekst met taal te gebruiken met Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}