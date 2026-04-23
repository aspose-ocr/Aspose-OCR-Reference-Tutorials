---
date: 2026-02-22
description: Tanulja meg, hogyan végezhet el elrendezés-elemzést OCR-rel, felismerve
  a szövegsorokat egy képen, és kinyerve a sorok téglalapjait az Aspose.OCR for .NET
  használatával.
linktitle: Layout Analysis OCR – Get Line Rectangles from Images
second_title: Aspose.OCR .NET API
title: Elrendezés-elemzés OCR – Sorok téglalapjainak kinyerése képekből
url: /hu/net/image-and-drawing-recognition/get-rectangles-for-lines/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Layout Analysis OCR – Sorok téglalapjainak lekérése képekből

## Bevezetés

Ebben az útmutatóban megtudja, **hogyan lehet OCR sorok téglalapjait** lekérni az Aspose.OCR for .NET segítségével. A útmutató végére képes lesz **szövegsorok felismerésére egy képen** és **sorkoordináták kinyerésére** minden észlelt sorhoz – tökéletes a további feldolgozáshoz, például **layout analysis OCR**, adatkinyerés vagy egyedi megjelenítés.

## Gyors válaszok
- **Mi jelentése a „get OCR line rectangles” kifejezésnek?** Visszaadja minden egyes képen észlelt szövegsor határoló téglalapját.  
- **Melyik API metódust használja?** `AsposeOcr.GetRectangles(..., AreasType.LINES, ...)`.  
- **Szükségem van licencre?** Egy ingyenes próba verzió fejlesztéshez működik; a termeléshez kereskedelmi licenc szükséges.  
- **Támogatott képformátumok?** PNG, JPEG, BMP, TIFF és továbbiak.  
- **Futtatható .NET Core-on?** Igen, az Aspose.OCR teljes mértékben támogatja a .NET Core-ot és a .NET 5/6-ot.

## Előfeltételek

Mielőtt belemerülne az útmutatóba, győződjön meg róla, hogy az alábbi előfeltételek rendelkezésre állnak:

- Alapvető C# és .NET fejlesztési ismeretek.  
- Integrált fejlesztőkörnyezet (IDE), például a Visual Studio.  
- Az Aspose.OCR for .NET könyvtár telepítve van. Letöltheti [itt](https://releases.aspose.com/ocr/net/).  
- Egy minta kép, amely szöveget tartalmaz az OCR felismeréshez.

## Névterek importálása

Győződjön meg róla, hogy a szükséges névterek importálva vannak a projektbe. Adja hozzá a következő sorokat a C# fájl tetejéhez:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

Most bontsuk le a sorok téglalapjainak lekérésének folyamatát az OCR képfelismerésben könnyen követhető lépésekre.

## layout analysis ocr – Lépésről‑lépésre útmutató

### 1. lépés: Dokumentum könyvtár beállítása

```csharp
// ExStart:3
string dataDir = "Your Document Directory";
// ExEnd:3
```

Cserélje le a `"Your Document Directory"` értéket a minta képet tartalmazó mappa tényleges útvonalára.

### 2. lépés: Aspose.OCR inicializálása

```csharp
// ExStart:4
AsposeOcr api = new AsposeOcr();
// ExEnd:4
```

Hozzon létre egy `AsposeOcr` osztálypéldányt az OCR funkció eléréséhez.

### 3. lépés: Kép útvonalának megadása

```csharp
// ExStart:5
string fullPath = dataDir + "sample.png";
// ExEnd:5
```

Adja meg a teljes útvonalat ahhoz a képhez, amelyen OCR-t szeretne végrehajtani.

### 4. lépés: Kép felismerése és téglalapok lekérése

```csharp
// ExStart:6
List<Rectangle> lines = api.GetRectangles(fullPath, AreasType.LINES, false);
// ExEnd:6
```

A `GetRectangles` metódus egy `Rectangle` objektumok listáját adja vissza, amelyek mindegyike egy észlelt szövegsor koordinátáit tartalmazzák. Ez a **OCR sorok téglalapjainak lekérése** magja, és lehetővé teszi a **layout analysis OCR**-t.

### 5. lépés: Eredmény kiírása

```csharp
// ExStart:7
Console.WriteLine("Areas coordinates:");
lines.ForEach(a => Console.WriteLine($"x:{a.X} y:{a.Y} width:{a.Width} height:{a.Height}"));
// ExEnd:7
```

Írja ki a felismert területek koordinátáit a konzolra. Olyan értékeket fog látni, amelyeket később a **sorkoordináták kinyerésére** használhat egyedi feldolgozáshoz.

## Miért használja az Aspose.OCR-t sorok téglalapjaihoz?

- **Magas pontosság** – Fejlett algoritmusok még zajos vagy ferde képeken is felismerik a sorokat.  
- **Kereszt‑platform** – Működik .NET Framework, .NET Core és .NET 5/6 környezetben.  
- **Nincs külső függőség** – Tiszta .NET könyvtár, nincs szállítandó natív DLL.  
- **Gazdag kimenet** – A sorok téglalapjai mellett szavakat, karaktereket és biztonsági pontszámokat is lekérhet.

## Gyakori problémák és megoldások

| Probléma | Megoldás |
|----------|----------|
| **Nem tér vissza téglalap** | Győződjön meg róla, hogy a kép tiszta, vízszintes szöveget tartalmaz, és hogy a `AreasType.LINES` van megadva. |
| **Helytelen koordináták** | Ellenőrizze a kép DPI-jét; alacsony felbontású képek pontatlan határokat eredményezhetnek. |
| **Teljesítménybeli szűk keresztmetszet nagy képeknél** | Méretezze át a képet egy ésszerű felbontásra a `GetRectangles` hívása előtt. |
| **Licenc kivétel** | Használjon próba licencet teszteléshez; alkalmazzon teljes licencet a termeléshez, hogy elkerülje a kiértékelési korlátokat. |

## Gyakran Ismételt Kérdések

**K: Kinyerhetek egyedi szavakat a teljes sorok helyett?**  
V: Igen, használja a `AreasType.WORDS`-t ugyanazzal a `GetRectangles` metódussal a szavak szintű határoló téglalapokhoz.

**K: Támogatja az API a többoldalas PDF-eket?**  
V: Először konvertálja minden PDF oldalt képpé, majd hívja meg a `GetRectangles`-t minden képen.

**K: Hogyan kezeljem a elfordított szöveget?**  
V: Engedélyezze az automatikus forgatás opciót az OCR beállításokban, vagy előre forgassa el a képet a feldolgozás előtt.

**K: Van mód a biztonsági pontszámok lekérésére minden sorhoz?**  
V: A téglalapok lekérése után hívja meg a `api.RecognizeImage(...).Lines`-t, hogy hozzáférjen a sorobjektumokhoz, amelyek tartalmazzák a biztonsági értékeket.

**K: Mely .NET verziók kompatibilisek?**  
V: A könyvtár működik .NET Framework 4.5+, .NET Core 3.1+, és .NET 5/6 verziókkal.

## Valós példák

- **Dokumentum layout analysis OCR** – Adja a sorok téglalapjait egy layout motorba az oszlopstruktúrák újraépítéséhez.  
- **Automatizált adatkinyerés** – Használja a koordinátákat egyes sorok kivágásához a további NLP folyamatokhoz.  
- **Egyedi megjelenítés** – Helyezzen rá határoló téglalapokat az eredeti képre vizuális ellenőrzés vagy UI rétegek céljából.  

## Következtetés

Gratulálunk! Sikeresen **lekérte az OCR sorok téglalapjait** egy képre az Aspose.OCR for .NET használatával. A határoló téglalapok birtokában most már a sorkoordinátákat beillesztheti a további munkafolyamatokba, például egyedi megjelenítés, adatkinyerés vagy **layout analysis OCR**.

---

**Last Updated:** 2026-02-22  
**Tested With:** Aspose.OCR 24.11 for .NET  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}