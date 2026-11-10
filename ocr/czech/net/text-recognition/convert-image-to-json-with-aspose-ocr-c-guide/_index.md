---
category: general
date: 2026-01-15
description: Převod obrázku na JSON pomocí Aspose OCR v C#. Naučte se, jak extrahovat
  text z obrázku, získat ohraničující rámečky v JSON a rozpoznat obrázek účtenky.
draft: false
keywords:
- convert image to json
- extract text from image
- aspose ocr c# example
- recognize receipt image
- json bounding boxes
language: cs
og_description: Převod obrázku do JSON pomocí Aspose OCR v C#. Podrobný návod, jak
  extrahovat text z obrázku, rozpoznat obrázek účtenky a získat ohraničující rámečky
  v JSON.
og_title: Převod obrázku do JSON pomocí Aspose OCR C# průvodce
tags:
- Aspose OCR
- C#
- JSON
- Image Processing
title: Převod obrázku do JSON pomocí Aspose OCR C# průvodce
url: /cs/net/text-recognition/convert-image-to-json-with-aspose-ocr-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Převod obrázku na JSON s Aspose OCR C# Průvodcem

Už jste někdy potřebovali **převést obrázek na JSON**, ale nebyli jste si jisti, která knihovna vám poskytne jak surový text, tak přesné souřadnice slov? Nejste v tom sami. Mnoho vývojářů narazí na tento problém, když se snaží extrahovat text z obrazových souborů – zejména účtenek – a zároveň potřebují strojově čitelný JSON payload pro další zpracování.

V tomto tutoriálu projdeme kompletním **Aspose OCR C# příkladem**, který vám ukáže, jak extrahovat text z obrázku, rozpoznat obrázek účtenky a výstup **JSON ohraničujících rámečků** pro každé slovo. Na konci budete mít připravenou konzolovou aplikaci, která vytiskne hezky formátovaný JSON řetězec, který můžete předat jakémukoli API, databázi nebo analytickému pipeline.

> **Co si z toho odnesete**  
> • Plně funkční C# projekt, který **převádí obrázek na JSON**  
> • Pochopení, proč povolujeme `IncludeBoundingBoxes` (je to klíč k `json bounding boxes`)  
> • Tipy pro práci s různými formáty obrázků a jazyky  

Pojďme začít.

---

## Co budete potřebovat

Než se ponoříme do kódu, ujistěte se, že máte nainstalovány následující předpoklady:

- **.NET 6.0 SDK** (nebo jakoukoli novější verzi) – kód cílí na .NET 6, ale funguje i na .NET Framework 4.7+.
- **Aspose.OCR for .NET** NuGet balíček – můžete jej získat pomocí `dotnet add package Aspose.OCR`.
- Ukázkový obrázek účtenky (`receipt.jpg`) umístěný ve složce, na kterou můžete odkazovat z projektu.
- Visual Studio 2022, VS Code nebo jakékoli IDE, které preferujete.

Žádné další externí služby nejsou vyžadovány; vše běží lokálně.

## Převod obrázku na JSON – Přehled

Základní myšlenka je jednoduchá: načíst obrázek, říct Aspose OCR, aby rozpoznal angličtinu (nebo jakýkoli podporovaný jazyk), požádat o zahrnutí ohraničujících rámečků a nakonec požádat o výsledek ve formátu **JSON**. Knihovna provádí veškerou těžkou práci – OCR, analýzu rozvržení a serializaci do JSON.

Zde je diagram vysoké úrovně toku (představte si malý obrázek):

```
[Image File] → Aspose OCR Engine → Recognition Options (JSON + Bounding Boxes) → JSON Output
```

Tento malý diagram zachycuje celý pipeline, který implementujeme.

## Krok 1: Nastavení projektu a instalace Aspose OCR

Nejprve vytvořte nový konzolový projekt a přidejte balíček Aspose OCR.

```bash
dotnet new console -n JsonOutputDemo
cd JsonOutputDemo
dotnet add package Aspose.OCR
```

> **Pro tip:** Pokud používáte Visual Studio, klikněte pravým tlačítkem na projekt → *Manage NuGet Packages* → vyhledejte **Aspose.OCR** a nainstalujte nejnovější stabilní verzi (aktuálně 23.12).

## Krok 2: Načtení obrázku, který chcete rozpoznat

Použijeme metodu `OcrImage.FromFile` k načtení obrázku účtenky. Ujistěte se, že cesta ukazuje na skutečný soubor; jinak narazíte na `FileNotFoundException`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Output;

class JsonOutputDemo
{
    static void Main()
    {
        // Step 2: Load the image you want to recognize
        var receiptImage = OcrImage.FromFile("YOUR_DIRECTORY/receipt.jpg");
```

Pokud je váš obrázek vedle souboru `.csproj`, můžete jednoduše použít `"receipt.jpg"`.

## Krok 3: Konfigurace OCR možností pro JSON ohraničující rámečky

Magie nastane, když povolíme `OutputFormat = OutputFormat.Json` **a** `IncludeBoundingBoxes = true`. První říká Aspose, aby výsledek serializoval jako JSON, zatímco druhý přidá `x`, `y`, `width` a `height` pro každé slovo – přesně to, co potřebujete pro `json bounding boxes`.

```csharp
        // Step 3: Configure OCR options
        var ocrOptions = new OcrOptions
        {
            OutputFormat = OutputFormat.Json,
            IncludeBoundingBoxes = true   // include coordinates for each recognized word
        };
```

Můžete také upravit `ocrOptions.Dpi` nebo `ocrOptions.Language`, pokud potřebujete vyšší rozlišení nebo jiný jazyk.

## Krok 4: Provedení rozpoznání – Extrakce textu z obrázku

Nyní zavoláme `Recognize`. Metoda vrací objekt `OcrResult`, který obsahuje JSON řetězec, surový text a další.

```csharp
        // Step 4: Perform recognition using English language and the configured options
        var ocrEngine = new OcrEngine();
        var ocrResult = ocrEngine.Recognize(receiptImage, Language.English, ocrOptions);
```

Pokud potřebujete pracovat s jinými jazyky, nahraďte `Language.English` za `Language.Spanish`, `Language.French` atd. Aspose podporuje více než 30 jazyků přímo.

## Krok 5: Výstup výsledku – Váš JSON payload

Nakonec vytiskneme JSON do konzole. Ve skutečné aplikaci byste jej pravděpodobně zapsali do souboru nebo odeslali do služby.

```csharp
        // Step 5: Output the resulting JSON string
        System.Console.WriteLine(ocrResult.Json);
    }
}
```

Spuštěním programu by se měl vytvořit JSON dokument podobný úryvku níže.

```json
{
  "Text": "Total $12.34\nDate 01/01/2024",
  "Words": [
    {
      "Text": "Total",
      "BoundingBox": { "X": 45, "Y": 112, "Width": 60, "Height": 20 }
    },
    {
      "Text": "$12.34",
      "BoundingBox": { "X": 110, "Y": 112, "Width": 70, "Height": 20 }
    },
    {
      "Text": "Date",
      "BoundingBox": { "X": 45, "Y": 140, "Width": 50, "Height": 20 }
    },
    {
      "Text": "01/01/2024",
      "BoundingBox": { "X": 100, "Y": 140, "Width": 120, "Height": 20 }
    }
  ]
}
```

Všimněte si, že každé slovo nyní nese svůj **JSON ohraničující rámeček** – ideální pro předání do UI overlay nebo následného parseru.

## Kompletní funkční příklad

Níže je kompletní program připravený ke zkopírování. Žádné skryté části, žádné externí volání – jen čistý C#.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Output;

class JsonOutputDemo
{
    static void Main()
    {
        // 1️⃣ Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // 2️⃣ Load the image you want to recognize
        var receiptImage = OcrImage.FromFile("YOUR_DIRECTORY/receipt.jpg");

        // 3️⃣ Configure OCR options to get detailed JSON output with word positions
        var ocrOptions = new OcrOptions
        {
            OutputFormat = OutputFormat.Json,
            IncludeBoundingBoxes = true   // include coordinates for each recognized word
        };

        // 4️⃣ Perform recognition using English language and the configured options
        var ocrResult = ocrEngine.Recognize(receiptImage, Language.English, ocrOptions);

        // 5️⃣ Output the resulting JSON string
        System.Console.WriteLine(ocrResult.Json);
    }
}
```

> **Dejte si pozor na:**  
> • **Chyby cesty k souboru** – dvakrát zkontrolujte umístění obrázku.  
> • **Chybějící NuGet balíček** – ujistěte se, že je odkaz na `Aspose.OCR`.  
> • **Nepodporované formáty obrázků** – pro nejlepší výsledky používejte JPEG, PNG, BMP nebo TIFF.

## Časté otázky a okrajové případy

### Mohu převést **PDF stránku** na JSON místo JPEG?

Ano. Nejprve převést stránku PDF na obrázek (např. pomocí `Aspose.PDF`), pak tento obrázek předat do stejného OCR pipeline. Výstup JSON bude identický, protože OCR krok se stará jen o rastrová data.

### Co když je účtenka rozmazaná?

Zvyšte DPI v `ocrOptions`. Například:

```csharp
ocrOptions.Dpi = 300; // higher DPI improves accuracy on low‑quality scans
```

Vyšší DPI může zvýšit spotřebu paměti, takže je třeba vyvážit kvalitu a výkon.

### Potřebuji **více jazyků** na stejné účtence (např. angličtina + španělština).

Můžete předat pole jazyků:

```csharp
var ocrResult = ocrEngine.Recognize(receiptImage, new[] { Language.English, Language.Spanish }, ocrOptions);
```

Aspose se pokusí rozpoznat každý jazyk ve zadaném pořadí.

### Jak zapíšu JSON do souboru?

Stačí nahradit řádek `Console.WriteLine` tímto:

```csharp
System.IO.File.WriteAllText("receipt.json", ocrResult.Json);
```

Nyní máte trvalý soubor, který můžete poslat dalším službám.

## Vizualizovaný souhrn

![příklad převodu obrázku na json](convert-image-to-json.png "příklad převodu obrázku na json")

*Snímek obrazovky ukazuje výstup JSON payload po spuštění dema.*

## Závěr

Právě jsme vám ukázali, jak **převést obrázek na JSON** pomocí Aspose OCR v C#. Nastavením `OutputFormat` a `IncludeBoundingBoxes` můžete **extrahovat text z obrázku**, **rozpoznat obrázek účtenky** a získat přesné **JSON ohraničující rámečky** pro každé slovo. Kompletní spustitelný kód je výše v úryvku, takže jej můžete okamžitě vložit do libovolného .NET projektu.

Co dál? Zkuste předat JSON do front‑endového prohlížeče, který zvýrazní každé slovo, nebo data poslat do modelu strojového učení, který klasifikuje položky na účtenkách. Můžete také experimentovat s dalšími jazyky, vyššími nastaveními DPI nebo dávkovým zpracováním více obrázků ve smyčce.

Pokud narazíte na problémy, vzpomeňte si na tipy ohledně cest k souborům, DPI a jazykových polí. Neváhejte zanechat komentář nebo otevřít issue v GitHub repozitáři, který pro tento demo vytvoříte. Šťastné programování a užívejte si převod obrázků na strukturovaný JSON!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}