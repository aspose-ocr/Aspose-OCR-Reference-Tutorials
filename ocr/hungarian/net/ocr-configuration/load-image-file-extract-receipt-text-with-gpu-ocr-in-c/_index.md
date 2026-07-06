---
category: general
date: 2026-02-14
description: Töltsd be a képfájlt, és nyerd ki a szöveget a nyugtáról az Aspose OCR
  GPU motor segítségével. Tanuld meg, hogyan állítsd be a maximális GPU memóriát,
  konfiguráld a GPU memóriát, és futtasd hatékonyan az OCR-t a képen.
draft: false
keywords:
- load image file
- extract text from receipt
- set max gpu memory
- run OCR on image
- configure gpu memory
language: hu
og_description: Kép fájl betöltése és a nyugtáról szöveg kinyerése az Aspose OCR GPU
  motor segítségével. Ez az útmutató bemutatja, hogyan állítható be a maximális GPU
  memória, és hogyan futtatható az OCR a képen C#-ban.
og_title: Képfájl betöltése és nyugta szövegének kinyerése GPU OCR-rel C#‑ban
tags:
- C#
- OCR
- Aspose
- GPU
title: Képfájl betöltése és nyugtatext kinyerése GPU OCR-rel C#‑ban
url: /hu/net/ocr-configuration/load-image-file-extract-receipt-text-with-gpu-ocr-in-c/
---

.

Now produce final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kép fájl betöltése és nyugta szövegének kinyerése GPU OCR-rel C#-ban

Valaha is szükséged volt **load image file** betöltésére és a nyugta pontos szövegének kinyerésére, de az OCR lépésnél elakadtál? Nem vagy egyedül. Sok valós alkalmazásban—költségkövetők, készletkezelő rendszerek vagy akár egyszerű nyugta‑szkennelő botok—a nyugta képének gyors olvasása igazi fordulópont lehet.  

A jó hír? Az Aspose.OCR GPU‑gyorsított motorjával **load image file**, **set max GPU memory**, és **run OCR on image** néhány tiszta C# sorban elvégezheted. Az alábbiakban végigvezetünk a teljes folyamaton, a GPU konfigurálásától a kinyert egyszerű szöveg kiírásáig.

## Mit fogsz megtanulni

* **Load image file** betöltése lemezről az Aspose `ImageStream` segítségével.
* **Configure GPU memory** úgy, hogy a motor soha ne használjon fel több RAM-ot, mint amit engedélyezel.
* **Run OCR on image** és minden karakter kinyerése a nyugtáról.
* Gyakori buktatók kezelése—például memóriahiány hibák vagy elmosódott szkennelések.
* A kimenet ellenőrzése és a beállítások finomhangolása a jobb pontosság érdekében.

Nincs külső szolgáltatás, nincs rejtett trükk—csak tiszta C# kód, amit bármely .NET 6+ projektbe beilleszthetsz.

---

## Előfeltételek

Mielőtt belemerülnénk, győződj meg róla, hogy rendelkezel:

* .NET 6 SDK vagy újabb telepítve.
* Érvényes Aspose.OCR licenccel (vagy használhatod az ingyenes értékelő módot).
* A `Aspose.OCR` és `Aspose.OCR.Gpu` NuGet csomagok hozzáadva a projekthez.
* Egy mintanyugta kép (`receipt.png`) a lemezen készen áll.

Ha valamelyik ismeretlennek tűnik, állj meg egy pillanatra és telepítsd a csomagokat:

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Gpu
```

Ennyi—nincs szükség extra natív könyvtárakra, mivel a GPU támogatás közvetlenül a NuGet csomagba van beépítve.

## Kép fájl betöltése és GPU motor előkészítése

Az első dolog, amit meg kell tenned, hogy **load image file** egy `ImageStream`‑be töltsd. Ez az objektum elrejti a fájlrendszer részleteit, és tiszta, memória‑beli reprezentációt ad az OCR motor számára.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;

// Step 1️⃣: Initialize the GPU‑accelerated engine.
var gpuEngine = new GpuEngine
{
    // Step 2️⃣: Set a safety net for GPU RAM usage.
    // Here we limit the engine to 1024 MB (1 GB). Adjust as needed.
    MaxDeviceMemory = 1024 // MB
};

// Step 3️⃣: Load the receipt image from disk.
var receiptImage = ImageStream.FromFile(@"C:\MyReceipts\receipt.png");

// At this point the image is ready for OCR.
```

**Miért fontos ez:**  
*A kép fájl* betöltése `ImageStream.FromFile`‑nal garantálja, hogy a motor a pontos pixel adatokat lássa, megőrizve a DPI‑t és a színmélységet. Ennek a lépésnek a kihagyása vagy egy sérült stream átadása miatt az OCR karaktereket hagyhat ki vagy kivételt dobhat.

> **Pro tipp:** Ha felhasználók által feltöltött fájlokkal dolgozol, tedd a `FromFile` hívást try‑catch blokkba, és először ellenőrizd a fájl méretét. Nagy képek felrobbantják a GPU memóriát, ha nem **configured GPU memory** megfelelően.

## Maximális GPU memória beállítása az optimális teljesítményhez

A GPU erőforrások értékesek, különösen megosztott szervereken vagy korlátozott VRAM-mal rendelkező laptopokon. A `MaxDeviceMemory` tulajdonság megmondja az Aspose-nak, hogy a GPU memóriájának mekkora részét oszthatja biztonságosan.

```csharp
// Example: Restrict to 512 MB for low‑end GPUs.
gpuEngine.MaxDeviceMemory = 512; // MB
```

Amikor **set max GPU memory**, a motor automatikusan visszatér a CPU feldolgozáshoz, ha a kérés nem teljesíthető—ez megelőzi az összeomlásokat. Ez a legbiztonságosabb mód a **configure GPU memory** beállítására anélkül, hogy eszköz‑specifikus korlátokat kódolnál be.

**Mikor érdemes módosítani:**  
* Ha `OutOfMemoryException`-t észlelsz intenzív kötegelt feldolgozás során, csökkentsd a limitet.  
* Ha a nyugtáid nagy felbontásúak (300 DPI+), növeld 2 GB-ra a sebesség fenntartásához.

## OCR futtatása képen a nyugta szövegének kinyeréséhez

Most a szórakoztató rész—valóban **run OCR on image**, és kinyered a nyugta szövegét. A `Recognize` metódus egy `OcrResult` objektumot ad vissza, amelynek `Text` tulajdonsága a egyszerű szöveges kimenetet tartalmazza.

```csharp
// Step 4️⃣: Perform OCR.
OcrResult ocrResult = gpuEngine.Recognize(receiptImage);

// Step 5️⃣: Output the extracted text.
Console.WriteLine("=== Receipt Text ===");
Console.WriteLine(ocrResult.Text);
```

A konzol valami ilyesmit fog mutatni:

```
=== Receipt Text ===
Store: Coffee Corner
Date: 02/13/2026
Item            Qty   Price
Latte           2     $5.00
Muffin          1     $2.50
Total                     $12.50
```

**Miért működik ez:**  
A GPU motor egy mély‑tanulási modellt futtat, amelyet különféle dokumentumelrendezéseken képeztek ki. Egy tiszta, helyesen betöltött kép átadásával a modellnek a legjobb esélye van a **extract text from receipt** pontos kinyerésére.

## A kimenet ellenőrzése és gyakori buktatók

Még egy erőteljes motor esetén sem varázslat az OCR. Íme néhány dolog, amire figyelj:

| Probléma | Ok | Megoldás |
|----------|----|----------|
| Elcsúszott karakterek | Alacsony kontraszt vagy elmosódott kép | Előfeldolgozás az Aspose `ImageProcessor`‑rel a kontraszt növeléséhez |
| Hiányzó sorok | A kép túl szorosan van levágva | Győződj meg róla, hogy a nyugta teljesen belefér a kép határaiba |
| Memóriahiány hibák | `MaxDeviceMemory` túl alacsony a kép méretéhez | `MaxDeviceMemory` növelése vagy a kép először lecsökkentése |
| Helytelen nyelv | A nyugta nem angol szöveget tartalmaz | `gpuEngine.Language = OcrLanguage.Spanish;` (vagy megfelelő) beállítása |

Ha valamelyikre belefutsz, a gyors megoldás, hogy a képet a leghosszabb oldalán 2000 px alá méretezd—ez jelentősen csökkenti a GPU terhelést anélkül, hogy a legtöbb nyugta olvashatóságát feláldozná.

## Teljes működő példa (másolás-beillesztés kész)

Az alábbiakban a teljes program, készen áll a fordításra. Cseréld le a fájl útvonalát a saját nyugta helyére.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;

class ReceiptOcrDemo
{
    static void Main()
    {
        // 1️⃣ Create GPU‑accelerated engine with a safe memory cap.
        var gpuEngine = new GpuEngine
        {
            MaxDeviceMemory = 1024 // MB – adjust for your hardware
        };

        // 2️⃣ Load the receipt image from disk.
        //    Make sure the path points to a valid PNG/JPEG file.
        var receiptImage = ImageStream.FromFile(@"C:\MyReceipts\receipt.png");

        // 3️⃣ Run OCR – this will automatically use the GPU if available.
        OcrResult ocrResult = gpuEngine.Recognize(receiptImage);

        // 4️⃣ Print the extracted text.
        Console.WriteLine("=== Receipt Text ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Várható konzol kimenet** (a nyugta természetesen eltérő lesz):

```
=== Receipt Text ===
Store: Coffee Corner
Date: 02/13/2026
Item            Qty   Price
Latte           2     $5.00
Muffin          1     $2.50
Total                     $12.50
```

Futtasd a programot a `dotnet run` paranccsal. Ha a szöveget kiírja, gratulálok—sikeresen **load image file**, **set max GPU memory**, és **run OCR on image** a **extract text from receipt** érdekében.

## Gyakran Ismételt Kérdések

**Q: Működik ez dedikált GPU nélküli gépeken?**  
A: Igen. Az Aspose.OCR elegánsan visszatér CPU módba, ha nem észlel kompatibilis GPU-t. Továbbra is képes leszel **load image file** és **run OCR on image**, csak valamivel lassabban.

**Q: Feldolgozhatok több nyugtát egy kötegben?**  
A: Természetesen. Tedd a felismerő kódot egy `foreach` ciklusba, de ne feledd újrahasználni ugyanazt a `GpuEngine` példányt—ez elkerüli a GPU erőforrások újra‑inicializálását minden fájlhoz.

**Q: Mi van, ha a nyugta nem angol nyelvű?**  
A: Állítsd be a nyelvet a `Recognize` hívása előtt:

```csharp
gpuEngine.Language = OcrLanguage.French;
```

A motor ezután a megfelelő karakterkészletet alkalmazza.

## Következő lépések és kapcsolódó témák

Miután elsajátítottad az alapokat, fontold meg a következők felfedezését:

* **Fine‑tuning OCR accuracy** – kísérletezz a `gpuEngine.RecognitionOptions` beállításokkal, például `EnableDeskew` vagy `ContrastEnhancement`.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}