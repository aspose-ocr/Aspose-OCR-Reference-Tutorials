---
category: general
date: 2026-08-12
description: herken tekst van afbeelding met Java OCR‑engine. Leer hoe je tekst uit
  een afbeelding kunt extraheren, de OCR‑nauwkeurigheid kunt verbeteren en de afbeelding
  kunt voorbewerken voor OCR op PNG‑bestanden.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- recognize text from image
- how to extract text from image
- how to improve OCR accuracy
- how to preprocess image for OCR
- perform OCR on PNG
language: nl
lastmod: 2026-08-12
og_description: herken tekst van afbeelding met Java. Deze tutorial laat zien hoe
  je tekst uit een afbeelding kunt extraheren, de OCR‑nauwkeurigheid kunt verhogen
  en OCR op PNG kunt uitvoeren met behulp van multithreading en GPU.
og_image_alt: Diagram showing Java OCR engine recognizing text from image
og_title: tekst herkennen uit afbeelding in Java – stap‑voor‑stap OCR‑tutorial
schemas:
- author: Aspose
  dateModified: '2026-08-12'
  description: recognize text from image using Java OCR engine. Learn how to extract
    text from image, improve OCR accuracy, and preprocess image for OCR on PNG files.
  headline: recognize text from image in Java – complete OCR guide
  type: TechArticle
- description: recognize text from image using Java OCR engine. Learn how to extract
    text from image, improve OCR accuracy, and preprocess image for OCR on PNG files.
  name: recognize text from image in Java – complete OCR guide
  steps:
  - name: Explanation of each step
    text: '| Step | Why it matters | How it helps you **recognize text from image**
      | |------|----------------|-----------------------------------------------|
      | 1️⃣ Create the OCR engine | Instantiates the core component that drives all
      subsequent operations. | Provides the entry point for all OCR actions. | '
  - name: Expected output
    text: 'If `sample-image.png` contains the sentence “Hello, world! 123”, the console
      will display something similar to:'
  - name: 1. Binarization with Otsu’s method
    text: '```java import java.awt.image.BufferedImage; import com.example.image.Binarizer;
      // hypothetical helper class'
  - name: 2. Scaling to 300 dpi
    text: '```java import com.example.image.Resizer;'
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: tekst herkennen uit afbeelding in Java – volledige OCR-gids
url: /nl/java/advanced-ocr-techniques/recognize-text-from-image-in-java-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# tekst uit afbeelding herkennen in Java – volledige OCR-gids

Als je **tekst uit afbeelding** moet herkennen in een Java‑applicatie, laat deze tutorial je precies zien hoe. Aan het einde van de gids kun je tekst uit afbeeldingsbestanden extraheren, de OCR‑nauwkeurigheid verbeteren en OCR uitvoeren op PNG‑bestanden met multi‑core‑ en GPU‑ondersteuning.

Veel ontwikkelaars vragen zich af **hoe je tekst uit afbeelding kunt extraheren** zonder een eigen neuraal netwerk te schrijven. De oplossing is een beproefde OCR‑engine te gebruiken, deze te configureren voor snelheid en nauwkeurigheid, en de juiste preprocessing‑stappen toe te passen. De volgende secties leiden je door elke vereiste, zodat je de code direct in je project kunt kopiëren.

## Wat je zult leren

* Een OCR‑engine opzetten in Java.
* Multi‑threading inschakelen en optionele GPU‑versnelling.
* Taalpakketten toevoegen voor Engels en Spaans.
* Afbeeldings‑preprocessing‑filters toepassen om de herkenningskwaliteit te verbeteren.
* De ingebouwde spell‑corrector inschakelen voor schonere output.
* OCR uitvoeren op PNG‑bestanden en de herkende tekst afdrukken.

Er zijn geen externe services nodig—alles draait lokaal, waardoor het ideaal is voor offline of privacy‑gevoelige toepassingen.

## Vereisten

* Java 17 of hoger (de code gebruikt de moderne `var`‑syntaxis maar kan worden teruggeporteerd).
* Een OCR‑bibliotheek die de klassen `OcrEngine`, `Language` en `EngineOptions` levert (bijv. **GroupDocs.Parser**, **Aspose.OCR**, of een compatibele SDK).
* Maven of Gradle voor afhankelijkheidsbeheer.
* Een voorbeeld‑PNG‑afbeelding (`sample-image.png`) geplaatst in `YOUR_DIRECTORY`.

> **Pro tip:** Als je van plan bent duizenden afbeeldingen te verwerken, reserveer dan voldoende RAM voor de GPU‑buffer en schakel de spell‑corrector alleen uit wanneer je ruwe OCR‑output nodig hebt.

## tekst uit afbeelding herkennen met Java OCR‑engine

Hieronder staat een complete, uitvoerbare Java‑programma dat de acht stappen volgt die in het oorspronkelijke fragment worden getoond. Het bevat imports, een `main`‑methode en inline‑commentaren die het doel van elke regel uitleggen.

```java
// File: OcrDemo.java
import com.example.ocr.OcrEngine;            // Replace with your OCR library's package
import com.example.ocr.Language;
import com.example.ocr.EngineOptions;
import com.example.ocr.ImagePreprocessingOptions;

public class OcrDemo {

    public static void main(String[] args) {
        // Step 1: Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Enable multi‑core processing for faster throughput
        ocrEngine.getEngineOptions().setUseMultiThreading(true);

        // Step 3: (Optional) Turn on GPU acceleration if a compatible GPU is present
        ocrEngine.getEngineOptions().setUseGpu(true);

        // Step 4: Add the languages you want to recognize (English and Spanish)
        ocrEngine.getLanguage().add(Language.English);
        ocrEngine.getLanguage().add(Language.Spanish);

        // Step 5: Apply common image‑preprocessing filters to improve OCR accuracy
        ImagePreprocessingOptions imgOpts = ocrEngine.getImagePreprocessingOptions();
        imgOpts.setRotate(true);   // Auto‑rotate based on EXIF orientation
        imgOpts.setDeskew(true);   // Straighten skewed text lines
        imgOpts.setDenoise(true);  // Reduce background noise

        // Step 6: Enable the built‑in spell corrector for cleaner output
        ocrEngine.getEngineOptions().setUseSpellCorrector(true);

        // Step 7: Perform OCR on the target PNG image
        // This demonstrates how to perform OCR on PNG files efficiently.
        String imagePath = "YOUR_DIRECTORY/sample-image.png";
        String ocrResult = ocrEngine.recognizeImage(imagePath);

        // Step 8: Output the recognized text
        System.out.println("=== OCR Result ===");
        System.out.println(ocrResult);
    }
}
```

### Uitleg van elke stap

| Stap | Waarom het belangrijk is | Hoe het je helpt **tekst uit afbeelding te herkennen** |
|------|--------------------------|------------------------------------------------------|
| 1️⃣ Create the OCR engine | Instantiëert de kerncomponent die alle volgende bewerkingen aandrijft. | Biedt het toegangspunt voor alle OCR‑acties. |
| 2️⃣ Enable multi‑core processing | Moderne CPU's hebben meerdere kernen; ze benutten verkort de totale verwerkingstijd. | Versnelt batch‑taken wanneer je **OCR uitvoert op PNG**‑bestanden parallel. |
| 3️⃣ Turn on GPU acceleration (optional) | GPU's blinken uit in parallelle pixelbewerkingen, vooral bij grote afbeeldingen. | Kan de herkenningstijd met tot 70 % verkorten op ondersteunde hardware. |
| 4️⃣ Add language packs | OCR‑nauwkeurigheid hangt af van taalmodellen; alleen de benodigde talen opgeven vermindert valse positieven. | Verbetert de kans om tekens correct te identificeren wanneer je **hoe je tekst uit afbeelding kunt extraheren** in meertalige scenario's. |
| 5️⃣ Image preprocessing | Rotatie, kantcorrectie en ruisonderdrukking verhelpen veelvoorkomende scanproblemen. | Direct **hoe je OCR‑nauwkeurigheid kunt verbeteren** door een schonere bitmap aan de engine te presenteren. |
| 6️⃣ Spell corrector | Post‑processing stap die veelvoorkomende OCR‑spelfouten corrigeert. | Levert meer leesbare output zonder handmatige opschoning. |
| 7️⃣ Perform OCR on PNG | De `recognizeImage`‑methode leest het bestand, past preprocessing toe en voert de herkenningspipeline uit. | Toont **OCR uitvoeren op PNG** terwijl format‑specifieke eigenaardigheden (bijv. verliesloze compressie) worden afgehandeld. |
| 8️⃣ Print result | Geeft je directe feedback om succes te verifiëren. | Staat je toe te bevestigen dat de tekst correct **herkend uit afbeelding** is. |

### Verwachte output

Als `sample-image.png` de zin “Hello, world! 123” bevat, zal de console iets soortgelijks weergeven:

```
=== OCR Result ===
Hello, world! 123
```

De exacte output kan enigszins variëren afhankelijk van de beeldkwaliteit en taalinstellingen, maar de spell‑corrector zal meestal kleine mis‑herkenningen corrigeren, zoals “Helli” → “Hello”.

## hoe je afbeelding voor OCR preprocesses – dieper duiken

Hoewel de bovenstaande code de ingebouwde preprocessing van de engine gebruikt, kun je ook aangepaste filters toepassen voordat je de afbeelding aan de OCR‑engine geeft. Hieronder staan twee veelvoorkomende technieken:

### 1. Binarisatie met Otsu‑methode

```java
import java.awt.image.BufferedImage;
import com.example.image.Binarizer; // hypothetical helper class

BufferedImage original = ImageIO.read(new File(imagePath));
BufferedImage binary = Binarizer.otsuThreshold(original);
ocrEngine.recognizeImage(binary);
```

Binarisatie zet de afbeelding om naar zwart‑wit, wat vaak **hoe je OCR‑nauwkeurigheid kunt verbeteren** voor scans met laag contrast.

### 2. Schalen naar 300 dpi

```java
import com.example.image.Resizer;

BufferedImage scaled = Resizer.scaleToDPI(original, 300);
ocrEngine.recognizeImage(scaled);
```

De meeste OCR‑engines verwachten minstens 300 dpi voor optimale tekenherkenning. Schalen voorkomt dat de engine kleine glyphs verkeerd leest.

> **Opmerking:** Als je zowel aangepaste preprocessing als de ingebouwde opties van de engine inschakelt, zal de engine zijn filters *na* de jouwe toepassen. Kies de volgorde die het beste bij de kenmerken van je afbeelding past.

## hoe je tekst uit afbeelding extraheert – omgaan met randgevallen

| Situatie | Aanbevolen aanpassing |
|----------|-----------------------|
| **Zeer ruisachtige achtergrond** | Verhoog de intensiteit van `setDenoise(true)` of voer een medianfilter uit vóór OCR. |
| **Kanteling > 15°** | Gebruik `setDeskew(true)` *en* geef een handmatige rotatiehoek op via `imgOpts.setRotateAngle(θ)`. |
| **Gemengde talen (bijv. Engels + Spaans)** | Voeg beide taalpakketten toe zoals getoond in Stap 4; de engine schakelt automatisch van context. |
| **Grote PDF's geconverteerd naar PNG** | Verwerk elke pagina als een aparte PNG en voeg de resultaten samen; multi‑threading (Stap 2) houdt de totale tijd laag. |
| **GPU niet beschikbaar** | Houd `setUseGpu(true)` aan maar wikkel het in een try‑catch; de engine valt terug op CPU zonder te crashen. |

## OCR uitvoeren op PNG – batch‑verwerking voorbeeld

Wanneer je **OCR moet uitvoeren op PNG**‑bestanden in een map, werkt een eenvoudige lus met dezelfde engine‑instantie goed:

```java
Path dir = Paths.get("YOUR_DIRECTORY");
try (Stream<Path> files = Files.list(dir)) {
    files.filter(p -> p.toString().endsWith(".png"))
         .forEach(p -> {
             String text = ocrEngine.recognizeImage(p.toString());
             System.out.println("File: " + p.getFileName());
             System.out.println(text);
             System.out.println("---");
         });
}
```

Omdat de engine al is geconfigureerd voor multi‑core en GPU, kan deze lus tientallen afbeeldingen parallel verwerken zonder extra code.

## Volledig werkend voorbeeld

Als we alles samenvoegen, hier is een zelfstandige klasse die je kunt kopiëren‑plakken in een IDE, de juiste Maven‑dependency kunt toevoegen, en direct kunt uitvoeren:



## Wat je hierna zou moeten leren

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat complete werkende code‑voorbeelden met stap‑voor‑stap‑uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Hoe OCR‑afbeeldingstekst met taal te gebruiken met Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Tekst uit afbeelding extraheren in Java met Aspose.OCR Detect Areas‑modus](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [afbeelding naar tekst java: Afbeelding naar tekst converteren met Aspose.OCR](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}