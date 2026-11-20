---
category: general
date: 2026-08-18
description: Hogyan engedélyezzük a GPU-t az OCR-hez Java-ban, és gyorsan felismerjük
  a képen lévő szöveget, kinyerjük a szöveget JPG-ből, szűrőt adunk hozzá, valamint
  beállítjuk a nyelvet az Aspose.OCR segítségével.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to enable gpu
- recognize image text
- extract text jpg
- how to add filter
- how to set language
language: hu
lastmod: 2026-08-18
og_description: Hogyan engedélyezzük a GPU-t az OCR-hez Java-ban, és azonnal felismerjük
  a képen lévő szöveget, kinyerjük a szöveget JPG-ből, szűrőt adunk hozzá, valamint
  beállítjuk a nyelvet az Aspose.OCR használatával.
og_image_alt: Screenshot showing Java code that enables GPU for OCR with Aspose.OCR
og_title: Hogyan aktiváljuk a GPU-t az OCR-hez Java-ban – teljes Aspose.OCR útmutató
schemas:
- author: Aspose
  dateModified: '2026-08-18'
  description: How to enable GPU for OCR in Java and quickly recognize image text,
    extract text JPG, add filter, and set language with Aspose.OCR.
  headline: How to enable GPU for OCR in Java using Aspose.OCR
  type: TechArticle
- description: How to enable GPU for OCR in Java and quickly recognize image text,
    extract text JPG, add filter, and set language with Aspose.OCR.
  name: How to enable GPU for OCR in Java using Aspose.OCR
  steps:
  - name: 3.1 Set the OCR language
    text: '```java // Choose the language for recognition – this is the “how to set
      language” step engine.setLanguage(OcrLanguage.ENGLISH); ```'
  - name: 3.2 Add a preprocessing filter
    text: 'Noise, compression artifacts, or uneven lighting can hurt accuracy. Adding
      a denoise filter is the typical **how to add filter** approach:'
  - name: Expected output
    text: '``` Recognized text: The quick brown fox jumps over the lazy dog. ```'
  type: HowTo
tags:
- OCR
- Java
- Aspose
- GPU acceleration
title: Hogyan engedélyezzük a GPU-t az OCR-hez Java-ban az Aspose.OCR használatával
url: /hu/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan engedélyezzük a GPU-t az OCR-hez Java-ban az Aspose.OCR használatával

Ha **hogyan engedélyezzük a GPU-t** az OCR-hez Java-ban, ez az útmutató végigvezet a pontos lépéseken. A GPU gyorsítás engedélyezése lehetővé teszi, hogy **képszöveget ismerjünk fel** akár többször gyorsabban, ami elengedhetetlen, ha **JPG fájlokból kell szöveget kinyerni** nagy mennyiségben. Emellett bemutatjuk a **szűrő hozzáadásának módját**, a **nyelv beállítását**, és a végső eredmény lekérését.

Az oktatóanyag végére egy teljes, futtatható programot kapsz, amely:

* Elindítja az Aspose.OCR motorját GPU támogatással.  
* Beállítja az OCR nyelvet (pl. English).  
* Zajcsökkentő szűrőt alkalmaz a pontosság javításához.  
* Betölti a JPEG képet, futtatja a felismerést, és kiírja a kinyert szöveget.

> **Előfeltétel:** Java 17 vagy újabb, Maven, és egy Aspose.OCR for Java licenc (az ingyenes próba a kiértékeléshez megfelelő).

![Hogyan engedélyezzük a GPU-t az OCR-hez Java-ban](/images/ocr-gpu.png){alt="Hogyan engedélyezzük a GPU-t az OCR-hez Java-ban"}

## Amire szükséged lesz

| Elem | Ok |
|------|----|
| **Java Development Kit (JDK) 17+** | Szükséges a példa lefordításához és futtatásához. |
| **Maven** | Egyszerűsíti az Aspose.OCR függőségkezelését. |
| **Aspose.OCR for Java** | Biztosítja az `OcrEngine` osztályt és a GPU támogatást. |
| **A sample JPEG image** (`sample.jpg`) | A **JPG szöveg kinyerés** bemutatására használjuk. |
| **GPU‑compatible hardware** (optional but recommended) | Lehetővé teszi a teljesítményjavulást, amelyet beállítunk. |

## 1. lépés: Maven projekt beállítása

Hozz létre egy új Maven projektet (vagy adj hozzá egy meglévőhöz), és add hozzá az Aspose.OCR függőséget:

```xml
<!-- pom.xml -->
<project xmlns="http://maven.apache.org/POM/4.0.0" ...>
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>ocr-gpu-demo</artifactId>
    <version>1.0.0</version>
    <properties>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
    </properties>

    <dependencies>
        <!-- Aspose.OCR for Java -->
        <dependency>
            <groupId>com.aspose</groupId>
            <artifactId>aspose-ocr</artifactId>
            <version>23.12</version> <!-- Use the latest stable version -->
        </dependency>
    </dependencies>
</project>
```

> **Pro tipp:** Tartsd naprakészen a verziószámot; az újabb kiadások javítják a GPU kezelését és új nyelvi csomagokat adnak hozzá.

## 2. lépés: Az OCR motor inicializálása és **hogyan engedélyezzük a GPU-t**

A megoldás központja a `OcrEngine`. A példányosítása egyszerű, de kifejezetten be kell kapcsolni a GPU gyorsítást:

```java
import com.aspose.ocr.*;

public class HelloWorldOcr {
    public static void main(String[] args) throws Exception {
        // Step 2.1: Initialize the OCR engine
        OcrEngine engine = new OcrEngine();

        // Step 2.2: Enable GPU acceleration (this is the “how to enable GPU” part)
        engine.setUseGpu(true); // <-- GPU is now active

        // Step 2.3: Configure language and preprocessing filter (covered later)
```

**Miért engedélyezzük a GPU-t?**  
Amikor a `setUseGpu(true)` hívás megtörténik, az Aspose.OCR a nehéz képfeldolgozó magokat a grafikus kártyára terheli át. Egy modern NVIDIA/AMD GPU-n a felismerési sebesség ~200 ms/ről < 80 ms-re nőhet oldalanként, ami drámaian csökkenti a teljes feldolgozási időt nagy kötegek esetén.

## 3. lépés: **Hogyan állítsuk be a nyelvet** és **hogyan adjunk hozzá szűrőt**

### 3.1 Az OCR nyelv beállítása

```java
        // Choose the language for recognition – this is the “how to set language” step
        engine.setLanguage(OcrLanguage.ENGLISH);
```

Az Aspose.OCR több mint 100 nyelvi csomaggal érkezik. Cseréld le az `ENGLISH`-t `FRENCH`, `CHINESE_SIMPLIFIED` stb.-re, hogy megfeleljen a forrásanyagnak.

### 3.2 Előfeldolgozó szűrő hozzáadása

A zaj, tömörítési hibák vagy egyenetlen megvilágítás ronthatja a pontosságot. Egy zajcsökkentő szűrő hozzáadása a tipikus **hogyan adjunk hozzá szűrőt** megközelítés:

```java
        // Add a denoising filter to improve OCR quality – “how to add filter”
        engine.addPreprocessFilter(FilterType.DENOISE);
```

Más hasznos szűrők közé tartozik a `FilterType.CONTRAST`, `FilterType.BRIGHTNESS` és a `FilterType.BINARIZE`. Több szűrőt is láncolhatsz úgy, hogy többször meghívod az `addPreprocessFilter`-t.

## 4. lépés: Kép betöltése – **JPG szöveg kinyerés**

Most a motorra mutatunk a feldolgozni kívánt JPEG fájlt:

```java
        // Load the JPEG image – this demonstrates “extract text JPG”
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.jpg"));
```

Cseréld le a `YOUR_DIRECTORY`-t a tényleges útvonalra, ahol a `sample.jpg` található. Az Aspose.OCR támogatja a PNG, BMP, TIFF és PDF formátumokat is; ugyanaz a hívás működik ezeknél a formátumoknál is.

## 5. lépés: OCR végrehajtása és **képszöveg felismerése**

A motor konfigurálása után hívd meg a felismerési rutint:

```java
        // Run the OCR operation – “recognize image text”
        engine.recognize();

        // Retrieve the recognized text
        String text = engine.getText();
        System.out.println("Recognized text: " + text);
    }
}
```

A `recognize()` metódus a képet a GPU-n (ha engedélyezve van) dolgozza fel, és feltölti a belső szövegpuffert. A `getText()` egy egyszerű szöveges `String`-et ad vissza, amelyet fájlba, adatbázisba írhat vagy továbbíthat a downstream NLP csővezetékeknek.

### Várható kimenet

```
Recognized text: The quick brown fox jumps over the lazy dog.
```

Ha a kép több sorból áll, a visszaadott string tartalmazza a sortörés karaktereket (`\n`), megőrizve az eredeti elrendezést.

## 6. lépés: GPU használat ellenőrzése (opcionális)

Annak megerősítésére, hogy a GPU valóban használatban van, engedélyezd az Aspose naplózást:

```java
        // Enable diagnostic logging (optional)
        engine.setLogLevel(com.aspose.ocr.logging.LogLevel.DEBUG);
        engine.setLogFile("ocr-debug.log");
```

Ellenőrizd a `ocr-debug.log`-ot egy futtatás után; olyan bejegyzéseket kell látnod, mint `GPU device: NVIDIA GeForce RTX 3080` és `Processing time (GPU): 78 ms`. Ha a napló **CPU**-t említ, ellenőrizd a driver telepítését és hogy a `setUseGpu(true)` hívás jelen van.

## Gyakori buktatók és hogyan kerüld el őket

| Tünet | Valószínű ok | Javítás |
|-------|--------------|---------|
| **`java.lang.UnsatisfiedLinkError: no aspose_ocr_native`** | Hiányzó natív GPU könyvtárak | Telepítsd a legújabb GPU drivert és győződj meg róla, hogy az `aspose-ocr` natív binárisok a `java.library.path`-on vannak. |
| **Gyenge pontosság sötét képeken** | Nincs előfeldolgozó szűrő | Add `engine.addPreprocessFilter(FilterType.BRIGHTNESS)` vagy növeld a `FilterType.CONTRAST` értékét. |
| **`OutOfMemoryError` nagy kötegeknél** | GPU memória kimerülés | Feldolgozd a képeket kisebb kötegekben vagy tiltsd le a GPU-t (`engine.setUseGpu(false)`) nagyon nagy felbontások esetén. |
| **Helytelen nyelvi kimenet** | Helytelen nyelv beállítása | Ellenőrizd, hogy a `engine.setLanguage(OcrLanguage.YOUR_LANGUAGE)` megegyezik a forrás szövegével. |

## Teljes, futtatható példa

Az alábbiakban a teljes Java osztály található, amelyet beilleszthetsz a `src/main/java/com/example/HelloWorldOcr.java` fájlba. Tartalmazza az összes lépést, a hibakezelést és az opcionális naplózást.

```java
package com.example;

import com.aspose.ocr.*;

public class HelloWorldOcr {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine
        OcrEngine engine = new OcrEngine();

        // -------------------------------------------------
        // 1️⃣ Enable GPU acceleration – how to enable GPU
        // -------------------------------------------------
        engine.setUseGpu(true);

        // -------------------------------------------------
        // 2️⃣ Set language – how to set language
        // -------------------------------------------------
        engine.setLanguage(OcrLanguage.ENGLISH); // Change if needed

        // -------------------------------------------------
        // 3️⃣ Add preprocessing filter – how to add filter
        // -------------------------------------------------
        engine.addPreprocessFilter(FilterType.DENOISE);
        // Optional: engine.addPreprocessFilter(FilterType.CONTRAST);

        // -------------------------------------------------
        // 4️⃣ Load the JPEG image – extract text JPG
        // -------------------------------------------------
        String imagePath = "YOUR_DIRECTORY/sample.jpg";
        engine.setImage(ImageStream.fromFile(imagePath));

        // -------------------------------------------------
        // 5️⃣ Perform OCR – recognize image text
        // -------------------------------------------------
        engine.recognize();

        // Retrieve and display the recognized text
        String text = engine.getText();
        System.out.println("Recognized text: " + text);

        // -------------------------------------------------
        // 6️⃣ Optional: write output to a file
        // -------------------------------------------------
        java.nio.file.Files.writeString(
                java.nio.file.Paths.get("output.txt"),
                text,
                java.nio.charset.StandardCharsets.UTF_8
        );

        // -------------------------------------------------
        // 7️⃣ Optional: enable debug logging to verify GPU usage
        // -------------------------------------------------
        engine.setLogLevel(com.aspose.ocr.logging.LogLevel.DEBUG);
        engine.setLogFile("ocr-debug.log");
    }
}
```

**A program futtatása**

```bash
mvn compile exec:java -Dexec.mainClass=com.example.HelloWorldOcr
```

A felismert szöveget a konzolra kell kiírni, és a `output.txt` fájlba menteni. Az `ocr-debug.log` fájl megerősíti a GPU használatát.

## Következtetés

Ebben az oktatóanyagban bemutattuk, hogyan **engedélyezzük a GPU-t** az Aspose.OCR számára Java-ban, hogyan **felismerjük a képszöveget**, **JPG szöveg kinyerés**, **hogyan adjunk hozzá szűrőt**, és **hogyan állítsuk be a nyelvet**—mindezt egyetlen, önálló programban. A GPU engedélyezésével jelentős sebességnövekedést érhetsz el, míg a szűrők és a nyelvi beállítások magas pontosságot biztosítanak különféle képforrások esetén.

**Következő lépések**

* Kísérletezz további szűrőkkel, például `FilterType.BINARIZE`-vel beolvasott dokumentumokhoz.  
* Válts más nyelvekre (`OcrLanguage.SPANISH`, `OcrLanguage.CHINESE_SIMPLIFIED`), hogy bővítsd a többnyelvű támogatást.  
* Kombináld ezt az OCR csővezetéket az Apache PDFBox-szal, hogy közvetlenül a PDF oldalakból nyerj szöveget.

Nyugodtan adaptáld a kódot kötegelt feldolgozáshoz, integráld egy Spring Boot szolgáltatásba, vagy csatlakoztasd egy üzenetsorhoz valós idejű OCR feladatokhoz. Boldog kódolást!

## Mit érdemes következőként megtanulni?

A következő oktatóanyagok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás tartalmaz teljesen működő kódrészleteket lépésről‑lépésre magyarázatokkal, hogy segítsenek elsajátítani további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [Hogyan olvassunk szöveget egy képről Java-ban az Aspose OCR használatával – Teljes útmutató](/ocr/english/java/ocr-basics/read-text-from-image-in-java-complete-aspose-ocr-guide/)
- [Hogyan OCR-eljünk képszöveget nyelvvel az Aspose.OCR használatával](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Kép előfeldolgozás OCR Java-ban az Aspose OCR-rel – Pontosság növelése és szöveg kinyerése](/ocr/english/java/advanced-ocr-techniques/preprocess-image-ocr-in-java-boost-accuracy-extract-text/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}