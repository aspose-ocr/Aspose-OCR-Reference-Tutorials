---
category: general
date: 2026-02-11
description: Naučte se, jak provádět OCR na vícestránkovém TIFFu v C# pomocí Aspose
  OCR. Převádějte TIFF na text, extrahujte text z TIFFu a rychle rozpoznávejte text
  z obrázku.
draft: false
keywords:
- how to run OCR
- recognize text from image
- convert tiff to text
- extract text from tiff
- perform OCR on image
language: cs
og_description: Jak spustit OCR na vícestránkovém TIFF pomocí Aspose OCR v C#. Krok
  za krokem průvodce převodem TIFF na text, extrakcí textu z TIFF a rozpoznáním textu
  z obrázku.
og_title: Jak spustit OCR na vícestránkových TIFF obrázcích – Kompletní C# tutoriál
tags:
- OCR
- C#
- Aspose
- TIFF
title: Jak spustit OCR na vícestránkových TIFF obrázcích s Aspose OCR – průvodce pro
  C#
url: /cs/net/text-recognition/how-to-run-ocr-on-multi-page-tiff-images-with-aspose-ocr-c-g/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak spustit OCR na vícestránkových TIFF obrázcích s Aspose OCR

Už jste se někdy zamysleli **jak spustit OCR** na naskenovaném TIFFu, který obsahuje několik stránek? Nejste sami – mnoho vývojářů narazí na tento problém, když potřebují získat prohledávatelný text ze starých dokumentů. Dobrá zpráva? S Aspose OCR můžete rozpoznat text z obrazových souborů během několika řádků C# kódu a získáte prostý spojený text připravený k indexaci nebo dalšímu zpracování.

V tomto tutoriálu projdeme celým pracovním postupem: od instalace balíčku Aspose OCR, načtení vícestránkového TIFFu, po převod TIFF na text a nakonec zobrazení extrahovaného obsahu. Na konci budete schopni **extrahovat text z TIFF** souborů, **rozpoznat text z obrázku** a dokonce automatizovat proces pro desítky souborů v dávkovém úkolu. Žádná magie, jen jasné, praktické kroky.

## Co se naučíte

- Jak nastavit Aspose OCR engine pro rozpoznávání anglického jazyka.  
- Přesný kód potřebný k **převodu TIFF na text** pomocí třídy `OcrEngine`.  
- Tipy pro práci s vícestránkovými obrázky a zajištění správného oddělení jednotlivých stránek.  
- Běžné úskalí (např. chybějící nativní závislosti) a jak se jim vyhnout.  

**Požadavky** – budete potřebovat .NET 6 nebo novější, Visual Studio (nebo jakýkoli C# editor) a internetové připojení pro funkci automatického stahování zdrojů. To je vše; žádné další nativní knihovny, se kterými byste se museli potýkat.

---

## Krok 1 – Instalace NuGet balíčku Aspose OCR

Než budete moci **provádět OCR na obrázku** souborech, musíte přidat knihovnu do svého projektu.

```bash
dotnet add package Aspose.OCR
```

> **Tip:** Pokud pracujete ve Visual Studio, můžete také kliknout pravým tlačítkem na projekt → *Manage NuGet Packages* → vyhledat “Aspose.OCR” a kliknout *Install*.

Balíček obsahuje vše, co potřebujete, a s `AutomaticResourceDownload = true` engine automaticky stáhne jazykové balíčky za běhu.

---

## Krok 2 – Inicializace OCR Engine (Jak spustit OCR)

Nyní, když je balíček na místě, vytvoříme a nakonfigurujeme instanci `OcrEngine`. To je jádro **jak spustit OCR** v našem scénáři.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System.Drawing;   // For Image class
using System;

// Step 2: Create and configure the OCR engine
var ocrEngine = new OcrEngine
{
    Language = OcrLanguage.English,          // Recognize English text
    AutomaticResourceDownload = true,        // Auto‑download language data
    OutputFormat = OcrOutputFormat.Text      // Get plain concatenated text
};
```

**Proč je to důležité:** Nastavení `Language` říká engine, jakou znakovou sadu očekávat, zatímco `AutomaticResourceDownload` vás ušetří ručního umisťování jazykových souborů na server. `OutputFormat` nastavený na `Text` nám poskytuje jednoduchý řetězec – ideální pro **převod TIFF na text** pipeline.

---

## Krok 3 – Načtení vícestránkového TIFF (Rozpoznání textu z obrázku)

TIFF může obsahovat mnoho snímků, z nichž každý představuje stránku. Třída `System.Drawing.Image` to pro nás abstrahuje.

```csharp
// Step 3: Load the multi‑page image to be processed
using (var image = Image.FromFile("YOUR_DIRECTORY/multi_page.tiff"))
{
    // Step 4: Run OCR on the image
    var ocrResult = ocrEngine.Recognize(image);

    // Step 5: Display the extracted text
    Console.WriteLine(ocrResult.Text);
}
```

> **Co když soubor není ve stejném adresáři?** Stačí zadat úplnou absolutní cestu nebo použít `Path.Combine` s `AppContext.BaseDirectory`.  
> **Co s využitím paměti?** Příkaz `using` uvolní obrázek po zpracování, čímž zabrání únikům – což je klíčové při dávkovém zpracování desítek velkých TIFFů.

Volání `Recognize` automaticky prochází každou stránku v TIFFu a spojuje výsledky s konci řádků. Proto uvidíte každou stránku oddělenou, když vytisknete `ocrResult.Text`.

---

## Krok 4 – Kompletní funkční příklad (Všechny kroky v jednom souboru)

Níže je kompletní, připravená ke spuštění konzolová aplikace. Zkopírujte a vložte ji do nového .NET konzolového projektu a stiskněte **F5**.

```csharp
// File: Program.cs
using System;
using System.Drawing;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace TiffOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Configure the OCR engine
            var ocrEngine = new OcrEngine
            {
                Language = OcrLanguage.English,
                AutomaticResourceDownload = true,
                OutputFormat = OcrOutputFormat.Text
            };

            // 2️⃣ Load your multi‑page TIFF (replace with your actual path)
            const string tiffPath = @"YOUR_DIRECTORY\multi_page.tiff";

            if (!System.IO.File.Exists(tiffPath))
            {
                Console.WriteLine($"File not found: {tiffPath}");
                return;
            }

            // 3️⃣ Perform OCR
            using (var image = Image.FromFile(tiffPath))
            {
                var result = ocrEngine.Recognize(image);

                // 4️⃣ Output the extracted text
                Console.WriteLine("=== OCR RESULT ===");
                Console.WriteLine(result.Text);
                Console.WriteLine("==================");
            }

            // Keep console open
            Console.WriteLine("Press any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**Očekávaný výstup** (zkrácený pro stručnost):

```
=== OCR RESULT ===
Page 1: The quick brown fox jumps over the lazy dog.
Page 2: Lorem ipsum dolor sit amet, consectetur adipiscing elit.
...
==================
Press any key to exit...
```

Každá stránka se zobrazí na vlastním řádku, protože `OcrOutputFormat.Text` vloží zalomení řádku mezi snímky. Pokud potřebujete jiný oddělovač, můžete po‑zpracovat `result.Text` pomocí `String.Replace`.

---

## Krok 5 – Řešení běžných okrajových případů

### 5.1 Velké TIFF soubory  
Při práci s TIFFy o velikosti gigabajtů může být načtení celého souboru do paměti problematické. Řešením je zpracovat každý snímek jednotlivě:

```csharp
using (var image = Image.FromFile(tiffPath))
{
    for (int i = 0; i < image.GetFrameCount(FrameDimension.Page); i++)
    {
        image.SelectActiveFrame(FrameDimension.Page, i);
        var pageResult = ocrEngine.Recognize(image);
        Console.WriteLine($"--- Page {i + 1} ---");
        Console.WriteLine(pageResult.Text);
    }
}
```

### 5. Není‑anglické dokumenty  
Pokud potřebujete **rozpoznat text z obrázku** ve španělštině nebo francouzštině, stačí změnit vlastnost `Language`:

```csharp
ocrEngine.Language = OcrLanguage.Spanish; // or OcrLanguage.French
```

Aspose automaticky stáhne odpovídající jazykové zdroje.

### 5. Ukládání výstupu  
Často budete chtít **převést TIFF na text** a uložit výsledek do souboru `.txt`:

```csharp
System.IO.File.WriteAllText("output.txt", ocrResult.Text);
```

Můžete také rozdělit výstup po stránkách pomocí `String.Split(Environment.NewLine)` a zapsat každý úsek do samostatného souboru.

---

## Pro tipy a úskalí

- **AutomaticResourceDownload** funguje při prvním spuštění aplikace; následná spuštění jsou offline.  
- Pokud vidíte poškozené znaky, zkontrolujte nastavení `Language`; nesprávné jazykové balíčky způsobují špatné rozpoznání.  
- Pro PDF, které byly rasterizovány do TIFFů, můžete zvýšit `ocrEngine.Dpi` (výchozí je 300) pro lepší přesnost.  
- Vždy obalte `Image.FromFile` do bloku `using`; jinak soubor uzamknete a nebudete jej moci později smazat nebo přesunout.

---

## Často kladené otázky

**Q: Funguje to i s jednostránkovými TIFFy?**  
A: Naprosto. Engine zachází s jednosnímkovým TIFFem stejně; získáte jen jeden řádek textu.

**Q: Mohu zpracovávat soubory PNG nebo JPEG stejným způsobem?**  
A: Ano – stačí změnit příponu souboru. Metoda `Recognize` přijímá jakýkoli formát `System.Drawing.Image`.

**Q: Co když potřebuji výsledek OCR jako PDF místo prostého textu?**  
A: Nastavte `OutputFormat = OcrOutputFormat.Pdf` a `ocrResult` bude obsahovat PDF pole bajtů, které můžete zapsat na disk.

---

## Závěr

Nyní máte kompletní, end‑to‑end řešení pro **jak spustit OCR** na vícestránkových TIFF souborech pomocí Aspose OCR v C#. Nakonfigurováním engine, načtením obrázku a voláním `Recognize` můžete **extrahovat text z TIFF**, **převést TIFF na text** a **rozpoznat text z obrázku** během několika řádků kódu. Klidně upravte jazyk, výstupní formát nebo zpracování snímek po snímku podle vašich potřeb dávkového zpracování.

Připraveni na další krok? Zkuste kombinovat tento přístup s folder‑watcher službou, která automaticky **provádí OCR na obrázku** souborech, jakmile se objeví ve složce, nebo integrujte výstup do vyhledávacího indexu pro okamžité full‑textové vyhledávání. Možnosti jsou neomezené a kód, který jste právě viděli, je solidní základ.

Pokud narazíte na nějaké problémy, zanechte komentář níže nebo mě kontaktujte na GitHubu. Šťastné programování a užívejte si převod těch neústupných TIFFů na prohledávatelný text!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}