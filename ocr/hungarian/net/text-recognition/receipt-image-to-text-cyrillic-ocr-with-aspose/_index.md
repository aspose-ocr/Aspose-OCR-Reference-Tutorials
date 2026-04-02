---
category: general
date: 2026-04-01
description: Tanulja meg, hogyan alakíthatja a nyugtaképet szöveggé az Aspose OCR
  segítségével. Ez az útmutató bemutatja, hogyan lehet kinyerni a cirill szöveget,
  betölteni a képet OCR-hez, és hatékonyan felismerni a cirill karaktereket.
draft: false
keywords:
- receipt image to text
- extract cyrillic text
- load image for ocr
- recognize cyrillic characters
- create OCR engine
language: hu
og_description: Alakítsa át a nyugtaképet szöveggé az Aspose OCR-rel. Tanulja meg,
  hogyan lehet cirill szöveget kinyerni, képet betölteni OCR-hez, és cirill karaktereket
  felismerni C#-ban.
og_title: nyugta kép szöveggé – cirill OCR az Aspose-szal
tags:
- OCR
- C#
- Aspose
- Cyrillic
title: nyugta kép szöveggé – cirill OCR az Aspose-szal
url: /hu/net/text-recognition/receipt-image-to-text-cyrillic-ocr-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# nyugta kép szöveggé – cirill OCR az Aspose-szal

Szükséged volt már arra, hogy **nyugta képet szöveggé** alakíts, de a karakterek mind cirill írásban vannak? Nem vagy egyedül ezzel a problémával. Sok kiskereskedelmi vagy könyvelő alkalmazásban a nyugták orosz, bolgár vagy szerb betűkkel jelennek meg, és mégis egy tiszta, kereshető sztringre van szükséged.  

Ebben az útmutatóban pontosan megmutatjuk, hogyan **nyerheted ki a cirill szöveget** egy nyugta fotóból, **töltsd be a képet OCR-hez**, és **ismerd fel a cirill karaktereket** az Aspose OCR könyvtár segítségével. A végére egy kész‑C# programod lesz, amely az OCR eredményt egy `.txt` fájlba írja.

## Amire szükséged lesz

- **.NET 6** (vagy bármely friss .NET verzió) – a kód .NET Framework 4.7+ alatt is működik.  
- **Aspose.OCR for .NET** NuGet csomag – `Install-Package Aspose.OCR`.  
- Egy minta nyugta kép, amely cirill szöveget tartalmaz (pl. `cyrillic_receipt.jpg`).  
- Fejlesztői környezet – Visual Studio, VS Code vagy Rider megfelel.  

További natív függőségekre nincs szükség; az Aspose magában szállítja a nyelvi modelleket és a nehéz munkát belsőleg kezeli.

## nyugta kép szöveggé – Az OCR motor beállítása

Az első lépés, hogy **létrehozzuk az OCR motor** példányát, és megadjuk, melyik nyelvre vagyunk kíváncsiak. Az Aspose ezt egyszerűvé teszi:

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;   // language and resource handling
using System.Drawing;      // Image class
using System.IO;

class CyrillicDemo
{
    static void Main()
    {
        // Step 1: Instantiate the OCR engine
        var ocrEngine = new OcrEngine();

        // Step 2: Tell Aspose we want Cyrillic support
        ocrEngine.Language = Language.Cyrillic;

        // Optional: Pre‑load the model if you’ll run offline later
        // ResourceManager.Preload(Language.Cyrillic);
```

> **Pro tipp:** A modell előtöltése elkerüli az első futtatáskor a hálózati hívást, ami kényelmes asztali vagy beágyazott környezetben.

## Hogyan nyerjünk ki cirill szöveget – A nyugta kép betöltése

Miután a motor készen áll, **be kell töltenünk a képet OCR-hez**. A `System.Drawing.Image` osztály tökéletesen működik a legtöbb bitmap formátumnál.

```csharp
        // Step 3: Point to your receipt image
        string imagePath = @"YOUR_DIRECTORY\cyrillic_receipt.jpg";

        // Step 4: Load the image inside a using block (ensures disposal)
        using (var image = Image.FromFile(imagePath))
        {
            // Step 5: Run the OCR process
            var recognitionResult = ocrEngine.Recognize(image);
```

Ha a fájl nem található, az `Image.FromFile` `FileNotFoundException`-t dob. Érdemes a teljes kódot egy `try…catch` blokkba helyezni a termelési környezetben.

## Cirill karakterek felismerése – A szöveg kinyerése

A `recognitionResult` objektum tartalmazza a nyers szöveget, a megbízhatósági pontszámokat, sőt akár a keretmezőket is, ha később szükséged van rájuk. Egy egyszerű “nyugta kép szöveggé” átalakításhoz csak a `Text` tulajdonságot írjuk ki egy fájlba:

```csharp
            // Step 6: Write the extracted text to a .txt file
            string outputPath = @"YOUR_DIRECTORY\cyrillic.txt";
            File.WriteAllText(outputPath, recognitionResult.Text);

            // Quick verification: print to console
            Console.WriteLine("OCR completed. Extracted text:");
            Console.WriteLine(recognitionResult.Text);
        }
    }
}
```

A program futtatásakor valami ilyesmit kell látnod:

```
OCR completed. Extracted text:
СЧЕТ № 12345
Дата: 01/04/2026
Товар      Кол-во   Цена
Хлеб       2        30,00
Молоко     1        45,00
Итого:               105,00
```

Ez a **nyugta kép szöveggé** eredmény, amit kerestél.

![receipt image to text example](receipt-ocr-example.png "Example of a receipt image being converted to text")

*Kép alternatív szövege: nyugta kép szöveggé konvertálása, amelyen az Aspose OCR által kinyert cirill karakterek láthatók.*

## Szélsőséges esetek és gyakori kérdések

### Mi van, ha a nyelvi modell még nincs letöltve?

Az Aspose automatikusan letölti a szükséges modellt, amikor először beállítod az `ocrEngine.Language = Language.Cyrillic;` értéket. Ha a gépnek nincs internetkapcsolata, az opcionális előtöltés sikertelen lesz. Ebben az esetben vagy manuálisan biztosítsd a modellt (lásd az Aspose dokumentációt), vagy győződj meg róla, hogy a készülék elérheti a `download.aspose.com` címet.

### Hogyan kezeljek több nyelvet egyetlen nyugtán?

Megadhatsz egy vesszővel elválasztott listát:

```csharp
ocrEngine.Language = Language.Cyrillic | Language.English;
```

Az Aspose megpróbálja felismerni a karaktereket mindkét készletből.

### A nyugtám elmosódott – javítható a pontosság?

Az Aspose OCR alapvető képelőfeldolgozást kínál:

```csharp
ocrEngine.ImagePreprocessor = new ImagePreprocessor
{
    Sharpen = true,
    Binarize = true,
    Denoise = true
};
```

Ezt a `Recognize` hívása előtt alkalmazd.

### Hogyan működik nagy kötegű feldolgozás?

A felismerési ciklust tedd egy `Parallel.ForEach`‑be, és használd ugyanazt az `OcrEngine` példányt (a modell betöltése után szálbiztos). Ne felejtsd el zárolni a motort, ha szálbiztonsági problémákba ütközöl.

## Teljes működő példa (minden lépés egyben)

Az alábbi program teljes, másolás‑beillesztés‑kész kód, amely tartalmazza az opcionális előtöltést és az alapvető hibakezelést:

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System;
using System.Drawing;
using System.IO;

class CyrillicDemo
{
    static void Main()
    {
        try
        {
            // Create OCR engine and select Cyrillic language
            var ocrEngine = new OcrEngine();
            ocrEngine.Language = Language.Cyrillic;

            // Optional: preload model for offline use
            // ResourceManager.Preload(Language.Cyrillic);

            // Path to the receipt image
            string imagePath = @"YOUR_DIRECTORY\cyrillic_receipt.jpg";

            // Verify the file exists
            if (!File.Exists(imagePath))
                throw new FileNotFoundException("Receipt image not found.", imagePath);

            using (var image = Image.FromFile(imagePath))
            {
                // Perform OCR
                var result = ocrEngine.Recognize(image);

                // Output path for extracted text
                string outputPath = @"YOUR_DIRECTORY\cyrillic.txt";
                File.WriteAllText(outputPath, result.Text);

                Console.WriteLine("✅ receipt image to text conversion succeeded.");
                Console.WriteLine("Extracted text saved to: " + outputPath);
                Console.WriteLine("\n--- Extracted Text ---\n");
                Console.WriteLine(result.Text);
            }
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine("❌ An error occurred: " + ex.Message);
        }
    }
}
```

Futtasd a programot (`dotnet run` a projekt mappájából), és kapsz egy `.txt` fájlt a **nyugta kép szöveggé** kimenettel.

## Összegzés

Most már van egy szilárd, vég‑től‑végig megoldásod a **nyugta kép szöveggé** átalakítására – kifejezetten cirill írásra – az Aspose OCR segítségével. Megmutattuk, hogyan **hozd létre az OCR motort**, **töltsd be a képet OCR-hez**, **nyerd ki a cirill szöveget**, és **ismerd fel a cirill karaktereket** néhány C# sorral.  

Mi a következő lépés? Próbáld ki egy mappa nyugtáinak feldolgozását, kísérletezz az `ImagePreprocessor`‑ral a pontosság növelése érdekében, vagy kombináld az OCR kimenetet egy adatbázissal az automatikus könyveléshez. Ha más ábécékkel is dolgoznod kell, cseréld le a  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}