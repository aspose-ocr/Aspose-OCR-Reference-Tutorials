---
category: general
date: 2026-04-08
description: Naučte se rozpoznávat čínský text z JPG obrázků pomocí Aspose OCR. Tento
  krok‑za‑krokem průvodce vám také ukáže, jak rychle extrahovat text z obrázku.
draft: false
keywords:
- recognize chinese text
- extract text from image
- recognize text from jpg
- Aspose OCR C#
- offline OCR resources
language: cs
og_description: Rozpoznávejte čínský text z JPG obrázků pomocí Aspose OCR. Postupujte
  podle tohoto kompletního návodu k offline extrakci textu z obrázku.
og_title: rozpoznat čínský text z JPG pomocí Aspose OCR
tags:
- OCR
- C#
- Aspose
title: Rozpoznat čínský text z JPG pomocí Aspose OCR
url: /cs/net/text-recognition/recognize-chinese-text-from-jpg-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# rozpoznat čínský text z JPG pomocí Aspose OCR

Už jste někdy potřebovali **recognize chinese text** z JPG souboru, ale nebyli jste si jisti, kde začít? Nejste v tom sami — mnoho vývojářů narazí na tento problém při tvorbě vícejazykových skenovacích aplikací. Dobrou zprávou je, že Aspose OCR to dělá hračkou, i když musíte pracovat offline.

V tomto tutoriálu projdeme celý proces extrahování textu z obrázku, ve stylu **extract text from image**, a ukážeme vám přesně, jak **recognize text from jpg** pomocí C#. Na konci budete mít spustitelný program, který načte čínsky‑jazykový obrázek a vypíše rozpoznané znaky do konzole.

## Co budete potřebovat

- .NET 6.0 nebo novější (jakákoli recentní verze funguje)
- NuGet balíček Aspose.OCR (`Install-Package Aspose.OCR`)
- Soubor zdrojů pro čínský jazyk (v tutoriálu je ukázáno, jak jej načíst offline)
- Soubor obrázku pojmenovaný `chinese_sample.jpg` umístěný ve složce, kterou ovládáte

Není potřeba žádné složité triky v IDE — Visual Studio, Rider nebo dokonce VS Code postačí.

## Krok 1: Nastavení projektu a instalace Aspose OCR

Nejprve vytvořte nový konzolový projekt a přidejte knihovnu Aspose OCR.

```bash
dotnet new console -n ChineseOcrDemo
cd ChineseOcrDemo
dotnet add package Aspose.OCR
```

> **Tip:** Pokud jste za firemním proxy, přidejte příznak `--no-cache`, aby se vynutilo stažení čerstvé verze.

## Krok 2: Zakázat automatické stahování zdrojů

Aspose OCR může načítat jazykové balíčky za běhu, ale pro produkci obvykle chcete soubory distribuovat spolu s aplikací. Zakázání automatického stahování zabraňuje nečekaným síťovým voláním.

```csharp
using Aspose.Ocr;

// Create the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Turn off the auto‑download feature
ocrEngine.Options.EnableAutomaticResourceDownload = false;
```

Proč to děláme? Udržení zdrojů lokálně zaručuje konzistentní výkon a umožňuje spustit aplikaci na strojích bez přístupu k internetu.

## Krok 3: Načtení čínských jazykových zdrojů offline

Aspose poskytuje jazyková data jako samostatné soubory. Předpokládejme, že jste čínský balíček (`zh`) umístili do složky `Resources` vedle spustitelného souboru, načtěte jej takto:

```csharp
// Path to the folder that contains the language files
string resourcePath = Path.Combine(AppContext.BaseDirectory, "Resources");

// Tell the engine where to look for resources
ocrEngine.Options.ResourcesFolder = resourcePath;

// Load the Simplified Chinese resources (offline = true)
ocrEngine.LoadLanguageResources("zh", offline: true);
```

> **Pozor:** Pokud je cesta špatná, získáte `FileNotFoundException`. Zkontrolujte název složky a citlivost na velikost písmen na Linuxu.

## Krok 4: Nastavení jazyka enginu na čínštinu

Nyní, když jsou data načtena, nasměrujte engine na správný jazykový kód.

```csharp
ocrEngine.Language = "zh"; // “zh” = Simplified Chinese
```

Explicitní nastavení jazyka zvyšuje přesnost, protože OCR nebude ztrácet cykly hádáním skriptů.

## Krok 5: Rozpoznání textu z JPG obrázku

Zde je jádro tutoriálu — předání JPG enginu a získání textu.

```csharp
// Full path to the image you want to process
string imagePath = Path.Combine(AppContext.BaseDirectory, "chinese_sample.jpg");

// Run the OCR operation
OcrResult ocrResult = ocrEngine.RecognizeImage(imagePath);

// Output the raw result
Console.WriteLine("=== Recognized Chinese Text ===");
Console.WriteLine(ocrResult.Text);
```

Pokud vše proběhne hladce, konzole zobrazí čínské znaky, které byly v `chinese_sample.jpg`. Můžete také získat `ocrResult.Confidence` jako metrickou hodnotu kvality.

## Krok 6: Kompletní funkční příklad

Sestavením všech částí získáte připravený spustitelný program. Uložte jej jako `Program.cs` ve složce vašeho projektu.

```csharp
using System;
using System.IO;
using Aspose.Ocr;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Initialize OCR engine
        // -------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine();

        // -------------------------------------------------
        // 2️⃣ Disable automatic resource download
        // -------------------------------------------------
        ocrEngine.Options.EnableAutomaticResourceDownload = false;

        // -------------------------------------------------
        // 3️⃣ Load Chinese language resources (offline)
        // -------------------------------------------------
        string resourcePath = Path.Combine(AppContext.BaseDirectory, "Resources");
        ocrEngine.Options.ResourcesFolder = resourcePath;
        ocrEngine.LoadLanguageResources("zh", offline: true);

        // -------------------------------------------------
        // 4️⃣ Set language to Simplified Chinese
        // -------------------------------------------------
        ocrEngine.Language = "zh";

        // -------------------------------------------------
        // 5️⃣ Recognize text from a JPG image
        // -------------------------------------------------
        string imagePath = Path.Combine(AppContext.BaseDirectory, "chinese_sample.jpg");
        OcrResult ocrResult = ocrEngine.RecognizeImage(imagePath);

        // -------------------------------------------------
        // 6️⃣ Show the result
        // -------------------------------------------------
        Console.WriteLine("=== Recognized Chinese Text ===");
        Console.WriteLine(ocrResult.Text);
        Console.WriteLine($"\nConfidence: {ocrResult.Confidence:P2}");
    }
}
```

### Očekávaný výstup

```
=== Recognized Chinese Text ===
欢迎使用Aspose OCR示例
Confidence: 96.45%
```

Přesný výstup se bude lišit podle zdrojového obrázku, ale měli byste vidět blok čínských znaků následovaný procentem důvěry.

## Krok 7: Běžné varianty a okrajové případy

### Rozpoznání textu z PNG nebo BMP

Metoda `RecognizeImage` přijímá libovolný formát podporovaný .NET `System.Drawing`. Stačí změnit příponu souboru:

```csharp
ocrEngine.RecognizeImage("sample.png");
```

### Zpracování více jazyků

Pokud potřebujete **extract text from image**, který kombinuje angličtinu a čínštinu, načtěte oba jazykové balíčky a nastavte `ocrEngine.Language = "zh,en";`. Engine automaticky přepíná mezi skripty.

### Práce s nízkým rozlišením obrázků

Nízké DPI může zničit přesnost OCR. Před voláním `RecognizeImage` můžete obrázek zvětšit:

```csharp
using System.Drawing;

Bitmap bmp = new Bitmap(imagePath);
Bitmap highRes = new Bitmap(bmp, new Size(bmp.Width * 2, bmp.Height * 2));
highRes.Save("highres.jpg");
ocrResult = ocrEngine.RecognizeImage("highres.jpg");
```

Pamatujte, že zvětšení nepřidá magicky detail, ale může algoritmu poskytnout více pixelů ke zpracování.

## Krok 8: Testování a ověření

Rychlá kontrola je porovnat výstup OCR s známým referenčním řetězcem.

```csharp
string expected = "欢迎使用Aspose OCR示例";
bool matches = ocrResult.Text.Trim() == expected;
Console.WriteLine($"Match with expected? {matches}");
```

Pokud je `matches` `false`, zvažte úpravu obrázku (např. zvýšení kontrastu) nebo povolení `ocrEngine.Options.UseAdvancedPreprocessing = true`.

## Závěr

Právě jste se naučili, jak **recognize chinese text** z JPG souboru pomocí Aspose OCR, a nyní víte, jak **extract text from image** v plně offline scénáři. Kompletní řešení — inicializace, načítání zdrojů, výběr jazyka a zpracování obrázku — se vejde do jediné, snadno spustitelné konzolové aplikace.

Co dál? Zkuste předat dávku obrázků stejnému enginu, experimentujte s různými jazykovými balíčky nebo integrujte OCR krok do ASP .NET Web API, aby uživatelé mohli nahrávat obrázky a okamžitě dostávat přeložený text. Možnosti jsou neomezené, když spojíte spolehlivé OCR s moderními .NET nástroji.

Šťastné programování a neváhejte zanechat komentář, pokud narazíte na potíže!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}