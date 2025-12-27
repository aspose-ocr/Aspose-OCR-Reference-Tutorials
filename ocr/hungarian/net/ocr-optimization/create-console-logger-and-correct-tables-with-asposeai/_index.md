---
category: general
date: 2025-12-27
description: Készíts konzol naplózót C#-ban, és engedélyezd az automatikus letöltést
  a helyes táblákhoz az AsposeAI használatával. Tanuld meg, hogyan jelenítheted meg
  a javított táblázat kimenetét néhány lépésben.
draft: false
keywords:
- create console logger
- enable auto download
- how to correct tables
- setup console logger
- display corrected table
language: hu
og_description: Készíts konzolnaplózót C#-ban, és engedélyezd az automatikus letöltést
  a megfelelő táblákra az AsposeAI használatával. Kövesd ezt az útmutatót, hogy gyorsan
  megjeleníthesd a javított táblázat kimenetét.
og_title: Készíts konzolnaplózót és javítsd a táblákat az AsposeAI-val
tags:
- AsposeAI
- C#
- OCR
- Table processing
title: Konzolnapló létrehozása és táblák javítása az AsposeAI-val
url: /hu/net/ocr-optimization/create-console-logger-and-correct-tables-with-asposeai/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Konzol naplózó létrehozása és táblázatok javítása az AsposeAI-val

Valaha is szükséged volt **create console logger** egy C# AI csővezetékhez, de nem tudtad, hol kezdjed? Ebben az útmutatóban végigvezetünk a teljes folyamaton – hogyan hozhatsz létre egy console logger‑t, hogyan engedélyezheted a modellfájlok automatikus letöltését, és végül **how to correct tables**, amelyek az OCR‑ből származnak. A végére képes leszel **display corrected table** eredményeket megjeleníteni a konzolon néhány kódsorral.

Mindent lefedünk a kezdeti naplóbeállítástól a végső takarításig, így nem kell szétválogatott dokumentumok között keresgélned. Nem szükséges előzetes tapasztalat az AsposeAI-val; egy alap C# és .NET ismeret elegendő. Útközben tippeket szórunk a **setup console logger** legjobb gyakorlatairól, beszélünk a szélsőséges esetekről, és megmutatjuk, hogyan kell kinéznie a kimenetnek.

---

## Előfeltételek

- .NET 6.0 vagy újabb (a kód modern nyelvi funkciókat használ)
- Visual Studio 2022 vagy bármely IDE, amely támogatja a C# projekteket
- **Aspose.AI** NuGet csomag telepítve (`Install-Package Aspose.AI`)
- **Aspose.OCR** NuGet csomag telepítve (`Install-Package Aspose.OCR`)
- Egy minta OCR eredményobjektum (`ocrResult`) egy korábbi Aspose.OCR hívásból

Ha bármelyik hiányzik, állj meg most és szerezd be őket – később meg fogod köszönni magadnak.

## 1. lépés: Console logger létrehozása és AsposeAI inicializálása

Az első dolog, amire szükségünk van, egy naplózó, amely közvetlenül a konzolra ír. Ez megkönnyíti a hibakeresést és élő visszajelzést ad, amíg az AI motor fut.

```csharp
using Aspose.AI;
using Aspose.AI.PostProcessor;
using Aspose.OCR;

// Step 1: Create a logger that writes to the console
ILogger consoleLogger = new ConsoleLogger();

// Step 2: Initialise the AsposeAI engine with the logger
AsposeAI asposeAI = new AsposeAI(consoleLogger);
```

**Miért fontos:**  
`ConsoleLogger` implementálja az `ILogger` interfészt, így az AsposeAI belső üzenetei (modell betöltése, post‑processor állapota, hibák) azonnal megjelennek a terminálodban. Ez a legegyszerűbb módja a **setup console logger** beállításának anélkül, hogy külső naplózási keretrendszereket vonnánk be.

> **Pro tip:** Ha később fájlnaplózásra van szükséged, egyszerűen cseréld le a `ConsoleLogger`‑t egy egyedi naplózóra, amely implementálja az `ILogger`‑t – a kód többi része érintetlen marad.

## 2. lépés: Automatikus letöltés engedélyezése az AI modellekhez

Az AsposeAI képes a szükséges modellfájlokat futás közben letölteni. Ennek bekapcsolása megspórolja a nagy bináris fájlok kézi letöltését.

```csharp
// Step 3: (Optional) Configure automatic model download and set the model directory
AsposeAIModelConfig modelConfig = new AsposeAIModelConfig
{
    AllowAutoDownload = true,               // <‑‑ enable auto download
    DirectoryModelPath = "YOUR_DIRECTORY"   // change to a writable folder
};
```

**Mi mehet félre?**  
Ha a `DirectoryModelPath` egy csak olvasható helyre mutat, az automatikus letöltés hibára fut, és kivételt látsz a konzolon. Győződj meg arról, hogy a mappa létezik, és az alkalmazásnak írási jogosultsága van.

## 3. lépés: Táblázat post‑processor létrehozása (how to correct tables)

Az OCR‑ből kinyert táblázatok gyakran rendezetlenek – egyesített cellák, hiányzó szegélyek vagy rosszul igazított szöveg. Az AsposeAI `TableAIProcessor` képes ezeket automatikusan megtisztítani.

```csharp
// Step 4: Create a table post‑processor that lets the engine decide when to run correction
TableAIProcessor tableProcessor = new TableAIProcessor(AITableDetectionMode.AUTO);
```

**Miért AUTO mód?**  
`AITableDetectionMode.AUTO` lehetővé teszi, hogy a motor megvizsgálja az OCR kimenetet, és eldöntse, szükséges‑e a javítás. Ha inkább manuális vezérlést szeretnél, használhatod a `MANUAL` módot, és saját magad hívhatod meg a `RunCorrection()`‑t.

## 4. lépés: Post‑processor és konfigurációjának csatolása

Most mindent összekapcsolunk – naplózót, modell konfigurációt és a táblázat processzort.

```csharp
// Step 5: Attach the post‑processor and its configuration to the AI engine
asposeAI.SetPostProcessor(tableProcessor, modelConfig);
```

Ekkor az AI motor tudja, *hol* tárolja a modelleket, *hogyan* naplózzon, és *milyen* post‑processzort alkalmazzon. Ez egy tiszta felelősségtér elválasztás, amely megkönnyíti a jövőbeni módosításokat.

## 5. lépés: Post‑processor futtatása az OCR eredményeden

Feltételezve, hogy már rendelkezel egy `ocrResult` objektummal az Aspose.OCR‑ból, egyszerűen add át a motorba.

```csharp
// Step 6: Run the post‑processor on the OCR result returned by Aspose.OCR
asposeAI.RunPostprocessor(ocrResult);
```

**Éles eset figyelmeztetés:**  
Ha az `ocrResult` nem tartalmaz táblázatot, a processzor csendben kihagyja a javítást. Utána ellenőrizheted a `tableProcessor.GetResult().Count` értékét, hogy megbizonyosodj arról, valóban történt-e feldolgozás.

## 6. lépés: **display corrected table** kimenet lekérése és megjelenítése

Végül, szedjük ki a megtisztított táblázat szövegét, és nyomtassuk ki a konzolra.

```csharp
// Step 7: Retrieve and display the corrected table text
Console.WriteLine("Corrected table output:");
Console.WriteLine(tableProcessor.GetResult()[0].RecognitionText);
```

A kimenet valahogy így fog kinézni (a forrásképtől függően):

```
Corrected table output:
| Item   | Quantity | Price |
|--------|----------|-------|
| Apple  | 10       | $1.20 |
| Banana | 5        | $0.80 |
```

Ha üres karakterláncot látsz, ellenőrizd újra, hogy az OCR valóban észlelt-e táblázatot, és hogy a `AllowAutoDownload` sikeres volt-e.

## 7. lépés: Erőforrások tisztítása

A jó polgári felelősség azt jelenti, hogy a befejezés után felszabadítod a nehéz objektumokat.

```csharp
// Step 8: Release resources used by the AI engine
asposeAI.Dispose();
```

Ennek a lépésnek a kihagyása fájlkezelőket hagy nyitva, különösen Windows rendszeren, ahol a modellfájlok zárolva maradnak.

## Teljes működő példa

Az alábbiakban a teljes programot találod, amelyet beilleszthetsz egy új konzol projektbe. Cseréld ki a `"YOUR_DIRECTORY"`-t egy valós útvonalra, és győződj meg róla, hogy az `ocrResult` fel van töltve, mielőtt meghívod a `RunPostprocessor`‑t.

```csharp
using System;
using Aspose.AI;
using Aspose.AI.PostProcessor;
using Aspose.OCR;

namespace AsposeAITableCorrection
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create a console logger
            ILogger consoleLogger = new ConsoleLogger();

            // 2️⃣ Initialise AsposeAI with the logger
            AsposeAI asposeAI = new AsposeAI(consoleLogger);

            // 3️⃣ Configure auto‑download (optional but recommended)
            AsposeAIModelConfig modelConfig = new AsposeAIModelConfig
            {
                AllowAutoDownload = true,
                DirectoryModelPath = @"C:\AsposeModels" // <-- change this
            };

            // 4️⃣ Create the table processor (auto‑detect mode)
            TableAIProcessor tableProcessor = new TableAIProcessor(AITableDetectionMode.AUTO);

            // 5️⃣ Attach processor and config
            asposeAI.SetPostProcessor(tableProcessor, modelConfig);

            // 6️⃣ Obtain OCR result (replace with your own OCR call)
            // Example placeholder – you should have this from Aspose.OCR already
            OcrResult ocrResult = GetOcrResultSomehow();

            // 7️⃣ Run post‑processor on the OCR output
            asposeAI.RunPostprocessor(ocrResult);

            // 8️⃣ Display corrected table
            Console.WriteLine("Corrected table output:");
            if (tableProcessor.GetResult().Count > 0)
            {
                Console.WriteLine(tableProcessor.GetResult()[0].RecognitionText);
            }
            else
            {
                Console.WriteLine("No tables were detected or corrected.");
            }

            // 9️⃣ Clean up
            asposeAI.Dispose();
        }

        // Dummy method – replace with your actual OCR logic
        static OcrResult GetOcrResultSomehow()
        {
            // For illustration only
            OcrEngine engine = new OcrEngine();
            engine.Image = ImageStream.FromFile("sample-table.png");
            return engine.Recognize();
        }
    }
}
```

**Várható konzol kimenet** (egyszerű táblázat képet feltételezve):

```
Corrected table output:
| Name   | Age | City      |
|--------|-----|-----------|
| Alice  | 30  | New York  |
| Bob    | 25  | Seattle   |
```

## Gyakori kérdések és válaszok

- **Szükségem van internetkapcsolatra az automatikus letöltéshez?**  
  Igen. Az első alkalommal, amikor a modellt kérik, az AsposeAI a CDN‑hez fordul. Miután a fájl a `DirectoryModelPath`‑ba került, a későbbi futtatások offline módúak.

- **Mi van, ha a táblázatom egyesített cellákat tartalmaz?**  
  Az AI modell megpróbálja szétválasztani az egyesített cellákat a vizuális jelek alapján. Ha az eredmény hibásnak tűnik, fontold meg a kép előfeldolgozását (kontraszt növelése, forgatás kiegyenlítése) az OCR előtt.

- **Feldolgozhatok több táblázatot egyszerre?**  
  Természetesen. A `tableProcessor.GetResult()` egy listát ad vissza; iterálj rajta, hogy minden táblázatot kiírd.

- **A `ConsoleLogger` szálbiztos?**  
  Közvetlenül a `System.Console`‑ra ír, amely egyszerű írások esetén szálbiztos. Nagy, több szálas esetekben egy szinkronizációval rendelkező egyedi naplózó lehet előnyösebb.

## Következő lépések és kapcsolódó témák

Most, hogy ismered a **how to correct tables** folyamatot, lehet, hogy szeretnél:

- **Enable auto download** más AsposeAI modellekhez (pl. nyelvi fordítás).
- **Setup console logger** különböző naplózási szintekkel (Info, Warning, Error) a finomabb vezérléshez.
- Fedezd fel a **display corrected table** megjelenítését egy GUI‑ban (WinForms vagy WPF) a konzol helyett.
- Kombináld a táblázatjavítást **data extraction**‑nel, hogy közvetlenül adatbázisba tápláld.

Mindegyik ezek közül az általunk felépített alapra épül, szóval bátran kísérletezz.

## Összegzés

Végigvezettük a teljes életciklust a **creating console logger**, az automatikus letöltés engedélyezésével és az AsposeAI-val történő **correcting tables** során, egy tiszta módszerrel zárva a **

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}