---
category: general
date: 2026-01-09
description: Gyorsan extrahálja a szöveget PNG‑ből az Aspose OCR‑rel. Tanulja meg,
  hogyan olvassa ki a képen lévő szöveget, javítsa az OCR pontosságát, és kapjon tiszta
  eredményeket C#‑ban.
draft: false
keywords:
- extract text from png
- read image text
- improve ocr accuracy
- extract text from image
- aspose ocr tutorial
language: hu
og_description: Gyorsan nyerjen ki szöveget PNG-ből az Aspose OCR-rel. Tanulja meg,
  hogyan olvassa el a képek szövegét, javítsa az OCR pontosságát, és szerezzen tiszta
  eredményeket C#‑ban.
og_title: Szöveg kinyerése PNG-ből – Teljes Aspose OCR útmutató
tags:
- Aspose OCR
- C#
- Image Processing
title: Szöveg kinyerése PNG-ből – Teljes Aspose OCR útmutató
url: /hu/net/text-recognition/extract-text-from-png-complete-aspose-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PNG-ből szöveg kinyerése – Teljes Aspose OCR bemutató

Valaha is szükséged volt **szöveg kinyerése PNG-ből** fájlokból, de az eredmények tele voltak érthetetlen szöveggel? Nem vagy egyedül. Sok valós projektben – számlák, bizonylatok vagy beolvasott űrlapok – az OCR kimenet minősége döntő lehet az automatizálási folyamatok sikerében.  

Ebben az útmutatóban lépésről‑lépésre megmutatjuk, hogyan olvassuk ki a képen lévő szöveget az Aspose OCR segítségével, hogyan használjunk egy egyedi szótárat az **OCR pontosságának javításához**, hogyan tisztítsuk meg a zajt, és végül hogyan nyomtassunk egy rendezett karakterláncot. A végére egy futtatható C# konzolalkalmazást kapsz, amely megbízhatóan kinyeri a szöveget PNG‑képekből.

> **Mit fogsz megtanulni**  
> * Egy komplett, futtatható kódmintát.  
> * Miért fontos egy egyedi szótár.  
> * Tippek a nehéz esetek, például alacsony kontrasztú beolvasások kezeléséhez.  

## Előfeltételek

- .NET 6 SDK vagy újabb (a kód .NET 6‑ra céloz, de .NET 5 is működik).  
- Visual Studio 2022 vagy bármelyik kedvenc szerkesztő.  
- Egy **PNG** kép, amelyet feldolgozni szeretnél – például `invoice.png`.  
- Az **Aspose.OCR** NuGet csomag (`dotnet add package Aspose.OCR`).  

Külön konfigurációs fájlra nincs szükség; minden egyetlen `.cs` fájlban van.

## 1. lépés – Aspose OCR telepítése és hivatkozása

Először húzd be a könyvtárat a projektedbe. Nyiss egy terminált a megoldás mappájában és futtasd:

```bash
dotnet add package Aspose.OCR
```

Ez az egyetlen sor letölti a legújabb stabil verziót (2026. januárjában, 23.9 verzió). A csomag tartalmazza a `OcrEngine` osztályt, amelyet a teljes útmutató során használni fogunk.

## 2. lépés – Az OCR motor inicializálása

Az `OcrEngine` példány létrehozása az alap. Olyan, mintha bekapcsolnád a szkennert, amely készen áll a pixelek értelmezésére.

```csharp
using Aspose.OCR;

// Initialize the OCR engine
var ocrEngine = new OcrEngine();
```

> **Pro tipp:** Ha sok képet szeretnél egy ciklusban feldolgozni, használd újra ugyanazt az `OcrEngine` példányt. Ez belső erőforrásokat cache‑el és felgyorsítja a későbbi hívásokat.

## 3. lépés – Pontosság növelése egy egyedi szótárral

A kész OCR jó, de elakadhat a domain‑specifikus szavaknál, mint például „Aspose”, „OCR” vagy „SDK”. Ezeknek a kifejezéseknek az **egyedi szótárba** való felvétele azt mondja a motornak, hogy ezek a karakterláncok érvényesek, ezáltal csökkentve a félreolvasásokat.

```csharp
// Define domain‑specific terms that the engine should recognize
ocrEngine.CustomDictionary = new HashSet<string>
{
    "Aspose",
    "OCR",
    "SDK",
    "invoice"
};
```

### Miért segít egy egyedi szótár

- **Statisztikai modellek** az OCR mögött erősen súlyozzák a gyakori nyelvi mintákat. A ritka szavak alacsony valószínűséggel bírnak, és hasonló kinézetű karakterekkel helyettesülhetnek.  
- Ha kifejezetten felsorolod őket, felülbírálod a modell találgatását.  
- Különösen hasznos **képen lévő szöveg olvasásához**, ha a szöveg termékkódokat, rövidítéseket vagy márkaneveket tartalmaz.

## 4. lépés – Szöveg felismerése a PNG fájlból

Most adjuk meg a motor számára a kép elérési útját. A `RecognizeImage` metódus egy nyers karakterláncot ad vissza, amely még ismeretlen tokeneket (pl. „#@!”) tartalmazhat, amelyeket a motor nem tudott leképezni.

```csharp
// Path to the PNG you want to process
string imagePath = @"YOUR_DIRECTORY/invoice.png";

// Perform OCR
string rawText = ocrEngine.RecognizeImage(imagePath);
```

> **Külön eset:** Ha a fájl nem található, a `RecognizeImage` `FileNotFoundException`‑t dob. Éles környezetben tedd a hívást try‑catch blokkba.

## 5. lépés – Az eredmény tisztítása a `CleanText`‑el

Az Aspose OCR egy segédfüggvényt biztosít, amely eltávolítja azokat a karaktereket, amelyeket „ismeretlennek” jelöl. Ez a lépés kulcsfontosságú **szöveg kinyerése képből** projektekhez, ahol a downstream parser csak alfanumerikus karaktereket és alapvető írásjeleket vár.

```csharp
// Remove unknown tokens and extra whitespace
string cleanedText = ocrEngine.CleanText(rawText);
```

A `CleanText` metódus emellett normalizálja a sorvégeket, így a kimenet biztonságosan tárolható adatbázisokban vagy továbbadható más szolgáltatásoknak.

## 6. lépés – A tisztított szöveg kiírása

Végül jelenítsd meg vagy tárold az eredményt. Egy konzolalkalmazásban a `Console.WriteLine` elvégzi a feladatot.

```csharp
Console.WriteLine("=== Cleaned OCR Output ===");
Console.WriteLine(cleanedText);
```

A program futtatásakor egy rendezett szövegrészt kell látnod, amely tükrözi a `invoice.png` tartalmát. Ha a kép tartalmazza az „Aspose” szót, az egyedi szótár biztosítja, hogy helyesen jelenjen meg, nem pedig például „A5p0se”.

## Teljes működő példa

Összegezve, itt van a teljes `Program.cs`, amelyet egyszerűen beilleszthetsz egy új konzolprojektbe:

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize the OCR engine
        var ocrEngine = new OcrEngine();

        // 2️⃣ Add domain‑specific terms to improve OCR accuracy
        ocrEngine.CustomDictionary = new HashSet<string>
        {
            "Aspose",
            "OCR",
            "SDK",
            "invoice"
        };

        // 3️⃣ Path to your PNG file (adjust as needed)
        string imagePath = @"YOUR_DIRECTORY/invoice.png";

        try
        {
            // 4️⃣ Recognize raw text from the image
            string rawText = ocrEngine.RecognizeImage(imagePath);

            // 5️⃣ Clean up unknown tokens
            string cleanedText = ocrEngine.CleanText(rawText);

            // 6️⃣ Show the result
            Console.WriteLine("=== Cleaned OCR Output ===");
            Console.WriteLine(cleanedText);
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error processing image: {ex.Message}");
        }
    }
}
```

**Várt kimenet** (feltételezve, hogy a PNG egy egyszerű számlát tartalmaz):

```
=== Cleaned OCR Output ===
Invoice #12345
Date: 01/08/2026
Total: $1,250.00
Thank you for your business!
```

Ha idegen szimbólumokat látsz, ellenőrizd a kép minőségét, vagy bővítsd ki az egyedi szótárat további kifejezésekkel.

## Bónusz: Alacsony minőségű beolvasások kezelése

Néha a PNG‑k 72 dpi‑en vannak beolvasva, vagy erős tömörítési artefaktusokkal rendelkeznek. Íme néhány gyors trükk az **OCR pontosságának javításához** C#‑on kívül:

1. **Előfeldolgozás** egy olyan könyvtárral, mint a `SixLabors.ImageSharp` – növeld a kontrasztot, konvertáld szürkeárnyalatosra, vagy alkalmazz enyhe elmosást a zaj csökkentésére.  
2. **Állítsd be a `Resolution` tulajdonságot** az `OcrEngine`‑en (pl. `ocrEngine.Resolution = 300;`) hogy a motor a képet nagyobb felbontásúnak tekintse.  
3. **Engedélyezd a nyelvi csomagokat**, ha nem‑angol szöveggel dolgozol (`ocrEngine.Language = Language.English;`).

Mindhárom megközelítést a `RecognizeImage` hívás előtt hozzáadhatod.

## Gyakran ismételt kérdések

- **Működik ez más képformátumokkal is?**  
  Igen. A `RecognizeImage` elfogadja a JPEG, BMP, TIFF és még a PDF‑et is (képkonténerként). Ugyanazok a lépések érvényesek.

- **Kinyerhetem a szöveget több PNG‑ból egy mappában?**  
  Természetesen. Csomagold a főlogikát egy `foreach (var file in Directory.GetFiles(folder, "*.png"))` ciklusba, és tárold az eredményeket listában vagy külön fájlokba írd őket.

- **Mi van, ha a szöveg koordinátáira is szükségem van?**  
  Az Aspose OCR biztosít `OcrResult` objektumokat, amelyek tartalmazzák a határoló dobozokat. Ehhez használd a `ocrEngine.RecognizeImageToResult(imagePath)` metódust a fejlettebb forgatókönyvekhez.

## Következtetés

Végigvezettünk egy **komplett, vég‑től‑végig** megoldáson a **szöveg kinyerése PNG‑ből** az Aspose OCR segítségével. Az motor inicializálásával, egy **egyedi szótár** hozzáadásával, a nyers kimenet tisztításával és néhány gyakori buktató kezelésével megbízhatóan **olvasni tudod a képen lévő szöveget** és **javíthatod az OCR pontosságát** saját C# alkalmazásaidban.

Készen állsz a következő lépésre? Próbáld ki a PNG‑t egy beolvasott bizonylattal, adj hozzá több domain‑specifikus szót a szótárhoz, vagy integráld a kimenetet egy adatbázissal az automatikus számlafeldolgozáshoz. Az ég a határ, amikor az Aspose OCR‑t a .NET gazdag ökoszisztémájával kombinálod.

Boldog kódolást, és legyen az OCR mindig pontos!

![Extract text from png example](/images/extract-text-from-png.png "extract text from png – Aspose OCR demo")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}