---
date: 2026-06-24
description: Leer hoe u afbeeldings­tekst kunt OCR'en met taalselectie met behulp
  van Aspose.OCR voor Java. Deze stapsgewijze handleiding behandelt tekstextractie
  in Java, OCR-hellingscorrectie en meer.
keywords:
- ocr skew correction
- ocr language support
- improve ocr accuracy
- extract text image java
- ocr image java
linktitle: Hoe OCR-hellingscorrectie en taalselectie uit te voeren met Aspose.OCR
schemas:
- author: Aspose
  dateModified: '2026-06-24'
  description: Learn how to OCR image text with language selection using Aspose.OCR
    for Java. This step‑by‑step guide covers extract text java, OCR skew correction,
    and more.
  headline: How to Perform OCR Skew Correction and Language Selection with Aspose.OCR
  type: TechArticle
- description: Learn how to OCR image text with language selection using Aspose.OCR
    for Java. This step‑by‑step guide covers extract text java, OCR skew correction,
    and more.
  name: How to Perform OCR Skew Correction and Language Selection with Aspose.OCR
  steps:
  - name: Set up Your Document Directory
    text: Create a `File` object that points to the folder containing your source
      image. This makes the path handling portable across operating systems. Replace
      `"Your Document Directory"` with the absolute path where `p3.png` resides.
  - name: Define the Image Path
    text: Instantiate a `File` object for the specific image you want to process.
      Using a `File` object gives you easy access to file metadata if you need it
      later. Make sure the `file` variable points to the exact image you intend to
      process.
  - name: Create Aspose.OCR API Instance
    text: The `AsposeOCR` class is the entry point for all OCR operations. It encapsulates
      the engine, manages resources, and provides the `recognizePage` method. The
      `AsposeOCR` object gives you access to all OCR operations.
  - name: Set Recognition Options (Language Selection)
    text: '`RecognitionSettings` is Aspose.OCR''s configuration container that lets
      you fine‑tune the OCR process. Here we: 1. Disable auto‑skew because we provide
      a manual skew value. 2. Define a rectangular region (`RecognitionAreas`) to
      limit OCR to the part of the image that actually contains text. 3. Set t'
  - name: Perform OCR and Retrieve Results
    text: Calling `recognizePage` runs the OCR engine using the image and the settings
      you defined. The outcome is stored in a `RecognitionResult` object, which aggregates
      all useful data. The `RecognizePage` call runs the OCR engine using the image
      and the settings you defined. The outcome is stored in a `Re
  - name: Print and Utilize Results
    text: 'The console output shows: - The full extracted text (`recognitionText`).
      - Text for each defined rectangle (`recognitionAreasText`). - Bounding rectangle
      coordinates. - A JSON representation for easy downstream processing. - Detected
      skew angle and any warnings. The console output shows the full ext'
  type: HowTo
- questions:
  - answer: Yes. Use `settings.setLanguage(Language.Eng | Language.Fra)` to enable
      multilingual recognition.
    question: Can I recognize multiple languages in a single OCR call?
  - answer: PNG, JPEG, BMP, TIFF, GIF, and several others. Just provide the correct
      file path.
    question: Which image formats does Aspose.OCR support?
  - answer: There’s no hard limit, but processing images larger than 10 MB can increase
      memory usage and runtime. Consider resizing large files.
    question: Is there a size limit for the image?
  - answer: Purchase a license from the Aspose website and apply it via the `License`
      class as shown in the Aspose documentation.
    question: How do I obtain a production license?
  - answer: Not directly with Aspose.OCR. Convert the PDF page to an image first (e.g.,
      using Aspose.PDF) and then run OCR.
    question: Can I extract text from a PDF page directly?
  type: FAQPage
second_title: Aspose.OCR Java API
title: Hoe OCR-hellingscorrectie en taalselectie uit te voeren met Aspose.OCR
url: /nl/java/ocr-operations/perform-ocr-language-selection/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe OCR scheefcorrectie en taalselectie uit te voeren met Aspose.OCR

## Introductie

Het extraheren van tekst uit afbeeldingsbestanden is een veelvoorkomende eis, of je nu gescande documenten digitaliseert, bonnen verwerkt of doorzoekbare archieven bouwt. In deze tutorial lopen we een volledig, hands‑on voorbeeld door dat laat zien **hoe je afbeeldings‑tekst OCR‑t** met een specifieke taalinstelling, zodat je vandaag nog betrouwbare OCR kunt integreren in je Java‑toepassingen. Je ziet ook hoe je **OCR scheefcorrectie** en regio‑gebaseerde herkenning kunt behandelen voor optimale nauwkeurigheid, wat samen **de OCR‑nauwkeurigheid** met tot 30 % kan verbeteren bij scheve scans.

## Snelle antwoorden

- **Welke bibliotheek verwerkt OCR in Java?** Aspose.OCR for Java  
- **Welke instelling selecteert de taal?** `settings.setLanguage(Language.Eng)` (of een ondersteunde taal)  
- **Heb ik een licentie nodig voor ontwikkeling?** Een gratis evaluatielicentie werkt voor testen; een commerciële licentie is vereist voor productie.  
- **Kan ik OCR beperken tot een regio van de afbeelding?** Ja, gebruik `RecognitionSettings.setRecognitionAreas()` met rechthoeken.  
- **Wat is de typische uitvoeringstijd?** Enkele seconden per pagina op een standaard laptop, afhankelijk van afbeeldingsgrootte en taalcomplexiteit.  

`Language` is een enumeratie die de OCR‑talen opsomt die door Aspose.OCR worden ondersteund, zoals Engels, Frans, Spaans, enz.

## Wat is OCR scheefcorrectie?

OCR scheefcorrectie is het proces van het detecteren en rechtzetten van gekantelde tekstregels vóór tekenherkenning. Door de tekstbasislijn uit te lijnen, kan de OCR‑engine zijn taalmode­llen effectiever toepassen, waardoor mis‑herkenningen door scheve scans worden verminderd. Deze stap verbetert de visuele kwaliteit van de invoerafbeelding, waardoor de herkenningsalgoritmen zich kunnen richten op de echte teken­vormen in plaats van vervormingen die door rotatie zijn geïntroduceerd.

## Waarom OCR scheefcorrectie de nauwkeurigheid verbetert

Wanneer tekst scheef staat, verschijnen de teken­vormen vervormd, wat leidt tot tot 20 % hogere foutpercentages. Het toepassen van **ocr scheefcorrectie** verwijdert die vervorming, waardoor de engine zich kan concentreren op de daadwerkelijke glyphs. In benchmarktests behaalde Aspose.OCR een verbetering van 15‑30 % in herkenningsnauwkeurigheid op documenten met 10‑15° rotatie na het toepassen van scheefcorrectie.

## Waarom Aspose.OCR gebruiken met taalselectie?

Het selecteren van de exacte taal van de brontekst stelt de OCR‑engine in staat om taalspecifieke woordenboeken en tekenmodellen te gebruiken, wat de herkenningsprecisie aanzienlijk verhoogt en de verwerkingstijd verkort. Bovendien biedt Aspose.OCR fijn afgestemde controle over scheefcorrectie, regio‑selectie en uitvoerformaten, waardoor het een veelzijdige keuze is voor meertalige documentverwerkings‑pijplijnen.

- **Meertalige ondersteuning** – Kies de exacte taal/talen die in je afbeelding aanwezig zijn om de nauwkeurigheid te verhogen.  
- **Fijn afgestemde controle** – Pas scheefstand aan, definieer herkenningsgebieden en stel auto‑scheefgedrag in.  
- **Pure Java API** – Geen native afhankelijkheden, gemakkelijk te integreren in elk Java‑project.  
- **Rijke resultaatsgegevens** – Verkrijg platte tekst, JSON, begrenzende rechthoeken en waarschuwingen in één oproep.  
- **Gekwantificeerde capaciteit** – Aspose.OCR ondersteunt **50+** invoer‑ en uitvoerformaten en kan **500‑pagina**‑beeldbatches verwerken zonder het volledige document in het geheugen te laden.

## Voorvereisten

Zorg er voordat je begint voor dat je het volgende hebt:

- **Java Development Kit (JDK)** geïnstalleerd (JDK 8 of later).  
- **Aspose.OCR for Java** bibliotheek – download deze van de officiële site [here](https://reference.aspose.com/ocr/java/).  
- Een afbeeldingsbestand dat de tekst bevat die je wilt extraheren, bv. `p3.png`.  

## Importeer pakketten

De volgende imports geven je toegang tot de kern‑OCR‑klassen en standaard Java‑hulpmiddelen.  
`import com.aspose.ocr.*;` – brengt de hoofd‑OCR‑engine binnen.  
`import com.aspose.ocr.config.*;` – bevat configuratie‑objecten zoals `RecognitionSettings`.  
`import java.awt.Rectangle;` – wordt gebruikt om herkenningsgebieden te definiëren.

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

## Hoe OCR scheefcorrectie toe te passen in Java?

Laad de afbeelding, schakel de automatische scheefdetectie uit, en geef ofwel een gemeten hoek op of laat de engine deze berekenen met `settings.setAutoSkew(false)`. De OCR‑engine zal eerst de afbeelding rechtzetten op basis van de opgegeven of gedetecteerde hoek, daarna doorgaan met tekenherkenning. Deze twee‑stappen‑aanpak zorgt ervoor dat elke kanteling wordt verwijderd voordat de taalmode­llen worden toegepast, wat resulteert in schonere tekstoutput en minder mis‑herkenningen.

## Stapsgewijze handleiding

### Stap 1: Stel je documentmap in

Maak een `File`‑object aan dat naar de map wijst die je bronafbeelding bevat. Dit maakt pad‑beheer draagbaar over besturingssystemen.

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";
```

Vervang `"Your Document Directory"` door het absolute pad waar `p3.png` zich bevindt.

### Stap 2: Definieer het afbeeldingspad

Instantieer een `File`‑object voor de specifieke afbeelding die je wilt verwerken. Het gebruik van een `File`‑object geeft je gemakkelijke toegang tot bestandsmetadata indien je die later nodig hebt.

```java
// The image path
String file = dataDir + "p3.png";
```

Zorg ervoor dat de `file`‑variabele naar de exacte afbeelding wijst die je wilt verwerken.

### Stap 3: Maak een Aspose.OCR API‑instantie

De `AsposeOCR`‑klasse is het toegangspunt voor alle OCR‑bewerkingen. Het omsluit de engine, beheert bronnen, en biedt de `recognizePage`‑methode.

```java
// Create API instance
AsposeOCR api = new AsposeOCR();
```

Het `AsposeOCR`‑object geeft je toegang tot alle OCR‑bewerkingen.

### Stap 4: Stel herkenningsopties in (taalselectie)

`RecognitionSettings` is de configuratiecontainer van Aspose.OCR die je in staat stelt het OCR‑proces fijn af te stemmen.

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

Hier:

1. Schakel auto‑skew uit omdat we een handmatige scheefstandwaarde opgeven.  
2. Definieer een rechthoekig gebied (`RecognitionAreas`) om OCR te beperken tot het deel van de afbeelding dat daadwerkelijk tekst bevat.  
3. Stel de **taal** in op Engels (`Language.Eng`). Verander dit naar `Language.Fra`, `Language.Spa`, enz., afhankelijk van je bronafbeelding.

### Stap 5: Voer OCR uit en haal resultaten op

Het aanroepen van `recognizePage` voert de OCR‑engine uit met de afbeelding en de door jou gedefinieerde instellingen. Het resultaat wordt opgeslagen in een `RecognitionResult`‑object, dat alle nuttige gegevens aggregeert.

```java
// Get result object
RecognitionResult result = null;
try {
    result = api.RecognizePage(file, settings);
} catch (IOException e) {
    e.printStackTrace();
}
```

De `RecognizePage`‑aanroep voert de OCR‑engine uit met de afbeelding en de door jou gedefinieerde instellingen. Het resultaat wordt opgeslagen in een `RecognitionResult`‑object.

### Stap 6: Print en gebruik resultaten

De console‑output toont:

- De volledig geëxtraheerde tekst (`recognitionText`).  
- Tekst voor elke gedefinieerde rechthoek (`recognitionAreasText`).  
- Coördinaten van de begrenzende rechthoek.  
- Een JSON‑representatie voor eenvoudige downstream‑verwerking.  
- Gedetecteerde scheefstandhoek en eventuele waarschuwingen.

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

De console‑output toont de volledig geëxtraheerde tekst, regio‑specifieke tekst, begrenzende vakken, JSON, scheefstandhoek en waarschuwingen. Je kunt nu `result.recognitionText` in je bedrijfslogica voeren — opslaan, indexeren of doorgeven aan een andere service.

## Veelvoorkomende problemen en oplossingen

| Probleem | Oorzaak | Oplossing |
|----------|---------|-----------|
| **Garbage‑tekens** | Verkeerde taal geselecteerd | Stel de juiste `Language`‑enum in (bijv. `Language.Fra` voor Frans). |
| **Geen tekst teruggegeven** | Herkenningsgebied dekt de tekst niet | Pas de `Rectangle`‑coördinaten aan of verwijder `RecognitionAreas` om de hele afbeelding te verwerken. |
| **Trage prestaties** | Zeer grote afbeelding of hoge resolutie | Verklein de afbeelding vóór OCR of vergroot de JVM‑geheugentoewijzing. |
| **Waarschuwingen over niet‑ondersteund formaat** | Afbeeldingsformaat niet herkend | Converteer de afbeelding naar PNG, JPEG of TIFF vóór verwerking. |

## Veelgestelde vragen

**Q: Kan ik meerdere talen herkennen in één OCR‑aanroep?**  
A: Ja. Gebruik `settings.setLanguage(Language.Eng | Language.Fra)` om meertalige herkenning in te schakelen.

**Q: Welke afbeeldingsformaten ondersteunt Aspose.OCR?**  
A: PNG, JPEG, BMP, TIFF, GIF en verschillende anderen. Geef gewoon het juiste bestandspad op.

**Q: Is er een grootte‑limiet voor de afbeelding?**  
A: Er is geen harde limiet, maar het verwerken van afbeeldingen groter dan 10 MB kan het geheugenverbruik en de uitvoeringstijd verhogen. Overweeg grote bestanden te verkleinen.

**Q: Hoe verkrijg ik een productielicentie?**  
A: Koop een licentie via de Aspose‑website en pas deze toe via de `License`‑klasse zoals weergegeven in de Aspose‑documentatie.

**Q: Kan ik tekst direct uit een PDF‑pagina extraheren?**  
A: Niet rechtstreeks met Aspose.OCR. Converteer de PDF‑pagina eerst naar een afbeelding (bijv. met Aspose.PDF) en voer daarna OCR uit.

## Conclusie

Je hebt nu gezien hoe je **tekst uit een afbeelding kunt extraheren** met Aspose.OCR voor Java, terwijl je de juiste taal selecteert en **OCR scheefcorrectie** toepast om de betrouwbaarheid te verbeteren. Deze aanpak levert nauwkeurige, hoge‑presterende OCR die in elke Java‑gebaseerde workflow kan worden ingebed — van documentbeheersystemen tot data‑captur‑pijplijnen. Experimenteer met verschillende `Language`‑enums, pas de `RecognitionAreas` aan, en integreer de JSON‑output in je downstream‑analyse voor een echt end‑to‑end‑oplossing.

---

**Laatst bijgewerkt:** 2026-06-24  
**Getest met:** Aspose.OCR 24.11 for Java  
**Auteur:** Aspose

## Gerelateerde tutorials

- [Hoe de scheefhoek in Java te berekenen met Aspose.OCR](/ocr/java/ocr-basics/calculate-skew-angle/)
- [Hoe afbeeldings‑tekst OCR‑en met taal met Aspose.OCR](/ocr/java/ocr-operations/perform-ocr-language-selection/)
- [OCR van PDF‑documenten herkennen in Aspose.OCR voor Java](/ocr/java/ocr-operations/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}