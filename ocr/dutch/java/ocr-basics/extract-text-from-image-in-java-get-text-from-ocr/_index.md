---
category: general
date: 2026-05-25
description: Tekst extraheren uit een afbeelding in Java met OCR. Leer hoe je een
  afbeelding laadt voor OCR, tekst herkent van een foto en tekst verkrijgt uit OCR
  met een eenvoudig codevoorbeeld.
draft: false
keywords:
- extract text from image
- get text from ocr
- recognize text from photo
- java image to text
- load image for ocr
language: nl
og_description: Haal tekst uit een afbeelding in Java met een stapsgewijze handleiding.
  Leer hoe je een afbeelding laadt voor OCR, tekst van een foto herkent en efficiënt
  tekst uit OCR haalt.
og_title: Tekst uit afbeelding extraheren in Java – Tekst ophalen met OCR
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: Extract text from image in Java using OCR. Learn how to load image
    for OCR, recognize text from photo, and get text from OCR with a simple code example.
  headline: Extract Text from Image in Java – Get Text from OCR
  type: TechArticle
- description: Extract text from image in Java using OCR. Learn how to load image
    for OCR, recognize text from photo, and get text from OCR with a simple code example.
  name: Extract Text from Image in Java – Get Text from OCR
  steps:
  - name: '**Wrong language setting** – If you forget step 2, the engine defaults
      to English, turning Cyrillic characters into gibberish. Always double‑check
      the language code.'
    text: '**Wrong language setting** – If you forget step 2, the engine defaults
      to English, turning Cyrillic characters into gibberish. Always double‑check
      the language code.'
  - name: '**Image quality matters** – Low‑resolution or blurry photos will degrade
      accuracy. Pre‑process with contrast enhancement or binarization if needed.'
    text: '**Image quality matters** – Low‑resolution or blurry photos will degrade
      accuracy. Pre‑process with contrast enhancement or binarization if needed.'
  - name: '**File path quirks** – On Windows, backslashes need escaping (`C:\images\file.jpg`).
      Using `Path.of(...)` from `java.nio.file` sidesteps this.'
    text: '**File path quirks** – On Windows, backslashes need escaping (`C:\images\file.jpg`).
      Using `Path.of(...)` from `java.nio.file` sidesteps this.'
  - name: '**Memory leaks** – `OcrEngine` holds native resources. Call `ocrEngine.dispose()`
      when you’re done, especially in long‑running services.'
    text: '**Memory leaks** – `OcrEngine` holds native resources. Call `ocrEngine.dispose()`
      when you’re done, especially in long‑running services.'
  - name: '**Thread safety** – The engine isn’t thread‑safe out of the box. Create
      a separate instance per thread or synchronize access.'
    text: '**Thread safety** – The engine isn’t thread‑safe out of the box. Create
      a separate instance per thread or synchronize access.'
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: Tekst extraheren uit afbeelding in Java – Tekst verkrijgen via OCR
url: /nl/java/ocr-basics/extract-text-from-image-in-java-get-text-from-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tekst extraheren uit afbeelding in Java – Tekst verkrijgen via OCR

Heb je ooit **tekst uit een afbeelding moeten extraheren** maar wist je niet welke Java‑bibliotheek je moet kiezen? Je bent niet de enige. Of je nu bonnen digitaliseert, serienummers uit productfoto's haalt, of gewoon met een leuk nevenproject speelt, een foto omzetten naar bewerkbare tekst is een veelvoorkomende uitdaging.

In deze tutorial lopen we stap voor stap door een compleet, kant‑klaar voorbeeld dat laat zien hoe je **afbeelding laadt voor OCR**, de engine configureert en uiteindelijk **tekst herkent van foto** zodat je **tekst kunt verkrijgen via OCR** met slechts een paar regels code. Geen vage verwijzingen – alles wat je nodig hebt staat hier.

## Wat je zult leren

* Hoe je een lichtgewicht OCR‑engine in Java opzet.  
* De exacte stappen om **afbeelding te laden voor OCR** en verschillende bestands‑paden af te handelen.  
* Waarom het configureren van de taal belangrijk is wanneer je **tekst uit een afbeelding** wilt extraheren die niet Engels is.  
* Hoe je het resultaat veilig uitvoert en wat te doen wanneer de engine niets retourneert.  
* Een handvol pro‑tips om de meest voorkomende valkuilen te vermijden.

Aan het einde van deze gids heb je een zelf‑containend programma dat een JPEG (of PNG) met Oekraïense tekens leest en de herkende string naar de console print. Voel je vrij om de taal of afbeelding te wisselen – alles is modulair.

---

![Diagram showing the flow of extracting text from image using Java OCR engine](/images/extract-text-from-image-java.png)

*Alt‑tekst: Stroomdiagram van het proces om tekst uit een afbeelding te extraheren in Java.*

## Voorvereisten

* **Java Development Kit (JDK) 11+** – de code maakt gebruik van het moderne modulesysteem, maar oudere versies werken met kleine aanpassingen.  
* **Maven of Gradle** – om de OCR‑bibliotheek binnen te halen (we gebruiken **Asprise OCR** als een lichtgewicht, gratis‑voor‑ontwikkeling optie).  
* Een voorbeeld‑afbeeldingsbestand (bijv. `ukrainian_sign.jpg`) op een locatie die je programma kan lezen.  
* Basiskennis van Java’s `main`‑methode en exception‑handling.

Als je dit hebt, kun je meteen aan de slag. Zo niet, download dan de JDK van Oracle of AdoptOpenJDK en zet een simpel Maven‑project op – niets te ingewikkeld.

---

## Stap 1: Voeg de OCR‑dependency toe

Vertel eerst je build‑tool om de OCR‑engine op te halen. Voor Maven, voeg dit toe aan `pom.xml`:

```xml
<dependency>
    <groupId>com.asprise.ocr</groupId>
    <artifactId>asprise-ocr</artifactId>
    <version>1.0.2</version>
</dependency>
```

Als je liever Gradle gebruikt, is het equivalent:

```gradle
implementation 'com.asprise.ocr:asprise-ocr:1.0.2'
```

Deze coördinaten halen een compacte JAR op die `OcrEngine`, `OcrLanguage` en de helper‑klassen bevat die we gaan gebruiken. Er zijn geen extra native binaries nodig voor basis‑Latijnse en Cyrillische scripts.

---

## Stap 2: Maak een Java‑klasse om **tekst uit afbeelding te extraheren**

Nu schrijven we het daadwerkelijke programma. Sla het volgende op als `ExtractTextDemo.java` in `src/main/java/com/example/ocr/`.

```java
package com.example.ocr;

import com.asprise.ocr.OcrEngine;
import com.asprise.ocr.OcrLanguage;

/**
 * Demonstrates how to extract text from image using Asprise OCR.
 * The example loads a JPEG, sets the language to Ukrainian,
 * runs recognition, and prints the result.
 */
public class ExtractTextDemo {

    public static void main(String[] args) {
        // ---- 1️⃣  Initialize the OCR engine ---------------------------------
        OcrEngine ocrEngine = new OcrEngine();

        // ---- 2️⃣  Configure the engine to recognize Ukrainian text -----------
        // This is crucial if your image contains non‑Latin characters.
        ocrEngine.getEngineOptions().setLanguage(OcrLanguage.UKRAINIAN);

        // ---- 3️⃣  Load the image that contains Ukrainian characters ----------
        // Replace the path with the location of your own picture.
        String imagePath = "YOUR_DIRECTORY/ukrainian_sign.jpg";
        try {
            ocrEngine.getImage().loadFromFile(imagePath);
        } catch (Exception e) {
            System.err.println("Failed to load image: " + e.getMessage());
            return;
        }

        // ---- 4️⃣  Perform OCR recognition and obtain the extracted text -------
        String recognizedText;
        try {
            recognizedText = ocrEngine.recognize().getText();
        } catch (Exception e) {
            System.err.println("Recognition error: " + e.getMessage());
            return;
        }

        // ---- 5️⃣  Output the recognized text to the console -------------------
        System.out.println("=== OCR Result ===");
        System.out.println(recognizedText);
    }
}
```

### Waarom deze structuur werkt

* **Gescheiden genummerde blokken** maken de stroom makkelijk te volgen, vooral wanneer je zoekt naar waar je **afbeelding laadt voor OCR** of **tekst herkent van foto**.  
* De `try/catch` rond het laden van de afbeelding en het herkennen zorgt ervoor dat het programma netjes faalt – handig wanneer het bestandspad onjuist is of de OCR‑engine de taaldataset niet kan vinden.  
* Het vroeg instellen van de taal (stap 2) verbetert de nauwkeurigheid drastisch voor niet‑Engelse scripts. Als je later **java image to text** voor andere talen nodig hebt, verwissel je gewoon `OcrLanguage.UKRAINIAN` voor `OcrLanguage.ENGLISH`, `FRENCH`, enz.

---

## Stap 3: Bouw en voer het programma uit

Voer vanuit de project‑root uit:

```bash
mvn clean compile exec:java -Dexec.mainClass="com.example.ocr.ExtractTextDemo"
```

Of, als je Gradle gebruikt:

```bash
./gradlew run --args="com.example.ocr.ExtractTextDemo"
```

Aangenomen dat `ukrainian_sign.jpg` de tekst *«Ласкаво просимо»* (Oekraïens voor “Welcome”) bevat, zou je iets moeten zien als:

```
=== OCR Result ===
Ласкаво просимо
```

Die output bevestigt dat je succesvol **tekst uit een afbeelding** hebt geëxtraheerd en **tekst hebt verkregen via OCR** in één enkele run.

---

## Stap 4: Pas de workflow aan – Van **Java‑afbeelding naar tekst** in echte projecten

Hoewel de demo minimaal is, hebben real‑world toepassingen vaak iets meer nodig:

| Scenario | Wat aan te passen | Reden |
|----------|-------------------|-------|
| **Batchverwerking** | Loop over een `List<Path>` en sla elk resultaat op in een database. | Vermindert handmatig werk wanneer je honderden foto’s hebt. |
| **Verschillende afbeeldingsformaten** | Gebruik `ImageIO.read(new File(path))` om voor te verwerken, en geef vervolgens de `BufferedImage` door aan `ocrEngine.getImage().loadFromBufferedImage(bufImg)`. | Ondersteunt PNG, BMP, of zelfs PDF’s na conversie. |
| **Prestatie‑afstemming** | Roep `ocrEngine.getEngineOptions().setSpeed(OcrEngine.Speed.FAST)` aan als je akkoord gaat met iets lagere nauwkeurigheid. | Versnelt herkenning op low‑end hardware. |
| **Post‑processing** | Trim whitespace, vervang veelvoorkomende OCR‑fouten (`0` → `O`, `1` → `I`). | Verbetert de kwaliteit van downstream data. |

Deze variaties behouden het kernidee – **tekst herkennen van foto** – terwijl ze je flexibiliteit geven voor productie‑workloads.

---

## Veelvoorkomende valkuilen & pro‑tips

1. **Verkeerde taalinstelling** – Als je stap 2 vergeet, valt de engine terug op Engels, waardoor Cyrillische tekens onleesbaar worden. Controleer altijd de taalcode.  
2. **Afbeeldingskwaliteit** – Lage resolutie of onscherpe foto’s verminderen de nauwkeurigheid. Pre‑process met contrastversterking of binarisatie indien nodig.  
3. **Bestandspad‑eigenaardigheden** – Op Windows moeten backslashes geescaped worden (`C:\\images\\file.jpg`). Gebruik `Path.of(...)` uit `java.nio.file` om dit te omzeilen.  
4. **Geheugenlekken** – `OcrEngine` houdt native resources vast. Roep `ocrEngine.dispose()` aan wanneer je klaar bent, vooral in langdurige services.  
5. **Thread‑veiligheid** – De engine is niet thread‑safe out‑of‑the‑box. Maak een aparte instantie per thread of synchroniseer de toegang.

---

## Volledig werkend voorbeeld (alles‑in‑één)

Hieronder vind je één enkel bestand dat je kunt copy‑pasten in elke IDE. Het bevat de `dispose()`‑aanroep en een kleine helper‑methode om de code net iets netter te maken.

```java
package com.example.ocr;

import com.asprise.ocr.OcrEngine;
import com.asprise.ocr.OcrLanguage;
import java.nio.file.Path;

/**
 * Complete, runnable demo that extracts text from an image using Java OCR.
 */
public class FullDemo {

    public static void main(String[] args) {
        // Path to the image – change this to your own file.
        Path imgPath = Path.of("YOUR_DIRECTORY/ukrainian_sign.jpg");

        // Run the OCR workflow and capture the output.
        String result = extractTextFromImage(imgPath, OcrLanguage.UKRAINIAN);
        if (result != null) {
            System.out.println("=== OCR Result ===");
            System.out.println(result);
        }
    }

    /**
     * Core method that encapsulates the 5‑step OCR process.
     *
     * @param imagePath Path to the image file.
     * @param language  Desired OCR language.
     * @return Recognized text, or {@code null} if something went wrong.
     */
    private static String extractTextFromImage(Path imagePath, OcrLanguage language) {
        OcrEngine engine = new OcrEngine();
        try {
            // 1️⃣ Set language
            engine.getEngineOptions().setLanguage(language);

            // 2️⃣ Load image
            engine.getImage().loadFromFile(imagePath.toString());

            // 3️⃣ Recognize and return text
            return engine.recognize().getText();
        } catch (Exception e) {
            System.err.println("Error during OCR: " + e.getMessage());
            return null;
        } finally {
            // 4️⃣ Release native resources
            engine.dispose();
        }
    }
}
```

Het uitvoeren van dit programma levert dezelfde console‑output op als eerder getoond. Voel je vrij om `OcrLanguage.UKRAINIAN` te vervangen door `OcrLanguage.ENGLISH` of een andere ondersteunde taal om te zien hoe de engine zich aanpast.

---

## Conclusie

We hebben alles doorlopen wat je nodig hebt om **tekst uit een afbeelding** te extraheren met Java: van het toevoegen van de OCR‑dependency, tot **afbeelding laden voor OCR**, 

## Gerelateerde tutorials

- [recognize text image with Aspose OCR – Full Java OCR Tutorial](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Convert Image to Text in Java using Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}