---
title: Szerezzen be téglalapokat a bekezdésekhez az OCR képfelismerésben
linktitle: Szerezzen be téglalapokat a bekezdésekhez az OCR képfelismerésben
second_title: Aspose.OCR .NET API
description: Fedezze fel a fejlett OCR-képességeket az Aspose.OCR for .NET segítségével. Könnyedén kivonhatja a bekezdés téglalapjait.
type: docs
weight: 11
url: /hu/net/image-and-drawing-recognition/get-rectangles-for-paragraphs/
---
## Bevezetés

Üdvözöljük átfogó útmutatónkban az Aspose.OCR for .NET kihasználásáról a bekezdés-téglalapok OCR képfelismerésben történő kinyeréséhez. Ha fejleszteni szeretné dokumentumfeldolgozási képességeit, és ki szeretné használni az optikai karakterfelismerés (OCR) erejét .NET-alkalmazásaiban, akkor jó helyen jár.

## Előfeltételek

Mielőtt belevágnánk az oktatóanyagba, győződjön meg arról, hogy a következő előfeltételek teljesülnek:

- C# és .NET fejlesztési alapismeretek.
-  Az Aspose.OCR-rel beállított fejlesztői környezet .NET-hez. Ha még nem tette meg, letöltheti[itt](https://releases.aspose.com/ocr/net/).
- A képfeldolgozási fogalmak megértése és az OCR fontossága a szöveg képekből történő kinyerésében.

## Névterek importálása

Győződjön meg arról, hogy a C#-kódban importálta a szükséges névtereket az Aspose.OCR hatékony használatához. Tegye fel a következőket a fájl tetejére:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## 1. lépés: Állítsa be a dokumentumkönyvtárat

Kezdje azzal, hogy inicializálja a dokumentumkönyvtár elérési útját, ahol az OCR-feldolgozáshoz szükséges képeket tárolják:

```csharp
string dataDir = "Your Document Directory";
```

## 2. lépés: Inicializálja az AsposeOcr példányt

Hozzon létre egy példányt az AsposeOcr osztályból, hogy hozzáférjen az OCR funkciókhoz:

```csharp
AsposeOcr api = new AsposeOcr();
```

## 3. lépés: Adja meg a kép elérési útját

Határozza meg a feldolgozni kívánt kép teljes elérési útját:

```csharp
string fullPath = dataDir + "sample.png";
```

## 4. lépés: Kép felismerése és bekezdéstéglalapok lekérése

 Hívja fel a`GetRectangles` módszer téglalapok létrehozására az OCR kép bekezdéseihez. Készlet`detect_areas` nak nek`true` Ha bekezdéseket szeretne kivonatolni:

```csharp
List<Rectangle> rectangles = api.GetRectangles(fullPath, AreasType.PARAGRAPHS, true);
```

## 5. lépés: Eredmények nyomtatása

Nyomtassa ki az azonosított területek koordinátáit:

```csharp
Console.WriteLine("Areas coordinates:");
rectangles.ForEach(a => Console.WriteLine($"x:{a.X} y:{a.Y} width:{a.Width} height:{a.Height}"));
```

## 6. lépés: Következtetés

Gratulálunk! Sikeresen végrehajtotta az OCR képfelismerési folyamatot, hogy téglalapokat kapjon a bekezdésekhez az Aspose.OCR for .NET használatával.

## Következtetés

Ebben az oktatóanyagban megvizsgáltuk az Aspose.OCR for .NET alkalmazásba való integrálásának alapvető lépéseit, lehetővé téve, hogy bekezdés-téglalapokat vonjon ki az OCR-feldolgozott képekből. Az Aspose.OCR leegyszerűsíti az OCR megvalósítását, így a dokumentumfeldolgozás és a szövegkivonás értékes eszközévé válik.

## GYIK

### 1. kérdés: Az Aspose.OCR kompatibilis a különböző képformátumokkal?

1. válasz: Igen, az Aspose.OCR különféle képformátumokat támogat, beleértve a PNG-t, JPEG-et és TIFF-et.

### 2. kérdés: Használhatom az Aspose.OCR-t több kép kötegelt feldolgozására?

A2: Abszolút! Az Aspose.OCR megkönnyíti a kötegelt feldolgozást több kép zökkenőmentes kezeléséhez.

### 3. kérdés: Elérhető ingyenes próbaverzió az Aspose.OCR for .NET számára?

 3. válasz: Igen, felfedezheti az ingyenes próbaverziót[itt](https://releases.aspose.com/).

### 4. kérdés: Hogyan szerezhetek ideiglenes licencet az Aspose.OCR számára?

 V4: Kaphat ideiglenes engedélyt[itt](https://purchase.aspose.com/temporary-license/).

### 5. kérdés: Hol találhatok további támogatást és megbeszéléseket az Aspose.OCR-rel kapcsolatban?

 A5: Menjen át a[Aspose.OCR fórum](https://forum.aspose.com/c/ocr/16) közösségi támogatásra és beszélgetésekre.