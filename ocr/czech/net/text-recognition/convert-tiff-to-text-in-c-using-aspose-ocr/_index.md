---
category: general
date: 2026-03-05
description: Převádějte TIFF na text v C# rychle pomocí Aspose OCR. Naučte se, jak
  během několika minut zobrazit OCR text z vícestránkových TIFF souborů.
draft: false
keywords:
- convert tiff to text
- aspose ocr c#
- display ocr text
language: cs
og_description: Převod TIFF na text v C# s Aspose OCR. Tento průvodce vám ukáže, jak
  krok za krokem zobrazit OCR text z vícestránkových TIFF obrázků.
og_title: Převod TIFF na text v C# – Kompletní průvodce Aspose OCR
tags:
- Aspose
- OCR
- C#
- TIFF
title: Převod TIFF na text v C# pomocí Aspose OCR
url: /cs/net/text-recognition/convert-tiff-to-text-in-c-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Převod TIFF na Text v C# pomocí Aspose OCR

Potřebujete **převést TIFF na text** v C#? Nejste v tom sami – mnoho vývojářů bojuje s extrahováním čitelných řetězců z více‑stránkových TIFF souborů. Dobrou zprávou je, že Aspose OCR C# dělá tuto práci téměř bezbolestnou a můžete **zobrazit OCR text** na konzoli nebo jej během několika sekund předat jinému systému.

V tomto tutoriálu vás provedeme kompletním, připraveným příkladem, který přesně ukazuje, jak načíst více‑stránkový TIFF, spustit OCR a vytisknout text každé stránky. Žádné skryté kroky, žádné zkratky typu „viz dokumentace“. Na konci budete mít samostatný program, který můžete vložit do libovolného .NET projektu.

## Co budete potřebovat

- .NET 6.0 nebo novější (příklad cílí na .NET 6, ale .NET 5 také funguje)  
- Platný licenční soubor Aspose OCR (`Aspose.OCR.lic`). Knihovna funguje i bez licence, ale zobrazí 20‑sekundovou zkušební vodoznak.  
- Více‑stránkový TIFF soubor, který chcete zpracovat (budeme jej nazývat `multipage.tif`).  
- Visual Studio 2022 nebo jakýkoli editor, který preferujete – nic exotického.

Pokud máte vše připravené, pojďme na to.

## Krok 1: Instalace NuGet balíčku Aspose OCR

Než se spustí jakýkoli kód, potřebujete samotnou knihovnu. Otevřete terminál ve složce projektu a spusťte:

```bash
dotnet add package Aspose.OCR
```

Tento jednorázový příkaz stáhne nejnovější stabilní verzi (k březnu 2026 je to 23.9).  

> **Tip:** Udržujte své balíčky aktuální; novější verze často obsahují vylepšení výkonu pro velké TIFF soubory.

## Krok 2: Nastavení licence Aspose OCR C# (volitelné, ale doporučené)

Spuštění OCR enginu bez licence je možné, ale výstup bude předponován varováním o zkušební verzi. Abyste tomu předešli, nasměrujte engine na váš soubor `.lic`:

```csharp
using Aspose.OCR;

// ...

// Step 2: Apply your Aspose OCR license (optional but recommended)
var ocrEngine = new OcrEngine();
ocrEngine.SetLicense(@"C:\Licenses\Aspose.OCR.lic");
```

Pokud tento krok přeskočíte, kód stále funguje – jen si pamatujte na dodatečný text ve výsledcích.

## Krok 3: Načtení a rozpoznání více‑stránkového TIFF

Nyní skutečně **převádíme TIFF na text**. Pomocná metoda `ImageStream.FromFile` načte soubor do formátu, který engine rozumí. Poté zavoláme `Recognize()`, která vrací objekt `OcrResult` obsahující text každé stránky.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

// ...

// Step 3: Load the multi‑page TIFF image to be processed
ocrEngine.Image = ImageStream.FromFile(@"C:\Images\multipage.tif");

// Step 4: Perform OCR on the loaded image
OcrResult ocrResult = ocrEngine.Recognize();
```

> **Proč je to důležité:** `Recognize()` provádí těžkou práci – analýzu pixelů, detekci jazyka a rekonstrukci řádků textu – vše v nativním C# kódu. Objekt výsledku vám poskytuje přístup stránka po stránce, což je ideální pro pozdější **zobrazení OCR textu**.

## Krok 4: Procházení stránek a **zobrazení OCR textu**

S výsledkem v ruce jednoduše projdeme stránky a každou vytiskneme. Toto je část, kde skutečně vidíte převod z obrázku na prostý text.

```csharp
// Step 5: Iterate through each page of the result and display the recognized text
for (int pageIndex = 0; pageIndex < ocrResult.PageCount; pageIndex++)
{
    Console.WriteLine($"--- Page {pageIndex + 1} ---");
    Console.WriteLine(ocrResult.GetPageText(pageIndex));
    Console.WriteLine(); // Blank line for readability
}
```

Spuštění programu vypíše výstup podobný následujícímu (váš skutečný text se bude lišit podle obsahu TIFF):

```
--- Page 1 ---
Hello, world!
This is the first page of our multi‑page TIFF.

--- Page 2 ---
Second page starts here.
More sample text follows.
```

A to je vše – úspěšně jste **převáděli TIFF na text** a **zobrazili OCR text** pro každou stránku.

## Kompletní funkční příklad

Níže je kompletní program, který můžete zkopírovat a vložit do nového konzolového projektu (`dotnet new console`). Obsahuje všechny using direktivy, zpracování licence a kontrolu chyb.

```csharp
// ConvertTiffToText.cs
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace ConvertTiffToText
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // Step 1: Create an OCR engine instance
            // -----------------------------------------------------------------
            var ocrEngine = new OcrEngine();

            // -----------------------------------------------------------------
            // Step 2: Apply your Aspose OCR license (optional but recommended)
            // -----------------------------------------------------------------
            try
            {
                ocrEngine.SetLicense(@"C:\Licenses\Aspose.OCR.lic");
            }
            catch (Exception ex)
            {
                Console.WriteLine("License file not found or invalid. Running in trial mode.");
                Console.WriteLine($"Details: {ex.Message}");
            }

            // -----------------------------------------------------------------
            // Step 3: Load the multi‑page TIFF image to be processed
            // -----------------------------------------------------------------
            const string tiffPath = @"C:\Images\multipage.tif";

            if (!System.IO.File.Exists(tiffPath))
            {
                Console.WriteLine($"Error: TIFF file not found at {tiffPath}");
                return;
            }

            ocrEngine.Image = ImageStream.FromFile(tiffPath);

            // -----------------------------------------------------------------
            // Step 4: Perform OCR – this is where we convert TIFF to text
            // -----------------------------------------------------------------
            OcrResult ocrResult = ocrEngine.Recognize();

            // -----------------------------------------------------------------
            // Step 5: Iterate through each page and display OCR text
            // -----------------------------------------------------------------
            Console.WriteLine($"Successfully processed {ocrResult.PageCount} page(s).");
            for (int i = 0; i < ocrResult.PageCount; i++)
            {
                Console.WriteLine($"--- Page {i + 1} ---");
                Console.WriteLine(ocrResult.GetPageText(i));
                Console.WriteLine(); // Add spacing between pages
            }

            // Keep the console window open when debugging
            Console.WriteLine("Press any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**Očekávaný výstup** (zkrácený pro stručnost) je zobrazen výše. Pokud vidíte zkušební vodoznak, dvakrát zkontrolujte, že cesta k licenci je správná.

## Časté problémy při převodu TIFF na text

| Problém | Proč se to děje | Jak opravit |
|-------|----------------|------------|
| **Nedostatek paměti u obrovských TIFF** | Engine načítá celý obrázek do RAM. | Použijte `ImageStream.FromFile(..., loadOnlyFirstPage: false)` a zpracovávejte stránky po dávkách, nebo zvýšte limit paměti procesu. |
| **Špatné znaky** | Nízké rozlišení zdrojových obrázků zmátne OCR engine. | Předzpracujte TIFF (např. zvýšte DPI na 300) před předáním Aspose OCR. |
| **Licence nebyla použita** | `SetLicense` vyhodí výjimku, kterou ignorujete. | Zabalte volání do try/catch (jak je ukázáno) a zaznamenejte chybu. |
| **Chybějící jazyková data** | Ve výchozím nastavení OCR předpokládá angličtinu. | Nastavte `ocrEngine.Language = OcrLanguage.French;` (nebo jakýkoli podporovaný jazyk) před voláním `Recognize()`. |

Řešení těchto okrajových případů zajistí, že váš převod bude v produkci běžet hladce.

## Další kroky: Přesahování jednoduchého zobrazení

Nyní, když můžete **převádět TIFF na text** a **zobrazovat OCR text**, můžete chtít:

- **Uložit extrahovaný text** do souboru `.txt` nebo databáze pro pozdější analýzu.  
- **Spojit více TIFF** do jednoho prohledávatelného PDF pomocí Aspose.PDF.  
- **Použít post‑processing** (kontrola pravopisu, čištění pomocí regexu) pro zvýšení přesnosti.  

Všechny tyto rozšíření staví na stejném základním vzoru, který jsme právě prošli.

---

### TL;DR

Prošli jsme kompletním C# řešením, které **převádí TIFF na text** pomocí Aspose OCR C#. Kód vytvoří `OcrEngine`, volitelně načte licenci, načte více‑stránkový TIFF, spustí OCR a **zobrazuje OCR text** stránku po stránce. S poskytnutým kompletním příkladem můžete tento kód vložit do libovolného .NET projektu a okamžitě začít extrahovat text.

Máte otázky ohledně výkonu, podpory jazyků nebo integrace s dalšími produkty Aspose? Zanechte komentář níže – šťastné programování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}