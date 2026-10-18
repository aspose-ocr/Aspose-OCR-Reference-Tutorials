---
category: general
date: 2026-04-01
description: Tanulja meg, hogyan ismerje fel gyorsan a szöveget PNG fájlokból a GPU
  eszközazonosító beállításával és a GPU gyorsítás engedélyezésével az Aspose OCR-ben.
  Lépésről lépésre C# útmutató.
draft: false
keywords:
- recognize text from png
- set gpu device id
- Aspose OCR GPU
- batch OCR C#
- OCR performance tips
language: hu
og_description: Ismerje fel a szöveget PNG fájlokból gyorsan a GPU eszközazonosító
  beállításával. Kövesse ezt a teljes C# útmutatót a GPU gyorsítás engedélyezéséhez
  az Aspose OCR-rel.
og_title: Szöveg felismerése PNG-ből – GPU-gyorsított Aspose OCR útmutató
tags:
- C#
- OCR
- GPU
- Aspose
title: Szöveg felismerése PNG-ből az Aspose OCR segítségével – GPU-gyorsított kötegelt
  demó
url: /hu/net/ocr-optimization/recognize-text-from-png-with-aspose-ocr-gpu-accelerated-batc/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# szöveg felismerése png‑ből – Teljes C# GPU‑Gyorsított Kötetes Útmutató

Valaha is szükséged volt **szöveg felismerése png‑ből** képeken, de a folyamatot fájdalmasan lassúnak találtad? Nem vagy egyedül. A legtöbb fejlesztő egy egyszerű OCR hívással kezd, majd egy konzolra bámul, amely úgy lassan halad, mint egy csiga, amikor egy mappa tucatnyi képernyőképet tartalmaz.  

A jó hír? Az Aspose OCR át tudja adni a nehéz munkát a grafikus kártyádnak, és néhány sorral **set gpu device id** beállíthatod a kívánt GPU-t. Ebben az útmutatóban végigvezetünk egy teljes, futtatható példán, amely egy mappából összegyűjti az összes PNG‑t, bekapcsolja a GPU gyorsítást, kiválasztja az első GPU‑t, és kiírja az egyes fájlok karakter számlálóját.

A végére egy önálló programod lesz, amelyet bármely .NET projektbe beilleszthetsz, és megérted, miért fontos a GPU engedélyezése, hogyan kell kezelni a szélsőséges eseteket, és mit lehet finomhangolni a még jobb teljesítmény érdekében.

## Amire szükséged lesz

- **.NET 6.0** vagy újabb (a kód .NET Core‑dal is lefordítható).  
- A **Aspose.OCR** NuGet csomag – telepítsd a `dotnet add package Aspose.OCR` paranccsal.  
- Egy gép CUDA‑kompatibilis GPU‑val (általában NVIDIA) és a megfelelő driverrel.  
- Egy mappa, amely tele van a feldolgozni kívánt **PNG** képekkel.  

Ha bármelyik is ismeretlennek tűnik, ne pánikolj. Az alábbi lépések tartalmazzák a szükséges pontos parancsokat, és megvitatjuk, mit tegyünk, ha nincs GPU.

## 1. lépés: Az OCR motor inicializálása és a GPU gyorsítás engedélyezése  

Az első dolog, amit tenned kell, egy `OcrEngine` példány létrehozása és a GPU támogatás bekapcsolása. Ez a jelző azt mondja az Aspose‑nak, hogy a natív CUDA könyvtárakat használja a háttérben.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU‑specific namespace
using System;

class GpuBatchDemo
{
    static void Main()
    {
        // Initialise the OCR engine
        var ocrEngine = new OcrEngine();

        // Enable GPU acceleration – huge speed boost for large batches
        ocrEngine.UseGpuAcceleration = true;
```

**Miért fontos:** `UseGpuAcceleration` nélkül minden képet a CPU dolgoz fel, ami nagyságrendekkel lassabb lehet, különösen a nagy felbontású PNG‑k esetén. A jelző engedélyezése felkészíti a motort, hogy később egy konkrét GPU eszközt is elfogadjon.

## 2. lépés: GPU eszköz ID beállítása (opcionális, de ajánlott)  

Ha a munkaállomásodnak egynél több GPU-ja van, kiválaszthatod, melyiket használod. Az eszköz ID‑k **0**‑tól kezdődnek, így a `0` az első GPU‑t, az `1` a másodikat választja, stb.

```csharp
        // Optional: Choose the GPU device – 0 selects the first GPU
        ocrEngine.GpuDeviceId = 0;   // <-- set gpu device id
```

**Pro tipp:** Megosztott szerveren történő futtatáskor a GPU eszköz ID explicit beállítása megakadályozhatja, hogy a feladatod erőforrásokat lopjon más folyamatokból. Ha kihagyod ezt a sort, az Aspose az alapértelmezett eszközt választja, ami általában megfelelő egy‑GPU‑s beállításnál.

## 3. lépés: Az összes PNG fájl összegyűjtése a kötegelt mappádból  

Ezután meg kell találnunk minden PNG‑t, amelyen OCR‑t szeretnél futtatni. A `Directory.GetFiles` metódus végzi a nehéz munkát.

```csharp
        // Retrieve all PNG images from the batch folder
        string[] imageFiles = System.IO.Directory.GetFiles(
            @"YOUR_DIRECTORY\Batch",   // <-- replace with your path
            "*.png",                  // only PNG files
            System.IO.SearchOption.TopDirectoryOnly);
```

**Szélsőséges eset:** Ha a mappa üres, a `imageFiles` egy üres tömb lesz. Ezt később egy barátságos üzenettel kezeljük.

## 4. lépés: Minden kép feldolgozása és a felismert karakterek számának kiírása  

Most a fő ciklus. Minden PNG‑nél meghívjuk a `Recognize` metódust, majd kiírjuk a fájl nevét és a kinyert szöveg hosszát.

```csharp
        // Verify we actually found files
        if (imageFiles.Length == 0)
        {
            Console.WriteLine("No PNG files found in the specified folder.");
            return;
        }

        // Process each image and display the recognised character count
        foreach (var imagePath in imageFiles)
        {
            var ocrResult = ocrEngine.Recognize(imagePath);
            Console.WriteLine($"{System.IO.Path.GetFileName(imagePath)} → {ocrResult.Text.Length} chars");
        }
    }
}
```

**Ami megjelenik:**  
```
invoice1.png → 342 chars
receipt_2023.png → 127 chars
screenshot.png → 0 chars
```

Ha egy kép nem tartalmaz szöveget, a számláló `0` lesz. Ez teljesen normális a kizárólag grafikus képernyőképeknél.

## 5. lépés: A program futtatása és a GPU használat ellenőrzése  

Fordítsd le a fájlt (`dotnet build`) és futtasd (`dotnet run`). Amíg a konzol görget, megnyithatod a GPU monitorozó eszközödet (például NVIDIA Smi), hogy lásd a GPU kihasználtság rövid emelkedését minden egyes kép esetén. Ha nem látsz semmilyen aktivitást, ellenőrizd újra, hogy:

1. A CUDA driver telepítve van.  
2. `UseGpuAcceleration` `true`‑ra van állítva.  
3. A megfelelő `GpuDeviceId` egy fizikai GPU‑nak felel meg.  

Ha a GPU nem érhető el, az Aspose automatikusan visszaáll CPU‑ra, de elveszíted a sebesség előnyét.

## Gyakori variációk és tippek  

| Helyzet | Mit kell módosítani |
|-----------|----------------|
| **Eltérő képformátum** (pl. JPEG) | Módosítsd a keresési mintát `*.jpg` vagy `*.*`-re, és az Aspose továbbra is fel fogja ismerni a szöveget. |
| **A köteg mérete óriási** (ezrek fájl) | Feldolgozd darabokban a memória nyomás elkerülése érdekében: oszd fel a `imageFiles`-t kisebb tömbökre. |
| **A tényleges szövegre van szükség, nem csak a hosszra** | Cseréld le a `ocrResult.Text.Length`-t `ocrResult.Text`-re a `WriteLine`-ban. |
| **Fej nélküli szerveren futtatás** | Győződj meg róla, hogy a szerveren van GPU driver; ellenkező esetben állítsd `UseGpuAcceleration = false`-ra a felesleges hibák elkerülése érdekében. |
| **Több GPU, terhelés kiegyensúlyozása** | A `foreach` belsejében ciklusba foglald a `ocrEngine.GpuDeviceId = i % gpuCount`-t az eszközök váltogatásához. |

## Várható kimenet és ellenőrzés  

Ha minden működik, a konzol kiírja minden fájl nevét a karakter számlálóval, ahogy korábban láttad. A tényleges OCR kimenet dupla ellenőrzéséhez ideiglenesen kiírhatod a szöveget:

```csharp
Console.WriteLine($"{Path.GetFileName(imagePath)} → {ocrResult.Text}");
```

Csak ne feledd, hogy nagy kötegek esetén távolítsd el vagy kommentáld ki ezt a sort; több ezer sor kiírása eláraszthatja a terminált.

## Teljes működő példa (másolás‑beillesztés kész)

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU‑specific namespace
using System;

class GpuBatchDemo
{
    static void Main()
    {
        // Step 1: Initialise the OCR engine and enable GPU acceleration
        var ocrEngine = new OcrEngine();
        ocrEngine.UseGpuAcceleration = true;

        // Step 2: (Optional) Choose the GPU device – 0 selects the first GPU
        ocrEngine.GpuDeviceId = 0;   // <-- set gpu device id

        // Step 3: Retrieve all PNG images from the batch folder
        string[] imageFiles = System.IO.Directory.GetFiles(
            @"YOUR_DIRECTORY\Batch",   // replace with your folder path
            "*.png",
            System.IO.SearchOption.TopDirectoryOnly);

        // Guard clause if no files are found
        if (imageFiles.Length == 0)
        {
            Console.WriteLine("No PNG files found in the specified folder.");
            return;
        }

        // Step 4: Process each image and display the recognised character count
        foreach (var imagePath in imageFiles)
        {
            var ocrResult = ocrEngine.Recognize(imagePath);
            Console.WriteLine($"{System.IO.Path.GetFileName(imagePath)} → {ocrResult.Text.Length} chars");
        }
    }
}
```

Mentsd el `GpuBatchDemo.cs` néven, futtasd a `dotnet add package Aspose.OCR` parancsot, majd `dotnet run`. A karakter számlálók szinte azonnal meg fognak jelenni minden PNG‑nél a GPU gyorsításnak köszönhetően.

## Következtetés  

Most már tudod, hogyan **szöveget felismerj png** fájlokból hatékonyan a GPU gyorsítás engedélyezésével és az Aspose OCR‑ban az **set gpu device id** kifejezett beállításával. A teljes, másolás‑beillesztés program kezeli a mappa felderítését, a szélsőséges esetek ellenőrzését, és azonnali visszajelzést ad az OCR teljesítményéről.

Következő lépések? Próbáld megcserélni a `Recognize` hívást `ocrEngine.RecognizeAsync`-ra, ha nem blokkoló feldolgozásra van szükséged, vagy kísérletezz az Aspose által biztosított különböző kép előfeldolgozási lehetőségekkel (pl. binarizálás). Az OCR eredményeket át is irányíthatod egy adatbázisba vagy kereső indexbe egy teljes szöveges keresési megoldáshoz.

Van kérdésed a többoldalas PDF‑ek kezelésével kapcsolatban, vagy szeretnéd összehasonlítani az Aspose OCR‑t a Tesseract‑tal? Hagyj egy megjegyzést, vagy nézd meg a többi útmutatónkat a **batch OCR C#**, **OCR teljesítmény tippek**, és **GPU‑vezérelt képfeldolgozás** témakörökben. Boldog kódolást!  

![Konzol kimenet, amely a PNG fájlok felismert karakter számlálóját mutatja – szöveg felismerése png‑ből GPU gyorsítással](image-placeholder.png "szöveg felismerése png kimeneti példa")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}