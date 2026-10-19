---
category: general
date: 2026-01-13
description: jak vyrovnat sklon obrazu a odstranit šum obrazu v C# – naučte se zvýšit
  kontrast obrazu, předzpracovat OCR obrazu a aplikovat více filtrů obrazu
draft: false
keywords:
- how to deskew image
- remove image noise
- increase image contrast
- preprocess image ocr
- multiple image filters
language: cs
og_description: jak vyrovnat zkosení obrázku a odstranit šum z obrázku v C# – naučte
  se zvýšit kontrast obrázku, předzpracovat OCR obrázku a použít více filtrů obrázku
og_title: Jak vyrovnat zkosený obrázek – Kompletní průvodce předzpracováním v C# pro
  OCR
tags:
- OCR
- C#
- Image Processing
title: jak vyrovnat obrázek – Kompletní průvodce předzpracováním v C# pro OCR
url: /cs/net/skew-angle-calculation/how-to-deskew-image-complete-c-pre-processing-guide-for-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# jak vyrovnat obrázek – Kompletní průvodce předzpracováním v C# pro OCR

Už jste se někdy zamýšleli nad **jak vyrovnat obrázek** před tím, než jej předáte OCR enginu? Nejste v tom sami. V mnoha reálných scénářích — naskenované smlouvy, účtenky nebo staré fotokopie — text leží pod mírným úhlem, obrázek je zrnitý a kontrast je nerovnoměrný. Dobrá zpráva? Několik řádků C# kódu může tento náklon narovnat, odstranit šum obrazu a zvýšit kontrast, čímž poskytne vašemu OCR pevný základ.

V tomto tutoriálu projdeme **kompletní, spustitelný příklad**, který vám přesně ukáže, jak vyrovnat obrázek, odstranit šum obrazu, zvýšit kontrast obrazu a poté spustit OCR pomocí Aspose.OCR. Na konci budete mít znovupoužitelnou pipeline, která aplikuje **více filtrů obrazu** v jediném, plynulém volání — žádné hádání není potřeba.

## Co budete potřebovat

- **.NET 6+** (nebo jakákoli novější verze .NET; API funguje stejně)
- **Aspose.OCR for .NET** NuGet balíček (`Aspose.OCR` a `Aspose.OCR.Filters`)
- Ukázkový naskenovaný obrázek (např. `skewed_noisy.png`), který vykazuje náklon, šum a nízký kontrast
- Vaše oblíbené IDE (Visual Studio, Rider, VS Code — vyberte si to, co vám vyhovuje)

Pokud už máte projekt nastavený, stačí přidat NuGet referenci:

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Filters
```

> **Tip:** Aspose nabízí bezplatnou zkušební verzi s omezeným počtem stránek — ideální pro vyzkoušení níže uvedeného kódu.

## Krok 1: Vytvoření instance OCR enginu

První věc, kterou uděláme, je vytvořit `OcrEngine`. Představte si ho jako mozek, který později přečte text. Není to nic složitého, ale je to základ pro vše, co následuje.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

class PreprocessDemo
{
    static void Main()
    {
        // Step 1: Initialize the OCR engine
        var ocrEngine = new OcrEngine();
```

> **Proč je to důležité:** Inicializace enginu jednou a jeho opakované používání pro mnoho obrázků eliminuje režii načítání jazykových dat při každém spuštění.

## Krok 2: Načtení surového naskenovaného obrázku

Dále načteme obrázek z disku. Metoda `OcrImage.FromFile` načte soubor do formátu, který Aspose dokáže manipulovat.

```csharp
        // Step 2: Load the raw scanned image (skewed, noisy, low‑contrast)
        var rawImage = OcrImage.FromFile(@"YOUR_DIRECTORY/skewed_noisy.png");
```

> **Hraniční případ:** Pokud je váš obrázek v nestandardním formátu (TIFF, BMP), Aspose jej stále zvládne, ale pro konzistenci můžete nejprve převést na PNG.

## Krok 3: Vytvoření pipeline předzpracování (Deskew → Denoise → Contrast)

Zde odpovídáme na hlavní otázku **jak vyrovnat obrázek**, zároveň **odstranit šum obrazu** a **zvýšit kontrast obrazu**. Fluent API od Aspose nám umožňuje řetězit filtry dohromady, takže kód čte jako věta.

```csharp
        // Step 3: Apply Deskew, Denoise, and Contrast filters in one pipeline
        var processedImage = rawImage
            .ApplyFilter(new DeskewFilter())      // Corrects rotation
            .ApplyFilter(new DenoiseFilter())     // Reduces grainy artifacts
            .ApplyFilter(new ContrastFilter());   // Boosts foreground/background separation
```

### Co každý filtr dělá

| Filter | Purpose | Typical Impact |
|--------|---------|----------------|
| **DeskewFilter** | Detekuje úhel textových řádků a otočí obrázek tak, aby byly vodorovné. | Odstraňuje náklon, který zmátne OCR, často snižuje chybovost o 30‑50 %. |
| **DenoiseFilter** | Používá vyhlazovací algoritmus, který zachovává hrany a odstraňuje náhodný šum pixelů. | Čistí naskenované účtenky nebo fotografie při slabém osvětlení, což zlepšuje čitelnost znaků. |
| **ContrastFilter** | Roztahuje histogram tak, že tmavé oblasti jsou tmavší a světlé oblasti jsou světlejší. | Zlepšuje rozdíl mezi textem a pozadím, což je zvláště užitečné u vybledlých dokumentů. |

> **Proč je řadit:** Nejprve vyrovnání zajišťuje, že odšumovač pracuje s korektně orientovaným obrázkem; zvýšení kontrastu na závěr nechává vyčištěný text vyniknout pro OCR engine.

## Krok 4: Provedení OCR na zpracovaném obrázku

Nyní, když je obrázek rovný, čistý a s vysokým kontrastem, předáme jej OCR enginu. Použijeme anglická jazyková data, ale Aspose podporuje více než 150 jazyků.

```csharp
        // Step 4: Recognize text using the English language pack
        var ocrResult = ocrEngine.Recognize(processedImage, OcrLanguage.English);
```

Pokud potřebujete jiný jazyk, stačí nahradit `OcrLanguage.English` odpovídající hodnotou enumu (např. `OcrLanguage.Spanish`).

## Krok 5: Výstup rozpoznaného textu

Nakonec výsledek vypíšeme do konzole. Ve skutečné aplikaci můžete zapisovat do souboru, databáze nebo předávat text do následných NLP pipeline.

```csharp
        // Step 5: Display the recognized text
        System.Console.WriteLine(ocrResult.Text);
    }
}
```

### Očekávaný výstup

Spuštěním celého programu na typické nakloněné účtence získáte něco jako:

```
Invoice #12345
Date: 2025‑12‑31
Total: $1,234.56
Thank you for your business!
```

Pokud výstup vypadá poškozeně, zkontrolujte původní obrázek — přílišná neostrost nebo extrémní temnota mohou vyžadovat další předzpracování (např. `SharpenFilter`).

![příklad jak vyrovnat obrázek](images/deskewed_example.png "jak vyrovnat obrázek – před a po zpracování")

*Obrázek výše ukazuje původní nakloněný sken vlevo a opravenou, odšumovanou, vysokokontrastní verzi vpravo.*

## Další tipy a běžné úskalí

### 1. Když je úhel náklonu extrémní

Pokud je dokument natočen o více než 30°, může mít `DeskewFilter` potíže. V takovém případě obrázek předem otočte ručně:

```csharp
var manuallyRotated = rawImage.Rotate(45); // rotates 45 degrees clockwise
var processed = manuallyRotated.ApplyFilter(new DeskewFilter());
```

### 2. Práce s barevnými obrázky

Filtry interně pracují s odstíny šedi, ale můžete vynutit konverzi:

```csharp
var grayImage = rawImage.ConvertToGrayscale();
var processed = grayImage.ApplyFilter(new DeskewFilter());
```

### 3. Ladění síly odšumu

`DenoiseFilter` přijímá volitelný parametr `strength` (0‑100). Vyšší hodnoty odstraní více šumu, ale mohou rozmazat jemné detaily.

```csharp
.ApplyFilter(new DenoiseFilter(strength: 70))
```

### 4. Použití více filtrů obrazu nad rámec základů

Aspose nabízí mnoho dalších filtrů: `SharpenFilter`, `BinarizeFilter`, `ResizeFilter` a další. Můžete je kombinovat a vytvořit si vlastní pipeline, která odpovídá vašemu konkrétnímu typu dokumentu.

```csharp
var processed = rawImage
    .ApplyFilter(new DeskewFilter())
    .ApplyFilter(new DenoiseFilter())
    .ApplyFilter(new BinarizeFilter())
    .ApplyFilter(new SharpenFilter());
```

## Kompletní funkční příklad (připravený ke kopírování)

Níže je celý program, připravený k vložení do konzolového projektu.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

class PreprocessDemo
{
    static void Main()
    {
        // Initialize OCR engine
        var ocrEngine = new OcrEngine();

        // Load the original scanned image
        var rawImage = OcrImage.FromFile(@"YOUR_DIRECTORY/skewed_noisy.png");

        // Build preprocessing pipeline: Deskew → Denoise → Contrast
        var processedImage = rawImage
            .ApplyFilter(new DeskewFilter())
            .ApplyFilter(new DenoiseFilter())
            .ApplyFilter(new ContrastFilter());

        // Run OCR using English language
        var ocrResult = ocrEngine.Recognize(processedImage, OcrLanguage.English);

        // Output recognized text
        System.Console.WriteLine(ocrResult.Text);
    }
}
```

Spusťte program pomocí `dotnet run`. Pokud je vše nastaveno správně, konzole zobrazí čistý, čitelný text extrahovaný z původně nakloněného,umového obrázku.

## Závěr

Právě jsme probrali **jak vyrovnat obrázek** v C# a zároveň **odstranit šum obrazu**, **zvýšit kontrast obrazu** a **předzpracovat OCR obrázku** řetězcem **více filtrů obrazu**. Hlavní ponaučení je, že dobře uspořádaná pipeline předzpracování může dramaticky zlepšit přesnost OCR — často promění sotva čitelný sken na dokonale čitelný text.

Jste připraveni na další krok? Zkuste vyměnit `ContrastFilter` za `BinarizeFilter` a podívejte se, jak binární (černobílá) konverze ovlivní výsledky, nebo experimentujte s `ResizeFilter`, abyste do enginu předali obrázek vyššího rozlišení. Stejný vzor platí bez ohledu na to, které filtry zvolíte, takže máte flexibilní základ pro všechny budoucí OCR projekty.

Máte otázky ohledně práce s PDF, vícejazyčného OCR nebo integrace do ASP.NET API? Zanechte komentář níže a šťastné programování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}