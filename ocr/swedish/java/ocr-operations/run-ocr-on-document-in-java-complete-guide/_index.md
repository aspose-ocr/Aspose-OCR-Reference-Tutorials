---
category: general
date: 2026-06-16
description: Kör OCR på dokument med Java på bara några steg. Lär dig hur du konfigurerar
  OCR, känner igen text från TIFF och extraherar text från flersidiga bilder.
draft: false
keywords:
- run OCR on document
- how to configure OCR
- recognize text from TIFF
- extract text from multi-page
language: sv
og_description: Kör OCR på dokument med Java. Den här guiden visar hur du konfigurerar
  OCR, känner igen text från TIFF‑filer och extraherar text från flersidiga bilder.
og_title: Kör OCR på dokument i Java – Steg‑för‑steg‑handledning
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Run OCR on document using Java in just a few steps. Learn how to configure
    OCR, recognize text from TIFF, and extract text from multi‑page images.
  headline: Run OCR on Document in Java – Complete Guide
  type: TechArticle
- description: Run OCR on document using Java in just a few steps. Learn how to configure
    OCR, recognize text from TIFF, and extract text from multi‑page images.
  name: Run OCR on Document in Java – Complete Guide
  steps:
  - name: '**Streamed processing** – Some OCR SDKs let you feed pages one‑by‑one instead
      of loading the entire TIFF into memory. Look for methods like `engine.setImageStream(...)`
      that accept an `InputStream`.'
    text: '**Streamed processing** – Some OCR SDKs let you feed pages one‑by‑one instead
      of loading the entire TIFF into memory. Look for methods like `engine.setImageStream(...)`
      that accept an `InputStream`.'
  - name: '**Memory limits** – If you hit `OutOfMemoryError`, lower the thread count
      or increase the JVM heap (`-Xmx2g`).'
    text: '**Memory limits** – If you hit `OutOfMemoryError`, lower the thread count
      or increase the JVM heap (`-Xmx2g`).'
  - name: '**Post‑processing** – Use regex or natural‑language libraries to clean
      up line breaks, remove headers/footers, or extract specific fields (e.g., invoice
      numbers).'
    text: '**Post‑processing** – Use regex or natural‑language libraries to clean
      up line breaks, remove headers/footers, or extract specific fields (e.g., invoice
      numbers).'
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: Kör OCR på dokument i Java – Komplett guide
url: /sv/java/ocr-operations/run-ocr-on-document-in-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kör OCR på dokument i Java – Komplett guide

Har du någonsin behövt **köra OCR på dokument**-filer men varit osäker på var du ska börja? Du är inte ensam. Oavsett om du digitaliserar gamla arkiv eller extraherar data från skannade formulär är det en vanlig smärta att få pålitlig text från bilder.

I den här handledningen går vi igenom ett praktiskt, end‑to‑end‑exempel som visar **hur man konfigurerar OCR**, **läser text från TIFF** och **extraherar text från flersidiga** dokument – allt med bara ett fåtal rader Java. Ingen onödig text, bara en fungerande lösning som du kan lägga in i ditt projekt idag.

## Vad du kommer att lära dig

- Sätt upp en OCR‑motorinstans i Java  
- Läs in en flersidig TIFF‑bild för bearbetning  
- Optimera motorn genom att konfigurera trådräkning (delen “hur man konfigurerar OCR”)  
- Utför igenkänning och skriv ut den extraherade texten  
- Hantera kantfall som stora filer och minnesgränser  

I slutet av den här guiden kommer du att kunna **köra OCR på dokument**‑bilder med självförtroende, och du kommer att ha en solid grund för att utöka lösningen till PDF‑filer, PNG‑filer eller till och med live‑kameraströmmar.

## Förutsättningar

- Java 17 eller nyare (koden använder `var`‑nyckelordet för korthet)  
- Ett OCR‑bibliotek som exponerar en `OcrEngine`‑klass (t.ex. *Aspose.OCR for Java* eller *Tesseract‑Java*‑wrapper).  
- En flersidig TIFF‑fil med namnet `multi_page.tif` placerad i en känd katalog.  

Om du saknar OCR‑biblioteket, lägg till det i din `pom.xml` (Maven) eller `build.gradle` (Gradle) – de exakta koordinaterna beror på leverantören, men de flesta tillhandahåller en enda JAR som du kan referera till.

---

## Steg 1: Initiera OCR‑motorn – Hur man kör OCR på dokument

Först och främst: du behöver ett motorobjekt som gör det tunga lyftet. Tänk på det som hjärnan bakom operationen.

```java
import com.example.ocr.OcrEngine;   // Replace with your actual package
import com.example.ocr.ImageStream;
import com.example.ocr.OcrResult;

public class OcrDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine instance
        OcrEngine engine = new OcrEngine();
```

> **Varför detta är viktigt:** `OcrEngine` kapslar in alla igenkänningsinställningar, språkpaket och hårdvaruanvändningsalternativ. Att skapa den en gång och återanvända den för flera bilder är mer effektivt än att instansiera den upprepade gånger.

---

## Steg 2: Läs in den flersidiga TIFF‑filen – Extrahera text från flersidiga bilder

Nu pekar vi motorn på filen vi vill bearbeta. TIFF är ett vanligt format för skannade dokument eftersom det kan lagra flera sidor i en enda fil.

```java
        // Step 2: Load the multi‑page image to be processed
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/multi_page.tif"));
```

> **Proffstips:** Om din TIFF ligger på en nätverksdelning, använd `ImageStream.fromUrl(...)` istället. Detta undviker att kopiera hela filen till minnet innan OCR påbörjas.

---

## Steg 3: Hur man konfigurerar OCR för maximal genomströmning

Färdiga OCR‑bibliotek kör ofta på en enda tråd, vilket kan bli en flaskhals på moderna fler‑kärniga maskiner. Här svarar vi på delen “**hur man konfigurerar OCR**” i pusslet.

```java
        // Step 3: Configure the engine to use all available CPU cores
        int availableCores = Runtime.getRuntime().availableProcessors();
        engine.getRecognitionSettings().setThreadCount(availableCores);
```

> **Varför detta fungerar:** Genom att matcha trådräkningen med antalet logiska processorer kan OCR‑motorn bearbeta olika sidor parallellt. På en 4‑kärnig laptop ser du ungefär en 3‑4× hastighetsökning när du hanterar flersidiga dokument.  
> **Kantfall:** Vissa miljöer (t.ex. Docker‑containrar med begränsade CPU‑kvoter) rapporterar fler kärnor än de får använda. I sådana fall bör du begränsa trådräkningen manuellt: `engine.getRecognitionSettings().setThreadCount(Math.min(availableCores, 2));`

---

## Steg 4: Läs av text från TIFF – Kärnan i OCR‑anropet

När allt är kopplat är det dags att faktiskt köra igenkänningen. Detta enkla anrop itererar över varje sida i TIFF‑filen, tillämpar språkmodellerna och returnerar ett sammansatt resultat.

```java
        // Step 4: Perform the OCR recognition
        OcrResult result = engine.recognize();
```

> **Vad händer under huven?** Motorn delar upp TIFF‑filen i enskilda rasterbilder, matar varje till OCR‑nätverket och sammanfogar den textuella utdata. Om du behöver sid‑specifik granularitet, ger `result.getPages()` dig en lista med `OcrPageResult`‑objekt.

---

## Steg 5: Skriv ut den igenkända texten – Verifiera extraktionen

Till sist skriver vi ut den extraherade texten till konsolen. I en verklig applikation skulle du sannolikt skriva den till en databas eller en JSON‑fil.

```java
        // Step 5: Output the recognized text
        System.out.println(result.getText());
    }
}
```

**Förväntad output (avkortad):**

```
Page 1:
Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00

Page 2:
Terms and Conditions...
```

Om du ser nonsens istället för rena tecken, dubbelkolla att rätt språkpaket är installerade och att bilden inte är för brusig. Förbehandlingssteg som räta upp eller binarisering kan avsevärt förbättra noggrannheten.

---

## Hantera stora flersidiga filer – Tips för extraktion

Även om vi redan har visat grundflödet kan verkliga dokument vara enorma. Här är några extra överväganden:

1. **Strömbaserad bearbetning** – Vissa OCR‑SDK:er låter dig mata in sidor en efter en istället för att ladda hela TIFF‑filen i minnet. Leta efter metoder som `engine.setImageStream(...)` som accepterar en `InputStream`.  
2. **Minnesgränser** – Om du får `OutOfMemoryError`, sänk trådräkningen eller öka JVM‑heapen (`-Xmx2g`).  
3. **Efterbehandling** – Använd regex eller naturliga språk‑bibliotek för att rensa bort radbrytningar, ta bort sidhuvuden/sidfötter, eller extrahera specifika fält (t.ex. fakturanummer).

---

## Fullt fungerande exempel (alla steg kombinerade)

Nedan är den kompletta, färdiga Java‑klassen. Klistra in den i din IDE, justera paketet/importerna och kör den.

```java
package com.example.ocrdemo;

import com.example.ocr.OcrEngine;
import com.example.ocr.ImageStream;
import com.example.ocr.OcrResult;

/**
 * Demonstrates how to run OCR on document images, configure the engine,
 * recognize text from TIFF files, and extract text from multi‑page documents.
 */
public class OcrDemo {
    public static void main(String[] args) throws Exception {
        // Create the OCR engine instance
        OcrEngine engine = new OcrEngine();

        // Load the multi‑page TIFF image
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/multi_page.tif"));

        // Configure the engine to use all CPU cores (how to configure OCR)
        int cores = Runtime.getRuntime().availableProcessors();
        engine.getRecognitionSettings().setThreadCount(cores);

        // Perform recognition (recognize text from TIFF)
        OcrResult result = engine.recognize();

        // Output the extracted text (extract text from multi‑page)
        System.out.println(result.getText());
    }
}
```

> **Proffstips:** Omge anropet `recognize()` med ett `try‑catch`‑block för att hantera `OcrException` på ett smidigt sätt, särskilt när du arbetar med korrupta bildfiler.

---

## Slutsats

Vi har just visat dig hur du **kör OCR på dokument**‑bilder med Java, och täckt allt från motorinitiering till extraktion av text från flersidiga dokument. Genom att förstå **hur man konfigurerar OCR** kan du pressa ut varje uns av prestanda från moderna CPU:er, medan stegen för **läsa av text från TIFF** och **extrahera text från flersidiga** filer ger dig en solid grund för alla dokument‑digitaliseringsprojekt.

Vad blir nästa steg? Prova att byta ut TIFF‑filen mot en PDF, experimentera med egna språkmodeller, eller skicka utdata till ett sökindex. Himlen är gränsen när du har den här grunden under bältet.

Om du stöter på problem – kanske OCR‑biblioteket du valt använder ett annat API – lämna en kommentar nedan. Lycka till med kodandet, och njut av att förvandla de skannade sidorna till sökbar text!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närliggande ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Extrahera text från bilder – OCR‑grunder med Aspose.OCR för Java](/ocr/english/java/ocr-basics/)
- [Hur man känner igen tiff med Aspose.OCR för Java](/ocr/english/java/ocr-operations/recognize-tiff/)
- [Hur man OCR‑avläser bildtext med språk med Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}