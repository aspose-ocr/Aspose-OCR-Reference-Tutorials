---
category: general
date: 2026-02-20
description: Naučte se, jak číst účtenku v C# extrahováním textu z obrázku a převodem
  do JSON. Krok za krokem kód pomocí Aspose OCR.
draft: false
keywords:
- how to read receipt
- extract text from image
- convert image to json
- load image file c#
- OCR receipt C#
- Aspose OCR tutorial
language: cs
og_description: Objevte, jak číst účtenku v C# načtením souboru s obrázkem, extrahováním
  textu pomocí Aspose OCR a převodem výsledku do JSON. Kompletní ukázkový kód.
og_title: Jak číst potvrzení v C# – Extrahovat text, převést na JSON
tags:
- C#
- OCR
- Image Processing
- JSON
title: Jak číst účtenku v C# – Kompletní průvodce extrakcí textu z obrázku
url: /cs/net/text-recognition/how-to-read-receipt-in-c-complete-guide-to-extract-text-from/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak číst účtenku v C# – Kompletní průvodce

Už jste se někdy zamýšleli **jak číst účtenky** z obrázků programově? Možná vytváříte aplikaci pro sledování výdajů a potřebujete získat položky z fotografie nákupní účtenky. Z mé zkušenosti je největší problém převést rozmazaný JPEG na strukturovaná data, která můžete skutečně použít. Dobrá zpráva? Několik řádků C# a Aspose OCR vám umožní **extrahovat text z obrázku**, pak **převést obrázek na JSON** téměř magickým způsobem.

V tomto tutoriálu získáte připravené řešení, které **načte soubor obrázku C#**, spustí OCR a vypíše podrobný JSON payload. Žádné externí služby, žádné zdlouhavé REST volání — jen čistý .NET kód, který můžete vložit do libovolného konzolového nebo ASP.NET projektu. Na konci pochopíte, proč je každý krok důležitý, jak řešit běžné hraniční případy (např. neobvyklé velikosti účtenek) a jak vypadá výstupní JSON.

## Co budete potřebovat

- **.NET 6.0 nebo novější** — kód používá `System.Drawing.Common`, který je podporován na Windows, Linuxu i macOS.
- **Aspose.OCR pro .NET** — můžete si stáhnout bezplatnou zkušební NuGet balíček (`Aspose.OCR`) nebo použít licencovanou verzi, pokud ji máte.
- **Ukázkový obrázek účtenky** (`receipt.jpg`) umístěný někde, kde ho aplikace dokáže přečíst.
- Jakékoliv IDE podle vašeho výběru (Visual Studio, Rider, VS Code).  

To je vše. Žádná další konfigurace, žádné API klíče.

---

## Krok 1 – Načtení souboru obrázku C# (Primární klíčové slovo v akci)

Než OCR engine může udělat své kouzlo, musíte obrázek načíst do paměti. Toto je klasický krok „load image file C#“, který mnohým vývojářům uniká.

```csharp
using System.Drawing;          // Required for Image
using Aspose.OCR;
using Aspose.OCR.Models;

// Path to your receipt image – adjust as needed
string imagePath = @"C:\Receipts\receipt.jpg";

// Load the image into a System.Drawing.Image object
Image receiptImage = Image.FromFile(imagePath);
```

**Proč je to důležité:**  
`Image.FromFile` načte soubor *jednou* a ponechá otevřený handle, což je ideální pro rychlý OCR průchod. Pokud zpracováváte mnoho účtenek ve smyčce, zvažte použití `Image.FromStream`, abyste se vyhnuli zamykání souboru.

> **Tip:** Pokud narazíte na *FileNotFoundException*, zkontrolujte cestu a ujistěte se, že obrázek skutečně existuje. Relativní cesty fungují také (`"./receipt.jpg"`), ale absolutní cesty jsou pro produkční úlohy bezpečnější.

---

## Krok 2 – Vytvoření a konfigurace OCR engine

Aspose OCR přichází s připraveným `OcrEngine`. Nemusíte trénovat model; knihovna už umí číst tištěný text, což je přesně to, co většina účtenek používá.

```csharp
// Instantiate the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Optional: tweak recognition settings if your receipts are low‑contrast
ocrEngine.Config.Language = OcrLanguage.English;
ocrEngine.Config.DetectOrientation = true;   // Handles rotated receipts
```

**Proč nastavujeme tyto možnosti:**  
`DetectOrientation` říká engine, aby automaticky otočil obrázek, pokud byla účtenka naskenována vzhůru nohama. Nastavení jazyka zužuje množinu znaků, což může zlepšit přesnost — zejména když potřebujete jen anglická alfanumerická data.

---

## Krok 3 – Rozpoznání obrázku a převod na JSON

Nyní přichází zábavná část: **extrahovat text z obrázku** a **převést obrázek na JSON** jedním voláním.

```csharp
// Perform OCR and get the result as a JSON string
string jsonResult = ocrEngine.RecognizeToJson(receiptImage);
```

Metoda `RecognizeToJson` vrací bohatou JSON strukturu, která obsahuje:

- `Text`: prostý spojený text.
- `Lines`: pole objektů řádků s koordináty.
- `Words`: každé slovo s hodnocením spolehlivosti.
- `Regions`: ohraničující rámečky pro detekované bloky textu.

JSON můžete deserializovat do C# objektu, pokud potřebujete typově bezpečný přístup, ale v mnoha scénářích stačí vypsat surový JSON.

---

## Krok 4 – Výpis JSON (nebo jeho uložení)

Podívejme se na výstup a proberme, co s ním dál dělat.

```csharp
// Write the JSON to the console – perfect for quick debugging
Console.WriteLine(jsonResult);

// Bonus: Save the JSON to a file for later processing
File.WriteAllText("receipt_output.json", jsonResult);
```

### Ukázkový výstup

```json
{
  "Text":"Walmart\n123 Main St\nItem A  $2.99\nItem B  $5.49\nTotal   $8.48",
  "Lines":[
    {"Text":"Walmart","BoundingBox":{"X":10,"Y":15,"Width":200,"Height":30}},
    {"Text":"123 Main St","BoundingBox":{"X":10,"Y":50,"Width":180,"Height":25}},
    {"Text":"Item A  $2.99","BoundingBox":{"X":10,"Y":85,"Width":210,"Height":28}},
    {"Text":"Item B  $5.49","BoundingBox":{"X":10,"Y":120,"Width":210,"Height":28}},
    {"Text":"Total   $8.48","BoundingBox":{"X":10,"Y":155,"Width":210,"Height":30}}
  ],
  "Words":[
    {"Text":"Walmart","Confidence":0.99,"BoundingBox":{...}},
    …
  ]
}
```

**Co dál?**  
Projděte pole `Lines` a vytáhněte částku `Total`, nebo pošlete JSON do downstream služby, která ukládá výdaje. Protože výsledek je už JSON, můžete jej přímo napojit na jakoukoli NoSQL databázi, Azure Function nebo Power Automate flow.

---

## Krok 5 – Řešení běžných hraničních případů

I ty nejlepší OCR engine mají své slabiny. Níže jsou scénáře, na které můžete narazit při učení **jak číst účtenky** z obrázků.

| Situace | Oprava / Doporučení |
|-----------|----------------------|
| **Nízké rozlišení účtenky (≤ 150 dpi)** | Nejprve upscale obrázek pomocí `Bitmap` a `Graphics` (`InterpolationMode.HighQualityBicubic`). |
| **Otočená nebo zkosená účtenka** | Nechte `DetectOrientation = true`. Pro výrazné zkosení předzpracujte pomocí `Image.RotateFlip` nebo knihovny třetí strany jako OpenCV. |
| **Barevné pozadí (např. účtenka na stole)** | Převeďte na odstíny šedi a zvýšte kontrast před OCR (`ImageAttributes`). |
| **Více účtenek na jednom fotografii** | Ořízněte každou oblast účtenky ručně nebo použijte `ocrEngine.Config.RecognizeMultipleRegions = true`. |
| **Velké soubory způsobující OutOfMemory** | Používejte `using` bloky k včasnému uvolnění objektů `Image`, nebo zpracovávejte po částech. |

```csharp
// Example: simple grayscale conversion
using (Bitmap bmp = new Bitmap(receiptImage))
{
    for (int y = 0; y < bmp.Height; y++)
        for (int x = 0; x < bmp.Width; x++)
        {
            Color c = bmp.GetPixel(x, y);
            int gray = (int)(c.R * 0.3 + c.G * 0.59 + c.B * 0.11);
            bmp.SetPixel(x, y, Color.FromArgb(gray, gray, gray));
        }
    receiptImage = (Image)bmp.Clone();
}
```

---

## Krok 6 – Kompletní funkční příklad (připravený ke zkopírování)

Níže je *úplný* program, který můžete ihned zkompilovat. Obsahuje všechny kroky, správné `using` direktivy a elegantní ošetření chyb.

```csharp
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace ReceiptReaderDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣ Load the image file C#
            // -------------------------------------------------
            string imagePath = @"YOUR_DIRECTORY\receipt.jpg";

            if (!File.Exists(imagePath))
            {
                Console.WriteLine($"❌ Image not found: {imagePath}");
                return;
            }

            Image receiptImage;
            try
            {
                receiptImage = Image.FromFile(imagePath);
            }
            catch (Exception ex)
            {
                Console.WriteLine($"⚠️ Failed to load image: {ex.Message}");
                return;
            }

            // -------------------------------------------------
            // 2️⃣ Create and configure OCR engine
            // -------------------------------------------------
            OcrEngine ocrEngine = new OcrEngine
            {
                Config =
                {
                    Language = OcrLanguage.English,
                    DetectOrientation = true
                }
            };

            // -------------------------------------------------
            // 3️⃣ Recognize and convert to JSON
            // -------------------------------------------------
            string jsonResult;
            try
            {
                jsonResult = ocrEngine.RecognizeToJson(receiptImage);
            }
            catch (Exception ex)
            {
                Console.WriteLine($"🛑 OCR failed: {ex.Message}");
                return;
            }

            // -------------------------------------------------
            // 4️⃣ Output results
            // -------------------------------------------------
            Console.WriteLine("🗂️ OCR JSON Result:");
            Console.WriteLine(jsonResult);

            // Optionally persist the JSON
            string outputPath = Path.Combine(
                Path.GetDirectoryName(imagePath) ?? ".", "receipt_output.json");
            File.WriteAllText(outputPath, jsonResult);
            Console.WriteLine($"✅ JSON saved to {outputPath}");
        }
    }
}
```

**Spusťte:**  
`dotnet run` ze složky projektu. Pokud je vše nastaveno správně, uvidíte JSON vytištěný v konzoli a uložený vedle vašeho obrázku účtenky.

---

## Závěr

Právě jsme prošli **jak číst účtenky** z obrázků v C# od začátku až do konce. Načtením obrázku, konfigurací Aspose OCR a voláním `RecognizeToJson` můžete **extrahovat text z obrázku** a **převést obrázek na JSON** téměř bez jakéhokoli boilerplate kódu. Přístup škáluje — od jedné ukázkové účtenky po dávkový procesor, který během noci zpracuje stovky účtenek.

Další kroky, které můžete prozkoumat:

- **Parsovat JSON** a vytáhnout data jako datum, částku a položky (použijte `System.Text.Json` nebo `Newtonsoft.Json`).
- **Integrovat s databází** (SQL, Cosmos DB) pro automatické ukládání výdajových záznamů.
- **Přidat UI** (WinForms, WPF nebo Blazor), aby uživatelé mohli přetahovat účtenky.
- **Vyměnit Aspose OCR** za jiný engine (Tesseract, Microsoft Azure OCR), pokud je licencování problém — stačí zachovat stejný vzor „load image file C#“.

Klidně experimentujte, rozbíjejte věci a pak se vraťte sem pro osvěžení. Pokud narazíte na problém, komunita (a fóra Aspose) jsou skvělá místa, kde se zeptat. Šťastné kódování a užijte si převod papírových účtenek na čistá, prohledávatelná data!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}