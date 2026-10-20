---
category: general
date: 2026-03-28
description: Leer hoe je afbeeldings­tekst herkent in Java met Aspose OCR, tekst uit
  PNG‑bestanden extraheert en GPU‑versnelling gebruikt voor snelle OCR van grote afbeeldingen.
draft: false
keywords:
- recognize image text
- extract text png
- use gpu acceleration
- ocr large image
- java ocr example
language: nl
og_description: Ontdek hoe je afbeeldings­tekst herkent in Java, tekst uit png‑bestanden
  extraheert en GPU‑versnelling gebruikt voor OCR van grote afbeeldingen.
og_title: herken afbeeldingstekst met Java OCR – GPU‑versneld voorbeeld
tags:
- OCR
- Java
- GPU
title: herken afbeeldingstekst met Java OCR – GPU‑versneld voorbeeld
url: /nl/java/advanced-ocr-techniques/recognize-image-text-with-java-ocr-gpu-accelerated-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# herken afbeeldingstekst met Java OCR – GPU‑Versnelde Voorbeeld

Heb je ooit **afbeeldingstekst moeten herkennen** uit een enorme PNG en vond je dat de CPU‑versie traag was? Je bent niet de enige. In veel real‑world pipelines—denk aan factuurscanning of archivering van historische documenten—kan de afbeeldingsgrootte enorm worden, en de standaard OCR‑engine kan het simpelweg niet bijhouden.  

Goed nieuws: Aspose OCR voor Java laat je **GPU‑versnelling gebruiken** om het proces een boost te geven, en de code is verrassend compact. In deze tutorial zie je een volledig, uitvoerbaar Java‑OCR‑voorbeeld dat **tekst uit PNG‑bestanden extraheert**, een CUDA‑ondersteunde GPU benut, en een **OCR‑grote‑afbeelding** verwerkt met slechts een paar regels code. Aan het einde weet je precies hoe je dit in je eigen Java‑project kunt integreren en waarom elke instelling belangrijk is.

## Wat je zult leren

- Hoe je Aspose OCR instelt in een Maven‑ of Gradle‑project.  
- Het stap‑voor‑stap proces om **afbeeldingstekst te herkennen** op de GPU.  
- Waarom het configureren van het aantal GPU‑streams de doorvoer kan verbeteren.  
- Hoe je de output verifieert en veelvoorkomende valkuilen oplost.  

> **Prerequisites** – Java 17 (of later), een CUDA‑compatibele GPU met de nieuwste driver, en een geldige Aspose OCR for Java‑licentie (de gratis trial werkt voor evaluatie). Geen andere externe libraries zijn vereist.

---

## Stap 1: Voeg Aspose OCR‑dependency toe

Breng eerst de Aspose OCR‑bibliotheek in je build. Als je **Maven** gebruikt, voeg dan het volgende fragment toe aan je `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- check Maven Central for the latest version -->
</dependency>
```

Voor **Gradle**, plaats dit in `build.gradle`:

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

> **Pro tip:** De nieuwste versie (vanaf maart 2026) bevat prestatie‑verbeteringen voor GPU‑workloads, dus haal altijd de nieuwste release.

---

## Stap 2: Initialise­er de OCR‑engine en schakel GPU in

Het aanmaken van een OCR‑engine is eenvoudig. Het cruciale deel is het inschakelen van de GPU‑vlag—anders valt de engine terug op CPU‑modus.

```java
import com.aspose.ocr.*;

public class GpuExample {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Enable GPU acceleration (requires a CUDA‑enabled GPU and driver)
        ocrEngine.getRecognitionSettings().setUseGpu(true);

        // 3️⃣ (Optional) Set the number of GPU streams for parallel processing
        //    More streams can improve throughput on multi‑core GPUs.
        ocrEngine.getRecognitionSettings().setGpuStreams(2);
```

### Waarom GPU inschakelen?

Wanneer je `setUseGpu(true)` inschakelt, besteedt Aspose de zware convolutionele neurale netwerk‑berekeningen uit aan de grafische kaart. Dit kan seconden schelen bij de verwerkingstijd van een **ocr‑grote‑afbeelding**, vooral wanneer de afbeelding groter is dan 4000 × 4000 px. Als je omgeving geen compatibele GPU heeft, wordt de aanroep simpelweg een no‑op en blijft de engine op de CPU draaien—geen crash, alleen langzamere prestaties.

---

## Stap 3: Herken een PNG‑afbeelding en extraheer de tekst

Wijs nu de engine naar het bestand dat je wilt verwerken. Het voorbeeld gebruikt `sample-large.png`, maar je kunt dit vervangen door elke PNG of JPEG.

```java
        // 4️⃣ Perform OCR on the input image
        OcrResult ocrResult = ocrEngine.recognizeImage("YOUR_DIRECTORY/sample-large.png");

        // 5️⃣ Print the recognized text to the console
        System.out.println("=== Recognized Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

Wanneer je het programma uitvoert, zou je iets moeten zien als:

```
=== Recognized Text ===
Invoice #12345
Date: 2026‑03‑27
Total: $1,234.56
...
```

Die output bevestigt dat de **herken afbeeldingstekst**‑operatie geslaagd is en dat je succesvol **tekst uit png** hebt geëxtraheerd.

---

## Stap 4: Verifieer GPU‑gebruik (optioneel maar nuttig)

Als je benieuwd bent of de GPU echt wordt gebruikt, open dan het GPU‑monitoring‑tool van je systeem (bijv. `nvidia-smi` op Linux). Terwijl het Java‑proces draait, zou je een bescheiden piek in geheugengebruik en compute‑utilisatie moeten zien.

```bash
$ nvidia-smi
+-----------------------------------------------------------------------------+
| Processes:                                                                  |
|  GPU   PID   Type   Process name                  GPU Memory               |
|  0    12345 C++    java                           1024MiB                  |
+-----------------------------------------------------------------------------+
```

Zie je geen activiteit, controleer dan het volgende:

1. De CUDA‑driver komt overeen met het GPU‑model.  
2. De aanroep `setUseGpu(true)` wordt later in de code niet overschreven.  
3. Je licentiebestand (indien aanwezig) beperkt het GPU‑gebruik niet.

---

## Stap 5: Veelvoorkomende randgevallen afhandelen

### Grote afbeeldingen die GPU‑geheugen overschrijden

Wanneer een afbeelding enorm is (bijv. 8000 × 8000 px), kan de GPU zonder geheugen komen te zitten. Een snelle oplossing is de afbeelding te verkleinen voordat je deze aan Aspose doorgeeft:

```java
import java.awt.image.BufferedImage;
import javax.imageio.ImageIO;
import java.io.File;

BufferedImage original = ImageIO.read(new File("sample-large.png"));
int maxDim = 4000; // target max dimension
int width = original.getWidth();
int height = original.getHeight();

float scale = Math.min((float)maxDim / width, (float)maxDim / height);
int newWidth = Math.round(width * scale);
int newHeight = Math.round(height * scale);

BufferedImage resized = new BufferedImage(newWidth, newHeight, original.getType());
// Simple scaling (for demo purposes)
resized.getGraphics().drawImage(original, 0, 0, newWidth, newHeight, null);
ImageIO.write(resized, "png", new File("sample-resized.png"));
```

Geef vervolgens `"sample-resized.png"` door aan `recognizeImage`. Zo blijft de OCR nauwkeurig terwijl je binnen de GPU‑limieten blijft.

### Multi‑page PDF’s

Aspose OCR kan ook PDF‑pagina’s één voor één verwerken. Loop over elke pagina, converteer deze naar een afbeelding, en geef deze aan de engine. Dezelfde **use gpu acceleration**‑vlag geldt, waardoor je een snelle PDF‑naar‑tekst‑pipeline krijgt.

---

## Volledig werkend voorbeeld (Klaar om te kopiëren)

Hieronder staat de complete Java‑klasse, klaar om te compileren en uit te voeren. Vervang `YOUR_DIRECTORY` door het pad naar jouw PNG‑bestand.

```java
import com.aspose.ocr.*;

public class GpuExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Enable GPU acceleration (requires a CUDA‑enabled GPU and driver)
        ocrEngine.getRecognitionSettings().setUseGpu(true);

        // Step 3: (Optional) Set the number of GPU streams for parallel processing
        // Using 2 streams works well on most modern GPUs.
        ocrEngine.getRecognitionSettings().setGpuStreams(2);

        // Step 4: Perform OCR on the input image
        // This will **recognize image text** from a PNG file.
        OcrResult ocrResult = ocrEngine.recognizeImage("YOUR_DIRECTORY/sample-large.png");

        // Step 5: Print the recognized text to the console
        System.out.println("=== Recognized Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

**Verwachte output** – een platte‑tekstweergave van alles wat de engine uit de afbeelding kon lezen. Als de afbeelding een tabel bevat, krijg je de celinhoud achter elkaar met regeleinden; Aspose behoudt de lay‑out niet, maar je kunt de string desgewenst post‑processen.

---

## Veelgestelde vragen

| Vraag | Antwoord |
|----------|--------|
| **Heb ik een betaalde licentie nodig?** | De trial werkt voor maximaal 200 pagina’s en schakelt het watermerk uit voor OCR. Voor productie verwijdert een licentie de limieten en ontgrendelt de volledige GPU‑stack. |
| **Wat als mijn GPU ouder is (bijv. GTX 750)?** | Oudere GPU’s kunnen nog werken, maar met verminderde snelheid; zorg voor minimaal Compute Capability 3.0. |
| **Kan ik JPG‑ of BMP‑bestanden verwerken?** | Absoluut—`recognizeImage` accepteert elk formaat dat door Java ImageIO wordt ondersteund. |
| **Is er een manier om veel afbeeldingen in batch te verwerken?** | Plaats de OCR‑aanroep in een lus, en overweeg `setGpuStreams` te verhogen naar het aantal gelijktijdige streams dat je wilt. |
| **Wat als ik de lay‑out wil behouden?** | Gebruik Aspose OCR’s `LayoutOptions` om begrenzings‑boxen te krijgen; dit valt buiten de scope van deze snelle gids maar staat beschreven in de API‑documentatie. |

---

## Conclusie

Je beschikt nu over een beknopt, end‑to‑end **java ocr voorbeeld** dat **afbeeldingstekst herkent**, **tekst uit png extraheert**, en **GPU‑versnelling** gebruikt om de verwerking van een **ocr‑grote‑afbeelding** te versnellen. Door het aantal GPU‑streams aan te passen en, indien nodig, te verkleinen, kun je de oplossing afstemmen op vrijwel elke hardware‑configuratie.

Klaar voor de volgende stap? Probeer een map met gescande bonnen door dezelfde pipeline te voeren, of experimenteer met Aspose’s `TextRegion`‑API om de oorspronkelijke lay‑out intact te houden. En als je ergens vastloopt, zijn de Aspose‑forums en Javadoc uitstekende bronnen—onthoud gewoon de basisprincipes die we hier hebben behandeld.

Happy coding, en moge je OCR bliksem‑snel zijn!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}