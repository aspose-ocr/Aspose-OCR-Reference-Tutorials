---
date: 2026-02-09
description: Tanulja meg, hogyan konvertálja a képet szöveggé, és hogyan nyerje ki
  a szövegterületek téglalapjait az Aspose OCR Java könyvtár segítségével. Lépésről‑lépésre
  útmutató kódrészletekkel.
linktitle: Recognize Text from Image and Retrieve Text Area Rectangles
second_title: Aspose.OCR Java API
title: Kép konvertálása szöveggé – Szöveg felismerése a képről és a szövegterületek
  téglalapjainak lekérése
url: /hu/java/ocr-basics/get-rectangles-with-text-areas/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kép konvertálása szöveggé – Szöveg felismerése képről és szövegterület téglalapjainak lekérése

## Bevezetés

Ha Java alkalmazásban **képet szeretne szöveggé konvertálni** és **szöveget felismerni képről**, az Aspose.OCR for Java gyors és pontos megoldást kínál. Ebben az útmutatóban lépésről lépésre bemutatjuk, hogyan lehet egy képből bekezdéseket kinyerni, minden szövegterülethez lekérni a körülhatároló téglalapokat, és ezeket a koordinátákat a konzolra kiírni. A végére megérti, miért működik ez a megközelítés, hogyan integrálja a könyvtárat, és hol bővítheti saját felhasználási esetekhez.

## Gyors válaszok
- **Mit jelent a „szöveg felismerése képről”?** Azt jelenti, hogy a képen lévő vizuális karaktereket szerkeszthető karakterlánc adatokká alakítjuk.  
- **Melyik könyvtár kezeli ezt Java-ban?** Aspose.OCR for Java.  
- **Szükségem van licencre a fejlesztéshez?** Teszteléshez elérhető egy ideiglenes licenc; a termeléshez teljes licenc szükséges.  
- **Kivonhatok bekezdéseket az egyes szavak helyett?** Igen – használja a `AreasType.PARAGRAPHS` értéket a bekezdés‑szintű téglalapok lekéréséhez.  
- **Kompatibilis a kód a Java 11+ verzióval?** Teljesen, az API működik a Java 11‑el és újabb verziókkal.

## Mi az a „kép konvertálása szöveggé” az Aspose.OCR-ben?
Az Aspose.OCR `RecognizePage` metódusa elemzi a bitmapet, alkalmazza az OCR algoritmusokat, és visszaadja a felismert karakterláncot. Ha szövegterületeket kér, a könyvtár kiszámítja az egyes szövegrészek pontos `Rectangle` koordinátáit, ami megkönnyíti a későbbi kiemelést vagy feldolgozást.

## Miért használja ezt a **java ocr library**-t?
- **Magas pontosság** – több nyelvet és összetett betűtípusokat támogat.  
- **Egyszerű integráció** – egyetlen JAR biztosítja a teljes OCR funkcionalitást.  
- **Rugalmas kimenet** – nyers szöveget, formázott HTML-t vagy pontos szövegterület‑téglalapokat kérhet le.  
- **Szálbiztos** – nagy áteresztőképességű szerverkörnyezetekhez alkalmas.

## Előfeltételek

- **Java Development Kit** (JDK 11 vagy újabb) telepítve van a gépén.  
- **Aspose.OCR for Java** könyvtár – töltse le a hivatalos oldalról [itt](https://releases.aspose.com/ocr/java/).  
- Egy IDE vagy build eszköz (Maven/Gradle) a JAR függőség kezeléséhez.

## Csomagok importálása

A Java projektjében importálja a szükséges osztályokat:

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

## Lépésről‑lépésre útmutató

### 1. lépés: Projekt beállítása
Hozzon létre egy új Java projektet (vagy adja hozzá egy meglévőhöz), és helyezze az Aspose.OCR JAR‑t a classpath‑ra. Ha Maven‑t használ, adja hozzá a függőséget a letöltött csomag leírása szerint.

### 2. lépés: Dokumentumkönyvtár és képadat útvonal meghatározása
Adja meg, hol található a minta kép:

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";

// The image path
String imagePath = dataDir + "p3.png";
```

### 3. lépés: Aspose.OCR példány létrehozása
Példányosítsa az OCR motorját:

```java
// Create AsposeOCR instance
AsposeOCR api = new AsposeOCR();
```

### 4. lépés: Szöveg felismerése a képen
Hívja meg a `RecognizePage` metódust, hogy a képet egyszerű szöveggé konvertálja. Ez a lépés bemutatja a **recognize text image java** alapvető képességét:

```java
try {
    // Recognize page by full path to file
    String result = api.RecognizePage(imagePath);
    System.out.println("Result: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

### 5. lépés: Téglalapok lekérése szövegterületekkel
Most kérje le a körülhatároló téglalapokat minden bekezdéshez (vagy más terület típusokhoz). Itt **extract paragraphs from image** és szerezheti meg a koordinátáikat:

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
| `IOException` a `RecognizePage`-nél | Helytelen fájlútvonal vagy hiányzó olvasási jogosultság | `imagePath` ellenőrzése, hogy létező PNG/JPG fájlra mutasson, és az alkalmazásnak legyen fájlrendszer hozzáférése. |
| Üres eredmény karakterlánc | Alacsony minőségű kép vagy nem támogatott nyelv | Előfeldolgozza a képet (kontraszt növelése, binarizálás) vagy megadja a megfelelő nyelvet a `api.setLanguage("eng")` használatával. |
| Nem térnek vissza téglalapok | Rossz `AreasType` használata (pl. `WORDS` a bekezdések helyett) | Váltson `AreasType.PARAGRAPHS` vagy `AreasType.LINES` típusra, ahogy szükséges. |

## Gyakran ismételt kérdések

**Q: Kompatibilis az Aspose.OCR a Java 11‑el?**  
A: Igen, az Aspose.OCR működik Java 11‑el és későbbi verziókkal.

**Q: Használhatom az Aspose.OCR‑t személyes és kereskedelmi projektekhez egyaránt?**  
A: Igen, bármilyen típusú projektben használható. A licenc részletekért látogasson el [ide](https://purchase.aspose.com/buy).

**Q: Hogyan szerezhetek ideiglenes licencet értékeléshez?**  
A: Ideiglenes licencet szerezhet [itt](https://purchase.aspose.com/temporary-license/).

**Q: Hol találok közösségi támogatást vagy hivatalos segítséget?**  
A: Támogatásért és megbeszélésekért látogassa meg az [Aspose.OCR fórumot](https://forum.aspose.com/c/ocr/16).

**Q: Támogatja az Aspose.OCR a több szálas feldolgozást?**  
A: Igen, a könyvtár szálbiztos, és párhuzamos környezetekben is használható a jobb teljesítmény érdekében.

## Összegzés

Ebben a **aspose ocr java tutorial**‑ban megtanulta, hogyan **konvertálja a képet szöveggé** az Aspose.OCR for Java segítségével, hogyan vonjon ki bekezdéseket, és hogyan kapja meg a pontos téglalapokat, amelyek minden szövegrészt körülvesznek. Ezek a képességek lehetővé teszik kereshető PDF‑ek létrehozását, a szöveg kiemelését UI‑rétegekben, vagy strukturált adatok továbbítását a downstream folyamatokba. Fedezze fel tovább az API‑t a nyelvi beállítások testreszabásához, különböző képformátumok kezeléséhez, vagy felhő tárolóval való integrációhoz.

---

**Last Updated:** 2026-02-09  
**Tested With:** Aspose.OCR 23.10 for Java  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}