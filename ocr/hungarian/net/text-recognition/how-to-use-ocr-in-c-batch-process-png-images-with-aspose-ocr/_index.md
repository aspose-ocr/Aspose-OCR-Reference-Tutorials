---
category: general
date: 2026-02-14
description: Hogyan használjunk OCR-t C#-ban a PNG fájlok szövegének gyors kinyeréséhez.
  Tanulja meg a kötegelt OCR képeket, több kép feldolgozását, és használja az Aspose
  OCR C#-t egyetlen útmutatóban.
draft: false
keywords:
- how to use OCR
- extract text png
- batch OCR images
- process multiple images
- aspose OCR c#
language: hu
og_description: Hogyan használjunk OCR-t C#-ban az Aspose OCR C#-val. Ez az útmutató
  bemutatja, hogyan lehet szöveget kinyerni PNG-fájlokból, kötegelt OCR-t végrehajtani
  képeken, és hatékonyan feldolgozni több képet.
og_title: Hogyan használjuk az OCR-t C#-ban – Tömeges PNG szövegkivonás
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Hogyan használjuk az OCR-t C#-ban – PNG képek kötegelt feldolgozása az Aspose
  OCR-rel
url: /hu/net/text-recognition/how-to-use-ocr-in-c-batch-process-png-images-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan használjuk az OCR-t C#-ban – PNG képek kötegelt feldolgozása az Aspose OCR-rel

Gondoltad már valaha, **hogyan használjuk az OCR-t**, hogy szöveget nyerjünk ki egy csomó PNG fájlból anélkül, hogy minden egyeshez külön rutint írnánk? Nem vagy egyedül. Sok fejlesztő akad el, amikor nagy mennyiségben kell **PNG szöveget kinyerni**, különösen, ha a képek egy mappában vannak, és minden fájlhoz el kell indítani az OCR motorját.  

Ebben az útmutatóban végigvezetünk egy teljes, azonnal futtatható megoldáson, amely **kötegelt OCR képeket**, **több képet** dolgoz fel párhuzamosan, és kihasználja a hatékony **Aspose OCR C#** könyvtárat. A végére egyetlen futtatható programod lesz, amely bármennyi PNG-t beolvas, kinyeri a szöveget, és kiírja az eredményeket a konzolra – mindezt csak néhány kódsorral.

## Előfeltételek

- .NET 6.0 vagy újabb (a kód működik .NET Core‑ral és .NET Framework‑kel is)  
- Érvényes Aspose.OCR for .NET licenc (vagy ingyenes próba) – a Aspose weboldaláról szerezhető be.  
- Egy mappa, amely tartalmazza a beolvasni kívánt PNG fájlokat.  
- Visual Studio 2022 (vagy bármely C#‑kompatibilis IDE).  

További NuGet csomagokra nincs szükség a `Aspose.OCR`-on kívül.

## 1. lépés: Hogyan használjuk az OCR-t – Az Aspose OCR motor inicializálása

Az első dolog, amire szükséged van, egy `Engine` osztály példány. Ez az objektum elrejti a mögöttes OCR technológiát, és futtatható CPU-n vagy GPU-n, a hardvertől és a licencetől függően.

```csharp
using System;
using System.Collections.Generic;
using System.Collections.Concurrent;
using System.Threading.Tasks;
using Aspose.OCR;

// Create an OCR engine (CPU by default; GPU can be enabled via EngineSettings if licensed)
var ocrEngine = new Engine();
```

*Miért fontos:* A motor egyszeri inicializálása és szálakon való újrafelhasználása memóriát takarít meg, és elkerüli az OCR modellek többszöri betöltésének terheit. Emellett biztosítja a beállítások konzisztenciáját minden képnél.

## 2. lépés: PNG szöveg kinyerése – Képek útvonalainak összegyűjtése

Ezután egy fájlútvonal-gyűjteményre van szükség. Egy valódi projektben dinamikusan olvashatod be a könyvtárat, de a tisztaság kedvéért felsorolunk néhány mintafájlt.

```csharp
// List the PNG files you want to process
var imagePaths = new List<string>
{
    "YOUR_DIRECTORY/img1.png",
    "YOUR_DIRECTORY/img2.png",
    "YOUR_DIRECTORY/img3.png"
};
```

*Tipp:* Cseréld le a `YOUR_DIRECTORY`-t a képek abszolút vagy relatív útvonalára. Ha tucatnyi fájlod van, a manuális listát helyettesítheted a `Directory.GetFiles("YOUR_DIRECTORY", "*.png")`-val.

## 3. lépés: Képek kötegelt OCR-ja – Felismerés párhuzamosan

A képek egymás után történő feldolgozása egyszerű, de lassú. A `Parallel.ForEach` használatával **több képet** dolgozhatunk fel egyszerre, kihasználva a többmagos CPU-kat.

```csharp
// Helper method that performs the parallel recognition
static IReadOnlyList<OcrResult> RecognizeImagesInParallel(Engine engine, IEnumerable<string> paths)
{
    var resultsBag = new ConcurrentBag<OcrResult>();

    Parallel.ForEach(paths, path =>
    {
        // Load the image stream (Aspose handles various formats)
        var image = ImageStream.FromFile(path);
        // Perform OCR
        OcrResult result = engine.Recognize(image);
        // Store the result safely for later use
        resultsBag.Add(result);
    });

    return resultsBag.ToArray();
}

// Execute the parallel OCR
var ocrResults = RecognizeImagesInParallel(ocrEngine, imagePaths);
```

*Miért párhuzamos?* Minden OCR hívás CPU‑igényes, de független, így a párhuzamos futtatás jelentősen lerövidítheti a teljes futási időt, különösen egy 4‑magos vagy erősebb gépen.

## 4. lépés: Több kép feldolgozása – Kinyert szöveg megjelenítése

Most, hogy van egy `OcrResult` objektumokból álló gyűjteményünk, végigiterálhatunk rajtuk és kiírhatjuk a felismert szöveget. Itt általában adatbázisba mentenénk vagy fájlba írnánk az eredményt, de a konzolkimenet a példát tömören tartja.

```csharp
int index = 1;
foreach (var result in ocrResults)
{
    Console.WriteLine($"--- Image {index++} ---");
    Console.WriteLine(result.Text);
}
```

**Várható konzolkimenet (példa):**

```
--- Image 1 ---
Hello world! This is the first image.
--- Image 2 ---
Invoice #12345
Total: $250.00
--- Image 3 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
```

Ha egy kép betöltése sikertelen, az Aspose kivételt dob; a `engine.Recognize` hívást try/catch blokkba teheted, hogy naplózd a hibákat anélkül, hogy a teljes köteget leállítaná.

## 5. lépés: Teljes működő példa – Minden rész együtt

Az alábbiakban a teljes program látható, amelyet beilleszthetsz egy új C# konzolprojektbe. Tartalmazza a `using` utasításoktól a végső kimeneti ciklusig mindent.

```csharp
using System;
using System.Collections.Generic;
using System.Collections.Concurrent;
using System.Threading.Tasks;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // Step 1: Initialize the OCR engine
        var ocrEngine = new Engine();

        // Step 2: Define the PNG files to process
        var imagePaths = new List<string>
        {
            "YOUR_DIRECTORY/img1.png",
            "YOUR_DIRECTORY/img2.png",
            "YOUR_DIRECTORY/img3.png"
        };

        // Step 3: Run OCR in parallel
        var ocrResults = RecognizeImagesInParallel(ocrEngine, imagePaths);

        // Step 4: Output the recognized text
        int index = 1;
        foreach (var result in ocrResults)
        {
            Console.WriteLine($"--- Image {index++} ---");
            Console.WriteLine(result.Text);
        }
    }

    // Helper method for parallel OCR
    static IReadOnlyList<OcrResult> RecognizeImagesInParallel(Engine engine, IEnumerable<string> paths)
    {
        var resultsBag = new ConcurrentBag<OcrResult>();

        Parallel.ForEach(paths, path =>
        {
            try
            {
                var image = ImageStream.FromFile(path);
                OcrResult result = engine.Recognize(image);
                resultsBag.Add(result);
            }
            catch (Exception ex)
            {
                // Log the error but keep the batch running
                Console.Error.WriteLine($"Error processing {path}: {ex.Message}");
            }
        });

        return resultsBag.ToArray();
    }
}
```

### A példa futtatása

1. Hozz létre egy új **Console App** projektet a Visual Studio-ban.  
2. Add the **Aspose.OCR** NuGet csomagot (`Install-Package Aspose.OCR`).  
3. Cseréld le a `YOUR_DIRECTORY`-t arra az útvonalra, amely a PNG fájljaidat tartalmazza.  
4. Build és futtasd – a kinyert szöveget a konzolon kell látnod.

## Pro tippek és szélhelyzetek

- **GPU gyorsítás:** Ha kompatibilis GPU-d és licencelt Aspose OCR-od van, engedélyezd a `EngineSettings`‑en keresztül a motor létrehozása előtt. Ez minden képnél néhány másodpercet takaríthat meg.  
- **Nagy fájlok:** 10 MB-nál nagyobb képek esetén fontold meg a méretcsökkentést, hogy csökkentsd a memóriaigényt.  
- **Nyelvtámogatás:** Alapértelmezés szerint a motor angolt feltételez. Állítsd be `engine.Language = Language.French;` (vagy bármely támogatott nyelvet) a nem angol szövegek pontosságának javításához.  
- **Hibakezelés:** A párhuzamos cikluson belüli `try/catch` biztosítja, hogy egy sérült fájl ne állítsa le a teljes köteget. A hibákat fájlba is naplózhatod későbbi áttekintés céljából.  
- **Eredmény tárolása:** A kiírás helyett a `result.Text`-et egy `.txt` fájlba is írhatod a `File.WriteAllText(Path.ChangeExtension(path, ".txt"))` segítségével.

## Következtetés

Most már tudod, **hogyan használjuk az OCR-t** C#-ban **PNG fájlok szövegének kinyerésére**, **képek kötegelt OCR‑jára**, és **több kép** hatékony feldolgozására az Aspose OCR C# segítségével. A megoldás teljesen önálló, párhuzamosan fut, és minimális módosítással bővíthető több száz vagy ezer fájl kezelésére.

Készen állsz a következő lépésre? Próbáld meg a konzolkimenetet CSV jelentésre cserélni, kísérletezz a GPU gyorsítással, vagy tápláld az OCR szöveget egy keresőindexbe. A lehetőségek végtelenek, és az alapminta – egyszeri inicializálás, párhuzamos futtatás, hibák elegáns kezelése – jól fog szolgálni minden képfeldolgozó csővezetékben.

Boldog kódolást, és legyenek az OCR feladataid gyorsak és hibamentesek!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}