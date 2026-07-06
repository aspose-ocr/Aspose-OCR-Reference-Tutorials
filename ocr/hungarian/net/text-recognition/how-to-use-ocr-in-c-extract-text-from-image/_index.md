---
category: general
date: 2026-03-05
description: Hogyan használjunk OCR-t C#-ban a képről szöveg kinyeréséhez. Tanulja
  meg, hogyan alakítsa a képet szöveggé, hogyan olvassa a koreai karaktereket, és
  hogyan töltse be a képet az OCR-hez gyorsan.
draft: false
keywords:
- how to use OCR
- extract text from image
- convert image to text
- read korean characters
- load image for OCR
language: hu
og_description: Hogyan használjunk OCR-t C#-ban, és azonnal nyerjünk ki szöveget a
  képből. Ez az útmutató megmutatja, hogyan konvertáljunk képet szöveggé, hogyan olvassuk
  a koreai karaktereket, és hogyan töltsünk be képet az OCR-hez.
og_title: Hogyan használjunk OCR-t C#-ban – Szöveg kinyerése képből
tags:
- OCR
- C#
- Aspose
title: Hogyan használjuk az OCR-t C#-ban – Szöveg kinyerése képből
url: /hu/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan használjuk az OCR-t C#‑ban – Szöveg kinyerése képből

Gondolkodtál már azon, **hogyan használjuk az OCR‑t**, amikor egy képernyőképen koreai szöveg van, és a tiszta karakterláncot szeretnéd visszakapni? Nem vagy egyedül ezzel a problémával. Ebben az útmutatóban egy teljes, azonnal futtatható példán keresztül mutatjuk be, hogyan **nyerünk ki szöveget képből**, **alakítunk képet szöveggé**, és még azt is, hogyan **olvassuk el a koreai karaktereket** az Aspose.OCR segítségével.

Kitérünk a gyakran figyelmen kívül hagyott **kép betöltése OCR‑hez** lépésre is, hogy ne érjen meglepetésként a „fájl nem található” hiba később. A végére egy önálló programot kapsz, amelyet bármely .NET projektbe beilleszthetsz.

## Amire szükséged lesz

- .NET 6+ (vagy .NET Framework 4.7.2 és újabb) – a kód mindkettőn működik.
- Aspose.OCR for .NET – a próbaverzió letölthető az Aspose weboldaláról.
- Egy minta kép (`korean_doc.png`), amely koreai szöveget tartalmaz.
- Kedvenc IDE‑d (Visual Studio, Rider, VS Code – bármi, ami tetszik).

Más harmadik féltől származó könyvtárra nincs szükség.

## 1. lépés: Projekt létrehozása és az Aspose.OCR hozzáadása

Először hozz létre egy új konzolalkalmazást:

```bash
dotnet new console -n OcrDemo
cd OcrDemo
```

Ezután add hozzá az Aspose.OCR NuGet csomagot:

```bash
dotnet add package Aspose.OCR
```

> **Pro tipp:** Ha van licencfájlod, helyezd a projekt gyökerébe; különben a ingyenes próba működik, de vízjelet ad a kimenethez.

## 2. lépés: Hogyan használjuk az OCR‑t – Motor inicializálása

Most megírjuk a C# kódot. Az első dolog, amikor **hogyan használjuk az OCR‑t**, hogy példányosítjuk a `OcrEngine`‑t. Ez az objektum a könyvtár szíve; tartalmazza az összes beállítást, amelyre később szükséged lesz.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 2: Initialize the OCR engine
            var ocrEngine = new OcrEngine();

            // Optional: apply your license to remove trial limitations
            // Replace the path with the actual location of your .lic file
            ocrEngine.SetLicense("YOUR_DIRECTORY/Aspose.OCR.lic");
```

**Miért fontos:** Megfelelő motorpéldány nélkül nem állíthatod be a nyelvet, nem tölthetsz be képeket, és nem kérheted le az eredményeket. A motor kezeli a belső erőforrásokat is, így egyszer létrehozni és újrahasználni hatékonyabb, mint minden alkalommal új objektumot létrehozni.

## 3. lépés: Nyelv kiválasztása – Koreai karakterek olvasása

A következő sor megmondja a motornak, melyik nyelvet keresse. Mivel a cél **koreai karakterek olvasása**, beállítjuk a `OcrLanguage.Korean`‑t. Cserélheted arabra, thaira, gujaratira stb., a felhasználási esetnek megfelelően.

```csharp
            // Step 3: Tell the engine which language to recognize
            ocrEngine.Language = OcrLanguage.Korean; // alternatives: Arabic, Thai, Gujarati, etc.
```

**Miért lényeges:** A nyelvválasztás drámaian javítja a pontosságot. Az OCR motor nyelvspecifikus szótárakat és karaktermodelleket használ; ha rossz nyelvet adsz meg, torz kimenetet kaphatsz.

## 4. lépés: Kép betöltése OCR‑hez – Kép átalakítása szöveggé

Mielőtt a motor bármit is tenne, **kép betöltése OCR‑hez** szükséges. Az `ImageStream.FromFile` metódus beolvassa a fájlt egy olyan formátumba, amelyet a motor ért.

```csharp
            // Step 4: Load the image that contains the text
            ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/korean_doc.png");
```

Ha a kép más mappában van, egyszerűen módosítsd az elérési utat. Ne felejtsd el a fájl *Build Action* beállítását „Copy if newer”‑re, hogy a futtatáskor megtalálja a végrehajtható.

> **Gyakori hiba:** Ha a karakterláncban visszaperjeleket (`\`) használsz escape‑elés nélkül, fordítási hibát kapsz. Használj dupla visszaperjeleket (`\\`) vagy verbatim stringet (`@"C:\path\file.png"`).

## 5. lépés: OCR végrehajtása – Szöveg kinyerése képből

Most jön a nehéz munka. A `Recognize()` hívás lefuttatja az OCR algoritmust, a `Text` tulajdonság pedig visszaadja a nyers karakterláncot.

```csharp
            // Step 5: Run OCR and get the recognized text
            string recognizedText = ocrEngine.Recognize().Text;
```

Ekkor már **kinyerted a szöveget a képből**, vagyis **kép‑szöveg átalakítást** hajtottál végre. Az eredmény tartalmazhat sortöréseket, ha az eredeti elrendezés sorokkal rendelkezett.

## 6. lépés: Eredmény megjelenítése – Kimenet ellenőrzése

Végül írjuk ki az eredményt a konzolra, hogy ellenőrizhesd, működik‑e.

```csharp
            // Step 6: Output the result to the console
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(recognizedText);
        }
    }
}
```

Futtasd a programot:

```bash
dotnet run
```

### Várt kimenet

```
=== Recognized Text ===
안녕하세요. 이것은 OCR 테스트 문서입니다.
```

Ha koreai karaktereket látsz, amelyek hasonlítanak a képen lévőkre, gratulálok – elsajátítottad a **hogyan használjuk az OCR‑t** az Aspose.OCR‑val!

![OCR használati példadiagram](image.png)

*Kép alternatív szöveg: OCR használati példadiagram, amely bemutatja a folyamatot a kép betöltésétől a felismert szöveg kiírásáig.*

## Szélsőséges esetek és variációk

### 1. Több oldal kezelése

Ha **kép‑szöveg átalakítást** szeretnél végezni olyan fájlokkal, amelyek több oldalt tartalmaznak (pl. többoldalas TIFF), akkor iterálj minden oldal felett, és hívd meg a `Recognize()`‑t minden egyes `ImageStream` példányra.

### 2. Alacsony minőségű beolvasások kezelése

Az alacsony felbontású képek csökkenthetik a pontosságot. A `Recognize()` hívása előtt javíthatod a képet az Aspose előfeldolgozó eszközeivel:

```csharp
ocrEngine.Image = ImageProcessing.Preprocess(ocrEngine.Image, ImageProcessingOptions.Deskew);
```

### 3. Nyelvek dinamikus váltása

Tegyük fel, hogy vegyes nyelvű dokumentumod van. A `ocrEngine.Language` értékét a felismerések között módosíthatod:

```csharp
ocrEngine.Language = OcrLanguage.English;
string english = ocrEngine.Recognize().Text;

ocrEngine.Language = OcrLanguage.Korean;
string korean = ocrEngine.Recognize().Text;
```

### 4. Eredmény mentése fájlba

Ha **kép‑szöveg átalakítást** szeretnél, és a szöveget fájlba szeretnéd menteni, egyszerűen írd ki a karakterláncot egy `.txt` fájlba:

```csharp
System.IO.File.WriteAllText("output.txt", recognizedText);
```

## Gyakran ismételt kérdések

- **Szükségem van licencre a kód futtatásához?**  
  Nem. A ingyenes próba megfelelő kísérletezéshez, de vízjelet ad a kimenethez. A megvásárolt licenc eltávolítja a vízjelet és teljes teljesítményt biztosít.

- **Futtatható-e Linuxon?**  
  Természetesen. Az Aspose.OCR platformfüggetlen; csak győződj meg róla, hogy a szükséges natív függőségek (pl. libgdiplus a .NET Core‑hoz Linuxon) telepítve vannak.

- **Mi van, ha a kép egy stream‑ben van, nem fájlban?**  
  Használd az `ImageStream.FromStream(yourStream)`‑t – az API bármely `System.IO.Stream`‑et elfogad.

## Következtetés

Lépésről lépésre végigvezettünk a **hogyan használjuk az OCR‑t** C#‑ban a **szöveg kinyeréséhez képből**, a **kép‑szöveg átalakításhoz**, és a **koreai karakterek olvasásához**, miközben megfelelően **betöltöttük a képet OCR‑hez**. A fenti, teljesen futtatható példa önmagában működik, az extra tippek pedig útmutatót adnak a fejlettebb forgatókönyvekhez.

Készen állsz a következő kihívásra? Próbálj ki más nyelvet, dolgozz PDF‑ek oldalanként, vagy integráld az OCR hívást egy web‑API‑ba, hogy a felhasználók képeket tölthessenek fel és azonnal megkapják a szöveget. A lehetőségek végtelenek, és most már szilárd alapokkal rendelkezel a további fejlesztéshez.

Boldog kódolást!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}