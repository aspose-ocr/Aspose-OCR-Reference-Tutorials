---
category: general
date: 2026-02-20
description: Jak provést OCR na souborech DjVu v C#. Naučte se rozpoznávat text z
  obrázku a rychle převádět DjVu na text pomocí Aspose OCR.
draft: false
keywords:
- how to perform OCR
- recognize text from image
- how to read djvu
- extract text from image
- convert djvu to text
language: cs
og_description: Jak provádět OCR na souborech DjVu v C#. Tento tutoriál vám ukáže,
  jak rozpoznat text z obrázku, číst DjVu a převést DjVu na text pomocí Aspose OCR.
og_title: Jak provést OCR na souborech DjVu v C# – Kompletní průvodce
tags:
- OCR
- C#
- DjVu
- Aspose
title: Jak provést OCR u souborů DjVu v C# – krok za krokem
url: /cs/net/text-recognition/how-to-perform-ocr-on-djvu-files-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak provést OCR na souborech DjVu v C# – Kompletní průvodce

Už jste se někdy zamýšleli **jak provést OCR** na dokumentu DjVu, aniž byste si trhali vlasy? Nejste v tom sami. Mnoho vývojářů narazí na problém, když potřebují **rozpoznat text z obrázku** zdrojů, které jsou uvnitř kontejnerů DjVu. Dobrá zpráva? S několika řádky C# a knihovnou Aspose OCR můžete ten skrytý text extrahovat během okamžiku.

V tomto tutoriálu projdeme vše, co potřebujete k převodu stránky DjVu na prostý text. Na konci budete vědět **jak číst DjVu**, jak **extrahovat text z obrázku** objektů a dokonce **jak převést DjVu na text** pro následné zpracování. Žádné externí služby, žádné nejasné odkazy – jen samostatný, spustitelný příklad.

## Požadavky

- .NET 6.0 SDK nebo novější (kód funguje také s .NET Framework 4.8).
- Visual Studio 2022 nebo jakýkoli editor, který podporuje C#.
- Licence Aspose OCR pro .NET (zdarma zkušební verze funguje pro testování).
- Vzorek souboru DjVu (`sample.djvu`) umístěný ve složce, na kterou můžete odkazovat.

Mít tyto věci připravené zajistí plynulý průběh – žádná překvapení typu „chybějící reference“ později.

## Jak provést OCR na stránce DjVu

Základní myšlenka je jednoduchá: načíst stránku DjVu jako obrázek, předat ji OCR enginu a přečíst výsledný řetězec. Rozložme to krok po kroku.

### Krok 1: Nainstalovat Aspose OCR

Otevřete terminál ve složce projektu a spusťte:

```bash
dotnet add package Aspose.OCR
```

Tím se stáhnou nejnovější binární soubory Aspose OCR a jejich závislosti. Pokud dáváte přednost UI NuGet Package Manageru, stačí vyhledat **Aspose.OCR** a kliknout **Install**.

### Krok 2: Inicializovat OCR engine

Vytvoření instance `OcrEngine` je první věc, kterou uděláte, když chcete **provést OCR**. Představte si to jako zapnutí mozku skeneru.

```csharp
using Aspose.OCR;

// ...

// Step 2: Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();
```

> **Tip:** Opětovné použití jedné instance `OcrEngine` pro více stránek šetří paměť a zrychluje zpracování.

### Krok 3: Načíst stránku DjVu jako obrázek

Soubory DjVu nejsou přímo podporovány většinou obrazových API, ale Aspose může každou stránku zacházet jako bitmapu. Zde používáme `System.Drawing.Image` k načtení souboru.

```csharp
using System.Drawing;

// ...

// Step 3: Load a DjVu page as an image
string djvuPath = @"C:\Path\To\Your\Directory\sample.djvu";
Image djvuPage = Image.FromFile(djvuPath);
```

> **Proč to funguje:** `Image.FromFile` automaticky dekóduje DjVu stream do rastrového formátu, který OCR engine rozumí. Pokud potřebujete zpracovat konkrétní stránku z více‑stránkového DjVu, použijte Aspose PDF nebo Aspose Imaging k nejprve extrahování stránky.

### Krok 4: Rozpoznat text z obrázku

Nyní se děje magie. Metoda `Recognize` prohledá bitmapu a vrátí řetězec obsahující rozpoznané znaky.

```csharp
// Step 4: Perform OCR to extract text from the image
string extractedText = ocrEngine.Recognize(djvuPage);
```

V tomto okamžiku jste **rozpoznali text z obrázku** dat, která původně byla uvnitř kontejneru DjVu. Řetězec může obsahovat zalomení řádků, interpunkci a dokonce i Unicode znaky, pokud zdrojový jazyk podporuje.

### Krok 5: Zobrazit nebo uložit výsledek

Pro rychlou kontrolu stačí vypsat text do konzole. Ve skutečné aplikaci byste jej pravděpodobně zapisovali do souboru nebo databáze.

```csharp
// Step 5: Display the recognized text
Console.WriteLine("=== Extracted Text ===");
Console.WriteLine(extractedText);
```

Spojením všech částí získáte kompletní, připravený k spuštění program.

```csharp
// File: DjvuOcrExample.cs
using System;
using System.Drawing;
using Aspose.OCR;

class DjvuExample
{
    static void Main()
    {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Load a DjVu page as an image
        Image djvuPage = Image.FromFile(@"C:\Path\To\Your\Directory\sample.djvu");

        // Perform OCR to extract text from the image
        string extractedText = ocrEngine.Recognize(djvuPage);

        // Display the recognized text
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(extractedText);
    }
}
```

**Očekávaný výstup** (zkrácený pro stručnost):

```
=== Extracted Text ===
The quick brown fox jumps over the lazy dog.
Lorem ipsum dolor sit amet, consectetur...
```

Pokud vidíte poškozené znaky, zkontrolujte, že soubor DjVu není šifrovaný a že jste nastavili správný jazyk v `ocrEngine.Language`. Ve výchozím nastavení předpokládá angličtinu; můžete přepnout na francouzštinu, němčinu atd. přiřazením `ocrEngine.Language = Language.French;`.

## Rozpoznání textu z obrázku – Časté úskalí

I když máte solidní příklad, vývojáři často narazí na několik okrajových případů:

| Problém | Proč se to děje | Řešení |
|-------|----------------|-----|
| **Prázdný výstup** | Rozlišení obrázku je příliš nízké (<300 dpi). | Použijte `ocrEngine.ImageResolution = 300;` před voláním `Recognize`. |
| **Špatný jazyk** | OCR ve výchozím nastavení používá angličtinu. | Nastavte `ocrEngine.Language = Language.Spanish;` (nebo jakýkoli podporovaný jazyk). |
| **Únik paměti** | Velké stránky DjVu zůstávají v paměti po zpracování. | Po dokončení zavolejte `djvuPage.Dispose();`. |
| **Více‑stránkový DjVu** | Načte se pouze první stránka. | Procházejte stránky pomocí třídy `DjvuImage` z Aspose Imaging. |

Řešení těchto problémů včas vám ušetří nespočet hodin ladění.

## Jak číst soubory DjVu v C# – Mimo jednoduché OCR

Pokud váš projekt vyžaduje více než jednu stránku, budete muset nejprve extrahovat každou stránku jako obrázek. Aspose Imaging to usnadňuje:

```csharp
using Aspose.Imaging;
using Aspose.Imaging.FileFormats.Djvu;

// ...

string djvuPath = @"sample.djvu";
using (DjvuImage djvu = (DjvuImage)Image.Load(djvuPath))
{
    for (int i = 0; i < djvu.Frames.Count; i++)
    {
        using (Image page = djvu.Frames[i].ConvertToRaster())
        {
            // Run OCR on each page
            string pageText = ocrEngine.Recognize(page);
            Console.WriteLine($"--- Page {i + 1} ---");
            Console.WriteLine(pageText);
        }
    }
}
```

Tento vzor vám umožní **převést DjVu na text** stránku po stránce, ideální pro dávkové zpracování velkých archivů.

## Extrahování textu z obrázku – Ladění přesnosti

Výchozí nastavení OCR funguje dobře pro čisté skeny, ale můžete zvýšit přesnost:

```csharp
ocrEngine.ImagePreprocessingOptions = new ImagePreprocessingOptions()
{
    // Binarize the image to improve contrast
    BinarizationMethod = BinarizationMethod.Otsu,
    // Deskew the image if it’s tilted
    Deskew = true,
    // Remove noise
    NoiseRemoval = true
};
```

Tyto úpravy jsou zvláště užitečné, když zdroj DjVu obsahuje ručně psané poznámky nebo grafiku s nízkým kontrastem.

## Převod DjVu na text – Kompletní end‑to‑end příklad

Níže je kompaktní verze, která spojuje vše: načtení více‑stránkového DjVu, předzpracování každé stránky, provedení OCR a uložení výstupu do souboru `.txt`.

```csharp
using System;
using System.IO;
using Aspose.Imaging;
using Aspose.Imaging.FileFormats.Djvu;
using Aspose.OCR;
using Aspose.OCR.Models;

class DjvuToTextConverter
{
    static void Main()
    {
        // Prepare OCR engine with preprocessing
        OcrEngine ocr = new OcrEngine
        {
            ImagePreprocessingOptions = new ImagePreprocessingOptions()
            {
                BinarizationMethod = BinarizationMethod.Otsu,
                Deskew = true,
                NoiseRemoval = true
            }
        };

        string inputPath = @"C:\Docs\sample.djvu";
        string outputPath = @"C:\Docs\sample_extracted.txt";

        using (DjvuImage djvu = (DjvuImage)Image.Load(inputPath))
        using (StreamWriter writer = new StreamWriter(outputPath))
        {
            for (int i = 0; i < djvu.Frames.Count; i++)
            {
                using (var page = djvu.Frames[i].ConvertToRaster())
                {
                    string text = ocr.Recognize(page);
                    writer.WriteLine($"--- Page {i + 1} ---");
                    writer.WriteLine(text);
                }
            }
        }

        Console.WriteLine($"Extraction complete. Text saved to {outputPath}");
    }
}
```

Spuštěním tohoto skriptu se vytvoří `sample_extracted.txt` s obsahem každé stránky přehledně odděleným. Je to nejrychlejší způsob, jak **převést DjVu na text** pro indexování, vyhledávání nebo archivaci.

## Závěr

Probrali jsme **jak provést OCR** na souborech DjVu od začátku do konce, prozkoumali způsoby, jak **rozpoznat text z

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}