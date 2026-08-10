---
category: general
date: 2026-03-26
description: Maak een doorzoekbare PDF met Aspose.OCR Java – leer een afbeelding te
  laden voor OCR, de primaire taal in te stellen, tekst uit de afbeelding te extraheren
  en de OCR‑PDF op te slaan.
draft: false
keywords:
- create searchable pdf
- set primary language
- extract text from image
- load image ocr
- save ocr pdf
language: nl
og_description: Maak een doorzoekbare pdf met Aspose.OCR Java. Stapsgewijze handleiding
  om afbeelding OCR te laden, de primaire taal in te stellen, tekst uit de afbeelding
  te extraheren en de OCR-pdf op te slaan.
og_title: Maak doorzoekbare PDF met Aspose.OCR – Java-gids
tags:
- Aspose.OCR
- Java
- PDF
- OCR
title: Maak doorzoekbare PDF met Aspose.OCR – Java-gids
url: /nl/java/ocr-operations/create-searchable-pdf-with-aspose-ocr-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Maak doorzoekbare PDF met Aspose.OCR – Java-gids

Heb je ooit een **doorzoekbare pdf** moeten maken van een gescand document, maar wist je niet waar je moest beginnen? Je bent niet de enige—veel ontwikkelaars lopen tegen die muur aan wanneer ze voor het eerst OCR in Java aanpakken. Het goede nieuws is dat Aspose.OCR de hele pijplijn—van het laden van een afbeelding tot het instellen van de primaire taal en uiteindelijk het opslaan van een OCR‑ingeschakelde PDF—vrij gemakkelijk maakt. In deze tutorial lopen we een volledig, uitvoerbaar voorbeeld door dat **tekst uit afbeelding extraheert**, je **primaire taal instelt**, en eindigt met een **OCR‑pdf opslaan** die je in elke lezer kunt openen.

We behandelen ook een paar praktische tips, zoals het inschakelen van GPU-versnelling voor snellere verwerking en het omgaan met documenten met meerdere talen (Tamil + Engels in ons geval). Aan het einde heb je een solide, productie‑klaar fragment dat je in je project kunt plaatsen.

## Wat je nodig hebt

- **Java 17** (of een recente JDK; Aspose.OCR ondersteunt Java 8+)
- **Aspose.OCR for Java** bibliotheek (download van de officiële site of toevoegen via Maven)
- Een **licentiebestand** (of de 30‑daagse proefversie)
- Een afbeeldingsbestand dat tekst bevat (de demo gebruikt `sample-mixed-tamil-eng.jpg`)

Geen extra frameworks, geen native afhankelijkheden—alleen plain Java en de Aspose.JARs.

---

## Stap 1: Doorzoekbare PDF maken – Het project opzetten

Voordat we in de code duiken, laten we ervoor zorgen dat het project klaar is om **doorzoekbare pdf**-bestanden te **maken**.

```bash
# Maven dependency (add to pom.xml)
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- check the latest version -->
</dependency>
```

> **Pro tip:** Houd het versienummer up‑to‑date; nieuwere releases bevatten vaak prestatieverbeteringen voor GPU‑gebruik.

Maak nu een eenvoudige Java‑klasse genaamd `RecentFeaturesDemo`. Deze klasse bevat alle logica die we nodig hebben om **image OCR te laden**, taalinstellingen te configureren, en uiteindelijk **OCR‑pdf op te slaan**.

---

## Stap 2: Image OCR laden en de engine initialiseren

De eerste echte stap in de pijplijn is om **image OCR te laden**. Dit vertelt Aspose.OCR welk bestand geanalyseerd moet worden.

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

> **Waarom dit belangrijk is:** Het inschakelen van GPU (`setUseGpu(true)`) kan de verwerkingstijd met tot 70 % verkorten op moderne hardware, terwijl parallel processing ervoor zorgt dat de CPU niet idle is wanneer de GPU bezig is.

---

## Stap 3: Primaire taal instellen (en een secundaire)

Als je deze stap overslaat, zal Aspose.OCR proberen de taal te raden, wat langzamer en minder nauwkeurig is. Hier lees je hoe je de **primaire taal** op Tamil instelt en Engels als fallback toevoegt.

```java
        // 3️⃣ Define languages – primary is Tamil, secondary is English
        ocrEngine.getLanguageSettings().setLanguage(Language.Tamil);
        ocrEngine.getLanguageSettings().setSecondaryLanguage(Language.English);
```

> **Uitleg:** De primaire taal beïnvloedt de tekenset en het woordenboek dat tijdens de herkenning wordt gebruikt. Het toevoegen van een secundaire taal is cruciaal voor documenten met gemengde scripts (denk aan een bon met zowel Tamil als Engelse tekst).  
> **Randgeval:** Als je document meer dan twee talen bevat, kun je `addAdditionalLanguage(...)` aanroepen voor elke extra taal.

---

## Stap 4: De afbeelding voorbewerken – Kantelen corrigeren & Ruis verwijderen

Gescannde afbeeldingen hebben vaak last van rotatie of achtergrondruis. Voorbewerking helpt de OCR‑engine **tekst uit afbeelding te extraheren** betrouwbaarder.

```java
        // 4️⃣ Pre‑processing options
        ocrEngine.getPreprocessingSettings()
                 .setDeskew(true)   // auto‑rotate tilted pages
                 .setDenoise(true); // suppress speckles and background patterns
```

> **Tip:** Als je weet dat de afbeelding al schoon is, kun je `setDenoise(true)` overslaan om een paar milliseconden te besparen.

---

## Stap 5: Het afbeeldingsbestand laden

Nu de engine klaar is, wijzen we deze naar het bestand dat we willen analyseren.

```java
        // 5️⃣ Load the image you want to recognize
        String imagePath = "YOUR_DIRECTORY/sample-mixed-tamil-eng.jpg";
        ocrEngine.setImage(ImageStream.fromFile(imagePath));
```

> **Wat als het pad onjuist is?** Aspose.OCR gooit een duidelijke `FileNotFoundException`. Plaats de oproep in een try‑catch als je een nette foutafhandeling nodig hebt.

---

## Stap 6: OCR uitvoeren en tekst uit afbeelding extraheren

Met alles geconfigureerd is het tijd om de herkenning daadwerkelijk uit te voeren. Deze stap **extraheert tekst uit afbeelding** en bereidt de gegevens voor die nodig zijn voor het maken van een PDF.

```java
        // 6️⃣ Perform recognition
        if (ocrEngine.recognize()) {
            String recognizedText = ocrEngine.getText();

            // Print the raw OCR output – handy for debugging
            System.out.println("Recognized text:");
            System.out.println(recognizedText);
```

Typische console‑output voor de demo‑afbeelding ziet er als volgt uit:

```
வணக்கம் World
This is a mixed language sample.
```

Je zult merken dat de Tamil‑regel correct wordt weergegeven, gevolgd door Engels. Dat is het resultaat van het correct **instellen van de primaire taal**.

---

## Stap 7: OCR‑PDF opslaan – Het laatste stuk

Het laatste stukje van de puzzel is om **OCR‑pdf op te slaan**. Aspose.OCR kan een onzichtbare tekstlaag bovenop de originele afbeelding embedden, waardoor de PDF doorzoekbaar wordt.

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

Open `searchable.pdf` in Adobe Reader, druk op **Ctrl + F**, en je kunt zowel Tamil‑ als Engelse woorden zoeken—precies wat een **doorzoekbare pdf maken** workflow belooft.

---

## Volledig werkend voorbeeld (Kopiëren‑Plakken)

Hieronder staat het volledige programma dat je kunt compileren en direct kunt uitvoeren. Vervang de placeholder‑paden door je eigen mappen.

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

Voer het uit met:

```bash
javac -cp "path/to/aspose-ocr.jar" RecentFeaturesDemo.java
java -cp ".:path/to/aspose-ocr.jar" RecentFeaturesDemo
```

Je zou de geëxtraheerde tekst in de console moeten zien, gevolgd door een bevestiging dat de **doorzoekbare pdf** naar schijf is geschreven.

---

## Veelgestelde vragen & randgevallen

### Wat als ik **image OCR moet laden** vanuit een byte‑array?

Je kunt `ImageStream.fromFile(imagePath)` vervangen door `ImageStream.fromBytes(byteArray)`. Dit is handig wanneer de afbeelding afkomstig is uit een database of een webservice.

### Hoe ga ik om met PDF’s die al afbeeldingen bevatten?

Aspose.OCR kan direct op PDF‑pagina’s werken: `ocrEngine.setDocument(PdfDocument.fromFile("input.pdf"))`. De engine rastert elke pagina intern voordat herkenning plaatsvindt.

### Mijn GPU wordt niet gedetecteerd—moet ik `setUseGpu(true)` behouden?

Als `setUseGpu(true)` faalt, valt Aspose.OCR automatisch terug op de CPU. Je kunt `ocrEngine.getEngineSettings().isGpuAvailable()` controleren voordat je het inschakelt.

### Kan ik **OCR‑pdf opslaan** met aangepaste metadata?

Ja. Na herkenning kun je `ocrEngine.getPdfSaveOptions().setTitle("My Document")` of `setAuthor("John Doe")` gebruiken voordat je `save` aanroept.

---

## Prestatie‑tips voor grote batches

- **Batchverwerking:** Hergebruik dezelfde `OcrEngine`‑instantie voor meerdere afbeeldingen. Roep alleen `ocrEngine.clear()` aan tussen runs.
- **Thread‑pool:** Plaats elke afbeeldingstaak in een `Callable` en dien deze in bij een `ExecutorService`. Omdat we parallel processing hebben ingeschakeld, profiteert elke thread van multi‑core gebruik.
- **Geheugenbeheer:** Voor gigapixel‑afbeeldingen, overweeg down‑sampling met `ocrEngine.getPreprocessingSettings().setResizeFactor(0.5)` om het RAM‑gebruik beheersbaar te houden.

---

## Conclusie

We hebben zojuist een volledige **doorzoekbare pdf maken** workflow doorlopen met Aspose.OCR voor Java. Beginnend met **image OCR laden**, hebben we 

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}