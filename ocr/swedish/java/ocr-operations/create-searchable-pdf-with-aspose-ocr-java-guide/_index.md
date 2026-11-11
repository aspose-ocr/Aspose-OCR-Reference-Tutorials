---
category: general
date: 2026-03-26
description: Skapa sökbar PDF med Aspose.OCR Java – lär dig att ladda bild‑OCR, ange
  primärt språk, extrahera text från bilden och spara OCR‑PDF.
draft: false
keywords:
- create searchable pdf
- set primary language
- extract text from image
- load image ocr
- save ocr pdf
language: sv
og_description: Skapa sökbar PDF med Aspose.OCR Java. Steg‑för‑steg‑guide för att
  ladda bild‑OCR, ange primärt språk, extrahera text från bilden och spara OCR‑PDF.
og_title: Skapa sökbar PDF med Aspose.OCR – Java‑guide
tags:
- Aspose.OCR
- Java
- PDF
- OCR
title: Skapa sökbar PDF med Aspose.OCR – Java‑guide
url: /sv/java/ocr-operations/create-searchable-pdf-with-aspose-ocr-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa sökbar PDF med Aspose.OCR – Java‑guide

Har du någonsin behövt **create searchable pdf** från ett skannat dokument men var osäker på var du ska börja? Du är inte ensam—många utvecklare stöter på den muren när de först tar sig an OCR i Java. Den goda nyheten är att Aspose.OCR gör hela pipeline—från att ladda en bild till att ställa in primära språket och slutligen spara en OCR‑aktiverad PDF—ganska smärtfri. I den här handledningen går vi igenom ett komplett, körbart exempel som **extracts text from image**, låter dig **set primary language**, och avslutas med en **save OCR pdf** som du kan öppna i vilken läsare som helst.

Vi kommer också att gå igenom några praktiska tips, som att aktivera GPU‑acceleration för snabbare bearbetning och hantera dokument med blandade språk (Tamil + English i vårt fall). I slutet har du ett robust, produktionsklart kodsnutt som du kan lägga in i ditt projekt.

## Vad du behöver

- **Java 17** (eller någon nyare JDK; Aspose.OCR stödjer Java 8+)
- **Aspose.OCR for Java**‑biblioteket (ladda ner från den officiella webbplatsen eller lägg till via Maven)
- En **license file** (eller 30‑dagars provversionen)
- En bildfil som innehåller text (demot använder `sample-mixed-tamil-eng.jpg`)

Inga extra ramverk, inga inhemska beroenden—bara ren Java och Aspose‑JAR‑filerna.

---

## Steg 1: Skapa sökbar PDF – Ställa in projektet

Innan vi dyker ner i koden, låt oss försäkra oss om att projektet är redo att **create searchable pdf**‑filer.

```bash
# Maven dependency (add to pom.xml)
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- check the latest version -->
</dependency>
```

> **Pro tip:** Håll versionsnumret uppdaterat; nyare versioner innehåller ofta prestandaförbättringar för GPU‑användning.

Skapa nu en enkel Java‑klass som heter `RecentFeaturesDemo`. Klassen kommer att innehålla all logik vi behöver för att **load image OCR**, konfigurera språkinställningar och slutligen **save OCR pdf**.

---

## Steg 2: Ladda bild‑OCR och initiera motorn

Det första verkliga steget i pipeline är att **load image OCR**. Detta talar om för Aspose.OCR vilken fil som ska analyseras.

```java
import com.aspose.ocr.*;

public class RecentFeaturesDemo {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Load your Aspose.OCR license (or use the 30‑day trial)
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.Java.lic");

        // 2️⃣ Create and configure the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Enable GPU acceleration – speeds up recognition dramatically
        ocrEngine.getEngineSettings().setUseGpu(true);
        // Use all available CPU cores for parallel processing
        ocrEngine.getEngineSettings().setUseParallelProcessing(true);
```

> **Why this matters:** Aktivering av GPU (`setUseGpu(true)`) kan minska bearbetningstiden med upp till 70 % på modern hårdvara, medan parallell bearbetning säkerställer att CPU:n inte är inaktiv när GPU:n är upptagen.

---

## Steg 3: Ställ in primärt språk (och ett sekundärt)

Om du hoppar över detta steg kommer Aspose.OCR att försöka gissa språket, vilket är långsammare och mindre exakt. Så här **set primary language** till Tamil och lägger till English som reserv.

```java
        // 3️⃣ Define languages – primary is Tamil, secondary is English
        ocrEngine.getLanguageSettings().setLanguage(Language.Tamil);
        ocrEngine.getLanguageSettings().setSecondaryLanguage(Language.English);
```

> **Explanation:** Det primära språket påverkar teckenuppsättningen och ordboken som används under igenkänning. Att lägga till ett sekundärt språk är avgörande för dokument med blandade skript (tänk på ett kvitto med både Tamil och English‑text).  
> **Edge case:** Om ditt dokument innehåller mer än två språk kan du anropa `addAdditionalLanguage(...)` för varje extra språk.

---

## Steg 4: Förbehandla bilden – Raka upp & Denoise

Skannade bilder lider ofta av rotation eller bakgrundsbrus. Förbehandling hjälper OCR‑motorn att **extract text from image** mer pålitligt.

```java
        // 4️⃣ Pre‑processing options
        ocrEngine.getPreprocessingSettings()
                 .setDeskew(true)   // auto‑rotate tilted pages
                 .setDenoise(true); // suppress speckles and background patterns
```

> **Tip:** Om du vet att bilden redan är ren kan du hoppa över `setDenoise(true)` för att spara några millisekunder.

---

## Steg 5: Ladda bildfilen

Nu när motorn är klar pekar vi den på filen vi vill analysera.

```java
        // 5️⃣ Load the image you want to recognize
        String imagePath = "YOUR_DIRECTORY/sample-mixed-tamil-eng.jpg";
        ocrEngine.setImage(ImageStream.fromFile(imagePath));
```

> **What if the path is wrong?** Aspose.OCR kastar ett tydligt `FileNotFoundException`. Omge anropet med en try‑catch om du behöver en smidig felhantering.

---

## Steg 6: Kör OCR och extrahera text från bild

Med allt konfigurerat är det dags att faktiskt köra igenkänningen. Detta steg både **extracts text from image** och förbereder data som behövs för PDF‑skapande.

```java
        // 6️⃣ Perform recognition
        if (ocrEngine.recognize()) {
            String recognizedText = ocrEngine.getText();

            // Print the raw OCR output – handy for debugging
            System.out.println("Recognized text:");
            System.out.println(recognizedText);
```

Typisk konsolutdata för demobilden ser ut så här:

```
வணக்கம் World
This is a mixed language sample.
```

Du kommer att märka att Tamil‑raden renderas korrekt, följt av English. Det är resultatet av att **set primary language** korrekt.

---

## Steg 7: Spara OCR‑PDF – Den sista biten

Den sista biten av pusslet är att **save OCR pdf**. Aspose.OCR kan bädda in ett osynligt textlager ovanpå originalbilden, vilket gör PDF‑filen sökbar.

```java
            // 7️⃣ (Optional) Save a searchable PDF with an OCR layer
            String pdfPath = "YOUR_DIRECTORY/searchable.pdf";
            ocrEngine.save(pdfPath, SaveFormat.PdfSearchable);

            System.out.println("\nSearchable PDF saved to: " + pdfPath);
        } else {
            System.err.println("Recognition failed: " + ocrEngine.getErrorMessage());
        }
    }
}
```

Öppna `searchable.pdf` i Adobe Reader, tryck **Ctrl + F**, och du kan söka efter både Tamil‑ och English‑ord—precis vad ett **create searchable pdf**‑arbetsflöde lovar.

---

## Fullt fungerande exempel (kopiera‑klistra in)

Nedan är det kompletta programmet som du kan kompilera och köra som det är. Ersätt platshållar‑sökvägarna med dina egna kataloger.

```java
import com.aspose.ocr.*;

public class RecentFeaturesDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Load your Aspose.OCR license (or use the 30‑day trial)
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.Java.lic");

        // Step 2: Create and configure the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getEngineSettings().setUseGpu(true);                     // enable CUDA GPU acceleration
        ocrEngine.getEngineSettings().setUseParallelProcessing(true);     // use multiple CPU cores
        ocrEngine.getLanguageSettings().setLanguage(Language.Tamil);      // primary language
        ocrEngine.getLanguageSettings().setSecondaryLanguage(Language.English); // secondary language
        ocrEngine.getPreprocessingSettings()
                 .setDeskew(true)   // correct image rotation
                 .setDenoise(true); // reduce background noise

        // Step 3: Load the image you want to recognize
        String imagePath = "YOUR_DIRECTORY/sample-mixed-tamil-eng.jpg";
        ocrEngine.setImage(ImageStream.fromFile(imagePath));

        // Step 4: Run OCR and obtain the plain‑text result
        if (ocrEngine.recognize()) {
            String recognizedText = ocrEngine.getText();

            // Step 5: (Optional) Save a searchable PDF with an OCR layer
            String pdfPath = "YOUR_DIRECTORY/searchable.pdf";
            ocrEngine.save(pdfPath, SaveFormat.PdfSearchable);

            System.out.println("Recognized text:");
            System.out.println(recognizedText);
            System.out.println("\nSearchable PDF saved to: " + pdfPath);
        } else {
            System.err.println("Recognition failed: " + ocrEngine.getErrorMessage());
        }
    }
}
```

Kör det med:

```bash
javac -cp "path/to/aspose-ocr.jar" RecentFeaturesDemo.java
java -cp ".:path/to/aspose-ocr.jar" RecentFeaturesDemo
```

Du bör se den extraherade texten skriven till konsolen, följt av en bekräftelse på att **searchable pdf** har skrivits till disk.

---

## Vanliga frågor & kantfall

### Vad om jag behöver **load image OCR** från en byte‑array?

Du kan ersätta `ImageStream.fromFile(imagePath)` med `ImageStream.fromBytes(byteArray)`. Detta är praktiskt när bilden kommer från en databas eller en webbtjänst.

### Hur hanterar jag PDF‑filer som redan innehåller bilder?

Aspose.OCR kan arbeta direkt på PDF‑sidor: `ocrEngine.setDocument(PdfDocument.fromFile("input.pdf"))`. Motorn rasteriserar varje sida internt innan igenkänning.

### Min GPU upptäcks inte—bör jag behålla `setUseGpu(true)`?

Om `setUseGpu(true)` misslyckas faller Aspose.OCR automatiskt tillbaka till CPU. Du kan kontrollera `ocrEngine.getEngineSettings().isGpuAvailable()` innan du aktiverar den.

### Kan jag **save OCR pdf** med anpassad metadata?

Ja. Efter igenkänning, använd `ocrEngine.getPdfSaveOptions().setTitle("My Document")` eller `setAuthor("John Doe")` innan du anropar `save`.

---

## Prestandatips för stora batcher

- **Batch processing:** Återanvänd samma `OcrEngine`‑instans för flera bilder. Anropa bara `ocrEngine.clear()` mellan körningar.
- **Thread pool:** Packa varje bilduppgift i en `Callable` och skicka till en `ExecutorService`. Eftersom vi aktiverade parallell bearbetning kommer varje tråd att dra nytta av fler‑kärnors användning.
- **Memory management:** För gigapixel‑bilder, överväg att nedskala med `ocrEngine.getPreprocessingSettings().setResizeFactor(0.5)` för att hålla RAM‑användningen rimlig.

---

## Slutsats

Vi har just gått igenom ett komplett **create searchable pdf**‑arbetsflöde med Aspose.OCR för Java. Med start från **load image OCR**, vi

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}