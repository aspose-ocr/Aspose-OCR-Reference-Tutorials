---
category: general
date: 2026-02-14
description: Tekst uit afbeelding extraheren met Aspose OCR in Java. Leer hoe je tekst
  uit formuliervelden met interessegebieden kunt extraheren voor nauwkeurige resultaten.
draft: false
keywords:
- extract text from image
- extract text from form
language: nl
og_description: Tekst extraheren uit afbeelding met Aspose OCR in Java. Deze tutorial
  laat zien hoe je tekst uit formuliervelden kunt extraheren via interessegebieden.
og_title: Tekst uit afbeelding extraheren met Aspose OCR – Java‑gids
tags:
- OCR
- Java
- Aspose
- Image Processing
title: Tekst extraheren uit afbeelding met Aspose OCR – Java-gids
url: /nl/java/advanced-ocr-techniques/extract-text-from-image-with-aspose-ocr-java-guide/
---

markdown formatting.

Now produce final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tekst extraheren uit afbeelding met Aspose OCR – Java-gids

Heb je ooit **tekst uit afbeelding te extraheren** maar eindigde je met het doorzoeken van de hele foto, waardoor je CPU-cycli verspilde en ruisende resultaten kreeg? Je bent niet de enige. In veel real‑world apps—denk aan factuurscanners, paspoortlezers of gegevensinvoervelden—geef je alleen om een handvol velden, niet om het volledige canvas.  

Het goede nieuws is dat Aspose OCR je in staat stelt **tekst uit afbeelding te extraheren** *en* uit specifieke formuliergebieden door polygonen te definiëren. In deze tutorial zie je precies hoe je **tekst uit formulier** velden kunt extraheren met Java, waarom de aanpak belangrijk is, en wat je moet aanpassen wanneer er iets misgaat.

Hieronder behandelen we alles, van het instellen van de bibliotheek tot het afhandelen van lastige randgevallen, zodat je aan het einde een kant‑klaar fragment hebt dat alleen de gegevens haalt die je nodig hebt.

## Wat je nodig hebt

- Java 17 (of een recente JDK) – nieuwere versies hebben betere Unicode-ondersteuning.  
- Aspose.OCR for Java 23.10 (of de nieuwste versie op het moment van lezen).  
- Een voorbeeldafbeelding genaamd `form.png` met duidelijk gedefinieerde velden.  
- Een IDE of eenvoudige teksteditor—IntelliJ IDEA, VS Code, of zelfs Notepad volstaat.

Geen Maven/Gradle tovenarij nodig voor de kern‑demo; voeg gewoon de Aspose OCR JAR toe aan je classpath.

---

## Stap 1 – Initialiseer de OCR‑engine en laad je afbeelding

Het eerste wat de engine nodig heeft is een bitmap om op te werken. We wijzen hem naar `form.png`, die zich in dezelfde map bevindt als het bronbestand.

```java
import com.aspose.ocr.*;
import java.awt.Polygon;
import java.util.*;

public class MultiRoiDemo {
    public static void main(String[] args) throws Exception {

        // Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Load the source image – replace the path if your file lives elsewhere
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/form.png"));
```

*Waarom dit belangrijk is:*  
Het maken van een nieuwe `OcrEngine` geeft je een schone lei, waardoor geen overgebleven instellingen je uitvoering beïnvloeden. Het vroeg laden van de afbeelding valideert ook dat het bestand bestaat, zodat je een nuttige uitzondering krijgt voordat je tijd verspilt aan latere stappen.

> **Pro tip:** Als je afbeelding enorm is (meer dan 5 MB), overweeg dan eerst te schalen. Aspose OCR werkt sneller op afbeeldingen onder 2000 px in beide dimensies.

---

## Stap 2 – Definieer polygonen voor de velden die je wilt lezen

Een *Region of Interest* (ROI) is simpelweg een polygoon die de engine vertelt waar te zoeken. Hieronder maken we twee rechthoeken—een voor “First Name” en een andere voor “Date of Birth”. Pas de coördinaten aan zodat ze bij jouw eigen formulier passen.

```java
        // Polygon for the first field (e.g., First Name)
        Polygon firstField = new Polygon(
                new int[]{50, 200, 200, 50},   // X‑coordinates
                new int[]{100, 100, 150, 150}, // Y‑coordinates
                4);

        // Polygon for the second field (e.g., Date of Birth)
        Polygon secondField = new Polygon(
                new int[]{300, 500, 500, 300},
                new int[]{200, 200, 250, 250},
                4);
```

*Waarom polygonen in plaats van rechthoeken?*  
Polygonen geven je de flexibiliteit om scheve of niet‑rechthoekige vakken te verwerken—veelvoorkomend bij het scannen van afgedrukte formulieren die niet perfect uitgelijnd zijn.

---

## Stap 3 – Laat Aspose OCR zich alleen op die regio's richten

Nu koppelen we de polygonen aan de engine. De `setRegionsOfInterest`‑methode accepteert een lijst, zodat je zoveel velden kunt toevoegen als je wilt.

```java
        // Limit OCR to the defined regions
        ocrEngine.getEngineOptions()
                 .setRegionsOfInterest(Arrays.asList(firstField, secondField));
```

*Wat er onder de motorkap gebeurt?*  
Aspose OCR snijdt elke polygoon bij tot een aparte bitmap, voert zijn herkenningsalgoritme uit en voegt vervolgens de resultaten samen. Dit vermindert valse positieven van omliggende graphics drastisch.

---

## Stap 4 – Voer het OCR‑proces uit

Met alles geconfigureerd starten we de OCR. De `process()`‑aanroep retourneert een `OcrResult`‑object dat de geëxtraheerde tekst en vertrouwensscores bevat.

```java
        // Execute OCR on the selected ROIs
        OcrResult ocrResult = ocrEngine.process();
```

Als je per‑veld vertrouwen nodig hebt, kun je `ocrResult.getRegions()` inspecteren—elke regio draagt zijn eigen score. Voor de meeste eenvoudige formulieren is de algemene tekst voldoende.

---

## Stap 5 – Toon (of sla) de geëxtraheerde tekst op

Tot slot printen we het resultaat naar de console. In een echte applicatie zou je het naar een database, JSON‑bestand kunnen schrijven of via een API verzenden.

```java
        // Output the extracted text
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

**Verwachte output (voorbeeld):**

```
=== Extracted Text ===
John Doe
12/04/1990
```

De twee regels komen overeen met de twee polygonen die we hebben gedefinieerd. Als je extra witruimte ziet, verwijder deze dan met `String.trim()`.

---

## Hoe tekst uit een formulier te extraheren wanneer je veel velden hebt

Wanneer een formulier tientallen invoervelden bevat, wordt het handmatig intypen van coördinaten vervelend. Hier is een snel patroon dat je kunt gebruiken:

1. **Maak een CSV** waarin elke rij `fieldName, x1, y1, x2, y2, x3, y3, x4, y4` bevat.  
2. **Laad de CSV** tijdens runtime, loop door elke regel, bouw een `Polygon` en voeg deze toe aan de ROI‑lijst.  

```java
List<Polygon> rois = new ArrayList<>();
try (BufferedReader br = new BufferedReader(new FileReader("fields.csv"))) {
    String line;
    while ((line = br.readLine()) != null) {
        String[] parts = line.split(",");
        int[] xs = { Integer.parseInt(parts[1]), Integer.parseInt(parts[3]),
                    Integer.parseInt(parts[5]), Integer.parseInt(parts[7]) };
        int[] ys = { Integer.parseInt(parts[2]), Integer.parseInt(parts[4]),
                    Integer.parseInt(parts[6]), Integer.parseInt(parts[8]) };
        rois.add(new Polygon(xs, ys, 4));
    }
}
ocrEngine.getEngineOptions().setRegionsOfInterest(rois);
```

*Waarom de moeite nemen?*  
Het automatiseren van ROI‑generatie stelt je in staat dezelfde Java‑code te hergebruiken voor meerdere formulierlay-outs, waardoor je project DRY (Don’t Repeat Yourself) blijft.

---

## Randgevallen & Tips waar je misschien niet aan gedacht hebt

- **Gedraaide scans:** Als de hele afbeelding gedraaid is, roep dan `ocrEngine.getEngineOptions().setRotateAngle(degrees)` aan.  
- **Lage contrast:** Stel `ocrEngine.getEngineOptions().setContrast(1.5f)` in om de leesbaarheid te verbeteren.  
- **Niet‑Latijnse scripts:** Wissel de taal met `ocrEngine.getEngineOptions().setLanguage(OcrLanguage.Spanish)` (of een andere ondersteunde taal).  
- **Gedeeltelijke OCR‑fouten:** Controleer altijd `ocrResult.getConfidence()`; als deze onder 80 % valt, overweeg dan de gebruiker om handmatige verificatie te vragen.  

---

## Volledig werkend voorbeeld (Klaar om te kopiëren‑plakken)

Hieronder staat het volledige programma, klaar om te compileren en uit te voeren. Vervang `YOUR_DIRECTORY` door de map die `form.png` bevat.

```java
import com.aspose.ocr.*;
import java.awt.Polygon;
import java.util.*;

public class MultiRoiDemo {
    public static void main(String[] args) throws Exception {

        // Step 1 – Initialize engine and load image
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/form.png"));

        // Step 2 – Define polygons for each form field
        Polygon firstField = new Polygon(
                new int[]{50, 200, 200, 50},
                new int[]{100, 100, 150, 150},
                4);
        Polygon secondField = new Polygon(
                new int[]{300, 500, 500, 300},
                new int[]{200, 200, 250, 250},
                4);

        // Step 3 – Limit OCR to those regions
        ocrEngine.getEngineOptions()
                 .setRegionsOfInterest(Arrays.asList(firstField, secondField));

        // Step 4 – Run OCR
        OcrResult ocrResult = ocrEngine.process();

        // Step 5 – Show the result
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

Compileer met:

```bash
javac -cp "aspose-ocr-23.10.jar" MultiRoiDemo.java
java -cp ".:aspose-ocr-23.10.jar" MultiRoiDemo
```

Je zou de twee regels tekst moeten zien die bij de gedefinieerde ROI's horen.

---

## Veelgestelde vragen

**Q: Werkt dit met PDF's?**  
A: Niet direct. Converteer elke PDF‑pagina eerst naar een afbeelding (bijv. met Aspose PDF) en voer vervolgens de afbeelding in de OCR‑engine.

**Q: Wat als mijn formulier selectievakjes heeft?**  
A: OCR kan geen booleaanse toestanden lezen, maar je kunt het gebied van het selectievakje als een ROI behandelen en de pixeldichtheid inspecteren om een vinkje af te leiden.

**Q: Kan ik tekst uit een meer‑pagina formulier in één keer extraheren?**  
A: Loop over elke paginabeeld, hergebruik dezelfde ROI‑lijst en concateneer de resultaten.

---

## Conclusie

We hebben een volledige, end‑to‑end oplossing doorgenomen voor **tekst uit afbeelding extraheren** met Aspose OCR, en laten zien hoe dezelfde techniek je **tekst uit formulier** velden met nauwkeurige precisie laat extraheren. Door polygonen te definiëren, de focus van de engine te beperken en veelvoorkomende valkuilen af te handelen, krijg je snelle, schone data zonder de overhead van het verwerken van de volledige afbeelding.

Klaar voor de volgende stap? Probeer deze OCR‑output te koppelen aan een JSON‑payload, of voer het in een machine‑learning‑model voor validatie. De mogelijkheden zijn eindeloos, en nu jij

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}