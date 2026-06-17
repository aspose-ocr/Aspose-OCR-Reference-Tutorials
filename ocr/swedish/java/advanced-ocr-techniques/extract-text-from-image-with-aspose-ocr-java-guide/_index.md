---
category: general
date: 2026-02-14
description: Extrahera text från bild med Aspose OCR i Java. Lär dig hur du extraherar
  text från formulärfält med intresseområden för precisa resultat.
draft: false
keywords:
- extract text from image
- extract text from form
language: sv
og_description: Extrahera text från en bild med Aspose OCR i Java. Denna handledning
  visar hur du extraherar text från formulärfält via intresseområden.
og_title: Extrahera text från bild med Aspose OCR – Java‑guide
tags:
- OCR
- Java
- Aspose
- Image Processing
title: Extrahera text från bild med Aspose OCR – Java‑guide
url: /sv/java/advanced-ocr-techniques/extract-text-from-image-with-aspose-ocr-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahera text från bild med Aspose OCR – Java‑guide

Har du någonsin behövt **extrahera text från bild** men slutade med att analysera hela bilden, slösa CPU‑cykler och få brusiga resultat? Du är inte ensam. I många verkliga applikationer—tänk fakturaskannrar, passläsare eller datainmatningsformulär—är du bara intresserad av ett fåtal fält, inte hela duken.  

Den goda nyheten är att Aspose OCR låter dig **extrahera text från bild** *och* från specifika formulärområden genom att definiera polygoner. I den här handledningen kommer du att se exakt hur du **extraherar text från formulär**‑fält med Java, varför metoden är viktig och vad du kan justera när något går fel.

Nedan täcker vi allt från att installera biblioteket till att hantera knepiga hörnfall, så att du i slutet har ett färdigt kodexempel som bara hämtar den data du behöver.

## Vad du behöver

- Java 17 (eller någon nyare JDK) – nyare versioner har bättre Unicode‑stöd.  
- Aspose.OCR för Java 23.10 (eller den senaste versionen vid läsningstillfället).  
- En exempelbild med namnet `form.png` som innehåller tydligt definierade fält.  
- En IDE eller enkel textredigerare—IntelliJ IDEA, VS Code eller till och med Notepad räcker.

Ingen Maven/Gradle‑magik behövs för grunddemo; lägg bara till Aspose OCR‑JAR‑filen i din classpath.

---

## Steg 1 – Initiera OCR‑motorn och ladda din bild

Det första motorn behöver är en bitmap att arbeta på. Vi pekar den på `form.png`, som ligger i samma mapp som källfilen.

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

*Varför detta är viktigt:*  
Att skapa en ny `OcrEngine` ger dig en ren start, så att inga tidigare inställningar påverkar körningen. Att ladda bilden tidigt validerar också att filen finns, så du får ett hjälpsamt undantag innan du slösar tid på senare steg.

> **Proffstips:** Om din bild är enorm (över 5 MB), överväg att ändra storlek först. Aspose OCR fungerar snabbare på bilder under 2000 px i någon av dimensionerna.

---

## Steg 2 – Definiera polygoner för fälten du vill läsa

En *Region of Interest* (ROI) är bara en polygon som talar om för motorn var den ska titta. Nedan skapar vi två rektanglar—en för “First Name” och en för “Date of Birth”. Justera koordinaterna så att de matchar ditt eget formulär.

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

*Varför polygoner istället för rektanglar?*  
Polygoner ger dig flexibiliteten att hantera snedvridna eller icke‑rektangulära rutor—vanligt när du skannar utskrivna formulär som inte är perfekt justerade.

---

## Steg 3 – Berätta för Aspose OCR att fokusera endast på dessa regioner

Nu binder vi polygonerna till motorn. Metoden `setRegionsOfInterest` accepterar en lista, så du kan lägga till hur många fält du vill.

```java
        // Limit OCR to the defined regions
        ocrEngine.getEngineOptions()
                 .setRegionsOfInterest(Arrays.asList(firstField, secondField));
```

*Vad händer under huven?*  
Aspose OCR beskär varje polygon till en separat bitmap, kör sitt igenkänningsalgoritm och sammanfogar sedan resultaten. Detta minskar dramatiskt falska positiva från omgivande grafik.

---

## Steg 4 – Kör OCR‑processen

När allt är konfigurerat startar vi OCR. Anropet `process()` returnerar ett `OcrResult`‑objekt som innehåller den extraherade texten och förtroendesiffror.

```java
        // Execute OCR on the selected ROIs
        OcrResult ocrResult = ocrEngine.process();
```

Om du behöver förtroende per fält kan du inspektera `ocrResult.getRegions()`—varje region har sin egen poäng. För de flesta enkla formulär räcker den övergripande texten.

---

## Steg 5 – Visa (eller lagra) den extraherade texten

Till sist skriver vi ut resultatet till konsolen. I en riktig applikation kan du skriva till en databas, JSON‑fil eller skicka via ett API.

```java
        // Output the extracted text
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

**Förväntad output (exempel):**

```
=== Extracted Text ===
John Doe
12/04/1990
```

De två raderna motsvarar de två polygonerna vi definierade. Om du ser extra blanksteg, trimma dem med `String.trim()`.

---

## Hur du extraherar text från formulär när du har många fält

När ett formulär innehåller dussintals inmatningar blir det tråkigt att skriva in koordinater manuellt. Här är ett snabbt mönster du kan använda:

1. **Skapa en CSV** där varje rad innehåller `fieldName, x1, y1, x2, y2, x3, y3, x4, y4`.  
2. **Läs in CSV‑filen** vid körning, loopa igenom varje rad, bygg en `Polygon` och lägg till den i ROI‑listan.  

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

*Varför bry sig?*  
Att automatisera ROI‑generering låter dig återanvända samma Java‑kod för flera formulärlayouter, vilket håller ditt projekt DRY (Don’t Repeat Yourself).

---

## Kantfall & Tips du kanske inte tänkt på

- **Rotated scans:** Om hela bilden är roterad, anropa `ocrEngine.getEngineOptions().setRotateAngle(degrees)`.  
- **Low contrast:** Ställ in `ocrEngine.getEngineOptions().setContrast(1.5f)` för att förbättra läsbarheten.  
- **Non‑Latin scripts:** Byt språk med `ocrEngine.getEngineOptions().setLanguage(OcrLanguage.Spanish)` (eller något annat stödjert språk).  
- **Partial OCR failures:** Kontrollera alltid `ocrResult.getConfidence()`; om den faller under 80 % bör du be användaren om manuell verifiering.  

---

## Fullt fungerande exempel (Klar att kopiera‑klistra in)

Nedan är det kompletta programmet, redo att kompileras och köras. Byt ut `YOUR_DIRECTORY` mot mappen som innehåller `form.png`.

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

Kompilera med:

```bash
javac -cp "aspose-ocr-23.10.jar" MultiRoiDemo.java
java -cp ".:aspose-ocr-23.10.jar" MultiRoiDemo
```

Du bör se de två raderna med text som tillhör de definierade ROI‑erna.

---

## Vanliga frågor

**Q: Fungerar detta med PDF‑filer?**  
A: Inte direkt. Konvertera varje PDF‑sida till en bild först (t.ex. med Aspose PDF) och mata sedan bilden till OCR‑motorn.

**Q: Vad händer om mitt formulär har kryssrutor?**  
A: OCR kan inte läsa booleska tillstånd, men du kan behandla kryssruteområdet som en ROI och undersöka pixeltätheten för att avgöra om den är ikryssad.

**Q: Kan jag extrahera text från ett flersidigt formulär på en gång?**  
A: Loopa över varje sidbild, återanvänd samma ROI‑lista och sammanfoga resultaten.

---

## Slutsats

Vi har gått igenom en komplett, end‑to‑end‑lösning för **extrahera text från bild** med Aspose OCR, och visat hur samma teknik låter dig **extrahera text från formulär**‑fält med exakt precision. Genom att definiera polygoner, begränsa motorns fokus och hantera vanliga fallgropar får du snabb, ren data utan kostnaden för att bearbeta hela bilden.

Redo för nästa steg? Prova att kedja detta OCR‑resultat till en JSON‑payload, eller mata in det i en maskininlärningsmodell för validering. Himlen är gränsen, och nu kan du

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}