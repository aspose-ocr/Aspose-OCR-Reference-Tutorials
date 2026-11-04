---
category: general
date: 2026-05-06
description: Naučte se provádět hromadné OCR v C# a rychle extrahovat text ze skenů
  pomocí Aspose OCR Batch. Postupujte podle kompletního průvodce krok za krokem s
  kódem, tipy a řešením okrajových případů.
draft: false
keywords:
- how to batch OCR
- extract text from scans
- Aspose OCR batch processing
- C# OCR automation
- GPU accelerated OCR
language: cs
og_description: Jak provádět hromadné OCR v C#? Tento průvodce vám ukáže, jak efektivně
  extrahovat text ze skenů pomocí Aspose OCR, podpory GPU a paralelního zpracování.
og_title: Jak provádět dávkové OCR v C# – Extrahovat text ze skenů
tags:
- C#
- OCR
- Aspose
title: Jak provádět dávkové OCR v C# – Extrahovat text ze skenů
url: /cs/net/text-recognition/how-to-batch-ocr-in-c-extract-text-from-scans/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak provádět dávkové OCR v C# – Extrahovat text ze skenů

Už jste se někdy zamýšleli **jak provádět dávkové OCR**, když máte složku plnou naskenovaných PDF nebo JPEG? Nejste jediní, kdo se dívá na horu obrázků a přemýšlí: „Musí existovat rychlejší způsob, jak získat text.“ V tomto tutoriálu projdeme praktické řešení, které vám nejen umožní **extrahovat text ze skenů**, ale také urychlí proces pomocí GPU akcelerace a paralelismu.

Jde o to, že provádět OCR po jednom souboru je obrovská ztráta času, zejména pokud máte desítky nebo stovky stránek. Na konci tohoto návodu budete mít připravenou spustitelnou C# konzolovou aplikaci, která zpracuje celý adresář jedním příkazem a poskytne vám čisté textové soubory připravené k indexaci, vyhledávání nebo čemukoli dalšímu.

## Požadavky

- **.NET 6.0 nebo novější** (kód používá moderní funkce C#).
- Licence pro **Aspose.OCR** (bezplatná zkušební verze funguje pro testování).
- Počítač kompatibilní s GPU **pokud chcete povolit `UseGpu`**; jinak se knihovna vrátí na CPU.
- Základní znalost **C# konzolových aplikací**.

Žádné externí služby, žádné skryté konfigurační soubory – jen SDK a složka s obrázky.

## Krok 1: Nainstalujte NuGet balíček Aspose.OCR

Nejprve přidejte knihovnu Aspose OCR do svého projektu. Otevřete terminál ve složce řešení a spusťte:

```bash
dotnet add package Aspose.OCR
```

> **Tip:** Pokud používáte Visual Studio, můžete balíček také přidat přes UI NuGet Package Manager.

## Krok 2: Vytvořte kostru konzolové aplikace

Nastavme minimální konzolovou aplikaci, která bude hostovat náš dávkový procesor. Vytvořte nový soubor s názvem `Program.cs` a vložte následující kostru:

```csharp
using System;
using Aspose.OCR.Batch;

namespace BatchOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll configure and run the OCR batch processor here.
        }
    }
}
```

Proč zabalit logiku do `Main`? Protože konzolová aplikace nám poskytuje okamžitou zpětnou vazbu pomocí `Console.WriteLine`, což je ideální pro rychlé ověření, že úloha **dávkového OCR** skutečně dokončila.

## Krok 3: Nakonfigurujte OcrBatchProcessor

Nyní samotné jádro řešení. Vytvoříme instanci `OcrBatchProcessor`, nasměrujeme ji na vstupní složku, určíme kam uložit výsledky a upravíme několik parametrů výkonu.

```csharp
// Step 3: Configure the OCR batch processor
var batch = new OcrBatchProcessor
{
    // Folder that contains the source images to be processed
    InputFolder = @"YOUR_DIRECTORY/Scans",

    // Folder where the OCR results will be saved
    OutputFolder = @"YOUR_DIRECTORY/OcrResults",

    // Specify the language of the documents (Spanish in this example)
    Language = OcrLanguage.Spanish,

    // Enable GPU acceleration for faster processing (if available)
    UseGpu = true,

    // Limit the number of concurrent OCR operations
    MaxDegreeOfParallelism = 4
};
```

### Proč jsou tato nastavení důležitá

| Nastavení | Co dělá | Kdy byste jej mohli změnit |
|-----------|----------|----------------------------|
| `InputFolder` | Cesta ke skenům, které chcete zpracovat. | Použijte relativní cestu pro přenositelnost. |
| `OutputFolder` | Kam bude uložen extrahovaný text každého obrázku jako soubor `.txt`. | Nastavte na síťové sdílení, pokud potřebujete centrální úložiště. |
| `Language` | Model jazyka OCR; zvolili jsme španělštinu pro ukázku vícejazyčné podpory. | Přepněte na `OcrLanguage.English` nebo jakýkoli podporovaný jazyk. |
| `UseGpu` | Přenáší těžké maticové výpočty na GPU. | Nastavte na `false` na serverech bez GPU. |
| `MaxDegreeOfParallelism` | Řídí, kolik obrázků se zpracovává najednou. | Snižte na strojích s nízkým CPU, aby nedošlo k přetížení. |

## Krok 4: Proveďte dávkovou operaci s ošetřením chyb

Spuštění dávky je tak jednoduché jako zavolat `Execute()`, ale zabalíme to do bloku try‑catch, abyste dostali užitečnou zprávu, pokud se něco pokazí (např. chybějící složka, nepodporovaný formát obrázku).

```csharp
try
{
    // Step 4: Run the batch OCR operation
    batch.Execute();

    // Step 5: Inform the user that processing has finished
    Console.WriteLine("Batch completed.");
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Error during batch OCR: {ex.Message}");
}
```

Až procesor dokončí, uvidíte v konzoli **Batch completed.** a ke každému zdrojovému obrázku bude v `OcrResults` odpovídající soubor `.txt`. Název souboru se shoduje s originálem, což usnadňuje mapování zpět na původní sken.

## Krok 5: Ověřte výstup – Co očekávat

Po spuštění programu otevřete libovolný soubor ve složce `YOUR_DIRECTORY/OcrResults`. Měli byste vidět čistý text extrahovaný z odpovídajícího obrázku, například:

```
Este es un documento de prueba.
Contiene varias líneas de texto.
```

Pokud výstup vypadá poškozeně, zkontrolujte, zda `Language` odpovídá jazyku vašich skenů. Aspose OCR podporuje více než 100 jazyků, takže můžete nahradit `OcrLanguage.Spanish` libovolným potřebným jazykem.

## Řešení okrajových případů a běžných úskalí

### 1. GPU není k dispozici

Pokud váš počítač nemá kompatibilní GPU, `UseGpu = true` se tiše vrátí do režimu CPU, ale ztratíte rychlostní zisk. Pro explicitnost můžete detekovat schopnost GPU:

```csharp
if (!OcrBatchProcessor.IsGpuSupported)
{
    batch.UseGpu = false;
    Console.WriteLine("GPU not detected – falling back to CPU processing.");
}
```

### 2. Velké soubory překračující paměť

Při práci s obrovskými TIFF nebo PDF zvažte jejich předběžné rozdělení na menší obrázky. Aspose OCR dokáže zpracovat více stránkové PDF, ale spotřeba paměti roste s počtem stránek. Jednoduchý předzpracovatelský krok pomocí `Aspose.Imaging` může dokument rozdělit na zvládnutelné části.

### 3. Soubory, které nejsou obrázky, ve vstupní složce

Dávkový procesor ignoruje soubory, které nedokáže zpracovat, ale je dobré udržovat složku čistou. Můžete filtrovat podle přípony:

```csharp
batch.InputFolder = @"YOUR_DIRECTORY/Scans";
batch.FileFilter = file => file.EndsWith(".png", StringComparison.OrdinalIgnoreCase)
                         || file.EndsWith(".jpg", StringComparison.OrdinalIgnoreCase);
```

*(Poznámka: `FileFilter` je hypotetická vlastnost; nahraďte ji skutečným API, pokud je k dispozici.)*

## Kompletní funkční příklad

Níže je kompletní program připravený ke zkopírování a vložení. Nahraďte `YOUR_DIRECTORY` absolutní cestou na vašem počítači.

```csharp
using System;
using Aspose.OCR.Batch;

namespace BatchOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Configure the batch processor
            var batch = new OcrBatchProcessor
            {
                InputFolder = @"C:\MyScans",          // <-- change this
                OutputFolder = @"C:\OcrResults",     // <-- change this
                Language = OcrLanguage.Spanish,
                UseGpu = true,
                MaxDegreeOfParallelism = 4
            };

            // Optional: fall back to CPU if no GPU is found
            if (!OcrBatchProcessor.IsGpuSupported)
            {
                batch.UseGpu = false;
                Console.WriteLine("GPU not detected – using CPU.");
            }

            try
            {
                // Run the batch job
                batch.Execute();

                Console.WriteLine("Batch completed.");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"Error during batch OCR: {ex.Message}");
            }
        }
    }
}
```

### Očekávaný výstup v konzoli

```
Batch completed.
```

A v `C:\OcrResults` najdete soubor `.txt` pro každý obrázek ve `C:\MyScans`.

## Závěr

Nyní máte solidní, připravené pro produkci řešení, jak **provádět dávkové OCR** v C# a **extrahovat text ze skenů** bez ručního otevírání každého souboru. Využitím Aspose batch API, GPU akcelerace a konfigurovatelného paralelismu se řešení škáluje od několika stránek až po tisíce.

Co dál? Vyzkoušejte tyto nápady:

- **Integrovat s vyhledávacím indexem** (např. Elasticsearch), aby byl extrahovaný text prohledávatelný.
- **Přidat post‑processing** jako kontrolu pravopisu nebo detekci jazyka.
- **Zabalit konzolovou aplikaci do Windows služby** pro kontinuální sledování složky pro vkládání.

Neváhejte experimentovat, ladit úroveň paralelismu nebo vyměnit jazykový model. Pokud narazíte na problémy, zanechte komentář níže – šťastné OCRování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}