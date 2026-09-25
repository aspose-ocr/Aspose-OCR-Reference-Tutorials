---
category: general
date: 2026-01-04
description: Naučte se, jak povolit formuláře a extrahovat tabulky z obrázků pomocí
  OCR v C#. Tento krok‑za‑krokem návod také ukazuje, jak spustit OCR na obrázku a
  detekovat tabulky pomocí OCR.
draft: false
keywords:
- how to enable forms
- how to extract tables
- run OCR image
- use OCR C#
- detect tables OCR
language: cs
og_description: Krok za krokem průvodce, jak povolit formuláře, extrahovat tabulky,
  spustit OCR obrázku a detekovat tabulky pomocí OCR v C#.
og_title: Jak povolit formuláře a extrahovat tabulky pomocí OCR v C#
tags:
- OCR
- C#
- Computer Vision
title: Jak povolit formuláře a extrahovat tabulky pomocí OCR v C# – Kompletní průvodce
url: /cs/net/image-and-drawing-recognition/how-to-enable-forms-and-extract-tables-with-ocr-in-c-complet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak povolit formuláře a extrahovat tabulky pomocí OCR v C# – Kompletní průvodce

Už jste se někdy zamysleli **jak povolit formuláře**, když skenujete faktury, účtenky nebo jakýkoli strukturovaný dokument? Nejste v tom sami. V mnoha reálných projektech je největší překážkou získat OCR, aby rozuměl jak polím formuláře **tak i** tabulkám, aniž byste museli psát milion řádků vlastního parsování.  

V tomto tutoriálu projdeme praktické, end‑to‑end řešení, které ukazuje **jak povolit formuláře**, **jak extrahovat tabulky** a dokonce **jak spustit OCR zpracování obrázku** v jediném C# programu. Na konci budete mít připravený úryvek kódu, který detekuje tabulky OCR‑styl, vytáhne páry klíč‑hodnota a vypíše je do konzole.

> **Požadavky** – .NET 6+ (nebo .NET Framework 4.7+), reference na OCR SDK, které používáte (příklad předpokládá obecnou třídu `OcrEngine`), a soubor obrázku (`invoice_table.png`) obsahující tabulku nebo formulář. Žádné další externí knihovny nejsou potřeba.

![jak povolit formuláře s OCR C#](image.png)

## Co tento tutoriál pokrývá

- **Povolení rozpoznávání formulářů**, aby pole jako „Invoice Number“ nebo „Date“ byla automaticky identifikována.  
- **Extrahování tabulek** ze skenovaných dokumentů, včetně počtu řádků/sloupců a obsahu buněk.  
- **Spuštění OCR zpracování obrázku** jedním voláním a programové zpracování výsledku.  
- Tipy pro **detekci tabulek OCR** v okrajových případech, jako jsou sloučené buňky nebo chybějící okraje.  

Pojďme na to.

## Krok 1: Nastavení OCR enginu – jak povolit formuláře

Než může dojít k jakémukoli rozpoznání, potřebujete instanci OCR enginu. Většina SDK poskytuje jednoduchý konstruktor; také ukážeme, kde můžete později doladit konfigurační možnosti.

```csharp
using System;
using System.Linq;

// Assume the OCR SDK namespace is OcrSdk
using OcrSdk;

public class OcrDemo
{
    public static void Main()
    {
        // Create the OCR engine – this is where “how to enable forms” starts.
        OcrEngine ocrEngine = new OcrEngine();

        // Load the image that contains a table or form.
        // Replace the path with the actual location of your PNG/JPEG/TIFF file.
        ocrEngine.LoadImage(@"YOUR_DIRECTORY/invoice_table.png");
```

**Proč je to důležité:** Vytvoření instance alokuje interní zdroje (např. jazykové modely). Pokud tento krok přeskočíte, následné volání `Recognize` vyhodí `NullReferenceException`.

## Krok 2: Zapnutí strukturovaného extrahování – jak extrahovat tabulky & detekovat tabulky OCR

Nyní povolíme dvě hlavní funkce: rozpoznávání tabulek a extrakci polí formuláře. Moderní OCR enginy obvykle nabízejí booleanové příznaky nebo podrobnější objekt `Config`.

```csharp
        // Enable structured extraction features.
        ocrEngine.Config.EnableTableRecognition = true;   // detect tables OCR
        ocrEngine.Config.EnableFormRecognition = true;    // how to enable forms
```

**Profesionální tip:** Pokud potřebujete jen jednu z funkcí, vypnutí druhé může zlepšit výkon až o 20 %.

## Krok 3: Spuštění OCR obrázku a získání výsledku – run OCR image

S nastaveným enginem jeden volání provede těžkou práci. Vrácený `OcrResult` obsahuje kolekce pro tabulky i pole formuláře.

```csharp
        // Run OCR – this is the “run OCR image” step.
        OcrResult ocrResult = ocrEngine.Recognize();

        // -----------------------------------------------------------------
        // Step 4: Process Detected Tables – how to extract tables
        // -----------------------------------------------------------------
        foreach (var table in ocrResult.Tables)
        {
            Console.WriteLine($"Table {table.Id}: {table.Rows.Count} rows, {table.Columns.Count} columns");

            // Show the first row for a quick sanity check.
            if (table.Rows.Count > 0)
            {
                var firstRow = table.Rows[0];
                Console.WriteLine(string.Join(" | ", firstRow.Cells.Select(c => c.Text)));
            }
        }

        // -----------------------------------------------------------------
        // Step 5: Process Detected Form Fields – how to enable forms
        // -----------------------------------------------------------------
        foreach (var field in ocrResult.FormFields)
        {
            Console.WriteLine($"{field.Key}: {field.Value}");
        }
    }
}
```

### Očekávaný výstup v konzoli

```
Table 1: 5 rows, 4 columns
Item | Qty | Price | Total
InvoiceNumber: INV-2025-001
Date: 2025-12-31
Customer: Acme Corp.
```

Přesná čísla se budou lišit podle vašeho vstupního obrázku, ale měli byste vidět souhrnný řádek pro každou tabulku následovaný hodnotami buněk prvního řádku a pak seznamem párů klíč‑hodnota pro pole formuláře.

## Krok 4: Řešení okrajových případů při detekci tabulek OCR

I při `EnableTableRecognition = true` může OCR narazit na:

| Problém | Proč k tomu dochází | Rychlé řešení |
|---------|---------------------|---------------|
| **Sloučené buňky** | Engine považuje sloučenou oblast za jednu buňku. | Post‑process řádky: hledejte neobvykle široké buňky a rozdělte je podle mezer. |
| **Chybějící okraje** | Čáry tabulky jsou slabé nebo přerušené. | Zvyšte kontrast obrázku před předáním enginu (`ocrEngine.PreprocessImage`). |
| **Otočené tabulky** | Dokument naskenován pod úhlem. | Použijte `ocrEngine.Config.AutoRotate = true` (pokud je k dispozici). |

**Tip:** Vždy ověřte `table.Rows.Count` a `table.Columns.Count` před přístupem k indexům, abyste předešli `IndexOutOfRangeException`.

## Krok 5: Sestavení všeho dohromady – kompletní, spustitelný příklad

Níže je celý program, který můžete zkopírovat do nového konzolového projektu. Obsahuje `using` direktivy, nastavení enginu i logiku zpracování ukázanou dříve.

```csharp
using System;
using System.Linq;
using OcrSdk;   // Replace with your actual OCR SDK namespace

public class OcrDemo
{
    public static void Main()
    {
        // 1️⃣ Create OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Load the target image
        ocrEngine.LoadImage(@"YOUR_DIRECTORY/invoice_table.png");

        // 3️⃣ Enable structured extraction (forms + tables)
        ocrEngine.Config.EnableTableRecognition = true;   // detect tables OCR
        ocrEngine.Config.EnableFormRecognition = true;    // how to enable forms

        // 4️⃣ Run OCR – “run OCR image”
        OcrResult ocrResult = ocrEngine.Recognize();

        // 5️⃣ Process tables – “how to extract tables”
        foreach (var table in ocrResult.Tables)
        {
            Console.WriteLine($"Table {table.Id}: {table.Rows.Count} rows, {table.Columns.Count} columns");
            if (table.Rows.Count > 0)
            {
                var firstRow = table.Rows[0];
                Console.WriteLine(string.Join(" | ", firstRow.Cells.Select(c => c.Text)));
            }
        }

        // 6️⃣ Process form fields – “how to enable forms”
        foreach (var field in ocrResult.FormFields)
        {
            Console.WriteLine($"{field.Key}: {field.Value}");
        }
    }
}
```

Spusťte program (`dotnet run` nebo `Ctrl+F5` ve Visual Studiu) a uvidíte výstup v konzoli popsaný výše.

## Často kladené otázky (FAQ)

**Q:** Funguje to s PDF vstupem?  
**A:** Většina OCR SDK přijímá PDF tím, že interně rasterizuje každou stránku. Stačí zavolat `ocrEngine.LoadPdf("file.pdf")` místo `LoadImage`.

**Q:** Co když můj obrázek obsahuje jak tabulku, *tak* podpis?  
**A:** Podpis se objeví jako samostatná oblast obrázku. Můžete jej ignorovat kontrolou `ocrResult.Images` pro text s nízkou důvěrou.

**Q:** Můžu exportovat tabulky do CSV?  
**A:** Rozhodně. Po iteraci přes `table.Rows` zapíšete každý `cell.Text` do `StringBuilder` odděleného čárkami a pak uložíte řetězec do souboru `.csv`.

## Závěr

Nyní víte **jak povolit formuláře**, **jak extrahovat tabulky** a přesné kroky k **spuštění OCR zpracování obrázku** pomocí C#. Příklad demonstruje celý workflow – od vytvoření enginu, přes konfiguraci, až po zpracování výsledků – takže jej můžete rovnou vložit do svých projektů.  

Dále zkuste nahradit ukázkový obrázek PDF fakturou s více stránkami, experimentujte s `ocrEngine.Config.AutoRotate`, nebo přeneste extrahovaná data do databáze. Tyto rozšíření prohloubí vaši znalost **detekce tabulek OCR** a **používání OCR v C#** v produkčních scénářích.

Pokud narazíte na problémy, neváhejte zanechat komentář níže. Šťastné programování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}