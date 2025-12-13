---
date: 2025-12-13
description: Tanulja meg, hogyan lehet szöveget kinyerni képből az Aspose.OCR for
  Java segítségével nyelvválasztással. Ez a lépésről‑lépésre Aspose OCR Java útmutató
  pontos OCR konfigurációt mutat be.
linktitle: How to Extract Text from Image with Language Selection Using Aspose.OCR
second_title: Aspose.OCR Java API
title: Hogyan lehet szöveget kinyerni képből nyelvválasztással az Aspose.OCR segítségével
url: /hu/java/ocr-operations/perform-ocr-language-selection/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan vonjunk ki szöveget képből nyelvválasztással az Aspose.OCR használatával

## Bevezetés

A szöveg kinyerése képfájlokból gyakori igény, legyen szó beolvasott dokumentumok digitalizálásáról, nyugták feldolgozásáról vagy kereshető archívumok építéséről. Az Aspose.OCR for Java egyszerűvé teszi ezt a feladatot, és finomhangolt vezérlést biztosít a nyelvválasztás, a dőléskorrekció és a felismerési területek felett. Ebben az útmutatóban egy teljes, gyakorlati példán keresztül mutatjuk be, **hogyan vonjunk ki szöveget képből** egy adott nyelvi beállítással, hogy még ma megbízható OCR-t integrálhasson Java‑alkalmazásaiba.

## Gyors válaszok
- **Melyik könyvtár kezeli az OCR-t Java‑ban?** Aspose.OCR for Java  
- **Melyik beállítás választja ki a nyelvet?** `settings.setLanguage(Language.Eng)` (vagy bármely támogatott nyelv)  
- **Szükségem van licencre fejlesztéshez?** Egy ingyenes értékelő licenc működik teszteléshez; a termeléshez kereskedelmi licenc szükséges.  
- **Korlátozhatom az OCR‑t a kép egy régiójára?** Igen, használja a `RecognitionSettings.setRecognitionAreas()`‑t téglalapokkal.  
- **Mi a tipikus futási idő?** Néhány másodperc oldalanként egy átlagos laptopon, a kép méretétől és a nyelv összetettségétől függően.

## Mi az a „szöveg kinyerése képből”?
A képből történő szöveg kinyerése (OCR) a karakterek vizuális ábrázolását gép‑olvasható karakterláncokká alakítja. Ez lehetővé teszi a keresést, az elemzést és az adatkinyerési munkafolyamatokat, amelyek egyébként manuális átírást igényelnének.

## Miért használjuk az Aspose.OCR‑t nyelvválasztással?
- **Többnyelvű támogatás** – Válassza ki a képen jelen lévő pontos nyelvet vagy nyelveket a pontosság növelése érdekében.  
- **Finomhangolt vezérlés** – Állítsa be a dőlést, definiálja a felismerési területeket, és szabályozza az automatikus dőléskorrekciót.  
- **Tiszta Java API** – Nincsenek natív függőségek, könnyen integrálható bármely Java projektbe.  
- **Gazdag eredményadatok** – Egy hívással kapja meg a sima szöveget, JSON‑t, körülhatároló téglalapokat és figyelmeztetéseket.

## Előkövetelmények

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

Cserélje le a `"Your Document Directory"`‑t az abszolút útra, ahol a `p3.png` található.

### 2. lépés: Kép útvonalának meghatározása

```java
// The image path
String file = dataDir + "p3.png";
```

Győződjön meg róla, hogy a `file` változó a pontosan feldolgozni kívánt képre mutat.

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

1. Letiltjuk az automatikus dőléskorrekciót, mivel manuális dőlésszöget adunk meg.  
2. Meghatározunk egy téglalap alakú régiót (`RecognitionAreas`), hogy az OCR csak a tényleges szöveget tartalmazó képrészre korlátozódjon.  
3. Beállítjuk a **nyelvet** angolra (`Language.Eng`). Ezt módosítsa `Language.Fra`, `Language.Spa` stb.-re a forráskép nyelvétől függően.

### 5. lépés: OCR végrehajtása és eredmények lekérése

```java
// Get result object
RecognitionResult result = null;
try {
    result = api.RecognizePage(file, settings);
} catch (IOException e) {
    e.printStackTrace();
}
```

A `RecognizePage` hívás elindítja az OCR motorát a megadott képpel és beállításokkal. Az eredmény egy `RecognitionResult` objektumban tárolódik.

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
- Szöveg minden definiált téglalaphoz (`recognitionAreasText`).  
- Körülhatároló téglalap koordináták.  
- JSON ábrázolás az egyszerű további feldolgozáshoz.  
- Detektált dőlésszög és esetleges figyelmeztetések.

Most már a `result.recognitionText`‑et átadhatja az üzleti logikájának – tárolhatja, indexelheti vagy továbbíthatja egy másik szolgáltatásnak.

## Gyakori problémák és megoldások

| Probléma | Ok | Megoldás |
|----------|----|----------|
| **Rossz karakterek** | Helytelen nyelv kiválasztva | Állítsa be a megfelelő `Language` enum‑ot (pl. `Language.Fra` a francia nyelvhez). |
| **Nem tér vissza szöveg** | A felismerési terület nem fedi le a szöveget | Állítsa be a `Rectangle` koordinátákat, vagy távolítsa el a `RecognitionAreas`‑t a teljes kép feldolgozásához. |
| **Lassú teljesítmény** | Nagyon nagy kép vagy magas felbontás | Kicsinyítse a képet OCR előtt, vagy növelje a JVM memória kiosztását. |
| **Figyelmeztetések a nem támogatott formátumról** | A képformátum nem ismerhető | Konvertálja a képet PNG, JPEG vagy TIFF formátumba a feldolgozás előtt. |

## Gyakran Ismételt Kérdések

**K: Tudok több nyelvet felismerni egyetlen OCR hívásban?**  
A: Igen. Használja a `settings.setLanguage(Language.Eng | Language.Fra)`‑t a többnyelvű felismerés engedélyezéséhez.

**K: Mely képformátumokat támogatja az Aspose.OCR?**  
A: PNG, JPEG, BMP, TIFF, GIF és több más. Csak adja meg a helyes fájl útvonalat.

**K: Van méretkorlát a képre?**  
A: Nincs szigorú korlát, de a nagyon nagy képek növelik a memóriahasználatot és a feldolgozási időt. Fontolja meg a nagy fájlok átméretezését.

**K: Hogyan szerezzek termelési licencet?**  
A: Vásároljon licencet az Aspose weboldaláról, és alkalmazza a `License` osztályon keresztül, ahogy az Aspose dokumentációban látható.

**K: Kinyerhetek szöveget közvetlenül egy PDF oldalról?**  
A: Nem közvetlenül az Aspose.OCR‑rel. Először konvertálja a PDF oldalt képpé (pl. az Aspose.PDF használatával), majd futtassa az OCR‑t.

## Összegzés

Most már látta, hogyan **vonjon ki szöveget képből** az Aspose.OCR for Java segítségével, miközben a megfelelő nyelvet választja ki és a felismerést meghatározott régiókra korlátozza. Ez a megközelítés pontos, nagy teljesítményű OCR‑t biztosít, amely bármely Java‑alapú munkafolyamatba beágyazható – legyen szó dokumentumkezelő rendszerekről vagy adatgyűjtő csővezetékekről.

---

**Utoljára frissítve:** 2025-12-13  
**Tesztelve a következővel:** Aspose.OCR 24.11 for Java  
**Szerző:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}