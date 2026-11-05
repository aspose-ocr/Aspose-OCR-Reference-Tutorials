---
category: general
date: 2026-06-06
description: hoe OCR uit te voeren in Java – snel tekst uit een afbeelding extraheren,
  afbeelding naar tekst converteren en tekst uit een jpg lezen met een eenvoudig codevoorbeeld.
draft: false
keywords:
- how to perform OCR
- ocr in java
- extract text from image
- convert image to text
- read text from jpg
language: nl
og_description: hoe OCR uit te voeren in Java – leer hoe je tekst uit een afbeelding
  haalt, afbeelding naar tekst converteert en tekst uit een jpg leest met een kant‑klaar
  voorbeeld.
og_title: Hoe OCR in Java uit te voeren – Stapsgewijze gids
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
title: Hoe OCR uit te voeren in Java – Complete gids voor het extraheren van tekst
  uit afbeeldingen
url: /nl/java/ocr-basics/how-to-perform-ocr-in-java-complete-guide-to-extract-text-fr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe OCR uit te voeren in Java – Complete gids om tekst uit afbeeldingen te extraheren

Heb je je ooit afgevraagd **how to perform OCR** op een foto die je met je telefoon hebt gemaakt? Je bent niet de enige. Of je nu een bon‑scanapp bouwt of gewoon tekst uit een gescande PDF wilt halen, **how to perform OCR** in Java is een vaardigheid die zich snel terugbetaalt. In deze tutorial lopen we een praktisch voorbeeld door dat **extracts text from image** bestanden, **converts image to text**, en zelfs laat zien hoe je **read text from jpg** met slechts een paar regels code.

> *Pro tip:* Dezelfde aanpak werkt voor PNG, BMP, of elk formaat dat de OCR‑engine ondersteunt—vervang gewoon de bestandsnaam.

## Hoe OCR uit te voeren in Java – Overzicht

Optical Character Recognition (OCR) is de technologie die afbeeldingen van letters omzet in daadwerkelijke, doorzoekbare tekst. In het Java‑ecosysteem zijn er verschillende bibliotheken—Tesseract, Asprise en commerciële SDK’s—die een vergelijkbare workflow bieden: een afbeelding laden, de engine vertellen welke taal verwacht wordt, de herkenning uitvoeren en het resultaat ophalen. Hieronder gebruiken we een generieke `OcrEngine`‑klasse om het voorbeeld duidelijk te houden, maar je kunt deze vervangen door elke concrete implementatie die hetzelfde patroon volgt.

### Wat je zult leren

- Installeer een OCR‑bibliotheek (ja, **ocr in java** is makkelijker dan je denkt).
- Maak en configureer een OCR‑engine‑instantie.
- Laad een JPG (of een andere afbeelding) en stel de taal in.
- Verwerk de afbeelding en **extract text from image** bestanden.
- Print de herkende string naar de console.

![voorbeeld van OCR uitvoeren](ocr-example.png "illustratie van OCR uitvoeren in Java")

## Stap 1 – Installeer en importeer een OCR‑bibliotheek (ocr in java)

Voordat je een enkele regel Java schrijft, heb je een bibliotheek nodig die het zware werk daadwerkelijk doet. Als je Maven gebruikt, voeg dan een afhankelijkheid toe zoals deze (vervang `com.example.ocr` door de echte group‑ID van de SDK die je gekozen hebt):

```xml
<dependency>
    <groupId>com.example</groupId>
    <artifactId>ocr-sdk</artifactId>
    <version>1.4.2</version>
</dependency>
```

Als je de voorkeur geeft aan Gradle:

```gradle
implementation 'com.example:ocr-sdk:1.4.2'
```

Zodra de JAR op je classpath staat, importeer je de klassen die je nodig hebt:

```java
import com.example.ocr.OcrEngine;
import com.example.ocr.OcrInputImage;
import com.example.ocr.OcrResult;
```

> **Waarom dit belangrijk is:** Het importeren van de juiste klassen voorkomt “cannot find symbol”-fouten en maakt je IDE blij—niets is frustrerender dan een ontbrekende import wanneer je probeert **convert image to text**.

## Stap 2 – Maak de OCR‑engine‑instantie (how to perform OCR)

Nu de bibliotheek klaar is, start je de engine. Beschouw de engine als het brein dat naar de pixels kijkt en de letters raadt.

```java
// Step 2: Create an OCR engine instance
OcrEngine ocrEngine = new OcrEngine();
```

Het maken van de engine is meestal goedkoop; de meeste SDK’s reserveren interne buffers lui, zodat je dezelfde instantie veilig kunt hergebruiken voor veel afbeeldingen als je een batch verwerkt.

## Stap 3 – Laad de afbeelding en stel de taal in (extract text from image)

De volgende stap is de engine iets te geven om te lezen. Hier laden we een JPEG van de schijf en vertellen we de OCR‑engine dat de tekst in het Mongools is (ISO 639‑2 code “mon”). Je kunt het pad of de taalcode aanpassen aan je gebruikssituatie.

```java
// Step 3: Load the image you want to recognize
ocrEngine.setImage(new OcrInputImage("YOUR_DIRECTORY/input.jpg"));

// Step 3b: Specify the language (e.g., English = "eng", Mongolian = "mon")
ocrEngine.getSettings().setLanguage("mon");
```

> **Kanttekening:** Als je geen taal instelt, gebruikt de engine standaard Engels, wat de nauwkeurigheid drastisch kan verlagen wanneer de tekst daadwerkelijk Cyrillisch of een ander schrift is. Geef altijd de juiste taal op wanneer je kunt.

## Stap 4 – Verwerk de afbeelding en haal het resultaat op (convert image to text)

Met de afbeelding en taal ingesteld, vraag je de engine om zijn magie te doen. De `process()`‑aanroep voert het OCR‑algoritme uit en retourneert een `OcrResult`‑object dat de herkende string en vertrouwensscores bevat.

```java
// Step 4: Process the image and obtain the recognition result
OcrResult ocrResult = ocrEngine.process();
```

Achter de schermen kan de engine voorverwerking uitvoeren—kantelen corrigeren, binariseren, ruisreductie—zodat je die stappen niet zelf hoeft te schrijven. Daarom zijn de meeste moderne OCR‑bibliotheken een plezier om te gebruiken voor **convert image to text** taken.

## Stap 5 – Output de geëxtraheerde tekst (read text from jpg)

Trek tenslotte de platte tekst uit het resultaat en doe er iets nuttigs mee. Voor deze demo printen we het simpelweg naar de console, maar je zou het naar een bestand kunnen schrijven, in een zoekindex kunnen voeren, of doorgeven aan een andere service.

```java
// Step 5: Output the extracted text
System.out.println(ocrResult.getText());
```

Die regel alleen al bewijst dat je succesvol **read text from jpg** (of een ander ondersteund formaat) hebt uitgevoerd. Als de output er onduidelijk uitziet, controleer dan de taalcode en de beeldkwaliteit.

## Volledig werkend voorbeeld (Alle stappen gecombineerd)

Hieronder staat een complete, kant‑klaar Java‑klasse die alle onderdelen samenvoegt. Kopieer deze naar een bestand genaamd `OcrDemo.java`, pas het afbeeldingspad en de taal aan, en voer vervolgens `javac OcrDemo.java && java OcrDemo` uit.

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

### Verwachte output

Als `input.jpg` de Mongoolse zin “Сайн байна уу?” bevat, zal de console tonen:

```
=== Recognized Text ===
Сайн байна уу?
```

Als de afbeelding onscherp is of de taalcode onjuist, zie je onduidelijke tekens of een lege string—veelvoorkomende valkuilen die we hierna bespreken.

## Veelvoorkomende valkuilen en hoe ze op te lossen

| Symptoom | Waarschijnlijke oorzaak | Oplossing |
|----------|--------------------------|-----------|
| Vervormde Cyrillische tekens | Verkeerde taalcode (standaard Engels) | Set `ocrEngine.getSettings().setLanguage("mon")` or the appropriate code. |
| Geen output | Afbeeldingspad onjuist of bestand onleesbaar | Verify the path, ensure the file exists, and that the process has read permissions. |
| Lage nauwkeurigheid (<70 %) | Afbeelding heeft weinig contrast of is gedraaid | Pre‑process the image: increase contrast, deskew, or convert to grayscale before feeding it to the engine. |
| `OutOfMemoryError` bij grote PDF's | Veel hoge‑resolutie pagina's tegelijk laden | Process pages one at a time, or downscale images before OCR. |

### Pro tip: batchverwerking

Als je **extract text from image** bestanden in bulk moet verwerken, wikkel dan de kernlogica in een lus:

```java
for (File img : new File("batchFolder").listFiles()) {
    ocrEngine.setImage(new OcrInputImage(img.getAbsolutePath()));
    OcrResult r = ocrEngine.process();
    System.out.println(r.getText());
}
```

Dat fragment laat zien hoe eenvoudig het is om op te schalen van één JPG naar een hele map met scans.

## Verder gaan – Wat kun je hierna verkennen?

- **Taalpakketten:** De meeste OCR‑SDK’s laten je extra taaldata‑bestanden downloaden. Het toevoegen van een nieuw pakket stelt je in staat **convert image to text** voor talen buiten Engels en Mongools.
- **PDF OCR:** Combineer deze code met Apache PDFBox om

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stapsgewijze uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Tekst uit afbeeldingen extraheren – OCR‑basisprincipes met Aspose.OCR voor Java](/ocr/english/java/ocr-basics/)
- [Afbeelding naar tekst converteren in Java met Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [Hoe OCR‑afbeeldingstekst met taal te gebruiken met Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}