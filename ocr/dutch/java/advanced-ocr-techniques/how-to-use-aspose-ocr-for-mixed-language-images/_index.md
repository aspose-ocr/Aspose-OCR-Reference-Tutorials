---
category: general
date: 2026-05-06
description: Hoe gebruik je Aspose OCR om tekst uit een afbeelding te herkennen, automatische
  taalherkenning in te schakelen en de OCR-snelheid in Java te verbeteren.
draft: false
keywords:
- how to use aspose
- recognize text from image
- improve ocr speed
- load image for ocr
- enable automatic language detection
language: nl
og_description: Hoe u Aspose OCR gebruikt om snel tekst uit een afbeelding te herkennen,
  automatische taaldetectie in te schakelen en de OCR-snelheid in Java te verbeteren.
og_title: Hoe Aspose OCR te gebruiken voor meertalige afbeeldingen
tags:
- Aspose
- OCR
- Java
- Image Processing
title: Hoe gebruik je Aspose OCR voor meertalige afbeeldingen
url: /nl/java/advanced-ocr-techniques/how-to-use-aspose-ocr-for-mixed-language-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe Aspose OCR te gebruiken voor afbeeldingen met meerdere talen

Heb je je ooit afgevraagd **hoe je Aspose** kunt gebruiken om tekst uit een afbeelding te halen die meerdere talen tegelijk bevat? Je bent niet de enige—ontwikkelaars lopen vaak tegen een muur aan wanneer een afbeelding Engels, Russisch, Hindi of een andere schrijfwijze combineert. Het goede nieuws is dat Aspose OCR dit soepel afhandelt, en je kunt zelfs **tekst uit afbeelding herkennen** sneller door de taallijst te verkleinen.

In deze tutorial lopen we stap voor stap door een compleet, kant‑klaar Java‑voorbeeld dat **afbeelding voor OCR laadt**, **automatische taaldetectie** inschakelt, en een eenvoudige truc toont om **OCR‑snelheid te verbeteren**. Aan het einde heb je een zelfstandige applicatie die de geëxtraheerde tekst naar de console print, en begrijp je waarom elke instelling belangrijk is.

> **Prerequisites** – Java 17+ geïnstalleerd, Maven of Gradle voor afhankelijkheidsbeheer, en een Aspose OCR‑licentie (de gratis proefversie werkt voor evaluatie). Geen andere bibliotheken zijn vereist.

---

## Stap 1 – Voeg Aspose OCR toe aan je project

Voordat je **Aspose kunt gebruiken**, moet je de bibliotheek op je classpath hebben. Met Maven ziet dat er zo uit:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- check for the latest version -->
</dependency>
```

Als je de voorkeur geeft aan Gradle:

```groovy
implementation 'com.aspose:aspose-ocr:23.12'
```

> **Pro tip:** Blijf bij de nieuwste stabiele release; nieuwere versies bevatten vaak prestatie‑verbeteringen die direct invloed hebben op **OCR‑snelheid verbeteren**.

---

## Stap 2 – Maak een OCR‑engine‑instantie  

Het hart van elke Aspose OCR‑workflow is de `OcrEngine`. Het instantieren is eenvoudig, maar het is het vermelden waard dat de engine interne caches bevat. Het hergebruiken van één instantie voor veel afbeeldingen kan de **OCR‑snelheid verbeteren** omdat de bibliotheek herhaalde native initialisatie vermijdt.

```java
import com.aspose.ocr.*;

public class MixedLanguageDemo {
    public static void main(String[] args) throws Exception {
        // Step 2: Initialise the OCR engine – one instance per application is ideal
        OcrEngine ocrEngine = new OcrEngine();
```

---

## Stap 3 – **Afbeelding voor OCR laden**  

Aspose ondersteunt veel afbeeldingsformaten (PNG, JPEG, TIFF, BMP). Hier demonstreren we het laden van een PNG die Engelse, Russische en Hindi‑tekst bevat. De `ImageStream.fromFile`‑helper abstraheert de bestand‑I/O‑details en zorgt ervoor dat de afbeelding correct naar de engine wordt gestreamd.

```java
        // Step 3: Load the picture that holds mixed languages
        // Replace the path with the actual location of your image file
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/mixed-lang.png"));
```

> **Wat als de afbeelding in het geheugen staat?** Gebruik in plaats daarvan `ImageStream.fromByteArray(byte[])`—perfect voor webservices die afbeeldingen ontvangen als byte‑streams.

---

## Stap 4 – Schakel automatische taaldetectie in  

Standaard gaat Aspose OCR uit van één taal, wat kan leiden tot onduidelijke output bij meertalige afbeeldingen. Het inschakelen van automatische detectie vertelt de engine om het schrift van elk tekstblok te sniffen vóór herkenning.

```java
        // Step 4: Turn on auto‑detect – this is the key to handling mixed‑language images
        ocrEngine.getSettings().setAutoDetectLanguage(true);
```

---

## Stap 5 – **OCR‑snelheid verbeteren** door de taalpools te beperken  

Volledige auto‑detectie scant elke taal die Aspose ondersteunt (meer dan 70). Als je de mogelijke talen van tevoren kent, kun je de engine een hint geven. Het leveren van een kleinere array verkleint de zoekruimte en **verbetert daardoor de OCR‑snelheid**.

```java
        // Step 5 (optional but recommended): Limit detection to known languages
        // "en" = English, "ru" = Russian, "hi" = Hindi
        ocrEngine.getSettings().setPossibleLanguages(new String[] { "en", "ru", "hi" });
```

> **Waarom helpt dit?** De engine slaat taalmodellen over die niet nodig zijn, waardoor CPU‑cycli en geheugen worden bespaard. Als je later meer talen toevoegt, werk je gewoon de array bij—geen code‑herwerking nodig.

---

## Stap 6 – Voer de herkenning uit en **tekst uit afbeelding herkennen**  

Nu gebeurt het zware werk. `recognize()` retourneert een `OcrResult`‑object dat de platte tekst, vertrouwensscores en zelfs de lay‑outinformatie bevat, mocht je die later nodig hebben.

```java
        // Step 6: Run the OCR process
        OcrResult ocrResult = ocrEngine.recognize();

        // Step 7: Output the recognized text to the console
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

### Verwachte console‑output

```
=== Extracted Text ===
Hello world!
Привет мир!
नमस्ते दुनिया!
```

Als de afbeelding extra ruis of scheefstaande tekst bevat, kun je lagere vertrouwensscores voor die regels zien. Overweeg in dat geval de afbeelding voor te bewerken (ontkanten, binariseren) voordat je deze aan Aspose doorgeeft.

---

## Veelgestelde vragen & randgevallen

### Wat als de afbeelding enorm is (bijv. >10 MP)?

Grote afbeeldingen verbruiken meer geheugen en kunnen de verwerking vertragen. Een snelle manier om de **OCR‑snelheid te verbeteren** is de afbeelding te verkleinen terwijl de leesbaarheid behouden blijft:

```java
// Example using java.awt for simple resizing (optional)
BufferedImage original = ImageIO.read(new File("large.png"));
int targetWidth = 2000; // adjust based on your needs
BufferedImage resized = new BufferedImage(targetWidth,
        (original.getHeight() * targetWidth) / original.getWidth(),
        BufferedImage.TYPE_INT_RGB);
Graphics2D g = resized.createGraphics();
g.drawImage(original, 0, 0, targetWidth, resized.getHeight(), null);
g.dispose();
ocrEngine.setImage(ImageStream.fromImage(resized));
```

### Hoe ga ik om met rechts‑naar‑links scripts zoals Arabisch?

Aspose OCR respecteert automatisch de script‑richting, maar je wilt misschien de `RightToLeft`‑vlag instellen voor nabewerking:

```java
ocrEngine.getSettings().setRightToLeft(true);
```

### Kan ik tekst uit PDF's halen in plaats van afbeeldingen?

Ja—converteer elke PDF‑pagina naar een afbeelding (met Aspose PDF of een rasterizer) en voer het resultaat in dezelfde OCR‑pipeline. Dezelfde **tekst uit afbeelding herkennen**‑logica is van toepassing.

---

## Volledig werkend voorbeeld (klaar om te kopiëren‑plakken)

```java
import com.aspose.ocr.*;
import java.io.File;

/**
 * Demonstrates how to use Aspose OCR to recognize text from an image
 * that contains multiple languages, with automatic language detection
 * and a speed‑optimising language whitelist.
 */
public class MixedLanguageDemo {
    public static void main(String[] args) throws Exception {
        // Initialise the OCR engine – reuse this instance for many images
        OcrEngine ocrEngine = new OcrEngine();

        // Load the image that holds mixed languages (replace with your path)
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/mixed-lang.png"));

        // Enable automatic detection of language per text block
        ocrEngine.getSettings().setAutoDetectLanguage(true);

        // OPTIONAL: Restrict detection to English, Russian, and Hindi to boost speed
        ocrEngine.getSettings().setPossibleLanguages(new String[] { "en", "ru", "hi" });

        // Run OCR and capture the result
        OcrResult ocrResult = ocrEngine.recognize();

        // Print the extracted text
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

Sla het bestand op als `MixedLanguageDemo.java`, compileer met `javac` en voer uit met `java MixedLanguageDemo`. Als alles correct is ingesteld, zie je de meertalige tekst in de console verschijnen.

---

## Conclusie

Je weet nu **hoe je Aspose** kunt gebruiken om **tekst uit afbeelding** te **herkennen** in bestanden die meerdere talen bevatten, hoe je **automatische taaldetectie** inschakelt, en een praktische tip om de **OCR‑snelheid te verbeteren** door de taalpools te beperken. De volledige code hierboven staat klaar om te kopiëren‑plakken, en de uitleg geeft je vertrouwen om de oplossing aan te passen—of je nu **afbeelding voor OCR** moet **laden** vanuit een stream, een byte‑array, of zelfs een webcam‑snapshot.

Volgende stappen? Probeer te experimenteren met:

* Toevoegen van afbeelding‑voorbewerking (denoise, binariseren) voor scans van lage kwaliteit.  
* Exporteren van `OcrResult` als JSON voor downstream‑services.  
* Integreren van de engine in een Spring Boot REST‑endpoint zodat clients afbeeldingen kunnen uploaden en direct geëxtraheerde tekst ontvangen.

Veel plezier met coderen, en moge je OCR‑pijplijnen snel, nauwkeurig en meertalig zijn!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}