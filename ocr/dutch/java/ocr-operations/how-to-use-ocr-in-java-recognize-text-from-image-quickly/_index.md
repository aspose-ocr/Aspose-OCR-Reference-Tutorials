---
category: general
date: 2026-02-17
description: Leer hoe je OCR in Java kunt gebruiken om tekst uit afbeeldingsbestanden
  te herkennen, tekst uit PNG‑bonnetjes te extraheren en een bon om te zetten naar
  JSON met Aspose OCR.
draft: false
keywords:
- how to use OCR
- recognize text from image
- extract text from png
- convert receipt to json
language: nl
og_description: Stapsgewijze gids over hoe OCR in Java te gebruiken om tekst uit een
  afbeelding te herkennen, tekst uit PNG‑bonnen te extraheren en de bon naar JSON
  te converteren.
og_title: Hoe OCR in Java te gebruiken – Tekst herkennen uit afbeelding
tags:
- OCR
- Java
- Aspose
- Image Processing
title: Hoe OCR in Java te gebruiken – Herken snel tekst uit een afbeelding
url: /nl/java/ocr-operations/how-to-use-ocr-in-java-recognize-text-from-image-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe OCR te gebruiken in Java – Tekst uit afbeelding snel herkennen

Heb je je ooit afgevraagd **hoe je OCR kunt gebruiken** om tekst uit een foto van een bon te halen? Misschien heb je een paar online tools geprobeerd, alleen om te eindigen met onleesbare tekens of een formaat dat je niet kunt verwerken. Het goede nieuws is dat je met een paar regels Java‑code **tekst uit afbeelding** kunt **herkennen**, **tekst uit PNG**‑bonnen kunt **extraheren**, en zelfs **bon naar JSON kunt converteren** voor downstream verwerking.  

In deze tutorial lopen we de volledige workflow door – van het licentiëren van de Aspose OCR‑bibliotheek tot het verkrijgen van een schone JSON‑payload die je kunt invoeren in een database of een machine‑learning‑model. Geen poespas, alleen een praktisch, uitvoerbaar voorbeeld dat je kunt copy‑pasten in je IDE. Aan het einde heb je een zelfstandige applicatie die `receipt.png` neemt en een kant‑klaar JSON‑string uitspuugt.

## Wat je nodig hebt

- **Java Development Kit (JDK) 8+** – elke recente versie werkt.
- **Aspose OCR for Java** bibliotheek (het Maven‑artifact is `com.aspose:aspose-ocr`).
- Een **geldig Aspose OCR licentiebestand** (`Aspose.OCR.lic`). De gratis proefversie werkt voor testen, maar een juiste licentie verwijdert evaluatielimieten.
- Een afbeeldingsbestand (PNG, JPEG, enz.) dat de tekst bevat die je wilt lezen—noemen we `receipt.png` en plaatsen we in een bekende map.
- Je favoriete IDE (IntelliJ IDEA, Eclipse, VS Code…) – je bent vrij om te kiezen.

> **Pro tip:** Houd je licentiebestand buiten de bronmap en verwijs ernaar via een absoluut of relatief pad om te voorkomen dat het wordt gecommit naar versiebeheer.

Nu de vereisten duidelijk zijn, duiken we in de daadwerkelijke code.

## Hoe OCR te gebruiken – Kernstappen

Hieronder vind je een overzicht op hoog niveau van de acties die we gaan uitvoeren:

1. **Laad de Aspose OCR bibliotheek** en pas je licentie toe.  
2. **Maak een `OcrEngine`‑instantie** – dit is de engine die het zware werk doet.  
3. **Bereid een `OcrInput`‑object** voor dat naar de afbeelding wijst die je wilt verwerken.  
4. **Roep `recognize` aan met `ResultFormat.JSON`** om een JSON‑representatie van de geëxtraheerde tekst te krijgen.  
5. **Verwerk de JSON‑output** – print het, schrijf het naar een bestand, of parseer het verder.

Elke stap wordt in detail uitgelegd in de volgende secties.

## Stap 1 – Installeer Aspose OCR en pas je licentie toe

Eerst voeg je de Aspose OCR‑dependency toe aan je `pom.xml` als je Maven gebruikt:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Check Maven Central for the latest version -->
</dependency>
```

Laad nu in je Java‑code de licentie. Deze stap is essentieel; zonder deze draait de bibliotheek in evaluatiemodus en kan er een watermerk in de output worden geplaatst.

```java
import com.aspose.ocr.*;

public class OcrSetup {
    public static void applyLicense() throws Exception {
        // Replace the path with the actual location of your Aspose.OCR.lic file
        License ocrLicense = new License();
        ocrLicense.setLicense("C:/licenses/Aspose.OCR.lic");
    }
}
```

> **Waarom dit belangrijk is:** Het `License`‑object vertelt de OCR‑engine dat je geautoriseerd bent om de volledige functionaliteit te gebruiken, inclusief hoge‑nauwkeurigheid herkenning en JSON‑export. Als je deze stap overslaat kun je nog steeds **tekst uit afbeelding** herkennen, maar de resultaten kunnen worden beperkt.

## Stap 2 – Maak de OCR‑engine‑instantie

De `OcrEngine`‑class is het toegangspunt voor alle OCR‑operaties. Beschouw het als het “brein” dat de pixels leest en beslist welke tekens ze vertegenwoordigen.

```java
import com.aspose.ocr.*;

public class OcrEngineFactory {
    public static OcrEngine createEngine() {
        // No special configuration needed for basic usage
        return new OcrEngine();
    }
}
```

Je kunt de engine later aanpassen (bijv. taal instellen, deskew inschakelen) als je bonnen niet‑Latijnse scripts bevatten of onder een hoek zijn gescand. Voor de meeste in de VS gebruikte bonnen werken de standaardinstellingen prima.

## Stap 3 – Laad de afbeelding die je wilt verwerken

Nu wijzen we de OCR‑engine naar het bestand dat de bon bevat. De `OcrInput`‑class kan meerdere afbeeldingen accepteren, maar voor deze tutorial houden we het simpel met één PNG.

```java
import com.aspose.ocr.*;

public class ImageLoader {
    public static OcrInput loadImage(String imagePath) {
        OcrInput input = new OcrInput();
        // Add the PNG receipt – this is where we **extract text from PNG**
        input.add(imagePath);
        return input;
    }
}
```

Als je ooit **tekst uit PNG**‑bestanden in bulk moet **extraheren**, roep dan gewoon herhaaldelijk `input.add()` aan of geef een lijst met bestands‑paden door.

## Stap 4 – Herken tekst en converteer bon naar JSON

Hier is het hart van de tutorial. We vragen de engine om de tekst te herkennen en vragen om het resultaat in JSON‑formaat. De `ResultFormat.JSON`‑vlag doet al het zware werk voor ons.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.output.*;

public class JsonRecognizer {
    public static String recognizeToJson(OcrEngine engine, OcrInput input) throws Exception {
        // Perform OCR and request JSON output
        OcrResult result = engine.recognize(input, ResultFormat.JSON);
        // Retrieve the JSON string
        return result.getJson();
    }
}
```

De JSON‑payload bevat elke herkende regel, de bijbehorende bounding box, confidence‑score en de ruwe tekst. Deze structuur maakt het triviaal om **bon naar JSON** te **converteren** en vervolgens in te voeren in elke downstream‑API.

## Stap 5 – Zet alles bij elkaar en voer het programma uit

Hieronder staat de volledige, kant‑klaar uitvoerbare Java‑klasse die alles samenbrengt. Sla het op als `JsonExportDemo.java` (of een andere naam naar keuze) en voer het uit vanuit je IDE of de commandoregel.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.output.*;

public class JsonExportDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Apply your Aspose OCR license (replace with your actual license file)
        License ocrLicense = new License();
        ocrLicense.setLicense("Aspose.OCR.lic"); // <-- adjust path if needed

        // 2️⃣ Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // 3️⃣ Prepare the input image that contains the text to be recognized
        OcrInput ocrInput = new OcrInput();
        // Replace with the absolute or relative path to your receipt PNG
        ocrInput.add("YOUR_DIRECTORY/receipt.png"); // <-- **extract text from PNG** here

        // 4️⃣ Perform recognition and request the result in JSON format
        OcrResult ocrResult = ocrEngine.recognize(ocrInput, ResultFormat.JSON);

        // 5️⃣ Retrieve the JSON string from the result
        String jsonResult = ocrResult.getJson();

        // 6️⃣ Output the JSON (or save it to a file for further processing)
        System.out.println(jsonResult);
    }
}
```

### Verwachte output

Het uitvoeren van het programma print een JSON‑string die lijkt op het volgende (de exacte inhoud hangt af van jouw bon):

```json
{
  "pages": [
    {
      "lines": [
        {
          "text": "Store Name",
          "confidence": 0.99,
          "boundingBox": [12, 34, 200, 45]
        },
        {
          "text": "Date: 2024-02-15",
          "confidence": 0.98,
          "boundingBox": [12, 60, 180, 45]
        },
        {
          "text": "Total: $23.45",
          "confidence": 0.97,
          "boundingBox": [12, 120, 150, 45]
        }
      ]
    }
  ]
}
```

Je kunt deze JSON nu invoeren in een database, een REST‑endpoint, of een data‑analyse‑pipeline. De **bon naar JSON**‑stap is al voor je uitgevoerd.

## Veelgestelde vragen en randgevallen

### Wat als de afbeelding gedraaid is?

Aspose OCR detecteert en corrigeert automatisch lichte rotaties. Voor sterk scheve afbeeldingen roep je `engine.getImagePreprocessingOptions().setDeskew(true)` aan vóór herkenning.

### Hoe ga ik om met meerdere talen?

Gebruik `engine.getLanguage()` om de gewenste taal in te stellen, bijvoorbeeld `engine.setLanguage(Language.FRENCH)`. Handig wanneer je **tekst uit afbeelding** moet **herkennen** die meertalige bonnen bevat.

### Kan ik platte tekst in plaats van JSON outputten?

Zeker. Vervang `ResultFormat.JSON` door `ResultFormat.TEXT` en roep `result.getText()` aan.

### Is er een manier om OCR te beperken tot een specifiek gebied?

Ja—gebruik `ocrInput.add(imagePath, new Rectangle(x, y, width, height))` om je te focussen op het bon‑gebied, wat snelheid en nauwkeurigheid kan verbeteren.

## Pro‑tips voor productie‑klare OCR

- **Cache het licentie‑object** als je veel bestanden in een lus verwerkt; het herhaaldelijk aanmaken voegt overhead toe.
- **Batch verwerken**: laad alle bon‑paden in één `OcrInput` en roep één keer `recognize` aan. De JSON zal een array van pagina's bevatten, elk met zijn eigen regels.
- **Valideer JSON**: nadat je de string hebt, parseer deze met een bibliotheek zoals Jackson om te verzekeren dat hij goed gevormd is voordat je hem opslaat.
- **Monitor confidence**: de JSON bevat een `confidence`‑veld per regel. Filter regels onder een drempel (bijv. 0.85) om onbruikbare data te vermijden.
- **Beveilig je licentie**: sla `Aspose.OCR.lic` op in een veilige kluis of als omgevingsvariabele, vooral bij cloud‑implementaties.

## Conclusie

We hebben behandeld **hoe je OCR** in Java kunt gebruiken om **tekst uit afbeelding** te **herkennen**, **tekst uit PNG**‑bonnen te **extraheren**, en **bon naar JSON** te **converteren** – alles met een beknopt, end‑to‑end voorbeeld. De stappen zijn eenvoudig, de code volledig uitvoerbaar, en de JSON‑output geeft je een gestructureerde weergave die klaar is voor elk downstream‑systeem.

Vervolgens kun je meer geavanceerde scenario's verkennen: de JSON invoeren in Apache Kafka voor realtime verwerking, regex‑patronen toepassen om regel‑item totalen te extraheren, of integreren met een cloud‑OCR‑service voor schaalbaarheid. Wat je ook kiest, de basisprincipes die je nu hebt geleerd blijven hetzelfde.

Heb je vragen, of liep je tegen een probleem aan tijdens het uitproberen? Laat een reactie achter hieronder, en laten we samen het probleem oplossen. Veel programmeerplezier, en geniet van het omzetten van die rommelige bonafbeeldingen naar schone, doorzoekbare data!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}