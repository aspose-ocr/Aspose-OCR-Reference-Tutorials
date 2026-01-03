---
category: general
date: 2026-01-02
description: Tanulja meg, hogyan ismerje fel a kínai szöveget, és hogyan nyerjen ki
  szöveget PNG‑fájlokból offline szövegfelismeréssel az Aspose.OCR segítségével. Internetkapcsolat
  nélkül – néhány lépésben végezhet OCR‑t a képen.
draft: false
keywords:
- recognize chinese text
- extract text from png
- offline text recognition
- perform OCR on image
language: hu
og_description: Ismerje fel a kínai szöveget internetkapcsolat nélkül. Ez az útmutató
  bemutatja, hogyan lehet PNG-fájlból szöveget kinyerni offline szövegfelismeréssel,
  és OCR-t végezni a képen C#-ban.
og_title: Kínai szöveg felismerése offline – Lépésről‑lépésre C# útmutató
tags:
- OCR
- C#
- Aspose
title: kínai szöveg felismerése offline – Teljes C# OCR útmutató
url: /hu/net/text-recognition/recognize-chinese-text-offline-complete-c-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# kínai szöveg felismerése offline – Teljes C# OCR útmutató

Volt már szükséged **kínai szöveg felismerésére** egy beolvasott PNG‑ről, de az alkalmazásod egy internetkapcsolat nélküli gépen fut? Nem vagy egyedül. Sok vállalati helyzetben—gondolj a levegővel elzárt szerverekre vagy a terepi eszközökre—a felhőszolgáltatásokra támaszkodni egyszerűen nem lehetséges.  

Ebben az útmutatóban egy önálló megoldáson vezetünk végig, amely lehetővé teszi, hogy **szöveget nyerj ki png** fájlokból, **offline szövegfelismerést** hajts végre, és **OCR‑t alkalmazz képeszközökre** az Aspose.OCR segítségével. A végére egy azonnal futtatható C# konzolprogramod lesz, amely a kínai karaktereket közvetlenül a konzolra írja.

## Előfeltételek

- .NET 6 SDK (vagy bármely friss .NET verzió) helyileg telepítve.  
- Visual Studio 2022 vagy VS Code – attól függően, melyiket kedveled.  
- Az Aspose.OCR for .NET NuGet csomag egy példánya (`Aspose.OCR`).  
- Az angol és egyszerű kínai nyelvi erőforrásfájlok (az útmutató bemutatja, hogyan tölthetők le automatikusan).  
- Egy `chinese_doc.png` nevű kép, amelyet egy olyan mappában helyezel el, amelyre hivatkozhatsz (`YOUR_DIRECTORY` helyőrző).

Nincs szükség további szolgáltatásokra, API kulcsokra—csak egy helyi DLL-re és néhány erőforrásfájlra.

---

## 1. lépés – A szükséges nyelvi erőforrások letöltése (egyszer)

Az Aspose.OCR a nyelvi csomagokat lemezen tárolja. Az alkalmazás első futtatásakor le kell tölteni őket. A `ResourceManager.DownloadResources` hívás pontosan ezt teszi, és mivel az angolt és az egyszerű kínait is megadjuk, a motor később hálózati forgalom nélkül tud közöttük váltani.

```csharp
using Aspose.OCR;

// Download English and Simplified Chinese language packs (run once)
ResourceManager.DownloadResources(Language.English, Language.ChineseSimplified);
```

> **Pro tipp:** Tartsd a letöltött mappát (`Aspose.OCR.Resources`) verziókezelés alatt, ha több gépen is reprodukálható buildeket szeretnél.

## 2. lépés – Az OCR motor inicializálása offline módban

Az `OfflineMode = true` beállítás azt mondja a könyvtárnak, hogy kerüljön el minden HTTP hívást. Ez a kulcsa a valódi **offline szövegfelismerésnek**.

```csharp
// Initialise the OCR engine for offline use
var ocrEngine = new OcrEngine()
{
    OfflineMode = true   // Guarantees no network traffic
};
```

> **Miért fontos:** Néhány OCR könyvtár a hiányzó nyelvi csomag esetén felhőszolgáltatásokra támaszkodik. Az offline mód kényszerítésével biztosítjuk a determinisztikus teljesítményt és a adatvédelmi szabályoknak való megfelelést.

## 3. lépés – A feldolgozni kívánt PNG betöltése

A képet a `System.Drawing.Bitmap` segítségével olvassuk be. Ha a projekt .NET 6+ verziót céloz meg nem‑Windows platformokon, fontold meg a `SkiaSharp` használatát alternatívaként, de a legtöbb Windows‑központú környezetben a `Bitmap` megfelelően működik.

```csharp
using System.Drawing;

// Load the PNG that contains Chinese characters
var imagePath = @"YOUR_DIRECTORY\chinese_doc.png";
var image = new Bitmap(imagePath);
```

> **Különleges eset:** Ha a PNG nagyon nagy (több mint 5 MP), érdemes először lecsökkenteni a felbontását a felismerés felgyorsítása és a memóriahasználat csökkentése érdekében:

```csharp
// Optional downscale for huge images
if (image.Width * image.Height > 5_000_000)
{
    var scaled = new Bitmap(image, new Size(image.Width / 2, image.Height / 2));
    image.Dispose();
    image = scaled;
}
```

## 4. lépés – A felismerés futtatása egyszerű kínai nyelven

Itt pontosan megadjuk a motor számára, hogy melyik nyelvet használja. A `RecognitionOptions` objektum lehetővé teszi olyan beállítások finomhangolását, mint a `DetectOrientation` vagy a `PreserveFormatting`, de az alapértelmezések a legtöbb nyomtatott dokumentumnál jól működnek.

```csharp
using Aspose.OCR;

// Perform OCR using Simplified Chinese language pack
var ocrResult = ocrEngine.Recognize(image, new RecognitionOptions
{
    Language = Language.ChineseSimplified
});
```

## 5. lépés – A kinyert szöveg megjelenítése (vagy további feldolgozása)

Az `OcrResult.Text` tulajdonság tartalmazza a sima szöveges ábrázolást. Kiírhatod a konzolra, egy fájlba, vagy továbbíthatod egy későbbi NLP csővezetékbe.

```csharp
// Output the recognized Chinese text to the console
Console.WriteLine("=== Recognized Chinese Text ===");
Console.WriteLine(ocrResult.Text);
```

### Várható kimenet

Ha a `chinese_doc.png` a „你好，世界！” kifejezést tartalmazza, a konzol a következőt fogja megjeleníteni:

```
=== Recognized Chinese Text ===
你好，世界！
```

> **Megjegyzés:** Az OCR pontossága a kép minőségétől, a betűk tisztaságától és a kontraszttól függ. A legjobb eredmény érdekében használj magas felbontású szkenneléseket (300 dpi vagy nagyobb) és győződj meg róla, hogy a szöveg nincs elferdítve.

---

## Teljes működő példa

Az alábbiakban a teljes, másolás‑beillesztésre kész program található. Mentsd el `Program.cs` néven egy új konzolprojektben, és futtasd a `dotnet run` parancsot. Minden lépés egyben van, így láthatod a folyamatot a erőforrás letöltésétől a végső kimenetig.

```csharp
// Program.cs
using Aspose.OCR;
using System;
using System.Drawing;

class OfflineExample
{
    static void Main()
    {
        // 1️⃣ Download language resources (only needed once)
        ResourceManager.DownloadResources(Language.English, Language.ChineseSimplified);

        // 2️⃣ Initialise OCR engine in offline mode
        var ocrEngine = new OcrEngine()
        {
            OfflineMode = true
        };

        // 3️⃣ Load the PNG image
        var imagePath = @"YOUR_DIRECTORY\chinese_doc.png";
        using var image = new Bitmap(imagePath);

        // 4️⃣ Recognise Simplified Chinese text
        var ocrResult = ocrEngine.Recognize(image, new RecognitionOptions
        {
            Language = Language.ChineseSimplified
        });

        // 5️⃣ Print the result
        Console.WriteLine("=== Recognized Chinese Text ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

> **Tipp:** Tedd a `ResourceManager.DownloadResources` hívást egy `try/catch` blokkba, ha szeretnél elegáns kezelést, amikor az internet valóban nem elérhető. Ellenkező esetben a metódus `NetworkException`-t dob.

---

## Gyakran Ismételt Kérdések (GYIK)

| Kérdés | Válasz |
|----------|--------|
| **Felismerhetek hagyományos kínait?** | Igen—cseréld le a `Language.ChineseSimplified`-t `Language.ChineseTraditional`-ra, és töltsd le a megfelelő csomagot. |
| **Mi van, ha JPEG‑ből kell szöveget kinyerni PNG helyett?** | Ugyanaz a kód működik; csak módosítsd a fájlkiterjesztést. A `Bitmap` a legtöbb általános raszteres formátumot támogatja. |
| **Van mód arra, hogy minden karakterhez kereteket (bounding box) kapjak?** | Állítsd be a `RecognitionOptions.DetectRegions = true` értéket. Az `OcrResult` ekkor `Region` objektumokat tartalmaz majd koordinátákkal. |
| **Hogyan futtathatom ezt Linuxon?** | Használd a `System.Drawing.Common` csomagot (1.0+). Fej nélküli Linuxon szükség lehet a `libgdiplus` natív függőségre. |
| **Feldolgozhatok egy mappában lévő képeket kötegelt módon?** | Természetesen—csomagold a felismerési logikát egy `foreach (var file in Directory.GetFiles(folder, "*.png"))` ciklusba. |

---

## Következő lépések és kapcsolódó témák

- **Pontosság javítása**: kísérletezz a `RecognitionOptions.PreprocessImage = true` beállítással, hogy a motor automatikusan javítsa a kontrasztot.  
- **Nyelvek kombinálása**: átadhatsz egy nyelvtömböt a `ResourceManager.DownloadResources`‑nek, és a motor automatikusan felismeri.  
- **Integrálás UI‑val**: helyezd a konzolos kódot egy WinForms vagy WPF alkalmazásba, és jelenítsd meg az OCR eredményt egy szövegmezőben.  
- **Fedezd fel az egyéb Aspose könyvtárakat**: `Aspose.PDF` PDF generáláshoz, `Aspose.Slides` diák automatizálásához, stb.  

Ha más képformátumokból szeretnél szöveget kinyerni, ugyanaz a minta alkalmazható—csak cseréld ki a fájl útvonalát, és szükség esetén állítsd be a előfeldolgozási beállításokat. Boldog kódolást!

---

![recognize chinese text example](/images/recognize-chinese-text.png "Screenshot showing recognize chinese text output in console")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}