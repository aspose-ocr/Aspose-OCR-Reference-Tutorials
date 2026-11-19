---
category: general
date: 2026-06-06
description: Haal tekst uit gescande afbeeldingen met Aspose OCR voor Java. Leer hoe
  je tekst uit tiff‑bestanden kunt herkennen met parallelle verwerking.
draft: false
keywords:
- extract text from scanned image
- recognize text from tiff
- Aspose OCR Java tutorial
- parallel OCR processing
- Java image recognition
language: nl
og_description: Tekst extraheren uit gescande afbeelding met Aspose OCR. Deze gids
  laat zien hoe je tekst uit tiff‑bestanden efficiënt kunt herkennen met Java.
og_title: Tekst extraheren uit gescande afbeelding – Aspose OCR Java‑tutorial
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Extract text from scanned image using Aspose OCR for Java. Learn how
    to recognize text from tiff files with parallel processing.
  headline: Extract Text from Scanned Image in Java – Complete Aspose OCR Guide
  type: TechArticle
- description: Extract text from scanned image using Aspose OCR for Java. Learn how
    to recognize text from tiff files with parallel processing.
  name: Extract Text from Scanned Image in Java – Complete Aspose OCR Guide
  steps:
  - name: Maven users
    text: 'Add the following dependency to your `pom.xml`:'
  - name: Manual JAR setup
    text: Download the latest `aspose-ocr-xx.jar` from the Aspose website and place
      it on your classpath.
  - name: Expected Output
    text: '``` === Extracted Text === Invoice Number: 12345 Date: 2024‑05‑01 Total:
      $1,250.00 ... ```'
  - name: What’s Next?
    text: '- **Batch processing**: Loop over a directory of TIFFs, store each result
      in its own file. - **Integrate with Elasticsearch**: Index the extracted text
      for fast full‑text search. - **Add language detection**: Use `OcrLanguage.AutoDetect`
      for multi‑lingual documents.'
  type: HowTo
- questions:
  - answer: Absolutely. `OcrInputImage` accepts any format that Java’s ImageIO can
      read. Just replace the file extension in the path.
    question: Does this work with PNG or JPEG files?
  - answer: You could, but remember other services may need CPU cycles. A good rule
      of thumb is “total cores – 1” for dedicated OCR workers.
    question: My server has 8 cores—should I set `setMaxThreads(8)`?
  - answer: 'Check that the image isn’t completely white, that you set the correct
      language, and that the resolution is at least 200 DPI. Low‑quality scans often
      need pre‑processing (deskew, contrast boost) before feeding them to Aspose OCR.
      --- ## Wrap‑Up We’ve just **extracted text from scanned image** files u'
    question: What if the OCR result is empty?
  type: FAQPage
tags:
- Java
- OCR
- Aspose
- Image Processing
title: Tekst extraheren uit gescande afbeelding in Java – Complete Aspose OCR-gids
url: /nl/java/advanced-ocr-techniques/extract-text-from-scanned-image-in-java-complete-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tekst extraheren uit gescande afbeelding – Complete Aspose OCR-gids

Heb je ooit **tekst uit een gescande afbeelding** moeten extraheren maar zat je vast bij het “hoe?”? Je bent niet de enige. Of je nu oude archieven digitaliseert, gegevens uit facturen haalt, of een doorzoekbare PDF-bibliotheek bouwt, betrouwbare tekst uit een TIFF-scan halen kan een knelpunt zijn.  

Goed nieuws: met Aspose OCR for Java kun je **tekst herkennen uit tiff**‑bestanden in slechts een paar regels code, en zelfs extra snelheid halen door de engine te beperken tot een handvol CPU‑kernen. In deze tutorial lopen we het volledige proces door – van het instellen van de bibliotheek tot het verwerken van het resultaat – zodat je meteen een werkend voorbeeld kunt copy‑pasten.

## Wat deze tutorial behandelt

- Installeren van Aspose OCR for Java (Maven of handmatige JAR)
- Laden van een grote gescande TIFF‑afbeelding
- Configureren van de engine om tot 4 threads te gebruiken (parallel OCR)
- Het OCR‑proces uitvoeren en de geëxtraheerde tekst afdrukken
- Veelvoorkomende valkuilen (geheugen, multi‑page TIFF’s) en hoe deze te vermijden
- Snelle prestatie‑tip: wanneer `setMaxThreads` af te stemmen

Aan het einde kun je **tekst uit gescande afbeelding**‑bestanden betrouwbaar extraheren, en begrijp je waarom het afstemmen van het aantal threads van belang is wanneer je *tekst herkent uit tiff* in een productie‑pipeline.

---

![voorbeeld van tekst extraheren uit gescande afbeelding](example.png "Schermafbeelding die de geëxtraheerde tekst van een gescande TIFF-afbeelding toont")

## Vereisten

Voordat we beginnen, zorg dat je het volgende hebt:

1. **Java Development Kit (JDK) 8+** – elke recente versie werkt.
2. **Maven** (of de mogelijkheid om JAR‑s handmatig toe te voegen) – we gebruiken Maven voor de eenvoud.
3. Een **Aspose OCR for Java**‑licentie (de gratis evaluatie werkt, maar voegt een watermerk toe).  
4. Een **grote TIFF‑scan** (bijv. `large_scan.tif`) die je wilt verwerken.

Als een van deze onbekend klinkt, geen zorgen – elke stap wordt hieronder uitgelegd.

## Stap 1: Voeg Aspose OCR toe aan je project

### Maven‑gebruikers

Voeg de volgende dependency toe aan je `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- check the latest version on Maven Central -->
</dependency>
```

### Handmatige JAR‑installatie

Download de nieuwste `aspose-ocr-xx.jar` van de Aspose‑website en plaats deze op je classpath.  

> **Pro tip:** Bewaar de JAR in een `libs/`‑map en verwijs ernaar in de projectinstellingen van je IDE. Dit voorkomt later “class not found” verrassingen.

## Stap 2: Maak een eenvoudige Java‑klasse

Maak een bestand genaamd `ParallelOcrDemo.java` in je source‑map (`src/main/java`). Deze klasse bevat de volledige OCR‑workflow.

```java
package com.example.ocr;

import com.aspose.ocr.*;

public class ParallelOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 2.1: Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2.2: Load the scanned TIFF image you want to process
        // Replace the path with the actual location of your image
        ocrEngine.setImage(new OcrInputImage("YOUR_DIRECTORY/large_scan.tif"));

        // Step 2.3: Limit the engine to use up to 4 CPU cores.
        // This is useful on servers where you don't want to hog all cores.
        ocrEngine.getSettings().setMaxThreads(4);

        // Step 2.4: Run the OCR operation
        OcrResult ocrResult = ocrEngine.process();

        // Step 2.5: Output the recognized text to the console
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

> **Waarom we threads beperken:** Standaard probeert Aspose OCR elke core te gebruiken, wat andere services op een gedeelde machine kan verhongeren. Door `setMaxThreads(4)` in te stellen, vertelt je de engine om tot vier parallelle workers te draaien – genoeg voor een merkbare snelheidswinst op de meeste moderne CPU’s zonder alle bronnen te monopoliseren.

## Stap 3: Compileer en voer uit

Open een terminal in de project‑root en voer uit:

```bash
mvn clean compile exec:java -Dexec.mainClass="com.example.ocr.ParallelOcrDemo"
```

Als je geen Maven gebruikt, compileer dan met `javac` en voer uit:

```bash
javac -cp "libs/*" src/main/java/com/example/ocr/ParallelOcrDemo.java
java -cp "libs/*:src/main/java" com.example.ocr.ParallelOcrDemo
```

### Verwachte uitvoer

```
=== Extracted Text ===
Invoice Number: 12345
Date: 2024‑05‑01
Total: $1,250.00
...
```

De console toont de platte‑tekstversie van wat er op de gescande pagina stond. Als de afbeelding meerdere pagina’s bevat, concateneert Aspose OCR ze in volgorde.

## Stap 4: Multi‑page TIFF’s verwerken (randgeval)

Een veelvoorkomend scenario is een **multi‑page TIFF** – denk aan een gescand boek. Standaard leest `OcrInputImage` alleen het eerste frame. Om alle pagina’s te verwerken, gebruik je `OcrInputImage` met een `FileInputStream` en schakel je multi‑page‑ondersteuning in:

```java
import java.io.FileInputStream;
import com.aspose.ocr.*;

FileInputStream fis = new FileInputStream("YOUR_DIRECTORY/multi_page.tif");
ocrEngine.setImage(new OcrInputImage(fis, true)); // 'true' enables multi‑page
```

Nu zal `ocrEngine.process()` één enkele `OcrResult` teruggeven die de samengevoegde tekst van elke pagina bevat.

## Stap 5: Fijn afstellen van herkenningsnauwkeurigheid

Als je **vervormde tekens** of ontbrekende woorden opmerkt, probeer dan deze aanpassingen:

| Instelling | Wat het doet | Wanneer te gebruiken |
|------------|--------------|----------------------|
| `ocrEngine.getSettings().setLanguage(OcrLanguage.English)` | Forceert het Engelse taalmodel (sneller, nauwkeuriger voor Engelse scans) | Je document is eentalig Engels |
| `ocrEngine.getSettings().setResolution(300)` | Schaltt lage‑resolutie afbeeldingen op voordat ze worden herkend | Scans onder 200 DPI |
| `ocrEngine.getSettings().setNoiseRemoval(true)` | Probeert vlekjes en artefacten te verwijderen | Scans met veel ruis |

Voorbeeld‑fragment:

```java
ocrEngine.getSettings().setLanguage(OcrLanguage.English);
ocrEngine.getSettings().setResolution(300);
ocrEngine.getSettings().setNoiseRemoval(true);
```

## Stap 6: Resultaten exporteren naar een bestand

Afdrukken naar de console is prima voor demo’s, maar productiecodel schrijft het resultaat meestal ergens nuttigs weg:

```java
import java.io.FileWriter;
import java.io.IOException;

// After processing
String extractedText = ocrResult.getText();
try (FileWriter writer = new FileWriter("output.txt")) {
    writer.write(extractedText);
}
System.out.println("Text saved to output.txt");
```

Nu heb je een platte‑tekst‑bestand dat je kunt voeden aan een zoekindex, een database, of een downstream‑analytics‑pipeline.

---

## Veelgestelde vragen (FAQ)

**Q: Werkt dit ook met PNG‑ of JPEG‑bestanden?**  
A: Absoluut. `OcrInputImage` accepteert elk formaat dat Java’s ImageIO kan lezen. Vervang gewoon de bestandsextensie in het pad.

**Q: Mijn server heeft 8 cores – moet ik `setMaxThreads(8)` instellen?**  
A: Dat kan, maar onthoud dat andere services CPU‑cycli nodig hebben. Een goede vuistregel is “totaal cores – 1” voor toegewijde OCR‑workers.

**Q: Wat als het OCR‑resultaat leeg is?**  
A: Controleer of de afbeelding niet volledig wit is, of je de juiste taal hebt ingesteld, en of de resolutie minstens 200 DPI bedraagt. Scans van lage kwaliteit hebben vaak voorafgaande bewerkingen (kantlijncorrectie, contrastverhoging) nodig voordat ze aan Aspose OCR worden gevoed.

## Afronding

We hebben zojuist **tekst uit gescande afbeelding**‑bestanden geëxtraheerd met Aspose OCR for Java, en je weet nu hoe je **tekst herkent uit tiff** efficiënt kunt doen met parallelle verwerking. De volledige code staat in de bovenstaande fragmenten, en je kunt ze direct in je eigen project copy‑pasten.

### Wat is het volgende?

- **Batchverwerking**: Loop door een map met TIFF‑bestanden en sla elk resultaat op in een eigen bestand.  
- **Integreren met Elasticsearch**: Index de geëxtraheerde tekst voor snelle full‑text zoekopdrachten.  
- **Taaldetectie toevoegen**: Gebruik `OcrLanguage.AutoDetect` voor meertalige documenten.  

Experimenteer met deze ideeën, en je zet snel een berg gescande papierwerk om in doorzoekbare, bruikbare data.

Happy coding, en laat gerust een reactie achter als je ergens vastloopt!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids zijn gedemonstreerd. Elke bron bevat complete werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [How to recognize tiff with Aspose.OCR for Java](/ocr/english/java/ocr-operations/recognize-tiff/)
- [Extract Text Images – OCR Basics with Aspose.OCR for Java](/ocr/english/java/ocr-basics/)
- [Extract Text from Image Java with Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}