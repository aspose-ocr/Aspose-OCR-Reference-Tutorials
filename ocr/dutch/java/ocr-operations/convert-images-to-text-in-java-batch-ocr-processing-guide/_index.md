---
category: general
date: 2026-08-28
description: Leer hoe je tekst uit png-afbeeldingen in Java kunt extraheren met Aspose
  OCR. Deze tutorial behandelt batch OCR-verwerking, het lezen van afbeeldingen uit
  een folder, en het filteren van bestanden op extensie.
draft: false
keywords:
- extract text from png
- read images from folder
- filter files by extension
- how to batch ocr
- aspose ocr java tutorial
lastmod: 2026-08-28
og_description: Leer hoe je tekst uit png-afbeeldingen in Java kunt extraheren met
  Aspose OCR. Deze tutorial behandelt batch OCR-verwerking, het lezen van afbeeldingen
  uit een folder, en het filteren van bestanden op extensie.
og_image_alt: 'Developer guide: extract text from png images in Java using Aspose
  OCR'
og_title: Hoe tekst uit png in Java te extraheren – batch OCR-gids
schemas:
- author: Aspose
  dateModified: '2026-08-28'
  description: Learn how to extract text from png images in Java using Aspose OCR.
    This tutorial covers batch OCR processing, reading images from a folder, and filtering
    files by extension.
  headline: How to extract text from png in Java – batch OCR guide
  type: TechArticle
- questions:
  - answer: Absolutely. Aspose OCR supports 30+ formats—including PDF, TIFF, BMP,
      and GIF—so just add the desired extensions to the filter in the directory‑walk
      step.
    question: Can I process PDFs or TIFFs as well?
  - answer: Change `RecognitionLanguage.ENGLISH` to `RecognitionLanguage.SPANISH`
      (or any supported language). The language packs are bundled with the library,
      so no extra download is required.
    question: What if I need a language other than English, such as Spanish?
  - answer: Yes. `Files.walk` traverses the entire tree recursively, so every nested
      PNG/J
    question: My folder contains sub‑folders—will they be scanned?
  - answer: Enable streaming mode by calling `ocrEngine.setUseStreaming(true)`. This
      tells the engine to read the image in chunks, dramatically reducing peak memory
      usage.
    question: How do I handle extremely large images that exceed 200 MB?
  - answer: Yes. When constructing `ParallelRecognizer`, pass the desired maximum
      thread count as the second argument (e.g., `new ParallelRecognizer(ocrEngine,
      4)`).
    question: Is there a way to limit the number of concurrent OCR threads?
  type: FAQPage
tags:
- OCR
- Java
- Aspose
title: Hoe tekst uit png in Java te extraheren – batch OCR-gids
url: /nl/java/ocr-operations/convert-images-to-text-in-java-batch-ocr-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe tekst uit png extraheren in Java – batch OCR-gids

Als je ooit **tekst uit png** bestanden moest extraheren maar niet wist hoe je de operatie kon opschalen voorbij een handvol afbeeldingen, ben je hier op de juiste plek. Veel ontwikkelaars beginnen met een OCR‑aanroep voor één afbeelding en lopen al snel tegen prestatie‑limieten aan wanneer de map groeit tot tientallen of honderden bestanden. Met Aspose OCR voor Java kun je een robuuste batch‑OCR‑pipeline opzetten die een directory doorloopt, alleen de afbeeldings‑types filtert die je nodig hebt, herkenning parallel uitvoert en de resultaten in dezelfde volgorde als de bronbestanden teruggeeft. Aan het einde van deze gids heb je een kant‑klaar Java‑fragment dat **batch OCR processing** betrouwbaar en efficiënt afhandelt.

![Voorbeeld van afbeeldingen naar tekst converteren](https://example.com/convert-images-to-text.png "Schermafbeelding van Java console‑output die geconverteerde tekst van PNG‑bestanden toont")

## Snelle antwoorden
- **Welke bibliotheek verwerkt OCR?** Aspose OCR for Java.
- **Kan ik PNG en JPG samen verwerken?** Ja – het voorbeeld filtert beide extensies.
- **Is de OCR‑engine thread‑safe?** Een enkele gedeelde `AsposeOCR`‑instantie is veilig voor gelijktijdig gebruik.
- **Heb ik een licentie nodig voor testen?** Een gratis tijdelijke sleutel is beschikbaar van Aspose.
- **Worden sub‑mappen automatisch gescand?** `Files.walk` doorloopt de volledige boom recursief.

## Wat is tekst uit png extraheren?

`extract text from png` verwijst naar het proces waarbij optische tekenherkenning (OCR) wordt toegepast op Portable Network Graphics‑bestanden zodat de zichtbare tekens doorzoekbare, bewerkbare strings worden. De engine van Aspose OCR leest pixeldata, identificeert glyph‑vormen en retourneert Unicode‑tekst in één methode‑aanroep.

## Waarom Aspose OCR voor Java gebruiken?

Aspose OCR ondersteunt **30+ talen**, verwerkt tot **500 afbeeldingen per minuut** op een standaard 8‑core server, en kan bestanden tot **200 MB** aan zonder de volledige afbeelding in het geheugen te laden. Deze gekwantificeerde mogelijkheden betekenen dat je betrouwbaar grootschalige batch‑taken kunt uitvoeren op gewone hardware zonder geheugenlimieten te raken.

## Vereisten
- Java 17 (of een recente LTS‑versie).
- Maven of Gradle voor afhankelijkheidsbeheer.
- Een map met PNG/JPG‑afbeeldingen die u wilt verwerken.
- Basiskennis van Java‑streams en het `java.nio.file`‑pakket.
- (Optioneel) Een tijdelijke licentiesleutel voor Aspose OCR voor evaluatie.

> **Pro tip:** De gratis tijdelijke sleutel verloopt na 30 dagen, maar geeft u volledige API‑toegang voor testen.

## Hoe behoudt de batch‑OCR‑pipeline de volgorde?

`Future<OcrResult>` vertegenwoordigt een nog te voltooien OCR‑resultaat dat kan worden opgehaald zodra de verwerking is afgerond. De pipeline behoudt de oorspronkelijke bestandsvolgorde door de `Future<OcrResult>`‑objecten in een lijst op te slaan die de volgorde van de invoer‑`Path`‑collectie weerspiegelt. Wanneer je later over de futures itereert en `get()` aanroept, blokkeert elke oproep alleen voor de bijbehorende afbeelding, zodat de uitvoersequentie overeenkomt met de invoersequentie zonder extra sorteerlogica.

## Wat is Aspose OCR voor Java?

`AsposeOCR` is de kernklasse van de Aspose OCR‑bibliotheek die alle taal‑pakketten, herkenningsinstellingen en interne native resources omvat. De klasse is ontworpen om één keer per levensduur van de applicatie te worden geïnstantieerd en veilig te worden gedeeld tussen meerdere threads. Omdat de taaldata slechts één keer wordt geladen, vermindert het hergebruiken van dezelfde instantie de initialisatie‑overhead en verbetert het de doorvoer voor batch‑operaties.

## Hoe het project op te zetten en Aspose OCR toe te voegen

Eerst maak je een Maven‑ (of Gradle‑)project aan en voeg je de Aspose OCR‑dependency toe aan je `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>24.10</version>
</dependency>
```

> **Waarom dit belangrijk is:** Het vooraf declareren van de dependency zorgt ervoor dat de compiler `AsposeOCR`, `ParallelRecognizer` en gerelateerde klassen kan vinden. Het garandeert ook dat dezelfde versie op alle machines wordt gebruikt, wat cruciaal is voor reproduceerbare **batch OCR processing**.

Ververs je IDE nadat de build is voltooid; je zou nu de Aspose‑pakketten onder **External Libraries** moeten zien.

## Hoe de OCR‑engine te initialiseren – één instantie delen

`AsposeOCR` is de hoofd‑OCR‑engineklasse die wordt geleverd door de Aspose OCR‑bibliotheek. We hebben slechts **één** OCR‑engine‑instantie nodig voor de volledige uitvoering. Het delen ervan tussen threads bespaart geheugen en versnelt de verwerking omdat de engine taal‑pakketten slechts één keer laadt.

```java
AsposeOCR ocrEngine = new AsposeOCR("YOUR_LICENSE_KEY");
```

`AsposeOCR` is thread‑safe, dus je kunt het veilig doorgeven aan een `ParallelRecognizer` die een pool van werk‑threads beheert.

> **Uitleg:** `ParallelRecognizer` wikkelt de engine in een thread‑pool. Wanneer je veel bestanden indient, krijgt elk zijn eigen werk‑thread, waardoor echte paralleliteit op multi‑core CPU’s mogelijk is.

## Hoe afbeeldingen uit een map te lezen – doorloop de directory‑boom

`Files.walk` is een Java NIO‑methode die recursief een bestandboom doorloopt en een stream van `Path`‑objecten retourneert. Nu moeten we **afbeeldingen uit een map lezen** en elke PNG of JPG verzamelen. De `Files.walk`‑API maakt dit tot één regel, maar we voegen een filter toe om **tekst uit png** alleen wanneer nodig te extraheren.

```java
List<Path> imagePaths = Files.walk(Paths.get("YOUR_DIRECTORY"))
    .filter(Files::isRegularFile)
    .filter(p -> {
        String lower = p.toString().toLowerCase();
        return lower.endsWith(".png") || lower.endsWith(".jpg");
    })
    .collect(Collectors.toList());
```

> **Waarom we hier filteren:** Met `filter` kunnen we **bestanden op extensie** vroeg filteren, waardoor onnodige I/O later wordt vermeden. Het houdt de code bovendien leesbaar — geen complexe regex‑patronen nodig.

## Hoe OCR‑taken asynchroon in te dienen

`recognizeAsync` dient een afbeelding in bij de OCR‑engine voor asynchrone verwerking en retourneert een `Future<OcrResult>` die het nog te voltooien resultaat vertegenwoordigt. Met de lijst van bestanden klaar, duwen we elk pad naar de `ParallelRecognizer`. De `recognizeAsync`‑methode retourneert een `Future<OcrResult>` die we later opslaan voor ophalen.

```java
ParallelRecognizer recognizer = new ParallelRecognizer(ocrEngine, Runtime.getRuntime().availableProcessors());
List<Future<OcrResult>> futures = new ArrayList<>();

for (Path imagePath : imagePaths) {
    futures.add(recognizer.recognizeAsync(imagePath));
}
```

> **Wat er onder de motorkap gebeurt:** Elke oproep plaatst een taak in de interne executor‑service van de recognizer. De taken draaien parallel, zodat een map met 100 afbeeldingen in een fractie van de tijd kan worden verwerkt die een enkel‑threaded lus zou kosten.

## Hoe resultaten op te halen terwijl de bestandsvolgorde behouden blijft

`Future<OcrResult>` bevat het resultaat van een asynchrone OCR‑taak en biedt een `get()`‑methode om de herkende tekst te verkrijgen. Omdat we de futures in dezelfde volgorde als `imagePaths` hebben opgeslagen, kunnen we eenvoudig over de lijst itereren en `get()` aanroepen. De oproep blokkeert alleen tot die specifieke afbeelding klaar is, waardoor de volgorde behouden blijft zonder extra administratie.

```java
for (int i = 0; i < futures.size(); i++) {
    try {
        OcrResult result = futures.get(i).get();
        System.out.println("File: " + imagePaths.get(i).getFileName());
        System.out.println("Text: " + result.getText());
    } catch (Exception e) {
        System.err.println("Failed to process " + imagePaths.get(i) + ": " + e.getMessage());
    }
}
```

**Voorbeeld console‑output** (afgekapt voor beknoptheid):

```
File: invoice1.png
Text: Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
...
```

> **Edge case handling:** Als een bepaalde afbeelding een uitzondering veroorzaakt (beschadigd bestand, niet‑ondersteund formaat), vangen we deze op en gaan we door met de rest — een essentiële gewoonte voor betrouwbare **batch OCR processing**‑pipelines.

## Hoe bronnen opruimen – de recognizer afsluiten

`ParallelRecognizer.shutdown()` stopt de interne thread‑pool en zorgt ervoor dat alle OCR‑taken zijn voltooid voordat de applicatie afsluit. Vergeet nooit de interne thread‑pool te sluiten; anders kan je JVM blijven hangen bij het afsluiten.

```java
recognizer.shutdown();
```

Dat is alles! Het programma doorloopt nu elke directory, filtert PNG/JPG‑bestanden, voert OCR parallel uit en print de resultaten in de oorspronkelijke volgorde.

---

## Volledig werkend voorbeeld (kopiëren‑en‑plakken)

Hieronder staat de complete, kant‑klaar te gebruiken Java‑klasse. Vervang `"YOUR_DIRECTORY"` door het pad naar je afbeeldingsmap en voer het uit vanuit je IDE of de commandoregel.

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.ParallelRecognizer;
import com.aspose.ocr.OcrResult;
import java.nio.file.*;
import java.util.*;
import java.util.concurrent.*;
import java.util.stream.*;

public class BatchOcrDemo {
    public static void main(String[] args) throws Exception {
        // Initialise the OCR engine (single shared instance)
        AsposeOCR ocrEngine = new AsposeOCR("YOUR_LICENSE_KEY");

        // Create a parallel recognizer that uses a thread pool
        ParallelRecognizer recognizer = new ParallelRecognizer(ocrEngine,
                Runtime.getRuntime().availableProcessors());

        // Walk the directory and collect PNG/JPG files
        List<Path> imagePaths = Files.walk(Paths.get("YOUR_DIRECTORY"))
                .filter(Files::isRegularFile)
                .filter(p -> {
                    String lower = p.toString().toLowerCase();
                    return lower.endsWith(".png") || lower.endsWith(".jpg");
                })
                .collect(Collectors.toList());

        // Submit OCR jobs asynchronously
        List<Future<OcrResult>> futures = new ArrayList<>();
        for (Path imagePath : imagePaths) {
            futures.add(recognizer.recognizeAsync(imagePath));
        }

        // Retrieve results in the original order
        for (int i = 0; i < futures.size(); i++) {
            try {
                OcrResult result = futures.get(i).get();
                System.out.println("File: " + imagePaths.get(i).getFileName());
                System.out.println("Text: " + result.getText());
            } catch (Exception e) {
                System.err.println("Failed to process " + imagePaths.get(i) + ": " + e.getMessage());
            }
        }

        // Clean up the recognizer's thread pool
        recognizer.shutdown();
    }
}
```

Voer de klasse uit, zie de console vullen met geëxtraheerde strings, en vier het feit dat je **afbeeldingen naar tekst** hebt geconverteerd zonder een enkele lus die blokkeert op I/O.

---

## Veelgestelde vragen (FAQ's)

**Q: Kan ik ook PDF’s of TIFF’s verwerken?**  
A: Absoluut. Aspose OCR ondersteunt 30+ formaten — waaronder PDF, TIFF, BMP en GIF — dus voeg simpelweg de gewenste extensies toe aan het filter in de directory‑walk stap.

**Q: Wat als ik een andere taal nodig heb dan Engels, bijvoorbeeld Spaans?**  
A: Verander `RecognitionLanguage.ENGLISH` naar `RecognitionLanguage.SPANISH` (of een andere ondersteunde taal). De taal‑pakketten zijn gebundeld met de bibliotheek, dus er is geen extra download nodig.

**Q: Mijn map bevat sub‑mappen—zullen die worden gescand?**  
A: Ja. `Files.walk` doorloopt de volledige boom recursief, zodat elke geneste PNG/J

**Q: Hoe ga ik om met extreem grote afbeeldingen die groter zijn dan 200 MB?**  
A: Schakel streaming‑modus in door `ocrEngine.setUseStreaming(true)` aan te roepen. Dit laat de engine de afbeelding in delen lezen, waardoor het piek‑geheugengebruik drastisch wordt verminderd.

**Q: Is er een manier om het aantal gelijktijdige OCR‑threads te beperken?**  
A: Ja. Bij het construeren van `ParallelRecognizer` kun je het gewenste maximale aantal threads als tweede argument doorgeven (bijv. `new ParallelRecognizer(ocrEngine, 4)`).

---

**Last Updated:** 2026-08-28  
**Tested with:** Aspose OCR for Java 24.10  
**Author:** Aspose  

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Check the latest version on Maven Central -->
</dependency>
```

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.ParallelRecognizer;
import com.aspose.ocr.OcrResult;
import com.aspose.ocr.RecognitionLanguage;

// ...

// Step 2: Create a single OCR engine instance and a parallel recognizer that uses it
AsposeOCR ocrEngine = new AsposeOCR();               // Loads language data internally
ParallelRecognizer parallelRecognizer = new ParallelRecognizer(ocrEngine);
```

```java
import java.nio.file.*;
import java.util.*;
import java.util.stream.Collectors;

// ...

// Step 3: Find all PNG and JPG images in the target directory
Path imagesRoot = Paths.get("YOUR_DIRECTORY"); // <-- replace with your path
List<Path> imagePaths = Files.walk(imagesRoot)
        .filter(p -> {
            String name = p.toString().toLowerCase();
            return name.endsWith(".png") || name.endsWith(".jpg");
        })
        .collect(Collectors.toList());

if (imagePaths.isEmpty()) {
    System.out.println("No PNG or JPG files found in " + imagesRoot);
    return;
}
```

```java
import java.util.concurrent.*;

// ...

// Step 4: Submit each image for asynchronous recognition
List<Future<OcrResult>> recognitionFutures = new ArrayList<>();

for (Path image : imagePaths) {
    Future<OcrResult> future = parallelRecognizer.recognizeAsync(
            image.toString(),
            RecognitionLanguage.ENGLISH); // Change language if needed
    recognitionFutures.add(future);
}
```

```java
// Step 5: Retrieve and display the OCR results in the original order
for (int i = 0; i < recognitionFutures.size(); i++) {
    try {
        OcrResult result = recognitionFutures.get(i).get(); // blocks if not ready
        System.out.println("File: " + imagePaths.get(i).getFileName());
        System.out.println(result.getText()); // The extracted text
        System.out.println("-----");
    } catch (InterruptedException | ExecutionException e) {
        System.err.println("Failed to process " + imagePaths.get(i) + ": " + e.getMessage());
    }
}
```

```
File: invoice_001.png
Invoice #001
Date: 2024‑03‑15
Total: $1,250.00
-----
File: receipt_202403.jpg
Receipt
Item A - $45.00
Item B - $30.00
Grand Total: $75.00
-----
```

```java
// Step 6: Shut down the recognizer to clean up its internal thread pool
parallelRecognizer.shutdown();
```

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.ParallelRecognizer;
import com.aspose.ocr.OcrResult;
import com.aspose.ocr.RecognitionLanguage;

import java.nio.file.*;
import java.util.*;
import java.util.concurrent.*;
import java.util.stream.Collectors;

public class BatchParallelExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create a single OCR engine instance and a parallel recognizer that uses it
        AsposeOCR ocrEngine = new AsposeOCR();
        ParallelRecognizer parallelRecognizer = new ParallelRecognizer(ocrEngine);

        // Step 2: Find all PNG and JPG images in the target directory
        List<Path> imagePaths = Files.walk(Paths.get("YOUR_DIRECTORY"))
                .filter(p -> {
                    String lower = p.toString().toLowerCase();
                    return lower.endsWith(".png") || lower.endsWith(".jpg");
                })
                .collect(Collectors.toList());

        if (imagePaths.isEmpty()) {
            System.out.println("No images found – nothing to convert.");
            parallelRecognizer.shutdown();
            return;
        }

        // Step 3: Submit each image for asynchronous recognition
        List<Future<OcrResult>> recognitionFutures = new ArrayList<>();
        for (Path image : imagePaths) {
            recognitionFutures.add(
                    parallelRecognizer.recognizeAsync(
                            image.toString(),
                            RecognitionLanguage.ENGLISH));
        }

        // Step 4: Retrieve and display the OCR results in the original order
        for (int i = 0; i < recognitionFutures.size(); i++) {
            try {
                OcrResult result = recognitionFutures.get(i).get(); // blocks until processed
                System.out.println("File: " + imagePaths.get(i).getFileName());
                System.out.println(result.getText());
                System.out.println("-----");
            } catch (InterruptedException | ExecutionException e) {
                System.err.println("Error processing " + imagePaths.get(i) + ": " + e.getMessage());
            }
        }

        // Step 5: Shut down the recognizer to clean up its internal thread pool
        parallelRecognizer.shutdown();
    }
}
```

## Gerelateerde tutorials

- [Afbeeldingen naar tekst converteren in Java batch OCR-verwerkingsgids](/ocr/java/ocr-operations/convert-images-to-text-in-java-batch-ocr-processing-guide/)
- [Tekst lezen van afbeelding in Java volledige Aspose OCR-gids](/ocr/java/ocr-basics/read-text-from-image-in-java-complete-aspose-ocr-guide/)
- [Tekst extraheren uit afbeeldingen met Aspose.OCR – Toegestane tekens](/ocr/java/advanced-ocr-techniques/specify-allowed-characters/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}