---
category: general
date: 2026-01-15
description: Kép konvertálása JSON-re az Aspose OCR használatával C#-ban. Tanulja
  meg, hogyan lehet szöveget kinyerni a képből, JSON határoló dobozokat kapni, és
  felismerni a nyugtaképet.
draft: false
keywords:
- convert image to json
- extract text from image
- aspose ocr c# example
- recognize receipt image
- json bounding boxes
language: hu
og_description: Kép konvertálása JSON-re az Aspose OCR segítségével C#-ban. Lépésről
  lépésre útmutató a képről szöveg kinyeréséhez, a nyugtakép felismeréséhez és a JSON
  körülhatároló dobozok lekéréséhez.
og_title: Kép átalakítása JSON-re az Aspose OCR C# útmutatóval
tags:
- Aspose OCR
- C#
- JSON
- Image Processing
title: Kép konvertálása JSON formátumba Aspose OCR C# útmutatóval
url: /hu/net/text-recognition/convert-image-to-json-with-aspose-ocr-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kép JSON formátumba konvertálása Aspose OCR C# útmutatóval

Valaha szükséged volt **convert image to JSON**-ra, de nem tudtad, melyik könyvtár adja meg egyszerre a nyers szöveget és a szavak pontos koordinátáit? Nem vagy egyedül. Sok fejlesztő szembesül ezzel a problémával, amikor képfájlokból – különösen nyugtákból – próbál szöveget kinyerni, miközben egy gép‑olvasható JSON terhet is igényelnek a további feldolgozáshoz.

Ebben az útmutatóban végigvezetünk egy teljes **Aspose OCR C# example**-en, amely megmutatja, hogyan lehet szöveget kinyerni a képből, felismerni a nyugta képet, és **JSON bounding boxes**-t kiadni minden egyes szóhoz. A végére egy azonnal futtatható konzolalkalmazásod lesz, amely szépen formázott JSON karakterláncot nyomtat, amelyet bármely API‑ba, adatbázisba vagy elemzési csővezetékbe be lehet táplálni.

> **Mit fogsz elsajátítani**  
> • Egy teljesen működőképes C# projekt, amely **converts image to JSON**  
> • Rálátás arra, miért engedélyezzük a `IncludeBoundingBoxes`-t (ez a kulcs a `json bounding boxes`-hoz)  
> • Tippek különböző képformátumok és nyelvek kezeléséhez  

Kezdjük el.

---

## Amire szükséged lesz

- **.NET 6.0 SDK** (vagy bármely későbbi verzió) – a kód a .NET 6-ra céloz, de a .NET Framework 4.7+ verziókon is működik.  
- **Aspose.OCR for .NET** NuGet csomag – a `dotnet add package Aspose.OCR` paranccsal telepíthető.  
- Egy minta nyugta kép (`receipt.jpg`), amelyet egy olyan mappába helyezel, amelyet a projekted hivatkozni tud.  
- Visual Studio 2022, VS Code vagy bármely kedvelt IDE.

Nem szükséges más külső szolgáltatás; minden helyben fut.

## Kép JSON formátumba konvertálása – Áttekintés

A lényeg egyszerű: betöltünk egy képet, megmondjuk az Aspose OCR-nek, hogy ismerje fel az angolt (vagy bármely támogatott nyelvet), kérjük, hogy tartalmazza a bounding box-okat, és végül kérjük az eredményt **JSON** formátumban. A könyvtár elvégzi a nehéz munkát – OCR, elrendezés-elemzés és JSON sorosítás.

Itt egy magas szintű diagram a folyamatról (képzelj el egy kis ábrát):

```
[Image File] → Aspose OCR Engine → Recognition Options (JSON + Bounding Boxes) → JSON Output
```

Ez a kis diagram rögzíti az egész csővezeték‑láncot, amelyet megvalósítunk.

## 1. lépés: A projekt beállítása és az Aspose OCR telepítése

Először hozz létre egy új konzolprojektet, és húzd be az Aspose OCR csomagot.

```bash
dotnet new console -n JsonOutputDemo
cd JsonOutputDemo
dotnet add package Aspose.OCR
```

> **Pro tipp:** Ha Visual Studio-t használsz, jobb‑kattints a projektre → *Manage NuGet Packages* → keresd meg a **Aspose.OCR**-t, és telepítsd a legújabb stabil verziót (jelenleg 23.12).

## 2. lépés: A felismerni kívánt kép betöltése

A `OcrImage.FromFile` metódust fogjuk használni a nyugta kép beolvasásához. Győződj meg róla, hogy az útvonal egy valódi fájlra mutat; ellenkező esetben `FileNotFoundException`-t kapsz.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Output;

class JsonOutputDemo
{
    static void Main()
    {
        // Step 2: Load the image you want to recognize
        var receiptImage = OcrImage.FromFile("YOUR_DIRECTORY/receipt.jpg");
```

Ha a képed a `.csproj` mellé van, egyszerűen használhatod a `"receipt.jpg"`-t.

## 3. lépés: OCR beállítások konfigurálása JSON Bounding Box-okhoz

A varázslat akkor történik, amikor engedélyezzük a `OutputFormat = OutputFormat.Json` **és** a `IncludeBoundingBoxes = true` beállítást. Az első azt mondja az Aspose-nak, hogy a eredményt JSON-ként sorosítsa, míg a második minden szóhoz hozzáadja az `x`, `y`, `width` és `height` értékeket – pontosan amire a `json bounding boxes`-hoz szükséged van.

```csharp
        // Step 3: Configure OCR options
        var ocrOptions = new OcrOptions
        {
            OutputFormat = OutputFormat.Json,
            IncludeBoundingBoxes = true   // include coordinates for each recognized word
        };
```

A `ocrOptions.Dpi` vagy `ocrOptions.Language` értékeket is módosíthatod, ha nagyobb felbontásra vagy más nyelvre van szükséged.

## 4. lépés: A felismerés végrehajtása – Szöveg kinyerése a képből

Most meghívjuk a `Recognize`. A metódus egy `OcrResult` objektumot ad vissza, amely tartalmazza a JSON karakterláncot, a nyers szöveget és egyebeket.

```csharp
        // Step 4: Perform recognition using English language and the configured options
        var ocrEngine = new OcrEngine();
        var ocrResult = ocrEngine.Recognize(receiptImage, Language.English, ocrOptions);
```

Ha más nyelveket kell kezelni, cseréld le a `Language.English`-t `Language.Spanish`, `Language.French` stb.-re. Az Aspose több mint 30 nyelvet támogat alapból.

## 5. lépés: Az eredmény kiírása – A JSON terhelésed

Végül kiírjuk a JSON-t a konzolra. Egy valódi alkalmazásban valószínűleg fájlba írnád vagy egy szolgáltatásba küldenéd.

```csharp
        // Step 5: Output the resulting JSON string
        System.Console.WriteLine(ocrResult.Json);
    }
}
```

A program futtatása egy alább láthatóhoz hasonló JSON dokumentumot kell, hogy előállítson.

```json
{
  "Text": "Total $12.34\nDate 01/01/2024",
  "Words": [
    {
      "Text": "Total",
      "BoundingBox": { "X": 45, "Y": 112, "Width": 60, "Height": 20 }
    },
    {
      "Text": "$12.34",
      "BoundingBox": { "X": 110, "Y": 112, "Width": 70, "Height": 20 }
    },
    {
      "Text": "Date",
      "BoundingBox": { "X": 45, "Y": 140, "Width": 50, "Height": 20 }
    },
    {
      "Text": "01/01/2024",
      "BoundingBox": { "X": 100, "Y": 140, "Width": 120, "Height": 20 }
    }
  ]
}
```

Vedd észre, hogy minden szó most már tartalmazza a **JSON bounding box**-ot – tökéletes a UI overlay vagy egy downstream parser számára.

## Teljes működő példa

Az alábbiakban a teljes, másolás‑beillesztésre kész program található. Nincs rejtett rész, nincs külső hívás – csak tiszta C#.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Output;

class JsonOutputDemo
{
    static void Main()
    {
        // 1️⃣ Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // 2️⃣ Load the image you want to recognize
        var receiptImage = OcrImage.FromFile("YOUR_DIRECTORY/receipt.jpg");

        // 3️⃣ Configure OCR options to get detailed JSON output with word positions
        var ocrOptions = new OcrOptions
        {
            OutputFormat = OutputFormat.Json,
            IncludeBoundingBoxes = true   // include coordinates for each recognized word
        };

        // 4️⃣ Perform recognition using English language and the configured options
        var ocrResult = ocrEngine.Recognize(receiptImage, Language.English, ocrOptions);

        // 5️⃣ Output the resulting JSON string
        System.Console.WriteLine(ocrResult.Json);
    }
}
```

> **Watch out for:**  
> • **File path errors** – ellenőrizd duplán a kép helyét.  
> • **Missing NuGet package** – győződj meg róla, hogy a `Aspose.OCR` hivatkozásban van.  
> • **Unsupported image formats** – maradj a JPEG, PNG, BMP vagy TIFF formátumoknál a legjobb eredményért.

## Gyakori kérdések és szélhelyzetek

### Átalakíthatok egy **PDF oldalt** JSON formátumba JPEG helyett?

Igen. Először a PDF oldalt képpé kell konvertálni (pl. a `Aspose.PDF` használatával), majd azt a képet a ugyanabba az OCR csővezetékbe táplálni. A JSON kimenet azonos lesz, mivel az OCR lépés csak a raszteres adatokat nézi.

### Mi van, ha a nyugta elmosódott?

Növeld a DPI-t az `ocrOptions`-ban. Például:

```csharp
ocrOptions.Dpi = 300; // higher DPI improves accuracy on low‑quality scans
```

A magasabb DPI növelheti a memóriahasználatot, ezért egyensúlyozz a minőség és a teljesítmény között.

### Több **nyelvre** van szükségem ugyanazon a nyugtán (pl. angol + spanyol).

Átadhatsz egy nyelv tömböt:

```csharp
var ocrResult = ocrEngine.Recognize(receiptImage, new[] { Language.English, Language.Spanish }, ocrOptions);
```

### Hogyan írjam a JSON-t fájlba?

Csak cseréld le a `Console.WriteLine` sort a következőre:

```csharp
System.IO.File.WriteAllText("receipt.json", ocrResult.Json);
```

Most már van egy tartós fájlod, amelyet más szolgáltatásokhoz küldhetsz.

## Vizuális összefoglaló

![convert image to json example](convert-image-to-json.png "convert image to json example")

*The screenshot shows the console output of the JSON payload after running the demo.*  
*A képernyőképen a JSON terhelés konzol kimenete látható a demó futtatása után.*

## Következtetés

Most megmutattuk, hogyan **convert image to JSON** Aspose OCR használatával C#-ban. Az `OutputFormat` és `IncludeBoundingBoxes` beállításával **extract text from image**, **recognize receipt image**, és pontos **JSON bounding boxes**-t kaphatsz minden egyes szóhoz. A teljes, futtatható kód a fenti kódrészletben található, így bármely .NET projektbe beillesztheted most.

Mi a következő? Próbáld meg a JSON-t egy front‑end nézőbe betáplálni, amely kiemeli a szavakat, vagy küldd az adatot egy gépi‑tanulási modellnek, amely a nyugták tételeit osztályozza. Kísérletezhetsz más nyelvekkel, magasabb DPI beállításokkal, vagy több kép kötegelt feldolgozásával egy ciklusban.

Ha bármilyen problémába ütközöl, emlékezz a fájlútvonalakra, DPI-re és a nyelvtömbökre vonatkozó tippekre. Nyugodtan hagyj megjegyzést vagy nyiss egy issue-t a GitHub repóban, amelyet ehhez a demóhoz hozol létre. Boldog kódolást, és élvezd a képek strukturált JSON‑ná alakítását!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}