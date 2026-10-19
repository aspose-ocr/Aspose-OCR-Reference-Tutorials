---
category: general
date: 2026-05-03
description: Hozzon létre fix szálpoolt Java-ban a képek szövegének gyors kinyeréséhez.
  Tanulja meg, hogyan futtasson OCR-t, konvertálja a képet szöveggé, és növelje a
  teljesítményt párhuzamos OCR-feldolgozással.
draft: false
keywords:
- create fixed thread pool
- extract text from images
- how to run OCR
- convert image to text
- parallel OCR processing
language: hu
og_description: Készíts rögzített szálkészletet Java-ban, hogy gyorsan szöveget nyerj
  ki képekből. Tanuld meg, hogyan futtass OCR-t, konvertáld a képet szöveggé, és növeld
  a teljesítményt párhuzamos OCR-feldolgozással.
og_title: Fix szálkészlet létrehozása párhuzamos OCR-hez Java-ban
tags:
- Java
- OCR
- Multithreading
title: Fix szálkészlet létrehozása párhuzamos OCR-hez Java-ban
url: /hu/java/advanced-ocr-techniques/create-fixed-thread-pool-for-parallel-ocr-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Fix szálcsoport létrehozása párhuzamos OCR-hez Java-ban

Valaha szükséged volt **fix szálcsoport létrehozására**, hogy felgyorsítsd az OCR feladatokat, de nem tudtad, hol kezdjed? Nem vagy egyedül. Sok képalapú projektben a szűk keresztmetszet az egy szálas OCR hívás, és a megoldás meglepően egyszerű: indíts egy munkás szálcsoportot, és hagyd, hogy párhuzamosan dolgozzák fel a fájlokat.  

Ebben az útmutatóban megtanulod, hogyan **nyerj ki szöveget képekből** az Aspose OCR használatával, hogyan **futtass OCR-t** hatékonyan, és hogyan **alakítsd át a képet szöveggé** anélkül, hogy leterhelnéd a CPU-t. A végére egy kész‑a‑futtatásra Java programod lesz, amely bemutatja a **párhuzamos OCR feldolgozást** néhány mintaképen.

## Mit fogsz építeni

* Beolvas egy listát a képek útvonalairól (PNG, JPG, TIFF, BMP).
* **Fix szálcsoportot hoz létre**, amely a CPU magok számához igazodik.
* Minden képhez OCR feladatot küld el.
* Összegyűjti a felismert szöveget, és kiírja a konzolra.
* Tiszta módon leállítja az executor-t.

Nincs szükség külső build eszközökre, nincs bonyolult keretrendszer—csak tiszta Java és az Aspose OCR könyvtár. Ha van Java 8+ és egy megfelelő IDE-d, készen állsz.

## Előfeltételek

* **Java Development Kit (JDK) 8 vagy újabb** – a kód lambda‑kat használ, ezért a régebbi verziók nem fordulnak le.
* **Aspose OCR for Java** – töltsd le a JAR‑t az Aspose weboldaláról, vagy szerezd be Maven‑en keresztül (`com.aspose:aspose-ocr`).
* Egy mappa néhány tesztképpel (a kód a `YOUR_DIRECTORY`‑re mutat).  
* Alapvető ismeretek a Java párhuzamosságról (a többit majd elmagyarázzuk).

> *Pro tipp:* Ha Maven‑t használsz, add hozzá a függőséget a `pom.xml`‑hez, és hagyd, hogy az IDE kezelje az osztályútvonalat.  

---

## 1. lépés: A szükséges importok hozzáadása

Először is hozd be a szükséges osztályokat a láthatóságba. Ez nem csak sablonkód; minden import megmondja a JVM‑nek, hol találja az OCR motor, a képkezelő segédprogramok és a párhuzamossági eszközök, amelyek lehetővé teszik, hogy **fix szálcsoportot hozzunk létre**.

```java
import com.aspose.ocr.*;
import java.util.*;
import java.util.concurrent.*;
```

* `com.aspose.ocr.*` – az alap OCR API.  
* `java.util.*` – gyűjtemények a képek útvonalainak és eredményeknek a tárolásához.  
* `java.util.concurrent.*` – a párhuzamossági csomag, amely tartalmazza az `ExecutorService`‑t és a `Future`‑t.

## 2. lépés: A feldolgozandó képek meghatározása

Ezután felsoroljuk azokat a fájlokat, amelyekből **szöveget szeretnénk kinyerni képekből**. Az `Arrays.asList` használata tömör kódot eredményez, és lehetővé teszi, hogy a saját könyvtáradat cseréld be anélkül, hogy a többi logikát módosítanád.

```java
List<String> imagePaths = Arrays.asList(
        "YOUR_DIRECTORY/image1.png",
        "YOUR_DIRECTORY/image2.jpg",
        "YOUR_DIRECTORY/image3.tif",
        "YOUR_DIRECTORY/image4.bmp"
);
```

Nyugodtan adj hozzá további bejegyzéseket; a szálcsoport automatikusan méreteződik a rendelkezésedre álló CPU magok száma alapján.

## 3. lépés: **Fix szálcsoport létrehozása** a CPU magoknak megfelelően

Itt van az útmutató szíve. Megkérdezzük a futtatókörnyezetet, hogy hány mag áll rendelkezésre, és a `Executors` gyártól kérünk egy pontosan ennyi méretű szálcsoportot. Miért fix? Mert egy előre meghatározott szál szám megakadályozza a rettegett „szálrobbanást”, amely az operációs rendszert erőforráshiányba taszíthatja.

```java
int coreCount = Runtime.getRuntime().availableProcessors();
ExecutorService executor = Executors.newFixedThreadPool(coreCount);
```

* `availableProcessors()` visszaadja a logikai magok számát (beleértve a hyper‑threadeket).  
* `newFixedThreadPool(coreCount)` garantálja, hogy soha ne lépjük túl a CPU kapacitását, ami a legbiztonságosabb módja a **párhuzamos OCR futtatásának**.

## 4. lépés: OCR feladat benyújtása minden képhez

Most minden fájlútvonalat egy callable‑vá alakítunk, amely **futtatja az OCR‑t**, felismeri a szöveget, és visszaadja az eredményt. Vedd észre, hogy a lambda‑ban egy új `OcrEngine` példányt hozunk létre – ez elkerüli a motor állapotának szálbiztonságtól nem védett megosztását.

```java
List<Future<String>> ocrResults = new ArrayList<>();
for (String path : imagePaths) {
    ocrResults.add(executor.submit(() -> {
        OcrEngine engine = new OcrEngine();          // fresh engine per task
        engine.setImage(ImageStream.fromFile(path));
        engine.getLanguage().setEnglish(true);
        return engine.recognize() ? engine.getText()
                                   : "Failed: " + path;
    }));
}
```

* Minden `submit` hívás átadja a lambda‑t a szálcsoportnak, amely egy üresjáró szálra ütemezi.  
* A `Future<String>` objektumok lehetővé teszik, hogy később lekérdezzük a felismert szöveget, megőrizve a sorrendet, ha szükséges.

## 5. lépés: A felismert szöveg lekérése és megjelenítése

Miután az összes feladat sorba került, egyszerűen végigiterálunk a `Future` listán, és a `get()` hívással blokkolunk, amíg az egyes OCR feladatok befejeződnek. Itt válik láthatóvá a **kép szöveggé alakítása** lépés: az `engine.getText()` hívás visszaadja a nyers karakterláncot.

```java
for (Future<String> result : ocrResults) {
    System.out.println("OCR result:\n" + result.get());
}
```

A tipikus konzolkimenet így néz ki:

```
OCR result:
Hello world!
OCR result:
Invoice #12345
Date: 2026‑04‑30
...
```

Ha egy fájl hibát okoz (például sérült), egy `Failed:` kezdetű sor jelenik meg, amelyet az útvonal követ – praktikus a gyors hibakereséshez.

## 6. lépés: Az Executor Service tisztítása

Soha ne felejtsd el leállítani a szálcsoportot; különben a JVM tovább fut, mintha még lenne munka. Egy elegáns leállítás lehetővé teszi, hogy a futó feladatok befejeződjenek, mielőtt a folyamat kilép.

```java
executor.shutdown();
```

Használhatod az `awaitTermination` hívást is, ha időkorlátot szeretnél érvényesíteni, de a legtöbb parancssori segédeszközhöz egy egyszerű `shutdown()` elegendő.

## Teljes működő példa

Az alábbiakban a teljes, azonnal futtatható program látható. Másold be egy `ParallelOcrTutorial.java` nevű fájlba, állítsd be a képek útvonalait, és futtasd a `javac` + `java` parancsokkal, ahogy szokás.

```java
import com.aspose.ocr.*;
import java.util.*;
import java.util.concurrent.*;

public class ParallelOcrTutorial {
    public static void main(String[] args) throws Exception {
        // Step 2: Define the images to be processed
        List<String> imagePaths = Arrays.asList(
                "YOUR_DIRECTORY/image1.png",
                "YOUR_DIRECTORY/image2.jpg",
                "YOUR_DIRECTORY/image3.tif",
                "YOUR_DIRECTORY/image4.bmp"
        );

        // Step 3: Create a fixed‑size thread pool matching the CPU cores
        int coreCount = Runtime.getRuntime().availableProcessors();
        ExecutorService executor = Executors.newFixedThreadPool(coreCount);

        // Step 4: Submit an OCR task for each image
        List<Future<String>> ocrResults = new ArrayList<>();
        for (String path : imagePaths) {
            ocrResults.add(executor.submit(() -> {
                OcrEngine engine = new OcrEngine();          // fresh engine per task
                engine.setImage(ImageStream.fromFile(path));
                engine.getLanguage().setEnglish(true);
                return engine.recognize() ? engine.getText()
                                           : "Failed: " + path;
            }));
        }

        // Step 5: Retrieve and display the recognized text
        for (Future<String> result : ocrResults) {
            System.out.println("OCR result:\n" + result.get());
        }

        // Step 6: Clean up the executor service
        executor.shutdown();
    }
}
```

**Várható eredmény:** minden kép szöveges tartalma ki lesz nyomtatva a konzolra, ugyanabban a sorrendben, mint az `imagePaths` lista. Ha egy képet nem lehet feldolgozni, egy hibaüzenetet látsz majd egy üres sor helyett.

## Gyakori kérdések és szélhelyzetek

### Mi van, ha több képet szeretnék feldolgozni, mint amennyi szál van?

A fix szálcsoport automatikusan sorba állítja a felesleges feladatokat. Amint egy szál befejezi a jelenlegi OCR feladatát, felveszi a következőt. Ez a sorba állítás a **párhuzamos OCR feldolgozás** lényege – maximális áteresztőképességet kapsz anélkül, hogy túlterhelnéd a CPU-t.

### Megváltoztathatom a nyelvet?

Természetesen. Cseréld le a `engine.getLanguage().setEnglish(true);` sort a megfelelő nyelvi flagre, például `setFrench(true)`, vagy több nyelvet engedélyezhetsz több setter hívásával a `recognize()` előtt.

### Hogyan kezeljem a nagyon nagy képeket?

A nagy fájlok szálanként jelentős memóriát fogyaszthatnak. Ha `OutOfMemoryError`-t észlelsz, fontold meg a kép lecsökkentését, mielőtt a motorba adod, vagy növeld a heap méretét a `-Xmx` kapcsolóval. Egy másik megközelítés a **cached thread pool** használata (`

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}