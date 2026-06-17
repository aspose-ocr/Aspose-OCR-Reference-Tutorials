---
category: general
date: 2026-03-13
description: Hogyan végezzünk gyorsan és megbízhatóan kötegelt OCR-t, miközben megtanuljuk,
  hogyan lehet szöveget kinyerni TIFF-fájlokból az Aspose.OCR használatával. Kövesse
  ezt a lépésről‑lépésre útmutatót.
draft: false
keywords:
- how to batch OCR
- extract text from tiff
- Aspose OCR batch processing
- C# OCR automation
- GPU accelerated OCR
language: hu
og_description: Ismerje meg, hogyan végezhet kötegelt OCR-t C#-ban, és hogyan nyerhet
  ki szöveget TIFF fájlokból az Aspose.OCR segítségével. Ez az útmutató bemutatja
  a beállítást, a kódot és a legjobb gyakorlatok tippeit.
og_title: Hogyan végezzünk kötegelt OCR-t C#-ban – Teljes programozási útmutató
tags:
- OCR
- C#
- Aspose
- Batch processing
title: Hogyan végezzünk kötegelt OCR-t C#‑ban – Teljes programozási útmutató
url: /hu/net/ocr-optimization/how-to-batch-ocr-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan végezzünk kötegelt OCR-t C#‑ban – Teljes programozási útmutató

Gondolkodtál már azon, **hogyan végezzünk kötegelt OCR‑t** egy hegynyi beolvasott számlán anélkül, hogy minden fájlhoz külön szkriptet írnál? Nem vagy egyedül. Sok valós projektben a fájdalom forrása nem maga az OCR pontossága, hanem a képek hatalmas mennyisége – gyakran TIFF‑ek –, amelyeket kereshető szöveggé kell alakítani.  

Ez a bemutató megmutatja, **hogyan végezzünk kötegelt OCR‑t** az Aspose.OCR `BatchProcessor` segítségével, miközben megtanít arra, hogyan **olvassunk ki szöveget tiff** fájlokból egyetlen, tiszta futás során. A végére egy azonnal futtatható konzolos alkalmazást kapsz, amely egy teljes mappát dolgoz fel, opcionálisan GPU gyorsítást használ, és a nyers szöveges eredményeket a kívánt helyre helyezi.

## Amire szükséged lesz

- **.NET 6+** (vagy .NET Framework 4.7.2, ha a klasszikus futtatókörnyezetet részesíted előnyben)  
- **Aspose.OCR for .NET** – a NuGet csomagot a `dotnet add package Aspose.OCR` paranccsal szerezheted be.  
- Egy mappa **TIFF** képekkel, amelyeket be szeretnél olvasni (a bemutató `Invoices` mappát használ példaként).  
- Opcionálisan: egy GPU, amely támogatja a DirectX 11‑et vagy a CUDA‑t, ha gyorsítani szeretnéd a feldolgozást.  

Nincs szükség extra szolgáltatásokra, felhőkulcsokra – csak egy helyi C# projektre és az Aspose könyvtárra.

## 1. lépés: A projekt beállítása és az Aspose.OCR telepítése

Először hozz létre egy konzolos alkalmazást.

```bash
dotnet new console -n BatchOcrDemo
cd BatchOcrDemo
dotnet add package Aspose.OCR
```

> **Pro tip:** Ha Windows‑t használsz, és GPU gyorsítást tervezel, győződj meg róla, hogy a legújabb grafikus driver telepítve van. Ellenkező esetben a `UseGpu = true` kapcsoló automatikusan CPU‑ra vált vissza.

## 2. lépés: A BatchProcessor konfigurációjának létrehozása

Most konfiguráljuk a `BatchProcessor`‑t. Ez a **kötegelt OCR** központja – megadod az Aspose‑nak, hogy milyen nyelvet várjon, milyen előfeldolgozó szűrőket alkalmazzon, és hogy használja‑e a GPU‑t.

```csharp
using Aspose.OCR;
using Aspose.OCR.Batch;

namespace BatchOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 2: Configure the batch processor
            // -------------------------------------------------
            BatchProcessor batchProcessor = new BatchProcessor
            {
                // Primary language – English works for most invoices
                Language = Language.English,

                // Set to true if you have a compatible GPU; otherwise false
                UseGpu = true,

                // Optional pre‑processing to improve OCR accuracy
                PreProcessingFilters = new FilterPipeline
                {
                    new DeskewFilter(),   // straightens tilted scans
                    new DespeckleFilter() // removes speckles and noise
                }
            };
```

**Miért ezek a beállítások?**  
- `Language = Language.English` azt mondja a motornak, hogy az angol nyelvi modellt használja, amely sokkal pontosabb, mint az általános modell.  
- `UseGpu` egy jó GPU‑n a feldolgozási időt felére csökkentheti, de biztonságos `false`‑ra állítani, ha laptopodban nincs GPU.  
- A szűrőcsővezeték azt utánozza, amit egy ember tenne: kiegyenesíti az oldalt és eltávolítja a foltokat, mielőtt az OCR motorhoz adná.

## 3. lépés: A feldolgozó mutatása a TIFF mappádra

A **kötegelt OCR** következő lépése, hogy megmondjuk a könyvtárnak, hol találhatók a forrásfájlok. A helyettesítő karakterek támogatottak, így egyetlen lépésben felveheted az összes `.tif` fájlt.

```csharp
            // -------------------------------------------------
            // Step 3: Add the folder containing TIFF images
            // -------------------------------------------------
            // Replace YOUR_DIRECTORY with the actual path on your machine
            batchProcessor.AddFolder(@"C:\Data\Invoices", "*.tif");
```

> **Edge case:** Ha a képeid vegyes kiterjesztésűek (`.tiff`, `.tif`, `.png`), hívd meg többször az `AddFolder`‑t, vagy használd a `*.*`‑t, és később szűrd le a kódban.

## 4. lépés: Az OCR eredmények helyének kiválasztása

Talán azt kérdezed, „Hová kerül a kinyert szöveg?” Ez a **kötegelt OCR** harmadik pillére – a kimeneti hely és formátum meghatározása. A nyers szövegfájlokat az eredeti fájlok mellett tároljuk.

```csharp
            // -------------------------------------------------
            // Step 4: Define output folder and format
            // -------------------------------------------------
            batchProcessor.OutputFolder = @"C:\Data\Output";
            batchProcessor.OutputFormat = OutputFormat.PlainText;
```

Ha a nyers szöveg helyett JSON‑t vagy XML‑t szeretnél, egyszerűen cseréld le a `OutputFormat.PlainText`‑t `OutputFormat.Json`‑ra vagy `OutputFormat.Xml`‑ra. A könyvtár elvégzi a konverziót.

## 5. lépés: A kötegelt feladat futtatása és az eredmények jelentése

Végül indítsd el a feladatot. Az `Execute` metódus blokkol, amíg minden fájl feldolgozásra nem kerül, ezután ellenőrizheted a `ProcessedCount`‑ot a siker megerősítéséhez.

```csharp
            // -------------------------------------------------
            // Step 5: Execute the batch job
            // -------------------------------------------------
            batchProcessor.Execute();

            // Simple verification output
            Console.WriteLine($"\nBatch completed. Processed files: {batchProcessor.ProcessedCount}");
            Console.WriteLine("Check C:\\Data\\Output for .txt files containing extracted text.");
        }
    }
}
```

### Várható kimenet

A program futtatásakor a konzol valami ilyesmit fog kiírni:

```
Batch completed. Processed files: 42
Check C:\Data\Output for .txt files containing extracted text.
```

Az `Output` mappában minden forrás TIFF‑hez találsz egy `.txt` fájlt, amely az eredeti kép nevével van elnevezve (pl. `Invoice_001.txt`). Bármelyik fájlt megnyitva a nyers OCR szöveget látod – tökéletes a keresőindexbe vagy egy későbbi adatkinyerési folyamatba való betápláláshoz.

## Gyakori problémák kezelése

### 1. GPU nem elérhető

Ha `UseGpu = true`, de nem található kompatibilis eszköz, az Aspose csendben CPU‑ra vált vissza. Ha explicit szeretnéd kezelni, elkaphatod a `DeviceNotFoundException`‑t:

```csharp
try
{
    batchProcessor.Execute();
}
catch (DeviceNotFoundException)
{
    Console.WriteLine("GPU not detected – switching to CPU mode.");
    batchProcessor.UseGpu = false;
    batchProcessor.Execute();
}
```

### 2. Nem‑TIFF fájlok ugyanabban a mappában

Ha vegyes mappád van, szűrd programozottan:

```csharp
var tiffFiles = Directory.GetFiles(@"C:\Data\Invoices", "*.*")
                         .Where(f => f.EndsWith(".tif", StringComparison.OrdinalIgnoreCase) ||
                                     f.EndsWith(".tiff", StringComparison.OrdinalIgnoreCase));

foreach (var file in tiffFiles)
    batchProcessor.AddFile(file);
```

### 3. Nagy fájlok, amelyek meghaladják a memóriát

Óriási többoldalas TIFF‑ek esetén engedélyezd a streaming‑et:

```csharp
batchProcessor.EnableMemoryManagement = true; // reduces RAM footprint
```

## Pro tippek a jobb pontosságért, amikor **szöveget olvasol ki tiff** fájlokból

- **A felbontás számít** – Cél a 300 dpi vagy annál nagyobb. Alatta az OCR motor karaktereket hagyhat ki.  
- **Szín vs. Szürkeárnyalat** – A színes beolvasásokat konvertáld szürkeárnyalatba az OCR előtt; a `DeskewFilter` már ezt a háttérben elvégzi, de hozzáadhatod a `ColorDepthReductionFilter`‑t a további sebességért.  
- **Utófeldolgozás** – Miután megvan a nyers szöveg, futtass helyesírás-ellenőrzést vagy regex‑tisztítást a gyakori OCR hibák javításához (pl. „0” vs „O”).

## Teljes működő példa (másolás‑beillesztés kész)

Az alábbiakban a teljes program látható, amelyet lefordíthatsz és futtathatsz. Csak cseréld ki a helyőrző útvonalakat a saját könyvtáraidra.

```csharp
using Aspose.OCR;
using Aspose.OCR.Batch;
using System;
using System.IO;
using System.Linq;

namespace BatchOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Configure the batch processor (how to batch OCR)
            // -------------------------------------------------
            BatchProcessor batchProcessor = new BatchProcessor
            {
                Language = Language.English,
                UseGpu = true, // set false if no GPU
                PreProcessingFilters = new FilterPipeline
                {
                    new DeskewFilter(),
                    new DespeckleFilter()
                },
                EnableMemoryManagement = true // helps with huge TIFFs
            };

            // -------------------------------------------------
            // Add source TIFF files
            // -------------------------------------------------
            string sourceFolder = @"C:\Data\Invoices";
            batchProcessor.AddFolder(sourceFolder, "*.tif");

            // -------------------------------------------------
            // Optional: add only TIFFs if folder contains other images
            // -------------------------------------------------
            var extraTiffs = Directory.GetFiles(sourceFolder, "*.*")
                                      .Where(f => f.EndsWith(".tiff", StringComparison.OrdinalIgnoreCase));
            foreach (var file in extraTiffs)
                batchProcessor.AddFile(file);

            // -------------------------------------------------
            // Define where results go
            // -------------------------------------------------
            batchProcessor.OutputFolder = @"C:\Data\Output";
            batchProcessor.OutputFormat = OutputFormat.PlainText;

            // -------------------------------------------------
            // Execute the batch job
            // -------------------------------------------------
            try
            {
                batchProcessor.Execute();
                Console.WriteLine($"\nBatch completed. Processed files: {batchProcessor.ProcessedCount}");
                Console.WriteLine("Check C:\\Data\\Output for .txt files containing extracted text.");
            }
            catch (DeviceNotFoundException)
            {
                Console.WriteLine("GPU not detected – falling back to CPU.");
                batchProcessor.UseGpu = false;
                batchProcessor.Execute();
                Console.WriteLine($"Batch completed (CPU). Processed files: {batchProcessor.ProcessedCount}");
            }
        }
    }
}
```

Fordítás és futtatás:

```bash
dotnet run
```

Most már egy rendezett `.txt` fájlgyűjteményed van – minden egyes fájl a **szöveg kinyerése tiff** fájlból egy teljesen automatizált kötegelt folyamat eredménye.

## Következtetés

Áttekintettük, **hogyan végezzünk kötegelt OCR‑t** C#‑ban az elejétől a végéig, lefedve mindent, ami a **szöveg kinyeréséhez tiff** fájlokból hatékonyan szükséges. A fő tanulságok:

1. Használd az Aspose.OCR `BatchProcessor`‑t, hogy elkerüld az ismétlődő ciklusok írását.  
2. Alkalmazz előfeldolgozó szűrőket (kiegyenesítés, folteltávolítás) a nagyobb pontosságért.  
3. Engedélyezd a GPU gyorsítást, ha lehetséges, de mindig legyen CPU visszaesés.  
4. Tárold az eredményeket egy előre meghatározott mappaszerkezetben, hogy a későbbi feladatok automatikusan fel tudják őket dolgozni.

Innen tovább felfedezheted:

- A nyers szöveg betáplálása egy **kereső indexbe** (pl. Elasticsearch), hogy a számlák kereshetők legyenek.  
- A kimenet konvertálása **JSON**‑ra, és egy gépi‑tanulási modellnek átadása, amely sorozatokat nyer ki.  
- **Hibakezelés** hozzáadása sérült TIFF‑ek vagy jogosultsági problémák esetén.

Próbáld ki,

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}