---
category: general
date: 2026-10-30
description: Leer hoe je snel tekst uit een afbeelding kunt extraheren met Aspose
  OCR GPU-ondersteuning in Java. Deze gids laat zien hoe je de GPU device ID instelt
  en hoge-prestaties OCR bereikt.
draft: false
keywords:
- extract text from image
- how to extract text
- aspose ocr gpu
- recognize text image java
- gpu acceleration OCR
lastmod: 2026-10-30
og_description: Leer hoe je snel tekst uit een afbeelding kunt extraheren met Aspose
  OCR GPU-ondersteuning in Java. Deze gids laat zien hoe je de GPU device ID instelt
  voor optimale prestaties.
og_image_alt: 'Developer guide: extract text from image using Aspose OCR GPU in Java'
og_title: Hoe tekst uit een afbeelding te extraheren met Aspose OCR GPU in Java
schemas:
- author: Aspose
  dateModified: '2026-10-30'
  description: Learn how to extract text from image quickly with Aspose OCR GPU support
    in Java. This guide shows how to set GPU device ID and achieve high‑performance
    OCR.
  headline: How to extract text from image with Aspose OCR GPU in Java
  type: TechArticle
- questions:
  - answer: Yes—just install a valid Aspose OCR license. The free trial is for evaluation
      only.
    question: Can I use this in a commercial application?
  - answer: Absolutely; as long as the NVIDIA driver and CUDA toolkit are installed,
      the library runs on headless Linux environments.
    question: Does the GPU version work on Linux servers?
  - answer: Aspose OCR can process images up to **5000 × 5000 px** without loading
      the whole file into memory.
    question: What is the maximum image size supported?
  - answer: Replace the old JAR with the new one and update your Maven/Gradle dependency
      version number.
    question: How do I upgrade to the latest Aspose OCR version?
  - answer: Yes—`OcrResult` provides layout information, including word‑level bounding
      boxes, when you enable the `setIncludeLayout(true)` option.
    question: Is there a way to get bounding‑box coordinates for each word?
  type: FAQPage
tags:
- Java
- OCR
- Aspose
- GPU
title: Hoe tekst uit een afbeelding te extraheren met Aspose OCR GPU in Java
url: /nl/java/advanced-ocr-techniques/recognize-text-image-using-aspose-ocr-gpu-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe tekst uit afbeelding te extraheren met Aspose OCR GPU in Java

Als je ooit hebt geprobeerd om **extract text from image** in een Java‑applicatie en je CPU worstelde met scans met hoge resolutie, ben je niet de enige. Veel ontwikkelaars lopen tegen prestatieknelpunten aan bij het verwerken van grote documenten. Aspose OCR voor Java verwijdert die hindernis door OCR op de GPU uit te voeren, waardoor de verwerkingstijd drastisch wordt verkort. In deze tutorial zie je een compleet, kant‑klaar voorbeeld dat laat zien hoe je de licentie instelt, GPU‑versnelling inschakelt en **set gpu device id** instelt wanneer er meerdere grafische kaarten aanwezig zijn.

## Snelle antwoorden
- **What is the fastest way to extract text from image in Java?** Gebruik Aspose OCR met GPU‑versnelling en stel de juiste GPU‑apparaat‑ID in.  
- **Which Java version is required?** Java 17 of nieuwer wordt aanbevolen voor de beste prestaties.  
- **Do I need a license for GPU support?** Ja—GPU‑functies worden alleen ontgrendeld met een geldige Aspose OCR‑licentie.  
- **Can I run this on a headless server?** Absoluut; alleen de GPU‑driver en CUDA‑toolkit zijn vereist.  
- **How many languages are supported?** Meer dan 30 talen, waaronder Engels, Chinees, Arabisch en Hindi.

## Wat is extract text from image?
Het extraheren van tekst uit een afbeelding betekent het omzetten van de visuele weergave van tekens, opgeslagen in bitmap‑formaten zoals PNG, JPG of TIFF, naar bewerkbare, doorzoekbare Unicode‑tekst. Dit proces, bekend als Optical Character Recognition (OCR), maakt downstream‑taken mogelijk zoals indexeren, vertalen en gegevens‑extractie.

## Waarom Aspose OCR GPU gebruiken?
Aspose OCR maakt gebruik van GPU‑versnelling om grote, hoge‑resolutie‑afbeeldingen veel efficiënter te verwerken dan alleen met de CPU. Het ondersteunt meer dan 30 invoerformaten en kan afbeeldingen tot 5000 × 5000 px verwerken terwijl het geheugenverbruik laag blijft, en levert tot vijf keer snellere herkenning op moderne NVIDIA‑GPU’s.

## Wat je nodig hebt
- **Java 17** of nieuwer (compatibel met Java 8+, maar LTS‑releases geven betere JIT‑prestaties).  
- **Aspose OCR for Java** bibliotheek (download de JAR van de Aspose‑website).  
- Een geldig **Aspose OCR license file** (`Aspose.OCR.lic`). De gratis proefversie werkt, maar GPU‑functies vereisen een gelicentieerde versie.  
- Een afbeeldingsbestand (`sample-image.png`) dat duidelijke, machinaal leesbare tekst bevat.  
- Een CUDA‑compatibele NVIDIA‑GPU (of equivalent) met de juiste driver geïnstalleerd.

Als een van deze onbekend klinkt, maak je geen zorgen—elk punt wordt uitgelegd terwijl we verder gaan.

## Stap 1: voeg Aspose OCR toe aan je project
Eerst moet je de Aspose OCR JAR aan je classpath toevoegen. Als je Maven gebruikt, voeg dan de volgende dependency toe aan `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- replace with the latest version -->
</dependency>
```

Voor Gradle gebruik je:

```gradle
implementation 'com.aspose:aspose-ocr:23.12'
```

Als je de handmatige route verkiest, plaats de JAR in een `libs/`‑map en voeg deze toe aan het module‑pad van de IDE.

> **Pro tip:** Houd het versienummer afgestemd op de release‑notes; nieuwere versies bevatten vaak prestatie‑verbeteringen voor GPU‑verwerking.

## Stap 2: laad de Aspose OCR‑licentie (vereist voor GPU‑gebruik)
Zonder licentie valt de `setEnableGpu(true)`‑aanroep stilletjes terug naar CPU‑modus. Laad de licentie direct aan het begin van `main`:

```java
import com.aspose.ocr.License;

// ...

License ocrLicense = new License();
ocrLicense.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");
```

Vervang `YOUR_DIRECTORY` door het absolute of relatieve pad waar je het `.lic`‑bestand hebt opgeslagen. Een onjuist pad veroorzaakt een `FileNotFoundException`, controleer dus de spelling.

## Stap 3: maak de OCR‑engine en schakel GPU‑versnelling in
De `OcrEngine`‑klasse is de kerncomponent die OCR‑bewerkingen op afbeeldingen uitvoert.

```java
import com.aspose.ocr.OcrEngine;

// ...

OcrEngine ocrEngine = new OcrEngine();
ocrEngine.getDevice().setEnableGpu(true);       // activate GPU support
ocrEngine.getDevice().setGpuDeviceId(0);        // optional: choose GPU index (0 = first card)
```

Waarom de apparaat‑ID? In een multi‑GPU‑omgeving kun je één kaart toewijzen aan preprocessing en een andere aan OCR. Het instellen van de ID zorgt ervoor dat de zware taken op de beoogde hardware worden uitgevoerd.

## Stap 4: bereid de invoerafbeelding voor
De `OcrInput`‑klasse vertegenwoordigt de verzameling afbeeldingen die je wilt verwerken.

```java
import com.aspose.ocr.OcrInput;

// ...

OcrInput ocrInput = new OcrInput();
ocrInput.add("YOUR_DIRECTORY/sample-image.png"); // path to the image you want to process
```

Als je een stream moet verwerken (bijv. een geüpload bestand), gebruik dan `ocrInput.add(InputStream)`.

## Stap 5: voer het herkenningsproces uit en haal het resultaat op
De `OcrResult`‑klasse bevat de platte tekst, vertrouwensscores en optionele lay‑out‑informatie die door de engine worden geretourneerd.

```java
import com.aspose.ocr.OcrResult;

// ...

OcrResult ocrResult = ocrEngine.recognize(ocrInput);
System.out.println("Recognized text:\n" + ocrResult.getText());
```

De console zal iets tonen als:

```
Recognized text:
Hello, world!
This is a sample image.
```

Als de afbeelding onscherp is of de taal niet wordt ondersteund, kan het resultaat leeg zijn. Controleer in dat geval de waarde van `ocrResult.getConfidence()` (0‑100) om te beslissen of je opnieuw moet proberen met preprocessing.

## Volledig, uitvoerbaar voorbeeld
Alle onderdelen samenvoegen levert een enkele Java‑klasse op die je kunt kopiëren‑plakken in je IDE:

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

> **Verwachte output:** De console print de exacte tekst die in `sample-image.png` verschijnt. Wanneer de GPU actief is, daalt de verwerkingstijd meestal van enkele seconden (CPU) tot minder dan één seconde voor een typische 300 dpi‑scan.

## Veelgestelde vragen & randgevallen

### Werkt dit op een headless server?
Ja. De GPU‑driver moet geïnstalleerd zijn, maar er is geen display vereist. Zorg ervoor dat de `CUDA`‑toolkit (of equivalent voor je GPU) beschikbaar is in het systeem‑`PATH`. Deze configuratie maakt het mogelijk OCR uit te voeren in cloud‑gebaseerde of gecontaineriseerde omgevingen zonder grafische interface.

### Wat als ik meer dan één GPU heb en GPU 1 wil gebruiken?
Verander de apparaat‑ID zoals getoond:

```java
ocrEngine.getDevice().setGpuDeviceId(1); // selects the second GPU (zero‑based index)
```

Het instellen van de ID op `1` laat de OCR‑engine de tweede GPU in het systeem gebruiken, wat nuttig kan zijn wanneer de eerste GPU gereserveerd is voor andere taken.

### Hoe tekst uit afbeelding te extraheren in een andere taal?
Stel de taal in voordat je `recognize` aanroept:

```java
ocrEngine.setLanguage(OcrLanguage.FRENCH);
```

Aspose OCR ondersteunt **meer dan 30 talen**, waaronder rechts‑naar‑links‑scripts zoals Arabisch en Hebreeuws. Het kiezen van de juiste taal verbetert de nauwkeurigheid aanzienlijk.

### Wat als de afbeelding meerdere pagina’s bevat (bijv. een PDF omgezet naar afbeeldingen)?
Maak een aparte `OcrInput`‑entry voor elke pagina, of loop over de bestanden:

```java
for (String path : imagePaths) {
    ocrInput.add(path);
}
```

De engine plakt de resultaten in volgorde aan elkaar, waardoor de paginavolgorde in de uiteindelijke output behouden blijft.

### Hoe om te gaan met resultaten met lage vertrouwensscore?
Controleer de vertrouwensscore:

```java
if (ocrResult.getConfidence() < 70) {
    System.out.println("Low confidence – consider preprocessing the image.");
}
```

Typische preprocessing‑stappen omvatten binarisatie, ruisreductie of schalen naar 300 dpi. Het opnieuw uitvoeren van OCR na dergelijke preprocessing verhoogt vaak de vertrouwensniveaus.

## Prestatietips
- **Batch processing:** Het toevoegen van veel afbeeldingen aan één `OcrInput` vermindert de overhead van het herhaaldelijk initialiseren van de GPU‑context.  
- **Warm‑up:** Voer één dummy‑herkenning uit na het starten van de JVM; de eerste aanroep veroorzaakt latentie door driver‑initialisatie.  
- **Memory management:** Verwijder grote `OcrInput`‑objecten (`ocrInput.clear()`) nadat je klaar bent om GPU‑geheugen vrij te maken.  

## Conclusie
Je weet nu hoe je **extract text from image** efficiënt kunt uitvoeren met de GPU‑engine van Aspose OCR in Java, hoe je **set gpu device id** instelt bij het werken met meerdere grafische kaarten, en hoe je meertalige scenario’s aanpakt. De volledige, uitvoerbare code hierboven zou direct moeten werken—vervang alleen je licentie‑ en afbeeldingspaden.

Klaar voor de volgende stap? Probeer een volledige map met gescande PDF’s te verwerken, experimenteer met verschillende `setLanguage`‑opties, of combineer OCR‑output met een machine‑learning‑model voor post‑processing. De prestatie‑winst door GPU‑versnelling maakt grootschalige projecten haalbaar.

Veel plezier met coderen, en voel je vrij een reactie achter te laten als je problemen tegenkomt!

## Veelgestelde vragen

**Q: Kan ik dit gebruiken in een commerciële applicatie?**  
A: Ja—installeer gewoon een geldige Aspose OCR‑licentie. De gratis proefversie is alleen voor evaluatie.

**Q: Werkt de GPU‑versie op Linux‑servers?**  
A: Absoluut; zolang de NVIDIA‑driver en CUDA‑toolkit geïnstalleerd zijn, draait de bibliotheek op headless Linux‑omgevingen.

**Q: Wat is de maximale ondersteunde afbeeldingsgrootte?**  
A: Aspose OCR kan afbeeldingen verwerken tot **5000 × 5000 px** zonder het volledige bestand in het geheugen te laden.

**Q: Hoe upgrade ik naar de nieuwste Aspose OCR‑versie?**  
A: Vervang de oude JAR door de nieuwe en werk het versienummer van je Maven/Gradle‑dependency bij.

**Q: Is er een manier om de begrenzings‑boxcoördinaten voor elk woord te krijgen?**  
A: Ja—`OcrResult` biedt lay‑out‑informatie, inclusief woord‑niveau begrenzings‑boxen, wanneer je de optie `setIncludeLayout(true)` inschakelt.

---

**Laatst bijgewerkt:** 2026-10-30  
**Getest met:** Aspose OCR for Java 24.11  
**Auteur:** Aspose

## Gerelateerde tutorials

- [Herken tekst uit afbeelding Java OCR met GPU‑versnelling](/ocr/java/advanced-ocr-techniques/recognize-text-from-image-java-ocr-with-gpu-acceleration/)
- [Hoe GPU in te schakelen voor OCR in Java om tekst uit afbeelding te extraheren](/ocr/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-extract-text-from-image/)
- [Tekst uit afbeelding extraheren met Aspose OCR Java snelle gids](/ocr/java/ocr-basics/extract-text-from-image-with-aspose-ocr-java-quick-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}