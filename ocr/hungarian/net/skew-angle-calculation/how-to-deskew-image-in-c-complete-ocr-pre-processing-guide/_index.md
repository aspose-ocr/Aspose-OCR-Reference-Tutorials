---
category: general
date: 2026-01-10
description: Hogyan korrigáljuk a kép dőlését és javítsuk az OCR eredményeket az Aspose.OCR-rel.
  Tanulja meg, hogyan előfeldolgozza a képet OCR-hez, hogyan távolítsa el a zajt a
  szkennelésből, és hogyan ismerje fel a szkennelésből származó szöveget.
draft: false
keywords:
- how to deskew image
- preprocess image for ocr
- recognize text from scan
- how to use ocr
- remove noise from scan
language: hu
og_description: Hogyan korrigáljuk a kép dőlését és növeljük az OCR pontosságát. Ez
  az útmutató bemutatja, hogyan előfeldolgozzuk a képet OCR-hez, hogyan távolítsuk
  el a zajt a szkennelésből, és hogyan ismerjük fel a szkennelésből származó szöveget
  az Aspose.OCR használatával.
og_title: Hogyan kiegyenesítsük a képet C#‑ban – Teljes OCR előfeldolgozási útmutató
tags:
- OCR
- C#
- Image Processing
title: Hogyan korrigáljuk a kép dőlését C#‑ban – Teljes OCR előfeldolgozási útmutató
url: /hu/net/skew-angle-calculation/how-to-deskew-image-in-c-complete-ocr-pre-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan korrigáljuk a kép ferdeségét C#‑ban – Teljes OCR előfeldolgozási útmutató

Gondoltad már, **hogyan korrigáljuk a kép ferdeségét** a fájloknál, mielőtt OCR motorba táplálnád őket? Nem vagy egyedül. A beolvasott dokumentumok gyakran ferde, zajos vagy alacsony kontrasztúak, ami megzavar minden szövegfelismerési kísérletet.

Ebben az útmutatóban végigvezetünk egy teljes, futtatható példán, amely **preprocesses image for OCR**, eltávolítja a zajt a beolvasásból, és végül **recognize text from scan** az Aspose.OCR könyvtár segítségével. A végére világos képet kapsz arról, **how to use OCR** C#‑ban, miközben a kód rövid és egyszerű marad.

> **Pro tipp:** Még egy kis elforgatás (5‑10°) is 30 % vagy annál nagyobb pontosságcsökkenést okozhat az OCR‑nél. A ferde kép korrigálása az első lépés, amit soha nem szabad kihagyni.

## Amire szükséged lesz

- **.NET 6+** (a kód .NET Framework‑ön is működik, de a .NET 6 a jelenlegi LTS)
- **Aspose.OCR for .NET** – letöltheted a NuGet‑ből (`Install-Package Aspose.OCR`)
- Egy minta TIFF/PNG/JPEG, amely el van forgatva vagy zajos (a példában a `noisy_rotated.tif`‑t használjuk)
- Bármely kedvenc IDE – a Visual Studio, Rider vagy a VS Code megfelel

Ennyi. Nincs szükség extra könyvtárakra, külső szolgáltatásokra.

## 1. lépés – A forráskép betöltése (Miért fontos)

Mielőtt **deskew image**-t tudnánk végrehajtani, be kell olvasnunk egy Aspose `ImageStream`‑be. Ez az objektum elrejti a fájl I/O részleteit, és egységes felületet biztosít az OCR motor számára.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

// Load the original scan – replace the path with your own file
var sourceImage = ImageStream.FromFile("YOUR_DIRECTORY/noisy_rotated.tif");

// Quick sanity check – make sure the image loaded
if (sourceImage == null)
{
    Console.WriteLine("Failed to load the image. Check the path and file permissions.");
    return;
}
```

*Miért először betöltés?* Mert az összes későbbi szűrő egy memóriában lévő képen dolgozik. Ha a fájlt nem lehet beolvasni, az egész folyamat összeomlik.

## 2. lépés – Előfeldolgozó csővezeték felépítése (Deskew + Denoise + Contrast)

Egy robusztus OCR munkafolyamat általában több szűrőt láncol össze. Itt történik a **preprocesses image for OCR**, és ami még fontosabb, a **how to deskew image** automatikus végrehajtása.

```csharp
// Create a pipeline that will run three filters in order
var preprocessPipeline = new PreprocessPipeline()
{
    // 1️⃣ DeskewFilter – detects rotation up to 30° and corrects it
    new DeskewFilter { MaxAngle = 30 },

    // 2️⃣ DenoiseFilter – smooths out speckles while keeping edges
    new DenoiseFilter { Strength = 0.8 },

    // 3️⃣ ContrastBoostFilter – makes faint characters pop
    new ContrastBoostFilter { Level = 1.3 }
};
```

**Miért ezek a három?**  
- **DeskewFilter** automatikusan megoldja a “how to deskew image” problémát; nem kell kitalálni a szöget.  
- **DenoiseFilter** kezeli a “remove noise from scan” igényt, amely egyébként fantom karaktereket hoz létre.  
- **ContrastBoostFilter** segít az OCR motorának megkülönböztetni a sötét szöveget a világos háttértől, ami klasszikus probléma, amikor *preprocess image for OCR*.

## 3. lépés – A csővezeték alkalmazása (A transzformáció megtekintése)

Most ténylegesen futtatjuk a szűrőket. A visszakapott `processedImage` lesz, amit az OCR motorba táplálunk.

```csharp
// Apply all filters – the result is a cleaned‑up bitmap
var processedImage = preprocessPipeline.Apply(sourceImage);

// Optional: Save the cleaned image for visual verification
processedImage.Save("cleaned_output.tif");
Console.WriteLine("Image preprocessing complete – cleaned_output.tif saved.");
```

Ha megnyitod a `cleaned_output.tif` fájlt, észre fogod venni, hogy a szöveg egyenes, kevésbé szemcsés, és nagyobb kontrasztú. Ez a vizuális ellenőrzés hasznos, amikor *remove noise from scan* és szeretnéd megerősíteni, hogy a deskew működött.

## 4. lépés – OCR motor létrehozása és konfigurálása (How to Use OCR)

Rendezett képpel a kezünkben, példányosítjuk a `OcrEngine`‑t. Ez a **how to use OCR** központja az Aspose‑nél.

```csharp
// Initialize the OCR engine
var ocrEngine = new OcrEngine
{
    // Assign the pre‑processed image
    Image = processedImage,

    // Optional: Set language (English is default)
    // Language = Language.English,
    
    // Enable automatic page segmentation (helps with multi‑column scans)
    AutoPageSegmentation = true
};
```

*Miért állítjuk be a `AutoPageSegmentation`‑t?* Mivel sok beolvasás táblázatot vagy több oszlopot tartalmaz. Bekapcsolva a motor intelligensen felosztja az oldalt, javítva a végső **recognize text from scan** eredményt.

## 5. lépés – A felismerési folyamat futtatása (Végül szöveg felismerése)

Most jön a döntő pillanat: megkérjük a motort, hogy olvassa el a szöveget.

```csharp
// Kick off the OCR process
ocrEngine.Recognize();

// Retrieve the plain‑text result
string recognizedText = ocrEngine.Text;

// Show the output in the console
Console.WriteLine("=== Recognized Text ===");
Console.WriteLine(recognizedText);
```

Ha minden zökkenőmentesen ment, egy tiszta szövegrészt látsz, amely megegyezik az eredeti dokumentummal. Ez a megfelelő **deskewing image**, **removing noise**, és **preprocesses image for OCR** eredménye.

## 6. lépés – Teljes működő példa (Másolás‑Beillesztés kész)

Az alábbiakban a teljes program, készen áll a fordításra. Csak cseréld ki a fájl útvonalát, és már indulhat is.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Load the source image
        // -------------------------------------------------
        var sourceImage = ImageStream.FromFile("YOUR_DIRECTORY/noisy_rotated.tif");
        if (sourceImage == null)
        {
            Console.WriteLine("Unable to load image. Check the path.");
            return;
        }

        // -------------------------------------------------
        // 2️⃣ Build the preprocessing pipeline
        // -------------------------------------------------
        var preprocessPipeline = new PreprocessPipeline()
        {
            new DeskewFilter { MaxAngle = 30 },          // how to deskew image
            new DenoiseFilter { Strength = 0.8 },       // remove noise from scan
            new ContrastBoostFilter { Level = 1.3 }      // improves OCR accuracy
        };

        // -------------------------------------------------
        // 3️⃣ Apply the pipeline
        // -------------------------------------------------
        var processedImage = preprocessPipeline.Apply(sourceImage);
        processedImage.Save("cleaned_output.tif");
        Console.WriteLine("Preprocessing finished – cleaned_output.tif saved.");

        // -------------------------------------------------
        // 4️⃣ Configure the OCR engine
        // -------------------------------------------------
        var ocrEngine = new OcrEngine
        {
            Image = processedImage,
            AutoPageSegmentation = true   // how to use OCR effectively
        };

        // -------------------------------------------------
        // 5️⃣ Recognize text from scan
        // -------------------------------------------------
        ocrEngine.Recognize();
        string result = ocrEngine.Text;

        Console.WriteLine("\n=== Recognized Text ===");
        Console.WriteLine(result);
    }
}
```

**Várható kimenet** (rövidítve a tömörség kedvéért):

```
=== Recognized Text ===
This is a sample scanned document.
It contains several lines of text,
and the OCR engine has correctly read them.
```

Ha a kimenet összezavarodottnak tűnik, ellenőrizd, hogy a forráskép nem fordult-e el 30°-nál többre, vagy növeld a `DeskewFilter.MaxAngle` értékét.

## Gyakran Ismételt Kérdések (Szélsőséges esetek és variációk)

| Kérdés | Válasz |
|----------|--------|
| **Mi van, ha a beolvasásom 45°-ra van elforgatva?** | `DeskewFilter` a `MaxAngle`‑nál korlátozódik. Emeld (pl. `MaxAngle = 60`) vagy előre forgasd el a képet egy grafikus könyvtárral, mielőtt a csővezetéknek adnád. |
| **Feldolgozhatom a PDF‑eket oldalanként?** | Igen. Konvertáld minden PDF oldalt képpé (pl. `Aspose.Pdf` használatával), és futtasd ugyanazt a csővezetéket minden bitmapen. |
| **A dokumentumom franciául van – kell valamit módosítanom?** | Állítsd be `ocrEngine.Language = Language.French;` vagy tölts be egy egyedi nyelvi csomagot. A csővezeték többi része változatlan marad. |
| **Van mód a eredeti felbontás megtartására?** | `PreprocessPipeline` az eredeti bitmapen dolgozik, megőrizve a DPI‑t. Kerüld el az `ImageStream.Resize` hívását, hacsak nem kell teljesítmény miatt lecsökkenteni a méretet. |
| **Hogyan befolyásolja a kontraszt növelése a színes beolvasásokat?** | `ContrastBoostFilter` minden csatornán működik; biztonságos szürkeárnyalatos vagy színes képeknél is, de előbb átalakíthatod szürkeárnyalatúvá a `new GrayscaleFilter()` használatával. |

## Kép példa (Vizuális segédlet)

![hogyan korrigáljuk a kép ferdeségét példa](/images/deskew-example.png)

*A kép egy 12°-ra elforgatott, zajos beolvasás előtte/utána állapotát mutatja, amelyet korrigáltak és megtisztítottak.*

## Következtetés

Áttekintettük, **how to deskew image** az Aspose.OCR segítségével, bemutattuk a teljes **preprocess image for OCR** csővezetéket, megmutattuk, hogyan **remove noise from scan**, és végül **recognize text from scan** néhány C# sorral. A `DeskewFilter`, `DenoiseFilter` és `ContrastBoostFilter` láncolásával egy rendezett bitmapet kapsz, amely lehetővé teszi az OCR motor számára, hogy a feladatát anélkül végezze, hogy a hibák megakadályoznák.

Következő lépések? Kísérletezz különböző szűrő erősségekkel, adj hozzá egy `BinarizationFilter`‑t a tiszta fekete‑fehér kimenethez, vagy tápláld a megtisztított képet egy későbbi NLP csővezetékbe. Ugyanez a minta működik nyugták, útlevelek és történelmi dokumentumok esetén is.

További kérdéseid vannak a **how to use OCR** más nyelveken vagy keretrendszerekben? Írj egy megjegyzést, és jó kódolást!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}