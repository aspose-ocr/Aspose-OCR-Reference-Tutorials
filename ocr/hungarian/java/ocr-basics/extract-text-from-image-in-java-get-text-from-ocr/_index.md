---
category: general
date: 2026-05-25
description: Szöveg kinyerése képből Java-ban OCR-rel. Tanulja meg, hogyan töltsön
  be képet OCR-hez, hogyan ismerje fel a szöveget a fényképen, és hogyan kapja meg
  a szöveget OCR-rel egy egyszerű kódrészlet segítségével.
draft: false
keywords:
- extract text from image
- get text from ocr
- recognize text from photo
- java image to text
- load image for ocr
language: hu
og_description: Képről szöveg kinyerése Java-ban lépésről‑lépésre útmutatóval. Tanulja
  meg, hogyan töltsön be képet OCR-hez, ismerje fel a szöveget a fényképről, és hatékonyan
  szerezze meg a szöveget az OCR-ből.
og_title: Kép szövegének kinyerése Java-ban – Szöveg lekérése OCR-rel
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: Extract text from image in Java using OCR. Learn how to load image
    for OCR, recognize text from photo, and get text from OCR with a simple code example.
  headline: Extract Text from Image in Java – Get Text from OCR
  type: TechArticle
- description: Extract text from image in Java using OCR. Learn how to load image
    for OCR, recognize text from photo, and get text from OCR with a simple code example.
  name: Extract Text from Image in Java – Get Text from OCR
  steps:
  - name: '**Wrong language setting** – If you forget step 2, the engine defaults
      to English, turning Cyrillic characters into gibberish. Always double‑check
      the language code.'
    text: '**Wrong language setting** – If you forget step 2, the engine defaults
      to English, turning Cyrillic characters into gibberish. Always double‑check
      the language code.'
  - name: '**Image quality matters** – Low‑resolution or blurry photos will degrade
      accuracy. Pre‑process with contrast enhancement or binarization if needed.'
    text: '**Image quality matters** – Low‑resolution or blurry photos will degrade
      accuracy. Pre‑process with contrast enhancement or binarization if needed.'
  - name: '**File path quirks** – On Windows, backslashes need escaping (`C:\images\file.jpg`).
      Using `Path.of(...)` from `java.nio.file` sidesteps this.'
    text: '**File path quirks** – On Windows, backslashes need escaping (`C:\images\file.jpg`).
      Using `Path.of(...)` from `java.nio.file` sidesteps this.'
  - name: '**Memory leaks** – `OcrEngine` holds native resources. Call `ocrEngine.dispose()`
      when you’re done, especially in long‑running services.'
    text: '**Memory leaks** – `OcrEngine` holds native resources. Call `ocrEngine.dispose()`
      when you’re done, especially in long‑running services.'
  - name: '**Thread safety** – The engine isn’t thread‑safe out of the box. Create
      a separate instance per thread or synchronize access.'
    text: '**Thread safety** – The engine isn’t thread‑safe out of the box. Create
      a separate instance per thread or synchronize access.'
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: Szöveg kinyerése képből Java-ban – Szöveg lekérése OCR-rel
url: /hu/java/ocr-basics/extract-text-from-image-in-java-get-text-from-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Képről szöveg kinyerése Java‑val – Szöveg lekérése OCR‑rel

Volt már, hogy **szöveget kellett kinyerni egy képből**, de nem tudtad, melyik Java‑könyvtárat válaszd? Nem vagy egyedül. Legyen szó nyugták digitalizálásáról, sorozatszámok kinyeréséről termékfotókból, vagy csak egy szórakoztató mellékprojekt kipróbálásáról, a kép szerkeszthető szöveggé alakítása gyakori akadály.

Ebben az útmutatóban egy teljes, azonnal futtatható példán keresztül mutatjuk be, hogyan **tölts be képet OCR‑hez**, hogyan konfiguráld a motort, és végül hogyan **ismerd fel a szöveget a fényképről**, hogy **szöveget kapj OCR‑rel** néhány kódsorral. Nincs homályos hivatkozás – minden, amire szükséged van, itt van.

## Mit fogsz megtanulni

* Hogyan állíts be egy könnyűsúlyú OCR‑motort Java‑ban.  
* A pontos lépéseket a **kép betöltéséhez OCR‑hez** és a különböző fájlutak kezeléséhez.  
* Miért fontos a nyelv beállítása, ha **szöveget szeretnél kinyerni a képből**, amely nem angol.  
* Hogyan jelenítsd meg biztonságosan az eredményt, és mit tegyél, ha a motor semmit sem ad vissza.  
* Néhány profi tipp a leggyakoribb buktatók elkerüléséhez.

Az útmutató végére egy önálló programod lesz, amely egy JPEG‑et (vagy PNG‑t) olvas be, amely ukrán karaktereket tartalmaz, és a felismert karakterláncot a konzolra írja. Nyugodtan cseréld le a nyelvet vagy a képet – minden moduláris.

---

![Diagram showing the flow of extracting text from image using Java OCR engine](/images/extract-text-from-image-java.png)

*Alt text: Flow diagram of extract text from image process in Java.*

## Előfeltételek

* **Java Development Kit (JDK) 11+** – a kód a modern modulrendszert használja, de régebbi verziók kisebb módosítással működnek.  
* **Maven vagy Gradle** – az OCR‑könyvtár lehúzásához (a példában a **Asprise OCR**‑t használjuk, amely könnyű, fejlesztéshez ingyenes).  
* Egy minta képfájl (pl. `ukrainian_sign.jpg`), amelyet a program el tud olvasni.  
* Alapvető ismeretek a Java `main` metódusáról és a kivételkezelésről.

Ha ezek megvannak, már indulhatsz. Ha nem, töltsd le a JDK‑t az Oracle‑tól vagy az AdoptOpenJDK‑tól, és állíts be egy egyszerű Maven‑projektet – semmi bonyolult.

---

## 1. lépés: Add hozzá az OCR függőséget

Először mondd meg a build‑eszköznek, hogy töltse le az OCR motort. Maven‑hez illeszd be ezt a `pom.xml`‑be:

```xml
<dependency>
    <groupId>com.asprise.ocr</groupId>
    <artifactId>asprise-ocr</artifactId>
    <version>1.0.2</version>
</dependency>
```

Ha Gradlet használsz, az ekvivalens:

```gradle
implementation 'com.asprise.ocr:asprise-ocr:1.0.2'
```

Ezek a koordináták egy kompakt JAR‑t hoznak be, amely tartalmazza az `OcrEngine`, `OcrLanguage` és a segédosztályokat, amelyeket használni fogunk. Alap latin és cirill betűkészletekhez nem szükségesek extra natív binárisok.

---

## 2. lépés: Hozz létre egy Java osztályt a **Képről szöveg kinyeréséhez**

Most megírjuk a tényleges programot. Mentsd el a következőt `ExtractTextDemo.java` néven a `src/main/java/com/example/ocr/` könyvtárba.

```java
package com.example.ocr;

import com.asprise.ocr.OcrEngine;
import com.asprise.ocr.OcrLanguage;

/**
 * Demonstrates how to extract text from image using Asprise OCR.
 * The example loads a JPEG, sets the language to Ukrainian,
 * runs recognition, and prints the result.
 */
public class ExtractTextDemo {

    public static void main(String[] args) {
        // ---- 1️⃣  Initialize the OCR engine ---------------------------------
        OcrEngine ocrEngine = new OcrEngine();

        // ---- 2️⃣  Configure the engine to recognize Ukrainian text -----------
        // This is crucial if your image contains non‑Latin characters.
        ocrEngine.getEngineOptions().setLanguage(OcrLanguage.UKRAINIAN);

        // ---- 3️⃣  Load the image that contains Ukrainian characters ----------
        // Replace the path with the location of your own picture.
        String imagePath = "YOUR_DIRECTORY/ukrainian_sign.jpg";
        try {
            ocrEngine.getImage().loadFromFile(imagePath);
        } catch (Exception e) {
            System.err.println("Failed to load image: " + e.getMessage());
            return;
        }

        // ---- 4️⃣  Perform OCR recognition and obtain the extracted text -------
        String recognizedText;
        try {
            recognizedText = ocrEngine.recognize().getText();
        } catch (Exception e) {
            System.err.println("Recognition error: " + e.getMessage());
            return;
        }

        // ---- 5️⃣  Output the recognized text to the console -------------------
        System.out.println("=== OCR Result ===");
        System.out.println(recognizedText);
    }
}
```

### Miért működik ez a felépítés

* **Külön számozott blokkok** teszik könnyen követhetővé a folyamatot, különösen, ha a **kép betöltését OCR‑hez** vagy a **szöveg felismerését a fényképről** keresed.  
* A `try/catch` a kép betöltése és a felismerés körül biztosítja, hogy a program elegánsan hibázzon – hasznos, ha a fájlútvonal hibás vagy az OCR‑motor nem találja a nyelvi adatokat.  
* A nyelv korai beállítása (2. lépés) drámaian javítja a pontosságot nem‑angol írásrendszerek esetén. Ha később **java image to text** más nyelvekre van szükséged, egyszerűen cseréld az `OcrLanguage.UKRAINIAN`‑t `OcrLanguage.ENGLISH`, `FRENCH` stb.-re.

---

## 3. lépés: Építsd és futtasd a programot

A projekt gyökeréből hajtsd végre:

```bash
mvn clean compile exec:java -Dexec.mainClass="com.example.ocr.ExtractTextDemo"
```

Vagy ha Gradlet használsz:

```bash
./gradlew run --args="com.example.ocr.ExtractTextDemo"
```

Feltételezve, hogy a `ukrainian_sign.jpg` a *«Ласкаво просимо»* (ukránul „Üdvözlet”) szöveget tartalmazza, valami ilyesmit kell látnod:

```
=== OCR Result ===
Ласкаво просимо
```

Ez a kimenet megerősíti, hogy sikeresen **kivettél szöveget a képből** és **szöveget kaptál OCR‑rel** egyetlen futtatás során.

---

## 4. lépés: Finomhangold a munkafolyamatot – **Java Image to Text** valós projektekben

Bár a demó minimalista, a valós alkalmazások gyakran igényelnek többet:

| Szenárió | Mit kell módosítani | Indoklás |
|----------|---------------------|----------|
| **Kötegelt feldolgozás** | `List<Path>`‑on iterálj, és minden eredményt tárold adatbázisban. | Csökkenti a manuális munkát, ha több száz fénykép áll rendelkezésre. |
| **Különböző képformátumok** | Használd az `ImageIO.read(new File(path))`‑t előfeldolgozáshoz, majd add át a `BufferedImage`‑t az `ocrEngine.getImage().loadFromBufferedImage(bufImg)`‑nek. | Kezeli a PNG‑t, BMP‑t vagy akár a PDF‑eket konverzió után. |
| **Teljesítményhangolás** | Hívd meg az `ocrEngine.getEngineOptions().setSpeed(OcrEngine.Speed.FAST)`‑t, ha elfogadható egy kicsit alacsonyabb pontosság. | Gyorsítja a felismerést alacsony teljesítményű hardveren. |
| **Utófeldolgozás** | Vágd le a felesleges szóközöket, cseréld ki a gyakori OCR‑hibákat (`0` → `O`, `1` → `I`). | Javítja a további adatminőséget. |

Ezek a variációk megtartják a központi elképzelést – **szöveg felismerése a fényképről** – miközben rugalmasságot biztosítanak a termelési környezethez.

---

## Gyakori hibák és profi tippek

1. **Helytelen nyelvi beállítás** – Ha kihagyod a 2. lépést, a motor alapértelmezés szerint angolt használ, és a cirill karaktereket értelmetlen szöveggé alakítja. Mindig ellenőrizd a nyelvkódot.  
2. **Képminőség számít** – Alacsony felbontású vagy elmosódott fotók csökkentik a pontosságot. Szükség esetén előfeldolgozhatod kontrasztjavítással vagy binarizálással.  
3. **Fájlútvonalak sajátosságai** – Windowson a backslash‑eknek escape‑elni kell (`C:\\images\\file.jpg`). A `Path.of(...)` használata a `java.nio.file`‑ból megkerüli ezt a problémát.  
4. **Memóriaszivárgás** – Az `OcrEngine` natív erőforrásokat tart fenn. Hívd meg az `ocrEngine.dispose()`‑t, amikor befejezted, különösen hosszú‑távú szolgáltatásoknál.  
5. **Szálbiztonság** – A motor önmagában nem szálbiztos. Hozz létre külön példányt szálanként, vagy szinkronizáld a hozzáférést.

---

## Teljes, működő példa (All‑In‑One)

Az alábbi egyetlen fájl, amelyet bármely IDE‑be beilleszthetsz. Tartalmazza a `dispose()` hívást és egy kis segítő metódust, hogy a kód egy kicsit tisztább legyen.

```java
package com.example.ocr;

import com.asprise.ocr.OcrEngine;
import com.asprise.ocr.OcrLanguage;
import java.nio.file.Path;

/**
 * Complete, runnable demo that extracts text from an image using Java OCR.
 */
public class FullDemo {

    public static void main(String[] args) {
        // Path to the image – change this to your own file.
        Path imgPath = Path.of("YOUR_DIRECTORY/ukrainian_sign.jpg");

        // Run the OCR workflow and capture the output.
        String result = extractTextFromImage(imgPath, OcrLanguage.UKRAINIAN);
        if (result != null) {
            System.out.println("=== OCR Result ===");
            System.out.println(result);
        }
    }

    /**
     * Core method that encapsulates the 5‑step OCR process.
     *
     * @param imagePath Path to the image file.
     * @param language  Desired OCR language.
     * @return Recognized text, or {@code null} if something went wrong.
     */
    private static String extractTextFromImage(Path imagePath, OcrLanguage language) {
        OcrEngine engine = new OcrEngine();
        try {
            // 1️⃣ Set language
            engine.getEngineOptions().setLanguage(language);

            // 2️⃣ Load image
            engine.getImage().loadFromFile(imagePath.toString());

            // 3️⃣ Recognize and return text
            return engine.recognize().getText();
        } catch (Exception e) {
            System.err.println("Error during OCR: " + e.getMessage());
            return null;
        } finally {
            // 4️⃣ Release native resources
            engine.dispose();
        }
    }
}
```

A program futtatása ugyanazt a konzolkimenetet adja, mint korábban. Nyugodtan cseréld le az `OcrLanguage.UKRAINIAN`‑t `OcrLanguage.ENGLISH`‑ra vagy bármely más támogatott nyelvre, hogy lásd, hogyan alkalmazkodik a motor.

---

## Összegzés

Áttekintettük mindazt, amire szükséged van a **kép szöveggé alakításához** Java‑val: az OCR‑függőség hozzáadásától a **kép betöltéséig OCR‑hez**,


## Kapcsolódó oktatóanyagok

- [recognize text image with Aspose OCR – Full Java OCR Tutorial](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Convert Image to Text in Java using Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}