---
title: Készítsen téglalapokat az OCR képfelismerésben
linktitle: Készítsen téglalapokat az OCR képfelismerésben
second_title: Aspose.OCR .NET API
description: Kibontakoztatja az Aspose.OCR-ben rejlő lehetőségeket .NET-hez átfogó útmutatónkkal. Ismerje meg lépésről lépésre, hogyan készítsen elő téglalapokat a képfelismeréshez. Emelje fel .NET-alkalmazásait a zökkenőmentes OCR-integrációval.
type: docs
weight: 11
url: /hu/net/ocr-optimization/prepare-rectangles/
---
## Bevezetés

A technológia folyamatosan fejlődő világában az Optical Character Recognition (OCR) kulcsszerepet játszik a képek géppel olvasható szöveggé alakításában. Az Aspose.OCR for .NET robusztus megoldás a fejlesztők számára, akik az OCR-képességeket .NET-alkalmazásaikba zökkenőmentesen integrálják. Ebben az átfogó útmutatóban megvizsgáljuk a téglalapok OCR-képfelismerésben az Aspose.OCR for .NET használatával történő elkészítésének folyamatát.

## Előfeltételek

Mielőtt belevágna az oktatóanyagba, győződjön meg arról, hogy a következő előfeltételek teljesülnek:

- .NET fejlesztési ismeretek.
-  Aspose.OCR for .NET könyvtár telepítve. Letöltheti[itt](https://releases.aspose.com/ocr/net/).
- A képfelismerési fogalmak alapvető ismerete.

## Névterek importálása

Kezdjük a szükséges névterek importálásával OCR-útvonalunk elindításához:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## 1. lépés: Állítsa be a dokumentumkönyvtárat

 Először adja meg a könyvtárat, ahol a dokumentumokat tárolja. Cserélje ki`"Your Document Directory"` a dokumentumok tényleges elérési útjával.

```csharp
// A dokumentumok könyvtárának elérési útja.
string dataDir = "Your Document Directory";

// Inicializálja az AsposeOcr egy példányát
AsposeOcr api = new AsposeOcr();
```

## 2. lépés: Több téglalappal rendelkező kép felismerése

Ebben a lépésben bemutatjuk, hogyan lehet szöveget felismerni egy képről több téglalap használatával. Kövesse az alábbi allépéseket:

### 2.1 Téglalapok meghatározása

```csharp
List<Rectangle> rects = new List<Rectangle>()
{
    new Rectangle(138, 352, 2033, 537),
    new Rectangle(147, 890, 2033, 1157),
    new Rectangle(923, 2045, 465, 102),
    new Rectangle(104, 2147, 2076, 819)
};
```

### 2.2 Hajtsa végre az OCR felismerést

```csharp
// első eset
List<string> listResult = api.RecognizeImage(dataDir + "sample.png", rects);

// Jelenítse meg a felismert szöveget
foreach (string s in listResult)
{
    Console.WriteLine(s);
}
```

## 3. lépés: Kép felismerése a felismerési beállításokkal

Ebben a lépésben egy alternatív módszert mutatunk be a RecognitionSettings segítségével a képfelismeréshez:

### 3.1 Felismerési beállítások megadása

```csharp
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings
{
    RecognitionAreas = rects
});
```

### 3.2 Felismert szöveg megjelenítése

```csharp
// Jelenítse meg a felismert szöveget
foreach (string s in result.RecognitionAreasText)
{
    Console.WriteLine(s);
}
```

## Következtetés

Gratulálunk! Sikeresen navigált a téglalapok előkészítési folyamatában az OCR képfelismerésben az Aspose.OCR for .NET használatával. Ez az útmutató lehetővé teszi, hogy az OCR-t zökkenőmentesen integrálja .NET-alkalmazásaiba, javítva azok szövegfelismerési képességeit.

### GYIK

### 1. kérdés: Használhatom az Aspose.OCR-t .NET-hez más .NET-keretrendszerekkel?

1. válasz: Igen, az Aspose.OCR for .NET kompatibilis a különböző .NET-keretrendszerekkel.

### 2. kérdés: Elérhető ingyenes próbaverzió az Aspose.OCR for .NET számára?

 A2: Abszolút! Hozzáférhet az ingyenes próbaverzióhoz[itt](https://releases.aspose.com/).

### 3. kérdés: Hogyan kaphatok támogatást az Aspose.OCR for .NET-hez?

 A3: Látogassa meg a[Aspose.OCR fórum](https://forum.aspose.com/c/ocr/16) dedikált támogatásért.

### 4. kérdés: Kaphatok ideiglenes licencet tesztelési célokra?

 V4: Igen, szerezhet ideiglenes engedélyt[itt](https://purchase.aspose.com/temporary-license/).

### 5. kérdés: Hol találom az Aspose.OCR for .NET dokumentációját?

 V5: A dokumentáció elérhető[itt](https://reference.aspose.com/ocr/net/).