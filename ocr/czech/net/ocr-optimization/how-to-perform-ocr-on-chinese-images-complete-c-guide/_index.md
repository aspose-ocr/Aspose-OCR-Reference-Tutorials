---
category: general
date: 2026-03-07
description: Jak provést OCR na čínských obrázcích pomocí Aspose OCR. Naučte se extrahovat
  čínský text, převést obrázek na ePub a zlepšit přesnost OCR v jednom tutoriálu.
draft: false
keywords:
- how to perform OCR
- extract chinese text
- convert image to epub
- how to improve OCR
- recognize simplified chinese
language: cs
og_description: Jak provést OCR čínských obrázků pomocí Aspose OCR. Získejte kód krok
  za krokem pro extrakci čínského textu, vylepšení OCR a export do ePub.
og_title: Jak provést OCR na čínských obrázcích – kompletní průvodce C#
tags:
- OCR
- C#
- Aspose
title: Jak provést OCR na čínských obrázcích – Kompletní průvodce C#
url: /cs/net/ocr-optimization/how-to-perform-ocr-on-chinese-images-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak provádět OCR na čínských obrázcích – Kompletní průvodce v C#  

Už jste se někdy zamysleli **jak provádět OCR** na obrázku, který obsahuje čínské znaky? Nejste v tom jediní. V mnoha aplikacích – skenování účtenek, digitalizace učebnic nebo tvorba vícejazykového vyhledávače – získání čistého textu z obrázku je klíčová funkce.  

V tomto tutoriálu projdeme reálné řešení, které **extrahuje čínský text**, uloží výsledek do souboru prostého textu a dokonce **převede obrázek na ePub** pro e‑čtečky. Po cestě budeme diskutovat **jak zlepšit přesnost OCR**, proč byste měli zapnout režim GPU a co je potřeba udělat, aby **rozpoznával zjednodušenou čínštinu** správně.  

Na konci tohoto průvodce budete mít plně spustitelný program v C#, několik praktických tipů a jasnou představu o dalších krocích, které můžete podniknout (např. přidání detekce jazyka nebo dávkové zpracování). Žádná externí dokumentace není potřeba – vše, co potřebujete, je zde.  

## Co budete potřebovat  

- .NET 6+ (nebo .NET Core 3.1 s Aspose OCR for .NET)  
- Platná licence Aspose OCR for .NET (bezplatná zkušební verze funguje pro experimentování)  
- Soubor obrázku, který obsahuje zjednodušené čínské znaky (např. `chinese_sample.jpg`)  
- Visual Studio 2022 nebo jakýkoli C# editor, který preferujete  

Pokud vám něco chybí, stáhněte si nyní balíček NuGet:

```bash
dotnet add package Aspose.OCR
```

A to je vše – žádné další nativní knihovny, žádný COM interop, jen jediný .NET balíček.

## Jak provádět OCR – Nastavení enginu Aspose OCR  

Prvním krokem je vytvořit a nakonfigurovat OCR engine. Tento krok je zásadní, protože nastavení enginu určuje **jak dobře OCR funguje** na čínských znacích a jak rychle běží.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using Aspose.OCR.Export;

// Step 1: Initialise the OCR engine with Chinese‑specific settings
var ocrEngine = new OcrEngine
{
    Settings =
    {
        // Primary language – Simplified Chinese
        Language = Language.ChineseSimplified,

        // Use GPU when available for a noticeable speed boost
        EngineMode = EngineMode.Gpu,

        // Build a processing pipeline to clean up the image first
        ImageProcessing = new ImageProcessingPipeline()
            .Add(new DeskewFilter()) // Fix rotation
            .Add(new BinarizationFilter
            {
                Method = BinarizationMethod.Sauvola // Improves contrast for Chinese glyphs
            })
    }
};
```

**Proč je to důležité:**  
- **Language = ChineseSimplified** říká Aspose načíst sadu znaků pro zjednodušenou čínštinu, což dramaticky snižuje chyby rozpoznávání.  
- **EngineMode.Gpu** může zkrátit dobu zpracování na polovinu na moderním GPU, ale v případě absence GPU se elegantně přepne na CPU.  
- **DeskewFilter** odstraňuje náklon, který se často objeví, když uživatelé pořizují fotografii telefonem.  
- **Sauvola binarization** vytvoří vysoce kontrastní černobílý obrázek, klasický trik pro zvýšení přesnosti OCR u hustých skriptů jako čínština.  

> **Pro tip:** Pokud pracujete s fotografiemi při slabém osvětlení, přidejte `ContrastFilter` před binarizací. Není to pro náš příklad vyžadováno, ale často vám ušetří několik problémů.  

![Diagram pipeline OCR](ocr-pipeline.png "Diagram pipeline OCR")  

> *Alt text:* Diagram pipeline OCR  

## Extrahovat čínský text z obrázku  

Nyní, když je engine připraven, načteme obrázek a necháme engine udělat své kouzlo. Toto je jádro **extrahování čínského textu**.

```csharp
// Step 2: Load the image you want to recognize
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/chinese_sample.jpg");

// Step 3: Run the recognition process
ocrEngine.Recognize();

// Step 4: Grab the recognized string
string recognizedText = ocrEngine.Text;

// Optional: Write the text to a .txt file for later analysis
File.WriteAllText(@"YOUR_DIRECTORY/out.txt", recognizedText);
```

**Co byste měli vidět:**  
Pokud `chinese_sample.jpg` obsahuje frázi “中华人民共和国”， soubor `out.txt` bude obsahovat přesně tyto znaky – žádné extra mezery, žádná poškozená latinská písmena.  

### Časté úskalí  

| Problém | Proč se to děje | Řešení |
|-------|----------------|-----|
| Chybějící znaky | Obrázek je příliš šumivý | Přidejte `MedianFilter` před binarizací |
| Detekováno špatné jazykové nastavení | `Language` nastaven na `English` | Zajistěte `Language = Language.ChineseSimplified` |
| Pomalé zpracování | GPU není povoleno | Ověřte, že váš počítač má kompatibilní CUDA driver |

## Převést obrázek na ePub  

Mnoho vývojářů se ptá, *„Mohu převést naskenovanou stránku na čitelnou e‑knihu?“* Rozhodně – Aspose OCR obsahuje exportér do ePub. To splňuje požadavek **convert image to epub**.

```csharp
// Step 5: Export the OCR result as an ePub file
ocrEngine.ExportToEpub(
    @"YOUR_DIRECTORY/out.epub",
    new EpubExportOptions { Title = "Chinese Sample" });
```

Vygenerovaný `out.epub` bude obsahovat extrahovaný čínský text, správně kódovaný v UTF‑8, a lze jej otevřít v Kindle, Apple Books nebo jakémkoli ePub čtečce.  

**Proč používat ePub?**  
- Je to reflowable (přizpůsobitelný), takže čtenáři mohou měnit velikost písma, aniž by se rozbil layout.  
- Formát udržuje text prohledávatelný, což je užitečné pro pozdější indexování.  

## Jak zlepšit OCR – Praktické úpravy  

I když máte solidní pipeline, můžete stále vidět občasné chyby rozpoznávání. Zde je rychlý kontrolní seznam pro **jak zlepšit OCR** na čínských dokumentech:

1. **Předzpracování obrázku** – Použijte `GaussianBlurFilter` k vyhlazení šumů, poté `ContrastFilter` pro zvýraznění hran.  
2. **Nastavte vyšší DPI** – Pokud řídíte proces skenování, cílem by mělo být 300 dpi nebo více; obrázky s nízkým rozlišením ztrácejí detaily tahů.  
3. **Povolit detekci jazyka** – Aspose může automaticky detekovat jazyk; kombinujte to s fallbackem na zjednodušenou čínštinu, pokud detekce selže.  
4. **Doladit binarizaci** – Vyměňte `Sauvola` za `Otsu`, pokud je pozadí rovnoměrně světlé.  
5. **Dávkové zpracování** – Zpracovávejte více stránek paralelně pomocí `Parallel.ForEach` k využití vícejádrových CPU.  

```csharp
// Example: Adding a Gaussian blur before binarization
ocrEngine.Settings.ImageProcessing
    .Add(new GaussianBlurFilter { Radius = 1.2 })
    .Add(new BinarizationFilter { Method = BinarizationMethod.Otsu });
```

## Rozpoznat zjednodušenou čínštinu – Okrajové případy  

Fráze **recognize simplified Chinese** často zmátne nováčky, protože stejný OCR engine může také zpracovávat tradiční čínštinu, japonštinu nebo korejštinu. Aby bylo chování deterministické:

- **Explicitně nastavte jazyk** (jak jsme udělali v kroku 1).  
- **Vyhněte se stránkám s míseným jazykem**; pokud stránka kombinuje zjednodušenou čínštinu s angličtinou, zvažte dva průchody: jeden s `Language.ChineseSimplified`, druhý s `Language.English`.  
- **Ověřte výstup** – Po rozpoznání spusťte jednoduchý regex, aby se zajistilo, že všechny znaky spadají do Unicode rozsahu `\u4E00‑\u9FFF`.  

```csharp
bool IsSimplifiedChinese(string text)
{
    return System.Text.RegularExpressions.Regex.IsMatch(
        text, @"^[\u4E00-\u9FFF\s]+$");
}
```

Pokud kontrola selže, můžete stránku zaznamenat pro ruční revizi.

## Kompletní funkční příklad  

Spojením všech částí dohromady, zde je jediný soubor, který můžete zkopírovat a vložit do nového konzolového projektu (`Program.cs`). Obsahuje všechny kroky, volitelné úpravy a závěrečnou stavovou řádku.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Filters;
using Aspose.OCR.Export;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Initialise OCR engine – Chinese‑specific settings
        // -------------------------------------------------
        var ocrEngine = new OcrEngine
        {
            Settings =
            {
                Language = Language.ChineseSimplified,
                EngineMode = EngineMode.Gpu,
                ImageProcessing = new ImageProcessingPipeline()
                    .Add(new DeskewFilter())
                    .Add(new BinarizationFilter
                    {
                        Method = BinarizationMethod.Sauvola
                    })
            }
        };

        // -------------------------------------------------
        // 2️⃣ Load image and run recognition
        // -------------------------------------------------
        string imgPath = @"YOUR_DIRECTORY/chinese_sample.jpg";
        ocrEngine.Image = ImageStream.FromFile(imgPath);
        ocrEngine.Recognize();

        // -------------------------------------------------
        // 3️⃣ Save plain‑text output
        // -------------------------------------------------
        string txtPath = @"YOUR_DIRECTORY/out.txt";
        File.WriteAllText(txtPath, ocrEngine.Text);
        Console.WriteLine($"✅ Text saved to {txtPath}");

        // -------------------------------------------------
        // 4️⃣ Export to ePub
        // -------------------------------------------------
        string epubPath = @"YOUR_DIRECTORY/out.epub";
        ocrEngine.ExportToEpub(epubPath,
            new EpubExportOptions { Title = "Chinese Sample" });
        Console.WriteLine($"✅ ePub generated at {epubPath}");

        // -------------------------------------------------
        // 5️⃣ Quick verification – length and charset
        // -------------------------------------------------
        Console.WriteLine($"Done – extracted text length: {ocrEngine.Text.Length}");
        Console.WriteLine($"Contains only Simplified Chinese? " +
                          $"{IsSimplifiedChinese(ocrEngine.Text)}");
    }

    // Helper to ensure only Simplified Chinese characters were extracted
    static bool IsSimplifiedChinese(string text)
    {
        return System.Text.RegularExpressions.Regex.IsMatch(
            text, @"^[\u4E00-\u9FFF\s]+$");
    }
}
```

**Očekávaný výstup v konzoli (příklad):**

```
✅ Text saved to C:\Images\out.txt
✅ ePub generated at C:\Images\out.epub
Done – extracted text length: 128
Contains only Simplified Chinese? True
```

Spusťte program, otevřete `out.txt` nebo `out.epub` a uvidíte čisté, prohledávatelné čínské znaky připravené pro další zpracování.

## Závěr  

Právě jsme prošli **jak provádět OCR** na čínských obrázcích od začátku do konce, ukázali vám, jak **extrahovat čínský text**, **převést výsledek na ePub**, a aplikovat několik  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}