---
category: general
date: 2026-09-06
description: OCR kép JSON konvertálás C#-ban az Aspose.OCR használatával – lépésről
  lépésre útmutató a képről szöveg kinyeréséhez és JSON kimenethez.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- ocr image to json
- extract text from image
- convert image to text
- recognize text from photo
- load image for ocr
language: hu
lastmod: 2026-09-06
og_description: OCR kép JSON formátumba C#-ban az Aspose.OCR használatával. Tanulja
  meg, hogyan töltsön be egy képet OCR-hez, ismerje fel a szöveget a fényképről, és
  konvertálja az eredményt JSON-ba.
og_image_alt: Screenshot of C# code that converts an OCR image to JSON using Aspose.OCR
og_title: OCR képet JSON formátumba konvertálni C#-ban – teljes Aspose.OCR útmutató
schemas:
- author: Aspose
  dateModified: '2026-09-06'
  description: ocr image to json conversion in C# using Aspose.OCR – step‑by‑step
    guide to extract text from image and get JSON output.
  headline: How to convert an OCR image to JSON in C# with Aspose.OCR
  type: TechArticle
- description: ocr image to json conversion in C# using Aspose.OCR – step‑by‑step
    guide to extract text from image and get JSON output.
  name: How to convert an OCR image to JSON in C# with Aspose.OCR
  steps:
  - name: Place an image named `input.jpg` in the project root.
    text: Place an image named `input.jpg` in the project root.
  - name: Execute `dotnet run`.
    text: Execute `dotnet run`.
  - name: Observe the console output and open `output.json` to see the structured
      data.
    text: Observe the console output and open `output.json` to see the structured
      data.
  type: HowTo
- questions:
  - answer: Yes. Use `ocrEngine.SaveJson(Stream)` to write directly to a `MemoryStream`,
      then call `stream.ToArray()`.
    question: Can I get the OCR result as a byte array instead of a file?
  - answer: Aspose.OCR can accept PDF pages converted to images via Aspose.PDF, but
      the OCR engine itself works on raster images. Convert PDFs to images first,
      then **load image for ocr**.
    question: Does the engine support PDF input?
  - answer: 'Set `ocrEngine.Language = OcrLanguage.Arabic`. The JSON includes the
      correct text direction, which you can render in UI frameworks that support RTL.
      ## Conclusion You now have a complete solution for **ocr image to json** in
      C#. By loading an image, configuring the language, running the OCR engine, '
    question: How do I handle right‑to‑left scripts like Arabic?
  type: FAQPage
tags:
- Aspose.OCR
- C#
- JSON
- Image processing
title: Hogyan konvertáljunk OCR képet JSON formátumba C#-ban az Aspose.OCR segítségével
url: /hu/net/text-recognition/how-to-convert-an-ocr-image-to-json-in-c-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan konvertáljunk OCR képet JSON formátumba C#-ban az Aspose.OCR segítségével

Ha **ocr image to json** funkcióra van szükséged egy .NET alkalmazásban, ez az útmutató megmutatja, hogyan valósítható meg az Aspose.OCR használatával. Végigvezetünk a kép betöltésén, a szöveg felismerésén a fényképről, és a végeredmény JSON formátumba konvertálásán, hogy az adatot API-k vagy adatbázisok felhasználhassák.

A képfájlokból történő szövegkivonás gyakori igény számlafeldolgozás, nyugtásképzés és archiválási projektek esetén. A tutorial végére képes leszel **convert image to text** műveletre, a nyers szöveg eredményének lekérésére, és egy strukturált JSON payload generálására, amely megőrzi a layout információkat.

## Prerequisites

Mielőtt elkezdenéd, győződj meg róla, hogy rendelkezel:

- .NET 6.0 SDK vagy újabb verzió telepítve  
- Visual Studio 2022 (vagy bármely .NET-et támogató szerkesztő)  
- Aspose.OCR NuGet csomag (`Aspose.OCR`) hozzáadva a projekthez  
- Egy minta kép (`input.jpg`) egy olyan mappában, amelyet a kódból elérhetsz  

Nem szükséges további OCR motor; az Aspose.OCR a nehéz munkát belsőleg elvégzi.

## Step 1: Install the Aspose.OCR NuGet package

Nyiss egy terminált a projekt mappájában, és futtasd:

```bash
dotnet add package Aspose.OCR
```

A csomag tartalmazza az `Aspose.OCR.OcrEngine` osztályt, amely **load image for ocr**, nyelvválasztás és eredményexportálás metódusait biztosítja.

## Step 2: Create a new C# console project

Ha még nincs projekted, hozz létre egyet:

```bash
dotnet new console -n OcrToJsonDemo
cd OcrToJsonDemo
```

Add hozzá a szükséges `using` direktívákat:

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;
using System.IO;
```

## Step 3: Load the image and configure the OCR engine

Az alábbi kód bemutatja, hogyan **load image for ocr**, állítsd be a nyelvet, és készítsd elő a motort a feldolgozáshoz. Ebben a példában cirill betűkészletet használunk, de átállíthatod `OcrLanguage.English`, `OcrLanguage.French` stb.-re a forrásnyelvtől függően.

```csharp
// Step 3: Initialize the OCR engine
var ocrEngine = new OcrEngine();

// Choose the language that matches the text in the image.
// Replace OcrLanguage.Cyrillic with the language you need.
ocrEngine.Language = OcrLanguage.Cyrillic;

// Load the image file. The ImageStream class abstracts file, stream, or byte[] sources.
string imagePath = Path.Combine(Environment.CurrentDirectory, "input.jpg");
ocrEngine.Image = ImageStream.FromFile(imagePath);
```

> **Why this matters:** A megfelelő nyelv beállítása drámaian javítja a pontosságot, amikor **recognize text from photo**-t végzel. A motor nyelvspecifikus szótárakat és karakterkészleteket használ.

## Step 4: Run the OCR process and retrieve results

Most futtasd az OCR motort. Ha a folyamat sikeres, **extract text from image**-t kaphatsz nyers szövegként, HTML‑ként vagy JSON‑ként. Az Aspose.OCR egy `SaveJson` metódust biztosít, amely a strukturált eredményt egy fájlba írja.

```csharp
// Step 4: Execute the OCR process
if (ocrEngine.Process())
{
    // Plain‑text output
    string plainText = ocrEngine.Text;
    Console.WriteLine("=== Plain Text ===");
    Console.WriteLine(plainText);

    // JSON output – includes bounding boxes, confidence scores, and line information
    string jsonPath = Path.Combine(Environment.CurrentDirectory, "output.json");
    ocrEngine.SaveJson(jsonPath);
    Console.WriteLine($"\nJSON result saved to: {jsonPath}");
}
else
{
    Console.WriteLine("OCR processing failed. Check the image path and format.");
}
```

### Expected JSON structure

Egy tipikus `output.json` fájl így néz ki (olvasóbarát formázásban):

```json
{
  "Pages": [
    {
      "PageNumber": 1,
      "Lines": [
        {
          "Text": "Пример текста",
          "Confidence": 0.96,
          "Rect": { "X": 45, "Y": 120, "Width": 210, "Height": 30 }
        },
        {
          "Text": "Еще одна строка",
          "Confidence": 0.93,
          "Rect": { "X": 45, "Y": 160, "Width": 230, "Height": 28 }
        }
      ]
    }
  ]
}
```

A JSON payload tartalmazza minden sor szövegét, egy megbízhatósági pontszámot, valamint a sor eredeti fényképen körülvevő téglalap koordinátáit. Ez megkönnyíti az OCR eredmény visszakapcsolását UI elemekhez vagy adatbázis mezőkhöz.

## Step 5: Full source code for the demo

Az alábbiakban megtalálod a teljes, azonnal futtatható programot, amely elvégzi a **ocr image to json** munkafolyamatot. Másold be a `Program.cs` fájlba, és futtasd a `dotnet run` parancsot.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace OcrToJsonDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize the OCR engine
            var ocrEngine = new OcrEngine();

            // 2️⃣ Select the language (Cyrillic in this example)
            ocrEngine.Language = OcrLanguage.Cyrillic;

            // 3️⃣ Load the image you want to process
            string imagePath = Path.Combine(Environment.CurrentDirectory, "input.jpg");
            if (!File.Exists(imagePath))
            {
                Console.WriteLine($"Image not found: {imagePath}");
                return;
            }
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // 4️⃣ Run the OCR process
            if (ocrEngine.Process())
            {
                // 5️⃣ Retrieve plain text (optional)
                string plainText = ocrEngine.Text;
                Console.WriteLine("=== Plain Text ===");
                Console.WriteLine(plainText);

                // 6️⃣ Save the result as JSON
                string jsonPath = Path.Combine(Environment.CurrentDirectory, "output.json");
                ocrEngine.SaveJson(jsonPath);
                Console.WriteLine($"\nJSON result saved to: {jsonPath}");
            }
            else
            {
                Console.WriteLine("OCR processing failed. Verify the image format and language settings.");
            }
        }
    }
}
```

### Running the example

1. Helyezz el egy `input.jpg` nevű képet a projekt gyökerében.  
2. Futtasd a `dotnet run` parancsot.  
3. Figyeld meg a konzol kimenetét, és nyisd meg az `output.json` fájlt a strukturált adatok megtekintéséhez.

## Pro tips and common pitfalls

| Situation | Recommendation |
|-----------|----------------|
| **Low‑resolution photos** | Növeld a DPI‑t a feldolgozás előtt, vagy használd az `ocrEngine.Image = ImageStream.FromFile(path, 300)` beállítást a 300 DPI kényszerítéséhez. |
| **Mixed languages** | Állítsd be `ocrEngine.Language = OcrLanguage.Multilingual`‑t, és opcionálisan adj meg egy nyelvlistát az `ocrEngine.Language = new[] { OcrLanguage.English, OcrLanguage.Cyrillic }` segítségével. |
| **Large documents** | Dolgozd fel egy oldalonként, hogy alacsony maradjon a memóriahasználat; a motor támogatja a többoldalas TIFF‑eket. |
| **Incorrect characters** | Ellenőrizd, hogy a megfelelő `OcrLanguage` van kiválasztva; a rossz nyelv kiválasztása csökkenti a pontosságot, amikor **convert image to text**-t végzel. |
| **JSON missing fields** | Győződj meg róla, hogy az Aspose.OCR 23.6 vagy újabb verzióját használod; a régebbi kiadások nem tartalmazták a `SaveJson` metódust. |

## Frequently asked questions

**Q: Can I get the OCR result as a byte array instead of a file?**  
A: Igen. Használd az `ocrEngine.SaveJson(Stream)` metódust, hogy közvetlenül egy `MemoryStream`‑be írd, majd hívd meg a `stream.ToArray()`‑t.

**Q: Does the engine support PDF input?**  
A: Az Aspose.OCR képes PDF oldalakat képekké konvertálni az Aspose.PDF segítségével, de magát az OCR motort csak raszteres képeken lehet futtatni. Konvertáld a PDF‑eket képekké, majd **load image for ocr**.

**Q: How do I handle right‑to‑left scripts like Arabic?**  
A: Állítsd be `ocrEngine.Language = OcrLanguage.Arabic`. A JSON tartalmazza a helyes szövegirányt, amelyet RTL‑t támogató UI keretrendszerekben megjeleníthetsz.

## Conclusion

Most már egy komplett megoldásod van a **ocr image to json** feladatra C#‑ban. Képet betöltve, nyelvet konfigurálva, az OCR motort futtatva és az eredményt JSON‑ként exportálva **extract text from image**, **convert image to text**, és **recognize text from photo** műveleteket egyetlen, egyszerű munkafolyamatban végezheted el.  

Innen tovább:

- A JSON kimenet integrálása egy Web API‑val (`ASP.NET Core`)  
- Az eredmény tárolása NoSQL adatbázisban, például MongoDB‑ben  
- Utófeldolgozás hozzáadása a gyakori OCR hibák javításához  

Nyugodtan kísérletezz különböző nyelvekkel, képformátumokkal és kimeneti opciókkal, hogy a projekted igényeihez legjobban illeszkedjen. Boldog kódolást!

## What Should You Learn Next?

A következő tutorialok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás komplett, működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsenek további API funkciók elsajátításában és alternatív megvalósítási megközelítések felfedezésében saját projektjeidben.

- [recognize text from image in C# – Complete Guide to OCR and JSON](/ocr/english/net/text-recognition/recognize-text-from-image-in-c-complete-guide-to-ocr-and-jso/)
- [Convert Image to Text in C# with Aspose OCR – Step‑by‑Step Guide](/ocr/english/net/text-recognition/convert-image-to-text-in-c-with-aspose-ocr-step-by-step-guid/)
- [How to Extract Text from Image Using Aspose.OCR for .NET](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}