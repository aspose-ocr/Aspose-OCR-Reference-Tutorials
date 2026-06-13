---
category: general
date: 2026-02-13
description: Kereshető PDF létrehozása képből az Aspose.OCR használatával. Tanulja
  meg, hogyan konvertáljon képet PDF-be, hogyan vonjon ki szöveget a képből, hogyan
  ágyazzon be betűtípusokat a PDF-be, és hogyan ismerje fel a szöveget PNG‑ből.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- extract text from image
- embed fonts in pdf
- recognize text from png
language: hu
og_description: Kereshető PDF létrehozása képből az Aspose.OCR-rel. Ez az útmutató
  megmutatja, hogyan konvertálhatja a képet PDF-be, ágyazhat betűtípusokat, és könnyedén
  kinyerheti a szöveget PNG-ből.
og_title: Kereshető PDF létrehozása képből – Lépésről lépésre C# oktatóanyag
tags:
- C#
- OCR
- Aspose
- PDF generation
title: Kereshető PDF létrehozása képből – Teljes C# útmutató
url: /hu/net/text-recognition/create-searchable-pdf-from-image-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Készíts kereshető PDF-et képből – Teljes C# útmutató

Valaha szükséged volt **kereshető PDF** létrehozására egy beolvasott PNG-ből, de nem tudtad, hol kezdjed? Nem vagy egyedül. Sok projektben – gondolj a számlák digitalizálására vagy a régi kézikönyvek archiválására – az, hogy egy képet PDF‑vé alakíthatsz, amelyben tényleg kereshetsz, igazi áttörés.  

Ebben az útmutatóban lépésről lépésre végigvezetünk a **kép PDF‑vé konvertálásának**, **szöveg kinyerésének a képből**, a szükséges betűtípusok beágyazásának, és végül egy teljesen kereshető PDF fájl létrehozásának. Nincsenek homályos hivatkozások, csak egy teljes, futtatható példa, amelyet ma be tudsz másolni a Visual Studio‑ba.

> **Mit kapsz:** egy C# konzolos alkalmazás, amely beolvassa a `input.png`‑t, OCR‑t futtat, betűtípusokat ágyaz be, az eredeti raszteres képet háttérként megtartja, és a `output.pdf`‑t írja ki. A végére megérted, *miért* fontos minden sor, és hogyan tudod testre szabni a saját eseteidhez.

---

## Előfeltételek

- .NET 6.0 SDK vagy újabb (a kód .NET Framework 4.7+‑vel is működik).  
- Aspose.OCR for .NET – letöltheted a NuGet‑ről (`Install-Package Aspose.OCR`).  
- Egy minta PNG kép (`input.png`) egy általad irányított mappában.  
- Alapvető ismeretek a C# konzolos projektekhez (ha még sosem hoztál létre ilyet, nyisd meg a Visual Studio‑t → **Create a new project** → **Console App** → **C#**).

> **Tipp:** Az Aspose ingyenes próbalicencet kínál; csak helyezd a `.lic` fájlt a futtatható fájl mellé, és a könyvtár vízjel nélkül fog működni.

---

## 1. lépés: Az OCR motor beállítása – Szöveg felismerése PNG‑ből

Az első dolog, amire szükségünk van, egy OCR motor, amely ténylegesen be tudja olvasni a karaktereket egy PNG fájlban. Az Aspose.OCR ezt egyszerűvé teszi.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Output;

// Initialize the OCR engine with English language support
OcrEngine ocrEngine = new OcrEngine
{
    // Primary language – you can add more if needed
    Language = OcrLanguage.English
};
```

**Miért fontos ez:**  
`Language` beállítása megmondja a motornak, milyen karakterkészletet várjon. Ha kihagyod, a motor egy általános módra vált, amely félreértheti a diakritikus karaktereket vagy számokat. Többnyelvű dokumentumok esetén megadhatsz vesszővel elválasztott listát, például `OcrLanguage.English | OcrLanguage.French`.

---

## 2. lépés: Kép betöltése és felismerése – Szöveg kinyerése a képből

Miután a motor készen áll, betápláljuk a feldolgozni kívánt PNG‑t.

```csharp
// Path to the source image; adjust as needed
string inputPath = @"YOUR_DIRECTORY/input.png";

// Perform OCR – this populates the engine's internal text representation
ocrEngine.RecognizeImage(inputPath);
```

**Mi történik a háttérben?**  
`RecognizeImage` beolvassa a bitmapet, azonosítja a szövegrészeket, és az eredményt az `ocrEngine`‑ben tárolja. Később elérheted az `ocrEngine.Text`‑et, ha csak a nyers karakterláncra van szükséged, de egy kereshető PDF‑hez hagyjuk, hogy az Aspose közvetlenül végezze a konverziót.

> **Szélsőséges eset:** Ha a PNG nagy (több mint 10 MB), memóriahiányba ütközhetsz. Ebben az esetben fontold meg a kép átméretezését először, vagy használd az `OcrEngine.RecognizeImage(Stream)`‑t az adat streaminghez.

---

## 3. lépés: PDF export beállítások konfigurálása – Betűtípusok beágyazása a PDF‑be

Egy kereshető PDF nem hasznos, ha a betűtípusok nincsenek beágyazva; a dokumentum töröttnek tűnhet olyan gépeken, ahol hiányzik a szükséges betűkészlet. Az Aspose egy egyszerű opcióobjektummal teszi lehetővé ennek beállítását.

```csharp
// Define how the searchable PDF should be built
SearchablePdfOptions pdfOptions = new SearchablePdfOptions
{
    // Guarantees the PDF renders correctly everywhere
    EmbedFonts = true,

    // Keeps the original raster image as a visual background
    KeepOriginalImage = true
};
```

**Miért ágyazzuk be a betűtípusokat?**  
Ha az `EmbedFonts` `true`, a PDF a betűtípus adatokat a fájlba ágyazza. Ez biztosítja, hogy bármely megjelenítő – Chrome, Adobe Reader vagy mobilalkalmazás – pontosan a tervezett módon jelenítse meg a szöveget, még ha a célrendszeren hiányzik is a betűtípus.

**Mikor állítanád a `KeepOriginalImage` értékét `false`‑ra?**  
Ha csak a kinyert szövegre van szükséged, és kisebb fájlt szeretnél, ennek kikapcsolása eltávolítja a háttérképet, így egy „tiszta”, csak szöveget tartalmazó PDF-et kapsz.

---

## 4. lépés: Exportálás kereshető PDF‑be – Kép konvertálása PDF‑vé

Miután az OCR eredmények és a PDF beállítások készen vannak, az utolsó lépés egy egyetlen soros kód, amely a kereshető PDF‑et a lemezre írja.

```csharp
// Destination path for the generated PDF
string outputPath = @"YOUR_DIRECTORY/output.pdf";

// Export the OCR result as a searchable PDF
ocrEngine.ExportToSearchablePdf(outputPath, pdfOptions);

// Let the user know we’re done
Console.WriteLine("Searchable PDF created.");
```

**Mit fogsz látni:**  
`output.pdf` megnyitása bármely megjelenítőben lehetővé teszi a szöveg kijelölését, másolását, és akár keresést (`Ctrl + F`) is futtathatsz, hogy megtaláld azokat a szavakat, amelyek eredetileg csak pixelekként voltak jelen a PNG‑ben.

---

## Teljes működő példa

Az alábbiakban a teljes program látható, amelyet azonnal lefordíthatsz és futtathatsz. Cseréld le a `YOUR_DIRECTORY`‑t arra a mappára, amely tartalmazza a `input.png`‑t.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Output;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine – set language to English
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.English
        };

        // 2️⃣ Recognize text from the PNG image
        string inputPath = @"YOUR_DIRECTORY/input.png";
        ocrEngine.RecognizeImage(inputPath);

        // 3️⃣ Prepare PDF options – embed fonts & keep raster background
        SearchablePdfOptions pdfOptions = new SearchablePdfOptions
        {
            EmbedFonts = true,
            KeepOriginalImage = true
        };

        // 4️⃣ Export to a searchable PDF file
        string outputPath = @"YOUR_DIRECTORY/output.pdf";
        ocrEngine.ExportToSearchablePdf(outputPath, pdfOptions);

        // 5️⃣ Notify the user
        Console.WriteLine("Searchable PDF created.");
    }
}
```

**Várható kimenet a konzolon:**  

```
Searchable PDF created.
```

Nyisd meg az `output.pdf`‑t, és próbálj meg keresni egy olyan szót, amely biztosan szerepel az `input.png`‑ben. Ha kiemeli, sikeresen **kereshető PDF-et hoztál létre** a képből.

---

## Gyakori kérdések és profi tippek

### „Feldolgozhatok több képet egy futtatás során?”

Természetesen. Csomagold a felismerési és exportálási logikát egy ciklusba, például a `Directory.GetFiles(..., "*.png")` használatával. Ne feledd, hogy minden PDF‑nek egyedi nevet adj, pl. `Path.GetFileNameWithoutExtension(img) + ".pdf"`.

### „Mi van, ha a dokumentum angol és spanyol szöveget is tartalmaz?”

Állítsd be a nyelv tulajdonságot egy kombinált zászlóra:

```csharp
ocrEngine.Language = OcrLanguage.English | OcrLanguage.Spanish;
```

Az Aspose ekkor megpróbálja felismerni a karaktereket mindkét ábécéből.

### „A PDF fájl hatalmas – hogyan tudom csökkenteni a méretét?”

Két gyors trükk:

1. Állítsd be a `pdfOptions.KeepOriginalImage = false` értéket, hogy eltávolítsd a raszteres háttérképet.  
2. Használd a `pdfOptions.ImageCompression = ImageCompression.Jpeg;` beállítást (ehhez hozzá kell adni a tulajdonságot), hogy tömörítsd a beágyazott képet.

### „Szükség van licencre a termelésben való használathoz?”

A próba jól működik teszteléshez, de kereskedelmi bevetésnél licencet kell vásárolni és a program elején regisztrálni:

```csharp
Aspose.OCR.License license = new Aspose.OCR.License();
license.SetLicense("Aspose.OCR.lic");
```

---

## A megoldás bővítése

Most, hogy tudod, hogyan **kereshető PDF-et készíts**, lehet, hogy szeretnél:

- **Vízjel hozzáadása** – használd az `PdfDocument`‑et az Aspose.PDF‑ből, hogy szöveget helyezz a képre az OCR után.  
- **Kötegelt PDF feldolgozás** – több kereshető PDF-et egyesíts egybe a `PdfFileEditor` használatával.  
- **Integráció Azure Blob Storage‑szal** – olvasd/írd a képet és a PDF adatfolyamokat közvetlenül a felhőből, ezzel kiküszöbölve a helyi fájl I/O‑t.

Ezek a kiterjesztések mind ugyanazt a mintát követik: szerezz OCR eredményt, konfiguráld a következő könyvtárat, és láncold össze a műveleteket.

---

## Összegzés

Most megtanultad, hogyan **készíts kereshető PDF-et** egy PNG képből az Aspose.OCR használatával C#‑ban. Az OCR motor inicializálásával, a szöveg felismerésével, a `SearchablePdfOptions` **betűtípusok PDF‑be beágyazására** való konfigurálásával és az exportálással egy olyan fájlt kapsz, amely vizuálisan megegyezik az eredetivel, és teljesen kereshető.

Innen nyugodtan kísérletezhetsz kötegelt konverziókkal, különböző nyelvekkel vagy szorosabb tömörítéssel – bármi, ami a munkafolyamatodhoz illik. Ha problémákba ütközöl, az Aspose fórumok és API dokumentációk jó források, de a fenti alaplépések lefedik a tipikus esetek 90 %-át.

Boldog kódolást, és legyenek a PDF-jeid mindig kereshetők!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}