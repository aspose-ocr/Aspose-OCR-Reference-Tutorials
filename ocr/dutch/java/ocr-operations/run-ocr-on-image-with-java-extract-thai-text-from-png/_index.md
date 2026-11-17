---
category: general
date: 2026-03-28
description: Voer OCR uit op een afbeelding in Java met Aspose OCR om de afbeelding
  naar tekst te converteren, en extraheer Thaise tekst uit PNG snel en betrouwbaar.
draft: false
keywords:
- run OCR on image
- convert image to text
- extract text from PNG
- extract Thai text
- recognize Thai text
language: nl
og_description: Voer OCR uit op een afbeelding met Java en Aspose OCR. Leer hoe je
  een afbeelding naar tekst converteert, Thaise tekst uit een PNG haalt en veelvoorkomende
  valkuilen aanpakt.
og_title: Voer OCR uit op een afbeelding met Java – Haal Thaise tekst snel eruit
tags:
- OCR
- Java
- Aspose
- Image Processing
title: Voer OCR uit op afbeelding met Java – Extraheer Thaise tekst uit PNG
url: /nl/java/ocr-operations/run-ocr-on-image-with-java-extract-thai-text-from-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR uitvoeren op afbeelding met Java – Volledige tutorial

Heb je je ooit afgevraagd hoe je **OCR op afbeelding**‑bestanden direct vanuit Java‑code kunt uitvoeren? Misschien heb je een verzameling Thaise bonnen, gescande documenten of screenshots en heb je de tekst nodig zonder deze handmatig te hoeven typen. Dat is een veelvoorkomend pijnpunt, vooral wanneer de bron een PNG is en de taal niet‑Latijns.  

In deze gids laten we je precies zien hoe je **OCR op afbeelding** kunt uitvoeren met de Aspose OCR‑bibliotheek, de foto kunt omzetten naar platte tekst en betrouwbaar Thaise tekens kunt extraheren. Aan het einde kun je **afbeelding naar tekst converteren**, **tekst uit PNG halen**, en zelfs **Thaise tekst herkennen** met slechts een paar regels code.

## Wat deze tutorial behandelt

* Het instellen van de Aspose OCR‑dependency in een Maven/Gradle‑project.  
* Het initialiseren van de `OcrEngine` en configureren voor de Thaise taal.  
* OCR uitvoeren op een PNG‑bestand en mogelijke fouten afhandelen.  
* Het resultaat naar de console printen en de output verifiëren.  

Ervaring met Aspose is niet vereist—alleen een basis‑Java‑IDE en een afbeeldingsbestand dat je wilt verwerken.

## Vereisten

* Java 8 of nieuwer geïnstalleerd (de bibliotheek werkt ook met Java 11+).  
* Een build‑tool – Maven of Gradle (we laten het Maven‑fragment zien).  
* Een Aspose OCR‑licentie (de gratis proefversie werkt voor testen, maar een licentie verwijdert evaluatielimieten).  
* Een PNG die Thaise tekst bevat, bijvoorbeeld `input.png` geplaatst in de resources‑map van je project.

---

## Stap 1: Voeg Aspose OCR toe aan je project

### Maven

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- Use the latest version -->
</dependency>
```

### Gradle (Kotlin DSL)

```kotlin
implementation("com.aspose:aspose-ocr:23.9")
```

> **Pro tip:** Houd de bibliotheekversie synchroon met de officiële Aspose‑release‑notes; nieuwere versies voegen taalpakketten en prestatie‑verbeteringen toe.

Zodra de dependency is opgehaald, zou je IDE de benodigde klassen automatisch moeten importeren.

## Stap 2: Initialise­er de OCR‑engine

De engine is het hart van het proces – beschouw het als het “brein” dat pixelpatronen analyseert. We vertellen het ook dat we alleen Thaise tekens nodig hebben.

```java
import com.aspose.ocr.*;

public class ThaiOcrDemo {
    public static void main(String[] args) throws Exception {
        // Step 2: Create the OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Tell the engine to look for Thai language patterns
        ocrEngine.getRecognitionSettings().setLanguage("th");
```

Waarom de taal expliciet instellen? Omdat het specificeren van `"th"` de tekenset beperkt, waardoor de herkenning sneller gaat en mis­interpretaties van gelijk uitziende glyphs worden verminderd.

## Stap 3: Voer OCR uit op het PNG‑bestand

Nu geven we de engine de afbeelding die we willen decoderen. De methode `recognizeImage` retourneert een `OcrResult`‑object dat de geëxtraheerde string en vertrouwensscores bevat.

```java
        // Step 3: Perform OCR on the target image
        String imagePath = "src/main/resources/input.png";
        OcrResult ocrResult = ocrEngine.recognizeImage(imagePath);
```

Als het bestand niet gevonden kan worden, gooit Aspose een `FileNotFoundException`. Het is een goed idee om de oproep in een `try‑catch`‑blok te wikkelen voor productcode, maar voor deze tutorial houden we het simpel.

## Stap 4: Output van de herkende tekst

Tot slot printen we het resultaat. De methode `getText()` retourneert een gewone Java `String` die je kunt opslaan, over een netwerk kunt sturen of naar een bestand kunt schrijven.

```java
        // Step 4: Display the extracted Thai text
        System.out.println("=== Recognized Thai Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

Wanneer je het programma uitvoert, zou je iets moeten zien als:

```
=== Recognized Thai Text ===
สวัสดีครับ นี่คือข้อความจากรูปภาพ
```

Als de output er onleesbaar uitziet, controleer dan of de bron‑PNG een hoge resolutie heeft (minstens 300 dpi) en of de taalcode `"th"` overeenkomt met je doeltaal.

### Volledige listing

Hieronder staat het complete, kant‑klaar Java‑bestand. Kopieer‑en‑plak het in je IDE, vervang het afbeeldingspad indien nodig, en klik op **Run**.

```java
import com.aspose.ocr.*;

public class ThaiOcrDemo {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Select Thai language for recognition
        ocrEngine.getRecognitionSettings().setLanguage("th");

        // Run OCR on the PNG image
        String imagePath = "src/main/resources/input.png";
        OcrResult ocrResult = ocrEngine.recognizeImage(imagePath);

        // Output the recognized text
        System.out.println("=== Recognized Thai Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

![run OCR on image example](image.png "run OCR on image example – Java code extracting Thai text from PNG")

## Stap 5: Veelvoorkomende variaties & randgevallen

### Afbeelding naar tekst converteren in andere formaten

Als je **afbeelding naar tekst** wilt **converteren** voor een JPEG of BMP, wijzig dan simpelweg de bestandsextensie in `imagePath`. Aspose OCR ondersteunt PNG, JPEG, BMP, TIFF en zelfs PDF‑pagina’s.

### Tekst uit PNG halen met meerdere talen

Je kunt de engine vragen om meerdere talen tegelijk te detecteren:

```java
ocrEngine.getRecognitionSettings().setLanguage("th,en");
```

Het resultaat zal een mix van Thaise en Engelse tekens bevatten, wat handig is voor tweetalige bonnen.

### Omgaan met afbeeldingen van lage kwaliteit

Voor wazige scans kun je overwegen preprocessing in te schakelen:

```java
ocrEngine.getRecognitionSettings().setPreprocessMode(PreprocessMode.Auto);
```

Dit activeert ingebouwde ruis‑vermindering en contrast‑verbeteringsalgoritmen, waardoor de stap **tekst uit PNG halen** wordt verbeterd.

### Licentie‑activatie

Zonder licentie voegt Aspose een watermerkregel toe aan de output na 100 pagina’s. Activeer je licentie vroegtijdig:

```java
License license = new License();
license.setLicense("Aspose.OCR.lic");
```

Plaats het `.lic`‑bestand naast je JAR of verwijs ernaar via een absoluut pad.

## Veelgestelde vragen

**V: Werkt dit op Linux?**  
A: Absoluut. Aspose OCR is pure Java, dus elk JVM‑compatibel OS is geschikt.

**V: Wat als de PNG handgeschreven Thais bevat?**  
A: Handgeschreven herkenning is beperkt; je hebt mogelijk een dedicated neurale‑netwerk‑model nodig. Aspose OCR blinkt uit bij gedrukte tekst.

**V: Kan ik een map met afbeeldingen batch‑verwerken?**  
A: Wikkel de `recognizeImage`‑aanroep in een lus over `Files.list(Paths.get("folder"))`. Hergebruik dezelfde `OcrEngine`‑instantie voor betere prestaties.

## Conclusie

We hebben een compleet, end‑to‑end voorbeeld doorlopen van hoe je **OCR op afbeelding**‑bestanden in Java kunt uitvoeren, specifiek om **Thaise tekst** uit een PNG te **extraheren**. Door de `OcrEngine` te initialiseren, de taal in te stellen, `recognizeImage` aan te roepen en het resultaat te printen, heb je nu een betrouwbare manier om **afbeelding naar tekst te converteren** zonder derden‑services.

Vanaf hier kun je:

* **tekst uit PNG**‑bestanden in bulk halen voor data‑mining projecten.  
* De OCR‑output combineren met een vertaal‑API om Engelse equivalenten te krijgen.  
* Andere talen verkennen die door Aspose worden ondersteund, zoals Chinees of Arabisch, door de taalcode te wijzigen.

Probeer het met je eigen afbeeldingen—pas de preprocessing‑instellingen aan, experimenteer met verschillende bestandsformaten, en zie hoe robuust de oplossing aanvoelt in je real‑world workflow.

Happy coding, en moge je OCR‑pijplijnen altijd accuraat zijn!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}