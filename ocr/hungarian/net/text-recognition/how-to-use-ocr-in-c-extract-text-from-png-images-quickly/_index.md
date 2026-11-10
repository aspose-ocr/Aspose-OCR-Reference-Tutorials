---
category: general
date: 2026-03-29
description: Hogyan használjuk az OCR-t az Aspose-szal szöveg kinyerésére PNG fájlokból
  és képek szöveggé konvertálására. Tanulja meg lépésről lépésre az aszinkron OCR-t
  C#-ban.
draft: false
keywords:
- how to use OCR
- extract text from png
- convert images to text
- extract text from images
language: hu
og_description: Hogyan használjunk OCR-t az Aspose-szal C#-ban PNG-fájlok szövegének
  kinyeréséhez. Ez az útmutató végigvezet az aszinkron OCR-en, a kódon és a tippeken.
og_title: Hogyan használjunk OCR-t C#-ban – Szöveg kinyerése PNG képekből
tags:
- OCR
- C#
- Aspose
title: Hogyan használjuk az OCR-t C#-ban – Szöveg gyors kinyerése PNG képekből
url: /hu/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-png-images-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan használjunk OCR-t C#‑ban – Szöveg kinyerése PNG képekből gyorsan

Gondolkodtál már azon, **hogyan használjunk OCR-t**, hogy szöveget nyerjünk ki néhány PNG képernyőképből? Lehet, hogy beolvasott nyugtákat, számlákat vagy UI maketteket (mock‑up) szereztél, és a szöveget kereshető formátumban kellene. A jó hír? Az Aspose.OCR-rel néhány sor aszinkron C# kóddal konvertálhatod a képeket szöveggé.  

Ebben az útmutatóban pontosan megmutatjuk, hogyan nyerjünk ki szöveget PNG fájlokból, elmagyarázzuk, miért fontos minden lépés, és adunk egy azonnal futtatható programot, amely minden oldalra kiírja a felismert szöveget. A végére képes leszel **szöveget kinyerni képekből**, anélkül, hogy a dokumentációban keresgélnél.

## Mit tanulhatsz meg

- Az Aspose.OCR NuGet csomag telepítése és hivatkozása.  
- Az OCR motor inicializálása és a nyelv beállítása (ebben a példában angol).  
- PNG fájlok tömbjének átadása a `RecognizeImagesAsync` metódusnak a gyors, nem blokkoló feldolgozáshoz.  
- A `OcrResult` objektumok bejárása és a kinyert karakterláncok kiírása.  

Nincs külső szolgáltatás, nincs bonyolult visszahívás—csak tiszta, aszinkron C#, amely a .NET 6+ verziókon működik.

---

## Előfeltételek

| Követelmény | Indoklás |
|-------------|----------|
| .NET 6 SDK (vagy újabb) | Modern nyelvi funkciók, mint a `async Main`. |
| Visual Studio 2022 vagy VS Code | IDE a kód fordításához és futtatásához. |
| Aspose.OCR NuGet csomag (`Aspose.OCR`) | Biztosítja a mintában használt `OcrEngine` osztályt. |
| Néhány PNG kép (`page1.png`, `page2.png`, …) | Bemeneti fájlok az OCR folyamathoz. |

Ha már van egy .NET projekted, egyszerűen futtasd a `dotnet add package Aspose.OCR` parancsot. Ellenkező esetben hozz létre egy új konzolos alkalmazást a `dotnet new console -n OcrDemo` paranccsal.

---

## 1. lépés: Aspose.OCR telepítése és a projekt beállítása

Először add hozzá az OCR könyvtárat a projektedhez:

```bash
dotnet add package Aspose.OCR
```

Miért fontos: Az Aspose.OCR tartalmazza a natív OCR motorot, nyelvi csomagokat és egy egyszerű API‑t. NuGet‑en keresztül történő beszerzése garantálja a verziókompatibilitást és az automatikus frissítéseket.

---

## 2. lépés: Az OCR motor inicializálása és nyelv kiválasztása

A motornak tudnia kell, melyik nyelvet keresse. Az angol a leggyakoribb, de cserélheted a `Language.Spanish`, `Language.French` stb. értékekre.

```csharp
using Aspose.OCR;

// ...

// Step 2: Create the engine and set the language to English
var ocrEngine = new OcrEngine
{
    Language = Language.English   // Change this if you need a different language
};
```

> **Pro tipp:** Mindig állítsd be a nyelvet kifejezetten; az alapértelmezett használata csökkentheti a pontosságot és növelheti a feldolgozási időt.

---

## 3. lépés: PNG fájlok listájának előkészítése

Egyetlen fájlt vagy egy tömböt is átadhatsz. Tömb átadása lehetővé teszi, hogy a motor aszinkron módon kötegelt feldolgozza őket, ami ideális néhány oldal esetén.

```csharp
// Step 3: Define the image files you want to process
string[] imagePaths = { "page1.png", "page2.png", "page3.png" };
```

Ha a képek egy almappában vannak, egyszerűen előzd meg a relatív úttal (`"images/page1.png"`). A motor egyértelmű `FileNotFoundException`‑t dob, ha az útvonal hibás – ezért ellenőrizd a fájlneveket.

---

## 4. lépés: Aszinkron OCR futtatása minden képen

A `RecognizeImagesAsync` metódus egy `OcrResult` tömböt ad vissza. Mivel aszinkron, a felhasználói felület (vagy a konzol) reagálók marad, amíg az OCR a háttérben fut.

```csharp
// Step 4: Perform async OCR on every image
OcrResult[] ocrResults = await ocrEngine.RecognizeImagesAsync(imagePaths);
```

**Miért aszinkron?**  
Ha OCR‑t egy web API‑ba vagy asztali alkalmazásba integrálsz, nem szeretnéd, hogy a szál blokkolódjon, amíg a motor minden pixelt átvizsgál. Az `await` visszaadja a szálat a szálkészletnek, ezáltal növelve a skálázhatóságot.

---

## 5. lépés: A kinyert szöveg megjelenítése minden oldalhoz

Most, hogy megvannak az eredmények, iterálj végig rajtuk, és írd ki a felismert szöveget. A `Text` tulajdonság a sima szöveges kimenetet tartalmazza, készen áll a további feldolgozásra (pl. adatbázisba mentés).

```csharp
// Step 5: Output the recognized text for every page
for (int i = 0; i < ocrResults.Length; i++)
{
    Console.WriteLine($"--- Page {i + 1} ---");
    Console.WriteLine(ocrResults[i].Text);
}
```

### Várható kimenet

Tegyük fel, hogy a `page1.png` tartalmazza a „Invoice #12345” szöveget, a `page2.png` pedig a „Total: $89.99” szöveget, akkor valami ilyesmit látsz majd:

```
--- Page 1 ---
Invoice #12345
Date: 03/28/2026
--- Page 2 ---
Total: $89.99
Paid by: Credit Card
```

Ha az OCR nem talál szöveget, a `Text` tulajdonság egy üres karakterlánc lesz – kezeld ezt a helyzetet a produkciós kódban a `string.IsNullOrWhiteSpace` ellenőrzésével.

---

## Teljes működő példa

Az alábbiakban a teljes programot találod, amelyet beilleszthetsz a `Program.cs`‑be. Tartalmazza az összes using direktívát, az aszinkron `Main`‑t és a lépéseket magyarázó megjegyzéseket.

```csharp
using System;
using System.Threading.Tasks;
using Aspose.OCR;

class Program
{
    // Async Main is supported from C# 7.1 onward
    static async Task Main()
    {
        // Step 1: Initialize the OCR engine and set the language to English
        var ocrEngine = new OcrEngine { Language = Language.English };

        // Step 2: Define the image files to be processed
        string[] imagePaths = { "page1.png", "page2.png", "page3.png" };

        // Step 3: Perform asynchronous OCR on all images
        OcrResult[] ocrResults = await ocrEngine.RecognizeImagesAsync(imagePaths);

        // Step 4: Output the recognized text for each page
        for (int i = 0; i < ocrResults.Length; i++)
        {
            Console.WriteLine($"--- Page {i + 1} ---");
            Console.WriteLine(ocrResults[i].Text);
        }
    }
}
```

Mentsd el a fájlt, helyezd a PNG‑eket a futtatható fájl mellé (vagy állítsd be az útvonalakat), és futtasd:

```bash
dotnet run
```

A konzolon meg kell jelennie a kinyert szövegnek, ami megerősíti, hogy sikeresen **képeket szöveggé konvertáltál**.

---

## Gyakori edge case‑ek kezelése

| Helyzet | Mit kell tenni |
|---------|----------------|
| **Alacsony felbontású PNG** | Növeld a `ocrEngine.ImageProcessingOptions.Dpi` értékét a felismerés előtt. |
| **Több nyelv** | Állítsd be a `ocrEngine.Language = Language.English | Language.Spanish;` (bitwise OR). |
| **Nagy köteg (százak fájl)** | Dolgozd fel darabokban (pl. 20 fájl per `RecognizeImagesAsync` hívás) a memóriacsúcsok elkerülése érdekében. |
| **Bizalmi pontszámra van szükség** | Használd a `ocrResults[i].Confidence`‑t (0 és 1 közötti float) az alacsony minőségű eredmények szűréséhez. |

Ezek a finomhangolások a OCR csővezetékedet robusztussá teszik, különösen, ha a demóról a produkcióra váltasz.

---

## Bónusz: Az eredmények mentése szövegfájlba

Ha inkább tartós másolatot szeretnél a konzol kimenet helyett, adj hozzá egy kis segédfüggvényt:

```csharp
using System.IO;

// After the for‑loop:
File.WriteAllLines("OcrOutput.txt", ocrResults.Select(r => r.Text));
Console.WriteLine("All pages saved to OcrOutput.txt");
```

Most már van egyetlen fájlod, amely **képekből szöveget nyer ki** a további feldolgozáshoz – tökéletes indexeléshez, kereséshez vagy egy nyelvi modellnek való betápláláshoz.

---

## Következtetés

Áttekintettük, **hogyan használjunk OCR-t** C#‑ban az Aspose‑szal, hogy **szöveget nyerjünk ki PNG** fájlokból és **képeket szöveggé konvertáljunk** hatékonyan. Az aszinkron megközelítés biztosítja, hogy az alkalmazásod reagáló maradjon, míg a egyszerű API a kódot olvashatóvá és karbantarthatóvá teszi.

Próbáld ki a saját dokumentumaiddal, kísérletezz különböző nyelvekkel, és akár láncolhatod is a kimenetet egy keresőindexbe vagy összegző szolgáltatásba. A lehetőségek határtalanok, ha megbízhatóan tudod a képeket kereshető karakterláncokká alakítani.

---

### Következő lépések és kapcsolódó témák

- **Szöveg kinyerése képekből** más formátumokban (JPEG, TIFF) – csak cseréld a fájl kiterjesztéseket.  
- **Kötegelt feldolgozás Parallel.ForEach‑el** nagy mennyiségű feladat esetén.  
- **Post‑OCR tisztítás** reguláris kifejezésekkel a dátumok, összegek vagy azonosítók normalizálásához.  
- **Integrálás Azure Cognitive Services‑szel** ha felhőalapú OCR‑ra és extra funkciókra van szükséged.  

Nyugodtan hagyj megjegyzést, ha elakadsz, vagy oszd meg, hogyan bővítetted ezt az alapfolyamatot. Boldog kódolást!   (Image: ![OCR result screenshot showing extracted text](/images/ocr-result.png){.align-center alt="OCR használati példa kimenete"} )

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}