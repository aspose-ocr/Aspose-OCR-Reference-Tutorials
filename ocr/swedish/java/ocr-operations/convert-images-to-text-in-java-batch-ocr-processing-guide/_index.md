---
category: general
date: 2026-01-02
description: Konvertera bilder till text med Java med Aspose OCR. Bemästra batch‑OCR‑behandling,
  läs bilder från mapp och filtrera filer efter filändelse.
draft: false
keywords:
- convert images to text
- batch ocr processing
- read images from folder
- extract text from png
- filter files by extension
language: sv
og_description: Konvertera bilder till text snabbt med Java. Den här handledningen
  täcker batch‑OCR‑behandling, läsning av bilder från en mapp och filtrering av filer
  efter filändelse.
og_title: Konvertera bilder till text i Java – Komplett batch‑OCR‑guide
tags:
- OCR
- Java
- Aspose
title: Konvertera bilder till text i Java – Guide för batch‑OCR‑behandling
url: /sv/java/ocr-operations/convert-images-to-text-in-java-batch-ocr-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Konvertera bilder till text i Java – Batch OCR‑bearbetningsguide

Har du någonsin behövt **konvertera bilder till text** men varit osäker på hur du ska hantera dussintals filer samtidigt? Du är inte ensam—utvecklare kämpar ständigt med att extrahera data från PNG‑, JPG‑ och andra skannade filer. Den goda nyheten? Med Aspose OCR kan du på några minuter sätta upp en batch‑OCR‑bearbetningspipeline, läsa bilder från mappstrukturer och till och med filtrera filer efter filändelse så att du bara arbetar med det som är relevant.

I den här handledningen bygger vi ett självständigt Java‑program som går igenom en katalog, plockar ut varje `.png` eller `.jpg`, skickar varje bild till Aspose OCR asynkront och skriver ut den extraherade texten i ursprunglig ordning. I slutet har du ett återanvändbart kodsnutt som du kan klistra in i vilket projekt som helst som behöver **konvertera bilder till text** i stor skala.

---

![Exempel på konvertering av bilder till text](https://example.com/convert-images-to-text.png "Skärmbild av Java-konsolutdata som visar konverterad text från PNG-filer")

## Vad du kommer att bygga

- En enda `AsposeOCR`‑motor som delas mellan trådar (effektiv och trådsäker).  
- En `ParallelRecognizer` som kör OCR‑jobb parallellt, perfekt för **batch OCR‑bearbetning**.  
- Logik som **läser bilder från mapp** med `java.nio.file.Files`.  
- Enkla filter för att **extrahera text från PNG**‑filer samtidigt som JPG‑filer hanteras.  
- Ren nedstängning av den interna trådpoolen för att undvika resurssläpp.

### Förutsättningar

- Java 17 (eller någon annan recent LTS‑version).  
- Maven eller Gradle för att hämta Aspose OCR‑biblioteket.  
- En mapp full av PNG/JPG‑bilder som du vill bearbeta.  
- Grundläggande kunskap om Java‑streams—inget avancerat krävs.

> **Proffstips:** Om du ännu inte har någon licens erbjuder Aspose en gratis temporär nyckel som du kan använda för testning.

---

## Steg 1 – Ställ in projektet och lägg till Aspose OCR

Först, skapa ett nytt Maven‑projekt (eller Gradle, ditt val). Lägg till Aspose OCR‑beroendet i `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Check the latest version on Maven Central -->
</dependency>
```

> **Varför detta är viktigt:** Att deklarera beroendet i förväg säkerställer att kompilatorn kan hitta `AsposeOCR`, `ParallelRecognizer` och relaterade klasser. Det garanterar också att samma version används på alla maskiner, vilket är avgörande för reproducerbar **batch OCR‑bearbetning**.

När bygget är klart, uppdatera din IDE så att du ser Aspose‑paketen under `External Libraries`.

---

## Steg 2 – Konvertera bilder till text – Initiera OCR‑motorn

Vi behöver bara **en** OCR‑motorinstans för hela körningen. Att dela den mellan trådar sparar minne och ökar hastigheten eftersom motorn bara laddar språkpaket en gång.

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

> **Förklaring:** `ParallelRecognizer` omsluter motorn i en trådpool. När du skickar in många filer får varje fil sin egen arbetstråd, vilket möjliggör sann parallellism på fler‑kärniga CPU:er.

---

## Steg 3 – Läs bilder från mapp – Gå igenom katalogträdet

Nu måste vi **läsa bilder från mapp** och samla alla PNG‑ eller JPG‑filer. `Files.walk`‑API:t gör detta till en endasrad, men vi lägger till ett filter för att **extrahera text från PNG** endast när det behövs.

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

> **Varför vi filtrerar här:** Genom att använda `filter` kan vi **filtrera filer efter filändelse** tidigt, vilket minskar onödig I/O senare. Det gör också koden mer läsbar—inga komplicerade regex‑uttryck behövs.

---

## Steg 4 – Batch OCR‑bearbetning – Skicka jobb asynkront

Med listan av filer klar, pushar vi varje sökväg till `ParallelRecognizer`. Metoden `recognizeAsync` returnerar ett `Future<OcrResult>` som vi sparar för senare hämtning.

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

> **Vad som händer under huven:** Varje anrop köar ett uppdrag i recognizerns interna executor‑service. Uppdragen körs parallellt, så en mapp med 100 bilder kan bearbetas på en bråkdel av den tid som en enkeltrådad loop skulle ta.

---

## Steg 5 – Hämta resultat i ursprunglig ordning – Bevara filsekvensen

Eftersom vi sparade futures i samma ordning som `imagePaths`, kan vi helt enkelt iterera över listan och anropa `get()`. Anropet blockerar bara tills just den bilden är klar, vilket bevarar ordningen utan extra bokföring.

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

**Exempel på konsolutdata** (avkortad för korthet):

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

> **Hantering av kantfall:** Om en specifik bild kastar ett undantag (korrupt fil, format som inte stöds) fångar vi det och fortsätter med resten—en nödvändig vana för pålitliga **batch OCR‑bearbetnings‑pipelines**.

---

## Steg 6 – Rensa upp – Stäng av recognizern

Glöm aldrig att stänga av den interna trådpoolen; annars kan din JVM hänga kvar vid avslut.

```java
// Step 6: Shut down the recognizer to clean up its internal thread pool
parallelRecognizer.shutdown();
```

Det var allt! Programmet kommer nu att gå igenom vilken katalog som helst, filtrera PNG/JPG‑filer, köra OCR parallellt och skriva ut resultaten.

---

## Fullt fungerande exempel

Nedan är den kompletta, kopiera‑och‑klistra‑klara Java‑klassen. Byt ut `"YOUR_DIRECTORY"` mot sökvägen till din bildmapp och kör den från din IDE eller kommandorad.

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

Kör klassen, se hur konsolen fylls med extraherade strängar, och fira det faktum att du just **konverterade bilder till text** utan att skriva en enda loop som blockerar I/O.

---

## Vanliga frågor (FAQ)

**Q: Kan jag också bearbeta PDF‑ eller TIFF‑filer?**  
A: Absolut. Aspose OCR stödjer många format—lägg bara till de relevanta filändelserna i filtret i Steg 2.

**Q: Vad händer om jag behöver ett annat språk, till exempel spanska?**  
A: Ändra `RecognitionLanguage.ENGLISH` till `RecognitionLanguage.SPANISH`. Se till att språkpaketet är installerat (Aspose inkluderar de flesta stora språk som standard).

**Q: Min mapp innehåller undermappar—kommer de att skannas?**  
A: Ja. `Files.walk` traverserar hela trädet rekursivt, så varje inbäddad PNG/J

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}