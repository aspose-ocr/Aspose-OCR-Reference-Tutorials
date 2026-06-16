---
category: general
date: 2026-03-07
description: Ismerje meg, hogyan olvashat szöveget PNG-ből, és nyerhet ki cirill szöveget
  az Aspose OCR segítségével, konvertálja a képet szöveggé, és töltse le a cirill
  nyelvi csomagot.
draft: false
keywords:
- read text from png
- extract cyrillic text
- convert image to text
- load image for ocr
- download cyrillic language pack
language: hu
og_description: Tanulja meg, hogyan olvashat szöveget PNG-ből, hogyan nyerhet ki cirill
  szöveget, és hogyan konvertálhatja a képet szöveggé az Aspose OCR használatával
  C#-ban.
og_title: szöveg olvasása PNG-ből – cirill szöveg kinyerése az Aspose OCR-rel
tags:
- Aspose OCR
- C#
- Image Processing
title: szöveg olvasása PNG-ből – cirill szöveg kinyerése az Aspose OCR-rel
url: /hu/net/ocr-configuration/read-text-from-png-extract-cyrillic-text-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# szöveg olvasása png‑ből – cirill szöveg kinyerése az Aspose OCR‑rel

Szükséged van **png‑ből szöveg olvasására** és a cirill karakterek kinyerésére? Ebben az útmutatóban megmutatjuk, hogyan olvassunk szöveget png‑ből az Aspose OCR‑rel, hogyan nyerjünk ki cirill szöveget, és hogyan **alakítsuk át a képet szöveggé** néhány C#‑sorral.  

Ha valaha is egy orosz számla képernyőképe előtt ültél, és azon tűnődtél, hogyan lehet a szavakat kereshető karakterláncba átalakítani, jó helyen vagy.  
Azt is bemutatjuk, hogyan **töltsd le automatikusan a cirill nyelvi csomagot**, így nem kell külön fájlokat keresgélned.

## Mit fogsz elérni

* **Tölts be egy képet OCR‑hez** közvetlenül lemezről vagy egy stream‑ből.  
* Állítsd be a motorra a **cirill nyelvet** manuális letöltés nélkül.  
* Futtasd a felismerést és **nyerd ki a cirill szöveget** egy PNG fájlból.  
* Lásd a felismert szöveget a konzolon kiírva – egy tiszta, egyszerű szöveg, amelyet adatbázisokba, keresőindexekbe vagy bármilyen más munkafolyamatba beilleszthetsz.

Nincs külső szolgáltatás, nincs felhőkulcs, csak az Aspose OCR NuGet csomag és néhány C# sor.

## Előfeltételek

* .NET 6.0 vagy újabb (a kód működik .NET Core‑on, .NET Framework‑ön és .NET 5+-ön).  
* Visual Studio 2022 vagy bármely kedvenc szerkesztő.  
* Az Aspose.OCR NuGet csomag (`dotnet add package Aspose.OCR`).  
* Egy PNG kép, amely cirill karaktereket tartalmaz – például a `cyrillic_sample.png` fájl, amely a `YOUR_DIRECTORY` mappában van elhelyezve.

> **Pro tipp:** Ha Visual Studio‑t használsz, jobb‑klikk a projektre → **NuGet csomagok kezelése** → keresd a „Aspose.OCR” kifejezést és telepítsd a legújabb stabil verziót.

## 1. lépés – Aspose OCR telepítése és a motor létrehozása

Először szükségünk van az OCR motor példányra. Az `OcrEngine` osztály minden művelet belépési pontja.

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;

// Create an OCR engine – this object holds all settings and results
var ocrEngine = new OcrEngine();
```

> **Miért fontos:** A motor tartalmazza a nyelvi csomagokat, a kép adatokat és a felismerési beállításokat. Egyszer példányosítva, és több képnél újra felhasználva javíthatja a teljesítményt.

## 2. lépés – **kép betöltése OCR‑hez** és a nyelv beállítása

Most megadjuk a motor számára, melyik képet dolgozza fel, és melyik nyelvet keresse. A `Language.Cyrillic` beállítása automatikusan letölti a szükséges nyelvi csomagot az első futtatáskor.

```csharp
// 1️⃣ Load the PNG that contains Cyrillic text
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/cyrillic_sample.png");

// 2️⃣ Tell Aspose we want to read Cyrillic characters
ocrEngine.Settings.Language = Language.Cyrillic;   // downloads pack if missing
```

> **Külön eset:** Ha a PNG nagy (több mint 5 MB), érdemes előbb átméretezni a felismerés gyorsítása érdekében. Az `Image` tulajdonság `Stream`‑et is elfogad, így betöltheted memóriából, webkéréssel vagy Azure Blob‑ból anélkül, hogy a fájlrendszert érintenéd.

## 3. lépés – **kép átalakítása szöveggé** egyetlen hívással

A felismerés olyan egyszerű, mint a `Recognize()` meghívása. E hívás után a `Text` tulajdonság tartalmazza a kinyert karakterláncot.

```csharp
// Run the OCR engine – this does the heavy lifting
ocrEngine.Recognize();

// Grab the result; it’s plain Unicode text
string extractedText = ocrEngine.Text;
```

> **Mi történik a háttérben?** Az Aspose egy neurális hálózaton alapuló osztályozót futtat, amelyet milliók cirill glifjeire képeztek ki. A könyvtár elrejti ezt a komplexitást, így csak tiszta Unicode‑ot kapsz.

## 4. lépés – Az eredmény kiírása (vagy továbbküldése máshová)

Demó céljából a szöveget a konzolra írjuk ki, de könnyen elmentheted fájlba, adatbázisba, vagy átadhatod egy keresőindexnek.

```csharp
// Show the OCR result in the console
Console.WriteLine("=== Recognized Cyrillic Text ===");
Console.WriteLine(extractedText);
```

**Várt kimenet** (feltételezve, hogy a `cyrillic_sample.png` a „Привет мир” kifejezést tartalmazza):

```
=== Recognized Cyrillic Text ===
Привет мир
```

Ha a kimenet összezavartnak tűnik, ellenőrizd, hogy a kép tiszta-e, és hogy beállítottad-e a `Language.Cyrillic` értéket. A motor alapértelmezés szerint angolt használ, ami a cirill karaktereket ismeretlen szimbólumként kezeli.

## 5. lépés – Teljes, futtatható példa

Összevonva, itt egy önálló program, amelyet beilleszthetsz egy új konzolprojektbe.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Create the OCR engine
        // -------------------------------------------------
        var ocrEngine = new OcrEngine();

        // -------------------------------------------------
        // 2️⃣ Load the PNG and select Cyrillic language
        // -------------------------------------------------
        // Replace the path with the location of your PNG
        ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/cyrillic_sample.png");
        ocrEngine.Settings.Language = Language.Cyrillic; // auto‑downloads pack

        // -------------------------------------------------
        // 3️⃣ Perform recognition
        // -------------------------------------------------
        ocrEngine.Recognize();

        // -------------------------------------------------
        // 4️⃣ Output the extracted text
        // -------------------------------------------------
        Console.WriteLine("=== Recognized Cyrillic Text ===");
        Console.WriteLine(ocrEngine.Text);
    }
}
```

Mentsd a fájlt `Program.cs` néven, futtasd a `dotnet run` parancsot, és a konzolon meg kell jelennie a cirill szövegnek.

## Gyakori kérdések és hibaelhárítás

| Kérdés | Válasz |
|----------|--------|
| **Mi van, ha a nyelvi csomag nem töltődik le?** | Győződj meg róla, hogy a gépnek van internetkapcsolata. A csomag a `%USERPROFILE%\.Aspose\OCR\Languages` mappában van gyorsítótárazva. Ennek a mappának a törlése friss letöltést kényszerít. |
| **Olvashatok más nyelveket is a cirill mellett?** | Természetesen – cseréld le a `Language.Cyrillic`-et `Language.English`, `Language.Arabic` stb. értékre. Ugyanaz az automatikus letöltési logika érvényes. |
| **A PNG-m zajos – az eredmények rosszak. Mit tehetek?** | Előfeldolgozhatod a képet: növeld a kontrasztot, konvertáld szürkeárnyalatosra, vagy alkalmazz medián szűrőt. Az Aspose OCR továbbá `Settings.ImagePreprocess` beállításokat kínál. |
| **Van mód arra, hogy minden szóhoz kapjunk körülhatároló dobozt?** | Igen, a `Recognize()` után ellenőrizheted az `ocrEngine.Regions`-t, amely minden felismert szóhoz egy téglalapot ad vissza. |
| **Szükségem van licencre a termelési környezetben?** | Az ingyenes értékelés legfeljebb 100 oldalra működik. Kereskedelmi projektekhez vásárolj licencet – ez eltávolítja az értékelési vízjelet és feloldja a nagysebességű kötegelt feldolgozást. |

## Következő lépések – a megoldás bővítése

* **Kötegelt feldolgozás:** Egy PNG‑mappán végig iterálva gyűjtsd össze a szövegeket egy CSV fájlba.  
* **Integráció az Azure Cognitive Search‑szel:** Indexeld a kinyert cirill karakterláncokat a gyors kereséshez.  
* **Kombinálás PDF konverzióval:** Használd az Aspose.PDF‑et a beolvasott PDF‑ek PNG‑vé alakításához, majd futtasd ugyanazt az OCR folyamatot.  

Mindezek a forgatókönyvek az általunk most bemutatott alapmintát használják: **kép betöltése OCR‑hez → nyelv beállítása → felismerés → a szöveg felhasználása**.

## Következtetés

Most már tudod, hogyan **olvass szöveget png‑ből**, **nyerj ki cirill szöveget**, és **alakítsd át a képet szöveggé** az Aspose OCR‑rel C#‑ban. A kulcsfontosságú lépések a motor létrehozása, a kép betöltése, a megfelelő nyelv kiválasztása (ami automatikusan **letölti a cirill nyelvi csomagot**), és végül a `Recognize()` meghívása.  

Próbáld ki különböző képekkel, kísérletezz a `Settings` beállításokkal, és figyeld, ahogy alkalmazásaid kereshetővé, többnyelvűvé és sokkal intelligensebbé válnak.  

Boldog kódolást, és nyugodtan hagyj megjegyzést, ha bármilyen problémába ütközöl!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}