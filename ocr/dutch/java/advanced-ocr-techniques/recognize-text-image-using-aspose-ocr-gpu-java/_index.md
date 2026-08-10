---
category: general
date: 2026-02-17
description: Herken tekst in afbeeldingen snel met Aspose OCR GPU-ondersteuning in
  Java. Leer tekst uit een afbeelding te extraheren en stel de GPU-apparaat‑ID in
  voor optimale prestaties.
draft: false
keywords:
- recognize text image
- extract text from image
- set gpu device id
- Aspose OCR Java
- GPU acceleration OCR
language: nl
og_description: Herken tekstafbeeldingen snel met Aspose OCR GPU-ondersteuning in
  Java. Deze gids laat zien hoe je tekst uit een afbeelding kunt extraheren en de
  GPU-apparaat‑ID kunt instellen.
og_title: herken tekstafbeelding met Aspose OCR GPU – Java
tags:
- Java
- OCR
- Aspose
- GPU
title: tekstafbeelding herkennen met Aspose OCR GPU – Java
url: /nl/java/advanced-ocr-techniques/recognize-text-image-using-aspose-ocr-gpu-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# tekstafbeelding herkennen met Aspose OCR GPU – Java

Heb je ooit **tekstafbeelding** moeten **herkennen** in een Java‑applicatie, maar hapte de CPU bij grote bestanden? Je bent niet de enige—veel ontwikkelaars lopen tegen die beperking aan bij het verwerken van scans met hoge resolutie. Het goede nieuws? Aspose OCR laat je **tekst uit afbeelding** halen op de GPU, waardoor de verwerkingstijd drastisch wordt verkort.  

In deze tutorial lopen we stap voor stap door een compleet, kant‑klaar voorbeeld dat laat zien hoe je de licentie instelt, GPU‑versnelling inschakelt en **gpu device id** instelt wanneer je meerdere grafische kaarten hebt. Aan het einde heb je een zelfstandig programma dat de herkende tekst naar de console schrijft—geen extra stappen nodig.

## Wat je nodig hebt

- **Java 17** of nieuwer (de API is compatibel met Java 8+, maar de nieuwste LTS biedt betere prestaties).  
- **Aspose OCR for Java**‑bibliotheek (download de JAR van de Aspose‑website).  
- Een geldig **Aspose OCR‑licentiebestand** (`Aspose.OCR.lic`). De gratis proefversie werkt, maar GPU‑functies zijn alleen beschikbaar in een gelicentieerde versie.  
- Een afbeeldingsbestand (`sample-image.png`) dat duidelijke, machinaal leesbare tekst bevat.  
- Een GPU‑geactiveerde omgeving (een NVIDIA‑CUDA‑compatibele kaart werkt het beste).  

Als een van deze punten je onbekend voorkomt, maak je geen zorgen—elke bullet wordt later uitgelegd.

## Stap 1: Voeg Aspose OCR toe aan je project

Plaats eerst de Aspose OCR‑JAR op je classpath. Als je Maven gebruikt, voeg dan de volgende dependency toe aan `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- replace with the latest version -->
</dependency>
```

Voor Gradle is het:

```gradle
implementation 'com.aspose:aspose-ocr:23.12'
```

Als je de handmatige route verkiest, zet je de JAR in je `libs/`‑map en voeg je deze toe aan het module‑pad van je IDE.

> **Pro tip:** Houd het versienummer synchroon met de release‑notes van de bibliotheek; nieuwere versies brengen vaak prestatie‑verbeteringen voor GPU‑verwerking.

## Stap 2: Laad de Aspose OCR‑licentie (vereist voor GPU‑gebruik)

Zonder licentie valt de aanroep `setEnableGpu(true)` stilletjes terug naar CPU‑modus. Laad de licentie direct aan het begin van `main`:

```java
import com.aspose.ocr.License;

// ...

License ocrLicense = new License();
ocrLicense.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");
```

Vervang `YOUR_DIRECTORY` door het absolute of relatieve pad waar je het `.lic`‑bestand hebt opgeslagen. Als het pad onjuist is, zal Aspose een `FileNotFoundException` gooien, controleer dus de spelling.

## Stap 3: Maak de OCR‑engine en schakel GPU‑versnelling in

Nu instantieren we `OcrEngine` en geven we aan dat deze de GPU moet gebruiken. Met de methode `setGpuDeviceId` kun je een specifieke kaart kiezen wanneer er meer dan één aanwezig is.

```java
import com.aspose.ocr.OcrEngine;

// ...

OcrEngine ocrEngine = new OcrEngine();
ocrEngine.getDevice().setEnableGpu(true);       // activate GPU support
ocrEngine.getDevice().setGpuDeviceId(0);        // optional: choose GPU index (0 = first card)
```

Waarom de device‑ID? Op een multi‑GPU‑server kun je één kaart reserveren voor beeld‑preprocessing en een andere voor OCR. Het instellen van de ID zorgt ervoor dat de juiste hardware het zware werk doet.

## Stap 4: Bereid de invoerafbeelding voor

Aspose OCR werkt met diverse formaten (PNG, JPG, BMP, TIFF). Verpak je bestand in een `OcrInput`‑object:

```java
import com.aspose.ocr.OcrInput;

// ...

OcrInput ocrInput = new OcrInput();
ocrInput.add("YOUR_DIRECTORY/sample-image.png"); // path to the image you want to process
```

Als je een stream moet verwerken (bijv. een geüpload bestand), gebruik dan `ocrInput.add(InputStream)` in plaats daarvan.

## Stap 5: Voer het herkenningsproces uit en haal het resultaat op

De methode `recognize` retourneert een `OcrResult` die de platte tekst, confidence‑scores en zelfs lay‑outinformatie bevat indien nodig.

```java
import com.aspose.ocr.OcrResult;

// ...

OcrResult ocrResult = ocrEngine.recognize(ocrInput);
System.out.println("Recognized text:\n" + ocrResult.getText());
```

De console toont iets als:

```
Recognized text:
Hello, world!
This is a sample image.
```

Als de afbeelding onscherp is of de taal niet wordt ondersteund, kan het resultaat leeg zijn. Controleer in dat geval de waarde van `ocrResult.getConfidence()` (0‑100) om te bepalen of je opnieuw moet proberen met preprocessing.

## Volledig, uitvoerbaar voorbeeld

Alle onderdelen samengevoegd krijg je een enkele Java‑klasse die je kunt copy‑pasten in je IDE:

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load license – required for GPU usage
        License ocrLicense = new License();
        ocrLicense.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");

        // 2️⃣ Create OCR engine and turn on GPU
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getDevice().setEnableGpu(true);      // enable GPU acceleration
        ocrEngine.getDevice().setGpuDeviceId(0);       // optional: select GPU index

        // 3️⃣ Load the image you want to process
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/sample-image.png");

        // 4️⃣ Perform recognition
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);

        // 5️⃣ Output the recognized text
        System.out.println("Recognized text:\n" + ocrResult.getText());
    }
}
```

> **Verwachte output:** De console print de exacte tekst die in `sample-image.png` staat. Als de GPU actief is, zie je de verwerkingstijd dalen van enkele seconden (CPU) naar minder dan een seconde voor typische 300 dpi‑scans.

## Veelgestelde vragen & randgevallen

### Werkt dit op een headless server?

Ja. Het GPU‑stuurprogramma moet geïnstalleerd zijn, maar er is geen display nodig. Zorg er alleen voor dat de `CUDA`‑toolkit (of het equivalent voor jouw GPU) in de systeem‑`PATH` staat.

### Wat als ik meer dan één GPU heb en GPU 1 wil gebruiken?

Wijzig de device‑ID:

```java
ocrEngine.getDevice().setGpuDeviceId(1); // selects the second GPU (zero‑based index)
```

### Hoe haal ik tekst uit een afbeelding in een andere taal?

Stel de taal in vóór het aanroepen van `recognize`:

```java
ocrEngine.setLanguage(OcrLanguage.FRENCH);
```

Aspose ondersteunt meer dan 30 talen; zie de API‑documentatie voor de volledige enumeratie.

### Wat als de afbeelding meerdere pagina’s bevat (bijv. een PDF omgezet naar afbeeldingen)?

Maak een aparte `OcrInput`‑entry voor elke pagina, of loop over de bestanden:

```java
for (String path : imagePaths) {
    ocrInput.add(path);
}
```

De engine concateneert de resultaten in volgorde.

### Hoe ga ik om met resultaten met lage confidence?

Controleer de confidence‑score:

```java
if (ocrResult.getConfidence() < 70) {
    System.out.println("Low confidence – consider preprocessing the image.");
}
```

Typische preprocessing‑stappen zijn binarisatie, ruisreductie of het schalen naar 300 dpi.

## Prestatie‑tips

- **Batchverwerking:** Veel afbeeldingen toevoegen aan één `OcrInput` vermindert de overhead van herhaaldelijk initialiseren van de GPU‑context.  
- **Warm‑up:** Voer één dummy‑herkenning uit direct na het starten van de JVM; de eerste oproep brengt driver‑initialisatie‑latentie met zich mee.  
- **Geheugenbeheer:** Maak grote `OcrInput`‑objecten leeg (`ocrInput.clear()`) nadat je klaar bent om GPU‑geheugen vrij te geven.  

## Conclusie

Je weet nu hoe je **tekstafbeelding** efficiënt kunt **herkennen** met de GPU‑engine van Aspose OCR in Java, hoe je **tekst uit afbeelding** kunt **extraheren** in elke ondersteunde taal, en hoe je **gpu device id** kunt **instellen** bij meerdere grafische kaarten. De volledige, uitvoerbare code hierboven zou direct moeten werken—vervang alleen je licentie‑ en afbeeldingspaden.

Klaar voor de volgende stap? Probeer een map met gescande PDF‑bestanden te verwerken, experimenteer met verschillende `setLanguage`‑opties, of combineer OCR met een machine‑learning‑model voor post‑processing. De mogelijkheden zijn eindeloos, en de prestatie‑winsten van GPU‑versnelling maken zelfs grootschalige projecten haalbaar.

Happy coding, en laat gerust een reactie achter als je ergens vastloopt!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}