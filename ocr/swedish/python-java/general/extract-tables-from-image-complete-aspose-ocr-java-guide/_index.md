---
category: general
date: 2026-05-03
description: Extrahera tabeller från en bild med Aspose OCR Java. Lär dig att ladda
  en bild för OCR, extrahera tabell från PNG, konvertera bildtabellens text och snabbt
  känna igen kvittobilder.
draft: false
keywords:
- extract tables from image
- extract table from png
- load image for ocr
- convert image table text
- recognize receipt image
language: sv
og_description: Extrahera tabeller från en bild med Aspose OCR Java. Den här guiden
  visar hur du laddar en bild för OCR, extraherar en tabell från en PNG, konverterar
  bildtabellens text och känner igen en kvittobild.
og_title: Extrahera tabeller från bild – Aspose OCR Java-handledning
tags:
- Aspose OCR
- Java
- Image Processing
title: Extrahera tabeller från bild – komplett Aspose OCR Java‑guide
url: /sv/python-java/general/extract-tables-from-image-complete-aspose-ocr-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahera tabeller från bild – Complete Aspose OCR Java Guide

Har du någonsin behövt **extract tables from image**‑filer men stött på hinder? Kanske har du ett skannat kvitto eller en fotograferad faktura och den tabulära datan är gömd i en PNG. I den här handledningen får du se exakt hur du *load image for OCR*, omvandlar bilden till strukturerade rader och **convert image table text** till något du kan arbeta med i Java.  

Vi går igenom varje steg, från att licensiera Aspose OCR‑motorn till att skriva ut varje cell i de upptäckta tabellerna. När du är klar kan du **recognize receipt image**‑filer och plocka ut deras tabeller utan problem.

## Vad du kommer att lära dig

- Hur du initierar Aspose OCR‑motorn och applicerar din licens.  
- Varför aktivering av table detection är nyckeln till **extract tables from image**.  
- Den exakta koden som behövs för att **load image for OCR** och köra igenkänning på en PNG.  
- Sätt att hantera flera tabeller, lågupplösta skanningar och vanliga fallgropar.  
- Hur du **convert image table text** till ett utskrivbart (eller databas‑klart) format.

Ingen extern dokumentation behövs – allt du behöver finns här.

## Förutsättningar

- Java 17 eller senare (koden använder det moderna modul‑systemet).  
- En Aspose OCR for Java‑licensfil (`Aspose.OCR.Java.lic`). Om du bara experimenterar fungerar en tillfällig utvärderingsnyckel också.  
- En PNG‑bild som innehåller en tydlig tabell (t.ex. `receipt_with_table.png`).  
- Maven eller Gradle för att hämta Aspose OCR‑beroendet:

```xml
<!-- Maven snippet -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version>
</dependency>
```

> **Pro tip:** Placera licensfilen bredvid din `src/main/resources`‑mapp så att sökvägen förblir stabil i olika miljöer.

---

## Steg 1 – Initiera OCR‑motorn för **extract tables from image**

Innan motorn kan göra någonting måste den veta att du är en legit användare.

```java
import com.aspose.ocr.*;

public class TableExtractor {
    public static void main(String[] args) throws Exception {

        // Step 1: Create the OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Apply your Aspose OCR license – this removes evaluation watermarks
        License license = new License();
        license.setLicense("Aspose.OCR.Java.lic");
        ocrEngine.setLicense(license);
```

*Varför detta är viktigt:* Utan en giltig licens körs OCR‑motorn i provläge, vilket kan kapa resultat eller lägga till oönskade vattenstämplar – vilket gör tabellutdragning opålitlig.

---

## Steg 2 – Aktivera table detection (**extract table from png**)

Table detection är avstängt som standard; du måste slå på den.

```java
        // Step 2: Turn on table detection so the engine looks for tabular structures
        ocrEngine.getConfig().setEnableTableDetection(true);
```

Att sätta på denna flagga får Aspose OCR att behandla grupper av justerad text som rader och kolumner, exakt vad du behöver när du vill **extract tables from image**‑filer som är PNG‑bilder.

---

## Steg 3 – **Load image for OCR** och **recognize receipt image**

Nu matar vi faktiskt in bilden i motorn.

```java
        // Step 3: Load the PNG that contains the table
        // You can also use Image.fromStream(...) for in‑memory data
        Image inputImage = Image.fromFile("YOUR_DIRECTORY/receipt_with_table.png");

        // Run the recognition process – this returns an OcrResult object
        OcrResult ocrResult = ocrEngine.recognize(inputImage);
```

Om du arbetar med ett **recognize receipt image**‑scenario kan det vara bra att förbehandla bilden (räta upp, öka kontrast). Det ligger utanför denna snabba guide men är värt att utforska för brusiga skanningar.

---

## Steg 4 – Bearbeta OCR‑resultatet och **convert image table text**

`OcrResult`‑objektet kan innehålla en eller flera tabeller. Låt oss iterera över dem och skriva ut varje cell.

```java
        // Step 4: Iterate over every detected table
        if (ocrResult.getTables().isEmpty()) {
            System.out.println("No tables were detected. Try improving image quality.");
            return;
        }

        for (Table table : ocrResult.getTables()) {
            System.out.println("Table detected:");
            for (TableRow row : table.getRows()) {
                // Join each cell's text with a tab for easy copy‑paste
                String line = row.getCells()
                                 .stream()
                                 .map(Cell::getText)
                                 .reduce((a, b) -> a + "\t" + b)
                                 .orElse("");
                System.out.println(line);
            }
            System.out.println(); // Blank line between tables
        }
    }
}
```

**Vad detta gör:**  

- Kontrollerar om några tabeller hittades; om inte föreslås en kvalitetsjustering.  
- För varje tabell skriver den ut rader med tab‑separerade celler, ett bekvämt format för CSV‑import.  
- Anropet `Cell::getText` är kärnan i **convert image table text** – det hämtar den råa OCR‑strängen från varje cell.

### Förväntad utskrift

Om `receipt_with_table.png` innehåller en enkel 3 × 2‑tabell får du något i stil med:

```
Table detected:
Item	Quantity
Apple	2
Banana	5
```

Om bilden har flera tabeller separeras varje tabell med en tom rad.

---

## Steg 5 – Verifiera de extraherade tabellerna och hantera kantfall

### Vanliga fallgropar

| Problem | Varför det händer | Snabb fix |
|---------|-------------------|-----------|
| **Inga tabeller upptäckta** | Bilden är för suddig eller har låg kontrast | Applicera binarisering (`ImageProcessing.applyThreshold`) före OCR |
| **Sammanfogade celler** | Tabelllinjer är svaga, OCR behandlar dem som ett block | Öka `TableDetectionSensitivity` i `ocrEngine.getConfig()` |
| **Fel kolumnordning** | Sned bild som orsakar feljustering | Använd `ImageProcessing.deskew` eller rotera bilden 90° |

### Vad du kan göra härnäst

- **Exportera till CSV** – ersätt `System.out.println(line);` med en `FileWriter` för att spara data.  
- **Mata in i en databas** – mappa varje rad till en POJO och använd JPA för persistens.  
- **Kombinera med andra API:er** – för kvitto‑behandling kan du även extrahera totalsummor med reguljära uttryck på OCR‑texten.

---

## Fullt fungerande exempel (Kopiera‑klistra‑klart)

```java
import com.aspose.ocr.*;

public class TableExtractor {
    public static void main(String[] args) throws Exception {

        // Initialize OCR engine and apply license
        OcrEngine ocrEngine = new OcrEngine();
        License license = new License();
        license.setLicense("Aspose.OCR.Java.lic");
        ocrEngine.setLicense(license);

        // Enable table detection – crucial for extracting tables from image
        ocrEngine.getConfig().setEnableTableDetection(true);

        // Load the PNG image (replace with your actual path)
        Image inputImage = Image.fromFile("YOUR_DIRECTORY/receipt_with_table.png");

        // Recognize the image – this step performs OCR on the whole picture
        OcrResult ocrResult = ocrEngine.recognize(inputImage);

        // Verify we have tables; otherwise suggest a quality fix
        if (ocrResult.getTables().isEmpty()) {
            System.out.println("No tables were detected. Try improving image quality.");
            return;
        }

        // Print each table row by row, converting image table text into tab‑separated values
        for (Table table : ocrResult.getTables()) {
            System.out.println("Table detected:");
            for (TableRow row : table.getRows()) {
                String line = row.getCells()
                                 .stream()
                                 .map(Cell::getText)
                                 .reduce((a, b) -> a + "\t" + b)
                                 .orElse("");
                System.out.println(line);
            }
            System.out.println(); // Blank line between tables
        }
    }
}
```

Kör detta program, peka på en PNG som innehåller en tydlig tabell, och se konsolen fyllas med snyggt formaterade rader.

---

## Slutsats

Du har nu en solid, end‑to‑end‑lösning för att **extract tables from image**‑filer med Aspose OCR för Java. Från licensiering till **load image for OCR**, aktivering av **extract table from png**, och slutligen **convert image table text**, är varje steg täckt med förklaringar och praktiska tips.  

Nästa steg: kedja utdata till en CSV‑fil, skicka raderna till en relationsdatabas, eller kombinera OCR‑steget med en rutin för att extrahera kvitto‑totalsummor. Samma mönster fungerar för fakturor, prislistor och alla skannade dokument som gömmer data bakom ett rutnät.

Har du frågor om hantering av lågupplösta kvitton eller hur du skalar detta till batch‑bearbetning? Lämna en kommentar nedan, och lycka till med kodandet!  

![Extract tables from image example](https://example.com/assets/extract-tables-from-image.png "Extract tables from image – sample output")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}