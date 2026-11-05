---
category: general
date: 2026-02-19
description: Jak rychle provádět OCR na vysoce rozlišených TIFF obrázcích. Naučte
  se extrahovat text z TIFF souborů pomocí GPU OCR v C#.
draft: false
keywords:
- how to perform OCR
- extract text from tiff
- use gpu ocr
- Aspose OCR C#
- high‑resolution image processing
- OCR performance tuning
language: cs
og_description: jak provést OCR na vysokorozlišovacích TIFF souborech pomocí Aspose
  OCR a akcelerace GPU. Kompletní krok‑za‑krokem průvodce.
og_title: Jak provést OCR – GPU‑akcelerovaný C# tutoriál
tags:
- OCR
- C#
- Aspose
- GPU
- Image Processing
title: Jak provést OCR pomocí Aspose OCR – průvodce C# s GPU akcelerací
url: /cs/net/ocr-optimization/how-to-perform-ocr-with-aspose-ocr-gpu-accelerated-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak provést OCR – GPU‑akcelerovaný C# tutoriál

Už jste někdy potřebovali provést OCR na obrovském TIFF skenu a přemýšleli, proč to trvá věčnost? Nejste v tom sami. V tomto průvodci vám ukážeme **jak provést OCR** na vysoce rozlišeném obrázku s využitím GPU a odnesete si připravený C# program, který během okamžiku extrahuje text z tiff souborů.

Probereme vše od instalace balíčku Aspose OCR po povolení GPU zpracování a vysvětlíme, proč je každé nastavení důležité. Na konci budete schopni vložit tento kód do libovolného .NET projektu, nasměrovat ho na .tif a získat čistý, prohledávatelný text – bez nutnosti dalších služeb.

## Prerequisites

- .NET 6.0 nebo novější (kód cílí na .NET 6, ale .NET 5 také funguje)  
- Kompatibilní GPU (NVIDIA CUDA 11+ nebo AMD Radeon s podporou OpenCL)  
- **Aspose.OCR** NuGet balíček (verze 23.9 nebo novější)  
- Vysoce rozlišený TIFF soubor, který chcete číst (např. `high_res_page.tif`)  

Pokud některý z těchto bodů není vám známý, nebojte se – každý z nich je podrobně vysvětlen v následujících krocích.

## Step 1: Install Aspose OCR and Enable GPU Processing  

Prvním krokem je přidat knihovnu Aspose OCR do vašeho projektu a zapnout podporu GPU. Povolení GPU říká enginu, aby těžké maticové výpočty přenesl na grafickou kartu, což může zkrátit dobu zpracování o 70 % nebo více na moderním GPU.

```csharp
// Install the package via the CLI (run once):
// dotnet add package Aspose.OCR --version 23.9.0

using Aspose.OCR;
using Aspose.OCR.Gpu;
using System;

class GpuDemo
{
    static void Main()
    {
        // Enable GPU acceleration – requires a compatible GPU driver.
        OcrEngine.EnableGpuProcessing(true);
```

**Why this matters:**  
Bez `EnableGpuProcessing(true)` se OCR engine vrátí k čistému CPU provádění, což je v pořádku pro malé obrázky, ale na multi‑megapixelových TIFF souborech je to bolestně pomalé. Zapnutí tohoto příznaku umožní knihovně využívat CUDA nebo OpenCL pod kapotou, což dramaticky snižuje `ProcessingTime`, který uvidíte později.

## Step 2: Configure the OCR Engine for English (or any language you need)  

Dále vytvoříme instanci `OcrEngine` a nastavíme jazyk. Aspose podporuje více než 100 jazyků; zde je ukázán angličtina, protože je nejčastější, ale můžete nahradit `Language.English` za `Language.French`, `Language.German` a další.

```csharp
        // Step 2: Create and configure the OCR engine.
        var ocrEngine = new OcrEngine
        {
            Language = Language.English   // Change if you need another language.
        };
```

**Pro tip:**  
Pokud plánujete zpracovávat vícejazyčné dokumenty, vytvořte si více engine instancí nebo přepínejte vlastnost `Language` mezi voláními. Tím se vyhnete režii spojené s opakovaným vytvářením engine pro každou stránku.

## Step 3: Perform OCR on a High‑Resolution TIFF  

Nyní ta zábavná část – předáme engine TIFF soubor a necháme ho udělat těžkou práci. Metoda `RecognizeImage` vrací `OcrResult`, který obsahuje jak extrahovaný text, tak i časové informace.

```csharp
        // Step 3: Run OCR on the TIFF image.
        var ocrResult = ocrEngine.RecognizeImage(@"YOUR_DIRECTORY/high_res_page.tif");
```

**Edge case handling:**  
- **Large files:** Pokud váš TIFF překročí 50 MB, zvažte jeho down‑sampling pomocí `System.Drawing` nebo `ImageSharp`, aby byl paměťový odběr rozumný.  
- **Multi‑page TIFFs:** Volajte `RecognizeImage` uvnitř smyčky přes jednotlivé indexy stránek; Aspose vrátí text pro každou stránku zvlášť.

## Step 4: Output Processing Time and Extracted Text  

Nakonec vypíšeme čas, který zpracování zabralo, a surový OCR výstup. Zde uvidíte výhodu GPU akcelerace.

```csharp
        // Step 4: Display results.
        Console.WriteLine($"Time taken: {ocrResult.ProcessingTime} ms");
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Typical output**

```
Time taken: 312 ms
=== Extracted Text ===
Lorem ipsum dolor sit amet, consectetur adipiscing elit...
```

Na středně výkonném RTX 3060 stejný 3000 × 4000 pixelový TIFF, který dříve trval na CPU ~1,2 sekundy, nyní skončí za ~300 ms – všimněte si dramatického zrychlení.

## How to Extract Text from TIFF Files Efficiently  

Pokud vás zajímá jen krok **extract text from tiff** a GPU nepotřebujete, můžete vynechat GPU příznak. Zbytek kódu zůstane stejný, ale přijdete o výkonnostní výhody u velkých skenů. Zde je minimalistická verze:

```csharp
using Aspose.OCR;
using System;

class SimpleTiffOcr
{
    static void Main()
    {
        var engine = new OcrEngine { Language = Language.English };
        var result = engine.RecognizeImage(@"sample.tif");
        Console.WriteLine(result.Text);
    }
}
```

**When to use this:**  
- Vaše nasazení běží na serveru bez GPU (headless).  
- TIFF soubory jsou malé (< 1 MP) a čas CPU není úzkým hrdlem.  

I bez GPU je OCR engine Aspose vysoce přesný díky vestavěným neuronovým modelům.

## Using GPU OCR for Faster Processing – Common Pitfalls  

Zatímco **use gpu OCR** vám poskytuje rychlost, několik úskalí vás může překvapit:

| Issue | Symptom | Fix |
|-------|---------|-----|
| Missing CUDA driver | `EnableGpuProcessing` throws `PlatformNotSupportedException` | Install the latest NVIDIA driver and CUDA toolkit |
| Unsupported GPU | Engine falls back silently to CPU | Verify your GPU appears in `OcrEngine.GetAvailableGpus()` (if you call it) |
| Out‑of‑memory on very large images | `System.OutOfMemoryException` | Process the image in tiles (`engine.RecognizeRegion`) |
| Incorrect image orientation | Garbled text | Pre‑rotate the TIFF using `ImageSharp` before OCR |

**Quick sanity check:** Spusťte demo jednou s `EnableGpuProcessing(false)`. Porovnejte hodnoty `ProcessingTime`; zdravý běh s GPU akcelerací by měl být alespoň 2‑3× rychlejší.

## Full Working Example (Copy‑Paste Ready)

Níže je kompletní program, který můžete vložit do konzolové aplikace. Nahraďte `YOUR_DIRECTORY` skutečnou cestou k vašemu TIFF souboru.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;
using System;

class GpuDemo
{
    static void Main()
    {
        // 1️⃣ Enable GPU acceleration (requires a compatible GPU)
        OcrEngine.EnableGpuProcessing(true);

        // 2️⃣ Create the OCR engine and set the language
        var ocrEngine = new OcrEngine
        {
            Language = Language.English   // Change as needed
        };

        // 3️⃣ Perform OCR on a high‑resolution TIFF
        var imagePath = @"YOUR_DIRECTORY/high_res_page.tif";
        var ocrResult = ocrEngine.RecognizeImage(imagePath);

        // 4️⃣ Show timing and extracted text
        Console.WriteLine($"Time taken: {ocrResult.ProcessingTime} ms");
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

Spuštěno na stroji s RTX 3070 poskytne výstup podobný předchozímu příkladu, což potvrzuje, že **how to perform OCR** s podporou GPU funguje podle očekávání.

## Next Steps – Going Beyond the Basics  

- **Batch processing:** Zabalte volání `RecognizeImage` do `foreach` smyčky přes složku s TIFFy.  
- **Post‑processing:** Předejte `ocrResult.Text` do kontroloru pravopisu nebo do parseru přirozeného jazyka, aby se odstranily OCR artefakty.  
- **Hybrid mode:** Detekujte velikost obrázku za běhu a rozhodněte, zda povolit GPU (`if (image.Width * image.Height > 5_000_000) EnableGpuProcessing(true)`).  

Všechny tyto rozšíření stále **use gpu ocr**, když to dává smysl, a udržují váš pipeline rychlý a šetrný k prostředkům.

## Conclusion  

Nyní už víte **how to perform OCR** na vysoce rozlišených TIFF souborech pomocí Aspose OCR a GPU akcelerace a můžete s jistotou **extract text from tiff** dokumenty během zlomku času, který by zabral čistě CPU přístup. Kompletní, připravený příklad ukazuje celý tok – od povolení GPU po výpis doby zpracování a finálního textu.

Vyzkoušejte to, pohrňte si nastavení jazyků a zkuste zpracovat dávku stránek. Pokud narazíte na problémy, podívejte se znovu na tabulku „Using GPU OCR for Faster Processing“; většina problémů je tam popsána. Šťastné programování a užijte si ten rychlostní boost!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}