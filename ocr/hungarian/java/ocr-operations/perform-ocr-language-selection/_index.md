---
date: 2026-02-12
description: Tanulja meg, hogyan OCR-ozhat képek szövegét nyelvválasztással az Aspose.OCR
  for Java használatával. Ez a lépésről‑lépésre útmutató lefedi a szöveg kinyerését
  Java-ban, az OCR dőléskorrekciót és még sok mást.
linktitle: How to OCR Image Text with Language Using Aspose.OCR
second_title: Aspose.OCR Java API
title: Hogyan OCR-eljük a képen lévő szöveget nyelvvel az Aspose.OCR segítségével
url: /hu/java/ocr-operations/perform-ocr-language-selection/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan OCR-eljünk képszöveget nyelvvel az Aspose.OCR segítségével

## Bevezetés

A szöveg kinyerése képfájlokból gyakori igény, legyen szó beolvasott dokumentumok digitalizálásáról, nyugták feldolgozásáról vagy kereshető archívumok építéséről. Ebben az oktatóanyagban egy teljes, gyakorlati példán keresztül mutatjuk be, **hogyan OCR-eljünk képszöveget** egy adott nyelvi beállítással, így már ma integrálhat megbízható OCR-t Java‑alkalmazásaiba. Emellett megismerheti az OCR dőléskorrekció és a terület‑alapú felismerés kezelését a legjobb pontosság érdekében.

## Gyors válaszok
- **Melyik könyvtár kezeli az OCR‑t Java‑ban?** Aspose.OCR for Java  
- **Melyik beállítás választja ki a nyelvet?** `settings.setLanguage(Language.Eng)` (vagy bármely támogatott nyelv)  
- **Szükségem van licencre fejlesztéshez?** Egy ingyenes értékelő licenc elegendő a teszteléshez; a termeléshez kereskedelmi licenc szükséges.  
- **Korlátozhatom az OCR‑t a kép egy régiójára?** Igen, használd a `RecognitionSettings.setRecognitionAreas()` metódust téglalapokkal.  
- **Mi a tipikus futási idő?** Néhány másodperc oldalanként egy átlagos laptopon, a kép méretétől és a nyelv összetettségétől függően.

## Hogyan OCR-eljünk képszöveget nyelvválasztással
Ebben a részben a fő kérdésre válaszolunk: **hogyan OCR-eljünk egy képet**, ha ismerjük a szöveg nyelvét. A megfelelő nyelv kiválasztása drámaian javítja a felismerés pontosságát, mivel az OCR‑motor nyelvspecifikus szótárakat és karaktermodelleket alkalmaz.

### Miért fontos ez
- **Magasabb pontosság** – a nyelvspecifikus modellek csökkentik a hibás felismeréseket.  
- **Teljesítményjavulás** – a motor kihagyja a felesleges nyelvellenőrzéseket.  
- **Jobb diakritikus kezelés** – a francia, spanyol, német stb. nyelvek helyesen ismerhetők fel, ha a megfelelő `Language` enumot használjuk.

## Mi az a „szöveg kinyerése képből”?
A szöveg kinyerése képből (OCR) a karakterek vizuális ábrázolását géppel olvasható karakterláncokká alakítja. Ez lehetővé teszi a keresést, az elemzést és az adatkinyerési munkafolyamatokat, amelyek egyébként manuális átírást igényelnének.

## Miért használjuk az Aspose.OCR‑t nyelvválasztással?
- **Többnyelvű támogatás** – Válassza ki a képen jelenlévő pontos nyelvet (nyelveket) a pontosság növelése érdekében.  
- **Finomhangolt vezérlés** – Állítsa be a dőlést, határozza meg a felismerési területeket, és konfigurálja az automatikus dőlést.  
- **Tiszta Java API** – Nincsenek natív függőségek, könnyen integrálható bármely Java projektbe.  
- **Gazdag eredményadat** – Egy hívásban kapja meg a sima szöveget, JSON‑t, határoló téglalapokat és figyelmeztetéseket.

## Előfeltételek

Mielőtt elkezdené, győződjön meg róla, hogy rendelkezik:

- **Java Development Kit (JDK)** telepítve (JDK 8 vagy újabb).  
- **Aspose.OCR for Java** könyvtár – töltse le a hivatalos oldalról [itt](https://reference.aspose.com/ocr/java/).  
- Egy képfájl, amely a kinyerni kívánt szöveget tartalmazza, például `p3.png`.

## Csomagok importálása

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.Language;
import com.aspose.ocr.License;
import com.aspose.ocr.RecognitionResult;
import com.aspose.ocr.RecognitionSettings;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

## Lépésről‑lépésre útmutató

### 1. lépés: Dokumentumkönyvtár beállítása

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";
```

Cserélje le a `"Your Document Directory"` szöveget arra az abszolút útvonalra, ahol a `p3.png` található.

### 2. lépés: Kép útvonalának meghatározása

```java
// The image path
String file = dataDir + "p3.png";
```

Győződjön meg arról, hogy a `file` változó a pontosan feldolgozni kívánt képre mutat.

### 3. lépés: Aspose.OCR API példány létrehozása

```java
// Create API instance
AsposeOCR api = new AsposeOCR();
```

Az `AsposeOCR` objektum hozzáférést biztosít az összes OCR művelethez.

### 4. lépés: Felismerési beállítások megadása (nyelvválasztás)

```java
// Set recognition options
RecognitionSettings settings = new RecognitionSettings();
settings.setAutoSkew(false);
ArrayList<Rectangle> rectangles = new ArrayList<Rectangle>();
rectangles.add(new Rectangle(90, 186, 775, 95));
settings.setRecognitionAreas(rectangles);
settings.setSkew(0.5);
settings.setLanguage(Language.Eng);
```

Itt:

1. Letiltjuk az automatikus dőlést, mert manuális dőlést adunk meg.  
2. Meghatározunk egy téglalap alakú régiót (`RecognitionAreas`), hogy az OCR csak a tényleges szöveget tartalmazó képrészre korlátozódjon.  
3. **language**‑t angolra (`Language.Eng`) állítjuk. Cserélje ezt `Language.Fra`, `Language.Spa` stb.-re a forráskép nyelvének megfelelően.

### 5. lépés: OCR végrehajtása és az eredmények lekérése

```java
// Get result object
RecognitionResult result = null;
try {
    result = api.RecognizePage(file, settings);
} catch (IOException e) {
    e.printStackTrace();
}
```

A `RecognizePage` hívás elindítja az OCR motorját a megadott képpel és beállításokkal. Az eredmény egy `RecognitionResult` objektumban tárolódik.

### 6. lépés: Eredmények kiírása és felhasználása

```java
// Print result
System.out.println("Result: \n" + result.recognitionText + "\n\n");
for (String n : result.recognitionAreasText) {
    System.out.println(n);
}
for (Rectangle n : result.recognitionAreasRectangles) {
    System.out.println(n.height + ":" + n.width + ":" + n.x + ":" + n.y);
}
System.out.println("\nJSON:" + result.GetJson());
System.out.println("Angle:" + result.skew);
for (String n : result.warnings) {
    System.out.println(n);
}

System.out.println("OCROperationWithLanguageSelection: execution complete");
```

A konzol kimenete a következőket mutatja:

- A teljes kinyert szöveg (`recognitionText`).  
- Az egyes téglalapokhoz tartozó szöveg (`recognitionAreasText`).  
- A határoló téglalap koordinátái.  
- Egy JSON ábrázolás a könnyű további feldolgozáshoz.  
- A detektált dőlésszög és esetleges figyelmeztetések.

Most már a `result.recognitionText`‑et beillesztheti az üzleti logikájába – tárolhatja, indexelheti vagy továbbíthatja egy másik szolgáltatásnak.

## Gyakori problémák és megoldások

| Probléma | Ok | Megoldás |
|----------|----|----------|
| **Garbage characters** | Wrong language selected | Set the correct `Language` enum (e.g., `Language.Fra` for French). |
| **No text returned** | Recognition area does not cover the text | Adjust the `Rectangle` coordinates or remove `RecognitionAreas` to process the whole image. |
| **Slow performance** | Very large image or high resolution | Downscale the image before OCR or increase memory allocation for the JVM. |
| **Warnings about unsupported format** | Image format not recognized | Convert the image to PNG, JPEG, or TIFF before processing. |

## GyIK

**Q: Felismerhetek több nyelvet egyetlen OCR hívásban?**  
A: Igen. Használja a `settings.setLanguage(Language.Eng | Language.Fra)` kifejezést a többnyelvű felismerés engedélyezéséhez.

**Q: Milyen képformátumokat támogat az Aspose.OCR?**  
A: PNG, JPEG, BMP, TIFF, GIF és több más formátum. Csak adja meg a helyes fájlútvonalat.

**Q: Van méretkorlátja a képnek?**  
A: Nincs szigorú korlát, de nagyon nagy képek növelik a memóriahasználatot és a feldolgozási időt. Fontolja meg a nagy fájlok átméretezését.

**Q: Hogyan szerezzek be egy éles licencet?**  
A: Vásároljon licencet az Aspose weboldaláról, és alkalmazza a `License` osztályon keresztül, ahogy az Aspose dokumentációjában szerepel.

**Q: Kinyerhetek szöveget közvetlenül egy PDF oldalról?**  
A: Nem közvetlenül az Aspose.OCR-rel. Először konvertálja a PDF oldalt képpé (például az Aspose.PDF használatával), majd futtassa az OCR‑t.

## Következtetés

Most már látta, hogyan **szöveget nyerhet ki képből** az Aspose.OCR for Java segítségével, miközben a megfelelő nyelvet választja ki és a felismerést meghatározott régiókra korlátozza. Ez a megközelítés pontos, nagy teljesítményű OCR‑t biztosít, amely beágyazható bármely Java‑alapú munkafolyamatba – legyen szó dokumentumkezelő rendszerekről vagy adatgyűjtő csővezetékekről. Készen áll a továbblépésre? Próbálja ki a nyelv‑enum cseréjét, kísérletezzen különböző felismerési területekkel, és integrálja az eredményeket saját alkalmazáslogikájába.

---

**Last Updated:** 2026-02-12  
**Tested With:** Aspose.OCR 24.11 for Java  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}