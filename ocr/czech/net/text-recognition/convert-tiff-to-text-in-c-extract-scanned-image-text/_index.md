---
category: general
date: 2026-03-05
description: Převod TIFF na text v C# pomocí Aspose OCR – rychle extrahujte text ze
  skenovaných obrázkových souborů a naučte se, jak načíst obrázkový soubor v C# pro
  OCR zpracování.
draft: false
keywords:
- convert TIFF to text
- extract text scanned image
- load image file C#
language: cs
og_description: Převod TIFF na text v C# pomocí Aspose OCR. Naučte se kompletní workflow
  pro extrakci textu ze skenovaných obrázků a efektivní načítání souborů obrázků.
og_title: Převod TIFF na text v C# – Extrahování textu ze skenovaného obrázku
tags:
- OCR
- C#
- Aspose
title: Převod TIFF na text v C# – Extrahování textu ze skenovaného obrázku
url: /cs/net/text-recognition/convert-tiff-to-text-in-c-extract-scanned-image-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Převod TIFF na text v C# – Extrahování textu ze skenovaného obrázku

Potřebujete **převést TIFF na text v C#**? Nejste jediní, kdo bojuje s vícestránkovými skenovanými obrázky, které se neústupně odmítají stát vyhledávatelnými řetězci.  
V tomto průvodci projdeme kompletní, připravené řešení, které vezme soubor TIFF, předá jej Aspose OCR a vrátí čistý text – bez dalších služeb, bez skryté magie.

> **Pro tip:** Pokud pracujete s vysoce rozlišenými skeny, povolení GPU zpracování může ušetřit sekundy u každé stránky.

Ukážeme vám také, jak **extrahovat text ze skenovaných obrázků** a nejlepší způsob, jak **načíst soubor obrázku v C#** do OCR enginu, abyste tuto logiku mohli dnes vložit do jakéhokoli .NET projektu.

---

## Co budete potřebovat

Předtím, než se ponoříme, ujistěte se, že máte na svém počítači následující:

| Požadavek | Důvod |
|-------------|--------|
| .NET 6.0+ (nebo .NET Framework 4.7.2+) | Moderní runtime, podporuje `Span<T>` a async I/O |
| Aspose.OCR pro .NET (NuGet balíček `Aspose.OCR`) | OCR engine, který použijeme |
| Platný licenční soubor Aspose OCR (`Aspose.OCR.lic`) | Bez něj narazíte na omezení zkušební verze |
| Soubor TIFF (jednostránkový nebo vícestránkový) pro testování | Použitý příklad: `scanned_multi_page.tif` |
| GPU s CUDA 11+ (volitelné) | Zrychluje rozpoznávání, když `EngineMode = Gpu` |

Pokud vám něco chybí, stáhněte si nyní NuGet balíček:

```bash
dotnet add package Aspose.OCR
```

---

## Krok 1: Nastavení projektu a importování jmenných prostorů

Vytvořte novou konzolovou aplikaci (nebo přidejte kód do existujícího projektu). První věc, kterou uděláme, je importovat třídy, které budeme potřebovat.

```csharp
using System;
using Aspose.OCR;          // Core OCR classes
using Aspose.OCR.Image;   // ImageStream helper
```

> **Proč je to důležité:** Importování `Aspose.OCR.Image` nám poskytuje továrnu `ImageStream`, která může číst soubory TIFF přímo z disku nebo ze streamu. Přeskočení tohoto kroku způsobí chybu při kompilaci.

---

## Krok 2: Inicializace OCR enginu a výběr režimu zpracování

OCR engine musí být nakonfigurován **před** přiřazením jakéhokoli obrázku. Zde rozhodujeme, zda běžet na CPU nebo využít GPU.

```csharp
// Step 2: Initialize the OCR engine and enable GPU processing (must be set before any OCR work)
OcrEngine ocrEngine = new OcrEngine();

// Choose the processing mode that fits your environment.
// Options: Cpu (default) | Gpu | Auto
ocrEngine.EngineMode = OcrEngineMode.Gpu;   // Switch to Cpu if you don’t have a compatible GPU
```

*Pokud běžíte na serveru bez grafické karty, změňte `Gpu` na `Cpu` nebo `Auto`.*  
Režim enginu ovlivňuje alokaci paměti a rychlost; GPU režim může být 2‑3× rychlejší u velkých, vysoce rozlišených TIFF souborů.

---

## Krok 3: Použití vaší Aspose OCR licence

Spuštění bez licence vás omezuje na několik stránek a vodoznaky. Načtěte licenci co nejdříve, aby každá následující operace byla neomezená.

```csharp
// Step 3: Apply the Aspose OCR license (replace with your own license file if needed)
ocrEngine.SetLicense("Aspose.OCR.lic");
```

> **Častá chyba:** Umístění `SetLicense` po `Recognize()` způsobí, že engine přejde do zkušebního režimu pro toto volání.

---

## Krok 4: Načtení TIFF souboru – zpracování jedno- a vícestránkových obrázků

Aspose OCR dokáže číst vícestránkové TIFF soubory přímo, ale musíte předat správný stream. Zde je robustní vzor, který funguje pro oba scénáře.

```csharp
// Step 4: Load the image to be recognized
string tiffPath = @"YOUR_DIRECTORY\scanned_multi_page.tif";

using (var imageStream = ImageStream.FromFile(tiffPath))
{
    // Step 5: Assign the image to the engine
    ocrEngine.Image = imageStream;

    // Step 6: Perform the OCR operation
    OcrResult ocrResult = ocrEngine.Recognize();

    // Step 7: Output the recognized text
    Console.WriteLine("=== OCR Output ===");
    Console.WriteLine(ocrResult.Text);
}
```

### Proč použít `ImageStream.FromFile`?

- Abstrahuje podkladový `FileStream`, interně zpracovává enumeraci stránek TIFF.  
- Funguje také s `MemoryStream`, takže můžete načítat obrázky z databáze nebo webového API, aniž byste se dotýkali souborového systému.

### Okrajový případ: Velmi velké TIFF soubory

Pokud váš TIFF překročí 200 MB, zvažte načítání po stránkách, abyste se vyhnuli výjimkám nedostatku paměti:

```csharp
int pageCount = ImageInfo.GetPageCount(tiffPath);
for (int i = 0; i < pageCount; i++)
{
    using var pageStream = ImageStream.FromFile(tiffPath, i);
    ocrEngine.Image = pageStream;
    var pageResult = ocrEngine.Recognize();
    Console.WriteLine($"--- Page {i + 1} ---");
    Console.WriteLine(pageResult.Text);
}
```

---

## Krok 5: Ověření výstupu

Po spuštění programu byste měli vidět něco jako:

```
=== OCR Output ===
Invoice #12345
Date: 2024‑12‑01
Total: $1,250.00
Thank you for your business!
```

Pokud text vypadá poškozeně, zkontrolujte:

1. **Rozlišení** – OCR funguje nejlépe při 300 dpi nebo vyšším.  
2. **EngineMode** – Přepněte na `Cpu`, pokud je ovladač GPU zastaralý.  
3. **Licence** – Ujistěte se, že cesta k licenčnímu souboru je správná a soubor je čitelný.

---

## Často kladené otázky (FAQ)

### Funguje to i s jinými formáty obrázků?

Ano. `ImageStream.FromFile` podporuje JPEG, PNG, BMP a dokonce i PDF (prostřednictvím Aspose.PDF). Stačí změnit příponu souboru.

### Co když potřebuji zpracovávat obrázky uložené v databázi?

Načtěte BLOB do `MemoryStream` a předávejte jej `ImageStream.FromStream(memoryStream)`. OCR engine s ním zachází stejně jako se souborovým streamem.

### Můžu to spustit na Linuxu?

Ano—Aspose OCR je multiplatformní. Nainstalujte vhodný .NET runtime a ujistěte se, že jsou k dispozici potřebné nativní knihovny pro GPU (pokud jsou používány).

---

## Kompletní funkční příklad (připravený ke kopírování)

Níže je celý program, připravený ke kompilaci. Nahraďte `YOUR_DIRECTORY` a cestu k licenčnímu souboru vašimi skutečnými umístěními.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Image;

namespace TiffToTextDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Initialize OCR engine
            OcrEngine ocrEngine = new OcrEngine();

            // Choose processing mode: Gpu, Cpu, or Auto
            ocrEngine.EngineMode = OcrEngineMode.Gpu; // Change to Cpu if no GPU

            // Apply license (skip if you only need a trial)
            ocrEngine.SetLicense("Aspose.OCR.lic");

            // Path to the TIFF file
            string tiffPath = @"YOUR_DIRECTORY\scanned_multi_page.tif";

            // Load the TIFF (handles multi‑page automatically)
            using (var imageStream = ImageStream.FromFile(tiffPath))
            {
                // Assign image to engine
                ocrEngine.Image = imageStream;

                // Run OCR
                OcrResult result = ocrEngine.Recognize();

                // Display result
                Console.WriteLine("=== OCR Output ===");
                Console.WriteLine(result.Text);
            }

            // Optional: Process each page individually for huge files
            // int pages = ImageInfo.GetPageCount(tiffPath);
            // for (int i = 0; i < pages; i++) { ... }
        }
    }
}
```

Uložte to jako `Program.cs`, spusťte `dotnet run` a sledujte text

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}