---
category: general
date: 2026-01-09
description: Rychle extrahujte text z PNG pomocí Aspose OCR. Naučte se, jak číst text
  z obrázku, zlepšit přesnost OCR a získat čisté výsledky v C#.
draft: false
keywords:
- extract text from png
- read image text
- improve ocr accuracy
- extract text from image
- aspose ocr tutorial
language: cs
og_description: Rychle extrahujte text z PNG pomocí Aspose OCR. Naučte se, jak číst
  text z obrázku, zlepšit přesnost OCR a získat čisté výsledky v C#.
og_title: Extrahování textu z PNG – Kompletní tutoriál Aspose OCR
tags:
- Aspose OCR
- C#
- Image Processing
title: Extrahovat text z PNG – Kompletní tutoriál Aspose OCR
url: /cs/net/text-recognition/extract-text-from-png-complete-aspose-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahování textu z PNG – Kompletní tutoriál Aspose OCR

Už jste někdy potřebovali **extrahovat text z PNG** souborů, ale výstup byl plný nesmyslů? Nejste v tom sami. V mnoha reálných projektech – faktury, účtenky nebo naskenované formuláře – kvalita OCR výstupu může rozhodnout o úspěchu automatizačních pipeline.

V tomto průvodci vám ukážeme **krok za krokem**, jak číst text z obrázku pomocí Aspose OCR, přidat vlastní slovník pro **zlepšení přesnosti OCR**, odstranit šum a nakonec vytisknout upravený řetězec. Na konci budete mít připravenou spustitelnou C# konzolovou aplikaci, která spolehlivě extrahuje text z PNG obrázků.

> **Co si odnesete**  
> * Kompletní, spustitelný ukázkový kód.  
> * Pochopení, proč je vlastní slovník důležitý.  
> * Tipy pro řešení okrajových případů, jako jsou snímky s nízkým kontrastem.  

## Požadavky

- .NET 6 SDK nebo novější (kód cílí na .NET 6, ale .NET 5 také funguje).  
- Visual Studio 2022 nebo jakýkoli editor, který preferujete.  
- **PNG** obrázek, který chcete zpracovat – například `invoice.png`.  
- NuGet balíček **Aspose.OCR** (`dotnet add package Aspose.OCR`).  

Žádné další konfigurační soubory nejsou potřeba; vše žije v jediném `.cs` souboru.

## Krok 1 – Instalace a reference Aspose OCR

Nejprve přidejte knihovnu do svého projektu. Otevřete terminál ve složce řešení a spusťte:

```bash
dotnet add package Aspose.OCR
```

Tento jediný řádek stáhne nejnovější stabilní verzi (k lednu 2026, verze 23.9). Balíček obsahuje třídu `OcrEngine`, kterou budeme používat po celou dobu tutoriálu.

## Krok 2 – Inicializace OCR enginu

Vytvoření instance `OcrEngine` je základem. Představte si to jako zapnutí skeneru, který je připraven interpretovat pixely.

```csharp
using Aspose.OCR;

// Initialize the OCR engine
var ocrEngine = new OcrEngine();
```

> **Tip:** Pokud plánujete zpracovávat mnoho obrázků ve smyčce, znovu použijte stejnou instanci `OcrEngine`. Tím se cache interních zdrojů a urychlí následné volání.

## Krok 3 – Zvýšení přesnosti pomocí vlastního slovníku

Out‑of‑the‑box OCR je dobrá, ale může zakopnout nad specifickými slovy jako “Aspose”, “OCR” nebo “SDK”. Přidání těchto termínů do **vlastního slovníku** říká enginu, že tyto řetězce jsou platné, čímž snižuje chybné rozpoznání.

```csharp
// Define domain‑specific terms that the engine should recognize
ocrEngine.CustomDictionary = new HashSet<string>
{
    "Aspose",
    "OCR",
    "SDK",
    "invoice"
};
```

### Proč vlastní slovník pomáhá

- **Statistické modely** OCR silně váží běžné jazykové vzory. Neobvyklá slova mají nízkou pravděpodobnost a mohou být nahrazena podobně vypadajícími znaky.  
- Výslovným uvedením těchto slov přepíšete odhad modelu.  
- Je to zvláště užitečné pro **čtení textu z obrázku**, který obsahuje kódy produktů, zkratky nebo značky.

## Krok 4 – Rozpoznání textu z PNG souboru

Nyní předáme enginu cestu k obrázku. Metoda `RecognizeImage` vrací surový řetězec, který stále obsahuje neznámé tokeny (např. “#@!”), které engine nedokázal mapovat.

```csharp
// Path to the PNG you want to process
string imagePath = @"YOUR_DIRECTORY/invoice.png";

// Perform OCR
string rawText = ocrEngine.RecognizeImage(imagePath);
```

> **Okrajový případ:** Pokud soubor není nalezen, `RecognizeImage` vyhodí `FileNotFoundException`. Pro produkční kód obalte volání do try‑catch bloku.

## Krok 5 – Vyčištění výsledku pomocí `CleanText`

Aspose OCR přichází s pomocníkem, který odstraňuje znaky označené jako “unknown”. Tento krok je klíčový pro projekty **extrahování textu z obrázku**, kde následné parsery očekávají jen alfanumerické znaky a základní interpunkci.

```csharp
// Remove unknown tokens and extra whitespace
string cleanedText = ocrEngine.CleanText(rawText);
```

Metoda `CleanText` také normalizuje konce řádků, což činí výstup bezpečným pro uložení v databázích nebo předání dalším službám.

## Krok 6 – Výstup vyčištěného textu

Nakonec zobrazte nebo uložte výsledek. V konzolové aplikaci `Console.WriteLine` udělá práci.

```csharp
Console.WriteLine("=== Cleaned OCR Output ===");
Console.WriteLine(cleanedText);
```

Po spuštění programu byste měli vidět úhledný blok textu, který odpovídá obsahu `invoice.png`. Pokud obrázek obsahuje slovo “Aspose”, vlastní slovník zajistí, že se zobrazí správně místo něčeho jako “A5p0se”.

## Kompletní funkční příklad

Spojením všeho dohromady získáte kompletní `Program.cs`, který můžete zkopírovat a vložit do nového konzolového projektu:

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize the OCR engine
        var ocrEngine = new OcrEngine();

        // 2️⃣ Add domain‑specific terms to improve OCR accuracy
        ocrEngine.CustomDictionary = new HashSet<string>
        {
            "Aspose",
            "OCR",
            "SDK",
            "invoice"
        };

        // 3️⃣ Path to your PNG file (adjust as needed)
        string imagePath = @"YOUR_DIRECTORY/invoice.png";

        try
        {
            // 4️⃣ Recognize raw text from the image
            string rawText = ocrEngine.RecognizeImage(imagePath);

            // 5️⃣ Clean up unknown tokens
            string cleanedText = ocrEngine.CleanText(rawText);

            // 6️⃣ Show the result
            Console.WriteLine("=== Cleaned OCR Output ===");
            Console.WriteLine(cleanedText);
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error processing image: {ex.Message}");
        }
    }
}
```

**Očekávaný výstup** (předpokládáme, že PNG obsahuje jednoduchou fakturu):

```
=== Cleaned OCR Output ===
Invoice #12345
Date: 01/08/2026
Total: $1,250.00
Thank you for your business!
```

Pokud uvidíte podivné symboly, zkontrolujte kvalitu obrázku nebo rozšiřte vlastní slovník o další termíny.

## Bonus: Zpracování nízkokvalitních skenů

Někdy jsou PNG skenovány při 72 dpi nebo mají silné kompresní artefakty. Zde je několik rychlých triků pro **zlepšení přesnosti OCR** bez opuštění C#:

1. **Předzpracujte obrázek** pomocí knihovny jako `SixLabors.ImageSharp` – zvýšte kontrast, převedete na odstíny šedi nebo aplikujte mírné rozostření pro snížení šumu.  
2. **Nastavte vlastnost `Resolution`** na `OcrEngine` (např. `ocrEngine.Resolution = 300;`) a řekněte enginu, že obrázek má vyšší rozlišení.  
3. **Povolte jazykové balíčky**, pokud pracujete s ne‑anglickým textem (`ocrEngine.Language = Language.English;`).

Všechny tři přístupy můžete přidat před volání `RecognizeImage`.

## Často kladené otázky

- **Funguje to i s jinými formáty obrázků?**  
  Ano. `RecognizeImage` přijímá JPEG, BMP, TIFF a dokonce PDF (jako kontejner obrázku). Stejné kroky platí.

- **Mohu extrahovat text z více PNG souborů ve složce?**  
  Rozhodně. Zabalte hlavní logiku do smyčky `foreach (var file in Directory.GetFiles(folder, "*.png"))` a uložte každý výsledek do seznamu nebo do samostatných souborů.

- **Co když potřebuji souřadnice textu?**  
  Aspose OCR také poskytuje objekty `OcrResult`, které obsahují ohraničující rámečky. Použijte `ocrEngine.RecognizeImageToResult(imagePath)` pro tento pokročilý scénář.

## Závěr

Prošli jsme **kompletním, end‑to‑end** řešením pro **extrahování textu z PNG** souborů pomocí Aspose OCR. Inicializací enginu, přidáním **vlastního slovníku**, vyčištěním surového výstupu a řešením několika běžných úskalí můžete spolehlivě **číst text z obrázku** a **zlepšovat přesnost OCR** ve svých C# aplikacích.

Jste připraveni na další krok? Vyzkoušejte nahradit PNG naskenovanou účtenkou, přidejte více doménově specifických slov do slovníku nebo integrujte výstup s databází pro automatické zpracování faktur. Možnosti jsou neomezené, když spojíte Aspose OCR s bohatým ekosystémem .NET.

Šťastné programování a ať je vaše OCR vždy na jedničku! 

![Extrahování textu z png příklad](/images/extract-text-from-png.png "extrahování textu z png – Aspose OCR demo")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}