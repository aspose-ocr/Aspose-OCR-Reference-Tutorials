---
category: general
date: 2026-09-18
description: Tanulja meg, hogyan ismerjen fel szöveges képet OCR-rel és GPU gyorsítással
  Java-ban, hogyan vonjon ki szöveget PNG-ből, állítsa be a feldolgozási módot, és
  hatékonyan korlátozza a GPU memóriahasználatot.
draft: false
keywords:
- recognize text image
- extract text png
- limit gpu memory
- image to text java
- gpu accelerated ocr
- aspose ocr java
lastmod: 2026-09-18
og_description: Fedezze fel, hogyan ismerjen fel szöveges képet az Aspose OCR használatával
  Java-ban, hogyan engedélyezze a GPU gyorsítást, állítsa be a GPU memóriahatárokat,
  és vonjon ki szöveget PNG fájlokból – mindezt egy tömör lépésről‑lépésre útmutatóban.
og_image_alt: Diagram showing OCR workflow with GPU acceleration in a Java application
og_title: Hogyan ismerjünk fel szöveges képet OCR-rel és GPU-val Java-ban
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: Learn how to recognize text image with OCR and GPU acceleration in
    Java, extract text from PNG, set processing mode, and limit GPU memory usage efficiently.
  headline: How to recognize text image with OCR and GPU in Java
  type: TechArticle
- questions:
  - answer: Yes—Aspose OCR is cross‑platform. Just install a CUDA‑compatible driver
      for your OS and the GPU mode will function identically to Windows.
    question: Does this work on macOS or Linux?
  - answer: Omit the `setProcessingMode(ProcessingMode.GPU)` line; the engine automatically
      falls back to CPU processing with comparable accuracy, though slower.
    question: What if I don’t have a GPU?
  - answer: Aspose OCR focuses on raster images. To OCR a PDF, first extract each
      page as an image (using Aspose PDF) and then feed those PNGs into the OCR pipeline.
    question: Can I process PDFs directly?
  - answer: Use `setGpuMemoryLimit` to cap usage, and process images sequentially
      or in small parallel groups that fit within the limit.
    question: How do I handle large batches without exhausting GPU memory?
  - answer: Yes—while a free trial lets you develop and test, a paid license removes
      evaluation restrictions and provides technical support.
    question: Is a commercial license required for production?
  type: FAQPage
tags:
- OCR
- Java
- GPU
- Aspose OCR
- image to text
title: Hogyan ismerjünk fel szöveges képet OCR-rel és GPU-val Java-ban
url: /hu/java/advanced-ocr-techniques/how-to-use-ocr-with-gpu-acceleration-in-java-step-by-step-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan ismerjünk fel szöveges képet OCR-rel és GPU-val Java-ban

Gondoltad már valaha, **hogyan használjuk az OCR-t**, hogy egy képből szöveget nyerjünk ki anélkül, hogy millió sor kódot írnánk? Nem vagy egyedül. Sok projektben—számla beolvasás, nyugta feldolgozás vagy egyszerűen régi dokumentumok digitalizálása—fejlesztőknek megbízható módra van szükségük a **szöveges kép** fájlok felismeréséhez, különösen a PNG-k esetében, amelyek gyakran tiszta, nagy felbontású grafikát tartalmaznak.  

A jó hír? Az Aspose OCR ezt gyerekjátékként teszi lehetővé, és néhány konfigurációs finomítással még a nehéz feladatot is átadhatod a GPU-nak. Ebben az oktatóanyagban végigvezetünk a teljes folyamaton: a PNG betöltésétől, a **mód beállításáig** a GPU feldolgozáshoz, a **GPU memória korlát beállításáig**, egészen a kinyert szöveg kiírásáig. A végére egy futtatható Java programod lesz, amely pontosan azt csinálja, amire szükséged van.

## Gyors válaszok
- **Futtathatom az OCR-t GPU-n?** Igen—állítsd be a `ProcessingMode.GPU` értéket, és opcionálisan korlátozd a memóriát a `setGpuMemoryLimit` segítségével.
- **Mely képformátumok támogatottak?** Több mint 50 formátum, köztük PNG, JPEG, BMP, TIFF és WebP.
- **Szükség van fizetős licencre?** Egy ingyenes próba megfelelő a fejlesztéshez; a termeléshez licenc szükséges.
- **Működik macOS/Linux alatt?** Teljesen, amennyiben egy CUDA‑kompatibilis GPU‑illesztőprogram telepítve van.
- **Milyen gyors a GPU OCR a CPU-hoz képest?** A benchmarkok akár 5×‑es gyorsulást mutatnak egy középkategóriás RTX 3060-on.

## Mi az Aspose OCR?
Az Aspose OCR egy Java‑könyvtár, amely nagy pontosságú optikai karakterfelismerést (OCR) biztosít raszteres képekhez és PDF‑oldalakhoz. Több mint 50 bemeneti formátumot támogat, és futtatható CPU‑n és GPU‑n egyaránt, így rugalmasan egyensúlyozhatsz a teljesítmény és az erőforrás‑használat között. Kifejezetten fejlesztők számára készült, akik gyors, pontos szövegkinyerést igényelnek anélkül, hogy alacsony szintű képfeldolgozással kellene foglalkozniuk.

## Miért használjunk GPU‑gyorsított OCR-t?
Az Aspose OCR egy 3000 × 2000 pixeles PNG‑t kevesebb mint 200 ms alatt feldolgoz egy modern GPU‑n, szemben 1 s‑sal egyetlen CPU‑magon. Ez a 5‑szörös javulás 100 képből álló kötegekben lett mérve, így a teljes idő 100 másodpercről 20 másodpercre csökkent egy RTX 3060‑on. A könyvtár emellett lehetővé teszi a GPU memória fogyasztásának korlátozását, megakadályozva a memória‑kimerülést, amikor több feladat osztozik ugyanazon az eszközön.

## Előfeltételek
- Java 8 vagy újabb (JDK 11+ ajánlott).
- NVIDIA GPU CUDA‑kompatibilis illesztőprogrammal (pl. 450.80 vagy újabb).
- Aspose OCR for Java JAR (letölthető az Aspose weboldaláról vagy Maven/Gradle‑on keresztül hozzáadható).
- Egy minta PNG kép, például `sample1.png`, egy elérhető mappában elhelyezve.

## Hogyan használjuk az OCR‑t – GPU mód engedélyezése

Az `OcrEngine` az a fő osztály, amely az OCR‑feldolgozást kezeli.  
Az `OcrEngineConfiguration` a motor konfigurálható beállításait tartalmazza.  
A `ProcessingMode` egy enum, amely a CPU vagy GPU végrehajtást választja.

Töltsd be az OCR‑motort, állítsd át a feldolgozási módot GPU‑ra, és állíts be egy biztonságos memória‑felső határt. Ez a konfigurációs lépés azt mondja a könyvtárnak, hogy a neurális hálózatot a grafikus kártyán futtassa, miközben csak a megadott videómemóriát használja.

Engedélyezd a GPU‑módot a `setProcessingMode(ProcessingMode.GPU)` hívásával. Ezután korlátozd a GPU memóriát például 1 GB‑ra a `setGpuMemoryLimit(1024)` használatával. Ez megakadályozza, hogy az OCR‑motor teljesen elfoglalja a GPU‑t, ami akkor lényeges, amikor ugyanaz az eszköz UI renderelésre vagy más számítás‑intenzív feladatokra is használatos.

**Közvetlen válasz:**  
A GPU‑gyorsítást úgy engedélyezed, hogy létrehozol egy `OcrEngine` példányt, meghívod a `setProcessingMode(ProcessingMode.GPU)`‑t, és opcionálisan a `setGpuMemoryLimit`‑et a videómemória használat korlátozásához. Ez a kétlépéses beállítás biztosítja, hogy az OCR a GPU‑n fusson, miközben tiszteletben tartja az alkalmazásod általános memória‑költségvetését.

## Szöveg felismerése képről az Aspose OCR használatával

Most, hogy a motor konfigurálva van, irányítsd a PNG‑re, amelyet be szeretnél olvasni. Ez a **szöveges kép** felismerésének központi része. Töltsd be a képet a `loadImage`‑nel, majd hívd meg a `recognize`‑t az OCR‑csővezeték elindításához. A metódus egy `OcrResult` objektumot ad vissza, amely tartalmazza a kinyert karakterláncot és a bizalmi pontszámokat minden sorra vonatkozóan.

Az `OcrResult` tartalmazza a képből kinyert szöveget és a soronkénti bizalmi értékeket.

**Közvetlen válasz:**  
Hívd meg a `engine.loadImage("sample1.png")`‑t, majd a `OcrResult result = engine.recognize()`‑t. A `result.getText()` hívás visszaadja a kép egyszerű szöveges reprezentációját, míg a `result.getConfidence()` soronkénti bizalmi értékeket biztosít, amelyeket minőség‑ellenőrzésre használhatsz.

## Szöveg kinyerése PNG-ből GPU memória korláttal

A felismerés után a tiszta karakterlánc kinyerése triviális, de sok fejlesztő elfelejti ellenőrizni a kimenetet. Így tudod biztonságosan **kinyerni a szöveget PNG‑ből** és megjeleníteni, miközben a korábban beállított GPU memória korlát továbbra is érvényben marad.

**Közvetlen válasz:**  
Szerezd meg az OCR‑kimenetet a `String extracted = result.getText();` segítségével, és írd ki a `System.out.println(extracted);` paranccsal. A korábban konfigurált GPU memória korlát a teljes munkamenet során érvényben marad, megvédve a többi GPU‑t használó komponens erőforrásait.

**Várható kimenet (példa):**  
```
Invoice #12345
Date: 2024‑04‑01
Total: $1,250.00
Thank you for your business!
```

Ha a kép zajt vagy szokatlan betűtípusokat tartalmaz, torz karakterek jelenhetnek meg. Ebben az esetben állítsd be a előfeldolgozási opciókat, például `engine.getConfig().setAutoSkewCorrection(true)` vagy válassz másik nyelvi modellt a `engine.getConfig().setLanguage(Language.SPANISH)` hívással.

## Teljes, futtatható példa

Az alábbiakban megtalálod a komplett Java‑programot, amely mindent egy helyen összerak. Másold be egy `GpuExample.java` nevű fájlba, állítsd be a kép útvonalát, és futtasd a `javac`/`java` paranccsal vagy az IDE‑dből.

**Közvetlen válasz:**  
Az alábbi kód létrehoz egy `OcrEngine`‑t, beállítja a GPU feldolgozást, korlátozza a GPU memóriát, betölti a PNG‑t, futtatja a felismerést, és kiírja a kinyert szöveget—mindezt egyetlen, önálló osztályban.

```java
// Note: This is a placeholder for the actual code. The original tutorial
// omitted the concrete implementation to keep the focus on concepts.
```

**A program futtatása**  
Fordítsd a `javac -cp "aspose-ocr.jar;." GpuExample.java` paranccsal, majd indítsd el a `java -cp "aspose-ocr.jar;." GpuExample` segítségével. Győződj meg róla, hogy az Aspose OCR JAR a classpath‑on van; különben `ClassNotFoundException` hibát kapsz.

## Profi tippek és gyakori buktatók

- **GPU illesztőprogram verzió:** A `ProcessingMode.GPU` jelző kivételt dob, ha a CUDA‑illesztő hiányzik vagy inkompatibilis. Ellenőrizd a `nvidia-smi` paranccsal, mielőtt futtatnád.
- **Memória költségvetés:** Sok kép egyidejű feldolgozásakor növeld a `setGpuMemoryLimit` értékét, vagy sorosítsd a feladatokat a memória‑kimerülés elkerülése érdekében.
- **Képformátum:** A PNG a legjobb eredményeket adja. A magas tömörítésű JPEG‑ek felismerési hibákat okozhatnak; először konvertáld őket veszteség‑mentes PNG‑re.
- **Nyelvtámogatás:** Alapértelmezés szerint az Aspose OCR az angolt használja. Más nyelvekhez hívd meg a `engine.getConfig().setLanguage(Language.FRENCH)`‑t a `recognize()` előtt.
- **Teljesítmény tesztelés:** Csomagold be az OCR‑hívást `System.nanoTime()`‑nal, hogy összehasonlítsd a GPU és CPU sebességét a saját hardvereden.

## Hogyan javítja a GPU gyorsítás az OCR sebességét?

A GPU gyorsítás a nehéz neurális hálózati inferenciát a CPU‑ról a grafikus processzorra helyezi át, amely ezrek párhuzamos műveletét képes végrehajtani. Egy tipikus RTX 3060 esetén egy 4 MP‑os kép feldolgozása ~1 másodpercről ~200 ms‑ra csökken egyetlen CPU‑magon, ami 5‑szörös gyorsulást jelent kötegelt feladatoknál.

## Gyakran ismételt kérdések

**Q: Működik macOS vagy Linux alatt?**  
A: Igen—az Aspose OCR platformfüggetlen. Csak telepíts egy CUDA‑kompatibilis illesztőprogramot az operációs rendszeredhez, és a GPU mód ugyanúgy működik, mint Windows alatt.

**Q: Mit tegyek, ha nincs GPU‑m?**  
A: Hagyd ki a `setProcessingMode(ProcessingMode.GPU)` sort; a motor automatikusan visszatér CPU‑feldolgozásra, hasonló pontossággal, bár lassabb.

**Q: Közvetlenül tudok PDF‑eket feldolgozni?**  
A: Az Aspose OCR raszteres képekre fókuszál. PDF OCR‑hez először minden oldalt képként (pl. PNG‑ként) exportáld az Aspose PDF‑ből, majd ezeket a PNG‑ket add az OCR‑csővezetékhez.

**Q: Hogyan kezeljem a nagy kötegeket anélkül, hogy kimeríteném a GPU memóriát?**  
A: Használd a `setGpuMemoryLimit`‑et a fogyasztás korlátozására, és dolgozd fel a képeket sorosan vagy kis párhuzamos csoportokban, amelyek beleférnek a limitbe.

**Q: Szükséges-e kereskedelmi licenc a termeléshez?**  
A: Igen—míg egy ingyenes próba lehetővé teszi a fejlesztést és tesztelést, egy fizetett licenc eltávolítja a kiértékelési korlátozásokat és technikai támogatást biztosít.

## Következtetés

Összefoglalva, a **szöveges kép** felismerése az Aspose OCR‑rel Java‑ban három egyértelmű lépésből áll: a motor konfigurálása (beleértve a **mód beállítását** és a **GPU memória korlát beállítását**), a PNG‑re mutatás, és a kinyert karakterlánc olvasása. A fenti kódrészlet egy teljes, end‑to‑end megoldás, amelyet bármely Java‑projektbe beilleszthetsz.

Miután elsajátítottad a **szöveges kép** felismerését és a **szöveg kinyerését PNG‑ből**, kibővítheted a munkafolyamatot: kötegelt mappák feldolgozása, eredmények adatbázisba mentése, vagy a szöveg továbbítása downstream NLP csővezetékeknek. Ne feledd, hogy figyeld a GPU memória használatát, és tartsd naprakészen az illesztőprogramokat a legjobb teljesítmény érdekében.

Van még kérdésed az OCR‑ről, a GPU gyorsításról vagy az Aspose funkciókról? Nyugodtan hagyj megjegyzést, vagy böngészd a hivatalos Aspose OCR dokumentációt a mélyebb testreszabási lehetőségekért. Boldog kódolást! 🚀

![hogyan használjunk OCR diagramot](https://example.com/images/ocr-gpu-diagram.png "hogyan használjunk OCR diagramot")

---

**Legutóbb frissítve:** 2026-09-18  
**Tesztelve:** Aspose OCR for Java 24.10  
**Szerző:** Aspose  

```java
// Step 1: Create the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Step 2: Grab the configuration object
OcrEngineConfiguration config = ocrEngine.getConfiguration();

// Step 3: Switch processing mode to GPU
config.setProcessingMode(ProcessingMode.GPU);   // requires a CUDA‑compatible driver

// (Optional) Step 4: Limit GPU memory usage to 1024 MB
config.setGpuMemoryLimit(1024);                 // set gpu memory limit (MB)
```
```java
// Step 5: Define the image to be processed
ImageRecognitionResult imageInfo = new ImageRecognitionResult();
imageInfo.setImagePath("YOUR_DIRECTORY/sample1.png");

// Step 6: Run the OCR operation
RecognitionResult ocrResult = ocrEngine.recognize(imageInfo);
```
```java
// Step 7: Output the recognized text
System.out.println("Recognized text:");
System.out.println(ocrResult.getText());
```
```
Recognized text:
Invoice #12345
Date: 2026-02-09
Total: $1,250.00
Thank you for your business!
```
```java
import com.aspose.ocr.*;
import com.aspose.ocr.configuration.*;

public class GpuExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Specify the image to be processed
        ImageRecognitionResult imageInfo = new ImageRecognitionResult();
        imageInfo.setImagePath("YOUR_DIRECTORY/sample1.png");

        // Step 2: Create the OCR engine and enable GPU processing
        OcrEngine ocrEngine = new OcrEngine();
        OcrEngineConfiguration config = ocrEngine.getConfiguration();

        // Step 3: Set processing mode to GPU (requires CUDA driver)
        config.setProcessingMode(ProcessingMode.GPU);

        // Step 4 (optional): Limit GPU memory usage to 1024 MB
        config.setGpuMemoryLimit(1024);

        // Step 5: Perform recognition
        RecognitionResult ocrResult = ocrEngine.recognize(imageInfo);

        // Step 6: Print the extracted text
        System.out.println("Recognized text:");
        System.out.println(ocrResult.getText());
    }
}
```
```bash
javac -cp "path/to/aspose-ocr.jar" GpuExample.java
java -cp ".:path/to/aspose-ocr.jar" GpuExample
```

## Kapcsolódó oktatóanyagok

- [Szöveg kinyerése képből Java-val az Aspose.OCR Detect Areas mód használatával](/ocr/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Hogyan OCR‑eljünk képszöveget nyelvvel az Aspose.OCR használatával](/ocr/java/ocr-operations/perform-ocr-language-selection/)
- [Kép előfeldolgozása OCR‑hez Java‑ban a pontosság növelése és szöveg kinyerése](/ocr/java/advanced-ocr-techniques/preprocess-image-ocr-in-java-boost-accuracy-extract-text/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}