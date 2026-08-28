---
category: general
date: 2026-08-28
description: Ismerje meg, hogyan lehet szöveget kinyerni png képekből Java-ban az
  Aspose OCR segítségével. Ez az útmutató a kötegelt OCR feldolgozást, a képek mappából
  történő beolvasását és a fájlok kiterjesztés szerinti szűrését tárgyalja.
draft: false
keywords:
- extract text from png
- read images from folder
- filter files by extension
- how to batch ocr
- aspose ocr java tutorial
lastmod: 2026-08-28
og_description: Ismerje meg, hogyan lehet szöveget kinyerni png képekből Java-ban
  az Aspose OCR segítségével. Ez az útmutató a kötegelt OCR feldolgozást, a képek
  mappából történő beolvasását és a fájlok kiterjesztés szerinti szűrését tárgyalja.
og_image_alt: 'Developer guide: extract text from png images in Java using Aspose
  OCR'
og_title: Hogyan lehet szöveget kinyerni png-ből Java-ban – kötegelt OCR útmutató
schemas:
- author: Aspose
  dateModified: '2026-08-28'
  description: Learn how to extract text from png images in Java using Aspose OCR.
    This tutorial covers batch OCR processing, reading images from a folder, and filtering
    files by extension.
  headline: How to extract text from png in Java – batch OCR guide
  type: TechArticle
- questions:
  - answer: Absolutely. Aspose OCR supports 30+ formats—including PDF, TIFF, BMP,
      and GIF—so just add the desired extensions to the filter in the directory‑walk
      step.
    question: Can I process PDFs or TIFFs as well?
  - answer: Change `RecognitionLanguage.ENGLISH` to `RecognitionLanguage.SPANISH`
      (or any supported language). The language packs are bundled with the library,
      so no extra download is required.
    question: What if I need a language other than English, such as Spanish?
  - answer: Yes. `Files.walk` traverses the entire tree recursively, so every nested
      PNG/J
    question: My folder contains sub‑folders—will they be scanned?
  - answer: Enable streaming mode by calling `ocrEngine.setUseStreaming(true)`. This
      tells the engine to read the image in chunks, dramatically reducing peak memory
      usage.
    question: How do I handle extremely large images that exceed 200 MB?
  - answer: Yes. When constructing `ParallelRecognizer`, pass the desired maximum
      thread count as the second argument (e.g., `new ParallelRecognizer(ocrEngine,
      4)`).
    question: Is there a way to limit the number of concurrent OCR threads?
  type: FAQPage
tags:
- OCR
- Java
- Aspose
title: Hogyan lehet szöveget kinyerni png-ből Java-ban – kötegelt OCR útmutató
url: /hu/java/ocr-operations/convert-images-to-text-in-java-batch-ocr-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan lehet szöveget kinyerni png-ből Java-ban – kötegelt OCR útmutató

Ha valaha is **szöveget kellett kinyerni png** fájlokból, de nem tudtad, hogyan skálázhatod a műveletet egy csomó kép fölé, jó helyen vagy. Sok fejlesztő egyetlen kép OCR hívással kezd, és gyorsan teljesítménykorlátokba ütközik, amikor a mappa tucatnyi vagy akár száz fájlra nő. Az Aspose OCR for Java segítségével egy robusztus kötegelt OCR csővezetéket hozhatsz létre, amely bejár egy könyvtárat, csak a kívánt képtípusokat szűri, párhuzamosan futtatja a felismerést, és az eredményeket ugyanabban a sorrendben adja vissza, mint a forrásfájlok. A végére egy kész Java kódrészletet kapsz, amely megbízhatóan és hatékonyan kezeli a **kötegelt OCR feldolgozást**.

![Képek szöveggé konvertálása példa](https://example.com/convert-images-to-text.png "Képernyőkép a Java konzol kimenetéről, amely a PNG fájlokból konvertált szöveget mutatja")

## Gyors válaszok
- **Melyik könyvtár kezeli az OCR-t?** Aspose OCR for Java.
- **Feldolgozhatom a PNG és JPG fájlokat együtt?** Igen – a minta mindkét kiterjesztést szűri.
- **Az OCR motor szálbiztos?** Egyetlen megosztott `AsposeOCR` példány biztonságosan használható párhuzamosan.
- **Szükségem van licencre a teszteléshez?** Egy ingyenes ideiglenes kulcs elérhető az Aspose-tól.
- **Alkönyvtárak automatikusan be lesznek járva?** A `Files.walk` rekurzívan bejárja az egész fát.

## Mi az a szöveg kinyerése png-ből?

A `extract text from png` a optikai karakterfelismerés (OCR) alkalmazását jelenti a Portable Network Graphics fájlokra, hogy a látható karakterek kereshető, szerkeszthető karakterláncokká váljanak. Az Aspose OCR motorja pixel adatokat olvas, felismeri a glifformákat, és egyetlen metódushívásban Unicode szöveget ad vissza.

## Miért használjuk az Aspose OCR for Java-t?

Az Aspose OCR **30+ nyelvet** támogat, akár **500 képet percenként** képes feldolgozni egy szabványos 8‑magos szerveren, és **200 MB**-ig terjedő fájlokat kezel anélkül, hogy az egész képet memóriába töltené. Ezek a számszerű képességek lehetővé teszik, hogy megbízhatóan futtass nagy léptékű kötegelt feladatokat átlagos hardveren, memóriahatárokba ütközés nélkül.

## Előfeltételek
- Java 17 (vagy bármely friss LTS verzió).
- Maven vagy Gradle a függőségkezeléshez.
- Egy könyvtár, amely PNG/JPG képeket tartalmaz, amelyeket feldolgozni szeretnél.
- Alapvető ismeretek a Java stream-ekről és a `java.nio.file` csomagról.
- (Opcionális) Aspose OCR ideiglenes licenckulcs értékeléshez.

> **Pro tipp:** Az ingyenes ideiglenes kulcs 30 nap után lejár, de teljes API hozzáférést biztosít a teszteléshez.

## Hogyan tartja meg a kötegelt OCR csővezeték a sorrendet?

A `Future<OcrResult>` egy függőben lévő OCR eredményt képvisel, amely a feldolgozás befejezése után lekérhető. A csővezeték az eredeti fájlsorrendet úgy őrzi meg, hogy a `Future<OcrResult>` objektumokat egy listában tárolja, amely tükrözi a bemeneti `Path` gyűjtemény sorrendjét. Amikor később iterálsz a future-ökön és meghívod a `get()`-et, minden hívás csak a hozzá tartozó képre blokkol, így a kimeneti sorozat megegyezik a bemeneti sorozattal extra rendezés nélkül.

## Mi az az Aspose OCR for Java?

Az `AsposeOCR` az Aspose OCR könyvtár központi osztálya, amely magába foglalja az összes nyelvi csomagot, a felismerési beállításokat és a belső natív erőforrásokat. Egy alkalmazás életciklusa során egyszer kell példányosítani, és biztonságosan megosztható több szál között. Mivel a nyelvi adatokat csak egyszer tölti be, ugyanannak az instance-nek a újrahasználata csökkenti a inicializálási terhelést és növeli a kötegelt műveletek áteresztőképességét.

## Hogyan állítsuk be a projektet és adjuk hozzá az Aspose OCR-t

Először hozz létre egy Maven (vagy Gradle) projektet, és add hozzá az Aspose OCR függőséget a `pom.xml`-hez:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>24.10</version>
</dependency>
```

> **Miért fontos:** A függőség előre deklarálása biztosítja, hogy a fordító lássa az `AsposeOCR`, `ParallelRecognizer` és a kapcsolódó osztályokat. Emellett garantálja, hogy minden gépen ugyanaz a verzió legyen használva, ami elengedhetetlen a reprodukálható **kötegelt OCR feldolgozáshoz**.

Frissítsd az IDE-t a build befejezése után; most már látnod kell az Aspose csomagokat a **External Libraries** alatt.

## Hogyan inicializáljuk az OCR motort – egyetlen példány megosztása

Az `AsposeOCR` a fő OCR motorosztály, amelyet az Aspose OCR könyvtár biztosít. Csak **egy** OCR motor példányra van szükségünk a teljes futtatáshoz. A szálak közötti megosztás memóriát takarít meg és felgyorsítja a folyamatot, mivel a motor csak egyszer tölti be a nyelvi csomagokat.

```java
AsposeOCR ocrEngine = new AsposeOCR("YOUR_LICENSE_KEY");
```

Az `AsposeOCR` szálbiztos, ezért nyugodtan átadhatod egy `ParallelRecognizer`-nek, amely egy munkás szálcsoportot kezel.

> **Magyarázat:** A `ParallelRecognizer` a motort egy szálpoolba csomagolja. Amikor sok fájlt küldesz be, mindegyik saját munkás szálat kap, ami valódi párhuzamosságot tesz lehetővé többmagos CPU-ken.

## Hogyan olvassuk be a képeket a mappából – a könyvtárfa bejárása

A `Files.walk` egy Java NIO metódus, amely rekurzívan bejár egy fájrafát, és `Path` objektumok stream-jét adja vissza. Most **be kell olvasnunk a képeket a mappából**, és összegyűjteni minden PNG vagy JPG fájlt. A `Files.walk` API ezt egy soros megoldássá teszi, de hozzáadunk egy szűrőt, hogy csak a **szöveg kinyerése png-ből** esetén szűrjünk.

```java
List<Path> imagePaths = Files.walk(Paths.get("YOUR_DIRECTORY"))
    .filter(Files::isRegularFile)
    .filter(p -> {
        String lower = p.toString().toLowerCase();
        return lower.endsWith(".png") || lower.endsWith(".jpg");
    })
    .collect(Collectors.toList());
```

> **Miért szűrünk itt:** A `filter` használatával **korán szűrhetünk fájlokat kiterjesztés szerint**, ami csökkenti a felesleges I/O-t később. Emellett a kód olvasható marad – nincs szükség bonyolult regexekre.

## Hogyan küldjünk OCR feladatokat aszinkron módon

A `recognizeAsync` egy képet küld az OCR motorhoz aszinkron feldolgozásra, és egy `Future<OcrResult>`-ot ad vissza, amely a függőben lévő eredményt képviseli. A fájlok listája készen áll, minden útvonalat a `ParallelRecognizer`-nek adunk. A `recognizeAsync` metódus egy `Future<OcrResult>`-ot ad vissza, amelyet később tárolunk.

```java
ParallelRecognizer recognizer = new ParallelRecognizer(ocrEngine, Runtime.getRuntime().availableProcessors());
List<Future<OcrResult>> futures = new ArrayList<>();

for (Path imagePath : imagePaths) {
    futures.add(recognizer.recognizeAsync(imagePath));
}
```

> **Mi történik a háttérben?** Minden hívás egy feladatot helyez be a recognizer belső executor szolgáltatásába. A feladatok párhuzamosan futnak, így egy 100 képet tartalmazó mappa töredékes idő alatt feldolgozható, amit egyetlen szálas ciklus igényelne.

## Hogyan nyerjük ki az eredményeket a fájl sorrend megőrzésével

A `Future<OcrResult>` egy aszinkron OCR feladat eredményét tárolja, és egy `get()` metódust biztosít a felismert szöveg lekéréséhez. Mivel a future-öket ugyanabban a sorrendben tároltuk, mint az `imagePaths`-t, egyszerűen iterálhatunk a listán és meghívhatjuk a `get()`-et. A hívás csak addig blokkol, amíg az adott kép be nem fejeződik, így a sorrend megmarad extra nyilvántartás nélkül.

```java
for (int i = 0; i < futures.size(); i++) {
    try {
        OcrResult result = futures.get(i).get();
        System.out.println("File: " + imagePaths.get(i).getFileName());
        System.out.println("Text: " + result.getText());
    } catch (Exception e) {
        System.err.println("Failed to process " + imagePaths.get(i) + ": " + e.getMessage());
    }
}
```

**Minta konzolkimenet** (rövidítve a tömörség kedvéért):

```
File: invoice1.png
Text: Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
...
```

> **Szélsőséges eset kezelése:** Ha egy adott kép kivételt dob (sérült fájl, nem támogatott formátum), elkapjuk és folytatjuk a többi feldolgozását – ez elengedhetetlen szokás a megbízható **kötegelt OCR feldolgozó** csővezetékekhez.

## Hogyan tisztítsuk meg az erőforrásokat – állítsuk le a recognizert

A `ParallelRecognizer.shutdown()` leállítja a belső szálpoolt, biztosítva, hogy minden OCR feladat befejeződjön, mielőtt az alkalmazás kilép. Soha ne felejtsd el leállítani a belső szálpoolt; ellenkező esetben a JVM a kilépéskor elakadhat.

```java
recognizer.shutdown();
```

Ennyi! A program most már bejár bármely könyvtárat, PNG/JPG fájlokra szűr, párhuzamosan futtat OCR-t, és az eredményeket az eredeti sorrendben írja ki.

---

## Teljes működő példa (másolás‑beillesztés)

Az alábbiakban a teljes, futtatható Java osztály található. Cseréld ki a `"YOUR_DIRECTORY"`-t a képek mappájának elérési útjára, és futtasd az IDE-ből vagy a parancssorból.

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.ParallelRecognizer;
import com.aspose.ocr.OcrResult;
import java.nio.file.*;
import java.util.*;
import java.util.concurrent.*;
import java.util.stream.*;

public class BatchOcrDemo {
    public static void main(String[] args) throws Exception {
        // Initialise the OCR engine (single shared instance)
        AsposeOCR ocrEngine = new AsposeOCR("YOUR_LICENSE_KEY");

        // Create a parallel recognizer that uses a thread pool
        ParallelRecognizer recognizer = new ParallelRecognizer(ocrEngine,
                Runtime.getRuntime().availableProcessors());

        // Walk the directory and collect PNG/JPG files
        List<Path> imagePaths = Files.walk(Paths.get("YOUR_DIRECTORY"))
                .filter(Files::isRegularFile)
                .filter(p -> {
                    String lower = p.toString().toLowerCase();
                    return lower.endsWith(".png") || lower.endsWith(".jpg");
                })
                .collect(Collectors.toList());

        // Submit OCR jobs asynchronously
        List<Future<OcrResult>> futures = new ArrayList<>();
        for (Path imagePath : imagePaths) {
            futures.add(recognizer.recognizeAsync(imagePath));
        }

        // Retrieve results in the original order
        for (int i = 0; i < futures.size(); i++) {
            try {
                OcrResult result = futures.get(i).get();
                System.out.println("File: " + imagePaths.get(i).getFileName());
                System.out.println("Text: " + result.getText());
            } catch (Exception e) {
                System.err.println("Failed to process " + imagePaths.get(i) + ": " + e.getMessage());
            }
        }

        // Clean up the recognizer's thread pool
        recognizer.shutdown();
    }
}
```

Futtasd az osztályt, nézd, ahogy a konzol megtelik kinyert karakterláncokkal, és ünnepeld, hogy **képeket szöveggé konvertáltál** anélkül, hogy egyetlen I/O‑ra blokkoló ciklust írtál volna.

---

## Gyakran ismételt kérdések (GYIK)

**K: Feldolgozhatok PDF-eket vagy TIFF-eket is?**  
V: Természetesen. Az Aspose OCR 30+ formátumot támogat – köztük PDF, TIFF, BMP és GIF – így csak add hozzá a kívánt kiterjesztéseket a könyvtár‑bejárás szűrőjéhez.

**K: Mi van, ha más nyelvre van szükségem, például spanyolra?**  
V: Cseréld le a `RecognitionLanguage.ENGLISH`-t `RecognitionLanguage.SPANISH`-ra (vagy bármely támogatott nyelvre). A nyelvi csomagok a könyvtárral együtt érkeznek, így nincs szükség extra letöltésre.

**K: A mappám almappákat is tartalmaz – be lesznek járva?**  
V: Igen. A `Files.walk` rekurzívan bejárja az egész fát, így minden beágyazott PNG/J

**K: Hogyan kezelem a 200 MB-nál nagyobb képeket?**  
V: Engedélyezd a streaming módot a `ocrEngine.setUseStreaming(true)` hívással. Ez a motor számára azt jelenti, hogy a képet darabokban olvassa, drámai módon csökkentve a csúcsteljesítmény memóriaigényét.

**K: Van mód a párhuzamos OCR szálak számának korlátozására?**  
V: Igen. A `ParallelRecognizer` létrehozásakor add meg a kívánt maximális szál számát második argumentumként (pl. `new ParallelRecognizer(ocrEngine, 4)`).

---

---

**Utoljára frissítve:** 2026-08-28  
**Tesztelve:** Aspose OCR for Java 24.10  
**Szerző:** Aspose  






```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Check the latest version on Maven Central -->
</dependency>
```

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

```java
// Step 6: Shut down the recognizer to clean up its internal thread pool
parallelRecognizer.shutdown();
```

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

## Kapcsolódó oktatóanyagok

- [Convert Images To Text In Java Batch Ocr Processing Guide](/ocr/java/ocr-operations/convert-images-to-text-in-java-batch-ocr-processing-guide/)
- [Read Text From Image In Java Complete Aspose Ocr Guide](/ocr/java/ocr-basics/read-text-from-image-in-java-complete-aspose-ocr-guide/)
- [Extract Text from Images Using Aspose.OCR – Allowed Characters](/ocr/java/advanced-ocr-techniques/specify-allowed-characters/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}