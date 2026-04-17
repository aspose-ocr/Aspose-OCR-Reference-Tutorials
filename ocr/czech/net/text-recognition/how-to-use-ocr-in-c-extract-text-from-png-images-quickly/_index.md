---
category: general
date: 2026-03-29
description: Jak použít OCR s Aspose k extrahování textu z PNG souborů a převodu obrázků
  na text. Naučte se krok za krokem asynchronní OCR v C#.
draft: false
keywords:
- how to use OCR
- extract text from png
- convert images to text
- extract text from images
language: cs
og_description: Jak použít OCR s Aspose v C# k extrakci textu z PNG souborů. Tento
  průvodce vás provede asynchronním OCR, kódem a tipy.
og_title: Jak používat OCR v C# – Extrahujte text z PNG obrázků
tags:
- OCR
- C#
- Aspose
title: Jak použít OCR v C# – Rychle extrahovat text z PNG obrázků
url: /cs/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-png-images-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak použít OCR v C# – Rychle extrahovat text z PNG obrázků

Už jste se někdy zamysleli **jak použít OCR** k získání textu z několika PNG snímků? Možná máte naskenované účtenky, faktury nebo UI mock‑upy a potřebujete ten text v prohledávatelném formátu. Dobrá zpráva? S Aspose.OCR můžete převést obrázky na text během několika řádků asynchronního C# kódu.  

V tomto tutoriálu vám ukážeme přesně, jak extrahovat text z PNG souborů, vysvětlíme, proč je každý krok důležitý, a poskytneme vám připravený program, který vytiskne rozpoznaný text pro každou stránku. Na konci budete schopni **extrahovat text z obrázků** bez zbytečného procházení dokumentace.

## Co se naučíte

- Nainstalujte a odkažte na NuGet balíček Aspose.OCR.  
- Inicializujte OCR engine a nastavte jazyk (v tomto příkladu angličtina).  
- Předávejte pole PNG souborů metodě `RecognizeImagesAsync` pro rychlé, neblokující zpracování.  
- Procházejte objekty `OcrResult` a vypište extrahované řetězce.  

Žádné externí služby, žádné komplikované callbacky — jen čistý, asynchronní C#, který funguje na .NET 6+.

---

## Požadavky

| Požadavek | Důvod |
|-------------|--------|
| .NET 6 SDK (or later) | Moderní jazykové funkce jako `async Main`. |
| Visual Studio 2022 or VS Code | IDE pro kompilaci a spuštění kódu. |
| Aspose.OCR NuGet package (`Aspose.OCR`) | Poskytuje třídu `OcrEngine` použitou ve vzorku. |
| A few PNG images (`page1.png`, `page2.png`, …) | Vstupní soubory pro OCR proces. |

Pokud již máte .NET projekt, stačí spustit `dotnet add package Aspose.OCR`. Jinak vytvořte novou konzolovou aplikaci pomocí `dotnet new console -n OcrDemo`.

---

## Krok 1: Nainstalujte Aspose.OCR a nastavte projekt

Nejprve přidejte OCR knihovnu do svého projektu:

```bash
dotnet add package Aspose.OCR
```

Proč je to důležité: Aspose.OCR obsahuje nativní OCR engine, jazykové balíčky a jednoduché API. Stažením přes NuGet zajistíte kompatibilitu verzí a automatické aktualizace.

---

## Krok 2: Inicializujte OCR engine a vyberte jazyk

Engine potřebuje vědět, jaký jazyk má hledat. Angličtina je nejčastější, ale můžete použít `Language.Spanish`, `Language.French` a další.

```csharp
using Aspose.OCR;

// ...

// Step 2: Create the engine and set the language to English
var ocrEngine = new OcrEngine
{
    Language = Language.English   // Change this if you need a different language
};
```

> **Tip:** Vždy nastavte jazyk explicitně; ponechání výchozího nastavení může snížit přesnost a prodloužit dobu zpracování.

---

## Krok 3: Připravte seznam PNG souborů

Můžete předat jeden soubor nebo pole. Poskytnutí pole umožní engine zpracovat je dávkově asynchronně, což je ideální pro několik stránek.

```csharp
// Step 3: Define the image files you want to process
string[] imagePaths = { "page1.png", "page2.png", "page3.png" };
```

Pokud jsou vaše obrázky v podsložce, stačí předřadit relativní cestu (`"images/page1.png"`). Engine vyhodí jasnou `FileNotFoundException`, pokud je cesta špatná — proto zkontrolujte názvy souborů.

---

## Krok 4: Spusťte asynchronní OCR na všech obrázcích

Metoda `RecognizeImagesAsync` vrací pole `OcrResult`. Protože je asynchronní, vaše UI (nebo konzole) zůstává responzivní, zatímco OCR běží na pozadí.

```csharp
// Step 4: Perform async OCR on every image
OcrResult[] ocrResults = await ocrEngine.RecognizeImagesAsync(imagePaths);
```

**Proč async?**  
Pokud integrujete OCR do webového API nebo desktopové aplikace, nechcete, aby vlákno blokovalo během skenování každého pixelu. `await` uvolní vlákno zpět do thread poolu, čímž zvyšuje škálovatelnost.

---

## Krok 5: Zobrazte extrahovaný text pro každou stránku

Nyní, když máme výsledky, projděte je a vytiskněte rozpoznaný text. Vlastnost `Text` obsahuje výstup v prostém textu, připravený pro další zpracování (např. uložení do databáze).

```csharp
// Step 5: Output the recognized text for every page
for (int i = 0; i < ocrResults.Length; i++)
{
    Console.WriteLine($"--- Page {i + 1} ---");
    Console.WriteLine(ocrResults[i].Text);
}
```

### Očekávaný výstup

Předpokládejme, že `page1.png` obsahuje „Invoice #12345“ a `page2.png` obsahuje „Total: $89.99“, uvidíte něco jako:

```
--- Page 1 ---
Invoice #12345
Date: 03/28/2026
--- Page 2 ---
Total: $89.99
Paid by: Credit Card
```

Pokud OCR neobjeví žádný text, vlastnost `Text` bude prázdný řetězec — v produkčním kódu tuto situaci ošetřete kontrolou `string.IsNullOrWhiteSpace`.

---

## Kompletní funkční příklad

Níže je kompletní program, který můžete zkopírovat a vložit do `Program.cs`. Obsahuje všechny using direktivy, asynchronní `Main` a komentáře, které objasňují každý krok.

```csharp
using System;
using System.Threading.Tasks;
using Aspose.OCR;

class Program
{
    // Async Main is supported from C# 7.1 onward
    static async Task Main()
    {
        // Step 1: Initialize the OCR engine and set the language to English
        var ocrEngine = new OcrEngine { Language = Language.English };

        // Step 2: Define the image files to be processed
        string[] imagePaths = { "page1.png", "page2.png", "page3.png" };

        // Step 3: Perform asynchronous OCR on all images
        OcrResult[] ocrResults = await ocrEngine.RecognizeImagesAsync(imagePaths);

        // Step 4: Output the recognized text for each page
        for (int i = 0; i < ocrResults.Length; i++)
        {
            Console.WriteLine($"--- Page {i + 1} ---");
            Console.WriteLine(ocrResults[i].Text);
        }
    }
}
```

Uložte soubor, umístěte PNG soubory vedle spustitelného souboru (nebo upravte cesty) a spusťte:

```bash
dotnet run
```

Měli byste vidět extrahovaný text vytištěný v konzoli, což potvrzuje, že jste úspěšně **převáděli obrázky na text**.

---

## Řešení běžných okrajových případů

| Situace | Co dělat |
|-----------|------------|
| **Low‑resolution PNG** | Zvyšte `ocrEngine.ImageProcessingOptions.Dpi` před rozpoznáním. |
| **Multiple languages** | Nastavte `ocrEngine.Language = Language.English | Language.Spanish;` (bitové OR). |
| **Large batch (hundreds of files)** | Zpracovávejte po částech (např. 20 souborů na volání `RecognizeImagesAsync`) aby nedošlo k nárůstu paměti. |
| **Need the confidence score** | Použijte `ocrResults[i].Confidence` (float mezi 0 a 1) k filtrování výsledků nízké kvality. |

Tyto úpravy udržují váš OCR pipeline robustní, zejména při přechodu z demo verze do produkce.

---

## Bonus: Ukládání výsledků do textového souboru

Pokud dáváte přednost trvalé kopii místo výstupu do konzole, přidejte malý pomocník:

```csharp
using System.IO;

// After the for‑loop:
File.WriteAllLines("OcrOutput.txt", ocrResults.Select(r => r.Text));
Console.WriteLine("All pages saved to OcrOutput.txt");
```

Nyní máte jeden soubor, který **extrahuje text z obrázků** pro následné zpracování — ideální pro indexování, vyhledávání nebo předání jazykovému modelu.

---

## Závěr

Prošli jsme **jak použít OCR** v C# s Aspose k **extrahování textu z PNG** souborů a **převodu obrázků na text** efektivně. Asynchronní přístup zajišťuje, že vaše aplikace zůstane responzivní, zatímco jednoduché API udržuje kód čitelný a udržovatelný.

Vyzkoušejte to s vlastními dokumenty, experimentujte s různými jazyky a možná i propojte výstup s vyhledávacím indexem nebo službou pro shrnutí. Možnosti jsou neomezené, když můžete spolehlivě převést obrázky na prohledávatelné řetězce.

---

### Další kroky a související témata

- **Extrahujte text z obrázků** v jiných formátech (JPEG, TIFF) — stačí změnit příponu souboru.  
- **Dávkové zpracování pomocí Parallel.ForEach** pro masivní úlohy.  
- **Post‑OCR čištění** pomocí regulárních výrazů pro normalizaci dat, částek nebo ID.  
- **Integrace s Azure Cognitive Services** pokud potřebujete cloudové OCR s dalšími funkcemi.  

Neváhejte zanechat komentář, pokud narazíte na problémy, nebo se podělit, jak jste rozšířili tento základní postup. Šťastné programování!   (Image: ![OCR result screenshot showing extracted text](/images/ocr-result.png){.align-center alt="příklad výstupu OCR"} )

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}