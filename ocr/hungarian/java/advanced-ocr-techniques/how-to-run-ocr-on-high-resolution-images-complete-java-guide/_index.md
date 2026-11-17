---
category: general
date: 2026-03-07
description: Tanulja meg, hogyan hajthat végre gyors OCR-t egy TIFF fájlon, töltsön
  be nagy felbontású képet, engedélyezze a párhuzamos OCR-feldolgozást, és nyerje
  ki az OCR-szöveget Java-ban.
draft: false
keywords:
- how to run OCR
- load high resolution image
- parallel OCR processing
- how to extract OCR text
- recognize text from tiff
language: hu
og_description: Lépésről‑lépésre útmutató arról, hogyan futtassunk OCR‑t, töltsünk
  be nagy felbontású képet, engedélyezzük a párhuzamos OCR‑feldolgozást, és nyerjünk
  ki OCR‑szöveget TIFF‑fájlokból.
og_title: Hogyan futtassunk OCR-t nagy felbontású képeken – Java útmutató
tags:
- OCR
- Java
- Image Processing
title: Hogyan futtass OCR-t nagy felbontású képeken – Teljes Java útmutató
url: /hu/java/advanced-ocr-techniques/how-to-run-ocr-on-high-resolution-images-complete-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan futtassunk OCR-t nagy felbontású képeken – Teljes Java útmutató

Gondolkodtál már azon, **hogyan futtassunk OCR-t** egy hatalmas beolvasott dokumentumon anélkül, hogy az alkalmazásod leállna? Nem vagy egyedül. Sok valós projektben a bemenet egy több megabájtos TIFF, amelyet gyorsan kell feldolgozni, és az egy szálas megközelítés egyszerűen nem elegendő.  

Ebben a tutorialban végigvezetünk a nagy felbontású kép betöltésén, a párhuzamos OCR feldolgozás bekapcsolásán, és végül az OCR szöveg kinyerésén – mind tiszta, termelésre kész Java kóddal. A végére pontosan tudni fogod, **hogyan nyerjünk ki OCR szöveget** egy TIFF‑ből, és miért fontos minden beállítás.

## Amit megtanulsz

- A pontos lépéseket **magas felbontású kép** fájlok betöltéséhez OCR‑hez.
- Hogyan konfiguráld az OCR motorját **párhuzamos OCR feldolgozásra** az összes elérhető CPU magon.
- A legjobb módját **szöveg felismerésének TIFF** fájlokból és a nyers szöveg eredmény lekérésének.
- Tippek, buktatók és szélsőséges esetek kezelése, hogy a megoldásod robusztus maradjon a gyártásban.

**Előfeltételek:** Java 11+ (vagy bármely friss JDK), egy OCR könyvtár, amely biztosítja az `OcrEngine`‑t (pl. Tesseract‑Java vagy egy kereskedelmi SDK), és egy TIFF fájl, amelyet be szeretnél olvasni. Egyéb külső eszközre nincs szükség.

![hogyan futtassunk OCR-t nagy felbontású TIFF képen](ocr-highres.png)

*Image alt text: hogyan futtassunk OCR-t nagy felbontású TIFF képen*

---

## 1. lépés: A projekt beállítása és a függőségek importálása

Mielőtt a kódba merülnénk, győződj meg róla, hogy az OCR könyvtár a classpath‑on van. Maven‑t használva adj hozzá valami ilyesmit:

```xml
<dependency>
    <groupId>com.example</groupId>
    <artifactId>ocr-sdk</artifactId>
    <version>2.4.1</version>
</dependency>
```

> **Pro tipp:** Használd a SDK legújabb stabil verzióját; az új kiadások gyakran javítják a több szálas teljesítményt és jobb TIFF támogatást nyújtanak.

Most hozz létre egy egyszerű Java osztályt, amely a demónkat tartalmazza:

```java
package com.example.ocrdemo;

import com.example.ocr.OcrEngine;
import com.example.ocr.OcrResult;
import com.example.io.ImageInputStream;
import java.io.IOException;
```

Ez minden import, amire a fő folyamatban szükséged van.

## 2. lépés: Magas felbontású kép betöltése OCR‑hez

Egy **magas felbontású kép** helyes betöltése minden OCR csővezeték alapja. Ha alacsony minőségű bélyegképet adsz a motorba, az soha nem fogja látni a karakterekhez szükséges részleteket.

```java
// Step 2: Load a high‑resolution TIFF image
String imagePath = "YOUR_DIRECTORY/high_res_scan.tif";
ImageInputStream imageStream = new ImageInputStream(imagePath);
```

> **Miért fontos:** Az `ImageInputStream` bájtonként olvassa a fájlt, megőrizve az eredeti DPI‑t. Néhány könyvtár automatikusan lecsökkenti a méretet; a nyers stream használatával minden pontot megtartunk, ami drámaian javítja a pontosságot, amikor később **szöveget ismerünk fel TIFF‑ből**.

## 3. lépés: Párhuzamos OCR feldolgozás engedélyezése

Az egy szálas OCR szűk keresztmetszet lehet, különösen egy többmagos szerveren. A használt SDK egyetlen flag‑gel engedélyezi a több szálas működést:

```java
// Step 3: Enable parallel OCR processing
OcrEngine ocrEngine = new OcrEngine();
ocrEngine.getConfig().setUseMultiThreading(true);
ocrEngine.getConfig().setThreadCount(Runtime.getRuntime().availableProcessors());
```

> **Mi történik a háttérben?** A motor a képet csempékre osztja, minden csempét egy munkás szálnak ad, majd összevonja az eredményeket. A `availableProcessors()`‑hez igazított szál számával a JVM dönt a hardvered optimális kihasználásáról.

### Szélsőséges eset: Túl sok szál

Ha a kódot egy olyan konténerben futtatod, amely korlátozza a CPU‑t, a `availableProcessors()` magasabb számot adhat, mint amennyi ténylegesen rendelkezésre áll. Ilyenkor állíts be alacsonyabb szál számot manuálisan:

```java
ocrEngine.getConfig().setThreadCount(4); // safe default for 4‑core containers
```

## 4. lépés: OCR felismerés futtatása

Miután a motor konfigurálva van és a kép készen áll, a tényleges felismerés egyetlen sorban elvégezhető:

```java
// Step 4: Perform OCR on the high‑resolution image
OcrResult ocrResult = ocrEngine.recognize(imageStream);
```

A `recognize` metódus egy `OcrResult` objektumot ad vissza, amely tartalmazza a nyers szöveget és opcionális metaadatokat (bizalmi pontszámok, keretek stb.).

## 5. lépés: OCR szöveg kinyerése és az eredmény ellenőrzése

Végül **hogyan nyerjünk ki OCR szöveget** a `OcrResult`‑ból. Az SDK egy egyszerű getter‑t biztosít:

```java
// Step 5: Extract and display the recognized text
String extractedText = ocrResult.getText();
System.out.println("=== OCR Output ===");
System.out.println(extractedText);
```

### Várható kimenet

Ha a TIFF egy „Hello, World!” feliratot tartalmazó beolvasott oldalt tartalmaz, a következőt kell látnod:

```
=== OCR Output ===
Hello, World!
```

Ha a kimenet összezavarodott, ellenőrizd, hogy valóban **magas felbontású képet töltöttél‑e be**, és hogy az OCR nyelvi csomagok egyeznek‑e a dokumentum nyelvével.

## Teljes, működő példa

Mindent összevonva, itt egy önálló program, amelyet egyszerűen másolj‑be az IDE‑dbe és azonnal futtathatsz:

```java
package com.example.ocrdemo;

import com.example.ocr.OcrEngine;
import com.example.ocr.OcrResult;
import com.example.io.ImageInputStream;
import java.io.IOException;

/**
 * Demonstrates how to run OCR on a high‑resolution TIFF using parallel processing.
 */
public class ParallelOcrDemo {

    public static void main(String[] args) {
        try {
            // 1️⃣ Create the OCR engine
            OcrEngine ocrEngine = new OcrEngine();

            // 2️⃣ Enable multi‑core processing
            ocrEngine.getConfig().setUseMultiThreading(true);
            ocrEngine.getConfig().setThreadCount(Runtime.getRuntime().availableProcessors());

            // 3️⃣ Load the high‑resolution image
            String imagePath = "YOUR_DIRECTORY/high_res_scan.tif";
            ImageInputStream imageStream = new ImageInputStream(imagePath);

            // 4️⃣ Run OCR
            OcrResult result = ocrEngine.recognize(imageStream);

            // 5️⃣ Extract and print the text
            String text = result.getText();
            System.out.println("=== OCR Output ===");
            System.out.println(text);
        } catch (IOException e) {
            System.err.println("Failed to read the image file: " + e.getMessage());
        } catch (Exception e) {
            System.err.println("OCR processing error: " + e.getMessage());
        }
    }
}
```

Futtasd a programot, és a kinyert karakterek a konzolra kerülnek. Így **hogyan futtassunk OCR‑t** vég‑től‑végig, a magas felbontású kép betöltésétől a tiszta szöveg lekéréséig.

---

## Gyakori kérdések és csapdák

| Kérdés | Válasz |
|----------|--------|
| **Mi van, ha a TIFF több oldalas?** | Az `ImageInputStream` képes az oldalakon iterálni; egyszerűen ciklusba foglalod `for (int i = 0; i < imageStream.getPageCount(); i++)` és minden oldalra meghívod a `recognize`‑t. |
| **Korlátozhatom a memóriahasználatot?** | Igen – állítsd be `ocrEngine.getConfig().setMaxMemoryMb(512)`‑t (vagy egy másik megfelelő limitet). A motor szükség esetén a csempéket lemezre írja. |
| **Működik a párhuzamos feldolgozás Windows‑on?** | Teljesen. Az SDK absztrahálja a szálkezelőt, így ugyanaz a kód Linuxon, macOS‑on vagy Windows‑on módosítás nélkül fut. |
| **Hogyan változtassam meg az OCR nyelvet?** | Hívd meg `ocrEngine.getConfig().setLanguage("eng+spa")` a `recognize` előtt. Ez akkor hasznos, ha **szöveget ismerünk fel TIFF‑ből** olyan fájlok esetén, amelyek több nyelvet tartalmaznak. |
| **Az eredményben felesleges sortörések vannak – mi a helyzet?** | Az OCR motor a képen látható szöveget adja vissza pontosan. Utófeldolgozhatod `String.replaceAll("\\r?\\n+", "\n")`‑val, vagy használhatsz elrendezés‑érzékeny elemzőt, ha oszlopmegőrzésre van szükség. |

---

## Összegzés

Áttekintettük, **hogyan futtassunk OCR‑t** egy nagy felbontású TIFF‑en, a **magas felbontású kép** betöltésétől a **párhuzamos OCR feldolgozás** engedélyezéséig, majd végül **hogyan nyerjünk ki OCR szöveget** a további felhasználáshoz. A fenti lépések követésével gyorsabb, megbízhatóbb eredményeket kapsz, miközben a kódbázisod rendezett és karbantartható marad.

Készen állsz a következő kihívásra? Próbáld ki:

- **Kötegelt feldolgozást** tucatnyi TIFF‑en egy futtatás során (ciklus egy könyvtáron, ugyanaz az `OcrEngine` példány újrahasználva).
- **Streaming OCR‑t**, ahol a képadatot hálózati forrásból kapod, anélkül, hogy leírnád a lemezre.
- **Finomhangolást** a motor bizalmi küszöbein, hogy kiszűrd az alacsony minőségű felismeréseket.

Ha kérdésed van a **szöveg felismeréséről TIFF** fájlokból, vagy szeretnél megosztani saját teljesítménytrükköket, írj egy megjegyzést alább. Boldog kódolást, és legyen az OCR‑d mindig pontos!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}