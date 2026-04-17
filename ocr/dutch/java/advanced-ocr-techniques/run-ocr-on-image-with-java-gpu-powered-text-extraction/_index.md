---
category: general
date: 2026-03-07
description: Voer OCR uit op een afbeelding met Java. Leer hoe je tekst uit een PNG
  herkent, tekst van een bon extraheert en een afbeelding laadt voor OCR met een compleet
  Java OCR‑voorbeeld.
draft: false
keywords:
- run OCR on image
- recognize text from png
- extract text from receipt
- java OCR example
- load image for OCR
language: nl
og_description: Voer OCR uit op een afbeelding met Java. Deze gids laat zien hoe je
  tekst uit een PNG herkent, tekst van een bon extraheert en een afbeelding laadt
  voor OCR met een volledig Java OCR‑voorbeeld.
og_title: Voer OCR uit op afbeelding met Java – GPU‑aangedreven teksterkenning
tags:
- OCR
- Java
- GPU
- Image Processing
title: OCR uitvoeren op afbeelding met Java – GPU-aangedreven tekstextractie
url: /nl/java/advanced-ocr-techniques/run-ocr-on-image-with-java-gpu-powered-text-extraction/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR uitvoeren op afbeelding met Java – GPU-aangedreven Tekstextractie

Heb je ooit **OCR op afbeelding** bestanden moeten uitvoeren maar wist je niet waar je moet beginnen in Java? Je bent niet de enige—veel ontwikkelaars lopen tegen dezelfde muur aan wanneer ze voor het eerst proberen tekst te extraheren uit een gescand bonnetje of een PNG‑screenshot.  

In deze tutorial lopen we je stap voor stap door een **volledig Java OCR‑voorbeeld** dat niet alleen **tekst uit PNG**‑bestanden herkent, maar ook laat zien hoe je **tekst uit bon‑afbeeldingen** kunt **extraheren**, terwijl je profiteert van GPU‑versnelling voor snelheid. Aan het einde heb je een kant‑klaar programma dat een afbeelding laadt voor OCR, deze verwerkt en het platte‑tekstresultaat afdrukt.

## Wat je zult leren

- Hoe je **afbeelding laadt voor OCR** met een eenvoudige `ImageInputStream`.
- GPU‑ondersteuning inschakelen zodat de engine sneller draait op moderne hardware.
- De exacte stappen om **tekst uit PNG** te **herkennen** en bruikbare strings uit een bon te halen.
- Veelvoorkomende valkuilen (bijv. verkeerde GPU‑apparaat‑ID) en best‑practice tips.
- Een volledig, uitvoerbaar code‑fragment dat je kunt kopiëren‑en‑plakken in je IDE.

**Voorvereisten**

- Java 17 of nieuwer (de code gebruikt het `var`‑keyword voor beknoptheid, maar je kunt het vervangen door expliciete types als je Java 8 gebruikt).
- Een OCR‑bibliotheek die de klassen `OcrEngine`, `ImageInputStream` en `OcrResult` levert (bijvoorbeeld de fictieve *FastOCR* SDK; vervang door de echte die je gebruikt).
- Een GPU‑enabled machine als je de prestatie‑boost wilt (optioneel maar aanbevolen).

---

## Stap 1: OCR uitvoeren op afbeelding – GPU‑versnelling inschakelen

Het eerste wat je moet doen is de OCR‑engine maken en aangeven dat deze de GPU moet gebruiken. Deze stap is cruciaal omdat zonder GPU‑ondersteuning de engine terugvalt op de CPU, wat merkbaar langzamer kan zijn voor hoge‑resolutie bonnetjes.

```java
// Step 1: Create the OCR engine and enable GPU acceleration
OcrEngine ocrEngine = new OcrEngine();

// Turn on GPU usage – this makes the recognition much faster
ocrEngine.getConfig().setUseGpu(true);          // enable GPU usage

// Optional: select which GPU device to use (0 = first GPU)
ocrEngine.getConfig().setGpuDeviceId(0);
```

**Waarom dit belangrijk is:**  
GPU‑versnelling ontlast de zware matrixberekeningen die OCR‑engines uitvoeren. Als je meerdere GPU's hebt, kun je degene met het meeste geheugen kiezen door de `setGpuDeviceId`‑waarde aan te passen. Het vergeten om de GPU in te schakelen is een veelvoorkomende oorzaak van klachten als “waarom is mijn OCR zo traag?”.

> **Pro tip:** Als je machine geen compatibele GPU heeft, wordt de `setUseGpu(true)`‑aanroep simpelweg genegeerd—geen crash, alleen langzamere verwerking.

---

## Stap 2: Afbeelding laden voor OCR

Nu de engine klaar is, moeten we er een afbeelding aan voeren. Het voorbeeld hieronder laat zien hoe je een PNG‑bon van de schijf laadt. Je kunt het pad vervangen door elk afbeeldingsformaat dat door je OCR‑bibliotheek wordt ondersteund.

```java
// Step 2: Load the image you want to recognize
ImageInputStream imageStream = new ImageInputStream("YOUR_DIRECTORY/receipt.png");
```

**Randgeval:**  
Als het bestand niet bestaat of het pad onjuist is, zal `ImageInputStream` een `IOException` gooien. Plaats de aanroep in een try‑catch‑blok en log een nuttig bericht:

```java
try {
    ImageInputStream imageStream = new ImageInputStream("YOUR_DIRECTORY/receipt.png");
} catch (IOException e) {
    System.err.println("Failed to load image: " + e.getMessage());
    return;
}
```

---

## Stap 3: Tekst herkennen uit PNG

Met de afbeelding geladen kan de OCR‑engine nu haar magie doen. Deze stap **herkent tekst uit PNG** (of elk ander ondersteund formaat) en retourneert een `OcrResult`‑object.

```java
// Step 3: Run the OCR process on the image
OcrResult ocrResult = ocrEngine.recognize(imageStream);
```

**Wat gebeurt er onder de motorkap?**  
De engine voert preprocessing uit (kantcorrectie, binarisatie), draait een neuraal netwerk om tekens te detecteren, en zet deze vervolgens samen tot tekstregels. Omdat we eerder de GPU hebben ingeschakeld, gebeuren die neuraal‑netwerkberekeningen op de grafische kaart, waardoor enkele seconden van de totale uitvoeringstijd worden bespaard.

---

## Stap 4: Tekst extraheren uit bon

Na herkenning wil je meestal alleen de ruwe tekst. De `OcrResult`‑klasse biedt doorgaans een `getText()`‑methode die een enkele `String` retourneert. Je kunt deze vervolgens post‑processen (bijv. met regex om totalen, datums, enz. te extraheren).

```java
// Step 4: Print the recognized plain‑text result
System.out.println("Recognized text:");
System.out.println(ocrResult.getText());
```

**Typische bonoutput:**  

```
Store: Coffee Corner
Date: 2026-03-07
Item      Qty   Price
Latte      2    $5.80
Muffin     1    $2.50
TOTAL           $8.30
```

Je kunt deze string nu aan je eigen parser geven om het totaalbedrag, de postregels of belastinginformatie te extraheren.

---

## Stap 5: Volledig Java OCR‑voorbeeld – Klaar om uit te voeren

Alles samenvoegend, hier is het **volledige Java OCR‑voorbeeld** dat je in een `Main.java`‑bestand kunt plaatsen. Zorg ervoor dat de OCR‑bibliotheek op je classpath staat.

```java
import com.fastocr.OcrEngine;
import com.fastocr.ImageInputStream;
import com.fastocr.OcrResult;

public class Main {
    public static void main(String[] args) {
        // 1️⃣ Create OCR engine and enable GPU
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getConfig().setUseGpu(true);          // enable GPU usage
        ocrEngine.getConfig().setGpuDeviceId(0);        // optional: select GPU #0

        // 2️⃣ Load the image you want to recognize
        ImageInputStream imageStream;
        try {
            imageStream = new ImageInputStream("YOUR_DIRECTORY/receipt.png");
        } catch (Exception e) {
            System.err.println("Error loading image: " + e.getMessage());
            return;
        }

        // 3️⃣ Run OCR on the image
        OcrResult ocrResult = ocrEngine.recognize(imageStream);

        // 4️⃣ Output the plain‑text result
        System.out.println("Recognized text:");
        System.out.println(ocrResult.getText());
    }
}
```

**Verwachte console‑output** (ervan uitgaande dat de voorbeeldbon hierboven):

```
Recognized text:
Store: Coffee Corner
Date: 2026-03-07
Item      Qty   Price
Latte      2    $5.80
Muffin     1    $2.50
TOTAL           $8.30
```

Als de output er onduidelijk uitziet, controleer dan of de afbeelding scherp is (hoge DPI) en of het OCR‑taalpakket overeenkomt met de taal van je bon.

---

## Veelgestelde vragen & valkuilen

| Question | Answer |
|----------|--------|
| *Wat als mijn GPU niet wordt gedetecteerd?* | De engine valt automatisch terug op de CPU. Controleer de drivers en dat de `setGpuDeviceId` overeenkomt met een bestaand apparaat (`nvidia-smi` op Linux kan helpen). |
| *Kan ik JPEG‑ of TIFF‑bestanden verwerken?* | Ja—verander gewoon de bestandsextensie in `ImageInputStream`. De OCR‑bibliotheek detecteert het formaat meestal automatisch. |
| *Is er een manier om veel bonnetjes in batch te verwerken?* | Plaats de herkenningscode in een lus en hergebruik dezelfde `OcrEngine`‑instantie; opnieuw initialiseren per afbeelding verspilt GPU‑geheugen. |
| *Hoe verbeter ik de nauwkeurigheid bij bonnetjes met weinig contrast?* | Pre‑process de afbeelding (verhoog het contrast, converteer naar grijswaarden) voordat je deze aan de OCR‑engine voert. Sommige bibliotheken bieden een `preprocess`‑API. |

---

## Conclusie

Je weet nu **hoe je OCR op afbeelding**‑bestanden in Java uitvoert, van het laden van de foto tot het extraheren van schone tekst uit een bon. De walkthrough behandelde **tekst herkennen uit PNG**, **tekst extraheren uit bon**, en toonde een **java OCR‑voorbeeld** dat je kunt aanpassen aan elk project.  

Volgende stappen? Probeer de GPU‑vlag uit te schakelen om het prestatieverschil te zien, experimenteer met verschillende afbeeldingsresoluties, of integreer een regex‑gebaseerde parser om totalen automatisch te halen. Als je nieuwsgierig bent naar meer geavanceerde onderwerpen, kijk dan naar **OCR post‑processing**, **taalmodelcorrectie**, of **batch‑verwerkings‑pijplijnen**.

Veel plezier met coderen, en moge je bonnetjes altijd leesbaar zijn!  

![OCR op afbeelding voorbeeld](/images/run-ocr-on-image.png "OCR op afbeelding – Java voorbeeld")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}