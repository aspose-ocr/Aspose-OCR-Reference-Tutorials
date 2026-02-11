---
category: general
date: 2026-01-02
description: Képek szöveggé konvertálása Java-val az Aspose OCR használatával. Tanulja
  meg a kötegelt OCR feldolgozást, olvassa be a képeket egy mappából, és szűrje a
  fájlokat kiterjesztés szerint.
draft: false
keywords:
- convert images to text
- batch ocr processing
- read images from folder
- extract text from png
- filter files by extension
language: hu
og_description: Konvertálja a képeket gyorsan szöveggé Java-val. Ez az útmutató a
  kötegelt OCR-feldolgozást, a képek mappából történő beolvasását és a fájlok kiterjesztés
  szerinti szűrését tárgyalja.
og_title: Képek szöveggé konvertálása Java-ban – Teljes kötegelt OCR útmutató
tags:
- OCR
- Java
- Aspose
title: Képek szöveggé konvertálása Java-ban – Kötetes OCR feldolgozási útmutató
url: /hu/java/ocr-operations/convert-images-to-text-in-java-batch-ocr-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Képek szöveggé konvertálása Java‑ban – Kötetes OCR feldolgozási útmutató

Szükséged volt már **képek szöveggé konvertálására**, de nem tudtad, hogyan kezeld egyszerre a tucatnyi fájlt? Nem vagy egyedül – a fejlesztők állandóan küzdenek azzal, hogy adatot nyerjenek ki PNG‑ekből, JPG‑ekből és egyéb beolvasott anyagokból. A jó hír? Az Aspose OCR‑rel percek alatt felállíthatsz egy kötetes OCR feldolgozási csővezetéket, beolvashatsz képeket mappaszerkezetből, és még a fájlkiterjesztés alapján is szűrhetsz, hogy csak a lényegesekkel dolgozz.

Ebben a tutorialban egy önálló Java‑programot építünk, amely bejár egy könyvtárat, kiválaszt minden `.png` és `.jpg` fájlt, aszinkron módon elküldi őket az Aspose OCR‑nek, és az eredeti sorrendben kiírja a kinyert szöveget. A végére egy újrahasználható kódrészletet kapsz, amelyet bármely projektbe beilleszthetsz, ha **képek szöveggé konvertálására** van szükség nagy mennyiségben.

---

![Képek szöveggé konvertálása példa](https://example.com/convert-images-to-text.png "Java konzol kimenetének képernyőképe, amely PNG‑fájlokból konvertált szöveget mutat")

## Mit fogunk építeni

- Egyetlen `AsposeOCR` motor, amely a szálak között megosztott (hatékony és szál‑biztonságos).  
- Egy `ParallelRecognizer`, amely párhuzamosan futtatja az OCR feladatokat, tökéletes **kötetes OCR feldolgozáshoz**.  
- Logika, amely **képeket olvas be mappából** a `java.nio.file.Files` segítségével.  
- Egyszerű szűrők, hogy **szöveget nyerjünk ki PNG** fájlokból, miközben a JPG‑eket is kezeljük.  
- A belső szálkészlet tiszta leállítása az erőforrás‑szivárgások elkerülése érdekében.

### Előfeltételek

- Java 17 (vagy bármely friss LTS verzió).  
- Maven vagy Gradle az Aspose OCR könyvtár letöltéséhez.  
- Egy mappa tele PNG/JPG képekkel, amelyeket feldolgozni szeretnél.  
- Alapvető ismeretek a Java stream‑ekről – semmi bonyolultra nincs szükség.

> **Pro tipp:** Ha még nincs licenced, az Aspose ingyenes ideiglenes kulcsot kínál teszteléshez.

---

## 1. lépés – Projekt beállítása és Aspose OCR hozzáadása

Először hozz létre egy új Maven projektet (vagy Gradle‑t, ahogy neked kényelmes). Add hozzá az Aspose OCR függőséget a `pom.xml`‑hez:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Check the latest version on Maven Central -->
</dependency>
```

> **Miért fontos:** A függőség deklarálása már a kezdetektől biztosítja, hogy a fordító lássa az `AsposeOCR`, `ParallelRecognizer` és a kapcsolódó osztályokat. Emellett garantálja, hogy minden gépen ugyanaz a verzió legyen használva, ami elengedhetetlen a reprodukálható **kötetes OCR feldolgozáshoz**.

A build befejezése után frissítsd az IDE‑det, és látnod kell az Aspose csomagokat az `External Libraries` alatt.

---

## 2. lépés – Képek szöveggé konvertálása – OCR motor inicializálása

Csak **egy** OCR motor példányra van szükség a teljes futtatáshoz. Ennek megosztása a szálak között memóriát takarít meg és felgyorsítja a folyamatot, mivel a motor csak egyszer tölti be a nyelvi csomagokat.

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.ParallelRecognizer;
import com.aspose.ocr.OcrResult;
import com.aspose.ocr.RecognitionLanguage;

// ...

// Step 2: Create a single OCR engine instance and a parallel recognizer that uses it
AsposeOCR ocrEngine = new AsposeOCR();               // Loads language data internally
ParallelRecognizer parallelRecognizer = new ParallelRecognizer(ocrEngine);
```

> **Magyarázat:** A `ParallelRecognizer` egy szál‑medencét csomagol a motor köré. Amikor sok fájlt küldesz be, mindegyik saját munkás‑szálat kap, ami valódi párhuzamosságot biztosít a többmagos CPU‑kon.

---

## 3. lépés – Képek beolvasása mappából – Könyvtárfa bejárása

Most már **képeket kell beolvasnunk mappából**, és összegyűjteni minden PNG vagy JPG fájlt. A `Files.walk` API ezt egyetlen sorba sűríti, de hozzáadunk egy szűrőt, hogy **szöveget nyerjünk ki csak PNG**‑ból, ha szükséges.

```java
import java.nio.file.*;
import java.util.*;
import java.util.stream.Collectors;

// ...

// Step 3: Find all PNG and JPG images in the target directory
Path imagesRoot = Paths.get("YOUR_DIRECTORY"); // <-- replace with your path
List<Path> imagePaths = Files.walk(imagesRoot)
        .filter(p -> {
            String name = p.toString().toLowerCase();
            return name.endsWith(".png") || name.endsWith(".jpg");
        })
        .collect(Collectors.toList());

if (imagePaths.isEmpty()) {
    System.out.println("No PNG or JPG files found in " + imagesRoot);
    return;
}
```

> **Miért szűrünk itt:** A `filter` használata lehetővé teszi, hogy **kiterjesztés szerint szűrjünk** már a kezdetekkor, ami jelentősen csökkenti a felesleges I/O‑t később. Emellett a kód olvasható marad – nincs szükség bonyolult regex‑ekre.

---

## 4. lépés – Kötetes OCR feldolgozás – Feladatok aszinkron benyújtása

Miután a fájlok listája készen áll, minden útvonalat átadunk a `ParallelRecognizer`‑nek. A `recognizeAsync` metódus egy `Future<OcrResult>`‑ot ad vissza, amelyet később lekérhetünk.

```java
import java.util.concurrent.*;

// ...

// Step 4: Submit each image for asynchronous recognition
List<Future<OcrResult>> recognitionFutures = new ArrayList<>();

for (Path image : imagePaths) {
    Future<OcrResult> future = parallelRecognizer.recognizeAsync(
            image.toString(),
            RecognitionLanguage.ENGLISH); // Change language if needed
    recognitionFutures.add(future);
}
```

> **Mi történik a háttérben?** Minden hívás egy feladatot helyez be a recognizer belső executor szolgáltatásába. A feladatok párhuzamosan futnak, így egy 100 képet tartalmazó mappa feldolgozása jóval kevesebb időt vesz igénybe, mint egy egy‑szálas ciklus esetén.

---

## 5. lépés – Eredmények lekérése az eredeti sorrendben – Fájl sorrend megőrzése

Mivel a `Future`‑kat ugyanabban a sorrendben tároltuk, ahogy az `imagePaths` listában voltak, egyszerűen végigiterálhatunk a listán, és meghívhatjuk a `get()`‑et. A hívás csak addig blokkol, amíg az adott kép feldolgozása be nem fejeződik, így a sorrend megmarad extra nyilvántartás nélkül.

```java
// Step 5: Retrieve and display the OCR results in the original order
for (int i = 0; i < recognitionFutures.size(); i++) {
    try {
        OcrResult result = recognitionFutures.get(i).get(); // blocks if not ready
        System.out.println("File: " + imagePaths.get(i).getFileName());
        System.out.println(result.getText()); // The extracted text
        System.out.println("-----");
    } catch (InterruptedException | ExecutionException e) {
        System.err.println("Failed to process " + imagePaths.get(i) + ": " + e.getMessage());
    }
}
```

**Minta konzol kimenet** (rövidítve):

```
File: invoice_001.png
Invoice #001
Date: 2024‑03‑15
Total: $1,250.00
-----
File: receipt_202403.jpg
Receipt
Item A - $45.00
Item B - $30.00
Grand Total: $75.00
-----
```

> **Szélsőséges eset kezelése:** Ha egy adott kép kivételt dob (sérült fájl, nem támogatott formátum), elkapjuk, és a többi feldolgozása folytatódik – ez egy alapvető szokás a megbízható **kötetes OCR feldolgozási** csővezetékeknél.

---

## 6. lépés – Takarítás – Recognizer leállítása

Soha ne felejtsd el leállítani a belső szálkészletet; különben a JVM a kilépéskor elakadhat.

```java
// Step 6: Shut down the recognizer to clean up its internal thread pool
parallelRecognizer.shutdown();
```

Ennyi! A program most már bármely könyvtárat bejár, PNG/JPG fájlokra szűr, párhuzamosan futtat OCR‑t, és kiírja az eredményeket.

---

## Teljes működő példa

Az alábbiakban megtalálod a komplett, másolás‑beillesztés‑kész Java osztályt. Cseréld le a `"YOUR_DIRECTORY"`‑t a képeid mappájának elérési útjára, és futtasd az IDE‑dből vagy a parancssorból.

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.ParallelRecognizer;
import com.aspose.ocr.OcrResult;
import com.aspose.ocr.RecognitionLanguage;

import java.nio.file.*;
import java.util.*;
import java.util.concurrent.*;
import java.util.stream.Collectors;

public class BatchParallelExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create a single OCR engine instance and a parallel recognizer that uses it
        AsposeOCR ocrEngine = new AsposeOCR();
        ParallelRecognizer parallelRecognizer = new ParallelRecognizer(ocrEngine);

        // Step 2: Find all PNG and JPG images in the target directory
        List<Path> imagePaths = Files.walk(Paths.get("YOUR_DIRECTORY"))
                .filter(p -> {
                    String lower = p.toString().toLowerCase();
                    return lower.endsWith(".png") || lower.endsWith(".jpg");
                })
                .collect(Collectors.toList());

        if (imagePaths.isEmpty()) {
            System.out.println("No images found – nothing to convert.");
            parallelRecognizer.shutdown();
            return;
        }

        // Step 3: Submit each image for asynchronous recognition
        List<Future<OcrResult>> recognitionFutures = new ArrayList<>();
        for (Path image : imagePaths) {
            recognitionFutures.add(
                    parallelRecognizer.recognizeAsync(
                            image.toString(),
                            RecognitionLanguage.ENGLISH));
        }

        // Step 4: Retrieve and display the OCR results in the original order
        for (int i = 0; i < recognitionFutures.size(); i++) {
            try {
                OcrResult result = recognitionFutures.get(i).get(); // blocks until processed
                System.out.println("File: " + imagePaths.get(i).getFileName());
                System.out.println(result.getText());
                System.out.println("-----");
            } catch (InterruptedException | ExecutionException e) {
                System.err.println("Error processing " + imagePaths.get(i) + ": " + e.getMessage());
            }
        }

        // Step 5: Shut down the recognizer to clean up its internal thread pool
        parallelRecognizer.shutdown();
    }
}
```

Futtasd az osztályt, figyeld, ahogy a konzol megtelik kinyert karakterláncokkal, és ünnepeld, hogy **képeket szöveggé konvertáltál** anélkül, hogy egyetlen blokkoló I/O‑ciklust is írtál volna.

---

## Gyakran Ismételt Kérdések (GYIK)

**Q: Feldolgozhatok PDF‑eket vagy TIFF‑eket is?**  
A: Természetesen. Az Aspose OCR számos formátumot támogat – csak add hozzá a megfelelő fájlkiterjesztéseket a 2. lépésben lévő szűrőhöz.

**Q: Mi van, ha más nyelvre, például spanyolra van szükségem?**  
A: Cseréld le a `RecognitionLanguage.ENGLISH`‑t `RecognitionLanguage.SPANISH`‑ra. Győződj meg róla, hogy a nyelvi csomag telepítve van (az Aspose a legtöbb főbb nyelvet alapból tartalmazza).

**Q: A mappám almappákat is tartalmaz – be lesznek-e olvasva?**  
A: Igen. A `Files.walk` rekurzívan bejárja az egész fastruktúrát, így minden beágyazott PNG/J

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}