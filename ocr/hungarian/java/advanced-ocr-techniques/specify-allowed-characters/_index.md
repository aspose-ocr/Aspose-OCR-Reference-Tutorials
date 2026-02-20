---
date: 2026-02-20
description: Tanulja meg, hogyan lehet szöveget kinyerni képekből az Aspose.OCR for
  Java segítségével, beállítani az engedélyezett karaktereket, és ideiglenes licencet
  alkalmazni – egy teljes Aspose OCR Java útmutató.
linktitle: Specifying Allowed Characters in Aspose.OCR
second_title: Aspose.OCR Java API
title: Szöveg kinyerése képekből az Aspose.OCR-rel – Engedélyezett karakterek
url: /hu/java/advanced-ocr-techniques/specify-allowed-characters/
weight: 15
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kép szövegének kinyerése az Aspose.OCR segítségével – Engedélyezett karakterek

## Bevezetés

A képekből történő szövegkinyerés gyakori követelmény a modern alkalmazásokban – legyen szó számlák feldolgozásáról, nyugták beolvasásáról vagy nyomtatott dokumentumok digitalizálásáról. Ebben az útmutatóban végigvezetünk egy teljes **aspose ocr java tutorial**-on, amely megmutatja, hogyan **extract text from images** az Aspose.OCR for Java segítségével, hogyan állítható be az engedélyezett karakterek listája, és hogyan alkalmazható egy ideiglenes licenc, ha csak a könyvtárat teszteli.

## Gyors válaszok
- **Mi a feladata az Aspose.OCR-nak?** Szöveget nyer ki a képekből magas pontossággal, és támogatja az egyedi karakterkészleteket.  
- **Szükségem van licencre?** Ideiglenes vagy állandó licenc szükséges a termelésben való használathoz.  
- **Mely JDK verzió támogatott?** A legújabb JDK kiadások teljesen kompatibilisek.  
- **Korlátozhatom a felismert karaktereket?** Igen – használja a `setAllowedCharacters` API-t a kimenet szűkítéséhez.  
- **Mennyi időt vesz igénybe a beállítás?** Körülbelül 10‑15 perc egy alapvető megvalósításhoz.

## Mi az a „szöveg kinyerése a képekből”?
A szöveg kinyerése a képekből a vizuális szöveg (például nyomtatott vagy kézírásos) géppel olvasható karakterláncokká alakításának folyamata. Ez lehetővé teszi az olyan későbbi feladatokat, mint a keresés, indexelés vagy adatelemzés.

## Miért használjuk az Aspose.OCR for Java-t?
- **Magas pontosság** több nyelven és betűtípuson.  
- **Egyszerű API**, amely bármely Java projektbe integrálható.  
- **Testreszabható** karakterkészletek, nyelvi csomagok és képelőfeldolgozás.  
- **Nincs külső függőség** – a könyvtár önálló.

## Előkövetelmények

Mielőtt elkezdené, győződjön meg róla, hogy a következőkkel rendelkezik:

### Java Development Kit (JDK)

Győződjön meg róla, hogy a legújabb Java Development Kit telepítve van a rendszerén. Letöltheti [innen](https://www.oracle.com/java/technologies/javase-downloads.html).

### Aspose.OCR for Java Library

Töltse le és telepítse az Aspose.OCR for Java könyvtárat a [letöltési hivatkozásról](https://releases.aspose.com/ocr/java/).

### Aspose.OCR License

Az Aspose.OCR teljes potenciáljának eléréséhez szerezzen be egy érvényes licencet. Szerezhet egyet [innen](https://purchase.aspose.com/buy), vagy tekintse meg a [temporary license](https://purchase.aspose.com/temporary-license/) lehetőséget egy próbaidőszakra.

## Ideiglenes licenc alkalmazása

A termék kiértékelésekor az ideiglenes licenc eltávolítja a kiértékelési vízjelet, és korlátozott időre teljes funkcionalitást biztosít. Hozza létre a licenc karakterláncot az Aspose portálon, majd adja át a `AsposeOCR` konstruktorának, ahogyan az alábbi kódrészletben látható. A termelési környezetben cserélje le az ideiglenes kulcsot a végleges licencére.

## OCR képelőfeldolgozási tippek

A jó képminőség jelentősen javítja a felismerési eredményeket. Az OCR motor meghívása előtt vegye figyelembe:

- A kép átalakítása szürkeárnyalatossá.  
- A kontraszt növelése a karakterek kiemeléséhez.  
- A háttérzaj eltávolítása binarizációs szűrővel.  
- Az alacsony felbontású képek átméretezése legalább 300 dpi-re.

Ezek a lépések a **ocr image preprocessing** részei, és bármely standard Java képkönyvtárral elvégezhetők az Aspose.OCR meghívása előtt.

## Csomagok importálása

Miután az előkövetelmények készen állnak, importálja a szükséges csomagokat a Java projektjébe:

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.examples.Utils;

import java.io.IOException;
```

## Lépésről‑lépésre útmutató

### 1. lépés: A dokumentum könyvtár beállítása

Határozzon meg egy mappát, ahol az OCR‑feldolgozott eredményeket tárolja. Ez az útvonal később a képfájl megtalálásához lesz használva.

```java
String dataDir = "Your Document Directory";
```

### 2. lépés: A kép útvonalának megadása

Mutassa meg az API-nak a feldolgozni kívánt képet.

```java
String imagePath = dataDir + "0001460985.Jpeg";
```

### 3. lépés: Aspose.OCR példány létrehozása

Példányosítsa az OCR motort a licenckulccsal. A kulcs lehet ideiglenes vagy állandó licenc karakterlánc.

```java
AsposeOCR api = new AsposeOCR("YourLicenseKey");
```

### 4. lépés: OCR felismerés végrehajtása

Hívja meg a `RecognizeLine` metódust, hogy egy sor szöveget nyerjen ki a képből. Az eredmény egy egyszerű karakterlánc, amelyet tovább feldolgozhat vagy tárolhat.

```java
try {
    String result = api.RecognizeLine(imagePath);
    System.out.println("File: " + imagePath);
    System.out.println("Result line: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

> **Pro tip:** Ha korlátozni szeretné a kimenetet egy meghatározott karakterkészletre (például csak számjegyek), használja a `setAllowedCharacters` metódust a `AsposeOCR` példányon a `RecognizeLine` meghívása előtt. Ez biztosítja, hogy a motor figyelmen kívül hagyja a meghatározott halmazon kívüli karaktereket.

## Gyakori problémák és megoldások

| Probléma | Ok | Megoldás |
|----------|----|----------|
| **Nincs kimenet vagy üres karakterlánc** | Helytelen képútvonal vagy nem támogatott képformátum | `imagePath` ellenőrzése és támogatott formátum (JPEG, PNG, BMP) használata |
| **Felismerési hibák** | Alacsony felbontású kép vagy zajos háttér | Előfeldolgozza a képet (kontraszt növelése, binarizálás) az OCR előtt |
| **Licenc nincs alkalmazva** | Hiányzó vagy érvénytelen licenckulcs | Győződjön meg róla, hogy a licenc karakterlánc helyes és a `AsposeOCR` konstruktorban van megadva |

## Gyakran ismételt kérdések

**K: Hogyan szerezhetek ideiglenes licencet az Aspose.OCR-hez?**  
V: Látogassa meg a [temporary license page](https://purchase.aspose.com/temporary-license/) oldalt, hogy próbaverzió licencet kérjen.

**K: Hol találok támogatást az Aspose.OCR-hez?**  
V: Csatlakozzon a közösséghez a [Aspose.OCR Forum](https://forum.aspose.com/c/ocr/16) oldalon segítségért és megbeszélésekért.

**K: Megadhatok engedélyezett karaktereket az Aspose.OCR-ben?**  
V: Igen, a `setAllowedCharacters` API-val testreszabhatja a karakterkészletet. Részletekért tekintse meg a hivatalos dokumentációt.

**K: Az Aspose.OCR kompatibilis a legújabb JDK verziókkal?**  
V: Teljesen – az Aspose.OCR rendszeresen frissül, hogy kompatibilis legyen a legújabb Java kiadásokkal.

**K: Vannak további OCR funkciók a sorfelismerésen kívül?**  
V: Igen, a könyvtár támogatja a blokk, bekezdés és teljes oldal felismerését, valamint nyelvi csomagokat és képelőfeldolgozási lehetőségeket.

## Összegzés

Az **aspose ocr java tutorial** követésével most már működő megoldással rendelkezik a **extract text from images** feladatra, és szabályozhatja, hogy mely karakterek legyenek felismert. Fedezze fel a teljes [documentation](https://reference.aspose.com/ocr/java/) oldalt a fejlett funkciók, például a többnyelvű támogatás, egyedi előfeldolgozás és kötegelt feldolgozás megismeréséhez.

---

**Utolsó frissítés:** 2026-02-20  
**Tesztelve:** Aspose.OCR for Java 24.11  
**Szerző:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}