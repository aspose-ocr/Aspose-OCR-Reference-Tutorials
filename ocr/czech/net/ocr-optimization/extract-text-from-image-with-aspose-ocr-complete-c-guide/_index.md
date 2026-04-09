---
category: general
date: 2026-04-08
description: Extrahujte text z obrázku pomocí Aspose OCR v C#. Naučte se, jak předzpracovat
  obrázek pro OCR a jak předzpracovat obrázek, aby se zvýšila přesnost.
draft: false
keywords:
- extract text from image
- preprocess image for ocr
- how to preprocess image
- Aspose OCR C#
- image preprocessing techniques
language: cs
og_description: Extrahujte text z obrázku pomocí Aspose OCR v C#. Tento průvodce ukazuje,
  jak předzpracovat obrázek pro OCR a jak předzpracovat obrázek pro dosažení nejlepších
  výsledků.
og_title: Extrahování textu z obrázku pomocí Aspose OCR – Kompletní průvodce C#
tags:
- C#
- OCR
- Aspose
- Image Processing
title: Extrahovat text z obrázku pomocí Aspose OCR – Kompletní průvodce C#
url: /cs/net/ocr-optimization/extract-text-from-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahování textu z obrázku pomocí Aspose OCR – Kompletní průvodce v C#

Už jste někdy potřebovali **extrahovat text z obrázku**, ale výsledky byly plné chyb? Nejste v tom sami — většina vývojářů narazí na tento problém, když je zdrojový obrázek nakřivený, šumivý nebo má nízký kontrast. Dobrou zprávou je, že krátká předzpracovatelská rutina může proměnit nejistý snímek v čistý zdroj pro OCR a Aspose OCR to celé udělá hračkou.

V tomto tutoriálu projdeme reálný příklad, který ukazuje **jak předzpracovat obrázek pro OCR** pomocí vestavěných filtrů Aspose OCR, a poté **extrahovat text z obrázku** pomocí několika řádků C#. Na konci budete mít připravený spustitelný program, pochopíte, proč je každý filtr důležitý, a budete vědět, jak si pipeline přizpůsobit pro vlastní okrajové případy.

## Co budete potřebovat

- .NET 6.0 nebo novější (kód také funguje na .NET Framework 4.7+)
- NuGet balíček Aspose.OCR (`Install-Package Aspose.OCR`)
- Ukázkový obrázek, který je nakřivený, šumivý nebo má nízký kontrast (např. `skewed_noisy.jpg`)
- Jakékoliv IDE, které vám vyhovuje — Visual Studio, Rider nebo VS Code jsou v pořádku

Žádné extra nativní knihovny, žádné webové služby, jen čisté C#.

## Krok 1: Nastavení OCR enginu — Výchozí bod pro extrahování textu

Nejprve vytvořte instanci `OcrEngine` a řekněte mu, jaký jazyk má hledat. Angličtina je nejčastější, ale můžete zaměnit `"en"` za `"fr"`, `"de"` a podobně.

```csharp
using Aspose.Ocr;
using Aspose.Ocr.Filters;
using System;

public static class ImageOcrDemo
{
    public static void PreprocessAndOcr()
    {
        // 1️⃣ Initialize the OCR engine – this is where we define the language.
        var ocrEngine = new OcrEngine { Language = "en" };
```

**Proč je to důležité:** Engine obsahuje interní slovníky a jazykově specifické heuristiky. Pokud jazyk nenastavíte, Aspose použije výchozí angličtinu, ale explicitní nastavení zabrání překvapením, když později změníte locale.

## Krok 2: Sestavení předzpracovatelské pipeline — Jak předzpracovat obrázek pro nejlepší výsledky

Nyní přidáme filtry. Představte si je jako mini‑sadu pro úpravu fotografií, která běží automaticky před krokem OCR. Níže uvedené tři filtry pokrývají nejčastější problémy:

| Filtr | Co opravuje | Kdy použít |
|--------|---------------|----------------|
| `DeskewFilter` | Otočí obrázek zpět do vodorovné polohy | Obrázky pořízené pod úhlem |
| `DenoiseFilter` | Snižuje náhodné skvrny a zrnitost | Fotky za slabého osvětlení nebo naskenované dokumenty |
| `ContrastStretchFilter` | Zvyšuje kontrast, aby tmavý text vynikl | Vybledlé tisky nebo vypláchnuté screenshoty |

```csharp
        // 2️⃣ Add preprocessing steps – this is the core of “how to preprocess image”.
        ocrEngine.Preprocess.Add(new DeskewFilter());               // correct skew
        ocrEngine.Preprocess.Add(new DenoiseFilter());             // reduce noise
        ocrEngine.Preprocess.Add(new ContrastStretchFilter());     // enhance contrast
```

**Tip:** Pořadí má význam. Nejprve Deskew, pak Denoise a nakonec ContrastStretch. Pokud je obrátíte, můžete místo odstranění šumu jen zesílit.

## Krok 3: Spuštění OCR — Konečně extrahovat text z obrázku

S připravenou pipeline předáte enginu cestu k vašemu obrázku. Aspose automaticky použije filtry a poté spustí rozpoznávací algoritmus.

```csharp
        // 3️⃣ Recognize text from the pre‑processed image.
        var ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/skewed_noisy.jpg");
```

Pokud soubor není nalezen, získáte jasnou `FileNotFoundException`. Proto doporučujeme během vývoje používat absolutní cesty a v produkci přejít na relativní cesty nebo konfigurační hodnoty.

## Krok 4: Zobrazení výsledku — Podívejte se, co jste získali

Objekt `OcrResult` obsahuje surový text, skóre důvěry a dokonce ohraničující rámečky každého slova. Pro rychlou ukázku jednoduše vypíšeme text do konzole.

```csharp
        // 4️⃣ Output the extracted text.
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

Po spuštění programu byste měli vidět něco jako:

```
=== OCR Output ===
Invoice Number: 2023-0456
Date: 03/15/2024
Total: $1,234.56
```

Pokud výstup vypadá poškozeně, zkontrolujte kvalitu obrázku nebo vyzkoušejte další filtry (např. `BinarizationFilter` pro binární obrázky).

## Kompletní funkční příklad — Zkopírujte, vložte a spusťte

Níže je kompletní, samostatný program. Stačí nahradit `YOUR_DIRECTORY/skewed_noisy.jpg` skutečnou cestou k vašemu testovacímu obrázku.

```csharp
using Aspose.Ocr;
using Aspose.Ocr.Filters;
using System;

public static class ImageOcrDemo
{
    public static void Main()
    {
        PreprocessAndOcr();
    }

    public static void PreprocessAndOcr()
    {
        // Step 1: Create OCR engine and set language
        var ocrEngine = new OcrEngine { Language = "en" };

        // Step 2: Build preprocessing pipeline
        ocrEngine.Preprocess.Add(new DeskewFilter());               // correct skew
        ocrEngine.Preprocess.Add(new DenoiseFilter());             // reduce noise
        ocrEngine.Preprocess.Add(new ContrastStretchFilter());     // enhance contrast

        // Step 3: Recognize text from the pre‑processed image
        var ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/skewed_noisy.jpg");

        // Step 4: Show the extracted text
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Očekávaný výstup** — Konzole vytiskne čistý textový řetězec toho, co je na obrázku. Pokud obrázek obsahuje jednoduchý nápis „OpenAI“, zobrazí se přesně toto slovo, bez dalších znaků.

## Okrajové případy a úprava pipeline

### 1️⃣ Velmi tmavé obrázky

Pokud filtr kontrastu nestačí, přidejte na začátek `BrightnessCorrectionFilter`:

```csharp
ocrEngine.Preprocess.Add(new BrightnessCorrectionFilter(30)); // increase brightness by 30%
```

### 2️⃣ Vícejazyčné dokumenty

Nastavte `Language = "en+fr"` (Aspose podporuje čárkou oddělené kódy jazyků) a přidejte `LanguageDetectionFilter`, pokud chcete, aby engine automaticky detekoval jazyk.

### 3️⃣ Velké PDF převedené na obrázky

Zpracování tisícstránkového PDF po jednom obrázku může být pomalé. Použijte `Parallel.ForEach` pro paralelní OCR na více obrázcích, ale pamatujte, že `OcrEngine` není thread‑safe — vytvořte samostatnou instanci pro každý vlákno.

```csharp
Parallel.ForEach(imagePaths, path =>
{
    var engine = new OcrEngine { Language = "en" };
    // add same filters...
    var result = engine.RecognizeImage(path);
    // store result...
});
```

### 4️⃣ Získání ohraničujících rámečků

Pokud potřebujete polohu každého slova (např. pro zvýraznění), podívejte se na `ocrResult.Regions`. Každý region obsahuje souřadnice `Rectangle`, které můžete předat do UI overlay.

```csharp
foreach (var region in ocrResult.Regions)
{
    Console.WriteLine($"{region.Text} at {region.Bounds}");
}
```

## Časté úskalí (a jak se jim vyhnout)

- **Přeskočení kroku Deskew** — I 2‑stupňové naklonění může snížit důvěru o 20 %. Vždy přidejte `DeskewFilter`, pokud zdroj není perfektně zarovnán.
- **Používání JPEG s vysokou kompresí** — Artefakty komprese vypadají jako šum; přepněte na PNG nebo TIFF pro lepší OCR.
- **Hardcodování cest** — Relativní cesty fungují lokálně, ale v CI/CD pipeline budete chtít číst umístění obrázku z konfigurace nebo environmentálních proměnných.

## Testování vašeho nastavení

1. Spusťte program s čistým, vysokokontrastním obrázkem. Měli byste získat téměř dokonalý text.
2. Nahraďte jej šumivou, nakřivenou fotografií. Ověřte, že výstup se zlepší po přidání tří filtrů.
3. Experimentujte tím, že postupně odeberete jeden filtr, a sledujte dopad — to vám pomůže pochopit, *proč* je každý krok důležitý.

## Závěr

Ukázali jsme, jak **extrahovat text z obrázku** pomocí Aspose OCR, a představili praktický způsob **předzpracování obrázku pro OCR**, který funguje ve většině reálných scénářů. Řetězením `DeskewFilter`, `DenoiseFilter` a `ContrastStretchFilter` poskytnete enginu čisté plátno, což dramaticky zvyšuje přesnost.

Odtud můžete zkoumat pokročilejší filtry, pracovat s více stránkovými dokumenty nebo integrovat OCR výsledky do vyhledávacího indexu. Ať už zvolíte cokoli, základní vzorec — inicializace, předzpracování, rozpoznání a využití — zůstává stejný.

Jste připraveni posunout se dál? Vyzkoušejte `BinarizationFilter` pro černobílé skeny, nebo napojte výstup do databáze pro prohledávatelné PDF. Šťastné programování a ať každý obrázek, který pošlete do Aspose, vrátí ostrý, čitelný text!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}