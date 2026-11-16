---
category: general
date: 2026-03-07
description: Tudja meg, hogyan lehet kiegyenesíteni a képet, növelni a kontrasztot,
  és szöveget kinyerni a beolvasott anyagból az Aspose OCR segítségével. Végezzen
  OCR-t a képen egy teljes C# példával, és könnyedén töltse be a képet az OCR-hez.
draft: false
keywords:
- how to deskew image
- extract text from scan
- how to boost contrast
- perform ocr on image
- load image for OCR
language: hu
og_description: Ismerje meg, hogyan lehet kiegyenesíteni a képet, növelni a kontrasztot,
  és szöveget kinyerni a beolvasott anyagból az Aspose OCR C#-ban. Végezzen OCR-t
  a képen lépésről‑lépésre bemutatott kóddal.
og_title: Hogyan kiegyenesítsük a képet és futtassuk az OCR-t C#-ban – Teljes útmutató
tags:
- C#
- OCR
- Image Processing
title: Hogyan korrigáljuk a kép ferdeségét és futtassuk az OCR-t C#‑ban – Teljes útmutató
url: /hu/net/ocr-optimization/how-to-deskew-image-and-run-ocr-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan korrigáljuk a kép ferdeségét és futtassuk az OCR-t C#‑ban – Teljes útmutató

Ha valaha is elgondolkodtál azon, **hogyan korrigáljuk a képet** az OCR futtatása előtt, jó helyen vagy. Ebben az útmutatóban végigvezetünk a kontraszt növelésén, a kép betöltésén OCR‑hez, és végül a **szkennelésből szöveg kinyerése** az Aspose OCR‑rel.  

Akár régi nyugtákat digitalizálsz, beolvasott szerződéseket tisztítasz meg, vagy egyszerűen csak egy megbízható módra van szükséged a ferde fényképről a szöveg olvasásához, az alábbi lépések mindent lefednek, amire szükséged van. Felesleges szócska nélkül – csak egy működő példát, amelyet be tudsz másolni a Visual Studio‑ba.  

## Mit fogsz elérni

* Javítsd ki a ferdeséget legfeljebb 30°-ra (ez a **hogyan korrigáljuk a képet** rész).  
* Növeld a kép kontrasztját a karakterek élesebb kontúrjaiért (**hogyan növeljük a kontrasztot**).  
* Töltsd be a képedet az OCR motorba (**kép betöltése OCR‑hez**).  
* Futtasd a felismerési folyamatot, és **szkennelésből szöveg kinyerése**.  

Mindez a legújabb Aspose.OCR .NET NuGet csomaggal működik (v23.11 a írás időpontjában).  

---

![Példa a kép ferdeségének korrigálására](/images/deskew-example.png "hogyan korrigáljuk a képet")

*A fenti kép egy beolvasott dokumentumot mutat a korrigálás előtti és utáni állapotban.*

## Előkövetelmények

* .NET 6.0 vagy újabb (a kód .NET Framework 4.7+‑on is fut).  
* Visual Studio 2022 (vagy bármely kedvenc C# IDE).  
* Aspose.OCR NuGet csomag – telepítés: `dotnet add package Aspose.OCR`.  

Ennyi. Nincs külső szolgáltatás, nincs API kulcs.

---

## Hogyan korrigáljuk a kép ferdeségét az Aspose OCR-rel

Az első lépés, hogy létrehozzunk egy **ImageProcessingPipeline**‑t, és hozzáadjuk a `DeskewFilter`‑t. A szűrő automatikusan felismeri a domináns szövegsor szögét, és a képet visszaforgatja vízszintes állapotba.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

// Create the OCR engine
var ocrEngine = new OcrEngine();

// Build a pipeline – Deskew is the first filter
var processingPipeline = new ImageProcessingPipeline()
    .Add(new DeskewFilter { MaxAngle = 30 })   // how to deskew image up to 30°
    .Add(new DenoiseFilter { Level = DenoiseLevel.High }) // remove noise
    .Add(new ContrastBoostFilter { Strength = 1.5 })      // how to boost contrast
    .Add(new BinarizationFilter { Method = BinarizationMethod.Sauvola }); // binarize

// Attach the pipeline to the engine
ocrEngine.Settings.ImageProcessing = processingPipeline;
```

**Miért fontos ez:**  
A ferde beolvasás összezavarja az OCR motort, mivel a karakterek már nem illeszkednek az alapvonalhoz. A `DeskewFilter` elemzi a kép hisztogramját, meghatározza a szöget, és elforgatja azt, ezzel drámaian javítva a felismerési pontosságot.

> **Pro tipp:** Ha tudod, hogy a dokumentumaid soha nem haladják meg a 15°‑os ferdeséget, állítsd be a `MaxAngle = 15`‑öt a feldolgozás felgyorsításához.

---

## Hogyan növeljük a kontrasztot a jobb felismerésért

A ferdeség korrigálása után a következő lépés, hogy a szöveget kiemeljük. A `ContrastBoostFilter` kiterjeszti a pixel intenzitás tartományt, ami különösen hasznos a kifakult nyomatoknál.

```csharp
// The ContrastBoostFilter is already in the pipeline above.
// You can tweak the Strength value (1.0 = no change, >1.0 = stronger boost)
.Add(new ContrastBoostFilter { Strength = 1.5 })
```

**Miért segít:**  
Az alacsony kontrasztú beolvasások szürkees karaktereket eredményeznek, amelyeket a binarizáló háttérnek vehet. A kontraszt növelése sötétebbé teszi a sötét pixeleket, világosabbá a világos pixeleket, így a következő `BinarizationFilter` tisztább vászonra kap.

---

## OCR végrehajtása képen – A fájl betöltése

Miután a kép előfeldolgozáson átesett, szükség van a **kép betöltésére OCR‑hez**. Az Aspose egy kényelmes `ImageStream.FromFile` segédfüggvényt kínál.

```csharp
// Load the source image – replace the path with your own file
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/skewed_noisy.jpg");
```

Ha a képed egy stream‑ben van (pl. egy web API‑val feltöltve), használhatod a `ImageStream.FromStream(yourStream)`‑t helyette. A motor támogatja a BMP, JPEG, PNG, TIFF és számos egyéb formátumot.

---

## A felismerési folyamat futtatása és a szkennelésből szöveg kinyerése

Miután minden összekapcsolódott, a `Recognize()` meghívása elvégzi a nehéz munkát. A hívás után a felismert szöveg a `ocrEngine.Text`‑en keresztül érhető el.

```csharp
// Run OCR
ocrEngine.Recognize();

// Output the result
Console.WriteLine("=== Extracted Text ===");
Console.WriteLine(ocrEngine.Text);
```

**Várható kimenet** (példa egy egyszerű számlára):

```
=== Extracted Text ===
Invoice #12345
Date: 03/05/2026
Total: $1,250.00
Thank you for your business!
```

Ha a kimenet összezavartnak tűnik, ellenőrizd a pipeline sorrendjét – először a ferdeség korrigálása, majd a zajcsökkentés, a kontraszt növelése, végül a binarizálás. A sorrend megcserélése ronthatja az eredményeket.

---

## Gyakori buktatók és szélsőséges esetek

| Probléma | Miért fordul elő | Javítás |
|----------|------------------|--------|
| **Üres eredmény** | A kép túl sötét vagy túl világos az alapértelmezett binarizálási módszerhez. | Növeld a `ContrastBoostFilter.Strength` értékét, vagy válts a `BinarizationMethod.Otsu`‑ra. |
| **Részleges szöveg hiányzik** | A zaj a zajcsökkentés után is megmarad. | Használd a `DenoiseLevel.Medium`‑et enyhébb képekhez, vagy adj hozzá egy második `DenoiseFilter`‑t. |
| **Helytelen forgatási irány** | A dokumentumnak vegyes tájolása van (pl. egy elfordított oldal fényképe). | Manuálisan állítsd alacsonyabbra a `DeskewFilter.MaxAngle`‑t, és előre forgasd a képet az `ImageProcessor.Rotate`‑vel. |
| **Teljesítménycsökkenés** | Nagy mennyiségű nagy felbontású kép. | Kicsinyítsd le a képeket (`ImageProcessor.Resize`) a pipeline előtt, vagy dolgozz párhuzamosan (`Parallel.ForEach`). |

---

## Teljes működő példa (másolás-beillesztés kész)

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // 1️⃣ Create OCR engine
        var ocrEngine = new OcrEngine();

        // 2️⃣ Build image‑processing pipeline
        var processingPipeline = new ImageProcessingPipeline()
            .Add(new DeskewFilter { MaxAngle = 30 })                     // how to deskew image up to 30°
            .Add(new DenoiseFilter { Level = DenoiseLevel.High })       // remove high‑level noise
            .Add(new ContrastBoostFilter { Strength = 1.5 })            // how to boost contrast
            .Add(new BinarizationFilter { Method = BinarizationMethod.Sauvola }); // binarize image

        // 3️⃣ Attach pipeline to OCR settings
        ocrEngine.Settings.ImageProcessing = processingPipeline;

        // 4️⃣ Load the image you want to OCR
        // Replace the path with the location of your own file
        ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/skewed_noisy.jpg");

        // 5️⃣ Run the recognition engine
        ocrEngine.Recognize();

        // 6️⃣ Display the extracted text
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrEngine.Text);
    }
}
```

Mentsd el `Program.cs`‑ként, futtasd a `dotnet run` parancsot, és figyeld, ahogy a konzol kiírja a **szkennelésből szöveg kinyerése** eredményt.  

---

## Következő lépések és kapcsolódó témák

* **Batch processing** – Csomagold a fenti logikát egy ciklusba, hogy tucatnyi fájlt kezelj.  
* **Custom language packs** – Ha nem latin írásrendszereket kell olvasnod, tölts be egy nyelvi modellt a `ocrEngine.Settings.Language = OcrLanguage.ChineseSimplified;` segítségével.  
* **PDF output** – Kombináld az Aspose.PDF‑et az OCR‑rel, hogy kereshető szöveget ágyazz be közvetlenül egy PDF fájlba.  
* **Performance tuning** – Kísérletezz az `ImageProcessingPipeline` sorrendjével; néha a zajcsökkentés a ferdeség korrigálása előtt gyorsabb eredményeket ad zajos fényképeken.  

Mindegyik ezek a fő koncepciókra épül, amelyeket bemutattunk: **hogyan korrigáljuk a képet**, **hogyan növeljük a kontrasztot**, **kép betöltése OCR‑hez**, **OCR végrehajtása képen**, és végül **szkennelésből szöveg kinyerése**.

---

## Összegzés

Most bemutattuk a teljes, termelésre kész módszert a **hogyan korrigáljuk a képet** és az OCR futtatására C#‑ban. Egy ferdeség‑korrigáló szűrő, egy zajcsökkentő lépés, egy kontraszt‑növelő és egy binarizáló láncolásával tiszta bemenetet kapsz, amely lehetővé teszi, hogy az Aspose OCR megbízhatóan **szkennelésből szöveg kinyerése**.  

Próbáld ki a kódot, finomítsd a szűrő paramétereit a saját dokumentumaidhoz, és meglátod, milyen gyorsan javul a felismerési pontosság. Van kérdésed? Írj egy megjegyzést, és jó kódolást!  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}