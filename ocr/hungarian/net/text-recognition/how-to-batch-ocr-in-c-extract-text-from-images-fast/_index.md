---
category: general
date: 2026-03-21
description: A kötegelt OCR C#-ban egyszerűen – tanulja meg, hogyan nyerjen ki szöveget
  képekből, konvertálja a képeket szöveggé, és mentse az OCR-t szövegként nyelvi beállításokkal.
draft: false
keywords:
- how to batch OCR
- extract text from images
- convert images to text
- save OCR as text
- set OCR language
language: hu
og_description: A C#-ban történő kötegelt OCR lehetővé teszi, hogy szöveget nyerjünk
  ki képekből, képeket szöveggé konvertáljunk, és az OCR-t szövegként mentsük, miközben
  könnyen beállítható az OCR nyelve.
og_title: Hogyan végezzünk kötegelt OCR-t C#-ban – Gyors útmutató
tags:
- OCR
- C#
- Aspose
title: Hogyan végezzünk kötegelt OCR-t C#-ban – Gyors szövegkivonás képekből
url: /hu/net/text-recognition/how-to-batch-ocr-in-c-extract-text-from-images-fast/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan végezzünk kötegelt OCR-t C#‑ban – Szöveg gyors kinyerése képekből

Gondoltad már valaha, **hogyan végezzünk kötegelt OCR-t**, amikor egy mappában több száz kép van? Nem vagy egyedül – a fejlesztők állandóan azt kérdezik, hogyan lehet szöveget kinyerni a képekből anélkül, hogy minden fájlhoz ciklust írnának. A jó hír, hogy az Aspose.OCR egy tiszta, párhuzamosan használható módot biztosít a **képek szöveggé konvertálására** néhány C# sorban.  

Ebben az útmutatóban végigvezetünk egy teljes, azonnal futtatható példán, amely megmutatja, hogyan **mentheted el az OCR-t szövegként**, válaszd ki a megfelelő nyelvet, és növeld a párhuzamos feldolgozást a sebesség érdekében. A végére egy önálló megoldást kapsz, amelyet bármely .NET projektbe beilleszthetsz.

## Amire szükséged lesz

- .NET 6 vagy újabb (az API működik .NET Core és .NET Framework alatt)
- Aspose.OCR for .NET (NuGet csomag `Aspose.OCR`)
- Egy mappa a feldolgozni kívánt képekkel (PNG, JPEG, TIFF, stb.)
- Egy kis kíváncsiság a párhuzamos programozás iránt (opcionális, de hasznos)

Nincs szükség extra szolgáltatásokra, felhőkulcsokra – csak tiszta C# kód, amely helyben fut.

---

![kötegelt OCR munkafolyamat](placeholder.png){alt="kötegelt OCR munkafolyamat diagram"}

## 1. lépés: A projekt beállítása és az Aspose.OCR telepítése

Először is, hozz létre egy konzolos alkalmazást (vagy használd egy meglévőt), és add hozzá az Aspose.OCR csomagot:

```bash
dotnet new console -n BatchOcrDemo
cd BatchOcrDemo
dotnet add package Aspose.OCR
```

> **Pro tipp:** Ha Visual Studio‑t használsz, jobb‑kattints a projektre → *Manage NuGet Packages* → keresd meg a *Aspose.OCR*‑t, és telepítsd a legújabb stabil verziót.

Ez hozzáférést biztosít a `OcrBatchProcessor`, `OcrEngineSettings` és a `Language` enumhoz.

## 2. lépés: Bemeneti és kimeneti mappák meghatározása

A kötegelt feldolgozónak tudnia kell, hol vannak a forrásképek, és hová kell írni a kinyert szövegfájlokat. Tartsd az útvonalakat abszolút vagy a projekt gyökeréhez relatív módon – csak győződj meg róla, hogy a mappák léteznek a kód futtatása előtt.

```csharp
var inputPath  = @"C:\MyImages\BatchInput";
var outputPath = @"C:\MyImages\BatchResults";

// Ensure the output directory exists
if (!Directory.Exists(outputPath))
    Directory.CreateDirectory(outputPath);
```

> **Miért fontos:** Ha a kimeneti mappa hiányzik, a feldolgozó kivételt dob, és megszakítja a teljes köteget. A mappa előzetes létrehozása biztosítja a zökkenőmentes futást.

## 3. lépés: Az OCR beállításainak konfigurálása (beleértve a nyelvet)

Itt **állíthatod be az OCR nyelvet** az egész köteghez. Az Aspose.OCR tucatnyi nyelvet támogat; az angol az alapértelmezett, de a `Language` enum értékének módosításával átválthatsz francia, spanyol stb. nyelvre.

```csharp
var ocrSettings = new OcrEngineSettings
{
    Language = Language.English   // Change to Language.French, Language.Spanish, etc.
};
```

Ha valaha különböző nyelveket kell feldolgoznod képenként, később felülírhatod ezt a beállítást fájlonként – erről később lesz szó.

## 4. lépés: Az `OcrBatchProcessor` objektum felépítése

Most összekapcsoljuk a dolgokat. Az `OcrBatchProcessor` lehetővé teszi a bemeneti mappa, kimeneti mappa, kimeneti formátum, párhuzamos opciók és a most létrehozott közös beállítások megadását.

```csharp
using Aspose.OCR.Batch;
using Aspose.OCR.Settings;
using System.Threading.Tasks;

var batch = new OcrBatchProcessor
{
    InputFolder   = inputPath,
    OutputFolder  = outputPath,
    OutputFormat  = OcrOutputFormat.PlainText, // **save OCR as text** in .txt files
    ParallelOptions = new ParallelOptions { MaxDegreeOfParallelism = 4 }, // up to 4 threads
    Settings = ocrSettings
};
```

> **Miért a párhuzamosság?** Ha tucatnyi vagy több száz kép van, azok egyesével történő feldolgozása fájdalmasan lassú lehet. A `MaxDegreeOfParallelism` 4‑re állítása lehetővé teszi, hogy a futtatókörnyezet egyszerre négy CPU magot használjon, drámaian lerövidítve az összidőt egy tipikus munkaállomáson.

## 5. lépés: A kötegelt művelet futtatása

A feldolgozó beállítása után a végrehajtás egyetlen metódushívás. A könyvtár automatikusan kezeli a fájlok felsorolását, az OCR‑t és az eredmények írását.

```csharp
batch.Execute();
Console.WriteLine("Batch OCR completed.");
```

Amikor a konzol kiírja a *„Batch OCR completed.”* üzenetet, a `BatchResults` mappában minden eredeti kép mellett megtalálod a `.txt` fájlt. Minden szövegfájl a forrásképből kinyert nyers karaktereket tartalmazza – pontosan azt, amire a **szöveg képekből történő kinyeréséhez** szükséged van a további feldolgozáshoz.

### Várható kimenet

```
C:\MyImages\BatchResults\image1.txt
C:\MyImages\BatchResults\image2.txt
...
```

Nyisd meg bármelyik fájlt, és láthatod a kép tartalmának egyszerű szöveges ábrázolását.

## 6. lépés: Az eredmények ellenőrzése (opcionális)

Jó szokás néhány fájlt kétszer ellenőrizni, hogy az OCR a várt módon működött-e. Egy gyors módszer, ha beolvasod minden generált fájl első sorát, és kiírod a konzolra:

```csharp
foreach (var txtFile in Directory.GetFiles(outputPath, "*.txt"))
{
    var firstLine = File.ReadLines(txtFile).FirstOrDefault();
    Console.WriteLine($"{Path.GetFileName(txtFile)} → {firstLine}");
}
```

Ha torz karaktereket látsz, fontold meg a `Language` beállítás módosítását vagy a képminőség finomhangolását (pl. DPI növelése, szürkeárnyalatos konvertálás).

## Haladó variációk és szélhelyzetek

### 1. Fájlonkénti nyelv felülírások
Néha egy köteg többnyelvű dokumentumokat tartalmaz. Megvizsgálhatod minden kép nevét, és futás közben hozzárendelhetsz egy nyelvet:

```csharp
batch.Settings = new OcrEngineSettings(); // default settings

batch.FileProcessing += (sender, args) =>
{
    if (args.FileName.Contains("_fr"))
        args.Settings.Language = Language.French;
    else if (args.FileName.Contains("_es"))
        args.Settings.Language = Language.Spanish;
    // otherwise keep the default (English)
};
```

### 2. Különböző kimeneti formátumok
Ha kereshető PDF‑eket szeretnél egyszerű szöveg helyett, módosítsd a `OutputFormat` értékét:

```csharp
batch.OutputFormat = OcrOutputFormat.SearchablePdf;
```

Ez **a képeket szöveggé konvertálja** egy PDF konténerben, megőrizve az eredeti elrendezést.

### 3. Nagy képek kezelése
A nagyon nagy felbontású képek memóriát emészthetnek fel. A folyamat könnyűsúlyúvá tételéhez engedélyezd a kép lecsökkentését:

```csharp
batch.Settings.Dpi = 300; // lowers internal processing DPI
```

### 4. Hibakeresés naplózása
A feldolgozó kivételeket dob olvashatatlan fájlok esetén. Tedd az `Execute`‑t try/catch blokkba, és naplózd a problémás fájlneveket:

```csharp
try
{
    batch.Execute();
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Failed on {ex.Data["FileName"]}: {ex.Message}");
}
```

## Teljes működő példa

Mindent összevonva, itt a teljes, másolás‑beillesztés‑kész program:

```csharp
using Aspose.OCR.Batch;
using Aspose.OCR.Settings;
using System;
using System.IO;
using System.Linq;
using System.Threading.Tasks;

class Program
{
    static void Main()
    {
        // 1️⃣ Input & output locations
        var inputFolder  = @"C:\MyImages\BatchInput";
        var outputFolder = @"C:\MyImages\BatchResults";

        if (!Directory.Exists(outputFolder))
            Directory.CreateDirectory(outputFolder);

        // 2️⃣ OCR settings – set OCR language
        var ocrSettings = new OcrEngineSettings
        {
            Language = Language.English // change as needed
        };

        // 3️⃣ Configure the batch processor
        var batch = new OcrBatchProcessor
        {
            InputFolder    = inputFolder,
            OutputFolder   = outputFolder,
            OutputFormat   = OcrOutputFormat.PlainText, // **save OCR as text**
            ParallelOptions = new ParallelOptions { MaxDegreeOfParallelism = 4 },
            Settings       = ocrSettings
        };

        // 4️⃣ Run the batch job
        batch.Execute();

        // 5️⃣ Confirmation message
        Console.WriteLine("Batch OCR completed.");

        // 6️⃣ (Optional) Quick verification of a few results
        foreach (var txtFile in Directory.GetFiles(outputFolder, "*.txt").Take(5))
        {
            var firstLine = File.ReadLines(txtFile).FirstOrDefault();
            Console.WriteLine($"{Path.GetFileName(txtFile)} → {firstLine}");
        }
    }
}
```

Mentsd el `Program.cs`‑ként, építsd fel a projektet, és futtasd a `dotnet run` parancsot. A konzol kimenetben láthatod a befejezés megerősítését, majd egy rövid előzetes a kinyert szövegről.

---

## Összegzés

Most bemutattuk, **hogyan végezzünk kötegelt OCR-t** C#‑ban az Aspose.OCR segítségével, megmutatva, hogyan **nyerhetünk ki szöveget a képekből**, **konvertálhatjuk a képeket szöveggé**, és **menthetjük az OCR‑t szövegként**, miközben **beállítjuk az OCR nyelvet**, hogy megfeleljen a tartalmadnak. A példa teljesen működőképes, tartalmaz párhuzamos feldolgozást a sebességért, és lehetőséget ad haladó forgatókönyvekre, mint a fájlonkénti nyelv felülírás vagy PDF kimenet.

Készen állsz a következő lépésre? Próbáld megcserélni az `OcrOutputFormat.PlainText`‑et `SearchablePdf`‑re, és lásd, milyen egyszerű kereshető PDF‑eket generálni. Vagy kísérletezz különböző `MaxDegreeOfParallelism` értékekkel, hogy minden egyes milliszekundumot kihozz egy többmagos gépről.

Ha problémákba ütközöl, ellenőrizd újra a mappák útvonalait, győződj meg róla, hogy a képek olvashatóak, és ellenőrizd, hogy a nyelv enum egyezik-e a képeken lévő szöveggel. Boldog kódolást, és legyen az OCR köteged gyors és pontos!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}