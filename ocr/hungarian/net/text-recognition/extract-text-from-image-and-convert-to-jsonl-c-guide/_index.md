---
category: general
date: 2026-01-02
description: Képből szöveg kinyerése Aspose OCR-rel C#-ban. Tanulja meg, hogyan konvertálja
  a képet gyorsan és megbízhatóan JSONL formátumba.
draft: false
keywords:
- extract text from image
- convert image to jsonl
language: hu
og_description: Képek szövegének kinyerése az Aspose OCR-rel, és átalakítása JSONL
  formátumba. Teljes lépésről‑lépésre C# oktatóanyag fejlesztőknek.
og_title: Képből szöveg kinyerése – JSONL formátumba konvertálás C#-ban
tags:
- C#
- OCR
- Aspose
- JSONL
title: Szöveg kinyerése képből és konvertálása JSONL formátumba – C# útmutató
url: /hu/net/text-recognition/extract-text-from-image-and-convert-to-jsonl-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Szöveg kinyerése képből és konvertálása JSONL formátumba – Teljes C# oktatóanyag

Volt már szükséged **szöveg kinyerésére képből**, de nem tudtad, melyik könyvtár adna tiszta, strukturált kimenetet? Nem vagy egyedül. Sok számlafeldolgozó vagy dokumentum‑digitalizációs projektben a szűk keresztmetszet a bitmap átalakítása kereshető szöveggé *és* gép‑olvasható formátummá.  

A jó hír? Az Aspose OCR‑val **szöveget nyerhetsz ki képből**, és néhány kódsorral **konvertálhatod a képet JSONL‑be** a további elemzésekhez. Ez az útmutató végigvezet a teljes folyamaton, a PNG betöltésétől egy JSON‑Lines fájl írásáig, amely adatcsővezetékbe streamelhető.

> **Hint:** Ha már .NET 6‑ot vagy újabbat használsz, ugyanaz a kód további konfiguráció nélkül működik.

## Előfeltételek — Amire szükséged lesz

- **.NET 6 SDK** (vagy bármely friss .NET verzió)
- **Aspose.OCR** NuGet csomag  
  ```bash
  dotnet add package Aspose.OCR
  ```
- **Newtonsoft.Json** a sorosításhoz  
  ```bash
  dotnet add package Newtonsoft.Json
  ```
- Egy mintakép (pl. `receipt.png`), amelyet egy hivatkozható mappában helyezel el.
- Egy tetszőleges IDE vagy szerkesztő – Visual Studio, VS Code, Rider, stb.

Nincs nehéz beállítás, nincs külső szolgáltatás, csak néhány NuGet csomag.

![Extract text from image using C#](https://example.com/assets/ocr-sample.png)

*Alt szöveg: szöveg kinyerése képből C#‑vel az Aspose OCR használatával*

## 1. lépés: A feldolgozni kívánt kép betöltése  

Az első dolog, amit megteszel, amikor **szöveget szeretnél kinyerni képből**, az, hogy egy bitmapet adsz az OCR motornak. A `System.Drawing.Bitmap` használata egyszerű, és a legtöbb raszteres formátumhoz működik.

```csharp
using System.Drawing;

// Adjust the path to where your receipt.png lives
string imagePath = @"C:\MyProjects\OCRDemo\receipt.png";
Bitmap receiptImage = new Bitmap(imagePath);
```

> **Miért fontos:** A kép `Bitmap`‑ként történő betöltése közvetlen pixelhozzáférést biztosít az OCR motor számára, ami javítja a felismerés sebességét és pontosságát a nyers bájtok streameléséhez képest.

## 2. lépés: Aspose OCR konfigurálása JSON‑Lines kimenethez  

Az Aspose OCR lehetővé teszi a nyelv, a kimeneti formátum és néhány teljesítménybeállítás megadását. Itt **JSON‑Lines**‑t kérünk (egy JSON objektum soronként), mivel ez később tökéletes a sor‑soron történő feldolgozáshoz.

```csharp
using Aspose.OCR;

// Create the engine
OcrEngine ocrEngine = new OcrEngine();

// Tell the engine we’re dealing with English text
RecognitionOptions options = new RecognitionOptions
{
    Language = Language.English,
    OutputFormat = OutputFormat.JsonLines   // This is the key for converting image to JSONL
};
```

> **Pro tipp:** Ha többnyelvű számlákra van szükséged, állítsd be a `Language = Language.Multilingual` értéket, vagy adj át egy `Language` értékekből álló tömböt.

## 3. lépés: Az OCR futtatása és az eredmény rögzítése  

Most már ténylegesen **szöveget nyerünk ki képből**. A `Recognize` metódus egy `OcrResult` objektumot ad vissza, amely `OcrLine` objektumok gyűjteményét tartalmazza, mindegyik egy felismert szövegsort és a hozzá tartozó keretet reprezentálja.

```csharp
// Perform OCR
OcrResult ocrResult = ocrEngine.Recognize(receiptImage, options);
```

Ebben a pontban az `ocrResult.Lines` tartalmazza a szükséges adatokat – nyers szöveget, bizalmi értékeket és koordinátákat.

## 4. lépés: A sorok sorosítása JSON‑Lines formátumba  

A gyűjteményt egy szépen formázott JSON karakterlánccá alakítjuk. Bár a JSON‑Lines általában kompakt, a behúzás hozzáadása megkönnyíti a fájl vizsgálatát fejlesztés közben.

```csharp
using Newtonsoft.Json;

// Serialize each line as a separate JSON object
string jsonLines = JsonConvert.SerializeObject(
    ocrResult.Lines,
    Formatting.Indented
);
```

Az eredményül kapott `jsonLines` változó valahogy így néz ki (rövidítve a tömörség kedvéért):

```json
{
  "Text": "Store XYZ",
  "Confidence": 0.98,
  "BoundingBox": { "X": 10, "Y": 15, "Width": 120, "Height": 20 }
}
{
  "Text": "Date: 01/01/2026",
  "Confidence": 0.95,
  "BoundingBox": { "X": 10, "Y": 45, "Width": 180, "Height": 20 }
}
```

Minden sor egy újsor karakterrel végződik, így egy valódi **JSONL** (JSON‑Lines) fájlt kapsz.

## 5. lépés: A JSON‑Lines írása lemezre  

Végül elmentjük a kimenetet, hogy más szolgáltatások – például Spark, Logstash vagy egy egyszerű Bash script – soronként be tudják olvasni.

```csharp
using System.IO;

// Choose a destination file
string outputPath = @"C:\MyProjects\OCRDemo\receipt.jsonl";
File.WriteAllText(outputPath, jsonLines);
```

Amikor megnyitod a `receipt.jsonl` fájlt, soronként egy JSON objektumot látsz, készen a streamelésre.

## 6. lépés: Az export ellenőrzése  

Egy gyors ellenőrzés órákat takarít meg a későbbi hibakeresésben. Olvassuk be az első néhány sort, és írjuk ki a konzolra.

```csharp
Console.WriteLine("First three lines of the JSONL output:");
foreach (var line in File.ReadLines(outputPath).Take(3))
{
    Console.WriteLine(line);
}
```

Tipikus konzol kimenet:

```
First three lines of the JSONL output:
{"Text":"Store XYZ","Confidence":0.98,"BoundingBox":{"X":10,"Y":15,"Width":120,"Height":20}}
{"Text":"Date: 01/01/2026","Confidence":0.95,"BoundingBox":{"X":10,"Y":45,"Width":180,"Height":20}}
{"Text":"Total   $23.45","Confidence":0.97,"BoundingBox":{"X":10,"Y":75,"Width":150,"Height":20}}
```

Ha hasonlót látsz, gratulálok – sikeresen **kivontad a szöveget a képből** és **konvertáltad a képet JSONL‑be**.

## Gyakori hibák és hogyan kerüld el őket  

| Probléma | Miért fordul elő | Megoldás |
|----------|------------------|----------|
| **Üres kimenet** | A kép útvonala helytelen vagy a fájl nem olvasható. | Használd a `File.Exists(imagePath)` ellenőrzést a bitmap létrehozása előtt. |
| **Alacsony bizalmi értékek** | A kép elmosódott vagy alacsony kontrasztú. | Előfeldolgozd a képet (pl. `Bitmap.RotateFlip`, `Graphics.Clear`) vagy növeld a DPI‑t. |
| **Helytelen nyelv** | Az OCR alapértelmezés szerint angol, de a számla más nyelven van. | Állítsd be a `options.Language = Language.Spanish` értéket (vagy a megfelelő enumot). |
| **A JSONL egyetlen JSON tömbként jelenik meg** | `Formatting.None`-t használtál újsor kezelés nélkül. | Győződj meg róla, hogy minden sorosított objektum `Environment.NewLine`-nel végződik. |

## Teljes működő példa  

Az alábbiakban a teljes, azonnal futtatható program látható. Illeszd be egy konzol projektbe, és nyomd meg az **F5**‑öt.

```csharp
using Aspose.OCR;
using System;
using System.Drawing;
using System.IO;
using System.Linq;
using Newtonsoft.Json;

namespace OcrToJsonlDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the image
            string imagePath = @"C:\MyProjects\OCRDemo\receipt.png";
            if (!File.Exists(imagePath))
            {
                Console.WriteLine($"Image not found at {imagePath}");
                return;
            }
            Bitmap receiptImage = new Bitmap(imagePath);

            // 2️⃣ Set up OCR options for JSON‑Lines output
            OcrEngine ocrEngine = new OcrEngine();
            RecognitionOptions options = new RecognitionOptions
            {
                Language = Language.English,
                OutputFormat = OutputFormat.JsonLines
            };

            // 3️⃣ Perform OCR
            OcrResult ocrResult = ocrEngine.Recognize(receiptImage, options);

            // 4️⃣ Serialize to JSON‑Lines
            string jsonLines = JsonConvert.SerializeObject(
                ocrResult.Lines,
                Formatting.Indented
            );

            // 5️⃣ Write to file
            string outputPath = @"C:\MyProjects\OCRDemo\receipt.jsonl";
            File.WriteAllText(outputPath, jsonLines);
            Console.WriteLine($"✅ JSONL saved to {outputPath}");

            // 6️⃣ Quick verification
            Console.WriteLine("\nFirst three lines of output:");
            foreach (var line in File.ReadLines(outputPath).Take(3))
            {
                Console.WriteLine(line);
            }
        }
    }
}
```

**Várható eredmény:** Egy `receipt.jsonl` fájl, amely soronként egy JSON objektumot tartalmaz, mindegyik `Text`, `Confidence` és `BoundingBox` mezőkkel. Ezt a fájlt most már bármely JSONL‑t fogyasztó elemzési csővezetékbe betáplálhatod.

## Következő lépések – Alap OCR‑n túl  

- **Kötegelt feldolgozás:** Csomagold be a fenti logikát egy `foreach` ciklusba, hogy teljes számlamappákat kezelj.  
- **Párhuzamosság:** Használd a `Parallel.ForEach`‑t többmagos gyorsításokhoz, ha több ezer képpel dolgozol.  
- **Utófeldolgozás:** Távolítsd el az alacsony bizalmi értékű sorokat (`Confidence < 0.9`) a tárolás előtt.  
- **Integráció:** Küldd a JSONL‑t közvetlenül az Azure Blob Storage‑ba vagy az AWS S3‑ba a megfelelő SDK‑kkal.  
- **Alternatív formátumok:** Válts `OutputFormat`‑ra `PlainText` vagy `Xml` értékre, ha a downstream rendszer ezeket részesíti előnyben.  

## Összegzés  

Most már egy szilárd, végponttól végpontig terjedő megoldással rendelkezel a **szöveg kinyerésére képből** és a **kép JSONL‑be konvertálására** az Aspose OCR használatával C#‑ban. Az oktatóanyag mindent lefedett a bitmap betöltésétől a kimenet ellenőrzéséig, valamint néhány gyakorlati tippet a csővezeték robusztusságának biztosításához.  

Próbáld ki a saját számláiddal, bizonylataiddal vagy beolvasott űrlapjaiddal – figyeld, ahogy az OCR motor a pixeleket kereshető, sor‑struktúrájú adatokra alakítja másodpercek alatt. Ha szélhelyzetekkel (pl. ferde beolvasások vagy többnyelvű szöveg) találkozol, nézd át újra a *RecognitionOptions* részt, és finomíts a nyelven vagy az előfeldolgozási lépéseken.  

Boldog kódolást, és legyenek adatszövegeid mindig tiszták!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}