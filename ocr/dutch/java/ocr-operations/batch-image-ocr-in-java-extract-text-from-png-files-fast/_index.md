---
category: general
date: 2026-02-14
description: 'Batchafbeelding‑OCR eenvoudig gemaakt: leer hoe je tekst uit PNG‑bestanden
  kunt extraheren met Aspose OCR en parallelle verwerking in Java.'
draft: false
keywords:
- batch image OCR
- extract text from png
- parallel OCR Java
- Aspose OCR async
- OCR batch processing
language: nl
og_description: Batch image OCR‑tutorial die laat zien hoe je tekst uit PNG‑bestanden
  kunt extraheren met de asynchrone API van Aspose OCR in Java.
og_title: Batchafbeeldingen OCR in Java – Snelle PNG-tekstextractie
tags:
- Java
- OCR
- Aspose
- Image Processing
title: Batchafbeeldingen OCR in Java – Haal snel tekst uit PNG‑bestanden
url: /nl/java/ocr-operations/batch-image-ocr-in-java-extract-text-from-png-files-fast/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Batch Image OCR in Java – Tekst uit PNG‑bestanden snel extraheren

Heb je ooit **batch image OCR** moeten uitvoeren op een map met PNG‑scans, maar maak je je zorgen over de snelheid? Je bent niet de enige. In veel real‑world projecten—factuurdigitalisering, archivering van gescande boeken, of het verwerken van bonnen—moeten ontwikkelaars **tekst uit PNG**‑afbeeldingen snel en betrouwbaar **extraheren**.  

Het goede nieuws? Met de asynchrone API van Aspose OCR kun je in slechts een paar regels Java een parallelle OCR‑pipeline opzetten. In deze gids lopen we stap voor stap door de volledige, uitvoerbare oplossing, leggen we uit waarom elk onderdeel belangrijk is, en laten we zien hoe je de resultaten kunt verifiëren. Aan het einde heb je een zelfstandige applicatie die een hele batch PNG‑bestanden parallel verwerkt, met schone, spell‑gecontroleerde tekst als output.

## Wat je zult leren

- Hoe je PNG‑bestanden kunt opsommen voor batchverwerking  
- Het configureren van de Aspose `OcrEngine` voor de Engelse taal en spell‑correctie  
- OCR asynchroon uitvoeren met `processAsync` en het `Future`‑resultaat afhandelen  
- Het lezen en weergeven van de herkende tekst voor elke afbeelding  
- Tips voor schalen, foutafhandeling en prestatie‑optimalisatie  

### Voorwaarden

- Java 8 of nieuwer geïnstalleerd (de code maakt gebruik van het standaard `java.util.concurrent`‑pakket)  
- Een Aspose OCR for Java‑licentie of een gratis proefversie (download van de Aspose‑website)  
- Een map met een paar PNG‑screenshots of gescande pagina’s die je wilt testen  

Nu, laten we beginnen.

## Stap 1 – Verzamel je PNG‑bestanden voor een batch

Voordat de OCR‑engine iets kan doen, moet hij weten welke afbeeldingen verwerkt moeten worden. De eenvoudigste manier is om een `List<String>` met absolute of relatieve bestands‑paden op te bouwen.

```java
// Step 1: Prepare a list of PNG files you want to run OCR on
List<String> imageFiles = Arrays.asList(
        "YOUR_DIRECTORY/page1.png",
        "YOUR_DIRECTORY/page2.png",
        "YOUR_DIRECTORY/page3.png",
        "YOUR_DIRECTORY/page4.png");
```

**Waarom dit belangrijk is:**  
Het vooraf maken van de lijst laat de engine elk bestand onafhankelijk inplannen, wat de basis vormt van echte batchverwerking. Als je later een map dynamisch wilt scannen, vervang je gewoon de statische `Arrays.asList` door een `Files.walk`‑stream.

## Stap 2 – Initialiseert en stem de Aspose OCR‑engine af

De `OcrEngine` van Aspose is zeer configureerbaar. Hier stellen we de taal in op Engels en schakelen we spell‑correctie in—twee opties die de kwaliteit van de geëxtraheerde tekst drastisch verbeteren, vooral bij ruisende PNG‑scans.

```java
// Step 2: Create and configure the OCR engine
OcrEngine ocrEngine = new OcrEngine();
ocrEngine.getEngineOptions()
         .setLanguage(OcrLanguage.ENGLISH)          // English language model
         .setSpellCorrectionEnabled(true);          // Enable spell‑checking
```

**Waarom deze instellingen:**  
- **Taalselectie** vertelt de engine welke tekenset en woordenboek gebruikt moeten worden, waardoor valse herkenningen afnemen.  
- **Spell‑correctie** vangt veelvoorkomende OCR‑fouten (bijv. “1” vs “l”) op zonder dat je de output later hoeft te verwerken.

> **Pro tip:** Als je afbeeldingen meerdere talen bevatten, kun je een lijst doorgeven zoals `setLanguage(OcrLanguage.ENGLISH, OcrLanguage.FRENCH)`.

## Stap 3 – Start asynchrone batchverwerking

Het zware werk gebeurt in `processAsync`. Deze methode retourneert een `Future<List<OcrResult>>`, waardoor je hoofdthread andere taken kan blijven uitvoeren terwijl de OCR op de achtergrond draait.

```java
// Step 3: Start asynchronous processing of the image batch
Future<List<OcrResult>> ocrFuture = ocrEngine.processAsync(imageFiles);

// (Optional) Do something useful while OCR runs, e.g., log progress, load UI, etc.
System.out.println("OCR started – you can perform other tasks now...");
```

**Waarom async:**  
OCR sequentieel uitvoeren kan extreem traag zijn—elke PNG kan een seconde of meer duren. Door het werk uit te besteden aan een thread‑pool benut je meerdere CPU‑kernen en verkort je de totale uitvoeringstijd aanzienlijk.

## Stap 4 – Haal de resultaten op wanneer ze klaar zijn

Wanneer je de output wilt gebruiken, roep je simpelweg `get()` aan op de `Future`. Deze oproep blokkeert alleen tot de OCR voltooid is, en levert vervolgens een lijst van `OcrResult`‑objecten in dezelfde volgorde als de invoerlijst.

```java
// Step 4: Wait for all results and retrieve them
List<OcrResult> ocrResults = ocrFuture.get(); // blocks until completion
```

**Time‑outs afhandelen:**  
Wil je een onbeperkte blokkering vermijden, gebruik dan `ocrFuture.get(60, TimeUnit.SECONDS)` en vang `TimeoutException` om een fallback te implementeren.

## Stap 5 – Toon de herkende tekst voor elke PNG

Nu je de resultaten hebt, kun je erover itereren en de geëxtraheerde tekst naast de oorspronkelijke bestandsnaam afdrukken. Dit is het moment waarop je eindelijk **tekst uit PNG**‑bestanden **extrahert**.

```java
// Step 5: Show the OCR output for each image
for (int i = 0; i < ocrResults.size(); i++) {
    System.out.println("File: " + imageFiles.get(i));
    System.out.println(ocrResults.get(i).getText());
    System.out.println("---");
}
```

**Voorbeeld van verwachte output**

```
File: YOUR_DIRECTORY/page1.png
Invoice #12345
Date: 2024‑03‑01
Total: $1,250.00
---
File: YOUR_DIRECTORY/page2.png
...
```

Als de OCR‑engine een pagina niet kan herkennen, zal de bijbehorende `getText()` een lege string teruggeven—dit is altijd het controleren waard in productcode.

## Volledig werkend voorbeeld

Hieronder staat het complete, kant‑klaar programma dat alle onderdelen samenvoegt. Kopieer‑en‑plak het in een bestand met de naam `ParallelOcrDemo.java`, vervang `YOUR_DIRECTORY` door het pad naar je PNG‑map, en voer `javac ParallelOcrDemo.java && java ParallelOcrDemo` uit.

```java
import com.aspose.ocr.*;
import java.util.*;
import java.util.concurrent.*;

public class ParallelOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Prepare a list of image files to be processed
        List<String> imageFiles = Arrays.asList(
                "YOUR_DIRECTORY/page1.png",
                "YOUR_DIRECTORY/page2.png",
                "YOUR_DIRECTORY/page3.png",
                "YOUR_DIRECTORY/page4.png");

        // Step 2: Create and configure the OCR engine (set language and enable spell‑checking)
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getEngineOptions()
                 .setLanguage(OcrLanguage.ENGLISH)
                 .setSpellCorrectionEnabled(true);

        // Step 3: Start asynchronous processing of the image batch
        Future<List<OcrResult>> ocrFuture = ocrEngine.processAsync(imageFiles);

        // (Optional) Perform other work here while OCR runs in the background...
        System.out.println("OCR processing started in background...");

        // Step 4: Wait for all results and retrieve them
        List<OcrResult> ocrResults = ocrFuture.get(); // blocks until completion

        // Step 5: Display the recognized text for each file
        for (int i = 0; i < ocrResults.size(); i++) {
            System.out.println("File: " + imageFiles.get(i));
            System.out.println(ocrResults.get(i).getText());
            System.out.println("---");
        }
    }
}
```

### Demo uitvoeren

1. **Compileren** – `javac -cp "aspose-ocr.jar" ParallelOcrDemo.java`  
2. **Uitvoeren** – `java -cp ".:aspose-ocr.jar" ParallelOcrDemo`  

Je zou elke PNG‑bestandsnaam moeten zien, gevolgd door de geëxtraheerde tekst, gescheiden door streepjes.  

> **Opmerking:** Als je een `LicenseException` tegenkomt, zorg er dan voor dat je je Aspose‑licentie laadt voordat je de engine aanmaakt:

```java
License lic = new License();
lic.setLicense("Aspose.OCR.Java.lic");
```

## Opschalen – Tips voor batch‑OCR in de praktijk

| Situatie | Aanbeveling |
|-----------|----------------|
| **Honderden PNG‑bestanden** | Verhoog de thread‑poolgrootte via `ocrEngine.setThreadPoolSize(8)` (of hoger, passend bij het aantal CPU‑kernen). |
| **Geheugenbeperkingen** | Verwerk bestanden in kleinere porties (bijv. batches van 50) en maak de `OcrResult`‑lijst na elke batch vrij. |
| **Variabele beeldkwaliteit** | Schakel `setPreprocessingOptions` in om automatisch te roteren, kantelen of het contrast te verbeteren vóór herkenning. |
| **Meerdere talen** | Roep `setLanguage(OcrLanguage.ENGLISH, OcrLanguage.SPANISH)` aan en stel eventueel een aangepast woordenboek in. |
| **Foutafhandeling** | Plaats `ocrFuture.get()` in een try‑catch‑blok voor `ExecutionException` om mislukte bestanden te loggen zonder de hele batch te onderbreken. |

Deze strategieën houden je **batch image OCR**‑pipeline robuust, zelfs wanneer de invoerset groeit.

## Veelgestelde vragen

**V: Werkt dit ook met JPEG‑ of TIFF‑bestanden?**  
A: Absoluut. De `processAsync`‑methode accepteert elk formaat dat door Aspose OCR wordt ondersteund (PNG, JPEG, TIFF, BMP, enz.). Pas gewoon de bestandsextensies in je lijst aan.

**V: Hoe kan ik de lay‑out behouden (tabellen, kolommen)?**  
A: Aspose OCR biedt een `getLayoutResult()`‑methode die positionele data teruggeeft. Je kunt tabellen reconstrueren door de begrenzings‑boxen van elk woord te analyseren.

**V: Kan ik dit op een serverless platform draaien?**  
A: Ja—pak simpelweg de JAR met de Aspose‑bibliotheek en zet die uit naar AWS Lambda, Azure Functions of Google Cloud Functions. Zorg ervoor dat je de geheugen‑toewijzing van de functie hoog genoeg zet voor de OCR‑thread‑pool.

## Conclusie

Je beschikt nu over een complete, zelfstandige **batch image OCR**‑oplossing die efficiënt **tekst uit PNG**‑bestanden extraheert met de asynchrone API van Aspose OCR in Java. De tutorial heeft alles behandeld, van het voorbereiden van de bestandslijst tot het configureren van taal en spell‑checking, het starten van parallelle verwerking, het afhandelen van resultaten, en het opschalen van de pipeline voor productie‑omgevingen.

Klaar voor de volgende stap? Probeer de taal te wijzigen naar Frans, experimenteer met aangepaste woordenboeken, of integreer de output in een doorzoekbare ElasticSearch‑index. De mogelijkheden zijn eindeloos wanneer je snelle batch‑OCR combineert met moderne Java‑concurrency.

Happy coding, en moge je tekst‑extractie snel en accuraat zijn! 

![Diagram showing parallel OCR workers handling multiple PNG files](/images/batch-ocr-diagram.png){: .center alt="Batch image OCR verwerkingsdiagram"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}