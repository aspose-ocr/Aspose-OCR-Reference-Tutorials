---
date: 2025-12-09
description: Tanulja meg, hogyan lehet szöveget kinyerni képekből az Aspose.OCR for
  Java használatával, és megadni az engedélyezett karaktereket – egy teljes Aspose
  OCR Java útmutató.
linktitle: Specifying Allowed Characters in Aspose.OCR
second_title: Aspose.OCR Java API
title: Szöveg kinyerése képekből az Aspose.OCR segítségével – Engedélyezett karakterek
url: /hu/java/advanced-ocr-techniques/specify-allowed-characters/
weight: 15
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Képek szövegének kinyerése az Aspose.OCR segítségével – Engedélyezett karakterek

## Bevezetés

A képekből történő szövegkinyerés gyakori igény a modern alkalmazásokban – legyen szó számlák feldolgozásáról, nyugták beolvasásáról vagy nyomtatott dokumentumok digitalizálásáról. **Aspose.OCR for Java** egyszerűvé teszi ezt a feladatot, magas pontosságú felismerést és rugalmas konfigurációs lehetőségeket kínál, például az engedélyezett karakterek megadását. Ebben az útmutatóban egy teljes **aspose ocr java tutorial**-t mutatunk be, amely lépésről‑lépésre bemutatja a könyvtár beállítását, az OCR futtatását és a karakterkészlet korlátozását az Ön igényei szerint.

## Gyors válaszok
- **Mi a feladata az Aspose.OCR-nak?** Képekből szöveget nyer ki magas pontossággal, és támogatja az egyedi karakterkészleteket.  
- **Szükségem van licencre?** Ideiglenes vagy állandó licenc szükséges a termelési használathoz.  
- **Melyik JDK verzió támogatott?** A legújabb JDK kiadások teljesen kompatibilisek.  
- **Korlátozhatom a felismert karaktereket?** Igen – használja az allowed‑characters API-t a kimenet korlátozásához.  
- **Mennyi időt vesz igénybe a beállítás?** Körülbelül 10‑15 perc egy alapvető megvalósításhoz.

## Mi az a „szöveg kinyerése képekből”?
A képekből történő szövegkinyerés a vizuális szöveg (például nyomtatott vagy kézírásos) géppel olvasható karakterláncokká alakításának folyamata. Ez lehetővé teszi az olyan további feladatokat, mint a keresés, indexelés vagy adat-elemzés.

## Miért használjuk az Aspose.OCR-t Java-hoz?
- **Magas pontosság** több nyelven és betűtípuson.  
- **Egyszerű API**, amely bármely Java projekttel integrálható.  
- **Testreszabható** karakterkészletek, nyelvi csomagok és képelőfeldolgozás.  
- **Nincs külső függőség** – a könyvtár önálló.

## Előkövetelmények

Mielőtt elkezdené, győződjön meg arról, hogy a következők rendelkezésre állnak:

### Java fejlesztői csomag (JDK)

Győződjön meg róla, hogy a legújabb Java Development Kit telepítve van a rendszerén. Letöltheti [innen](https://www.oracle.com/java/technologies/javase-downloads.html).

### Aspose.OCR for Java könyvtár

Töltse le és telepítse az Aspose.OCR for Java könyvtárat a [download link](https://releases.aspose.com/ocr/java/) segítségével.

### Aspose.OCR licenc

Az Aspose.OCR teljes potenciáljának kihasználásához szerezzen be érvényes licencet. Licencet kaphat [innen](https://purchase.aspose.com/buy), vagy egy [ideiglenes licencet](https://purchase.aspose.com/temporary-license/) próbaverzióra is igényelhet.

## Csomagok importálása

Miután az előkövetelmények készen állnak, importálja a szükséges csomagokat a Java projektjébe:

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.examples.Utils;

import java.io.IOException;
```

## Lépésről‑lépésre útmutató

### 1. lépés: Dokumentumkönyvtár beállítása

Határozzon meg egy mappát, ahol az OCR‑feldolgozott eredményeket tárolja. Ez az útvonal később a kép fájl megtalálásához lesz használva.

```java
String dataDir = "Your Document Directory";
```

### 2. lépés: Kép útvonalának megadása

Iránnyalja az API‑t a feldolgozni kívánt képre.

```java
String imagePath = dataDir + "0001460985.Jpeg";
```

### 3. lépés: Aspose.OCR példány létrehozása

Hozza létre az OCR motor példányát a licenckulcsával. A kulcs lehet ideiglenes vagy állandó licenc karakterlánc.

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

> **Pro tip:** Ha a kimenetet egy meghatározott karakterkészletre (például csak számokra) szeretné korlátozni, használja a `setAllowedCharacters` metódust az `AsposeOCR` példányon a `RecognizeLine` hívása előtt. Így a motor figyelmen kívül hagyja az előre definiált halmazon kívüli karaktereket.

## Gyakori problémák és megoldások

| Probléma | Ok | Megoldás |
|----------|----|----------|
| **Nincs kimenet vagy üres karakterlánc** | Helytelen képútvonal vagy nem támogatott képformátum | Ellenőrizze az `imagePath`‑t, és használjon támogatott formátumot (JPEG, PNG, BMP) |
| **Felismerési hibák** | Alacsony felbontású kép vagy zajos háttér | Előfeldolgozza a képet (növelje a kontrasztot, binarizálja) OCR előtt |
| **Licenc nem alkalmazva** | Hiányzó vagy érvénytelen licenckulcs | Győződjön meg róla, hogy a licenckulcs helyes, és a `AsposeOCR` konstruktorban van megadva |

## Gyakran Ismételt Kérdések

**K: Hogyan szerezhetek ideiglenes licencet az Aspose.OCR-hez?**  
V: Látogassa meg a [temporary license page](https://purchase.aspose.com/temporary-license/) oldalt, hogy próbaverzió licencet kérjen.

**K: Hol találok támogatást az Aspose.OCR-hez?**  
V: Csatlakozzon a közösséghez a [Aspose.OCR Forum](https://forum.aspose.com/c/ocr/16) oldalon segítségért és megbeszélésekért.

**K: Megadhatom az engedélyezett karaktereket az Aspose.OCR-ben?**  
V: Igen, a `setAllowedCharacters` API‑val testreszabhatja a karakterkészletet. Tekintse meg a hivatalos dokumentációt a részletekért.

**K: Az Aspose.OCR kompatibilis a legújabb JDK verziókkal?**  
V: Teljesen – az Aspose.OCR rendszeresen frissül, hogy kompatibilis legyen a legújabb Java kiadásokkal.

**K: Vannak további OCR funkciók a sorfelismerésen kívül?**  
V: Igen, a könyvtár támogatja a blokk, bekezdés és teljes oldal felismerését, valamint nyelvi csomagokat és képelőfeldolgozási lehetőségeket.

## Összegzés

Az **aspose ocr java tutorial** követésével most már működő megoldása van a **képek szövegének kinyerésére**, és szabályozhatja, hogy mely karakterek legyenek felismerve. Tekintse meg a teljes [documentation](https://reference.aspose.com/ocr/java/) oldalt, hogy felfedezze a fejlett funkciókat, például a többnyelvű támogatást, egyedi előfeldolgozást és kötegelt feldolgozást.

---

**Last Updated:** 2025-12-09  
**Tested With:** Aspose.OCR for Java 24.11  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}