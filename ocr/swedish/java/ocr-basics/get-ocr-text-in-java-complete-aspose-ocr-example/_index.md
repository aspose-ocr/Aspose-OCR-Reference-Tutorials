---
category: general
date: 2026-01-07
description: Hämta OCR‑text från en bild med Aspose OCR Java. Lär dig hur du extraherar
  text från en bild, laddar bild‑OCR och kör ett Java‑OCR‑exempel på några minuter.
draft: false
keywords:
- get OCR text
- extract text image
- java OCR example
- aspose OCR Java
- load image OCR
language: sv
og_description: Hämta OCR‑text från bilder med Aspose OCR Java. Den här guiden visar
  ett Java‑OCR‑exempel, hur man extraherar text från en bild och hur man laddar bild‑OCR
  effektivt.
og_title: Hämta OCR‑text i Java – Komplett Aspose OCR‑handledning
tags:
- OCR
- Java
- Aspose
- Image Processing
title: Hämta OCR‑text i Java – komplett Aspose OCR‑exempel
url: /sv/java/ocr-basics/get-ocr-text-in-java-complete-aspose-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hämta OCR‑text i Java – Komplett Aspose OCR‑exempel

Har du någonsin behövt **hämta OCR‑text** från ett skannat dokument men varit osäker på vilket bibliotek du ska välja? Du är inte ensam. I många verkliga projekt—tänk fakturautomatisk, kvittohantering eller flerspråkig formulärdigitalisering—är extrahering av text från bilder det första steget mot automatisering.  

I den här handledningen går vi igenom ett **java OCR‑exempel** som använder Aspose OCR för Java‑biblioteket. När du är klar vet du hur du **laddar bild‑OCR**, kör motorn och **extraherar text‑bild**‑data med bara några rader kod. Inga onödiga detaljer, bara en praktisk lösning som du kan kopiera‑klistra in i ditt eget projekt.

## Vad du kommer att lära dig

- Hur du konfigurerar Aspose OCR för Java (inklusive Maven‑koordinater).  
- De exakta stegen för att **ladda bild‑OCR** och ange ett språk.  
- Hur du **hämtar OCR‑text** som en vanlig sträng och skriver ut den i konsolen.  
- Tips för att hantera flerspråkiga bilder och automatisk språkdetektering.  

*Förutsättningar*: Java 8 eller nyare, en Maven‑kompatibel IDE (IntelliJ IDEA, Eclipse eller VS Code) och en giltig Aspose OCR för Java‑licens (gratis provversion fungerar för utvärdering).

---

![Flödesschema som visar hur man hämtar OCR‑text från en bild med Aspose OCR Java](https://example.com/ocr-flowchart.png "Flödesschema för att hämta OCR‑text")

## Steg 1 – Lägg till Aspose OCR‑beroende (Ladda bild‑OCR)

Först, låt Maven hämta Aspose OCR‑biblioteket. Öppna din `pom.xml` och sätt in följande `<dependency>`‑block innanför `<dependencies>`:

```xml
<!-- Aspose OCR for Java -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- Use the latest version available -->
</dependency>
```

> **Pro tip**: Om du använder Gradle är motsvarigheten `implementation 'com.aspose:aspose-ocr:23.9'`. Att lägga till beroendet är det billigaste sättet att **ladda bild‑OCR**‑funktionaliteten i ditt projekt.

## Steg 2 – Skapa OCR‑motorn och ladda din bild

Nu skriver vi en liten Java‑klass som skapar en `OcrEngine`‑instans, pekar den på en bildfil och talar om för motorn vilket språk som ska kännas igen. Språket identifieras med sin ISO‑639‑2‑kod (t.ex. `"tam"` för Tamil).

```java
package com.example.ocr;

import com.aspose.ocr.*;

public class LanguageExample {

    public static void main(String[] args) throws Exception {
        // 2️⃣ Initialize the OCR engine
        OcrEngine engine = new OcrEngine();

        // 2️⃣ Load the image you want to process – this is the "load image OCR" step
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/multilingual.png"));

        // 2️⃣ Choose the language (ISO‑639‑2). Change "tam" to any supported code.
        engine.getEngineOptions().setLanguage("tam");
        // If you prefer automatic detection, uncomment the next line:
        // engine.getEngineOptions().setAutoDetectLanguage(true);
```

### Varför ange språk explicit?

Att specificera språk minskar falska positiva resultat och snabbar upp igenkänningen. För flerspråkiga PDF‑filer kan du loopa över en array med språkkoder, eller aktivera automatisk detektering för bekvämlighet.

## Steg 3 – Kör OCR‑processen och **hämta OCR‑text**

När motorn är konfigurerad utför nästa rad själva igenkänningen. Resultatobjektet innehåller den extraherade strängen samt ytterligare metadata.

```java
        // 3️⃣ Perform OCR – this is where we finally **get OCR text**
        OcrResult result = engine.recognize();

        // 3️⃣ Output the recognized text to the console
        System.out.println("=== Extracted Text ===");
        System.out.println(result.getText());
    }
}
```

När du kör `LanguageExample` bör du se något liknande:

```
=== Extracted Text ===
தமிழ் உரை இங்கு வருகிறது...
```

Om du använde `setAutoDetectLanguage(true)` kommer motorn att försöka gissa språket åt dig, vilket är praktiskt när du hanterar okända dokument.

## Steg 4 – Hantera vanliga kantfall (Extrahera text‑bild‑variationer)

### Hantera lågupplösta bilder

OCR‑noggrannheten sjunker kraftigt under 300 dpi. Om din källbild har låg upplösning, överväg att först skala upp den:

```java
engine.getEngineOptions().setResolution(300); // forces 300 DPI
```

### Ta bort bakgrundsbrus

Ibland har skannade formulär prickar som förvirrar motorn. Du kan aktivera förbehandling:

```java
engine.getEngineOptions().setPreprocessMode(EngineOptions.PreprocessMode.Auto);
```

### Extrahera text från specifika regioner

Om du bara behöver text från en viss rektangel (t.ex. en tabellcell), sätt en `Rectangle` innan du anropar `recognize()`:

```java
engine.setRegion(new Rectangle(50, 100, 400, 200));
```

Dessa justar gör ditt **java OCR‑exempel** robust nog för produktionsmiljöer.

## Steg 5 – Verifiera resultatet (Vad kan du förvänta dig?)

En lyckad körning skriver ut den rena textversionen av bilden. För flerspråkiga bilder kan du se blandade skript:

```
Hello World
こんにちは世界
مرحبا بالعالم
```

Om utskriften är tom eller förvrängd, dubbelkolla:

1. Filvägen i `setImage` (är den korrekt?).  
2. Språkkoden matchar skriptet i bilden.  
3. Bildkvaliteten (kontrast, DPI) är tillräcklig.

## Fullt fungerande exempel (Kopiera‑klistra redo)

Nedan är hela filen, klar att kompileras och köras. Ersätt `YOUR_DIRECTORY/multilingual.png` med den faktiska sökvägen till din testbild.

```java
package com.example.ocr;

import com.aspose.ocr.*;

public class LanguageExample {
    public static void main(String[] args) throws Exception {
        // Initialize OCR engine
        OcrEngine engine = new OcrEngine();

        // Load the image – this is the core "load image OCR" step
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/multilingual.png"));

        // Set language (ISO‑639‑2). For Tamil use "tam". Change as needed.
        engine.getEngineOptions().setLanguage("tam");
        // Uncomment for auto‑detect:
        // engine.getEngineOptions().setAutoDetectLanguage(true);

        // Optional: improve accuracy on low‑res images
        // engine.getEngineOptions().setResolution(300);
        // engine.getEngineOptions().setPreprocessMode(EngineOptions.PreprocessMode.Auto);

        // Perform OCR and retrieve text
        OcrResult result = engine.recognize();

        // Print the extracted text – this is how we **get OCR text**
        System.out.println("=== Extracted Text ===");
        System.out.println(result.getText());
    }
}
```

Kompilera och kör:

```bash
mvn compile exec:java -Dexec.mainClass="com.example.ocr.LanguageExample"
```

Du bör nu se det extraherade innehållet skrivet i din konsol.

---

## Slutsats

Vi har just visat dig **hur du hämtar OCR‑text** från en bild med Aspose OCR för Java. Genom att följa detta **java OCR‑exempel** kan du **extrahera text‑bild**‑data, **ladda bild‑OCR**, och även finjustera motorn för flerspråkiga eller brusiga indata.  

Härifrån kan du:

- Integrera OCR‑steget i ett större arbetsflöde (t.ex. lagra texten i en databas).  
- Kombinera det med ett översättnings‑API för att omvandla flerspråkiga skanningar till ett enda språk.  
- Experimentera med andra Aspose OCR‑funktioner som PDF‑konvertering eller streckkoddetektering.

Prova, bryt några saker, och finjustera sedan inställningarna tills resultatet är perfekt. Lycka till med kodningen, och må din OCR alltid vara kristallklar!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}