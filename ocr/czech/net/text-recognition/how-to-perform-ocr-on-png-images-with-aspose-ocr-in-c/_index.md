---
category: general
date: 2026-11-26
description: Naučte se, jak provádět OCR na souborech PNG, převádět PNG na text a
  extrahovat cyrilický text pomocí Aspose.OCR – krok za krokem průvodce pro vývojáře.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to perform OCR
- convert PNG to text
- recognize text from PNG
- extract Cyrillic text
- load image for OCR
language: cs
lastmod: 2026-11-26
og_description: Jak provést OCR na souborech PNG a extrahovat cyrilický text pomocí
  Aspose.OCR v C#. Sledujte tento kompletní návod k převodu PNG na text.
og_image_alt: how to perform OCR on a PNG image using Aspose.OCR
og_title: Jak provést OCR na PNG obrázcích pomocí Aspose.OCR – průvodce pro C#
schemas:
- author: Aspose
  dateModified: '2026-11-26'
  description: Learn how to perform OCR on PNG files, convert PNG to text, and extract
    Cyrillic text using Aspose.OCR – step‑by‑step guide for developers.
  headline: How to perform OCR on PNG images with Aspose.OCR in C#
  type: TechArticle
- description: Learn how to perform OCR on PNG files, convert PNG to text, and extract
    Cyrillic text using Aspose.OCR – step‑by‑step guide for developers.
  name: How to perform OCR on PNG images with Aspose.OCR in C#
  steps:
  - name: Handling large images
    text: 'If the PNG is larger than 2 MB, consider down‑scaling it before recognition
      to speed up processing:'
  - name: 'Edge case: Missing language module'
    text: 'If the download fails (e.g., offline environment), the engine throws an
      `OcrException`. Catch it to provide a graceful fallback:'
  - name: Expected output
    text: 'If `sample_image.png` contains the Cyrillic phrase “Привет мир”, the console
      will display:'
  - name: How it works
    text: 1. **Engine creation** – prepares the OCR pipeline. 2. **Image loading**
      – supports both raw PNG and down‑scaled versions for performance. 3. **Language
      selection** – demonstrates **extract Cyrillic text** while handling missing
      modules. 4. **Recognition** – the core **recognize text from PNG** call
  type: HowTo
tags:
- OCR
- C#
- Aspose.OCR
title: Jak provést OCR na PNG obrázcích pomocí Aspose.OCR v C#
url: /cs/net/text-recognition/how-to-perform-ocr-on-png-images-with-aspose-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak provést OCR na PNG obrázcích pomocí Aspose.OCR v C#

Pokud potřebujete **jak provést OCR** na souboru PNG, tento návod vám ukáže přesné kroky, jak převést PNG na text pomocí Aspose.OCR. Ať už extrahujete cyrilický text ze skenovaných dokumentů nebo jen rozpoznáváte text z PNG snímků obrazovky, řešení funguje ihned a vyžaduje jen několik řádků kódu v C#.

V tomto tutoriálu se naučíte, jak:

* **load image for OCR** z místní složky,
* nakonfigurovat engine pro **extract Cyrillic text**,
* **recognize text from PNG** a získat čistý řetězec,
* řešit běžné úskalí, jako jsou chybějící jazykové moduly a velké obrázky.

Žádná předchozí zkušenost s Aspose.OCR není vyžadována – stačí .NET vývojové prostředí a PNG obrázek, který chcete zpracovat.

## Požadavky

* .NET 6.0 (nebo novější) nainstalovaný.
* Licencovaná nebo zkušební kopie **Aspose.OCR for .NET**. Bezplatnou zkušební verzi můžete získat na webu Aspose.
* Visual Studio 2022 (nebo jakékoli IDE podporující .NET).
* PNG soubor obsahující text, který chcete extrahovat (v příkladu se používá `sample_image.png`).

## Krok 1: Instalace NuGet balíčku Aspose.OCR

Otevřete terminál ve složce projektu a spusťte:

```bash
dotnet add package Aspose.OCR
```

Balíček obsahuje jádro OCR enginu a všechny jazykové moduly. Když požádáte o jazyk, který není lokálně k dispozici, Aspose.OCR jej automaticky stáhne.

## Krok 2: Vytvoření instance OCR enginu (jak provést OCR)

Prvním konkrétním krokem v jakémkoli OCR workflow je vytvořit instanci enginu. Tento objekt spravuje všechny následné operace, jako je načtení obrázku a provedení rozpoznání.

```csharp
using Aspose.OCR;

// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();
```

**Why this matters:** Třída `OcrEngine` zapouzdřuje OCR pipeline. Vytvoření jediné instance a její opakované používání napříč více obrázky snižuje paměťovou zátěž a zlepšuje výkon.

## Krok 3: Načtení obrázku pro OCR – určení zdrojového PNG souboru

Načtení obrázku je okamžik, kdy **load image for OCR**. Aspose.OCR podporuje několik typů vstupu; nejjednodušší je `ImageStream.FromFile`.

```csharp
// Load the PNG image from disk
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/sample_image.png");
```

> **Pro tip:** Použijte absolutní cestu nebo `Path.Combine`, abyste se vyhnuli chybám za běhu v různých prostředích.

### Zpracování velkých obrázků

Pokud je PNG větší než 2 MB, zvažte jeho zmenšení před rozpoznáním, aby se zrychlilo zpracování:

```csharp
using System.Drawing;

// Downscale large images to a maximum width of 1200 pixels
Bitmap original = new Bitmap(@"YOUR_DIRECTORY/sample_image.png");
int maxWidth = 1200;
int newHeight = (int)(original.Height * (maxWidth / (double)original.Width));
Bitmap resized = new Bitmap(original, new Size(maxWidth, newHeight));

using (var ms = new MemoryStream())
{
    resized.Save(ms, System.Drawing.Imaging.ImageFormat.Png);
    ocrEngine.Image = ImageStream.FromStream(ms);
}
```

## Krok 4: Nastavení jazyka – extrakce cyrilického textu

Ve výchozím nastavení předpokládá Aspose.OCR angličtinu. Pro **extract Cyrillic text** nastavte vlastnost `Language` na `Language.Cyrillic`. Požadovaný modul bude automaticky stažen při prvním spuštění kódu.

```csharp
// Set the OCR language to Cyrillic
ocrEngine.Language = Language.Cyrillic;
```

Pokud potřebujete rozpoznávat více jazyků (např. angličtinu a cyriliku), můžete je kombinovat:

```csharp
ocrEngine.Language = Language.English | Language.Cyrillic;
```

### Okrajový případ: Chybějící jazykový modul

Pokud stažení selže (např. v offline prostředí), engine vyhodí `OcrException`. Zachyťte ji a poskytněte elegantní náhradní řešení:

```csharp
try
{
    ocrEngine.Language = Language.Cyrillic;
}
catch (OcrException ex)
{
    Console.WriteLine($"Language module could not be loaded: {ex.Message}");
    // Optionally, fall back to English or abort the process
}
```

## Krok 5: Provedení rozpoznávací operace (rozpoznat text z PNG)

Nyní, když jsou obrázek a jazyk nastaveny, můžete **recognize text from PNG**. Metoda `Recognize` spustí OCR pipeline synchronně.

```csharp
// Run OCR
ocrEngine.Recognize();
```

**Why it works:** Interně Aspose.OCR provádí předzpracování (binarizaci, odstranění šumu) před předáním obrázku do neuronové sítě optimalizované pro vybraný jazyk.

## Krok 6: Získání a zobrazení rozpoznaného textu (převod PNG na text)

Po rozpoznání je extrahovaný řetězec k dispozici přes vlastnost `Text`. Toto je poslední krok v **convert PNG to text**.

```csharp
// Get the recognized text
string recognizedText = ocrEngine.Text;

// Output the result
Console.WriteLine("=== OCR Result ===");
Console.WriteLine(recognizedText);
```

### Očekávaný výstup

Pokud `sample_image.png` obsahuje cyrilickou frázi “Привет мир”, konzole zobrazí:

```
=== OCR Result ===
Привет мир
```

Výstup může obsahovat zalomení řádků a interpunkci přesně tak, jak jsou v obrázku. V případě potřeby můžete řetězec následně zpracovat pomocí `String.Trim()`, `Regex` nebo jiných utilit pro čištění textu.

## Krok 7: Volitelné – Uložení výsledku do souboru

Uložení OCR výsledku umožňuje následné zpracování (např. indexování, překlad). Zde je rychlý způsob, jak zapsat text do souboru UTF‑8:

```csharp
File.WriteAllText(@"YOUR_DIRECTORY/ocr_output.txt", recognizedText, Encoding.UTF8);
Console.WriteLine("OCR text saved to ocr_output.txt");
```

## Běžné úskalí a jak se jim vyhnout

| Problém | Symptom | Řešení |
|---------|----------|--------|
| **Chybějící jazykový modul** | `OcrException` on `Language = Language.Cyrillic` | Zajistěte připojení k internetu při prvním spuštění nebo předem stáhněte moduly pomocí offline balíčku Aspose. |
| **Rozmazaný nebo nízkokontrastní obrázek** | Nízká přesnost, mnoho znaků “?” | Předzpracujte obrázek: zvýšte kontrast, aplikujte ostření nebo jej převěďte na odstíny šedi před předáním enginu. |
| **Velmi velký PNG** | Dlouhá doba zpracování, možná `OutOfMemoryException` | Zmenšete velikost, jak je ukázáno v Kroku 3, nebo rozdělte vícestránkový obrázek na samostatné dlaždice. |
| **Ne‑UTF‑8 znaky** | Poškozený výstup | Ověřte, že konzole nebo zapisovač souboru používá kódování UTF‑8 (`Encoding.UTF8`). |

## Kompletní, spustitelný příklad

Níže je kompletní program, který zahrnuje všechny výše uvedené kroky. Zkopírujte jej do nového konzolového projektu a spusťte po úpravě cest k souborům.

```csharp
using System;
using System.Drawing;
using System.IO;
using System.Text;
using Aspose.OCR;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1. Create OCR engine
            OcrEngine ocrEngine = new OcrEngine();

            // 2. Load PNG image (with optional down‑scaling for large files)
            string imagePath = @"YOUR_DIRECTORY/sample_image.png";
            Bitmap original = new Bitmap(imagePath);
            const int maxWidth = 1200;

            if (original.Width > maxWidth)
            {
                int newHeight = (int)(original.Height * (maxWidth / (double)original.Width));
                Bitmap resized = new Bitmap(original, new Size(maxWidth, newHeight));

                using (var ms = new MemoryStream())
                {
                    resized.Save(ms, System.Drawing.Imaging.ImageFormat.Png);
                    ocrEngine.Image = ImageStream.FromStream(ms);
                }
            }
            else
            {
                ocrEngine.Image = ImageStream.FromFile(imagePath);
            }

            // 3. Set language to Cyrillic (fallback to English if needed)
            try
            {
                ocrEngine.Language = Language.Cyrillic;
            }
            catch (OcrException ex)
            {
                Console.WriteLine($"Failed to load Cyrillic module: {ex.Message}");
                Console.WriteLine("Falling back to English.");
                ocrEngine.Language = Language.English;
            }

            // 4. Recognize text
            ocrEngine.Recognize();

            // 5. Retrieve and display the text (convert PNG to text)
            string recognizedText = ocrEngine.Text;
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(recognizedText);

            // 6. Save result to a UTF‑8 file
            string outputPath = @"YOUR_DIRECTORY/ocr_output.txt";
            File.WriteAllText(outputPath, recognizedText, Encoding.UTF8);
            Console.WriteLine($"OCR text saved to {outputPath}");
        }
    }
}
```

### Jak to funguje

1. **Vytvoření enginu** – připravuje OCR pipeline.  
2. **Načtení obrázku** – podporuje jak původní PNG, tak zmenšené verze pro výkon.  
3. **Výběr jazyka** – ukazuje **extrakci cyrilického textu** při zacházení s chybějícími moduly.  
4. **Rozpoznání** – hlavní volání **rozpoznat text z PNG**.  
5. **Zpracování výsledku** – ukazuje **převod PNG na text** a zapisuje výstup do souboru.

Program spusťte pomocí `dotnet run`. Pokud je vše správně nastaveno, uvidíte rozpoznaný text vytištěný v konzoli a uložený do `ocr_output.txt`.

## Závěr

V tomto tutoriálu jste se naučili **jak provést OCR** na PNG souborech pomocí Aspose.OCR pro .NET, od **load image for OCR** po **extract Cyrillic text** a **convert PNG to text**. Kompletní, spustitelný příklad demonstruje standardní workflow, běžné okrajové případy a praktické tipy, které udrží váš OCR pipeline spolehlivý.

**Další kroky**

* Prozkoumejte **recognize text from PNG** s dalšími jazyky (arabština, čínština) kombinací `Language` příznaků.  
* Integrovaní OCR výsledku s Azure Cognitive Search pro prohledávatelné archivní dokumenty.  
* Experimentujte s nastavením `OcrEngine` v Aspose.OCR, jako je `Resolution`.

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, abyste si mohli osvojit další funkce API a prozkoumat alternativní implementační přístupy ve svých projektech.

- [How to Download Aspose.OCR Model and Extract Text from PNG in C#](/ocr/english/net/text-recognition/how-to-download-ocr-model-and-extract-text-from-png-using-as/)
- [How to Perform OCR in C# – Recognize Cyrillic Text with Aspose](/ocr/english/net/text-recognition/how-to-perform-ocr-in-c-recognize-cyrillic-text-with-aspose/)
- [How to Batch OCR in C# – Fast Way to Extract Text PNG Files](/ocr/english/net/ocr-optimization/how-to-batch-ocr-in-c-fast-way-to-extract-text-png-files/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}