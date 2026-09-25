---
category: general
date: 2026-02-11
description: Készíts kereshető PDF-et arab képből C#-ban. Tanulja meg, hogyan konvertálja
  a képet PDF-be, hogyan vonja ki az arab szöveget, és hogyan adjon hozzá rejtett
  szöveget az Aspose OCR használatával.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- extract arabic text
- pdf with hidden text
- ocr arabic image
language: hu
og_description: Készíts kereshető PDF-et arab képből az Aspose OCR használatával C#-ban.
  Kövesd ezt az útmutatót a kép PDF-re konvertálásához, az arab szöveg kinyeréséhez
  és a rejtett szöveg beágyazásához.
og_title: Kereshető PDF létrehozása arab képből – Lépésről lépésre
tags:
- Aspose
- OCR
- PDF
- C#
- Arabic
title: Kereshető PDF létrehozása arab képből – Teljes útmutató
url: /hu/net/text-recognition/create-searchable-pdf-from-arabic-image-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kereshető PDF létrehozása arab képből – Teljes útmutató

Valaha szükséged volt **kereshető PDF** létrehozására egy beolvasott arab számláról, de nem tudtad, hogyan tartsd meg az eredeti megjelenést, miközben a szöveget kiválaszthatóvá teszed? Nem vagy egyedül. Sok dokumentum‑automatizálási projektben a kihívás nem csak a kép PDF‑re konvertálása, hanem a vizuális elrendezés megőrzése és egy rejtett szövegréteg hozzáadása, amelyet a keresőmotorok indexelni tudnak.

Ebben az útmutatóban végigvezetünk a teljes folyamaton: **kép konvertálása PDF‑re**, **arab szöveg kinyerése** az Aspose OCR‑rel, és végül a szöveg beágyazása **rejtett szöveggel rendelkező PDF‑be**, így a létrehozott fájl teljesen kereshető lesz. A végére egy kész C# kódrészletet kapsz, amelyet bármely .NET megoldásba beilleszthetsz. Nincs külső szolgáltatás, csak az általad már használt Aspose könyvtárak.

## Amire szükséged lesz

- .NET 6 vagy újabb (a kód .NET Core‑ral is működik)  
- **Aspose.OCR** és **Aspose.Pdf** NuGet csomagok (a legújabb verziók 2026 februárjában)  
- Egy arab nyelvű képfájl (például `arabic_invoice.jpg`), amelyet kereshető PDF‑vé szeretnél alakítani  
- Egy kis C# ismeret – a koncepciók egyszerűek, de elmagyarázzuk a sorok mögötti „miértet”.

> **Pro tipp:** Ha még nem adtad hozzá a NuGet csomagokat, futtasd a projekt mappádból  
> `dotnet add package Aspose.OCR` és  
> `dotnet add package Aspose.Pdf`.

Most, hogy a feltételek rendben vannak, merüljünk el a lépésről‑lépésre megvalósításban.

## 1. lépés – Az OCR motor beállítása arab szöveghez

Az első dolog, amit tennünk kell, hogy az Aspose OCR‑t úgy konfiguráljuk, hogy felismerje az arab karaktereket. Az arab jobbról balra íródó írásrendszer, ezért meg kell mondanunk a motornak, melyik nyelvet töltse be, és engedélyezni kell az automatikus erőforrásletöltést, ha a nyelvi adatok még nincsenek a gépen.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// Configure OCR for Arabic and let Aspose fetch the language pack if needed
var ocrEngine = new OcrEngine
{
    Language = OcrLanguage.Arabic,
    AutomaticResourceDownload = true
};
```

**Miért fontos:**  
Ha kihagyod a `Language = OcrLanguage.Arabic` beállítást, a motor alapértelmezés szerint angolt használ, és torz karakterekkel fogsz végezni. Az `AutomaticResourceDownload` engedélyezése megkímél a nyelvi fájlok kézi elhelyezésétől a szerveren.

## 2. lépés – A forráskép betöltése

Ezután betöltjük a képet, amely az arab szöveget tartalmazza. Az `Image.FromFile` használata biztosítja, hogy a kép egy GDI+ `Image` objektumba legyen beolvasva, amit az Aspose OCR elvár.

```csharp
using System.Drawing;          // For Image
using System.IO;                // For MemoryStream

// Replace with the actual path to your Arabic invoice
string imagePath = @"YOUR_DIRECTORY/arabic_invoice.jpg";

using (var inputImage = Image.FromFile(imagePath))
{
    // The rest of the workflow lives inside this using block
```

**Szélsőséges eset:** Ha a kép hatalmas (például egy beolvasott A3 oldal), érdemes előbb lekicsinyíteni a teljesítmény javítása érdekében. Az OCR motor képes nagy fájlok kezelésére, de a memóriahasználat gyorsan megugrik.

## 3. lépés – Arab szöveg felismerése és az eredmény rögzítése

Most ténylegesen futtatjuk az OCR‑t. A `Recognize` metódus egy `OcrResult` objektumot ad vissza, amely a felismert szöveget, a megbízhatósági pontszámokat és a keretmezőket tartalmazza (ha valaha is szükséged lenne rájuk fejlett elrendezés‑elemzéshez).

```csharp
    // Perform OCR on the loaded image
    OcrResult ocrResult = ocrEngine.Recognize(inputImage);
    string extractedText = ocrResult.Text;

    // Quick sanity check: print the first 200 characters to the console
    Console.WriteLine("Extracted Arabic text (preview):");
    Console.WriteLine(extractedText.Substring(0, Math.Min(200, extractedText.Length)));
```

**Miért tartsuk meg az előnézetet?**  
A kinyert szöveg egy részletének megtekintése segít ellenőrizni, hogy a nyelvi csomag helyesen betöltődött, mielőtt időt pazarolnál a PDF generálására.

## 4. lépés – Új PDF dokumentum létrehozása és üres oldal hozzáadása

A szöveg birtokában elkezdhetjük felépíteni a PDF‑et. Az Aspose PDF egy `Document` objektumot biztosít, amely a teljes fájlt képviseli. Egy oldal hozzáadása egy vásznat ad, ahová az eredeti képet és a rejtett szövegréteget is elhelyezhetjük.

```csharp
    // Initialize a new PDF document
    var pdfDocument = new Aspose.Pdf.Document();

    // Add a blank page – this will become the background for our image
    var pdfPage = pdfDocument.Pages.Add();
```

**Megjegyzés:** Több oldalt is hozzáadhatsz, ha többoldalas TIFF‑et vagy PDF‑et dolgozol fel, de egyetlen kép esetén egy oldal elegendő.

## 5. lépés – Az eredeti kép beillesztése háttérelemként

Azt szeretnénk, hogy a végső PDF pontosan úgy nézzen ki, mint a beolvasott számla, ezért a képet látható háttérként ágyazzuk be. Az Aspose PDF `Image` osztálya egy stream‑et vár, ezért a fájlt egy `MemoryStream`‑be olvassuk.

```csharp
    // Load the same image bytes for the PDF background
    var backgroundImage = new Aspose.Pdf.Image
    {
        ImageStream = new MemoryStream(File.ReadAllBytes(imagePath))
    };

    // Add the image to the page's paragraph collection
    pdfPage.Paragraphs.Add(backgroundImage);
```

**Miért használjunk háttérképet?**  
A kép közvetlen elhelyezése az oldalon megőrzi az eredeti elrendezést, színeket és minden bélyeget vagy logót, amelyet az OCR motor egyébként figyelmen kívül hagyna.

## 6. lépés – OCR szöveg hozzáadása rejtett rétegként

A **kereshető PDF** titkos összetevője egy rejtett szövegréteg, amely a kép fölött helyezkedik el. A betűméret `0`‑ra állításával a szöveget láthatatlanná tesszük az emberi szem számára, miközben továbbra is kiválasztható és kereshető marad.

```csharp
    // Create a TextFragment with the extracted Arabic text
    var searchableText = new Aspose.Pdf.Text.TextFragment(extractedText)
    {
        // Hide the visible text; only the text layer remains searchable
        TextState = { FontSize = 0 }
    };

    // Add the hidden text fragment to the same page
    pdfPage.Paragraphs.Add(searchableText);
```

**Fontos részlet:**  
Ha a rejtett szöveget pontosan a képpel szeretnéd összehangolni (például ha az OCR koordinátákat ad vissza), használhatod a `TextFragmentAbsorber`‑t, és manuálisan pozícionálhatod az egyes fragmentumokat. A legtöbb számla esetén egy egyszerű teljes oldalra kiterjedő átfedés is megfelelő.

## 7. lépés – A kereshető PDF mentése

Végül a PDF‑et leírjuk a lemezre. A kimeneti fájl tartalmazni fogja a vizuális képet és a rejtett arab szöveget is, így teljesen kereshető lesz az Adobe Readerben, a Google Drive‑ban vagy bármely OCR‑t támogató megjelenítőben.

```csharp
    // Define the output path
    string outputPath = @"YOUR_DIRECTORY/arabic_invoice_searchable.pdf";

    // Save the document
    pdfDocument.Save(outputPath);

    Console.WriteLine($"Searchable PDF created at: {outputPath}");
}
```

### Teljes működő példa

Az összes részt összeállítva, itt a teljes, azonnal futtatható program:

```csharp
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // 1️⃣ Configure OCR for Arabic
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.Arabic,
            AutomaticResourceDownload = true
        };

        // 2️⃣ Load the source image
        string imagePath = @"YOUR_DIRECTORY/arabic_invoice.jpg";
        using (var inputImage = Image.FromFile(imagePath))
        {
            // 3️⃣ Run OCR and get the text
            OcrResult ocrResult = ocrEngine.Recognize(inputImage);
            string extractedText = ocrResult.Text;

            // Optional preview
            Console.WriteLine("Extracted Arabic text (preview):");
            Console.WriteLine(extractedText.Substring(0, Math.Min(200, extractedText.Length)));

            // 4️⃣ Create PDF document
            var pdfDocument = new Document();
            var pdfPage = pdfDocument.Pages.Add();

            // 5️⃣ Add original image as background
            var backgroundImage = new Aspose.Pdf.Image
            {
                ImageStream = new MemoryStream(File.ReadAllBytes(imagePath))
            };
            pdfPage.Paragraphs.Add(backgroundImage);

            // 6️⃣ Add hidden searchable text
            var searchableText = new TextFragment(extractedText)
            {
                TextState = { FontSize = 0 }
            };
            pdfPage.Paragraphs.Add(searchableText);

            // 7️⃣ Save the searchable PDF
            string outputPath = @"YOUR_DIRECTORY/arabic_invoice_searchable.pdf";
            pdfDocument.Save(outputPath);
            Console.WriteLine($"Searchable PDF created at: {outputPath}");
        }
    }
}
```

**Várt eredmény:** Nyisd meg a generált `arabic_invoice_searchable.pdf` fájlt bármely PDF‑megtekintőben, nyomd meg a **Ctrl + F** kombinációt, és írj be egy arab szót, amely az eredeti számlán szerepel. A megtekintőnek meg kell találnia a szót, még akkor is, ha nem látsz semmilyen szövegréteget.

## Gyakori kérdések és buktatók

- **Működik más nyelvekkel is?**  
  Természetesen. Csak módosítsd a `Language = OcrLanguage.YourLanguage` beállítást, és győződj meg róla, hogy a nyelvi csomag elérhető. A folyamat többi része változatlan.

- **Mi van, ha az OCR megbízhatósága alacsony?**  
  Ellenőrizheted az `ocrResult.Confidence` értékét (0 és 1 között). Ha egy küszöbérték alá esik (például 0,75), fontold meg a kép előfeldolgozását – kiegyenesítés, kontraszt növelés vagy szürkeárnyalatos konvertálás – mielőtt a motorba adod.

- **Hozzáadhatok több képet egy PDF‑hez?**  
  Igen. Iterálj egy képfájl‑útvonalak gyűjteményén, minden egyeshez adj egy új oldalt, és ismételd meg az 5‑6. lépéseket. Ne felejtsd el a `using` blokkot minden képhez, hogy felszabadítsd a GDI erőforrásokat.

- **A rejtett szöveg valóban láthatatlan?**  
  A `FontSize = 0` beállítás a legtöbb megjelenítőben láthatatlanná teszi a szöveget. Ha egy megjelenítő mégis egy halvány karaktert mutat, beállíthatod a szövegszínt teljesen átlátszóra is (`TextState.FillColor = Color.Transparent`).

## Következő lépések

Most, hogy tudod, hogyan **hozz létre kereshető PDF‑et** egy arab képből, érdemes lehet tovább kutatni:

- **Kötegelt feldolgozás** – olvasd be egy mappa összes képét, és minden fájlhoz generálj egy kereshető PDF‑et.  
- **OCR koordináták hozzáadása** – használd az `OcrResult.Regions`‑t, hogy minden szövegfragmentumot pontosan oda helyezd, ahol megjelenik, ez javítja a keresési pontosságot összetett elrendezéseknél.  
- **PDF titkosítása** – az Aspose PDF lehetővé teszi jelszavak vagy digitális aláírások hozzáadását, ha extra biztonságra van szükség.  
- **Integráció Azure Blob Storage‑szal** – tárold a generált PDF‑eket közvetlenül a felhőben a további munkafolyamatokhoz.  

Ezek a témák természetesen magukban foglalják a másodlagos kulcsszavakat **convert image to pdf**, **extract

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}