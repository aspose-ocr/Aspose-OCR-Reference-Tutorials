---
category: general
date: 2026-02-19
description: Készítsen kereshető PDF-et JPG képből az Aspose OCR segítségével Java-ban.
  Konvertálja a JPG-t PDF-re, és gyorsan ismerje fel a képen lévő szöveget.
draft: false
keywords:
- create searchable pdf
- image to searchable pdf
- recognize text from image
- extract text from jpg
- convert jpg to pdf
language: hu
og_description: Készítsen kereshető PDF-et egy JPG képből az Aspose OCR segítségével.
  Ismerje meg, hogyan konvertálhat JPG-t PDF-be, és hogyan ismerheti fel a szöveget
  a képen Java‑ban.
og_title: Kereshető PDF létrehozása JPG-ből – Java OCR útmutató
tags:
- aspose-ocr
- java
- pdf
- ocr
title: Kereshető PDF létrehozása JPG-ből – Kép konvertálása kereshető PDF-re Java
  útmutató
url: /hu/java/ocr-operations/create-searchable-pdf-from-jpg-image-to-searchable-pdf-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kereshető PDF létrehozása JPG-ből – Kép → Kereshető PDF Java útmutató

Valaha szükséged volt **kereshető PDF** létrehozására egy beolvasott képből, de nem tudtad, hol kezdjed? Nem vagy egyedül – sok fejlesztő ütközik ugyanabba a problémába, amikor egy JPG‑nek kereshetőnek kell lennie. A jó hír, hogy az Aspose OCR for Java segítségével néhány kódsorral teljesen kereshető PDF‑et készíthetsz a képből.

Ebben az útmutatóban végigvezetünk a teljes folyamaton: JPG betöltése, a szöveg felismerése, és az eredmény mentése kereshető PDF‑ként. A végére tudni fogod, hogyan **convert jpg to pdf**, hogyan **extract text from jpg**, és miért gyakran megbízhatóbb ez a megközelítés, mint a PDF‑re utólag OCR‑t alkalmazni.

## Amire szükséged lesz

* **Java Development Kit (JDK) 8 vagy újabb** – a kód a szabványos Java API‑kat használja.
* **Aspose OCR for Java** könyvtár – beszerezheted a Maven Central‑ból vagy letöltheted a JAR‑t az Aspose weboldaláról.
* Egy **minta JPG**, amely olvasható szöveget tartalmaz (pl. beolvasott számla vagy egy dokumentum képernyőképe).

Nem szükséges további keretrendszer; a példa egy egyszerű Java projekttel működik.

## 1. lépés – A projekt beállítása és az Aspose OCR hozzáadása

Először hozz létre egy új Maven projektet (vagy egyszerűen egy mappát a JAR‑ral a classpath‑on). Ha Maven‑t használsz, add hozzá ezt a függőséget a `pom.xml`‑hez:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- check for the latest version -->
</dependency>
```

> **Pro tip:** Mindig ellenőrizd a legújabb verziót az Aspose Maven tárolóban; az újabb kiadások tartalmaznak teljesítményjavításokat és hibajavításokat.

Miután a függőség feloldódott, készen állsz a Java kód megírására, amely **create searchable PDF**.

## 2. lépés – Kép betöltése (image to searchable pdf)

Az első tényleges lépés, hogy az OCR motorra mutassuk a forrásképet. Itt kezdődik igazán a **image to searchable pdf** átalakítás.

```java
import com.aspose.ocr.*;

public class SearchablePdfExample {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Load the JPG you want to turn into a searchable PDF
        // Replace "YOUR_DIRECTORY/input.jpg" with the actual path to your file
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/input.jpg"));
```

> **Miért fontos:** A `setImage` megmondja az Aspose‑nak, melyik bitmapet elemezze. Ha alacsony felbontású képet adsz meg, az OCR minősége romlik, ezért győződj meg róla, hogy a JPG legalább 300 dpi legyen a legjobb eredményhez.

## 3. lépés – Szöveg felismerése a képről

Miután a motor tudja, melyik képpel dolgozik, kérhetjük, hogy **recognize text from image**. Az Aspose OCR a háttérben elvégzi a nehéz munkát, kezelve a nyelvfelismerést, a karakterszegmentálást és a megbízhatósági pontszámot.

```java
        // Perform OCR and directly output a searchable PDF
        ocrEngine.recognize()
                 .save("YOUR_DIRECTORY/output-searchable.pdf", OcrOutputFormat.SEARCHABLE_PDF);
```

A `recognize()` hívás egy fluent interfészt ad vissza, amely lehetővé teszi a `save` metódus láncolását. Az `OcrOutputFormat.SEARCHABLE_PDF` megadásával a könyvtár egy láthatatlan szövegréteget ágyaz be a PDF‑be, miközben megőrzi az eredeti kép megjelenését.

> **Különleges eset:** Ha a JPG több oldalt tartalmaz (pl. többoldalas TIFF, amely külön JPG‑ként van mentve), akkor minden fájlon végig kell iterálni, és a későbbiekben össze kell fűzni a keletkezett PDF‑eket. Ugyanaz az OCR motor újra felhasználható minden iterációhoz.

## 4. lépés – Az eredmény ellenőrzése

A mentési művelet befejezése után egy egyszerű konzolüzenet jelzi, hogy minden rendben ment.

```java
        // Let the user know the PDF is ready
        System.out.println("Searchable PDF created.");
    }
}
```

Amikor megnyitod az `output-searchable.pdf`-et egy nézegetőben, például az Adobe Acrobatban, képesnek kell lenned a rejtett szöveg kijelölésére, másolására vagy keresésre – pontosan ez, amit egy **searchable PDF**‑től vársz.

### Várható kimenet

A program futtatása a következőt írja ki:

```
Searchable PDF created.
```

A generált PDF megjeleníti az eredeti JPG‑t, miközben lehetővé teszi a szöveg kijelölését. Ha megnyitod a PDF „Properties → Description → PDF Producer” részét, olyasmit látsz, mint `Aspose.OCR for Java`.

## Teljes működő példa

Az alábbiakban a teljes, azonnal futtatható forrásfájl található. Másold be a kedvenc IDE‑dbe, állítsd be a fájlutakat, és indítsd el.

```java
import com.aspose.ocr.*;

public class SearchablePdfExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the source image containing the text to be recognized
        // Make sure the path points to a real JPG on your disk
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/input.jpg"));

        // Step 3: Recognize the text and directly save it as a searchable PDF
        ocrEngine.recognize()
                 .save("YOUR_DIRECTORY/output-searchable.pdf", OcrOutputFormat.SEARCHABLE_PDF);

        // Step 4: Notify that the PDF has been created
        System.out.println("Searchable PDF created.");
    }
}
```

> **Mi van, ha az OCR nem sikerül?**  
> * Általában ez akkor fordul elő, ha a kép túl zajos vagy a nyelv nincs alapból támogatva. A pontosságot javíthatod a kép előfeldolgozásával (kontraszt növelése, kiegyenesítés) vagy a nyelv kifejezett beállításával a `ocrEngine.getLanguage().setLanguage(OcrLanguage.English);` segítségével.

## Gyakori kérdések és buktatók

| Question | Answer |
|----------|--------|
| **Kivonhatom a sima szöveget PDF helyett?** | Igen. Használd a `ocrEngine.recognize().save("output.txt", OcrOutputFormat.TEXT);` parancsot. |
| **Mi van, ha PNG‑t kell feldolgozni?** | Ugyanaz az API működik; csak cseréld ki a fájlkiterjesztést a `fromFile`‑ben. |
| **A létrehozott PDF valóban kereshető minden nézegetőben?** | A modern nézegetők (Adobe Reader, Foxit, Chrome) tiszteletben tartják a rejtett szövegréteget. A régebbi eszközök esetleg figyelmen kívül hagyják. |
| **Hogyan szabályozhatom a PDF oldal méretét?** | Az Aspose OCR alapértelmezés szerint a kép méreteit használja. Egyedi méretezéshez manuálisan generálj PDF‑et, és helyezd rá az OCR szövegréteget – ez egy haladó szintű forgatókönyv. |

## Teljesítmény tippek

* **Kötegelt feldolgozás:** Használd újra egyetlen `OcrEngine` példányt több képhez, hogy elkerüld a natív könyvtár többszöri betöltését.
* **Szálbiztonság:** A motor **nem** szálbiztos; ha párhuzamosítasz, hozz létre egy példányt szálanként.
* **Memóriahasználat:** Nagy képek sok RAM-ot fogyaszthatnak. Ha `OutOfMemoryError`-t kapsz, méretezd le a képet, mielőtt a motorba adod.

## Következő lépések

Most, hogy tudod, hogyan **create searchable PDF**, érdemes lehet kapcsolódó feladatokat is felfedezni:

* **Convert jpg to pdf** OCR nélkül (használd az Aspose PDF könyvtárat egy egyszerű kép‑PDF‑hez).
* **Extract text from jpg** egy `.txt` fájlba az indexeléshez.
* **Combine multiple searchable PDFs** egyetlen dokumentummá az Aspose PDF `PdfFileEditor`‑jével.  

Ezek mind ugyanazon az alapon nyugszanak, amelyet most felállítottál.

---

### Gyors összefoglaló

* Létrehoztunk egy **searchable PDF**‑et egy JPG‑ből az Aspose OCR for Java segítségével.
* A folyamat magában foglalta a kép betöltését, a szöveg felismerését és a kereshető PDF‑ként való mentést.
* Most már van egy újrahasználható minta a **image to searchable PDF**, **recognize text from image**, **extract text from jpg**, és **convert jpg to pdf** feladatokra.

Próbáld ki a saját dokumentumaiddal, ha szükséges, finomítsd a nyelvi beállításokat, és hagyd, hogy az OCR elvégezze a nehéz munkát. Jó kódolást!  

![Create searchable PDF example](placeholder.png){alt="Kereshető PDF példa"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}