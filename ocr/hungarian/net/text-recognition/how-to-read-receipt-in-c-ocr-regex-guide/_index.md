---
category: general
date: 2026-02-13
description: Hogyan olvassunk be egy nyugtát gyorsan az Aspose OCR-rel, és vonjuk
  ki az összeget regex segítségével. Tanulja meg lépésről lépésre a nyugta OCR-rel
  történő feldolgozását.
draft: false
keywords:
- how to read receipt
- extract amount using regex
- regex find total
- process receipt with ocr
language: hu
og_description: Hogyan olvassunk le egy nyugtát C#-ban az Aspose OCR és regex segítségével.
  Ez az útmutató megmutatja, hogyan dolgozzuk fel a nyugtát OCR-rel, és hogyan nyerjük
  ki a teljes összeget.
og_title: Hogyan olvassunk be nyugtát C#‑ban – Teljes OCR és regex útmutató
tags:
- OCR
- C#
- Regex
- Aspose
title: Hogyan olvassuk be a nyugtát C#-ban – OCR + Regex útmutató
url: /hu/net/text-recognition/how-to-read-receipt-in-c-ocr-regex-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan olvassuk be a nyugtát C#‑ban – OCR + Regex útmutató

Gondolkodtál már azon, **hogyan olvass be nyugtákat** képekből anélkül, hogy minden sort kézzel beírnál? Sok kisvállalkozási alkalmazásban a nyugta fényképéről kell kinyerni a teljes összeget, és a kézi beírás aláássa az automatizálás célját. A jó hír? Az Aspose OCR segítségével a motor elvégezheti a nehéz munkát, majd egy egyszerű reguláris kifejezés megtalálja a végösszeget. Ebben az útmutatóban végigvezetünk a **process receipt with OCR** folyamaton, kinyerjük az összeget regex‑szel, és egy használatra kész végösszeggel zárunk.

Látni fogsz egy teljes, futtatható példát, megtudod, miért fontos a nyugta nyelvi modell, és tippeket kapsz a szélsőséges esetek kezelésére, például különböző pénznem szimbólumok vagy hiányzó „Total” címkék esetén. Külső dokumentumok nem szükségesek – minden, amire szükséged van, itt van.

## Mit fogsz megtanulni

- Hogyan állítsd be az Aspose OCR‑t nyugta‑specifikus felismeréshez (a `Receipt` nyelvi modell automatikusan kiegyenesíti és zajtalanítja a képet).  
- Hogyan alkalmazz egy reguláris kifejezést, amely **extract amount using regex** mintákat használ, és a legtöbb amerikai stílusú nyugtán működik.  
- Hogyan kezeld a gyakori változatokat, mint a „TOTAL”, „Total:”, vagy „Grand Total – $12.34”.  
- Hogyan jelenítsd meg az eredményt biztonságosan, és mit tegyél, ha a minta nem található.  

**Előfeltételek**: .NET 6+ (vagy .NET Framework 4.7+), érvényes Aspose OCR licenc vagy próba, valamint egy helyileg mentett nyugta kép. Ennyi – nincs extra NuGet csomag az Aspose.OCR‑n kívül.

---

## 1. lépés – Aspose OCR telepítése és a projekt előkészítése

### Miért fontos ez

Az Aspose OCR egy kifejezetten a **process receipt with OCR** feladatra épített modellt biztosít, amely tudja kiegyenesíteni a gyűrődött papírt és figyelmen kívül hagyni a háttérzajt. Az általános szövegmodell használata több hibát eredményez, különösen alacsony felbontású beolvasásoknál.

### Code

```csharp
// Install the package via NuGet first:
//   dotnet add package Aspose.OCR
using Aspose.OCR;
using Aspose.OCR.Enums;
using System.Text.RegularExpressions;

// If you have a license file, load it now (optional but removes trial watermark)
var license = new Aspose.OCR.License();
license.SetLicense("Aspose.OCR.lic");
```

> **Pro tipp:** Tartsd a licencfájlt a forráskód-kezelő mappádon kívül, hogy elkerüld a véletlen commit-okat.

---

## 2. lépés – Az OCR motor konfigurálása nyugta felismeréshez

### Miért fontos ez

A `Receipt` nyelvi modell beépített kiegyenesítést és zajcsökkentést tartalmaz, ami drámaian javítja a pontosságot a valós nyugtákon, amelyek gyakran hajtogatottak vagy gyűröttek.

### Code

```csharp
// Step 2: Create and configure the OCR engine for receipt processing
var ocrEngine = new OcrEngine
{
    // Receipt model is optimized for invoices, grocery receipts, etc.
    Language = OcrLanguage.Receipt
};
```

---

## 3. lépés – Szöveg felismerése a nyugta képről

### Miért fontos ez

A nyers szövegre van szükséged, mielőtt bármilyen regex‑et alkalmaznál. A `RecognizeImage` metódus egy `OcrResult`‑et ad vissza, amely tartalmazza a teljes karakterláncot, a bizalmi pontszámokat, és egyebeket, ha később szükséged van rá.

### Code

```csharp
// Step 3: Recognize text from the receipt image
// Replace the path with the actual location of your receipt file.
string receiptPath = @"C:\Receipts\sample-receipt.jpg";

OcrResult receiptResult = ocrEngine.RecognizeImage(receiptPath);

// Quick sanity check – print the whole OCR output (helps debugging)
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(receiptResult.Text);
Console.WriteLine("===================\n");
```

**Expected OCR output (example)**  
```
Walmart Supercenter
123 Main St.
Anytown, USA
Date: 02/12/2026
Item A   $3.45
Item B   $7.89
Subtotal $11.34
Tax      $0.91
Total:   $12.25
Thank you!
```

---

## 4. lépés – Regex felépítése az **Extract Amount Using Regex**-hez

### Miért fontos ez

A nyugták sokféle formátumban jelennek meg, de a „Total” (vagy egy közeli változat) szó, amelyet egy dollárösszeg követ, megbízható horgony. Az alábbi minta megengedi az opcionális szóközöket, kettőspontokat, kötőjeleket, és egy opcionális `$` jelet.

### Code

```csharp
// Step 4: Use a regular expression to locate the total amount in the recognized text
string pattern = @"Total\s*[:\-]?\s*\$?(\d+(\.\d{2})?)";
RegexOptions options = RegexOptions.IgnoreCase;

Match totalMatch = Regex.Match(receiptResult.Text, pattern, options);
```

**A minta magyarázata**

| Part | Meaning |
|------|---------|
| `Total` | A „Total” szót keresi (kis‑nagybetű érzéketlen). |
| `\s*[:\-]?` | Bármilyen szóközt enged, majd egy opcionális kettőspontot vagy kötőjelet. |
| `\s*\$?` | Opcionális szóköz és opcionális dollárjel. |
| `(\d+(\.\d{2})?)` | Egy vagy több számjegyet rögzít, opcionálisan egy tizedesjeggyel és két centtel. |

---

## 5. lépés – Kinyert összeg kiírása vagy hiányzó adatok kezelése

### Miért fontos ez

Még a legjobb OCR is kihagyhat egy szót, különösen a homályos nyugtákon. Egy elegáns visszaesés biztosítása megakadályozza a leállásokat, és lehetőséget ad egyedi logikához (pl. a felhasználó megerősítésének kérése).

### Code

```csharp
// Step 5: Output the extracted total, or indicate it wasn't found
if (totalMatch.Success)
{
    string amount = totalMatch.Groups[1].Value;
    Console.WriteLine($"Total: ${amount}");
}
else
{
    Console.WriteLine("Total amount not found. Consider reviewing the OCR output manually.");
}
```

**Sample console output**

```
Total: $12.25
```

---

## Teljes működő példa – Minden lépés egy fájlban

Az alábbi egy önálló program, amelyet egyszerűen beilleszthetsz egy konzolos projektbe. Tartalmaz megjegyzéseket, hibakezelést és az opcionális licenc betöltését.

```csharp
// ---------------------------------------------------------------
// How to Read Receipt in C# – OCR + Regex (Complete Example)
// ---------------------------------------------------------------
using Aspose.OCR;
using Aspose.OCR.Enums;
using System;
using System.Text.RegularExpressions;

class Program
{
    static void Main()
    {
        // 0️⃣ Optional: Load your Aspose OCR license (remove trial watermark)
        try
        {
            var license = new Aspose.OCR.License();
            license.SetLicense("Aspose.OCR.lic"); // path to .lic file
        }
        catch (Exception ex)
        {
            Console.WriteLine("License not found – running in trial mode.");
        }

        // 1️⃣ Configure the OCR engine for receipt processing
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.Receipt // receipt model = de‑skew + de‑noise
        };

        // 2️⃣ Path to the receipt image (change to your file)
        string receiptPath = @"YOUR_DIRECTORY/receipt.jpg";

        // 3️⃣ Perform OCR
        OcrResult receiptResult = ocrEngine.RecognizeImage(receiptPath);

        // 4️⃣ Debug: show full OCR text (helps when regex fails)
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(receiptResult.Text);
        Console.WriteLine("===================\n");

        // 5️⃣ Regex to **extract amount using regex** (find the total)
        string pattern = @"Total\s*[:\-]?\s*\$?(\d+(\.\d{2})?)";
        Match totalMatch = Regex.Match(receiptResult.Text, pattern,
                                        RegexOptions.IgnoreCase);

        // 6️⃣ Output
        if (totalMatch.Success)
        {
            string amount = totalMatch.Groups[1].Value;
            Console.WriteLine($"Total: ${amount}");
        }
        else
        {
            Console.WriteLine("Total amount not found. You might need to adjust the regex or improve image quality.");
        }
    }
}
```

**A program futtatása**

1. Hozz létre egy új konzolos projektet (`dotnet new console -n ReceiptReader`).  
2. Add hozzá az Aspose.OCR NuGet csomagot (`dotnet add package Aspose.OCR`).  
3. Cseréld le a `YOUR_DIRECTORY/receipt.jpg`‑t a nyugta kép tényleges elérési útjára.  
4. Buildeld és futtasd (`dotnet run`).  

A képernyőn látnod kell az OCR kimenetet, majd a `Total: $xx.xx` sort, ha minden megfelelően működik.

---

## Szélsőséges esetek és gyakori változatok kezelése

### 1. Különböző pénznem szimbólumok

Ha euróval (€) vagy fonttal (£) dolgozol, bővítsd a mintát:

```csharp
string pattern = @"Total\s*[:\-]?\s*[$€£]?\s*(\d+(\.\d{2})?)";
```

### 2. Hiányzó „Total” címke

Néhány nyugta csak a „Grand Total” feliratot tartalmazza. Adj hozzá egy alternatívát:

```csharp
string pattern = @"(?:Total|Grand\s*Total)\s*[:\-]?\s*[$]?\s*(\d+(\.\d{2})?)";
```

### 3. Több összeg (pl. „Subtotal” és „Total”)

Ha a regex az első előfordulást találja, lehet, hogy a **utolsó** egyezést szeretnéd:

```csharp
MatchCollection matches = Regex.Matches(receiptResult.Text, pattern,
                                         RegexOptions.IgnoreCase);
Match last = matches.Count > 0 ? matches[matches.Count - 1] : null;
```

### 4. Alacsony felbontású képek

- Növeld a DPI‑t a beolvasáskor (`300 DPI` egy jó érték).  
- Előfeldolgozd a képet egy egyszerű elmosódás‑csökkentő szűrővel, mielőtt az Aspose‑nak adnád (az útmutató keretein kívül, de érdemes kipróbálni).

---

## Pro tippek valós projektekhez

- **Cache‑eld az OCR eredményt**, ha több mezőt (adó, tételek stb.) kell kinyerned – az OCR költséget csak egyszer fizeted.  
- **Logold a nyers OCR szöveget** egy adatbázisba; ez értékes audit nyomot biztosít vitatott költségekhez.  
- Web API építésekor **futtasd az OCR‑t háttérszálon**; néhány száz milliszekundumot vehet igénybe, ami aszinkron módon rendben van, de szinkron kérésnél nem ideális.  
- **Érvényesítsd a kinyert összeget** az üzleti szabályokkal (pl. az összegnek > 0‑nak kell lennie) mielőtt tárolnád.

---

## Összegzés

Áttekintettük, hogyan **read receipt** képeket olvassunk be C#‑ban az Aspose OCR segítségével, majd **extract amount using regex**‑szal megbízhatóan megtaláljuk a végösszeg sort. A `Receipt` nyelvi modell használatával kiegyenesített, zajtalanított szöveget kapsz, és egy tömör reguláris kifejezés kezeli a formázási sajátosságok nagy részét. A fenti teljes kódrészlet készen áll bármely .NET konzol vagy szolgáltatás projektbe való beillesztésre, és a további szélsőséges esetekre vonatkozó javaslatok szilárd alapot adnak a termeléshez.

Készen állsz a következő lépésre? Próbáld meg bővíteni a megoldást, hogy egyedi tételeket vonjon ki, automatikusan számolja a adót, vagy integrálja egy költségkövető API‑val. És ha olyan nyugtával találkozol, amely megtöri a mintát, ne feledd, hogy a **regex find total** megközelítés csak egy kiindulópont – a mintát mindig módosíthatod a saját területedhez.

Boldog kódolást, és legyen a nyugta‑feldolgozásod gyors, pontos és teljesen automatizált!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}