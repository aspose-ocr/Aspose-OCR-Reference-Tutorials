---
category: general
date: 2026-10-11
description: Tanulja meg, hogyan végezhet OCR-t egy PNG képen Java-ban, hogyan nyerhet
  ki szöveget a képből, és hogyan konvertálhatja a képet szöveggé egy egyszerű OcrEngine
  példával.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to perform OCR
- extract text from image
- recognize text from PNG
- load image java
- convert image to text
language: hu
lastmod: 2026-10-11
og_description: Hogyan végezzünk OCR-t egy PNG képen Java-ban, szöveget nyerjünk ki
  a képből, és alakítsuk át a képet szöveggé egy tömör, azonnal futtatható példával.
og_image_alt: Diagram showing how to perform OCR on a PNG image using Java
og_title: Hogyan végezzünk OCR-t egy PNG képen Java-ban – teljes útmutató
schemas:
- author: Aspose
  dateModified: '2026-10-11'
  description: Learn how to perform OCR on a PNG image in Java, extract text from
    image and convert image to text with a simple OcrEngine example.
  headline: How to perform OCR on a PNG image in Java
  type: TechArticle
- description: Learn how to perform OCR on a PNG image in Java, extract text from
    image and convert image to text with a simple OcrEngine example.
  name: How to perform OCR on a PNG image in Java
  steps:
  - name: 4.1 Handling low‑resolution PNGs
    text: 'Tesseract performs best on images with at least 300 DPI. If your source
      PNG is smaller, upscale it before OCR:'
  - name: 4.2 Extracting non‑English text
    text: 'To **extract text from image** that contains other languages, download
      the appropriate `.traineddata` files and set the language code:'
  - name: 4.3 Batch processing multiple PNGs
    text: 'If you need to **recognize text from PNG** files in a folder, iterate over
      the directory:'
  - name: 4.4 Dealing with OCR errors
    text: 'Typical OCR mistakes include misreading `0` (zero) as `O` or `1` as `l`.
      Post‑processing with regular expressions can clean the result:'
  type: HowTo
tags:
- OCR
- Java
- Image Processing
- Text Extraction
title: Hogyan hajtsunk végre OCR-t egy PNG képen Java-ban
url: /hu/java/ocr-basics/how-to-perform-ocr-on-a-png-image-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan végezzünk OCR-t egy PNG képen Java-ban

Ha **OCR-t kell végrehajtani** egy képfájlon, akkor a **hogyan kell OCR-t végrehajtani** Java-ban elsajátítása elengedhetetlen számos automatizálási feladathoz. Akár nyugtákat digitalizálsz, beolvasott dokumentumokat indexelsz, vagy kereshető fényképarchívumot építesz, a **szöveg kinyerése a képből** fájlokból rengeteg manuális órát takarít meg.

Ez a bemutató egy teljes, futtatható megoldást mutat be, amely betölt egy PNG-t, futtat egy OCR motort, és **szöveg felismerése PNG-ből** fájlokból. Emellett megmutatjuk, hogyan **kép átalakítása szöveggé**, és hogyan kezeljünk gyakori buktatókat, mint az alacsony felbontású bemenet vagy a nem ASCII karakterek.

## Mit fogsz elérni

* **load image java** kód, amely PNG-t olvas le a lemezről,
* egy könnyűsúlyú OCR motor inicializálása,
* **extract text from image** és az eredmény kiírása a konzolra,
* a megoldás adaptálása más képfájlformátumokra vagy kötegelt feldolgozásra.

Nincs szükség külső szolgáltatásokra – csak egy nyílt forráskódú OCR könyvtárra (Tess4J) és a Java SE futtatókörnyezetre.

---

## Előkövetelmények

* Java 17 vagy újabb (a kód JDK 17‑kel fordul).
* Maven vagy Gradle a függőségkezeléshez.
* Alapvető ismeretek a parancssorról és a választott IDE-ről.
* A `tess4j` könyvtár (a Tesseract Java wrapper). Add the following Maven dependency:

```xml
<dependency>
    <groupId>net.sourceforge.tess4j</groupId>
    <artifactId>tess4j</artifactId>
    <version>5.4.0</version>
</dependency>
```

If you use Gradle, the equivalent is:

```gradle
implementation 'net.sourceforge.tess4j:tess4j:5.4.0'
```

Szükséged lesz a Tesseract adatfájlokra (`.traineddata`). Töltsd le az angol adatcsomagot a hivatalos tárolóból, és helyezd el a projekt gyökerében található `tessdata` nevű mappában.

---

## 1. lépés: Kép betöltése Java-ban

A PNG betöltése egyszerű a szabványos `ImageIO` osztállyal. Az alábbi kód bemutatja a **load image java**-t egy biztonságos, kivétel‑tudatos módon:

```java
import java.awt.image.BufferedImage;
import java.io.File;
import javax.imageio.ImageIO;

/**
 * Reads a PNG file from the given path and returns a BufferedImage.
 *
 * @param path absolute or relative path to the PNG file
 * @return BufferedImage representation of the file
 * @throws Exception if the file cannot be read or is not a PNG
 */
private static BufferedImage loadPng(String path) throws Exception {
    File imgFile = new File(path);
    if (!imgFile.exists()) {
        throw new IllegalArgumentException("File not found: " + path);
    }
    BufferedImage img = ImageIO.read(imgFile);
    if (img == null) {
        throw new IllegalArgumentException("Unsupported image format or corrupt file: " + path);
    }
    return img;
}
```

**Miért fontos:** A `ImageIO.read` automatikusan felismeri a képfájltípust, de kifejezetten ellenőrizzük a `null` értéket, hogy elkerüljük a csendes hibákat, ha a PNG sérült. Ez a minta a legjobb gyakorlat, amikor **load image java**-t használsz OCR-hez.

---

## 2. lépés: OCR motor inicializálása

A Tess4J a natív Tesseract binárist burkolja, egy egyszerű Java API-t biztosítva. Az alábbi metódus létrehoz egy `Tesseract` példányt, a `tessdata` mappára mutat, és az angol nyelvet állítja be:

```java
import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.Tesseract;

/**
 * Configures and returns a ready‑to‑use Tesseract instance.
 *
 * @return configured ITesseract object
 */
private static ITesseract createOcrEngine() {
    ITesseract tesseract = new Tesseract();
    // Path to the folder that contains .traineddata files
    tesseract.setDatapath("tessdata");
    // Language code – "eng" for English; you can add more languages later
    tesseract.setLanguage("eng");
    // Optional: increase OCR accuracy for PNGs with low DPI
    tesseract.setOcrEngineMode(ITesseract.OEM_DEFAULT);
    return tesseract;
}
```

**Miért így teszünk:** A motor egyszeri inicializálása és többszöri újrahasználata több kép esetén csökkenti a betöltési költséget. A `setOcrEngineMode` hívás a alapértelmezett módot választja, ami a legtöbb PNG-nél jól működik. Ha zajos beolvasásokat tapasztalsz, kísérletezhetsz más módokkal (pl. `OEM_LSTM_ONLY`).

---

## 3. lépés: OCR végrehajtása és **szöveg felismerése PNG-ből**

Most kombináljuk a képtöltőt és az OCR motort. Az alábbi metódus OCR-t futtat egy `BufferedImage`-en, és visszaadja a kinyert karakterláncot:

```java
/**
 * Runs OCR on the supplied image and returns the recognized text.
 *
 * @param image BufferedImage containing the PNG to process
 * @param tesseract configured OCR engine
 * @return plain‑text result of OCR
 * @throws Exception if OCR fails
 */
private static String extractText(BufferedImage image, ITesseract tesseract) throws Exception {
    // Tess4J can directly accept a BufferedImage
    return tesseract.doOCR(image);
}
```

**Teljes futtatható példa**

```java
import java.awt.image.BufferedImage;
import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.TesseractException;

public class OcrDemo {

    public static void main(String[] args) {
        try {
            // 1️⃣ Load the PNG file
            BufferedImage image = loadPng("sample.png");

            // 2️⃣ Create and configure the OCR engine
            ITesseract ocrEngine = createOcrEngine();

            // 3️⃣ Recognize text from PNG
            String recognizedText = extractText(image, ocrEngine);

            // 4️⃣ Display the result – this is the **convert image to text** step
            System.out.println("=== OCR RESULT ===");
            System.out.println(recognizedText);
        } catch (Exception e) {
            System.err.println("Error during OCR processing:");
            e.printStackTrace();
        }
    }

    // ----- Helper methods from previous steps -----
    // loadPng, createOcrEngine, extractText (copy-pasted here for completeness)
    // ... (methods omitted for brevity; see the sections above) ...
}
```

**Várt kimenet**

```
=== OCR RESULT ===
Invoice #12345
Date: 2024‑09‑30
Total: $1,234.56
Thank you for your business!
```

A konzol a `sample.png`-ből az OCR motor által kinyert pontos karaktereket fogja mutatni. Ha a PNG csak egy szót tartalmaz, a kimenet az lesz, amely szó egy újsorral követve.

---

## 4. lépés: Gyakori változatok és szélső esetek

### 4.1 Alacsony felbontású PNG-k kezelése

A Tesseract a legalább 300 DPI-s képeken működik a legjobban. Ha a forrás PNG kisebb, méretezze fel OCR előtt:

```java
import java.awt.Graphics2D;
import java.awt.Image;
import java.awt.RenderingHints;

private static BufferedImage upscale(BufferedImage src, int scaleFactor) {
    int width = src.getWidth() * scaleFactor;
    int height = src.getHeight() * scaleFactor;
    Image tmp = src.getScaledInstance(width, height, Image.SCALE_SMOOTH);
    BufferedImage resized = new BufferedImage(width, height, BufferedImage.TYPE_INT_ARGB);
    Graphics2D g2d = resized.createGraphics();
    g2d.setRenderingHint(RenderingHints.KEY_INTERPOLATION,
                         RenderingHints.VALUE_INTERPOLATION_BICUBIC);
    g2d.drawImage(tmp, 0, 0, null);
    g2d.dispose();
    return resized;
}
```

Használd az `upscale(image, 2)` függvényt az `extractText` hívása előtt a pontosság javítása érdekében.

### 4.2 Nem angol szöveg kinyerése

A **extract text from image**-hez, amely más nyelveket tartalmaz, töltsd le a megfelelő `.traineddata` fájlokat, és állítsd be a nyelvkódot:

```java
tesseract.setLanguage("eng+deu"); // English + German
```

### 4.3 Tömeges feldolgozás több PNG-vel

Ha egy mappában lévő **recognize text from PNG** fájlokból kell szöveget kinyerni, iterálj a könyvtáron:

```java
File folder = new File("pngs/");
for (File file : folder.listFiles((d, name) -> name.toLowerCase().endsWith(".png"))) {
    BufferedImage img = loadPng(file.getPath());
    String text = extractText(img, ocrEngine);
    System.out.println("File: " + file.getName());
    System.out.println(text);
}
```

### 4.4 OCR hibák kezelése

A tipikus OCR hibák közé tartozik a `0` (nulla) `O`-ként vagy az `1` `l`-ként való félreolvasása. A reguláris kifejezésekkel történő utófeldolgozás tisztíthatja az eredményt:

```java
String cleaned = recognizedText.replaceAll("[\\r\\n]+", " ").trim();
```

---

## Pro tippek a megbízható OCR-hez Java-ban

| Tipp | Ok |
|-----|--------|
| **Használj veszteségmentes PNG-t** | A JPEG tömörítési hibái összezavarhatják a motort. |
| **Vágd le a fehér szegélyeket** | A felesleges üreshely növeli a feldolgozási időt és hamis pozitív eredményeket okozhat. |
| **Állítsd be a `tesseract.setPageSegMode(ITesseract.PSM_AUTO)`-t** csak akkor, ha a layout ismeretlen; egyébként válassz egy konkrét módot (pl. `PSM_SINGLE_BLOCK`). | |
| **Cache-eld az `ITesseract` példányt** | |

## Mit érdemes még megtanulni?

Az alábbi bemutatók szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljesen működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsenek elsajátítani további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [How to Read Text from an Image in Java Using Aspose OCR – Complete Guide](/ocr/english/java/ocr-basics/read-text-from-image-in-java-complete-aspose-ocr-guide/)
- [How to Use OCR in Java – Recognize Text from Image Quickly](/ocr/english/java/ocr-operations/how-to-use-ocr-in-java-recognize-text-from-image-quickly/)
- [Batch Image OCR in Java – Extract Text from PNG Files Fast](/ocr/english/java/ocr-operations/batch-image-ocr-in-java-extract-text-from-png-files-fast/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}