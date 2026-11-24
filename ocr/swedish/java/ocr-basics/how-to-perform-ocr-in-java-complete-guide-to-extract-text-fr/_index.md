---
category: general
date: 2026-06-06
description: hur man utför OCR i Java – snabbt extrahera text från bild, konvertera
  bild till text och läsa text från jpg med ett enkelt kodexempel.
draft: false
keywords:
- how to perform OCR
- ocr in java
- extract text from image
- convert image to text
- read text from jpg
language: sv
og_description: hur man utför OCR i Java – lär dig hur du extraherar text från bild,
  konverterar bild till text och läser text från jpg med ett färdigt exempel.
og_title: Hur man utför OCR i Java – Steg‑för‑steg‑guide
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: how to perform OCR in Java – quickly extract text from image, convert
    image to text, and read text from jpg using a simple code example.
  headline: How to Perform OCR in Java – Complete Guide to Extract Text from Images
  type: TechArticle
- description: how to perform OCR in Java – quickly extract text from image, convert
    image to text, and read text from jpg using a simple code example.
  name: How to Perform OCR in Java – Complete Guide to Extract Text from Images
  steps:
  - name: What You’ll Learn
    text: '- Install an OCR library (yes, **ocr in java** is easier than you think).
      - Create and configure an OCR engine instance. - Load a JPG (or any image) and
      set the language. - Process the image and **extract text from image** files.
      - Print the recognized string to the console.'
  - name: Expected Output
    text: 'If `input.jpg` contains the Mongolian phrase “Сайн байна уу?” the console
      will show:'
  - name: 'Pro Tip: Batch Processing'
    text: 'If you need to **extract text from image** files in bulk, wrap the core
      logic in a loop:'
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: Hur man utför OCR i Java – Komplett guide för att extrahera text från bilder
url: /sv/java/ocr-basics/how-to-perform-ocr-in-java-complete-guide-to-extract-text-fr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man utför OCR i Java – Komplett guide för att extrahera text från bilder

Har du någonsin undrat **how to perform OCR** på en bild du tog med din telefon? Du är inte ensam. Oavsett om du bygger en kvittoskanningsapp eller bara behöver dra ut text från en skannad PDF, **how to perform OCR** i Java är en färdighet som snabbt lönar sig. I den här handledningen går vi igenom ett praktiskt exempel som **extracts text from image**‑filer, **converts image to text**, och till och med visar hur du **read text from jpg** med bara några rader kod.

> *Pro tip:* Samma tillvägagångssätt fungerar för PNG, BMP eller vilket format OCR‑motorn stödjer—byt bara filnamnet.

## Hur man utför OCR i Java – Översikt

Optisk teckenigenkänning (OCR) är tekniken som omvandlar bilder av bokstäver till faktisk, sökbar text. I Java‑ekosystemet finns flera bibliotek—Tesseract, Asprise och kommersiella SDK‑er—alla med ett liknande arbetsflöde: ladda en bild, tala om för motorn vilket språk som förväntas, kör igenkänningen och hämta resultatet. Nedan använder vi en generisk `OcrEngine`‑klass för att hålla exemplet tydligt, men du kan ersätta den med vilken konkret implementation som helst som följer samma mönster.

### Vad du kommer att lära dig

- Installera ett OCR‑bibliotek (ja, **ocr in java** är enklare än du tror).
- Skapa och konfigurera en OCR‑motorninstans.
- Ladda en JPG (eller någon bild) och ange språket.
- Bearbeta bilden och **extract text from image**‑filer.
- Skriv ut den igenkända strängen till konsolen.

När du är klar har du ett fristående Java‑program som du kan släppa in i vilket projekt som helst och köra omedelbart.

![how to perform OCR example](ocr-example.png "how to perform OCR in Java illustration")

## Steg 1 – Installera och importera ett OCR‑bibliotek (ocr in java)

Innan du skriver en enda rad Java behöver du ett bibliotek som faktiskt utför det tunga arbetet. Om du använder Maven, lägg till ett beroende så här (byt ut `com.example.ocr` mot det faktiska grupp‑ID:t för ditt valda SDK):

```xml
<dependency>
    <groupId>com.example</groupId>
    <artifactId>ocr-sdk</artifactId>
    <version>1.4.2</version>
</dependency>
```

Om du föredrar Gradle:

```gradle
implementation 'com.example:ocr-sdk:1.4.2'
```

När JAR‑filen är på din classpath, importera de klasser du behöver:

```java
import com.example.ocr.OcrEngine;
import com.example.ocr.OcrInputImage;
import com.example.ocr.OcrResult;
```

> **Why this matters:** Att importera rätt klasser förhindrar “cannot find symbol”-fel och gör din IDE glad—inget är mer frustrerande än en saknad import när du försöker **convert image to text**.

## Steg 2 – Skapa OCR‑motorninstansen (how to perform OCR)

Nu när biblioteket är klart, starta motorn. Tänk på motorn som hjärnan som kommer att titta på pixlarna och gissa bokstäverna.

```java
// Step 2: Create an OCR engine instance
OcrEngine ocrEngine = new OcrEngine();
```

Att skapa motorn är vanligtvis billigt; de flesta SDK‑er allokerar interna buffertar efter behov, så du kan säkert återanvända samma instans för många bilder om du bearbetar en batch.

## Steg 3 – Ladda bilden och ange språket (extract text from image)

Nästa steg är att ge motorn något att läsa. Här laddar vi en JPEG från disk och talar om för OCR‑motorn att texten är på mongoliska (ISO 639‑2‑kod “mon”). Du kan ändra sökvägen eller språkkoden för att passa ditt användningsfall.

```java
// Step 3: Load the image you want to recognize
ocrEngine.setImage(new OcrInputImage("YOUR_DIRECTORY/input.jpg"));

// Step 3b: Specify the language (e.g., English = "eng", Mongolian = "mon")
ocrEngine.getSettings().setLanguage("mon");
```

> **Side note:** Om du inte anger ett språk, använder motorn engelska som standard, vilket kan kraftigt minska noggrannheten när texten faktiskt är kyrillisk eller i ett annat skriftsystem. Ange alltid rätt språk när du kan.

## Steg 4 – Bearbeta bilden och hämta resultatet (convert image to text)

Med bilden och språket på plats, be motorn göra sin magi. Anropet `process()` kör OCR‑algoritmen och returnerar ett `OcrResult`‑objekt som innehåller den igenkända strängen och förtroendesiffror.

```java
// Step 4: Process the image and obtain the recognition result
OcrResult ocrResult = ocrEngine.process();
```

Bakom kulisserna kan motorn utföra förbehandling—rättning av snedvridning, binarisering, brusreducering—så att du inte behöver skriva dessa steg själv. Det är därför de flesta moderna OCR‑bibliotek är ett nöje att använda för **convert image to text**‑uppgifter.

## Steg 5 – Skriv ut den extraherade texten (read text from jpg)

Till sist, hämta rentexten från resultatet och gör något användbart med den. För den här demonstrationen skriver vi helt enkelt ut den till konsolen, men du skulle kunna skriva den till en fil, mata in den i ett sökindex eller skicka den till en annan tjänst.

```java
// Step 5: Output the extracted text
System.out.println(ocrResult.getText());
```

Den raden i sig bevisar att du framgångsrikt har **read text from jpg** (eller något annat stödd format). Om utskriften ser förvrängd ut, dubbelkolla språkkoden och bildkvaliteten.

## Fullständigt fungerande exempel (Alla steg kombinerade)

Nedan är en komplett, färdig‑att‑köra Java‑klass som binder ihop alla delar. Kopiera den till en fil med namnet `OcrDemo.java`, justera bildsökvägen och språket, och kör sedan `javac OcrDemo.java && java OcrDemo`.

```java
import com.example.ocr.OcrEngine;
import com.example.ocr.OcrInputImage;
import com.example.ocr.OcrResult;

/**
 * Demonstrates how to perform OCR in Java using a generic OCR SDK.
 * This example loads a JPG, sets the language to Mongolian, and prints
 * the recognized text to the console.
 *
 * Replace the import package with the actual library you are using.
 */
public class OcrDemo {

    public static void main(String[] args) {
        // Validate command‑line arguments
        if (args.length < 2) {
            System.err.println("Usage: java OcrDemo <image-path> <language-code>");
            System.exit(1);
        }

        String imagePath = args[0];   // e.g., "input.jpg"
        String language = args[1];    // e.g., "mon" for Mongolian

        // Step 1: Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image
        ocrEngine.setImage(new OcrInputImage(imagePath));

        // Step 3: Set the language (ISO‑639‑2)
        ocrEngine.getSettings().setLanguage(language);

        // Step 4: Run the recognition
        OcrResult result = ocrEngine.process();

        // Step 5: Print the extracted text
        System.out.println("=== Recognized Text ===");
        System.out.println(result.getText());
    }
}
```

### Förväntad utskrift

Om `input.jpg` innehåller den mongoliska frasen “Сайн байна уу?” kommer konsolen att visa:

```
=== Recognized Text ===
Сайн байна уу?
```

Om bilden är suddig eller språkkoden är fel, kommer du att se förvrängda tecken eller en tom sträng—vanliga fallgropar som vi kommer att diskutera härnäst.

## Vanliga fallgropar och hur du åtgärdar dem

| Symptom | Trolig orsak | Åtgärd |
|---------|--------------|-----|
| Förvrängda kyrilliska tecken | Fel språkkod (standard är engelska) | Sätt `ocrEngine.getSettings().setLanguage("mon")` eller rätt kod. |
| Ingen utskrift alls | Fel bildsökväg eller filen kan inte läsas | Verifiera sökvägen, säkerställ att filen finns och att processen har läsrättigheter. |
| Låg noggrannhet (<70 %) | Bilden har låg kontrast eller är roterad | Förbehandla bilden: öka kontrast, räta upp, eller konvertera till gråskala innan du skickar den till motorn. |
| `OutOfMemoryError` på stora PDF‑filer | Laddar många högupplösta sidor samtidigt | Bearbeta sidor en i taget, eller skala ner bilder innan OCR. |

### Proffstips: Batch‑bearbetning

Om du behöver **extract text from image**‑filer i bulk, omslut kärnlogiken i en loop:

```java
for (File img : new File("batchFolder").listFiles()) {
    ocrEngine.setImage(new OcrInputImage(img.getAbsolutePath()));
    OcrResult r = ocrEngine.process();
    System.out.println(r.getText());
}
```

## Gå vidare – Vad du kan utforska härnäst?

- **Language Packs:** De flesta OCR‑SDK‑er låter dig ladda ner ytterligare språkdatafiler. Att lägga till ett nytt paket låter dig **convert image to text** för språk utöver engelska och mongoliska.
- **PDF OCR:** Kombinera den här koden med Apache PDFBox för att

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Extract Text Images – OCR Basics with Aspose.OCR for Java](/ocr/english/java/ocr-basics/)
- [Convert Image to Text in Java using Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}