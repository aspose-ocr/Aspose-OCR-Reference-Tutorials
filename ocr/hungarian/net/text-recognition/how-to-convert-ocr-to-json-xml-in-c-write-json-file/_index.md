---
category: general
date: 2026-04-01
description: Hogyan konvertáljuk az OCR kimenetet JSON és XML formátumba C#-ban –
  tanulja meg, hogyan vonjon ki szöveget képből, és hogyan írjon JSON fájlt C#-ban
  az Aspose.OCR használatával.
draft: false
keywords:
- how to convert ocr
- extract text from image
- write json file c#
- write xml file c#
- how to extract text
language: hu
og_description: Hogyan konvertáljuk az OCR eredményeket strukturált JSON és XML fájlokká
  C#-ban. Lépésről‑lépésre útmutató a képről szöveg kinyeréséhez és JSON fájl írásához
  C#-ban.
og_title: Hogyan konvertáljuk az OCR-t JSON és XML formátumba C#‑ban – JSON fájl írása
tags:
- OCR
- C#
- Aspose
title: Hogyan konvertáljuk az OCR-t JSON-re és XML-re C#-ban – JSON fájl írása
url: /hu/net/text-recognition/how-to-convert-ocr-to-json-xml-in-c-write-json-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan konvertáljuk az OCR-t JSON-re és XML-re C#‑ban – JSON fájl írása

**How to convert OCR** eredmények átalakítása valamire, amit tényleg használhatsz, sok fejlesztő kérdése. Ebben az útmutatóban megmutatjuk, hogyan lehet szöveget kinyerni egy képből, az OCR kimenetet szépen formázott JSON‑ra és XML‑re alakítani, majd ezeket a fájlokat lemezre írni C#‑ban.

Ha valaha is egy nyers OCR karakterláncra bámultál és azt gondoltad, „Biztos van jobb módja ennek a tárolásnak,” akkor jó helyen vagy. A végére egy teljes, futtatható programod lesz, amely nem csak **extracts text from image** fájlokból, hanem tudja, hogyan **write JSON file C#** és **write XML file C#** anélkül, hogy izzadna.

## Amire szükséged lesz

- **.NET 6.0** vagy újabb (a kód .NET Framework 4.6+‑vel is működik).  
- **Aspose.OCR** NuGet csomag – telepítsd a `dotnet add package Aspose.OCR` paranccsal.  
- Egy szöveget tartalmazó kép (pl. `invoice.png`).  
- Bármelyik kedvenc IDE – Visual Studio, Rider vagy VS Code megfelel.

> **Pro tip:** Tartsd a képfájljaidat egy dedikált mappában (pl. `Resources/`), hogy az útvonalak rendezettek maradjanak.

## 1. lépés: Az OCR motor beállítása – How to Convert OCR

Először létrehozunk egy `OcrEngine` példányt, és megadjuk, melyik nyelvet keresse. A legtöbb esetben az angol elegendő, de a `Language.English`‑t bármely támogatott nyelvre cserélheted.

```csharp
using Aspose.OCR;
using System.IO;

class JsonXmlOcrDemo
{
    static void Main()
    {
        // Step 1: Initialise the OCR engine for English text
        var ocrEngine = new OcrEngine { Language = Language.English };
```

> **Why this matters:** A motor helyes nyelvvel történő inicializálása drámaian javítja a pontosságot, különösen a nem latin írásrendszerek esetén.

## 2. lépés: Szöveg felismerése – Extract Text from Image

Most betápláljuk a képet a motorba. A `Recognize` metódus egy `OcrResult` objektumot ad vissza, amely a nyers szöveget és a helyzetadatokat tartalmazza.

```csharp
        // Step 2: Recognise text from the supplied image
        // Replace "YOUR_DIRECTORY/invoice.png" with your actual file path
        var ocrResult = ocrEngine.Recognize("YOUR_DIRECTORY/invoice.png");
```

Ha a kép nem található, a `Recognize` `FileNotFoundException`‑t dob. A bemutató egyszerűségéért feltételezzük, hogy az útvonal helyes, de éles környezetben érdemes try‑catch blokkba helyezni.

## 3. lépés: Az eredmény konvertálása JSON-re – Write JSON File C#

Az Aspose.OCR könnyűvé teszi a sorosítást. A `ToJson` metódus egy `indent` kapcsolót fogad, amely szép, formázott kimenetet állít elő, ami tökéletes, ha szövegszerkesztőben szeretnéd megnyitni a fájlt.

```csharp
        // Step 3: Convert OCR result to formatted JSON
        string jsonOutput = ocrResult.ToJson(indent: true);
```

### Várható JSON minta

```json
{
  "Text": "Invoice #12345\nDate: 2024‑03‑31\nTotal: $250.00",
  "Regions": [
    {
      "Bounds": { "X": 10, "Y": 20, "Width": 200, "Height": 30 },
      "Text": "Invoice #12345"
    }
    // … more regions …
  ]
}
```

> **How to extract text**: A `Text` tulajdonság adja meg a sima karakterláncot, amelyet más szolgáltatásokba (keresőindexek, adatbázisok stb.) táplálhatsz.

## 4. lépés: A JSON mentése – Write JSON File C# (Folytatás)

A JSON karakterlánc elkészülte után egyszerűen a `File.WriteAllText`‑el írjuk fájlba. Ez alapértelmezés szerint UTF‑8 kódolást biztosít.

```csharp
        // Step 4: Save JSON to disk
        File.WriteAllText("YOUR_DIRECTORY/invoice.json", jsonOutput);
```

Most már van egy `invoice.json` a képed mellett, készen áll a további feldolgozásra.

## 5. lépés: Az eredmény konvertálása XML-re – Write XML File C#

Ha az örökölt rendszerekhez XML-t részesítesz előnyben, a `ToXml` metódus elvégzi a nehéz munkát. A `ToJson`‑hoz hasonlóan ez is támogatja a szép formázást.

```csharp
        // Step 5: Convert OCR result to formatted XML
        string xmlOutput = ocrResult.ToXml(indent: true);
```

### Várható XML minta

```xml
<OcrResult>
  <Text>Invoice #12345
Date: 2024-03-31
Total: $250.00</Text>
  <Regions>
    <Region>
      <Bounds X="10" Y="20" Width="200" Height="30" />
      <Text>Invoice #12345</Text>
    </Region>
    <!-- … more regions … -->
  </Regions>
</OcrResult>
```

## 6. lépés: Az XML mentése – Write XML File C# (Folytatás)

Az XML mentése megegyezik a JSON lépéssel; csak egy `.xml` kiterjesztést kell megadni.

```csharp
        // Step 6: Save XML to disk
        File.WriteAllText("YOUR_DIRECTORY/invoice.xml", xmlOutput);
    }
}
```

### Teljes működő példa

Összegezve, itt a teljes program, amelyet beilleszthetsz egy konzolos alkalmazásba:

```csharp
using Aspose.OCR;
using System.IO;

class JsonXmlOcrDemo
{
    static void Main()
    {
        // Initialise OCR engine for English
        var ocrEngine = new OcrEngine { Language = Language.English };

        // Recognise text from image
        var ocrResult = ocrEngine.Recognize("YOUR_DIRECTORY/invoice.png");

        // Convert to JSON and save
        string jsonOutput = ocrResult.ToJson(indent: true);
        File.WriteAllText("YOUR_DIRECTORY/invoice.json", jsonOutput);

        // Convert to XML and save
        string xmlOutput = ocrResult.ToXml(indent: true);
        File.WriteAllText("YOUR_DIRECTORY/invoice.xml", xmlOutput);
    }
}
```

Futtasd a programot, és két új fájlt találsz – `invoice.json` és `invoice.xml` – pontosan ott, ahol megadtad. Nyisd meg őket, hogy ellenőrizd, a struktúra megegyezik a fenti mintákkal.

## Gyakori kérdések és szélhelyzetek

| Question | Answer |
|----------|--------|
| **Mi van, ha a kép több nyelvet tartalmaz?** | Hozz létre külön `OcrEngine` példányokat minden nyelvhez, vagy használd a `Language.Multi`‑t, ha támogatott. |
| **Kezelhetem a kimeneti formátumot (pl. kizárhatom a régióadatokat)?** | Igen. A `ToJson` és a `ToXml` egyaránt elfogadnak opcionális paramétereket a mezők szűrésére; nézd meg az Aspose.OCR dokumentációját a `ExportOptions`‑ra vonatkozóan. |
| **Hogyan kezelem a sok oldalas nagy PDF-eket?** | Minden oldalt külön-külön dolgozz fel, aggregáld az eredményeket, majd egyszer sorosítsd. |
| **Biztonságos-e a kimenet UTF‑8-ban?** | Teljesen – az Aspose.OCR belsőleg Unicode‑ot használ, és a `File.WriteAllText` alapértelmezés szerint UTF‑8‑at ír. |
| **Mi a helyzet a teljesítménnyel?** | Az OCR CPU‑igényes. K batch feladatoknál fontold meg a párhuzamos feldolgozást több magon, vagy az Aspose felhő‑API‑jának használatát. |

## Összegzés

Most már tudod, hogyan **convert OCR** eredményeket JSON‑ra és XML‑re konvertálni C#‑ban. A fenti lépéseket követve **extract text from image** tudsz, majd **write JSON file C#** és **write XML file C#** csak néhány sorral. Ez a megközelítés gyors, megbízható, és bármilyen, az Aspose.OCR által támogatott képtípussal működik.

Készen állsz a következő kihívásra? Próbáld meg a következőt betáplálni a

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}