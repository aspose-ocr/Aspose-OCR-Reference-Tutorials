---
category: general
date: 2026-02-09
description: Naučte se, jak předzpracovat OCR obrázku a rozpoznat text na obrázku
  pomocí Aspose OCR. Snižte šum na obrázku, přidejte filtry a během několika minut
  extrahujte čistý text.
draft: false
keywords:
- preprocess image OCR
- recognize text image
- extract plain text
- reduce image noise
- how to add filters
language: cs
og_description: Rychle předzpracujte OCR obrázku. Tento návod ukazuje, jak přidat
  filtry, snížit šum obrazu a extrahovat prostý text z jakéhokoli obrázku.
og_title: Předzpracování OCR obrázku v C# – krok za krokem tutoriál
tags:
- OCR
- C#
- Image Processing
title: Předzpracování obrazu pro OCR v C# – Kompletní průvodce s filtry
url: /cs/net/ocr-optimization/preprocess-image-ocr-in-c-complete-guide-with-filters/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Předzpracování OCR obrazu v C# – Kompletní průvodce s filtry

Už jste někdy měli potíže s **předzpracováním OCR obrazu**, protože vaše skeny jsou šikmé, zrnitější nebo prostě těžko čitelné? Nejste v tom sami. V mnoha reálných projektech může roztřesená fotografie účtenky nebo šumová naskenovaná formulář způsobit, že OCR engine vypíše nesmysly místo užitečných dat.  

Dobrá zpráva? Můžete tyto obrázky vyčistit ještě před tím, než je předáte engine, a výsledek je dramaticky vyšší přesnost při **rozpoznávání textu z obrazu**. V tomto tutoriálu vás provede přesně **jak přidat filtry**, snížit šum a nakonec **extrahovat prostý text** pomocí Aspose.OCR v C#.

Probereme vše, co potřebujete – od instalace knihovny po spuštění kódu a ověření výstupu – abyste mohli okamžitě zkopírovat a vložit funkční řešení.

---

## Co budete potřebovat

- **.NET 6+** (nebo jakýkoli recentní .NET runtime; API funguje stejně)
- **Aspose.OCR for .NET** NuGet balíček  
  ```bash
  dotnet add package Aspose.OCR
  ```
- Vzorek obrázku, který trpí rotací, šumem nebo nízkým kontrastem (např. `skewed_noisy.jpg`)
- IDE nebo editor, který máte rádi (Visual Studio, VS Code, Rider — vyberte si podle libosti)

To je vše. Žádné extra nativní knihovny, žádné těžké frameworky pro zpracování obrazu. Aspose přichází s potřebnými filtry.

## Krok 1 – Vytvoření instance OCR engine  

První věc, kterou uděláte, je vytvořit `OcrEngine`. Představte si ho jako mozek, který později přečte znaky poté, co jsme obrázek vyčistili.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Filters;

class FilterExample
{
    static void Main()
    {
        // Initialize the OCR engine – this object will hold our filters and settings
        OcrEngine ocrEngine = new OcrEngine();
```

> **Proč je to důležité:** Engine obsahuje **pipeline předzpracování**. Přidání filtrů později je automaticky použije při každém volání `Recognize`.

## Krok 2 – Přidání filtrů pro snížení šumu obrazu a zlepšení čitelnosti  

Nyní **přidáváme filtry**. Každý filtr řeší konkrétní nedostatek:

| Filtr | Co opravuje | Typické použité hodnoty |
|--------|---------------|---------------------|
| `DeskewFilter` | Otočený text (skew) | `MaxAngle = 12` (stupňů) |
| `DenoiseFilter` | Náhodné skvrny, zrnitost | `Strength = 0.6` (0‑1) |
| `ContrastBoostFilter` | Bledé písmo | `Level = 1.3` (1‑2) |
| `BinarizeAdaptiveFilter` | Nerovnoměrné osvětlení | výchozí hodnoty fungují dobře |

```csharp
        // Step 2: Add preprocessing filters to improve image quality
        //   • Deskew to correct rotation (max 12°)
        //   • Denoise to reduce noise (strength 0.6)
        //   • Contrast boost to enhance visibility (level 1.3)
        //   • Adaptive binarization for better binarization
        ocrEngine.Preprocessing.Add(new DeskewFilter { MaxAngle = 12 });
        ocrEngine.Preprocessing.Add(new DenoiseFilter { Strength = 0.6 });
        ocrEngine.Preprocessing.Add(new ContrastBoostFilter { Level = 1.3 });
        ocrEngine.Preprocessing.Add(new BinarizeAdaptiveFilter());
```

> **Tip:** Pokud jsou vaše obrázky již narovnané, můžete krok deskew přeskočit. Odstranění zbytečných filtrů urychlí zpracování.

## Krok 3 – Načtení obrázku, který chcete zpracovat  

Dále řekneme engine, který obrázek má vyčistit. `ImageStream.FromFile` načte soubor do formátu, který OCR engine rozumí.

```csharp
        // Step 3: Load the image that needs OCR processing
        ImageStream image = ImageStream.FromFile(@"YOUR_DIRECTORY/skewed_noisy.jpg");
```

> **Okrajový případ:** Při práci se streamy pocházejícími z webového API nahraďte `FromFile` za `FromStream`, abyste se vyhnuli přístupu k souborovému systému.

## Krok 4 – Spuštění OCR engine a rozpoznání textu z obrazu  

Nyní se děje magie. Engine aplikuje všechny přidané filtry a poté provede rozpoznání znaků.

```csharp
        // Step 4: Run the OCR engine on the prepared image
        OcrResult ocrResult = ocrEngine.Recognize(image);
```

> **Proč to funguje:** Pipeline předzpracování zajišťuje, že obrázek předaný rozpoznávači je co nejčistší, což přímo zvyšuje přesnost **rozpoznání textu z obrazu**.

## Krok 5 – Extrahování prostého textu a jeho zobrazení  

Nakonec získáme výsledek jako prostý text a vypíšeme jej do konzole. Toto je část **extrahování prostého textu** pracovního postupu.

```csharp
        // Step 5: Output the recognized plain text
        Console.WriteLine(ocrResult.PlainText);
    }
}
```

### Očekávaný výstup

Pokud `skewed_noisy.jpg` obsahuje jednoduchý řádek faktury jako `Total: $123.45`, měli byste vidět:

```
Total: $123.45
```

I když byl původní soubor otočen o 10°, měl skvrny a nízký kontrast, filtry by jej měly dostatečně vyčistit, aby OCR engine jej mohl správně přečíst.

## Vizualní přehled  

Níže je rychlá ilustrace pipeline předzpracování. Diagram není nutný pro spuštění kódu, ale pomáhá vizualizovat tok.

![pipeline předzpracování OCR](https://example.com/ocr-pipeline.png "pipeline předzpracování OCR")

*Alt text: pipeline předzpracování OCR ukazující kroky deskew, denoise, zvýšení kontrastu a adaptivní binarizaci.*

## Časté otázky a úskalí  

- **Co když je výsledek OCR stále nečitelný?**  
  Zkuste zvýšit `DenoiseFilter.Strength` na `0.8` nebo snížit `ContrastBoostFilter.Level` na `1.1`. Přílišné zvýšení kontrastu může někdy vytvořit halo, které zmátne rozpoznávač.

- **Mohu přidat vlastní vlastní filtr?**  
  Ano. Aspose.OCR vám umožní implementovat `IFilter` a vložit jej do `ocrEngine.Preprocessing`. Jedná se o pokročilé téma, ale je užitečné, když máte specifické požadavky na předzpracování.

- **Funguje to s PDF?**  
  Pouze pokud nejprve převedete každou stránku PDF na obrázek (např. pomocí Aspose.PDF). Jakmile máte bitmapu, použije se stejný řetězec filtrů.

- **Je knihovna thread‑safe?**  
  Instance `OcrEngine` **není** thread‑safe. Vytvořte samostatný engine pro každé vlákno nebo obalte volání zámkem.

## Rozšíření příkladu  

Nyní, když máte solidní základ, zvažte následující kroky:

1. **Dávkové zpracování** – Procházet složku s obrázky, aplikovat stejný řetězec filtrů a zapisovat každý výsledek do souboru `.txt`.  
2. **Jazykové balíčky** – Pokud potřebujete rozpoznávat francouzštinu nebo němčinu, načtěte odpovídající jazyková data pomocí `ocrEngine.Language = "fra"` (nebo `"deu"`).  
3. **Oblast zájmu (ROI)** – Použijte `ocrEngine.Recognize(image, new Rectangle(x, y, width, height))` k zaměření na konkrétní oblast, což může urychlit zpracování velkých skenů.

## Závěr  

V tomto průvodci **předzpracujeme OCR obrazu** přidáním série vestavěných filtrů, poté **rozpoznáme text z obrazu** a nakonec **extrahujeme prostý text** z šumu a šikmého obrázku. Kompletní spustitelný kód je výše a můžete jej přizpůsobit libovolnému projektu v C#, který potřebuje spolehlivé výsledky OCR.  

Pamatujte, klíč k dobrému OCR není jen výkonný engine – je to čistý vstup. Snížením šumu obrazu a správným zarovnáním textu dáváte rozpoznávači nejlepší možnou šanci na úspěch.  

Neváhejte experimentovat s hodnotami filtrů, zkoušet různé formáty obrázků nebo kombinovat tento přístup s dalšími knihovnami Aspose. Pokud narazíte na problém, zanechte komentář níže nebo si prohlédněte oficiální dokumentaci Aspose pro podrobnější informace o jednotlivých třídách filtrů. Šťastné programování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}