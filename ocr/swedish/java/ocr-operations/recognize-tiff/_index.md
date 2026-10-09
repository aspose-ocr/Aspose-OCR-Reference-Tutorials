---
date: 2026-05-19
description: Lär dig hur du extraherar text från tiff och konverterar den till sökbart
  innehåll med Aspose.OCR for Java. Denna steg-för-steg-handledning täcker installation,
  kod och bästa praxis.
keywords:
- extract text from tiff
- how to recognize tiff
- java ocr library
- convert tiff to searchable
- java ocr tutorial
linktitle: OCR-igenkänning av TIFF-bilder i Aspose.OCR for Java
schemas:
- author: Aspose
  dateModified: '2026-05-19'
  description: Learn how to extract text from tiff and convert it to searchable content
    using Aspose.OCR for Java. This step‑by‑step tutorial covers setup, code, and
    best practices.
  headline: How to extract text from tiff with Aspose.OCR for Java
  type: TechArticle
- description: Learn how to extract text from tiff and convert it to searchable content
    using Aspose.OCR for Java. This step‑by‑step tutorial covers setup, code, and
    best practices.
  name: How to extract text from tiff with Aspose.OCR for Java
  steps:
  - name: Set Up Your Project
    text: Create a new Java project (IDE or command line) and place the Aspose.OCR
      JAR on the classpath.
  - name: Define Your Document Directory and Image Path
    text: Set `dataDir` to the folder that contains your TIFF files, e.g., `String
      dataDir = "C:/Images/";`.
  - name: Create AsposeOCR Instance
    text: Instantiate `AsposeOCR ocr = new AsposeOCR();` to access OCR functions.
  - name: Set Recognition Options
    text: Create a `DocumentRecognitionSettings` object to specify language, mode,
      and output options.
  - name: Perform Text Recognition
    text: The method returns an `OcrResult` containing the extracted text and metadata.
  - name: Print Recognition Results
    text: Iterate over the `OcrResult` fields to display the recognized text.
  - name: Implement the `printResult` Method
    text: The `printResult` helper formats and outputs the OCR data to the console.
  type: HowTo
- questions:
  - answer: It means converting the visual characters inside a TIFF image into editable,
      searchable text using OCR.
    question: What does “extract text from tiff” mean?
  - answer: Aspose.OCR for Java, available from the official Aspose site.
    question: Which library should I use?
  - answer: Yes—use a free trial for evaluation, then purchase a commercial license
      for deployment.
    question: Is a license required for production?
  - answer: Absolutely; the `RecognizeTiff` method processes all pages automatically.
    question: Can I handle multi‑page TIFFs?
  - answer: Java 8 or later is fully supported.
    question: What Java version is supported?
  type: FAQPage
second_title: Aspose.OCR Java API
title: Hur man extraherar text från tiff med Aspose.OCR for Java
url: /sv/java/ocr-operations/recognize-tiff/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahera text från TIFF‑bilder med Aspose.OCR för Java

I den här omfattande guiden kommer du att lära dig **hur du extraherar text från tiff**‑filer med Aspose.OCR för Java. Oavsett om du behöver sökbara PDF‑filer för ett dokumenthanteringssystem eller vill indexera skannade kontrakt, så guidar den här tutorialen dig genom varje steg—från installation av biblioteket till utskrift av OCR‑resultaten—så att du kan börja bearbeta TIFF‑bilder på några minuter.

## Snabba svar
- **Vad betyder “extract text from tiff”?** Det betyder att konvertera de visuella tecknen i en TIFF‑bild till redigerbar, sökbar text med hjälp av OCR.  
- **Vilket bibliotek ska jag använda?** Aspose.OCR för Java, tillgängligt från den officiella Aspose‑webbplatsen.  
- **Krävs en licens för produktion?** Ja—använd en gratis provversion för utvärdering, köp sedan en kommersiell licens för distribution.  
- **Kan jag hantera flersidiga TIFF‑filer?** Absolut; metoden `RecognizeTiff` bearbetar alla sidor automatiskt.  
- **Vilken Java‑version stöds?** Java 8 eller senare stöds fullt ut.

## Vad är extract text from tiff?
*Extract text from tiff* är OCR‑operationen som läser pixeldata i en TIFF‑fil och returnerar de underliggande tecknen som Unicode‑text. Detta möjliggör fulltextsökning, indexering och efterföljande dataanalys. Genom att konvertera skannade bilder till maskinläsbara strängar kan du integrera innehållet i databaser, tillämpa naturlig språkbehandling eller skapa sökbara PDF‑filer för arkiveringsändamål.

## Varför använda Aspose.OCR för Java?
Aspose.OCR stöder **50+ in‑ och utdataformat** och kan bearbeta TIFF‑filer upp till **500 MB** utan att ladda hela dokumentet i minnet. API‑et är ren Java, har **inga externa beroenden**, och levererar **>95 % noggrannhet** på tryckt engelsk text direkt ur lådan.

## Förutsättningar
- Java Development Kit (JDK) 8 eller nyare installerat.  
- Aspose.OCR för Java‑biblioteket hämtat och lagt till i ditt projekt. Hämta det från den officiella nedladdningssidan **[här](https://releases.aspose.com/ocr/java/)**.  
- En TIFF‑bild som innehåller den text du vill extrahera.  
- (Valfritt) Grundläggande kunskap om **read tiff file java** med `java.io` om du föredrar manuell filhantering.

## Importera paket
`AsposeOCR`‑klassen och relaterade inställningar finns i `com.aspose.ocr`‑namnrymden. Importera dem högst upp i din källfil.

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.DetectAreasMode;
import com.aspose.ocr.DocumentRecognitionSettings;
import com.aspose.ocr.Language;
import com.aspose.ocr.RecognitionResult;
import com.aspose.ocr.RecognitionResult.LinesResult;
import com.aspose.ocr.pdf.AsposeOCRPdf;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.util.ArrayList;
```

## Hur extraherar man text från tiff med Aspose.OCR för Java?
Läs in TIFF‑filen med `new AsposeOCR()` och anropa `recognizeTiff()`—det enda anropet läser varje sida, tillämpar språk‑specifika modeller och returnerar ett strukturerat `OcrResult`‑objekt som innehåller ren text, stycken och förtroendescore. Metoden fungerar på under en sekund för vanliga 300 dpi‑skanningar.

### Steg 1: Ställ in ditt projekt
Skapa ett nytt Java‑projekt (IDE eller kommandorad) och placera Aspose.OCR‑JAR‑filen på klassvägen.

### Steg 2: Definiera din dokumentkatalog och bildsökväg
Sätt `dataDir` till mappen som innehåller dina TIFF‑filer, t.ex. `String dataDir = "C:/Images/";`.

```java
String dataDir = "Your Document Directory";
String file = dataDir + "multipage.tif";
```

### Steg 3: Skapa AsposeOCR‑instans
Instansiera `AsposeOCR ocr = new AsposeOCR();` för att få åtkomst till OCR‑funktionerna.

```java
AsposeOCR api = new AsposeOCR();
```

### Steg 4: Ställ in igenkänningsalternativ
Skapa ett `DocumentRecognitionSettings`‑objekt för att ange språk, läge och utdataalternativ.

```java
DocumentRecognitionSettings settings = new DocumentRecognitionSettings(2);
settings.setDetectAreasMode(DetectAreasMode.PHOTO);
```

### Steg 5: Utför textigenkänning
Metoden returnerar ett `OcrResult` som innehåller den extraherade texten och metadata.

```java
ArrayList<RecognitionResult> result = api.RecognizeTiff(file, settings);
```

### Steg 6: Skriv ut igenkänningsresultat
Iterera över `OcrResult`‑fälten för att visa den igenkända texten.

```java
for (RecognitionResult r : result) {
    printResult(r);
}
```

### Steg 7: Implementera `printResult`‑metoden
`printResult`‑hjälpfunktionen formaterar och skriver ut OCR‑data till konsolen.

```java
static void printResult(RecognitionResult result) {
    // Your implementation here
}
```

## Vanliga problem och lösningar

| Problem | Varför det händer | Hur man åtgärdar |
|---------|-------------------|------------------|
| **Ingen text returnerad** | Fel filväg eller TIFF‑komprimering som inte stöds. | Verifiera `dataDir`‑sökvägen, säkerställ att TIFF‑filen inte är korrupt, och använd okomprimerad TIFF när det är möjligt. |
| **Skräptecken** | Lågre lösning eller dålig kontrast. | Förbehandla bilden (öka DPI till 300+, öka kontrasten) innan du anropar `recognizeTiff`. |
| **Ej stödd språk** | Språk inte angivet i `DocumentRecognitionSettings`. | Lägg till `settings.setLanguage(Language.SPANISH);` (eller ditt mål‑språk) före igenkänning. |

## Vanliga frågor

**Q1: Är Aspose.OCR lämplig för att känna igen text på flera språk?**  
A: Ja, Aspose.OCR stöder över 60 språk, vilket låter dig ange önskat språk i `DocumentRecognitionSettings`.

**Q2: Kan jag integrera Aspose.OCR i en webbtjänst?**  
A: Absolut. Biblioteket körs på vilken Java‑kompatibel server som helst, och du kan exponera OCR‑funktionaliteten via REST‑slutpunkter.

**Q3: Vilka licensalternativ finns tillgängliga?**  
A: Du kan utforska licensalternativ och köpa en licens **[här](https://purchase.aspose.com/buy)**.

**Q4: Finns en gratis provversion?**  
A: Ja—ladda ner en provversion **[här](https://releases.aspose.com/)** för att utvärdera alla funktioner utan kostnad.

**Q5: Var kan jag få community‑support?**  
A: Gå med i diskussionen på **[Aspose.OCR‑forumet](https://forum.aspose.com/c/ocr/16)** för tips, kodexempel och felsökningshjälp.

**Senast uppdaterad:** 2026-05-19  
**Testat med:** Aspose.OCR för Java 24.11 (senaste vid skrivande)  
**Author:** Aspose

## Relaterade handledningar

- [Extrahera textbilder – OCR‑grunder med Aspose.OCR för Java](/ocr/java/ocr-basics/)
- [OCR‑igenkänning av PDF‑dokument i Aspose.OCR för Java](/ocr/java/ocr-operations/recognize-pdf/)
- [Extrahera text från bild Java med Aspose.OCR Detect Areas‑läge](/ocr/java/ocr-operations/perform-ocr-detect-areas-mode/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< blocks/products/products-backtop-button >}}
{{< /blocks/products/pf/main-wrap-class >}}