---
category: general
date: 2026-05-03
description: Maak een vaste threadpool in Java om snel tekst uit afbeeldingen te extraheren.
  Leer hoe je OCR uitvoert, afbeeldingen naar tekst converteert en de prestaties verbetert
  met parallelle OCR‑verwerking.
draft: false
keywords:
- create fixed thread pool
- extract text from images
- how to run OCR
- convert image to text
- parallel OCR processing
language: nl
og_description: Maak een vaste threadpool in Java om snel tekst uit afbeeldingen te
  extraheren. Leer hoe je OCR uitvoert, afbeeldingen naar tekst converteert en de
  prestaties verbetert met parallelle OCR‑verwerking.
og_title: Maak een vaste threadpool voor parallelle OCR in Java
tags:
- Java
- OCR
- Multithreading
title: Maak een vaste threadpool voor parallelle OCR in Java
url: /nl/java/advanced-ocr-techniques/create-fixed-thread-pool-for-parallel-ocr-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Maak een vaste threadpool voor parallelle OCR in Java

Heb je ooit een **fixed thread pool** moeten maken om OCR‑taken te versnellen, maar wist je niet waar te beginnen? Je bent niet de enige. In veel beeldintensieve projecten is de bottleneck de single‑threaded OCR‑aanroep, en de oplossing is verrassend eenvoudig: start een pool van werkthreads en laat ze de bestanden parallel verwerken.  

In deze tutorial leer je hoe je **tekst uit afbeeldingen kunt extraheren** met Aspose OCR, hoe je **OCR efficiënt kunt uitvoeren**, en hoe je **afbeelding naar tekst kunt converteren** zonder je CPU te overbelasten. Aan het einde heb je een kant‑klaar Java‑programma dat **parallelle OCR‑verwerking** demonstreert op een handvol voorbeeldafbeeldingen.

## Wat je gaat bouwen

We zetten een kleine console‑applicatie in elkaar die:

* Een lijst met afbeeldingspaden (PNG, JPG, TIFF, BMP) leest.  
* **Een vaste threadpool maakt** met een grootte gelijk aan het aantal CPU‑kernen.  
* Een OCR‑taak voor elke afbeelding dispatcht.  
* De herkende tekst verzamelt en naar de console print.  
* De executor netjes afsluit.

Geen externe build‑tools, geen fancy frameworks—alleen plain Java en de Aspose OCR‑bibliotheek. Als je Java 8+ en een degelijke IDE hebt, ben je klaar om te starten.

## Vereisten

* **Java Development Kit (JDK) 8 of nieuwer** – de code gebruikt lambda‑expressies, dus oudere versies compileren niet.  
* **Aspose OCR for Java** – download de JAR van de Aspose‑website of haal hem op via Maven (`com.aspose:aspose-ocr`).  
* Een map met een paar test‑afbeeldingen (de code verwijst naar `YOUR_DIRECTORY`).  
* Basiskennis van Java‑concurrency (we leggen de rest uit).

> *Pro tip:* Als je Maven gebruikt, voeg dan de dependency toe aan je `pom.xml` en laat de IDE de classpath regelen.  

---

## Stap 1: Voeg de benodigde imports toe

Eerst halen we de klassen die we nodig hebben binnen bereik. Dit is niet zomaar boilerplate; elke import vertelt de JVM waar de OCR‑engine, beeldverwerkings‑utilities en de concurrency‑tools te vinden zijn die ons in staat stellen **fixed thread pool**‑instanties te **maken**.

```java
import com.aspose.ocr.*;
import java.util.*;
import java.util.concurrent.*;
```

* `com.aspose.ocr.*` – de core OCR‑API.  
* `java.util.*` – collecties voor het opslaan van afbeeldingspaden en resultaten.  
* `java.util.concurrent.*` – het concurrency‑pakket dat `ExecutorService` en `Future` bevat.

---

## Stap 2: Definieer de afbeeldingen die verwerkt moeten worden

Vervolgens maken we een lijst van de bestanden waarvan we **tekst uit afbeeldingen** willen **extraheren**. Het gebruik van `Arrays.asList` houdt de code beknopt en laat ons jouw eigen map invoegen zonder de rest van de logica aan te passen.

```java
List<String> imagePaths = Arrays.asList(
        "YOUR_DIRECTORY/image1.png",
        "YOUR_DIRECTORY/image2.jpg",
        "YOUR_DIRECTORY/image3.tif",
        "YOUR_DIRECTORY/image4.bmp"
);
```

Voel je vrij om meer items toe te voegen; de threadpool schaalt automatisch op basis van het aantal CPU‑kernen dat je hebt.

---

## Stap 3: **Create Fixed Thread Pool** passend bij de CPU‑kernen

Hier is het hart van de tutorial. We vragen de runtime hoeveel kernen beschikbaar zijn en laten de `Executors`‑factory ons een pool van precies die grootte geven. Waarom vast? Omdat een voorspelbaar aantal threads de gevreesde “thread‑explosie” voorkomt die het OS kan uitputten.

```java
int coreCount = Runtime.getRuntime().availableProcessors();
ExecutorService executor = Executors.newFixedThreadPool(coreCount);
```

* `availableProcessors()` geeft het aantal logische kernen terug (inclusief hyper‑threads).  
* `newFixedThreadPool(coreCount)` garandeert dat we nooit de capaciteit van de CPU overschrijden, wat de veiligste manier is om **OCR parallel** uit te voeren.

---

## Stap 4: Dien een OCR‑taak in voor elke afbeelding

Nu maken we van elk bestandspad een `Callable` die **OCR uitvoert**, de tekst herkent en het resultaat teruggeeft. Merk op dat we binnen de lambda een verse `OcrEngine` instantieren—dit voorkomt thread‑onveilige deling van engine‑status.

```java
List<Future<String>> ocrResults = new ArrayList<>();
for (String path : imagePaths) {
    ocrResults.add(executor.submit(() -> {
        OcrEngine engine = new OcrEngine();          // fresh engine per task
        engine.setImage(ImageStream.fromFile(path));
        engine.getLanguage().setEnglish(true);
        return engine.recognize() ? engine.getText()
                                   : "Failed: " + path;
    }));
}
```

* Elke `submit`‑aanroep geeft de lambda door aan de pool, die deze inplant op een vrije thread.  
* De `Future<String>`‑objecten laten ons later de herkende tekst ophalen, waarbij de volgorde behouden blijft indien nodig.

---

## Stap 5: Haal de herkende tekst op en toon deze

Zodra alle taken in de wachtrij staan, itereren we simpelweg over de `Future`‑lijst en roepen `get()` aan om te blokkeren tot elke OCR‑taak klaar is. Hier wordt de **convert image to text**‑stap zichtbaar: de aanroep `engine.getText()` levert de ruwe string op.

```java
for (Future<String> result : ocrResults) {
    System.out.println("OCR result:\n" + result.get());
}
```

Typische console‑output ziet er als volgt uit:

```
OCR result:
Hello world!
OCR result:
Invoice #12345
Date: 2026‑04‑30
...
```

Als een bestand faalt (bijvoorbeeld omdat het corrupt is), zie je een regel die begint met `Failed:` gevolgd door het pad—handig voor snelle debugging.

---

## Stap 6: Maak de Executor Service schoon

Vergeet nooit de pool af te sluiten; anders kan de JVM blijven hangen omdat hij denkt dat er nog werk is. Een nette shutdown laat lopende taken afmaken voordat het proces eindigt.

```java
executor.shutdown();
```

Je kunt ook `awaitTermination` aanroepen als je een timeout wilt afdwingen, maar voor de meeste command‑line utilities is een eenvoudige `shutdown()` voldoende.

---

## Volledig werkend voorbeeld

Hieronder staat het complete, kant‑klaar programma. Kopieer‑en‑plak het in een bestand met de naam `ParallelOcrTutorial.java`, pas de afbeeldingspaden aan, en compileer en voer uit met `javac` + `java` zoals je normaal zou doen.

```java
import com.aspose.ocr.*;
import java.util.*;
import java.util.concurrent.*;

public class ParallelOcrTutorial {
    public static void main(String[] args) throws Exception {
        // Step 2: Define the images to be processed
        List<String> imagePaths = Arrays.asList(
                "YOUR_DIRECTORY/image1.png",
                "YOUR_DIRECTORY/image2.jpg",
                "YOUR_DIRECTORY/image3.tif",
                "YOUR_DIRECTORY/image4.bmp"
        );

        // Step 3: Create a fixed‑size thread pool matching the CPU cores
        int coreCount = Runtime.getRuntime().availableProcessors();
        ExecutorService executor = Executors.newFixedThreadPool(coreCount);

        // Step 4: Submit an OCR task for each image
        List<Future<String>> ocrResults = new ArrayList<>();
        for (String path : imagePaths) {
            ocrResults.add(executor.submit(() -> {
                OcrEngine engine = new OcrEngine();          // fresh engine per task
                engine.setImage(ImageStream.fromFile(path));
                engine.getLanguage().setEnglish(true);
                return engine.recognize() ? engine.getText()
                                           : "Failed: " + path;
            }));
        }

        // Step 5: Retrieve and display the recognized text
        for (Future<String> result : ocrResults) {
            System.out.println("OCR result:\n" + result.get());
        }

        // Step 6: Clean up the executor service
        executor.shutdown();
    }
}
```

**Verwacht resultaat:** de tekstinhoud van elke afbeelding wordt naar de console geprint, in dezelfde volgorde als de `imagePaths`‑lijst. Als een afbeelding niet verwerkt kan worden, zie je een foutmelding in plaats van een lege regel.

---

## Veelgestelde vragen & randgevallen

### Wat als ik meer afbeeldingen heb dan threads?

De vaste threadpool zal de overtollige taken automatisch in de wachtrij plaatsen. Zodra een thread klaar is met zijn huidige OCR‑taak, pakt hij de volgende op. Dit queue‑gedrag is de essentie van **parallel OCR processing**—je krijgt maximale doorvoer zonder de CPU te overbelasten.

### Kan ik de taal wijzigen?

Zeker. Vervang `engine.getLanguage().setEnglish(true);` door de gewenste taalknop, bijvoorbeeld `setFrench(true)` of schakel meerdere talen in door verschillende setters aan te roepen vóór `recognize()`.

### Hoe ga ik om met zeer grote afbeeldingen?

Grote bestanden kunnen per thread veel geheugen verbruiken. Als je `OutOfMemoryError` ziet, overweeg dan de afbeelding te verkleinen voordat je deze aan de engine geeft, of vergroot de heap‑grootte met `-Xmx`. Een andere aanpak is om een **cached thread pool** te gebruiken (`

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}