---
date: 2025-12-17
description: Tanulja meg, hogyan lehet téglalapokat kinyerni a bekezdésekhez OCR‑képeken
  az Aspose.OCR for .NET használatával – a legfontosabb útmutató a téglalapok és a
  bekezdéskoordináták kinyeréséhez.
linktitle: Get Rectangles for Paragraphs in OCR Image Recognition
second_title: Aspose.OCR .NET API
title: Hogyan vonjunk ki téglalapokat a bekezdésekhez OCR képfelismerésben
url: /hu/net/image-and-drawing-recognition/get-rectangles-for-paragraphs/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan vonjunk ki téglalapokat a bekezdésekhez OCR képfelismerésben

## Bevezetés

Üdvözöljük átfogó útmutatónkban, amely **hogyan vonjunk ki téglalapokat** a bekezdésekhez OCR képfelismerésben az Aspose.OCR for .NET segítségével. Ha a dokumentumfeldolgozó folyamatát szeretné fejleszteni, bekezdéshatárokat kinyerni, és az adatkinyerést automatizálni, jó helyen jár. Lépésről lépésre végigvezetjük a beállítástól a téglalap koordináták kiírásáig, hogy azonnal használni tudja az OCR eredményeket.

## Gyors válaszok
- **Mit jelent a „téglalapok kinyerése”?** A detektált szövegtartományok határoló dobozait (x, y, szélesség, magasság) adja vissza.  
- **Melyik API metódus biztosítja a téglalapokat?** `AsposeOcr.GetRectangles` a `AreasType.PARAGRAPHS` paraméterrel.  
- **Szükség van licencre fejlesztéshez?** Ingyenes próba verzió teszteléshez elegendő; a termeléshez kereskedelmi licenc szükséges.  
- **Feldolgozhatok több képet egyszerre?** Igen – iteráljon a képlistán, és hívja meg a `GetRectangles` metódust minden fájlra.  
- **Mely formátumok támogatottak?** PNG, JPEG, TIFF, BMP és még sok más.

## Mi az a „téglalapok kinyerése” az OCR-ben?
Az OCR terminológiában a téglalapok kinyerése azt jelenti, hogy meghatározzuk a geometriai határokat, amelyek minden bekezdést vagy szövegsort körülölelnek egy képen. Ezek a koordináták lehetővé teszik a kiemelést, kivágást vagy a beolvasott dokumentum adott szakaszainak további elemzését.

## Miért érdemes bekezdéskoordinátákat kinyerni?
- **Pontos utófeldolgozás** – minden téglalapot átadhat a további munkafolyamatoknak (pl. fordítás, elhomályosítás).  
- **Javított UI/UX** – a határoló dobozok megjelenítése az eredeti képen segíti a felhasználókat a szöveg helyének megértésében.  
- **Kötegelt automatizálás** – gyorsan megtalálja és elkülöníti a bekezdéseket nagy dokumentumkészletekben.

## Előfeltételek

- Alapvető C# és .NET fejlesztési ismeretek.  
- Aspose.OCR for .NET telepítve a fejlesztői környezetben – letöltheti [itt](https://releases.aspose.com/ocr/net/).  
- Ismeretek a képfeldolgozás alapjairól és arról, miért fontos az OCR a beolvasott fájlok szövegének kinyeréséhez.

## Névtér importálása

A C# fájlban importálja a szükséges névtereket, hogy az OCR osztályok elérhetők legyenek:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## 1. lépés: Dokumentumkönyvtár beállítása

Adja meg azt a mappát, amely a feldolgozni kívánt képeket tartalmazza:

```csharp
string dataDir = "Your Document Directory";
```

## 2. lépés: AsposeOcr példány inicializálása

Hozzon létre egy `AsposeOcr` objektumot – ez biztosítja az összes OCR funkció elérését:

```csharp
AsposeOcr api = new AsposeOcr();
```

## 3. lépés: Képfájl útvonalának megadása

Mutassa meg a pontos képfájlt, amelyet feldolgozni szeretne:

```csharp
string fullPath = dataDir + "sample.png";
```

## 4. lépés: Kép felismertetése és bekezdés téglalapok lekérése

Hívja meg a `GetRectangles` metódust. A `detect_areas` `true` értékre állítása azt mondja a motornak, hogy **bekezdés** téglalapokat adjon vissza:

```csharp
List<Rectangle> rectangles = api.GetRectangles(fullPath, AreasType.PARAGRAPHS, true);
```

## 5. lépés: Eredmények kiírása

Írja ki a koordinátákat, hogy láthassa a **bekezdés koordináták kinyerését**, amelyeket a rendszer detektált:

```csharp
Console.WriteLine("Areas coordinates:");
rectangles.ForEach(a => Console.WriteLine($"x:{a.X} y:{a.Y} width:{a.Width} height:{a.Height}"));
```

## Gyakori problémák és megoldások

| Probléma | Ok | Megoldás |
|----------|----|----------|
| Nem tér vissza téglalap | A kép minősége túl alacsony vagy rossz `AreasType` | Győződjön meg róla, hogy a kép tiszta, és használja a `AreasType.PARAGRAPHS` értéket. |
| A koordináták egy egységgel eltolódnak | DPI skálázási eltérés | Állítsa be a megfelelő DPI‑t a kép betöltésekor, vagy használja az `api.Config.Dpi` beállítást. |
| Licenc kivétel | Érvénytelen vagy hiányzó licenc a termelésben | Alkalmazzon ideiglenes vagy végleges licencet a `api.SetLicense` metódussal. |

## Gyakran ismételt kérdések

**Q: Az Aspose.OCR kompatibilis különböző képformátumokkal?**  
A: Igen, az Aspose.OCR támogatja a PNG, JPEG, TIFF, BMP és számos más gyakori formátumot.

**Q: Használhatom az Aspose.OCR‑t kötegelt feldolgozáshoz több képen?**  
A: Természetesen! Iteráljon egy fájlútvonal‑gyűjteményen, és hívja meg a `GetRectangles` metódust minden képre.

**Q: Elérhető ingyenes próba a Aspose.OCR for .NET‑hez?**  
A: Igen, egy ingyenes próbaverziót felfedezhet [itt](https://releases.aspose.com/).

**Q: Hogyan szerezhetek ideiglenes licencet az Aspose.OCR‑hez?**  
A: Ideiglenes licencet kaphat [itt](https://purchase.aspose.com/temporary-license/).

**Q: Hol találok további támogatást és megbeszéléseket az Aspose.OCR‑rel kapcsolatban?**  
A: Látogasson el az [Aspose.OCR fórumra](https://forum.aspose.com/c/ocr/16) a közösségi támogatásért és megbeszélésekért.

## Összegzés

Ebben a bemutatóban **hogyan vonjunk ki téglalapokat** a bekezdésekhez az Aspose.OCR for .NET segítségével, áttekintettük minden kódrészletet, és elmagyaráztuk, hogyan értelmezze a visszakapott koordinátákat. Ezeknek a lépéseknek az alkalmazásba való beépítésével megbízhatóan kinyerheti a bekezdéshatárokat, javíthatja a dokumentumfolyamatokat, és intelligensebb OCR‑alapú megoldásokat építhet.

---

**Legutóbb frissítve:** 2025-12-17  
**Tesztelve:** Aspose.OCR 24.11 for .NET  
**Szerző:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}