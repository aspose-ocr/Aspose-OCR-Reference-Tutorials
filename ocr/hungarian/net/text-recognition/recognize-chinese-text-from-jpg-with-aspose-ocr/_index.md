---
category: general
date: 2026-04-08
description: Tanulja meg, hogyan ismerje fel a kínai szöveget JPG képekből az Aspose
  OCR használatával. Ez a lépésről‑lépésre útmutató azt is megmutatja, hogyan lehet
  gyorsan szöveget kinyerni a képből.
draft: false
keywords:
- recognize chinese text
- extract text from image
- recognize text from jpg
- Aspose OCR C#
- offline OCR resources
language: hu
og_description: Ismerje fel a kínai szöveget JPG képeken az Aspose OCR segítségével.
  Kövesse ezt a teljes útmutatót a szöveg offline kinyeréséhez a képből.
og_title: Kínai szöveg felismerése JPG-ből az Aspose OCR-rel
tags:
- OCR
- C#
- Aspose
title: Kínai szöveg felismerése JPG-ből az Aspose OCR-rel
url: /hu/net/text-recognition/recognize-chinese-text-from-jpg-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kínai szöveg felismerése JPG-ből az Aspose OCR-rel

Szükséged volt már **kínai szöveg felismerésére** egy JPG fájlból, de nem tudtad, hol kezdjed? Nem vagy egyedül — számos fejlesztő ütközik ebbe a problémába többnyelvű szkennelő alkalmazások építésekor. A jó hír, hogy az Aspose OCR-val ez gyerekjáték, még akkor is, ha offline kell dolgoznod.

Ebben a bemutatóban végigvezetünk a teljes folyamaton, a **szöveg kinyerése képből** stílusban, és megmutatjuk, hogyan **szöveg felismerése jpg-ből** C#‑ban. A végére egy futtatható programod lesz, amely egy kínai nyelvű képet beolvas, és a felismert karaktereket a konzolra írja.

## Amit szükséged lesz

- .NET 6.0 vagy újabb (bármely friss verzió megfelelő)
- Az Aspose.OCR NuGet csomag (`Install-Package Aspose.OCR`)
- Egy kínai nyelvi erőforrásfájl (a bemutató megmutatja, hogyan töltsd be offline)
- Egy `chinese_sample.jpg` nevű képfájl, amelyet egy általad irányított mappába helyezel

Nem szükséges semmilyen különleges IDE‑trükk — Visual Studio, Rider vagy akár VS Code is megfelelő.

## 1. lépés: Projekt létrehozása és az Aspose OCR telepítése

Először hozz létre egy új konzolos projektet, és húzd be az Aspose OCR könyvtárat.

```bash
dotnet new console -n ChineseOcrDemo
cd ChineseOcrDemo
dotnet add package Aspose.OCR
```

> **Pro tip:** Ha vállalati proxy mögött vagy, add hozzá a `--no-cache` kapcsolót a friss letöltés kényszerítéséhez.

## 2. lépés: Az automatikus erőforrásletöltés letiltása

Az Aspose OCR képes a nyelvi csomagokat futás közben letölteni, de a termékben általában azt szeretnéd, hogy a fájlok az alkalmazásoddal együtt kerüljenek szállításra. Az automatikus letöltés letiltása megakadályozza a váratlan hálózati hívásokat.

```csharp
using Aspose.Ocr;

// Create the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Turn off the auto‑download feature
ocrEngine.Options.EnableAutomaticResourceDownload = false;
```

Miért csináljuk ezt? Az erőforrások helyi tárolása garantálja a konzisztens teljesítményt, és lehetővé teszi az alkalmazás futtatását internetkapcsolat nélküli gépeken is.

## 3. lépés: Kínai nyelvi erőforrások betöltése offline

Az Aspose a nyelvi adatokat külön fájlokban szállítja. Feltételezve, hogy a kínai csomagot (`zh`) egy `Resources` mappába helyezted a futtatható fájlod mellé, töltsd be így:

```csharp
// Path to the folder that contains the language files
string resourcePath = Path.Combine(AppContext.BaseDirectory, "Resources");

// Tell the engine where to look for resources
ocrEngine.Options.ResourcesFolder = resourcePath;

// Load the Simplified Chinese resources (offline = true)
ocrEngine.LoadLanguageResources("zh", offline: true);
```

> **Figyelem:** Ha az útvonal hibás, `FileNotFoundException`‑t kapsz. Ellenőrizd a mappanevet és a Linuxon a kis‑nagybetű érzékenységet.

## 4. lépés: Az motor nyelvének beállítása kínaira

Miután az adat betöltődött, állítsd be a motor megfelelő nyelvkódját.

```csharp
ocrEngine.Language = "zh"; // “zh” = Simplified Chinese
```

A nyelv explicit megadása javítja a pontosságot, mivel az OCR nem pazarolja az erőforrásokat a szkriptek kitalálására.

## 5. lépés: Szöveg felismerése JPG képből

Itt a bemutató központi része — a JPG átadása a motornak és a szöveg kinyerése.

```csharp
// Full path to the image you want to process
string imagePath = Path.Combine(AppContext.BaseDirectory, "chinese_sample.jpg");

// Run the OCR operation
OcrResult ocrResult = ocrEngine.RecognizeImage(imagePath);

// Output the raw result
Console.WriteLine("=== Recognized Chinese Text ===");
Console.WriteLine(ocrResult.Text);
```

Ha minden rendben ment, a konzol megjeleníti a `chinese_sample.jpg`‑ben lévő kínai karaktereket. A `ocrResult.Confidence` segítségével a minőségi mutatót is lekérdezheted.

## 6. lépés: Teljes működő példa

Az összes részegység egyesítése egy kész, futtatható programot eredményez. Mentsd el `Program.cs`‑ként a projekt mappájába.

```csharp
using System;
using System.IO;
using Aspose.Ocr;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Initialize OCR engine
        // -------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine();

        // -------------------------------------------------
        // 2️⃣ Disable automatic resource download
        // -------------------------------------------------
        ocrEngine.Options.EnableAutomaticResourceDownload = false;

        // -------------------------------------------------
        // 3️⃣ Load Chinese language resources (offline)
        // -------------------------------------------------
        string resourcePath = Path.Combine(AppContext.BaseDirectory, "Resources");
        ocrEngine.Options.ResourcesFolder = resourcePath;
        ocrEngine.LoadLanguageResources("zh", offline: true);

        // -------------------------------------------------
        // 4️⃣ Set language to Simplified Chinese
        // -------------------------------------------------
        ocrEngine.Language = "zh";

        // -------------------------------------------------
        // 5️⃣ Recognize text from a JPG image
        // -------------------------------------------------
        string imagePath = Path.Combine(AppContext.BaseDirectory, "chinese_sample.jpg");
        OcrResult ocrResult = ocrEngine.RecognizeImage(imagePath);

        // -------------------------------------------------
        // 6️⃣ Show the result
        // -------------------------------------------------
        Console.WriteLine("=== Recognized Chinese Text ===");
        Console.WriteLine(ocrResult.Text);
        Console.WriteLine($"\nConfidence: {ocrResult.Confidence:P2}");
    }
}
```

### Várható kimenet

```
=== Recognized Chinese Text ===
欢迎使用Aspose OCR示例
Confidence: 96.45%
```

A pontos kimenet a forrásképtől függ, de egy kínai karakterekből álló blokkot és egy megbízhatósági százalékot kell látnod.

## 7. lépés: Gyakori variációk és szélhelyzetek

### Szöveg felismerése PNG‑ből vagy BMP‑ből

A `RecognizeImage` metódus bármely, a .NET `System.Drawing`‑ja által támogatott formátumot elfogad. Csak cseréld le a fájlkiterjesztést:

```csharp
ocrEngine.RecognizeImage("sample.png");
```

### Több nyelv kezelése

Ha **szöveg kinyerése képből** olyan képet kell feldolgoznod, amely angolt és kínait is tartalmaz, töltsd be mindkét nyelvi csomagot, és állítsd be `ocrEngine.Language = "zh,en";`. A motor automatikusan vált a szkriptek között.

### Alacsony felbontású képek kezelése

Az alacsony DPI rontja az OCR pontosságát. A `RecognizeImage` meghívása előtt érdemes lehet felskálázni a képet:

```csharp
using System.Drawing;

Bitmap bmp = new Bitmap(imagePath);
Bitmap highRes = new Bitmap(bmp, new Size(bmp.Width * 2, bmp.Height * 2));
highRes.Save("highres.jpg");
ocrResult = ocrEngine.RecognizeImage("highres.jpg");
```

Ne feledd, a felskálázás nem varázsolja hozzá a hiányzó részleteket, de több pixelt ad az algoritmusnak a feldolgozáshoz.

## 8. lépés: Tesztelés és ellenőrzés

Egy gyors sanity‑check, hogy összehasonlítsd az OCR kimenetet egy ismert referencia‑szöveggel.

```csharp
string expected = "欢迎使用Aspose OCR示例";
bool matches = ocrResult.Text.Trim() == expected;
Console.WriteLine($"Match with expected? {matches}");
```

Ha a `matches` értéke `false`, próbáld meg módosítani a képet (pl. növeld a kontrasztot), vagy engedélyezd a `ocrEngine.Options.UseAdvancedPreprocessing = true` beállítást.

## Összegzés

Most már tudod, hogyan **kínai szöveg felismerése** egy JPG fájlból az Aspose OCR segítségével, és hogyan **szöveg kinyerése képből** egy teljesen offline környezetben. A teljes megoldás — inicializálás, erőforrásbetöltés, nyelvválasztás és képfeldolgozás — egyetlen, könnyen futtatható konzolos alkalmazásba illeszkedik.

Mi a következő lépés? Próbálj meg egy képköteget feldolgozni ugyanazzal a motorral, kísérletezz különböző nyelvi csomagokkal, vagy integráld az OCR‑lépést egy ASP .NET Web API‑ba, hogy a felhasználók feltölthessék a képeket, és helyben megkapják a lefordított szöveget. A határ csak a képzeleted, ha megbízható OCR‑t kombinálsz a modern .NET eszközökkel.

Boldog kódolást, és nyugodtan írj kommentet, ha elakadsz!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}