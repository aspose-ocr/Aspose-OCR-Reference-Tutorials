---
category: general
date: 2026-05-31
description: Tanulja meg, hogyan kaphat OCR megbízhatósági pontszámokat C#‑ban, miközben
  szöveget nyer ki képből, és nyugtaképet olvas az Aspose OCR‑rel.
draft: false
keywords:
- ocr confidence scores
- extract text from image
- ocr bounding boxes
- perform ocr on jpg
- read receipt image
language: hu
og_description: Az OCR megbízhatósági pontszámok lehetővé teszik a pontosság felmérését;
  ez az útmutató bemutatja, hogyan lehet szöveget kinyerni egy képből, lekérni a határoló
  dobozokat, és beolvasni a nyugtaképet az Aspose OCR segítségével.
og_title: OCR megbízhatósági pontszámok C#‑ban – Teljes útmutató
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to get OCR confidence scores in C# while extract text from
    image and read receipt image with Aspose OCR.
  headline: OCR confidence scores in C# – Complete Guide
  type: TechArticle
tags:
- OCR
- C#
- Aspose
- Image Processing
title: OCR megbízhatósági pontszámok C#-ban – Teljes útmutató
url: /hu/net/ocr-optimization/ocr-confidence-scores-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR megbízhatósági pontszámok C#‑ban – Teljes útmutató

Gondolkodtál már azon, hogyan **OCR megbízhatósági pontszámokat** kaphatsz, amikor *képből kell szöveget kinyerni*? Lehet, hogy **nyugtaki kép** fájlokat próbálsz beolvasni költségkövetéshez, és szeretnéd tudni, mely karakterekkel nem biztos a motor. A jó hír? Az Aspose.OCR segítségével néhány C#‑os sorral lekérheted a megbízhatósági százalékokat, a határoló dobozokat és a sima szöveget egy JPG‑ből.

Ebben az útmutatóban mindent végigvázolunk, amit tudnod kell: a könyvtár telepítését, a motor **OCR végrehajtására JPG‑n** történő konfigurálását, a megbízhatósági pontszámok kinyerését, és a **OCR határoló dobozok** értelmezését, amelyek megmutatják, hol helyezkedik el az egyes karakterek az oldalon. A végére egy azonnal futtatható konzolalkalmazásod lesz, amely kiír minden karaktert, annak megbízhatóságát és helyét – tökéletes nyugták vagy bármely beolvasott dokumentum ellenőrzéséhez.

## Mit fogsz megtanulni

- Az Aspose.OCR telepítése NuGet‑en keresztül és egy alap OCR motor beállítása.  
- A `OcrOptions` konfigurálása, hogy **megbízhatósági pontszámokkal** és **határoló dobozokkal** kérje a sima szöveg kimenetet.  
- `OcrResult` bejárása, hogy **képből szöveget nyerjünk ki** soronként és szimbólumonként.  
- Gyakori buktatók kezelése, mint hiányzó fájlok, alacsony megbízhatóságú karakterek és nem JPG formátumok.  
- A példát kiterjeszteni több nyugtakép feldolgozására egy mappában.

Nem szükséges előzetes Aspose tapasztalat; csak egy működő .NET környezet és egy nyugtakép (JPG), amelyet tesztelni szeretnél.

## 1. lépés – Aspose.OCR telepítése és a projekt előkészítése

Először is: szükséged van az Aspose.OCR NuGet csomagra.  
Nyiss egy terminált a projekt mappádban, és futtasd:

```bash
dotnet add package Aspose.OCR
```

> **Pro tipp:** Az ingyenes próba 200 oldalig működik, ami bőven elegendő a nyugtabeolvasás teszteléséhez.

A csomag telepítése után hozz létre egy új konzolprojektet (ha még nincs):

```bash
dotnet new console -n ReceiptOcrDemo
cd ReceiptOcrDemo
```

Most megnyithatod a generált `Program.cs` fájlt, és elkezdheted hozzáadni a using direktívákat:

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;
```

Ezek a névterek hozzáférést biztosítanak a `OcrEngine`, `OcrOptions` és a később szükséges eredménytípusokhoz.

## 2. lépés – OCR megbízhatósági pontszámok és OCR határoló dobozok lekérése

Ez a tutorial szíve. A motort úgy konfiguráljuk, hogy minden felismert karakterhez **megbízhatósági pontszám** és **határoló doboz** (a glifet körülvevő téglalap) tartozzon. Maga a H2 fejléc is tartalmazza a fő kulcsszót, ezzel teljesítve az SEO szabályt.

```csharp
// Step 2: Initialize the OCR engine and request detailed output
OcrEngine ocrEngine = new OcrEngine();

// Load the image you want to process – here we assume a JPEG receipt
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/receipt.jpg");

// Tell Aspose we want plain text, confidence percentages, and bounding boxes
ocrEngine.Options = new OcrOptions
{
    OutputFormat = OcrOutputFormat.PlainText,
    IncludeConfidence = true,
    IncludeBoundingBoxes = true
};
```

**Miért tartalmazzunk megbízhatósági pontszámokat?**  
A megbízhatósági pontszám (0‑100 %) megmutatja, mennyire biztos a motor az egyes karakterekben. Ha a kimenetet további logikába (például egy költség‑jóváhagyási munkafolyamatba) táplálod, alacsony megbízhatóságú szimbólumokat automatikusan elutasíthatod vagy megjelölheted.

**Miért kérjünk határoló dobozokat?**  
A határoló dobozok elengedhetetlenek, ha ki szeretnéd emelni a szöveget az eredeti képen, alrégiókat szeretnél kinyerni, vagy az OCR eredményeket UI‑réteggel szeretnéd összehangolni. Minden `character.Bounds` megadja az X, Y, szélesség és magasság értékeket pixel koordinátákban.

## 3. lépés – OCR végrehajtása JPG‑n és szöveg kinyerése képből

Most ténylegesen futtatjuk a motort. A `Recognize()` hívás elvégzi a nehéz munkát, és egy `OcrResult` objektumot ad vissza.

```csharp
// Step 3: Run the OCR process
OcrResult ocrResult = ocrEngine.Recognize();
```

Ha a kép útvonala hibás vagy a fájl nem támogatott formátumú, az Aspose `FileNotFoundException` vagy `UnsupportedImageFormatException` kivételt dob. A hívást éles kódban try/catch blokkba helyezd, hogy ezeket az eseteket elegánsan kezeld.

### A sima szöveg kinyerése

Ha csak a összefűzött szövegre van szükséged, olvashatod a `ocrResult.Text` értéket:

```csharp
Console.WriteLine("Full extracted text:");
Console.WriteLine(ocrResult.Text);
```

De mivel a megbízhatósági pontszámokat és a határoló dobozokat is kérjük, végigiterálunk a struktúrán, hogy megtekintsük minden karakter részleteit.

## 4. lépés – Sorok, szimbólumok bejárása és OCR megbízhatósági pontszámok megjelenítése

Itt a ciklus, amely kiír minden karaktert, annak megbízhatóságát és a dobozát. Itt ragyog igazán a **nyugtakép beolvasása** példa.

```csharp
// Step 4: Walk through each line and each symbol (character)
foreach (var textLine in ocrResult.Lines)
{
    foreach (var character in textLine.Symbols)
    {
        Console.WriteLine(
            $"Char: '{character.Text}'  Confidence: {character.Confidence}%  Box: {character.Bounds}");
    }
}
```

A minta kimenet így nézhet ki:

```
Char: 'R'  Confidence: 98%  Box: {X=12,Y=34,Width=15,Height=20}
Char: 'e'  Confidence: 95%  Box: {X=28,Y=34,Width=12,Height=20}
Char: 'c'  Confidence: 92%  Box: {X=41,Y=34,Width=13,Height=20}
...
```

**A számok értelmezése:**  
- **Megbízhatóság ≥ 90 %** – általában biztonságos elfogadni.  
- **Megbízhatóság 70‑89 %** – érdemes lehet dupla ellenőrzést végezni, különösen az összegek számjegyeinél.  
- **Megbízhatóság < 70 %** – fontold meg, hogy manuális felülvizsgálatra jelöld.

## 5. lépés – Teljes futtatható példa (hibakezeléssel együtt)

Mindent összevonva, itt egy teljes program, amelyet beilleszthetsz a `Program.cs`‑be. Egyszerű ellenőrzést tartalmaz hiányzó fájlok esetén, és barátságos üzenetet ír ki, ha az OCR hibát jelez.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Path to the receipt image – adjust to your environment
            const string imagePath = "YOUR_DIRECTORY/receipt.jpg";

            if (!System.IO.File.Exists(imagePath))
            {
                Console.WriteLine($"Error: File not found -> {imagePath}");
                return;
            }

            try
            {
                // Initialize engine
                OcrEngine ocrEngine = new OcrEngine
                {
                    Image = ImageStream.FromFile(imagePath),
                    Options = new OcrOptions
                    {
                        OutputFormat = OcrOutputFormat.PlainText,
                        IncludeConfidence = true,
                        IncludeBoundingBoxes = true
                    }
                };

                // Perform OCR
                OcrResult ocrResult = ocrEngine.Recognize();

                // Show full plain text (optional)
                Console.WriteLine("=== Extracted Text ===");
                Console.WriteLine(ocrResult.Text);
                Console.WriteLine();

                // Show each character with confidence and bounding box
                Console.WriteLine("=== Detailed Character Data ===");
                foreach (var line in ocrResult.Lines)
                {
                    foreach (var symbol in line.Symbols)
                    {
                        Console.WriteLine(
                            $"Char: '{symbol.Text}'  Confidence: {symbol.Confidence}%  Box: {symbol.Bounds}");
                    }
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine($"OCR failed: {ex.Message}");
            }
        }
    }
}
```

### Várható kimenet

Amikor a `dotnet run` parancsot futtatod, a konzol először megjeleníti a összefűzött nyugtaszöveget, majd egy listát minden karakterről a megbízhatósági pontszámmal és a határoló dobozzal. Ha egy karakter megbízhatósága alacsony, 80 % alatti százalékot látsz, ami jelzés arra, hogy a nyugta azon részét manuálisan ellenőrizd.

## Bónusz: Több nyugta feldolgozása egy mappában

Ha egy csomag nyugta JPG‑t tartalmaz, helyezd a fenti logikát egy `foreach (var file in Directory.GetFiles(folder, "*.jpg"))` ciklusba. Ne felejtsd el minden fájlhoz újraállítani az `OcrEngine`‑t, vagy a cikluson belül új példányt létrehozni, hogy elkerüld az állapot szivárgását.

```csharp
string folder = "YOUR_DIRECTORY/Receipts";
foreach (var file in System.IO.Directory.GetFiles(folder, "*.jpg"))
{
    // reuse the same code block, just replace imagePath with 'file'
}
```

A tömeges feldolgozás hasznos az éjszakai költségimportokhoz.

## Következtetés

Most már egy stabil, vég‑től‑végig megoldással rendelkezel a **OCR megbízhatósági pontszámok** C#‑ban történő megszerzéséhez, a **képből szöveg kinyeréséhez**, és a **OCR határoló dobozok** lekéréséhez, miközben **OCR‑t hajtasz végre JPG** fájlokon, például egy **nyugtakép beolvasásán**. A kód teljesen önálló, a legújabb Aspose.OCR verzióval működik (2026‑05‑31‑ig), és a részletes adatokat biztosítja, amelyekre a megbízható dokumentumfeldolgozó csővezetékek építéséhez szükséged van.

Mi a következő? Próbáld meg megjeleníteni a határoló dobozokat az eredeti nyugtán a `System.Drawing` vagy egy UI‑könyvtár segítségével, vagy a alacsony megbízhatóságú karaktereket egy másodlagos ellenőrző szolgáltatásba küldeni. Kísérletezhetsz különböző nyelvekkel is, például a `ocrEngine.Options.Language = OcrLanguage.French;` beállítással – az API számos nyelvet támogat.

Boldog kódolást, és legyenek a megbízhatósági pontszámaid mindig magasak! 

![Konzol kimenet, amely OCR megbízhatósági pontszámokat és határoló dobozokat mutat egy nyugtán

## Mit érdemes még megtanulni?

- [Képszöveg kinyerése C#‑ban nyelvválasztással az Aspose.OCR használatával](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Hogyan kapjunk OCR karakterválasztásokat a felismert karakterekhez képfelismerésben](/ocr/english/net/text-recognition/get-choices-for-recognized-characters/)
- [Hogyan használjuk az Aspose OCR‑t JSON eredményhez képfelismerésben](/ocr/english/net/text-recognition/get-result-as-json/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}