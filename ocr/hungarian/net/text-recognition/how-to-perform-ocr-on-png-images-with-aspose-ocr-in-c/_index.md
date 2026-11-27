---
category: general
date: 2026-11-26
description: Ismerje meg, hogyan végezhet OCR-t PNG fájlokon, konvertálhatja a PNG-t
  szöveggé, és nyerhet ki cirill szöveget az Aspose.OCR segítségével – fejlesztőknek
  szóló lépésről‑lépésre útmutató.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to perform OCR
- convert PNG to text
- recognize text from PNG
- extract Cyrillic text
- load image for OCR
language: hu
lastmod: 2026-11-26
og_description: Hogyan végezzünk OCR-t PNG fájlokon, és nyerjünk ki cirill szöveget
  az Aspose.OCR használatával C#-ban. Kövesd ezt a teljes útmutatót a PNG szöveggé
  konvertálásához.
og_image_alt: how to perform OCR on a PNG image using Aspose.OCR
og_title: Hogyan végezzünk OCR-t PNG képeken az Aspose.OCR-rel – C# útmutató
schemas:
- author: Aspose
  dateModified: '2026-11-26'
  description: Learn how to perform OCR on PNG files, convert PNG to text, and extract
    Cyrillic text using Aspose.OCR – step‑by‑step guide for developers.
  headline: How to perform OCR on PNG images with Aspose.OCR in C#
  type: TechArticle
- description: Learn how to perform OCR on PNG files, convert PNG to text, and extract
    Cyrillic text using Aspose.OCR – step‑by‑step guide for developers.
  name: How to perform OCR on PNG images with Aspose.OCR in C#
  steps:
  - name: Handling large images
    text: 'If the PNG is larger than 2 MB, consider down‑scaling it before recognition
      to speed up processing:'
  - name: 'Edge case: Missing language module'
    text: 'If the download fails (e.g., offline environment), the engine throws an
      `OcrException`. Catch it to provide a graceful fallback:'
  - name: Expected output
    text: 'If `sample_image.png` contains the Cyrillic phrase “Привет мир”, the console
      will display:'
  - name: How it works
    text: 1. **Engine creation** – prepares the OCR pipeline. 2. **Image loading**
      – supports both raw PNG and down‑scaled versions for performance. 3. **Language
      selection** – demonstrates **extract Cyrillic text** while handling missing
      modules. 4. **Recognition** – the core **recognize text from PNG** call
  type: HowTo
tags:
- OCR
- C#
- Aspose.OCR
title: Hogyan végezzünk OCR-t PNG képeken az Aspose.OCR segítségével C#-ban
url: /hu/net/text-recognition/how-to-perform-ocr-on-png-images-with-aspose-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan végezzünk OCR-t PNG képeken az Aspose.OCR használatával C#-ban

Ha **hogyan végezzünk OCR-t** egy PNG fájlon, ez az útmutató megmutatja a pontos lépéseket a PNG szöveggé konvertálásához az Aspose.OCR használatával. Akár cirill szöveget szeretne kinyerni beolvasott dokumentumokból, akár egyszerűen szöveget felismerni PNG képernyőképekről, a megoldás azonnal működik, és csak néhány C# sorra van szükség.

Ebben a tutorialban megtanulja, hogyan:

* **képet betölteni OCR-hez** egy helyi mappából,
* konfigurálja a motorot a **cirill szöveg kinyeréséhez**,
* **szöveget felismerése PNG-ből** és tiszta karakterláncot kap,
* kezelje a gyakori buktatókat, például a hiányzó nyelvi modulokat és a nagy képeket.

Nem szükséges előzetes tapasztalat az Aspose.OCR-rel – elegendő egy .NET fejlesztői környezet és egy PNG kép, amelyet feldolgozni szeretne.

## Előkövetelmények

Mielőtt elkezdené, győződjön meg róla, hogy rendelkezik:

* .NET 6.0 (vagy újabb) telepítve.
* Licencelt vagy próbaverziós **Aspose.OCR for .NET**. Ingyenes próbaverziót a Aspose weboldaláról szerezhet.
* Visual Studio 2022 (vagy bármely .NET-et támogató IDE).
* Egy PNG fájl, amely a kinyerni kívánt szöveget tartalmazza (a példában a `sample_image.png` fájlt használjuk).

## 1. lépés: Az Aspose.OCR NuGet csomag telepítése

Nyisson egy terminált a projekt mappájában, és futtassa a következőt:

```bash
dotnet add package Aspose.OCR
```

A csomag tartalmazza a mag OCR motorját és az összes nyelvi modult. Ha egy helyileg nem elérhető nyelvet kér, az Aspose.OCR automatikusan letölti a szükséges modult.

## 2. lépés: OCR motor példány létrehozása (hogyan végezzünk OCR-t)

Az első végrehajtható lépés bármely OCR munkafolyamatban a motor példányosítása. Ez az objektum kezeli az összes további műveletet, például a kép betöltését és a felismerést.

```csharp
using Aspose.OCR;

// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();
```

**Miért fontos:** A `OcrEngine` osztály magába foglalja az OCR csővezetéket. Egyetlen példány létrehozása és többszöri újrahasználata több képnél csökkenti a memóriahasználatot és javítja a teljesítményt.

## 3. lépés: Kép betöltése OCR-hez – a forrás PNG fájl megadása

A kép betöltése az a pont, ahol **képet betölteni OCR-hez**. Az Aspose.OCR több bemeneti típust is elfogad; a legegyszerűbb a `ImageStream.FromFile`.

```csharp
// Load the PNG image from disk
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/sample_image.png");
```

> **Pro tipp:** Használjon abszolút elérési utat vagy a `Path.Combine`-t a futásidejű hibák elkerülése érdekében különböző környezetekben.

### Nagy képek kezelése

Ha a PNG nagyobb, mint 2 MB, fontolja meg a méretezés csökkentését a felismerés előtt a feldolgozás felgyorsítása érdekében:

```csharp
using System.Drawing;

// Downscale large images to a maximum width of 1200 pixels
Bitmap original = new Bitmap(@"YOUR_DIRECTORY/sample_image.png");
int maxWidth = 1200;
int newHeight = (int)(original.Height * (maxWidth / (double)original.Width));
Bitmap resized = new Bitmap(original, new Size(maxWidth, newHeight));

using (var ms = new MemoryStream())
{
    resized.Save(ms, System.Drawing.Imaging.ImageFormat.Png);
    ocrEngine.Image = ImageStream.FromStream(ms);
}
```

## 4. lépés: Nyelv beállítása – cirill szöveg kinyerése

Alapértelmezés szerint az Aspose.OCR az angolt feltételezi. A **cirill szöveg kinyeréséhez** állítsa a `Language` tulajdonságot `Language.Cyrillic`-ra. A szükséges modul automatikusan letöltődik, amikor először futtatja a kódot.

```csharp
// Set the OCR language to Cyrillic
ocrEngine.Language = Language.Cyrillic;
```

Ha több nyelvet kell felismerni (például angolt és cirillt), kombinálhatja őket:

```csharp
ocrEngine.Language = Language.English | Language.Cyrillic;
```

### Szélsőséges eset: Hiányzó nyelvi modul

Ha a letöltés sikertelen (például offline környezetben), a motor `OcrException`-t dob. Fogja el, hogy elegáns visszaesést biztosítson:

```csharp
try
{
    ocrEngine.Language = Language.Cyrillic;
}
catch (OcrException ex)
{
    Console.WriteLine($"Language module could not be loaded: {ex.Message}");
    // Optionally, fall back to English or abort the process
}
```

## 5. lépés: Felismerési művelet végrehajtása (szöveg felismerése PNG-ből)

Miután a kép és a nyelv be van állítva, **szöveget felismerhet PNG-ből**. A `Recognize` metódus szinkron módon futtatja az OCR csővezetéket.

```csharp
// Run OCR
ocrEngine.Recognize();
```

**Miért működik:** Belsőleg az Aspose.OCR előfeldolgozást (binarizálás, zajszűrés) alkalmaz, mielőtt a képet egy a kiválasztott nyelvre hangolt neurális hálózaton alapuló felismerőbe adná.

## 6. lépés: Felismert szöveg lekérése és megjelenítése (PNG konvertálása szöveggé)

A felismerés után a kinyert karakterlánc a `Text` tulajdonságon keresztül érhető el. Ez az utolsó lépés a **PNG konvertálása szöveggé** folyamatban.

```csharp
// Get the recognized text
string recognizedText = ocrEngine.Text;

// Output the result
Console.WriteLine("=== OCR Result ===");
Console.WriteLine(recognizedText);
```

### Várt kimenet

Ha a `sample_image.png` a cirill „Привет мир” kifejezést tartalmazza, a konzol a következőt jeleníti meg:

```
=== OCR Result ===
Привет мир
```

A kimenet tartalmazhat sortöréseket és írásjeleket pontosan úgy, ahogy a képen megjelennek. Szükség esetén a karakterláncot utófeldolgozhatja a `String.Trim()`, `Regex` vagy egyéb szöveg‑tisztító eszközökkel.

## 7. lépés: Opcionális – Az eredmény mentése fájlba

Az OCR eredmény tárolása lehetővé teszi a további feldolgozást (például indexelés, fordítás). Íme egy gyors mód a szöveg UTF‑8 fájlba írására:

```csharp
File.WriteAllText(@"YOUR_DIRECTORY/ocr_output.txt", recognizedText, Encoding.UTF8);
Console.WriteLine("OCR text saved to ocr_output.txt");
```

## Gyakori buktatók és hogyan kerülhetők el

| Issue | Symptom | Fix |
|-------|----------|-----|
| **Hiányzó nyelvi modul** | `OcrException` a `Language = Language.Cyrillic` esetén | Győződjön meg róla, hogy az első futtatáskor van internetkapcsolat, vagy töltse le előre a modulokat az Aspose offline csomagjával. |
| **Elmosódott vagy alacsony kontrasztú kép** | Gyenge pontosság, sok “?” karakter | Előfeldolgozás: növelje a kontrasztot, alkalmazzon élesítést, vagy konvertálja szürkeárnyalatúvá a képet, mielőtt a motorba adná. |
| **Nagyon nagy PNG** | Hosszú feldolgozási idő, esetleg `OutOfMemoryException` | Csökkentse a méretet a 3. lépésben leírt módon, vagy bontsa a többoldalas képet külön csempékre. |
| **Nem UTF‑8 karakterek** | Torult kimenet | Ellenőrizze, hogy a konzol vagy a fájlíró UTF‑8 kódolást használ (`Encoding.UTF8`). |

## Teljes, futtatható példa

Az alábbiakban a teljes program látható, amely tartalmazza a fenti összes lépést. Másolja be egy új konzol projektbe, és futtassa a fájlutak módosítása után.

```csharp
using System;
using System.Drawing;
using System.IO;
using System.Text;
using Aspose.OCR;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1. Create OCR engine
            OcrEngine ocrEngine = new OcrEngine();

            // 2. Load PNG image (with optional down‑scaling for large files)
            string imagePath = @"YOUR_DIRECTORY/sample_image.png";
            Bitmap original = new Bitmap(imagePath);
            const int maxWidth = 1200;

            if (original.Width > maxWidth)
            {
                int newHeight = (int)(original.Height * (maxWidth / (double)original.Width));
                Bitmap resized = new Bitmap(original, new Size(maxWidth, newHeight));

                using (var ms = new MemoryStream())
                {
                    resized.Save(ms, System.Drawing.Imaging.ImageFormat.Png);
                    ocrEngine.Image = ImageStream.FromStream(ms);
                }
            }
            else
            {
                ocrEngine.Image = ImageStream.FromFile(imagePath);
            }

            // 3. Set language to Cyrillic (fallback to English if needed)
            try
            {
                ocrEngine.Language = Language.Cyrillic;
            }
            catch (OcrException ex)
            {
                Console.WriteLine($"Failed to load Cyrillic module: {ex.Message}");
                Console.WriteLine("Falling back to English.");
                ocrEngine.Language = Language.English;
            }

            // 4. Recognize text
            ocrEngine.Recognize();

            // 5. Retrieve and display the text (convert PNG to text)
            string recognizedText = ocrEngine.Text;
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(recognizedText);

            // 6. Save result to a UTF‑8 file
            string outputPath = @"YOUR_DIRECTORY/ocr_output.txt";
            File.WriteAllText(outputPath, recognizedText, Encoding.UTF8);
            Console.WriteLine($"OCR text saved to {outputPath}");
        }
    }
}
```

### Hogyan működik

1. **Engine creation** – előkészíti az OCR csővezetéket.  
2. **Image loading** – támogatja a nyers PNG-t és a lecsökkentett verziókat a teljesítmény érdekében.  
3. **Language selection** – bemutatja a **cirill szöveg kinyerését**, miközben kezeli a hiányzó modulokat.  
4. **Recognition** – a központi **szöveg felismerése PNG-ből** hívás.  
5. **Result handling** – bemutatja a **PNG konvertálása szöveggé** folyamatot, és a kimenetet fájlba írja.

Futtassa a programot a `dotnet run` paranccsal. Ha minden megfelelően be van állítva, a felismert szöveget a konzolra nyomtatva és a `ocr_output.txt` fájlba mentve fogja látni.

## Következtetés

Ebben az útmutatóban megtanulta, **hogyan végezzünk OCR-t** PNG fájlokon az Aspose.OCR for .NET használatával, lefedve mindent a **képet betölteni OCR-hez**-től a **cirill szöveg kinyeréséig** és a **PNG konvertálása szöveggé**-ig. A teljes, futtatható példa bemutatja a szabványos munkafolyamatot, a gyakori szélsőséges eseteket és a gyakorlati tippeket, amelyek megbízhatóvá teszik az OCR csővezetéket.

**Következő lépések**

* Fedezze fel a **szöveg felismerése PNG-ből** további nyelvekkel (arab, kínai) a `Language` zászlók kombinálásával.  
* Integrálja az OCR eredményt az Azure Cognitive Search-be kereshető dokumentumarchívumokhoz.  
* Kísérletezzen az Aspose.OCR `OcrEngine` beállításaival, például a `Resolution`-nel.

## Mit érdemes még megtanulni?

A következő útmutatók szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás tartalmaz teljes, működő kódpéldákat lépésről‑lépésre magyarázatokkal, hogy segítsen elsajátítani további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeiben.

- [Hogyan töltsük le az Aspose.OCR modellt és nyerjünk ki szöveget PNG-ből C#-ban](/ocr/english/net/text-recognition/how-to-download-ocr-model-and-extract-text-from-png-using-as/)
- [Hogyan végezzünk OCR-t C#-ban – Cirill szöveg felismerése az Aspose segítségével](/ocr/english/net/text-recognition/how-to-perform-ocr-in-c-recognize-cyrillic-text-with-aspose/)
- [Hogyan végezzünk kötegelt OCR-t C#-ban – Gyors módszer PNG fájlok szövegének kinyerére](/ocr/english/net/ocr-optimization/how-to-batch-ocr-in-c-fast-way-to-extract-text-png-files/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}