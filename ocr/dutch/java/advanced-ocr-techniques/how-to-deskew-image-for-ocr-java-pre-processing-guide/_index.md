---
category: general
date: 2026-03-18
description: Hoe je een afbeelding snel kunt rechtzetten met Aspose OCR Java. Leer
  de afbeelding voor OCR voor te bewerken, de gescande afbeelding te reinigen en de
  OCR‑nauwkeurigheid te verbeteren in slechts een paar stappen.
draft: false
keywords:
- how to deskew image
- preprocess image for ocr
- extract text from image
- clean scanned image
- improve ocr accuracy
language: nl
og_description: Hoe een afbeelding rechtzetten met Aspose OCR Java, afbeelding voorbewerken
  voor OCR, gescande afbeelding opschonen en OCR-nauwkeurigheid verbeteren.
og_title: Hoe een afbeelding te deskewen voor OCR – Java-gids
tags:
- OCR
- Java
- Image Processing
title: Hoe een afbeelding te deskewen voor OCR – Java-preprocessinggids
url: /nl/java/advanced-ocr-techniques/how-to-deskew-image-for-ocr-java-pre-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe een afbeelding rechtzetten voor OCR – Java Pre‑Processing Gids

Heb je je ooit afgevraagd **hoe je een afbeelding** die scheef van een scanner komt, recht kunt zetten? Je bent niet de enige—veel ontwikkelaars lopen tegen dit probleem aan wanneer ze tekst uit beeld‑zware documenten willen halen. Het goede nieuws? Met een paar regels Java en Aspose OCR kun je de afbeelding rechtzetten, ruis verwijderen en schone tekst extraheren zonder al te veel gedoe.

In deze tutorial lopen we het volledige workflow door: een ruisende, gedraaide scan laden, een deskew‑filter toepassen, visuele rommel verwijderen en uiteindelijk **tekst uit afbeelding** extraheren. Aan het einde weet je hoe je **afbeelding preprocessen voor OCR**, **gescande afbeeldingen reinigen** en **OCR‑nauwkeurigheid verbeteren** voor elk project dat betrouwbare teksterkenning vereist.

## Wat je nodig hebt

- Java 17 (of een recente JDK) – de code maakt gebruik van de standaardtaalfeatures.
- Aspose OCR voor Java bibliotheek (de gratis trial werkt prima voor experimenten).
- Een voorbeeldafbeelding die zowel ruisig als gedraaid is (bijv. `noisy-rotated.png`).
- Je favoriete IDE (IntelliJ IDEA, Eclipse, VS Code…) – alles wat Java kan compileren.

Geen extra frameworks, geen Maven/Gradle toverij nodig; de enige import‑statements zijn die hieronder getoond worden.

---

## Hoe een afbeelding rechtzetten met Aspose OCR

Het eerste dat we moeten aanpakken is de kanteling van de afbeelding. Als de tekstregels niet horizontaal zijn, zal de OCR‑engine tekens verkeerd lezen. De `DeskewFilter` doet het zware werk.

```java
import com.aspose.ocr.OcrEngine;
import com.aspose.ocr.Image;
import com.aspose.ocr.preprocess.DeskewFilter;
import com.aspose.ocr.preprocess.DenoiseFilter;

public class PreprocessDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the raw scanned image
        Image scannedImage = Image.load("YOUR_DIRECTORY/noisy-rotated.png");

        // Step 3: Correct the image orientation (deskew)
        DeskewFilter deskewFilter = new DeskewFilter();
        scannedImage = deskewFilter.apply(scannedImage);

        // Step 4: Reduce visual noise (denoise)
        DenoiseFilter denoiseFilter = new DenoiseFilter();
        scannedImage = denoiseFilter.apply(scannedImage);

        // Step 5: Perform OCR on the cleaned image
        String recognizedText = ocrEngine.recognize(scannedImage);

        // Step 6: Output the extracted text
        System.out.println(recognizedText);
    }
}
```

> **Waarom dit belangrijk is:** De `DeskewFilter` analyseert de geometrie van de afbeelding, schat de rotatiehoek en draait de bitmap terug naar een horizontaal niveau. Zonder deze stap behandelen de meeste OCR‑engines scheve letters als volledig andere glyphs, waardoor je **OCR‑nauwkeurigheid verbeteren** inspanningen ten onder gaan.

> **Pro tip:** Als je te maken hebt met documenten die mogelijk ondersteboven staan, schakel dan de `setAutoRotate`‑vlag in op de `DeskewFilter` (beschikbaar in nieuwere Aspose‑releases). Deze draait automatisch 180° wanneer nodig.

![Diagram dat vóór‑ en na‑rotatie toont – hoe een afbeelding rechtzetten](https://example.com/deskew-diagram.png "voorbeeld van hoe een afbeelding rechtzetten")

*Afbeeldings‑alt‑tekst: voorbeeld van hoe een afbeelding rechtzetten*

---

## Afbeelding preprocessen voor OCR – Ruisonderdrukking en Reiniging

Zodra de afbeelding recht staat, is de volgende hindernis visuele ruis—die stippen, compressie‑artefacten of vage achtergrondpatronen die de OCR‑engine verwarren. De `DenoiseFilter` past een subtiel gladstrijkingsalgoritme toe dat randen (de letters) behoudt terwijl het korrel verwijdert.

```java
// Step 4 (continued): Reduce visual noise (denoise)
DenoiseFilter denoiseFilter = new DenoiseFilter();
scannedImage = denoiseFilter.apply(scannedImage);
```

### Wanneer de Denoising‑instellingen aanpassen

- **Zeer donkere scans:** Verhoog de sterkte van het filter (`denoiseFilter.setStrength(2)`) om achtergrondschaduwen weg te halen.
- **Fijne lettertypen:** Verlaag de sterkte om te voorkomen dat kleine schreefjes vervagen.
- **Gekleurde documenten:** Converteer eerst naar grijstinten (`scannedImage = scannedImage.toGrayscale();`)—de OCR‑engine werkt het beste op enkel‑kanaal afbeeldingen.

Deze aanpassingen maken deel uit van **gescande afbeeldingen reinigen** best practices; een schonere bitmap vertaalt zich direct naar hogere vertrouwensscores van de OCR‑engine.

---

## Tekst uit afbeelding extraheren – De OCR‑engine draaien

Nu de afbeelding recht en stil is, is het tijd om **tekst uit afbeelding** te **extraheren**. De `OcrEngine`‑klasse regelt alles achter de schermen: segmentatie, karakterclassificatie en taalmodellering.

```java
// Step 5: Perform OCR on the cleaned image
String recognizedText = ocrEngine.recognize(scannedImage);
System.out.println(recognizedText);
```

#### Verwachte output

Bevat je bronbestand de regel “**Invoice # 12345**”, dan zou de console iets dergelijks moeten afdrukken:

```
Invoice # 12345
Date: 2026-03-18
Total: $1,250.00
```

Als de output er rommelig uitziet, controleer dan de vorige stappen—vooral het rechtzetten. Zelfs een kanteling van 1 graad kan cijfers en symbolen corrumperen.

---

## Veelvoorkomende valkuilen & Tips om **OCR‑nauwkeurigheid te verbeteren**

| Probleem | Waarom het de nauwkeurigheid schaadt | Snelle oplossing |
|----------|--------------------------------------|------------------|
| **Resterende rotatie** | OCR verwacht horizontale basislijnen. | Controleer met `deskewFilter.getAngle()` en log de waarde. |
| **Over‑denoising** | Vervaagt dunne streken, waardoor “i” verandert in “l”. | Gebruik `setStrength(0.5)` voor delicate lettertypen. |
| **Verkeerd afbeeldingsformaat** | JPEG‑compressie voegt artefacten toe. | Geef de voorkeur aan PNG of TIFF voor verliesvrije opslag. |
| **Onjuiste taal** | Engine gaat standaard uit van Engels; andere alfabetten vereisen expliciete instelling. | `ocrEngine.setLanguage(OcrEngine.Language.Spanish);` |
| **Lage DPI (≤150)** | Niet genoeg pixeldata voor betrouwbare segmentatie. | Resample naar 300 DPI vóór verwerking (`scannedImage = scannedImage.resample(300);`). |

### Bonus: Batchverwerking

Heb je een map met scans, wikkel dan de demo in een lus:

```java
File folder = new File("YOUR_DIRECTORY");
for (File file : folder.listFiles((dir, name) -> name.endsWith(".png"))) {
    Image img = Image.load(file.getAbsolutePath());
    img = new DeskewFilter().apply(img);
    img = new DenoiseFilter().apply(img);
    String text = ocrEngine.recognize(img);
    System.out.println("=== " + file.getName() + " ===");
    System.out.println(text);
}
```

Dit patroon laat je **afbeelding preprocessen voor OCR** op schaal, houdt de codebase overzichtelijk en de prestaties voorspelbaar.

---

## Samenvatting & Volgende stappen

We hebben behandeld **hoe je een afbeelding** rechtzet, **afbeelding preprocessen voor OCR**, en tenslotte **tekst uit afbeelding** extraheren met Aspose OCR Java. Door de scan recht te zetten, de ruis te verwijderen en een onberispelijke bitmap aan de engine te voeren, verbeter je merkbaar de **OCR‑nauwkeurigheid**.

Wat nu? Overweeg deze uitbreidingen:

- **Taaldetectie** – schakel `ocrEngine.setLanguage` op basis van gedetecteerd schrift.
- **PDF‑output** – voer de herkende tekst in een PDF‑generator voor doorzoekbare documenten.
- **Machine‑learning post‑processing** – voer spell‑check of aangepaste woordenboeken uit op het OCR‑resultaat.

Probeer die ideeën, experimenteer met verschillende filtersterktes, en je hebt al snel een robuuste pijplijn voor elk document‑digitaliseringsproject.

---

*Happy coding! Als je een probleem tegenkomt, laat dan een reactie achter—ik help je graag de deskew‑ en denoise‑parameters af te stemmen.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}