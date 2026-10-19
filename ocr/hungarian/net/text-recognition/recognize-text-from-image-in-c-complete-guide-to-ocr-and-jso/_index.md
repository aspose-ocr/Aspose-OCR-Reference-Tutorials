---
category: general
date: 2026-01-10
description: Tanulja meg, hogyan ismerje fel a szöveget a képről, hogyan nyerje ki
  a szöveg koordinátáit, és hogyan konvertálja a nyugtát JSON formátumba az Aspose
  OCR használatával C#‑ban. Lépésről‑lépésre útmutató.
draft: false
keywords:
- recognize text from image
- how to extract text
- extract text coordinates
- convert receipt to json
language: hu
og_description: Szöveg felismerése képről C#-ban az Aspose OCR használatával. Ez az
  útmutató bemutatja, hogyan lehet szöveget kinyerni, koordinátákat lekérni, és a
  nyugtát JSON formátumba konvertálni.
og_title: szöveg felismerése képről – Teljes C# OCR útmutató
tags:
- OCR
- C#
- Aspose
title: Szöveg felismerése képről C#-ban – Teljes útmutató az OCR-hez és a JSON-hez
url: /hu/net/text-recognition/recognize-text-from-image-in-c-complete-guide-to-ocr-and-jso/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Képről szöveg felismerése – Teljes C# OCR útmutató

Valaha szükséged volt már arra, hogy képről szöveget ismerj fel, de nem tudtad, melyik könyvtárat válaszd? Nem vagy egyedül. Sok valós alkalmazásban – költségkövetők, nyugtabeolvasók vagy dokumentumarchívumok – a szöveg megbízható kinyerése az első akadály.

Ebben az útmutatóban végigvezetünk a **szöveg kinyerésének** folyamatán, lekérjük a határoló dobozokat, és végül **átalakítjuk a nyugtát JSON formátumba** az Aspose.OCR for .NET segítségével. A végére egy önálló C# projekted lesz, amely egy nyugta fényképét veszi, és egy rendezett JSON fájlt ad ki a megbízhatósági pontszámokkal és koordinátákkal.

## Amire szükséged lesz

Mielőtt belevágnánk, győződj meg róla, hogy a következő elemek telepítve vannak a gépeden:

- **.NET 6.0 SDK** (vagy bármely újabb verzió). Régebbi keretrendszerek is működnek, de a .NET 6 a legideálisabb a modern könyvtárakhoz.
- **Visual Studio 2022** vagy VS Code a C# kiegészítővel.
- **Aspose.OCR for .NET** NuGet csomag (`Aspose.OCR` és `Aspose.OCR.Output`). Telepítheted a Package Manager Console‑on keresztül:

```powershell
Install-Package Aspose.OCR
Install-Package Aspose.OCR.Output
```

- Egy minta nyugta kép (például `receipt.jpg`), amelyet egy később hivatkozott mappában helyezel el.

Ennyi—nincs extra SDK, nincs natív bináris, csak tiszta managed kód.

## 1. lépés: Új konzolprojekt létrehozása

Először is, indíts egy konzolalkalmazást. Ez a leggyorsabb módja az OCR tesztelésének UI terhelés nélkül.

```csharp
// Program.cs
using System;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll fill this in later.
        }
    }
}
```

> **Pro tipp:** Tartsd rendezettnek a projekt mappát; hozz létre egy `Resources` almappát, és helyezd bele a `receipt.jpg` fájlt. Így a útvonalkezelés egyszerű lesz.

## 2. lépés: A nyugta kép betöltése

Most már ténylegesen **szöveget ismerünk fel képről**. Az első lépés, hogy az OCR motorra mutassuk a fájlt.

```csharp
// Inside Main()
string imagePath = @"Resources/receipt.jpg";
if (!System.IO.File.Exists(imagePath))
{
    Console.WriteLine($"❌ Image not found at {imagePath}");
    return;
}

// Initialise the OCR engine
OcrEngine ocrEngine = new OcrEngine
{
    Image = ImageStream.FromFile(imagePath)
};

Console.WriteLine("✅ Image loaded successfully.");
```

Miért csomagoljuk a betöltést egy egyszerű létezés‑ellenőrzéssel? Mert éles környezetben gyakran felhasználói feltöltésekkel dolgozol, amelyek hiányozhatnak vagy sérültek lehetnek. A probléma korai elkapása megakadályozza a későbbi rejtélyes kivételeket.

## 3. lépés: OCR végrehajtása – **szöveg felismerése képről**

Miután a kép a memóriában van, megkérjük az Aspose‑t, hogy **szöveget ismerjen fel képről**. Ez a művelet szinkron, és gazdag eredményhalmazt ad vissza.

```csharp
// Still inside Main()
try
{
    ocrEngine.Recognize();
    Console.WriteLine("🧠 OCR completed.");
}
catch (Exception ex)
{
    Console.WriteLine($"❗ OCR failed: {ex.Message}");
    return;
}
```

A háttérben az Aspose egy több millió karakteren tanított neurális hálózatot futtat. A motor feltölti a `ocrEngine.Text`, `ocrEngine.RecognitionResult` és egy `OcrRegion` objektumok gyűjteményét, amelyek koordinátákat tartalmaznak. Pontosan ez kell a következő lépéshez.

## 4. lépés: **Hogyan nyerjünk ki szöveget** – Nyers karakterlánc lekérése

Ha csak a tiszta szöveg érdekel (például gyors kereséshez), közvetlenül a motorból is kinyerheted:

```csharp
string plainText = ocrEngine.Text;
Console.WriteLine("\n--- Extracted Text ---");
Console.WriteLine(plainText);
```

Észre fogod venni a sortöréseket, ahol az OCR bekezdés határokat észlelt. Sok nyugta‑olvasási esetben a nyers karakterlánc elegendő a végösszeg, dátum vagy kereskedő neve egyszerű reguláris kifejezésekkel történő kinyeréséhez.

## 5. lépés: **szöveg koordináták kinyerése** – Határoló dobozok minden szóhoz

Gyakran szükséges tudni, hogy a képen *hol* található egy adott szövegrész – például a teljes összeg kiemeléséhez a felhasználói felületen. Az Aspose ezt `OcrRegion` objektumokkal biztosítja.

```csharp
Console.WriteLine("\n--- Text Coordinates (extract text coordinates) ---");
foreach (var region in ocrEngine.RecognitionResult.Regions)
{
    // Each region represents a word or a line depending on the engine settings.
    string word = region.Text;
    var bounds = region.BoundingBox; // X, Y, Width, Height
    Console.WriteLine($"Word: \"{word}\" | Box: X={bounds.X}, Y={bounds.Y}, W={bounds.Width}, H={bounds.Height}");
}
```

Vedd észre, hogy minden felismert szegmenshez **szöveg koordinátákat nyerünk ki** egy ciklusban. A koordináták az eredeti képhez képest relatívak, így felülhelyezheted őket egy grafikus vásznon vagy egy HTML `<canvas>` elemben.

## 6. lépés: **nyugta átalakítása JSON‑ba** – Részletes eredmények mentése

Most jön az a rész, amely mindent összekapcsol: egy gép‑olvasó struktúrát szeretnénk, amely tartalmazza a szöveget, a megbízhatósági pontszámokat és a határoló dobozokat. Az Aspose a `JsonSaveOptions`‑zal érkezik, ami ezt egyszerűvé teszi.

```csharp
// Define where the JSON will be saved
string jsonPath = @"Resources/receipt.json";

// Configure JSON options to keep confidence and bounding boxes
JsonSaveOptions jsonOptions = new JsonSaveOptions
{
    IncludeConfidence = true,
    IncludeBoundingBoxes = true
};

// Save the OCR result
ocrEngine.Save(jsonPath, jsonOptions);
Console.WriteLine($"\n💾 Detailed OCR results saved to {jsonPath}");
```

Az eredményül kapott fájl valahogy így néz ki (rövidítve a tömörség kedvéért):

```json
{
  "Regions": [
    {
      "Text": "Store",
      "Confidence": 0.99,
      "BoundingBox": { "X": 45, "Y": 120, "Width": 80, "Height": 20 }
    },
    {
      "Text": "Total",
      "Confidence": 0.97,
      "BoundingBox": { "X": 300, "Y": 560, "Width": 70, "Height": 22 }
    }
    // ... more regions ...
  ]
}
```

Most már rendelkezel egy **nyugta átalakítása JSON‑ba** művelettel, amelyet továbbíthatsz downstream szolgáltatások felé – például költségjelentés API‑k, elemzési csővezetékek vagy akár egy egyszerű UI, amely téglalapokat rajzol minden szó köré.

## Teljes működő példa

Az összes elemet összeállítva, itt a teljes `Program.cs`, amelyet beilleszthetsz a projektedbe:

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣ Load the image
            // -------------------------------------------------
            string imagePath = @"Resources/receipt.jpg";
            if (!System.IO.File.Exists(imagePath))
            {
                Console.WriteLine($"❌ Image not found at {imagePath}");
                return;
            }

            OcrEngine ocrEngine = new OcrEngine
            {
                Image = ImageStream.FromFile(imagePath)
            };
            Console.WriteLine("✅ Image loaded.");

            // -------------------------------------------------
            // 2️⃣ Run OCR – recognize text from image
            // -------------------------------------------------
            try
            {
                ocrEngine.Recognize();
                Console.WriteLine("🧠 OCR completed.");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"❗ OCR failed: {ex.Message}");
                return;
            }

            // -------------------------------------------------
            // 3️⃣ Extract plain text (how to extract text)
            // -------------------------------------------------
            Console.WriteLine("\n--- Extracted Text ---");
            Console.WriteLine(ocrEngine.Text);

            // -------------------------------------------------
            // 4️⃣ Get coordinates (extract text coordinates)
            // -------------------------------------------------
            Console.WriteLine("\n--- Text Coordinates ---");
            foreach (var region in ocrEngine.RecognitionResult.Regions)
            {
                var box = region.BoundingBox;
                Console.WriteLine($"Word: \"{region.Text}\" | Box: X={box.X}, Y={box.Y}, W={box.Width}, H={box.Height}");
            }

            // -------------------------------------------------
            // 5️⃣ Save detailed JSON (convert receipt to json)
            // -------------------------------------------------
            string jsonPath = @"Resources/receipt.json";
            JsonSaveOptions jsonOptions = new JsonSaveOptions
            {
                IncludeConfidence = true,
                IncludeBoundingBoxes = true
            };
            ocrEngine.Save(jsonPath, jsonOptions);
            Console.WriteLine($"\n💾 JSON saved at {jsonPath}");
        }
    }
}
```

Futtasd a programot (`dotnet run`) és figyeld a konzol kimenetet. Nyisd meg a `Resources/receipt.json` fájlt a struktúra ellenőrzéséhez.

## Gyakori kérdések és szélhelyzetek

- **Mi van, ha a kép elmosódott?**  
  Az Aspose OCR a legjobban 300 dpi vagy annál magasabb felbontásnál működik. Ha alacsony megbízhatósági pontszámokat kapsz, fontold meg egy élesítő szűrő alkalmazását a kép motorba való betáplálása előtt.

- **Több nyelvet is fel tudok ismerni?**  
  Igen. Állítsd be `ocrEngine.Language = Language.English | Language.Spanish;` a `Recognize()` hívása előtt.

- **Hogyan korlátozhatom a kimenetet csak számokra (pl. összeg)?**  
  Miután megvan a tiszta szöveg, futtass egy reguláris kifejezést, például `\d+\.\d{2}` a `ocrEngine.Text`‑en. Mivel már rendelkezünk koordinátákkal, a megtalált karakterláncot visszafejtheted a megfelelő régióra a vizuális kiemeléshez.

- **A JSON formátum testreszabható?**  
  A `JsonSaveOptions` osztály néhány flag‑et tesz elérhetővé. Ha teljesen egyedi sémára van szükséged, iterálhatsz a `ocrEngine.RecognitionResult.Regions` elemein, és saját magad sorosíthatod az objektumokat a `System.Text.Json`‑nal.

## Összegzés

Most bemutattuk, hogyan **ismerjünk fel szöveget képről** C#‑ban az Aspose.OCR használatával, **hogyan nyerjünk ki szöveget**, **szöveg koordinátákat nyerjünk ki**, és végül **nyugtát alakítsunk át JSON‑ba**. Az egész folyamat egyetlen, könnyen futtatható konzolalkalmazásban él, ami tökéletes prototípusokhoz vagy nagyobb rendszerek építőelemeként.

Következő lépések? Próbáld meg a JSON‑t egy front‑endbe betáplálni, amely kirajzolja a határoló dobozokat, vagy csatlakoztasd a kimenetet egy költségjelentő szolgáltatáshoz. Kísérletezhetsz különböző képformátumokkal (PNG, TIFF) vagy kötegelt feldolgozással egy nyugták mappáját.

További kérdéseid vannak az OCR‑rel, az Aspose‑szal vagy a JSON kezelésével kapcsolatban? Írj egy megjegyzést alább, és jó kódolást! 

![Nyugta kép példa a szöveg felismeréséhez képről](receipt.jpg "Nyugta kép példa")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}