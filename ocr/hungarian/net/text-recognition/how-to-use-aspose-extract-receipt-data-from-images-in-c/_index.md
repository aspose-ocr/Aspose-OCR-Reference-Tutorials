---
category: general
date: 2026-04-04
description: Ismerje meg, hogyan használja az Aspose-t a nyugták adatainak kinyeréséhez,
  a nyugta képének betöltéséhez és a nyugta képének OCR-hez egy teljes C# példával.
  Lépésről lépésre útmutató fejlesztőknek.
draft: false
keywords:
- how to use aspose
- extract receipt data
- how to extract receipt
- load receipt image
- ocr receipt image
language: hu
og_description: Hogyan használjuk az Aspose-t a nyugták adatinak kinyerésére beolvasott
  nyugta képből. Teljes C# kód, magyarázatok és tippek az OCR nyugta kép feldolgozásához.
og_title: Az Aspose használata – Nyugtaadatok kinyerése képekből
tags:
- Aspose
- OCR
- C#
- Receipt Processing
title: Hogyan használjuk az Aspose-t – Nyugtaadatok kinyerése képekből C#-ban
url: /hu/net/text-recognition/how-to-use-aspose-extract-receipt-data-from-images-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan használjuk az Aspose‑t – Számlaadatok kinyerése képekből C#‑ban

Gondolkodtál már azon, **hogyan használjuk az Aspose‑t**, hogy strukturált információkat nyerjünk ki egy nyugta fényképéből? Nem vagy egyedül. Akár költségkövető alkalmazást építesz, akár számlabevitelt automatizálsz, a probléma ugyanaz: van egy PNG vagy JPEG, és a kereskedő neve, a dátum és a végösszeg szükséges manuális gépelés nélkül.

A lényeg, hogy az Aspose.OCR ezt a teljes folyamatot egy könnyed feladattá varázsolja. Ebben az útmutatóban végigvezetünk egy nyugta kép betöltésén, az OCR futtatásán, majd a nyugta adatainak kinyerésén néhány C# sorral. A végére egy futtatható konzolprogramod lesz, amely a kereskedő nevét, a dátumot és a végösszeget közvetlenül a konzolra írja.

> **Gyors megoldás:** Ha csak a kódra van szükséged, ugorj a „Teljes működő példa” szekcióra az alján, és másold be.

## Amire szükséged lesz

- **.NET 6.0 vagy újabb** (az API működik .NET Core‑dal és .NET Framework‑kel)
- **Aspose.OCR for .NET** NuGet csomag (`Install-Package Aspose.OCR`)
- Egy minta nyugta kép (PNG, JPG vagy BMP), helyileg mentve
- Visual Studio 2022 vagy bármely szerkesztő, amely támogatja a C# projekteket

Más harmadik féltől származó könyvtár nem szükséges. Az egyetlen előfeltétel a C# konzolalkalmazások alapvető ismerete – ha már írtál „Hello World” programot, készen állsz.

## 1. lépés – Aspose.OCR telepítése és hivatkozása

Ahhoz, hogy **hogyan használjuk az Aspose‑t**, először a könyvtárra van szükség a projektedben. Nyisd meg a Package Manager Console‑t, és futtasd:

```powershell
Install-Package Aspose.OCR
```

Alternatívaként használhatod a NuGet UI‑t, és keresd a „Aspose.OCR” kifejezést. A telepítés után add hozzá a szükséges névtereket a fájlod tetejéhez:

```csharp
using Aspose.OCR;
using Aspose.OCR.Structured;
```

> **Pro tipp:** Tartsd naprakészen a NuGet csomagjaidat. 2026. április állása szerint a legújabb stabil verzió a 23.11.0, amely teljesítményjavításokat tartalmaz a nagy felbontású nyugták OCR‑jéhez.

## 2. lépés – Nyugta kép betöltése

Amikor **nyugta képet töltesz be**, két gyakori forrásod lehet: egy helyi útvonal vagy egy webkérésből származó stream. Ebben a tutorialban egyszerűen leolvassuk a lemezről:

```csharp
// Step 2: Load the receipt image to be processed
var ocrEngine = new OcrEngine
{
    Language = Language.English // set language for better accuracy
};

ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/receipt.png");
```

Cseréld le a `YOUR_DIRECTORY/receipt.png`‑t a nyugta fájlod tényleges útvonalára. Ha felhasználói feltöltésekkel dolgozol, egy `MemoryStream`‑et adhatunk át a `ImageStream.FromStream`‑nek.

> **Miért fontos:** A nyelv (English) megadása azt mondja az OCR motornak, milyen karakterkészletet várjon, ezáltal csökkentve a hibás felismeréseket – különösen fontos, amikor **ocr receipt image**‑t futtatsz, amely számokat és szimbólumokat tartalmaz.

## 3. lépés – OCR futtatása és elrendezési információk rögzítése

Az OCR lépés nem csak nyers szöveget ad vissza; a layoutot is rögzíti, ami később a strukturált kinyeréshez elengedhetetlen.

```csharp
// Step 3: Run OCR to generate text and layout information (required for structured extraction)
ocrEngine.Recognize();
```

A `Recognize()` befejezése után az `ocrEngine` tartalmazza a sima szöveget és minden szó pozíciós adatait. Ez a kiindulópont a következő lépéshez, ahol az Aspose‑t megkérdezzük, **hogyan lehet nyugtából kinyerni** a mezőket automatikusan.

## 4. lépés – Layout Recognizer inicializálása

Az Aspose egy `LayoutRecognizer` osztályt biztosít, amely tudja, hogyan vannak általában felépítve a nyugták (kereskedő felül, dátumsor, összeg alul). Egyszerűen átadod a konfigurált OCR motorodat:

```csharp
// Step 4: Initialize the layout recognizer with the OCR engine
var layoutRecognizer = new LayoutRecognizer(ocrEngine);
```

A háttérben a recognizer egy sor heurisztikát alkalmaz – például pénznem szimbólumok vagy dátumminták keresését – hogy a nyers szöveget szemantikus mezőkhöz rendelje.

## 5. lépés – Strukturált nyugta adatok kinyerése

Most jön a legizgalmasabb rész: **nyugta adatok kinyerése**. Egy metódushívás elvégzi a nehéz munkát:

```csharp
// Step 5: Extract structured receipt data (merchant, date, total amount)
var receiptData = layoutRecognizer.ExtractReceiptData();
```

A `receiptData` egy `ReceiptData` típusú objektum (`Aspose.OCR.Structured`‑ban definiálva). Három fő tulajdonsága van:

- `Merchant` – a bolt neve
- `Date` – a vásárlás dátuma `DateTime`‑ként (ha felismerték)
- `TotalAmount` – a végösszeg `decimal`‑ként

Ha a motor nem talál egy adott mezőt, a tulajdonság `null` vagy `0` lesz. Szükség esetén hozzáadhatsz visszaeső logikát (pl. felhasználói megerősítés kérése).

## 6. lépés – Kinyert információk megjelenítése

Végül írd ki az eredményeket a konzolra. Itt látod a munkád gyümölcsét:

```csharp
// Step 6: Display the extracted information
Console.WriteLine($"Merchant: {receiptData.Merchant}");
Console.WriteLine($"Date:     {receiptData.Date:d}");
Console.WriteLine($"Total:    {receiptData.TotalAmount:C}");
```

A formátum stringek (`:d` és `:C`) rövid dátumot és pénznem formátumú szöveget állítanak elő, így az output emberi olvasásra alkalmas.

### Várható kimenet

Tegyük fel, hogy a nyugta a „Coffee Corner”‑hez tartozik, 2025‑12‑01‑én kiállított, és a végösszeg 4,75 $. Ebben az esetben a konzol a következőt mutatja:

```
Merchant: Coffee Corner
Date:     12/1/2025
Total:    $4.75
```

Ha valamelyik mező hiányzik, egy üres sor vagy alapértelmezett érték jelenik meg – tökéletes hibakereséshez.

## Szélsőséges esetek és gyakori hibák

### 1. Alacsony felbontású képek
Ha a nyugta kép elmosódott vagy kevesebb, mint 150 dpi, az OCR pontossága drámaian csökken. A kép egyszerű bilineáris szűrővel történő felméretezése az Aspose‑nak előzetesen javíthatja az eredményeket.

```csharp
ocrEngine.Image = ImageStream.FromFile("receipt.png")
    .Resize(2.0, InterpolationMode.Bilinear);
```

### 2. Nem‑angol nyugták
Az első példában a `Language.English` van használva. Többnyelvű nyugták esetén állítsd a `Language`‑t a megfelelő enumra (pl. `Language.French`), vagy használd a `Language.AutoDetect`‑et, ha nem vagy biztos benne.

### 3. Több nyugta egy képen
Az Aspose layout recognizer egyetlen nyugtát vár képenként. Ha több nyugta van egymás mellett egy fotón, először elő kell dolgozni a képet – minden nyugtát külön fájlba kell vágni, mielőtt az OCR‑t futtatnád.

### 4. Hiányzó pénznem szimbólum
Néha a végösszeg `$` jel nélkül jelenik meg. A recognizer még mindig fel tudja ismerni a számokat, de előfordulhat, hogy utófeldolgozással kell biztosítani a helyes tizedes elválasztást.

```csharp
if (receiptData.TotalAmount == 0 && rawText.Contains("Total"))
{
    // fallback parsing logic here
}
```

## Pro tippek termeléshez

- **Cache‑eld az OCR motort**, ha sok nyugtát dolgozol fel egy kötegben; ugyanazt az instance‑t újra‑használva csökkentheted a memóriafoglalást.
- **Logold a nyers OCR szöveget** (`ocrEngine.Text`) audit célokra. Hasznos, ha egy mező nem kerül kinyerésre.
- **Tedd a teljes folyamatot try/catch‑be**, és jeleníts meg felhasználóbarát hibaüzenetet (pl. „Nem sikerült beolvasni a nyugtát, kérlek tölts fel tisztább képet”).

## Teljes működő példa

Az alábbi önálló konzolalkalmazás közvetlenül lefordítható és futtatható. Csak cseréld le a kép útvonalát, és már indulhat is.

```csharp
// ------------------------------------------------------------
// How to Use Aspose – Extract Receipt Data from Images (C#)
// ------------------------------------------------------------
using System;
using Aspose.OCR;
using Aspose.OCR.Structured;

namespace ReceiptExtractor
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create and configure the OCR engine for English language
            var ocrEngine = new OcrEngine
            {
                Language = Language.English
            };

            // 2️⃣ Load the receipt image you want to process
            // 👉 Make sure the file exists; otherwise an exception will be thrown.
            const string imagePath = "YOUR_DIRECTORY/receipt.png";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // 3️⃣ Run OCR – this also captures layout information
            ocrEngine.Recognize();

            // 4️⃣ Initialize the layout recognizer with the OCR engine
            var layoutRecognizer = new LayoutRecognizer(ocrEngine);

            // 5️⃣ Extract structured receipt data (merchant, date, total amount)
            var receiptData = layoutRecognizer.ExtractReceiptData();

            // 6️⃣ Display the extracted information
            Console.WriteLine($"Merchant: {receiptData.Merchant ?? "Not detected"}");
            Console.WriteLine($"Date:     {(receiptData.Date == DateTime.MinValue ? "Not detected" : receiptData.Date.ToShortDateString())}");
            Console.WriteLine($"Total:    {(receiptData.TotalAmount == 0 ? "Not detected" : receiptData.TotalAmount.ToString("C"))}");

            // Keep the console window open when debugging
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**A kód futtatása**

1. Hozz létre egy új .NET konzolprojektet (`dotnet new console -n ReceiptExtractor`).
2. Add hozzá az Aspose.OCR csomagot (`dotnet add package Aspose.OCR`).
3. Cseréld le a generált `Program.cs`‑t a fenti kódrészlettel.
4. Helyezz el egy nyugta képet a megadott útvonalon.
5. Építsd és futtasd (`dotnet run`).

A konzol a kereskedő nevét, a dátumot és a végösszeget pontosan úgy fogja kiírni, ahogy korábban bemutattuk.

## Összegzés

Ebben az útmutatóban bemutattuk, **hogyan használjuk az Aspose‑t** a **nyugta kép betöltésére**, az **ocr receipt image** futtatására, és végül a **receipt data** kinyerésére néhány sor kóddal. A fő tanulság, hogy az Aspose.OCR elvégzi a nehéz munkát – miután az OCR motort beállítottad, a `LayoutRecognizer` a nyers szöveget egy megbízható strukturált objektummá alakítja.

Mi a következő lépés? Tárold a kinyert értékeket egy adatbázisban, generálj PDF nyugta összefoglalót, vagy akár egy gépi tanulási modellt használj a költségkategorizáláshoz. Kísérletezhetsz más strukturált dokumentumtípusokkal is, mint például számlák vagy szállítási címkék – az Aspose `ExtractInvoiceData` funkciója nagyon hasonló módon működik.

Van kérdésed a szélsőséges esetekkel kapcsolatban, vagy szeretnéd látni, hogyan kezelj többoldalas PDF‑eket? Írj kommentet, vagy nézd meg az hivatalos Aspose.OCR dokumentációt a haladó szcenáriókhoz. Boldog kódolást, és élvezd az **hogyan használjuk az Aspose‑t** nyújtotta egyszerűséget a nyugta automatizálásban!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}