---
category: general
date: 2026-02-22
description: Leer hoe je GPU inschakelt in Java OCR om tekst uit een afbeelding te
  herkennen en snel tekst uit een factuur te extraheren met Aspose OCR.
draft: false
keywords:
- how to enable gpu
- recognize text from image
- extract text from invoice
- java ocr example
- load image for ocr
language: nl
og_description: Hoe GPU in Java OCR in te schakelen, tekst uit een afbeelding te herkennen
  en tekst uit een factuur te extraheren met een compleet Java OCR‑voorbeeld.
og_title: Hoe GPU voor Java OCR in te schakelen – Snelle gids
tags:
- Java
- OCR
- GPU
- Aspose
title: Hoe GPU voor Java OCR in te schakelen – Tekst uit afbeelding herkennen
url: /nl/java/advanced-ocr-techniques/how-to-enable-gpu-for-java-ocr-recognize-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe GPU in te schakelen voor Java OCR – Tekst herkennen uit afbeelding

Heb je je ooit afgevraagd **hoe je GPU kunt inschakelen** bij het doen van OCR in Java? Je bent niet de enige—veel ontwikkelaars lopen tegen een prestatiewaarde aan bij het verwerken van grote, hoge‑resolutie documenten zoals facturen. Het goede nieuws? Met Aspose OCR kun je één enkele schakelaar omzetten en de grafische kaart het zware werk laten doen. In deze tutorial lopen we door een **java ocr voorbeeld** dat een afbeelding laadt, GPU‑verwerking inschakelt, en de tekst van een factuur in een oogwenk extraheert.

We behandelen alles, van het installeren van de bibliotheek tot het afhandelen van randgevallen zoals ontbrekende GPU‑stuurprogramma's. Aan het einde kun je **tekst herkennen uit afbeelding** bestanden direct, en heb je een solide sjabloon voor toekomstige OCR‑projecten. Geen externe referenties nodig—alleen pure, uitvoerbare code.

## Vereisten

- **Java Development Kit (JDK) 11** of nieuwer geïnstalleerd op je machine.  
- **Maven** (of Gradle) voor afhankelijkheidsbeheer.  
- Een **GPU‑capable system** met up‑to‑date drivers (NVIDIA, AMD, of Intel).  
- Een afbeeldingsbestand van een factuur (bijv. `large_invoice_300dpi.png`).  

Als je een van deze mist, regel ze dan eerst; de rest van de gids gaat ervan uit dat ze aanwezig zijn.

## Stap 1: Voeg Aspose OCR toe aan je project

Het eerste wat we nodig hebben is de Aspose OCR bibliotheek. Met Maven plaats je simpelweg het volgende fragment in je `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- Use the latest version available -->
</dependency>
```

> **Pro tip:** Het versienummer verandert regelmatig; controleer Maven Central voor de nieuwste release om up‑to‑date te blijven.

Als je de voorkeur geeft aan Gradle, is het equivalent:

```groovy
implementation 'com.aspose:aspose-ocr:23.10'
```

Zodra de afhankelijkheid is opgelost, ben je klaar om code te schrijven die met de OCR‑engine communiceert.

## Stap 2: Hoe GPU in te schakelen in de Aspose OCR Engine

Nu komt de ster van de show—GPU‑verwerking inschakelen. Aspose OCR biedt drie verwerkingsmodi:

| Mode | Beschrijving |
|------|-------------|
| `CPU_ONLY` | Pure CPU, veilig voor elke machine. |
| `GPU_ONLY` | Dwingt GPU af, faalt als er geen compatibel apparaat is. |
| `AUTO_GPU` | Detecteert een GPU en gebruikt deze wanneer beschikbaar, anders valt terug op CPU. |

Voor de meeste scenario's raden we **`AUTO_GPU`** aan omdat het het beste van beide werelden biedt. Zo schakel je het in:

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 2.1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2.2: Enable GPU processing (AUTO_GPU uses GPU when available)
        ocrEngine.setProcessingMode(OcrEngine.ProcessingMode.AUTO_GPU);

        // The rest of the steps follow...
    }
}
```

> **Waarom dit belangrijk is:** Het inschakelen van GPU kan de verwerkingstijd voor een 300 dpi factuur verkorten van meerdere seconden tot onder een seconde, afhankelijk van je hardware.

## Stap 3: Afbeelding laden voor OCR – Tekst herkennen uit afbeelding

Voordat de engine iets kan lezen, moet je hem een afbeelding geven. De `OcrInput`‑klasse van Aspose OCR accepteert bestandspaden, streams, of zelfs `BufferedImage`‑objecten. Voor de eenvoud gebruiken we een bestandspad:

```java
// Step 3.1: Prepare the input image
OcrInput ocrInput = new OcrInput();
ocrInput.add("YOUR_DIRECTORY/large_invoice_300dpi.png"); // <-- replace with your actual path
```

> **Randgeval:** Als de afbeelding groter is dan 5 MB, overweeg dan eerst te down‑samplen om out‑of‑memory fouten op de GPU te voorkomen.

## Stap 4: OCR uitvoeren en tekst uit factuur extraheren

Nu vragen we de engine om zijn magie te doen. De `recognize`‑methode retourneert een `OcrResult`‑object dat de geëxtraheerde tekst, vertrouwensscores en lay‑outinformatie bevat.

```java
// Step 4.1: Run the recognition
OcrResult ocrResult = ocrEngine.recognize(ocrInput);

// Step 4.2: Print the extracted text to console
System.out.println("=== Extracted Text ===");
System.out.println(ocrResult.getText());
```

Wanneer je het programma uitvoert, zou je iets moeten zien als:

```
=== Extracted Text ===
Invoice #12345
Date: 2026-02-20
Total: $1,245.67
...
```

Als de output er rommelig uitziet, controleer dan dubbel of de afbeelding duidelijk is en of de OCR‑taal correct is ingesteld (Aspose standaard op Engels, maar je kunt dit wijzigen via `ocrEngine.setLanguage(OcrEngine.Language.SPANISH)` enz.).

## Stap 5: Volledig werkend voorbeeld (Klaar om te kopiëren‑plakken)

Hieronder staat de volledige, zelfstandige Java‑klasse. Plak deze in je IDE, pas het afbeeldingspad aan, en druk op **Run**.

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Create OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Enable GPU (auto‑detect)
        ocrEngine.setProcessingMode(OcrEngine.ProcessingMode.AUTO_GPU);

        // 3️⃣ Load the image you want to process
        OcrInput ocrInput = new OcrInput();
        // 👉 Replace with the absolute or relative path to your invoice image
        ocrInput.add("YOUR_DIRECTORY/large_invoice_300dpi.png");

        // 4️⃣ Run OCR
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);

        // 5️⃣ Output the text
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

### Verwachte output

Het uitvoeren van de code op een duidelijke 300 dpi factuur levert doorgaans een platte‑tekst weergave op van elke regel in het document. De exacte output hangt af van de factuurlay‑out, maar je zult velden zien zoals *Invoice Number*, *Date*, *Total Amount*, en beschrijvingen van regelitems.

## Veelvoorkomende valkuilen & hoe ze op te lossen

| Symptoom | Waarschijnlijke oorzaak | Oplossing |
|----------|--------------------------|----------|
| **`java.lang.UnsatisfiedLinkError`** | GPU‑stuurprogramma ontbreekt of is incompatibel | Installeer het nieuwste stuurprogramma van NVIDIA/AMD/Intel. |
| **Very slow processing** | GPU valt stilzwijgend terug op CPU | Controleer dat `ocrEngine.getProcessingMode()` `AUTO_GPU` retourneert en dat `SystemInfo.isGpuAvailable()` true is. |
| **Blank output** | Afbeelding te donker of laag contrast | Pre‑process de afbeelding (verhoog contrast, binariseer) voordat je deze aan OCR geeft. |
| **Out‑of‑Memory** | Zeer grote afbeelding (>10 MP) | Verklein of splits de afbeelding in tegels; verwerk elke tegel afzonderlijk. |

## Stapsgewijze samenvatting (Snelle referentie)

| Stap | Wat je deed |
|------|--------------|
| 1 | Aspose OCR‑afhankelijkheid toegevoegd |
| 2 | `OcrEngine` aangemaakt en `AUTO_GPU` ingesteld |
| 3 | Een factuurafbeelding geladen via `OcrInput` |
| 4 | `recognize` aangeroepen en `ocrResult.getText()` afgedrukt |
| 5 | Veelvoorkomende fouten afgehandeld en output geverifieerd |

## Verder gaan – Volgende stappen

- **Batchverwerking:** Loop over een map met facturen en sla elk resultaat op in een database.  
- **Taalondersteuning:** Schakel `ocrEngine.setLanguage(OcrEngine.Language.FRENCH)` in voor meertalige facturen.  
- **Post‑processing:** Gebruik reguliere expressies om velden zoals *Invoice Number* of *Total Amount* uit de ruwe tekst te extraheren.  
- **GPU‑afstemming:** Als je meerdere GPU's hebt, verken `ocrEngine.setGpuDeviceId(int id)` om de snelste te kiezen.

## Conclusie

We hebben **hoe je GPU kunt inschakelen** voor Java OCR laten zien, een helder **java ocr voorbeeld** gedemonstreerd, en de volledige stroom van **afbeelding laden voor OCR** tot **tekst extraheren uit factuur** doorlopen. Door gebruik te maken van Aspose’s `AUTO_GPU`‑modus krijg je een prestatieboost zonder compatibiliteit op te offeren—perfect voor zowel ontwikkelmachines als productieservers.

Probeer het, pas de afbeelding‑preprocessing aan, en experimenteer met batch‑taken. De mogelijkheden zijn eindeloos wanneer je GPU‑versnelling combineert met een robuuste OCR‑bibliotheek.

---

![Diagram dat GPU‑versnelde OCR‑pipeline toont – hoe GPU in te schakelen voor Java OCR](https://example.com/images/gpu-ocr-pipeline.png "hoe GPU in te schakelen voor Java OCR")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}