---
category: general
date: 2026-02-13
description: Hogyan használjuk az OCR-t C#-ban a képből történő szövegkivonáshoz,
  a fényképen vagy JPG-n lévő szöveg felismeréséhez, és hogyan futtassunk OCR-t képen
  internetkapcsolat nélkül.
draft: false
keywords:
- how to use OCR
- extract text from image
- recognize text from photo
- recognize text from jpg
- run OCR on image
language: hu
og_description: Hogyan használjunk OCR-t C#-ban szöveg kinyerésére képről, szöveg
  felismerésére fényképről, és OCR futtatására képen egy teljes, futtatható példával.
og_title: Hogyan használjuk az OCR-t C#-ban – Szöveg kinyerése képből
tags:
- OCR
- C#
- Image Processing
title: Hogyan használjuk az OCR-t C#-ban – Szöveg kinyerése képből és szöveg felismerése
  fényképről
url: /hu/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-image-and-recognize-te/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan használjunk OCR-t C#‑ban – Szöveg kinyerése képből és szöveg felismerése fényképről

Gondolkodtál már azon, **hogyan használjunk OCR-t**, hogy szavakat nyerjünk ki egy képernyőképből, egy beolvasott nyugtából vagy egy véletlenszerű fényképből, amit a telefonoddal készítettél? Nem vagy egyedül. Sok valós alkalmazásban képeket kell kereshető szöveggé alakítanunk, és ha ezt helyben, internetkapcsolat nélkül csináljuk, az igazi fejtörő lehet.

Ezért ez az útmutató lépésről‑lépésre mutatja be, hogyan **nyerjünk ki szöveget képből** C# OCR motor segítségével, valamint azt is, hogyan **ismerjünk fel szöveget fényképről**, **ismerjünk fel szöveget JPG‑ról**, és hogyan **futtassunk OCR‑t képen** közvetlenül a lemezen. A végére egy teljes, másolás‑beillesztésre kész programot kapsz, ami azonnal működik.

## Amit megtanulsz

- Hogyan konfigurálj egy OCR motort egyszerű kínai (vagy bármely általad beállított nyelv) számára.  
- A pontos kód, amely **betölti az erőforrásokat** egy helyi mappából – hálózati hívás nélkül.  
- Hogyan **ismerjünk fel szöveget fényképről** olyan fájlokban, mint a JPEG, PNG vagy BMP.  
- Tippek a gyakori széljegyek kezelésére, például hiányzó modellfájlok vagy nem támogatott képformátumok esetén.  
- Egy teljes, futtatható példa, amelyet beilleszthetsz a Visual Studio‑ba, és azonnal láthatod az eredményt.

### Előfeltételek

- .NET 6.0 vagy újabb (az itt használt API a .NET Standard 2.0‑ra céloz, így a régebbi verziók is működnek).  
- Alapvető ismeretek C#‑ból és Visual Studio‑ból (vagy bármely kedvenc IDE‑ből).  
- Az általad használt OCR könyvtár (a kódrészlet egy fiktív `OcrEngine` osztályt feltételez, amely nyelvi modellekkel érkezik).  
- Egy mappa, amely a szükséges nyelvi modellfájlokat tartalmazza – tekintsd ezt a motor „agyának”, amely a kínai karakterek olvasásához szükséges.

> **Pro tipp:** Ha még nincs meg a kínai modellfájl, töltsd le egyszer a szállító weboldaláról, és helyezd el egy `C:\OcrResources`‑hez hasonló mappában. A motor ezután soha többé nem fog online menni.

---

![Diagram showing OCR process on a photo](path/to/ocr-diagram.png "Diagram showing OCR process on a photo")

## Hogyan használjunk OCR‑t: Motor beállítása

Az első dolog, amire szükséged van, egy OCR motor példány, a kívánt nyelvre konfigurálva. Ebben a bemutatóban **egyszerű kínai** nyelvet célozunk, de a `OcrLanguage.ChineseSimplified` helyettesítése `OcrLanguage.English`‑re (vagy bármely más enum értékre) csak egy soros módosítás.

```csharp
using System;
using YourOcrLibrary;   // Replace with the actual namespace of your OCR SDK

// Step 1: Create and configure the OCR engine for Simplified Chinese
var ocrEngine = new OcrEngine
{
    // Primary keyword appears here naturally
    Language = OcrLanguage.ChineseSimplified,

    // Point to a folder that already contains the Chinese model files
    ResourceFolder = @"C:\OcrResources"
};
```

**Miért fontos ez:**  
A `Language` tulajdonság beállítása megmondja a motornak, milyen karakterkészletet várjon. A `ResourceFolder` az a hely, ahol a motor a neurális‑hálózati súlyokat és nyelvi szótárakat keresi – tekintsd ezt az agy memóriabankjának. Ha rossz mappára mutatsz, a motor `FileNotFoundException`‑t dob, és elakadsz.

## Szöveg kinyerése képből – Erőforrások betöltése

Mielőtt a motor ténylegesen olvasna bármit, be kell töltened a modellfájlokat a memóriába. Ez a lépés **kritikus**, mert elkerüli a hálózati hívást minden egyes kép feldolgozásakor.

```csharp
// Step 2: Load the language resources from the specified folder (no internet required)
try
{
    ocrEngine.LoadResources();
    Console.WriteLine("Resources loaded successfully.");
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Failed to load OCR resources: {ex.Message}");
    // In a real app you might fallback to a default language or abort gracefully
}
```

**Mi mehet félre?**  
Ha a mappa útvonala hibás vagy a fájlok sérültek, a `LoadResources()` kivételt dob. A fenti `try/catch` blokk a hibamentes kezelést mutatja be – ami a gyakorlatban gyakran szükséges.

## Szöveg felismerése fényképről – OCR futtatása

Most jön a szórakoztató rész: egy képfájlt átadni a motornak, és visszakapni a felismert szöveget. Ez a **run OCR on image** forgatókönyvek középpontja, legyen szó JPEG‑ről, PNG‑ről vagy akár BMP‑ről.

```csharp
// Step 3: Recognize text from an image file
string imagePath = @"C:\OcrResources\photo.jpg";

try
{
    var recognitionResult = ocrEngine.RecognizeImage(imagePath);
    Console.WriteLine("=== OCR Output ===");
    Console.WriteLine(recognitionResult.Text);
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Error during OCR processing: {ex.Message}");
}
```

A `RecognizeImage` metódus egy `RecognitionResult`‑ot (vagy amit a SDK‑d hív) ad vissza, amely általában a következőket tartalmazza:

- `Text` – a sima szöveges átirat.  
- `Confidence` – numerikus pontszám, amely azt jelzi, mennyire biztos a motor az egyes sorokban.  
- `BoundingBoxes` – opcionális koordináták, amelyek megmutatják, hol helyezkedik el az egyes szavak a képen.

**Miért lehet fontos a biztonsági fokozat:**  
Ha adatbevitel‑automatizálási eszközt építesz, beállíthatsz egy küszöbértéket (pl. 0,85), és a felhasználót megkérheted, hogy erősítse meg az alacsony biztonságú sorokat. Ez drámaian javítja a teljes pontosságot.

## Szöveg felismerése JPG‑ról – Különböző formátumok kezelése

Sok fejlesztő azt hiszi, az OCR csak PNG‑kkel működik, de a modern motorok **JPG** fájlokat is könnyedén kezelnek. Az egyetlen buktató, hogy a JPEG tömörítés olyan artefaktusokat hozhat létre, amelyek összezavarhatják a modellt.

```csharp
// Bonus: Recognize text from a JPG with optional preprocessing
string jpgPath = @"C:\OcrResources\scanned_doc.jpg";

// Optional: use a simple image‑preprocess step to improve accuracy
var preprocessed = ImageHelper.DenoiseAndDeskew(jpgPath); // pseudo‑method
var result = ocrEngine.RecognizeImage(preprocessed);
Console.WriteLine($"Detected text ({result.Confidence:P0} confidence):");
Console.WriteLine(result.Text);
```

Ha nincs `DenoiseAndDeskew` segédfüggvényed, számos könyvtár (pl. OpenCvSharp) biztosítja ezeket a funkciókat. A fő tanulság: **run OCR on image** fájlok esetén érdemes egy kis tisztítást végezni, ha a kép szkennerből vagy telefonkamerából származik.

## Run OCR on Image – Tippek, széljegyek és legjobb gyakorlatok

### 1. Memóriakezelés
Nagy nyelvi modellek betöltése több száz megabájtot is fogyaszthat. A motor használata után szabadítsd fel az erőforrásokat:

```csharp
ocrEngine.Dispose(); // or using statement if the SDK implements IDisposable
```

### 2. Kötetes feldolgozás
Ha tucatnyi fényképet kell feldolgoznod, töltsd be az erőforrásokat egyszer, majd ismételd a ciklust:

```csharp
string[] files = Directory.GetFiles(@"C:\BatchPhotos", "*.jpg");
foreach (var file in files)
{
    var res = ocrEngine.RecognizeImage(file);
    File.WriteAllText(Path.ChangeExtension(file, ".txt"), res.Text);
}
```

### 3. Többnyelvű forgatókönyvek
Nyelveket váltogathatsz “útközben”, ha újra beállítod az `ocrEngine.Language`‑t és újra meghívod a `LoadResources()`‑t. Csak vedd figyelembe a töltési időt.

### 4. Üres eredmények kezelése
Néha a motor üres stringet ad vissza. Ez általában azt jelenti, hogy a kép túl homályos, vagy a szöveg színe beleolvad a háttérbe. Egy gyors ellenőrzés:

```csharp
if (string.IsNullOrWhiteSpace(recognitionResult.Text))
{
    Console.WriteLine("No text detected – consider increasing image contrast.");
}
```

### 5. Biztonsági megfontolások
Soha ne adj felhasználó által feltöltött fájlokat közvetlenül az OCR motorba validáció nélkül. Legalább ellenőrizd a fájlkiterjesztést és a méretet, és fontold meg a malware‑szkennelést.

---

## Teljesen működő példa

Az alábbi egy önálló program, amelyet beilleszthetsz egy új Console App projektbe. Bemutatja, hogyan **használjunk OCR‑t**, **nyerjünk ki szöveget képből**, **ismerjünk fel szöveget fényképről**, **ismerjünk fel szöveget JPG‑ról**, és **futtassunk OCR‑t képen** – mindezt egy lépésben.

```csharp
// File: Program.cs
using System;
using System.IO;
using YourOcrLibrary; // Replace with actual namespace

namespace OcrDemo
{
    class Program
    {
        static void Main()
        {
            // ------------------------------
            // 1️⃣ Configure the OCR engine
            // ------------------------------
            var ocrEngine = new OcrEngine
            {
                Language = OcrLanguage.ChineseSimplified,
                ResourceFolder = @"C:\OcrResources"
            };

            // Load language resources (no internet needed)
            try
            {
                ocrEngine.LoadResources();
                Console.WriteLine("Resources loaded.");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"Failed to load resources: {ex.Message}");
                return;
            }

            // -------------------------------------------------
            // 2️⃣ Recognize text from a photo (JPG in this case)
            // -------------------------------------------------
            string imagePath = @"C:\OcrResources\photo.jpg";

            if (!File.Exists(imagePath))
            {
                Console.Error.WriteLine($"Image not found: {imagePath}");
                return;
            }

            try
            {
                var result = ocrEngine.RecognizeImage(imagePath);
                Console.WriteLine("\n=== OCR Output ===");
                Console.WriteLine(result.Text);
                Console.WriteLine($"\nConfidence: {result.Confidence:P2}");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"OCR error: {ex.Message}");
            }

            // Clean up
            ocrEngine.Dispose();
        }
    }
}
```

**Várható kimenet (példa):**

```
Resources loaded.

=== OCR Output ===
中华人民共和国
北京
2026年02月13日

Confidence: 92.45%
```

A tényleges szöveg a kép tartalmától függ, de a konzolon egy Unicode karakterekből álló blokkot kell látnod, amelyhez egy biztonsági százalék is tartozik.

---

## Következtetés

Végigvezettünk a **hogyan használjunk OCR‑t** C#‑ban a kezdetektől a befejezésig – a motor konfigurálását, a nyelvi erőforrások betöltését, és végül a **szöveg felismerését fényképről** vagy **JPG‑ról** anélkül, hogy valaha is az internetet érintettük volna. A fenti lépéseket követve **szöveget nyerhetsz ki képfájlokból**, **futtathatsz OCR‑t képi eszközökön**, és kezelheted a leggyakoribb buktatókat, amelyek a kezdőket gyakran meglepik.

Készen állsz a következő kihívásra? Próbáld meg a motort egy PDF‑oldalra konvertált képpel táplálni, vagy kísérletezz egy másik nyelvi csomaggal, hogy lásd, hogyan változnak a biztonsági pontszámok. You might

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}