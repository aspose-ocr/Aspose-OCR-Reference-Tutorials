---
category: general
date: 2026-05-31
description: Naučte se rozpoznávat text z obrázku v C# pomocí Aspose OCR, včetně toho,
  jak extrahovat text z TIFF souborů a efektivně načítat obrázek pro OCR.
draft: false
keywords:
- recognize text from image
- extract text from tiff
- load image for OCR
- Aspose OCR C#
- GPU accelerated OCR
language: cs
og_description: Krok za krokem průvodce rozpoznáváním textu z obrázku pomocí Aspose
  OCR, zahrnující extrakci z TIFF a správné načtení obrázku pro OCR.
og_title: rozpoznat text z obrázku v C# pomocí Aspose OCR
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to recognize text from image in C# with Aspose OCR, including
    how to extract text from tiff files and load image for OCR efficiently.
  headline: recognize text from image in C# using Aspose OCR
  type: TechArticle
- questions:
  - answer: Reduce its resolution before feeding it to the engine, or increase `GpuMemoryLimit`
      if you have enough VRAM.
    question: What if the image is huge (over 10 MB)?
  - answer: Absolutely. Just reuse the same `OcrEngine` instance and assign a new
      `ImageStream` each iteration.
    question: Can I process multiple images in a loop?
  - answer: '`OcrEngine` implements `IDisposable`. Wrap it in a `using` block for
      clean resource management, especially when working with GPU resources.'
    question: Do I need to dispose of anything?
  - answer: Set `engine.Language = OcrLanguage.Spanish` (or any supported language)
      before calling `Recognize()`.
    question: What about languages other than English?
  type: FAQPage
tags:
- OCR
- C#
- Aspose
title: Rozpoznat text z obrázku v C# pomocí Aspose OCR
url: /cs/net/text-recognition/recognize-text-from-image-in-c-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# rozpoznání textu z obrázku v C# pomocí Aspose OCR

Už jste někdy potřebovali **rozpoznat text z obrázku**, ale nevedeli ste, kde v C# začít? Nejste sami — mnoho vývojářů narazí na tuto překážku při práci s naskenovanými dokumenty nebo více‑stránkovými TIFFy. V tomto průvodci vás provedeme kompletním, připraveným příkladem, který **rozpozná text z obrázku** pomocí knihovny Aspose OCR, a také vám ukážeme, jak **extrahovat text z tiff** a nejlepší způsob, jak **načíst obrázek pro OCR**, aniž byste si trhali vlasy.

Probereme vše od instalace NuGet balíčku až po práci s akcelerací GPU a přepnutím na CPU, pokud je to potřeba. Na konci tohoto tutoriálu budete mít konzolovou aplikaci, která vypíše rozpoznaný text a dobu zpracování — žádné chybějící části, žádné vágní odkazy.

## Co si vytvoříte

- Jednoduchou .NET konzolovou aplikaci, která načte obrázek (včetně více‑stránkového TIFF)  
- OCR engine nastavený pro využití GPU, s elegantním přepnutím na CPU  
- Extrakci prostého textu z obrázku, vytištěnou do konzole  
- Informace o čase, abyste viděli dopad výkonu GPU vs. CPU  

**Požadavky**

- .NET 6 SDK nebo novější (kód funguje s .NET Core i .NET Framework)  
- Základní znalost C# a práce s příkazovým řádkem  
- Připojení k internetu pro stažení NuGet balíčku Aspose.OCR  

Pokud máte vše připravené, pojďme na to.

![C# kód pro rozpoznání textu z obrázku pomocí Aspose OCR](image.png "C# kód pro rozpoznání textu z obrázku pomocí Aspose OCR")

## Krok 1 – Rozpoznání textu z obrázku: Nastavení OCR engine

Nejprve potřebujeme instanci `OcrEngine`. Aspose OCR vám umožní vybrat zařízení pro zpracování — GPU pro rychlost, CPU jako záložní možnost. Engine také přijímá nápovědu pro limit paměti, což může být užitečné na sdílených strojích.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // Create the OCR engine and request GPU acceleration.
        // If no compatible GPU is found, Aspose silently falls back to CPU.
        OcrEngine engine = new OcrEngine
        {
            Device = OcrDevice.Gpu,      // Try GPU first
            GpuMemoryLimit = 1024        // Optional: cap GPU memory usage (MB)
        };
```

**Proč je to důležité:**  
Volba `OcrDevice.Gpu` může u velkých obrázků, zejména více‑stránkových TIFFů, ušetřit sekundy. `GpuMemoryLimit` zabraňuje tomu, aby vaše aplikace spotřebovala veškerou GPU paměť na sdílené pracovní stanici.

## Krok 2 – Načtení obrázku pro OCR (včetně podpory TIFF)

Nyní předáme engine obrázek. `ImageStream.FromFile` od Aspose přijímá **jakýkoli** formát, který knihovna podporuje — TIFF, PNG, JPEG, atd. Tento krok přímo řeší požadavek **načíst obrázek pro OCR**.

```csharp
        // Load the image you want to process.
        // Replace the path with the actual location of your TIFF or other image.
        engine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/sample_multi_page.tif");
```

**Tip:** Pokud pracujete s více‑stránkovým TIFFem, Aspose automaticky zachází s každou stránkou jako s odděleným rámcem a engine je zpracuje sekvenčně. Žádný další kód není potřeba.

## Krok 3 – Spuštění rozpoznání a **extrakce textu z tiff**

S připraveným enginem a načteným obrázkem spustíme operaci OCR. Metoda `Recognize` vrací `OcrResult`, který obsahuje prostý text, skóre důvěry a podrobnosti o čase.

```csharp
        // Perform the OCR operation.
        OcrResult result = engine.Recognize();
```

**Zvládání okrajových případů:**  
Pokud není GPU k dispozici, `engine.Recognize()` stále funguje, protože engine tiše přepne na CPU. Po rozpoznání můžete zkontrolovat `engine.Device`, pokud potřebujete zaznamenat, které zařízení bylo skutečně použito.

## Krok 4 – Získání rozpoznaného prostého textu

Extrahování textu je jednoduché — stačí přečíst vlastnost `Text`. Zde konečně **extrahujete text z tiff** (nebo jakéhokoli jiného obrázku) a předáte jej uživateli.

```csharp
        // Output the plain text that was extracted.
        Console.WriteLine($"Text:\n{result.Text}");
```

Uvidíte surové znaky, přičemž zalomení řádků jsou zachována tak, jak jsou v původním obrázku. Pro strukturovanější výstup (např. JSON nebo CSV) můžete prozkoumat `result.Regions` a `result.Lines`, ale prostý text obvykle stačí pro rychlé skripty.

## Krok 5 – Měření doby zpracování a ošetření přepnutí na GPU

Výkon je důležitý, zejména když zpracováváte desítky stránek. Vlastnost `ProcessingTime` vám přesně řekne, jak dlouho OCR trvalo, ať už běželo na GPU nebo CPU.

```csharp
        // Show how long the recognition took.
        Console.WriteLine($"Time elapsed: {result.ProcessingTime.TotalSeconds}s");
    }
}
```

**Proč by vás to mělo zajímat:**  
Pokud si všimnete, že čas roste, můžete upravit `GpuMemoryLimit` nebo výslovně přepnout na CPU (`Device = OcrDevice.Cpu`). Naopak, výsledek pod sekundu u velkého TIFFu znamená, že akcelerace GPU dělá svou práci.

## Kompletní, připravený příklad

Zkopírujte níže uvedený kód do nového konzolového projektu (`dotnet new console -n OcrDemo`) a spusťte `dotnet add package Aspose.OCR`. Pak nahraďte `YOUR_DIRECTORY/sample_multi_page.tif` cestou k vašemu obrázku.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // Step 1: Initialize the OCR engine with GPU preference.
        OcrEngine engine = new OcrEngine
        {
            Device = OcrDevice.Gpu,
            GpuMemoryLimit = 1024
        };

        // Step 2: Load image for OCR (supports TIFF, PNG, JPEG, etc.).
        engine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/sample_multi_page.tif");

        // Step 3: Run recognition – this will also **extract text from tiff**.
        OcrResult result = engine.Recognize();

        // Step 4: Retrieve and display the recognized plain text.
        Console.WriteLine($"Text:\n{result.Text}");

        // Step 5: Display how long the operation took.
        Console.WriteLine($"Time elapsed: {result.ProcessingTime.TotalSeconds}s");
    }
}
```

**Očekávaný výstup (zkrácený pro stručnost):**

```
Text:
Invoice #12345
Date: 2026-05-01
Total: $1,250.00
...
Time elapsed: 1.42s
```

Pokud váš počítač nemá výkonnou GPU, může být uplynulý čas o několik sekund delší, ale text bude stále správně extrahován.

## Časté otázky a úskalí

- **Co když je obrázek obrovský (více než 10 MB)?**  
  Snižte jeho rozlišení před předáním enginu, nebo zvýšte `GpuMemoryLimit`, pokud máte dostatek VRAM.  
- **Mohu zpracovávat více obrázků v cyklu?**  
  Rozhodně. Stačí znovu použít stejnou instanci `OcrEngine` a při každé iteraci přiřadit nový `ImageStream`.  
- **Musím něco uvolňovat?**  
  `OcrEngine` implementuje `IDisposable`. Zabalte jej do `using` bloku pro čistou správu zdrojů, zejména při práci s GPU prostředky.  

```csharp
using (OcrEngine engine = new OcrEngine { Device = OcrDevice.Gpu })
{
    // ... same steps as before
}
```

- **Co jazykové varianty kromě angličtiny?**  
  Nastavte `engine.Language = OcrLanguage.Spanish` (nebo jakýkoli podporovaný jazyk) před voláním `Recognize()`.  

## Závěr

Nyní máte kompletní, end‑to‑end řešení, které **rozpozná text z obrázku** v C# pomocí Aspose OCR. Tutoriál ukázal, jak **načíst obrázek pro OCR**, jak **extrahovat text z tiff**, a jak měřit výkon při elegantním přepínání mezi GPU a CPU.

Odtud můžete:

- Experimentovat s různými formáty obrázků (BMP, PDF) a sledovat, jak je Aspose zpracuje.  
- Prozkoumat `result.Regions` pro data o ohraničujících rámečcích, pokud potřebujete rozvržení‑citlivé informace.

## Co byste se měli naučit dál?

- [How to Use Aspose to Recognize Image from Stream in OCR Image Recognition](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [Extract Text from Image – Recognize Line with Aspose.OCR](/ocr/english/net/image-and-drawing-recognition/recognize-line/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}