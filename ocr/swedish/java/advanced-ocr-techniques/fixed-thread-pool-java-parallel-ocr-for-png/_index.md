---
category: general
date: 2026-02-17
description: Lär dig hur du använder en fast trådpool i Java för att extrahera text
  från PNG‑bilder med parallell OCR‑behandling och korrekt stänga av executor‑tjänsten.
draft: false
keywords:
- fixed thread pool java
- extract text from png
- parallel ocr processing
- convert scanned pages text
- shut down executor service
language: sv
og_description: Upptäck hur en fast trådpool i Java kan extrahera text från PNG‑bilder
  parallellt, konvertera skannade sidors text och säkert stänga av executor‑tjänsten.
og_title: Fast trådpool java – parallell OCR för PNG
tags:
- java
- ocr
- multithreading
- aspose
title: fast trådpool java – parallell OCR för PNG
url: /sv/java/advanced-ocr-techniques/fixed-thread-pool-java-parallel-ocr-for-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# fast trådpool java – parallell OCR för PNG

Har du någonsin funderat på hur du kan snabba upp OCR på en massa PNG‑filer med en **fixed thread pool java**? I den här handledningen går vi igenom hur du **extraherar text från PNG**‑bilder parallellt, **konverterar skannade sidors text** till redigerbara strängar, och säkert **stänger av executor‑service** när arbetet är klart.

Om du någonsin har stirrat på en enkeltrådad loop som drar ut på minuter, känner du frustrationen av att vänta på att varje sida ska bli klar innan nästa ens startar. Den goda nyheten? Med några rader Java och Aspose OCR kan du utnyttja kraften i alla dina CPU‑kärnor, omvandla de skannade sidorna till sökbar text och hålla din applikation responsiv.  

Nedan hittar du ett komplett, färdigt exempel, plus förklaringar till varför varje del är viktig, vanliga fallgropar och tips du kan använda med vilket OCR‑bibliotek som helst.

---

## Vad du behöver

- **Java 17** (eller någon recent JDK) – koden använder den moderna `var`‑syntaxen sparsamt, men fungerar även på äldre versioner.  
- **Aspose.OCR for Java**‑biblioteket – du kan hämta det från Maven Central eller ladda ner en provversion från Aspose.  
- En uppsättning **PNG**‑filer du vill bearbeta – tänk skannade kvitton, boksidor eller skärmbilder.  
- Grundläggande kunskap om Java‑konkurrens – inte nödvändigt, men hjälpsamt.

Det är allt. Inga externa tjänster, ingen Docker, bara ren Java och lite multitrådad magi.

## Steg 1: Lägg till Aspose OCR‑beroende & licens (valfritt)

Först, se till att Aspose OCR‑JAR‑filen finns på din classpath. Om du använder Maven, lägg till:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version>
</dependency>
```

Om du inte har en licens körs biblioteket i utvärderingsläge; koden fungerar på samma sätt. För att ladda en licens (rekommenderas för produktion), placera `Aspose.OCR.lic` i din resources‑mapp och använd:

```java
// Load the Aspose OCR license (optional)
License license = new License();
license.setLicense("Aspose.OCR.lic");
```

> **Proffstips:** Håll licensfilen utanför versionskontrollen för att undvika oavsiktlig exponering.

## Steg 2: Skapa en trådsäker `OcrEngine`‑instans

Aspose OCR:s `OcrEngine` är trådsäker så länge du återanvänder samma instans över uppgifter. Att skapa den en gång sparar minne och undviker overheaden av att återinitialisera motorn för varje bild.

```java
// One shared OcrEngine for all threads
OcrEngine ocrEngine = new OcrEngine();
```

Varför återanvända? Tänk på motorn som en tung arbetskraft som laddar språkmodeller i minnet. Att starta en ny motor per bild skulle vara som att anställa en ny specialist för varje liten uppgift – kostsamt och onödigt.

## Steg 3: Ställ in en fast trådpool Java

Nu kommer stjärnan i showen: en **fixed thread pool java**. Vi dimensionerar den efter antalet logiska processorer så varje kärna får arbete utan att överbelasta.

```java
// Determine available processors and create a fixed pool
int threadCount = Runtime.getRuntime().availableProcessors();
ExecutorService threadPool = Executors.newFixedThreadPool(threadCount);
```

Att använda en *fast* pool (istället för en cachad) ger dig förutsägbar resursanvändning och förhindrar de fruktade “out‑of‑memory”‑spikar när hundratals bilder anländer på en gång.

## Steg 4: Lista PNG‑filerna du vill bearbeta (Extrahera text från PNG)

Samla sökvägarna till de bilder du vill OCR‑behandla. I ett riktigt projekt kan du skanna en katalog eller läsa från en databas; här hårdkodar vi några exempel.

```java
List<String> imageFiles = Arrays.asList(
        "YOUR_DIRECTORY/page1.png",
        "YOUR_DIRECTORY/page2.png",
        "YOUR_DIRECTORY/page3.png"
);
```

> **Obs:** Filändelsen **png** är viktig eftersom Aspose OCR automatiskt upptäcker formatet, men du kan även mata in JPEG eller TIFF.

## Steg 5: Skicka OCR‑uppgifter – parallell OCR‑bearbetning

Varje bild blir ett callable‑objekt som returnerar den igenkända texten. Eftersom `OcrEngine` delas behöver vi bara skicka filvägen till uppgiften.

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

Varför packa in det i en `Future`? Det låter oss avfyra alla jobb omedelbart, och sedan samla resultaten i den ordning de skickades – perfekt för att bevara sidordningen när **convert scanned pages text** återförs till ett dokument.

## Steg 6: Hämta resultat och visa (Konvertera skannade sidors text)

Nu väntar vi på att varje `Future` ska bli klar och skriver ut resultatet. `get()`‑anropet blockerar bara tills den specifika uppgiften är färdig, inte hela poolen.

```java
for (Future<String> future : ocrFutures) {
    System.out.println("----");
    System.out.println(future.get()); // prints OCR result for one PNG
}
```

Typisk konsolutmatning ser ut så här:

```
----
The quick brown fox jumps over the lazy dog.
----
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
----
Page 3 content goes here…
```

Om du föredrar att skriva resultaten till filer, ersätt `System.out.println` med ett `Files.writeString`‑anrop.

## Steg 7: Stäng av executor‑tjänsten på ett rent sätt

När alla uppgifter är klara är det avgörande att **shut down executor service**; annars kan din JVM hålla icke‑daemon‑trådar levande, vilket hindrar en smidig avslutning.

```java
threadPool.shutdown();               // No new tasks accepted
if (!threadPool.awaitTermination(60, TimeUnit.SECONDS)) {
    threadPool.shutdownNow();        // Force shutdown after timeout
}
```

`awaitTermination`‑mönstret ger poolen en chans att avsluta pågående arbete innan vi tvingar den. Att ignorera detta steg är en vanlig källa till minnesläckor i långlivade applikationer.

## Fullt fungerande exempel

Sätter vi ihop allt får du det kompletta programmet som du kan kopiera‑klistra in i `ParallelBatchDemo.java` och köra:

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