---
category: general
date: 2026-03-29
description: Szöveg kinyerése képből Aspose OCR segítségével C#-ban. Tanulja meg az
  automatikus forgatású OCR-t és a beolvasott kép kiegyenesítését a tökéletes eredményért.
draft: false
keywords:
- extract text from image
- auto rotate ocr
- how to deskew scanned image
- Aspose OCR C#
- image preprocessing OCR
language: hu
og_description: Képről szöveg kinyerése az Aspose OCR-rel. Ez az útmutató bemutatja
  az automatikus forgatású OCR-t és azt, hogyan lehet kiegyenesíteni a beolvasott
  képet C#-ban.
og_title: Szöveg kinyerése képből C#-ban – Automatikus forgatás OCR és kiegyenesítés
tags:
- C#
- OCR
- Aspose
- Image Processing
title: Képről szöveg kinyerése C#‑ban – Automatikus forgatás OCR és kiegyenesítés
  útmutató
url: /hu/net/ocr-optimization/extract-text-from-image-in-c-auto-rotate-ocr-deskew-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kép szövegének kinyerése C#‑ban – Automatikus forgatás OCR és kiegyenesítés útmutató

Valaha is szükséged volt **szöveg kinyerésére képből**, de a fájl egy furcsa szögben érkezett? Ez gyakori fejfájás – különösen, ha beolvasott számlákkal, fényképezett nyugtákkal vagy ferde PDF‑ekkel dolgozol. A jó hír, hogy nem kell saját forgatási algoritmust írnod. Az Aspose OCR beépített *auto rotate OCR* funkciójával a motor egyenlíti a képet, majd **szöveg kinyerése képből** egyetlen sima lépésben történik.

Ebben a bemutatóban egy teljes, azonnal futtatható C# programon keresztül mutatjuk be, hogyan:

* Inicializáljuk az OCR motorját automatikus tájolással és kiegyenesítéssel,
* Felismerünk egy elforgatott vagy ferde képet,
* Visszakapjuk a detektált forgatási szöget és a kinyert szöveget.

Nincs külső szolgáltatás, nincs bonyolult matematikai számítás – csak néhány kódsor és egy világos magyarázat arra, hogyan **kiegyenesítsd a beolvasott képet**, ha szükséges.

## Amit szükséged lesz

| Előfeltétel | Miért fontos |
|--------------|----------------|
| .NET 6.0 vagy újabb (vagy .NET Framework 4.6+) | Az Aspose OCR NuGet csomagként érhető el, amely ezeket a futtatókörnyezeteket célozza. |
| Visual Studio 2022 (vagy bármely C# szerkesztő) | Egyszerűvé teszi a NuGet csomagok hozzáadását és a konzolos alkalmazás futtatását. |
| Minta kép (`rotated_document.jpg`) | A fájlnak JPEG, PNG, BMP vagy TIFF formátumúnak kell lennie, és nem lehet tökéletesen függőleges. |
| Aspose.OCR NuGet csomag (`Install-Package Aspose.OCR`) | Biztosítja az `OcrEngine`, `PreprocessingFilters` és a kapcsolódó típusokat. |

Ha ezek a dobozok be vannak jelölve, már indulhatsz. Ha nem, szerezd be a legújabb Aspose OCR‑t a NuGet‑ről – egy kattintásos telepítés.

---

## 1. lépés – Az OCR motor inicializálása (Elsődleges kulcsszó akcióban)

Az első dolog, amit teszünk, hogy létrehozunk egy `OcrEngine` példányt, és beállítjuk, hogy **auto rotate OCR** és **deskew** legyen minden bejövő képre. Ez a két jelző bitwise OR‑ral (`|`) van kombinálva, mivel a `PreprocessingFilters` egy `[Flags]` attribútummal ellátott enum.

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // Initialise the OCR engine with English language and preprocessing options
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = Language.English,
            // Enable both auto‑rotate and auto‑deskew
            Preprocessing = PreprocessingFilters.AutoRotate | PreprocessingFilters.AutoDeskew
        };
```

> **Miért fontos:**  
> *Auto‑rotate OCR* megvizsgálja a kép szöveg‑alapvonalát, kitalálja a helyes tájolást, és belsőleg elforgatja a felismerés előtt. *Auto‑deskew* ugyanezt teszi a gyakran előforduló enyhe ferdeségek esetén. Mindkettő engedélyezésével a legjobb **szöveg kinyerése képből** eredményt kapod manuális képszerkesztés nélkül.

---

## 2. lépés – Kép felismerése és az eredmény lekérése

Most átadjuk a motor számára a fájl útvonalát. A `RecognizeImage` metódus egy `OcrResult` objektumot ad vissza, amely tartalmazza a detektált forgatási szöget, a biztonsági pontszámokat és a nyers szöveges kimenetet.

```csharp
        // Recognise the image file and obtain the OCR result
        OcrResult ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/rotated_document.jpg");
```

> **Tipp:** Ha egy stream‑el dolgozol (pl. feltöltött fájl), használd a `ocrEngine.RecognizeImage(Stream)` metódust. A ugyanazok a előfeldolgozó jelzők érvényesek, így továbbra is élvezheted az **auto rotate OCR** előnyeit.

---

## 3. lépés – A forgatási szög és a kinyert szöveg megjelenítése

Végül két információt nyomtatunk a konzolra: a motor által becsült forgatási szöget, valamint a ténylegesen kinyert szöveget.

```csharp
        // Show the detected rotation and the recognised text
        Console.WriteLine($"Detected rotation: {ocrResult.RotationAngle}°");
        Console.WriteLine("----- Extracted Text -----");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Várt kimenet** (a számaid az input képtől fognak eltérni):

```
Detected rotation: 12.3°
----- Extracted Text -----
Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
Thank you for your business!
```

Ha a kép már függőleges volt, a forgatási szög `0°` lesz, és a *auto‑deskew* algoritmusnak köszönhetően továbbra is tiszta szöveget kapsz.

---

## 4. lépés – A „hogyan kiegyenesítsük a beolvasott képet” megértése (Másodlagos kulcsszó mélymerülés)

Elgondolkodhatsz, *hogyan kiegyenesítsük a beolvasott képet*, amikor az OCR motor nem‑nulla forgatást jelez. A háttérben az Aspose OCR egy **Hough transzformációt** alkalmaz a domináns szövegsor tájolásának meghatározására. Ezután a bitmapet a szög ellentétesével forgatja, ezzel egyenlíti a szöveget.

**Mikor számít ez?**  
* Szkennerek, amelyek papírt enyhén ferde módon adagolnak (gyakori irodai környezetben).  
* Kézben tartott okostelefonos fényképek – a horizont ritkán tökéletes.  

**Különleges esetek kezelése:**  
Ha a `RotationAngle` értéke szokatlanul nagy (pl. > 45°), a motor félreérthette a képet (lehet, hogy egy logó vagy nem‑szöveges grafika). Ebben az esetben:

1. Manuálisan forgasd el a képet a `System.Drawing` használatával, mielőtt átadod a motorba, vagy  
2. Kapcsold ki az `AutoRotate`‑t, és csak az `AutoDeskew`‑et hagyd bekapcsolva, ha tudod, hogy a dokumentum már függőleges.

```csharp
// Example: manually rotate 90° clockwise before OCR
using (var img = Aspose.OCR.Image.Load("rotated_document.jpg"))
{
    img.Rotate(90);
    OcrResult result = ocrEngine.RecognizeImage(img);
    Console.WriteLine(result.Text);
}
```

---

## 5. lépés – Gyakori buktatók és profi tippek (E‑E‑A‑T akcióban)

| Buktató | Miért fordul elő | Megoldás |
|---------|------------------|----------|
| **Elmosódott vagy alacsony felbontású képek** | Az OCR pontossága drámaian csökken; a forgatási detektálás is kudarcot vallhat. | Használj legalább 300 dpi‑s beolvasásokat; alkalmazz élesítő szűrőt az OCR előtt. |
| **Vegyes nyelvek** | A motor alapértelmezés szerint angolt használ; a külföldi karakterek torzulnak. | Állítsd be `Language = Language.English | Language.Spanish` (vagy a megfelelő kombinációt). |
| **Nagy fájlok (> 10 MB)** | Memória nyomás `OutOfMemoryException`‑t okozhat. | Először méretezd le a képet, vagy dolgozz csempékben a `OcrEngine.RecognizeRegion` használatával. |
| **Helytelen fájlútvonal** | `FileNotFoundException` leállítja a programot. | Használd a `Path.Combine(Environment.CurrentDirectory, "rotated_document.jpg")`‑t a robusztusságért. |

> **Profi tipp:** Mindig naplózd az `ocrResult.RotationAngle` és az `ocrResult.Confidence` (ha elérhető) értékeket. Ezek a metrikák segítenek eldönteni, hogy érdemes‑e újra próbálkozni más előfeldolgozási beállításokkal.

---

## 6. lépés – A példa bővítése (Mi a következő?)

Most, hogy **szöveg kinyerése képből** automatikus forgatással és kiegyenesítéssel már működik, gondold át a következő lépéseket:

* **Kötegelt feldolgozás** – Iterálj egy mappában lévő képeken, tárold az eredményeket egy adatbázisban, és jelöld meg azokat, ahol a `RotationAngle > 5°` manuális ellenőrzést igényel.  
* **PDF konvertálás** – Kombináld a kinyert szöveget az eredeti képpel egy kereshető PDF‑ben az Aspose.PDF segítségével.  
* **Nyelvfelismerés** – Használd az Aspose.OCR `AutoDetectLanguage` jelzőjét, hogy a motor automatikusan a legmegfelelőbb nyelvet válassza.  

Ezek mind ugyanazon alapelvre épülnek: hagyd, hogy a könyvtár kezelje a tájolást, te pedig az üzleti logikára koncentrálj.

---

## Teljes működő példa (Másolás‑beillesztés kész)

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialise the OCR engine with auto‑rotate and auto‑deskew
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = Language.English,
            Preprocessing = PreprocessingFilters.AutoRotate | PreprocessingFilters.AutoDeskew
        };

        // 2️⃣ Recognise the image – replace the path with your own file
        string imagePath = "YOUR_DIRECTORY/rotated_document.jpg";
        OcrResult ocrResult = ocrEngine.RecognizeImage(imagePath);

        // 3️⃣ Output the rotation angle and the recognised text
        Console.WriteLine($"Detected rotation: {ocrResult.RotationAngle}°");
        Console.WriteLine("----- Extracted Text -----");
        Console.WriteLine(ocrResult.Text);
    }
}
```

Mentsd a fájlt `Program.cs` néven, futtasd a `dotnet add package Aspose.OCR` parancsot, majd `dotnet run`. A konzolon meg kell jelennie a szögnek és a tiszta szövegnek.

---

## Összegzés

Most bemutattuk, hogyan **szöveg kinyerése képből** C#‑ban, miközben az Aspose OCR gondoskodik az *auto rotate OCR*‑ról és a bonyolult *hogyan kiegyenesítsük a beolvasott képet* problémáról. A két előfeldolgozó jelző engedélyezésével a motor automatikusan egyenesíti a ferde képeket, felismeri a helyes tájolást, és pontos szöveget ad – manuális képszerkesztés nélkül.

Nyugodtan kísérletezz nagyobb kötegekkel, különböző nyelvekkel, vagy integráld a kimenetet egy kereshető PDF‑be. A lehetőségek csak a képzeletedre vannak korlátozva, amíg az OCR motor elvégzi a nehéz munkát.

**Készen állsz, hogy szintet lépj a dokumentumfolyamodban?** Vedd a kódot, irányítsd a saját beolvasásaidra, és nézd, ahogy a forgatási szögek eltűnnek. Ha bármi akadályba ütközöl, írj egy megjegyzést alul – jó kódolást!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}