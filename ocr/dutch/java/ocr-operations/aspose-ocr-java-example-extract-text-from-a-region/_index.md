---
category: general
date: 2026-05-03
description: Het Aspose OCR Java‑voorbeeld toont hoe je een afbeelding laadt voor
  OCR en tekst uit een gebied extraheert in slechts een paar regels code.
draft: false
keywords:
- aspose ocr java example
- load image for OCR
- extract text from region
language: nl
og_description: Aspose OCR Java‑voorbeeld toont het laden van een afbeelding voor
  OCR en het extraheren van tekst uit een specifiek gebied, perfect voor factuurverwerking.
og_title: Aspose OCR Java-voorbeeld – Regio‑tekstextractie
tags:
- Aspose OCR
- Java
- Image Processing
title: 'Aspose OCR Java-voorbeeld: Tekst uit een regio extraheren'
url: /nl/java/ocr-operations/aspose-ocr-java-example-extract-text-from-a-region/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR Java-voorbeeld: Tekst extraheren uit een regio

Zoek je een **Aspose OCR Java example** die je alleen het deel laat ophalen dat je nodig hebt uit een afbeelding? In deze gids lopen we **een afbeelding laden voor OCR** en **tekst extraheren uit een regio** door, perfect voor factuurnummers, formuliervelden, of elk stukje data dat zich verstopt in een grotere afbeelding.

Je vraagt je misschien af waarom je OCR zou beperken tot een rechthoek in plaats van de hele pagina te scannen. Het korte antwoord: snelheid en nauwkeurigheid. Wanneer de engine alleen naar een gedefinieerd deel kijkt, slaat hij irrelevante ruis over, werkt sneller en levert vaak schonere resultaten op. Aan het einde van deze tutorial heb je een zelfstandige Java‑programma dat precies dat doet, plus een reeks tips om de veelvoorkomende valkuilen te vermijden die nieuwkomers tegenkomen.

## Wat je nodig hebt

- **Java Development Kit (JDK) 11** of nieuwer geïnstalleerd.
- **Aspose.OCR for Java** bibliotheek (je kunt de nieuwste JAR halen van de Maven Central repository of het Aspose‑downloadportaal).
- Een afbeeldingsbestand dat de tekst bevat die je wilt lezen – voor onze demo gebruiken we `invoice.png`, dat ergens in de rechter‑bovenhoek een factuurnummer bevat.
- Een favoriete IDE of een eenvoudige teksteditor plus een terminal; elk build‑tool (Maven, Gradle, of gewone `javac`) volstaat.

Dat is alles. Geen extra OCR‑engines, geen native binaries, alleen pure Java en Aspose.

![Aspose OCR Java voorbeeld screenshot](/images/aspose-ocr-java-example.png "Aspose OCR Java voorbeeld toont regio-extractie")

## Aspose OCR Java-voorbeeld – Initialiseer de OCR-engine

Het eerste wat elke OCR‑workflow nodig heeft, is een engine‑instance. Aspose levert een lichtgewicht `OcrEngine`‑klasse die alles afhandelt, van het laden van afbeeldingen tot het selecteren van talen.

```java
import com.aspose.ocr.*;

public class RegionOcrExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();
```

**Waarom dit belangrijk is:** Door de engine van tevoren te maken, krijg je een schoon object om te configureren. Je kunt dezelfde `OcrEngine` hergebruiken voor meerdere afbeeldingen als je een batch verwerkt, wat geheugen en initialisatietijd bespaart.

## Afbeelding laden voor OCR

Vervolgens vertellen we de engine welke afbeelding hij moet scannen. Aspose biedt de helper `ImageStream.fromFile`, die de low‑level `FileInputStream`‑boilerplate abstraheert.

```java
        // Step 2: Load the image that contains the invoice
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/invoice.png"));
```

**Tip:** Vervang `YOUR_DIRECTORY` door een absoluut pad of een relatief pad dat verwijst naar de locatie waar je `invoice.png` hebt opgeslagen. Als het bestand niet gevonden kan worden, gooit Aspose een `IOException`, dus je wilt dit wellicht in een try‑catch‑blok wikkelen voor productiecodel.

## Definieer en extraheren tekst uit een regio

Nu komt de ster van de show: het rechthoekige gebied dat de engine vertelt waar te zoeken. De constructor van `java.awt.Rectangle` neemt `(x, y, width, height)` – allemaal gemeten in pixels.

```java
        // Step 3: Define the region where the invoice number is located (x, y, width, height)
        java.awt.Rectangle invoiceRegion = new java.awt.Rectangle(120, 250, 300, 80);
        ocrEngine.setRegion(invoiceRegion);   // restrict recognition to this area
```

**Hoe het werkt:** Door `setRegion` aan te roepen, beperk je de OCR‑scan tot een 300‑pixel‑brede slice die 120 pixels vanaf de linkerkant en 250 pixels vanaf de bovenkant begint. Pas deze getallen aan om bij jouw lay‑out te passen; een snelle manier om ze te vinden is de afbeelding te openen in een grafische editor die pixelcoördinaten toont.

## Taal inschakelen en herkenning uitvoeren

Aspose OCR ondersteunt tientallen talen, maar voor een factuurnummer hebben we alleen Engels nodig. Het inschakelen van de juiste taal vermindert valse positieven drastisch.

```java
        // Step 4: Enable English language for recognition
        ocrEngine.getLanguage().setEnglish(true);

        // Step 5: Perform recognition and output the extracted text
        if (ocrEngine.recognize()) {
            System.out.println("Extracted region text: " + ocrEngine.getText());
        } else {
            System.err.println("OCR recognition failed.");
        }
    }
}
```

**Waarom alleen Engels inschakelen?** De OCR‑engine probeert tekens te matchen uit elke ingeschakelde taalset, wat verwarring kan veroorzaken wanneer de tekst eenvoudige alfanumerieke tekens bevat. Het beperken van de taalkeuze verbetert zowel snelheid als precisie.

### Verwachte output

Wanneer alles goed is afgestemd, zie je iets als:

```
Extracted region text: INV-12345
```

Als het rechthoekige gebied een paar pixels verschoven is, kan de output onsamenhangend of leeg zijn. Dat is een eenvoudige sanity‑check: voer het programma uit, kijk naar de console, en controleer of de tekst overeenkomt met wat je in de afbeelding ziet.

## Voer de code uit en controleer de output

Als je Maven gebruikt, voeg dan de Aspose OCR‑dependency toe aan je `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- Use the latest version available -->
</dependency>
```

Compileer en voer uit:

```bash
mvn compile exec:java -Dexec.mainClass=RegionOcrExample
```

Of, als je liever gewone `javac` gebruikt:

```bash
javac -cp "aspose-ocr-23.10.jar" RegionOcrExample.java
java -cp ".:aspose-ocr-23.10.jar" RegionOcrExample
```

Je zou de regel **Extracted region text** in de console moeten zien verschijnen. Als je “OCR recognition failed” krijgt, controleer dan het bestandspad en zorg ervoor dat het gebied daadwerkelijk leesbare tekens bevat.

## Randgevallen & Veelvoorkomende variaties

| Situatie | Wat te wijzigen |
|-----------|----------------|
| **Meerdere talen** (bijv. Engels + Spaans) | Roep `ocrEngine.getLanguage().setSpanish(true);` aan naast Engels. |
| **Regio buiten afbeeldingsgrenzen** | Aspose zal het rechthoekje stilletjes bijsnijden, maar je verliest data. Gebruik `ImageInfo` (`ocrEngine.getImage().getWidth()`) om de afmetingen te verifiëren voordat je de regio instelt. |
| **Dynamische facturen** (verschillende lay‑outs) | Overweeg een lichte pre‑scan van de hele afbeelding om trefwoorden zoals “Invoice #” te vinden en bereken vervolgens het rechthoekje programmatisch. |
| **Afbeeldingen met hogere DPI** | Verhoog `ocrEngine.getImage().setResolution(300);` voor betere nauwkeurigheid bij gescande documenten. |
| **Prestatie‑optimalisatie** | Schakel onnodige talen uit, houd de regio zo klein mogelijk, en hergebruik één enkele `OcrEngine`‑instance voor veel bestanden. |

## Pro‑tips uit de praktijk

- **Pro tip:** Als je alleen cijfers nodig hebt (gebruikelijk voor factuurnummers), schakel de numerieke modus in met `ocrEngine.getLanguage().setDigits(true);`. Dit elimineert alfabetische ruis.
- **Let op:** Transparante PNG’s. Aspose interpreteert soms het alfakanaal verkeerd; het converteren van de afbeelding naar een JPEG met een effen achtergrond kan vreemde lege outputs oplossen.
- **Onthoud:** Het rechthoekje gebruikt het native coördinatensysteem van de afbeelding, niet de UI‑schaling die je op het scherm ziet. Test altijd met exact het bestand dat je in productie gaat verwerken.

## Wat is het volgende?

Nu je een solide **Aspose OCR Java example** hebt voor regio‑gebaseerde extractie, kun je het in verschillende nuttige richtingen uitbreiden:

- **Batchverwerking:** Loop over een map met facturen en hergebruik dezelfde `OcrEngine` om de doorvoersnelheid te verhogen.
- **Gegevensvalidatie:** Stuur de geëxtraheerde tekst door een regex zoals `INV-\\d{5}` om te verzekeren dat je een geldig factuurnummer hebt vastgelegd.
- **Integratie met PDF:** Gebruik Aspose.PDF om de geëxtraheerde tekst terug over de originele document te leggen voor audit‑trails.
- **Cloud‑implementatie:** Verpak de code in een lichte REST‑service (Spring Boot) zodat andere systemen er op aanvraag gebruik van kunnen maken.

Elk van deze stappen maakt gebruik van dezelfde kernconcepten — **afbeelding laden voor OCR**, **tekst extraheren uit een regio**, en de resultaten verwerken — zodat de overgang moeiteloos zal verlopen.

---

*Happy coding! Als je ergens vastloopt, laat dan een reactie achter of bekijk de Aspose‑forums waar de community real‑world tweaks deelt voor lastige lay‑outs.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}