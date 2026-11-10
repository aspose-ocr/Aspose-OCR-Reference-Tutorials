---
category: general
date: 2026-05-25
description: Konvertálja a TIFF fájlokat szöveggé az Aspose.OCR segítségével C#-ban.
  Tanulja meg a kötegelt kép‑szöveg átalakítást, és hatékonyan nyerjen ki szöveget
  TIFF fájlokból.
draft: false
keywords:
- convert tiff to text
- extract text from tiff
- batch image to text conversion
- convert scanned images txt
language: hu
og_description: Konvertálja a TIFF-et szöveggé az Aspose.OCR segítségével. Ez az útmutató
  bemutatja a kötegelt kép‑szöveg konverziót, valamint azt, hogyan lehet néhány C#
  sorral szöveget kinyerni a TIFF fájlokból.
og_title: TIFF konvertálása szöveggé C#-ban – Teljes kötegelt OCR útmutató
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: Convert TIFF to text using Aspose.OCR in C#. Learn batch image to text
    conversion and extract text from TIFF files efficiently.
  headline: Convert TIFF to Text in C# – Complete Batch OCR Guide
  type: TechArticle
- description: Convert TIFF to text using Aspose.OCR in C#. Learn batch image to text
    conversion and extract text from TIFF files efficiently.
  name: Convert TIFF to Text in C# – Complete Batch OCR Guide
  steps:
  - name: '**Create** an OCR engine set for English.'
    text: '**Create** an OCR engine set for English.'
  - name: '**Collect** every TIFF file from the target folder.'
    text: '**Collect** every TIFF file from the target folder.'
  - name: '**Run** `BatchOcr.RecognizeAll` with four threads, turning each image into
      a string.'
    text: '**Run** `BatchOcr.RecognizeAll` with four threads, turning each image into
      a string.'
  - name: '**Loop** over the results, swapping the `.tif` extension for `.txt` and
      writing the string to disk.'
    text: '**Loop** over the results, swapping the `.tif` extension for `.txt` and
      writing the string to disk.'
  type: HowTo
tags:
- C#
- OCR
- Aspose
- TIFF
title: TIFF konvertálása szöveggé C#-ban – Teljes kötegelt OCR útmutató
url: /hu/net/text-recognition/convert-tiff-to-text-in-c-complete-batch-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# TIFF konvertálása szöveggé C#‑ban – Teljes kötegelt OCR útmutató

Valaha szükséged volt **TIFF szöveggé konvertálásra**, de nem tudtad, hol kezdj? Nem vagy egyedül – sok fejlesztő elakad a kötegelt OCR‑nál, amikor beolvasott dokumentumokkal dolgozik. Ebben az útmutatóban egy gyakorlati megoldáson keresztül vezetünk, amely **kivonja a szöveget a TIFF** fájlokból az Aspose.OCR használatával, és párhuzamosan hajtjuk végre, így a nagy mappák másodpercek alatt elkészülnek.

Érinteni fogjuk a **kötegelt kép‑szöveg konverzió** legjobb gyakorlatait is, így a végére egy újrahasználható kódrészletet kapsz, amely egy teljes könyvtár beolvasott képet átalakít rendezett *.txt* fájlokká – tökéletes indexeléshez, kereséshez vagy a további elemzésekhez.

## Amire szükséged lesz

- **.NET 6.0** vagy újabb (a kód .NET Framework‑ön is lefordítható)  
- **Aspose.OCR for .NET** NuGet csomag (`Install-Package Aspose.OCR`)  
- Egy mappa, amely egy vagy több *.tif* fájlt tartalmaz (a klasszikus TIFF‑szkennelési formátum)  
- A kedvenc IDE‑d (Visual Studio, VS Code, Rider – bármi, amit kedvelsz)

Ennyi. Nincsenek külső szolgáltatások, API kulcsok, csak tiszta C# és Aspose.

![Képernyőkép egy feldolgozott TIFF fájlról és a keletkezett szövegfájlról](/images/ocr-result.png "OCR eredmény, amely a TIFF szöveggé konvertált kimenetet mutatja")

*(Alt szöveg: Képernyőkép, amely a konvertált TIFF szöveggé kimenetet mutatja a képernyőn)*

## 1. lépés: OCR motor beállítása – TIFF konvertálása szöveggé

Először is szükségünk van egy `OcrEngine` példányra, amely tudja, hogy angol karaktereket kell olvasnia. A motor a konverzió szíve; helyes beállítása megbízható eredményeket biztosít.

```csharp
using Aspose.OCR;
using System.IO;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // Create an OCR engine configured for English – this is the core of convert TIFF to text
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.English
        };
```

*Miért fontos ez:*  
Az Aspose.OCR több tucat nyelvet támogat. Ha többnyelvű beolvasásról van szó, egyszerűen változtasd meg a `OcrLanguage.English` értéket a megfelelő enum értékre. Ha a nyelvet nem definiálod, a motor automatikus felismerés módba kerül, ami lassabb és kevésbé pontos lehet.

## 2. lépés: Összes TIFF fájl összegyűjtése – Hatékony szövegkinyerés TIFF‑ből

Ezután minden *.tif* fájlt lekérünk egy általad megadott mappából. A `Directory.GetFiles` használata egy tiszta tömböt ad, amelyet a kötegelt feldolgozóba táplálhatunk.

```csharp
        // Locate every TIFF in the input folder – adjust the path to your own directory
        string inputFolder = @"C:\Scans\Batch";
        string[] tiffFiles = Directory.GetFiles(inputFolder, "*.tif", SearchOption.TopDirectoryOnly);

        if (tiffFiles.Length == 0)
        {
            System.Console.WriteLine("No TIFF files found. Check the folder path.");
            return;
        }
```

*Pro tipp:* A `SearchOption.AllDirectories` jelző használható, ha a beolvasásaid almappákban vannak. Csak ne feledd, hogy a mélyebb rekurzió növelheti a memóriahasználatot a kötegelt lépés során.

## 3. lépés: Párhuzamos OCR végrehajtása – Kötegelt kép‑szöveg konverzió

Most jön a szórakoztató rész. Az Aspose.OCR egy statikus segédfüggvényt tartalmaz, a `BatchOcr.RecognizeAll`‑t, amely egy fájlútvonalak tömbjét, egy motort és egy `parallelism` tippet fogad. Négy szálat indítunk, ami egy modern négymagos laptopon közel lineáris gyorsulást eredményez.

```csharp
        // Run OCR on all files in parallel (4 threads by default)
        // The result is a dictionary where Key = file path, Value = extracted text
        Dictionary<string, string> ocrResults = BatchOcr.RecognizeAll(tiffFiles, ocrEngine, parallelism: 4);
```

*Miért a párhuzamosság?*  
Nagy felbontású TIFF‑k kötegének beolvasása CPU‑igényes lehet. A munka több szálra osztásával minden magot foglalkoztatunk, így drámaian csökkentve az összidőt. Ha szerveren több maggal futtatod, növeld a `parallelism` értékét ennek megfelelően.

## 4. lépés: Kimenet írása – Beolvasott képek TXT fájlokká konvertálása

Végül végigiterálunk a szótáron, és minden szövegrészt egy *.txt* fájlba írunk, amely az eredeti alapnevet viseli. Ez az a pillanat, amikor a **convert scanned images txt** valósággá válik.

```csharp
        // Save each recognized text to a .txt file with the same base name as the source TIFF
        foreach (var kvp in ocrResults)
        {
            string sourcePath = kvp.Key;
            string extractedText = kvp.Value;

            // Change extension from .tif to .txt
            string txtPath = Path.ChangeExtension(sourcePath, ".txt");

            // Write the text – UTF‑8 ensures all characters are preserved
            File.WriteAllText(txtPath, extractedText);
            System.Console.WriteLine($"Saved: {txtPath}");
        }

        System.Console.WriteLine("Batch conversion complete!");
    }
}
```

### Mit csinál a kód, egyszerűen magyarul

1. **Create** egy angol nyelvre beállított OCR motort.  
2. **Collect** minden TIFF fájlt a célmappából.  
3. **Run** a `BatchOcr.RecognizeAll`‑t négy szállal, minden képet karakterlánccá alakítva.  
4. **Loop** a eredmények felett, a `.tif` kiterjesztést `.txt`‑re cserélve, és a karakterláncot lemezre írva.

Ez a teljes **convert TIFF to text** munkafolyamat kevesebb, mint 50 kódsorban.

## Szélsőséges esetek kezelése – Amikor a dolgok nem mennek simán

- **Missing or corrupted TIFFs** – a `BatchOcr` `OcrException`‑t dob. Ha szükséged van a hibamentes visszaesésre, tedd a hívást egy `try / catch` blokkba.  
- **Non‑English documents** – változtasd a `OcrLanguage.English`‑t `OcrLanguage.Spanish`, `OcrLanguage.French` stb. értékre, vagy használd a `OcrLanguage.AutoDetect`‑et.  
- **Very large images** – fontold meg a DPI csökkentését OCR előtt (`ocrEngine.ImagePreprocessing.Dpi = 200`), hogy memóriát takaríts meg, bár ez csökkentheti a pontosságot.  
- **Output encoding** – ha egy adott kódlapra (pl. Windows‑1252) van szükséged, add át a `File.WriteAllText(txtPath, extractedText, Encoding.GetEncoding(1252))`‑nek.

## Profi tippek a robusztus kötegelt konverziókhoz

- **Log failures**: hozz létre egy `List<string> failedFiles` listát, és adj hozzá minden olyan fájlt, amely hibát dob; a ciklus után írd ki a listát egy naplóba.  
- **Reuse the engine**: ugyanaz a `OcrEngine` példány újra felhasználható sok fájl esetén; ne hozd létre a cikluson belül.  
- **Validate the result**: egy egyszerű `if (string.IsNullOrWhiteSpace(extractedText))` jelzi a üres vagy olvashatatlan beolvasásokat.  
- **Combine with PDF**: ha a forrásod egy többoldalas PDF, először konvertáld minden oldalt TIFF‑re (az Aspose.PDF ezt megteszi), majd futtasd le ezt a köteget.

## Következő lépések – A egyszerű konverzión túl

Most, hogy tömegesen **extract text from TIFF** fájlokból tudsz szöveget kinyerni, lehet, hogy szeretnéd:

- A *.txt* fájlokat egy keresőindexbe (Elasticsearch, Azure Cognitive Search) betáplálni.  
- Minden eredményen nyelvfelismerést futtatni, hogy a dokumentumokat helyi specifikus folyamatokba irányítsuk.  
- Kereshető PDF‑eket generálni az OCR szöveget visszahelyezve az eredeti képekre (újra az Aspose.PDF‑vel).  

Mindez ugyanarra az alapötletre épül: a **batch image to text conversion** egy építőköve a nagyobb dokumentum‑feldolgozó rendszereknek.

---

### Következtetés

Most megtanultad, hogyan **convert TIFF to text** az Aspose.OCR használatával, egy teljes mappát párhuzamosan feldolgozni, és minden eredményt tiszta *.txt* fájlként menteni. A megoldás könnyű, teljesen konfigurálható, és készen áll a termelésre – akár régi számlákat digitalizálsz, beolvasott szerződéseket archiválsz, vagy egy szövegkereső motorral működtetsz.  

Próbáld ki, finomítsd a párhuzamosságot, és kezd el a frissen létrehozott szövegfájlokat a szükséges munkafolyamatba betáplálni. Boldog OCR‑olást!

---

## Kapcsolódó útmutatók

- [Szöveg kinyerése képekből OCR művelettel mappákon](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Szöveg kinyerése képből – OCR optimalizálás Aspose.OCR for .NET használatával](/ocr/english/net/ocr-optimization/)
- [Képszöveg kinyerése C#‑ban nyelvválasztással az Aspose.OCR segítségével](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}