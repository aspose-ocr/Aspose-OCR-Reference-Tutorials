---
category: general
date: 2026-02-28
description: Készíts kereshető PDF-et C#-ban képek függőleges összekapcsolásával.
  Tanulja meg, hogyan lehet a képeket függőlegesen egymásra helyezni, és a beolvasott
  oldalak PDF-jét átalakítani az Aspose OCR-rel.
draft: false
keywords:
- create searchable pdf
- combine images vertically
- how to stack images vertically
- convert scanned pages pdf
language: hu
og_description: Kereshető PDF létrehozása C#-ban képek függőleges kombinálásával.
  Ez az útmutató bemutatja, hogyan lehet képeket függőlegesen egymásra helyezni, és
  hogyan konvertálhatók a beolvasott oldalak PDF-re az Aspose OCR segítségével.
og_title: Kereshető PDF létrehozása C#-ban – Képek függőleges egyesítése
tags:
- Aspose OCR
- C#
- PDF generation
title: Kereshető PDF létrehozása C#-ban – Képek függőleges egyesítése
url: /hu/net/text-recognition/create-searchable-pdf-in-c-combine-images-vertically/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kereshető PDF létrehozása C#‑ban – Képek függőleges egyesítése

Valaha is szükséged volt **kereshető PDF** létrehozására néhány beolvasott PNG‑ből, de nem tudtad, hol kezdjed? Nem vagy egyedül. Sok dokumentum‑automatizálási projektben a legnagyobb gond az, hogy egy halom képfájlt egy rendezett, kereshető PDF‑vé alakítsunk, amelyet indexelhetsz és megoszthatsz.  

Ebben az útmutatóban egy teljes, azonnal futtatható példán keresztül vezetünk végig, amely megmutatja, hogyan **rakj egymásra képeket függőlegesen**, **egyesíts képeket függőlegesen**, és végül hogyan **konvertáld a beolvasott oldalak PDF‑jét** egyetlen kereshető dokumentummá az Aspose.OCR GPU‑gyorsított motorjával. A végére egy önálló programod lesz, amelyet bármely .NET megoldásba beilleszthetsz.

> **Mit fogsz megtanulni**
> - OCR motor inicializálása GPU támogatással.
> - Képek kötegének párhuzamos feldolgozása.
> - **Képek függőleges egyesítése** többoldalas beolvasás utánzásához.
> - Kereshető PDF és részletes JSON jelentés exportálása az utólagos elemzéshez.

## Előfeltételek

- .NET 6+ (a kód .NET 6, .NET 7 vagy .NET 8 alatt fordul)
- Aspose.OCR NuGet csomag (`Install-Package Aspose.OCR`)
- GPU‑támogatott gép, ha meg akarod tartani a `ProcessingMode.Gpu` beállítást (CPU tartalék is működik)
- Mappa néhány beolvasott PNG/JPEG fájllal (a demó `page1.png`, `page2.png`, `page3.png` fájlokat használ)

Nincsenek külső szolgáltatások, rejtett konfigurációs fájlok – csak tiszta C#.

## 1. lépés – OCR motor beállítása **kereshető PDF** létrehozásához

Először létrehozunk egy `OcrEngine`‑t, bekapcsoljuk a GPU gyorsítást, angolt választunk nyelvként, és hozzáadunk néhány előfeldolgozó szűrőt. Ezek a szűrők javítják a pontosságot a ferde oldalak kiegyenesítésével (`DeskewFilter`) és a zaj eltávolításával (`DenoiseFilter`).

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;
using System.Collections.Generic;
using System.Drawing;

class AllInOneDemo
{
    static void Main()
    {
        // Initialize OCR engine – this is the heart of creating a searchable PDF
        var ocrEngine = new OcrEngine
        {
            ProcessingMode = ProcessingMode.Gpu,   // Switch to CPU if no GPU
            Language = OcrLanguage.English
        };
        // Pre‑processing improves OCR quality
        ocrEngine.Filters.Add(new DeskewFilter());
        ocrEngine.Filters.Add(new DenoiseFilter());
```

**Miért fontos:** Az OCR motor végzi a szövegfelismerés nehéz munkáját. A `ProcessingMode.Gpu` engedélyezése felére csökkentheti a felismerési időt egy modern grafikus kártyán, míg a szűrők csökkentik a gyakori beolvasási hibákat, amelyek egyébként torz kimenetet eredményeznének.

## 2. lépés – Kötegfeldolgozó konfigurálása a **beolvasott oldalak PDF** hatékony konvertálásához

Az egyes oldalak egyesével történő feldolgozása néhány kép esetén rendben van, de a valós projektek gyakran tucatnyi vagy akár több száz oldalt is érintenek. Az Aspose.OCR `OcrBatchProcessor` lehetővé teszi a felismerések párhuzamos futtatását, drámaian felgyorsítva a **beolvasott oldalak pdf** konvertálási lépést.

```csharp
        // Set up batch processor – ideal for converting many scanned pages to PDF
        var batchProcessor = new OcrBatchProcessor
        {
            MaxDegreeOfParallelism = 2,          // Adjust based on CPU/GPU cores
            Language = OcrLanguage.English,
            ProcessingMode = ProcessingMode.Gpu
        };

        // List the image files you want to turn into a searchable PDF
        List<string> imageFiles = new()
        {
            "YOUR_DIRECTORY/page1.png",
            "YOUR_DIRECTORY/page2.png",
            "YOUR_DIRECTORY/page3.png"
        };
```

**Pro tipp:** Ha csak CPU‑val rendelkező gépen vagy, állítsd be a `ProcessingMode = ProcessingMode.Cpu` értéket. A kötegfeldolgozó továbbra is figyelembe veszi a `MaxDegreeOfParallelism` beállítást, így finomhangolhatod, hogy elkerüld a gép túlterhelését.

## 3. lépés – OCR futtatása a kötegen és az eredmények összegyűjtése

Most ténylegesen felismerjük a szöveget. A `Recognize` metódus egy `OcrResult` objektumok listáját adja vissza, amelyek mindegyike tartalmazza az eredeti képet és a kinyert szöveget.

```csharp
        // Run OCR on all images at once
        List<OcrResult> ocrResults = batchProcessor.Recognize(imageFiles);
```

Ekkor már minden megvan, ami szükséges a **kereshető PDF** létrehozásához: a képek (még memóriában) és a hozzájuk tartozó szövegrétegek.

## 4. lépés – **Képek függőleges egyesítése** és a kereshető PDF generálása

A legtöbb beolvasott dokumentum többoldalas PDF, ezért össze kell varrni az egyes oldalképeket egy magas képpé, amely egy fizikai halmot tükröz. Az Aspose.OCR pontosan erre a célra biztosítja a `Image.CombineVertical`‑t.

```csharp
        // Stitch the page images into one tall image – this is how we **combine images vertically**
        using var combinedImage = Image.CombineVertical(
            ocrResults.ConvertAll(r => r.Image));

        // Finally, create a searchable PDF from the combined image
        ocrEngine.RecognizeToPdf(combinedImage, "YOUR_DIRECTORY/combined_searchable.pdf");
```

Az eredményül kapott fájl (`combined_searchable.pdf`) minden oldalkép alatt kiválasztható, kereshető szöveget tartalmaz – pontosan ez kell a beolvasott forrásokból **kereshető PDF** létrehozásához.

![Kereshető PDF példa](/images/create-searchable-pdf.png "kereshető pdf példa")

*Kép alternatív szövege: kereshető pdf példa, amely egy kombinált PDF‑et mutat kereshető szöveggel.*

**Miért függőleges egymásra helyezés?** Sok OCR könyvtár minden képet külön oldalként kezel. Az egymásra helyezéssel megőrizhetjük a PDF oldal sorrendjét, miközben egyetlen OCR átfutást használunk a teljes dokumentumra.

## 5. lépés – Részletes JSON exportálása az első oldalhoz (hasznos az utólagos munkafolyamatokhoz)

Néha többre van szükség, mint egy PDF; lehet, hogy az OCR adatokat egy adatbázisba vagy gépi tanulási folyamatba szeretnéd betáplálni. Az Aspose.OCR lehetővé teszi, hogy minden `OcrResult`‑ot JSON‑ba sorosíts, megőrizve a határoló dobozokat, a megbízhatósági pontszámokat és egyebeket.

```csharp
        // Dump the first page’s OCR result to pretty‑printed JSON
        string jsonOutput = ocrResults[0].ToJson(prettyPrint: true);
        Console.WriteLine("--- JSON for first page ---");
        Console.WriteLine(jsonOutput);
    }
}
```

**Várható JSON részlet (csonkítva):**

```json
{
  "Text": "Sample scanned text …",
  "Confidence": 0.97,
  "Blocks": [
    {
      "Text": "Header",
      "BoundingBox": { "X": 15, "Y": 10, "Width": 480, "Height": 30 }
    }
    // …
  ]
}
```

Most már ezt a JSON‑t bármely utólagos rendszerbe betáplálhatod – legyen szó a szöveg Elasticsearch‑ben való indexeléséről vagy egy egyedi analitikai irányítópultba való betáplálásról.

---

## Hogyan **Rakj képeket függőlegesen** – Gyors összefoglaló

Ha azon gondolkodsz, **hogyan rakj képeket függőlegesen** Aspose nélkül, használhatod a `System.Drawing`‑ot egy új bitmap létrehozásához, és minden oldalt egymás után rajzolhatsz. Azonban az Aspose beépített `Image.CombineVertical` kezeli a DPI‑t, a pixel formátumot és a memória kezelést, így a legmegbízhatóbb választás a produkciós kódban.

### Alternatíva: `System.Drawing` használata (csak a kíváncsiság kedvéért)

```csharp
int totalHeight = 0;
int maxWidth = 0;
foreach (var img in ocrResults)
{
    totalHeight += img.Image.Height;
    maxWidth = Math.Max(maxWidth, img.Image.Width);
}
var canvas = new Bitmap(maxWidth, totalHeight);
using var g = Graphics.FromImage(canvas);
int offset = 0;
foreach (var img in ocrResults)
{
    g.DrawImage(img.Image, 0, offset);
    offset += img.Image.Height;
}
canvas.Save("combined_manual.png");
```

A kézi megközelítés működik, de elveszíted az automatikus DPI kezelés kényelmét és a lehetőséget, hogy közvetlenül a `RecognizeToPdf`‑ba visszatápláld az eredményt. Maradj a `CombineVertical`‑nél, hacsak nincs nagyon specifikus igényed.

## Gyakori buktatók és hogyan kerüld el őket

| Probléma | Miért fordul elő | Megoldás |
|----------|------------------|----------|
| **Memóriahiányos hibák** amikor tucatnyi nagy felbontású beolvasást dolgozol fel | Minden kép a PDF írásáig a memóriában marad | `Image` objektumok azonnali eldobása (`using` blokkok) a használat után, vagy a képek méretezése kisebbre az egyesítés előtt |
| **Rossz szöveg** az OCR után | Ferdes beolvasások vagy alacsony kontraszt | Tartsd meg a `DeskewFilter` és `DenoiseFilter` szűrőket; szükség esetén fontold meg a `ContrastFilter` hozzáadását |
| **Hiányzó kereshető réteg** | `Recognize` használata `RecognizeToPdf` helyett | Győződj meg róla, hogy a kombinált képen meghívod a `ocrEngine.RecognizeToPdf`‑t |
| **GPU tartalék sikertelen** a megfelelő illesztőprogramok nélküli gépeken | `ProcessingMode.Gpu` kivételt dob | Tekerj egy try/catch‑et a motor létrehozása köré, és térj vissza `ProcessingMode.Cpu`‑ra |

## Következő lépések – A munkafolyamat kibővítése

Most, hogy tudod, hogyan **kereshető PDF**-et készíts, lehet, hogy szeretnél:

- **Kötegelt feldolgozás teljes mappákról** a `Directory.GetFiles` és egy `foreach` ciklus használatával.
- **Vízjelek hozzáadása** minden oldalhoz az egyesítés előtt (használd az `ImageProcessor`‑t az Aspose.Imaging‑ből).
- **A kereshető PDF visszaosztása egyes oldalakra** ha később oldalankénti PDF‑re van szükséged (`PdfDocument.Split` az Aspose.PDF‑ből).
- **Integráció Azure Blob Storage‑szal** a képek felhőből való lekéréséhez és a végleges PDF visszaküldéséhez.

Mindezek a kiterjesztések természetesen ugyanazokat az alapfogalmakat érintik: OCR beállítás, képfeldolgozás és PDF export.

---

## Összegzés

Mindezt lefedtük, ami szükséges a **kereshető PDF** létrehozásához beolvasott képek gyűjteményéből C#‑ban. Egy GPU‑támogatott `OcrEngine` inicializálásával, egy párhuzamos köteg futtatásával az `OcrBatchProcessor`‑rel, **képek függőleges egyesítésével**, és végül a `RecognizeToPdf` meghívásával egy rendezett, kereshető dokumentumot kapsz, amely készen áll az archiválásra vagy indexelésre. A kiegészítő JSON export teljes betekintést nyújt az OCR eredményekbe, lehetőséget teremtve az analitikához vagy egyedi munkafolyamatokhoz.

Próbáld ki, kísérletezz különböző szűrőkkel, és figyeld, ahogy a dokumentum‑automatizálási folyamat sokkal simábbá válik. Ha bármilyen furcsasággal találkozol, írj egy megjegyzést – jó kódolást!

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}