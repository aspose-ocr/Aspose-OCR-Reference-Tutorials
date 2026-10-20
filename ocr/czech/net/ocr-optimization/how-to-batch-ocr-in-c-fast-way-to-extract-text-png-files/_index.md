---
category: general
date: 2026-04-03
description: Naučte se provádět hromadné OCR pomocí Aspose.OCR v C#. Tento průvodce
  vám ukáže, jak extrahovat text z PNG obrázků a efektivně převádět obrázky na text.
draft: false
keywords:
- how to batch ocr
- extract text png
- convert images to text
- Aspose OCR
- C# parallel processing
language: cs
og_description: Objevte, jak provádět hromadné OCR v C# pro extrakci textu z PNG obrázků
  a převádět obrázky na text pomocí Aspose.OCR. Kompletní kód je zahrnut.
og_title: Jak provádět dávkové OCR v C# – rychlý průvodce
tags:
- OCR
- C#
- Aspose
title: Jak provádět dávkové OCR v C# – Rychlý způsob, jak extrahovat text z PNG souborů
url: /cs/net/ocr-optimization/how-to-batch-ocr-in-c-fast-way-to-extract-text-png-files/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak provádět hromadné OCR v C# – Rychlý způsob extrakce textu z PNG souborů

Už jste se někdy zamýšleli **jak provádět hromadné OCR** celé složky snímků obrazovky, aniž byste museli psát smyčku pro každý soubor? Nejste v tom sami. V mnoha projektech – například digitalizace faktur nebo archivace naskenovaných účtenek – skončíte s desítkami, někdy stovkami PNG souborů, ze kterých je potřeba získat text. Dobrá zpráva? S Aspose.OCR můžete **extrahovat text z PNG** obrázků paralelně a celý proces lze zabalit do několika řádků C#.

V tomto tutoriálu projdeme kompletním, připraveným příkladem, který vám ukáže, jak **převést obrázky na text** pomocí dávkového procesoru. Probereme předpoklady, vysvětlíme, proč je každá řádka důležitá, a přidáme i několik tipů, abyste se vyhnuli běžným úskalím.

## Předpoklady

Než se pustíme do kódu, ujistěte se, že máte:

- **.NET 6.0** (nebo novější) nainstalovaný na vašem počítači. Starší runtime fungují, ale nejnovější poskytuje lepší výkon a podporu async.
- **Aspose.OCR for .NET** balíček. Přidejte jej přes NuGet: `dotnet add package Aspose.OCR`.
- Složku plnou **PNG** obrázků, které chcete zpracovat. V průvodci ji budeme označovat jako `YOUR_DIRECTORY`.
- Přiměřené množství RAM – dávkové OCR může být náročné na paměť, pokud zvýšíte paralelismus, ale použití `Environment.ProcessorCount` to udrží v bezpečných mezích.

> **Tip:** Pokud pracujete v CI/CD pipeline, přidejte licenční soubor Aspose jako tajný klíč, abyste se vyhnuli limitu 20 stránek ve volné verzi.

Teď si můžeme popustit prsty.

## Krok 1: Nastavení dávkového OCR procesoru (Primary Keyword in Header)

Prvním, co potřebujete, je instance třídy `BatchOcrProcessor`. Tato třída abstrahuje logiku vláken a umožní vám soustředit se na to, co dělat s každým obrázkem.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class BatchDemo
{
    static void Main()
    {
        // Create a batch OCR processor and tell it to use all CPU cores
        var ocrBatch = new BatchOcrProcessor
        {
            Engine = new OcrEngine(),
            MaxDegreeOfParallelism = Environment.ProcessorCount
        };
```

**Proč je to důležité:**  
- `Engine = new OcrEngine()` vytvoří čerstvý OCR engine pro každé vlákno, čímž se zabrání soutěži o zdroje.  
- `MaxDegreeOfParallelism = Environment.ProcessorCount` se automaticky přizpůsobí počtu jader, což poskytne nejlepší možný propustnost bez ručního ladění.

## Krok 2: Připojení k událostem průběhu (Helps Track Extraction)

Sledování průběhu je nezbytné při zpracování stovek souborů. Událost `ProgressChanged` se spustí po dokončení každého souboru a umožní vám zaznamenat stav.

```csharp
        // Subscribe to progress updates so we know which file is being processed
        ocrBatch.ProgressChanged += (s, e) =>
            Console.WriteLine($"Processed {e.Current}/{e.Total}: {e.FilePath}");
```

**Proč to oceníte:**  
- Zpětná vazba v reálném čase zabraňuje otázkám, zda aplikace uvízla.  
- Pokud budete potřebovat pozastavit nebo zrušit běh, už máte hák, který vám umožní porovnat `e.Current` a `e.Total`.

## Krok 3: Definice skenování složky a vzoru souborů (Extract Text PNG)

Nyní řekneme procesoru, kde hledat a jaké soubory vybírat. Vzor `"*.png"` zajistí, že budeme zpracovávat jen PNG obrázky.

```csharp
        // Run OCR on every PNG image in the target folder
        ocrBatch.ProcessFolder(
            @"YOUR_DIRECTORY",          // folder containing the images
            "*.png",                    // file pattern
            (imagePath, ocrText) =>     // callback for each processed file
            {
                // Step 4 is inside this callback – see next section
            });
```

**Proč je to klíčové:**  
- Použití globálního vzoru udržuje kód flexibilní; změňte `*.png` na `*.jpg`, pokud budete později potřebovat JPEGy.  
- Callback získá jak cestu k obrázku, tak rozpoznaný text, takže máte plnou kontrolu nad dalším zpracováním.

## Krok 4: Uložení rozpoznaného textu vedle zdroje (Convert Images to Text)

Uvnitř callbacku zapíšeme výstup OCR do souboru `.txt`, který bude ležet přímo vedle původního PNG. Toto je nejjednodušší způsob, jak **převést obrázky na text** pro další zpracování.

```csharp
                // Save the recognized text next to the image as a .txt file
                string txtPath = Path.ChangeExtension(imagePath, ".txt");
                File.WriteAllText(txtPath, ocrText);
```

**Proč volíme soubor `.txt` vedle obrázku:**  
- Vztah je zřejmý – otevřete PNG, otevřete TXT, porovnejte.  
- V malých projektech není potřeba databáze ani další úložná vrstva.

## Krok 5: Závěrečné přátelské oznámení o dokončení

Úhledná zpráva v konzoli vám řekne, kdy je vše hotovo.

```csharp
        // Indicate that batch processing has finished
        Console.WriteLine("Batch processing completed.");
    }
}
```

Po spuštění programu uvidíte výstup podobný tomuto:

```
Processed 1/27: C:\Images\invoice1.png
Processed 2/27: C:\Images\invoice2.png
...
Batch processing completed.
```

Každý PNG nyní má sourozenecký `.txt` soubor obsahující extrahovaný text.

## Kompletní funkční příklad (Všechny kroky dohromady)

Níže je celý program, který můžete zkopírovat a vložit do nového konzolového projektu. Nic nechybí – jen nahraďte `YOUR_DIRECTORY` absolutní cestou k vašim obrázkům.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class BatchDemo
{
    static void Main()
    {
        // Step 1: Create a batch OCR processor and configure it to use all CPU cores
        var ocrBatch = new BatchOcrProcessor
        {
            Engine = new OcrEngine(),
            MaxDegreeOfParallelism = Environment.ProcessorCount
        };

        // Step 2: Subscribe to progress updates to see which file is being processed
        ocrBatch.ProgressChanged += (s, e) =>
            Console.WriteLine($"Processed {e.Current}/{e.Total}: {e.FilePath}");

        // Step 3: Run OCR on every PNG image in the target folder
        ocrBatch.ProcessFolder(
            @"C:\MyImages",          // folder containing the images
            "*.png",                // file pattern
            (imagePath, ocrText) => // callback for each processed file
            {
                // Step 4: Save the recognized text next to the image as a .txt file
                string txtPath = Path.ChangeExtension(imagePath, ".txt");
                File.WriteAllText(txtPath, ocrText);
            });

        // Step 5: Indicate that batch processing has finished
        Console.WriteLine("Batch processing completed.");
    }
}
```

### Očekávaný výsledek

- Pro každý `image.png` ve `C:\MyImages` se objeví `image.txt` vedle něj.  
- Konzole vypisuje řádky průběhu, což usnadňuje sledování velkých dávek.  
- Žádné ruční smyčky ani správa vláken – `BatchOcrProcessor` vše zařídí.

## Často kladené otázky a okrajové případy

### Co když moje obrázky nejsou PNG?

Stačí změnit druhý argument v `ProcessFolder` na `"*.jpg"` nebo `"*.*"`, aby se zahrnuly všechny soubory. OCR engine funguje s většinou rastrových formátů.

### Kolik paměti to spotřebuje?

`BatchOcrProcessor` načítá jeden obrázek na vlákno. Při `Environment.ProcessorCount` nastaveném například na 8 jader budete mít najednou osm obrázků v paměti. Pokud narazíte na výjimky OutOfMemory, snižte paralelismus:

```csharp
MaxDegreeOfParallelism = 4; // or any number that fits your machine
```

### Můžu si přizpůsobit jazyk OCR?

Určitě. Po vytvoření engine nastavte jeho vlastnost `Language`:

```csharp
Engine = new OcrEngine { Language = Language.English };
```

Aspose podporuje mnoho jazyků; v případě potřeby přidejte odpovídající NuGet balíček.

### Jak řešit chyby?

Obalte callback do `try/catch` bloku a logujte selhání. Procesor bude pokračovat dalším souborem, takže jeden poškozený obrázek neukončí celý běh.

```csharp
(imagePath, ocrText) =>
{
    try
    {
        string txtPath = Path.ChangeExtension(imagePath, ".txt");
        File.WriteAllText(txtPath, ocrText);
    }
    catch (Exception ex)
    {
        Console.Error.WriteLine($"Failed on {imagePath}: {ex.Message}");
    }
}
```

## Tipy pro škálování

- **Rozdělení složky**: Pokud máte desítky tisíc souborů, rozdělte je do podsložek a spusťte více dávkových úloh po sobě.  
- **Použijte cloudový VM**: Stroj s více jádry (např. 32‑core) dokončí úlohu výrazně rychleji. Nezapomeňte upravit licenční limity.  
- **Post‑processing textu**: Po extrakci můžete spustit regulární výrazy pro získání čísel faktur nebo dat. `.txt` soubory jsou ideálním vstupem pro takové pipeline.

## Závěr

Nyní máte solidní, připravený recept na **jak provádět hromadné OCR** adresáře PNG souborů, **extrahovat text z PNG** souborů a **převést obrázky na text** pomocí Aspose.OCR v C#. Příklad je samostatný, vysvětluje „proč“ za každou řádkou a obsahuje tipy pro práci s většími objemy nebo jinými typy souborů.

Jste připraveni na další krok? Zkuste změnit callback tak, aby výsledky ukládal do databáze, nebo přidejte předzpracování obrazu (např. deskew) před OCR. Vzor se dobře škáluje, takže jej můžete přizpůsobit libovolnému scénáři hromadného zpracování.

Šťastné programování a ať jsou vaše OCR pipeline rychlé a bez chyb!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}