---
category: general
date: 2026-03-18
description: Táblázat kinyerése képből az Aspose OCR használatával C#-ban. Tanulja
  meg, hogyan konvertálja a táblázatot JSON formátumba, hogyan szerezze meg a táblázat
  JSON-ját, és hogyan nyerjen ki szöveget a képből percek alatt.
draft: false
keywords:
- extract table from image
- convert table to json
- convert image to json
- extract text from image
- get table json
language: hu
og_description: Táblázat kinyerése képből az Aspose OCR használatával C#-ban. Tanulja
  meg, hogyan konvertálja a táblázatot JSON-re, szerezze meg a táblázat JSON-ját,
  és gyorsan nyerjen ki szöveget a képből.
og_title: Táblázat kinyerése képből az Aspose OCR segítségével – Teljes C# útmutató
tags:
- Aspose OCR
- C#
- Table Extraction
title: Táblázat kinyerése képből az Aspose OCR segítségével – Teljes C# útmutató
url: /hu/net/text-recognition/extract-table-from-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Táblázat kinyerése képből – Teljes C# útmutató

Valaha szükséged volt **extract table from image**-re, de nem tudtad, melyik könyvtár tudja ezt megtenni anélkül, hogy hegyeknyi manuális feldolgozást igényelne? Nem vagy egyedül. Sok számlafeldolgozó vagy nyugtáskánáló projektben a valódi fájdalom pont az, hogy egy zajos bitmapet strukturált táblázattá alakítsunk, amelyet a downstream rendszered fel tud használni.

A jó hír? Az Aspose OCR segítségével néhány sorban **convert table to JSON**-t tudsz végrehajtani, és megkapod a teljes kép egyszerű szövegét is, így a **extract text from image** egy bónusz. Ebben az útmutatóban végigvezetünk a teljes folyamaton – a kép betöltésétől a felismert táblázat rendezett JSON ábrázolásáig.

> **Gyors nyeremény:** A végére egy futtatható C# konzolalkalmazást kapsz, amely kiírja a nyers OCR szöveget és egy JSON karakterláncot, amelyet közvetlenül egy adatbázisba vagy API-ba táplálhatsz.

## Előkövetelmények

- .NET 6.0 SDK (vagy bármely friss .NET verzió) telepítve.  
- Érvényes Aspose OCR licenc vagy ingyenes próba (a könyvtár licenc nélkül is működik, de vízjelet ad).  
- Egy olyan kép, amely ténylegesen tartalmaz táblázatot – például `invoice_table.png`.  
- Visual Studio 2022, VS Code vagy bármely kedvelt szerkesztő.

A `Aspose.OCR`-n kívül nincs szükség további NuGet csomagokra.

## 1. lépés: A projekt beállítása és az Aspose OCR telepítése

Először hozz létre egy új konzolprojektet, és húzd be az OCR könyvtárat.

```bash
dotnet new console -n TableJsonDemo
cd TableJsonDemo
dotnet add package Aspose.OCR
```

> **Pro tipp:** Ha vállalati proxy-t használsz, add hozzá a `--no-restore` kapcsolót, és később futtasd a `dotnet restore`-t a megfelelő környezeti változókkal.

## 2. lépés: Az OCR motor inicializálása és a táblázatfelismerés engedélyezése

A megoldás szíve a `OcrEngine`. Az `EnableTableRecognition` beállításával azt mondjuk az Aspose OCR-nek, hogy rácsszerű struktúrákat keressen, ahelyett, hogy mindent egyszerű szövegként kezelne.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Structure;

class TableJsonDemo
{
    static void Main()
    {
        // Create the OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Enable table detection – this is what lets us get a JSON table later
        ocrEngine.Settings.EnableTableRecognition = true;
```

Miért kulcsfontosságú ez a lépés? Táblázatfelismerés nélkül a motor a képet egyetlen karakterláncba lapítja, ami lehetetlenné teszi a sorok és oszlopok későbbi rekonstruálását. Ennek engedélyezése egy könnyűsúlyú elrendezés-elemzési fázist ad hozzá, amely szinte semmilyen teljesítményköltséggel nem jár, de hatalmas downstream előnyöket hoz.

## 3. lépés: A kép betöltése és a felismerés futtatása

Most a motorra irányítjuk azt a fájlt, amely a táblázatot tartalmazza. A `ImageStream.FromFile` a legtöbb gyakori formátumot támogatja (PNG, JPEG, TIFF).

```csharp
        // Load the image that contains the table
        ImageStream image = ImageStream.FromFile("YOUR_DIRECTORY/invoice_table.png");

        // Perform OCR – this returns an OcrResult object with multiple helpers
        OcrResult ocrResult = ocrEngine.Recognize(image);
```

Ha a kép nagy, fontold meg először átméretezni a feldolgozás felgyorsítása érdekében. Az Aspose OCR automatikusan felismeri a DPI-t, de egy 300 DPI-s beolvasás a legtöbb táblázat számára ideális.

## 4. lépés: Az egyszerű szöveg kinyerése – „extract text from image”

Bár a fő célunk a táblázat, gyakran mégis szükség van a nyers szövegre naplózáshoz vagy tartalék feldolgozáshoz.

```csharp
        // Output the full recognized text
        Console.WriteLine("Full text:");
        Console.WriteLine(ocrResult.Text);
```

A `Text` tulajdonság összefűzi mindazt, amit a motor lát, megőrizve a sortöréseket. Ez hasznos, ha ellenőrizned kell, hogy az OCR helyesen olvasta-e a táblázaton kívüli fejléceket vagy lábléceket.

## 5. lépés: A felismert táblázat lekérése JSON-ként – „convert table to json” & „get table json”

Itt történik a varázslat. A `GetTableAsJson()` sorozatba (serializálja) a felismert sorokat, oszlopokat és cellatartalmakat egy tiszta JSON karakterláncba.

```csharp
        // Retrieve the table structure as a JSON string
        string tableJson = ocrResult.GetTableAsJson();

        Console.WriteLine("\nDetected table (JSON):");
        Console.WriteLine(tableJson);
    }
}
```

Az eredményül kapott JSON valahogy így néz ki (olvasásra formázva):

```json
{
  "Rows": [
    {
      "Cells": [
        { "Text": "Item", "ColumnIndex": 0 },
        { "Text": "Quantity", "ColumnIndex": 1 },
        { "Text": "Price", "ColumnIndex": 2 }
      ]
    },
    {
      "Cells": [
        { "Text": "Widget A", "ColumnIndex": 0 },
        { "Text": "10", "ColumnIndex": 1 },
        { "Text": "$5.00", "ColumnIndex": 2 }
      ]
    },
    {
      "Cells": [
        { "Text": "Widget B", "ColumnIndex": 0 },
        { "Text": "7", "ColumnIndex": 1 },
        { "Text": "$8.50", "ColumnIndex": 2 }
      ]
    }
  ]
}
```

Miért előnyös a JSON? Nyelvfüggetlen, könnyen deszerializálható objektumokká, és remekül működik a modern web API-kkal. Ha CSV-re van szükséged, egyszerűen iterálj a sorokon, és a cella szövegeket vesszővel összekapcsolva hozd létre.

## 6. lépés: (Opcionális) A JSON .NET objektummá konvertálása – „convert image to json”

Ha erős típusokkal szeretnél dolgozni, deszerializáld a JSON-t a `System.Text.Json` segítségével.

```csharp
using System.Text.Json;

...

        // Deserialize into a C# class (optional)
        var table = JsonSerializer.Deserialize<TableModel>(tableJson);
        Console.WriteLine("\nFirst cell value: " + table.Rows[0].Cells[0].Text);
```

Definiálnád a `TableModel`, `RowModel` és `CellModel` osztályokat, hogy megfeleljenek a JSON sémának. Ez a lépés megmutatja, hogyan juthatsz el a **convert image to json**-tól egy típusos objektumig, megkönnyítve a downstream validációt.

## Teljes működő példa

Mindent összevonva, itt a teljes, azonnal futtatható program. Mentsd el `Program.cs` néven a korábban létrehozott projekt mappájába.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Structure;
using System.Text.Json;

class TableJsonDemo
{
    static void Main()
    {
        // Step 1: Create OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Enable table recognition
        ocrEngine.Settings.EnableTableRecognition = true;

        // Step 3: Load image containing a table
        ImageStream image = ImageStream.FromFile("YOUR_DIRECTORY/invoice_table.png");

        // Step 4: Run OCR
        OcrResult ocrResult = ocrEngine.Recognize(image);

        // Step 5: Print full text (extract text from image)
        Console.WriteLine("Full text:");
        Console.WriteLine(ocrResult.Text);

        // Step 6: Get table as JSON (convert table to json, get table json)
        string tableJson = ocrResult.GetTableAsJson();
        Console.WriteLine("\nDetected table (JSON):");
        Console.WriteLine(tableJson);

        // Optional: Deserialize JSON to C# objects (convert image to json)
        var table = JsonSerializer.Deserialize<TableModel>(tableJson);
        Console.WriteLine("\nFirst cell value: " + table.Rows[0].Cells[0].Text);
    }
}

// Helper classes matching Aspose's JSON structure
public class TableModel
{
    public RowModel[] Rows { get; set; }
}
public class RowModel
{
    public CellModel[] Cells { get; set; }
}
public class CellModel
{
    public string Text { get; set; }
    public int ColumnIndex { get; set; }
}
```

### Várható kimenet

Amikor a `dotnet run` parancsot futtatod, valami ehhez hasonlót kell látnod:

```
Full text:
Item Quantity Price
Widget A 10 $5.00
Widget B 7 $8.50

Detected table (JSON):
{
  "Rows":[
    {"Cells":[{"Text":"Item","ColumnIndex":0},{"Text":"Quantity","ColumnIndex":1},{"Text":"Price","ColumnIndex":2}]},
    {"Cells":[{"Text":"Widget A","ColumnIndex":0},{"Text":"10","ColumnIndex":1},{"Text":"$5.00","ColumnIndex":2}]},
    {"Cells":[{"Text":"Widget B","ColumnIndex":0},{"Text":"7","ColumnIndex":1},{"Text":"$8.50","ColumnIndex":2}]}
  ]
}

First cell value: Item
```

Ha a kimenet üresnek tűnik, ellenőrizd, hogy az `EnableTableRecognition` `true`-ra van állítva, és a kép ténylegesen tartalmaz tiszta rácsvonalakat.

## Gyakori buktatók és hogyan kerüld el őket

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **Nem jön JSON** | A táblázatfelismerés le van tiltva vagy a kép túl alacsony kontrasztú. | Győződj meg róla, hogy `ocrEngine.Settings.EnableTableRecognition = true`, és javítsd a kép minőségét (növeld a kontrasztot, binarizáld). |
| **Részleges sorok** | Az OCR összezavarodott az egyesített cellák vagy a forgatott szöveg miatt. | Előfeldolgozd a képet: kiegyenesítsd (`ImageProcessor.Rotate`) vagy oszd szét manuálisan az egyesített cellákat. |
| **Unicode szemét** | A betűtípus nem ismerhető (pl. kézírás). | Válts nyelvi csomagra a `ocrEngine.Language = Language.English;` segítségével, vagy használj másik OCR motor kézírásra. |
| **Teljesítménycsökkenés** | Nagyon nagy kép (>5 MP). | Méretezd le körülbelül 1500 px szélességre, miközben megőrzöd a DPI-t. |

## Következő lépések: Túl a alapokon

Most, hogy tudsz **extract table from image**-t és **convert table to JSON**-t, fontold meg ezeket a kiterjesztéseket:

- **A JSON tárolása** adatbázisba az Entity Framework segítségével.  
- **Utófeldolgozás** a JSON-on a pénznemformátumok normalizálásához (pl. `$` eltávolítása).  
- **Kötegelt feldolgozás** egy számlamappán a `Directory.GetFiles` használatával és párhuzamosítás `Parallel.ForEach`-rel.  
- **Integrálás** Azure Functions vagy AWS Lambda segítségével szerver nélküli OCR folyamatokhoz.

Ezek a témák természetesen magukban foglalják a többi másodlagos kulcsszót is, mint például **convert image to json** (amikor az egész OCR eredményt egy felhő végpontra küldöd) és **get table json** a downstream elemzésekhez.

---

### Következtetés

Most mutattuk meg, hogyan **extract table from image**-t használva az Aspose OCR-t, hogyan alakíthatod a táblázatot tiszta JSON-ná, és akár deszerializálhatod C# objektumokká. Ugyanaz a minta

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}