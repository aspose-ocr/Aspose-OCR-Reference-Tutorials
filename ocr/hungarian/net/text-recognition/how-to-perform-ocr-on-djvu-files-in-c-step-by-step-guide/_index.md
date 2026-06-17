---
category: general
date: 2026-02-20
description: Hogyan végezzünk OCR-t DjVu fájlokon C#-ban. Tanulja meg, hogyan ismerje
  fel a szöveget a képről, és konvertálja gyorsan a DjVu-t szöveggé az Aspose OCR
  segítségével.
draft: false
keywords:
- how to perform OCR
- recognize text from image
- how to read djvu
- extract text from image
- convert djvu to text
language: hu
og_description: Hogyan végezzünk OCR-t DjVu fájlokon C#-ban. Ez az útmutató megmutatja,
  hogyan ismerjünk fel szöveget képről, olvassuk a DjVu-t, és konvertáljuk a DjVu-t
  szöveggé az Aspose OCR használatával.
og_title: Hogyan végezzünk OCR-t DjVu fájlokon C#-ban – Teljes útmutató
tags:
- OCR
- C#
- DjVu
- Aspose
title: Hogyan végezzünk OCR-t DjVu fájlokon C#‑ban – Lépésről lépésre útmutató
url: /hu/net/text-recognition/how-to-perform-ocr-on-djvu-files-in-c-step-by-step-guide/
---

How to Perform OCR on DjVu Files in C# – Complete Guide" => "Hogyan végezzünk OCR-t DjVu fájlokon C#-ban – Teljes útmutató"

Paragraphs.

We'll translate naturally.

Let's produce final answer.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan végezzünk OCR-t DjVu fájlokon C#‑ban – Teljes útmutató

Gondolkodtál már azon, **hogyan végezzünk OCR‑t** egy DjVu dokumentumon anélkül, hogy a hajadhoz nyúlnál? Nem vagy egyedül. Sok fejlesztő akad el, amikor **szöveget kell felismerni képek** forrásából, amelyek DjVu konténerekben élnek. A jó hír? Néhány C# sorral és az Aspose OCR könyvtárral pillanatok alatt kinyerheted a rejtett szöveget.

Ebben az útmutatóban végigvezetünk minden lépésen, ami ahhoz kell, hogy egy DjVu oldalt egyszerű szöveggé alakíts. A végére **tudni fogod, hogyan olvassunk DjVu‑t**, hogyan **nyerjünk ki szöveget képek** objektumaiból, és még **hogyan konvertáljunk DjVu‑t szöveggé** további feldolgozáshoz. Nincs külső szolgáltatás, nincs homályos hivatkozás – csak egy önálló, futtatható példa.

## Előfeltételek

Mielőtt belevágnánk, győződj meg róla, hogy a következők a rendelkezésedre állnak:

- .NET 6.0 SDK vagy újabb (a kód .NET Framework 4.8‑al is működik).
- Visual Studio 2022 vagy bármely szerkesztő, amely támogatja a C#‑t.
- Aspose OCR for .NET licenc (az ingyenes próba verzió tesztelésre elegendő).
- Egy minta DjVu fájl (`sample.djvu`), amelyet egy hivatkozható mappában helyeztél el.

Ezek előkészítése biztosítja a zökkenőmentes munkafolyamatot – nem lesznek “hiányzó hivatkozás” meglepetések később.

## Hogyan végezzünk OCR‑t egy DjVu oldalon

Az alapgondolat egyszerű: betöltjük a DjVu oldalt képként, átadjuk az OCR motornak, majd kiolvassuk a kapott karakterláncot. Lépésről lépésre bontva:

### 1. lépés: Telepítsd az Aspose OCR‑t

Nyiss egy terminált a projekt mappádban, és futtasd:

```bash
dotnet add package Aspose.OCR
```

Ez letölti a legújabb Aspose OCR binárisokat és azok függőségeit. Ha a NuGet Package Manager UI‑t részesíted előnyben, egyszerűen keresd meg a **Aspose.OCR**‑t és kattints a **Install** gombra.

### 2. lépés: Inicializáld az OCR motort

Az `OcrEngine` példány létrehozása az első dolog, amit megteszel, amikor **OCR‑t szeretnél végezni**. Gondolj rá úgy, mint a szkenner agyának bekapcsolására.

```csharp
using Aspose.OCR;

// ...

// Step 2: Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();
```

> **Pro tipp:** Egyetlen `OcrEngine` újra‑használata több oldal esetén memóriát takarít meg és felgyorsítja a feldolgozást.

### 3. lépés: Töltsd be a DjVu oldalt képként

A DjVu fájlok nem közvetlenül támogatottak a legtöbb képi API‑ban, de az Aspose minden oldalt bitmapként kezelhet. Itt a `System.Drawing.Image`‑t használjuk a fájl beolvasásához.

```csharp
using System.Drawing;

// ...

// Step 3: Load a DjVu page as an image
string djvuPath = @"C:\Path\To\Your\Directory\sample.djvu";
Image djvuPage = Image.FromFile(djvuPath);
```

> **Miért működik:** Az `Image.FromFile` automatikusan dekódolja a DjVu adatfolyamot egy raszteres formátumba, amelyet az OCR motor ért. Ha egy többoldalas DjVu egy adott oldalát szeretnéd feldolgozni, előbb használd az Aspose PDF vagy Aspose Imaging‑et az oldal kinyeréséhez.

### 4. lépés: Szövegfelismerés képről

Most jön a varázslat. A `Recognize` metódus átvizsgálja a bitmapet, és egy karakterláncot ad vissza, amely a felismert karaktereket tartalmazza.

```csharp
// Step 4: Perform OCR to extract text from the image
string extractedText = ocrEngine.Recognize(djvuPage);
```

Ekkor már **szöveget ismerünk fel képről**, amely eredetileg egy DjVu konténerben volt. A karakterlánc tartalmazhat sortöréseket, írásjeleket, sőt Unicode karaktereket is, ha a forrásnyelv támogatja őket.

### 5. lépés: Az eredmény megjelenítése vagy tárolása

Gyors ellenőrzésként egyszerűen írd ki a szöveget a konzolra. Egy valós alkalmazásban valószínűleg fájlba vagy adatbázisba írnád.

```csharp
// Step 5: Display the recognized text
Console.WriteLine("=== Extracted Text ===");
Console.WriteLine(extractedText);
```

Összeállítva, itt a teljes, azonnal futtatható program.

```csharp
// File: DjvuOcrExample.cs
using System;
using System.Drawing;
using Aspose.OCR;

class DjvuExample
{
    static void Main()
    {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Load a DjVu page as an image
        Image djvuPage = Image.FromFile(@"C:\Path\To\Your\Directory\sample.djvu");

        // Perform OCR to extract text from the image
        string extractedText = ocrEngine.Recognize(djvuPage);

        // Display the recognized text
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(extractedText);
    }
}
```

**Várható kimenet** (rövidítve):

```
=== Extracted Text ===
The quick brown fox jumps over the lazy dog.
Lorem ipsum dolor sit amet, consectetur...
```

Ha torz karaktereket látsz, ellenőrizd, hogy a DjVu fájl nincs-e titkosítva, és hogy a `ocrEngine.Language` megfelelő nyelvre van-e állítva. Alapértelmezés szerint az angolt használja; francia, német stb. nyelvre a `ocrEngine.Language = Language.French;` beállítással válthatsz.

## Recognize Text from Image – Gyakori hibák

Még egy jól működő példával is a fejlesztők gyakran elakadhatnak néhány széljegyen:

| Probléma | Miért fordul elő | Megoldás |
|----------|------------------|----------|
| **Üres kimenet** | A képfelbontás túl alacsony (<300 dpi). | Használd a `ocrEngine.ImageResolution = 300;` beállítást a `Recognize` hívása előtt. |
| **Rossz nyelv** | Az OCR alapértelmezés szerint angolt használ. | Állítsd be a `ocrEngine.Language = Language.Spanish;` (vagy bármely támogatott nyelvet). |
| **Memóriaszivárgás** | Nagy DjVu oldalak a feldolgozás után a memóriában maradnak. | Hívd meg a `djvuPage.Dispose();`‑t, miután befejezted. |
| **Többoldalas DjVu** | Csak az első oldal töltődik be. | Iterálj az oldalakon az Aspose Imaging `DjvuImage` osztályával. |

Ezek korai kezelése rengeteg hibakeresési órát takarít meg.

## Hogyan olvassunk DjVu fájlokat C#‑ban – Az egyszerű OCR‑n túl

Ha a projekted több, mint egyetlen oldalt igényel, előbb minden oldalt képként kell kinyerned. Az Aspose Imaging ezt könnyedén megoldja:

```csharp
using Aspose.Imaging;
using Aspose.Imaging.FileFormats.Djvu;

// ...

string djvuPath = @"sample.djvu";
using (DjvuImage djvu = (DjvuImage)Image.Load(djvuPath))
{
    for (int i = 0; i < djvu.Frames.Count; i++)
    {
        using (Image page = djvu.Frames[i].ConvertToRaster())
        {
            // Run OCR on each page
            string pageText = ocrEngine.Recognize(page);
            Console.WriteLine($"--- Page {i + 1} ---");
            Console.WriteLine(pageText);
        }
    }
}
```

Ez a minta lehetővé teszi, hogy **DjVu‑t szöveggé konvertálj** oldalanként, ami tökéletes nagy archívumok kötegelt feldolgozásához.

## Extract Text from Image – Pontosság finomhangolása

Az alap OCR beállítások jól működnek tiszta szkenneléseknél, de a pontosságot tovább növelheted:

```csharp
ocrEngine.ImagePreprocessingOptions = new ImagePreprocessingOptions()
{
    // Binarize the image to improve contrast
    BinarizationMethod = BinarizationMethod.Otsu,
    // Deskew the image if it’s tilted
    Deskew = true,
    // Remove noise
    NoiseRemoval = true
};
```

Ezek a finomhangolások különösen hasznosak, ha a DjVu forrás kézírásos jegyzeteket vagy alacsony kontrasztú grafikákat tartalmaz.

## Convert DjVu to Text – Teljes vég‑végi példa

Az alábbi kompakt verzió mindent egy helyen mutat: többoldalas DjVu betöltése, minden oldal előfeldolgozása, OCR végrehajtása, és az eredmény mentése egy `.txt` fájlba.

```csharp
using System;
using System.IO;
using Aspose.Imaging;
using Aspose.Imaging.FileFormats.Djvu;
using Aspose.OCR;
using Aspose.OCR.Models;

class DjvuToTextConverter
{
    static void Main()
    {
        // Prepare OCR engine with preprocessing
        OcrEngine ocr = new OcrEngine
        {
            ImagePreprocessingOptions = new ImagePreprocessingOptions()
            {
                BinarizationMethod = BinarizationMethod.Otsu,
                Deskew = true,
                NoiseRemoval = true
            }
        };

        string inputPath = @"C:\Docs\sample.djvu";
        string outputPath = @"C:\Docs\sample_extracted.txt";

        using (DjvuImage djvu = (DjvuImage)Image.Load(inputPath))
        using (StreamWriter writer = new StreamWriter(outputPath))
        {
            for (int i = 0; i < djvu.Frames.Count; i++)
            {
                using (var page = djvu.Frames[i].ConvertToRaster())
                {
                    string text = ocr.Recognize(page);
                    writer.WriteLine($"--- Page {i + 1} ---");
                    writer.WriteLine(text);
                }
            }
        }

        Console.WriteLine($"Extraction complete. Text saved to {outputPath}");
    }
}
```

A script futtatása létrehozza a `sample_extracted.txt` fájlt, amelyben minden oldal tartalma tisztán elválasztva szerepel. Ez a leggyorsabb mód a **DjVu‑t szöveggé konvertáláshoz** indexelés, keresés vagy archiválás céljából.

## Összegzés

Megmutattuk, **hogyan végezzünk OCR‑t** DjVu fájlokon az elejétől a végéig, és bemutattuk a **szövegfelismerés** lehetőségeit a

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}