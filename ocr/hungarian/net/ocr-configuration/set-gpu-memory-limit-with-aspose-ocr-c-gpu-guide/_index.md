---
category: general
date: 2026-04-03
description: GPU memória limit beállítása Aspose OCR használatával C#-ban. Tanulja
  meg, hogyan konfigurálja a GPU memóriát, hogyan ismerje fel az orosz szöveget, és
  hogyan kerülje el a gyakori hibákat.
draft: false
keywords:
- set gpu memory limit
- Aspose OCR GPU
- C# GPU OCR
- GPU memory management
- Aspose OcrEngine settings
- limit GPU memory usage
language: hu
og_description: GPU memória korlát beállítása Aspose OCR-rel C#-ban. Ez az útmutató
  lépésről lépésre bemutatja, hogyan konfiguráljuk a GPU memóriát, futtassuk az OCR-t,
  és kezeljük a szélsőséges eseteket.
og_title: GPU memória korlát beállítása Aspose OCR segítségével – C# GPU útmutató
tags:
- Aspose
- OCR
- C#
- GPU
title: GPU memória korlát beállítása az Aspose OCR-rel – C# GPU útmutató
url: /hu/net/ocr-configuration/set-gpu-memory-limit-with-aspose-ocr-c-gpu-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# GPU memória korlát beállítása az Aspose OCR-rel – Teljes C# útmutató

Valaha is szükséged volt **GPU memória korlát beállítására** egy OCR feladathoz, és nem tudtad, hol kezdjed? Nem vagy egyedül – sok fejlesztő szembesül a problémával, amikor a GPU memória elfogy, miközben nagy felbontású nyugtákat vagy számlákat dolgoz fel. A jó hír, hogy az Aspose OCR GPU támogatása lehetővé teszi a memóriahasználat korlátozását néhány kódsorral, így alkalmazásod stabil maradhat, és még mindig élvezheted a hardveres gyorsítás sebességnyereségét.

Ebben az útmutatóban végigvezetünk a teljes folyamaton: az Aspose OCR GPU támogatással való telepítése, a **GpuSettings** konfigurálása a **GPU memória korlát beállításához**, egy orosz nyelvű OCR feladat futtatása, és a leggyakoribb hibák elhárítása. A végére egy futtatható C# konzolalkalmazást kapsz, amely tiszteletben tartja a memória korlátaidat, és tiszta szöveget ad vissza.

## Előkövetelmények

- .NET 6.0 SDK vagy újabb (az API működik .NET Core és .NET Framework alatt)
- CUDA‑t (NVIDIA) vagy DirectX 12‑t (Windows) támogató GPU
- Visual Studio 2022 vagy bármely kedvenc IDE
- `receipt.png` képfájl, amelyet feldolgozni szeretnél
- **Aspose.OCR** NuGet csomag (a GPU‑támogatott verzió)

> **Pro tipp:** Ha fejlesztői gépen korlátozott GPU RAM-mal dolgozol, kezd `MaxMemory = 512` MB értékkel, és csak szükség szerint növeld.

## 1. lépés: Aspose OCR telepítése GPU támogatással

Először add hozzá az Aspose OCR könyvtárat, amely tartalmazza a GPU kötéseket.

```bash
dotnet add package Aspose.OCR.Gpu
```

## 2. lépés: A feldolgozni kívánt kép betöltése

`System.Drawing.Image`-t használjuk a nyugta fájl beolvasásához. Győződj meg róla, hogy az útvonal egy létező fájlra mutat; különben a program `FileNotFoundException`-t dob.

```csharp
using System;
using System.Drawing;
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU support namespace

class GpuDemo
{
    static void Main()
    {
        // Load the image from disk
        Image receiptImage = Image.FromFile(@"YOUR_DIRECTORY/receipt.png");
```

> **Miért fontos:** A kép korai betöltése lehetővé teszi, hogy ellenőrizzük a fájl elérhetőségét, mielőtt GPU erőforrásokat foglalnánk.

## 3. lépés: OCR motor létrehozása és **GPU memória korlát beállítása**

Most jön a tutorial szíve – a `GpuSettings` konfigurálása, hogy az OCR motor **GPU memória korlátot állítson be** egy biztonságos értékre. A `MaxMemory` tulajdonság megabájtban várja az értéket.

```csharp
        // Initialize the OCR engine with GPU settings
        OcrEngine ocrEngine = new OcrEngine(new GpuSettings
        {
            // Primary keyword in action: set GPU memory limit to 1024 MB
            MaxMemory = 1024,               // limit GPU memory usage (in MB)
            AutoDownloadResources = true   // automatically fetch language packs
        });
```

Vedd észre, hogy a **GPU memória korlátot** közvetlenül a `GpuSettings` objektumban állítjuk be. Ez azt mondja az Aspose OCR-nek, hogy legfeljebb 1 GB GPU RAM-ot foglaljon, megelőzve a memóriahiányos összeomlásokat közepes GPU-kkal.

## 4. lépés: Felismerési nyelv kiválasztása

Az Aspose OCR több mint 100 nyelvet támogat. Ebben a demóban orosz szöveget fogunk felismerni, de a `OcrLanguage.Russian`-t bármely más támogatott enum értékre cserélheted.

```csharp
        // Select the language for OCR
        ocrEngine.Language = OcrLanguage.Russian;
```

Ha egy futtatás során több nyelvet kell feldolgozni, használhatod a `OcrLanguage.Multilingual`-t vagy kombinálhatod a flag-eket.

## 5. lépés: OCR folyamat futtatása

A motor konfigurálása után hívd meg a `Recognize` metódust, és add át a betöltött képet. A metódus visszaadja a kinyert szöveget.

```csharp
        // Perform OCR on the image
        string recognizedText = ocrEngine.Recognize(receiptImage);

        // Show the result in the console
        Console.WriteLine("GPU OCR result:");
        Console.WriteLine(recognizedText);
    }
}
```

**Várható kimenet** (rövidítve a tömörség kedvéért):

```
GPU OCR result:
Кассовый чек № 12345
Дата: 03/04/2026
Сумма: 1 250,00 ₽
```

Ha a GPU memória korlát túl alacsony, az Aspose OCR automatikusan CPU feldolgozásra vált, amit a konzolnaplóban figyelmeztetésként láthatsz.

## 6. lépés: Ellenőrizd, hogy a memória korlát betartásra került-e

Az Aspose OCR diagnosztikai információkat ír a szabványos kimenetre, ha az `AutoDownloadResources` engedélyezve van. Keress egy hasonló sort:

```
[INFO] GPU memory allocated: 987 MB (requested max: 1024 MB)
```

Ha a lefoglalt mennyiség meghaladja a `MaxMemory` beállításodat, ellenőrizd, hogy a GPU csomag megfelelő verzióját használod-e, és hogy a driver támogatja-e a korlát API-t.

## Gyakori buktatók és tippek (Másodlagos kulcsszavak akcióban)

### 1. **Aspose OCR GPU** nem ismerhető

- Győződj meg róla, hogy a fájl tetején importáltad az `Aspose.OCR.Gpu`-t.
- Ellenőrizd, hogy a NuGet csomag verziója megegyezik a .NET futtatókörnyezeteddel (pl. 23.10 vagy újabb).

### 2. **C# GPU OCR** `DllNotFoundException`-t dob

- Ez általában azt jelenti, hogy a natív CUDA könyvtárak nincsenek a rendszer `PATH`-jában. Telepítsd a legújabb CUDA toolkit-et, vagy másold a `cudart64_*.dll` fájlokat a végrehajtható mappába.

### 3. **GPU memória kezelés** kézi kezelése

- Futásidőben módosíthatod a `MaxMemory`-t, ha különböző méretű kötegeket dolgozol fel. Egyszerűen hozd létre újra az `OcrEngine`-t egy új `GpuSettings`-tel minden egyes köteg előtt.

### 4. **Aspose OcrEngine beállítások** használata kötegelt feldolgozáshoz

```csharp
foreach (var file in Directory.GetFiles(@"batch_folder", "*.png"))
{
    Image img = Image.FromFile(file);
    ocrEngine.Language = OcrLanguage.English; // switch language per batch
    string text = ocrEngine.Recognize(img);
    // store or log `text` as needed
}
```

### 5. **GPU memória használat korlátozása** több bérlővel rendelkező szervereken

- Ha több szolgáltatás osztozik ugyanazon a GPU-n, minden szolgáltatásnak egy szeletet oszthatsz a `MaxMemory` beállításával a teljes VRAM egy részére (pl. `MaxMemory = totalVRAM / servicesCount`).

## Teljes működő példa

Az alábbiakban a teljes, másolás‑beillesztésre készen álló program látható, amely **GPU memória korlátot állít be**, futtatja az OCR-t, és kiírja az eredményt. Mentsd `Program.cs` néven, és futtasd a `dotnet run` parancsot.

```csharp
using System;
using System.Drawing;
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU support

class GpuDemo
{
    static void Main()
    {
        // Step 1: Load the image
        Image receiptImage = Image.FromFile(@"YOUR_DIRECTORY/receipt.png");

        // Step 2: Create OCR engine with GPU settings (set GPU memory limit)
        OcrEngine ocrEngine = new OcrEngine(new GpuSettings
        {
            MaxMemory = 1024,               // limit GPU memory usage to 1 GB
            AutoDownloadResources = true   // fetch language data automatically
        });

        // Step 3: Choose language (Russian in this example)
        ocrEngine.Language = OcrLanguage.Russian;

        // Step 4: Perform OCR
        string recognizedText = ocrEngine.Recognize(receiptImage);

        // Step 5: Display result
        Console.WriteLine("GPU OCR result:");
        Console.WriteLine(recognizedText);
    }
}
```

Futtasd a programot, és a konzolon meg kell jelennie az OCR szövegnek, a GPU memória korlát betartásával a teljes művelet során.

## Összegzés

Most bemutattuk, hogyan **állítható be a GPU memória korlát** az Aspose OCR GPU motorjának C#-ból történő használatakor. A `GpuSettings.MaxMemory` konfigurálásával finomhangolt vezérlést kapsz a VRAM fogyasztás felett, elkerülheted a lemez alacsony végű GPU-k összeomlását, és még mindig élvezheted a hardveres gyorsítás teljesítményelőnyeit. Az útmutató lefedte a telepítést, a kódlépéseket, az ellenőrzést, és néhány gyakorlati tippet a **Aspose OCR GPU**, **C# GPU OCR**, és **GPU memória kezelés** témakörökben.

Mi a következő? Kísérletezz nagyobb képekkel, különböző nyelvekkel, vagy akár több `OcrEngine` példány párhuzamosításával – csak ne feledd, hogy minden példány `MaxMemory` értékét a teljes VRAM költségvetésen belül tartsd. Ha hasznosnak találtad ezt az útmutatót, oszd meg a csapattagokkal, vagy hagyj egy megjegyzést, ha bármilyen problémába ütköztél.

Boldog kódolást, és legyen a GPU-d hűvös! 

![GPU memória korlát beállítása példa](placeholder-image.png "GPU memória korlát beállítása példa")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}