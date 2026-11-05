---
category: general
date: 2026-06-16
description: Futtass OCR-t a dokumentumon Java-val néhány lépésben. Tanuld meg, hogyan
  konfiguráld az OCR-t, hogyan ismerj fel szöveget TIFF-ből, és hogyan nyerj ki szöveget
  többoldalas képekből.
draft: false
keywords:
- run OCR on document
- how to configure OCR
- recognize text from TIFF
- extract text from multi-page
language: hu
og_description: Futtass OCR-t dokumentumon Java-val. Ez az útmutató bemutatja, hogyan
  konfiguráljuk az OCR-t, hogyan ismerjük fel a szöveget TIFF‑fájlokból, és hogyan
  nyerjünk ki szöveget többoldalas képekből.
og_title: OCR futtatása dokumentumon Java-ban – Lépésről lépésre útmutató
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Run OCR on document using Java in just a few steps. Learn how to configure
    OCR, recognize text from TIFF, and extract text from multi‑page images.
  headline: Run OCR on Document in Java – Complete Guide
  type: TechArticle
- description: Run OCR on document using Java in just a few steps. Learn how to configure
    OCR, recognize text from TIFF, and extract text from multi‑page images.
  name: Run OCR on Document in Java – Complete Guide
  steps:
  - name: '**Streamed processing** – Some OCR SDKs let you feed pages one‑by‑one instead
      of loading the entire TIFF into memory. Look for methods like `engine.setImageStream(...)`
      that accept an `InputStream`.'
    text: '**Streamed processing** – Some OCR SDKs let you feed pages one‑by‑one instead
      of loading the entire TIFF into memory. Look for methods like `engine.setImageStream(...)`
      that accept an `InputStream`.'
  - name: '**Memory limits** – If you hit `OutOfMemoryError`, lower the thread count
      or increase the JVM heap (`-Xmx2g`).'
    text: '**Memory limits** – If you hit `OutOfMemoryError`, lower the thread count
      or increase the JVM heap (`-Xmx2g`).'
  - name: '**Post‑processing** – Use regex or natural‑language libraries to clean
      up line breaks, remove headers/footers, or extract specific fields (e.g., invoice
      numbers).'
    text: '**Post‑processing** – Use regex or natural‑language libraries to clean
      up line breaks, remove headers/footers, or extract specific fields (e.g., invoice
      numbers).'
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: OCR futtatása dokumentumon Java-ban – Teljes útmutató
url: /hu/java/ocr-operations/run-ocr-on-document-in-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR futtatása dokumentumon Java‑ban – Teljes útmutató

Valaha szükséged volt **OCR futtatására dokumentum** fájlokon, de nem tudtad, hol kezdjed? Nem vagy egyedül. Akár régi archívumokat digitalizálsz, akár beolvasott űrlapokból nyersz adatot, a képekből megbízható szöveg kinyerése gyakori nehézség.

Ebben az útmutatóban egy gyakorlati, vég‑ponttól‑végig példán keresztül mutatjuk be, hogyan **konfiguráljuk az OCR‑t**, **szöveget ismerünk fel TIFF‑ből**, és **szöveget nyerünk ki többoldalas** dokumentumokból – mindezt csak néhány Java sorral. Felesleges részlet nélkül, csak egy működő megoldás, amit ma beilleszthetsz a projektedbe.

## Mit fogsz megtanulni

- OCR motor példány beállítása Java‑ban  
- Többoldalas TIFF kép betöltése feldolgozáshoz  
- A motor optimalizálása szálak számának beállításával (az „hogyan konfiguráljuk az OCR‑t” rész)  
- Felismerés végrehajtása és a kinyert szöveg kiírása  
- Széljegyek kezelése, mint nagy fájlok és memóriahatárok  

A útmutató végére magabiztosan **futtathatsz OCR‑t dokumentum** képeken, és szilárd alapot kapsz a megoldás PDF‑ekre, PNG‑kre vagy akár élő kameraáramokra való kiterjesztéséhez.

## Előfeltételek

- Java 17 vagy újabb (a kód a `var` kulcsszót használja a rövidség kedvéért)  
- OCR könyvtár, amely elérhetővé teszi az `OcrEngine` osztályt (pl. *Aspose.OCR for Java* vagy *Tesseract‑Java* wrapper).  
- Egy `multi_page.tif` nevű többoldalas TIFF fájl, amely egy ismert könyvtárban van elhelyezve.  

Ha hiányzik az OCR könyvtár, add hozzá a `pom.xml`‑hez (Maven) vagy a `build.gradle`‑hez (Gradle) – a pontos koordináták a szállítótól függenek, de a legtöbb egyetlen JAR‑t biztosít, amelyre hivatkozhatsz.

---

## 1. lépés: Az OCR motor inicializálása – Hogyan futtassunk OCR‑t dokumentumon

Először is: szükséged van egy motor objektumra, amely a nehéz munkát elvégzi. Gondolj rá úgy, mint a művelet agyára.

```java
import com.example.ocr.OcrEngine;   // Replace with your actual package
import com.example.ocr.ImageStream;
import com.example.ocr.OcrResult;

public class OcrDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine instance
        OcrEngine engine = new OcrEngine();
```

> **Miért fontos:** Az `OcrEngine` magába foglalja az összes felismerési beállítást, nyelvi csomagot és hardverhasználati opciót. Egyszer létrehozni és többször felhasználni több képhez hatékonyabb, mint minden alkalommal újra példányosítani.

---

## 2. lépés: Többoldalas TIFF betöltése – Szöveg kinyerése többoldalas képekből

Most a motorra irányítjuk azt a fájlt, amelyet feldolgozni szeretnénk. A TIFF gyakori formátum a beolvasott dokumentumoknál, mivel egyetlen fájlban több oldalt is tárolhat.

```java
        // Step 2: Load the multi‑page image to be processed
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/multi_page.tif"));
```

> **Pro tipp:** Ha a TIFF egy hálózati megosztáson van, használj `ImageStream.fromUrl(...)`‑t helyette. Ez elkerüli a teljes fájl memóriába másolását az OCR megkezdése előtt.

---

## 3. lépés: Hogyan konfiguráljuk az OCR‑t a maximális áteresztőképességért

A kész OCR könyvtárak gyakran egyetlen szálon futnak, ami szűk keresztmetszet lehet a modern többmagos gépeken. Itt válaszolunk a „**hogyan konfiguráljuk az OCR‑t**” részre.

```java
        // Step 3: Configure the engine to use all available CPU cores
        int availableCores = Runtime.getRuntime().availableProcessors();
        engine.getRecognitionSettings().setThreadCount(availableCores);
```

> **Miért működik:** Ha a szálak számát a logikai processzorok számához igazítod, az OCR motor párhuzamosan tudja feldolgozni a különböző oldalakat. Egy 4‑magos laptop esetén körülbelül 3‑4‑szörös sebességnövekedést láthatsz többoldalas dokumentumok esetén.  
> **Széljegy:** Egyes környezetek (pl. korlátozott CPU kvótával rendelkező Docker konténerek) több magot jeleznek, mint amennyit ténylegesen használhatnak. Ilyenkor manuálisan korlátozd a szálak számát: `engine.getRecognitionSettings().setThreadCount(Math.min(availableCores, 2));`

---

## 4. lépés: Szöveg felismerése TIFF‑ből – A fő OCR hívás

Miután minden össze van kötve, itt az ideje ténylegesen futtatni a felismerést. Ez az egyetlen hívás végigiterál a TIFF minden oldalán, alkalmazza a nyelvi modelleket, és egy összetett eredményt ad vissza.

```java
        // Step 4: Perform the OCR recognition
        OcrResult result = engine.recognize();
```

> **Mi történik a háttérben?** A motor a TIFF‑et egyedi raszterképekre bontja, mindegyiket az OCR neurális hálózatba táplálja, majd a szöveges kimenetet összefűzi. Ha oldalankénti részletezésre van szükséged, a `result.getPages()` egy `OcrPageResult` objektumok listáját adja.

---

## 5. lépés: A felismert szöveg kiírása – Az extrakció ellenőrzése

Végül kiírjuk a kinyert szöveget a konzolra. Egy valós alkalmazásban valószínűleg adatbázisba vagy JSON fájlba írnád.

```java
        // Step 5: Output the recognized text
        System.out.println(result.getText());
    }
}
```

**Várható kimenet (csonkítva):**

```
Page 1:
Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00

Page 2:
Terms and Conditions...
```

Ha értelmetlen karaktereket látsz a tiszta szöveg helyett, ellenőrizd, hogy a megfelelő nyelvi csomagok telepítve vannak-e, és a kép nem túl zajos. Az előfeldolgozó lépések, mint a kiegyenesítés vagy binarizálás, jelentősen javíthatják a pontosságot.

---

## Nagy többoldalas fájlok kezelése – Tippek az extrakcióhoz

Még ha már bemutattuk is az alapfolyamatot, a valós dokumentumok hatalmasak lehetnek. Íme néhány további szempont:

1. **Folyamatos feldolgozás** – Egyes OCR SDK‑k lehetővé teszik, hogy oldalanként adjuk át a képeket a teljes TIFF memóriába töltése helyett. Keress olyan metódusokat, mint a `engine.setImageStream(...)`, amelyek `InputStream`‑et fogadnak.  
2. **Memória korlátok** – Ha `OutOfMemoryError`-t kapsz, csökkentsd a szálak számát vagy növeld a JVM heap‑et (`-Xmx2g`).  
3. **Utófeldolgozás** – Használj regex‑et vagy természetes nyelvfeldolgozó könyvtárakat a sortörések tisztításához, fejlécek/láblécek eltávolításához vagy specifikus mezők (pl. számlaszámok) kinyeréséhez.

---

## Teljes működő példa (minden lépés egyben)

Az alábbiakban a teljes, azonnal futtatható Java osztály látható. Másold be az IDE‑dbe, igazítsd a csomagot/importokat, és futtasd.

```java
package com.example.ocrdemo;

import com.example.ocr.OcrEngine;
import com.example.ocr.ImageStream;
import com.example.ocr.OcrResult;

/**
 * Demonstrates how to run OCR on document images, configure the engine,
 * recognize text from TIFF files, and extract text from multi‑page documents.
 */
public class OcrDemo {
    public static void main(String[] args) throws Exception {
        // Create the OCR engine instance
        OcrEngine engine = new OcrEngine();

        // Load the multi‑page TIFF image
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/multi_page.tif"));

        // Configure the engine to use all CPU cores (how to configure OCR)
        int cores = Runtime.getRuntime().availableProcessors();
        engine.getRecognitionSettings().setThreadCount(cores);

        // Perform recognition (recognize text from TIFF)
        OcrResult result = engine.recognize();

        // Output the extracted text (extract text from multi‑page)
        System.out.println(result.getText());
    }
}
```

> **Pro tipp:** Tedd a `recognize()` hívást egy `try‑catch` blokkba, hogy elegánsan kezeld az `OcrException`‑t, különösen sérült képfájlok esetén.

---

## Következtetés

Most megmutattuk, hogyan **futtassunk OCR‑t dokumentum** képeken Java‑val, lefedve mindent a motor inicializálásától a többoldalas szövegkivonásig. A **hogyan konfiguráljuk az OCR‑t** megértésével kihozhatod a modern CPU‑k teljes teljesítményét, míg a **szöveg felismerése TIFF‑ből** és a **szöveg kinyerése többoldalas** fájlokból lépései szilárd alapot adnak bármely dokumentum‑digitalizációs projekthez.

Mi a következő? Próbáld meg a TIFF‑et PDF‑re cserélni, kísérletezz egyedi nyelvi modellekkel, vagy irányítsd a kimenetet egy keresőindexbe. A lehetőségek határtalanok, ha már van ez az alapod.

Ha bármilyen akadályba ütközöl – például a választott OCR könyvtár más API‑t használ – írj egy megjegyzést alább. Boldog kódolást, és élvezd a beolvasott oldalak kereshető szöveggé alakítását!

## Mit érdemes még tanulni?

Az alábbi útmutatók szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás tartalmaz teljes működő kódrészleteket lépésről‑lépésre magyarázatokkal, hogy elsajátíthasd a további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [Képek szövegének kinyerése – OCR alapok Aspose.OCR for Java‑val](/ocr/english/java/ocr-basics/)
- [Hogyan ismerjünk fel TIFF‑et Aspose.OCR for Java‑val](/ocr/english/java/ocr-operations/recognize-tiff/)
- [Hogyan OCR‑eljünk képszöveget nyelvvel Aspose.OCR használatával](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}