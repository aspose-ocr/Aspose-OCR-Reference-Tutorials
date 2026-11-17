---
category: general
date: 2026-03-21
description: Tanulja meg, hogyan lehet kiegyenesíteni a képfájlokat és felismerni
  a szöveges képet az Aspose OCR-rel. Konvertálja a jpg fájlokat szöveggé, és javítsa
  a kép forgását néhány C# kódsorral.
draft: false
keywords:
- how to deskew image
- recognize text image
- convert jpg to text
- correct image rotation
- recognize text jpg
language: hu
og_description: Hogyan korrigáljuk a kép dőlését és nyerjünk ki szöveget JPEG-ekből
  az Aspose OCR-rel. Kövesse ezt a lépésről‑lépésre útmutatót a jpg szöveggé konvertáláshoz
  és a kép forgatásának javításához.
og_title: Hogyan kiegyenesítsünk képet C#-ban – Gyors Aspose OCR útmutató
tags:
- OCR
- C#
- Aspose
title: Hogyan kiegyenesítsünk képet C#-ban – Teljes útmutató az Aspose OCR használatával
url: /hu/net/skew-angle-calculation/how-to-deskew-image-in-c-complete-guide-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan korrigáljunk ferde képet C#‑ban – Teljes útmutató az Aspose OCR használatával

Gondolkodtál már azon, **hogyan korrigáljunk ferde képet** olyan fájloknál, amelyek egy szkennertől származnak és furcsa szögben vannak elfordítva? Nem vagy egyedül – sok fejlesztő szembesül ezzel a problémával, amikor számlákról, bizonylatokról vagy kézzel írt jegyzetekről próbál szöveget kinyerni. A jó hír, hogy az Aspose OCR segítségével korrigálhatod a kép forgását, és tiszta, kereshető szöveget nyerhetsz ki néhány sor kóddal.

Ebben az útmutatóban végigvezetünk a teljes folyamaton: a könyvtár telepítésétől, az automatikus ferde kép korrigálás engedélyezéséig, a szövegkép felismeréséig, és végül egy JPG‑t szöveggé konvertálásáig. A végére egy kész, futtatható konzolos alkalmazást kapsz, amely **recognize text jpg** fájlokat képes feldolgozni anélkül, hogy előzetesen manuálisan forgatnád őket.

## Amire szükséged lesz

- **.NET 6.0** vagy újabb (a kód .NET Core‑on és .NET Framework‑ön egyaránt működik)  
- **Aspose.OCR for .NET** NuGet csomag – ajánlott a 23.12 vagy újabb verzió  
- Egy példa **ferde JPEG** (pl. `skewed_receipt.jpg`), amelyet az alkalmazásod el tud olvasni  
- Visual Studio, VS Code vagy bármely kedvenc C# szerkesztő  

Nem szükséges más harmadik féltől származó eszköz. A könyvtár belül kezeli a ferde kép korrigálást, az OCR‑t és még a nyelvfelismerést is.

![hogyan korrigáljunk ferde képet példa](/images/deskew-example.png "hogyan korrigáljunk ferde képet az Aspose OCR segítségével")

## 1. lépés: Projekt beállítása és az Aspose.OCR telepítése

A rendezettség kedvéért indíts egy új konzolos projektet:

```bash
dotnet new console -n DeskewDemo
cd DeskewDemo
dotnet add package Aspose.OCR --version 23.12.0
```

A `dotnet add package` sor letölti az **Aspose.OCR** binárisokat és az összes natív függőséget. Windows alatt a natív DLL‑eket automatikusan megkapod; Linux/macOS esetén szükség lehet a `libgdiplus` csomagra, de ez egyszeri telepítés.

## 2. lépés: Automatikus ferde kép korrigálás engedélyezése (Kép forgásának javítása)

Nyisd meg a `Program.cs` fájlt, és cseréld le a tartalmát az alábbi kóddal. A kulcsfontosságú sor itt a `ocrEngine.Settings.Deskew = true;` – ez a jelző, amely megmondja a motornak, **hogyan korrigáljunk ferde képet** automatikusan.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

namespace DeskewDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // 1️⃣ Create an OCR engine (CPU mode is fine for most desktop apps)
            // -----------------------------------------------------------------
            var ocrEngine = new OcrEngine();

            // ---------------------------------------------------------------
            // 2️⃣ Turn on deskewing – this corrects image rotation for us
            // ---------------------------------------------------------------
            ocrEngine.Settings.Deskew = true;   // <-- how to deskew image is handled here

            // ---------------------------------------------------------------
            // 3️⃣ Point the engine at the JPEG you want to process
            // ---------------------------------------------------------------
            string imagePath = "YOUR_DIRECTORY/skewed_receipt.jpg";

            // ---------------------------------------------------------------
            // 4️⃣ Run OCR – the result already contains the corrected text
            // ---------------------------------------------------------------
            OcrResult ocrResult = ocrEngine.Recognize(imagePath);

            // ---------------------------------------------------------------
            // 5️⃣ Output the text – this is your “convert jpg to text” step
            // ---------------------------------------------------------------
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

### Miért engedélyezzük a ferde kép korrigálást?

Ha egy szkenner oldalát szöge miatt ferde módon adja át, a szöveg alapvonala is el van döntve. A hagyományos OCR motorok minden karaktert ferde változatként olvasnának, ami drámaian csökkenti a pontosságot. A `Deskew = true` beállítással az Aspose OCR egy gyors Hough‑transzformációt hajt végre a háttérben, a bitmapet visszaforgatja vízszintes állásba, majd elvégzi a felismerést. Az eredmény olyan, mintha a képet manuálisan forgattad volna Photoshopban – csak gyorsabb és teljesen automatizált.

## 3. lépés: Szövegkép felismerése és JPG konvertálása szöveggé

A `Recognize` hívás egyszerre két dolgot végez:

1. **Korrigálja** a képet (mivel bekapcsoltuk a jelzőt).  
2. **Kinyeri** a szöveges tartalmat, és egy `OcrResult` objektumban adja vissza.

A `ocrResult.Text` értéket egyszerű karakterláncként kezelheted, fájlba írhatod, vagy továbbíthatod a későbbi feldolgozási csővezetékekbe. Ha a szavak nyers bizalmi pontszámaira van szükséged, a `ocrResult.Words` egy gyűjteményt ad `Confidence` értékekkel.

### Példa kimenet

Feltételezve, hogy a `skewed_receipt.jpg` egy egyszerű bizonylatot tartalmaz, a következőhöz hasonló kimenetet láthatsz:

```
=== Recognized Text ===
Store: Coffee Corner
Date: 2026-03-20
Item   Qty   Price
Latte   2    5.00
Bagel   1    2.50
Total          12.50
```

Vedd észre, hogy a számok szépen sorban állnak, annak ellenére, hogy az eredeti kép körülbelül 7°‑kal volt elforgatva. Ez a **kép forgásának javítása** varázsa, amely a könyvtárban be van építve.

## 4. lépés: Példa futtatása és az eredmények ellenőrzése

Fordítsd le és futtasd:

```bash
dotnet run
```

Ha minden helyesen van beállítva, a kinyert szöveget a konzolra fogja nyomtatni. Ha például `FileNotFoundException` kivételt kapsz, ellenőrizd a JPEG elérési útját, és győződj meg róla, hogy a fájl olvasható.

### Gyakori buktatók és profi tippek

- **Nagy képek** – az OCR memóriahasználata a kép méretével nő. Mielőtt a motorba adod, méretezd át a túl nagy fájlokat (pl. > 3000 px szélesség).  
- **Nem latin írásrendszerek** – Alapértelmezésben a motor az angolt feltételezi. Állítsd be a `ocrEngine.Settings.Language = OcrLanguage.French;` (vagy bármely támogatott nyelvet), ha más ábécében kell **recognize text image**.  
- **Kötegelt feldolgozás** – Sok fájl esetén használd újra ugyanazt a `OcrEngine` példányt; egy új motor létrehozása fájlonként felesleges terhelést okoz.  
- **Minőségellenőrzés** – A ferde kép korrigálása után exportálhatod a javított bitmapet a `ocrEngine.Settings.DeskewedImage.Save("corrected.jpg");` paranccsal, hogy vizuálisan ellenőrizd a forgatás javítását.

## Teljes működő példa (mind együtt)

Az alább látható a teljes, önálló program, amelyet beilleszthetsz a `Program.cs`‑be. Tartalmaz megjegyzéseket, hibakezelést, és egy opcionális lépést a ferde kép mentéséhez.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Settings;

namespace DeskewDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Path to the input JPEG – change this to your actual file location
            string inputPath = @"YOUR_DIRECTORY\skewed_receipt.jpg";

            if (!File.Exists(inputPath))
            {
                Console.WriteLine($"Error: File not found – {inputPath}");
                return;
            }

            try
            {
                // 1️⃣ Create OCR engine (CPU mode is sufficient for most scenarios)
                var ocrEngine = new OcrEngine();

                // 2️⃣ Enable automatic deskewing – this is the core of how to deskew image
                ocrEngine.Settings.Deskew = true;

                // Optional: Save the corrected image to verify the rotation fix
                // ocrEngine.Settings.DeskewedImagePath = "corrected.jpg";

                // 3️⃣ Perform OCR – this simultaneously deskews and extracts text
                OcrResult result = ocrEngine.Recognize(inputPath);

                // 4️⃣ Output the recognized text – effectively convert jpg to text
                Console.WriteLine("=== Recognized Text ===");
                Console.WriteLine(result.Text);
            }
            catch (Exception ex)
            {
                Console.WriteLine("An unexpected error occurred:");
                Console.WriteLine(ex.Message);
            }
        }
    }
}
```

A program futtatása **recognize text jpg** fájlokat fog feldolgozni, automatikusan kijavítja a ferdeséget, és tiszta, kereshető szöveget nyomtat a konzolra.

## Összegzés

Most már van egy stabil, éles környezetben is használható kódrészlet, amely megmutatja, **hogyan korrigáljunk ferde képet** fájlok esetén, és hogyan nyerheted ki a tartalmukat az Aspose OCR segítségével. A megközelítés működik számlák, bizonylatok, beolvasott szerződések vagy bármely JPEG esetén, ahol a szöveg nem teljesen vízszintes.

A következő lépések, amelyeket érdemes felfedezni:

- **Kötegelt feldolgozás** egy JPEG‑mappában, és minden eredmény írása egy `.txt` fájlba (kapcsolódik a *convert jpg to text* feladathoz).  
- Az OCR lépés integrálása egy ASP.NET Core API‑ba, hogy a kliensek képeket tölthessenek fel, és JSON‑formátumú szöveget kapjanak.  
- Kísérletezés különböző OCR beállításokkal, mint a `ocrEngine.Settings.Language` vagy a `ocrEngine.Settings.RecognitionMode`, a nem angol dokumentumok pontosságának javítása érdekében.  

Próbáld ki, finomítsd a beállításokat, és hagyd, hogy a motor végezze a nehéz munkát. Ahogy mindig, ha elakadsz vagy van egy okos optimalizációd, oszd meg a megjegyzésben. Jó kódolást!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}