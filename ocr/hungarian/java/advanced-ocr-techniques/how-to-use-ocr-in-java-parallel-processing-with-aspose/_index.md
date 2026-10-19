---
category: general
date: 2026-02-27
description: Tanulja meg, hogyan használja az OCR-t Java-ban a TIFF és PDF fájlok
  képszövegének kinyeréséhez az Aspose OCR párhuzamos feldolgozásával. Gyors, egyszerű
  útmutató.
draft: false
keywords:
- how to use ocr
- perform ocr on pdf
- extract text from tiff
- extract image text java
language: hu
og_description: Tanulja meg, hogyan használja az OCR-t Java-ban a képszöveg kinyeréséhez
  TIFF és PDF fájlokból az Aspose OCR párhuzamos feldolgozásával.
og_title: Hogyan használjunk OCR-t Java-ban – Párhuzamos feldolgozás az Aspose-szal
tags:
- OCR
- Java
- Aspose
title: Hogyan használjunk OCR-t Java-ban – párhuzamos feldolgozás az Aspose-szal
url: /hu/java/advanced-ocr-techniques/how-to-use-ocr-in-java-parallel-processing-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan használjunk OCR-t Java-ban – Párhuzamos feldolgozás az Aspose-szal

Gondolkodtál már azon, **hogyan használjunk OCR-t**, hogy szöveget nyerjünk ki egy beolvasott dokumentumból anélkül, hogy izzadnál? Nem vagy egyedül. A fejlesztők gyakran ütköznek akadályba, amikor képekből – különösen TIFF‑ekből és PDF‑ekből – kell szöveget olvasniuk, miközben a teljesítményt is szem előtt tartják.  

Ebben az útmutatóban egy teljes, azonnal futtatható megoldást mutatunk be, amely **kivonja a képek szövegét Java-ban** az Aspose OCR segítségével, bekapcsolja a párhuzamos feldolgozást, és még a szálak számát is korlátozhatod. A végére egyetlen osztályod lesz, amely **PDF‑eken OCR‑t végez**, és **TIFF képekből szöveget nyer ki** egy töredéknyi idő alatt, mint egy egy‑szálas megközelítés.

> **Mit fogsz megtanulni**  
> * Egyértelmű magyarázat arról, hogy miért fontos a párhuzamos OCR.  
> * Egy teljes Java program (hiányzó importok nélkül).  
> * Tippek a szálhasználat finomhangolásához és a gyakori buktatók kezeléséhez.  

## Előfeltételek

- Java 8 vagy újabb (a kód JDK 11‑kel is lefordítható).  
- Aspose.OCR for Java könyvtár – a legújabb JAR‑t a Maven Central‑ról szerezheted be (`com.aspose:aspose-ocr`).  
- Egy képfájl (`.tif`, `.tiff`) vagy egy PDF, amelyet feldolgozni szeretnél.  
- Mérsékelt mennyiségű RAM – a párhuzamos feldolgozás néhány szálat indít, de az Aspose memória‑hatékony.

Ha ezek megvannak, merüljünk el.

![Diagram showing the OCR pipeline – how to use OCR in Java with parallel processing](how-to-use-ocr-pipeline.png)

*Image alt text: hogyan használjunk OCR példadiagram*

---

## 1. lépés: Projekt beállítása és Aspose OCR hozzáadása

### Miért fontos

Mielőtt **PDF‑en OCR‑t végeznél** vagy bármilyen képen, a könyvtárnak a classpath‑on kell lennie. Nélküle a fordító `ClassNotFoundException`‑t dob, és a második lépésnél elakadsz.

### Hogyan csináljuk

Ha Maven‑t használsz, add hozzá a függőséget:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- check for the newest version -->
</dependency>
```

Gradle esetén:

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

> **Pro tipp:** Tartsd a verziószámot szinkronban az Aspose kiadási megjegyzésekkel; az újabb verziók gyakran tartalmaznak teljesítményjavításokat a párhuzamos feldolgozáshoz.

---

## 2. lépés: OCR motor létrehozása és párhuzamos feldolgozás engedélyezése

### Miért fontos

Alapértelmezés szerint az Aspose OCR egyetlen szálon fut. Ha egy többoldalas PDF‑et vagy egy TIFF‑készletet adsz neki, a motor minden oldalt egymás után dolgoz fel – lassú és hatékonytalan. A párhuzamos feldolgozás lehetővé teszi, hogy a CPU egyszerre több oldalt is dolgozzon fel, ezzel drámaian lerövidítve a futási időt.

### Kód

```java
import com.aspose.ocr.*;

public class ParallelOcrDemo {

    public static void main(String[] args) throws Exception {
        // 1️⃣ Path to the input file (TIFF or PDF)
        String inputPath = "YOUR_DIRECTORY/input.tif";

        // 2️⃣ Instantiate the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 3️⃣ Turn on parallel processing – this is the core of how to use OCR efficiently
        ocrEngine.getConfig().setUseParallelProcessing(true);

        // 4️⃣ (Optional) Limit threads – you can cap it to the number of cores you have
        // ocrEngine.getConfig().setMaxThreads(Runtime.getRuntime().availableProcessors());

        // 5️⃣ Run OCR
        OcrResult ocrResult = ocrEngine.processImage(inputPath);

        // 6️⃣ Output the recognised text
        System.out.println(ocrResult.getText());
    }
}
```

**A kulcsfontosságú sorok magyarázata**

- `setUseParallelProcessing(true)`: azt mondja az Aspose‑nak, hogy ossza szét a munkát a rendelkezésre álló CPU‑magok között.  
- `setMaxThreads(...)`: korlátozhatod a szálkészletet, ha megosztott szerveren vagy, vagy szeretnél helyet hagyni más szolgáltatásoknak.  
- `processImage(inputPath)`: mind képfájlokra, mind PDF‑dokumentumokra működik, így ugyanazzal a hívással **PDF‑en OCR‑t végez** és TIFF‑en is.

---

## 3. lépés: Különböző bemeneti típusok kezelése – PDF vs. TIFF

### Miért fontos

Bár a `processImage` egy útvonal‑stringet fogad, a háttérben a kezelés eltérő. A PDF‑ek gyakran több oldalt tartalmaznak, amelyek mindegyike külön OCR‑feladat lesz. A TIFF‑ek lehetnek egy‑ vagy többoldalasak; az Aspose minden keretet oldalként kezel.

### Mire figyelj

| Bemenet | Tipikus buktató | Ajánlott megoldás |
|---------|------------------|-------------------|
| PDF | Nagy PDF‑ek memória‑kimerülést okozhatnak, ha egyszerre minden oldalt betölti. | Használd a `ocrEngine.getConfig().setMemoryOptimization(true);` beállítást (újabb kiadásokban elérhető). |
| Többoldalas TIFF | Egyes régi TIFF‑ek nem támogatott tömörítést használnak. | Konvertáld egy támogatott formátumba, vagy használd az Aspose `TiffImage` segédeszközét. |

Az alábbi gyors kódrészlet megmutatja, hogyan detektáld a fájltípust és írj barátságos naplóbejegyzést:

```java
import java.nio.file.*;

String ext = Files.probeContentType(Paths.get(inputPath)).toLowerCase();
if (ext.contains("pdf")) {
    System.out.println("Processing a PDF – expect multiple pages.");
} else if (ext.contains("tiff") || ext.contains("tif")) {
    System.out.println("Processing a TIFF image.");
} else {
    System.out.println("Unsupported file type. This demo works with PDF and TIFF.");
}
```

---

## 4. lépés: Kimenet ellenőrzése – Mit kell látnod?

Amikor a program befejeződik, a nyers kinyert szöveget a konzolra írja. Egy egyszerű beolvasott számla esetén a kimenet például így nézhet ki:

```
Invoice #12345
Date: 02/15/2026
Total Amount: $1,250.00
Thank you for your business!
```

Ha az OCR egy adott oldalon nehézségekbe ütközik, az Aspose egy helyőrző sort szúr be, például `[Unrecognizable]`. Ezeket később kiszűrheted, ha tiszta adatot szeretnél.

**Gyors ellenőrzés**

```java
if (ocrResult.getText().trim().isEmpty()) {
    System.err.println("No text detected – verify the image quality or try a different language.");
}
```

---

## 5. lépés: Teljesítmény finomhangolása – Mikor módosítsd a szálak számát?

### Miért fontos

Több szál nem mindig jelent gyorsabb eredményt. Egy 4‑magos laptopon 8 szál indítása kontextus‑váltási többletet okozhat. Ezzel szemben egy 32‑magos szerveren érdemes a teljes kapacitást kiaknázni.

### Hogyan találd meg az optimális beállítást

```java
int cores = Runtime.getRuntime().availableProcessors();
System.out.println("Available processors: " + cores);

// Experiment: set max threads to half the cores first
ocrEngine.getConfig().setMaxThreads(Math.max(1, cores / 2));
```

Futtasd a programot különböző beállításokkal és mérd az időt:

```java
long start = System.nanoTime();
ocrEngine.processImage(inputPath);
long elapsed = System.nanoTime() - start;
System.out.println("Elapsed time (ms): " + elapsed / 1_000_000);
```

Rögzítsd az eredményeket, válaszd ki a legjobb áteresztőképességet biztosító konfigurációt, és rögzítsd a termelésben.

---

## 6. lépés: A bemutató kiterjesztése – Több fájl kötegelt feldolgozása

Ha egy egész mappából szeretnél **kép szöveget Java‑ban kinyerni**, csomagold be a főlogikát egy ciklusba:

```java
Path folder = Paths.get("YOUR_DIRECTORY");
try (DirectoryStream<Path> stream = Files.newDirectoryStream(folder, "*.{tif,tiff,pdf}")) {
    for (Path file : stream) {
        System.out.println("\n--- Processing: " + file.getFileName() + " ---");
        OcrResult result = ocrEngine.processImage(file.toString());
        // Save or further process result.getText()
    }
}
```

Ez a minta jól skálázódik, mivel a motor már a fájl egyes oldalait párhuzamosan dolgozza fel. A külső ciklus sorban fut, de akár minden fájlt egy `ExecutorService`‑nek is átadhatsz, ha egy hatalmas CPU‑farmot szeretnél telítetni.

---

## Gyakori buktatók és elkerülésük módja

| Tünet | Valószínű ok | Megoldás |
|-------|--------------|----------|
| `OutOfMemoryError` | Túl sok oldal betöltése egyszerre (különösen hatalmas PDF‑eknél). | Engedélyezd a memóriaoptimalizálást (`setMemoryOptimization(true)`) vagy dolgozd fel a PDF‑et oldalanként a `processPage`‑el. |
| Torz karakterek | Hibás nyelv/karakterkészlet beállítás. | Hívd meg a `ocrEngine.getConfig().setLanguage(OcrLanguage.English);`‑t vagy a megfelelő nyelvi enumot. |
| Lassú teljesítmény a párhuzamos jelző ellenére | Az OS korlátozza a szálak létrehozását vagy a JVM alacsony heap mérettel fut. | Növeld a `-Xmx` heap flag‑et, és ellenőrizd az OS szálkorlátait (`ulimit -u`). |
| Üres kimenet | Bemeneti kép felbontása < 300 dpi. | Növeld fel a képet OCR előtt, vagy használj nagyobb felbontású szkennert. |

---

## Összefoglalás – Mit tanultunk

- **Hogyan használjunk OCR‑t** Java‑ban az Aspose `OcrEngine`‑jével.  
- A **párhuzamos feldolgozás** engedélyezése a **PDF‑en OCR‑hoz** és a **TIFF‑ről szöveg kinyeréséhez**.  
- A szálak számának finomhangolása az optimális teljesítményért.  
- Edge‑case‑ek kezelése, mint a nagy PDF‑ek, többoldalas TIFF‑ek és nyelvi beállítások.  
- A egyfájlos demó kiterjesztése kötegelt feldolgozásra a valós környezetben.

---

## Következő lépések

Most, hogy az alapokat elsajátítottad, érdemes ezeket a kapcsolódó témákat is felfedezni:

- **Kép szöveg Java‑ban** kézzel írott jegyzetekből (kapcsold be a `setHandwritingRecognition(true)`‑t).  
- Az OCR kimenet integrálása az Apache Tika‑val a metaadat‑kinyeréshez.  
- Az eredmények tárolása Elasticsearch‑ben kereshető dokumentumarchívumokhoz.  
- Az Aspose OCR használata más nyelveken, például Python vagy .NET – az elvek ugyanazok.

Nyugodtan kísérletezz különböző szálkorlátokkal, képformátumokkal és nyelvi csomagokkal. Minél többet játszol vele, annál jobban megérted a sebesség és pontosság közötti kompromisszumokat.

---

### Boldog kódolást!

Ha elakadsz, vagy ötleted van a további optimalizálásra, írj egy megjegyzést lent. Mindig szívesen beszélgetek OCR trükkökről – semmi izzadság, csak kód.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}