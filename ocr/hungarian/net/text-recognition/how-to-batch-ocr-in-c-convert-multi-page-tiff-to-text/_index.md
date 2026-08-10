---
category: general
date: 2026-03-28
description: Tanulja meg, hogyan végezhet kötegelt OCR-t C#-ban, és konvertálja egyszerűen
  a TIFF fájlokat szöveggé. Ez a lépésről‑lépésre útmutató bemutatja a szöveg kinyerését
  TIFF fájlokból az Aspose OCR segítségével.
draft: false
keywords:
- how to batch ocr
- convert tiff to text
- extract text from tiff
- c# ocr tutorial
language: hu
og_description: Hogyan végezzünk kötegelt OCR-t C#-ban? Kövesd ezt a teljes útmutatót,
  hogy többoldalas TIFF fájlokat konvertálj kereshető szöveggé az Aspose OCR segítségével.
og_title: Hogyan végezzünk kötegelt OCR-t C#‑ban – Többoldalas TIFF konvertálása szöveggé
tags:
- OCR
- C#
- Aspose
title: Hogyan végezzünk kötegelt OCR-t C#-ban – Többoldalas TIFF konvertálása szöveggé
url: /hu/net/text-recognition/how-to-batch-ocr-in-c-convert-multi-page-tiff-to-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan végezzünk kötegelt OCR‑t C#‑ban – Többoldalas TIFF konvertálása szöveggé

Gondolkodtál már azon, **hogyan végezzünk kötegelt OCR‑t** egy halom beolvasott oldalon anélkül, hogy minden képhez külön ciklust írnál? Nem vagy egyedül. Sok projektben – gondolj csak a számlafeldolgozásra vagy az archiválás digitalizálására – naponta felmerül a **TIFF szöveggé konvertálása** igénye, és ha egyesével dolgozod fel az oldalakat, az gyorsan rémálommá válik.

A jó hír? Néhány C# sorral és az Aspose OCR‑rel betáplálhatsz egy egész többoldalas TIFF‑et a motorba, és egy szótárat kapsz, amely az oldal számát a kinyert szöveggel párosítja. Ebben a tutorialban egy teljes, futtatható példán keresztül mutatjuk be, **hogyan végezzünk kötegelt OCR‑t**, **hogyan nyerjünk ki szöveget TIFF‑ből**, és miért felülmúlja ez a megközelítés a manuális alternatívát.

## Amit megtanulsz

- Az Aspose OCR könyvtár beállítása egy .NET projektben.  
- Többoldalas TIFF fájl betöltése `Image.FromMultiPageFile` segítségével.  
- `RecognizeBatch` futtatása, amely egy `Dictionary<int,string>` típusú oldalankénti eredményt ad vissza.  
- Az eredmény kiírása tiszta, olvasható formátumban.  

A végére egy kész konzolalkalmazásod lesz, amely bármely többoldalas TIFF‑et egyszerű szöveggé alakít – további eszközök nélkül.

### Előfeltételek

- .NET 6.0 SDK (vagy bármely friss .NET verzió).  
- Visual Studio 2022 vagy VS Code – a kedvenc IDE‑d is megfelel.  
- Érvényes Aspose OCR licenc vagy ingyenes értékelő kulcs (az API licenc nélkül is működik, de vízjelet ad).  
- Egy `multipage.tif` nevű minta többoldalas TIFF, amelyet egy hivatkozható mappába helyeztél.

> **Pro tipp:** Windows alatt a projekt alapmappája kényelmes hely a TIFF elhelyezéséhez; Linux/macOS esetén csak a megfelelő útvonalra kell módosítanod.

## 1. lépés: Aspose OCR NuGet csomag telepítése

Mielőtt kódot írnánk, szükségünk van az OCR könyvtárra. Nyiss egy terminált a projekt mappájában, és futtasd:

```bash
dotnet add package Aspose.OCR
```

Ez letölti a legújabb stabil verziót (2026. március állása szerint v23.9), és hozzáadja a szükséges DLL‑eket a projekthez. Egyszerű konzolalkalmazáshoz nincs szükség további konfigurációra.

## 2. lépés: A konzolalkalmazás vázának létrehozása

Készítsünk egy minimális programot, amely hivatkozik az OCR motorra. A `using` direktívák kulcsfontosságúak – nélkülük a fordító hiányzó típusokra panaszkodik.

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;   // Required for Image class
```

> **Miért fontos:** Az `Image` osztály egy alnévtérben található, és ha elfelejted az `ImageProcessing` importot, “type or namespace not found” hibát kapsz, ami akár egy órát is elveszíthetsz a hibakeresésben.

Most add hozzá a `Main` metódust és egy rövid megjegyzést, amely leírja a célját:

```csharp
/// <summary>
/// Demonstrates how to batch OCR a multi‑page TIFF and output each page's text.
/// </summary>
class BatchOcrTutorial
{
    static void Main()
    {
        // Implementation will go here
    }
}
```

## 3. lépés: Az OCR motor inicializálása

Az `OcrEngine` a munkagépe. Egyszeri példányosítása és újrahasználata minden oldalhoz memóriatakarékos és gyors.

```csharp
// Step 3: Create an OCR engine instance
var ocrEngine = new OcrEngine();
```

> **Mi történik a háttérben?** A motor betölti a nyelvi modelleket és előre beállítja az alapértelmezett beállításokat (pl. angol, automatikus forgatás). Később módosíthatod ezeket, de az alapértelmezések a legtöbb dokumentumhoz megfelelőek.

## 4. lépés: Többoldalas TIFF betöltése

Az Aspose egyszerűvé teszi a többkeretes képek betöltését. Add meg a teljes vagy relatív útvonalat a futtatható állomány munkakönyvtárához képest.

```csharp
// Step 4: Load a multi‑page TIFF image
string tiffPath = "YOUR_DIRECTORY/multipage.tif";   // ← replace with your actual path
var multiPageImage = Image.FromMultiPageFile(tiffPath);
```

Ha a fájl nem található, a `FromMultiPageFile` `FileNotFoundException`‑t dob. Ha szeretnél elegáns hibakezelést, tedd `try/catch`‑be – ezt a következő lépésben mutatjuk be.

## 5. lépés: Kötegelt OCR végrehajtása

Most jön a főszereplő: `RecognizeBatch`. Egy `Dictionary<int,string>`‑et ad vissza, ahol a kulcs az oldal indexe (0‑tól kezdve), az érték pedig a felismert szöveg.

```csharp
// Step 5: Perform batch OCR on all pages
Dictionary<int, string> ocrResults = ocrEngine.RecognizeBatch(multiPageImage);
```

> **Széljegyzet:** Egyes TIFF‑ek üres oldalakat tartalmaznak. Az Aspose ezekhez üres stringet ad vissza, amit később szűrhetsz, ha nem szeretnél felesleges kimenetet.

## 6. lépés: Az eredmények megjelenítése

Végül iterálj a szótáron, és írd ki minden oldal szövegét. Az interpolált stringek használata tisztán tartja a kódot.

```csharp
// Step 6: Output the recognized text for each page
foreach (var pageResult in ocrResults)
{
    Console.WriteLine($"--- Page {pageResult.Key + 1} ---"); // +1 for human‑friendly numbering
    Console.WriteLine(pageResult.Value);
    Console.WriteLine(); // Blank line for readability
}
```

A program futtatása valami ilyesmit kell, hogy kiírjon:

```
--- Page 1 ---
Invoice #12345
Date: 2024‑12‑01
Total: $1,250.00
...

--- Page 2 ---
Terms and Conditions
...
```

Ha torz kimenetet látsz, ellenőrizd, hogy a forrás‑TIFF nem sérült, és hogy a szöveg nyelve megegyezik a motor alapértelmezett nyelvével (angol). Nem‑angol dokumentumokhoz például beállíthatod: `ocrEngine.Language = OcrLanguage.Spanish;`.

## Teljes működő példa

Az összes darabot egy helyre rakva, itt a komplett program, amelyet egyszerűen másolj be a `Program.cs`‑be és futtass:

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;   // Needed for Image class

/// <summary>
/// Demonstrates how to batch OCR a multi‑page TIFF and output each page's text.
/// </summary>
class BatchOcrTutorial
{
    static void Main()
    {
        try
        {
            // Step 1: Create an OCR engine instance
            var ocrEngine = new OcrEngine();

            // Step 2: Load a multi‑page TIFF image
            string tiffPath = "YOUR_DIRECTORY/multipage.tif";   // Change to your actual file location
            var multiPageImage = Image.FromMultiPageFile(tiffPath);

            // Step 3: Perform batch OCR on all pages
            Dictionary<int, string> ocrResults = ocrEngine.RecognizeBatch(multiPageImage);

            // Step 4: Output the recognized text for each page
            foreach (var pageResult in ocrResults)
            {
                Console.WriteLine($"--- Page {pageResult.Key + 1} ---");
                Console.WriteLine(pageResult.Value);
                Console.WriteLine(); // Extra line for visual separation
            }
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error during OCR processing: {ex.Message}");
        }
    }
}
```

Mentés, build és futtatás:

```bash
dotnet run
```

Minden oldal kinyert tartalma megjelenik a konzolon. Ez a teljes **c# ocr tutorial**, amelyet kértél.

## Gyakran ismételt kérdések és széljegyzetek

### Mi a teendő, ha a TIFF több tucat oldalt tartalmaz?

A `RecognizeBatch` egy hívással feldolgozza az összes keretet, de a memóriahasználat lineárisan nő az oldalak számával. Nagyon nagy dokumentumok (százak oldal) esetén érdemes darabokra bontani a feldolgozást:

```csharp
for (int i = 0; i < multiPageImage.PageCount; i += 50)
{
    var subImage = multiPageImage.GetPages(i, Math.Min(50, multiPageImage.PageCount - i));
    var partialResults = ocrEngine.RecognizeBatch(subImage);
    // Merge partialResults into the main dictionary...
}
```

### Menthetem a kinyert szöveget fájlokba a konzolra írás helyett?

Természetesen. Cseréld le a `Console.WriteLine` blokkot fájl‑I/O‑ra:

```csharp
string outputFolder = "ExtractedText";
Directory.CreateDirectory(outputFolder);

foreach (var pageResult in ocrResults)
{
    string filePath = Path.Combine(outputFolder, $"Page_{pageResult.Key + 1}.txt");
    File.WriteAllText(filePath, pageResult.Value);
}
```

Ezzel minden oldal saját `.txt` fájlt kap – tökéletes a további indexeléshez.

### Hogyan változtathatom meg a kimeneti nyelvet vagy kapcsolhatom be az automatikus forgatást?

```csharp
ocrEngine.Language = OcrLanguage.French; // or any supported language
ocrEngine.AutoRotate = true;             // Detects rotated text automatically
```

Ezeket a beállításokat **a** `RecognizeBatch` **hívása előtt** kell alkalmazni.

## Összegzés

Áttekintettük, **hogyan végezzünk kötegelt OCR‑t** egy többoldalas TIFF‑en az Aspose OCR segítségével C#‑ban. Az kép egyszeri betöltésével, a `RecognizeBatch` meghívásával és a kapott szótár iterálásával **TIFF‑et szöveggé** alakíthatsz néhány másodperc alatt. A példa bemutatja, hogyan **nyerjünk ki szöveget TIFF‑ből**, hogyan kezeljünk hibákat, és opcionálisan hogyan írjuk az eredményeket fájlokba – mindezt egy tiszta, önálló konzolalkalmazásban.

Készen állsz a következő lépésre? Próbáld meg kombinálni ezt a megközelítést egy PDF‑generáló könyvtárral, hogy kereshető PDF‑eket hozz létre, vagy csatlakoztasd a kimenetet egy adatbázishoz a kereshető archívumokért. Kísérletezhetsz más képformátumokkal (PNG, JPEG) is, ha az `Image.FromMultiPageFile`‑t `Image.FromFile`‑ra cseréled.

További kérdéseid vannak OCR‑rel, licenceléssel vagy teljesítményhangolással kapcsolatban? Írj egy megjegyzést alább, és jó kódolást kívánunk!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}