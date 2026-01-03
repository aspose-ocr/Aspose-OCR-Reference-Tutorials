---
category: general
date: 2026-01-02
description: Converteer afbeeldingen naar tekst met Java en Aspose OCR. Beheers batch‑OCR‑verwerking,
  lees afbeeldingen uit een map en filter bestanden op extensie.
draft: false
keywords:
- convert images to text
- batch ocr processing
- read images from folder
- extract text from png
- filter files by extension
language: nl
og_description: Converteer afbeeldingen snel naar tekst met Java. Deze tutorial behandelt
  batch-OCR-verwerking, het lezen van afbeeldingen uit een map en het filteren van
  bestanden op extensie.
og_title: Afbeeldingen converteren naar tekst in Java – Complete batch OCR-gids
tags:
- OCR
- Java
- Aspose
title: Afbeeldingen naar Tekst Converteren in Java – Gids voor Batch-OCR Verwerking
url: /nl/java/ocr-operations/convert-images-to-text-in-java-batch-ocr-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Afbeeldingen naar Tekst Converteren in Java – Batch OCR Verwerkingsgids

Heb je ooit **afbeeldingen naar tekst moeten converteren**, maar wist je niet hoe je tientallen bestanden tegelijk moest verwerken? Je bent niet de enige—ontwikkelaars worstelen voortdurend met het extraheren van gegevens uit PNG's, JPG's en andere scans. Het goede nieuws? Met Aspose OCR kun je in enkele minuten een batch‑OCR‑verwerkingspipeline opzetten, afbeeldingen lezen uit mapstructuren en zelfs bestanden filteren op extensie, zodat je alleen werkt aan wat echt belangrijk is.

In deze tutorial bouwen we een zelfstandige Java‑applicatie die een map doorloopt, elke `.png` of `.jpg` selecteert, elke afbeelding asynchroon naar Aspose OCR stuurt en de geëxtraheerde tekst in de oorspronkelijke volgorde afdrukt. Aan het einde heb je een herbruikbaar code‑fragment dat je in elk project kunt plaatsen dat **afbeeldingen naar tekst moet converteren** op schaal.

![Convert images to text example](https://example.com/convert-images-to-text.png "Screenshot of Java console output showing converted text from PNG files")

## Wat je gaat bouwen

- Een enkele `AsposeOCR` engine die gedeeld wordt over threads (efficiënt en thread‑veilig).  
- Een `ParallelRecognizer` die OCR‑taken parallel uitvoert, perfect voor **batch OCR processing**.  
- Logica die **afbeeldingen uit map leest** met `java.nio.file.Files`.  
- Eenvoudige filters om **tekst uit PNG**‑bestanden te extraheren terwijl JPG‑bestanden nog steeds worden verwerkt.  
- Schone afsluiting van de interne thread‑pool om resource‑lekken te voorkomen.

### Vereisten

- Java 17 (of een recente LTS‑versie).  
- Maven of Gradle om de Aspose OCR‑bibliotheek te downloaden.  
- Een map vol PNG/JPG‑afbeeldingen die je wilt verwerken.  
- Basiskennis van Java‑streams—geen geavanceerde kennis vereist.

> **Pro tip:** Als je nog geen licentie hebt, biedt Aspose een gratis tijdelijke sleutel die je kunt gebruiken voor testen.

## Stap 1 – Het project opzetten en Aspose OCR toevoegen

Maak eerst een nieuw Maven‑project aan (of Gradle, naar keuze). Voeg de Aspose OCR‑dependency toe aan `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Check the latest version on Maven Central -->
</dependency>
```

> **Waarom dit belangrijk is:** Het vooraf declareren van de dependency zorgt ervoor dat de compiler `AsposeOCR`, `ParallelRecognizer` en gerelateerde klassen kan vinden. Het garandeert bovendien dat dezelfde versie op alle machines wordt gebruikt, wat cruciaal is voor reproduceerbare **batch OCR processing**.

## Stap 2 – Afbeeldingen naar Tekst Converteren – Initialiseer de OCR‑Engine

We hebben slechts **één** OCR‑engine‑instantie nodig voor de volledige uitvoering. Het delen ervan over threads bespaart geheugen en versnelt de verwerking omdat de engine de taalpakketten slechts één keer laadt.

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

> **Uitleg:** `ParallelRecognizer` verpakt de engine in een thread‑pool. Wanneer je veel bestanden indient, krijgt elk een eigen werkthread, waardoor echte paralleliteit op multi‑core CPU's mogelijk wordt.

## Stap 3 – Afbeeldingen uit Map Lezen – Doorloop de Directory‑Boom

Nu moeten we **afbeeldingen uit een map lezen** en elke PNG of JPG verzamelen. De `Files.walk`‑API maakt dit tot één regel code, maar we voegen een filter toe om **tekst uit PNG** alleen wanneer nodig te extraheren.

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

> **Waarom we hier filteren:** Met `filter` kunnen we **bestanden op extensie filteren** in een vroeg stadium, wat later onnodige I/O vermindert. Het houdt de code bovendien leesbaar—geen complexe regexes nodig.

## Stap 4 – Batch OCR Processing – Taken Asynchroon Indienen

Met de lijst van bestanden klaar, sturen we elk pad naar de `ParallelRecognizer`. De `recognizeAsync`‑methode retourneert een `Future<OcrResult>` die we opslaan voor later ophalen.

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

> **Wat er achter de schermen gebeurt:** Elke oproep plaatst een taak in de interne executor‑service van de recognizer. De taken draaien parallel, zodat een map met 100 afbeeldingen in een fractie van de tijd kan worden verwerkt die een enkel‑threaded lus zou kosten.

## Stap 5 – Resultaten Ophalen in Originele Volgorde – Bestandsvolgorde Behouden

Omdat we de futures in dezelfde volgorde als `imagePaths` hebben opgeslagen, kunnen we eenvoudig over de lijst itereren en `get()` aanroepen. De oproep blokkeert alleen tot die specifieke afbeelding klaar is, waardoor de volgorde behouden blijft zonder extra administratie.

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

**Sample console output** (truncated for brevity):

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

> **Afhandeling van randgevallen:** Als een bepaalde afbeelding een uitzondering veroorzaakt (beschadigd bestand, niet‑ondersteund formaat), vangen we deze op en gaan we door met de rest—een essentiële gewoonte voor betrouwbare **batch OCR processing**‑pijplijnen.

## Stap 6 – Opruimen – De Recognizer Afsluiten

Vergeet nooit de interne thread‑pool af te sluiten; anders kan je JVM blijven hangen bij het afsluiten.

```java
// Step 6: Shut down the recognizer to clean up its internal thread pool
parallelRecognizer.shutdown();
```

Dat is alles! Het programma doorloopt nu elke map, filtert op PNG/JPG‑bestanden, voert OCR parallel uit en drukt de resultaten af.

## Volledig Werkend Voorbeeld

Hieronder staat de volledige, kant‑en‑klaar te kopiëren Java‑klasse. Vervang `"YOUR_DIRECTORY"` door het pad naar je afbeeldingsmap en voer het uit vanuit je IDE of de commandoregel.

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

Voer de klasse uit, zie de console vullen met geëxtraheerde strings, en vier het feit dat je zojuist **afbeeldingen naar tekst hebt geconverteerd** zonder een enkele lus te schrijven die blokkeert op I/O.

## Veelgestelde Vragen (FAQ's)

**V: Kan ik ook PDF's of TIFF's verwerken?**  
A: Absoluut. Aspose OCR ondersteunt veel formaten—voeg simpelweg de juiste bestandsextensies toe aan het filter in Stap 2.

**V: Wat als ik een andere taal nodig heb, bijvoorbeeld Spaans?**  
A: Verander `RecognitionLanguage.ENGLISH` naar `RecognitionLanguage.SPANISH`. Zorg ervoor dat het taalpakket geïnstalleerd is (Aspose bevat de meeste grote talen standaard).

**V: Mijn map bevat sub‑mappen—worden die gescand?**  
A: Ja. `Files.walk` doorloopt de volledige boom recursief, zodat elke geneste PNG/J

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}