---
category: general
date: 2026-11-17
description: Leer hoe je OCR op een afbeelding in Java uitvoert en tekst uit foto's
  haalt met een eenvoudig codevoorbeeld. Inclusief tips voor het lezen van afbeeldingen
  in Java.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to perform OCR
- extract text image
- read image java
- convert image to text
- image to text java
language: nl
lastmod: 2026-11-17
og_description: Hoe je OCR op een afbeelding in Java uitvoert en snel tekst extraheert.
  Volg deze gids om een afbeelding in Java te lezen en afbeelding naar tekst te converteren
  met een kant‑klaar voorbeeld.
og_image_alt: Screenshot showing Java code that performs OCR on an image
og_title: Hoe OCR op een afbeelding in Java uit te voeren – stapsgewijze handleiding
schemas:
- author: Aspose
  dateModified: '2026-11-17'
  description: Learn how to perform OCR on an image in Java and extract text from
    pictures using a simple code example. Includes read image Java tips.
  headline: How to perform OCR on an image in Java – step‑by‑step guide
  type: TechArticle
tags:
- OCR
- Java
- Image processing
- Text extraction
title: Hoe OCR op een afbeelding in Java uit te voeren – stapsgewijze handleiding
url: /nl/java/ocr-basics/how-to-perform-ocr-on-an-image-in-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe OCR uit te voeren op een afbeelding in Java – stapsgewijze handleiding

Als je **hoe OCR uit te voeren** op een afbeelding nodig hebt, laat deze tutorial je een complete, uitvoerbare oplossing in Java zien. Je ziet hoe je een afbeeldingsbestand leest, een OCR‑engine configureert en de tekst extraheert die de engine herkent.

Werken met gescande documenten, bonnen of screenshots vereist vaak het omzetten van visuele inhoud naar doorzoekbare tekst. Deze gids leidt je door elke stap, van het laden van de afbeelding tot het afdrukken van de geëxtraheerde tekst, en behandelt ook veelvoorkomende valkuilen zoals niet‑ondersteunde bestandsformaten en null‑resultaten.

## Vereisten

* Java Development Kit (JDK) 8 of nieuwer geïnstalleerd.
* Een build‑tool (Maven of Gradle) om de OCR‑bibliotheek te downloaden.
* Een afbeeldingsbestand (JPEG, PNG, BMP) dat je wilt verwerken.

De code gebruikt de **OCR library from the `com.asprise.ocr` package** omdat deze slechts één JAR vereist en op alle belangrijke platforms werkt. Vervang deze door een andere provider (Tesseract, Google Vision, enz.) door de import‑statements en engine‑initialisation code te wijzigen.

## Stap 1: Voeg de OCR‑afhankelijkheid toe

Als je Maven gebruikt, voeg dan de volgende afhankelijkheid toe aan je `pom.xml`:

```xml
<dependency>
    <groupId>com.asprise.ocr</groupId>
    <artifactId>asprise-ocr</artifactId>
    <version>1.2.0</version>
</dependency>
```

Voor Gradle, plaats deze regel in `build.gradle`:

```gradle
implementation 'com.asprise.ocr:asprise-ocr:1.2.0'
```

Deze regels zorgen ervoor dat de **read image Java** code kan compileren en dat de OCR‑engine beschikbaar is tijdens runtime.

## Stap 2: Lees de afbeelding met Java

Het lezen van een afbeeldingsbestand is de eerste concrete stap in elke **extract text image** workflow. Java’s ingebouwde `ImageIO`‑klasse verwerkt de meeste gangbare formaten.

```java
import java.awt.image.BufferedImage;
import java.io.File;
import javax.imageio.ImageIO;

/**
 * Loads an image from the supplied path.
 *
 * @param path absolute or relative path to the image file
 * @return a BufferedImage instance, or null if the file cannot be read
 */
private static BufferedImage loadImage(String path) {
    try {
        return ImageIO.read(new File(path));
    } catch (Exception e) {
        System.err.println("Failed to read image: " + e.getMessage());
        return null;
    }
}
```

**Why this matters:** `ImageIO.read` returns `null` for unsupported formats or corrupted files. The method above logs the problem and returns `null` so the next step can react gracefully.

## Stap 3: Maak en configureer de OCR‑engine

De OCR‑engine moet weten welke taal hij moet herkennen. Het instellen van de taal verbetert de nauwkeurigheid drastisch, vooral voor niet‑Engelse documenten.

```java
import com.asprise.ocr.Ocr;

/**
 * Instantiates an OCR engine configured for English.
 *
 * @return a ready‑to‑use Ocr object
 */
private static Ocr createEngine() {
    Ocr ocrEngine = new Ocr();
    // The first argument is the language; "eng" is the ISO code for English.
    ocrEngine.startEngine("eng", Ocr.SPEED_FAST);
    return ocrEngine;
}
```

**Why this matters:** Starting the engine is a relatively heavy operation, so you should create it once and reuse it for multiple images if your application processes batches.

## Stap 4: Voer OCR uit en zet de afbeelding om naar tekst

Nu de afbeelding is geladen en de engine klaar is, kun je de herkenningsstap uitvoeren. Dit is de kern van **how to perform OCR**.

```java
/**
 * Runs OCR on a BufferedImage and returns the recognized text.
 *
 * @param ocrEngine an initialized Ocr instance
 * @param image     the image to process
 * @return the extracted text, or an empty string if nothing is recognized
 */
private static String extractText(Ocr ocrEngine, BufferedImage image) {
    if (image == null) {
        return "";
    }
    // The third parameter (0) tells the engine to return plain text.
    String result = ocrEngine.recognize(image, 0);
    return result != null ? result.trim() : "";
}
```

**Edge‑case handling:** If the image is `null`, the method returns an empty string instead of throwing a `NullPointerException`. This makes the surrounding code more robust when dealing with user‑supplied files.

## Stap 5: Toon de geëxtraheerde tekst

Tot slot, print het resultaat naar de console of stuur het door naar een ander component (bijv. een database of een UI‑widget).

```java
/**
 * Demonstrates the full OCR workflow.
 *
 * @param args command‑line arguments (first argument = path to image)
 */
public static void main(String[] args) {
    if (args.length == 0) {
        System.err.println("Usage: java OcrDemo <path-to-image>");
        return;
    }

    String imagePath = args[0];
    BufferedImage image = loadImage(imagePath);
    Ocr ocrEngine = createEngine();

    String text = extractText(ocrEngine, image);
    System.out.println("=== Recognized Text ===");
    System.out.println(text.isEmpty() ? "(no text detected)" : text);

    // Clean up the OCR engine to free native resources.
    ocrEngine.stopEngine();
}
```

Wanneer je het programma uitvoert met `java OcrDemo sample.jpg`, toont de console de herkende tekens. Dit voltooit de **convert image to text** cyclus.

### Verwachte uitvoer

```
=== Recognized Text ===
The quick brown fox jumps over the lazy dog.
```

Als de afbeelding geen leesbare tekens bevat, print het programma `(no text detected)`.

## Veelvoorkomende variaties en hoe ze aan te passen

| Variatie | Wat verandert | Wanneer te gebruiken |
|----------|---------------|----------------------|
| **Andere taal** | Vervang `"eng"` door `"spa"` voor Spaans, `"fra"` voor Frans, enz. | Documenten geschreven in een andere taal dan Engels |
| **Batchverwerking** | Loop over een lijst met bestandspaden, hergebruik dezelfde `Ocr`‑instantie. | Grote sets gescande pagina's |
| **Hogere nauwkeurigheid** | Gebruik `Ocr.SPEED_SLOW` of schakel `ocrEngine.setConfig("tessedit_char_whitelist", "0123456789")` in voor alleen‑numerieke scans. | Wanneer OCR‑kwaliteit cruciaal is (bijv. factuurnummers) |
| **Tesseract‑alternatief** | Vervang de import door `net.sourceforge.tess4j.Tesseract` en pas de initialisatiecode aan. | Projecten die al afhankelijk zijn van Tesseract |

## Pro‑tips

* **Resize grote afbeeldingen** voordat je ze aan de engine geeft; OCR‑snelheid schaalt met het aantal pixels.
* **Pre‑process** de afbeelding (grijstinten, contrastverhoging) met bibliotheken zoals OpenCV als de bron ruis bevat.
* **Cache de OCR‑engine** als je deze vaak in een korte periode aanroept—het starten en stoppen van de engine veroorzaakt overhead.
* **Valideer het resultaat** met reguliere expressies wanneer je een specifiek formaat verwacht (bijv. datums, telefoonnummers).

## Conclusie

Je weet nu **hoe OCR uit te voeren** op een afbeelding in Java, van het lezen van het bestand tot het tonen van de geëxtraheerde tekst. De tutorial behandelde **read image Java**, **extract text image**, **convert image to text**, en **image to text java** technieken, en gaf praktische tips voor real‑world scenario's.  

Vanaf hier kun je:

* De OCR‑stap integreren in een webservice die uploads ontvangt.
* De output combineren met een zoekindex voor full‑text search over gescande documenten.
* Geavanceerde OCR‑opties verkennen zoals multi‑language support of aangepaste tekensets.

Happy coding, and enjoy turning pictures into searchable text!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids zijn gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Hoe OCR te gebruiken in Java – Tekst extraheren uit afbeelding met spellingscorrectie](/ocr/english/java/ocr-operations/how-to-use-ocr-in-java-extract-text-from-image-with-spell-co/)
- [Afbeelding naar tekst converteren in Java met Aspose OCR – Volledige gids](/ocr/english/java/ocr-operations/convert-image-to-text-in-java-using-aspose-ocr-full-guide/)
- [Hoe GPU in te schakelen voor OCR in Java – Tekst extraheren uit afbeelding](/ocr/english/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-extract-text-from-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}