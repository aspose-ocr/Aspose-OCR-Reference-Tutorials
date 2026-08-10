---
category: general
date: 2026-03-17
description: Jak rychle provádět hromadné OCR PNG obrázků v C#. Naučte se extrahovat
  text z PNG souborů, převádět PNG na text a číst obrázky z adresáře pomocí jednoduchého
  skriptu.
draft: false
keywords:
- how to batch OCR
- extract text png
- convert png to text
- read images from directory
language: cs
og_description: Jak dávkově provádět OCR PNG obrázků v C# pomocí krok‑za‑krokem kódu.
  Extrahujte text z PNG souborů, převádějte PNG na text a snadno načítejte obrázky
  z adresáře.
og_title: Jak dávkově provádět OCR PNG obrázků v C# – kompletní průvodce
tags:
- OCR
- C#
- Image Processing
title: Jak dávkově provádět OCR PNG obrázků v C# – Kompletní průvodce
url: /cs/net/text-recognition/how-to-batch-ocr-png-images-in-c-complete-guide/
---

code or placeholders.

Now produce final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak hromadně provádět OCR PNG obrázků v C# – Kompletní průvodce

Už jste se někdy zamysleli nad tím, **jak hromadně provádět OCR** na složku plnou snímků obrazovky, aniž byste otevírali každý soubor ručně? Nejste jediní – vývojáři se neustále ptají, jak hromadně provádět OCR velkých kolekcí PNG, zejména když je cílem **extrahovat text z PNG** souborů pro následnou analýzu.  

V tomto tutoriálu projdeme připravený spustitelný C# příklad, který **extrahuje text z PNG** souborů, **převádí PNG na text** a ukáže vám nejlepší způsob, jak **číst obrázky ze složky**. Na konci budete mít jediný skript, který vytvoří soubor `.txt` vedle každého obrázku, čímž vám ušetří hodiny ručního kopírování‑vkládání.

## Co dosáhnete

- Inicializovat OCR engine jednou a znovu jej použít pro celý batch.  
- Prohledat každý `*.png` v dané složce, aniž byste museli psát smyčku sami.  
- Zapsat každý OCR výsledek do vlastního textového souboru, zachovávající původní název souboru.  
- Elegantně ošetřit běžné okrajové případy, jako jsou prázdné složky nebo soubory, které nejsou obrázky.

### Požadavky

- .NET 6.0 nebo novější (kód funguje také na .NET Core a .NET Framework).  
- OCR knihovna, která poskytuje typy `OcrEngine`, `ImageStream` a `OcrResult` (například fiktivní **FastOCR** SDK použité ve výpisech).  
- Základní znalost C# – není potřeba pokročilé vzory.

---

## Jak hromadně provádět OCR PNG obrázků – Přehled

Níže je **kompletní, spustitelný program**. Klidně jej zkopírujte a vložte do nového konzolového projektu, nahraďte zástupné cesty a stiskněte **F5**.

```csharp
using System;
using System.IO;
using System.Linq;
using FastOCR;               // <-- Replace with your actual OCR namespace

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Initialize the OCR engine (language = English)
        // -------------------------------------------------
        var ocrEngine = new OcrEngine();
        ocrEngine.Config.Language = Language.English;

        // -------------------------------------------------
        // Step 2: Locate every PNG file in the input folder
        // -------------------------------------------------
        string inputFolder = @"YOUR_DIRECTORY\images";
        string[] imagePaths = Directory.GetFiles(inputFolder, "*.png");

        if (imagePaths.Length == 0)
        {
            Console.WriteLine("No PNG files found – nothing to process.");
            return;
        }

        // -------------------------------------------------
        // Step 3: Convert file paths to ImageStream objects
        // -------------------------------------------------
        var imageStreams = imagePaths
            .Select(path => ImageStream.FromFile(path))
            .ToList();

        // -------------------------------------------------
        // Step 4: Recognize text in the entire batch
        // -------------------------------------------------
        IReadOnlyList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);

        // -------------------------------------------------
        // Step 5: Write each result to a .txt file next to the image
        // -------------------------------------------------
        string outputFolder = @"YOUR_DIRECTORY\output";
        Directory.CreateDirectory(outputFolder); // ensures the folder exists

        for (int i = 0; i < ocrResults.Count; i++)
        {
            string originalFileName = Path.GetFileNameWithoutExtension(imagePaths[i]);
            string outputPath = Path.Combine(outputFolder, $"{originalFileName}.txt");
            File.WriteAllText(outputPath, ocrResults[i].Text);
            Console.WriteLine($"✅ {originalFileName}.txt created");
        }

        Console.WriteLine("All done! Check the output folder for your text files.");
    }
}
```

> **Očekávaný výstup:** Pro každý `image01.png` najdete `image01.txt` obsahující rozpoznané znaky. Konzole vypíše každý soubor při jeho zápisu.

![Diagram hromadného OCR](how-to-batch-ocr-diagram.png "Diagram ilustrující hromadné OCR PNG obrázků pomocí C#")

---

## Krok‑za‑krokem vysvětlení

### 1. Inicializace OCR Engine – srdce procesu  

Řádek `var ocrEngine = new OcrEngine();` vytvoří jedinou instanci engine, která bude znovu použita pro celý batch. Opětovné používání engine je **klíčové**, protože většina OCR knihoven alokuje těžké zdroje (např. jazykové modely) při konstrukci. Jednorázová inicializace dramaticky zlepšuje výkon – zejména když máte desítky nebo stovky PNG.  

> **Pro tip:** Pokud potřebujete jazyk jiný než angličtinu, nastavte `ocrEngine.Config.Language = Language.Spanish;` (nebo jakýkoli podporovaný enum).  

### 2. Čtení obrázků ze složky – nalezení každého PNG  

`Directory.GetFiles(@"YOUR_DIRECTORY\images", "*.png")` dělá přesně to, co slibuje sekundární klíčové slovo *read images from directory*. Vrací pole absolutních cest, které později předáme OCR engine.  

> **Proč nepoužít `SearchOption.AllDirectories`?** Pokud jsou vaše obrázky vnořené, můžete přepnout na `GetFiles(path, "*.png", SearchOption.AllDirectories)`. Jen si pamatujte, že hlubší skenování může přinést nechtěné soubory, takže je vhodné filtrovat.  

### 3. Převod cest k souborům na objekty ImageStream  

Většina OCR SDK očekává stream místo surové cesty. LINQ výraz `Select(path => ImageStream.FromFile(path)).ToList()` vytvoří **seznam streamů**, který batch rozpoznávač může zpracovat jedním voláním. Tento krok také zajišťuje, že souborové handly jsou otevřeny jen jednou, což snižuje I/O zátěž.  

> **Okrajový případ:** Pokud je soubor poškozený, `ImageStream.FromFile` může vyhodit výjimku. Zabalte převod do `try/catch`, pokud potřebujete odolnost.  

### 4. Rozpoznání textu v celém batchi  

`ocrEngine.RecognizeBatch(imageStreams)` je ideální řešení pro *how to batch OCR*. Místo procházení každého obrázku a volání metody pro jeden obrázek předáme celé kolekci engine. Interně může knihovna paralelizovat práci, což vám poskytne zvýšení rychlosti na vícejádrových strojích.  

> **Tip:** Pokud vaše OCR knihovna neexponuje batch metodu, můžete dosáhnout podobného výkonu pomocí `Parallel.ForEach` kolem volání `Recognize` pro jeden obrázek.  

### 5. Zápis každého OCR výsledku – převod PNG na text  

Poslední `for` smyčka zapisuje `ocrResults[i].Text` do souboru `.txt`, jehož název odráží původní PNG. To je přesně to, co popisuje sekundární klíčové slovo *convert PNG to text*. Volání `Path.Combine` zajišťuje, že výstupní složka existuje a zabraňuje chybám při průchodu cestou.  

> **Častá chyba:** Zapomenutí vytvořit výstupní adresář nejprve způsobí `DirectoryNotFoundException`. Řádek `Directory.CreateDirectory(outputFolder);` to předem řeší.  

---

## Řešení reálných variací

| Situace | Co změnit | Proč |
|-----------|----------------|-----|
| **Prázdná vstupní složka** | Ponechat počáteční kontrolu `if (imagePaths.Length == 0)` | Zabrání zbytečnému volání OCR a zobrazí přátelskou zprávu |
| **Smíšené typy souborů** | Use `Directory.EnumerateFiles(..., "*.*", SearchOption.TopDirectoryOnly).Where(f => f.EndsWith(".png", StringComparison.OrdinalIgnoreCase))` | Zaručuje, že zpracujete jen PNG, což splňuje *extract text png* bez chyb |
| **Obrovské obrázky ( > 5 MB )** | Downscale before feeding to OCR: `ImageStream.FromFile(path).Resize(1920, 1080)` (if API supports) | Snižuje zatížení paměti a často zlepšuje přesnost rozpoznání |
| **Jiný OCR jazyk** | Set `ocrEngine.Config.Language = Language.French;` | Nastaví engine na jazyk zdrojových obrázků |

---

## Často kladené otázky (FAQ)

**Q: Funguje to i s JPEG nebo TIFF soubory?**  
A: Základní logika zůstává stejná; stačí změnit vzor vyhledávání na `"*.jpg"` nebo `"*.tif"` a zajistit, aby OCR knihovna dokázala tyto formáty dekódovat.

**Q: Jak mohu zpracovat tisíce obrázků, aniž bych vyčerpával paměť?**  
A: Nahraďte batch volání streamingovým přístupem – zpracovávejte po částech, například po 50 obrázcích najednou, a uvolněte streamy před načtením další části.

**Q: Potřebuji skóre důvěryhodnosti OCR. Kde ho najdu?**  
A: Většina objektů `OcrResult` poskytuje vlastnost `Confidence`. Můžete rozšířit krok zápisu:

```csharp
var result = ocrResults[i];
string content = $"Confidence: {result.Confidence:P2}\n{result.Text}";
File.WriteAllText(outputPath, content);
```

---

## Závěr

Právě jsme prošli **jak hromadně provádět OCR** PNG obrázky v C# od začátku do konce. Inicializací jediného engine, čtením obrázků ze složky, převodem na streamy, rozpoznáním celého batche a nakonec zápisem každého výsledku do textového souboru máte nyní solidní, připravený pro produkci vzor pro úkoly **extrahovat text z PNG**, **převádět PNG na text** a **číst obrázky ze složky**.  

Co dál? Zkuste vyměnit OCR poskytovatele, přidat vícevláknové post‑zpracování (např. kontrolu pravopisu), nebo nasměrovat `.txt` soubory do vyhledávacího indexu. Možnosti jsou neomezené, jakmile ovládnete batch workflow.  

Máte vlastní nápad, který chcete sdílet? Zanechte komentář a šťastné kódování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}