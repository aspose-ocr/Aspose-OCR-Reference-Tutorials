---
category: general
date: 2026-05-25
description: Extrahera text från en bild i Java med OCR. Lär dig hur du laddar en
  bild för OCR, känner igen text från ett foto och får text från OCR med ett enkelt
  kodexempel.
draft: false
keywords:
- extract text from image
- get text from ocr
- recognize text from photo
- java image to text
- load image for ocr
language: sv
og_description: Extrahera text från bild i Java med en steg‑för‑steg‑guide. Lär dig
  att ladda bild för OCR, känna igen text från foto och hämta text från OCR effektivt.
og_title: Extrahera text från bild i Java – Hämta text från OCR
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: Extract text from image in Java using OCR. Learn how to load image
    for OCR, recognize text from photo, and get text from OCR with a simple code example.
  headline: Extract Text from Image in Java – Get Text from OCR
  type: TechArticle
- description: Extract text from image in Java using OCR. Learn how to load image
    for OCR, recognize text from photo, and get text from OCR with a simple code example.
  name: Extract Text from Image in Java – Get Text from OCR
  steps:
  - name: '**Wrong language setting** – If you forget step 2, the engine defaults
      to English, turning Cyrillic characters into gibberish. Always double‑check
      the language code.'
    text: '**Wrong language setting** – If you forget step 2, the engine defaults
      to English, turning Cyrillic characters into gibberish. Always double‑check
      the language code.'
  - name: '**Image quality matters** – Low‑resolution or blurry photos will degrade
      accuracy. Pre‑process with contrast enhancement or binarization if needed.'
    text: '**Image quality matters** – Low‑resolution or blurry photos will degrade
      accuracy. Pre‑process with contrast enhancement or binarization if needed.'
  - name: '**File path quirks** – On Windows, backslashes need escaping (`C:\images\file.jpg`).
      Using `Path.of(...)` from `java.nio.file` sidesteps this.'
    text: '**File path quirks** – On Windows, backslashes need escaping (`C:\images\file.jpg`).
      Using `Path.of(...)` from `java.nio.file` sidesteps this.'
  - name: '**Memory leaks** – `OcrEngine` holds native resources. Call `ocrEngine.dispose()`
      when you’re done, especially in long‑running services.'
    text: '**Memory leaks** – `OcrEngine` holds native resources. Call `ocrEngine.dispose()`
      when you’re done, especially in long‑running services.'
  - name: '**Thread safety** – The engine isn’t thread‑safe out of the box. Create
      a separate instance per thread or synchronize access.'
    text: '**Thread safety** – The engine isn’t thread‑safe out of the box. Create
      a separate instance per thread or synchronize access.'
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: Extrahera text från bild i Java – Hämta text från OCR
url: /sv/java/ocr-basics/extract-text-from-image-in-java-get-text-from-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahera text från bild i Java – Hämta text från OCR

Har du någonsin behövt **extrahera text från bild** men varit osäker på vilket Java‑bibliotek du ska välja? Du är inte ensam. Oavsett om du digitaliserar kvitton, hämtar serienummer från produktfoton, eller bara leker med ett roligt sidoprojekt, är det en vanlig utmaning att omvandla en bild till redigerbar text.

I den här handledningen går vi igenom ett komplett, färdigt‑att‑köra‑exempel som visar dig hur du **laddar bild för OCR**, konfigurerar motorn och slutligen **läser av text från foto** så att du kan **hämta text från OCR** med bara några rader kod. Inga vaga referenser—allt du behöver finns här.

## Vad du kommer att lära dig

* Hur du sätter upp en lättviktig OCR‑motor i Java.  
* De exakta stegen för att **ladda bild för OCR** och hantera olika filsökvägar.  
* varför konfiguration av språket är viktigt när du vill **extrahera text från bild** som inte är engelska.  
* Hur du säkert skriver ut resultatet och vad du ska göra när motorn returnerar inget.  
* Ett antal pro‑tips för att undvika de vanligaste fallgroparna.

I slutet av den här guiden har du ett självständigt program som läser en JPEG (eller PNG) som innehåller ukrainska tecken och skriver ut den igenkända strängen till konsolen. Känn dig fri att byta språk eller bild—allt är modulärt.

![Diagram showing the flow of extracting text from image using Java OCR engine](/images/extract-text-from-image-java.png)

*Alt text: Flödesdiagram för processen att extrahera text från bild i Java.*

## Förutsättningar

* **Java Development Kit (JDK) 11+** – koden använder det moderna modulsystemet, men äldre versioner fungerar med mindre justeringar.  
* **Maven eller Gradle** – för att hämta OCR‑biblioteket (vi kommer att använda **Asprise OCR** som ett lättviktigt, gratis‑för‑utveckling‑alternativ).  
* En exempelbildfil (t.ex. `ukrainian_sign.jpg`) placerad någonstans där ditt program kan läsa den.  
* Grundläggande kunskap om Javas `main`‑metod och undantagshantering.

Om du har detta är du redo att köra. Annars, hämta JDK från Oracle eller AdoptOpenJDK och sätt upp ett enkelt Maven‑projekt—inget för komplicerat.

## Steg 1: Lägg till OCR‑beroendet

Först, tala om för ditt byggverktyg att hämta OCR‑motorn. För Maven, lägg in detta i `pom.xml`:

```xml
<dependency>
    <groupId>com.asprise.ocr</groupId>
    <artifactId>asprise-ocr</artifactId>
    <version>1.0.2</version>
</dependency>
```

Om du föredrar Gradle, är motsvarigheten:

```gradle
implementation 'com.asprise.ocr:asprise-ocr:1.0.2'
```

Dessa koordinater hämtar en kompakt JAR som inkluderar `OcrEngine`, `OcrLanguage` och hjälparklasserna vi kommer att använda. Inga extra inhemska binärer krävs för grundläggande latinska och kyrilliska skript.

## Steg 2: Skapa en Java‑klass för att **extrahera text från bild**

Nu ska vi skriva själva programmet. Spara följande som `ExtractTextDemo.java` i `src/main/java/com/example/ocr/`.

```java
package com.example.ocr;

import com.asprise.ocr.OcrEngine;
import com.asprise.ocr.OcrLanguage;

/**
 * Demonstrates how to extract text from image using Asprise OCR.
 * The example loads a JPEG, sets the language to Ukrainian,
 * runs recognition, and prints the result.
 */
public class ExtractTextDemo {

    public static void main(String[] args) {
        // ---- 1️⃣  Initialize the OCR engine ---------------------------------
        OcrEngine ocrEngine = new OcrEngine();

        // ---- 2️⃣  Configure the engine to recognize Ukrainian text -----------
        // This is crucial if your image contains non‑Latin characters.
        ocrEngine.getEngineOptions().setLanguage(OcrLanguage.UKRAINIAN);

        // ---- 3️⃣  Load the image that contains Ukrainian characters ----------
        // Replace the path with the location of your own picture.
        String imagePath = "YOUR_DIRECTORY/ukrainian_sign.jpg";
        try {
            ocrEngine.getImage().loadFromFile(imagePath);
        } catch (Exception e) {
            System.err.println("Failed to load image: " + e.getMessage());
            return;
        }

        // ---- 4️⃣  Perform OCR recognition and obtain the extracted text -------
        String recognizedText;
        try {
            recognizedText = ocrEngine.recognize().getText();
        } catch (Exception e) {
            System.err.println("Recognition error: " + e.getMessage());
            return;
        }

        // ---- 5️⃣  Output the recognized text to the console -------------------
        System.out.println("=== OCR Result ===");
        System.out.println(recognizedText);
    }
}
```

### Varför denna struktur fungerar

* **Separata numrerade block** gör flödet lätt att följa, särskilt när du letar efter var du **laddar bild för OCR** eller **läser av text från foto**.  
* `try/catch`‑blocket runt bildladdning och igenkänning säkerställer att programmet misslyckas på ett kontrollerat sätt—användbart när filsökvägen är fel eller OCR‑motorn inte hittar språkdata.  
* Att sätta språket tidigt (steg 2) förbättrar noggrannheten avsevärt för icke‑engelska skript. Om du senare behöver **java image to text** för andra språk, byt bara `OcrLanguage.UKRAINIAN` mot `OcrLanguage.ENGLISH`, `FRENCH` osv.

## Steg 3: Bygg och kör programmet

Från projektets rot, kör:

```bash
mvn clean compile exec:java -Dexec.mainClass="com.example.ocr.ExtractTextDemo"
```

Eller, om du använder Gradle:

```bash
./gradlew run --args="com.example.ocr.ExtractTextDemo"
```

Förutsatt att `ukrainian_sign.jpg` innehåller texten *«Ласкаво просимо»* (ukrainska för “Welcome”), bör du se något liknande:

```
=== OCR Result ===
Ласкаво просимо
```

Detta resultat bekräftar att du framgångsrikt **extraherar text från bild** och **hämtar text från OCR** i ett enda körning.

## Steg 4: Finjustera arbetsflödet – Från **Java Image to Text** i riktiga projekt

Medan demon är minimal, kräver verkliga applikationer ofta lite mer:

| Scenario | Vad som ska justeras | Orsak |
|----------|----------------------|-------|
| **Batch‑behandling** | Loopa över en `List<Path>` och lagra varje resultat i en databas. | Minskar manuellt arbete när du har hundratals foton. |
| **Olika bildformat** | Använd `ImageIO.read(new File(path))` för förbehandling, och skicka sedan `BufferedImage` till `ocrEngine.getImage().loadFromBufferedImage(bufImg)`. | Hantera PNG, BMP eller till och med PDF‑filer efter konvertering. |
| **Prestanda‑optimering** | Anropa `ocrEngine.getEngineOptions().setSpeed(OcrEngine.Speed.FAST)` om du accepterar något lägre noggrannhet. | Snabbar upp igenkänning på lågpresterande hårdvara. |
| **Efterbehandling** | Trimma blanksteg, ersätt vanliga OCR‑fel (`0` → `O`, `1` → `I`). | Förbättrar datakvaliteten i efterföljande steg. |

Dessa variationer behåller kärnidén—**läser av text från foto**—intakt samtidigt som de ger dig flexibilitet för produktionsarbetsbelastningar.

## Vanliga fallgropar & pro‑tips

1. **Fel språkinställning** – Om du glömmer steg 2, använder motorn engelska som standard, vilket gör att kyrilliska tecken blir nonsens. Kontrollera alltid språk‑koden.  
2. **Bildkvalitet spelar roll** – Lågreolution eller suddiga foton försämrar noggrannheten. Förbehandla med kontrastförbättring eller binarisering om det behövs.  
3. **Filsökvägs‑egenskaper** – På Windows måste bakstreck escapetas (`C:\\images\\file.jpg`). Att använda `Path.of(...)` från `java.nio.file` kringgår detta.  
4. **Minnesläckor** – `OcrEngine` håller inhemska resurser. Anropa `ocrEngine.dispose()` när du är klar, särskilt i långlivade tjänster.  
5. **Trådsäkerhet** – Motorn är inte trådsäker från början. Skapa en separat instans per tråd eller synkronisera åtkomsten.

## Fullt fungerande exempel (allt‑i‑ett)

Nedan är en enda fil du kan kopiera‑och‑klistra in i vilken IDE som helst. Den inkluderar anropet `dispose()` och en liten hjälpfunktion för att göra koden lite renare.

```java
package com.example.ocr;

import com.asprise.ocr.OcrEngine;
import com.asprise.ocr.OcrLanguage;
import java.nio.file.Path;

/**
 * Complete, runnable demo that extracts text from an image using Java OCR.
 */
public class FullDemo {

    public static void main(String[] args) {
        // Path to the image – change this to your own file.
        Path imgPath = Path.of("YOUR_DIRECTORY/ukrainian_sign.jpg");

        // Run the OCR workflow and capture the output.
        String result = extractTextFromImage(imgPath, OcrLanguage.UKRAINIAN);
        if (result != null) {
            System.out.println("=== OCR Result ===");
            System.out.println(result);
        }
    }

    /**
     * Core method that encapsulates the 5‑step OCR process.
     *
     * @param imagePath Path to the image file.
     * @param language  Desired OCR language.
     * @return Recognized text, or {@code null} if something went wrong.
     */
    private static String extractTextFromImage(Path imagePath, OcrLanguage language) {
        OcrEngine engine = new OcrEngine();
        try {
            // 1️⃣ Set language
            engine.getEngineOptions().setLanguage(language);

            // 2️⃣ Load image
            engine.getImage().loadFromFile(imagePath.toString());

            // 3️⃣ Recognize and return text
            return engine.recognize().getText();
        } catch (Exception e) {
            System.err.println("Error during OCR: " + e.getMessage());
            return null;
        } finally {
            // 4️⃣ Release native resources
            engine.dispose();
        }
    }
}
```

Att köra detta program ger samma konsolutdata som visades tidigare. Känn dig fri att ersätta `OcrLanguage.UKRAINIAN` med `OcrLanguage.ENGLISH` eller något annat stödjande språk för att se hur motorn anpassar sig.

## Slutsats

Vi har gått igenom allt du behöver för att **extrahera text från bild** med Java: från att lägga till OCR‑beroendet till **ladda bild för OCR**,

## Relaterade handledningar

- [igenkänna textbild med Aspose OCR – Full Java OCR‑handledning](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Hur man OCR‑läser bildtext med språk med Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Konvertera bild till text i Java med Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}