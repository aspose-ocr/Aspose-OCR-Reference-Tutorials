---
category: general
date: 2026-04-04
description: Készíts kereshető PDF-et TIF képből C#-ban – tanulja meg, hogyan konvertálja
  a képet PDF-be, adjon hozzá PDF metaadatokat, és generáljon kereshető dokumentumot
  az Aspose.OCR használatával.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- add metadata to pdf
- add pdf metadata
- create pdf from tif
language: hu
og_description: Készítsen kereshető PDF-et TIF fájlból C#-ban. Konvertálja a képet
  PDF-be, adjon hozzá PDF metaadatokat, és hozza létre a kereshető dokumentumot az
  Aspose.OCR segítségével.
og_title: Kereshető PDF létrehozása TIF-ből – Lépésről lépésre útmutató
tags:
- Aspose.OCR
- C#
- PDF generation
title: Kereshető PDF létrehozása TIF‑ből – Kép PDF‑vé konvertálása, PDF metaadatok
  hozzáadása
url: /hu/net/text-recognition/create-searchable-pdf-from-tif-convert-image-to-pdf-add-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kereshető PDF létrehozása TIF‑ből – Teljes C# útmutató

Valaha is szükséged volt **kereshető PDF** létrehozására egy beolvasott számlából, de nem tudtad, hogyan tartsd a szöveget kereshetőnek és a fájl metaadatait rendezettnek? Nem vagy egyedül. Sok automatizálási projektben a PDF‑nek mind gép‑olvashatónak, mind megfelelően címkézettnek kell lennie olyan információkkal, mint a cím, a szerző és a megbízhatósági küszöbök.

Ebben az útmutatóban végigvezetünk egy teljes megoldáson, amely **képet PDF‑vé konvertál**, **PDF metaadatokat** injektál, és szűri az alacsony megbízhatóságú OCR eredményeket — mindezt az Aspose.OCR könyvtárral. A végére egy kész, használatra készen álló kódrészletet kapsz, amelyet bármely .NET projektbe beilleszthetsz, valamint néhány tippet a szélsőséges esetek kezeléséhez.

## Előkövetelmények

- .NET 6.0 vagy újabb (a kód .NET Framework 4.6+‑on is működik)  
- Aspose.OCR NuGet csomag (`Install-Package Aspose.OCR`)  
- Egy TIF kép, amelyet kereshető PDF‑vé szeretnél alakítani (pl. `input.tif`)  
- Alapvető ismeretek C#‑ban és Visual Studio‑ban (vagy a kedvenc IDE‑dben)

Nem szükséges más külső szolgáltatás – a teljes folyamat helyben fut.

## 1. lépés – OCR motor beállítása (Kereshető PDF mag létrehozása)

Az első dolog, amire szükségünk van, egy `OcrEngine` példány, amely tudja, melyik nyelvet kell felismertesse. A legtöbb üzleti esetben az angol elegendő, de a `Language.English`‑t bármely támogatott nyelvre cserélheted.

```csharp
using Aspose.OCR;
using Aspose.OCR.Pdf;   // PDF‑related extensions

// Initialize OCR engine with English language
OcrEngine ocrEngine = new OcrEngine
{
    Language = Language.English
};
```

**Miért fontos:** Az OCR motor végzi a nehéz munkát, a raszter pixeleket Unicode szöveggé alakítja. A nyelv helyes beállítása javítja a pontosságot, és csökkenti az alacsony megbízhatóságú szavak számát, amelyeket később kiszűrünk.

> **Pro tipp:** Ha többnyelvű dokumentumokat dolgozol fel, hozz létre több motor példányt, vagy használd a `Language.Multilingual`‑t, hogy az Aspose automatikusan kezelje a nyelvfelismerést.

## 2. lépés – TIF kép betöltése (PDF létrehozása TIF‑ből)

Most a motorra mutatunk a forrásfájlra. A `ImageStream.FromFile` segédfüggvény beolvassa a képet egy áramlásba, amelyet az OCR motor felhasználhat.

```csharp
// Load the TIF image you want to make searchable
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/input.tif");
```

Elgondolkodhatsz, *„Betáplálhatok helyette JPEG‑et vagy PNG‑t?”* Természetesen – az Aspose.OCR a legtöbb raszter formátumot támogatja. Csak változtasd meg a fájlkiterjesztést, és már indulhat is.

## 3. lépés – PDF beállítások konfigurálása (Metaadatok hozzáadása a PDF‑hez)

A konvertálás előtt definiálunk egy `PdfOptions` objektumot. Itt **PDF metaadatokat** adunk meg, például a címet és a szerzőt, valamint azt is beállítjuk, hogy a motor eldobja azokat a szavakat, amelyek megbízhatósága egy küszöb alá esik.

```csharp
PdfOptions searchablePdfOptions = new PdfOptions
{
    Title = "Invoice #12345",
    Author = "MyCompany",
    // Hide words with confidence lower than 0.8 (80%)
    MinConfidence = 0.8f
};
```

**Mi történik itt?**  
- A `Title` és `Author` a PDF dokumentuminformációs szótárának részévé válnak, ami megkönnyíti a fájl indexelését dokumentumkezelő rendszerekben.  
- A `MinConfidence` egy védőkorlát: az OCR gyakran félreolvassa a halvány karaktereket; ezek kiszűrése tisztává teszi a kereshető réteget és javítja a későbbi szövegkinyerést.

Ha egyedi metaadatokra van szükséged (pl. `Subject`, `Keywords`), azokat a `PdfOptions.CustomProperties`‑on keresztül állíthatod be.

## 4. lépés – Kép konvertálása kereshető PDF‑vé (Kép konvertálása PDF‑be)

Miután a motor elő van készítve és a beállítások megvannak, az utolsó hívás elvégzi a konvertálást. Egy kereshető PDF‑et ír a lemezre, amely az OCR szövegréteget az eredeti kép alá ágyazza.

```csharp
ocrEngine.ConvertToSearchablePdf(
    outputPath: @"YOUR_DIRECTORY/output.pdf",
    pdfOptions: searchablePdfOptions);
```

Ez a sor lefutása után a `output.pdf` tartalmazza:
- Az eredeti TIF képet vizuális háttérként  
- Egy láthatatlan szövegréteget, amelyet a keresőmotorok és a másolás‑beillesztés műveletek is olvasni tudnak  
- A korábban definiált metaadatokat (cím, szerző, stb.)

### Várható eredmény

Nyisd meg a generált PDF‑et az Adobe Reader‑ben vagy bármely PDF‑megtekintőben, és próbáld ki a szöveg kijelölését. Képesnek kell lenned másolni a mondatokat, amelyek megegyeznek az eredeti beolvasással. A dokumentum **Tulajdonságok** párbeszédablaka a „Invoice #12345” címet és a „MyCompany” szerzőt fogja mutatni.

## 5. lépés – Megbízhatósági szűrés ellenőrzése (Miért segít a MinConfidence)

Hasznos megerősíteni, hogy az alacsony megbízhatóságú szavak valóban eltávolításra kerültek. A PDF rejtett szövegét ellenőrizheted egy olyan eszközzel, mint a `pdftotext`:

```bash
pdftotext output.pdf - | grep -i "unlikelyword"
```

Ha a szó soha nem jelenik meg, a `MinConfidence` szűrő a kívánt módon működött. Állítsd a küszöböt (pl. `0.7f`), ha agresszívebb vagy engedékenyebb szűrésre van szükséged.

## 6. lépés – Többoldalas kezelés (Kereshető PDF létrehozása többoldalas TIF‑ből)

Sok számla többoldalas TIFF‑ként érkezik. Az Aspose.OCR automatikusan minden keretet külön oldalként kezel. Csak a motorra mutass a többoldalas fájlra; ugyanaz a `ConvertToSearchablePdf` hívás egy többoldalas kereshető PDF‑et generál.

```csharp
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/multi_page.tif");
ocrEngine.ConvertToSearchablePdf(@"YOUR_DIRECTORY/multi_output.pdf", searchablePdfOptions);
```

**Szélsőséges eset:** Ha egy oldal üres, az OCR még mindig generálhat egy üres szövegréteget, ami ártalmatlan. Azonban kihagyhatod az üres oldalakat a `ocrEngine.HasText` ellenőrzésével a konvertálás előtt.

## 7. lépés – Teljes példa csomagolása (Minden lépés együtt)

Az alábbi egy önálló, futtatható program, amely mindent összekapcsol. Cseréld le a `YOUR_DIRECTORY`‑t a géped tényleges mappájának elérési útjára.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Pdf;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = Language.English
        };

        // 2️⃣ Load the TIF image (create pdf from tif)
        string inputPath = @"YOUR_DIRECTORY/input.tif";
        ocrEngine.Image = ImageStream.FromFile(inputPath);

        // 3️⃣ Set PDF metadata and confidence filter
        PdfOptions pdfOptions = new PdfOptions
        {
            Title = "Invoice #12345",
            Author = "MyCompany",
            MinConfidence = 0.8f
        };

        // 4️⃣ Convert to searchable PDF (convert image to pdf)
        string outputPath = @"YOUR_DIRECTORY/output.pdf";
        ocrEngine.ConvertToSearchablePdf(outputPath, pdfOptions);

        Console.WriteLine($"✅ Searchable PDF created at: {outputPath}");
    }
}
```

Futtasd a programot (`dotnet run` vagy nyomd meg a **F5**‑öt a Visual Studio‑ban), és láthatod a megerősítő üzenetet. A generált PDF a forrásképed mellett helyezkedik el, készen áll az indexelésre vagy archiválásra.

## Gyakori kérdések és buktatók

| Kérdés | Válasz |
|----------|--------|
| **Hozzáadhatok egy egyedi betűtípust a kereshető réteghez?** | Az OCR réteg Unicode‑ot használ; a vizuális megjelenést az alatta lévő kép határozza meg, így nincs szükség további betűtípus beágyazására. |
| **Mi van, ha a TIF színes?** | Az Aspose.OCR automatikusan szürkeárnyalatossá konvertálja a színes képeket az OCR‑hez, de az eredeti színeket a PDF‑ben megtarthatod a `PdfOptions.PreserveColor = true` beállítással. |
| **A könyvtár szálbiztos?** | Minden `OcrEngine` példányt egyetlen szál használjon. Párhuzamos feldolgozáshoz hozz létre külön motor példányt szálanként. |
| **Hogyan titkosíthatom a PDF‑et?** | Használd a `PdfOptions.Security`‑t, hogy jelszót és jogosultságokat állíts be az OCR konvertálás után. |

## Következő lépések (Bővítsd a PDF eszköztáradat)

- **Kötegelt feldolgozás:** Egy mappában lévő TIFF‑ek felett iterálva generálj minden egyeshez kereshető PDF‑et.  
- **Utófeldolgozás:** Használd az Aspose.PDF‑et a generált PDF‑ek egyetlen fő dokumentummá egyesítéséhez.  
- **Haladó metaadatok:** Tölts fel egyedi XMP mezőket a jobb integráció érdekében a SharePoint vagy ECM rendszerekkel.  

Mindezek a kiterjesztések az általunk most bemutatott alapmintára épülnek: **kereshető PDF létrehozása**, **kép konvertálása PDF‑be**, és **PDF metaadatok hozzáadása**.

*Boldog kódolást! Ha bármilyen problémába ütközöl, hagyj megjegyzést alább, vagy nézd meg az Aspose.OCR dokumentációt a legújabb API‑frissítésekért.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}