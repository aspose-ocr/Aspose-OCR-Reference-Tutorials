---
date: 2025-12-10
description: Tanulja meg, hogyan ismerjen fel szöveget képről, és hogyan nyerjen ki
  bekezdéseket képről az Aspose.OCR for Java segítségével. Lépésről‑lépésre útmutató
  kódrészletekkel.
linktitle: Recognize Text from Image and Retrieve Text Area Rectangles
second_title: Aspose.OCR Java API
title: Képről szöveg felismerése és a szövegterület téglalapjainak lekérése
url: /hu/java/ocr-basics/get-rectangles-with-text-areas/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Képről szöveg felismerése és a szövegterületek téglalapjainak lekérése

## Bevezetés

Ha **képfájlokból kell szöveget felismerni** egy Java‑alkalmazásban, az Aspose.OCR for Java gyors és pontos megoldást kínál. Ebben az útmutatóban lépésről‑lépésre bemutatjuk, hogyan lehet egy képből bekezdéseket kinyerni, minden szövegterülethez tartozó körülhatároló téglalapot lekérni, és ezeket a koordinátákat a konzolra kiírni. A végére megérted, miért működik ez a megközelítés, hogyan integrálhatod a könyvtárat, és hol bővítheted saját felhasználási eseteidhez.

## Gyors válaszok
- **Mit jelent a „recognize text from image”?** A képben lévő vizuális karakterek szerkeszthető karakterláncokká alakítását.  
- **Melyik könyvtár végzi ezt Java‑ban?** Aspose.OCR for Java.  
- **Szükség van licencre fejlesztéshez?** Teszteléshez elérhető egy ideiglenes licenc; a termeléshez teljes licenc szükséges.  
- **Kinyerhetek bekezdéseket az egyes szavak helyett?** Igen – használd a `AreasType.PARAGRAPHS` értéket a bekezdés‑szintű téglalapokhoz.  
- **A kód kompatibilis a Java 11+ verziókkal?** Teljesen, az API működik Java 11‑el és újabb verziókkal.

## Mi a „recognize text from image” az Aspose.OCR‑ben?
Az Aspose.OCR `RecognizePage` metódusa elemzi a bitmapet, alkalmazza az OCR algoritmusokat, és visszaadja a felismert karakterláncot. Amikor szövegterületeket kérsz, a könyvtár kiszámítja az egyes szövegrészek pontos `Rectangle` koordinátáit is, így később könnyen kiemelhetők vagy feldolgozhatók a kívánt szakaszok.

## Miért válaszd az Aspose.OCR for Java‑t?
- **Magas pontosság** – több nyelvet és összetett betűtípusokat támogat.  
- **Egyszerű integráció** – egyetlen JAR biztosítja a teljes OCR funkcionalitást.  
- **Rugalmas kimenet** – nyers szöveget, formázott HTML‑t vagy pontos szöveg‑terület téglalapokat is lekérhetsz.  
- **Szálbiztos** – alkalmas nagy forgalmú szerverkörnyezetekhez.

## Előfeltételek

- **Java Development Kit** (JDK 11 vagy újabb) telepítve a gépeden.  
- **Aspose.OCR for Java** könyvtár – letölthető a hivatalos oldalról [itt](https://releases.aspose.com/ocr/java/).  
- IDE vagy build eszköz (Maven/Gradle) a JAR függőség kezeléséhez.

## Csomagok importálása

A Java projektedben importáld a szükséges osztályokat:

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AreasType;
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

## Lépés‑ről‑lépésre útmutató

### 1. lépés: Projekt beállítása
Hozz létre egy új Java projektet (vagy adj hozzá egy meglévőhöz), és helyezd az Aspose.OCR JAR‑t a classpath‑ba. Maven‑t használva add hozzá a függőséget a letöltött csomag leírása szerint.

### 2. lépés: Dokumentumkönyvtár és képút meghatározása
Add meg, hol található a minta képed:

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";

// The image path
String imagePath = dataDir + "p3.png";
```

### 3. lépés: Aspose.OCR példány létrehozása
Inicializáld az OCR motorját:

```java
// Create Aspose.OCR instance
AsposeOCR api = new AsposeOCR();
```

### 4. lépés: Szöveg felismerése a képen
Hívd meg a `RecognizePage` metódust a kép szöveggé alakításához. Ez a lépés demonstrálja a **recognize text from image** alapvető képességét:

```java
try {
    // Recognize page by full path to file
    String result = api.RecognizePage(imagePath);
    System.out.println("Result: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

### 5. lépés: Téglalapok lekérése a szövegterületekkel
Most kérd le a körülhatároló téglalapokat minden bekezdéshez (vagy más terület‑típusokhoz). Itt **kinyerheted a bekezdéseket a képből** és megkapod a koordinátáikat:

```java
// Get rectangles with text areas in the image.
ArrayList<Rectangle> rectResult = api.getTextAreas(imagePath, AreasType.PARAGRAPHS, true);

// Print each text area rectangle
for (Rectangle r : rectResult) {
    System.out.println("Text area:" + r);
}
```

## Gyakori problémák és hibaelhárítás

| Tünet | Valószínű ok | Megoldás |
|-------|--------------|----------|
| `IOException` a `RecognizePage`‑nél | Hibás fájlútvonal vagy hiányzó olvasási jogosultság | Ellenőrizd, hogy az `imagePath` egy létező PNG/JPG fájlra mutat, és az alkalmazásnak van fájlrendszer‑hozzáférése. |
| Üres eredmény‑karakterlánc | Alacsony minőségű kép vagy nem támogatott nyelv | Előfeldolgozás (kontraszt növelése, binarizálás) vagy a megfelelő nyelv megadása `api.setLanguage("eng")`‑vel. |
| Nem térnek vissza téglalapok | Rossz `AreasType` használata (pl. `WORDS` a bekezdések helyett) | Válts `AreasType.PARAGRAPHS`‑ra vagy szükség szerint `AreasType.LINES`‑ra. |

## Gyakran ismételt kérdések

**K: Az Aspose.OCR kompatibilis a Java 11‑el?**  
V: Igen, az Aspose.OCR működik Java 11‑el és újabb verziókkal.

**K: Használhatom az Aspose.OCR‑t személyes és kereskedelmi projektekben is?**  
V: Igen, bármilyen típusú projektben alkalmazható. A licenc részletekért látogasd meg [ezt az oldalt](https://purchase.aspose.com/buy).

**K: Hogyan szerezhetek ideiglenes licencet értékeléshez?**  
V: Ideiglenes licencet kaphatsz [innen](https://purchase.aspose.com/temporary-license/).

**K: Hol találok közösségi támogatást vagy hivatalos segítséget?**  
V: Támogatásért és megbeszélésekért látogasd meg az [Aspose.OCR fórumot](https://forum.aspose.com/c/ocr/16).

**K: Támogatja az Aspose.OCR a több szálon való futtatást?**  
V: Igen, a könyvtár szálbiztos, és párhuzamos környezetben is használható a jobb teljesítmény érdekében.

## Összegzés

Ebben az útmutatóban megtanultad, hogyan **recognize text from image** fájlokkal használhatod az Aspose.OCR for Java‑t, hogyan nyerheted ki a bekezdéseket, és hogyan kérheted le a pontos téglalapokat, amelyek minden szövegblokkot körülhatárolnak. Ezek a képességek lehetővé teszik kereshető PDF‑ek létrehozását, szöveg kiemelését UI‑átfedésekben, vagy strukturált adatok továbbítását downstream folyamatokba. Fedezd fel tovább az API‑t a nyelvi beállítások testreszabásához, különböző képformátumok kezeléséhez, vagy felhő‑tárolóval való integráláshoz.

---

**Utoljára frissítve:** 2025-12-10  
**Tesztelve a következővel:** Aspose.OCR 23.10 for Java  
**Szerző:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}