---
category: general
date: 2026-07-05
description: Extrahera text från tiff med Aspose OCR Java i en parallell OCR‑bearbetningsmiljö.
  Detta koncisa Aspose OCR Java‑exempel visar hur man ökar prestandan med fler‑kärnig
  trådning.
draft: false
keywords:
- extract text from tiff
- aspose ocr java example
- parallel ocr processing
- java ocr multithreading
- tiff image recognition
language: sv
og_description: Extrahera text från tiff med Aspose OCR Java och parallell OCR‑behandling.
  Följ detta steg‑för‑steg Java‑exempel för att snabba upp flersidig bildigenkänning.
og_title: Extrahera text från TIFF med Aspose OCR Java – Guide
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Extract text from tiff using Aspose OCR Java in a parallel OCR processing
    setup. This concise Aspose OCR Java example shows how to boost performance with
    multi‑core threading.
  headline: Extract text from tiff using Aspose OCR Java – Guide
  type: TechArticle
tags:
- Java
- OCR
- Aspose
- TIFF
title: Extrahera text från TIFF med Aspose OCR Java – Guide
url: /sv/java/advanced-ocr-techniques/extract-text-from-tiff-using-aspose-ocr-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahera text från tiff med Aspose OCR Java – Guide

Har du någonsin behövt **extrahera text från tiff**‑filer men upptäckt att processen går i snigelfart? Du är inte ensam. När du kastar en flersidig TIFF på en enkeltrådad OCR‑motor kan väntetiden kännas oändlig – särskilt i ett batch‑bearbetningsscenario.

Det är så här: Aspose OCR för Java kan utnyttja varje logisk kärna på din maskin och förvandla den tröga enkeltrådade bearbetningen till en smidig, parallell OCR‑behandlingspipeline. I den här handledningen går vi igenom ett komplett **Aspose OCR Java‑exempel** som visar exakt hur du konfigurerar motorn, matar in en flersidig TIFF och **extraherar text från tiff**‑filer på en bråkdel av den ursprungliga tiden.

## Vad du får med dig

- En körbar Java‑klass som demonstrerar **parallell OCR‑behandling** med Aspose OCR.  
- Klara förklaringar till varför varje konfiguration är viktig, inte bara vad du ska skriva.  
- Tips för att hantera kantfall som varierande sidantal, stora bildfiler och minnesbegränsningar.  
- En solid grund för att anpassa koden till dina egna dokument‑automatiseringsprojekt.

> **Förutsättningar**  
> • Java 8 eller nyare installerat (koden kompileras även med JDK 11).  
> • Maven eller Gradle för att hämta Aspose OCR för Java‑biblioteket.  
> • En flersidig TIFF‑bild (du kan skapa en med valfri bildredigerare eller använda exempel‑`multi_page.tif` som följer med Aspose).  

Om du har dessa grunder på plats, låt oss dyka ner.

![Extract text from tiff using Aspose OCR Java – parallel processing diagram](image.png "Diagram illustrating how parallel OCR processing extracts text from tiff files")

## Steg 1: Ställ in ditt projekt – det snabbaste Aspose OCR Java‑exemplet

Innan vi kommer till kärnan i **parallell OCR‑behandling** behöver vi ett Java‑projekt som kan se Aspose OCR‑JAR‑filerna. Det enklaste sättet är att använda Maven:

```xml
<!-- pom.xml snippet -->
<dependencies>
    <dependency>
        <groupId>com.aspose</groupId>
        <artifactId>aspose-ocr</artifactId>
        <version>23.12</version> <!-- check for the latest version -->
    </dependency>
</dependencies>
```

Om du föredrar Gradle är motsvarigheten:

```groovy
implementation 'com.aspose:aspose-ocr:23.12'
```

> **Proffstips:** Att lägga till beroendet via Maven Central säkerställer att du alltid hämtar den senaste, säkerhetsuppdaterade bygget. Ingen anledning att ladda ner JAR‑filer manuellt.

När din byggfil är klar kör du `mvn clean compile` (eller `gradle build`) för att verifiera att Aspose‑klasserna finns på klassvägen. Om du inte får några fel är du redo att köra.

## Steg 2: Skapa OCR‑motorn och aktivera flerkärnsexekvering

Nu skriver vi Java‑klassen som faktiskt utför OCR. Nyckelraden som förvandlar en vanlig OCR‑motor till en **parallell OCR‑behandlingskraftverk** är `setThreadCount`. Detta talar om för Aspose OCR hur många logiska kärnor den får använda.

```java
package com.example.ocr;

import com.aspose.ocr.OcrEngine;
import com.aspose.ocr.RecognitionResult;

/**
 * ParallelOcrDemo – a concise Aspose OCR Java example that extracts text from tiff
 * images using multiple threads.
 */
public class ParallelOcrDemo {

    public static void main(String[] args) throws Exception {
        // Step 2.1: Instantiate the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2.2: Tell the engine to use 4 logical cores (adjust to your CPU)
        // This is the heart of parallel OCR processing.
        ocrEngine.setThreadCount(4);

        // Step 2.3: Point the engine at a multi‑page TIFF file.
        // Replace the path with the location of your own TIFF.
        String tiffPath = "YOUR_DIRECTORY/multi_page.tif";

        // Step 2.4: Run the recognition. The method returns a RecognitionResult
        // which holds the extracted text and additional metadata.
        RecognitionResult result = ocrEngine.recognizeImage(tiffPath);

        // Step 2.5: Output the extracted text – this is where we finally
        // extract text from tiff and show it on the console.
        System.out.println("=== Extracted Text Start ===");
        System.out.println(result.getText());
        System.out.println("=== Extracted Text End ===");
    }
}
```

### Varför `setThreadCount` är viktigt

Aspose OCR delar internt varje sida i en flersidig TIFF i separata uppgifter. Som standard körs den på en enda tråd, vilket betyder att varje sida väntar på att den föregående ska bli klar. Genom att sätta `threadCount` till antalet fysiska kärnor (eller lite mindre för att hålla UI‑responsen) låter du motorn bearbeta flera sidor samtidigt. I benchmark‑tester kan en 4‑kärnig maskin minska den totala bearbetningstiden med **upp till 70 %** jämfört med standardläget med en tråd.

> **Obs:** Om du sätter trådtalet högre än antalet tillgängliga kärnor kommer OS att börja tids‑slicinga, vilket faktiskt kan försämra prestandan. Håll dig till `Runtime.getRuntime().availableProcessors()` som en säker övre gräns.

## Steg 3: Hantera stora TIFF‑filer och minnesbegränsningar

När du **extraherar text från tiff**‑filer som innehåller dussintals högupplösta sidor kan minnesanvändningen skjuta i höjden. Aspose OCR erbjuder några reglage för att hålla saker och ting prydligt:

```java
// Optional: Reduce memory footprint by lowering image resolution before OCR
ocrEngine.getImagePreprocessingOptions().setResolution(150); // DPI

// Optional: Enable streaming mode for massive TIFFs (>500 MB)
ocrEngine.setEnableStreaming(true);
```

- **Minskning av upplösning** ger lite mindre noggrannhet men en stor minnesvinst. De flesta tryckta dokument är fortfarande läsbara vid 150 DPI.  
- **Strömningsläge** bearbetar sidor en i taget utan att ladda hela TIFF‑filen i RAM. Detta är avgörande för batch‑jobb på servernivå.

## Steg 4: Verifiera resultatet och felsök vanliga problem

Efter att du kört demon bör du se den extraherade texten omsluten av markörerna “=== Extracted Text Start ===”. Om utskriften ser tom eller förvrängd ut, överväg följande kontroller:

| Symptom | Trolig orsak | Snabb åtgärd |
|---------|--------------|--------------|
| Ingen text alls | Fel filväg eller TIFF‑komprimering som inte stöds | Verifiera `tiffPath` och säkerställ att TIFF‑filen inte använder en proprietär komprimering (t.ex. CCITT Group 4 är ok; JPEG‑2000 kan behöva extra codecs). |
| Saknade tecken (t.ex. accentuerade bokstäver) | OCR‑språk ej satt | Anropa `ocrEngine.setLanguage(OcrEngine.Language.English);` eller ladda ett anpassat språkpaket. |
| Out‑of‑memory‑fel | Mycket stor TIFF utan strömningsläge | Aktivera `setEnableStreaming(true)` och/eller sänk upplösningen. |
| Långsam prestanda trots `setThreadCount` | Hyper‑threading avstängd eller JVM‑begränsningar | Säkerställ att din JVM inte är begränsad av `-Xmx`‑flaggor; ge den tillräckligt med heap (t.ex. `-Xmx2g`). |

## Steg 5: Skala upp – bearbeta en mapp med TIFF‑filer parallellt

Demo‑exemplet med en enda fil är utmärkt för inlärning, men i produktion krävs ofta batch‑bearbetning. Nedan följer en lättviktig utökning som går igenom en katalog, startar en trådpool och kör OCR‑motorn på varje fil samtidigt. Detta visar **parallell OCR‑behandling** på applikationsnivå.



## Vad du bör lära dig härnäst

Följande handledningar täcker närliggande ämnen som bygger vidare på teknikerna i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i egna projekt.

- [Extract Text Images – OCR Basics with Aspose.OCR for Java](/ocr/english/java/ocr-basics/)
- [Extract Text from Image Java with Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [How to extract text from image from URL using Aspose.OCR for Java](/ocr/english/java/advanced-ocr-techniques/perform-ocr-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}