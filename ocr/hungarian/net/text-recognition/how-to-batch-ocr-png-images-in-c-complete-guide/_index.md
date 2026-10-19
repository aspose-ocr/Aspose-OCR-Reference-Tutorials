---
category: general
date: 2026-03-17
description: Hogyan végezzünk kötegelt OCR-t PNG képeken C#-ban gyorsan. Tanulja meg,
  hogyan nyerjen ki szöveget PNG fájlokból, konvertáljon PNG-t szöveggé, és olvassa
  be a képeket egy könyvtárból egy egyszerű szkripttel.
draft: false
keywords:
- how to batch OCR
- extract text png
- convert png to text
- read images from directory
language: hu
og_description: Hogyan végezzünk kötegelt OCR-t PNG képeken C#-ban lépésről‑lépésre
  kóddal. Szöveg kinyerése PNG fájlokból, PNG konvertálása szöveggé, és képek beolvasása
  könyvtárból könnyedén.
og_title: Hogyan végezzünk kötegelt OCR-t PNG képeken C#-ban – Teljes útmutató
tags:
- OCR
- C#
- Image Processing
title: Hogyan végezzünk kötegelt OCR-t PNG képeken C#-ban – Teljes útmutató
url: /hu/net/text-recognition/how-to-batch-ocr-png-images-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan végezzünk kötegelt OCR‑t PNG képeken C#‑ben – Teljes útmutató

Gondolkodtál már azon, **hogyan végezzünk kötegelt OCR‑t** egy mappában lévő képernyőképeken anélkül, hogy egyesével megnyitnád a fájlokat? Nem vagy egyedül – a fejlesztők folyamatosan kérdezik, hogyan lehet kötegelt OCR‑t alkalmazni nagy mennyiségű PNG‑re, különösen, ha a cél a szöveg kinyerése a PNG fájlokból a további elemzéshez.  

Ebben az útmutatóban végigvezetünk egy azonnal futtatható C# példán, amely **kivonja a szöveget a PNG** fájlokból, **PNG‑t szöveggé konvertál**, és megmutatja a legjobb módot a **képek beolvasására a könyvtárból**. A végére egyetlen szkriptet kapsz, amely minden kép mellé egy `.txt` fájlt helyez el, ezzel órákat takarítva meg a kézi másolás‑beillesztésből.

## Amit el fogsz érni

- Inicializálj egy OCR motorot egyszer, és használd újra az egész kötegben.  
- Olvasd be minden `*.png` fájlt egy adott mappában anélkül, hogy saját ciklust írnál.  
- Mentsd el minden OCR eredményt egy saját szövegfájlba, az eredeti fájlnév megtartásával.  
- Kezeld a gyakori szélhelyzeteket, mint például az üres mappák vagy a nem képfájlok, elegánsan.

### Előfeltételek

- .NET 6.0 vagy újabb (a kód .NET Core‑on és .NET Framework‑ön is működik).  
- Egy OCR könyvtár, amely elérhetővé teszi az `OcrEngine`, `ImageStream` és `OcrResult` típusokat (például a fiktív **FastOCR** SDK, amely a kódrészletekben szerepel).  
- Alapvető C# ismeretek – nincs szükség haladó mintákra.

---

## Hogyan végezzünk kötegelt OCR‑t PNG képeken – Áttekintés

Az alábbiakban a **teljes, futtatható program** látható. Nyugodtan másold be egy új konzolprojektbe, cseréld ki a helyőrző útvonalakat, és nyomd meg a **F5**‑öt.

```csharp
using System;
using System.IO;
using System.Linq;
using FastOCR;               // <-- Replace with your actual OCR namespace

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Initialize the OCR engine (language = English)
        // -------------------------------------------------
        var ocrEngine = new OcrEngine();
        ocrEngine.Config.Language = Language.English;

        // -------------------------------------------------
        // Step 2: Locate every PNG file in the input folder
        // -------------------------------------------------
        string inputFolder = @"YOUR_DIRECTORY\images";
        string[] imagePaths = Directory.GetFiles(inputFolder, "*.png");

        if (imagePaths.Length == 0)
        {
            Console.WriteLine("No PNG files found – nothing to process.");
            return;
        }

        // -------------------------------------------------
        // Step 3: Convert file paths to ImageStream objects
        // -------------------------------------------------
        var imageStreams = imagePaths
            .Select(path => ImageStream.FromFile(path))
            .ToList();

        // -------------------------------------------------
        // Step 4: Recognize text in the entire batch
        // -------------------------------------------------
        IReadOnlyList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);

        // -------------------------------------------------
        // Step 5: Write each result to a .txt file next to the image
        // -------------------------------------------------
        string outputFolder = @"YOUR_DIRECTORY\output";
        Directory.CreateDirectory(outputFolder); // ensures the folder exists

        for (int i = 0; i < ocrResults.Count; i++)
        {
            string originalFileName = Path.GetFileNameWithoutExtension(imagePaths[i]);
            string outputPath = Path.Combine(outputFolder, $"{originalFileName}.txt");
            File.WriteAllText(outputPath, ocrResults[i].Text);
            Console.WriteLine($"✅ {originalFileName}.txt created");
        }

        Console.WriteLine("All done! Check the output folder for your text files.");
    }
}
```

> **Várható kimenet:** Minden `image01.png` fájl mellé megtalálod a `image01.txt` fájlt, amely a felismert karaktereket tartalmazza. A konzol minden fájlt felsorol, ahogy az írásra kerül.

![How to batch OCR diagram](how-to-batch-ocr-diagram.png "Diagram illustrating how to batch OCR PNG images using C#")

---

## Lépésről‑lépésre magyarázat

### 1. Az OCR motor inicializálása – a folyamat szíve  

A `var ocrEngine = new OcrEngine();` sor egyetlen motorpéldányt hoz létre, amelyet az egész kötegben újra felhasználunk. A motor újrahasználata **kritikus**, mivel a legtöbb OCR könyvtár nehéz erőforrásokat (például nyelvi modelleket) foglal le a konstrukció során. Egyszeri inicializálás jelentősen javítja a teljesítményt – különösen, ha tucatnyi vagy akár több száz PNG‑vel dolgozol.  

> **Pro tipp:** Ha angol nyelven kívül más nyelvre van szükséged, állítsd be `ocrEngine.Config.Language = Language.Spanish;` (vagy bármely támogatott enum értéket).  

### 2. Képek beolvasása a könyvtárból – minden PNG megtalálása  

`Directory.GetFiles(@"YOUR_DIRECTORY\images", "*.png")` pontosan azt teszi, amit a *read images from directory* kulcsszó ígér. Egy abszolút útvonalakból álló tömböt ad vissza, amelyet később az OCR motorba adunk.  

> **Miért ne használjuk a `SearchOption.AllDirectories`‑t?** Ha a képeid alkönyvtárakban vannak, átállíthatod `GetFiles(path, "*.png", SearchOption.AllDirectories)`‑re. Csak ne feledd, hogy a mélyebb keresés nemkívánatos fájlokat is hozhat, ezért szűrd megfelelően.

### 3. Fájlútvonalak konvertálása ImageStream objektumokká  

A legtöbb OCR SDK egy stream‑et vár nyers útvonal helyett. A LINQ kifejezés `Select(path => ImageStream.FromFile(path)).ToList()` egy **stream listát** épít, amelyet a kötegelt felismerő egy hívással felhasználhat. Ez a lépés biztosítja, hogy a fájlkezelők csak egyszer legyenek megnyitva, csökkentve az I/O terhelést.  

> **Szélhelyzet:** Ha egy fájl sérült, a `ImageStream.FromFile` kivételt dobhat. Ha ellenállóbb megoldásra van szükséged, tedd a konverziót `try/catch`‑be.  

### 4. Szöveg felismerése az egész kötegben  

`ocrEngine.RecognizeBatch(imageStreams)` a tökéletes megoldás a *how to batch OCR* feladatra. Ahelyett, hogy minden képen ciklusban meghívnánk az egykép‑metódust, az egész gyűjteményt átadjuk a motor számára. A könyvtár belsőleg párhuzamosíthatja a munkát, így többmagos gépeken jelentős sebességnövekedést érhetsz el.  

> **Tipp:** Ha az OCR könyvtárad nem biztosít kötegelt metódust, hasonló teljesítményt érhetsz el a `Parallel.ForEach` használatával az egykép‑`Recognize` hívás körül.  

### 5. Minden OCR eredmény írása – PNG konvertálása szöveggé  

Az utolsó `for` ciklus a `ocrResults[i].Text`‑et egy `.txt` fájlba írja, amelynek neve megegyezik az eredeti PNG‑vel. Ez pontosan azt a *convert PNG to text* kulcsszót írja le. A `Path.Combine` hívás biztosítja, hogy a kimeneti mappa létezik, és megakadályozza az útvonal‑traverszálási hibákat.  

> **Gyakori hibaforrás:** Ha elfelejted előre létrehozni a kimeneti könyvtárat, `DirectoryNotFoundException` keletkezik. A `Directory.CreateDirectory(outputFolder);` sor előre megoldja ezt.  

---

## Valós világbeli variációk kezelése

| Situation | What to Change | Why |
|-----------|----------------|-----|
| **Üres bemeneti mappa** | Tartsd meg a korai `if (imagePaths.Length == 0)` ellenőrzést | Megakadályozza a felesleges OCR hívást és barátságos üzenetet ad |
| **Vegyes fájltípusok** | Használd a `Directory.EnumerateFiles(..., "*.*", SearchOption.TopDirectoryOnly).Where(f => f.EndsWith(".png", StringComparison.OrdinalIgnoreCase))` kifejezést | Biztosítja, hogy csak PNG‑ket dolgozz fel, ezzel megfelelve az *extract text png* kulcsszónak hibák nélkül |
| **Nagy képek ( > 5 MB )** | Méretezd le a képet az OCR előtt: `ImageStream.FromFile(path).Resize(1920, 1080)` (ha az API támogatja) | Csökkenti a memória terhelést és gyakran javítja a felismerés pontosságát |
| **Más OCR nyelv** | Állítsd be `ocrEngine.Config.Language = Language.French;` | Az OCR motor nyelvét a forrásképek nyelvéhez igazítja |

## Gyakran Ismételt Kérdések (GYIK)

**K: Működik ez JPEG vagy TIFF fájlokkal is?**  
V: A fő logika változatlan; csak módosítsd a keresési mintát `"*.jpg"` vagy `"*.tif"`‑re, és győződj meg róla, hogy az OCR könyvtár képes ezeket a formátumokat dekódolni.

**K: Hogyan dolgozhatok fel több ezer képet anélkül, hogy kifogyok a memóriából?**  
V: Cseréld le a kötegelt hívást egy streaming megközelítésre – dolgozz egyszerre egy, például 50 képből álló csomagot, majd a következő csomag betöltése előtt szabadítsd fel a stream‑eket.

**K: Szükségem van az OCR megbízhatósági pontszámra. Hol találom?**  
V: A legtöbb `OcrResult` objektum rendelkezik `Confidence` tulajdonsággal. Kiterjesztheted a kiírási lépést:

```csharp
var result = ocrResults[i];
string content = $"Confidence: {result.Confidence:P2}\n{result.Text}";
File.WriteAllText(outputPath, content);
```

---

## Összegzés

Most már áttekintettük, **hogyan végezzünk kötegelt OCR‑t** PNG képeken C#‑ben az elejétől a végéig. Egyetlen motor inicializálásával, a képek könyvtárból való beolvasásával, stream‑ekké konvertálásával, a teljes köteg felismerésével és végül minden eredmény szövegfájlba írásával most egy stabil, termelés‑kész mintát kaptál a **extract text PNG**, **convert PNG to text** és **read images from directory** feladatokhoz.  

Mi a következő? Próbáld ki egy másik OCR szolgáltatóra cserélni, adj hozzá több szálas utófeldolgozást (pl. helyesírás‑ellenőrzés), vagy tápláld a `.txt` fájlokat egy keresőindexbe. A lehetőségek végtelenek, miután elsajátítottad a kötegelt munkafolyamatot.  

Van egy saját trükköd, amit megosztanál? Írj egy megjegyzést, és jó kódolást!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}