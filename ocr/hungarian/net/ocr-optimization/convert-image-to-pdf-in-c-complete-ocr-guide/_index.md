---
category: general
date: 2025-12-30
description: Kép konvertálása PDF-be az Aspose OCR segítségével C#-ban. Tanulja meg,
  hogyan előfeldolgozza a képet OCR-hez, hogyan ismerje fel a koreai szöveges képet,
  és hogyan hozzon létre gyorsan kereshető PDF-et.
draft: false
keywords:
- convert image to pdf
- preprocess image for ocr
- recognize korean text image
- create searchable pdf image
language: hu
og_description: Kép PDF-re konvertálása az Aspose OCR-rel. Ez az útmutató bemutatja,
  hogyan előfeldolgozzuk a képet OCR-hez, hogyan ismerjük fel a koreai szöveges képet,
  és hogyan hozunk létre kereshető PDF-et.
og_title: Kép konvertálása PDF-be C#-ban – Teljes OCR útmutató
tags:
- C#
- OCR
- Aspose
- PDF
title: Kép konvertálása PDF-be C#-ban – Teljes OCR útmutató
url: /hu/net/ocr-optimization/convert-image-to-pdf-in-c-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kép PDF‑vé konvertálása C#‑ban – Teljes OCR útmutató

Szükséged volt már **convert image to PDF**-re, de azt is szeretted volna, hogy a benne lévő szöveg kereshető legyen? Nem vagy egyedül. Sok fejlesztő ugyanazzal a problémával szembesül a beolvasott oldalak kezelésekor, különösen a koreai nyelven írottak esetén. A jó hír, hogy az Aspose OCR segítségével **preprocess image for OCR**, **recognize Korean text image**, és végül **create searchable PDF image** csak néhány sorban elvégezhető.

Ebben az útmutatóban végigvezetünk az egész folyamaton – a koreai könyvoldal nyers JPEG‑jének betöltésétől, tisztításán, a szöveg kinyeréséig, és mindez egy kereshető PDF‑be csomagolásáig. A végére egy kész‑használatra készen álló C# konzolalkalmazásod lesz, amelyet bármely .NET projektbe beilleszthetsz.

## Amire szükséged lesz

- **.NET 6.0 vagy újabb** (a kód .NET Core‑on és .NET Framework‑ön egyaránt működik)  
- **Aspose.OCR for .NET** NuGet csomag (`Aspose.OCR`) – ingyenes próbaverzió kulcsok elérhetők az Aspose weboldalán.  
- Egy minta kép, amely koreai szöveget tartalmaz (pl. `korean_book_page.jpg`).  
- A választott fejlesztői környezet (Visual Studio, VS Code, Rider – én VS 2022‑t használok).

> **Pro tipp:** Tartsd a képfájljaidat egy dedikált mappában, például `Resources/`, hogy az útvonal minden gépen konzisztens maradjon.

## A folyamat áttekintése

1. **Initialize the OCR engine** GPU‑támogatással a gyorsaság érdekében.  
2. **Add preprocessing filters** (deskew, denoise) a felismerési pontosság javításához.  
3. **Download and load the Korean language model** – az Aspose ezt automatikusan megteszi, ha szükséges.  
4. **Run the recognition** a bemeneti képen.  
5. **Export the result as a searchable PDF** a beépített exporterrel.  
6. **Optional, serialize the result to JSON** további elemzés vagy naplózás céljából.

Az alábbiakban minden lépést részletezünk, elmagyarázzuk, *miért* fontos, és megadjuk a pontos kódot, amelyet másolás‑beillesztéssel használhatsz.

---

## ## Kép PDF‑vé konvertálása – Teljes munkafolyamat

Az alábbi kódrészlet a *teljes* program. Nyugodtan hozz létre egy új konzolprojektet (`dotnet new console -n OcrPdfDemo`), és cseréld le a generált `Program.cs`-t erre a kódra.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;
using Aspose.OCR.Export;
using Aspose.OCR.Result;   // for JsonResult

namespace OcrPdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // Step 1: Initialise the OCR engine (GPU enabled, offline mode off)
            // -----------------------------------------------------------------
            var ocrEngine = new OcrEngine
            {
                UseGpu = true,          // leverages your graphics card for faster inference
                OfflineMode = false    // allows on‑the‑fly language model download
            };

            // --------------------------------------------------------------
            // Step 2: Add preprocessing filters to improve accuracy
            // --------------------------------------------------------------
            // Deskew corrects slight rotations; MaxAngle = 12° is a safe default.
            ocrEngine.Filters.Add(new DeskewFilter { MaxAngle = 12 });

            // Denoise removes isolated speckles that often appear in scanned books.
            ocrEngine.Filters.Add(new DenoiseFilter());

            // --------------------------------------------------------------
            // Step 3: Load the Korean language model
            // --------------------------------------------------------------
            // Aspose will download the model the first time you run this on a new machine.
            ocrEngine.LoadLanguage(LanguageModel.Korean);

            // --------------------------------------------------------------
            // Step 4: Recognise text from the input image
            // --------------------------------------------------------------
            // Replace the path with your actual image location.
            string imagePath = "Resources/korean_book_page.jpg";
            var recognitionResult = ocrEngine.Recognize(imagePath);

            // --------------------------------------------------------------
            // Step 5: Export the recognised page as a searchable PDF
            // --------------------------------------------------------------
            string pdfPath = "Resources/korean_page.pdf";
            var exporter = new SearchablePdfExporter { OutputPath = pdfPath };
            exporter.Export(ocrEngine, imagePath);

            // --------------------------------------------------------------
            // Step 6: Obtain a structured JSON representation of the result
            // --------------------------------------------------------------
            string json = JsonResult.FromRecognitionResult(recognitionResult).ToString(true);
            Console.WriteLine("=== OCR JSON Result ===");
            Console.WriteLine(json);

            Console.WriteLine("\n✅ Conversion complete!");
            Console.WriteLine($"PDF saved to: {pdfPath}");
        }
    }
}
```

### Miért működik ez

- **GPU acceleration** a felismerési időt nagyjából felére csökkenti a csak CPU‑s módhoz képest.  
- **Deskew** és **Denoise** klasszikus *preprocess image for OCR* technikák; kijavítják a gyakori beolvasási hibákat, amelyek egyébként a motor karakterek kihagyásához vezetnek.  
- **Language model loading** elengedhetetlen a **recognize Korean text image** számára – a koreai modell nélkül a motor egy általános latin ábécére vált vissza, és értelmetlen eredményt ad.  
- A **SearchablePdfExporter** az eredeti bitmapet és egy láthatatlan szövegréteget csomagolja, így egy **create searchable pdf image** eredményt kapsz, amelyet bármely PDF‑olvasó indexelhet.

---

## ## Preprocess Image for OCR – Tippek és trükkök

Míg a két szűrő, amit hozzáadtunk, általában elegendő, előfordulhat, hogy makacs képekkel találkozol. Íme néhány további lépés, amelyet kipróbálhatsz:

| Probléma | További szűrő | Hozzáadás módja |
|-------|-------------------|------------|
| Low contrast | `ContrastFilter { Level = 30 }` | `ocrEngine.Filters.Add(new ContrastFilter { Level = 30 });` |
| Heavy background noise | `BinarizationFilter { Threshold = 128 }` | `ocrEngine.Filters.Add(new BinarizationFilter { Threshold = 128 });` |
| Mixed orientation (portrait & landscape) | `OrientationFilter()` | `ocrEngine.Filters.Add(new OrientationFilter());` |

> **Megjegyzés:** Túl sok szűrő hozzáadása lelassíthatja a feldolgozást. Minden változtatást egyetlen oldalon tesztelj, mielőtt nagyobb mennyiségre alkalmaznád.

---

## ## Recognize Korean Text Image – Gyakori buktatók

A koreai írásrendszer Hangul szótagokat tartalmaz, amelyek vizuálisan sűrűek. Ha torz kimenetet észlelsz:

1. **Ensure the language model is fully downloaded** – ellenőrizd a konzolt egy olyan üzenetért, mint a “Downloading Korean model…”.  
2. **Increase the `MaxAngle`** a `DeskewFilter`‑ben, ha a beolvasott képek 12°‑nál nagyobb szögben vannak elforgatva.  
3. **Boost GPU memory** a `ocrEngine.GpuMemoryLimit = 2048;` beállításával (érték MB‑ban).

Ezek a beállítások közvetlenül befolyásolják a **recognize Korean text image** sikerét.

---

## ## Create Searchable PDF Image – Az eredmény ellenőrzése

A program befejezése után nyisd meg a `korean_page.pdf`-t bármely PDF‑olvasóban (Adobe Acrobat Reader, Foxit, akár Chrome). A következőket kell tudnod:

- **Select text** az egérrel, mintha natív PDF lenne.  
- **Search** a beépített keresőmezővel koreai szavakra.

Ha a szövegréteg üresnek tűnik, ellenőrizd, hogy az `Export` metódus a helyes képadat-útvonalat kapta-e, és hogy az OCR eredmény tartalmaz-e nem üres `RecognitionResult.Text`‑et.

---

## ## Full JSON Output – Mit várhatsz

A konzol egy szépen formázott JSON payload‑ot ír ki. Egy levágott példa így néz ki:

```json
{
  "Text": "첫 번째 페이지의 내용...",
  "Blocks": [
    {
      "Text": "첫 번째 페이지의 내용...",
      "BoundingBox": { "X": 12, "Y": 34, "Width": 560, "Height": 780 },
      "Confidence": 0.98
    }
  ],
  "Language": "Korean",
  "ProcessingTimeMs": 842
}
```

---

## ## Hibaelhárítás és GYIK

**Q: A PDF‑em hatalmas a eredeti képhez képest.**  
A: Az exporter az eredeti bitmapet a natív felbontásában ágyazza be. Ha a méret aggály, méretezd le a képet *a* felismerés *előtt*:

```csharp
ocrEngine.Filters.Add(new ResizeFilter { MaxWidth = 1240, MaxHeight = 1754 });
```

**Q: Az OCR üres karakterláncokat ad vissza.**  
A: Ellenőrizd, hogy a képadat-útvonal helyes-e, és a fájl nem sérült. Emellett győződj meg róla, hogy a GPU‑illesztőprogram naprakész; a régebbi driverek csendes hibákat okozhatnak.

**Q: Több oldalt is tudok feldolgozni egy ciklusban?**  
A: Természetesen. A 4‑6. lépéseket egy `foreach (var file in Directory.GetFiles("Resources", "*.jpg"))` ciklusba helyezd, és a kimeneti PDF‑útvonalat ennek megfelelően módosítsd.

---

## ## Összegzés

Most **converted image to PDF**-t hajtottunk végre, miközben a kereshető szöveget megőriztük, mindezt az Aspose OCR erőteljes csővezetékének köszönhetően. A **preprocess image for OCR** segítségével növeled a pontosságot; a **recognize Korean text image** révén kezelsz összetett írásrendszereket; és a **create searchable pdf image** által egy hordozható, indexelhető dokumentumot kapsz.

Vedd a kódot, irányítsd a saját beolvasott képeidre, és kísérletezz további szűrőkkel vagy nyelvi modellekkel. Ugyanez a minta működik kínai, japán vagy bármely latin‑alapú nyelv esetén – csak cseréld le a `LanguageModel.Korean`‑t a megfelelő enumra.

Van még kérdésed? Hagyj megjegyzést, és jó kódolást!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}