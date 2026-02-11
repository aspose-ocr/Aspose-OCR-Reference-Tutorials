---
date: 2025-12-22
description: Ismerje meg, hogyan lehet szöveget kinyerni a képből az Aspose.OCR for
  .NET segítségével. Ez az útmutató végigvezet a téglalapok előkészítésén az OCR képfelismeréshez,
  és a pontosság növelésén.
linktitle: Prepare Rectangles in OCR Image Recognition
second_title: Aspose.OCR .NET API
title: Hogyan vonjunk ki szöveget a képből téglalapok előkészítésével az OCR-ben
url: /hu/net/ocr-optimization/prepare-rectangles/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Téglalapok előkészítése OCR képfelismeréshez

## Bevezetés

Az optikai karakterfelismerés (OCR) elengedhetetlen a vizuális tartalom kereshető, szerkeszthető szöveggé alakításához. Ebben az útmutatóban **kivonja a szöveget a képből** egyedi téglalapok előkészítésével, amelyek a OCR motorra a specifikus területekre fókuszálnak. Az Aspose.OCR for .NET használatával lépésről lépésre végigvezetünk – a projekt beállításától a felismert szöveg lekéréséig –, hogy erőteljes kép‑szöveg funkciót integrálhass a .NET alkalmazásaiba.

## Gyors válaszok
- **Mit jelent a „kivonja a szöveget a képből”?** Azt jelenti, hogy a képen lévő vizuális karaktereket gép‑olvasható karakterláncokká alakítja.  
- **Melyik könyvtár segít ebben .NET‑ben?** Aspose.OCR for .NET.  
- **Szükségem van licencre a fejlesztéshez?** Egy ingyenes próba verzió tesztelésre megfelelő; a termeléshez licenc szükséges.  
- **Célzhatok konkrét területeket?** Igen, téglalapok definiálásával, amelyek korlátozzák az OCR hatókörét.  
- **Mely .NET verziók támogatottak?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.

## Mi az a „kivonja a szöveget a képből” téglalapokkal?

Amikor téglalap alakú zónákat definiálsz egy képen, az OCR motor csak ezeket a zónákat dolgozza fel. Ez javítja a pontosságot, csökkenti a feldolgozási időt, és lehetővé teszi, hogy figyelmen kívül hagyd a zajos háttérképeket vagy a nem releváns részeket.

## Miért kell téglalapokat előkészíteni az OCR előtt?

- **A releváns tartalomra fókuszálás:** Fejlécek, láblécek vagy díszítő grafikák kihagyása.  
- **Teljesítmény növelése:** Kisebb területek gyorsabb felismerést jelentenek.  
- **Pontosság javítása:** Kevesebb vizuális zaj tisztább eredményeket hoz.

## Előfeltételek

- C# és .NET fejlesztés ismerete.  
- Aspose.OCR for .NET könyvtár telepítve – letöltheted **[itt](https://releases.aspose.com/ocr/net/)**.  
- Egy minta kép (pl. `sample.png`), amely tartalmazza a kivonni kívánt szöveget.

## Névtér importálása

Először hozd be a szükséges névtereket a láthatóságba:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## 1. lépés: Dokumentumkönyvtár beállítása

Add meg, hogy hol találhatók a képfájlok, és hozz létre egy OCR motor példányt.

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Hogyan vonjunk ki szöveget a képből több téglalap használatával

### 2. lépés: Kép felismerése több téglalappal

#### 2.1 Téglalapok definiálása

Hozz létre egy `Rectangle` objektumok listáját, amelyek meghatározzák a területeket, amelyeket az OCR motornak be kell olvasnia.

```csharp
List<Rectangle> rects = new List<Rectangle>()
{
    new Rectangle(138, 352, 2033, 537),
    new Rectangle(147, 890, 2033, 1157),
    new Rectangle(923, 2045, 465, 102),
    new Rectangle(104, 2147, 2076, 819)
};
```

#### 2.2 OCR felismerés végrehajtása

Add meg a kép útvonalát és a téglalap listát a `RecognizeImage` metódusnak. A metódus egy karakterláncok gyűjteményét adja vissza – minden bejegyzés egy téglalapnak felel meg.

```csharp
// first case
List<string> listResult = api.RecognizeImage(dataDir + "sample.png", rects);

// Display the recognized text
foreach (string s in listResult)
{
    Console.WriteLine(s);
}
```

### 3. lépés: Kép felismerése felismerési beállításokkal (alternatív megközelítés)

Ha inkább a `RecognitionSettings` használatát részesíted előnyben, ugyanazt az eredményt elérheted egy kissé eltérő API hívással.

#### 3.1 Felismerési beállítások definiálása

```csharp
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings
{
    RecognitionAreas = rects
});
```

#### 3.2 Felismert szöveg megjelenítése

```csharp
// Display the recognized text
foreach (string s in result.RecognitionAreasText)
{
    Console.WriteLine(s);
}
```

## Gyakori problémák és tippek

- **Helytelen téglalap koordináták:** Győződj meg arról, hogy az `X`, `Y`, `Width` és `Height` értékek helyesen térképezik a kívánt régiót.  
- **Képminőség:** Alacsony felbontású képek gyenge OCR eredményeket adhatnak; fontold meg az előfeldolgozást (pl. binarizálás).  
- **Üres eredmények:** Ellenőrizd, hogy a téglalapok valóban tartalmaznak szöveget; különben a motor üres karakterláncokat ad vissza.

## Következtetés

Most már megtanultad, hogyan **vonj ki szöveget a képből** egyedi téglalapok előkészítésével az Aspose.OCR for .NET segítségével. Ez a technika finomhangolt irányítást biztosít az OCR feldolgozás felett, segítve, hogy gyorsabb és pontosabb szöveg‑kivonási funkciókat építs alkalmazásaidba.

## Gyakran ismételt kérdések

**Q:** Használhatom az Aspose.OCR for .NET-et más .NET keretrendszerekkel?  
**A:** Igen, az Aspose.OCR for .NET kompatibilis különböző .NET keretrendszerekkel.

**Q:** Elérhető ingyenes próba verzió az Aspose.OCR for .NET-hez?  
**A:** Természetesen! Az ingyenes próbát **[itt](https://releases.aspose.com/)** érheted el.

**Q:** Hogyan kaphatok támogatást az Aspose.OCR for .NET-hez?  
**A:** Látogasd meg az **[Aspose.OCR fórumot](https://forum.aspose.com/c/ocr/16)** a dedikált támogatásért.

**Q:** Kaphatok ideiglenes licencet tesztelési célokra?  
**A:** Igen, ideiglenes licencet **[itt](https://purchase.aspose.com/temporary-license/)** szerezhetsz.

**Q:** Hol találom az Aspose.OCR for .NET dokumentációját?  
**A:** A dokumentáció **[itt](https://reference.aspose.com/ocr/net/)** érhető el.

---

**Utoljára frissítve:** 2025-12-22  
**Tesztelve:** Aspose.OCR 24.11 for .NET  
**Szerző:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}