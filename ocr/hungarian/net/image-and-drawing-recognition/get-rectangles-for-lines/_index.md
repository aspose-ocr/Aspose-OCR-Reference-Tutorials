---
date: 2025-12-17
description: Ismerje meg, hogyan lehet OCR sor téglalapokat lekérni az Aspose.OCR
  for .NET használatával, hogy könnyedén felismerje a képek szövegsorait és kinyerje
  a sorok koordinátáit.
linktitle: Get OCR Line Rectangles for Image Text Lines
second_title: Aspose.OCR .NET API
title: OCR sorok téglalapjainak lekérése a képen lévő szövegsorokhoz
url: /hu/net/image-and-drawing-recognition/get-rectangles-for-lines/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR sor téglalapok lekérése képen lévő szövegsorokhoz

## Bevezetés

Ebben az útmutatóban megtudja, **hogyan lehet OCR sor téglalapokat lekérni** az Aspose.OCR for .NET segítségével. A útmutató végére képes lesz **szövegsorok felismerésére egy képen** és **sor koordináták kinyerésére** minden észlelt sorhoz – tökéletes a további feldolgozáshoz, például elrendezés elemzéshez, adatkinyeréshez vagy egyedi rendereléshez.

## Gyors válaszok
- **Mi jelent a „get OCR line rectangles”?** Visszaadja minden egyes képen észlelt szövegsor határoló dobozát.  
- **Melyik API metódust használja?** `AsposeOcr.GetRectangles(..., AreasType.LINES, ...)`.  
- **Szükségem van licencre?** Egy ingyenes próba verzió fejlesztéshez működik; a termeléshez kereskedelmi licenc szükséges.  
- **Támogatott képfájl formátumok?** PNG, JPEG, BMP, TIFF és továbbiak.  
- **Futtatható .NET Core-on?** Igen, az Aspose.OCR teljes mértékben támogatja a .NET Core-ot és a .NET 5/6-ot.

## Előfeltételek

Mielőtt belemerülne az útmutatóba, győződjön meg arról, hogy a következő előfeltételek rendelkezésre állnak:

- Alapvető C# és .NET fejlesztési ismeretek.  
- Integrált fejlesztőkörnyezet (IDE), például a Visual Studio.  
- Az Aspose.OCR for .NET könyvtár telepítve. Letöltheti [itt](https://releases.aspose.com/ocr/net/).  
- Egy mintakép, amely szöveget tartalmaz az OCR felismeréshez.

## Névtér importálása

Győződjön meg arról, hogy a szükséges névterek importálva vannak a projektjébe. Adja hozzá a következő sorokat a C# fájlja tetejéhez:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

Most bontsuk le a sorokhoz tartozó téglalapok lekérésének folyamatát az OCR képfelismerésben könnyen követhető lépésekre.

## 1. lépés: Dokumentumkönyvtár beállítása

```csharp
// ExStart:3
string dataDir = "Your Document Directory";
// ExEnd:3
```

Cserélje le a `"Your Document Directory"`-t a minta képet tartalmazó mappa tényleges elérési útjára.

## 2. lépés: Aspose.OCR inicializálása

```csharp
// ExStart:4
AsposeOcr api = new AsposeOcr();
// ExEnd:4
```

Hozzon létre egy `AsposeOcr` osztálypéldányt az OCR funkció eléréséhez.

## 3. lépés: Kép útvonalának megadása

```csharp
// ExStart:5
string fullPath = dataDir + "sample.png";
// ExEnd:5
```

Adja meg a teljes elérési utat ahhoz a képhez, amelyen OCR-t szeretne végrehajtani.

## 4. lépés: Kép felismerése és téglalapok lekérése

```csharp
// ExStart:6
List<Rectangle> lines = api.GetRectangles(fullPath, AreasType.LINES, false);
// ExEnd:6
```

A `GetRectangles` metódus egy `Rectangle` objektumok listáját adja vissza, amelyek mindegyike egy észlelt szövegsor koordinátáit tartalmazzák. Ez a **OCR sor téglalapok lekérésének** központi része.

## 5. lépés: Eredmény kiírása

```csharp
// ExStart:7
Console.WriteLine("Areas coordinates:");
lines.ForEach(a => Console.WriteLine($"x:{a.X} y:{a.Y} width:{a.Width} height:{a.Height}"));
// ExEnd:7
```

Írja ki a detektált területek koordinátáit a konzolra. Olyan értékeket fog látni, amelyeket később **sor koordináták kinyerésére** használhat egyedi feldolgozáshoz.

## Miért használja az Aspose.OCR-t sor téglalapokhoz?

- **Magas pontosság** – Fejlett algoritmusok még zajos vagy ferde képeken is felismerik a sorokat.  
- **Keresztplatformos** – Működik .NET Framework, .NET Core és .NET 5/6 környezetben.  
- **Nincs külső függőség** – Tiszta .NET könyvtár, nincs szállítandó natív DLL.  
- **Gazdag kimenet** – A sor téglalapok mellett szavakat, karaktereket és bizalmi értékeket is lekérhet.

## Gyakori problémák és megoldások

| Probléma | Megoldás |
|----------|----------|
| **Nem tér vissza téglalap** | Győződjön meg arról, hogy a kép tiszta, vízszintes szöveget tartalmaz, és hogy a `AreasType.LINES` van megadva. |
| **Helytelen koordináták** | Ellenőrizze a kép DPI-jét; alacsony felbontású képek pontatlan határokat eredményezhetnek. |
| **Teljesítménybeli szűk keresztmetszet nagy képeknél** | Méretezzék át a képet egy ésszerű felbontásra a `GetRectangles` hívása előtt. |
| **Licenc kivétel** | Használjon próba licencet teszteléshez; alkalmazzon teljes licencet a termeléshez, hogy elkerülje a kiértékelési korlátokat. |

## GYIK

### Q1: Használhatom az Aspose.OCR for .NET-et bármilyen típusú képpel?

**A1:** Az Aspose.OCR számos képfájl formátumot támogat, így rugalmasan alkalmazható az OCR megoldásaiban.

### Q2: Mennyire pontos az OCR felismerés?

**A2:** Az Aspose.OCR fejlett algoritmusokat használ a magas pontosság érdekében, így különböző szövegfelismerési helyzetekben is megfelelő.

### Q3: Van ingyenes próba verzió?

**A3:** Igen, a [ingyenes próba](https://releases.aspose.com/) verzióval felfedezheti az Aspose.OCR for .NET képességeit.

### Q4: Hol találok részletes dokumentációt?

**A4:** Tekintse meg a [dokumentációt](https://reference.aspose.com/ocr/net/) a részletes információkért és használati útmutatóért.

### Q5: Szükségem van segítségre vagy konkrét kérdéseim vannak?

**A5:** Látogassa meg az [Aspose.OCR fórumot](https://forum.aspose.com/c/ocr/16) a közösségi támogatásért és megbeszélésekért.

## Gyakran Ismételt Kérdések

**Q: Kivonhatok egyedi szavakat a teljes sorok helyett?**  
A: Igen, használja a `AreasType.WORDS`-t ugyanazzal a `GetRectangles` metódussal a szó‑szintű határoló dobozok lekéréséhez.

**Q: Támogatja az API a többoldalas PDF-eket?**  
A: Először konvertálja minden PDF oldalt képpé, majd hívja meg a `GetRectangles`-t az egyes képeken.

**Q: Hogyan kezeljem a forgatott szöveget?**  
A: Engedélyezze az automatikus forgatás opciót az OCR beállításokban, vagy előre forgassa el a képet a feldolgozás előtt.

**Q: Van mód a bizalmi értékek lekérésére minden sorhoz?**  
A: A téglalapok lekérése után hívja meg a `api.RecognizeImage(...).Lines`-t, hogy hozzáférjen a sorobjektumokhoz, amelyek tartalmazzák a bizalmi értékeket.

**Q: Mely .NET verziók kompatibilisek?**  
A: A könyvtár működik .NET Framework 4.5+, .NET Core 3.1+, és .NET 5/6 verziókkal.

## Összegzés

Gratulálunk! Sikeresen **lekérte az OCR sor téglalapokat** egy képről az Aspose.OCR for .NET segítségével. A határoló dobozok birtokában most már a sor koordinátákat beillesztheti a további munkafolyamatokba, például egyedi rendereléshez, adatkinyeréshez vagy elrendezés elemzéshez.

---

**Utoljára frissítve:** 2025-12-17  
**Tesztelve a következővel:** Aspose.OCR 24.11 for .NET  
**Szerző:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}