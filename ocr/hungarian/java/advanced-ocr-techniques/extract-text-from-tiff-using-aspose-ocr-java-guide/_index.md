---
category: general
date: 2026-07-05
description: Szöveg kinyerése TIFF fájlból az Aspose OCR Java segítségével párhuzamos
  OCR feldolgozási környezetben. Ez a tömör Aspose OCR Java példa bemutatja, hogyan
  lehet a teljesítményt többmagos szálazással növelni.
draft: false
keywords:
- extract text from tiff
- aspose ocr java example
- parallel ocr processing
- java ocr multithreading
- tiff image recognition
language: hu
og_description: Tiff fájlok szövegének kinyerése Aspose OCR Java-val és párhuzamos
  OCR feldolgozással. Kövesd ezt a lépésről‑lépésre Java példát a többoldalas képfelismerés
  felgyorsításához.
og_title: Szöveg kinyerése TIFF-ből az Aspose OCR Java segítségével – Útmutató
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Extract text from tiff using Aspose OCR Java in a parallel OCR processing
    setup. This concise Aspose OCR Java example shows how to boost performance with
    multi‑core threading.
  headline: Extract text from tiff using Aspose OCR Java – Guide
  type: TechArticle
tags:
- Java
- OCR
- Aspose
- TIFF
title: Szöveg kinyerése TIFF-fájlból az Aspose OCR Java segítségével – Útmutató
url: /hu/java/advanced-ocr-techniques/extract-text-from-tiff-using-aspose-ocr-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Szöveg kinyerése tiff fájlokból Aspose OCR Java – Útmutató

Valaha szükséged volt **szöveg kinyerésére tiff** fájlokból, de a folyamatot úgy lassúnak találtad, mint egy csiga? Nem vagy egyedül. Ha egy többoldalas TIFF-et egy egy‑szálas OCR motorra dobsz, a várakozási idő végtelennek tűnhet – különösen kötegelt feldolgozási helyzetben.

A lényeg: az Aspose OCR for Java képes kihasználni a géped minden logikai magját, így a lassú egy‑szálas folyamatot egy sima, párhuzamos OCR feldolgozási csővezetékké alakítja. Ebben az útmutatóban végigvezetünk egy teljes **Aspose OCR Java példán** keresztül, amely pontosan megmutatja, hogyan konfiguráld a motort, hogyan add át neki egy többoldalas TIFF-et, és hogyan **nyerj ki szöveget tiff** fájlokból az eredeti idő töredékével.

## Mit fogsz elsajátítani

- Egy futtatható Java osztály, amely bemutatja az **párhuzamos OCR feldolgozást** az Aspose OCR-rel.
- Világos magyarázatok arra, hogy miért fontos minden beállítás, nem csak arra, hogy mit kell beírni.
- Tippek a szélhelyzetek kezeléséhez, például változó oldalszám, nagy képfájlok és memória korlátok.
- Egy szilárd alap a kód saját dokumentum‑automatizálási projektjeidhez való adaptálásához.

> **Prerequisites**  
> • Java 8 vagy újabb telepítve (a kód JDK 11‑gyel is lefordítható).  
> • Maven vagy Gradle a Aspose OCR for Java könyvtár letöltéséhez.  
> • Egy többoldalas TIFF kép (bármely képszerkesztővel létrehozhatsz, vagy használhatod az Aspose‑nal szállított `multi_page.tif` mintát).  

Ha ezek az alapok rendben vannak, merüljünk el.

![Szöveg kinyerése tiff fájlokból Aspose OCR Java – párhuzamos feldolgozási diagram](image.png "Diagram, amely bemutatja, hogyan nyer ki szöveget a párhuzamos OCR feldolgozás tiff fájlokból")

## 1. lépés: Projekt beállítása – a leggyorsabb Aspose OCR Java példa

Mielőtt a **párhuzamos OCR feldolgozás** lényegéhez érnénk, szükségünk van egy Java projektre, amely láthatja az Aspose OCR JAR fájlokat. A legegyszerűbb módja a Maven használata:

```xml
<!-- pom.xml snippet -->
<dependencies>
    <dependency>
        <groupId>com.aspose</groupId>
        <artifactId>aspose-ocr</artifactId>
        <version>23.12</version> <!-- check for the latest version -->
    </dependency>
</dependencies>
```

Ha a Gradle-t részesíted előnyben, az ekvivalens:

```groovy
implementation 'com.aspose:aspose-ocr:23.12'
```

> **Pro tipp:** A függőség Maven Central‑on keresztüli hozzáadása biztosítja, hogy mindig a legújabb, biztonsági javításokkal ellátott buildet húzd le. Nem szükséges kézzel letölteni a JAR‑okat.

Miután a build fájlod készen áll, futtasd a `mvn clean compile` (vagy `gradle build`) parancsot, hogy ellenőrizd, az Aspose osztályok a classpath‑on vannak. Ha nem látsz hibát, készen állsz a továbbiakra.

## 2. lépés: OCR motor létrehozása és többmagos végrehajtás engedélyezése

Most megírjuk a Java osztályt, amely ténylegesen végrehajtja az OCR‑t. A kulcsfontosságú sor, amely egy szabályos OCR motort **párhuzamos OCR feldolgozó** erőművé változtatja, a `setThreadCount`. Ez megmondja az Aspose OCR‑nek, hány logikai magot használhat.

```java
package com.example.ocr;

import com.aspose.ocr.OcrEngine;
import com.aspose.ocr.RecognitionResult;

/**
 * ParallelOcrDemo – a concise Aspose OCR Java example that extracts text from tiff
 * images using multiple threads.
 */
public class ParallelOcrDemo {

    public static void main(String[] args) throws Exception {
        // Step 2.1: Instantiate the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2.2: Tell the engine to use 4 logical cores (adjust to your CPU)
        // This is the heart of parallel OCR processing.
        ocrEngine.setThreadCount(4);

        // Step 2.3: Point the engine at a multi‑page TIFF file.
        // Replace the path with the location of your own TIFF.
        String tiffPath = "YOUR_DIRECTORY/multi_page.tif";

        // Step 2.4: Run the recognition. The method returns a RecognitionResult
        // which holds the extracted text and additional metadata.
        RecognitionResult result = ocrEngine.recognizeImage(tiffPath);

        // Step 2.5: Output the extracted text – this is where we finally
        // extract text from tiff and show it on the console.
        System.out.println("=== Extracted Text Start ===");
        System.out.println(result.getText());
        System.out.println("=== Extracted Text End ===");
    }
}
```

### Miért fontos a `setThreadCount`

Az Aspose OCR belsőleg minden egyes oldalát egy többoldalas TIFF‑nek külön feladatokra osztja. Alapértelmezés szerint egyetlen szálon fut, ami azt jelenti, hogy minden oldal a előző befejezésére vár. A `threadCount` beállítása a fizikai magok számára (vagy egy kicsit kevesebbre a UI válaszkészségének megőrzése érdekében) lehetővé teszi, hogy a motor egyszerre több oldalt dolgozzon fel. Teljesítménytesztek szerint egy 4‑magos gép **akár 70 %**-kal csökkentheti a teljes feldolgozási időt az alapértelmezett egy‑szálas módhoz képest.

> **Megjegyzés:** Ha a szálak számát a rendelkezésre álló magok számánál magasabbra állítod, az operációs rendszer időosztást kezd, ami valójában rontja a teljesítményt. Maradj a `Runtime.getRuntime().availableProcessors()` értéknél, mint biztonságos felső határ.

## 3. lépés: Nagy TIFF‑ek és memória korlátok kezelése

Amikor **szöveget nyersz ki tiff** fájlokból, amelyek tucatnyi nagy felbontású oldalt tartalmaznak, a memóriahasználat megugorhat. Az Aspose OCR néhány beállítást kínál a rendezett működéshez:

```java
// Optional: Reduce memory footprint by lowering image resolution before OCR
ocrEngine.getImagePreprocessingOptions().setResolution(150); // DPI

// Optional: Enable streaming mode for massive TIFFs (>500 MB)
ocrEngine.setEnableStreaming(true);
```

- **Felbontás csökkentése** egy kis pontosságot cserél egy nagy memória nyereségért. A legtöbb nyomtatott dokumentum még 150 DPI‑n is olvasható.
- **Streaming mód** egyesével dolgozza fel az oldalakat anélkül, hogy az egész TIFF-et RAM‑ba töltené. Ez elengedhetetlen a szerver‑oldali kötegelt feladatokhoz.

## 4. lépés: Kimenet ellenőrzése és gyakori hibák elhárítása

A demo futtatása után a kinyert szöveget a “=== Extracted Text Start ===” jelzők között kell látnod. Ha a kimenet üresnek vagy torzultnak tűnik, fontold meg a következő ellenőrzéseket:

| Tünet | Valószínű ok | Gyors megoldás |
|---------|--------------|-----------|
| Egyáltalán nincs szöveg | Helytelen fájlútvonal vagy nem támogatott TIFF tömörítés | Ellenőrizd a `tiffPath` értékét, és győződj meg róla, hogy a TIFF nem használ proprietárius tömörítést (pl. a CCITT Group 4 rendben van; a JPEG‑2000 további kodekeket igényelhet). |
| Hiányzó karakterek (pl. ékezetes betűk) | Az OCR nyelv nincs beállítva | Hívd meg a `ocrEngine.setLanguage(OcrEngine.Language.English);` metódust vagy tölts be egy egyedi nyelvi csomagot. |
| Memória‑hiány hibák | Nagyon nagy TIFF streaming nélkül | Engedélyezd a `setEnableStreaming(true)` beállítást és/vagy csökkentsd a felbontást. |
| Lassú teljesítmény a `setThreadCount` ellenére | CPU hyper‑threading letiltva vagy JVM korlátok | Győződj meg róla, hogy a JVM nincs korlátozva `-Xmx` flag‑ekkel; biztosíts elegendő heap memóriát (pl. `-Xmx2g`). |

## 5. lépés: Méretezés – több TIFF mappa párhuzamos feldolgozása

Az egyfájlos demo nagyszerű a tanuláshoz, de a termelés gyakran kötegelt feldolgozást igényel. Az alábbi könnyű kiterjesztés bejár egy könyvtárat, elindít egy szál‑medencét, és párhuzamosan futtatja az OCR motort minden egyes fájlon. Ez az **párhuzamos OCR feldolgozást** mutatja be az alkalmazásszinten.



## Mit érdemes következőként megtanulni?

A következő útmutatók szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljes, működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsenek elsajátítani további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [Képek szövegének kinyerése – OCR alapok Aspose.OCR for Java‑val](/ocr/english/java/ocr-basics/)
- [Képből szöveg kinyerése Java‑val az Aspose.OCR Detect Areas Mode‑val](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Hogyan nyerjünk ki szöveget képből URL‑ről az Aspose.OCR for Java‑val](/ocr/english/java/advanced-ocr-techniques/perform-ocr-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}