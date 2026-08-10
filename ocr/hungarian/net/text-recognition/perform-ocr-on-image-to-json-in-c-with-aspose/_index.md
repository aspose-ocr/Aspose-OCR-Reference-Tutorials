---
category: general
date: 2026-04-08
description: Ismerje meg, hogyan végezhet OCR-t képen, és írhat JSON-fájlt C#-ban
  az Aspose OCR használatával. Ez az Aspose OCR C# oktatóanyag bemutatja az OCR képről
  JSON-re történő átalakítást a bizalmi értékekkel.
draft: false
keywords:
- perform OCR on image
- write JSON file C#
- OCR image to JSON
- Aspose OCR C# tutorial
language: hu
og_description: Képen OCR-t hajtson végre, és exportálja az eredményeket JSON fájlba
  C#-ban. Ez az útmutató a teljes Aspose OCR C# munkafolyamatot mutatja be, beleértve
  a bizonyossági pontszámokat.
og_title: OCR végrehajtása képről JSON-re C#‑ban – Aspose OCR útmutató
tags:
- Aspose
- OCR
- C#
- JSON
title: OCR végrehajtása képen JSON-re C#-ban az Aspose-szal
url: /hu/net/text-recognition/perform-ocr-on-image-to-json-in-c-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR végrehajtása képen JSON-re C#-ban az Aspose-szal

Valaha szükséged volt **OCR végrehajtására képen** fájlokon, de nem tudtad, hogyan juttasd az eredményeket strukturált formátumba? Nem vagy egyedül – a fejlesztők állandóan azt kérdezik: „Hogyan alakítsam át a beolvasott képet használható adatokra?” A jó hír, hogy az Aspose.OCR ezt gyerekjátékká teszi, és még **JSON fájlt is írhetsz C#‑stílusban** a bizalmi pontszámokkal együtt.

Ebben az útmutatóban végigvezetünk egy teljes **aspose OCR C# tutorial**-on, amely mindent lefed a kép betöltésétől a felismert szöveg JSON-ként való exportálásáig. A végére egy futtatható konzolalkalmazást kapsz, amely **OCR-t hajt végre képen**, az eredményt JSON-re (a bizalmi értékekkel együtt) konvertálja, és egyetlen kódsorral menti el. Nincsenek rejtett lépések, nincs külső script – csak tiszta C#.

## Előfeltételek

Before we dive in, make sure you have:

- .NET 6.0 SDK vagy újabb (a kód működik .NET Core és .NET Framework esetén is)
- Visual Studio 2022 (vagy bármely kedvelt szerkesztő)
- Érvényes **Aspose.OCR for .NET** licenc vagy ingyenes ideiglenes licenc (az ingyenes próba a teszteléshez megfelelő)
- Egy képfájl (`input.png`), amelyet feldolgozni szeretnél (bármely általános formátum – PNG, JPG, BMP – megfelel)

Ennyi. Ha valamelyik hiányzik, szerezd be most; a tutorial további része feltételezi, hogy már rendelkezésre állnak.

## 1. lépés: Az Aspose.OCR NuGet csomag telepítése

Először is—add hozzá a könyvtárat a projekthez. Nyiss egy terminált a projekt mappájában, és futtasd:

```bash
dotnet add package Aspose.OCR
```

## 2. lépés: Az OCR motor inicializálása (OCR végrehajtása képen)

Most létrehozunk egy `OcrEngine` példányt, és megadjuk, melyik nyelvet használja. Az angol (`"en"`) a leggyakoribb, de cserélheted `"fr"`, `"de"` vagy bármely támogatott nyelvre.

```csharp
using Aspose.Ocr;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // Path to your input image – change as needed
        string inputPath = Path.Combine(Environment.CurrentDirectory, "input.png");
        // Path where the JSON will be saved
        string outputPath = Path.Combine(Environment.CurrentDirectory, "output.json");

        // Step 2: Initialize the OCR engine – this is where we **perform OCR on image**
        var ocrEngine = new OcrEngine
        {
            Language = "en"               // Set language; you can use ISO‑639‑1 codes
        };

        // Optional: tweak recognition options (speed vs. accuracy)
        // ocrEngine.RecognitionMode = RecognitionMode.LargeText; // Uncomment for large blocks
```

**Miért inicializáljuk itt:** A `OcrEngine` tartalmazza a felismerési folyamat összes szükséges beállítását. A nyelv előzetes beállítása biztosítja, hogy a motor a megfelelő karakterkészletet használja, ami jelentősen javítja a pontosságot.

## 3. lépés: A kép felismerése és a bizalmi rögzítése

Miután a motor készen áll, betápláljuk a képfájlt. A `RecognizeImage` metódus egy `OcrResult` objektumot ad vissza, amely tartalmazza a kinyert szöveget és egy bizalmi pontszámot minden egyes szóhoz.

```csharp
        // Step 3: Perform OCR on the image file
        OcrResult ocrResult = ocrEngine.RecognizeImage(inputPath);

        // Verify that the result is not null
        if (ocrResult == null)
        {
            Console.WriteLine("OCR failed – check the file path and format.");
            return;
        }

        // For debugging: print the plain text to the console
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
```

**Mi történik a háttérben?** Az Aspose egy neurális hálózaton alapuló felismerőt futtat, amely minden pixelblokkot elemez, összeveti a nyelvi modelljével, és egy bizalmi értéket (0‑100) ad hozzá, amely megmutatja, mennyire biztos minden egyes szóban.

## 4. lépés: Az eredmény konvertálása JSON-re (OCR kép JSON-re)

Az Aspose könnyűvé teszi a konvertálást. Az `includeConfidence: true` átadással egy ilyen JSON terhet kapunk:

```json
{
  "Text": "Hello world",
  "Words": [
    { "Value": "Hello", "Confidence": 97.3 },
    { "Value": "world", "Confidence": 95.8 }
  ]
}
```

Itt a kód, amely előállítja a JSON karakterláncot:

```csharp
        // Step 4: Convert OCR result to JSON, including confidence values
        string jsonResult = ocrResult.ToJson(includeConfidence: true);
```

**Miért tartalmazza a bizalmat?** Ha az adatokat további folyamatokba (pl. validálás, UI kiemelés) szeretnéd továbbadni, a bizonytalan szavak ismerete segít eldönteni, kell-e a felhasználótól megerősítést kérni.

## 5. lépés: JSON fájl írása C#‑stílusban

Most ténylegesen **JSON fájlt írunk C#‑ban**. A `File.WriteAllText` metódus atomi, platformfüggetlen, így tökéletes konzolalkalmazásokhoz.

```csharp
        // Step 5: Save the JSON output to a file
        File.WriteAllText(outputPath, jsonResult);
        Console.WriteLine($"✅ JSON with confidence saved to: {outputPath}");
    }
}
```

Ez az egész munkafolyamat – öt tömör lépés, amely **OCR-t hajt végre képen**, az eredményt JSON-re alakítja, és elmenti.

## Teljes működő példa

Az alábbiakban a teljes program található, amelyet beilleszthetsz a `Program.cs`-be. Győződj meg róla, hogy az `input.png` ugyanabban a mappában van, mint a lefordított bináris, vagy állítsd be a megfelelő útvonalakat.

```csharp
using Aspose.Ocr;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // -------------------------------------------------------
        // 1️⃣ Set up file locations (feel free to change paths)
        // -------------------------------------------------------
        string inputPath = Path.Combine(Environment.CurrentDirectory, "input.png");
        string outputPath = Path.Combine(Environment.CurrentDirectory, "output.json");

        // -------------------------------------------------------
        // 2️⃣ Initialize the OCR engine – this is where we **perform OCR on image**
        // -------------------------------------------------------
        var ocrEngine = new OcrEngine
        {
            Language = "en" // English – replace with "fr", "es", etc. as needed
        };

        // -------------------------------------------------------
        // 3️⃣ Recognize the image and obtain confidence values
        // -------------------------------------------------------
        OcrResult ocrResult = ocrEngine.RecognizeImage(inputPath);

        if (ocrResult == null)
        {
            Console.WriteLine("❌ OCR failed – verify the image path and format.");
            return;
        }

        // Show plain text (optional)
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
        Console.WriteLine();

        // -------------------------------------------------------
        // 4️⃣ Convert the result to JSON – **OCR image to JSON**
        // -------------------------------------------------------
        string jsonResult = ocrResult.ToJson(includeConfidence: true);

        // -------------------------------------------------------
        // 5️⃣ Write the JSON file – **write JSON file C#** style
        // -------------------------------------------------------
        File.WriteAllText(outputPath, jsonResult);
        Console.WriteLine($"✅ JSON with confidence saved to: {outputPath}");
    }
}
```

### Várható kimenet

A program futtatásakor (`dotnet run`) valami ilyesmit látsz majd:

```
=== Extracted Text ===
Hello world

✅ JSON with confidence saved to: C:\YourProject\output.json
```

És az `output.json` a korábban bemutatott strukturált JSON-t fogja tartalmazni, minden szóhoz a bizalmi százalékokkal együtt.

## Pro tippek és speciális esetek

- **Missing file handling:** Csomagold a `RecognizeImage` hívást egy `try/catch` blokkba `FileNotFoundException`-ra, ha dinamikus útvonalakat vársz.
- **Different languages:** Állítsd be `ocrEngine.Language = "fr"` a francia nyelvhez, vagy tölts be egy egyedi nyelvi csomagot a `ocrEngine.LoadLanguage("custom.lang")` segítségével.
- **Large documents:** Többoldalas PDF-ek esetén először konvertáld minden oldalt képre (pl. a `Aspose.PDF` használatával), majd hajtsd végre az OCR lépéseket ciklusban.
- **Performance tuning:** Ha csak gyors eredményre van szükséged, válts `RecognitionMode.Fast`-ra – egy kicsit csökken a pontosság, de nő a sebesség.
- **JSON formatting:** Szép, formázott JSON-t szeretnél? Használd a `JsonConvert.SerializeObject`-t a Newtonsoft‑tól `Formatting.Indented` opcióval, miután deszerializáltad az Aspose JSON karakterláncot.

## Gyakran ismételt kérdések

**Q: Működik ez .NET Framework‑kel?**  
A: Teljesen. Ugyanaz a NuGet csomag .NET Standard 2.0-ra céloz, így .NET Framework 4.6.1 és újabb verziókból is hivatkozhatsz rá.

**Q: Mi van, ha a teljes dokumentumra, nem csak szavanként szeretném a bizalmat?**  
A: Az `OcrResult` tartalmazza az `OverallConfidence` értéket is. Ezt manuálisan hozzáadhatod a JSON-hoz:

```csharp
var customObj = new
{
    Text = ocrResult.Text,
    OverallConfidence = ocrResult.OverallConfidence,
    Words = ocrResult.Words
};
string json = JsonConvert.SerializeObject(customObj, Formatting.Indented);
```

**Q: Streamelhetem a JSON-t közvetlenül egy web API‑nak?**  
A: Igen. Cseréld le a `File.WriteAllText`-et egy `HttpClient` POST-ra, amely elküldi a `jsonResult

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}