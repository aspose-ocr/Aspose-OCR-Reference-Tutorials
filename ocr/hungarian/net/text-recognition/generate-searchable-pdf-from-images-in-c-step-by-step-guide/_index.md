---
category: general
date: 2026-02-22
description: Készítsen kereshető PDF-et és nyerjen ki szöveget a képből az Aspose
  OCR használatával. Tanulja meg, hogyan konvertáljon képet PDF-be, és hogyan állítson
  elő egyszerű szöveget egyetlen útmutatóban.
draft: false
keywords:
- generate searchable pdf
- extract text from image
- convert image to pdf
- output plain text
- convert scanned image pdf
language: hu
og_description: Készíts kereshető PDF-et beolvasott képekből az Aspose OCR-rel. Ez
  az útmutató bemutatja, hogyan lehet szöveget kinyerni a képből, egyszerű szöveget
  előállítani, és a képet PDF-re konvertálni.
og_title: Kereshető PDF létrehozása képekből – Teljes C# útmutató
tags:
- C#
- OCR
- PDF generation
- Aspose
title: Kereshető PDF létrehozása képekből C#-ban – Lépésről lépésre útmutató
url: /hu/net/text-recognition/generate-searchable-pdf-from-images-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kereshető PDF generálása képekből C#‑ban – Teljes útmutató

Valaha szükséged volt **kereshető PDF** létrehozására egy beolvasott képből, de nem tudtad, hol kezdjed? Nem vagy egyedül – a legtöbb fejlesztő ugyanebbe a falba ütközik, amikor először találkozik az OCR-rel. A jó hír? Az Aspose OCR‑rel **szöveget nyerhetsz ki a képből**, **egyszerű szöveget exportálhatsz**, és **képet PDF‑vé konvertálhatsz** néhány C#‑sorral.

Ebben az útmutatóban végigvezetünk a teljes folyamaton, a PNG‑fájl betöltésétől a kereshető PDF és egy egyszerű szövegfájl mentéséig. A végére lesz egy újrahasználható kódrészlet, amelyet bármely .NET projektbe beilleszthetsz. Felesleges szócséplés nélkül, csak a lényeg, ami a feladatot elvégzi.

## Mit tanulhatsz meg

- Hogyan állítsd be az **Aspose.OCR**‑t egy .NET konzolos alkalmazásban.  
- A **output plain text** és a **searchable PDF** módok közötti különbség.  
- Hogyan **extract text from image** és írd egy `.txt` fájlba.  
- Hogyan **convert image to PDF**, amely megőrzi az eredeti bitmapet, miközben egy rejtett szövegréteget ad hozzá.  
- Tippek nagy kötegek kezeléséhez, gyakori buktatók, és hol finomhangolhatod a beállításokat a jobb pontosság érdekében.

> **Prerequisites** – Szükséged van .NET 6+ (vagy .NET Framework 4.7+), Visual Studio 2022 (vagy bármely szerkesztő), valamint egy Aspose OCR licencre (vagy ingyenes próbaidőszakra). Más harmadik féltől származó könyvtárra nincs szükség.

![kereshető pdf generálásának példája](image-placeholder.png "Példa egy generált kereshető PDF‑re")

## 1. lépés: Aspose OCR telepítése és a motor létrehozása

Először is—add the NuGet package to your project:

```bash
dotnet add package Aspose.OCR
```

Most már elindíthatjuk az OCR motorot, és megmondhatjuk, melyik nyelvvel dolgozunk. Az angol az alapértelmezett, de a `Language` enum módosításával átválthatsz francia, spanyol stb. nyelvre.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System.IO;

class Program
{
    static void Main()
    {
        // Initialize the OCR engine for English
        OcrEngine ocrEngine = new OcrEngine { Language = Language.English };
```

**Miért fontos:** A motor tartalmazza az összes konfigurációt – nyelv, kimeneti formátum és opcionális előfeldolgozási flag-ek. Egyszer beállítva és újrahasználva elkerülhető az új példány létrehozásának terhe minden egyes fájlhoz.

## 2. lépés: Szöveg kinyerése és mentése egyszerű szövegként

Ha csak a nyers karakterekre van szükséged, állítsd a motort `OutputFormat.Text` módba. Ez azt mondja az Aspose OCR‑nek, hogy hagyja el a PDF generálást, és adjon egy stringet.

```csharp
        // Tell the engine to return plain text
        ocrEngine.OutputFormat = OutputFormat.Text;

        // Path to your source image (PNG, JPEG, BMP, etc.)
        string inputImagePath = @"YOUR_DIRECTORY/input.png";

        // Perform recognition – the result contains the extracted string
        OcrResult plainTextResult = ocrEngine.Recognize(Image.Load(inputImagePath));

        // Write the text to a .txt file
        string textOutputPath = @"YOUR_DIRECTORY/output.txt";
        File.WriteAllText(textOutputPath, plainTextResult.Text);
```

**Pro tipp:** A `plainTextResult.Text` már eltávolítja az OCR elrendezéshez tartozó sortöréseket. Ha az eredeti szóközökre van szükséged, nézd meg a `plainTextResult.TextBlocks` értéket.

### Várható eredmény

Nyisd meg az `output.txt` fájlt, és valami ilyesmit kell látnod:

```
Hello, world!
This is a sample scanned document.
```

Ez a **output plain text** része az útmutatónak – gyors, könnyű, és tökéletes a további feldolgozáshoz (pl. indexelés).

## 3. lépés: Átváltás kereshető PDF módra

Most hozzunk létre egy **searchable PDF**-et. A motor beágyazza az eredeti bitmapet, és az OCR‑által generált szöveget egy rétegként helyezi alá, így a dokumentum kereshető lesz bármely PDF‑olvasóban.

```csharp
        // Change the output format to searchable PDF
        ocrEngine.OutputFormat = OutputFormat.SearchablePdf;

        // Recognize the same image again – this time we get PDF bytes
        OcrResult pdfResult = ocrEngine.Recognize(Image.Load(inputImagePath));

        // Save the PDF bytes to a file
        string pdfOutputPath = @"YOUR_DIRECTORY/output.pdf";
        File.WriteAllBytes(pdfOutputPath, pdfResult.RawData);
    }
}
```

**Miért ismerjük fel újra:** Az OCR motor cache‑eli az utolsó képet, de a kimeneti formátum határozza meg, milyen adatot ad vissza. A formátum váltása egy új átfutást kényszerít, amely tartalmazza a rejtett szövegréteget.

### Hogyan néz ki a PDF

Nyisd meg az `output.pdf` fájlt az Adobe Readerben vagy bármely más megjelenítőben, és próbáld ki a szöveg kijelölését. Látni fogod, hogy másolni, keresni és kiemelni tudod a tartalmat – még akkor is, ha a vizuális megjelenés továbbra is az eredeti bitmap. Ez a **convert scanned image pdf** jellegzetessége.

## 4. lépés: Több fájl kezelése (opcionális)

A valós projektek ritkán dolgoznak egyetlen képpel. Az alábbi gyors ciklus minden PNG‑t feldolgoz egy mappában, és a megfelelő `.txt` és `.pdf` fájlokat hozza létre.

```csharp
        string folder = @"YOUR_DIRECTORY";
        foreach (var file in Directory.GetFiles(folder, "*.png"))
        {
            // Plain‑text extraction
            ocrEngine.OutputFormat = OutputFormat.Text;
            var txtResult = ocrEngine.Recognize(Image.Load(file));
            File.WriteAllText(Path.ChangeExtension(file, ".txt"), txtResult.Text);

            // Searchable PDF generation
            ocrEngine.OutputFormat = OutputFormat.SearchablePdf;
            var pdfResult = ocrEngine.Recognize(Image.Load(file));
            File.WriteAllBytes(Path.ChangeExtension(file, ".pdf"), pdfResult.RawData);
        }
```

**Edge case megjegyzés:** A nagy képek kimeríthetik a memóriát. Ha `OutOfMemoryException`-t kapsz, fontold meg a `Image.Resize` használatát a felismertetés előtt, vagy dolgozd fel a fájlokat kisebb kötegekben.

## 5. lépés: OCR pontosság finomhangolása

Az Aspose OCR néhány beállítást kínál, amelyeket módosíthatsz:

| Beállítás | Mit csinál | Mikor használjuk |
|-----------|------------|-------------------|
| `ocrEngine.PageSegmentationMode` | Azt szabályozza, hogyan osztja a motor a képet szövegrészekre. | Hasznos többoszlopos elrendezéseknél. |
| `ocrEngine.Deskew` | Automatikusan elforgatja a kissé ferde oldalakat. | Beolvasott dokumentumok, amelyek nem tökéletesen egyenesek. |
| `ocrEngine.RemoveNoise` | Megpróbálja eltávolítani a foltokat és a háttérzajokat. | Alacsony minőségű beolvasások vagy faxolt oldalak. |

Példa:

```csharp
ocrEngine.Deskew = true;
ocrEngine.RemoveNoise = true;
```

Ezeknek a beállításoknak a engedélyezése növelheti a feldolgozási időt, de a **extract text from image** minőségében elért javulás gyakran megéri.

## 6. lépés: A kimenet programozott ellenőrzése

Néha ellenőrizned kell, hogy a PDF valóban tartalmaz kereshető szöveget (pl. automatizált tesztekben). A legegyszerűbb ellenőrzés, hogy a PDF bájt tömb nem üres, és a `RawData` hossza meghaladja a kép méretét.

```csharp
if (pdfResult.RawData.Length > Image.Load(inputImagePath).Data.Length)
{
    Console.WriteLine("Searchable PDF generated successfully!");
}
else
{
    Console.WriteLine("Warning: PDF may not contain hidden text.");
}
```

Mélyebb validációhoz használhatsz PDF könyvtárat (például iTextSharp), hogy kinyerd a szövegfolyamot, és összehasonlítsd a `plainTextResult.Text`‑el.

## Gyakori buktatók és elkerülésük módja

- **Missing License** – Érvényes Aspose licenc hiányában a könyvtár értékelő módban fut, és vízjelet ad a PDF‑ekhez. Regisztráld a licencet korán (`License license = new License(); license.SetLicense("Aspose.OCR.lic");`).  
- **Incorrect Path** – Az abszolút útvonalak kézi kódolása a saját gépeden működik, de máshol hibát okoz. Használd a `Path.Combine`‑t az `AppDomain.CurrentDomain.BaseDirectory`‑vel a hordozhatóságért.  
- **Unsupported Image Formats** – A többkeretes GIF‑ek és TIFF‑ek speciális kezelést igényelnek (`Image.LoadMultiPage`). Ha csak az első oldalt kell, konvertáld őket PNG/JPEG formátumba.  
- **Performance Bottlenecks** – A `OcrEngine` újra‑létrehozása egy cikluson belül költséges. Tarts egyetlen példányt, és csak a `OutputFormat`‑ot változtasd, ahogy látható.

## Összefoglalás

Áttekintettük a teljes munkafolyamatot a **generate searchable PDF** létrehozásához egy beolvasott képből az Aspose OCR használatával:

1. Telepítsd a NuGet csomagot és hozd létre az `OcrEngine`‑t.  
2. Állítsd a `OutputFormat.Text`‑et **output plain text** módra, és írd egy `.txt` fájlba.  
3. Válts `OutputFormat.SearchablePdf`‑re, hogy **convert image to PDF** legyen egy láthatatlan szövegréteggel.  
4. Mentsd el a PDF bájtokat, és opcionálisan hajts végre egy mappán való ciklust kötegelt feldolgozáshoz.  
5. Finomhangold a pontosságot a deskew, zajeltávolítás és oldal szegmentálás beállításaival.  

Mindez egy kompakt, önálló programba illeszkedik, amelyet be tudsz másolni a Visual Studio‑ba.

## Mit próbálj ki legközelebb?

- **Batch processing** – UI front‑enddel (WinForms vagy WPF), hogy a felhasználók drag‑and‑drop‑olhassák a fájlokat.  
- **Language detection** – Az Aspose OCR képes automatikusan felismerni a nyelvet; próbáld ki a `ocrEngine.Language = Language.AutoDetect` beállítást.  
- **Post‑processing** – Tedd az kinyert szöveget egy kereső indexbe (ElasticSearch, Azure Cognitive Search) a gyors dokumentum‑lekérdezéshez.  
- **Alternative outputs** – Használd a `OutputFormat.Hocr`‑t HTML‑alapú OCR eredményekhez, ami hasznos webes előnézetekhez.  

Nyugodtan kísérletezz különböző kép felbontásokkal, színmódokkal és OCR beállításokkal. Minél többet játszol vele, annál jobban megérted a sebesség és pontosság közötti kompromisszumokat.

---

**Boldog kódolást!** Ha bármilyen furcsasággal találkozol, írj egy megjegyzést alább, vagy nézd meg az Aspose OCR dokumentációját a mélyebb részletekért. A következő projekted – legyen az számlázás, archiválás vagy egy kereshető tudásbázis építése – most sokkal könnyebb lesz.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}