---
category: general
date: 2026-02-22
description: Hogyan használjunk OCR-t Java-ban a képből szöveg kinyerésére, hogyan
  javíthatjuk az OCR pontosságát, és hogyan tölthetünk be képet OCR-hez gyakorlati
  kódrészletekkel.
draft: false
keywords:
- how to use OCR
- extract text from image
- improve OCR accuracy
- load image for OCR
- OCR preprocessing
language: hu
og_description: Hogyan használjunk OCR-t Java-ban a képről szöveg kinyeréséhez és
  az OCR pontosságának javításához. Kövesse ezt az útmutatót egy azonnal futtatható
  példáért.
og_title: Hogyan használjuk az OCR-t Java-ban – Teljes lépésről‑lépésre útmutató
tags:
- OCR
- Java
- Image Processing
title: OCR használata Java-ban – Teljes lépésről lépésre útmutató
url: /hu/java/ocr-operations/how-to-use-ocr-in-java-complete-step-by-step-guide/
---

all translations, preserving everything else.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan használjunk OCR-t Java-ban – Teljes lépésről‑lépésre útmutató

Valaha szükséged volt **how to use OCR**-re egy remegő képernyőképen, és elgondolkodtál, miért néz ki a kimenet úgy, mint egy kusza szöveg? Nem vagy egyedül. Sok valós alkalmazásban—számlák beolvasása, űrlapok digitalizálása vagy szöveg kinyerése mémekből—megbízható eredmény eléréséhez néhány egyszerű beállításra van szükség.

Ebben az útmutatóban végigvezetünk a **how to use OCR** folyamaton, hogy *extract text from image* fájlokból szöveget nyerjünk ki, megmutatjuk, hogyan **improve OCR accuracy**, és bemutatjuk a helyes **load image for OCR** módot egy népszerű Java OCR könyvtár használatával. A végére egy önálló programod lesz, amelyet bármely projektbe beilleszthetsz.

## Amit megtanulsz

- A pontos kód, amire szükséged van a **load image for OCR**-hez (rejtett függőségek nélkül).
- Mely előfeldolgozási flag-ek növelik a **improve OCR accuracy**-t, és miért fontosak.
- Hogyan olvasd ki az OCR eredményt és írd ki a konzolra.
- Gyakori buktatók—például a érdeklődési terület (ROI) beállításának elhagyása vagy a zajcsökkentés figyelmen kívül hagyása—és hogyan kerüld el őket.

### Előfeltételek

- Java 17 vagy újabb (a kód bármely friss JDK-val lefordítható).
- Egy OCR könyvtár, amely biztosítja az `OcrEngine`, `ImagePreprocessingOptions`, `OcrInput` és `OcrResult` osztályokat (például a fiktív `com.example.ocr` csomag a példában). Cseréld le a saját használt könyvtáradra.
- Egy minta kép (`skewed_noisy.png`), amely egy hivatkozható mappában van elhelyezve.

> **Pro tipp:** Ha kereskedelmi SDK-t használsz, győződj meg róla, hogy a licencfájl a classpath-eden van; ellenkező esetben a motor inicializációs hibát dob.

---

## 1. lépés: OCR motor példány létrehozása – **how to use OCR** hatékonyan

Az első dolog, amire szükséged van, egy `OcrEngine` objektum. Gondolj rá úgy, mint egy agyra, amely értelmezi a pixeleket.

```java
// Step 1: Initialize the OCR engine
import com.example.ocr.OcrEngine;

OcrEngine ocrEngine = new OcrEngine();
```

*Miért fontos:* Motor nélkül nincs kontextusod a nyelvi modellekhez, karakterkészletekhez vagy képi heurisztikákhoz. A korai példányosítás lehetővé teszi, hogy később előfeldolgozási beállításokat csatolj.

---

## 2. lépés: Kép előfeldolgozás beállítása – **improve OCR accuracy**

Az előfeldolgozás a titkos összetevő, amely egy zajos beolvasást tiszta, gép‑olvasható szöveggé alakít. Az alábbiakban engedélyezzük a deskew-et, a magas szintű zajcsökkentést, az automatikus kontrasztot és egy érdeklődési területet (ROI), hogy a kép releváns részére fókuszáljunk.

```java
import com.example.ocr.ImagePreprocessingOptions;
import java.awt.Rectangle;

// Step 2: Set up preprocessing to improve OCR accuracy
ImagePreprocessingOptions preprocessing = new ImagePreprocessingOptions();
preprocessing.setDeskewEnabled(true); // Correct image rotation
preprocessing.setNoiseReductionLevel(
        ImagePreprocessingOptions.NoiseReduction.HIGH); // Reduce speckles
preprocessing.setAutoContrastEnabled(true); // Boost contrast
preprocessing.setRegionOfInterest(new Rectangle(100, 200, 800, 600)); // Process a sub‑region only

ocrEngine.setPreprocessingOptions(preprocessing);
```

*Miért fontos:*  
- **Deskew** igazítja a forgatott szöveget, ami elengedhetetlen, ha a nyugtákat nem tökéletesen sík felületen szkennelik.  
- **Noise reduction** eltávolítja a szóró pixeleket, amelyeket egyébként karakterként értelmezne a rendszer.  
- **Auto‑contrast** kibővíti a tónus tartományt, így a halvány betűk is kiemelkednek.  
- **ROI** azt mondja a motornak, hogy hagyja figyelmen kívül a nem releváns kereteket, ezzel időt és memóriát takarítva meg.

Ha kihagyod ezeket, valószínűleg csökkenést fogsz látni a **improve OCR accuracy** eredményekben.

---

## 3. lépés: Kép betöltése OCR-hez – **load image for OCR** helyesen

Most már ténylegesen a motorra mutatunk a beolvasni kívánt fájlra. Az `OcrInput` osztály több képet is elfogadhat, de ebben a példában egyszerűen tartjuk.

```java
import com.example.ocr.OcrInput;

// Step 3: Load the image you want to extract text from
OcrInput ocrInput = new OcrInput();
ocrInput.add("YOUR_DIRECTORY/skewed_noisy.png"); // replace with your real path
```

*Miért fontos:* Az útvonalnak abszolútnak vagy a munkakönyvtárhoz relatívnak kell lennie; ellenkező esetben a motor `FileNotFoundException`-t dob. Emellett vedd figyelembe, hogy az `add` metódus neve arra utal, hogy több képet is sorba állíthatsz—hasznos kötegelt feldolgozáshoz.

---

## 4. lépés: OCR végrehajtása és a felismert szöveg kiírása – **how to use OCR** vég‑végig

Végül megkérjük a motort, hogy ismerje fel a szöveget és írja ki. Az `OcrResult` objektum tartalmazza a nyers karakterláncot, a megbízhatósági pontszámokat és sor‑soron metaadatokat (ha később szükséged van rá).

```java
import com.example.ocr.OcrResult;

// Step 4: Run OCR and print the extracted text
OcrResult ocrResult = ocrEngine.recognize(ocrInput);
System.out.println("=== OCR Output ===");
System.out.println(ocrResult.getText());
```

**Várható kimenet** (feltételezve, hogy a minta kép a „Hello, OCR World!” szöveget tartalmazza):

```
=== OCR Output ===
Hello, OCR World!
```

Ha az eredmény összezavarodottnak tűnik, menj vissza a 2. lépéshez és finomítsd az előfeldolgozási beállításokat—például csökkentsd a zajcsökkentés szintjét vagy állítsd be a ROI téglalapot.

---

## Teljes, futtatható példa

Az alábbiakban egy teljes Java programot találsz, amelyet beilleszthetsz egy `OcrDemo.java` nevű fájlba. Összekapcsolja a megbeszélt minden lépést.

```java
// OcrDemo.java – A complete, runnable example showing how to use OCR in Java
import com.example.ocr.OcrEngine;
import com.example.ocr.ImagePreprocessingOptions;
import com.example.ocr.OcrInput;
import com.example.ocr.OcrResult;
import java.awt.Rectangle;

public class OcrDemo {
    public static void main(String[] args) {
        // 1️⃣ Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Configure preprocessing (this is the key to improve OCR accuracy)
        ImagePreprocessingOptions preprocessing = new ImagePreprocessingOptions();
        preprocessing.setDeskewEnabled(true);
        preprocessing.setNoiseReductionLevel(
                ImagePreprocessingOptions.NoiseReduction.HIGH);
        preprocessing.setAutoContrastEnabled(true);
        preprocessing.setRegionOfInterest(new Rectangle(100, 200, 800, 600));
        ocrEngine.setPreprocessingOptions(preprocessing);

        // 3️⃣ Load the image you want to extract text from
        OcrInput ocrInput = new OcrInput();
        // 👉 Replace the path with your own image location
        ocrInput.add("YOUR_DIRECTORY/skewed_noisy.png");

        // 4️⃣ Run the OCR engine and print the result
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);
        System.out.println("=== OCR Output ===");
        System.out.println(ocrResult.getText());
    }
}
```

Mentsd el a fájlt, fordítsd le a `javac OcrDemo.java` paranccsal, és futtasd a `java OcrDemo`-t. Ha minden helyesen van beállítva, a konzolon megjelenik a kinyert szöveg.

---

## Gyakori kérdések és szélhelyzetek

| Kérdés | Válasz |
|----------|--------|
| **Mi van, ha a kép JPEG formátumban van?** | Az `OcrInput.add()` metódus bármely támogatott raszteres formátumot elfogad—PNG, JPEG, BMP, TIFF. Csak módosítsd a fájl kiterjesztését az útvonalban. |
| **Feldolgozhatok több oldalt egyszerre?** | Természetesen. Hívd meg az `ocrInput.add()`-ot minden egyes fájlhoz, majd add át ugyanazt az `ocrInput`-ot a `recognize()`-nek. A motor egy összefűzött `OcrResult`-ot ad vissza. |
| **Mi van, ha az OCR eredmény üres?** | Ellenőrizd, hogy a ROI valóban tartalmaz-e szöveget. Győződj meg arról is, hogy a `setDeskewEnabled(true)` be van kapcsolva; egy 90°-os forgatás miatt a motor a képet üresnek tekintheti. |
| **Hogyan változtathatom meg a nyelvi modellt?** | A legtöbb könyvtár egy `setLanguage(String)` metódust biztosít az `OcrEngine`-en. Hívd meg a `recognize()` előtt, például `ocrEngine.setLanguage("eng")`. |
| **Van mód a megbízhatósági pontszámok lekérésére?** | Igen, az `OcrResult` gyakran biztosít `getConfidence()`-t soronként vagy karakterenként. Használd ezt az alacsony megbízhatóságú eredmények szűrésére. |

---

## Következtetés

Áttekintettük a **how to use OCR** használatát Java-ban a kezdetektől a végéig: a motor létrehozását, az előfeldolgozás beállítását a **improve OCR accuracy** érdekében, a **load image for OCR** helyes elvégzését, és végül a kinyert szöveg kiírását. A teljes kódrészlet készen áll a futtatásra, és a magyarázatok választ adnak arra, hogy „miért” van minden sor.

Készen állsz a következő lépésre? Próbáld ki a ROI téglalap cseréjét, hogy a kép különböző részeire fókuszálj, kísérletezz a `NoiseReduction.MEDIUM`-mal, vagy integráld a kimenetet egy kereshető PDF-be. Továbbá felfedezheted a kapcsolódó témákat, például a **extract text from image** használatát felhőszolgáltatásokkal, vagy több ezer fájl kötegelt feldolgozását több szálas sorral.

További kérdéseid vannak az OCR-rel, a kép előfeldolgozással vagy a Java integrációval kapcsolatban? Hagyj egy megjegyzést, és jó kódolást! 

![Hogyan használjunk OCR-t példa](/images/ocr-demo.png "hogyan használjunk OCR – Java példa az előfeldolgozás és az eredmény bemutatásával")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}