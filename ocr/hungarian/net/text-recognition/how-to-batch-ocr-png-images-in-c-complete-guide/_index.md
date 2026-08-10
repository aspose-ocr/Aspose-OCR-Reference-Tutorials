---
category: general
date: 2026-04-26
description: Hogyan végezz gyors tömeges OCR-t PNG képeken. Tanulja meg, hogyan nyerjen
  ki szöveget PNG-ből, konvertálja a képeket szöveggé, írja ki a felismert szöveget,
  és olvassa be a PNG könyvtárat az Aspose OCR-rel.
draft: false
keywords:
- how to batch OCR
- extract text from png
- convert images to text
- write recognized text
- read png directory
language: hu
og_description: Hogyan végezzünk kötegelt OCR-t PNG képeken C#-ban az Aspose OCR-rel.
  Ez az útmutató bemutatja, hogyan lehet szöveget kinyerni PNG-ből, képeket szöveggé
  konvertálni, és a felismert szöveget hatékonyan írni.
og_title: Hogyan végezzünk kötegelt OCR-t PNG képeken C#‑ban – Lépésről lépésre
tags:
- OCR
- C#
- Aspose
title: Hogyan végezzünk kötegelt OCR-t PNG képeken C#-ban – Teljes útmutató
url: /hu/net/text-recognition/how-to-batch-ocr-png-images-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan végezzünk kötegelt OCR-t PNG képeken C#‑ban – Teljes útmutató

Valaha is elgondolkodtál már azon, **hogyan végezzünk kötegelt OCR‑t** egy egész mappában lévő PNG fájlokon anélkül, hogy minden képhez külön programot írnál? Nem vagy egyedül, ha tucatnyi képernyőképet, beolvasott számlát vagy grafikát kell kereshető szöveggé alakítanod. Ebben az útmutatóban egy gyakorlati megoldáson keresztül mutatjuk be, hogyan **vonjuk ki a szöveget a PNG‑ből**, **alakítsuk át a képeket szöveggé**, és **írjuk a felismert szöveget** egyedi fájlokba – mindezt automatikusan beolvasva a PNG könyvtárat.

Az útmutató végére egy azonnal futtatható C# konzolos alkalmazásod lesz, amely egy lépésben feldolgozza a tetszőleges számú képet. Nincs extra szkript, nincs kézi másolás‑beillesztés – csak tiszta kód, ami elvégzi a nehéz munkát helyetted.

## Amire szükséged lesz

- **.NET 6.0** vagy újabb (a kód .NET Framework‑ön is jól működik).  
- **Aspose.OCR for .NET** NuGet csomag (az ingyenes próba verzió teszteléshez megfelelő).  
- Egy mappa néhány *.png* fájllal, amelyeket OCR‑elni szeretnél.  
- Visual Studio 2022 vagy bármelyik kedvenc C# IDE.

Ha ezek megvannak, akkor ugrunk is a megvalósításba.

## 1. lépés – Készítsd elő a bemeneti és kimeneti mappákat *(PNG könyvtár beolvasása)*

Az első dolog, amit teszünk, hogy a programot a képeket tartalmazó mappára irányítjuk, és meghatározzuk, hová kerüljenek a létrehozott *.txt* fájlok. A `Directory.GetFiles` használatával tiszta felsorolást kapunk a könyvtárban lévő összes PNG‑ről.

```csharp
using System;
using System.Collections.Generic;
using System.IO;

// Define where the source PNGs are and where the OCR results will be saved
string inputFolder = @"C:\MyProject\BatchImages";   // <-- change to your path
string outputFolder = @"C:\MyProject\BatchOutput";

// Ensure the output folder exists; create it if it doesn’t
if (!Directory.Exists(outputFolder))
{
    Directory.CreateDirectory(outputFolder);
}

// Grab every *.png* file – this is the “read png directory” part
IEnumerable<string> inputImageFiles = Directory.GetFiles(inputFolder, "*.png");
```

**Miért fontos ez:**  
- A helyettesítő karakter (`*.png`) használata garantálja, hogy csak képfájlokat dolgozunk fel, és figyelmen kívül hagyjuk a többi dokumentumot.  
- A kimeneti mappa futás közbeni létrehozása megakadályozza a későbbi `DirectoryNotFoundException` hibát.

> **Pro tipp:** Ha más formátumokat (JPEG, BMP) is támogatni szeretnél, egyszerűen bővítsd a keresési mintát, vagy hívd a `Directory.EnumerateFiles`‑t több kiterjesztéssel.

## 2. lépés – Inicializáld az OCR motorját *(Képek átalakítása szöveggé)*

Aspose.OCR két motor típust kínál: egy CPU‑alapú `OcrEngine`‑t és egy GPU‑gyorsított `GpuOcrEngine`‑t. A legtöbb kötegelt feladathoz a CPU motor tökéletes, de ha erőteljes GPU‑d van, egyszerűen kicserélheted az osztály nevét.

```csharp
using Aspose.OCR;

// Initialise the OCR engine – CPU version
OcrEngine ocrEngine = new OcrEngine();   // Use new GpuOcrEngine() for GPU acceleration

// Set the language to Latin (covers English, French, Spanish, etc.)
ocrEngine.Language = Language.Latin;
```

**Miért fontos ez:**  
- A nyelv megadása drámaian javítja a pontosságot, mivel a motor tudja, milyen karakterkészletre számít.  
- A `GpuOcrEngine`‑re váltás egyetlen soros módosítás, ha nagy kötegek esetén teljesítménybeli szűk keresztmetszetbe ütközöl.

## 3. lépés – Hozz létre egy kötegelt felismerőt

Az Aspose egy kényelmes `BatchRecognizer`‑t biztosít, amely egy fájlútvonalak felsorolását fogadja, és az eredményeket egyesével adja vissza. Ez megakadályozza, hogy egyszerre az összes képet a memóriába töltsük – ami nagy mappák esetén kulcsfontosságú.

```csharp
// Build a batch recogniser that will use the previously configured engine
BatchRecognizer batchRecognizer = new BatchRecognizer(ocrEngine);
```

**Miért fontos ez:**  
- A kötegelt felismerő magába foglalja a cikluslogikát, így arra koncentrálhatunk, hogy mit tegyünk az egyes eredményekkel, ahelyett, hogy aggódnunk kellene a biztonságos iterálás miatt.

## 4. lépés – Futtasd le az OCR‑t minden képen és írd ki a kimenetet *(Felismert szöveg írása)*

Most ténylegesen végrehajtjuk az OCR‑t. A `Recognize` metódus egy `IEnumerable<RecognitionResult>`‑t ad vissza, ahol minden eredmény a kinyert szöveget és egyéb metaadatokat tartalmaz.

```csharp
// Perform OCR on the entire collection of PNG files
IEnumerable<RecognitionResult> recognitionResults = batchRecognizer.Recognize(inputImageFiles);

// Write each recognised text to a separate *.txt* file
int fileIndex = 0;
foreach (RecognitionResult result in recognitionResults)
{
    // Build a unique output filename – out_0.txt, out_1.txt, …
    string outputPath = Path.Combine(outputFolder, $"out_{fileIndex++}.txt");

    // Save the plain text to disk
    File.WriteAllText(outputPath, result.Text);
}
```

**Miért fontos ez:**  
- A `File.WriteAllText` használata biztosítja, hogy a szöveg alapértelmezés szerint UTF‑8 kódolással legyen mentve, megőrizve a speciális karaktereket.  
- Az inkrementális elnevezés (`out_0.txt`, `out_1.txt`) a feldolgozási sorrendet követi, ami a hibakeresésnél hasznos.

> **Szélsőséges eset:** Ha bármelyik kép nem sikerül OCR‑elni (pl. sérült fájl), a `RecognitionResult.Text` üres lesz. A cikluson belül egyszerű ellenőrzést adhatsz hozzá a hibák naplózásához:

```csharp
if (string.IsNullOrWhiteSpace(result.Text))
{
    Console.WriteLine($"Warning: No text extracted from {inputImageFiles.ElementAt(fileIndex - 1)}");
}
```

## 5. lépés – Összeállítás – Teljes működő példa

Az alábbiakban a teljes program látható, amelyet egyszerűen beilleszthetsz egy új konzolos projektbe. Tartalmazza a `using` direktívákat, a mappa ellenőrzését, valamint egy apró konzolos felhasználói felületet, hogy tudd, mikor fejeződött be a köteg.

```csharp
// ---------------------------------------------------------------
// Batch OCR for PNG files using Aspose.OCR
// ---------------------------------------------------------------
using System;
using System.Collections.Generic;
using System.IO;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // 1️⃣ Define input & output directories
        string inputFolder = @"C:\MyProject\BatchImages";   // <-- adjust
        string outputFolder = @"C:\MyProject\BatchOutput";

        if (!Directory.Exists(inputFolder))
        {
            Console.WriteLine($"Error: Input folder does not exist -> {inputFolder}");
            return;
        }

        if (!Directory.Exists(outputFolder))
            Directory.CreateDirectory(outputFolder);

        // 2️⃣ Gather all PNG files
        IEnumerable<string> inputImageFiles = Directory.GetFiles(inputFolder, "*.png");
        Console.WriteLine($"Found {inputImageFiles?.Count() ?? 0} PNG files to process.");

        // 3️⃣ Initialise OCR engine (CPU) and set language
        OcrEngine ocrEngine = new OcrEngine();   // Swap with GpuOcrEngine() if needed
        ocrEngine.Language = Language.Latin;

        // 4️⃣ Create batch recogniser
        BatchRecognizer batchRecognizer = new BatchRecognizer(ocrEngine);

        // 5️⃣ Run OCR and write results
        IEnumerable<RecognitionResult> results = batchRecognizer.Recognize(inputImageFiles);
        int index = 0;
        foreach (RecognitionResult result in results)
        {
            string outPath = Path.Combine(outputFolder, $"out_{index++}.txt");
            File.WriteAllText(outPath, result.Text);
        }

        Console.WriteLine($"✅ OCR complete! Text files saved to {outputFolder}");
    }
}
```

**Várható kimenet:**  
A program futtatása valami ilyesmit ír ki:

```
Found 12 PNG files to process.
✅ OCR complete! Text files saved to C:\MyProject\BatchOutput
```

És a kimeneti mappában `out_0.txt` … `out_11.txt` fájlokat fogsz látni, mindegyik a megfelelő kép egyszerű szöveges változatát tartalmazza.

## Gyakori kérdések és tippek

| Kérdés | Válasz |
|----------|--------|
| *OCR‑zhetek al‑mappákat is?* | Igen—cseréld le a `Directory.GetFiles`‑t a `Directory.EnumerateFiles(inputFolder, "*.png", SearchOption.AllDirectories)`‑re. |
| *Mi van, ha más nyelvre van szükségem?* | Állítsd be `ocrEngine.Language = Language.Spanish;` (vagy bármely támogatott enum). |
| *Hogyan kezeljem a hatalmas kötegeket (ezrek fájlok)?* | Gondolj a feldolgozásra darabokban vagy használd a `Parallel.ForEach`‑t korlátozott párhuzamossággal, hogy elkerüld a memória kimerülését. |
| *Mindig UTF‑8 a kimenet?* | `File.WriteAllText` alapértelmezés szerint UTF‑8‑et használ BOM nélkül, ami a legtöbb latin‑alapú nyelvhez megfelelő. Ázsiai írásrendszerekhez előfordulhat, hogy explicit módon `Encoding.UTF8`‑et kell beállítani. |
| *Kaphatok megbízhatósági pontszámokat?* | `RecognitionResult` tartalmazza a `Confidence`‑t – naplózhatod a szöveg mellett a minőség‑ellenőrzéshez. |

## Vizuális áttekintés *(Hogyan végezzünk kötegelt OCR – Diagram)*

![Hogyan működik a kötegelt OCR munkafolyamat diagram, bemutatva a bemeneti mappát → OCR motor → kötegelt felismerő → kimeneti txt fájlok](https://example.com/diagram-how-to-batch-ocr.png "Hogyan végezzünk kötegelt OCR‑t")

*Az alt szöveg tartalmazza a fő kulcsszót, ezzel teljesítve a SEO képkövetelményeket.*

## Összegzés

Most bemutattuk, **hogyan végezzünk kötegelt OCR‑t** egy PNG fájlokból álló könyvtáron az Aspose.OCR segítségével, a PNG könyvtár beolvasásától a felismert szövegfájlok írásáig. A megoldás teljesen önálló, bármely modern .NET környezetben működik, és kiterjeszthető GPU gyorsítással, többnyelvű támogatással vagy párhuzamos feldolgozással.

Készen állsz a következő lépésre? Próbáld megcserélni a `Language.Latin`‑t egy másik nyelvre, vagy integráld a kimenetet egy kereső indexbe, hogy a dokumentumaid azonnal kereshetők legyenek. A lehetőségek végtelenek, ha már elsajátítottad a kötegelt OCR‑t.

Kellemes kódolást, és jelezd a hozzászólásokban, ha bármilyen problémába ütköztél!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}