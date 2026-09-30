---
category: general
date: 2026-02-09
description: Szöveges képek gyors kinyerése C#-ban a maximális párhuzamosság beállításával
  kötegelt OCR-hez – tanulja meg a beolvasott oldalak konvertálását, a több képes
  OCR kezelését és a PNG szöveg hatékony olvasását.
draft: false
keywords:
- extract text images
- set max parallelism
- convert scanned pages
- multiple image ocr
- read png text
language: hu
og_description: Képek szövegének kinyerése C#-ban a maximális párhuzamosság beállításával.
  Ez az útmutató bemutatja, hogyan konvertálhatók beolvasott oldalak, futtatható több
  képen OCR, és olvasható a PNG szöveg az Aspose OCR-rel.
og_title: Szöveges képek kinyerése PNG-fájlokból C#-val – Teljes kötegelt OCR útmutató
tags:
- OCR
- C#
- Aspose
- Batch Processing
title: Szöveges képek kinyerése PNG-ekből C#-val – Tömeges OCR az Aspose OCR-rel
url: /hu/net/ocr-optimization/extract-text-images-from-pngs-with-c-batch-ocr-using-aspose/
---

.

Proceed.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# szövegképek kinyerése PNG‑ekből C#‑ban – Tömeges OCR az Aspose OCR segítségével

Valaha is szükséged volt **szövegképek kinyerésére** egy mappában lévő beolvasott PNG‑ekből, de elakadtál a „hogyan tudom gyorsan?” kérdésnél? Nem vagy egyedül. Sok valós projektben a fejlesztőknek **maximális párhuzamosságot kell beállítaniuk**, hogy tucatnyi oldal másodpercek alatt, ne perc alatt legyen feldolgozva.  

Ebben az útmutatóban egy teljes, futtatható példán keresztül mutatjuk be, hogyan **alakítunk át beolvasott oldalakat**, futtatunk **több képes OCR‑t**, és végül **olvassuk ki a png szöveget** gond nélkül. Nincsenek homályos „lásd a dokumentációt” hivatkozások – csak másolható‑beilleszthető kód, magyarázatok arról, miért fontos minden sor, és tippek a gyakori buktatók elkerüléséhez.

> **Pro tipp:** Ha már használod az Aspose OCR‑t máshol, észre fogod venni, hogy ugyanaz a `OcrEngine` osztály jelenik meg itt is, de a valódi párhuzamos feldolgozáshoz finomhangoljuk a konfigurációját.

---

## Amire szükséged lesz

- **.NET 6+** (vagy .NET Framework 4.6+). Az API ugyanúgy működik, de az újabb futtatókörnyezetek jobb szálkezelést biztosítanak.  
- **Aspose.OCR for .NET** – telepítsd a NuGet‑en keresztül: `Install-Package Aspose.OCR`.  
- Egy mappa, amely néhány PNG beolvasást tartalmaz (`page1.png`, `page2.png`, …).  
- Egy IDE vagy szerkesztő, amivel kényelmesen dolgozol (Visual Studio, Rider, VS Code…).

Ennyi. Nincs szükség extra szolgáltatásokra, felhőkulcsokra, csak tiszta helyi feldolgozás.

---

## extract text images – Max párhuzamosság beállítása tömeges OCR‑hez

Amikor több fájlon indítod el az OCR‑t, az motor alapértelmezés szerint egyetlen szálat használ. Ez biztonságos, de fájdalmasan lassú. A `MaxDegreeOfParallelism` beállításával megmondod a motornak, hány szálat indíthat egyszerre.

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.Models;

class BatchExample
{
    static void Main()
    {
        // 1️⃣ Create an OCR engine and allow up to 4 parallel threads
        var ocrEngine = new OcrEngine
        {
            Configuration = { MaxDegreeOfParallelism = 4 }
        };
```

**Miért 4?**  
A négy a legtöbb modern laptopon egy kedvező kiindulópont – elég mag a CPU elfoglalásához, de nem annyira, hogy más folyamatok éhezzenek. Ha szerveren 16 maggal futtatod, növeld a számot 12‑re vagy 14‑re a jelentős gyorsulás érdekében.

---

## Convert scanned pages – Képadatfolyam-gyűjtemény felépítése

Az Aspose minden képet `ImageStream`‑ként vár. A `FromFile` segédfüggvény beolvassa a fájlt, memóriában tartja, és átadja az OCR motornak. Ha a képek adatbázisból vagy HTTP‑válaszból érkeznek, `MemoryStream`‑et is használhatsz.

```csharp
        // 2️⃣ Build a collection of image streams to be processed
        List<ImageStream> imageStreams = new List<ImageStream>
        {
            ImageStream.FromFile(@"YOUR_DIRECTORY/page1.png"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/page2.png"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/page3.png")
        };
```

**Szélső eset:** Ha egy fájl hiányzik vagy sérült, a `FromFile` `FileNotFoundException`‑t dob. Csomagold a konstrukciót `try/catch`‑be, ha megbízhatatlan bemenetet vársz.

---

## multiple image ocr – Tömeges OCR végrehajtása

Most jön a nehéz munka. A `RecognizeBatch` annyi szálat indít, amennyit korábban beállítottál, feldolgozza az egyes képeket, és egy `OcrResult` objektumok listáját adja vissza.

```csharp
        // 3️⃣ Perform batch OCR on the prepared images
        IList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);
```

A háttérben minden szál betölti a saját képét, futtatja a neurális hálót, és kinyeri a sima szöveget. Az eredmények sorrendje megegyezik a bemeneti lista sorrendjével, így biztonságosan leképezheted az 1. oldalt → 0. eredményre, stb.

---

## read png text – Kinyert tartalom megjelenítése

Végül végigiterálunk az eredményeken és kiírjuk a sima szöveget a konzolra. Itt már átirányíthatod a kimenetet fájlba, adatbázisba vagy akár egy downstream NLP szolgáltatásba is.

```csharp
        // 4️⃣ Display the extracted text for each page
        for (int i = 0; i < ocrResults.Count; i++)
        {
            Console.WriteLine($"--- Page {i + 1} ---");
            Console.WriteLine(ocrResults[i].PlainText);
        }
    }
}
```

### Várt konzolkimenet

```
--- Page 1 ---
This is the first scanned line of text.
Another line appears here.

--- Page 2 ---
Second page starts with a header.
More content follows…

--- Page 3 ---
Final page ends with a signature.
```

Ha üres szakaszokat látsz, ellenőrizd, hogy a PNG‑k nem tisztán fehér képek‑e; az OCR‑nek kontrasztra van szüksége.

---

## Gyakorlati tippek és gyakori buktatók

| Helyzet | Mit tegyél |
|-----------|------------|
| **Memória nyomás** nagy kötegek esetén | Dolgozd fel a képeket 10‑20 fájlos darabokban, majd hívd meg a `GC.Collect()`‑t, ha csúcsokat észlelsz. |
| **Helytelen nyelvfelismerés** | Állítsd be a `ocrEngine.Configuration.Language = OcrLanguage.English;`‑t (vagy a célnyelvedet) a `RecognizeBatch` hívása előtt. |
| **Lassú teljesítmény a párhuzamosság ellenére** | Ellenőrizd, hogy az SSD nem korlátozza az I/O‑t; olvasd be először az összes fájlt memóriába (ahogy a `ImageStream.FromFile` teszi). |
| **Hiányzó karakterek** | Növeld a `ocrEngine.Configuration.DPI = 300;` értéket a nagyobb felbontású feldolgozáshoz. |

---

## A példa kibővítése – PNG‑ről PDF‑re vagy DOCX‑re

Ha végül **beolvasott oldalakat** kereshető PDF‑ekbe szeretnéd konvertálni, egyszerűen add át a `ocrResults[i].PlainText`‑et egy PDF könyvtárnak (pl. Aspose.PDF) és helyezd rá a szöveget láthatatlan rétegként. Ugyanez a párhuzamossági trükk ott is működik.

---

## Teljes forráskód (másolás‑beillesztés kész)

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.Models;

class BatchExample
{
    static void Main()
    {
        // Step 1: Create an OCR engine and allow up to 4 parallel threads
        var ocrEngine = new OcrEngine
        {
            Configuration = { MaxDegreeOfParallelism = 4 }
        };

        // Step 2: Build a collection of image streams to be processed
        List<ImageStream> imageStreams = new List<ImageStream>
        {
            ImageStream.FromFile(@"YOUR_DIRECTORY/page1.png"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/page2.png"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/page3.png")
        };

        // Step 3: Perform batch OCR on the prepared images
        IList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);

        // Step 4: Display the extracted text for each page
        for (int i = 0; i < ocrResults.Count; i++)
        {
            Console.WriteLine($"--- Page {i + 1} ---");
            Console.WriteLine(ocrResults[i].PlainText);
        }
    }
}
```

Mentsd el `BatchExample.cs`‑ként, futtasd `dotnet run`‑nal, és nézd, ahogy a konzol megtelik a korábban a PNG‑ekben rejtett szöveggel.

---

## Vizuális összefoglaló

![extract text images example](images/ocr-batch.png){alt="extract text images example"}

A diagram a folyamatot mutatja: **PNG fájlok → ImageStream gyűjtemény → OcrEngine (max párhuzamosság) → OCR eredmények → Konzol / downstream tárolás**.

---

## Következtetés

Most már van egy szilárd, vég‑től‑végig recepted arra, hogyan **szövegképeket nyerj ki** C#‑ban, miközben **maximális párhuzamosságot állítasz be**, **beolvasott oldalakat konvertálsz**, **több képes OCR‑t kezelsz**, és **png szöveget olvasol** hatékonyan. A kód önálló, a magyarázatok lefedik a „hogyan” és a „miért” kérdéseket, a tippek pedig megakadályozzák a gyakori fejfájásokat.

Mi a következő lépés? Próbáld ki a PNG‑lista helyett egy dinamikus `Directory.GetFiles` ciklust, kísérletezz különböző szál számokkal, vagy irányítsd a kimenetet egy kereshető PDF‑be. Ugyanez a minta könnyedén skálázódik több száz oldalra is, alig egy sor extra kóddal.

Van kérdésed vagy egy nehéz szélső eset? Írj egy megjegyzést alul, és jó kódolást kívánok!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}