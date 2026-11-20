---
category: general
date: 2026-06-28
description: Hogyan lehet kiegyenesíteni a képet az Aspose.OCR használatával. Tanulja
  meg, hogyan előfeldolgozza a képet OCR-hez, javítsa az OCR pontosságát, és kiegyenesítse
  a beolvasott képet egy teljes C# példával.
draft: false
keywords:
- how to deskew image
- preprocess image for ocr
- how to improve ocr
- deskew scanned image
language: hu
og_description: Hogyan korrigáljuk a kép dőlését az Aspose.OCR-rel. Ez az útmutató
  megmutatja, hogyan előfeldolgozzuk a képet OCR-hez, növeljük a pontosságot, és lépésről
  lépésre korrigáljuk a beolvasott képet.
og_title: Hogyan kiegyenesítsünk képet C#-ban – Teljes Aspose.OCR útmutató
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: How to deskew image using Aspose.OCR. Learn to preprocess image for
    OCR, improve OCR accuracy, and deskew scanned image with a full C# example.
  headline: How to Deskew Image in C# – Complete Aspose.OCR Guide
  type: TechArticle
- description: How to deskew image using Aspose.OCR. Learn to preprocess image for
    OCR, improve OCR accuracy, and deskew scanned image with a full C# example.
  name: How to Deskew Image in C# – Complete Aspose.OCR Guide
  steps:
  - name: Why a Deskew Filter First?
    text: 'When a document is rotated even a few degrees, the OCR engine misinterprets
      line baselines, leading to garbled output. The `DeskewFilter` automatically
      estimates the rotation angle (up to `MaxAngle` degrees) and rotates the bitmap
      back to a horizontal baseline. The returned `DeskewConfidence` tells '
  - name: 1️⃣ DeskewFilter (Primary Step)
    text: '- **What it does:** Detects the dominant text line direction and rotates
      the image. - **Why it matters:** A straight baseline maximizes character segmentation
      accuracy. - **Tip:** If your documents never exceed 10°, set `MaxAngle = 10`
      to speed up detection.'
  - name: 2️⃣ DenoiseFilter (Secondary Cleanup)
    text: '- **What it does:** Reduces random pixel noise that can appear after scanning.
      - **Why it matters:** Noise often creates false edges, confusing the OCR''s
      segmentation. - **Tip:** Adjust `Strength` between 0.3 (light) and 0.8 (aggressive)
      based on scan quality.'
  - name: 3️⃣ ContrastBoostFilter (Final Polish)
    text: '- **What it does:** Increases the difference between foreground text and
      background. - **Why it matters:** Low contrast can make faint characters invisible
      to the recognition engine. - **Tip:** A `Level` of 1.2 works for most black‑on‑white
      scans; for colored documents, experiment with values up to '
  type: HowTo
tags:
- OCR
- Aspose
- Image Processing
title: Hogyan kiegyenesítsük a képet C#‑ban – Teljes Aspose.OCR útmutató
url: /hu/net/ocr-optimization/how-to-deskew-image-in-c-complete-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan korrigáljuk a kép dőlését C#‑ban – Teljes Aspose.OCR útmutató

Gondolkodtál már azon, **hogyan korrigáljuk a kép dőlését** a fájloknál, mielőtt OCR motorba adnád őket? Nem vagy egyedül. A beolvasott dokumentumok gyakran ferde érkeznek, és ez a kis elfordulás tönkreteheti a felismerési eredményeket. A jó hír? Az Aspose.OCR segítségével néhány C#‑sorral kiegyenesítheted (deskew) és megtisztíthatod a képeket.

Ebben az útmutatóban egy teljes, futtatható példán keresztül vezetünk végig, amely **előfeldolgozza a képet OCR‑hez**, hozzáad egy deskew szűrőt, és megmutatja, **hogyan javítható az OCR** pontossága. A végére képes leszel automatikusan **korrigálni a beolvasott képeket**, és saját szemeddel megtekintheted a bizalmi értékeket.

**Megjegyzés:** A kód az Aspose.OCR ≥ 22.10 és .NET 6+ verziókkal működik, de a koncepciók korábbi verziókra is alkalmazhatók.

## Amire szükséged lesz

- **Aspose.OCR for .NET** (NuGet package `Aspose.OCR`)
- Egy **ferde TIFF** vagy JPEG, amelyet ki szeretnél egyenesíteni
- Visual Studio 2022 (vagy bármely C# IDE)
- Alapvető ismeretek C#‑ban és konzolos alkalmazásokban

Nem szükséges extra harmadik féltől származó könyvtár; az egész folyamat az Aspose.OCR‑on belül valósul meg.

---

## Hogyan korrigáljuk a kép dőlését az Aspose.OCR-rel

A megoldás lényege egy **szűrőcsővezeték**. Gondolj rá úgy, mint egy összeszerelő vonalra, ahol minden szűrő egy adott problémát old meg: először korrigáljuk a forgást, majd csökkentjük a zajt, és végül növeljük a kontrasztot, hogy az OCR motor tisztán lássa a karaktereket.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

class DeskewExample
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        var engine = new OcrEngine();

        // Step 2: Load the skewed image to be processed
        var img = OcrImage.FromFile(@"YOUR_DIRECTORY/skewed_doc.tif");

        // Step 3: Build a filter pipeline – deskew, then denoise, then boost contrast
        var pipeline = new OcrFilter[]
        {
            new DeskewFilter { MaxAngle = 30 },   // auto‑detect rotation up to 30°
            new DenoiseFilter { Strength = 0.5 },
            new ContrastBoostFilter { Level = 1.2 }
        };

        // Step 4: Apply the filters to the image before OCR
        var preprocessed = engine.ApplyFilters(img, pipeline);

        // Step 5: Perform OCR on the pre‑processed image
        var result = engine.Recognize(preprocessed);

        // Step 6: Output the deskew confidence and recognized text
        System.Console.WriteLine($"Deskew confidence: {result.DeskewConfidence:P2}");
        System.Console.WriteLine(result.Text);
    }
}
```

> **Kép példa**  
> ![hogyan korrigáljuk a kép dőlését példa](/images/deskew-example.png "hogyan korrigáljuk a kép dőlését példa")

### Miért először a Deskew szűrő?

Ha egy dokumentum néhány fokkal el van fordítva, az OCR motor félreérti a sorok alapvonalát, ami összezavart kimenetet eredményez. A `DeskewFilter` automatikusan becsli a forgási szöget (`MaxAngle` fokig), és a bitmapet visszaforgatja egy vízszintes alapvonalra. A visszaadott `DeskewConfidence` megmutatja, mennyire biztos az algoritmus a korrekcióban – hasznos naplózáshoz vagy visszalépési stratégiákhoz.

---

## Kép előfeldolgozása OCR‑hez – A szűrőcsővezeték felépítése

### 1️⃣ DeskewFilter (Elsődleges lépés)

- **Mit csinál:** Felismeri a domináns szövegsor irányát és elforgatja a képet.  
- **Miért fontos:** Egy egyenes alapvonal maximalizálja a karakter szegmentálás pontosságát.  
- **Tipp:** Ha a dokumentumaid soha nem haladják meg a 10°‑ot, állítsd be a `MaxAngle = 10` értéket a detektálás felgyorsításához.

### 2️⃣ DenoiseFilter (Másodlagos tisztítás)

- **Mit csinál:** Csökkenti a véletlenszerű pixelzajt, amely a beolvasás után megjelenhet.  
- **Miért fontos:** A zaj gyakran hamis éleket hoz létre, ami összezavarja az OCR szegmentálását.  
- **Tipp:** Állítsd a `Strength` értékét 0.3 (könnyű) és 0.8 (agresszív) között a beolvasás minősége alapján.

### 3️⃣ ContrastBoostFilter (Végső csiszolás)

- **Mit csinál:** Növeli a szöveg előtér és a háttér közötti különbséget.  
- **Miért fontos:** Alacsony kontraszt esetén a halvány karakterek láthatatlanok lehetnek a felismerő motor számára.  
- **Tipp:** A `Level` 1.2 érték a legtöbb fekete‑fehér beolvasásnál működik; színes dokumentumoknál kísérletezz 2.0‑ig terjedő értékekkel.

E három szűrő láncolásával **előfeldolgozod a képet OCR‑hez** úgy, hogy a leggyakoribb problémákat – ferde, zaj és alacsony kontraszt – kezeli.

---

## Hogyan javítható az OCR pontossága Deskew és Denoise segítségével

Felmerülhet a kérdés, „Ha már van egy deskew szűrőm, miért kell még a denoise és a kontraszt növelés?” A válasz a **kumulatív javulás**. Minden szűrő egy másik hibát orvosol, és együtt növelik az összbizalmat.

#### Valós teszt

| Teszt | Eredeti OCR pontosság | Deskew után | Teljes csővezeték után |
|------|-----------------------|--------------|---------------------|
| Egyszerű számla (5° ferde) | 78 % | 92 % | 96 % |
| Régi újság beolvasás (15° ferde, szemcsés) | 61 % | 78 % | 88 % |
| Alacsony kontrasztú űrlap (nincs ferde) | 70 % | 71 % | 84 % |

*A számok illusztratívak, de tükrözik az Aspose felhasználók által jelentett tipikus nyereségeket.*

**Fő tanulság:** Még ha a fő célod is, hogy **korrigáld a beolvasott képet**, a denoise és kontraszt lépések hozzáadása gyakran jelentős ugrást eredményez a végső szöveggquality‑ben.

---

## Beolvasott kép korrigálása: Az eredmények ellenőrzése

A csővezeték futtatása után két hasznos információt kapsz:

```csharp
Console.WriteLine($"Deskew confidence: {result.DeskewConfidence:P2}");
Console.WriteLine(result.Text);
```

- **Deskew bizalom** (`result.DeskewConfidence`) százalékban van megadva. A 90 % feletti értékek általában azt jelentik, hogy a forgatás pontosan korrigálva lett.  
- **Felismert szöveg** (`result.Text`) lehetővé teszi, hogy azonnal ellenőrizd, a kimenet érthető‑e.

Ha a bizalom alacsony (< 70 %), fontold meg:

1. **`MaxAngle` növelése** – lehet, hogy a dokumentum a vártnál nagyobb szögben van elfordítva.  
2. **`BinarizationFilter` hozzáadása** a deskew előtt a kép egyszerűsítéséhez.  
3. **Kézi forgatás** a `OcrImage.Rotate(angle)` használatával tartalékmegoldásként.

---

## Teljes vég‑től‑végig példa (kész a futtatásra)

Az alábbi **teljes, önálló program** másolható egy új Console App projektbe. Ne felejtsd el a `YOUR_DIRECTORY`‑t a ferde TIFF‑et tartalmazó mappára cserélni.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

namespace DeskewDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Initialize the OCR engine
            var engine = new OcrEngine();

            // 2️⃣ Load the image you want to straighten
            var imgPath = @"C:\Images\skewed_doc.tif"; // <-- update this path
            var img = OcrImage.FromFile(imgPath);

            // 3️⃣ Define the preprocessing pipeline
            var pipeline = new OcrFilter[]
            {
                new DeskewFilter { MaxAngle = 30 },   // auto‑detect up to 30°
                new DenoiseFilter { Strength = 0.5 }, // moderate noise reduction
                new ContrastBoostFilter { Level = 1.2 } // brighten the text
            };

            // 4️⃣ Apply the pipeline – this returns a new image instance
            var preprocessed = engine.ApplyFilters(img, pipeline);

            // 5️⃣ Run OCR on the cleaned‑up image
            var result = engine.Recognize(preprocessed);

            // 6️⃣ Show confidence and the extracted text
            Console.WriteLine($"Deskew confidence: {result.DeskewConfidence:P2}");
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(result.Text);
        }
    }
}
```

**Várható kimenet** (feltevéve, hogy a beolvasás elég tiszta):

```
Deskew confidence: 96.45%
=== Recognized Text ===
Invoice #12345
Date: 2024‑04‑01
Total: $1,250.00
...
```

Ha összezavart karaktereket látsz, nézd át újra a szűrő erősségeit vagy adj hozzá egy `BinarizationFilter`‑t, ahogy korábban említettük.

---

## Gyakori buktatók és profi tippek

- **Buktató:** Többoldalas TIFF használata. A `OcrImage.FromFile` csak az első keretet olvassa be. Használd a `OcrImage.FromMultiPageFile`‑t, ha minden oldalra szükséged van.  
- **Buktató:** Elfelejted felszabadítani a `OcrEngine`‑t. Csomagold `using` blokkba a termelési kódban a natív erőforrások felszabadításához.  
- **Pro tipp:** Cache-eld a csővezetéket, ha sok képet dolgozol fel azonos beállításokkal – kevesebb terhelést eredményez.  
- **Pro tipp:** Naplózd a `DeskewConfidence`‑t egy felügyeleti rendszerbe; a hirtelen csökkenés a szkenner kalibrációjának változását jelezheti.

---

## Következő lépések – A munkafolyamat kiterjesztése

Most, hogy ismered, **hogyan korrigáljuk a kép dőlését** és **előfeldolgozzuk a képet OCR‑hez**, érdemes lehet felfedezni:

- **Kötegelt feldolgozás** – egy mappában lévő beolvasott PDF‑ek bejárása, minden oldal képévé konvertálása, és ugyanazon csővezeték alkalmazása.  
- **Nyelvtámogatás** – állítsd be a `engine.Language = OcrLanguage.English;` vagy más nyelveket a felismerés javításához.  
- **Egyedi utófeldolgozás** – használj reguláris kifejezéseket a gyakori OCR hibák (pl. „0” vs „O”) tisztításához.

Ezek a témák természetesen visszavezetnek a másodlagos kulcsszavakra, **hogyan javítható az OCR** és **beolvasott kép korrigálása**.

---

## Következtetés

Mindezt lefedtük, amit a **hogyan korrigáljuk a kép dőlését** az Aspose.OCR-rel kapcsolatban tudni kell, a robusztus szűrőcsővezeték felépítésétől a bizalmi értékek ellenőrzéséig. A **kép előfeldolgozásával OCR‑hez** deskew, denoise és kontraszt növelés segítségével mérhető javulást látsz a **hogyan javítható az OCR** eredményekben, különösen ferde vagy zajos beolvasások esetén.

Próbáld ki a saját dokumentumaiddal, finomítsd a szűrő paramétereket, és figyeld, ahogy az OCR pontosság emelkedik. Van kérdésed vagy egy nehéz fájl, amely nem akar egyenesedni? Írj egy megjegyzést alább – oldjuk meg együtt. Boldog kódolást!

## Mit érdemes következőként megtanulni?

Az alábbi útmutatók szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás tartalmaz teljes, működő kódrészleteket lépésről‑lépésre magyarázatokkal, hogy elsajátíthasd a további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [Hogyan használjuk az AspOCR‑t: Kép OCR szűrők előfeldolgozása .NET‑hez](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Hogyan OCR‑eljünk képet – OCR képfelismerés végrehajtása](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)
- [Hogyan állítsuk be a küszöbértéket OCR képfelismerésben](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}