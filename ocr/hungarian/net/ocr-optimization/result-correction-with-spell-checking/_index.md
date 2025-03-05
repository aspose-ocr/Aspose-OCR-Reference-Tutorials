---
title: Eredményjavítás helyesírás-ellenőrzéssel az OCR képfelismerésben
linktitle: Eredményjavítás helyesírás-ellenőrzéssel az OCR képfelismerésben
second_title: Aspose.OCR .NET API
description: Növelje az OCR pontosságát az Aspose.OCR for .NET segítségével. Helyesírások javítása, szótárak testreszabása és hibamentes szövegfelismerés problémamentesen.
type: docs
weight: 13
url: /hu/net/ocr-optimization/result-correction-with-spell-checking/
---
## Bevezetés

Az optikai karakterfelismerés (OCR) területén a pontos eredmények elérése kulcsfontosságú ahhoz, hogy értelmes információkat nyerjünk ki a képekből. Az egyik gyakori kihívás a hibásan írt szavak kezelése a felismerési folyamat során. Szerencsére az Aspose.OCR for .NET hatékony megoldást kínál az OCR-eredmények javítására a helyesírás-ellenőrzés révén.

Ez az oktatóanyag végigvezeti az eredmények javításának folyamatán a helyesírás-ellenőrzéssel az Aspose.OCR for .NET használatával. A végére képes lesz javítani az OCR-eredetű szöveg pontosságát, így még kifinomultabb és hibamentes kimenetet biztosít.

## Előfeltételek

Mielőtt belemerülnénk a helyesírás-ellenőrző varázslatba, győződjön meg arról, hogy a következő előfeltételek teljesülnek:

-  Aspose.OCR for .NET Library: Töltse le és telepítse az Aspose.OCR könyvtárat a[kiadási oldal](https://releases.aspose.com/ocr/net/).

- Dokumentumkönyvtár: Győződjön meg arról, hogy rendelkezik egy kijelölt könyvtárral a dokumentumok számára. Cserélje le a „Saját dokumentumkönyvtárat” a kódrészletekben a tényleges elérési úttal.

## Névterek importálása

Kezdjük a szükséges névterek importálásával a .NET-projektben:

```csharp
using System;
using Aspose.OCR.SpellChecker;
using System.Collections.Generic;
```

## 1. lépés: Inicializálja az Aspose.OCR-t

Az OCR folyamat elindításához inicializálja az Aspose.OCR egy példányát.

```csharp
// A dokumentumok könyvtárának elérési útja.
string dataDir = "Your Document Directory";

// Inicializálja az AsposeOcr egy példányát
AsposeOcr api = new AsposeOcr();
```

## 2. lépés: Kép felismerése

Ezután ismerje fel a szöveget a képen az Aspose.OCR segítségével. Íme egy részlet, amely bemutatja ezt a folyamatot:

```csharp
// Kép felismerése
RecognitionResult result = api.RecognizeImage(dataDir + "sample_bad.png", new RecognitionSettings(Language.Eng));
```

## 3. lépés: A javítás előtt

A javítás előtt kérje le az OCR eredményét, hogy összehasonlítsa a javított verzióval.

```csharp
// Szerezzen eredményt
Console.WriteLine("BEFORE CORRECTION:\n" + result.RecognitionText);
```

## 4. lépés: Javítás után

Alkalmazza a helyesírás-ellenőrzést a javított eredmény eléréséhez. A következő kódrészlet illusztrálja ezt a lépést:

```csharp
// Javított eredmény elérése
string correctedResult = result.GetSpellCheckCorrectedText(SpellCheckLanguage.Eng);
Console.WriteLine("AFTER CORRECTION:\n" + correctedResult);
```

## 5. lépés: Rosszul írt szavak és javaslatok

Szerezze meg a hibásan írt szavak listáját a javasolt javításokkal együtt a következő kód segítségével:

```csharp
// Szerezze meg a hibásan írt szavak listáját javaslatokkal
List<SpellCheckError> errorsList = result.GetSpellCheckErrorList(SpellCheckLanguage.Eng);
foreach (var word in errorsList)
{
	Console.Write("Word:" + word.Word);
	Console.Write(" StartPosition:" + word.StartPosition);
	Console.WriteLine(" Length:" + word.Length);
	Console.WriteLine("SuggestedWords:");
	foreach (var suggest in word.SuggestedWords)
	{
		Console.Write(suggest.Word + " ");
	}
	Console.WriteLine();
}
```

## 6. lépés: Helyes felhasználói szöveg

Javítsa ki a felhasználó által megadott szöveget az Aspose.OCR könyvtár használatával:

```csharp
// Helyes felhasználói szöveg
Console.WriteLine("recogniition -> " + api.CorrectSpelling("recogniition"));
```

## 7. lépés: Javítás felhasználói szótárral

Fokozza tovább a javítást egyéni felhasználói szótár beépítésével:

```csharp
// Szerezzen javított eredményt a felhasználói szótár segítségével
string correctedResultUserDict = result.GetSpellCheckCorrectedText(SpellCheckLanguage.Eng, dataDir+"dictionary.txt");
Console.WriteLine("AFTER CORRECTION WITH USER DICTIONARY:\n" + correctedResultUserDict);
```

## Következtetés

Gratulálunk! Sikeresen navigált az Aspose.OCR for .NET helyesírás-ellenőrző funkciói között. Ez a funkció lehetővé teszi az OCR-eredmények finomítását, biztosítva a pontosságot és kiküszöbölve a hibákat.

## GYIK

### 1. kérdés: Használhatom az Aspose.OCR-t az angoltól eltérő nyelvekhez?

1. válasz: Igen, az Aspose.OCR több nyelvet is támogat. Módosítsa ennek megfelelően a nyelvi beállításokat.

### 2. kérdés: Hogyan integrálhatom az Aspose.OCR-t .NET-projektembe?

 A2: Lásd a[dokumentáció](https://reference.aspose.com/ocr/net/) a részletes integrációs lépésekért.

### 3. kérdés: Elérhető az Aspose.OCR próbaverziója?

 V3: Igen, felfedezheti a funkciókat a[ingyenes próbaverzió](https://releases.aspose.com/).

### 4. kérdés: Feltölthetek egyéni szótárt helyesírás-ellenőrzéshez?

A4: Abszolút! Az oktatóanyag bemutatja, hogyan lehet javítani a javítást a felhasználó által biztosított szótár használatával.

### 5. kérdés: Hol kérhetek támogatást az Aspose.OCR-hez?

 A5: Látogassa meg a[Aspose.OCR fórum](https://forum.aspose.com/c/ocr/16) közösségi támogatásért és útmutatásért.