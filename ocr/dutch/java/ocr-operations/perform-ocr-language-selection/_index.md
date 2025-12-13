---
date: 2025-12-13
description: Leer hoe u tekst uit een afbeelding kunt extraheren met Aspose.OCR voor
  Java met taalkeuze. Deze stapsgewijze Aspose OCR Java‑tutorial toont een nauwkeurige
  OCR‑configuratie.
linktitle: How to Extract Text from Image with Language Selection Using Aspose.OCR
second_title: Aspose.OCR Java API
title: Hoe tekst uit een afbeelding te extraheren met taalkeuze met Aspose.OCR
url: /nl/java/ocr-operations/perform-ocr-language-selection/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe tekst uit een afbeelding te extraheren met taalselectie met behulp van Aspose.OCR

## Introductie

Tekst uit afbeeldingsbestanden extraheren is een veelvoorkomende behoefte, of je nu gescande documenten digitaliseert, bonnetjes verwerkt of doorzoekbare archieven bouwt. Aspose.OCR voor Java maakt deze taak eenvoudig en biedt je fijnmazige controle over taalselectie, scheefcorrectie en herkenningsgebieden. In deze tutorial lopen we stap voor stap door een compleet, hands‑on voorbeeld dat laat zien **hoe tekst uit een afbeelding** te extraheren met een specifieke taalinstelling, zodat je betrouwbare OCR vandaag nog kunt integreren in je Java‑applicaties.

## Snelle antwoorden
- **Welke bibliotheek verwerkt OCR in Java?** Aspose.OCR voor Java  
- **Welke instelling selecteert de taal?** `settings.setLanguage(Language.Eng)` (of een andere ondersteunde taal)  
- **Heb ik een licentie nodig voor ontwikkeling?** Een gratis evaluatielicentie werkt voor testen; een commerciële licentie is vereist voor productie.  
- **Kan ik OCR beperken tot een regio van de afbeelding?** Ja, gebruik `RecognitionSettings.setRecognitionAreas()` met rechthoeken.  
- **Wat is de typische uitvoeringstijd?** Enkele seconden per pagina op een standaard laptop, afhankelijk van afbeeldingsgrootte en taalcomplexiteit.

## Wat is “tekst uit afbeelding extraheren”?
Tekst uit een afbeelding (OCR) zet de visuele weergave van tekens om in machine‑leesbare strings. Dit maakt zoeken, analyses en data‑extractieworkflows mogelijk die anders handmatige transcriptie zouden vereisen.

## Waarom Aspose.OCR gebruiken met taalselectie?
- **Meertalige ondersteuning** – Kies de exacte taal(en) die in je afbeelding aanwezig zijn om de nauwkeurigheid te verhogen.  
- **Fijn afgestemde controle** – Pas scheefstand aan, definieer herkenningsgebieden en stel auto‑skew gedrag in.  
- **Pure Java‑API** – Geen native afhankelijkheden, eenvoudig te integreren in elk Java‑project.  
- **Rijke resultaatsgegevens** – Verkrijg platte tekst, JSON, begrenzende rechthoeken en waarschuwingen in één oproep.

## Voorvereisten

Voordat je begint, zorg dat je het volgende hebt:

- **Java Development Kit (JDK)** geïnstalleerd (JDK 8 of later).  
- **Aspose.OCR voor Java** bibliotheek – download deze van de officiële site [here](https://reference.aspose.com/ocr/java/).  
- Een afbeeldingsbestand dat de tekst bevat die je wilt extraheren, bijv. `p3.png`.

## Importeer pakketten

In je Java‑bronbestand, voeg de benodigde Aspose.OCR‑klassen en standaard Java‑hulpmiddelen toe:

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.Language;
import com.aspose.ocr.License;
import com.aspose.ocr.RecognitionResult;
import com.aspose.ocr.RecognitionSettings;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

## Stapsgewijze handleiding

### Stap 1: Stel uw documentmap in

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";
```

Vervang `"Your Document Directory"` door het absolute pad waar `p3.png` zich bevindt.

### Stap 2: Definieer het afbeeldingspad

```java
// The image path
String file = dataDir + "p3.png";
```

Zorg ervoor dat de `file`‑variabele naar de exacte afbeelding wijst die je wilt verwerken.

### Stap 3: Maak een Aspose.OCR API‑instantie

```java
// Create API instance
AsposeOCR api = new AsposeOCR();
```

Het `AsposeOCR`‑object geeft je toegang tot alle OCR‑bewerkingen.

### Stap 4: Stel herkenningsopties in (taalselectie)

```java
// Set recognition options
RecognitionSettings settings = new RecognitionSettings();
settings.setAutoSkew(false);
ArrayList<Rectangle> rectangles = new ArrayList<Rectangle>();
rectangles.add(new Rectangle(90, 186, 775, 95));
settings.setRecognitionAreas(rectangles);
settings.setSkew(0.5);
settings.setLanguage(Language.Eng);
```

Hier doen we het volgende:

1. Schakel auto‑skew uit omdat we een handmatige skew‑waarde leveren.  
2. Definieer een rechthoekig gebied (`RecognitionAreas`) om OCR te beperken tot het deel van de afbeelding dat daadwerkelijk tekst bevat.  
3. Stel de **taal** in op Engels (`Language.Eng`). Verander dit naar `Language.Fra`, `Language.Spa`, enz., afhankelijk van je bronafbeelding.

### Stap 5: Voer OCR uit en haal resultaten op

```java
// Get result object
RecognitionResult result = null;
try {
    result = api.RecognizePage(file, settings);
} catch (IOException e) {
    e.printStackTrace();
}
```

De `RecognizePage`‑aanroep start de OCR‑engine met de afbeelding en de door jou gedefinieerde instellingen. Het resultaat wordt opgeslagen in een `RecognitionResult`‑object.

### Stap 6: Print en gebruik resultaten

```java
// Print result
System.out.println("Result: \n" + result.recognitionText + "\n\n");
for (String n : result.recognitionAreasText) {
    System.out.println(n);
}
for (Rectangle n : result.recognitionAreasRectangles) {
    System.out.println(n.height + ":" + n.width + ":" + n.x + ":" + n.y);
}
System.out.println("\nJSON:" + result.GetJson());
System.out.println("Angle:" + result.skew);
for (String n : result.warnings) {
    System.out.println(n);
}

System.out.println("OCROperationWithLanguageSelection: execution complete");
```

De console‑output toont:

- De volledige geëxtraheerde tekst (`recognitionText`).  
- Tekst voor elk gedefinieerd rechthoek (`recognitionAreasText`).  
- Coördinaten van de begrenzende rechthoek.  
- Een JSON‑representatie voor eenvoudige downstream‑verwerking.  
- Gedetecteerde skew‑hoek en eventuele waarschuwingen.

Je kunt nu `result.recognitionText` gebruiken in je bedrijfslogica — opslaan, indexeren of doorgeven aan een andere service.

## Veelvoorkomende problemen en oplossingen

| Probleem | Oorzaak | Oplossing |
|----------|---------|-----------|
| **Garbage characters** | Verkeerde taal geselecteerd | Stel de juiste `Language`‑enum in (bijv. `Language.Fra` voor Frans). |
| **No text returned** | Herkenningsgebied dekt de tekst niet | Pas de `Rectangle`‑coördinaten aan of verwijder `RecognitionAreas` om de hele afbeelding te verwerken. |
| **Slow performance** | Zeer grote afbeelding of hoge resolutie | Schaal de afbeelding naar beneden vóór OCR of vergroot de geheugentoewijzing voor de JVM. |
| **Warnings about unsupported format** | Afbeeldingsformaat niet herkend | Converteer de afbeelding naar PNG, JPEG of TIFF vóór verwerking. |

## Veelgestelde vragen

**Q: Kan ik meerdere talen herkennen in één OCR‑oproep?**  
A: Ja. Gebruik `settings.setLanguage(Language.Eng | Language.Fra)` om meertalige herkenning in te schakelen.

**Q: Welke afbeeldingsformaten ondersteunt Aspose.OCR?**  
A: PNG, JPEG, BMP, TIFF, GIF en diverse andere. Geef gewoon het juiste bestandspad op.

**Q: Is er een limiet voor de afbeeldingsgrootte?**  
A: Er is geen harde limiet, maar zeer grote afbeeldingen verhogen het geheugenverbruik en de verwerkingstijd. Overweeg grote bestanden te verkleinen.

**Q: Hoe verkrijg ik een productielicentie?**  
A: Koop een licentie via de Aspose‑website en pas deze toe via de `License`‑klasse zoals weergegeven in de Aspose‑documentatie.

**Q: Kan ik tekst direct uit een PDF‑pagina extraheren?**  
A: Niet rechtstreeks met Aspose.OCR. Converteer de PDF‑pagina eerst naar een afbeelding (bijv. met Aspose.PDF) en voer daarna OCR uit.

## Conclusie

Je hebt nu gezien hoe je **tekst uit een afbeelding** kunt extraheren met Aspose.OCR voor Java, terwijl je de juiste taal selecteert en de herkenning beperkt tot specifieke regio's. Deze aanpak levert nauwkeurige, high‑performance OCR die in elke Java‑gebaseerde workflow kan worden ingebed — van documentbeheersystemen tot data‑capture pipelines.

---

**Last Updated:** 2025-12-13  
**Tested With:** Aspose.OCR 24.11 for Java  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}