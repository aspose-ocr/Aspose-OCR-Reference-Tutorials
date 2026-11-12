---
category: general
date: 2026-04-03
description: Szöveg felismerése képről Aspose OCR használatával C#-ban. Tanulja meg,
  hogyan töltsön be képet OCR-hez, hogyan vonjon ki szöveget a képből, hogyan írjon
  JSON fájlt C#-ban, és hogyan végezzen OCR-t PNG-en.
draft: false
keywords:
- recognize text from image
- write json file c#
- load image for ocr
- extract text from image
- perform ocr on png
language: hu
og_description: Aspose OCR használata C#-ban a képen lévő szöveg felismeréséhez. Lépésről
  lépésre útmutató a kép betöltéséhez OCR-hez, a szöveg kinyeréséhez a képből, JSON
  fájl írásához C#-ban, és OCR végrehajtásához PNG-n.
og_title: Szöveg felismerése képről C#-ban – Teljes Aspose OCR útmutató
tags:
- OCR
- C#
- Aspose
title: Szöveg felismerése képről C#-ban – Teljes Aspose OCR útmutató
url: /hu/net/text-recognition/recognize-text-from-image-in-c-full-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# szöveg felismerése képről C#‑ban – Teljes Aspose OCR útmutató

Valaha is szükséged volt **szöveg felismerésére képről**, de nem tudtad, melyik könyvtárat válaszd? Lehet, hogy egy csomó beolvasott nyugtát, egy PNG képernyőképet vagy egy kézzel írott jegyzetet szeretnél kereshető adatokká alakítani. A jó hír: az Aspose.OCR‑rel néhány C# sorral megoldható, és még egy rendezett JSON fájlt is kapsz, amit más rendszereknek átadhatsz.

Ebben az útmutatóban végigvezetünk a kép betöltésén OCR‑hez, a szöveg kinyerésén, az eredmény JSON‑ba sorosításán, és végül a PNG fájlok kezelésén anélkül, hogy izzadnál. A végére egy azonnal futtatható konzolos alkalmazást kapsz, amely **szöveget felismer képről**, és az eredményt az *output.json* fájlba írja.

## Amire szükséged lesz

- .NET 6.0 vagy újabb (a kód .NET Framework‑ön is működik)
- Aspose.OCR NuGet csomag (`Install-Package Aspose.OCR`)
- Egy PNG (vagy bármely támogatott formátum), amelyet feldolgozni szeretnél
- Visual Studio, VS Code vagy bármely kedvenc C# szerkesztő

Nem szükséges további harmadik féltől származó könyvtár – csak az Aspose OCR motor és a beépített `System.Text.Json` sorosító.

## 1. lépés: Szöveg felismerése képről az Aspose OCR‑rel

Az első teendő egy `OcrEngine` példány létrehozása. Ez az objektum végzi a nehéz munkát a háttérben.

```csharp
using Aspose.OCR;
using System.Drawing;
using System.IO;
using System.Text.Json;

class JsonExportDemo
{
    static void Main()
    {
        // Initialize the OCR engine – this is where the magic starts.
        OcrEngine ocrEngine = new OcrEngine();

        // Load the image for OCR – replace the path with your own file.
        Image sourceImage = Image.FromFile(@"YOUR_DIRECTORY/input.png");

        // Perform OCR on the loaded image and get a structured result.
        OcrResult ocrResult = ocrEngine.RecognizeToResult(sourceImage);

        // Serialize the result into a nicely indented JSON string.
        string json = JsonSerializer.Serialize(
            ocrResult,
            new JsonSerializerOptions { WriteIndented = true });

        // Write JSON file C# – this will create output.json next to your exe.
        File.WriteAllText(@"YOUR_DIRECTORY/output.json", json);
    }
}
```

**Miért fontos:** Az `OcrEngine` egyszeri példányosítása és újrahasználata hatékonyabb, mint minden fájlhoz új motor létrehozása. A `RecognizeToResult` hívás egy `OcrResult` objektumot ad vissza, amely már tartalmazza a kinyert szöveget, a megbízhatósági pontszámokat és a határoló dobozokat – tökéletes a további feldolgozáshoz.

## 2. lépés: Kép betöltése OCR‑hez – különböző formátumok kezelése

Az Aspose OCR képes PNG, JPEG, BMP és még sok más formátum olvasására. Ha egy átlátszóságot tartalmazó PNG‑vel dolgozol, érdemes először laposra konvertálni, hogy elkerüld a váratlan üres részeket.

```csharp
// Optional: flatten PNG with transparency to a white background.
if (sourceImage.RawFormat.Equals(System.Drawing.Imaging.ImageFormat.Png))
{
    Bitmap flat = new Bitmap(sourceImage.Width, sourceImage.Height);
    using (Graphics g = Graphics.FromImage(flat))
    {
        g.Clear(Color.White);
        g.DrawImage(sourceImage, 0, 0);
    }
    sourceImage = flat;
}
```

**Pro tipp:** Mindig ellenőrizd, hogy a kép méretei ésszerűek legyenek (pl. szélesség > 50 px). Nagyon kis képek esetén az OCR motor kihagyhat karaktereket, ami alacsony megbízhatósági pontszámokhoz vezet.

## 3. lépés: JSON fájl írása C#‑ban – a kimenet felhasználhatóvá tétele

A `System.Text.Json` sorosító gyors és beépített, de cserélhető `Newtonsoft.Json`‑ra, ha egyedi konverterekre van szükséged. A fenti példa már `WriteIndented = true` beállítással rendelkezik, így a kapott fájl emberi olvasásra alkalmas.

```csharp
// Expected output (truncated):
{
  "Text": "Hello World",
  "Pages": [
    {
      "PageNumber": 1,
      "Lines": [
        {
          "Text": "Hello World",
          "Confidence": 0.98,
          "BoundingBox": { "X": 10, "Y": 20, "Width": 120, "Height": 30 }
        }
      ]
    }
  ]
}
```

Az OCR adatok JSON‑ban való tárolása lehetővé teszi a könnyű importálást adatbázisokba, HTTP‑n keresztüli küldést, vagy gépi tanulási csővezetékekbe való betáplálást.

## 4. lépés: Az eredmény ellenőrzése – gyors sanity check

A program futtatása után nyisd meg az `output.json` fájlt, és keresd a `"Text"` mezőt. Ha a várt szöveget tartalmazza, sikeresen **kivetted a szöveget képről**. Ha a megbízhatóság alacsony, fontold meg a kép előfeldolgozását (pl. kontraszt növelése vagy bináris küszöb alkalmazása).

```csharp
Console.WriteLine($"Extracted text: {ocrResult.Text}");
Console.WriteLine($"Overall confidence: {ocrResult.Confidence:P2}");
```

A konzol valami ilyesmit fog kiírni:

```
Extracted text: Hello World
Overall confidence: 98.00%
```

Ez egy erős jelzés arra, hogy az OCR a tervek szerint működött.

## Gyakori hibák és széljegyek

| Probléma | Miért fordul elő | Hogyan javítsuk |
|----------|------------------|-----------------|
| **Üres kimenet** | A kép túl sötét vagy nem támogatott színteret használ | Konvertáld szürkeárnyalatba, növeld a fényerőt, vagy laposra tedd a PNG‑t (lásd 2. lépés) |
| **Rossz karakterek** | Alacsony DPI (< 72) vagy erős zaj | Növeld a kép felbontását, vagy alkalmazz zajszűrőt a `RecognizeToResult` előtt |
| **Nagy fájlok memória nyomást okoznak** | Több megabájtos PNG betöltése `Bitmap`‑ként sok RAM‑ot fogyaszt | Dolgozd fel a képeket darabokban, vagy méretezd le őket úgy, hogy a olvashatóság megmaradjon |
| **JSON sorosítási hiba** | Az `OcrResult` körkörös hivatkozásokat tartalmaz (ritka) | Használd a `JsonSerializerOptions { ReferenceHandler = ReferenceHandler.IgnoreCycles }` beállítást |

## Bónusz: OCR végrehajtása PNG‑kön kötegelt ciklusban

Ha egy mappában sok PNG fájl van, a demót kibővítheted, hogy mindegyiken végigmenjen:

```csharp
string[] pngFiles = Directory.GetFiles(@"YOUR_DIRECTORY", "*.png");
foreach (var file in pngFiles)
{
    Image img = Image.FromFile(file);
    OcrResult res = ocrEngine.RecognizeToResult(img);
    string outPath = Path.ChangeExtension(file, ".json");
    File.WriteAllText(outPath, JsonSerializer.Serialize(res, new JsonSerializerOptions { WriteIndented = true }));
    Console.WriteLine($"Processed {Path.GetFileName(file)} → {Path.GetFileName(outPath)}");
}
```

Most a program **OCR‑t hajt végre PNG fájlokon** tömegesen, és minden képhez egy megfelelő JSON fájlt ír.

## Összegzés

Most már tudod, hogyan **szöveget felismerj képről C#‑ban az Aspose OCR‑rel**, **képet tölts be OCR‑hez**, **szöveget nyerj ki képről**, és **JSON fájlt írj C#‑ban** a végeredmény tárolásához. A teljes, futtatható példa lefedi az alapvető lépéseket, elmagyarázza, miért fontos minden részlet, és még a PNG‑specifikus sajátosságok kezelését is bemutatja.

Mi a következő lépés? Próbáld meg a JSON‑t keresőindexbe betölteni, kombináld nyelvfelismeréssel, vagy integráld egy webes API‑ba, amely élő feltöltéseket dolgoz fel. Érdemes továbbá felfedezni az Aspose kézírás‑felismerés támogatását, ha az a te esetedben releváns.

Van kérdésed a széljegyekkel vagy a teljesítményhangolással kapcsolatban? Írj kommentet alább – jó kódolást!

![szöveg felismerése képről bemutató](/images/ocr-demo.png "Diagram, amely azt mutatja, hogyan ismeri fel az Aspose OCR a szöveget képről")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}