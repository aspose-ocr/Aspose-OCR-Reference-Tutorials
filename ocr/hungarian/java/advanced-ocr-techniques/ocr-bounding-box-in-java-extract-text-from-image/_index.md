---
category: general
date: 2026-06-16
description: Az OCR bounding box tutorial Java-ban bemutatja, hogyan lehet szöveget
  kinyerni egy képből, szöveget olvasni a képből, és OCR megbízhatósági pontszámot
  kapni JPG fájlok esetén.
draft: false
keywords:
- ocr bounding box
- extract text from image
- ocr confidence score
- recognize text from jpg
- read text from image
language: hu
og_description: Az OCR körülhatároló doboz Java-ban lehetővé teszi, hogy JPG fájlokból
  szöveget ismerj fel, a képből kinyerd a szöveget, és megtekintsd az OCR megbízhatósági
  pontszámokat – mindezt egy egyszerű kódrészletben.
og_title: OCR körülhatároló keret Java-ban – Szöveg kinyerése képből
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: OCR bounding box tutorial in Java shows how to extract text from image,
    read text from image, and get OCR confidence score for JPG files.
  headline: OCR Bounding Box in Java – Extract Text from Image
  type: TechArticle
tags:
- OCR
- Java
- image-processing
- text-recognition
title: OCR körülhatároló doboz Java-ban – Szöveg kinyerése a képből
url: /hu/java/advanced-ocr-techniques/ocr-bounding-box-in-java-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR Bounding Box in Java – Extract Text from Image

Valaha is elgondolkodtál, hogyan lehet megkapni az **ocr bounding box**-ot minden egyes szövegrészlethez egy Java‑os képen? Ebben az útmutatóban megmutatjuk, hogyan **extract text from image** fájlokból, hogyan **read text from image**, és még az **ocr confidence score**‑t is megtekintheted, miközben **recognize text from jpg** fájlokból dolgozol. A rövid válasz? Néhány sor kód egy modern OCR könyvtárral, valamint egy kis magyarázat arról, hogy miért fontos minden hívás.

Alább egy teljes, azonnal futtatható példát találsz, lépésről‑lépésre bontva, valamint néhány gyakorlati tippet, amelyeket egyszerűen beilleszthetsz a saját projektedbe. A végére képes leszel olyan kimenetet előállítani, mint:

```
Text: "Hello World"  Confidence: 0.97  Box: (x=12, y=45, width=210, height=30)
```

## What You’ll Need

- **Java 11** vagy újabb (az alábbi szintaxis a `var` kulcsszót használja a rövidség kedvéért, de régebbi JDK‑k esetén elhagyható).  
- Egy OCR könyvtár, amely Java API‑t kínál – ebben az útmutatóban a **[Tesseract4J](https://github.com/nguyenq/tess4j)**‑t használjuk, ami egy könnyű wrapper a népszerű Tesseract motor köré.  
- Egy JPEG kép (`.jpg`), amely tiszta, nyomtatott szöveget tartalmaz.  
- A kedvenc IDE‑d (IntelliJ IDEA, Eclipse, VS Code…) – bármelyik megfelel.

Ha hiányzik a könyvtár, csak add hozzá ezt a Maven függőséget:

```xml
<dependency>
    <groupId>net.sourceforge.tess4j</groupId>
    <artifactId>tess4j</artifactId>
    <version>5.4.0</version>
</dependency>
```

Most merüljünk el.

![OCR bounding box example](ocr-bounding-box.png "OCR bounding box example")

## OCR Bounding Box: Setting Up the Engine

Az első dolog, amit meg kell tenned, egy OCR engine példány létrehozása. Gondolj rá úgy, mint a szkenner bekapcsolására, amely később olvassa a pixeleket.

```java
import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;

ITesseract ocrEngine = new Tesseract();          // Step 1 – create the OCR engine
ocrEngine.setDatapath("tessdata");               // point to the language data files
ocrEngine.setLanguage("eng");                    // we’ll work with English for now
```

**Why this matters:**  
A `datapath` beállítása nélkül a Tesseract nem tudja, hol vannak a nyelvi csomagok, és egy titokzatos “Failed loading language” hibát kapsz. A `setLanguage` hívás opcionális, ha csak az alapértelmezett angol csomagra van szükséged, de az explicit megadás világosabbá teszi a kódot a jövőbeli olvasók számára.

## Load the Image You Want to Process

Ezután add meg az engine‑nek a JPEG‑et, amelyet elemezni szeretnél. A könyvtár elfogad egy `File`‑t vagy `BufferedImage`‑t; egyszerűség kedvéért egy `File`‑t használunk.

```java
import java.io.File;

File imageFile = new File("YOUR_DIRECTORY/text_page.jpg");   // Step 2 – load the image
```

**Pro tip:**  
Ha a képed a resources‑ban (pl. egy JAR‑on belül) található, használd a `getResourceAsStream`‑t, és csomagold be `ImageIO.read`‑nel. Így az útmutató helyben és egy csomagolt alkalmazásban is működik.

## Perform OCR Recognition

Most már ténylegesen megkérjük az engine‑t, hogy olvassa el a képet. Az eredmény egy egyszerű szöveges karakterlánc, de mi szeretnénk az **ocr confidence score**‑t és az **ocr bounding box**‑ot is minden sorhoz.

```java
try {
    // Step 3 – run OCR and get a result object with layout data
    var result = ocrEngine.doOCR(imageFile, null);
    // The simple doOCR call returns only text; to get boxes we need the
    // getWords method with a specific page iterator level.
    var words = ocrEngine.getWords(imageFile, ITesseract.PageIteratorLevel.RIL_WORD);
    
    // Step 4 – iterate over each detected word
    for (var word : words) {
        System.out.printf(
            "Text: \"%s\"  Confidence: %.2f  Box: %s%n",
            word.getText(),
            word.getConfidence(),
            word.getBoundingBox().toString()
        );
    }
} catch (TesseractException e) {
    System.err.println("OCR failed: " + e.getMessage());
}
```

**Why we use `getWords` instead of the plain `doOCR`:**  
A `doOCR` visszaadja a nyers karakterláncot, de eldobja a térbeli információkat. A `getWords` hívás `RIL_WORD`‑del (vagy `RIL_TEXTLINE`‑nel, ha sor‑szintű dobozokra van szükséged) egy `Word` objektumok listáját adja vissza, amelyek mindegyike tartalmazza a szöveget, a biztonsági értéket és a körülhatároló téglalapot. Ez a **ocr bounding box** funkció szíve.

## Understanding the Output

A fenti kódrészlet futtatása egy tiszta JPEG‑en hasonló kimenetet eredményez:

```
Text: "Hello"  Confidence: 0.99  Box: java.awt.Rectangle[x=34,y=12,width=112,height=28]
Text: "World"  Confidence: 0.97  Box: java.awt.Rectangle[x=156,y=12,width=98,height=28]
```

- **Text** – a felismert karakterek.  
- **Confidence** – egy 0 és 1 közötti lebegőpontos érték; minél nagyobb, annál biztosabb a motor.  
- **Box** – a téglalap, amely a szót pixelkoordinátákban (x, y, szélesség, magasság) körülhatárolja.  

Most már **read text from image** és pontosan tudod, hol helyezkedik el minden részlet a vásznon – tökéletes kiemeléshez, kivágáshoz vagy downstream NLP pipeline‑okba való továbbításra.

## Edge Cases & Common Pitfalls

| Situation | What to Watch For | Fix / Work‑around |
|-----------|-------------------|-------------------|
| Image is blurry or low‑contrast | Confidence scores drop dramatically (often below 0.6). | Pre‑process with OpenCV: increase contrast, apply thresholding. |
| JPEG contains rotated text | Bounding boxes appear skewed or missing. | Use `ocrEngine.setPageSegMode(ITesseract.PageSegMode.PSM_AUTO_OSD)` to let Tesseract auto‑detect orientation. |
| Large images cause OutOfMemoryError | Java heap fills up when loading big pictures. | Downscale the image before OCR (`ImageIO.read` → `BufferedImage.getScaledInstance`). |
| You need line‑level boxes instead of word‑level | `RIL_WORD` returns per‑word boxes. | Switch to `ITesseract.PageIteratorLevel.RIL_TEXTLINE`. |
| Non‑English characters appear as � | Language data not loaded. | Download the appropriate `.traineddata` file and point `setDatapath` to its folder. |

Az ilyen problémák korai kezelése órákat takarít meg a későbbi hibakeresésben.

## Full Working Example (All Steps in One File)

Below is a self‑contained Java class you can copy‑paste into a `src/main/java` folder and run with `mvn exec:java`. It pulls together everything we discussed.

```java
package com.example.ocrdemo;

import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.ITesseract.RenderedFormat;
import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;
import net.sourceforge.tess4j.Word;

import java.io.File;
import java.util.List;

public class OcrBoundingBoxDemo {

    public static void main(String[] args) {
        // ==== Step 1: Initialize the OCR engine ====
        ITesseract ocrEngine = new Tesseract();
        ocrEngine.setDatapath("tessdata"); // folder containing .traineddata files
        ocrEngine.setLanguage("eng");      // English language pack

        // Optional: improve accuracy for printed text
        ocrEngine.setPageSegMode(ITesseract.PageSegMode.PSM_AUTO);
        ocrEngine.setOcrEngineMode(ITesseract.OEM_TESSERACT_ONLY);

        // ==== Step 2: Load the JPEG you want to read ====
        File imageFile = new File("YOUR_DIRECTORY


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Extract Text from Image Java with Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Extract Text Images – OCR Basics with Aspose.OCR for Java](/ocr/english/java/ocr-basics/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}