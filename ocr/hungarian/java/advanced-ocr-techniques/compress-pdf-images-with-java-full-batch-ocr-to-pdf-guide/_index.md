---
category: general
date: 2026-07-05
description: Tömörítsd a PDF képeket a PNG PDF-re konvertálása közben Java-val. Ismerd
  meg a képelőfeldolgozást OCR-hez, a szöveg felismerését JPG-ből, és a kötegelt OCR-t
  PDF-be egyetlen útmutatóban.
draft: false
keywords:
- compress pdf images
- convert png to pdf
- image preprocessing for ocr
- recognize text jpg
- batch ocr to pdf
language: hu
og_description: Tömörítse a PDF képeket, és konvertálja a PNG-t PDF-be Java használatával.
  Ez az útmutató a képek előfeldolgozását OCR-hez, a JPG szövegfelismerést és a kötegelt
  OCR-t PDF-be tárgyalja.
og_title: PDF képek tömörítése Java-val – Teljes kötegelt OCR útmutató
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Compress PDF images while converting PNG to PDF using Java. Learn image
    preprocessing for OCR, recognize text JPG, and batch OCR to PDF in one tutorial.
  headline: Compress PDF Images with Java – Full Batch OCR to PDF Guide
  type: TechArticle
- description: Compress PDF images while converting PNG to PDF using Java. Learn image
    preprocessing for OCR, recognize text JPG, and batch OCR to PDF in one tutorial.
  name: Compress PDF Images with Java – Full Batch OCR to PDF Guide
  steps:
  - name: Expected Output
    text: 'Running the program prints a line for each image, e.g.:'
  - name: What if my server has no GPU?
    text: Just set `gpuSettings.setEnabled(false)`. The rest of the pipeline remains
      unchanged, and you still get multithreaded CPU processing.
  - name: My PDFs are still too large—can I lower the quality further?
    text: Yes. Adjust `options.setImageQuality(70)` or even `50`. Lower values shrink
      size more aggressively but may blur fine glyphs. Test with a representative
      sample.
  - name: How do I handle other image formats (TIFF, BMP)?
    text: 'Add the extensions to the filter lambda:'
  - name: Can I keep the original color images instead of binarizing?
    text: Replace `.addBinarize()` with `.addGrayscale()` in the preprocessor builder
      if you need color retention for downstream analysis.
  type: HowTo
tags:
- ocr
- java
- pdf
- image-processing
title: PDF képek tömörítése Java-val – Teljes kötegelt OCR PDF-hez útmutató
url: /hu/java/advanced-ocr-techniques/compress-pdf-images-with-java-full-batch-ocr-to-pdf-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF képek tömörítése Java-val – Teljes kötegelt OCR PDF útmutató

Valaha szükséged volt **PDF képek tömörítésére**, miközben egy PNG mappát kereshető PDF-ekké alakítod? Nem vagy egyedül. Sok automatizálási folyamatban a legnagyobb gond az, hogy egyszerre kell egyensúlyozni a képminőséget, az OCR pontosságát és a végső PDF méretét.

Ebben az útmutatóban egy gyakorlati megoldáson vezetünk végig, amely **PNG‑t PDF‑re konvertál**, **képelőfeldolgozást alkalmaz OCR-hez**, és végül **PDF képeket tömörít**, hogy a kimenet könnyű maradjon. A végére tudni fogod, hogyan **szöveget ismerj fel JPG** fájlokban, hogyan állíts be egy **kötegelt OCR PDF‑hez** munkafolyamatot, és hogyan tartsd rendezettnek a PDF-eket.

## Mit fogsz megtanulni

- Aspose OCR for Java beállítása és licenc alkalmazása.  
- A motor konfigurálása több szálra, GPU gyorsításra és helyesírási javításra.  
- Újrahasználható **képelőfeldolgozási pipeline OCR-hez** (zajszűrés, kontraszt, binarizálás) felépítése.  
- **PdfSaveOptions** használata **PDF képek tömörítéséhez** az olvashatóság feláldozása nélkül.  
- Könyvtár bejárása **PNG‑t PDF‑re konvertáláshoz** és **szöveg felismerés JPG** tömegesen.  
- Egy teljes, azonnal futtatható Java program, amelyet bármely projektbe beilleszthetsz.

> **Előfeltételek**: Java 8+, Maven vagy Gradle, egy Aspose OCR for Java licenc, és egy PNG/JPG képeket tartalmazó mappa, amelyet feldolgozni szeretnél.

## 1. lépés: Aspose OCR licenc alkalmazása (elengedhetetlen a termeléshez)

Mielőtt bármely OCR API-t meghívnád, be kell töltened egy érvényes licencet; különben a próbaverzió korlátaival leszel korlátozva.

```java
import com.aspose.ocr.*;

public class LicenseSetup {
    public static void loadLicense() throws Exception {
        License license = new License();
        // Point to your license file – keep it out of source control!
        license.setLicense("Aspose.OCR.Java.lic");
    }
}
```

*Miért fontos*: Egy licencelt motor engedélyezi a GPU támogatást, magasabb pontosságot, és eltávolítja a vízjeleket, amelyek egyébként megnövelnék a PDF fájljaid méretét.

## 2. lépés: OCR motor konfigurálása – szálak, GPU és helyesírási javítás

Egy gyors OCR motor a **kötegelt OCR PDF‑hez** feladatok gerince. Annyi szálat indítunk, amennyit a gazda CPU képes kezelni, engedélyezzük a GPU gyorsítást (ha van kompatibilis kártyád), és szigorúbbá tesszük a helyesírási javítást az OCR hibák tisztításához.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.gpu.GPUSettings;
import com.aspose.ocr.spell.SpellCorrectionOptions;

public class EngineConfig {
    public static OcrEngine createEngine() {
        OcrEngine ocrEngine = new OcrEngine();

        // Use all available logical processors
        ocrEngine.setThreadCount(Runtime.getRuntime().availableProcessors());

        // Enable GPU – huge speedup for large batches
        GPUSettings gpu = new GPUSettings();
        gpu.setEnabled(true);
        ocrEngine.setGpuSettings(gpu);

        // Light spell correction: fix common typos without over‑correcting
        SpellCorrectionOptions spellOpts = new SpellCorrectionOptions();
        spellOpts.setMaxEditDistance(1);
        ocrEngine.getSpellCorrection().setOptions(spellOpts);

        return ocrEngine;
    }
}
```

*Pro tipp*: Ha egy grafikus felület nélküli szerveren futsz GPU nélkül, egyszerűen állítsd be a `gpu.setEnabled(false)` értéket – a kód továbbra is működik, csak egy kicsit lassabban.

## 3. lépés: Képelőfeldolgozási pipeline felépítése

A nyers szkennelések gyakran zajt, alacsony kontrasztot vagy egyenetlen megvilágítást mutatnak. **Képelőfeldolgozás OCR-hez** drámaian javítja a felismerési arányt, különösen **szöveg felismerés JPG** esetekben.

```java
import com.aspose.ocr.*;

public class PreprocessorSetup {
    public static ImagePreprocessor createPreprocessor() {
        return new ImagePreprocessor.Builder()
                .addDenoise(0.7)      // Reduce grain while preserving edges
                .addContrast(1.15)    // Boost contrast for clearer glyphs
                .addBinarize()        // Convert to black‑and‑white for OCR
                .build();
    }
}
```

*Miért láncoljuk ezeket*: Először a zajszűrés megakadályozza, hogy a binarizáló felerősítse a foltokat; a kontraszt ezután biztosítja, hogy a karakterek kiemelkedjenek; végül a binarizálás tiszta bináris képet ad az OCR motor számára.

## 4. lépés: PDF mentési beállítások előkészítése – **PDF képek hatékony tömörítése**

Az Aspose lehetővé teszi a PDF kimenet finomhangolását. Bekapcsoljuk a képtömörítést, és beállítunk egy minőségi szintet, amely egyensúlyt teremt a méret és az olvashatóság között.

```java
import com.aspose.ocr.pdf.PdfSaveOptions;

public class PdfOptions {
    public static PdfSaveOptions createOptions() {
        PdfSaveOptions options = new PdfSaveOptions();
        options.setCompressImages(true);   // This is the key to compress PDF images
        options.setImageQuality(90);       // 90% retains sharp text while shrinking file size
        return options;
    }
}
```

*Eredmény*: Minden kereshető PDF észrevehetően kisebb lesz – ideális archiváláshoz vagy e‑mailben történő küldéshez.

## 5. lépés: Mappa feldolgozása – **PNG‑t PDF‑re konvertálás** és **szöveg felismerés JPG** egyetlen ciklusban

Most mindent összehozzuk. A ciklus bejár egy bemeneti könyvtárat, OCR-t futtat minden PNG vagy JPG fájlon, és egy kereshető PDF-et ír ki egy kimeneti mappába. A PDF neve tükrözi a forráskép nevét.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.pdf.PdfSaveOptions;
import java.io.File;

public class BatchOcrTutorial {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load license
        LicenseSetup.loadLicense();

        // 2️⃣ Engine & preprocessing
        OcrEngine ocrEngine = EngineConfig.createEngine();
        ocrEngine.setPreprocessor(PreprocessorSetup.createPreprocessor());

        // 3️⃣ PDF options (compress PDF images)
        PdfSaveOptions pdfOptions = PdfOptions.createOptions();

        // 4️⃣ Define input / output folders
        File inputFolder = new File("YOUR_DIRECTORY/input");
        File outputFolder = new File("YOUR_DIRECTORY/output");
        if (!outputFolder.exists()) outputFolder.mkdirs();

        // 5️⃣ Filter PNG & JPG files
        File[] imageFiles = inputFolder.listFiles((dir, name) ->
                name.toLowerCase().endsWith(".png") || name.toLowerCase().endsWith(".jpg"));

        if (imageFiles == null || imageFiles.length == 0) {
            System.out.println("No PNG or JPG files found in the input folder.");
            return;
        }

        // 6️⃣ Process each file
        for (File image : imageFiles) {
            // Recognize text – works for both PNG and JPG
            ocrEngine.recognizeImage(image.getAbsolutePath());

            // Build output PDF path (same base name)
            String pdfPath = outputFolder.getAbsolutePath() + File.separator +
                    image.getName().replaceAll("\\.(png|jpg)$", ".pdf");

            // Save as searchable PDF – this step also compresses images
            ocrEngine.saveAsSearchablePdf(pdfPath, pdfOptions);

            System.out.println("✅ Processed: " + image.getName() + " → " + pdfPath);
        }

        System.out.println("🎉 All files have been converted and compressed!");
    }
}
```

### Várt kimenet

A program futtatása minden képre egy sort nyomtat, például:

```
✅ Processed: invoice1.png → /output/invoice1.pdf
✅ Processed: receipt23.jpg → /output/receipt23.pdf
🎉 All files have been converted and compressed!
```

Nyiss meg bármely eredmény PDF-et egy megjelenítőben, és láthatod a kijelölhető, kereshető szöveget, miközben a fájlméret általában **30‑50 % kisebb** egy nem tömörített változatnál.

## Gyakori kérdések és szélhelyzetek

### Mi van, ha a szerveremnek nincs GPU-ja?

Csak állítsd be a `gpuSettings.setEnabled(false)` értéket. A pipeline többi része változatlan marad, és továbbra is több szálas CPU feldolgozást kapsz.

### A PDF-jeim még mindig túl nagyok – csökkenthetem még a minőséget?

Igen. Állítsd be a `options.setImageQuality(70)` vagy akár `50` értéket. Az alacsonyabb értékek agresszívebben csökkentik a méretet, de elmoshatják a finom karaktereket. Tesztelj egy reprezentatív mintával.

### Hogyan kezeljem a többi képfájltípust (TIFF, BMP)?

Add the extensions to the filter lambda:

```java
name.toLowerCase().endsWith(".png") ||
name.toLowerCase().endsWith(".jpg") ||
name.toLowerCase().endsWith(".tif") ||
name.toLowerCase().endsWith(".bmp")
```

### Megtarthatom az eredeti színes képeket a binarizálás helyett?

Cseréld le a `.addBinarize()`-t `.addGrayscale()`-re a preprocessor builderben, ha színmegőrzésre van szükséged a további elemzéshez.

## Profi tippek a termelés‑kész kötegelt OCR-hez

- **Memóriakezelés**: Használj egyetlen `OcrEngine` példányt (ahogy látható), hogy elkerüld az objektumok képenkénti létrehozásának/megsemmisítésének terheit.  
- **Hibakezelés**: Tedd a fájlonkénti blokkot `try/catch`-be, hogy naplózd a hibákat anélkül, hogy a teljes köteget megszakítanád.  
- **Naplózás**: Használj megfelelő naplózási keretrendszert (SLF4J, Log4j) a `System.out.println` helyett a skálázható megoldásokhoz.  
- **Párhuzamosság**: Nagy mappák esetén fontold meg az alkönyvtárak párhuzamos stream‑ekkel való feldolgozását, de figyelj a GPU versengésre.  
- **Biztonság**: Tárold a licencfájlt a tárolón kívül, és védd fájlrendszer jogosultságokkal.

## Következtetés

Most bemutattuk, hogyan **tömöríthetőek a PDF képek** egy **kötegelt OCR PDF‑hez** konverzió során, amely **PNG‑t PDF‑re konvertál**, **szöveget felismer JPG** fájlokban, és egy robusztus **képelőfeldolgozási pipeline OCR‑hez** alkalmaz. A teljes Java program önálló, bármely modern JDK-n fut, és könnyű, kereshető PDF-eket állít elő, amelyek készen állnak archiválásra vagy további elemzésre.

Következő lépések? Kísérletezz különböző előfeldolgozási paraméterekkel, próbálj ki más nyelvű OCR‑t, mint az angol, vagy integráld a munkafolyamatot egy Spring Boot mikroservice‑be, amely figyeli a könyvtárat és helyben dolgozza fel a fájlokat. A fő koncepciók – licenc betöltése, motor konfigurálása, előfeldolgozás és PDF tömörítés – változatlanok, így szilárd alapot adnak bármely OCR‑alapú projekthez.

Van kérdésed vagy szeretnéd megosztani a saját módosításaidat? Hagyj egy megjegyzést alább, és jó kódolást!

![Diagram of batch OCR workflow showing input images, preprocessing, OCR engine, and compressed PDF output](alt="Diagram of batch OCR workflow showing input images, preprocessing, OCR engine, and compressed PDF output")

## Mit érdemes legközelebb megtanulni?

A következő útmutatók szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljes, működő kódpéldákat tartalmaz lépésről‑lépésre magyarázatokkal, hogy elsajátíthasd a további API funkciókat, és alternatív megvalósítási megközelítéseket fedezhess fel saját projektjeidben.

- [PDF szöveg felismerése – OCR műveletek Aspose.OCR for Java-val](/ocr/english/java/ocr-operations/)
- [szöveg kép felismerése Aspose OCR-rel – Teljes Java OCR útmutató](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Kép konvertálása szöveggé Java-ban az Aspose.OCR BufferedImage használatával](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}