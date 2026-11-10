---
category: general
date: 2026-02-11
description: Tanulja meg, hogyan futtathat OCR-t többoldalas TIFF-fájlon C#-ban az
  Aspose OCR használatával. Konvertálja a TIFF-et szöveggé, nyerjen ki szöveget a
  TIFF-ből, és gyorsan ismerje fel a képről a szöveget.
draft: false
keywords:
- how to run OCR
- recognize text from image
- convert tiff to text
- extract text from tiff
- perform OCR on image
language: hu
og_description: Hogyan futtassunk OCR-t többoldalas TIFF-fájlon az Aspose OCR használatával
  C#-ban. Lépésről lépésre útmutató a TIFF szöveggé konvertálásához, a szöveg kinyeréséhez
  a TIFF-ből, és a kép szövegének felismeréséhez.
og_title: Hogyan futtassunk OCR-t többoldalas TIFF képeken – Teljes C# útmutató
tags:
- OCR
- C#
- Aspose
- TIFF
title: Hogyan hajtsunk végre OCR-t többoldalas TIFF képeken az Aspose OCR segítségével
  – C# útmutató
url: /hu/net/text-recognition/how-to-run-ocr-on-multi-page-tiff-images-with-aspose-ocr-c-g/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan futtassunk OCR-t többoldalas TIFF képeken az Aspose OCR-rel

Gondoltad már, **hogyan futtassunk OCR-t** egy több oldalt tartalmazó beolvasott TIFF-en? Nem vagy egyedül – sok fejlesztő ütközik ebbe a problémába, amikor régi dokumentumokból kereshető szöveget kell kinyerni. A jó hír? Az Aspose OCR-rel néhány C# kódsorral felismerheted a szöveget képfájlokból, és egyszerű, összefűzött szöveget kapsz, amely készen áll az indexelésre vagy további feldolgozásra.

Ebben az útmutatóban végigvezetünk a teljes munkafolyamaton: az Aspose OCR csomag telepítésétől, a többoldalas TIFF betöltéséig, a TIFF szöveggé konvertálásáig, egészen a kinyert tartalom megjelenítéséig. A végére képes leszel **szöveget kinyerni TIFF** fájlokból, **szöveget felismerni képről** forrásokból, és akár automatizálni a folyamatot tucatnyi fájl esetén egy kötegelt feladatban. Nincs varázslat, csak egyértelmű, gyakorlati lépések.

## Mit fogsz megtanulni

- Hogyan állítsuk be az Aspose OCR motorját angol nyelv felismeréséhez.  
- A pontos kód, amely a `OcrEngine` osztály segítségével **convert TIFF to text**-t valósítja meg.  
- Tippek a többoldalas képek kezeléséhez és annak biztosításához, hogy minden oldal helyesen legyen elválasztva.  
- Gyakori buktatók (például hiányzó natív függőségek) és hogyan kerüljük el őket.  

**Prerequisites** – szükséged lesz .NET 6 vagy újabb verzióra, Visual Studio-ra (vagy bármilyen C# szerkesztőre), és internetkapcsolatra az automatikus erőforrásletöltés funkcióhoz. Ennyi; nincs további natív könyvtár, amivel bajlódni kell.

---

## 1. lépés – Aspose OCR NuGet csomag telepítése

Mielőtt **perform OCR on image** fájlokon dolgozhatnál, hozzá kell adnod a könyvtárat a projektedhez.

```bash
dotnet add package Aspose.OCR
```

> **Pro tip:** Ha a Visual Studio-ban dolgozol, jobb‑kattints a projektre → *Manage NuGet Packages* → keresd a “Aspose.OCR” kifejezést, és kattints a *Install* gombra.

A csomag mindent tartalmaz, amire szükséged van, és az `AutomaticResourceDownload = true` beállítással a motor a futás közben letölti a nyelvi csomagokat.

## 2. lépés – OCR motor inicializálása (Hogyan futtassunk OCR-t)

Most, hogy a csomag a helyén van, létrehozzuk és konfiguráljuk az `OcrEngine` példányt. Ez a **how to run OCR** központja a mi esetünkben.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System.Drawing;   // For Image class
using System;

// Step 2: Create and configure the OCR engine
var ocrEngine = new OcrEngine
{
    Language = OcrLanguage.English,          // Recognize English text
    AutomaticResourceDownload = true,        // Auto‑download language data
    OutputFormat = OcrOutputFormat.Text      // Get plain concatenated text
};
```

**Why this matters:** A `Language` beállítása megmondja a motornak, milyen karakterkészletet várjon, míg az `AutomaticResourceDownload` megkímél a nyelvi fájlok kézi elhelyezésétől a szerveren. Az `OutputFormat` `Text` értéke egyszerű karakterláncot ad – tökéletes a **convert TIFF to text** folyamatokhoz.

## 3. lépés – Többoldalas TIFF betöltése (Recognize Text from Image)

Egy TIFF sok keretet (frame-et) tartalmazhat, mindegyik egy oldalt képvisel. A `System.Drawing.Image` osztály ezt számunkra absztrahálja.

```csharp
// Step 3: Load the multi‑page image to be processed
using (var image = Image.FromFile("YOUR_DIRECTORY/multi_page.tiff"))
{
    // Step 4: Run OCR on the image
    var ocrResult = ocrEngine.Recognize(image);

    // Step 5: Display the extracted text
    Console.WriteLine(ocrResult.Text);
}
```

> **Mi van, ha a fájl nem ugyanabban a mappában van?** Adj meg egy teljes abszolút elérési utat, vagy használd a `Path.Combine`-t az `AppContext.BaseDirectory`-vel.  
> **Mi a helyzet a memóriahasználattal?** A `using` utasítás a feldolgozás után felszabadítja a képet, megakadályozva a szivárgásokat – ez kulcsfontosságú, ha tucatnyi nagy TIFF-et dolgozol fel kötegelt módon.

A `Recognize` hívás automatikusan végigiterál a TIFF minden oldalán, és az eredményeket sortörésekkel fűzi össze. Ezért láthatod, hogy minden oldal külön sorban jelenik meg, amikor kiírod az `ocrResult.Text`-et.

## 4. lépés – Teljes működő példa (Minden lépés egy fájlban)

Az alábbiakban egy teljes, azonnal futtatható konzolalkalmazás található. Másold be egy új .NET konzolprojektbe, és nyomd meg a **F5**-öt.

```csharp
// File: Program.cs
using System;
using System.Drawing;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace TiffOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Configure the OCR engine
            var ocrEngine = new OcrEngine
            {
                Language = OcrLanguage.English,
                AutomaticResourceDownload = true,
                OutputFormat = OcrOutputFormat.Text
            };

            // 2️⃣ Load your multi‑page TIFF (replace with your actual path)
            const string tiffPath = @"YOUR_DIRECTORY\multi_page.tiff";

            if (!System.IO.File.Exists(tiffPath))
            {
                Console.WriteLine($"File not found: {tiffPath}");
                return;
            }

            // 3️⃣ Perform OCR
            using (var image = Image.FromFile(tiffPath))
            {
                var result = ocrEngine.Recognize(image);

                // 4️⃣ Output the extracted text
                Console.WriteLine("=== OCR RESULT ===");
                Console.WriteLine(result.Text);
                Console.WriteLine("==================");
            }

            // Keep console open
            Console.WriteLine("Press any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**Várható kimenet** (rövidítve):

```
=== OCR RESULT ===
Page 1: The quick brown fox jumps over the lazy dog.
Page 2: Lorem ipsum dolor sit amet, consectetur adipiscing elit.
...
==================
Press any key to exit...
```

Minden oldal saját sorban jelenik meg, mivel az `OcrOutputFormat.Text` sortörést szúr be a keretek között. Ha más elválasztót szeretnél, a `result.Text`-et a `String.Replace` segítségével utófeldolgozhatod.

## 5. lépés – Gyakori szélsőséges esetek kezelése

### 5.1 Nagy TIFF fájlok  
Gigabájt méretű TIFF-ek esetén a teljes fájl memóriába töltése problémás lehet. Egy megoldás, hogy minden keretet egyenként dolgozunk fel:

```csharp
using (var image = Image.FromFile(tiffPath))
{
    for (int i = 0; i < image.GetFrameCount(FrameDimension.Page); i++)
    {
        image.SelectActiveFrame(FrameDimension.Page, i);
        var pageResult = ocrEngine.Recognize(image);
        Console.WriteLine($"--- Page {i + 1} ---");
        Console.WriteLine(pageResult.Text);
    }
}
```

### 5. Nem angol nyelvű dokumentumok  
Ha **recognize text from image**-t szeretnél spanyol vagy francia nyelven, csak módosítsd a `Language` tulajdonságot:

```csharp
ocrEngine.Language = OcrLanguage.Spanish; // or OcrLanguage.French
```

Az Aspose automatikusan letölti a megfelelő nyelvi erőforrásokat.

### 5. Kimenet mentése  
Gyakran szeretnél **convert TIFF to text**-et, és az eredményt egy `.txt` fájlba menteni:

```csharp
System.IO.File.WriteAllText("output.txt", ocrResult.Text);
```

A kimenetet oldalanként is feloszthatod a `String.Split(Environment.NewLine)` használatával, és minden szeletet külön fájlba írhatod.

## Pro tippek és buktatók

- **AutomaticResourceDownload** az első futtatáskor működik; a későbbi futások offline módban vannak.  
- Ha torz karaktereket látsz, ellenőrizd a `Language` beállítást; a nem megfelelő nyelvi csomagok hibás felismerést okoznak.  
- PDF-ek esetén, amelyeket TIFF-re rasterizáltak, érdemes növelni az `ocrEngine.Dpi` értékét (alapértelmezett 300) a jobb pontosság érdekében.  
- Mindig a `Image.FromFile`-t `using` blokkba tedd; különben a fájl zárolva lesz, és később nem tudod törölni vagy áthelyezni.

## Gyakran ismételt kérdések

**Q: Működik ez egyoldalas TIFF-ekkel is?**  
A: Teljesen. A motor egy egykeretes TIFF-et ugyanúgy kezeli; csak egy sor szöveget kapsz.

**Q: Feldolgozhatok PNG vagy JPEG fájlokat is ugyanígy?**  
A: Igen – csak változtasd meg a fájl kiterjesztését. A `Recognize` metódus bármely `System.Drawing.Image` formátumot elfogad.

**Q: Mi van, ha az OCR eredményt PDF-ként szeretném, nem egyszerű szövegként?**  
A: Állítsd be `OutputFormat = OcrOutputFormat.Pdf`-ra, és az `ocrResult` egy PDF bájt tömböt tartalmaz, amelyet leírhatsz a lemezre.

## Összegzés

Most már egy teljes, vég‑től‑végig megoldással rendelkezel a **how to run OCR** többoldalas TIFF fájlokra az Aspose OCR C#-ban való használatával. A motor konfigurálásával, a kép betöltésével és a `Recognize` meghívásával **szöveget nyerhetsz ki TIFF**-ből, **convert TIFF to text**-t végezhetsz, és **recognize text from image**-t néhány kódsorral. Nyugodtan módosíthatod a nyelvet, a kimeneti formátumot vagy a keret‑enkénti feldolgozást, hogy megfeleljen a saját kötegelt feldolgozási igényeidnek.

Készen állsz a következő lépésre? Próbáld meg kombinálni ezt a megközelítést egy mappa‑figyelő szolgáltatással, hogy automatikusan **perform OCR on image** fájlokat dolgozzon fel, amint azok egy drop mappába kerülnek, vagy integráld a kimenetet egy kereső indexbe a pillanatnyi teljes szöveges kereséshez. A lehetőségek végtelenek, és a most látott kód egy szilárd alapot nyújt.

Ha bármilyen problémába ütköztél, hagyj megjegyzést alább, vagy jelölj meg a GitHub-on. Boldog kódolást, és élvezd, ahogy ezeket a makacs TIFF-eket kereshető szöveggé alakítod!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}