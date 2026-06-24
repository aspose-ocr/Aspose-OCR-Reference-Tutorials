---
category: general
date: 2026-06-16
description: OCR‑rutavgränsningshandledning i Java visar hur man extraherar text från
  en bild, läser text från en bild och får OCR‑tillförlitlighetspoäng för JPG‑filer.
draft: false
keywords:
- ocr bounding box
- extract text from image
- ocr confidence score
- recognize text from jpg
- read text from image
language: sv
og_description: OCR-ram i Java låter dig känna igen text från JPG-filer, extrahera
  text från bild och visa OCR‑tillförlitlighetspoäng – allt i ett enkelt kodexempel.
og_title: OCR‑avgränsningsruta i Java – Extrahera text från bild
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: OCR bounding box tutorial in Java shows how to extract text from image,
    read text from image, and get OCR confidence score for JPG files.
  headline: OCR Bounding Box in Java – Extract Text from Image
  type: TechArticle
tags:
- OCR
- Java
- image-processing
- text-recognition
title: OCR‑avgränsningsruta i Java – Extrahera text från bild
url: /sv/java/advanced-ocr-techniques/ocr-bounding-box-in-java-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR‑ram i Java – Extrahera text från bild

Har du någonsin funderat på hur du får **ocr bounding box** för varje textstycke i en Java‑bild? I den här handledningen visar vi hur du **extraherar text från bild**‑filer, **läser text från bild**, och även ser **ocr confidence score** medan du **läser text från jpg**‑filer. Det korta svaret? Några rader kod med ett modernt OCR‑bibliotek, plus en kort förklaring till varför varje anrop är viktigt.

Nedan hittar du ett komplett, färdigt exempel, steg‑för‑steg‑genomgång och ett gäng praktiska tips som du kan kopiera rakt in i ditt eget projekt. I slutet kan du skriva ut något liknande:

```
Text: "Hello World"  Confidence: 0.97  Box: (x=12, y=45, width=210, height=30)
```

## Vad du behöver

- **Java 11** eller nyare (syntaxen nedan använder nyckelordet `var` för korthet, men du kan ta bort det för äldre JDK‑versioner).  
- Ett OCR‑bibliotek som erbjuder ett Java‑API – i den här guiden använder vi **[Tesseract4J](https://github.com/nguyenq/tess4j)**, ett tunt omslag runt det populära Tesseract‑motorn.  
- En JPEG‑bild (`.jpg`) som innehåller tydlig, tryckt text.  
- Din favoriteditor (IntelliJ IDEA, Eclipse, VS Code…) – vilken som helst fungerar.

Om du saknar biblioteket, lägg bara till detta Maven‑beroende:

```xml
<dependency>
    <groupId>net.sourceforge.tess4j</groupId>
    <artifactId>tess4j</artifactId>
    <version>5.4.0</version>
</dependency>
```

Nu kör vi igång.

![OCR‑ram exempel](ocr-bounding-box.png "OCR‑ram exempel")

## OCR‑ram: Konfigurera motorn

Det första du måste göra är att skapa en OCR‑motorsinstans. Tänk på det som att slå på skannern som senare ska läsa pixlarna.

```java
import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;

ITesseract ocrEngine = new Tesseract();          // Step 1 – create the OCR engine
ocrEngine.setDatapath("tessdata");               // point to the language data files
ocrEngine.setLanguage("eng");                    // we’ll work with English for now
```

**Varför detta är viktigt:**  
Utan att sätta `datapath` vet inte Tesseract var språkpaketen finns, och du får ett kryptiskt fel “Failed loading language”. Anropet `setLanguage` är valfritt om du bara behöver standard‑engelska paketet, men att vara explicit gör koden tydligare för framtida läsare.

## Ladda bilden du vill bearbeta

Nästa steg är att mata motorn med den JPEG du vill analysera. Biblioteket accepterar ett `File` eller `BufferedImage`; vi använder ett `File` för enkelhetens skull.

```java
import java.io.File;

File imageFile = new File("YOUR_DIRECTORY/text_page.jpg");   // Step 2 – load the image
```

**Proffstips:**  
Om din bild finns i resurser (t.ex. inuti en JAR), använd `getResourceAsStream` och slå in den med `ImageIO.read`. På så sätt fungerar handledningen både lokalt och i ett paketerat program.

## Utför OCR‑igenkänning

Nu ber vi faktiskt motorn att läsa bilden. Resultatet är en ren textsträng, men vi vill också ha **ocr confidence score** och **ocr bounding box** för varje rad.

```java
try {
    // Step 3 – run OCR and get a result object with layout data
    var result = ocrEngine.doOCR(imageFile, null);
    // The simple doOCR call returns only text; to get boxes we need the
    // getWords method with a specific page iterator level.
    var words = ocrEngine.getWords(imageFile, ITesseract.PageIteratorLevel.RIL_WORD);
    
    // Step 4 – iterate over each detected word
    for (var word : words) {
        System.out.printf(
            "Text: \"%s\"  Confidence: %.2f  Box: %s%n",
            word.getText(),
            word.getConfidence(),
            word.getBoundingBox().toString()
        );
    }
} catch (TesseractException e) {
    System.err.println("OCR failed: " + e.getMessage());
}
```

**Varför vi använder `getWords` istället för den enkla `doOCR`:**  
`doOCR` ger dig den råa strängen men kastar bort den rumsliga informationen. Genom att anropa `getWords` med `RIL_WORD` (eller `RIL_TEXTLINE` om du föredrar radrutor) får vi en lista med `Word`‑objekt som var och en innehåller text, confidence och omgivande rektangel. Det är kärnan i **ocr bounding box**‑funktionen.

## Förstå resultatet

Att köra kodsnutten ovan mot en ren JPEG ger en utskrift liknande:

```
Text: "Hello"  Confidence: 0.99  Box: java.awt.Rectangle[x=34,y=12,width=112,height=28]
Text: "World"  Confidence: 0.97  Box: java.awt.Rectangle[x=156,y=12,width=98,height=28]
```

- **Text** – de igenkända tecknen.  
- **Confidence** – ett flyttal mellan 0 och 1; högre betyder att motorn är säkrare.  
- **Box** – rektangeln som omger ordet i pixelkoordinater (x, y, bredd, höjd).  

Du kan nu **läsa text från bild** och dessutom exakt veta var varje snippet finns på duken – perfekt för markering, beskärning eller för att föra in i efterföljande NLP‑pipelines.

## Edge Cases & Common Pitfalls

| Situation | Vad du bör hålla utkik efter | Fix / Work‑around |
|-----------|------------------------------|-------------------|
| Bilden är suddig eller har låg kontrast | Confidence‑värdena sjunker dramatiskt (ofta under 0,6). | Förprocessa med OpenCV: öka kontrast, tillämpa tröskelvärde. |
| JPEG‑filen innehåller roterad text | Ramarna blir skeva eller saknas. | Använd `ocrEngine.setPageSegMode(ITesseract.PageSegMode.PSM_AUTO_OSD)` för att låta Tesseract automatiskt upptäcka orientering. |
| Stora bilder orsakar OutOfMemoryError | Java‑heapen fylls när stora bilder läses in. | Nedskala bilden innan OCR (`ImageIO.read` → `BufferedImage.getScaledInstance`). |
| Du behöver rad‑nivå‑ramar istället för ord‑nivå | `RIL_WORD` returnerar ramar per ord. | Byt till `ITesseract.PageIteratorLevel.RIL_TEXTLINE`. |
| Icke‑engelska tecken visas som � | Språkdatan är inte laddad. | Ladda ner rätt `.traineddata`‑fil och peka `setDatapath` på dess mapp. |

Att ta itu med dessa problem tidigt sparar dig timmar av felsökning senare.

## Fullt fungerande exempel (Alla steg i en fil)

Nedan är en fristående Java‑klass som du kan kopiera‑klistra in i en `src/main/java`‑mapp och köra med `mvn exec:java`. Den samlar allt vi har gått igenom.

```java
package com.example.ocrdemo;

import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.ITesseract.RenderedFormat;
import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;
import net.sourceforge.tess4j.Word;

import java.io.File;
import java.util.List;

public class OcrBoundingBoxDemo {

    public static void main(String[] args) {
        // ==== Step 1: Initialize the OCR engine ====
        ITesseract ocrEngine = new Tesseract();
        ocrEngine.setDatapath("tessdata"); // folder containing .traineddata files
        ocrEngine.setLanguage("eng");      // English language pack

        // Optional: improve accuracy for printed text
        ocrEngine.setPageSegMode(ITesseract.PageSegMode.PSM_AUTO);
        ocrEngine.setOcrEngineMode(ITesseract.OEM_TESSERACT_ONLY);

        // ==== Step 2: Load the JPEG you want to read ====
        File imageFile = new File("YOUR_DIRECTORY


## Vad bör du lära dig härnäst?

Följande handledningar täcker närliggande ämnen som bygger vidare på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Extrahera text från bild Java med Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Extrahera textbilder – OCR‑grunder med Aspose.OCR för Java](/ocr/english/java/ocr-basics/)
- [Hur man OCR‑läser bildtext med språk med Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}