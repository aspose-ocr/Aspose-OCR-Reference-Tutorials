---
category: general
date: 2026-03-18
description: Készíts kereshető PDF-et az Aspose OCR-rel C#-ban. Konvertáld a képet
  PDF-re, adj hozzá OCR szövegréteget, és írd a PDF bájtokat fájlba néhány egyszerű
  lépésben.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- recognize text from image
- add ocr text layer
- write pdf bytes to file
language: hu
og_description: Gyorsan hozzon létre kereshető PDF-et az Aspose OCR-rel C#-ban. Tanulja
  meg, hogyan konvertáljon képet PDF-be, adjon hozzá OCR szövegréteget, és írja a
  PDF bájtokat fájlba.
og_title: Kereshető PDF létrehozása képből – Gyors C# OCR útmutató
tags:
- OCR
- PDF
- C#
- Aspose
title: Kereshető PDF létrehozása képből OCR-rel – C# útmutató
url: /hu/net/text-recognition/create-searchable-pdf-from-image-with-ocr-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kereshető PDF létrehozása képből OCR-rel – C# útmutató

Szükséged volt már **kereshető PDF** létrehozására egy beolvasott képből? Az Aspose OCR segítségével néhány sorban megteheted, nehéz könyvtárak nélkül. Ebben az útmutatóban **képet konvertálunk PDF‑be**, ráhelyezünk egy **OCR szövegréteget**, és végül **PDF bájtokat írunk fájlba**, így egy szabványoknak megfelelő PDF/A‑2b dokumentumot kapsz, amelyet a felhasználóid ténylegesen kereshetnek.

Ha azon tűnődsz, miért érdemes kereshető PDF‑et készíteni egy egyszerű csak képet tartalmazó fájl helyett, gondolj a felhasználói élményre: egy kereshető PDF lehetővé teszi a szöveg másolását, kijelölését és indexelését – nagyszerű archívumokhoz, jogi dokumentumokhoz vagy bármilyen munkafolyamathoz, amely később szövegkinyerést igényel. Vágjunk bele.

## Amire szükséged lesz

- .NET 6 vagy újabb (a kód .NET Framework 4.7+ alatt is működik)
- Aspose.OCR NuGet csomag (`Aspose.OCR` 23.10 vagy újabb verzió)
- Raster kép (`.png`, `.jpg`, stb.), amelyet kereshető PDF‑vé szeretnél alakítani
- Alapvető C# ismeretek – semmi bonyolult, csak az alapok

Ennyi. Nincs külső eszköz, nincs extra konverter. Minden nehéz feladatot az Aspose OCR motor végez.

## Kereshető PDF létrehozása – Áttekintés

Mielőtt a kódba merülnénk, vázoljuk fel a folyamatot:

1. **Példányosítsd** az OCR motorját – ez az objektum tudja, hogyan olvassa a szöveget a képekről.  
2. **Töltsd be** a forrásképet – egy `ImageStream`‑et adunk a motorhoz.  
3. **Állítsd be** a PDF/A‑2b mentési beállításokat – ez azt mondja az Aspose‑nak, hogy ágyazza be a felismert szöveget rejtett rétegként.  
4. **Futtasd** az OCR‑t és **rögzítsd** a keletkezett PDF bájtokat.  
5. **Írd** ezeket a bájtokat a lemezre, így létrehozva a végső kereshető PDF fájlt.

Ezek a lépések közvetlenül egy-két C# sorra vezetnek, így az egész munkafolyamat egy apró szkriptnek tűnik, nem egy hatalmas projektnek.

## 1. lépés: Kép konvertálása PDF‑be – Kép betöltése

Először is: meg kell adnunk az OCR motorjának valamit, amit olvashasson. A `ImageStream.FromFile` segédfüggvény betölti a fájlt egy áramlásba, amelyet az Aspose feldolgozhat.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Output;
using System;

// 1️⃣ Load the source image you want to turn into a searchable PDF
ImageStream image = ImageStream.FromFile("YOUR_DIRECTORY/input.png");
```

> **Pro tipp:** Tartsd a kép felbontását 300 dpi vagy magasabb szinten; az OCR pontossága drámaian csökken az alacsony felbontású beolvasásoknál.

## 2. lépés: Szöveg felismerése a képből és OCR szövegréteg hozzáadása

Most létrehozzuk az OCR motorját és megmondjuk neki, hogy ismerje fel a szöveget. A varázslat akkor történik, amikor a felismerési eredményt egy `PdfSaveOptions`‑szel párosítjuk, amelyben `IncludeTextLayer = true`. Ez a jelző arra kényszeríti az Aspose‑t, hogy a kinyert karaktereket egy láthatatlan szövegrétegként ágyazza be, ami a PDF‑et kereshetővé teszi.

```csharp
// 2️⃣ Create the OCR engine instance
OcrEngine ocrEngine = new OcrEngine();

// 3️⃣ Set up PDF/A‑2b save options – includes the hidden text layer
PdfSaveOptions pdfSaveOptions = new PdfSaveOptions
{
    PdfCompliance = PdfCompliance.PdfA2b, // ensures PDF/A‑2b compliance
    IncludeTextLayer = true               // this is the key for searchable PDFs
};
```

Miért PDF/A‑2b? Ez egy ISO‑szabványú archiválási formátum, amely garantálja a hosszú távú megőrzést, és számunkra fontos, hogy a PDF tartalmazzon kereshető szövegréteget. Ha nincs szükséged archiválási megfelelésre, elhagyhatod a `PdfCompliance` beállítást, de megtartása nem jelent plusz költséget.

## 3. lépés: PDF bájtok írása fájlba – Az eredmény mentése

Miután a motor készen áll és a beállítások megvannak, futtatjuk a felismerést, és azonnal kérjük az Aspose‑t, hogy adja meg a PDF‑et `byte[]`‑ként. Ezután a `File.WriteAllBytes`‑szal írjuk a bájtokat a lemezre. Egyszerű, de hatékony.

```csharp
// 4️⃣ Perform OCR on the image and get the PDF bytes
byte[] pdfBytes = ocrEngine.Recognize(image).Save(pdfSaveOptions);

// 5️⃣ Write the PDF/A‑2b file to the output location
System.IO.File.WriteAllBytes("YOUR_DIRECTORY/output.pdf", pdfBytes);
Console.WriteLine("PDF/A‑2b file created – you now have a searchable PDF!");
```

Ez a `Console.WriteLine` sor opcionális, de azonnali visszajelzést ad, amikor a programot terminálból futtatod.

## Teljes működő példa

Mindent összevonva, itt a teljes, azonnal futtatható program. Másold be egy új konzolprojektbe, cseréld le a `YOUR_DIRECTORY`‑t egy valós útvonalra, és nyomd meg a **F5**‑öt.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Output;
using System;

class PdfA2bDemo
{
    static void Main()
    {
        // Step 1: Load the source image
        ImageStream image = ImageStream.FromFile("YOUR_DIRECTORY/input.png");

        // Step 2: Create OCR engine and configure PDF/A‑2b options
        OcrEngine ocrEngine = new OcrEngine();
        PdfSaveOptions pdfSaveOptions = new PdfSaveOptions
        {
            PdfCompliance = PdfCompliance.PdfA2b,
            IncludeTextLayer = true
        };

        // Step 3: Recognize and save as PDF bytes
        byte[] pdfBytes = ocrEngine.Recognize(image).Save(pdfSaveOptions);

        // Step 4: Write the bytes to a searchable PDF file
        System.IO.File.WriteAllBytes("YOUR_DIRECTORY/output.pdf", pdfBytes);
        Console.WriteLine("PDF/A‑2b file created.");
    }
}
```

### Várt kimenet

- `output.pdf` nevű fájl jelenik meg a megadott mappában.  
- Nyisd meg az Adobe Acrobat Readerben vagy bármely PDF‑olvasóban, és próbáld ki a szöveg kijelölését – ha tudsz szavakat másolni, sikeresen **létrehoztad a kereshető PDF‑et**.  
- A dokumentum át fog menni a PDF/A‑2b validációs eszközökön is, mivel a megfelelő megfelelőségi jelzőt használtuk.

## Gyakori kérdések és széljegyek

**Mi van, ha a képem több oldalt tartalmaz?**  
Csomagold minden oldalt egy saját `ImageStream`‑be, és add őket sorban az `OcrEngine`‑nek. Az Aspose automatikusan egyetlen PDF‑be fűzi össze az oldalakat.

**Módosíthatom az OCR nyelvet?**  
Természetesen. Állítsd be a `ocrEngine.Language = Language.English;`‑t (vagy bármely támogatott nyelvet) a `Recognize` hívása előtt.

**Mi a helyzet a memóriahasználattal nagy fájlok esetén?**  
Ha gigabájt méretű beolvasásokat dolgozol fel, fontold meg az eredmény közvetlen streamelését egy `FileStream`‑ba, ahelyett, hogy az egész `byte[]`‑t a memóriában tartanád:

```csharp
using (var file = new FileStream("output.pdf", FileMode.Create))
{
    ocrEngine.Recognize(image).Save(pdfSaveOptions, file);
}
```

**Szükségem van licencre?**  
Az Aspose ingyenes próbaidőszakot kínál vízjel‑nélküli értékeléssel. Gyártási használathoz vásárolj licencet a kiértékelő banner eltávolításához és a teljes funkciók feloldásához.

## Tippek a jobb OCR pontossághoz

- **Előfeldolgozd** a képet: egyenesítsd, távolítsd el a zajt, és növeld a kontrasztot.  
- **Használj veszteségmentes formátumokat**, mint a PNG; a JPEG tömörítési hibái összezavarhatják a motort.  
- **Kerüld a színes háttereket**; egy egyszerű fehér háttér adja a legjobb eredményt.

## Következő lépések

Most, hogy **kereshető PDF‑et tudsz létrehozni**, esetleg szeretnéd:

- `Directory.GetFiles` használatával **kötegelt feldolgozni** egy mappában lévő képeket.  
- Később **kivonni a rejtett szöveget** a `PdfDocument` API‑kkal indexeléshez.  
- Az OCR‑t **digitális aláírásokkal kombinálni**, hogy manipulációra ellenálló archívumokat hozz létre.

Ezek mind ugyanarra az alapmintára épülnek, amit bemutattunk: betöltés, felismerés, konfigurálás, mentés.

---

*Készen állsz, hogy a beolvasott archívumaidat kereshető PDF‑ekké alakítsd? Szerezd meg a kódot, irányítsd a képeidre, és hagyd, hogy az Aspose végezze a nehéz munkát. Boldog kódolást!*

![Kereshető PDF példa](/images/create-searchable-pdf.png "Illusztráció egy képből generált kereshető PDF-ről")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}