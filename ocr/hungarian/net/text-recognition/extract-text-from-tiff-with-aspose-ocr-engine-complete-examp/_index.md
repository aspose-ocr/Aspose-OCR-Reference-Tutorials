---
category: general
date: 2026-04-04
description: Tanulja meg, hogyan lehet szöveget kinyerni TIFF fájlokból egy OCR motor
  példával C#-ban. Lépésről lépésre útmutató JSON és XML kimenettel.
draft: false
keywords:
- extract text from tiff
- ocr engine example
- Aspose OCR C#
- multi‑page TIFF OCR
- JSON OCR result
language: hu
og_description: Szöveg kinyerése TIFF fájlokból OCR motor segítségével C# példában.
  Részletes lépések, teljes kód és tippek JSON/XML kimenethez.
og_title: Szöveg kinyerése TIFF-fájlból az Aspose OCR motor segítségével – Teljes
  útmutató
tags:
- C#
- OCR
- Aspose
- Image Processing
title: Szöveg kinyerése TIFF-fájlból az Aspose OCR motorral – Teljes példa
url: /hu/net/text-recognition/extract-text-from-tiff-with-aspose-ocr-engine-complete-examp/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Szöveg kinyerése TIFF‑ből – Teljes OCR motor példa C#‑ban

Valaha is szükséged volt **szöveg kinyerésére TIFF** képekből, de nem tudtad, melyik könyvtár tudja kezelni a többoldalas fájlokat anélkül, hogy körülményes megoldásokat kellene alkalmazni? Nem vagy egyedül. Sok régi rendszerben a dokumentumok többoldalas TIFF‑szkenként érkeznek, és a nyers szöveg kinyerése elengedhetetlen a keresés, a megfelelőség vagy az adatbevitel automatizálása szempontjából.

A jó hír? Az Aspose OCR‑rel néhány sor kóddal megoldható – anélkül, hogy alacsony szintű pixelpufferekkel kellene bajlódni. Ez a bemutató egy **teljes OCR motor példát** vezet végig, amely betölti a többoldalas TIFF‑et, felismert minden oldalt, és szép formázott JSON‑t valamint opcionális XML‑t generál. A végére egy azonnal futtatható C# konzolalkalmazást kapsz, amely másodpercek alatt kinyeri a szöveget TIFF fájlokból.

## Mit fogsz megtanulni

- Hogyan állítsd be az Aspose OCR motort egy .NET projektben.  
- A pontos kód, amely **szöveg kinyerését TIFF** fájlokból végzi, beleértve a többoldalas kezelését.  
- Miért lehet előnyös a JSON a XML helyett, és hogyan generálhatod mindkettőt.  
- Tippek a gyakori hibák elhárításához (pl. kép DPI, memóriahasználat).  

### Előfeltételek

- .NET 6.0 SDK vagy újabb (a kód működik .NET Core‑dal és .NET Framework‑kel is).  
- Érvényes Aspose OCR licenc (vagy egy ingyenes próbaverzió kulcs).  
- Visual Studio 2022 vagy bármely kedvenc C# szerkesztő.  
- Egy minta többoldalas TIFF fájl (a példában `multi-page.tiff` néven).  

> **Pro tipp:** Ha szűk költségvetésed van, az ingyenes próbaverzió még mindig lehetővé teszi, hogy havonta akár 100 oldal szövegét kinyerd – tökéletes teszteléshez.

---

## 1. lépés – OCR motor inicializálása (ocr engine example)

Mielőtt **szöveg kinyerését TIFF**‑ből elvégezhetnénk, szükségünk van egy OCR motor példányra. Ez az objektum tárolja az összes konfigurációt, amelyet később módosíthatsz (nyelv, felbontás stb.).

```csharp
using Aspose.OCR;
using System.IO;

// Create a new OCR engine – this is the core of our ocr engine example
var ocrEngine = new OcrEngine();

// Optional: set language if you know the document’s language
// ocrEngine.Language = Language.English;
```

*Miért fontos:* Az `OcrEngine` osztály elrejti a nehéz munkát. Egyszer példányosítva, és több képhez újra felhasználva memóriatakarékosabb, mint minden oldalhoz új motort létrehozni.

---

## 2. lépés – Többoldalas TIFF betöltése (extract text from TIFF)

Most a motort a forrásfájlra irányítjuk. Az `ImageStream.FromFile` támogatja a TIFF, JPEG, PNG és sok más formátumot, de ebben a bemutatóban a TIFF‑re koncentrálunk.

```csharp
// Load the multi‑page TIFF you want to process
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/multi-page.tiff");
```

> **Megjegyzés:** Cseréld le a `YOUR_DIRECTORY`‑t a gépeden lévő tényleges mappára.  
> **Tipp:** Ha a TIFF‑ed alacsony DPI‑vel (150 alatti) rendelkezik, fontold meg előfeldolgozását az OCR pontosságának javítása érdekében.

---

## 3. lépés – Minden oldal felismerése

A `Recognize()` meghívása lefuttatja az OCR algoritmust a TIFF **minden oldalán**. Az eredményobjektum tartalmazza a nyers szöveget, a biztonsági pontszámokat és az oldalankénti szegmentációt.

```csharp
// Run OCR on the loaded image – this extracts text from all pages
var ocrResult = ocrEngine.Recognize();
```

*Mit kapsz vissza:* Az `ocrResult` egy `PageResult` objektumok gyűjteményét tartalmazza. Egy oldal szövege a `ocrResult.Pages[i].Text`‑en keresztül érhető el. A motor továbbá biztonsági szinteket is biztosít, amelyek hasznosak lehetnek a minőség-ellenőrzéshez.

---

## 4. lépés – Eredmények mentése JSON‑ként (és opcionális XML)

A legtöbb modern adatcsővezeték a JSON‑t részesíti előnyben, de a régi rendszerek még mindig XML‑t használnak. Íme, hogyan generálhatod mindkettőt, szép formázással.

```csharp
// Convert the recognition result to pretty‑printed JSON
string jsonResult = ocrResult.ToJson(prettyPrint: true);
File.WriteAllText(@"YOUR_DIRECTORY/result.json", jsonResult);

// Optional: also output XML for older workflows
string xmlResult = ocrResult.ToXml();
File.WriteAllText(@"YOUR_DIRECTORY/result.xml", xmlResult);
```

### Minta JSON kimenet (csonkítva)

```json
{
  "Pages": [
    {
      "PageNumber": 1,
      "Text": "Invoice #12345\nDate: 2024‑03‑15\nTotal: $1,250.00",
      "Confidence": 0.97
    },
    {
      "PageNumber": 2,
      "Text": "Itemized List\n1. Widget A – $500.00\n2. Widget B – $750.00",
      "Confidence": 0.95
    }
  ]
}
```

A JSON ember által olvasható, így a hibakeresés gyerekjáték. Az XML ugyanazt a struktúrát tükrözi, ha szükséged van rá.

---

## 5. lépés – Kinyerés ellenőrzése (extract text from TIFF)

A fájlok írása után egy gyors ellenőrzés segít megbizonyosodni arról, hogy semmi sem ment félre.

```csharp
// Load the JSON back just to confirm it was saved correctly
string loadedJson = File.ReadAllText(@"YOUR_DIRECTORY/result.json");
Console.WriteLine("First 200 characters of JSON output:");
Console.WriteLine(loadedJson.Substring(0, Math.Min(200, loadedJson.Length)));
```

Ha a kódrészlet megjelenik a konzolon, sikeresen **kivontad a szöveget a TIFF‑ből**, és elmentetted. Innen a JSON‑t betáplálhatod egy keresőindexbe, adatbázisba vagy bármely downstream szolgáltatásba.

---

## Miért használjuk az Aspose OCR‑t a TIFF‑ből történő szövegkivonáshoz?

- **Beépített többoldalas támogatás** – nincs szükség a TIFF manuális felosztására.  
- **Magas pontosság** a saját, proprietáris neurális hálózati modelljeinek köszönhetően.  
- **Keresztplatformos** – működik Windows, Linux és macOS .NET futtatókörnyezeteken.  
- **Gazdag kimeneti formátumok** (JSON, XML, plain text), amelyek mind a modern, mind a régi stackekhez illeszkednek.  

Ha még bizonytalan vagy, próbáld ki az ingyenes próbaverziót egy mintadokumentummal. Érezni fogod a sebességet és az egyszerűséget a nyílt forráskódú alternatívákkal szemben, amelyek gyakran extra képelőfeldolgozást igényelnek.

---

## Gyakori buktatók és hogyan kerüld el őket

| Probléma | Tünet | Megoldás |
|----------|-------|----------|
| Alacsony felbontású TIFF | Hiányzó karakterek, alacsony biztonság | Növeld a kép felbontását ≥150 DPI OCR előtt (`ocrEngine.Image = ImageStream.FromFile(...).Resize(150)` ) |
| Rossz nyelv | Torz szavak, különösen nem‑angol szövegnél | Állítsd be `ocrEngine.Language = Language.Spanish` (vagy a megfelelő nyelvet) a `Recognize()` előtt |
| Memóriahiány nagy fájloknál | `OutOfMemoryException` | Oldalak feldolgozása kötegekben: iterálj a `ocrEngine.Image.Pages`‑en és hívd a `RecognizePage(i)`‑t |
| Licenc nincs alkalmazva | „Evaluation” vízjel a kimeneten | Regisztráld a licencet: `License license = new License(); license.SetLicense("Aspose.OCR.lic");` |

---

## Teljes működő példa (másolás-beillesztés kész)

Az alábbi teljes programot beillesztheted egy új konzolprojektbe. Tartalmazza a megbeszélt összes részt – inicializálás, betöltés, felismerés és mentés.

```csharp
using Aspose.OCR;
using System;
using System.IO;

namespace TiffOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣  Initialize the OCR engine (ocr engine example)
            // -------------------------------------------------
            var ocrEngine = new OcrEngine();

            // Optional: set license if you have one
            // var license = new License();
            // license.SetLicense("Aspose.OCR.lic");

            // -------------------------------------------------
            // 2️⃣  Load the multi‑page TIFF (extract text from TIFF)
            // -------------------------------------------------
            string tiffPath = @"YOUR_DIRECTORY/multi-page.tiff";
            if (!File.Exists(tiffPath))
            {
                Console.WriteLine($"File not found: {tiffPath}");
                return;
            }

            ocrEngine.Image = ImageStream.FromFile(tiffPath);

            // -------------------------------------------------
            // 3️⃣  Recognize every page
            // -------------------------------------------------
            var ocrResult = ocrEngine.Recognize();

            // -------------------------------------------------
            // 4️⃣  Save JSON (pretty) and optional XML
            // -------------------------------------------------
            string jsonPath = @"YOUR_DIRECTORY/result.json";
            string jsonResult = ocrResult.ToJson(prettyPrint: true);
            File.WriteAllText(jsonPath, jsonResult);
            Console.WriteLine($"JSON saved to {jsonPath}");

            // Optional XML output
            string xmlPath = @"YOUR_DIRECTORY/result.xml";
            string xmlResult = ocrResult.ToXml();
            File.WriteAllText(xmlPath, xmlResult);
            Console.WriteLine($"XML saved to {xmlPath}");

            // -------------------------------------------------
            // 5️⃣  Quick verification (extract text from TIFF)
            // -------------------------------------------------
            string preview = jsonResult.Length > 200 ? jsonResult.Substring(0, 200) + "..." : jsonResult;
            Console.WriteLine("\nPreview of JSON output:");
            Console.WriteLine(preview);
        }
    }
}
```

Mentsd a fájlt `Program.cs` néven, futtasd a `dotnet run` parancsot, és figyeld, ahogy a konzol megmutatja, hová került a JSON és az XML. Ennyi – most egy **ocr engine példát** hajtottál végre, amely szöveget nyer ki TIFF‑ből.

---

## Következő lépések és kapcsolódó témák

- **Kötegelt feldolgozás:** Csomagold be a fenti logikát egy `foreach` ciklusba, hogy automatikusan több tucat TIFF fájlt kezelj.  
- **Keresőintegráció:** Tedd a JSON‑t Elasticsearch‑be vagy Azure Cognitive Search‑be, hogy teljes szöveges keresést biztosíts a beolvasott dokumentumokban.  
- **Kép előfeldolgozás:** Fedezd fel az Aspose `ImageProcessing` API‑ját a dőléskorrekcióra, zajcsökkentésre vagy kontrasztállításra OCR előtt.  
- **Alternatív kimenet:** Használd az `ocrResult.ToPlainText()`‑t, ha csak nyers sztringekre van szükséged metaadatok nélkül.  

Ha érdekelnek más képformátumok, ugyanaz a minta működik PDF‑ekkel (csak cseréld ki a forrásfájlt) vagy PNG‑kkel. A fő tanulság, hogy miután a motor beállításra került, a többi egy ismételhető adatcsővezeték.

---

## Összegzés

Áttekintettünk egy **teljes OCR motor példát**, amely lehetővé teszi a **szöveg kinyerését TIFF** fájlokból az Aspose OCR segítségével, tiszta JSON‑t és opcionális XML‑t generálva bármely downstream munkafolyamat számára. A kód önálló, a magyarázatok pedig lefedik az egyes lépések „miértjeit”.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}