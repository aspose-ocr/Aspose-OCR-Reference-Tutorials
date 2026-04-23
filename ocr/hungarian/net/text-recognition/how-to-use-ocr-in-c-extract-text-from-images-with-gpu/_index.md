---
category: general
date: 2026-02-13
description: Tanulja meg, hogyan használjon OCR-t C#-ban a képfájlok szövegének kinyeréséhez,
  engedélyezze a GPU-feldolgozást, és gyorsan alakítsa át a beolvasott anyagokat szöveggé.
draft: false
keywords:
- how to use OCR
- extract text from image
- how to extract text
- convert scan to text
- enable gpu processing
language: hu
og_description: Hogyan használjunk OCR-t C#-ban? Ez az útmutató megmutatja, hogyan
  lehet szöveget kinyerni képfájlokból, engedélyezni a GPU feldolgozást, és a beolvasott
  anyagokat szöveggé konvertálni.
og_title: Hogyan használjuk az OCR-t C#-ban – Szöveg kinyerése képekből GPU-val
tags:
- OCR
- C#
- Aspose
- GPU
- Image Processing
title: Hogyan használjunk OCR-t C#‑ban – Szöveg kinyerése képekből GPU‑val
url: /hu/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-images-with-gpu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan használjunk OCR-t C#‑ban – Szöveg kinyerése képekből GPU-val

Valaha is elgondolkodtál már azon, **hogyan használjunk OCR-t**, hogy egy beolvasott dokumentumból könnyedén kinyerjünk szöveget? Nem vagy egyedül – a fejlesztők állandóan azt kérdezik: „Hogyan tudok hatékonyan szöveget kinyerni képfájlokból?” A jó hír, hogy az Aspose.OCR segítségével pontosan ezt megteheted, és még **GPU feldolgozást is engedélyezhetsz**, ami jelentős sebességnövekedést biztosít a támogatott hardveren.

Ebben az útmutatóban végigvezetünk egy teljes, vég‑től‑végig példán, amely megmutatja, **hogyan használjunk OCR-t**, hogyan **nyerjünk ki szöveget képből**, hogyan **alakítsuk át a beolvasást szöveggé**, és mit tegyünk, ha a GPU nem érhető el. A végére egy kész, futtatható C# konzolalkalmazásod lesz, amely kiírja a felismert szöveget, és megmondja, hogy a GPU valóban használatban volt‑e.

## Amire szükséged lesz

- .NET 6 SDK vagy újabb (a kód .NET Core‑ral is működik)  
- Visual Studio 2022 vagy bármely kedvelt szerkesztő  
- Aspose.OCR for .NET csomag (elérhető a NuGet‑en keresztül)  
- Egy nagy felbontású képfájl (pl. `highres_scan.tif`) a teszteléshez  

Nem szükséges bonyolult beállítás – csak néhány NuGet parancs, és már indulhatsz.

## 1. lépés: Aspose.OCR telepítése és a projekt előkészítése

Először is. Be kell hoznod az OCR könyvtárat a projektedbe. Nyiss egy terminált a megoldás mappájában, és futtasd:

```bash
dotnet new console -n OcrDemo
cd OcrDemo
dotnet add package Aspose.OCR
```

Ez létrehoz egy új konzolprojektet **OcrDemo** néven, és hozzáadja az `Aspose.OCR` NuGet csomagot. A könyvtár tartalmazza a `OcrEngine` osztályt, amelyet használni fogunk.

> **Pro tipp:** Ha dedikált GPU‑val rendelkező gépen vagy, győződj meg róla, hogy a legújabb grafikus driver telepítve van; ellenkező esetben a könyvtár automatikusan CPU módra vált vissza.

## 2. lépés: A teljes OCR kód megírása

Most nyisd meg a `Program.cs` fájlt, és cseréld le a tartalmát a következőre. Minden sor meg van kommentálva, hogy lásd, *miért* csináljuk azt, amit csinálunk.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Enums;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣  Create an OCR engine and request GPU processing.
            //    If the GPU isn’t present, Aspose.OCR will silently
            //    switch to CPU mode – no crash, no extra code needed.
            // -------------------------------------------------
            var ocrEngine = new OcrEngine
            {
                ProcessingMode = OcrProcessingMode.Gpu
            };

            // -------------------------------------------------
            // 2️⃣  Define the path to the image you want to process.
            //    Replace the placeholder with the actual file location.
            // -------------------------------------------------
            string imagePath = @"YOUR_DIRECTORY/highres_scan.tif";

            // -------------------------------------------------
            // 3️⃣  Perform the recognition. The method returns an
            //    OcrResult object that contains the extracted text,
            //    confidence scores, and more.
            // -------------------------------------------------
            OcrResult ocrResult = ocrEngine.RecognizeImage(imagePath);

            // -------------------------------------------------
            // 4️⃣  Report whether the GPU was really used.
            //    This is handy for debugging performance issues.
            // -------------------------------------------------
            Console.WriteLine($"GPU used: {ocrEngine.IsGpuEnabled}");

            // -------------------------------------------------
            // 5️⃣  Output the recognized text to the console.
            //    In a real app you might write this to a file,
            //    a database, or feed it into another workflow.
            // -------------------------------------------------
            Console.WriteLine("=== Extracted Text ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

### Miért működik ez

- **ProcessingMode = Gpu** azt mondja a motornak, hogy először a GPU‑t próbálja. A könyvtár elrejti az alacsony szintű CUDA/OpenCL hívásokat, így nem kell saját magadnak kezelni az eszközkörnyezeteket.  
- **IsGpuEnabled** egy logikai érték, amely megerősíti, hogy a GPU út sikeres volt-e. Ha `false`‑t látsz, a motor automatikusan CPU‑ra váltott – nincs ok a pánikra.  
- **RecognizeImage** végzi el a nehéz munkát: betölti a képet, futtatja az OCR modellt, és visszaadja a sima szöveg eredményt. Nincs szükség a bitmap kézi előfeldolgozására, hacsak nincs speciális igényed (pl. dőléskorrekció).

## 3. lépés: Az alkalmazás futtatása és a kimenet ellenőrzése

Fordítsd le és futtasd:

```bash
dotnet run
```

Ha minden helyesen van beállítva, valami ilyesmit fogsz látni:

```
GPU used: True
=== Extracted Text ===
This is the first line of the scanned document.
Here is the second line, and so on…
```

Ha a GPU nem érhető el, az első sor `GPU used: False` lesz, de a kinyert szöveg továbbra is megjelenik – köszönhetően a kifogástalan visszalépésnek.

> **Gyakori kérdés:** *Mi van, ha a képem JPEG, nem TIFF?*  
> A `RecognizeImage` metódus bármely, a .NET `System.Drawing` által támogatott formátumot elfogad (JPEG, PNG, BMP, stb.). Csak változtasd meg a fájlkiterjesztést az `imagePath`‑ben.

## 4. lépés: Opcionális – Beállítások finomhangolása a jobb pontosságért

Aspose.OCR néhány beállítást kínál, amelyeket módosíthatsz:

| Beállítás | Mit csinál | Mikor használjuk |
|-----------|------------|-------------------|
| `ocrEngine.Language` | Egy adott nyelvet kényszerít (pl. `OcrLanguage.English`) | Ha ismered a dokumentum nyelvét |
| `ocrEngine.PageSegMode` | Szabályozza, hogyan osztja a motor az oldalakat blokkokra | Többoszlopos elrendezéseknél |
| `ocrEngine.DetectOrientation` | Automatikusan elforgatja a nem függőleges szöveget | Olyan beolvasásoknál, amelyek fejjel lefelé lehetnek |

Beállíthatod ezeket a tulajdonságokat a `RecognizeImage` hívása előtt. Például:

```csharp
ocrEngine.Language = OcrLanguage.English;
ocrEngine.DetectOrientation = true;
```

## 5. lépés: A folyamat vizualizálása (Kép alt szöveggel)

Az alábbi egyszerű diagram szemlélteti, **hogyan használjunk OCR-t** opcionális GPU gyorsítással. Nem szükséges a kód futtatásához, de segít átlátni a nagy képet.

![Diagram, amely bemutatja, hogyan használjunk OCR-t GPU feldolgozással](/images/ocr-gpu-flow.png)

*Alt szöveg:* *Diagram, amely bemutatja, hogyan használjunk OCR-t GPU feldolgozással, kiemelve a CPU-ra való visszalépést, ha szükséges.*

## Szélsőséges esetek és hibaelhárítás

1. **Out‑of‑Memory a GPU‑n** – Nagyon nagy képek meghaladhatják a GPU memória kapacitását. Ebben az esetben a könyvtár automatikusan visszatér a CPU‑ra. Előzetesen átméretezheted a képet, hogy alacsony maradjon a memóriahasználat.  
2. **Nem támogatott képfájl formátum** – Ha a `RecognizeImage` *NotSupportedException*-t dob, ellenőrizd a fájlkiterjesztést, és győződj meg róla, hogy a kép nem sérült. PNG‑re konvertálás gyakran megoldja a problémát.  
3. **Alacsony bizalmi pontszámok** – Ha az OCR eredmény sok olvashatatlan karaktert tartalmaz, fontold meg az előfeldolgozást (binarizálás, zajszűrés) vagy válts nagyobb felbontású beolvasásra.  

## Összegzés: Mit értünk el

Most bemutattuk, **hogyan használjunk OCR-t** egy C# konzolalkalmazásban, megmutattuk, hogyan **nyerjünk ki szöveget képfájlokból**, és azt, hogyan **engedélyezzük a GPU feldolgozást** a gyorsabb eredményekért. Most már tudod, hogyan **alakítsd át a beolvasást szöveggé**, ellenőrizheted, hogy a GPU valóban használatban volt‑e, és finomhangolhatsz néhány beállítást a szélsőséges esetekhez.

### Következő lépések

- Próbáld meg a kimenetet egy **kereső indexbe** (pl. Elasticsearch) betáplálni, hogy a beolvasott PDF‑ek kereshetők legyenek.  
- Kísérletezz **kötegelt feldolgozással** – iterálj egy képmappán, és írd az eredményt egy `.txt` fájlba.  
- Az OCR-t kombináld **fordítási API‑kkal**, hogy automatikusan lefordítsd a beolvasott, idegen nyelvű dokumentumokat.  

További kérdésed van? Hagyj egy megjegyzést, és jó kódolást!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}