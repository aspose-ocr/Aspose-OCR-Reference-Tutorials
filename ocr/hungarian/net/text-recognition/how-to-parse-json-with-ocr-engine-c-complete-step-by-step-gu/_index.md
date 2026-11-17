---
category: general
date: 2026-03-17
description: Tudja meg, hogyan kell JSON-t feldolgozni OCR-eredményekből C#-ban. Ez
  az útmutató bemutatja, hogyan lehet szöveget kinyerni, képet betölteni OCR-hez,
  OCR-felismerést futtatni, és hatékonyan használni az OCR-motort C#-ban.
draft: false
keywords:
- how to parse json
- how to extract text
- load image for OCR
- run OCR recognition
- use OCR engine C#
language: hu
og_description: Hogyan dolgozzuk fel a JSON-t az OCR kimenetből C#-ban. Kövesd útmutatónkat
  a szöveg kinyeréséhez, a kép betöltéséhez OCR-hez, az OCR felismerés futtatásához,
  és az OCR motor C#-ban való használatához.
og_title: Hogyan dolgozzuk fel a JSON-t OCR motorral C#-ban – Teljes útmutató
tags:
- C#
- OCR
- JSON
- Image Processing
title: Hogyan parse-oljuk a JSON-t OCR motorral C#-ban – Teljes lépésről lépésre útmutató
url: /hu/net/text-recognition/how-to-parse-json-with-ocr-engine-c-complete-step-by-step-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan parse-oljuk a JSON-t OCR motorral C#‑ban – Teljes lépésről‑lépésre útmutató

Gondolkodtál már azon, **hogyan parse-oljuk a json‑t**, ami közvetlenül egy OCR motorból érkezik? Nem vagy egyedül. A legtöbb fejlesztő ugyanabba a csapdába ütközik – nyers JSON-t kap, majd ki kell találnia, hogyan nyerje ki a hasznos adatokat, mint a megbízhatósági pontszámok vagy a tényleges szöveg. Ebben az útmutatóban végigvezetünk egy kép betöltésén OCR‑hez, az OCR felismerés futtatásán, és végül **hogyan parse-oljuk a json‑t** tiszta, karbantartható módon.

A tutorial végére képes leszel:

* Egy képet betölteni OCR‑hez néhány sor kóddal.  
* OCR felismerést futtatni egy C# OCR motorral.  
* **Hogyan nyerjük ki a szöveget** és egyéb metaadatokat a JSON payload‑ból.  
* Közös edge case‑eket kezelni (hiányzó mezők, váratlan formátumok) anélkül, hogy összeomlana a program.

Külső dokumentációra nincs szükség – minden, amire szükséged van, itt van.

## Előfeltételek

Mielőtt belevágnánk, győződj meg róla, hogy rendelkezel:

* .NET 6.0 vagy újabb (a kód .NET Framework 4.7+‑on is lefordítható).  
* Hivatkozással az általad használt OCR könyvtárra (a példa egy hipotetikus `OcrEngine` osztályt használ).  
* A `Newtonsoft.Json` NuGet csomagra a JSON kezeléshez (`Install-Package Newtonsoft.Json`).  
* Egy kép fájlra (pl. `passport.png`), amelyet az alkalmazásod el tud olvasni.

> **Pro tipp:** Ha kereskedelmi OCR SDK‑t használsz, ellenőrizd, hogy a JSON kimeneti formátum engedélyezve van‑e; a legtöbb szállító ezt egy konfigurációs tulajdonságon keresztül teszi elérhetővé, például `ocrEngine.Config.OutputFormat`.

## 1. lépés – OCR motor létrehozása és konfigurálása (Primary Keyword in Action)

Az első dolog, amit tenned kell, hogy példányosítod az OCR motort, és beállítod, hogy JSON‑t adjon vissza. Itt jelenik meg először a **how to parse json** kifejezés a kódban, mert a motor egy JSON stringet ad majd, amelyet később parse‑olunk.

```csharp
using System;
using Newtonsoft.Json.Linq;   // For JSON parsing
// Assume OcrEngine, OutputFormat, and ImageStream live in the OCR SDK namespace
using OcrSdk;                  // <-- replace with the real namespace

// Step 1: Create an OCR engine instance and set JSON output
var ocrEngine = new OcrEngine();
ocrEngine.Config.OutputFormat = OutputFormat.Json;
```

**Miért fontos:** Az `OutputFormat` `Json`‑ra állítása biztosítja, hogy a válasz tartalmazza a felismert szöveget **és** a hasznos metaadatokat, például a megbízhatósági pontszámokat. Ha ezt a lépést kihagyod, csak egyszerű szöveget kapsz, és a **how to parse json** kérdés értelmetlen lesz.

## 2. lépés – Kép betöltése OCR‑hez

Most betöltjük azt a képet, amelyet elemezni szeretnénk. Itt jön a másodlagos kulcsszó **load image for OCR** a fókuszba.

```csharp
// Step 2: Load the image you want to recognize
// Make sure the path points to a real file; otherwise an exception is thrown.
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY\passport.png");
```

> **Mi van, ha a fájl nem létezik?** Tedd a hívást egy `try/catch` blokkba, és jeleníts meg egy barátságos üzenetet – így az alkalmazás nem omlik össze, és a felhasználók tudni fogják, mi a hiba.

## 3. lépés – OCR felismerés futtatása

Miután a motor készen áll és a kép betöltődött, a következő logikus lépés a felismerés tényleges futtatása. Ez teljesíti a másodlagos kulcsszót **run OCR recognition**.

```csharp
// Step 3: Execute OCR and get the raw result object
var ocrResult = ocrEngine.Recognize();
```

Az `ocrResult.Text` tulajdonság most egy JSON stringet tartalmaz. Ha a konzolra írod, valami ilyesmit látsz:

```json
{
  "OverallConfidence": 0.92,
  "Pages": [
    {
      "Text": "John Doe\nPassport No: 123456789",
      "Confidence": 0.95
    }
  ]
}
```

## 4. lépés – Hogyan nyerjük ki a szöveget (és egyéb mezőket) a JSON‑ból

Itt jön a tutorial szíve: **how to parse json** és **how to extract text** az OCR payload‑ból. A `Newtonsoft.Json.Linq.JObject`‑et fogjuk használni a rugalmasság miatt.

```csharp
// Step 4: Output the raw JSON (optional, helps debugging)
Console.WriteLine("Raw OCR JSON:");
Console.WriteLine(ocrResult.Text);
Console.WriteLine();

// Step 5: Parse the JSON into a JObject
JObject jsonObject = JObject.Parse(ocrResult.Text);

// Extract the overall confidence score
var overallConfidence = jsonObject["OverallConfidence"]?.Value<double>() ?? 0.0;
Console.WriteLine($"Overall confidence: {overallConfidence:P0}");

// Extract the text from the first page (how to extract text)
string pageText = jsonObject["Pages"]?[0]?["Text"]?.Value<string>() ?? string.Empty;
Console.WriteLine("Extracted text:");
Console.WriteLine(pageText);
```

**Miért használjuk a `JObject`‑et?** Lehetővé teszi, hogy biztonságosan navigálj a JSON fában anélkül, hogy teljes C# modell osztályt definiálnál. A null‑conditional (`?.`) operátorok megvédnek a `NullReferenceException`‑től, ha az OCR motor valaha kihagy egy mezőt.

### Edge case‑ek kezelése

* **Hiányzó mezők:** A `?.Value<T>() ?? default` minta értelmes visszaesést ad.  
* **Több oldal:** Iterálj a `jsonObject["Pages"]` elemein, ha több oldalt vársz.  
* **Nem numerikus megbízhatóság:** Használd a `double.TryParse`‑t, ha az SDK időnként stringet ad vissza.

## 5. lépés – Minden összefoglalása egy újrahasználható metódusban

Az ismétlődő boilerplate elkerülése érdekében csomagold az egész folyamatot egy segédmetódusba. Ez egyben bemutatja a **use OCR engine C#** használatát tiszta, újrahasználható módon.

```csharp
public static void RunOcrAndParseJson(string imagePath)
{
    // 1️⃣ Create engine & set JSON output
    var engine = new OcrEngine();
    engine.Config.OutputFormat = OutputFormat.Json;

    // 2️⃣ Load image (load image for OCR)
    engine.Image = ImageStream.FromFile(imagePath);

    // 3️⃣ Run OCR (run OCR recognition)
    var result = engine.Recognize();

    // 4️⃣ Show raw JSON (optional)
    Console.WriteLine("=== Raw JSON ===");
    Console.WriteLine(result.Text);
    Console.WriteLine();

    // 5️⃣ Parse JSON (how to parse json)
    JObject obj = JObject.Parse(result.Text);

    // 6️⃣ Extract useful data (how to extract text)
    double confidence = obj["OverallConfidence"]?.Value<double>() ?? 0.0;
    string text = obj["Pages"]?[0]?["Text"]?.Value<string>() ?? string.Empty;

    Console.WriteLine($"Overall confidence: {confidence:P0}");
    Console.WriteLine("Extracted text:");
    Console.WriteLine(text);
}
```

Most már meghívhatod a `RunOcrAndParseJson(@"C:\Images\passport.png");`‑t a `Main`‑ből vagy az alkalmazás bármely más részéből.

## Teljes működő példa

Az alábbi egy komplett, önálló konzolprogram, amelyet beilleszthetsz egy új `.csproj`‑ba. Tartalmazza az összes korábban tárgyalt elemet, valamint egy kis hibakezelést.

```csharp
// File: Program.cs
using System;
using Newtonsoft.Json.Linq;
using OcrSdk;               // Replace with the actual namespace of your OCR library

class Program
{
    static void Main()
    {
        try
        {
            // Adjust the path to point at a real image on your machine
            string imagePath = @"YOUR_DIRECTORY\passport.png";

            RunOcrAndParseJson(imagePath);
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Unexpected error: {ex.Message}");
        }
    }

    /// <summary>
    /// Demonstrates how to parse JSON returned by an OCR engine,
    /// and how to extract text, confidence, and other metadata.
    /// </summary>
    /// <param name="imagePath">Full path to the image file.</param>
    public static void RunOcrAndParseJson(string imagePath)
    {
        // 1️⃣ Initialize OCR engine (use OCR engine C#)
        var engine = new OcrEngine();
        engine.Config.OutputFormat = OutputFormat.Json;

        // 2️⃣ Load image for OCR
        engine.Image = ImageStream.FromFile(imagePath);

        // 3️⃣ Run OCR recognition
        var result = engine.Recognize();

        // 4️⃣ Print raw JSON (helps debugging)
        Console.WriteLine("=== Raw OCR JSON ===");
        Console.WriteLine(result.Text);
        Console.WriteLine();

        // 5️⃣ Parse JSON (how to parse json)
        JObject json = JObject.Parse(result.Text);

        // 6️⃣ Extract overall confidence
        double overallConf = json["OverallConfidence"]?.Value<double>() ?? 0.0;
        Console.WriteLine($"Overall confidence: {overallConf:P0}");

        // 7️⃣ Extract text from first page (how to extract text)
        string firstPageText = json["Pages"]?[0]?["Text"]?.Value<string>() ?? string.Empty;
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(firstPageText);
    }
}
```

**Várható kimenet** (ha az OCR sikeres):

```
=== Raw OCR JSON ===
{
  "OverallConfidence": 0.92,
  "Pages": [
    {
      "Text": "John Doe\nPassport No: 123456789",
      "Confidence": 0.95
    }
  ]
}

Overall confidence: 92%
=== Extracted Text ===
John Doe
Passport No: 123456789
```

Ha a képet nem lehet beolvasni, az SDK kivételt dob, amelyet a `Main`‑ben elkapunk, és egy barátságos hibaüzenetet írunk ahelyett, hogy összeomlana a program.

## Gyakran Ismételt Kérdések (GYIK)

**Q: Mi van, ha az OCR motor oldalak tömbjét adja vissza?**  
A: Iterálj a `json["Pages"]` elemein, és fűzd össze minden `["Text"]` értékét, vagy dolgozd fel őket egyenként a felhasználási esetedtől függően.

**Q: Deszerializálhatom a JSON‑t egy típusos C# osztályba?**  
A: Természetesen. Definiálj egy osztálystruktúrát, amely megfelel a JSON sémának, és használd a `JsonConvert.DeserializeObject<YourRootClass>(result.Text)`‑t. Ez fordítási időben biztosítja a típusosságot, de megköveteli, hogy a modell szinkronban legyen az SDK kimenetével.

**Q: Működik ez aszinkron OCR API‑kkal?**  
A: Igen. Cseréld le az `engine.Recognize()`‑t `await engine.RecognizeAsync()`‑ra, és tedd a `RunOcrAndParseJson` metódust `async Task`‑é. A JSON parse‑olási rész változatlan marad.

**Q: Hogyan mentsem a JSON‑t egy fájlba későbbi elemzéshez?**  
A: Miután a `result.Text` lekérted, hívd meg a `File.WriteAllText(@"output.json", result.Text);`‑t. Később újra beolvashatod a `JObject.Parse(File.ReadAllText(...))`‑val.

## Következő lépések

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}