---
date: 2026-02-12
description: Leer hoe je afbeeldings­tekst kunt OCR’en met taalkeuze met behulp van
  Aspose.OCR voor Java. Deze stapsgewijze gids behandelt tekstextractie in Java, OCR‑kantcorrectie
  en meer.
linktitle: How to OCR Image Text with Language Using Aspose.OCR
second_title: Aspose.OCR Java API
title: Hoe afbeeldingstekst met taal OCR'en met Aspose.OCR
url: /nl/java/ocr-operations/perform-ocr-language-selection/
weight: 11
---

02-12" keep same.

"**Tested With:** Aspose.OCR 24.11 for Java" keep.

"**Author:** Aspose" keep.

Then closing shortcodes.

Then backtop button shortcode unchanged.

Make sure to keep all markdown formatting.

Now produce final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe OCR-tekst uit afbeelding met taal gebruiken met Aspose.OCR

## Introductie

Tekst uit afbeeldingsbestanden extraheren is een veelvoorkomende behoefte, of je nu gescande documenten digitaliseert, bonnen verwerkt, of doorzoekbare archieven bouwt. In deze tutorial lopen we een compleet, hands‑on voorbeeld door dat laat zien **hoe OCR-tekst uit een afbeelding** met een specifieke taalinstelling te gebruiken, zodat je vandaag nog betrouwbare OCR in je Java‑applicaties kunt integreren. Je ziet ook hoe je OCR‑scheefstandcorrectie en regio‑gebaseerde herkenning kunt afhandelen voor optimale nauwkeurigheid.

## Snelle antwoorden
- **Welke bibliotheek verwerkt OCR in Java?** Aspose.OCR for Java  
- **Welke instelling selecteert de taal?** `settings.setLanguage(Language.Eng)` (of een andere ondersteunde taal)  
- **Heb ik een licentie nodig voor ontwikkeling?** Een gratis evaluatielicentie werkt voor testen; een commerciële licentie is vereist voor productie.  
- **Kan ik OCR beperken tot een regio van de afbeelding?** Ja, gebruik `RecognitionSettings.setRecognitionAreas()` met rechthoeken.  
- **Wat is de typische uitvoeringstijd?** Enkele seconden per pagina op een standaard laptop, afhankelijk van afbeeldingsgrootte en taalkomplexiteit.

## Hoe OCR-tekst uit afbeelding met taalselectie
In deze sectie beantwoorden we de kernvraag **hoe OCR** een afbeelding uit te voeren wanneer je de taal van de tekst kent. Het selecteren van de juiste taal verbetert de herkenningsnauwkeurigheid drastisch omdat de OCR‑engine taalspecifieke woordenboeken en tekenmodellen kan toepassen.

### Waarom dit belangrijk is
- **Hogere nauwkeurigheid** – taalspecifieke modellen verminderen foutieve herkenningen.  
- **Prestatieverbetering** – de engine slaat onnodige taalkontrollen over.  
- **Betere handling van diakritische tekens** – Frans, Spaans, Duits, enz. worden correct herkend wanneer de overeenkomstige `Language` enum wordt gebruikt.

## Wat is “tekst uit afbeelding extraheren”?
Tekst uit afbeelding (OCR) zet de visuele weergave van tekens om in machine‑leesbare strings. Dit maakt zoeken, analyses en data‑extractieworkflows mogelijk die anders handmatige transcriptie zouden vereisen.

## Waarom Aspose.OCR gebruiken met taalselectie?
- **Meertalige ondersteuning** – Kies de exacte taal/talen die in uw afbeelding aanwezig zijn om de nauwkeurigheid te verhogen.  
- **Fijn afgestemde controle** – Pas scheefstand aan, definieer herkenningsgebieden, en stel auto‑scheefstandgedrag in.  
- **Pure Java API** – Geen native afhankelijkheden, eenvoudig te integreren in elk Java‑project.  
- **Rijke resultaatsgegevens** – Verkrijg platte tekst, JSON, begrenzende rechthoeken en waarschuwingen in één oproep.

## Vereisten

Voordat je begint, zorg dat je het volgende hebt:

- **Java Development Kit (JDK)** geïnstalleerd (JDK 8 of later).  
- **Aspose.OCR for Java** bibliotheek – download deze van de officiële site [here](https://reference.aspose.com/ocr/java/).  
- Een afbeeldingsbestand dat de tekst bevat die u wilt extraheren, bijv. `p3.png`.

## Pakketten importeren

In uw Java‑bronbestand, neem de vereiste Aspose.OCR‑klassen en standaard Java‑hulpmiddelen op:

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

Zorg ervoor dat de `file`‑variabele naar de exacte afbeelding wijst die u wilt verwerken.

### Stap 3: Maak een Aspose.OCR API‑instantie

```java
// Create API instance
AsposeOCR api = new AsposeOCR();
```

Het `AsposeOCR`‑object geeft u toegang tot alle OCR‑bewerkingen.

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

Hier doen we:

1. Schakel auto‑scheefstand uit omdat we een handmatige scheefstandwaarde geven.  
2. Definieer een rechthoekig gebied (`RecognitionAreas`) om OCR te beperken tot het deel van de afbeelding dat daadwerkelijk tekst bevat.  
3. Stel de **taal** in op Engels (`Language.Eng`). Verander dit naar `Language.Fra`, `Language.Spa`, enz., afhankelijk van uw bronafbeelding.

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

De `RecognizePage`‑aanroep voert de OCR‑engine uit met de afbeelding en de door u gedefinieerde instellingen. Het resultaat wordt opgeslagen in een `RecognitionResult`‑object.

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
- Coördinaten van begrenzende rechthoeken.  
- Een JSON‑representatie voor eenvoudige downstream verwerking.  
- Gedetecteerde scheefstandhoek en eventuele waarschuwingen.

U kunt nu `result.recognitionText` in uw bedrijfslogica voeden — opslaan, indexeren of doorgeven aan een andere service.

## Veelvoorkomende problemen en oplossingen

| Probleem | Oorzaak | Oplossing |
|----------|---------|-----------|
| **Onjuiste tekens** | Verkeerde taal geselecteerd | Stel de juiste `Language` enum in (bijv. `Language.Fra` voor Frans). |
| **Geen tekst geretourneerd** | Herkenningsgebied dekt de tekst niet | Pas de `Rectangle`‑coördinaten aan of verwijder `RecognitionAreas` om de hele afbeelding te verwerken. |
| **Langzame prestaties** | Zeer grote afbeelding of hoge resolutie | Verklein de afbeelding vóór OCR of vergroot de geheugenallocatie voor de JVM. |
| **Waarschuwingen over niet‑ondersteund formaat** | Afbeeldingsformaat niet herkend | Converteer de afbeelding naar PNG, JPEG of TIFF vóór verwerking. |

## Veelgestelde vragen

**V: Kan ik meerdere talen herkennen in één OCR‑oproep?**  
**A:** Ja. Gebruik `settings.setLanguage(Language.Eng | Language.Fra)` om meertalige herkenning in te schakelen.

**V: Welke afbeeldingsformaten ondersteunt Aspose.OCR?**  
**A:** PNG, JPEG, BMP, TIFF, GIF en verschillende andere. Geef gewoon het juiste bestandspad op.

**V: Is er een grootte‑limiet voor de afbeelding?**  
**A:** Er is geen harde limiet, maar zeer grote afbeeldingen verhogen het geheugenverbruik en de verwerkingstijd. Overweeg grote bestanden te verkleinen.

**V: Hoe verkrijg ik een productielicentie?**  
**A:** Koop een licentie via de Aspose‑website en pas deze toe via de `License`‑klasse zoals weergegeven in de Aspose‑documentatie.

**V: Kan ik tekst direct uit een PDF‑pagina extraheren?**  
**A:** Niet direct met Aspose.OCR. Converteer de PDF‑pagina eerst naar een afbeelding (bijv. met Aspose.PDF) en voer vervolgens OCR uit.

## Conclusie

U heeft nu gezien hoe **tekst uit afbeelding** te extraheren met Aspose.OCR voor Java, terwijl u de juiste taal selecteert en de herkenning beperkt tot specifieke regio's. Deze aanpak levert nauwkeurige, hoge‑presterende OCR die in elke Java‑gebaseerde workflow kan worden ingebed — van documentbeheersystemen tot data‑capture‑pijplijnen. Klaar om verder te gaan? Probeer de taal‑enum te wijzigen, experimenteer met verschillende herkenningsgebieden, en integreer de resultaten in uw eigen applicatielogica.

---

**Last Updated:** 2026-02-12  
**Tested With:** Aspose.OCR 24.11 for Java  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}