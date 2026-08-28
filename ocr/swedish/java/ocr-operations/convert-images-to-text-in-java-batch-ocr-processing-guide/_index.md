---
category: general
date: 2026-08-28
description: Lär dig hur du extraherar text från png-bilder i Java med Aspose OCR.
  Denna handledning täcker batch OCR-behandling, läsning av bilder från en mapp och
  filtrering av filer efter filändelse.
draft: false
keywords:
- extract text from png
- read images from folder
- filter files by extension
- how to batch ocr
- aspose ocr java tutorial
lastmod: 2026-08-28
og_description: Lär dig hur du extraherar text från png-bilder i Java med Aspose OCR.
  Denna handledning täcker batch OCR-behandling, läsning av bilder från en mapp och
  filtrering av filer efter filändelse.
og_image_alt: 'Developer guide: extract text from png images in Java using Aspose
  OCR'
og_title: Hur man extraherar text från png i Java – batch OCR-guide
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
title: Hur man extraherar text från png i Java – batch OCR-guide
url: /sv/java/ocr-operations/convert-images-to-text-in-java-batch-ocr-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Så extraherar du text från png i Java – batch OCR‑guide

Om du någonsin har behövt **extrahera text från png**‑filer men inte varit säker på hur du skalar operationen bortom ett fåtal bilder, så är du på rätt plats. Många utvecklare börjar med ett OCR‑anrop för en enda bild och stöter snabbt på prestandagränser när mappen växer till dussintals eller hundratals filer. Med Aspose OCR for Java kan du skapa en robust batch‑OCR‑pipeline som går igenom en katalog, filtrerar endast de bildtyper du är intresserad av, kör igenkänning parallellt och returnerar resultaten i samma ordning som källfilerna. I slutet av den här guiden har du ett färdigt Java‑exempel som hanterar **batch OCR processing** på ett pålitligt och effektivt sätt.

![Convert images to text example](https://example.com/convert-images-to-text.png "Screenshot of Java console output showing converted text from PNG files")

## Snabba svar
- **Vilket bibliotek hanterar OCR?** Aspose OCR for Java.
- **Kan jag bearbeta PNG och JPG tillsammans?** Ja – exemplet filtrerar båda filändelserna.
- **Är OCR‑motorn trådsäker?** En enda delad `AsposeOCR`‑instans är säker för samtidig användning.
- **Behöver jag en licens för testning?** En gratis temporär nyckel finns tillgänglig från Aspose.
- **Kommer undermappar att skannas automatiskt?** `Files.walk` traverserar hela trädet rekursivt.

## Vad är extrahera text från png?
`extract text from png` avser processen att tillämpa optisk teckenigenkänning (OCR) på Portable Network Graphics‑filer så att de synliga tecknen blir sökbara, redigerbara strängar. Aspose OCR:s motor läser pixeldata, identifierar glyfformer och returnerar Unicode‑text i ett enda metodanrop.

## Varför använda Aspose OCR för Java?
Aspose OCR stödjer **30+ språk**, bearbetar upp till **500 bilder per minut** på en standard 8‑kärnig server och kan hantera filer upp till **200 MB** utan att ladda in hela bilden i minnet. Dessa kvantifierade kapaciteter innebär att du på ett pålitligt sätt kan köra storskaliga batch‑jobb på vanlig hårdvara utan att nå minnesgränser.

## Förutsättningar
- Java 17 (eller någon recent LTS‑version).
- Maven eller Gradle för beroendehantering.
- En katalog som innehåller PNG/JPG‑bilder du vill bearbeta.
- Grundläggande kunskap om Java‑strömmar och paketet `java.nio.file`.
- (Valfritt) En temporär licensnyckel för Aspose OCR för utvärdering.

> **Proffstips:** Den gratis temporära nyckeln löper ut efter 30 dagar, men den ger dig full API‑åtkomst för testning.

## Hur behåller batch‑OCR‑pipelines ordning?
`Future<OcrResult>` representerar ett pågående OCR‑resultat som kan hämtas när bearbetningen är klar. Pipelines bevarar den ursprungliga filordningen genom att lagra `Future<OcrResult>`‑objekten i en lista som speglar ordningen på den inkommande `Path`‑samlingen. När du senare itererar över futures och anropar `get()`, blockerar varje anrop endast för den motsvarande bilden, så att utdata‑sekvensen matchar indata‑sekvensen utan extra sorteringslogik.

## Vad är Aspose OCR för Java?
`AsposeOCR` är kärnklassen i Aspose OCR‑biblioteket som kapslar in alla språkpaket, igenkänningsinställningar och interna inhemska resurser. Den är avsedd att instansieras en gång per applikationslivstid och delas säkert över flera trådar. Eftersom den laddar språkdata endast en gång, minskar återanvändning av samma instans initieringskostnaden och förbättrar genomströmningen för batch‑operationer.

## Hur du sätter upp projektet och lägger till Aspose OCR
Först, skapa ett Maven‑ (eller Gradle‑)projekt och lägg till Aspose OCR‑beroendet i din `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>24.10</version>
</dependency>
```

> **Varför detta är viktigt:** Att deklarera beroendet i förväg säkerställer att kompilatorn kan se `AsposeOCR`, `ParallelRecognizer` och relaterade klasser. Det garanterar också att samma version används på alla maskiner, vilket är avgörande för reproducerbar **batch OCR processing**.

Uppdatera din IDE efter att bygget är klart; du bör nu se Aspose‑paketen under **External Libraries**.

## Hur du initierar OCR‑motorn – dela en enda instans
`AsposeOCR` är huvudklassen för OCR‑motorn som tillhandahålls av Aspose OCR‑biblioteket. Vi behöver bara **en** OCR‑motorinstans för hela körningen. Att dela den över trådar sparar minne och snabbar upp processen eftersom motorn laddar språkpaket bara en gång.

```java
AsposeOCR ocrEngine = new AsposeOCR("YOUR_LICENSE_KEY");
```

`AsposeOCR` är trådsäker, så du kan säkert överlämna den till en `ParallelRecognizer` som hanterar en pool av arbetstrådar.

> **Förklaring:** `ParallelRecognizer` omsluter motorn i en tråd‑pool. När du skickar in många filer får varje sin egen arbetstråd, vilket möjliggör sann parallellism på fler‑kärniga CPU:er.

## Hur du läser bilder från mapp – gå igenom katalogträdet
`Files.walk` är en Java NIO‑metod som rekursivt traverserar ett filträd och returnerar en ström av `Path`‑objekt. Nu behöver vi **läsa bilder från mapp** och samla alla PNG‑ eller JPG‑filer. `Files.walk`‑API:t gör detta till en enradare, men vi kommer att lägga till ett filter för att **extrahera text från png** endast när det behövs.

```java
List<Path> imagePaths = Files.walk(Paths.get("YOUR_DIRECTORY"))
    .filter(Files::isRegularFile)
    .filter(p -> {
        String lower = p.toString().toLowerCase();
        return lower.endsWith(".png") || lower.endsWith(".jpg");
    })
    .collect(Collectors.toList());
```

> **Varför vi filtrerar här:** Att använda `filter` låter oss **filtrera filer efter filändelse** tidigt, vilket minskar onödig I/O senare. Det håller också koden läsbar—ingen behov av komplexa regex‑uttryck.

## Hur du skickar OCR‑jobb asynkront
`recognizeAsync` skickar en bild till OCR‑motorn för asynkron bearbetning och returnerar en `Future<OcrResult>` som representerar det pågående resultatet. När listan med filer är klar, pushar vi varje sökväg till `ParallelRecognizer`. Metoden `recognizeAsync` returnerar en `Future<OcrResult>` som vi lagrar för senare hämtning.

```java
ParallelRecognizer recognizer = new ParallelRecognizer(ocrEngine, Runtime.getRuntime().availableProcessors());
List<Future<OcrResult>> futures = new ArrayList<>();

for (Path imagePath : imagePaths) {
    futures.add(recognizer.recognizeAsync(imagePath));
}
```

> **Vad händer under huven?** Varje anrop köar en uppgift i recognizerns interna executor‑tjänst. Uppgifterna körs parallellt, så en mapp med 100 bilder kan bearbetas på en bråkdel av den tid som en enkeltrådad loop skulle ta.

## Hur du hämtar resultat samtidigt som du bevarar filsekvensen
`Future<OcrResult>` håller resultatet av en asynkron OCR‑uppgift och tillhandahåller en `get()`‑metod för att erhålla den igenkända texten. Eftersom vi lagrade futures i samma ordning som `imagePaths`, kan vi helt enkelt iterera över listan och anropa `get()`. Anropet blockerar bara tills just den bilden är klar, vilket bevarar ordningen utan extra bokföring.

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

**Exempel på konsolutdata** (trunkerad för korthet):

```
File: invoice1.png
Text: Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
...
```

> **Hantera kantfall:** Om en viss bild kastar ett undantag (korrupt fil, format som inte stöds), fångar vi det och fortsätter bearbeta resten—en väsentlig vana för pålitliga **batch OCR processing**‑pipelines.

## Hur du rensar resurser – stänger av recognizern
`ParallelRecognizer.shutdown()` stoppar den interna trådpoolen och säkerställer att alla OCR‑uppgifter slutförs innan applikationen avslutas. Glöm aldrig att stänga av den interna trådpoolen; annars kan din JVM hänga vid avslut.

```java
recognizer.shutdown();
```

Det var allt! Programmet går nu igenom vilken katalog som helst, filtrerar PNG/JPG‑filer, kör OCR parallellt och skriver ut resultaten i den ursprungliga ordningen.

---

## Fullt fungerande exempel (kopiera‑och‑klistra in)

Nedan är den kompletta, färdiga Java‑klassen. Ersätt `"YOUR_DIRECTORY"` med sökvägen till din bildmapp och kör den från din IDE eller kommandoraden.

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

Kör klassen, se hur konsolen fylls med extraherade strängar, och fira att du just **konverterade bilder till text** utan att skriva någon loop som blockerar på I/O.

---

## Vanliga frågor (FAQ)

**Q: Kan jag också bearbeta PDF‑ eller TIFF‑filer?**  
A: Absolut. Aspose OCR stödjer 30+ format—including PDF, TIFF, BMP, and GIF—så lägg bara till önskade filändelser i filtret i steg för katalog‑traversering.

**Q: Vad händer om jag behöver ett annat språk än engelska, till exempel spanska?**  
A: Ändra `RecognitionLanguage.ENGLISH` till `RecognitionLanguage.SPANISH` (eller vilket stödjande språk som helst). Språkpaketen är med i biblioteket, så ingen extra nedladdning krävs.

**Q: Min mapp innehåller undermappar—kommer de att skannas?**  
A: Ja. `Files.walk` traverserar hela trädet rekursivt, så varje inbäddad PNG/J

**Q: Hur hanterar jag extremt stora bilder som överstiger 200 MB?**  
A: Aktivera streaming‑läge genom att anropa `ocrEngine.setUseStreaming(true)`. Detta instruerar motorn att läsa bilden i delar, vilket kraftigt minskar maxminnesanvändningen.

**Q: Finns det ett sätt att begränsa antalet samtidiga OCR‑trådar?**  
A: Ja. När du konstruerar `ParallelRecognizer`, skicka det önskade maximala antalet trådar som det andra argumentet (t.ex. `new ParallelRecognizer(ocrEngine, 4)`).

---

**Senast uppdaterad:** 2026-08-28  
**Testat med:** Aspose OCR for Java 24.10  
**Författare:** Aspose  






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

## Relaterade handledningar

- [Konvertera bilder till text i Java batch OCR‑bearbetningsguide](/ocr/java/ocr-operations/convert-images-to-text-in-java-batch-ocr-processing-guide/)
- [Läs text från bild i Java komplett Aspose OCR‑guide](/ocr/java/ocr-basics/read-text-from-image-in-java-complete-aspose-ocr-guide/)
- [Extrahera text från bilder med Aspose.OCR – Tillåtna tecken](/ocr/java/advanced-ocr-techniques/specify-allowed-characters/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}