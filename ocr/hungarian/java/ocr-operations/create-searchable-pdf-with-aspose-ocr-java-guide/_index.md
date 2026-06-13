---
category: general
date: 2026-03-26
description: Kereshető PDF létrehozása Aspose.OCR Java segítségével – tanulja meg,
  hogyan töltsön be képet OCR-rel, állítsa be az elsődleges nyelvet, nyerje ki a szöveget
  a képből, és mentse el OCR PDF-ként.
draft: false
keywords:
- create searchable pdf
- set primary language
- extract text from image
- load image ocr
- save ocr pdf
language: hu
og_description: Kereshető PDF létrehozása az Aspose.OCR Java segítségével. Lépésről‑lépésre
  útmutató a kép OCR betöltéséhez, az elsődleges nyelv beállításához, a szöveg kinyeréséhez
  a képből, és az OCR PDF mentéséhez.
og_title: Kereshető PDF létrehozása az Aspose.OCR-rel – Java útmutató
tags:
- Aspose.OCR
- Java
- PDF
- OCR
title: Kereshető PDF létrehozása az Aspose.OCR segítségével – Java útmutató
url: /hu/java/ocr-operations/create-searchable-pdf-with-aspose-ocr-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kereshető PDF létrehozása Aspose.OCR-rel – Java útmutató

Valaha szükséged volt **create searchable pdf** létrehozására egy beolvasott dokumentumból, de nem tudtad, hol kezdjed? Nem vagy egyedül – sok fejlesztő szembesül ezzel a problémával, amikor először foglalkozik az OCR-rel Java-ban. A jó hír, hogy az Aspose.OCR leegyszerűsíti az egész folyamatot – a kép betöltésétől a fő nyelv beállításáig, egészen egy OCR‑támogatott PDF mentéséig – meglehetősen könnyűvé teszi. Ebben az útmutatóban egy teljes, futtatható példán keresztül vezetünk végig, amely **extracts text from image**, lehetővé teszi a **set primary language** beállítását, és egy **save OCR pdf**-vel zárul, amelyet bármely olvasóval megnyithatsz.

A továbbiakban néhány gyakorlati tippet is bemutatunk, például a GPU gyorsítás engedélyezését a gyorsabb feldolgozás érdekében, valamint a vegyes nyelvű dokumentumok kezelését (Tamil + English a mi esetünkben). A végére egy stabil, termelés‑kész kódrészletet kapsz, amelyet beilleszthetsz a projektedbe.

## Amire szükséged lesz

- **Java 17** (vagy bármely friss JDK; az Aspose.OCR támogatja a Java 8+ verziókat)
- **Aspose.OCR for Java** könyvtár (töltsd le a hivatalos oldalról vagy add hozzá Maven‑en keresztül)
- **license file** (vagy a 30‑napos próba)
- Egy képfájl, amely szöveget tartalmaz (a demó a `sample-mixed-tamil-eng.jpg` fájlt használja)

Nincs szükség extra keretrendszerekre, natív függőségekre – csak tiszta Java és az Aspose.JAR-ok.

---

## 1. lépés: Kereshető PDF létrehozása – A projekt beállítása

Mielőtt belemerülnénk a kódba, győződjünk meg róla, hogy a projekt készen áll **create searchable pdf** fájlok létrehozására.

```bash
# Maven dependency (add to pom.xml)
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- check the latest version -->
</dependency>
```

> **Pro tip:** Tartsd naprakészen a verziószámot; az újabb kiadások gyakran tartalmaznak teljesítményjavításokat a GPU használatához.

Most hozz létre egy egyszerű Java osztályt `RecentFeaturesDemo` néven. Az osztály tartalmazni fogja az összes logikát, amelyre szükségünk van a **load image OCR** betöltéséhez, a nyelvi beállítások konfigurálásához, és végül a **save OCR pdf** mentéséhez.

## 2. lépés: **load image OCR** betöltése és a motor inicializálása

Az első tényleges lépés a folyamatban a **load image OCR**. Ez jelzi az Aspose.OCR számára, melyik fájlt kell elemezni.

```java
import com.aspose.ocr.*;

public class RecentFeaturesDemo {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Load your Aspose.OCR license (or use the 30‑day trial)
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.Java.lic");

        // 2️⃣ Create and configure the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Enable GPU acceleration – speeds up recognition dramatically
        ocrEngine.getEngineSettings().setUseGpu(true);
        // Use all available CPU cores for parallel processing
        ocrEngine.getEngineSettings().setUseParallelProcessing(true);
```

> **Why this matters:** A GPU engedélyezése (`setUseGpu(true)`) akár 70 %-kal is csökkentheti a feldolgozási időt a modern hardveren, míg a párhuzamos feldolgozás biztosítja, hogy a CPU ne legyen tétlen, amikor a GPU dolgozik.

## 3. lépés: Fő nyelv beállítása (és egy másodlagos)

Ha kihagyod ezt a lépést, az Aspose.OCR megpróbálja kitalálni a nyelvet, ami lassabb és kevésbé pontos. Íme, hogyan állíthatod be a **set primary language**-t tamilra, és adhatod hozzá az angolt tartalék nyelvként.

```java
        // 3️⃣ Define languages – primary is Tamil, secondary is English
        ocrEngine.getLanguageSettings().setLanguage(Language.Tamil);
        ocrEngine.getLanguageSettings().setSecondaryLanguage(Language.English);
```

> **Explanation:** A fő nyelv befolyásolja a felismert karakterkészletet és szótárat. Másodlagos nyelv hozzáadása kulcsfontosságú a vegyes írásrendszerű dokumentumoknál (gondolj egy nyugtára, amely tamil és angol szöveget is tartalmaz).  
> **Edge case:** Ha a dokumentum több mint két nyelvet tartalmaz, minden további nyelvhez meghívhatod a `addAdditionalLanguage(...)` metódust.

## 4. lépés: Kép előfeldolgozása – Egyenesítés és zajcsökkentés

A beolvasott képek gyakran szenvednek elforgatástól vagy háttérzajtól. Az előfeldolgozás segít az OCR motor **extract text from image** megbízhatóbban.

```java
        // 4️⃣ Pre‑processing options
        ocrEngine.getPreprocessingSettings()
                 .setDeskew(true)   // auto‑rotate tilted pages
                 .setDenoise(true); // suppress speckles and background patterns
```

> **Tip:** Ha tudod, hogy a kép már tiszta, kihagyhatod a `setDenoise(true)` hívást, hogy néhány ezredmásodpercet spórolj.

## 5. lépés: Kép fájl betöltése

Most, hogy a motor készen áll, megadjuk neki a fájlt, amelyet elemezni szeretnénk.

```java
        // 5️⃣ Load the image you want to recognize
        String imagePath = "YOUR_DIRECTORY/sample-mixed-tamil-eng.jpg";
        ocrEngine.setImage(ImageStream.fromFile(imagePath));
```

> **What if the path is wrong?** Az Aspose.OCR egy egyértelmű `FileNotFoundException`-t dob. Tedd a hívást try‑catch blokkba, ha kifinomult hibakezelésre van szükséged.

## 6. lépés: OCR futtatása és szöveg kinyerése a képből

Miután minden be van állítva, itt az ideje ténylegesen futtatni a felismerést. Ez a lépés **extracts text from image** és előkészíti a PDF létrehozásához szükséges adatokat.

```java
        // 6️⃣ Perform recognition
        if (ocrEngine.recognize()) {
            String recognizedText = ocrEngine.getText();

            // Print the raw OCR output – handy for debugging
            System.out.println("Recognized text:");
            System.out.println(recognizedText);
```

A demó kép tipikus konzol kimenete a következőképpen néz ki:

```
வணக்கம் World
This is a mixed language sample.
```

Észre fogod venni, hogy a tamil sor helyesen jelenik meg, majd az angol. Ez a **set primary language** helyes beállításának eredménye.

## 7. lépés: OCR PDF mentése – Az utolsó darab

A rejtvény utolsó darabja a **save OCR pdf**. Az Aspose.OCR képes egy láthatatlan szövegréteget beágyazni az eredeti kép fölé, így a PDF kereshető lesz.

```java
            // 7️⃣ (Optional) Save a searchable PDF with an OCR layer
            String pdfPath = "YOUR_DIRECTORY/searchable.pdf";
            ocrEngine.save(pdfPath, SaveFormat.PdfSearchable);

            System.out.println("\nSearchable PDF saved to: " + pdfPath);
        } else {
            System.err.println("Recognition failed: " + ocrEngine.getErrorMessage());
        }
    }
}
```

Nyisd meg a `searchable.pdf`-et az Adobe Readerben, nyomd meg a **Ctrl + F**-et, és kereshetsz mind tamil, mind angol szavakra – pontosan azt, amit egy **create searchable pdf** munkafolyamat ígér.

## Teljes működő példa (másolás‑beillesztés)

Az alábbiakban a teljes program található, amelyet úgy fordíthatsz és futtathatsz, ahogy van. Cseréld ki a helyőrző útvonalakat a saját könyvtáraidra.

```java
import com.aspose.ocr.*;

public class RecentFeaturesDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Load your Aspose.OCR license (or use the 30‑day trial)
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.Java.lic");

        // Step 2: Create and configure the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getEngineSettings().setUseGpu(true);                     // enable CUDA GPU acceleration
        ocrEngine.getEngineSettings().setUseParallelProcessing(true);     // use multiple CPU cores
        ocrEngine.getLanguageSettings().setLanguage(Language.Tamil);      // primary language
        ocrEngine.getLanguageSettings().setSecondaryLanguage(Language.English); // secondary language
        ocrEngine.getPreprocessingSettings()
                 .setDeskew(true)   // correct image rotation
                 .setDenoise(true); // reduce background noise

        // Step 3: Load the image you want to recognize
        String imagePath = "YOUR_DIRECTORY/sample-mixed-tamil-eng.jpg";
        ocrEngine.setImage(ImageStream.fromFile(imagePath));

        // Step 4: Run OCR and obtain the plain‑text result
        if (ocrEngine.recognize()) {
            String recognizedText = ocrEngine.getText();

            // Step 5: (Optional) Save a searchable PDF with an OCR layer
            String pdfPath = "YOUR_DIRECTORY/searchable.pdf";
            ocrEngine.save(pdfPath, SaveFormat.PdfSearchable);

            System.out.println("Recognized text:");
            System.out.println(recognizedText);
            System.out.println("\nSearchable PDF saved to: " + pdfPath);
        } else {
            System.err.println("Recognition failed: " + ocrEngine.getErrorMessage());
        }
    }
}
```

Futtasd a következővel:

```bash
javac -cp "path/to/aspose-ocr.jar" RecentFeaturesDemo.java
java -cp ".:path/to/aspose-ocr.jar" RecentFeaturesDemo
```

A konzolon meg kell jelennie a kinyert szövegnek, majd egy megerősítésnek, hogy a **searchable pdf** a lemezre íródott.

## Gyakori kérdések és edge case-ek

### Mi van, ha **load image OCR**-t kell byte tömbből betölteni?

A `ImageStream.fromFile(imagePath)` helyett használhatod a `ImageStream.fromBytes(byteArray)`-t. Ez akkor hasznos, ha a kép egy adatbázisból vagy egy webszolgáltatásból érkezik.

### Hogyan kezeljem azokat a PDF-eket, amelyek már tartalmaznak képeket?

Az Aspose.OCR közvetlenül dolgozhat PDF oldalakon: `ocrEngine.setDocument(PdfDocument.fromFile("input.pdf"))`. A motor minden oldalt belsőleg rasterizál a felismerés előtt.

### A GPU-m nem kerül észlelésre – hagyjam meg a `setUseGpu(true)`-t?

Ha a `setUseGpu(true)` sikertelen, az Aspose.OCR automatikusan visszatér a CPU-hoz. Engedélyezés előtt ellenőrizheted a `ocrEngine.getEngineSettings().isGpuAvailable()` értéket.

### Menthetek **save OCR pdf**-t egyedi metaadatokkal?

Igen. Felismerés után használd a `ocrEngine.getPdfSaveOptions().setTitle("My Document")` vagy a `setAuthor("John Doe")` metódust, mielőtt meghívnád a `save`-et.

## Teljesítmény tippek nagy köteghez

- **Batch processing:** Használd újra ugyanazt a `OcrEngine` példányt több kép esetén. Csak a futások között hívd meg a `ocrEngine.clear()`-t.
- **Thread pool:** Csomagolj minden képfeladatot egy `Callable`-ba, és add át egy `ExecutorService`-nek. Mivel engedélyeztük a párhuzamos feldolgozást, minden szál profitál a többmagos használatból.
- **Memory management:** Gigapixel képek esetén fontold meg a lecsökkentést a `ocrEngine.getPreprocessingSettings().setResizeFactor(0.5)` használatával, hogy a RAM használat ésszerű maradjon.

## Összegzés

Épp most jártuk végig a teljes **create searchable pdf** munkafolyamatot az Aspose.OCR for Java használatával. A **load image OCR**-től kezdve mi...

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}