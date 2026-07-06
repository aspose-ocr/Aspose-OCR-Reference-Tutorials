---
category: general
date: 2026-04-29
description: tekst extraheren uit een afbeelding in Java met Aspose OCR – leer hoe
  je een afbeelding laadt voor OCR en tekst van een bon herkent in JSON‑formaat.
draft: false
keywords:
- extract text from image java
- load image for OCR
- recognize text from receipt
- Aspose OCR Java
- JSON OCR result
language: nl
og_description: tekst extraheren uit afbeelding met Java en Aspose OCR. Deze tutorial
  laat zien hoe je een afbeelding laadt voor OCR en tekst van een bon herkent, met
  JSON als output.
og_title: tekst uit afbeelding halen met Java – Complete gids
tags:
- Java
- OCR
- Aspose
title: tekst uit afbeelding extraheren java – afbeelding laden voor OCR
url: /nl/java/ocr-operations/extract-text-from-image-java-load-image-for-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# tekst uit afbeelding extraheren java – Complete gids

Heb je ooit **tekst uit afbeelding extraheren java** nodig gehad, maar wist je niet welke bibliotheek je moet kiezen? Je bent niet de enige. Veel ontwikkelaars lopen tegen een muur aan wanneer ze proberen een afbeelding te laden voor OCR en vervolgens de ruwe tekst terugkrijgen in een formaat dat moeilijk te verwerken is.  

In deze tutorial lopen we een schone, end‑to‑end oplossing door die niet alleen **load image for OCR** doet, maar ook **recognize text from receipt** en een nette JSON‑string oplevert. Aan het einde heb je een kant‑klaar Java‑klasse die je in elk project kunt plaatsen—zonder extra gedoe.

## Wat je zult leren

- Hoe je Aspose OCR voor Java instelt (de bibliotheek die het zware werk moeiteloos maakt).  
- De exacte stappen om **load image for OCR** van schijf te laden.  
- Hoe je de engine configureert om resultaten in JSON terug te geven, wat perfect is voor downstream verwerking.  
- Hoe je **recognize text from receipt** afbeeldingen herkent en de output verifieert.  

Ervaring met Aspose is niet nodig; alleen een werkende JDK en een IDE waar je vertrouwd mee bent.

## Vereisten

| Vereiste | Waarom het belangrijk is |
|----------|--------------------------|
| **Java 17+** (of een recente JDK) | Aspose OCR wordt geleverd met gecompileerde binaries voor moderne Java‑runtime‑omgevingen. |
| **Maven of Gradle** (om de Aspose OCR‑dependency te halen) | Maakt dependency‑beheer een fluitje van een cent. |
| **Een voorbeeld bonafbeelding** (bijv. `receipt.png`) | We gebruiken dit bestand om **recognize text from receipt** te demonstreren. |
| **Internetverbinding** (eenmalig) | Nodig om de Aspose JAR de eerste keer te downloaden. |

Als je deze al hebt, geweldig—laten we beginnen.

## Stap 1: Voeg Aspose OCR toe aan je project

Het eerste wat je nodig hebt is de Aspose OCR‑bibliotheek. Als je Maven gebruikt, voeg dan het volgende fragment toe aan je `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- Check the latest version on Maven Central -->
</dependency>
```

Voor Gradle ziet het er zo uit:

```groovy
implementation 'com.aspose:aspose-ocr:23.10'
```

> **Pro tip:** Vergrendel het versienummer. Later upgraden kan subtiele API‑wijzigingen introduceren die je code breken.

Zodra de dependency is opgelost, ben je klaar om Java‑code te schrijven die daadwerkelijk **extract text from image java** uitvoert.

## Stap 2: Laad de afbeelding voor OCR

Nu laten we de exacte regel zien die **load image for OCR** doet. Aspose biedt een handige `ImageStream.fromFile` helper.

```java
// Step 2: Load the image you want to process
ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/receipt.png"));
```

Vervang `YOUR_DIRECTORY` door het absolute of relatieve pad naar je bonbestand. Als het pad onjuist is, zal de engine een `FileNotFoundException` gooien, controleer dus de spelling.

> **Waarom dit belangrijk is:** Het correct laden van de afbeelding is de basis. Als de afbeelding niet wordt gelezen, heeft de OCR‑engine niets om te herkennen, en eindig je met een leeg JSON‑resultaat.

## Stap 3: Laat de engine JSON teruggeven

Aspose OCR kan XML, platte tekst of JSON produceren. Voor moderne API's is JSON het meest flexibel, dus we stellen het formaat expliciet in.

```java
ocrEngine.getResultSettings()
         .setResultFormat(OcrResultFormat.JSON); // XML is also available
```

Je kunt overschakelen naar `OcrResultFormat.XML` met één wijziging als je downstream‑systeem XML verkiest. De API is ontworpen om uitwisselbaar te zijn.

## Stap 4: Voer het herkenningsproces uit

Met de afbeelding geladen en het formaat ingesteld, is de volgende stap daadwerkelijk **recognize text from receipt**. Hier gebeurt het zware werk.

```java
// Step 4: Perform OCR
OcrResult ocrResult = ocrEngine.recognize();
```

De `recognize()`‑aanroep blokkeert totdat de engine klaar is met het analyseren van de afbeelding. Voor grote afbeeldingen wil je dit misschien in een achtergrondthread uitvoeren, maar voor een typische bon voltooit het zich in een fractie van een seconde.

## Stap 5: Haal het JSON‑resultaat op

Tot slot halen we de ruwe JSON‑string op en printen deze. Deze string bevat elk stuk herkende tekst, de bijbehorende begrenzingsvak, vertrouwensscores en meer.

```java
// Step 5: Retrieve the JSON string
String jsonResult = ocrResult.getResultAsString();
System.out.println(jsonResult);
```

### Verwachte output

Het uitvoeren van het volledige programma op een duidelijke bon levert iets als volgt op:

```json
{
  "pages": [
    {
      "blocks": [
        {
          "text": "Store Name",
          "confidence": 0.98,
          "rectangle": { "x": 12, "y": 15, "width": 200, "height": 30 }
        },
        {
          "text": "Date: 2026-04-28",
          "confidence": 0.95,
          "rectangle": { "x": 12, "y": 50, "width": 180, "height": 20 }
        },
        {
          "text": "Total $23.45",
          "confidence": 0.99,
          "rectangle": { "x": 12, "y": 120, "width": 150, "height": 25 }
        }
      ]
    }
  ]
}
```

Let op hoe elke regel van de bon een apart blok is met een vertrouwensscore. Je kunt deze JSON nu in elk downstream‑systeem voeren—opslaan in een database, verzenden via HTTP, of invoeren in een machine‑learning‑model.

## Volledig werkend voorbeeld

Hieronder staat de volledige, zelfstandige Java‑klasse die alles samenvoegt. Kopieer‑en‑plak het, pas het afbeeldingspad aan, en voer `mvn compile exec:java` uit (of het equivalente Gradle‑commando).

```java
import com.aspose.ocr.*;

public class JsonExportExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image you want to process
        // Make sure the path points to a real receipt image on your machine
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/receipt.png"));

        // Step 3: Configure the engine to return results in JSON format
        ocrEngine.getResultSettings()
                 .setResultFormat(OcrResultFormat.JSON); // XML is also available

        // Step 4: Run the OCR recognition process
        OcrResult ocrResult = ocrEngine.recognize();

        // Step 5: Retrieve the raw JSON string and output it
        String jsonResult = ocrResult.getResultAsString();
        System.out.println(jsonResult);
    }
}
```

> **Let op:**  
> • **Bestandspad‑fouten** – controleer de schuine strepen op Windows versus macOS/Linux.  
> • **Out‑of‑memory** – grote afbeeldingen hebben mogelijk `ocrEngine.setMemoryOptimization(true)` nodig.  
> • **Taalinstellingen** – als je bon niet‑Latijnse tekens bevat, roep `ocrEngine.setLanguage(OcrLanguage.SPANISH)` (of een andere ondersteunde taal) aan vóór `recognize()`.

## De oplossing testen

1. **Voer het programma uit** – je zou een JSON‑blob in de console moeten zien.  
2. **Valideer de JSON** – kopieer de output naar <https://jsonlint.com/> om te controleren of deze goed gevormd is.  
3. **Parseer het** – in een echt project zou je een bibliotheek zoals Jackson of Gson gebruiken om de JSON naar POJO's te mappen voor gemakkelijker gebruik.

Als je een lege `pages`‑array tegenkomt, zijn de meest voorkomende oorzaken: het afbeeldingsbestand wordt niet gevonden, of de afbeelding is te onscherp voor de standaardinstellingen van de engine. In het laatste geval, probeer de DPI te verhogen of een voorverwerkingsstap (bijv. binarisatie) toe te passen voordat je het aan Aspose geeft.

## Variaties & randgevallen

| Scenario | Wat te wijzigen |
|----------|-----------------|
| **Meerdere pagina's** (bijv. multi‑page PDF geconverteerd naar afbeeldingen) | Loop over elke afbeelding, roep `ocrEngine.setImage(...)` aan binnen de lus, en aggregeer de JSON‑resultaten. |
| **Ander uitvoerformaat** | Vervang `OcrResultFormat.JSON` door `OcrResultFormat.XML` of `OcrResultFormat.PLAIN_TEXT`. |
| **Prestatie‑afstemming** | Gebruik `ocrEngine.setRecognitionMode(OcrRecognitionMode.FAST)` voor snelheid, of `OcrRecognitionMode.ACCURATE` voor kwaliteit. |
| **Niet‑bon documenten** | Pas `ocrEngine.getPageSegmentationSettings().setDetectTables(true)` aan als je tabelextractie nodig hebt. |

Deze aanpassingen laten je de kernstroom **extract text from image java** aanpassen aan een breed scala van real‑world problemen.

## Conclusie

We hebben zojuist een beknopte, productie‑klare manier behandeld om **extract text from image java** te gebruiken met Aspose OCR. Door de vijf stappen te volgen—maak de engine, **load image for OCR**, stel JSON‑output in, **recognize text from receipt**, en lees tenslotte de JSON—kun je OCR in elke Java‑backend integreren met minimale moeite.

Vanaf hier wil je misschien:

- De JSON opslaan in een NoSQL‑database voor latere analyses.  
- Het resultaat doorsturen naar een chatbot die vragen over bonnen beantwoordt.  
- Dit combineren met Apache Tika om PDF's, DOCX en andere formaten te verwerken.

Probeer het, pas de instellingen aan op jouw specifieke documenten, en laat de machine het zware werk doen terwijl jij je richt op het creëren van waarde.

---

![tekst uit afbeelding extraheren java](placeholder-image.png "tekst uit afbeelding extraheren java")

*Figuur: Visuele weergave van de OCR‑pipeline – van afbeeldingsbestand naar JSON‑output.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}