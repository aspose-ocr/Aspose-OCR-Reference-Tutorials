---
category: general
date: 2026-03-28
description: Naučte se provádět hromadné OCR v C# a snadno převádět TIFF na text.
  Tento krok‑za‑krokem průvodce ukazuje, jak extrahovat text z TIFF souborů pomocí
  Aspose OCR.
draft: false
keywords:
- how to batch ocr
- convert tiff to text
- extract text from tiff
- c# ocr tutorial
language: cs
og_description: Jak provádět dávkové OCR v C#? Postupujte podle tohoto kompletního
  tutoriálu a převádějte více‑stránkové TIFF soubory na prohledávatelný text pomocí
  Aspose OCR.
og_title: Jak provádět dávkové OCR v C# – převést vícestránkový TIFF na text
tags:
- OCR
- C#
- Aspose
title: Jak provádět dávkové OCR v C# – převést vícestránkový TIFF na text
url: /cs/net/text-recognition/how-to-batch-ocr-in-c-convert-multi-page-tiff-to-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak provést hromadné OCR v C# – Převod vícestránkového TIFF na text

Už jste se někdy zamysleli nad **tím, jak provést hromadné OCR** zásobník naskenovaných stránek, aniž byste museli psát smyčku pro každý obrázek? Nejste v tom sami. V mnoha projektech—například při zpracování faktur nebo digitalizaci archivů—se denně objevuje potřeba **převést TIFF na text**, a provádět to stránku po stránce se rychle stane noční můrou.

Dobrá zpráva? S několika řádky C# a Aspose OCR můžete načíst celý vícestránkový TIFF do enginu a získat slovník čísel stránek přiřazených k jejich extrahovaným řetězcům. V tomto tutoriálu projdeme kompletním, spustitelným příkladem, který přesně ukazuje **jak provést hromadné OCR**, jak **extrahovat text z TIFF**, a proč tento přístup překonává manuální alternativu.

## Co se naučíte

- Nastavit knihovnu Aspose OCR v .NET projektu.  
- Načíst vícestránkový TIFF soubor pomocí `Image.FromMultiPageFile`.  
- Spustit `RecognizeBatch` a získat `Dictionary<int,string>` s výsledky po stránkách.  
- Vytisknout výstup v čistém, čitelném formátu.  

Na konci budete mít připravenou spustitelnou konzolovou aplikaci, která převádí jakýkoli vícestránkový TIFF na prostý text—bez potřeby dalších nástrojů.

### Požadavky

- .NET 6.0 SDK (nebo jakákoli recentní verze .NET).  
- Visual Studio 2022 nebo VS Code—stačí vám oblíbené IDE.  
- Platná licence Aspose OCR nebo bezplatný evaluační klíč (API funguje i bez licence, ale přidá vodoznak).  
- Ukázkový vícestránkový TIFF pojmenovaný `multipage.tif` umístěný ve složce, na kterou můžete odkazovat.

> **Tip:** Pokud používáte Windows, výchozí složka projektu je pohodlné místo pro umístění TIFF; na Linux/macOS stačí upravit cestu podle potřeby.

## Krok 1: Nainstalujte NuGet balíček Aspose OCR

Než napíšeme jakýkoli kód, potřebujeme OCR knihovnu. Otevřete terminál ve složce projektu a spusťte:

```bash
dotnet add package Aspose.OCR
```

Tím se stáhne nejnovější stabilní verze (k březnu 2026 v23.9) a přidají se potřebné DLL soubory do vašeho projektu. Pro jednoduchou konzolovou aplikaci není potřeba žádná další konfigurace.

## Krok 2: Vytvořte kostru konzolové aplikace

Vytvořme minimální program, který odkazuje na OCR engine. Direktivy `using` jsou klíčové—bez nich se kompilátor bude stěžovat na chybějící typy.

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;   // Required for Image class
```

> **Proč je to důležité:** Třída `Image` se nachází v pod‑namespace, a zapomenutí importu `ImageProcessing` vám způsobí chybu „type or namespace not found“, která může ztratit hodinu ladění.

Nyní přidejte metodu `Main` a stručný komentář popisující účel:

```csharp
/// <summary>
/// Demonstrates how to batch OCR a multi‑page TIFF and output each page's text.
/// </summary>
class BatchOcrTutorial
{
    static void Main()
    {
        // Implementation will go here
    }
}
```

## Krok 3: Inicializujte OCR engine

`OcrEngine` je hlavní komponenta. Vytvořit jej jednou a znovu použít pro všechny stránky je jak úsporné na paměť, tak rychlé.

```csharp
// Step 3: Create an OCR engine instance
var ocrEngine = new OcrEngine();
```

> **Co se děje pod kapotou?** Engine načítá jazykové modely a předkonfiguruje výchozí nastavení (např. angličtina, automatické otáčení). Tyto můžete později upravit, ale výchozí hodnoty jsou vhodné pro většinu dokumentů.

## Krok 4: Načtěte vícestránkový TIFF

Aspose usnadňuje načítání více‑rámcových obrázků. Zadejte úplnou cestu nebo relativní cestu vzhledem k pracovnímu adresáři spustitelného souboru.

```csharp
// Step 4: Load a multi‑page TIFF image
string tiffPath = "YOUR_DIRECTORY/multipage.tif";   // ← replace with your actual path
var multiPageImage = Image.FromMultiPageFile(tiffPath);
```

Pokud soubor není nalezen, `FromMultiPageFile` vyhodí `FileNotFoundException`. Zabalte to do `try/catch`, pokud potřebujete elegantní zpracování chyb—něco, co ukážeme v dalším kroku.

## Krok 5: Proveďte hromadné OCR

Nyní přichází hvězda představení: `RecognizeBatch`. Vrací `Dictionary<int,string>`, kde klíč je index stránky (začíná na 0) a hodnota je rozpoznaný text.

```csharp
// Step 5: Perform batch OCR on all pages
Dictionary<int, string> ocrResults = ocrEngine.RecognizeBatch(multiPageImage);
```

> **Hraniční případ:** Některé TIFFy obsahují prázdné stránky. Aspose vrátí prázdný řetězec pro tyto stránky, který můžete později odfiltrovat, pokud nechcete nepořádek ve výstupu.

## Krok 6: Zobrazte výsledky

Nakonec projděte slovník a vytiskněte text každé stránky. Použití interpolovaných řetězců udržuje kód přehledný.

```csharp
// Step 6: Output the recognized text for each page
foreach (var pageResult in ocrResults)
{
    Console.WriteLine($"--- Page {pageResult.Key + 1} ---"); // +1 for human‑friendly numbering
    Console.WriteLine(pageResult.Value);
    Console.WriteLine(); // Blank line for readability
}
```

Spuštěním programu by se mělo zobrazit něco jako:

```
--- Page 1 ---
Invoice #12345
Date: 2024‑12‑01
Total: $1,250.00
...

--- Page 2 ---
Terms and Conditions
...
```

Pokud vidíte poškozený výstup, dvakrát zkontrolujte, že zdrojový TIFF není poškozený a že jazyk textu odpovídá výchozímu nastavení engine (angličtina). Pro neanglické dokumenty můžete také nastavit `ocrEngine.Language = OcrLanguage.Spanish;`.

## Kompletní funkční příklad

Spojením všech částí dohromady, zde je kompletní program, který můžete zkopírovat do `Program.cs` a spustit:

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;   // Needed for Image class

/// <summary>
/// Demonstrates how to batch OCR a multi‑page TIFF and output each page's text.
/// </summary>
class BatchOcrTutorial
{
    static void Main()
    {
        try
        {
            // Step 1: Create an OCR engine instance
            var ocrEngine = new OcrEngine();

            // Step 2: Load a multi‑page TIFF image
            string tiffPath = "YOUR_DIRECTORY/multipage.tif";   // Change to your actual file location
            var multiPageImage = Image.FromMultiPageFile(tiffPath);

            // Step 3: Perform batch OCR on all pages
            Dictionary<int, string> ocrResults = ocrEngine.RecognizeBatch(multiPageImage);

            // Step 4: Output the recognized text for each page
            foreach (var pageResult in ocrResults)
            {
                Console.WriteLine($"--- Page {pageResult.Key + 1} ---");
                Console.WriteLine(pageResult.Value);
                Console.WriteLine(); // Extra line for visual separation
            }
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error during OCR processing: {ex.Message}");
        }
    }
}
```

Uložte, sestavte a spusťte:

```bash
dotnet run
```

Měli byste vidět extrahovaný obsah každé stránky vytištěný do konzole. To je celý **c# ocr tutorial**, o který jste požádali.

## Často kladené otázky a hraniční případy

### Co když můj TIFF obsahuje desítky stránek?

`RecognizeBatch` zpracuje všechny snímky v jednom volání, ale využití paměti roste lineárně s počtem stránek. Pro velmi velké dokumenty (stovky stránek) zvažte zpracování po částech:

```csharp
for (int i = 0; i < multiPageImage.PageCount; i += 50)
{
    var subImage = multiPageImage.GetPages(i, Math.Min(50, multiPageImage.PageCount - i));
    var partialResults = ocrEngine.RecognizeBatch(subImage);
    // Merge partialResults into the main dictionary...
}
```

### Mohu uložit extrahovaný text do souborů místo tisknutí?

Určitě. Nahraďte blok `Console.WriteLine` operacemi se soubory:

```csharp
string outputFolder = "ExtractedText";
Directory.CreateDirectory(outputFolder);

foreach (var pageResult in ocrResults)
{
    string filePath = Path.Combine(outputFolder, $"Page_{pageResult.Key + 1}.txt");
    File.WriteAllText(filePath, pageResult.Value);
}
```

Nyní každá stránka získá svůj vlastní soubor `.txt`—ideální pro následné indexování.

### Jak změním výstupní jazyk nebo povolím automatické otáčení?

```csharp
ocrEngine.Language = OcrLanguage.French; // or any supported language
ocrEngine.AutoRotate = true;             // Detects rotated text automatically
```

Tato nastavení musí být aplikována **před** voláním `RecognizeBatch`.

## Závěr

Probrali jsme **jak provést hromadné OCR** vícestránkového TIFF pomocí Aspose OCR v C#. Načtením obrázku jednou, voláním `RecognizeBatch` a iterací přes výsledný slovník můžete **převést TIFF na text** během několika sekund. Příklad také ukazuje, jak **extrahovat text z TIFF**, zpracovávat chyby a volitelně zapisovat výsledky do souborů—vše v čisté, samostatné konzolové aplikaci.

Jste připraveni na další krok? Zkuste zkombinovat tento přístup s knihovnou pro generování PDF a vytvořit prohledávatelná PDF, nebo napojte výstup do databáze pro prohledávatelné archivy. Můžete také experimentovat s jinými formáty obrázků (PNG, JPEG) výměnou `Image.FromMultiPageFile` za `Image.FromFile`.

Máte další otázky ohledně OCR, licencování nebo ladění výkonu? Zanechte komentář níže a šťastné programování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}