---
category: general
date: 2026-05-21
description: Kép OCR végrehajtása C#-ban. Tanulja meg, hogyan töltsön be képet OCR-hez,
  hogyan nyerjen ki szöveget PNG-ből, és hogyan ismerje fel a szöveget a képen egy
  kis kódrészlettel.
draft: false
keywords:
- perform OCR on image
- extract text from PNG
- recognize text from image
- load image for OCR
language: hu
og_description: Végezzen gyors OCR-t képen C#-ban. Ez az útmutató bemutatja, hogyan
  töltsön be képet OCR-hez, hogyan nyerjen ki szöveget PNG-ből, és hogyan ismerje
  fel a szöveget a képen elrendezés‑tudatos HTML kimenettel.
og_title: Kép OCR-olása C#-al – Teljes programozási útmutató
schemas:
- author: Aspose
  dateModified: '2026-05-21'
  description: Perform OCR on image using C#. Learn how to load image for OCR, extract
    text from PNG, and recognize text from image with a tiny code sample.
  headline: Perform OCR on Image with C# – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Perform OCR on image using C#. Learn how to load image for OCR, extract
    text from PNG, and recognize text from image with a tiny code sample.
  name: Perform OCR on Image with C# – Complete Step‑by‑Step Guide
  steps:
  - name: Load Image for OCR
    text: The line `engine.Image = ImageStream.FromFile("YOUR_DIRECTORY/form.png");`
      is where we **load image for OCR**. The `ImageStream` helper abstracts away
      file‑format details, so you can feed JPEG, BMP, or TIFF without changing code.
  - name: Extract Text from PNG
    text: 'Once `engine.Recognize()` finishes, the OCR engine holds the recognized
      text internally. You can pull it out as a string if you only need raw text:'
  - name: Recognize Text from Image
    text: 'The `Recognize()` call does the heavy lifting. Under the hood the engine:'
  - name: Handling Layout‑Aware HTML Output
    text: 'Most developers stop at plain text, but the `HtmlSaveOptions` we used let
      you **perform OCR on image** and keep the visual structure intact. Two flags
      matter:'
  - name: Scaling to Multiple Files
    text: 'If you need to **perform OCR on image** files in a folder, wrap the core
      logic in a simple loop:'
  type: HowTo
tags:
- OCR
- C#
- Image Processing
- Aspose.OCR
title: OCR végrehajtása képen C#‑val – Teljes lépésről‑lépésre útmutató
url: /hu/net/text-recognition/perform-ocr-on-image-with-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kép OCR végrehajtása C#‑ban – Teljes lépésről‑lépésre útmutató

Gondolkodtál már azon, hogyan **perform OCR on image** fájlokon dolgozhatsz anélkül, hogy nehézkes GUI‑kat kellene kezelned? Nem vagy egyedül. Akár nyugtákat digitalizálsz, adatokat nyersz be beolvasott űrlapokból, vagy egyszerűen csak egy PNG‑t szeretnél kereshető szöveggé alakítani, néhány C#‑sorral megoldható.

Ebben az útmutatóban végigvezetünk a kép OCR‑hoz való betöltésén, a szöveg felismerésén a képről, és végül a PNG‑ből történő szöveg kinyerésén tiszta HTML‑ként. A végére egy azonnal futtatható konzolos alkalmazásod lesz, amely **performs OCR on image** fájlokon, és megőrzi az eredeti elrendezést.

## Mit fogsz építeni

- Egy minimális konzolprogram, amely PNG‑t (vagy bármely támogatott képet) olvas be  
- OCR motor használata a **recognize text from image** feladatra  
- Az eredményt elrendezés‑tudatos HTML‑ként menti, beágyazva az eredeti képet  
- Bemutatja, hogyan **load image for OCR**, **extract text from PNG**, és kezelje a gyakori széljegyeket  

> **Prerequisites**  
> - .NET 6.0 SDK vagy későbbi (célzhatsz .NET Framework 4.7+ is)  
> - Egy NuGet‑kompatibilis OCR könyvtár – a példában *Aspose.OCR* van, de bármely hasonló API‑val rendelkező könyvtár működik  
> - Alap C# ismeretek (semmi bonyolult)  

Got those? Great—let’s dive in.

## OCR végrehajtása képen – Teljes kódfutás

Az alábbi **complete, runnable** program. Másold be egy új konzolos projektbe (`dotnet new console`), és nyomd meg a **F5**‑öt.

```csharp
using System;
using Aspose.OCR;               // OCR engine namespace
using Aspose.OCR.Models;        // Save options namespace
using Aspose.OCR.ImageProcessing; // Image loading helpers

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Create an OCR engine and set the language
            // -------------------------------------------------
            var engine = new OcrEngine
            {
                Language = OcrLanguage.English   // You can change to French, German, etc.
            };

            // -------------------------------------------------
            // Step 2: Load the image for OCR
            // -------------------------------------------------
            // Replace the path with your actual PNG/JPEG/TIFF file.
            engine.Image = ImageStream.FromFile("YOUR_DIRECTORY/form.png");

            // -------------------------------------------------
            // Step 3: Perform OCR recognition
            // -------------------------------------------------
            engine.Recognize();

            // -------------------------------------------------
            // Step 4: Configure HTML save options – keep layout
            // -------------------------------------------------
            var htmlOptions = new HtmlSaveOptions
            {
                PreserveLayout = true,   // Keep columns, tables, and spacing
                EmbedImages = true       // Embed the original PNG inside the HTML
            };

            // -------------------------------------------------
            // Step 5: Save the recognized content as layout‑aware HTML
            // -------------------------------------------------
            engine.Save("YOUR_DIRECTORY/form.html", htmlOptions);

            Console.WriteLine("HTML with layout saved.");
        }
    }
}
```

> **Várható kimenet**  
> ```
> HTML with layout saved.
> ```  
> A futtatás után a `form.html` fájlt a PNG mellett találod. Nyisd meg böngészőben, és ugyanazt az elrendezést látod, csak most a szöveg kijelölhető és kereshető.

### Kép betöltése OCR‑hez

A `engine.Image = ImageStream.FromFile("YOUR_DIRECTORY/form.png");` sorban **load image for OCR** történik. Az `ImageStream` segítő elrejti a fájlformátum részleteit, így JPEG‑et, BMP‑t vagy TIFF‑et is betáplálhatsz kód módosítása nélkül.

**Miért ne csak egy `Bitmap`-et adjunk át?**  
Mert sok OCR SDK egy olyan streamet vár, amely DPI metaadatot is tartalmaz. A könyvtár beépített betöltőjének használata garantálja, hogy a motor pontosan úgy látja a képet, ahogy a képernyőn megjelenik, ami javítja a pontosságot.

#### Pro tip  
Ha egy fájlkészletet dolgozol fel, tedd a betöltési lépést egy `try/catch`‑be, és naplózd a `FileNotFoundException`‑t. Ez megakadályozza, hogy az egész köteg összeomoljon egy hiányzó fájl miatt.

### Szöveg kinyerése PNG‑ből

Miután az `engine.Recognize()` befejeződik, az OCR motor belsőleg tárolja a felismert szöveget. Ha csak nyers szövegre van szükséged, kinyerheted stringként:

```csharp
string plainText = engine.Text;   // Returns the whole document as plain text
Console.WriteLine(plainText);
```

Ez a leggyorsabb mód a **extract text from PNG** feladatra, ha nem érdekel az elrendezés. A legtöbb adatbevitelhez a sima szöveg elegendő – csak ne felejtsd el levágni a sortöréseket, ha CSV‑be szeretnéd importálni.

### Szöveg felismerése képről

A `Recognize()` hívás végzi a nehéz munkát. A motor a háttérben:

1. Normalizálja a képet (kiegyenesíti, zajt távolít el)  
2. Sorokra és szavakra bontja  
3. Egy milliók glyphjeire tanított neurális hálózat osztályozót futtat  

Mivel `Language = OcrLanguage.English`‑t állítottuk be, a motor angol‑specifikus szótárakat használ, ami drámaian csökkenti a hamis pozitív találatokat. Ha többnyelvű támogatásra van szükség, egyszerűen adj át egy nyelv tömböt:

```csharp
engine.Language = OcrLanguage.English | OcrLanguage.Spanish;
```

### Elrendezés‑tudatos HTML kimenet kezelése

A legtöbb fejlesztő csak a sima szövegnél áll meg, de a `HtmlSaveOptions`, amelyet használtunk, lehetővé teszi, hogy **perform OCR on image** és megőrizze a vizuális struktúrát. Két beállítás számít:

- `PreserveLayout = true` – megőrzi az oszlopokat, táblázatokat és a távolságokat.  
- `EmbedImages = true` – beilleszti az eredeti PNG‑t Base64‑kódolt `<img>` elemként, így a HTML önálló.

Ha könnyebb fájlt szeretnél, állítsd `EmbedImages = false`‑ra, és a HTML a lemezen lévő eredeti PNG‑re hivatkozik.

#### Széljegy: Nagy fájlok

5 MB-nál nagyobb képek esetén a beágyazás felrobbanthatja a HTML méretét. Ilyenkor válts külső kép hivatkozásokra, és fontold meg a PNG előzetes tömörítését az `ImageProcessor.Compress`‑szel.

## Gyakori buktatók és Pro tippek

| Tünet | Valószínű ok | Javítás |
|--------|--------------|-----|
| Torz karakterek | Rossz nyelv beállítása vagy hiányzó nyelvi csomag | Telepítsd a megfelelő nyelvi adatfájlokat, és állítsd be helyesen az `engine.Language`‑t |
| Nincs szöveg a kimenetben | A kép túl sötét vagy alacsony felbontású | Előfeldolgozás: `engine.Image = ImageProcessor.AdjustContrast(engine.Image, 1.2)` |
| Az elrendezés megtört a HTML‑ben | `PreserveLayout` alapértelmezett `false` értéken maradt | Állítsd `PreserveLayout = true`‑ra a `HtmlSaveOptions`‑ban |
| Lassú feldolgozás sok oldalon | A motor minden fájlnál újra inicializálódik | Használd ugyanazt az `OcrEngine` példányt, és csak a `engine.Image`‑t változtasd minden ciklusban |

### Skálázás több fájlra

Ha egy mappában lévő **perform OCR on image** fájlokon kell dolgozni, csomagold a fő logikát egy egyszerű ciklusba:

```csharp
foreach (var file in Directory.GetFiles("YOUR_DIRECTORY", "*.png"))
{
    engine.Image = ImageStream.FromFile(file);
    engine.Recognize();
    var htmlPath = Path.ChangeExtension(file, ".html");
    engine.Save(htmlPath, htmlOptions);
    Console.WriteLine($"Processed {Path.GetFileName(file)}");
}
```

Vedd észre, hogy a **load image for OCR** a cikluson belül történik, de ugyanazt az `engine` és `htmlOptions` objektumot használjuk. Ez csökkenti a memóriaforgalmat és felgyorsítja a kötegelt feladatokat.

## Tovább lépés: Exportálás PDF‑be vagy DOCX‑be

Ugyanaz a `engine` más formátumokba is menthet:

```csharp
engine.Save("output.pdf", new PdfSaveOptions { PreserveLayout = true });
engine.Save("output.docx", new WordSaveOptions { PreserveLayout = true });
```

Ha a downstream rendszer kereshető PDF‑eket vár, ez egy egy‑soros módosítás – nincs szükség külön konverziós csővezeték írására.

## Összegzés

Most bemutattuk, hogyan **perform OCR on image** fájlokkal C#‑ban, a kép betöltésétől a **extract text from PNG**-ig, majd végül a **recognize text from image** egy elrendezés‑tudatos HTML fájlba. A teljes példa futtatható, és most már érted, miért fontos minden lépés, hogyan hangolhatod különböző nyelvekhez, és milyen buktatókra kell figyelni.

Következő lépésként próbáld ki az angol nyelv helyettesítését egy másik nyelvvel, kísérletezz a `PreserveLayout = false` beállítással, hogy könnyebb HTML‑t kapj, vagy irányítsd a sima szöveg kimenetet egy adatbázisba kereshető archívumokhoz. A lehetőségek határtalanok, ha egy erős OCR motort pár C#‑sorral kombinálsz.

Van kérdésed a többoldalas TIFF‑ek kezelésével kapcsolatban, vagy szeretnéd tudni, hogyan integráld ezt egy ASP.NET Core API‑ba? Hagyj egy megjegyzést alább, és jó kódolást!

## Kapcsolódó útmutatók

- [Kép szövegének kinyerése C#‑ban nyelvválasztással az Aspose.OCR használatával](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Hogyan nyerjünk ki szöveget képről téglalapok előkészítésével az OCR‑ban](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Kép szövegének kinyerése – sor felismerése az Aspose.OCR‑rel](/ocr/english/net/image-and-drawing-recognition/recognize-line/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}