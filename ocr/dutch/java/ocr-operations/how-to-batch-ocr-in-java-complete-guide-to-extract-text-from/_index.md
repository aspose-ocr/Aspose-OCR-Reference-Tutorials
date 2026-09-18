---
category: general
date: 2026-09-18
description: Leer hoe je tekst uit afbeeldingen in Java kunt extraheren met Aspose
  OCR. Batch verwerk PNG-, JPG- en TIFF-bestanden efficiënt in één oproep.
keywords:
- extract text from images
- convert images to text
- how to batch ocr
- extract text from png
- extract text from jpg
- extract text from tiff
lastmod: 2026-09-18
og_description: Beheers hoe je tekst uit afbeeldingen in Java kunt extraheren met
  batch OCR. Gebruik Aspose OCR om PNG-, JPG- en TIFF-bestanden in één oproep te converteren.
og_image_alt: Diagram showing multiple image files processed together for batch OCR
og_title: Tekst extraheren uit afbeeldingen in Java – batch OCR-gids
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: Learn how to extract text from images in Java using Aspose OCR. Batch
    process PNG, JPG, and TIFF files efficiently in a single call.
  headline: How to extract text from images in Java by batch OCR
  type: TechArticle
- questions:
  - answer: Yes, Aspose OCR is pure Java and requires no UI components, so it works
      perfectly on headless environments.
    question: Can I run this on a headless server?
  - answer: A commercial license is needed for production deployments; a free trial
      is available for evaluation.
    question: Is a license required for production use?
  - answer: Any OS that can run Java 17+, including Windows, Linux, and macOS.
    question: Which operating systems are supported?
  - answer: Over 60 languages are supported out of the box, ranging from English and
      Spanish to Arabic and Chinese.
    question: How many languages can Aspose OCR recognise?
  - answer: Individual image files up to 200 MB are supported; larger files should
      be split before processing.
    question: What is the maximum file size Aspose OCR can handle?
  type: FAQPage
tags:
- OCR
- Java
- Aspose
title: Hoe tekst uit afbeeldingen te extraheren in Java met batch OCR
url: /nl/java/ocr-operations/how-to-batch-ocr-in-java-complete-guide-to-extract-text-from/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe tekst uit afbeeldingen te extraheren in Java met batch-OCR

Als je snel **tekst uit afbeeldingen** wilt **extraheren** zonder voor elk bestand een lus te schrijven, is batch OCR de oplossing. In veel real‑world projecten ontvang je een map vol scans—PNG‑bonnen, JPG‑screenshots of multi‑page TIFF‑bestanden—en moet je ze omzetten naar doorzoekbare tekst. Aspose OCR laat je dat precies doen met één methode‑aanroep die PNG, JPG en TIFF‑bestanden samen verwerkt, waardoor zowel ontwikkelingstijd als CPU‑cycli worden bespaard.

## Snelle antwoorden
- **Wat doet batch OCR?** Het verwerkt meerdere afbeeldingsbestanden in één verzoek en retourneert tekst voor elk bestand.
- **Welke formaten worden ondersteund?** PNG, JPG/JPEG en multi‑page TIFF worden direct ondersteund.
- **Heb ik een aparte native bibliotheek nodig?** Nee, de Aspose OCR JAR bevat alles wat je nodig hebt.
- **Kan ik het aantal threads dat draait controleren?** Ja, gebruik `setMaxParallelism` op de batchprocessor.
- **Welke Java‑versie is vereist?** Java 17 of nieuwer.

## Wat is Aspose OCR?
Aspose OCR is een Java‑bibliotheek die gedrukt en handgeschreven tekst in afbeeldingsbestanden herkent zonder externe afhankelijkheden. Het ondersteunt meer dan 60 talen en kan tot 100 afbeeldingen per batch verwerken, waardoor het ideaal is voor grootschalige documentdigitalisatie.

## Wat deze tutorial behandelt
Laad een lijst met afbeeldingspaden, maak een `OcrBatchProcessor` aan, stel parallelisme af, voer een enkele `recognize`‑aanroep uit en print de geëxtraheerde strings. Aan het einde heb je een kant‑klaar Java‑programma dat tekst uit PNG, JPG en TIFF‑bestanden in bulk **extrahert**.

- **Hoe batch‑OCR** te gebruiken met Aspose’s `OcrBatchProcessor`.
- Manieren om **tekst uit afbeeldingen** van verschillende formaten (PNG, JPG, TIFF) te **extraheren**.
- Tips voor het beheersen van parallelisme om je app responsief te houden.
- Een complete, uitvoerbare Java‑programma dat je direct kunt kopiëren‑plakken en uitvoeren.

Geen voorafgaande ervaring met Aspose vereist—alleen een basis‑Java‑installatie en een IDE naar keuze. Aan het einde heb je een solide basis om tekst uit PNG, JPG en TIFF‑bestanden in bulk te herkennen.

---

![Diagram die laat zien hoe meerdere afbeeldingsbestanden batch-OCR worden verwerkt](/images/batch-ocr-diagram.png "hoe batch ocr")

*Afbeeldingsalt‑tekst: diagram hoe batch ocr die meerdere afbeeldingsbestanden samen verwerkt.*

## Vereisten

| Vereiste | Waarom het belangrijk is |
|----------|--------------------------|
| Java 17 of nieuwer | Aspose OCR richt zich op moderne JVM's. |
| Maven of Gradle | Vereenvoudigt het toevoegen van de Aspose OCR‑bibliotheek. |
| Basis Java‑kennis | Nodig om de code‑stroom te begrijpen. |
| Een set voorbeeldafbeeldingen (`.png`, `.jpg`, `.tif`) | Om de extractie in actie te zien. |

Als je deze al hebt, geweldig—laten we beginnen.

## Stap 1: voeg Aspose OCR toe aan je project

Het eerste wat je nodig hebt is de Aspose OCR JAR. Met Maven plaats je dit in je `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- use the latest stable version -->
</dependency>
```

Als je Gradle verkiest, is het equivalent:

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

Het toevoegen van de afhankelijkheid zorgt ervoor dat alles wat nodig is voor **tekst extraheren uit png**, **tekst extraheren uit jpg**, en **tekst extraheren uit tiff** wordt meegeleverd. Er zijn geen extra native bibliotheken nodig.

## Stap 2: definieer de afbeeldingsbestanden die je wilt verwerken

Nu vertellen we de OCR‑engine welke bestanden verwerkt moeten worden. Hier komt **hoe batch‑OCR** echt van pas—geef simpelweg een lijst met paden door en laat de bibliotheek het zware werk doen.

```java
import java.util.Arrays;
import java.util.List;

// Step 2: List your image files (PNG, JPG, TIFF)
List<String> imageFiles = Arrays.asList(
        "YOUR_DIRECTORY/img1.png",   // PNG file – recognize text from png
        "YOUR_DIRECTORY/img2.jpg",   // JPG file – recognize text from jpg
        "YOUR_DIRECTORY/img3.tif");  // TIFF file – recognize text from tiff
```

> **Pro‑tip:** Houd je bestandspaden absoluut of gebruik `Paths.get(...)` om verrassingen op verschillende besturingssystemen te voorkomen.

## Stap 3: maak de batchprocessor en stel parallelisme af

Aspose OCR levert `OcrBatchProcessor` mee, die meerdere herkenningen parallel kan uitvoeren. Het beperken van het aantal threads voorkomt dat je app te veel CPU verbruikt wanneer je tientallen afbeeldingen hebt.

```java
import com.aspose.ocr.OcrBatchProcessor;

// Step 3: Initialise the batch processor
OcrBatchProcessor ocrProcessor = new OcrBatchProcessor();

// Limit to 4 concurrent threads – a sweet spot for most desktops
ocrProcessor.setMaxParallelism(4);
```

Waarom parallelisme beperken? Als je te veel threads op een bescheiden laptop draait, kun je een vertraging in plaats van een versnelling ervaren. Met `setMaxParallelism` kun je snelheid en stabiliteit in balans brengen.

## Stap 4: voer de batch‑OCR‑aanroep uit

Hier is de kern van **hoe batch‑OCR**: een enkele `recognize`‑aanroep die een lijst van `RecognitionResult`‑objecten teruggeeft, één per afbeelding.  
`recognize` verwerkt de opgegeven afbeeldingen en retourneert een lijst van `RecognitionResult`‑objecten, elk met de geëxtraheerde tekst.

```java
import com.aspose.ocr.RecognitionResult;
import java.util.List;

// Step 4: Execute batch OCR
List<RecognitionResult> recognitionResults = ocrProcessor.recognize(imageFiles);
```

De methode blokkeert tot elke afbeelding is verwerkt, waarna de tekst wordt teruggegeven. Als je niet‑blokerend gedrag nodig hebt, kun je dit wikkelen in een `CompletableFuture`, maar voor de meeste scripts houdt de synchrone aanroep de code overzichtelijk.

## Stap 5: print de geëxtraheerde tekst

Tot slot itereren we over de resultaten en tonen we de herkende strings. Dit toont aan dat we succesvol **tekst uit afbeeldingen** van verschillende formaten hebben **geëxtraheerd**.  
`RecognitionResult` bevat de OCR‑output voor één afbeelding, inclusief de geëxtraheerde tekst en een vertrouwensscore.

```java
// Step 5: Output the recognized text for each file
for (int i = 0; i < recognitionResults.size(); i++) {
    System.out.println("File: " + imageFiles.get(i));
    System.out.println(recognitionResults.get(i).getText());
    System.out.println("---");
}
```

### Verwachte output

```
File: YOUR_DIRECTORY/img1.png
The quick brown fox jumps over the lazy dog.
---
File: YOUR_DIRECTORY/img2.jpg
Invoice #12345
Total: $567.89
---
File: YOUR_DIRECTORY/img3.tif
Page 1 of 3
Report generated on 2026-02-09
---
```

Als de OCR‑engine een bestand niet kan lezen, retourneert de `getText()`‑methode een lege string, zodat je een eenvoudige controle kunt toevoegen om waarschuwingen te loggen.

## Volledig werkend voorbeeld

Alles bij elkaar, hier is de complete, kant‑klaar Java‑klasse. Kopieer deze naar een bestand genaamd `BatchOcrTutorial.java`, pas de afbeeldingspaden aan en voer `javac && java` uit.

```java
import com.aspose.ocr.*;
import java.util.Arrays;
import java.util.List;

public class BatchOcrTutorial {
    public static void main(String[] args) throws Exception {

        // Step 1: Define the image files to be processed
        List<String> imageFiles = Arrays.asList(
                "YOUR_DIRECTORY/img1.png",
                "YOUR_DIRECTORY/img2.jpg",
                "YOUR_DIRECTORY/img3.tif");

        // Step 2: Create the batch OCR processor and optionally limit parallelism
        OcrBatchProcessor ocrProcessor = new OcrBatchProcessor();
        ocrProcessor.setMaxParallelism(4); // limit to 4 concurrent threads

        // Step 3: Perform OCR on all images in a single batch call
        List<RecognitionResult> recognitionResults = ocrProcessor.recognize(imageFiles);

        // Step 4: Output the recognized text for each file
        for (int i = 0; i < recognitionResults.size(); i++) {
            System.out.println("File: " + imageFiles.get(i));
            System.out.println(recognitionResults.get(i).getText());
            System.out.println("---");
        }
    }
}
```

Voer het uit, en je ziet de console de geëxtraheerde tekst voor elke PNG, JPG en TIFF‑bestand afdrukken—precies wat je nodig hebt wanneer **hoe batch‑OCR** de vraag is.

## Veelgestelde vragen & randgevallen

### Wat als ik meer dan drie afbeeldingen heb?
Voeg gewoon meer items toe aan de `imageFiles`‑lijst. De batchprocessor splitst het werk automatisch over de threads die je met `setMaxParallelism` hebt geconfigureerd.

### Mijn afbeeldingen staan in een submap—moet ik ze handmatig opsommen?
`Files.list` retourneert een lui gevulde stream van paden in een directory.

```java
try (Stream<Path> paths = Files.walk(Paths.get("YOUR_DIRECTORY"))) {
    List<String> imageFiles = paths
        .filter(Files::isRegularFile)
        .filter(p -> p.toString().matches(".*\\.(png|jpg|tif|tiff)$"))
        .map(Path::toString)
        .collect(Collectors.toList());
}
```

Dit houdt de code flexibel en respecteert nog steeds **hoe batch‑OCR**.

### Hoe ga ik om met resultaten met lage betrouwbaarheid?
`getConfidence()` geeft een numerieke vertrouwenswaarde terug die aangeeft hoe waarschijnlijk de herkende tekst correct is.

```java
ocrProcessor.setResolution(300); // increase DPI for better accuracy
```

### Ondersteunt Aspose OCR andere talen?
Ja—roep `ocrProcessor.setLanguage(OcrLanguage.Spanish)` (of een andere ondersteunde enum) aan vóór de `recognize`‑aanroep. Hiermee breid je de functionaliteit uit voorbij het Engels, waardoor **tekst uit afbeeldingen** echt meertalig wordt.

## Prestatietips

* **Batch‑grootte is belangrijk** – Grotere batches verminderen overhead, maar zeer grote lijsten kunnen meer geheugen verbruiken. Test met 50–200 afbeeldingen per batch.
* **Parallelisme** – Op een 4‑core CPU levert `setMaxParallelism(4)` meestal de beste doorvoer. Pas aan op basis van de belasting van je server.
* **Afbeelding voorbewerken** – Het omzetten van afbeeldingen naar grijstinten of het verhogen van het contrast vóór OCR kan de nauwkeurigheid verbeteren, vooral bij ruisende scans.

## Conclusie

Je weet nu **hoe batch‑OCR** in Java te gebruiken met Aspose OCR, hoe **tekst uit afbeeldingen** van verschillende formaten te **extraheren**, en waarom het beheersen van parallelisme van belang is. Het volledige code‑voorbeeld toont hoe je tekst uit PNG, JPG en TIFF‑bestanden in één efficiënte aanroep herkent.

Klaar voor de volgende stap? Stuur de OCR‑output naar een zoekindex, een database of een AI‑samenvatter. Je kunt ook experimenteren met PDF‑invoer (Aspose OCR ondersteunt dit) of dit combineren met beeld‑voorbewerkingsbibliotheken zoals OpenCV voor nog hogere nauwkeurigheid.

Veel programmeerplezier, en onthoud—batch OCR hoeft geen hoofdpijn te zijn. Met de juiste tools en een duidelijk patroon zet je stapels afbeeldingen om in doorzoekbare tekst in een mum van tijd.

## Veelgestelde vragen

**Q: Kan ik dit op een headless server draaien?**  
A: Ja, Aspose OCR is pure Java en vereist geen UI‑componenten, dus het werkt perfect in headless omgevingen.

**Q: Is een licentie vereist voor productiegebruik?**  
A: Een commerciële licentie is nodig voor productiedeployments; een gratis proefversie is beschikbaar voor evaluatie.

**Q: Welke besturingssystemen worden ondersteund?**  
A: Elk OS dat Java 17+ kan draaien, inclusief Windows, Linux en macOS.

**Q: Hoeveel talen kan Aspose OCR herkennen?**  
A: Meer dan 60 talen worden direct ondersteund, variërend van Engels en Spaans tot Arabisch en Chinees.

**Q: Wat is de maximale bestandsgrootte die Aspose OCR aankan?**  
A: Individuele afbeeldingsbestanden tot 200 MB worden ondersteund; grotere bestanden moeten vóór verwerking worden gesplitst.

---

**Last Updated:** 2026-09-18  
**Tested with:** Aspose OCR 24.9 for Java  
**Author:** Aspose

## Gerelateerde tutorials

- [Tekst extraheren uit afbeeldingen – OCR-basis voor Java](/ocr/java/ocr-basics/)
- [Hoe batch-OCR in Java – Complete gids om tekst uit te extraheren](/ocr/java/ocr-operations/how-to-batch-ocr-in-java-complete-guide-to-extract-text-from/)
- [Afbeelding voorbewerken OCR in Java – Nauwkeurigheid verhogen, tekst extraheren](/ocr/java/advanced-ocr-techniques/preprocess-image-ocr-in-java-boost-accuracy-extract-text/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}