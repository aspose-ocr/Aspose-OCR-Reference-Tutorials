---
category: general
date: 2026-02-17
description: Leer hoe je een vaste threadpool in Java gebruikt om tekst uit PNG‑afbeeldingen
  te extraheren met parallelle OCR‑verwerking en de executor‑service correct afsluit.
draft: false
keywords:
- fixed thread pool java
- extract text from png
- parallel ocr processing
- convert scanned pages text
- shut down executor service
language: nl
og_description: Ontdek hoe een vaste threadpool in Java tekst uit PNG-afbeeldingen
  parallel kan extraheren, gescande paginatekst kan converteren en de executor‑service
  veilig kan afsluiten.
og_title: Vaste thread pool Java – parallelle OCR voor PNG
tags:
- java
- ocr
- multithreading
- aspose
title: vaste threadpool java – parallel OCR voor PNG
url: /nl/java/advanced-ocr-techniques/fixed-thread-pool-java-parallel-ocr-for-png/
---

ens.

Now produce final output with all translations.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# fixed thread pool java – parallel OCR voor PNG

Heb je je ooit afgevraagd hoe je OCR op een reeks PNG‑bestanden kunt versnellen met een **fixed thread pool java**? In deze tutorial lopen we **extract text from PNG**‑afbeeldingen parallel door, **convert scanned pages text** om naar bewerkbare strings, en sluiten we veilig **shut down executor service** af zodra het werk klaar is.

Als je ooit naar een single‑threaded loop hebt gekeken die minutenlang duurt, ken je de frustratie van het wachten tot elke pagina klaar is voordat de volgende zelfs maar begint. Het goede nieuws? Met een paar regels Java en Aspose OCR kun je de kracht van al je CPU‑kernen benutten, die gescande pagina's omzetten in doorzoekbare tekst, en je applicatie responsief houden.  

Hieronder vind je een compleet, kant‑klaar voorbeeld, plus uitleg waarom elk onderdeel belangrijk is, veelvoorkomende valkuilen, en tips die je op elke OCR‑bibliotheek kunt toepassen.

---

## Wat je nodig hebt

- **Java 17** (of een recente JDK) – de code gebruikt spaarzaam de moderne `var`‑syntaxis, maar werkt ook op oudere versies.  
- **Aspose.OCR for Java**‑bibliotheek – je kunt deze ophalen van Maven Central of een proefversie downloaden van Aspose.  
- Een set **PNG**‑bestanden die je wilt verwerken – denk aan gescande bonnen, boekpagina's of screenshots.  
- Basiskennis van Java‑concurrency – niet vereist, maar wel handig.

Dat is alles. Geen externe services, geen Docker, alleen plain Java en een beetje multithreading‑magie.

## Stap 1: Voeg Aspose OCR‑dependency & licentie toe (optioneel)

Zorg er eerst voor dat de Aspose OCR‑JAR op je classpath staat. Als je Maven gebruikt, voeg dan toe:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version>
</dependency>
```

Als je geen licentie hebt, draait de bibliotheek in evaluatiemodus; de code werkt op dezelfde manier. Om een licentie te laden (aanbevolen voor productie), plaats `Aspose.OCR.lic` in je resources‑map en gebruik:

```java
// Load the Aspose OCR license (optional)
License license = new License();
license.setLicense("Aspose.OCR.lic");
```

> **Pro tip:** Houd het licentiebestand buiten versiebeheer om accidentele blootstelling te voorkomen.

## Stap 2: Maak een thread‑veilige `OcrEngine`‑instantie

De `OcrEngine` van Aspose OCR is thread‑safe zolang je dezelfde instantie hergebruikt over taken heen. Eén keer aanmaken bespaart geheugen en voorkomt de overhead van het opnieuw initialiseren van de engine voor elke afbeelding.

```java
// One shared OcrEngine for all threads
OcrEngine ocrEngine = new OcrEngine();
```

Waarom hergebruiken? Beschouw de engine als een zwaargewichtwerker die taalmodellen in het geheugen laadt. Een nieuwe engine per afbeelding starten zou zijn als het inhuren van een nieuwe specialist voor elke kleine taak – kostbaar en onnodig.

## Stap 3: Stel een Fixed Thread Pool Java in

Nu komt de ster van de show: een **fixed thread pool java**. We zullen deze dimensioneren op het aantal logische processoren zodat elke core werk krijgt zonder oversubscriberen.

```java
// Determine available processors and create a fixed pool
int threadCount = Runtime.getRuntime().availableProcessors();
ExecutorService threadPool = Executors.newFixedThreadPool(threadCount);
```

Het gebruik van een *fixed* pool (in plaats van een cached) geeft je voorspelbaar resource‑gebruik en voorkomt de gevreesde “out‑of‑memory”‑pieken wanneer er ineens honderden afbeeldingen binnenkomen.

## Stap 4: Lijst de PNG‑bestanden die je wilt verwerken (Extract Text from PNG)

Verzamel de paden naar de afbeeldingen die je wilt OCR‑en. In een echt project scan je misschien een map of lees je uit een database; hier coderen we een paar voorbeelden hard‑coded.

```java
List<String> imageFiles = Arrays.asList(
        "YOUR_DIRECTORY/page1.png",
        "YOUR_DIRECTORY/page2.png",
        "YOUR_DIRECTORY/page3.png"
);
```

> **Opmerking:** De bestandsextensie **png** is belangrijk omdat Aspose OCR het formaat automatisch detecteert, maar je kunt ook JPEG of TIFF gebruiken.

## Stap 5: Dien OCR‑taken in – Parallel OCR Processing

Elke afbeelding wordt een callable die de herkende tekst retourneert. Omdat de `OcrEngine` gedeeld wordt, hoeven we alleen het bestandspad aan de taak door te geven.

```java
List<Future<String>> ocrFutures = new ArrayList<>();

for (String imagePath : imageFiles) {
    ocrFutures.add(threadPool.submit(() -> {
        // Prepare input for this image
        OcrInput input = new OcrInput();
        input.add(imagePath);

        // Perform OCR using the shared engine
        OcrResult result = ocrEngine.recognize(input);

        // Return the plain text
        return result.getText();
    }));
}
```

Waarom het in een `Future` wikkelen? Het stelt ons in staat om alle taken meteen te starten, en later de resultaten te verzamelen in de volgorde waarin ze zijn ingediend – perfect om de paginavolgorde te behouden wanneer **convert scanned pages text** terug naar een document wordt omgezet.

## Stap 6: Haal resultaten op en toon (Convert Scanned Pages Text)

Nu wachten we tot elke `Future` klaar is en printen we de output. De `get()`‑aanroep blokkeert alleen tot de specifieke taak voltooid is, niet de hele pool.

```java
for (Future<String> future : ocrFutures) {
    System.out.println("----");
    System.out.println(future.get()); // prints OCR result for one PNG
}
```

Typische console‑output ziet er als volgt uit:

```
----
The quick brown fox jumps over the lazy dog.
----
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
----
Page 3 content goes here…
```

Als je de resultaten liever naar bestanden schrijft, vervang dan `System.out.println` door een `Files.writeString`‑aanroep.

## Stap 7: Sluit de Executor Service netjes af

Wanneer elke taak voltooid is, is het cruciaal om de **shut down executor service** uit te voeren; anders kan je JVM non‑daemon threads levend houden, waardoor een nette afsluiting wordt verhinderd.

```java
threadPool.shutdown();               // No new tasks accepted
if (!threadPool.awaitTermination(60, TimeUnit.SECONDS)) {
    threadPool.shutdownNow();        // Force shutdown after timeout
}
```

Het `awaitTermination`‑patroon geeft de pool de kans om lopend werk af te ronden voordat we dwingen te stoppen. Het negeren van deze stap is een veelvoorkomende bron van geheugenlekken in langdurige applicaties.

## Volledig werkend voorbeeld

Alles bij elkaar genomen, hier is het volledige programma dat je kunt copy‑pasten in `ParallelBatchDemo.java` en uitvoeren:

```java
import com.aspose.ocr.*;

import java.util.*;
import java.util.concurrent.*;

public class ParallelBatchDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load license (optional)
        License license = new License();
        license.setLicense("Aspose.OCR.lic");

        // 2️⃣ Shared, thread‑safe OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 3️⃣ Fixed thread pool java – one thread per core
        int threadCount = Runtime.getRuntime().availableProcessors();
        ExecutorService threadPool = Executors.newFixedThreadPool(threadCount);

        // 4️⃣ Files to process – extract text from png
        List<String> imageFiles = Arrays.asList(
                "YOUR_DIRECTORY/page1.png",
                "YOUR_DIRECTORY/page2.png",
                "YOUR_DIRECTORY/page3.png"
        );

        // 5️⃣ Submit tasks – parallel OCR processing
        List<Future<String>> ocrFutures = new ArrayList<>();
        for (String imagePath : imageFiles) {
            ocrFutures.add(threadPool.submit(() -> {
                OcrInput input = new OcrInput();
                input.add(imagePath);
                OcrResult result = ocrEngine.recognize(input);
                return result.getText();
            }));
        }

        // 6️⃣ Retrieve and print – convert scanned pages text
        for (Future<String> future : ocrFutures) {
            System.out.println("----");
            System.out.println(future.get());
        }

        // 7️⃣ Shut down executor service cleanly
        threadPool.shutdown();
        if (!threadPool.awaitTermination(60, TimeUnit.SECONDS)) {
            threadPool.shutdownNow();

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}