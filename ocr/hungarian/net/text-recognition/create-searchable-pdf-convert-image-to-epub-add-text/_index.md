---
category: general
date: 2026-03-13
description: Készíts kereshető PDF-et bármilyen képből az Aspose OCR segítségével.
  Tanulja meg, hogyan konvertálja a képet EPUB formátumba, adjon hozzá kereshető szöveget,
  és generáljon kereshető PDF-et C#-ban.
draft: false
keywords:
- create searchable pdf
- convert image to epub
- ocr image to pdf
- add searchable text
- generate searchable pdf
language: hu
og_description: Készíts kereshető PDF-et bármilyen képből az Aspose OCR használatával.
  Ez az útmutató bemutatja, hogyan konvertálhatod a képet EPUB formátumba, hogyan
  adhatod hozzá a kereshető szöveget, és hogyan generálhatsz kereshető PDF-et C#-ban.
og_title: Kereshető PDF létrehozása – Kép konvertálása EPUB formátumba és szöveg hozzáadása
tags:
- Aspose OCR
- C#
- PDF
- EPUB
title: Kereshető PDF létrehozása – Kép EPUB formátumba konvertálása és szöveg hozzáadása
url: /hu/net/text-recognition/create-searchable-pdf-convert-image-to-epub-add-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kereshető PDF létrehozása – Kép konvertálása EPUB‑ra és szöveg hozzáadása

Szeretnél **kereshető PDF‑et** létrehozni egy beolvasott nyugtáról vagy bármely képről? Ebben az útmutatóban megmutatjuk, hogyan készíts kereshető PDF‑et az Aspose OCR segítségével, miközben **képet konvertálsz EPUB‑ra** és **kereshető szövegréteget** adsz hozzá – mindezt egyetlen C# projektben.

Ha már előfordult, hogy szép, de nem kereshető PDF‑ekkel dolgoztál, nem vagy egyedül. A rejtett szövegréteg egy lapos képet teljesen kereshető dokumentummá változtat, és az Aspose ezt szinte fájdalommentesen megoldja.

## Amit megtanulsz

* Hogyan inicializáljuk az Aspose OCR motorját és állítjuk be a nyelvet.  
* A pontos lépések a **kép EPUB‑ra konvertálásához** e‑könyv terjesztéshez.  
* Hogyan konfiguráljuk a PDF írót, hogy a kimenet rejtett, kereshető szövegréteget tartalmazzon.  
* Tippek a szélhelyzetek kezeléséhez, például többoldalas nyugták vagy nem angol nyelvek esetén.  

Minden, amire előzetesen szükséged van, egy .NET fejlesztői környezet (Visual Studio 2022 vagy újabb) és egy Aspose OCR NuGet csomag. Nincs külső szolgáltatás, nincs bonyolult konfigurációs fájl – csak egyszerű C# kód, amit másolhatsz‑beilleszthetsz és futtathatsz.

## Előfeltételek

| Követelmény | Miért fontos |
|-------------|--------------|
| .NET 6.0+   | Az Aspose OCR a .NET Standard 2.0+ célplatformot használja, így a .NET 6 a legújabb futtatókörnyezet‑fejlesztéseket biztosítja. |
| Aspose.OCR NuGet csomag | Biztosítja az `OcrEngine`, `EpubWriter` és `PdfWriter` osztályokat, amelyeket a kódban használunk. |
| Képfájl (pl. `receipt.jpg`) | Az a forrás, amelyen az OCR‑t futtatni fogod. Bármely raszteres kép (PNG, JPEG, BMP) megfelelő. |
| Alap C# ismeretek | A kódrészleteket olvasni és módosítani fogod, nem pedig a nyelvet tanulni kell először. |

A csomagot a következő paranccsal telepítheted:

```bash
dotnet add package Aspose.OCR
```

> **Pro tip:** Ha Visual Studio‑t használsz, a NuGet Package Manager UI ugyanazt a feladatot elvégzi – csak keresd meg a “Aspose.OCR” kifejezést.

## 1. lépés – Kereshető PDF létrehozása az Aspose OCR‑rel

Az első dolog, amire szükségünk van, egy `OcrEngine` példány, amely tudja, melyik nyelvet kell felismertesse. Az angol az alapértelmezett, de a `ocrEngine.Language` beállításával könnyen cserélhető francia, német stb. nyelvre.

```csharp
using Aspose.OCR;
using Aspose.OCR.Output;

// Initialise the OCR engine and set the language
OcrEngine ocrEngine = new OcrEngine
{
    Language = Language.English          // Change this if your document isn’t English
};
```

Miért inicializáljuk először a motort? A motor a felismerési modellt a memóriában tartja, így egyszer létrehozni és több kép esetén újra‑használni CPU‑t és RAM‑ot takarít meg. Nagyobb kötegelt feladatoknál a teljes futtatás során ugyanazt a példányt tartanád életben.

## 2. lépés – Kép betöltése és OCR végrehajtása

Ezután a motort a feldolgozni kívánt fájlra irányítjuk. Az `ImageStream.FromFile` beolvassa a képet egy olyan formátumba, amelyet az OCR motor ért.
 
```csharp
// Load the image you want to process
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/receipt.jpg");

// Run the recognition engine – this populates the internal text buffer
ocrEngine.Recognize();
```

> **Mi van, ha a kép több oldalas?**  
> Az Aspose OCR natívan kezeli a többoldalas TIFF‑eket. Csak add meg a TIFF fájl elérési útját; a motor automatikusan végigiterál az egyes oldalakon.

## 3. lépés – Kép konvertálása EPUB‑ra

Ha a beolvasott dokumentumhoz e‑könyv változatra is szükséged van, az Aspose egyetlen sorban megoldja. Az `EpubWriter` ugyanazt a `OcrEngine` példányt használja, így az OCR eredmények újrafeldolgozás nélkül újra felhasználhatók.

```csharp
// Export the recognised content to an ePub file
EpubWriter epubWriter = new EpubWriter();
epubWriter.Save(ocrEngine, "YOUR_DIRECTORY/receipt.epub");
```

Miért exportálunk EPUB‑ra? Az EPUB egy újra‑folyatható formátum – tökéletes mobil olvasókhoz. Az OCR szöveg kiválasztható lesz, míg az eredeti kép háttérként marad, megőrizve a beolvasott dokumentum kinézetét.

## 4. lépés – Kereshető szövegréteg hozzáadása a PDF‑hez

Most jön a rész, amely ténylegesen **kereshető PDF‑et hoz létre**. Az `AddSearchableTextLayer` engedélyezésével a PDF író egy láthatatlan szövegréteget ágyaz be, amely tükrözi az OCR kimenetet. A felhasználók kereshetnek, másolhatnak vagy kiemelhetnek szöveget, mintha natív PDF‑ről lenne szó.

```csharp
// Configure PDF writer to include a hidden searchable text layer
PdfWriter pdfWriter = new PdfWriter
{
    AddSearchableTextLayer = true   // Enables the hidden text layer for searchability
};

// Save the OCR result as a searchable PDF
pdfWriter.Save(ocrEngine, "YOUR_DIRECTORY/receipt_searchable.pdf");
```

> **Gyakori hibaforrás:** Ha elfelejtjük beállítani az `AddSearchableTextLayer`‑t, a PDF ugyanúgy néz ki, de nem tartalmaz kereshető szöveget. Mindig ellenőrizd ezt a jelzőt, ha kereshető dokumentumra van szükséged.

## 5. lépés – Teljes működő példa

Mindent összevonva, itt egy önálló konzolalkalmazás, amelyet beilleszthetsz egy új .NET projektbe és azonnal futtathatsz.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace OcrToPdfAndEpub
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialise OCR engine
            OcrEngine ocrEngine = new OcrEngine
            {
                Language = Language.English
            };

            // 2️⃣ Load the source image
            string imagePath = "YOUR_DIRECTORY/receipt.jpg";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // 3️⃣ Perform OCR
            ocrEngine.Recognize();

            // 4️⃣ Convert to EPUB (optional but handy)
            EpubWriter epubWriter = new EpubWriter();
            string epubPath = "YOUR_DIRECTORY/receipt.epub";
            epubWriter.Save(ocrEngine, epubPath);
            Console.WriteLine($"EPUB saved to {epubPath}");

            // 5️⃣ Create searchable PDF
            PdfWriter pdfWriter = new PdfWriter
            {
                AddSearchableTextLayer = true
            };
            string pdfPath = "YOUR_DIRECTORY/receipt_searchable.pdf";
            pdfWriter.Save(ocrEngine, pdfPath);
            Console.WriteLine($"Searchable PDF saved to {pdfPath}");
        }
    }
}
```

### Várható kimenet

* `receipt.epub` – egy EPUB fájl, amelyet megnyithatsz a Calibre‑ben, Apple Books‑ban vagy bármely e‑olvasóban.  
* `receipt_searchable.pdf` – egy PDF, ahol a **Ctrl + F** megnyomásával megtalálhatod az eredeti képen megjelenő bármely szót.

Ha a PDF‑et az Adobe Acrobat‑ban nyitod meg, és a **File → Properties → Description** menüpontot nézed, a **Fonts** fül alatt egy rejtett szövegfolyamot látsz, ami megerősíti, hogy a kereshető réteg jelen van.

## Gyakori kérdések és szélhelyzetek

**K: Működik ez nem‑angol nyelvekkel is?**

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}