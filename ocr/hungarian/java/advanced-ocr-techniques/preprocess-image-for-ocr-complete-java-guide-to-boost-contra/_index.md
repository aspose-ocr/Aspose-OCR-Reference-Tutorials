---
category: general
date: 2026-02-17
description: Készíts elő képet az OCR-hez az Aspose OCR Java használatával. Tanulja
  meg, hogyan növelheti a kép kontrasztját, állíthatja be a kontraszt szintjét, és
  percek alatt felismerheti a szöveget a képen.
draft: false
keywords:
- preprocess image for ocr
- boost image contrast
- recognize text from image
- extract text using OCR
- set contrast level
language: hu
og_description: Képek előfeldolgozása OCR-hez az Aspose OCR Java használatával. Ez
  az útmutató bemutatja, hogyan lehet növelni a kép kontrasztját, beállítani a kontraszt
  szintjét, és gyorsan felismerni a szöveget a képről.
og_title: Kép előfeldolgozása OCR-hez – Java útmutató a kontraszt növeléséhez és a
  szöveg kinyeréséhez
tags:
- Java
- OCR
- Image Processing
title: Kép előfeldolgozása OCR-hez – Teljes Java útmutató a kontraszt növeléséhez
  és a szöveg kinyeréséhez
url: /hu/java/advanced-ocr-techniques/preprocess-image-for-ocr-complete-java-guide-to-boost-contra/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR-hez előfeldolgozott kép – Teljes Java útmutató

Valaha is szükséged volt **preprocess image for OCR**-ra, de nem tudtad, mely beállítások hoznak valódi különbséget? Nem vagy egyedül. A legtöbb fejlesztő csak rátesz egy képet az OCR motorra, és reméli, hogy varázslat történik, csak hogy összekuszálódott kimenetet kapjon. Ebben az útmutatóban egy gyakorlati, vég‑től‑végig példán keresztül mutatjuk be, hogyan **boosts image contrast**, módosítjuk a **contrast level**‑t, és végül **recognizes text from image**‑t használva az Aspose OCR for Java-t.

Amikor befejezed, egy újrahasználható kódrészletet kapsz, amely megbízhatóan **extracts text using OCR**, még zajos szkenneléseknél is. Nincsenek rejtett trükkök, csak tiszta lépések és a mögöttük álló érvelés.

## Amire szükséged lesz

- Java 17 vagy újabb (a kód bármely friss JDK-val fordítható)
- Aspose OCR for Java könyvtár (letölthető a hivatalos Aspose weboldalról)
- Érvényes Aspose OCR licencfájl (`Aspose.OCR.lic`)
- Bemeneti kép (`input.jpg`), amelyet be szeretnél olvasni
- Kedvenc IDE vagy egyszerű parancssori beállítás

Ha már megvannak ezek, nagyszerű—merüljünk el azonnal.

## 1. lépés: Az Aspose OCR licenc betöltése (Alapbeállítás)

Mielőtt az OCR motor bármit tenne, tudnia kell, hogy licencelt vagy. Ellenkező esetben egy próba‑vízjelet kapsz.

```java
import com.aspose.ocr.*;

public class PreprocessDemo {
    public static void main(String[] args) throws Exception {

        // Load the Aspose OCR license – this disables the evaluation limits
        License ocrLicense = new License();
        ocrLicense.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");
```

**Miért fontos:** Megfelelő licenc nélkül a motor értékelő módban fut, ami lerövidítheti az eredményeket vagy vízjeleket ad hozzá. A licenc korai beállítása biztosítja, hogy a későbbi előfeldolgozási beállítások teljes funkciókészlettel legyenek alkalmazva.

## 2. lépés: Az OCR motor inicializálása

Egy `OcrEngine` példány létrehozása hozzáférést biztosít a felismerési és az előfeldolgozási folyamatokhoz egyaránt.

```java
        // Initialise the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
```

**Pro tipp:** Tartsd a motort singletonként, ha sok képet szeretnél kötegben feldolgozni; ez belső erőforrásokat cache-el és felgyorsítja a későbbi hívásokat.

## 3. lépés: Az előfeldolgozás beállítása – Deskew, Denoise és kontrasztnövelés

Itt történik a **preprocess image for OCR**. A három beállítás, amelyet módosítunk:

1. **Deskew** – korrigálja a kisebb elforgatásokat.
2. **Denoise** – eltávolítja azokat a szemcséket, amelyek megzavarják a karakterek szegmentálását.
3. **Contrast enhancement** – a sötét szöveget kiemeli a háttérből.

```java
        // Access preprocessing settings
        PreprocessingSettings preprocessing = ocrEngine.getPreprocessing();

        // Enable automatic deskew (helps with scanned pages that are a few degrees off)
        preprocessing.setDeskew(true);
        preprocessing.setDeskewAngleTolerance(0.1); // tolerance in degrees

        // Turn on denoising – median works well for salt‑and‑pepper noise
        preprocessing.setDenoise(true);
        preprocessing.setDenoiseMode(DenoiseMode.MEDIAN); // alternatives: GAUSSIAN

        // Boost contrast – this is the “boost image contrast” step
        preprocessing.setContrastEnhance(true);
        preprocessing.setContrastLevel(1.3f); // 1.0 = no change, >1.0 = stronger contrast
```

### Miért állítsuk be a kontrasztszintet?

A kontrasztszint növelése kinyújtja a kép hisztogramját, sötét pixeleket sötétebbé, világos pixeleket világosabbá téve. Gyakorlatban egy **contrast level** érték `1.3f` gyakran a legjobb egyensúlyt adja nyomtatott dokumentumoknál, míg a `1.5f` feletti érték túlzottan kiemelheti a vékony vonalakat. Nyugodtan kísérletezz; a beállítás olcsó módosítani, és drámaian javíthatja a **recognize text from image** sikerességét.

## 4. lépés: A bemeneti kép előkészítése

Az `OcrInput` osztály elrejti a fájlkezelést. Több képet is hozzáadhatsz, ha kötegelt feldolgozásra van szükség.

```java
        // Prepare the image for OCR – you can add more files to the same OcrInput
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/input.jpg");
```

**Edge case:** Ha a képed nem szabványos formátumban van (pl. többoldalas TIFF), akkor minden oldalt külön betölthetsz, vagy először PNG/JPEG formátumba konvertálhatod.

## 5. lépés: A felismerés végrehajtása

Most a motor lefuttatja a korábban beállított előfeldolgozási csővezetéket, majd a tisztított képet átadja a fő OCR algoritmusnak.

```java
        // Run OCR – this returns a result object containing the extracted text
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);
```

**Mi történik a háttérben?** Az Aspose OCR először alkalmazza a deskew transzformációt, majd futtatja a denoise szűrőt, végül állítja be a kontrasztot, mielőtt a képet a neurális‑hálózaton alapuló felismerőnek adná. A sorrend szándékos; a módosítása alacsonyabb eredményekhez vezethet.

## 6. lépés: A felismert szöveg kiírása

Végül kiírjuk a kinyert karakterláncot a konzolra. Egy valódi alkalmazásban fájlba írhatod vagy hálózaton keresztül küldheted.

```java
        // Print the recognized text to the console
        System.out.println(ocrResult.getText());
    }
}
```

### Várható kimenet

Ha a `input.jpg` a “Hello World!” kifejezést tartalmazza, a konzolnak a következőt kell mutatnia:

```
Hello World!
```

Ha a kimenet összekuszáltnak tűnik, ellenőrizd újra az előfeldolgozási értékeket – különösen a **contrast level**‑t és a **denoise mode**‑t – és próbálj ki másik képformátumot.

## Bónusz: Az előfeldolgozott kép megjelenítése (opcionális)

Néha szeretnéd látni, hogy a motor mit lát a deskew, denoise és kontrasztnövelés után. Az Aspose OCR lehetővé teszi a köztes bitmap exportálását:

```java
        // Export the pre‑processed image for debugging
        BufferedImage processed = preprocessing.getProcessedImage();
        ImageIO.write(processed, "png", new File("processed.png"));
```

Nyisd meg a `processed.png`-t az eredetivel egymás mellett; észre fogod venni a egyenesebb vízszintet és a tisztább szöveget. Ez a lépés hasznos, ha azt vizsgálod, miért hibás egy adott szken.

![OCR-hez előfeldolgozott kép példája](/images/ocr-preprocess-example.png "OCR előfeldolgozása – kontraszt növelése előtte és után")

*A fenti kép azt mutatja, hogyan alakítja a kontraszt növelése és a zajszűrés egy homályos szkennelt képet tiszta, OCR‑kész képpé.*

## Gyakori buktatók és elkerülésük módjai

| Pitfall | Why it Happens | Fix |
|---------|----------------|-----|
| **Over‑contrasting** (`setContrastLevel` túl magas) | A világos háttér fehérre vált, és elhalványuló karaktereket töröl | Tartsd a szintet 1.1 és 1.4 között a legtöbb nyomtatott szöveghez |
| **Deskew tolerance too low** | A kis elforgatások nem kerülnek korrigálásra | `setDeskewAngleTolerance` értékét emeld 0.2‑re vagy 0.3‑ra a beolvasott könyvekhez |
| **Using GAUSSIAN denoise on binary images** | Elmosódik a szélek, és a karakterek egyesülnek | Használd a `DenoiseMode.MEDIAN`‑t fekete‑fehér szkenneléseknél |
| **Missing license** | A motor próba‑módra vált, és a kimenetet lerövidíti | Ellenőrizd az `Aspose.OCR.lic` elérési útját, és hogy a fájl olvasható‑e |

## Következő lépések: Alapvető előfeldolgozáson túl

Most, hogy képes vagy **preprocess image for OCR**‑ra és **extract text using OCR**‑ra, fontold meg ezeket a kiterjesztéseket:

- **Language packs** – tölts be specifikus nyelvi szótárakat a nem‑angol szövegek pontosságának javításához.
- **Region‑of‑interest (ROI) cropping** – a kép egy részére fókuszálj, ha csak az oldal egy részére van szükség.
- **Batch processing** – egy könyvtár képeit iteráld, ugyanazt a `OcrEngine` példányt újrahasználva a sebességért.
- **Integrate with PDF** – kombináld az Aspose OCR‑t az Aspose PDF‑el, hogy a beolvasott PDF‑eket egy lépésben kereshető PDF‑vé alakítsd.

Ezek a témák természetesen tartalmazzák a másodlagos kulcsszavainkat: továbbra is **boosts image contrast**, **set contrast level**, és **recognize text from image**‑t fogsz használni számos szituációban.

## Összegzés

Mindezt lefedtük, ami a **preprocess image for OCR**‑hoz szükséges az Aspose OCR for Java használatával: a licenc betöltése, a deskew, denoise és kontrasztnövelés beállítása, a kép betáplálása, és végül a **recognize text from image**. A fenti teljes, futtatható példával most már **extract text using OCR**‑t hajthatsz végre bármely megfelelően előkészített képen.

Próbáld ki a kódot, állítsd be a **contrast level**‑t, és figyeld, ahogy a pontosság növekszik. Amikor készen állsz, fedezd fel a nyelvspecifikus modelleket vagy a kötegelt folyamatokat, hogy ezt az egyképes demót termelés‑kész megoldássá alakítsd.

*Boldog kódolást, és legyenek a szkenneléseid mindig élesek!*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}