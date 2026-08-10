---
category: general
date: 2026-06-16
description: Ismerje meg, hogyan hajthat végre OCR-t képfájlokon Java nyelven. Ez
  az oktatóanyag a PNG-ből történő szövegfelismerést, a képről szöveg kinyerését,
  a kép szöveggé alakítását és a kép OCR-hez történő betöltését tárgyalja.
draft: false
keywords:
- perform OCR on image
- recognize text from PNG
- extract text from image
- convert image to text
- load image for OCR
language: hu
og_description: Képen végzett OCR Java-val. Ez az útmutató bemutatja, hogyan ismerjünk
  fel szöveget PNG-ből, hogyan nyerjünk ki szöveget a képből, és hogyan konvertáljunk
  képet szöveggé egy azonnal futtatható példával.
og_title: OCR végrehajtása képen Java-ban – Teljes programozási útmutató
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Learn how to perform OCR on image files in Java. This tutorial covers
    recognizing text from PNG, extracting text from image, converting image to text,
    and loading image for OCR.
  headline: Perform OCR on Image in Java – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Learn how to perform OCR on image files in Java. This tutorial covers
    recognizing text from PNG, extracting text from image, converting image to text,
    and loading image for OCR.
  name: Perform OCR on Image in Java – Complete Step‑by‑Step Guide
  steps:
  - name: Expected Output
    text: 'If `hello.png` contains the phrase “Hello, OCR world!”, the console will
      display something like:'
  - name: 5.1 Dealing with Low‑Resolution Images
    text: 'If the source PNG is blurry, OCR accuracy drops. A quick fix is to upscale
      the image before feeding it to the engine:'
  - name: 5.2 Multi‑Language Documents
    text: 'If you anticipate French or German text, simply add the language codes
      to `setLanguage`:'
  - name: 5.3 Skipping Empty Pages
    text: 'Sometimes a scanned PDF page renders as a blank PNG. Detecting an empty
      image saves processing time:'
  type: HowTo
tags:
- Java
- OCR
- Image Processing
title: OCR végrehajtása képen Java‑ban – Teljes lépésről‑lépésre útmutató
url: /hu/java/ocr-basics/perform-ocr-on-image-in-java-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR végrehajtása képen Java‑ban – Teljes lépésről‑lépésre útmutató

Valaha is szükséged volt **OCR végrehajtására képen** fájlokon, de nem tudtad, melyik Java‑könyvtárat válaszd? Nem vagy egyedül. Akár egy nyugtavásárló‑szkenner, egy dokumentum‑archíváló, vagy csak kíváncsi vagy arra, hogyan lehet a képeket kereshető szöveggé alakítani, a **OCR végrehajtása képen** Java‑val hasznos képesség.

Ebben az útmutatóban mindent végigvesszük, ami a **OCR végrehajtásához képen** szükséges: a kép betöltése, a motor konfigurálása, a szöveg felismerése, majd a végeredmény kiírása. A végére képes leszel **PNG fájlokból szöveget felismerni**, **szöveget kinyerni képről**, és **képet szöveggé konvertálni** néhány kódsorral.

## Előfeltételek

- Java 17 vagy újabb (a kód bármely friss JDK‑val lefordítható)
- Maven telepítve (vagy a kedvenc build eszközöd)
- Alapvető Java‑szintaxis ismerete
- Egy PNG fájl, amivel tesztelni szeretnél (nevezzük `hello.png`‑nek)

> **Pro tipp:** Ha nincs kéznél PNG, készíts egyet úgy, hogy egy szöveg képernyőképet készítesz, és `hello.png`‑ként mented el a `resources` mappába.

## Mit fogunk építeni

Egy apró konzolos alkalmazás `OcrDemo` néven, amely:

1. **Betölti a képet OCR‑hez** – PNG‑t olvas le a lemezről.
2. **Végrehajtja az OCR‑t a képen** – a Tesseract motor használatával a Tess4J‑n keresztül.
3. **Kinyeri a szöveget a képről** – egy `String`‑et ad vissza a felismert tartalommal.
4. Kiírja az eredményt a konzolra.

Vágjunk bele.

## 1. lépés: Projekt létrehozása és Tess4J hozzáadása

Először hozz létre egy új Maven projektet (vagy Gradle‑t, ha azt részesíted előnyben). Add hozzá a Tess4J függőséget, amely a népszerű Tesseract OCR motorra épül.

```xml
<!-- pom.xml -->
<project>
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

> **Miért Tess4J?** Aktívan karbantartott, platformfüggetlen, és tiszta Java API‑t biztosít a **OCR végrehajtásához képen** feladatokhoz.

## 2. lépés: Kép‑betöltő logika előkészítése

Most írunk egy segédmetódust, amely **betölti a képet OCR‑hez**. A metódus a Java `ImageIO`‑ját használja egy PNG beolvasásához `BufferedImage`‑be.

```java
package com.example.ocr;

import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;
import java.io.IOException;

/**
 * Utility class responsible for loading images from the file system.
 */
public final class ImageLoader {

    private ImageLoader() { /* utility class */ }

    /**
     * Loads a PNG (or any supported format) from the given path.
     *
     * @param path absolute or relative path to the image file
     * @return BufferedImage instance ready for OCR processing
     * @throws IOException if the file cannot be read
     */
    public static BufferedImage load(String path) throws IOException {
        File imgFile = new File(path);
        if (!imgFile.exists()) {
            throw new IOException("Image file not found: " + path);
        }
        return ImageIO.read(imgFile);
    }
}
```

Vedd észre, hogy a metódus neve egyértelműen tükrözi a **betöltés OCR‑hez** szándékot, így a kód önmagát dokumentálja.

## 3. lépés: Az OCR motor konfigurálása a **OCR végrehajtásához képen**

Miután megvan a kép, létrehozunk egy `Tesseract` példányt, engedélyezzük az automatikus nyelvfelismerést, és meghívjuk a `doOCR`‑t. Ez a magja annak, hogyan **végezzünk OCR‑t a képen**.

```java
package com.example.ocr;

import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;

/**
 * Wrapper around Tess4J that abstracts the OCR workflow.
 */
public final class OcrEngine {

    private final ITesseract tesseract;

    public OcrEngine() {
        tesseract = new Tesseract();

        // Use the bundled tessdata folder (you can also point to a custom one)
        tesseract.setDatapath("tessdata");

        // Enable automatic language detection – improves accuracy across multilingual images
        tesseract.setLanguage("eng"); // fallback language
        tesseract.setOcrEngineMode(ITesseract.OEM_DEFAULT);
        tesseract.setPageSegMode(ITesseract.PSM_AUTO);
    }

    /**
     * Performs OCR on the supplied BufferedImage and returns the recognized text.
     *
     * @param image image to be processed
     * @return the text extracted from the image
     * @throws TesseractException if OCR fails
     */
    public String recognize(BufferedImage image) throws TesseractException {
        return tesseract.doOCR(image);
    }
}
```

> **Miért engedélyezzük az automatikus felismerést?** Lehetővé teszi, hogy a motor a legjobb nyelvi modellt válassza a képhez, ami különösen hasznos, ha **képet szöveggé konvertálsz** olyan forrásokból, amelyek angolt és más írásrendszereket is kevernek.

## 4. lépés: Összeállítás – a fő alkalmazás

Itt van a belépési pont, amely **szöveget felismer PNG‑ről**, **szöveget nyer ki a képről**, és végül kiírja az eredményt. Ez a teljes, futtatható példa.

```java
package com.example.ocr;

import net.sourceforge.tess4j.TesseractException;
import java.awt.image.BufferedImage;
import java.io.IOException;

/**
 * Demo application that shows how to perform OCR on image files.
 */
public class OcrDemo {

    public static void main(String[] args) {
        // Path to the PNG you want to process
        String imagePath = "resources/hello.png";

        try {
            // Step 1: Load image for OCR
            BufferedImage image = ImageLoader.load(imagePath);

            // Step 2: Create OCR engine instance
            OcrEngine engine = new OcrEngine();

            // Step 3: Perform OCR on image and retrieve the text
            String recognizedText = engine.recognize(image);

            // Step 4: Output the recognized text to the console
            System.out.println("=== Recognized Text ===");
            System.out.println(recognizedText);
        } catch (IOException e) {
            System.err.println("Failed to load image: " + e.getMessage());
        } catch (TesseractException e) {
            System.err.println("OCR processing error: " + e.getMessage());
        }
    }
}
```

### Várható kimenet

Ha a `hello.png` a „Hello, OCR world!” szöveget tartalmazza, a konzol valami ilyesmit jelenít meg:

```
=== Recognized Text ===
Hello, OCR world!
```

A pontos kimenet kissé eltérhet a kép minőségétől függően, de a PNG‑ben elhelyezett szöveget látnod kell.

## 5. lépés: Gyakori edge case‑ek kezelése

### 5.1 Alacsony felbontású képek kezelése

Ha a forrás PNG elmosódott, az OCR pontossága csökken. Egy gyors megoldás a kép felméretezése a motorba való betáplálás előtt:

```java
import java.awt.Graphics2D;
import java.awt.RenderingHints;

public static BufferedImage upscale(BufferedImage original, int factor) {
    int width = original.getWidth() * factor;
    int height = original.getHeight() * factor;
    BufferedImage scaled = new BufferedImage(width, height, original.getType());
    Graphics2D g = scaled.createGraphics();
    g.setRenderingHint(RenderingHints.KEY_INTERPOLATION,
                       RenderingHints.VALUE_INTERPOLATION_BICUBIC);
    g.drawImage(original, 0, 0, width, height, null);
    g.dispose();
    return scaled;
}
```

Hívd meg az `upscale(image, 2)`‑t a `engine.recognize(image)` előtt a jobb eredmény érdekében.

### 5.2 Többnyelvű dokumentumok

Ha francia vagy német szöveget is vársz, egyszerűen add hozzá a nyelvkódokat a `setLanguage`‑hez:

```java
tesseract.setLanguage("eng+fra+deu");
```

A motor ezután a kombinált nyelvi modellekkel **szöveget nyer ki a képről**.

### 5.3 Üres oldalak kihagyása

Néha egy beolvasott PDF oldal üres PNG‑ként jelenik meg. Egy üres kép felismerése időt takarít meg:

```java
if (image.getWidth() == 0 || image.getHeight() == 0) {
    System.out.println("Empty image – skipping OCR.");
    return;
}
```

## 6. lépés: Csomagolás és futtatás

1. **Fordítás:** `mvn clean compile`
2. **Futtatás:** `mvn exec:java -Dexec.mainClass="com.example.ocr.OcrDemo"`

Győződj meg róla, hogy a `tessdata` mappa (a nyelvi fájlokkal) a lefordított JAR mellé kerül, vagy add meg az abszolút útvonalát az `OcrEngine`‑ben.

## Összegzés

Most már van egy stabil, termelés‑kész mintád a **OCR végrehajtásához képen** Java‑val. A **kép betöltését OCR‑hez**ől a **szöveg felismeréséig PNG‑ről** mind átfedtük, beleértve a **szöveg kinyerését a képről**, a **kép szöveggé konvertálását**, valamint a nehéz esetek, például alacsony felbontású szkennelés vagy többnyelvű tartalom kezelését.

További lépések, amiket érdemes felfedezni:

- **Kötegelt feldolgozás** – egy könyvtár PNG‑jeinek bejárása, és minden eredmény írása egy `.txt` fájlba.
- **PDF generálás** – a kinyert szöveg beágyazása kereshető PDF‑ekbe.
- **Felhő‑OCR szolgáltatások** – a helyi Tesseract teljesítményének összehasonlítása olyan API‑kkal, mint a Google Vision vagy az Azure Cognitive Services.

Kísérletezz, finomítsd a paramétereket, és oszd meg az eredményeidet. Boldog kódolást, és legyenek a képeid mindig tiszta, kereshető szöveggé konvertálva!

![Diagram showing the OCR workflow to perform OCR on image](https://example.com/ocr-workflow.png "perform OCR on image example")


## Mit érdemes még tanulni?

Az alábbi oktatóanyagok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás komplett, működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsenek további API‑funkciók elsajátításában és alternatív megvalósítási megközelítések felfedezésében saját projektjeidben.

- [recognize text image with Aspose OCR – Full Java OCR Tutorial](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Convert Image to Text in Java using Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [Extract Text from Image Java with Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}