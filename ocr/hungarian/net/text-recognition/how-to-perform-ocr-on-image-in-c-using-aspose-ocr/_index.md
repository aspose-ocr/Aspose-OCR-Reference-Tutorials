---
category: general
date: 2026-10-11
description: Tanulja meg, hogyan végezhet OCR-t képen C#-ban az Aspose.OCR segítségével,
  beleértve a System.Drawing.Common telepítését és a JPG fájlok szövegének kinyerését.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- perform OCR on image
- extract text from JPG
- recognize text from picture
- load image for OCR
- install System.Drawing.Common package
language: hu
lastmod: 2026-10-11
og_description: OCR végrehajtása képen C#-ban az Aspose.OCR használatával. Ez az útmutató
  megmutatja, hogyan telepítsd a System.Drawing.Common csomagot, hogyan tölts be egy
  képet OCR-hez, és hogyan nyerd ki a szöveget egy JPG-ből.
og_image_alt: Screenshot of C# console output displaying recognized text after performing
  OCR on image
og_title: OCR végrehajtása képen C#-ban – lépésről lépésre útmutató
schemas:
- author: Aspose
  dateModified: '2026-10-11'
  description: Learn how to perform OCR on image in C# with Aspose.OCR, including
    installing System.Drawing.Common and extracting text from JPG files.
  headline: How to perform OCR on image in C# using Aspose.OCR
  type: TechArticle
tags:
- OCR
- C#
- Aspose
title: Hogyan végezzünk OCR-t egy képen C#-ban az Aspose.OCR használatával
url: /hu/net/text-recognition/how-to-perform-ocr-on-image-in-c-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan végezzünk OCR-t képen C#‑ban az Aspose.OCR használatával

Ha .NET alkalmazásban **OCR‑t kell végezni képfájlokon**, ez az útmutató egy komplett megoldást mutat be. Az Aspose.OCR segítségével gyorsan **szöveget ismerhet fel a képről** olyan fájlokban, mint a JPG, és megjelenítheti az eredményt egy konzolablakban.

Megtanulja, hogyan:

* **install System.Drawing.Common package** – a könyvtár, amely biztosítja az `Image` osztályt,
* **load image for OCR** – JPEG vagy PNG beolvasása memóriába,
* a nyelvi modellt konfigurálja,
* **perform OCR on image**, majd
* **extract text from JPG** és kiírja azt.

A lépések .NET 6+ környezetre íródtak, de .NET Framework 4.6.1 vagy újabb verzióval is működnek.

---

## Prerequisites

| Requirement | Why it matters |
|-------------|----------------|
| .NET 6 SDK (or .NET Framework 4.6.1+) | Biztosítja a futtatókörnyezetet a C# konzolos alkalmazáshoz. |
| Visual Studio 2022 (or any IDE) | Egyszerűvé teszi a NuGet csomagok hozzáadását és a program futtatását. |
| Internet connection (first run only) | Az Aspose.OCR automatikusan letölti a nyelvi modult. |
| A sample image containing Cyrillic or Latin text (e.g., `sample_cyrillic.jpg`) | A **extract text from JPG** bemutatására szolgál. |

---

## Step 1: Install System.Drawing.Common package

A `System.Drawing.Common` NuGet csomag biztosítja az `Image` osztályt, amelyet a **load image for OCR** során használni fog. Nyissa meg a Package Manager Console‑t, és futtassa:

```powershell
Install-Package System.Drawing.Common
```

> **Pro tip:** Célozza a `net6.0-windows` keretrendszert, vagy adja hozzá a `<UseWindowsForms>true</UseWindowsForms>` elemet a projektfájlhoz, ha platform‑specifikus figyelmeztetéseket kap Linuxon/macOS‑en.

---

## Step 2: Add the Aspose.OCR NuGet package

Az Aspose.OCR tartalmazza az OCR motorját és a nyelvi modelleket. Telepítse a következő paranccsal:

```powershell
Install-Package Aspose.OCR
```

A csomag könnyű; a szükséges nyelvi adatok (pl. Cyrillic) az első `OcrEngine.Language` beállításkor kerülnek letöltésre.

---

## Step 3: How to load image for OCR

A kép betöltése az első konkrét lépés, mielőtt **perform OCR on image** műveletet végezhetne. Az `Image.FromFile` metódus bármely, a GDI+ által támogatott formátumot beolvas, beleértve a JPG‑t, PNG‑t, BMP‑t és TIFF‑et.

```csharp
using System.Drawing; // Requires System.Drawing.Common

// Replace the path with the location of your test picture.
string imagePath = @"YOUR_DIRECTORY/sample_cyrillic.jpg";
Image ocrImage = Image.FromFile(imagePath);
```

*Ha a fájl nem létezik, `FileNotFoundException` kerül dobásra – a termelési kódban érdemes try/catch blokkba helyezni a hívást.*

---

## Step 4: Configure the engine and **perform OCR on image**

Hozzon létre egy `OcrEngine` példányt, válassza ki a nyelvi modellt, rendelje hozzá a betöltött képet, majd hívja meg a `Recognize()` metódust.

```csharp
using Aspose.OCR;

// Step 4: Initialize OCR engine and set language
var ocrEngine = new OcrEngine
{
    // Choose the language you need; Cyrillic is used in this example.
    Language = OcrLanguage.Cyrillic,
    Image = ocrImage
};

// Execute the OCR operation
OcrResult ocrResult = ocrEngine.Recognize();
```

A `Recognize()` metódus egy `OcrResult` objektumot ad vissza, amely a kinyert szöveget, a megbízhatósági pontszámokat és a körülhatároló dobozokat tartalmazza. A nyelvi modul automatikusan letöltődik az első használatkor, így nincs szükség további fájlokra.

---

## Step 5: **Extract text from JPG** and display it

Most már **recognize text from picture** és kiírhatja az eredményt. Az `OcrResult` `Text` tulajdonsága a tiszta karakterláncot tartalmazza.

```csharp
// Step 5: Output recognized text
Console.WriteLine("Recognized text:");
Console.WriteLine(ocrResult.Text);
```

### Expected console output

```
Recognized text:
Пример текста на кириллице
```

Ha a forráskép angol szöveget tartalmaz, a kimenet az a angol mondat lesz, amelyet a képre helyezett.

---

## Edge cases and best‑practice tips

| Situation | Recommendation |
|-----------|----------------|
| **Large images ( > 5 MB )** | Módosítsa a kép méretét ≤ 2000 px-re a leghosszabb oldalon OCR előtt, hogy csökkentse a memóriahasználatot és növelje a sebességet. |
| **Multiple languages in one picture** | Hívja meg a `ocrEngine.AddLanguage(OcrLanguage.English)`-t a Cyrillic mellett, majd állítsa be a `ocrEngine.Language = OcrLanguage.Multilingual` értéket. |
| **Low‑contrast scans** | Növelje a kontrasztot a `System.Drawing.Graphics` segítségével, mielőtt a bitmapet átadná a motornak. |
| **Running on Linux/macOS** | Győződjön meg róla, hogy a `libgdiplus` natív függőség telepítve van (`sudo apt-get install -y libgdiplus`). |
| **Repeated OCR calls** | Használja újra ugyanazt az `OcrEngine` példányt, és csak cserélje le az `ocrEngine.Image`‑t, hogy elkerülje a modul többszöri betöltését. |

---

## Full, runnable program

Az alábbiakban a teljes konzolos alkalmazás látható, amely magában foglalja az összes korábbi lépést. Másolja a kódot egy új C# konzolprojektbe, cserélje le a kép útvonalát, és futtassa.

```csharp
using System;
using System.Drawing;                 // Install System.Drawing.Common if needed
using Aspose.OCR;                     // NuGet package: Aspose.OCR

class Program
{
    static void Main()
    {
        // Step 1: Install System.Drawing.Common (handled via NuGet)
        // Step 2: Install Aspose.OCR (handled via NuGet)

        // Step 3: Load the image that contains the text to be recognized
        // Replace the placeholder with the actual path to your JPG or PNG file.
        string imagePath = @"YOUR_DIRECTORY/sample_cyrillic.jpg";
        Image ocrImage;
        try
        {
            ocrImage = Image.FromFile(imagePath);
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Failed to load image: {ex.Message}");
            return;
        }

        // Step 4: Create the OCR engine and choose the language model
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.Cyrillic, // Change to OcrLanguage.English for Latin scripts
            Image = ocrImage
        };

        // Step 5: Perform OCR on the loaded picture
        OcrResult ocrResult = ocrEngine.Recognize();

        // Step 6: Display the extracted text
        Console.WriteLine("Recognized text:");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Running the program** kiírja a felismert karakterláncot a konzolra, ezzel megerősítve, hogy sikeresen **performed OCR on image** és **extracted text from JPG**.

---

## Conclusion

Most már tudja, hogyan **perform OCR on image** fájlokon C#‑ban az Aspose.OCR használatával, a szükséges **System.Drawing.Common package** telepítésétől a **loading image for OCR**‑ig, a megfelelő nyelv kiválasztásáig, és végül a **extracting text from JPG**‑ig. Ez az end‑to‑end példa szilárd alapot ad a fejlettebb dokumentum‑feldolgozó csővezetékek építéséhez, például képek mappáinak kötegelt feldolgozásához vagy az OCR integrálásához egy web‑API‑ba.

### What’s next?

* Fedezze fel a **recognize text from picture** funkciót PDF‑ekben, az egyes oldalak képpé konvertálása után.
* Kísérletezzen az `OcrEngine` `Resolution`, `Threshold` és `MaxProcessingTime` tulajdonságaival a zajos beolvasások pontosságának finomhangolásához.
* Kombinálja az OCR kimenetet egy természetes nyelvfeldolgozó könyvtárral, hogy automatikusan kategorizálja a kinyert tartalmat.

Nyugodtan módosítsa a kódot más képformátumokhoz, adjon hozzá hibakezelést, vagy integrálja nagyobb alkalmazásokba. Boldog kódolást!

## What Should You Learn Next?

A következő oktatóanyagok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás komplett, működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsen elsajátítani további API‑funkciókat és alternatív megvalósítási megközelítéseket saját projektjeiben.

- [Extract Text from Image in C# – Complete Aspose OCR Guide](/ocr/english/net/text-recognition/extract-text-from-image-in-c-complete-aspose-ocr-guide/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [How to Perform Image Text Extraction from Stream Using Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}