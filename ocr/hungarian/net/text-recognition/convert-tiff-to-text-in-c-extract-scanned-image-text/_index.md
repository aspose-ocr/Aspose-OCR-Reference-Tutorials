---
category: general
date: 2026-03-05
description: Konvertálja a TIFF fájlokat szöveggé C#-ban az Aspose OCR segítségével—gyorsan
  nyerjen ki szöveget beolvasott képfájlokból, és tanulja meg, hogyan töltsön be képfájlt
  C#-ban OCR feldolgozáshoz.
draft: false
keywords:
- convert TIFF to text
- extract text scanned image
- load image file C#
language: hu
og_description: Konvertálja a TIFF-et szöveggé C#-ban az Aspose OCR használatával.
  Ismerje meg a teljes munkafolyamatot a beolvasott képek szövegének kinyeréséhez
  és a képfájlok hatékony betöltéséhez.
og_title: TIFF konvertálása szöveggé C#‑ban – Szkennelt kép szövegének kinyerése
tags:
- OCR
- C#
- Aspose
title: TIFF konvertálása szöveggé C#-ban – Szkennelt kép szövegének kinyerése
url: /hu/net/text-recognition/convert-tiff-to-text-in-c-extract-scanned-image-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# TIFF konvertálása szöveggé C#‑ban – Szkennelt kép szövegének kinyerése

Szükséged van **TIFF szöveggé konvertálására C#‑ban**? Nem vagy egyedül azokkal a többoldalas szkennelt képekkel, amelyek makacsul ellenállnak, hogy kereshető karakterláncokká váljanak.  
Ebben az útmutatóban végigvezetünk egy teljes, azonnal futtatható megoldáson, amely egy TIFF fájlt vesz, átadja az Aspose OCR‑nek, és egyszerű szöveget ad vissza—további szolgáltatások vagy rejtett varázslat nélkül.

> **Pro tip:** Ha nagy felbontású szkennelésekkel dolgozol, a GPU feldolgozás engedélyezése másodperceket takaríthat meg oldalanként.

Megmutatjuk, hogyan **kinyerheted a szkennelt képfájlok szövegét** és a legjobb módját annak, hogy **C#‑ban betölts egy képfájlt** az OCR motorba, így ma már beágyazhatod ezt a logikát bármely .NET projektbe.

---

## Amire szükséged lesz

Mielőtt belevágunk, győződj meg róla, hogy a következők telepítve vannak a gépeden:

| Követelmény | Ok |
|-------------|----|
| .NET 6.0+ (vagy .NET Framework 4.7.2+) | Modern futtatókörnyezet, támogatja a `Span<T>`‑t és az aszinkron I/O‑t |
| Aspose.OCR for .NET (NuGet csomag `Aspose.OCR`) | Az OCR motor, amelyet használni fogunk |
| Érvényes Aspose OCR licencfájl (`Aspose.OCR.lic`) | Enélkül el fogod érni a kiértékelési korlátokat |
| Egy TIFF fájl (egyetlen vagy többoldalas) a teszteléshez | Példa: `scanned_multi_page.tif` |
| GPU CUDA 11+ támogatással (opcionális) | Felgyorsítja a felismerést, ha `EngineMode = Gpu` |

Ha valamelyik hiányzik, szerezd be most a NuGet csomagot:

```bash
dotnet add package Aspose.OCR
```

## 1. lépés: A projekt beállítása és a névterek importálása

Hozz létre egy új konzolos alkalmazást (vagy add hozzá a kódot egy meglévő projekthez). Az első dolog, amit teszünk, hogy importáljuk a szükséges osztályokat.

```csharp
using System;
using Aspose.OCR;          // Core OCR classes
using Aspose.OCR.Image;   // ImageStream helper
```

> **Miért fontos ez:** Az `Aspose.OCR.Image` importálása biztosítja számunkra az `ImageStream` gyárat, amely közvetlenül a lemezről vagy egy adatfolyamból képes TIFF fájlokat olvasni. Ennek a lépésnek a kihagyása fordítási hibát okoz.

## 2. lépés: Az OCR motor inicializálása és a feldolgozási mód kiválasztása

Az OCR motort **mielőtt** bármilyen képet hozzárendelnél konfigurálni kell. Itt döntjük el, hogy CPU-n vagy GPU-n futtassuk.

```csharp
// Step 2: Initialize the OCR engine and enable GPU processing (must be set before any OCR work)
OcrEngine ocrEngine = new OcrEngine();

// Choose the processing mode that fits your environment.
// Options: Cpu (default) | Gpu | Auto
ocrEngine.EngineMode = OcrEngineMode.Gpu;   // Switch to Cpu if you don’t have a compatible GPU
```

*Ha egy grafikus kártya nélküli headless szerveren vagy, változtasd a `Gpu`‑t `Cpu`‑ra vagy `Auto`‑ra.*  
A motor módja befolyásolja a memóriafoglalást és a sebességet; a GPU mód 2‑3× gyorsabb lehet nagy, nagy felbontású TIFF‑eken.

## 3. lépés: Az Aspose OCR licenc alkalmazása

Licenc nélkül futtatva csak néhány oldalra és vízjelekre vagy korlátozva. Töltsd be a licencet korán, hogy minden későbbi művelet korlátlan legyen.

```csharp
// Step 3: Apply the Aspose OCR license (replace with your own license file if needed)
ocrEngine.SetLicense("Aspose.OCR.lic");
```

> **Gyakori hibaforrás:** A `SetLicense` elhelyezése a `Recognize()` után azt eredményezi, hogy a motor az adott hívásra visszatér a próbaverzió módba.

## 4. lépés: A TIFF fájl betöltése – Egy- és többoldalas képek kezelése

Az Aspose OCR képes többoldalas TIFF‑eket natívan olvasni, de a megfelelő adatfolyamot kell átadni. Íme egy robusztus minta, amely mindkét esetben működik.

```csharp
// Step 4: Load the image to be recognized
string tiffPath = @"YOUR_DIRECTORY\scanned_multi_page.tif";

using (var imageStream = ImageStream.FromFile(tiffPath))
{
    // Step 5: Assign the image to the engine
    ocrEngine.Image = imageStream;

    // Step 6: Perform the OCR operation
    OcrResult ocrResult = ocrEngine.Recognize();

    // Step 7: Output the recognized text
    Console.WriteLine("=== OCR Output ===");
    Console.WriteLine(ocrResult.Text);
}
```

### Miért használjuk az `ImageStream.FromFile`‑t?

- Elrejti a háttérben lévő `FileStream`‑et, és belsőleg kezeli a TIFF oldalak felsorolását.  
- `MemoryStream`‑mel is működik, így képeket tölthetsz be adatbázisból vagy web API‑ból anélkül, hogy a fájlrendszert érintenéd.

### Szélsőséges eset: Nagyon nagy TIFF‑ek

Ha a TIFF fájlod meghaladja a 200 MB‑ot, fontold meg oldalankénti betöltését, hogy elkerüld a memóriahiányos kivételeket:

```csharp
int pageCount = ImageInfo.GetPageCount(tiffPath);
for (int i = 0; i < pageCount; i++)
{
    using var pageStream = ImageStream.FromFile(tiffPath, i);
    ocrEngine.Image = pageStream;
    var pageResult = ocrEngine.Recognize();
    Console.WriteLine($"--- Page {i + 1} ---");
    Console.WriteLine(pageResult.Text);
}
```

## 5. lépés: A kimenet ellenőrzése

A program futtatásakor valami ilyesmit kell látnod:

```
=== OCR Output ===
Invoice #12345
Date: 2024‑12‑01
Total: $1,250.00
Thank you for your business!
```

Ha a szöveg torzultnak tűnik, ellenőrizd a következőket:

1. **Felbontás** – Az OCR a legjobban 300 dpi vagy annál magasabb felbontásnál működik.  
2. **EngineMode** – Válts `Cpu`‑ra, ha a GPU driver elavult.  
3. **Licenc** – Győződj meg róla, hogy a licencfájl elérési útja helyes és a fájl olvasható.

## Gyakran Ismételt Kérdések (GYIK)

### Működik ez más képformátumokkal is?

Természetesen. Az `ImageStream.FromFile` támogatja a JPEG, PNG, BMP és még a PDF (az Aspose.PDF‑en keresztül) formátumokat is. Csak cseréld ki a fájlkiterjesztést.

### Mi a teendő, ha adatbázisban tárolt képeket kell feldolgozni?

Olvasd be a BLOB‑ot egy `MemoryStream`‑be, és add át az `ImageStream.FromStream(memoryStream)`‑nek. Az OCR motor ugyanúgy kezeli, mint egy fájl‑alapú adatfolyamot.

### Futtatható ez Linuxon?

Igen—az Aspose OCR platformfüggetlen. Telepítsd a megfelelő .NET futtatókörnyezetet, és győződj meg róla, hogy a GPU‑hoz szükséges natív könyvtárak (ha használod) elérhetők.

## Teljes működő példa (másolás-beillesztés kész)

Az alábbiakban a teljes program található, készen áll a fordításra. Cseréld ki a `YOUR_DIRECTORY`‑t és a licencfájl útvonalát a saját helyeidre.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Image;

namespace TiffToTextDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Initialize OCR engine
            OcrEngine ocrEngine = new OcrEngine();

            // Choose processing mode: Gpu, Cpu, or Auto
            ocrEngine.EngineMode = OcrEngineMode.Gpu; // Change to Cpu if no GPU

            // Apply license (skip if you only need a trial)
            ocrEngine.SetLicense("Aspose.OCR.lic");

            // Path to the TIFF file
            string tiffPath = @"YOUR_DIRECTORY\scanned_multi_page.tif";

            // Load the TIFF (handles multi‑page automatically)
            using (var imageStream = ImageStream.FromFile(tiffPath))
            {
                // Assign image to engine
                ocrEngine.Image = imageStream;

                // Run OCR
                OcrResult result = ocrEngine.Recognize();

                // Display result
                Console.WriteLine("=== OCR Output ===");
                Console.WriteLine(result.Text);
            }

            // Optional: Process each page individually for huge files
            // int pages = ImageInfo.GetPageCount(tiffPath);
            // for (int i = 0; i < pages; i++) { ... }
        }
    }
}
```

Mentsd el `Program.cs`‑ként, futtasd a `dotnet run` parancsot, és figyeld a szöveget

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}