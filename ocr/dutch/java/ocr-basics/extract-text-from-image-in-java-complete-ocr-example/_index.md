---
category: general
date: 2026-02-19
description: Tekst extraheren uit een afbeelding met Java OCR. Leer een Java OCR‑voorbeeld
  dat een afbeelding laadt voor OCR en tekst uit factuurbestanden haalt in slechts
  een paar stappen.
draft: false
keywords:
- extract text from image
- java ocr example
- load image for ocr
- extract text from invoice
language: nl
og_description: Tekst extraheren uit afbeelding met Java OCR. Deze gids laat zien
  hoe je een afbeelding laadt voor OCR en tekst uit facturen haalt met een eenvoudig
  Java OCR‑voorbeeld.
og_title: Tekst uit afbeelding extraheren in Java – Volledig OCR‑voorbeeld
tags:
- OCR
- Java
- Aspose
- Image Processing
title: Tekst uit afbeelding extraheren in Java – Volledig OCR‑voorbeeld
url: /nl/java/ocr-basics/extract-text-from-image-in-java-complete-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tekst uit afbeelding extraheren in Java – Volledig OCR‑voorbeeld

Heb je ooit **tekst uit een afbeelding** moeten halen, maar wist je niet welke bibliotheek je moest kiezen? Je bent niet de enige—veel ontwikkelaars lopen tegen dit obstakel aan bij het automatiseren van factuurverwerking of het bouwen van doorzoekbare archieven. Het goede nieuws? Met een paar regels Java kun je een afbeelding laden voor OCR, een interessegebied definiëren en de exacte tekst ophalen die je nodig hebt.  

In deze tutorial lopen we een **java ocr example** door die precies laat zien hoe je **image for OCR** laadt, een ROI instelt en **text from invoice** bestanden extraheert met Aspose.OCR. Aan het einde heb je een uitvoerbaar programma dat je in elk Java‑project kunt plaatsen.

## Wat je gaat leren

- Hoe je een `OcrEngine`‑instantie maakt en waarom dat belangrijk is.  
- De juiste manier om **image for OCR** te **loaden** met Aspose’s `ImageStream`.  
- Het instellen van een **region of interest (ROI)** zodat je alleen het deel van de afbeelding verwerkt dat het factuurtotaal bevat.  
- Het extraheren van de herkende tekst en deze naar de console printen.  
- Veelvoorkomende valkuilen (bijv. verkeerde rechthoek‑coördinaten) en snelle oplossingen.

**Prerequisites**

- Java 8 of nieuwer geïnstalleerd.  
- Maven of Gradle om de Aspose.OCR‑bibliotheek (`com.aspose:aspose-ocr`) te downloaden.  
- Een voorbeeld‑factuurafbeelding (`invoice.png`) geplaatst in een bekende map.

Alles klaar? Geweldig—laten we beginnen.

![Extract text from image using Java OCR](/images/extract-text-from-image-java.png "extract text from image example")

## Tekst uit afbeelding extraheren – Stap‑voor‑stap Java OCR‑voorbeeld

Hieronder staat de volledige broncode. Voel je vrij om deze te copy‑pasten in `RoiOcrExample.java` en direct uit te voeren.

```java
import com.aspose.ocr.*;

public class RoiOcrExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance.
        // The engine holds all configuration and performs the heavy lifting.
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the source image.
        // You can point to any PNG, JPG, or TIFF file. Here we use a sample invoice.
        String imagePath = "YOUR_DIRECTORY/invoice.png";
        ocrEngine.setImage(ImageStream.fromFile(imagePath));

        // Step 3: Define the region of interest (ROI) you want to recognize.
        // x = 120, y = 340, width = 500, height = 120 – tweak these values for your own layout.
        Rectangle regionOfInterest = new Rectangle(120, 340, 500, 120);
        ocrEngine.setRegionOfInterest(regionOfInterest);

        // Step 4: Perform OCR on the specified ROI and retrieve the text.
        // recognize() returns an OcrResult object; getText() extracts the plain string.
        String extractedText = ocrEngine.recognize().getText();

        // Step 5: Output the recognized text.
        System.out.println("ROI text: " + extractedText);
    }
}
```

### Waarom elke stap belangrijk is

1. **Creating the OCR engine** – zonder een engine is er geen context voor beeldverwerking. Het object stelt je later ook in staat om taalpakketten aan te passen als je multi‑language support nodig hebt.  
2. **Loading the image** – `ImageStream.fromFile` abstraheert het bestandsformaat, zodat de engine de bytes correct kan lezen. Als je dit overslaat, krijg je een `NullPointerException`.  
3. **Setting the ROI** – het verwerken van de hele pagina kan onnodig veel tijd kosten. Door de rechthoek te beperken tot het gebied van het factuurtotaal, versnel je de herkenning en verminder je ruis.  
4. **Calling `recognize()`** – hier gebeurt de magie. De methode voert het OCR‑algoritme uit over de ROI en levert een result‑object op.  
5. **Printing the output** – in echte projecten sla je de tekst waarschijnlijk op in een database, maar `System.out.println` is perfect voor een snelle demo.

## Load Image for OCR

Vraag je je af of het pad absoluut of relatief moet zijn? Beide werken—zorg er alleen voor dat het Java‑proces het bestand kan lezen. Op Windows moeten backslashes worden geescaped (`C:\\images\\invoice.png`) of je kunt forward slashes gebruiken (`C:/images/invoice.png`).  

**Pro tip:** Als je veel facturen in een lus verwerkt, hergebruik dan dezelfde `OcrEngine`‑instantie; deze cachet interne resources en verbetert de doorvoersnelheid.

## Define Region of Interest (ROI)

Het juiste rechthoek kiezen is vaak een kwestie van trial‑and‑error. Een handige manier om de coördinaten te vinden is de afbeelding te openen in een grafische editor (zoals GIMP of Paint.NET) en met de muis over het gebied te bewegen—de X/Y‑waarden verschijnen in de statusbalk.  

Edge case: sommige facturen hebben variabele lay‑outs. In dat scenario kun je eerst een snelle pre‑scan over de hele afbeelding uitvoeren, sleutelwoorden zoals “Total:” zoeken met een regex, en vervolgens de ROI dynamisch aanpassen.

## Perform OCR and Get Text

De `recognize()`‑aanroep is synchroon—je thread blokkeert tot de engine klaar is. Voor grote batches kun je een thread‑pool gebruiken en afbeeldingen parallel verwerken. Vergeet niet dat elke thread zijn eigen `OcrEngine`‑instantie nodig heeft; ze zijn niet thread‑safe.

## Run and Verify Output

Compileer en voer uit:

```bash
javac -cp "path/to/aspose-ocr.jar" RoiOcrExample.java
java -cp ".:path/to/aspose-ocr.jar" RoiOcrExample
```

Je zou iets moeten zien als:

```
ROI text: $1,254.00
```

Als de output er onleesbaar uitziet, controleer dan de ROI‑coördinaten en zorg dat de afbeelding van hoge kwaliteit is (300 dpi of hoger werkt het beste).  

### Common Pitfalls & How to Fix Them

| Symptom | Likely Cause | Fix |
|---------|--------------|-----|
| Empty string | ROI outside image bounds | Verify rectangle values against image dimensions |
| Misspelled words | Low resolution | Use a higher‑resolution source or apply image preprocessing (e.g., binarization) |
| `java.lang.NoClassDefFoundError` | Missing Aspose JAR on classpath | Add `aspose-ocr.jar` to `-cp` or use Maven/Gradle dependency management |

## Conclusion

Je weet nu hoe je **text from image** kunt **extract** in Java met een beknopt **java ocr example**. Door de afbeelding correct te laden, een gerichte ROI te definiëren en `recognize()` aan te roepen, kun je betrouwbaar **text from invoice** bestanden extraheren en die data doorsturen naar downstream‑systemen.

Wat nu? Probeer de ROI te vervangen door andere velden (datum, leveranciersnaam), experimenteer met taalpakketten voor meertalige facturen, of integreer de OCR‑stap in een Spring Boot‑microservice. Hetzelfde patroon werkt voor kassabonnen, paspoorten of elk document waarbij je precieze tekstextractie nodig hebt.

Heb je vragen over het schalen van deze oplossing of over het omgaan met ruisvolle scans? Laat dan een reactie achter—happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}