---
category: general
date: 2026-04-06
description: Extrahujte text z obrázku pomocí Aspose OCR GPU v C#. Naučte se načíst
  obrázek ze souboru a nastavit limit paměti GPU v tomto průvodci krok za krokem.
draft: false
keywords:
- extract text from image
- load image from file
- set gpu memory limit
- aspose ocr example
- aspose ocr gpu
language: cs
og_description: Extrahujte text z obrázku pomocí Aspose OCR GPU v C#. Naučte se načíst
  obrázek ze souboru a nastavit limit paměti GPU v tomto průvodci krok za krokem.
og_title: Extrahování textu z obrázku pomocí Aspose OCR GPU – Kompletní průvodce C#
tags:
- Aspose OCR
- C#
- GPU
- OCR
title: Extrahujte text z obrázku pomocí Aspose OCR GPU – Kompletní průvodce C#
url: /cs/net/ocr-configuration/extract-text-from-image-with-aspose-ocr-gpu-full-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahování textu z obrázku pomocí Aspose OCR GPU – Kompletní průvodce v C#

Už jste někdy potřebovali **extrahovat text z obrázku**, ale uvízli jste v okamžiku, kdy výkon začal hrát roli? Nejste sami — mnoho vývojářů narazí na stejnou překážku, když se OCR stane úzkým hrdlem. V tomto tutoriálu vám ukážeme, jak přesně extrahovat text z obrázku pomocí GPU runtime Aspose OCR, načíst obrázek ze souboru a dokonce nastavit limit paměti GPU pro přísnější kontrolu zdrojů.

Provedeme vás kompletním, připraveným k spuštění příkladem v C#, vysvětlíme, proč je každý řádek důležitý, a upozorníme na běžné úskalí, na která můžete narazit. Na konci budete mít pevný základ pro tvorbu rychlých, škálovatelných OCR pipeline, které běží na GPU.

## Co tento průvodce pokrývá

- **Požadavky**: .NET 6+ (nebo .NET Framework 4.6+), NuGet balíček Aspose.OCR, kompatibilní ovladač GPU.
- **Krok‑za‑krokem kód**, který načte obrázek ze souboru, nakonfiguruje GPU engine Aspose OCR a extrahuje text.
- **Proč** můžete chtít nastavit limit paměti GPU a jak to udělat bezpečně.
- **Zvládání okrajových případů**: nízké rozlišení obrázků, chybějící GPU a řešení problémů s confidence skóre.
- **Další kroky**: dávkové zpracování, integrace s ASP.NET Core a přepnutí zpět na CPU, pokud bude potřeba.

> **Tip:** Pokud si nejste jisti, zda se GPU používá, podívejte se na monitor aktivity GPU (např. NVIDIA‑SMI) během běhu OCR. Uvidíte špičku ve využití paměti, která odpovídá nastavenému limitu.

---

![Diagram zobrazující tok extrahování textu z obrázku pomocí Aspose OCR GPU enginu](extract-text-from-image-aspose-ocr-gpu.png "extrahování textu z obrázku pomocí Aspose OCR GPU")

## Krok 1: Inicializace Aspose OCR engine pro GPU zpracování

Prvním, co potřebujete, je instance `OcrEngine`, která ví, že má běžet na GPU. Aspose poskytuje čistý objekt `OcrEngineSettings`, kde můžete specifikovat runtime.

```csharp
using Aspose.OCR;
using Aspose.OCR.Runtime;
using System;
using System.Drawing;

// Create the OCR engine and tell it to use the GPU runtime
var ocrEngine = new OcrEngine(new OcrEngineSettings
{
    Runtime = OcrRuntime.Gpu   // Switches processing to the GPU
});
```

**Proč je to důležité:** Ve výchozím nastavení Aspose OCR přechází na CPU, což stačí pro malé obrázky, ale může být bolestivě pomalé pro vysoce rozlišené fotografie. Explicitním nastavením `Runtime = OcrRuntime.Gpu` přenesete těžkou práci na grafickou kartu a získáte znatelný nárůst rychlosti.

## Krok 2: (Volitelné) Nastavení limitu paměti GPU

Pokud pracujete na sdílené pracovní stanici nebo v kontejneru s omezenými GPU zdroji, můžete omezit množství paměti, kterou OCR engine spotřebuje. Tím zabráníte pádům z nedostatku paměti a udržíte ostatní procesy spokojené.

```csharp
// Limit the GPU memory usage to 1024 MB (1 GB)
ocrEngine.Settings.GpuMemoryLimit = 1024;
```

**Kdy to použít:**  
- **Multi‑tenantní prostředí**, kde několik služeb sdílí stejný GPU.  
- **CI/CD pipeline**, které přidělují pevné množství GPU paměti na úlohu.  

Pokud tuto řádku vynecháte, Aspose použije tolik paměti, kolik potřebuje, což je v pořádku na dedikované pracovní stanici.

## Krok 3: Načtení obrázku ze souboru

Nyní musíme obrázek načíst do paměti. Aspose OCR pracuje s `System.Drawing.Image`, takže použijeme `Image.FromFile`. Ujistěte se, že cesta ukazuje na skutečný soubor; jinak bude vyhozena výjimka.

```csharp
// Replace with the actual path to your high‑resolution image
string imagePath = @"YOUR_DIRECTORY/high_res_photo.png";

using (var image = Image.FromFile(imagePath))
{
    // The image is now ready for OCR processing
    // (the next step will happen inside this using block)
}
```

**Proč je načítání ze souboru důležité:** Mnoho vývojářů se snaží předat přímo pole bajtů, což funguje, ale přidává zbytečný konverzní krok. Použití `Image.FromFile` je přímočaré a `using` blok zaručuje, že souborový handle bude rychle uvolněn.

## Krok 4: Spuštění OCR a získání výsledku

S nakonfigurovaným enginem a načteným obrázkem můžeme konečně extrahovat text. Metoda `Recognize` vrací `OcrResult`, který obsahuje jak surový text, tak confidence skóre.

```csharp
using (var image = Image.FromFile(imagePath))
{
    // Perform OCR on the loaded image
    var ocrResult = ocrEngine.Recognize(image);

    // Display the confidence and the extracted text
    Console.WriteLine($"GPU OCR confidence: {ocrResult.Confidence:P2}");
    Console.WriteLine("Extracted text:");
    Console.WriteLine(ocrResult.Text);
}
```

**Porozumění výstupu:**  
- `Confidence` je hodnota mezi 0 a 1. Confidence 0,95 (nebo 95 %) obvykle znamená, že OCR je přesná.  
- `Text` obsahuje zalomení řádků tak, jak se objevují v obrázku, což je užitečné pro další zpracování.

## Krok 5: Ověření výstupu a zvládání okrajových případů

### Kontrola úrovně confidence

Pokud confidence klesne pod, řekněme, 80 %, můžete přejít zpět na CPU zpracování nebo aplikovat předzpracování obrazu (např. binarizaci).

```csharp
if (ocrResult.Confidence < 0.80)
{
    Console.WriteLine("Low confidence detected – consider preprocessing or CPU fallback.");
    // Example fallback: switch to CPU runtime temporarily
    ocrEngine.Settings.Runtime = OcrRuntime.Cpu;
    var cpuResult = ocrEngine.Recognize(image);
    Console.WriteLine($"CPU OCR confidence: {cpuResult.Confidence:P2}");
    Console.WriteLine(cpuResult.Text);
}
```

### Řešení chybějícího GPU

Ne každá mašina má kompatibilní GPU. Aspose vyhodí `OcrException`, pokud se nepodaří inicializovat GPU runtime.

```csharp
try
{
    var ocrResult = ocrEngine.Recognize(image);
    // Normal processing...
}
catch (OcrException ex) when (ex.Message.Contains("GPU"))
{
    Console.WriteLine("GPU not available – falling back to CPU.");
    ocrEngine.Settings.Runtime = OcrRuntime.Cpu;
    var cpuResult = ocrEngine.Recognize(image);
    Console.WriteLine(cpuResult.Text);
}
```

### Velké rozlišení obrázků

Velmi velké obrázky (např. > 4000 px na šířku) mohou spotřebovat hodně GPU paměti. Pokud narazíte na limit, který jste nastavili dříve, Aspose zkrátí zpracování. V takovém případě nejprve obrázek zmenšete:

```csharp
using (var original = Image.FromFile(imagePath))
{
    int maxWidth = 2000;
    var resized = new Bitmap(original, new Size(maxWidth, original.Height * maxWidth / original.Width));
    var ocrResult = ocrEngine.Recognize(resized);
    // Continue as before
}
```

## Kompletní funkční příklad

Níže je kompletní program, který můžete zkopírovat a vložit do nového konzolového projektu. Obsahuje všechny kroky, ošetření chyb a volitelnou logiku přepnutí na CPU.

```csharp
// Program.cs
using Aspose.OCR;
using Aspose.OCR.Runtime;
using System;
using System.Drawing;

class Program
{
    static void Main()
    {
        // Step 1: Initialize OCR engine to use GPU
        var ocrEngine = new OcrEngine(new OcrEngineSettings
        {
            Runtime = OcrRuntime.Gpu   // Switches processing to the GPU
        });

        // Step 2: (Optional) Limit GPU memory usage to 1 GB
        ocrEngine.Settings.GpuMemoryLimit = 1024;

        // Path to the image you want to process
        string imagePath = @"YOUR_DIRECTORY/high_res_photo.png";

        // Step 3: Load image from file
        using (var image = Image.FromFile(imagePath))
        {
            try
            {
                // Step 4: Run OCR on the image
                var ocrResult = ocrEngine.Recognize(image);

                // Step 5: Output confidence and extracted text
                Console.WriteLine($"GPU OCR confidence: {ocrResult.Confidence:P2}");
                Console.WriteLine("Extracted text:");
                Console.WriteLine(ocrResult.Text);

                // Edge‑case: low confidence handling
                if (ocrResult.Confidence < 0.80)
                {
                    Console.WriteLine("\nLow confidence detected – trying CPU fallback...");
                    ocrEngine.Settings.Runtime = OcrRuntime.Cpu;
                    var cpuResult = ocrEngine.Recognize(image);
                    Console.WriteLine($"CPU OCR confidence: {cpuResult.Confidence:P2}");
                    Console.WriteLine(cpuResult.Text);
                }
            }
            catch (OcrException ex) when (ex.Message.Contains("GPU"))
            {
                Console.WriteLine("GPU not available – falling back to CPU runtime.");
                ocrEngine.Settings.Runtime = OcrRuntime.Cpu;
                var cpuResult = ocrEngine.Recognize(image);
                Console.WriteLine($"CPU OCR confidence: {cpuResult.Confidence:P2}");
                Console.WriteLine(cpuResult.Text);
            }
        }
    }
}
```

### Očekávaný výstup

```
GPU OCR confidence: 96.45%
Extracted text:
This is the text that was
found in the high‑resolution
image you supplied.

```

Pokud confidence klesne pod nastavený práh, uvidíte další zprávy o přepnutí na CPU.

---

## Závěr

Nyní víte, **jak extrahovat text z obrázku** pomocí GPU enginu Aspose OCR, **jak načíst obrázek ze souboru** a proč můžete chtít **nastavit limit paměti GPU** pro produkční zatížení. Výše uvedený příklad je plně funkční, citovatelně hodný řešení, které můžete vložit do libovolného .NET projektu.

Co dál? Zvažte:

- **Dávkové zpracování**: procházet složku s obrázky a zapisovat výsledky do CSV.  
- **Integraci s ASP.NET Core**: vystavit API endpoint, který přijme nahraný obrázek a vrátí OCR text.  
- **Ladění výkonu**: experimentovat s různými hodnotami `GpuMemoryLimit` a sledovat využití GPU pro nalezení optimálního nastavení.

Neváhejte kód přizpůsobit vlastnímu scénáři — ať už budujete pipeline pro digitalizaci dokumentů, aplikaci pro překlad v reálném čase nebo službu pro skenování účtenek. Základy zůstávají stejné: inicializovat GPU engine, rozumně spravovat paměť a vždy ověřovat confidence.

Máte otázky nebo narazíte na problém? Zanechte komentář níže a pojďme to společně vyřešit. Šťastné kódování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}