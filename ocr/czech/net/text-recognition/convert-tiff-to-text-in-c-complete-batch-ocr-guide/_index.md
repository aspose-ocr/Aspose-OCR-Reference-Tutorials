---
category: general
date: 2026-05-25
description: Převod TIFF na text pomocí Aspose.OCR v C#. Naučte se hromadný převod
  obrázků na text a efektivně extrahujte text z TIFF souborů.
draft: false
keywords:
- convert tiff to text
- extract text from tiff
- batch image to text conversion
- convert scanned images txt
language: cs
og_description: Převod TIFF na text pomocí Aspose.OCR. Tento průvodce ukazuje hromadný
  převod obrázků na text a jak extrahovat text z TIFF souborů pomocí několika řádků
  kódu v C#.
og_title: Převod TIFF na text v C# – Kompletní průvodce dávkovým OCR
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: Convert TIFF to text using Aspose.OCR in C#. Learn batch image to text
    conversion and extract text from TIFF files efficiently.
  headline: Convert TIFF to Text in C# – Complete Batch OCR Guide
  type: TechArticle
- description: Convert TIFF to text using Aspose.OCR in C#. Learn batch image to text
    conversion and extract text from TIFF files efficiently.
  name: Convert TIFF to Text in C# – Complete Batch OCR Guide
  steps:
  - name: '**Create** an OCR engine set for English.'
    text: '**Create** an OCR engine set for English.'
  - name: '**Collect** every TIFF file from the target folder.'
    text: '**Collect** every TIFF file from the target folder.'
  - name: '**Run** `BatchOcr.RecognizeAll` with four threads, turning each image into
      a string.'
    text: '**Run** `BatchOcr.RecognizeAll` with four threads, turning each image into
      a string.'
  - name: '**Loop** over the results, swapping the `.tif` extension for `.txt` and
      writing the string to disk.'
    text: '**Loop** over the results, swapping the `.tif` extension for `.txt` and
      writing the string to disk.'
  type: HowTo
tags:
- C#
- OCR
- Aspose
- TIFF
title: Převod TIFF na text v C# – Kompletní průvodce hromadným OCR
url: /cs/net/text-recognition/convert-tiff-to-text-in-c-complete-batch-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Převod TIFF na text v C# – Kompletní průvodce hromadným OCR

Už jste někdy potřebovali **převést TIFF na text**, ale nebyli jste si jisti, kde začít? Nejste v tom sami — mnoho vývojářů narazí na hromadné OCR při práci s naskenovanými dokumenty. V tomto tutoriálu vás provedeme praktickým řešením, které **extrahuje text z TIFF** souborů pomocí Aspose.OCR, a uděláme to paralelně, takže velké složky skončí během několika sekund.

Také se dotkneme nejlepších postupů pro **hromadný převod obrázku na text**, takže na konci budete mít znovupoužitelný úryvek, který převádí celý adresář naskenovaných obrázků na úhledné soubory *.txt* — ideální pro indexaci, vyhledávání nebo předávání do následných analytických procesů.

## Co budete potřebovat

- **.NET 6.0** nebo novější (kód se také kompiluje na .NET Framework)  
- NuGet balíček **Aspose.OCR for .NET** (`Install-Package Aspose.OCR`)  
- Složka obsahující jeden nebo více souborů *.tif* (klasický formát skenování TIFF)  
- Vaše oblíbené IDE (Visual Studio, VS Code, Rider — cokoli preferujete)

A to je vše. Žádné externí služby, žádné API klíče, jen čistý C# a Aspose.

![Snímek obrazovky TIFF souboru, který se zpracovává, a výsledného textového souboru](/images/ocr-result.png "Výsledek OCR zobrazující převod TIFF na text")

*(Alt text: Snímek obrazovky ukazující převod TIFF na text na obrazovce)*

## Krok 1: Nastavení OCR enginu — Převod TIFF na text

Nejprve potřebujeme instanci `OcrEngine`, která ví, že má číst anglické znaky. Engine je srdcem převodu; jeho správné nastavení zajišťuje spolehlivé výsledky.

```csharp
using Aspose.OCR;
using System.IO;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // Create an OCR engine configured for English – this is the core of convert TIFF to text
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.English
        };
```

*Proč je to důležité:*  
Aspose.OCR podporuje desítky jazyků. Pokud pracujete s vícejazyčnými skeny, stačí změnit `OcrLanguage.English` na odpovídající hodnotu výčtu. Pokud jazyk nedefinujete, engine přejde do režimu automatické detekce, což může být pomalejší a méně přesné.

## Krok 2: Shromáždění všech TIFF souborů — Efektivní extrakce textu z TIFF

Dále načteme každý soubor *.tif* ze zadané složky. Použití `Directory.GetFiles` nám poskytne čisté pole, které můžeme předat hromadnému procesoru.

```csharp
        // Locate every TIFF in the input folder – adjust the path to your own directory
        string inputFolder = @"C:\Scans\Batch";
        string[] tiffFiles = Directory.GetFiles(inputFolder, "*.tif", SearchOption.TopDirectoryOnly);

        if (tiffFiles.Length == 0)
        {
            System.Console.WriteLine("No TIFF files found. Check the folder path.");
            return;
        }
```

*Tip:* Příznak `SearchOption.AllDirectories` lze použít, pokud jsou vaše skeny vnořeny ve podsložkách. Jen si uvědomte, že hlubší rekurze může během hromadného kroku zvýšit spotřebu paměti.

## Krok 3: Paralelní OCR — Hromadný převod obrázku na text

Nyní zábavná část. Aspose.OCR obsahuje statického pomocníka `BatchOcr.RecognizeAll`, který přijímá pole cest k souborům, engine a parametr `parallelism`. Spustíme čtyři vlákna, což na moderním čtyřjádrovém notebooku poskytuje téměř lineární zrychlení.

```csharp
        // Run OCR on all files in parallel (4 threads by default)
        // The result is a dictionary where Key = file path, Value = extracted text
        Dictionary<string, string> ocrResults = BatchOcr.RecognizeAll(tiffFiles, ocrEngine, parallelism: 4);
```

*Proč paralelismus?*  
Skenování hromady vysokého rozlišení TIFF může být náročné na CPU. Rozdělením práce mezi více vláken udržíme všechna jádra vytížená, což dramaticky zkrátí celkový čas běhu. Pokud to spustíte na serveru s více jádry, zvyšte hodnotu `parallelism` odpovídajícím způsobem.

## Krok 4: Zápis výstupu — Převod naskenovaných obrázků na TXT soubory

Nakonec projdeme slovník a zapíšeme každý kus textu do souboru *.txt*, který má stejný základní název jako původní soubor. To je okamžik, kdy **convert scanned images txt** se stává realitou.

```csharp
        // Save each recognized text to a .txt file with the same base name as the source TIFF
        foreach (var kvp in ocrResults)
        {
            string sourcePath = kvp.Key;
            string extractedText = kvp.Value;

            // Change extension from .tif to .txt
            string txtPath = Path.ChangeExtension(sourcePath, ".txt");

            // Write the text – UTF‑8 ensures all characters are preserved
            File.WriteAllText(txtPath, extractedText);
            System.Console.WriteLine($"Saved: {txtPath}");
        }

        System.Console.WriteLine("Batch conversion complete!");
    }
}
```

### Co kód dělá, v prostém jazyce

1. **Vytvořte** OCR engine nastavený na angličtinu.  
2. **Shromážděte** každý TIFF soubor z cílové složky.  
3. **Spusťte** `BatchOcr.RecognizeAll` se čtyřmi vlákny, které každému obrázku převádějí na řetězec.  
4. **Projděte** výsledky, zaměňte příponu `.tif` za `.txt` a zapište řetězec na disk.

To je celý workflow **convert TIFF to text** v méně než 50 řádcích kódu.

## Řešení okrajových případů — Když věci neprobíhají hladce

- **Chybějící nebo poškozené TIFF** — `BatchOcr` vyhodí `OcrException`. Zabalte volání do `try / catch`, pokud potřebujete elegantní degradaci.  
- **Dokumenty v jiném jazyce než angličtině** — změňte `OcrLanguage.English` na `OcrLanguage.Spanish`, `OcrLanguage.French` atd., nebo použijte `OcrLanguage.AutoDetect`.  
- **Velmi velké obrázky** — zvažte snížení DPI před OCR (`ocrEngine.ImagePreprocessing.Dpi = 200`) pro úsporu paměti, i když můžete ztratit část přesnosti.  
- **Kódování výstupu** — pokud potřebujete konkrétní kódovou stránku (např. Windows‑1252), předávejte ji do `File.WriteAllText(txtPath, extractedText, Encoding.GetEncoding(1252))`.

## Profesionální tipy pro robustní hromadné převody

- **Logujte selhání**: vytvořte `List<string> failedFiles` a přidejte do něj každý soubor, který vyhodí výjimku; po smyčce zapište seznam do logu.  
- **Znovu použijte engine**: stejná instance `OcrEngine` může být použita napříč mnoha soubory; nevytvářejte ji uvnitř smyčky.  
- **Validujte výsledek**: rychlá kontrola `if (string.IsNullOrWhiteSpace(extractedText))` může označit skeny, které jsou prázdné nebo nečitelné.  
- **Kombinujte s PDF**: pokud je vaším zdrojem vícestránkový PDF, nejprve převěďte každou stránku na TIFF (Aspose.PDF to umí) a pak spusťte tento batch.

## Další kroky — Přesahování jednoduchého převodu

Nyní, když můžete **extrahovat text z TIFF** souborů hromadně, můžete chtít:

- Zavést soubory *.txt* do vyhledávacího indexu (Elasticsearch, Azure Cognitive Search).  
- Spustit detekci jazyka na každém výsledku pro směrování dokumentů do lokálně specifických pipeline.  
- Vytvořit prohledávatelné PDF překrytím OCR textu zpět na původní obrázky (znovu Aspose.PDF).

Všechny tyto scénáře staví na stejném základním principu: **batch image to text conversion** je stavební kámen pro větší systémy zpracování dokumentů.

---

### Závěr

Právě jste se naučili, jak **převést TIFF na text** pomocí Aspose.OCR, zpracovat celou složku paralelně a uložit každý výsledek jako čistý soubor *.txt*. Řešení je lehké, plně konfigurovatelné a připravené do produkce — ať už digitalizujete staré faktury, archivujete naskenované smlouvy nebo napájíte vyhledávač textu.

Vyzkoušejte to, upravte paralelismus a začněte zavádět nově vytvořené textové soubory do libovolného pracovního postupu, který potřebujete. Šťastné OCRování!

---

## Související tutoriály

- [Extrahovat text z obrázků pomocí OCR operace ve složkách](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Extrahovat text z obrázku — optimalizace OCR s Aspose.OCR pro .NET](/ocr/english/net/ocr-optimization/)
- [Extrahovat text z obrázku v C# s výběrem jazyka pomocí Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}