---
category: general
date: 2026-01-01
description: Hogyan végezzünk kötegelt OCR-t az Aspose OCR Engine segítségével C#-ban.
  Tanulja meg, hogyan ismerje fel a szöveget képeken, és hogyan nyerjen ki szöveget
  TIFF-fájlokból GPU-gyorsítással.
draft: false
keywords:
- how to batch OCR
- recognize text from images
- extract text from TIFF
language: hu
og_description: Hogyan végezzünk kötegelt OCR-t C#-ban az Aspose OCR motorral. Ez
  az útmutató megmutatja, hogyan ismerhetünk fel szöveget képekből, és hogyan vonhatunk
  ki szöveget TIFF fájlokból hatékonyan.
og_title: Hogyan végezzünk kötegelt OCR-t C#-ban – Teljes Aspose útmutató
tags:
- OCR
- C#
- Aspose
- GPU
title: Hogyan végezzünk kötegelt OCR-t C#-ban az Aspose OCR motorral
url: /hu/net/ocr-optimization/how-to-batch-ocr-in-c-with-aspose-ocr-engine/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan végezzünk kötegelt OCR-t C#-ban az Aspose OCR motorral

Valaha is elgondolkodtál **arról, hogyan végezzünk kötegelt OCR-t**, amikor egy mappában tucatnyi beolvasott dokumentum hever? Nem vagy egyedül – sok fejlesztő szembesül ezzel a problémával, amikor az egykép‑felismerésről egy teljes gyűjtemény feldolgozására vált. A jó hír, hogy az Aspose OCR ezt gyerekjátéká teszi, akár CPU‑n, akár a GPU gyorsítást használva.

Ebben az útmutatóban egy teljes, futtatható példán keresztül vezetünk végig, amely **képekből szöveget ismer fel** és akár **TIFF fájlokból is kinyer szöveget** tömegesen. Nincsenek homályos „lásd a dokumentációt” rövidítések – csak egy önálló megoldás, amelyet ma másolhatsz‑beilleszthetsz és futtathatsz.

## Előkövetelmények

* .NET 6.0 vagy újabb telepítve (a kód a .NET 6‑ra céloz, de a .NET 5 is működik).
* Aspose.OCR for .NET NuGet csomag (mind CPU, mind GPU verzió elérhető; telepítsd a hardverednek megfelelőt).
* Egy mappa néhány mintat TIFF vagy PNG fájllal, amelyeket fel szeretnél dolgozni.
* Visual Studio 2022 vagy bármely kedvelt IDE.

> **Pro tipp:** Ha a GPU verziót tervezed használni, ellenőrizd, hogy a grafikus driver naprakész-e, és hogy a CUDA 11+ telepítve van. A motor automatikusan visszaáll CPU‑ra, ha nem talál kompatibilis GPU‑t.

## 1. lépés – A projekt beállítása és az Aspose.OCR telepítése

### H2: Új konzolos alkalmazás létrehozása és az Aspose.OCR hozzáadása

Nyiss egy terminált (vagy a Package Manager Console‑t a Visual Studio‑ban) és futtasd:

```bash
dotnet new console -n GpuBatchDemo
cd GpuBatchDemo
dotnet add package Aspose.OCR --version 23.12
```

Ha GPU‑támogatott licenced van, add hozzá a GPU csomagot helyette:

```bash
dotnet add package Aspose.OCR.GPU --version 23.12
```

Ennyi—most a projekted hivatkozik az OCR könyvtárra, amelyet a **kötegelt OCR**-hez fogunk használni.

## 2. lépés – Az OCR motor inicializálása (CPU vagy GPU)

### H2: Hogyan végezzünk kötegelt OCR-t – Motor inicializálása

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;

class GpuBatchDemo
{
    static void Main()
    {
        // Create the OCR engine. It works with both CPU and GPU builds.
        var ocrEngine = new OcrEngine();

        // OPTIONAL: Force GPU usage if a compatible device is present.
        // Setting this to true won’t break on CPU‑only machines—it simply tries GPU first.
        ocrEngine.Settings.UseGpu = true;
```

**Miért fontos:** A `UseGpu` átkapcsolásával az Aspose dönt a leggyorsabb útról. Ha a GPU nem érhető el, a motor csendben visszakapcsol CPU‑ra, így a kötegelt feladat soha nem omlik össze hiányzó hardver miatt.

## 3. lépés – A feldolgozandó fájlok összegyűjtése

### H2: Szöveg felismerése képekről – Fájllista összeállítása

```csharp
        // Prepare a list of image files (TIFF, PNG, JPEG, etc.).
        var imageFiles = new List<string>
        {
            @"C:\OCR\Input\doc1.tif",
            @"C:\OCR\Input\doc2.tif",
            @"C:\OCR\Input\doc3.tif"
        };

        // You could also populate the list dynamically:
        // var imageFiles = Directory.GetFiles(@"C:\OCR\Input", "*.tif").ToList();
```

**Széljegyzet:** Ha különböző formátumok keverékével dolgozol, módosítsd a keresési mintát `"*.*"`‑re, és a cikluson belül szűrd a kiterjesztést. Ez rugalmasabbá teszi a kötegelt feldolgozást.

## 4. lépés – Minden kép feldolgozása és előnézet megjelenítése

### H2: Szöveg kinyerése TIFF-ből – Fájlok bejárása

```csharp
        // Loop through each file, run OCR, and print a short preview.
        foreach (var filePath in imageFiles)
        {
            // Load the image into Aspose's OcrImage object.
            var ocrImage = OcrImage.FromFile(filePath);

            // Run recognition.
            var ocrResult = ocrEngine.Recognize(ocrImage);

            // Display the first 50 characters of the recognized text.
            Console.WriteLine($"{filePath}: {ocrResult.Text.Substring(0, Math.Min(50, ocrResult.Text.Length))}...");
        }
    }
}
```

**Ami látható lesz:** Minden TIFF esetén a konzol valami ilyesmit ír ki:

```
C:\OCR\Input\doc1.tif: The quick brown fox jumps over the laz...
C:\OCR\Input\doc2.tif: Invoice #12345
Date: 2023-11-01
Total: $1,250.00
...
```

Ez az előnézet megerősíti, hogy a köteg sikeresen lefutott anélkül, hogy minden fájlt kézzel meg kellene nyitni.

## 5. lépés – Eredmények mentése (opcionális, de hasznos)

### H3: OCR kimenet mentése szövegfájlokba

Ha a teljes szövegre downstream feldolgozáshoz van szükséged, add hozzá ezt a `foreach` cikluson belül:

```csharp
            // Define an output path based on the source file name.
            var outputPath = Path.ChangeExtension(filePath, ".txt");
            File.WriteAllText(outputPath, ocrResult.Text);
```

Most minden TIFF-hez egy hozzá tartozó `.txt` fájl jön létre, amely a teljes OCR kimenetet tartalmazza – tökéletes indexeléshez, kereséshez vagy nyelvi modellbe való betápláláshoz.

## 6. lépés – A demó futtatása és ellenőrzése

1. Építsd fel a projektet: `dotnet build`.
2. Futtasd: `dotnet run --project GpuBatchDemo.csproj`.

Látnod kell a konzolra kiírt előnézeti sorokat, és (ha hozzáadtad az opcionális lépést) egy sor `.txt` fájlt a forrásképek mellett.

### H3: Gyakori hibák és megoldások

| Tünet | Valószínű ok | Megoldás |
|---------|--------------|-----|
| **Üres `ocrResult.Text`** | Túl sötét kép vagy alacsony DPI | Előfeldolgozás (kontraszt növelése, felméretezés) vagy `ocrEngine.Settings.PreprocessImage = true` beállítása. |
| **GPU hiba: „CUDA driver version is insufficient”** | Elavult driver | Frissítsd a GPU drivert, vagy állítsd `UseGpu = false`-ra a CPU kényszerítéséhez. |
| **Kivétel: „File not found”** | Hibás útvonal-elválasztó Linux/macOS rendszeren | Használd a `Path.Combine`‑t vagy a perjel (`/`) karaktert. |

## 7. lépés – Méretezés (több fájl esetén)

Amikor néhány TIFF‑ról több ezerre váltasz, fontold meg a következőket:

* **Párhuzamos feldolgozás:** A `foreach`-t `Parallel.ForEach`‑be helyezd (győződj meg róla, hogy a motor példány szálbiztos; egyébként hozz létre egyet szálanként).
* **Darabolt I/O:** Olvasd a képeket kötegekben, hogy elkerüld a RAM kimerülését.
* **Naplózás:** Írd a folyamatot egy naplófájlba; segít a visszaállításban egy összeomlás után.

```csharp
Parallel.ForEach(imageFiles, filePath =>
{
    // Same OCR logic as before, but each thread gets its own engine.
    var engine = new OcrEngine { Settings = { UseGpu = true } };
    // ... rest of the code
});
```

> **Ne feledd:** A GPU memória megosztott, így túl sok párhuzamos GPU feladat indítása valójában lelassíthat. Először néhány szállal tesztelj.

## Teljes működő példa (másolás-beillesztés kész)

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;
using System.IO;

class GpuBatchDemo
{
    static void Main()
    {
        // Step 1 – Create OCR engine (CPU or GPU)
        var ocrEngine = new OcrEngine();
        ocrEngine.Settings.UseGpu = true; // Try GPU, fallback to CPU automatically

        // Step 2 – List of TIFF files to process
        var imageFiles = new List<string>
        {
            @"C:\OCR\Input\doc1.tif",
            @"C:\OCR\Input\doc2.tif",
            @"C:\OCR\Input\doc3.tif"
        };

        // Step 3 – Process each file
        foreach (var filePath in imageFiles)
        {
            var ocrImage = OcrImage.FromFile(filePath);
            var ocrResult = ocrEngine.Recognize(ocrImage);

            // Show a short preview
            Console.WriteLine($"{filePath}: {ocrResult.Text.Substring(0, Math.Min(50, ocrResult.Text.Length))}...");

            // Optional: Save full text to a .txt file
            var outputPath = Path.ChangeExtension(filePath, ".txt");
            File.WriteAllText(outputPath, ocrResult.Text);
        }
    }
}
```

A program futtatása **képekből szöveget fog felismerni**, **TIFF‑ből szöveget nyer ki**, és hatékonyan bemutatja, **hogyan végezzünk kötegelt OCR-t**.

## Következtetés

Most már egy szilárd, vég‑től‑végig példát rendelkezel arra, **hogyan végezzünk kötegelt OCR-t** C#‑ban az Aspose OCR motorjával. Az útmutató mindent lefedett a projekt beállításától, a GPU gyorsítás átkapcsolásán, a fájllista összeállításán, a képek feldolgozásán, egészen az eredmények mentéséig. Akár TIFF‑ből, akár bármely más képformátumból nyersz szöveget, ugyanaz a minta alkalmazható – csak cseréld ki a fájlkiterjesztéseket.

Készen állsz a következő lépésre? Próbáld meg integrálni az OCR kimenetet egy keresőindexbe, betáplálni a szöveget egy nagy nyelvi modellbe, vagy kísérletezz a párhuzamos feldolgozással, hogy perceket takaríts meg hatalmas kötegek esetén. A határ a csillagos ég, és már megvan az alap, amire építhetsz.

Van kérdésed vagy szeretnéd megosztani a saját kötegelt OCR trükkjeidet? Hagyj egy megjegyzést alább – jó kódolást!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}