---
category: general
date: 2026-03-07
description: Naučte se, jak vyrovnat zkosení obrazu, zvýšit kontrast a extrahovat
  text ze skenu pomocí Aspose OCR. Proveďte OCR na obrázku s kompletním příkladem
  v C# a snadno načtěte obrázek pro OCR.
draft: false
keywords:
- how to deskew image
- extract text from scan
- how to boost contrast
- perform ocr on image
- load image for OCR
language: cs
og_description: Naučte se, jak vyrovnat zkosení obrázku, zvýšit kontrast a extrahovat
  text ze skenu pomocí Aspose OCR v C#. Proveďte OCR na obrázku pomocí kódu krok za
  krokem.
og_title: Jak vyrovnat obrázek a spustit OCR v C# – Kompletní průvodce
tags:
- C#
- OCR
- Image Processing
title: Jak narovnat obrázek a spustit OCR v C# – kompletní průvodce
url: /cs/net/ocr-optimization/how-to-deskew-image-and-run-ocr-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak vyrovnat obrázek a spustit OCR v C# – Kompletní průvodce

Pokud jste se někdy ptali, **jak vyrovnat obrázek** před spuštěním OCR, jste na správném místě. V tomto tutoriálu vás provedeme zvýšením kontrastu, načtením obrázku pro OCR a nakonec **extrahováním textu ze skenu** pomocí Aspose OCR.  

Ať už digitalizujete staré účtenky, čistíte naskenované smlouvy, nebo jen potřebujete spolehlivý způsob, jak přečíst text ze šikmé fotografie, níže uvedené kroky pokrývají vše, co potřebujete. Žádné zbytečnosti – jen funkční příklad, který můžete zkopírovat a vložit do Visual Studio.  

## Co dosáhnete

Na konci tohoto průvodce budete schopni:

* Opravit sklon až do 30° (to je část **jak vyrovnat obrázek**).  
* Zvýšit kontrast obrázku pro ostřejší hrany znaků (**jak zvýšit kontrast**).  
* Načíst svůj obrázek do OCR enginu (**načíst obrázek pro OCR**).  
* Spustit proces rozpoznávání a **extrahovat text ze skenu**.  

Vše funguje s nejnovějším balíčkem Aspose.OCR .NET NuGet (v23.11 v době psaní).  

---

![Příklad vyrovnání obrázku](/images/deskew-example.png "jak vyrovnat obrázek")

*Obrázek výše ukazuje naskenovaný dokument před a po vyrovnání.*

## Požadavky

* .NET 6.0 nebo novější (kód také běží na .NET Framework 4.7+).  
* Visual Studio 2022 (nebo jakékoli C# IDE, které máte rádi).  
* Aspose.OCR NuGet balíček – nainstalujte pomocí `dotnet add package Aspose.OCR`.  

To je vše. Žádné externí služby, žádné API klíče.

---

## Jak vyrovnat obrázek pomocí Aspose OCR

První věc, kterou uděláme, je vytvořit **ImageProcessingPipeline** a přidat `DeskewFilter`. Filtr automaticky detekuje dominantní úhel textové řádky a otočí obrázek zpět do vodorovné polohy.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

// Create the OCR engine
var ocrEngine = new OcrEngine();

// Build a pipeline – Deskew is the first filter
var processingPipeline = new ImageProcessingPipeline()
    .Add(new DeskewFilter { MaxAngle = 30 })   // how to deskew image up to 30°
    .Add(new DenoiseFilter { Level = DenoiseLevel.High }) // remove noise
    .Add(new ContrastBoostFilter { Strength = 1.5 })      // how to boost contrast
    .Add(new BinarizationFilter { Method = BinarizationMethod.Sauvola }); // binarize

// Attach the pipeline to the engine
ocrEngine.Settings.ImageProcessing = processingPipeline;
```

**Proč je to důležité:**  
Šikmý sken zmátne OCR engine, protože znaky již nejsou zarovnané s osnovou. `DeskewFilter` analyzuje histogram obrázku, najde úhel a otočí jej, což dramaticky zlepšuje přesnost rozpoznávání.

> **Tip:** Pokud víte, že vaše dokumenty nikdy nepřesahují sklon 15°, nastavte `MaxAngle = 15` pro zrychlení zpracování.

---

## Jak zvýšit kontrast pro lepší rozpoznávání

Po vyrovnání je dalším krokem udělat text výraznější. `ContrastBoostFilter` roztahuje rozsah intenzity pixelů, což je zvláště užitečné u vybledlých tisků.

```csharp
// The ContrastBoostFilter is already in the pipeline above.
// You can tweak the Strength value (1.0 = no change, >1.0 = stronger boost)
.Add(new ContrastBoostFilter { Strength = 1.5 })
```

**Proč to pomáhá:**  
Nízkokontrastní skeny produkují šedivé znaky, které binarizér může interpretovat jako pozadí. Zvýšení kontrastu posouvá tmavé pixely tmavěji a světlé pixely světleji, čímž poskytuje `BinarizationFilter` čistší podklad.

---

## Proveďte OCR na obrázku – načtení souboru

Nyní, když je obrázek předzpracován, musíme **načíst obrázek pro OCR**. Aspose nabízí pohodlný pomocník `ImageStream.FromFile`.

```csharp
// Load the source image – replace the path with your own file
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/skewed_noisy.jpg");
```

Pokud váš obrázek existuje ve streamu (např. nahraný přes webové API), můžete místo toho použít `ImageStream.FromStream(yourStream)`. Engine přijímá BMP, JPEG, PNG, TIFF a mnoho dalších formátů.

---

## Spusťte proces rozpoznávání a extrahujte text ze skenu

Se vším připraveným, volání `Recognize()` udělá těžkou práci. Po volání je rozpoznaný text dostupný přes `ocrEngine.Text`.

```csharp
// Run OCR
ocrEngine.Recognize();

// Output the result
Console.WriteLine("=== Extracted Text ===");
Console.WriteLine(ocrEngine.Text);
```

**Očekávaný výstup** (příklad pro jednoduchou fakturu):

```
=== Extracted Text ===
Invoice #12345
Date: 03/05/2026
Total: $1,250.00
Thank you for your business!
```

Pokud výstup vypadá poškozeně, zkontrolujte pořadí pipeline – nejprve deskew, pak denoise, zvýšení kontrastu a nakonec binarizaci. Přehazování těchto kroků může výsledek zhoršit.

---

## Časté problémy a okrajové případy

| Problém | Proč se vyskytuje | Řešení |
|---------|-------------------|--------|
| **Prázdný výsledek** | Obrázek je příliš tmavý nebo příliš světlý pro výchozí binarizační metodu. | Zvyšte `ContrastBoostFilter.Strength` nebo přepněte na `BinarizationMethod.Otsu`. |
| **Chybějící část textu** | Po denoisingu zůstává šum. | Použijte `DenoiseLevel.Medium` pro mírnější obrázky, nebo přidejte druhý `DenoiseFilter`. |
| **Špatný směr otáčení** | Dokument má smíšenou orientaci (např. foto otočené stránky). | Manuálně nastavte nižší `DeskewFilter.MaxAngle` a předem otočte obrázek pomocí `ImageProcessor.Rotate`. |
| **Zpomalení výkonu** | Velká dávka vysoce rozlišených obrázků. | Před pipeline zmenšete rozlišení (`ImageProcessor.Resize`) nebo zpracovávejte paralelně (`Parallel.ForEach`). |

---

## Kompletní funkční příklad (připravený ke kopírování)

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // 1️⃣ Create OCR engine
        var ocrEngine = new OcrEngine();

        // 2️⃣ Build image‑processing pipeline
        var processingPipeline = new ImageProcessingPipeline()
            .Add(new DeskewFilter { MaxAngle = 30 })                     // how to deskew image up to 30°
            .Add(new DenoiseFilter { Level = DenoiseLevel.High })       // remove high‑level noise
            .Add(new ContrastBoostFilter { Strength = 1.5 })            // how to boost contrast
            .Add(new BinarizationFilter { Method = BinarizationMethod.Sauvola }); // binarize image

        // 3️⃣ Attach pipeline to OCR settings
        ocrEngine.Settings.ImageProcessing = processingPipeline;

        // 4️⃣ Load the image you want to OCR
        // Replace the path with the location of your own file
        ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/skewed_noisy.jpg");

        // 5️⃣ Run the recognition engine
        ocrEngine.Recognize();

        // 6️⃣ Display the extracted text
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrEngine.Text);
    }
}
```

Uložte tento soubor jako `Program.cs`, spusťte `dotnet run` a sledujte, jak konzole vytiskne výsledek **extrahování textu ze skenu**.  

---

## Další kroky a související témata

* **Dávkové zpracování** – Zabalte výše uvedenou logiku do smyčky pro zpracování desítek souborů.  
* **Vlastní jazykové balíčky** – Pokud potřebujete číst ne‑latinské skripty, načtěte jazykový model pomocí `ocrEngine.Settings.Language = OcrLanguage.ChineseSimplified;`.  
* **PDF výstup** – Kombinujte Aspose.PDF s OCR pro vložení prohledávatelného textu přímo do PDF souboru.  
* **Ladění výkonu** – Experimentujte s pořadím `ImageProcessingPipeline`; někdy denoising před deskewem přináší rychlejší výsledky u špinavých fotografií.  

Všechny tyto body staví na základních konceptech, které jsme probrali: **jak vyrovnat obrázek**, **jak zvýšit kontrast**, **načíst obrázek pro OCR**, **provést OCR na obrázku** a nakonec **extrahovat text ze skenu**.

---

## Závěr

Právě jsme ukázali kompletní, produkčně připravený způsob, jak **vyrovnat obrázek** a spustit OCR v C#. Řetězením filtru pro deskew, kroku denoise, zvýšení kontrastu a binarizéru získáte čistý vstup, který umožní Aspose OCR spolehlivě **extrahovat text ze skenu**.  

Vyzkoušejte kód, upravte parametry filtrů pro své dokumenty a uvidíte, jak rychle se zlepší přesnost rozpoznávání. Máte otázky? Zanechte komentář a šťastné programování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}