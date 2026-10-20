---
category: general
date: 2026-02-14
description: Jak použít OCR v C# k rychlému získávání textu z PNG souborů. Naučte
  se hromadné OCR obrázků, zpracování více obrázků a použití Aspose OCR C# v jednom
  průvodci.
draft: false
keywords:
- how to use OCR
- extract text png
- batch OCR images
- process multiple images
- aspose OCR c#
language: cs
og_description: Jak používat OCR v C# s Aspose OCR C#. Tento tutoriál ukazuje, jak
  extrahovat text z PNG souborů, provádět hromadné OCR obrázků a efektivně zpracovávat
  více obrázků.
og_title: Jak používat OCR v C# – Hromadné získávání textu z PNG
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Jak používat OCR v C# – Dávkové zpracování PNG obrázků s Aspose OCR
url: /cs/net/text-recognition/how-to-use-ocr-in-c-batch-process-png-images-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak používat OCR v C# – Dávkové zpracování PNG obrázků pomocí Aspose OCR

Už jste se někdy zamýšleli **how to use OCR**, jak získat text z hromady PNG souborů, aniž byste museli psát samostatnou rutinu pro každý z nich? Nejste sami. Mnoho vývojářů narazí na problém, když potřebují **extract text PNG** aktiva ve velkém měřítku, zejména když jsou obrázky v adresáři a musíte spustit OCR engine pro každý soubor.  

V tomto průvodci projdeme kompletním, připraveným řešením, které **batch OCR images**, **process multiple images** paralelně a využívá výkonnou knihovnu **Aspose OCR C#**. Na konci budete mít jediný spustitelný soubor, který načte libovolný počet PNG, extrahuje jejich text a vypíše výsledky do konzole – vše jen s několika řádky kódu.

## Požadavky

- .NET 6.0 nebo novější (kód funguje také s .NET Core a .NET Framework)  
- Platná licence Aspose.OCR pro .NET (nebo bezplatná zkušební verze) – můžete ji získat na webu Aspose.  
- Složka obsahující PNG soubory, které chcete číst.  
- Visual Studio 2022 (nebo jakékoli C#‑kompatibilní IDE).  

Kromě balíčku `Aspose.OCR` nejsou vyžadovány žádné další NuGet balíčky.

## Krok 1: Jak používat OCR – Inicializace Aspose OCR Engine

Prvním, co potřebujete, je instance třídy `Engine`. Tento objekt abstrahuje podkladovou OCR technologii a může běžet na CPU nebo GPU, v závislosti na vašem hardwaru a licenci.

```csharp
using System;
using System.Collections.Generic;
using System.Collections.Concurrent;
using System.Threading.Tasks;
using Aspose.OCR;

// Create an OCR engine (CPU by default; GPU can be enabled via EngineSettings if licensed)
var ocrEngine = new Engine();
```

*Proč je to důležité:* Inicializace engine jednou a jeho opětovné používání napříč vlákny šetří paměť a zabraňuje režii opakovaného načítání OCR modelů. Také zajišťuje konzistentní nastavení pro všechny obrázky.

## Krok 2: Extract Text PNG – Shromáždění cest k obrázkům

Dále potřebujeme kolekci cest k souborům. V reálném projektu můžete adresář načítat dynamicky, ale pro přehlednost uvedeme několik ukázkových souborů.

```csharp
// List the PNG files you want to process
var imagePaths = new List<string>
{
    "YOUR_DIRECTORY/img1.png",
    "YOUR_DIRECTORY/img2.png",
    "YOUR_DIRECTORY/img3.png"
};
```

*Tip:* Nahraďte `YOUR_DIRECTORY` absolutní nebo relativní cestou k vašim obrázkům. Pokud máte desítky souborů, můžete ruční seznam nahradit `Directory.GetFiles("YOUR_DIRECTORY", "*.png")`.

## Krok 3: Batch OCR Images – Spuštění rozpoznávání paralelně

Zpracování obrázků jedno po druhém je jednoduché, ale pomalé. Použitím `Parallel.ForEach` můžeme **process multiple images** současně a využít výhod multi‑core CPU.

```csharp
// Helper method that performs the parallel recognition
static IReadOnlyList<OcrResult> RecognizeImagesInParallel(Engine engine, IEnumerable<string> paths)
{
    var resultsBag = new ConcurrentBag<OcrResult>();

    Parallel.ForEach(paths, path =>
    {
        // Load the image stream (Aspose handles various formats)
        var image = ImageStream.FromFile(path);
        // Perform OCR
        OcrResult result = engine.Recognize(image);
        // Store the result safely for later use
        resultsBag.Add(result);
    });

    return resultsBag.ToArray();
}

// Execute the parallel OCR
var ocrResults = RecognizeImagesInParallel(ocrEngine, imagePaths);
```

*Proč paralelně?* Každé volání OCR je náročné na CPU, ale nezávislé, takže jejich souběžné spuštění může dramaticky zkrátit celkový čas běhu, zejména na 4‑jádrovém nebo výkonnějším stroji.

## Krok 4: Process Multiple Images – Zobrazení extrahovaného textu

Nyní, když máme kolekci objektů `OcrResult`, můžeme je iterovat a vytisknout rozpoznaný text. Zde byste normálně uložili výstup do databáze nebo zapisovali do souborů, ale výstup do konzole udržuje příklad stručný.

```csharp
int index = 1;
foreach (var result in ocrResults)
{
    Console.WriteLine($"--- Image {index++} ---");
    Console.WriteLine(result.Text);
}
```

**Očekávaný výstup v konzoli (ukázka):**

```
--- Image 1 ---
Hello world! This is the first image.
--- Image 2 ---
Invoice #12345
Total: $250.00
--- Image 3 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
```

Pokud se některý obrázek nepodaří načíst, Aspose vyhodí výjimku; můžete volání `engine.Recognize` zabalit do try/catch bloku a zaznamenat chyby, aniž byste přerušili celý batch.

## Krok 5: Kompletní funkční příklad – Vše dohromady

Níže je kompletní program, který můžete zkopírovat a vložit do nového C# konzolového projektu. Obsahuje vše od `using` direktiv až po finální výstupní smyčku.

```csharp
using System;
using System.Collections.Generic;
using System.Collections.Concurrent;
using System.Threading.Tasks;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // Step 1: Initialize the OCR engine
        var ocrEngine = new Engine();

        // Step 2: Define the PNG files to process
        var imagePaths = new List<string>
        {
            "YOUR_DIRECTORY/img1.png",
            "YOUR_DIRECTORY/img2.png",
            "YOUR_DIRECTORY/img3.png"
        };

        // Step 3: Run OCR in parallel
        var ocrResults = RecognizeImagesInParallel(ocrEngine, imagePaths);

        // Step 4: Output the recognized text
        int index = 1;
        foreach (var result in ocrResults)
        {
            Console.WriteLine($"--- Image {index++} ---");
            Console.WriteLine(result.Text);
        }
    }

    // Helper method for parallel OCR
    static IReadOnlyList<OcrResult> RecognizeImagesInParallel(Engine engine, IEnumerable<string> paths)
    {
        var resultsBag = new ConcurrentBag<OcrResult>();

        Parallel.ForEach(paths, path =>
        {
            try
            {
                var image = ImageStream.FromFile(path);
                OcrResult result = engine.Recognize(image);
                resultsBag.Add(result);
            }
            catch (Exception ex)
            {
                // Log the error but keep the batch running
                Console.Error.WriteLine($"Error processing {path}: {ex.Message}");
            }
        });

        return resultsBag.ToArray();
    }
}
```

### Spuštění ukázky

1. Vytvořte nový projekt **Console App** ve Visual Studiu.  
2. Přidejte NuGet balíček **Aspose.OCR** (`Install-Package Aspose.OCR`).  
3. Nahraďte `YOUR_DIRECTORY` cestou, která obsahuje vaše PNG soubory.  
4. Sestavte a spusťte – měli byste vidět extrahovaný text vytištěný v konzoli.

## Pro tipy a okrajové případy

- **GPU akcelerace:** Pokud máte kompatibilní GPU a licencovaný Aspose OCR, povolte ji pomocí `EngineSettings` před vytvořením engine. To může ušetřit sekundy u každého obrázku.  
- **Velké soubory:** Pro obrázky větší než 10 MB zvažte jejich předchozí zmenšení, aby se snížil tlak na paměť.  
- **Podpora jazyků:** Ve výchozím nastavení engine předpokládá angličtinu. Nastavte `engine.Language = Language.French;` (nebo jakýkoli podporovaný jazyk) pro zlepšení přesnosti u textu v jiném jazyce.  
- **Zpracování chyb:** `try/catch` uvnitř paralelní smyčky zajišťuje, že poškozený soubor nepřeruší celý batch. Můžete také zaznamenávat selhání do souboru pro pozdější revizi.  
- **Ukládání výsledků:** Místo výpisu můžete zapsat `result.Text` do souboru `.txt` pomocí `File.WriteAllText(Path.ChangeExtension(path, ".txt"))`.

## Závěr

Nyní víte **how to use OCR** v C# k **extract text PNG** souborům, **batch OCR images**, a **process multiple images** efektivně s Aspose OCR C#. Řešení je zcela samostatné, běží paralelně a může být rozšířeno tak, aby zpracovávalo stovky nebo tisíce souborů s minimálními změnami.

Jste připraveni na další krok? Zkuste nahradit výstup do konzole CSV reportem, experimentovat s GPU akcelerací nebo předat OCR text do vyhledávacího indexu. Možnosti jsou neomezené a základní vzor – inicializovat jednou, spustit paralelně, elegantně zpracovávat chyby – vám dobře poslouží v jakémkoli pipeline pro zpracování obrázků.

Šťastné programování a ať jsou vaše OCR úlohy rychlé a bez chyb!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}