---
category: general
date: 2026-01-12
description: Extrahera text från bild med Aspose OCR i Java. Lär dig hur du extraherar
  text från en fakturabild med ett Java‑OCR‑exempel och får den extraherade OCR‑texten.
draft: false
keywords:
- extract text from image
- how to extract text
- java ocr example
- process invoice image
- output ocr text
language: sv
og_description: Extrahera text från bild med Aspose OCR i Java. Denna guide visar
  hur du extraherar text från en fakturabild, innehåller ett Java OCR‑exempel och
  skriver ut OCR‑text.
og_title: Extrahera text från bild i Java – Komplett OCR‑exempel
tags:
- OCR
- Java
- Aspose
title: Extrahera text från bild i Java – Komplett OCR‑exempel
url: /sv/java/ocr-basics/extract-text-from-image-in-java-complete-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahera text från bild i Java – Komplett OCR‑exempel

Har du någonsin funderat på hur man **extraherar text från bild**‑filer utan att dra i håret? Kanske har du en hög med skannade fakturor och behöver siffrorna snabbt. Enligt min erfarenhet är det enklaste sättet att låta ett dedikerat OCR‑bibliotek göra det tunga arbetet. Denna handledning visar *hur man extraherar text* från en typisk fakturabild med Aspose OCR för Java, och den demonstrerar dessutom ett **java ocr example** som skriver ut OCR‑texten som du kan skicka vidare till ditt downstream‑system.

Vi går igenom allt du behöver veta: från att sätta upp projektet, definiera regionen av intresse (ROI) som fokuserar på rubriken och totalsumman, till att slutligen skriva ut den extraherade texten. När du är klar kommer du kunna **process invoice image**‑filer automatiskt och hämta ren, sökbar text.

> **Vad du får:** ett färdigt Java‑program som går att köra, tydliga förklaringar av varje steg och praktiska tips för att hantera fakturor i verkligheten.

---

## Förutsättningar

Innan vi dyker ner, se till att du har följande:

- Java Development Kit (JDK) 8 eller nyare installerat.
- Maven eller Gradle för beroendehantering (Maven‑exempel visas).
- En Aspose OCR för Java‑licens (gratis provversion fungerar för testning).
- En fakturabild (`invoice.png`) placerad i en känd katalog.

Om något av detta låter obekant, oroa dig inte – de flesta är bara ett nedladdningssteg bort, och koden kommer fortfarande att kompilera med community‑edition.

---

## Steg 1: Skapa ditt Maven‑projekt

Först, skapa ett nytt Maven‑projekt (eller lägg till i ett befintligt). I din `pom.xml`, lägg till Aspose OCR‑beroendet:

```xml
<!-- pom.xml -->
<dependencies>
    <dependency>
        <groupId>com.aspose</groupId>
        <artifactId>aspose-ocr</artifactId>
        <version>23.9</version> <!-- Use the latest version available -->
    </dependency>
</dependencies>
```

> **Proffstips:** Håll versionsnumret uppdaterat; nyare releaser förbättrar ofta noggrannheten för knepiga typsnitt som finns på fakturor.

Efter att du sparat filen, kör `mvn clean install` för att hämta biblioteket till ditt lokala repository.

---

## Steg 2: Läs in fakturabilden

Nu när biblioteket är redo, låt oss skriva en liten Java‑klass. Det första vi gör är att skapa en `OcrEngine`‑instans och peka den på bilden du vill läsa.

```java
import com.aspose.ocr.*;

public class RoiExample {
    public static void main(String[] args) throws Exception {
        // Step 2: Load the source image
        OcrEngine engine = new OcrEngine();
        engine.setImage("YOUR_DIRECTORY/invoice.png"); // <-- replace with your path
```

Varför skapar vi motorn **innan** vi läser in bilden? Motorn håller konfiguration som språk, DPI och ROI. Att sätta bilden tidigt säkerställer att dessa inställningar gäller för exakt den fil du ska bearbeta.

---

## Steg 3: Definiera regioner av intresse (ROI)

Fakturor innehåller ofta mycket brus – tabeller, logotyper och finstilt text. Genom att begränsa OCR till bara rubriken och totalsumman ökar både hastighet och precision dramatiskt. Aspose låter dig beskriva dessa zoner med rektanglar.

```java
        // Step 3: Define the regions of interest (header and total amount)
        OcrRegion region = OcrRegion.builder()
                .addRectangle(0, 0, 800, 150)      // header area
                .addRectangle(0, 1200, 800, 200)   // total amount area
                .build();

        // Apply ROI to the engine
        engine.setRegion(region);
```

Koordinaterna är i pixlar (`x`, `y`, `width`, `height`). Om dina fakturor varierar i storlek kan du beräkna dessa värden dynamiskt – kanske genom att först kontrollera bildens dimensioner. Det är en fin utökning om du behöver en **process invoice image**‑lösning som fungerar på batcher.

---

## Steg 4: Kör OCR på de specificerade regionerna

Med ROI på plats kan OCR‑motorn fokusera sin uppmärksamhet där det verkligen räknas. Metoden `recognize()` returnerar ett `OcrResult` som innehåller den extraherade texten.

```java
        // Step 4: Run OCR on the specified regions
        OcrResult result = engine.recognize();
```

Bakom kulisserna utför Aspose flera förbehandlingssteg: binarisering, brusreducering och teckensegmentering. Du behöver inte anropa dem manuellt – låt bara `recognize()` göra jobbet.

---

## Steg 5: Skriv ut den extraherade texten

Till sist skriver vi ut texten till konsolen. I en riktig applikation kan du lagra den i en databas, skicka den till en downstream‑analyspipeline eller till och med generera en sökbar PDF.

```java
        // Step 5: Output the extracted text
        System.out.println("ROI text:");
        System.out.println(result.getText());
    }
}
```

När du kör programmet bör du se något i stil med:

```
ROI text:
Acme Corp.
Invoice #12345
Date: 2025-12-31
Total Amount: $1,250.00
```

Om utskriften ser förvrängd ut, dubbelkolla rektangelkoordinaterna eller öka bildens upplösning. OCR‑motorer älskar skarpa, hög‑DPI‑skanningar.

---

## Fullt fungerande exempel

Nedan är den kompletta, fristående Java‑filen som du kan kopiera‑klistra in i `src/main/java/RoiExample.java`. Inga externa kodsnuttar behövs – allt du behöver finns här.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.region.*;

public class RoiExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create the OCR engine and load the source image
        OcrEngine engine = new OcrEngine();
        engine.setImage("YOUR_DIRECTORY/invoice.png");

        // Step 2: Define the regions of interest (header and total amount)
        OcrRegion region = OcrRegion.builder()
                .addRectangle(0, 0, 800, 150)      // header area
                .addRectangle(0, 1200, 800, 200)   // total amount area
                .build();

        // Step 3: Apply the ROI configuration to the engine
        engine.setRegion(region);

        // Step 4: Run OCR on the specified regions
        OcrResult result = engine.recognize();

        // Step 5: Output the extracted text
        System.out.println("ROI text:");
        System.out.println(result.getText());
    }
}
```

> **Obs:** Ersätt `YOUR_DIRECTORY` med den absoluta sökvägen till din fakturabild. Om du använder en relativ sökväg, se till att arbetskatalogen matchar där du kör `java`‑kommandot.

---

## Vanliga frågor & kantfall

### Vad händer om fakturans storlek förändras?

Du kan beräkna ROI dynamiskt:

```java
int imgWidth = engine.getImage().getWidth();
int imgHeight = engine.getImage().getHeight();

int headerHeight = imgHeight / 10;
int totalHeight = imgHeight / 8;

OcrRegion region = OcrRegion.builder()
        .addRectangle(0, 0, imgWidth, headerHeight)
        .addRectangle(0, imgHeight - totalHeight, imgWidth, totalHeight)
        .build();
```

### Hur hanterar jag flera språk?

Aspose OCR stödjer språkpaket. Ställ bara in språket innan du anropar `recognize()`:

```java
engine.setLanguage(OcrLanguage.Spanish); // or OcrLanguage.English, etc.
```

### Vad gör jag om OCR returnerar tomma strängar?

Vanliga orsaker är:

- Låg bildupplösning (< 300 DPI). Skala upp eller begär skanningar av högre kvalitet.
- Alltför mörka eller ljusa bakgrunder. Applicera ett enkelt kontrast‑förbättringsfilter före OCR.
- Felaktiga ROI‑koordinater som missar texten helt.

---

## Tips för produktionsklar OCR

1. **Batch‑behandling:** Packa logiken i en loop som itererar över en katalog med fakturafiler. Logga varje resultat för spårbarhet.
2. **Felfångst:** Fånga `OcrException` för att smidigt hoppa över korrupta bilder utan att stoppa hela jobbet.
3. **Prestanda:** Återanvänd en enda `OcrEngine`‑instans över flera bilder; att skapa en ny motor per fil ger onödig overhead.
4. **Validering:** Efter extraktion, kör en regex‑kontroll på totalsumman (`\$\d{1,3}(,\d{3})*(\.\d{2})?`) för att säkerställa att siffran ser realistisk ut.

Genom att implementera dessa förslag förvandlar du ett enkelt **java ocr example** till en robust, skalbar lösning för alla företag som behöver **process invoice image**‑filer varje natt.

---

## Slutsats

Vi har just gått igenom hur man **extraherar text från bild**‑filer i Java med Aspose OCR, med fokus på ett praktiskt fakturabehandlingsscenario. Genom att definiera en region av intresse, köra OCR‑motorn och skriva ut **output OCR text**, har du nu en solid grund för att bygga automatiserade data‑fångst‑pipelines.

Nästa steg? Prova att utöka ROI för att inkludera rad‑item‑tabeller, experimentera med olika språkinställningar, eller skicka de extraherade strängarna till ett PDF‑genereringsbibliotek för sökbara dokument. Himlen är gränsen när du kombinerar OCR med moderna Java‑verktyg.

Har du fler frågor om **hur man extraherar text** från andra dokumenttyper, eller behöver hjälp med att finjustera ROI för ovanliga layouter? Lämna en kommentar nedan – happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}