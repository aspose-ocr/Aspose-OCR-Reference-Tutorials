---
category: general
date: 2026-03-18
description: Hogyan korrigáljuk a kép dőlését és csökkentsük a zajt a beolvasott fájlokban.
  Tanulja meg, hogyan töltsön be képet fájlból, hogyan nyerjen ki szöveget TIFF-ből,
  és hogyan ismerje fel a szöveget a képen az Aspose OCR-rel.
draft: false
keywords:
- how to deskew image
- how to reduce noise
- recognize text from image
- load image from file
- extract text from tiff
language: hu
og_description: Hogyan korrigáljuk gyorsan a kép ferdeségét az Aspose OCR-rel. Ez
  az útmutató bemutatja, hogyan csökkenthetjük a zajt, tölthetünk be képet fájlból,
  és hogyan nyerhetünk ki szöveget TIFF-ből C#-ban.
og_title: Hogyan kiegyenesítsük a képet – Teljes C# OCR útmutató
tags:
- OCR
- C#
- Image Processing
title: Hogyan állítsuk egyenesre a képet és tisztítsuk meg a szkenneléseket – Teljes
  C# útmutató
url: /hu/net/skew-angle-calculation/how-to-deskew-image-and-clean-up-scans-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan egyenesítsünk képet – Teljes C# OCR útmutató

Valaha is elgondolkodtál **how to deskew image** fájlokon, amelyek úgy néznek ki, mintha egy ingatag szkennerről származnának? Nem vagy egyedül. A legtöbb fejlesztő ebben a helyzetben akad el, amikor a forrás TIFF egy kicsit ferde, és az OCR eredmények rendetlenek lesznek. A jó hír? Néhány C# sorral kiegyenesítheted a képet, eltávolíthatod a szemcsés hátteret, és tiszta, kereshető szöveget nyerhetsz ki a fájlból.

Ebben az útmutatóban végigvezetünk a **how to reduce noise**, **load image from file**, és végül a **recognize text from image** folyamatokon az Aspose OCR használatával. A végére képes leszel **extract text from tiff** dokumentumokból anélkül, hogy izzadnál.

> **Pro tipp:** Ha már használod az Aspose OCR‑t más projektekben, ezeket a szűrőket bármilyen extra licencelési gond nélkül beillesztheted.

---

## Amire szükséged lesz

- .NET 6 vagy újabb (a kód .NET Core‑on is működik)  
- Aspose.OCR NuGet csomag (`Install-Package Aspose.OCR`)  
- Egy beolvasott TIFF, amely kissé elfordult vagy zajos (példaként a `skewed_scanned_doc.tif` fájlt használjuk)  
- Szövegszerkesztő vagy IDE (Visual Studio, VS Code, Rider – válaszd a kedved szerint)

Nem szükséges további könyvtár, a használandó szűrők be vannak építve az Aspose OCR‑be.

## 1. lépés – OCR motor létrehozása (How to Deskew Image)

Az első dolog, amit csinálsz, egy `OcrEngine` példány létrehozása. Gondolj rá úgy, mint egy agyra, amely később elolvassa helyetted a karaktereket.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Filters;

class PreprocessDemo
{
    static void Main()
    {
        // Initialize the OCR engine – this object holds all settings
        var ocrEngine = new OcrEngine();
```

Miért hozod létre előre a motort? Egyetlen helyet biztosít a előfeldolgozó szűrők, nyelvi csomagok és kimeneti beállítások csatolásához. Ha ezt a lépést kihagyod, és közvetlenül meghívod az `OcrEngine.Recognize`‑t, elveszíted a lehetőséget, hogy előbb megtisztítsd a képet – ami pont az egyenesítés miatt fontos.

## 2. lépés – Deskew és zajcsökkentő szűrők hozzáadása (How to Reduce Noise)

Most két szűrőt csatolunk:

| Szűrő | Mit csinál | Miért fontos |
|--------|--------------|----------------|
| `AutoDeskewFilter` | Felismeri és korrigálja a forgatást | Egyenesíti a szövegsorokat, hogy az OCR motor helyesen olvashassa őket |
| `NoiseReductionFilterV2` | Eltávolítja a foltokat és a háttérzajt | A tisztább pixelek kevesebb hibás felismerést eredményeznek |

```csharp
        // Add filters to improve OCR accuracy
        ocrEngine.Settings.Filters.Add(new AutoDeskewFilter());          // corrects rotation
        ocrEngine.Settings.Filters.Add(new NoiseReductionFilterV2());   // reduces background noise
```

A `NoiseReductionFilterV2` helyettesíthető a régebbi verzióval, de a v2 algoritmus jobban kezeli a modern szkennereket. Ha a dokumentumod már tökéletesen sík, a deskew szűrő egyszerűen változatlanul továbbadja a képet – semmi baj.

## 3. lépés – Kép betöltése fájlból (Load Image from File)

Az Aspose egy kényelmes `ImageStream.FromFile` segédfüggvényt biztosít, amely számos formátumot olvas, köztük TIFF, JPEG, PNG és BMP. Íme, hogyan töltjük be a fájlt a memóriába:

```csharp
        // Load the scanned image you want to preprocess
        var image = ImageStream.FromFile(@"YOUR_DIRECTORY/skewed_scanned_doc.tif");
```

Cseréld le a `YOUR_DIRECTORY`‑t a géped tényleges elérési útjára. Ha relatív úttal dolgozol, győződj meg róla, hogy a fájl a végrehajtható fájlod mellett helyezkedik el, vagy állítsd be megfelelően a munkakönyvtárat.

## 4. lépés – OCR futtatása az előfeldolgozott képen (Recognize Text from Image)

A szűrők beállítása és a kép betöltése után végül megkérjük az Aspose‑t, hogy olvassa el a karaktereket:

```csharp
        // Perform OCR – the engine will automatically apply the filters first
        var ocrResult = ocrEngine.Recognize(image);
```

A háttérben a motor lefuttatja a deskew algoritmust, kisimítja a zajt, majd egy neurális‑hálózaton alapuló felismerőt alkalmaz. Az eredmény egy `OcrResult` objektumba van csomagolva, amely nyújtja a nyers szöveget, a megbízhatósági pontszámokat, és akár a körülhatároló dobozokat is, ha később szükséged lenne rájuk.

## 5. lépés – Kinyert szöveg megjelenítése vagy mentése (Extract Text from TIFF)

Egy gyors demóhoz egyszerűen a konzolra írjuk a szöveget, de akár fájlba, adatbázisba is mentheted, vagy egy további munkafolyamatba továbbadhatod.

```csharp
        // Show the recognized text in the console
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Várható kimenet** (példa, a dokumentumtól függően változik):

```
Invoice #12345
Date: 2023‑04‑01
Total: $1,250.00
Thank you for your business!
```

Ha a kimenet még mindig torz karaktereket tartalmaz, ellenőrizd, hogy az eredeti TIFF nem túl alacsony felbontású (minimum 300 dpi ajánlott), és hogy a nyelv helyesen van beállítva az `ocrEngine.Settings.Language`‑ben.

## Teljes működő példa (All Steps in One Place)

Az alábbi teljes programot másold be egy új konzolprojektbe, és futtasd azonnal.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Filters;

class PreprocessDemo
{
    static void Main()
    {
        // 1️⃣ Create OCR engine
        var ocrEngine = new OcrEngine();

        // 2️⃣ Add preprocessing filters
        ocrEngine.Settings.Filters.Add(new AutoDeskewFilter());          // deskew image
        ocrEngine.Settings.Filters.Add(new NoiseReductionFilterV2());   // reduce noise

        // 3️⃣ Load the image file (TIFF, JPEG, etc.)
        var image = ImageStream.FromFile(@"YOUR_DIRECTORY/skewed_scanned_doc.tif");

        // 4️⃣ Recognize text – filters run automatically
        var ocrResult = ocrEngine.Recognize(image);

        // 5️⃣ Output the extracted text
        Console.WriteLine(ocrResult.Text);
    }
}
```

Mentsd a fájlt `Program.cs` néven, futtasd a `dotnet run` parancsot, és a tisztított szövegnek meg kell jelennie a terminálodban.

## Gyakran ismételt kérdések és széljegyek

### Mi van, ha a TIFF több oldalt tartalmaz?

Az Aspose OCR képes többoldalas képeket feldolgozni a `image.GetPages()` (vagy `image.Pages`) ciklusával. Minden oldal saját `OcrResult`‑ot ad vissza. Ha egyetlen szövegre van szükséged, kombináld őket `StringBuilder`‑rel.

### Működik a deskew szűrő erősen elfordított képeken?

Legfeljebb körülbelül ±15°-os forgatást kezel. Ezen felül előfordulhat, hogy manuálisan kell előforgatnod a képet egy grafikus könyvtárral (pl. `System.Drawing` vagy `SkiaSharp`) az Aspose‑ba való betáplálás előtt.

### Hogyan javíthatom a pontosságot nem‑angol szövegek esetén?

Állítsd be a nyelvet kifejezetten:

```csharp
ocrEngine.Settings.Language = Language.English; // or Language.French, etc.
```

Egyedi nyelvi csomagokat is betölthetsz, ha a beépített nem fedi le az ábécédet.

### Futtatható ez Linuxon?

Természetesen. Az Aspose OCR platformfüggetlen; csak győződj meg róla, hogy a natív függőségek jelen vannak (általában nincs szükség a tiszta .NET verzióhoz). Használd a `dotnet publish -r linux-x64` parancsot egy önálló bináris létrehozásához.

## Bónusz: Az egyenesített kép megjelenítése

Ha szeretnéd látni a korrigált képet az OCR előtt, vissza is mentheted a lemezre:

```csharp
// After OCR, the filtered image is stored in ocrEngine.Settings.FiltersResult
var corrected = ocrEngine.Settings.FiltersResult;
corrected.Save(@"output/deskewed_cleaned.tif");
```

![hogyan egyenesítsünk képet példa](https://example.com/deskew-demo.png "hogyan egyenesítsünk képet példa")

*Kép alternatív szövege:* **hogyan egyenesítsünk képet példa** – egy elfordult TIFF előtte/utána állapotát mutatja, amelyet az AutoDeskewFilter korrigált.

## Összegzés

Áttekintettük, hogyan **how to deskew image** fájlokat, **how to reduce noise**-t, és az egész folyamatot a **recognize text from image**, **load image from file**, valamint **extract text from tiff** lépésekkel az Aspose OCR használatával C#‑ban. A fő tanulság? Csak két előfeldolgozó szűrő hozzáadásával egy ingatag, szemcsés szkennt tiszta, kereshető dokumentummá alakíthatsz külső eszközök nélkül.

Készen állsz a következő lépésre? Próbáld ki a `AutoDeskewFilter` helyett a `AutoRotateFilter` használatát, ha a dokumentumaid fejjel lefelé vannak, vagy kísérletezz a `ContrastEnhancementFilter`‑rel elhalványult nyomatok esetén. Ugyanaz a minta – motor → szűrők → betöltés → felismerés – minden Aspose OCR szcenárióban érvényes, így újrahasznosíthatod ezt a vázat PDF‑ekhez, PNG‑khez vagy akár fényképekhez is.

Boldog kódolást, és legyen az OCR‑d mindig pontos!  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}