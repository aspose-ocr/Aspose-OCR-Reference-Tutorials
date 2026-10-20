---
category: general
date: 2026-01-09
description: Extrahujte text z TIFF souborů pomocí Aspose OCR v C#. Naučte se, jak
  získat prvních 50 znaků každého výsledku v tomto krok‑za‑krokem tutoriálu.
draft: false
keywords:
- extract text from tiff
- get first 50 characters
- aspose ocr c# tutorial
language: cs
og_description: Extrahujte text z TIFF pomocí Aspose OCR v C#. Tento průvodce ukazuje,
  jak krok za krokem získat prvních 50 znaků každého výsledku OCR.
og_title: Extrahujte text z TIFF pomocí Aspose OCR – Kompletní průvodce C#
tags:
- Aspose OCR
- C#
- TIFF processing
title: Extrahování textu z TIFF pomocí Aspose OCR C# – Kompletní tutoriál
url: /cs/net/text-recognition/extract-text-from-tiff-with-aspose-ocr-c-full-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahovat text z TIFF – Kompletní tutoriál Aspose OCR C# 

Už jste někdy potřebovali **extrahovat text z TIFF** obrázků, ale nebyli jste si jisti, kterou knihovnu použít? Nejste v tom sami. Mnoho vývojářů narazí na problém, když se snaží získat prohledávatelný text z více‑stránkových TIFF souborů, zejména když záleží na výkonu.

V tomto **aspose ocr c# tutorial** projdeme připravený příklad, který nejen extrahuje celý text, ale také vám ukáže, jak **získat prvních 50 znaků** každé stránky pro rychlé náhledy. Na konci budete mít samostatný program, který můžete vložit do libovolného .NET projektu.

## Co budete potřebovat

- .NET 6 (nebo jakákoli recentní verze .NET) – kód se kompiluje jak s .NET Core, tak s .NET Framework.  
- Aktivní licence Aspose.OCR pro .NET (můžete začít s bezplatnou zkušební verzí).  
- Složka, která obsahuje jeden nebo více souborů `.tif`, které chcete zpracovat.  
- Visual Studio, VS Code nebo jakékoli IDE, které preferujete – příklad je čistý C#, takže volba editoru není podstatná.  

> **Tip:** Pokud běžíte na CI serveru, přidejte NuGet balíček Aspose.OCR (`Aspose.OCR`) do souboru projektu; knihovna je plně spravovaná a nemá žádné nativní závislosti.

## Krok 1: Nainstalujte NuGet balíček Aspose OCR

Nejprve přiveďme OCR engine do projektu. Otevřete terminál ve složce řešení a spusťte:

```bash
dotnet add package Aspose.OCR
```

Tento příkaz stáhne nejnovější stabilní verzi (k lednu 2026 je to 23.9) a automaticky aktualizuje váš `.csproj`. Není potřeba ručně manipulovat s DLL soubory.

## Krok 2: Inicializujte OCR Engine

Nyní vytvoříme instanci `OcrEngine`. Představte si ji jako „mozek“, který přečte každou stránku TIFF.

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;
using System.IO;

namespace TiffOcrDemo
{
    class Program
    {
        static void Main()
        {
            // Step 2: Initialize the OCR engine
            var ocrEngine = new OcrEngine();

            // Optional: tweak recognition settings if you know the language
            // ocrEngine.Language = Language.English;
            // ocrEngine.Dpi = 300; // higher DPI can improve accuracy
```

Proč vytváříme engine jen jednou? Protože `RecognizeImages` může přijmout kolekci cest k souborům, což umožňuje engine znovu použít interní buffery a výrazně zrychlit dávkové zpracování.

## Krok 3: Získejte všechny TIFF soubory najednou

Místo toho, abyste sami procházeli adresář, necháme .NET udělat těžkou práci. Metoda `Directory.GetFiles` vrací `IEnumerable<string>`, který můžeme přímo předat volání OCR.

```csharp
            // Step 3: Collect all TIFF images from the batch folder
            IEnumerable<string> imageFiles = Directory.GetFiles(@"YOUR_DIRECTORY/Batch", "*.tif");

            if (!imageFiles.Any())
            {
                Console.WriteLine("No TIFF files found in the specified folder.");
                return;
            }
```

> **Co když jsou mé obrázky JPEG nebo PNG?** Stačí změnit vyhledávací vzor (`"*.jpg"` nebo `"*.*"`). Aspose OCR funguje se všemi běžnými rastrovými formáty.

## Krok 4: Spusťte OCR na celé kolekci

Zde je kouzelný řádek, který zpracuje každý soubor v jednom požadavku. Metoda vrací slovník, kde klíč je cesta k souboru a hodnota je objekt `OcrResult` obsahující rozpoznaný text.

```csharp
            // Step 4: Perform OCR on the entire collection in one call
            var ocrResults = ocrEngine.RecognizeImages(imageFiles);
```

Proč dávkové zpracování? Snižuje režii opakovaného načítání OCR engine a na vícejádrových strojích Aspose interně paralelizuje práci, což vám poskytne znatelný nárůst rychlosti.

## Krok 5: Zobrazte náhled – Získejte prvních 50 znaků

Většina UI scénářů potřebuje jen úryvek, ne celý dokument. Extrahujeme prvních 50 znaků (nebo méně, pokud je stránka krátká) a vytiskneme je spolu s názvem souboru.

```csharp
            // Step 5: Display each file name with a preview of the recognized text
            foreach (var entry in ocrResults) // entry.Key = file path, entry.Value = OcrResult
            {
                string fileName = Path.GetFileName(entry.Key);
                string fullText = entry.Value.Text ?? string.Empty;
                string preview = fullText.Substring(0, Math.Min(50, fullText.Length));

                Console.WriteLine($"{fileName} → {preview}...");
            }
        }
    }
}
```

Řádek `Math.Min(50, fullText.Length)` zajišťuje, že nepřekročíme hranice řetězce – malá ochrana, která zabraňuje `ArgumentOutOfRangeException`, když je výsledek OCR kratší než 50 znaků.

### Očekávaný výstup v konzoli

Předpokládejme, že máte dva TIFF soubory (`invoice1.tif` a `receipt2.tif`), konzole může zobrazit:

```
invoice1.tif → Invoice Number: 2025-07-14 Date: 07/14/...
receipt2.tif → Store: QuickMart Total: $23.45 Date: ...
```

Každý řádek končí třemi tečkami (`...`), aby naznačil, že náhled je jen začátek delšího textového bloku.

## Krok 6: Ošetřete okrajové případy a běžné úskalí

### Prázdné nebo poškozené soubory

Pokud soubor nelze přečíst, `RecognizeImages` stále vrátí položku s prázdnou vlastností `Text`. Můžete je odfiltrovat:

```csharp
if (string.IsNullOrWhiteSpace(fullText))
{
    Console.WriteLine($"{fileName} → (No recognizable text)");
    continue;
}
```

### Velké dávky

Zpracování tisíců TIFF souborů může spotřebovat hodně paměti. V takových případech použijte přetížení, které přijímá `Stream` pro každý obrázek, nebo zpracovávejte seznam v menších částech:

```csharp
var batches = imageFiles.Chunk(100); // .NET 6+ extension
foreach (var batch in batches)
{
    var batchResults = ocrEngine.RecognizeImages(batch);
    // handle batchResults...
}
```

### Podpora jazyků a fontů

Pokud vaše dokumenty obsahují ne‑latinské znaky, nastavte jazyk před voláním `RecognizeImages`:

```csharp
ocrEngine.Language = Language.Spanish; // or Language.MultiLanguage
```

Tato malá úprava může výrazně zvýšit přesnost.

## Krok 7: Kompletní funkční příklad (připravený ke kopírování a vložení)

Níže je kompletní program, který můžete vložit do nového konzolového projektu (`dotnet new console`) a spustit tak, jak je (jen nahraďte `YOUR_DIRECTORY/Batch` skutečnou cestou).

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;

namespace TiffOcrDemo
{
    class Program
    {
        static void Main()
        {
            // Initialize the OCR engine
            var ocrEngine = new OcrEngine();

            // Optional: set language or DPI for better accuracy
            // ocrEngine.Language = Language.English;
            // ocrEngine.Dpi = 300;

            // Collect all TIFF files from the batch folder
            IEnumerable<string> imageFiles = Directory.GetFiles(@"YOUR_DIRECTORY/Batch", "*.tif");

            if (!imageFiles.Any())
            {
                Console.WriteLine("No TIFF files found in the specified folder.");
                return;
            }

            // Perform OCR on the entire collection
            var ocrResults = ocrEngine.RecognizeImages(imageFiles);

            // Show a preview – get first 50 characters of each result
            foreach (var entry in ocrResults)
            {
                string fileName = Path.GetFileName(entry.Key);
                string fullText = entry.Value.Text ?? string.Empty;

                if (string.IsNullOrWhiteSpace(fullText))
                {
                    Console.WriteLine($"{fileName} → (No recognizable text)");
                    continue;
                }

                string preview = fullText.Substring(0, Math.Min(50, fullText.Length));
                Console.WriteLine($"{fileName} → {preview}...");
            }
        }
    }
}
```

Spusťte program pomocí `dotnet run`. Měli byste vidět stručný náhled pro každý TIFF soubor, což potvrzuje, že jste úspěšně **extrahovali text z TIFF** obrázků pomocí Aspose OCR.

## Často kladené otázky (FAQ)

**Q: Funguje to s více‑stránkovými TIFFy?**  
A: Ano. Aspose OCR interně zachází s každou stránkou jako s odděleným obrázkem, takže více‑stránkový TIFF poskytuje jeden spojený řetězec na soubor. V případě potřeby jej můžete později rozdělit.

**Q: Jaká je přesnost OCR hned po instalaci?**  
A: U čistých, vysoce rozlišených skenů (300 DPI nebo vyšší) můžete očekávat >95 % přesnost u anglického textu. Předzpracování (odklon, binarizace) může přesnost ještě zvýšit.

**Q: Můžu výstup uložit do CSV souboru?**  
A: Rozhodně. Nahraďte `Console.WriteLine` pomocí `StreamWriter` a zapisujte řádky `fileName,preview`. Nezapomeňte v textu náhledu escapovat čárky.

## Další kroky a související témata

- **Uložit výsledky OCR** – Uložte celý text do databáze pro prohledávatelné archivy.  
- **Kombinovat s konverzí PDF** – Použijte Aspose.PDF k vložení extrahovaného textu zpět do prohledávatelných PDF.  
- **Dávkové zpracování na Azure Functions** – Šiřte OCR práci bez správy serverů.  

Všechny tyto rozšíření se vážou k hlavní myšlence **extrahovat text z TIFF** efektivně, přičemž vám stále umožňují **získat prvních 50 znaků** pro rychlé UI náhledy.

---

*Šťastné programování! Pokud narazíte na nějaké problémy, zanechte komentář níže – udělám vše pro to, abych vám pomohl doladit OCR pipeline.* 

![Extract text from TIFF using Aspose OCR](https://example.com/images/extract-text-from-tiff.png "Extract text from TIFF using Aspose OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}