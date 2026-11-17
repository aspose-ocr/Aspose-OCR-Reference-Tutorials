---
category: general
date: 2026-05-06
description: Hoe OCR te gebruiken om tekst uit een afbeelding te extraheren in Java.
  Leer OCR‑afbeelding‑naar‑tekstconversie, corrigeer OCR‑fouten en laad een afbeelding
  voor OCR met Aspose OCR.
draft: false
keywords:
- how to use ocr
- extract text from image
- ocr image to text
- correct ocr errors
- load image for ocr
language: nl
og_description: Hoe OCR in Java te gebruiken om tekst uit een afbeelding te extraheren,
  OCR‑fouten te corrigeren en een afbeelding te laden voor OCR met Aspose OCR.
og_title: Hoe OCR in Java te gebruiken – Complete gids
tags:
- OCR
- Java
- Aspose
title: Hoe OCR in Java te gebruiken – Tekst uit afbeelding halen met spellingscorrectie
url: /nl/java/ocr-operations/how-to-use-ocr-in-java-extract-text-from-image-with-spell-co/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe OCR te gebruiken in Java – Tekst extraheren uit afbeelding met spellingscorrectie

Heb je je ooit afgevraagd **hoe je OCR kunt gebruiken** om een wazige bonfoto om te zetten in schone, doorzoekbare tekst? Je bent niet de enige. In veel projecten—uitgaven‑volgapparaten, factuur‑digitaliseringspijplijnen, of zelfs een snel notitiescript—het verkrijgen van betrouwbare tekst uit een afbeelding is de eerste hindernis.  

Deze tutorial laat je precies zien hoe je OCR in Java gebruikt, van het laden van de afbeelding voor OCR tot het corrigeren van OCR‑fouten zodat het resultaat leest alsof het door een mens is getypt. Aan het einde kun je **tekst uit afbeelding extraheren**, **OCR afbeelding naar tekst** conversie uitvoeren, en veelvoorkomende herkenningsfouten automatisch corrigeren.

## Wat je gaat bouwen

We maken een klein Java console‑programma dat:

1. Laadt een PNG (of elk ondersteund formaat) in de Aspose OCR‑engine.  
2. Schakelt de ingebouwde spell‑correction‑functie in om **OCR‑fouten te corrigeren**.  
3. Voert het herkenningsproces uit en print de opgeschoonde tekst.  

Geen externe services, geen zware frameworks—slechts één JAR en een paar regels code.

### Vereisten

- Java Development Kit (JDK) 8 of nieuwer.  
- Maven (of een ander build‑tool) om de Aspose OCR‑bibliotheek te downloaden.  
- Een afbeeldingsbestand (bijv. `receipt.png`) dat je wilt analyseren.  

Als je de Aspose OCR‑JAR mist, voeg dan deze afhankelijkheid toe aan je `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- use the latest stable version -->
</dependency>
```

> **Pro tip:** De gratis evaluatieversie werkt voor testen, maar een licentie verwijdert het evaluatiewatermerk.

## Stap 1 – Initialise de OCR‑engine (Primaire trefwoord in actie)

Het eerste wat je moet doen is een instantie van `OcrEngine` maken. Beschouw het als het brein dat de pixels leest en ze omzet in tekens.

```java
import com.aspose.ocr.*;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {

        // Initialise the OCR engine – this is where we start using OCR
        OcrEngine ocrEngine = new OcrEngine();
```

*Waarom dit belangrijk is:* Het initialiseren van de engine zet interne bronnen op (taalmodellen, woordenboeken, enz.). Het overslaan van deze stap zou later een `NullPointerException` veroorzaken wanneer je probeert een afbeelding te laden.

## Stap 2 – Afbeelding laden voor OCR

Nu **laden we daadwerkelijk de afbeelding voor OCR**. Aspose biedt een handige `ImageStream.fromFile` helper, maar je kunt ook een `byte[]` gebruiken als je dat liever hebt.

```java
        // Load the image you want to analyse – replace the path with your own file
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/receipt.png"));
```

*Veelvoorkomende valkuil:* Het bestandspad moet absoluut of relatief zijn ten opzichte van de werkmap. Als de afbeelding niet gevonden kan worden, gooit de engine een `IOException`. Controleer het pad nogmaals, vooral bij het uitvoeren vanuit een IDE versus een verpakte JAR.

## Stap 3 – Spell‑correction inschakelen om **OCR‑fouten te corrigeren**

Standaard OCR kan ruisig zijn—denk aan “l0ve” in plaats van “love” of “0” voor “O”. Het inschakelen van spell‑correction vertelt de engine om een post‑processing stap uit te voeren die typische fouten corrigeert.

```java
        // Turn on the spell‑correction feature – this helps to correct OCR errors
        ocrEngine.getSettings().setEnableSpellCorrection(true);
```

*Waarom je dit wilt:* Zonder spell‑correction moet je de output handmatig opschonen, wat het doel van automatisering ondermijnt. Het ingebouwde woordenboek werkt goed voor Engels en verschillende andere talen.

## Stap 4 – De herkenning uitvoeren (**OCR afbeelding naar tekst**)

Met de afbeelding geladen en spell‑correction ingeschakeld, kunnen we de engine eindelijk vragen de tekst te herkennen.

```java
        // Run the OCR process – this converts the image to text
        OcrResult ocrResult = ocrEngine.recognize();
```

*Randgeval:* Als de afbeelding weinig contrast heeft of sterk scheef staat, kan het resultaat nog steeds onzin bevatten. Overweeg pre‑processing (bijv. binarisatie, deskew) voordat je het aan de engine geeft.

## Stap 5 – De opgeschoonde tekst weergeven

De laatste stap is simpelweg het resultaat afdrukken. In een echte applicatie schrijf je het misschien naar een database of een bestand, maar voor deze demo is `System.out` voldoende.

```java
        // Display the corrected text
        System.out.println("Corrected text:");
        System.out.println(ocrResult.getText());
    }
}
```

### Verwachte output

Als we aannemen dat `receipt.png` een duidelijke lijst van items bevat, zie je mogelijk iets als:

```
Corrected text:
Item           Qty   Price
Apple          2     $1.20
Banana         5     $0.75
Total               $5.55
```

Let op hoe “Qty” en “Price” correct gespeld zijn, zelfs als de originele scan een losse “Qy” had.

## Volledig werkend voorbeeld

Hieronder staat het volledige programma dat je kunt kopiëren‑plakken in een bestand genaamd `SpellCorrectDemo.java`. Zorg ervoor dat de Aspose OCR‑JAR op je classpath staat.

```java
import com.aspose.ocr.*;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Initialise the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image you want to process
        // Replace "YOUR_DIRECTORY/receipt.png" with the actual path
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/receipt.png"));

        // Step 3: Enable spell correction to improve accuracy
        ocrEngine.getSettings().setEnableSpellCorrection(true);

        // Step 4: Perform OCR recognition (OCR image to text)
        OcrResult ocrResult = ocrEngine.recognize();

        // Step 5: Output the corrected text
        System.out.println("Corrected text:");
        System.out.println(ocrResult.getText());
    }
}
```

Voer het uit met:

```bash
javac -cp "aspose-ocr-23.9.jar" SpellCorrectDemo.java
java -cp ".:aspose-ocr-23.9.jar" SpellCorrectDemo
```

Je zou nu de opgeschoonde tekst in de console moeten zien verschijnen.

## Bonus: Instellingen aanpassen voor betere nauwkeurigheid

Hoewel de standaardconfiguratie werkt voor de meeste gedrukte documenten, moet je mogelijk een paar parameters aanpassen voor gespecialiseerde scenario's:

| Instelling | Wat het doet | Wanneer te wijzigen |
|------------|--------------|---------------------|
| `setLanguage(OcrLanguage.English)` | Dwingt Engels woordenboek af (vermindert false positives) | Als je afbeelding alleen Engelse tekst bevat. |
| `setResolution(300)` | Geeft de engine de DPI van de bronafbeelding door | Voor scans met hoge resolutie. |
| `setEnableAutoSkewCorrection(true)` | Roteert licht scheve pagina's automatisch | Wanneer afbeeldingen met een telefoon zijn vastgelegd. |

```java
ocrEngine.getSettings().setLanguage(OcrLanguage.English);
ocrEngine.getSettings().setResolution(300);
ocrEngine.getSettings().setEnableAutoSkewCorrection(true);
```

## Veelgestelde vragen

**Q: Werkt dit met PDF’s?**  
A: Ja. Converteer elke PDF‑pagina naar een afbeelding (bijv. met Aspose PDF) en voer de afbeelding in de OCR‑engine.

**Q: Wat als mijn afbeelding in BMP‑formaat is?**  
A: `ImageStream.fromFile` ondersteunt PNG, JPEG, BMP, TIFF en GIF direct. Verander gewoon de bestandsextensie.

**Q: Kan ik spell‑correction uitschakelen?**  
A: Zeker—stel `setEnableSpellCorrection(false)` in als je ruwe OCR‑output nodig hebt voor verdere verwerking.

## Conclusie

Je weet nu **hoe je OCR kunt gebruiken** in Java om **tekst uit afbeelding te extraheren**, automatisch **OCR‑fouten te corrigeren**, en correct **afbeelding te laden voor OCR** met Aspose OCR. De vijf‑stappenstroom—initialiseren, laden, spell‑correction inschakelen, herkennen en output—dekt de meeste alledaagse OCR‑taken.  

Vanaf hier kun je deze logica koppelen aan een database‑schrijfbewerking, een REST‑endpoint, of een batch‑processor om tientallen bonnen tegelijk te verwerken. Experimenteer met de extra instellingen‑tabel hierboven om elke laatste teken van nauwkeurigheid eruit te persen.

Veel plezier met coderen, en moge je OCR‑resultaten altijd schoner zijn dan je met koffie bevlekte bonnen! 

![diagram hoe OCR te gebruiken, toont afbeelding → OCR engine → gecorrigeerde tekststroom]

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}