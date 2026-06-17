---
category: general
date: 2026-02-17
description: Tanulja meg, hogyan használjon fix szálkészletet Java-ban a PNG képek
  szövegének párhuzamos OCR feldolgozással történő kinyeréséhez, és hogyan állítsa
  le megfelelően az executor szolgáltatást.
draft: false
keywords:
- fixed thread pool java
- extract text from png
- parallel ocr processing
- convert scanned pages text
- shut down executor service
language: hu
og_description: Fedezze fel, hogyan tud egy fix szálkészletű Java párhuzamosan szöveget
  kinyerni PNG képekből, átalakítani a beolvasott oldalak szövegét, és biztonságosan
  leállítani az executor szolgáltatást.
og_title: fix szálkészlet Java – párhuzamos OCR PNG-hez
tags:
- java
- ocr
- multithreading
- aspose
title: Fix szálkészlet Java – párhuzamos OCR PNG-hez
url: /hu/java/advanced-ocr-techniques/fixed-thread-pool-java-parallel-ocr-for-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# fix szálkészlet Java – párhuzamos OCR PNG-hez

Valaha is elgondolkodtál, hogyan lehet felgyorsítani az OCR-t egy csomó PNG fájlon a **fixed thread pool java** használatával? Ebben az útmutatóban végigvezetünk a **extract text from PNG** képek párhuzamos feldolgozásán, a **convert scanned pages text** szerkeszthető karakterláncokká alakításán, és biztonságosan **shut down executor service** a munka befejezése után.

Ha már valaha egy egy‑szálas ciklusra bámultál, amely perceken át húzódik, ismered azt a frusztrációt, amikor minden oldal befejezésére vársz, mielőtt a következő elindulna. A jó hír? Néhány Java‑sorral és az Aspose OCR‑rel kiaknázhatod az összes CPU‑magod erejét, a beolvasott oldalakat kereshető szöveggé alakíthatod, és az alkalmazásod továbbra is reagálékony marad.  

Alább egy teljes, azonnal futtatható példát találsz, valamint magyarázatot arra, hogy miért fontos minden rész, gyakori buktatókat és tippeket, amelyeket bármely OCR‑könyvtárra alkalmazhatsz.

---

## Amire szükséged lesz

- **Java 17** (vagy bármely újabb JDK) – a kód csak néhány helyen használja a modern `var` szintaxist, de régebbi verziókon is működik.  
- **Aspose.OCR for Java** könyvtár – letöltheted a Maven Central‑ról vagy egy próbaverziót az Aspose‑tól.  
- Egy sor **PNG** fájl, amelyet feldolgozni szeretnél – gondolj beolvasott nyugtákra, könyvlapokra vagy képernyőképekre.  
- Alapvető ismeretek a Java párhuzamosságról – nem kötelező, de hasznos.

Ennyi. Nincs külső szolgáltatás, nincs Docker, csak tiszta Java és egy kis multithreading varázslat.

---

## 1. lépés: Aspose OCR függőség és licenc hozzáadása (opcionális)

Először győződj meg róla, hogy az Aspose OCR JAR a classpath‑odban van. Maven‑t használva add hozzá:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version>
</dependency>
```

Ha nincs licenced, a könyvtár értékelő módban fog futni; a kód ugyanúgy működik. Licenc betöltéséhez (ajánlott éles környezetben) helyezd az `Aspose.OCR.lic` fájlt a resources mappádba, és használd:

```java
// Load the Aspose OCR license (optional)
License license = new License();
license.setLicense("Aspose.OCR.lic");
```

> **Pro tip:** Tartsd a licencfájlt a verziókezelésen kívül, hogy elkerüld a véletlen kiszivárgást.

---

## 2. lépés: Hozz létre egy szálbiztos `OcrEngine` példányt

Az Aspose OCR `OcrEngine` szálbiztos, amíg ugyanazt a példányt használod a feladatok között. Egyszeri létrehozása memóriát takarít meg és elkerüli a motor minden egyes képhez való újra‑inicializálásának költségét.

```java
// One shared OcrEngine for all threads
OcrEngine ocrEngine = new OcrEngine();
```

Miért újrahasználni? Gondolj a motorra, mint egy nehéz súlyú munkásra, amely a nyelvi modelleket memóriába tölti. Minden képhez új motor indítása olyan lenne, mintha minden apró feladathoz új szakértőt alkalmaznál – költséges és szükségtelen.

---

## 3. lépés: Állíts be egy fix szálkészletet Java‑ban

Most jön a főszereplő: egy **fixed thread pool java**. Méretét a logikai processzorok számához igazítjuk, így minden mag kap munkát anélkül, hogy túlterhelnénk őket.

```java
// Determine available processors and create a fixed pool
int threadCount = Runtime.getRuntime().availableProcessors();
ExecutorService threadPool = Executors.newFixedThreadPool(threadCount);
```

Egy *fix* pool (a cache‑elt helyett) kiszámítható erőforrás‑használatot biztosít, és megakadályozza a rettenetes „out‑of‑memory” csúcsokat, amikor egyszerre több száz kép érkezik.

---

## 4. lépés: Listázd a feldolgozni kívánt PNG fájlokat (Extract Text from PNG)

Gyűjtsd össze azoknak a képeknek az elérési útját, amelyeket OCR‑elni szeretnél. Egy valódi projektben egy könyvtár beolvasásával vagy adatbázisból olvasással oldanád meg; itt néhány példát hard‑code‑olunk.

```java
List<String> imageFiles = Arrays.asList(
        "YOUR_DIRECTORY/page1.png",
        "YOUR_DIRECTORY/page2.png",
        "YOUR_DIRECTORY/page3.png"
);
```

> **Megjegyzés:** A **png** fájlkiterjesztés fontos, mert az Aspose OCR automatikusan felismeri a formátumot, de JPEG‑et vagy TIFF‑et is megadhatsz.

---

## 5. lépés: Küldd el az OCR feladatokat – párhuzamos OCR feldolgozás

Minden kép egy callable‑t kap, amely a felismert szöveget adja vissza. Mivel az `OcrEngine` megosztott, csak a fájlútvonalat kell átadni a feladatnak.

```java
List<Future<String>> ocrFutures = new ArrayList<>();

for (String imagePath : imageFiles) {
    ocrFutures.add(threadPool.submit(() -> {
        // Prepare input for this image
        OcrInput input = new OcrInput();
        input.add(imagePath);

        // Perform OCR using the shared engine
        OcrResult result = ocrEngine.recognize(input);

        // Return the plain text
        return result.getText();
    }));
}
```

Miért csomagoljuk `Future`‑ba? Lehetővé teszi, hogy az összes feladatot azonnal elindítsuk, majd később a benyújtási sorrendben gyűjtsük össze az eredményeket – tökéletes a lapok sorrendjének megőrzéséhez, amikor **convert scanned pages text** vissza egy dokumentumba.

---

## 6. lépés: Eredmények lekérése és megjelenítés (Convert Scanned Pages Text)

Most várunk minden `Future` befejezésére, és kiírjuk a kimenetet. A `get()` hívás csak a konkrét feladat befejezéséig blokkol, nem az egész pool‑t.

```java
for (Future<String> future : ocrFutures) {
    System.out.println("----");
    System.out.println(future.get()); // prints OCR result for one PNG
}
```

A tipikus konzolkimenet például:

```
----
The quick brown fox jumps over the lazy dog.
----
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
----
Page 3 content goes here…
```

Ha inkább fájlokba írnád az eredményeket, cseréld le a `System.out.println`‑t egy `Files.writeString` hívásra.

---

## 7. lépés: A Executor Service tiszta leállítása

Amikor minden feladat befejeződött, elengedhetetlen a **shut down executor service**, különben a JVM nem‑daemon szálak miatt nem tud rendesen kilépni.

```java
threadPool.shutdown();               // No new tasks accepted
if (!threadPool.awaitTermination(60, TimeUnit.SECONDS)) {
    threadPool.shutdownNow();        // Force shutdown after timeout
}
```

Az `awaitTermination` minta lehetőséget ad a pool‑nak, hogy befejezze a futó munkákat, mielőtt kényszerítenénk a leállítást. Ennek a lépésnek a kihagyása gyakori memória‑szivárgáshoz vezet hosszú‑futású alkalmazásokban.

---

## Teljes működő példa

Összeállítva, itt a teljes program, amelyet bemásolhatsz a `ParallelBatchDemo.java` fájlba és futtathatsz:

```java
import com.aspose.ocr.*;

import java.util.*;
import java.util.concurrent.*;

public class ParallelBatchDemo {
    public static main(String[] args) throws Exception {
        // 1️⃣ Load license (optional)
        License license = new License();
        license.setLicense("Aspose.OCR.lic");

        // 2️⃣ Shared, thread‑safe OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 3️⃣ Fixed thread pool java – one thread per core
        int threadCount = Runtime.getRuntime().availableProcessors();
        ExecutorService threadPool = Executors.newFixedThreadPool(threadCount);

        // 4️⃣ Files to process – extract text from png
        List<String> imageFiles = Arrays.asList(
                "YOUR_DIRECTORY/page1.png",
                "YOUR_DIRECTORY/page2.png",
                "YOUR_DIRECTORY/page3.png"
        );

        // 5️⃣ Submit tasks – parallel OCR processing
        List<Future<String>> ocrFutures = new ArrayList<>();
        for (String imagePath : imageFiles) {
            ocrFutures.add(threadPool.submit(() -> {
                OcrInput input = new OcrInput();
                input.add(imagePath);
                OcrResult result = ocrEngine.recognize(input);
                return result.getText();
            }));
        }

        // 6️⃣ Retrieve and print – convert scanned pages text
        for (Future<String> future : ocrFutures) {
            System.out.println("----");
            System.out.println(future.get());
        }

        // 7️⃣ Shut down executor service cleanly
        threadPool.shutdown();
        if (!threadPool.awaitTermination(60, TimeUnit.SECONDS)) {
            threadPool.shutdownNow();

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}