---
category: general
date: 2026-02-19
description: Leer hoe je een afbeelding kunt rechtzetten en ruis kunt verwijderen
  voor OCR. Deze tutorial laat zien hoe je tekstafbeeldingen kunt herkennen, de rotatie
  van de afbeelding kunt corrigeren en OCR-beeldvoorverwerking kunt uitvoeren met
  Aspose OCR.
draft: false
keywords:
- how to deskew image
- recognize text image
- how to remove noise
- correct image rotation
- preprocess image ocr
language: nl
og_description: Hoe je een afbeelding kunt rechtzetten en ruis kunt verwijderen zodat
  je snel tekst in de afbeelding kunt herkennen. Volg deze gids om de rotatie van
  de afbeelding te corrigeren en de OCR van de afbeelding voor te verwerken met Aspose.
og_title: Hoe een afbeelding rechtzetten – Complete OCR‑voorverwerkingstutorial
tags:
- OCR
- Java
- Image Processing
title: Hoe een afbeelding rechtzetten — Stapsgewijze OCR‑voorverwerkingsgids
url: /nl/java/ocr-operations/how-to-deskew-image-step-by-step-ocr-pre-processing-guide/
---

text:" to "Alt‑tekst:". Keep the phrase "how to deskew image". So: "*Alt‑tekst: how to deskew image – before and after processing.*"

Similarly headings etc.

Now produce final content.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe een afbeelding rechtzetten — Complete OCR‑pre‑processing‑tutorial

Heb je je ooit afgevraagd **hoe je een afbeelding moet rechtzetten** voordat je deze aan een OCR‑engine geeft? Misschien heb je een stapel bonnetjes gescand en lijken de pagina’s een beetje te leunen, of is de scan bezaaid met willekeurige stippen. Dat is een veelvoorkomend probleem—hellende, ruisende afbeeldingen laten teksterkenning haperen.  

Het goede nieuws? Je kunt de rotatie corrigeren (image rotation) en ruis verwijderen (how to remove noise) in slechts een paar regels Java met Aspose.OCR. In deze gids lopen we de volledige workflow door: van het laden van een ruis‑en‑geroteerde PNG, het toepassen van deskew + median denoise, tot **recognize text image** en het afdrukken van het resultaat. Aan het einde heb je een herbruikbare snippet die je in elk Java‑project kunt gebruiken.

## Wat je nodig hebt

- **Java 17** of nieuwer (de code compileert ook met oudere versies, maar 17 is de ideale keuze).  
- **Aspose.OCR for Java** – haal de nieuwste JAR op via Maven Central (`com.aspose:aspose-ocr`).  
- Een afbeeldingsbestand dat zowel geroteerd als ruisig is (bijv. `noisy-rotated.png`).  
- Een eenvoudige IDE (IntelliJ, Eclipse, of zelfs VS Code).  

Er zijn geen ingewikkelde build‑tools nodig; een simpele `javac` + `java`‑run werkt prima.

---

## Stap 1 – Maak een OCR‑engine‑instance  

Het eerste wat je doet, is een `OcrEngine` opstarten. Beschouw het als het brein dat later de tekens voor je zal lezen.

```java
import com.aspose.ocr.*;

public class PreprocessExample {
    public static void main(String[] args) throws Exception {

        // Initialize the OCR engine – this object holds all settings
        OcrEngine ocrEngine = new OcrEngine();
```

> **Pro tip:** Houd de engine als singleton als je veel afbeeldingen verwerkt; hij hergebruikt interne buffers en versnelt het proces.

## Stap 2 – Schakel Deskew en Median Denoise in (How to Remove Noise)

Nu vertellen we de engine om **image rotation** te corrigeren en **how to remove noise** toe te passen. Beide filters zijn optioneel, maar samen verbeteren ze de nauwkeurigheid drastisch.

```java
        // Turn on preprocessing filters
        ocrEngine.getPreprocessing().setDeskew(true);          // fixes rotation
        ocrEngine.getPreprocessing().setMedianDenoise(true);   // smooths out speckles
```

Waarom median denoise? Het behoudt randen (de lijnen die tekens definiëren) terwijl geïsoleerde pixels worden weggehaald—precies wat je nodig hebt voor schone OCR.

## Stap 3 – Laad de afbeelding die je wilt verwerken  

Hier wijzen we de engine op het bestand dat opgeschoond moet worden. `ImageStream.fromFile` leest de PNG in het geheugen.

```java
        // Load the noisy‑rotated image
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/noisy-rotated.png"));
```

Als je afbeelding zich op een externe server bevindt, geef dan een `InputStream` door—Aspose handelt dat moeiteloos af.

## Stap 4 – Voer OCR uit en vang de herkende tekst op  

Met preprocessing ingeschakeld leest de engine nu de gecorrigeerde afbeelding. De `recognize()`‑aanroep retourneert een `RecognitionResult` die de geëxtraheerde string bevat.

```java
        // Perform OCR – the engine automatically applies deskew & denoise first
        String recognizedText = ocrEngine.recognize().getText();

        // Show the output
        System.out.println("=== Recognized Text ===");
        System.out.println(recognizedText);
    }
}
```

Je zou schone, leesbare tekst in de console moeten zien, zelfs als de oorspronkelijke foto scheef en korrelig was.

## Stap 5 – Controleer het resultaat (What to Expect)

Als alles werkt, print de console iets als:

```
=== Recognized Text ===
Invoice #12345
Date: 2026‑02‑15
Total: $1,234.56
```

Als de output nog steeds onleesbare tekens bevat, controleer dan:

- De beeldresolutie (≥ 300 dpi is ideaal).  
- Of het bestandspad correct is.  
- Of extra filters (bijv. `setContrastStretch`) kunnen helpen.

---

## Optioneel: Visuele bevestiging met een voorbeeldafbeelding  

Hieronder zie je een klein voorbeeld van een geroteerde, ruisige bon. Merk de kanteling op—onze code zal deze voor je rechtzetten.

![how to deskew image example](deskew-demo.png "how to deskew image")

*Alt‑tekst: how to deskew image – before and after processing.*

---

## Veelgestelde vragen

### Werkt dit met PDF’s of alleen PNG/JPEG?  
Aspose.OCR kan PDF’s direct lezen; vervang gewoon `ImageStream.fromFile` door `ImageStream.fromPdf`. Dezelfde preprocessing‑vlaggen gelden, dus je krijgt nog steeds **how to deskew image** en **how to remove noise**.

### Wat als ik de oorspronkelijke oriëntatie later nog nodig heb?  
Je kunt de afbeelding clonen vóór preprocessing:

```java
Image original = ocrEngine.getImage().clone();
ocrEngine.getPreprocessing().apply(); // modifies the internal copy
// Use original later if needed
```

### Kan ik de deskew‑hoek handmatig instellen?  
Ja—`setDeskewAngle(double degrees)` laat je het auto‑detectie‑algoritme overschrijven. Handig wanneer auto‑detectie faalt bij extreme rotaties.

### Hoe verschilt median denoise van Gaussian blur?  
Median‑filters vervangen elke pixel door de mediaan van zijn buren, waardoor randen behouden blijven. Gaussian blur maakt alles glad, waardoor mogelijk karakterstreken vervagen—median is dus veiliger voor OCR.

---

## Afronding  

In deze tutorial hebben we **how to deskew image** behandeld, **how to remove noise** gedemonstreerd, en laten zien hoe je **recognize text image** gebruikt met de ingebouwde preprocessing van Aspose OCR. Door `setDeskew(true)` en `setMedianDenoise(true)` in te schakelen, corrigeer je automatisch **image rotation** en verwijder je stippen, waardoor een rommelige scan verandert in een schone tekststring.  

Voel je vrij om te experimenteren: probeer verschillende denoise‑strategieën, verwerk PDF’s, of koppel meerdere afbeeldingen in een lus. Hetzelfde patroon—engine → preprocess → recognize—geldt voor elk scenario, waardoor dit een solide basis vormt voor elke OCR‑pipeline.

**Volgende stappen** die je kunt verkennen:

- **Batchverwerking** – itereren over een map met afbeeldingen en elk resultaat naar een `.txt`‑bestand schrijven.  
- **Taalpakketten** – laad een specifiek taalwoordenboek om de nauwkeurigheid voor niet‑Engelse tekst te verhogen.  
- **Geavanceerde filters** – zoals `setContrastStretch` of `setBinarization` voor scans met weinig contrast.  

Heb je meer vragen? Laat een reactie achter, en happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}