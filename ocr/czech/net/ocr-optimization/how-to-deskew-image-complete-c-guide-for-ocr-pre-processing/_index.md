---
category: general
date: 2026-03-20
description: Naučte se, jak vyrovnat obrázek a odstranit šum z obrázku pomocí Aspose
  OCR. Tento krok‑za‑krokem průvodce také ukazuje, jak předzpracovat obrázek pro OCR
  a zlepšit přesnost OCR.
draft: false
keywords:
- how to deskew image
- remove image noise
- preprocess image for OCR
- recognize text from image
- improve OCR accuracy
language: cs
og_description: Naučte se, jak vyrovnat obrázek a odstranit šum pomocí Aspose OCR.
  Zvyšte přesnost OCR během několika minut.
og_title: Jak narovnat obrázek – Kompletní průvodce C# pro předzpracování OCR
tags:
- OCR
- C#
- Image Processing
title: Jak vyrovnat obrázek – Kompletní průvodce C# pro předzpracování OCR
url: /cs/net/ocr-optimization/how-to-deskew-image-complete-c-guide-for-ocr-pre-processing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak vyrovnat obrázek – Kompletní C# průvodce pro předzpracování OCR

Už jste se někdy zamysleli nad tím, **jak vyrovnat obrázek** soubory, které vyšly ze skeneru pod podivným úhlem? Nejste v tom sami; mnoho vývojářů narazí na tento problém, když se snaží vložit fotografii do OCR enginu. Dobrou zprávou je, že s několika řádky C# a Aspose OCR můžete narovnat, odstranit šum a zvýšit kontrast v jedné přehledné pipeline—bez potřeby Photoshopu.

V tomto tutoriálu projdeme vše, co potřebujete vědět: od načtení nakloněného obrázku, přes **odstranění šumu z obrázku**, až po **předzpracování obrázku pro OCR**, a nakonec **rozpoznání textu z obrázku** s vysokým skóre **zlepšení přesnosti OCR**. Na konci budete mít připravenou konzolovou aplikaci, která promění nečistý sken na čistý, prohledávatelný text.

## Co budete potřebovat

- .NET 6 nebo novější (kód používá syntaxi `using var`, která je podporována od C# 8)
- Balíček NuGet Aspose OCR (`Aspose.OCR`) – nainstalujte pomocí `dotnet add package Aspose.OCR`
- Ukázkový obrázek, který je jak nakloněný, tak i šumivý (např. `skewed_noisy.png`)
- IDE nebo editor dle vašeho výběru (Visual Studio, VS Code, Rider… podle vás)

> **Tip:** Pokud nemáte ukázkový soubor, stačí otočit čistý snímek o několik stupňů a posypat jej “solí‑a‑pepřem” šumu pomocí editoru obrázků.  Pipeline funguje stejným způsobem.

## Krok 1: Jak vyrovnat obrázek pomocí filtru Deskew

Prvním krokem je opravit rotaci. Aspose poskytuje `DeskewFilter`, který dokáže automaticky detekovat úhly až do konfigurovatelného `MaxAngle`. Nastavení na **5°** je bezpečná výchozí hodnota pro většinu skenovaných dokumentů.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Filters;
using System.Drawing;   // For Image class

// Initialize the OCR engine – English is the most common language
using var ocrEngine = new OcrEngine
{
    Language = Language.English
};

// Build the preprocessing pipeline
var preprocessPipeline = new PreprocessPipeline()
    .Add(new DeskewFilter { MaxAngle = 5 })          // This is where we answer “how to deskew image”
    .Add(new DespeckleFilter { Strength = 2 })      // Next we’ll remove image noise
    .Add(new ContrastFilter { Level = 1.5 });        // Finally we boost contrast for OCR
```

**Proč je to důležité:**  
Pokud je text nakloněný, OCR algoritmus může špatně interpretovat znaky—např. „l“ se změní na „i“.  Tím, že nejprve **deskew** (vyrovnáte), poskytnete enginu rovnou plochu k práci.

## Krok 2: Odstranění šumu z obrázku pomocí Despeckle

Skeny z levných telefonů nebo starých skenerů často obsahují skvrny, které vypadají jako náhodné tečky. Tyto skvrny matí rozpoznávač znaků. `DespeckleFilter` vyhladí obrázek při zachování hran.

```csharp
// The DespeckleFilter is already part of the pipeline (see Step 1)
// Strength = 2 is a balanced setting; increase for very noisy pics
```

Pokud potřebujete **odstranit šum z obrázku** agresivněji, zvyšte `Strength` na 3 nebo 4—ale dejte pozor na ztrátu tenkých tahů.

## Krok 3: Předzpracování obrázku pro OCR – Zvýšení kontrastu

Skeny s nízkým kontrastem (světle šedá na bílém papíru) mohou způsobit, že OCR přehlédne slabé písmena. `ContrastFilter` rozšíří tonální rozsah, čímž udělá tmavé pixely tmavější a světlé pixely světlejší.

```csharp
// Contrast level of 1.5 is a good starting point.
// You can experiment with values between 1.0 (no change) and 2.0 (strong boost).
```

**Okrajový případ:** Pokud je váš zdrojový obrázek již vysokokontrastní, aplikace tohoto filtru může vymazat detaily. V takovém případě nastavte `Level` na `1.0` (prakticky jej vypnete).

## Krok 4: Načtení a vyčištění zdrojového obrázku

Nyní skutečně načteme obrázek a spustíme jej přes pipeline, kterou jsme právě sestavili.

```csharp
// Load the source image – replace the path with your own file location
var sourceImage = Image.FromFile("YOUR_DIRECTORY/skewed_noisy.png");

// Apply the entire preprocessing pipeline
var cleanedImage = preprocessPipeline.Apply(sourceImage);
```

> **Poznámka:** Metoda `Apply` vrací nový objekt `Image`; originál zůstává nedotčený. To usnadňuje porovnání „před“ a „po“, pokud chcete proces ladit.

## Krok 5: Rozpoznání textu z obrázku pomocí Aspose OCR

S rovnou, bezšumnou, vysokokontrastní fotografií v ruce ji nakonec předáme OCR enginu.

```csharp
// Perform OCR on the cleaned image
var ocrResult = ocrEngine.Recognize(cleanedImage);

// Output the recognized text to the console
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);
```

**Co byste měli vidět:** Konzole vypíše textový obsah původního skenu, obvykle s mnohem méně chybami než při přímém zadání surového souboru.

## Krok 6: Ověření a zlepšení přesnosti OCR

I když máte solidní pipeline, některé znaky mohou být stále špatně – zejména pokud je původní font neobvyklý. Zde je několik rychlých tipů, jak **zlepšit přesnost OCR**:

| Problém | Rychlé řešení |
|-------|-----------|
| Chybějící malá interpunkce | Přidejte `BinaryThresholdFilter` před krokem kontrastu |
| Smíšený jazyk (např. English + Spanish) | Nastavte `ocrEngine.Language = Language.English | Language.Spanish;` |
| Velmi tmavé pozadí | Před vyrovnáním invertujte obrázek (`new InvertFilter()`) |
| Velké dokumenty | Zpracovávejte stránky paralelně (`Parallel.ForEach`) pro zrychlení |

Experimentujte s pořadím filtrů; někdy aplikace **kontrastu** před **despeckle** přináší lepší výsledky u nízkokvalitních skenů.

## Kompletní funkční příklad

Níže je celý program, který můžete zkopírovat a vložit do nového konzolového projektu. Obsahuje všechny části, o kterých jsme mluvili, plus několik bezpečnostních kontrol.

```csharp
// File: Program.cs
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Filters;
using System;
using System.Drawing;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Initialize OCR engine (English language)
        // -------------------------------------------------
        using var ocrEngine = new OcrEngine
        {
            Language = Language.English
        };

        // -------------------------------------------------
        // 2️⃣ Build preprocessing pipeline:
        //    Deskew → Despeckle → Contrast Boost
        // -------------------------------------------------
        var preprocessPipeline = new PreprocessPipeline()
            .Add(new DeskewFilter { MaxAngle = 5 })          // how to deskew image
            .Add(new DespeckleFilter { Strength = 2 })      // remove image noise
            .Add(new ContrastFilter { Level = 1.5 });        // preprocess image for OCR

        // -------------------------------------------------
        // 3️⃣ Load the source image (adjust path as needed)
        // -------------------------------------------------
        const string imagePath = "YOUR_DIRECTORY/skewed_noisy.png";
        if (!System.IO.File.Exists(imagePath))
        {
            Console.WriteLine($"❌ File not found: {imagePath}");
            return;
        }

        var sourceImage = Image.FromFile(imagePath);

        // -------------------------------------------------
        // 4️⃣ Apply the pipeline → cleaned image
        // -------------------------------------------------
        var cleanedImage = preprocessPipeline.Apply(sourceImage);

        // -------------------------------------------------
        // 5️⃣ Recognize text (this is the “recognize text from image” step)
        // -------------------------------------------------
        var ocrResult = ocrEngine.Recognize(cleanedImage);

        // -------------------------------------------------
        // 6️⃣ Output the result
        // -------------------------------------------------
        Console.WriteLine("\n=== OCR Output ===\n");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Očekávaný výstup** (předpokládáme, že ukázkový obrázek obsahuje „Hello World!“):

```
=== OCR Output ===

Hello World!
```

Pokud vidíte nesrozumitelné znaky, dvakrát zkontrolujte pořadí pipeline nebo zvyšte `DespeckleFilter.Strength`.

## Závěr

Probrali jsme **jak vyrovnat obrázek**, **odstranit šum z obrázku**, **předzpracovat obrázek pro OCR**, a nakonec **rozpoznat text z obrázku** pomocí Aspose OCR—vše s ohledem na **zlepšení přesnosti OCR**. Kompletní, spustitelný příklad ukazuje každý krok v kontextu, takže jej můžete vložit do libovolného .NET projektu a okamžitě začít extrahovat text.

Jste připraveni na další výzvu? Zkuste rozšířit pipeline tak, aby zvládala více‑stránkové PDF, nebo experimentujte s jazykovými balíčky pro vícejazyčné dokumenty. Stejné koncepty platí—stačí vyměnit příznak `Language` a případně přidat `RotateFilter` pro stránky, které jsou vzhůru nohama.

Máte otázky nebo obtížný obrázek, který stále ne spolupracuje? Zanechte komentář níže a společně to vyřešíme. Šťastné kódování!

![how to deskew image example](/images/deskew-example.png "Illustration of how to deskew image using Aspose OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}