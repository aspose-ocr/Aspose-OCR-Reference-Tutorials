---
category: general
date: 2026-05-28
description: Koreai nyelvű OCR oktatóanyag Aspose használatával C#-ban. Tanulja meg,
  hogyan töltsön be képet adatfolyamból, hogyan nyerjen ki egyszerű szöveget, hogyan
  konvertálja a képet PDF-be, és hogyan exportáljon kereshető PDF-et.
draft: false
keywords:
- korean language ocr
- convert image to pdf
- load image from stream
- extract plain text
- export searchable pdf
language: hu
og_description: Koreai nyelvű OCR C#-ban az Aspose használatával. Lépésről lépésre
  útmutató a kép betöltéséhez streamből, a sima szöveg kinyeréséhez, a kép PDF-re
  konvertálásához és kereshető PDF exportálásához.
og_title: Koreai nyelvű OCR – Kép PDF-be konvertálása és szöveg kinyerése (C# útmutató)
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: Korean Language OCR tutorial using Aspose in C#. Learn how to load
    image from stream, extract plain text, convert image to PDF and export searchable
    PDF.
  headline: 'Korean Language OCR with Aspose: Convert Image to PDF and Extract Text
    in C#'
  type: TechArticle
tags:
- Aspose OCR
- C#
- Image Processing
title: 'Koreai nyelvű OCR az Aspose-szal: Kép konvertálása PDF-be és szöveg kinyerése
  C#‑ban'
url: /hu/net/text-recognition/korean-language-ocr-with-aspose-convert-image-to-pdf-and-ext/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Koreai nyelvű OCR az Aspose-szal: Kép PDF-be konvertálása és szöveg kinyerése C#-ban

Gondolkodtál már azon, hogyan futtathatnád a **Koreai nyelvű OCR**-t egy képen anélkül, hogy bármit is a felhőbe küldenél? Nem vagy egyedül. Legyen szó utcajelzések digitalizálásáról, nyugták feldolgozásáról vagy többnyelvű keresőindex építéséről, a koreai karakterek helyi felismerése időt, pénzt és adatvédelmi fejfájást takaríthat meg.

Ebben az útmutatóban egy teljes, futtatható példán keresztül mutatjuk be, hogyan **tölts be képet streamből**, **nyerj ki egyszerű szöveget**, **konvertáld a képet PDF-be**, és végül **exportálj kereshető PDF-et** – mindezt az Aspose.OCR és néhány C# sor segítségével. Nincs külső szolgáltatás, nincs rejtett varázslat – csak tiszta .NET kód, amit bármely konzolos alkalmazásba beilleszthetsz.

## Mit fogsz megtanulni

- Egy működő konzolos programot, amely JPEG fájlt olvas be fájl stream segítségével.  
- Koreai szöveget, amely egyszerű Unicode karakterláncként kerül kinyerésre.  
- Részletes JSON jelentést az OCR futásról hibakeresés vagy elemzés céljából.  
- Kereshető PDF-et, amelyet bármely PDF-olvasóval megnyithatsz, és valóban ki tudod jelölni a koreai szavakat.  

**Előfeltételek**  
- .NET 6.0 vagy újabb (a kód .NET Framework 4.7+ alatt is működik).  
- Aspose.OCR for .NET NuGet csomag telepítve (`Install-Package Aspose.OCR`).  
- Egy mappa, amely tartalmazza a `korean_sign.jpg` fájlt, valamint egy írható hely a kimeneti fájlok számára.  

Ha már megvannak ezek a darabok, nagyszerű – vágjunk bele.

## 1. lépés: Az OCR motor inicializálása koreai nyelvű OCR-hoz

Az első dolog, amire szükséged van, egy `OcrEngine` példány. A GPU engedélyezése (ha van) drámaian felgyorsítja a felismerést, és az automatikus erőforrásletöltés kikapcsolása biztosítja, hogy a könyvtár az általad biztosított offline nyelvi csomagokat használja.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Enums;

// Create the OCR engine
var ocrEngine = new OcrEngine();

// Enable GPU acceleration – optional but fast
ocrEngine.Configuration.EnableGpu = true;

// We’ll supply the Korean language pack ourselves
ocrEngine.Configuration.AutomaticResourceDownload = false;
ocrEngine.Configuration.ResourcesFolder = @"YOUR_DIRECTORY/Resources";
```

> **Miért fontos:**  
> *GPU gyorsítás* a feldolgozási időt másodpercekből ezrekbe csökkentheti nagy kötegek esetén. Az `AutomaticResourceDownload` `false` értékre állítása garantálja, hogy a demó offline módban működjön – ez kritikus követelmény sok vállalati környezetben.

## 2. lépés: Kép betöltése streamből

A kép streamből való olvasása rugalmasságot biztosít: fájlokat húzhatsz le lemezről, hálózati megosztásból vagy akár memória‑gyorsítótárolt blobokból is. Itt egy helyi JPEG fájlt nyitunk meg, de ugyanaz a minta bármely `Stream` esetén működik.

```csharp
using System.IO;

// Open the image file as a read‑only stream
using var imageStream = File.OpenRead(@"YOUR_DIRECTORY/korean_sign.jpg");

// Feed the stream to the OCR engine
ocrEngine.Image = ImageStream.FromStream(imageStream);
```

> **Pro tipp:** Ha valaha webes API-n keresztül feltöltött képeket kell feldolgoznod, egyszerűen cseréld le a `File.OpenRead`-t a bejövő `IFormFile.OpenReadStream()`-re – a többi változatlan marad.

## 3. lépés: Koreai nyelv kiválasztása és előfeldolgozó szűrők alkalmazása

Az Aspose.OCR néhány előfeldolgozó lépést támogat, amelyek tisztítják a képet a felismerés előtt. Koreai jelzéseknél általában elegendő a dőléskorrekció és a zajszűrés.

```csharp
using Aspose.OCR.Enums;

// Tell the engine we’re dealing with Korean text
ocrEngine.Configuration.Language = Language.Korean;

// Apply deskew and denoise filters
ocrEngine.Configuration.PreprocessFilters = PreprocessFilter.Deskew |
                                            PreprocessFilter.Denoise;
```

> **Mi történik a háttérben?**  
> A `Deskew` szűrő kiegyenesíti a elfordított szöveget, míg a `Denoise` eltávolítja a szemcsézettséget, ami összezavarhatja a karakterosztályozót. Ezeknek a lépéseknek a kihagyása gyakran torz kimenetet eredményez, különösen alacsony felbontású fényképeknél.

## 4. lépés: Egyszerű szöveg aszinkron kinyerése

Most jön a döntő pillanat – a motor megkérdezése, hogy ismerje fel a karaktereket és adjon vissza egy tiszta karakterláncot. A `RecognizeAsync` használata a UI‑t responszívvá teszi, ha asztali vagy webalkalmazásba ágyazod.

```csharp
// Run OCR and get the plain text result
string plainText = await ocrEngine.RecognizeAsync();
```

A program futtatásakor valami ilyesmit kell látnod:

```
OCR complete. Extracted text:
서울시청
```

> **Miért async?**  
> Az OCR CPU‑igényes lehet. Az aszinkron végrehajtás megakadályozza, hogy a szál blokkolódjon, ami különösen hasznos az ASP.NET Core‑ban, ahol a szálak hiánya komoly problémát jelenthet.

## 5. lépés: Részletes felismerési eredmény lekérése és mentése JSON‑ként

Néha többre van szükség, mint a nyers karakterlánc – például bizalmi értékekre, keretboxokra vagy az eredeti képadatokra. A `RecognizeDetailed` metódus egy `RecognitionResult` objektumot ad vissza, amely későbbi elemzéshez JSON‑ként sorosítható.

```csharp
// Detailed result includes confidence, coordinates, etc.
RecognitionResult detailedResult = ocrEngine.RecognizeDetailed();

// Convert to nicely indented JSON
string jsonResult = detailedResult.ToJson(indent: true);

// Persist the JSON to disk
File.WriteAllText(@"YOUR_DIRECTORY/korean_ocr.json", jsonResult);
```

A `korean_ocr.json` megnyitása egy a következőhöz hasonló struktúrát mutat:

```json
{
  "Pages": [
    {
      "Text": "서울시청",
      "Confidence": 0.98,
      "Words": [
        {
          "Text": "서울시청",
          "BoundingBox": [12,34,56,78],
          "Confidence": 0.98
        }
      ]
    }
  ]
}
```

> **Mikor érdemes használni?**  
> Ha keresőindexet építesz, a bizalmi értékek segítenek kiszűrni az alacsony minőségű találatokat. Ha UI‑ban szeretnél szöveget kiemelni, a keretboxok a térképed.

## 6. lépés: Kép konvertálása PDF‑be és kereshető PDF exportálása

Az Aspose könnyedén átalakítja a rasztert vektorrá. Az `OutputFormat` `SearchablePdf`‑re állításával a könyvtár beágyazza az eredeti képet, és egy láthatatlan szövegréteget helyez rá, amely az OCR kimenetet tartalmazza. Az így kapott PDF kereshető, másolható és indexelhető, mint bármely natív PDF.

```csharp
using Aspose.OCR.Enums;

// Tell the engine to produce a searchable PDF
ocrEngine.Configuration.OutputFormat = OutputFormat.SearchablePdf;

// Save the PDF to the target folder
ocrEngine.Save(@"YOUR_DIRECTORY/korean_searchable.pdf");
```

Nyisd meg a `korean_searchable.pdf`-et az Adobe Readerben vagy bármely PDF‑nézőben, nyomd meg a **Ctrl+F**‑et, írd be egy koreai szót, és a dokumentum pontosan arra a helyre ugrik, ahol a szó található. Ez a kereshető PDF ereje.

> **Extra tipp:** Ha csak vizuális PDF‑re van szükséged a rejtett szövegréteg nélkül, állítsd az `OutputFormat`-ot `Pdf`‑re.

## Teljes működő példa

Az alábbiakban a teljes program látható – másold, illeszd be, cseréld le a `YOUR_DIRECTORY`-t egy valós útvonalra, és nyomd meg az **F5**‑öt.

```csharp
using System;
using System.IO;
using System.Threading.Tasks;
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Enums;

class OcrDemo
{
    static async Task Main()
    {
        // Step 1: Create the OCR engine and enable GPU with offline resources
        var ocrEngine = new OcrEngine();
        ocrEngine.Configuration.EnableGpu = true;
        ocrEngine.Configuration.AutomaticResourceDownload = false;
        ocrEngine.Configuration.ResourcesFolder = @"YOUR_DIRECTORY/Resources";

        // Step 2: Select the language and apply preprocessing filters
        ocrEngine.Configuration.Language = Language.Korean;
        ocrEngine.Configuration.PreprocessFilters = PreprocessFilter.Deskew |
                                                    PreprocessFilter.Denoise;

        // Step 3: Load the image to be recognized from a file stream
        using var imageStream = File.OpenRead(@"YOUR_DIRECTORY/korean_sign.jpg");
        ocrEngine.Image = ImageStream.FromStream(imageStream);

        // Step 4: Run OCR asynchronously and obtain the plain text result
        string plainText = await ocrEngine.RecognizeAsync();

        // Step 5: Get a detailed recognition result, convert it to JSON, and save it
        RecognitionResult detailedResult = ocrEngine.RecognizeDetailed();
        string jsonResult = detailedResult.ToJson(indent: true);
        File.WriteAllText(@"YOUR_DIRECTORY/korean_ocr.json", jsonResult);

        // Step 6: Export the recognized page as a searchable PDF
        ocrEngine.Configuration.OutputFormat = OutputFormat.SearchablePdf;
        ocrEngine.Save(@"YOUR_DIRECTORY/korean_searchable.pdf");

        Console.WriteLine("OCR complete. Extracted text:");
        Console.WriteLine(plainText);
    }
}
```

### Várható konzolkimenet

```
OCR complete. Extracted text:
서울시청
```

És három új fájlt találsz a forrásképed mellett:

- `korean_ocr.json` – a teljes felismerési adat.  
- `korean_searchable.pdf` – egy kereshető PDF.  
- (opcionális) bármilyen köztes napló, amelyet hozzáadsz.

## Gyakori kérdések és széljegyek

**Mi van, ha nincs GPU-m?**  
Állítsd `EnableGpu = false`‑ra; a CPU‑fallback tökéletesen megfelelő kis kötegekhez.

**Feldolgozhatok több képet egy futtatásban?**  
Természetesen. Csomagold a fő logikát egy `foreach (var file in Directory.GetFiles(...))` ciklusba, és minden iterációban állítsd be újra az `ocrEngine.Image`‑t.

**Hogyan kezelem a koreai mellett más nyelveket is?**  
Az Aspose.OCR lehetővé teszi, hogy `Language = Language.AutoDetect`‑et állíts be, vagy a bitwise OR operátorral kombináld a nyelveket (pl. `Language.Korean | Language.English`).

**Mi a teendő, ha az OCR bizalmi értéke alacsony?**  
Vizsgáld meg a `detailedResult.Pages[0].Words` elemeit, és szűrd ki azokat, ahol `Confidence < 0.7`. Emellett finomíthatod az előfeldolgozó szűrőket – próbáld ki a `PreprocessFilter.ContrastEnhancement` hozzáadását.

## Összegzés

Most már láttad, hogyan hajtható végre a **Koreai nyelvű OCR** vég‑től‑végig, a **kép betöltését streamből** a **szöveg egyszerű kinyeréséig**, majd a **kép PDF‑be konvertálásáig** és végül a **kereshető PDF exportálásáig**. A megközelítés moduláris, így könnyen cserélheted a képforrást, módosíthatod a kimeneti formátumot, vagy a JSON‑t bármely downstream pipeline-ba beillesztheted.

Mi a következő lépés


## Kapcsolódó oktatóanyagok

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [recognize text image with Aspose OCR for multiple languages](/ocr/english/net/ocr-settings/working-with-different-languages/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}