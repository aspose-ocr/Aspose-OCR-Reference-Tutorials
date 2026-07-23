---
date: 2026-07-23
description: Ismerje meg, hogyan nyerhet ki szöveget képből az Aspose.OCR for .NET
  használatával, téglalapok előkészítésével a OCR pontosságának javítása és a kép
  szöveggé konvertálása hatékonyan.
keywords:
- extract text from image
- convert image to text
- improve ocr accuracy
lastmod: 2026-07-23
linktitle: Téglalapok előkészítése OCR képfelismerésben
og_description: Szöveg kinyerése képből az Aspose.OCR for .NET használatával. Ismerje
  meg a téglalapok előkészítését, az OCR pontosságának növelését, és a kép szöveggé
  konvertálását hatékonyan.
og_image_alt: Guide to extract text from image using rectangles with Aspose.OCR for
  .NET
og_title: Szöveg kinyerése képből téglalapokkal – OCR útmutató
schemas:
- author: Aspose
  dateModified: '2026-07-23'
  description: Learn how to extract text from image using Aspose.OCR for .NET, preparing
    rectangles to improve OCR accuracy and convert image to text efficiently.
  headline: Extract Text from Image with Rectangles – OCR Guide
  type: TechArticle
- questions:
  - answer: It converts visual characters in a picture into machine‑readable strings.
    question: What does “extract text from image” mean?
  - answer: Aspose.OCR for .NET provides a full‑featured OCR engine.
    question: Which library handles this in .NET?
  - answer: A free trial works for development; a commercial license is required for
      deployment.
    question: Do I need a license for production?
  - answer: Yes—define rectangles to target only the areas that contain useful text.
    question: Can I limit OCR to specific zones?
  - answer: .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.
    question: What .NET versions are supported?
  type: FAQPage
second_title: Aspose.OCR .NET API
tags:
- ocr
- Aspire.OCR
- .NET image processing
- extract text from image
title: Szöveg kinyerése képből téglalapokkal – OCR útmutató
url: /hu/net/ocr-optimization/prepare-rectangles/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kép szövegének kinyerése téglalapokkal – OCR útmutató

## Bevezetés

Az optikai karakterfelismerés (OCR) lehetővé teszi, hogy **kép szövegét kinyerje** a fájlokból, így azok kereshetővé és szerkeszthetővé válnak. Ebben az útmutatóban megmutatjuk, hogyan növelheti az OCR pontosságát egyedi téglalapok előkészítésével, amelyek a motorra a pontosan szükséges zónákat fókuszálják. Az Aspose.OCR for .NET használatával megtekintheti a teljes munkafolyamatot – a projekt beállításától a felismert karakterláncok lekéréséig – így megbízható kép‑szöveg konverziót ágyazhat be bármely .NET alkalmazásba.

## Gyors válaszok
- **Mi jelent a “extract text from image”?** Átalakítja a képen látható vizuális karaktereket géppel olvasható karakterláncokká.  
- **Melyik könyvtár kezeli ezt .NET‑ben?** Az Aspose.OCR for .NET teljes körű OCR motorral rendelkezik.  
- **Szükségem van licencre a termeléshez?** A ingyenes próba verzió fejlesztéshez működik; a telepítéshez kereskedelmi licenc szükséges.  
- **Korlátozhatom az OCR‑t meghatározott zónákra?** Igen – definiáljon téglalapokat, hogy csak a hasznos szöveget tartalmazó területekre fókuszáljon.  
- **Mely .NET verziók támogatottak?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.

## Mi az a “extract text from image” téglalapokkal?

Az `extract text from image` folyamat a meghatározott téglalapos zónákon belüli karaktereket olvassa, mindent mást figyelmen kívül hagyva. Az OCR ezen zónákra korlátozásával magasabb pontosságot, gyorsabb feldolgozást és kevesebb utófeldolgozási munkát ér el. Ez a megközelítés elkülöníti a kívánt szöveget, miközben eldobja a háttérgrafikákat, díszítő elemeket és egyéb vizuális zajt, amelyek összezavarhatják az OCR motort.

## Miért készítsünk téglalapokat az OCR előtt?

A téglalapok előkészítése lehetővé teszi, hogy az OCR motor a kép legrelevánsabb részeire összpontosítson, ami javítja mind a sebességet, mind a pontosságot. Az elemzési terület szűkítésével csökkenti a motor által vizsgálandó adat mennyiségét, ami gyorsabb eredményeket és kevesebb félreolvasást eredményez a felesleges vizuális zaj miatt.

- **A releváns tartalomra fókuszálás:** Hagyja ki a fejléceket, lábléceket vagy díszítő grafikákat, amelyek összezavarnák a motort.  
- **Teljesítmény növelése:** A kisebb területek kevesebb számítást igényelnek, ami akár 40 %-kal is csökkentheti a futási időt nagy szkenneléseknél.  
- **Pontosság javítása:** A vizuális zaj csökkentése a karakterfelismerési arányt ~85 %-ról >95 %-ra emeli zajos dokumentumok esetén.

## Miért fontos ez a valós projektekben

Sok üzleti dokumentum – nyugták, számlák, személyi igazolványok – szöveget kever a logókkal vagy vonalkódokkal. A szükséges mezők köré téglalapok rajzolásával csak a hasznos adatokat nyeri ki, jelentősen csökkentve az utólagos tisztítási munkát és növelve az automatizált munkafolyamatok megbízhatóságát. Ez a célzott kinyerés csökkenti az utófeldolgozási erőfeszítést és segít a adatkezelési szabványoknak való megfelelésben.

## Általános felhasználási esetek

- **Adatbevitel automatizálása:** Kivonja a konkrét mezőket beolvasott űrlapokból vagy költségnyugtákból.  
- **Megfelelőség ellenőrzése:** Elkülöníti a jogi záradékokat vagy szabályozási nyilatkozatokat ellenőrzés céljából.  
- **Tartalom indexelése:** Csak a kép címsorát vagy feliratát indexeli a keresőmotor láthatósága érdekében.

## Előfeltételek

- Alapvető C# és .NET fejlesztési ismeretek.  
- Az Aspose.OCR for .NET könyvtár telepítve – töltsd le **[itt](https://releases.aspose.com/ocr/net/)** vagy böngészd az összes kiadást **[itt](https://releases.aspose.com/)**.  
- Egy minta kép (pl. `sample.png`), amely tartalmazza a kinyerni kívánt szöveget.

## Névterek importálása

A `using` utasítások beviszik az OCR motort és a geometriai osztályokat a láthatóságba.

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## 1. lépés: Dokumentumkönyvtár beállítása

Adja meg a mappát, amely a képeket tartalmazza, és hozzon létre egy példányt az OCR motorból.

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Hogyan nyerjünk ki szöveget képből több téglalap használatával

Töltsd be a képet egyszer, majd add át a téglalapok listáját az OCR motornak. Minden téglalap egy érdeklődési területet definiál, és a motor minden régióhoz külön karakterláncot ad vissza, lehetővé téve a mezők egyedi kezelését és az eredmények szükség szerint történő kombinálását.

### Téglalapok definiálása

`Rectangle` objektumok leírják az X‑Y koordinátákat és a méretet minden egyes szkennelni kívánt zónához.  

```csharp
List<Rectangle> rects = new List<Rectangle>()
{
    new Rectangle(138, 352, 2033, 537),
    new Rectangle(147, 890, 2033, 1157),
    new Rectangle(923, 2045, 465, 102),
    new Rectangle(104, 2147, 2076, 819)
};
```

### OCR felismerés végrehajtása

A `RecognizeImage` metódus a megadott téglalaplistával dolgozza fel a képet, és minden régióhoz visszaadja a felismert szöveget.  

```csharp
// first case
List<string> listResult = api.RecognizeImage(dataDir + "sample.png", rects);

// Display the recognized text
foreach (string s in listResult)
{
    Console.WriteLine(s);
}
```

## Hogyan nyerjünk ki szöveget képből RecognitionSettings használatával (alternatív megközelítés)

Ha inkább beállítás‑alapú hívást szeretnél, ugyanazt az eredményt elérheted a `RecognitionSettings` segítségével. Ez az objektum lehetővé teszi a téglalapdefiníciók, a nyelv, a DPI és egyéb OCR beállítások egyesítését, tiszta, egy‑paraméteres API hívást biztosítva.

### Felismerési beállítások definiálása

`RecognitionSettings` lehetővé teszi, hogy a téglalaplistát és további opciókat (pl. nyelv, DPI) egyetlen objektumba csomagold.  

```csharp
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings
{
    RecognitionAreas = rects
});
```

### Felismert szöveg megjelenítése

Iterálj a visszaadott karakterláncokon, és írd ki minden régió szövegét.  

```csharp
// Display the recognized text
foreach (string s in result.RecognitionAreasText)
{
    Console.WriteLine(s);
}
```

## Általános problémák és tippek

- **Helytelen téglalap koordináták:** Ellenőrizd, hogy az `X`, `Y`, `Width` és `Height` a kívánt területre mutat-e.  
- **Képminőség:** Alacsony felbontású vagy erősen tömörített képek rontják az OCR eredményeket; fontold meg az előfeldolgozást, például binarizálást.  
- **Üres eredmények:** Győződj meg róla, hogy a téglalapok ténylegesen olvasható szöveget tartalmaznak; különben a motor üres karakterláncokat ad vissza.

## Hibakeresés és legjobb gyakorlatok

| Tünet | Valószínű ok | Megoldás |
|-------|--------------|----------|
| Nincs kimenet vagy üres karakterláncok | A téglalapok a kép határain kívül vannak | Ellenőrizd újra a kép méreteit és a téglalap koordinátákat |
| Torzuló karakterek | Gyenge kontraszt vagy zaj | Alkalmazz szürkeárnyalatos átalakítást és küszöbölést az OCR előtt |
| Lassú teljesítmény nagy fájloknál | Túl sok téglalap vagy nagyon nagy kép | Oszd fel a képet vagy csökkentsd a téglalapok számát, ahol lehetséges |

## Következtetés

Most már tudod, hogyan **kép szövegét kinyerheted** egyedi téglalapok előkészítésével az Aspose.OCR for .NET segítségével. Ez a megközelítés pontos irányítást biztosít az OCR feldolgozás felett, gyorsabb és pontosabb szöveg‑kinyerési funkciókat nyújtva bármely .NET megoldáshoz.

## Gyakran Ismételt Kérdések

**Q:** Használhatom az Aspose.OCR for .NET-et más .NET keretrendszerekkel?  
**A:** Igen, az Aspose.OCR for .NET működik .NET Framework 4.5+, .NET Core 3.1+, és .NET 5/6/7 verziókkal.

**Q:** Elérhető ingyenes próba?  
**A:** Természetesen! Töltsd le a próbaverziót **[itt](https://releases.aspose.com/)**.

**Q:** Hol kaphatok támogatást az Aspose.OCR for .NET-hez?  
**A:** Látogasd meg a **[Aspose.OCR fórumot](https://forum.aspose.com/c/ocr/16)** a dedikált segítségért.

**Q:** Kaphatok ideiglenes licencet teszteléshez?  
**A:** Igen, ideiglenes licenc elérhető **[itt](https://purchase.aspose.com/temporary-license/)**.

**Q:** Hol található a hivatalos dokumentáció?  
**A:** A teljes API referencia **[itt](https://reference.aspose.com/ocr/net/)** érhető el.

---

**Utolsó frissítés:** 2026-07-23  
**Tesztelve ezzel:** Aspose.OCR 24.11 for .NET  
**Szerző:** Aspose  

{{< blocks/products/products-backtop-button >}}

## Kapcsolódó oktatóanyagok

- [Hogyan nyerjünk ki téglalapokat bekezdésekhez az OCR képfelismerésben](/ocr/net/image-and-drawing-recognition/get-rectangles-for-paragraphs/)
- [Hogyan OCR-eljünk képet – OCR végrehajtása képen az OCR képfelismerésben](/ocr/net/image-and-drawing-recognition/perform-ocr-on-image/)
- [Hogyan nyerjünk ki szöveget képből az Aspose.OCR for .NET használatával](/ocr/net/text-recognition/get-recognition-result/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}