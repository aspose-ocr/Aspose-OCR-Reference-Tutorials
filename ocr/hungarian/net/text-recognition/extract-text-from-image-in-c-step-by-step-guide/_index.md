---
category: general
date: 2026-05-06
description: Képből szöveg kinyerése Aspose OCR-rel C#-ban. Tanulja meg, hogyan konvertáljon
  JPG-t szöveggé, állítsa be az OCR nyelvet, és olvassa el hatékonyan a szöveget a
  JPG-ből.
draft: false
keywords:
- extract text from image
- convert jpg to text
- image to text c#
- read text from jpg
- set OCR language
language: hu
og_description: Szöveg kinyerése képből C#-ban az Aspose OCR-rel. Ez az útmutató bemutatja,
  hogyan konvertáljunk JPG-t szöveggé, állítsuk be az OCR nyelvet, és olvassuk ki
  a szöveget a JPG-ből.
og_title: Szöveg kinyerése képből C#-ban – Teljes útmutató
tags:
- OCR
- C#
- Aspose
title: Kép szövegének kinyerése C#-ban – Lépésről lépésre útmutató
url: /hu/net/text-recognition/extract-text-from-image-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Szöveg kinyerése képből C#‑ban – Teljes programozási útmutató

Valaha is szükséged volt **szöveg kinyerésére képből**, de nem tudtad, melyik könyvtárat válaszd? Nem vagy egyedül – a fejlesztők gyakran kérdezik: „Hogyan konvertáljak JPG‑t szöveggé anélkül, hogy adatot küldenék a felhőbe?” A jó hír, hogy az Aspose OCR egy teljesen offline megoldást kínál, amely közvetlenül a .NET alkalmazásodban működik.

Ebben a tutorialban mindent végigvezetünk: az Aspose OCR NuGet csomag telepítésétől, a **OCR nyelv beállításáig** orosz szöveghez, egészen a **JPG‑ből szöveg olvasásáig**. A végére egy újrahasználható kódrészletet kapsz, amelyet bármely C# projektbe beilleszthetsz, és azonnal szöveget nyerhetsz ki képekből.

> **Mit fogsz megtanulni**  
> • Egy tiszta, futtatható példát, amely **szöveget nyer ki képfájlokból**.  
> • Tudást arról, hogyan **konvertálj JPG‑t szöveggé** az Aspose OCR motor segítségével.  
> • Tippeket a **OCR nyelv beállításához** többnyelvű forgatókönyvekhez.  
> • Edge‑case kezelést olvashatatlan képek és hiányzó nyelvi csomagok esetén.

## Előfeltételek

Mielőtt belevágnánk, győződj meg róla, hogy a következőkkel rendelkezel:

| Követelmény | Miért fontos |
|-------------|--------------|
| .NET 6.0 vagy újabb (bármely friss .NET runtime) | Az Aspose OCR a .NET Standard 2.0+‑t célozza, így az újabb runtime‑ok a legjobb teljesítményt nyújtják. |
| Visual Studio 2022 (vagy VS Code C# kiegészítőkkel) | Egy barátságos IDE segít gyorsan hibakeresni az OCR folyamatot. |
| Internetkapcsolat **egyszer** a Aspose OCR NuGet csomag letöltéséhez | Az első telepítés után engedélyezheted a **offline erőforrásokat**, így további letöltések nem szükségesek. |
| Egy minta JPG kép (`input.jpg`), amely orosz szöveget tartalmaz (vagy bármely más nyelvet, amelyet használni szeretnél) | A tutorial orosz példát használ, de bármely telepített nyelvi csomagra cserélheted. |

Ha valamelyik ismeretlennek tűnik, ne aggódj. Egy NuGet csomag telepítése olyan egyszerű, mint egyetlen parancs beírása, és a többi lépés minden Aspose által támogatott képformátumra ugyanúgy működik.

## A megoldás áttekintése

Magas szinten a folyamat a következőképpen néz ki:

1. **Létrehozunk** egy `OcrEngine`‑t offline erőforrásokkal, hogy a könyvtár ne próbáljon nyelvi adatokat letölteni futás közben.  
2. **Beállítjuk** a kívánt nyelvet (pl. orosz) az `OcrLanguage` enum segítségével.  
3. **Meghívjuk** a `RecognizeImage`‑t egy helyi JPG fájlon.  
4. **Kiírjuk** a kinyert szöveget a konzolra, vagy átadjuk a saját munkafolyamatodnak.

Az alábbi egyszerű diagram szemlélteti az adatáramlást:

![Extract text from image using Aspose OCR in C#](https://example.com/placeholder-image.png){.align-center alt="kép szövegének kinyerése Aspose OCR segítségével C#‑ban"}

*A diagram csak illusztráció; a tényleges munka a kódban történik.*

## Szöveg kinyerése képből – Alapfogalmak

Mielőtt kódot írnánk, bontsuk le néhány gyakran félreértett fogalmat:

- **OfflineResources** – Ha `true`, az Aspose OCR a korábban letöltött nyelvi csomagokat keresi. Ez megszünteti az „auto‑download” lépést, amely lassíthatja a rendszerindítást termelési környezetben.  
- **OcrLanguage** – Az enum tucatnyi nyelvi azonosítót tartalmaz (`English`, `Russian`, `Japanese`, …). A megfelelő nyelv kiválasztása drámaian javítja a pontosságot, mivel a motor nyelvspecifikus heurisztikákat alkalmaz.  
- **Képminőség** – Az OCR a magas kontrasztú, zajmentes képeken működik a legjobban. Ha torz eredményt kapsz, fontold meg az előfeldolgozást (pl. binarizálás) a kép motorba való betáplálása előtt.

Ezeknek a megértése segít eldönteni, mikor **állítsd be kézzel az OCR nyelvet**, és miért nem elég egy egyszerű **JPG‑t szöveggé konvertálás** egy sorban.

## 1. lépés: Aspose OCR NuGet csomag telepítése

Nyiss egy terminált a projekt könyvtárában, és futtasd:

```bash
dotnet add package Aspose.OCR
```

*Pro tipp:* Az első telepítés után add hozzá a `-v latest` kapcsolót, hogy mindig a legújabb stabil buildot kapd. A csomag mérete körülbelül 15 MB, ami a legtöbb asztali vagy szerver környezet számára elfogadható.

## 2. lépés: JPG‑t szöveggé konvertálás – Motor inicializálása

Miután a könyvtár a gépeden van, hozzunk létre egy offline módot használó `OcrEngine`‑t.

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // Step 2.1: Create an OCR engine with offline resources.
        // This prevents the SDK from trying to download language data at runtime.
        var ocrEngine = new OcrEngine(new OcrEngineSettings
        {
            OfflineResources = true   // <-- crucial for production stability
        });

        // Step 2.2: Choose the language pack you need.
        // Here we use Russian; replace with OcrLanguage.English for English text.
        ocrEngine.Language = OcrLanguage.Russian;

        // Step 2.3: Perform OCR on a local JPG file.
        // The file path can be absolute or relative to the executable.
        var result = ocrEngine.RecognizeImage("YOUR_DIRECTORY/input.jpg");

        // Step 2.4: Output the extracted text.
        Console.WriteLine("=== OCR RESULT ===");
        Console.WriteLine(result.Text);
    }
}
```

### Miért fontos

- **Offline mód** garantálja a determinisztikus indítási időket – nincs meglepetés hálózati hívás, amikor egy lezárt szerverre telepíted.  
- **A nyelv beállítása** (`OcrLanguage.Russian`) azt mondja a motornak, hogy az orosz karakterkészletet használja, ami a tiszta képek esetén a felismerési pontosságot ~70 %-ról >95 %-ra növeli.  
- A `RecognizeImage` metódus bármely, az Aspose által támogatott képformátumot elfogad (`.jpg`, `.png`, `.tiff`, …). Ezért **olvasni tudunk szöveget JPG‑ből** anélkül, hogy extra konverzióra lenne szükség.

## 3. lépés: OCR nyelv beállítása – Több nyelv kezelése

Előfordulhat, hogy vegyes nyelvű dokumentumokat kell feldolgoznod (pl. orosz és angol). Az Aspose OCR lehetővé teszi egy *fallback* nyelvi tömb megadását:

```csharp
// Example: Russian primary, English secondary
ocrEngine.Language = OcrLanguage.Russian;
ocrEngine.AdditionalLanguages = new[] { OcrLanguage.English };
```

Ha az elsődleges nyelv nem ismer fel egy karaktert, a motor automatikusan ellenőrzi a kiegészítő listát. Ez a technika különösen hasznos számlák esetén, ahol a cirill betűkkel írt cégnevek keverednek az angol termékkódokkal.

> **Megjegyzés:** A nyelvi csomagoknak a projekt `Resources` mappájában kell lenniük. Ha `FileNotFoundException` hibát kapsz, töltsd le a hiányzó csomagot az Aspose portáljáról, és helyezd a futtatható fájl mellé.

## 4. lépés: Szöveg olvasása JPG‑ből – Gyakori hibák és megoldások

Még a megfelelő nyelvi csomaggal is előfordulhatnak problémák:

| Probléma | Tipikus tünet | Gyors megoldás |
|----------|---------------|----------------|
| Alacsony kontraszt | Torz vagy üres kimenet | Alkalmazz egyszerű kontraszt‑nyújtó szűrőt a `System.Drawing`‑ban OCR előtt. |
| Elforgatott kép | A szöveg oldalra áll | Használd az `ocrEngine.ImageRotation = OcrRotation.Rotate90;` (vagy 180/270) beállítást a `RecognizeImage` hívása előtt. |
| Nagy fájlméret | Lassú felismerés, magas memóriahasználat | Méretezd át a képet legfeljebb 2000 px-re a leghosszabb oldal mentén; az OCR minősége megmarad. |

Itt egy kompakt segédfüggvény, amely átméretezi és javítja a képet, mielőtt a motorba adná:

```csharp
using System.Drawing;
using System.Drawing.Imaging;

static string PreprocessAndRead(string jpgPath)
{
    // Load the original image
    using var original = new Bitmap(jpgPath);

    // Resize while preserving aspect ratio (max 2000px)
    int maxDim = 2000;
    int newWidth, newHeight;
    if (original.Width > original.Height)
    {
        newWidth = maxDim;
        newHeight = original.Height * maxDim / original.Width;
    }
    else
    {
        newHeight = maxDim;
        newWidth = original.Width * maxDim / original.Height;
    }

    using var resized = new Bitmap(original, new Size(newWidth, newHeight));

    // Optional: increase contrast (simple linear stretch)
    var contrast = new ImageAttributes();
    float[][] matrix = {
        new float[] {1.2f, 0, 0, 0, 0},
        new float[] {0, 1.2f, 0, 0, 0},
        new float[] {0, 0, 1.2f, 0, 0},
        new float[] {0, 0, 0, 1, 0},
        new float[] {0, 0, 0, 0, 1}
    };
    contrast.SetColorMatrix(new ColorMatrix(matrix));

    using var graphics = Graphics.FromImage(resized);
    graphics.DrawImage(resized, new Rectangle(0, 0, newWidth, newHeight), 0, 0, newWidth, newHeight, GraphicsUnit.Pixel, contrast);

    // Save to a temporary file (Aspose OCR works with file paths)
    string tempPath = Path.GetTempFileName() + ".jpg";
    resized.Save(tempPath, ImageFormat.Jpeg);

    // Run OCR
    var engine = new OcrEngine(new OcrEngineSettings { OfflineResources = true });
    engine.Language = OcrLanguage.Russian;
    var res = engine.RecognizeImage(tempPath);
    File.Delete(tempPath); // clean up
    return res.Text;
}
```

Ezután meghívhatod: `Console.WriteLine(PreprocessAndRead("YOUR_DIRECTORY/input.jpg"));`, és tisztább eredményt kapsz.

## Teljes működő példa – Minden lépés egy fájlban

Az alábbi *komplett* programot másold be a `Program.cs`‑be. Tartalmazza a telepítési megjegyzéseket, a nyelvi konfigurációt, az előfeldolgozást és a hibakezelést.

```csharp
using System;
using System.Drawing;
using System.Drawing.Imaging;
using System.IO;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        string imagePath = "YOUR_DIRECTORY/input.jpg";

        try
        {

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}