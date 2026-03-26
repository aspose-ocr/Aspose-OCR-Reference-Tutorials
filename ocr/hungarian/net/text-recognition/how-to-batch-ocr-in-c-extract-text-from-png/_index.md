---
category: general
date: 2026-03-26
description: A C#‑ban történő kötegelt OCR használata megkönnyíti a szöveg kinyerését
  PNG fájlokból. Kövesse ezt a lépésről‑lépésre útmutatót a C# OCR‑hoz a kötegelt
  szövegkivonáshoz az Aspose OCR segítségével.
draft: false
keywords:
- how to batch OCR
- extract text from png
- c# ocr tutorial
- how to create OCR
- batch text extraction
language: hu
og_description: A C#-ban történő kötegelt OCR lehetővé teszi, hogy gyorsan szöveget
  nyerjünk ki PNG fájlokból. Ez az útmutató végigvezet egy teljes C# OCR tutorialon
  a kötegelt szövegkinyeréshez.
og_title: Hogyan végezzünk kötegelt OCR-t C#-ban – Szöveg kinyerése PNG-ből
tags:
- OCR
- C#
- Aspose
title: Hogyan végezzünk kötegelt OCR-t C#‑ban – Szöveg kinyerése PNG‑ből
url: /hu/net/text-recognition/how-to-batch-ocr-in-c-extract-text-from-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan végezzünk kötegelt OCR-t C#-ban – Szöveg kinyerése PNG-ből

Gondolkodtál már azon, **hogyan végezzünk kötegelt OCR-t** egy halom képernyőképen anélkül, hogy minden egyes fájlhoz külön programot írnál? Nem vagy egyedül. Sok projektben tucatnyi PNG-vel dolgozunk, amelyeknek a szövegét ki kell nyerni, és egyesével végrehajtani ez fájdalmas.

A jó hír? Az Aspose OCR-rel elindíthatsz egy apró C# konzolos alkalmazást, amely párhuzamosan feldolgozza az összes képet, gyors **kötegelt szövegkivonást** és tiszta eredményhalmazt biztosítva. Ebben az útmutatóban végigvezetünk egy teljes **c# ocr tutorial**-on, elmagyarázzuk, miért fontos minden rész, és megmutatjuk, hogyan néz ki pontosan a kimenet.

Az cikk végére képes leszel:

* Egy lépésben betölteni egy PNG-fájlok (vagy bármely támogatott kép) listáját.  
* Konfigurálni egy megosztott `OcrEngine`-t, hogy a beállítások konzisztensen maradjanak a kötegben.  
* A felismerési sor futtatása legfeljebb négy párhuzamos munkavállalóval.  
* Az egyes oldalak felismert szövegének lekérése és a konzolra írása.

Nincs varázslat, csak megbízható kód, amelyet ma beilleszthetsz a megoldásodba.

## Amire szükséged lesz

Miután elkezdünk, győződj meg róla, hogy rendelkezel:

* .NET 6 SDK-val (vagy bármely friss .NET verzióval).  
* Érvényes Aspose OCR licenccel vagy ideiglenes értékelő kulccsal.  
* Egy mappával, amely tartalmazza a feldolgozni kívánt PNG-fájlokat.  
* Visual Studio 2022-vel vagy a kedvenc szerkesztőddel.

Ennyi—nem szükséges extra NuGet csomag a `Aspose.OCR` és a szabványos `System.Collections.Generic` mellett.

## Kötegelt OCR beállítása – A projekt létrehozása

Először is, hozz létre egy új konzolos projektet, és húzd be az Aspose OCR könyvtárat.

```bash
dotnet new console -n BatchOcrDemo
cd BatchOcrDemo
dotnet add package Aspose.OCR
```

A visszaállítás befejezése után nyisd meg a **Program.cs**-t (vagy hozz létre egy új fájlt), és add hozzá a szokásos `using` direktívákat:

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
```

Ez az egyszerű váz biztosítja a hozzáférést a `OcrEngine`, `RecognitionQueue` és a később szükséges segédosztályokhoz.

## Szöveg kinyerése PNG-ből – Képlista előkészítése

Most meg kell mondanunk a programnak, **mely PNG-ket** kell OCR-en átfuttatni. A legegyszerűbb mód egy `List<string>` létrehozása, amely abszolút vagy relatív útvonalakat tartalmaz.

```csharp
// Step 1: Define the image files to be processed
var imagePaths = new List<string>
{
    @"YOUR_DIRECTORY/page1.png",
    @"YOUR_DIRECTORY/page2.png",
    @"YOUR_DIRECTORY/page3.png",
    @"YOUR_DIRECTORY/page4.png"
};
```

Cseréld le a `YOUR_DIRECTORY`-t a tényleges mappaútvonalra. Ha dinamikus halmazod van, használhatod a `Directory.GetFiles(@"YOUR_DIRECTORY", "*.png")`-t is, és az eredményt betáplálhatod a listába. A lényeg, hogy a **szöveg kinyerése PNG-ből** csupán a megfelelő fájlnevek sorba állítását jelenti.

![Hogyan végezzünk kötegelt OCR munkafolyamat](https://example.com/placeholder.png "Diagram, amely bemutatja, hogyan végezzünk kötegelt OCR-t PNG-fájlok gyűjteményén")

*Kép alternatív szöveg: hogyan végezzünk kötegelt OCR munkafolyamat diagram*

## C# OCR tutorial – A felismerési sor konfigurálása

A kötegelt művelet szíve a `RecognitionQueue`. Gondolj rá úgy, mint egy szállítószalagra, amely minden képet átad egy megosztott `OcrEngine`-nek. Az motor megosztásával alacsonyan tartjuk a memóriahasználatot, és garantáljuk az azonos beállításokat minden oldalra.

```csharp
// Step 2: Create a recognition queue with shared OCR engine and parallelism
var recognitionQueue = new RecognitionQueue
{
    MaxDegreeOfParallelism = 4,          // run up to 4 images at the same time
    Engine = new OcrEngine()            // shared configuration for all images
};
```

Miért állítjuk a `MaxDegreeOfParallelism`-t 4-re? Egy tipikus négymagos laptopon ez a legjobb áteresztőképességet biztosítja anélkül, hogy az operációs rendszert elnyomná. Ha szerveren több maggal futtatod, növeld a számot ennek megfelelően.

### Pro tipp

Ha egyedi nyelvi csomagokra, DPI-beállításokra vagy érdeklődési terület kivágására van szükséged, **egyszer** hajtsd végre a megosztott `Engine`-en, mielőtt bármilyen képet sorba állítanál. Például:

```csharp
recognitionQueue.Engine.Language = Language.English;
recognitionQueue.Engine.Dpi = 300;
```

Minden későbbi felismerés automatikusan örökli ezeket a beállításokat – ez a **hogyan hozzunk létre OCR** csővezetékek lényege, amelyek konzisztens maradnak.

## Kötegelt szövegkivonás – Képek sorba állítása és a sor futtatása

Miután a sor készen áll, a következő lépés, hogy minden képet feltegyünk rá. Az `Enqueue` metódus egy `OcrImage` példányt fogad, amelyet egy fájlútvonalból hozunk létre.

```csharp
// Step 3: Enqueue each image for OCR processing
foreach (var path in imagePaths)
    recognitionQueue.Enqueue(OcrImage.FromFile(path));
```

Miután minden fájl sorba került, elindítjuk a feldolgozást:

```csharp
// Step 4: Run the queue and collect OCR results
List<OcrResult> ocrResults = recognitionQueue.ExecuteAll();
```

`ExecuteAll` blokkol, amíg minden kép be nem fejeződik, majd egy listát ad vissza, ahol minden elem a bemeneti sorrendnek felel meg. Ez garantálja, hogy az 1. oldal eredménye a 0. indexen, a 2. oldal a 1. indexen stb. van – hasznos, ha vissza kell térképezni az eredményeket a forrásfájlokra.

## Hogyan hozzunk létre OCR – Az eredmények megjelenítése

Végül, nyomtassuk ki a felismert szöveget a konzolra. Itt láthatod valóban a **kötegelt szövegkivonás** működését.

```csharp
// Step 5: Output the recognized text for each page
for (int i = 0; i < ocrResults.Count; i++)
{
    Console.WriteLine($"--- Page {i + 1} ---");
    Console.WriteLine(ocrResults[i].Text);
}
```

Amikor futtatod a programot (`dotnet run`), valami ilyesmit kell látnod:

```
--- Page 1 ---
Welcome to the quarterly report.
--- Page 2 ---
Revenue increased by 12% YoY.
--- Page 3 ---
All figures are provisional.
--- Page 4 ---
Contact finance@example.com for details.
```

Ha bármely kép hibát jelez (pl. sérült fájl), a megfelelő `OcrResult` üres `Text` tulajdonsággal rendelkezik, és a diagnosztikához megtekintheted a `ocrResults[i].Exception`-t.

## Hogyan hozzunk létre OCR – Tippek, szélsőséges esetek és legjobb gyakorlatok

### Nagy kötegek kezelése

Százak PNG-fájljának feldolgozása még mindig sok memóriát fogyaszthat, ha minden `OcrResult` objektumot életben tartasz. Ilyen esetben írd ki a kimenetet fájlba vagy adatbázisba, amint minden eredmény megérkezik:

```csharp
recognitionQueue.OnResultReady += (sender, args) =>
{
    File.AppendAllText("OcrOutput.txt",
        $"--- {args.Image.Path} ---{Environment.NewLine}{args.Result.Text}{Environment.NewLine}");
};
```

### Nem‑PNG formátumok kezelése

Az Aspose OCR natívan támogatja a JPEG, BMP és TIFF formátumokat is. Csak módosítsd a fájlkiterjesztést a listádban, vagy használj helyettesítő karakteres keresést. Ugyanazok a **c# ocr tutorial** lépések érvényesek – nincs szükség kódváltoztatásra.

### Üres oldalak kihagyása

Ha beolvasott PDF-eket használsz, amelyek néha üres oldalakat tartalmaznak, szűrheted az eredményeket:

```csharp
if (!string.IsNullOrWhiteSpace(result.Text))
    // process non‑empty text
```

### Licencelési szempontok

Az értékelő verzió minden oldalra vízjelet helyez. Éles környezetben győződj meg róla, hogy a `Main` elején beágyazod a licencfájlt:

```csharp
License lic = new License();
lic.SetLicense("Aspose.OCR.lic");
```

### Párhuzamosság finomhangolása

`MaxDegreeOfParallelism` alapértelmezett értéke `Environment.ProcessorCount`. Ha magas CPU-használatot vagy memória nyomást észlelsz, csökkentsd az értéket. Ellenkező esetben, egy sokmagos felhő VM-en növeld, hogy teljes mértékben kihasználd a hardvert.

## Összegzés

Most már van egy teljes **hogyan végezzünk kötegelt OCR** megoldás C#-ban, amely **szöveget nyer ki PNG** fájlokból, párhuzamosan futtatja őket, és tiszta, rendezett eredményeket ad. Egyetlen `OcrEngine` megosztásával megtanultad, hogyan hozz létre **hogyan hozzunk létre OCR** csővezetékeket, amelyek memóriahatékonyak és könnyen karbantarthatók. Ez a **c# ocr tutorial** azt is megmutatja, hogyan skálázhatsz **kötegelt szövegkivonás**-ra több száz kép esetén néhány extra sorral.

---

### Mi a következő?

* Próbáld meg hozzáadni a nyelvfelismerést (`Engine.Language = Language.AutoDetect`).  
* Kísérletezz a kimeneti formátumokkal – írd az eredményeket JSON vagy CSV formátumba a további elemzésekhez.  
* Kombináld ezt a kötegelt OCR-t egy PDF‑kép konverziós lépéssel, hogy teljes beolvasott dokumentumokat dolgozz fel.

Nyugodtan finomhangold a párhuzamosságot, cseréld ki a saját képforrásaidra, vagy csatlakoztasd az eredményeket egy keresőindexhez. A határ csak a képzeleted, ha elsajátítod a **hogyan végezzünk kötegelt OCR**-t C#-ban.

Boldog kódolást, és legyenek az OCR futásaid gyorsak és hibamentesek!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}