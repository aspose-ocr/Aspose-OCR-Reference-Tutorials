---
category: general
date: 2026-02-14
description: 'A kötegelt képes OCR egyszerűen: tanulja meg, hogyan lehet szöveget
  kinyerni PNG‑fájlokból az Aspose OCR és a párhuzamos feldolgozás használatával Java‑ban.'
draft: false
keywords:
- batch image OCR
- extract text from png
- parallel OCR Java
- Aspose OCR async
- OCR batch processing
language: hu
og_description: Kötegelt képes OCR oktatóanyag, amely bemutatja, hogyan lehet szöveget
  kinyerni PNG-fájlokból az Aspose OCR aszinkron API-jának Java nyelven történő használatával.
og_title: Kötegelt képek OCR-ja Java-ban – Gyors PNG szövegkivonás
tags:
- Java
- OCR
- Aspose
- Image Processing
title: Kötegelt képes OCR Java-ban – Szöveg gyors kinyerése PNG-fájlokból
url: /hu/java/ocr-operations/batch-image-ocr-in-java-extract-text-from-png-files-fast/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tömeges képes OCR Java-ban – Gyors szövegkinyerés PNG fájlokból

Valaha is szükséged volt **tömeges képes OCR** futtatására egy PNG beolvasott fájlok mappájában, de aggódtál a sebesség miatt? Nem vagy egyedül. Sok valós projektben – számlák digitalizálása, beolvasott könyvek archiválása vagy nyugták feldolgozása – a fejlesztőknek gyorsan és megbízhatóan kell **szöveget kinyerni PNG** képekből.

A jó hír? Az Aspose OCR aszinkron API-jával párhuzamos OCR csővezetéket indíthatsz néhány Java sorral. Ebben az útmutatóban végigvezetünk a teljes, futtatható megoldáson, elmagyarázzuk, miért fontos minden részlet, és megmutatjuk, hogyan ellenőrizheted az eredményeket. A végére egy önálló programod lesz, amely párhuzamosan dolgozza fel a teljes PNG fájl köteget, tiszta, helyesírás-ellenőrzött szöveget adva vissza.

## Mit fogsz megtanulni

- Hogyan listázz PNG fájlokat tömeges feldolgozáshoz  
- Az Aspose `OcrEngine` konfigurálása angol nyelvre és helyesírás‑javításra  
- OCR futtatása aszinkron módon a `processAsync`‑val és a `Future` eredmény kezelése  
- A felismert szöveg olvasása és megjelenítése minden képnél  
- Tippek a méretezéshez, hibakezeléshez és a teljesítmény finomhangolásához  

### Előfeltételek

- Java 8 vagy újabb telepítve (a kód a szabványos `java.util.concurrent` csomagot használja)  
- Aspose OCR for Java licenc vagy ingyenes próba (letölthető az Aspose weboldaláról)  
- Egy mappa, amely néhány PNG képernyőképet vagy beolvasott oldalt tartalmaz, amivel tesztelni szeretnél  

Most pedig vágjunk bele.

## 1. lépés – PNG fájlok összegyűjtése egy köteghez

Mielőtt az OCR motor bármit is csinálna, tudnia kell, mely képeket kell feldolgozni. A legegyszerűbb mód egy `List<String>` felépítése abszolút vagy relatív fájlutakkal.

```java
// Step 1: Prepare a list of PNG files you want to run OCR on
List<String> imageFiles = Arrays.asList(
        "YOUR_DIRECTORY/page1.png",
        "YOUR_DIRECTORY/page2.png",
        "YOUR_DIRECTORY/page3.png",
        "YOUR_DIRECTORY/page4.png");
```

**Miért fontos ez:**  
A lista előre létrehozása lehetővé teszi, hogy a motor minden fájlt önállóan ütemezzen, ami a valódi tömeges feldolgozás alapja. Ha később dinamikusan szeretnél egy könyvtárat beolvasni, csak cseréld le a statikus `Arrays.asList`-t egy `Files.walk` streamre.

## 2. lépés – Az Aspose OCR motor inicializálása és finomhangolása

Az Aspose `OcrEngine` rendkívül konfigurálható. Itt állítjuk be a nyelvet angolra és bekapcsoljuk a helyesírás‑javítást – két opció, amely drámaian javítja a kinyert szöveg minőségét, különösen zajos PNG beolvasások esetén.

```java
// Step 2: Create and configure the OCR engine
OcrEngine ocrEngine = new OcrEngine();
ocrEngine.getEngineOptions()
         .setLanguage(OcrLanguage.ENGLISH)          // English language model
         .setSpellCorrectionEnabled(true);          // Enable spell‑checking
```

**Miért ezek a beállítások:**  
- **Nyelvválasztás** megmondja a motornak, mely karakterkészletet és szótárat használja, csökkentve a hibás felismeréseket.  
- **Helyesírás‑javítás** elkapja a gyakori OCR félreolvasásokat (pl. „1” vs „l”) anélkül, hogy utófeldolgozást kellene végezni.

> **Pro tip:** Ha a képeiden több nyelv is szerepel, átadhatsz egy listát, például `setLanguage(OcrLanguage.ENGLISH, OcrLanguage.FRENCH)`.

## 3. lépés – Aszinkron kötegelt feldolgozás indítása

A nehéz munkát a `processAsync` végzi. Ez egy `Future<List<OcrResult>>`‑t ad vissza, ami lehetővé teszi, hogy a fő szál más feladatokkal is foglalkozzon, míg az OCR a háttérben fut.

```java
// Step 3: Start asynchronous processing of the image batch
Future<List<OcrResult>> ocrFuture = ocrEngine.processAsync(imageFiles);

// (Optional) Do something useful while OCR runs, e.g., log progress, load UI, etc.
System.out.println("OCR started – you can perform other tasks now...");
```

**Miért aszinkron:**  
Az OCR soros futtatása fájdalmasan lassú lehet – egy PNG akár egy másodpercet vagy többet is igényelhet. A feladat egy szálkezelő poolra delegálásával több CPU magot használsz ki, és drámaian csökkented a teljes futási időt.

## 4. lépés – Az eredmények lekérése, amikor készen állnak

Amikor készen állsz a kimenet felhasználására, egyszerűen hívd meg a `get()`‑et a `Future`‑on. Ez a hívás csak addig blokkol, amíg az OCR be nem fejeződik, majd egy `OcrResult` objektumok listáját adja vissza ugyanabban a sorrendben, mint a bemeneti lista.

```java
// Step 4: Wait for all results and retrieve them
List<OcrResult> ocrResults = ocrFuture.get(); // blocks until completion
```

**Időtúllépések kezelése:**  
Ha el akarod kerülni a végtelen blokkolást, használd a `ocrFuture.get(60, TimeUnit.SECONDS)`‑t, és kapj el egy `TimeoutException`‑t a visszalépés megvalósításához.

## 5. lépés – A felismert szöveg megjelenítése minden PNG-hez

Most, hogy megvannak az eredmények, iterálj rajtuk, és nyomtasd ki a kinyert szöveget az eredeti fájlnév mellett. Itt végre **szöveget nyersz ki PNG** fájlokból.

```java
// Step 5: Show the OCR output for each image
for (int i = 0; i < ocrResults.size(); i++) {
    System.out.println("File: " + imageFiles.get(i));
    System.out.println(ocrResults.get(i).getText());
    System.out.println("---");
}
```

**Várható kimeneti példa**

```
File: YOUR_DIRECTORY/page1.png
Invoice #12345
Date: 2024‑03‑01
Total: $1,250.00
---
File: YOUR_DIRECTORY/page2.png
...
```

Ha az OCR motor nem tud egy oldalt felismerni, a megfelelő `getText()` egy üres stringet ad vissza – mindenképpen ellenőrizd ezt a termelési kódban.

## Teljes működő példa

Az alábbiakban a teljes, azonnal futtatható program látható, amely minden részt összevon. Másold be egy `ParallelOcrDemo.java` nevű fájlba, cseréld le a `YOUR_DIRECTORY`‑t a PNG mappád elérési útjára, majd futtasd a `javac ParallelOcrDemo.java && java ParallelOcrDemo` parancsot.

```java
import com.aspose.ocr.*;
import java.util.*;
import java.util.concurrent.*;

public class ParallelOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Prepare a list of image files to be processed
        List<String> imageFiles = Arrays.asList(
                "YOUR_DIRECTORY/page1.png",
                "YOUR_DIRECTORY/page2.png",
                "YOUR_DIRECTORY/page3.png",
                "YOUR_DIRECTORY/page4.png");

        // Step 2: Create and configure the OCR engine (set language and enable spell‑checking)
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getEngineOptions()
                 .setLanguage(OcrLanguage.ENGLISH)
                 .setSpellCorrectionEnabled(true);

        // Step 3: Start asynchronous processing of the image batch
        Future<List<OcrResult>> ocrFuture = ocrEngine.processAsync(imageFiles);

        // (Optional) Perform other work here while OCR runs in the background...
        System.out.println("OCR processing started in background...");

        // Step 4: Wait for all results and retrieve them
        List<OcrResult> ocrResults = ocrFuture.get(); // blocks until completion

        // Step 5: Display the recognized text for each file
        for (int i = 0; i < ocrResults.size(); i++) {
            System.out.println("File: " + imageFiles.get(i));
            System.out.println(ocrResults.get(i).getText());
            System.out.println("---");
        }
    }
}
```

### A demó futtatása

1. **Fordítás** – `javac -cp "aspose-ocr.jar" ParallelOcrDemo.java`  
2. **Végrehajtás** – `java -cp ".:aspose-ocr.jar" ParallelOcrDemo`  

Minden PNG fájl neve után a kinyert szöveg jelenik meg, kötőjelek elválasztásával.  

> **Megjegyzés:** Ha `LicenseException`‑t kapsz, győződj meg róla, hogy a licenc betöltése megtörtént az engine létrehozása előtt:

```java
License lic = new License();
lic.setLicense("Aspose.OCR.Java.lic");
```

## Méretezés – Tippek a valós környezetben történő tömeges OCR-hez

| Helyzet | Ajánlás |
|-----------|----------------|
| **Százszáz PNG** | Növeld a szálkezelő pool méretét a `ocrEngine.setThreadPoolSize(8)`‑val (vagy nagyobbra, a CPU magok számának megfelelően). |
| **Memória korlátok** | Dolgozz kisebb csomagokban (pl. 50 fájlonként) és a `OcrResult` listát minden csomag után szabadítsd fel. |
| **Változó képminőség** | Engedélyezd a `setPreprocessingOptions`‑t, hogy automatikusan forgassa, kiegyenesítse vagy növelje a kontrasztot a felismerés előtt. |
| **Több nyelv** | Hívd meg a `setLanguage(OcrLanguage.ENGLISH, OcrLanguage.SPANISH)`‑t, és opcionálisan állíts be egy egyedi szótárat. |
| **Hibakezelés** | Tekerj be egy `try‑catch` blokkot a `ocrFuture.get()` köré `ExecutionException`‑re, hogy a hibás fájlokat naplózd anélkül, hogy a teljes köteg leállna. |

Ezek a stratégiák biztosítják, hogy a **tömeges képes OCR** csővezetéked robusztus maradjon, még akkor is, ha a bemeneti halmaz nő.

## Gyakran Ismételt Kérdések

**K: Működik ez JPEG vagy TIFF fájlokkal is?**  
V: Teljesen. A `processAsync` metódus bármely, az Aspose OCR által támogatott formátumot elfogad (PNG, JPEG, TIFF, BMP, stb.). Csak cseréld le a fájlkiterjesztéseket a listádban.

**K: Mit tehetek, ha meg kell őrizni a layoutot (táblázatok, oszlopok)?**  
V: Az Aspose OCR egy `getLayoutResult()` metódust biztosít, amely pozíciós adatokat ad vissza. A szavak körülhatároló dobozainak elemzésével újraépítheted a táblázatokat.

**K: Futtatható ez szerver nélküli platformon?**  
V: Igen – csomagold be a JAR‑t az Aspose könyvtárral, és telepítsd AWS Lambda, Azure Functions vagy Google Cloud Functions környezetbe. Ne feledd, hogy a funkció memóriáját elég magasra állítsd az OCR szálkezelő poolhoz.

## Következtetés

Most már rendelkezel egy teljes, önálló **tömeges képes OCR** megoldással, amely hatékonyan **szöveget nyer ki PNG** fájlokból az Aspose OCR aszinkron API-jának segítségével Java-ban. A tutorial lefedte a fájllista előkészítését, a nyelv és helyesírás‑javítás konfigurálását, a párhuzamos feldolgozás indítását, az eredmények kezelését és a pipeline méretezését éles környezetben.

Készen állsz a következő lépésre? Próbáld ki a nyelvet franciára cserélni, kísérletezz egyedi szótárakkal, vagy integráld a kimenetet egy kereshető ElasticSearch indexbe. A lehetőségek határtalanok, ha a gyors tömeges OCR‑t modern Java konkurenciával kombinálod.

Boldog kódolást, és legyen a szövegkinyerésed gyors és pontos! 

![Diagram, amely párhuzamos OCR munkavállalókat mutat több PNG fájl kezelésére](/images/batch-ocr-diagram.png){: .center alt="Tömeges képes OCR feldolgozási diagram"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}