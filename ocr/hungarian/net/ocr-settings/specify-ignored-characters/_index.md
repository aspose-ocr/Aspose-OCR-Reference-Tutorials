---
date: 2025-12-27
description: Fedezze fel a fejlett OCR nyelvtámogatást és képességeket az Aspose.OCR
  for .NET segítségével. Hatékony, pontos és fejlesztőbarát.
linktitle: OCR Language Support – Ignored Characters in Image Recognition
second_title: Aspose.OCR .NET API
title: OCR nyelvi támogatás – Figyelmen kívül hagyott karakterek a képfelismerésben
url: /hu/net/ocr-settings/specify-ignored-characters/
weight: 14
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR nyelvi támogatás: Figyelmen kívül hagyott karakterek megadása a képfelismerésben

## Bevezetés

Az OCR nyelvi támogatás a modern dokumentumautomatizálás egyik alappillére, lehetővé téve az alkalmazások számára, hogy szöveget olvassanak képekből számos ábécén és szimbólumon keresztül. Ebben az útmutatóban megtanulja, hogyan mondja meg a **Aspose.OCR for .NET**-nek, hogy figyelmen kívül hagyjon bizonyos karaktereket a felismerés során – ez egy elengedhetetlen trükk, ha tisztább kimenetre van szüksége, vagy ha ki szeretné szűrni a zajt, például az oldalszámokat vagy díszítő szimbólumokat. A útmutató végére egy kész, futtatható kódrészletet kap, amely végponttól végpontig bemutatja a funkciót.

## Gyors válaszok
- **Mi jelent a „figyelmen kívül hagyott karakterek” kifejezés?** Olyan karakterek, amelyeket az OCR motor kihagy a végeredmény karakterláncának összeállítása során.  
- **Miért használjuk?** Javítja a pontosságot, ha bizonyos szimbólumok nem relevánsak az üzleti logikája számára.  
- **Melyik API metódus kezeli?** `RecognitionSettings.IgnoredCharacters`.  
- **Kombinálható nyelvi csomagokkal?** Igen – a figyelmen kívül hagyott karakterek együtt működnek bármely betöltött nyelvvel.  
- **Szükséges licenc?** Ideiglenes vagy teljes licenc szükséges a termelésben való használathoz.

## Előfeltételek

Mielőtt elmélyedne az Aspose.OCR for .NET által nyújtott gazdag funkcionalitásban, győződjön meg arról, hogy a következő előfeltételek rendelkezésre állnak:

1. Aspose.OCR telepítése  

   Győződjön meg arról, hogy sikeresen telepítette az Aspose.OCR for .NET-et. A szükséges fájlokat a [letöltési oldalon](https://releases.aspose.com/ocr/net/) találja.

2. Dokumentumkönyvtár beállítása  

   Hozzon létre egy dedikált könyvtárat a dokumentumok számára. Ez elengedhetetlen a példák zökkenőmentes futtatásához. Frissítse a példákban a `dataDir` változót a dokumentumkönyvtár elérési útjával.

3. Ideiglenes licenc (opcionális)  

   Ha ideiglenes licenccel szeretné kipróbálni az Aspose.OCR for .NET-et, szerezze be azt [innen](https://purchase.aspose.com/temporary-license/).

## Névterek importálása

Az Aspose.OCR for .NET használatának megkezdéséhez importálnia kell a szükséges névtereket. Adja hozzá a következő sorokat a kódjához:

```csharp
using System.IO;

using Aspose.OCR;
using System;
```

## Miért kell megadni a figyelmen kívül hagyott karaktereket?

Sok valós helyzetben – például számlák, nyugták vagy többnyelvű űrlapok feldolgozásakor – előfordulhatnak ismétlődő karakterek, amelyek nem részei a lényeges adatoknak (például elválasztóként használt kötőjelek, oldalszámok vagy díszítő szimbólumok). Ha a OCR motor számára megmondja, hogy hagyja ki ezeket, csökkenti a post‑feldolgozási erőfeszítést és javítja a downstream analitikák megbízhatóságát.

## Lépésről‑lépésre útmutató

### 1. lépés: Dokumentumkönyvtár beállítása

Kezdje azzal, hogy megadja azt a könyvtárat, ahol a dokumentumai tárolva vannak. Cserélje le a `"Your Document Directory"`-t a dokumentumok tényleges elérési útjára.

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";
```

### 2. lépés: Aspose.OCR inicializálása

Hozzon létre egy példányt az OCR motorból. Ez az objektum kezeli majd az összes későbbi felismerési hívást.

```csharp
// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

### 3. lépés: Kép felismerése figyelmen kívül hagyott karakterekkel

Adja át a képfájlt egy `RecognitionSettings` objektummal, amely felsorolja a figyelmen kívül hagyandó karaktereket. Ebben a példában a `a`, `b` és `1` karaktereket hagyjuk ki.

```csharp
// Recognize image with specified ignored characters
RecognitionResult result = api.RecognizeImage(dataDir + "SpanishOCR.bmp", new RecognitionSettings
{
    IgnoredCharacters = "ab1"
});
```

### 4. lépés: Felismert szöveg megjelenítése

Végül írja ki a megtisztított szöveget a konzolra vagy bármely más kimenetre, amelyet preferál.

```csharp
// Display the recognized text
Console.WriteLine(result.RecognitionText);
```

## Gyakori problémák és tippek

- **Helytelen útvonal:** Győződjön meg arról, hogy a `dataDir` a megfelelő útvonalelválasztóval (`\` vagy `/`) végződik az operációs rendszeréhez.  
- **Nem támogatott nyelv:** Az OCR motornak rendelkeznie kell a forráskép nyelvi csomagjával; ellenkező esetben a figyelmen kívül hagyott karakterek nem lesznek helyesen alkalmazva.  
- **Licenc hibák:** Ha licenckivételt észlel, ellenőrizze, hogy az ideiglenes licencfájl helyesen van-e hivatkozva a projektben.

## Következtetés

Az Aspose.OCR for .NET fejlesztőket fejlett OCR képességekkel ruház fel, egyszerűsítve a képek szerkeszthető és kereshető szöveggé alakításának folyamatát. A lépésről‑lépésre útmutató követésével megtanulta, hogyan zárja ki a nem kívánt karaktereket, így OCR csővezetékét tisztábbá és megbízhatóbbá teszi. Tekintse meg a [dokumentációt](https://reference.aspose.com/ocr/net/) a mélyebb betekintésért, és fedezze fel, hogyan emelheti az Aspose.OCR a OCR projektjeit.

## Gyakran ismételt kérdések

### Q1: Használhatom az Aspose.OCR for .NET-et nem kereskedelmi projektekben?

A1: Igen, az Aspose.OCR for .NET használható kereskedelmi és nem kereskedelmi projektekben egyaránt. További információkért tekintse meg a [licenc részleteket](https://purchase.aspose.com/buy).

### Q2: Elérhető ingyenes próba?

A2: Természetesen! Ingyenes próbaverziót érhet el [innen](https://releases.aspose.com/), hogy felfedezze az Aspose.OCR for .NET funkcióit és előnyeit, mielőtt elköteleződne.

### Q3: Hogyan kaphatok támogatást az Aspose.OCR-hez?

A3: Bármilyen kérdés vagy segítség esetén látogassa meg az [Aspose.OCR fórumot](https://forum.aspose.com/c/ocr/16), hogy kapcsolatba léphessen a közösséggel és szakértői tanácsot kérhessen.

### Q4: Milyen nyelveket támogat az Aspose.OCR?

A4: Az Aspose.OCR számos nyelvet támogat, így sokoldalú választás az OCR feladatokhoz. A teljes listáért tekintse meg a dokumentációt.

### Q5: Vásárolhatok ideiglenes licencet az Aspose.OCR-hez?

A5: Igen, ha ideiglenes licencre van szüksége, azt [innen](https://purchase.aspose.com/temporary-license/) szerezheti be rövid távú használatra.

**Utolsó frissítés:** 2025-12-27  
**Tesztelve:** Aspose.OCR 23.12 for .NET  
**Szerző:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}