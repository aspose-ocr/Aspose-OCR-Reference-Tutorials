---
category: general
date: 2026-01-01
description: Az orosz szöveg azonnali felismerése az Aspose OCR C# használatával.
  Tanulja meg a kínai szöveg felismerését, a PDF oldalszám olvasását, és a PDF oldal
  szövegének konvertálását egyetlen útmutatóban.
draft: false
keywords:
- recognize russian text
- aspose ocr c#
- recognize chinese text
- read pdf page count
- convert pdf page text
language: hu
og_description: Ismerje fel gyorsan az orosz szöveget az Aspose OCR C# segítségével.
  Ez az útmutató azt is bemutatja, hogyan lehet felismerni a kínai szöveget, kiolvasni
  a PDF oldalszámát, és átalakítani a PDF oldal szövegét.
og_title: Orosz szöveg felismerése az Aspose OCR C#-val – Teljes útmutató
tags:
- Aspose OCR
- C#
- PDF processing
title: Orosz szöveg felismerése Aspose OCR C#-val – Teljes többoldalas PDF útmutató
url: /hu/net/text-recognition/recognize-russian-text-with-aspose-ocr-c-full-multi-page-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# orosz szöveg felismerése Aspose OCR C#‑vel – Teljes többoldalas PDF útmutató

Valaha is szükséged volt **orosz szöveg felismerésére** egy olyan PDF-ben, amely nyelveket kever, és elgondolkodtál, hogyan lehet ezt megoldani anélkül, hogy minden oldalhoz külön eszközt kellene használnod? Nem vagy egyedül. Sok valós projektben egyetlen PDF-et kapsz, amely különböző oldalakon angolt, oroszt és még kínait is tartalmaz, és mégis egyetlen, tiszta szövegkimenetet szeretnél.

Ebben az útmutatóban pontosan megmutatjuk, hogyan **orosz szöveg felismerése** (és más nyelveket) használva a **Aspose OCR C#**‑t, miközben bemutatjuk, hogyan **pdf oldal számának olvasása**, **kínai szöveg felismerése**, és **pdf oldal szövegének konvertálása** egy kényelmes konzol kiíratásba. Nincsenek külső szolgáltatások, rejtett lépések – csak tiszta C# kód, amelyet egyszerűen másolhatsz és futtathatsz.

> **Mit fogsz megtanulni**  
> * Egy futtatható C# konzolalkalmazás, amely többoldalas PDF-et dolgoz fel.  
> * Oldalankénti nyelvválasztás (orosz, kínai, angol).  
> * Technikák a PDF oldal számának lekérdezésére és az egyes oldalak szövegének kinyerésére.  
> * Tippek, buktatók és kiegészítések, amelyeket saját projektjeidben alkalmazhatsz.  

## Előkövetelmények

- .NET 6.0 vagy újabb (a kód .NET Framework 4.7+‑on is működik).  
- **Aspose.OCR for .NET** NuGet csomag telepítve (`dotnet add package Aspose.OCR`).  
- Egy PDF fájl, amely vegyes nyelveket tartalmaz; a bemutatóhoz a `mixed_lang.pdf` fájlt használjuk.  
- Alapvető ismeretek a C# konzolalkalmazásokról.

Ha valamelyik hiányzik, szerezd be a legújabb Aspose OCR‑t a NuGet‑ről, és helyezd a PDF‑et egy olyan helyre, amely elérhető a projekt mappájából.

## 1. lépés – Az Aspose OCR motor inicializálása

Az első dolog, amire szükséged van, egy `OcrEngine` példány. Ez az objektum tárolja az összes beállítást (például a nyelvet), és elvégzi a nehéz munkát.

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;

class MultiPageDemo
{
    static void Main()
    {
        // Create the OCR engine – this is where we’ll set language per page
        OcrEngine ocrEngine = new OcrEngine();
```

> **Miért fontos:**  
> A motor újrahasználható, így nem pazarolunk memóriát minden oldalhoz új példány létrehozásával. Újrahasználata lehetővé teszi a nyelv dinamikus változtatását, ami elengedhetetlen a **orosz szöveg felismeréséhez** egy oldalon és a **kínai szöveg felismeréséhez** egy másikon.  

## 2. lépés – A PDF betöltése és az oldalak számának meghatározása

Mielőtt elkezdenénk a felismerést, szükségünk van a PDF objektumra és az oldal számra. Az Aspose OCR minden oldalt `OcrImage`‑ként kezel.

```csharp
        // Load the multi‑page PDF
        OcrImage multiPageImage = OcrImage.FromFile(@"YOUR_DIRECTORY/mixed_lang.pdf");

        // Print the total number of pages – this answers the “read pdf page count” question
        Console.WriteLine($"PDF contains {multiPageImage.PageCount} pages.");
```

> **Tipp:** Ha a PDF nagy, érdemes előbb leolvasni a számot, és eldönteni, hogy az összes oldalt vagy csak egy részhalmazt dolgozzuk fel.  

## 3. lépés – Minden oldal hozzárendelése a kívánt nyelvhez

Az Aspose OCR sok nyelvet támogat, de meg kell mondanod, melyiket használja az egyes oldalakhoz. Az alábbiakban létrehozunk egy `Dictionary<int, OcrLanguage>`‑t, ahol a kulcs a nulláról induló oldalindex.

```csharp
        // Define which language each page should be read with
        var languageMap = new Dictionary<int, OcrLanguage>
        {
            { 0, OcrLanguage.English },   // Page 1 – English
            { 1, OcrLanguage.Russian },   // Page 2 – Russian (our primary focus)
            { 2, OcrLanguage.Chinese }    // Page 3 – Chinese
        };
```

> **Miért kulcsfontosságú:**  
> Ezen térkép nélkül az OCR motor egyetlen alapértelmezett nyelvet próbálna minden oldalra, ami torz kimenetet eredményezne orosz vagy kínai szöveg esetén. Ez a lépés közvetlenül lehetővé teszi a **orosz szöveg felismerését** és a **kínai szöveg felismerését** helyesen.  

## 4. lépés – Az összes oldal bejárása, nyelv beállítása és szöveg felismerése

Most minden oldalon végigiterálunk, a térkép alapján váltjuk a nyelvet, és meghívjuk a `Recognize`‑t. Az eredményt az `OcrResult` tárolja, amelyből a tiszta szöveget nyerjük ki.

```csharp
        // Process each page one by one
        for (int pageIndex = 0; pageIndex < multiPageImage.PageCount; pageIndex++)
        {
            // Choose language – default to English if we haven’t specified one
            ocrEngine.Settings.Language = languageMap.ContainsKey(pageIndex)
                                          ? languageMap[pageIndex]
                                          : OcrLanguage.English;

            // Perform OCR on the current page
            var pageResult = ocrEngine.Recognize(multiPageImage.GetPage(pageIndex));

            // Output the recognized text – this is the “convert pdf page text” step
            Console.WriteLine($"--- Page {pageIndex + 1} ({ocrEngine.Settings.Language}) ---");
            Console.WriteLine(pageResult.Text);
            Console.WriteLine(); // Blank line for readability
        }
    }
}
```

### Várható konzol kimenet

```
PDF contains 3 pages.
--- Page 1 (English) ---
This is an English paragraph on the first page.

--- Page 2 (Russian) ---
Это русский текст на второй странице.

--- Page 3 (Chinese) ---
这是第三页的中文文本。
```

> **A folyamat magyarázata:**  
> * A ciklus tiszteletben tartja a korábban kiírt **pdf oldal számának olvasása** értéket.  
> * Az `ocrEngine.Settings.Language` minden iterációban történő cseréjével biztosítjuk a pontos **orosz szöveg felismerését** a 2. oldalon és a **kínai szöveg felismerését** a 3. oldalon.  
> * A `Console.WriteLine` utasítások hatékonyan **pdf oldal szövegének konvertálását** végzik ember által olvasható karakterlánccá.  

## 5. lépés – Futtatás, ellenőrzés és finomhangolás

1. A projekt felépítése (`dotnet build`).  
2. Futtatás (`dotnet run`).  
3. A konzol kimenet összehasonlítása az eredeti PDF‑el.  

Ha hiányzó karaktereket észlelsz, fontold meg:

- **Az OCR pontosságának növelését** a `ocrEngine.Settings.DetectTextOrientation = true;` beállítással.  
- **Egy egyedi nyelvi csomag biztosítását**, ha a beépített orosz vagy kínai szótárak elavultak.  
- **A DPI módosítását** a PDF betöltésekor (`OcrImage.FromFile(path, 300)`), ami javíthatja a felismerést alacsony felbontású beolvasásoknál.  

## Bónusz: Szélsőséges esetek kezelése

### Mi van, ha egy oldal nyelve nincs a térképben?

A kód már most visszaesik az angolra, de hozzáadhatsz egy tartalékot is, amely figyelmeztetést naplóz:

```csharp
if (!languageMap.TryGetValue(pageIndex, out var lang))
{
    Console.WriteLine($"Warning: No language defined for page {pageIndex + 1}. Using English.");
    lang = OcrLanguage.English;
}
ocrEngine.Settings.Language = lang;
```

### Feldolgozhatunk-e több mint három nyelvet tartalmazó PDF‑eket?

Természetesen. Bővítsd a `languageMap`‑et további indexekkel és támogatott `OcrLanguage` értékekkel (pl. `OcrLanguage.French`). A ciklus bármennyi oldalt kezelni fog.

### Hogyan exportáljuk az eredményeket fájlba a konzol helyett?

Cseréld le a `Console.WriteLine` hívásokat `File.AppendAllText("output.txt", …)`‑re, vagy használj egy `StringBuilder`‑t, amelyet a ciklus után egyszer írsz ki.

## Kép illusztráció

![recognize russian text example](/images/recognize-russian-text.png "Screenshot showing OCR output for Russian text")

*A fenti kép bemutatja a konzol kimenetet, amikor **orosz szöveg felismerése** történik egy vegyes nyelvű PDF‑en.*

## Összegzés

Áttekintettünk egy teljes, vég‑től‑végig példát, amely megmutatja, hogyan **orosz szöveg felismerése** (és a **kínai szöveg felismerése**) egy többoldalas PDF‑ből az **Aspose OCR C#** használatával. A PDF oldal számának leolvasásával, az egyes oldalak megfelelő nyelvhez való hozzárendelésével és a dokumentum bejárásával **pdf oldal szövegének konvertálását** egyszerű karakterláncokká tudod elvégezni, amelyek készen állnak a tárolásra, indexelésre vagy további elemzésre.

Röviden:

- **Inicializáld** egyetlen `OcrEngine`‑t.  
- **Töltsd be** a PDF‑et és **olvasd ki a pdf oldal számát**.  
- **Térképezd** az oldalakat nyelvekre (orosz, kínai, stb.).  
- **Iterálj**, állítsd be az `ocrEngine.Settings.Language`‑t, és **ismerd fel** minden oldalt.  
- **Kimenet** vagy mentsd el a kinyert szöveget.

Nyugodtan alkalmazd ezt a mintát nagyobb dokumentumokra, adj hozzá hibakezelést, vagy csatlakoztasd az eredményeket egy keresőindexhez. A lényeges ötlet – oldalankénti nyelvválasztás – változatlan marad, és ez teszi lehetővé a megbízható **orosz szöveg felismerését** vegyes nyelvű PDF‑ekben.

Másik szituációd van, például képek beolvasása PDF‑ek helyett? Ugyanaz a motor működik; csak cseréld le az `OcrImage.FromFile`‑t `OcrImage.FromStream`‑re vagy `FromBitmap`‑ra. Boldog kódolást, és legyen az OCR‑ed mindig pontos!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}