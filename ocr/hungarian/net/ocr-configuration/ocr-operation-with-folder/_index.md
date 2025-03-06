---
title: OCR művelet mappával az OCR képfelismerésben
linktitle: OCR művelet mappával az OCR képfelismerésben
second_title: Aspose.OCR .NET API
description: Az Aspose.OCR segítségével felszabadíthatja az OCR képfelismerés erejét a .NET-ben. Könnyedén kivonhatja a szöveget a képekből.
weight: 11
url: /hu/net/ocr-configuration/ocr-operation-with-folder/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR művelet mappával az OCR képfelismerésben

## Bevezetés

Üdvözöljük az optikai karakterfelismerés (OCR) világában az Aspose.OCR for .NET használatával! Ha .NET-alkalmazásaiban zökkenőmentesen szeretne szöveget kivonni a képekből, akkor jó helyen jár. Ez az oktatóanyag végigvezeti az OCR-képfelismerés folyamatán mappákkal, kihasználva az Aspose.OCR hatékony képességeit.

## Előfeltételek

Mielőtt belevágna az oktatóanyagba, győződjön meg arról, hogy rendelkezik a következő előfeltételekkel:

- C# és .NET fejlesztési ismeretek.
- A Visual Studio telepítve van a gépedre.
-  Aspose.OCR for .NET könyvtár, amelyet letölthet[itt](https://releases.aspose.com/ocr/net/).
- Az OCR-fogalmak alapvető ismerete.

## Névterek importálása

Győződjön meg arról, hogy a C#-kódban importálta az Aspose.OCR használatához szükséges névtereket. A szkript elejére írja be a következőket:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## 1. lépés: Állítsa be a dokumentumkönyvtárat

```csharp
// ExStart:1
// A dokumentumok könyvtárának elérési útja.
string dataDir = "Your Document Directory";
```

Győződjön meg arról, hogy a „Dokumentumkönyvtár” kifejezést a képek tárolási útvonalával cseréli le.

## 2. lépés: Inicializálja az Aspose.OCR-t

```csharp
// Inicializálja az AsposeOcr egy példányát
AsposeOcr api = new AsposeOcr();
```

Hozzon létre egy példányt az AsposeOcr osztályból a funkcióinak használatához.

## 3. lépés: Adja meg a kép elérési útját

```csharp
//Kép elérési útja
string fullPath = dataDir + "OCR";
```

Kösse össze a dokumentumkönyvtár elérési útját a képeket tartalmazó adott mappával.

## 4. lépés: Képek felismerése

```csharp
// Kép felismerése
RecognitionResult[] result = api.RecognizeMultipleImages(fullPath, new RecognitionSettings
{
    //alapértelmezett vagy egyéni
});
```

Használja a RecognizeMultipleImages metódust, hogy a megadott mappán belül több képen OCR-t hajtson végre.

## 5. lépés: Eredmények nyomtatása

```csharp
// Eredmény nyomtatása
for (int i = 0; i < result.Length; i++)
{
    Console.WriteLine($"Image: {i}\n Result:\n {result[i].RecognitionText}");
}
```

Keresse át az eredményeket, és nyomtassa ki a felismert szöveget minden egyes képhez.

## 6. lépés: Következtetés

```csharp
// ExEnd:1
Console.WriteLine("OCROperationWithFolder executed successfully");
```

Győződjön meg arról, hogy a szkript befejeződött, hogy jelezze az OCR művelet sikeres végrehajtását a mappákkal.

## Következtetés

Gratulálunk! Sikeresen megtanulta, hogyan valósítsa meg az OCR képfelismerést mappákkal az Aspose.OCR for .NET használatával. Ez a hatékony eszköz számtalan lehetőséget nyit meg a .NET-alkalmazások képeiből szövegek kinyerésére.

## GYIK

### 1. kérdés: Használhatom az Aspose.OCR-t .NET-hez kereskedelmi projektekben?

 1. válasz: Igen, az Aspose.OCR for .NET egy kereskedelmi termék. Az engedélyezéssel kapcsolatos információkért látogasson el a webhelyre[itt](https://purchase.aspose.com/buy).

### Q2:. Van ingyenes próbaverzió?

 2. válasz: Igen, felfedezheti az ingyenes próbaverziót[itt](https://releases.aspose.com/).

### 3. kérdés: Hol találom a dokumentációt?

 A3: A dokumentáció elérhető[itt](https://reference.aspose.com/ocr/net/).

### 4. kérdés: Hogyan szerezhetek ideiglenes licencet?

 A4: Ideiglenes engedélyek szerezhetők be[itt](https://purchase.aspose.com/temporary-license/).

### 5. kérdés: Támogatásra van szüksége, vagy kérdései vannak?

 A5: Látogassa meg a[Aspose.OCR fórum](https://forum.aspose.com/c/ocr/16) közösségi támogatásért.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
