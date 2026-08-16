---
category: general
date: 2026-03-13
description: Hogyan hajtsunk végre OCR-t C#-ban, és nyerjünk ki szöveget képből az
  OcrEngine segítségével. Tanulja meg, hogyan konvertálja gyorsan a képet szöveggé
  egy teljes lépésről‑lépésre útmutatóval.
draft: false
keywords:
- how to perform OCR
- extract text from image
- convert image to text
- read text from picture
- how to extract text
language: hu
og_description: Hogyan végezzünk OCR-t C#-ban? Ez az útmutató megmutatja, hogyan lehet
  szöveget kinyerni egy képből, képet szöveggé konvertálni, és szöveget olvasni egy
  képről az OcrEngine segítségével.
og_title: Hogyan végezzünk OCR-t C#-ban – Szöveg kinyerése képből
tags:
- OCR
- C#
- Image Processing
title: Hogyan végezzünk OCR-t C#-ban – Szöveg kinyerése képből
url: /hu/net/text-recognition/how-to-perform-ocr-in-c-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan hajtsunk végre OCR-t C#-ban – Szöveg kinyerése képből

Az, hogy hogyan hajtsunk végre OCR-t C#-ban, gyakori kérdés a fejlesztők körében, akiknek **szöveget kell olvasniuk képfájlokból**. Ebben az útmutatóban végigvezetünk a képről szöveg kinyerésén a `OcrEngine` könyvtár segítségével, néhány sor kóddal a képeket kereshető karakterláncokká alakítva.  

Ha valaha is egy beolvasott számla, egy kézzel írt jegyzet vagy egy képernyőfotó előtt ültél, és azon tűnődtél, *„hogyan tudok szöveget kinyerni?”*, jó helyen vagy. Kitérünk arra is, hogyan konvertáljunk képet szöveggé kötegelt feldolgozáshoz, hogy automatizálhasd a teljes munkafolyamatot.

---

## Amire szükséged lesz

- **.NET 6.0 vagy újabb** (az általunk használt API a .NET Standard 2.0+ verzióval működik)
- A **OcrEngine** NuGet csomag (vagy bármely kompatibilis OCR könyvtár, amely elérhetővé teszi a `Language`, `Image`, `Recognize` és `Text` tulajdonságokat)
- Egy minta képfájl, például `hindi_page.jpg`, egy olyan mappában elhelyezve, amelyre a kódból hivatkozhatsz
- Alapvető C# szintaxis ismeret – nincs szükség haladó trükkökre

Ennyi. Nincs külső szolgáltatás, nincs API kulcs, csak egy helyi könyvtár, amely elvégzi a nehéz munkát.

---

## Lépésről‑lépésre megvalósítás

Alább a folyamatot logikai egységekre bontjuk. Minden szakasznak van egy egyértelmű címe, egy rövid kódrészlete, és egy magyarázat arra, **miért** fontos a lépés – nem csak **mit** csinál.

### Hogyan hajtsunk végre OCR-t – Alaplépések

Az általános folyamat öt műveletben összefoglalható:

1. **Create** egy OCR motor példányt
2. **Select** a nyelvet, amelyet fel szeretnél ismerni
3. **Load** a szöveget tartalmazó képet
4. **Run** a felismerési algoritmust
5. **Read** a kinyert szöveget

Ez a váz; a következő szakaszok részletezik.

---

### Szöveg kinyerése képből – Motor létrehozása

Először is szükségünk van egy objektumra, amely tud kommunikálni az OCR motorral.

```csharp
using System;
using OcrLibrary;   // Replace with the actual namespace of your OCR package

// Step 1: Create an OCR engine instance
OcrEngine ocrEngine = new OcrEngine();
```

*Miért fontos:* Az `OcrEngine` példányosítása lefoglalja az összes belső puffert és betölti a képelemzéshez szükséges natív DLL-eket. Ennek a lépésnek a kihagyása azt jelentené, hogy később nem lesz hívható felismerő.

> **Pro tipp:** Ha sok képet szeretnél egymás után feldolgozni, tartsd életben ugyanazt a `ocrEngine` példányt. Újra felhasználja a nyelvi modelleket és felgyorsítja a későbbi hívásokat.

---

### Kép konvertálása szöveggé – Válaszd ki a nyelvet

Az OCR pontossága erősen függ a használt nyelvi modelltől. Hindi, Tamil vagy bármely más írásrendszer esetén állítsd be ennek megfelelően a `Language` tulajdonságot.

```csharp
// Step 2: Select the language of the text to recognize (e.g., Hindi)
ocrEngine.Language = Language.Hindi;   // You can also use Language.Tamil, Language.English, etc.
```

*Miért fontos:* A motor nyelvspecifikus karakterkészleteket és statisztikai modelleket használ. A rossz nyelv megadása gyakran torz kimenetet eredményez, különösen a nem latin írásrendszerek esetén.

> **Különleges eset:** Ha többnyelvű támogatásra van szükséged, egyes könyvtárak lehetővé teszik egy tartaléklista beállítását, például `ocrEngine.Language = Language.Multilingual;`.

---

### Szöveg olvasása képből – Forráskép betöltése

Most a motorra mutatunk arra a fájlra, amely a vizuális szöveget tartalmazza.

```csharp
// Step 3: Load the image that contains the text
ocrEngine.Image = ImageStream.FromFile(@"C:\OCR\Samples\hindi_page.jpg");
```

*Miért fontos:* Az `ImageStream.FromFile` a nyers fájlt bitmap formátummá alakítja, amelyet az OCR mag megért. Hibás vagy nem támogatott formátum (például SVG) megadása kivételt okoz.

> **Figyelem:** A nagy képek sok memóriát fogyaszthatnak. Ha nagy felbontású beolvasásokat dolgozol fel, fontold meg a `Image.Resize` használatát a motorhoz való átadás előtt.

---

### Kép konvertálása szöveggé – Felismerés futtatása

Miután a motor készen áll és a kép betöltődött, végül meghívjuk az OCR folyamatot.

```csharp
// Step 4: Perform the OCR operation
ocrEngine.Recognize();
```

*Miért fontos:* A `Recognize` egy sor belső lépést indít el – előfeldolgozás, szegmentálás, karakterosztályozás és utófeldolgozás. A hívás blokkoló, vagyis a szál addig vár, amíg a szöveg készen nem áll.

> **Teljesítményjegyzet:** Egy tipikus asztali gépen egy 300 dpi oldal felismerése < 1 másodpercet vesz igénybe. Szerveren érdemes háttérfeladatban futtatni, hogy elkerüld a UI lefagyását.

---

### Hogyan nyerjünk ki szöveget – Az eredmény lekérése

Miután a felismerés befejeződik, a motor a `Text` tulajdonságban tárolja a nyers szöveges kimenetet.

```csharp
// Step 5: Output the recognized text
Console.WriteLine(ocrEngine.Text);
```

*Miért fontos:* A `Text` tulajdonság egy tiszta, UTF‑8 karakterláncot ad, amelyet fájlba írhatsz, adatbázisba táplálhatsz, vagy továbbadhatsz downstream NLP csővezetékeknek.

> **Várható kimenet:** A minta Hindi oldal esetén valami ilyesmit láthatsz  
> `यह एक उदाहरण पाठ है जो OCR द्वारा पहचाना गया है।`  
> (A pontos kimenet a kép minőségétől és a nyelvi modelltől függ.)

---

## További szempontok valós projektekhez

Az alábbiakban néhány „mi‑ha” szcenáriót találsz, amelyekkel valószínűleg szembe fogsz nézni, amikor **szöveget nyersz ki képből** a termelésben.

### Több kép kezelése ciklusban

Ha **képet kell szöveggé konvertálni** tucatnyi fájlhoz, csomagold a lépéseket egy `foreach` ciklusba, és használd újra ugyanazt a `ocrEngine`-t:

```csharp
string[] files = Directory.GetFiles(@"C:\OCR\Batch\", "*.jpg");
foreach (var file in files)
{
    ocrEngine.Image = ImageStream.FromFile(file);
    ocrEngine.Recognize();
    File.WriteAllText(Path.ChangeExtension(file, ".txt"), ocrEngine.Text);
}
```

### Alacsony minőségű beolvasások kezelése

- **Pre‑process** binarizálással (`Image.Binarize()`), zajeltávolítással vagy kiegyenesítéssel.
- **Increase DPI** a beolvasáskor (300 dpi egy biztonságos alapérték).
- **Choose a language model** amely támogatja a script ligatúráit (pl. Devanagari a Hindihez).

### Szöveg olvasása képből a weben

Amikor a kép egy URL-ről érkezik, először töltsd le egy memóriafolyamba:

```csharp
using (HttpClient client = new())
{
    byte[] data = await client.GetByteArrayAsync(imageUrl);
    using var ms = new MemoryStream(data);
    ocrEngine.Image = ImageStream.FromStream(ms);
    ocrEngine.Recognize();
    Console.WriteLine(ocrEngine.Text);
}
```

### Szálbiztonság és párhuzamosság

A legtöbb OCR könyvtár **nem** szálbiztos alapból. Ha **szöveget szeretnél olvasni képből** párhuzamosan, indíts külön `OcrEngine` példányokat szálanként, vagy használj producer‑consumer sort a hozzáférés sorosításához.

---

## Teljes működő példa

Mindent egybe rakva, itt egy kész‑a‑futtatni konzolos alkalmazás, amely bemutatja, hogyan **hajtsunk végre OCR-t**, **szöveget nyerjünk ki képből**, és **szöveget olvassunk képből** egy összefüggő programban.

```csharp
using System;
using OcrLibrary;               // Adjust to your OCR library's namespace
using System.IO;

class Program
{
    static void Main()
    {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Choose the language (Hindi in this case)
        ocrEngine.Language = Language.Hindi;

        // Load the image file
        string imagePath = @"C:\OCR\Samples\hindi_page.jpg";
        if (!File.Exists(imagePath))
        {
            Console.WriteLine($"Image not found: {imagePath}");
            return;
        }

        ocrEngine.Image = ImageStream.FromFile(imagePath);

        // Run the recognition process
        ocrEngine.Recognize();

        // Output the extracted text
        string result = ocrEngine.Text;
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(result);

        // Optional: Save to a .txt file
        string txtPath = Path.ChangeExtension(imagePath, ".txt");
        File.WriteAllText(txtPath, result);
        Console.WriteLine($"Text saved to {txtPath}");
    }
}
```

**Ami látnod kell:** A konzol kiírja a `hindi_page.jpg`-ból kinyert Hindi mondatot, majd egy megerősítést, hogy a szövegfájl létrejött. Ha a kép tiszta, a kimenet gyakorlatilag megegyezik az eredeti nyomtatott szöveggel.

---

## Következtetés

Most már tudod, hogyan **hajtsunk végre OCR-t** C#-ban az elejétől a végéig, hogyan **szöveget nyerjünk ki képből**, **képet konvertáljunk szöveggé**, és **szöveget olvassunk képből** egy egyszerű `OcrEngine` munkafolyamat segítségével. Az öt lépésből álló minta – létrehozás, nyelv beállítása, betöltés, felismerés, olvasás – lefedi a legtöbb felhasználási esetet, és a további tippek segítenek a kötegelt feladatok, alacsony minőségű beolvasások és web‑alapú források kezelésében.

Készen állsz a következő kihívásra? Próbáld meg a nyelvet angolra cserélni, egy PDF oldalt képként betáplálni, vagy az OCR kimenetet egy kereső‑index csővezetékbe láncolni. A lehetőségek határtalanok, ha már elsajátítottad az OCR alapjait C#-ban.

Van kérdésed vagy egy nehéz kép, ami nem működik? Írj egy megjegyzést alább, és oldjuk meg együtt. Boldog kódolást!  

![how to perform OCR example](images/ocr-example.png "how to perform OCR example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}