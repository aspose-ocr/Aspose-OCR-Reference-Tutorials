---
category: general
date: 2026-01-02
description: Futtass OCR-t PNG-n gyorsan az Aspose OCR és GPU támogatás segítségével.
  Tanuld meg, hogyan ismerj fel szöveget a képről, hogyan extraháld a szöveget a képből,
  és hogyan állítsd be a GPU memória korlátot.
draft: false
keywords:
- run OCR on PNG
- recognize text from image
- extract text from image
- how to extract text
- set GPU memory limit
language: hu
og_description: Futtass OCR-t PNG-n hatékonyan az Aspose OCR és a GPU gyorsítás kihasználásával.
  Ez az útmutató megmutatja, hogyan ismerhet fel szöveget a képről, hogyan vonhat
  ki szöveget a képből, és hogyan szabályozhatja a GPU memóriahasználatot.
og_title: OCR futtatása PNG-en GPU-val – Teljes C# útmutató
tags:
- OCR
- C#
- GPU
title: OCR futtatása PNG-en GPU-val – Teljes C# útmutató
url: /hu/net/ocr-optimization/run-ocr-on-png-with-gpu-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR futtatása PNG-n GPU-val – Teljes C# útmutató

Valaha is szükséged volt **OCR futtatására PNG** fájlokon, de a teljesítmény határnál elakadtál? Nem vagy egyedül. Sok valós világú folyamatban egyetlen nagy felbontású PNG lelassíthatja a csak CPU‑t használó OCR motorokat, így egy gyors keresés egy perces várakozássá válik.  

A jó hír, hogy az Aspose OCR GPU kiterjesztésekkel érkezik, amelyekkel **szöveget ismerhetsz fel képfájlokból** töredékes idő alatt. Ebben az útmutatóban egy gyakorlati példán keresztül mutatjuk be, hogyan **futtathatsz OCR-t PNG-n** C#‑ban, hogyan **nyerhetsz ki szöveget képből**, és még hogyan **állíthatod be a GPU memória korlátot**, hogy a hardvered keretein belül maradj.

Részletesen kitérünk minden lépés „hogyan” és „miért” aspektusára, így nem csak egy másol‑beillesztéses kódrészletet kapsz, hanem egy szilárd mentális modellt is.

## Mit tanulhatsz meg

- Az Aspose OCR GPU támogatásának előfeltételei.  
- Hogyan tölts be egy PNG‑t `Bitmap`‑ként, és add át az OCR motornak.  
- Hogyan konfiguráld a `GpuDevice`‑et és a `GpuMemoryLimitMb`‑t az optimális teljesítményért.  
- Hogyan **ismerj fel szöveget képből**, és hogyan kapd meg a nyers szöveges eredményt.  
- Tippek a gyakori edge case‑ek kezelésére, például alacsony memória kapacitású GPU‑k vagy többoldalas PNG‑k esetén.  

A végére képes leszel **OCR‑t futtatni PNG‑n** GPU sebességgel, és magabiztosan kezelni az OCR feladatok memóriaigényét.

![Diagram showing run OCR on PNG with GPU acceleration](run-ocr-on-png-diagram.png "run OCR on PNG example")

## Előfeltételek

Mielőtt belevágnánk, győződj meg róla, hogy rendelkezel:

1. .NET 6.0 vagy újabb verzióval (a kód .NET Core‑dal és .NET Framework‑kel is működik).  
2. NVIDIA GPU‑val CUDA támogatással (a példa a 0‑ás eszközindexet használja).  
3. Az Aspose.OCR NuGet csomaggal és annak GPU kiterjesztéseivel (`Aspose.OCR.Extensions`).  
4. Egy minta PNG‑vel (`input.png`), amely a projektedből hivatkozható mappában van.  

Ha bármelyik ismeretlennek tűnik, ne aggódj – a megfelelő alternatívákat megjegyezzük.

---

## 1. lépés – Aspose OCR és GPU kiterjesztések telepítése

Először is. A megfelelő könyvtárak nélkül a kód nem fog lefordulni.

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Extensions
```

A `Aspose.OCR.Extensions` csomag tartalmazza a GPU gyorsításhoz szükséges natív CUDA binárisokat.  
*Pro tipp:* Ha gépednek nincs GPU-ja, a projektet továbbra is lefordíthatod; csak később állítsd be a `PreferGpu = false` értéket.

---

## 2. lépés – Töltsd be a feldolgozni kívánt PNG‑t

Most már **OCR‑t futtathatsz PNG-n** azzal, hogy betöltöd egy `Bitmap`‑be. Ez a lépés egyszerű, de érdemes megjegyezni: a `Bitmap` fájlútvonalat vár, ezért győződj meg róla, hogy az útvonal helyes a futtatható fájlodhoz képest.

```csharp
using System.Drawing;        // Bitmap handling
using Aspose.OCR;
using Aspose.OCR.Extensions; // GPU support extensions

// ...

// Step 2: Load the PNG image
string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "YOUR_DIRECTORY", "input.png");
Bitmap imageBitmap = new Bitmap(imagePath);
```

Ha a PNG szokatlanul nagy (például > 5000 px egy oldalra), érdemes előbb lecsökkenteni a méretét, hogy ne merítsd ki a GPU memóriát. Itt jön jól a **GPU memória korlát beállítása** később.

---

## 3. lépés – Az OCR motor létrehozása és GPU használatra konfigurálása

Itt jön a tutorial szíve: az OCR motor konfigurálása, hogy **szöveget ismerjen fel képből** a GPU segítségével. Két tulajdonság kulcsfontosságú:

- `GpuDevice` – kiválasztja, melyik CUDA eszközt használja.  
- `GpuMemoryLimitMb` – korlátozza, mennyi GPU memóriát foglalhat le a motor.

```csharp
// Step 3: Initialize OCR engine with GPU settings
OcrEngine ocrEngine = new OcrEngine()
{
    // Pick the first CUDA device (index 0)
    GpuDevice = GpuDeviceInfo.GetDevice(0),

    // Optional: limit GPU memory consumption (in MB)
    GpuMemoryLimitMb = 2048   // Adjust based on your GPU's VRAM
};
```

**Miért állíts be memória korlátot?** Néhány GPU megosztja a memóriát a kijelzővel, vagy egyszerre több feladatot futtat. A korlát beállításával elkerülheted a memória‑hiányból adódó összeomlásokat, különösen ha sok PNG‑t dolgozol fel párhuzamosan.

---

## 4. lépés – Felismerési beállítások meghatározása (nyelv & GPU preferencia)

A `RecognitionOptions` objektum megmondja a motornak, milyen nyelvet keressen, és hogy **előnyben részesítse-e a GPU‑t** még kis képek esetén is. A legtöbb angol nyelvű dokumentumhoz ez elegendő, de a `Language.English`‑t kicserélheted más támogatott nyelvre.

```csharp
// Step 4: Set recognition options
RecognitionOptions recognitionOptions = new RecognitionOptions
{
    Language = Language.English,
    PreferGpu = true // Force GPU path even for smaller images
};
```

Ha valaha **szöveget szeretnél kinyerni képből** egy nem angol nyelven, csak módosítsd a `Language` enum‑t. A könyvtár több tucat nyelvet támogat natívan.

---

## 5. lépés – OCR futtatása és az eredmény lekérése

Minden összekötve, a végső hívás egyetlen sor, amely ténylegesen **OCR‑t futtat PNG‑n**, és egy gazdag eredményobjektumot ad vissza.

```csharp
// Step 5: Perform OCR
OcrResult ocrResult = ocrEngine.Recognize(imageBitmap, recognitionOptions);

// Output the extracted text
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);
```

Az `OcrResult` nem csak a nyers szöveget (`ocrResult.Text`) tartalmazza, hanem konfidencia‑pontszámokat, határoló dobozokat, sőt az eredeti képet kiemelt szavakkal – hasznos, ha hibakeresés vagy vizualizáció a cél.

**Várható kimenet** (egy „Hello World” feliratú minta PNG‑hez):

```
=== OCR Output ===
Hello World
```

Ha a szöveg torznak tűnik, ellenőrizd, hogy a PNG nem sérült, és hogy a GPU memória korlát nem túl alacsony a kép méretéhez képest.

---

## 6. lépés – Edge case‑ek kezelése és legjobb gyakorlatok

### Alacsony memória kapacitású GPU‑k

Ha `CudaException: out of memory` hibát látsz, csökkentsd a `GpuMemoryLimitMb` értékét, vagy oszd fel a PNG‑t csempékre a feldolgozás előtt. A csempézés megvalósítható a `Graphics.DrawImage`‑vel egy `Bitmap` klónon.

### Több PNG feldolgozása kötegben

Mappában lévő PNG‑k feldolgozásakor használd ugyanazt az `OcrEngine` példányt – egyszeri inicializálásával GPU kontextus‑váltásokat takaríthatsz meg.

```csharp
foreach (var file in Directory.GetFiles("images", "*.png"))
{
    using var bmp = new Bitmap(file);
    var result = ocrEngine.Recognize(bmp, recognitionOptions);
    Console.WriteLine($"{Path.GetFileName(file)}: {result.Text}");
}
```

### Visszaesés CPU‑ra

Ha nincs GPU, egyszerűen állítsd be a `PreferGpu = false` értéket. A motor automatikusan CPU‑ra vált kódmódosítás nélkül.

```csharp
recognitionOptions.PreferGpu = false; // Safe CPU path
```

---

## Teljes működő példa

Az alábbi program a teljes példát tartalmazza, amelyet beilleszthetsz egy új konzolos projektbe. Tartalmazza az összes fentebb bemutatott lépést, valamint néhány biztonsági ellenőrzést.

```csharp
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Extensions; // GPU support extensions

class GpuExample
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Load the PNG image
        // -------------------------------------------------
        string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory,
                                         "YOUR_DIRECTORY", "input.png");

        if (!File.Exists(imagePath))
        {
            Console.Error.WriteLine($"File not found: {imagePath}");
            return;
        }

        using Bitmap imageBitmap = new Bitmap(imagePath);

        // -------------------------------------------------
        // Step 2: Initialize OCR engine with GPU settings
        // -------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine()
        {
            GpuDevice = GpuDeviceInfo.GetDevice(0), // First CUDA device
            GpuMemoryLimitMb = 2048                  // Adjust as needed
        };

        // -------------------------------------------------
        // Step 3: Set recognition options
        // -------------------------------------------------
        RecognitionOptions recognitionOptions = new RecognitionOptions
        {
            Language = Language.English,
            PreferGpu = true // Force GPU even for small images
        };

        // -------------------------------------------------
        // Step 4: Perform OCR
        // -------------------------------------------------
        OcrResult ocrResult = ocrEngine.Recognize(imageBitmap, recognitionOptions);

        // -------------------------------------------------
        // Step 5: Output the extracted text
        // -------------------------------------------------
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

Mentsd a fájlt `Program.cs`‑ként, futtasd a `dotnet run` parancsot, és a konzolra ki kell nyomtatnia a kinyert szöveget.

---

## Összegzés

Most már megmutattuk, hogyan **futtathatsz OCR‑t PNG‑n** az Aspose OCR GPU kiterjesztéseivel, hogyan **ismerhetsz fel szöveget képből**, és hogyan **nyerhetsz ki szöveget képből**, miközben a **GPU memória korlát beállítását** is irányítod. A `GpuDevice` és a `GpuMemoryLimitMb` megfelelő konfigurálásával alkalmazásod gyors és stabil marad, még szerény GPU‑kon is.

Innen tovább:

- Kísérletezz más nyelvekkel (`Language.French`, `Language.Spanish`).  
- Integráld az OCR lépést egy nagyobb dokumentum‑feldolgozó csővezetékbe.  
- Adj hozzá utófeldolgozást, például helyesírás‑ellenőrzést vagy entitás‑kinyerést a nyers szöveg finomításához.  

Ne feledd, a kulcs nem csak a kódban, hanem abban is rejlik, hogy miért fontos minden beállítás. Ha tudod, mikor kell **GPU memória korlátot beállítani**, és mikor kell visszaesni CPU‑ra, akkor olyan OCR megoldásokat építhetsz, amelyek méretezhetőek és megbízhatóak.

Van kérdésed egy konkrét PNG mérettel, többoldalas TIFF‑ekkel vagy GPU hibák hibaelhárításával kapcsolatban? Írj kommentet alább, és jó kódolást!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}