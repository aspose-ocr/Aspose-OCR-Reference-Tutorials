---
category: general
date: 2026-07-21
description: Szöveg kinyerése képről Java OCR segítségével. Tanulja meg, hogyan konvertálja
  a PNG-t szöveggé, hogyan olvassa el a szöveget a PNG-ből, hogyan töltse be a képet
  OCR-hez, és hogyan végezzen OCR-t a képen néhány lépésben.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- extract text from image
- convert png to text
- read text from png
- load image for ocr
- perform ocr on image
language: hu
lastmod: 2026-07-21
og_description: Szöveg kinyerése képből Java-val. Ez az útmutató megmutatja, hogyan
  konvertálhat PNG-t szöveggé, olvashat szöveget PNG-ből, betöltheti a képet OCR-hez,
  és hatékonyan végezhet OCR-t a képen.
og_image_alt: Screenshot of Java code extracting text from an image using OCR
og_title: Szöveg kinyerése képből Java-ban – Lépésről lépésre OCR útmutató
schemas:
- author: Aspose
  dateModified: '2026-07-21'
  description: Extract text from image using Java OCR. Learn how to convert PNG to
    text, read text from PNG, load image for OCR, and perform OCR on image in just
    a few steps.
  headline: Extract Text from Image in Java – Complete OCR Guide
  type: TechArticle
- description: Extract text from image using Java OCR. Learn how to convert PNG to
    text, read text from PNG, load image for OCR, and perform OCR on image in just
    a few steps.
  name: Extract Text from Image in Java – Complete OCR Guide
  steps:
  - name: Low‑Quality Images
    text: 'If the PNG is blurry or has low contrast, OCR accuracy drops. A quick fix
      is to pre‑process the image:'
  - name: Multi‑Language Support
    text: Tess4J can handle many languages. Just download the appropriate `.traineddata`
      file and point `tesseract.setLanguage("spa")` for Spanish, for example.
  - name: Large PDFs or Multi‑Page Images
    text: If you need to **extract text from image** files inside a PDF, split each
      page into PNGs first (using PDFBox) and then feed each PNG to the same OCR routine.
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: Képből szöveg kinyerése Java-ban – Teljes OCR útmutató
url: /hu/java/ocr-basics/extract-text-from-image-in-java-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Szöveg kinyerése képből Java-ban – Teljes OCR útmutató

Valaha is szükséged volt **extract text from image**-re, de nem tudtad, melyik Java könyvtárat válaszd? Nem vagy egyedül. Akár nyugtákat digitalizálsz, PDF-eket szkennelsz, vagy kereshető archívumot építesz, egy PNG-ből szöveget kinyerni sok fejlesztő számára mindennapi problémát jelent.

Ebben az oktatóanyagról lépésről lépésre bemutatunk egy gyakorlati megoldást, amely lehetővé teszi, hogy **convert PNG to text**, **read text from PNG**, **load image for OCR**, és **perform OCR on image** – mind mindössze néhány sor tiszta Java kóddal. A végére lesz egy futtatható programod, amelyet bármely projektbe beilleszthetsz.

## Amit építeni fogsz

Készítünk egy kis Java konzolalkalmazást, amely:

1. Betölt egy PNG fájlt a lemezről.  
2. Elküldi a képet egy OCR motorba (Tess4J, egy Java wrapper a Tesseract-hez).  
3. Kiírja a felismert szöveget a konzolra.

Nincs külső szolgáltatás, nincs varázslat – csak tiszta Java és egy nyílt forráskódú OCR motor.

## Előfeltételek

- **Java 17** vagy újabb (a kód régebbi verziókkal is lefordítható, de a Java 17 a legújabb nyelvi funkciókat biztosítja).  
- **Maven** vagy **Gradle** a függőségkezeléshez.  
- Egy `sample.png` nevű minta PNG, amelyet egy hivatkozható mappában helyezel el (pl. `src/main/resources`).  
- Alapvető ismeretek a Java `main` metódusáról és a kivételkezelésről.

Ha bármelyik ismeretlennek tűnik, ne aggódj – minden lépés tartalmaz egy gyors összefoglalót.

## 1. lépés: A projekt beállítása és az OCR könyvtár hozzáadása

Először hozz létre egy új Maven projektet (vagy Gradlet, ha azt részesíted előnyben). Add hozzá a Tess4J függőséget, amely automatikusan tartalmazza a Tesseract binárisait.

```xml
<!-- pom.xml -->
<project xmlns="http://maven.apache.org/POM/4.0.0" ...>
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>ocr-demo</artifactId>
    <version>1.0.0</version>
    <properties>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
    </properties>

    <dependencies>
        <!-- Tess4J – Java wrapper for Tesseract OCR -->
        <dependency>
            <groupId>net.sourceforge.tess4j</groupId>
            <artifactId>tess4j</artifactId>
            <version>5.5.1</version>
        </dependency>
    </dependencies>
</project>
```

> **Pro tipp:** Ha Gradlet használsz, az ekvivalens sor `implementation 'net.sourceforge.tess4j:tess4j:5.5.1'`.

Ennek a könyvtárnak a hozzáadása biztosítja a `Tesseract` osztályt, amely a **performing OCR on image** adatfeldolgozás nehéz részét végzi.

## 2. lépés: Kép betöltése OCR-hez

Most szükségünk van a **load image for OCR**-ra. A Tess4J a `java.awt.image.BufferedImage`-tel dolgozik, ezért a PNG-t az `ImageIO`-val olvassuk be.

```java
package com.example.ocrdemo;

import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;

import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;
import java.io.IOException;

public class OcrDemo {

    /**
     * Loads a PNG file from the given path and returns a BufferedImage.
     *
     * @param path absolute or relative path to the PNG file
     * @return BufferedImage containing the image data
     * @throws IOException if the file cannot be read
     */
    private static BufferedImage loadImage(String path) throws IOException {
        // Step 2: Load the image to be recognized
        File imgFile = new File(path);
        return ImageIO.read(imgFile);
    }
```

A fenti metódus tisztán elkülöníti a **load image for OCR** logikát, így a kód többi része könnyebben tesztelhető. Vedd észre a megjegyzést – tükrözi az eredeti kódrészletet, miközben a tisztaság kedvéért kibővíti.

## 3. lépés: OCR végrehajtása a képen

Miután a kép a memóriában van, most már **perform OCR on image**-t hajthatunk végre. A `Tesseract` példány a motorunk; beállítjuk, hogy a Tess4J-vel szállított alapértelmezett angol nyelvi adatot használja.

```java
    /**
     * Runs OCR on the supplied BufferedImage and returns the extracted text.
     *
     * @param image the image to analyze
     * @return plain text recognized from the image
     * @throws TesseractException if the OCR process fails
     */
    private static String extractText(BufferedImage image) throws TesseractException {
        // Step 1: Initialize the OCR engine
        Tesseract tesseract = new Tesseract();

        // Optional: set the datapath if you have a custom tessdata folder
        // tesseract.setDatapath("tessdata");

        // Step 4: Run OCR and capture the recognized text
        return tesseract.doOCR(image);
    }
```

Itt egyesítettük az eredeti “Step 1” és “Step 4” lépéseket egyetlen metódusba, mivel a `Tesseract` objektum létrehozása olcsó, és szeretnénk, hogy a kód kompakt maradjon. A megjegyzés továbbra is az eredeti lépéseket hivatkozza a nyomon követhetőség érdekében.

## 4. lépés: Összeállítás – Main metódus

Végül mindent összehozzuk a `main`-ben. Itt fogod **read text from PNG**-t végrehajtani, és a konzolon megjeleníteni az eredményt.

```java
    public static void main(String[] args) {
        // Adjust the path to point at your PNG file
        String imagePath = "src/main/resources/sample.png";

        try {
            // Load the PNG image
            BufferedImage image = loadImage(imagePath);

            // Extract text from the image
            String recognizedText = extractText(image);

            // Step 5: Display the extracted text
            System.out.println("=== OCR Result ===");
            System.out.println(recognizedText);
        } catch (IOException e) {
            System.err.println("Failed to load image: " + e.getMessage());
        } catch (TesseractException e) {
            System.err.println("OCR error: " + e.getMessage());
        }
    }
}
```

Amikor futtatod a `mvn compile exec:java -Dexec.mainClass="com.example.ocrdemo.OcrDemo"` parancsot (vagy a Gradle megfelelőjét), valami ilyesmit kell látnod:

```
=== OCR Result ===
Hello, world!
This is a sample PNG file.
```

Ez a kimenet bizonyítja, hogy sikeresen **extract text from image**, **convert PNG to text**, és **read text from PNG**-t hajtottál végre egyetlen, rendezett programban.

## Gyakori esetek kezelése

### Alacsony minőségű képek

Ha a PNG elmosódott vagy alacsony kontrasztú, az OCR pontossága csökken. Egy gyors megoldás a kép előfeldolgozása:

```java
// Example: Convert to grayscale and apply a binary threshold
BufferedImage gray = new BufferedImage(
        image.getWidth(), image.getHeight(),
        BufferedImage.TYPE_BYTE_GRAY);
Graphics2D g = gray.createGraphics();
g.drawImage(image, 0, 0, null);
g.dispose();

// Simple binary threshold
for (int y = 0; y < gray.getHeight(); y++) {
    for (int x = 0; x < gray.getWidth(); x++) {
        int rgb = gray.getRGB(x, y) & 0xFF;
        int binary = rgb < 128 ? 0x000000 : 0xFFFFFF;
        gray.setRGB(x, y, binary);
    }
}
String text = extractText(gray);
```

### Többnyelvű támogatás

A Tess4J sok nyelvet támogat. Csak töltsd le a megfelelő `.traineddata` fájlt, és állítsd be a `tesseract.setLanguage("spa")`-t például a spanyolhoz.

### Nagy PDF-ek vagy többoldalas képek

Ha **extract text from image** fájlokat kell kinyerni egy PDF-ből, először bontsd szét az egyes oldalakat PNG-ké, (PDFBox használatával), majd minden PNG-t add át ugyanahhoz az OCR rutinhoz.

## Teljes működő példa (Minden kód egy helyen)

Az alábbiakban a teljes, azonnal futtatható Java osztály található. Másold be a `src/main/java/com/example/ocrdemo/OcrDemo.java` fájlba, és már használhatod.

```java
package com.example.ocrdemo;

import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;

import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;
import java.io.IOException;

/**
 * Demonstrates how to extract text from image (PNG) using Java and Tess4J.
 */
public class OcrDemo {

    private static BufferedImage loadImage(String path) throws IOException {
        // Step 2: Load the image for OCR
        File imgFile = new File(path);
        return ImageIO.read(imgFile);
    }

    private static String extractText(BufferedImage image) throws TesseractException {
        // Step 1: Initialize the OCR engine
        Tesseract tesseract = new Tesseract();
        // Uncomment and set if you have a custom tessdata folder
        // tesseract.setDatapath("tessdata");
        // Step 4: Perform OCR on image
        return tesseract.doOCR(image);
    }

    public static void main(String[] args) {
        // Path to the PNG you want to convert to text
        String imagePath = "src/main/resources/sample.png";

        try {
            BufferedImage image = loadImage(imagePath);
            String recognizedText = extractText(image);
            System.out.println("=== OCR Result ===");
            System.out.println(recognizedText);
        } catch (IOException e) {
            System.err.println("Failed to load image: " + e.getMessage());
        } catch (TesseractException e) {
            System.err.println("Error during OCR: " + e.getMessage());
        }
    }
}
```

Az osztály futtatása kiírja az OCR eredményt, megerősítve, hogy sikeresen **performed OCR on image**-t hajtottál végre, és a PNG-d szerkeszthető szöveggé vált.

## Összefoglalás és további lépések

Azzal kezdtük, hogy **extracting text from image**-t használtunk egy könnyű Java környezetben. Most már tudod, hogyan **load image for OCR**, **perform OCR on image**, és **read text from PNG** – ezek alapvető építőelemei minden dokumentum‑digitalizációs folyamatnak.

Szeretnél továbbmenni? Próbáld ki ezeket az ötleteket:

- **Batch processing:** Egy PNG könyvtáron iterálva minden eredményt írj egy `.txt` fájlba.  
- **Integrate with a database:** Tárold a kinyert szövegeket metaadatokkal együtt a kereshető archívumokhoz.  
- **Combine with NLP:** Az OCR kimenetet egy sentiment‑analysis modellbe tápláld a gyors betekintéshez.  

Ezek a kiegészítések mind ugyanazokra az alapelvekre épülnek, amelyeket bemutattunk, így készen állsz a kísérletezésre.

---

*Boldog kódolást! Ha bármilyen problémába ütközöl

## Mit érdemes legközelebb megtanulni?

A következő oktatóanyagok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás tartalmaz teljesen működő kódrészleteket lépésről‑lépésre magyarázatokkal, hogy elsajátíthasd a további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [Szöveg kinyerése képből Java-val az Aspose.OCR Detect Areas Mode használatával](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [image to text java: Kép konvertálása szöveggé az Aspose.OCR segítségével](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [Hogyan OCR-eljünk képszöveget nyelvvel az Aspose.OCR használatával](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}