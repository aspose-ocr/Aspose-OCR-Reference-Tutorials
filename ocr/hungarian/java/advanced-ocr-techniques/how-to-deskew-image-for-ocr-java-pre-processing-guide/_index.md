---
category: general
date: 2026-03-18
description: Hogyan lehet gyorsan kiegyenesíteni a képet az Aspose OCR Java használatával.
  Tanulja meg, hogyan előkészítse a képet OCR-hez, tisztítsa meg a beolvasott képet,
  és javítsa az OCR pontosságát néhány lépésben.
draft: false
keywords:
- how to deskew image
- preprocess image for ocr
- extract text from image
- clean scanned image
- improve ocr accuracy
language: hu
og_description: Hogyan korrigáljuk a kép ferdeségét az Aspose OCR Java-val, előfeldolgozzuk
  a képet OCR-hez, megtisztítjuk a beolvasott képet és javítjuk az OCR pontosságát.
og_title: Hogyan kiegyenesítsük a képet OCR-hez – Java útmutató
tags:
- OCR
- Java
- Image Processing
title: Hogyan állítsuk egyenesre a képet OCR-hez – Java előfeldolgozási útmutató
url: /hu/java/advanced-ocr-techniques/how-to-deskew-image-for-ocr-java-pre-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan korrigáljuk a kép dőlését OCR-hez – Java előfeldolgozási útmutató

Valaha is elgondolkodtál azon, **hogyan korrigáljuk a kép dőlését** olyan fájloknál, amelyek a szkennertől furcsa szögben jönnek ki? Nem vagy egyedül – sok fejlesztő szembesül ezzel a problémával, amikor szöveget próbál kinyerni kép‑intenzív dokumentumokból. A jó hír? Néhány Java‑sor és az Aspose OCR segítségével kiegyenesítheted, zajtalaníthatod, és tiszta szöveget nyerhetsz ki anélkül, hogy izzadnál.

Ebben a tutorialban végigvezetünk a teljes munkafolyamaton: egy zajos, elfordított szkennelés betöltése, deskew szűrő alkalmazása, vizuális zavarok eltávolítása, és végül **kép szövegének kinyerése**. A végére megtanulod, hogyan **előfeldolgozni a képet OCR-hez**, **tisztítani a beolvasott képet**, és **javítani az OCR pontosságát** bármely projektnél, amely megbízható szövegkinyerést igényel.

## Amire szükséged lesz

- Java 17 (vagy bármely újabb JDK) – a kód a szabványos nyelvi funkciókat használja.
- Aspose OCR for Java könyvtár (az ingyenes próba verzió jól működik kísérletezéshez).
- Egy mintakép, amely zajos és elfordított is (például `noisy-rotated.png`).
- A kedvenc IDE-d (IntelliJ IDEA, Eclipse, VS Code…) – bármi, ami képes Java-t fordítani.

Nem szükséges extra keretrendszer, Maven/Gradle varázslás; az egyetlen import utasítások azok, amik alább láthatók.

---

## Hogyan korrigáljuk a kép dőlését az Aspose OCR-rel

Az első dolog, amit meg kell oldani, a kép dőlése. Ha a szövegsorok nem vízszintesen helyezkednek el, az OCR motor helytelenül olvassa a karaktereket. A `DeskewFilter` végzi a nehéz munkát.

```java
import com.aspose.ocr.OcrEngine;
import com.aspose.ocr.Image;
import com.aspose.ocr.preprocess.DeskewFilter;
import com.aspose.ocr.preprocess.DenoiseFilter;

public class PreprocessDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the raw scanned image
        Image scannedImage = Image.load("YOUR_DIRECTORY/noisy-rotated.png");

        // Step 3: Correct the image orientation (deskew)
        DeskewFilter deskewFilter = new DeskewFilter();
        scannedImage = deskewFilter.apply(scannedImage);

        // Step 4: Reduce visual noise (denoise)
        DenoiseFilter denoiseFilter = new DenoiseFilter();
        scannedImage = denoiseFilter.apply(scannedImage);

        // Step 5: Perform OCR on the cleaned image
        String recognizedText = ocrEngine.recognize(scannedImage);

        // Step 6: Output the extracted text
        System.out.println(recognizedText);
    }
}
```

> **Miért fontos:** A `DeskewFilter` elemzi a kép geometriáját, becsli a forgatási szöget, és visszaforgatja a bitmapet egy szintbe. Enélkül a legtöbb OCR motor a ferde betűket teljesen más glifként kezeli, ami lecsökkenti a **javítani az OCR pontosságát** erőfeszítéseidet.
> 
> **Pro tipp:** Ha olyan dokumentumokkal dolgozol, amelyek fejjel lefelé is lehetnek, engedélyezd a `setAutoRotate` flag-et a `DeskewFilter`‑n (újabb Aspose kiadásokban elérhető). Automatikusan 180°‑ot fordít, ha szükséges.

![Diagram showing before and after rotation – how to deskew image example](https://example.com/deskew-diagram.png "hogyan korrigáljuk a kép dőlését példa")

*Image alt text: hogyan korrigáljuk a kép dőlését példa*

---

## Előfeldolgozni a képet OCR-hez – Zajszűrés és tisztítás

Miután a kép kiegyenesedett, a következő akadály a vizuális zaj – azok a foltok, tömörítési artefaktok vagy halvány háttérminták, amelyek összezavarják az OCR motort. A `DenoiseFilter` egy finom simító algoritmust alkalmaz, amely megőrzi a széleket (a betűket), miközben eltávolítja a szemcsét.

```java
// Step 4 (continued): Reduce visual noise (denoise)
DenoiseFilter denoiseFilter = new DenoiseFilter();
scannedImage = denoiseFilter.apply(scannedImage);
```

### Mikor állítsuk be a zajszűrés beállításait

- **Nagyon sötét beolvasások:** Növeld a szűrő erősségét (`denoiseFilter.setStrength(2)`) a háttérárnyékok eltávolításához.
- **Finom nyomtatott betűtípusok:** Csökkentsd az erősséget, hogy elkerüld a kis szárnyak elmosódását.
- **Színes dokumentumok:** Először konvertáld szürkeárnyalatúra (`scannedImage = scannedImage.toGrayscale();`) – az OCR motor a legjobban egycsatornás képeken működik.

Ezek a finomhangolások a **tisztítani a beolvasott képet** legjobb gyakorlatai; egy tisztább bitmap közvetlenül magasabb bizalmi pontszámokhoz vezet az OCR motorban.

---

## Kép szövegének kinyerése – OCR motor futtatása

Most, hogy a kép egyenes és csendes, itt az ideje **kép szövegének kinyerésének**. Az `OcrEngine` osztály mindent a háttérben kezel: szegmentálás, karakterosztályozás és nyelvi modellezés.

```java
// Step 5: Perform OCR on the cleaned image
String recognizedText = ocrEngine.recognize(scannedImage);
System.out.println(recognizedText);
```

#### Várható kimenet

Ha a forrásfájlod tartalmazza a “**Invoice # 12345**” sort, a konzol valami ilyesmit kell, hogy kiírjon:

```
Invoice # 12345
Date: 2026-03-18
Total: $1,250.00
```

Ha a kimenet összemosódottnak tűnik, ellenőrizd a korábbi lépéseket – különösen a deskew‑et. Már egy 1‑fokos dőlés is tönkreteheti a számokat és szimbólumokat.

---

## Gyakori buktatók és tippek az **OCR pontosság javításához**

| Probléma | Miért rontja a pontosságot | Gyors megoldás |
|----------|----------------------------|----------------|
| **Maradék forgatás** | Az OCR vízszintes alapvonalakat vár. | Ellenőrizd a `deskewFilter.getAngle()` értékét és logold. |
| **Túlzott zajszűrés** | Elmosódnak a vékony vonalak, a “i” “l”‑vé válik. | Használd a `setStrength(0.5)`‑ot finom betűtípusokhoz. |
| **Rossz képformátum** | A JPEG tömörítés artefaktusokat ad hozzá. | Előnyben részesítsd a PNG vagy TIFF formátumot veszteségmentes tároláshoz. |
| **Helytelen nyelv** | A motor alapértelmezés szerint angolt használ; más ábécékhez explicit beállítás szükséges. | `ocrEngine.setLanguage(OcrEngine.Language.Spanish);` |
| **Alacsony DPI (≤150)** | Nem elegendő pixeladat a megbízható szegmentáláshoz. | Resample-eld 300 DPI‑re a feldolgozás előtt (`scannedImage = scannedImage.resample(300);`). |

### Bónusz: Kötetes feldolgozás

Ha egy mappában több szkennelésed van, csomagold a demót egy ciklusba:

```java
File folder = new File("YOUR_DIRECTORY");
for (File file : folder.listFiles((dir, name) -> name.endsWith(".png"))) {
    Image img = Image.load(file.getAbsolutePath());
    img = new DeskewFilter().apply(img);
    img = new DenoiseFilter().apply(img);
    String text = ocrEngine.recognize(img);
    System.out.println("=== " + file.getName() + " ===");
    System.out.println(text);
}
```

Ez a minta lehetővé teszi, hogy **előfeldolgozni a képet OCR-hez** nagy léptékben, miközben a kódbázis rendezett és a teljesítmény kiszámítható marad.

---

## Összefoglalás és következő lépések

Áttekintettük, hogyan **korrigáljuk a kép dőlését**, **előfeldolgozni a képet OCR-hez**, és végül **kép szövegének kinyerése** az Aspose OCR Java segítségével. A szkennelés kiegyenesítésével, a zaj eltávolításával és egy tiszta bitmap átadásával az OCR motorhoz, jelentősen **javítani fogod az OCR pontosságát** minden esetben.

Mi a következő? Fontold meg ezeket a kiterjesztéseket:

- **Nyelvfelismerés** – állítsd be a `ocrEngine.setLanguage`‑t a felismert írásrendszer alapján.
- **PDF kimenet** – a felismert szöveget egy PDF generátorba tápláld kereshető dokumentumok létrehozásához.
- **Gépi tanulás utófeldolgozás** – futtass helyesírás-ellenőrzést vagy egyedi szótárakat az OCR eredményen.

Próbáld ki ezeket az ötleteket, kísérletezz különböző szűrőerősségekkel, és hamarosan egy szilárd csővezetéked lesz bármely dokumentum‑digitalizációs projekthez.

*Boldog kódolást! Ha elakadsz, hagyj egy megjegyzést alul – segítek finomhangolni a deskew és denoise paramétereket.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}