---
category: general
date: 2026-01-12
description: c# OCR útmutató, amely bemutatja, hogyan ismerj fel szöveges képet, hogyan
  extraháld a szöveget C#-ban, és hogyan generálj képből PDF OCR fájlt bizalmi pontszámokkal.
draft: false
keywords:
- c# ocr tutorial
- image to pdf ocr
- recognize text image
- ocr confidence scores
- extract text image c#
language: hu
og_description: Ismerj meg egy teljes C# OCR útmutatót a szöveges képek felismeréséhez,
  a szöveg kinyeréséhez C#-ban, és egy kép PDF OCR dokumentummá alakításához megbízhatósági
  pontszámokkal.
og_title: c# OCR útmutató – Képek konvertálása kereshető PDF-ekre
tags:
- OCR
- C#
- PDF
title: c# OCR útmutató – Képek átalakítása kereshető PDF-ekbe
url: /hu/net/text-recognition/c-ocr-tutorial-turn-images-into-searchable-pdfs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr tutorial – Képek átalakítása kereshető PDF‑ekké

Gondoltad már, hogyan **szkenneld fel a szöveges képeket** egy C# projektben anélkül, hogy harmadik fél szolgáltatásait keresnéd? Nem vagy egyedül. Sok valós alkalmazásban – gondoljunk csak a számlaszkennerre, a nyugták nyomon követésére vagy a többnyelvű dokumentumarchívumokra – a fejlesztőknek megbízható, helyi OCR motorra van szükségük, amely még a bizalmi pontszámokat is kiadja.  

Ez a **c# ocr tutorial** végigvezet mindenen, amire szükséged van: a kép betöltésétől, a nyelvi modellek kiválasztásán, a GPU gyorsítás be‑ és kikapcsolásán, egészen a kereshető PDF‑ként való mentésig. A végére egy azonnal futtatható kódmintát kapsz, amely kinyeri a szöveget, jelentést készít az OCR biztonságról, és opcionálisan létrehoz egy *image to pdf ocr* fájlt – mindezt egy perc alatt.

## Mit fogsz építeni

- Tölts be egy többnyelvű képet (`sample_multi_lang.jpg` helyőrzőként van használva).  
- Válaszd ki az arab, hindi és orosz nyelvi modelleket (továbbiakat is hozzáadhatsz).  
- Kapcsold be a GPU feldolgozást, ha a géped támogatja.  
- Szerezd meg a nyers OCR eredményt **bizalmi pontszámokkal**.  
- Sorold a eredményt szépen formázott JSON‑ba **vagy** írj ki egy kereshető PDF‑et.  

## Előfeltételek

- .NET 6.0 vagy újabb (a kód .NET Core‑on és .NET Framework‑ön is lefordítható).  
- Visual Studio 2022 (vagy bármely kedvelt IDE).  
- Aspose.OCR for .NET licenc (az ingyenes próba verzió teszteléshez használható).  
- Opcionális: CUDA‑kompatibilis GPU, ha gyorsítani szeretnéd a felismerést.

> **Pro tipp:** Ha nincs GPU-d, egyszerűen állítsd be a `UseGpu = false` értéket, és a motor CPU‑ra vált vissza kódbeli módosítás nélkül.

## 1. lépés: A szükséges NuGet csomagok telepítése

Nyisd meg a **Package Manager Console**‑t, és futtasd:

```powershell
Install-Package Aspose.OCR
Install-Package Aspose.OCR.Gpu
Install-Package Newtonsoft.Json
```

Ezek a három csomag biztosítja az OCR motort, a GPU gyorsítást, és egy szép JSON sorosítót a bizalmi kimenethez.

## 2. lépés: A projekt struktúrájának beállítása

Hozz létre egy új konzolos projektet (`dotnet new console -n AsposeOcrDemo`) és cseréld le a generált `Program.cs`‑t az alábbi kóddal.  
Minden logika a `Program` osztályban található; az egyetlen extra típus egy kis kiterjesztési metódus, amely az OCR eredményt JSON‑ra formázza.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Gpu;
using Aspose.OCR.Models;
using Newtonsoft.Json;

namespace AsposeOcrDemo
{
    class Program
    {
        // Step 1: Input image and language models
        private const string InputImagePath = @"YOUR_DIRECTORY/sample_multi_lang.jpg";
        private static readonly string[] Languages = { LanguageModel.Arabic, LanguageModel.Hindi, LanguageModel.Russian };

        // Step 2: Processing options (GPU toggle & output format)
        private const bool UseGpu = true;               // set false if no GPU
        private const string OutputFormat = "Json";     // change to "Pdf" for PDF output

        static void Main()
        {
            // Step 3: Initialise the appropriate OCR engine
            IOcrEngine engine = UseGpu ? (IOcrEngine)new GpuOcrEngine() : new OcrEngine();

            // Step 4: Run OCR – language models are auto‑downloaded if missing
            OcrResult result = engine.Recognize(
                InputImagePath,
                new OcrOptions { LanguageModels = Languages, AutoDownloadResources = true });

            // Step 5: Emit the result in the chosen format
            if (OutputFormat.Equals("json", StringComparison.OrdinalIgnoreCase))
            {
                string json = JsonConvert.SerializeObject(
                    result.GetWordsWithConfidence(),
                    Formatting.Indented);
                Console.WriteLine(json);
            }
            else if (OutputFormat.Equals("pdf", StringComparison.OrdinalIgnoreCase))
            {
                string pdfPath = Path.ChangeExtension(InputImagePath, ".pdf");
                File.WriteAllBytes(pdfPath, result.Pdf);
                Console.WriteLine($"PDF saved to: {pdfPath}");
            }
        }
    }

    // Helper that flattens OcrResult into a JSON‑friendly structure
    internal static class OcrResultExtensions
    {
        public static object GetWordsWithConfidence(this OcrResult result)
        {
            var words = new System.Collections.Generic.List<object>();
            foreach (var w in result.Words)
                words.Add(new
                {
                    Text = w.Text,
                    Confidence = w.Confidence,
                    BoundingBox = new { w.Bounds.X, w.Bounds.Y, w.Bounds.Width, w.Bounds.Height }
                });

            return new
            {
                RecognizedText = result.Text,
                LanguageModels = result.UsedLanguageModels,
                Words = words,
                ProcessingTimeMs = result.ProcessingTime.TotalMilliseconds
            };
        }
    }
}
```

### Miért működik ez a kód

1. **GPU kapcsoló** – A `GpuOcrEngine` a CUDA magokat használja; a ternáris operátor egyszerűvé teszi a váltást.  
2. **Automatikus nyelvi letöltés** – Az `AutoDownloadResources = true` biztosítja, hogy az arab, hindi és orosz modellek az első futtatáskor letöltődjenek.  
3. **Bizalmi pontszámok** – A `result.Words` minden felismert szóhoz tartalmaz egy `Confidence` értéket; a kiterjesztési metódus ezeket egy tiszta JSON objektummá formázza.  
4. **Kereshető PDF** – A `result.Pdf` már egy teljesen kereshető PDF, így csak a byte tömböt írjuk lemezre. Nincs szükség extra könyvtárakra.

## 6. lépés: A minta futtatása

Nyiss egy terminált, navigálj a projekt mappájába, és hajtsd végre:

```bash
dotnet run
```

Ha **JSON** kimenetet választottál, valami ilyesmit látsz majd:

```json
{
  "RecognizedText": "مرحبا Hello Привет",
  "LanguageModels": [
    "Arabic",
    "Hindi",
    "Russian"
  ],
  "Words": [
    {
      "Text": "مرحبا",
      "Confidence": 0.98,
      "BoundingBox": { "X": 45, "Y": 12, "Width": 120, "Height": 30 }
    },
    {
      "Text": "Hello",
      "Confidence": 0.99,
      "BoundingBox": { "X": 180, "Y": 12, "Width": 80, "Height": 30 }
    },
    {
      "Text": "Привет",
      "Confidence": 0.97,
      "BoundingBox": { "X": 280, "Y": 12, "Width": 110, "Height": 30 }
    }
  ],
  "ProcessingTimeMs": 312
}
```

Ha **PDF**‑re váltottál, a konzol kiírja az elérési utat, és a forráskép mellett megtalálod a kereshető PDF‑et.

## Gyakori kérdések és szélsőséges esetek

- **Mi van, ha egy nyelvi modell nem elérhető?**  
  Az OCR motor egyértelmű `ResourceNotFoundException`‑t dob. Mivel az `AutoDownloadResources = true`‑t állítottuk be, a hiányzó modell automatikusan letöltődik az első futtatáskor, így a kivétel a termelésben ritkán jelentkezik.

- **Feldolgozhatok egy képköteget?**  
  Természetesen. A `engine.Recognize` hívást egy `foreach` ciklusba teheted, amely egy könyvtárban lévő fájlok felett iterál. Az ugyanaz a `OcrResultExtensions` minden képre működik.

- **Szükség van licencre a GPU‑hoz?**  
  Nem. Az ingyenes próba mind CPU, mind GPU esetén működik. A teljes licenc eltávolítja a próba‑vízjelet és feloldja az oldalszám‑korlátozásokat.

- **Mennyire pontosak a bizalmi pontszámok?**  
  A pontszámok 0,0‑tól (nincs bizalom) 1,0‑ig (tökéletes bizalom) terjednek. Gyakorlatban a 0,90‑nél magasabb értékek megbízhatóak a további feldolgozáshoz; alacsonyabb bizalmi szavakat szűrheted, ha szigorúbb validációra van szükség.

## 7. lépés: Következő lépések (Bővítsd az OCR eszköztárad)

1. **További nyelvek hozzáadása** – egyszerűen add hozzá a `LanguageModel.French` (vagy bármely támogatott modell) a `Languages` tömbhöz.  
2. **OCR kombinálása PDF/A konverzióval** – Az Aspose.PDF beágyazhatja az OCR réteget egy PDF/A‑2b kompatibilis dokumentumba archiválás céljából.  
3. **Integrálás Azure Functions‑szel** – csomagold a logikát egy szerver nélküli végpontra, hogy valós időben feldolgozza a feltöltéseket.  
4. **A bizalmi küszöbök finomhangolása** – használd a `result.Words.Where(w => w.Confidence < 0.85)` kifejezést, hogy a bizonytalan szavakat manuális ellenőrzésre jelöld.

---

### TL;DR

Ez a **c# ocr tutorial** megmutatja, hogyan:

- Kép betöltése és több nyelvi modell kiválasztása.  
- GPU gyorsítás bekapcsolása egyetlen logikai kapcsolóval.  
- OCR eredmények **bizalmi pontszámokkal** lekérése és JSON‑ba sorolása.  
- Opcionálisan kereshető PDF írása (**image to pdf ocr**).  

Mindez néhány sor kóddal, egy ingyenes Aspose.OCR próba verzióval és a fenti kóddal megvalósítható. Próbáld ki, finomítsd a nyelvi listát, és percek alatt egy termelés‑kész OCR csővezetéked lesz.

![c# ocr tutorial példakép](https://example.com/placeholder-image.jpg "c# ocr tutorial példakép")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}