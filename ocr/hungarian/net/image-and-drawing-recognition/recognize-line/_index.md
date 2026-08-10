---
date: 2026-02-22
description: Tanulja meg, hogyan lehet szöveget kinyerni a képből az Aspose.OCR for
  .NET használatával, PNG-t szöveggé konvertálni, és javítani az OCR pontosságát C#
  alkalmazásokban.
linktitle: Extract Text from Image – Recognize Line with Aspose.OCR
second_title: Aspose.OCR .NET API
title: Képből szöveg kinyerése – Sor felismerése az Aspose.OCR segítségével
url: /hu/net/image-and-drawing-recognition/recognize-line/
weight: 14
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kép szövegének kinyerése – Sor felismerése az Aspose.OCR-rel

## Introduction

Az optikai karakterfelismerés (OCR) a szöveges képek kereshető, szerkeszthető tartalommá alakításának elsődleges megoldásává vált. Ha gyorsan és megbízhatóan szeretne **szöveget kinyerni képfájlokból**, az Aspose.OCR for .NET egy erőteljes, fejlesztőbarát API-t kínál, amely mind a teljes .NET Framework, mind a **ASP OCR .NET Core** projektekben működik. Ebben az útmutatóban végigvezetjük, hogyan ismerjen fel sorokat egy képen, hogyan konvertálja ezeket a sorokat egyszerű szöveggé, és hogyan jelenítse meg az eredményt – mindezt tiszta, könnyen követhető C# kóddal.

## Quick Answers
- **Az Aspose.OCR mit csinál?** Nyomtatott vagy kézírásos szöveget olvas be képfájlformátumokból, és egyszerű karakterláncokat ad vissza.  
- **Mely képfájlformátumok támogatottak?** PNG, JPEG, BMP, GIF, TIFF és továbbiak.  
- **Szükség van licencre a teszteléshez?** Ingyenes próba verzió használható fejlesztéshez; a termeléshez licenc szükséges.  
- **Futtatható .NET Core-on?** Igen – a könyvtár támogatja a .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6 verziókat.  
- **Mennyi időt vesz igénybe egy egyszerű sorfelismerés?** Általában egy másodpercnél kevesebb egy szabványos PNG esetén.

## What is “extract text from image”?

A szöveg kinyerése egy képből azt jelenti, hogy OCR technológiát használunk a vizuális pixelek elemzésére, a karakterek azonosítására, és azok géppel olvasható szövegként való kiadására. Ez lehetővé teszi például beolvasott dokumentumok digitalizálását, nyugták adatbevitelének automatizálását, vagy kereshető archívumok létrehozását.

## Why use Aspose.OCR for .NET?

- **Magas pontosság** több nyelven és betűtípusban.  
- **Nincs külső függőség** – tiszta managed kód, könnyen integrálható.  
- **Átfogó formátumtámogatás** – működik PNG, JPEG, BMP és további formátumokkal.  
- **Egyszerű API** – néhány kódsorral eljuthatsz a képből a szövegig.  

### How does this help you **convert PNG to text**?

Mivel az Aspose.OCR közvetlenül képes PNG fájlok olvasására, egy beolvasott PNG képet átadhatsz a `RecognizeLine` metódusnak, és tiszta karakterláncot kapsz anélkül, hogy köztes konverziós lépésekre lenne szükség.

## Prerequisites

Mielőtt elkezdenénk, győződj meg róla, hogy rendelkezel:

- **Fejlesztői környezettel** – Visual Studio 2022 (vagy bármely kedvelt .NET IDE).  
- **Aspose.OCR for .NET** – letöltheted a [letöltési hivatkozásról](https://releases.aspose.com/ocr/net/).  
- **Dokumentum könyvtárral** – egy mappával a gépeden, ahol a mintakép (`sample_line.png`) található. A kódban cseréld le a „Your Document Directory” szöveget a tényleges útvonalra.

## Import Namespaces

.NET-ben a névterek biztosítják a szükséges osztályok elérését. Add hozzá ezeket a using utasításokat a C# fájlod tetejére:

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

## How to extract text from image using Aspose.OCR

Az alábbiakban a lépésről‑lépésre megvalósítás található. Minden kódrészlet változatlan az eredeti útmutatóból, biztosítva, hogy a logika pontosan megmaradjon.

### Step 1: Initializing Aspose.OCR

```csharp
// ExStart:1
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
// ExEnd:1
```

> **Pro tipp:** Használj abszolút útvonalat vagy a `Path.Combine`-t, hogy elkerüld az útvonal‑elválasztó problémákat különböző operációs rendszerek között.

### Step 2: Recognizing Image Lines

```csharp
// ExStart:3
// Recognize image
string result = api.RecognizeLine(dataDir + "sample_line.png");
// ExEnd:3
```

A `RecognizeLine` metódus egyetlen szövegsorra fókuszál, így ideális, ha ismered a kép elrendezését. Emellett nagyszerű módja a **beolvasott képszöveg olvasásának**, ha a dokumentum egy fontos adatot tartalmazó egyetlen sorból áll.

### Step 3: Displaying Recognized Text

```csharp
// ExStart:4
// Display the recognized text
Console.WriteLine(result);
// ExEnd:4
```

A program futtatása kiírja a kinyert sort a konzolra, ezzel megerősítve, hogy a **szöveg kinyerése képből** művelet sikeres volt.

### Step 4: Completion Message

```csharp
Console.WriteLine("RecognizeLine executed successfully");
```

Ennek az üzenetnek a megjelenése azt jelenti, hogy az OCR folyamat hibamentesen befejeződött.

## How to improve OCR accuracy with Aspose.OCR?

- **Használj nagy felbontású képeket** (300 dpi vagy magasabb).  
- **Alkalmazz képelőfeldolgozást** például binarizálást vagy zajeltávolítást a `api.PreprocessImage` segítségével.  
- **Válaszd ki a megfelelő nyelvet** a `api.Language = OcrLanguage.English;` (vagy a megfelelő nyelvi enum) használatával.  
- **Vágd le a szegélyeket**, hogy eltávolítsd a nem releváns háttért.  

Ezek a finomhangolások segítenek **javítani az OCR pontosságát**, különösen alacsony minőségű beolvasások esetén.

## Common Issues & Solutions

| Probléma | Ok | Megoldás |
|----------|----|----------|
| `FileNotFoundException` | Helytelen `dataDir` útvonal | Ellenőrizd a mappa útvonalát, és győződj meg róla, hogy a `sample_line.png` létezik. |
| Rossz pontosság | Alacsony felbontású kép | Használj nagyobb felbontású forrást vagy előfeldolgozd a képet (pl. binarizálás). |
| Nem támogatott formátum | A kép nincs a támogatott listán | Konvertáld a képet PNG vagy JPEG formátumba, mielőtt meghívod a `RecognizeLine`-t. |

## Frequently Asked Questions

### Q1: Is Aspose.OCR compatible with all image formats?

A1: Az Aspose.OCR széles körű képfájlformátumot támogat, többek között PNG, JPEG, GIF, BMP és továbbiak. A részletes listaért lásd a [dokumentációt](https://reference.aspose.com/ocr/net/).

### Q2: Can I use Aspose.OCR for commercial projects during the trial period?

A2: Igen, a próbaidőszak alatt kereskedelmi projektekben is felfedezheted az Aspose.OCR lehetőségeit. Hosszabb használathoz fontold meg a [licenc megvásárlását](https://purchase.aspose.com/buy).

### Q3: How do I seek help or contribute to the Aspose.OCR community?

A3: Kapcsolatba léphetsz az élénk Aspose.OCR közösséggel a [támogatási fórumon](https://forum.aspose.com/c/ocr/16) segítség és együttműködés érdekében.

### Q4: Are temporary licenses available for Aspose.OCR?

A4: Igen, ideiglenes licenceket szerezhetsz az Aspose.OCR-hez a funkciók kipróbálásához. További részletekért látogasd meg [ezt a linket](https://purchase.aspose.com/temporary-license/).

### Q5: What are the system requirements for Aspose.OCR for .NET?

A5: A teljes rendszerkövetelményekért lásd a [dokumentációt](https://reference.aspose.com/ocr/net/).

## Conclusion

A lépések követésével megtanultad, hogyan **nyerj ki szöveget képfájlokból** az Aspose.OCR for .NET segítségével, különösen az egyes sorok felismerésével. Ez a képesség lehetővé teszi az adatgyűjtés automatizálását, kereshető archívumok létrehozását, és az OCR integrálását bármely .NET alkalmazásba – legyen szó a teljes keretrendszerről vagy a **ASP OCR .NET Core**-ról.

---

**Last Updated:** 2026-02-22  
**Tested With:** Aspose.OCR 24.12 for .NET  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}