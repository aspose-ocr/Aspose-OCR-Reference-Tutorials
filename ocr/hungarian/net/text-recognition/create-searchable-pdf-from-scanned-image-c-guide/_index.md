---
category: general
date: 2026-04-26
description: Készítsen kereshető PDF-et szkennelt képből az Aspose OCR használatával
  C#-ban. Tanulja meg, hogyan konvertálja a szkennelt képet, vonja ki a szöveget,
  és gyorsan generáljon kereshető PDF-et.
draft: false
keywords:
- create searchable pdf
- convert scanned image
- extract text from image
- how to ocr document
- convert tiff to pdf
language: hu
og_description: Készítsen kereshető PDF-et beolvasott képből az Aspose OCR használatával.
  Lépésről lépésre C# kód a konvertáláshoz, szöveg kinyeréséhez és kereshető PDF generálásához.
og_title: Kereshető PDF létrehozása beolvasott képből – C# útmutató
tags:
- Aspose OCR
- C#
- PDF
- OCR
title: Kereshető PDF létrehozása beolvasott képből – C# útmutató
url: /hu/net/text-recognition/create-searchable-pdf-from-scanned-image-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kereshető PDF létrehozása beolvasott képből – C# útmutató

Szükséged volt már **kereshető PDF** fájlok létrehozására papír szerződésekből, nyugtákból vagy régi archívumokból? Nem vagy egyedül – a legtöbb fejlesztő ebben a helyzetben akad el, amikor egy ügyfél egy csomó TIFF beolvasást ad át, és kereshető PDF-et vár a végső eredményként.  

Ebben az útmutatóban pontosan megmutatjuk, **hogyan kell OCR-rel feldolgozni egy dokumentumot**, és egy beolvasott képet **kereshető PDF**-vé alakítani az Aspose OCR for .NET segítségével. A végére képes leszel **beolvasott képfájlok** átalakítására, **szöveg kinyerésére a képből**, és még a többoldalas TIFF-ek kezelésére is gond nélkül.

## Amire szükséged lesz

* .NET 6.0 vagy újabb (az API működik .NET Core, .NET Framework és .NET 5+ környezetben).  
* Érvényes Aspose OCR licenc, vagy ha elégedett vagy a kiértékelési vízjellel.  
* A `Aspose.OCR` NuGet csomag telepítve (`dotnet add package Aspose.OCR`).  
* Egy minta TIFF fájl (pl. `contract_scan.tif`), amelyet kereshető PDF‑vé szeretnél alakítani.

Ennyi – nincs extra könyvtár, nincs bonyolult konfiguráció. Készen állsz? Kezdjünk bele.

![Create searchable PDF example](create-searchable-pdf.png "create searchable pdf example")

## 1. lépés – Az OCR motor inicializálása (Kereshető PDF létrehozása)

Először is szükséged van egy `OcrEngine` példányra. Ez az objektum a munkavégző, amely beolvassa a bitmapet, azonosítja a karaktereket, és visszaadja a szöveget.  

```csharp
using Aspose.OCR;
using Aspose.OCR.Output;

// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Tell the engine which language to look for – Latin works for most English documents
ocrEngine.Language = Language.Latin;
```

**Miért állítsuk be a nyelvet?**  
Ha az alapértelmezett beállítást hagyod, az Aspose minden nyelvi csomagot megpróbál, ami lelassítja a folyamatot. A `Language.Latin` megadása azt mondja a motornak, hogy a latin ábécére koncentráljon, így gyorsabb és pontosabb eredményt kapsz az angol nyelvű szerződésekhez.

## 2. lépés – A beolvasott kép betöltése (Beolvasott kép átalakítása)

Most betápláljuk a motorba a feldolgozni kívánt képet. Az Aspose képes fájlútvonalat, streamet vagy akár `byte[]`-t is olvasni. Egyszerűség kedvéért a `ImageStream.FromFile`-t használjuk.  

```csharp
// Load the TIFF (or any supported image format)
ocrEngine.Image = ImageStream.FromFile(@"C:\Docs\contract_scan.tif");
```

Ha később **TIFF‑et PDF‑vé kell konvertálni**, tartsd szem előtt, hogy a többoldalas TIFF-ek automatikusan kezelődnek – minden keret külön PDF‑oldallá válik.

## 3. lépés – OCR futtatása és a szöveg kinyerése (Szöveg kinyerése a képből)

Az OCR futtatása olyan egyszerű, mint a `Recognize` meghívása. A motor egy `RecognitionResult` objektumot ad vissza, amely tartalmazza a tiszta szöveget, a megbízhatósági pontszámokat és a layout információkat.  

```csharp
// Perform the OCR operation
RecognitionResult result = ocrEngine.Recognize();

// The raw text is available via the Text property
string extractedText = result.Text;

// Quick sanity check – print the first 200 characters
Console.WriteLine(extractedText.Substring(0, Math.Min(200, extractedText.Length)));
```

**Pro tipp:** Ha csak a szövegre van szükséged (PDF nélkül), itt megállhatsz, és a `extractedText`-et egy `.txt` fájlba írhatsz. De a legtöbb esetben a cél egy kereshető PDF, ezért folytatjuk.

## 4. lépés – Mentés kereshető PDF‑ként (Kereshető PDF létrehozása)

Az Aspose a végső lépést egyszerűvé teszi: csak hívd meg a `Save` metódust a `SaveFormat.PdfSearchable` paraméterrel. A könyvtár a háttérben a kinyert szöveget egy láthatatlan rétegként ágyazza be, miközben megőrzi az eredeti kép megjelenését.  

```csharp
// Save the result as a searchable PDF
ocrEngine.Save(@"C:\Docs\contract_searchable.pdf", SaveFormat.PdfSearchable);
```

Amikor megnyitod a `contract_searchable.pdf`-et bármely PDF‑megtekintőben, képes leszel kiválasztani, másolni és keresni a szöveget – pontosan azt, amit az ügyfél egy “kereshető PDF”-től vár.

## Többoldalas TIFF-ek kezelése (TIFF‑et PDF‑vé konvertálás)

Ha a forrásfájl több oldalt tartalmaz, az Aspose automatikusan minden keretet külön oldalként kezel. Nem szükséges extra ciklus. Azonban előfordulhat, hogy a DPI-t vagy a képminőséget szeretnéd szabályozni minden oldalnál:  

```csharp
// Optional: tweak image processing settings before OCR
ocrEngine.ImageProcessingOptions.Dpi = 300; // higher DPI improves accuracy
ocrEngine.ImageProcessingOptions.Compression = ImageCompression.Jpeg;
```

Ezeknek a beállításoknak a megadása után ismételd meg a **2. lépést** minden keretnél, vagy egyszerűen irányítsd a `ImageStream.FromFile`-t a többoldalas TIFF-re, és hagyd, hogy az Aspose végezze a nehéz munkát.

## Gyakori hibák és megoldásaik

| Tünet | Valószínű ok | Megoldás |
|---------|--------------|-----|
| A szöveg torz vagy hiányzik | Helytelen nyelv beállítása | Állítsd be az `ocrEngine.Language`-t a megfelelő nyelvi csomagra (pl. `Language.German`). |
| A PDF hatalmas (10 MB egyoldalas beolvasásnál) | Az alapértelmezett képkompresszió alacsony | Állítsd be az `ocrEngine.ImageProcessingOptions.Compression`-t `Jpeg`-re, és adj meg egy ésszerű `Quality` értéket (0‑100). |
| Az OCR nagyon lassan fut | Az alapértelmezett `Auto` nyelvfelismerés használata | Explicit módon állítsd be a várt nyelvet. |
| Nem jelenik meg kereshető réteg | `SaveFormat.Pdf`-vel mentve a `PdfSearchable` helyett | `PdfSearchable`-t használj. |

## Teljes vég‑től‑végig példa

Mindent összevonva, itt egy kész, futtatható konzolalkalmazás, amelyet kimásolhatsz a Visual Studio-ba:  

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace SearchablePdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize OCR engine
            OcrEngine ocrEngine = new OcrEngine
            {
                Language = Language.Latin,
                // Optional: improve accuracy for low‑resolution scans
                ImageProcessingOptions = { Dpi = 300, Compression = ImageCompression.Jpeg }
            };

            // 2️⃣ Load the scanned image (convert scanned image)
            string inputPath = @"C:\Docs\contract_scan.tif";
            ocrEngine.Image = ImageStream.FromFile(inputPath);

            // 3️⃣ Run OCR and extract text (extract text from image)
            RecognitionResult result = ocrEngine.Recognize();
            Console.WriteLine("First 200 characters of extracted text:");
            Console.WriteLine(result.Text.Substring(0, Math.Min(200, result.Text.Length)));

            // 4️⃣ Save as searchable PDF (create searchable pdf)
            string outputPath = @"C:\Docs\contract_searchable.pdf";
            ocrEngine.Save(outputPath, SaveFormat.PdfSearchable);
            Console.WriteLine($"Searchable PDF created at: {outputPath}");
        }
    }
}
```

**Ami megjelenik:**  
* Egy konzolablak, amely az OCR‑elt szöveg egy részletét írja ki.  
* Egy `contract_searchable.pdf` fájl, amely az eredeti TIFF mellett helyezkedik el. Nyisd meg, nyomd meg a **Ctrl + F**-et, és keress bármely szót, amely az eredeti beolvasásban megjelent – voilà, működik.

## Következő lépések és kapcsolódó témák

* **Hogyan OCR‑elj dokumentumcsoportokat** – csomagold be a fenti kódot egy `foreach` ciklusba, és dolgozz fel egy teljes mappát.  
* **Beolvasott képek** konvertálása TIFF‑en kívül (PNG, JPEG) – ugyanaz az API működik; csak változtasd meg a fájl kiterjesztését.  
* **Szöveg kinyerése a képből** további elemzéshez – add át a `result.Text`-et egy természetes nyelvfeldolgozó csővezetéknek.  
* **PDF méret optimalizálása** – vizsgáld meg a `PdfSaveOptions`-t a képek további tömörítéséhez vagy a betűkészletek csak szükség esetén történő beágyazásához.  

Kísérletezz ezekkel az ötletekkel, és hamarosan a legjobb szakember leszel minden “alakítsd ezt a beolvasást kereshető PDF‑vé” kérésre.

---

### TL;DR

Most már tudod, hogyan kell **kereshető PDF** fájlokat létrehozni beolvasott képekből az Aspose OCR C#‑ban használva. A folyamat: motor inicializálása, kép betöltése, OCR futtatása, majd mentés `PdfSearchable`‑vel. Állítsd be a nyelvi beállításokat, a DPI‑t és a tömörítést a speciális esetek kezeléséhez, és készen állsz **beolvasott kép** átalakítására, **szöveg kinyerésére a képből**, sőt **TIFF‑et PDF‑vé** konvertálni nagy mennyiségben. Boldog kódolást!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}