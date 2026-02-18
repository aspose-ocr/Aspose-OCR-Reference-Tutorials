---
category: general
date: 2026-02-17
description: Hogyan végezzünk kötegelt OCR-t több PDF-en és képen C#-ban az Aspose
  OCR használatával. Tanulja meg, hogyan nyerjen ki szöveget PDF-ből, konvertálja
  a PDF-et szöveggé, és ismerje fel a szöveget képekről.
draft: false
keywords:
- how to batch OCR
- extract text from pdf
- convert pdf to text
- recognize text from images
- extract text scanned pdf
language: hu
og_description: Hogyan végezzünk kötegelt OCR-t több dokumentumon C#-ban az Aspose
  OCR segítségével. Szerezzen lépésről‑lépésre kódot a szöveg kinyeréséhez PDF‑ből,
  a PDF szöveggé konvertálásához, és a szöveg felismeréséhez képekről.
og_title: Hogyan végezzünk kötegelt OCR-feldolgozást C#-ban – Teljes útmutató
tags:
- OCR
- C#
- Aspose
- PDF
- Text Extraction
title: Hogyan hajtsunk végre kötegelt OCR-t C#-ban – Teljes kódrészlet
url: /hu/net/text-recognition/how-to-batch-ocr-files-in-c-full-code-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan kötegelt OCR-t végezzünk fájlokon C#-ban – Teljes útmutató

Gondolkodtál már azon, **hogyan kötegelt OCR-t** végezz egy csomó PDF-en és képszkennelésen anélkül, hogy minden fájlhoz külön ciklust írnál? Nem vagy egyedül. A legtöbb fejlesztő erre a problémára fut bele, amikor egyszerre szeretne szöveget kinyerni tucatnyi oldalról. A jó hír? Az Aspose OCR segítségével egy gyűjteményt adhatunk egyetlen motorba, és az elvégzi a nehéz munkát.

Ebben az útmutatóban egy gyakorlati megoldáson vezetünk végig, amely lehetővé teszi, hogy **extract text from pdf**, **convert pdf to text**, és **recognize text from images** egyetlen kötegelt futtatásban. A végére egy azonnal futtatható konzolalkalmazást kapsz, amely minden oldal OCR-eredményét kiírja, és megérted az egyes lépések mögötti okokat, hogy saját projektjeidhez is adaptálhasd.

## Előfeltételek – Amire szükséged van, mielőtt elkezded

- **.NET 6.0 vagy újabb** (a kód .NET Frameworkön is működik, de a .NET 6+ ajánlott)
- **Aspose.OCR NuGet csomag** – telepítsd a `dotnet add package Aspose.OCR` paranccsal
- Néhány mintafájl: egy többoldalas PDF (`doc1.pdf`) és egy beolvasott TIFF (`doc2.tif`). Helyezd őket egy mappába, amelyre hivatkozhatsz, például `C:\OCRSamples`.
- Alap C# ismeretek – kényelmesen kell tudnod a `using` utasításokat és a gyűjteményeket.

> Pro tipp: Ha nincs licenced, az Aspose ingyenes ideiglenes kulcsot kínál, amely a fejlesztés során eltávolítja a 100 oldalas korlátot.

## 1. lépés: A projekt beállítása és a névterek importálása

Először hozz létre egy új konzolprojektet (vagy adj hozzá egy meglévőhöz), és importáld a szükséges névtereket.

```csharp
// Program.cs
using System;
using System.Collections.Generic;
using Aspose.OCR;          // Aspose OCR core library
using Aspose.OCR.Image;   // ImageStream helper class
```

> **Miért fontos:** Az `Aspose.OCR.Image` importálása biztosítja a kényelmes `ImageStream.FromFile` metódust, amely automatikusan szétválasztja a PDF oldalakat külön képes áramlásokra. Ez a titkos összetevő, amely a kötegelt feldolgozást fájdalommentessé teszi.

## 2. lépés: Az OCR motor inicializálása

A motor a munkagép, amely a háttérben lévő OCR motorral kommunikál. A teljes köteghez csak egy példányra van szükség.

```csharp
// Step 2: Create a single OcrEngine instance
OcrEngine ocrEngine = new OcrEngine();
```

> **Magyarázat:** Ugyanannak a `OcrEngine`-nek az újrahasználata csökkenti a memóriaforgalmat és felgyorsítja a feldolgozást, mivel a natív könyvtárak az oldalak között betöltve maradnak.

## 3. lépés: Képes áramlások listájának felépítése

Itt gyűjtjük össze az összes feldolgozni kívánt dokumentumot. Az `ImageStream.FromFile` elég okos ahhoz, hogy egy PDF-et egyes oldalakra bontson, így egy háromoldalas PDF három külön áramlássá válik a háttérben.

```csharp
// Step 3: Assemble the collection of image streams
List<ImageStream> imageStreams = new List<ImageStream>
{
    ImageStream.FromFile(@"C:\OCRSamples\doc1.pdf"),
    ImageStream.FromFile(@"C:\OCRSamples\doc2.tif")
};
```

> **Szélsőséges eset:** Ha PDF-ek, TIFF-ek, JPEG-ek vagy PNG-k keverékével dolgozol, egyszerűen add hozzá ugyanahhoz a listához – az Aspose automatikusan kezeli a formátumfelismerést.

## 4. lépés: A kötegelt OCR művelet futtatása

Most átadjuk a listát a motornak. A `RecognizeBatch` egy `OcrResult` objektumok gyűjteményét adja vissza, egyet oldalanként.

```csharp
// Step 4: Perform batch OCR on the supplied streams
IList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);
```

> **Miért kötegelt?** Az OCR oldalankénti futtatása manuális ciklusban minden alkalommal újra inicializálja a motort, ami megduplázhatja a feldolgozási időt. A `RecognizeBatch` melegen tartja a motort, és az eredményeket folyamatosan visszaadja, amint elérhetők.

## 5. lépés: A felismert szöveg kiírása

Végül végigiterálunk az eredményeken, és minden oldal szövegét a konzolra írjuk. Itt cserélheted a `Console.WriteLine`-t fájlírásra, adatbázis-beillesztésre vagy bármilyen más utólagos műveletre.

```csharp
// Step 5: Display the OCR output for each page
for (int pageIndex = 0; pageIndex < ocrResults.Count; pageIndex++)
{
    Console.WriteLine($"--- Page {pageIndex + 1} ---");
    Console.WriteLine(ocrResults[pageIndex].Text);
}
```

### Várható konzol kimenet

```
--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit...
--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore...
--- Page 3 ---
Ut enim ad minim veniam, quis nostrud exercitation...
```

Ha a programot a mintafájlokkal futtatod, minden oldalra egy szövegtömböt kell látnod, ami bizonyítja, hogy sikeresen **extract text scanned pdf** tartalmat nyertél ki egyetlen lépésben.

## Gyakori problémák kezelése

| Probléma | Miért fordul elő | Gyors megoldás |
|----------|------------------|----------------|
| **Out‑of‑memory hibák** | Nagy PDF-ek sok nagy felbontású képet generálnak. | Korlátozd a DPI-t PDF betöltésekor: `ocrEngine.Settings.ImageDpi = 200;` |
| **Szemetelés karakterek** | A forrás szken alacsony minőségű vagy nem támogatott nyelvet használ. | Állítsd be explicit módon a nyelvet: `ocrEngine.Language = Language.English;` |
| **Részleges eredmények** | A köteglista egy sérült fájlt tartalmaz. | Tedd a `RecognizeBatch`-et try/catch blokkba, és logold a `e.Message`-t a hibás fájlhoz. |
| **Teljesítmény szűk keresztmetszet** | Egyetlen szálon fut egy többmagos gépen. | Használd a `Parallel.ForEach`-t külön `OcrEngine` példányokkal szálanként (haladó). |

## Bónusz: OCR eredmények mentése szövegfájlokba

Ha inkább minden oldalhoz külön `.txt` fájlt szeretnél, csak adj egy kis írási blokkot a ciklusba:

```csharp
string outputPath = @"C:\OCRResults";
System.IO.Directory.CreateDirectory(outputPath);

for (int i = 0; i < ocrResults.Count; i++)
{
    string fileName = System.IO.Path.Combine(outputPath, $"Page_{i + 1}.txt");
    System.IO.File.WriteAllText(fileName, ocrResults[i].Text);
}
```

Most a **convert pdf to text** egy rendezett mappává alakítottad, amely tiszta szövegfájlokat tartalmaz – tökéletes a további indexeléshez vagy kereséshez.

## Teljes működő példa

Az alábbiakban a teljes, másolás‑beillesztésre kész program található. Nincs rejtett függőség, nincs külső script.

```csharp
// FullProgram.cs
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.Image;

class Program
{
    static void Main()
    {
        // Initialise OCR engine (reuse for the whole batch)
        OcrEngine ocrEngine = new OcrEngine();

        // Optional: tweak settings for speed or accuracy
        ocrEngine.Settings.ImageDpi = 200;          // lower memory usage
        ocrEngine.Language = Language.English;     // set language explicitly

        // Build the list of image streams (PDF pages auto‑split)
        List<ImageStream> imageStreams = new List<ImageStream>
        {
            ImageStream.FromFile(@"C:\OCRSamples\doc1.pdf"),
            ImageStream.FromFile(@"C:\OCRSamples\doc2.tif")
        };

        // Perform batch OCR
        IList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);

        // Output each page's text to console
        for (int pageIndex = 0; pageIndex < ocrResults.Count; pageIndex++)
        {
            Console.WriteLine($"--- Page {pageIndex + 1} ---");
            Console.WriteLine(ocrResults[pageIndex].Text);
        }

        // (Optional) Save each page to a .txt file
        string outputFolder = @"C:\OCRResults";
        System.IO.Directory.CreateDirectory(outputFolder);
        for (int i = 0; i < ocrResults.Count; i++)
        {
            string txtPath = System.IO.Path.Combine(outputFolder, $"Page_{i + 1}.txt");
            System.IO.File.WriteAllText(txtPath, ocrResults[i].Text);
        }
    }
}
```

Futtasd a `dotnet run` parancsot a projekt mappájából, és figyeld, ahogy a konzol megtelik a kinyert szöveggel. Ez **how to batch OCR** egy dokumentumgyűjtemény néhány C# sorban.

## Amit lefedtünk – Gyors összefoglaló

- .NET konzolalkalmazás beállítása és az Aspose.OCR telepítése.  
- Egyetlen `OcrEngine` példány létrehozása a hatékony folyamat érdekében.  
- `ImageStream` objektumok listájának felépítése, amelyek automatikusan szétválasztják a PDF-eket oldalanként.  
- `RecognizeBatch` végrehajtása a **extract text from pdf** és más képformátumok egy lépésben történő feldolgozásához.  
- Az eredmények kiírása, és opcionálisan egyedi `.txt` fájlokba mentése, befejezve a **convert pdf to text** munkafolyamatot.  

## Következő lépések és kapcsolódó témák

- **Scale up**: Használd a `Parallel.ForEach`-t egy `OcrEngine` objektumokból álló pool-lal, hogy több száz fájlt dolgozz fel párhuzamosan.  
- **Language packs**: Cseréld le a `Language.English`-t `Language.French`-re vagy tölts be egy egyedi szótárat, amikor **recognize text from images** más nyelveken kell.  
- **Post‑processing**: Az OCR kimenetet irányítsd át egy helyesírás-ellenőrzőnek vagy egy természetes nyelv feldolgozó parsernek, hogy javítsd a pontosságot beolvasott szerződések esetén.  
- **Alternative libraries**: Hasonlítsd össze az Aspose OCR-t a Tesseract.NET-tel, ha nyílt forráskódú megoldást keresel – mindkettő **extract text scanned pdf** képes, de eltérnek a licencelésben és a kész pontosságban.  

![hogyan kötegelt OCR példája](alt="how to batch OCR example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}