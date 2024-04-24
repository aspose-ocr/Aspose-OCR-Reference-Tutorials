---
title: Eredmény mentése dokumentumként az OCR képfelismerésben
linktitle: Eredmény mentése dokumentumként az OCR képfelismerésben
second_title: Aspose.OCR .NET API
description: Engedje ki az Aspose.OCR-ben rejlő lehetőségeket a .NET számára. Könnyen felismerheti a képek szövegét, és mentheti az eredményeket különböző dokumentumformátumokba.
type: docs
weight: 10
url: /hu/net/ocr-settings/save-result-as-document/
---
## Bevezetés

Üdvözöljük az optikai karakterfelismerés (OCR) izgalmas világában az Aspose.OCR for .NET segítségével! Ebben az átfogó oktatóanyagban elmélyülünk az Aspose.OCR használatának fortélyaiban a képek szövegének felismerésére, és bemutatjuk, hogyan mentheti el az eredményeket különböző dokumentumformátumokba.

## Előfeltételek

Mielőtt nekivágnánk ennek az OCR-útnak, győződjön meg arról, hogy a következő előfeltételek teljesülnek:

-  Aspose.OCR .NET-hez. Győződjön meg arról, hogy telepítve van az Aspose.OCR könyvtár. Letöltheti[itt](https://releases.aspose.com/ocr/net/).

-  Dokumentumkönyvtár: rendelkezzen egy kijelölt könyvtárral a dokumentumok számára, és frissítse a`dataDir` változót a megadott kódban ennek megfelelően.

## Névterek importálása

Kezdje a szükséges névterek importálásával. Ezek azok az építőelemek, amelyek OCR-képességekkel ruházzák fel kódját.

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

Most bontsuk fel a példát több lépésre:

## 1. lépés: Inicializálja az Aspose.OCR-t

```csharp
// A dokumentumok könyvtárának elérési útja.
string dataDir = "Your Document Directory";

// Inicializálja az AsposeOcr egy példányát
AsposeOcr api = new AsposeOcr();
```

Ez a lépés az Aspose.OCR API inicializálásával állítja be a szakaszt.

## 2. lépés: Kép felismerése

```csharp
// Kép felismerése
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings { });
```

Itt az Aspose.OCR-t használjuk a megadott képen belüli szöveg felismerésére (a "sample.png" kifejezést cserélje ki a képfájljára).

## 3. lépés: Mentse el az eredményt különböző formátumokban

```csharp
// Mentse el az eredményt a kívánt formátumban
result.Save(RunExamples.GetDataDir_OCR() + "sample.docx", SaveFormat.Docx);
result.Save(RunExamples.GetDataDir_OCR() + "sample.txt", SaveFormat.Text);
result.Save(RunExamples.GetDataDir_OCR() + "sample.pdf", SaveFormat.Pdf);
result.Save(RunExamples.GetDataDir_OCR() + "sample.xlsx", SaveFormat.Xlsx);
```

Szabja testre ezt a lépést igényei szerint. Az Aspose.OCR lehetővé teszi, hogy a felismert szöveget különféle dokumentumformátumokba mentse, például DOCX, TXT, PDF és XLSX.

## 4. lépés: Jelenítse meg a sikeres üzenetet

```csharp
Console.WriteLine("SaveResultAsDocument executed successfully");
```

Egy egyszerű megerősítő üzenet, amely tájékoztatja Önt, hogy a folyamat gond nélkül befejeződött.

Az alábbi lépések követésével sikeresen kamatoztatta az Aspose.OCR for .NET erejét a képeken belüli szöveg felismerésében, és az eredmények különböző dokumentumformátumokba mentésében.

## Következtetés

Összefoglalva, az Aspose.OCR for .NET a lehetőségek világát nyitja meg a képekben történő szövegfelismeréshez. Akár adatokat nyer ki, akár kereshető dokumentumokat hoz létre, az Aspose.OCR intuitív API-jával leegyszerűsíti a folyamatot.

## GYIK

### Q1. Az Aspose.OCR kompatibilis a különböző képformátumokkal?

1. válasz: Igen, az Aspose.OCR a képformátumok széles skáláját támogatja, rugalmasságot biztosítva az OCR-feladatokban.

### 2. kérdés: Testreszabhatom a felismerési beállításokat a nagyobb pontosság érdekében?

A2: Abszolút! Az Aspose.OCR felismerési beállításokat biztosít az OCR folyamat finomhangolásához az Ön egyedi igényei szerint.

### 3. kérdés: Van ingyenes próbaverzió?

 3. válasz: Igen, megkezdheti az ingyenes próbaverziót[itt](https://releases.aspose.com/).

### 4. kérdés: Hogyan szerezhetek ideiglenes licenceket az Aspose.OCR-hez?

 A4: Ideiglenes engedélyek szerezhetők be[itt](https://purchase.aspose.com/temporary-license/).

### 5. kérdés: Hol kérhetek segítséget vagy csatlakozhatok a közösséghez?

 5. válasz: Csatlakozzon az Aspose.OCR közösséghez a címen[Aspose fórum](https://forum.aspose.com/c/ocr/16) támogatásért és megbeszélésekért.