---
category: general
date: 2026-06-06
description: Extrahera text från skannad bild med Aspose OCR för Java. Lär dig hur
  du känner igen text från tiff‑filer med parallell bearbetning.
draft: false
keywords:
- extract text from scanned image
- recognize text from tiff
- Aspose OCR Java tutorial
- parallel OCR processing
- Java image recognition
language: sv
og_description: Extrahera text från skannad bild med Aspose OCR. Den här guiden visar
  hur du på ett effektivt sätt kan känna igen text från tiff‑filer med Java.
og_title: Extrahera text från skannad bild – Aspose OCR Java-handledning
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
title: Extrahera text från skannad bild i Java – Komplett Aspose OCR-guide
url: /sv/java/advanced-ocr-techniques/extract-text-from-scanned-image-in-java-complete-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahera text från skannad bild – Komplett Aspose OCR‑guide

Har du någonsin behövt **extrahera text från skannad bild** men känt dig fast vid “hur?”? Du är inte ensam. Oavsett om du digitaliserar gamla arkiv, hämtar data från fakturor eller bygger ett sökbart PDF‑bibliotek, kan det vara en smärta att få pålitlig text ur en TIFF‑skanning.  

God nyhet: med Aspose OCR för Java kan du **känna igen text från tiff**‑filer med bara några rader kod, och till och med öka hastigheten genom att begränsa motorn till ett fåtal CPU‑kärnor. I den här handledningen går vi igenom hela processen – från att installera biblioteket till att hantera resultatet – så att du kan kopiera‑klistra ett fungerande exempel direkt.

## Vad den här handledningen täcker

- Installera Aspose OCR för Java (Maven eller manuellt JAR)
- Ladda en stor skannad TIFF‑bild
- Konfigurera motorn för att använda upp till 4 trådar (parallell OCR)
- Köra OCR‑processen och skriva ut den extraherade texten
- Vanliga fallgropar (minne, fler‑sidiga TIFF‑filer) och hur du undviker dem
- Snabb prestandatips: när du ska justera `setMaxThreads`

När du är klar kommer du kunna **extrahera text från skannad bild**‑filer på ett pålitligt sätt, och du förstår varför justering av trådräkningen spelar roll när du *känner igen text från tiff* i en produktionspipeline.

---

![extrahera text från skannad bild exempel](example.png "Skärmbild som visar extraherad text från en skannad TIFF‑bild")

## Förutsättningar

Innan vi dyker ner, se till att du har:

1. **Java Development Kit (JDK) 8+** – någon recent version fungerar.
2. **Maven** (eller möjlighet att lägga till JAR‑filer manuellt) – vi använder Maven för enkelhetens skull.
3. En **Aspose OCR för Java**‑licens (den fria utvärderingen fungerar, men den lägger till ett vattenstämpel).  
4. En **stor TIFF‑skanning** (t.ex. `large_scan.tif`) som du vill bearbeta.

Om någon av dessa är okända, oroa dig inte – varje steg förklaras nedan.

## Steg 1: Lägg till Aspose OCR i ditt projekt

### Maven‑användare

Lägg till följande beroende i din `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- check the latest version on Maven Central -->
</dependency>
```

### Manuell JAR‑installation

Ladda ner den senaste `aspose-ocr-xx.jar` från Aspose‑webbplatsen och placera den på din classpath.  

> **Proffstips:** Håll JAR‑filen i en `libs/`‑mapp och referera den i ditt IDE:s projektinställningar. Detta undviker “class not found”-överraskningar senare.

## Steg 2: Skapa en enkel Java‑klass

Skapa en fil med namnet `ParallelOcrDemo.java` i din källkods‑mapp (`src/main/java`). Denna klass kommer att innehålla hela OCR‑arbetsflödet.

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

> **Varför vi begränsar trådar:** Som standard försöker Aspose OCR använda varje kärna, vilket kan kväva andra tjänster på en delad maskin. Att sätta `setMaxThreads(4)` talar om för motorn att köra upp till fyra parallella arbetare – tillräckligt för en märkbar hastighetsökning på de flesta moderna CPU‑er utan att monopoliserar resurserna.

## Steg 3: Kompilera och kör

Öppna en terminal i projektets rot och kör:

```bash
mvn clean compile exec:java -Dexec.mainClass="com.example.ocr.ParallelOcrDemo"
```

Om du inte använder Maven, kompilera med `javac` och kör:

```bash
javac -cp "libs/*" src/main/java/com/example/ocr/ParallelOcrDemo.java
java -cp "libs/*:src/main/java" com.example.ocr.ParallelOcrDemo
```

### Förväntad output

```
=== Extracted Text ===
Invoice Number: 12345
Date: 2024‑05‑01
Total: $1,250.00
...
```

Konsolen kommer att visa den rena textversionen av vad som än fanns på den skannade sidan. Om bilden innehåller flera sidor, konkatenerar Aspose OCR dem i ordning.

## Steg 4: Hantera fler‑sidiga TIFF‑filer (kantfall)

Ett vanligt scenario är en **fler‑sidig TIFF** – tänk en skannad bok. Som standard läser `OcrInputImage` bara den första ramen. För att bearbeta alla sidor, använd `OcrInputImage` med en `FileInputStream` och aktivera stöd för fler‑sidiga filer:

```java
import java.io.FileInputStream;
import com.aspose.ocr.*;

FileInputStream fis = new FileInputStream("YOUR_DIRECTORY/multi_page.tif");
ocrEngine.setImage(new OcrInputImage(fis, true)); // 'true' enables multi‑page
```

Nu kommer `ocrEngine.process()` att returnera ett enda `OcrResult` som innehåller den konkatenerade texten från varje sida.

## Steg 5: Finjustera igenkänningsnoggrannheten

Om du märker **förvrängda tecken** eller saknade ord, prova dessa justeringar:

| Inställning | Vad den gör | När du ska använda den |
|-------------|--------------|------------------------|
| `ocrEngine.getSettings().setLanguage(OcrLanguage.English)` | Tvingar engelskt språkmodell (snabbare, mer exakt för engelska skanningar) | Ditt dokument är enspråkigt engelska |
| `ocrEngine.getSettings().setResolution(300)` | Skalar upp lågupplösta bilder innan igenkänning | Skanningar under 200 DPI |
| `ocrEngine.getSettings().setNoiseRemoval(true)` | Försöker rensa bort prickar och artefakter | Skanningar med mycket brus |

Exempelkod:

```java
ocrEngine.getSettings().setLanguage(OcrLanguage.English);
ocrEngine.getSettings().setResolution(300);
ocrEngine.getSettings().setNoiseRemoval(true);
```

## Steg 6: Exportera resultat till en fil

Att skriva ut till konsolen är okej för demo, men produktionskod skriver vanligtvis utdata någonstans där den är användbar:

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

Nu har du en ren‑text‑fil som du kan mata in i ett sökindex, en databas eller en efterföljande analys‑pipeline.

---

## Vanliga frågor (FAQ)

**Q: Fungerar detta med PNG‑ eller JPEG‑filer?**  
A: Absolut. `OcrInputImage` accepterar alla format som Java’s ImageIO kan läsa. Byt bara filändelsen i sökvägen.

**Q: Min server har 8 kärnor – ska jag sätta `setMaxThreads(8)`?**  
A: Du kan, men kom ihåg att andra tjänster kan behöva CPU‑cykler. En bra tumregel är “totala kärnor – 1” för dedikerade OCR‑arbetare.

**Q: Vad händer om OCR‑resultatet är tomt?**  
A: Kontrollera att bilden inte är helt vit, att du har angett rätt språk, och att upplösningen är minst 200 DPI. Låga kvalitetsskanningar kräver ofta förbehandling (räta upp, öka kontrast) innan de matas till Aspose OCR.

---

## Sammanfattning

Vi har just **extraherat text från skannad bild**‑filer med Aspose OCR för Java, och du vet nu hur du **känner igen text från tiff** effektivt med parallell bearbetning. Den kompletta koden finns i kodsnuttarna ovan, och du kan kopiera‑klistra den direkt in i ditt eget projekt.

### Vad blir nästa steg?

- **Batch‑bearbetning**: Loop över en katalog med TIFF‑filer, spara varje resultat i en egen fil.  
- **Integrera med Elasticsearch**: Indexera den extraherade texten för snabb fulltextsökning.  
- **Lägg till språkdetection**: Använd `OcrLanguage.AutoDetect` för flerspråkiga dokument.  

Experimentera med dessa idéer, så förvandlar du snabbt en hög av skannade papper till sökbar, handlingsbar data.

Lycka till med kodandet, och lämna gärna en kommentar om du stöter på problem!

## Vad bör du lära dig härnäst?

De följande handledningarna täcker närbesläktade ämnen som bygger vidare på teknikerna i den här guiden. Varje resurs innehåller kompletta kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [How to recognize tiff with Aspose.OCR for Java](/ocr/english/java/ocr-operations/recognize-tiff/)
- [Extract Text Images – OCR Basics with Aspose.OCR for Java](/ocr/english/java/ocr-basics/)
- [Extract Text from Image Java with Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}