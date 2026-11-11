---
category: general
date: 2026-03-17
description: c# OCR oktatóanyag – fedezd fel, hogyan lehet szöveget kinyerni képfájlokból,
  szöveget olvasni WebP fotókból, és képet szöveggé konvertálni egy egyszerű OcrEngine
  segítségével.
draft: false
keywords:
- c# OCR tutorial
- extract text from image
- read text from webp
- recognize text from photo
- convert image to text
language: hu
og_description: A C# OCR oktató bemutatja, hogyan lehet szöveget kinyerni képfájlokból,
  szöveget olvasni WebP fotókból, és néhány sor kóddal képet szöveggé konvertálni.
og_title: c# OCR útmutató – Szöveg kinyerése képekből percek alatt
tags:
- C#
- OCR
- Image Processing
title: 'c# OCR útmutató: Szöveg kinyerése képekből (WebP, Fotó) – Gyors útmutató'
url: /hu/net/text-recognition/c-ocr-tutorial-extract-text-from-images-webp-photo-quick-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# OCR tutorial – Szöveg kinyerése képekből (WebP, Fotó)

Valaha szükséged volt **képfájlokból szöveg kinyerésére**, de nem tudtad, hol kezdj hozzá C#‑ban? Lehet, hogy van egy WebP képernyőfotód, egy JPEG nyugta, vagy egy beolvasott PDF oldal, és csak a benne lévő szavakat szeretnéd. Ebben a **c# OCR tutorial**‑ban végigvezetünk egy teljes, azonnal futtatható példán, amely egy fotóból olvas szöveget, kezeli a WebP‑t és más modern formátumokat, és a képet egyszerű szöveggé alakítja – mind néhány sorban.

**Mi a haszon?** Bármely szöveget tartalmazó képet kereshető karakterláncokká alakíthatsz, betáplálhatod adatbázisokba, vagy továbbíthatod downstream AI folyamatokba. Nincs varázslat, csak egy megbízható OCR motor, néhány .NET API, és világos magyarázatok arra, hogy „miért” minden lépés.

## Amire szükséged lesz

- **.NET 6 SDK** (vagy újabb). Az alábbi kód .NET 6+‑vel fordítható, és Windows, Linux vagy macOS rendszeren fut.
- **Visual Studio 2022** vagy bármely kedvelt szerkesztő (a VS Code is megfelelő).
- A **`Microsoft.Windows.SDK.Contracts`** NuGet csomag (biztosítja a `Windows.Media.Ocr`‑t). Telepítsd a következővel:

```bash
dotnet add package Microsoft.Windows.SDK.Contracts
```

- Egy képfájl, amelyet feldolgozni szeretnél – ebben a tutorialban egy **WebP** fotót használunk, amely `photo.webp` néven található a `YOUR_DIRECTORY` mappában.

> Pro tipp: Ha nem Windows platformon vagy, kicserélheted az `OcrEngine`‑t egy cross‑platform könyvtárra, például **Tesseract**‑ra. A környező kód gyakorlatilag változatlan marad.

## 1. lépés: C# OCR tutorial projekt létrehozása

Először hozz létre egy új konzolos alkalmazást. Nyiss egy terminált, és futtasd:

```bash
dotnet new console -n OcrDemo
cd OcrDemo
```

Add hozzá a szükséges csomagot (ahogy fent láttad), és nyisd meg a projektet az IDE‑ben. Ez a váz biztosítja a tiszta kiindulási pontot a **c# OCR tutorial**‑hoz.

## 2. lépés: Névterek importálása és a kép előkészítése

Néhány `using` direktívára van szükségünk, hogy a fordító tudja, hol találja az `OcrEngine`, `SoftwareBitmap` és a kép‑betöltő segédfüggvényeket.

```csharp
using System;
using System.IO;
using Windows.Graphics.Imaging;
using Windows.Media.Ocr;
using Windows.Storage.Streams;
```

> **Miért ezek a névterek?**  
> `Windows.Media.Ocr` tartalmazza az `OcrEngine` osztályt, amely ténylegesen végzi a felismerést. `Windows.Graphics.Imaging` lehetővé teszi a kép (beleértve a WebP‑t) dekódolását `SoftwareBitmap`‑be, amelyet a motor ért. A `System.IO` és `Windows.Storage.Streams` segédfüggvények egyszerűvé teszik a fájlok betöltését.

Most töltsd be a képet. A beépített dekóder képes kezelni a WebP, HEIF, PNG, JPEG és további formátumokat, így **WebP‑ból is olvashatsz szöveget** extra pluginek nélkül.

```csharp
// Step 2: Load the image file into a SoftwareBitmap
string imagePath = Path.Combine("YOUR_DIRECTORY", "photo.webp");

// Open the file as a random access stream
using (IRandomAccessStream stream = File.OpenRead(imagePath).AsRandomAccessStream())
{
    // Decode the image (auto-detects format)
    BitmapDecoder decoder = await BitmapDecoder.CreateAsync(stream);
    SoftwareBitmap bitmap = await decoder.GetSoftwareBitmapAsync();
    
    // Optional: Convert to grayscale for better OCR accuracy
    SoftwareBitmap grayBitmap = SoftwareBitmap.Convert(bitmap, BitmapPixelFormat.Gray8);
    
    // Pass the bitmap to the next step
    await RecognizeTextAsync(grayBitmap);
}
```

> **Külön eset:** Ha a képed már fekete‑fehér, kihagyhatod a konverziós lépést. A szürkeárnyalatos átalakítás kis teljesítményelőny, és gyakran javítja a felismerést zajos fotókon.

## 3. lépés: OCR motor futtatása – Szöveg felismerése a fotóból

Itt van a **c# OCR tutorial** szíve. Létrehozunk egy `OcrEngine` példányt, betápláljuk a bitmapet, és kinyerjük a felismert szöveget.

```csharp
static async Task RecognizeTextAsync(SoftwareBitmap bitmap)
{
    // Step 3: Create the OCR engine instance – it automatically picks the best language
    OcrEngine ocrEngine = OcrEngine.TryCreateFromUserProfileLanguages();

    if (ocrEngine == null)
    {
        Console.WriteLine("❌ No OCR engine available for the current language.");
        return;
    }

    // Perform recognition
    OcrResult ocrResult = await ocrEngine.RecognizeAsync(bitmap);

    // Step 4: Display the extracted text – this is the “convert image to text” part
    Console.WriteLine("📝 Recognized text:");
    Console.WriteLine(ocrResult.Text);
}
```

**Mi történik?**  
- `TryCreateFromUserProfileLanguages()` a Windows felhasználói profil nyelv(ek)ét választja, ami általában lefedi az angolt, spanyolt stb. Ha egy konkrét nyelvre van szükséged, használd a `OcrEngine.TryCreateFromLanguage(new Language("fr-FR"))`‑t.  
- `RecognizeAsync` a nehéz munkát egy háttérszálon végzi, és egy `OcrResult`‑ot ad vissza, amely tartalmazza a nyers szöveget, a szavak kereteit és a bizalmi pontszámokat.  
- Végül kiírjuk az `ocrResult.Text`‑et, így megkapod a **convert image to text** eredményt, amelyet tovább használhatsz.

## 4. lépés: Teljes, futtatható példa

Összeállítva, itt egy önálló program, amelyet beilleszthetsz a `Program.cs`‑be. Lefordul, fut, és kiírja a `photo.webp`‑ből kinyert szöveget.

```csharp
// Program.cs – Complete c# OCR tutorial example
using System;
using System.IO;
using System.Threading.Tasks;
using Windows.Graphics.Imaging;
using Windows.Media.Ocr;
using Windows.Storage.Streams;

class Program
{
    static async Task Main(string[] args)
    {
        // Replace with your actual directory and file name
        string imagePath = Path.Combine("YOUR_DIRECTORY", "photo.webp");

        if (!File.Exists(imagePath))
        {
            Console.WriteLine($"❗ Image not found: {imagePath}");
            return;
        }

        // Load and optionally preprocess the image
        using (IRandomAccessStream stream = File.OpenRead(imagePath).AsRandomAccessStream())
        {
            BitmapDecoder decoder = await BitmapDecoder.CreateAsync(stream);
            SoftwareBitmap bitmap = await decoder.GetSoftwareBitmapAsync();

            // Convert to grayscale – improves OCR accuracy on many photos
            SoftwareBitmap grayBitmap = SoftwareBitmap.Convert(bitmap, BitmapPixelFormat.Gray8);

            // Run OCR
            await RecognizeTextAsync(grayBitmap);
        }
    }

    static async Task RecognizeTextAsync(SoftwareBitmap bitmap)
    {
        // Create OCR engine (auto‑detect language)
        OcrEngine ocrEngine = OcrEngine.TryCreateFromUserProfileLanguages();

        if (ocrEngine == null)
        {
            Console.WriteLine("❌ Unable to create OCR engine. Ensure language packs are installed.");
            return;
        }

        // Perform recognition
        OcrResult result = await ocrEngine.RecognizeAsync(bitmap);

        // Output the extracted text
        Console.WriteLine("\n--- OCR Output ---");
        Console.WriteLine(result.Text);
        Console.WriteLine("--- End of Output ---\n");
    }
}
```

### Várt kimenet

Ha a `photo.webp` a „Hello, world! This is a test.” mondatot tartalmazza, akkor valami ilyesmit látsz majd:

```
--- OCR Output ---
Hello, world!
This is a test.
--- End of Output ---
```

A pontos sortörések a forráskép elrendezésétől függenek, de a **extract text from image** eredmény mindig egy egyszerű karakterlánc lesz, amelyet tovább feldolgozhatsz.

## Gyakori kérdések és külön esetek

### Működik ez más képformátumokkal is?

Természetesen. A használt dekóder (`BitmapDecoder`) automatikusan felismeri a JPEG, PNG, BMP, GIF, **WebP**, HEIF és további formátumokat. Így **WebP‑ból, JPEG‑ből vagy akár TIFF‑ből is olvashatsz szöveget** a kód módosítása nélkül.

### Mit tegyünk, ha az OCR motor alacsony bizalmat ad vissza?

Vizsgálhatod az `ocrResult.Lines`‑t és minden `OcrWord`‑t a `ConfidenceScore`‑ért. Ha a pontszám egy küszöb alatt van (pl. 0.6), fontold meg:
- A kép előfeldolgozását (kontraszt növelése, élesítés, kiegyenesítés).
- Magasabb felbontású forráskép használatát.
- Egy dedikált könyvtárra, például **Tesseract**‑ra való váltást a többnyelvű támogatáshoz.

### Hogyan kezeljünk több nyelvet egy képen?

Hozz létre külön `OcrEngine` példányokat minden nyelvhez, és futtasd őket sorban, vagy használj olyan könyvtárat, amely kevert nyelvű detektálást támogat. A beépített motor esetén átadhatsz egy `Language` objektumot:

```csharp
var spanishEngine = OcrEngine.TryCreateFromLanguage(new Language("es-ES"));
```

### Futtatható ez Linuxon/macOS‑on?

A `Windows.Media.Ocr` API csak Windowson érhető el. Nem‑Windows platformokon cseréld le az OCR részt **Tesseract**‑ra (`Tesseract.Net.SDK`‑val). A betöltési és előfeldolgozó kód változatlan marad, így a **c# OCR tutorial** többi része továbbra is alkalmazható.

## Pro tippek a jobb pontosságért

- **Resize** nagy képeket legfeljebb 2000 px-re a leghosszabb oldalon – az OCR motorok gyorsabban működnek közepes méreteken.
- **Denoise** egyszerű Gauss-elmosással, ha a fotó szemcsés.
- **Deskew** a bitmapet, ha a szöveg nem teljesen vízszintes; a `SoftwareBitmap` forgatható, mielőtt átadnád az `OcrEngine`‑nek.
- **Cache** az `OcrEngine` példányt, ha sok képet dolgozol fel egy kötegben; az ismételt létrehozás többletterhet jelent.

## Kapcsolódó témák, amiket érdemes felfedezni

- **Convert image to text** **Tesseract**‑tel cross‑platform projektekhez.
- **Extract text from PDF** úgy, hogy először minden oldalt képpé rendereljük.
- **Batch OCR**

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}