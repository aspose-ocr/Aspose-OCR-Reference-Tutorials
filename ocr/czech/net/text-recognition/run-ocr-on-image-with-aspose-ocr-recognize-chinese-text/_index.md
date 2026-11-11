---
category: general
date: 2026-03-04
description: Spusťte OCR na obrázku pomocí Aspose OCR v C#. Naučte se, jak rozpoznat
  čínský text, extrahovat text z obrázku a načíst obrázek pro OCR během několika kroků.
draft: false
keywords:
- run OCR on image
- recognize chinese text
- extract text from image
- load image for OCR
- recognize simplified chinese
language: cs
og_description: Spusťte OCR na obrázku pomocí Aspose OCR v C#. Tento průvodce vám
  ukáže, jak rozpoznat čínský text, extrahovat text z obrázku a efektivně načíst obrázek
  pro OCR.
og_title: Spusťte OCR na obrázku s Aspose OCR – Rychlé rozpoznávání čínského textu
tags:
- Aspose OCR
- C#
- Chinese OCR
title: Spusťte OCR na obrázku s Aspose OCR – Rozpoznání čínského textu
url: /cs/net/text-recognition/run-ocr-on-image-with-aspose-ocr-recognize-chinese-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Spusťte OCR na obrázku – Kompletní průvodce C# pro čínský text

Už jste někdy potřebovali **run OCR on image** soubory, ale nebyli jste si jisti, která knihovna zvládne zjednodušenou čínštinu bez problémů? Nejste v tom sami. Mnoho vývojářů narazí na překážku, když se snaží **recognize Chinese text**, a končí s tím, že si trhají vlasy kvůli problémům s kódováním.  

V tomto tutoriálu se dostaneme k jádru a ukážeme vám krok za krokem, jak **run OCR on image** prostředky pomocí Aspose OCR, stáhnout potřebný jazykový model jen jednou a nakonec **extract text from image** soubory obsahující znaky zjednodušené čínštiny. Na konci budete mít připravenou konzolovou aplikaci, která vytiskne rozpoznaný text do konzole.

> **Co získáte:** kompletní, kompilovatelný C# program, vysvětlení *proč* je každý řádek důležitý, a tipy pro řešení běžných problémů, jako chybějící zdroje nebo špatné formáty obrázků.

## Co budete potřebovat

Než se pustíme dál, ujistěte se, že máte na svém vývojovém počítači nainstalovány následující předpoklady:

| Předpoklad | Proč je důležitý |
|------------|-------------------|
| .NET 6.0 SDK or later | Poskytuje runtime a kompilátor pro C# projekty. |
| Visual Studio 2022 (or VS Code with C# extension) | Poskytuje IntelliSense a snadné ladění. |
| Aspose.OCR NuGet package | Jádrová knihovna, která poskytuje OCR funkce. |
| An image containing Simplified Chinese characters (e.g., `chinese_sample.png`) | Zdroj, ze kterého **load image for OCR**. |

NuGet balíček můžete stáhnout pomocí:

```bash
dotnet add package Aspose.OCR
```

Nyní, když je základ položen, pojďme rozběhnout engine.

## Krok 1 – Vyberte jazykový model (Recognize Simplified Chinese)

Aspose OCR odděluje jazyková data od jádrového enginu, což znamená, že musíte SDK sdělit, který model potřebujete. Protože pracujeme se znaky kontinentální čínštiny, vybereme model **Simplified Chinese**.

```csharp
using Aspose.OCR;
using Aspose.OCR.ResourceManagement;

// Select the Simplified Chinese language model
LanguageModel languageModel = LanguageModel.ChineseSimplified;
```

*Proč je to důležité:* OCR engine používá jazykově specifické slovníky a tvary znaků. Výběr správného modelu dramaticky zvyšuje přesnost, zejména u hustých skriptů jako čínština.

## Krok 2 – Stáhněte model jednou (Extract Text from Image)

Při prvním spuštění kódu budete muset stáhnout soubory modelu ze serverů Aspose. `ResourceDownloader` to za vás zařídí. V produkční aplikaci byste to pravděpodobně udělali asynchronně, ale pro přehlednost tutoriálu použijeme blokování pomocí `.Wait()`.

```csharp
// Initialise the downloader and fetch the model (runs once)
ResourceDownloader resourceDownloader = new ResourceDownloader();
resourceDownloader.DownloadModelAsync(languageModel).Wait();
```

> **Tip:** Uložte stažené zdroje do složky, která je součástí vašeho projektu (např. `OcrResources`). Tím se při dalších spuštěních vynechá síťové volání, což proces zrychlí.

## Krok 3 – Nastavte engine na vaše lokální zdroje (Load Image for OCR)

Nyní vytvoříme OCR engine a řekneme mu, kde jsou soubory modelu uloženy. `LocalResourceProvider` čte soubory z disku, čímž eliminuje další síťový provoz.

```csharp
// Create the OCR engine and link it to the local resources folder
OcrEngine ocrEngine = new OcrEngine
{
    ResourceProvider = new LocalResourceProvider(@"YOUR_DIRECTORY/OcrResources")
};
```

Nahraďte `YOUR_DIRECTORY` absolutní nebo relativní cestou, která ukazuje na místo, kde jsou modelové soubory uloženy.

*Proč je to důležité:* Pokud engine nedokáže najít jazykové zdroje, vyhodí `FileNotFoundException` a nebudete schopni **run OCR on image** vůbec.

## Krok 4 – Nastavte jazyk pro rozpoznávání (Recognize Chinese Text)

I když jsme stáhli model Simplified Chinese, musíme engine stále informovat, který jazyk má během rozpoznávání použít.

```csharp
// Tell the engine to use Simplified Chinese for this session
ocrEngine.Language = Language.ChineseSimplified;
```

Pokud budete někdy potřebovat během běhu přepnout jazyk (např. z čínštiny na angličtinu), můžete jednoduše změnit tuto vlastnost před voláním `Recognize`.

## Krok 5 – Načtěte obrázek a spusťte OCR (Run OCR on Image)

Zde je jádro tutoriálu: načtení souboru obrázku a extrakce jeho textového obsahu. Metoda `ImageInfo.Load` načte soubor do formátu, který OCR engine rozumí.

```csharp
// Load the image that contains Chinese characters
var imageInfo = ImageInfo.Load(@"YOUR_DIRECTORY/chinese_sample.png");

// Perform OCR – this is where we actually run OCR on image
OcrResult ocrResult = ocrEngine.Recognize(imageInfo);
```

Pokud je obrázek velký nebo šumivý, zvažte jeho předzpracování (např. binarizaci) před tímto krokem. Aspose OCR také nabízí filtry, ale to přesahuje rámec tohoto úvodního průvodce.

## Krok 6 – Výstup rozpoznaného textu (Extract Text from Image)

Nakonec vytiskneme extrahovaný řetězec do konzole. V reálném scénáři byste ho mohli zapsat do databáze, souboru nebo předat jiné službě.

```csharp
// Show the OCR result in the console
Console.WriteLine("=== Recognized Text ===");
Console.WriteLine(ocrResult.Text);
```

Spuštěním programu by se mělo zobrazit něco jako:

```
=== Recognized Text ===
你好，世界！这是一个测试。
```

A to je vše—váš první **run OCR on image**, který **recognize Chinese text**.

## Kompletní, připravený příklad

Níže je celý program, který můžete zkopírovat a vložit do nového konzolového projektu (`dotnet new console`). Nezapomeňte nahradit `YOUR_DIRECTORY` skutečnou cestou na vašem počítači.

```csharp
// ------------------------------------------------------------
// Complete C# example: Run OCR on Image and Recognize Simplified Chinese
// ------------------------------------------------------------
using System;
using Aspose.OCR;
using Aspose.OCR.ResourceManagement;

class Program
{
    static void Main()
    {
        // 1️⃣ Choose the language model (Simplified Chinese)
        LanguageModel languageModel = LanguageModel.ChineseSimplified;

        // 2️⃣ Download the model (only the first time)
        var downloader = new ResourceDownloader();
        downloader.DownloadModelAsync(languageModel).Wait();   // Blocking for tutorial simplicity

        // 3️⃣ Initialise OCR engine with local resources folder
        var ocrEngine = new OcrEngine
        {
            ResourceProvider = new LocalResourceProvider(@"YOUR_DIRECTORY/OcrResources")
        };

        // 4️⃣ Set the language for this session
        ocrEngine.Language = Language.ChineseSimplified;

        // 5️⃣ Load the image that contains Chinese text
        var imageInfo = ImageInfo.Load(@"YOUR_DIRECTORY/chinese_sample.png");

        // 6️⃣ Run OCR on the image and capture the result
        OcrResult result = ocrEngine.Recognize(imageInfo);

        // 7️⃣ Output the extracted text
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(result.Text);
    }
}
```

> **Očekávaný výstup:** Konzole vytiskne čínské znaky nalezené v `chinese_sample.png`. Pokud je obrázek čistý, přesnost často přesahuje 95 %.

## Časté problémy a jak se jim vyhnout

| Příznak | Pravděpodobná příčina | Řešení |
|---------|-----------------------|--------|
| `FileNotFoundException` on startup | Špatná cesta ke složce zdrojů | Zkontrolujte cestu v `LocalResourceProvider`. Použijte `Path.Combine` pro bezpečnost napříč platformami. |
| Prázdný výstup (`ocrResult.Text` prázdný) | Obrázek je příliš šumivý nebo nepodporovaný formát | Převěďte obrázek na vysokokontrastní PNG, nebo použijte `ocrEngine.PreprocessImage(imageInfo)` před `Recognize`. |
| Exception: `Unsupported language` | Jazykový model nebyl stažen | Znovu spusťte krok stahování, nebo smažte poškozenou složku a nechte ji stáhnout znovu. |
| Slow first run | Stahování modelu přes pomalé připojení | Uložte model do sdílené síťové lokace nebo jej předem zahrňte do instalátoru. |

## Rozšíření řešení (Další kroky)

- **Dávkové zpracování:** Procházejte adresář obrázků a volajte stejnou metodu `Recognize` pro každý soubor. To vám umožní **extract text from image** kolekce bez ruční práce.  
- **Post‑zpracování:** Použijte regulární výrazy k vyčištění OCR artefaktů (např. osamělé interpunkce).  
- **Detekce jazyka:** Pokud potřebujete zpracovávat vícejazyčné dokumenty, podívejte se na `ocrResult.DetectedLanguage` (k dispozici v novějších verzích Aspose) a podle toho přepněte `ocrEngine.Language`.  

## Závěr

Prošli jsme vše, co potřebujete k **run OCR on image** souborům pomocí Aspose OCR v C#. Od výběru správného modelu **recognize simplified Chinese**, přes stažení zdrojů, konfiguraci enginu až po **extract text from image**, tutoriál vám poskytuje samostatné řešení připravené ke zkopírování.

Nyní můžete s jistotou **recognize Chinese text** v libovolném PNG nebo JPEG, který předáte engine, a máte pevný základ pro rozšíření na dávkové úlohy, podporu více jazyků nebo integraci s následnými analytickými pipeline.

Máte otázky ohledně ladění nastavení OCR nebo práce s jinými skripty? Zanechte komentář a šťastné programování! 

![Run OCR on image example](image.png "Run OCR on image example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}